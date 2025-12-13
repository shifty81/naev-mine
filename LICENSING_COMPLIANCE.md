# SubSpace Licensing Compliance Documentation

## Executive Summary

**Is Naev suitable for open source game development?** ✅ **YES**

**Can you make a game from Naev?** ✅ **YES**

Naev is licensed under **GNU General Public License version 3 or later (GPL-3.0-or-later)**, which is:
- ✅ A genuine open source license approved by OSI (Open Source Initiative)
- ✅ Compatible with Debian Free Software Guidelines (DFSG)
- ✅ Allows commercial and non-commercial use
- ✅ Permits modifications and derivatives
- ✅ Free to use, modify, and distribute

## Understanding the GPL-3.0-or-later License

### What You CAN Do

#### Freedom to Use
- ✅ Use the software for any purpose
- ✅ Run the program for personal use
- ✅ Use for commercial purposes
- ✅ Use in educational settings
- ✅ Use for game development

#### Freedom to Study and Modify
- ✅ Access the source code
- ✅ Study how the program works
- ✅ Modify the code to suit your needs
- ✅ Create derivative works
- ✅ Customize and rebrand

#### Freedom to Distribute
- ✅ Distribute copies of the original
- ✅ Distribute your modified versions
- ✅ Sell copies (as long as source is available)
- ✅ Give away copies for free
- ✅ Create forks of the project

#### Freedom to Share Improvements
- ✅ Share your modifications with others
- ✅ Contribute back to the community
- ✅ Publish your derivative work
- ✅ Release under GPL-3.0-or-later

### What You MUST Do (GPL Requirements)

#### 1. Preserve License
- ⚠️ **MUST** distribute under GPL-3.0-or-later
- ⚠️ **MUST** include a copy of the GPL license
- ⚠️ **MUST** keep existing copyright notices
- ⚠️ **CANNOT** change to a different license

#### 2. Provide Source Code
- ⚠️ **MUST** make source code available
- ⚠️ Source must be in a modifiable form
- ⚠️ Must provide build instructions
- ⚠️ Can distribute via repository, download, or physical media

#### 3. Document Changes
- ⚠️ **MUST** mark modified files
- ⚠️ Should include changelog or commit history
- ⚠️ Must indicate what was changed
- ⚠️ Must preserve original authors' credits

#### 4. Maintain Attribution
- ⚠️ **MUST** credit original authors (Naev Dev Team)
- ⚠️ **MUST** preserve copyright notices
- ⚠️ Should include link to original project
- ⚠️ Must acknowledge derivative status

#### 5. License Compatibility
- ⚠️ **MUST** use GPL-compatible licenses for additions
- ⚠️ Third-party libraries must be GPL-compatible
- ⚠️ Assets should use compatible licenses
- ⚠️ Cannot add proprietary components

### What You CANNOT Do

#### Licensing Restrictions
- ❌ **CANNOT** make it proprietary/closed source
- ❌ **CANNOT** add additional restrictions
- ❌ **CANNOT** remove GPL requirements
- ❌ **CANNOT** sub-license under different terms
- ❌ **CANNOT** claim original authorship

#### Distribution Restrictions
- ❌ **CANNOT** distribute without source code
- ❌ **CANNOT** distribute binaries without GPL
- ❌ **CANNOT** charge for source code access
- ❌ **CANNOT** use DRM that prevents modification

## SubSpace Specific Compliance

### How SubSpace Complies with GPL

#### Source Code Availability
```
✅ Source code repository: https://github.com/shifty81/naev-mine
✅ Full source code available
✅ Build instructions provided
✅ No hidden or proprietary components
```

#### Attribution
```
✅ Credits Naev as original work
✅ Preserves Naev copyright notices
✅ Documents derivative status
✅ Maintains original LICENSE file
```

#### License Preservation
```
✅ Licensed under GPL-3.0-or-later
✅ Includes full GPL text (gpl.txt)
✅ LICENSE file preserved and updated
✅ No conflicting licenses added
```

#### Modification Documentation
```
✅ Git history tracks all changes
✅ SUBSPACE_PROJECT.md documents changes
✅ Commit messages describe modifications
✅ Clear distinction from original Naev
```

### SubSpace License Structure

