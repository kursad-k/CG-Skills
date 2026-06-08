# Godot - Scripting

**Pages:** 4

---

## Creating your first script — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/step_by_step/scripting_first_script.html

**Contents:**
- Creating your first script
- Project setup
- Creating a new script
- Hello, world!
- Turning around
  - Moving forward
- Complete script
- User-contributed notes

In this lesson, you will code your first script to make the Godot icon turn in circles. As we mentioned in the introduction, we assume you have programming foundations.

This tutorial is written for GDScript, and the equivalent C# code is included in another tab of each codeblock for convenience.

To learn more about GDScript, its keywords, and its syntax, head to the GDScript section. To learn more about C#, head to the C#/.NET section.

Please create a new project to start with a clean slate. Your project should contain one picture: the Godot icon, which we often use for prototyping in the community.

We need to create a Sprite2D node to display it in the game. In the Scene dock, click the Other Node button.

Type "Sprite2D" in the search bar to filter nodes and double-click on Sprite2D to create the node.

Your Scene tab should now only have a Sprite2D node.

A Sprite2D node needs a texture to display. In the Inspector on the right, you can see that the Texture property says <empty>. To display the Godot icon, click and drag the file icon.svg from the FileSystem dock onto the Texture slot.

You can create Sprite2D nodes automatically by dragging and dropping images on the viewport.

Then, click and drag the icon in the viewport to center it in the game view.

To create and attach a new script to our node, right-click on Sprite2D in the Scene dock and select Attach Script.

The Attach Node Script window appears. It allows you to select the script's language and file path, among other options.

Change the Template field from Node: Default to Object: Empty to start with a clean file. Leave the other options set to their default values and click the Create button to create the script.

C# script names need to match their class name. In this case, you should name the file MySprite2D.cs.

The Script workspace should appear with your new sprite_2d.gd file open and the following line of code:

Every GDScript file is implicitly a class. The extends keyword defines the class this script inherits or extends. In this case, it's Sprite2D, meaning our script will get access to all the properties and functions of the Sprite2D node, including classes it extends, like Node2D, CanvasItem, and Node.

In GDScript, if you omit the line with the extends keyword, your class will implicitly extend RefCounted, which Godot uses to manage your application's memory.

Inherited properties include the ones you can see in the Inspector dock, like our node's texture.

By default, the Inspector displays a node's properties in "Title Case", with capitalized words separated by a space. In GDScript code, these properties are in "snake_case", which is lowercase with words separated by an underscore.

You can hover over any property's name in the Inspector to see a description and its identifier in code.

Our script currently doesn't do anything. Let's make it print the text "Hello, world!" to the Output bottom panel to get started.

Add the following code to your script:

Let's break it down. The func keyword defines a new function named _init. This is a special name for our class's constructor. The engine calls _init() on every object or node upon creating it in memory, if you define this function.

GDScript is an indent-based language. The tab at the start of the line that says print() is necessary for the code to work. If you omit it or don't indent a line correctly, the editor will highlight it in red and display the following error message: "Indented block expected".

Save the scene as sprite_2d.tscn if you haven't already, then press F6 (Cmd + R on macOS) to run it. Look at the Output bottom panel that expands. It should display "Hello, world!".

Delete the _init() function, so you're only left with the line extends Sprite2D.

It's time to make our node move and rotate. To do so, we're going to add two member variables to our script: the movement speed in pixels per second and the angular speed in radians per second. Add the following after the extends Sprite2D line.

Member variables sit near the top of the script, after any "extends" lines, but before functions. Every node instance with this script attached to it will have its own copy of the speed and angular_speed properties.

Angles in Godot work in radians by default, but you have built-in functions and properties available if you prefer to calculate angles in degrees instead.

To move our icon, we need to update its position and rotation every frame in the game loop. We can use the _process() virtual function of the Node class. If you define it in any class that extends the Node class, like Sprite2D, Godot will call the function every frame and pass it an argument named delta, the time elapsed since the last frame.

Games work by rendering many images per second, each called a frame, and they do so in a loop. We measure the rate at which a game produces images in Frames Per Second (FPS). Most games aim for 60 FPS, although you might find figures like 30 FPS on slower mobile devices or 90 to 240 for virtual reality games.

The engine and game developers do their best to update the game world and render images at a constant time interval, but there are always small variations in frame render times. That's why the engine provides us with this delta time value, making our motion independent of our framerate.

At the bottom of the script, define the function:

The func keyword defines a new function. After it, we have to write the function's name and arguments it takes in parentheses. A colon ends the definition, and the indented blocks that follow are the function's content or instructions.

Notice how _process(), like _init(), starts with a leading underscore. By convention, Godot's virtual functions, that is to say, built-in functions you can override to communicate with the engine, start with an underscore.

The line inside the function, rotation += angular_speed * delta, increments our sprite's rotation every frame. Here, rotation is a property inherited from the class Node2D, which Sprite2D extends. It controls the rotation of our node and works with radians.

