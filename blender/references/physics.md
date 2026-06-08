# Blender - Physics

**Pages:** 47

---

## Boids¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/physics/boids.html

**Contents:**
- Boids¶
- Movement¶
- Battle¶
- Misc¶
- Relations¶
  - Deflection¶
  - Force Fields¶
- Boid Brain¶
  - Goal Rule¶
  - Avoid Rule¶

Particle System ‣ Physics

Boid Physics settings.¶

Boids particle systems are controlled by a limited artificial intelligence, which can be programmed to follow basic rules and behaviors. They are ideal for simulating flocks, swarms, herds and schools of various kind of animals, insects and fishes or predators vs. preys simulations. They can react on the presence of other objects and on the members of their own system. Boids can handle only a certain amount of information, therefore the sequence of the Boid Brain rules is very important. In certain situations only the first three parameter are evaluated.

Particle System ‣ Physics ‣ Movement

Boid Movement settings.¶

Boids avoid objects with Collision enabled, move toward goals, and flee from “predators” based on the Boid Brain. Their behavior changes depending on whether they are in the air or on land.

Enables movement in the air.

Enables movement on land.

Enables climbing toward goal objects.

The maximum velocity boids can achieve while in the air.

The minimum velocity boids maintain while flying.

Controls how quickly boids can change direction in the air, expressed as a percentage of their maximum velocity. Higher values result in more agile movements.

Limits how sharply boids can turn in the air, expressed as a percentage of 180 degrees. Lower values create smoother curves during flight.

The radius of personal space for boids in the air, as a percentage of their particle size. Larger values reduce crowding in swarms.

Adjusts how softly boids land on surfaces. Higher values ensure gradual transitions when landing.

The maximum velocity boids can achieve on land.

The velocity boids achieve during jumps.

Controls how quickly boids can change direction on land, expressed as a percentage of their maximum velocity.

Limits how sharply boids can turn on land, expressed as a percentage of 180 degrees. Lower values create smoother, less abrupt turns.

The radius of personal space for boids on land, as a percentage of their particle size. Larger values reduce crowding in herds or groups.

Determines the strength of a force required to influence boids on land. Use lower values to allow boids to move more freely when interacting with forces.

Restricts collisions to objects within the specified collection. This is useful for limiting interactions to certain objects or environments.

Particle System ‣ Physics ‣ Battle

Initial boid health when born.

Maximum caused damage per second on attack.

Boid will fight this time stronger than enemy.

Maximum distance of which a boid can attack.

Particle System ‣ Physics ‣ Misc

Amount of rotation around velocity vector on turns. Banking of 1.0 gives a natural banking effect.

Amount of rotation around side vector.

Boid height relative to particle size.

Particle System ‣ Physics ‣ Relations

This list view allows you to set up other particle systems to react with the boids.

A data ID to select an object with a particle system set on.

Index of the Object‘s particle system as set in the list view in the particle panel.

Setting the type to Enemy will cause the systems to fight with each other.

Will make the systems work together.

Will not cause them to align or fight with each other.

Boids will try to avoid deflector objects according to the Collision rule’s weight. It works best for convex surfaces (some work needed for concave surfaces).

As other physics types, Boids is also influenced by external force fields.

In addition, special Boid force fields can be used with the Boids physics. These effectors could be predators (positive Strength) that boids try to avoid, or targets (negative Strength) that boids try to reach according to the (respectively) Avoid and Goal rules of the Boid Brain.

Particle System ‣ Physics ‣ Boid Brain

The Boid Brain panel controls how the boids particles will react with each other. The boids’ behavior is controlled by a list of rules. Only a certain amount of information in the list can be evaluated. If the memory capacity is exceeded, the remaining rules are ignored.

The rules are by default parsed from top-list to bottom-list (thus giving explicit priorities), and the order can be modified using the little arrows buttons on the right side.

There are three ways to control how rules are evaluated:

All rules are averaged.

A random rule is selected for each boid.

Uses fuzzy logic to evaluate rules. Rules are gone through top to bottom. Only the first rule that affect above the Rule Fuzziness threshold is evaluated. The value should be considered how hard the boid will try to respect a given rule (a value of 1 means the Boid will always stick to it, a value of 0 means it will never). If the boid meets more than one conflicting condition at the same time, it will try to fulfill all the rules according to the respective weight of each.

A given boid will try as much as it can to comply to each of the rules it is given, but it is more than likely that some rule will take precedence on other in some cases. For example, in order to avoid a predator, a boid could probably “forget” about Collision, Separate and Flock rules, meaning that “while panicked” it could well run into obstacles, e.g. even if instructed not to, most of the time.

The current rule affects boids while they are flying.

The current rule affects boids while they are not flying.

Specifies the goal object. If not specified, Boid force fields with negative Strength are used as goals.

Predict target’s movements.

Specifies the object to avoid. If not specified, Boid force fields with positive Strength are used as predators.

Predict target’s movements.

Avoid object if danger from it is above this threshold.

Avoid objects with activated Deflection.

Avoid collision with other boids.

Avoid collision with deflector objects.

Time to look ahead in seconds.

Boids move away from each other.

Copy movements of neighboring boids, but avoid each other.

Follows a leader object instead of a boid.

Distance behind leader to follow.

Follow the leader in a line.

How many boids that are allowed to follow in a line.

Maintain average velocity.

Percentage of maximum speed.

How fast velocity’s direction is randomized.

How much velocity’s Z component is kept constant.

Move toward nearby boids.

Attack boids at a maximum of this distance.

Flee to this distance.

---

## Cache¶

**URL:** https://docs.blender.org/manual/en/latest/physics/cloth/settings/cache.html

**Contents:**
- Cache¶
- Editing the Cached Simulation¶

Physics ‣ Cloth Cache

After you have set up the deflection mesh for the frame range you intend to run the simulation (including animating that mesh via armatures), you can now tell the cloth simulation to compute (and avoid) collisions. Select the cloth object and in the Object tab, Physics tab, set the Start and End settings for the simulation frames you wish to compute, and click the Bake button.

Cache settings for cloth are the same as with other dynamic systems. See Particle Cache for details.

If you move or edit the cloth object after you have already run the simulations, you must clear the cache; otherwise, Blender will use the position of the current/cached mesh’s vertices when trying to represent where they are.

Subdivision Surface Modifier

A bake/cache is done for every subdivision level so please use the equal subdivision level for render and preview.

You cannot change Start or End without clearing the bake simulation. When the simulation has finished, you will notice you have the option to free the bake, edit the bake and re-bake.

Editing the cached simulation is not currently working, see: blender/blender#77114 for details.

---

## Cache¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/cache.html

**Contents:**
- Cache¶
- Hints¶

Particle System ‣ Cache

In order to improve real-time response and avoid unnecessary recalculation of particles, the particle data can be cached in memory or stored on a drive.

The Emitter particle system uses a unified system for caching and baking (together with Soft Body and Cloth).

Particles Cache settings.¶

See the General Baking docs for more information.

The simulation is only calculated for positive frames in between the Start and End frames of the Cache panel, whether you bake or not. So if you want a simulation that is longer than the default frame range, you have to change the End frame.

When an animation is played, each physics system writes each frame to the cache. Note that for the cache to fill up, one has to start the playback before or on the frame that the simulation starts.

The cache is cleared automatically on changes. But not on all changes, so it may be necessary to delete it manually, e.g. if you change a force field.

The system is protected against changes after baking. If for example the mesh changes the simulation is not calculated anew.

The bake result can be cleared by clicking on the Delete Bake button in the simulation cache settings.

A simulation can only be edited in Particle Edit Mode when it has been baked in memory. And cannot be edited if the Disk Cache is used.

If you are not allowed to write to the required subdirectory caching will not take place, e.g. if your blend-file path is very long and your operating system has a limit on the path length that is supported.

Be careful with the sequence of modifiers in the modifier stack. You may have a different number of faces in the 3D Viewport and for rendering (e.g. when using subdivision surface), if so, the rendered result may be very different from what you see in the 3D Viewport.

---

## Cache¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/settings/cache.html

**Contents:**
- Cache¶

Physics ‣ Soft Body ‣ Cache

Soft Body physics simulations use a unified system for caching and baking. See Particle Cache and General Baking documentation for reference.

---

## Children¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/children.html

**Contents:**
- Children¶
- Common Options¶
  - Clumping¶
    - Clump Noise¶
  - Roughness¶
  - Kink¶
- Simple¶
- Interpolated¶
  - Parting¶
- Example¶

Particle System ‣ Children

Children are Hair or Emitter particles originating from individual particles. They make it possible to work primarily with a relatively low amount of Parent particles, for whom the physics are calculated. The children are then aligned to their parents. The number and visualization of the children can be changed without a recalculation of the physics.

If you activate children, the parents are no longer rendered. This can be enabled in the Render panel Parent Particles. By default, parent particles are not rendered because the shape of the children can be quite different from that of their parents.

No children are generated.

Children are emitted from the parent position.

Children are emitted between the Parent particles on the faces of a mesh. They interpolate between adjacent parents. This is especially useful for fur, because you can achieve an even distribution. Some of the children can become virtual parents, which are influencing other particles nearby.

The number of children in the 3D Viewport.

The number of children to be rendered.

Length of child paths.

Amount of particles left untouched by child path length.

Offset in the random number table for child particles, to get a different randomized result.

Particle System ‣ Children ‣ Clumping

Use Curve Widget instead of parameters.

Clumping amount along child strands. The children may meet at their tip (1.0) or start together at their root (-1.0).

Form of Clump. Either inverse parabolic (0.99) or exponentially (-0.99).

Creates random clumps around the parent hair.

The size of the clumps.

Particle System ‣ Children ‣ Roughness

Use Curve Widget instead of parameters.

It is based on children location so it varies the paths in a similar way when the children are near.

“Rough End” randomizes path ends (a bit like random negative clumping). Shape may be varied from <1 (parabolic) to 10.0 (hyperbolic).

It is based on a random vector so it is not the same for nearby children. The threshold can be specified to apply this to only a part of children. This is useful for creating a few stray children that will not do what others do.

