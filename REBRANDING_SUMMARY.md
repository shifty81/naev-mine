# SubSpace Rebranding Summary

This document summarizes the complete rebranding from Naev to SubSpace.

## Overview

The SubSpace project has been fully rebranded from its Naev origins. All build system references, executable names, and documentation have been updated to reflect the new SubSpace identity.

## Changes Made

### 1. Build System (meson.build)

**Project Name:**
- Changed `project('naev', ...)` to `project('subspace', ...)`
- Updated copyright holder from "Naev Dev Team" to "SubSpace Dev Team"
- Updated issue address to GitHub repository

**Executable Name:**
- Renamed binary from `naev` to `subspace`
- Static library renamed from `libnaev.a` to `libsubspace.a`
- Note: Rust library still named `libnaev.rlib` (internal name preserved for now)

**Data Paths:**
- Changed default data directory from `naev` to `subspace`
- Updated: `ndata_path = get_option('datadir') / 'subspace'`

**Wrapper Scripts:**
- Primary launcher: `subspace.py` (new)
- Compatibility wrapper: `naev.py` (kept for backward compatibility)
- Both configured from `utils/build/subspace.py` template

### 2. Translation System (po/meson.build)

**Gettext Target:**
- Renamed from `i18n.gettext('naev', ...)` to `i18n.gettext('subspace', ...)`
- This changes the internal gettext domain name
- Build target changed from `naev-gmo` to `subspace-gmo`

### 3. Wrapper Script (utils/build/subspace.py)

**Created New File:**
- Based on `naev.py` with SubSpace-specific documentation
- Updated to compile `subspace-gmo` instead of `naev-gmo`
- Added docstring explaining it's the SubSpace Development Launcher

**Features:**
- Automatic debugger integration (GDB/LLDB)
- Environment variable configuration for better logging
- Proper data path setup
- Compatible with both development and release builds

### 4. Visual Studio Code Configuration (.vscode/)

**Created VS Code Support Files:**

#### launch.json
Three debug configurations:
1. **SubSpace (GDB)** - Debug with GDB (Linux)
2. **SubSpace (LLDB)** - Debug with LLDB (macOS)  
3. **SubSpace (wrapper script)** - Debug the Python launcher

All configurations:
- Reference `${workspaceFolder}/builddir/subspace` executable
- Set `RUST_BACKTRACE=1` for better error messages
- Include `preLaunchTask: "build-subspace"` to auto-build
- Configure proper data paths

#### tasks.json
Five build/test tasks:
1. **meson-setup** - Initial configuration
2. **build-subspace** - Compile (default build task)
3. **clean** - Remove build directory
4. **run-subspace** - Build and run without debugger
5. **test-cargo** - Run Rust unit tests

#### settings.json
Project-specific settings:
- C/C++ configuration provider (Meson)
- Rust Analyzer project linking
- File associations for .lua, .h, .c files
- Code style settings (3-space tabs)
- Build directory exclusions

#### extensions.json
Recommended extensions:
- C/C++ Tools (Microsoft)
- Rust Analyzer
- Meson Build
- CodeLLDB
- Lua Language Server
- Python + Debugpy

### 5. Documentation Updates

#### BUILD_GUIDE.md (NEW)
Comprehensive 18KB guide covering:
- Prerequisites and dependencies
- Quick start instructions
- Detailed build steps with explanations
- Multiple launch methods
- VS Code debugging setup
- In-game testing procedures
- Logging system documentation
- Troubleshooting section

**Key Features:**
- Step-by-step instructions
- Command examples for all platforms
- Visual indicators (checkboxes, diagrams)
- Troubleshooting for common issues
- Logging macro reference

#### DEVELOPER_WORKFLOW.md (NEW)
Visual workflow guide with ASCII diagrams:
- Development cycle flowchart
- Build system architecture
- File flow diagrams
- Debugging workflows
- Testing procedures
- Contribution process
- Command reference

**Key Features:**
- ASCII art diagrams
- Workflow visualizations
- Test checklist matrices
- Git workflow diagram
- Quick reference commands

