# Unreal-Engine - Getting Started

**Pages:** 11

---

## Directory Structure

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-directory-structure

**Contents:**
- Directory Structure
- Root Directory
- Common Directories
  - Modules and Plugins
- Engine-specific Directories
- Game Project Directories
- Solution Directories

Overview of the directories that make up the engine and game projects.

At the top level, there is the Engine directory as well as any game projects you have. The Engine directory contains the engine itself and all of the tools that come with it. Each game folder contains all of the files pertaining to that game.

Some subdirectories are common amongst both the Engine and game project directories:

Some directories exist both in the engine's common directories and specific game directories. For example, the Content directory might exist in both the engine directory (../Engine/Content) and in your game directory (../GAME_DIR/Content). Files in your game's content directory are only accessible within that particular game whereas files contained in the engine's content directory is accessible by any project that uses that particular engine distribution.

Unreal Engine functionality is organized into many modules and plugins. One of the primary differences between modules and plugins is that modules only contain code. As an example, when you create a project in Unreal Engine, your project source code is organized into a module with a *.Build.cs file. Plugins contain their own source files, binaries, and a .uplugin file. Plugins can also contain assets whereas modules cannot. As a result of this, you can redistribute your plugin to use it in other UE projects.

For more information about modules, plugins, and the distinctions between the two, see the Modules and Plugins documentation pages.

Some subdirectories are specific to the Engine directory:



---

## Understanding the Basics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-the-basics-of-unreal-engine?application_version=5.2

**Contents:**
- Understanding the Basics
- Installing Unreal Engine
- Foundational Knowledge
- Content Browser
- Customizing Unreal Engine
- Working with Projects and Templates
- Levels
- Assets and Content Packs
- Actors and Components
- Playing and Simulating

Essential skills and concepts to help you get started in Unreal Engine.

This section covers the fundamentals of Unreal Engine 5 (UE5) and its tools. If you are new to UE5, you should become familiar with the Unreal Editor interface, Blueprint visual scripting, and the types of content you can use inside an Unreal project.

Refer to the sections below to see what kind of UE5 skills you can learn.

Learn how to download and install Unreal Engine, and get acquainted with the Unreal Engine 5 system requirements for Windows, macOS, and Linux.

Become familiar with the major components of the Unreal Editor interface, the various tools and editors you can use, and the most common Unreal Engine terms.

Learn how to work with Assets in the Content Browser, which is the primary area of the Unreal Editor for creating, importing, organizing, viewing, and managing content.

Customize Unreal Engine's layout, keybindings, and behavior, and learn how to add useful features by enabling plugins.

Learn how to work with Unreal projects, which hold the contents of anything you build in Unreal Engine. You can also read about two of the basic project templates that Unreal Engine offers, which serve as starting points for a first-person or third-person experience.

Levels (sometimes called Maps) contain everything a player can see and interact with, like environments, usable objects, other characters, and so on. Every Unreal Engine project contains at least one Level. Read more about how to create and manage Levels on the pages below.

Any piece of content in an Unreal Engine project is called an Asset. Read more about how to work with Assets on the pages below.

At a more granular level, Unreal projects contain Actors (individual pieces of content) which can have one or more Components attached to them. The pages below can teach you more about Actors and Components.

Learn how to test your content directly inside Unreal Editor.

Package your application for different platforms.



---

## Understanding the Basics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-the-basics-of-unreal-engine?application_version=5.0

**Contents:**
- Understanding the Basics
- Installing Unreal Engine
- Foundational Knowledge
- Content Browser
- Customizing Unreal Engine
- Working with Projects and Templates
- Levels
- Assets and Content Packs
- Actors and Components
- Playing and Simulating

Essential skills and concepts to help you get started in Unreal Engine.

This section covers the fundamentals of Unreal Engine 5 (UE5) and its tools. If you are new to UE5, you should become familiar with the Unreal Editor interface, Blueprint visual scripting, and the types of content you can use inside an Unreal project.

Refer to the sections below to see what kind of UE5 skills you can learn.

Learn how to download and install Unreal Engine, and get acquainted with the Unreal Engine 5 system requirements for Windows, macOS, and Linux.

Become familiar with the major components of the Unreal Editor interface, the various tools and editors you can use, and the most common Unreal Engine terms.

Learn how to work with Assets in the Content Browser, which is the primary area of the Unreal Editor for creating, importing, organizing, viewing, and managing content.

Customize Unreal Engine's layout, keybindings, and behavior, and learn how to add useful features by enabling plugins.

Learn how to work with Unreal projects, which hold the contents of anything you build in Unreal Engine. You can also read about two of the basic project templates that Unreal Engine offers, which serve as starting points for a first-person or third-person experience.

Levels (sometimes called Maps) contain everything a player can see and interact with, like environments, usable objects, other characters, and so on. Every Unreal Engine project contains at least one Level. Read more about how to create and manage Levels on the pages below.

Any piece of content in an Unreal Engine project is called an Asset. Read more about how to work with Assets on the pages below.

