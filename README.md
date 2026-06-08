# CG Skills

This repo is a collection of agentic workflow skills for 3D, computer graphics, VFX and game development work.

It is meant to give agents useful local context for common 3d, game engine, and tool workflow questions. Each skill folder includes a `SKILL.md` file and a set of reference notes pulled from the related documentation. The notes are organized by topic so the agent can load only the parts that matter for the current task.

## What is included

- `blender` covers Blender workflows like modeling, animation, rendering, shading, compositing, video editing, and Python scripting.
- `godot` covers Godot Engine topics like scripting, scenes, rendering, physics, input, export, plugins, and editor workflows.
- `unreal-engine` covers Unreal Engine topics like Blueprints, C++, rendering, animation, gameplay systems, editor tools, optimization, and deployment.
- `upbge` covers UPBGE and Blender game engine style workflows.

## How it is used

These folders are intended to be installed or referenced as agents skills. When a task matches one of the tools, agents can read the related skill file and pull in the reference notes it needs.

To install it locally, put this repo under `~/.agents/skills/CG-Skills`.

That means you can ask for help with things like a Blender Python operator, a Godot gameplay script, an Unreal material setup, or a general engine workflow, and the agent has a better starting point than memory alone.

## Repo layout

Each skill follows the same basic layout.

```text
tool-name/
  SKILL.md
  references/
```

`SKILL.md` describes when the skill should be used. The `references` folder holds the larger notes grouped by topic.

## Notes

This is not a full replacement for the official docs. It is a practical local reference set for agent work, quick lookups, and project help.

The content may be refreshed over time as the tools and engines change.
