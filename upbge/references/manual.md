# Upbge - Manual

**Pages:** 470

---

## 1. Camera Movement

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_nodes/2d_side_scroller/camera_movement.html

**Contents:**
- 1. Camera Movement

In 2d scroller games, camera is usually showing player from the side, and it moves perpendicularly together with the player. If you press Numpad 0 (zero - camera perspective), or Numpad 3, you should see player from same perspective (press Numpad , (comma) to focus the player).

Add a new logic tree, name it ‘player_2d_camera’, and set ‘Fake User’.

Next add, from left to right, Get World Position, set ‘player’ as Object - it will get player’s position, so camera knows where to go, following the player.

Add Separate XYZ vector node, to separate 3D vector into separate XYZ coordinates from ‘World Position’; connect the sockets.

Under above node, add 2 Float nodes - one will set camera distance from player, the other will set following speed. Select both ‘Float’ nodes, hit Ctrl-J - this will group both nodes into a frame, for better organization. Rename top node to ‘camera distance’, and set value to i.e. 30.0; rename bottom one to ‘slow camera’, set value to i.e. 0.15 (with node selected - side N-panel > Node > Label). Also, with frame selected, rename it i.e. into ‘camera custom’, and also change frame color (below ‘Label’).

Next add Math node, set operation to Add, connect X coordinate from Separate XYZ into A socket, and Float output socket from camera distance into B socket. This will get player’s X position (horizontal) and set camera’s X position accordingly.

Add another Math node under the first one, connect Z coordinate from Separate XYZ into A socket, and set B value to 1.0.

Add Combine XYZ node, connect top Math node into X, bottom Math node into Z, and Y socket from Separate XYZ directly into Y socket.

Above first Math node, add Active Camera, next another Get World Position above Combine XYZ, and connect Camera as Object.

Next add Vector Math node, set ‘Operation’ to Add, connect Get World Position into top Vector 1 socket, Combine XYZ into Vector 2 socket.

Next add another Vector Math, set ‘Operation’ to Scale, connect previous node into Vector 1, and slow follow into Scale.

Add On Update above last node, next Set World Position node; connect On Update into Condition socket, Active Camera as Object, and last Vector Math into Value socket.

With ‘player’ selected, Apply To Selected.

2D player camera nodes setup

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## 2D Side Scroller

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_nodes/2d_side_scroller/index.html

**Contents:**
- 2D Side Scroller

In this tutorial we will:

Open .blend file with level;

Fix and clean the file, to reflect our inner ‘zen’ state;

Add logic nodes game logic;

Update and upgrade efficient UPBGE workflow on-the-go.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## 2. Player Movement

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_nodes/2d_side_scroller/player_movement.html

**Contents:**
- 2. Player Movement

From the game logic perspective, player can do few movements:

It can walk/run, either to the left, or to the right, relative to the screen space.

It can fall off the rock into the void.

For this reason, we need to know what state/movement a player is in. We need properties to keep those states updated while the game is running.

With player selected, first add Properties > Game > Game Properties > Add Game Property, name it running, leave default type Float, and also default value 0.0. Save often.

In Logic Node Editor, add new node tree, name it player_2d_movement, and set ‘Fake User’.

Next add Get Object Property, Object > player, and Property > running.

Connect above node Property Value socket into Math > A socket, set B to 0.20, set Operation > Multiply.

Connect Math Result > Combine XYZ Y socket, leave X and Z at default value (0.0).

Below Combine XYZ node add Get Attribute - World Position, and Object > player.

Next add Vector Math, connect Combine XYZ Vector > Vector 1, World Position > Vector 2, Operation > Add.

Above Vector Math add On Update, next Rotate To, connect Out > Condition (red to red socket), and Result > Target (blue to blue socket).

Next add Walk, and above it Set Attribute - World Position; Rotate To Done > Condition - both nodes, Combine XYZ Vector > Walk Vector, uncheck Set World Position Y and Z, both nodes Object > player, also uncheck Walk Local.

For organizing purpose, select all > Ctrl-J to put all into a frame, with frame still selected > N-panel > Node > Node > Label > Change player rotation based on 'running' property.

Player movement setup - rotation part

Next we add collision detection - if player falls into the void, when it collides with Bedrock object, it will be ‘teleported’ back to the beginning. This is the sole purpose of Bedrock object.

First we need to add a property to Bedrock object > select it in Outliner, then Add Game Property, same as we did above for the player; name it bedrock, leave the rest as default.

In Logic Node Editor, under Player movement frame, add Collision, and Set Attribute - World Position - it makes sense, doesn’t it, because when player will fall into the void, and touch (collide) with the Bedrock, we will reset its position, otherwise player would keep falling deeper and deeper into the void - forever.

Set Collision Property > bedrock, check Continuous, connect On Collision output to Set World Position > Condition, and last node Object > player.

Done. Simple as that.

Reset player position nodes setup

In case you need to ‘teleport’ player somewhere else than at the beginning, change Set World Position Value fields (from top to bottom - X, Y, Z). This is used in case when player manages to advance to some ‘checkpoint’ inside the level, but it fails to make it to the end - it is ‘teleported’ to last ‘checkpoint’.

If you run the game, not much will happen - the game is not yet functional. We need to add more functionality to the player. And Apply To Selected all logic trees to player, of course.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## 3D Basic Concepts

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/getting_started/3D_basic_concepts.html

**Contents:**
- 3D Basic Concepts
- 3D Basics
  - Coordinate System
  - Points, Edges, Triangles, and Meshes
  - Basic Transforms
  - Materials and Textures
  - Lights
  - Camera
  - Animation

If you haven’t used any 3D application before, the terms modeling, animation, and rendering might be foreign to you. So before you go off to create the spectacular game that you always wanted to make, let’s have a quick refresher on the basics of computer graphics. You don’t have to endure the boring section below if you are already know what RGB stands for and the difference between Cartesian and Gaussian.

The knowledge in this section is universal and applies to all other 3D applications. So even if you are coming from a different application, the same concepts drive all of them.

We live in a three-dimensional world that has width, height, and depth. So to represent anything that resembles real life as a virtual world inside a computer, we need to think and work in three dimensions. The most common system used is called the Cartesian coordinate system, where the three dimensions are represented by X, Y, and Z, laid out as intersecting planes. Where the three axes meet is called the origin. You can think of the origin as the center of your digital universe. A single position in space is represented by a set of numbers that corresponds to its position from the origin: thus (2, -4, 8) is a point in space that is 2 units from the origin along the X axis, 4 units from the origin along the -Y axis, and 8 units up in the Z direction.

Although we can define a position in space using the XYZ coordinates, a single point (or a vertex, as it’s more commonly known in computer graphics) is not terribly useful; after all, you can’t see a dot that is infinitesimally small. But you can join this vertex with another vertex to form a line (also known as an edge). An edge by itself still wouldn’t be very visible, so you create another vertex and join all three vertices together with lines and fill in the middle. Suddenly, something far more interesting is created - a triangle (also known as a face)! By linking multiple faces together, you can create any shape, the result of which is called a mesh or model. Figure below shows how a mesh can be broken down into faces, then edges, and ultimately, into vertices.

Teapot, cube, face, edge and vertex

Why is the triangle so important? Turns out, modern computer graphics use the triangle as the basic building block for almost any shape. A rectangular plane (also known as a quadrangle, or more commonly a quad) is simply two triangles arranged side by side. A cube is simply six squares put together. Even a sphere is just made of tiny facelets arranged into a ball shape.

The cylinder cap can be made up of triangles, quads, or a n-gon

In Blender, a mesh can be made from a combination of triangles, quads, or n-gons. The benefit of n-gons is their ability to retain a clean topology while modeling. Without n-gons, certain areas of a model (such as a window on a wall) would require a higher number of triangles or quads to approximate, as shown below. While n-gons make modeling easier in some cases, Blender still converts them to triangles when you start the game.

The process of creating a mesh by rearranging vertices, edges, and faces is called modeling. Blender has many tools that help artists define the geometry they want.

It is worth noting that unlike the real world, polygonal models do not have volumes. They are just a shell made of interconnected faces that take the shape of the object, but the inside of the object is always “hollow.”

Surface normals are displayed as cyan lines protruding from the faces

Another concept that a modeler will likely encounter is surface normals, or “normals” for short. Normal is a property of each face that indicates the direction a polygon is facing. Because normals are used for shading computation of the surface, ideally all the normals for a mesh should be pointed “outward”. Wrongly oriented normals can cause the mesh to show up as black or invisible. Fortunately, there is a Make Normals Consistent function in Blender that can usually resolve the issue. Figure above shows how normals are presented in Blender.

Technically, there are other approaches to computer graphics that do not rely on triangles or polygons, such as NURBS (Non-uniform rational B-spline) and voxel (short for VOlumetric piXEL). But polygon modeling and rendering is by far the most common, and it is the only supported method in the game engine.

The three basic transforms that you should be familiar with are:

Translation: The moving of an object in any direction, without rotating it.

Scaling: The resizing of an object around a point.

Rotation: The rotating of an object around a point.

These three are the most common manipulations you will encounter. They are illustrated below.

Translation, scaling, and rotation

Using polygons, you can define the shape of a mesh. To alter the color and appearance of it, you need to apply materials to the object. Material controls the color, shininess, bumpiness, and even transparency of the object. These variables ultimately all serve to add details to the object.

Often, changing the color is not enough to make a surface look realistic. This is where textures come in. Texturing is a common technique used to add color and detail to a mesh by wrapping the mesh with an image, like a decal. Imagine a toy globe: if you carefully peel off the paper map that is glued onto the plastic ball and lay it out flat on the table, that map would be the texture, and the plastic ball would be the mesh. The projection of the 2D image onto a 3D mesh is called texture mapping. Texture mapping can be an automatic process, using one of the predefined projections, or a manual process, which uses a UV layout to map the 2D image onto the 3D mesh. Figure below illustrates how an image is mapped onto a model.

Meshes with texture applied

Traditionally, a texture changes the color of a surface. But that’s not all it can do: textures can also be used to alter other properties of the surface such as its transparency, reflectivity, and even bumpiness to create the illusion of a much more detailed surface.

Diffuse map, normal map, and specular map

A diffuse map controls the base color of the surface. A normal map controls the surface normal of an object, creating a bumpy effect by changing the way the light is reflected off the object. A specular map controls the specular reflection of an object, making it look shiny in certain places and dull in others. A texture map can also have transparent pixels, rendering part of the object transparent.

Generally, textures are image files. But there are also other ways to texture a surface, such as using a procedural texture. Procedural texture differs from an image in that it’s generated by an algorithm in real time, rather than from a pre-made image file.

Everything you see is the result of light hitting your eyes-without lights, the world would be pitch black. Likewise, light is just as important in a virtual world. With light comes shadow as well. Shadow might not be something that you think about every day, but the interplay of shadow and light makes a huge difference in how the scene is presented.

Point, Sun, Spot and Area light

In most 3D applications, there are several different types of light available to the artist; each type has its advantages and disadvantages. For example, a spot lamp approximates a lamp with a conical influence; a sun lamp approximates a light source from infinitely far away. Lamps in Blender are treated like regular objects: they can be positioned and rotated just like any other object. Figure above shows how different lamps look in Blender.

Think of lighting as more than something that makes your scene visible. Good lighting can enhance the purpose of the scene by highlighting details while hiding irrelevant areas in shadow. Skillful placement of lighting also adds drama and realism to the scene, making an otherwise boring scene look visually exciting.

When you are creating a 3D scene, you are looking at the virtual world from an omniscient view. In this mode, you can view and edit the world from any angle just like a movie director walking around a set in order to adjust things. Once the game starts, the player must view the game through a predetermined camera. Note that a predetermined camera does not mean the camera is fixed; almost all games have a camera that reacts to a player’s input. In an action game, the camera tends to follow the character from behind; in a strategy game, the camera might be hovering high above, looking down; in a platformer, the camera is usually looking at the scene from the side.

A camera is also treated as a regular object in Blender, so you can manipulate its location and orientation just as you can with any other object.

Drawing and Composition for Visual Storytellers

Speaking of lights and cameras, this is the part where we point out the wonderful book by Marcos Mateu-Mestre called Framed Ink. The book uses tons of beautiful drawings to illustrate the many key principles in visual storytelling.

In this context, animation refers to the technique of making things change over time. For example, animation can involve moving an object, deforming it, or changing its color. To set up an animation, you create “keyframes,” which are snapshots in time that store specific values pertaining to the animation. The software can then automatically interpolate in between those values to create a smooth transition. The image below shows Blender’s Dopesheet Editor. The Dopesheet allows you to see the various properties that change during an animation: the horizontal axis represents time; the vertical axis shows the various properties, such as location or rotation that are keyframed.

Dopesheet Editor keyframes

The easiest way to animate is to alter the location, rotation, and scaling of an object over time. For example, by altering these variables, you can realistically animate the movement of a bouncing ball. Keep in mind that the curves represent the value of the channels (in this case xyz location) of the ball, not the actual motion path of the ball itself.

Bouncing ball animation

To animate something more complicated, such as a human, it’s not enough to just move, rotate, and scale the object as a whole. This is where armatures come in. Armatures are skeletons that can be “inserted” into a model to control the model’s deformation. Using this system, you can create complex yet organic-looking animations.

A third way to animate is using shape keys. Shape keys are snapshots of the mesh in different shapes. They are often used to animate nuanced changes that cannot be otherwise easily animated with armatures.

Shape keys animation

Finally, keep in mind that making objects move doesn’t always have to be a manual process. You can also make objects move by using the physics engine.

Procedural physics-based motion

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## 3. Player Properties

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_nodes/2d_side_scroller/player_properties.html

**Contents:**
- 3. Player Properties

Previously we added a single property to the player - running. In this chapter we will add some more properties, and use them with the game logic.

First, let’s add game properties to player.

Add Game Property > grounded > Float > 0.0 (default values), falling > Timer > 0.0, jumped > Boolean > unchecked, landed > Boolean > unchecked, start_falling > Boolean > unchecked.

Added player game properties

Next we add new logic tree, name it player_2d_properties. Be kindly informed, this logic tree is a bit larger than previous ones. Did you remember to set ‘Fake User’?

It is recommended to switch to ‘fullscreen area/window’ mode - mouse over Logic Node Editor > Ctrl-Space (toggle fullscreen).

First we add Float, set its value Float > 0.1. If player is on the ground, this value will be used.

Below it add Get Physics Info, Object > player. This node will provide physics data for player.

Next add Value Switch, connect Float to top Type/Value input (second input socket from top), set bottom Type/Value to Float > 0.03, and Get Physics Info On Ground > A if True, else B (top conditional input).

Player properties - first chunk of nodes

Approximately four node heights higher, we will start second nodes chunk. From now on, unless indicated otherwise, all Object fields should be set to player, and this will not be indicated for each node explicitly. Also previous node will be not named, just its output, for a sake of simplicity, except in case of ambiguity. If unclear, refer to relevant image, usually below the text.

Add Get Object Property, Property > start_falling.

Add On Value Changed To, Property Value > Value, Bool checked.

Add Set Object Property, Result > Condition, Property > falling, Float > 0.0.

This is one row. Below it add another row.

On Value Changed To, Bool checked > Value of On Value Changed, If Changed > Condition of Set Object Property, Property > landed, New > bottom most input socket.

Copy last row one row below.

On Value Changed To Bool uncheck, Set Object Property Property > start_falling.

Get Object Property Property > Grounded, below it add Value Switch, bottom field Float > 0.0, next one above Float > 1.0, connect On Ground > A if True, else B.

Add Interpolate, Property Value > From, Result > To, Factor > 0.3.

Above Interpolate add On Update, Out > Condition of Set Object Property, Property > Grounded.

Also connect On Ground > On take off & When landed (left-most, see image below) Value sockets. Use Reroute utility, if you desire so.

Using Reroute utility

Shift-RMB over existing noodle, and you get Reroute socket for free. LMB the noodle from it just the same as you would from output socket, drag it to input socket. To move it around - LMB-select it, G to grab, move with mouse, LMB to ‘land it’ wherever you wish. Shift-Tab to toggle grid snapping.

Second chunk of nodes

One but last chunk. This one is for player walking. Same as before - from left to right, below existing noodle soup, sorry, group.

Add 2 x Keyboard Key, one below the other, A for left, D for right movement.

Gate, Gate Type > Or, connect the red dots.

Below it, add Value Switch, bottom field Float > 1.0, field above Float > -1.0, If Pressed A > A if True, else B.

Add/duplicate Value Switch, Gate Result > A if True, else B, Result > next (middle) socket, bottom socket Float > 0.0.

Above last node add Get Object Property, Property > running.

Next Interpolate, Property Value > From, Result > To, first Value Switch` > Factor.

At the end, Set Object Property, from above On Update > Condition, Property > running, Value > bottom input socket.

One-but-last chunk of nodes

Ignore left yellow arrow in above image, this connection is not from On Ground.

And the last chunk, this one for jumping.

Keyboard Key, Space for jumping.

Gate, above Get Physics Info On Ground > Condition A, If Pressed > Condition B.

Jump, Result > Condition.

On Value Changed, Done > Value.

Yes, last one, Set Object Property, If Changed > Condition, New > bottom-most input socket.

Yes, finally, we are done with this logic tree.

Next we add player animations, so it will look like it is walking.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## 4. Player Animations

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_nodes/2d_side_scroller/player_animations.html

**Contents:**
- 4. Player Animations

In this chapter we add animations of player body, so it looks alive.

Animations are pre-made for you, as part of initial .blend file.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## About the UPBGE Manual

**URL:** https://upbge.org/docs/latest/manual/manual/contribute/about.html

**Contents:**
- About the UPBGE Manual
- Conventions
  - Keyboard
  - Mouse

The purpose is to provide a complete and concise reference manual, with:

Insight into Blender/UPBGE’s way of working, its internal (technical) design, in order to understand options and tools;

Detailed functional description of all features, tools and options in UPBGE.

These conventions are for people reading the manual. We have a more detailed list of conventions for authors under the Writing Style section.

Hotkey letters are shown in this manual like they appear on a keyboard; for example:

G refers to the lowercase g.

Shift, Ctrl, Alt are specified as modifier keys.

Ctrl-W, Shift-Alt-A indicates that these keys should be pressed simultaneously.

Numpad0 to Numpad9, NumpadPlus refer to the keys on the separate numeric keypad.

Other keys are referred to by their names, such as Esc, Tab, F1 to F12. Of special note are the arrow keys, Left, Right and so on.

This manual refers to mouse buttons as:

LMB - Left Mouse Button;

RMB - Right Mouse Button;

MMB - Middle Mouse Button;

Wheel - Scrolling the Mouse Wheel.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Absolute

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/absolute.html

**Contents:**
- Absolute
- Inputs
- Outputs

A value to perform absolute operation on.

Resulting absolute value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Absolute Vector

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/vectors/absolute_vector.html

**Contents:**
- Absolute Vector
- Inputs
- Outputs

Resulting absolute vector values.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Accelerate

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/vehicle/accelerate.html

**Contents:**
- Accelerate
- Parameters
- Inputs
- Outputs

Selected axis of vehicle wheels.

If connected, condition must be fulfilled for node to activate.

Vehicle object to use.

Number of wheels for selected axis.

Applied power to selected axis.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Active Camera

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/camera/active_camera.html

**Contents:**
- Active Camera
- Outputs

Current active camera in the scene.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Actuators

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/actuators/index.html

**Contents:**
- Actuators
- Actuators Types

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Actuator Editing

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/actuators/editing.html

**Contents:**
- Actuator Editing
- Column Heading
- Actuators
- Object Heading

Actuator Column with a typical actuator

UPBGE actuators can be set up and edited in the right-hand column of the Logic Panel. This page describes the general column controls, and also those parameters which are common to all individual actuator types.

The image shows a typical actuator column with a single example actuator. At the top of this column, the column heading includes menus and buttons to control which of all the actuators in the current Game Logic are displayed.

Actuator Column heading

The column headings contain controls to set which actuators are displayed, and the level of detail given, in the actuator column. This is very useful for hiding unnecessary actuators, so that the necessary ones are visible and easier to reach. Both these can be controlled individually.

Collapses all objects to just a bar with their name.

Expands all actuators.

Collapses all actuators to bars with their names.

It is also possible to filter which actuators are viewed using the four heading buttons:

Shows all actuators for selected objects.

Shows only actuators belonging to the active object.

Shows actuators which have a link to a controller.

Only actuators connected to a controller with active states are shown.

Actuator Object heading

In the column list, actuators are grouped by object. By default, actuators for every selected object appear in the list, but this may be modified by the column heading filters.

At the head of each displayed object sensor list, two entries appear:

The name of the object.

When clicked, a menu appears with the available actuator types. Selecting an entry adds a new actuator to the object. See Actuators for list of available actuator types.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Actuator Sensor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/types/actuator.html

**Contents:**
- Actuator Sensor
- Properties
- Example

See the Python reference of this logic brick in SCA_ActuatorSensor.

The Actuator Sensor detects when a particular actuator receives an activation pulse. It sends a TRUE pulse when the specified actuator is activated. The sensor also sends a FALSE pulse when the specified actuator is deactivated.

See Sensor Common Options for common options.

The actuator referenced must be owned by the same object.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Additional Details

**URL:** https://upbge.org/docs/latest/manual/manual/editors/logic_nodes/editor_details.html

**Contents:**
- Additional Details
- N-panel Tabs
- RMB Context
- Socket Type by Colors

After new logic tree is added, N-panel includes:

Group - add a group socket or a panel;

Node - set node name in Label field, change color, and see Properties;

Tool - active tool for i.e. selection;

View - manage Annotations;

Dashboard - main access point to Logic Node Editor functionality - apply logic tree to node, use a tree template, see properties;

Custom Nodes - add user created custom nodes;

Help & Documentation - update Uplogic module, access UPBGE manual and API.

With mouse inside Logic Node Editor, RMB context has two versions:

No node selected - add, paste, find node, cut and mute links; for a fast workflow, use the hotkeys.

RMB context with no node selected

Node selected - copy, paste etc. Use the hotkeys, if you dare.

RMB context with node selected

Put some Logic Nodes into the editor (any will do for testing), connect them, and:

LMB-select them > Shift-J to put them all into a frame; keep Frame selected > Node tab > add text into Label field > Enter.

Ctrl-RMB-drag over a noodle (aka link) to delete it/cut the link.

Also useful for learning/testing/debugging are M > mute nodes, and for final packed design Ctrl-H > hide unused sockets, or even H > collapse the nodes.

Test other hotkeys as per figures above.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Add Constraint

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/add_constraint.html

**Contents:**
- Add Constraint
- Parameters
- Inputs
- Outputs

This node will create a new physics constraint on the selected object.

Selected constraint type to add.

If connected, condition must be fulfilled for node to activate.

Which object to apply the constraint to.

Which object to use as target for the constraint (may not be the same as Object socket).

Unique name for this constraint for later access.

Calculate the pivot in world space instead of local.

Pivot for physics calculations.

If enabled, object will collide with target.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Add Filter

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/post_fx/add_filter.html

**Contents:**
- Add Filter
- Parameters
- Inputs
- Outputs

This node will add a new GL filter, modifying the render output.

Available filters are: - FXAA - HBAO - SSAO - Vignette - Brightness - Chromatic Abberation - Grayscale - Levels - Mist - Blur

If connected, condition must be fulfilled for node to activate.

Higher indices will affect the rendered image by lower indices.

Strength of the effect.

Color of the added filter (if applicable).

Brightness of the selected filter (if applicable).

Starting distance of the mist. For Mist filter only.

Density of the mist. For Mist filter only.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Add Logic Tree To Object

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/trees/add_logic_tree_to_object.html

**Contents:**
- Add Logic Tree To Object
- Inputs
- Outputs

Add a new logic tree to an object to be executed.

If connected, condition from attached node must be fulfilled for node to activate.

Which object to add Logic Tree to.

Which Node Tree to add.

Set this tree to active when added.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Add Object

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/add_object.html

**Contents:**
- Add Object
- Inputs
- Outputs

Add a copy of an object into the current scene.

Which condition will be used for node to activate.

Object Data Block to add into the scene.

Copy the transform data from this object (optional).

Total amount of frames after which the object is removed.

Duplicate the data used by the spawned object. This will duplicate any material, action etc. used by this Data Block.

True if the node performed successfully, else False.

Spawned instance of the object.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Add Widget

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/add_widget.html

**Contents:**
- Add Widget
- Inputs
- Outputs

Add one widget to another. Child widgets will inherit positioning and rotation from their parent and can be placed locally. They will also only be visible if their parent is also visible.

If connected, condition must be fulfilled for node to activate.

Parent to which to add the widget.

Widget to add to the parent.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Align Axis to Vector

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/align_axis_to_vector.html

**Contents:**
- Align Axis to Vector
- Properties
- Input
- Output

Direction of the object will be the same direction that the vector has, in relation to the World Origin.

If vector is in a certain position relative to World Origin, object will receive the same angulation in this relation: World Origin to Object.

The condition for this node to start.

Object that will be aligned.

Location within three-dimensional space where the object will be aligned.

The axis that will be given as front of the object.

Each time this node is activated (through Condition), the object will rotate to its destination by a certain amount. It can be completed in just one activation (Factor: 1.00) or up to 100 activations (Factor: 0.01). Any other value can be written between 0 and 1.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Always Sensor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/types/always.html

**Contents:**
- Always Sensor
- Properties
- Example

See the Python reference of this logic brick in SCA_AlwaysSensor.

The Always Sensor gives a continuous output signal at regular intervals. It is used for things that need to be done every logic tick, or at every x logic tick (with non-null Skip), or at start-up (with Tap).

See Sensor Common Options for common options.

This sensor does not have any special options.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Animation

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/index.html

**Contents:**
- Animation

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Animation Status

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/animation_status.html

**Contents:**
- Animation Status
- Inputs
- Outputs

Retrieve information about an action currently playing on an object.

Get an action currently playing on this object.

Select the layer from which to pick the action.

True if an animation is playing on the selected layer.

Name of the action currently playing on the selected layer.

Current frame of the action currently playing on the selected layer.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## API Stubs

**URL:** https://upbge.org/docs/latest/manual/manual/tools/api_stubs.html

**Contents:**
- API Stubs
- What Are They?
- UPBGE-stubs
- Using UPBGE-stubs
- Examples

Python is a dynamically-typed language, but that doesn’t mean you can’t have such quality-of-life features like auto-completion or type information for APIs, which all modern IDEs provide.

The only reason you can’t have them for UPBGE projects is that the relevant modules (namely, bpy.* and bge.*) are only available inside UPBGE.

There are two possible options to deal with this problem. Firstly, you can build UPBGE/Blender as a Python module, which would give your IDE the most accurate and up-to-date API information as possible.

But it’s not always easy to build UPBGE from source, especially if you are not familiar with the task. In this case, using API stubs could be a good alternative.

An utility to generate Python API stubs from documentation files in reStructuredText format called BPY Stub Generator (bpystubgen) can help us to get the UPBGE python API stubs.

The main usage of the program is to create Python API stubs from the documentation generated during the build process of UPBGE so that an IDE can provide autocompletion support and type hints for relevant modules like bpy or bge.

There are already a number of tools created with a similar goal in mind, notably fake-bpy-module and fake-bge-module which can be a good alternative to this project.

However, bpystubgen has a few advantages over the others:

It’s very fast - some of those tools may take over an hour to generate the entire stubs for blender, but bpystubgen can do it under a minute (1,593 source documents).

The generated stub modules preserve most of the source documentation, so you can use them as a manual as well.

It generates pep-561 compliant stub modules, so it’s safe to include them in your runtime module path.

Along with its fast execution speed, the project also provides well-organised api and test suites to make it easier to fix bugs or improve the output quality.

If you just want to use the API stubs, you can install them from PyPI without having to generate them yourself. As for UPBGE, stubs are available for the 0.3 release, which you can install as follows:

Once you install it via pip (or any other package manager you may prefer), you can configure the IDE of your choice as described in the project page BPY Stub Generator (bpystubgen).

After that, you can enjoy nice auto-completion and type information for most of the UPBGE’s Python API.

Auto-completion at work in PyCharm

Pop-up documentation support in VSCode

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (unknown):
```unknown
pip install upbge-stubs==0.3.*
```

Example 2 (unknown):
```unknown
pip install upbge-stubs==0.3.*
```

Example 3 (unknown):
```unknown
pip install upbge-stubs==0.3.*
```

---

## Append

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/list/append.html

**Contents:**
- Append
- Inputs
- Outputs

Append a value in the end of a given list.

Condition to be fulfilled for node to activate.

Which list to append to.

Type and the value to append.

True if node performs successfully, else False.

The given list with the new value attached at the end.

Square socket indicates a list.

If you give the list [1, 2, 3, 4] and the Integer 5, the output will be the list [1, 2, 3, 4, 5]

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Apply Force

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/apply_force.html

**Contents:**
- Apply Force
- Parameters
- Input
- Output

Applies an offset force to an object on any axis of the Cartesian plane. To function properly, the object must have a physical property that enables displacement.

Game Physics > Physics Type: Dynamic, Rigid Body, Soft Body.

The node applies force to the entire object. In contrast, the Apply Impulse node applies force at a specific point.

Selected mode of operation.

If checked, force will be applied in the direction of the object’s local axes, else of the object’s global axes.

The condition for this node to start.

Object that will be pushed away.

Value of the force that will be applied to the object, by the direction of the axes in the Cartesian plane. It can be a value referring to the axes of the world (global) or the axes of the object (local).

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Apply Impulse

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/apply_impulse.html

**Contents:**
- Apply Impulse
- Parameters
- Input
- Output

Applies a displacement force that has an origin (point) and a direction. To function properly, the object must have a physical property that enables displacement.

Game Physics > Physics Type: Dynamic, Rigid Body, Soft Body.

This node applies force at a specific point. In contrast, the Apply Force node applies force in entire object.

Selected mode of operation to apply.

If checked, object’s local axes will be used, else global axes are used.

The condition for this node to start.

Object that will be pushed away.

The point on which to apply the impulse.

The impulse to be applied to the object.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Apply Movement

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/apply_movement.html

**Contents:**
- Apply Movement
- Parameters
- Input
- Output

Moves the object a certain vector-defined distance. Does not apply acceleration.

The object is still subject to other forces while the motion is being applied, such as acceleration due to the force of gravity.

The node can be applied to some types of physical properties, i.e. Game Physics.

Selected mode of operation.

If checked, local coordinates will be used.

The condition for this node to start.

Object that will be moved.

The amount of displacement that will be applied to the object.

True if the node performed successfully else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Apply Rotation

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/apply_rotation.html

**Contents:**
- Apply Rotation
- Parameters
- Input
- Output

Rotates an object a certain vector-defined angulation. Each time this node is activated, the defined rotation will happen.

Selected mode of operation.

The rotation will be applied following the object’s local axes.

The condition for this node to start.

Object that will be rotated.

The value that will be applied to the rotation in degrees.

True if the node performed successfully.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Apply Torque

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/apply_torque.html

**Contents:**
- Apply Torque
- Properties
- Input
- Output

Rotates an object using torque mechanics and tries to follow real-world physical rules. It uses the Newton-meter as a unit of measure (torque = force x length of the lever).

In the real world, applying torque requires a lever with length and an object that is experiencing a binding force. For movement to take place on this object the torque must be greater than the bonding force. The real bonding force generally encompasses friction and tension.

Unlike in the real world, where the wrench holds the screw that is being rotated, in the UPBGE there is no such limitation and so all torque force is applied at once, which can perpetuate the rotation continuity.

If the object has some kind of Collision Bounds different from sphere, it will need a torque value greater than the force that makes the object static.

In order to limit pivoting of the torque, assign a rotation limit to a certain origin with either an Armature Bone or a Rigid Body Joint Constraint.

Selected mode of operation to apply.

If checked, Torque will be applied following the object’s local axes, else global axes.

The condition for this node to start.

Object that will be rotated.

The value that will be applied to the rotation in Newton-meters.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Armature / Rig

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/armature_rig/index.html

**Contents:**
- Armature / Rig

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Armature Sensor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/types/armature.html

**Contents:**
- Armature Sensor
- Properties
- Example

See the Python reference of this logic brick in SCA_ArmatureSensor.

The Armature Sensor is used to detect changes in values of an IK solver.

The Armature Sensor is available for armature objects only.

The bone to check for changes in value.

The bone constraint to check for changes in value.

How the sensor checks for changes in the bone.

Any changes will invoke the sensor.

Any value below of the amount of residual error in Blender space unit for constraints that work on position will invoke the sensor.

Any value above of the amount of residual error in Blender space unit for constraints that work on position will invoke the sensor.

Any value below of the amount of residual error in radians for constraints that work on orientation will invoke the sensor.

Any value above of the amount of residual error in radians for constraints that work on orientation will invoke the sensor.

Some tests will take a value, this value is used in the comparison when detecting changes.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## A Deeper Look

**URL:** https://upbge.org/docs/latest/manual/manual/introduction/deeper_look.html

**Contents:**
- A Deeper Look
- Use Cases
- Sample Games
- Under The Hood
- Project Development Process

UPBGE allows you to create real-time interactive 3D applications or simulations. This allows you to create almost any type of interactive project, like architectural presentations, virtual prototypes for robotic projects, physics simulation projects, simple and complex games, and much more.

Much can be achieved through UPBGE by default, as it provides a blank canvas full of features to be used, and even more can be accomplished by extending these features according to your needs. For example, if you’re working with robotics and needs to send or receive commands through a USB port, you can install the PySerial Python module for use with UPBGE. Or if you need a graphical feature that can’t be accomplished through the default UPBGE’s capabilities, you can write your own OpenGL shaders. The list goes on, and there’s a big chance that the project you aim to can be brought to life with UPBGE, using its features and abilities to be extended.

Here are some examples of games made with BGE/UPBGE:

Game Name / Creator Name: Krum - Battle Arena by Haidme produced with BGE/UPBGE.

Game Name / Creator Name: Tomato Jones 2 by Haidme produced with BGE/UPBGE.

Game Name / Creator Name: The Future’s End by Mark Telles produced with UPBGE 0.2.5.

Game Name / Creator Name: GTA-like prototype by ThePajlok Studios produced with UPBGE 0.3.

UPBGE oversees a game loop, which processes logic, sound, physics and rendering simulations in sequential order. The engine is written in C++.

By default, the user has access to a powerful and high-level visual logic programming interface. The visual programming in UPBGE provides deep interaction with the simulation, and its functionality can be extended through Python scripting. It is designed to abstract the complex engine features into a simple user interface, which does not require experience with Programming.

UPBGE is closely integrated with the existing code base of Blender, which permits quick transitions between the traditional modeling feature set and game-specific functionality provided by the program. In this sense, the UPBGE can be efficiently used in all areas of game design, from prototyping to final release.

UPBGE can simulate content within Blender, however it also includes the ability to export a binary run-time to Linux, MacOS, and MS-Windows.

There are a number of powerful libraries the UPBGE takes advantage of:

Audaspace: A sound library for control of audio. Uses OpenAL or SDL.

Bullet: A physics engine featuring 3D collision detection, soft body dynamics and rigid body dynamics.

Detour: A pathfinding and spatial reasoning toolkit.

Recast: A state of the art navigation mesh construction tool set for games.

When creating a game or simulation in UPBGE, there are four essential steps:

Create visual elements that can be rendered. Usually, 3D models.

Enable interaction within the scene using logic to enable custom behavior and determine how it is invoked.

Create one (or more) camera to give a frustum from which to render the scene, and modify the parameters to support the environment in which the game will be displayed, such as VR rendering.

Launch the game, using the internal player or exporting a runtime to the appropriate platform.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## A First Example

**URL:** https://upbge.org/docs/latest/manual/manual/editors/logic_nodes/a_first_example.html

**Contents:**
- A First Example
- Activating the Logic Nodes Add-on
- System Console
- Creating a New Logic Tree
- Adding Nodes
- Applying Logic Trees

The Logic Nodes add-on comes pre-installed in UPB eGE 0.3+. If not already, it needs to be activated:

Edit -> Preferences -> Add-ons

Navigate to Preferences

There, search/filter for logic, and check the box for Logic Nodes+.

Search for ‘logic’ and check the box

Click the little arrow, next to the check box, to expand the Logic Nodes+ add-on menu, and in the Preferences click Install or Update Uplogic Module button.

Install or Update Uplogic Module

This same Preferences menu can be used to report a bug > click Report a Bug button (internet connection is required). The default web browser will open github.com web page. There, click New issue button, and follow the instructions.

Houston, the eagle has landed. We’re good to go.

UPBGE uses system console/terminal to print info and error messages. To see those messages:

Window ‣ Toggle System Console menu.

Run UPBGE on Linux or Mac terminal

We will print some text to the console when a keyboard key is pressed. This is the “Hello World” example for the Logic Nodes.

Now let’s get started. First we need to create a logic tree. Switch the Editor Type to the Logic Node Editor.

Select Logic Node Editor

This editor is similar to the Shader Editor or Geometry Node Editor. Click on New and a new empty tree (named Logic Node Editor by default) will be created.

New empty Node Tree with side Dashboard

With mouse cursor inside Logic Node Editor, press Shift-A, or click Add button in top header. This will pop-up a menu with all available Logic Nodes, organized in sub-menus. Go ahead and take a look at what is available.

Available Logic Nodes in Add menu

For this example, we’re looking for two nodes: Keyboard Key and Print node. Easiest way to add nodes:

press Shift-A hotkey, to invoke adding a node;

immediately after that start typing, i.e. print - UPBGE is smart and will search for it;

if accidentally wrong node is selected, press ESC to cancel, and repeat.

Editor searches for node

Beside finding the node, Search pop-up also shows in which menu/sub-menu the nodes are.

Keyboard Key node is a node of the condition type. These nodes do not actually do anything in-game; they either provide a condition, or can be used to check for a more complex set of conditions.

Print node is an action type node. These nodes actually do something. They move objects, change properties, add constraints etc. - you name it.

Those two nodes need to be connected together. The Keyboard Key node has an If Pressed output socket, colored red. Connect it (click-and-drag) to the Condition input socket of the Print node and enter “Hello World” in the text box at the bottom, next to Value input socket (blue sockets are for strings). Also, if not already, look at the Keyboard Key node and you’ll see that it expects user to choose a key. Click the bottom field and press SPACE key, which will set that key as selected one. It should look something like this now:

Logic Nodes added and connected

Once done, all that’s left is to apply the tree to an object. Logic trees work the following way:

each tree can be applied to as many objects as you want;

meaning it is executed by each object it is applied to, separately.

Example: if this tree is attached to 4 objects and user presses SPACE key once, the message would be printed 4 times, once for each object.

To apply a tree to a cube, first a cube is added; select it and press Apply To Selected button, in the Dashboard tab of side N-panel. Press N to toggle N-panel, if it is hidden.

Apply logic tree to selected object

Be careful, trees can be applied to multiple objects at once!

To see which objects have been applied with a Logic Node tree, scroll down the Dashboard tab, and check the Tree applied to: sub-panel at the bottom.

Objects with applied Logic Node tree

If needed, sub-panels can be rearranged:

for easier rearranging, first collapse sub-panels - click small arrow next to the sub-panel title;

click-and-drag top-right icon (4 by 2 dots) of sub-panel.

Collapsed and rearranged N-panel sub-panels

What is left now is to run our example 'game':

in Render panel of a Properties editor, click Embedded Start or Standalone Start (hotkey is P) - the 'game' shall start;

with 'game' running, press SPACE (or whichever keyboard key is assigned in Keyboard Key node) once;

Start the game in Render panel

Finally check the system console - it should have our message printed:

once if logic tree was applied to one object;

twice if logic tree was applied to two objects;

four times if logic tree was applied to two objects, and SPACE was pressed twice etc.

System console/terminal output

See System Console for more info.

The Print node prints to the system console only, not to the Python interactive console. This is a feature of Blender and is not changeable.

Press ESC key to end the 'game'.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Barrier

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/time/barrier.html

**Contents:**
- Barrier
- Inputs
- Outputs

Only activate if the condition is true for the given amount of time. Example: If the condition is “Press A” and the Time socket is set to “1.0”, A has to be pressed for 1 second for the output socket to return True.

If connected, condition must be fulfilled for node to activate.

Output socket will return True if input condition has been true for this amount of seconds.

True if input condition has been True for Time seconds, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Basic Concepts

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_python_scripting/basic_concepts.html

**Contents:**
- Basic Concepts
- If you don’t know enough Python to begin
- Logic Bricks: Python Controller

This tutorial will give you a quick introduction about how to use Python within the Game Engine. Basically, it will enable you to start with Python scripting avoiding typical errors and wrong paths.

When writing Python code for the UPBGE we recommend to keep the UPBGE Python API open as reference. You can find it here: UPBGE Python API.

This tutorial is not a tutorial to teach you Python. If you don’t know enough Python to begin, find an online Python beginner tutorial, and learn the basics. Some recommendations:

jakevdp.github.io/WhirlwindTourOfPython.

techbeamers.com/python-tutorial-step-by-step.

developers.google.com/edu/python/set-up.

Just pick your poison. Take your time and learn the basics :-). If you go through it, you’ll be ready to try your new spells on the UPBGE!

Controller brick at Logic Bricks editor

A Python controller is basically a logic brick that you can program using Python scripts.

If you look at how a controllers usually behave, they do pretty simple things:

AND Controller: When all connected sensors are positive, activate all connected actuators.

OR Controller: When one of the connected sensors is positive, activate all connected actuators.

NAND Controller: When no connected sensor is positive, activate all connected actuators.

XOR Controller: When only one of the connected sensors is positive, activate all, etc.

These are all basic logic gates, but what if you want more control? What if you want to test if a sensor is positive, and actually check some values from it?

This is when you use a Python controller:

Python controller at Logic Bricks editor

You need at least one sensor connected to the controller in order to trigger it! It can be anything, but the trigger comes from a sensor.

Now to write a script, open UPBGE text editor, and start writing your first script.

So, little bit of disclaimer: When people see programming code, they usually go “that’s so hacker, it is too complex”. But fear not: Programs are written using English words, a bit like a recipe! It is a simple list of instructions to get from a state A to a state B.

Lot of comments in this code, but if you read the code word by word, it is pretty easy to understand what is going to happen once the Python controller will execute it!

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (julia):
```julia
import bge # the module to interact with the Blender Game Engine

# When this script gets executed by a controller (when it will be its turn)
# the following variable will point to the current running controller.
# The BGE executes each controller one after the other, but boy is it fast.
controller = bge.logic.getCurrentController()

# Controller "objects" (in Python) have a property named ".owner" that
# refers to the object owning the currently running controller.
# This is because this script can be shared by different Python controllers
# attached to other objects. Since we will run multiple times in a different context,
# this line allows us to figure out what object is currently running the controller!
owner = controller.owner

# In this example, let's do something silly, and move the cube up
owner.worldPosition.z += 0.1

# Let's make it turn too
owner.applyRotation([0, 0, 0.1]) # [x, y, z]
```

Example 2 (julia):
```julia
import bge # the module to interact with the Blender Game Engine

# When this script gets executed by a controller (when it will be its turn)
# the following variable will point to the current running controller.
# The BGE executes each controller one after the other, but boy is it fast.
controller = bge.logic.getCurrentController()

# Controller "objects" (in Python) have a property named ".owner" that
# refers to the object owning the currently running controller.
# This is because this script can be shared by different Python controllers
# attached to other objects. Since we will run multiple times in a different context,
# this line allows us to figure out what object is currently running the controller!
owner = controller.owner

# In this example, let's do something silly, and move the cube up
owner.worldPosition.z += 0.1

# Let's make it turn too
owner.applyRotation([0, 0, 0.1]) # [x, y, z]
```

Example 3 (julia):
```julia
import bge # the module to interact with the Blender Game Engine

# When this script gets executed by a controller (when it will be its turn)
# the following variable will point to the current running controller.
# The BGE executes each controller one after the other, but boy is it fast.
controller = bge.logic.getCurrentController()

# Controller "objects" (in Python) have a property named ".owner" that
# refers to the object owning the currently running controller.
# This is because this script can be shared by different Python controllers
# attached to other objects. Since we will run multiple times in a different context,
# this line allows us to figure out what object is currently running the controller!
owner = controller.owner

# In this example, let's do something silly, and move the cube up
owner.worldPosition.z += 0.1

# Let's make it turn too
owner.applyRotation([0, 0, 0.1]) # [x, y, z]
```

---

## Blender/UPBGE Basics

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/getting_started/blender_basic.html

**Contents:**
- Blender/UPBGE Basics
- Blender/UPBGE
- Main Menu
- 3D Viewport
- Outliner Editor
- Properties Editor
- Timeline Editor
- Workspace Customization
- More on the 3D View
  - Viewport Shading Modes

When you start Blender/UPBGE, you will be greeted with the splash screen. Although you can customize all aspect of Blender/UPBGE, in this manual we will assume you are using the default Blender/UPBGE settings and shortcuts.

Clicking anywhere else to dismiss the splash screen, you are presented with a default workspace.

Blender/UPBGE workspace

Blender/UPBGE window is divided into Editors. Each Editor region can be resized, moved, and changed to display a specific set of content. For now, let’s focus on the default setup.

At the top of the screen is the main menu, which offers basic functionalities such as File, Edit, Render and Help.

Selecting the Game Engine

By default, EEVEE render engine is selected. This engine enables certain features that are not accessible normally, and also disables features that are not available in UPBGE.

Occupying the majority of the screen is a 3D Viewport. Here you can see the 3D world you created and test the game. For now, feel free to explore the 3D Viewport by holding down your middle mouse button over the 3D Viewport and dragging the mouse; the view should rotate with the mouse movement. (Mac users can use the two-finger rotate gesture on the trackpad.) The default scene contains three objects: an immortal Cube, a camera, and a light. To select one of the objects, click on it.

Basic Navigation Controls

There are more than one way to navigate in UPBGE. Hold MMB to rotate the 3D view, scroll the Wheel to zoom in/out the 3D view. LMB to select a 3D object. Selected objects are highlighted in yellow. RMB to open context menu. Another way is Ctrl-MMB > move mouse to zoom, Shift-MMB > move mouse to pan. Not much new here, those are standard application navigation actions.

Numpad with default assigned views

Another common setup for the 3D Viewport is to split the view into four quadrants: top (Numpad 7), front (Numpad 1), side (Numpad 3) and a perspective/orthographic (Numpad 5) view. Turn on Quad view by Ctrl-Alt-Q with the mouse over the 3D Viewport. Press the same key combination to go back to the single view.

To quickly snap to one of the predetermined views (side, top, front, and so on), the number pad is the way to go.

To the right of the screen are two editors. The top portion is the Outliner, which contains a listing of all the data in the current Blender file. For a large project, the Outliner is an indispensable tool for organizing your scene. For now, you can safely ignore it.

Under the Outliner on the right, you have the Properties. Here you can access global settings for the file, as well as settings for individual objects. This is one of the most frequently used panels in Blender, after the 3D view perhaps. The Properties Editor is context sensitive, which means it will automatically display different content, depending on the object that is active. Take a closer look at the icons on the left side of the Properties, as shown in figure. These tabs organize the properties into groups, with the more general settings on top, and more specific settings at the bottom. Mouse-over the tab, the popup will tell the name of it (Edit > Preferences > Interface > Display > User Tooltips to enable the popup).

At the very bottom of the screen is a Timeline window, which will be useful when you start making animations.

The default screen, as described previously, is set up for general use. At some point, it becomes necessary to change the screen layout to accomplish other tasks. To select a different workspace, click the workspace tabs at the top.

Apart from the predefined workspaces, you can customize each one however you like. You can either split an existing editor into two or merge two adjacent editors together.

Editor, Region, and Area

A region within the Blender/UPBGE window is called an editor. An editor displays a specific set of content and tools. Common areas include: 3D Viewport, Properties, UV/Image Editor and more. Specific to UPBGE are Logic Brick Editor, Logic Brick Node View and Logic Node Editor.

Area/window splitting

Figure shows one area split into two. You can do it by dragging the top corner of the area to the right or bottom.

To merge two adjacent areas into one is exactly the same as shown in figure, but it is done in reverse order. Optionally, RMB on the edge between area(s) you want to split or join, and select the option in the Area Options pop-up menu.

Not only can you change the size and layout of the editor, but the type of editor can also be changed. As you can see in above figure, the left-most icon in the header can be used to change the editor type.

Dopesheet, Image Editor, and Logic Brick Editor

Almost everything a studio needs to create the game is integrated into a single interface: you can create the game, test the game, and play the game all from the same app. This means that, as an artist, you can create a game in the shortest time possible, without having to worry about importing and exporting files between different applications. As a programmer, you won’t have to switch back and forth between different software just to test your code. Figure above shows some screenshots of different editors that you will be using throughout the manual.

3D view is where you will spend most of your time, so let’s take a look at it in a bit more detail. You’ve already learned a few ways to navigate around the scene earlier in this chapter, using both mouse and the keyboard.

Viewport Shading Modes

Four different Viewport Shading modes available are used to change the way the scene is displayed onscreen. Those are:

Toggle X-Ray - enables X-ray of all objects; useful when the scene gets really complex; not a Viewport mode per se, rather an option.

Wireframe - draws all objects as wireframe, which allows you to see through objects.

Solid - draws all objects as solid faces, which is commonly used when modeling.

Material Preview - draws all objects as solid faces, with texture and accurate lighting. This is useful for previewing the scene.

Rendered - draws all objects as they will be rendered, also with texture and accurate lighting. This is how final rendered scene will look like.

Two most commonly used Shading modes are Solid and Material Preview. Press the Z > number/hotkey (underlined) to pop-up a circular selector and select desired mode. Alt-Z to toggle X-ray on and off - only available in Wireframe and Solid Shading mode.

Individual objects can override the Viewport Shading mode via Properties > Object > Viewport Display > Display As.

Far to the left of the Shading mode selector is the Editing Mode selector.

Object Mode - the default mode, which allows the manipulation of objects in the scene as a whole. From this mode, you can select any object in the scene, then move, rotate and scale it. In fact, almost everything apart from modeling can be done from Object mode.

Edit Mode - this mode can be seen as the counterpart to Object mode. It allows you to edit the underlying geometry of the object. If you are modeling, you’ll probably want to be in Edit mode, except if you are sculpting. For this reason, Edit mode is not available when a non-editable object is selected (for example, a camera or light).

To switch between Object mode and Edit mode, press the Tab key.

In addition to the two editing modes we just discussed, there are a few other modes that are less commonly used.

Sculpt Mode - only available for Mesh objects. Allows modeling the mesh as if it were clay.

Vertex, Weight and Texture Paint Mode - only available for Mesh objects. These modes allow the assignment of color or weight to the mesh.

Pose Mode - is used to animate bones in an armature. Only visible when Object has bones attached.

Edit and Object mode are by far the most commonly used editing modes, so we will refrain from diving too deeply into the other modes for now.

The joke is that to move an object in Blender, you have to press the G key, which stands for movinG. This gag stems from the fact that to a beginner, many of the shortcuts in Blender/UPBGE seem counter-intuitive. However, there is a very good reason why G is preferred over M - it can be easily accessed on the keyboard by the left hand while the right hand is on the mouse. Also, officially, G stands for Grab.

By default, Mac keyboard uses Command instead of Control as the default modifier key. So whenever you see Ctrl-Something, mentally map it to Cmd if you are using a Jobsian product.

Additionally, Blender/UPBGE has good support for multi-touch gestures on OS X. You can pinch to zoom, rotate to orbit around, and pan around.

Shortcuts that work the way you would expect:

Ctrl-Q - close (quit) application.

Those shortcuts work anywhere within Blender: they are effectively global. Unfortunately, the familiarity ends here.

To manipulate an object in the 3D view, generally you have to select it first:

Shift-LMB - extend selection to multiple objects;

Shift-A - deselect all.

All actions above are “reversible”. If something is already selected, LMB on it will deselect it. If all the objects are already selected, double-tapping A will deselect all.

Once an object is selected, you can manipulate it. The keyboard shortcuts below correspond to the three most basic transforms:

Move mouse - carry out transform action;

LMB - confirm transformation;

Enter - confirm transformation.

Pressing one of the keys will start the transformation, and then you can move a mouse to transform/move the object. To finalize the transformation, LMB or Enter.

The final tip that you will learn is the search functionality. If you are unable to recall how to invoke a certain operation, whether through a button or a keyboard shortcut, a quick way to find it is by using the search functionality. Press F3 key and start typing in what you are looking for, and the result should appear.

Blender/UPBGE is designed with certain philosophies in mind. Understanding these will allow you to use Blender the way it is intended, which allows you to navigate around Blender faster and work more efficiently.

Let the brainwashing begin!

Because Blender was originally created as an in-house software, its interface is designed to maximize speed and efficiency for users who have mastered it. Since Blender 2.5, a lot of work has been done to make the interface more user-friendly. That said, Blender is probably unlike any other program you’ve used before, including other kinds of 3D software. Luckily, the Blender interface is very consistent within the application. This means that once you learn to do something, you’ll be able to use it in another part of the program.

Because of the large number of commands Blender is capable of performing, invoking a function through a quick tap on the keyboard is generally faster than using the mouse to find the menu entry. As you follow through the rest of this section, pay special attention to the shortcut keys that are used, because Blender is designed to let you work fast once you learn the shortcuts.

N-panel > View > 3D Navigation

Blender’s keyboard shortcuts are optimized for a full-sized English QWERTY keyboard. The number pad (which, unfortunately, is not present on many laptops) is used to quickly navigate around the 3D scene. Laptop users usually have to press extra keys on their keyboard (such as the Fn or a toggle) in order to simulate a number pad key. As a solution, go to Edit > Preferences > Input > Keyboard tab and enable Emulate Numpad option to use main 1 to 0 keys instead of Numpad keys.

Alternatively, Blender also has an add-on called 3D Navigation that provides an easier way to navigate around the world for people without a number pad. To enable the 3D navigation plug-in, enable Edit > Preferences > Add-Ons > 3D Views: 3D Navigation add-on. Then you can switch views quickly from the 3D view’s Toolshelf.

Blender is designed for a three-button mouse: a mouse with two buttons and a scroll wheel. Although there is an option to emulate the middle-mouse button (when you click on the scroll wheel), this book will assume that you are working with a three-button mouse for convenience.

How to Emulate a Three-Button Mouse

If you don’t have a three-button mouse, you can use the Alt-LMB combination to emulate the middle mouse button. To enable this feature, go to Edit > Preferences > Input > Mouse and turn on Emulate 3 Button Mouse. On some Linux distros, it is possible to press LMB & RMB at the same time to emulate MMB press.

In Blender, the actions you can perform at any given time are limited to the current state of Blender, also known collectively as the “context”. For example, certain operations can only be invoked when you have an object selected; the Property Editors change, depending on which object is selected; the effect of the keyboard shortcuts even changes, depending on where your mouse is positioned. This context-sensitive nature lets you focus on the task at hand by only providing you with options that makes sense at the time. This is Blender’s way of preventing the interface from getting too cluttered.

The “context” usually refers to one or a combination of the following:

Active rendering engine - EEVEE and Workbench are available.

Active editor - is defined as the window subdivision that the mouse cursor is hovering over. Shortcut keys often have different effects, depending on which editor the mouse is over.

Active object - is defined as the object that is most recently selected.

Selected object - all the objects that have been selected (highlighted). Keep in mind that there can be more than one selected object, but only one active object.

Editing mode - Blender has six different modes of editing; most commonly used are the Edit mode and the Object mode. In Object mode, you can manipulate objects as a whole. In Edit mode, you can change the shape of a mesh. In each mode, there is a unique set of tools and options at your disposal. You will learn about the other four modes (Sculpt, Vertex Paint, Texture Paint, Weight Paint) in later chapters.

Often, a single Blender file contains hundreds of objects, each with different colors, textures, and animations. How is all this organized?

Blender uses “data blocks” to represent content stored within a Blender file. Each data block represents a collection of data or settings. Some common datablock types you will encounter are Object, Mesh, Material, Texture and Image datablock.

In order to reduce the apparent complexity of the program, Blender further organizes data blocks into hierarchies. At the top level are scenes, which can have a number of worlds, each of which can have any number of objects (objects can be a mesh, a light, a camera, and so on). If the object is a mesh, then a Mesh datablock is attached to it. If the object is a light, then a Light datablock is attached to the object.

Throughout the Blender interface, you will run into many datablock managers. They all look like the figure aside.

Because datablocks can be shared, copied, and reused, large scenes can be managed efficiently through the use of shared datablocks.

Collections and parenting both allow you to introduce some form of order to the scene by setting up arbitrary relationships between different objects. But collections and parenting work in different ways.

Parenting is used to establish links between multiple objects so that basic transformations like location, rotation, and scaling are propagated from the parent to its children. This way, any transformation applied to the parent is automatically applied to all the children. Parenting is a useful way to “glue” different objects together so they behave as one.

To parent one object to another, simply select the object you want to be the child first. If more than one object is to be a child, select all of them. Select the object that you want to be the parent last. Ctrl-P to parent them.

An object can only have one parent object, but a parent object can have many children. Manage parent/child relations from Properties > Object > Relations.

Collections can also be used to logically link objects in the scene together without any transformation constraints to the objects. Unlike parenting, collection does not have a parent-child relationship; objects are simply members of a collection.

Select all the objects you want to group, Ctrl-G to add them to a new collection. You can also manage collection membership from Properties > Object > Collections.

Collection, by itself, it not very useful. But collection can be quickly “instanced”. Collection Instance is a very useful way to create multiple copies of objects without making actual copies of the objects. Collection will also come in handy for asset management, which will be discussed in another chapter.

A single object can be in multiple collections. A collection can have multiple objects.

Blender is designed so that older files can be opened with newer versions of Blender. But due to the rate that Blender matures, some unexpected behaviors are to be expected when you least expect them.

Due to the Blender Python API change in Blender 2.5, old scripts written for 2.4x will be broken in later versions of Blender. But by the time you are reading this, there should be enough new content available for you to find.

This concludes the crash course on Blender and the game engine. By now, you should have a cursory understanding of the function of a game engine and be familiar with the Blender interface. In the next chapter, you will get your hands dirty and build a simple game by following the step-by-step tutorial.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Bone Constraints

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/bone_constraints/index.html

**Contents:**
- Bone Constraints

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Bone Status

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/armature_rig/bone_status.html

**Contents:**
- Bone Status
- Inputs
- Outputs

This node is deprecated.

Get information about a specific armature bone.

Which object to inspect.

String representation of a desired bone.

Position of the Bone in pose matrix transform.

Rotation of the Bone in pose matrix transform.

Scale of the Bone in pose matrix transform.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Boolean

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/boolean.html

**Contents:**
- Boolean
- Parameters
- Inputs
- Outputs

Selected data type to be used - boolean.

True if checked, else False, or result of socket input.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Brake

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/vehicle/brake.html

**Contents:**
- Brake
- Parameters
- Inputs
- Outputs

Selected axis of vehicle wheels.

If connected, condition must be fulfilled for node to activate.

Vehicle object to use.

Number of wheels for selected axis.

Applied power to selected axis.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Branch

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/branch.html

**Contents:**
- Branch
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Bricks

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/bricks/index.html

**Contents:**
- Bricks

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Briefing

**URL:** https://upbge.org/docs/latest/manual/manual/introduction/briefing.html

**Contents:**
- Briefing
- An Origin Story
  - Blender Begins
  - The Dark Nights
  - Blender Rises
  - Blender vs UPBGE
  - Features
  - Development

It was the mid-1990s, and the personal computer was taking off faster than anyone had anticipated. With it, there arose the advent of animated graphics and 3D games.

It was at this ripe time that Blender came into being. Blender started off as an in-house 3D animation software created by a small Dutch animation studio called NeoGeo. Perhaps it was because of the lack of a cheap and capable substitute; perhaps it was due to sheer ambition, NeoGeo decided to create its own animation software from scratch rather than using what was available.

The chief programmer of Blender was Ton Roosendaal, who was responsible for writing a large part of the core Blender functionalities.

For the next few years, Blender remained the internal tool of a very successful animation studio. The software became so good that in 1998, Blender was made available to the public. A new company, Not a Number (NaN), was formed to oversee the development and distribution of Blender. Largely via the Internet, Blender was distributed as two separate versions: a free version with limited functionality and a version that was not free (called Blender Publisher) that had a few additional features. Being the only complete 3D animation and game creation package available for free at a time when computer graphics was still in its infancy, Blender started gaining popularity, and many online communities developed that allowed artists to share knowledge and their work.

Blender 1.6 and Blender 2.5

Alas, with the collapse of the Internet bubble and some other unfortunate circumstances, Not a Number (NaN) filed for bankruptcy in 2002. Since Blender was the intellectual property of the company at the time, dissolving the company meant an uncertain future for Blender. The Blender community did not want to see their favorite software go down with NaN. So a deal was struck in which NaN would release the source code of Blender to the public for a payment of €100,000. A “Free the Blender” fundraising campaign was started. The online community responded very generously. A few months later, enough money was collected to convince NaN to re-release Blender as an open source software to the newly established Blender Foundation. The foundation was created specifically to manage the now open source Blender. Ton Roosendaal, the original creator of Blender, heads the foundation.

Located in beautiful Amsterdam, the Blender Foundation now oversees the development, distribution, and marketing of Blender. But because of the open source nature of the software, its development has been driven largely by volunteer contributors from across the world.

The Blender Foundation also created the Blender Institute, an animation and game studio that focuses on movie and game development using Blender. The Institute produced the movies Elephants Dream, Big Buck Bunny, Sintel, Tears of Steel, Cosmos Laundromat and the game Yo, Frankie!. These projects serve two main goals: The production process is an opportunity to improve Blender in a real studio environment, and the end result also serves as an advertisement for the software itself.

Then came Blender 2.5, which changed much of how Blender looked and behaved. This refactoring, as it was called, took years of planning and coding. Blender 2.5 marks a significant milestone in the history of Blender. For users coming from the Blender 2.4x series, the entire interface looks radically different: menus items are rearranged, keyboard shortcuts are altered, even the default color scheme has changed from a boring gray to a slightly less boring shade of gray. Blender 2.5 is designed to be more intuitive, faster to use, and easier to learn than its predecessor.

Blender uses the Python programming language for scripting. With Python, you can customize the behavior of Blender, extend its functionality, and, more importantly, control the game engine. Knowing how to program is not a requirement for using Blender, but knowing Python will make you a far more capable game-maker.

The year 2012 marked the tenth anniversary of Blender going open source. During these 10 years of open source development, more than 150 people have contributed something to the source code, totaling 50,000 contributions (“commits,” in GIT techno-jargon), averaging nearly 30 commits every day over the past year. Needless to say, the program has improved much over the years, and it shows no sign of slowing down when it reaches almost to the thirtieth anniversary. The image below shows the Blender development statistics gathered from the official GIT repository including Blender trunk all its branches.

You already know that Blender is an open source 3D software that is capable of modeling, animation, rendering, compositing, and producing a game all in one package. Let’s analyze the term “open source 3D software”: “Open source 3D software” means that Blender’s source code is available for anyone to access and modify. The most obvious advantage to open source software is that as an artist, you can use Blender for free, for non-commercial as well as commercial work. As a developer, you are allowed to modify Blender in any way you want to suit your specific needs. But open source does not mean that anyone can make changes to the Blender code without approval. Blender is licensed under the GNU Public License v2 (GPL2). In a nutshell, it means that Blender can be copied, modified, and if re-shared, the changes in the source code have to be available and licensed in an equivalent license.

The Uchronia Project Blender Game Engine (UPBGE) is a Blender’s builtin tool derived from Blender Foundation’s Blender Game Engine for real-time projects, from architectural visualizations and simulations to games.

Originally created by Tristan Porteries as a fork from the Blender Game Engine with the purpose to develop the Blender Game Engine in a faster way, became independent with the Blender Foundation’s announcement of BGE’s removal when it reached to Blender 2.80. With this independency, the UPBGE’s developers (former BGE developers) have freedom to change and add features that could not be changed before (because the possibility of an official Blender merge, now discarded).

Basically, due to its periodic synchronization with Blender source code (almost daily), UPBGE, as its acronym suggests, has become a Blender from a parallel universe in which the game engine was never removed.

In any case, UPBGE is kriptonian for “hope”. Who knows if in the future that parallel universe merges with our universe and we may add another line entitled “Justice League” to this beautiful story :-).

Until that time comes, UPBGE has adopted the new physically based and state-of-the-art real-time render engine, EEVEE. This way all you can do in Blender/UPBGE editor you can translate it to the Game Engine. A truly WYSIWYG (What You See Is What You Get) Game Engine, the strongest UPBGE feature.

Of course, software exists to serve the users - that’s you. Every time a Blender and/or UPBGE user creates a piece of artwork, it justifies, even if just a little, the enormous amount of time that went into creating the software. We hope that by picking up this manual, you are on your way to creating something amazing to share with the world.

Compared to some of the commercial game engines available today, the Uchronia Project Blender Game Engine (UPBGE or BGE or GE for short) is relatively simple. Is that a bad thing? Not necessarily. A simple platform like UPBGE is very easy to learn, and yet it’s flexible enough to do a lot.

UPBGE have lots of new features, improvements and bugs fixed. Some features that UPBGE supports are:

Realtime advanced physics powered by Bullet, including rigid bodies, obstacle simulation and path finding.

Fully integrated audio engine powered by OpenAL and Audaspace,supporting 3D sound and sound effects.

Two easy and straightforward visual logic systems, Logic Bricks and Logic Nodes.

Powerful Python language bindings, allowing support to even more libraries through the use of PyPI.

Development process entirely inside Blender, without needing to import/export assets, although most used formats are supported through import/export add-ons (FBX, Collada, glTF, obj, stl, etc).

Execution of game in Blender’s viewport (for fast previewing) or on an standalone executable.

Rendering powered by state of art Blender’s EEVEE engine including PBR shading, SSR reflections, GTAO ambient occlusion, Bloom, Soft and contact shadows, Light probes for global illumination, Volumetrics, etc.

Blender’s Linked Libraries feature, allowing to organize projects in multiple blend files.

GLSL custom shaders for visual effects and post processing.

UPBGE is maintained by a group of developers in their spare time and its community. You can contribute to UPBGE if you code in C++ or Python: just open a pull request, submit your changes and wait for the reviewers. Also, even if you don’t code, you can contribute by submitting bug reports, feature requests and participating discussions on issues.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Camera

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/camera/index.html

**Contents:**
- Camera

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Camera Ray

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/raycasts/camera_ray.html

**Contents:**
- Camera Ray
- Inputs
- Outputs

Cast a ray from the camera in the direction of coordinates on the screen.

Which condition will be used for node to activate.

Screen coordinates at which to cast the ray.

Which property to use.

Ignore objects that don’t have the given property.

Maximum reach of the ray.

True if the ray has hit a target, else False

The object the ray has hit, or None

The world point the ray has hit, or None

The normal of the face the ray has hit, or None

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Character

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/character/index.html

**Contents:**
- Character

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Character Controller Templates

**URL:** https://upbge.org/docs/latest/manual/manual/python_components/getting_started/character_controller_templates.html

**Contents:**
- Character Controller Templates
- Character Controller Component
- First Person Camera Component
- Third Person Camera Component
- Simple Animator Component

These templates were created to help UPBGE users to create games or any kind of interactive things that requests a Character Controller. Easy to use, easy to attach to your project.

To use, just select it from template label at script editor and you’re done! You can use this template in your projects, even for commercial projects. You only need to give credits to Guilherme Teres Nunes (UnidayStudio) for this. It’s very easy to use: Just load this script into your .blend file through template label (or paste it in the same folder that your .blend is), select the object that you want, and attach the script into the object’s components using Register Component button.

This component will serve as a Character Controller for your game. With this, you can easily made an object move using W, A, S, D, run with LSHIFT and Jump with SPACE. You simply have to create a capsule for your character, set the physics type to “Character” and attach this Component to them. It’s very simple to configure:

Character Controller component

Activate: If you want this component running.

Walk Speed: The character’s walk speed.

Run Speed: The character’s run speed.

Max Jumps: The character’s max jumps. Set to 0 if you don’t want the character to jump.

Static Jump Direction: If you want to make your character jump in a static direction, activate “Static Jump Direction”. It means that, if the player wasn’t moving when he pressed Space, the character will jump up and the player will not be able to change this during the jump. The same for when he was moving when pressed Space. The jump direction will be the character direction when the player press space.

Static Jump Rotation: Exactly like the Jump Direction, but for the character rotation.

Avoid Sliding: If your character object have Collision Bounds activated, I’d recommend to enable the “Avoid Sliding” option. If so, the component will avoid the character from sliding on ramps.

Smooth Character Movement: You can make the movement gets more smooth by increasing this value (0.0 to 1.0).

Make Object Invisible: Makes the object invisible ingame (useful if you attach this component to a capsule object that have a armature inside).

This component was created to be attached to your camera and to give you a great mouselook control. Very useful for First Person games.

To use, add a camera in your scene, parent it into your character capsule (you can use the Character controller Component on it), and attach this Component to the camera. Don’t forgot to position the camera in a place near the “head” of your character.

You can configure the mouse sensibility, invert X or Y axis and enable/disable the camera rotation limit. It’s very simple to configure:

First Person Camera component

Activate: If you want this component running.

Mouse Sensibility: The mouse sensibility.

Invert Mouse X Axis: To invert the mouselook on the X axis.

Invert Mouse Y Axis: To invert the mouselook on the Y axis.

Limit Camera Rotation: Limits the camera rotation on the X local axis. Very useful for First Person games to avoid the camera from flip upside down.

This component was created to be attached to your camera to give you a great third person mouselook control. Very useful for Adventure games, RPGs, Open Worlds, or any kind of games that may require a third person camera.

To use, add a camera in your scene, parent it into your character capsule (you can use the Character controller Component on it), and attach this Component to the camera. And you’re done! The component will do the rest for you. :)

You can configure the mouse sensibility, invert X or Y axis and enable/disable the camera rotation limit. It’s very simple to configure:

Third Person Camera component

Activate: If you want this component running.

Mouse Sensibility: The mouse sensibility.

Invert Mouse X Axis: To invert the mouselook on the X axis.

Invert Mouse Y Axis: To invert the mouselook on the Y axis.

Camera Height: The height that you want your camera to be (consider height zero = the center of your character).

Camera Distance: How far from the character that you want your camera to be.

Camera Crab (Side): You can make the camera stay on the side of your character, if you want. Just adjust this variable.

Camera Collision: If you want your camera to have collision (to prevent the camera from traversing walls).

Camera Collision Property: The property that you want your camera to avoid (if you want the camera to avoid all the objects, leave this blank).

Align Player to View: You can define when you want the player (character) to look at the camera view direction: Never, just when the player moves or always.

Align Player Smooth: How smooth you want the player to look at the camera direction. 0 means no smooth and 1 means maximum smooth possible.

By using this Component, you can also call some functions using python (from other components) to help you: setCameraAlign(type), setCameraPos(x,y,z), alignPlayerToView(), getCameraView(). Take a look at the implementation to see how these functions works.

This component will automatically align the armature to the move direction of your character, runs the right animations accordding to the speed and if the character is on air or not.

To use, attach this component to the armature of your character. It’s important that the armature is parented with an capsule object with physics type equals to Character. It’s very simple to configure:

Simple Animator component

Activate: If you want this component running.

Max Walk Speed: Define the max speed that you want while executing the walk animation. After this speed, the character will start interpolating the run animation. (Read the notes at the end).

Max Run Speed: Define the max speed that you want while executing the run animation. After this speed, the animation will not change.

Suspend Children’s Physics: Enable this if you want to remove all the physics from the armature’s childrens (recursive). Useful to avoid these childrens to collide with the player capsule, causing a physics bug.

Align To Move Direction: Enable this if you want to make you character faces the direction that the player is going.

Align Smooth: How smooth you want to align the character with the direction. 0 Means no smooth and 1 means max smooth.

Idle Animation: Define the name of the Idle (stopped) animation, the frame start and frame end.

Walk Animation: Define the name of the Walk animation, the frame start and frame end.

Run Animation: Define the name of the Run animation, the frame start and frame end.

Jump Up Animation: Define the name of the Jump Up animation, the frame start and frame end.

Jump Down Animation: Define the name of the Jump Down animation, the frame start and frame end. The Jump animations should be divided in two: Jump Up and Jump Down. The first one will be executed when the character is going up. The second, whe the character is falling. Both should be loop animations.

The anim interpolation/transition between idle-walk and walk-run according to the speed is not implemented yet.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Check Angle

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/vectors/check_angle.html

**Contents:**
- Check Angle
- Parameters
- Inputs
- Outputs

Compare the angle between two vectors against a given value.

Which operation to use at checking.

First vector to use for operation.

Second vector to use for operation.

Compare the angle between the two vectors agains this value.

The selected operation outcome.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Clamp

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/clamp.html

**Contents:**
- Clamp
- Inputs
- Outputs

Will clamp Value between Min and Max values.

Minimum value to clamp to.

Maximum value to clamp to.

Resulting clamped value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Clear Variables

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/variables/clear_variables.html

**Contents:**
- Clear Variables
- Inputs
- Outputs

Remove all stored variables from the selected file.

Which condition must be fulfilled for node to activate.

Path to the directory containing the requested file.

Name of the file itself, ending can be omitted.

True if variables have been cleared successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Collections

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/collections/index.html

**Contents:**
- Collections

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Collision

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/collision.html

**Contents:**
- Collision
- Parameters
- Inputs
- Outputs

Detect and react to collisions involving a given object.

Monitor for continuous collision, not just initial one.

The monitored object.

If enabled, changes the “Property” socket to a “Material” one.

If set, only detect collisions with objects that have this property.

If set, only detect collisions with objects that have this material applied.

True if a collision has occured according to the “Continuous” property, else False.

The object with which the monitored object is colliding with.

A list of objects with which the monitored object is colliding with.

The point in world space where the collision has occured.

The normal of the face on which the collision has occured.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Collision Sensor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/types/collision.html

**Contents:**
- Collision Sensor
- Properties
- Example

See the Python reference of this logic brick in SCA_CollisionSensor.

A Collision Sensor works like a “touch sensor” but can also filter by property or material. Only objects with the property/material with that name will generate a positive pulse upon collision. Leave blank for collision detection with any object.

Soft Bodies The Collision sensor cannot detect collisions with soft bodies. This is a limitation in Bullet, the physics library used by the Game Engine.

See Sensor Common Options for common options.

Makes it sensible to other collisions even if it is still in touch with the object that triggered the last positive pulse.

Toggles between material and property filtering.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Color RGBA

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/vector/color_rgba.html

**Contents:**
- Color RGBA
- Inputs
- Outputs

Fixed selected color, or a result from connected socket.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Color RGB

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/vector/color_rgb.html

**Contents:**
- Color RGB
- Inputs
- Outputs

Selected color or result from connected node.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Combine XYZW

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/vector/combine_xyzw.html

**Contents:**
- Combine XYZW
- Inputs
- Outputs

Accepts float inputs and combines them into Quaternion.

Fixed input X float value, or result from connected node.

Fixed input Y float value, or result from connected node.

Fixed input Z float value, or result from connected node.

Fixed input W float value, or result from connected node.

Resulting XYZW Quaternion.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Combine XYZ

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/vector/combine_xyz.html

**Contents:**
- Combine XYZ
- Inputs
- Outputs

Accepts float inputs and combines them into Vector3.

Fixed input X float value, or result from connected node.

Fixed input Y float value, or result from connected node.

Fixed input Z float value, or result from connected node.

Resulting XYZ Vector3.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Combine XY

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/vector/combine_xy.html

**Contents:**
- Combine XY
- Inputs
- Outputs

Accepts float inputs and combines them into Vector2.

Either fixed input float value, or result from connected node.

Either fixed input float value, or result from connected node.

Resulting XY Vector2.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Commit Guidelines

**URL:** https://upbge.org/docs/latest/manual/manual/contribute/commit.html

**Contents:**
- Commit Guidelines
- Writing a Good Commit Message

Access to directly submit changes is limited to people with commit access to the repository. Once you are provided with commit access you can start committing directly instead of creating a patch file.

You can make commits from your Git client or using the Git command line tool. The following command will create a commit and send it to the central repository:

If you leave out -m "message", you will be prompted to type the message in a text editor.

You should make sure you are always on the latest revision before committing. You may not be able to commit directly if there are conflicting changes in the latest revision. To avoid this, update your local repository before committing.

Blender’s Git usage guide

When making changes to the manual that directly relate to a specific commit (change) it is helpful to make the title of the commit the same as the commit. It is requested that you include the commit hash of the commit made to source code.

For example, the commit rBM8473 includes a descriptive indicative of the changes made along with the hash rBa71d2b260170. Hash can be extracted from the URL provided in the documentation task for a specific upcoming release.

Other more general changes do not have to follow the above policy, however, it is still important to make the description clear about what changes you made and why. It can be helpful to prefix the commit title with a prefix word such as Cleanup: or Fix: when you are making general cleanups or fixes respectively.

Writing good commit messages helps administrators keep track of changes made and ensures all new features are properly documented.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (unknown):
```unknown
git commit -m "This is what I did"
git push
```

Example 2 (unknown):
```unknown
git commit -m "This is what I did"
git push
```

---

## Compare

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/compare.html

**Contents:**
- Compare
- Parameters
- Inputs
- Outputs

Will compare two float values, according to selected standard mathematical/programming Operator.

Selected operator for comparing.

First type and value to use for comparing.

Second type and value to use for comparing.

Resulting boolean value of comparison. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Compatibility Notes

**URL:** https://upbge.org/docs/latest/manual/manual/introduction/compatibility_notes.html

**Contents:**
- Compatibility Notes
- UPBGE VS Blender
  - UPBGE VS BGE

UPBGE is fully integrated into Blender environment, but it doesn’t mean it supports all the features that Blender provides. Here’s some compatibility info about various features present in Blender relative to UPBGE.

Object types supported

Any other object type (like Curve, Speaker, Force Field, etc) will not be rendered into game. A Curve Object can be converted to Mesh though.

Data-blocks supported

Shapekey (with Action, otherwise unused)

Particle (partially supported)

Any other data-block type (like Line Styles, Brushes, etc) have no use or will not be rendered into game.

BGE also have some incompatibilities with UPBGE. UPBGE can partially load and execute games made in BGE, but a game made in UPBGE can’t be executed in BGE, resulting in several issues like:

Logic can’t run most of the times.

Materials get messed up.

UPBGE do not support Multitexture material mode anymore. Set to GLSL when in vanilla BGE.

Sometimes physics simulation get messed up.

Along with this compatibility with BGE, UPBGE comes with features not supported by BGE, like Modifiers applied automatically at game start (instead of discarded, as in BGE).

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Constraints

**URL:** https://upbge.org/docs/latest/manual/manual/editors/properties/constraints.html

**Contents:**
- Constraints
- Rigid Body Joint Constraint
- Options

The Constraints tab in Properties editor exposes constraints setups for current object.

Currently in UPBGE only the Rigid Body Joint constraint can be set through the user interface.

The Rigid Body Joint constraint is very special, it is used by the physics part of UPBGE to simulate a joint between its owner and its target. It offers four joint types: hinge type, ball-and-socket type, cone-twist type, and generic six-DoF type.

The joint point and axes are defined and fixed relative to the owner. The target moves as if it were stuck to the center point of a stick, the other end of the stick rotating around the joint/pivot point.

In order for this constraint to work properly, both objects (so the owner and the target object) need to have Collision Bounds enabled.

Rigid Body Joint panel

Object used to select the constraints target, and is not functional (red state) when it has none.

Works like an ideal ball-and-socket joint, i.e. allows rotations around all axes like a shoulder joint.

Works in one plane, like an elbow: the owner and target can only rotate around the X axis of the pivot (joint point).

Angular limits for the X axis

Similar to Ball, this is a point-to-point joint with limits added for the cone and twist axis.

Works like the Ball option, but the target is no longer constrained at a fixed distance from the pivot point, by default (hence the six degrees of freedom: rotation and translation around/along the three axes). In fact, there is no longer a joint by default, with this option, but it enables additional settings which allow you to restrict some of these DoF:

Linear and angular limits for a given axis (of the pivot) in Blender Units and degrees respectively.

The 6DOF constraint has a limitation due to it uses euler angles instead of quaternions. Basically, the rotation of Y-axis can be +/-90 degrees only, if you exceed that maximum the constrain will go haywire. A good solution to avoid issues is to modify your model in a way that the free rotation doesn’t match with the Y local axis of your object.

Normally, leave this blank. You can reset it to blank by right-clicking and selecting Reset to Default Value.

When enabled, this will disable the collision detection between the owner and the target (in the physical engine of the BGE).

When enabled, this will draw the pivot of the joint in the 3D Views. The most useful, especially with the Generic 6DOF joint type!

Allow breaking of constraint on high impulse.

Break constraint on impulse greater than threshold.

These three numeric fields allow you to relocate the pivot point, in the owner’s space.

These three numeric fields allow you to rotate the pivot point, in the owner’s space.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Contribute

**URL:** https://upbge.org/docs/latest/manual/manual/contribute/contribute.html

**Contents:**
- Contribute
- Install Dependencies
  - Linux
  - macOs
  - Windows
- Download the Repository
- Setup the Build Environment
- Build the Manual
- Troubleshooting
- Editing the Manual

The UPBGE Manual is a community driven effort to which anyone can contribute. If you found a typo or you want to improve the general quality of the documentation, there are several options for helping out. You can:

Fix problems, improve the documentation and write new sections. Make a Pull Request (PR) with the proposed changes in UPBGE Docs project. Detailed instructions are in following pages.

Report errors in the documentation.

Join UPBGE Discord channel for help and chat.

UPBGE source-code repository can be found on github.

If you want to contribute several things directly, ask for commit rights.

To build the documentation we need:

Python 3 to run Sphinx;

Sphinx to build html pages;

ReadTheDocs Theme for Sphinx as default theme;

git to clone the documentation and commit changes.

For the appropriate system, run the command in a terminal:

$ sudo apt-get install python3 python3-pip git

$ pip3 install sphinx sphinx-rtd-theme

$ sudo yum install python3 python3-pip git

$ pip3 install sphinx sphinx-rtd-theme

$ sudo pacman -S python3 python3-pip git

$ pip3 install sphinx sphinx-rtd-theme

If using Homebrew, run the following commands in the terminal:

Download the Python installation package for Windows, and install Python with the installation wizard.

Please make sure that you enable the Add Python to PATH option. The option must be enabled so you can build the manual with the make script. All other settings can remain as set by default.

Navigate into desired folder, where UPBGE-Docs will be installed:

Clone the UPBGE Manual repository:

git clone https://github.com/UPBGE/UPBGE-Docs.git

The repository will be downloaded, which may take a few minutes, depending on your internet connection.

Below command will install sphinx and sphinx_rtd_theme. If you already installed them, following the above instructions, there is no need to install them again. This is for Windows users.

Navigate into UPBGE-Docs folder, which was just created by git clone:

Inside that folder is a file called requirements.txt, which contains a list of all the dependencies we need. To install these dependencies, we use the pip command:

pip install -r requirements.txt

Every now and then you may want to make sure your dependencies are up to date using:

pip install -r requirements.txt --upgrade

Once all dependencies are installed, navigate into UPBGE-Docs folder and run the make command:

This command will build the documentation files into the build directory.

Navigate into build/html folder, and run index.html file, either from terminal, or file explorer, by double-clicking the file. Documentation will be opened with OS default web browser.

On MS Windows you can double-click make.bat file, to easily run the command, without having to open the Command Prompt and typing commands.

If for some reason the build fails, check if the C-compiler or build-essential (or build-essentials) are installed on your operating system. Search the web or post a question in online forums for more information.

If after build the structure of the Manual, i.e. navigation/toc side panel does not work as expected, deleting whole build directory, and runing make html command again might help solve the issue.

If rst formatting is not displayed as expected, try adding:

directive to the top of the .rst file.

Before editing the Manual, it is advised to copy the UPBGE-Docs folder, and rename this copy, i.e. UPBGE-Docs-edit. Make the changes in this copy, and when satisfied with changes you want to commit, copy-paste the relevant files into original UPBGE-Docs folder.

As a good developer practice, it is also advisable to have your personal document file, where notes are kept: copy-paste info from web, what works and what not, fixes that were applied and solved issues etc.

With your favorite text/code editor, make some changes, fix typos, add images, and commit the changes back to github repository. Guidelines about .rst files, Writing Style and Markup Style are in the following pages.

Antônio Froz (uayten)

Denis Nicolas (denicolas)

Guilherme Teres Nunes (UnidayStudio)

Joel Gomes da Silva (joelgomes1994)

Jorge Bernal (lordloki)

Tristan Porteries (panzergame)

Ulysse Martin (youle31)

Xavier Cho (mysticfall)

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (julia):
```julia
.. highlight:: rst
```

Example 2 (julia):
```julia
.. highlight:: rst
```

---

## Contribute

**URL:** https://upbge.org/docs/latest/manual/manual/contribute/index.html

**Contents:**
- Contribute

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Controllers

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/controllers/index.html

**Contents:**
- Controllers
- Controller Types

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Controller Editing

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/controllers/editing.html

**Contents:**
- Controller Editing
- Column Heading
- Controllers
- Object Heading
- Standard Controller Parts

Controller Column with a typical sensor

UPBGE controllers can be set up and edited in the central column of the Logic Bricks Panel. This page describes the general column controls, those parameters which are common to all individual controller types, and how different states for the objects in the logic system can be set up and edited.

The image shows a typical controller column with a single controller. At the top of this column, and for sensors and actuators, the column heading includes menus and buttons to control which of all the controllers in the current Game Logic are displayed.

Controller Column headings

The column headings contain controls to set which controllers appear, and the level of detail given, in the controller column. This is very useful for hiding unnecessary controllers so that the necessary ones are visible and easier to reach. Both these can be controlled individually.

Collapses all objects to just a bar with their name.

Expands all Controllers.

Collapses all Controllers to bars with their names.

It is also possible to filter which controllers are viewed using the three heading buttons:

Shows all controllers for selected objects.

Shows only controllers belonging to the active object.

Shows controllers which have a link to actuators/sensors.

In the column list, controllers are grouped by object. By default, controllers for every selected object appear in the list, but this may be modified by the column heading filters.

At the head of each displayed object controller list, three entries appear:

Shows which states are in use for the object (toggle). Detailed description of the marked panel is given in States.

The name of the object.

When clicked, a menu appears with the available controller types. Selecting an entry adds a new controller to the object. See Controllers for a list of available controller types.

The controller heading is standard to every controller.

Collapses the sensor information to a single line (toggle).

Specifies the type of the controller.

The name of the controller. This can be selected by the user. It is used to access controllers with Python; it needs to be unique among the selected objects.

If on, this controller will operate before all other non-preference controllers (useful for start-up scripts).

Move the sensor up or down over other sensors within the column.

When unchecked the controller is deactivated, no pulses will be sent to the connected actuators. Very useful to check different logics without unlink or delete the controller.

Deletes the controller.

Sets the designated state for which this controller will operate.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Controller Status

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/bricks/controller_status.html

**Contents:**
- Controller Status
- Inputs
- Outputs

Which Object to inspect.

Which Controller to inspect.

Resulting status of the controller.

Resulting sensors of the controller.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Copy Property From Object

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/copy_property_from_object.html

**Contents:**
- Copy Property From Object
- Parameters
- Inputs
- Outputs

Selected property mode.

If connected, condition must be fulfilled for node to activate.

Which object to copy from.

To which object to copy.

String representation of the property to copy.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Create Button

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/widgets/create_button.html

**Contents:**
- Create Button
- Parameters
- Inputs
- Outputs

Create an interactive button.

Widget horizontal alignment

Widget vertical alignment

Text horizontal alignment.

Text vertical alignment.

If connected, condition must be fulfilled for node to activate.

If connected, the created widget will be added as a child to this parent.

If enabled, position will use a factor value (0-1) instead of pixels.

X and Y position of this Widget.

If enabled, Size will use a factor value (0-1) instead of pixels.

Width and Height of this Widget.

Button color in normal state.

Button color when mouse is hovering over.

Width of border line, in pixels.

Color of border line.

Text displayed on top of the button.

Text position in local button coordinates.

Graphical font to use for the button text.

Display size for the text.

Line spacing in factor (1.5 = 1.5 x Font Size).

Color of the button text.

True if node performed successfully, else False.

True when Button is clicked.

True when cursor is hovering over this widget.

True when Button was clicked and is released again.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Create Canvas

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/create_canvas.html

**Contents:**
- Create Canvas
- Parameters
- Outputs

If checked, canvas will be created on game initialization.

True if node performed successfully, else False.

Resulting canvas data. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Create Image

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/widgets/create_image.html

**Contents:**
- Create Image
- Parameters
- Inputs
- Outputs

Widget horizontal alignment

Widget vertical alignment

If connected, condition must be fulfilled for node to activate.

If connected, the created widget will be added as a child to this parent.

X and Y position of this Widget.

If enabled, Size will use a factor value (0-1) instead of pixels.

Width and Height of this Widget.

Path to the image to use.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Create Label

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/widgets/create_label.html

**Contents:**
- Create Label
- Parameters
- Inputs
- Outputs

Text horizontal alignment

Text vertical alignment

If connected, condition must be fulfilled for node to activate.

If connected, the created widget will be added as a child to this parent.

If enabled, position will use a factor value (0-1) instead of pixels.

X and Y position of this Widget.

Text content as string.

Graphical font to use for the text.

Display size for the text.

Line spacing in factor (1.5 = 1.5 x Font Size).

Color to use for font.

If checked, text will drop a shadow on background.

Offset of the drop shadow in pixels.

Color of the shadow drawn behind the text.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Create Layout

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/widgets/create_layout.html

**Contents:**
- Create Layout
- Parameters
- Inputs
- Outputs

Selected layout type.

Widget horizontal alignment

Widget vertical alignment

If connected, condition must be fulfilled for node to activate.

If connected, the created widget will be added as a child to this parent.

If enabled, position will use a factor value (0-1) instead of pixels.

X and Y position of this Widget.

If enabled, Size will use a factor value (0-1) instead of pixels.

Width and Height of this Widget.

Background color of this widget.

Width of border line, in pixels.

Color of border line.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Create New Vehicle

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/vehicle/create_new_vehicle.html

**Contents:**
- Create New Vehicle
- Inputs
- Outputs

Attaches a vehicle constraint to an object. This object will become the collider for the vehicle.

This node needs a specific object setup to work correctly. A vehicle needs to be ceated only once, otherwise the vehicle control nodes won’t be able to address the correct constraint. Of course, there must be the collider object. This will be the object executing the tree. Parented directly to this collider must be all the wheels.

The wheels must follow a naming convention:

If FWheel appears somewhere in the wheels name, it will be a front mounted wheel.

If RWheel appears somewhere in the wheels name, it will be a rear mounted wheel.

Wheels will be mounted in the position they are placed at, but the difference is that vehicle control nodes can be targeted to either front, rear or all wheels, which are accessed differently.

The collider may have any number of wheels. It may also have other children, as everything not named FWheel or RWheel will be ignored.

The node will return a vehicle constraint which can be used to drive the vehicle or modify its attributes. This constraint will also be automatically saved to the collider object and can be accessed via:

If connected, condition must be fulfilled for node to activate.

Object that will act as collider for vehicle.

Vehicle suspension height.

Vehicle suspension stiffness, will determine how much vehicle wiggles.

The rate at which suspension activity will subside.

The grip of the wheel. Pavement would be a higher value than mud.

True if node performed successfully, else False.

A vehicle constraint.

A list of wheel objects.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (csharp):
```csharp
# obj is the collider object
vehicle_constraint = obj['_vconst']
```

Example 2 (csharp):
```csharp
# obj is the collider object
vehicle_constraint = obj['_vconst']
```

---

## Create Path

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/widgets/create_path.html

**Contents:**
- Create Path
- Parameters
- Inputs
- Outputs

Draw the path in screen or world coordinates.

If connected, condition must be fulfilled for node to activate.

If connected, the created widget will be added as a child to this parent.

If enabled, position will use a factor value (0-1) instead of pixels.

X and Y position of this Widget.

If enabled, each point in Points will use a factor value for its position (0-1) instead of pixels.

Color to draw the line with.

Width of Path line, in pixels.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Create Slider

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/widgets/create_slider.html

**Contents:**
- Create Slider
- Parameters
- Inputs
- Outputs

Selected slider type.

Selected slider orientation.

Widget horizontal alignment

Widget vertical alignment

If connected, condition must be fulfilled for node to activate.

If connected, the created widget will be added as a child to this parent.

If enabled, position will use a factor value (0-1) instead of pixels.

X and Y position of this Widget.

If enabled, Size will use a factor value (0-1) instead of pixels.

Width and Height of this Widget.

Width of the slider bar.

Color of the slider bar.

Slider color when in mouse-over state.

Size of the control knob (only on some slider types).

Color of the knob when in mouse-over state.

If step functionality is required, i.e. slider moves by value of 10-20-30 etc. 0 (zero) will enable smooth value changing.

If checked, clicking on the bar has the same effect as clicking on the knob.

True if node performed successfully, else False.

Current slider value.

Knob position in pixel screen coordinates.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Cursor Visibility

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/mouse/cursor_visibility.html

**Contents:**
- Cursor Visibility
- Inputs
- Outputs

Used to set the visibility status of the system mouse cursor.

If connected, condition from connected node must be fulfilled for node to activate.

Target state for the system cursor.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Curves

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/curves/index.html

**Contents:**
- Curves

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Curve Interpolation

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/curve_interpolation.html

**Contents:**
- Curve Interpolation
- Inputs
- Outputs

Curve node enables advanced value manipulation, via curve points:

LMB-select a point, below the graph is a row with point settings - click X to delete.

LMB-drag the point to desired location on graph.

In a row below the graph, click-select icon to change handle type, or change position values (X Y coordinates) for selected point.

Above the graph are option icons - zoom in/out, use Clipping (will clamp output values between 0 and 1), use dropdown menu to Reset View, Reset Curve etc.

Input float value for curve interpolation.

Resulting interpolated value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Custom

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/events/custom/index.html

**Contents:**
- Custom

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Data

**URL:** https://upbge.org/docs/latest/manual/manual/editors/properties/data.html

**Contents:**
- Data

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Data-Blocks

**URL:** https://upbge.org/docs/latest/manual/manual/datablocks/index.html

**Contents:**
- Data-Blocks
- Data-Block Types
  - Object-related Datablocks
  - File-related Datablocks
  - Other Datablocks
- Life Time
  - Protected
- Sharing
- Making Single User
- Removing Data-Blocks

This page is based on Blender Manual Data-blocks. Please see the link for additional details.

The base unit for any Blender project is the data-block. Examples of data-blocks include mesh, object, material, texture, node tree, scene, text, brush, and even workspaces.

Blender File mode in Outliner

A data-block is a generic abstraction of very different kinds of data, which features a common set of basic features, properties and behaviors.

Some common characteristics:

They are the primary contents of the blend-file.

They can reference each other, for reuse and instancing (child/parent, object/object-data, materials/images, in modifiers or constraints too …).

Their names are unique within a blend-file, for a given type.

They can be added/removed/edited/duplicated.

They can be linked between files (only enabled for a limited set of data-blocks).

They can have their own animation data.

They can have custom properties.

User will typically interact with the higher level data types (objects, meshes etc.). When doing more complex projects, managing data-blocks becomes more important, especially when inter-linking blend-files. The main editor for that is the Outliner Editor.

Data-block types with their icons

Not all data in Blender is a data-block; i.e. bones, sequence strips or vertex groups are not - they belong to armature, scene and mesh types respectively.

For reference, here is a table of data-block types stored in blend-files.

Library Linking, supports being linked into other blend-files.

File Packing, supports file contents being packed into the blend-file (not applicable for most data-blocks which have no file reference).

A table-representation of data-blocks supported in UPBGE.

Shift-scroll over the table if text is cut/hidden.

Skeleton used to deform meshes; used as data of armature objects, and by the Armature Modifier

Used as data by camera objects

Group and organize objects in scenes; used to instance objects, and in library linking

Used as object data by light objects

Geometry made of vertices/edges/faces; used as data of mesh objects

An entity in the scene with location, scale, rotation; used by scenes & collections

Text data; used by Python scripts and OSL shaders

Image files; used by shader nodes and textures

References to an external blend-file; access from the Outliner’s Blender File view

Reference to sound files; used as data of speaker objects

Stores animation F-Curves; used as data-block animation data, and the Nonlinear Animation editor

Set shading and texturing render properties; used by objects, meshes & curves

Primary store of all data displayed and animated; used as top-level storage for objects & animation

2D/3D textures; used by brushes and modifiers

Define global render environment settings

Every data-block has its usage counted (reference count) - when there is more than one, you can see the number of current users of a data-block to the right of its name in the interface. Blender follows the general rule that unused data is eventually removed.

Since it is common to add and remove a lot of data while working, this has the advantage of not having to manually manage every single data-block. This works by skipping zero user data-blocks when writing blend-files.

Protected (blue shield) data-block

Since zero user data-blocks are not saved, there are times when you want to force the data to be kept irrespective of its users.

If you are building a blend-file to serve as a library of assets that you intend to link to and from other files, you will need to make sure that they do not accidentally get deleted from the library file.

To protect a data-block, use the button with the shield icon next to its name. The data-block will then never be silently deleted by Blender, but you can still manually remove it if needed.

Data-blocks can be shared among other data-blocks.

Examples where sharing data is common:

Sharing textures among materials.

Sharing meshes between objects (instances).

Sharing animated actions between objects, for example to make all the lights dim together.

You can also share data-blocks between files.

When a data-block is shared between several users, you can make a copy of it for a given user. To do so, click on the user count button to the right of its name (number 43 in above image). This will duplicate that data-block and assign the newly created copy to that usage only.

Objects have a set of more advanced actions to become single-user.

As covered in Life Time, data-blocks are typically removed when they are no longer used. They can also be manually unlinked or deleted.

Unlinking a data-block means that its user won’t use it anymore. This can be achieved by clicking on the X icon next to a data-block’s name (see above image). If you unlink a data-block from all of its users, it will eventually be deleted by Blender as described above (unless it is a protected one).

Deleting a data-block directly erases it from the blend-file, automatically unlinking it from all of its users. This can be achieved by Shift-LMB on the X icon next to its name.

Deleting some data-blocks can lead to deletion of some of its users, which would become invalid without them. The main example is that object-data deletion (like mesh, curve, camera …) will also delete all objects using it.

Those two operations are also available in the context menu when RMB-clicking on a data-block in the Outliner.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Data

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/index.html

**Contents:**
- Data

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Dealing With Group Instances

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_python_scripting/group_instances.html

**Contents:**
- Dealing With Group Instances
- Setup
- Spawning Script
- Advanced Usage

Learn to dynamically spawn and manage group instances.

Create a group named “Projectile”

Make sure it has a Rigid Body setup

Add Always + Python Controller

Object pooling for better performance

Damage system on collision

Particle trail effects

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (python):
```python
import bge
from random import uniform

def spawn_projectiles(scene, owner):
    if bge.logic.keyboard.events[bge.events.SPACEKEY] == bge.logic.KX_INPUT_ACTIVE:
        # Random position near spawner
        pos = [uniform(-2, 2), uniform(-2, 2), 3]

        # Create instance
        new_obj = scene.addObject("Projectile", owner, 0)
        new_obj.worldPosition = pos

        # Apply physics force
        new_obj.applyForce([0, 0, -50], local=False)

scene = bge.logic.getCurrentScene()
controller = bge.logic.getCurrentController()
owner = controller.owner
spawn_projectiles(scene, owner)
```

Example 2 (python):
```python
import bge
from random import uniform

def spawn_projectiles(scene, owner):
    if bge.logic.keyboard.events[bge.events.SPACEKEY] == bge.logic.KX_INPUT_ACTIVE:
        # Random position near spawner
        pos = [uniform(-2, 2), uniform(-2, 2), 3]

        # Create instance
        new_obj = scene.addObject("Projectile", owner, 0)
        new_obj.worldPosition = pos

        # Apply physics force
        new_obj.applyForce([0, 0, -50], local=False)

scene = bge.logic.getCurrentScene()
controller = bge.logic.getCurrentController()
owner = controller.owner
spawn_projectiles(scene, owner)
```

Example 3 (python):
```python
import bge
from random import uniform

def spawn_projectiles(scene, owner):
    if bge.logic.keyboard.events[bge.events.SPACEKEY] == bge.logic.KX_INPUT_ACTIVE:
        # Random position near spawner
        pos = [uniform(-2, 2), uniform(-2, 2), 3]

        # Create instance
        new_obj = scene.addObject("Projectile", owner, 0)
        new_obj.worldPosition = pos

        # Apply physics force
        new_obj.applyForce([0, 0, -50], local=False)

scene = bge.logic.getCurrentScene()
controller = bge.logic.getCurrentController()
owner = controller.owner
spawn_projectiles(scene, owner)
```

---

## Delay

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/time/delay.html

**Contents:**
- Delay
- Inputs
- Outputs

Wait a certain time between the reception of True and the output of True.

If connected, condition must be fulfilled for node to activate.

Delay in seconds until the node set it output to True.

True one frame after the condition input has been fulfilled and the Delay has elapsed, else False.

Delay will handle muliple inputs at the same time and will stack them, unlike the Timer node. For example, if you connect a Keyboard key node to a Delay set to 5 seconds and press the key a first time and then 2 seconds later you press the key again, Delay will output True 5 seconds after the first key press and another one time True at 7 seconds, unlike Timer.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Delay Sensor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/types/delay.html

**Contents:**
- Delay Sensor
- Properties
- Example

See the Python reference of this logic brick in SCA_DelaySensor.

The Delay Sensor is designed for delaying reactions a number of logic ticks. This is useful if an other action has to be done first or to time events.

See Sensor Common Options for common options.

The number of logic ticks the sensor waits before sending a positive pulse.

The number of logic ticks the sensor waits before sending the negative pulse.

Makes the sensor restart after the delay and duration time is up.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Delta Factor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/time/delta_factor.html

**Contents:**
- Delta Factor
- Outputs

Return the delta factor, a normalized multiplier based on the ratio between the actual number of FPS and the target number of FPS (the number of FPS the logic is runnig at).

Delta Factor between the actual number of FPS and the number of FPS used by the logic (Float). Used to dissociate logic and framerate, to maintain the same speed for actions managed by logic even with an unlimited number of FPS. For example, used to calculate the walk speed of a character.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Deployment

**URL:** https://upbge.org/docs/latest/manual/manual/deployment/index.html

**Contents:**
- Deployment

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Deployment Procedure

**URL:** https://upbge.org/docs/latest/manual/manual/deployment/release_procedure.html

**Contents:**
- Deployment Procedure

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Dictionary From Items

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/dict/dictionary_from_items.html

**Contents:**
- Dictionary From Items
- Inputs
- Outputs

Name for dictionary key.

Type and value to be paired with matching key.

Dictionary will be created and its data passed out. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Dict

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/dict/index.html

**Contents:**
- Dict

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Draw

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/utility/draw.html

**Contents:**
- Draw
- Parameters
- Inputs
- Outputs

If checked/connected, condition must be fulfilled for node to activate.

Which color to use for drawing.

Starting point of the shape to be drawn.

End point of the shape. todo

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Duplicate

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/list/duplicate.html

**Contents:**
- Duplicate
- Inputs
- Outputs

Duplicate a list in order to do changes on it without altering the original list.

Which list to duplicate.

Resulting duplicated list.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Editors

**URL:** https://upbge.org/docs/latest/manual/manual/editors/index.html

**Contents:**
- Editors

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## EEVEE

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/eevee/index.html

**Contents:**
- EEVEE

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Euler

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/vector/euler.html

**Contents:**
- Euler
- Parameters
- Inputs
- Outputs

Accepts float inputs and combines them into Euler angle.

Selected order of vectors.

Fixed input X value, or result from connected node.

Fixed input Y value, or result from connected node.

Fixed input Z value, or result from connected node.

Resulting Euler angle.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Evaluate Object Property

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/evaluate_object_property.html

**Contents:**
- Evaluate Object Property
- Parameters
- Inputs
- Outputs

Selected property mode.

Type of selected operation to perform.

Name of property to modify.

Selected type of evaluated property.

Resulting evaluated value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Events

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/events/index.html

**Contents:**
- Events

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Extend

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/list/extend.html

**Contents:**
- Extend
- Inputs
- Outputs

Extend (concatenate) one list with another.

List to be extended. This list will be placed first in the output list.

List to use for extending. This list will be placed just after List 1 in the output list.

A new list made by concatenating List 1 and List 2.

If you give List 1 [1, 2, 3, 4] and List 2 [5, 6, 7, 8, 9, 10], the output will be the list [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## File

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/file/index.html

**Contents:**
- File

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## File Path

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/file_path.html

**Contents:**
- File Path
- Inputs
- Outputs

Enter the path or click the Folder icon to open popup window, and navigate to the required file.

Resulting path to file.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## First Person Camera

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_bricks/first_person_camera.html

**Contents:**
- First Person Camera
- Camera

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## First Person Shooter

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_nodes/first_person_shooter.html

**Contents:**
- First Person Shooter

In this tutorial we will:

Open .blend file with level assets - barrels and cubes, a brick walls, and a player with camera;

Use Logic Nodes to add W S A D movement and a jump with some extras;

Upgrade with Logic Nodes into a FPS game;

Placement options for Annotation tool

We will also learn few handy shortcuts on-the-go. Shall we?

Download/open level with assets .blend file. Follow the instructions precisely. :)

Shift-Space > D for on-screen scribble tool, called Annotation in blenderland.

Annotation tool is useful for quick sketch, storyboard, and transferring ideas to collaborators. Also for annotations. He he he. Try all three Placement options for Annotation tool, rotate 3D viewport in-between, to see different placements of your scribbles. Go to N-panel > View > Annotations and select individual colors to be able to erase them. Or click X to delete all at once quickly.

Ok, enough chit-chat - let’s fight!

Player as parent of many children

In Outliner Editor top > search for Player.

Take a look of the level objects, particularly the hierarchy of Player object. Below Player object there is a bunch of other objects, being a children of Player, our main Parent object. Wherever Player goes, all children will follow. Also take a look at Properties Editor - under Object tab (orange square) there are Relations and Collections sub-panels, and close to the bottom, a Viewport Display sub-panel - under Display As a Wire is selected, and this is why Player looks underfed, sorry, wireframed. Since during the gameplay the Player is actually not visible, this will save some computer power. Not much though. :)

Of our main interest is a Head object, which is of type Empty object - those are commonly used as Parent object. In our case, Head is a parent of Camera object - this is the “eyes” of our player. No camera - no image on our screen.

Next, under the Camera, there is a Gun object, and this one has an Animation object with Action assigned to it.

Those are main building blocks of the game development, which we will incorporate into Logic Nodes workflow. Let the party begin!

Delete Text object (it was showing > W to exit Annotation tool), we do not need it. Switch to Logic Nodes workspace (top-most header). Arrange the editors as you see fit, the one we will use most is Logic Node Editor.

Both game and 3D model development require use of multiple editors at once. This can clutter the screen, particularly small one, quickly. To remedy this, few workflows are at our disposal.

Dedicate each workspace, like default Blender startup file. In this case there are workspaces, which can be switched by clicking top-most header, in our example:

Layout | Logic Nodes | Animation | Scripting

There is also + tab, if you want to add another workspace. And you can assign hotkeys for switching previous/next workspace: Edit > Preferences > Keymap - search for Screen > Cycle Workspace. Assign 2 keyboard keys, one for previous and one for next workspace.

I trust you can figure out how to delete a workspace by yourself.

Use Blender/UPBGE handy shortcut, Ctrl-Space, which will toggle-maximize the editor window under the mouse cursor. This was a preferred workflow of now late Johnny Maccarony, world-known heavy consumer of Logic Node noodles.

In Logic Node Editor, first create new logic tree, click Logic Node Editor, rename to player, and mark Protected (Fake User); next add basic movement nodes, same as for Moving A Cube chapter.

Add 5 Keyboard Key nodes, assign D A W S keys for right/left and forward/backward movement, and Space for jumping.

Add 2 Math nodes and connect with above 4 movement nodes.

Add Apply Force node, connect remaining Keyboard Key node If Pressed output socket to Condition input socket, add Player as object, set vector Z (up/down axis) to 200.0 - this much force will be applied. Local ? Judge yourself, or use time-tested very successful procedure - trial & error. Lucky you, just 2 options are available.

Add Combine XYZ node, connect above Math nodes. Leave Z at default 0.0 value.

Add Vector Math node, set to Normalize, connect those 2 cute blue-ish dots.

Add another Vector Math node, set Operation to Scale. This node will determine speed of the Player. Connect Result from above node to Vector 1 input socket.

If you want nodes to be aligned, turn on magnet icon in top-right corner of Logic Node Editor, above N-panel. Nodes will now snap to invisible grid. Hotkey is Shift-Tab.

Add Game Property and Apply To Selected

Before we continue with nodes, we need to add Game Property. With Player selected:

In Properties > Game > Game Properties, click Add Game Property, name it speed, leave default Float type, and set value to 1.0.

Apply To Selected - this will create NL__player game property, player object tree, and a nl_player.py script. NL/nl stands for node logic.

Good job. Now we can continue with nodes.

Add Get Object Property node; if not already, select Game Property from dropdown, and in Property field type speed - this is the speed property that we just created above. Connect this node to Scale input socket of the last Vector Math node, and add Player as owner object - click Object and select from menu.

Add On Update and a Apply Movement node - connect Out to Condition, and last Vector Math into Vector; also set Player as object, and yes, check Local.

This is our node setup so far:

Player movement nodes setup so far

Another very useful Blender habit to grow - almost all buttons & commands have option to Add to Quick Favorites or Assign Shortcut:

Go to Properties > Render > Game Resolution;

Hover mouse over Embedded Start button, RMB and select Add to Quick Favorites.

Use this tip whenever you find yourself using/repeating same actions over and over. It is a great time saver.

Q for Quick Favorites > E for Start

According to the Holy Blender Bible, Embedded Start can be invoked with hotkey P, which seems to be not working in current UPBGE by default. So we added it into Quick Favorites, although we could as easily assign a P shortcut. We will now run game and test if node setup is working as expected. With mouse over 3D-Viewport:

Numpad 0 > Home > Q will move into ‘camera view’ > zoom-in/maximize/center the camera view > open Quick Favorites menu; there, another hotkey is offered for the Embedded Start - this depends on various factors, and is recognizable by any of the letters being underscored - E in figure; in your case might be something else. Pressing that key should start the game. Esc to end the game.

While the game is running, press movement keys and observe Player behavior.

First of all, it is moving way to fast > reduce the speed property; trial & error is the name of the game, until you find comfortable settings. Hint - halve the speed value for a start, and do not forget - Player should be selected in order to change its speed property.

Second of all, keys are wrong > fix them until character moves properly relative to pressed keys > W forward; S backward; A left; D right.

If you’re done fixing, let’s continue.

Add Mouse Look and connect Out from On Update to Condition, set Player as Object and Head as Head. Run the game, test, if needed, adjust settings in Mouse Look node: Cap Up/Down will limit Head movement, Smoothing will smooth mouse moves.

Next we upgrade walking to run:

Add/duplicate Keyboard Key & Math, add Value Switch. The logic here is:

When Shift is pressed, add some float value to speed, and use resulting value for movement;

If not pressed, use existing speed value.

Test the game, adjust values as you see fit.

Value Switch for running

Now it is time for some actions - we’ll add gun shooting. Switch to Animation workspace, in the left editor/window > top-right, check Shading options - little arrow at far right side will dropdown some setting, which you are free and advised to change.

With object selected, you can ‘focus’ it with Numpad , (comma); this works in 3D Viewport, Outliner, and other editors. Use this if you ‘loose’ the object from sight.

Action Editor context with action dots

Expand/enlarge bottom Dope Sheet Editor, select/expand Gun object (Outliner > Search if needed), and you shall see some orange dots in Dope Sheet - this is gun Action - when gun is fired, bullet pushes it back and up. Hit Space to toggle animation playing. We need to attach this action to Player and connect it with an input.

Switch Editing context from Dope Sheet to Action Editor - name of our action is shown in the header > Shot.

Back to Logic Nodes workspace (or modify workspace to include Logic Node Editor window/area). Add Mouse Button, Pulsify, Stop Animation and Play Animation nodes, connect them red-to-red dot.

Shot action is how long? Set Play Animation to Object > Gun, and Action > Shot, End > last action frame. Test the game, adjust settings.

Gun is moving when shooting now, but still needs to actually shoot something. And the sound is missing.

Add below Active Camera, Get World Position, and Get Axis Vector - connect Camera to both Get World Position > Object, and Get Axis Vector > Object, set Axis > -Z Axis (object/player forward-facing direction).

Get Axis Vector will take Active Camera orientation and feed it to Raycast for aiming direction.

Get World Position will take Active Camera (player body/head) position and feed it to Raycast as shooting origin point/position.

Add Raycast, connect Get World Position > Origin, Get Axis Vector > Aim, and above Stop Animation > Condition, check Custom Distance and Local.

Add Apply Impulse, connect Raycast top two output sockets color-to-color, and Picked Point > Vector, Ray Direction > Direction.

Add Draw node, set to Cube, connect Apply Impulse > Condition, Raycast Picked Point > Origin, set Width to something small, i.e. 0.02, and check Use Volume Origin.

Cube will act as improvised bullet. In final game this bullet would probably best be hidden.

Done - test and adjust settings.

Shot audio clip node

Search/download ‘machine gun shot single audio’, a short sound clip, save to disk, somewhere close to our working .blend file.

Next to above Play Animation add Start Sound, set as 2D Sample, connect Play Animation Started > Condition, Sound attribute > folder icon > load shot audio clip, note icon > load from dropdown. Test the game, take a break.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Float

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/float.html

**Contents:**
- Float
- Parameters
- Inputs
- Outputs

Selected data type -floating number value.

Either fixed float value or result from socket, if connected.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## FMod

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/sound/fmod/index.html

**Contents:**
- FMod

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Follow Path

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/follow_path.html

**Contents:**
- Follow Path
- Input
- Output

Select an object to move through the points of a Nurbs Curve. Only works in conjunction with Get Curve Points. Use on NPCs that need to walk around.

The condition for this node to start.

Object that will be moved.

Object that will rotate when changing direction.

Use in combination with Get Curve Points node.

Selected: after arriving at the position of the last curve point, the object will return to the start of the displacement.

Unselected: The object will end the displacement at the last curve point.

If there is a boundary in the area where the object travels, select the Navigation Mesh.

Dynamic objects give and receive collisions, so other objects can dynamically affect the trajectory of the Moving Object. See Dynamic for more info.

Linear speed of the object, basically the travelling speed.

Distance to the target it needs to count as arrived.

If selected, the front of the object will observe the direction of displacement.

Speed at which the object will move sideways when making a change of direction.

When the object makes a change of direction, on which axis will rotate.

Which axis is the front of the object.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Formatted String

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/formatted_string.html

**Contents:**
- Formatted String
- Inputs
- Outputs
- Example

Fixed string format, or result from connected socket.

Resulting string formated from all input strings.

Above setup will pull text values from two String nodes, format them through Formatted String, and print the resulting string into console, on LMB click. Additional inputs can be added with {} string - inputs will be added automatically.

Printed resulting string in System Console

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Formula

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/formula.html

**Contents:**
- Formula
- Parameters
- Inputs
- Outputs

Will perform mathemathical calculations, according to Formula input. There are numerous predefined mathemathical formulas to choose from dropdown menu. Enjoy. :)

Predefined mathematical formulas for calculations. Includes User Defined option.

String representation of mathematical formula for calculation.

First operator value.

Second operator value.

Resulting value of math operation.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Gamepad

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/gamepad/index.html

**Contents:**
- Gamepad

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Gamepad Active

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/gamepad/gamepad_active.html

**Contents:**
- Gamepad Active
- Inputs
- Outputs

Detects if the controller at given index has any activity.

The controller index to monitor.

True if the controller has activity, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Gamepad Button

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/gamepad/gamepad_button.html

**Contents:**
- Gamepad Button
- Parameters
- Inputs
- Outputs

Detects if a specified button has been pressed on the controller at given index.

Which button/trigger is monitored.

Input detection mode. Tap is activated the first frame that the key is pressed, Down is activated while the key is pressed and Up is activated once the last frame the key is pressed.

The controller index to monitor.

True if the button is active in the selected mode, else False.

Value of the trigger from 0 to 1. Only visible if button is LT/L2 or RT/R2.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Gamepad Look

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/gamepad/gamepad_look.html

**Contents:**
- Gamepad Look
- Parameters
- Inputs
- Outputs

A quick way to make objects follow controller stick movement. It’s possible to assign a Body and a Head object.

If no Head object is assigned, the Body will be used for both axis, but that is generally discouraged as it can lead to unwanted side effects.

Which stick of the controller to use for the transformation.

Input condition for node activaton.

Head object. If set, both objects will be rotated along their corresponding local axis.

Option to invert movement for each axis (Vector2).

The index of the controller to poll.

Multiplier for translating controller stick movement to object rotation.

Exponent for fine-tuning the stick behavior.

Limit the body objects rotation on its local Z axis.

The limits for the body object local Z rotation (Vec2). Visible if Cap Left/Right is selected.

Limit the head object rotation on its local X/Y axis.

Limits for the head object local X/Y rotation (Vec2). Visible if Cap Up/Down is selected.

Ignore stick values under this threshold. Used to avoid stick drift.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Gamepad Sticks

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/gamepad/gamepad_sticks.html

**Contents:**
- Gamepad Sticks
- Parameters
- Inputs
- Outputs

Detects stick values of the controller at given index.

Which stick values to read.

Checked axis will be inverted.

The controller index to monitor.

Multiplier for the axis values.

Dead-zone for the stick. Used to avoid stick drift.

Stick values as vector (X, Y, 0) (Vector3).

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Gamepad Vibrate

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/gamepad/gamepad_vibrate.html

**Contents:**
- Gamepad Vibrate
- Inputs
- Outputs

Detects if the controller at given index has any activity.

Condition that need be fulfilled to activate the node.

The controller index to vibrate.

Force with which to rotate the weight in the left handle.

Force with which to rotate the weight in the right handle.

How many seconds the vibration has to play.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Game

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/game/index.html

**Contents:**
- Game

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Game Basic Concepts

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/getting_started/game_basic_concepts.html

**Contents:**
- Game Basic Concepts
- Game
  - Game Loop
  - Scene Loop
  - Logic Ticks

So far, we have talked about 3D at length. But how does the game engine fit into? Well, a game engine simply takes the existing 3D assets and attaches a “brain” to them so the objects know how to respond to events. The “brain” can be in the form of logic bricks (which can perform different actions depending on the user input), scripts (which can extend the functionality of logic bricks), or other physical properties of an object (such as rigid body settings to make an object tumble and fall realistically).

Object + logic = game

A game engine is made up of many distinct components:

Rendering Engine - turns the 3D scene you’ve built (including models, lights, and camera) into an image to be displayed onscreen.

Physics - handles collisions and physical simulations of objects.

Logic/Scripting - the brain behind a game, it reacts to the user input, makes decisions, and keeps track of what’s going on in the game.

Sound - produces the audio events.

The above list is not meant to be exhaustive, but it should give you an idea of what a game engine does. The Blender game engine gives you a lot of control over each of these components, which you will learn one by one in later chapters.

Quality vs. Performance

Making a video game is a constant balancing act between quality and performance. As artists, you want to make the virtual world as rich and detailed as possible; on the other hand, you need to make sure the game can run smoothly for people who might not have top-of-the-line computers. Throughout the process of game-making, you will run into cases where you have to make a decision whether to prioritize the visual quality or the performance of the game. You will also learn tricks to achieve high-quality visual without compromising the performance, as well as how to optimize the game by identifying what is slowing it down.

The game loop is something that every game or general software has: it consists of several processing steps and then, repeating it. To make it clear, think of a video player processing steps:

It reads a portion of the video file from disk.

It decodes the read file portion into a image.

It shows the decoded image in the screen as a single frame.

It repeats everything from the start.

Nevertheless, this article will present you how the game loop is built in UPBGE. It is essential to know how it works: if you keep that in mind, it will explain a lot of mysterious behavior that you might discover.

Each cycle in the game loop represents a logical frame, also known as logic tick. It is the smallest time unit within your game. In each loop:

The scenes are processed.

The devices are checked for input.

The final image is rendered.

It is important to know that the render part might be skipped if the last frame was spending too much processing time , resulting in lag. There is a limit on how much renders can be skipped (default = 5). If this limit exceeds, a render will take place regardless how long it takes. Such ‘render’ lags will result in ‘logic’ lags, making the game run slower than expected.

This loop is a bit more complex. The scenes loop cycles through all active scenes performing the following steps for each scene:

This first step processes the logic of the game, be it visual or Python.

The physics update will be done after the logic runs, but before the render is drawn.

The sound playing is put in the last step of the scene loop.

Once all these steps are taken for all active scenes, the main loop continues.

The logic processing works through frames called logic ticks. By default, a game running at 60 frames per second also can run 60 logic ticks per second. In practical examples:

If I have a number 0 and increase it by 1 each frame, after 1 second its value will be 60.

If I have an object and move it 0.1 meters each frame, after 1 second it should have been moved 6 meters.

In UPBGE you can control the logic tick intervals for each object by skipping a given ammount of ticks, allowing you to run logic at exact custom time intervals or optimize logic which doesn’t need to run each frame. The following diagram shows how logic tick skipping work.

Logic tick skipping diagram

In the given diagram, where dark red is logic execution and grey is a interval:

No ticks skipped between logic ticks, the logic runs each game frame.

Skipping of 2 ticks between each logic execution.

Skipping of 6 ticks between each logic execution.

To understand how the game loop and logic triggering works is important for you to shape the way your logic will be made and understand internal behaviors that UPBGE may show.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Gate

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/gate.html

**Contents:**
- Gate
- Parameters
- Inputs
- Outputs

Resulting gate operation between A and B.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Gate List

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/gate_list.html

**Contents:**
- Gate List
- Parameters
- Inputs
- Outputs

Add a socket to list.

Resulting value from gate operation.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Geometry

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/geometry/index.html

**Contents:**
- Geometry

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Getting Started

**URL:** https://upbge.org/docs/latest/manual/manual/python_components/getting_started/index.html

**Contents:**
- Getting Started

This subchapter aims to show the basic Python Component templates included in UPBGE, from the character controller movements to the most common operations used in game development. This will give you important information on how to use the reusable components, included in the UPBGE, in all your games.

The Python Component templates are included under the template option in the script editor.

Python Component template list

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Getting Started

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/getting_started/index.html

**Contents:**
- Getting Started

This tutorial aims to show the basic concepts of UPBGE, from the game loop behavior to the most common operations used in game development. This will give you important notions on how UPBGE works and how are its procedures.

Keep in mind that the focus of this tutorial are UPBGE and its game engine behavior, although basic Blender navigation (like selection, shortcuts, etc.) and panels will be explained.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Actuator Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/bricks/get_actuator_value.html

**Contents:**
- Get Actuator Value
- Inputs
- Outputs

Which object to inspect.

Which actuator to inspect.

Which field to inspect.

Resulting actuator value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Attribute

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/index.html

**Contents:**
- Get Attribute

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Axis Vector

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/object_data/get_axis_vector.html

**Contents:**
- Get Axis Vector
- Parameters
- Inputs
- Outputs

Selected axis to get.

Which object to inspect for axis vector.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Child By Index

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_child_by_index.html

**Contents:**
- Get Child By Index
- Inputs
- Outputs

A parent object of a child object which to inspect.

Resulting data of the child object.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Child By Name

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_child_by_name.html

**Contents:**
- Get Child By Name
- Inputs
- Outputs

A parent object of the child object to inpect.

A child object to inspect.

Resulting child object data.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Collection

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/collections/get_collection.html

**Contents:**
- Get Collection
- Inputs
- Outputs

Resulting collection data.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Color

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_color.html

**Contents:**
- Get Color
- Parameters
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Curve Points

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/curves/get_curve_points.html

**Contents:**
- Get Curve Points
- Inputs
- Outputs

Which curve to inspect for points.

A list of resulting curve points.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Dictionary Key

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/dict/get_dictionary_key.html

**Contents:**
- Get Dictionary Key
- Inputs
- Outputs

Which dictionary to use.

Which key to search for.

If default value is to be used. todo

Resulting value matching the input conditions.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Font

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/file/get_font.html

**Contents:**
- Get Font
- Inputs
- Outputs

Font to get. Load with Folder icon and select/set from selection menu.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Fullscreen

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/get_fullscreen.html

**Contents:**
- Get Fullscreen
- Outputs

True if Fullscreen is enabled, else False. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Global Property

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/get_global_property.html

**Contents:**
- Get Global Property
- Inputs
- Outputs

Name of the property to get.

Resulting retrieved value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Image

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/file/get_image.html

**Contents:**
- Get Image
- Inputs
- Outputs

Image to get. Load with Folder icon and select/set from selection menu.

Resulting image data.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Instance Attribute

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/python/get_instance_attribute.html

**Contents:**
- Get Instance Attribute
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Light Color

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/lights/get_light_color.html

**Contents:**
- Get Light Color
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Light Power

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/lights/get_light_power.html

**Contents:**
- Get Light Power
- Inputs
- Outputs

Resulting strength of the light.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get List Index

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/list/get_list_index.html

**Contents:**
- Get List Index
- Inputs
- Outputs

Retrieve value at specified index of the list.

Resulting value at index from list.

The list index start at 0, so for example, in the list [4, 2, 5, 8, 9], if you retrieve the value at index 4, the node output will be 9.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Local Angular Velocity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_local_angular_velocity.html

**Contents:**
- Get Local Angular Velocity
- Parameters
- Inputs
- Outputs

Local Angular Velocity

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Local Linear Velocity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_local_linear_velocity.html

**Contents:**
- Get Local Linear Velocity
- Parameters
- Inputs
- Outputs

Local Linear Velocity todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Local Orientation

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_local_orientation.html

**Contents:**
- Get Local Orientation
- Parameters
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Local Position

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_local_position.html

**Contents:**
- Get Local Position
- Parameters
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Local Scale

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_local_scale.html

**Contents:**
- Get Local Scale
- Parameters
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Local Transform

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_local_transform.html

**Contents:**
- Get Local Transform
- Parameters
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Master Folder

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/path/get_master_folder.html

**Contents:**
- Get Master Folder
- Inputs
- Outputs

Go up in directories until the directory name matches the given string.

Name of the folder to look for.

Full path to the directory. If no directory is found, an empty string is returned.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Name

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_name.html

**Contents:**
- Get Name
- Parameters
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Node

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/materials/get_node.html

**Contents:**
- Get Node
- Inputs
- Outputs

Which material to inspect.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Node Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/geometry/get_node_value.html

**Contents:**
- Get Node Value
- Inputs
- Outputs

Geometry node to inspect.

String representation of node name.

Resulting node value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Node Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/materials/get_node_value.html

**Contents:**
- Get Node Value
- Inputs
- Outputs

String representation of node name.

Resulting node value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Node Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/groups/get_node_value.html

**Contents:**
- Get Node Value
- Inputs
- Outputs

Resulting node value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Objects

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/collections/get_objects.html

**Contents:**
- Get Objects
- Inputs
- Outputs

Collection to get objects from.

A list of resulting objects.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Object

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_object.html

**Contents:**
- Get Object
- Inputs
- Outputs

Which object to inspect.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Object ID

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/object_data/get_object_id.html

**Contents:**
- Get Object ID
- Inputs
- Outputs

Which object to inspect.

Resulting ID of the object.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Object Names

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/collections/get_object_names.html

**Contents:**
- Get Object Names
- Inputs
- Outputs

Collection to get object names from.

A list of resulting object names.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Object Property

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/get_object_property.html

**Contents:**
- Get Object Property
- Parameters
- Inputs
- Outputs
- Example

Will get a property from selected object, if exists, and output it as a value.

Selected property mode.

Name of the property, either fixed, or result from connected node.

Resulting property value.

Get Object Property example

A game property is manually added, and accessed with Get Object Property node.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Parent

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_parent.html

**Contents:**
- Get Parent
- Inputs
- Outputs

A child object for which to get its parent.

Data of the resulting parent object.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Physics Info

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/character/get_physics_info.html

**Contents:**
- Get Physics Info
- Parameters
- Inputs
- Outputs

Which character object to use.

Max allowed jumps while character is in the air. todo

Current number of jumps.

Applied gravity. todo

Vector of walking direction. todo

If character is on ground, not jumping. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Random List Item

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/list/get_random_list_item.html

**Contents:**
- Get Random List Item
- Inputs
- Outputs

Randomly pick an item from a given list.

Which list to use for getting a random item.

A value of the random item from the list.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Resolution

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/get_resolution.html

**Contents:**
- Get Resolution
- Outputs

Resulting screen width. todo

Resulting screen height. todo

Current screen resolution. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Scene

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/get_scene.html

**Contents:**
- Get Scene
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Sensor Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/bricks/get_sensor_value.html

**Contents:**
- Get Sensor Value
- Inputs
- Outputs

Which object to inspect.

Resulting sensor value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Socket Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/groups/get_socket_value.html

**Contents:**
- Get Socket Value
- Inputs
- Outputs

Geometry node to use. todo

String representation of node name.

Resulting socket value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Socket Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/materials/get_socket_value.html

**Contents:**
- Get Socket Value
- Inputs
- Outputs

Resulting socket value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Socket Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/geometry/get_socket_value.html

**Contents:**
- Get Socket Value
- Inputs
- Outputs

Geometry node to inspect.

String representation of node name.

Resulting value for getting node socket.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Sound

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/file/get_sound.html

**Contents:**
- Get Sound
- Inputs
- Outputs

Sound File to get. If node is connected todo, else load with Folder icon and select/set from selection dropdown.

Resulting sound file.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Timescale

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/get_timescale.html

**Contents:**
- Get Timescale
- Outputs

Current timescale of the scene.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Tree Property

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/get_tree_property.html

**Contents:**
- Get Tree Property
- Inputs
- Outputs

Name of the tree to use.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Vertices

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/object_data/get_vertices.html

**Contents:**
- Get Vertices
- Inputs
- Outputs

Which object to get vertices from.

A list of resulting vertices.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Visibility

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_visibility.html

**Contents:**
- Get Visibility
- Parameters
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get VSync

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/get_vsync.html

**Contents:**
- Get VSync
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get Widget Attribute

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/get_widget_attribute.html

**Contents:**
- Get Widget Attribute
- Parameters
- Inputs
- Outputs

Widget from which to get an attribute.

Resulting output value. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get World Angular Velocity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_world_angular_velocity.html

**Contents:**
- Get World Angular Velocity
- Parameters
- Inputs
- Outputs

World Angular Velocity todo.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get World Gravity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/get_world_gravity.html

**Contents:**
- Get World Gravity
- Outputs

Gravity data of current world/scene.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get World Linear Velocity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_world_linear_velocity.html

**Contents:**
- Get World Linear Velocity
- Parameters
- Inputs
- Outputs

World Linear Velocity todo.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get World Orientation

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_world_orientation.html

**Contents:**
- Get World Orientation
- Parameters
- Inputs
- Outputs

World Orientation todo.

World Orientation todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get World Position

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_world_position.html

**Contents:**
- Get World Position
- Parameters
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get World Scale

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_world_scale.html

**Contents:**
- Get World Scale
- Parameters
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Get World Transform

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/get_attribute/get_world_transform.html

**Contents:**
- Get World Transform
- Parameters
- Inputs
- Outputs

World Transform todo.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Glossary

**URL:** https://upbge.org/docs/latest/manual/manual/glossary/index.html

**Contents:**
- Glossary

This page lists definitions for terms used in Blender and UPBGE Manual, in alphabetical order.

Area of the screen visible on most devices. Place content inside it to ensure it does not get cut off.

When many items are selected, the last selected item will be the active one. Used in situations where the interface only shows options for one item at a time.

Rendering artifacts in the form of jagged lines.

Additional channel in an image for transparency.

Method where RGBA channels are stored as (R, G, B, A) channels, with the RGB channels unaffected by the alpha channel. This is the alpha type used by paint programs such as Photoshop or Gimp, and used in common file formats like PNG, BMP or Targa. So, image textures or output for the web are usually straight alpha.

Method where RGBA channels are stored as (R × A, G × A, B × A, A), with the alpha multiplied into the RGB channel.

This is the natural output of render engines, with the RGB channels representing the amount of light that comes toward the viewer, and alpha representing how much of the light from the background is blocked. The OpenEXR file format uses this alpha type. So, intermediate files for rendering and compositing are often stored as premultiplied alpha.

Conversion between the two alpha types is not a simple operation and can involve data loss, as both alpha types can represent data that the other cannot, though it is often subtle.

Straight alpha can be considered to be an RGB color image with a separate alpha mask. In areas where this mask is fully transparent, there can still be colors in the RGB channels. On conversion to premultiplied alpha, this mask is applied and the colors in such areas become black and are lost.

Premultiplied alpha, on the other hand, can represent renders that are both emitting light and letting through light from the background. For example, a transparent fire render might be emitting light, but also letting through all light from objects behind it. On converting to straight alpha, this effect is lost.

A separate image map is stored for each color and alpha channel. Channel packing is commonly used by game engines to save memory and to optimize memory access.

The light that comes from the surrounding environment as a whole.

A ratio of how much Ambient Light a surface point would be likely to receive. If a surface point is under a foot or table, it will end up much darker than the top of someone’s head or the tabletop.

Simulation of motion.

Is the technique of minimizing Aliasing, by e.g. rendering multiple samples per pixel.

An Object consisting of Bones. Used to Rig characters, props, etc.

Curated data-blocks that are meant for reuse, usually contained in an Asset Library.

Note that there are other meanings of the word “asset” – sometimes this is used more generically, and refers to any “useful thing”, like images, models, materials, and more.

Container for assets, similar to what a directory is for files.

Directory on drive, registered in the list of asset libraries in the preferences.

Asset-related information, such as its catalog, description, author, preview, and tags.

A generic term to describe data stored per-element in a geometry data-block.

A reference line which defines coordinates along one cardinal direction in n-dimensional space.

Rotation method where X, Y, and Z correspond to the axis definition, while W corresponds to the angle around that axis, in radians.

The process of computing and storing the result of a potentially time-consuming calculation so as to avoid needing to calculate it again.

The operation to chamfer or bevel edges of an object.

A computer graphics technique for generating and representing curves.

The exponent value (with base two) for how many colors can be represented within a single color channel. A higher bit depth will allow more possible colors, reducing banding, and increasing precision. Yet a higher bit depth will increase memory usage exponentially.

Methods for blending two colors together. See also Blend Modes on Krita docs.

The timespan of a Blender instance. The session begins with starting an instance of Blender and ends with closing it. In some cases, loading a new file may be considered beginning a new session. If so, the documentation should mention that.

The building block of an Armature. Made up of a Head, Tail and Roll Angle which define a set of local axes and a point of rotation at the Head. Also see Pose Bone.

Collection of bones of an Armature, identified by its name. Bone collections can be used to organise bones and toggle their visibility.

A type of logic dealing with binary true/false states.

The box that encloses the shape of an object. The box is aligned with the local space of the object.

Technique for simulating slight variations in surface height using a grayscale “heightmap” texture.

A hierarchical structure of geometric objects. See also Bounding Volume Hierarchy on Wikipedia.

The optical phenomenon of light concentration focused by specular reflections or refracting objects. In example observable on light passing through a glass of water onto a table or the pattern at the bottom of a swimming pool.

In rendering this refers to diffuse reflected light paths after a glossy or refraction bounce. See also Caustics on Wikipedia.

An Object that is affected by its Parent.

In general, a resulting image color decomposition, where its (L or Y) luminance channel is separated. There are two different contexts whereas this term is used:

Refers to the general color decomposition resulting in Y (Luminance) and C (Chrominance) channels, whereas the chrominance is represented by: U = ( Blue minus Luminance ) and V = ( Red minus Luminance ).

Refers to a point in the color gamut surrounded by a mixture of a determined spectrum of its RGB neighboring colors. This point is called Chroma key and this key (a chosen color) is used to create an Alpha Mask. The total amount of gamut space for this chrominance point is defined by users in a circular or square-shaped format.

The coordinates of the Primaries on the CIE 1931 xy chromaticity diagram.

Limits a variable to a range. The values over or under the range are set to the constant values of the range’s minimum or maximum.

A device for organizing objects.

A gamut traditionally refers to the volume of color a particular color model/space can cover. In many instances, it is illustrated via a 2D model using CIE Yxy coordinates.

A mechanism for representing colors as numbers.

An additive system where three primaries; red, green, and blue are combined to make other colors.

Three values often considered as more intuitive (human perception) than the RGB system. In this model, colors are represented as Hue, Saturation, and Value.

Similar to HSV except the colors are represented as Hue, Saturation, and Luminance.

Luminance-Chrominance standard used in broadcasting analog PAL (European) video.

Luminance-ChannelBlue-ChannelRed component video for digital broadcast use, whose standards have been updated for HDTV and commonly referred to as the HDMI format for component video.

A coordinate system in which a vector represent a color value. This way the color space defines three things:

The exact color of each of the Primaries;

The color spaces supported by Blender depend on the active OCIO config.

A color space that uses the Rec .709 Primaries and a D65 white point, and 2.2 gamma correction value as the transfer function.

Face in which one vertex is inside a triangle formed by other vertices of the face. See also Convex and concave polygons on Wikipedia.

A way of controlling one Object with data from another.

Face where, if lines were drawn from each vertex to every other vertex, all lines would remain in the face. Opposite of a Concave Face.

Refers to any set of elements that are all aligned to the same 2D plane in 3D space.

Property of an Edge. Used to define the sharpness of edges in Subdivision Surface meshes.

Asset library that is not a directory on drive, but only reflects the assets in the current blend-file. This library is available regardless of the location of the blend-file.

A type of object defined in terms of a line interpolated between Control Vertices. Available types of curves include Bézier, NURBS and Poly.

The part of a curve connecting two adjacent control points.

Often referring to an object being circular. This term is often associated with Curve.

An existing Blender object, which is using its own data, or linked data (data owned and controlled by another Blender object).

A material for real world objects that are electrical insulators such as plastics, wood, glass, ect. Essentially this summarizes any material that is solid and non metallic.

Even, directed light coming off a surface. For most things, diffuse light is the main lighting we see. Diffuse light comes from a specific direction or location and creates shading. Surfaces facing towards the light source will be brighter, while surfaces facing away from the light source will be darker.

The light that has a specific direction, but no location. It seems to come from an infinitely far away source, like the sun. Surfaces facing the light are illuminated more than surfaces facing away, but their location does not matter. A directional light illuminates all objects in the scene, no matter where they are.

A method for distorting vertices based on an image or texture. Similar to Bump Mapping, but instead operates on the mesh’s actual geometry. This relies on the mesh having enough geometry to represent details in the image.

Refers to an image whose Luminance channel is limited to a certain range of values (usually 0-1). The reason it is called display referenced is because a display cannot display an infinite range of values. So, the term Scene Referenced must go through a transfer function to be converted from one to the other.

The distance in front of and behind the subject which appears to be in focus. For any given lens setting, there is only one distance at which a subject is precisely in focus, but focus falls off gradually on either side of that distance, so there is a region in which the blurring is tolerable. This region is greater behind the point of focus than it is in front, as the angle of the light rays change more rapidly; they approach being parallel with increasing distance.

Technique for rendering and displaying content on the screen. Blender uses two buffers (images) to render the interface, the content of one buffer is displayed while rendering occurs on the other buffer. When rendering is complete, the buffers are switched.

Straight segment (line) that connects two Vertices, and can be part of a Face.

Chain of Edges belonging to consecutive Quads. An edge loop ends at a pole or a boundary. Otherwise, it is cyclic.

Path of all Edge along a Face Loop that share two faces belonging to that loop.

Objects that are able to spontaneously return to their original shape after all outside forces are removed from the object.

The amount a material is elastic versus inelastic.

An Object without any Vertices, Edges or Face.

Rotation method where rotations are applied to each of the X, Y, Z axes in a specific order.

Euler orders in Blender are most intuitive when read backwards: XYZ Euler is similar to rotating around Local Z using the Rotate tool in the 3D Viewport, followed by Local Y and then Local X.

A curve that holds the animation values of a specific property.

Mesh element that defines a piece of surface. It consists of three or more Edges.

Chain of consecutive Quads. A face loop stops at a Triangle or N-gon (which do not belong to the loop), or at a boundary. Otherwise, it is cyclic.

The normalized vector perpendicular to the plane that a Face lies in. Each face has its own normal.

A special Data User, a program construct that is used to mark an object (e.g. material) to be saved in a blend-file, even when no Real User is using the object. Objects that are not used by any Data User are not included in saved blend-files.

The area in which objects are visible to the camera. Also see Focal Length.

Rendering artifacts encountered with path tracing resulting from improbable samples that contribute very high values to pixels.

The process of determining the movement of interconnected segments or bones of a body or model in the order from the parent bones to the child bones. Using forward kinematics on a hierarchically structured object, you can move the upper arm then the lower arm and hand go along with the movement. Without forward kinematics the lower arm and hand would disconnect from upper arm and would move independently in space. See also Inverse Kinematics.

The distance required by a lens to focus collimated light. Defines the magnification power of a lens. Also see Field of View.

In video compression, a frame can be compressed by several different algorithms. These algorithms are known as picture types or frame types and there are three major types: I, P, and B frames.

The least compressible but don’t require other video frames to decode.

Use data from previous frames to decompress and are more compressible than I‑frames.

Use both previous and forward frames for data reference to get the highest amount of compression.

An operation used to adjust the brightness of an image. See also Gamma correction on Wikipedia.

Relating to the shortest possible path between two points on a curved surface.

The mean average of the positions of all vertices making up the object.

A pivoted support that allows the rotation of an object about a single axis. See also Gimbal on Wikipedia.

A superset of Radiosity and ray tracing. The goal is to compute all possible light interactions in a given scene, and thus, obtain a truly photorealistic image. All combinations of diffuse and specular reflections and transmissions must be accounted for. Effects such as color bleeding and caustics must be included in a global illumination simulation.

A set of techniques that allow a far greater dynamic range of exposures than normal digital imaging techniques. The intention is to accurately represent the wide range of intensity levels found in real scenes, ranging from direct sunlight to the deepest shadows. See also HDRI on Wikipedia.

A subcomponent of a Bone. The point of rotation for the bone has X, Y, and Z coordinates measured in the Local Space of the Armature object. Used in conjunction with the Tail to define the local Y axis of the bone in Pose Mode. The larger of the two ends when displayed as an Octahedron.

A shade of light out of the color spectrum.

The process of determining the movement of interconnected segments or bones of a body or model in the order from the child bones to the parent bones. Using inverse kinematics on a hierarchically structured object, you can move the hand then the upper and lower arm will automatically follow that movement. Without inverse kinematics the hand would come off the model and would move independently in space. See also Forward Kinematics.

The process of calculating new data between points of known value, like Keyframes.

A property of transparent materials. When a light ray travels through the same volume it follows a straight path. However, if it passes from one transparent volume to another, it bends. The angle by which the ray is bent can be determined by the IOR of the materials of both volumes.

A frame in an animated sequence drawn or otherwise constructed directly by the animator. In classical animation, when all frames were drawn by animators, the senior artist would draw these frames, leaving the “in between” frames to an apprentice. Now, the animator creates only the first and last frames of a simple sequence (keyframes); the computer fills in the gap.

Inserting Keyframes to build an animated sequence.

A type of object consisting of a non-renderable three-dimensional grid of vertices.

Refers to the reflection or transmission of a light ray upon interaction with a material.

A 3D coordinate system that originates (for Objects) at the Object Origin. Or (for Bones) at the Head of the Bone. Compare to World Space.

The intensity of light either in an image/model channel, or emitted from a surface per square unit in a given direction.

Manifold meshes, also called ‘water-tight’ meshes, define a closed non-self-intersecting volume (see also Non-manifold).

A manifold mesh is a mesh in which the structure of the connected faces in a closed volume will always point the normals (and their surfaces) to the outside or to the inside of the mesh without any overlaps. If you recalculate those normals, they will always point at a predictable direction (to the outside or to the inside of the volume). When working with non-closed volumes, a manifold mesh is a mesh in which the normals will always define two different and non-consecutive surfaces. A manifold mesh will always define an even number of non-overlapped surfaces.

Stands for “material capture”, using an image to represent a complete material including lighting and reflections.

A grayscale image used to include or exclude parts of an image. A matte is applied as an Alpha Channel, or it is used as a mix factor when applying Color Blend Modes.

Type of object consisting of Vertices, Edges and Faces.

A polygon roughly the size of a pixel or smaller.

‘MIP’ is an acronym of the Latin phrase ‘multum in parvo’, meaning ‘much in little’. Mip-maps are progressively lower resolution representations of an image, generally reduced by half squared interpolations using Anti-Aliasing.

Mip-mapping is the process used to calculate lower resolutions of the same image, reducing memory usage to help speed visualization, but increasing memory usage for calculations and allocation. Mip-mapping is also a process used to create small anti-aliased samples of an image used for texturing.

Mip-mapping calculations are made by CPUs, but modern graphic processors can be selected for this task and are way faster.

A process of estimating the direction of light rays to improve sampling quality. See Importance sampling on Wikipedia.

A non-destructive operation that is applied on top of some sort of data.

The phenomenon that occurs when we perceive a rapidly moving object. The object appears to be blurred because of our persistence of vision. Simulating motion blur makes computer animation appear more realistic.

Rendering multiple samples per pixel, for Anti-Aliasing.

A Face that contains more than four Vertices.

A general term used to describe a 3D mouse, or any input devices which supports more degrees of freedom than a conventional 2D input device.

Non-Manifold meshes essentially define geometry which cannot exist in the real world. This kind of geometry is not suitable for several types of operations, especially those where knowing the volume (inside/outside) of the object is important (refraction, fluids, Boolean operations, or 3D printing, to name a few).

A non-manifold mesh is a mesh in which the structure of a non-overlapped surface (based on its connected faces) will not determine the inside or the outside of a volume based on its normals, defining a single surface for both sides, but ended with flipped normals. When working with non-closed volumes, a non-manifold mesh will always determine at least one discontinuity in the normal directions, either by an inversion of a connected loop, or by an odd number of surfaces. A non-manifold mesh will always define an odd number of surfaces. There are several types of non-manifold geometry:

Some borders and holes (edges with only a single connected face), as faces have no thickness.

Edges and vertices not belonging to any face (wire).

Edges connected to three or more faces (interior faces).

Vertices belonging to faces that are not adjoining (e.g. two cones sharing the vertex at the apex).

Animation technique that allows the animator to edit motions as a whole, not just the individual keys. Nonlinear animation allows you to combine, mix, and blend different motions to create entirely new animations.

The normalized vector perpendicular to a surface. Normals can be assigned to vertices, faces and modulated across a surface using Normal Mapping. See also Normals on Wikipedia.

Is similar to Bump Mapping, but instead of the image being a grayscale heightmap, the colors define in which direction the normal should be shifted, the three color channels being mapped to the three directions X, Y and Z. This allows more detail and control over the effect.

A computer graphics technique for generating and representing curves and surfaces.

Container for a type (mesh, curve, surface, metaball, text, armature, lattice, empty, camera, light) and basic 3D transform data (Object Origin).

A reference point used to position, rotate, and scale an Object and to define its Local Space coordinates.

An eight-sided figure commonly used to depict the Bones of an Armature.

The graphics system used by Blender (and many other graphics applications) for rendering 3D graphics, often taking advantage of hardware acceleration. See also OpenGL on Wikipedia.

An executable action that is completed the moment they’re initiated.

The term used to describe the situation. when not all of a televised image is present on a viewing screen.

A user interface element that contains buttons. Panels are collapsible to hide there contents and can often be rearranged.

An Object that affects its Child objects.

Creating a Parent-Child relationship between two objects.

Technique that simulates certain kinds of fuzzy phenomena, which are otherwise very hard to reproduce with conventional rendering techniques. Common examples include fire, explosions, smoke, sparks, falling leaves, clouds, fog, snow, dust, meteor tails, stars, and galaxies, or abstract visual effects like glowing trails, magic spells. Also used for things like fur, grass or hair.

Local illumination model that can produce a certain degree of realism in three-dimensional objects by combining three elements: diffuse, specular and ambient for each considered point on a surface. It has several assumptions – all lights are points, only surface geometry is considered, only local modeling of diffuse and specular, specular color is the same as light color, ambient is a global constant.

The pivot point is the point in space around which all rotation, scaling and mirror transformations are centered.

The smallest unit of information in a 2D raster image, representing a single color made up of red, green, and blue channels. If the image has an Alpha Channel, the pixel will contain a corresponding fourth channel.

A list of points in 3D space.

Vertex where three, five, or more edges meet. A vertex connected to one, two, or four edges is not a pole.

Pose-specific properties of a Bone, such as its location / rotation / scale relative to the Armature’s rest pose. Its properties are stored on the Object, and thus can be different for each user of the Armature. The Pose Bone also stores constraints.

Used for Posing, Keyframing, Weight Painting, Constraining and Parenting the Bones of an Armature.

Moving, Rotating and Scaling the Pose Bones of an Armature to achieve an aesthetically pleasing pose for a character.

In color theory, primaries (often known as primary colors) are the abstract lights, using an absolute model, that make up a Color Space.

A basic object that can be used as a basis for modeling more complicated objects.

Computer generated (generic) textures that can be configured via different parameters.

In computer graphics, there are two common camera projections used.

A perspective view is geometrically constructed by taking a scene in 3D and placing an observer at point O. The 2D perspective scene is built by placing a plane (e.g. a sheet of paper) where the 2D scene is to be rendered in front of point O, perpendicular to the viewing direction. For each point P in the 3D scene a PO line is drawn, passing by O and P. The intersection point S between this PO line and the plane is the perspective projection of that point. By projecting all points P of the scene you get a perspective view.

In an orthographic projection, you have a viewing direction but not a viewing point O. The line is then drawn through point P so that it is parallel to the viewing direction. The intersection S between the line and the plane is the orthographic projection of the point P. By projecting all points P of the scene you get the orthographic view.

For video editing, a proxy is a smaller version of the original file, typically using an optimized video codec and lower resolution version (faster to load) that stands in for the main image or video.

When proxies are built, editing functions like scrubbing and scrolling and compositing is much faster but gives lower resolution and slightly imprecise result.

Face that contains exactly four Vertices.

Rotation method where rotations are defined by four values (X, Y, Z, and W). X, Y, and Z also define an Axis, and W an angle, but it is quite different from Axis Angle.

Quaternion values can be interpreted geometrically as defining a point on a unit sphere in 4D space. Moving along any great circle of the sphere represents rotating around a fixed axis, with one full circle matching two full rotations.

A global lighting method that calculates patterns of light and shadow for rendering graphics images from three-dimensional models. One of the many different tools which can simulate diffuse lighting in Blender. See also Radiosity (computer graphics) on Wikipedia.

Blender uses pseudo random number generators, which produce numbers that appear to be random, but given the same initial condition, they will always produce the exact same sequence of numbers. This is a critical feature to get reproducible and/or stable effects (otherwise e.g. your hair simulation would change every time you re-run it, without any way to control the outcome).

The seed is a number that represents the initial condition of a random generator, if you change its seed, it will produce a new sequence of pseudo-random numbers. See also Random seed on Wikipedia.

Rendering technique that works by tracing the path taken by a ray of light through the scene, and calculating reflection, refraction, or absorption of the ray whenever it intersects an object in the world. More accurate than Scanline, but much slower.

A Blender object, which is a Data User. Opposite of Fake User, which is only a program construct.

The change in direction of a wave due to a change in velocity. It happens when waves travel from a medium with a given Index of Refraction to a medium with another. At the boundary between the media, the wave changes direction; its wavelength increases or decreases but frequency remains constant.

The process of computationally generating a 2D image from 3D geometry.

External files such as images, sounds, fonts and volumes files that can be packed into a blend-file.

A color model based on the traditional primary colors, Red/Green/Blue. RGB colors are also directly broadcasted to most computer monitors.

A system of relationships that determine how something moves. The act of building of such a system.

The orientation of the local X and Z axes of a Bone. Has no effect on the local Y axis as local Y is determined by the location of the Head and Tail.

In real CMOS cameras the sensor is read out with scanlines and hence different scanlines are sampled at a different moment in time. This, for example, make vertical straight lines being curved when doing a horizontal camera pan. See also Rolling Shutter on Wikipedia.

A grayscale texture that defines how rough or smooth the surface of a material is. This may also be known as a Glossy Map.

Also known as colorfulness, saturation is the quantity of hue in the color (from desaturated – a shade of gray – to saturated – brighter colors).

Rendering technique. Much faster than Ray Tracing, but allows fewer effects, such as reflections, refractions, motion blur and focal blur.

An image whose Luminance channel is not limited. See also Display Referenced.

Process of altering the color of an object/surface in the 3D scene, based on its angle to lights and its distance from lights to create a photorealistic effect.

Defines how Face is shaded. Faces can be either solid (faces are rendered flat) or smooth (faces are smoothed by interpolating the normal on every point of the face).

A light which is reflected precisely, like a mirror. Also used to refer to highlights on reflective objects.

Mechanism of light transport in which light penetrates the surface of a translucent object, is scattered by interacting with the material, and exits the surface at a different point. All non-metallic materials are translucent to some degree. In particular, materials such as marble, skin, and milk are extremely difficult to simulate realistically without taking subsurface scattering into account.

A method of creating smooth higher poly surfaces which can take a low polygon mesh as input. See also Catmull-Clark subdivision surface on Wikipedia.

Technique for adding more geometry to a mesh. It creates new vertices on subdivided edges, new edges between subdivisions and new faces based on new edges. If new edges cross a new vertex is created at their crossing point.

Refers to decomposition of an arbitrary rotation into a sequence of two single axis rotations: a swing rotation that aims a chosen axis in its final direction using the shortest possible rotation path, followed by a twist rotation around that axis.

In the Quaternion representation the swing rotation always has 0 as the X/Y/Z component corresponding to the selected axis, while twist always has 0 as the other two components.

A subcomponent of a Bone. Has X, Y and Z coordinates measured in the Local Space of the armature object. Used in conjunction with the Head to define the local Y axis of a bone in Pose Mode. The smaller of the two ends when displayed as an Octahedron.

A line that intersects a surface at exactly one point, a tangent is perpendicular to a Normal.

The tiling of a plane using one or more geometric shapes usually resulting in Micropolygons.

Specifies visual patterns on surfaces and simulates physical surface structure.

The bounding box to use when using Generated mapping to add a Texture to an image.

A coded signal on videotape or film giving information about the frame number and time the frame was recorded. Timecodes are used to sync media between different recording devices, including both audio and video.

Area of the screen visible on all devices. Place text and graphics inside this area to make sure they do not get cut off.

The arrangement of Vertices, Edges, and Faces which define the shape of a mesh. See Vertex, Edge, and Face.

The combination of location, rotation, and scale. Can be expressed in World Space or Local Space.

Face with exactly three Vertices.

Defines a relation between the surface of a mesh and a 2D texture. In detail, each face of the mesh is mapped to a corresponding face on the texture. It is possible and often common practice to map several faces of the mesh to the same or overlapping areas of the texture.

The brightness of the color (dark to light).

A point in 3D space containing a location. Vertices are the terminating points of Edges.

Collection of Vertices. Vertex groups are useful for limiting operations to specific areas of a mesh.

A cubic 3D equivalent to the square 2D pixel. The name is a combination of the terms “Volumetric” and “Pixel”. Used to store smoke and fire data from physics simulations.

In animation, a walk cycle is a character that has just the walking function animated. Later on in the animation process, the character is placed in an environment and the rest of the functions are animated.

Assigning Vertices to a Vertex Group with a weight of 0.0 - 1.0.

A reference value for white light when all primaries of a color model are combined evenly.

A white point is defined by a set of CIE illuminates which correspond to a color temperature. For example, D65 corresponds to 6500 K light and D70 corresponding to 7000 K.

A 3D coordinate system that originates at a point at the origin of the world. Compare to Local Space.

Raster-based storage of the distance measurement between the camera and the surface points. Surface points which are in front of the camera have a positive Z value and points behind have negative values. The Z-depth map can be visualized as a grayscale image.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Groups

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/groups/index.html

**Contents:**
- Groups

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Guidelines

**URL:** https://upbge.org/docs/latest/manual/manual/contribute/guidelines.html

**Contents:**
- Guidelines
- Bigger Changes
- Getting Help

You can modify the manual by editing local .rst text files. These files are kept in sync with those online via a repository, based on this the server will update the online manual.

The manual is written in reStructuredText (RST) markup language, and can be edited using a plain text editor. For a local preview, build the Manual source files from RST into HTML web pages.

If you are going to add or overhaul a section, be sure to check carefully that it does not already exist. The docs may be disorganized so that sections may be duplicated or in a strange location. In such cases please create an issue explaining the issue, and optionally include a revision (actual changes).

Before you make any edits that are not simple and plainly justified (for example, moving folders around), you should verify with a manual maintainer that your contribution is along the community’s vision for the manual. This ensures the best use of your time and good will as it is otherwise possible that, for some reason, your changes will conflict and be rejected or need time-consuming review. For example, another person may be already working on the section you wish to change, the section may be scheduled for deletion or to be updated according to a planned changes.

Communicating early and frequently is the key to have a productive environment, to not waste people’s effort and to attain a better Manual as a result.

If you are in doubt about functionality that you wish to document, you should pose your questions to the UPBGE developers responsible for that area or ask at the unofficial user support channels.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Inheritance And Composition

**URL:** https://upbge.org/docs/latest/manual/manual/python_scripting/understanding_inheritance.html

**Contents:**
- Inheritance And Composition
- Introduction
  - Type and Inheritance
  - Problems of Inheritance
  - Composition Over Inheritance
  - Dynamic Component Model
  - Why Inheritance Still Matters?
  - Mixins And Traits
  - Mixins and Components in UPBGE

Let us imagine we are making a video game in which characters can attack each other and receive damage. You will likely want to add a few properties like health or max_health to each object and write simple scripts to calculate them when the character gets hit or drinks a potion. Pretty simple, isn’t it?

In many cases, writing game scripts doesn’t require much more knowledge than that. A game engine is supposed to handle most of the heavy lifting for you, and all you need to do is declaring a few such variables, or writing a few conditional statements, loops, or functions to stitch them together. There is a reason why writing game logic is called ‘scripting’ even when it’s done with a compiled language like C#, after all.

But what if you want to try something more complex, like creating an RPG where you can bash a door or a chest until it breaks open? Do you see the resemblance between hitting an enemy with a sword and doing the same to a crate?

Of course, you can simply add the same variables to the crate and copy and paste the same code you used to calculate a character’s health. But what if there are many similar cases and you have to paste the same code to hundreds of them? Wouldn’t it make your project challenging to understand or modify?

Although software engineering is not a popular topic among most game developers, some of its principles like DRY or SOLID can offer a helpful guide in such a situation.

And with slight exaggeration, we can say that the entire idea of software design revolves around the concept of generalisation and abstraction, which is a tool invented to solve precisely such a kind of problem. In other words, how can we generalise the idea of something that can be damaged into a reusable code so that we don’t have to repeatedly copy and paste the same code over and over?

Object-Oriented Programming or OOP is a software paradigm that provides powerful tools we can utilise to solve such a problem. Even though it has seen increasing challenges over the years, it remains one of the most widely used software paradigms, well supported by popular languages like Python or C#. So, let’s look into the concept briefly in the next chapter.

To put it simply, a type in an OOP language determines an object’s nature (i.e. properties and behaviours). It also applies to a dynamically typed language like Python, which allows you to write code without caring too much about types. You know that you can change the value of a variable from abc to ABC by invoking its ‘upper()’ API because it has the type of str which declares upper() as its method.

But the real benefit of having a type system goes further than allowing you to figure out what functions an existing object provides. It can also serve as a tool to express a set of common characteristics that things can share, like the fact that they can be damaged, for example.

A character can be attacked and receives damage, and so can a crate. In other words, they are both something capable of being damaged and probably also destroyed after getting hit repeatedly. Let’s generalise this idea as Damageable type as follows:

But how can you use (or ‘reuse’) it to eliminate the repetition? And that is where the concept of ‘inheritance’ comes in.

If you want to make your character or a crate class damageable, you can simply make them ‘inherit’ or derive from ‘Damageable’ type like this:

As you can see, inheritance is a powerful tool to generalise ideas and promote code reuse. But it is not without problems which we will discuss in the following chapter.

We just made a crate damageable by deriving it from Damageable type. But what if we also want to add some other features, like being able to be opened? Maybe we could define another class Openable to describe the concept of something which can be opened. But can an object inherit from both of those types?

This can pose a serious issue in a language that does not allow multiple inheritance like C#. And even with languages that do, deriving from multiple parents may bring more headaches than benefits sometimes, causing issues like the infamous Diamond Problem.

Furthermore, it can also introduce additional challenges in the context of game development. Typically a game engine handles all performance-critical operations in its native layer while exposing a small set of features as a scripting API in a higher-level language like C# or Python to offer better productivity and ease of use for its users.

Because of this, some game engines (e.g. a famous private one that keeps them “united” :-)) do not allow instantiating such game-related classes directly in the scripting layer, making it difficult or even impossible to extend them by subtyping, as we discussed in the previous chapter.

And even those that do (e.g. Godot), the typical workflow they provide involves providing initial parameters from the editor, which the engine uses to instantiate objects for the user. So, if you create game objects directly in code, you’ll lose all the conveniences the editor provides. (This, however, is not the case in UPBGE as it has a unique feature that allows you to combine both approaches. We will discuss this feature later.)

Due to such limitations, it is often desirable to take a different approach to promote code reuse when working on a game project. Fortunately, a design principle can be used to overcome this particular problem called Composition Over Inheritance, which also works well when writing game scripts.

The basic idea of composition is implementing each feature of an object as a modular ‘component’. By doing so, we can compose such elements to describe the behaviours and properties of the whole.

For example, instead of making the Crate class inherit from Damageable type, we can rename the latter to HitBox and make it a property of the enclosing class:

Similarly, we can also make the crate ‘openable’ by creating a Door component and assign an instance of it as a property of Crate:

In this way, you can add as many features to an object as you like without the concern of introducing potential conflict in the type hierarchy.

Let’s take the idea one step further and generalise the concept of components itself. What if we replace individual properties like door or hit_box with a generic list?

As you see, now we can attach an arbitrary behaviour to an existing object without modifying the class definition. And what if we make the Character class damageable in the same manner? Wouldn’t it make Character look almost identical with Crate?

They look similar indeed! Then why not replace them both with something more generic, like GameObject?

If you want to make it a bit more precise, you can define a common base type to represent a component, like Component and derive both HitBox and Door from it. Using Python’s typing support for clarity, the code would look like the following example:

In fact, this is what objects and components in game engines are all about. They may be named differently or have slightly different APIs, depending on the game engine you choose. But be it GameObject/MonoBehaviour in other game engine or KX_GameObject/KX_PythonComponent in UPBGE, the core idea behind it remains the same nonetheless.

The dynamic nature - namely, the ability to define arbitrary behaviour as a component and attach it to an object without modifying its source - of the compositional pattern fits game development so well that many game engines enforce it as the only viable method to write game scripts.

But could it be a ‘silver bullet’ of software design pattern? If composition is so good for everything, why almost all major OOP languages still support inheritance?

One prominent case where using inheritance over composition would make sense is when the concepts you want to represent as types have an is-a relationship with each other.

Suppose you want to make an inventory system that can store things like food or weapons. Both an apple and a dagger may take up some space if you put them in your inventory, and they may also have other common traits like having specific weight and so on.

In other words, we can say that any item has a specific inventory slot size and weight. As long as Potion or Weapon is an Item, it inherits common properties like inventory_size or weight from its parent type. Bearing that in mind, it shouldn’t be difficult to see how saying that “a dagger is an item” is much more intuitive than saying that “it contains a component with item-specific properties and behaviours”.

Another disadvantage of using the compositional pattern could be its dynamic nature itself. As with most things in software development, there is a trade-off relationship between dynamically attaching properties or behaviours of an object and statically defining them.

Remember our first version of Character class that directly extends Damageable?

Now, compare that with a componentised version:

Can you see the difference? Aside from being slightly more verbose, the latter version is also much more prone to errors. With the former example, a decent Python IDE with a proper setup will autocomplete methods like damage and warn you if you accidentally make a typo, like when you type character.destroeyd instead of character.destroyed, for example.

And in case you want to rename a method or property, like changing damage to hit, for instance, you rely on refactoring support that most IDEs provide to perform the task without an error.

However, you will lose all such conveniences with the dynamic approach as your IDE won’t be able to infer proper types in that case, which could become a significant issue if your project grows larger and more complex.

Now, examine this method signature:

Can you guess the proper usage of that API or how to implement its body if you are a developer? If you are not sure, how about this version?

Now you know that you are expected to pass a GameObject instance as the first parameter and specify the amount you want to heal as a float value. But what is a GameObject really?

As we learned from the previous chapter, it’s just something that contains components. It may mean anything - anything from a character to a house. You may make a good guess from the method name and assume it would expect a GameObject with a Hitbox attached to it, but nobody will stop you if you pass an actual house as long as it’s also a GameObject.

Also, others may not be as smart as you and may have difficulty guessing the proper type of object to pass as the first parameter without having good documentation.

But what if we haven’t adopted the component approach but just used the plain inheritance model instead?

Now it became immediately apparent what the function expects as its first parameter. If you use an IDE, it will also let you know that the target argument supports damage method, which you can use to implement the function body as target.damage(-amount). Furthermore, it will also warn you if you attempt to pass a non-Damageable type object like a House, all of which can help you maintain your codebase as it grows in size.

However, there was a good reason why we considered adopting the more dynamic approach before, and we may still want to keep some of its benefits.

Suppose you want to derive your Crate class directly from Openable type instead of attaching a Door component to it as we did before. Wouldn’t it be still nice if you can assign different kinds of doors - like one with an animation, or another with a locking mechanism, and so on - without having to rewrite the Crate class every time?

A language feature or a design pattern called mixin can provide an answer to this question.

According to a relevant Wikipedia article, a mixin is “a class that contains methods for use by other classes without having to be the parent class of those other classes”.

Such a class is sometimes called a trait and often named as an adjective like Damageable or Openable to describe a specific aspect or characteristic of the target object.

The idea is, you can define various aspects of an object as “traits” and “mix them in” as needed. It is a powerful tool that provides a way to add behaviours to an existing class in a compositional manner without erasing the type information as the component pattern does.

Let’s make our Crate class again using the technique:

You may have noticed how intuitive the class definition reads now. Even without any comment or having to read the source code, you can immediately see the purpose of the Crate class as it’s a “damageable and openable item”, indeed.

Also, because the class is a proper subtype of both Damageable and Openable, an IDE will be able to autocomplete such methods like damage(amount) or open() for you. It also enables you to tighten the type signature when you write an API like def heal(damageable: Damageable, amount: Float) -> None so that an IDE can warn you if you attempt to pass an object with a wrong type by mistake.

But how can we preserve the dynamic nature of the component model? What if I want to add crates in the game editor and make some of them have a unique animation when they open?

Of course, you can still benefit from the dynamic nature of using components, well, by using components! In fact, mixins and components are not mutually exclusive concepts since you can write a trait that relies on a component to implement a behaviour.

As the trait is now mixed into a GameObject, it can reference its components property from which it can find a suitable component to work with, in this case, a Door. And the fact that the Door class is a component means that you can dynamically assign a specific implementation of it from the game editor without modifying the source code of either Crate or Openable.

If you want to add an animation to some of the crates, for example, you can write a special subtype of Door like class AnimatedDoor(Door) and attach it to a game object with the Openable trait. As long as the target object has the trait, it wouldn’t matter if it’s a crate or a gate. And as long as the component derives from Door, it will work perfectly fine with any Openable object, be it an animated door or one that requires a key to open it, for instance.

As shown in the previous chapters, the component model and mixins are powerful tools to design your software while maintaining a clean separation of concern between classes responsible for different functionalities.

To reap the full benefits of these design patterns, however, it is necessary to have a proper programming environment that supports such concepts.

An older version of C# (before 8.0), for example, didn’t allow providing a default implementation of a method defined in an interface, thus severely limiting its usefulness when used as a trait.

And while most of the game engines enforced either the component model (e.g. private one that keeps them united) or the inheritance model (e.g. Godot) on their users, few, if any, support both of them like UPBGE now does.

With its recent introduction of the custom game object feature, you can define either static or dynamic (i.e. component-based) traits and mix them into any game object in UPBGE. It provides programmers with a powerful tool to design and organise game-related classes without sacrificing the ability to configure them graphically within UPBGE.

The example code shown above will work almost verbatim on UPBGE if you simply replace GameObject with KX_GameObject and Component with KX_PythonComponent like this:

Now you can assign different initial health values to each crate in UPBGE or add an animated door to some of them without writing a new class for such cases. Also, when you write scripts, you can directly invoke any API they define without having to look up nested components or losing the valuable type information.

Those are some of the few unique advantages that UPBGE has over its competitors.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (python):
```python
class Damageable:
  def __init__(self, init_health: int = 100):
    self.health = init_health

  def damage(self, amount: int) -> None:
    self.health = max(0, self.health - amount)

  @property
  def destroyed(self) -> bool:
    return self.health == 0
```

Example 2 (python):
```python
class Damageable:
  def __init__(self, init_health: int = 100):
    self.health = init_health

  def damage(self, amount: int) -> None:
    self.health = max(0, self.health - amount)

  @property
  def destroyed(self) -> bool:
    return self.health == 0
```

Example 3 (python):
```python
class Damageable:
  def __init__(self, init_health: int = 100):
    self.health = init_health

  def damage(self, amount: int) -> None:
    self.health = max(0, self.health - amount)

  @property
  def destroyed(self) -> bool:
    return self.health == 0
```

Example 4 (php):
```php
class Character(Damageable):
  pass

class Crate(Damageable):
  pass

character = Character()

character.damage(40)
crate.damage(120)

print(character.health) # Prints "60"
print(character.destroyed) # Prints "False"

print(crate.health) # Prints "0"
print(crate.destroyed) # Prints "True"
```

---

## Input

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/index.html

**Contents:**
- Input

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Integer

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/integer.html

**Contents:**
- Integer
- Parameters
- Inputs
- Outputs

Selected data type - integer value.

Fixed input integer value, or a result from connected node.

Resulting output integer value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Interpolate

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/interpolate.html

**Contents:**
- Interpolate
- Inputs
- Outputs

Interpolate from which value.

Interpolate to this value.

Interpolation factor. todo

Resulting interpolated value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introducing Logic Bricks

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_bricks/index.html

**Contents:**
- Introducing Logic Bricks

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introducing Logic Nodes

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_nodes/index.html

**Contents:**
- Introducing Logic Nodes

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introducing Python Components

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_python_components/index.html

**Contents:**
- Introducing Python Components

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introducing Python Scripting

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_python_scripting/index.html

**Contents:**
- Introducing Python Scripting

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introduction

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/introduction.html

**Contents:**
- Introduction
- Logic Trees
- Logic Nodes
- Global Variables
- Architecture

As an alternative to Python scripts and Logic Bricks, Logic Nodes provide an intuitive and versatile way to create game logic. Designed to support rapid prototyping, they enable artists and game designers to quickly test and even fully implement desired features.

4-Key Template for Object/Player Movement

Logic Nodes use a visual approach to programming, allowing developers to skip learning a programming language and the engine’s API, to get their game done. With a set of 300+ nodes, close to all functionality is covered - including calling custom scripts and referencing Logic Bricks to make full use of UPBGE’s power.

Logic Trees are different from Logic Bricks, as they are not directly bound to an object. They can be created, edited and compiled without any object in the scene. To be executed though, they need to be applied to at least one object (or called through another tree, but more on that later). Now the difference between being bound and being applied to an object is that multiple objects can have the same Logic Node Tree applied to them, while Logic Bricks are unique for each object.

Basically, Logic Node Trees work just as Material Node Trees do - you add nodes, connect them to one another and something happens. One difference would be that with a material, you always need to route the end of the nodes chain back to the Material Output. This is not the case with Logic Nodes. You can have a lot of smaller patches within a single tree which will be executed, regardless if they’re connected or not. As there’s no such thing as an Output Node, each part of the tree is evaluated “as is”.

The system is built around nodes, and each node has Sockets that can be connected to the Sockets of other nodes. Normally the code isn’t very picky and will try to work with whatever comes its way, meaning that you can try to combine different types of Sockets without having to fear a complete crash.

It is generally advised to try to keep Logic Trees as small as possible to keep the performance high. You would for example use the Formula Node for more complex equations instead of putting multiple Math nodes together.

With the Logic Nodes addon also comes the ability to create and read Global Variables. They work very similarly to Properties, but again they are not bound to an object, but to the scene. These variables are intended to be used to store data about the world like time, temperature etc., or game settings, though they can just as well be used for player or entity data that wouldn’t really make sense on an object.

Under the hood, Logic Nodes are actually generating Python scripts to be executed by the game engine. The generated component will have options for executing the tree only at startup and for executing the tree only when a certain property is set. Using this method will prevent you from accessing Logic Bricks directly, but you can still access them via custom Python calls.

Due to the way Logic Nodes work, they are the most performance-heavy way to create logic.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introduction

**URL:** https://upbge.org/docs/latest/manual/manual/editors/logic_nodes/introduction.html

**Contents:**
- Introduction
- Logic Node Add-On
  - Why use logic nodes when there’s logic bricks
  - Things to consider
  - The main loop
  - How does it work
- Basic Node Types
  - Condition Nodes
  - Parameter Nodes
  - Action Nodes

Logic Node add-on adds a large variety of logic nodes to the UPBGE game engine, enabling easy visual game development, just like in the Unreal Engine or Armory3D.

Basically, there’s two ways to get logic into your game.

Using nodes is effectively scripting in python, only visually. They have the advantage of being a lot more versatile than logic bricks. Nodes can be placed freely, trees can be nested and eventually, the code contained by each node will be accessible.

Logic bricks are fastest

This is because they are using Blenders native C++ API, which makes them simply creepy fast. Second fastest is custom python code, and logic nodes are the slowest.

Only execute code when needed

You always want to avoid the On Update node, which basically executes every frame. Only use this when necessary, otherwise try to get some kind of condition. Logic trees can also be linked to every sensor the logic bricks can offer, make good use of that.

Main loop is most basic calculation the engine has to go through effectively 60 times a second, keep that in mind. In that loop, every sensor logic brick on every object is checked for its status (whether it is active or not), which is incredibly fast.

If any sensor is active, the linked controller will be executed. A controller can be either a logic gate, in which case it fires up the linked actuators, or it can be python controller, in which case the referenced python code is evaluated.

This is where you need to be careful what you do. You don’t want to run a lot of unnecessary code each frame, so put in breaking conditions as often as you can to avoid overhead in the main loop.

Under the hood, each logic node includes some lines of python code. That code is executed when the condition for the node is met. If a node has no condition, it is executed each time the sensor logic brick connected to it is active.

When pressing :menuselection:Apply To Selected (or :menuselection:Force Compile) in the logic node tree editor, a .py file is generated. The file defines a reference class for each node in a particular order so that every node is executed only when all values needed for it are computed.

Then, whenever the connected sensor is active, the :py:evaluate() function for each node is called. This is where the magic happens. This function collects all the input values from its sockets before waltzing though the lines of code that make something happen in-game.

For general nodes overview see Blender’s nodes chapter.

There are 3 basic logic node types:

These nodes are either conditions themselves (like sensors) or they can act as logic gates.

Most parameter nodes do not need a condition to perform. They are pre-defined calculations or data fetchers.

These are the nodes that manipulate, generate or remove something in the game. From moving objects to writing save files, these nodes perform a certain action.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introduction

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/introduction.html

**Contents:**
- Introduction
- Common Options

Sensors are the logic bricks that cause the logic to do anything. Sensors give an output when something happens, e.g. a trigger event such as a collision between two objects, a key pressed on the keyboard, or a timer for a timed event going off. When a sensor is triggered, a positive pulse is sent to all controllers that are linked to it.

The logic blocks for all types of sensor may be constructed and changed using the Logic Editor; details of this process are given in the Sensor Editing page.

Common Sensor options

All sensors have a set of common buttons, fields and menus. They are organized as follows:

Collapses the sensor information to a single line (toggle).

Specifies the type of the sensor.

The name of the sensor. This can be selected by the user. It is used to access sensors with Python; it needs to be unique among the selected objects.

Display the sensor even when it is not linked to a visible states controller.

Move the sensor up or down over other sensors within the column.

When unchecked the sensor is deactivated, no pulses will be sent to the connected controllers. Very useful to check different logics without unlink or delete the sensor.

Triggers If a controller does not get triggered by any connected sensor (regardless of the sensors’ state) it will not be activated at all.

A sensor triggers the connected controllers on state change. When the sensor changes its state from negative to positive or positive to negative, the sensor triggers the connected controllers. A sensor triggers a connected controller as well when the sensor changes from deactivation to activation.

The following parameters specify how the sensor triggers connected controllers:

If this is set, the connected controllers will be triggered as long as the sensor’s state is positive. The sensor will trigger skipping the logic ticks (See parameter: Skip) indicated in the sensor.

If this is set, the connected controllers will be triggered as long as the sensor’s state is negative. The sensor will trigger skipping the logic ticks (See parameter: Skip) indicated in the sensor.

This parameter sets the number of logic ticks skipped between 2 active pulses or triggers. The default value is 0 and it means no logic tick is skipped. It is only used if at least one of the level triggering parameters are enabled.

Raising the value of Skip is a good way for saving performance costs by avoiding to execute controllers or activate actuators more often than necessary.

Examples: (assuming the default frame rate with a frequency of 60 Hz (60 frames per second)).

Frames without trigger

Frequency in frames/sec

The sensor triggers the next frame.

The sensor triggers at one frame and skips another one until it triggers again. It results in half speed.

The sensor triggers at one frame and skips 29 frames until it triggers again.

The sensor triggers at one frame and skips 59 frames until it triggers again.

Triggers connected controllers when state (of the build-in state machine) changes (for more information see States).

The following parameters specify how the sensor’s status gets evaluated:

Changes the sensor’s state to negative one frame after changing to positive even if the sensor evaluation remains positive. As this is a state change it triggers the connected controllers as well. Only one of Tap or Level can be activated. If the TRUE level triggering is set, the sensor state will consecutive change from True to False until the sensor evaluates False. The FALSE level triggering will be ignored when the Tap parameter is set.

This inverts the sensor output. If this is set, the sensor’s state will be inverted. This means the sensor’s state changes to positive when evaluating False and changes to False when evaluating True. If the Tap parameter is set, the sensor triggers the controller based on the inverted sensor state.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introduction

**URL:** https://upbge.org/docs/latest/manual/manual/physics/introduction.html

**Contents:**
- Introduction
- What Is Physics?
- Bullet Physics Library
- Overview
- Visualizing Physics
- Show Framerate and Profile
- Mesh Deformations
- Soft Bodies
- Actions
- Ragdolls

In the real world, the laws of physics govern everything from the smallest subatomic particle to the largest galaxy far, far away. Luckily for us, we don’t have to understand quantum mechanics, Newtonian physics, or Euclidean space in order to make a fun game. A physics engine handles game events such as collision detection between objects, moves objects in a physically realistic way, and even deforms objects as if they are made up of a soft material.

A physics engine moves things based on a set of predefined rules so that you, the artist, don’t have to manually animate every object interaction. Compared to traditional keyframe animations, which are premade, the dynamic nature of the physics engine means that it is inherently non-deterministic. The motion of the object depends on the physical property of the object and its state in the physical world. This unique property makes games that utilize real-time physics fun to play around with, if not unpredictable sometimes.

As usual, this chapter comes with a collection of example files that showcase what the physics engine can do. You can find them in the folder /chapters6/demos.

UPBGE includes advanced physics simulation in the form of the Bullet Physics Engine (Bullet Physics). Most of your work will involve setting the right properties on the objects in your scene, then you can sit back and let the engine take over. The physics simulation can be used for games, but also for animation.

UPBGE is based on rigid body physics, which differs significantly from the complementary set of tools available in the form of soft body physics simulations. Though the UPBGE does have a soft body type, it is not nearly as advanced as the non-BGE soft body. The inverse is even more true: it is difficult to get the non-BGE physics to resemble anything like a stiff shape. Rigid body physics does not have, as an effect or a cause, any mesh deformations. For a discussion on how to partially overcome this, see: Mesh Deformations.

Because physics is such an integral part of the Blender game engine, physics-related settings are found in many different places. However scattered they might look at first glance, there is a pattern in this chaos.

The physics settings can be broken down into these sections:

World settings: The world or global Physics Engine settings can be found in the World Properties, which include the Gravity strength constant and some important engine performance tweaks.

World Properties Editor

Object Physics settings: Any game-engine object (mesh, lamp, camera, empty, and text) can be turned into a physical object. Once physics is enabled for an object, it starts obeying the rules of the physics engine, transforming the object from a static object into something that falls, collides, tumbles, and deforms. Figure 6.3 shows the Physics Properties Editor.

Physics Properties Editor

Material Physics settings: The Material panel is not only a place where all the graphic magic happens; it also contains additional physics that control how the surface of the object behaves. Settings such as surface friction can be found here. Because an object can have multiple materials, material physics settings allow the artist to assign different surface materials for different parts of a single object. These seetings are meant to be used in conjunction with the object physics settings, not replace it. Figure 6.4 shows the Material Properties Editor.

Material Properties Editor

Constraints: Physics constraints allow you to set up simple rules that the objects follow, rules such as tracking one object to another or limiting their range of motion. With constraints, it’s possible to realistically represent many of the structures that have a limited degree of motion, such as hinges, wheels, and chains.

It is imperative to understand that the Blender constraints generally do not work inside the BGE. This means interesting effects such as Copy Rotation are unavailable directly.

Your options include:

Parenting - but not Vertex Parenting.

Rigid Body Joint - this is the one constraint that you can set up through the UI that works in the BGE. It has several options, and can be very powerful - see ITS page for a detailed description and demo blend-file. Do not forget that you can loop through objects using bpy instead of clicking thousands of times to set up chains of these constraints.

Rigid body joints on-the-fly - you can add/remove them after the BGE starts by using bge.constraints.createConstraint(). This can be good either to simply automate their setup, or to truly make them dynamic. A simple demo can be viewed in: TODO_FIXME

Python Controllers - as always, in the BGE, you can get the most power when you drop into Python and start toying with the settings directly. For instance, the Copy Rotation mentioned above is not hard - all you have to do is something to the effect of:

Object Constraints Properties Editor

Physics sensors and actuators: Except for maybe the case of a Rube Goldberg machine, where everything happens in a predetermined manner, most games would be pretty boring if there were no way to make an object move at a user’s command or to trigger a reaction when two objects collide. Actuators and sensors fulfill these two roles, respectively. Actuators are part of logic brick that carries out an action (such as applying a force to the object to make it move). Sensors are triggers that detect when something happens in the game, such as when two objects touch. A combination of sensors and actuators makes a game truly interactive, by giving the game engine the ability to make decisions. Figure 6.6 shows the Logic Brick Editor. In case you forgot, there is a full chapter in this book about logic bricks.

Python: In addition to all the physics settings one can access from the graphic user interface, an extensive Python API is at your disposal. The Python API gives you programmable control over many aspects of the physics engine. With Python, you can dynamically set many of the physics options while the game is running. It even allows you to accomplish a few things that are not possible from the graphic interface. For instance, Python can be used to create realistic vehicle physics. Figure 6.7 shows the Text Editor with a Python script open.

So now that you have an overview of what physics is all about and where to find all the settings, the rest of the chapter will explain how to use these settings in combination to achieve various effects.

Physics Visualization

Go to Game > Show Physics Visualization to show lines representing various attributes of the Bullet representation of your objects. Note that these might be easier to see when you turn on Wireframe Mode Z before you press P. Also note that you can see how the Bullet triangulation is working (it busts all your Quads to Tris at run-time, but the BGE meshes are still quads at run-time).

RGB/XYZ Widget - representing the object’s Local Orientation and Origin.

Green - “sleeping meshes” that are not moving, saving calculations until an external event “wakes” them.

White - white lines represent active bounding meshes at are undergoing physics calculations, until such calculations are so small that the object is put to rest. This is how you can see the effects of the Collision Bounds.

Thick, or Many White Lines - a compound collision mesh/meshes.

Violet - bounding meshes for soft bodies.

Red - the bounding box, the outer boundary of object. It is always aligned with global X, Y and Z, and is used to optimize calculations. Also represents meshes that have been forced into “no sleep” status.

Black - when in wireframe, this is your mesh’s visual appearance.

If you want finer-grained control over the display options, you can add this as a Python Controller and uncomment whichever pieces you want to see:

For all debug modes, see API docs for bge.constraints.

A shot of Manual-BGE-Physics-DancingSticks.blend with Game > Show Framerate and Profile enabled.

If you enable Game > Show Framerate and Profile, it will put some statistics in the upper left area of the game window.

These can be very informative, but also a bit cryptic. Moguri has elaborated on their meanings: Moguri’s blog.

As mentioned above, rigid body physics do not affect mesh deformations, nor do they account for them in the physics model. This leaves you with a few options:

You can try using a Soft Body, but these are fairly hard to configure well.

To use an Action Actuator to do the deformation, you have to make a choice. If you use shape keys in the Action, you will be fine as far as the overall collisions (but see below for the note on reinstancePhysicsMesh()). The mesh itself is both a display and a physics mesh, so there is not much to configure.

To use an armature as the deformer will require a bit of extra thought and effort. Basically the armature will only deform a mesh if the armature is the parent of that mesh. But at that point, your mesh will lose its physics responsiveness, and only hang in the air (it is copying the location/rotation of the armature). To somewhat fix this you can then parent the armature to a collision mesh (perhaps a simple box or otherwise very low-poly mesh). This “Deformation Mesh” will be the physics representative, being type: Dynamic or Rigid Body, but it will be set to Invisible. Then “display mesh” will be the opposite set to No Collision, but visible. This still leaves the problem mentioned in the previous paragraph.

When you deform a display mesh, it does not update the corresponding physics mesh. You can view this evidently when you enable physics visualization (Visualizing Physics) – the collision bounds will remain exactly as when they began. To fix this, you must call own.reinstancePhysicsMesh() in some form. Currently this only works on Triangle Mesh bounds, not Convex Hull.

We have prepared a demonstration file in Manual-BGE-Physics-DancingSticks.blend. Note that, we had to increase the World ‣ Physics ‣ Physics Steps ‣ Substeps to make the collisions work well. The more basic case is the case the Shapekeyed Action, which you can see in the back area of the scene. Since it is the only object involved, you can call reinstancePhysicsMesh() unadorned, and it will do the right thing.

The more complicated case is the Collision Mesh ‣ Armature ‣ Display Mesh cluster, which you can see in the front of the scene. What it does in the blend-file is call reinstancePhysicsMesh(viz), that is, passing in a reference to the visual mesh. If we tried to establish this relationship without the use of Python, we would find that Blender’s dependency check system would reject it as a cyclic setup. This is an example of where Blender’s checking is too coarsely-grained, as this circle is perfectly valid: the grandparent object (the collision mesh) controls the location/rotation, while the middle object (the armature) receives the animated Action, where the child (the Display Mesh) receives the deformation, and passes that on up to the top, harmlessly. Something to note is that the collision mesh is merely a plane – that is all it requires for this, since it will be getting the mesh data from viz.

A third option is to create your items out of many sub-objects, connected together with rigid body joints or similar. This can be quite a bit more work, but the results can be much more like a realistic response to collisions. For an add-on that can help you out in the process, check out the Blender Ragdoll Implementation Kit.

Sometimes you will want to look at:

The main Bullet Physics page

Beyond gaming, sometimes you wish to render a complex scene that involves collisions, multiple forces, friction between multiple bodies, and air drag or even a simple setup that is just easier to achieve using the real-time physics.

Blender provides a way to ‘’bake’’ or ‘’record’’ a physics simulation into keyframes allowing it then to be played as an action either for animation or games. Keep in mind that the result of this method is a recording, no longer a simulation. This means that the result is completely deterministic (the same every time it is run) and unable to interact with new objects that are added to the physics simulation after it was recorded. This may, or not, be desired according to the situation.

Menu to record Keyframes to the Dope Sheet

All you have to do to achieve this effect is to execute the following script:

it will lock away your keyframes for use in Blender Render mode. You can go back to the 3D View and press Alt-A to play it back, or Ctrl-F12 to render it out as an animation.

Note that you can also use Game Logic Bricks and scripting. Everything will be recorded.

Resulting recorded animation

Record Animation keys redundant data (data that did not change relative to the last frame). Pressing O while in the Dope Sheet will remove all superfluous keyframes. Unwanted channels can also be removed.

Cleaned up recording

You can snapshot the physics world at any time with the following code:

This will allow importing into other Bullet-based projects. See the Bullet Wiki on Serialization for more.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (unknown):
```unknown
own.worldOrientation =
bge.logic.getCurrentScene().objects['TheTargetObject'].worldOrientation
```

Example 2 (unknown):
```unknown
own.worldOrientation =
bge.logic.getCurrentScene().objects['TheTargetObject'].worldOrientation
```

Example 3 (unknown):
```unknown
own.worldOrientation =
bge.logic.getCurrentScene().objects['TheTargetObject'].worldOrientation
```

Example 4 (python):
```python
import bge

debugs = (
   bge.constraints.DBG_DRAWAABB,
   )
for d in debugs:
   bge.constraints.setDebugMode(d)
```

---

## Introduction

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/controllers/introduction.html

**Contents:**
- Introduction
- Controller Types

The controllers are the bricks that collect data sent by the sensors, and also specify the state for which they operate. After performing the specified logic operations, they send out pulse signals to drive the actuators to which they are connected.

When a sensor is activated, it sends out a positive pulse, and when it is deactivated, it sends out a negative pulse. The controllers’ job is to check and combine these pulses to trigger the proper response.

The logic blocks for all types of controller may be constructed and changed using the Logic Editor; details of this process are given in the Controller Editing page.

There are eight types of controller logic brick to carry out the logic process on the input signal(s). This table gives a quick overview of the logic operations performed by the logical controller types. The first column, input, represents the number of positive pulses sent from the connected sensors. The following columns represent each controller’s response to those pulses. True means the conditions of the controller are fulfilled, and the actuators it is connected to will be activated; false means the controller’s conditions are not met and nothing will happen. Please consult the individual controller pages for a more detailed description of each controller.

It is assumed that more than one sensor is connected to the controller. For only one sensor, consult the “All” line.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introduction

**URL:** https://upbge.org/docs/latest/manual/manual/python_components/introduction.html

**Contents:**
- Introduction
- What Is A Python Component?
- Python Component Creation
- Create Component
- Add Component

The idea of a component is a simple one. They are modules that can be attached to game objects. You can attach as many as you want, and each one serves a specific purpose such as third person character movement with WASD keys. After a component has been attached to an object, it can have various exposed settings that you can edit. In the case of a third person movement component, this could be things such as movement speed and turn speed.

Python Component (Vehicle Wheeled template)

Python component can be compared to python logic bricks with parameters. The python component is a script loaded in the UI, this script defined a component class by inheriting from KX_PythonComponent. This class must contain a dictionary of properties: args and two default functions: start() and update(). Additionally, the component can include an optional function: dispose().

The script used to create the component must have .py extension. The component properties are loaded from the args attribute from the UI at loading time. When the game start the function start() is called with as arguments a dictionary of the properties’ name and value. The update() function is called each frame during the logic stage before running logics bricks. The goal of this function is to handle and process everything.

The following component example moves and rotates the object when pressing the keys W, A, S and D.

The standard property types supported are float, integer, boolean, string, set (for enumeration) and Vector 2D, 3D and 4D. The following example shows all of these property types:

Additionally, the following data (ID) property types are supported too:

Data (ID) Property Types supported

The optional dispose() function is called when the component is destroyed. It is only necessary in very specific cases.

Inside of UPBGE there are several python component templates that can help us with common tasks. We will analyze them in the next subchapters.

The Python Component panel, or also called Game Component panel, is placed in the Properties editor under the Game Object Properties tab.

Game Component panel

You will find there two ways to make a Python Component in UPBGE, Add and Create.

2 ways to make a Python Component

When you click Create button a panel will appear. In that panel you can write the component module and the class name, separated by a dot. Clicking on the Ok button, a new python script with the name of the component’s module will be created in the script editor. That python script will contain an empty class which name will be the one entered previously.

Create Component process

As the component script is developed you can click on the component reload option to see the updated component.

Python Component reload process

This process is the opposite of the previous one. First of all, we already have a python script previously formatted as a component that can be placed either in the script editor or at the same level as the .blend file.

When we click the Add button we will have to enter the name of the python script (without the .py), followed by a dot and the class name. After clicking Ok the Python Component will be created.

Add Component process

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (python):
```python
import bge
from collections import OrderedDict

class ThirdPerson(bge.types.KX_PythonComponent):
   """Basic third person controls

   W: move forward
   A: turn left
   S: move backward
   D: turn right

   """

   args = OrderedDict([
         ("Move Speed", 0.1),
         ("Turn Speed", 0.04)
   ])

   def start(self, args):
      self.move_speed = args['Move Speed']
      self.turn_speed = args['Turn Speed']

   def update(self):
      keyboard = bge.logic.keyboard.events

      move = 0
      rotate = 0

      if keyboard[bge.events.WKEY]:
         move += self.move_speed
      if keyboard[bge.events.SKEY]:
         move -= self.move_speed

      if keyboard[bge.events.AKEY]:
         rotate += self.turn_speed
      if keyboard[bge.events.DKEY]:
         rotate -= self.turn_speed

      self.object.applyMovement((0, move, 0), True)
      self.object.applyRotation((0, 0, rotate), True)
```

Example 2 (python):
```python
import bge
from collections import OrderedDict

class ThirdPerson(bge.types.KX_PythonComponent):
   """Basic third person controls

   W: move forward
   A: turn left
   S: move backward
   D: turn right

   """

   args = OrderedDict([
         ("Move Speed", 0.1),
         ("Turn Speed", 0.04)
   ])

   def start(self, args):
      self.move_speed = args['Move Speed']
      self.turn_speed = args['Turn Speed']

   def update(self):
      keyboard = bge.logic.keyboard.events

      move = 0
      rotate = 0

      if keyboard[bge.events.WKEY]:
         move += self.move_speed
      if keyboard[bge.events.SKEY]:
         move -= self.move_speed

      if keyboard[bge.events.AKEY]:
         rotate += self.turn_speed
      if keyboard[bge.events.DKEY]:
         rotate -= self.turn_speed

      self.object.applyMovement((0, move, 0), True)
      self.object.applyRotation((0, 0, rotate), True)
```

Example 3 (python):
```python
import bge
from collections import OrderedDict

class ThirdPerson(bge.types.KX_PythonComponent):
   """Basic third person controls

   W: move forward
   A: turn left
   S: move backward
   D: turn right

   """

   args = OrderedDict([
         ("Move Speed", 0.1),
         ("Turn Speed", 0.04)
   ])

   def start(self, args):
      self.move_speed = args['Move Speed']
      self.turn_speed = args['Turn Speed']

   def update(self):
      keyboard = bge.logic.keyboard.events

      move = 0
      rotate = 0

      if keyboard[bge.events.WKEY]:
         move += self.move_speed
      if keyboard[bge.events.SKEY]:
         move -= self.move_speed

      if keyboard[bge.events.AKEY]:
         rotate += self.turn_speed
      if keyboard[bge.events.DKEY]:
         rotate -= self.turn_speed

      self.object.applyMovement((0, move, 0), True)
      self.object.applyRotation((0, 0, rotate), True)
```

Example 4 (python):
```python
from bge import *
from mathutils import *
from collections import OrderedDict

class Component(types.KX_PythonComponent):
args = OrderedDict([
      ("Float", 58.6),
      ("Integer", 150),
      ("Boolean", True),
      ("String", "Cube"),
      ("Enum", {"Enum 1", "Enum 2", "Enum 3"}),
      ("Vector 2D", Vector((0.8, 0.7))),
      ("Vector 3D", Vector((0.4, 0.3, 0.1))),
      ("Vector 4D", Vector((0.5, 0.2, 0.9, 0.6)))
])

def start(self, args):
   print(args)

def update(self):
   pass
```

---

## Introduction

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/actuators/introduction.html

**Contents:**
- Introduction
- Common Options

Actuators perform actions, such as move, create objects, play a sound. The actuators initiate their functions when they get a positive pulse from one (or more) of their controllers.

The logic blocks for all types of actuator may be constructed and changed using the Logic Bricks Editor; details of this process are given in the Actuator Editing page.

Common Actuator options

All actuators have a set of common buttons, fields and menus. They are organized as follows:

Collapses the sensor information to a single line (toggle).

Specifies the type of the sensor.

The name of the actuator. This can be selected by the user. It is used to access actuators with Python; it needs to be unique among the selected objects.

Display the actuator even when it is not linked to a visible states controller.

Move the actuator up or down over other actuators within the column.

When unchecked the actuator is deactivated, no action will be done. Very useful to check different logics without unlink or delete the actuator.

Deletes the actuator.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introduction

**URL:** https://upbge.org/docs/latest/manual/manual/introduction/index.html

**Contents:**
- Introduction

This section gives an overview of UPBGE’s capabilities, features, history and some differences between it and BGE, but not directly comparing UPBGE to BGE.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introduction

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/introduction.html

**Contents:**
- Introduction
- Logic Bricks
- Properties
- States
- Architecture

What makes a game different than a movie? Let’s see. In both you can find yourself buried in a comfortable seat eating junk food and alienated from the world. And funny 3D goggles are not exclusive to either. But what about interactivity? In a game you can control a player and interact with the virtual (or real!) world and the game elements. The story can be dynamically created in front of your eyes.

Therefore, as a director and content creator you will play different roles in a movie or a game. In a movie, for example, you have to direct the flow of the story, but for a game, you have to direct how the player controls and experiences this flow. More than ever, it’s time to narrow the gap between what technology can deliver and what the public can experiment with and assimilate as part of their own nature. It is necessary to give all the power to the user.

Traditionally, to design your game interaction in the past, you would have needed coding expertise and a highly technical background. If, as a creative artist, any words such as technical, code, or programming scare you, Have confidence! “Pure artists” are still scared with code. The idea here is not that they will no longer be afraid of it. Instead, with the UPBGE they will not have to face their fears. Logic Bricks are an alternative to hardcore coding, known to be “artists friendly” more. Logic Bricks is here to rescue you. Logic Bricks is a visual set of tools responsible for integrating the game components together. By using Logic Bricks, you can determine what to do after a mouse click, when to play an animation, how to move your character, and so on, as shown in following picture.

Logic Bricks is high level visual programming.

Logic Bricks system is the default “scripting” layer in the Game Engine. Each Game Object in the game may store a collection of logical components (Logic Bricks) which control its behavior within the scene. Logic bricks can be combined to perform user-defined actions that determine the progression of the simulation.

The main part of Logic Bricks system can be set up through a graphical interface, the Logic Bricks Editor, and therefore does not require detailed programming knowledge. Logic is set up as blocks (or “bricks”) which represent preprogrammed functions; these can be tweaked and combined to create the game/application.

Logic Brick system is composed of three main elements: Sensors, Controllers and Actuators. Sensors are an event system used to trigger an action upon a specific event (for example, an object collides with another object or the joystick is used). Once one or more sensors is triggered, you can use a controller to control whether or not this set of events will produce an event in the game (and which effect). Controllers work as logic pipes, evaluating sensors through simple logic conditions, such as And, Or, and Not. Finally, when a controller validates a set of sensors, it will activate an actuator. An actuator is responsible for a specific action of the game (such as ending the game, moving an object, and so on).

In this chapter, we’ll cover sensors, controllers, and actuators in detail specifically, how and when to use them. Additionally, you will learn about object game properties, the State Machine system, how the interface works, and the architecture of the system as a whole. As a system used to build new worlds, this is no place for do’s and don’ts. It will be up to you to find the best set of features that fits your project and creativity. Nevertheless, when possible, we’ll present suggestions of when and how people have used the tools in the past, but you don’t have to feel constrained by that. Treat Logic Bricks as small Lego pieces and surprise us and yourself.

Logic Bricks are really easy and quick to use. You can make entire games with them with absolutely no need for coding.

Properties are like variables in other programming languages. They are used to save and access data values either for the whole game (e.g. scores), or for particular objects/players (e.g. names). However, in the UPBGE, a property is associated with an object. Properties can be of different types, and are set up in a special area of the Logic Editor.

Another useful feature is object States. At any time while the simulation is running, the object will process any logic which belongs to the current state of the object. States can be used to define groups of behavior – e.g. an actor object may be “sleeping”, “awake” or “dead”, and its logic behavior may be different in each of these three states. The states of an object are set up, displayed and edited in the Controller logic bricks for the object.

The game engine was designed to revolve around game objects. Twenty years ago, when it was first developed, this was a breakthrough design. The idea of having events controlled per object, as opposed to a central controller, worked well for the early days of 3D engines. Nowadays, some people may advocate that controlling elements per object is less scalable and more difficult to manage. That will be up to you to decide. Regardless of your thoughts on that subject, the game engine still allows you to emulate a centralized controlling system, while giving autonomy to each object to deal with its own business. Part of this flexibility is due to the hooked-up Python layer and the Logic Brick system. Through the Python interface, you can replace or at least control most of the effects and logic setups you create with Logic Bricks. With Logic Bricks, you can quickly set up a system that is easy to visualize, implement, and test. The strength of the game engine comes from the trade-off between the two sibling systems. A flexible design may lack features and performance compared to specific engines. Nevertheless, the different kinds of applications you can prototype and develop quickly with the game engine make up for the compromise.

If you look at a level deep into the object structure, you will find that the architecture of the Logic Bricks system is “controller-centric.” It revolves around the controllers of the game because they are the ones to determine what do to with the sensors and what actuators to activate. This doesn’t have to be followed strictly, but based on this design, you will want to keep your sensors and actuators to a minimum and optimize their usage with the controllers. Actually, in order to optimize the performance, the game engine disables any sensor and actuator that is unlinked to a controller or linked to a controller in a non-active state. This is one of the (many) reasons why Python controllers are so popular. They allow you to replace the use of multiple sensors and actuators by direct calls to their equivalents in the source code. The chapter Python Scripting is entirely dedicated to that aspect of the game engine, and will complement the applications of Logic Bricks discussed in this chapter.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Introduction to Scripting

**URL:** https://upbge.org/docs/latest/manual/manual/python_scripting/introduction.html

**Contents:**
- Introduction to Scripting
- Why Script When You Can Logic Brick It?
- Sane Replacement for Large-Scale Logic-Bricked Objects
- Better Handling of Multiple Objects
- Access to UPBGE’s Advanced Features
- Use Features That Are Not Part of UPBGE
- Keep Track of Your Changes with a Version Control System
- Debug Your Game While It Runs
- So What Exactly Is Python?
- Flexible Data Types

Congratulations, you finally arrived at one of the most technical parts of the manual. Keep that in mind in case you get lost.

The UPBGE game engine was once famous for letting you create a full game without touching a single piece of code. Although this may sound attractive, it also leads to a very limited game-making experience. Logic bricks, as presented in Logic Bricks chapter, are very handy for quick prototyping. However, once you need to access advanced resources, external libraries and devices, or simply optimize your application, a programming language becomes your new best friend.

Through the use of a scripting language called Python, the game engine (as UPBGE itself) is fully extensible. This programming language is easy to learn, although extremely powerful. Be aware, though, that you will not find a complete guide to learning Python here. There are plenty of resources online and offline that will serve you better. However, even if you are not inclined to study Python deeply now, sooner or later you will find yourself struggling with script files. So, it’s important to know what you are dealing with.

For those experienced Python programmers (or for those catching up with the reference learning material), always remember: if you can do something with Python, chances are, you can do it in the game engine.

After the brief overview in the Python basics, we will explain how to apply your knowledge of Python inside the game engine. You’ll also learn how to access the Python methods, properties, and objects you’ll be using.

We can compare logic bricks with real bricks. On the one hand, we have strong elements on which to build our system, but, on the other hand, we have a system as flexible as a blind wall.

There are many occasions when the same effect can be achieved in different ways. Different phases of the production may also require varied workflows. The reason for picking a particular method is often personal. Nevertheless, we present here a few arguments that may convince you to crack a good Python book and start learning more about it:

Sane replacement for large-scale logic-bricked objects.

Better handling of multiple objects.

Access to UPBGE’s advanced features.

Use features that are not part of UPBGE.

Keep track of your changes with a version control system.

Debug your game while it runs.

Logic Brick, the Necessary Good

You can’t ever get away from logic bricks. Even when using Python exclusively for your game, you will need to invoke the scripts from a Python controller. The ideal is to find the balance that fits your project.

It’s always good to have an excuse to show an image in a programming chapter, and here it is. In the next pìcture you see the logic bricks for Frankie, the main character of the open game Yo Frankie!

This system is well organized: different actions belong to different states and sensors; controllers and actuators are properly named. Nevertheless, it’s not hard to lose yourself trying to understand which sensor connects to which controller. One of the reasons for such a complex project to rely on logic bricks is because Yo Frankie! serves as a didactic project for artists wanting to start with the game engine. Anyone with a little programming experience can take the files and expand the game freely. (Have you tried it yet?)

However, you often aim for performance and workflow. Having everything centralized in a single script file can save you a lot of time.

Another important aspect while working is to document your project. It’s easy to open a file only a few months old and find yourself completely lost. Script files, on the other hand, are naturally structured to be self-documented. To document logic bricks, you need to rely on text files inside or outside your Blender files (and neat image diagrams). It’s definitively not as handy as inline comments along your code. (Code diagrams can still be useful, but that’s a different topic.)

Big projects lead to multiple files, this is an inevitable truth. Even when you use external linking and libraries, it’s crucial to optimize the time spent in changing multiple sets at once. This is one of the weaknesses of logic bricks, they make it hard to automatically change a big range of elements at the same time.

If you need to change a property name or initial value of an object, you will need to repeat that change in other instances of the same. We have ways to make it easier by using copy and paste of logic bricks/properties between objects or even through logic sharing. Nevertheless, you will still have to update all the Property sensors, controllers, and actuators that may rely on the old value. That’s especially true for objects with logic bricks across them, as we saw, the game engine allows you to link logic bricks from different objects. However, self-contained objects/logic bricks are easier to work with (and with less spaghetti).

If you thought that before picture was a mess, try to make sense of next picture. Here we have the logic bricks of Frankie, plus the objects that have logic bricks connected to it. As you recall, you can restrict the visible logics through the Show Panel option, but this illustrates how difficult it is to get a global view of your system.

Once you start to work with scripts, you will see how easy it is to assume control over all your scene elements in a global way. It will give you lots of benefits in the long run.

You will be happy to know that the game engine has a powerful set of features beyond those found in the logic brick’s interface. Also, almost all the functionality found in the logic bricks can be accomplished through an equivalent method of the game engine API (which will be covered in the section “Using the Game Engine API - Application Programming Interface”). The API ranges from tasks that could be performed with logic bricks, such as to change a property in a sensor or to completely remove an object from the game, all the way to functionality not available otherwise, such as playing videos and network connection.

There are a few reasons for not having all the methods accessible through logic bricks. First, a graphic interface is very limited for complex coding. You may end up with a slow system that is far from optimized. Second, having methods independent from the interface allows it to be expanded more easily and constantly (from a development point of view). Some advanced features, such as mirroring system, dynamic load of meshes, OpenGL calls, and custom constraints would hardly fit in the current game engine interface. They would probably end up not being implemented because of the amount of extra work required. Other things you will find in the game engine built-in methods are: make screenshots; change world settings (gravity, logic tic rates); access the returned data from sensors (pressed keys, mouse position); change object properties (camera lens, light colors, object mass); and many others we will cover in the course of this chapter.

No man is an island. No game is an island either (except Monkey Island). And the easiest way to integrate your UPBGE game with the exterior world is with Python. If you want to use external devices to control the game input or to tie external applications to your game, you may find Python suitable for that task.

Here are some examples that showcase what can be done with Python external libraries:

Grab data off the Internet for game score.

Control your game with a Nintendo Wiimote controller.

Combine Head-tracking and immersive displays for augmented reality.

Those possibilities go with the previous statement that almost everything that you can do with Python, you can do in the game engine. And since Python can be used with modules written in other languages (properly wrapped), you can virtually use any application as a basis for your system.

Cross-Platform, Yes; Cross-Version, Not

To use external libraries, you must know the Python version they were built against. The Python library you are using must be compatible with the Python version that comes with your UPBGE. It’s also valuable to check how often the library is updated and if it will be maintained in the future.

If you take a Blender file in two different moments of your production, you will have a hard time finding what has changed between them. This is because UPBGE/Blender’s native file format is a binary type. Binary files are written in a way that you can’t get to them directly, they are designed to be accessed by programs and not by human beings.

Scripts, on the other hand, are plain text files. You can open a script in any text editor and immediately see the differences between two similar files. Finding those differences are vital to going forward and backward with your experimentations during work. Actually, if you don’t want to check for differences manually, you may want to consider using external script files with a version control system such as Git, SVN, Mercury, or CVN.

This works only for scripts maintained outside UPBGE. This is one of the strong reasons to prefer Python Module controllers as opposed to Python Script controllers.

A version control system allows you to move between working versions of your project files. It makes it relatively safe to experiment with different methods in a destructive way. In other words, it’s a system to protect you from yourself. In next image, you can see an application of this. Someone changed the script file online while we were working locally on it. Instead of manually tracking down the differences, we could use a tool to merge both changes into a new file and commit it.

Interpreted languages (also known as scripting languages) are slower than compiled code. Therefore, to speed up their performance they are precompiled and cached the first time they run (when you launch your game). This is not mandatory, though, and if you are using external Python scripts (instead of those created inside UPBGE), you can use the debugging button to have them reloaded every time they are called.

In next figure, we have the reload.reload_me module that will be reloaded every frame. That way you can dynamically change the content of your scripts, variables, and functions without having to restart the game. Try it yourself: download the example 001_reloadme.zip to your computer, extract it and launch debug_python.blend. Play your game, and you will see a spinning cube. The speed of the cube is controlled by the 14th line of the file reload.py, found in the same folder.

Debugging button at Python Module controller

Without closing UPBGE or even stopping your game, open the file script.py in a text editor, change this line to 0.05, for example, and save it. You will see the speed changing immediately. Your game is literally being updated at runtime, and you can change any module that’s been called with the debug option on.

Turn It Off When You Leave

Remember to turn debugging off when you are done with this script. Reloading the script every frame can drastically reduce your performance.

Now that you are aware of all the benefits of using Python, it’s time to understand what Python is. Once again, we can’t go over all the aspects of the language here. Nevertheless, a general overview is still desirable to help you understand the examples presented in this book.

To study your scripts, you must be aware of the following aspects:

OOP, Object-Oriented Programming.

Whenever you write a program, you have to use variables to store changing values at runtime. Unlike languages such as C and Java, Python variables are very flexible: they can be declared on the fly when you first use them; you can assign different data types for the same variable; and you can even name them dynamically:

This snip of code is the equivalent to the following:

As you can see, the variable names are created at runtime. Therefore, if you name your objects correctly in the Blender file, you can store them in variables named after them. The following code snip assigns the scene objects (retrieved from the game engine) to variables named after their names.

Although we have flexible data types, we must respect variable types while manipulating and passing/returning them to functions. Here you can see a list of the data types you will find in the UPBGE game engine API:

Integer: This is the most common of the numerical types. It can store any number that fits in your computer memory. You can perform any regular math operations on it, such as sum, subtraction, division, modulus, and potency.

Float: This type is very similar to integers, but has a range of numbers that includes fractions. If you divide an even number by its half, Python will automatically convert your integer to a float number.

Boolean: As simple as it sounds, this data type stores a true or a false value. It can also be understood as an integer with the value of 1 or 0.

List: A list contains a conjunct of elements ordered by ascending indexes. Although the size of a list can change on the fly, you can’t access a list index that wasn’t created yet (this will crash Python). List can have mixed elements such as integers, strings, and objects.

Tuple: This is another kind of list where elements can’t be overwritten. As with lists, you can read them using indexes. But it’s more common to access all the values at once, assigning them to different variables.

String: Whenever you need to store a text, you will use strings. As words are a combination of individual letters, a string consists of individual characters. Indeed, strings can be understood as a list of characters because you can access them using their location index, though you can’t overwrite them (like in a tuple).

Dictionary: Like a list, a dictionary can store multiple values. Unlike a list, a dictionary is not based on numerical index access. Therefore, we have strings working as “keys” to store and retrieve the individual variables. In fact, anything can be a key to a dictionary, a number, an object, a class …

Custom Types: These are things such as vectors and matrixes. The game engine combines some of the basic data types to create more complex ones. They are mainly used for vectors and matrixes. That way you can interact mathematically with them in a way that basic types won’t do.

Indentation, the amount of white spaces or tabs you leave before a new line.

When coding in a particular programming language, it’s mandatory to follow its general syntax. In that regard, Python is one of the most restricted languages out there. Think of this as a tough grammar exam. You won’t be able to score high unless you follow all the pre-established grammar rules. Now imagine that it could be even worse, as bad as a written legal document. We are talking about strict paragraphs, indentation, information hierarchy, and similar rules.

As in a legal document, those rules have a raison d’etrê. With strict form/syntax, you can focus more on the content of the text. And ambiguity in the context of code making is fatal.

Indentation is the most important aspect of Python syntax. Python code uses the indentation level to define where loops, functions, and general nesting start/end. Take a look at this example:

Here we are defining a function (1–2), calling a built-in print function (3), defining another function (4–5), calling another built-in print function (6), and finally calling the first function we declared (7).

The output of such script will be:

I’m outside the function.

I’m still outside the function.

I’m inside the first function.

The first thing you may notice is that Python runs from top to bottom. Therefore, you must define your function before you call it. Secondly, you can see that the second function is never called. So how can the code interpreter determine which print statements to call? The answer is: indentation! Whenever you change the indentation level (lines 1–2, 2–3, 4–5, and 5–6), you determine the hierarchical relation between the elements. Therefore line 2 belongs to the function defined in line 1, line 5 to line 4, and the other lines are all at the same level.

Python pep-8 standard recommends to use spaces for identation. In the manual we will use 2 spaces identation.

Pound Sign, I (Finally) Love You

If, like me, you never understood the reason for the number/pound sign key (#) on your phone, you will eventually find it very useful. In Python, any text to the right of a pound sign is ignored by the interpreter. Therefore, the pound sign is used to add commentaries to your code or to temporarily deactivate part of it.

Since games deal with 3D world objects, it makes sense to use a language that is oriented to them. The game engine itself is written in C++, a very strong and object-oriented language, and Python OOP capabilities let you handle the game data in a Python-native way. It reflects in the game engine objects having their own set of functions and variables directly accessed from a Python API (to be explained later in this chapter in the section “Using the Game Engine API - Application Programming Interface”).

In the Python code, you can (and will) create your own classes, modules, and elements. For example, you may want to control some 3D elements as a group defined by your code. It will make it easy to get to all of them at once. Therefore, you can have a custom class that will store all the related objects you want to access and preserve some properties as a group.

Download the example 002_oop.zip, extract it and load the oop.blend file.

The first script that runs in this file is the init_world.py. Here we are creating two groups to store different kind of elements (cube and sphere). In order to sort the objects between the groups, we go over the entire scene object list and check for objects with a property “cube” or “sphere” and append them to their respective lists.

After storing them in the global module bge.logic, we wait for the user to click in the cube or sphere in the middle of the scene. When that happens, it will toggle the value of the on/off property of the cube or sphere. The following script (which runs every frame) will then hide/unhide the group’s objects accordingly.

And we are done with this interaction. Play with the file by adding new elements (tubes, planes, monkeys) and make them interact as we have here. A few copies and pastes should be enough to adapt this code to your new situation. Remember to note the current indentation used.

If you have previous experience with another programming language, you will learn Python in no time. If you go over some basic Python tutorials, look at some script examples, and check the UPBGE game engine API, that might be enough. But if learning Python is your first step into coding experience, don’t worry. Take the time to read through the basics of the language, start with the simplest tasks, and never give up.

Usually, a good way to start is tweaking ready-to-use scripts, which doesn’t require you to understand all the aspects of the language before your first experiments. Also, it gives you a good motivational boost by producing quick results for your efforts. We recommend you first learn Python and then focus on its application in the game engine. But you may be more comfortable messing with game engine files first and then later learning Python more deeply.

Below are some websites where you can learn more about Python.

http://www.python.org/ and https://docs.python.org/3/tutorial/index.html

Learn about new Python versions, API changes, and module documentation.

https://upbge.org/docs/latest/api/

Official Blender + UPBGE API Documentation, all the built-in modules that can be used with the game engine.

www.blenderartists.org/forum

Blender Artists forum, you can find good script examples in the Python section (general Blender Python) and in the game engine section.

http://www.diveintopython3.net

Dive Into Python 3 covers Python 3 and its differences from Python 2. A complete book available online.

https://www.learnpython.org/

This interactive tutorial website offers a great introduction to Python for beginners.

Books, there are plenty of them in your nearby library.

You can also access help directly in Python.

The Python function “dir” creates a list with all the functions/modules/attributes available to be accessed from this object.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (sql):
```sql
# edit the speed value and you will see the rotation changing

# (try with values from 0.01 to 0.05)

speed = 0.025
```

Example 2 (sql):
```sql
# edit the speed value and you will see the rotation changing

# (try with values from 0.01 to 0.05)

speed = 0.025
```

Example 3 (sql):
```sql
# edit the speed value and you will see the rotation changing

# (try with values from 0.01 to 0.05)

speed = 0.025
```

Example 4 (bash):
```bash
for i in range(10):
  exec("var_%d = %d" % (i,i))
```

---

## Invert

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/invert.html

**Contents:**
- Invert
- Inputs
- Outputs

Fixed value, or resulting connected value to invert.

Resulting inverted value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Is None

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/is_none.html

**Contents:**
- Is None
- Inputs
- Outputs

True if value is none.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Join Path

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/path/join_path.html

**Contents:**
- Join Path
- Parameters
- Inputs
- Outputs

Join multiple components of a path regardless of operating system.

Will add another socket for additional items.

Full path to the directory.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Joystick Sensor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/types/joystick.html

**Contents:**
- Joystick Sensor
- Properties
  - Stick Directions
  - Stick Axis
  - Shoulder Triggers
  - Buttons
- Example

See the Python reference of this logic brick in SCA_JoystickSensor.

The Joystick Sensor triggers whenever the joystick moves. It also detects events on a range of ancillary controls on the joystick device (shoulder triggers, buttons, etc.). More than one joystick may be used (see “Joystick Index”).

UPBGE maps all the joysticks against the layout of Xbox 360 game controller. This way is easier to setup the different movements or actions because you have to do it for one type of controller only.

See Sensor Common Options for common options.

A menu to select which joystick event to use, each is described later.

Specifies which joystick to use.

Sensor triggers for all events on this joystick’s current type.

Detect movement in a stick.

Joystick Stick Directions

Stick to detect a input: Left Stick/Right Stick.

Direction of the stick moving: Right/Left, Up/Down.

Detects the axis of the joystick.

Which axis either of the sticks are moving on Left Stick Horizontal/Vertical, Right Stick Horizontal/Vertical.

Joystick Shoulder Triggers

Triggers that are used: Left/Right Shoulder Trigger.

Buttons that are used: A, B, X, Y, Dpad Right/Left/Up/Down, Right/Left Shoulder, Right/Left Stick, Start and Guide.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Jump

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/character/jump.html

**Contents:**
- Jump
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which object to use as character.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Keyboard

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/keyboard/index.html

**Contents:**
- Keyboard

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Keyboard Active

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/keyboard/keyboard_active.html

**Contents:**
- Keyboard Active
- Outputs

Detects any activity on the keyboard.

True if keyboard state changed, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Keyboard Key

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/keyboard/keyboard_key.html

**Contents:**
- Keyboard Key
- Parameters
- Inputs
- Outputs

Detects if a specified key has been pressed.

Input detection mode. Tap is activated the first frame that the key is pressed, Down is activated while the key is pressed (even the first frame) and Up is activated once the last frame the key is pressed.

The key to monitor; click & press a desired key.

True if the key is active in the selected mode, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Keyboard Sensor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/types/keyboard.html

**Contents:**
- Keyboard Sensor
- Properties
- Example

See the Python reference of this logic brick in SCA_KeyboardSensor.

The Keyboard sensor is for detecting keyboard input. It can also save keyboard input to a String property.

See Sensor Common Options for common options.

This field detects presses on a named key. Press the button with no label and a key to assign that key to the sensor. This is the active key, which will trigger the TRUE pulse. Click the button and then click outside of the button to deassign the key. A FALSE pulse is given when the key is released.

Sends a TRUE pulse when any key is pressed. This is useful for custom key maps with a Python controller.

Specifies additional key(s), all of which must be held down while the active key is pressed in order for the sensor to give a TRUE pulse. These are selected in the same way as Key. This is useful if you wish to use key combinations, for example Ctrl-R or Shift-Alt-Esc to do a specific action.

Assigns a Bool property which determines if the keystroke will or will not be logged in the target String. This property needs to be TRUE if you wish to log your keystrokes.

The name of property to which the keystrokes are saved. This property must be of type String. Together with a Property sensor this can be used for example to enter passwords.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Key Code

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/keyboard/key_code.html

**Contents:**
- Key Code
- Inputs
- Outputs

Retrieves a specified key’s numeric code. This node is meant for debugging purposes.

The key to translate.

Integer code of the selected key.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Key Logger

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/keyboard/instream.html

**Contents:**
- Key Logger
- Inputs
- Outputs

Records keyboard activity.

Boolean value for condition. todo

True if the node performed successfully, else False.

Character represented by the key pressed (String). For example 'a' will be returned for key A.

Integer code of the recorded key (Integer).

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## LAN Client

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/network/lan_client.html

**Contents:**
- LAN Client
- Parameters
- Inputs
- Outputs

Connect to specified web address at game start.

Condition to be fulfilled for node to activate. todo

IP address to connect to.

Port to use for connection.

If Stop condition is received, connection is cut.

Connection established signal is emitted. todo

True while connected to server. todo

Connection stopped signal is emitted. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## LAN Server

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/network/lan_server.html

**Contents:**
- LAN Server
- Parameters
- Inputs
- Outputs

Connect to specified web address at game start.

Condition to be fulfilled for node to activate.

IP address to connect to.

Port to use for connection.

If Stop condition is received, connection is cut.

Connection established signal is emitted. todo

True while connected to server. todo

Connection stopped signal is emitted. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## License

**URL:** https://upbge.org/docs/latest/manual/manual/contribute/license.html

**Contents:**
- License

UPBGE itself is released under the GNU General Public License.

Except where otherwise noted, the content of the UPBGE Manual is available under a Creative Commons Attribution-ShareAlike 4.0 International License or any later version. Excluded from the CC-BY-SA are also the used logos, trademarks, icons, source code and Python scripts.

This UPBGE manual contains exclusive information from UPBGE Documentation Team but it is also based on others manuals and articles whose authors are exposed below:

This means that when someone contributes to the manual, they don’t hold exclusive copyright to their text. They are of course, acknowledged and appreciated for their contribution. However, others’ can change and improve any or all text in order to keep the manual consistent and up to date.

If you want to use the UPBGE manual in other sites or other formats, please attribute the different authors and include hyperlinks (online) or URLs (in print) to the different manuals as pointed out above.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (unknown):
```unknown
The Blender Manual
by the Blender Documentation Team
is licensed under a CC-BY-SA v4.0.
```

Example 2 (unknown):
```unknown
The "Game Development with Blender" book
by the Mike Pan, Dalai Felinto and other authors
is licensed under a CC-BY-SA v4.0.
```

Example 3 (unknown):
```unknown
The UPBGE Manual
by the UPBGE Documentation Team
is licensed under a CC-BY-SA v4.0.
```

---

## Licensing of Games

**URL:** https://upbge.org/docs/latest/manual/manual/deployment/licensing.html

**Contents:**
- Licensing of Games
- Standalone Games
- More Information

Blender and the UPBGE/BGE are licensed as GNU GPL, which means that your games (if they include Blender software) have to comply with that license as well. This only applies to the software, or the bundle if it has software in it, not to the artwork you make with Blender. All your Blender creations are your sole property.

GNU GPL – also called “Free Software” – is a license that aims at keeping the licensed software free, forever. GNU GPL does not allow you to add new restrictions or limitations on the software you received under that license. That works fine if you want your clients or your audience to have the same rights as you have (with Blender).

In summary, the software and source code are bound to the GNU GPL, but the blend-files (models, textures, sounds) are not.

In case you save out your game as a single standalone (using addons for this purpose, for example), the blend-file gets included in the binary (the Blender Player). That requires the blend-file to be compatible with the GNU GPL license.

In this case, you could decide to load and run another blend-file game (using the Game Actuator logic brick). That file then is not part of the binary, so you can apply any license you wish on it.

More information you can find in the blender.org FAQ.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Lights

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/lights/index.html

**Contents:**
- Lights

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Limit Range

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/limit_range.html

**Contents:**
- Limit Range
- Parameters
- Inputs
- Outputs

Selected operator for range limit.

Minimum value to compare against.

Maximum value to compare against.

Resulting value within limited range.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## List

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/list/index.html

**Contents:**
- List

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## List From Items

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/list/list_from_items.html

**Contents:**
- List From Items
- Parameters
- Inputs
- Outputs

Create a new list with the given items.

Add another socket for additional items inputs.

Item to add to list. Each press of Add Socket will add another Item input. Items will be add to the list from top (index 0) to bottom (index list length-1).

New list with the added items.

Leaving an Item input blank will result in a Null item in your list. TODO: Add an example with mutiple blank item inputs.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## List Saved Variables

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/variables/list_saved_variables.html

**Contents:**
- List Saved Variables
- Inputs
- Outputs

Quickly summarize saved variables from a given file.

Which condition will be used for node to activate. If checked, always True.

Path to the directory containing the requested file.

Name of the file itself, ending can be omitted.

If checked, list will be printed.

True if listing is performed, else False.

Resulting list of saved variables.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Load Bank

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/sound/fmod/load_bank.html

**Contents:**
- Load Bank
- Inputs
- Outputs

Load a .bank file from the system for later use.

If connected, condition must be fulfilled for node to activate.

Path to the .bank file. .bank files are build with the FMod application.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Load Blender File

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/game/load_blender_file.html

**Contents:**
- Load Blender File
- Inputs
- Outputs

This is the in-game equivalent of File Open. It loads directly into the runtime version of another .blend file.

Input condition needed for node to activate.

Full path to the target .blend file; supports relative paths.

True if the node performed successfully, else False.

Output exists, but is disabled in code, therefore it is not visible.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Load File Content

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/load_file_content.html

**Contents:**
- Load File Content
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if node executed properly, else False. todo

Type of data that was loaded, represented as string. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Load Game

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/game/load_game.html

**Contents:**
- Load Game
- Parameters
- Inputs
- Outputs

Reads information about the state of the current scene from a previously saved .json file.

Path to where the save files are stored.

The condition for this node to activate.

Index of this save file.

True if the node performed successfully, else False.

No information is read about which scene is loaded, so this node can only be used per scene.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Load Scene

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/load_scene.html

**Contents:**
- Load Scene
- Inputs
- Outputs

Which condition will be used for node to activate.

True if node executed properly. todo

Type of data that was loaded, represented as string. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Load Variable

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/variables/load_variable.html

**Contents:**
- Load Variable
- Inputs
- Outputs

Load a previously saved value from an external file.

Path to the directory containing the requested file.

Name of the file itself, ending can be omitted.

If enabled, this value will be used as default if Name is not found.

Resulting value that was loaded.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Load Variable Dict

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/variables/load_variable_dict.html

**Contents:**
- Load Variable Dict
- Inputs
- Outputs

Load a file with previously saved values as dictionary.

Path to the directory containing the requested file.

Name of the file itself, ending can be omitted.

Dictionary containing all saved variables in this file.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Logic Bricks

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/index.html

**Contents:**
- Logic Bricks

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Logic Bricks Editor

**URL:** https://upbge.org/docs/latest/manual/manual/editors/logic_bricks/index.html

**Contents:**
- Logic Bricks Editor
- Main View
  - Sensor Column
  - Controller Column
  - Actuator Column
- Property Region
- Python Components Region

The Logic Bricks Editor provides the main method of setting up and editing the game logic for the various actors (i.e. objects) that make up the game. The logic for the objects which are currently selected in the associated 3D View are displayed as logic bricks, which are shown as a table with three columns, showing sensors, controllers, and actuators, respectively. The links joining the logic bricks conduct the pulses between sensor-controller and controller-actuator.

To give you a better understanding of the Logic Bricks Editor, the image below shows a typical editor content in which the major components have been labeled. We will look at each one individually.

The different parts of the Logic Editor

Property Region | 2) Object Name | 3a) Links | 3b) Link socket | 4) Sensor column | 5) Controller Column | 6) Actuator Column | 7) Python Components Region.

This toggle shows the name of the object which owns the logic bricks below.

Links (3A) indicate the direction of logical flow between objects. Link lines are drawn by LMB dragging from one Link socket (3B) to another. Links can be drawn from Sensors to Controllers, or from Controllers to Actuators. If you try to link directly a Sensor with an Actuator a new Controller will appear between both. Actuators cannot be linked back to Sensors (however, special actuator and sensor types are available to provide these connections).

Sending nodes (the chain link found on the right-hand side of Sensors and Controllers) can send to multiple Reception nodes (the chain link found on the left-hand side of Controllers and Actuators). Reception nodes can likewise receive multiple links.

Links can be created between logic bricks belonging to different objects. To delete a link between two nodes, CTRL-RMB drag between the two nodes.

This column contains a list of all sensors owned by the active object (and any other selected objects). New sensors for the active object are created using the “Add Sensor” button. For a more in-depth look at the content, layout and available operations in this area, see Sensors.

This column contains a list of all controllers owned by the active object (and any other selected objects). New controllers for the active object are created using the “Add Controller” button, together with the creation of states for the active object. For a more in-depth look at the content, layout, and available operations in this area, see Controllers.

This column contains a list of all actuators owned by the active object (and any other selected objects). New actuators for the active object are created using the “Add Actuator” button. For a more in-depth look at the content, layout, and available operations in this area, see Actuators.

Game properties are like variables in other programming languages. They are used to save and access data associated with an object. Several types of properties are available. Properties are declared by clicking the Add Game Property button in this region. For a more in-depth look at the content, layout and available operations in this region, see Properties.

This region is where the Python Components are placed. Python Components are an independently logic system from Logic Bricks system. They are modules that can be attached to game objects. For a more in-depth look at the content, layout and available operations in this region, see Python Components.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Logic

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/index.html

**Contents:**
- Logic

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Logic Nodes

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/index.html

**Contents:**
- Logic Nodes

This page lists available Logic Nodes, which are many. There are 6 categories in Logic Node Editor Add menu, with sub-menus: either jump into one here below, or scroll down the page for direct access to Logic Nodes.

Events | | Game | | Input | | Values

Animation | | Lights | | Nodes | | Objects | | Scene | | Sound

Logic | | Math | | Physics | | Python | | Raycasts | | Time

Data | | File | | Network

The sub-menu Layout is not a particular part of Logic Nodes - those are tools for organizing and connecting, and are common feature for all node editors.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Logic Node Editor

**URL:** https://upbge.org/docs/latest/manual/manual/editors/logic_nodes/index.html

**Contents:**
- Logic Node Editor

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Logic Tree Status

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/trees/logic_tree_status.html

**Contents:**
- Logic Tree Status
- Inputs
- Outputs

Which object to inspect.

Which Node Tree todo.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Maintenance

**URL:** https://upbge.org/docs/latest/manual/manual/contribute/maintenance.html

**Contents:**
- Maintenance
- Adding/Removing/Moving Files

When RST-files are added or removed the corresponding locale files are added or removed automatically by the update script. However, if files need to be moved please use this Python script:

RST-files can then be freely moved and the remap script will move the locale file after:

It is best to avoid moving/renaming files as this breaks URLs and without this script translators will lose all their work in these files. Please ask an administrator if you think something should be renamed/moved.

This script also works for image file names.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (unknown):
```unknown
python tools/utils_maintenance/rst_remap.py start
```

Example 2 (unknown):
```unknown
python tools/utils_maintenance/rst_remap.py start
```

Example 3 (unknown):
```unknown
python tools/utils_maintenance/rst_remap.py finish
```

Example 4 (unknown):
```unknown
python tools/utils_maintenance/rst_remap.py finish
```

---

## Make Light Unique

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/lights/make_light_unique.html

**Contents:**
- Make Light Unique
- Inputs
- Outputs

Which condition will be used for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Map Range

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/map_range.html

**Contents:**
- Map Range
- Parameters
- Inputs
- Outputs

Selected mode of operation.

Clamp values between 0 and 1. todo

Resulting value from ranging operation.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Markup Style Guide

**URL:** https://upbge.org/docs/latest/manual/manual/contribute/markup_style.html

**Contents:**
- Markup Style Guide
- Conventions
- Headings
- Text Styling
- Interface Elements
- Code Samples
- Images
  - Files
  - Usage Guides
- Videos

This page covers the conventions for writing and use of the reStructuredText (RST) markup syntax.

Three (3) space indentation.

Lines should be less than 120 characters long.

Use italics for button/menu names.

Other loose conventions:

Avoid Unicode characters.

(i.e. sentences can have their own lines).

Parts should only be used for contents or index pages. Each .rst file should only have one chapter heading (=) per file - top heading.

See the overview on ReStructuredText for more information on how to style the various elements of the documentation and on how to add lists, tables, pictures and code blocks. The Sphinx reference provides more insight into additional constructs.

Do not manually format/break lines in .rst files; use your editor’s wrap text functionality. 80 characters is standard line length for computer files.

The following are useful markups for text styling:

:kbd:`LMB` - keyboard and mouse shortcuts.

*Mirror* - interface labels.

:menuselection:`3D Viewport --> Add --> Mesh --> Monkey` - menus.

There is support for syntax highlighting if the programming language is provided, and line numbers can be optionally shown with the :linenos: option:

Figures are used to place images:

For consistency, and since it would be good to ensure that screenshots are all of similar size when floated next to text, writers should take screenshots in the following manner:

Prepare the area you would like to capture making sure to use the default theme and setting. (In some cases you may not want to use the default settings e.g. if some options are hidden behind a checkbox.)

Zoom to the maximum zoom level (hold NumpadPlus or Ctrl-MMB or similar).

Zoom out eight zoom levels (NumpadMinus – eight times).

In some cases you will want to leave a small margin around the thing you are trying to capture. This should be around 30px but does not have to be exact.

This can be applied to several parts of the interface but might not work for all cases.

If really needed, use additinal directives for image formatting:

Lower case filenames underscore between words.

Order naming with specific identifiers at the end.

Use .png for images that have solid colors such as screenshots of the Blender interface, and .jpg for images with a high amount of color variance, such as sample renders and photographs.

Do not use animated .gif files, these are hard to maintain, can be distracting and are usually large in file size. Instead use a video if needed (see Videos below).

Place the images in the manual/images folder, and use subfolders, if needed.

For naming files use dashes to separate chapters and sections, and use underscore to connect sections that are two or more words, i.e. for image files:

chapter-subsection-sub_subsection-id.png:

interface-splash-current.png

interface-undo_redo-last.png

interface-undo_redo-repeat_history-menu.png

Do not use special characters or spaces!

Avoid specifying the resolution of the image, so that the theme can handle the images consistently and provide the best layout across different screen sizes.

When documenting a panel or section of the UI, it is better to use a single image that shows all of the relevant areas (rather than multiple images for each icon or button) placed at the top of the section you are writing, and then explain the features in the order that they appear in the image.

It is important that the manual can be maintained long term. UI and tool options change, so try to avoid having a lot of images (when they are not especially necessary). Otherwise, this becomes too much of a maintenance burden.

This is from Blender manual. It might not be suitable for UPBGE-Docs developers.

Videos can be embedded from Blender’s self-hosted PeerTube instance, which can be found at video.blender.org. To embed a video use the following directive:

The ID is found in the video’s URL, e.g.:

ID for https://video.blender.org/videos/watch/47448bc1-0cc0-4bd1-b6c8-9115d8f7e08c

is 47448bc1-0cc0-4bd1-b6c8-9115d8f7e08c.

To get a new video uploaded, contact a Documentation Project Administrator.

Avoid adding videos that rely on voice or words, as this is difficult to translate.

Do not embed video tutorials as a means of explaining a feature, the writing itself should explain it adequately. (Though you may include a link to the video at the bottom of the page under the heading Tutorials.)

|BLENDER_VERSION| - Resolves to the current Blender version.

:abbr:`SSAO (Screen Space Ambient Occlusion)` - Abbreviations display the full text as a tooltip for the reader.

Hover mouse over here

:term:`Manifold` - Links to an entry in the Glossary.

You can link to another part of the Manual with folder path:

To link to a specific section in another file (or the same one), explicit labels are available:

Explicit labels should immediatelly preceed the title. I.e.:

will not work. Should be:

Linking to a title in the same file:

Linking to the outside world:

It is possible to link to a specific part of the manual from inside the Blender by opening the context menu (right click) of a property or operator and selecting Online Manual. In order for this to work, this needs to be accounted for in the documentation. To link a property or operator to a specific part of the manual you need to add an external reference link tag whose ID matches Blender’s RNA tag. The easiest way to find out what is the tag for a property, is to open the context menu of the property/operator and select Online Python Reference to extract the tag from the URL. Some examples of how this looks in the RST document are given below:

To learn more about reStructuredText, see:

Good basic introduction.

Verbose reStructuredText cheat-sheet.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (markdown):
```markdown
#################
  Document Part
#################

================
Document Chapter
================

Document Section
++++++++++++++++

Document Subsection
-------------------

Document Subsubsection
^^^^^^^^^^^^^^^^^^^^^^

Document Paragraph
""""""""""""""""""
```

Example 2 (markdown):
```markdown
#################
  Document Part
#################

================
Document Chapter
================

Document Section
++++++++++++++++

Document Subsection
-------------------

Document Subsubsection
^^^^^^^^^^^^^^^^^^^^^^

Document Paragraph
""""""""""""""""""
```

Example 3 (markdown):
```markdown
*italic*
**bold**
``literal``
```

Example 4 (markdown):
```markdown
*italic*
**bold**
``literal``
```

---

## Materials

**URL:** https://upbge.org/docs/latest/manual/manual/editors/properties/materials.html

**Contents:**
- Materials
- Game Settings
- Face Orientation

This panel contains properties that control how the object surfaces that use the material are rendered in real-time by the Blender Game Engine.

Hide the back-faces of objects rendered with this material. If “Off”, both sides of the surface are visible (at the expense of lower rendering speed). Note that this setting is applied per material and not per face; e.g. if the material is applied to a cube, only the back and front faces of the cube are visible, and not both sides of each face.

Hide all faces of objects rendered with this material.

Use material as Text object in the Game Engine.

Controls how the alpha channel is used to create a transparent texture in the rendered image.

Orders the sequence in which transparent objects are drawn on top of each other, so that ones in front receive more light than ones behind.

Uses the alpha values present in the bitmap image sourced in the Image slot.

Uses the alpha channel as a simple mask.

Render face transparent and add color of face.

All alpha values are ignored; the scene is completely non-transparent.

Provides options regarding the orientation (i.e. rotation transformation) of faces to which the material is applied.

Faces are used for shadow.

Billboard with Z-axis constraint.

Screen-aligned billboard.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Materials

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/materials/index.html

**Contents:**
- Materials

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Math

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/math.html

**Contents:**
- Math
- Parameters
- Inputs
- Outputs
- Example

Selected mathematical operation.

Resulting value from math operation.

Math nodes making sure that pressing the keyboard keys is fun

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Math

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/index.html

**Contents:**
- Math

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Matrix To XYZ

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/vectors/matrix_to_xyz.html

**Contents:**
- Matrix To XYZ
- Parameters
- Inputs
- Outputs

Selected type for operation.

Selected matrix dimension for operation.

Resulting XYZ vector.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Message Sensor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/types/message.html

**Contents:**
- Message Sensor
- Properties
- Example

See the Python reference of this logic brick in KX_NetworkMessageSensor.

The Message Sensor can be used to detect either text messages or property values. The sensor sends a positive pulse once an appropriate message is sent from anywhere in the engine. It can be set up to only send a pulse upon a message with a specific subject.

See Message Actuator for how to send messages.

See Sensor Common Options for common options.

Specifies the message that must be received to trigger the sensor (this can be left blank).

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Modify Object Property

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/modify_object_property.html

**Contents:**
- Modify Object Property
- Parameters
- Inputs
- Outputs

Selected property mode.

Type of selected operation to perform.

Clamp the value to 0-1 range.

If connected, condition must be fulfilled for node to activate.

Name of property to modify.

Value to use for modification.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Mouse

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/mouse/index.html

**Contents:**
- Mouse

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Mouse Button

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/mouse/mouse_button.html

**Contents:**
- Mouse Button
- Parameters
- Inputs
- Outputs

Detects mouse button activity.

Input detection mode for mouse button.

Which button to monitor.

True if the corresponding button is pressed, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Mouse Look

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/mouse/mouse_look.html

**Contents:**
- Mouse Look
- Parameters
- Inputs
- Outputs

A quick way to make objects follow the mouse movement. It’s possible to assign a Body and a Head object.

If no Head object is assigned, the body will be used for both axis, but that is generally discouraged as it can lead to unwanted side effects.

Look direction of the Head Object. If set to Y, the rotational axis will be X and vice versa.

If checked, the mouse cursor will be centered in the game window.

If connected, condition must be fulfilled for node to activate.

The head object. If set, both objects will be rotated along their corresponding local axis.

Option to invert movement for each axis (Vector2).

Multiplier for translating mouse movement to object rotation.

Limit the body objects rotation on its local Z axis.

The limits for the body object’s local Z rotation (Vector2). Only shown if Cap Left/Right is selected.

Limit the head object’s rotation on its local X/Y axis.

The limits for the head object’s local X/Y rotation (Vector2). Only shown if Cap Up/Down is selected.

Use linear interpolation to slowly adapt the object transformation to mouse movement.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Mouse Moved

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/mouse/mouse_moved.html

**Contents:**
- Mouse Moved
- Parameters
- Outputs

Detects mouse movement.

Boolean value to select between Once (unchecked) and Each Frame (checked) modes.

True if mouse movement is detected, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Mouse Over

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/mouse/mouse_over.html

**Contents:**
- Mouse Over
- Inputs
- Outputs
- Example

Matches the mouse position to an object on screen.

Which object to monitor, if mouse cursor is over.

True on the first frame the mouse position matches the object bounds, else False.

True while the mouse position matches the object bounds, else False.

True on the first frame the mouse position leaves the object bounds, else False.

World Position of the mouse cursor matched to the object (Vector3).

Face normal of the targeted mesh face (Vector3).

With Cube object selected, apply the logic tree (click Apply To Selected button).

Run the UPBGE from terminal (Linux & mac), or open the console (Windows). See System Console if needed.

Make sure that in Render > Game Debug > Mouse Cursor is selected.

Run the example, and move mouse cursor over the Cube which has logic tree applied to it. In system terminal/console, see printed results.

Add Once node, run and observe different terminal output. Only once per Mouse Over is now system message printed. Uncheck Repeat and exactly once is message printed - on first Mouse Over event only.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Mouse Ray

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/raycasts/mouse_ray.html

**Contents:**
- Mouse Ray
- Inputs
- Outputs

Which condition will be used for node to activate.

Which property to use.

Mask layers to use. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Mouse Sensor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/types/mouse.html

**Contents:**
- Mouse Sensor
- Properties

See the Python reference of this logic brick in SCA_MouseSensor.

The Mouse Sensor detects mouse events.

See Sensor Common Options for common options.

The controller consist only of a list of types of mouse events. A FALSE pulse is given when any of these conditions ends.

Gives a TRUE pulse if the mouse moves over any game object.

Gives a TRUE pulse if the mouse moves over the owner object.

Any movement with the mouse causes a stream of TRUE pulses.

Causes a stream of TRUE pulses as the scroll wheel of the mouse moves down.

Causes a stream of TRUE pulses as the scroll wheel of the mouse moves up.

Gives a TRUE pulse when right mouse button is pressed.

Gives a TRUE pulse when middle mouse button is pressed.

Gives a TRUE pulse when left mouse button is pressed.

Gives a TRUE pulse when 4th mouse button is pressed.

Gives a TRUE pulse when 5th mouse button is pressed.

Gives a TRUE pulse when 6th mouse button is pressed. This button depends in mouse configuration software. It is possible that doesn’t work correctly.

Gives a TRUE pulse when 7th mouse button is pressed. This button depends in mouse configuration software. It is possible that doesn’t work correctly.

There is a logic brick for specific mouse movement and reactions (such as first person camera), see Mouse Actuator.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Mouse Status

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/mouse/mouse_status.html

**Contents:**
- Mouse Status
- Outputs

Gives informations about the mouse cursor and wheel scroll.

The XY position of the cursor from the top left corner of the game window (Vector2).

The XY movement of the cursor on the game window comparing to previous frame position (Vector2).

The X position of the cursor from the top left corner of the game window.

The Y position of the cursor from the top left corner of the game window.

The X movement of the cursor on the game window compared to previous frame position.

The Y movement of the cursor on the game window compared to previous frame position.

1 if the wheel is scrolled up and -1 if the wheel is scrolled down, else 0.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Movement Sensor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/types/movement.html

**Contents:**
- Movement Sensor
- Properties

See the Python reference of this logic brick in SCA_MovementSensor.

The Movement Sensor detects the object movement along one or more axis.

See Sensor Common Options for common options.

This menu determines the direction of the object movement to be detected. The ± signs is whether it is on the axis direction (+), or the opposite (-).

Indicates whether the movement detected is in local or global coordinates.

Indicates the amount of displacement from which movement is detected.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Move To

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/move_to.html

**Contents:**
- Move To
- Input
- Output

Moves a selected object to a specific location in the scene.

The condition for this node to start.

Object that will be moved.

Final destination of the object.

Dynamic objects give and receive collisions, so other objects can dynamically affect the trajectory of the Moving Object.

Amount of displacement that will be applied to the object on each Condition activation.

A distance that the object needs to be close to the Target Location, to complete the move.

True if the node performed successfully, else False.

True if the object is within stopping distance, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Move To with Navmesh

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/move_to_with_navmesh.html

**Contents:**
- Move To with Navmesh
- Input
- Output

Moves an object in a space delimited by Navigation Mesh.

Navigation Mesh is an object that’s invisible in-game - it defines where AI can walk and what’s off-limit.

To define an object as a Navigation Mesh, go to the Physics properties area of the object and select in Game Physics the object as being Navigation Mesh.

The condition for this node to start.

Object that will be moved.

Object that will rotate when the direction changes.

Object that will limit the movement area.

Final destination of the object. It can be a value using coordinates or location of another object.

Dynamic objects give and receive collisions, so other objects can dynamically affect the trajectory of the Moving Object.

Linear speed of the object, basically the travelling speed.

Distance to the target it needs to count as arrived.

If selected, the front of the object will observe the direction of displacement.

When the object makes a change of direction, which axis will rotate.

Which axis is the front of the object.

Speed at which the object will move sideways when making a change of direction.

View the displacement path with a red line during gameplay.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Moving A Cube

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_python_scripting/move_object.html

**Contents:**
- Moving A Cube
- Setup:
- Full Python Script:
- Explanation:
- Extensions:

In this tutorial, we’ll move a cube in 3D space using Python, with full WASD controls and rotation.

Add a Cube to the scene.

Add an Always sensor linked to a Python Controller (no other setup needed).

`applyMovement`: Moves the cube relative to its local rotation (so “W” always moves forward).

`applyRotation`: Rotates around the Z-axis (yaw) with Q/E.

No Logic Bricks setup: All input is handled via Python.

Add gravity with owner.worldPosition.z -= 0.05.

Use bge.render.showMouse(True) for mouse look.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (python):
```python
import bge
from math import radians

def update_movement(owner, speed=0.1, rot_speed=1.0):
    keyboard = bge.logic.keyboard
    events = keyboard.events

    # Movement (WASD)
    move_vec = [0.0, 0.0, 0.0]
    if events[bge.events.WKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[1] += speed  # Forward (Y-axis)
    if events[bge.events.SKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[1] -= speed  # Backward
    if events[bge.events.AKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[0] -= speed  # Left (X-axis)
    if events[bge.events.DKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[0] += speed  # Right

    # Apply movement relative to the cube’s rotation
    owner.applyMovement(move_vec, local=True)

    # Rotation (Q/E for yaw)
    if events[bge.events.QKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.applyRotation([0, 0, radians(rot_speed)], local=True)
    if events[bge.events.EKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.applyRotation([0, 0, radians(-rot_speed)], local=True)

# Main
controller = bge.logic.getCurrentController()
owner = controller.owner
update_movement(owner)
```

Example 2 (python):
```python
import bge
from math import radians

def update_movement(owner, speed=0.1, rot_speed=1.0):
    keyboard = bge.logic.keyboard
    events = keyboard.events

    # Movement (WASD)
    move_vec = [0.0, 0.0, 0.0]
    if events[bge.events.WKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[1] += speed  # Forward (Y-axis)
    if events[bge.events.SKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[1] -= speed  # Backward
    if events[bge.events.AKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[0] -= speed  # Left (X-axis)
    if events[bge.events.DKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[0] += speed  # Right

    # Apply movement relative to the cube’s rotation
    owner.applyMovement(move_vec, local=True)

    # Rotation (Q/E for yaw)
    if events[bge.events.QKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.applyRotation([0, 0, radians(rot_speed)], local=True)
    if events[bge.events.EKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.applyRotation([0, 0, radians(-rot_speed)], local=True)

# Main
controller = bge.logic.getCurrentController()
owner = controller.owner
update_movement(owner)
```

Example 3 (python):
```python
import bge
from math import radians

def update_movement(owner, speed=0.1, rot_speed=1.0):
    keyboard = bge.logic.keyboard
    events = keyboard.events

    # Movement (WASD)
    move_vec = [0.0, 0.0, 0.0]
    if events[bge.events.WKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[1] += speed  # Forward (Y-axis)
    if events[bge.events.SKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[1] -= speed  # Backward
    if events[bge.events.AKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[0] -= speed  # Left (X-axis)
    if events[bge.events.DKEY] == bge.logic.KX_INPUT_ACTIVE:
        move_vec[0] += speed  # Right

    # Apply movement relative to the cube’s rotation
    owner.applyMovement(move_vec, local=True)

    # Rotation (Q/E for yaw)
    if events[bge.events.QKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.applyRotation([0, 0, radians(rot_speed)], local=True)
    if events[bge.events.EKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.applyRotation([0, 0, radians(-rot_speed)], local=True)

# Main
controller = bge.logic.getCurrentController()
owner = controller.owner
update_movement(owner)
```

---

## Moving A Cube

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_nodes/moving_cube.html

**Contents:**
- Moving A Cube

See Logic Node Editor for node basics.

Moving an object requires input from user, processing this input, and applying movement to object. To run the game, a Camera object is also required.

Add 4 Keyboard Key nodes, and assign A for left, D for right, W for forward, and S for backward movement.

Add 2 Math nodes, set both to Subtract, and connect 2 above nodes to each Math node, i.e. A and D nodes to one Math node, W and S to the other Math node.

Next add a Combine XY, connect above Math nodes to X and Y input sockets.

Connect to Vector Math Vector 1 socket, set Normalize property from dropdown menu.

Connect the Result output to another Vector Math node > Vector 1 socket. Set property to Scale.

Either add new node, or select existing one > Shift-D to duplicate > move with mouse > LMB to ‘land’ it. Keep mouse cursor close to the node while duplicating.

Add Float node, set value to 0.1, and connect it to the last Vector Math node, Scale input. This will determine movement speed for the object.

Add Apply Movement node; output from above Vector Math node goes into Vector input. Check Local box, and in the Object input select an object to move, i.e. Cube.

Last, add On Update node, and connect to above Apply Movement > Condition socket.

Alright, now we apply this logic tree to an object.

Select (or add) any object, in Logic Nodes Editor select all nodes (A), and in N-panel > Dashboard > Administration click Apply To Selected button.

If the game does not run as expected, also click Force Compile.

Logic tree should look like this:

Logic tree for moving an object with keyboard

Run the game, use the keyboard keys we set in first step to move the Cube.

If object is moving in wrong direction, either swap keys in Keyboard Key nodes (i.e. A > D and D > A), or swap A and B inputs in Math node.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Moving A Cube

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_bricks/move_object.html

**Contents:**
- Moving A Cube
- Setup Scene
- Adding Logic
- Logic Depending On Properties
- Conclusion

In this short tutorial we will introduce two essential elements for logic in UPBGE: logic triggering and game properties. These elements allows the interactivity with the set up objects.

A game property (also known as variable) is a value that is kept inside a object, allowing multiple uses. A common use of game properties is the ammount life of the player, the current song playing, or anything else that can be useful to track for later use.

The logic triggering is the act of triggering some kind of event in the game. There’s lots of ways to trigger events in UPBGE, from detecting if a key is pressed to detecting an object colliding with another, or even triggering events continuously without detecting anything. After the detection of an trigger, an event can be happen, like a object to move, a property be changed, etc.

First, we must add objects to compose our scene (mouse-over 3D Viewport > Shift-A). We need three basic objects:

A camera will allow us to see our scene from a point of view.

A light will illuminate the scene objects, allowing us to see them. In this example we’ll use a Sun light, which will illuminate all objects in the scene.

A Cube object will be our visual feedback of our logic. As we can’t see a camera or light, we’ll move the Cube.

Once all objects were added, place them somewhat like the picture below:

Cube at the center of the scene

Our Cube is not centered in the screen on purpose: we’ll move it in the front direction (-Y), so it’s good to see it moving after certain point.

After the scene is set up, with Cube selected, follow these steps:

Go to the Logic Bricks Editor.

Add a Keyboard Sensor through the dropdown menu Add Sensor.

Add a AND Controller through the dropdown menu Add Controller.

Add a Motion Actuator through the dropdown menu Add Actuator.

Connect each brick by dragging and dropping one insert into another (chain link icon).

Now we must fill some information on the bricks:

On the Keyboard Sensor, click on the Key field and press a key to assign a key to it.

On the Motion Actuator, insert the value -0.05 in the field Y of Loc.

The Logic Bricks Editor should look like this:

Keyboard Sensor > AND Controller > Motion Actuator

Start the game engine (by default, pressing P while focusing/mouse-over the 3D Viewport). If you press the key you assigned to the Keyboard Sensor, the Cube will move in the -Y direction, and if you release the key, the Cube will stop.

This behavior happens for several reasons:

The Keyboard Sensor emits a positive signal when the selected key is pressed, and emits a negative signal when the key is released.

The AND Controller receives the signals from all connected sensors, and if all signals are positive, the controller emits an activation signal to all connected actuators, or an deactivation signal if one or more incoming signals are negative.

The Motion Actuator receives the activation signal from the controller and perform the motion. When it receives a deactivation signal, it stops performing the motion.

This is the basic of visual logic when using UPBGE, pretty straightforward. However, according to what you want to achieve, it can get a lot more complex.

In games, the logic depends on statuses most of the time. An enemy dies when its life reaches 0, the player can shoot while its ammo is greater than 0, and so on. In UPBGE, you can do these conditions through the use of properties.

To continue, perform the following steps:

In Logic Bricks Editor (No. 1 - Properties), add a property through Add Game Property, set its name to fuel, its type to Integer and its value to 200.

Next add a Property Sensor, set its evaluation type to Greater Than, the Property to fuel and the value to 0.

Connect the Property Sensor to the AND Controller, along with the Keyboard Sensor.

Property Sensor (left side) properly filled and Fuel property added (right side)

This makes our Cube move only if the value of fuel is greater than 0. You can set the property fuel to 0 and play the game, and you will see that the Cube will not move. However, it would be good if we decrease the value of fuel as our Cube moves, until it reaches 0. To do that, do the following steps:

Add a Property Actuator and connect it to the AND Controller.

Set the mode of Property Actuator to Add, its property to fuel and its value to -1.

Enable the pulse mode on Keyboard Sensor.

Fuel consumption logic: Sensors > And Controller > Property Actuator

There’s a new factor involved here: the pulse mode on Keyboard Sensor (blue up arrow in top left corner). By default, a sensor sends a single positive signal to the controller when active, and a single negative signal when inactive. The pulse mode makes the signal be sent each logical frame (default is 60 frames per second). This is useful for us now, because we need our fuel to be decreased while we press the key without the need of releasing and pressing it again.

Go ahead and play the game. The Cube will move and, after some time, it stops. It happens because the Property Actuator has decreased 1 unit of fuel each frame, according to the Keyboard Sensor pulse mode, and when fuel reaches 0, the logic of the Motion Actuator doesn’t respond anymore. It would be good, however, to see the value of fuel be decreased over time. You can do this by enabling the debug flag on the fuel property (Properties Editor > Game > Game Properties), or Logic Bricks Editor > N-panel > Properties, as shown in the figure below.

Debug settings and display on screen

The goal of this basic tutorial is to show how to work with the visual logic and properties on UPBGE. There’s more to be discovered about visual logic and properties, like other Property Types, the use of States with logic bricks, etc, and those subjects can be better understood on their own pages.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Network

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/network/index.html

**Contents:**
- Network

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## New Dictionary

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/dict/new_dictionary.html

**Contents:**
- New Dictionary
- Outputs

Creates new empty dictionary.

Diamond socket indicates dictionary.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## New List

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/list/new_list.html

**Contents:**
- New List
- Inputs
- Outputs

Create a new empty list.

List length - how many items will it have.

Resulting empty list of specified length.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Nodes

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/index.html

**Contents:**
- Nodes

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Not None

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/not_none.html

**Contents:**
- Not None
- Inputs
- Outputs

True if value is not none.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Objects

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/index.html

**Contents:**
- Objects

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Object

**URL:** https://upbge.org/docs/latest/manual/manual/editors/properties/object.html

**Contents:**
- Object
- Name
- Culling Bounding Volume
- Activity Culling
- Levels of Detail
  - Tools
  - Settings
- Transform and Delta Transform
- Relations
- Relations Extras

Object tab in Properties Editor

The Object tab from Properties Editor exposes settings and properties related to the current object. These properties and settings can be position, rotation, level of detail, group options and so on. For more detailed info about this tab, see Object properties in Blender Manual.

Object’s name field in Object tab

The object’s name will identify the object in most cases, specially in fields inside the Blender editors. In UPBGE, if two identical objects are added in game (for example, with an Add Object logic or instanced through a group), both objects will have the same name, differently from Blender which appends a number in a repeating object, so be aware that retrieving an object through its name may not work sometimes. Prefer using Game Properties, instead.

Predefined mesh bounding volume used when Auto Update Bound is disabled.

UPBGE’s Activity Culling feature allows to disable object’s physics and logic based on the distance to the nearest camera. This allows better performance by not processing objects which are too far away.

Suspend physics of this object by its distance to nearest camera.

Distance to begin suspend physics of this object

Suspend logic and animation of this object by its distance to nearest camera.

Distance to begin suspend logic and animation of this object

When creating visual assets it is often desirable to have a high amount of detail in the asset for up close viewing. However, this high amount of detail is wasted if the object is viewed from a distance, and brings down the scene’s performance. To solve this, the asset can be swapped out at certain viewing distances. This is commonly referred to as a level of detail system. Each visual step of the asset is known as a level of detail. Levels of detail are most appropriate to use when you have a large scene where certain objects can be viewed both up close and from a distance.

The factor applied to distance computed in LoD.

Add a level of detail to this object

Tools dropdown menu in Levels of Detail panel

Some tools for making levels of detail easier to manage and create can be found from the select menu next to the add button in the Levels of Detail panel.

Searches the scene for specifically named objects and attempts to set them up as levels of detail on the currently selected object. The selected object must be the base level of detail (e.g. LOD0). This can be useful to quickly setup levels of detail on imported assets. In order to make use of this tool, your naming must be consistent, and each level must be prefixed or suffixed with “lodx” where x is the level that object is intended for. The case on “lod” must be consistent across all objects. Below are some example names that the tool will recognize.

LOD0_Box, LOD1_Box, LOD2_Box

Box.lod0, Box.lod1, Box.lod2

LoD0box, LoD1box, LoD2box

This tool generates and sets up levels of details based on the selected object. Generation is done using the Decimate Modifier. Generation does not apply the modifier to allow further changing the settings. Generated objects are automatically named based on the level they are generated for. Below are some settings for the operator.

The number of levels desired after generation. This operator creates Count-1 new objects.

The ratio setting for the Decimate Modifier on the last level of detail. The ratio settings for the other levels are determined by linear interpolation.

With this setting enabled the operator performs some extra tasks to make the asset ready for easy linking into a new file. The base object and all of its levels of detail are placed into a group based on the base object’s name. Levels other than the base are hidden for both the viewport and rendering. This simplifies the appearance of the system and does not affect the appearance of the base object. Finally, all levels are parented to the base object to remove clutter from the Outliner.

Clears the level of detail settings from the current object.

Level of detail settings can be found in the Object settings when the renderer is set to Blender Game. In the Levels of Detail panel is a button to add a new level of detail to the current object. The settings for each level of detail are displayed in its own box. The exception to this is the base level of detail. This is automatically setup as the current object with a distance setting of 0. To remove a level of detail, click on the X button in the top right corner of the box of the level to be removed.

The object to use for this level of detail.

The distance at which this level of detail becomes visible.

When this option is enabled, the mesh from the level of detail object is used until a lower level of detail overrides it.

When this option is enabled, the material from the level of detail object is used until a lower level of detail overrides it.

Object’s transform panels in Object tab

The Transform panel exposes the position, rotation and scale properties of the object, and the Delta Transform panel increments additional transformation values to Transform values. Note that these properties behave according to the object’s parent transform properties. However, this explanation is just a base to understand how the transformation values work in UPBGE. More info about the Transform panel can be found at Transform Properties.

In UPBGE there are two types of transformation values for the object: the World and the Local properties. The World values are the transformation values relative to the center of the world, and the Local values are the transformation values relative to the object’s parent object. For example:

An object with a World Position of (0, 0, 0) is literally at the center of the world.

An object with a Local Position of (0, 0, 0) is at the same position of its parent, even if its parent is not at the center of the world.

Be aware that, if the object doesn’t have a parent, the Local values behave the same as the World values.

Technically, with the given information, the Transform panel works the same as the Local transform values, and the Delta Transform panel values are added to the World values of the object at game start.

Exposes values of relations of current object to other objects, scene, etc. For detailed info about object relations, see Object Relations.

The layers which the object is on the scene, multiple can be selected. The behavior is similar to Blender’s layers, as layers can keep the object hidden / shown or some actions can be applied only to objects in a specific layer (as lamps and shadows). Also, only objects in hidden layers can be added through logic. Detailed info about layers can be found at Layers.

The parent object of the current one. While the current object have a parent, its transformation values will be inherited from the parent. A parent may have multiple children, but the reverse is not true. The parenting behavior changes according to the selected mode in dropdown menu. Detailed info about parenting can be found at Parenting Objects.

Exposes some extra settings about object’s relationship. Detailed info about relations extras can be found at Relations Extras.

Creates a delay in parent relationship. Useful to easily smooth movement for character cameras, for example.

The ammount of delay in Slow Parent.

Groups have multiple uses in Blender, but in UPBGE its main use is to allow creating maintainable libraries for games through the use of dupli group instances. Once one or several objects are added to a group, instances of this group can be added to the scene, and editing the original objects edits all the instances automatically in Blender. Detailed info about groups can be found at Groups.

These settings (except for Object Color) don’t affect the current object in UPBGE, only does in 3D Viewport. The exception, Object Color, can be used in game as value in material nodes, Python and material’s Object Color option. Detailed info about the Display panel can be found at Display.

Exposes several duplication modes, but the useful one in UPBGE is Group. When a group is selected in the dropdown menu, a group is instanced in the current object. By default, only empties are used in order to instance groups, but any kind of object can do it as well. More about dupli group instances uses in UPBGE on Groups. Detailed info about the dupli group feature can be found at DupliGroup.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Object Data

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/object_data/index.html

**Contents:**
- Object Data

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Object Has Property

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/object_has_property.html

**Contents:**
- Object Has Property
- Parameters
- Inputs
- Outputs

Will check if selected object has required property.

Selected property mode.

Which object to inspect.

Name of the property to inspect.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Once

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/events/once.html

**Contents:**
- Once
- Inputs
- Outputs
- Example

Restricts a continuous True condition to only the first frame.

Allow another activation after the input condition is reset to False.

True for the first frame of a True input condition, else False.

On Update linked to Once node would be equal to On Init.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## On Init

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/events/on_init.html

**Contents:**
- On Init
- Outputs

Used to set up a scene. It activates only on the first frame - game initialization.

True on the first frame, when the scene is initialized

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## On Next Frame

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/events/on_next_frame.html

**Contents:**
- On Next Frame
- Inputs
- Outputs

Delays a condition by one tick/frame.

If True, the condition is reserved until the next tick/frame.

True one tick/frame after the Condition socket is activated.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## On Update

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/events/on_update.html

**Contents:**
- On Update
- Outputs

Activates each frame. It is used to continuously do something. It is node equivalent to the Always Sensor.

On Update can be expensive depending on the logic attached to it, and should only be used if necessary.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## On Value Changed

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/events/on_value_changed.html

**Contents:**
- On Value Changed
- Parameters
- Inputs
- Outputs

Stores a value internally, and as soon as a value other than the stored one is pulled through the input, it activates. Then the new value is stored.

If checked, the node will ignore the change from None to the first value pulled from the input socket

Connected value is pulled each frame.

True if the new value is different from the stored one, else False.

The value pulled from the input socket.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## On Value Changed To

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/events/on_value_changed_to.html

**Contents:**
- On Value Changed To
- Inputs
- Outputs

Stores a value internally, and as soon as the value pulled through the input matches the target value, it activates. Then the new value is stored.

The connected value is pulled each frame.

Compare the new value to this value.

True if the new value matches the target, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Path

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/path/index.html

**Contents:**
- Path

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Pause Sound

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/sound/pause_sound.html

**Contents:**
- Pause Sound
- Inputs
- Outputs
- Example

If connected, condition must be fulfilled for node to activate.

True if node performed successfully, else False.

This example will play sound when Space key is pressed, will pause sound when P is pressed, and will resume sound when E key is pressed.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Performance Considerations

**URL:** https://upbge.org/docs/latest/manual/manual/deployment/performance.html

**Contents:**
- Performance Considerations

When developing games, game engineers, software and hardware developers uses some tools to fine-tune their games to specific platforms and operating systems, defining a basic usage scenario whereas the users would have the best possible experience with the game.

Most of these tools, are software tools available for the specific Game Engines whereas the games were being developed and will run.

Blender Game Engine also comes with some visual tools to fine-tune the games being developed, so the game developers could test the best usage scenario and minimum software and hardware requirements to run the game.

In Blender, those tools are available at the System and Display panel of Render tab in the Properties editor. There are options for specific performance adjusts and measurements, ways to control the frame rate or the way the contents are rendered in Blender window (game viewport) while the game runs, as well as controls for maintaining geometry allocated in graphic cards memory.

System – controls for Scene rendering while the game is running.

Display – controls for showing specific data about performance while the game is running.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Physics

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/index.html

**Contents:**
- Physics

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Physics

**URL:** https://upbge.org/docs/latest/manual/manual/editors/properties/physics.html

**Contents:**
- Physics
- Physics
- Collision Bounds
  - Options
- Create Obstacle

Options in Physics panel change according to its selected Physics Type. See below:

Collision Bounds panel in Physics tab

The first thing you must understand is the idea of the 3D Bounding Box. If you run through all the vertices of a mesh and record the lowest and highest x values, you have found the x min/max the complete boundary for all x values within the mesh. Do this again for y and z, then make a rectangular prism out of these values, and you have a Bounding Box. This box could be oriented relative globally to the world or locally to the object’s rotation.

Local Bounding Box (left) and a Global Bounding Box (right)

The x extent, then, is half of the distance between the x min/max.

Throughout all of this you must be cognizant of the Object Origin. For the Game engine, the default Shift-Ctrl-Alt-C, 3 or Set Origin ‣ Origin to Geometry is unlikely to get the desired placement of the Collision Bounds that you want. Instead, you should generally set the origin by looking at the Tool Shelf after you do the Set Origin, and changing the Center from Median Center to Bounds Center. Blender will remember this change for future Shift-Ctrl-Alt-C executions.

All Collision Bounds are centered on this origin. All boxes are oriented locally, so object rotation matters.

Setting the origin to Bounds Center instead of Median Center

A final introductory comment: When you set the Collision Bounds on an object, Blender will attempt to display a visualization of the bounds in the form of a dotted outline. Currently, there is a bug: The 3D View does not display this bounds preview where it actually will be during the game. To see it, go to Game ‣ Show Physics Visualization and look for the white (or green, if sleeping) geometry.

Now we can explain the various options for the Collision Bounds settings:

For Dynamic and Static objects, it is a Triangle Mesh (see below). For everything else, it is a Sphere (see below).

Which is a cylinder with hemispherical caps, like a pill. Radius of the hemispheres is the greater of the X or Y extent. Height is the Z bounds.

The X, Y, Z bounding box, as defined above.

Radius is defined by the object’s scale (visible in the N properties panel) times the physics radius (can be found in Physics ‣ Attributes ‣ Radius). Note: This is the only bounds that respects the Radius option.

Radius is the greater of the x or y extent. Height is the z bounds.

Base radius is the greater of the x or y extent. Height is the z bounds.

Forms a shrink-wrapped, simplified geometry around the object.

A convex hull sketch

Most expensive, but most precise. Collision will happen with all of triangulated polygons, instead of using a virtual mesh to approximate that collision.

This is not an option in the Physics tab’s Collision Bounds settings, but a different approach, entirely. You create a second mesh, which is invisible, to be the physics representation. This becomes the parent for your display object. Then, your display object is set to ghost so it does not fight with the parent object. This method allows you to strike a balance between the accuracy of Triangle Mesh with the efficiency of some of the others. See the demo of this in the dune buggy to the right.

Another way to create Collision Bounds - by hand

There are only two options in the Collision Bounds subpanel.

“Add extra margin around object for collision detection, small amount required for stability.” If you find your objects are getting stuck in places they should not, try increasing this to, say, 0.06.

Sometimes 0.06 is the default (such as on the Default Cube), but sometimes it is not. You have to keep an eye on the setting, or else learn the symptoms so you can respond when it gives you trouble. If you are lazy/paranoid/unsure/diligent/bored, you can always run this on the Python Console to bump all 0.0 margins to 0.06: for obj in bpy.data.objects: obj.game.collision_margin = obj.game.collision_margin or 0.06

“Add children to form compound collision object.” Basically, if you have a child object and do not have this enabled, the child’s collisions will not have an effect on that object “family” (though it will still push other objects around). If you do have it checked, the parent’s physics will respond to the child’s collision (thus updating the whole family).

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Physics

**URL:** https://upbge.org/docs/latest/manual/manual/physics/index.html

**Contents:**
- Physics

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Playing An Animation

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_bricks/play_animation.html

**Contents:**
- Playing An Animation
- Before We Start
- The Logic
- Conclusion

In games, animations can be used in many places other than characters - a sliding menu, a opening door, coins rotating, etc. In UPBGE, an animation can be played through the use of an Action. This tutorial will show you how to play an animation of an object and the concept of animation layering, allowing you to play and blend multiple animations at once in a single object.

Before we start using animations through logic, we need some animations. As we said before, UPBGE animations work through the use of Action, so we need to set our default Dope Sheet editor from Dope Sheet mode to Action Editor mode. Now, assuming you already know how to make simple animations adding keyframes, we’ll make two simple actions on a cube of a total 50 frames each, with the following settings:

Rotation action named rotate: No rotation at frame 1, 180° at Z axis on frame 25, more 180° at Z axis on frame 50 (that is, a full 360°).

Scaling action named scale: 0 scale at frame 1, double scale at frame 25 and 0 scale at frame 50 again.

Action Editor showing both actions

Note the transform channels: rotate action only has Euler Rotation channels, and scale action only has Scale channels. This is important to properly blend those actions later on, as having the same channels on both (even without an actual transform) may not have the expected result in the end.

Now, go to the Logic Bricks Editor and do the following setup:

Add two Keyboard Sensor through the dropdown menu Add Sensor.

Add two AND Controller through the dropdown menu Add Controller.

Add two Action Actuator through the dropdown menu Add Actuator.

Connect each brick by dragging and dropping one insert into another.

Now we must fill some fields:

On the Keyboard Sensor, rename both, respectively, to rotate and scale, and set the field Key to, respectively, A and S.

On the Action Actuator, rename both, respectively, to rotate and scale, set the playback type to Loop Stop, the value to its respective actions, End Frame to 50 and Layer to, respectively, 0 and 1.

The setup should look somewhat like the figure below:

Logic Bricks Editor with the given logic set

Now, play the game by pressing P while focusing the 3D Viewport. When you press A the cube should rotate, and when you press S the cube should scale. When pressing both buttons the cube will rotate and scale at the same time, blending both actions. This is only possible due to different animation layers being blended together. For a matter of testing, set the actuator scale Layer to 0, the same value from the actuator rotate. When you play the game, you can’t play both animations at the same time: the last triggered actuator overwrites the currently playing.

This is how you play and blend animations using visual logic in UPBGE. There’s more to be discovered, like playback modes, blending and more, and this can be learnt from the Action Actuator page.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Playing An Animation

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_python_scripting/play_animation.html

**Contents:**
- Playing An Animation
- Setup
- Animation Control Script
- Key Features

This tutorial covers animation control through pure Python scripting.

Create an Armature with animation actions

Add an Always sensor + Python Controller

Play/pause toggle with single key

Dynamic speed adjustment

Smooth blending between states

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (python):
```python
import bge

def handle_animation(owner):
    keyboard = bge.logic.keyboard
    anim = owner.playAction

    # Toggle animation with P key
    if keyboard.events[bge.events.PKEY] == bge.logic.KX_INPUT_ACTIVE:
        if owner.getActionFrame() == 0:
            anim("Walk", 1, 30, speed=1.0, blendin=5)
        else:
            anim("Walk", 0, 0, speed=0)  # Pause

    # Speed control
    if keyboard.events[bge.events.PLUSKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.actionSpeed = 2.0
    if keyboard.events[bge.events.MINUSKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.actionSpeed = 0.5

controller = bge.logic.getCurrentController()
owner = controller.owner
handle_animation(owner)
```

Example 2 (python):
```python
import bge

def handle_animation(owner):
    keyboard = bge.logic.keyboard
    anim = owner.playAction

    # Toggle animation with P key
    if keyboard.events[bge.events.PKEY] == bge.logic.KX_INPUT_ACTIVE:
        if owner.getActionFrame() == 0:
            anim("Walk", 1, 30, speed=1.0, blendin=5)
        else:
            anim("Walk", 0, 0, speed=0)  # Pause

    # Speed control
    if keyboard.events[bge.events.PLUSKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.actionSpeed = 2.0
    if keyboard.events[bge.events.MINUSKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.actionSpeed = 0.5

controller = bge.logic.getCurrentController()
owner = controller.owner
handle_animation(owner)
```

Example 3 (python):
```python
import bge

def handle_animation(owner):
    keyboard = bge.logic.keyboard
    anim = owner.playAction

    # Toggle animation with P key
    if keyboard.events[bge.events.PKEY] == bge.logic.KX_INPUT_ACTIVE:
        if owner.getActionFrame() == 0:
            anim("Walk", 1, 30, speed=1.0, blendin=5)
        else:
            anim("Walk", 0, 0, speed=0)  # Pause

    # Speed control
    if keyboard.events[bge.events.PLUSKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.actionSpeed = 2.0
    if keyboard.events[bge.events.MINUSKEY] == bge.logic.KX_INPUT_ACTIVE:
        owner.actionSpeed = 0.5

controller = bge.logic.getCurrentController()
owner = controller.owner
handle_animation(owner)
```

---

## Play Animation

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/play_animation.html

**Contents:**
- Play Animation
- Inputs
- Outputs

If connected, required condition must be present for node to act.

Which object will receive animation.

Which action will be played.

Start of animation. todo

End of animation. todo

Animation layer. todo

Play mode to be used for animation.

Playing speed of animation.

Blending strength. todo

True if animation started.

True if animation is running.

What to do when animation ends.

Integer of the current frame of animation.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Play Sequence

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/materials/play_sequence.html

**Contents:**
- Play Sequence
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which sprite/material to use.

Emits True signal that sequence started playing.

True when sequence is playing.

Emits True signal when sequence stops.

Integer value of current sequence frame.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Post FX

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/post_fx/index.html

**Contents:**
- Post FX

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Preparation

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_nodes/2d_side_scroller/preparation.html

**Contents:**
- Preparation
- Adding Game Logic

Many times free asset files are available on Internet, for you to be used freely, as a starting point. They may include single object, i.e. a spaceship, or complete levels with hundred of objects. In both cases, they are usually poorly organized, with unclear names, and also often with missing data, mostly materials.

If we want them to be better organized, some renaming and cleaning is necessary. This becomes very important when game includes many scenes or levels. Let’s see how this can be achieved efficiently.

There are many naming conventions in computer programming - snake_case, camelCase etc. We use snake_case in our tutorials.

It is assumed that reader has a keyboard with Numpad - using Blender/UPBGE, this is highly recommended.

In our .blend assets file, find a player object. Not a simple task, since there is no object with that name - names in Outliner are all cryptic/default. Although there is a hint, if you search the Outliner, we’ll assume this is not the case.

Switch to layout workspace, select the ‘egg’ object.

Mouse-over Outliner > Numpad , (comma) - currently selected object is focused in Outliner. Rename to player or whatever you prefer. This works also in reverse - select object in Outliner > mouse-over 3D Viewport > Numpad ,.

Next, there are many objects with same name (except for end numbering). Let’s rename those too. Lucky we, Blender has a built-in tool for batch renaming.

3D Viewport > click big object (rock) under player, and find it in Outliner (hotkey above) - should be named ‘Icosphere.002’.

F3 for Search pop-up > type ‘batch rename’ > Enter (there is also hotkey indicated in Search pop-up).

Search pop-up > All (also hotkey is indicated - Alt-A). If you want to only rename selected objects > Selected.

Leave next field as ‘Objects’, since we are renaming objects. But do feel free to explore other available options in dropdown menu. This goes for next ‘Type’ field too.

‘Find’ field > type ‘icosphere’ (Case Sensitive is unchecked) > ‘Replace’ field > type ‘big_rock’ (or whatever you prefer). For the sake of this tutorial, we will rename the Cube objects at the same time.

Click + button at the right side - this will add another sub-window. ‘Find’ > ‘Cube’ > ‘Replace’ > ‘rock’. Hit OK.

The result is not ok, because we also renamed all trees into rock. Ctrl-Z few times to undo. You now know how to quickly rename objects. If you want to do it properly:

Shift-select all trees in 3D Viewport > Batch Rename > ‘Selected’ > ‘Find’ > ‘cube’ > ‘Replace’ > ‘tree’. Repeat for big rocks and small rocks, rename accordingly.

Blender will sometimes not zoom enough into the object. Solution: select an object > Numpad , - object is centered and focused, now you can zoom in. This procedure works best with single object selected.

In general, it is recommended that game logic is split into small chunks/logic trees - this way it is easier both to write and to manage a game logic.

For above reason, we’ll altogether add five logic node trees:

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Print

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/utility/print.html

**Contents:**
- Print
- Parameters
- Inputs
- Outputs
- Example

Will print messages to System Console. Useful for debugging/game development.

Printed message type.

If checked/connected, condition must be fulfilled for node to activate.

String/text to print.

True if node performed successfully, else False.

See Formatted String node for Print node example.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Projectile Ray

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/raycasts/projectile_ray.html

**Contents:**
- Projectile Ray
- Inputs
- Outputs

Which condition will be used for node to activate.

Vector3 values of origin point. todo

Vector3 values for aim to . todo

Power value for . todo

Distance value . todo

Which property to use.

Mask layers to use. todo

A list of values for . todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Properties

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/properties.html

**Contents:**
- Properties
- Property Types
- Using Properties

Properties are the game logic equivalent to variables. They are stored with the object, and can be used to represent things about them such as ammo, health, name, and so on.

There are five types of properties:

Starts at the property value and counts upwards as long as the object exists. It can for example be used if you want to know how long time it takes the player to complete a level.

This timer uses the simulation time (or frame time) not the real time. When we have 60 fps both times are equal but in other circunstances not.

Uses decimal numbers as values, can range from -10000.000 to 10000.000. It is useful for precision values.

Uses integers (whole numbers) as values, between -10000 and 10000. Useful for counting things such as ammunition, where decimals are unnecessary.

Takes text as value. Can store 128 characters.

Boolean variable, has two values: TRUE or FALSE. This is useful for things that have only two modes, like a light switch.

When a game is running, values of properties are set, manipulated, and evaluated using the Property Sensor and the Property Actuator.

Logic Properties are created and edited using the panel on the right (although it can be moved to the left with F5) of the Logic Bricks Editor panel. The top menu provides a list of the available property types.

Properties Panel of the Logic Editor

This button adds a new property to the list, default is a Float property named prop, followed by a number if there already is one with this name.

Where you give your property its name, this is how you are going to access it through Python or expressions. The way to do so in Python is by dictionary style look-up (GameObject["propname"]). The name is case sensitive.

This menu determines which type of property it is. The available options are in Property Types.

Sets the initial value of the property.

Display property value in debug information. If debugging is turned on, the value of the property is given in the top left-hand corner of the screen while the game is running. To turn debugging on, tick the Debug Properties checkbox in the Game Debug panel of the Render Properties. All properties with debugging activated will then be presented with their object name, property name and value during gameplay. This is useful if you suspect something with your properties is causing problems.

Move the property up or down over other properties within the column.

Deletes the property.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Properties

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/index.html

**Contents:**
- Properties

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Properties Editor

**URL:** https://upbge.org/docs/latest/manual/manual/editors/properties/index.html

**Contents:**
- Properties Editor

Properties Editor tabs

The Properties Editor is an essential part of the development process. There, you can change almost all properties of the selected object, scene, camera, etc, like:

The screen resolution;

Name and position of selected object;

Constraints and modifiers;

Materials and textures properties;

Physics properties of selected object;

In this section you have a detailed description about each tab of the Properties editor.

The Render layers and Particles tabs don’t apply to UPBGE, so they won’t be explained here.

This section will explain properties belonging to UPBGE only (Blender Game renderer) or, at most, relevant properties for game development. For other Blender properties, see the official Blender manual.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Pulsify

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/time/pulsify.html

**Contents:**
- Pulsify
- Inputs
- Outputs

Returns True periodically (pulses) from a continuous input, according to a defined duration and frequency.

If connected, condition must be fulfilled for node to activate.

A gap between pulses.

True when pulses occur, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Python and the Game Engine

**URL:** https://upbge.org/docs/latest/manual/manual/python_scripting/python_game_engine.html

**Contents:**
- Python and the Game Engine
- Integrating Python in the Game Engine
- Writing Your Python Scripts
  - Text Editors
  - UPBGE Text Editor
  - Visual Studio Code or PyCharm
- Reference Material and Documentation
- Testing Your Scripts
  - Designing Your Python Script - Study Example
- 3D World Elements

This whole chapter is organized into three main parts: why, what, and how. Thus, if you have read from the beginning, you already have solid reasons to start using scripts for your project, and you understand what Python is. The final part of this chapter will cover how to use your Python knowledge inside the game engine. This part is divided into four submodules:

Integrating Python in the game engine.

Writing your Python scripts.

Designing your script.

Using the Game Engine API.

In the game engine, the script interface is controller-centric by design. Therefore, you can consider the Python script simply as a more complex controller to replace the Expression or the Boolean controllers. In those cases, the script will be responsible for controlling how the sensors are related with the actuators of a given object. In fact, the sensors, actuators, and even the object where you are calling the script from are all attributes of the controller.

As we mentioned earlier, with a Python script you can control external devices, control multiple objects at once, and much more. However, you will never be free from using a logic brick framework. And from the combination of logic bricks, individual sensors, global sensors, and actuators, the elegance of your system will arise.

In the first example, you will find a very simple case study of how to make your Python controller work. It will cover the basic behavior of receiving sensors’ input in the script and triggering actuators from it.

Download the example 003_template.zip, extract it and load the abracadabra.blend file.

Launch the game and keep the spacebar pressed. In above figure, you can see the result before and after you press the key. Can you read the spinning text? It may not be impressive, but it certainly is didactic. Here is the script behind this effect:

This script is triggered from a keyboard sensor, runs from a controller in the camera object, activates an actuator in the camera itself, and changes a property in the text object. Next figure shows logic bricks for this one.

Simple logic bricks with a Python controller

Let’s look at it from the beginning:

The first lines import the module bge and then the submodule logic. No big deal here. We actually don’t need to explicitly import the bge module since we are importing a submodule directly. However, it doesn’t hurt to do it. Lines 4 and 5 will store the current controller in a variable and create a pointer to the object where it was called from (known as _owner_). We are not using the owner variable here, but it’s good to be familiar with it. You will be using it a lot.

The following lines get more elements from the game to be used in the script: scene will give you direct access to the current scene; objects is the current list to be used later; font_obj is one element of the objects list (accessed by its name in Blender).

In the above code we used the bge module to get the font game object but using the bge module only we are limiting us to get/set the game object plus to make transforms with this game object (position, rotate or scale). Whether we want to access to the inner parts of the Text object and modify them then we need to understand that the Text object is a bpy object (type TextCurve) and we need to adquire its bpy object data. Once adquired we can use all the properties of bpy.types.TextCurve class.

Remember when we said that the game engine is controller-centric? All the sensors and actuators are accessed from the controller, not from the object they belong to (its owner), as you might expect. Lines 11 and 12, respectively, read the built-in sensor and actuator list to get the ones we are looking for.

In a way similar to how logic bricks work, we are going to activate the actuator if the sensor triggers positive and deactivate it otherwise. The deactivation happens in the frame after the sensor ceases to validate, for example, the key is unpressed or the mouse button is released.

We are not restricted to controlling only actuators, though. Lines 19-21 and 24-26 change the text, the size and the resolution of the object when you press/release the spacebar:

This file can be simple, but holds the essence of the game engine architecture design. Now is a good time to go over the other game engine template files that come with the example 003_template.zip and spend some time studying those examples.

If you haven’t started your own scripts, now is a good time to do so. You will need a text editor, the API modules documented, and a good way to test your files.

It’s important to find a script editor that you find pleasant to work with. The most important features you will be looking for are: syntax coloring and highlighting, auto indentation, and auto completion. You can find editors with even more features than these, so experiment with different alternatives and decide what’s best for you.

As you probably know, UPBGE has its own internal text editor (see next figure). Although it may not be as powerful as software designed exclusively for this particular task, it can be very convenient. It’s useful for quick tests, small scripts, or when you want to keep everything bundled inside the Blender file. Here are its main features:

Indentation conversion (spaces to tabs and vice versa);

Line counting and navigation;

Search over multiple internal files;

Sync with external files;

Icon viewer (small but marvellous feature to get what is the icon that you want to use).

UPBGE internal text editor

External editors as Visual Studio Code or PyCharm have many more features than internal UPBGE Text editor. The weakest point of using external editors is the auto-completion and the documentation visualization directly from the code.

Using a Python API stub generated from UPBGE .rst documentation can solve both issues. In the API Stubs chapter you can see how install the upbge-stubs package to improve the external editor experience.

Since the UPBGE game engine Python API is available online, you have an official excuse to keep a Web browser open while you work. It’s not a bad idea to keep an offline version of it, too. Use it when you need to be more productive and the Internet is getting in your way (as in, always).

It’s good if you can start to gather example materials from the Internet and keep them organized. If you use the append feature in Blender to navigate to and import text files from your “collection”, you will not even need to open another Blender application. Also, if you are consistent with your naming style, indentation rules, and file structures, you will find easy to reuse your own scripts.

It doesn’t matter how easy Python is, you will spend evenings testing and retesting your scripts before you have them working properly. The more complete way to test your script is to play it inside the game engine. However, you may not want to load your game every time you need to be sure of some Python syntax, data types’ built-in functions, or simply to check if the math of a result is correct.

In those cases, you can use an interactive interpreter to help you. If you have Python installed on your system, you have it already. If you are using Windows, this will be the python.exe application in your Python installation directory (C:Python39by default, considering the installation of Python 3.9), as seen in Figure 7.8. In Linux or OSX, you have to type “python” in any console and you are good to go.

You can also use the UPBGE Python console. Change one of your current windows into the console, and you should see the screen shown in the next figure.

UPBGE Python console

Now you can use it to type simple codes, or to run a help or a dir into any of the Python modules. Unfortunately, only Blender modules have the auto-complete working from there.

Additionally, you can also use the in-game python console for debugging the game from python. In the scene properties tab you can activate it and set-up its short-cut.

Set-up In-game UPBGE Python console

To activate it, once the game has started you have to press the short-cut. Then the game will be paused and in the Windows console or linux terminal you will see the interactive python console, as you can see in the next figure. Whether you want to continue the game you need simply ending the interpreter, for Linux Ctrl-D and for Windows Ctrl-Z > Enter.

In-game UPBGE Python console

Another important strategy is to keep the development of new functionalities outside the main file. For example, if you need to develop a navigation system (as we will soon), you don’t need to use your real big, high-textured scenario. Definitively not for the early tests. If you keep independent systems that work together, you will be able to identify errors faster and easier and even to port fixes over to other projects smoothly.

We are now going to dive into an example of writing and planning a Python script for the game engine from scratch. We will assume that you have already covered all the basics of Python scripting and the general understanding of game engine internals so we can move on to its real usage. More specifically, we are going over the writing process of a camera navigation system for an architectural visualization walkthrough. This study case is actually the system developed for a commercial project for an Italian book project. In general, we needed to implement a system to navigate and interact in a virtual model of an Italian Doric temple. Here, however, we are going to develop it under a sandbox and reapply it into another file, emulating what you could do with your own projects.

Unlike gaming cameras, a virtual walkthrough can use a very simple navigation system compound of (1) an orbit mode to look at the exterior of the building; (2) a walk mode to navigate inside the building with gravity simulation and collision; (3) and a fly mode to freely explore the virtual environment with collision only. The other requirement was to make the system as portable as possible, and with the least amount of logic bricks.

All of those aspects must be considered from the first phases of the coding process. With a well-defined design, you can plan the most efficient system in the short and long run.

Pencil and Paper, Valuable Coding Assets

It doesn’t matter how advanced and technical the coding is that you are working on; you can always have a great time sketching your ideas and plans with old-fashioned pencil and paper. This is how the problems are solved, clearly laying down the ideas and organizing them logically.

The system will consist of one camera for the orbit mode, and one to be used for both the fly and walk mode. Each mode works as described in the following table:

Vertical Rotation Angle (Z)

Horizontal Rotation Angle (X)

Horizontal Rotation Pivot

Vertical Rotation Pivot

Empty: is an empty object the camera is parented to.

In order to illustrate it better, you can see the working system demonstrated in the book file: BookChapter74_navigation_systemcamera_navigation.blend. To switch modes press 1, 2, or 3. This will change the mode to orbit, walk, and fly, respectively. To navigate, you can use the mouse and the keys W A S D.

Open up the file BookChapter74_navigation_systemcamera_navigation.blend.

You will find two cameras and different empty objects in the first layer:

scripts - an empty to calls all the scripts.

CAM_Move - the camera for the walk and fly mode.

CAM_Orbit - the camera for the orbit mode.

CAM_back, CAM_front, CAM_side, CAM_top - empties to store the position and orientation for the game cameras.

MOVE_PIVOT - the pivot for the walk and fly camera.

ORB_PIVOT - the pivot for the orbit camera.

In the second layer, you will find the collision meshes[md]the ground and the vertical elements. Everything is very simple here, since we only need to test the system, and for that a few low poly obstacles work fine.

/Book/Chapter7/4_navigation_system/camera_navigation.py

This program is divided into five different parts:

Global Initialization;

The diagram in Figure 7.10 illustrates how they relate to one another. Now let’s take an inside look at each of them.

camera_navigation.init_world()

There is one function that is loaded once at the beginning of the game; we call it init_world inside scripts.py. We are going to check the priority option in the Python controller to make sure this script runs on top of all the others. In this function, you will first find the global initialization. We are going to store in the global module logic all the elements we are going to reuse over the scripts. That way we don’t need to get the object list every time we need a particular object. A common technique is to store the scene object as well. Therefore, for every scene, you can run a script at the beginning of the game that stores a reference to the current scene globally:

Save and Load a game with GlobalDict

Since the module logic is accessible from all the functions and all the scenes, it can be used to store “global” objects. If you need to preserve those objects and variables between game sessions (i.e., after you close your game), you can store them inside the dictionary logic.globalDict and use logic.saveGlobalDict() and logic.loadGlobalDict() to save and load it.

To store the camera information, we are first going to create a global dictionary named cameras. We will use it to store the camera objects, their pivot, and the original orientation of the orbit pivot:

Now that we have our objects instanced, we can set the initial values for our functions, such as the camera rotation restrictions. We don’t want the cameras to look under the ground; thus, we need to manually set our limits. Although we could set those limits directly in the orbit and look functions, having all the parameters in the same part of code is easier to tweak (and slightly faster since they don’t need to be reassigned every frame).

External Settings File

Another common workflow is to have a separate python file (for example, settings.py) with all the variables set. Then in your working script, you simply have to do: import settings.py and use e.g. settings.left.

Last, but not least, we need to create the variables we are going to read and write between the functions. Initializing them here allows us to read them since the first frame of the game. This is especially important for variables that are going to be used in the event management functions - for different values of nav_mode and walk_fly, we are going to run different functions for the camera movement.

Apart from the Always sensor needed for the camera_navigation.init_world() function, there are two other sensors we need - a keyboard and a mouse sensor. All the interaction you will have with this navigation system will run through those functions.

Let’s first take a look at the mouse sensor controlling system:

It looks quite similar to the script template we saw recently. A difference is that instead of activating an actuator, we are calling a function to rotate the view. Actually, according to the current camera (orbit or fly/walk), we will have to call different functions (orbit_camera and look_camera respectively). Also, you can see that the function gets the controller passed as an argument. The game engine passes the controller by default for the module when using the Python Module controller. The argument declaration in the function is actually optional. So you could replace line 210 of the code with the following two lines, and it would work just as well:

The second event management function handles keyboard inputs. This function takes the sensor input and calls internal functions according to the pressed key. If the pressed key is W, A, S, or D, we move the camera. If the key is 1, 2, or 3, we switch it.

For a World with Fewer Logic Bricks

If you don’t want to use a keyboard sensor, you can use an internal instance of the keyboard module. You can read about this in the “bge.logic API” section later in this chapter, or on the online API page: _http://www.blender.org/documentation/blender_python_api_2_66_release/bge.logic.html#bge.logic.keyboard._

These three functions are called from the event management functions. In their lines, you can find the math responsible for the camera movement. We’re calling them “internal functions” because they are the bridge between the sensors’ inputs and the outputs in the game engine world.

The function responsible for the camera movement is very simple. In the walk and fly mode, we are going to move the pivot in the desired direction (which is passed as argument). Therefore, we first need to create a vector to this course. If you are unfamiliar with vectorial math, think of vector as the direction between the origin [0, 0, 0] and the vector coordinates [X, Y, Z].

Here the vector is the movement we need to apply to the pivot in order to get it moving. The size of the vector (MOVE) will act as intensity or speed of the movement.

We decided to use different methods for the walk/fly camera and the orbit one. In the orbit camera, every position on the screen corresponds to an orientation of the camera.

If you want to study this part of the script in particular, you can turn on the Mouse Cursor in the Render Panel. That way, you can see that the same cursor position will (or should) always generate the same view.

The first lines that deserve our attention here are the normalizing operation. To normalize a value means to convert it to a range from 0.0 to 1.0. In our case, it can be understood as the mouse pointer coordinates relative to the screen dimensions (width and height):

Even Fewer Logic Bricks and Normalized Mouse Coordinates

It’s important to always use normalized coordinates for your screen operations. Otherwise, different desktop resolutions will produce different results in a game. As a counter edge case, you may need the absolute coordinates for mouse events if you want to assure minimum clickable areas for your events. You don’t always need to normalize the mouse coordinates manually. Like the keyboard sensor, you can replace the mouse sensor by an internal instance of the mouse module. The coordinates from bge.logic.mouse run from 0.0 to 1.0 and can be read anytime. (You can even link your script to an Always sensor, leaving the Mouse sensor for the times where you are using more logic bricks.) You can read about this in the “bge.logic API” section in this chapter or on the online API page: _http://www.blender.org/documentation/blender_python_api_2_66_release/bge.logic.html#bge.logic.keyboard_

Now a simple operation to convert the normalized value into a value inside our horizontal angle range (-220º to 220º):

We run the same operation for the vertical coordinate of the mouse. Though you must be aware that the canvas height runs from the top (0) to the bottom (height), this is different from what we could expect (or from OpenGL coordinates, for example). In order to better understand the flipping operation (line 257), you can first comment/uncomment the code to see the difference.

Next find in the .blend file the pivot empty (ORB_PIVOT) and play with its rotation in the X axis. The rotation is demonstrated in Figure 7.11. Therefore, if we subtract our angle from 90º (__PI__/2 in radians), we get the proper angle to rotate the pivot vertically.

Orbit pivot rotation

The function to rotate the walk/fly camera is quite different from the orbit one. We don’t have a direct relation between mouse coordinate and camera rotation anymore. Here we get the relative position of the cursor (from the center) and later force the mouse to be re-centered[md]to avoid continuous movement unless the mouse is moved again.

In order to get the relative position of the cursor, the normalizing function needs to be different. This time we want the center of the screen to be 0.0 and the extreme edges of the canvas (border of the game window) to be -0.5 and 0.5.

The values of x and y can be used directly as radians angles to rotate the camera. However, when we are walking, we want to restrict the view vertically. This design decision means that we need to limit the view angle to a maximum and minimum range. Sure, this turns tying your shoes into a circus challenge. Though it may seem like overkill, this limitation helps add a better sense of reality to our navigation system.

The solution is to get the current camera vertical angle and see if by adding the new angle (i.e., vertical mouse move) we would end up over the limit of 45º. If so, we clamp the new angle to respect this value. To get the vertical angle, remember that the camera pivot (an empty object) is always parallel to the ground. Therefore, the vertical angle can be extracted from the camera’s local orientation matrix. If that still doesn’t make sense to you, try to find some 3D math tutorials online).

For the actual project this was originally designed for, we ended up moving the orbit camera code to be a subset of the walk/fly. Having the mouse always centered comes in handy when you have a user interface on top of that, and it needs to alternate between mouse clicking and camera rotating. Although the methods are different, the results are the same.

And the outcome of the functions:

In the previous section, we saw how the angles and directions were calculated with Python. However, we deliberately skipped the most important part: applying it to the game engine elements. It includes activating actuators (as we do in the change_view() function) or directly interfering in our game elements (cameras and pivots).

Let’s put the pieces together now. We already know the camera future orientation and position. Therefore, there is almost nothing left to be calculated here. Nevertheless, there are distinct ways to change the object position and orientation.

In move_camera(), we are going to use an instance method of the pivot object called applyMovement (vector, local). This is part of the game engine methods (another one is applyRotation you will see next) we explain later in this chapter in the “Using the Game Engine API” section. This built-in function translates the object using the vector passed as a parameter. It can either be relative to the local or world coordinates:

In a similar way in the look_camera() function, we will apply the rotation in the camera object. This has the advantage of sparing the hassles of 3D math, matrixes, and orientations. Also, instead of manually computing the new orientation matrix in Python, we can rely on the game engine C++ native (i.e., fast) implementation for that task.

Although we are leaving the math calculation to the game engine, we should still be aware of how it works. The applyRotation() routine works with Euler angles (as a gimbal machine). The effects for the walk and the fly modes are very similar. The only difference is whether the rotation is local or global and the axis to rotate around:

In the orbit_camera() function, we calculated the orientation matrix of the pivot. This matrix is no more than a fancy mathematical way of describing a rotation. Since we already have the matrix, all we need to do is to set it to our pivot orientation.

The orientation is a Python built-in variable that can be read and written directly by our script. We will talk more about this in the “Using the Game Engine API - Application Programming Interface” part of this chapter.

After the user presses a key (1, 2, or 3) to change the view, we call the change_view() function to switch to the new camera (with a parameter specifying which camera to use). This function consists of two parts: first, we set the correct position and orientation for the camera and pivot; secondly, we change the current camera to the new one.

Decomposing the View Orientation

Keep in mind that the desired orientation (stored in the empty and accessed through the G.views dictionary) represents the new view orientation. In our system, this view orientation is the combination of the parent object (pivot) orientation with the child one (camera).

Let’s start simple and build up as we go. First the orbit camera: in the orbit mode the camera is stationary[md]its position never changes. All we need to do is reset the pivot orientation to its initial values. Its orientation was globally stored back in the init_world() function. So now we can retrieve and apply it to the pivot:

The fly camera is slightly different. In this case, the camera orientation contains no rotation (i.e., an identity matrix). Therefore, it’s up to the pivot orientation to match the view orientation. In other words, the pivot orientation matrix is exactly the same as the view orientation matrix:

For the walk camera, we have yet another situation. The mode we are coming from (fly) has the camera pivot orientation (same as camera.worldOrientation) as the current view orientation. However, for the walk mode, the pivot needs to be parallel to the ground.

For that, we need to rotate it a few degrees to align with the horizon. The camera now will be looking to a different point (above/below the original direction). In order to realign the camera with the view orientation, we need to rotate the camera in the opposite direction. This way, the pivot and camera rotations void each other (with the benefit of having the pivot now properly aligned with the ground).

Reasoning Behind the Design

There is another reason for keeping this as a separate function. Originally, I was planning to switch modes (walk/fly) while keeping the same camera position and view. Although I dropped the idea, I decided to keep the system flexible in case of any turn of events (clients who understands their minds?).

Now that the new camera and pivot have the correct position and orientation, we can effectively switch cameras. For that, we first set the new camera in the Scene Set Camera actuator. Next, we activate the actuator and the camera will change:

The script system shown so far handles all the interaction from the game engine sensors to the 3D world elements. Even though this covers most parts of a typical script architecture, I’d be lying if I said this is all you will be doing in your projects. Very often, you will need a script called once in a while that deals directly with the game engine data. In our case, we will have two “PySensors” to control the collision and to stick our camera to the ground while walking.

We could have them both working attached to an Always sensor. However, this would not be too efficient. Since we only need them while walking and flying, they can be integrated with the Keyboard sensor pipeline. The stick_to_ground() function will be called after any key is pressed if the current mode is “walk”:

The collision system can be used even more specifically. Inside the move_camera() function, we will use the collision test to validate or discard our moving vector:

If the collision_check() test finds any obstacle in front of the camera, it returns a null vector ([0, 0, 0]). Otherwise, it leaves the vector as it was set, which will then move the camera.

The code of those functions is very particular to this project; therefore, we’re not going into more detail here. (You are encouraged to take a look at the complete code in the book file, though). Nevertheless, the key point is to understand the role of those functions in the script architecture. Those scripts can complement the functionality of other functions, to rule your game in a global and direct way, or simply to tie things together.

One of the reasons this system was designed so carefully is because of the need for portability. You don’t want to rewrite a navigation system every time you have a new project. This is not particular to this script example. Very often, you will be recycling your own scripts to adapt them to new files. Let’s go over some principles you should know.

The first thing to have in mind is how your final file will look. Do you want the script system to be merged with the rest of the existent Blender file? Do you want to keep them in separated scenes (very common for user interfaces)? Will you need to access/edit the script system elements later?

In our case, there is no need for an extra scene. However, we need to make sure that the navigation system elements are easy to access (especially the empties with the cameras’ positions). If you can afford to dedicate one layer exclusively to the navigation system elements, do it. Make sure that the desired layer is empty in the model file and that all the objects you want to import are contained in this layer.

If it’s not possible to have all your elements in a single layer, you can create a group for them. That way, you can always quickly isolate them to be listed in the outliner and selected individually. The other advantage of using groups is during importing. It’s easier to select a group to be imported than to go over all the individual objects, determining which one should be imported and which one is part of the test environment (which usually doesn’t have to be imported).

Open the file /Book/Chapter7/4_navigation_system/walkthrough_1_base/walkthrough.blend

This small file is part of the presentation of an architectural walkthrough of an urban project (see Figure 7.12) that I (Dalai) did. It’s an academic project and only my second project using the game engine. As you can see, there are absolutely no scripts in it[md]all the interaction is done with logic bricks. I didn’t use Python for this project mainly because I had absolutely no knowledge of Python at all back then (and the project was done in six days).

Architectural walkthrough example file

It’s time for redemption. Let’s replace its navigation system with the Python system we just studied. For convenience, this file was already organized to receive the navigation elements (cameras, empties, and so on.).

In this case, we decided to group all the navigation elements in a group called NAVIGATIONSYSTEM and to make sure they are all in layer 1. You can use the Outliner to make sure you didn’t miss any object out of the group. Leave the lamps and the collision objects out of the group.

To see a snapshot of the file at this moment, you can find it in the book files at: /Book/Chapter7/4_navigation_system/walkthrough_2_partial/camera_navigation.blend

Now open the walkthrough file again and append the NAVIGATIONSYSTEMwe created. It’s important not to link the group but to append it. Linked elements can only be moved in their original files; thus, you should avoid them in this case.

Open the Append Objects Dialog (Shift+F1).

Find the NAVIGATIONSYSTEM group inside the camera_navigation file.

Make sure the option “Instance Groups” is not checked. (This would insert the group, not the individual elements.)

Click on the “Link/Append from Library”. (This will add the group.)

Set CAM_Orbit as the default camera. (Tip: Use the Outliner to find the object; it’s inside the ORB_PIVOT.)

A snapshot with those changes can be found at:

/Book/Chapter7/4_navigation_system/walkthrough_2_partial/walkthrough.blend

Now if you run the application, the navigation system should work - kind of (see Figure 7.13).

As you can see in Figure 7.13, the new camera system looks absurdly wrong. There are two main reasons for that: the walkthrough file elements are far away from the file origin [0, 0, 0], and the cameras are not prepared for a project with this magnitude (their clipping parameters are way too low). We will need to move the objects to their new correct places, adjust the camera parameters, and do a small intervention in the script file:

All the elements from NAVIGATIONSYSTEM group (layer 1):

Move them 2000 in X and 350 in Y.

CAM_front and CAM_back - Those empties will hold the position for walk cameras. Make sure their position from the ground is at the human eyes (~1.68).

CAM_top and CAM_side - Those empties will be used in Fly Mode. Here, we should also make sure their initial orientation looks good. The easiest way to do that is by using the Fly Mode (select the object, set it as current camera, and use Shift+F).

The one thing missing for the camera is to increase the clipping distance. That way, we can see all the skydome around the camera (see before and after in Figure 7.14).

CAM_Orbit - Adjust initial Z, change clip ending to 1000.

CAM_Move - change clip ending to 1000.

A snapshot with those changes can be found at:

/Book/Chapter7/4_navigation_system/walkthrough_3_partial/walkthrough.blend

Camera clipping of 400

Camera clipping of 1000

Make Sure That Collision Is Set Properly

All the houses, the ground, and the other 3D objects already have collision enabled in this file. In other situations, however, you may need to change the collision objects, enabling or disabling their collisions accordingly. The Python raycast uses the internal Bullet Physics engine under the hood. In order to prevent the camera from going through the walls and the ground, set enough collision surfaces (but not too much, so that you don’t compromise the performance of your game).

Finally, it’s good to fiddle a bit with the script. Due to the particularities of this project (mainly its scale), you may feel that everything happens a bit too fast. It’s up to you to change the settings in the init_world function. Also, it would be interesting to explore multiple viewpoints for this presentation. We have already positioned the side and back empties. Although we were not using them previously, their names are present in the script as part of the available cameras list:

The difference now is that we will make the camera actually change to the side and back views when you press the keys four and five respectively. As you can see here, it’s really easy to expand a system like this. Try to create a fifth camera (add a new empty) and see how it goes. To enable the “side” and “back” cameras, the only code we have to add is:

There is not much more to be done here. This is a simple script, but its structure and the workflow we presented are not much different from what you will find in more complex systems you may have to implement or work with. There are different ways to implement a navigation system. This one was designed focusing on a didactic structure (clean code as opposed to a highly optimized system that is hard to read) and robustness (easy to expand). Try to find other examples or, better yet, build one yourself.

The final file is on the book files as:

/Book/Chapter7/4_navigation_system/walkthrough_4_final/walkthrough.blend.

The game engine API is a bridge connecting your Python scripts with your game data. Through those modules, methods, and variables you can interact with your existent logic bricks, game objects, and general game functions.

The official documentation can be found online in the Blender Foundation website (TODO to be changed):

http://www.blender.org/documentation/blender_python_api_2_66_release

We will now walk through the highlights of the modules. After you are familiar with their main functionality, you should feel comfortable to navigate the documentation and find other resources.

Game Engine Internal Modules

Game Logic (bge.logic)

Game Types (bge.types)

Rasterizer (bge.render)

Game Keys (bge.events)

Video Texture (bge.texture)

Physics Constraints (bge.constraints)

Application Data (bge.app) //TODO

Math Types and Utilities (mathutils)

The main module is a mix of utility functions, global game settings, and logic bricks replacements. Some of those functions were already covered in the tutorial, but they are here again for convenience sake. We will look at some of the highlights.

Returns the current controller. This is used to get a list of sensors and actuators (to check status and deactivate respectively), and the object the controller belongs to:

If you are using Python modules instead of Python scripts directly (see Python Controller), the controller is passed as an argument for the function:

This function returns the current scene the script was called from. The most common usage is to give you a list of all the game objects:

If you need to access an external file (image, video, Blender, etc.), you need to first get its absolute path in the computer. Use single backslash (/) to separate folders and double backslash (//) if you need to refer to the current folder:

These functions copy the functionality of existent actuators. They are Python replacement for those global events when you need a direct way to call them, bypassing the logic bricks.

There are cases when you need to load the content of an external Blender file at runtime. This is known as _dynamic loading._ The game engine supports dynamic loading of actions, meshes, or complete scenes. The new data blocks are merged into the current scene and behave just like internal objects:

New Lamp objects can be dynamically loaded from external files. However, in GLSL mode, they will not work as a light source for the material shaders, since the shaders would need to be recompiled for that.

The bge.logic.globalDict is a Python dictionary that is alive during the whole game. It’s a game place to store data if you need to restart the game or load a new file (level) and need to save some properties. In fact, you can even save the globalDict with the Blender file during the game and reload later.

You can handle all the keyboard inputs directly from a script. The usage and syntax are very similar to the Keyboard sensor. You need a script running every logic tic (Always sensor pulsing with a frequency of 0 or every time a key is pressed; Keyboard sensor with “All Keys” set) where you can read the status of all the keys in the bge.logic.keyboard. events dictionary. If instead of inquiry for the status of a particular key (e.g., if spacebar is pressed), you want to list all the pressed keys, you can use the dictionary bge.logic.keyboard.active_events.

The keys for both event dictionaries are the same you use with the Keyboard sensor (see the bge.events module). The status of each key (whether it was pressed, released, kept pressed, or nothing) is the value stored in the dictionary. The keys values are defined in the bge.logic module itself:

A sample file can be seen at BookChapter75_game_keyskey_detector_python.blend . This shows the more Python-centric way of handling keyboard. For the classic method of using a Keyboard sensor, look further in this chapter into the “bge.events” section.

Similar to the keyboard, this Python object can work as a replacement for the Mouse sensor. There are a few differences that make it even more appealing for scripting[md]in particular, the fact that the mouse coordinates are already normalized. As we explained in the tutorial, this helps you get consistent results, regardless of the desktop resolution. The available attributes are:

events - a dictionary with all the events of the mouse (left-click, wheel up, and so on) and their status (for example, bge.logic.KX_INPUT_JUST_ACTIVED).

position - normalized position of the mouse cursor in the screen (from [0,0] to [1,1]).

visible - show/hide the mouse cursor (can also be set in the Render panel for the initial state).

This is a list of all the joysticks your computer supports. That means the list is mainly populated by None objects, and a few, if any, joystick Python objects. To print the index, name, number of axis, and active buttons of the connected joysticks, you can do:

There are even more functions available in this module (setMist, getLogicTicRate, and setGravity, for example). Make sure that you visit the online documentation (or the documentation included on the book files) to see them all.

Objects, meshes, logic bricks, and even shaders are all different game types. Every time you call an internal function from one of them, you are accessing one of those functions. This happens when you get a position of an object, change an actuator value, and so on.

Each one of the classes has the same anatomy. You can access instance methods and instance variables. In order to explain their use properly, we will go over one of the most commonly used modules, the game object.

Some of the variables will only work inside the correct context. Therefore, you can’t get the mouse position of a Mouse sensor if the sensor was not triggered yet. Be aware of the right context and the game type.

If you run a print(dir (object)) inside your script, you will get a very confusing list. It includes Python internal methods, instance methods, and instance variables. Most of them are common to all objects, so we are going to talk about them first. However, lamps and cameras not only inherit all the game object methods but also extend them with specific ones.

The Truth Is Out There

In order to see all available methods, please refer to the documentation. We are only covering a few of them here.

__class__, __doc__, __delattr__ …

Most of those methods are inherited from the Python object we are dealing with. However, given the nature of the Python classes presented in Blender, some of those methods may not be fully accessible. It’s unlikely you will be using them. So for now it’s safe to ignore any method starting and ending with double underlines (__ignoreme__).

endObject(), rayCast(), getAxisVect(), suspendDynamics(), getPropertyNames() …

If it looks like a function, it should be one. Every game engine object provides you with a set of functions to interact with them or from them to the others. Here are some methods you should know about:

rayCast (objto, objfrom, dist, prop, face, xray, poly)

“Look from a point/object to another point/object and find first object hit within dist that matches prop.”

This method is a more complete version of the rayCastTo(). It has so many applications that it becomes hard to delimitate its usage. For instance, this was the method used to calculate the collision in the navigation system script we studied previously.

“Get a list of all property names.”

Once you retrieve the list of property names, you can use it to see if the object has a specific property before using it. To get individual properties, you can use if “prop” in object: or object.get(“prop”, default=None).

Properties have multiple uses in the game engine. One of those uses is to mark an object to be identified by the Python script. Why not use their names instead? While names work fine to retrieve individual objects, properties allow you to easily mark and access multiple objects at once. Frankly, it’s easier to create an organized, named, and tagged MP3 collection than it is to find time to properly name all your Blender data blocks[ms]objects, meshes, materials, textures, images, and so on.

“Delete this object can be used in place of the EndObject Actuator.”

This method is one of the functions that mimic existent actuators. You will also find this design in methods such as sendMessage(), setParent(), and replaceMesh().

“Set the game object’s movement/rotation.”

There are a few methods that will free you from doing 3D math manually. This particular one is a replacement for multiplying the object orientation matrix by a rotation matrix. (If you are “old school,” you can still set the orientation matrix directly though.)

Other methods are applyMovement(), applyForce(), applyTorque(), getDistanceTo(), getVectTo(), getAxisVect(), and alignAxisToVect().

_name, position, mass, sensors, actuators …_

Last but definitively not least, we have the built-in variables. They work as internal parameters of the object (for example, name, position, orientation) or class objects linked to it (for example, parent, sensors, actuators). In Blender versions prior to 2.49, those variables were only accessible through a conjunct of get and set statements (setPosition(), getOrientation(), and so on). In Blender 2.5, 2.6 and on, they not only can be accessed directly, but also manipulated as any other variable, list, dictionary, vector, or matrix you may have:

position, localPosition, worldPosition

Position is a vector [x, y, z] with the location of the object in the scene. We can get the absolute position (worldPosition) or the position relative to the parent of the object (localPosition). And what about accessing the position variable directly? This is deprecated, but you may run into it in old files you find online. If you access the position variable directly, you get the world position on reading and set the local position on writing. Confusing? That is why this is deprecated ;)

orientation, localOrientation, worldOrientation

This variable gives you access to a matrix 3x3 with the orientation of the object. The orientation matrix is the result of the rotation transformation of an object and the influence of its parent object. As with position, the orientation variable will give you the world orientation on reading and set the local orientation on writing. As with position, you should always specify whether you want the local or world orientation.

We have different ways to set the visibility of an object. If your material is not set to invisible in the game panel, you can use this method. To change the visibility recursively (to the children of the object), you must use the method setVisibility.

sensors, controllers, actuators

All the logic bricks of an object can be accessed through those dictionaries. The name of the sensor/controller/actuator will be used as the dictionary key, for it’s important to name them correctly.

Not all the objects have access to the same methods and variables. For example, an empty object doesn’t have mass, and a static object doesn’t have torque.

When the object is a camera, the difference is even more distinct. The camera object has its own class derived from KX_GameObject. It inherits all the instance variables and methods and expands it with its own. You will find some screen space functions (getScreenPosition(),getScreenVect(), getScreenRay()), some frustum methods (sphereInsideFrustum(), boxInsideFrustum(), pointInsideFrustum()), and some instance variables (lens, near, far, frustum_culling, world_to_camera, camera_to_world).

Like cameras, lamps also have their own subclass. It inherits all the instance variables and methods, and only expands the available variables.

The parameters that can be changed with Python include all that can be animated with the Action actuator: energy, color, distance, attenuation, spot size, and spot blend. Additionally, you can change the lamp layer in runtime.

If we compare gaming with traditional 3D artwork, rasterizer would be the rendering phase of the process. Internally, it’s when all the geometry is finally drawn to the screen with the light calculation, the filters applied, and the canvas set. For this reason, the Rasterizer module presents functions related to stereoscopy, windows and mouse management, world settings, and global GLSL material settings.

getWindowWidth() / getWindowHeight()

Get the width/height of the window (in pixels).

Enable or disable the operating system mouse cursor.

setMousePosition(x, y)

Set the mouse cursor position (in pixels).

setBackgroundColor(rgba), setAmbientColor(rgb)

Set the ambient and background color.

setMistColor(rgb), disableMist(), setMistStart(start), setMistEnd(end)

Configure the mist (fog) settings.

getEyeSeparation() / setEyeSeparation(eyesep)

Get the current eye separation for stereo mode. Usually focal length/30 provides a comfortable value.

getFocalLength() / setFocalLength(focallength)

Get the current focal length for stereo mode. It uses the current camera focal length as initial value

getMaterialMode(mode) / setMaterialMode(mode)

Get/set the material mode to use for OpenGL rendering. The available modes are:

KX_TEXFACE_MATERIAL, KX_BLENDER_MULTITEX_MATERIAL, KX_BLENDER_GLSL_MATERIAL

getGLSLMaterialSetting(setting) / setGLSLMaterialSetting(setting, enable)

Get/set the state of a GLSL material setting. The available settings are:

“lights”, “shaders”, “shadows”, “ramps”, “nodes”, “extra_textures”

drawLine(fromVec, toVec, color)

Draw a line in the 3D scene.

enableMotionBlur(factor) / disableMotionBlur()

Enable/disable the motion blue effect.

makeScreenshot(filename)

Write a screenshot to the given filename.

The Keyboard sensor allows you to set individual keys. As you can see in Figure 7.15, it can also be triggered by any key once you enable the option “All Keys.” This is very useful to configure text input in your game or to centralize all keyboard events with a single sensor and script.

![Key codes visualizer](../figures/Chapter7/Fig07-15.png)

In this case, every key pressed into a Keyboard sensor, will be registered as a unique integer. Each number corresponds to a specific key, and finding them allows you to control your actions accordingly to the desired key map. In order to clarify this a bit more, try the file in /Book/Chapter7/5_game_keyskey_detector_logicbrick.blend.

This file is similar to the key_detector_python.blend we used to demonstrate bge.logic.keyboard. However, this file is using the Keyboard sensor directly, instead of its wrapper.

This script is called every time someone presses a key. The key (or keys) are registers as a list of events, each one being a list with the pressed key and its status. In this case, we are reading only the first pressed key:

pressed_key = sensor.events[0][0]

This line stores the integer that identifies the pressed key. However, we usually would need to know the actual pressed key, not its internal integer value. Therefore, we are using the only two functions available in this module to convert our key to an understandable value:

After that, we are checking for a specific key (spacebar). bge.events.SPACEKEY is actually an integer (to find the other keys’ names, visit the API page):

And, voilà, now we only need to visualize the pressed key:

The status of a key is what informs you whether the key has just been pressed or if it was pressed already. The Keyboard sensor is always positive as long as any key is held, and you may need to trigger different functions when some keys are pressed and released. The status values are actually stored in bge.logic:

The texture module was first discussed in the Chapter 5, “Graphics.” With the texture module, you can change any texture from your game while the game is running. The texture can be replaced by a single image, a video, a game camera, and even a webcam stream.

Let’s look at a basic example. Please open the file: BookChapter76_texturebasic_texture_replacement.blend.

This file has a single plane with a texture we will replace with an external image. Press the spacebar to change the image and Enter to return to the original one. The script responsible for the texture switching is:

It’s a simple script, but let’s look at the individual steps. We start by getting the material ID (that can be retrieved for an image used by an object, hence the prefix IM) or a material that uses a texture (with the prefix MA).

With this ID, we can create a Texture object that controls the texture to be used by this object (and the other objects sharing the same image/material).

The next step is to create the source to replace the texture with. The bge.texture module supports the following sources: ImageFFmpeg (images), VideoFFmpeg (videos), ImageBuff (data buffer), ImageMirror (mirror), ImageRender (game camera), ImageViewport (current viewport), and ImageMix (a mix of sources).

Now we only need to assign the new source to be used by the object texture and to refresh the latter. The refresh function has a Boolean argument for advanced settings. A rule of thumb is: for videos, use refresh (True); for everything else, try refresh (False) first.

For the image to be permanent, we have to make sure the new dynamic_texture is not destructed after we leave our Python function. Therefore, we store it in the global module bge.logic. If you need to reset the texture to its original source, simply delete the stored object (for example, del logic.dynamic_texture).

Since this is a simple image, you don’t need to do anything after that. If you are using a video as source, you need to keep refreshing the texture every frame. Videos also support an audio-video syncing system. To make them play harmoniously together, you first play the audio and then query its current position to pass as a parameter when updating the video frame (for example, _logic.video.refresh(True, logic.sound.time)_). The audio can come from an Audaspace object or even a Sound actuator.

In the book files, you can find other examples using different sorts of source objects:

Basic replacement of texture:

/Book/Chapter7/6_texture/basic_texture_replacement.blend

Basic video playback with Sound actuator:

/Book/Chapter7/6_texture/basic_video_sound.blend

Video player with interface controllers:

/Book/Chapter7/6_texture/player_video_audio.blend

Basic video playback with Audaspace:

/Book/Chapter7/6_texture/video_audaspace.blend

/Book/Chapter7/6_texture/mirror.blend

/Book/Chapter7/6_texture/render_to_texture.blend

/Book/Chapter7/6_texture/webcam.blend

The Bullet Physics engine allows for advanced control over the physics simulation in your game. Using Bullet as a backend, this module (formerly known as Physics Constraints) allows you to create and set up rigid joints, dynamic constraints, and even a vehicle wrapper. The constraints’ functionalities make sense only when you understand the context in which they are to be used (with physic dynamic objects). Therefore, this module is covered in the previous chapter on game physics.

Mathutils is a generic module common to both Blender and the game engine. There are a lot of methods to facilitate your script in handling 3D math operations. You won’t have to reinvent the wheel every time you need to multiply vectors or transpose matrixes. Simply using the mathutils classes and built-in methods frees you to invest your time in something far more important: relearning all of the long-forgotten math lessons you skipped.

Unless your background is in math, physics, or engineering, you won’t use this module any time soon. For those already familiar with the passionate secrets of math, you’ll be glad to know that those module’s functions are mainly self-explanatory. Names such as cross, dot, slerp (what?), and a quick look at their specifications will be all you need to know to start working with them. Nevertheless, newcomers often use this module without even knowing it. Every time you change an object position, get the vector from an object, or apply a rotation, you are using mathutils classes and methods. Therefore, it’s good to have this module as a reference for further studies and more advanced coding. (We all get there eventually.)

We are going to present the four available classes in this module: vector, matrix, Euler, and quaternion. For a list of the available methods, refer to the API documentation.

This class was already present in the KX_GameObject class and in the script example. It behaves like a list object, with some advanced features (for example, swizzle and slicing) expanded with its instance methods. Some of those methods are: reflect, dot, cross, and normalize.

A recurring problem that new Python programmers have is with list copying. If you forget to manually copy the list when assigning it to a new variable, you end up with two variables sharing the same list values forever (each of the variables becomes a pointer to the same data).

The same behavior happens with Vectors. Look at the differences:

new_vector = old_vector

if you change new_vector you will automatically change old_vector (and vice-versa).

new_vector = old_vector[:]

new_vector is a new independent list object initialized with the old_vector values.

new_vector = vector.copy()

new_vector is a new Vector, an independent copy of the old_vector object.

While vectors behave similarly to lists, matrices behave similarly to multidimensional lists. A multidimensional list is a list of a list, organized either in columns or rows.

While in Python, a list of a list is always the same:

matrix_row = [[1,2,3], [4,5,6], [7,8,9]]

In a mathutils.Matrix, the data can be stored differently, accordingly to the matrix orientation (row/column). Following you can see how the order of the elements in a matrix changes, according to its orientation (note, this is not actual Python code):

It’s important to be aware of the ordering of your matrices; otherwise, you end up using a transposed matrix for your calculations. Since all the game engine internal matrices (orientation, camera to world, and so on) are column-major oriented, you will be safer sticking to this standard.

If your matrix represents a transformation matrix (rotation, translation, and scale) you can get its values separately. Matrix.to_quaternion() and Matrix.to_euler() will give you the rotation part of the matrix in the form you prefer (see next section), and Matrix.to_translation() and Matrix.to_scale () will give you the translation and the scale vector, respectively.

Euler and quaternion are different rotation systems. The same rotation can be represented using Euler, quaternion, or an orientation matrix.

You can find two great video tutorials on the Guerrilla CG vimeo channel that explain and compare the two rotation system:

Euler Rotations Explained: http://vimeo.com/2824431

The Rotation Problem: http://vimeo.com/2649637

When you convert an orientation matrix to Euler (Matrix.to_euler()), you get a list with three angles. They represent the rotation in the x, y, z axis of the object. In the navigation system script example, we are using this exact method to determine the horizontal camera angle. You can find this usage in the function fly_to_walk() (lines 190 to 199 of navigation_system.py or in the early pages of this chapter).

Conversion Between Different Rotation Forms

You can convert an orientation matrix to Euler, an Euler to a quaternion, a quaternion to an orientation matrix, and on and on and on:

In this example, converted_matrix ends up as the same matrix as original_matrix.

This module allows you to play sounds directly from your scripts. There are three classes you will be working with: Device, Factory, and Handle.

The audaspace module in a nutshell: you need to create one audio Device per game. You need one Factory per audio file (which can also be any video file containing a sound track). And every time you need to play a sound, a new Handle object will be generated from the Factory (this is where its name comes from).

## load sound file (it can be a video file with audio)

## play the audio, this return a handle to control play/pause

## if the audio is not too big and will be used often you can buffer it

## stop the sounds (otherwise they play until their ends)

We start by creating an audio device. This is simply a Python object you will use to play your sounds. Next, we create a Factory object. A factory is a container for a sound file. When we pass the Factory object into the device play function, it will start playing the sound and return a handle. Handles are used to control pause/resume and to stop an audio.

When Will This Music Stop?

After you initialize a sound, you can get its current position in seconds with the handle.position Python property. This is especially useful to keep videos and audio in sync. If you need to check whether or not the audio is ended, you shouldn’t rely on the position, though. Instead, you can get the status of the sound by the property handle.status. If you are using the sound position to control a video playback, the sound status will also tell you if the video is over (handle.status = aud.AUD_STATUS_INVALID). The possible statuses are:

This module is a wrapping of OpenGL constants and functions. It allows you to access low-level graphic resources within the game engine. You can use this module to draw directly to the screen or to read OpenGL matrices and buffers directly.

Sometimes, you will need to run your OpenGL code specifically before or after the game engine drawing routine, so you can store your Python function as a list element either in the scene attributes pre_draw and/or in the post_draw. This will be demonstrated in our first example.

You can find good OpenGL learning material on the Internet or in a bookstore. The Official Guide to Learning OpenGL (also known as The Red Book) is highly recommended, and some older versions of it can be found online for download.

Open the file /Book/Chapter7/7_bgl/line_width.blend.

(run it in wireframe mode)

This code needs to run only once per frame and will change the line width of the objects. Be aware that the line is only drawn in the wireframe mode.

You will find on the book files another example where the line width changes dynamically - /Book/Chapter7/7_bgl/line_width_animate.blend.

Open the file /Book/Chapter7/7_bgl/color_pickup.blend.

In this file, you can change the light color according to where you click.

There are three important bgl methods been used here. The first one is bgl.Buffer. It creates space in the memory to be filled in with information taken from the graphics driver:

The second one is the bgl.glGetIntegerv. We use it to get the current Viewport position and dimension to the buffer object previously created:

The buffer coordinates run from the left bottom [0.0, 0.0] to the right top [1.0, 1.0]. The mouse coordinates, on the other hand, run from left top [0, 0] to the right bottom [width, height]. We need to convert the mouse coordinate position to the correspondent one in the Buffer.

The third one is bgl.glReadPixels. This is the method that’s actually reading the pixel color and storing it in the other buffer object:

And, finally, let’s apply the pixel color to the lamp:

If you need to control text drawing directly from your scripts, you may need to use this module. Be aware, though, that this module is a low-level API that has to be combined with the OpenGL wrapper to handle texts properly.

The blf module works in three stages:

Create a new font object.

Set the parameters for the text (size, position, and so on).

Draw the text on the screen.

Open the file /Book/Chapter7/8_blf/hello_world.blend.

In the init function, we load a new font in memory and store the generated font ID to use later.

The actual function responsible for writing the text is stored in the scene post_draw routine. Apart from the OpenGL calls, the setup for using the text is quite simple.

On the book files, in the same folder, you can find two other examples following the same framework: hello_world_2.blend and object_names.blend.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (python):
```python
import bge
from bge import logic

# Use bge module to get/set game property + transform
cont = logic.getCurrentController()
owner = cont.owner
scene = logic.getCurrentScene()
objects = scene.objects
font_object = objects["Text"]

# Use bpy.types.TextCurve attributes to set other text settings (size, body, etc)
font_object_data = font_object.blenderObject.data

sens = cont.sensors['my_sensor']
act = cont.actuators['my_actuator']

if sens.positive:
  cont.activate(act)
  font_object_data.body = "CADABRA"
  font_object_data.size = 2
  font_object_data.resolution_u = 1
else:
  cont.deactivate(act)
  font_object_data.body = "ABRA"
  font_object_data.size = 1
  font_object_data.resolution_u = 4
```

Example 2 (python):
```python
import bge
from bge import logic

# Use bge module to get/set game property + transform
cont = logic.getCurrentController()
owner = cont.owner
scene = logic.getCurrentScene()
objects = scene.objects
font_object = objects["Text"]

# Use bpy.types.TextCurve attributes to set other text settings (size, body, etc)
font_object_data = font_object.blenderObject.data

sens = cont.sensors['my_sensor']
act = cont.actuators['my_actuator']

if sens.positive:
  cont.activate(act)
  font_object_data.body = "CADABRA"
  font_object_data.size = 2
  font_object_data.resolution_u = 1
else:
  cont.deactivate(act)
  font_object_data.body = "ABRA"
  font_object_data.size = 1
  font_object_data.resolution_u = 4
```

Example 3 (python):
```python
import bge
from bge import logic

# Use bge module to get/set game property + transform
cont = logic.getCurrentController()
owner = cont.owner
scene = logic.getCurrentScene()
objects = scene.objects
font_object = objects["Text"]

# Use bpy.types.TextCurve attributes to set other text settings (size, body, etc)
font_object_data = font_object.blenderObject.data

sens = cont.sensors['my_sensor']
act = cont.actuators['my_actuator']

if sens.positive:
  cont.activate(act)
  font_object_data.body = "CADABRA"
  font_object_data.size = 2
  font_object_data.resolution_u = 1
else:
  cont.deactivate(act)
  font_object_data.body = "ABRA"
  font_object_data.size = 1
  font_object_data.resolution_u = 4
```

Example 4 (python):
```python
import bge
from bge import logic
```

---

## Python

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/python/index.html

**Contents:**
- Python

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Python Components

**URL:** https://upbge.org/docs/latest/manual/manual/python_components/index.html

**Contents:**
- Python Components

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Python Scripting

**URL:** https://upbge.org/docs/latest/manual/manual/python_scripting/index.html

**Contents:**
- Python Scripting

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Quit Game

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/game/quit_game.html

**Contents:**
- Quit Game
- Inputs

Exits the current runtime. In standalone mode it closes the runtime window entirely.

The condition for this node to activate.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Random Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/random_value.html

**Contents:**
- Random Value
- Parameters
- Inputs
- Outputs

Selected data type for random value.

Resulting random value from Min-Max range.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Ranged Treshold

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/ranged_treshold.html

**Contents:**
- Ranged Treshold
- Parameters
- Inputs
- Outputs

Selected mode for operation.

Minimum value to compare against.

Maximum value to compare against.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Raycasts

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/raycasts/index.html

**Contents:**
- Raycasts

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Raycast

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/raycasts/raycast.html

**Contents:**
- Raycast
- Parameters
- Inputs
- Outputs

Which condition will be used for node to activate.

Vector3 values for . todo

Vector3 values for aim to . todo

Which property to use.

Which material to use.

todo. Only visible if Custom Distance is checked.

Mask layers to use. todo

The direction of ray to cast.

todo. Only visible if Face Data input is checked.

UV coordinates of todo. Only visible if Face Data is checked.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Rebuild Data

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/network/rebuild_data.html

**Contents:**
- Rebuild Data
- Parameters
- Inputs
- Outputs

Resulting data . todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Receive Event

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/events/custom/receive_event.html

**Contents:**
- Receive Event
- Inputs
- Outputs

Reacts to events sent via the Send Event node or the Uplogic module. An event can store some data, which can be extracted using this node.

True if an event has been found, else False.

Content of this event, can be anything.

Messenger of this event, expected to be a KX_GameObject.

If multiple events have the same ID (subject), older events are overwritten.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Remove Constraint

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/remove_constraint.html

**Contents:**
- Remove Constraint
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which object to use todo.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Remove Dictionary Key

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/dict/remove_dictionary_key.html

**Contents:**
- Remove Dictionary Key
- Inputs
- Outputs

If connected, condition must be fullfiled for node to activate.

Which dictionary to use.

Which key will be removed from above dictionary.

True if node performs successfully, else False.

Resulting dictionary after removal.

Value that was removed. todo

Socket in diamond shape indicates dictionary.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Remove Filter

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/post_fx/remove_filter.html

**Contents:**
- Remove Filter
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Remove Index

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/list/remove_index.html

**Contents:**
- Remove Index
- Inputs
- Outputs

Remove the value at a given index on a list.

Condition to be fulfilled for node to be activated.

Which index to remove from above list.

True if removal of index is successful, else False.

Resulting list after removal.

The list index start at 0, so for example, in the list [4, 2, 5, 8, 9], the value at index 2 will be 5.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Remove Object

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/remove_object.html

**Contents:**
- Remove Object
- Inputs
- Outputs

Which condition is used for node to activate.

Which object to remove.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Remove Overlay Collection

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/collections/remove_overlay_collection.html

**Contents:**
- Remove Overlay Collection
- Inputs
- Outputs

The condition for this node to activate.

Which collection to remove overlay from.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Remove Parent

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/remove_parent.html

**Contents:**
- Remove Parent
- Inputs
- Outputs

Which condition is used for node to activate.

Object which will get its parent removed.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Remove Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/list/remove_value.html

**Contents:**
- Remove Value
- Inputs
- Outputs

Remove the first iteration of a given value in a list.

Condition to be fulfilled for node to activate.

List to remove the value from.

Which type and value to remove from list.

True if value is removed, else False.

Resulting list after value removal.

This node will only remove the first iteration in the list, for example if you give the list [1, 4, 104, 1] and the value integer 1, the output list will be [4, 104, 1] and not [4, 104] like we can think at first.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Remove Variable

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/variables/remove_variable.html

**Contents:**
- Remove Variable
- Inputs
- Outputs

Remove a previously saved variable.

If connected, condition must be fulfilled for node to activate.

Path to the directory containing the requested file.

Name of the file itself, ending can be omitted.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Render

**URL:** https://upbge.org/docs/latest/manual/manual/editors/properties/render.html

**Contents:**
- Render
- Embedded Player
- Standalone Player
- Stereo
- Shading
- System
- Animations
- Display
- Debug
- Bake

The Render tab in Properties Editor exposes options related to game screen rendering.

Some of the options showed here may behave differently according to the conditions, as there are two separate game “players” for previewing the game during development. Note that while UPBGE is running in either player, the computer’s mouse and keyboard are captured by the game and by default, the mouse cursor is not visible (this can be changed in the Display panel of this tab). To exit the game, press the Esc key.

Make sure that the render engine is set to EEVEE when attempting to set these controls, otherwise this description will not apply to what you see!

In Render tab, there are several panels available, as shown. Each one can be expanded or contracted using the usual triangle button. The features in each panel will be described in details below.

Embedded Player panel

This panel provides information for the Embedded Player which allows games to be run inside the Blender 3D Viewport. Embedded Player renders onto the 3D Viewport editor in the Blender GUI using the current perspective and zoom level of the 3D Viewport.

Note that the Resolution settings are independent of the size of the viewport preview pane. In fact, the Resolution controls seem to have no effect at all. The resolution and aspect ratio of the embedded preview are always fixed to the 3D Viewport editor, which behaves much like the Extend framing mode for the Standalone Player.

Starts UPBGE inside the current Blender 3D View. Shortcut P with mouse-over 3D Viewport.

Sets the internal X/Y rendering resolution.

Standalone Player panel

This panel provides information for the Standalone Player which allows games to be run without Blender. See Standalone Player for further details.

The Standalone Player renders the scene from the perspective of the active scene camera and either creates a new desktop window or switches into fullscreen rendering mode.

The semantics of the Standalone Player’s Resolution controls differ for Windowed and Fullscreen modes. In Windowed mode (Fullscreen checkbox unchecked), the Resolution controls set the initial dimensions of the desktop window. The user may resize the window at any time, causing the rendering resolution to change accordingly. In Fullscreen mode (Fullscreen checkbox checked), the Resolution controls set the internal rendering resolution. The actual display resolution will be a best fit depending on the user’s hardware. In either mode, the aspect ratio/cropping/scaling are determined by the Framing selection under the Display panel.

Regarding Fullscreen mode, it is important to remember that the Resolution settings in Fullscreen mode are only hints to the operating system. Each display and monitor combination will have a different set of resolutions that they are capable of displaying; so there can be little confidence that all end-users will actually get the resolution you suggest; unless you choose one of the most standard resolutions (e.g. 800x600 or 1024x768). If you insist on using higher resolutions, then you may want to state clearly in your documentation that only certain resolutions are supported. In most other cases, the user’s machine may select a resolution that is close to the one suggested; but the results can be unpredictable, especially in Letterbox framing mode.

Note that the Desktop checkbox has no effect in Windowed mode.

Launches the current blend file with the Standalone Player.

Sets the X (width) window size or fullscreen display resolution.

Sets the Y (height) window size or fullscreen display resolution.

Opens standalone game as a new window.

Opens standalone game in fullscreen.

Attempts to obey the Resolution specified above when in Fullscreen mode.

Keeps the current desktop resolution when in Fullscreen mode.

The number of AA samples to use for MSAA.

Number of bits used to represent color of each pixel in fullscreen display.

Number of frames per second of fullscreen display.

Toggle if use an stereo mode and, if use, select a stereo mode that will be used to capture stereo images of the game (and also, by implication, that stereo displays will use to render images in the Standalone Player).

Render single images with no stereo.

Render dual images for stereo viewing using appropriate equipment. See Stereo Camera for full details of available options.

Specifies each singe visual components that will be rendered in the game.

Toggles lights rendering.

Toggles GLSL shaders.

Toggles realtime shadows from lamps.

Toggles environment lighting from World tab.

Toggles material ramps.

Toggles material nodes.

Toggles extra textures, like normal or specular maps.

System panel in the Render tab

The System panel at the Render tab lets the game developer specify options about the system performance regarding to frame discard and restrictions about frame rendering, the key to stop UPBGE, etc.

Respect the frame rate rather than rendering as many frames as possible. When unchecked, this will inform Blender to run freely without frame rate restrictions. The frame rate is specified at the Display panel, also in the Render tab. For more information about frame rates, see Display panel.

Every time when the game developer uses a deprecated functionality (which in some cases are outdated or crippled OpenGL Graphic cards functions), the system will emit warnings about the deprecated function on the console.

Change Vsync settings.

Set how many samples use in anti-aliasing.

The precision of the screen display (between 8, 16 and 32 bits).

This button specifies which key-press will exit the game.

Animations panel in the Render tab

Specifies animations settings of game, like frame rate.

This number button/slider specify the maximum frame rate at which the game will run. Minimum is 1, maximum is 120.

Restrict number of animation updates to the animation FPS. This is better for performance, but can cause issues with smooth playback. When checked, this will force UPBGE to discard frames (even at the middle of redrawing, sometimes causing tearing artifacts) if the rate of frames rendered by the GPU is greater than the specified on Display panel.

Display panel at the Render tab

The Display panel in the Render tab lets the game developer specify whether the mouse cursor is shown during the game execution, and options to specify the framing style of the game to fit the window with the specified resolution.

Whether to show or not the mouse cursor when the game is running.

Selects how the scene is to be fitted onto the display window or screen. There are three types of framing available:

Maintains a 4:3 aspect ratio by scaling to fit the current window dimensions without cropping, covering any portions of the display that lie outside of the aspect ratio with color bars.

The behavior of this combination seems to be heavily dependent on the user’s hardware. The result can be quite unpredictable, especially when the resolution and aspect ratio differ too much from the machine’s capabilities. For this reason, Extend mode should be preferred for Fullscreen applications.

This mode behaves much like Letterbox mode, maintaining a 4:3 aspect ratio by scaling whenever possible; except that the camera frustum is expanded or contracted wherever necessary to fill any portions of the display that lie outside of the aspect ratio, instead of covering those portions of the scene with color bars, as with Letterbox mode, or distorting then scene, as with Scale mode.

In this mode, no attempt is made to maintain a particular aspect ratio. The scene and objects within will be stretched or squashed to fit the display exactly.

This will let the game developer choose the bar colors when using the Letterbox Framing mode.

Debug panel at the Render tab

The Debug panel at the Render tab toggles various specific debug helpers on UPBGE, from frame rate being showed on the screen to detailed physics visualization of specific elements, like armatures and camera frustum.

When checked, this will show values for each of the calculations Blender is doing while the game is running on the top left of the screen.

Shows render queries information while the game runs.

When checked, the values of any properties which are selected to be debugged in the objects are shown on the top left side of the screen.

Shows a visualization of physics bounds and interactions (like hulls and collision shapes), and their interaction.

The following remaining options are dropdown menus which allows the following options: - Disable: Disables the debug of the current option. - Allow: Allow debugging from individual settings of the current option. - Force: Allow debugging of the current option.

Shows bounding volume boxes of objects while the game is running.

Shows armatures while the game is running.

Shows camera limits visualization according to the current viewport dimensions while the game is running.

Shows lamp’s shadows bounds while the game is running.

The Bake panel in the Render tab is very similar to its Blender Render counterpart and serves much the same purpose. See Render Baking for further details.

Different Bake modes in the Render tab

Bake image textures of selected objects.

Shading information to bake into the image.

Bakes all materials, textures, and lighting except specularity and SSS.

Bakes ambient occlusion as specified in the World panels. Ignores all lights in the scene.

Bakes shadows and lighting.

Bakes tangent and camera-space normals (among many others) to an RGB image.

Bakes colors of materials and textures only, without shading.

Similar to baking normal maps, displacement maps can also be baked from a high-res object to an unwrapped low-res object, using the Selected to Active option.

Bakes Emit, or the Glow color of a material.

Bakes Alpha values, or transparency of a material.

Bake mirror intensity values.

Bake specular intensity values.

Bake specular colors.

Bake directly from a multi-resolution object.

Normalize to the distance.

Normalize without using material’s settings.

Normals can be baked in different spaces:

Normals in world coordinates, dependent on object transformation and deformation.

Normals in object coordinates, independent of object transformation, but dependent on deformation.

Normals in tangent space coordinates, independent of object transformation and deformation. This is the new default, and the right choice in most cases, since then the normal map can be used for animated objects too.

Bake to vertex colors instead of to a UV-mapped image.

If selected, clears the image to selected background color (default is black) before render.

Baked result is extended this many pixels beyond the border of each UV “island”, to soften seams in the texture.

Bake shading on the surface of selected objects to the active object.

Maximum distance in blender units from active object to other object.

Bias in blender units toward faces further away from the object.

The method used to split a quad into two triangles for baking.

Split quads predictably (0,1,2)(0,2,3).

Split quads predictably (1,2,3)(1,3,0).

Split quads to give the least distortion while baking.

Apply a custom scale to the derivative map instead of normalizing to the default (0.1).

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Render

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/index.html

**Contents:**
- Render

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Replace Mesh

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/object_data/replace_mesh.html

**Contents:**
- Replace Mesh
- Inputs
- Outputs

Which condition will be used for node to activate.

Target object for mesh replacement.

New mesh to use for replacing.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Resize Vector

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/vector/resize_vector.html

**Contents:**
- Resize Vector
- Parameters
- Inputs
- Outputs

Selected dimension for resizing.

Either fixed input XYZ values, or result from connected node.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Restart Game

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/game/restart_game.html

**Contents:**
- Restart Game
- Inputs
- Outputs

Reverts the state of the current runtime to it’s original version.

The condition for this node to activate.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Resume Sound

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/sound/resume_sound.html

**Contents:**
- Resume Sound
- Inputs
- Outputs
- Example

If connected, condition must be fulfilled for node to activate.

True if node performed successfully, else False.

See previous node (Pause Sound) for an example.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Rotate To

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/rotate_to.html

**Contents:**
- Rotate To
- Input
- Output

Rotates selected object to a specific angle, instantaneous or with speed. Applies rotation only on a single axis and fixed angulation in the world.

See also Apply Rotation.

Condition for this node to start.

Object that will be rotated.

Object’s rotation defined in degrees.

Speed to complete the move. Every time the node is activated, the displacement made will be smaller.

The axis of the object that will be used to rotate it during node execution.

Which axis is the front of the object.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Run Logic Tree

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/trees/run_logic_tree.html

**Contents:**
- Run Logic Tree
- Inputs
- Outputs

If connected, condition from attached node must be fulfilled for node to activate. If checked, always True, else False.

Which object to apply Logic Tree to.

Which Node Tree to run.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Run Python Code

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/python/run_python_code.html

**Contents:**
- Run Python Code
- Parameters
- Inputs
- Outputs

Selected Python mode. todo

Which condition will be used for node to activate.

Path/file with Python code to run.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Save Game

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/game/save_game.html

**Contents:**
- Save Game
- Parameters
- Inputs
- Outputs

Stores information about the state of the scene in a .json file.

Path to where the save files are stored.

The condition for this node to activate.

Index of this save file. If a save file already exists at this index, it will be overwritten.

True if the node performed successfully, else False.

No information is saved about which scene is loaded, so this node can only be used per scene.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Save Variable

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/variables/save_variable.html

**Contents:**
- Save Variable
- Inputs
- Outputs

Save a value into an external .json file.

Which condition will be used for node to activate.

Path to the directory containing the requested file.

Name of the file itself, ending can be omitted.

Which type and value to save.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Save Variable Dict

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/variables/save_variable_dict.html

**Contents:**
- Save Variable Dict
- Inputs
- Outputs

Save a dictionary as external json.

If connected, condition must be fulfilled for node to activate.

Path to the directory containing the requested file.

Name of the file itself, ending can be omitted.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Scene

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/index.html

**Contents:**
- Scene

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Scene

**URL:** https://upbge.org/docs/latest/manual/manual/editors/properties/scene.html

**Contents:**
- Scene
- Physics
- Obstacle Simulation
- Navigation Mesh
- Level of Detail
- Python Console
- Scene
- Units

The Scene tab in Properties Editor exposes options related to the current scene.

Scene tab’s Physics panel

The Physics panel located in the Scene tab determine the type of physical rules that govern the current UPBGE scene, the gravity value to be used and some other options.

Set the type of physics engine to use.

The default physics engine, in active development. It handles movement and collision detection. The things that collide transfer momentum to the collided object.

No physics in use. Things are not affected by gravity and can fly about in a virtual space. Objects in motion stay in that motion.

The physics constraints solver to use.

Sequential physics solver, default solver.

MLCP Dantzig physics solver.

MLCP Lemke physics solver.

The gravitational acceleration, m.s-2 (in units of meters per squared second), of this world. Each object that is an actor has a mass and size slider. In conjunction with the frame rate, Blender uses this info to calculate how fast the object should accelerate downward.

Sets the maximum number of physics steps per game frame if graphics slow down the game. Higher value allows physics to keep up with real-time.

Sets the number of simulation sub-steps per physics time step. Higher value give better physics precision.

Set the nominal number of game frames per second. Physics fixed timestep = 1/fps, independently of actual frame rate.

Time scale to slow down or speed up animations and physics in game.

Sets the maximum number of logic frame per game frame if graphics slows down the game, higher value allows better synchronization with physics.

These settings control the threshold at which physics is deactivated. These settings help reducing the processing spent on Physics simulation during the game.

The speed limit under which a rigid body will go to sleep (stop moving) if it stays below the limits for a time equal or longer than the deactivation time (sleeping is disabled when deactivation time is set to 0).

Same as linear threshold, but for rotation limit (in rad/s).

The amount of time in which the object must have motion below the thresholds for physics to be disabled (0.0 disables physics deactivation).

Use optimized Bullet DBVT tree for view frustum and occlusion culling (more efficient, but it can waste unnecessary CPU if the scene doesn’t have occluder objects).

The size of the occlusion culling buffer in pixel, use higher value for better precision (slower). The optimized Bullet DBVT for view frustum and occlusion culling is activated internally by default.

Enable object activity culling in this scene. The culling options can be set individually by object on Activity Culling panel on Object tab.

Scene tab’s Obstacle Simulation panel

Simulation used for obstacle avoidance in UPBGE, based on the RVO (Reciprocal Velocity Obstacles) principle. The aim is to prevent one or more actors colliding with obstacles.

Obstacle simulation is disabled, actors are not able to avoid obstacles.

Obstacle simulation is based on the RVO method with cell sampling.

Obstacle simulation is based on the RVO method with ray sampling.

Max difference in heights of obstacles to enable their interaction. Used to define minimum margin between obstacles by height, when they are treated as those which are situated one above the other i.e. they does not influence to each other.

Enable debug visualization for obstacle simulation.

Scene tab’s Navigation Mesh panel.

Rasterized cell size.

Rasterized cell height.

Minimum height where the agent can still walk.

Maximum height between grid cells the agent can climb.

Maximum walkable slope angle in degrees.

Minimum regions size. Smaller regions will be deleted.

Minimum regions size. Smaller regions will be merged.

Classic Recast partitioning method generating the nicest tessellation.

The fastest navmesh generation method, but may cause long thin polygons.

A reasonably fast method that produces better triangles than monotone partitioning.

Maximum contour edge length.

Maximum distance error from contour to cells.

Max number of vertices per polygon.

Detail mesh sample spacing.

Detail mesh simplification max sample error.

Scene tab’s Level of Detail panel

Use LoD hysteresis settings for the current scene.

Minimum distance change required to transition to the previous level of detail.

Scene tab’s Python Console panel

Enabling the panel’s checkbox allows to trigger an interactive Python console when the game is running through the specified shortcut.

Set the keys to be pressed in order to activate the Python console in game.

Scene tab’s Scene panel

Used to select which camera is used as the active camera. You can also set the active camera in the 3D View with Ctrl-0.

Allows you to use a scene as a background, this is typically useful when you want to focus on animating the foreground for example, without background elements getting in the way.

This scene can have its own animation, physics simulations, etc, but you will have to select it from the Scene data-block menu, if you want to edit any of its contents.

Sets can themselves have a background set (they’re recursively included). So you can always make additions to existing scenes by using them as a background to a newly created scene where your additions are made.

This can also be used in combination with Linking to a Scene, where one blend-file contains the environment, which can be reused in many places.

Active camera, used for rendering the scene.

Background set scene.

Scene tab’s Units panel

Common unit scales to use.

Standard unit of measurement for lengths.

Standard unit for angular measurement.

When you are using Degrees, the radian value is also displayed in the tooltip.

Scale factor to use when converting between Blender Units and Metric/Imperial.

Usually you will want to use the Length presets to change to scale factor, as this does not require looking up values to use for conversion.

When Metric or Imperial display units as multiple values, for example, “2.285m” will become “2m 28.5cm”.

The Audio panel settings in Scene tab don’t have effect in UPBGE. For audio settings, see Preferences.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Screen To World

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/camera/screen_to_world.html

**Contents:**
- Screen To World
- Inputs
- Outputs

Screen X (horizontal) position.

Screen Y (vertical) position.

Resulting world position.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Send Data

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/network/send_data.html

**Contents:**
- Send Data
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Send Event

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/events/custom/send_event.html

**Contents:**
- Send Event
- Properties
- Inputs
- Outputs

Creates an event that can be reacted to, using the Receive Event node or the Uplogic module. An event can store Content, and a Messenger can be assigned.

Enables access to the Content and Messenger sockets.

If True, the event is created.

Content of this event. Can be anything. Visible only if Advanced is selected.

Messenger attached to this event, expected to be KX_GameObject. Visible only if Advanced is selected.

True if the node performed successfully, else False.

Events are only created for the next frame. After that, they are erased. If multiple events have the same ID (subject), older events are overwritten.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Send Message

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/send_message.html

**Contents:**
- Send Message
- Inputs
- Outputs

Which condition is used for node to activate.

From which object to send message.

To which object to send a message.

Title text of a message.

Message text to send.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Sensors

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/index.html

**Contents:**
- Sensors
- Sensor Types

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Sensor Editing

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/sensors/editing.html

**Contents:**
- Sensor Editing
- Column Heading
- Sensors
- Object Heading

Sensor Column with a typical sensor

UPBGE sensors can be set up and edited in the left-hand column of the Logic Panel. This page describes the general column controls, and also those parameters which are common to all individual sensor types.

The image shows a typical sensor column with a single example sensor. At the top of this column, the column heading includes menus and buttons to control which of all the sensors in the current Game Logic are displayed.

Sensor Column heading

The column headings contain controls to set which sensors, and the level of detail given, in the sensor column. This is very useful for hiding unnecessary sensors so that the necessary ones are visible and easier to reach. Both these can be controlled individually.

Collapses all objects to just a bar with their name.

Collapses all sensors to bars with their names.

It is also possible to filter which sensors are viewed using the four heading buttons:

Shows all sensors for selected objects.

Shows only sensors belonging to the active object.

Shows sensors which have a link to a controller.

Only sensors connected to a controller with active states are shown.

Sensor Object Heading

In the column list, sensors are grouped by object. By default, sensors for every selected object appear in the list, but this may be modified by the column heading filters.

At the head of each displayed object sensor list, two entries appear:

The name of the object.

When clicked, a menu appears with the available sensor types. Selecting an entry adds a new sensor to the object. See Sensors for a list of available sensor types.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Sensor Positive

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/bricks/sensor_positive.html

**Contents:**
- Sensor Positive
- Inputs
- Outputs

Which object to inspect.

Which sensor to inspect.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Separate XYZ

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/vector/separate_xyz.html

**Contents:**
- Separate XYZ
- Inputs
- Outputs

Accepts Vector3 input, separates it into X, Y and Z float values.

Either fixed input values, or a result from connected node.

Resulting X float value.

Resulting Y float value.

Resulting Z float value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Separate XY

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/vector/separate_xy.html

**Contents:**
- Separate XY
- Inputs
- Outputs

Accepts Vector2 input, separates it into X and Y float values.

Either fixed input X and Y vector value, or a result from connected socket.

Resulting X float value.

Resulting Y float value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Serialize Data

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/network/serialize_data.html

**Contents:**
- Serialize Data
- Parameters
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Setting Up A Python Component

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_python_components/python_component.html

**Contents:**
- Setting Up A Python Component

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Actuator Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/bricks/set_actuator_value.html

**Contents:**
- Set Actuator Value
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which Object to set a value to.

Which Actuator to set.

Which Attribute to set.

Selected type and value to set.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Ambient Occlusion

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/eevee/set_ambient_occlusion.html

**Contents:**
- Set Ambient Occlusion
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

If checked, Ambient Occlusion will be used.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Animation Frame

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/set_animation_frame.html

**Contents:**
- Set Animation Frame
- Inputs
- Outputs

Condition which is required for node to activate.

Object for which to set animation frame.

Which animation action to use.

If checked (True), the animation will be freezed. todo

True if animation finished successfully.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Attribute

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/bone_constraints/set_attribute.html

**Contents:**
- Set Attribute
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which armature to use.

Name of the attribute to be set.

Type and value to set.

True if node performs successfully.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Attribute

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/index.html

**Contents:**
- Set Attribute

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Bloom

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/eevee/set_bloom.html

**Contents:**
- Set Bloom
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

If checked, Bloom will be used.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Bone Position

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/armature_rig/set_bone_position.html

**Contents:**
- Set Bone Position
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which armature to use.

String representation of bone to use.

Vector representation of position to set.

True if the node performed successfuly.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Camera

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/camera/set_camera.html

**Contents:**
- Set Camera
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Character Gravity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/set_character_gravity.html

**Contents:**
- Set Character Gravity
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Collection Visibility

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/collections/set_collection_visibility.html

**Contents:**
- Set Collection Visibility
- Inputs
- Outputs

The condition for this node to start.

If checked, collection is visible, else it is hidden.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Collision Group

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/set_collision_group.html

**Contents:**
- Set Collision Group
- Parameters
- Inputs
- Outputs

Selected mode for collision group node.

If connected, condition must be fulfilled for node to activate.

Which object to use todo.

16 layers available to set collision on. Hold Shift and LMB-drag over the layers to select multiple. todo

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Collision Mask

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/set_collision_mask.html

**Contents:**
- Set Collision Mask
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which object to use todo.

16 layers available to set collision on. Hold Shift and LMB-drag over the layers to select multiple. todo

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Color

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_color.html

**Contents:**
- Set Color
- Parameters
- Inputs
- Outputs

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Constraint Attribute

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/object_data/set_constraint_attribute.html

**Contents:**
- Set Constraint Attribute
- Inputs
- Outputs

Which condition will be used for node to activate.

Which object to set constraint on.

Which constraint to set.

Which attribute the constraing will be applied to.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Cursor Position

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/mouse/set_cursor_position.html

**Contents:**
- Set Cursor Position
- Inputs
- Outputs

Places the mouse cursor on corresponding coordinates between (0, 0) and (1, 1) on the game window from the top left corner.

Input condition needed for node to activate.

Horizontal cursor position between 0 and 1.

Vertical cursor position between 0 and 1.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Curve Points

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/curves/set_curve_points.html

**Contents:**
- Set Curve Points
- Inputs
- Outputs

Which condition will be used for node to activate.

Which curve to set points to.

A list of points to set.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Custom Cursor

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/set_custom_cursor.html

**Contents:**
- Set Custom Cursor
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Image to use as custom cursor.

Size of above image for cursor.

True if node performed successfully, else False.

Resulting cursor data. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Dictionary Key

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/dict/set_dictionary_key.html

**Contents:**
- Set Dictionary Key
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which dictionary will be used.

Which key will be set. todo

Which type and value to set.

True if node performs successfully, else False.

Resulting dictionary. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Dynamics

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/set_dynamics.html

**Contents:**
- Set Dynamics
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Exposure

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/eevee/set_exposure.html

**Contents:**
- Set Exposure
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Value of the Exposure to set.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Filter State

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/post_fx/set_filter_state.html

**Contents:**
- Set Filter State
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set FOV

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/camera/set_fov.html

**Contents:**
- Set FOV
- Inputs
- Outputs

Will set a Field of View to selected camera.

If connected, condition must be fulfilled for node to activate.

Which camera to set a FOV to.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Fullscreen

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/set_fullscreen.html

**Contents:**
- Set Fullscreen
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

If checked, Fullscreen will be set.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Gamma

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/eevee/set_gamma.html

**Contents:**
- Set Gamma
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Value of the Gamma to set.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Global Property

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/set_global_property.html

**Contents:**
- Set Global Property
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Name of property to set.

Selected type and value of property to set.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Influence

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/bone_constraints/set_influence.html

**Contents:**
- Set Influence
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which armature object to use.

Influence of the bone, ranged 0-1.

True if node performs successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Jump Force

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/character/set_jump_force.html

**Contents:**
- Set Jump Force
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which character object to use.

Force to apply to jump.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Light Color

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/lights/set_light_color.html

**Contents:**
- Set Light Color
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which color to assign to light.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Light Power

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/lights/set_light_power.html

**Contents:**
- Set Light Power
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

The strength of the light. Can be negative.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Light Shadow

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/lights/set_light_shadow.html

**Contents:**
- Set Light Shadow
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

If checked, light will produce shadows. Accepts Boolean result from connected node.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set List Index

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/list/set_list_index.html

**Contents:**
- Set List Index
- Inputs
- Outputs

Set a value for a given index on a list.

If connected, a condition must be fulfilled for note to activate.

Which type and value to set for above list.

True if node sets an index successfully, else False.

Resulting list after setting the index.

This node cannot be used to add a new value at the end of a list, it will result in an out of range error. Instead use the Append node to do this.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Local Angular Velocity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_local_angular_velocity.html

**Contents:**
- Set Local Angular Velocity
- Parameters
- Inputs
- Outputs

Local Angular Velocity todo

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Local Linear Velocity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_local_linear_velocity.html

**Contents:**
- Set Local Linear Velocity
- Parameters
- Inputs
- Outputs

Local Linear Velocity todo

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Local Orientation

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_local_orientation.html

**Contents:**
- Set Local Orientation
- Parameters
- Inputs
- Outputs

Local Orientation todo

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Local Position

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_local_position.html

**Contents:**
- Set Local Position
- Parameters
- Inputs
- Outputs

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Local Transform

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_local_transform.html

**Contents:**
- Set Local Transform
- Parameters
- Inputs
- Outputs

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Material

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_material.html

**Contents:**
- Set Material
- Inputs
- Outputs

Which condition is used for node to activate.

Which object will receive a material.

Which material slot to use for setting.

Which material to set.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Max Jumps

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/character/set_max_jumps.html

**Contents:**
- Set Max Jumps
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which character object to use.

Max allowed number of jumps while character is in the air. todo

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Node Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/materials/set_node_value.html

**Contents:**
- Set Node Value
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

String representation for node name.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Node Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/geometry/set_node_value.html

**Contents:**
- Set Node Value
- Inputs
- Outputs

Which condition will be used for node to activate.

Geometry node to use.

String representation of node name.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Node Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/groups/set_node_value.html

**Contents:**
- Set Node Value
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

String representation of node name.

The internal socket is for modifying attributes that aren’t stored directly on the node but in another container (i.e. ShaderNodeTexImage.image_user.offset > image_user would be the internal entry).

Type and value to set.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Object Attribute

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/python/set_object_attribute.html

**Contents:**
- Set Object Attribute
- Inputs
- Outputs

Which condition will be used for node to activate.

Which object instance to use. todo

Which attribute to set.

Type and value to set.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Object Property

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/set_object_property.html

**Contents:**
- Set Object Property
- Parameters
- Inputs
- Outputs

Selected property mode.

If connected, condition must be fulfilled for node to activate.

Name of the property, either fixed, or result from connected node.

Type of selected property to set.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Orthographic Scale

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/camera/set_orthographic_scale.html

**Contents:**
- Set Orthographic Scale
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which camera to set to.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Overlay Collection

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/collections/set_overlay_collection.html

**Contents:**
- Set Overlay Collection
- Inputs
- Outputs

The condition for this node to start.

Which camera is used for overlay display.

Which collection to set overlay to.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Parent

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_parent.html

**Contents:**
- Set Parent
- Inputs
- Outputs

Which condition is used for node to activate.

Child object for which to set a parent.

An object that will become a parent. Congratulations!

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Physics

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/set_physics.html

**Contents:**
- Set Physics
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Resolution

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/set_resolution.html

**Contents:**
- Set Resolution
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Resolution width to set.

Resolution height to set.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Rigid Body

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/set_rigid_body.html

**Contents:**
- Set Rigid Body
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Scene

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/set_scene.html

**Contents:**
- Set Scene
- Inputs
- Outputs

The condition for this node to activate.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Sensor Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/bricks/set_sensor_value.html

**Contents:**
- Set Sensor Value
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which object to set a value to.

Which attribute to set.

Selected type and value to set.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Socket

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/materials/set_socket.html

**Contents:**
- Set Socket
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which material node to set. todo

String representation of node name.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Socket

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/groups/set_socket.html

**Contents:**
- Set Socket
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Socket

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/nodes/geometry/set_socket.html

**Contents:**
- Set Socket
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Geometry node to use.

String representation of node name.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set SSR

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/eevee/set_ssr.html

**Contents:**
- Set SSR
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

If checked, SSR (Screen Space Reflection) will be used.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Target

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/bone_constraints/set_target.html

**Contents:**
- Set Target
- Inputs
- Outputs

Which condition will be used for node to activate.

Which armature to use.

Which object to use as target.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Timescale

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/set_timescale.html

**Contents:**
- Set Timescale
- Inputs
- Outputs

The condition for this node to activate.

Timescale value to set.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Tree Property

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/set_tree_property.html

**Contents:**
- Set Tree Property
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Name of the tree to use.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Vehicle Attribute

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/vehicle/set_vehicle_attribute.html

**Contents:**
- Set Vehicle Attribute
- Parameters
- Inputs
- Outputs

Selected vehicle wheels axis.

If connected, condition must be fulfilled for node to activate.

Object that will act as collider for vehicle. todo

Number of wheels for selected axis.

Vehicle suspension settings.

Vehicle suspension stiffness. todo

Vehicle suspension damping. todo

Vehicle wheels friction. todo

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Velocity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/character/set_velocity.html

**Contents:**
- Set Velocity
- Parameters
- Inputs
- Outputs

Use character’s local axis.

If connected, condition must be fulfilled for node to activate.

Which object to use as character.

Vector3 values to set. todo

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Visibility

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_visibility.html

**Contents:**
- Set Visibility
- Inputs
- Outputs

Which condition is used for node to activate.

Which object to set visibility to.

If checked, set Visible state, else set not Visible State.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Volumetric Light

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/eevee/set_volumetric_light.html

**Contents:**
- Set Volumetric Light
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

If checked, Volumetric Light will be used.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set VSync

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/set_vsync.html

**Contents:**
- Set VSync
- Parameters
- Inputs
- Outputs

Selected mode of VSync to set. todo

If connected, condition must be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set Widget Attribute

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/set_widget_attribute.html

**Contents:**
- Set Widget Attribute
- Parameters
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which widget to set attribute to.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set World Angular Velocity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_world_angular_velocity.html

**Contents:**
- Set World Angular Velocity
- Parameters
- Inputs
- Outputs

World Angular Velocity todo

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set World Gravity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/set_world_gravity.html

**Contents:**
- Set World Gravity
- Inputs
- Outputs

The condition for this node to activate.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set World Linear Velocity

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_world_linear_velocity.html

**Contents:**
- Set World Linear Velocity
- Parameters
- Inputs
- Outputs

World Linear Velocity todo

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set World Orientation

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_world_orientation.html

**Contents:**
- Set World Orientation
- Parameters
- Inputs
- Outputs

World Orientation todo

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set World Position

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_world_position.html

**Contents:**
- Set World Position
- Parameters
- Inputs
- Outputs

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set World Scale

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_world_scale.html

**Contents:**
- Set World Scale
- Parameters
- Inputs
- Outputs

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Set World Transform

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/set_attribute/set_world_transform.html

**Contents:**
- Set World Transform
- Parameters
- Inputs
- Outputs

Condition to be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Show Framerate

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/show_framerate.html

**Contents:**
- Show Framerate
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

If checked/enabled, Framerate will be shown.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Show Profile

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/render/show_profile.html

**Contents:**
- Show Profile
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

If checked/enabled, Framerate will be shown.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Slow Follow

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/slow_follow.html

**Contents:**
- Slow Follow
- Parameters
- Input
- Output

todo - check description Rotates a selected object to a specific angle instantly. Applies rotation only on a single axis and fixed angulation in the world.

See also Apply Rotation.

Condition for this node to start.

Object that will be rotated.

Target object to follow.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Sound

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/sound/index.html

**Contents:**
- Sound

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Spawn Pool

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/spawn_pool.html

**Contents:**
- Spawn Pool
- Parameters
- Inputs
- Outputs

If selected, pool will be spawn on game start.

Selected behavior of spawn pool.

Object instance which will be spawn.

Quantinty of spawned instances.

Life length of spawned instances. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Standalone Player

**URL:** https://upbge.org/docs/latest/manual/manual/deployment/blender_player.html

**Contents:**
- Standalone Player
- Personalize The Game Icon

The standalone player allows a Blender game to be run without having to load the Blender system. This allows games to be distributed to other users, without requiring them a detailed knowledge of Blender (and also without the possibility of unauthorized modification). Note that the Game Engine Save as Runtime is an add-on facility which must be pre-loaded before use.

The following procedure will give a standalone version of a working game.

Edit > Preferences > Add-ons > Game Engine > Save As Game Engine Runtime enable the checkbox. (You can also Save User Settings, in which case the add-on will always be present whenever Blender is re-loaded).

File ‣ Export ‣ Save As Game Engine Runtime (give appropriate directory/filename) confirm with Save as Game Engine Runtime.

The game can then be executed by running the appropriate .exe file. Note that all appropriate libraries are automatically loaded by the add-on.

If you are interested in licensing your game, read Licensing for a discussion of the issues involved.

Exporting… If the game is to be exported to other computers, make a new empty directory for the game runtime and all its ancillary libraries, etc. Then make sure the whole directory is transferred to the target computer.

This is option is available for Windows only. You can personalize the icon using the option shown in the figure below.

Personalize game icon

Here is a small video tutorial showing all the process, from .ico creation to its use in an example game:

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Start Event

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/sound/fmod/start_event.html

**Contents:**
- Start Event
- Parameters
- Inputs
- Outputs

Start an event by name.

If active, an object reference will be used for the position and orientation of this sound.

If connected, condition must be fulfilled for node to activate.

Name of the event. Event names are defined within the FMod application.

World position of this event.

Reference object for position and orientation.

Channel for grouping events together.

True if node performed successfully, else False.

The Event or EventSpeaker python object.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Start Logic Tree

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/trees/start_logic_tree.html

**Contents:**
- Start Logic Tree
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which Node Tree to apply to the object.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Start Sound

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/sound/start_sound.html

**Contents:**
- Start Sound
- Parameters
- Inputs
- Outputs
  - Example

2D or 3D sound or sample; sample has additional 2 more inputs.

If selected, additional inputs are activated.

If selected, Position is changed to Object field; enter object name or pick from list.

If connected, condition must be fulfilled for node to activate.

Vector position of the sound source.

Which file to play. Pick sound file from dropdown list, or load it with folder icon.

How many times to play the sound.

Set pitch of the sound.

If checked, timescale will be ignored.

Attenuation value of the sound. Only visible if Show Advanced Options is selected.

todo. Only visible if Show Advanced Options is selected.

Size of inner and outer sound cone. Only visible if Show Advanced Options is selected.

Volume of outer cone. Only visible if Show Advanced Options is selected.

Start signal is emitted.

End signal is emitted.

Resulting sound output.

Above example will play selected Sound File, when mouse cursor enters the selected Object - a non-default Cube in this example.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Start Speaker

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/sound/start_speaker.html

**Contents:**
- Start Speaker
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Speaker Object to use.

Selected Speaker play times.

Start signal is emitted.

End signal is emitted.

Resulting sound output.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## States

**URL:** https://upbge.org/docs/latest/manual/manual/logic_bricks/states.html

**Contents:**
- States
- How States Operate
- Editing States
- Visible States
- Initial State

In the BGE, an object can have different “states”. At any time while the game is playing, the current state of the object defines its behavior. For instance, a character in your game may have states representing awake, sleeping or dead. At any moment their behavior in response to a loud bang will be dependent on their current state; they may crouch down (awake); wake up (asleep) or do nothing (dead).

States are set up and used through controllers: note that only controllers, not actuators and sensors, are directly controlled by the state system. Each object has a number of states (up to 30; default = 1), and can only be in one state at any particular time. A controller must always specify the state for which it will operate – it will only give an output pulse if a) its logic conditions are met, and b) the object is currently in the specified State. States are set up and edited in the object’s Controller settings (for details see below).

State settings are automatic in simple games. By default, the number of states for each object is 1, and all controllers are set to use State 1. So, if a game does not need multiple states, everything will work without explicitly setting states – you do not need to bother about states at all.

One of the actuators, the State actuator, can set or unset the object’s State bits, and so allow the object’s reaction to a sensor signal to depend on its current state. So, in the above example, the actor will have a number of controllers connected to the “loud bang” sensor, for each of the “awake”, “asleep” or “dead” states. These will operate different actuators depending on the current state of the actor, and some of these actuators may switch the actor’s state under appropriate conditions.

States are set up and edited using the Controller (center) column of the Game Logic Panel. To see the State panel, click on the State Panel Button shown. The panel shows two areas for each of the 30 available states; these show Visible states, and Initial states (see below). Setting up the State system for a game is performed by choosing the appropriate state for each controller in the object’s logic.

The display of an object’s state logic, and other housekeeping, is carried out using the State Panel for the object, which is switched on and off using the button shown. The panel is divided into two halves, Visible and Initial.

In the Visible area, each of the 30 available states is represented by a light-gray square. This panel shows what logic is visible for the logic brick displayed for the object. At the right is the All button; if clicked, then all the object’s logic bricks are displayed (this is a toggle), and all State Panel squares are light gray. Otherwise, individual states can be clicked to make their logic visible. (Note that you can click more than one square). Clicking the square again deselects the state.

States for the object that are in use (i.e. the object has controllers which operate in that state) have dots in them, and squares are dark gray if these controllers are shown in the Game Logic display. The display of their connected sensors and actuators can also be controlled if the State buttons at the head of their columns are ticked.

In the Initial area, each of the 30 available states is again represented by a light-gray square. One of these states may be clicked as the state in which the object starts when the game is run.

At the right is the button; if clicked, and the Render properties > Game Debug panel > Debug Properties checkbox is clicked, the current state of the object is shown in the top left-hand corner of the display while the game is running.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Steer

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/vehicle/steer.html

**Contents:**
- Steer
- Parameters
- Inputs
- Outputs

Selected vehicle wheels axis.

If connected, condition must be fulfilled for node to activate.

Which object to use for steering.

Number of wheels for selected axis.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Stop All Sounds

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/sound/stop_all_sounds.html

**Contents:**
- Stop All Sounds
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Stop Animation

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/animation/stop_animation.html

**Contents:**
- Stop Animation
- Inputs
- Outputs

If connected, certain condition is required for node to activate.

Which object will be used stop animating.

True if animation is stopped successfully.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Stop Logic Tree

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/trees/stop_logic_tree.html

**Contents:**
- Stop Logic Tree
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which Node Tree to apply to stop.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Stop Sound

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/sound/stop_sound.html

**Contents:**
- Stop Sound
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Store Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/store_value.html

**Contents:**
- Store Value
- Parameters
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Data type of value to be stored.

Resulting stored value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## String

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/string.html

**Contents:**
- String
- Parameters
- Inputs
- Outputs

Selected data type - string data type.

Fixed input string value, or a result from connected node.

Output string result.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Templates

**URL:** https://upbge.org/docs/latest/manual/manual/contribute/templates.html

**Contents:**
- Templates
- Operator Menus
- Panels
- Properties
- Nodes
- Directory Layout
  - Table of Contents

The following guide provides patterns for interface elements and directories.

Each operator should receive its own heading or page based on the length of the content. At the start should be a reference admonition documenting the context of the operator:

Panels should be documented by their own heading, nested panels should use decreasing heading levels. Each panel could have its own page based on the length of documentation and/or the amount of panels. Expanded menus that toggle what properties are presented to the user should be treated like subpanels:

Properties should be documented using definition lists. Properties that are hidden based on other properties should used nested definitions:

Select menus should be documented using the following syntax:

Nodes have three headings: properties, inputs, and outputs. Only include any of them if it is present on node. At the end of the page can be an optional example(s) section:

Sections should be generally structured as follows:

index.rst (contains links to internal files)

The idea is to enclose all the content of a section inside of a folder. Ideally every section should have an index.rst, containing the TOC for that section, and an introduction.rst to the contents of the section.

By default, a table of contents should show one level of depth:

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (php):
```php
.. admonition:: Reference
   :class: refbox

   :Mode:      Edit Mode
   :Menu:      :menuselection:`Curve --> Snap`
   :Shortcut:  :kbd:`Shift-S`
```

Example 2 (php):
```php
.. admonition:: Reference
   :class: refbox

   :Mode:      Edit Mode
   :Menu:      :menuselection:`Curve --> Snap`
   :Shortcut:  :kbd:`Shift-S`
```

Example 3 (yaml):
```yaml
Panel Title
===========

Nested Panel Title
------------------
```

Example 4 (yaml):
```yaml
Panel Title
===========

Nested Panel Title
------------------
```

---

## Texture

**URL:** https://upbge.org/docs/latest/manual/manual/editors/properties/texture.html

**Contents:**
- Texture

The Texture tab in Properties editor exposes textures and its attributes.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Text Editor

**URL:** https://upbge.org/docs/latest/manual/manual/editors/text/index.html

**Contents:**
- Text Editor
- Header
  - View Menu
  - Text Menu
  - Edit Menu
  - Select Menu
  - Format Menu
  - Template Menu
    - Main View
    - Sidebar

UPBGE has a Text Editor among its editor types, accessible via the Editor type menu, or the shortcut Shift-F11.

Text Editor for Python/GLSL edition

The newly opened Text editor is empty, with a very simple header. More options become available when a text file is created or opened.

Text header with a text loaded

The standard editor selection button.

Resolves modified file conflicts when an external text file is updated from another program.

Opens the file from drive again, overriding any local changes.

Converts the external text data-block into an internal one.

Hides the warning message until the external text file is modified externally again.

A data-block menu to select a text or to create a new one. After that the header will change.

Executes the text as a Python script Alt-P. This execution has placed out of Game Engine only, and it is focused for development mainly. If you want to execute a Python script inside the Game Engine check the Python Scripting chapter.

Toggle display options.

Line Numbers, Word Wrap, Syntax Highlighting

Show or hide the sidebar.

Displays the text file’s line numbers on the left of the Main View.

Wraps words that are too long to fit into the horizontal space by pushing them to a new “pseudo line”.

Colors special words, in the Main View, that are used in the Python or GLSL programming language.

Emphasizes the active line by altering the color of the background.

Moves the view and cursor to the start of the text file.

Moves the view and cursor to the end of the text file.

Moves the cursor to the start of the current line.

Moves the cursor to the end of the current line.

Moves the cursor to the same position in the line above the current line.

Moves the cursor to the same position in the line below the current line.

Moves the cursor to the beginning of the previous word. If the cursor is in the middle of a word, the cursor is moved to the beginning of the current word.

Moves the cursor to the end of the next word. If the cursor is in the middle of a word, the cursor is moved to the end of the current word.

Creates a new text Data Block.

Loads an external text file that is selected via the File Browser.

Reopens (reloads) the current buffer (all non-saved modifications are lost).

Saves an already open file.

Saves text as a new text file, a File Browser is opened to select the directory to save the file along with giving the file a name/file extension.

Registers the current text data-block as a module on loading (the text name must end with .py).

Executes the text as a Python script, see Running Scripts for more information.

Cuts out the marked text into the text clipboard.

Copies the marked text into the text clipboard.

Pastes the text from the clipboard at the cursor location in the Text editor.

Duplicates the current line.

Swaps the current/selected line(s) with the above.

Swaps the current/selected line(s) with the below.

Shows the Find & Replace panel in the Sidebar.

Finds the next instance of the selected text.

Shows a pop-up, which lets you select a line number where to move the cursor to.

Shows a selectable list of words already used in the text.

Converts the text file to a Text Object either as One Object or One Object Per Line.

Selects the entire text file.

Selects the entire current line.

Selects the entire current word.

Selects everything above the cursor.

Selects everything below the cursor.

Selects everything between the beginning of the current line and the cursor.

Selects everything between the cursor and the end of the current line.

Selects everything between the cursor and the position of the cursor one line above.

Selects everything between the cursor and the position of the cursor one line below.

Selects everything between the cursor and the beginning of the previous word. If the cursor is in the middle of a word, select everything to the beginning of the current word.

Selects everything between the cursor and the end of the next word. If the cursor is in the middle of a word, select everything to the end of the current word.

Inserts a tab character at the cursor.

Unindents the selection.

Toggles whether the selected line(s) are a Python comment. If no lines are selected the current line is toggled.

Converts indentation characters To Spaces or To Tabs.

Text Editor has some dedicated templates for Python scripts, Python Components and GLSL shaders, which are useful for writing tools, like a class/function/variable browser, completion…

Typing on the keyboard produces text in the text buffer.

As usual, pressing, dragging and releasing LMB selects text. Pressing RMB opens the context menu.

Text editor is handy also when you want to share your blend-files with others. I.e write a README text explaining the contents of your blend-file. Be sure to keep it visible when saving!

Searches for instances of a text that occur after the cursor. Using the eyedropper icon will search for the currently selected text and sets the selection to the match. Find Next searches for the next instance of the text.

Searches for the text specified in Find Text and replaces it with the new text. Using the eyedropper icon will set the currently selected text as the replace text. Replace searches for the next match and replaces it. Replace All searches for the match and replaces all occurrences of the match with the new text.

Search is sensitive to upper-case and lower-case letters.

Search again from the start of the file when reaching the end.

Search in all text data-blocks instead of only the active one.

Shows a right margin to help keep line length at a reasonable length when scripting. The width of the margin is specified in Margin Column.

The size of the font used to display text.

The number of character spaces to display tab characters with.

Use Tabs or Spaces for indentations.

The Text editor footer displays if the text is saved internal or external and if there are unsaved changes to an external file. For external files, this region also displays the file path to the text file.

The most notable keystroke is Alt-P which makes the content of the buffer being parsed by the internal Python interpreter built into UPBGE. Before going on it is worth noticing that UPBGE comes with a fully functional Python interpreter built-in, and with a lots of Blender/UPBGE-specific modules.

This script execution takes place outside Game Engine, and it is intended for development purpose only. If you want to execute a Python script inside the Game Engine check the Python Scripting chapter.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Timer

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/time/timer.html

**Contents:**
- Timer
- Inputs
- Outputs

Wait a certain time between the reception of True and the output of True.

Condition required for timer to be set.

Seconds needed to pass until timer activates.

Condition/node to execute when timer has elapsed.

Timer node is tied to the CPU clock, not to game FPS.

Timer will only handle one input at a time and will not stack them, unlike the Delay node. For example, if you connect a Keyboard key node to a Timer set to 5 seconds and press the key a first time and then 2 seconds later you press the key again, Timer will only output True 5 seconds after the first key press and not another one time True at 7 seconds, unlike Delay.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Time

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/time/index.html

**Contents:**
- Time

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Time Data

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/time/time_data.html

**Contents:**
- Time Data
- Outputs

Return useful data about the time within your game.

The number of seconds elapsed since the game engine was launched (Float).

The value returned here is independent of a scene change (time will continue to be counted without resetting the count), but it will be reset after loading a .blend file because it relaunches the game engine.

The number of seconds elapsed between the last two frames (Float). Used for calculations requiring absolute temporal precision, such as progressive transitions, interpolations or mechanics requiring fine temporal management. For example, if you want to animate an object that has to move exactly 10 units over 5 seconds.

Frames Per Second of the running game (Float).

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Toggle Filter

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/post_fx/toggle_filter.html

**Contents:**
- Toggle Filter
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

True if the node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Toggle Object Property

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/properties/toggle_object_property.html

**Contents:**
- Toggle Object Property
- Parameters
- Inputs
- Outputs

If connected, condition must be fulfilled for node to activate.

Which property to toggle.

True if node performed successfully, else False.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Tools

**URL:** https://upbge.org/docs/latest/manual/manual/tools/index.html

**Contents:**
- Tools

For a small project, editing Python scripts using Blender’s source editor could be the most straightforward option to develop a UPBGE game. However, you may find an external, more dedicated development setup to be more desirable as your project grows in size and complexity.

This section introduces several Python-related tools you can use in conjunction with your project and explains how to prepare them for UPBGE development.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Top Down Templates

**URL:** https://upbge.org/docs/latest/manual/manual/python_components/getting_started/top_down_templates.html

**Contents:**
- Top Down Templates
- Mouse Camera Drag Component
- Mouse Point And Click Component
- Object Chaser Component

This template was created to help UPBGE users to create games or any kind of interactive thing that request a Top Down Controller. Easy to use, easy to attach to your project.

To use, just select it from template label at script editor and you’re done! You can use this template in your projects, even for commercial projects. You only need to give credits to Guilherme Teres Nunes (UnidayStudio) for this. It’s very easy to use: Just load this script into your .blend file through template label (or paste it in the same folder that your .blend is), select the object that you want, and attach the script into the object’s components using Register Component button.

This component will allow the player to move the camera (or other objects) by simple holding a mouse button (you decide what button) and dragging the mouse around. Very useful for top down games. It will also allow the player to move the camera (or other objects) by pressing W, A, S, D keys. There is some configuration to help you adapting this logic to better fit in your project. If you want to drag the camera in a vertial way, to create a side scroller game, for example, you can easly change the “Up Axis” to allow this.

Mouse Camera Drag component

You can attach this component into your camera or into other objects. It’s very simple to configure:

Show Mouse: Enable if you want to show the mouse

Mouse Movement: Enable if you want to activate the mouse drag logic

Mouse Button: Which mouse button you want to use

Keyboard Movement: Enable if you want to move the object using W, A, S, D

Up Axis: Select the UP axis.

Local Movement: Local or Global movement? You decide!

Mouse Sensibility: The mouse sensibility!

Keyboard Speed: If you enabled the Keyboard Movement, control the speed here!

Limit Area: You can limit the area that the object can stay by playing around with this values. If you don’t want, just set to 0.

This component will allow you to teleport an object right into the point that the player clicks. You can limit the scope of the clicks by adding a property.

Mouse Point and Click component

This feature is very useful for top down/point and click games, because you need a pivot to point where the player wants the character to go. It’s very simple to configure:

Activate: Activate or deactivate the logic

Mouse Button: Which mouse button you want to use

Align To Normal: Enable if you want to align the object to the mouse over normal.

Property: The property that you want to interact with (leave this blank if you want to interact with everything).

This component will make the object chase a target (another object) when they have certain distance. Note that is necessary to have a navmesh in your scene. You can also change the Target object in realtime by calling the function setTarget(). It’s very simple to configure:

Object Chaser component

Activate: Activate or deactivate the logic.

Navmesh Name: The name of your navmesh.

Target Object: The name of your target.

Min Distance: The minimum distance that you want the object from the target.

Tolerance Distance: Once the object is already near the target, the extra tolerance distance that they can have before it starts chasing again.

Speed: The speed of the object while chasing the target.

Front Axis: The front Axis (put Y axis if you don’t know).

Up Axis: The UP Axis (put Z if you don’t know).

Smooth Turn: To smooth the path following turns.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Transformation

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/objects/transformation/index.html

**Contents:**
- Transformation

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Trees

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/logic/trees/index.html

**Contents:**
- Trees

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Treshold

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/treshold.html

**Contents:**
- Treshold
- Parameters
- Inputs
- Outputs

Selected treshold operation.

Value to compare against.

Resulting value of treshold operation.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Tutorials

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/index.html

**Contents:**
- Tutorials

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Tween Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/tween_value.html

**Contents:**
- Tween Value
- Parameters
- Inputs
- Outputs

Move a value along a given curve over a set duration. This node can be used to map a linear value of 0-1 to a curve.

LMB-select a point, below the graph is a row with point settings - click X to delete.

LMB-drag the point to desired location on graph.

In a row below the graph, click-select icon to change handle type, or change its position values (X Y coordinates).

Above the graph are option icons - zoom in/out, use Clipping (will clamp output values between 0 and 1), use dropdown menu to Reset View, Reset Curve etc.

A value type to process.

Automatically move right on the curve if the “Result” socket is being accessed.

Move right on the curve.

Move left on the curve.

Starting tween value.

Duration of Tweening in seconds.

True if node performed successfully, else False.

True if the factor is either 0 or 1, else False.

Resulting tween value.

Current X-Axis position.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Typecast Value

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/python/typecast_value.html

**Contents:**
- Typecast Value
- Parameters
- Inputs
- Outputs

Typecast Python value to which type.

Type and value to cast.

Resulting output value of selected type.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## UI

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/index.html

**Contents:**
- UI

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## UPBGE Manual

**URL:** https://upbge.org/docs/latest/manual/

**Contents:**
- UPBGE Manual

Welcome to UPBGE’s documentation! Here you will find definitions of the available tools and features in UPBGE, step-by-step tutorials to certain tasks and a lot of examples for game logic programming with detailed information.

Visit the UPBGE’s website or contribute to this manual. Contribution guidelines are in the Contribute chapter.

Also, if you want to read the whole manual offline you can download it from this link.

Keyboard navigation is supported - use arrow keys left/right for previous/next page, and up/down to scroll the page up/down. Press Alt-left/right to go back/forward by browser history. To focus the Search field, press / (slash) key, Enter to search, Tab to unfocus.

See About the UPBGE Manual for a cheatsheet of most common abbreviations used in this manual.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## UPBGE Manual

**URL:** https://upbge.org/docs/latest/manual/index.html

**Contents:**
- UPBGE Manual

Welcome to UPBGE’s documentation! Here you will find definitions of the available tools and features in UPBGE, step-by-step tutorials to certain tasks and a lot of examples for game logic programming with detailed information.

Visit the UPBGE’s website or contribute to this manual. Contribution guidelines are in the Contribute chapter.

Also, if you want to read the whole manual offline you can download it from this link.

Keyboard navigation is supported - use arrow keys left/right for previous/next page, and up/down to scroll the page up/down. Press Alt-left/right to go back/forward by browser history. To focus the Search field, press / (slash) key, Enter to search, Tab to unfocus.

See About the UPBGE Manual for a cheatsheet of most common abbreviations used in this manual.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Using Linked Libraries In Game

**URL:** https://upbge.org/docs/latest/manual/manual/tutorials/introducing_logic_bricks/linked_libraries.html

**Contents:**
- Using Linked Libraries In Game
- Before We Start
- Linking Collections
- Managing the Links
  - Relocating the references

Linked Library is a Blender feature that allows referencing a datablock from another blend file into the current one, allowing easier manipulation of common assets and better project management, as you only need to edit the original file to update all the references. UPBGE supports this Blender feature, specially group instances, which ones are fairly well integrated through Python. This tutorial aims to show how to use linked libraries, group instances and manage the links.

To proceed with this tutorial, we need some base files first. On a directory, save three empty blend files: game.blend (which will contain the references from the libraries), lib_character.blend (which will contain the actual model of our character) and lib_scenery.blend (which will contain the actual model of our ground). We’ll edit the file game.blend later, first we must create the contents of our libraries.

Add a Monkey object, add it to a collection (M) and rename the collection to player.

Add a Plane, scale it up by 5 (select plane > S > 5 > Enter > size of 10x10), and add it to a collection named ground.

Both files should be set up somewhat like this:

Split view of the two files

Now, we’ll create a blend file named game.blend on the same directory as our previous files. In this file, we’ll do the following procedures:

Select either lib_character.blend or lib_scenery.blend file.

Select the Collection folder.

Select corresponding collection and double click it/click Link.

Repeat linking the other collection.

If everything went right, you should see in the 3D Viewport the collection instances added. They are not editable as they are only Empty objects referencing collections from the original files. The Outliner shows chain icons, signifying those collections are linked.

Collections instanced in game.blend scene

With the instances added, all you have to do is place them with the desired transformations, and if you need to edit all the placed instances, just edit the original file to update all the references. Pretty handy, isn’t it?

If you rename or move any of your libraries to another folder, you will face a common problem: broken links. There are several ways to deal with this problem, and this section will present you the use of the Outliner to manage links.

I have renamed the library files to LibCharacter and LibScenery, which are different names from the previous ones (with underlines and only lower case characters). When opening game.blend, the editor will complain about the non-existing libraries, and our instances will be shown only as Empty objects.

Opening game.blend after libraries be renamed

To fix this, we must go to the Outliner and select the Blender File mode. On this mode we’ll see all Data-blocks in our .blend file.

Blender File mode in Outliner

The important elements here are the references to our libraries at the bottom: they are being shown as cracked icons and their previous names. To fix this issue:

Right click the references, select Relocate and select the corresponding file.

Broken references fix modes in Outliner

After fixing the broken references, their icons will change back to normal and the objects will be automatically updated in the 3D Viewport.

Understanding how to use and manage linked libraries is important to maintain a complex and healthy project environment. Much more can be achieved through the use of bge.logic.LibLoad, loading and unloading libraries dynamically using Python, but for simpler projects, linked libraries should do the job.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Utility

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/utility/index.html

**Contents:**
- Utility

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Utils Templates

**URL:** https://upbge.org/docs/latest/manual/manual/python_components/getting_started/util_templates.html

**Contents:**
- Utils Templates
- Sound Speaker Component
- Minimap Component

These templates were created to help UPBGE users to create games or any kind of interactive things. Easy to use, easy to attach to your project.

To use, just select it from template label at script editor and you’re done! You can use this template in your projects, even for commercial projects. You only need to give credits to Guilherme Teres Nunes (UnidayStudio) for this. It’s very easy to use: Just load this script into your .blend file through template label (or paste it in the same folder that your .blend is), select the object that you want, and attach the script into the object’s components using Register Component button.

This component will serve as an sound Speaker for your game. With this, you can easly control 3D sound, volume. Unfortunatelly, the sounds needs to be mono to make the 3D sound works. You can convert your sound to mono using windows CMD like this: ‘> ffmpeg -i Sound.wav -ac 1 SoundMono.wav’ It’s very simple to configure:

Sound Speaker component

Sound File: The file name, example: “Assets/DoorMono.wav”.

Loop Sound: If you want the sound to loop or just play once.

3D Sound: If you want the sound to be 3D.

Min Distance: If 3D Sound is enabled, the sound will have the max volume if the listener is at this distance or minor.

Max Distance: If 3D Sound is enabled, the sound will volume down until zero when the listener reach this distance.

Delete Object After End: If enabled, the object will be deleted at the end of the sound (if Loop Sound equals to false).

This component will spawn a minimap based on the camera (which owns the component) view. Add this component to a camera and position it on top of your character. To configure, take a look at the values:

Camera Type: You can choose between Perspertive or Ortographic camera.

Camera Height: Define the height that you want your minimap camera to be. If you don’t want the component to modify this, just set to 0.

Minimap Position: The position of the center of the minimap on the screen (values go from 0 to 1).

Minimap Size: The size of the minimap (values go from 0 to 1).

Follow Object: You can define an object for the minimap to follow (like the player). Leave it empty if you don’t want.

Rotate on Z axis: If you define a Follow Object, you can also makes the minimap rotate on the Z axis according to the follow object’s rotation.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Values

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/index.html

**Contents:**
- Values

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Value Switch

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/value_switch.html

**Contents:**
- Value Switch
- Inputs
- Outputs
- Example

Will switch between two values, if condition is True. Used i.e. to switch movement speed of a character, if Shift key is pressed.

If checked, A will be selected, else B value will be selected. Accepts Boolean result from connected node.

Fixed value for A field, or a result from connected node. Value type is selected from dropdown menu.

Fixed value for B field, or a result from connected node. Value type is selected from dropdown menu.

Will result in A value (0.20) if Shift key is held down

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Value Switch List

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/value_switch_list.html

**Contents:**
- Value Switch List
- Inputs
- Outputs

Fixed value of selected type, or resulting value from connected node.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Value Switch List Compare

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/value_switch_list_compare.html

**Contents:**
- Value Switch List Compare
- Parameters
- Inputs
- Outputs

Boolean operator for comparison evaluation.

Resulting value of comparison.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Variables

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/data/variables/index.html

**Contents:**
- Variables

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Vectors

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/vectors/index.html

**Contents:**
- Vectors

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Vector

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/values/vector/index.html

**Contents:**
- Vector

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Vector Math

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/vector_math.html

**Contents:**
- Vector Math
- Parameters
- Inputs
- Outputs
- Example

Mode of vector math to perform.

I.e. Multiply takes 2 vectors (blue-ish input dot), Scale takes a vector and a float (gray input dot). Normalize only exposes 1 input socket, and will normalize input values between 0 to 1.

Result of vector math operation.

Vector Math nodes in Normalize and Scale mode

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Vector Rotate

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/vectors/vector_rotate.html

**Contents:**
- Vector Rotate
- Parameters
- Inputs
- Outputs

Selected mode for rotation.

Vector values of origin point.

Vector values of pivot point.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Vehicle

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/vehicle/index.html

**Contents:**
- Vehicle

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## VR

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/vr/index.html

**Contents:**
- VR

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## VR Controller

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/vr/vr_controller.html

**Contents:**
- VR Controller
- Parameters
- Outputs

Retrieves the current position and orientation of the VR controller if there is a running VR session.

Use the left or the right hand controller.

World position of the controller.

World orientation of the controller.

World orientation of the controller tip.

World orientation of the controller tip.

Index finger trigger value.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## VR Headset

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/input/vr/vr_headset.html

**Contents:**
- VR Headset
- Outputs

Retrieves the current position and orientation of the VR headset if there is a running VR session.

World position of the headset.

World orientation of the headset.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Walk

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/physics/character/walk.html

**Contents:**
- Walk
- Parameters
- Inputs
- Outputs
- Example

Use character’s local axis for walking.

If connected, condition must be fulfilled for node to activate.

Which character to use.

Vector3 values for walking to apply. todo

True if node performed successfully, else False.

Walk node at the end of the 4-Key Template

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## What’s New

**URL:** https://upbge.org/docs/latest/manual/manual/contribute/whats_new.html

**Contents:**
- What’s New

This page lists major changes and additions to the manual. The UPBGE release notes are located on the website.

UPBGE Manual Creation, 2018 Jul 9.

UPBGE big upgrade for version 0.3 and later, started, 2020 Jul 2.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Widgets

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/ui/widgets/index.html

**Contents:**
- Widgets

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Within Range

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/within_range.html

**Contents:**
- Within Range
- Parameters
- Inputs
- Outputs

Selected mode of operation.

Minumum value to compare against.

Maximum value to compare against.

If value is within range. todo

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## World

**URL:** https://upbge.org/docs/latest/manual/manual/editors/properties/world.html

**Contents:**
- World
- World
- Environment Lighting
- Mist

World settings enable you to set some basic effects which affect all scenes throughout your game, so giving it a feeling of unity and continuity. These include ambient light, depth effects (mist), etc.

World tab’s World panel

These color settings allow you to set some general lighting effects for your game.

Flatten blend or texture coordinates.

Render background with natural progression from horizon to zenith.

Render background with a real horizon, relative to the camera angle.

The RGB color at the horizon; i.e. the color and intensity of any areas in the scene which are not filled explicitly.

The RGB color at the zenith.

Ambient light mimics an overall background illumination obtained from diffusing surfaces. Its general color and intensity are set by these controls.

Ammount of exponential color correction for light.

The color range that will be mapped to 0-1.

World tab’s Environment Lighting panel

Environment Light provides light coming from all directions.

Light is calculated with a ray-traced method which is the same as that used by Ambient Occlusion. The difference is that Environment lighting takes into account the “ambient” parameter of the material shading settings, which indicates the amount of ambient light/color that that material receives.

Also, you can choose the environment color source (white, sky color, sky texture) and the light energy.

Defines the strength of environment light.

Defines where the color of the environment light comes from.

Using both settings simultaneously produces better global lighting. It is good for mimicking the sky in outdoor lighting.

World tab’s Mist panel

Mist can greatly enhance the illusion of depth in your rendering. To create Mist, UPBGE makes objects farther away more transparent (decreasing their Alpha value) so that they mix more of the background color with the object color. With Mist enabled, the further the object is away from the camera the less its alpha value will be.

Toggles mist on and off.

Sets the shape of the falloff of the mist.

The starting distance of the mist effect, measured from the camera. No misting will take place for objects closer than this distance.

The depth at which the opacity of objects falls to zero.

Overall minimum intensity of the mist effect.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## World Physics

**URL:** https://upbge.org/docs/latest/manual/manual/physics/world.html

**Contents:**
- World Physics
- Physics Panel
- Navigation Mesh
- Obstacle Simulation

The Game Physics located in the World panel determine the type of physical rules that govern the Game Engine scene, and the gravity value to be used. Based on the physics engine selected, in physics simulations in the Game Engine, Blender will automatically move Actors in the downward (-Z) direction. After you arrange the actors and they move as you wish, you can then bake this computed motion into keyframes (see Digging Deeper for more info).

Set the type of physics engine to use.

The default physics engine, in active development. It handles movement and collision detection. The things that collide transfer momentum to the collided object.

No physics in use. Things are not affected by gravity and can fly about in a virtual space. Objects in motion stay in that motion.

The gravitational acceleration, m.s-2 (in units of meters per squared second), of this world. Each object that is an actor has a mass and size slider. In conjunction with the frame rate, Blender uses this info to calculate how fast the object should accelerate downward.

The size of the occlusion culling buffer in pixel, use higher value for better precision (slower). The optimized Bullet DBVT for view frustum and occlusion culling is activated internally by default.

Sets the maximum number of physics steps per game frame if graphics slow down the game. higher value allows physics to keep up with real-time.

Sets the number of simulation sub-steps per physics time step. Higher value give better physics precision.

Set the nominal number of game frames per second. Physics fixed timestep = 1/fps, independently of actual frame rate.

Sets the maximum number of logic frame per game frame if graphics slows down the game, higher value allows better synchronization with physics.

These settings control the threshold at which physics is deactivated. These settings help reducing the processing spent on Physics simulation during the game.

The speed limit under which a rigid body will go to sleep (stop moving) if it stays below the limits for a time equal or longer than the deactivation time (sleeping is disabled when deactivation time is set to 0).

Same as linear threshold, but for rotation limit (in rad/s)

The amount of time in which the object must have motion below the thresholds for physics to be disabled (0.0 disables physics deactivation).

Rasterized cell size.

Rasterized cell height.

Minimum height where the agent can still walk.

Maximum height between grid cells the agent can climb.

Maximum walkable slope angle in degrees.

Minimum regions size. Smaller regions will be deleted.

Minimum regions size. Smaller regions will be merged.

Classic Recast partitioning method generating the nicest tessellation.

The fastest navmesh generation method, but may cause long thin polygons.

A reasonably fast method that produces better triangles than monotone partitioning.

Maximum contour edge length.

Maximum distance error from contour to cells.

Max number of vertices per polygon.

Detail mesh sample spacing.

Detail mesh simplification max sample error.

Simulation used for obstacle avoidance in the Game Engine, based on the RVO (Reciprocal Velocity Obstacles) principle. The aim is to prevent one or more actors colliding with obstacles.

See Pathfinding and steering behaviors for more details.

Obstacle simulation is disabled, actors are not able to avoid obstacles.

Obstacle simulation is based on the RVO method with cell sampling.

Obstacle simulation is based on the RVO method with ray sampling.

Max difference in heights of obstacles to enable their interaction. Used to define minimum margin between obstacles by height, when they are treated as those which are situated one above the other i.e. they does not influence to each other.

Enable debug visualization for obstacle simulation.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## World To Screen

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/scene/camera/world_to_screen.html

**Contents:**
- World To Screen
- Inputs
- Outputs

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---

## Writing Style Guide

**URL:** https://upbge.org/docs/latest/manual/manual/contribute/writing_style.html

**Contents:**
- Writing Style Guide
- Primary Goals
- Content Guidelines
- Glossary
- Examples

In order to maintain a consistent writing style within the manual, please keep this page in mind and only deviate from it when you have a good reason to do so.

While some areas of computer graphics are highly technical, this manual shall be kept understandable by non-technical users.

The manual aims to provide detailed functional description of all features, tools and options in UPBGE. This does not mean we have to document every small detail. The manual should provide information on what a feature is, how to use it, and its purpose.

Computer graphics is a vast field, there are many rules, exceptions to the rules, and interesting details. Expanding into details can add unnecessary content, so keep the text concise and relevant to the topic at hand.

Try to write content that will not have to be redone the moment some small change is made. This helps a small documentation community to maintain the manual.

Spell checking is strongly recommended.

Use American English (i.e. modeling and not modelling, color and not colour) also for formatting numbers (i.e. 2,718.28 and not 2 718,28).

Take care about grammar, appropriate wording and use simple English.

Keep sentences short and clear, resulting in text that is easy to read, objective and to the point.

Including why or how an option might be useful is a good idea.

If you are unsure about how a feature works, ask a developer or someone else.

Avoid writing in first person perspective, about yourself or your own opinions.

Issues that are known to the developers and are not going to be resolved before the next release can be documented as Known Limitations.

Avoid product placements, i.e. unnecessarily promoting software or hardware brands. Keep content vendor-neutral where possible.

Avoid technical explanations about the mathematical/algorithmic implementation of a feature - keep it simple.

Simply explain it once, and from then on refer to that explanation. For general terminology, consider defining a :term: in the glossary.

Such lists are only showing what is already obvious in the interface and end up being a lot of text to read and maintain.

That is what the release notes are for. We only need to document the current state of documentation.

Unless a unit or a value is obscure and unpredictable, there is no need to mention it.

People will come to the manual to learn more than what is provided by the UI.

Use a TODO comment (which is not shown in the HTML page, but useful for other editors):

This section is specifically about the Glossary section, where we define common terms in Blender/UPBGE and computer graphics.

Terms are added with :term: syntax, explained in Markup Style Guide.

Define the term before providing any further information.

Avoid using constructs such as “it is” or “xyz is” before the definition.

Avoid repeating the term immediately or using it in the definition.

Avoid adding terms not found in UPBGE/Blender’s interface or manual.

Avoid overly long entries. If an explanation of a complex term is needed, supplement with external links.

Avoid duplicating documentation; if explaining the term is the primary focus of another section of the manual (e.g. if the term is the name of a tool), either just link to that section, or avoid creating a glossary entry entirely.

URL references are to be added at the end, formatted as follows, e.g:

would be written like this instead, putting a definition first:

would be written like this, avoiding the immediate repetition of the term:

would be written like this, avoiding the “it is”:

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

**Examples:**

Example 1 (julia):
```julia
.. TODO:: how does this tool work ? ask Joe.
```

Example 2 (unknown):
```unknown
See also `OpenGL <https://en.wikipedia.org/wiki/OpenGL>`__ on Wikipedia.
```

Example 3 (unknown):
```unknown
Displacement Mapping
   Uses a grayscale heightmap, like Bump Mapping,
   but the image is used to physically move the vertices of the mesh at render time.
   This is of course only useful if the mesh has large amounts of vertices.
```

Example 4 (unknown):
```unknown
Displacement Mapping
   Uses a grayscale heightmap, like Bump Mapping,
   but the image is used to physically move the vertices of the mesh at render time.
   This is of course only useful if the mesh has large amounts of vertices.
```

---

## XYZ To Matrix

**URL:** https://upbge.org/docs/latest/manual/manual/logic_nodes/math/vectors/xyz_to_matrix.html

**Contents:**
- XYZ To Matrix
- Inputs
- Outputs

Vector3 values to convert.

Resulting matrix values.

© Copyright : This page is licensed under a CC-BY-SA 4.0 Int. License.

---