Particle System ‣ Children ‣ Kink

Child particles with Kink.¶

From left to right: Curl, Radial, Wave, Braid, Spiral.

With Kink you can rotate the children around the parent. See Fig. Child particles with Kink. above picture for the different types of Kink.

Children grow in a spiral around the parent hairs.

Children form around the parent a wave shape that passes through the parent hair.

Children form a wave, all in the same direction.

Children braid themselves around the parent hair.

Generates a spiral at the end of each hair.

Define the overall size.

Makes the spiral grow in- or outward.

Alignment Limitations

When hair is pointing straight up (along the chosen spiral axis, default Z), spirals may not show up! This is a limitation of the projection method used. Giving a slight tilt or random orientation to hairs fixes this.

The amplitude of the offset.

How much clump effects kink amplitude.

How flat the hairs are.

The frequency of the offset (1/total length). The higher the frequency the more rotations are done.

Where the rotation starts (offset of rotation).

A multiplier for children size.

Random variation to the size of child particles.

The radius in which the children are distributed around their parents. This is 3D, so children may be emitted higher or lower than their parents.

The roundness of the children around their parents. Either in a sphere (1.0) or in-plane (0.0).

Relative amount of virtual parents.

Calculate children that suit long hair well.

Creates parting in the children based on parent strands.

The minimum/maximum root to tip angle (tip distance/root distance for long hair).

From left to right: Round: 0.0, Round: 1.0, Clump: 1.0, Clump: -1.0, Shape: -0.99.¶

---

## Collection¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/object/properties/instancing/collection.html

**Contents:**
- Collection¶
- Basic Usage¶
- Collections and Dynamic Linking¶
- Making an Instanced Collection Real¶

Properties ‣ Object Properties ‣ Instancing ‣ Collection

Instance Collections allows you to create an instance of a collection for each instance of another object. Collections may contain animations, objects with physics simulations and even other nested collections.

Create a new collection (this can be done via the Outliner).

Link the objects that need to be instanced as part of the newly created collection.

Add ‣ Collection Instance

At this point, an instance of the collection and an empty object will appear. You can duplicate the empty, and the Instance Collections settings will be preserved for each empty. This way, you can get multiple copies of linked data very easily.

See Appending and Linking to understand how to dynamically link data from another blend-file into the current file. You can dynamically link collections from one blend-file to another. When you do so, the linked collection does not appear anywhere in your scene until you create an object controlling where the collection instance appears.

If you want to make further edits on an instanced collection select the Instance Collection. Then call Make Instances Real to convert the collection into regular objects that can be transformed and animated normally.

Note that if the instanced collection was linked from an external file, the Object Data (mesh, materials, textures, transforms) will also still be linked from the original collection. However, the various object’s parent-child relationships do not carry over.

---

## Collisions¶

**URL:** https://docs.blender.org/manual/en/latest/physics/cloth/settings/collisions.html

**Contents:**
- Collisions¶
- Object Collisions¶
- Self-Collisions¶
  - Troubleshooting¶

Physics ‣ Cloth ‣ Collision

In most cases, a piece of cloth does not just hang there in 3D space, it collides with other objects in the environment. To ensure proper simulation, there are several items that have to be set up and working together:

The Cloth object must be told to participate in collisions.

Optionally (but recommended) tell the cloth to collide with itself.

Other objects must be visible to the Cloth object via shared layers.

The other objects must be mesh objects.

The other objects may move or be themselves deformed by other objects (like an armature or shape key).

The other mesh objects must be told to deflect the cloth object.

The blend-file must be saved in a directory so that simulation results can be saved.

You then Bake the simulation. The simulator computes the shape of the cloth for a frame range.

You can then edit the simulation results, or make adjustments to the cloth mesh, at specific frames.

You can make adjustments to the environment or deforming objects, and then re-run the cloth simulation from the current frame forward.

Cloth Collisions panel.¶

A general setting for how fine and good a simulation you wish. Higher numbers take more time but ensure less tears and penetrations through the cloth.

If the cloth object needs to be deflected by some other object. To deflect a cloth, the object must be enabled as an object that collides with the cloth object. To enable objects to collide with cloth objects enable collision physics for the collider object (not on the cloth object).

If your colliding object is not a mesh object, such as a NURBS surface, or a text object, you must convert it to a mesh object using Convert.

The distance another object must get to the cloth for the simulation to repel the cloth out of the way. Smaller values might give errors but gives some speed-up while larger will give unrealistic results if too large and can be slow. It is best to find a good in between value.

Prevents explosions in tight and complicated collision situations by restricting the amount of movement after a collision.

Faces that have all vertices assigned to this Vertex Group are excluded from collision with objects.

Only objects that are a part of this Collection can collide with the cloth. Note that these objects must also have Collision physics enabled.

Real cloth cannot penetrate itself, so you normally want the cloth to self-collide. Enable this to tell the cloth object that it should not penetrate itself. This adds to the simulation’s compute time, but provides more realistic results.

A flag, viewed from a distance does not need this enabled, but a close-up of a cape or blouse on a character should have this enabled.

A coefficient for how slippery the cloth is when it collides with itself. For example, silk has a lower coefficient of friction than cotton.

As cloth at this distance begins to repel away from itself. Smaller values might give errors but gives some speed-up while larger will give unrealistic results if too large and can be slow. It is best to find a good in between value.

Prevents explosions in tight and complicated collision situations by restricting the amount of movement after a collision.

Faces that have all vertices assigned to this Vertex Group are excluded from self-collision.

Example blend-file: Cloth self-collisions.

If you encounter some problems with collision detection, there are a few ways to fix them:

The fastest solution is to increase the Distance for Object/Self Collisions. This will be the fastest way to fix the clipping; however, it will be less accurate and will not look as good. Using this method tends to make it look like the cloth is resting on air, and gives it a very rounded look.

A second method is to increase the Quality (in the Cloth panel). This results in smaller steps for the simulator and therefore to a higher probability that fast-moving collisions get caught. You can also increase the Collisions Quality to perform more iterations to get collisions solved.

If none of the methods help, you can easily edit the cached/baked result in Edit Mode afterwards.

If the Cloth is torn by the deforming mesh; increase the stiffness settings.

---

## Collisions¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/properties/collisions.html

**Contents:**
- Collisions¶
- Surface Response¶
- Sensitivity¶
- Collections¶

Physics ‣ Rigid Body ‣ Collisions

Rigid Body Collisions panel.¶

Determines the collision shape of the object; these can be broken into two categories: primitive shapes and mesh based shapes.

Primitive shapes (Box, Sphere, Capsule, Cylinder, and Cone) are best in terms of memory and performance but do not necessarily reflect the actual shape of the object. The size of the shape is calculated based on the object’s bounding box. The center of gravity is always in the geometric center of the shape. Primitive shapes can be shown in the 3D Viewport by enabling Extras Overlay.

Mesh based shapes (Convex Hull and Mesh) are calculated based on the geometry of the object so they are a better representation of the object. The center of gravity for these shapes is the object origin.

Box-like shapes (e.g. cubes), including planes (e.g. ground planes). The size per axis is calculated from the bounding box.

Sphere-like shapes. The radius is the largest axis of the bounding box.

This points up the Z axis.

This points up the Z axis. The height is taken from the Z axis, while the radius is the larger of the X or Y axes.

This points up the Z axis. The height is taken from the Z axis, while the radius is the larger of the X or Y axes.

A mesh-like surface encompassing (e.g. shrink-wrapped over) all vertices (best results with fewer vertices). A convex approximation of the object, which has good performance and stability.

Mesh consisting of triangles only, allowing for more detailed interactions than convex hulls. Allows simulating concave objects, but is rather slow and unstable.

Takes the collision shapes from the object’s children and combines them. This makes it possible to create concave shapes from primitive shapes. This usually results in a faster simulation than the Mesh collision shape while also being generally more stable.

Source of the mesh used to create the collision shape.

The base mesh of the object.

Includes any deformations added to the mesh (shape keys, deform modifiers).

Includes all deformations and modifiers.

Mesh shapes can deform during simulation.

Resistance of object to movement. Specifies how much velocity is lost when objects collide with each other.

Tendency of object to bounce after colliding with another (0 to 1) (rigid to perfectly elastic). Specifies how much objects can bounce after collisions.

The collision margin is used to improve the performance and stability of rigid bodies. Depending on the shape, it behaves differently: some shapes embed it, while others have a visible gap around them.

The margin is embedded for these shapes:

Convex Hull: Only allows for uniform scale when embedded.

The margin is not embedded for these shapes:

Passive Triangle Mesh: Can be set to 0 most of the time.

Threshold of distance near the surface where collisions are still considered (best results when nonzero).

Allows rigid body collisions allocate on different groups (maximum 20).

---

## Collision¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/collision.html

**Contents:**
- Collision¶
- Collisions with Other Objects¶
  - Examples¶
  - Calculating Collisions¶
  - Good Collisions¶
- Self-Collisions¶

There are two different collision types that you may use: collision between different objects and internal collision. We should set one thing straight from the start – the primary targets of the collision calculation are the vertices of a soft body. So if you have too few vertices too few collision takes place. Secondarily, you can use edges and faces to improve the collision calculation.

For a soft body to collide with another object there are a few prerequisites:

If Collision Collection is set, the object must belong to the collection.

The collision object has to be a mesh object.

You have to activate the Collision in the Physics tab for the collision object. The collision object may also be a soft body.

A soft body cube colliding with a plane (Fig. A soft body cube colliding with a plane.) works pretty well, but a soft body plane falls right through a cube that it is supposed to collide with (Fig. A soft body plane colliding with a cube, so no interaction at all.).

A soft body cube colliding with a plane.¶

A soft body plane colliding with a cube, so no interaction at all.¶

Why is that? Because the default method of calculation only checks to see if the four vertices of the soft body plane collides with the cube as the plane is pulled down by gravity. You can activate Collision: Face (in the Soft Body Edges panel) to enable collision between the face of the plane and the object instead, but this type of calculation takes much longer.

Let us have a closer look at the collision calculation, so you can get an idea of how we might optimize it.