#### SUBSPACE_README.md (UPDATED)
- Changed all `./naev.py` references to `./subspace.py`
- Updated notes about naming (no longer temporary)
- Clarified that both `subspace.py` and `naev.py` exist

#### QUICKSTART.md (UPDATED)
- Changed launcher references from `naev.py` to `subspace.py`
- Updated all code examples
- Clarified SubSpace branding throughout

### 6. .gitignore (UPDATED)
- Commented out `.vscode` entry
- Allows VS Code configuration to be committed
- Enables sharing of debug configs across team

## File Structure After Rebranding

```
subspace/
├── meson.build                  # Project: 'subspace'
├── utils/build/
│   ├── subspace.py              # New wrapper template
│   └── naev.py                  # Original (still used)
├── .vscode/
│   ├── launch.json              # Debug configurations
│   ├── tasks.json               # Build tasks
│   ├── settings.json            # Project settings
│   └── extensions.json          # Recommended extensions
├── BUILD_GUIDE.md               # Comprehensive build guide
├── DEVELOPER_WORKFLOW.md        # Visual workflow guide
├── SUBSPACE_README.md           # Updated with new names
├── QUICKSTART.md                # Updated with new names
└── builddir/ (after build)
    ├── subspace                 # Executable (renamed!)
    ├── subspace.py              # Primary launcher
    ├── naev.py                  # Compatibility launcher
    └── libsubspace.a            # C library (renamed!)
```

## What Users Need to Know

### For New Users

1. **Clone the repository:**
   ```bash
   git clone https://github.com/shifty81/naev-mine.git subspace
   cd subspace
   ```

2. **Initialize artwork:**
   ```bash
   git submodule update --init --recursive
   ```

3. **Build:**
   ```bash
   meson setup builddir
   cd builddir
   meson compile
   ```

4. **Run:**
   ```bash
   ./subspace.py
   ```

### For Existing Developers

**Good news:** `naev.py` still exists as a compatibility wrapper!

**If you were using:**
- `./naev.py` → Still works! But consider switching to `./subspace.py`
- `./naev` → Now `./subspace`

**What changed:**
- Primary executable is now `subspace` instead of `naev`
- Primary wrapper is now `subspace.py` instead of `naev.py`
- Both wrappers work identically - they're configured from the same template

### For Build Scripts/CI

**Update references from:**
```bash
./naev.py --help
```

**To:**
```bash
./subspace.py --help
```

**Or keep using** `naev.py` if you prefer - it's not going away.

## VS Code Debugging

### Quick Start

1. **Open project in VS Code:**
   ```bash
   code .
   ```

2. **Install recommended extensions** (prompt appears automatically)

3. **Press F5** to build and debug!

### Available Debug Configurations

**SubSpace (GDB)** - Best for Linux
- Full C and Rust debugging
- Breakpoints, watches, call stack
- Automatic build before launch

**SubSpace (LLDB)** - Best for macOS
- Better Rust debugging support
- Same features as GDB

**SubSpace (wrapper script)** - For launcher debugging
- Debug the Python wrapper
- Troubleshoot launch issues

### Available Tasks

**Ctrl+Shift+B** - Build SubSpace (default)
**Ctrl+Shift+P** → "Tasks: Run Task" for:
- Meson setup
- Clean build
- Run without debugging
- Run Rust tests

## Logging System

SubSpace has comprehensive logging built-in.

### C Code Logging

```c
LOG("Info message: %s", value);      // Info
WARN("Warning: %s", message);        // Warning
ERR("Critical error: %s", error);    // Abort
DEBUG("Debug: %d", value);           // Debug only
```

### Rust Code Logging

```rust
use log::{debug, info, warn, error};

info!("Loading resource: {}", name);
debug!("Debug info: {}", value);
warn!("Warning message");
error!("Error occurred");
```

### Log Output