At a more granular level, Unreal projects contain Actors (individual pieces of content) which can have one or more Components attached to them. The pages below can teach you more about Actors and Components.

Learn how to test your content directly inside Unreal Editor.

Package your application for different platforms.



---

## Understanding the Basics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-the-basics-of-unreal-engine?application_version=5.4

**Contents:**
- Understanding the Basics
- Installing Unreal Engine
- Foundational Knowledge
- Content Browser
- Customizing Unreal Engine
- Working with Projects and Templates
- Levels
- Assets and Content Packs
- Actors and Components
- Playing and Simulating

Essential skills and concepts to help you get started in Unreal Engine.

This section covers the fundamentals of Unreal Engine 5 (UE5) and its tools. If you are new to UE5, you should become familiar with the Unreal Editor interface, Blueprint visual scripting, and the types of content you can use inside an Unreal project.

Refer to the sections below to see what kind of UE5 skills you can learn.

Learn how to download and install Unreal Engine, and get acquainted with the Unreal Engine 5 system requirements for Windows, macOS, and Linux.

Become familiar with the major components of the Unreal Editor interface, the various tools and editors you can use, and the most common Unreal Engine terms.

Learn how to work with Assets in the Content Browser, which is the primary area of the Unreal Editor for creating, importing, organizing, viewing, and managing content.

Customize Unreal Engine's layout, keybindings, and behavior, and learn how to add useful features by enabling plugins.

Learn how to work with Unreal projects, which hold the contents of anything you build in Unreal Engine. You can also read about two of the basic project templates that Unreal Engine offers, which serve as starting points for a first-person or third-person experience.

Levels (sometimes called Maps) contain everything a player can see and interact with, like environments, usable objects, other characters, and so on. Every Unreal Engine project contains at least one Level. Read more about how to create and manage Levels on the pages below.

Any piece of content in an Unreal Engine project is called an Asset. Read more about how to work with Assets on the pages below.

At a more granular level, Unreal projects contain Actors (individual pieces of content) which can have one or more Components attached to them. The pages below can teach you more about Actors and Components.

Learn how to test your content directly inside Unreal Editor.

Package your application for different platforms.



---

## Understanding the Basics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-the-basics-of-unreal-engine?application_version=5.3

**Contents:**
- Understanding the Basics
- Installing Unreal Engine
- Foundational Knowledge
- Content Browser
- Customizing Unreal Engine
- Working with Projects and Templates
- Levels
- Assets and Content Packs
- Actors and Components
- Playing and Simulating

Essential skills and concepts to help you get started in Unreal Engine.

This section covers the fundamentals of Unreal Engine 5 (UE5) and its tools. If you are new to UE5, you should become familiar with the Unreal Editor interface, Blueprint visual scripting, and the types of content you can use inside an Unreal project.

Refer to the sections below to see what kind of UE5 skills you can learn.

Learn how to download and install Unreal Engine, and get acquainted with the Unreal Engine 5 system requirements for Windows, macOS, and Linux.

Become familiar with the major components of the Unreal Editor interface, the various tools and editors you can use, and the most common Unreal Engine terms.

Learn how to work with Assets in the Content Browser, which is the primary area of the Unreal Editor for creating, importing, organizing, viewing, and managing content.

Customize Unreal Engine's layout, keybindings, and behavior, and learn how to add useful features by enabling plugins.

Learn how to work with Unreal projects, which hold the contents of anything you build in Unreal Engine. You can also read about two of the basic project templates that Unreal Engine offers, which serve as starting points for a first-person or third-person experience.

Levels (sometimes called Maps) contain everything a player can see and interact with, like environments, usable objects, other characters, and so on. Every Unreal Engine project contains at least one Level. Read more about how to create and manage Levels on the pages below.

Any piece of content in an Unreal Engine project is called an Asset. Read more about how to work with Assets on the pages below.

At a more granular level, Unreal projects contain Actors (individual pieces of content) which can have one or more Components attached to them. The pages below can teach you more about Actors and Components.

Learn how to test your content directly inside Unreal Editor.

Package your application for different platforms.



---

## Understanding the Basics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-the-basics-of-unreal-engine

**Contents:**
- Understanding the Basics
- Installing Unreal Engine
- Foundational Knowledge
- Content Browser
- Customizing Unreal Engine
- Working with Projects and Templates
- Levels
- Assets and Content Packs
- Actors and Components
- Playing and Simulating

Essential skills and concepts to help you get started in Unreal Engine.

This section covers the fundamentals of Unreal Engine 5 (UE5) and its tools. If you are new to UE5, you should become familiar with the Unreal Editor interface, Blueprint visual scripting, and the types of content you can use inside an Unreal project.

Refer to the sections below to see what kind of UE5 skills you can learn.

Learn how to download and install Unreal Engine, and get acquainted with the Unreal Engine 5 system requirements for Windows, macOS, and Linux.

Install Unreal Engine

Download and update Unreal Engine from the Epic Games Launcher.

Become familiar with the major components of the Unreal Editor interface, the various tools and editors you can use, and the most common Unreal Engine terms.

Unreal Engine Terminology