Soft body simulations are by default done on a per-vertex basis. If the vertices of the soft body do not collide with the collision object, there will be no interaction between the two objects.

In the video below, you can see the vertices colliding with a plane. If a vertex penetrates the zone between Outer and Inner, it is repulsed by a force in the direction of the face normal. The position that a vertex finally ends up in is dependent on the forces that act upon it. In the example (the first vertex on the left in the video below) gravity and the repulsion force of the face balance out. The speed at which the vertex is pulled out of the collision zone is influenced by the Choke parameter in the Soft Body Solver settings.

Download the blend-file.

Now let’s see what happens if we make vertices heavier and let them travel at a faster speed. In the video above, you can see vertices traveling at different speeds. The two on the far right (fifth and sixth) are traveling so fast that they pass right through the collision zone (this is because of the default solver precision, which we can fix later). You will notice that the fourth vertex also travels quite fast and because it is heavier it breaches the inner zone. The first three vertices collide correctly.

You can set up your collision so that edges and even faces are included in the collision calculation in the Soft Body Edges panel with the Collision Face and Edge options. The collision is then calculated differently. It is checked whether the edge or face intersects with the collision object, the collision zones are not used.

If the collision you have set up is not behaving properly, you can try the following:

The soft body object must have more subdivisions than the collision object. Add loop cuts to the soft body object in strategic areas that you know are most likely to be involved in a collision.

Check the direction of the face normals.

If the collision object has sharp spikes, they might penetrate the soft body.

The resolution of the solver must match the speed at which soft body vertices are traveling. Lower the parameter Error Limit and carefully increase Min Step.

Outer and Inner should be large enough, but zones of opposite faces should not overlap, or you have forces in opposite directions.

If you use strong forces you should use large zones.

Set Choke to a high enough value (all the way up if necessary) if you have difficulties with repelled vertices.

Colliding faces are difficult to control and need long calculation times. Try not to use them.

Often it is better to create a simplified mesh to use as your collision object, however, this may be difficult if you are using an animated mesh.

For information on self-collision please refer to the Self Collision settings.

---

## Dynamics¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/properties/dynamics.html

**Contents:**
- Dynamics¶
- Deactivation¶

Physics ‣ Rigid Body ‣ Dynamics

Rigid Body Dynamics panel.¶

Used to control the physics of the rigid body simulation. This panel is available only for Active type of rigid bodies.

Amount of linear velocity that is lost over time.

Amount of angular velocity that is lost over time.

Enable deactivation of resting rigid bodies. Allows the object to be deactivated during the simulation (improves the performance and stability, but can cause glitches).

The rigid body starts deactivated. It will be activated when in proximity of moving active rigid body objects. The proximity check uses the object’s bounding box to determine if a moving object is close enough to activate it.

Specifies the linear deactivation velocity below which the rigid body is deactivated and the simulation stops simulating the object.

Specifies the angular deactivation velocity below which the rigid body is deactivated and the simulation stops simulating the object.

---

## Edges¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/settings/edges.html

**Contents:**
- Edges¶
- Aerodynamics¶
- Stiffness¶

Physics ‣ Soft Body ‣ Edges

Allow the edges in a mesh object to act like springs. See interior forces.

Use a specified vertex group for spring strength values.

The spring stiffness for edges (how much the edges are allowed to stretch). A low value means very weak springs (a very elastic material), a high value is a strong spring (a stiffer material) that resists being pulled apart.

A value of 0.5 is latex, 0.9 is like a sweater, 0.999 is a highly-starched napkin or leather. The soft body simulation tends to get unstable if you use a value of 0.999, so you should lower this value a bit if that happens.

How much the soft body resists being scrunched together, like a compression spring. Low values for fabric, high values for inflated objects and stiff material.

The friction for edge springs. High values (max of 50) dampen the Push/Pull effect and calm down the cloth.

Permanent deformation of the object after a collision. The vertices take a new position without applying the modifier.

This option creates virtual connections between a vertex and the vertices connected to its neighbors. This includes diagonal edges. Damping also applies to these connections.

The edges can shrink or be blown up. This value is given in percent, 0 disables this function. 100% means no change, the body keeps 100% of its size.

Checks for edges of the soft body mesh colliding.

Checks for any portion of the face of the soft body mesh colliding (which is computationally intensive). While Face enabled can solve collision errors, there does not seem to be any dampening settings for it. So parts of the soft body object near a collision mesh tend to “jitter” as they bounce off and fall back, even when there is no motion of any meshes. Edge collision has dampening, so that can be controlled, but Deflection dampening value on a collision object does not seem to affect the face collision.

Force from surrounding media. See exterior forces for details.

Edges receive a drag force from the surrounding media.

Edges receive a lift force when passing through the surrounding media.

How much aerodynamic force to use. Try a value of 30 at first.

For quad faces, the diagonal edges are used as springs. This stops quad faces to collapse completely on collisions (what they would do otherwise).

Stiffness of the virtual springs created for quad faces.

---

## Emission¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/emission.html

**Contents:**
- Emission¶
- Source¶

Particle System ‣ Emission

The Emitter system works just like its name says: it emits/produces particles for a certain amount of time. In such a system, particles are emitted from the selected object from the Start frame to the End frame and have a certain lifespan. These particles are rendered default as Halos, but you may also render this kind of particles as objects (depending on the particle system’s render settings, see Visualization).

Particle Emission settings.¶

The buttons in the Emission panel control the way particles are emitted over time:

The maximum amount of parent particles used in the simulation.

Blender uses this as starting point to produce random numbers during the simulation.

The start frame of particle emission. You may set negative values, which enables you to start the simulation before the actual rendering.

The end frame of particle emission.

The lifespan (in frames) of the particles.

A random variation of the lifetime of a given particle. The shortest possible lifetime is Lifetime × (1 - Random). Values above 1.0 are not allowed. For example with the default Lifetime value of 50 a Random setting of 0.5 will give you particles with a live span ranging from 50 frames to \(50 × (1.0 - 0.5) = 25\) frames, and with a Random setting of 0.75 you will get particles with live spans ranging from 50 frames to \(50 × (1.0 - 0.75) = 12.5\) frames.

Particle System ‣ Emission ‣ Source

Defines how and where the particles are emitted, giving precise control over their distribution.

You may use vertex groups to confine the emission, that is done in the Vertex Groups panel.

Emits particles from the vertices of a mesh.

Emits particles from the surface of a mesh’s faces.

Emits particles from the volume of an enclosed mesh.

Your mesh must be Manifold to emit particles from the volume. Some modifiers like the Edge Split Modifier break up the surface, in which case volume emission will not work correctly!

Take any Modifiers above the Particle Modifier in the modifier stack into account when emitting particles, else it uses the original mesh geometry.

Note that particles may differ in the final render if these modifiers generate different geometry between the viewport and render.

These settings control how the emissions of particles are distributed throughout the emission locations when emitting from either Faces or Volume.

Particles are placed at jittered intervals on the emitter elements.

Number of emissions per face (0 = automatic).

Amount of jitter applied to the sampling.

Particles are emitted from random locations in the emitter’s elements.

Particles are set in a 3D grid and particles near/in the elements are kept.

Invert what is considered the object and what is not.

Uses a hexagonal-shaped grid instead of a rectangular one.

Resolution of the grid.

Add a random offset to grid locations.

The emitter element indices are gone through in a random order instead of linearly (one after the other).

Not available for Grid distribution.

Particle distribution is made even based on surface area of the elements, i.e. small elements emit less particles than large elements, so that the particle density is even.

---

## Emission¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/hair/emission.html

**Contents:**
- Emission¶

Particle System ‣ Emission

Hair particle system settings.¶

Sets the amount of hair strands. Use as few particles as possible (especially if you plan to use soft body animation later), but still enough to cover the surface and have good control. A few thousand particles is generally enough for a regular haircut. The hair will be made denser later on using Children.

Controls the length of the hair.

Emitter particles Emission panel

---

## Examples¶

**URL:** https://docs.blender.org/manual/en/latest/physics/cloth/examples.html

**Contents:**
- Examples¶
- Using Simulation to Shape/Sculpt a Mesh¶
- Smoothing of Cloth¶
- Cloth on Armature¶
- Cloth with Animated Vertex Groups¶
- Cloth with Dynamic Paint¶
- Using Cloth for Soft Bodies¶
- Cloth with Wind¶

To start with cloth, the first thing you need, of course, is some fabric. So, let us delete the default cube and add a plane. In order to get some good floppy and flexible fabric, you will need to subdivide it several times, about eight is a good number. So Tab into Edit Mode and subdivide the mesh a couple of times.

Now, we will make this cloth by going to the Physics tab. Scroll down until you see the Cloth panel, and press the Cloth button. Now, a lot of settings will appear, most of which we will ignore for now.

That is all you need to do to set your cloth up for animating, but if you playback the animation, the drop of your newly created fabric will be quite unspectacular. That is what we will cover in the next two sections about pinning and colliding.

You can Apply the Cloth Modifier at any point to freeze the mesh in position at that frame. You can then re-enable the cloth, setting the start and end frames from which to run the simulation forward.

Another example of aging is a flag. Define the flag as a simple grid shape and pin the edge against the flagpole. Simulate for 50 frames or so, and the flag will drop to its “rest” position. Apply the Cloth Modifier. If you want the flag to flap or otherwise move in the scene, re-enable it for the frame range when it is in camera view.

Now, if you followed this from the previous section, your cloth is probably looking a little blocky. In order to make it look nice and smooth like the picture you need to apply a Smooth and/or Subdivision Surface Modifier in the Modifiers tab. Then, in the Toolbar, find the Edit panel and Press Smooth.

Clothing can be simulated and pinned to an armature. For example, a character could have a baggy tunic pinned to the character’s waist with a belt.

The typical workflow for pinning:

Set the armature to its bind pose.

Model clothing that encloses but does not penetrate the character’s mesh.

Parent the clothing objects to the armature. The armature will now have several child meshes bound to it.

Create a new vertex group on each cloth object for its pinned vertices.

Add vertices to be pinned to this vertex group and give these vertices nonzero weights (you probably want weight = 1). For example the belt area of the tunic would be in the vertex group and have weight one.

