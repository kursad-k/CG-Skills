# Godot - Getting Started

**Pages:** 16

---

## Coding the player — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/first_2d_game/03.coding_the_player.html

**Contents:**
- Coding the player
- Choosing animations
- Preparing for collisions
- User-contributed notes

In this lesson, we'll add player movement, animation, and set it up to detect collisions.

To do so, we need to add some functionality that we can't get from a built-in node, so we'll add a script. Click the Player node and click the "Attach Script" button:

In the script settings window, you can leave the default settings alone. Just click "Create":

If you're creating a C# script or other languages, select the language from the language drop down menu before hitting create.

If this is your first time encountering GDScript, please read Scripting languages before continuing.

Start by declaring the member variables this object will need:

Using the export keyword on the first variable speed allows us to set its value in the Inspector. This can be handy for values that you want to be able to adjust just like a node's built-in properties. Click on the Player node and you'll see the property now appears in the Inspector in a new section with the name of the script. Remember, if you change the value here, it will override the value written in the script.

If you're using C#, you need to (re)build the project assemblies whenever you want to see new export variables or signals. This build can be manually triggered by clicking the Build button at the top right of the editor.

Your player.gd script should already contain a _ready() and a _process() function. If you didn't select the default template shown above, create these functions while following the lesson.

The _ready() function is called when a node enters the scene tree, which is a good time to find the size of the game window:

Now we can use the _process() function to define what the player will do. _process() is called every frame, so we'll use it to update elements of our game, which we expect will change often. For the player, we need to do the following:

Move in the given direction.

Play the appropriate animation.

First, we need to check for input - is the player pressing a key? For this game, we have 4 direction inputs to check. Input actions are defined in the Project Settings under "Input Map". Here, you can define custom events and assign different keys, mouse events, or other inputs to them. For this game, we will map the arrow keys to the four directions.

Click on Project -> Project Settings to open the project settings window and click on the Input Map tab at the top. Type "move_right" in the top bar and click the "Add" button to add the move_right action.

We need to assign a key to this action. Click the "+" icon on the right, to open the event manager window.

The "Listening for Input..." field should automatically be selected. Press the "right" key on your keyboard, and the menu should look like this now.

Select the "ok" button. The "right" key is now associated with the move_right action.

Repeat these steps to add three more mappings:

move_left mapped to the left arrow key.

move_up mapped to the up arrow key.

And move_down mapped to the down arrow key.

Your input map tab should look like this:

Click the "Close" button to close the project settings.

We only mapped one key to each input action, but you can map multiple keys, joystick buttons, or mouse buttons to the same input action.

You can detect whether a key is pressed using Input.is_action_pressed(), which returns true if it's pressed or false if it isn't.

We start by setting the velocity to (0, 0) - by default, the player should not be moving. Then we check each input and add/subtract from the velocity to obtain a total direction. For example, if you hold right and down at the same time, the resulting velocity vector will be (1, 1). In this case, since we're adding a horizontal and a vertical movement, the player would move faster diagonally than if it just moved horizontally.

We can prevent that if we normalize the velocity, which means we set its length to 1, then multiply by the desired speed. This means no more fast diagonal movement.

If you've never used vector math before, or need a refresher, you can see an explanation of vector usage in Godot at Vector math. It's good to know but won't be necessary for the rest of this tutorial.

We also check whether the player is moving so we can call play() or stop() on the AnimatedSprite2D.

$ is shorthand for get_node(). So in the code above, $AnimatedSprite2D.play() is the same as get_node("AnimatedSprite2D").play().

In GDScript, $ returns the node at the relative path from the current node, or returns null if the node is not found. Since AnimatedSprite2D is a child of the current node, we can use $AnimatedSprite2D.

Now that we have a movement direction, we can update the player's position. We can also use clamp() to prevent it from leaving the screen. Clamping a value means restricting it to a given range. Add the following to the bottom of the _process function (make sure it's not indented under the else):

The delta parameter in the _process() function refers to the frame length - the amount of time that the previous frame took to complete. Using this value ensures that your movement will remain consistent even if the frame rate changes.

Click "Run Current Scene" (F6, Cmd + R on macOS) and confirm you can move the player around the screen in all directions.

If you get an error in the "Debugger" panel that says

Attempt to call function 'play' in base 'null instance' on a null instance

this likely means you spelled the name of the AnimatedSprite2D node wrong. Node names are case-sensitive and $NodeName must match the name you see in the scene tree.

Now that the player can move, we need to change which animation the AnimatedSprite2D is playing based on its direction. We have the "walk" animation, which shows the player walking to the right. This animation should be flipped horizontally using the flip_h property for left movement. We also have the "up" animation, which should be flipped vertically with flip_v for downward movement. Let's place this code at the end of the _process() function:

The boolean assignments in the code above are a common shorthand for programmers. Since we're doing a comparison test (boolean) and also assigning a boolean value, we can do both at the same time. Consider this code versus the one-line boolean assignment above:

Play the scene again and check that the animations are correct in each of the directions.

A common mistake here is to type the names of the animations wrong. The animation names in the SpriteFrames panel must match what you type in the code. If you named the animation "Walk", you must also use a capital "W" in the code.

When you're sure the movement is working correctly, add this line to _ready(), so the player will be hidden when the game starts:

We want Player to detect when it's hit by an enemy, but we haven't made any enemies yet! That's OK, because we're going to use Godot's signal functionality to make it work.

Add the following at the top of the script. If you're using GDScript, add it after extends Area2D. If you're using C#, add it after public partial class Player : Area2D:

This defines a custom signal called "hit" that we will have our player emit (send out) when it collides with an enemy. We will use Area2D to detect the collision. Select the Player node and click the "Node" tab next to the Inspector tab to see the list of signals the player can emit:

Notice our custom "hit" signal is there as well! Since our enemies are going to be RigidBody2D nodes, we want the body_entered(body: Node2D) signal. This signal will be emitted when a body contacts the player. Click "Connect.." and the "Connect a Signal" window appears.

Godot will create a function with that exact name directly in script for you. You don't need to change the default settings right now.

If you're using an external text editor (for example, Visual Studio Code), a bug currently prevents Godot from doing so. You'll be sent to your external editor, but the new function won't be there.

In this case, you'll need to write the function yourself into the Player's script file.

Note the green icon indicating that a signal is connected to this function; this does not mean the function exists, only that the signal will attempt to connect to a function with that name, so double-check that the spelling of the function matches exactly!

Next, add this code to the function:

Each time an enemy hits the player, the signal is going to be emitted. We need to disable the player's collision so that we don't trigger the hit signal more than once.

Disabling the area's collision shape can cause an error if it happens in the middle of the engine's collision processing. Using set_deferred() tells Godot to wait to disable the shape until it's safe to do so.

The last piece is to add a function we can call to reset the player when starting a new game.

With the player working, we'll work on the enemy in the next lesson.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Creating instances — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/step_by_step/instancing.html

**Contents:**
- Creating instances
- In practice
- Editing scenes and instances
- Scene instances as a design language
- Summary
- User-contributed notes

This tutorial refers to instancing scenes in the editor. To learn how to instance scenes from code, see Nodes and scene instances.

Godot's approach to instancing described below should not be confused with hardware instancing that can be used to render large amounts of similar objects quickly. See Optimization using MultiMeshes instead.

In the previous part, we saw that a scene is a collection of nodes organized in a tree structure, with a single node as its root. You can split your project into any number of scenes. This feature helps you break down and organize your game's different components.

You can create as many scenes as you'd like and save them as files with the .tscn extension, which stands for "text scene". The label.tscn file from the previous lesson was an example. We call those files "Packed Scenes" as they pack information about your scene's content.

Here's an example of a ball. It's composed of a RigidBody2D node as its root named Ball, which allows the ball to fall and bounce on walls, a Sprite2D node, and a CollisionShape2D.

Once you have saved a scene, it works as a blueprint: you can reproduce it in other scenes as many times as you'd like. Replicating an object from a template like this is called instancing.

As we mentioned in the previous part, instanced scenes behave like a node: the editor hides their content by default. When you instance the Ball, you only see the Ball node. Notice also how each duplicate has a unique name.

Every instance of the Ball scene starts with the same structure and properties as ball.tscn. However, you can modify each independently, such as changing how they bounce, how heavy they are, or any property exposed by the source scene.

Let's use instancing in practice to see how it works in Godot. We invite you to download the ball's sample project we prepared for you: instancing_starter.zip.