Covers the most commonly used terms when working with Unreal Engine.

An overview of the different types of Editors contained within Unreal Engine 5.

Settings for configuring general editor behavior for controls, viewports, source control, and much more.

Overview of the directories that make up the engine and game projects.

Installing, enabling, and disabling plugins in Unreal Engine

Customizing Keyboard Shortcuts

Change keyboard shortcuts for common commands in Unreal Engine and create new shortcuts to suit your workflows.

Tool for interactively choosing colors to assign to color properties of actors.

Coordinate System and Spaces

Introduction to the coordinate system and different coordinate spaces.

Measure quantities of interest.

Learn how to work with Assets in the Content Browser, which is the primary area of the Unreal Editor for creating, importing, organizing, viewing, and managing content.

A tool you can use to view, manage, and work with all of the Assets in your project.

Content Browser Interface

Describes the Content Browser interface and functionality.

Iterate and collaborate with other developers using the Developers folder.

Sources Panel Reference

Reference for working with the Sources panel inside the Content Browser

Content Browser Settings Reference

Adjust thumbnail display, Asset filtering, and other areas of the Content Browser.

Filters and Collections

Use filters and Collections to sort and group Assets within the Content Browser.

Advanced Search Syntax

Reference for advanced search operators you can use in the Content Browser.

Customize Unreal Engine's layout, keybindings, and behavior, and learn how to add useful features by enabling plugins.

Customizing Unreal Engine

Customize Unreal Engine's layout, keybindings, and functionality to better suit your workflows.

Learn how to work with Unreal projects, which hold the contents of anything you build in Unreal Engine. You can also read about two of the basic project templates that Unreal Engine offers, which serve as starting points for a first-person or third-person experience.

Projects and Templates

Describes creating and managing Unreal Engine projects, using templates as a starting point, and creating custom templates.

Creating a New Project

Describes how to create and configure a new project in Unreal Engine.

Opening an Existing Project

Describes how to access and open an existing project in Unreal Engine.

Templates available with Unreal Engine and how to use them.

Updating Projects to Newer Versions of Unreal Engine

Learn how to update projects to a newer version of Unreal Engine.

Plugin to help recover an Unreal Engine session after a crash or abnormal exit.

Creating Custom Templates

Steps for converting an existing project to a template

Levels (sometimes called Maps) contain everything a player can see and interact with, like environments, usable objects, other characters, and so on. Every Unreal Engine project contains at least one Level. Read more about how to create and manage Levels on the pages below.

How to create, save, and open level assets.

Managing Multiple Levels

Use the Levels window to manage your persistent level and sublevels.

The World Settings panel is where you set and override Level-specific settings.

Changing the Default Level

How to set the default editor and game Levels for your project

Any piece of content in an Unreal Engine project is called an Asset. Read more about how to work with Assets on the pages below.

Importing Assets Directly

Describes two methods of importing small sets of Assets into your Unreal Engine project.

How to create, delete, and manage Assets from the Content Browser.

How to copy Assets from one project to another.

Describes how to create, read, and modify metadata on your Unreal Engine Assets.

Access Fab directly from within Unreal Engine

Reimporting Assets Automatically

This document outlines how to the auto-reimport functionality of UE4 works, and how to set it up to get the most out of the feature.

Use the Reference Viewer tool to find and organize Asset references.

Remove duplicate Assets by consolidating multiple Assets into a single one and fixing up references.

Tool for examining Unreal Engine classes and creating child classes.

Use the Global Asset Picker to quickly find Assets from any folder in the Asset Tree.

Tool for viewing and editing multiple properties of multiple actors at the same time.

At a more granular level, Unreal projects contain Actors (individual pieces of content) which can have one or more Components attached to them. The pages below can teach you more about Actors and Components.

Defines Actors and describes how to use them in level design. Also includes a rundown of the most common types of Actors.

Shows how you can place Actors such as props, lights, and cameras into your Level.

Overview of methods available for selecting Actors in the Level Editor viewport.

How to modify the location, rotation, and scale of Actors in a Level.

Overview of Actor snapping in Unreal Engine.

Setting that controls whether an Actor can move or change in some way during gameplay.

How to create and work with groups of Actors in Unreal Engine.

How to merge two or more Static Mesh Actors into a single Actor in Unreal Engine.

Describes the most common types of Actors in Unreal Engine and where you can learn more about them.

Describes the most common types of Components in Unreal Engine and where you can learn more about them.

Learn how to test your content directly inside Unreal Editor.

Playing and Simulating

Play-testing and simulating your game inside the Unreal Editor.

Package your application for different platforms.

Packaging Unreal Engine Projects

Packaging Unreal game projects for distribution.



---

## Understanding the Basics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-the-basics-of-unreal-engine?application_version=5.7

**Contents:**
- Understanding the Basics
- Installing Unreal Engine
- Foundational Knowledge
- Content Browser
- Customizing Unreal Engine
- Working with Projects and Templates
- Levels
- Assets and Content Packs
- Actors and Components
- Playing and Simulating

Essential skills and concepts to help you get started in Unreal Engine.