Designate the clothing objects as “cloth” in the Physics tab of the Properties. Make sure the Cloth Modifier is below the Armature Modifier in the modifier stack.

In the cloth Shape panel select the vertex group.

Add collision physics to the character’s mesh.

The clothing is now ready; non-pinned vertices will be under control of the Cloth modifier. Pinned vertices will be under control of the Armature modifier.

When animating or posing the character you must begin from the bind pose. Move the character to its initial pose over several frames so the physics engine can simulate the clothing moving. Very fast movements and teleport jumps can break the physics simulation.

Regression blend-file.

Cloth with animated pinned vertices: Regression blend-file. Unsupported: Starting with a goal of 0 and increasing it, but still having the vertex not pinned will not work (e.g. from goal = 0 to goal = 0.5).

Cloth with Dynamic Paint using animated vertex groups: Regression blend-file. Unsupported: Starting with a goal of 0 and increasing it, but still having the vertex not pinned will not work (e.g. from goal = 0 to goal = 0.5) because the necessary “goal springs” cannot be generated on-the-fly.

Using cloth for soft bodies.¶

Cloth can also be used to simulate soft bodies. It is for sure not its main purpose but it works nonetheless. The example image uses standard Rubber material, no fancy settings, just Alt-A.

Blend-file for the example image: Using Cloth for soft bodies.

Flag with wind applied.¶

Regression blend-file for Cloth with wind and self-collisions (also the blend for the image above): Cloth flag with wind and self-collisions.

---

## Examples¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/examples.html

**Contents:**
- Examples¶
- A Bouncing Cube¶
  - The Process¶
  - The Result¶

Here are some simple examples showing the power of soft body physics.

First, change your start and end frames to 1 and 150.

Then, add a plane, and scale it five times. Next, go to the physics tab, and add a collision. The default settings are fine for this example.

Now add a cube, or use the default cube, then enter Edit Mode to subdivide it three times. Add a Bevel Modifier to it to smoothen the edges and then to add a little more, press R twice, and move your cursor a bit.

When finished, your scene should look like this:

The scene, ready for soft body physics.¶

Everything is ready to add the soft body physics. Go to Properties ‣ Physics and choose Soft Body. Uncheck the Soft Body Goal, and check Soft Body Self Collision. Also, under Soft Body Edges, increase the Bending to 10.

Playing the animation will now give a slow animation of a bouncing cube. To speed things up, we need to bake the soft body physics.

Under Soft Body Cache change the values of your start and end frames. In this case 1 and 150. Now, to test if everything is working, you can take a cache step of 5 or 10, but for the final animation it is better to reduce it to 1, to cache everything.

When finished, your physics panel should look like this:

The physics cache settings.¶

The physics edges and self collision settings.¶

You can now bake the simulation, give the cube materials and textures and render the animation.

The rendered bouncing cube

---

## Exterior¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/forces/exterior.html

**Contents:**
- Exterior¶
- Example¶
- Force Fields¶
  - Soft Body Field Weights¶
- Aerodynamics¶
- Goal¶
  - Goal Strength¶
- Technical Details¶

Exterior forces are applied to the vertices (and nearly exclusively to the vertices) of soft body objects. This is done using Newton’s Laws of Physics:

If there is no force on a vertex, it stays either unmoved or moves with constant speed in a straight line.

The acceleration of a vertex depends on its mass and the force. The heavier the mass of a vertex the slower the acceleration. The larger the force the greater the acceleration.

For every action there is an equal and opposite reaction.

Well, this is done only in the range of computing accurateness, there is always a little damping to avoid overshoot of the calculation.

We will begin with a very simple example: the default cube.

To judge the effect of the external forces you should at first turn off the Goal, so that the vertices are not retracted to their original position.

Start playback to run the simulation.

What happens? The cube moves in negative Z direction. Each of its eight vertices is affected by a global, constant force – the gravitation. Gravitation without friction is independent from the weight of an object, so each object you would use as a soft body here would fall with the same acceleration. The object does not deform, because every vertex moves with the same speed in the same direction.

Soft body vertices interact with all the Force Fields applied (usually to particles) in the layer, such as wind, force fields, and what ever physics field effect is on a common layer.

Physics ‣ Soft Body ‣ Field Weights

The Soft Body Field Weights panel allows you to control how much influence each type of external force field has on the soft body system.

Limit effectors to a specified group. Only effectors in this group will have an effect on the current system.

Control how much the Global Gravity has an effect on the system.

Scale all of the effector weights.

Edges can be affected by wind as they move, and sail or flutter in a breeze. A simple aerodynamic model of a flag sailing in the wind.

This special exterior force is not applied to the vertices but to the connecting edges. Technically, a force perpendicular to the edge is applied. The force scales with the projection of the relative speed on the edge (dot product). Note that the force is the same if wind is blowing or if you drag the edge through the air with the same speed. That means that an edge moving in its own direction subject to no force, and an edge moving perpendicular to its own direction is subjected to maximum force.

The angle and the relative speed between medium and edge is used to calculate the force on the edge. This force results that vertices with few connecting edges (front of a plane) fall faster than vertices with more connecting edges (middle of a plane). If all vertices have the same amount of edges in a direction they fall with equal speed.

The Aerodynamics settings are set in the Soft Body Edges panel.

A “goal” is a shape that a soft body object tries to conform to. It acts like a pin on a chosen set of vertices, controlling how much of an effect soft body has on them.

Enabling Soft Body Goal tells Blender to use the position (or animated position) of a vertex in the simulation. Animating the vertices can be done in all the usual ways (F-Curves, armatures, parents, lattices, etc.) before the soft body simulation is applied. The “goal” is the desired end position for vertices. How a soft body tries to achieve this goal can be defined using stiffness forces and damping.

See the Goal Settings for details.

The Goal Strength defines how much motion from an animation system gets applied.

A Goal value of 1.0 means no soft body simulation, the object act like any regular animated object (i.e. the vertex is kept at its original position). When setting Goal to 0.0 (or no goal), the vertex is only influenced by physical laws according to soft body simulation.

By setting goal values between 0.0 and 1.0, you can blend between having the object affected only by the animation system, and having the object affected only by the soft body effect.

Goal also serves as a memory, to make sure soft objects don’t deform too much, ending up in the non-soft animated shape. Using the Vertex Group weight system, you can define a Goal weight per vertex. To make this look more natural, spring forces can be defined to control how far vertices can move from their original position.

Often Weight Paint is used to adjust the weight comfortably. For non-mesh objects the Weight parameter of their vertices/control points is used instead; Use the Context menu in Edit Mode or the Transform panel in the Sidebar region. The weight of Hair particles can also be painted in Particle Edit Mode.

In the Soft Body world, vertices of meshes are treated as particles having a mass. Their movement is determined by the forces affecting them. Beside other forces the individual particles can interact with another along edges using a physical model which is very close to shock absorbers used in cars. The working parts are:

A spring trying to keep the particles at a certain distance. How hard the spring tries to do that is controlled by the soft body parameter Stiffness.

A damping element to calm the movement down. The resistance the element builds up against motion is controlled by the soft body parameter Damping.

---

## Field Weights¶

**URL:** https://docs.blender.org/manual/en/latest/physics/cloth/settings/field_weights.html

**Contents:**
- Field Weights¶

Physics ‣ Cloth ‣ Field Weights

As other physics dynamics systems, Cloth simulation is also influenced by external force effectors.

---

## Force Fields¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/force_field.html

**Contents:**
- Force Fields¶
- Field Weights¶
- Force Fields Settings¶

Particle System ‣ Field Weights

The Field Weight panel allows you to control how much influence each type of external force field, or effector, has on the particle system. Force fields are external forces that give dynamic system’s motion. The force fields types are detailed on the Force Field Page.

Limit effectors to a specified group. Only effectors in this group will have an effect on the current system.

Control how much the Global Gravity has an effect on the system.

Scale all of the effector weights.

Particle System ‣ Force Fields Settings

The Force Field Settings panel allows you to make each individual act as a force field, allowing them to affect other dynamic systems, or even, each other.

Causes the particle force fields to have an effect on other particles within the same system.

Set how many of the particles act as force fields. 0 means all of them are effectors.

You can give particle systems up to two force fields. By default they do not have any. Choose an effector type from the selector to enable them. Settings are described in the Common Settings section.

---

## Hair¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/hair/index.html

**Contents:**
- Hair¶

This page is about the end of life hair system. Read about the new hair system on the Hair Nodes page.

---

## Hair Dynamics¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/hair/dynamics.html

**Contents:**
- Hair Dynamics¶
- Collisions¶
- Structure¶
- Volume¶

Particle System ‣ Hair Dynamics

Hair particles can have dynamic properties using physics. To enable hair physics, click the checkbox beside Hair Dynamics.

Quality of the simulation in steps per frame (higher is better quality but slower).

Spring stiffness of the vertex target position.

If you use motion blur in your animation, you will need to bake one extra frame past the last frame which you will be rendering.

A general setting for how fine and good a simulation you wish. Higher numbers take more time but ensure less tears and penetrations through the hair.

The distance another object must get to the hair for the simulation to repel the hair out of the way. Smaller values might cause errors but provide some speed-up while larger will give unrealistic results if too large and can be slow. It is best to find a good in between value.

Prevents explosions in tight and complicated collision situations by restricting the amount of movement after a collision.

Only objects that are a part of this Collection can collide with the hair. Note that these objects must also have Collision physics enabled.

Particle System ‣ Hair Dynamics ‣ Structure

Value for the mass of the hair.

Controls the bending stiffness of the hair strands.

Random stiffness of hair.

Damping of bending motion.

Particle System ‣ Hair Dynamics ‣ Volume

Some phenomena of real-world hair can be simulated more efficiently using a volumetric model instead of the basic geometric strand model. This means constructing a regular grid such as those used in fluid simulations and interpolating hair properties between the grid cells.

Controls how thick the air is around the hair causing the hair to flow slower.

Amount of friction between individual hairs.

Size of the voxel grid cells for interaction effects.

Maximum density of the hair.

