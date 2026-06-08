# Unreal-Engine - Gameplay Systems

**Pages:** 19

---

## Enhanced Input

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/EnhancedInput

**Contents:**
- Enhanced Input
- Navigation
- Modules
- Plugin Dependencies
- Plugin Dependents

API > API/PluginIndex

Input handling that allows for contextual and dynamic mappings.



---

## Enhanced Input Code Quality Unreal Test Plugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/CQTestEnhancedInput

**Contents:**
- Enhanced Input Code Quality Unreal Test Plugin
- Navigation
- Modules
- Plugin Dependencies

API > API/PluginIndex

Simplified testing of the Enhanced Input for Unreal Engine



---

## EOS Overlay Input Provider

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/EOSOverlayInputProvider

**Contents:**
- EOS Overlay Input Provider
- Navigation
- Modules
- Plugin Dependencies
- Plugin Dependents

API > API/PluginIndex

Responsible for providing input forwarding to the EOSSDK Overlay.



---

## Gameplay Ability System

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-ability-system-for-unreal-engine

**Contents:**
- Gameplay Ability System
- Valley of the Ancient Sample
  - Walking Animation Example
  - Charge Attack Example
- Topic Directory

High-level view of the Gameplay Ability System

The Gameplay Ability System is a framework for building attributes, abilities, and interactions that an Actor can own and trigger. The system is designed to be adapted to a wide variety of Gameplay-Driven projects such as Role-Playing Games(RPGs), Action-Adventure games, and Multiplayer Online Battle Arenas games(MOBA).

With the Gameplay Ability System, you can:

Use the Ability System Component. The Ability System Component includes all the base functionality that an Actor Component implements.

The Ability System Component implements its own Interface to access and interact with the framework of the Gameplay Ability System.

Create active or passive Gameplay Abilities, for Actors that coordinate with your project's gameplay mechanics, visual effects,animations, sounds, and other data-driven elements.

Use Attributes and Attribute Sets that store, calculate, and modify your gameplay-related values as they interact with the Gameplay Ability System.

Change Attributes with Gameplay Effects that provide a method to directly modify attribute values with your project's design. Gameplay Effects contain Gameplay Effect Components that determine how a Gameplay Effect behaves.

Ability Tasks(UAbilityTask) are a specialized form of a Gameplay Task class that work with Gameplay Abilities. Games that use the Gameplay Ability System usually include a variety of custom Ability Tasks which implement their unique gameplay features. They perform asynchronous work during a Gameplay Ability's execution, and have the capability to affect execution flow by calling Delegates in native C++ code or moving through one or more output execution pins like Blueprints.

Using this system, you can create abilities like a single attack, or add more complexity like a spell that triggers many status effects depending on data from the user and the targets.

Echo's charge and attack animation and their walking animation are examples of a Gameplay Ability.

See the Valley of the Ancient Sample for additional features.



---

## Gameplay Framework

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-framework-in-unreal-engine

**Contents:**
- Gameplay Framework
- Overview
- Gameplay Framework Classes
- Directory

Core game systems such as game mode, player state, controllers, pawns, cameras, and so on.

Unreal Engine's Gameplay Framework is a collection of classes that provides you with a modular foundation upon which to build your gameplay experience. You can pick and choose which elements are right for your game knowing that these classes are designed to work with and complement one another.

Visual representation of the gameplay framework classes and how they are associated with one another in Unreal Engine. Click image to expand.

The game instance is instantiated on engine launch and remains active until the engine shuts down. It is a manager class that has no physical presence in the game, but rather exists to track data and run code. The game instance is not replicated and exists independently on the server and all connected clients in network multiplayer. Anything that you want to persist between level loads should live in the game instance. For example, this makes the game instance a good place to manage your save game system. The game instance also acts as a manager for any number of game instance subsystems that are created and destroyed by the game instance and exist for the same lifetime as the game instance itself. An example of one of these subsystems is the Online Subsystems which you can use to manage online services functionality such as friends, game sessions, lobbies, leaderboards, and much more in your game.

The game mode is instantiated immediately after your level is loaded in the engine and the world is created. The game mode is a server-based manager class inherited from the actor class. Since this class is created upon level load, it is not persistent across levels. Game mode is the first actor to instantiate upon level load and can be set on map-by-map basis. Game mode exists at the heart of the gameplay framework managing the overall rules and structure of a gameplay session and instantiating the remaining framework actors upon creation. The first two are game state and player state.

