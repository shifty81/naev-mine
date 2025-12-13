# SubSpace Technical Architecture

## Overview

SubSpace is built on the Naev game engine, which provides a solid foundation for 2D space simulation. This document outlines the technical architecture of both the inherited Naev systems and planned SubSpace enhancements.

## Engine Foundation (Naev)

### Core Technologies

#### Programming Languages
- **C**: Core engine, physics, rendering (~70% of codebase)
- **Rust**: Modern components, safety-critical systems (~20% of codebase)
- **Lua**: Scripting, missions, AI, game logic (~10% of codebase)

#### Graphics & Audio
- **OpenGL 3.3+**: Graphics rendering
- **SDL3**: Window management, input, audio
- **OpenAL**: 3D audio positioning
- **FreeType2**: Font rendering

#### Data & Storage
- **PhysFS**: Virtual file system
- **libxml2**: XML data parsing
- **PCRE2**: Regular expressions
- **cmark**: Markdown rendering

#### Mathematics & Physics
- **OpenBLAS**: Linear algebra
- **SuiteSparse**: Sparse matrix operations
- **GLPK**: Linear programming for optimization

#### Networking
- **ENet**: Reliable UDP networking (foundation for multiplayer)

### Architecture Layers

```
┌─────────────────────────────────────────────────┐
│         Game Logic Layer (Lua Scripts)          │
│  Missions, Events, AI, Factions, Economy       │
└─────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────┐
│      Scripting Interface Layer (C/Rust)         │
│  Lua bindings, Script execution, API surface    │
└─────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────┐
│        Core Game Engine (C/Rust)                │
│  Physics, Rendering, Audio, Input, Systems      │
└─────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────┐
│      Platform Layer (SDL3, OpenGL, etc.)        │
│  OS abstraction, Graphics API, Audio API        │
└─────────────────────────────────────────────────┘
```

## Current System Architecture

### Subsystems

#### 1. Rendering System
- **Location**: `src/opengl*.c`, `src/renderer/`
- **Technology**: OpenGL 3.3, custom shader system
- **Features**:
  - Particle effects
  - Sprite rendering
  - Shader-based effects
  - Background rendering (nebulae, stars)
  - Trail effects

#### 2. Physics System
- **Location**: `src/physics/`, `src/physics.c`
- **Features**:
  - 2D space physics
  - Collision detection
  - Projectile simulation
  - Ship movement and dynamics

#### 3. AI System
- **Location**: `src/ai.c`, `dat/ai/`
- **Features**:
  - Behavior trees
  - Fleet coordination
  - Combat tactics
  - Trading behaviors
  - Pathfinding

#### 4. Mission System
- **Location**: `src/mission.c`, `dat/missions/`
- **Features**:
  - Lua-scripted missions
  - Event system
  - Conditional triggers
  - Reward system

#### 5. Economy System
- **Location**: `src/economy.c`, `dat/commodities/`
- **Features**:
  - Supply/demand simulation
  - Dynamic pricing
  - Trade route optimization
  - Commodity system

#### 6. Save System
- **Location**: `src/save.c`
- **Features**:
  - XML-based save files
  - Version migration
  - Compression
  - Integrity checks

#### 7. UI System
- **Location**: `src/toolkit.c`, `src/tk/`
- **Features**:
  - Widget-based UI
  - Modal dialogs
  - Custom rendering
  - Input handling

## SubSpace Enhancements

### New Systems to Implement

#### 1. SubSpace Travel System

**Location**: `src/subspace/` (new)

**Components**:
- `subspace_manager.c` - Core SubSpace logic
- `subspace_gates.c` - Gate management
- `subspace_drive.c` - Drive mechanics
- `subspace_hazards.c` - Environmental effects
- `subspace_render.c` - Visual effects

**Architecture**:
```c
// SubSpace state machine
typedef enum {
    SUBSPACE_NORMAL,      // Normal space
    SUBSPACE_ENTERING,    // Transition to SubSpace
    SUBSPACE_TRANSIT,     // Traveling in SubSpace
    SUBSPACE_EXITING,     // Transition to normal
    SUBSPACE_EMERGENCY    // Emergency exit
} SubSpaceState;

// SubSpace context
typedef struct {
    SubSpaceState state;
    double entry_time;
    Vector2d destination;
    double stability;
    double energy_drain;
    // Hazards, effects, etc.
} SubSpaceContext;
```

**Integration Points**:
- Physics system (modified movement)
- Rendering system (special effects)
- UI system (SubSpace HUD elements)
- Save system (SubSpace state persistence)

#### 2. Multiplayer System

**Location**: `src/multiplayer/` (new)

**Components**:
- `mp_server.c` - Server logic
- `mp_client.c` - Client logic
- `mp_sync.c` - State synchronization
- `mp_protocol.c` - Network protocol
- `mp_lobby.c` - Lobby system