In the code editor, you can Ctrl + Click (Cmd + Click on macOS) on any built-in property or function like position, rotation, or _process to open the corresponding documentation in a new tab.

Run the scene to see the Godot icon turn in-place.

In C#, notice how the delta argument taken by _Process() is a double. We therefore need to convert it to float when we apply it to the rotation.

Let's now make the node move. Add the following two lines inside of the _process() function, ensuring the new lines are indented the same way as the rotation += angular_speed * delta line before them.

As we already saw, the var keyword defines a new variable. If you put it at the top of the script, it defines a property of the class. Inside a function, it defines a local variable: it only exists within the function's scope.

We define a local variable named velocity, a 2D vector representing both a direction and a speed. To make the node move forward, we start from the Vector2 class's constant Vector2.UP, a vector pointing up, and rotate it by calling the Vector2 method rotated(). This expression, Vector2.UP.rotated(rotation), is a vector pointing forward relative to our icon. Multiplied by our speed property, it gives us a velocity we can use to move the node forward.

We add velocity * delta to the node's position to move it. The position itself is of type Vector2, a built-in type in Godot representing a 2D vector.

Run the scene to see the Godot head run in circles.

Moving a node like that does not take into account colliding with walls or the floor. In Your first 2D game, you will learn another approach to moving objects while detecting collisions.

Our node currently moves by itself. In the next part, Listening to player input, we'll use player input to control it.

Here is the complete sprite_2d.gd file for reference.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Listening to player input — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/step_by_step/scripting_player_input.html

**Contents:**
- Listening to player input
- Moving when pressing "up"
- Complete script
- Summary
- User-contributed notes

Building upon the previous lesson, Creating your first script, let's look at another important feature of any game: giving control to the player. To add this, we need to modify our sprite_2d.gd code.

You have two main tools to process the player's input in Godot:

The built-in input callbacks, mainly _unhandled_input(). Like _process(), it's a built-in virtual function that Godot calls every time the player presses a key. It's the tool you want to use to react to events that don't happen every frame, like pressing Space to jump. To learn more about input callbacks, see Using InputEvent.

The Input singleton. A singleton is a globally accessible object. Godot provides access to several in scripts. It's the right tool to check for input every frame.

We're going to use the Input singleton here as we need to know if the player wants to turn or move every frame.

For turning, we should use a new variable: direction. In our _process() function, replace the rotation += angular_speed * delta line with the code below.

Our direction local variable is a multiplier representing the direction in which the player wants to turn. A value of 0 means the player isn't pressing the left or the right arrow key. A value of 1 means the player wants to turn right, and -1 means they want to turn left.

To produce these values, we introduce conditional statements and the use of Input. A conditional statement starts with the if keyword in GDScript and ends with a colon. The condition is specifically the expression between the keyword and the colon at the end of the line.

To check if a key was pressed this frame, we call Input.is_action_pressed(). The method takes a text string representing an input action and returns true if the action is pressed, false otherwise.

The two actions we use above, "ui_left" and "ui_right", are predefined in every Godot project. They respectively trigger when the player presses the left and right arrows on the keyboard or left and right on a gamepad's D-pad.

You can see and edit input actions in your project by going to Project > Project Settings and clicking on the Input Map tab.

Finally, we use the direction as a multiplier when we update the node's rotation: rotation += angular_speed * direction * delta.

Comment out the lines var velocity = Vector2.UP.rotated(rotation) * speed and position += velocity * delta like this:

This will ignore the code that moved the icon's position in a circle without user input from the previous exercise.

If you run the scene with this code, the icon should rotate when you press Left and Right.

To only move when pressing a key, we need to modify the code that calculates the velocity. Uncomment the code and replace the line starting with var velocity with the code below.

We initialize the velocity with a value of Vector2.ZERO, another constant of the built-in Vector type representing a 2D vector of length 0.

If the player presses the "ui_up" action, we then update the velocity's value, causing the sprite to move forward.

Here is the complete sprite_2d.gd file for reference.

If you run the scene, you should now be able to rotate with the left and right arrow keys and move forward by pressing Up.

In summary, every script in Godot represents a class and extends one of the engine's built-in classes. The node types your classes inherit from give you access to properties, such as rotation and position in our sprite's case. You also inherit many functions, which we didn't get to use in this example.

In GDScript, the variables you put at the top of the file are your class's properties, also called member variables. Besides variables, you can define functions, which, for the most part, will be your classes' methods.

Godot provides several virtual functions you can define to connect your class with the engine. These include _process(), to apply changes to the node every frame, and _unhandled_input(), to receive input events like key and button presses from the users. There are quite a few more.

The Input singleton allows you to react to the player's input anywhere in your code. In particular, you'll get to use it in the _process() loop.

In the next lesson, Using signals, we'll build upon the relationship between scripts and nodes by having our nodes trigger code in scripts.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Scripting development — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/scripting_development.html

**Contents:**
- Scripting development
- GDScript
  - Annotation guidelines
