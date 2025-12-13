# SubSpace

![SubSpace Logo](https://naev.org/imgs/naev.png)
*Logo pending - currently using Naev placeholder*

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

## About SubSpace

**SubSpace** is an open source 2D space trading and combat game derived from [Naev](https://naev.org). 

SubSpace takes the solid foundation of Naev and expands it with new features focusing on:
- **SubSpace Travel**: Dimensional corridors and faster-than-light mechanics
- **Multiplayer**: Cooperative gameplay and shared universe
- **Territory Control**: Player factions and station construction
- **Living Universe**: Dynamic events and evolving factions
- **Enhanced Exploration**: Procedural content and discovery systems

You pilot a spaceship from a top-down perspective in an open galaxy where you're free to trade, fight, explore, build, and shape your own destiny.

## Status

**⚠️ Early Development Phase**

SubSpace is currently in the initial development phase. We are:
- ✅ Establishing the project foundation based on Naev
- ✅ Reviewing and documenting the codebase
- ✅ Planning SubSpace-specific features
- 🔄 Rebranding and customization in progress
- 📋 Roadmap and feature specifications being finalized

**The game is currently playable using the original Naev features.** SubSpace-specific features are under development.

## Licensing & Open Source

SubSpace is **100% open source** and suitable for use as a base for game development!

### License
- **Source Code**: GNU General Public License v3.0 or later (GPL-3.0-or-later)
- **Compliance**: Fully compatible with Debian Free Software Guidelines
- **Assets**: Various licenses documented in LICENSE file
  - Graphics: See `dat/gfx/ARTWORK_LICENSE.yaml`
  - Fonts: See `dat/fonts/FONT_LICENSE.yaml`
  - Audio: See `dat/snd/SOUND_LICENSE.yaml`
  - Other files: Creative Commons Attribution-ShareAlike 4.0 or later

### Attribution
SubSpace is derived from **Naev** (https://naev.org)
- Original Naev Copyright © Naev Dev Team
- SubSpace modifications Copyright © 2025 SubSpace Dev Team

For detailed licensing information, see:
- [LICENSE](LICENSE) - Full license details
- [SUBSPACE_PROJECT.md](SUBSPACE_PROJECT.md) - Project overview and features

### Can I Make a Game From This?
**Yes!** The GPL-3.0-or-later license means you can:
- ✅ Use the code for your own game
- ✅ Modify and customize it freely
- ✅ Distribute your modifications
- ✅ Use it commercially

**Requirements:**
- ⚠️ Must distribute source code under GPL-3.0-or-later
- ⚠️ Must credit original authors (Naev and SubSpace)
- ⚠️ Must document your changes
- ⚠️ Respect individual asset licenses

## SubSpace Features

### Current Features (Inherited from Naev)
- **Open Galaxy Exploration** - Hundreds of star systems to discover
- **Dynamic Combat** - Top-down space combat with various weapon systems
- **Trading & Economy** - Buy low, sell high across the galaxy
- **Mission System** - Story missions and procedural content
- **Ship Customization** - Dozens of ships with hundreds of outfits
- **Faction System** - Complex relationships with multiple factions
- **Plugin Support** - Extend the game with mods

### Planned SubSpace Features
See [SUBSPACE_PROJECT.md](SUBSPACE_PROJECT.md) for detailed feature roadmap including:
- SubSpace travel mechanics and dimensional corridors
- Multiplayer support with shared universe
- Territory control and player factions
- Enhanced crafting and manufacturing
- Procedural exploration content
- Advanced character progression
- And much more!

## Getting Started

### Playing SubSpace
Currently, SubSpace is in early development. You can:
1. Build from source (see below)
2. Wait for official releases (coming soon)

### Dependencies

SubSpace requires the same dependencies as Naev:
- Rust 1.88 or later
- bindgen 0.72 or later
- SDL3
- libxml2
- freetype2
- OpenAL
- OpenBLAS
- libvorbis
- intltool
- SuiteSparse
- enet
- physfs
- lua 5.1 / luajit
- pcre2
- GLPK
- libunibreak
- cmark
- pyyaml (compilation only)

For detailed OS-specific instructions, see the [Naev Wiki](https://codeberg.org/naev/naev/wiki/Compiling).

### Building SubSpace

#### Cloning the Repository

```bash
git clone https://github.com/shifty81/naev-mine.git subspace
cd subspace
git submodule update --init --recursive
```

#### Compilation

```bash
meson setup builddir .
cd builddir
meson compile
./naev.py  # Note: Still named 'naev.py' - will be renamed to 'subspace' in future
```

**⚠️ Temporary Naming**: The executable is currently named `naev.py` throughout the documentation as SubSpace is in early development. This will be renamed to `subspace` in a future release once the rebranding is complete.

#### Development Build

```bash
meson setup builddir --buildtype=debug -Db_sanitize=address
cd builddir
meson compile
./naev.py  # (will be renamed to 'subspace' in future)
```

#### Release Build

```bash
meson setup builddir --buildtype=release -Db_lto=true
cd builddir
meson compile
./naev.py  # (will be renamed to 'subspace' in future)
```

## Contributing

SubSpace is an open source project and welcomes contributions! See [SUBSPACE_PROJECT.md](SUBSPACE_PROJECT.md) for details on:
- How to contribute code
- Content creation guidelines
- Testing and feedback
- Documentation improvements

### Quick Contribution Guide
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Test your changes
5. Commit with clear messages (`git commit -m 'Add amazing feature'`)
6. Push to your fork (`git push origin feature/amazing-feature`)
7. Open a Pull Request

### Coding Standards
- Follow existing code style
- Ensure GPL-3.0-or-later compatibility
- Document your changes
- Add tests where applicable
- Use pre-commit hooks (run `pre-commit install`)

## Development Roadmap

See [SUBSPACE_PROJECT.md](SUBSPACE_PROJECT.md) for the complete roadmap.

**Current Phase**: Foundation & Rebranding
- [x] Project review and licensing compliance
- [x] Initial documentation
- [ ] Complete rebranding
- [ ] Set up community infrastructure
- [ ] Begin SubSpace-specific feature development

## Community

### Stay Connected
- **Repository**: https://github.com/shifty81/naev-mine
- **Original Naev**: https://naev.org
- **Issues**: [GitHub Issues](https://github.com/shifty81/naev-mine/issues)
- **Discord**: [Coming Soon]

### Get Involved
- Report bugs and suggest features
- Contribute code or content
- Help with testing
- Improve documentation
- Spread the word!

## Credits

### SubSpace Team
- Development team being formed

### Based on Naev
SubSpace is built upon the excellent work of the Naev development team:
- Original Naev project: https://naev.org
- Naev repository: https://codeberg.org/naev/naev
- Naev Dev Team and all contributors

Thank you to the Naev community for creating such a solid foundation!

## License

SubSpace is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see https://www.gnu.org/licenses/.

---

**Original Naev Copyright © Naev Dev Team**  
**SubSpace Modifications Copyright © 2025 SubSpace Dev Team**

SubSpace is derived from Naev and maintains full GPL-3.0-or-later compliance.