Extract the archive on your computer. To import it, you need the Project Manager. The Project Manager is accessed by opening Godot, or if you already have Godot opened, click on Project > Quit to Project List (Ctrl + Shift + Q, Ctrl + Option + Cmd + Q on macOS)

In the Project Manager, click the Import button to import the project.

In the pop-up that appears navigate to the folder you extracted. Double-click the project.godot file to open it.

Finally, click the Import button.

A window notifying you that the project was last opened in an older Godot version may appear, that's not an issue. Click Ok to open the project.

The project contains two packed scenes: main.tscn, containing walls against which the ball collides, and ball.tscn. The Main scene should open automatically. If you're seeing an empty 3D scene instead of the main scene, click the 2D button at the top of the screen.

Let's add a ball as a child of the Main node. In the Scene dock, select the Main node. Then, click the link icon at the top of the scene dock. This button allows you to add an instance of a scene as a child of the currently selected node.

Double-click the ball scene to instance it.

The ball appears in the top-left corner of the viewport.

Click on it and drag it towards the center of the view.

Play the game by pressing F5 (Cmd + B on macOS). You should see it fall.

Now, we want to create more instances of the Ball node. With the ball still selected, press Ctrl + D (Cmd + D on macOS) to call the duplicate command. Click and drag to move the new ball to a different location.

You can repeat this process until you have several in the scene.

Play the game again. You should now see every ball fall independently from one another. This is what instances do. Each is an independent reproduction of a template scene.

There is more to instances. With this feature, you can:

Change the properties of one ball without affecting the others using the Inspector.

Change the default properties of every Ball by opening the ball.tscn scene and making a change to the Ball node there. Upon saving, all instances of the Ball in the project will see their values update.

Changing a property on an instance always overrides values from the corresponding packed scene.

Let's try this. Double-click ball.tscn in the FileSystem to open it.

In the Scene dock on the left, select the Ball node. Then, in the Inspector on the right, click on the PhysicsMaterial property to expand it.

Set its Bounce property to 0.5 by clicking on the number field, typing 0.5, and pressing Enter.

Play the game by pressing F5 (Cmd + B on macOS) and notice how all balls now bounce a lot more. As the Ball scene is a template for all instances, modifying it and saving causes all instances to update accordingly.

Let's now adjust an individual instance. Head back to the Main scene by clicking on the corresponding tab above the viewport.

Select one of the instanced Ball nodes and, in the Inspector, set its Gravity Scale value to 10.

A grey "revert" button appears next to the adjusted property.

This icon indicates you are overriding a value from the source packed scene. Even if you modify the property in the original scene, the value override will be preserved in the instance. Clicking the revert icon will restore the property to the value in the saved scene.

Rerun the game and notice how this ball now falls much faster than the others.

You may notice you are unable to change the values of the PhysicsMaterial of the ball. This is because PhysicsMaterial is a resource, and needs to be made unique before you can edit it in a scene that is linking to its original scene. To make a resource unique for one instance, right-click on the Physics Material property in the Inspector and click Make Unique in the context menu.

Resources are another essential building block of Godot games we will cover in a later lesson.

Instances and scenes in Godot offer an excellent design language, setting the engine apart from others out there. We designed Godot around this concept from the ground up.

We recommend dismissing architectural code patterns when making games with Godot, such as Model-View-Controller (MVC) or Entity-Relationship diagrams. Instead, you can start by imagining the elements players will see in your game and structure your code around them.

For example, you could break down a shooter game like so:

You can come up with a diagram like this for almost any type of game. Each rectangle represents an entity that's visible in the game from the player's perspective. The arrows point towards the instantiator of each scene.

Once you have a diagram, we recommend creating a scene for each element listed in it to develop your game. You'll use instancing, either by code or directly in the editor, to build your tree of scenes.

Programmers tend to spend a lot of time designing abstract architectures and trying to fit components into it. Designing based on scenes makes development faster and more straightforward, allowing you to focus on the game logic itself. Because most game components map directly to a scene, using a design based on scene instantiation means you need little other architectural code.

Here's the example of a scene diagram for an open-world game with tons of assets and nested elements:

Imagine we started by creating the room. We could make a couple of different room scenes, with unique arrangements of furniture in them. Later, we could make a house scene that uses multiple room instances for the interior. We would create a citadel out of many instanced houses and a large terrain on which we would place the citadel. Each of these would be a scene instancing one or more sub-scenes.

Later, we could create scenes representing guards and add them to the citadel. They would be indirectly added to the overall game world.

With Godot, it's easy to iterate on your game like this, as all you need to do is create and instantiate more scenes. We designed the editor to be accessible to programmers, designers, and artists alike. A typical team development process can involve 2D or 3D artists, level designers, game designers, and animators, all working with the Godot editor.

Instancing, the process of producing an object from a blueprint, has many handy uses. With scenes, it gives you:

The ability to divide your game into reusable components.

A tool to structure and encapsulate complex systems.

A language to think about your game project's structure in a natural way.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Creating the enemy — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/first_2d_game/04.creating_the_enemy.html

**Contents:**
- Creating the enemy
- Node setup
- Enemy script
- User-contributed notes

Now it's time to make the enemies our player will have to dodge. Their behavior will not be very complex: mobs will spawn randomly at the edges of the screen, choose a random direction, and move in a straight line.

We'll create a Mob scene, which we can then instance to create any number of independent mobs in the game.

Click Scene -> New Scene from the top menu and add the following nodes:

RigidBody2D (named Mob)

VisibleOnScreenNotifier2D

Don't forget to set the children so they can't be selected, like you did with the Player scene. This is done by selecting the parent node (RigidBody2D) in the Scene tree dock, then using the Group button at the top of the 2D editor (or pressing Ctrl + G).

Select the Mob node and set its Gravity Scale property in the RigidBody2D section of the inspector to 0. This will prevent the mob from falling downwards.

In addition, under the CollisionObject2D section just beneath the RigidBody2D section, expand the Collision group and uncheck the 1 inside the Mask property. This will ensure the mobs do not collide with each other.

Set up the AnimatedSprite2D like you did for the player. This time, we have 3 animations: fly, swim, and walk. There are two images for each animation in the art folder.

The Animation Speed property has to be set for each individual animation. Adjust it to 3 for all 3 animations.

You can use the "Play Animation" buttons on the right of the Animation Speed input field to preview your animations.

We'll select one of these animations randomly so that the mobs will have some variety.

Like the player images, these mob images need to be scaled down. Set the AnimatedSprite2D's Scale property to (0.75, 0.75).

As in the Player scene, add a CapsuleShape2D for the collision. To align the shape with the image, you'll need to set the Rotation property to 90 (under "Transform" in the Inspector).

Add a script to the Mob like this:

Now let's look at the rest of the script. In _ready() we play the animation and randomly choose one of the three animation types:

First, we get the list of animation names from the AnimatedSprite2D's sprite_frames property. This returns an Array containing all three animation names: ["walk", "swim", "fly"].

In the GDScript code, we use the Array.pick_random method to select one of these animation names at random. Meanwhile, in the C# code, we pick a random number between 0 and 2 to select one of these names from the list (array indices start at 0). The expression GD.Randi() % n selects a random integer between 0 and n-1.

Finally, we call play() to start playing the chosen animation.

The last piece is to make the mobs delete themselves when they leave the screen. Connect the screen_exited() signal of the VisibleOnScreenNotifier2D node to the Mob and add this code:

queue_free() is a function that essentially 'frees', or deletes, the node at the end of the frame.

This completes the Mob scene.

With the player and enemies ready, in the next part, we'll bring them together in a new scene. We'll make enemies spawn randomly around the game board and move forward, turning our project into a playable game.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Creating the player scene — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/first_2d_game/02.player_scene.html

**Contents:**
- Creating the player scene
- Node structure
- Sprite animation
- User-contributed notes

With the project settings in place, we can start working on the player-controlled character.

The first scene will define the Player object. One of the benefits of creating a separate Player scene is that we can test it separately, even before we've created other parts of the game.

To begin, we need to choose a root node for the player object. As a general rule, a scene's root node should reflect the object's desired functionality - what the object is. In the upper-left corner, in the "Scene" tab, click the "Other Node" button and add an Area2D node to the scene.

When you add the Area2D node, Godot will display the following warning icon next to it in the scene tree:

This warning tells us that the Area2D node requires a shape to detect collisions or overlaps. We can ignore the warning temporarily because we will first set up the player's visuals (using an animated sprite). Once the visuals are ready, we will add a collision shape as a child node. This will allow us to accurately size and position the shape based on the sprite's appearance.

With Area2D we can detect objects that overlap or run into the player. Change the node's name to Player by double-clicking on it. Now that we've set the scene's root node, we can add additional nodes to give it more functionality.

Before we add any children to the Player node, we want to make sure we don't accidentally move or resize them by clicking on them. Select the node and click the icon to the right of the lock. Its tooltip says "Groups the selected node with its children. This causes the parent to be selected when any child node is clicked in 2D and 3D view."

Save the scene as player.tscn. Click Scene > Save, or press Ctrl + S on Windows/Linux or Cmd + S on macOS.

For this project, we will be following the Godot naming conventions.

GDScript: Classes (nodes) use PascalCase, variables and functions use snake_case, and constants use ALL_CAPS (See GDScript style guide).

C#: Classes, export variables and methods use PascalCase, private fields use _camelCase, local variables and parameters use camelCase (See C# style guide). Be careful to type the method names precisely when connecting signals.

Click on the Player node and add (Ctrl + A on Windows/Linux or Cmd + A on macOS) a child node AnimatedSprite2D. The AnimatedSprite2D will handle the appearance and animations for our player. Notice that there is a warning symbol next to the node. An AnimatedSprite2D requires a SpriteFrames resource, which is a list of the animations it can display. Make sure AnimatedSprite2D is selected and then find the Sprite Frames property under the Animation section in the Inspector and click "[empty]" -> "New SpriteFrames":

Click on the SpriteFrames you just created to open the "SpriteFrames" panel:

On the left is a list of animations. Click the default one and rename it to walk. Then click the Add Animation button to create a second animation named up.

Find the player images in the FileSystem dock - they're in the art folder you unzipped earlier. Drag the two images for each animation, into the Animation Frames side of the panel for the corresponding animation:

playerGrey_walk1 and playerGrey_walk2 for the walk animation

playerGrey_up1 and playerGrey_up2 for the up animation

The player images are a bit too large for the game window, so we need to scale them down. Click on the AnimatedSprite2D node and set the Scale property to (0.5, 0.5). You can find it in the Inspector under the Node2D heading.

Finally, add a CollisionShape2D as a child of Player. This will determine the player's "hitbox", or the bounds of its collision area. For this character, a CapsuleShape2D node gives the best fit, so next to "Shape" in the Inspector, click "[empty]" -> "New CapsuleShape2D". Using the two size handles, resize the shape to cover the sprite:

When you're finished, your Player scene should look like this:

Once this is done, the warning on the Area2D node will disappear, as it now has a shape assigned and can interact with other objects.

Make sure to save the scene again after these changes.

In the next part, we'll add a script to the player node to move and animate it. Then, we'll set up collision detection to know when the player got hit by something.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Finishing up — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/first_2d_game/07.finishing-up.html

**Contents:**
- Finishing up
- Background
- Sound effects
- Keyboard shortcut
- Sharing the finished game with others
- User-contributed notes

We have now completed all the functionality for our game. Below are some remaining steps to add a bit more "juice" to improve the game experience.

Feel free to expand the gameplay with your own ideas.

The default gray background is not very appealing, so let's change its color. One way to do this is to use a ColorRect node. Make it the first node under Main so that it will be drawn behind the other nodes. ColorRect only has one property: Color. Choose a color you like and select "Layout" -> "Anchors Preset" -> "Full Rect" either in the toolbar at the top of the viewport or in the inspector so that it covers the screen.

You could also add a background image, if you have one, by using a TextureRect node instead.

Sound and music can be the single most effective way to add appeal to the game experience. In your game's art folder, you have two sound files: "House In a Forest Loop.ogg" for background music, and "gameover.wav" for when the player loses.

Add two AudioStreamPlayer nodes as children of Main. Name one of them Music and the other DeathSound. On each one, click on the Stream property, select "Load", and choose the corresponding audio file.

All audio is automatically imported with the Loop setting disabled. If you want the music to loop seamlessly, click on the Stream file arrow, select Make Unique, then click on the Stream file and check the Loop box.

To play the music, add $Music.play() in the new_game() function and $Music.stop() in the game_over() function.

Finally, add $DeathSound.play() in the game_over() function.

Since the game is played with keyboard controls, it would be convenient if we could also start the game by pressing a key on the keyboard. We can do this with the "Shortcut" property of the Button node.

In a previous lesson, we created four input actions to move the character. We will create a similar input action to map to the start button.

Select "Project" -> "Project Settings" and then click on the "Input Map" tab. In the same way you created the movement input actions, create a new input action called start_game and add a key mapping for the Enter key.

Now would be a good time to add controller support if you have one available. Attach or pair your controller and then under each input action that you wish to add controller support for, click on the "+" button and press the corresponding button, d-pad, or stick direction that you want to map to the respective input action.

In the HUD scene, select the StartButton and find its Shortcut property in the Inspector. Create a new Shortcut resource by clicking within the box, open the Events array and add a new array element to it by clicking on Array[InputEvent] (size 0).

Create a new InputEventAction and name it start_game.

Now when the start button appears, you can either click it or press Enter to start the game.

And with that, you completed your first 2D game in Godot.

You got to make a player-controlled character, enemies that spawn randomly around the game board, count the score, implement a game over and replay, user interface, sounds, and more. Congratulations!

There's still much to learn, but you can take a moment to appreciate what you achieved.

And when you're ready, you can move on to Your first 3D game to learn to create a complete 3D game from scratch, in Godot.

If you want people to try out your game without having to install Godot, you'll need to export the project for each operating system you want the game to be playable on. See Exporting projects for instructions.

After exporting the project, compress the exported executable and PCK file (not the raw project files) to a ZIP file, then upload this ZIP file to a file sharing website.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## First look at Godot's interface — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/introduction/first_look_at_the_editor.html

**Contents:**
- First look at Godot's interface
- The Project Manager
- First look at Godot's editor
- The five main screens
- Integrated class reference
- User-contributed notes

This page will give you a brief overview of Godot's interface. We're going to look at the different main screens and docks to help you situate yourself.

For a comprehensive breakdown of the editor's interface and how to use it, see the Editor manual.

When you launch Godot, the first window you see is the Project Manager. In the default tab Projects, you can manage existing projects, import or create new ones, and more.

At the top of the window, there is another tab named Asset Library. The first time you go to this tab you'll see a "Go Online" button. For privacy reasons, the Godot project manager does not access the internet by default. To change this click the "Go Online" button. You can change this option later in the settings.

Once your network mode is set to "online", you can search for demo projects in the open source asset library, which includes many projects developed by the community:

The Project Manager's settings can be opened using the Settings menu:

From here, you can change the editor's language (default is the system language), interface theme, display scale, network mode, and also the directory naming convention.

To learn the Project Manager's ins and outs, read Using the Project Manager.

When you open a new or an existing project, the editor's interface appears. Let's look at its main areas:

By default, along the window's top edge, it features main menu on the left, workspace switching buttons in the center (active workspace is highlighted), and playtest buttons and the Movie Maker Mode toggle on the right:

Just below the workspace buttons, the opened scenes as tabs are seen. The plus (+) button right next to the tabs will add a new scene to the project. With the button on the far right, distraction-free mode can be toggled, which maximizes or restores the viewport's size by hiding docks in the interface:

In the center, below the scene selector is the viewport with its toolbar at the top, where you'll find different tools to move, scale, or lock the scene's nodes (currently the 3D workspace is active):

This toolbar changes based on the context and selected node. Here is the 2D toolbar:

To learn more on workspaces, read The five main screens.

To learn more on the 3D viewport and 3D in general, read Introduction to 3D.

On either side of the viewport sit the docks. And at the bottom of the window lies the bottom panel.

Let's look at the docks. The FileSystem dock lists your project files, including scripts, images, audio samples, and more:

The Scene dock lists the active scene's nodes:

The Inspector allows you to edit the properties of a selected node:

To read more on inspector, see Inspector Dock.

Docks can be customized. Read more on Moving and resizing docks.

The bottom panel, situated below the viewport, is the host for the debug console, the animation editor, the audio mixer, and more. They can take precious space, that's why they're folded by default:

When you click on one, it expands vertically. Below, you can see the animation editor opened:

