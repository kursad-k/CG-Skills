# Godot - Index.Html

**Pages:** 15

---

## All classes — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/classes/index.html

**Contents:**
- All classes
- Globals
- Nodes
- Resources
- Other objects
- Editor-only
- Variant types

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Asset Library — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/community/asset_library/index.html

**Contents:**
- Asset Library

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Building from source — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/index.html

**Contents:**
- Building from source
- Basics of building Godot
- Building for target platforms
- Other compilation targets and options

Godot prides itself on being very easy to build, by C++ project standards. Godot uses the SCons build system, and after the initial setup compiling the engine for your current platform should be as easy as running:

But you will probably need to use at least some of the available options to configure the build to match your specific needs, be it a custom engine fork, a lightweight build stripped of extra modules, or an executable targeting engine development.

The articles below should help you navigate configuration options available, as well as prerequisites required to compile Godot exactly the way you need.

Let's start with basics, and learn how to get Godot's source code, and then which options to use to compile it regardless of your target platform.

Below you can find instructions for compiling the engine for your specific target platform. Note that Godot supports cross-compilation, which means you can compile it for a target platform that doesn't match your current platform (say, target Linux while being on Windows). The guides will try their best to cover all possible situations.

Some additional universal compilation options require further setup. Namely, while Godot does have C#/.NET support as a part of its main codebase, it does not get compiled by default to reduce the executable size for users who don't need C# for their projects.

Articles below explain how to configure the buildsystem for cases like this, and also cover some optimization techniques.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Class reference primer — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/class_reference/index.html

**Contents:**
- Class reference primer
- How to edit class XML
  - Improve formatting with BBCode style tags
    - Linking
    - Formatting text
    - Formatting code blocks
    - Formatting notes and warnings
  - Marking API as deprecated/experimental
- User-contributed notes

This page explains how to write the class reference. You will learn where to write new descriptions for the classes, methods, and properties for Godot's built-in node types.

To learn to submit your changes to the Godot project using the Git version control system, see Class reference contribution documentation.

The reference for each class is contained in an XML file like the one below:

It starts with brief and long descriptions. In the generated docs, the brief description is always at the top of the page, while the long description lies below the list of methods, variables, and constants. You can find methods, member variables, constants, and signals in separate XML nodes.

For each, you want to learn how they work in Godot's source code. Then, fill their documentation by completing or improving the text in these tags:

