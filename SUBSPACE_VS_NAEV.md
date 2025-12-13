# SubSpace vs Naev: What's the Difference?

This document explains the relationship between SubSpace and Naev, and what makes SubSpace unique.

## Quick Answer

**SubSpace is a derivative work based on Naev**, adding new features while maintaining the solid foundation that makes Naev great.

```
Naev (Original)
    ↓
    ├─→ Fork/Derivative
    ↓
SubSpace (New Features + Naev Base)
```

## The Relationship

### What is Naev?

**Naev** is an excellent open source 2D space trading and combat game, inspired by Escape Velocity. It features:
- Open galaxy exploration
- Dynamic space combat
- Trading and economy
- Mission system
- Ship customization
- Active development since 2006

Website: https://naev.org  
License: GPL-3.0-or-later

### What is SubSpace?

**SubSpace** takes Naev as its foundation and builds upon it with:
- SubSpace dimensional travel mechanics
- Multiplayer and cooperative gameplay
- Territory control and conquest
- Enhanced crafting system
- Living universe with dynamic events
- Player-driven economy

Repository: https://github.com/shifty81/naev-mine  
License: GPL-3.0-or-later (same as Naev)

## Comparison Table

| Feature | Naev | SubSpace | Status |
|---------|------|----------|--------|
| **Core Gameplay** |
| Space Combat | ✅ | ✅ | Same |
| Trading System | ✅ | ✅ Enhanced | Planned |
| Open Galaxy | ✅ | ✅ | Same |
| Mission System | ✅ | ✅ Enhanced | Planned |
| Ship Customization | ✅ | ✅ Enhanced | Planned |
| Faction System | ✅ | ✅ Enhanced | Planned |
| **SubSpace Features** |
| Dimensional Travel | ❌ | ✅ | Planned |
| SubSpace Gates | ❌ | ✅ | Planned |
| SubSpace Hazards | ❌ | ✅ | Planned |
| **Multiplayer** |
| Single Player | ✅ | ✅ | Same |
| Multiplayer | ❌ | ✅ | Planned |
| Co-op Missions | ❌ | ✅ | Planned |
| Shared Economy | ❌ | ✅ | Planned |
| Player Trading | ❌ | ✅ | Planned |
| **Territory & Conquest** |
| Territory Control | ❌ | ✅ | Planned |
| Player Factions | ❌ | ✅ | Planned |
| Station Building | ❌ | ✅ | Planned |
| Resource Control | ❌ | ✅ | Planned |
| **Crafting** |
| Basic Crafting | Limited | ✅ | Planned |
| Blueprint System | ❌ | ✅ | Planned |
| Manufacturing | ❌ | ✅ | Planned |
| Resource Gathering | ❌ | ✅ | Planned |
| **Exploration** |
| Static Galaxy | ✅ | ✅ | Same |
| Procedural Content | Limited | ✅ | Planned |
| Archaeological Sites | ❌ | ✅ | Planned |
| Player Mapping | ❌ | ✅ | Planned |
| **Universe** |
| Dynamic Events | Limited | ✅ | Planned |
| Evolving Factions | Limited | ✅ | Planned |
| News System | ✅ | ✅ Enhanced | Planned |
| Economic Simulation | ✅ | ✅ Enhanced | Planned |
| **Technical** |
| Languages | C, Rust, Lua | C, Rust, Lua | Same |
| Engine | Custom | Custom (Naev) | Same |
| Graphics | OpenGL 3.3+ | OpenGL 3.3+ | Same |
| Platforms | Win/Linux/Mac | Win/Linux/Mac | Same |
| Plugin System | ✅ | ✅ Enhanced | Planned |
| **Community** |
| Open Source | ✅ GPL-3.0+ | ✅ GPL-3.0+ | Same |
| Active Development | ✅ | ✅ | Both |
| Community | Established | Growing | Different |

**Legend**:
- ✅ = Available
- ❌ = Not available
- Enhanced = Available with improvements
- Same = Identical to Naev
- Planned = Coming in SubSpace

## Current Status (December 2025)

### What's Available Now