This section covers the fundamentals of Unreal Engine 5 (UE5) and its tools. If you are new to UE5, you should become familiar with the Unreal Editor interface, Blueprint visual scripting, and the types of content you can use inside an Unreal project.

Refer to the sections below to see what kind of UE5 skills you can learn.

Learn how to download and install Unreal Engine, and get acquainted with the Unreal Engine 5 system requirements for Windows, macOS, and Linux.

Install Unreal Engine

Download and update Unreal Engine from the Epic Games Launcher.

Become familiar with the major components of the Unreal Editor interface, the various tools and editors you can use, and the most common Unreal Engine terms.

Unreal Engine Terminology

Covers the most commonly used terms when working with Unreal Engine.

An overview of the different types of Editors contained within Unreal Engine 5.

Settings for configuring general editor behavior for controls, viewports, source control, and much more.

Overview of the directories that make up the engine and game projects.

Installing, enabling, and disabling plugins in Unreal Engine

Customizing Keyboard Shortcuts

Change keyboard shortcuts for common commands in Unreal Engine and create new shortcuts to suit your workflows.

Tool for interactively choosing colors to assign to color properties of actors.

Coordinate System and Spaces

Introduction to the coordinate system and different coordinate spaces.

Measure quantities of interest.

Learn how to work with Assets in the Content Browser, which is the primary area of the Unreal Editor for creating, importing, organizing, viewing, and managing content.

A tool you can use to view, manage, and work with all of the Assets in your project.

Content Browser Interface

Describes the Content Browser interface and functionality.

Iterate and collaborate with other developers using the Developers folder.

Sources Panel Reference

Reference for working with the Sources panel inside the Content Browser

Content Browser Settings Reference

Adjust thumbnail display, Asset filtering, and other areas of the Content Browser.

Filters and Collections

Use filters and Collections to sort and group Assets within the Content Browser.

Advanced Search Syntax

Reference for advanced search operators you can use in the Content Browser.

Customize Unreal Engine's layout, keybindings, and behavior, and learn how to add useful features by enabling plugins.

Customizing Unreal Engine

Customize Unreal Engine's layout, keybindings, and functionality to better suit your workflows.

Learn how to work with Unreal projects, which hold the contents of anything you build in Unreal Engine. You can also read about two of the basic project templates that Unreal Engine offers, which serve as starting points for a first-person or third-person experience.

Projects and Templates

Describes creating and managing Unreal Engine projects, using templates as a starting point, and creating custom templates.

Creating a New Project

Describes how to create and configure a new project in Unreal Engine.

Opening an Existing Project

Describes how to access and open an existing project in Unreal Engine.

Templates available with Unreal Engine and how to use them.

Updating Projects to Newer Versions of Unreal Engine

Learn how to update projects to a newer version of Unreal Engine.

Plugin to help recover an Unreal Engine session after a crash or abnormal exit.

Creating Custom Templates

Steps for converting an existing project to a template

Levels (sometimes called Maps) contain everything a player can see and interact with, like environments, usable objects, other characters, and so on. Every Unreal Engine project contains at least one Level. Read more about how to create and manage Levels on the pages below.

How to create, save, and open level assets.

Managing Multiple Levels

Use the Levels window to manage your persistent level and sublevels.

The World Settings panel is where you set and override Level-specific settings.

Changing the Default Level

How to set the default editor and game Levels for your project

Any piece of content in an Unreal Engine project is called an Asset. Read more about how to work with Assets on the pages below.

Importing Assets Directly

Describes two methods of importing small sets of Assets into your Unreal Engine project.

How to create, delete, and manage Assets from the Content Browser.

How to copy Assets from one project to another.

Describes how to create, read, and modify metadata on your Unreal Engine Assets.

Access Fab directly from within Unreal Engine

Reimporting Assets Automatically

This document outlines how to the auto-reimport functionality of UE4 works, and how to set it up to get the most out of the feature.

Use the Reference Viewer tool to find and organize Asset references.

Remove duplicate Assets by consolidating multiple Assets into a single one and fixing up references.

Tool for examining Unreal Engine classes and creating child classes.

Use the Global Asset Picker to quickly find Assets from any folder in the Asset Tree.

Tool for viewing and editing multiple properties of multiple actors at the same time.

At a more granular level, Unreal projects contain Actors (individual pieces of content) which can have one or more Components attached to them. The pages below can teach you more about Actors and Components.

Defines Actors and describes how to use them in level design. Also includes a rundown of the most common types of Actors.

Shows how you can place Actors such as props, lights, and cameras into your Level.

Overview of methods available for selecting Actors in the Level Editor viewport.

How to modify the location, rotation, and scale of Actors in a Level.

Overview of Actor snapping in Unreal Engine.

Setting that controls whether an Actor can move or change in some way during gameplay.

How to create and work with groups of Actors in Unreal Engine.

How to merge two or more Static Mesh Actors into a single Actor in Unreal Engine.

Describes the most common types of Actors in Unreal Engine and where you can learn more about them.

Describes the most common types of Components in Unreal Engine and where you can learn more about them.