The influence that the Density Target has on the simulation.

---

## Interior¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/forces/interior.html

**Contents:**
- Interior¶
- Stiffness¶
- Bending Stiffness¶

By default, the edges of a soft-body mesh act like springs. This means that, like a mechanical spring, they can stretch under tension and squeeze under pressure. Their initial length is also their “ideal” or “rest” length, which they try to return to.

Having edges act like springs is what holds the mesh together. If you were to disable this behavior (as well as the Goal), each vertex would be free to go anywhere independently of the others, which would stretch the mesh until it’s no longer recognizable.

Having springs along edges alone typically isn’t enough, however: vertices in quads are still free to move towards their diagonal opposite, potentially collapsing the quad into a line.

You could solve this by creating diagonal edges everywhere, but fortunately, you don’t have to: simply enable the Stiffness option to have Blender create diagonal springs internally. This way, you don’t have to change your mesh.

Base springs along edges.¶

Additional springs when Stiffness is enabled.¶

Another method of preventing mesh collapse is applying Bending Stiffness, which adds rotational resistance: making edges try to keep their relative angles.

Both of these methods are described in more detail below. You can configure them, as well as other settings, in the Soft Body Edges panel.

To show the effect of the Stiffness setting, we will drop two cubes onto a plane (see Collisions). The blue cube uses quads, while the red one uses triangles. Both cubes have their Goal setting disabled.

If Stiffness is disabled, the quad-only cube will collapse completely, while the tri cube only temporarily deforms from the impact:

If Stiffness is enabled, the quad cube maintains its shape as well thanks to the extra springs:

The second method to stop an object from collapsing is to give it Bending Stiffness. Just like the other settings, this can be combined with Stiffness to add bending resistance to the diagonal springs as well.

We first do the same cube experiment as before, using only Bending Stiffness:

Both cubes keep their shape. Now, we try the same thing with subdivided planes, again a quad-based one and a triangulated one:

No bending stiffness.¶

High bending stiffness (10).¶

Without any Bending Stiffness, the faces can rotate freely as though their edges were hinges. Enabling Stiffness to add diagonal springs would not change this (just as triangulating doesn’t).

With a high Bending Stiffness, however, the edges resist this rotation, and the planes act more like planks than towels.

---

## Keyed¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/physics/keyed.html

**Contents:**
- Keyed¶
- Options¶
- Relations¶

Particle System ‣ Physics

The path of Keyed particles is determined between particles of any two (or more) particle systems. This allows the creation of a chains of systems to create long strands or groovy moving particles. Basically the particles have no dynamics but are interpolated from one system to the next each frame.

To setup Keyed particles you need at least two particle systems in the Keys list.

Keyed Physics settings.¶

Sets the number of times the entire Keys list is repeated. Disabled if Use Timing is enabled.

Enabling this option allows you to specify the timing for each key independently, using the Time and Duration options. By default, the Use Timing option is deactivated, and the particles will pass through all keys for a time equal to its lifetime. A shorter lifetime means faster movement. The lifetime will be split equally between the keys, this may lead to varying particle speeds between the targets.

Particle System ‣ Physics ‣ Relations

The list view of keys (target particle systems).

The name of a target object for the selected key. If empty it uses the current particle system.

Index of particle system on the target object.

The time (frame number) at which the particles will be at the position of the selected system. Note also that the Start frame of the Keyed system adds an offset to this time.

How long (in frames) the particles stay on this system before they start moving to the next one.

---

## Newtonian¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/physics/newtonian.html

**Contents:**
- Newtonian¶
- Forces¶
- Integration¶
- Deflection¶

Particle System ‣ Physics

The particles will move according to classical (Newtonian) mechanics. Particles start their life with the specified initial velocities and angular velocities, and move according to external forces. The response to environment and to forces is computed differently, according to the given integrator chosen by the animator.

Newtonian Physics settings.¶

Particle System ‣ Physics ‣ Forces

Specify the amount of Brownian motion. Brownian motion adds random motion to the particles based on a Brownian noise field. This is nice to simulate small, random wind forces.

A force that reduces particle velocity in relation to its speed and size (useful in order to simulate air drag or water drag).

Reduces particle velocity (deceleration, friction, dampening).

Particle System ‣ Physics ‣ Integration

Integrators are a set of mathematical methods available to calculate the movement of particles. The following guidelines will help to choose a proper integrator, according to the behavior aimed at by the animator.

Also known as “Forward Euler”. Simplest integrator. Very fast but also with less exact results. If no dampening is used, particles get more and more energy over time. For example, bouncing particles will bounce higher and higher each time. Should not be confused with “Backward Euler” (not implemented) which has the opposite feature, the energy decrease over time, even with no dampening. Use this integrator for short simulations or simulations with a lot of dampening where speedy calculations are more important than accuracy.

Very fast and stable integrator, energy is conserved over time with very little numerical dissipation.

Also known as “2nd order Runge-Kutta”. Slower than Euler but much more stable. If the acceleration is constant (no drag for example), it is energy conservative. It should be noted that in example of the bouncing particles, the particles might bounce higher than they started once in a while, but this is not a trend. This integrator is a generally good integrator for use in most cases.

Short for “4th order Runge-Kutta”. Similar to Midpoint but slower and in most cases more accurate. It is energy conservative even if the acceleration is not constant. Only needed in complex simulations where Midpoint is found not to be accurate enough.

The amount of simulation time (in seconds) that passes during each frame.

The number of simulation steps per frame. Subframes to simulate for improved stability and finer granularity in simulations. Use higher values for faster-moving particles.

The following options are only available for Fluid type physics:

Automatically set the number of subframes.

A tolerance value that allows the number of subframes to vary. It sets the relative distance a particle can move before requiring more subframes.

The number of steps per frame will be at least Subframes + 1. More subframes may be simulated if the fluid becomes turbulent, according to the Threshold.

Particle System ‣ Physics ‣ Deflection

Use the particle size in deflections.

Kill particle when it hits a deflector object.

If set, particles collide with objects from the collection.

---

## Object¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/settings/object.html

**Contents:**
- Object¶

The friction of the surrounding medium. Generally friction dampens a movement. The larger the friction, the more viscous is the medium. Friction always appears when a vertex moves relative to its surround medium.

Mass value for vertices. Larger mass slows down acceleration, except for gravity where the motion is constant regardless of mass. Larger mass means larger inertia, so also braking a soft body is more difficult.

You can paint weights and use a specified vertex group for mass values.

---

## Particle Edit Mode¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/mode.html

**Contents:**
- Particle Edit Mode¶
- Usage¶
  - Setup for Hair Particles¶
  - Setup for Particle, Cloth, and Soft Body Simulations¶
  - Bake the Simulation¶
  - Edit the Simulation¶
- Selecting¶
  - Select Random¶
  - Select Modes¶
- Tools¶

Using Particle Edit Mode you can edit the keyed points (keyframes) and paths of Hair, Particle, Cloth, and Soft Body simulations. (You can also edit and style hair before baking.)

Since working in Particle Edit Mode is pretty easy and very similar to working with vertices in the 3D Viewport, we will show how to set up a particle system and then give a reference of the various functions.

Particle Edit Mode, specifically for hair is deprecated; please use the new Empty Hair object with its associated Sculpt Mode instead.

Editing a cached cloth simulation is not currently working, see: blender/blender#77114 for details.

Only Frames Baked to Memory are Editable!

If you cannot edit the particles, check that you are not baking to a Disk Cache.

Create a Hair particle system.

Give it an initial velocity in the Normal direction.

Check the Hair Dynamics box.

Editing hair strands in Particle Edit Mode.¶

Use Emitter particles, or a cloth/soft body simulation.

Create a simulation by setting up objects and/or emitters, set your time range (use a small range if you are just starting out and experimenting), set up the simulation how you want it, play the animation to preview it.

Once you are happy with the general simulation, bake the simulation from Object Mode. The simulation must be baked to enable editing.

Switch to Particle Edit from the Mode select menu in the header of the 3D Viewport to edit the particle’s paths/Keyframes. You may need to press T from within the 3D Viewport to see the Particle Edit toolbox. Move to the frame you want to edit and use the various tools to edit your simulation.

Switch to the Point select mode (see below) in the header of the 3D Viewport to be able to see and select the keypoints.

Add to/remove from selection: Shift-LMB.

Lasso Select: Ctrl-Alt-LMB.

Select Linked: Move the mouse over a path and press L to add all its points to the selection.

Unselect Linked: Move the mouse over a path and press Shift-L to remove all its points from the selection.

Root/Tips: Select ‣ Roots / Tips.

Randomly selects particles.

Percent of particles to randomly select.

Seed value to use for the selection.

Select random can be either used to select or deselect particles.

Selects either hair or points. Here these terms can be confusing because hair/point does not refer to the particle type but the path/points of the hair/particle.

No keypoints are visible, you can select/deselect only all particles.

You see all of the keypoints.

You can see and edit (including the brushes) only the tip of the particles, i.e. the last keypoint.

Moves the keypoints (similar to the Proportional Editing tool).

Hair particles only – Do not move keypoints through the emitting mesh.

The distance to keep from the Emitter.

Parallels visually adjacent segments.

The number of new particles per step.

Interpolate the shape of new hairs from existing ones.

Amount of brush steps.

How many keys to make new particles with.

Scales the segments, so it makes the hair longer with Grow or shorter with Shrink.

Sets the brush to add the effect or reverse it.

Rotates the hair around its first keypoint (root). So it makes the hair stand up with Add or lay down with Sub.

Apply puff to unselected end points, (Helps to maintain the hair volume when puffing the root.)

Scales the segments until the last keypoint reaches the brush.

This is especially useful for soft body animations, because the weight defines the soft body Goal. A keypoint with a weight of 1 will not move at all, a keypoint with a weight of 0 subjects fully to soft body animation. This value is scaled by the Strength Min to Max range of soft body goals…

Below the brush types, their settings appear:

Set the radius of the brush.

Set the strength of the brush effect (not for Add brush).

Tool Settings ‣ Options

Recalculate velocities of particles according to their edited paths. Otherwise, the original velocities values remains unchanged regardless of the actual distance that the particles moves.