**In SubSpace Today** (inherited from Naev):
- ✅ All Naev 0.13.0-beta.4 features
- ✅ Full single-player experience
- ✅ Complete trading and combat systems
- ✅ Hundreds of star systems to explore
- ✅ Dozens of ships and equipment
- ✅ Mission system and storylines

**SubSpace-Specific** (in development):
- 🔄 Project documentation and planning
- 🔄 Rebranding and identity
- 📋 SubSpace travel mechanics
- 📋 Multiplayer framework
- 📋 Territory control system
- 📋 Enhanced features

### Timeline

| Phase | Timeline | Focus |
|-------|----------|-------|
| **Phase 1** | 0-3 months | Foundation, first SubSpace features |
| **Phase 2** | 3-6 months | Core SubSpace systems, multiplayer alpha |
| **Phase 3** | 6-9 months | Content expansion, territory control |
| **Phase 4** | 9-12 months | Polish, beta release |

## Why Fork Naev?

### Why Not Just Contribute to Naev?

**Good question!** Here's why SubSpace is a separate project:

1. **Different Vision**: SubSpace focuses on multiplayer and dimensional travel, which may not align with Naev's vision
2. **Experimental Features**: We can experiment freely without affecting Naev's stability
3. **Faster Iteration**: Independent development allows rapid prototyping
4. **Community Focus**: Different target audience and gameplay style
5. **GPL Allows It**: The license explicitly permits derivative works

### Relationship with Naev

**We maintain a positive relationship with Naev**:
- ✅ Credit Naev prominently
- ✅ Follow GPL license requirements
- ✅ May contribute improvements back
- ✅ Respect Naev's project and community
- ✅ Acknowledge our derivative status

**We are NOT**:
- ❌ Competing with Naev
- ❌ Claiming to be better
- ❌ Trying to replace Naev
- ❌ Disrespecting Naev's work

**We ARE**:
- ✅ Exploring different gameplay directions
- ✅ Building on Naev's solid foundation
- ✅ Growing the space game ecosystem
- ✅ Grateful for Naev's existence

## Should You Play SubSpace or Naev?

### Play Naev if you want:
- ✅ Stable, mature game
- ✅ Single-player focus
- ✅ Traditional space trader experience
- ✅ Well-established community
- ✅ Regular releases and updates
- ✅ Proven gameplay

### Play SubSpace if you want:
- ✅ Experimental features
- ✅ Multiplayer and co-op (when ready)
- ✅ Territory control and conquest
- ✅ SubSpace dimensional mechanics
- ✅ Contribute to early development
- ✅ Influence game direction

### Play Both!
**You can play both games!** They're both open source and free. Try Naev for stable gameplay, and follow SubSpace development for new features.

## Technical Differences

### Architecture

**Naev**:
```
Traditional single-player architecture
Event-driven gameplay
Lua scripting for missions
Local save files
```

**SubSpace** (planned):
```
Client-server architecture for multiplayer
Enhanced event system
Extended Lua API
Cloud save support (optional)
Multiplayer synchronization
```

### Performance

**Naev**:
- Optimized for single-player
- ~500 ships maximum
- 60+ FPS typical
- ~500MB memory

**SubSpace** (target):
- Optimized for multiplayer
- ~500 ships per player view
- 60+ FPS target
- ~600MB memory (with multiplayer)

### Data Structure

**Naev**:
```
XML data files
Static galaxy definition
Event-based changes
```

**SubSpace** (planned):
```
XML + dynamic data
Procedural content support
Persistent universe state
Player-driven changes
```

## Can I Convert Between Games?

### Naev → SubSpace

**Currently**: SubSpace uses Naev data, so Naev content works in SubSpace.

**Future**: When SubSpace adds unique features, saves may not be fully compatible.

### SubSpace → Naev

**No**: SubSpace features won't work in Naev. SubSpace saves can't be loaded in Naev.

## Contributing

### Contributing to Naev

If you want to contribute to Naev:
- Visit https://naev.org
- Check https://codeberg.org/naev/naev
- Follow their contribution guidelines

### Contributing to SubSpace

