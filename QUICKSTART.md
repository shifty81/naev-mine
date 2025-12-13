# SubSpace Quick Start Guide

Welcome to SubSpace! This guide will help you get up and running quickly.

## For the Impatient

```bash
# Clone the repo
git clone https://github.com/shifty81/naev-mine.git subspace
cd subspace

# Get artwork
git submodule update --init --recursive

# Build (requires dependencies)
meson setup builddir
cd builddir
meson compile

# Run
./naev.py
```

**Note**: Currently runs as Naev - SubSpace features are under development!

## What is SubSpace?

SubSpace is an **open source 2D space trading and combat game** based on Naev, featuring:

🚀 **Space Exploration** - Hundreds of star systems  
⚔️ **Dynamic Combat** - Top-down space battles  
💰 **Trading & Economy** - Buy low, sell high  
🌀 **SubSpace Travel** - Dimensional corridors (coming soon)  
👥 **Multiplayer** - Cooperative gameplay (planned)  
🏰 **Territory Control** - Build your empire (planned)

## Is This Free & Open Source?

**YES!** 100% free and open source.

- **License**: GPL-3.0-or-later
- **Free to**: Use, modify, distribute, even commercially
- **Requirements**: Keep it open source, credit authors

See [LICENSING_COMPLIANCE.md](LICENSING_COMPLIANCE.md) for details.

## Can I Make a Game From This?

**YES!** That's exactly what we're doing!

The GPL-3.0-or-later license allows you to:
- ✅ Create derivative games
- ✅ Rebrand and customize
- ✅ Distribute freely or sell
- ✅ Modify any part of the code

Just remember to:
- ⚠️ Keep source code available
- ⚠️ Use GPL-3.0-or-later license
- ⚠️ Credit original authors

## Documentation Map

### Start Here
- **This file (QUICKSTART.md)** - You are here!
- **[SUBSPACE_README.md](SUBSPACE_README.md)** - Full project overview
- **[PROJECT_SUMMARY.md](PROJECT_SUMMARY.md)** - Executive summary

### For Users
- **[SUBSPACE_README.md](SUBSPACE_README.md)** - How to play
- **Original Readme.md** - Naev documentation

### For Developers
- **[CONTRIBUTING_SUBSPACE.md](CONTRIBUTING_SUBSPACE.md)** - How to contribute
- **[ARCHITECTURE.md](ARCHITECTURE.md)** - Technical details
- **[FEATURES_BRAINSTORM.md](FEATURES_BRAINSTORM.md)** - Feature ideas

### For Legal/Business
- **[LICENSING_COMPLIANCE.md](LICENSING_COMPLIANCE.md)** - License guide
- **[LICENSE](LICENSE)** - Full license text
- **[gpl.txt](gpl.txt)** - GPL text

### For Project Management
- **[SUBSPACE_PROJECT.md](SUBSPACE_PROJECT.md)** - Project overview
- **[PROJECT_SUMMARY.md](PROJECT_SUMMARY.md)** - Status summary

## Current Status

**Phase**: Foundation & Early Development

**What Works**:
- ✅ All original Naev features
- ✅ Single-player gameplay
- ✅ Trading and combat
- ✅ Missions and storylines
- ✅ Ship customization

**What's Coming** (SubSpace-specific):
- 🔄 SubSpace travel mechanics
- 🔄 Multiplayer support
- 📋 Territory control
- 📋 Enhanced crafting
- 📋 Living universe features

## Installation

### Prerequisites

You need these installed:
- **Rust** 1.88+
- **Meson** build system
- **SDL3**, libxml2, freetype2, OpenAL, etc.

See [SUBSPACE_README.md](SUBSPACE_README.md) for full dependency list.

### Quick Install (Linux/macOS)

```bash
# Clone
git clone https://github.com/shifty81/naev-mine.git subspace
cd subspace

# Get artwork submodule
git submodule update --init --recursive

# Configure build
meson setup builddir

# Compile
cd builddir
meson compile

# Run
./naev.py
```

### Windows