Enable mirror editing across the local X axis.

Keep the length of the segments between the keypoints when combing or smoothing the hair. This is done by moving all the other keypoints.

Keep first key unmodified, so you cannot transplant hair.

A mesh object which boundary is used by the Shape Cut tool.

This grooming tool trims hairs to a shape defined by the Shape Object. This is a quicker way of avoiding protruding hair sections from lengthening than using the Cutting tool. It works especially well for characters with extensive fur, where working in a single plane with the Cutting tool becomes tedious.

The number of steps used to draw the path; improves the smoothness of the particle path.

Displays the children of the particles too. This allows to fine-tune the particles and see their effects on the result, but it may slow down your system if you have many children.

Displays the actual particles on top of the paths.

Fade out paths and keys further away from current time.

How many frames to fade.

To move selected keypoints press G, or use one of the various other methods to move vertices.

To move a particle root you have to turn off Keep Root in the Toolbar.

You can do many of the things like with vertices, including scaling, rotating and removing (complete particles or single keys).

You may not duplicate or extrude keys or particles, but you can subdivide particles which adds new keypoints Particle ‣ Subdivide.

Alternatively you can re-key a particle Particle ‣ Rekey.

How smoothly the hair and particle paths are displayed depends on the Path Steps setting in the Toolbar. Low settings produce blocky interpolation between points, while high settings produce a smooth curve.

If you want to create an X axis symmetrical haircut you have to do following steps:

Select all particles with A.

Mirror the particles with Particle ‣ Mirror.

Turn on X Mirror in Sidebar Region ‣ Tool ‣ Options.

It may happen that after mirroring two particles occupy nearly the same place. Since this would be a waste of memory and render time, you can use Merge by Distance from the Particle menu.

Particle ‣ Unify Length

This tool is used to make all selected hair uniform length by finding the average length.

Hiding and unhiding of particles works similar as with vertices in the 3D Viewport. Select one or more keypoints of the particle you want to hide and press H. The particle in fact does not vanish, only the key points.

Hidden particles (i.e. particles whose keypoints are hidden) do not react on the various brushes. But:

If you use Mirror Editing even particles with hidden keypoints may be moved, if their mirrored counterpart is moved.

To unhide all hidden particles press Alt-H.

---

## Particle System Panel¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/particle_system_panel.html

**Contents:**
- Particle System Panel¶
- Workflow¶
  - Creating a Particle System¶
    - Types of Particle Systems¶

Particle System ‣ Particle System

Particle System panel.¶

These are the basic settings.

The List View of the objects Particle Modifier(s).

Copies the active particle system to all selected objects.

Copies all particle systems from the active object to all selected objects.

Duplicates the particle system within the active object. The Duplicate Settings option (in the Adjust Last Operation panel) will duplicate settings as well, so the new particle system uses its own settings.

Remove all particle system within the active object.

The Data-Block menu for settings.

Main selector of the system type.

In such a system, particles are emitted from the object.

Use Hair type, rendered as strands.

Regrows the hair for each frame. This is useful when you are animating properties.

Enables advanced settings which reflect the same ones as working in Emitter mode.

This manual assumes that this option is enabled.

Controls the number of parts a hair is made of. Increasing this value will improve the quality of animations.

The process for working with standard particles is:

Create the mesh which will emit the particles.

Create one or more Particle Systems to emit from the mesh. Many times, multiple particle systems interact or merge with each other to achieve the overall desired effect.

Tailor each Particle System’s settings to achieve the desired effect.

Animate the base mesh and other particle meshes involved in the scene.

Define and shape the path and flow of the particles.

For Hair particle systems: Sculpt the emitter’s flow (cut the hair to length and comb it for example).

Make final render and do physics simulation(s), and tweak as needed.

Adding a particle system.¶

To add a new particle system to an object, go to the Particles tab of the Properties editor and click the button. An object can have many Particle Systems.

Each particle system has separate settings attached to it. These settings can be shared among different particle systems, so one does not have to copy every setting manually and can use the same effect on multiple objects.

Particle System Types.¶

After you have created a particle system, the Properties fills with many panels and buttons. But do not panic! There are two different types of particle systems, and you can change between these two with the Type selector: Emitter and Hair.

The settings in the Particle System tab are partially different for each system type.

---

## Physical Properties¶

**URL:** https://docs.blender.org/manual/en/latest/physics/cloth/settings/physical_properties.html

**Contents:**
- Physical Properties¶
- Stiffness¶
- Damping¶
- Internal Springs¶
- Pressure¶

Physics ‣ Cloth ‣ Physical Properties

The mass of the cloth material.

Air has some thickness which slows falling things down.

Cloth model with linear bending springs (old).

Cloth model with angular bending springs.

How much the material resists stretching.

How much the material resists compression.

Overall stiffness of the cloth (only in linear bending model).

How much the material resists shearing.

Wrinkle coefficient. Higher creates more large folds.

Amount of damping in stretching behavior.

Amount of damping in compression behavior.

Amount of damping in stretching behavior (only in linear bending model).

Amount of damping in shearing behavior.

Amount of damping in bending behavior.

As stated in the introduction, cloth physics are simulated through Springs connecting vertices on the surface of a mesh. But these springs only interact on the surface and only apply to 2D surfaces. 3D or Internal Springs can be used to make a mesh behave similarly to a Soft Body. Internal springs can be enabled by toggling the checkbox in the Internal Springs panel header.

The maximum length an internal spring can have during creation. If the distance between internal points is greater than this, no internal spring will be created between these points. A length of zero means that there is no length limit.

The maximum angle that is allowed to use to connect the internal points can diverge from the vertex normal.

Requires the points the internal springs connect to have opposite normal directions.

How much the material resists stretching.

How much the material resists compression.

The Tension and Compression of internal springs can be controlled via a Vertex Group to specify which the portions of the mesh have internal springs or the spring strength.

Maximum tension stiffness value.

Maximum Compression stiffness value.

Cloth pressure allows the simulation of soft-shelled objects such as balloons or balls that are filled with a type of fluid. This fluid is modeled as a gas; to emulate an incompressible liquid set Pressure Scale as high as possible without breaking the simulation. Cloth pressure can be enabled by toggling the checkbox in the Pressure panel header.

Non-manifold meshes will work with cloth pressure however, pressure will escape out of the mesh holes and cause drifting or propulsion forces. One way to get around this is by using the Vertex Group to exclude the non-manifold portions of the mesh.

The uniform pressure that is constantly applied to the mesh. This value is specified in units of Pressure Scale, and can be negative to simulate implosions or any other case where an object has outside pressure pushing inwards.

Use the Target Volume parameter as the initial volume for the cloth, instead of computing it from the mesh itself.

The mesh volume where the inner/outer pressure will be the same. If set to zero, changes in the volume of the object will not affect pressure.

Ambient pressure (in kPa) that exists both inside and outside the object, balancing out when the volume matches the target. Increase the value to make the object resist changes in volume more strongly.

Specifies the density of the fluid contained inside the object (in kg/liter = 1000 kg/m3, use 1 for water), used to generate a hydrostatic pressure gradient that simulates the weight of the fluid. If the value is negative, it instead models buoyancy from a surrounding fluid.

The fluid is not actually simulated, so while the setting helps to achieve a more plausible object shapes at rest, it cannot create realistic fluid dynamics effects. It can also be used to give more weight to a soft body like object with heavy and sufficiently flexible filling, even if it is not a fluid by itself.

The volume of the object is not preserved. If that is desired it should be used together with Pressure Scale. Fluid density times object size times 50 is a good start value for Scale to make sure that no more than 10% volume change if the object does not experience higher acceleration than standard gravity.

Cloth pressure can be controlled via a Vertex Group to specify which the portions of the mesh to apply pressure. Zero weight means no pressure while a weight of one means full pressure.

Note, faces with a vertex that has zero weight will be excluded from the Target Volume calculation.

---

## Property Weights¶

**URL:** https://docs.blender.org/manual/en/latest/physics/cloth/settings/property_weights.html

**Contents:**
- Property Weights¶

Physics ‣ Cloth ‣ Property Weights

This panel is used to constrain certain cloth properties to a certain vertex group. The properties that they control can be found in a combination of the Physical Properties and Shape panels.

Defines a vertex group to control over structural stiffness.

Maximum tension stiffness value.

Maximum Compression stiffness value.

Vertex group for fine control over shear stiffness.

Maximum shear scaling value.

Vertex group for fine control over bending stiffness.

Maximum bending stiffness value.

Vertex group for shrinking cloth.

Max amount to shrink cloth by, specifying a negative value controls the max amount for the cloth to grow.

---

## Render¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/render.html

**Contents:**
- Render¶
- Common Settings¶
- Render As¶
  - None¶
  - Halo¶
  - Path¶
  - Timing¶
  - Object¶
  - Collection¶
    - Use Count¶

Particle System ‣ Render

The Render Panel controls how particles appear when they are rendered.

Cycles supports only Object and Collection render types.

Set which of the object’s materials is used to shade the particles.

Use a different object’s coordinates to determine the birth of particles.

When disabled, the emitter is no longer rendered. Activate the button Emitter to also render the mesh.

When set to None, particles are not rendered. This is useful if you are using the particles to duplicate objects.

Halos are rendered as glowing dots or a little cloud of light. Although they are not really lights because they do not cast light into the scene like a light object. They are called Halos because you can see them, but they do not have any substance.

The Visualization panel for Path visualization.¶

The Path visualization needs a Hair particle system or Keyed particles.

Interpolate hair using B-splines. This may be an option for you if you want to use low Render values. You loose a bit of control but gain smoother paths.

Set the number of subdivisions of the rendered paths (the value is a power of 2). You should set this value carefully, because if you increase the render value by two you need four times more memory to render. Also the rendering is faster if you use low render values (sometimes drastically). But how low you can go with this value depends on the waviness of the hair (the value is a power of 2). This means 0 steps give 1 subdivision, 1 give 2 subdivisions, 2 → 4, 3 → 8, 4 → 16, … 𝓃 → 2𝓃.

Particle System ‣ Render ‣ Timing

