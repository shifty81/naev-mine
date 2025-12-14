# SubSpace Build, Launch, and Test Guide

A comprehensive visual guide to building, launching, and testing SubSpace.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [Detailed Build Instructions](#detailed-build-instructions)
- [Launching SubSpace](#launching-subspace)
- [Debugging with Visual Studio Code](#debugging-with-visual-studio-code)
- [Testing In-Game Features](#testing-in-game-features)
- [Logging System](#logging-system)
- [Troubleshooting](#troubleshooting)

---

## Prerequisites

### Required Software

Before building SubSpace, ensure you have the following installed:

#### Core Build Tools
- **Rust** 1.88 or later
  - Install: `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
  - Verify: `rustc --version`
- **Meson** 1.7.0 or later
  - Install: `pip3 install meson` or use your package manager
  - Verify: `meson --version`
- **Ninja** (build backend)
  - Install: Use your package manager (apt, brew, choco, etc.)
  - Verify: `ninja --version`
- **Clang** (required for bindgen)
  - Install: Use your package manager
  - Verify: `clang --version`
- **bindgen** 0.72 or later
  - Install: `cargo install bindgen-cli`
  - Verify: `bindgen --version`

#### Dependencies

**Linux (Ubuntu/Debian):**
```bash
sudo apt-get install libsdl3-dev libxml2-dev libfreetype6-dev \
  libopenal-dev libopenblas-dev libvorbis-dev intltool \
  libsuitesparse-dev libenet-dev libphysfs-dev liblua5.1-dev \
  libpcre2-dev libglpk-dev libunibreak-dev libcmark-dev python3-yaml
```

**macOS:**
```bash
brew install sdl3 libxml2 freetype openal-soft openblas libvorbis \
  intltool suitesparse enet physfs lua@5.1 pcre2 glpk libunibreak cmark
```

**Windows:**
See [Windows Compilation Guide](https://codeberg.org/naev/naev/wiki/Compiling-on-Windows)

---

## Quick Start

For the impatient, here's the fastest path from zero to running SubSpace:

```bash
# 1. Clone the repository
git clone https://github.com/shifty81/naev-mine.git subspace
cd subspace

# 2. Initialize artwork submodule
git submodule update --init --recursive

# 3. Configure build system
meson setup builddir

# 4. Compile
cd builddir
meson compile

# 5. Run SubSpace
./subspace.py
```

**Time estimate:** 5-15 minutes (depending on your system and internet speed)

---

## Detailed Build Instructions

### Step 1: Clone the Repository

```bash
git clone https://github.com/shifty81/naev-mine.git subspace
cd subspace
```

**What this does:**
- Downloads the SubSpace source code
- Creates a `subspace` directory with all the game files

### Step 2: Initialize Submodules

SubSpace's artwork assets are stored in a separate git submodule. You must initialize it:

```bash
git submodule update --init --recursive
```

**What this does:**
- Downloads artwork assets from the naev-artwork repository
- Places them in the `assets/` directory
- Essential for the game to display graphics

**Pro tip:** Set automatic submodule updates:
```bash
git config submodule.recurse true
```

### Step 3: Configure the Build

Create a build directory and configure Meson:

**For Development (with debugging):**
```bash
meson setup builddir --buildtype=debug -Db_sanitize=address
```

**For Release (optimized):**
```bash
meson setup builddir --buildtype=release -Db_lto=true
```

**What this does:**
- Creates a `builddir/` directory for build artifacts
- Analyzes dependencies
- Generates build files
- Configures compiler flags

**Build types explained:**
- `debug`: Includes debugging symbols, no optimization, easier to debug
- `debugoptimized`: Some optimization, still debuggable
- `release`: Full optimization, smaller binary, harder to debug

### Step 4: Compile SubSpace

```bash
cd builddir
meson compile
```

**What this does:**
- Compiles C source files
- Compiles Rust source files
- Links everything into the `subspace` executable
- Generates wrapper scripts (`subspace.py`, `naev.py`)
- Builds translation files

**Time estimate:** 
- First build: 5-10 minutes
- Incremental rebuilds: 30 seconds - 2 minutes

**Tip:** For parallel compilation (faster):
```bash
meson compile -j $(nproc)  # Linux
meson compile -j $(sysctl -n hw.ncpu)  # macOS
```

### Step 5: Verify the Build

After compilation completes, you should see:

```
builddir/
├── subspace           # The executable
├── subspace.py        # Development wrapper script
├── naev.py            # Legacy wrapper (compatibility)
└── meson_overlay.zip  # Generated data overlay
```

Check that the executable exists:
```bash
ls -lh subspace
```

---

## Launching SubSpace

There are multiple ways to launch SubSpace, depending on your needs:

### Method 1: Using the Wrapper Script (Recommended for Development)

The wrapper script sets up the correct data paths and optionally launches a debugger:

```bash
cd builddir
./subspace.py
```

**Features:**
- Automatic data path configuration
- Optional GDB/LLDB integration for crash debugging
- Environment variable setup for better error messages
- Proper cleanup on exit

**Customization:**
```bash
# Disable automatic debugger attachment
WITHDEBUGGER=false ./subspace.py

# Prefer LLDB over GDB
PREFERLLDB=true ./subspace.py

# Pass arguments to SubSpace
./subspace.py --help
./subspace.py -f  # Fullscreen mode
```

### Method 2: Direct Execution

Run the executable directly (requires manual data path setup):

```bash
cd builddir
./subspace -d meson_overlay.zip -d ../dat -d ../assets -d dat -d ..
```

**When to use:**
- Performance testing (no wrapper overhead)
- Integration with external tools
- Custom launch scenarios

### Method 3: Using Visual Studio Code

Open the project in VS Code and press **F5** or use the **Run and Debug** panel.

See [Debugging with Visual Studio Code](#debugging-with-visual-studio-code) section below.

---

## Debugging with Visual Studio Code

SubSpace includes pre-configured VS Code debugging support.

### Setup

1. **Install VS Code:** https://code.visualstudio.com/

2. **Install Recommended Extensions:**
   - C/C++ (Microsoft)
   - Rust Analyzer
   - Meson Build
   - CodeLLDB (for LLDB debugging)

   VS Code will prompt you to install these when you open the project.

3. **Open the SubSpace Project:**
   ```bash
   code /path/to/subspace
   ```

### Debug Configurations

Three debug configurations are available (in `.vscode/launch.json`):

#### 1. SubSpace (GDB)
- Uses GDB debugger
- Best for Linux
- Full C/Rust debugging support

**To use:** 
1. Open VS Code
2. Go to **Run and Debug** panel (Ctrl+Shift+D)
3. Select "SubSpace (GDB)" from dropdown
4. Press **F5** or click green play button

#### 2. SubSpace (LLDB)
- Uses LLDB debugger
- Best for macOS
- Better Rust debugging

**To use:** Same as GDB, but select "SubSpace (LLDB)"

#### 3. SubSpace (wrapper script)
- Debugs the Python wrapper script
- Useful for troubleshooting launch issues

**To use:** Same as above, select "SubSpace (wrapper script)"

### Setting Breakpoints

1. Open a source file (e.g., `src/naev.c`, `src/naev.rs`)
2. Click in the left margin next to a line number
3. A red dot appears (breakpoint set)
4. Launch debugger (F5)
5. Execution will pause at breakpoint

### Debug Controls

When paused at a breakpoint:
- **F5**: Continue execution
- **F10**: Step over (next line)
- **F11**: Step into (enter function)
- **Shift+F11**: Step out (exit function)
- **Ctrl+Shift+F5**: Restart
- **Shift+F5**: Stop debugging

### Inspecting Variables

- **Variables panel**: Shows local variables and their values
- **Watch panel**: Add expressions to monitor
- **Call Stack panel**: Shows function call hierarchy
- **Debug Console**: Execute expressions while paused

### Build Tasks

Available tasks in VS Code (Ctrl+Shift+P → "Tasks: Run Task"):
- **build-subspace**: Compile the project (Ctrl+Shift+B)
- **meson-setup**: Configure build system
- **clean**: Remove build directory
- **run-subspace**: Build and run without debugger
- **test-cargo**: Run Rust unit tests

---

## Testing In-Game Features

Once SubSpace is running, here's how to test various game features:

### 1. Main Menu

**What to test:**
- [ ] Menu navigation with mouse
- [ ] Menu navigation with keyboard (arrow keys, Enter)
- [ ] Background animation plays smoothly
- [ ] Music plays (if audio working)

**Expected behavior:**
- Smooth menu transitions
- No crashes
- Responsive input

### 2. Starting a New Game

**Steps:**
1. Click "New Game"
2. Select a starting ship
3. Choose starting location
4. Select difficulty

**What to test:**
- [ ] Ship previews display correctly
- [ ] Ship descriptions are readable
- [ ] Can cycle through options
- [ ] "Start" button creates a new game

### 3. Basic Flight

**Controls:**
- **W/Up**: Accelerate
- **S/Down**: Decelerate  
- **A/Left** and **D/Right**: Turn
- **Mouse**: Aim direction
- **Space**: Primary weapon (when equipped)
- **Tab**: Target nearest ship
- **R**: Face target
- **T**: Board target (when close)

**What to test:**
- [ ] Ship responds to controls smoothly
- [ ] Ship rotation is fluid
- [ ] Acceleration/deceleration feels responsive
- [ ] No stuttering or lag

### 4. Landing on Planets

**Steps:**
1. Fly close to a planet or station
2. Press **L** when "Land" option appears
3. Explore landing menu

**What to test:**
- [ ] Landing interface loads
- [ ] Can navigate spaceport menu
- [ ] Bar, Mission Computer, Outfitter, Shipyard accessible
- [ ] Can take off again

### 5. Taking a Mission

**Steps:**
1. Land on a planet
2. Go to Mission Computer
3. Select a mission
4. Accept it
5. Complete mission objectives

**What to test:**
- [ ] Mission list displays
- [ ] Mission descriptions are readable
- [ ] Can accept missions
- [ ] Mission objectives appear in OSD (on-screen display)
- [ ] Mission progresses correctly
- [ ] Rewards given on completion

### 6. Combat Testing

**Steps:**
1. Find hostile ships (pirates, etc.)
2. Engage in combat
3. Use weapons

**What to test:**
- [ ] Weapon effects display
- [ ] Damage is calculated
- [ ] Ships explode when destroyed
- [ ] AI ships fight back
- [ ] No crashes during combat

### 7. Trading

**Steps:**
1. Land on a planet with a commodity exchange
2. Buy commodities
3. Travel to another system
4. Sell commodities

**What to test:**
- [ ] Commodity prices display
- [ ] Can buy/sell goods
- [ ] Cargo capacity respected
- [ ] Credits update correctly

### 8. Map and Navigation

**Controls:**
- **M**: Open map
- **Mouse**: Pan and zoom
- Click systems to plot course

**What to test:**
- [ ] Map displays correctly
- [ ] Can navigate map
- [ ] Can plot courses
- [ ] Autopilot works
- [ ] Hyperspace jumps function

### 9. Saving and Loading

**Steps:**
1. Play for a bit
2. Land and save game
3. Quit to main menu
4. Load the save

**What to test:**
- [ ] Can save game
- [ ] Save game appears in load menu
- [ ] Game loads correctly
- [ ] Progress is preserved
- [ ] No corruption

### 10. Performance Testing

**What to monitor:**
- FPS counter (if enabled)
- Memory usage
- CPU usage
- No memory leaks over time

**How to test:**
- Play for extended period (30+ minutes)
- Engage in multiple combats
- Visit many systems
- Monitor system resources

---

## Logging System

SubSpace has a comprehensive logging system for debugging and troubleshooting.

### Logging Macros (for developers)

SubSpace uses these logging macros in C code:

```c
LOG("This is an info message: %d", value);     // Info level
WARN("Warning: %s might be wrong", thing);     // Warning level
ERR("Critical error: %s", error);              // Error level (aborts)
DEBUG("Debug info: %d", debug_value);          // Debug level (only in debug builds)
```

**Log levels:**
- **LOG**: General information
- **WARN**: Warnings that don't stop execution
- **ERR**: Critical errors (terminates program)
- **DEBUG**: Verbose debugging info (only in debug builds)

### Where Logs Go

**Console Output:**
- All logs print to stdout/stderr
- Visible when running from terminal
- Captured by debugger console in VS Code

**Log Files:**
SubSpace creates log files in:
- **Linux**: `~/.local/share/subspace/logs/`
- **macOS**: `~/Library/Application Support/SubSpace/logs/`
- **Windows**: `%APPDATA%\SubSpace\logs\`

**Log file format:**
```
[2025-12-13 23:45:12] [INFO] Loading configuration...
[2025-12-13 23:45:13] [INFO] Initializing OpenGL...
[2025-12-13 23:45:14] [WARN] Audio device not found, using default
[2025-12-13 23:45:15] [INFO] Game started successfully
```

### Enabling Verbose Logging

**During development:**
Build with debug mode to enable DEBUG() logs:
```bash
meson setup builddir --buildtype=debug
```

**Runtime environment variables:**
```bash
# Enable Rust backtraces (already set by wrapper)
export RUST_BACKTRACE=1

# Verbose OpenAL audio logging
export ALSOFT_LOGLEVEL=3

# Trap OpenAL errors immediately
export ALSOFT_TRAP_AL_ERROR=1
```

### Reading Crash Logs

When SubSpace crashes:

1. **Check the console output** for the last log messages
2. **Look for stack traces** (if Rust panic or assertion failure)
3. **Check crash dumps** (if using debugger)

**Example crash log:**
```
[2025-12-13 23:50:42] [INFO] Loading mission script: foo.lua
[2025-12-13 23:50:42] [ERROR] Lua error: attempt to index nil value
thread 'main' panicked at 'Mission load failed', src/mission.c:342
stack backtrace:
  0: rust_begin_unwind
  1: mission_load
  2: event_run
  ...
```

### Adding Your Own Logs

When developing/debugging, add logs liberally:

```c
// In C code
DEBUG("Function foo() called with value: %d", value);

if (some_condition) {
   WARN("Unexpected condition in foo()");
}

if (critical_error) {
   ERR("Cannot continue: %s", error_message);
}
```

```rust
// In Rust code
use log::{debug, info, warn, error};

debug!("Function foo() called with value: {}", value);
info!("Loading resource: {}", name);
warn!("Unexpected condition");
error!("Critical error occurred");
```

---

## Troubleshooting

Common issues and solutions:

### Build Fails

**Problem:** `meson setup` fails with dependency errors

**Solution:**
- Ensure all dependencies are installed
- Check dependency versions: `rustc --version`, `meson --version`
- Try using subproject fallbacks: `meson setup builddir --wrap-mode=forcefallback`

---

**Problem:** Compilation fails with C/Rust errors

**Solution:**
- Clean and rebuild: `rm -rf builddir && meson setup builddir`
- Update Rust: `rustup update`
- Check for conflicting library versions

---

**Problem:** Linker errors about missing symbols

**Solution:**
- Ensure all dependencies are properly installed
- Check that `libsubspace.a` was built successfully
- Try `meson setup builddir --wipe` to reconfigure

---

### Launch Fails

**Problem:** `./subspace` not found

**Solution:**
- Verify you're in the `builddir` directory: `cd builddir`
- Check that compilation succeeded: `ls -lh subspace`
- If missing, recompile: `meson compile`

---

**Problem:** Segmentation fault on startup

**Solution:**
- Run with debugger to get stack trace: `gdb ./subspace` then `run`
- Check that artwork submodule is initialized: `git submodule update --init`
- Verify data paths: ensure `dat/`, `assets/` exist

---

**Problem:** "Failed to load data files"

**Solution:**
- Use wrapper script: `./subspace.py` (sets paths automatically)
- Or manually specify: `./subspace -d ../dat -d ../assets`
- Check artwork submodule: `ls assets/` should show files

---

### Graphics Issues

**Problem:** Black screen or no graphics

**Solution:**
- Check OpenGL support: `glxinfo | grep OpenGL` (Linux)
- Update graphics drivers
- Try forcing software rendering: `LIBGL_ALWAYS_SOFTWARE=1 ./subspace.py`

---

**Problem:** Low FPS / stuttering

**Solution:**
- Build with release mode: `meson setup builddir --buildtype=release`
- Disable debug sanitizers: remove `-Db_sanitize=address`
- Check GPU usage: ensure hardware acceleration enabled
- Lower graphics settings in-game

---

### Audio Issues

**Problem:** No sound

**Solution:**
- Check audio backend: `ls /dev/snd/` (Linux)
- Test audio: `speaker-test` or `paplay`
- Check OpenAL: `openal-info`
- Review audio logs in console

---

**Problem:** Audio crackling/distortion

**Solution:**
- Adjust OpenAL settings: edit `~/.alsoftrc`
- Try different audio backend
- Check system audio server (PulseAudio, PipeWire, etc.)

---

### Debug Issues

**Problem:** Breakpoints not working in VS Code

**Solution:**
- Ensure debug build: `--buildtype=debug`
- Check that `compile_commands.json` exists
- Reload VS Code: Ctrl+Shift+P → "Developer: Reload Window"
- Verify debugger is installed: `gdb --version` or `lldb --version`

---

**Problem:** Can't see variable values in debugger

**Solution:**
- Variables may be optimized out in release builds
- Use debug build: `--buildtype=debug`
- Some complex types require pretty-printers

---

### Performance Issues

**Problem:** Memory leaks

**Solution:**
- Run with ASAN: `meson setup builddir -Db_sanitize=address`
- Use valgrind: `valgrind --leak-check=full ./subspace`
- Check logs for unreleased resources

---

**Problem:** High CPU usage

**Solution:**
- Check for infinite loops (use profiler)
- Enable VSync to cap frame rate
- Review recent code changes

---

## Getting Help

If you're still stuck:

1. **Check existing issues:** https://github.com/shifty81/naev-mine/issues
2. **Search documentation:** Look through other `.md` files
3. **Ask for help:** Open a new issue with:
   - Description of problem
   - Steps to reproduce
   - Build configuration
   - Log output
   - System information

---

## Summary

This guide covered:
- ✅ Installing dependencies
- ✅ Building SubSpace from source
- ✅ Launching the game
- ✅ Debugging with VS Code
- ✅ Testing in-game features
- ✅ Understanding the logging system
- ✅ Troubleshooting common issues

**Next steps:**
- Read [CONTRIBUTING_SUBSPACE.md](CONTRIBUTING_SUBSPACE.md) to start contributing
- Explore [ARCHITECTURE.md](ARCHITECTURE.md) for technical details
- Check [FEATURES_BRAINSTORM.md](FEATURES_BRAINSTORM.md) for planned features

---

**Happy coding and flying! 🚀**

*SubSpace Development Team*