Bottom panels can also be shown or hidden using the shortcuts defined in Editor Settings > Shortcuts, under the Bottom Panels category.

There are five main screen buttons centered at the top of the editor: 2D, 3D, Script, Game and Asset Library.

You'll use the 2D screen for all types of games. In addition to 2D games, the 2D screen is where you'll build your interfaces.

In the 3D screen, you can work with meshes, lights, and design levels for 3D games.

Read Introduction to 3D for more detail about the 3D main screen.

The Game screen is where your project will appear when running it from the editor. You can go through your project to test it, and pause it and adjust it in real time. Note that this is for testing how adjustments would work, any changes made here are not saved when the game stops running.

The Script screen is a complete code editor with a debugger, rich auto-completion, and built-in code reference.

Finally, the Asset Library is a library of free and open source add-ons, scripts, and assets to use in your projects.

You can learn more about the asset library in About the Asset Library.

Godot comes with a built-in class reference.

You can search for information about a class, method, property, constant, or signal by any one of the following methods:

Pressing F1 (or Opt + Space on macOS, or Fn + F1 for laptops with a Fn key) anywhere in the editor.

Clicking the "Search Help" button in the top-right of the Script main screen.

Clicking on the Help menu and Search Help.

Ctrl + Click (Cmd + Click on macOS) on a class name, function name, or built-in variable in the script editor.

When you do any of these, a window pops up. Type to search for any item. You can also use it to browse available objects and methods.

Double-click on an item to open the corresponding page in the script main screen.

Clicking while pressing the Ctrl key on a class name, function name, or built-in variable in the script editor.

Right-clicking on nodes and choosing Open Documentation or choosing Lookup Symbol for elements in script editor will directly open their documentation.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Godot's design philosophy — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/introduction/godot_design_philosophy.html

**Contents:**
- Godot's design philosophy
- Object-oriented design and composition
- All-inclusive package
- Open source
- Community-driven
- The Godot editor is a Godot game
- Separate 2D and 3D engines
- User-contributed notes

Now that you've gotten your feet wet, let's talk about Godot's design.

Every game engine is different and fits different needs. Not only do they offer a range of features, but the design of each engine is unique. This leads to different workflows and different ways to form your games' structures. This all stems from their respective design philosophies.

This page is here to help you understand how Godot works, starting with some of its core pillars. It is not a list of available features, nor is it an engine comparison. To know if any engine can be a good fit for your project, you need to try it out for yourself and understand its design and limitations.

Please watch Godot explained in 7 minutes if you're looking for an overview of the engine's features.

Godot embraces object-oriented design at its core with its flexible scene system and Node hierarchy. It tries to stay away from strict programming patterns to offer an intuitive way to structure your game.

For one, Godot lets you compose or aggregate scenes. It's like nested prefabs: you can create a BlinkingLight scene and a BrokenLantern scene that uses the BlinkingLight. Then, create a city filled with BrokenLanterns. Change the BlinkingLight's color, save, and all the BrokenLanterns in the city will update instantly.

On top of that, you can inherit from any scene.

A Godot scene could be a Weapon, a Character, an Item, a Door, a Level, part of a level… anything you'd like. It works like a class in pure code, except you're free to design it by using the editor, using only the code, or mixing and matching the two.

It's different from prefabs you find in several 3D engines, as you can then inherit from and extend those scenes. You may create a Magician that extends your Character. Modify the Character in the editor and the Magician will update as well. It helps you build your projects so that their structure matches the game's design.

Also note that Godot offers many different types of objects called nodes, each with a specific purpose. Nodes are part of a tree and always inherit from their parents up to the Node class. Although the engine does feature some nodes like collision shapes that a parent physics body will use, most nodes work independently from one another.

In other words, Godot's nodes do not work like components in some other game engines.

Sprite2D is a Node2D, a CanvasItem and a Node. It has all the properties and features of its three parent classes, like transforms or the ability to draw custom shapes and render with a custom shader.

Godot tries to provide its own tools to answer most common needs. It has a dedicated scripting workspace, an animation editor, a tilemap editor, a shader editor, a debugger, a profiler, the ability to hot-reload locally and on remote devices, etc.

The goal is to offer a full package to create games and a continuous user experience. You can still work with external programs as long as there is an import plugin available in Godot for it.

That is also partly why Godot offers its own programming language GDScript along with C#. GDScript is designed for the needs of game developers and game designers, and is tightly integrated in the engine and the editor.

GDScript lets you write code using an indentation-based syntax, yet it detects types and offers a static language's quality of auto-completion. It is also optimized for gameplay code with built-in types like Vectors and Colors.

Note that with GDExtension, you can write high-performance code using compiled languages like C, C++, Rust, D, Haxe, or Swift without recompiling the engine.

Note that the 3D workspace doesn't feature as many tools as the 2D workspace. You'll need external programs or add-ons to edit terrains, animate complex characters, and so on. Godot provides a complete API to extend the editor's functionality using game code. See The Godot editor is a Godot game below.

Godot offers a fully open source codebase under the MIT license. This means that the codebase is free for anyone to download, use, modify, or share, as long as its license file is kept intact.

All technologies that ship with Godot, including third-party libraries, must be legally compatible with this open source license. Therefore, most parts of Godot are developed from the ground up by community contributors.

Anyone can plug in proprietary tools for the needs of their projects — they just won't ship with the engine. This may include Google AdMob, or FMOD. Any of these can come as third-party plugins instead.

On the other hand, an open codebase means you can learn from and extend the engine to your heart's content. You can also debug games easily, as Godot will print errors with a stack trace, even if they come from the engine itself.

This does not affect the work you do with Godot in any way: there's no strings attached to the engine or anything you make with it.

Godot is made by its community, for the community, and for all game creators out there. It's the needs of the users and open discussions that drive the core updates. New features from the core developers often focus on what will benefit the most users first.

That said, although a handful of core developers work on it full-time, the project has thousands of contributors at the time of writing. Benevolent programmers work on features they may need themselves, so you'll see improvements in all corners of the engine at the same time in every major release.

The Godot editor runs on the game engine. It uses the engine's own UI system, it can hot-reload code and scenes when you test your projects, or run game code in the editor. This means you can use the same code and scenes for your games, or build plugins and extend the editor.

This leads to a reliable and flexible UI system, as it powers the editor itself. With the @tool annotation, you can run any game code in the editor.

RPG in a Box is a voxel RPG editor made with Godot. It uses Godot's UI tools for its node-based programming system and for the rest of the interface.

Put the @tool annotation at the top of any GDScript file and it will run in the editor. This lets you import and export plugins, create plugins like custom level editors, or create scripts with the same nodes and API you use in your projects.

The editor is fully written in C++ and is statically compiled into the binary. This means you can't import it as a typical project that would have a project.godot file.

Godot offers dedicated 2D and 3D rendering engines. As a result, the base unit for 2D scenes is pixels. Even though the engines are separate, you can render 2D in 3D, 3D in 2D, and overlay 2D sprites and interfaces over your 3D world.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Heads up display — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/first_2d_game/06.heads_up_display.html

**Contents:**
- Heads up display
- ScoreLabel
- Message
- StartButton
- Connecting HUD to Main
- Removing old creeps
- User-contributed notes

The final piece our game needs is a User Interface (UI) to display things like score, a "game over" message, and a restart button.

Create a new scene, click the "Other Node" button and add a CanvasLayer node named HUD. "HUD" stands for "heads-up display", an informational display that appears as an overlay on top of the game view.

The CanvasLayer node lets us draw our UI elements on a layer above the rest of the game, so that the information it displays isn't covered up by any game elements like the player or mobs.

The HUD needs to display the following information:

Score, changed by ScoreTimer.

A message, such as "Game Over" or "Get Ready!"

A "Start" button to begin the game.

The basic node for UI elements is Control. To create our UI, we'll use two types of Control nodes: Label and Button.

Create the following as children of the HUD node:

Label named ScoreLabel.

Button named StartButton.

Timer named MessageTimer.

Click on the ScoreLabel and type a number into the Text field in the Inspector. The default font for Control nodes is small and doesn't scale well. There is a font file included in the game assets called "Xolonium-Regular.ttf". To use this font, do the following:

Under "Theme Overrides > Fonts", choose "Load" and select the "Xolonium-Regular.ttf" file.

The font size is still too small, increase it to 64 under "Theme Overrides > Font Sizes". Once you've done this with the ScoreLabel, repeat the changes for the Message and StartButton nodes.