Game state and player state are non-physical actors that are designed to track the state of the game and the players within it, respectively. These classes replicate their state information between the authoritative server and all connected clients in network multiplayer. Game state contains data and logic relevant to all players in a game, such as team scores, objectives, and a list of all players and their associated player states. On the other hand, the player state handles data and logic relevant to its associated player, such as health, ammo count, and inventory. A single game state is created by the game mode. A player state is created for each player when they join a game or upon entrance into the level.

The game mode spawns players when they join the game. A player primarily consists of a controller and a pawn. The controller classes handle the logic that dictates a player's actions in the game world. There are two types of controller class in UE that are widely used: player controller and AI controller. The player controller class is a manager class that can process input from a human, display heads-up information, and possess physical representations in the game. The AI controller class is a manager class that possesses physical representations in the game and dictates their actions with the help of UE's artificial intelligence, including: behavior trees, state trees, navigation, and so on.

As a non-physical actor class, the controller class and its derived classes do not have a physical manifestation in the game world. The pawn class consists of the physical manifestation of the player in the game world. The pawn class is as important to creating a player as the controller class. Controllers possess pawns and direct the pawn to perform actions in the game. Pawns, as actor-derived classes, consist of several actor components such as collision component, static mesh component, and movement component. The character class is a pawn-derived subclass that builds upon the default pawn class with more feature rich components, including: character movement component, skeletal mesh component, and capsule component.

The Begin Play Epic Developer Community learning tutorial presents a video of a comprehensive overview of the gameplay framework in Unreal Engine.

The following table provides an overview of important classes contained within the gameplay framework, a brief description of the class, and a link to each class' dedicated documentation pages:

An Actor is any object that can be placed into a level, such as a Camera, static mesh, or player start location. Actors support transformations such as translation, rotation, and scaling. They can be spawned and destroyed through gameplay code.

Actors are also containers that hold special types of objects called actor components. Different types of components are used to control how actors move, how they are rendered, etc. The other main function of actors is the replication of properties and function calls across the network during play.

You can customize and use most of the classes in UE's gameplay framework in either C++, Blueprint, or, the most common, a combination of both.



---

## Game Input Base

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/GameInput

**Contents:**
- Game Input Base
- Navigation
- Modules
- Plugin Dependents

API > API/PluginIndex

GameInput is a next-generation input API that exposes input devices of all kinds through a single consistent interface.



---

## Game Input (Windows)

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/GameInputWindows

**Contents:**
- Game Input (Windows)
- Navigation
- Modules
- Plugin Dependencies

API > API/PluginIndex

GameInput is a next-generation input API that exposes input devices of all kinds through a single consistent interface.



---

## Game Mode and Game State

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/game-mode-and-game-state-in-unreal-engine

**Contents:**
- Game Mode and Game State
- Game Modes
  - AGameModeBase
  - AGameMode
  - Game Mode Blueprints
  - Setting the Game Mode
- Game State

Overview of the Game Mode and Game State

There are two main classes which handle information about the game being played: Game Mode and Game State.

Even the most open-ended game has an underpinning of rules, and these rules make up a Game Mode. On the most basic level, these rules include:

When rule-related events in the game happen and need to be tracked and shared with all players, that information is stored and synced through the Game State. This information includes:

While certain fundamentals, like the number of players required to play, or the method by which those players join the game, are common to many types of games, limitless rule variations are possible depending on the specific game you are developing. Regardless of what those rules are, Game Modes are designed to define and implement them. There are currently two commonly-used base classes for Game Modes.

Engine version 4.14 introduces AGameModeBase, which is the base class for all Game Modes and is a simplified and streamlined version of the classic AGameMode. AGameMode, the Game Mode base class before version 4.14, still exists and functions as it did before, but is now a child of AGameModeBase. AGameMode is more suited to standard game types like multiplayer shooters due to its implementation of the concept of match state. AGameModeBase is the new default game mode included in new code projects due to its simplicity and efficiency.

All Game Modes are subclasses of AGameModeBase, which contains considerable base functionality that can be overridden. Some of the common functions include:

The InitGame event is called before any other scripts (including PreInitializeComponents), and is used by AGameModeBase to initialize parameters and spawn its helper classes.

This is called before any Actor runsPreInitializeComponents, including the Game Mode instance itself.