**Architecture**:
```
Client-Server Model:
┌──────────┐         ┌──────────┐         ┌──────────┐
│ Client A │ ←─────→ │  Server  │ ←─────→ │ Client B │
└──────────┘         └──────────┘         └──────────┘
                            │
                     ┌──────┴──────┐
                     ↓             ↓
              Game State     Authority
              Database       System
```

**Technology**:
- ENet for networking (already available)
- Snapshot interpolation
- Client prediction
- Server reconciliation

**Challenges**:
- State synchronization (large number of entities)
- Latency compensation
- Anti-cheat measures
- Server scaling

#### 3. Territory Control System

**Location**: `src/territory/` (new)

**Components**:
- `territory_manager.c` - Territory logic
- `territory_factions.c` - Player faction system
- `territory_influence.c` - Influence calculation
- `territory_combat.c` - Territory warfare

**Data Structure**:
```c
typedef struct {
    int system_id;
    int controller_faction;
    double influence[MAX_FACTIONS];
    Station** stations;
    int num_stations;
    TerritoryState state;
} TerritoryData;
```

**Integration**:
- Faction system (extended)
- Combat system (territory impact)
- Economy system (trade routes)
- Mission system (territory missions)

#### 4. Crafting System

**Location**: `src/crafting/` (new)

**Components**:
- `craft_manager.c` - Crafting logic
- `craft_blueprints.c` - Blueprint system
- `craft_resources.c` - Resource management
- `craft_production.c` - Manufacturing

**Database Schema**:
```lua
-- Blueprint definition (Lua data)
blueprint = {
    id = "custom_laser_mk1",
    type = "weapon",
    requirements = {
        skill_level = 5,
        blueprints = {"laser_base", "advanced_focusing"}
    },
    materials = {
        {resource = "refined_metal", amount = 50},
        {resource = "electronic_parts", amount = 20},
        {resource = "energy_crystals", amount = 5}
    },
    production_time = 3600, -- seconds
    result = "custom_laser"
}
```

#### 5. Enhanced AI System

**Location**: `src/ai/` (extended from `src/ai.c`)

**Enhancements**:
- Learning algorithms (basic ML)
- Improved pathfinding (A* with dynamic obstacles)
- Fleet coordination (formation AI)
- Economic AI (market manipulation)
- Adaptive difficulty

**Architecture**:
```
Traditional AI → Enhanced AI
Behavior Trees → Utility AI + Behavior Trees
Static → Dynamic learning
Individual → Coordinated fleets
Scripted → Emergent behaviors
```

### Database Extensions

#### New Data Files

**SubSpace Configuration**: `dat/subspace/`
```
subspace_gates.xml     - Gate definitions
subspace_hazards.xml   - Hazard types
subspace_effects.xml   - Visual effects
```

**Territory Data**: `dat/territory/`
```
territories.xml        - Territory definitions
influence_rules.xml    - Influence calculations
control_benefits.xml   - Control bonuses
```

**Crafting Data**: `dat/crafting/`
```
blueprints.xml        - Blueprint definitions
resources.xml         - Resource types
production.xml        - Production rules
```

**Multiplayer Config**: `dat/multiplayer/`
```
server_config.xml     - Server settings
sync_rules.xml        - Sync configuration
lobbies.xml           - Lobby definitions
```

## Data Flow

### Game Loop

```
┌─────────────────────────────────────┐
│         Input Processing            │
│  Keyboard, Mouse, Joystick, Network │
└────────────────┬────────────────────┘
                 ↓
┌─────────────────────────────────────┐
│          Update Logic               │
│  Physics, AI, Scripts, Systems      │
└────────────────┬────────────────────┘
                 ↓
┌─────────────────────────────────────┐
│          Render Frame               │
│  OpenGL, Particles, UI              │
└────────────────┬────────────────────┘
                 ↓
┌─────────────────────────────────────┐
│        Audio Processing             │
│  Sound effects, Music, 3D audio     │
└─────────────────────────────────────┘
```

### SubSpace Game Loop Integration

```
Normal Loop:
Input → Update → Render → Audio

With SubSpace:
Input → SubSpace Check → Update* → Render* → Audio
                ↓
         SubSpace Systems:
         - Transit simulation
         - Hazard processing
         - Special effects
         - Modified physics
         
*Modified based on SubSpace state
```

## Performance Considerations

### Current Performance Profile
- **Target FPS**: 60+
- **Physics Updates**: 60 Hz
- **Max Ships**: ~500 simultaneous
- **Memory Usage**: ~500MB typical

### SubSpace Impact Analysis

#### SubSpace Travel
- **CPU**: +5-10% (physics modifications, hazard calculation)
- **GPU**: +10-15% (special effects, shaders)
- **Memory**: +50MB (SubSpace state, effects)

#### Multiplayer
- **Network**: 10-30 KB/s per client (depends on activity)
- **CPU**: +20-40% on server (state management)
- **Memory**: +100MB per 50 players (state replication)

#### Territory System
- **CPU**: +5% (influence calculations, background updates)
- **Memory**: +20MB (territory data, faction states)