Anchors: Control nodes have a position and size, but they also have anchors. Anchors define the origin - the reference point for the edges of the node.

Arrange the nodes as shown below. You can drag the nodes to place them manually, or for more precise placement, use "Anchor Presets".

Set the "Horizontal Alignment" and "Vertical Alignment" to Center.

Choose the "Anchor Preset" Center Top.

Add the text Dodge the Creeps!.

Set the "Horizontal Alignment" and "Vertical Alignment" to Center.

Set the "Autowrap Mode" to Word, otherwise the label will stay on one line.

Under "Control - Layout/Transform" set "Size X" to 480 to use the entire width of the screen.

Choose the "Anchor Preset" Center.

Under "Control - Layout/Transform", set "Size X" to 200 and "Size Y" to 100 to add a little bit more padding between the border and text.

Choose the "Anchor Preset" Center Bottom.

Under "Control - Layout/Transform", set "Position Y" to 580.

On the MessageTimer, set the Wait Time to 2 and set the One Shot property to "On".

Now add this script to HUD:

We now want to display a message temporarily, such as "Get Ready", so we add the following code

We also need to process what happens when the player loses. The code below will show "Game Over" for 2 seconds, then return to the title screen and, after a brief pause, show the "Start" button.

When you need to pause for a brief time, an alternative to using a Timer node is to use the SceneTree's create_timer() function. This can be very useful to add delays such as in the above code, where we want to wait some time before showing the "Start" button.

Add the code below to HUD to update the score

Connect the pressed() signal of StartButton and the timeout() signal of MessageTimer to the HUD node, and add the following code to the new functions:

Now that we're done creating the HUD scene, go back to Main. Instance the HUD scene in Main like you did the Player scene. The scene tree should look like this, so make sure you didn't miss anything:

Now we need to connect the HUD functionality to our Main script. This requires a few additions to the Main scene:

In the Node tab, connect the HUD's start_game signal to the new_game() function of the Main node by clicking the "Pick" button in the "Connect a Signal" window and selecting the new_game() method or type "new_game" below "Receiver Method" in the window. Verify that the green connection icon now appears next to func new_game() in the script.

In new_game(), update the score display and show the "Get Ready" message:

In game_over() we need to call the corresponding HUD function:

Finally, add this to _on_score_timer_timeout() to keep the display in sync with the changing score:

Remember to remove the call to new_game() from _ready() if you haven't already, otherwise your game will start automatically.

Now you're ready to play! Click the "Play the Project" button.

If you play until "Game Over" and then start a new game right away, the creeps from the previous game may still be on the screen. It would be better if they all disappeared at the start of a new game. We just need a way to tell all the mobs to remove themselves. We can do this with the "group" feature.

