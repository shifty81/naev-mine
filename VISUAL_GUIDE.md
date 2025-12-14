# SubSpace Visual Quick Reference

Quick visual guide with step-by-step screenshots and commands.

## 🚀 Quick Start Visual Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                    FROM ZERO TO PLAYING                          │
└─────────────────────────────────────────────────────────────────┘

Step 1: Get the Code
━━━━━━━━━━━━━━━━━━━━
$ git clone https://github.com/shifty81/naev-mine.git subspace
$ cd subspace

Step 2: Get the Assets
━━━━━━━━━━━━━━━━━━━━━
$ git submodule update --init --recursive
[This downloads ~500MB of graphics and sounds]

Step 3: Configure Build
━━━━━━━━━━━━━━━━━━━━━━
$ meson setup builddir
[Checks dependencies, sets up build system]

Step 4: Compile
━━━━━━━━━━━━━━━
$ cd builddir
$ meson compile
[Takes 5-10 minutes first time]

Step 5: Play!
━━━━━━━━━━━━
$ ./subspace.py
[Game launches with cool space theme]

Total time: ~20 minutes (including downloads)
```

---

## 📁 Project Structure Visualization

```
subspace/                          ← Your clone directory
│
├── 📄 meson.build                 ← Build configuration
├── 📄 BUILD_GUIDE.md              ← Read this! (you are here)
├── 📄 SUBSPACE_README.md          ← Project overview
│
├── 📂 src/                        ← Source code
│   ├── naev.c                     ← Main C code
│   ├── naev.rs                    ← Main Rust code
│   ├── player.c                   ← Player logic
│   ├── mission.c                  ← Mission system
│   └── ... (hundreds more)
│
├── 📂 dat/                        ← Game data
│   ├── missions/                  ← Mission scripts (.lua)
│   ├── ships/                     ← Ship definitions (.xml)
│   ├── outfits/                   ← Equipment (.xml)
│   └── ...
│
├── 📂 assets/                     ← Graphics & Sound (submodule)
│   ├── gfx/                       ← Images, sprites
│   ├── snd/                       ← Music, sound effects
│   └── ...
│
├── 📂 utils/                      ← Development tools
│   └── build/
│       └── subspace.py            ← Launcher template
│
├── 📂 .vscode/                    ← VS Code configuration
│   ├── launch.json                ← Debug configs
│   ├── tasks.json                 ← Build tasks
│   └── settings.json              ← Editor settings
│
└── 📂 builddir/                   ← Build output (after compile)
    ├── 🎮 subspace                ← The game executable
    ├── 📄 subspace.py             ← Development launcher
    ├── 📄 naev.py                 ← Compatibility launcher
    └── ... (compiled files)
```

---

## 🔧 Build System Visual

```
┌──────────────────────────────────────────────────────────────────┐
│                HOW FILES BECOME A GAME                            │
└──────────────────────────────────────────────────────────────────┘

SOURCE CODE           COMPILATION              OUTPUT
───────────           ───────────              ──────

src/naev.c      ─┐
src/player.c    ─┤
src/mission.c   ─┤──→  C Compiler (clang)  ──→  libsubspace.a
src/...         ─┘