A subclass of the AGameModeBase class may be created for each match format, mission type, or special zone that the game offers. A game may have any number of Game Modes, and thus subclasses of the AGameModeBase class; however, only one Game Mode may be in use at any given time. A Game Mode Actor is instantiated each time a level is initialized for play via the UGameEngine::LoadMap() function.

The Game Mode is not replicated to any remote clients that join in a multiplayer game; it exists only on the server, so local clients can see the stock Game Mode class (or Blueprint) that was used, but cannot access the actual instance and check its variables to see what has changed as the game progresses. If players do need updated information relating to the current Game Mode, that information is easily kept in sync by being stored on an AGameStateBase Actor, one of which will be created along with the Game Mode and then replicated out to all remote clients.

AGameMode is a subclass of AGameModeBase that has some extra functionality to support multiplayer matches and legacy behavior. All newly created projects use AGameModeBase by default, but you can switch to inheriting from AGameMode if you need this extra behavior. If you inherit from AGameMode, you should also inherit your game state from AGameState, which also supports the match state machine.

AGameMode contains a state machine that tracks the state of the match or the general gameplay flow. To query the current state, you can use GetMatchState, or wrappers like HasMatchStarted, IsMatchInProgress, and HasMatchEnded. Here are the possible match states:

The match state will almost always be InProgress since this is the state where BeginPlay is called and actors begin ticking. However, individual games can override the behavior of these states to build a multiplayer game with more complicated rules, such as permitting players to fly around the level freely while waiting for other players to join in a multiplayer shooter.

It is possible to create Blueprints derived from Game Mode classes, and use these as the default Game Mode for your project or level.

Blueprints derived from Game Modes can set the following defaults:

In addition, Blueprints of Game Modes are very useful because they enable adjustment of variables without altering code, and can therefore be used to adapt a single Game Mode to multiple different levels without using hard-coded asset references or requiring engineering support and code changes for every tweak.

There are several methods to set the Game Mode for a level, ordered here from lowest priority to highest priority:

Setting the GlobalDefaultGameMode entry in the /Script/EngineSettings.GameMapsSettings section of the DefaultEngine.ini file will set the default game mode for all maps in the project.

To override the project settings for an individual map, set the GameMode Override in the World Settings tab in the editor.

URLs can be passed to the executable to force the game to load with specific options. Use the game option to set the game mode. See Command-Line Arguments for more information.

Finally, map prefixes (and aliases for the URL method) can be set in the /Script/Engine.WorldSettings/ section of the DefaultEngine.ini file. These prefixes set the default game mode for all maps that have a given prefix.

For an example of setting up a Game Mode, refer to the Setting Up a Game Mode documentation.

The Game State is responsible for enabling the clients to monitor the state of the game. Conceptually, the Game State should manage information that is meant to be known to all connected clients and is specific to the Game Mode but is not specific to any individual player. It can keep track of game-wide properties such as the list of connected players, team score in Capture The Flag, missions that have been completed in an open world game, and so on.

Game State is not the best place to keep track of player-specific things like how many points one specific player has scored for the team in a Capture The Flag match because that can be handled more cleanly by Player State. In general, the GameState should track properties that change during gameplay and are relevant and visible to everyone. While the Game mode exists only on the server, the Game State exists on the server and is replicated to all clients, keeping all connected machines up to date as the game progresses.

AGameStateBase is the base implementation, and some of its default functionality includes:

AGameStateBase is very commonly extended in C++ or Blueprints to contain additional variables and functions that are needed to keep players informed of what's going on in the game. The specific modifications made are generally based on a paired Game Mode for which the Game State is made. The Game Mode itself can also override its default Game State type to be any C++ class or Blueprint derived from AGameStateBase.



**Examples:**

Example 1 (json):
```json
[/Script/EngineSettings.GameMapsSettings]
          GlobalDefaultGameMode="/Script/MyGame.MyGameGameMode"
          GlobalDefaultServerGameMode="/Script/MyGame.MyGameGameMode"
```

Example 2 (unknown):
```unknown
UE4Editor.exe /Game/Maps/MyMap?game=MyGameMode -game
```

Example 3 (json):
```json
[/Script/EngineSettings.GameMapsSettings]
          +GameModeMapPrefixes=(Name="DM",GameMode="/Script/UnrealTournament.UTDMGameMode")
          +GameModeClassAliases=(Name="DM",GameMode="/Script/UnrealTournament.UTDMGameMode")
```

---

