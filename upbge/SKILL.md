---
name: upbge
description: Complete UPBGE Game Engine knowledge base. Merges Official Manual with comprehensive Source Code (C++, Python, GLSL, CMake, XML).
---

# Upbge Skill

Complete upbge game engine knowledge base. merges official manual with comprehensive source code (c++, python, glsl, cmake, xml)., generated from official documentation.

## When to Use This Skill

This skill should be triggered when:
- Working with upbge
- Asking about upbge features or APIs
- Implementing upbge solutions
- Debugging upbge code
- Learning upbge best practices

## Quick Reference

### Common Patterns

**Pattern 1:** UPBGE Manual Manual Introduction Tutorials Editors Logic Bricks Logic Nodes Python Scripting Python Components Physics Data-Blocks Deployment Tools...

```
g
```

**Pattern 2:** UPBGE Manual Manual Introduction Tutorials Editors Properties Editor Logic Bricks Editor Logic Node Editor Introduction A First Example Additional ...

```
logic
```

**Pattern 3:** UPBGE Manual Manual Introduction Tutorials Getting Started Introducing Logic Bricks Introducing Logic Nodes Moving A Cube First Person Shooter 2D S...

```
level with assets
```

**Pattern 4:** UPBGE Manual Manual Introduction Tutorials Editors Logic Bricks Logic Nodes Python Scripting Introduction to Scripting Python and the Game Engine I...

```
class Damageable:
  def __init__(self, init_health: int = 100):
    self.health = init_health

  def damage(self, amount: int) -> None:
    self.health = max(0, self.health - amount)

  @property
  def destroyed(self) -> bool:
    return self.health == 0
```

**Pattern 5:** UPBGE Manual Manual Introduction Tutorials Editors Logic Bricks Logic Nodes Python Scripting Introduction to Scripting Why Script When You Can Logi...

```
001_reloadme.zip
```

**Pattern 6:** UPBGE Manual Manual Introduction Tutorials Editors Properties Editor Render Scene World Object Constraints Texture Physics Materials Data Logic Bri...

```
(0, 0, 0)
```

**Pattern 7:** UPBGE Manual Manual Introduction Tutorials Editors Logic Bricks Logic Nodes Python Scripting Introduction to Scripting Python and the Game Engine I...

```
003_template.zip
```

**Pattern 8:** UPBGE Manual Manual Introduction Tutorials Editors Logic Bricks Logic Nodes Python Scripting Python Components Physics Data-Blocks Deployment Tools...

```
.. admonition:: Reference
   :class: refbox

   :Mode:      Edit Mode
   :Menu:      :menuselection:`Curve --> Snap`
   :Shortcut:  :kbd:`Shift-S`
```

## Reference Files

This skill includes comprehensive documentation in `references/`:

- **manual.md** - Manual documentation

Use `view` to read specific reference files when detailed information is needed.

## Working with This Skill

### For Beginners
Start with the getting_started or tutorials reference files for foundational concepts.

### For Specific Features
Use the appropriate category reference file (api, guides, etc.) for detailed information.

### For Code Examples
The quick reference section above contains common patterns extracted from the official docs.

## Resources

### references/
Organized documentation extracted from official sources. These files contain:
- Detailed explanations
- Code examples with language annotations
- Links to original documentation
- Table of contents for quick navigation

### scripts/
Add helper scripts here for common automation tasks.

### assets/
Add templates, boilerplate, or example projects here.

## Notes

- This skill was automatically generated from official documentation
- Reference files preserve the structure and examples from source docs
- Code examples include language detection for better syntax highlighting
- Quick reference patterns are extracted from common usage examples in the docs

## Updating

To refresh this skill with updated documentation:
1. Re-run the scraper with the same configuration
2. The skill will be rebuilt with the latest information