Learn how to test your content directly inside Unreal Editor.

Playing and Simulating

Play-testing and simulating your game inside the Unreal Editor.

Package your application for different platforms.

Packaging Unreal Engine Projects

Packaging Unreal game projects for distribution.



---

## Understanding the Basics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-the-basics-of-unreal-engine?application_version=5.1

**Contents:**
- Understanding the Basics
- Installing Unreal Engine
- Foundational Knowledge
- Content Browser
- Customizing Unreal Engine
- Working with Projects and Templates
- Levels
- Assets and Content Packs
- Actors and Components
- Playing and Simulating

Essential skills and concepts to help you get started in Unreal Engine.

This section covers the fundamentals of Unreal Engine 5 (UE5) and its tools. If you are new to UE5, you should become familiar with the Unreal Editor interface, Blueprint visual scripting, and the types of content you can use inside an Unreal project.

Refer to the sections below to see what kind of UE5 skills you can learn.

Learn how to download and install Unreal Engine, and get acquainted with the Unreal Engine 5 system requirements for Windows, macOS, and Linux.

Become familiar with the major components of the Unreal Editor interface, the various tools and editors you can use, and the most common Unreal Engine terms.

Learn how to work with Assets in the Content Browser, which is the primary area of the Unreal Editor for creating, importing, organizing, viewing, and managing content.

Customize Unreal Engine's layout, keybindings, and behavior, and learn how to add useful features by enabling plugins.

Learn how to work with Unreal projects, which hold the contents of anything you build in Unreal Engine. You can also read about two of the basic project templates that Unreal Engine offers, which serve as starting points for a first-person or third-person experience.

Levels (sometimes called Maps) contain everything a player can see and interact with, like environments, usable objects, other characters, and so on. Every Unreal Engine project contains at least one Level. Read more about how to create and manage Levels on the pages below.

Any piece of content in an Unreal Engine project is called an Asset. Read more about how to work with Assets on the pages below.

At a more granular level, Unreal projects contain Actors (individual pieces of content) which can have one or more Components attached to them. The pages below can teach you more about Actors and Components.

Learn how to test your content directly inside Unreal Editor.

Package your application for different platforms.



---

## Understanding the Basics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-the-basics-of-unreal-engine?application_version=5.6

**Contents:**
- Understanding the Basics
- Installing Unreal Engine
- Foundational Knowledge
- Content Browser
- Customizing Unreal Engine
- Working with Projects and Templates
- Levels
- Assets and Content Packs
- Actors and Components
- Playing and Simulating

Essential skills and concepts to help you get started in Unreal Engine.

This section covers the fundamentals of Unreal Engine 5 (UE5) and its tools. If you are new to UE5, you should become familiar with the Unreal Editor interface, Blueprint visual scripting, and the types of content you can use inside an Unreal project.

Refer to the sections below to see what kind of UE5 skills you can learn.

Learn how to download and install Unreal Engine, and get acquainted with the Unreal Engine 5 system requirements for Windows, macOS, and Linux.

Install Unreal Engine

Download and update Unreal Engine from the Epic Games Launcher.

Become familiar with the major components of the Unreal Editor interface, the various tools and editors you can use, and the most common Unreal Engine terms.

Unreal Engine Terminology

Covers the most commonly used terms when working with Unreal Engine.

An overview of the different types of Editors contained within Unreal Engine 5.

Settings for configuring general editor behavior for controls, viewports, source control, and much more.

Overview of the directories that make up the engine and game projects.

Installing, enabling, and disabling plugins in Unreal Engine

Customizing Keyboard Shortcuts

Change keyboard shortcuts for common commands in Unreal Engine and create new shortcuts to suit your workflows.

Tool for interactively choosing colors to assign to color properties of actors.

Coordinate System and Spaces

Introduction to the coordinate system and different coordinate spaces.

Measure quantities of interest.

Learn how to work with Assets in the Content Browser, which is the primary area of the Unreal Editor for creating, importing, organizing, viewing, and managing content.

A tool you can use to view, manage, and work with all of the Assets in your project.

Content Browser Interface

Describes the Content Browser interface and functionality.

Iterate and collaborate with other developers using the Developers folder.

Sources Panel Reference

Reference for working with the Sources panel inside the Content Browser

Content Browser Settings Reference

Adjust thumbnail display, Asset filtering, and other areas of the Content Browser.

Filters and Collections

Use filters and Collections to sort and group Assets within the Content Browser.

Advanced Search Syntax

Reference for advanced search operators you can use in the Content Browser.

Customize Unreal Engine's layout, keybindings, and behavior, and learn how to add useful features by enabling plugins.

Customizing Unreal Engine

Customize Unreal Engine's layout, keybindings, and functionality to better suit your workflows.

Learn how to work with Unreal projects, which hold the contents of anything you build in Unreal Engine. You can also read about two of the basic project templates that Unreal Engine offers, which serve as starting points for a first-person or third-person experience.

Projects and Templates

Describes creating and managing Unreal Engine projects, using templates as a starting point, and creating custom templates.