<method> (in its <description> tag; return types and arguments don't take separate documentation strings)

<signal> (in its <description> tag; arguments don't take separate documentation strings)

Write in a clear and simple language. Always follow the writing guidelines to keep your descriptions short and easy to read. Do not leave empty lines in the descriptions: each line in the XML file will result in a new paragraph, even if it is empty.

Edit the file for your chosen class in doc/classes/ to update the class reference. The folder contains an XML file for each class. The XML lists the constants and methods you will find in the class reference. Godot generates and updates the XML automatically.

For some modules in the engine's source code, you'll find the XML files in the modules/<module_name>/doc_classes/ directory instead.

Edit it using your favorite text editor. If you use a code editor, make sure that it doesn't change the indent style: you should use tabs for the XML and four spaces inside BBCode-style blocks. More on that below.

To check that the modifications you've made are correct in the generated documentation, navigate to the doc/ folder and run the command make rst. This will convert the XML files to the online documentation's format and output errors if anything's wrong.

Alternatively, you can build Godot and open the modified page in the built-in code reference. To learn how to compile the engine, read the compilation guide.

We recommend using a code editor that supports XML files like Vim, Atom, Visual Studio Code, Notepad++, or another to comfortably edit the file. You can also use their search feature to find classes and properties quickly.

If you use Visual Studio Code, you can install the vscode-xml extension to get linting for class reference XML files.

Godot's XML class reference supports BBCode-like tags for linking as well as formatting text and code. In the tables below you can find the available tags, usage examples and the results after conversion to reStructuredText.

Whenever you link to a member of another class, you need to specify the class name. For links to the same class, the class name is optional and can be omitted.

See [annotation @GDScript.@rpc].

See [constant Color.RED].

See [enum Mesh.ArrayType].

Get [member Node2D.scale].

Call [method Node3D.hide].

Use [constructor Color.Color].

Use [operator Color.operator *].

Use Color.operator *.

Emit [signal Node.renamed].

See [theme_item Label.font].

Takes [param size] for the size.

Takes size for the size.

Currently only @GDScript has annotations.

[lb]b[rb]text[lb]/b[rb]

Do [b]not[/b] call this method.

Do not call this method.

Returns the [i]global[/i] position.

Returns the global position.

[u]Always[/u] use this method.

[s]Outdated information.[/s]

[center]2 + 2 = 4[/center]

Press [kbd]Ctrl + C[/kbd].

Returns [code]true[/code].

Some supported tags like [color] and [font] are not listed here because they are not recommended in the engine documentation.

[kbd] disables BBCode until the parser encounters [/kbd].

[code] disables BBCode until the parser encounters [/code].

There are two options for formatting code blocks:

Use [codeblock] if you want to add an example for a specific language.

Use [codeblocks], [gdscript], and [csharp] if you want to add the same example for both languages, GDScript and C#.

By default, [codeblock] highlights GDScript syntax. You can change it using the lang attribute. Currently supported options are:

[codeblock lang=text] disables syntax highlighting;

[codeblock lang=gdscript] highlights GDScript syntax;

[codeblock lang=csharp] highlights C# syntax (only in .NET version).

[codeblock] disables BBCode until the parser encounters [/codeblock].

Use [codeblock] for pre-formatted code blocks. Since Godot 4.5, tabs should be used for indentation.

If you need to have different code version in GDScript and C#, use [codeblocks] instead. If you use [codeblocks], you also need to have at least one of the language-specific tags, [gdscript] and [csharp].

Always write GDScript code examples first! You can use this experimental code translation tool to speed up your workflow.

The above will display as:

To denote important information, add a paragraph starting with "[b]Note:[/b]" at the end of the description:

To denote crucial information that could cause security issues or loss of data if not followed carefully, add a paragraph starting with "[b]Warning:[/b]" at the end of the description:

In all the paragraphs described above, make sure the punctuation is part of the BBCode tags for consistency.

To mark an API as deprecated or experimental, you need to add the corresponding XML attribute. The attribute value must be a message explaining why the API is not recommended (BBCode markup is supported) or an empty string (the default message will be used). If an API element is marked as deprecated/experimental, then it is considered documented even if the description is empty.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Configuring an IDE — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/configuring_an_ide/index.html

**Contents:**
- Configuring an IDE

We assume that you have already cloned and compiled Godot.

You can easily develop Godot with any text editor and by invoking scons on the command line, but if you want to work with an IDE (Integrated Development Environment), here are setup instructions for some popular ones:

It is possible to use other IDEs, but their setup is not documented yet.

If your editor supports the language server protocol, you can use clangd for completion, diagnostics, and more. You can generate a compilation database for use with clangd one of two ways:

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Debugging and profiling — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/debugging/index.html

**Contents:**
- Debugging and profiling
- Debugging the editor

This section contains pages that provide guidance if you're looking at the engine code trying to find an underlying issue or an optimization possibility.

When working on the Godot editor keep in mind that by default the executable will start in the Project Manager mode. Opening a project from the Project Manager spawns a new process, which stops the debugging session. To avoid that you should launch directly into the project using -e and --path launch options.

For example, using gdb directly, you may do this:

You can also run the editor directly from your project's folder. In that case, only the -e option is required.

You can learn more about these launch options and other command line arguments in the command line tutorial.

If you're using a code editor or an IDE to debug Godot, check out our configuration guides, which cover the setup process for building and debugging with your particular editor.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Editor development — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/editor/index.html

**Contents:**
- Editor development

This section documents how to work with the source code of the Godot editor. When contributing to the Godot engine, you should also read the editor style guide.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Engine architecture — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/index.html

**Contents:**
- Engine architecture
- Getting started with Godot's source code
- Extending Godot by modifying its source code

The following pages are meant to introduce the global organization of Godot Engine's source code, and give useful tips for extending and fixing the engine on the C++ side.

This section covers the basics that you will encounter in (almost) every source file.

This section covers what you can do by modifying Godot's C++ source code.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Engine development — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/index.html

**Contents:**
- Engine development

The guides below explain how to work on the engine's codebase. If you plan to contribute to the engine, please make sure to also read the contribution guidelines.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Godot file formats — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/file_formats/index.html

**Contents:**
- Godot file formats

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Introduction — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/introduction/index.html

**Contents:**
- Introduction

This series will introduce you to Godot and give you an overview of its features.

In the following pages, you will get answers to questions such as "Is Godot for me?" or "What can I do with Godot?". We will then introduce the engine's most essential concepts, run you through the editor's interface, and give you tips to make the most of your time learning it.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Step by step — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/step_by_step/index.html

**Contents:**
- Step by step

This series builds upon the Introduction to Godot and will get you started with the editor and the engine. You will learn more about nodes and scenes, code your first classes with GDScript, use signals to make nodes communicate with one another, and more.

The following lessons are here to prepare you for Your first 2D game, a step-by-step tutorial where you will code a game from scratch. By the end of it, you will have the necessary foundations to explore more features in other sections. We also included links to pages that cover a given topic in-depth where appropriate.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Vulkan — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/debugging/vulkan/index.html

**Contents:**
- Vulkan

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Your first 2D game — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/first_2d_game/index.html

**Contents:**
- Your first 2D game
- Prerequisites
- Contents

In this step-by-step tutorial series, you will create your first complete 2D game with Godot. By the end of the series, you will have a simple yet complete game of your own, like the image below.

You will learn how the Godot editor works, how to structure a project, and build a 2D game.

This project is an introduction to the Godot engine. It assumes that you have some programming experience already. If you're new to programming entirely, you should start here: Scripting languages.

The game is called "Dodge the Creeps!". Your character must move and avoid the enemies for as long as possible.

Create a complete 2D game with the Godot editor.

Structure a simple game project.

Move the player character and change its sprite.

Spawn random enemies.

You'll find another series where you'll create a similar game but in 3D. We recommend you to start with this one, though.

If you are new to game development or unfamiliar with Godot, we recommend starting with 2D games. This will allow you to become comfortable with both before tackling 3D games, which tend to be more complicated.

You can find a completed version of this project at this location:

https://github.com/godotengine/godot-demo-projects/tree/master/2d/dodge_the_creeps

This step-by-step tutorial is intended for beginners who followed the complete Step by step.

If you're an experienced programmer, you can find the complete demo's source code here: Dodge the Creeps source code.

We prepared some game assets you'll need to download so we can jump straight to the code.

You can download them by clicking the link below.

dodge_the_creeps_2d_assets.zip.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Your first 3D game — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/first_3d_game/index.html

**Contents:**
- Your first 3D game
- Contents

In this step-by-step tutorial series, you will create your first complete 3D game with Godot. By the end of the series, you will have a simple yet finished project of your own like the animated gif below.

The game we'll code here is similar to Your first 2D game, with a twist: you can now jump and your goal is to squash the creeps. This way, you will both recognize patterns you learned in the previous tutorial and build upon them with new code and features.

Work with 3D coordinates with a jumping mechanic.

Use kinematic bodies to move 3D characters and detect when and how they collide.

Use physics layers and a group to detect interactions with specific entities.

Code basic procedural gameplay by instancing monsters at regular time intervals.

Design a movement animation and change its speed at runtime.

Draw a user interface on a 3D game.

This tutorial is for beginners who followed the complete getting started series. We'll start slow with detailed instructions and shorten them as we do similar steps. If you're an experienced programmer, you can browse the complete demo's source code here: Squash the Creep source code.

You can follow this series without having done the 2D one. However, if you're new to game development, we recommend you to start with 2D. 3D game code is always more complex and the 2D series will give you foundations to follow along more comfortably.

We prepared some game assets so we can jump straight to the code. You can download them here: Squash the Creeps assets.

We will first work on a basic prototype for the player's movement. We will then add the monsters that we'll spawn randomly around the screen. After that, we'll implement the jump and squashing mechanic before refining the game with some nice animation. We'll wrap up with the score and the retry screen.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---