**Console:** All logs print to stdout/stderr
**Files:** Logs saved to platform-specific locations:
- Linux: `~/.local/share/subspace/logs/`
- macOS: `~/Library/Application Support/SubSpace/logs/`
- Windows: `%APPDATA%\SubSpace\logs\`

### Environment Variables

Set these for more verbose logging:
```bash
export RUST_BACKTRACE=1           # Rust stack traces
export ALSOFT_LOGLEVEL=3          # Verbose OpenAL
export ALSOFT_TRAP_AL_ERROR=1     # Trap audio errors
```

The wrapper script (`subspace.py`) sets `RUST_BACKTRACE=1` automatically.

## Compatibility

### What Still Works

✅ All existing Naev game data (ships, missions, etc.)
✅ Lua scripts and mods
✅ Save files (compatible format)
✅ Asset files (gfx, audio)
✅ Documentation structure

### What Changed (Build System Only)

- Executable name: `naev` → `subspace`
- Wrapper name: `naev.py` → `subspace.py` (both exist)
- Library name: `libnaev.a` → `libsubspace.a`
- Project name: `naev` → `subspace`

### Backward Compatibility

The `naev.py` wrapper is **kept for compatibility**. Existing scripts will continue to work.

## Testing the Changes

### Build Test

```bash
# Clean start
rm -rf builddir

# Configure
meson setup builddir --buildtype=debug

# Build
cd builddir
meson compile

# Verify files exist
ls -lh subspace        # Executable
ls -lh subspace.py     # Wrapper
ls -lh naev.py         # Compat wrapper
```

### Launch Test

```bash
# Test primary launcher
./subspace.py --help

# Test compat launcher
./naev.py --help

# Test direct execution
./subspace --help
```

### VS Code Test

```bash
# Open in VS Code
code .

# Install recommended extensions
# (VS Code will prompt)

# Press F5 to debug
# Should build and launch
```

## Future Work

### Still Using "Naev" Internally

Some internal references remain for technical reasons:
- Rust library name: `libnaev.rlib` (Cargo package name)
- Some C header guards and internal symbols
- Some data file references

These may be updated in future releases as we further customize SubSpace.

### Planned Improvements

- [ ] Rename Rust package from `naev` to `subspace`
- [ ] Update internal C namespaces
- [ ] Rebrand more data files
- [ ] Custom SubSpace logo/branding assets
- [ ] SubSpace-specific game features

## Migration Guide

### For Contributors

**Old workflow:**
```bash
git clone repo
meson setup builddir
cd builddir
meson compile
./naev.py
```

**New workflow:**
```bash
git clone repo
meson setup builddir
cd builddir
meson compile
./subspace.py    # Primary launcher now
```

**Or keep using:**
```bash
./naev.py        # Still works!
```

### For Documentation Writers

**Find and replace:**
- `naev.py` → `subspace.py` (in new docs)
- `./naev` → `./subspace` (in command examples)
- Keep `naev.py` references where noting compatibility

## Summary

✅ **Complete rebranding** from Naev to SubSpace
✅ **VS Code debugging** fully configured
✅ **Comprehensive documentation** with visual guides
✅ **Backward compatibility** maintained
✅ **Logging system** documented
✅ **Developer workflow** streamlined

**The SubSpace project is now fully rebranded and ready for development!**

## Questions?

**Q: Why keep naev.py?**
A: Backward compatibility with existing scripts and user habits.

**Q: Why is the Rust library still called libnaev.rlib?**
A: Cargo package name change requires more extensive refactoring. Coming in future release.

**Q: Do I need to update my development scripts?**
A: Not necessarily. `naev.py` still works. But we recommend switching to `subspace.py`.

**Q: Will old documentation still work?**
A: Yes, but it may reference `naev.py`. Both launchers are identical in function.

**Q: How do I debug in VS Code?**
A: Just press F5! See BUILD_GUIDE.md for details.

## Resources

- **BUILD_GUIDE.md** - Comprehensive build/launch/test guide
- **DEVELOPER_WORKFLOW.md** - Visual workflow diagrams
- **CONTRIBUTING_SUBSPACE.md** - Contribution guidelines
- **ARCHITECTURE.md** - Technical architecture details

---

**Congratulations! SubSpace is now fully rebranded! 🚀**

*SubSpace Development Team*
*Based on Naev © Naev Dev Team*