Creating a New Project

Describes how to create and configure a new project in Unreal Engine.

Opening an Existing Project

Describes how to access and open an existing project in Unreal Engine.

Templates available with Unreal Engine and how to use them.

Updating Projects to Newer Versions of Unreal Engine

Learn how to update projects to a newer version of Unreal Engine.

Plugin to help recover an Unreal Engine session after a crash or abnormal exit.

Creating Custom Templates

Steps for converting an existing project to a template

Levels (sometimes called Maps) contain everything a player can see and interact with, like environments, usable objects, other characters, and so on. Every Unreal Engine project contains at least one Level. Read more about how to create and manage Levels on the pages below.

How to create, save, and open level assets.

Managing Multiple Levels

Use the Levels window to manage your persistent level and sublevels.

The World Settings panel is where you set and override Level-specific settings.

Changing the Default Level

How to set the default editor and game Levels for your project

Any piece of content in an Unreal Engine project is called an Asset. Read more about how to work with Assets on the pages below.

Importing Assets Directly

Describes two methods of importing small sets of Assets into your Unreal Engine project.

How to create, delete, and manage Assets from the Content Browser.

How to copy Assets from one project to another.

Access Fab directly from within Unreal Engine

Describes how to create, read, and modify metadata on your Unreal Engine Assets.

Reimporting Assets Automatically

This document outlines how to the auto-reimport functionality of UE4 works, and how to set it up to get the most out of the feature.

Use the Reference Viewer tool to find and organize Asset references.

Remove duplicate Assets by consolidating multiple Assets into a single one and fixing up references.

Tool for examining Unreal Engine classes and creating child classes.

Use the Global Asset Picker to quickly find Assets from any folder in the Asset Tree.

Tool for viewing and editing multiple properties of multiple actors at the same time.

At a more granular level, Unreal projects contain Actors (individual pieces of content) which can have one or more Components attached to them. The pages below can teach you more about Actors and Components.

Defines Actors and describes how to use them in level design. Also includes a rundown of the most common types of Actors.

Shows how you can place Actors such as props, lights, and cameras into your Level.

Overview of methods available for selecting Actors in the Level Editor viewport.

How to modify the location, rotation, and scale of Actors in a Level.

Overview of Actor snapping in Unreal Engine.

Setting that controls whether an Actor can move or change in some way during gameplay.

How to create and work with groups of Actors in Unreal Engine.

How to merge two or more Static Mesh Actors into a single Actor in Unreal Engine.

Describes the most common types of Actors in Unreal Engine and where you can learn more about them.

Describes the most common types of Components in Unreal Engine and where you can learn more about them.

Learn how to test your content directly inside Unreal Editor.

Playing and Simulating

Play-testing and simulating your game inside the Unreal Editor.

Package your application for different platforms.

Packaging Unreal Engine Projects

Packaging Unreal game projects for distribution.



---

## Understanding the Basics

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-the-basics-of-unreal-engine?application_version=5.5

**Contents:**
- Understanding the Basics
- Installing Unreal Engine
- Foundational Knowledge
- Content Browser
- Customizing Unreal Engine
- Working with Projects and Templates
- Levels
- Assets and Content Packs
- Actors and Components
- Playing and Simulating

Essential skills and concepts to help you get started in Unreal Engine.

This section covers the fundamentals of Unreal Engine 5 (UE5) and its tools. If you are new to UE5, you should become familiar with the Unreal Editor interface, Blueprint visual scripting, and the types of content you can use inside an Unreal project.

Refer to the sections below to see what kind of UE5 skills you can learn.

Learn how to download and install Unreal Engine, and get acquainted with the Unreal Engine 5 system requirements for Windows, macOS, and Linux.

Installing Unreal Engine

Steps for installing Unreal Engine

Become familiar with the major components of the Unreal Editor interface, the various tools and editors you can use, and the most common Unreal Engine terms.

Unreal Editor Interface

Overview of the key elements of the Unreal Editor interface

Unreal Engine Terminology

Covers the most commonly used terms when working with Unreal Engine.

An overview of the different types of Editors contained within Unreal Engine 5.

Coordinate System and Spaces

Introduction to the coordinate system and different coordinate spaces.

Onboarding Guide for Games Licensees

Steps to getting started with Unreal Engine.

Onboarding Guide for Non-Games Licensees

Steps to getting started with Unreal Engine.

Overview of the directories that make up the engine and game projects.

Mathematical Foundations

Learn about the mathematical foundations of Unreal Engine structures and operations.

Get started with Unreal Engine as a licensee.

Getting Started with Dev Portal

A guide to using the Epic Games Developer Portal for the first time.

Learn how to work with Assets in the Content Browser, which is the primary area of the Unreal Editor for creating, importing, organizing, viewing, and managing content.

A tool you can use to view, manage, and work with all of the Assets in your project.

Content Browser Interface

Describes the Content Browser interface and functionality.

Iterate and collaborate with other developers using the Developers folder.

Sources Panel Reference

Reference for working with the Sources panel inside the Content Browser

Content Browser Settings Reference