Path timing is in absolute frames.

End time of the practical path.

Give the path length a random variation.

Particle System ‣ Render ‣ Object

The specified object is instanced in place of each particle.

Use object’s global coordinates for instancing.

Use the rotation of the object.

Use the size of the object.

Particle System ‣ Render ‣ Collection

The objects that belong to a collection are instanced sequentially in the place of the particles.

Use the whole group at once, instead of one of its elements, the group being displayed in place of each particle.

The objects in the group are selected in a random order, and only one object is displayed in place of a particle.

Use object’s global coordinates for instancing.

Use the rotation of the objects.

Use the size of the objects.

Particle System ‣ Render ‣ Collection ‣ Use Count

Use objects multiple times in the same groups. Specify the order and number of times to repeat each object with the list view that appears.

Duplicates the selected object in the list.

Removes the selected object from the list.

Particle System ‣ Render ‣ Extra

Render also parent particles if child particles are used. Children have a lot of different deformation options, so the straight parents would stand between their curly children. So by default Parents are not rendered if you activate Children. See Children.

Render particles before they are born.

Render particles after they have died. This is very useful if particles die in a collision Die on hit, so you can cover objects with particles.

---

## Render¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/hair/render.html

**Contents:**
- Render¶

Particle System ‣ Render

Hair can be rendered as a Path, Object, or Group. See Particle Visualization for descriptions and the Hair Shape settings.

Blender Hair Basics, a thorough overview of all of the hair particle settings.

---

## Rigid Body¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/object/editing/rigid_body.html

**Contents:**
- Rigid Body¶
- Calculate Mass¶

Object ‣ Rigid Body ‣ Calculate Mass

Calculate mass values for rigid body objects based on their volume and density. The volume is calculated automatically, the density needs to be given based on the object you want to simulate.

A list of preset density values for real-world materials, if a material is not given you can research the density and use the Custom preset to input the density manually.

When the Custom Material Preset is selected, this is the input density, in kg/m3, to use.

---

## Rigid Body Properties¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/properties/index.html

**Contents:**
- Rigid Body Properties¶

Role of the rigid body in the simulation.

The object is dynamic and is directly controlled by simulation results.

The object remains static and is directly controlled by animation system, thus does not have Dynamics properties.

---

## Rigid Body World¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/world.html

**Contents:**
- Rigid Body World¶
- Settings¶
- Rigid Body Cache¶
- Rigid Body Field Weights¶

Scene ‣ Rigid Body World

The Rigid Body World is a group of rigid body objects, which holds settings that apply to all rigid bodies in this simulation.

When you add rigid body physics to an object, primary there is created a group of objects with default “RigidBodyWorld” name. Rigid body objects automatically are added to this group when you add rigid body physics for them. You can create several Rigid Body World Collections and allocate the rigid body objects with the Collections panel.

Rigid body objects and constraints are only taken into account by the simulation if they are in the collection specified in the Collection field of the Rigid Body World panel in the Scene tab.

Enable/disable evaluation of the rigid body simulation based on the rigid body objects participating in the specified group of Rigid Body World.

Remove rigid body simulation from the current scene.

Containing rigid body objects participating in this simulation.

Containing rigid body object constraints participating in the simulation.

Simulation quality and timing settings:

Can be used to speed up/slow down the simulation.

Enable/disable reducing extra velocity that can build up when objects collide (lowers the simulation stability a little so use only when necessary). Limits the force with which objects are separated on collision, generally produces nicer results, but makes the simulation less stable (especially when stacking many objects).

Number of simulation steps taken per frame (higher values are more accurate but slower). This only influences the accuracy and not the speed of the simulation.

Amount of constraint solver iterations made per simulation step (higher values are more accurate but slower). Increasing this makes constraints and object stacking more stable.

Scene ‣ Rigid Body World ‣ Cache

The Cache subpanel specifies the frame range in which the simulation is active. Can be used to bake the simulation.

First and last frame of the simulation.

Calculates the simulation and protects the cache. You need to be in Object Mode to bake.

Active after the baking of simulation. Clears the baked cache.

Bake physics to current frame.

Deletes all baked caches of all objects in the current scene.

Update cache to current frame.

If you have not saved the blend-file, the cache is created in memory, so save your file first or the cache may be lost.

Scene ‣ Rigid Body World ‣ Field Weights

As other physics dynamics systems, rigid body simulation are also influenced by external force effectors.

---

## Rotation¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/rotation.html

**Contents:**
- Rotation¶
- Angular Velocity¶

Particle System ‣ Rotation

These parameters specify how the individual particles are rotated at the start of, and during, their lifetime. You can visualize their orientation by setting Display As to Axis in the Viewport Display panel.

Aligns the X axis of new particles to:

The emitter’s surface normal.

The emitter’s surface normal, additionally aligning the particle’s Y axis to the positive V direction in the emitter’s active UV map. This makes it possible to deform the emitter while keeping particle rotation consistent.

The particle’s initial velocity vector/hair growth direction.

One of the global axes.

One of the emitter’s local axes.

How much to randomize the particle’s initial rotation (along all axes).

Initial rotation around the particle’s X axis, going from -1 (-180°) to 1 (180°).

Maximum random rotation to add to the Phase, going from 0 (0°) to 2 (360°).

Whether the particles’ rotation can change over time.

Particle System ‣ Rotation ‣ Angular Velocity

Lets you configure if and how particles should spin over time. Dynamic needs to be enabled for this to work.

The axis to spin around. If this is set to Velocity, Horizontal, or Vertical, particles will additionally spin to keep the same orientation relative to their direction of movement, even if Amount is zero.

Spinning is disabled.

Spin around the particle’s velocity vector.

Spin around the axis that’s horizontal (lying in the global XY plane) and perpendicular to the particle’s velocity. Particles moving along the global Z axis won’t spin because no unique rotation axis exists in this case.

Spin around the axis that’s perpendicular to both the particle’s velocity and the above Horizontal axis. Particles moving along the global Z axis won’t spin.

Spin around the chosen global axis.

Spin around a random axis.

If you use a Curve Guide and want the particles to always point in the direction of the curve, you should set the Orientation Axis to Velocity / Hair, enable Dynamic, and set the Angular Velocity Axis to Velocity.

(For a regular object, you’d normally use the Follow Curve option of a Follow Path Constraint or the legacy Follow option of the curve itself, but these don’t work for particles.)

How fast to spin around the Axis.

---

## Scene Properties¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/scene/properties.html

**Contents:**
- Scene Properties¶
- Scene¶
- Units¶
- Gravity¶
- Simulation¶
- Keying Sets¶
- Audio¶
- Rigid Body World¶
- Animation¶
- Custom Properties¶

Properties ‣ Scene ‣ Scene

Used to select which camera is used as the active camera. You can also set the active camera in the 3D Viewport with Ctrl-Numpad0.

Allows you to use a scene as a background, this is typically useful when you want to focus on animating the foreground for example, without background elements getting in the way.

This scene can have its own animation, physics simulations, etc, but you will have to select it from the Scene data-block menu, if you want to edit any of its contents.

Background Scenes can themselves have a Background Scene (they’re recursively included). So you can always make additions to existing scenes by using them as a background to a newly created scene where your additions are made.

This can also be used in combination with Linking to a Scene, where one blend-file contains the environment, which can be reused in many places.

Selects a Movie Clip that can be used by Motion Tracking Constraints or a camera’s Background Images.

Properties ‣ Scene ‣ Units

The unit system to use for user interface controls.

Use units that have with no relation to the real world, practically this is the same as Metric just without unit names.

Use the metric unit system in this scene.

Use the imperial unit system in this scene.

Scale factor to use when converting between internal units and values displayed in the user interface. This can be changed when modeling at microscopic or astronomical scales.

This only influences the values displayed in the user interface and not how things behave internally. For example, physics simulations don’t take the unit scale into account.

When using Metric or Imperial, display properties as multiple values. For example, 2.285m will become 2m 28.5cm.

Unit to use for displaying/editing rotation values.

Use degrees for angles in the user interface.

Use radians for angles in the user interface.

Unit that will be used to display length values.

The unit used for a specific value depends on the magnitude of the value. For example, some values might be displayed as 23cm while others are displayed as 10km.

A fixed unit that will be used for all lengths in the user interface.

Properties ‣ Scene ‣ Gravity

Options to control global gravity used for physics effects.

See the Physics chapter for more information.

Use a simulation range that is different from the scene range for Simulation Nodes that do not override the frame range themselves.

The frame at which the simulation starts/ends.

Properties ‣ Scene ‣ Keying Sets

Properties ‣ Scene ‣ Audio

Options to control global audio settings. To control how sounds is played back from within Blender, see the audio settings in the Preferences.

Volume for the scene.

Changes how the sound attenuation is calculated based on the distance. Most physically correct is the Inverse model, but it’s also possible to choose a linear and an exponential falloff. The clamped modes limit the volume to be lower than 100% (1.0), that means if the distance is smaller than the reference distance, the volume is always 100%. For an exact description of each option see the OpenAL documentation.

Speed of the sound for the Doppler effect calculations. The typical value is 343.3 m/s in air, in water for example this value is around 1560 m/s.

Controls how strong the Doppler effect is. You can exaggerate or attenuate the change of pitch, but physically correct is a factor of 1.0.

Updates the audio animation cache. This is useful if you start noticing artifact in the audio.

Properties ‣ Scene ‣ Rigid Body World

The Rigid Body World is a group of rigid body objects, which holds settings that apply to all rigid bodies in this simulation.

See Rigid Body World for more information.

Properties ‣ Scene ‣ Animation

Controls animation data for scene-level properties, including active Actions and their assigned Slot.

See Manually Assigning Actions and Slots for more information.

Specifies the action and slot where animation data for scene properties is stored/retrieved.

Create and manage your own properties to store data in the scene’s data block. See the Custom Properties page for more information.

---

## Self Collision¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/settings/self_collision.html

**Contents:**
- Self Collision¶

Physics ‣ Soft Body ‣ Self Collision

Self-Collision is working only if you have activated Use Edges.

