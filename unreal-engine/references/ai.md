# Unreal-Engine - Ai

**Pages:** 3

---

## Artificial Intelligence

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/artificial-intelligence-in-unreal-engine

**Contents:**
- Artificial Intelligence
- General Topics
- Machine Learning

Describes the systems available within Unreal Engine that can be used to create believable AI entities in your projects.



---

## Behavior Trees

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine

**Contents:**
- Behavior Trees
- Starting Out
- Essentials

Documents the Behavior Trees asset in Unreal Engine and how it can be used to create Artificial Intelligence (AI) for non-player characters in your projects.

Behavior Trees assets in Unreal Engine 5 (Unreal Engine) can be used to create artificial intelligence (AI) for non-player characters in your projects. While the Behavior Tree asset is used to execute branches containing logic, to determine which branches should be executed, the Behavior Tree relies on another asset called a Blackboard which serves as the "brain" for a Behavior Tree.

The Blackboard contains several user-defined Keys that hold information used by the Behavior Tree to make decisions. For example, you could have a Boolean Key called Is Light On which the Behavior Tree can reference to see if the value has changed. If the value is true, it could execute a branch that causes a roach to flee. If it is false, it could execute a different branch where the roach maybe moves randomly around the environment. Behavior Trees can be as simplistic as the roach example given, or as complex as simulating another human player in a multiplayer game that finds cover, shoots at players, and looks for item pickups.

If you are new to Behavior Trees in Unreal Engine, it is recommended that you go through the Behavior Tree Quick Start guide to quickly get an AI character up and running. If you are already familiar with the concept of Behavior Trees from other applications, you may want to check out the Essentials section which contains an overview of how Behavior Trees work in Unreal Engine, a User Guide to working with Behavior Trees and Blackboards, as well as reference pages for the different types of nodes available within Behavior Trees.



---

## Environment Query System

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-system-in-unreal-engine

**Contents:**
- Environment Query System
- Starting Out
- Essentials

Documents the Environment Query System (EQS) and how it can be used to query the environment for data. That data can then be used to provide the AI with data used in the decision-making process on how to proceed.

The Environment Query System (EQS) is a feature within the Artificial Intelligence system in Unreal Engine 5 (Unreal Engine) that is used to collect data from the environment. Within EQS, you can ask questions about the data collected through a variety of different Tests which produces an Item that best fits the type of question asked.

An EQS Query can be called from a Behavior Tree and used to make decisions on how to proceed based on the results of your Tests. EQS Queries are primarily made up of Generators (which are used to produce the locations or Actors that will be tested and weighted) and Contexts (which are used as a frame of reference for any Tests or Generators). EQS Queries can be used to instruct AI characters to find the best possible location that will provide a line of sight to a player to attack, the nearest health or ammo pickup, or where the closest cover point (among other possibilities).

Once you have a general understanding of how Behavior Trees work in Unreal Engine and want to have your AI query the environment, you may want to start with the Environment Query System Quick Start guide which will walk you through an end-to-end example of having the AI find the best possible position to attack from a range against the player. Also refer to the Essentials section for an overview of EQS, a User Guide to working with EQS, and a node reference page that breaks down the available nodes and properties within EQS.



---