Adjust thumbnail display, Asset filtering, and other areas of the Content Browser.

Filters and Collections

Use filters and Collections to sort and group Assets within the Content Browser.

Advanced Search Syntax

Reference for advanced search operators you can use in the Content Browser.

Customize Unreal Engine's layout, keybindings, and behavior, and learn how to add useful features by enabling plugins.

Customizing Unreal Engine

Customize Unreal Engine's layout, keybindings, and functionality to better suit your workflows.

Learn how to work with Unreal projects, which hold the contents of anything you build in Unreal Engine. You can also read about two of the basic project templates that Unreal Engine offers, which serve as starting points for a first-person or third-person experience.

Creating a New Project

Describes how to create and configure a new project in Unreal Engine.

Opening an Existing Project

Describes how to access and open an existing project in Unreal Engine.

Templates available with Unreal Engine and how to use them.

Updating Projects to Newer Versions of Unreal Engine

Learn how to update projects to a newer version of Unreal Engine.

Plugin to help recover an Unreal Engine session after a crash or abnormal exit.

Creating Custom Templates

Steps for converting an existing project to a template

Levels (sometimes called Maps) contain everything a player can see and interact with, like environments, usable objects, other characters, and so on. Every Unreal Engine project contains at least one Level. Read more about how to create and manage Levels on the pages below.

How to create, save, and open level assets.

Managing Multiple Levels

Use the Levels window to manage your persistent level and sublevels.

The World Settings panel is where you set and override Level-specific settings.

Changing the Default Level

How to set the default editor and game Levels for your project

Any piece of content in an Unreal Engine project is called an Asset. Read more about how to work with Assets on the pages below.

Importing Assets Directly

Describes two methods of importing small sets of Assets into your Unreal Engine project.

How to create, delete, and manage Assets from the Content Browser.

How to copy Assets from one project to another.

Describes how to create, read, and modify metadata on your Unreal Engine Assets.

Reimporting Assets Automatically

This document outlines how to the auto-reimport functionality of UE4 works, and how to set it up to get the most out of the feature.

Use the Reference Viewer tool to find and organize Asset references.

Remove duplicate Assets by consolidating multiple Assets into a single one and fixing up references.

Tool for examining Unreal Engine classes and creating child classes.

Use the Global Asset Picker to quickly find Assets from any folder in the Asset Tree.

Tool for viewing and editing multiple properties of multiple actors at the same time.

At a more granular level, Unreal projects contain Actors (individual pieces of content) which can have one or more Components attached to them. The pages below can teach you more about Actors and Components.

Defines Actors and describes how to use them in level design. Also includes a rundown of the most common types of Actors.

Shows how you can place Actors such as props, lights, and cameras into your Level.

Overview of methods available for selecting Actors in the Level Editor viewport.

How to modify the location, rotation, and scale of Actors in a Level.

Overview of Actor snapping in Unreal Engine.

Setting that controls whether an Actor can move or change in some way during gameplay.

How to create and work with groups of Actors in Unreal Engine.

How to merge two or more Static Mesh Actors into a single Actor in Unreal Engine.

Describes the most common types of Actors in Unreal Engine and where you can learn more about them.

Describes the most common types of Components in Unreal Engine and where you can learn more about them.

Learn how to test your content directly inside Unreal Editor.

Playing and Simulating

Play-testing and simulating your game inside the Unreal Editor.

Package your application for different platforms.

Packaging Unreal Engine Projects

Packaging Unreal game projects for distribution.



---

## Unreal Engine Terminology

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-terminology

**Contents:**
- Unreal Engine Terminology
- Project
- Blueprint
- Object
- Class
- Actor
- Casting
- Component
- Pawn
- Character

Covers the most commonly used terms when working with Unreal Engine.

This page describes the most commonly used terms when working with Unreal Engine. If you find yourself wondering, "What is an Actor?" or "What is a Component?" this page will answer your questions, and more.

Once you understand a term, check the topics linked at the end of the section to learn more.

This page uses some programming concepts, notably classes and subclasses. In C++, a class is a code template that contains variables and behavior and can be extended. A subclass is a class that inherits some or all code and functionality from a parent class.

All of the C++ classes mentioned on this page are specific to Unreal Engine.

An Unreal Engine 5 Project holds all the contents of your game. It contains a number of folders on your disk, such as Blueprints and Materials. You can name and organize folders inside a Project however you wish. The Content Browser panel inside the Unreal Editor shows the same directory structure found inside the Project folder on your disk.

Every project has a .uproject file associated with it. The .uproject file is how you create, open, or save a project. You can create any number of different projects and work on them in parallel.

For more information, see Projects and Templates.

The Blueprint Visual Scripting system is a complete gameplay scripting system that uses a node-based interface to create gameplay elements from within Unreal Editor. As with many common scripting languages, it is used to define object-oriented (OO) classes or objects in the engine. As you use Unreal Engine, you'll often find that objects defined using Blueprint are colloquially referred to as "Blueprints."

For more information, see Blueprints Visual Scripting.