## InputBindingEditor

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Editor/InputBindingEditor

**Contents:**
- InputBindingEditor
- Navigation
- Interfaces



---

## InputCore

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/InputCore

**Contents:**
- InputCore
- Navigation
- Classes
- Structs
- Interfaces
- Typedefs
- Enums
  - Public



---

## InputDevice

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/InputDevice

**Contents:**
- InputDevice
- Navigation
- Structs
- Interfaces



---

## Input

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/input-in-unreal-engine

**Contents:**
- Input
- Topics

Different methods to create and setup input in Unreal Engine

The PlayerInput Object is responsible for converting input from the player into data that Actors (like PlayerControllers or Pawns) can understand and use. It is part of an input processing flow that translates hardware input from players into game events and movement with Player Input mappings and Input Components.

You can get started with the Input Overview or choose any of the topics below.



---

## Input Debugging

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/InputDebugging

**Contents:**
- Input Debugging
- Navigation
- Modules

API > API/PluginIndex

Input debugging and visualization.



---

## LiveLinkInputDevice

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/LiveLinkInputDevice

**Contents:**
- LiveLinkInputDevice
- Navigation
- Modules
- Plugin Dependencies

API > API/PluginIndex

Live Link plugin for Unreal Engine Input Devices, i.e. Game Controllers. It uses the InputDevice system to query values and share state over LiveLink.



---

## Networking and Multiplayer

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/networking-and-multiplayer-in-unreal-engine

**Contents:**
- Networking and Multiplayer
- Basics
- Managing Sessions
- Network Multiplayer Programming
- Iris Replication System
- Replication Graph
- Replay System
- Deploying Multiplayer Games
- Debugging and Optimization
- Tutorials and Examples

Setting up networked games for multiplayer.

Modern multiplayer experiences require synchronizing vast amounts of data between large numbers of clients spread around the world. What data you send and how you send it is extremely important to providing a compelling experience to users since it can drastically affect how your project performs and feels. In Unreal Engine (UE), Replication is the name for the process of synchronizing data and procedure calls between clients and servers. The Replication system provides a higher-level abstraction along with low-level customization to make it easier to deal with all the various situations you might encounter when creating a project designed for multiple simultaneous users.



---

## Saving and Loading Your Game

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/saving-and-loading-your-game-in-unreal-engine

**Contents:**
- Saving and Loading Your Game
- Creating a SaveGame Object
  - Header
  - Source
- Saving A Game
  - Asynchronous Saving
  - Synchronous Saving
  - Binary Saving
- Loading A Game
  - Asynchronous Loading

Overview of how to save and load your game

The meaning of "saving the game" can vary considerably from one game to the next, but the general idea of enabling players to quit the game and then resume where they left off at a later time is a part of most modern games. Depending on what type of game you're making, you may only need a few basic pieces of information, such as the last checkpoint the player reached and maybe which items the player has found. Or you may need much more detailed information, possibly involving things like a long list of the player's social interactions with other in-game characters, or the current status of a variety of quests, mission objectives, or subplots.

Unreal Engine (UE) features a saving and loading system that revolves around one or more custom SaveGame classes that you create to meet your game's specific needs, including all of the information that you need to preserve across multiple play sessions. The system supports the ability to have multiple saved game files, and to save different SaveGame classes to those files. This is useful for separating globally-unlocked features from playthrough-specific game data.

The USaveGame class sets up an object that can be used as a target for the saving and loading functions declared in Kismet/GameplayStatics.h.

You can create a new class based on USaveGame using the C++ Class Wizard.

In this example, the new USaveGame class is called UMySaveGame. In order to use it, add the following lines to your game module's header file, after any other #include directives:

In the header file for your SaveGame object, you can declare any variables you want your SaveGame to store.

In this example, there are also variables declared that will be used to store default values for the SaveSlotName and the UserIndex, so that each class that saves to this SaveGame object will not have to independently set those variables. This step is optional, and will cause there to be one save slot that gets overwritten if the default values are not changed.

Generally, the SaveGame object's source file does not need any particular code to function, unless your particular save system has additional functionality you would like to set up here.

This example does define the values of SaveSlotName and UserIndex in the class constructor, so they can be read out and used by other gameplay classes.

Once you have created a SaveGame class, you can populate it with variables to store your game's data. For example, you might create an integer variable to store the player's score, or a string variable for the player's name. When you save the game, you will transfer that information from the current game world into a SaveGame object, and when loading a game, you will copy it from the SaveGame object to game object like Characters, the Player Controller, or the Game Mode.