#### Crafting System
- **CPU**: Minimal (event-driven)
- **Memory**: +30MB (blueprints, resources)

### Optimization Strategies

1. **Spatial Partitioning**: QuadTree for collision and rendering
2. **Level of Detail**: Reduce detail for distant objects
3. **Instanced Rendering**: Batch similar objects
4. **Async Loading**: Background loading of assets
5. **State Caching**: Cache computed states
6. **Network Optimization**: Delta compression, snapshot interpolation

## Build System

### Meson Build

SubSpace uses Meson build system (inherited from Naev).

**Key Build Files**:
- `meson.build` - Main build configuration
- `meson_options.txt` - Build options
- `subprojects/` - Dependency subprojects

**Build Configuration**:
```bash
# Development build
meson setup builddir --buildtype=debug

# Release build
meson setup builddir --buildtype=release -Db_lto=true

# With SubSpace features
meson setup builddir -Dsubspace_multiplayer=enabled
```

### New Build Options

**Planned Options**:
```
-Dsubspace_multiplayer=enabled/disabled
-Dsubspace_server_mode=enabled/disabled
-Dsubspace_debug_render=enabled/disabled
-Dsubspace_experimental=enabled/disabled
```

## Testing Strategy

### Current Testing
- Unit tests: Limited
- Integration tests: Manual
- Performance tests: Ad-hoc

### SubSpace Testing Plan

#### Unit Tests
- SubSpace physics calculations
- Gate logic
- Territory influence algorithms
- Crafting recipes

#### Integration Tests
- SubSpace travel sequences
- Multiplayer synchronization
- Territory conquest flows
- Crafting workflows

#### Performance Tests
- SubSpace render performance
- Multiplayer scaling (50, 100, 200 clients)
- Large-scale battles (100+ ships)
- Long-running sessions

#### Network Tests
- Latency simulation
- Packet loss handling
- Bandwidth limitations
- Connection stability

## Development Tools

### Debugging
- **GDB/LLDB**: C/Rust debugging
- **Valgrind**: Memory leak detection
- **RenderDoc**: Graphics debugging
- **Wireshark**: Network analysis

### Profiling
- **perf**: CPU profiling
- **Callgrind**: Call graph analysis
- **Massif**: Heap profiling
- **Custom**: In-game profiler

### Content Creation
- **Map Editor**: In-game system editor
- **Mission Editor**: Planned
- **Ship Editor**: XML-based
- **Blueprint Editor**: Planned

## Plugin System

### Current Plugin API
- Lua-based plugins
- Hook system
- Event system
- Data overrides

### SubSpace Plugin Enhancements
- **SubSpace Hooks**: SubSpace-specific events
- **Multiplayer Plugins**: Server-side logic
- **Territory Plugins**: Custom territory rules
- **Crafting Plugins**: Custom recipes and mechanics

**Plugin Architecture**:
```lua
-- SubSpace plugin example
function subspace_enter_hook(player, gate)
    -- Custom logic when entering SubSpace
    print("Entering SubSpace via " .. gate.name)
    -- Add custom effects, modify behavior, etc.
end

-- Register hook
hook.subspace_enter("subspace_enter_hook")
```

## Security Considerations

### Current Security
- Save file integrity checks
- Basic input validation
- Limited mod sandboxing

### SubSpace Security Enhancements

#### Multiplayer Security
- Server authority model
- Anti-cheat detection
- Rate limiting
- Input validation
- Encrypted communication (TLS)

#### Client Security
- Sandbox Lua execution
- Validate network data
- Prevent code injection
- Secure save files

#### Server Security
- DDoS protection
- Authentication system
- Authorization checks
- Audit logging
- Resource limits

## Future Considerations

### Scalability
- Distributed server architecture
- Database backend (PostgreSQL/Redis)
- Microservices for features
- Cloud deployment support

### Cross-Platform
- Windows, Linux, macOS (current)
- Console support (future)
- Mobile support (experimental)

### Modding Support
- Steam Workshop integration
- In-game mod browser
- Automatic mod updates
- Dependency management

### Analytics
- Usage telemetry (opt-in)
- Performance metrics
- Error reporting
- A/B testing framework

## Documentation

### Code Documentation
- Doxygen for C code
- RustDoc for Rust code
- LDoc for Lua code
- Architecture diagrams

### API Documentation
- Lua API reference
- Plugin development guide
- Networking protocol spec
- Database schema docs

## Conclusion

SubSpace builds upon Naev's solid technical foundation while adding significant new features. The modular architecture allows for gradual implementation of SubSpace features without disrupting the core engine.

Key technical challenges:
1. Multiplayer synchronization
2. Performance with enhanced features
3. Territory system complexity
4. Network security and anti-cheat

These will be addressed iteratively through prototyping, testing, and community feedback.

---

*This document will be updated as SubSpace development progresses.*

*Last Updated: December 2025*  
*SubSpace Technical Team*