Objects are the most basic class in Unreal Engine - in other words, they act like building blocks and contain a lot of the essential functionality for your Assets. Almost everything in Unreal Engine inherits (or gets some functionality) from an Object.

In C++, UObject is the base class of all objects; it implements features such as garbage collections, metadata (UProperty) support for exposing variables to the Unreal Editor, and serialization for loading and saving.

For more information, see:

A Class defines the behaviors and properties of a particular Actor or Object in Unreal Engine. Classes are hierarchical, meaning a Class inherits information from its parent Class (that is, the Class it was derived or "sub-classed" from) and passes that information to its children. Classes can be created in C++ code or in Blueprints.

For more information, see:

An Actor is any object that can be placed into a level, such as a Camera, static mesh, or player start location. Actors support 3D transformations such as translation, rotation, and scaling. They can be created (spawned) and destroyed through gameplay code (C++ or Blueprints).

In C++, AActor is the base class of all Actors.

For more information, see:

Casting is an action that takes an Actor of a specific class and tries to treat it as if it were of a different class. Casting can succeed or fail. If casting succeeds, you can then access class-specific functionality on the Actor you cast to.

For example, let's say you're making a game where you have multiple types of Volumes that can affect the player character in different ways. One of these volumes is Fire, which decreases player health over time. When the player overlaps with any Volume in the Level, you can cast that Volume to Fire to try to access its ""damage player health"" functionality.

Casting is different from simply checking whether an Actor is of a given class, which would return a binary (yes or no) answer, but wouldn't allow you to interact with any specific functionality of that class.

A Component is a piece of functionality that can be added to an Actor.

When you add a Component to an Actor, the Actor can use the functionality that the Component provides. For example:

Components must be attached to an Actor and can't exist by themselves.

For more information, see:

Pawns are a subclass of Actor and serve as an in-game avatar or persona (for example, the characters in a game). Pawns can be controlled by a player or by the game's AI, as non-player characters (NPCs).

When a Pawn is controlled by a human or AI player, it is considered to be Possessed. Conversely, when a Pawn is not controlled by a human or AI player, it is considered to be Unpossessed.

For more information, see:

A Character is a subclass of a Pawn Actor that is intended to be used as a player character. The Character subclass includes a collision setup, input bindings for bipedal movement, and additional code for player-controlled movement.

For more information, see:

A Player Controller takes player input and translates it into interactions in the game. Every game has at least one Player Controller in it. A Player Controller often possesses a Pawn or Character as a representation of the player in a game.

The Player Controller is also the primary network interaction point for multiplayer games. During multiplayer play, the server has one instance of a Player Controller for every player in the game since it must be able to make network function calls to each player. Each client only has the Player Controller that corresponds to their player and can only use their Player Controller to communicate with the server.

The associated C++ class is PlayerController.

For more information, see Player Controllers.

Just as the Player Controller possesses a Pawn as a representation of the player in a game, an AI Controller possesses a Pawn to represent a non-player character (NPC) in a game. By default, Pawns and Characters will end up with a base AI Controller unless they are specifically possessed by a Player Controller or told not to create an AI Controller for themselves.

The associated C++ class is AIController.

For more information, see AI Controllers.

A Player State is the state of a participant in the game, such as a human player or a bot that is simulating a player. Non-player AI that exists as part of the game world doesn't have a Player State.

Some examples of player information that the Player State can contain include:

For multiplayer games, Player States for all players exist on all machines and can replicate data from the server to the client to keep things in sync. This is different from a Player Controller, which will only exist on the machine of the player it represents.

The associated C++ class is PlayerState.

For more information, see Gameplay Framework Quick Reference.

The Game Mode sets the rules of the game that is being played. These rules can include:

You can set the default Game Mode in the Project Settings and override it for different Levels. Regardless of how you choose to implement it, you can only have one Game Mode for each Level.

In a multiplayer game, the Game Mode only exists on the server and the rules are replicated (sent) to each of the connected clients.

The associated C++ class is GameMode.

For more information, see:

A Game State is a container that holds information you want replicated to every client in a game. In simpler terms, it is 'The State of the Game' for everyone connected.

Some examples of what the Game State can contain include:

For multiplayer games, there is one local instance of the Game State on each player's machine. Local Game State instances get their updated information from the server's instance of the Game State.

The associated C++ class is GameState.

For more information, see Game Mode and Game State.

A Brush is an Actor that describes a 3D shape, such as a cube or a sphere. You can place brushes in a level to define level geometry (these are known as Binary Space Partition or BSP brushes). This is useful if you want to quickly block out a level, for example.

For more information, see:

Volumes are bounded 3D spaces that have different uses based on the effects attached to them. For example:

For more information, see Actors Reference.

A Level is a gameplay area that you define. Levels contain everything a player can see and interact with, such as geometry, Pawns, and Actors.

Unreal Engine saves each level as a separate .umap file, which is why you will sometimes see them referred to as Maps.

For more information, see:

A World is a container for all the Levels that make up your game. It handles the streaming of Levels and the spawning (creation) of dynamic Actors.

For more information, see:



---