```
SubSpace Project
├── Source Code (C, Rust, Lua)
│   ├── Original Naev code: GPL-3.0-or-later (© Naev Dev Team)
│   ├── SubSpace modifications: GPL-3.0-or-later (© SubSpace Dev Team)
│   └── Must remain GPL-3.0-or-later
│
├── Graphics Assets (dat/gfx/)
│   ├── Various licenses per ARTWORK_LICENSE.yaml
│   ├── Must check individual asset licenses
│   └── Some may require attribution
│
├── Font Assets (dat/fonts/)
│   ├── Various licenses per FONT_LICENSE.yaml
│   └── Must respect font licenses
│
├── Audio Assets (dat/snd/)
│   ├── Various licenses per SOUND_LICENSE.yaml
│   └── Must respect audio licenses
│
├── Data Files (XML, etc.)
│   ├── Creative Commons Attribution-ShareAlike 4.0
│   └── Compatible with modification and distribution
│
└── Documentation
    ├── Creative Commons Attribution-ShareAlike 4.0
    └── Can be freely modified and shared
```

## Common Questions

### Q: Can I sell a game based on SubSpace/Naev?
**A: Yes!** GPL allows commercial use. However:
- You must still provide source code under GPL
- Users can redistribute it freely
- Business model should account for this (e.g., support, hosting, additional content)

### Q: Can I make my modifications private?
**A: Partially.** 
- If you only use it privately: Yes, no obligation to share
- If you distribute binaries: No, must provide source
- If you run it as a service (like a game server): Gray area, but ethically should share

### Q: Can I use proprietary assets with GPL code?
**A: Yes, with caveats.**
- Assets (art, audio) can have different licenses
- Code must remain GPL
- Asset licenses should be clearly documented
- Proprietary assets should not prevent code modification

### Q: What if I want to add a proprietary feature?
**A: You cannot.**
- All code additions must be GPL-compatible
- Cannot add DRM or usage restrictions
- Cannot make any part proprietary
- Consider if GPL aligns with your goals

### Q: Do I need permission from Naev developers?
**A: No.**
- GPL grants permission automatically
- No need to ask for authorization
- Should follow GPL requirements
- Courtesy notification is appreciated but not required

### Q: Can I rename and rebrand the game?
**A: Yes!**
- You can rebrand completely
- Must still credit original work
- Cannot claim to be official Naev
- Must indicate it's a derivative

### Q: What about contributions from others?
**A: Must be GPL-compatible.**
- Contributors must agree to GPL
- Should have contributor agreement
- All contributions become GPL
- Cannot accept proprietary contributions

## Best Practices for Compliance

### 1. Documentation
- Maintain clear CHANGELOG
- Document all major modifications
- Credit all contributors appropriately
- Keep license files up to date

### 2. Source Distribution
- Use public repository (GitHub, GitLab, etc.)
- Provide clear build instructions
- Include all dependencies or instructions to obtain them
- Make source as accessible as binaries

### 3. Attribution
- Include credits in game
- Link to original Naev project
- Acknowledge derivative status
- Credit specific contributors when using their code

### 4. Asset Management
- Track licenses for all assets
- Document asset sources
- Ensure asset compatibility
- Replace incompatible assets if necessary

### 5. Community Relations
- Be respectful to original project
- Consider contributing improvements back
- Engage with community positively
- Follow upstream developments

## Enforcement and Violations

### What Happens if You Violate GPL?
- Copyright holders can sue for infringement
- You may be required to comply or cease distribution
- Damages may be awarded
- Reputation damage in open source community

### How to Fix Violations
1. Stop distribution immediately
2. Release source code
3. Add proper licensing
4. Correct attribution
5. Resume distribution after compliance

## Resources

### GPL License
- Full Text: [gpl.txt](gpl.txt)
- Official Site: https://www.gnu.org/licenses/gpl-3.0.html
- FAQ: https://www.gnu.org/licenses/gpl-faq.html

### Compliance Guides
- FSF Compliance Guide: https://www.fsf.org/licensing/
- SPDX License List: https://spdx.org/licenses/
- Choose a License: https://choosealicense.com/

### Original Project
- Naev Website: https://naev.org
- Naev Repository: https://codeberg.org/naev/naev
- Naev License: See original LICENSE file

## Conclusion

✅ **SubSpace is fully compliant with GPL-3.0-or-later**

✅ **Naev is suitable for open source game development**

✅ **You can legally create games based on this codebase**

The GPL license provides extensive freedoms while ensuring the software remains free and open source. As long as you follow the GPL requirements (provide source, preserve license, maintain attribution), you have full rights to use, modify, and distribute this software.

---

**For questions about licensing compliance, consult:**
- A lawyer specializing in open source licensing
- Free Software Foundation: https://www.fsf.org/licensing/
- Software Freedom Law Center: https://softwarefreedom.org/

**This document is for informational purposes and does not constitute legal advice.**

---

*Last Updated: December 2025*  
*SubSpace Project Team*