src/naev.rs     ─┐
src/core/*.rs   ─┤──→  Rust Compiler      ──→  libnaev.rlib
                 ┘      (rustc + cargo)

libsubspace.a   ─┐
libnaev.rlib    ─┤──→  Linker (meson)     ──→  🎮 subspace
dependencies    ─┘                                 ↓
                                               [PLAYABLE!]

dat/*.lua       ─────────────────────────────→  (loaded at runtime)
assets/gfx/*    ─────────────────────────────→  (loaded at runtime)
```

---

## 🐛 Debug Workflow Visual

```
┌──────────────────────────────────────────────────────────────────┐
│              VISUAL STUDIO CODE DEBUGGING                         │
└──────────────────────────────────────────────────────────────────┘

1. Open Project
   ┌────────────────────────┐
   │ $ code .               │
   │                        │
   │ VS Code opens with:    │
   │ • File explorer        │
   │ • Recommended exts     │
   │ • Debug configs ready  │
   └────────────────────────┘

2. Set Breakpoint
   ┌─────────────────────────────────────┐
   │  src/player.c                       │
   │  ───────────────────────────────────│
   │  340  void player_init() {          │
   │  341  🔴  Player *p = &player;     │← Click here
   │  342      p->credits = 1000;        │
   └─────────────────────────────────────┘

3. Press F5
   ┌─────────────────────────────────────┐
   │  Debug: SubSpace (GDB) ▼  ▶️ Start │
   └─────────────────────────────────────┘
   
   Behind the scenes:
   • Runs "build-subspace" task
   • meson compile
   • Launches GDB
   • Runs ./subspace
   • Waits at breakpoint

4. Execution Paused
   ┌─────────────────────────────────────┐
   │  ⚠️ PAUSED AT BREAKPOINT            │
   │  src/player.c:341                   │
   │  341  ⚫ Player *p = &player;       │
   │                                     │
   │  Variables:                         │
   │  ├─ p = 0x0 (uninitialized)        │
   │  └─ player = {...}                  │
   │                                     │
   │  Call Stack:                        │
   │  ├─ player_init() ← YOU ARE HERE   │
   │  ├─ game_start()                   │
   │  └─ main()                          │
   │                                     │
   │  [F5: Continue] [F10: Step Over]   │
   └─────────────────────────────────────┘

5. Inspect Variables
   ┌─────────────────────────────────────┐
   │  VARIABLES                          │
   │  ────────────────────────────────── │
   │  ▼ Local                            │
   │    ├─ p = 0x7fffffffe0              │
   │    └─ player                        │
   │       ├─ name = "Player"            │
   │       ├─ credits = 1000             │
   │       ├─ ship = (Pilot*) 0x...      │
   │       └─ ...                        │
   │                                     │
   │  WATCH                              │
   │  ────────────────────────────────── │
   │  + Add Expression                   │
   │    player.credits = 1000            │
   │    player.ship != NULL = true       │
   └─────────────────────────────────────┘

6. Debug Console
   ┌─────────────────────────────────────┐
   │  DEBUG CONSOLE                      │
   │  ────────────────────────────────── │
   │  > print player.name                │
   │  $1 = "Player"                      │
   │  > print player.credits             │
   │  $2 = 1000                          │
   │  > player.credits = 9999            │
   │  > continue                         │
   │  [Continuing...]                    │
   └─────────────────────────────────────┘
```

---

## 🎮 Game Testing Visual

```
┌──────────────────────────────────────────────────────────────────┐
│                IN-GAME TESTING CHECKLIST                          │
└──────────────────────────────────────────────────────────────────┘

Launch Game
━━━━━━━━━━━
$ ./subspace.py

Main Menu
━━━━━━━━━
┌───────────────────────────┐
│     ✨ SUBSPACE ✨        │
│                           │
│   ▶ New Game              │← Test this
│     Load Game             │
│     Options               │
│     Quit                  │
│                           │
│   [Background: Stars]     │
│   [Music: Playing]        │
└───────────────────────────┘

✓ Menu navigation works
✓ Background animates
✓ Music plays

New Game Setup
━━━━━━━━━━━━━━
┌───────────────────────────┐
│   Choose Your Ship        │
│                           │
│   ┌───┐ ┌───┐ ┌───┐      │
│   │ ⛴ │ │ ⛴ │ │ ⛴ │      │← Test selection
│   └───┘ └───┘ └───┘      │
│   Scout  Trader  Courier  │
│                           │
│   [< Prev]  [Next >]      │
│   [      Start      ]     │
└───────────────────────────┘

✓ Ship previews display
✓ Can cycle ships
✓ Can start game

In-Game Flight
━━━━━━━━━━━━━━
┌───────────────────────────┐
│  🌟                       │
│     🛸 ←Your ship         │
│           ↑               │
│       🪐 Planet           │
│                  ☄️       │
│                           │
│  ┌─────────────────────┐  │
│  │ Speed: 250 m/s      │  │
│  │ Shield: ▓▓▓▓▓ 100%  │  │
│  │ Armor:  ▓▓▓▓▓ 100%  │  │
│  └─────────────────────┘  │
└───────────────────────────┘

Controls to test:
• W/Up Arrow    → Accelerate  ✓
• S/Down Arrow  → Brake       ✓
• A/D or ←→     → Turn        ✓
• Mouse         → Aim         ✓
• Space         → Fire        ✓
• L             → Land        ✓
• M             → Map         ✓

Landing on Planet
━━━━━━━━━━━━━━━━━
┌───────────────────────────┐
│   🏛️ Spaceport Menu       │
│                           │
│   ▶ Mission Computer      │← Test this
│     Outfitter             │
│     Shipyard              │
│     Commodity Exchange    │
│     Bar                   │
│     Take Off              │
└───────────────────────────┘

✓ Landing works
✓ Menu displays
✓ Can navigate

Mission Computer
━━━━━━━━━━━━━━━━
┌───────────────────────────┐
│   Available Missions      │
│   ─────────────────────   │
│   ▶ Cargo Delivery        │
│     Reward: 5,000¢        │
│     Difficulty: Easy      │
│                           │
│     Rush Delivery         │
│     Reward: 10,000¢       │
│     Difficulty: Medium    │
│                           │
│   [Accept] [Decline]      │
└───────────────────────────┘

✓ Missions list
✓ Can accept mission
✓ Mission appears in log

Combat Test
━━━━━━━━━━━
┌───────────────────────────┐
│  💥 PEW PEW              │
│     🛸 ←You               │
│        ╲                  │
│         ╲═════╗ Laser     │
│              💥           │
│           ☠️ ←Pirate      │
│                           │
│  Target: Pirate Scout     │
│  Shield: ▓▓▓░░ 60%        │
│  Hull:   ▓▓▓▓░ 80%        │
└───────────────────────────┘

✓ Weapons fire
✓ Damage applied
✓ Ships explode
✓ No crashes

Performance Check
━━━━━━━━━━━━━━━━━
Monitor:
• FPS: 60+ ✓
• Memory: Stable ✓
• CPU: Reasonable ✓
• No memory leaks ✓
```

---

## 📊 Logging Visual

```
┌──────────────────────────────────────────────────────────────────┐
│                    LOGGING SYSTEM                                 │
└──────────────────────────────────────────────────────────────────┘

In Code                     In Console
───────                     ──────────

LOG("Starting game");       [2025-12-13 23:45:12] [INFO] Starting game
                           
DEBUG("Loading: %s", f);    [2025-12-13 23:45:13] [DEBUG] Loading: ship.xml
                           
WARN("Low memory");         [2025-12-13 23:45:14] [WARN] Low memory
                           
ERR("Fatal error");         [2025-12-13 23:45:15] [ERROR] Fatal error
                            thread 'main' panicked at 'Fatal error'
                            ┌─────────────────────────────────┐
                            │  Stack Backtrace:               │
                            │  0: rust_begin_unwind           │
                            │  1: main                        │
                            │  ...                            │
                            └─────────────────────────────────┘

Log Files Location
──────────────────
Linux:   ~/.local/share/subspace/logs/
macOS:   ~/Library/Application Support/SubSpace/logs/
Windows: %APPDATA%\SubSpace\logs\

Example log file:
┌──────────────────────────────────────────────────────┐
│  subspace-2025-12-13.log                             │
│  ──────────────────────────────────────────────────  │
│  [23:45:12] [INFO]  SubSpace starting...             │
│  [23:45:13] [INFO]  Loading configuration            │
│  [23:45:13] [DEBUG] Config file: ~/.config/subspace  │
│  [23:45:14] [INFO]  Initializing OpenGL 3.3          │
│  [23:45:14] [INFO]  OpenGL vendor: NVIDIA            │
│  [23:45:15] [INFO]  Loading game data                │
│  [23:45:16] [WARN]  Old save file version            │
│  [23:45:16] [INFO]  Game ready                       │
└──────────────────────────────────────────────────────┘
```

---

## 🔄 Development Cycle Visual

```
┌──────────────────────────────────────────────────────────────────┐
│                  TYPICAL DEV SESSION                              │
└──────────────────────────────────────────────────────────────────┘

Morning Coffee ☕
     ↓
Open VS Code
$ code ~/subspace
     ↓
Review Yesterday's Work
git log --oneline -5
     ↓
Pull Latest Changes
git pull origin main
     ↓
Create Feature Branch
git checkout -b feature/shields
     ↓
Edit Code
src/player.c
• Add shield regen logic
• Update ship stats
     ↓
Build (Ctrl+Shift+B)
meson compile
[Building... 30 seconds]
✓ Build successful
     ↓
Debug (F5)
[Game launches]
[Breakpoint hit in shield code]
• Inspect variables ✓
• Step through logic ✓
• Verify behavior ✓
     ↓
Fix Bug Found
src/player.c:123
- p->shield += 1;
+ p->shield += p->shield_regen;
     ↓
Rebuild (Ctrl+Shift+B)
[Building... 5 seconds]
✓ Build successful
     ↓
Test In-Game
./subspace.py
• Start game
• Take damage
• Wait...
• Shield regenerates! ✓
     ↓
Write Tests
• Add unit test
• Add integration test
     ↓
Run Tests
meson test
✓ All tests pass
     ↓
Commit Changes
git add src/player.c
git commit -m "[Feature] Add shield regen"
     ↓
Push to Fork
git push origin feature/shields
     ↓
Create Pull Request
github.com → New PR
• Add description
• Reference issue
• Request review
     ↓
Code Review
• Reviewer comments
• Make changes
• Push updates
     ↓
PR Approved & Merged
✓ Feature shipped!
     ↓
Celebrate 🎉
     ↓
Next feature...
```

---

## 🛠️ Troubleshooting Visual

```
┌──────────────────────────────────────────────────────────────────┐
│                 COMMON ISSUES FLOWCHART                           │
└──────────────────────────────────────────────────────────────────┘

Build Failed?
├─ Missing dependencies?
│  └─► Install: sudo apt-get install ...
│      OR: brew install ...
│      OR: Check BUILD_GUIDE.md
│
├─ Rust too old?
│  └─► Update: rustup update
│
└─ Meson error?
   └─► Clean: rm -rf builddir
       Then: meson setup builddir

Game Won't Start?
├─ "File not found"?
│  └─► Check: git submodule update --init
│      Verify: ls assets/
│
├─ Segmentation fault?
│  └─► Debug: gdb ./subspace
│      Run: run
│      Check: backtrace
│
└─ Black screen?
   └─► Check: glxinfo | grep OpenGL
       Update graphics drivers

No Sound?
├─ OpenAL issue?
│  └─► Check: openal-info
│      Test: speaker-test
│
└─ Wrong device?
   └─► Configure: ~/.alsoftrc

Slow Performance?
├─ Debug build?
│  └─► Use release: --buildtype=release
│
├─ Software rendering?
│  └─► Check: glxinfo | grep renderer
│      Enable hardware acceleration
│
└─ Memory leak?
   └─► Profile: valgrind ./subspace
```

---

## ⚡ Quick Command Reference

```
┌──────────────────────────────────────────────────────────────────┐
│                    CHEAT SHEET                                    │
└──────────────────────────────────────────────────────────────────┘

FIRST TIME SETUP
────────────────
git clone https://github.com/shifty81/naev-mine.git subspace
cd subspace
git submodule update --init --recursive
meson setup builddir
cd builddir
meson compile
./subspace.py

DAILY DEVELOPMENT
─────────────────
git pull                          # Get latest
git checkout -b feature/my-feat   # New branch
code .                            # Open VS Code
[Edit code]
Ctrl+Shift+B                      # Build
F5                                # Debug
./subspace.py                     # Test
git commit -am "Change"           # Commit
git push origin feature/my-feat   # Push

BUILD COMMANDS
──────────────
meson setup builddir              # Configure
meson compile                     # Build all
meson compile subspace            # Build exe only
meson compile -j 8                # Parallel build
meson test                        # Run tests
rm -rf builddir                   # Clean all

RUN COMMANDS
────────────
./subspace.py                     # With wrapper
./subspace.py --help              # See options
./subspace.py -f                  # Fullscreen
WITHDEBUGGER=false ./subspace.py  # No debugger
./subspace                        # Direct (manual paths)

DEBUG COMMANDS
──────────────
code .                            # VS Code
F5                                # Start debug
F10                               # Step over
F11                               # Step into
Shift+F5                          # Stop
gdb ./subspace                    # Command line GDB
lldb ./subspace                   # Command line LLDB

GIT COMMANDS
────────────
git status                        # Check status
git add .                         # Stage all
git commit -m "msg"               # Commit
git push origin branch            # Push
git pull                          # Pull latest
git log --oneline -10             # Recent commits
```

---

## 🎯 Success Checklist

```
INITIAL SETUP COMPLETE
□ Repository cloned
□ Submodules initialized
□ Dependencies installed
□ Build configured (meson setup)
□ First compile successful
□ Game launches

VS CODE SETUP COMPLETE
□ VS Code installed
□ Project opened
□ Extensions installed
□ Can build (Ctrl+Shift+B)
□ Can debug (F5)
□ Breakpoints work

READY TO CONTRIBUTE
□ Can edit code
□ Can build changes
□ Can test in-game
□ Can commit code
□ Can push to fork
□ Can create PR

READY TO PLAY
□ Game launches
□ Graphics display
□ Sound works
□ Controls respond
□ Can save/load
□ Performance good
```

---

**You're all set! Happy coding and flying! 🚀**

See [BUILD_GUIDE.md](BUILD_GUIDE.md) for detailed explanations.

*SubSpace Development Team*