When enabled, allows you to control how Blender will prevent the soft body from intersecting with itself. Every vertex is surrounded with an elastic virtual ball. Vertices may not penetrate the balls of other vertices. If you want a good result you may have to adjust the size of these balls. Normally it works pretty well with the default options.

The Ball Size directly sets the ball size.

The average length of all edges attached to the vertex is calculated and then multiplied with the Ball Size setting. Works well with evenly distributed vertices.

The ball size is as large as the smallest/largest spring length of the vertex multiplied with the Ball Size.

Size = ((Min + Max)/2) × Ball Size.

Fraction of the length of attached edges. The edge length is computed based on the chosen algorithm. This setting is the factor that is multiplied by the spring length. It is a spherical distance (radius) within which, if another vertex of the same mesh enters, the vertex starts to deflect in order to avoid a self-collision.

Set this value to the fractional distance between vertices that you want them to have their own “space”. Too high of a value will include too many vertices at all times and slow down the calculation. Too low of a level will let other vertices get too close and thus possibly intersect because there will not be enough time to slow them down.

How elastic that ball of personal space is. A high stiffness means that the vertex reacts immediately to another vertex enters their space.

How the vertex reacts. A low value just slows down the vertex as it gets too close. A high value repulses it.

Collisions with other objects are set in the (other) Collision panel. To collide with another object they have to share at least one common layer.

---

## Settings¶

**URL:** https://docs.blender.org/manual/en/latest/physics/cloth/settings/index.html

**Contents:**
- Settings¶

Contains a number of preset cloth examples.

Set the number of simulation steps per frame. Higher values result in better quality, but will be slower.

Adjust how fast time progresses in the cloth simulation.

---

## Settings¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/properties/settings.html

**Contents:**
- Settings¶

Physics ‣ Rigid Body ‣ Settings

Default rigid body panel.¶

Specifies how heavy the object is and “weights” irrespective of gravity.

There are predefined mass presets available with the Calculate Mass operator.

Enables/disables rigid body simulation for the object.

Allows the rigid body to additionally be controlled by the animation system.

---

## Settings¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/settings/index.html

**Contents:**
- Settings¶

If set, soft body collides with objects from the collection, instead of using objects that are on the same layer.

---

## Shape¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/hair/shape.html

**Contents:**
- Shape¶

Particle System ‣ Hair Shape

These settings control the shape of hair curves for rendering.

A shape parameter that controls the transition in thickness between the root and tip. Negative values make the primitive rounded more towards the top, the value of zero makes the primitive linear, and positive values make the primitive rounded more towards the bottom.

Multiplier of the hair width at the root.

Multiplier of the hair width at the tip.

Multiplier for the Root and Tip values. This can be used to change the thickness of the hair.

Sets the thickness at the tip to zero, even when using a nonzero tip multiplier.

---

## Shape¶

**URL:** https://docs.blender.org/manual/en/latest/physics/cloth/settings/shape.html

**Contents:**
- Shape¶

Physics ‣ Cloth ‣ Shape

Vertex group to use for pinning.

The shape of the cloth can be controlled by pinning cloth to a Vertex Group. There are several ways of doing this including Weight Painting areas you want to pin. The weight of each vertex in the group controls how strongly it is pinned.

Target position stiffness.

Another method of restraining cloth similar to pinning is sewing springs. Sewing springs are virtual springs that pull vertices in one part of a cloth mesh toward vertices in another part of the cloth mesh. This is different from pinning which binds vertices of the cloth mesh in place or to another object. A clasp on a cloak could be created with a sewing spring. The spring could pull two corners of a cloak about a character’s neck. This could result in a more realistic simulation than pinning the cloak to the character’s neck since the cloak would be free to slide about the character’s neck and shoulders.

Sewing springs are created by adding extra edges to a cloth mesh that are not included in any faces. They should connect vertices in the mesh that should be pulled together. For example the corners of a cloak.

Maximum force that can be applied by sewing springs. Zero means unbounded, but it is not recommended to leave the field at zero in most cases, as it can cause instability due to extreme forces in the initial frames where the ends of the sewing springs are far apart.

Factor by which to shrink the cloth, specifying a negative value controls the amount for the cloth to grow.

Allows animating the rest shape of cloth using shape keys or modifiers (e.g. an Armature modifier or any deformation modifier) placed above the Cloth modifier. When it is enabled, the rest shape is recalculated every frame, allowing unpinned cloth to squash and stretch following the character with the help of shape keys or modifiers, but otherwise move freely under control of the physics simulation.

Normally cloth uses the state of the object in the first frame to compute the natural rest shape of the cloth, and keeps that constant throughout the simulation. This is reasonable for fully realistic scenes, but does not quite work for clothing on cartoon style characters that use a lot of squash and stretch.

Allows starting the cloth simulation using a specific Shape Key as the rest state, instead of the shape that results from evaluating shape keys and preceding modifiers in the regular way. This option is mutually exclusive with Dynamic Mesh.

This can be used to start the simulation with the cloth in a pre-draped state without applying that shape as a plastic deformation that relaxes all springs as a side effect.

This property is only visible if the mesh has shape keys.

---

## Simulation¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/settings/simulation.html

**Contents:**
- Simulation¶

You can control the internal timing of the soft body system with this value. It sets the correlation between frame rate and tempo of the simulation. A free falling body should cover a distance of about five meters after one second and travel at a speed of ten meters per seconds.

You can adjust the scale of your scene and simulation with this correlation. If you render with 25 frames per second, you will have to set Speed to 1.3.

---

## Solver¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/settings/solver.html

**Contents:**
- Solver¶
- Diagnostics¶
- Helpers¶

Physics ‣ Soft Body ‣ Solver

The settings in the Soft Body Solver panel determine the accuracy of the simulation.

Minimum simulation steps per frame. Increase this value, if the soft body misses fast-moving collision objects.

Maximum simulation steps per frame. Normally the number of simulation steps is set dynamically (with the Error Limit) but you have probably a good reason to change it.

Use velocities for automatic step sizes. Helps the Solver figure out how much work it needs to do based on how fast things are moving.

Rules the overall quality of the solution delivered. The most critical setting that defines how precise the solver should check for collisions. Start with a value that is half the average edge length. If there are visible errors, jitter, or over-exaggerated responses, decrease the value. The solver keeps track of how “bad” it is doing and the Error Limit causes the solver to do some “adaptive step sizing”.

Prints on the console how the solver is doing.

Estimate matrix, split to COM, ROT, SCALE.

These settings control how the soft body will react (deform) once it either gets close to or actually intersects (cuts into) another collision object on the same layer.

Calms down (reduces the exit velocity of) a vertex or edge once it penetrates a collision mesh.

Fuzziness while on collision, high values make collision handling faster but less stable. Simulation is faster, but less accurate.

---

## Velocity¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/velocity.html

**Contents:**
- Velocity¶

Particle System ‣ Velocity

The initial velocity of particles can be set through different parameters, based on the type of the particle system. If the particle system type is Emitter or Hair, then the following parameters give the particle an initial velocity.

The emitter’s surface normals (i.e. let the surface normal give the particle a starting speed).

Let the tangent speed give the particle a starting speed.

Rotates the surface tangent.

Give an initial velocity in the X, Y, and Z axes.

The emitter objects movement (i.e. let the object give the particle a starting speed).

Gives the starting speed a random variation. You can use a texture to only change the value, see Controlling Emission, Interaction and Time.

---

## Vertex Groups¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/vertex_groups.html

**Contents:**
- Vertex Groups¶

Particle System ‣ Vertex Groups

The Vertex groups panel allows you to specify vertex groups to use for several child particle settings. You can also negate the effect of each vertex group with the checkboxes. You can affect the following attributes:

Defines the density of the particle distribution.

Defines the length of the hair.

Controls the amount of clumping. The weight of 1.0 gives current Clump value, weight of 0.0 completely removes effect.

Controls the frequency of the children Kink.

Adjusts the Uniform roughness parameter.

Adjusts the Random roughness parameter.

Adjusts the Endpoint roughness parameter.

Vertex group to control the children’s Twist effect. Gives control over the direction of the twist, as well as the amount. The weight of 0.5 is neutral, i.e. there is no twist effect.

---

## Viewport Display¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/display.html

**Contents:**
- Viewport Display¶

Particle System ‣ Viewport Display

The Display Panel controls how particles are displayed in the 3D Viewport. This does not necessarily determine how they will appear when rendered.

The particles are not shown in the 3D Viewport and are not rendered. The emitter may be rendered though.

Particles are displayed the way they are rendered.

Particles are displayed as square points. Their size is independent of the distance from the camera.

Particles are displayed as circles that face the view. Their size is independent of the distance from the camera.

Particles are displayed as 6-point crosses that align to the rotation of the particles. Their size is independent of the distance from the camera.

Particles are displayed as 3-point axes. This is useful if you want to see the orientation and rotation of particles in the viewport. Increase the Display Size until you can clearly distinguish the axis.

Particles visualized like Point, Circle, Cross and Axis do not have any special options, but can be very useful when you have multiple particle systems at play, if you do not want to confuse particles of one system from another (e.g. in simulations using Boids physics).

The Color Menu allows you to display particle’s color according to certain particle properties.

Particles are colored according to the material they are given.

Color particles according to their speed. The color is a ramp from blue to green to red, Blue being the slowest, and Red being velocities approaching the value of Max or above. Increasing Max allows for a wider range of particle velocities.

Color particles according to their acceleration.

Specifies the percentage of all particles to show in the viewport (all particles are still rendered).

Make instancer visible in viewport.

---

## Viewport Display¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/hair/display.html

**Contents:**
- Viewport Display¶

Particle System ‣ Display

Display hair as curves.

Display just the end points of the hairs.

The number of segments (control points minus 1) of the hair strand. In between the control points the segments are interpolated. The number of control points is important:

For the soft body animation, because the control points are animated like vertices, so more control points mean longer calculation times.

For the interactive editing, because you can only move the control points (but you may recalculate the number of control points in Particle Edit Mode).

Ten Segments should be sufficient even for very long hair, five Segments are enough for shorter hair, and two or three segments should be enough for short fur.

---
