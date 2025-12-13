# Contributing to SubSpace

Thank you for your interest in contributing to SubSpace! This document provides guidelines for contributing to the project.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Types of Contributions](#types-of-contributions)
3. [Development Workflow](#development-workflow)
4. [Coding Standards](#coding-standards)
5. [License Requirements](#license-requirements)
6. [Community Guidelines](#community-guidelines)

## Getting Started

### Prerequisites

Before contributing, make sure you have:

1. **Read the documentation**:
   - [SUBSPACE_README.md](SUBSPACE_README.md) - Project overview
   - [SUBSPACE_PROJECT.md](SUBSPACE_PROJECT.md) - Features and roadmap
   - [LICENSING_COMPLIANCE.md](LICENSING_COMPLIANCE.md) - Licensing information
   - [ARCHITECTURE.md](ARCHITECTURE.md) - Technical architecture

2. **Set up the development environment**:
   - Install all dependencies (see [SUBSPACE_README.md](SUBSPACE_README.md))
   - Build the project successfully
   - Run the game to verify your setup

3. **Understand the license**:
   - SubSpace is GPL-3.0-or-later
   - All contributions must be GPL-compatible
   - You retain copyright but grant GPL rights

### Communication Channels

- **GitHub Issues**: Bug reports, feature requests
- **GitHub Discussions**: General discussion, questions
- **Discord**: Real-time chat (coming soon)
- **Pull Requests**: Code contributions

## Types of Contributions

### 1. Code Contributions

#### Bug Fixes
- Fix reported issues
- Add tests for the fix
- Update documentation if needed
- Reference issue number in commit

#### New Features
- Discuss in an issue first
- Follow architecture guidelines
- Include tests
- Update documentation
- Consider performance impact

#### Optimization
- Profile before optimizing
- Document performance gains
- Maintain code readability
- Avoid premature optimization

### 2. Content Contributions

#### Missions
- Write Lua mission scripts
- Follow mission template
- Test thoroughly
- Ensure story consistency
- Respect existing lore

#### Ships & Equipment
- Create XML definitions
- Balance against existing items
- Provide lore/description
- Consider gameplay impact

#### Visual Assets
- **Must use GPL-compatible license**
- Provide source files
- Match existing art style
- Optimize for performance
- Document creation tools

#### Audio Assets
- **Must use GPL-compatible license**
- Provide source files if possible
- Match audio quality standards
- Consider file size

### 3. Documentation

#### Code Documentation
- Document public APIs
- Explain complex algorithms
- Add examples
- Keep comments up to date

#### User Documentation
- Game manual improvements
- Tutorial content
- FAQ entries
- Troubleshooting guides

#### Developer Documentation
- Architecture explanations
- API references
- Build guides
- Contributing guides

### 4. Testing

#### Manual Testing
- Play test new features
- Try to break things
- Test edge cases
- Document steps to reproduce issues

#### Automated Testing
- Write unit tests
- Create integration tests
- Add performance tests
- Maintain existing tests

### 5. Translation

#### Game Text
- Translate UI strings
- Translate missions and lore
- Follow translation guidelines
- Test in game

#### Documentation
- Translate README files
- Translate user guides
- Maintain consistency

## Development Workflow

### 1. Find or Create an Issue

- Check existing issues first
- For bugs: describe steps to reproduce
- For features: explain use case and benefits
- Wait for maintainer feedback before starting

### 2. Fork and Clone

```bash
# Fork the repository on GitHub
# Then clone your fork
git clone https://github.com/YOUR_USERNAME/naev-mine.git
cd naev-mine

# Add upstream remote
git remote add upstream https://github.com/shifty81/naev-mine.git

# Initialize submodules
git submodule update --init --recursive
```

### 3. Create a Branch

```bash
# Update your main branch
git checkout main
git pull upstream main

# Create a feature branch
git checkout -b feature/your-feature-name
# or
git checkout -b fix/issue-number-description
```

**Branch Naming**:
- `feature/subspace-gates` - New feature
- `fix/123-crash-on-load` - Bug fix
- `docs/architecture-update` - Documentation
- `refactor/physics-cleanup` - Code refactoring
- `test/multiplayer-sync` - Test additions

### 4. Make Changes

#### Code Changes
```bash
# Make your changes
# Test your changes
meson compile -C builddir
./builddir/naev.py

# Run tests (when available)
meson test -C builddir
```

#### Pre-commit Checks
```bash
# Install pre-commit hooks
pre-commit install

# Run manually
pre-commit run -a
```

### 5. Commit Changes

#### Commit Message Format
```
<type>: <short summary>

<detailed description>

<references>
```

**Types**:
- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation
- `style:` - Code style (formatting, no logic change)
- `refactor:` - Code refactoring
- `test:` - Test additions or changes
- `chore:` - Maintenance tasks

**Example**:
```
feat: Add SubSpace gate construction system

Implement the ability for players to construct SubSpace gates
in systems where they have sufficient reputation and resources.

- Add gate construction UI
- Implement resource requirements
- Add faction permission checks
- Update documentation

Fixes #42
```

#### Commit Best Practices
- Make atomic commits (one logical change)
- Write clear, descriptive messages
- Reference issues when applicable
- Sign your commits (optional but recommended)

### 6. Push and Create Pull Request

```bash
# Push to your fork
git push origin feature/your-feature-name

# Create pull request on GitHub
```

#### Pull Request Description

Use this template:

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
How have you tested this?

## Screenshots (if applicable)
Add screenshots or videos

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex code
- [ ] Documentation updated
- [ ] No new warnings
- [ ] Tests added/updated
- [ ] GPL-compliant

## Related Issues
Fixes #123
Related to #456
```

### 7. Code Review Process

1. **Automated checks**: CI must pass
2. **Maintainer review**: At least one approval required
3. **Address feedback**: Make requested changes
4. **Approval**: PR approved for merge
5. **Merge**: Maintainer merges the PR

#### Responding to Feedback
- Be respectful and professional
- Ask for clarification if needed
- Explain your reasoning
- Be open to suggestions
- Update code based on feedback

## Coding Standards

### General Principles

1. **Clarity over cleverness**: Write readable code
2. **Consistency**: Follow existing patterns
3. **Documentation**: Comment complex logic
4. **Testing**: Test your code
5. **Performance**: Consider impact, but don't prematurely optimize

### C Code Style

**Based on Naev conventions**:

```c
// Use descriptive names
int subspace_gate_count;

// Function names use snake_case
void subspace_enter_gate(Player *player, Gate *gate)
{
    // Braces on same line for functions
    // Use 3-space indentation (Naev standard)
    if (gate == NULL) {
        WARN("Attempted to enter NULL gate");
        return;
    }

    // Clear logic flow
    player->in_subspace = 1;
    subspace_apply_effects(player);
}

// Constants in UPPER_CASE
#define SUBSPACE_MAX_DISTANCE 1000.0

// Structs use CamelCase
typedef struct SubSpaceGate {
    char *name;
    Vector2d pos;
    int system_dest;
} SubSpaceGate;
```

**Key Points**:
- 3-space indentation (Naev standard)
- Opening brace on same line
- Descriptive variable names
- Comment complex logic
- Check for NULL
- Use const where appropriate

### Rust Code Style

**Follow Rust conventions**:

```rust
// Use snake_case for functions and variables
fn calculate_subspace_drift(velocity: f64, time: f64) -> f64 {
    // Clear, idiomatic Rust
    let drift = velocity * time * DRIFT_FACTOR;
    drift.clamp(MIN_DRIFT, MAX_DRIFT)
}

// CamelCase for types
struct SubSpaceContext {
    state: SubSpaceState,
    entry_time: f64,
    stability: f64,
}

// Use Result for error handling
fn enter_subspace(player: &mut Player) -> Result<(), SubSpaceError> {
    if !player.has_subspace_drive() {
        return Err(SubSpaceError::NoDrive);
    }
    
    Ok(())
}
```

**Key Points**:
- Follow rustfmt
- Use clippy for linting
- Prefer Result over panic
- Document public APIs
- Write tests

### Lua Code Style

**Based on Naev mission scripts**:

```lua
-- Use snake_case
local subspace_active = false

-- Document functions
--- Enters SubSpace through a gate
-- @param player The player object
-- @param gate The gate to use
-- @return true if successful
function subspace_enter(player, gate)
    if not gate:isActive() then
        return false
    end
    
    -- Apply SubSpace effects
    player:msg("Entering SubSpace...")
    subspace_active = true
    return true
end

-- Clear logic
function update_subspace()
    if not subspace_active then
        return
    end
    
    -- Update logic here
end
```

**Key Points**:
- snake_case for variables and functions
- Document function purpose
- Use meaningful names
- Keep it simple
- Test in game

### XML Data Files

**Consistent formatting**:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<gates>
   <!-- Well-commented data -->
   <gate name="Alpha Gate">
      <pos>
         <x>1000</x>
         <y>2000</y>
      </pos>
      <stability>0.95</stability>
      <destination system="Sol" />
      <activation>
         <energy>500</energy>
         <time>10</time>
      </activation>
   </gate>
</gates>
```

**Key Points**:
- Proper indentation (3 spaces)
- Consistent attribute ordering
- Comments for complex sections
- Validate against schema

## License Requirements

### Source Code

**All source code contributions must be GPL-3.0-or-later compatible**.

Add this header to new source files:

```c
/*
 * See Licensing and Copyright notice in naev.h
 */

/**
 * @file subspace_gates.c
 * @brief SubSpace gate system implementation
 *
 * Copyright © 2025 SubSpace Dev Team
 * Based on Naev - Copyright © 2025 Naev Dev Team
 *
 * SubSpace is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 */
```

### Assets

**Graphics, audio, and other assets**:

1. **Must be GPL-compatible** (GPL, CC-BY, CC-BY-SA, Public Domain, etc.)
2. **Document the license** in asset metadata
3. **Provide attribution** for external assets
4. **Include sources** when possible (e.g., .blend files for 3D)

**Asset License Declaration**:

Create/update relevant LICENSE.yaml files:
```yaml
- file: subspace_gate.png
  license: CC-BY-SA-4.0
  author: YourName
  source: Created specifically for SubSpace
  
- file: subspace_ambient.ogg
  license: CC-BY-4.0
  author: SomeArtist
  source: https://example.com/audio
  modifications: Trimmed and normalized
```

### Contributor Agreement

By contributing, you agree that:

1. You have the right to submit the work
2. You grant GPL-3.0-or-later license to your contribution
3. You understand your work will be publicly available
4. You retain your copyright
5. You allow your contribution to be modified

**Optional: Sign your commits**:
```bash
git config user.signingkey YOUR_GPG_KEY
git commit -S -m "Your commit message"
```

## Community Guidelines

### Code of Conduct

1. **Be respectful**: Treat everyone with respect
2. **Be patient**: Remember everyone is learning
3. **Be constructive**: Provide helpful feedback
4. **Be inclusive**: Welcome diverse perspectives
5. **Be professional**: Keep discussions on-topic

### Communication Best Practices

#### In Issues and PRs
- Stay on topic
- Provide context
- Be specific
- Include examples
- Test before reporting

#### In Discussions
- Search before posting
- Use clear titles
- Tag appropriately
- Follow up on your posts
- Help others when you can

#### In Chat (Discord)
- Use appropriate channels
- Don't spam
- Respect others' time
- Be helpful
- Have fun!

### Conflict Resolution

If you experience or witness unacceptable behavior:

1. Document the incident
2. Contact project maintainers
3. Maintainers will investigate
4. Appropriate action will be taken

## Getting Help

### Where to Get Help

- **Documentation**: Read the docs first
- **GitHub Issues**: For bug reports and feature requests
- **GitHub Discussions**: For questions and discussions
- **Discord**: For real-time help (coming soon)

### How to Ask Questions

1. Search existing resources first
2. Provide context and details
3. Include error messages
4. Describe what you've tried
5. Be specific about your environment

### Mentorship

New contributors welcome! We're happy to help you get started:

- Look for "good first issue" labels
- Ask for guidance on complex tasks
- Request code reviews for learning
- Pair programming opportunities (planned)

## Recognition

### Contributors

All contributors are credited in:
- `dat/AUTHORS` - In-game credits
- GitHub contributors page
- Release notes for significant contributions

### Contribution Types Recognized

- Code contributions
- Content creation
- Documentation
- Testing and bug reports
- Community support
- Translations
- Infrastructure and tooling

## Development Resources

### Useful Links

- **Project Repository**: https://github.com/shifty81/naev-mine
- **Original Naev**: https://naev.org
- **GPL License**: https://www.gnu.org/licenses/gpl-3.0.html
- **Meson Build System**: https://mesonbuild.com
- **Lua Reference**: https://www.lua.org/manual/5.1/

### Tools and IDE Setup

#### VS Code
```json
{
    "editor.rulers": [80],
    "editor.tabSize": 3,
    "editor.insertSpaces": true,
    "[c]": {
        "editor.defaultFormatter": "xaver.clang-format"
    }
}
```

#### Vim
```vim
set tabstop=3
set shiftwidth=3
set expandtab
```

### Learning Resources

- C Programming: K&R "The C Programming Language"
- Rust: "The Rust Book" (https://doc.rust-lang.org/book/)
- Lua: "Programming in Lua" (https://www.lua.org/pil/)
- OpenGL: "Learn OpenGL" (https://learnopengl.com)

## Conclusion

Thank you for contributing to SubSpace! Your contributions help make the game better for everyone.

If you have questions about contributing, please:
- Open an issue
- Start a discussion
- Ask in Discord (coming soon)

We're excited to see what you'll contribute!

---

*Happy coding!*

*SubSpace Development Team*