First, call CreateSaveGameObject (from the UGameplayStatics library) to get a new UMySaveGame object. Once you have the object, you can populate it with the data you want to save. Finally, call SaveGameToSlot or AsyncSaveGameToSlot to write the data out to your device.

AsyncSaveGameToSlot is the recommended method for saving the game. Running asynchronously prevents a sudden framerate hitch, making it less noticeable to players and avoiding a possible certification issue on some platforms. When the save process is complete, the delegate (of type FAsyncSaveGameToSlotDelegate) will be called with the slot name, the user index, and a bool indicating success or failure.

SaveGameToSlot is sufficient for small SaveGame formats, and for saving the game while paused or in a menu. It's also easy to use, as it simply saves the game immediately and returns a bool indicating success or failure. For larger amounts of data, or for auto-saving game while the player is still actively interacting with your game world, AsyncSaveGameToSlot is a better choice.

You can transfer a SaveGame object to memory with the SaveGameToMemory function. This function only offers synchronous operation, but is faster than saving to a drive. The caller provides a reference to a buffer (a TArray<uint8>&) where the data will be stored. On success, the function returns true.

You can also save binary data directly to a file, similar to the SaveGameToSlot function, by calling SaveDataToSlot with the buffer (a const TArray<uint8>&) and the slot name and user ID information. As with SaveGameToMemory, this function only offers synchronous operation, and returns a bool to indicate success or failure.

On development platforms, saved game files use the .sav extension and appear in the project's Saved\SaveGames folder. On other platforms, particularly consoles, this varies to accommodate the specific file system.

To load a saved game, you must provide the save slot name and user ID that you used when you saved it. If the SaveGame you specified exists, the Engine will populate your SaveGame object with the data it contains and return it as a base SaveGame (class USaveGame) object. You can then cast that object back to your custom SaveGame class and access the data. Depending on what kind of data your SaveGame type contains, you may want to keep a copy of it, or simply use the data and discard the object.

As with saving, you can load synchronously or asynchronously. If you have a large amount of data, or wish to use a loading screen or animation during load time, we recommend the asychronous method. For small amounts of data that load quickly, a synchronous method exists.

When loading asynchronously with AsyncLoadGameFromSlot, you must provide a callback delegate in order to receive the data that the system loads.

The LoadGameFromSlot function will create and return a USaveGame object if it succeeds.

You can load SaveGame data from a file in raw, binary form with LoadDataFromSlot. This function is very similar to LoadGameFromSlot, except that it does not create a SaveGame object. Only synchronous operation is available for this type of loading.

You can also convert this binary data to a SaveGame object by calling LoadGameFromMemory. This is a synchronous call, and returns a new USaveGame object upon success, or a null pointer on failure.



**Examples:**

Example 1 (cpp):
```cpp
#include "MySaveGame.h"
	#include "Kismet/GameplayStatics.h"
```

Example 2 (cpp):
```cpp
UPROPERTY(VisibleAnywhere, Category = Basic)
	FString PlayerName;
```

Example 3 (markdown):
```markdown
#pragma once

	#include "GameFramework/SaveGame.h"
	#include "MySaveGame.generated.h"

	/**
	 *
	 */
	UCLASS()
	class [PROJECTNAME]_API UMySaveGame : public USaveGame
```

Example 4 (cpp):
```cpp
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.

	#include "[ProjectName].h"
	#include "MySaveGame.h"

	UMySaveGame::UMySaveGame()
	{
		SaveSlotName = TEXT("TestSaveSlot");
		UserIndex = 0;
	}
```

---

## Stylus & Tablet Plugin

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/StylusInput

**Contents:**
- Stylus & Tablet Plugin
- Navigation
- Modules
- Plugin Dependents

API > API/PluginIndex

Support for advanced stylus and tablet inputs such as pressure, stylus and tablet buttons, and pen angles.



---

## Windows RawInput

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/RawInput

**Contents:**
- Windows RawInput
- Navigation
- Modules

API > API/PluginIndex

RawInput provides an interface to receive input from Flight Sticks, Steering Wheels, and other non-XInput supported devices in Windows.



---

## XInput Device

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/XInputDevice

**Contents:**
- XInput Device
- Navigation
- Modules

API > API/PluginIndex

XInput is a Game Controller API for Windows.



---