See [Naev Windows Compilation Guide](https://codeberg.org/naev/naev/wiki/Compiling-on-Windows)

### Pre-built Binaries

Coming soon! For now, build from source.

## First Steps

### 1. Start a New Game

Launch SubSpace and start a new game. Choose your:
- Ship
- Starting location
- Difficulty

### 2. Learn the Basics

- **WASD** or **Arrow Keys**: Move
- **Mouse**: Aim and target
- **Space**: Primary weapon
- **Tab**: Target nearest enemy
- **L**: Land on planets
- **M**: Open map

### 3. Take Your First Mission

- Land on a planet
- Visit the Mission Computer
- Accept a simple mission
- Complete it for credits

### 4. Explore!

The galaxy is yours. Trade, fight, or explore as you wish!

## Getting Help

### In-Game Help

Press **F1** in-game for help.

### Documentation

- Check the docs in the `docs/` folder
- Visit original Naev docs: https://naev.org

### Community

- **GitHub Issues**: https://github.com/shifty81/naev-mine/issues
- **Discussions**: https://github.com/shifty81/naev-mine/discussions
- **Discord**: Coming soon!

### Common Issues

**Q: Build fails with missing dependencies**  
A: Install all dependencies listed in [SUBSPACE_README.md](SUBSPACE_README.md)

**Q: Game crashes on start**  
A: Check that artwork submodule is initialized: `git submodule update --init --recursive`

**Q: Controls don't work**  
A: Check Options → Input settings. Reset to defaults if needed.

**Q: Where are SubSpace features?**  
A: Currently in development! You're playing Naev with SubSpace docs. SubSpace features coming in future releases.

## Contributing

Want to help? Great! Here's how:

### Non-Developers

- **Test & Report Bugs**: Play and report issues
- **Suggest Features**: Share your ideas
- **Spread the Word**: Tell others about SubSpace
- **Create Content**: Write guides, tutorials, videos

### Developers

1. Read [CONTRIBUTING_SUBSPACE.md](CONTRIBUTING_SUBSPACE.md)
2. Check [GitHub Issues](https://github.com/shifty81/naev-mine/issues)
3. Fork the repo
4. Make changes
5. Submit pull request

### Content Creators

- **Missions**: Write Lua scripts
- **Ships**: Create XML definitions
- **Art**: Make sprites (GPL-compatible)
- **Audio**: Create sounds/music (GPL-compatible)

See [CONTRIBUTING_SUBSPACE.md](CONTRIBUTING_SUBSPACE.md) for details.

## FAQ

### General

**Q: What is SubSpace?**  
A: An open source 2D space game based on Naev, with unique SubSpace travel mechanics and multiplayer features.

**Q: Is it free?**  
A: Yes! Free as in freedom AND free as in beer.

**Q: Can I play it now?**  
A: Yes! It currently has all Naev features. SubSpace-specific features are coming.

**Q: When will SubSpace features be ready?**  
A: We're in early development. Check roadmap in [SUBSPACE_PROJECT.md](SUBSPACE_PROJECT.md).

### Technical

**Q: What platforms are supported?**  
A: Linux, Windows, macOS. Same as Naev.

**Q: What are the system requirements?**  
A: Modest - any PC from the last 10 years should work. Needs OpenGL 3.3+.

**Q: Can I mod it?**  
A: Yes! It has a plugin system. More modding support coming.

### Legal

**Q: Is it really open source?**  
A: Yes! GPL-3.0-or-later license. See [LICENSING_COMPLIANCE.md](LICENSING_COMPLIANCE.md).

**Q: Can I use this for my own game?**  
A: Yes! As long as you comply with GPL (keep it open source, credit authors).

**Q: Can I sell it?**  
A: Yes! GPL allows commercial use. But you must provide source code.

### Development

**Q: How can I contribute?**  
A: See [CONTRIBUTING_SUBSPACE.md](CONTRIBUTING_SUBSPACE.md). Code, content, testing, docs - all welcome!

**Q: What skills do I need?**  
A: Depends on what you want to do! C/Rust/Lua for code, art for graphics, etc.

**Q: Is there a roadmap?**  
A: Yes! See [SUBSPACE_PROJECT.md](SUBSPACE_PROJECT.md) and [PROJECT_SUMMARY.md](PROJECT_SUMMARY.md).

## What's Next?

### For Players

1. **Play the current version** (Naev features)
2. **Provide feedback** on what you'd like to see
3. **Join the community** (Discord coming soon)
4. **Try multiplayer** when it's ready

### For Contributors

1. **Read the docs** (especially [CONTRIBUTING_SUBSPACE.md](CONTRIBUTING_SUBSPACE.md))
2. **Pick an issue** or propose a feature
3. **Submit your contribution**
4. **Engage with the community**

### For the Project

**Short-term** (0-3 months):
- Complete rebranding
- First SubSpace prototype
- Community building

**Mid-term** (3-6 months):
- SubSpace travel working
- Multiplayer alpha
- Territory basics

**Long-term** (6-12 months):
- Beta release
- Full feature set
- Growing player base

## Resources

### Essential Links

- **Repository**: https://github.com/shifty81/naev-mine
- **Issues**: https://github.com/shifty81/naev-mine/issues
- **Discussions**: https://github.com/shifty81/naev-mine/discussions
- **Original Naev**: https://naev.org

### Documentation

All documentation is in the repository root:

- `QUICKSTART.md` ← You are here
- `SUBSPACE_README.md` - Full README
- `SUBSPACE_PROJECT.md` - Project details
- `LICENSING_COMPLIANCE.md` - License info
- `FEATURES_BRAINSTORM.md` - Feature ideas
- `ARCHITECTURE.md` - Technical architecture
- `CONTRIBUTING_SUBSPACE.md` - Contribution guide
- `PROJECT_SUMMARY.md` - Project summary

### Learning Resources

- **Naev Manual**: In `docs/manual/`
- **Lua API**: https://naev.org/api/
- **Naev Wiki**: https://codeberg.org/naev/naev/wiki
- **GPL Guide**: https://www.gnu.org/licenses/gpl-3.0.html

## Final Notes

### This is Early Days

SubSpace is in **early development**. Things will change, improve, and grow. Be patient and join us on this journey!

### We Need You

Open source thrives on community. Whether you:
- Code
- Create content
- Test
- Document
- Spread the word
- Just play and have fun

**You are valuable to this project!**

### Stay in Touch

- Star the repo on GitHub
- Watch for updates
- Join discussions
- Contribute when you can

### Thank You

Thank you for your interest in SubSpace!

Special thanks to:
- **Naev Dev Team** - For the excellent foundation
- **Open Source Community** - For making projects like this possible
- **You** - For reading this and being interested!

---

**Ready to start your adventure in SubSpace?**

```bash
git clone https://github.com/shifty81/naev-mine.git subspace
cd subspace
git submodule update --init --recursive
meson setup builddir && cd builddir && meson compile
./naev.py
```

**See you in space! 🚀**

---

*SubSpace Development Team*  
*"Exploring dimensions, building universes"*
