---
name: godot
description: Complete Godot Engine knowledge base combining official documentation and source code analysis
---

# Godot Skill

This skill helps with Godot Engine work, including scripting, scenes, rendering, physics, input, navigation, networking, UI, animation, audio, plugins, addons, export, XR, editor workflows, official documentation, and source code analysis.

## When to Use This Skill

This skill should be triggered when:
- Working with godot
- Asking about godot features or APIs
- Implementing godot solutions
- Debugging godot code
- Learning godot best practices

## Quick Reference

### Common Patterns

**Pattern 1:** 3D Particle system properties Emitter properties The checkbox next to the Emitting property activates and deactivates the particle system

```
Emitting
```

**Pattern 2:** Example: Emitting 32 particles with a lifetime of 4 seconds each would mean the system emits 8 particles per second

```
Interp to End
```

**Pattern 3:** Advanced Import Settings While the regular import panel provides many essential options for imported 3D models, the advanced import settings provi...

```
.res
```

**Pattern 4:** While Godot can import materials authored in 3D modeling software, the default configuration may not be suitable for your needs

```
.tres
```

**Pattern 5:** Advanced vector math Planes The dot product has another interesting property with unit vectors

```
var distance = normal.dot(point)
```

**Pattern 6:** With this in mind, let's describe a full plane as a normal N and a distance from the origin scalar D

```
var point_in_plane = N*D
```

**Pattern 7:** Android in-app purchases Godot offers a first-party GodotGooglePlayBilling Android plugin compatible with Godot 4

```
GodotGooglePlayBilling
```

**Pattern 8:** AnimatedSprite2D Inherits: Node2D < CanvasItem < Node < Object Sprite node that contains multiple textures as frames to play for animation

```
&"default"
```

## Reference Files

This skill includes comprehensive documentation in `references/`:

- **3d.md** - 3D documentation
- **api.md** - Api documentation
- **engine_details.md** - Engine Details documentation
- **getting_started.md** - Getting Started documentation
- **index.html.md** - Index.Html documentation
- **other.md** - Other documentation
- **scripting.md** - Scripting documentation
- **tutorials.md** - Tutorials documentation

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