- User-contributed notes

Create annotations for modifiers that act on the script or its code. Additionally, create annotations for behavior that is specific to the Godot engine and editor; if the primary purpose is to affect the way that the engine or editor treats or interacts with the script, implement the token as an annotation.

Do not create annotations for general programming language features.

For historical reasons, some existing annotations and keywords do not strictly follow these guidelines. Choosing between implementing a feature as an annotation or as a language keyword is a nuanced decision that should be made through discussion with other GDScript developers.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Scripting languages — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/step_by_step/scripting_languages.html

**Contents:**
- Scripting languages
- Available scripting languages
- Which language should I use?
  - GDScript
  - .NET / C#
  - C++ via GDExtension
- Summary
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

This lesson will give you an overview of the available scripting languages in Godot. You will learn the pros and cons of each option. In the next part, you will write your first script using GDScript.

Scripts attach to a node and extend its behavior. This means that scripts inherit all functions and properties of the node they attach to.

For example, take a game where a Camera2D node follows a ship. The Camera2D node follows its parent by default. Imagine you want the camera to shake when the player takes damage. As this feature is not built into Godot, you would attach a script to the Camera2D node and code the shake.

Godot offers four gameplay programming languages: GDScript, C#, and, via its GDExtension technology, C and C++. There are more community-supported languages, but these are the official ones.

You can use multiple languages in a single project. For instance, in a team, you could code gameplay logic in GDScript as it's fast to write, and use C# or C++ to implement complex algorithms and maximize their performance. Or you can write everything in GDScript or C#. It's your call.

We provide this flexibility to answer the needs of different game projects and developers.

If you're a beginner, we recommend to start with GDScript. We made this language specifically for Godot and the needs of game developers. It has a lightweight and straightforward syntax and provides the tightest integration with Godot.

For C#, you will need an external code editor like VSCode or Visual Studio. While C# support is now mature, you will find fewer learning resources for it compared to GDScript. That's why we recommend C# mainly to users who already have experience with the language.

Let's look at each language's features, as well as its pros and cons.

GDScript is an object-oriented and imperative programming language built for Godot. It's made by and for game developers to save you time coding games. Its features include:

A simple syntax that leads to short files.

Blazing fast compilation and loading times.

Tight editor integration, with code completion for nodes, signals, and more information from the scene it's attached to.

Built-in vector and transform types, making it efficient for heavy use of linear algebra, a must for games.

Supports multiple threads as efficiently as statically typed languages.

No garbage collection, as this feature eventually gets in the way when creating games. The engine counts references and manages the memory for you in most cases by default, but you can also control memory if you need to.

Gradual typing. Variables have dynamic types by default, but you also can use type hints for strong type checks.

GDScript looks like Python as you structure your code blocks using indentations, but it doesn't work the same way in practice. It's inspired by multiple languages, including Squirrel, Lua, and Python.

Why don't we use Python or Lua directly?

Years ago, Godot used Python, then Lua. Both languages' integration took a lot of work and had severe limitations. For example, threading support was a big challenge with Python.

Developing a dedicated language doesn't take us more work and we can tailor it to game developers' needs. We're now working on performance optimizations and features that would've been difficult to offer with third-party languages.

As Microsoft's C# is a favorite amongst game developers, we officially support it. C# is a mature and flexible language with tons of libraries written for it. We were able to add support for it thanks to a generous donation from Microsoft.

C# offers a good tradeoff between performance and ease of use, although you should be aware of its garbage collector.

You must use the .NET edition of the Godot editor to script in C#. You can download it on the Godot website's download page.

Since Godot uses .NET 8, in theory, you can use any third-party .NET library or framework in Godot, as well as any Common Language Infrastructure-compliant programming language, such as F#, Boo, or ClojureCLR. However, C# is the only officially supported .NET option.

GDScript code itself doesn't execute as fast as compiled C# or C++. However, most script code calls functions written with fast algorithms in C++ code inside the engine. In many cases, writing gameplay logic in GDScript, C#, or C++ won't have a significant impact on performance.

Projects written in C# using Godot 4 currently cannot be exported to the web platform. To use C# on that platform, consider Godot 3 instead. Android and iOS platform support is available as of Godot 4.2, but is experimental and some limitations apply.

To learn more about C#, head to the C#/.NET section.

GDExtension allows you to write game code in C++ without needing to recompile Godot.

You can use any version of the language or mix compiler brands and versions for the generated shared libraries, thanks to our use of an internal C API Bridge.

GDExtension is the best choice for performance. You don't need to use it throughout an entire game, as you can write other parts in GDScript or C#.

When working with GDExtension, the available types, functions, and properties closely resemble Godot's actual C++ API.

Scripts are files containing code that you attach to a node to extend its functionality.

Godot supports four official scripting languages, offering you flexibility between performance and ease of use.

You can mix languages, for instance, to implement demanding algorithms with C or C++ and write most of the game logic with GDScript or C#.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---