In the Mob scene, select the root node and click the "Node" tab next to the Inspector (the same place where you find the node's signals). Next to "Signals", click "Groups" to open the group overview and the "+" button to open the "Create New Group" dialog.

Name the group mobs and click "ok" to add a new scene group.

Now all mobs will be in the "mobs" group.

We can then add the following line to the new_game() function in Main:

The call_group() function calls the named function on every node in a group - in this case we are telling every mob to delete itself.

The game's mostly done at this point. In the next and last part, we'll polish it a bit by adding a background, looping music, and some keyboard shortcuts.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Introduction to Godot — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/introduction/introduction_to_godot.html

**Contents:**
- Introduction to Godot
- What is Godot?
- What can the engine do?
- How does it work and look?
- Programming languages
- What do I need to know to use Godot?
- User-contributed notes

This article is here to help you figure out whether Godot might be a good fit for you. We will introduce some broad features of the engine to give you a feel for what you can achieve with it and answer questions such as "what do I need to know to get started?".

This is by no means an exhaustive overview. We will introduce many more features in this getting started series.

Godot is a general-purpose 2D and 3D game engine designed to support all sorts of projects. You can use it to create games or applications you can then release on desktop or mobile, as well as on the web.

You can also create console games with it, although you either need strong programming skills or a developer to port the game for you.

The Godot team can't provide an open source console export due to the licensing terms imposed by console manufacturers. Regardless of the engine you use, though, releasing games on consoles is always a lot of work. You can read more on that here: Console support in Godot.

Godot was initially developed in-house by an Argentinian game studio. Its development started in 2001, and the engine was rewritten and improved tremendously since its open source release in 2014.

Some examples of games created with Godot include Cassette Beasts, PVKK, and Usagi Shima. As for applications, the open source pixel art drawing program Pixelorama is powered by Godot, and so is the voxel RPG creator RPG in a Box. You can find many more examples in the Official Showcase.

PVKK: Planetenverteidigungskanonenkommandant

Godot comes with a fully-fledged game editor with integrated tools to answer the most common needs. It includes a code editor, an animation editor, a tilemap editor, a shader editor, a debugger, a profiler, and more.

The team strives to offer a feature-rich game editor with a consistent user experience. While there is always room for improvement, the user interface keeps getting refined.

Of course, if you prefer, you can work with external programs. We officially support importing 3D scenes designed in Blender and maintain plugins to code in VSCode and Emacs for GDScript and C#. We also support Visual Studio for C# on Windows.

Let's talk about the available programming languages.

You can code your games using GDScript, a Godot-specific and tightly integrated language with a lightweight syntax, or C#, which is popular in the games industry. These are the two main scripting languages we support.

With the GDExtension technology, you can also write gameplay or high-performance algorithms in C++ or other languages without recompiling the engine. You can use this technology to integrate third-party libraries and other Software Development Kits (SDK) in the engine.

Of course, you can also directly add modules and features to the engine, as it's completely free and open source.

Godot is a feature-packed game engine. With its thousands of features, there is a lot to learn. To make the most of it, you need good programming foundations. While we try to make the engine accessible, you will benefit a lot from knowing how to think like a programmer first.

Godot relies on the object-oriented programming paradigm. Being comfortable with concepts such as classes and objects will help you code efficiently in it.

If you are entirely new to programming, we recommend following the CS50 open courseware from Harvard University. It's a great free course that will teach you everything you need to know to be off to a good start. It will save you countless hours and hurdles learning any game engine afterward.

In CS50, you will learn multiple programming languages. Don't be afraid of that: programming languages have many similarities. The skills you learn with one language transfer well to others.

We will provide you with more Godot-specific learning resources in Learning new features.

In the next part, you will get an overview of the engine's essential concepts.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Learning new features — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/introduction/learning_new_features.html

**Contents:**
- Learning new features
- Making the most of this manual
- Learning to think like a programmer
- Learning with the community
- Community tutorials
- User-contributed notes

Godot is a feature-rich game engine. There is a lot to learn about it. This page explains how you can use the online manual, built-in code reference, and join online communities to learn new features and techniques.

What you are reading now is the user manual. It documents each of the engine's concepts and available features. When learning a new topic, you can start by browsing the corresponding section of this website. The left menu allows you to explore broad topics while the search bar will help you find more specific pages. If a page exists for a given theme, it will often link to more related content.

The manual has a companion class reference that explains each Godot class's available functions and properties when programming. While the manual covers general features, concepts, and how to use the editor, the reference is all about using Godot's scripting API (Application Programming Interface). You can access it both online and offline. We recommend browsing the reference offline, from within the Godot editor. To do so, go to Help -> Search Help or press F1.

To browse it online, head to the manual's Class Reference section.

A class reference's page tells you:

Where the class exists in the inheritance hierarchy. You can click the top links to jump to parent classes and see the properties and methods a type inherits.

A summary of the class's role and use cases.

An explanation of the class's properties, methods, signals, enums, and constants.

Links to manual pages further detailing the class.

If the manual or class reference is missing or has insufficient information, please open an Issue in the official godot-docs GitHub repository to report it.

You can hold Ctrl (macOS Cmd) and then mouseover text like the name of a class, property, method, signal, or constant to underline it, then Ctrl + Click (macOS Cmd + Click) it to jump to it.

Teaching programming foundations and how to think like a game developer is beyond the scope of Godot's documentation. If you're new to programming, we recommend two excellent free resources to get you started:

Harvard university offers a free courseware to learn to program, CS50. It will teach you programming fundamentals, how code works, and how to think like a programmer. These skills are essential to become a game developer and learn any game engine efficiently. You can see this course as an investment that will save you time and trouble when you learn to create games.

If you prefer books, check out the free ebook Automate The Boring Stuff With Python by Al Sweigart.

Godot has a growing community of users. If you're stuck on a problem or need help to better understand how to achieve something, you can ask other users for help on one of the many active communities.

The best place to ask questions and find already answered ones is the official Godot Forum. These responses show up in search engine results and get saved, allowing other users to benefit from discussions on the platform. Once you have asked a question there, you can share its link on other social platforms. Before asking a question, be sure to look for existing answers that might solve your problem on this website or using your preferred search engine.

Asking questions well and providing details will help others answer you faster and better. When asking questions, we recommend including the following information:

Describe your goal. You want to explain what you are trying to achieve design-wise. If you are having trouble figuring out how to make a solution work, there may be a different, easier solution that accomplishes the same goal.

If there is an error involved, share the exact error message. You can copy the exact error message in the editor's Debugger bottom panel by clicking the Copy Error icon. Knowing what it says can help community members better identify how you triggered the error.

If there is code involved, share a code sample. Other users won't be able to help you fix a problem without seeing your code. Share the code as text directly. To do so, you can copy and paste a short code snippet in a chat box, or use a website like Pastebin to share long files.

Share a screenshot of your Scene dock along with your written code. Most of the code you write affects nodes in your scenes. As a result, you should think of those scenes as part of your source code.

Also, please don't take a picture with your phone, the low quality and screen reflections can make it hard to understand the image. Your operating system should have a built-in tool to take screenshots with the PrtSc (Print Screen) key (macOS: use Cmd + Shift + 3 for a full screen shot, more information here).

Alternatively, you can use a program like ShareX on Windows, or Flameshot on Windows/macOS/Linux.

Sharing a video of your running game can also be really useful to troubleshoot your game. You can use programs like OBS Studio and Screen to GIF to capture your screen.

You can then use a service like streamable or a cloud provider to upload and share your videos for free.

If you're not using the stable version of Godot, please mention the version you're using. The answer can be different as available features and the interface evolve rapidly.

Following these guidelines will maximize your chances of getting the answer you're looking for. They will save time both for you and the persons helping you.

This manual aims to provide a comprehensive reference of Godot's features. Aside from the 2D and 3D getting started series, it does not contain tutorials to implement specific game genres. If you're looking for a tutorial about creating a role-playing game, a platformer, or other, please see Tutorials and resources, which lists content made by the Godot community.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Learn to code with GDScript — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/introduction/learn_to_code_with_gdscript.html

**Contents:**
- Learn to code with GDScript
- Learn in your browser with the GDScript app
- User-contributed notes

In Godot, you can write code using the GDScript and C# programming languages.

If you are new to programming, we recommend starting with GDScript because we designed it to be simpler than all-purpose languages like C#. It will be both faster and easier to learn.

While GDScript is a language specific to Godot, the techniques you will learn with it will apply to other programming languages.

Note that it is completely normal for a programmer to learn and use multiple languages. Programming languages have more similarities than differences, so once you know one, you can learn another much faster.

To learn GDScript, you can use the app Learn GDScript From Zero. It is a complete beginner course with interactive practices you can do right in your browser.

Click here to access the app: Learn GDScript From Zero app

This app is an open-source project. To report bugs or contribute, head to the app's source code repository: GitHub repository.

In the next part, you will get an overview of the engine's essential concepts.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Nodes and Scenes — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/step_by_step/nodes_and_scenes.html

**Contents:**
- Nodes and Scenes
- Nodes
- Scenes
- Creating your first scene
- Changing a node's properties
- Running the scene
- Setting the main scene
- User-contributed notes

In Overview of Godot's key concepts, we saw that a Godot game is a tree of scenes and that each scene is a tree of nodes. In this lesson, we explain a bit more about them. You will also create your first scene.

Nodes are the fundamental building blocks of your game. They are like the ingredients in a recipe. There are dozens of kinds that can display an image, play a sound, represent a camera, and much more.

All nodes have the following characteristics:

They receive callbacks to update every frame.

You can extend them with new properties and functions.

You can add them to another node as a child.

The last characteristic is important. Together, nodes form a tree, which is a powerful feature to organize projects. Since different nodes have different functions, combining them produces more complex behavior. As we saw before, you can build a playable character the camera follows using a CharacterBody2D node, a Sprite2D node, a Camera2D node, and a CollisionShape2D node.

When you organize nodes in a tree, like our character, we call this construct a scene. Once saved, scenes work like new node types in the editor, where you can add them as a child of an existing node. In that case, the instance of the scene appears as a single node with its internals hidden.

Scenes allow you to structure your game's code however you want. You can compose nodes to create custom and complex node types, like a game character that runs and jumps, a life bar, a chest with which you can interact, and more.

The Godot editor essentially is a scene editor. It has plenty of tools for editing 2D and 3D scenes, as well as user interfaces. A Godot project can contain as many of these scenes as you need. The engine only requires one as your application's main scene. This is the scene Godot will first load when you or a player runs the game.

On top of acting like nodes, scenes have the following characteristics:

They always have one root node, like the "Player" in our example.

You can save them to your local drive and load them later.

You can create as many instances of a scene as you'd like. You could have five or ten characters in your game, created from your Character scene.

Let's create our first scene with a single node. To do so, you will need to create a new project first. After opening the project, you should see an empty editor.

In an empty scene, the Scene dock on the left shows several options to add a root node quickly. 2D Scene adds a Node2D node, 3D Scene adds a Node3D node, and User Interface adds a Control node. These presets are here for convenience; they are not mandatory. Other Node lets you select any node to be the root node. In an empty scene, Other Node is equivalent to pressing the Add Child Node button at the top-left of the Scene dock, which usually adds a new node as a child of the currently selected node.

We're going to add a single Label node to our scene. Its function is to draw text on the screen.

Press the Add Child Node button or Other Node to create a root node.

The Create New Node dialog opens, showing the long list of available nodes.

Select the Label node. You can type its name to filter down the list.

Click on the Label node to select it and click the Create button at the bottom of the window.

A lot happens when you add a scene's first node. The scene changes to the 2D workspace because Label is a 2D node type. The Label appears, selected, in the top-left corner of the viewport. The node appears in the Scene dock on the left, and the node's properties appear in the Inspector dock on the right.

The next step is to change the Label's Text property. Let's change it to "Hello World".

Head to the Inspector dock on the right of the viewport. Click inside the field below the Text property and type "Hello World".

You will see the text draw in the viewport as you type.

You can edit any property listed in the Inspector as we did with the Text. For a complete reference of the Inspector dock, see Inspector Dock.

You can move your Label node in the viewport by selecting the move tool in the toolbar.

With the Label selected, click and drag anywhere in the viewport to move it to the center of the view delimited by the rectangle.

Everything's ready to run the scene! Press the Run Current Scene button in the top-right of the screen or press F6 (Cmd + R on macOS).

A popup invites you to save the scene, which is required to run it. Click the Save button in the file browser to save it as label.tscn.

The Save Scene As dialog, like other file dialogs in the editor, only allows you to save files inside the project. The res:// path at the top of the window represents the project's root directory and stands for "resource path". For more information about file paths in Godot, see File system.

The application should open in a new window and display the text "Hello World".

Close the window or press F8 (Cmd + . on macOS) to quit the running scene.

To run our test scene, we used the Run Current Scene button. Another button next to it, Run Project, allows you to set and run the project's main scene. You can also press F5 (Cmd + B on macOS) to do so.

Running the project's main scene is distinct from running the current scene. If you encounter unexpected behavior, check to ensure you are running the correct scene.

A popup window appears and invites you to select the main scene.

Click the Select button, and in the file dialog that appears, double click on label.tscn.

The demo should run again. Moving forward, every time you run the project, Godot will use this scene as a starting point.

The editor saves the main scene's path in a project.godot file in your project's directory. While you can edit this text file directly to change project settings, you can also use the Project > Project Settings window to do so. For more information, see Project Settings.

In the next part, we will discuss another key concept in games and in Godot: creating instances of a scene.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Overview of Godot's key concepts — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/introduction/key_concepts_overview.html

**Contents:**
- Overview of Godot's key concepts
- Scenes
- Nodes
- The scene tree
- Signals
- Summary
- User-contributed notes

Every game engine revolves around abstractions you use to build your applications. In Godot, a game is a tree of nodes that you group together into scenes. You can then wire these nodes so they can communicate using signals.

These are the four concepts you will learn here. We're going to look at them briefly to give you a sense of how the engine works. In the getting started series, you will get to use them in practice.

In Godot, you break down your game in reusable scenes. A scene can be a character, a weapon, a menu in the user interface, a single house, an entire level, or anything you can think of. Godot's scenes are flexible; they fill the role of both prefabs and scenes in some other game engines.

You can also nest scenes. For example, you can put your character in a level, and drag and drop a scene as a child of it.

A scene is composed of one or more nodes. Nodes are your game's smallest building blocks that you arrange into trees. Here's an example of a character's nodes.

It is made of a CharacterBody2D node named "Player", a Camera2D, a Sprite2D, and a CollisionShape2D.

The node names end with "2D" because this is a 2D scene. Their 3D counterparts have names that end with "3D". Be aware that "Spatial" Nodes are now called "Node3D" starting with Godot 4.

Notice how nodes and scenes look the same in the editor. When you save a tree of nodes as a scene, it then shows as a single node, with its internal structure hidden in the editor.

Godot provides an extensive library of base node types you can combine and extend to build more powerful ones. 2D, 3D, or user interface, you will do most things with these nodes.

All your game's scenes come together in the scene tree, literally a tree of scenes. And as scenes are trees of nodes, the scene tree also is a tree of nodes. But it's easier to think of your game in terms of scenes as they can represent characters, weapons, doors, or your user interface.

Nodes emit signals when some event occurs. This feature allows you to make nodes communicate without hard-wiring them in code. It gives you a lot of flexibility in how you structure your scenes.

Signals are Godot's version of the observer pattern. You can read more about it here: https://gameprogrammingpatterns.com/observer.html

For example, buttons emit a signal when pressed. You can connect a piece of code to this signal which will run in reaction to this event, like starting the game or opening a menu.

Other built-in signals can tell you when two objects collided, when a character or monster entered a given area, and much more. You can also define new signals tailored to your game.

Nodes, scenes, the scene tree, and signals are four core concepts in Godot that you will manipulate all the time.

Nodes are your game's smallest building blocks. You combine them to create scenes that you then combine and nest into the scene tree. You can then use signals to make nodes react to events in other nodes or different scene tree branches.

After this short breakdown, you probably have many questions. Bear with us as you will get many answers throughout the getting started series.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Setting up the project — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/first_2d_game/01.project_setup.html

**Contents:**
- Setting up the project
- Organizing the project
- User-contributed notes

In this short first part, we'll set up and organize the project.

Launch Godot and create a new project.

When creating the new project, you only need to choose a valid Project Path. You can leave the other default settings alone.

Download dodge_the_creeps_2d_assets.zip. The archive contains the images and sounds you'll be using to make the game. Extract the archive and move the art/ and fonts/ directories to your project's directory.

Download dodge_the_creeps_2d_assets.zip. The archive contains the images and sounds you'll be using to make the game. Extract the archive and move the art/ and fonts/ directories to your project's directory.

Ensure that you have the required dependencies to use C# in Godot. You need the latest stable .NET SDK, and an editor such as VS Code. See Prerequisites.

The C++ part of this tutorial wasn't rewritten for the new GDExtension system yet.

Your project folder should look like this.

This game is designed for portrait mode, so we need to adjust the size of the game window. Click on Project -> Project Settings to open the project settings window, in the left column open the Display -> Window tab. There, set "Viewport Width" to 480 and "Viewport Height" to 720. You can see the "Project" menu on the upper left corner.

Also, under the Stretch options, set Mode to canvas_items and Aspect to keep. This ensures that the game scales consistently on different sized screens.

In this project, we will make 3 independent scenes: Player, Mob, and HUD, which we will combine into the game's Main scene.

In a larger project, it might be useful to create folders to hold the various scenes and their scripts, but for this relatively small game, you can save your scenes and scripts in the project's root folder, identified by res://. You can see your project folders in the FileSystem dock in the lower left corner:

With the project in place, we're ready to design the player scene in the next lesson.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## The main game scene — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/first_2d_game/05.the_main_game_scene.html

**Contents:**
- The main game scene
- Spawning mobs
- Main script
- Testing the scene
- User-contributed notes

Now it's time to bring everything we did together into a playable game scene.

Create a new scene and add a Node named Main. (The reason we are using Node instead of Node2D is because this node will be a container for handling game logic. It does not require 2D functionality itself.)

Click the Instance button (represented by a chain link icon) and select your saved player.tscn.

Now, add the following nodes as children of Main, and name them as shown:

Timer (named MobTimer) - to control how often mobs spawn

Timer (named ScoreTimer) - to increment the score every second

Timer (named StartTimer) - to give a delay before starting

Marker2D (named StartPosition) - to indicate the player's start position

Set the Wait Time property of each of the Timer nodes as follows (values are in seconds):

In addition, set the One Shot property of StartTimer to "On" and set Position of the StartPosition node to (240, 450).

The Main node will be spawning new mobs, and we want them to appear at a random location on the edge of the screen. Click the Main node in the Scene dock, then add a child Path2D node named MobPath. When you select Path2D, you will see some new buttons at the top of the editor:

Select the middle one ("Add Point") and draw the path by clicking to add the points at the corners shown. To have the points snap to the grid, make sure "Use Grid Snap" and "Use Smart Snap" are both selected. These options can be found to the left of the "Lock" button, appearing as a magnet next to some dots and intersecting lines, respectively.

Draw the path in clockwise order, or your mobs will spawn pointing outwards instead of inwards!

After placing point 4 in the image, click the "Close Curve" button and your curve will be complete.

Now that the path is defined, add a PathFollow2D node as a child of MobPath and name it MobSpawnLocation. This node will automatically rotate and follow the path as it moves, so we can use it to select a random position and direction along the path.

Your scene should look like this:

Add a script to Main. At the top of the script, we use @export var mob_scene: PackedScene to allow us to choose the Mob scene we want to instance.

Click the Main node and you will see the Mob Scene property in the Inspector under "Main.gd".

You can assign this property's value in two ways:

Drag mob.tscn from the "FileSystem" dock and drop it in the Mob Scene property.

Click the down arrow next to "[empty]" and choose "Load". Select mob.tscn.

Next, select the instance of the Player scene under Main node in the Scene dock, and access the Node dock on the sidebar. Make sure to have the Signals tab selected in the Node dock.

You should see a list of the signals for the Player node. Find and double-click the hit signal in the list (or right-click it and select "Connect..."). This will open the signal connection dialog. We want to make a new function named game_over, which will handle what needs to happen when a game ends. Type "game_over" in the "Receiver Method" box at the bottom of the signal connection dialog and click "Connect". You are aiming to have the hit signal emitted from Player and handled in the Main script. Add the following code to the new function, as well as a new_game function that will set everything up for a new game:

Now we'll connect the timeout() signal of each Timer node (StartTimer, ScoreTimer, and MobTimer) to the main script. For each of the three timers, select the timer in the Scene dock, open the Signals tab of the Node dock, then double-click the timeout() signal in the list. This will open a new signal connection dialog. The default settings in this dialog should be fine, so select Connect to create a new signal connection.

Once all three timers have this set up, you should be able to see each timer have a Signal connection for their respective timeout() signal, showing in green, within their respective Signals tabs:

(For MobTimer): _on_mob_timer_timeout()

(For ScoreTimer): _on_score_timer_timeout()

(For StartTimer): _on_start_timer_timeout()

Now we define how each of these timers operate by adding the code below. Notice that StartTimer will start the other two timers, and that ScoreTimer will increment the score by 1.

In _on_mob_timer_timeout(), we will create a mob instance, pick a random starting location along the Path2D, and set the mob in motion. The PathFollow2D node will automatically rotate as it follows the path, so we will use that to select the mob's direction as well as its position. When we spawn a mob, we'll pick a random value between 150.0 and 250.0 for how fast each mob will move (it would be boring if they were all moving at the same speed).

Note that a new instance must be added to the scene using add_child().

Why PI? In functions requiring angles, Godot uses radians, not degrees. Pi represents a half turn in radians, about 3.1415 (there is also TAU which is equal to 2 * PI). If you're more comfortable working with degrees, you'll need to use the deg_to_rad() and rad_to_deg() functions to convert between the two.

Let's test the scene to make sure everything is working. Add this new_game call to _ready():

Let's also assign Main as our "Main Scene" - the one that runs automatically when the game launches. Press the "Play" button and select main.tscn when prompted.

If you had already set another scene as the "Main Scene", you can right click main.tscn in the FileSystem dock and select "Set As Main Scene".

You should be able to move the player around, see mobs spawning, and see the player disappear when hit by a mob.

When you're sure everything is working, remove the call to new_game() from _ready() and replace it with pass.

What's our game lacking? Some user interface. In the next lesson, we'll add a title screen and display the player's score.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Using signals — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/getting_started/step_by_step/signals.html

**Contents:**
- Using signals
- Scene setup
- Connecting a signal in the editor
- Connecting a signal via code
- Complete script
- Custom signals
- Summary
- User-contributed notes

In this lesson, we will look at signals. They are messages that nodes emit when something specific happens to them, like a button being pressed. Other nodes can connect to that signal and call a function when the event occurs.

Signals are a delegation mechanism built into Godot that allows one game object to react to a change in another without them referencing one another. Using signals limits coupling and keeps your code flexible.

For example, you might have a life bar on the screen that represents the player's health. When the player takes damage or uses a healing potion, you want the bar to reflect the change. To do so, in Godot, you would use signals.

Like methods (Callable), signals are a first-class type since Godot 4.0. This means you can pass them around as method arguments directly without having to pass them as strings, which allows for better autocompletion and is less error-prone. See the Signal class reference for a list of what you can do with the Signal type directly.

As mentioned in the introduction, signals are Godot's version of the observer pattern. You can learn more about it in Game Programming Patterns.

We will now use a signal to make our Godot icon from the previous lesson (Listening to player input) move and stop by pressing a button.

For this project, we will be following the Godot naming conventions.

GDScript: Classes (nodes) use PascalCase, variables and functions use snake_case, and constants use ALL_CAPS (See GDScript style guide).

C#: Classes, export variables and methods use PascalCase, private fields use _camelCase, local variables and parameters use camelCase (See C# style guide). Be careful to type the method names precisely when connecting signals.

To add a button to our game, we will create a new scene which will include both a Button and the sprite_2d.tscn scene we created in the Creating your first script lesson.

Create a new scene by going to the menu Scene > New Scene.

In the Scene dock, click the 2D Scene button. This will add a Node2D as our root.

In the FileSystem dock, click and drag the sprite_2d.tscn file you saved previously onto the Node2D to instantiate it.

We want to add another node as a sibling of the Sprite2D. To do so, right-click on Node2D and select Add Child Node.

Search for the Button node and add it.

The node is small by default. Click and drag on the bottom-right handle of the Button in the viewport to resize it.

If you don't see the handles, ensure the select tool is active in the toolbar.

Click and drag on the button itself to move it closer to the sprite.

You can also write a label on the Button by editing its Text property in the Inspector. Enter Toggle motion.

Your scene tree and viewport should look like this.

Save your newly created scene as node_2d.tscn, if you haven't already. You can then run it with F6 (Cmd + R on macOS). At the moment, the button will be visible, but nothing will happen if you press it.

Here, we want to connect the Button's "pressed" signal to our Sprite2D, and we want to call a new function that will toggle its motion on and off. We need to have a script attached to the Sprite2D node, which we do from the previous lesson.

You can connect signals in the Node dock. Select the Button node and, on the right side of the editor, click on the tab named Node next to the Inspector.

The dock displays a list of signals available on the selected node.

Double-click the "pressed" signal to open the node connection window.

There, you can connect the signal to the Sprite2D node. The node needs a receiver method, a function that Godot will call when the Button emits the signal. The editor generates one for you. By convention, we name these callback methods "_on_node_name_signal_name". Here, it'll be "_on_button_pressed".

When connecting signals via the editor's Node dock, you can use two modes. The simple one only allows you to connect to nodes that have a script attached to them and creates a new callback function on them.

The advanced view lets you connect to any node and any built-in function, add arguments to the callback, and set options. You can toggle the mode in the window's bottom-right by clicking the Advanced button.

If you are using an external editor (such as VS Code), this automatic code generation might not work. In this case, you need to connect the signal via code as explained in the next section.

Click the Connect button to complete the signal connection and jump to the Script workspace. You should see the new method with a connection icon in the left margin.

If you click the icon, a window pops up and displays information about the connection. This feature is only available when connecting nodes in the editor.

Let's replace the line with the pass keyword with code that'll toggle the node's motion.

Our Sprite2D moves thanks to code in the _process() function. Godot provides a method to toggle processing on and off: Node.set_process(). Another method of the Node class, is_processing(), returns true if idle processing is active. We can use the not keyword to invert the value.

This function will toggle processing and, in turn, the icon's motion on and off upon pressing the button.

Before trying the game, we need to simplify our _process() function to move the node automatically and not wait for user input. Replace it with the following code, which we saw two lessons ago:

Your complete sprite_2d.gd code should look like the following.

Run the current scene by pressing F6 (Cmd + R on macOS), and click the button to see the sprite start and stop.

You can connect signals via code instead of using the editor. This is necessary when you create nodes or instantiate scenes inside of a script.

Let's use a different node here. Godot has a Timer node that's useful to implement skill cooldown times, weapon reloading, and more.

Head back to the 2D workspace. You can either click the "2D" text at the top of the window or press Ctrl + F1 (Ctrl + Cmd + 1 on macOS).

In the Scene dock, right-click on the Sprite2D node and add a new child node. Search for Timer and add the corresponding node. Your scene should now look like this.

With the Timer node selected, go to the Inspector and enable the Autostart property.

Click the script icon next to Sprite2D to jump back to the scripting workspace.

We need to do two operations to connect the nodes via code:

Get a reference to the Timer from the Sprite2D.

Call the connect() method on the Timer's "timeout" signal.

To connect to a signal via code, you need to call the connect() method of the signal you want to listen to. In this case, we want to listen to the Timer's "timeout" signal.

We want to connect the signal when the scene is instantiated, and we can do that using the Node._ready() built-in function, which is called automatically by the engine when a node is fully instantiated.

To get a reference to a node relative to the current one, we use the method Node.get_node(). We can store the reference in a variable.

The function get_node() looks at the Sprite2D's children and gets nodes by their name. For example, if you renamed the Timer node to "BlinkingTimer" in the editor, you would have to change the call to get_node("BlinkingTimer").

We can now connect the Timer to the Sprite2D in the _ready() function.

The line reads like so: we connect the Timer's "timeout" signal to the node to which the script is attached. When the Timer emits timeout, we want to call the function _on_timer_timeout(), that we need to define. Let's add it at the bottom of our script and use it to toggle our sprite's visibility.

By convention, we name these callback methods in GDScript as "_on_node_name_signal_name" and in C# as "OnNodeNameSignalName". Here, it'll be "_on_timer_timeout" for GDScript and OnTimerTimeout() for C#.

The visible property is a boolean that controls the visibility of our node. The line visible = not visible toggles the value. If visible is true, it becomes false, and vice-versa.

If you run the Node2D scene now, you will see that the sprite blinks on and off, at one second intervals.

That's it for our little moving and blinking Godot icon demo! Here is the complete sprite_2d.gd file for reference.

This section is a reference on how to define and use your own signals, and does not build upon the project created in previous lessons.

You can define custom signals in a script. Say, for example, that you want to show a game over screen when the player's health reaches zero. To do so, you could define a signal named "died" or "health_depleted" when their health reaches 0.

As signals represent events that just occurred, we generally use an action verb in the past tense in their names.

Your signals work the same way as built-in ones: they appear in the Node tab and you can connect to them like any other.

To emit a signal in your scripts, call emit() on the signal.

A signal can optionally declare one or more arguments. Specify the argument names between parentheses:

The signal arguments show up in the editor's node dock, and Godot can use them to generate callback functions for you. However, you can still emit any number of arguments when you emit signals. So it's up to you to emit the correct values.

To emit values along with the signal, add them as extra arguments to the emit() function:

Any node in Godot emits signals when something specific happens to them, like a button being pressed. Other nodes can connect to individual signals and react to selected events.

Signals have many uses. With them, you can react to a node entering or exiting the game world, to a collision, to a character entering or leaving an area, to an element of the interface changing size, and much more.

For example, an Area2D representing a coin emits a body_entered signal whenever the player's physics body enters its collision shape, allowing you to know when the player collected it.

In the next section, Your first 2D game, you'll create a complete 2D game and put everything you learned so far into practice.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---