If you want to contribute to SubSpace:
- Visit https://github.com/shifty81/naev-mine
- Read [CONTRIBUTING_SUBSPACE.md](CONTRIBUTING_SUBSPACE.md)
- Join our community (Discord coming soon)

### Contributing to Both

**You can contribute to both projects!** The licenses allow it, and cross-pollination of ideas benefits both communities.

## Licensing

### Both Projects

- **License**: GPL-3.0-or-later
- **Open Source**: Yes
- **Free**: Yes (freedom and price)
- **Derivatives Allowed**: Yes
- **Commercial Use**: Yes

### Key Points

1. **SubSpace is legal**: GPL explicitly allows derivative works
2. **No permission needed**: License grants rights automatically
3. **Attribution required**: Must credit Naev
4. **Source code required**: Must provide source under GPL
5. **Same license**: SubSpace must also be GPL-3.0-or-later

See [LICENSING_COMPLIANCE.md](LICENSING_COMPLIANCE.md) for details.

## Community

### Naev Community

- **Website**: https://naev.org
- **Repository**: https://codeberg.org/naev/naev
- **Discord**: https://discord.gg/nd2M5BR (check website for current invite)
- **Forums**: Via website
- **Active since**: 2006

### SubSpace Community

- **Repository**: https://github.com/shifty81/naev-mine
- **Issues**: https://github.com/shifty81/naev-mine/issues
- **Discussions**: https://github.com/shifty81/naev-mine/discussions
- **Discord**: Coming soon
- **Active since**: 2025

### Bridge Both Communities

We encourage positive interaction between communities:
- Share knowledge and experiences
- Respect both projects
- Learn from each other
- Celebrate space games!

## FAQ

### Is SubSpace trying to replace Naev?

**No!** SubSpace explores different gameplay directions. Both projects can coexist and thrive.

### Will SubSpace features be added to Naev?

**Maybe!** If Naev developers want to adopt SubSpace features, we'd be honored. The GPL allows it, and we'd welcome the cross-pollination.

### Can I use SubSpace mods in Naev?

**Depends on the mod.** If it only uses Naev features, probably yes. If it uses SubSpace-specific features, no.

### Does SubSpace get Naev updates?

**We can merge them**, but must do so manually. SubSpace will diverge over time, so updates may require adaptation.

### Which has better performance?

**Currently the same.** SubSpace is based on Naev. Future SubSpace features may impact performance, but we'll optimize.

### Which has more content?

**Currently the same.** SubSpace starts with all Naev content. SubSpace-specific content is being developed.

### Can I switch between them?

**Yes!** Install both and play both. They're separate games with separate save files.

## Acknowledgments

### To Naev

Thank you to the Naev Development Team and all contributors for creating such an excellent foundation. SubSpace would not exist without your hard work and dedication to open source.

**Naev Credits**:
- Edgar Simo-Serra (@bobbens) and the entire Naev Dev Team
- All contributors over the years
- The open source community

### To Open Source

Thank you to the open source movement for making projects like this possible. The GPL license enables derivative works, fostering innovation and community.

## Conclusion

### Summary

**SubSpace and Naev**:
- Share a common foundation
- Explore different directions
- Both are open source and free
- Both welcome contributors
- Both celebrate space games!

**SubSpace is**:
- A derivative work (legal and acknowledged)
- An experiment in new features
- A community-driven project
- Respectful of Naev's legacy
- Excited about the future!

### Final Thoughts

If you love space games, both Naev and SubSpace have something to offer. Try them both, contribute to both, enjoy both!

The more space games, the better for everyone! 🚀

---

**Links**:
- **SubSpace**: https://github.com/shifty81/naev-mine
- **Naev**: https://naev.org

**Documentation**:
- [QUICKSTART.md](QUICKSTART.md) - Get started quickly
- [SUBSPACE_README.md](SUBSPACE_README.md) - Full SubSpace info
- [SUBSPACE_PROJECT.md](SUBSPACE_PROJECT.md) - Project details
- [LICENSING_COMPLIANCE.md](LICENSING_COMPLIANCE.md) - Legal info

---

*"Standing on the shoulders of giants"*  
*SubSpace Development Team*
