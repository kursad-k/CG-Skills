# Godot - Core Concepts

**Pages:** 52

---

## 2D antialiasing

**URL:** https://docs.godotengine.org/en/stable/tutorials/2d/2d_antialiasing.html

**Contents:**
- 2D antialiasing
- Introduction
- Antialiasing property in Line2D and custom drawing
- Multisample antialiasing (MSAA)
- User-contributed notes

Godot also supports antialiasing in 3D rendering. This is covered on the 3D antialiasing page.

Due to their limited resolution, scenes rendered in 2D can exhibit aliasing artifacts. These artifacts usually manifest in the form of a "staircase" effect on geometry edges, and are most noticeable when using nodes such as Line2D, Polygon2D or TextureProgressBar. Custom drawing in 2D can also have aliasing artifacts for methods that don't support antialiasing.

In the example below, you can notice how edges have a blocky appearance:

Image is scaled by 2× with nearest-neighbor filtering to make aliasing more noticeable.

To combat this, Godot supports several methods of enabling antialiasing on 2D rendering.

This is the recommended method, as it has a lower performance impact in most cases.

Line2D has an Antialiased property which you can enable in the inspector. Also, several methods for Custom drawing in 2D support an optional antialiased parameter, which can be set to true when calling the function.

These methods do not require MSAA to be enabled, which makes their baseline performance cost low. In other words, there is no permanent added cost if you're not drawing any antialiased geometry at some point.

The downside of these antialiasing methods is that they work by generating additional geometry. If you're generating complex 2D geometry that's updated every frame, this may be a bottleneck. Also, Polygon2D, TextureProgressBar, and several custom drawing methods don't feature an antialiased property. For these nodes, you can use 2D multisample antialiasing instead.

This is only available in the Forward+ and Mobile renderers, not the Compatibility renderer.

Before enabling MSAA in 2D, it's important to understand what MSAA will operate on. MSAA in 2D follows similar restrictions as in 3D. While it does not introduce any blurriness, its scope of application is limited. The main applications of 2D MSAA are:

Geometry edges, such as line and polygon drawing.

Sprite edges only for pixels touching one of the texture's edges. This works for both linear and nearest-neighbor filtering. Sprite edges created using transparency on the image are not affected by MSAA.

The downside of MSAA is that it only operates on edges. This is because MSAA increases the number of coverage samples, but not the number of color samples. However, since the number of color samples did not increase, fragment shaders are still run for each pixel only once. As a result, MSAA will not affect the following kinds of aliasing in any way:

Aliasing within nearest-neighbor filtered textures (pixel art).

Aliasing caused by custom 2D shaders.

Specular aliasing when using Light2D.

Aliasing in font rendering.

MSAA can be enabled in the Project Settings by changing the value of the Rendering > Anti Aliasing > Quality > MSAA 2D setting. It's important to change the value of the MSAA 2D setting and not MSAA 3D, as these are entirely separate settings.

Comparison between no antialiasing (left) and various MSAA levels (right). The top-left corner contains a Line2D node, the top-right corner contains 2 TextureProgressBar nodes. The bottom contains 8 pixel art sprites, with 4 of them touching the edges (green background) and 4 of them not touching the edges (Godot logo):

Please read the User-contributed notes policy before submitting a comment.

---

## 2D lights and shadows

**URL:** https://docs.godotengine.org/en/stable/tutorials/2d/2d_lights_and_shadows.html

**Contents:**
- 2D lights and shadows
- Introduction
- Nodes
- Point lights
- Directional light
- Common light properties
- Setting up shadows
  - Automatically generating a light occluder
  - Manually drawing a light occluder
- Normal and specular maps

By default, 2D scenes in Godot are unshaded, with no lights and shadows visible. While this is fast to render, unshaded scenes can look bland. Godot provides the ability to use real-time 2D lighting and shadows, which can greatly enhance the sense of depth in your project.

No 2D lights or shadows, scene is unshaded

2D lights enabled (without shadows)

2D lights and shadows enabled

There are several nodes involved in a complete 2D lighting setup:

CanvasModulate (to darken the rest of the scene)

PointLight2D (for omnidirectional or spot lights)

DirectionalLight2D (for sunlight or moonlight)

LightOccluder2D (for light shadow casters)

Other 2D nodes that receive lighting, such as Sprite2D or TileMapLayer.

CanvasModulate is used to darken the scene by specifying a color that will act as the base "ambient" color. This is the final lighting color in areas that are not reached by any 2D light. Without a CanvasModulate node, the final scene would look too bright as 2D lights would only brighten the existing unshaded appearance (which appears fully lit).

Sprite2Ds are used to display the textures for the light blobs, the background, and for the shadow casters.

PointLight2Ds are used to light the scene. The way a light typically works is by adding a selected texture over the rest of the scene to simulate lighting.

LightOccluder2Ds are used to tell the shader which parts of the scene cast shadows. These occluders can be placed as independent nodes or can be part of a TileMapLayer node.

The shadows appear only on areas covered by the PointLight2D and their direction is based on the center of the Light.

The background color does not receive any lighting. If you want light to be cast on the background, you need to add a visual representation for the background, such as a Sprite2D.

The Sprite2D's Region properties can be helpful to quickly create a repeating background texture, but remember to also set Texture > Repeat to Enabled in the Sprite2D's properties.

Point lights (also called positional lights) are the most common element in 2D lighting. Point lights can be used to represent light from torches, fire, projectiles, etc.

PointLight2D offers the following properties to tweak in the inspector:

Texture: The texture to use as a light source. The texture's size determines the size of the light. The texture may have an alpha channel, which is useful when using Light2D's Mix blend mode, but it is not required if using the Add (default) or Subtract blend modes.

Offset: The offset for the light texture. Unlike when you move the light node, changing the offset does not cause shadows to move.

Texture Scale: The multiplier for the light's size. Higher values will make the light extend out further. Larger lights have a higher performance cost as they affect more pixels on screen, so consider this before increasing a light's size.

Height: The light's virtual height with regards to normal mapping. By default, the light is very close to surfaces receiving lights. This will make lighting hardly visible if normal mapping is used, so consider increasing this value. Adjusting the light's height only makes a visible difference on surfaces that use normal mapping.

If you don't have a pre-made texture to use in a light, you can use this "neutral" point light texture (right-click > Save Image As…):

Neutral point light texture

If you need different falloff, you can procedurally create a texture by assigning a New GradientTexture2D on the light's Texture property. After creating the resource, expand its Fill section and set the fill mode to Radial. You will then have to adjust the gradient itself to start from opaque white to transparent white, and move its starting location to be in the center.

New in Godot 4.0 is the ability to have directional lighting in 2D. Directional lighting is used to represent sunlight or moonlight. Light rays are casted parallel to each other, as if the sun or moon was infinitely far away from the surface that is receiving the light.

DirectionalLight2D offers the following properties:

Height: The light's virtual height with regards to normal mapping (0.0 = parallel to surfaces, 1.0 = perpendicular to surfaces). By default, the light is fully parallel with the surfaces receiving lights. This will make lighting hardly visible if normal mapping is used, so consider increasing this value. Adjusting the light's height only makes a visual difference on surfaces that use normal mapping. Height does not affect shadows' appearance.

Max Distance: The maximum distance from the camera center objects can be before their shadows are culled (in pixels). Decreasing this value can prevent objects located outside the camera from casting shadows (while also improving performance). Camera2D zoom is not taken into account by Max Distance, which means that at higher zoom values, shadows will appear to fade out sooner when zooming onto a given point.

Directional shadows will always appear to be infinitely long, regardless of the value of the Height property. This is a limitation of the shadow rendering method used for 2D lights in Godot.

To have directional shadows that are not infinitely long, you should disable shadows in the DirectionalLight2D and use a custom shader that reads from the 2D signed distance field instead. This distance field is automatically generated from LightOccluder2D nodes present in the scene.

Both PointLight2D and DirectionalLight2D offer common properties, which are part of the Light2D base class:

Enabled: Allows toggling the light's visibility. Unlike hiding the light node, disabling this property will not hide the light's children.

Editor Only: If enabled, the light is only visible within the editor. It will be automatically disabled in the running project.

Color: The light's color.

Energy: The light's intensity multiplier. Higher values result in a brighter light.

Blend Mode: The blending formula used for light computations. The default Add is suited for most use cases. Subtract can be used for negative lights, which are not physically accurate but can be used for special effects. The Mix blend mode mixes the value of pixels corresponding to the light's texture with the values of pixels under it by linear interpolation.

Range > Z Min: The lowest Z index affected by the light.

Range > Z Max: The highest Z index affected by the light.

Range > Layer Min: The lowest visual layer affected by the light.

Range > Layer Max: The highest visual layer affected by the light.

Range > Item Cull Mask: Controls which nodes receive light from this node, depending on the other nodes' enabled visual layers Occluder Light Mask. This can be used to prevent certain objects from receiving light.

After enabling the Shadow > Enabled property on a PointLight2D or DirectionalLight2D node, you will not see any visual difference initially. This is because no nodes in your scene have any occluders yet, which are used as a basis for shadow casting.

For shadows to appear in the scene, LightOccluder2D nodes must be added to the scene. These nodes must also have occluder polygons that are designed to match the sprite's outline.

Along with their polygon resource (which must be set to have any visual effect), LightOccluder2D nodes have 2 properties:

SDF Collision: If enabled, the occluder will be part of a real-time generated signed distance field that can be used in custom shaders. When not using custom shaders that read from this SDF, enabling this makes no visual difference and has no performance cost, so this is enabled by default for convenience.

Occluder Light Mask: This is used in tandem with PointLight2D and DirectionalLight2D's Shadow > Item Cull Mask property to control which objects cast shadows for each light. This can be used to prevent specific objects from casting shadows.

There are two ways to create light occluders:

Occluders can be created automatically from Sprite2D nodes by selecting the node, clicking the Sprite2D menu at the top of the 2D editor then choosing Create LightOccluder2D Sibling.

In the dialog that appears, an outline will surround your sprite's edges. If the outline matches the sprite's edges closely, you can click OK. If the outline is too far away from the sprite's edges (or is "eating" into the sprite's edges), adjust Grow (pixels) and Shrink (pixels), then click Update Preview. Repeat this operation until you get satisfactory results.

Create a LightOccluder2D node, then select the node and click the "+" button at the top of the 2D editor. When asked to create a polygon resource, answer Yes. You can then start drawing an occluder polygon by clicking to create new points. You can remove existing points by right-clicking them, and you can create new points from the existing line by clicking on the line then dragging.

The following properties can be adjusted on 2D lights that have shadows enabled:

Color: The color of shaded areas. By default, shaded areas are fully black, but this can be changed for artistic purposes. The color's alpha channel controls how much the shadow is tinted by the specified color.

Filter: The filter mode to use for shadows. The default None is the fastest to render, and is well suited for games with a pixel art aesthetic (due to its "blocky" visuals). If you want a soft shadow, use PCF5 instead. PCF13 is even softer, but is the most demanding to render. PCF13 should only be used for a few lights at once due to its high rendering cost.

Filter Smooth: Controls how much softening is applied to shadows when Filter is set to PCF5 or PCF13. Higher values result in a softer shadow, but may cause banding artifacts to be visible (especially with PCF5).

Item Cull Mask: Controls which LightOccluder2D nodes cast shadows, depending on their respective Occluder Light Mask properties.

Soft shadows (PCF13, Filter Smooth 1.5)

Soft shadows with streaking artifacts due to Filter Smooth being too high (PCF5, Filter Smooth 4)

Normal maps and specular maps can greatly enhance the sense of depth of your 2D lighting. Similar to how these work in 3D rendering, normal maps can help make lighting look less flat by varying its intensity depending on the direction of the surface receiving light (on a per-pixel basis). Specular maps further help improve visuals by making some of the light reflect back to the viewer.

Both PointLight2D and DirectionalLight2D support normal mapping and specular mapping. Since Godot 4.0, normal and specular maps can be assigned to any 2D element, including nodes that inherit from Node2D or Control.

A normal map represents the direction in which each pixel is "pointing" towards. This information is then used by the engine to correctly apply lighting to 2D surfaces in a physically plausible way. Normal maps are typically created from hand-painted height maps, but they can also be automatically generated from other textures.

A specular map defines how much each pixel should reflect light (and in which color, if the specular map contains color). Brighter values will result in a brighter reflection at that given spot on the texture. Specular maps are typically created with manual editing, using the diffuse texture as a base.

If you don't have normal or specular maps for your sprites, you can generate them using the free and open source Laigter tool.

To set up normal maps and/or specular maps on a 2D node, create a new CanvasTexture resource for the property that draws the node's texture. For example, on a Sprite2D:

Creating a CanvasTexture resource for a Sprite2D node

Expand the newly created resource. You can find several properties you will need to adjust:

Diffuse > Texture: The base color texture. In this property, load the texture you're using for the sprite itself.

Normal Map > Texture: The normal map texture. In this property, load a normal map texture you've generated from a height map (see the tip above).

Specular > Texture: The specular map texture, which controls the specular intensity of each pixel on the diffuse texture. The specular map is usually grayscale, but it can also contain color to multiply the color of reflections accordingly. In this property, load a specular map texture you've created (see the tip above).

Specular > Color: The color multiplier for specular reflections.

Specular > Shininess: The specular exponent to use for reflections. Lower values will increase the brightness of reflections and make them more diffuse, while higher values will make reflections more localized. High values are more suited for wet-looking surfaces.

Texture > Filter: Can be set to override the texture filtering mode, regardless of what the node's property is set to (or the Rendering > Textures > Canvas Textures > Default Texture Filter project setting).

Texture > Repeat: Can be set to override the texture filtering mode, regardless of what the node's property is set to (or the Rendering > Textures > Canvas Textures > Default Texture Repeat project setting).

After enabling normal mapping, you may notice that your lights appear to be weaker. To resolve this, increase the Height property on your PointLight2D and DirectionalLight2D nodes. You may also want to increase the lights's Energy property slightly to get closer to how your lighting's intensity looked prior to enabling normal mapping.

If you run into performance issues when using 2D lights, it may be worth replacing some of them with Sprite2D nodes that use additive blending. This is particularly suited for short-lived dynamic effects, such as bullets or explosions.

Additive sprites are much faster to render, since they don't need to go through a separate rendering pipeline. Additionally, it is possible to use this approach with AnimatedSprite2D (or Sprite2D + AnimationPlayer), which allows for animated 2D "lights" to be created.

However, additive sprites have a few downsides compared to 2D lights:

The blending formula is inaccurate compared to "actual" 2D lighting. This is usually not a problem in sufficiently lit areas, but this prevents additive sprites from correctly lighting up areas that are fully dark.

Additive sprites cannot cast shadows, since they are not lights.

Additive sprites ignore normal and specular maps used on other sprites.

To display a sprite with additive blending, create a Sprite2D node and assign a texture to it. In the inspector, scroll down to the CanvasItem > Material section, unfold it and click the dropdown next to the Material property. Choose New CanvasItemMaterial, click the newly created material to edit it, then set Blend Mode to Add.

Please read the User-contributed notes policy before submitting a comment.

---

## Advanced Import Settings

**URL:** https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/advanced_import_settings.html

**Contents:**
- Advanced Import Settings
- Using the Advanced Import Settings dialog
  - Configuring node import options
  - Configuring mesh and material import options
- Extracting materials to separate files
- Animation options
  - Optimizer
  - Save to file
  - Slices
- User-contributed notes

While the regular import panel provides many essential options for imported 3D models, the advanced import settings provides per object options, model previews, and animation previews. To open it select the Advanced... button at the bottom of the import dock.

This is available for 3D models imported as scenes, as well as animation libraries.

This page does not go over options also available in the import dock, or anything outside of the advanced import settings. For information on those please read the Import configuration page.

The first tab you'll see is the Scene tab. The options available in the panel on the right are identical to the Import dock, but you have access to a 3D preview. The 3D preview can be rotated by holding down the left mouse button then dragging the mouse. Zoom can be adjusted using the mouse wheel.

Advanced Import Settings dialog (Scene tab). Credit: Modern Arm Chair 01 - Poly Haven

You can select individual nodes that compose the scene while in the Scene tab using the tree view at the left:

Selecting a node in the Advanced Import Settings dialog (Materials tab)

This exposes several per-node import options:

Skip Import: If checked, the node will not be present in the final imported scene. Enabling this disables all other options.

Generate > Physics: If checked, generates a PhysicsBody3D parent node with collision shapes that are siblings to the MeshInstance3D node.

Generate > NavMesh: If checked, generates a NavigationRegion3D child node for navigation. Mesh + NavMesh will keep the original mesh visible, while NavMesh Only will only import the navigation mesh (without a visual representation). NavMesh Only is meant to be used when you've manually authored a simplified mesh for navigation.

Generate > Occluder: If checked, generates an OccluderInstance3D sibling node for occlusion culling using the mesh's geometry as a basis for the occluder's shape. Mesh + Occluder will keep the original mesh visible, while Occluder Only will only import the occluder (without a visual representation). Occluder Only is meant to be used when you've manually authored a simplified mesh for occlusion culling.

These options are only visible if some of the above options are enabled:

Physics > Body Type: Only visible if Generate > Physics is enabled. Controls the PhysicsBody3D that should be created. Static creates a StaticBody3D, Dynamic creates a RigidBody3D, Area creates an Area3D.

Physics > Shape Type: Only visible if Generate > Physics is enabled. Trimesh allows for precise per-triangle collision, but it can only be used with a Static body type. Other types are less precise and may require manual configuration, but can be used with any body type. For static level geometry, use Trimesh. For dynamic geometry, use primitive shapes if possible for better performance, or use one of the convex decomposition modes if the shape is large and complex.

Decomposition > Advanced: Only visible if Physics > Shape Type is Decompose Convex. If checked, allows adjusting advanced decomposition options. If disabled, only a preset Precision can be adjusted (which is usually sufficient).

Decomposition > Precision: Only visible if Physics > Shape Type is Decompose Convex. Controls the precision to use for convex decomposition. Higher values result in more detailed collision, at the cost of slower generation and increased CPU usage during physics simulation. To improve performance, it's recommended to keep this value as low as possible for your use cases.

Occluder > Simplification Distance: Only visible if Generate > Occluder is set to Mesh + Occluder or Occluder Only. Higher values result in an occluder mesh with fewer vertices (resulting in decreased CPU utilization), at the cost of more occlusion culling issues (such as false positives or false negatives). If you run into objects disappearing when they shouldn't when the camera is near a certain mesh, try decreasing this value.

In the Advanced Import Settings dialog, there are 2 ways to select individual meshes or materials:

Switch to the Meshes or Materials tab in the top-left corner of the dialog.

Stay in the Scene tab, but unfold the options on the tree view on the left. After choosing a mesh or material, this presents the same information as the Meshes and Materials tabs, but in a tree view instead of a list.

If you select a mesh, different options will appear in the panel on the right:

Advanced Import Settings dialog (Meshes tab)

The options are as follows:

Save to File: Saves the Mesh resource to an external file (this isn't a scene file). You generally don't need to use this for placing the mesh in a 3D scene – instead, you should instance the 3D scene directly. However, having direct access to the Mesh resource is useful for specific nodes, such as MeshInstance3D, MultiMeshInstance3D, GPUParticles3D or CPUParticles3D. - You will also need to specify an output file path using the option that appears after enabling Save to File. It's recommended to use the .res output file extension for smaller file sizes and faster loading speeds, as .tres is inefficient for writing large amounts of data.

Generate > Shadow Meshes: Per-mesh override for the Meshes > Create Shadow Meshes scene-wide import option described in Using the Import dock. Default will use the scene-wide import option, while Enable or Disable can forcibly enable or disable this behavior on a specific mesh.

Generate > Lightmap UV: Per-mesh override for the Meshes > Light Baking scene-wide import option described in Using the Import dock. Default will use the scene-wide import option, while Enable or Disable can forcibly enable or disable this behavior on a specific mesh. - Setting this to Enable on a scene with the Static light baking mode is equivalent to configuring this mesh to use Static Lightmaps. Setting this to Disable on a scene with the Static Lightmaps light baking mode is equivalent to configuring this mesh to use Static instead.

Generate > LODs: Per-mesh override for the Meshes > Generate LODs scene-wide import option described in Using the Import dock. Default will use the scene-wide import option, while Enable or Disable can forcibly enable or disable this behavior on a specific mesh.

LODs > Normal Merge Angle: The minimum angle difference between two vertices required to preserve a geometry edge in mesh LOD generation. If running into visual issues with LOD generation, decreasing this value may help (at the cost of less efficient LOD generation).

If you select a material, only one option will appear in the panel on the right:

Advanced Import Settings dialog (Materials tab)

When Use External is checked and an output path is specified, this lets you use an external material instead of the material that is included in the original 3D scene file; see the section below.

While Godot can import materials authored in 3D modeling software, the default configuration may not be suitable for your needs. For example:

You want to configure material features not supported by your 3D application.

You want to use a different texture filtering mode, as this option is configured in the material since Godot 4.0 (and not in the image).

You want to replace one of the materials with an entirely different material, such as a custom shader.

To be able to modify the 3D scene's materials in the Godot editor, you need to use external material resources.

In the top-left corner of the Advanced Import Settings dialog, choose Actions… > Extract Materials:

Extracting all built-in materials to external resources in the Advanced Import Settings dialog

After choosing this option, select a folder to extract material .tres files to, then confirm the extraction:

Confirming material extraction in the Advanced Import Settings subdialog

After extracting materials, the 3D scene will automatically be configured to use external material references. As a result, you don't need to manually enable Use External on every material to make the external .tres material effective.

When Use External is enabled, remember that the Advanced Import Settings dialog will keep displaying the mesh's original materials (the ones designed in the 3D modeling software). This means your customizations to the materials won't be visible within this dialog. To preview your modified materials, you need to place the imported 3D scene in another scene using the editor.

Godot will not overwrite changes made to extracted materials when the source 3D scene is reimported. However, if the material name is changed in the source 3D file, the link between the original material and the extracted material will be lost. As a result, you'll need to use the Advanced Import Settings dialog to associate the renamed material to the existing extracted material.

The above can be done in the dialog's Materials tab by selecting the material, enabling Save to File, then specifying the save path using the Path option that appears after enabling Save to File.

Several extra options are available for the generated AnimationPlayer nodes, as well as their individual animations when they're selected in the Scene tab.

When animations are imported, an optimizer is run, which reduces the size of the animation considerably. In general, this should always be turned on unless you suspect that an animation might be broken due to it being enabled.

By default, animations are saved as built-in. It is possible to save them to a file instead. This allows adding custom tracks to the animations and keeping them after a reimport.

It is possible to specify multiple animations from a single timeline as slices. For this to work, the model must have only one animation that is named default. To create slices, change the slice amount to something greater than zero. You can then name a slice, specify which frames it starts and stops on, and choose whether the animation loops or not.

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationLibrary

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationlibrary.html

**Contents:**
- AnimationLibrary
- Description
- Tutorials
- Methods
- Signals
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Container for Animation resources.

An animation library stores a set of animations accessible through StringName keys, for use with AnimationPlayer nodes.

Animation tutorial index

add_animation(name: StringName, animation: Animation)

get_animation(name: StringName) const

get_animation_list() const

get_animation_list_size() const

has_animation(name: StringName) const

remove_animation(name: StringName)

rename_animation(name: StringName, newname: StringName)

animation_added(name: StringName) 🔗

Emitted when an Animation is added, under the key name.

animation_changed(name: StringName) 🔗

Emitted when there's a change in one of the animations, e.g. tracks are added, moved or have changed paths. name is the key of the animation that was changed.

See also Resource.changed, which this acts as a relay for.

animation_removed(name: StringName) 🔗

Emitted when an Animation stored with the key name is removed.

animation_renamed(name: StringName, to_name: StringName) 🔗

Emitted when the key for an Animation is changed, from name to to_name.

Error add_animation(name: StringName, animation: Animation) 🔗

Adds the animation to the library, accessible by the key name.

Animation get_animation(name: StringName) const 🔗

Returns the Animation with the key name. If the animation does not exist, null is returned and an error is logged.

Array[StringName] get_animation_list() const 🔗

Returns the keys for the Animations stored in the library.

int get_animation_list_size() const 🔗

Returns the key count for the Animations stored in the library.

bool has_animation(name: StringName) const 🔗

Returns true if the library stores an Animation with name as the key.

void remove_animation(name: StringName) 🔗

Removes the Animation with the key name.

void rename_animation(name: StringName, newname: StringName) 🔗

Changes the key of the Animation associated with the key name to newname.

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeStateMachinePlayback

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodestatemachineplayback.html

**Contents:**
- AnimationNodeStateMachinePlayback
- Description
- Tutorials
- Properties
- Methods
- Signals
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Provides playback control for an AnimationNodeStateMachine.

Allows control of AnimationTree state machines created with AnimationNodeStateMachine. Retrieve with $AnimationTree.get("parameters/playback").

resource_local_to_scene

true (overrides Resource)

get_current_length() const

get_current_node() const

get_current_play_position() const

get_fading_from_node() const

get_travel_path() const

start(node: StringName, reset: bool = true)

travel(to_node: StringName, reset_on_teleport: bool = true)

state_finished(state: StringName) 🔗

Emitted when the state finishes playback. If state is a state machine set to grouped mode, its signals are passed through with its name prefixed.

If there is a crossfade, this will be fired when the influence of the get_fading_from_node() animation is no longer present.

state_started(state: StringName) 🔗

Emitted when the state starts playback. If state is a state machine set to grouped mode, its signals are passed through with its name prefixed.

float get_current_length() const 🔗

Returns the current state length.

Note: It is possible that any AnimationRootNode can be nodes as well as animations. This means that there can be multiple animations within a single state. Which animation length has priority depends on the nodes connected inside it. Also, if a transition does not reset, the remaining length at that point will be returned.

StringName get_current_node() const 🔗

Returns the currently playing animation state.

Note: When using a cross-fade, the current state changes to the next state immediately after the cross-fade begins.

float get_current_play_position() const 🔗

Returns the playback position within the current animation state.

StringName get_fading_from_node() const 🔗

Returns the starting state of currently fading animation.

Array[StringName] get_travel_path() const 🔗

Returns the current travel path as computed internally by the A* algorithm.

bool is_playing() const 🔗

Returns true if an animation is playing.

If there is a next path by travel or auto advance, immediately transitions from the current state to the next state.

void start(node: StringName, reset: bool = true) 🔗

Starts playing the given animation.

If reset is true, the animation is played from the beginning.

Stops the currently playing animation.

void travel(to_node: StringName, reset_on_teleport: bool = true) 🔗

Transitions from the current state to another one, following the shortest path.

If the path does not connect from the current state, the animation will play after the state teleports.

If reset_on_teleport is true, the animation is played from the beginning when the travel cause a teleportation.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var state_machine = $AnimationTree.get("parameters/playback")
state_machine.travel("some_state")
```

Example 2 (gdscript):
```gdscript
var stateMachine = GetNode<AnimationTree>("AnimationTree").Get("parameters/playback").As<AnimationNodeStateMachinePlayback>();
stateMachine.Travel("some_state");
```

---

## AnimationNodeStateMachineTransition

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodestatemachinetransition.html

**Contents:**
- AnimationNodeStateMachineTransition
- Description
- Tutorials
- Properties
- Signals
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

A transition within an AnimationNodeStateMachine connecting two AnimationRootNodes.

The path generated when using AnimationNodeStateMachinePlayback.travel() is limited to the nodes connected by AnimationNodeStateMachineTransition.

You can set the timing and conditions of the transition in detail.

advance_condition_changed() 🔗

Emitted when advance_condition is changed.

SwitchMode SWITCH_MODE_IMMEDIATE = 0

Switch to the next state immediately. The current state will end and blend into the beginning of the new one.

SwitchMode SWITCH_MODE_SYNC = 1

Switch to the next state immediately, but will seek the new state to the playback position of the old state.

SwitchMode SWITCH_MODE_AT_END = 2

Wait for the current state playback to end, then switch to the beginning of the next state animation.

AdvanceMode ADVANCE_MODE_DISABLED = 0

Don't use this transition.

AdvanceMode ADVANCE_MODE_ENABLED = 1

Only use this transition during AnimationNodeStateMachinePlayback.travel().

AdvanceMode ADVANCE_MODE_AUTO = 2

Automatically use this transition if the advance_condition and advance_expression checks are true (if assigned).

StringName advance_condition = &"" 🔗

void set_advance_condition(value: StringName)

StringName get_advance_condition()

Turn on auto advance when this condition is set. The provided name will become a boolean parameter on the AnimationTree that can be controlled from code (see Using AnimationTree). For example, if AnimationTree.tree_root is an AnimationNodeStateMachine and advance_condition is set to "idle":

String advance_expression = "" 🔗

void set_advance_expression(value: String)

String get_advance_expression()

Use an expression as a condition for state machine transitions. It is possible to create complex animation advance conditions for switching between states and gives much greater flexibility for creating complex state machines by directly interfacing with the script code.

AdvanceMode advance_mode = 1 🔗

void set_advance_mode(value: AdvanceMode)

AdvanceMode get_advance_mode()

Determines whether the transition should be disabled, enabled when using AnimationNodeStateMachinePlayback.travel(), or traversed automatically if the advance_condition and advance_expression checks are true (if assigned).

bool break_loop_at_end = false 🔗

void set_break_loop_at_end(value: bool)

bool is_loop_broken_at_end()

If true, breaks the loop at the end of the loop cycle for transition, even if the animation is looping.

void set_priority(value: int)

Lower priority transitions are preferred when travelling through the tree via AnimationNodeStateMachinePlayback.travel() or advance_mode is set to ADVANCE_MODE_AUTO.

void set_reset(value: bool)

If true, the destination animation is played back from the beginning when switched.

SwitchMode switch_mode = 0 🔗

void set_switch_mode(value: SwitchMode)

SwitchMode get_switch_mode()

void set_xfade_curve(value: Curve)

Curve get_xfade_curve()

Ease curve for better control over cross-fade between this state and the next. Should be a unit Curve.

float xfade_time = 0.0 🔗

void set_xfade_time(value: float)

float get_xfade_time()

The time to cross-fade between this state and the next.

Note: AnimationNodeStateMachine transitions the current state immediately after the start of the fading. The precise remaining time can only be inferred from the main animation. When AnimationNodeOutput is considered as the most upstream, so the xfade_time is not scaled depending on the downstream delta. See also AnimationNodeOneShot.fadeout_time.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (bash):
```bash
$animation_tree.set("parameters/conditions/idle", is_on_floor and (linear_velocity.x == 0))
```

Example 2 (typescript):
```typescript
GetNode<AnimationTree>("animation_tree").Set("parameters/conditions/idle", IsOnFloor && (LinearVelocity.X == 0));
```

---

## AnimationNodeStateMachine

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodestatemachine.html

**Contents:**
- AnimationNodeStateMachine
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AnimationRootNode < AnimationNode < Resource < RefCounted < Object

A state machine with multiple AnimationRootNodes, used by AnimationTree.

Contains multiple AnimationRootNodes representing animation states, connected in a graph. State transitions can be configured to happen automatically or via code, using a shortest-path algorithm. Retrieve the AnimationNodeStateMachinePlayback object from the AnimationTree node to control it programmatically.

allow_transition_to_self

add_node(name: StringName, node: AnimationNode, position: Vector2 = Vector2(0, 0))

add_transition(from: StringName, to: StringName, transition: AnimationNodeStateMachineTransition)

get_graph_offset() const

get_node(name: StringName) const

get_node_list() const

get_node_name(node: AnimationNode) const

get_node_position(name: StringName) const

AnimationNodeStateMachineTransition

get_transition(idx: int) const

get_transition_count() const

get_transition_from(idx: int) const

get_transition_to(idx: int) const

has_node(name: StringName) const

has_transition(from: StringName, to: StringName) const

remove_node(name: StringName)

remove_transition(from: StringName, to: StringName)

remove_transition_by_index(idx: int)

rename_node(name: StringName, new_name: StringName)

replace_node(name: StringName, node: AnimationNode)

set_graph_offset(offset: Vector2)

set_node_position(name: StringName, position: Vector2)

enum StateMachineType: 🔗

StateMachineType STATE_MACHINE_TYPE_ROOT = 0

Seeking to the beginning is treated as playing from the start state. Transition to the end state is treated as exiting the state machine.

StateMachineType STATE_MACHINE_TYPE_NESTED = 1

Seeking to the beginning is treated as seeking to the beginning of the animation in the current state. Transition to the end state, or the absence of transitions in each state, is treated as exiting the state machine.

StateMachineType STATE_MACHINE_TYPE_GROUPED = 2

This is a grouped state machine that can be controlled from a parent state machine. It does not work independently. There must be a state machine with state_machine_type of STATE_MACHINE_TYPE_ROOT or STATE_MACHINE_TYPE_NESTED in the parent or ancestor.

bool allow_transition_to_self = false 🔗

void set_allow_transition_to_self(value: bool)

bool is_allow_transition_to_self()

If true, allows teleport to the self state with AnimationNodeStateMachinePlayback.travel(). When the reset option is enabled in AnimationNodeStateMachinePlayback.travel(), the animation is restarted. If false, nothing happens on the teleportation to the self state.

bool reset_ends = false 🔗

void set_reset_ends(value: bool)

bool are_ends_reset()

If true, treat the cross-fade to the start and end nodes as a blend with the RESET animation.

In most cases, when additional cross-fades are performed in the parent AnimationNode of the state machine, setting this property to false and matching the cross-fade time of the parent AnimationNode and the state machine's start node and end node gives good results.

StateMachineType state_machine_type = 0 🔗

void set_state_machine_type(value: StateMachineType)

StateMachineType get_state_machine_type()

This property can define the process of transitions for different use cases. See also StateMachineType.

void add_node(name: StringName, node: AnimationNode, position: Vector2 = Vector2(0, 0)) 🔗

Adds a new animation node to the graph. The position is used for display in the editor.

void add_transition(from: StringName, to: StringName, transition: AnimationNodeStateMachineTransition) 🔗

Adds a transition between the given animation nodes.

Vector2 get_graph_offset() const 🔗

Returns the draw offset of the graph. Used for display in the editor.

AnimationNode get_node(name: StringName) const 🔗

Returns the animation node with the given name.

Array[StringName] get_node_list() const 🔗

Returns a list containing the names of all animation nodes in this state machine.

StringName get_node_name(node: AnimationNode) const 🔗

Returns the given animation node's name.

Vector2 get_node_position(name: StringName) const 🔗

Returns the given animation node's coordinates. Used for display in the editor.

AnimationNodeStateMachineTransition get_transition(idx: int) const 🔗

Returns the given transition.

int get_transition_count() const 🔗

Returns the number of connections in the graph.

StringName get_transition_from(idx: int) const 🔗

Returns the given transition's start node.

StringName get_transition_to(idx: int) const 🔗

Returns the given transition's end node.

bool has_node(name: StringName) const 🔗

Returns true if the graph contains the given animation node.

bool has_transition(from: StringName, to: StringName) const 🔗

Returns true if there is a transition between the given animation nodes.

void remove_node(name: StringName) 🔗

Deletes the given animation node from the graph.

void remove_transition(from: StringName, to: StringName) 🔗

Deletes the transition between the two specified animation nodes.

void remove_transition_by_index(idx: int) 🔗

Deletes the given transition by index.

void rename_node(name: StringName, new_name: StringName) 🔗

Renames the given animation node.

void replace_node(name: StringName, node: AnimationNode) 🔗

Replaces the given animation node with a new animation node.

void set_graph_offset(offset: Vector2) 🔗

Sets the draw offset of the graph. Used for display in the editor.

void set_node_position(name: StringName, position: Vector2) 🔗

Sets the animation node's coordinates. Used for display in the editor.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var state_machine = $AnimationTree.get("parameters/playback")
state_machine.travel("some_state")
```

Example 2 (typescript):
```typescript
var stateMachine = GetNode<AnimationTree>("AnimationTree").Get("parameters/playback") as AnimationNodeStateMachinePlayback;
stateMachine.Travel("some_state");
```

---

## AnimationNodeSub2

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodesub2.html

**Contents:**
- AnimationNodeSub2
- Description
- Tutorials
- User-contributed notes

Inherits: AnimationNodeSync < AnimationNode < Resource < RefCounted < Object

Blends two animations subtractively inside of an AnimationNodeBlendTree.

A resource to add to an AnimationNodeBlendTree. Blends two animations subtractively based on the amount value.

This animation node is usually used for pre-calculation to cancel out any extra poses from the animation for the "add" animation source in AnimationNodeAdd2 or AnimationNodeAdd3.

In general, the blend value should be in the [0.0, 1.0] range, but values outside of this range can be used for amplified or inverted animations.

Note: This calculation is different from using a negative value in AnimationNodeAdd2, since the transformation matrices do not satisfy the commutative law. AnimationNodeSub2 multiplies the transformation matrix of the inverted animation from the left side, while negative AnimationNodeAdd2 multiplies it from the right side.

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeSync

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodesync.html

**Contents:**
- AnimationNodeSync
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: AnimationNode < Resource < RefCounted < Object

Inherited By: AnimationNodeAdd2, AnimationNodeAdd3, AnimationNodeBlend2, AnimationNodeBlend3, AnimationNodeOneShot, AnimationNodeSub2, AnimationNodeTransition

Base class for AnimationNodes with multiple input ports that must be synchronized.

An animation node used to combine, mix, or blend two or more animations together while keeping them synchronized within an AnimationTree.

void set_use_sync(value: bool)

If false, the blended animations' frame are stopped when the blend value is 0.

If true, forcing the blended animations to advance frame.

Please read the User-contributed notes policy before submitting a comment.

---

## Animation

**URL:** https://docs.godotengine.org/en/stable/tutorials/animation/index.html

**Contents:**
- Animation

This section of the tutorial covers using the two animation nodes in Godot and the animation editor.

See Importing 3D scenes for information on importing animations from a 3D model.

---

## Autoloads versus regular nodes

**URL:** https://docs.godotengine.org/en/stable/tutorials/best_practices/autoloads_versus_internal_nodes.html

**Contents:**
- Autoloads versus regular nodes
- The cutting audio issue
- Managing shared functionality or data
- When you should use an Autoload
- User-contributed notes

Godot offers a feature to automatically load nodes at the root of your project, allowing you to access them globally, that can fulfill the role of a Singleton: Singletons (Autoload). These autoloaded nodes are not freed when you change the scene from code with SceneTree.change_scene_to_file.

In this guide, you will learn when to use the Autoload feature, and techniques you can use to avoid it.

Other engines can encourage the use of creating manager classes, singletons that organize a lot of functionality into a globally accessible object. Godot offers many ways to avoid global state thanks to the node tree and signals.

For example, let's say we are building a platformer and want to collect coins that play a sound effect. There's a node for that: the AudioStreamPlayer. But if we call the AudioStreamPlayer while it is already playing a sound, the new sound interrupts the first.

A solution is to code a global, autoloaded sound manager class. It generates a pool of AudioStreamPlayer nodes that cycle through as each new request for sound effects comes in. Say we call that class Sound, you can use it from anywhere in your project by calling Sound.play("coin_pickup.ogg"). This solves the problem in the short term but causes more problems:

Global state: one object is now responsible for all objects' data. If the Sound class has errors or doesn't have an AudioStreamPlayer available, all the nodes calling it can break.

Global access: now that any object can call Sound.play(sound_path) from anywhere, there's no longer an easy way to find the source of a bug.

Global resource allocation: with a pool of AudioStreamPlayer nodes stored from the start, you can either have too few and face bugs, or too many and use more memory than you need.

About global access, the problem is that any code anywhere could pass wrong data to the Sound autoload in our example. As a result, the domain to explore to fix the bug spans the entire project.

When you keep code inside a scene, only one or two scripts may be involved in audio.

Contrast this with each scene keeping as many AudioStreamPlayer nodes as it needs within itself and all these problems go away:

Each scene manages its own state information. If there is a problem with the data, it will only cause issues in that one scene.

Each scene accesses only its own nodes. Now, if there is a bug, it's easy to find which node is at fault.

Each scene allocates exactly the amount of resources it needs.

Another reason to use an Autoload can be that you want to reuse the same method or data across many scenes.

In the case of functions, you can create a new type of Node that provides that feature for an individual scene using the class_name keyword in GDScript.

When it comes to data, you can either:

Create a new type of Resource to share the data.

Store the data in an object to which each node has access, for example using the owner property to access the scene's root node.

GDScript supports the creation of static functions using static func. When combined with class_name, this makes it possible to create libraries of helper functions without having to create an instance to call them. The limitation of static functions is that they can't reference member variables, non-static functions or self.

Since Godot 4.1, GDScript also supports static variables using static var. This means you can now share variables across instances of a class without having to create a separate autoload.

Still, autoloaded nodes can simplify your code for systems with a wide scope. If the autoload is managing its own information and not invading the data of other objects, then it's a great way to create systems that handle broad-scoped tasks. For example, a quest or a dialogue system.

An autoload is not necessarily a singleton. Nothing prevents you from instantiating copies of an autoloaded node. An autoload is only a tool that makes a node load automatically as a child of the root of your scene tree, regardless of your game's node structure or which scene you run, e.g. by pressing the F6 key.

As a result, you can get the autoloaded node, for example an autoload called Sound, by calling get_node("/root/Sound").

Please read the User-contributed notes policy before submitting a comment.

---

## Available 3D formats

**URL:** https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/available_formats.html

**Contents:**
- Available 3D formats
- Exporting glTF 2.0 files from Blender (recommended)
- Importing .blend files directly within Godot
- Exporting DAE files from Blender
- Importing OBJ files in Godot
- Importing FBX files in Godot
- User-contributed notes

When dealing with 3D assets, Godot has a flexible and configurable importer.

Godot works with scenes. This means that the entire scene being worked on in your favorite 3D modeling software will be transferred as close as possible.

Godot supports the following 3D scene file formats:

glTF 2.0 (recommended). Godot has support for both text (.gltf) and binary (.glb) formats.

.blend (Blender). This works by calling Blender to export to glTF in a transparent manner (requires Blender to be installed).

DAE (COLLADA), an older format that is supported.

OBJ (Wavefront) format + their MTL material files. This is also supported, but pretty limited given the format's limitations (no support for pivots, skeletons, animations, UV2, PBR materials, ...).

FBX, supported via the ufbx library. The previous import workflow used FBX2glTF integration. This requires installing an external program that links against the proprietary FBX SDK, so we recommend using the default ufbx method or other formats listed above (if suitable for your workflow).

Copy the scene file together with the textures and mesh data (if separate) to the project repository, then Godot will do a full import when focusing the editor window.

There are 3 ways to export glTF files from Blender:

As a glTF binary file (.glb).

As a glTF text-based file with separate binary data and textures (.gltf file + .bin file + textures).

glTF binary files (.glb) are the smaller option. They include the mesh and textures set up in Blender. When brought into Godot the textures are part of the object's material file.

There are two reasons to use glTF with the textures separate. One is to have the scene description in a text based format and the binary data in a separate binary file. This can be useful for version control if you want to review changes in a text-based format. The second is you need the texture files separate from the material file. If you don't need either of those, glTF binary files are fine.

The glTF import process first loads the glTF file's data into an in-memory GLTFState class. This data is then used to generate a Godot scene. When importing files at runtime, this scene can be directly added to the tree. The export process is the reverse of this, a Godot scene is converted to a GLTFState class, then the glTF file is generated from that.

When importing glTF files in the editor, there are two more steps. After generating the Godot scene, the ResourceImporterScene class is used to apply additional import settings, including settings you set through the Import dock and the Advanced Import Settings dialog. This is then saved as a Godot scene file, which is what gets used when you run/export your game.

If your model contains blend shapes (also known as "shape keys" and "morph targets"), your glTF export setting Data > Armature > Export Deformation Bones Only needs to be configured to Enabled.

Exporting non-deforming bones anyway will lead to incorrect shading.

Blender versions older than 3.2 do not export emissive textures with the glTF file. If your model uses one and you're using an older version of Blender, it must be brought in separately.

By default, Blender has backface culling disabled on materials and will export materials to match how they render in Blender. This means that materials in Godot will have their cull mode set to Disabled. This can decrease performance since backfaces will be rendered, even when they are being culled by other faces. To resolve this, enable Backface Culling in Blender's Materials tab, then export the scene to glTF again.

This functionality requires Blender 3.0 or later. For best results, we recommend using Blender 3.5 or later, as it includes many fixes to the glTF exporter.

It is strongly recommended to use an official Blender release downloaded from blender.org, as opposed to a Linux distribution package or Flatpak. This avoids any issues related to packaging, such as different library versions that can cause incompatibilities or sandboxing restrictions.

The editor can directly import .blend files by calling Blender's glTF export functionality in a transparent manner.

This allows you to iterate on your 3D scenes faster, as you can save the scene in Blender, alt-tab back to Godot then see your changes immediately. When working with version control, this is also more efficient as you no longer need to commit a copy of the exported glTF file to version control.

To use .blend import, you must install Blender before opening the Godot editor (if opening a project that already contains .blend files). If you keep Blender installed at its default location, Godot should be able to detect its path automatically. If this isn't the case, configure the path to the Blender executable in the Editor Settings (Filesystem > Import > Blender > Blender Path).

If you keep .blend files within your project folder but don't want them to be imported by Godot, disable Filesystem > Import > Blender > Enabled in the advanced Project Settings.

The .blend import process converts to glTF first, so it still uses Godot's glTF import code. Therefore, the .blend import process is the same as the glTF import process, but with an extra step at the beginning.

When working in a team, keep in mind using .blend files in your project will require all team members to have Blender installed. While Blender is a free download, this may add friction when working on the project. .blend import is also not available on the Android and web editors, as these platforms can't call external programs.

If this is problematic, consider using glTF scenes exported from Blender instead.

Blender has built-in COLLADA support, but it does not work properly for the needs of game engines and shouldn't be used as-is. However, scenes exported with the built-in Collada support may still work for simple scenes without animation.

For complex scenes or scenes that contain animations it is highly recommend to use glTF instead.

OBJ is one of the simplest 3D formats out there, so Godot should be able to import most OBJ files successfully. However, OBJ is also a very limited format: it doesn't support skinning, animation, UV2 or PBR materials.

There are 2 ways to use OBJ meshes in Godot:

Load them directly in a MeshInstance3D node, or any other property that expects as mesh (such as GPUParticles3D). This is the default mode.

Change their import mode to OBJ as Scene in the Import dock then restart the editor. This allows you to use the same import options as glTF or Collada scenes, such as unwrapping UV2 on import (for Using Lightmap global illumination).

Blender 3.4 and later can export RGB vertex colors in OBJ files (this is a nonstandard extension of the OBJ format). Godot is able to import those vertex colors, but they will not be displayed on the material unless you enable Vertex Color > Use As Albedo on the material.

Vertex colors from OBJ meshes keep their original color space once imported (sRGB/linear), but their brightness is clamped to 1.0 (they can't be overbright).

By default any FBX file added to a Godot project in Godot 4.3 or later will use the ufbx import method. Any file that was was added to a project in a previous version, such as 4.2, will continue to be imported via the FBX2glTF method unless you go into that files import settings, and change the importer to ufbx.

If you keep .fbx files within your project folder but don't want them to be imported by Godot, disable Filesystem > Import > FBX > Enabled in the advanced Project Settings.

If you want to setup the FBX2glTF workflow, which is generally not recommend unless you have a specific reason to use it, you need to download the FBX2glTF executable, then specify the path to that executable in the editor settings under Filesystem > Import > FBX > FBX2glTFPath

The FBX2glTF import process converts to glTF first, so it still uses Godot's glTF import code. Therefore, the FBX import process is the same as the glTF import process, but with an extra step at the beginning.

The full installation process for using FBX2glTF in Godot is described on the FBX import page of the Godot website.

Please read the User-contributed notes policy before submitting a comment.

---

## Camera2D

**URL:** https://docs.godotengine.org/en/stable/classes/class_camera2d.html

**Contents:**
- Camera2D
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Node2D < CanvasItem < Node < Object

Camera node for 2D scenes.

Camera node for 2D scenes. It forces the screen (current layer) to scroll following this node. This makes it easier (and faster) to program scrollable scenes than manually changing the position of CanvasItem-based nodes.

Cameras register themselves in the nearest Viewport node (when ascending the tree). Only one camera can be active per viewport. If no viewport is available ascending the tree, the camera will register in the global viewport.

This node is intended to be a simple helper to get things going quickly, but more functionality may be desired to change how the camera works. To make your own custom camera node, inherit it from Node2D and change the transform of the canvas by setting Viewport.canvas_transform in Viewport (you can obtain the current Viewport by using Node.get_viewport()).

Note that the Camera2D node's Node2D.global_position doesn't represent the actual position of the screen, which may differ due to applied smoothing or limits. You can use get_screen_center_position() to get the real position. Same for the node's Node2D.global_rotation which may be different due to applied rotation smoothing. You can use get_screen_rotation() to get the current rotation of the screen.

drag_horizontal_enabled

drag_horizontal_offset

drag_vertical_enabled

editor_draw_drag_margin

position_smoothing_enabled

position_smoothing_speed

Camera2DProcessCallback

rotation_smoothing_enabled

rotation_smoothing_speed

force_update_scroll()

get_drag_margin(margin: Side) const

get_limit(margin: Side) const

get_screen_center_position() const

get_screen_rotation() const

get_target_position() const

set_drag_margin(margin: Side, drag_margin: float)

set_limit(margin: Side, limit: int)

AnchorMode ANCHOR_MODE_FIXED_TOP_LEFT = 0

The camera's position is fixed so that the top-left corner is always at the origin.

AnchorMode ANCHOR_MODE_DRAG_CENTER = 1

The camera's position takes into account vertical/horizontal offsets and the screen size.

enum Camera2DProcessCallback: 🔗

Camera2DProcessCallback CAMERA2D_PROCESS_PHYSICS = 0

The camera updates during physics frames (see Node.NOTIFICATION_INTERNAL_PHYSICS_PROCESS).

Camera2DProcessCallback CAMERA2D_PROCESS_IDLE = 1

The camera updates during process frames (see Node.NOTIFICATION_INTERNAL_PROCESS).

AnchorMode anchor_mode = 1 🔗

void set_anchor_mode(value: AnchorMode)

AnchorMode get_anchor_mode()

The Camera2D's anchor point.

Node custom_viewport 🔗

void set_custom_viewport(value: Node)

Node get_custom_viewport()

The custom Viewport node attached to the Camera2D. If null or not a Viewport, uses the default viewport instead.

float drag_bottom_margin = 0.2 🔗

void set_drag_margin(margin: Side, drag_margin: float)

float get_drag_margin(margin: Side) const

Bottom margin needed to drag the camera. A value of 1 makes the camera move only when reaching the bottom edge of the screen.

bool drag_horizontal_enabled = false 🔗

void set_drag_horizontal_enabled(value: bool)

bool is_drag_horizontal_enabled()

If true, the camera only moves when reaching the horizontal (left and right) drag margins. If false, the camera moves horizontally regardless of margins.

float drag_horizontal_offset = 0.0 🔗

void set_drag_horizontal_offset(value: float)

float get_drag_horizontal_offset()

The relative horizontal drag offset of the camera between the right (-1) and left (1) drag margins.

Note: Used to set the initial horizontal drag offset; determine the current offset; or force the current offset. It's not automatically updated when drag_horizontal_enabled is true or the drag margins are changed.

float drag_left_margin = 0.2 🔗

void set_drag_margin(margin: Side, drag_margin: float)

float get_drag_margin(margin: Side) const

Left margin needed to drag the camera. A value of 1 makes the camera move only when reaching the left edge of the screen.

float drag_right_margin = 0.2 🔗

void set_drag_margin(margin: Side, drag_margin: float)

float get_drag_margin(margin: Side) const

Right margin needed to drag the camera. A value of 1 makes the camera move only when reaching the right edge of the screen.

float drag_top_margin = 0.2 🔗

void set_drag_margin(margin: Side, drag_margin: float)

float get_drag_margin(margin: Side) const

Top margin needed to drag the camera. A value of 1 makes the camera move only when reaching the top edge of the screen.

bool drag_vertical_enabled = false 🔗

void set_drag_vertical_enabled(value: bool)

bool is_drag_vertical_enabled()

If true, the camera only moves when reaching the vertical (top and bottom) drag margins. If false, the camera moves vertically regardless of the drag margins.

float drag_vertical_offset = 0.0 🔗

void set_drag_vertical_offset(value: float)

float get_drag_vertical_offset()

The relative vertical drag offset of the camera between the bottom (-1) and top (1) drag margins.

Note: Used to set the initial vertical drag offset; determine the current offset; or force the current offset. It's not automatically updated when drag_vertical_enabled is true or the drag margins are changed.

bool editor_draw_drag_margin = false 🔗

void set_margin_drawing_enabled(value: bool)

bool is_margin_drawing_enabled()

If true, draws the camera's drag margin rectangle in the editor.

bool editor_draw_limits = false 🔗

void set_limit_drawing_enabled(value: bool)

bool is_limit_drawing_enabled()

If true, draws the camera's limits rectangle in the editor.

bool editor_draw_screen = true 🔗

void set_screen_drawing_enabled(value: bool)

bool is_screen_drawing_enabled()

If true, draws the camera's screen rectangle in the editor.

bool enabled = true 🔗

void set_enabled(value: bool)

Controls whether the camera can be active or not. If true, the Camera2D will become the main camera when it enters the scene tree and there is no active camera currently (see Viewport.get_camera_2d()).

When the camera is currently active and enabled is set to false, the next enabled Camera2D in the scene tree will become active.

bool ignore_rotation = true 🔗

void set_ignore_rotation(value: bool)

bool is_ignoring_rotation()

If true, the camera's rendered view is not affected by its Node2D.rotation and Node2D.global_rotation.

int limit_bottom = 10000000 🔗

void set_limit(margin: Side, limit: int)

int get_limit(margin: Side) const

Bottom scroll limit in pixels. The camera stops moving when reaching this value, but offset can push the view past the limit.

bool limit_enabled = true 🔗

void set_limit_enabled(value: bool)

bool is_limit_enabled()

If true, the limits will be enabled. Disabling this will allow the camera to focus anywhere, when the four limit_* properties will not work.

int limit_left = -10000000 🔗

void set_limit(margin: Side, limit: int)

int get_limit(margin: Side) const

Left scroll limit in pixels. The camera stops moving when reaching this value, but offset can push the view past the limit.

int limit_right = 10000000 🔗

void set_limit(margin: Side, limit: int)

int get_limit(margin: Side) const

Right scroll limit in pixels. The camera stops moving when reaching this value, but offset can push the view past the limit.

bool limit_smoothed = false 🔗

void set_limit_smoothing_enabled(value: bool)

bool is_limit_smoothing_enabled()

If true, the camera smoothly stops when reaches its limits.

This property has no effect if position_smoothing_enabled is false.

Note: To immediately update the camera's position to be within limits without smoothing, even with this setting enabled, invoke reset_smoothing().

int limit_top = -10000000 🔗

void set_limit(margin: Side, limit: int)

int get_limit(margin: Side) const

Top scroll limit in pixels. The camera stops moving when reaching this value, but offset can push the view past the limit.

Vector2 offset = Vector2(0, 0) 🔗

void set_offset(value: Vector2)

The camera's relative offset. Useful for looking around or camera shake animations. The offsetted camera can go past the limits defined in limit_top, limit_bottom, limit_left and limit_right.

bool position_smoothing_enabled = false 🔗

void set_position_smoothing_enabled(value: bool)

bool is_position_smoothing_enabled()

If true, the camera's view smoothly moves towards its target position at position_smoothing_speed.

float position_smoothing_speed = 5.0 🔗

void set_position_smoothing_speed(value: float)

float get_position_smoothing_speed()

Speed in pixels per second of the camera's smoothing effect when position_smoothing_enabled is true.

Camera2DProcessCallback process_callback = 1 🔗

void set_process_callback(value: Camera2DProcessCallback)

Camera2DProcessCallback get_process_callback()

The camera's process callback.

bool rotation_smoothing_enabled = false 🔗

void set_rotation_smoothing_enabled(value: bool)

bool is_rotation_smoothing_enabled()

If true, the camera's view smoothly rotates, via asymptotic smoothing, to align with its target rotation at rotation_smoothing_speed.

Note: This property has no effect if ignore_rotation is true.

float rotation_smoothing_speed = 5.0 🔗

void set_rotation_smoothing_speed(value: float)

float get_rotation_smoothing_speed()

The angular, asymptotic speed of the camera's rotation smoothing effect when rotation_smoothing_enabled is true.

Vector2 zoom = Vector2(1, 1) 🔗

void set_zoom(value: Vector2)

The camera's zoom. Higher values are more zoomed in. For example, a zoom of Vector2(2.0, 2.0) will be twice as zoomed in on each axis (the view covers an area four times smaller). In contrast, a zoom of Vector2(0.5, 0.5) will be twice as zoomed out on each axis (the view covers an area four times larger). The X and Y components should generally always be set to the same value, unless you wish to stretch the camera view.

Note: FontFile.oversampling does not take Camera2D zoom into account. This means that zooming in/out will cause bitmap fonts and rasterized (non-MSDF) dynamic fonts to appear blurry or pixelated unless the font is part of a CanvasLayer that makes it ignore camera zoom. To ensure text remains crisp regardless of zoom, you can enable MSDF font rendering by enabling ProjectSettings.gui/theme/default_font_multichannel_signed_distance_field (applies to the default project font only), or enabling Multichannel Signed Distance Field in the import options of a DynamicFont for custom fonts. On system fonts, SystemFont.multichannel_signed_distance_field can be enabled in the inspector.

Aligns the camera to the tracked node.

void force_update_scroll() 🔗

Forces the camera to update scroll immediately.

float get_drag_margin(margin: Side) const 🔗

Returns the specified Side's margin. See also drag_bottom_margin, drag_top_margin, drag_left_margin, and drag_right_margin.

int get_limit(margin: Side) const 🔗

Returns the camera limit for the specified Side. See also limit_bottom, limit_top, limit_left, and limit_right.

Vector2 get_screen_center_position() const 🔗

Returns the center of the screen from this camera's point of view, in global coordinates.

Note: The exact targeted position of the camera may be different. See get_target_position().

float get_screen_rotation() const 🔗

Returns the current screen rotation from this camera's point of view.

Note: The screen rotation can be different from Node2D.global_rotation if the camera is rotating smoothly due to rotation_smoothing_enabled.

Vector2 get_target_position() const 🔗

Returns this camera's target position, in global coordinates.

Note: The returned value is not the same as Node2D.global_position, as it is affected by the drag properties. It is also not the same as the current position if position_smoothing_enabled is true (see get_screen_center_position()).

bool is_current() const 🔗

Returns true if this Camera2D is the active camera (see Viewport.get_camera_2d()).

void make_current() 🔗

Forces this Camera2D to become the current active one. enabled must be true.

void reset_smoothing() 🔗

Sets the camera's position immediately to its current smoothing destination.

This method has no effect if position_smoothing_enabled is false.

void set_drag_margin(margin: Side, drag_margin: float) 🔗

Sets the specified Side's margin. See also drag_bottom_margin, drag_top_margin, drag_left_margin, and drag_right_margin.

void set_limit(margin: Side, limit: int) 🔗

Sets the camera limit for the specified Side. See also limit_bottom, limit_top, limit_left, and limit_right.

Please read the User-contributed notes policy before submitting a comment.

---

## Change scenes manually

**URL:** https://docs.godotengine.org/en/stable/tutorials/scripting/change_scenes_manually.html

**Contents:**
- Change scenes manually
- User-contributed notes

Sometimes it helps to have more control over how you swap scenes around. A Viewport's child nodes will render to the image it generates. This holds true even for nodes outside of the "current" scene. Autoloads fall into this category, and also scenes which you instantiate and add to the tree at runtime:

To complete the cycle and swap out the new scene with the old one, you have a choice to make. Many strategies exist for removing a scene from view of the Viewport. The tradeoffs involve balancing operation speed and memory consumption, as well as balancing data access and integrity.

Delete the existing scene. SceneTree.change_scene_to_file() and SceneTree.change_scene_to_packed() will delete the current scene immediately. You can also delete the main scene. Assuming the root node's name is "Main", you could do get_node("/root/Main").free() to delete the whole scene.

Pro: RAM is no longer dragging the dead weight.

Con: Returning to that scene is now more expensive since it must be loaded back into memory again (takes time AND memory). Not a problem if returning soon is unnecessary.

Con: No longer have access to that scene's data. Not a problem if using that data soon is unnecessary.

Note: It can be useful to preserve the data in a soon-to-be-deleted scene by re-attaching one or more of its nodes to a different scene, or even directly to the SceneTree.

Pro: No nodes means no processing, physics processing, or input handling. The CPU is available to work on the new scene's contents.

Con: Those nodes' processing and input handling no longer operate. Not a problem if using the updated data is unnecessary.

Hide the existing scene. By changing the visibility or collision detection of the nodes, you can hide the entire node sub-tree from the player's perspective.

Pro: You can still access the data if needed.

Pro: There's no need to move any more nodes around to save data.

Con: More data is being kept in memory, which will be become a problem on memory-sensitive platforms like web or mobile.

Processing continues.

Pro: Data continues to receive processing updates, so the scene will keep any data within it that relies on delta time or frame data updated.

Pro: Nodes are still members of groups (since groups belong to the SceneTree).

Con: The CPU's attention is now divided between both scenes. Too much load could result in low frame rates. You should be sure to test performance as you go to ensure the target platform can support the load from this approach.

Remove the existing scene from the tree. Assign a variable to the existing scene's root node. Then use Node.remove_child(Node) to detach the entire scene from the tree.

Memory still exists (similar pros/cons as hiding it from view).

Processing stops (similar pros/cons as deleting it completely).

Pro: This variation of "hiding" it is much easier to show/hide. Rather than potentially keeping track of multiple changes to the scene, you only need to call the add/remove_child methods. This is similar to disabling game objects in other engines.

Con: Unlike with hiding it from view only, the data contained within the scene will become stale if it relies on delta time, input, groups, or other data that is derived from SceneTree access.

There are also cases where you may wish to have many scenes present at the same time, such as adding your own singleton at runtime, or preserving a scene's data between scene changes (adding the scene to the root node).

Another case may be displaying multiple scenes at the same time using SubViewportContainers. This is optimal for rendering different content in different parts of the screen (e.g. minimaps, split-screen multiplayer).

Each option will have cases where it is best appropriate, so you must examine the effects of each approach, and determine what path best fits your unique situation.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var simultaneous_scene = preload("res://levels/level2.tscn").instantiate()

func _add_a_scene_manually():
    # This is like autoloading the scene, only
    # it happens after already loading the main scene.
    get_tree().root.add_child(simultaneous_scene)
```

Example 2 (json):
```json
public Node simultaneousScene;

public MyClass()
{
    simultaneousScene = ResourceLoader.Load<PackedScene>("res://levels/level2.tscn").Instantiate();
}

public void _AddASceneManually()
{
    // This is like autoloading the scene, only
    // it happens after already loading the main scene.
    GetTree().Root.AddChild(simultaneousScene);
}
```

Example 3 (unknown):
```unknown
get_tree().root.add_child(scene)
```

Example 4 (unknown):
```unknown
GetTree().Root.AddChild(scene);
```

---

## CSGShape3D

**URL:** https://docs.godotengine.org/en/stable/classes/class_csgshape3d.html

**Contents:**
- CSGShape3D
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: GeometryInstance3D < VisualInstance3D < Node3D < Node < Object

Inherited By: CSGCombiner3D, CSGPrimitive3D

This is the CSG base class that provides CSG operation support to the various CSG nodes in Godot.

Performance: CSG nodes are only intended for prototyping as they have a significant CPU performance cost. Consider baking final CSG operation results into static geometry that replaces the CSG nodes.

Individual CSG root node results can be baked to nodes with static resources with the editor menu that appears when a CSG root node is selected.

Individual CSG root nodes can also be baked to static resources with scripts by calling bake_static_mesh() for the visual mesh or bake_collision_shape() for the physics collision.

Entire scenes of CSG nodes can be baked to static geometry and exported with the editor glTF scene exporter: Scene > Export As... > glTF 2.0 Scene...

Prototyping levels with CSG

ConcavePolygonShape3D

bake_collision_shape()

get_collision_layer_value(layer_number: int) const

get_collision_mask_value(layer_number: int) const

is_root_shape() const

set_collision_layer_value(layer_number: int, value: bool)

set_collision_mask_value(layer_number: int, value: bool)

Operation OPERATION_UNION = 0

Geometry of both primitives is merged, intersecting geometry is removed.

Operation OPERATION_INTERSECTION = 1

Only intersecting geometry remains, the rest is removed.

Operation OPERATION_SUBTRACTION = 2

The second shape is subtracted from the first, leaving a dent with its shape.

bool calculate_tangents = true 🔗

void set_calculate_tangents(value: bool)

bool is_calculating_tangents()

Calculate tangents for the CSG shape which allows the use of normal and height maps. This is only applied on the root shape, this setting is ignored on any child. Setting this to false can speed up shape generation slightly.

int collision_layer = 1 🔗

void set_collision_layer(value: int)

int get_collision_layer()

The physics layers this area is in.

Collidable objects can exist in any of 32 different layers. These layers work like a tagging system, and are not visual. A collidable can use these layers to select with which objects it can collide, using the collision_mask property.

A contact is detected if object A is in any of the layers that object B scans, or object B is in any layer scanned by object A. See Collision layers and masks in the documentation for more information.

int collision_mask = 1 🔗

void set_collision_mask(value: int)

int get_collision_mask()

The physics layers this CSG shape scans for collisions. Only effective if use_collision is true. See Collision layers and masks in the documentation for more information.

float collision_priority = 1.0 🔗

void set_collision_priority(value: float)

float get_collision_priority()

The priority used to solve colliding when occurring penetration. Only effective if use_collision is true. The higher the priority is, the lower the penetration into the object will be. This can for example be used to prevent the player from breaking through the boundaries of a level.

Operation operation = 0 🔗

void set_operation(value: Operation)

Operation get_operation()

The operation that is performed on this shape. This is ignored for the first CSG child node as the operation is between this node and the previous child of this nodes parent.

void set_snap(value: float)

Deprecated: The CSG library no longer uses snapping.

This property does nothing.

bool use_collision = false 🔗

void set_use_collision(value: bool)

bool is_using_collision()

Adds a collision shape to the physics engine for our CSG shape. This will always act like a static body. Note that the collision shape is still active even if the CSG shape itself is hidden. See also collision_mask and collision_priority.

ConcavePolygonShape3D bake_collision_shape() 🔗

Returns a baked physics ConcavePolygonShape3D of this node's CSG operation result. Returns an empty shape if the node is not a CSG root node or has no valid geometry.

Performance: If the CSG operation results in a very detailed geometry with many faces physics performance will be very slow. Concave shapes should in general only be used for static level geometry and not with dynamic objects that are moving.

Note: CSG mesh data updates are deferred, which means they are updated with a delay of one rendered frame. To avoid getting an empty shape or outdated mesh data, make sure to call await get_tree().process_frame before using bake_collision_shape() in Node._ready() or after changing properties on the CSGShape3D.

ArrayMesh bake_static_mesh() 🔗

Returns a baked static ArrayMesh of this node's CSG operation result. Materials from involved CSG nodes are added as extra mesh surfaces. Returns an empty mesh if the node is not a CSG root node or has no valid geometry.

Note: CSG mesh data updates are deferred, which means they are updated with a delay of one rendered frame. To avoid getting an empty mesh or outdated mesh data, make sure to call await get_tree().process_frame before using bake_static_mesh() in Node._ready() or after changing properties on the CSGShape3D.

bool get_collision_layer_value(layer_number: int) const 🔗

Returns whether or not the specified layer of the collision_layer is enabled, given a layer_number between 1 and 32.

bool get_collision_mask_value(layer_number: int) const 🔗

Returns whether or not the specified layer of the collision_mask is enabled, given a layer_number between 1 and 32.

Array get_meshes() const 🔗

Returns an Array with two elements, the first is the Transform3D of this node and the second is the root Mesh of this node. Only works when this node is the root shape.

Note: CSG mesh data updates are deferred, which means they are updated with a delay of one rendered frame. To avoid getting an empty shape or outdated mesh data, make sure to call await get_tree().process_frame before using get_meshes() in Node._ready() or after changing properties on the CSGShape3D.

bool is_root_shape() const 🔗

Returns true if this is a root shape and is thus the object that is rendered.

void set_collision_layer_value(layer_number: int, value: bool) 🔗

Based on value, enables or disables the specified layer in the collision_layer, given a layer_number between 1 and 32.

void set_collision_mask_value(layer_number: int, value: bool) 🔗

Based on value, enables or disables the specified layer in the collision_mask, given a layer_number between 1 and 32.

Please read the User-contributed notes policy before submitting a comment.

---

## Curve

**URL:** https://docs.godotengine.org/en/stable/classes/class_curve.html

**Contents:**
- Curve
- Description
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

A mathematical curve.

This resource describes a mathematical curve by defining a set of points and tangents at each point. By default, it ranges between 0 and 1 on the X and Y axes, but these ranges can be changed.

Please note that many resources and nodes assume they are given unit curves. A unit curve is a curve whose domain (the X axis) is between 0 and 1. Some examples of unit curve usage are CPUParticles2D.angle_curve and Line2D.width_curve.

add_point(position: Vector2, left_tangent: float = 0, right_tangent: float = 0, left_mode: TangentMode = 0, right_mode: TangentMode = 0)

get_domain_range() const

get_point_left_mode(index: int) const

get_point_left_tangent(index: int) const

get_point_position(index: int) const

get_point_right_mode(index: int) const

get_point_right_tangent(index: int) const

get_value_range() const

remove_point(index: int)

sample(offset: float) const

sample_baked(offset: float) const

set_point_left_mode(index: int, mode: TangentMode)

set_point_left_tangent(index: int, tangent: float)

set_point_offset(index: int, offset: float)

set_point_right_mode(index: int, mode: TangentMode)

set_point_right_tangent(index: int, tangent: float)

set_point_value(index: int, y: float)

Emitted when max_domain or min_domain is changed.

Emitted when max_value or min_value is changed.

TangentMode TANGENT_FREE = 0

The tangent on this side of the point is user-defined.

TangentMode TANGENT_LINEAR = 1

The curve calculates the tangent on this side of the point as the slope halfway towards the adjacent point.

TangentMode TANGENT_MODE_COUNT = 2

The total number of available tangent modes.

int bake_resolution = 100 🔗

void set_bake_resolution(value: int)

int get_bake_resolution()

The number of points to include in the baked (i.e. cached) curve data.

float max_domain = 1.0 🔗

void set_max_domain(value: float)

float get_max_domain()

The maximum domain (x-coordinate) that points can have.

float max_value = 1.0 🔗

void set_max_value(value: float)

float get_max_value()

The maximum value (y-coordinate) that points can have. Tangents can cause higher values between points.

float min_domain = 0.0 🔗

void set_min_domain(value: float)

float get_min_domain()

The minimum domain (x-coordinate) that points can have.

float min_value = 0.0 🔗

void set_min_value(value: float)

float get_min_value()

The minimum value (y-coordinate) that points can have. Tangents can cause lower values between points.

int point_count = 0 🔗

void set_point_count(value: int)

int get_point_count()

The number of points describing the curve.

int add_point(position: Vector2, left_tangent: float = 0, right_tangent: float = 0, left_mode: TangentMode = 0, right_mode: TangentMode = 0) 🔗

Adds a point to the curve. For each side, if the *_mode is TANGENT_LINEAR, the *_tangent angle (in degrees) uses the slope of the curve halfway to the adjacent point. Allows custom assignments to the *_tangent angle if *_mode is set to TANGENT_FREE.

Recomputes the baked cache of points for the curve.

Removes duplicate points, i.e. points that are less than 0.00001 units (engine epsilon value) away from their neighbor on the curve.

void clear_points() 🔗

Removes all points from the curve.

float get_domain_range() const 🔗

Returns the difference between min_domain and max_domain.

TangentMode get_point_left_mode(index: int) const 🔗

Returns the left TangentMode for the point at index.

float get_point_left_tangent(index: int) const 🔗

Returns the left tangent angle (in degrees) for the point at index.

Vector2 get_point_position(index: int) const 🔗

Returns the curve coordinates for the point at index.

TangentMode get_point_right_mode(index: int) const 🔗

Returns the right TangentMode for the point at index.

float get_point_right_tangent(index: int) const 🔗

Returns the right tangent angle (in degrees) for the point at index.

float get_value_range() const 🔗

Returns the difference between min_value and max_value.

void remove_point(index: int) 🔗

Removes the point at index from the curve.

float sample(offset: float) const 🔗

Returns the Y value for the point that would exist at the X position offset along the curve.

float sample_baked(offset: float) const 🔗

Returns the Y value for the point that would exist at the X position offset along the curve using the baked cache. Bakes the curve's points if not already baked.

void set_point_left_mode(index: int, mode: TangentMode) 🔗

Sets the left TangentMode for the point at index to mode.

void set_point_left_tangent(index: int, tangent: float) 🔗

Sets the left tangent angle for the point at index to tangent.

int set_point_offset(index: int, offset: float) 🔗

Sets the offset from 0.5.

void set_point_right_mode(index: int, mode: TangentMode) 🔗

Sets the right TangentMode for the point at index to mode.

void set_point_right_tangent(index: int, tangent: float) 🔗

Sets the right tangent angle for the point at index to tangent.

void set_point_value(index: int, y: float) 🔗

Assigns the vertical position y to the point at index.

Please read the User-contributed notes policy before submitting a comment.

---

## C# signals

**URL:** https://docs.godotengine.org/en/stable/tutorials/scripting/c_sharp/c_sharp_signals.html

**Contents:**
- C# signals
- Signals as C# events
- Custom signals as C# events
- Signal emission
- Bound values
- Signal creation at runtime
- Using Connect and Disconnect
- Disconnecting automatically when the receiver is freed
  - No automatic disconnection: a lambda expression that captures a variable
  - No automatic disconnection: a custom signal

For a detailed explanation of signals in general, see the Using signals section in the step by step tutorial.

Signals are implemented using C# events, the idiomatic way to represent the observer pattern in C#. This is the recommended way to use signals in C# and the focus of this page.

In some cases it's necessary to use the older Connect() and Disconnect() APIs. See Using Connect and Disconnect for more details.

If you encounter a System.ObjectDisposedException while handling a signal, you might be missing a signal disconnection. See Disconnecting automatically when the receiver is freed for more details.

To provide more type-safety, Godot signals are also all available through events. You can handle these events, as any other event, with the += and -= operators.

In addition, you can always access signal names associated with a node type through its nested SignalName class. This is useful when, for example, you want to await on a signal (see await keyword).

To declare a custom event in your C# script, use the [Signal] attribute on a public delegate type. Note that the name of this delegate needs to end with EventHandler.

Once this is done, Godot will create the appropriate events automatically behind the scenes. You can then use said events as you'd do for any other Godot signal. Note that events are named using your delegate's name minus the final EventHandler part.

If you want to connect to these signals in the editor, you will need to (re)build the project to see them appear.

You can click the Build button in the upper-right corner of the editor to do so.

To emit signals, use the EmitSignal method. Note that, as for signals defined by the engine, your custom signal names are listed under the nested SignalName class.

In contrast with other C# events, you cannot use Invoke to raise events tied to Godot signals.

Signals support arguments of any Variant-compatible type.

Consequently, any Node or RefCounted will be compatible automatically, but custom data objects will need to inherit from GodotObject or one of its subclasses.

Sometimes you'll want to bind values to a signal when the connection is established, rather than (or in addition to) when the signal is emitted. To do so, you can use an anonymous function like in the following example.

Here, the Button.Pressed signal does not take any argument. But we want to use the same ModifyValue for both the "plus" and "minus" buttons. So we bind the modifier value at the time we're connecting the signals.

Finally, you can create custom signals directly while your game is running. Use the AddUserSignal method for that. Be aware that it should be executed before any use of said signals (either connecting to them or emitting them). Also, note that signals created this way won't be visible through the SignalName nested class.

In general, it isn't recommended to use Connect() and Disconnect(). These APIs don't provide as much type safety as the events. However, they're necessary for connecting to signals defined by GDScript and passing ConnectFlags.

In the following example, pressing the button for the first time prints Greetings!. OneShot disconnects the signal, so pressing the button again does nothing.

Normally, when any GodotObject is freed (such as any Node), Godot automatically disconnects all connections associated with that object. This happens for both signal emitters and signal receivers.

For example, a node with this code will print "Hello!" when the button is pressed, then free itself. Freeing the node disconnects the signal, so pressing the button again doesn't do anything:

When a signal receiver is freed while the signal emitter is still alive, in some cases automatic disconnection won't happen:

The signal is connected to a lambda expression that captures a variable.

The signal is a custom signal.

The following sections explain these cases in more detail and include suggestions for how to disconnect manually.

Automatic disconnection is totally reliable if a signal emitter is freed before any of its receivers are freed. With a project style that prefers this pattern, the above limits may not be a concern.

If you connect to a lambda expression that captures variables, Godot can't tell that the lambda is associated with the instance that created it. This causes this example to have potentially unexpected behavior:

On tick 4, the lambda expression tries to access the Name property of the node, but the node has already been freed. This causes the exception.

To disconnect, keep a reference to the delegate created by the lambda expression and pass that to -=. For example, this node connects and disconnects using the _EnterTree and _ExitTree lifecycle methods:

In this example, Free causes the node to leave the tree, which calls _ExitTree. _ExitTree disconnects the signal, so _tick is never called again.

The lifecycle methods to use depend on what the node does. Another option is to connect to signals in _Ready and disconnect in Dispose.

Godot uses Delegate.Target to determine what instance a delegate is associated with. When a lambda expression doesn't capture a variable, the generated delegate's Target is the instance that created the delegate. When a variable is captured, the Target instead points at a generated type that stores the captured variable. This is what breaks the association. If you want to see if a delegate will be automatically cleaned up, try checking its Target.

Callable.From doesn't affect the Delegate.Target, so connecting a lambda that captures variables using Connect doesn't work any better than +=.

Connecting to a custom signal using += doesn't disconnect automatically when the receiving node is freed.

To disconnect, use -= at an appropriate time. For example:

Another solution is to use Connect, which does disconnect automatically with custom signals:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (typescript):
```typescript
Timer myTimer = GetNode<Timer>("Timer");
myTimer.Timeout += () => GD.Print("Timeout!");
```

Example 2 (swift):
```swift
await ToSignal(GetTree(), SceneTree.SignalName.ProcessFrame);
```

Example 3 (json):
```json
[Signal]
public delegate void MySignalEventHandler();

[Signal]
public delegate void MySignalWithArgumentEventHandler(string myString);
```

Example 4 (gdscript):
```gdscript
public override void _Ready()
{
    MySignal += () => GD.Print("Hello!");
    MySignalWithArgument += SayHelloTo;
}

private void SayHelloTo(string name)
{
    GD.Print($"Hello {name}!");
}
```

---

## Exporting 3D scenes

**URL:** https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/exporting_3d_scenes.html

**Contents:**
- Exporting 3D scenes
- Overview
- Limitations
- User-contributed notes

In Godot, it is possible to export 3D scenes as a glTF 2.0 file. You can export as a glTF binary (.glb file) or glTF embedded with textures (gltf + .bin + textures). This allows you to create scenes in Godot, such as a CSG mesh blockout for a level, export it to clean it up in a program such as Blender, and then bring it back into Godot.

Only Blender 2.83 and newer can import glTF files exported by Godot.

To export a scene in the editor go to Scene > Export As... > glTF 2.0 Scene...

There are several limitations with glTF export.

No support for exporting particles since their implementation varies across engines.

ShaderMaterials cannot be exported.

No support for exporting 2D scenes.

3D scenes can be saved at runtime using runtime file loading and saving, including from an exported project.

Please read the User-contributed notes policy before submitting a comment.

---

## GLTFState

**URL:** https://docs.godotengine.org/en/stable/classes/class_gltfstate.html

**Contents:**
- GLTFState
- Description
- Tutorials
- Properties
- Methods
- Constants
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: FBXState

Represents all data of a glTF file.

Contains all nodes and resources of a glTF file. This is used by GLTFDocument as data storage, which allows GLTFDocument and all GLTFDocumentExtension classes to remain stateless.

GLTFState can be populated by GLTFDocument reading a file or by converting a Godot scene. Then the data can either be used to create a Godot scene or save to a glTF file. The code that converts to/from a Godot scene can be intercepted at arbitrary points by GLTFDocumentExtension classes. This allows for custom data to be stored in the glTF file or for custom data to be converted to/from Godot nodes.

Runtime file loading and saving

glTF asset header schema

Array[PackedByteArray]

import_as_skeleton_bones

add_used_extension(extension_name: String, required: bool)

append_data_to_buffers(data: PackedByteArray, deduplication: bool)

append_gltf_node(gltf_node: GLTFNode, godot_scene_node: Node, parent_node_index: int)

get_additional_data(extension_name: StringName)

get_animation_player(idx: int)

get_animation_players_count(idx: int)

Array[GLTFBufferView]

get_handle_binary_image()

get_node_index(scene_node: Node)

get_scene_node(idx: int)

Array[GLTFTextureSampler]

get_texture_samplers()

get_unique_animation_names()

set_accessors(accessors: Array[GLTFAccessor])

set_additional_data(extension_name: StringName, additional_data: Variant)

set_animations(animations: Array[GLTFAnimation])

set_buffer_views(buffer_views: Array[GLTFBufferView])

set_cameras(cameras: Array[GLTFCamera])

set_handle_binary_image(method: int)

set_images(images: Array[Texture2D])

set_lights(lights: Array[GLTFLight])

set_materials(materials: Array[Material])

set_meshes(meshes: Array[GLTFMesh])

set_nodes(nodes: Array[GLTFNode])

set_skeletons(skeletons: Array[GLTFSkeleton])

set_skins(skins: Array[GLTFSkin])

set_texture_samplers(texture_samplers: Array[GLTFTextureSampler])

set_textures(textures: Array[GLTFTexture])

set_unique_animation_names(unique_animation_names: Array[String])

set_unique_names(unique_names: Array[String])

HANDLE_BINARY_DISCARD_TEXTURES = 0 🔗

Discards all embedded textures and uses untextured materials.

HANDLE_BINARY_EXTRACT_TEXTURES = 1 🔗

Extracts embedded textures to be reimported and compressed. Editor only. Acts as uncompressed at runtime.

HANDLE_BINARY_EMBED_AS_BASISU = 2 🔗

Embeds textures VRAM compressed with Basis Universal into the generated scene.

HANDLE_BINARY_EMBED_AS_UNCOMPRESSED = 3 🔗

Embeds textures compressed losslessly into the generated scene, matching old behavior.

float bake_fps = 30.0 🔗

void set_bake_fps(value: float)

The baking fps of the animation for either import or export.

String base_path = "" 🔗

void set_base_path(value: String)

String get_base_path()

The folder path associated with this glTF data. This is used to find other files the glTF file references, like images or binary buffers. This will be set during import when appending from a file, and will be set during export when writing to a file.

Array[PackedByteArray] buffers = [] 🔗

void set_buffers(value: Array[PackedByteArray])

Array[PackedByteArray] get_buffers()

There is currently no description for this property. Please help us by contributing one!

String copyright = "" 🔗

void set_copyright(value: String)

String get_copyright()

The copyright string in the asset header of the glTF file. This is set during import if present and export if non-empty. See the glTF asset header documentation for more information.

bool create_animations = true 🔗

void set_create_animations(value: bool)

bool get_create_animations()

There is currently no description for this property. Please help us by contributing one!

String filename = "" 🔗

void set_filename(value: String)

String get_filename()

The file name associated with this glTF data. If it ends with .gltf, this is text-based glTF, otherwise this is binary GLB. This will be set during import when appending from a file, and will be set during export when writing to a file. If writing to a buffer, this will be an empty string.

PackedByteArray glb_data = PackedByteArray() 🔗

void set_glb_data(value: PackedByteArray)

PackedByteArray get_glb_data()

The binary buffer attached to a .glb file.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedByteArray for more details.

bool import_as_skeleton_bones = false 🔗

void set_import_as_skeleton_bones(value: bool)

bool get_import_as_skeleton_bones()

If true, forces all GLTFNodes in the document to be bones of a single Skeleton3D Godot node.

Dictionary json = {} 🔗

void set_json(value: Dictionary)

Dictionary get_json()

The original raw JSON document corresponding to this GLTFState.

int major_version = 0 🔗

void set_major_version(value: int)

int get_major_version()

There is currently no description for this property. Please help us by contributing one!

int minor_version = 0 🔗

void set_minor_version(value: int)

int get_minor_version()

There is currently no description for this property. Please help us by contributing one!

PackedInt32Array root_nodes = PackedInt32Array() 🔗

void set_root_nodes(value: PackedInt32Array)

PackedInt32Array get_root_nodes()

The root nodes of the glTF file. Typically, a glTF file will only have one scene, and therefore one root node. However, a glTF file may have multiple scenes and therefore multiple root nodes, which will be generated as siblings of each other and as children of the root node of the generated Godot scene.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedInt32Array for more details.

String scene_name = "" 🔗

void set_scene_name(value: String)

String get_scene_name()

The name of the scene. When importing, if not specified, this will be the file name. When exporting, if specified, the scene name will be saved to the glTF file.

bool use_named_skin_binds = false 🔗

void set_use_named_skin_binds(value: bool)

bool get_use_named_skin_binds()

There is currently no description for this property. Please help us by contributing one!

void add_used_extension(extension_name: String, required: bool) 🔗

Appends an extension to the list of extensions used by this glTF file during serialization. If required is true, the extension will also be added to the list of required extensions. Do not run this in GLTFDocumentExtension._export_post(), as that stage is too late to add extensions. The final list is sorted alphabetically.

int append_data_to_buffers(data: PackedByteArray, deduplication: bool) 🔗

Appends the given byte array data to the buffers and creates a GLTFBufferView for it. The index of the destination GLTFBufferView is returned. If deduplication is true, the buffers are first searched for duplicate data, otherwise new bytes are always appended.

int append_gltf_node(gltf_node: GLTFNode, godot_scene_node: Node, parent_node_index: int) 🔗

Appends the given GLTFNode to the state, and returns its new index. This can be used to export one Godot node as multiple glTF nodes, or inject new glTF nodes at import time. On import, this must be called before GLTFDocumentExtension._generate_scene_node() finishes for the parent node. On export, this must be called before GLTFDocumentExtension._export_node() runs for the parent node.

The godot_scene_node parameter is the Godot scene node that corresponds to this glTF node. This is highly recommended to be set to a valid node, but may be null if there is no corresponding Godot scene node. One Godot scene node may be used for multiple glTF nodes, so if exporting multiple glTF nodes for one Godot scene node, use the same Godot scene node for each.

The parent_node_index parameter is the index of the parent GLTFNode in the state. If -1, the node will be a root node, otherwise the new node will be added to the parent's list of children. The index will also be written to the GLTFNode.parent property of the new node.

Array[GLTFAccessor] get_accessors() 🔗

There is currently no description for this method. Please help us by contributing one!

Variant get_additional_data(extension_name: StringName) 🔗

Gets additional arbitrary data in this GLTFState instance. This can be used to keep per-file state data in GLTFDocumentExtension classes, which is important because they are stateless.

The argument should be the GLTFDocumentExtension name (does not have to match the extension name in the glTF file), and the return value can be anything you set. If nothing was set, the return value is null.

AnimationPlayer get_animation_player(idx: int) 🔗

Returns the AnimationPlayer node with the given index. These nodes are only used during the export process when converting Godot AnimationPlayer nodes to glTF animations.

int get_animation_players_count(idx: int) 🔗

Returns the number of AnimationPlayer nodes in this GLTFState. These nodes are only used during the export process when converting Godot AnimationPlayer nodes to glTF animations.

Array[GLTFAnimation] get_animations() 🔗

Returns an array of all GLTFAnimations in the glTF file. When importing, these will be generated as animations in an AnimationPlayer node. When exporting, these will be generated from Godot AnimationPlayer nodes.

Array[GLTFBufferView] get_buffer_views() 🔗

There is currently no description for this method. Please help us by contributing one!

Array[GLTFCamera] get_cameras() 🔗

Returns an array of all GLTFCameras in the glTF file. These are the cameras that the GLTFNode.camera index refers to.

int get_handle_binary_image() 🔗

There is currently no description for this method. Please help us by contributing one!

Array[Texture2D] get_images() 🔗

Gets the images of the glTF file as an array of Texture2Ds. These are the images that the GLTFTexture.src_image index refers to.

Array[GLTFLight] get_lights() 🔗

Returns an array of all GLTFLights in the glTF file. These are the lights that the GLTFNode.light index refers to.

Array[Material] get_materials() 🔗

There is currently no description for this method. Please help us by contributing one!

Array[GLTFMesh] get_meshes() 🔗

Returns an array of all GLTFMeshes in the glTF file. These are the meshes that the GLTFNode.mesh index refers to.

int get_node_index(scene_node: Node) 🔗

Returns the index of the GLTFNode corresponding to this Godot scene node. This is the inverse of get_scene_node(). Useful during the export process.

Note: Not every Godot scene node will have a corresponding GLTFNode, and not every GLTFNode will have a scene node generated. If there is no GLTFNode index for this scene node, -1 is returned.

Array[GLTFNode] get_nodes() 🔗

Returns an array of all GLTFNodes in the glTF file. These are the nodes that GLTFNode.children and root_nodes refer to. This includes nodes that may not be generated in the Godot scene, or nodes that may generate multiple Godot scene nodes.

Node get_scene_node(idx: int) 🔗

Returns the Godot scene node that corresponds to the same index as the GLTFNode it was generated from. This is the inverse of get_node_index(). Useful during the import process.

Note: Not every GLTFNode will have a scene node generated, and not every generated scene node will have a corresponding GLTFNode. If there is no scene node for this GLTFNode index, null is returned.

Array[GLTFSkeleton] get_skeletons() 🔗

Returns an array of all GLTFSkeletons in the glTF file. These are the skeletons that the GLTFNode.skeleton index refers to.

Array[GLTFSkin] get_skins() 🔗

Returns an array of all GLTFSkins in the glTF file. These are the skins that the GLTFNode.skin index refers to.

Array[GLTFTextureSampler] get_texture_samplers() 🔗

Retrieves the array of texture samplers that are used by the textures contained in the glTF.

Array[GLTFTexture] get_textures() 🔗

There is currently no description for this method. Please help us by contributing one!

Array[String] get_unique_animation_names() 🔗

Returns an array of unique animation names. This is only used during the import process.

Array[String] get_unique_names() 🔗

Returns an array of unique node names. This is used in both the import process and export process.

void set_accessors(accessors: Array[GLTFAccessor]) 🔗

There is currently no description for this method. Please help us by contributing one!

void set_additional_data(extension_name: StringName, additional_data: Variant) 🔗

Sets additional arbitrary data in this GLTFState instance. This can be used to keep per-file state data in GLTFDocumentExtension classes, which is important because they are stateless.

The first argument should be the GLTFDocumentExtension name (does not have to match the extension name in the glTF file), and the second argument can be anything you want.

void set_animations(animations: Array[GLTFAnimation]) 🔗

Sets the GLTFAnimations in the state. When importing, these will be generated as animations in an AnimationPlayer node. When exporting, these will be generated from Godot AnimationPlayer nodes.

void set_buffer_views(buffer_views: Array[GLTFBufferView]) 🔗

There is currently no description for this method. Please help us by contributing one!

void set_cameras(cameras: Array[GLTFCamera]) 🔗

Sets the GLTFCameras in the state. These are the cameras that the GLTFNode.camera index refers to.

void set_handle_binary_image(method: int) 🔗

There is currently no description for this method. Please help us by contributing one!

void set_images(images: Array[Texture2D]) 🔗

Sets the images in the state stored as an array of Texture2Ds. This can be used during export. These are the images that the GLTFTexture.src_image index refers to.

void set_lights(lights: Array[GLTFLight]) 🔗

Sets the GLTFLights in the state. These are the lights that the GLTFNode.light index refers to.

void set_materials(materials: Array[Material]) 🔗

There is currently no description for this method. Please help us by contributing one!

void set_meshes(meshes: Array[GLTFMesh]) 🔗

Sets the GLTFMeshes in the state. These are the meshes that the GLTFNode.mesh index refers to.

void set_nodes(nodes: Array[GLTFNode]) 🔗

Sets the GLTFNodes in the state. These are the nodes that GLTFNode.children and root_nodes refer to. Some of the nodes set here may not be generated in the Godot scene, or may generate multiple Godot scene nodes.

void set_skeletons(skeletons: Array[GLTFSkeleton]) 🔗

Sets the GLTFSkeletons in the state. These are the skeletons that the GLTFNode.skeleton index refers to.

void set_skins(skins: Array[GLTFSkin]) 🔗

Sets the GLTFSkins in the state. These are the skins that the GLTFNode.skin index refers to.

void set_texture_samplers(texture_samplers: Array[GLTFTextureSampler]) 🔗

Sets the array of texture samplers that are used by the textures contained in the glTF.

void set_textures(textures: Array[GLTFTexture]) 🔗

There is currently no description for this method. Please help us by contributing one!

void set_unique_animation_names(unique_animation_names: Array[String]) 🔗

Sets the unique animation names in the state. This is only used during the import process.

void set_unique_names(unique_names: Array[String]) 🔗

Sets the unique node names in the state. This is used in both the import process and export process.

Please read the User-contributed notes policy before submitting a comment.

---

## Godot notifications

**URL:** https://docs.godotengine.org/en/stable/tutorials/best_practices/godot_notifications.html

**Contents:**
- Godot notifications
- _process vs. _physics_process vs. *_input
- _init vs. initialization vs. export
- _ready vs. _enter_tree vs. NOTIFICATION_PARENTED
- User-contributed notes

Every Object in Godot implements a _notification method. Its purpose is to allow the Object to respond to a variety of engine-level callbacks that may relate to it. For example, if the engine tells a CanvasItem to "draw", it will call _notification(NOTIFICATION_DRAW).

Some of these notifications, like draw, are useful to override in scripts. So much so that Godot exposes many of them with dedicated functions:

_ready(): NOTIFICATION_READY

_enter_tree(): NOTIFICATION_ENTER_TREE

_exit_tree(): NOTIFICATION_EXIT_TREE

_process(delta): NOTIFICATION_PROCESS

_physics_process(delta): NOTIFICATION_PHYSICS_PROCESS

_draw(): NOTIFICATION_DRAW

What users might not realize is that notifications exist for types other than Node alone, for example:

Object::NOTIFICATION_POSTINITIALIZE: a callback that triggers during object initialization. Not accessible to scripts.

Object::NOTIFICATION_PREDELETE: a callback that triggers before the engine deletes an Object, i.e. a "destructor".

And many of the callbacks that do exist in Nodes don't have any dedicated methods, but are still quite useful.

Node::NOTIFICATION_PARENTED: a callback that triggers anytime one adds a child node to another node.

Node::NOTIFICATION_UNPARENTED: a callback that triggers anytime one removes a child node from another node.

One can access all these custom notifications from the universal _notification() method.

Methods in the documentation labeled as "virtual" are also intended to be overridden by scripts.

A classic example is the _init method in Object. While it has no NOTIFICATION_* equivalent, the engine still calls the method. Most languages (except C#) rely on it as a constructor.

So, in which situation should one use each of these notifications or virtual functions?

Use _process() when one needs a framerate-dependent delta time between frames. If code that updates object data needs to update as often as possible, this is the right place. Recurring logic checks and data caching often execute here, but it comes down to the frequency at which one needs the evaluations to update. If they don't need to execute every frame, then implementing a Timer-timeout loop is another option.

Use _physics_process() when one needs a framerate-independent delta time between frames. If code needs consistent updates over time, regardless of how fast or slow time advances, this is the right place. Recurring kinematic and object transform operations should execute here.

While it is possible, to achieve the best performance, one should avoid making input checks during these callbacks. _process() and _physics_process() will trigger at every opportunity (they do not "rest" by default). In contrast, *_input() callbacks will trigger only on frames in which the engine has actually detected the input.

One can check for input actions within the input callbacks just the same. If one wants to use delta time, one can fetch it from the related delta time methods as needed.

If the script initializes its own node subtree, without a scene, that code should execute in _init(). Other property or SceneTree-independent initializations should also run here.

The C# equivalent to GDScript's _init() method is the constructor.

_init() triggers before _enter_tree() or _ready(), but after a script creates and initializes its properties. When instantiating a scene, property values will set up according to the following sequence:

Initial value assignment: the property is assigned its initialization value, or its default value if one is not specified. If a setter exists, it is not used.

_init() assignment: the property's value is replaced by any assignments made in _init(), triggering the setter.

Exported value assignment: an exported property's value is again replaced by any value set in the Inspector, triggering the setter.

As a result, instantiating a script versus a scene may affect both the initialization and the number of times the engine calls the setter.

When instantiating a scene connected to the first executed scene, Godot will instantiate nodes down the tree (making _init() calls) and build the tree going downwards from the root. This causes _enter_tree() calls to cascade down the tree. Once the tree is complete, leaf nodes call _ready. A node will call this method once all child nodes have finished calling theirs. This then causes a reverse cascade going up back to the tree's root.

When instantiating a script or a standalone scene, nodes are not added to the SceneTree upon creation, so no _enter_tree() callbacks trigger. Instead, only the _init() call occurs. When the scene is added to the SceneTree, the _enter_tree() and _ready() calls occur.

If one needs to trigger behavior that occurs as nodes parent to another, regardless of whether it occurs as part of the main/active scene or not, one can use the PARENTED notification. For example, here is a snippet that connects a node's method to a custom signal on the parent node without failing. Useful on data-centric nodes that one might create at runtime.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
# Allows for recurring operations that don't trigger script logic
# every frame (or even every fixed frame).
func _ready():
    var timer = Timer.new()
    timer.autostart = true
    timer.wait_time = 0.5
    add_child(timer)
    timer.timeout.connect(func():
        print("This block runs every 0.5 seconds")
    )
```

Example 2 (gdscript):
```gdscript
using Godot;

public partial class MyNode : Node
{
    // Allows for recurring operations that don't trigger script logic
    // every frame (or even every fixed frame).
    public override void _Ready()
    {
        var timer = new Timer();
        timer.Autostart = true;
        timer.WaitTime = 0.5;
        AddChild(timer);
        timer.Timeout += () => GD.Print("This block runs every 0.5 seconds");
    }
}
```

Example 3 (php):
```php
using namespace godot;

class MyNode : public Node {
    GDCLASS(MyNode, Node)

public:
    // Allows for recurring operations that don't trigger script logic
    // every frame (or even every fixed frame).
    virtual void _ready() override {
        Timer *timer = memnew(Timer);
        timer->set_autostart(true);
        timer->set_wait_time(0.5);
        add_child(timer);
        timer->connect("timeout", callable_mp(this, &MyNode::run));
    }

    void run() {
        UtilityFunctions::print("This block runs every 0.5 seconds.");
    }
};
```

Example 4 (gdscript):
```gdscript
# Called every frame, even when the engine detects no input.
func _process(delta):
    if Input.is_action_just_pressed("ui_select"):
        print(delta)

# Called during every input event.
func _unhandled_input(event):
    match event.get_class():
        "InputEventKey":
            if Input.is_action_just_pressed("ui_accept"):
                print(get_process_delta_time())
```

---

## Groups

**URL:** https://docs.godotengine.org/en/stable/tutorials/scripting/groups.html

**Contents:**
- Groups
- Managing groups
  - Using the Node dock
  - Using code
- User-contributed notes

Groups in Godot work like tags in other software. You can add a node to as many groups as you want. Then, in code, you can use the SceneTree to:

Get a list of nodes in a group.

Call a method on all nodes in a group.

Send a notification to all nodes in a group.

This is a useful feature to organize large scenes and decouple code.

Groups are created by adding a node to a new group name, and likewise they are removed by removing all nodes from a given group.

There are two ways to add/remove nodes to groups:

During design, by using the Node dock in the editor, or the Global Groups in project settings.

During execution, by calling Node.add_to_group() or Node.remove_from_group().

You can create new groups using the Groups tab in the Node dock.

Select a node in the Scene dock then click the add button with the + symbol.

You should now see the Create New Group modal appear. Write the group name in the field.

You can optionally mark the option "Global", which will make the group visible project-wide, and able to be reused in any project scene. This will also allow you to give it a description.

When done, press Ok to create it.

You should see the new groups appear in the Groups tab under Scene Groups if the Global option was unmarked, or under Global Groups if that option was marked.

A selected Node from the Scene dock can be added into groups by marking the checkbox on the left side of the groups in the Groups dock. The node you had selected when creating a new group will be automatically checked.

All groups present in the project that were marked as Global, created from any scene, will be visible under Global Groups.

Any other group derived from nodes in the current scene will appear under Scene Groups.

The same underlying logic is used for both Global and Scene groups. Groups with the same name are considered one and the same. This feature is purely organizational.

You can manage Global Groups in the Global Groups dock, inside Project Settings. There, you will be able to add new global groups, or change existing groups' names and descriptions.

You can also manage groups from scripts. The following code adds the node to which you attach the script to the guards group as soon as it enters the scene tree.

Imagine you're creating an infiltration game. When an enemy spots the player, you want all guards and robots to be on alert.

In the fictional example below, we use SceneTree.call_group() to alert all enemies that the player was spotted.

The above code calls the function enter_alert_mode on every member of the group guards.

To get the full list of nodes in the guards group as an array, you can call SceneTree.get_nodes_in_group():

The SceneTree class provides many more useful methods to interact with scenes, their node hierarchy, and groups. It allows you to switch scenes easily or reload them, quit the game or pause and unpause it. It also provides useful signals.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    add_to_group("guards")
```

Example 2 (gdscript):
```gdscript
public override void _Ready()
{
    base._Ready();

    AddToGroup("guards");
}
```

Example 3 (go):
```go
func _on_player_spotted():
    get_tree().call_group("guards", "enter_alert_mode")
```

Example 4 (json):
```json
public void _OnPlayerDiscovered()
{
    GetTree().CallGroup("guards", "enter_alert_mode");
}
```

---

## Importing 3D scenes

**URL:** https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/index.html

**Contents:**
- Importing 3D scenes

Godot supports importing 3D scenes from various file formats. This documentation section describes what those formats are, and how to use them, including exporting with the correct conventions and best practices, and how to customize the node type using a suffix in the node name. The import configuration article describes how to customize the imported data using the import dock, the advanced import settings dialog, and inherited scenes.

3D scenes can be loaded at runtime using runtime file loading and saving, including from an exported project.

---

## Import configuration

**URL:** https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/import_configuration.html

**Contents:**
- Import configuration
- Import workflows
  - Using the Import dock
  - Using import scripts for automation
  - Using animation libraries
  - Filter script
- Scene inheritance
- User-contributed notes

Godot provides several ways to customize the imported data, such as the import dock, the advanced import setting dialog, and inherited scenes. This can be used to make further changes to the imported scene, such as adjusting meshes, adding physics information, and adding new nodes. You can also write a script that runs code at the end of the import process to perform arbitrary customization.

Note that, when applicable, modifying the original data should be preferred to configuring the scene after import. This helps minimize the differences between the 3D modeling application and the imported scene. See the Model export considerations and Node type customization using name suffixes articles for more information.

Since Godot can only save its own scene format (.tscn/.scn), Godot cannot save over the original 3D scene file (which uses a different format). This is also a safer approach as it avoids making accidental changes to the source file.

To allow customizing the scene and its materials, Godot's scene importer allows for different workflows regarding how data is imported.

Import dock after selecting a 3D scene in the FileSystem dock

This import process is customizable using 3 separate interfaces, depending on your needs:

The Import dock, after selecting the 3D scene by clicking it once in the FileSystem dock.

The Advanced Import Settings dialog, which can be accessed by double-clicking the 3D scene in the FileSystem dock or by clicking the Advanced… button in the Import dock. This allows you to customize per-object options in Godot, and preview models and animations. please see the Advanced Import Settings page for more information.

Import hints, which are special suffixes added to object names in the 3D modeling software. This allows you to customize per-object options in the 3D modeling software.

For basic customization, using the Import dock suffices. However, for more complex operations such as defining material overrides on a per-material basis, you'll need to use the Advanced Import Settings dialog, import hints, or possibly both.

The following options can be adjusted in the Import dock after selecting a 3D scene in the FileSystem dock:

Root Type: The node type to use as a root node. Using node types that inherit from Node3D is recommended. Otherwise, you'll lose the ability to position the node directly in the 3D editor.

Root Name: The name of the root node in the imported scene. This is generally not noticeable when instancing the scene in the editor (or drag-and-dropping from the FileSystem dock), as the root node is renamed to match the filename in this case.

Apply Root Scale: If enabled, Root Scale will be applied on the meshes and animations directly, while keeping the root node's scale to the default (1, 1, 1). This means that if you add a child node later on within the imported scene, it won't be scaled. If disabled, Root Scale will multiply the scale of the root node instead.

Ensure Tangents: If checked, generate vertex tangents using Mikktspace if the input meshes don't have tangent data. When possible, it's recommended to let the 3D modeling software generate tangents on export instead on relying on this option. Tangents are required for correct display of normal and height maps, along with any material/shader features that require tangents. If you don't need material features that require tangents, disabling this can reduce output file size and speed up importing if the source 3D file doesn't contain tangents.

Generate LODs: If checked, generates lower detail variants of the mesh which will be displayed in the distance to improve rendering performance. Not all meshes benefit from LOD, especially if they are never rendered from far away. Disabling this can reduce output file size and speed up importing. See Mesh level of detail (LOD) for more information.

Create Shadow Meshes: If checked, enables the generation of shadow meshes on import. This optimizes shadow rendering without reducing quality by welding vertices together when possible. This in turn reduces the memory bandwidth required to render shadows. Shadow mesh generation currently doesn't support using a lower detail level than the source mesh (but shadow rendering will make use of LODs when relevant).

Light Baking: Configures the meshes' global illumination mode in the 3D scene. If set to Static Lightmaps, sets the meshes' GI mode to Static and generates UV2 on import for lightmap baking.

Lightmap Texel Size: Only visible if Light Baking is set to Static Lightmaps. Controls the size of each texel on the baked lightmap. A smaller value results in more precise lightmaps, at the cost of larger lightmap sizes and longer bake times.

Use Named Skins: If checked, use named Skins for animation. The MeshInstance3D node contains 3 properties of relevance here: a skeleton NodePath pointing to the Skeleton3D node (usually ..), a mesh, and a skin:

The Skeleton3D node contains a list of bones with names, their pose and rest, a name and a parent bone.

The mesh is all of the raw vertex data needed to display a mesh. In terms of the mesh, it knows how vertices are weight-painted and uses some internal numbering often imported from 3D modeling software.

The skin contains the information necessary to bind this mesh onto this Skeleton3D. For every one of the internal bone IDs chosen by the 3D modeling software, it contains two things. Firstly, a Matrix known as the Bind Pose Matrix, Inverse Bind Matrix, or IBM for short. Secondly, the Skin contains each bone's name (if Use Named Skins is enabled), or the bone's index within the Skeleton3D list (if Use Named Skins is disabled).

Together, this information is enough to tell Godot how to use the bone poses in the Skeleton3D node to render the mesh from each MeshInstance3D. Note that each MeshInstance3D may share binds, as is common in models exported from Blender, or each MeshInstance3D may use a separate Skin object, as is common in models exported from other tools such as Maya.

Import: If checked, import animations from the 3D scene.

FPS: The number of frames per second to use for baking animation curves to a series of points with linear interpolation. It's recommended to configure this value to match the value you're using as a baseline in your 3D modeling software. Higher values result in more precise animation with fast movement changes, at the cost of higher file sizes and memory usage. Thanks to interpolation, there is usually not much benefit in going above 30 FPS (as the animation will still appear smooth at higher rendering framerates).

Trimming: Trim the beginning and end of animations if there are no keyframe changes. This can reduce output file size and memory usage with certain 3D scenes, depending on the contents of their animation tracks.

Remove Immutable Tracks: Remove animation tracks that only contain default values. This can reduce output file size and memory usage with certain 3D scenes, depending on the contents of their animation tracks.

Path: Path to an import script, which can run code after the import process has completed for custom processing. See Using import scripts for automation for more information.

Embedded Texture Handling: Controls how textures embedded within glTF scenes should be handled. Discard All Textures will not import any textures, which is useful if you wish to manually set up materials in Godot instead. Extract Textures extracts textures to external images, resulting in smaller file sizes and more control over import options. Embed as Basis Universal and Embed as Uncompressed keeps the textures embedded in the imported scene, with and without VRAM compression respectively.

Importer Which import method is used. ubfx handles fbx files as fbx files. FBX2glTF converts FBX files to glTF on import and requires additional setup. FBX2glTF is not recommended unless you have a specific rason to use it over ufbx or working with a different file format.

Allow Geometry Helper Nodes enables or disables geometry helper nodes

Embedded Texture Handling: Controls how textures embedded within fbx scenes should be handled. Discard All Textures will not import any textures, which is useful if you wish to manually set up materials in Godot instead. Extract Textures extracts textures to external images, resulting in smaller file sizes and more control over import options. Embed as Basis Universal and Embed as Uncompressed keeps the textures embedded in the imported scene, with and without VRAM compression respectively.

Blender-specific options

Only visible for .blend files.

Visible: All imports everything, even invisible objects. Visible Only only imports visible objects. Renderable only imports objects that are marked as renderable in Blender, regardless of whether they are actually visible. In Blender, renderability is toggled by clicking the camera icon next to each object in the Outliner, while visibility is toggled by the eye icon.

Active Collection Only: If checked, only imports nodes that are in the active collection in Blender.

Punctual Lights: If checked, imports lights (directional, omni, and spot) from Blender. "Punctual" is not to be confused with "positional", which is why directional lights are also included.

Cameras: If checked, imports cameras from Blender.

Custom Properties: If checked, imports custom properties from Blender as glTF extras. This data can then be used from an editor plugin that uses GLTFDocument.register_gltf_document_extension(), which can set node metadata on import (among other use cases).

Modifiers: If set to No Modifiers, object modifiers are ignored on import. If set to All Modifiers, applies modifiers to objects on import.

Colors: If checked, imports vertex colors from Blender.

UVs: If checked, imports vertex UV1 and UV2 from Blender.

Normals: If checked, imports vertex normals from Blender.

Export Geometry Nodes Instances: If checked, imports geometry node instances from Blender.

Tangents: If checked, imports vertex tangents from Blender.

Skins: None skips skeleton skin data import from Blender. 4 Influences (Compatible) imports skin data to be compatible with all renderers, at the cost of lower precision for certain rigs. All Influences imports skin data with all influences (up to 8 in Godot), which is more precise but may not be compatible with all renderers.

Export Bones Deforming Mesh Only: If checked, only imports bones that deform the mesh from Blender.

Unpack Enabled: If checked, unpacks the original images to the Godot filesystem and uses them. This allows changing image import settings like VRAM compression. If unchecked, allows Blender to convert the original images, such as repacking roughness and metallic into one roughness + metallic texture. In most cases, this option should be left checked, but if the .blend file's images aren't in the correct format, this must be disabled for correct behavior.

Export Materials: If set to Placeholder, does not import materials, but keeps surface slots so that separate materials can be assigned to different surfaces. If set to Export, imports materials as-is (note that procedural Blender materials may not work correctly). If set to Named Placeholder, imports materials, but doesn't import images that are packed into the .blend file. Textures will have to be reassigned manually in the imported materials.

Limit Playback: If checked, limits animation import to the playback range defined in Blender (the Start and End options at the right of the animation timeline in Blender). This can avoid including unused animation data, making the imported scene smaller and faster to load. However, this can also result in missing animation data if the playback range is not set correctly in Blender.

Always Sample: If checked, forces animation sampling on import to ensure consistency between how Blender and glTF perform animation interpolation, at the cost of larger file sizes. If unchecked, there may be differences in how animations are interpolated between what you see in Blender and the imported scene in Godot, due to different interpolation semantics between both.

Group Tracks: If checked, imports animations (actives and on NLA tracks) as separate tracks. If unchecked, all the currently assigned actions become one glTF animation.

A special script to process the whole scene after import can be provided. This is great for post-processing, changing materials, doing funny stuff with the geometry, and more.

Create a script that is not attached to any node by right-clicking in the FileSystem dock and choosing New > Script…. In the script editor, write the following:

The _post_import(scene: Node) function takes the imported scene as argument (the parameter is actually the root node of the scene). The scene that will finally be used must be returned (even if the scene can be entirely different).

To use your script, locate the script in the import tab's "Path" option under the "Import Script" category.

As of Godot 4.0, you can choose to import only animations from a glTF file and nothing else. This is used in some asset pipelines to distribute animations separately from models. For example, this allows you to use one set of animations for several characters, without having to duplicate animation data in every character.

To do so, select the glTF file in the FileSystem dock, then change the import mode to Animation Library in the Import dock:

Changing the import type to Animation Library in the Import dock

Click Reimport and restart the editor when prompted. After restarting, the glTF file will be imported as an AnimationLibrary instead of a PackedScene. This animation library can then be referenced in an AnimationPlayer node.

The import options that are visible after changing the import mode to Animation Library act the same as when using the Scene import mode. See Using the Import dock for more information.

It is possible to specify a filter script in a special syntax to decide which tracks from which animations should be kept.

The filter script is executed against each imported animation. The syntax consists of two types of statements, the first for choosing which animations to filter, and the second for filtering individual tracks within the matched animation. All name patterns are performed using a case-insensitive expression match, with support for ? and * wildcards (using String.matchn() under the hood).

The script must start with an animation filter statement (as denoted by the line beginning with an @). For example, if we would like to apply filters to all imported animations which have a name ending in "_Loop":

Similarly, additional patterns can be added to the same line, separated by commas. Here is a modified example to additionally include all animations with names that begin with "Arm_Left", but also exclude all animations which have names ending in "Attack":

Following the animation selection filter statement, we add track filtering patterns to indicate which animation tracks should be kept or discarded. If no track filter patterns are specified, then all tracks within the matched animations will be discarded!

It's important to note that track filter statements are applied in order for each track within the animation, this means that one line may include a track, a later rule can still discard it. Similarly, a track excluded by an early rule may then be re-included once again by a filter rule further down in the filter script.

For example: include all tracks in animations with names ending in "_Loop", but discard any tracks affecting a "Skeleton" which end in "Control", unless they have "Arm" in their name:

In the above example, tracks like "Skeleton:Leg_Control" would be discarded, while tracks such as "Skeleton:Head" or "Skeleton:Arm_Left_Control" would be retained.

Any track filter lines that do not begin with a + or - are ignored.

In many cases, it may be desired to make manual modifications to the imported scene. By default, this is not possible because if the source 3D asset changes, Godot will re-import the whole scene.

However, it is possible to make local modifications by using scene inheritance. If you try to open the imported scene using Scene > Open Scene… or Scene > Quick Open Scene…, the following dialog will appear:

Dialog when opening an imported 3D scene in the editor

In inherited scenes, the only limitations for modification are:

Nodes from the base scene can't be removed, but additional nodes can be added anywhere.

Subresources can't be edited. Instead, you need to save them externally as described above.

Other than that, everything is allowed.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
@tool # Needed so it runs in editor.
extends EditorScenePostImport

# This sample changes all node names.
# Called right after the scene is imported and gets the root node.
func _post_import(scene):
    # Change all node names to "modified_[oldnodename]"
    iterate(scene)
    return scene # Remember to return the imported scene

# Recursive function that is called on every node
# (for demonstration purposes; EditorScenePostImport only requires a `_post_import(scene)` function).
func iterate(node):
    if node != null:
        print_rich("Post-import: [b]%s[/b] -> [b]%s[/b]" % [node.name, "modified_" + node.name])
        node.name = "modified_" + node.name
        for child in node.get_children():
            iterate(child)
```

Example 2 (unknown):
```unknown
@+*_Loop, +Arm_Left*, -*Attack
```

Example 3 (unknown):
```unknown
@+*_Loop
+*
-Skeleton:*Control
+*Arm*
```

---

## Instancing with signals

**URL:** https://docs.godotengine.org/en/stable/tutorials/scripting/instancing_with_signals.html

**Contents:**
- Instancing with signals
- Shooting example
- User-contributed notes

Signals provide a way to decouple game objects, allowing you to avoid forcing a fixed arrangement of nodes. One sign that a signal might be called for is when you find yourself using get_parent(). Referring directly to a node's parent means that you can't easily move that node to another location in the scene tree. This can be especially problematic when you are instancing objects at runtime and may want to place them in an arbitrary location in the running scene tree.

Below we'll consider an example of such a situation: firing bullets.

Consider a player character that can rotate and shoot towards the mouse. Every time the mouse button is clicked, we create an instance of the bullet at the player's location. See Creating instances for details.

We'll use an Area2D for the bullet, which moves in a straight line at a given velocity:

However, if the bullets are added as children of the player, then they will remain "attached" to the player as it rotates:

Instead, we need the bullets to be independent of the player's movement - once fired, they should continue traveling in a straight line and the player can no longer affect them. Instead of being added to the scene tree as a child of the player, it makes more sense to add the bullet as a child of the "main" game scene, which may be the player's parent or even further up the tree.

You could do this by adding the bullet to the main scene directly:

However, this will lead to a different problem. Now if you try to test your "Player" scene independently, it will crash on shooting, because there is no parent node to access. This makes it a lot harder to test your player code independently and also means that if you decide to change your main scene's node structure, the player's parent may no longer be the appropriate node to receive the bullets.

The solution to this is to use a signal to "emit" the bullets from the player. The player then has no need to "know" what happens to the bullets after that - whatever node is connected to the signal can "receive" the bullets and take the appropriate action to spawn them.

Here is the code for the player using signals to emit the bullet:

In the main scene, we then connect the player's signal (it will appear in the "Node" tab of the Inspector)

Now the bullets will maintain their own movement independent of the player's rotation:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Area2D

var velocity = Vector2.RIGHT

func _physics_process(delta):
    position += velocity * delta
```

Example 2 (csharp):
```csharp
using Godot;

public partial class Bullet : Area2D
{
    public Vector2 Velocity { get; set; } = Vector2.Right;

    public override void _PhysicsProcess(double delta)
    {
        Position += Velocity * (float)delta;
    }
}
```

Example 3 (gdscript):
```gdscript
var bullet_instance = Bullet.instantiate()
get_parent().add_child(bullet_instance)
```

Example 4 (unknown):
```unknown
Node bulletInstance = Bullet.Instantiate();
GetParent().AddChild(bulletInstance);
```

---

## Model export considerations

**URL:** https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/model_export_considerations.html

**Contents:**
- Model export considerations
- 3D asset direction conventions
- Exporting textures separately
- Exporting considerations
- Lighting considerations
- User-contributed notes

Before exporting a 3D model from a 3D modeling application, such as Blender, there are some considerations that should be taken into account to ensure that the model follows the conventions and best practices for Godot.

Godot uses a right-handed, Y-is-up coordinate system, with the -Z axis as the camera's forward direction. This is the same as OpenGL. This implies that +Z is back, +X is right, and -X is left for a camera.

The convention for 3D assets is to face the opposite direction as the camera, so that characters and other assets are facing the camera by default. This convention is extremely common in 3D modeling applications, and is codified in glTF as part of the glTF 2.0 specification. This means that for oriented 3D assets (such as characters), the +Z axis is the direction of the front, so -Z is the rear, +X is the left side, and -X is the right side for a 3D asset. In Blender, this means that +Y is rear and -Y is front for an asset.

When rotating an oriented 3D asset in Godot, use the use_model_front option on the look_at functions, and use the Vector3.MODEL_* constants to perform calculations in the oriented asset's local space.

For assets without an intrinsic front side or forward direction, such as a game map or terrain, take note of the cardinal directions instead. The convention in Godot and the vast majority of other applications is that +X is east and -X is west. Due to Godot's right-handed Y-is-up coordinate system, this implies that +Z is south and -Z is north. In Blender, this means that +Y is north and -Y is south.

While textures can be exported with a model in certain file formats, such as glTF 2.0, you can also export them separately. Godot uses PBR (physically based rendering) for its materials, so if a texturing program can export PBR textures, they can work in Godot. This includes the Substance suite, ArmorPaint (open source), and Material Maker (open source).

For more information on Godot's materials, see Standard Material 3D and ORM Material 3D.

Since GPUs can only render triangles, meshes that contain quads or N-gons have to be triangulated before they can be rendered. Godot can triangulate meshes on import, but results may be unpredictable or incorrect, especially with N-gons. Regardless of the target application, triangulating before exporting the scene will lead to more consistent results and should be done whenever possible.

To avoid issues with incorrect triangulation after importing in Godot, it is recommended to make the 3D modeling software triangulate objects on its own. In Blender, this can be done by adding a Triangulate modifier to your objects and making sure Apply Modifiers is checked in the export dialog. Alternatively, depending on the exporter, you may be able to find and enable a Triangulate Faces option in the export dialog.

To avoid issues with 3D selection in the editor, it is recommended to apply the object transform in the 3D modeling software before exporting the scene.

It is important that the mesh is not deformed by bones when exporting. Make sure that the skeleton is reset to its T-pose or default rest pose before exporting with your favorite 3D editor.

While it's possible to import lights from a 3D scene using the glTF, .blend or Collada formats, it's generally advised to design the scene's lighting in the Godot editor after importing the scene.

This allows you to get a more accurate feel for the final result, as different engines will render lights in a different manner. This also avoids any issues with lights appearing excessively strong or faint as a result of the import process.

Please read the User-contributed notes policy before submitting a comment.

---

## MultiplayerSpawner

**URL:** https://docs.godotengine.org/en/stable/classes/class_multiplayerspawner.html

**Contents:**
- MultiplayerSpawner
- Description
- Properties
- Methods
- Signals
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Node < Object

Automatically replicates spawnable nodes from the authority to other multiplayer peers.

Spawnable scenes can be configured in the editor or through code (see add_spawnable_scene()).

Also supports custom node spawns through spawn(), calling spawn_function on all peers.

Internally, MultiplayerSpawner uses MultiplayerAPI.object_configuration_add() to notify spawns passing the spawned node as the object and itself as the configuration, and MultiplayerAPI.object_configuration_remove() to notify despawns in a similar way.

add_spawnable_scene(path: String)

clear_spawnable_scenes()

get_spawnable_scene(index: int) const

get_spawnable_scene_count() const

spawn(data: Variant = null)

despawned(node: Node) 🔗

Emitted when a spawnable scene or custom spawn was despawned by the multiplayer authority. Only called on remote peers.

spawned(node: Node) 🔗

Emitted when a spawnable scene or custom spawn was spawned by the multiplayer authority. Only called on remote peers.

Callable spawn_function 🔗

void set_spawn_function(value: Callable)

Callable get_spawn_function()

Method called on all peers when a custom spawn() is requested by the authority. Will receive the data parameter, and should return a Node that is not in the scene tree.

Note: The returned node should not be added to the scene with Node.add_child(). This is done automatically.

int spawn_limit = 0 🔗

void set_spawn_limit(value: int)

int get_spawn_limit()

Maximum number of nodes allowed to be spawned by this spawner. Includes both spawnable scenes and custom spawns.

When set to 0 (the default), there is no limit.

NodePath spawn_path = NodePath("") 🔗

void set_spawn_path(value: NodePath)

NodePath get_spawn_path()

Path to the spawn root. Spawnable scenes that are added as direct children are replicated to other peers.

void add_spawnable_scene(path: String) 🔗

Adds a scene path to spawnable scenes, making it automatically replicated from the multiplayer authority to other peers when added as children of the node pointed by spawn_path.

void clear_spawnable_scenes() 🔗

Clears all spawnable scenes. Does not despawn existing instances on remote peers.

String get_spawnable_scene(index: int) const 🔗

Returns the spawnable scene path by index.

int get_spawnable_scene_count() const 🔗

Returns the count of spawnable scene paths.

Node spawn(data: Variant = null) 🔗

Requests a custom spawn, with data passed to spawn_function on all peers. Returns the locally spawned node instance already inside the scene tree, and added as a child of the node pointed by spawn_path.

Note: Spawnable scenes are spawned automatically. spawn() is only needed for custom spawns.

Please read the User-contributed notes policy before submitting a comment.

---

## Nodes and scene instances

**URL:** https://docs.godotengine.org/en/stable/tutorials/scripting/nodes_and_scene_instances.html

**Contents:**
- Nodes and scene instances
- Getting nodes
- Node paths
  - Syntactic sugar
- Creating nodes
- Instancing scenes
- User-contributed notes

This guide explains how to get nodes, create nodes, add them as a child, and instantiate scenes from code.

Check the Creating instances tutorial to learn about Godot's approach to scene instancing.

You can get a reference to a node by calling the Node.get_node() method. For this to work, the child node must be present in the scene tree. Getting it in the parent node's _ready() function guarantees that.

If, for example, you have a scene tree like this, and you want to get a reference to the Sprite2D and Camera2D nodes to access them in your script.

To do so, you can use the following code.

Note that you get nodes using their name, not their type. Above, "Sprite2D" and "Camera2D" are the nodes' names in the scene.

If you rename the Sprite2D node as Skin in the Scene dock, you have to change the line that gets the node to get_node("Skin") in the script.

When getting a reference to a node, you're not limited to getting a direct child. The get_node() function supports paths, a bit like when working with a file browser. Add a slash to separate nodes.

Take the following example scene, with the script attached to the UserInterface node.

To get the AnimationPlayer node, you would use the following code.

As with file paths, you can use ".." to get a parent node. The best practice is to avoid doing that though not to break encapsulation. You can also start the path with a forward slash to make it absolute, in which case your topmost node would be "/root", the application's predefined root viewport.

You can use two shorthands to shorten your code in GDScript. Firstly, putting the @onready annotation before a member variable makes it initialize right before the _ready() callback.

There is also a short notation for get_node(): the dollar sign, "$". You place it before the name or path of the node you want to get.

To create a node from code, call its new() method like for any other class-based datatype.

You can store the newly created node's reference in a variable and call add_child() to add it as a child of the node to which you attached the script.

To delete a node and free it from memory, you can call its queue_free() method. Doing so queues the node for deletion at the end of the current frame after it has finished processing. At that point, the engine removes the node from the scene and frees the object in memory.

Before calling sprite2d.queue_free(), the remote scene tree looks like this.

After the engine freed the node, the remote scene tree doesn't display the sprite anymore.

You can alternatively call free() to immediately destroy the node. You should do this with care as any reference to it will instantly become null. We recommend using queue_free() unless you know what you're doing.

When you free a node, it also frees all its children. Thanks to this, to delete an entire branch of the scene tree, you only have to free the topmost parent node.

Scenes are templates from which you can create as many reproductions as you'd like. This operation is called instancing, and doing it from code happens in two steps:

Loading the scene from the local drive.

Creating an instance of the loaded PackedScene resource.

Preloading the scene can improve the user's experience as the load operation happens when the compiler reads the script and not at runtime. This feature is only available with GDScript.

At that point, scene is a packed scene resource, not a node. To create the actual node, you need to call PackedScene.instantiate(). It returns a tree of nodes that you can use as a child of your current node.

The advantage of this two-step process is you can keep a packed scene loaded and create new instances on the fly. For example, to quickly instance several enemies or bullets.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var sprite2d
var camera2d

func _ready():
    sprite2d = get_node("Sprite2D")
    camera2d = get_node("Camera2D")
```

Example 2 (gdscript):
```gdscript
private Sprite2D _sprite2D;
private Camera2D _camera2D;

public override void _Ready()
{
    base._Ready();

    _sprite2D = GetNode<Sprite2D>("Sprite2D");
    _camera2D = GetNode<Camera2D>("Camera2D");
}
```

Example 3 (gdscript):
```gdscript
var animation_player

func _ready():
    animation_player = get_node("ShieldBar/AnimationPlayer")
```

Example 4 (gdscript):
```gdscript
private AnimationPlayer _animationPlayer;

public override void _Ready()
{
    base._Ready();

    _animationPlayer = GetNode<AnimationPlayer>("ShieldBar/AnimationPlayer");
}
```

---

## Node type customization using name suffixes

**URL:** https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/node_type_customization.html

**Contents:**
- Node type customization using name suffixes
- Opting out
- Remove nodes and animations (-noimp)
- Create collisions (-col, -convcol, -colonly, -convcolonly)
- Create Occluder (-occ, -occonly)
- Create navigation (-navmesh)
- Create a VehicleBody (-vehicle)
- Create a VehicleWheel (-wheel)
- Rigid Body (-rigid)
- Animation loop (-loop, -cycle)

Many times, when editing a scene, there are common tasks that need to be done after exporting:

Adding collision detection to objects.

Setting objects as navigation meshes.

Deleting nodes that are not used in the game engine (like specific lights used for modeling).

To simplify this workflow, Godot offers several suffixes that can be added to the names of the objects in your 3D modeling software. When imported, Godot will detect suffixes in object names and will perform actions automatically.

All the suffixes described below can be used with -, $, and _ and are case-insensitive.

If you do not want Godot to perform any of the actions described below, you can set the nodes/use_node_type_suffixes import option to false. This will disable all node type suffixes, which keeps nodes the same type as the original file indicated. However, the -noimp suffix will still be respected, as well as non-node suffixes like -vcol or -loop.

Alternatively, you can completely opt out of all name suffixes by setting the nodes/use_name_suffixes import option to false. This will completely stop the general scene import code from looking at name suffixes. However, the format-specific import code may still look at name suffixes, such as the glTF importer checking for the -loop suffix.

Disabling these options makes editor-imported files more similar to the original files, and more similar to importing files at runtime. For an import workflow that works at runtime, gives more predictable results, and only has explicitly defined behavior, consider setting these options to false and using GLTFDocumentExtension instead.

Nodes and animations that have the -noimp suffix will be removed at import time no matter what their type is. They will not appear in the imported scene.

This is equivalent to enabling Skip Import for a node in the Advanced Import Settings dialog.

The option -col will work only for Mesh objects. If it is detected, a child static collision node will be added, using the same geometry as the mesh. This will create a triangle mesh collision shape, which is a slow, but accurate option for collision detection. This option is usually what you want for level geometry (but see also -colonly below).

The option -convcol will create a ConvexPolygonShape3D instead of a ConcavePolygonShape3D. Unlike triangle meshes which can be concave, a convex shape can only accurately represent a shape that doesn't have any concave angles (a pyramid is convex, but a hollow box is concave). Due to this, convex collision shapes are generally not suited for level geometry. When representing simple enough meshes, convex collision shapes can result in better performance compared to a triangle collision shape. This option is ideal for simple or dynamic objects that require mostly-accurate collision detection.

However, in both cases, the visual geometry may be too complex or not smooth enough for collisions. This can create physics glitches and slow down the engine unnecessarily.

To solve this, the -colonly modifier exists. It will remove the mesh upon importing and will create a StaticBody3D collision instead. This helps the visual mesh and actual collision to be separated.

The option -convcolonly works in a similar way, but will create a ConvexPolygonShape3D instead using convex decomposition.

With Collada files, the option -colonly can also be used with Blender's empty objects. On import, it will create a StaticBody3D with a collision node as a child. The collision node will have one of a number of predefined shapes, depending on Blender's empty draw type:

Choosing a draw type for an Empty on creation in Blender

Single arrow will create a SeparationRayShape3D.

Cube will create a BoxShape3D.

Image will create a WorldBoundaryShape3D.

Sphere (and the others not listed) will create a SphereShape3D.

When possible, try to use a few primitive collision shapes instead of triangle mesh or convex shapes. Primitive shapes often have the best performance and reliability.

For better visibility on Blender's editor, you can set the "X-Ray" option on collision empties and set some distinct color for them by changing Edit > Preferences > Themes > 3D Viewport > Empty.

If using Blender 2.79 or older, follow these steps instead: User Preferences > Themes > 3D View > Empty.

See Collision shapes (3D) for a comprehensive overview of collision shapes.

If a mesh is imported with the -occ suffix an Occluder3D node will be created based on the geometry of the mesh, it does not replace the mesh. A mesh node with the -occonly suffix will be converted to an Occluder3D on import.

A mesh node with the -navmesh suffix will be converted to a navigation mesh. The original Mesh object will be removed at import-time.

A mesh node with the -vehicle suffix will be imported as a child to a VehicleBody3D node.

A mesh node with the -wheel suffix will be imported as a child to a VehicleWheel3D node.

A mesh node with the -rigid suffix will be imported as a RigidBody3D.

Animation clips in the source 3D file that start or end with the token loop or cycle will be imported as a Godot Animation with the loop flag set. Unlike the other suffixes described above, this does not require a hyphen.

In Blender, this requires using the NLA Editor and naming the Action with the loop or cycle prefix or suffix.

A material with the -alpha suffix will be imported with the TRANSPARENCY_ALPHA transparency mode.

A material with the -vcol suffix will be imported with the FLAG_ALBEDO_FROM_VERTEX_COLOR and FLAG_SRGB_VERTEX_COLOR flags set.

Please read the User-contributed notes policy before submitting a comment.

---

## Optimization using Servers

**URL:** https://docs.godotengine.org/en/stable/tutorials/performance/using_servers.html

**Contents:**
- Optimization using Servers
- Servers
- RIDs
- Creating a sprite
- Instantiating a Mesh into 3D space
- Creating a 2D RigidBody and moving a sprite with it
- Getting data from the servers
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

Engines like Godot provide increased ease of use thanks to their high-level constructs and features. Most of them are accessed and used via the Scene System. Using nodes and resources simplifies project organization and asset management in complex games.

There are, of course, always drawbacks:

There is an extra layer of complexity.

Performance is lower than when using simple APIs directly.

It is not possible to use multiple threads to control them.

More memory is needed.

In many cases, this is not really a problem (Godot is very optimized, and most operations are handled with signals, so no polling is required). Still, sometimes it can be. For example, dealing with tens of thousands of instances for something that needs to be processed every frame can be a bottleneck.

This type of situation makes programmers regret they are using a game engine and wish they could go back to a more handcrafted, low-level implementation of game code.

Still, Godot is designed to work around this problem.

You can see how using low-level servers works in action using the Bullet Shower demo project

One of the most interesting design decisions for Godot is the fact that the whole scene system is optional. While it is not currently possible to compile it out, it can be completely bypassed.

At the core, Godot uses the concept of Servers. They are very low-level APIs to control rendering, physics, sound, etc. The scene system is built on top of them and uses them directly. The most common servers are:

RenderingServer: handles everything related to graphics.

PhysicsServer3D: handles everything related to 3D physics.

PhysicsServer2D: handles everything related to 2D physics.

AudioServer: handles everything related to audio.

Explore their APIs and you will realize that all the functions provided are low-level implementations of everything Godot allows you to do.

The key to using servers is understanding Resource ID (RID) objects. These are opaque handles to the server implementation. They are allocated and freed manually. Almost every function in the servers requires RIDs to access the actual resource.

Most Godot nodes and resources contain these RIDs from the servers internally, and they can be obtained with different functions. In fact, anything that inherits Resource can be directly casted to an RID. Not all resources contain an RID, though: in such cases, the RID will be empty. The resource can then be passed to server APIs as an RID.

Resources are reference-counted (see RefCounted), and references to a resource's RID are not counted when determining whether the resource is still in use. Make sure to keep a reference to the resource outside the server, or else both it and its RID will be erased.

For nodes, there are many functions available:

For CanvasItem, the CanvasItem.get_canvas_item() method will return the canvas item RID in the server.

For CanvasLayer, the CanvasLayer.get_canvas() method will return the canvas RID in the server.

For Viewport, the Viewport.get_viewport_rid() method will return the viewport RID in the server.

For 3D, the World3D resource (obtainable in the Viewport and Node3D nodes) contains functions to get the RenderingServer Scenario, and the PhysicsServer Space. This allows creating 3D objects directly with the server API and using them.

For 2D, the World2D resource (obtainable in the Viewport and CanvasItem nodes) contains functions to get the RenderingServer Canvas, and the Physics2DServer Space. This allows creating 2D objects directly with the server API and using them.

The VisualInstance3D class, allows getting the scenario instance and instance base via the VisualInstance3D.get_instance() and VisualInstance3D.get_base() respectively.

Try exploring the nodes and resources you are familiar with and find the functions to obtain the server RIDs.

It is not advised to control RIDs from objects that already have a node associated. Instead, server functions should always be used for creating and controlling new ones and interacting with the existing ones.

This is an example of how to create a sprite from code and move it using the low-level CanvasItem API.

The Canvas Item API in the server allows you to add draw primitives to it. Once added, they can't be modified. The Item needs to be cleared and the primitives re-added (this is not the case for setting the transform, which can be done as many times as desired).

Primitives are cleared this way:

The 3D APIs are different from the 2D ones, so the instantiation API must be used.

This creates a RigidBody2D using the PhysicsServer2D API, and moves a CanvasItem when the body moves.

The 3D version should be very similar, as 2D and 3D physics servers are identical (using RigidBody3D and PhysicsServer3D respectively).

Try to never request any information from RenderingServer, PhysicsServer2D or PhysicsServer3D by calling functions unless you know what you are doing. These servers will often run asynchronously for performance and calling any function that returns a value will stall them and force them to process anything pending until the function is actually called. This will severely decrease performance if you call them every frame (and it won't be obvious why).

Because of this, most APIs in such servers are designed so it's not even possible to request information back, until it's actual data that can be saved.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Node2D


# RenderingServer expects references to be kept around.
var texture


func _ready():
    # Create a canvas item, child of this node.
    var ci_rid = RenderingServer.canvas_item_create()
    # Make this node the parent.
    RenderingServer.canvas_item_set_parent(ci_rid, get_canvas_item())
    # Draw a texture on it.
    # Remember, keep this reference.
    texture = load("res://my_texture.png")
    # Add it, centered.
    RenderingServer.canvas_item_add_texture_rect(ci_rid, Rect2(-texture.get_size() / 2, texture.get_size()), texture)
    # Add the item, rotated 45 degrees and translated.
    var xform = Transform2D().rotated(deg_to_rad(45)).translated(Vector2(20, 30))
    RenderingServer.canvas_item_set_transform(ci_rid, xform)
```

Example 2 (csharp):
```csharp
public partial class MyNode2D : Node2D
{
    // RenderingServer expects references to be kept around.
    private Texture2D _texture;

    public override void _Ready()
    {
        // Create a canvas item, child of this node.
        Rid ciRid = RenderingServer.CanvasItemCreate();
        // Make this node the parent.
        RenderingServer.CanvasItemSetParent(ciRid, GetCanvasItem());
        // Draw a texture on it.
        // Remember, keep this reference.
        _texture = ResourceLoader.Load<Texture2D>("res://MyTexture.png");
        // Add it, centered.
        RenderingServer.CanvasItemAddTextureRect(ciRid, new Rect2(-_texture.GetSize() / 2, _texture.GetSize()), _texture.GetRid());
        // Add the item, rotated 45 degrees and translated.
        Transform2D xform = Transform2D.Identity.Rotated(Mathf.DegToRad(45)).Translated(new Vector2(20, 30));
        RenderingServer.CanvasItemSetTransform(ciRid, xform);
    }
}
```

Example 3 (unknown):
```unknown
RenderingServer.canvas_item_clear(ci_rid)
```

Example 4 (unknown):
```unknown
RenderingServer.CanvasItemClear(ciRid);
```

---

## Overridable functions

**URL:** https://docs.godotengine.org/en/stable/tutorials/scripting/overridable_functions.html

**Contents:**
- Overridable functions
- User-contributed notes

Godot's Node class provides virtual functions you can override to update nodes every frame or on specific events, like when they enter the scene tree.

This document presents the ones you'll use most often.

Under the hood, these functions rely on Godot's low-level notifications system. To learn more about it, see Godot notifications.

Two functions allow you to initialize and get nodes besides the class's constructor: _enter_tree() and _ready().

When the node enters the Scene Tree, it becomes active and the engine calls its _enter_tree() method. That node's children may not be part of the active scene yet. As you can remove and re-add nodes to the scene tree, this function may be called multiple times throughout a node's lifetime.

Most of the time, you'll use _ready() instead. This function is called only once in a node's lifetime, after _enter_tree(). _ready() ensures that all children have entered the scene tree first, so you can safely call get_node() on them.

To learn more about getting node references, read Nodes and scene instances.

Another related callback is _exit_tree(), which the engine calls every time a node is about to exit the scene tree. This can be when you call Node.remove_child() or when you free a node.

The two virtual methods _process() and _physics_process() allow you to update the node, every frame and every physics frame respectively. For more information, read the dedicated documentation: Idle and Physics Processing.

Two more essential built-in node callback functions are Node._unhandled_input() and Node._input(), which you use to both receive and process individual input events. The _unhandled_input() method receives every key press, mouse click, etc. that have not been handled already in an _input() callback or in a user interface component. You want to use it for gameplay input in general. The _input() callback allows you to intercept and process input events before _unhandled_input() gets them.

To learn more about inputs in Godot, see the Input section.

There are some more overridable functions like Node._get_configuration_warnings(). Specialized node types provide more callbacks like CanvasItem._draw() to draw programmatically or Control._gui_input() to handle clicks and input on UI elements.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
# Called every time the node enters the scene tree.
func _enter_tree():
    pass

# Called when both the node and its children have entered the scene tree.
func _ready():
    pass

# Called when the node is about to leave the scene tree, after all its
# children received the _exit_tree() callback.
func _exit_tree():
    pass
```

Example 2 (gdscript):
```gdscript
// Called every time the node enters the scene tree.
public override void _EnterTree()
{
    base._EnterTree();
}

// Called when both the node and its children have entered the scene tree.
public override void _Ready()
{
    base._Ready();
}

// Called when the node is about to leave the scene tree, after all its
// children.
public override void _ExitTree()
{
    base._ExitTree();
}
```

Example 3 (gdscript):
```gdscript
# Called every frame.
func _process(delta):
    pass

# Called every physics frame.
func _physics_process(delta):
    pass
```

Example 4 (gdscript):
```gdscript
public override void _Process(double delta)
{
    // Called every frame.
    base._Process(delta);
}

public override void _PhysicsProcess(double delta)
{
    // Called every physics frame.
    base._PhysicsProcess(delta);
}
```

---

## ResourceImporterOBJ

**URL:** https://docs.godotengine.org/en/stable/classes/class_resourceimporterobj.html

**Contents:**
- ResourceImporterOBJ
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: ResourceImporter < RefCounted < Object

Imports an OBJ 3D model as an independent Mesh or scene.

Unlike ResourceImporterScene, ResourceImporterOBJ will import a single Mesh resource by default instead of importing a PackedScene. This makes it easier to use the Mesh resource in nodes that expect direct Mesh resources, such as GridMap, GPUParticles3D or CPUParticles3D. Note that it is still possible to save mesh resources from 3D scenes using the Advanced Import Settings dialog, regardless of the source format.

See also ResourceImporterScene, which is used for more advanced 3D formats such as glTF.

force_disable_mesh_compression

generate_lightmap_uv2

generate_lightmap_uv2_texel_size

bool force_disable_mesh_compression = false 🔗

If true, mesh compression will not be used. Consider enabling if you notice blocky artifacts in your mesh normals or UVs, or if you have meshes that are larger than a few thousand meters in each direction.

bool generate_lightmap_uv2 = false 🔗

If true, generates UV2 on import for LightmapGI baking.

float generate_lightmap_uv2_texel_size = 0.2 🔗

Controls the size of each texel on the baked lightmap. A smaller value results in more precise lightmaps, at the cost of larger lightmap sizes and longer bake times.

Note: Only effective if generate_lightmap_uv2 is true.

bool generate_lods = true 🔗

If true, generates lower detail variants of the mesh which will be displayed in the distance to improve rendering performance. Not all meshes benefit from LOD, especially if they are never rendered from far away. Disabling this can reduce output file size and speed up importing. See Mesh level of detail (LOD) for more information.

bool generate_shadow_mesh = true 🔗

If true, enables the generation of shadow meshes on import. This optimizes shadow rendering without reducing quality by welding vertices together when possible. This in turn reduces the memory bandwidth required to render shadows. Shadow mesh generation currently doesn't support using a lower detail level than the source mesh (but shadow rendering will make use of LODs when relevant).

bool generate_tangents = true 🔗

If true, generate vertex tangents using Mikktspace if the source mesh doesn't have tangent data. When possible, it's recommended to let the 3D modeling software generate tangents on export instead on relying on this option. Tangents are required for correct display of normal and height maps, along with any material/shader features that require tangents.

If you don't need material features that require tangents, disabling this can reduce output file size and speed up importing if the source 3D file doesn't contain tangents.

Vector3 offset_mesh = Vector3(0, 0, 0) 🔗

Offsets the mesh's data by the specified value. This can be used to work around misaligned meshes without having to modify the source file.

Vector3 scale_mesh = Vector3(1, 1, 1) 🔗

Scales the mesh's data by the specified value. This can be used to work around misscaled meshes without having to modify the source file.

Please read the User-contributed notes policy before submitting a comment.

---

## ResourceSaver

**URL:** https://docs.godotengine.org/en/stable/classes/class_resourcesaver.html

**Contents:**
- ResourceSaver
- Description
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

A singleton for saving Resources to the filesystem.

A singleton for saving resource types to the filesystem.

It uses the many ResourceFormatSaver classes registered in the engine (either built-in or from a plugin) to save resource data to text-based (e.g. .tres or .tscn) or binary files (e.g. .res or .scn).

add_resource_format_saver(format_saver: ResourceFormatSaver, at_front: bool = false)

get_recognized_extensions(type: Resource)

get_resource_id_for_path(path: String, generate: bool = false)

remove_resource_format_saver(format_saver: ResourceFormatSaver)

save(resource: Resource, path: String = "", flags: BitField[SaverFlags] = 0)

set_uid(resource: String, uid: int)

SaverFlags FLAG_NONE = 0

No resource saving option.

SaverFlags FLAG_RELATIVE_PATHS = 1

Save the resource with a path relative to the scene which uses it.

SaverFlags FLAG_BUNDLE_RESOURCES = 2

Bundles external resources.

SaverFlags FLAG_CHANGE_PATH = 4

Changes the Resource.resource_path of the saved resource to match its new location.

SaverFlags FLAG_OMIT_EDITOR_PROPERTIES = 8

Do not save editor-specific metadata (identified by their __editor prefix).

SaverFlags FLAG_SAVE_BIG_ENDIAN = 16

Save as big endian (see FileAccess.big_endian).

SaverFlags FLAG_COMPRESS = 32

Compress the resource on save using FileAccess.COMPRESSION_ZSTD. Only available for binary resource types.

SaverFlags FLAG_REPLACE_SUBRESOURCE_PATHS = 64

Take over the paths of the saved subresources (see Resource.take_over_path()).

void add_resource_format_saver(format_saver: ResourceFormatSaver, at_front: bool = false) 🔗

Registers a new ResourceFormatSaver. The ResourceSaver will use the ResourceFormatSaver as described in save().

This method is performed implicitly for ResourceFormatSavers written in GDScript (see ResourceFormatSaver for more information).

PackedStringArray get_recognized_extensions(type: Resource) 🔗

Returns the list of extensions available for saving a resource of a given type.

int get_resource_id_for_path(path: String, generate: bool = false) 🔗

Returns the resource ID for the given path. If generate is true, a new resource ID will be generated if one for the path is not found. If generate is false and the path is not found, ResourceUID.INVALID_ID is returned.

void remove_resource_format_saver(format_saver: ResourceFormatSaver) 🔗

Unregisters the given ResourceFormatSaver.

Error save(resource: Resource, path: String = "", flags: BitField[SaverFlags] = 0) 🔗

Saves a resource to disk to the given path, using a ResourceFormatSaver that recognizes the resource object. If path is empty, ResourceSaver will try to use Resource.resource_path.

The flags bitmask can be specified to customize the save behavior.

Returns @GlobalScope.OK on success.

Note: When the project is running, any generated UID associated with the resource will not be saved as the required code is only executed in editor mode.

Error set_uid(resource: String, uid: int) 🔗

Sets the UID of the given resource path to uid. You can generate a new UID using ResourceUID.create_id().

Since resources will normally get a UID automatically, this method is only useful in very specific cases.

Please read the User-contributed notes policy before submitting a comment.

---

## Resources

**URL:** https://docs.godotengine.org/en/stable/tutorials/scripting/resources.html

**Contents:**
- Resources
- Nodes and resources
- External vs built-in
- Loading resources from code
- Loading scenes
- Freeing resources
- Creating your own resources
- User-contributed notes

Up to this tutorial, we focused on the Node class in Godot as that's the one you use to code behavior and most of the engine's features rely on it. There is another datatype that is just as important: Resource.

Nodes give you functionality: they draw sprites, 3D models, simulate physics, arrange user interfaces, etc. Resources are data containers. They don't do anything on their own: instead, nodes use the data contained in resources.

Anything Godot saves or loads from disk is a resource. Be it a scene (a .tscn or a .scn file), an image, a script... Here are some Resource examples:

When the engine loads a resource from disk, it only loads it once. If a copy of that resource is already in memory, trying to load the resource again will return the same copy every time. As resources only contain data, there is no need to duplicate them.

Every object, be it a Node or a Resource, can export properties. There are many types of Properties, like String, integer, Vector2, etc., and any of these types can become a resource. This means that both nodes and resources can contain resources as properties:

There are two ways to save resources. They can be:

External to a scene, saved on the disk as individual files.

Built-in, saved inside the .tscn or the .scn file they're attached to.

To be more specific, here's a Texture2D in a Sprite2D node:

Clicking the resource preview allows us to view the resource's properties.

The path property tells us where the resource comes from. In this case, it comes from a PNG image called robi.png. When the resource comes from a file like this, it is an external resource. If you erase the path or this path is empty, it becomes a built-in resource.

The switch between built-in and external resources happens when you save the scene. In the example above, if you erase the path "res://robi.png" and save, Godot will save the image inside the .tscn scene file.

Even if you save a built-in resource, when you instance a scene multiple times, the engine will only load one copy of it.

There are two ways to load resources from code. First, you can use the load() function anytime:

You can also preload resources. Unlike load, this function will read the file from disk and load it at compile-time. As a result, you cannot call preload with a variable path: you need to use a constant string.

Scenes are also resources, but there is a catch. Scenes saved to disk are resources of type PackedScene. The scene is packed inside a Resource.

To get an instance of the scene, you have to use the PackedScene.instantiate() method.

This method creates the nodes in the scene's hierarchy, configures them, and returns the root node of the scene. You can then add it as a child of any other node.

The approach has several advantages. As the PackedScene.instantiate() function is fast, you can create new enemies, bullets, effects, etc. without having to load them again from disk each time. Remember that, as always, images, meshes, etc. are all shared between the scene instances.

When a Resource is no longer in use, it will automatically free itself. Since, in most cases, Resources are contained in Nodes, when you free a node, the engine frees all the resources it owns as well if no other node uses them.

Like any Object in Godot, users can also script Resources. Resource scripts inherit the ability to freely translate between object properties and serialized text or binary data (*.tres, *.res). They also inherit the reference-counting memory management from the RefCounted type.

This comes with many distinct advantages over alternative data structures, such as JSON, CSV, or custom TXT files. Users can only import these assets as a Dictionary (JSON) or as a FileAccess to parse. What sets Resources apart is their inheritance of Object, RefCounted, and Resource features:

They can define constants, so constants from other data fields or objects are not needed.

They can define methods, including setter/getter methods for properties. This allows for abstraction and encapsulation of the underlying data. If the Resource script's structure needs to change, the game using the Resource need not also change.

They can define signals, so Resources can trigger responses to changes in the data they manage.

They have defined properties, so users know 100% that their data will exist.

Resource auto-serialization and deserialization is a built-in Godot Engine feature. Users do not need to implement custom logic to import/export a resource file's data.

Resources can even serialize sub-Resources recursively, meaning users can design even more sophisticated data structures.

Users can save Resources as version-control-friendly text files (*.tres). Upon exporting a game, Godot serializes resource files as binary files (*.res) for increased speed and compression.

Godot Engine's Inspector renders and edits Resource files out-of-the-box. As such, users often do not need to implement custom logic to visualize or edit their data. To do so, double-click the resource file in the FileSystem dock or click the folder icon in the Inspector and open the file in the dialog.

They can extend other resource types besides just the base Resource.

Godot makes it easy to create custom Resources in the Inspector.

Create a new Resource object in the Inspector. This can even be a type that derives Resource, so long as your script is extending that type.

Set the script property in the Inspector to be your script.

The Inspector will now display your Resource script's custom properties. If one edits those values and saves the resource, the Inspector serializes the custom properties too! To save a resource from the Inspector, click the save icon at the top of the Inspector, and select "Save" or "Save As...".

If the script's language supports script classes, then it streamlines the process. Defining a name for your script alone will add it to the Inspector's creation dialog. This will auto-add your script to the Resource object you create.

Let's see some examples. Create a Resource and name it bot_stats. It should appear in your file tab with the full name bot_stats.tres. Without a script, it's useless, so let's add some data and logic! Attach a script to it named bot_stats.gd (or just create a new script, and then drag it to it).

To make the new resource class appear in the Create Resource GUI you need to provide a class name for GDScript, or use the [GlobalClass] attribute in C#.

Now, create a CharacterBody3D, name it Bot, and add the following script to it:

Now, select the CharacterBody3D node which we named bot, and drag&drop the bot_stats.tres resource onto the Inspector. It should print 10! Obviously, this setup can be used for more advanced features than this, but as long you really understand how it all worked, you should figure out everything else related to Resources.

Resource scripts are similar to Unity's ScriptableObjects. The Inspector provides built-in support for custom resources. If desired though, users can even design their own Control-based tool scripts and combine them with an EditorPlugin to create custom visualizations and editors for their data.

Unreal Engine's DataTables and CurveTables are also easy to recreate with Resource scripts. DataTables are a String mapped to a custom struct, similar to a Dictionary mapping a String to a secondary custom Resource script.

Instead of inlining the Dictionary values, one could also, alternatively:

Import a table of values from a spreadsheet and generate these key-value pairs.

Design a visualization within the editor and create a plugin that adds it to the Inspector when you open these types of Resources.

CurveTables are the same thing, except mapped to an Array of float values or a Curve/Curve2D resource object.

Beware that resource files (*.tres/*.res) will store the path of the script they use in the file. When loaded, they will fetch and load this script as an extension of their type. This means that trying to assign an inner class of a script (i.e. using the class keyword in GDScript) won't work. Godot will not serialize the custom properties on the script inner class properly.

In the example below, Godot would load the Node script, see that it doesn't extend Resource, and then determine that the script failed to load for the Resource object since the types are incompatible.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    # Godot loads the Resource when it reads this very line.
    var imported_resource = load("res://robi.png")
    $sprite.texture = imported_resource
```

Example 2 (gdscript):
```gdscript
public override void _Ready()
{
    // Godot loads the Resource when it executes this line.
    var texture = GD.Load<Texture>("res://Robi.png");
    var sprite = GetNode<Sprite2D>("sprite");
    sprite.Texture = texture;
}
```

Example 3 (gdscript):
```gdscript
func _ready():
    # Godot loads the resource at compile-time
    var imported_resource = preload("res://robi.png")
    get_node("sprite").texture = imported_resource
```

Example 4 (unknown):
```unknown
// 'preload()' is unavailable in C Sharp.
```

---

## SceneState

**URL:** https://docs.godotengine.org/en/stable/classes/class_scenestate.html

**Contents:**
- SceneState
- Description
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Provides access to a scene file's information.

Maintains a list of resources, nodes, exported and overridden properties, and built-in scripts associated with a scene. They cannot be modified from a SceneState, only accessed. Useful for peeking into what a PackedScene contains without instantiating it.

This class cannot be instantiated directly, it is retrieved for a given scene as the result of PackedScene.get_state().

get_base_scene_state() const

get_connection_binds(idx: int) const

get_connection_count() const

get_connection_flags(idx: int) const

get_connection_method(idx: int) const

get_connection_signal(idx: int) const

get_connection_source(idx: int) const

get_connection_target(idx: int) const

get_connection_unbinds(idx: int) const

get_node_count() const

get_node_groups(idx: int) const

get_node_index(idx: int) const

get_node_instance(idx: int) const

get_node_instance_placeholder(idx: int) const

get_node_name(idx: int) const

get_node_owner_path(idx: int) const

get_node_path(idx: int, for_parent: bool = false) const

get_node_property_count(idx: int) const

get_node_property_name(idx: int, prop_idx: int) const

get_node_property_value(idx: int, prop_idx: int) const

get_node_type(idx: int) const

is_node_instance_placeholder(idx: int) const

GenEditState GEN_EDIT_STATE_DISABLED = 0

If passed to PackedScene.instantiate(), blocks edits to the scene state.

GenEditState GEN_EDIT_STATE_INSTANCE = 1

If passed to PackedScene.instantiate(), provides inherited scene resources to the local scene.

Note: Only available in editor builds.

GenEditState GEN_EDIT_STATE_MAIN = 2

If passed to PackedScene.instantiate(), provides local scene resources to the local scene. Only the main scene should receive the main edit state.

Note: Only available in editor builds.

GenEditState GEN_EDIT_STATE_MAIN_INHERITED = 3

If passed to PackedScene.instantiate(), it's similar to GEN_EDIT_STATE_MAIN, but for the case where the scene is being instantiated to be the base of another one.

Note: Only available in editor builds.

SceneState get_base_scene_state() const 🔗

Returns the SceneState of the scene that this scene inherits from, or null if it doesn't inherit from any scene.

Array get_connection_binds(idx: int) const 🔗

Returns the list of bound parameters for the signal at idx.

int get_connection_count() const 🔗

Returns the number of signal connections in the scene.

The idx argument used to query connection metadata in other get_connection_* methods in the interval [0, get_connection_count() - 1].

int get_connection_flags(idx: int) const 🔗

Returns the connection flags for the signal at idx. See ConnectFlags constants.

StringName get_connection_method(idx: int) const 🔗

Returns the method connected to the signal at idx.

StringName get_connection_signal(idx: int) const 🔗

Returns the name of the signal at idx.

NodePath get_connection_source(idx: int) const 🔗

Returns the path to the node that owns the signal at idx, relative to the root node.

NodePath get_connection_target(idx: int) const 🔗

Returns the path to the node that owns the method connected to the signal at idx, relative to the root node.

int get_connection_unbinds(idx: int) const 🔗

Returns the number of unbound parameters for the signal at idx.

int get_node_count() const 🔗

Returns the number of nodes in the scene.

The idx argument used to query node data in other get_node_* methods in the interval [0, get_node_count() - 1].

PackedStringArray get_node_groups(idx: int) const 🔗

Returns the list of group names associated with the node at idx.

int get_node_index(idx: int) const 🔗

Returns the node's index, which is its position relative to its siblings. This is only relevant and saved in scenes for cases where new nodes are added to an instantiated or inherited scene among siblings from the base scene. Despite the name, this index is not related to the idx argument used here and in other methods.

PackedScene get_node_instance(idx: int) const 🔗

Returns a PackedScene for the node at idx (i.e. the whole branch starting at this node, with its child nodes and resources), or null if the node is not an instance.

String get_node_instance_placeholder(idx: int) const 🔗

Returns the path to the represented scene file if the node at idx is an InstancePlaceholder.

StringName get_node_name(idx: int) const 🔗

Returns the name of the node at idx.

NodePath get_node_owner_path(idx: int) const 🔗

Returns the path to the owner of the node at idx, relative to the root node.

NodePath get_node_path(idx: int, for_parent: bool = false) const 🔗

Returns the path to the node at idx.

If for_parent is true, returns the path of the idx node's parent instead.

int get_node_property_count(idx: int) const 🔗

Returns the number of exported or overridden properties for the node at idx.

The prop_idx argument used to query node property data in other get_node_property_* methods in the interval [0, get_node_property_count() - 1].

StringName get_node_property_name(idx: int, prop_idx: int) const 🔗

Returns the name of the property at prop_idx for the node at idx.

Variant get_node_property_value(idx: int, prop_idx: int) const 🔗

Returns the value of the property at prop_idx for the node at idx.

StringName get_node_type(idx: int) const 🔗

Returns the type of the node at idx.

String get_path() const 🔗

Returns the resource path to the represented PackedScene.

bool is_node_instance_placeholder(idx: int) const 🔗

Returns true if the node at idx is an InstancePlaceholder.

Please read the User-contributed notes policy before submitting a comment.

---

## SceneTree

**URL:** https://docs.godotengine.org/en/stable/classes/class_scenetree.html

**Contents:**
- SceneTree
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: MainLoop < Object

Manages the game loop via a hierarchy of nodes.

As one of the most important classes, the SceneTree manages the hierarchy of nodes in a scene, as well as scenes themselves. Nodes can be added, fetched and removed. The whole scene tree (and thus the current scene) can be paused. Scenes can be loaded, switched and reloaded.

You can also use the SceneTree to organize your nodes into groups: every node can be added to as many groups as you want to create, e.g. an "enemy" group. You can then iterate these groups or even call methods and set properties on all the nodes belonging to any given group.

SceneTree is the default MainLoop implementation used by the engine, and is thus in charge of the game loop.

debug_collisions_hint

debug_navigation_hint

physics_interpolation

call_group(group: StringName, method: StringName, ...) vararg

call_group_flags(flags: int, group: StringName, method: StringName, ...) vararg

change_scene_to_file(path: String)

change_scene_to_packed(packed_scene: PackedScene)

create_timer(time_sec: float, process_always: bool = true, process_in_physics: bool = false, ignore_time_scale: bool = false)

get_first_node_in_group(group: StringName)

get_multiplayer(for_path: NodePath = NodePath("")) const

get_node_count() const

get_node_count_in_group(group: StringName) const

get_nodes_in_group(group: StringName)

get_processed_tweens()

has_group(name: StringName) const

is_accessibility_enabled() const

is_accessibility_supported() const

notify_group(group: StringName, notification: int)

notify_group_flags(call_flags: int, group: StringName, notification: int)

queue_delete(obj: Object)

quit(exit_code: int = 0)

reload_current_scene()

set_group(group: StringName, property: String, value: Variant)

set_group_flags(call_flags: int, group: StringName, property: String, value: Variant)

set_multiplayer(multiplayer: MultiplayerAPI, root_path: NodePath = NodePath(""))

unload_current_scene()

node_added(node: Node) 🔗

Emitted when the node enters this tree.

node_configuration_warning_changed(node: Node) 🔗

Emitted when the node's Node.update_configuration_warnings() is called. Only emitted in the editor.

node_removed(node: Node) 🔗

Emitted when the node exits this tree.

node_renamed(node: Node) 🔗

Emitted when the node's Node.name is changed.

Emitted immediately before Node._physics_process() is called on every node in this tree.

Emitted immediately before Node._process() is called on every node in this tree.

Emitted after the new scene is added to scene tree and initialized. Can be used to reliably access current_scene when changing scenes.

Emitted any time the tree's hierarchy changes (nodes being moved, renamed, etc.).

tree_process_mode_changed() 🔗

Emitted when the Node.process_mode of any node inside the tree is changed. Only emitted in the editor, to update the visibility of disabled nodes.

enum GroupCallFlags: 🔗

GroupCallFlags GROUP_CALL_DEFAULT = 0

Call nodes within a group with no special behavior (default).

GroupCallFlags GROUP_CALL_REVERSE = 1

Call nodes within a group in reverse tree hierarchy order (all nested children are called before their respective parent nodes).

GroupCallFlags GROUP_CALL_DEFERRED = 2

Call nodes within a group at the end of the current frame (can be either process or physics frame), similar to Object.call_deferred().

GroupCallFlags GROUP_CALL_UNIQUE = 4

Call nodes within a group only once, even if the call is executed many times in the same frame. Must be combined with GROUP_CALL_DEFERRED to work.

Note: Different arguments are not taken into account. Therefore, when the same call is executed with different arguments, only the first call will be performed.

bool auto_accept_quit = true 🔗

void set_auto_accept_quit(value: bool)

bool is_auto_accept_quit()

If true, the application automatically accepts quitting requests.

For mobile platforms, see quit_on_go_back.

void set_current_scene(value: Node)

Node get_current_scene()

The root node of the currently loaded main scene, usually as a direct child of root. See also change_scene_to_file(), change_scene_to_packed(), and reload_current_scene().

Warning: Setting this property directly may not work as expected, as it does not add or remove any nodes from this tree.

bool debug_collisions_hint = false 🔗

void set_debug_collisions_hint(value: bool)

bool is_debugging_collisions_hint()

If true, collision shapes will be visible when running the game from the editor for debugging purposes.

Note: This property is not designed to be changed at run-time. Changing the value of debug_collisions_hint while the project is running will not have the desired effect.

bool debug_navigation_hint = false 🔗

void set_debug_navigation_hint(value: bool)

bool is_debugging_navigation_hint()

If true, navigation polygons will be visible when running the game from the editor for debugging purposes.

Note: This property is not designed to be changed at run-time. Changing the value of debug_navigation_hint while the project is running will not have the desired effect.

bool debug_paths_hint = false 🔗

void set_debug_paths_hint(value: bool)

bool is_debugging_paths_hint()

If true, curves from Path2D and Path3D nodes will be visible when running the game from the editor for debugging purposes.

Note: This property is not designed to be changed at run-time. Changing the value of debug_paths_hint while the project is running will not have the desired effect.

Node edited_scene_root 🔗

void set_edited_scene_root(value: Node)

Node get_edited_scene_root()

The root of the scene currently being edited in the editor. This is usually a direct child of root.

Note: This property does nothing in release builds.

bool multiplayer_poll = true 🔗

void set_multiplayer_poll_enabled(value: bool)

bool is_multiplayer_poll_enabled()

If true (default value), enables automatic polling of the MultiplayerAPI for this SceneTree during process_frame.

If false, you need to manually call MultiplayerAPI.poll() to process network packets and deliver RPCs. This allows running RPCs in a different loop (e.g. physics, thread, specific time step) and for manual Mutex protection when accessing the MultiplayerAPI from threads.

bool paused = false 🔗

void set_pause(value: bool)

If true, the scene tree is considered paused. This causes the following behavior:

2D and 3D physics will be stopped, as well as collision detection and related signals.

Depending on each node's Node.process_mode, their Node._process(), Node._physics_process() and Node._input() callback methods may not called anymore.

bool physics_interpolation = false 🔗

void set_physics_interpolation_enabled(value: bool)

bool is_physics_interpolation_enabled()

If true, the renderer will interpolate the transforms of objects (both physics and non-physics) between the last two transforms, so that smooth motion is seen even when physics ticks do not coincide with rendered frames.

The default value of this property is controlled by ProjectSettings.physics/common/physics_interpolation.

Note: Although this is a global setting, finer control of individual branches of the SceneTree is possible using Node.physics_interpolation_mode.

bool quit_on_go_back = true 🔗

void set_quit_on_go_back(value: bool)

bool is_quit_on_go_back()

If true, the application quits automatically when navigating back (e.g. using the system "Back" button on Android).

To handle 'Go Back' button when this option is disabled, use DisplayServer.WINDOW_EVENT_GO_BACK_REQUEST.

The tree's root Window. This is top-most Node of the scene tree, and is always present. An absolute NodePath always starts from this node. Children of the root node may include the loaded current_scene, as well as any AutoLoad configured in the Project Settings.

Warning: Do not delete this node. This will result in unstable behavior, followed by a crash.

void call_group(group: StringName, method: StringName, ...) vararg 🔗

Calls method on each node inside this tree added to the given group. You can pass arguments to method by specifying them at the end of this method call. Nodes that cannot call method (either because the method doesn't exist or the arguments do not match) are ignored. See also set_group() and notify_group().

Note: This method acts immediately on all selected nodes at once, which may cause stuttering in some performance-intensive situations.

Note: In C#, method must be in snake_case when referring to built-in Godot methods. Prefer using the names exposed in the MethodName class to avoid allocating a new StringName on each call.

void call_group_flags(flags: int, group: StringName, method: StringName, ...) vararg 🔗

Calls the given method on each node inside this tree added to the given group. Use flags to customize this method's behavior (see GroupCallFlags). Additional arguments for method can be passed at the end of this method. Nodes that cannot call method (either because the method doesn't exist or the arguments do not match) are ignored.

Note: In C#, method must be in snake_case when referring to built-in Godot methods. Prefer using the names exposed in the MethodName class to avoid allocating a new StringName on each call.

Error change_scene_to_file(path: String) 🔗

Changes the running scene to the one at the given path, after loading it into a PackedScene and creating a new instance.

Returns @GlobalScope.OK on success, @GlobalScope.ERR_CANT_OPEN if the path cannot be loaded into a PackedScene, or @GlobalScope.ERR_CANT_CREATE if that scene cannot be instantiated.

Note: See change_scene_to_packed() for details on the order of operations.

Error change_scene_to_packed(packed_scene: PackedScene) 🔗

Changes the running scene to a new instance of the given PackedScene (which must be valid).

Returns @GlobalScope.OK on success, @GlobalScope.ERR_CANT_CREATE if the scene cannot be instantiated, or @GlobalScope.ERR_INVALID_PARAMETER if the scene is invalid.

Note: Operations happen in the following order when change_scene_to_packed() is called:

The current scene node is immediately removed from the tree. From that point, Node.get_tree() called on the current (outgoing) scene will return null. current_scene will be null, too, because the new scene is not available yet.

At the end of the frame, the formerly current scene, already removed from the tree, will be deleted (freed from memory) and then the new scene will be instantiated and added to the tree. Node.get_tree() and current_scene will be back to working as usual.

This ensures that both scenes aren't running at the same time, while still freeing the previous scene in a safe way similar to Node.queue_free().

If you want to reliably access the new scene, await the scene_changed signal.

SceneTreeTimer create_timer(time_sec: float, process_always: bool = true, process_in_physics: bool = false, ignore_time_scale: bool = false) 🔗

Returns a new SceneTreeTimer. After time_sec in seconds have passed, the timer will emit SceneTreeTimer.timeout and will be automatically freed.

If process_always is false, the timer will be paused when setting paused to true.

If process_in_physics is true, the timer will update at the end of the physics frame, instead of the process frame.

If ignore_time_scale is true, the timer will ignore Engine.time_scale and update with the real, elapsed time.

This method is commonly used to create a one-shot delay timer, as in the following example:

Note: The timer is always updated after all of the nodes in the tree. A node's Node._process() method would be called before the timer updates (or Node._physics_process() if process_in_physics is set to true).

Tween create_tween() 🔗

Creates and returns a new Tween processed in this tree. The Tween will start automatically on the next process frame or physics frame (depending on its TweenProcessMode).

Note: A Tween created using this method is not bound to any Node. It may keep working until there is nothing left to animate. If you want the Tween to be automatically killed when the Node is freed, use Node.create_tween() or Tween.bind_node().

Node get_first_node_in_group(group: StringName) 🔗

Returns the first Node found inside the tree, that has been added to the given group, in scene hierarchy order. Returns null if no match is found. See also get_nodes_in_group().

int get_frame() const 🔗

Returns how many physics process steps have been processed, since the application started. This is not a measurement of elapsed time. See also physics_frame. For the number of frames rendered, see Engine.get_process_frames().

MultiplayerAPI get_multiplayer(for_path: NodePath = NodePath("")) const 🔗

Searches for the MultiplayerAPI configured for the given path, if one does not exist it searches the parent paths until one is found. If the path is empty, or none is found, the default one is returned. See set_multiplayer().

int get_node_count() const 🔗

Returns the number of nodes inside this tree.

int get_node_count_in_group(group: StringName) const 🔗

Returns the number of nodes assigned to the given group.

Array[Node] get_nodes_in_group(group: StringName) 🔗

Returns an Array containing all nodes inside this tree, that have been added to the given group, in scene hierarchy order.

Array[Tween] get_processed_tweens() 🔗

Returns an Array of currently existing Tweens in the tree, including paused tweens.

bool has_group(name: StringName) const 🔗

Returns true if a node added to the given group name exists in the tree.

bool is_accessibility_enabled() const 🔗

Returns true if accessibility features are enabled, and accessibility information updates are actively processed.

bool is_accessibility_supported() const 🔗

Returns true if accessibility features are supported by the OS and enabled in project settings.

void notify_group(group: StringName, notification: int) 🔗

Calls Object.notification() with the given notification to all nodes inside this tree added to the group. See also Godot notifications and call_group() and set_group().

Note: This method acts immediately on all selected nodes at once, which may cause stuttering in some performance-intensive situations.

void notify_group_flags(call_flags: int, group: StringName, notification: int) 🔗

Calls Object.notification() with the given notification to all nodes inside this tree added to the group. Use call_flags to customize this method's behavior (see GroupCallFlags).

void queue_delete(obj: Object) 🔗

Queues the given obj to be deleted, calling its Object.free() at the end of the current frame. This method is similar to Node.queue_free().

void quit(exit_code: int = 0) 🔗

Quits the application at the end of the current iteration, with the given exit_code.

By convention, an exit code of 0 indicates success, whereas any other exit code indicates an error. For portability reasons, it should be between 0 and 125 (inclusive).

Note: On iOS this method doesn't work. Instead, as recommended by the iOS Human Interface Guidelines, the user is expected to close apps via the Home button.

Error reload_current_scene() 🔗

Reloads the currently active scene, replacing current_scene with a new instance of its original PackedScene.

Returns @GlobalScope.OK on success, @GlobalScope.ERR_UNCONFIGURED if no current_scene is defined, @GlobalScope.ERR_CANT_OPEN if current_scene cannot be loaded into a PackedScene, or @GlobalScope.ERR_CANT_CREATE if the scene cannot be instantiated.

void set_group(group: StringName, property: String, value: Variant) 🔗

Sets the given property to value on all nodes inside this tree added to the given group. Nodes that do not have the property are ignored. See also call_group() and notify_group().

Note: This method acts immediately on all selected nodes at once, which may cause stuttering in some performance-intensive situations.

Note: In C#, property must be in snake_case when referring to built-in Godot properties. Prefer using the names exposed in the PropertyName class to avoid allocating a new StringName on each call.

void set_group_flags(call_flags: int, group: StringName, property: String, value: Variant) 🔗

Sets the given property to value on all nodes inside this tree added to the given group. Nodes that do not have the property are ignored. Use call_flags to customize this method's behavior (see GroupCallFlags).

Note: In C#, property must be in snake_case when referring to built-in Godot properties. Prefer using the names exposed in the PropertyName class to avoid allocating a new StringName on each call.

void set_multiplayer(multiplayer: MultiplayerAPI, root_path: NodePath = NodePath("")) 🔗

Sets a custom MultiplayerAPI with the given root_path (controlling also the relative subpaths), or override the default one if root_path is empty.

Note: No MultiplayerAPI must be configured for the subpath containing root_path, nested custom multiplayers are not allowed. I.e. if one is configured for "/root/Foo" setting one for "/root/Foo/Bar" will cause an error.

Note: set_multiplayer() should be called before the child nodes are ready at the given root_path. If multiplayer nodes like MultiplayerSpawner or MultiplayerSynchronizer are added to the tree before the custom multiplayer API is set, they will not work.

void unload_current_scene() 🔗

If a current scene is loaded, calling this method will unload it.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
# This code should be inside an autoload.
get_tree().change_scene_to_file(other_scene_path)
await get_tree().scene_changed
print(get_tree().current_scene) # Prints the new scene.
```

Example 2 (markdown):
```markdown
# Calls "hide" to all nodes of the "enemies" group, at the end of the frame and in reverse tree order.
get_tree().call_group_flags(
        SceneTree.GROUP_CALL_DEFERRED | SceneTree.GROUP_CALL_REVERSE,
        "enemies", "hide")
```

Example 3 (swift):
```swift
func some_function():
    print("start")
    await get_tree().create_timer(1.0).timeout
    print("end")
```

Example 4 (swift):
```swift
public async Task SomeFunction()
{
    GD.Print("start");
    await ToSignal(GetTree().CreateTimer(1.0f), SceneTreeTimer.SignalName.Timeout);
    GD.Print("end");
}
```

---

## Scene organization

**URL:** https://docs.godotengine.org/en/stable/tutorials/best_practices/scene_organization.html

**Contents:**
- Scene organization
- How to build relationships effectively
- Choosing a node tree structure
- User-contributed notes

This article covers topics related to the effective organization of scene content. Which nodes should you use? Where should you place them? How should they interact?

When Godot users begin crafting their own scenes, they often run into the following problem:

They create their first scene and fill it with content only to eventually end up saving branches of their scene into separate scenes as the nagging feeling that they should split things up starts to accumulate. However, they then notice that the hard references they were able to rely on before are no longer possible. Re-using the scene in multiple places creates issues because the node paths do not find their targets and signal connections established in the editor break.

To fix these problems, you must instantiate the sub-scenes without them requiring details about their environment. You need to be able to trust that the sub-scene will create itself without being picky about how it's used.

One of the biggest things to consider in OOP is maintaining focused, singular-purpose classes with loose coupling to other parts of the codebase. This keeps the size of objects small (for maintainability) and improves their reusability.

These OOP best practices have several implications for best practices in scene structure and script usage.

If at all possible, you should design scenes to have no dependencies. That is, you should create scenes that keep everything they need within themselves.

If a scene must interact with an external context, experienced developers recommend the use of Dependency Injection. This technique involves having a high-level API provide the dependencies of the low-level API. Why do this? Because classes which rely on their external environment can inadvertently trigger bugs and unexpected behavior.

To do this, you must expose data and then rely on a parent context to initialize it:

Connect to a signal. Extremely safe, but should be used only to "respond" to behavior, not start it. By convention, signal names are usually past-tense verbs like "entered", "skill_activated", or "item_collected".

Call a method. Used to start behavior.

Initialize a Callable property. Safer than a method as ownership of the method is unnecessary. Used to start behavior.

Initialize a Node or other Object reference.

Initialize a NodePath.

These options hide the points of access from the child node. This in turn keeps the child loosely coupled to its environment. You can reuse it in another context without any extra changes to its API.

Although the examples above illustrate parent-child relationships, the same principles apply towards all object relations. Nodes which are siblings should only be aware of their own hierarchies while an ancestor mediates their communications and references.

The same principles also apply to non-Node objects that maintain dependencies on other objects. Whichever object owns the other objects should manage the relationships between them.

You should favor keeping data in-house (internal to a scene), though, as placing a dependency on an external context, even a loosely coupled one, still means that the node will expect something in its environment to be true. The project's design philosophies should prevent this from happening. If not, the code's inherent liabilities will force developers to use documentation to keep track of object relations on a microscopic scale; this is otherwise known as development hell. Writing code that relies on external documentation to use it safely is error-prone by default.

To avoid creating and maintaining such documentation, you convert the dependent node ("child" above) into a tool script that implements _get_configuration_warnings(). Returning a non-empty PackedStringArray from it will make the Scene dock generate a warning icon with the string(s) as a tooltip by the node. This is the same icon that appears for nodes such as the Area2D node when it has no child CollisionShape2D nodes defined. The editor then self-documents the scene through the script code. No content duplication via documentation is necessary.

A GUI like this can better inform project users of critical information about a Node. Does it have external dependencies? Have those dependencies been satisfied? Other programmers, and especially designers and writers, will need clear instructions in the messages telling them what to do to configure it.

So, why does all this complex switcheroo work? Well, because scenes operate best when they operate alone. If unable to work alone, then working with others anonymously (with minimal hard dependencies, i.e. loose coupling) is the next best thing. Inevitably, changes may need to be made to a class, and if these changes cause it to interact with other scenes in unforeseen ways, then things will start to break down. The whole point of all this indirection is to avoid ending up in a situation where changing one class results in adversely affecting other classes dependent on it.

Scripts and scenes, as extensions of engine classes, should abide by all OOP principles. Examples include...

You might start to work on a game but get overwhelmed by the vast possibilities before you. You might know what you want to do, what systems you want to have, but where do you put them all? How you go about making your game is always up to you. You can construct node trees in countless ways. If you are unsure, this guide can give you a sample of a decent structure to start with.

A game should always have an "entry point"; somewhere you can definitively track where things begin so that you can follow the logic as it continues elsewhere. It also serves as a bird's eye view of all other data and logic in the program. For traditional applications, this is normally a "main" function. In Godot, it's a Main node.

Node "Main" (main.gd)

The main.gd script will serve as the primary controller of your game.

Then you have an in-game "World" (a 2D or 3D one). This can be a child of Main. In addition, you will need a primary GUI for your game that manages the various menus and widgets the project needs.

Node2D/Node3D "World" (game_world.gd)

Control "GUI" (gui.gd)

When changing levels, you can then swap out the children of the "World" node. Changing scenes manually gives you full control over how your game world transitions.

The next step is to consider what gameplay systems your project requires. If you have a system that...

tracks all of its data internally

should be globally accessible

should exist in isolation

... then you should create an autoload 'singleton' node.

For smaller games, a simpler alternative with less control would be to have a "Game" singleton that simply calls the SceneTree.change_scene_to_file() method to swap out the main scene's content. This structure more or less keeps the "World" as the main game node.

Any GUI would also need to be either a singleton, a transitory part of the "World", or manually added as a direct child of the root. Otherwise, the GUI nodes would also delete themselves during scene transitions.

If you have systems that modify other systems' data, you should define those as their own scripts or scenes, rather than autoloads. For more information, see Autoloads versus regular nodes.

Each subsystem within your game should have its own section within the SceneTree. You should use parent-child relationships only in cases where nodes are effectively elements of their parents. Does removing the parent reasonably mean that the children should also be removed? If not, then it should have its own place in the hierarchy as a sibling or some other relation.

In some cases, you need these separated nodes to also position themselves relative to each other. You can use the RemoteTransform / RemoteTransform2D nodes for this purpose. They will allow a target node to conditionally inherit selected transform elements from the Remote* node. To assign the target NodePath, use one of the following:

A reliable third party, likely a parent node, to mediate the assignment.

A group, to pull a reference to the desired node (assuming there will only ever be one of the targets).

When you should do this is subjective. The dilemma arises when you must micro-manage when a node must move around the SceneTree to preserve itself. For example...

Add a "player" node to a "room".

Need to change rooms, so you must delete the current room.

Before the room can be deleted, you must preserve and/or move the player.

If memory is not a concern, you can...

Move the player to the new room.

If memory is a concern, instead you will need to...

Move the player somewhere else in the tree.

Instantiate and add the new room.

Re-add the player to the new room.

The issue is that the player here is a "special case" where the developers must know that they need to handle the player this way for the project. The only way to reliably share this information as a team is to document it. Keeping implementation details in documentation is dangerous. It's a maintenance burden, strains code readability, and unnecessarily bloats the intellectual content of a project.

In a more complex game with larger assets, it can be a better idea to keep the player somewhere else in the SceneTree entirely. This results in:

No "special cases" that must be documented and maintained somewhere.

No opportunity for errors to occur because these details are not accounted for.

In contrast, if you ever need a child node that does not inherit the transform of its parent, you have the following options:

The declarative solution: place a Node in between them. Since it doesn't have a transform, they won't pass this information to its children.

The imperative solution: Use the top_level property for the CanvasItem or Node3D node. This will make the node ignore its inherited transform.

If building a networked game, keep in mind which nodes and gameplay systems are relevant to all players versus those just pertinent to the authoritative server. For example, users do not all need to have a copy of every players' "PlayerController" logic - they only need their own. Keeping them in a separate branch from the "world" can help simplify the management of game connections and the like.

The key to scene organization is to consider the SceneTree in relational terms rather than spatial terms. Are the nodes dependent on their parent's existence? If not, then they can thrive all by themselves somewhere else. If they are dependent, then it stands to reason that they should be children of that parent (and likely part of that parent's scene if they aren't already).

Does this mean nodes themselves are components? Not at all. Godot's node trees form an aggregation relationship, not one of composition. But while you still have the flexibility to move nodes around, it is still best when such moves are unnecessary by default.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (markdown):
```markdown
# Parent
$Child.signal_name.connect(method_on_the_object)

# Child
signal_name.emit() # Triggers parent-defined behavior.
```

Example 2 (unknown):
```unknown
// Parent
GetNode("Child").Connect("SignalName", Callable.From(ObjectWithMethod.MethodOnTheObject));

// Child
EmitSignal("SignalName"); // Triggers parent-defined behavior.
```

Example 3 (php):
```php
// Parent
Node *node = get_node<Node>("Child");
if (node != nullptr) {
    // Note that get_node may return a nullptr, which would make calling the connect method crash the engine if "Child" does not exist!
    // So unless you are 1000% sure get_node will never return a nullptr, it's a good idea to always do a nullptr check.
    node->connect("signal_name", callable_mp(this, &ObjectWithMethod::method_on_the_object));
}

// Child
emit_signal("signal_name"); // Triggers parent-defined behavior.
```

Example 4 (markdown):
```markdown
# Parent
$Child.method_name = "do"

# Child, assuming it has String property 'method_name' and method 'do'.
call(method_name) # Call parent-defined method (which child must own).
```

---

## Scene Unique Nodes

**URL:** https://docs.godotengine.org/en/stable/tutorials/scripting/scene_unique_nodes.html

**Contents:**
- Scene Unique Nodes
- Introduction
- Creation and usage
- Same-scene limitation
- Alternatives
- User-contributed notes

Using get_node() to reference nodes from a script can sometimes be fragile. If you move a button in a UI scene from one panel to another, the button's node path changes, and if a script uses get_node() with a hard-coded node path, the script will not be able to find the button anymore.

In situations like this, the node can be turned into a scene unique node to avoid having to update the script every time the node's path is changed.

There are two ways to create a scene unique node.

In the Scene tree dock, right-click on a node and select Access as Unique Name in the context menu.

After selecting the option, the node will now have a percent symbol (%) next to its name in the scene tree:

You can also do this while renaming the node by adding "%" to the beginning of the name. Once you confirm, the percent symbol will appear next to its name.

You can now use the node in your script. For example, you can reference it with a get_node() method call by typing the % symbol, followed by the node's name:

A scene unique node can only be retrieved by a node inside the same scene. To demonstrate this limitation, consider this example Player scene that instances a Sword scene:

Here are the results of get_node() calls inside the Player script:

get_node("%Eyes") returns the Eyes node.

get_node("%Hilt") returns null.

These are the results of get_node() calls inside the Sword script:

get_node("%Eyes") returns null.

get_node("%Hilt") returns the Hilt node.

If a script has access to a node in another scene, it can call get_node() on that node to get scene unique nodes from that node's scene. This also works in a node path, which avoids multiple get_node() calls. Here are two ways to get the Hilt node from the Player script using scene unique nodes:

get_node("Hand/Sword").get_node("%Hilt") returns the Hilt node.

get_node("Hand/Sword/%Hilt") also returns the Hilt node.

Scene unique names don't only work at the end of a node path. They can be used in the middle to navigate from one node to another. For example, the Sword node is marked as a scene unique node in the Player scene, so this is possible:

get_node("%Sword/%Hilt") returns the Hilt node.

Scene unique nodes are a useful tool to navigate a scene. However, there are some situations where other techniques may be better.

A Group allows locating a node (or a group of many nodes) from any other node, no matter what scene the two nodes are located in.

A Singleton (Autoload) is an always loaded node that can be accessed directly by any node regardless of the scene. These are useful when some data or functionality is shared globally.

Node.find_child() finds a node by name without knowing its full path. This seems similar to a scene unique node, but this method is able to find nodes in nested scenes, and doesn't require marking the node in the scene editor in any way. However, this method is slow. Scene unique nodes are cached by Godot and are fast to retrieve, but each time the method is called, find_child() needs to check every descendant (every child, grandchild, and so on).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
get_node("%RedButton").text = "Hello"
%RedButton.text = "Hello" # Shorter syntax
```

Example 2 (typescript):
```typescript
GetNode<Button>("%RedButton").Text = "Hello";
```

---

## Theme

**URL:** https://docs.godotengine.org/en/stable/classes/class_theme.html

**Contents:**
- Theme
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

A resource used for styling/skinning Controls and Windows.

A resource used for styling/skinning Control and Window nodes. While individual controls can be styled using their local theme overrides (see Control.add_theme_color_override()), theme resources allow you to store and apply the same settings across all controls sharing the same type (e.g. style all Buttons the same). One theme resource can be used for the entire project, but you can also set a separate theme resource to a branch of control nodes. A theme resource assigned to a control applies to the control itself, as well as all of its direct and indirect children (as long as a chain of controls is uninterrupted).

Use ProjectSettings.gui/theme/custom to set up a project-scope theme that will be available to every control in your project.

Use Control.theme of any control node to set up a theme that will be available to that control and all of its direct and indirect children.

Using the theme editor

add_type(theme_type: StringName)

clear_color(name: StringName, theme_type: StringName)

clear_constant(name: StringName, theme_type: StringName)

clear_font(name: StringName, theme_type: StringName)

clear_font_size(name: StringName, theme_type: StringName)

clear_icon(name: StringName, theme_type: StringName)

clear_stylebox(name: StringName, theme_type: StringName)

clear_theme_item(data_type: DataType, name: StringName, theme_type: StringName)

clear_type_variation(theme_type: StringName)

get_color(name: StringName, theme_type: StringName) const

get_color_list(theme_type: String) const

get_color_type_list() const

get_constant(name: StringName, theme_type: StringName) const

get_constant_list(theme_type: String) const

get_constant_type_list() const

get_font(name: StringName, theme_type: StringName) const

get_font_list(theme_type: String) const

get_font_size(name: StringName, theme_type: StringName) const

get_font_size_list(theme_type: String) const

get_font_size_type_list() const

get_font_type_list() const

get_icon(name: StringName, theme_type: StringName) const

get_icon_list(theme_type: String) const

get_icon_type_list() const

get_stylebox(name: StringName, theme_type: StringName) const

get_stylebox_list(theme_type: String) const

get_stylebox_type_list() const

get_theme_item(data_type: DataType, name: StringName, theme_type: StringName) const

get_theme_item_list(data_type: DataType, theme_type: String) const

get_theme_item_type_list(data_type: DataType) const

get_type_list() const

get_type_variation_base(theme_type: StringName) const

get_type_variation_list(base_type: StringName) const

has_color(name: StringName, theme_type: StringName) const

has_constant(name: StringName, theme_type: StringName) const

has_default_base_scale() const

has_default_font() const

has_default_font_size() const

has_font(name: StringName, theme_type: StringName) const

has_font_size(name: StringName, theme_type: StringName) const

has_icon(name: StringName, theme_type: StringName) const

has_stylebox(name: StringName, theme_type: StringName) const

has_theme_item(data_type: DataType, name: StringName, theme_type: StringName) const

is_type_variation(theme_type: StringName, base_type: StringName) const

merge_with(other: Theme)

remove_type(theme_type: StringName)

rename_color(old_name: StringName, name: StringName, theme_type: StringName)

rename_constant(old_name: StringName, name: StringName, theme_type: StringName)

rename_font(old_name: StringName, name: StringName, theme_type: StringName)

rename_font_size(old_name: StringName, name: StringName, theme_type: StringName)

rename_icon(old_name: StringName, name: StringName, theme_type: StringName)

rename_stylebox(old_name: StringName, name: StringName, theme_type: StringName)

rename_theme_item(data_type: DataType, old_name: StringName, name: StringName, theme_type: StringName)

rename_type(old_theme_type: StringName, theme_type: StringName)

set_color(name: StringName, theme_type: StringName, color: Color)

set_constant(name: StringName, theme_type: StringName, constant: int)

set_font(name: StringName, theme_type: StringName, font: Font)

set_font_size(name: StringName, theme_type: StringName, font_size: int)

set_icon(name: StringName, theme_type: StringName, texture: Texture2D)

set_stylebox(name: StringName, theme_type: StringName, texture: StyleBox)

set_theme_item(data_type: DataType, name: StringName, theme_type: StringName, value: Variant)

set_type_variation(theme_type: StringName, base_type: StringName)

DataType DATA_TYPE_COLOR = 0

Theme's Color item type.

DataType DATA_TYPE_CONSTANT = 1

Theme's constant item type.

DataType DATA_TYPE_FONT = 2

Theme's Font item type.

DataType DATA_TYPE_FONT_SIZE = 3

Theme's font size item type.

DataType DATA_TYPE_ICON = 4

Theme's icon Texture2D item type.

DataType DATA_TYPE_STYLEBOX = 5

Theme's StyleBox item type.

DataType DATA_TYPE_MAX = 6

Maximum value for the DataType enum.

float default_base_scale = 0.0 🔗

void set_default_base_scale(value: float)

float get_default_base_scale()

The default base scale factor of this theme resource. Used by some controls to scale their visual properties based on the global scale factor. If this value is set to 0.0, the global scale factor is used (see ThemeDB.fallback_base_scale).

Use has_default_base_scale() to check if this value is valid.

void set_default_font(value: Font)

Font get_default_font()

The default font of this theme resource. Used as the default value when trying to fetch a font resource that doesn't exist in this theme or is in invalid state. If the default font is also missing or invalid, the engine fallback value is used (see ThemeDB.fallback_font).

Use has_default_font() to check if this value is valid.

int default_font_size = -1 🔗

void set_default_font_size(value: int)

int get_default_font_size()

The default font size of this theme resource. Used as the default value when trying to fetch a font size value that doesn't exist in this theme or is in invalid state. If the default font size is also missing or invalid, the engine fallback value is used (see ThemeDB.fallback_font_size).

Values below 1 are invalid and can be used to unset the property. Use has_default_font_size() to check if this value is valid.

void add_type(theme_type: StringName) 🔗

Adds an empty theme type for every valid data type.

Note: Empty types are not saved with the theme. This method only exists to perform in-memory changes to the resource. Use available set_* methods to add theme items.

Removes all the theme properties defined on the theme resource.

void clear_color(name: StringName, theme_type: StringName) 🔗

Removes the Color property defined by name and theme_type, if it exists.

Fails if it doesn't exist. Use has_color() to check for existence.

void clear_constant(name: StringName, theme_type: StringName) 🔗

Removes the constant property defined by name and theme_type, if it exists.

Fails if it doesn't exist. Use has_constant() to check for existence.

void clear_font(name: StringName, theme_type: StringName) 🔗

Removes the Font property defined by name and theme_type, if it exists.

Fails if it doesn't exist. Use has_font() to check for existence.

void clear_font_size(name: StringName, theme_type: StringName) 🔗

Removes the font size property defined by name and theme_type, if it exists.

Fails if it doesn't exist. Use has_font_size() to check for existence.

void clear_icon(name: StringName, theme_type: StringName) 🔗

Removes the icon property defined by name and theme_type, if it exists.

Fails if it doesn't exist. Use has_icon() to check for existence.

void clear_stylebox(name: StringName, theme_type: StringName) 🔗

Removes the StyleBox property defined by name and theme_type, if it exists.

Fails if it doesn't exist. Use has_stylebox() to check for existence.

void clear_theme_item(data_type: DataType, name: StringName, theme_type: StringName) 🔗

Removes the theme property of data_type defined by name and theme_type, if it exists.

Fails if it doesn't exist. Use has_theme_item() to check for existence.

Note: This method is analogous to calling the corresponding data type specific method, but can be used for more generalized logic.

void clear_type_variation(theme_type: StringName) 🔗

Unmarks theme_type as being a variation of another theme type. See set_type_variation().

Color get_color(name: StringName, theme_type: StringName) const 🔗

Returns the Color property defined by name and theme_type, if it exists.

Returns the default color value if the property doesn't exist. Use has_color() to check for existence.

PackedStringArray get_color_list(theme_type: String) const 🔗

Returns a list of names for Color properties defined with theme_type. Use get_color_type_list() to get a list of possible theme type names.

PackedStringArray get_color_type_list() const 🔗

Returns a list of all unique theme type names for Color properties. Use get_type_list() to get a list of all unique theme types.

int get_constant(name: StringName, theme_type: StringName) const 🔗

Returns the constant property defined by name and theme_type, if it exists.

Returns 0 if the property doesn't exist. Use has_constant() to check for existence.

PackedStringArray get_constant_list(theme_type: String) const 🔗

Returns a list of names for constant properties defined with theme_type. Use get_constant_type_list() to get a list of possible theme type names.

PackedStringArray get_constant_type_list() const 🔗

Returns a list of all unique theme type names for constant properties. Use get_type_list() to get a list of all unique theme types.

Font get_font(name: StringName, theme_type: StringName) const 🔗

Returns the Font property defined by name and theme_type, if it exists.

Returns the default theme font if the property doesn't exist and the default theme font is set up (see default_font). Use has_font() to check for existence of the property and has_default_font() to check for existence of the default theme font.

Returns the engine fallback font value, if neither exist (see ThemeDB.fallback_font).

PackedStringArray get_font_list(theme_type: String) const 🔗

Returns a list of names for Font properties defined with theme_type. Use get_font_type_list() to get a list of possible theme type names.

int get_font_size(name: StringName, theme_type: StringName) const 🔗

Returns the font size property defined by name and theme_type, if it exists.

Returns the default theme font size if the property doesn't exist and the default theme font size is set up (see default_font_size). Use has_font_size() to check for existence of the property and has_default_font_size() to check for existence of the default theme font.

Returns the engine fallback font size value, if neither exist (see ThemeDB.fallback_font_size).

PackedStringArray get_font_size_list(theme_type: String) const 🔗

Returns a list of names for font size properties defined with theme_type. Use get_font_size_type_list() to get a list of possible theme type names.

PackedStringArray get_font_size_type_list() const 🔗

Returns a list of all unique theme type names for font size properties. Use get_type_list() to get a list of all unique theme types.

PackedStringArray get_font_type_list() const 🔗

Returns a list of all unique theme type names for Font properties. Use get_type_list() to get a list of all unique theme types.

Texture2D get_icon(name: StringName, theme_type: StringName) const 🔗

Returns the icon property defined by name and theme_type, if it exists.

Returns the engine fallback icon value if the property doesn't exist (see ThemeDB.fallback_icon). Use has_icon() to check for existence.

PackedStringArray get_icon_list(theme_type: String) const 🔗

Returns a list of names for icon properties defined with theme_type. Use get_icon_type_list() to get a list of possible theme type names.

PackedStringArray get_icon_type_list() const 🔗

Returns a list of all unique theme type names for icon properties. Use get_type_list() to get a list of all unique theme types.

StyleBox get_stylebox(name: StringName, theme_type: StringName) const 🔗

Returns the StyleBox property defined by name and theme_type, if it exists.

Returns the engine fallback stylebox value if the property doesn't exist (see ThemeDB.fallback_stylebox). Use has_stylebox() to check for existence.

PackedStringArray get_stylebox_list(theme_type: String) const 🔗

Returns a list of names for StyleBox properties defined with theme_type. Use get_stylebox_type_list() to get a list of possible theme type names.

PackedStringArray get_stylebox_type_list() const 🔗

Returns a list of all unique theme type names for StyleBox properties. Use get_type_list() to get a list of all unique theme types.

Variant get_theme_item(data_type: DataType, name: StringName, theme_type: StringName) const 🔗

Returns the theme property of data_type defined by name and theme_type, if it exists.

Returns the engine fallback value if the property doesn't exist (see ThemeDB). Use has_theme_item() to check for existence.

Note: This method is analogous to calling the corresponding data type specific method, but can be used for more generalized logic.

PackedStringArray get_theme_item_list(data_type: DataType, theme_type: String) const 🔗

Returns a list of names for properties of data_type defined with theme_type. Use get_theme_item_type_list() to get a list of possible theme type names.

Note: This method is analogous to calling the corresponding data type specific method, but can be used for more generalized logic.

PackedStringArray get_theme_item_type_list(data_type: DataType) const 🔗

Returns a list of all unique theme type names for data_type properties. Use get_type_list() to get a list of all unique theme types.

Note: This method is analogous to calling the corresponding data type specific method, but can be used for more generalized logic.

PackedStringArray get_type_list() const 🔗

Returns a list of all unique theme type names. Use the appropriate get_*_type_list method to get a list of unique theme types for a single data type.

StringName get_type_variation_base(theme_type: StringName) const 🔗

Returns the name of the base theme type if theme_type is a valid variation type. Returns an empty string otherwise.

PackedStringArray get_type_variation_list(base_type: StringName) const 🔗

Returns a list of all type variations for the given base_type.

bool has_color(name: StringName, theme_type: StringName) const 🔗

Returns true if the Color property defined by name and theme_type exists.

Returns false if it doesn't exist. Use set_color() to define it.

bool has_constant(name: StringName, theme_type: StringName) const 🔗

Returns true if the constant property defined by name and theme_type exists.

Returns false if it doesn't exist. Use set_constant() to define it.

bool has_default_base_scale() const 🔗

Returns true if default_base_scale has a valid value.

Returns false if it doesn't. The value must be greater than 0.0 to be considered valid.

bool has_default_font() const 🔗

Returns true if default_font has a valid value.

Returns false if it doesn't.

bool has_default_font_size() const 🔗

Returns true if default_font_size has a valid value.

Returns false if it doesn't. The value must be greater than 0 to be considered valid.

bool has_font(name: StringName, theme_type: StringName) const 🔗

Returns true if the Font property defined by name and theme_type exists, or if the default theme font is set up (see has_default_font()).

Returns false if neither exist. Use set_font() to define the property.

bool has_font_size(name: StringName, theme_type: StringName) const 🔗

Returns true if the font size property defined by name and theme_type exists, or if the default theme font size is set up (see has_default_font_size()).

Returns false if neither exist. Use set_font_size() to define the property.

bool has_icon(name: StringName, theme_type: StringName) const 🔗

Returns true if the icon property defined by name and theme_type exists.

Returns false if it doesn't exist. Use set_icon() to define it.

bool has_stylebox(name: StringName, theme_type: StringName) const 🔗

Returns true if the StyleBox property defined by name and theme_type exists.

Returns false if it doesn't exist. Use set_stylebox() to define it.

bool has_theme_item(data_type: DataType, name: StringName, theme_type: StringName) const 🔗

Returns true if the theme property of data_type defined by name and theme_type exists.

Returns false if it doesn't exist. Use set_theme_item() to define it.

Note: This method is analogous to calling the corresponding data type specific method, but can be used for more generalized logic.

bool is_type_variation(theme_type: StringName, base_type: StringName) const 🔗

Returns true if theme_type is marked as a variation of base_type.

void merge_with(other: Theme) 🔗

Adds missing and overrides existing definitions with values from the other theme resource.

Note: This modifies the current theme. If you want to merge two themes together without modifying either one, create a new empty theme and merge the other two into it one after another.

void remove_type(theme_type: StringName) 🔗

Removes the theme type, gracefully discarding defined theme items. If the type is a variation, this information is also erased. If the type is a base for type variations, those variations lose their base.

void rename_color(old_name: StringName, name: StringName, theme_type: StringName) 🔗

Renames the Color property defined by old_name and theme_type to name, if it exists.

Fails if it doesn't exist, or if a similar property with the new name already exists. Use has_color() to check for existence, and clear_color() to remove the existing property.

void rename_constant(old_name: StringName, name: StringName, theme_type: StringName) 🔗

Renames the constant property defined by old_name and theme_type to name, if it exists.

Fails if it doesn't exist, or if a similar property with the new name already exists. Use has_constant() to check for existence, and clear_constant() to remove the existing property.

void rename_font(old_name: StringName, name: StringName, theme_type: StringName) 🔗

Renames the Font property defined by old_name and theme_type to name, if it exists.

Fails if it doesn't exist, or if a similar property with the new name already exists. Use has_font() to check for existence, and clear_font() to remove the existing property.

void rename_font_size(old_name: StringName, name: StringName, theme_type: StringName) 🔗

Renames the font size property defined by old_name and theme_type to name, if it exists.

Fails if it doesn't exist, or if a similar property with the new name already exists. Use has_font_size() to check for existence, and clear_font_size() to remove the existing property.

void rename_icon(old_name: StringName, name: StringName, theme_type: StringName) 🔗

Renames the icon property defined by old_name and theme_type to name, if it exists.

Fails if it doesn't exist, or if a similar property with the new name already exists. Use has_icon() to check for existence, and clear_icon() to remove the existing property.

void rename_stylebox(old_name: StringName, name: StringName, theme_type: StringName) 🔗

Renames the StyleBox property defined by old_name and theme_type to name, if it exists.

Fails if it doesn't exist, or if a similar property with the new name already exists. Use has_stylebox() to check for existence, and clear_stylebox() to remove the existing property.

void rename_theme_item(data_type: DataType, old_name: StringName, name: StringName, theme_type: StringName) 🔗

Renames the theme property of data_type defined by old_name and theme_type to name, if it exists.

Fails if it doesn't exist, or if a similar property with the new name already exists. Use has_theme_item() to check for existence, and clear_theme_item() to remove the existing property.

Note: This method is analogous to calling the corresponding data type specific method, but can be used for more generalized logic.

void rename_type(old_theme_type: StringName, theme_type: StringName) 🔗

Renames the theme type old_theme_type to theme_type, if the old type exists and the new one doesn't exist.

Note: Renaming a theme type to an empty name or a variation to a type associated with a built-in class removes type variation connections in a way that cannot be undone by reversing the rename alone.

void set_color(name: StringName, theme_type: StringName, color: Color) 🔗

Creates or changes the value of the Color property defined by name and theme_type. Use clear_color() to remove the property.

void set_constant(name: StringName, theme_type: StringName, constant: int) 🔗

Creates or changes the value of the constant property defined by name and theme_type. Use clear_constant() to remove the property.

void set_font(name: StringName, theme_type: StringName, font: Font) 🔗

Creates or changes the value of the Font property defined by name and theme_type. Use clear_font() to remove the property.

void set_font_size(name: StringName, theme_type: StringName, font_size: int) 🔗

Creates or changes the value of the font size property defined by name and theme_type. Use clear_font_size() to remove the property.

void set_icon(name: StringName, theme_type: StringName, texture: Texture2D) 🔗

Creates or changes the value of the icon property defined by name and theme_type. Use clear_icon() to remove the property.

void set_stylebox(name: StringName, theme_type: StringName, texture: StyleBox) 🔗

Creates or changes the value of the StyleBox property defined by name and theme_type. Use clear_stylebox() to remove the property.

void set_theme_item(data_type: DataType, name: StringName, theme_type: StringName, value: Variant) 🔗

Creates or changes the value of the theme property of data_type defined by name and theme_type. Use clear_theme_item() to remove the property.

Fails if the value type is not accepted by data_type.

Note: This method is analogous to calling the corresponding data type specific method, but can be used for more generalized logic.

void set_type_variation(theme_type: StringName, base_type: StringName) 🔗

Marks theme_type as a variation of base_type.

This adds theme_type as a suggested option for Control.theme_type_variation on a Control that is of the base_type class.

Variations can also be nested, i.e. base_type can be another variation. If a chain of variations ends with a base_type matching the class of the Control, the whole chain is going to be suggested as options.

Note: Suggestions only show up if this theme resource is set as the project default theme. See ProjectSettings.gui/theme/custom.

Please read the User-contributed notes policy before submitting a comment.

---

## TileSetScenesCollectionSource

**URL:** https://docs.godotengine.org/en/stable/classes/class_tilesetscenescollectionsource.html

**Contents:**
- TileSetScenesCollectionSource
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: TileSetSource < Resource < RefCounted < Object

Exposes a set of scenes as tiles for a TileSet resource.

When placed on a TileMapLayer, tiles from TileSetScenesCollectionSource will automatically instantiate an associated scene at the cell's position in the TileMapLayer.

Scenes are instantiated as children of the TileMapLayer after it enters the tree, at the end of the frame (their creation is deferred). If you add/remove a scene tile in the TileMapLayer that is already inside the tree, the TileMapLayer will automatically instantiate/free the scene accordingly.

Note: Scene tiles all occupy one tile slot and instead use alternate tile ID to identify scene index. TileSetSource.get_tiles_count() will always return 1. Use get_scene_tiles_count() to get a number of scenes in a TileSetScenesCollectionSource.

Use this code if you want to find the scene path at a given tile in TileMapLayer:

create_scene_tile(packed_scene: PackedScene, id_override: int = -1)

get_next_scene_tile_id() const

get_scene_tile_display_placeholder(id: int) const

get_scene_tile_id(index: int)

get_scene_tile_scene(id: int) const

get_scene_tiles_count()

has_scene_tile_id(id: int)

remove_scene_tile(id: int)

set_scene_tile_display_placeholder(id: int, display_placeholder: bool)

set_scene_tile_id(id: int, new_id: int)

set_scene_tile_scene(id: int, packed_scene: PackedScene)

int create_scene_tile(packed_scene: PackedScene, id_override: int = -1) 🔗

Creates a scene-based tile out of the given scene.

Returns a newly generated unique ID.

int get_next_scene_tile_id() const 🔗

Returns the scene ID a following call to create_scene_tile() would return.

bool get_scene_tile_display_placeholder(id: int) const 🔗

Returns whether the scene tile with id displays a placeholder in the editor.

int get_scene_tile_id(index: int) 🔗

Returns the scene tile ID of the scene tile at index.

PackedScene get_scene_tile_scene(id: int) const 🔗

Returns the PackedScene resource of scene tile with id.

int get_scene_tiles_count() 🔗

Returns the number or scene tiles this TileSet source has.

bool has_scene_tile_id(id: int) 🔗

Returns whether this TileSet source has a scene tile with id.

void remove_scene_tile(id: int) 🔗

Remove the scene tile with id.

void set_scene_tile_display_placeholder(id: int, display_placeholder: bool) 🔗

Sets whether or not the scene tile with id should display a placeholder in the editor. This might be useful for scenes that are not visible.

void set_scene_tile_id(id: int, new_id: int) 🔗

Changes a scene tile's ID from id to new_id. This will fail if there is already a tile with an ID equal to new_id.

void set_scene_tile_scene(id: int, packed_scene: PackedScene) 🔗

Assigns a PackedScene resource to the scene tile with id. This will fail if the scene does not extend CanvasItem, as positioning properties are needed to place the scene on the TileMapLayer.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var source_id = tile_map_layer.get_cell_source_id(Vector2i(x, y))
if source_id > -1:
    var scene_source = tile_map_layer.tile_set.get_source(source_id)
    if scene_source is TileSetScenesCollectionSource:
        var alt_id = tile_map_layer.get_cell_alternative_tile(Vector2i(x, y))
        # The assigned PackedScene.
        var scene = scene_source.get_scene_tile_scene(alt_id)
```

Example 2 (json):
```json
int sourceId = tileMapLayer.GetCellSourceId(new Vector2I(x, y));
if (sourceId > -1)
{
    TileSetSource source = tileMapLayer.TileSet.GetSource(sourceId);
    if (source is TileSetScenesCollectionSource sceneSource)
    {
        int altId = tileMapLayer.GetCellAlternativeTile(new Vector2I(x, y));
        // The assigned PackedScene.
        PackedScene scene = sceneSource.GetSceneTileScene(altId);
    }
}
```

---

## VisualShaderNodeSample3D

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodesample3d.html

**Contents:**
- VisualShaderNodeSample3D
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeTexture2DArray, VisualShaderNodeTexture3D

A base node for nodes which samples 3D textures in the visual shader graph.

A virtual class, use the descendants instead.

Source SOURCE_TEXTURE = 0

Creates internal uniform and provides a way to assign it within node.

Source SOURCE_PORT = 1

Use the uniform texture from sampler port.

Source SOURCE_MAX = 2

Represents the size of the Source enum.

void set_source(value: Source)

An input source type.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeScreenNormalWorldSpace

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodescreennormalworldspace.html

**Contents:**
- VisualShaderNodeScreenNormalWorldSpace
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node that unpacks the screen normal texture in World Space.

The ScreenNormalWorldSpace node allows to create outline effects.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeScreenUVToSDF

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodescreenuvtosdf.html

**Contents:**
- VisualShaderNodeScreenUVToSDF
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A function to convert screen UV to an SDF (signed-distance field), to be used within the visual shader graph.

Translates to screen_uv_to_sdf(uv) in the shader language. If the UV port isn't connected, SCREEN_UV is used instead.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeSDFRaymarch

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodesdfraymarch.html

**Contents:**
- VisualShaderNodeSDFRaymarch
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

SDF raymarching algorithm to be used within the visual shader graph.

Casts a ray against the screen SDF (signed-distance field) and returns the distance travelled.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeSDFToScreenUV

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodesdftoscreenuv.html

**Contents:**
- VisualShaderNodeSDFToScreenUV
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A function to convert an SDF (signed-distance field) to screen UV, to be used within the visual shader graph.

Translates to sdf_to_screen_uv(sdf_pos) in the shader language.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeSmoothStep

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodesmoothstep.html

**Contents:**
- VisualShaderNodeSmoothStep
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Calculates a SmoothStep function within the visual shader graph.

Translates to smoothstep(edge0, edge1, x) in the shader language.

Returns 0.0 if x is smaller than edge0 and 1.0 if x is larger than edge1. Otherwise, the return value is interpolated between 0.0 and 1.0 using Hermite polynomials.

OpType OP_TYPE_SCALAR = 0

A floating-point scalar type.

OpType OP_TYPE_VECTOR_2D = 1

OpType OP_TYPE_VECTOR_2D_SCALAR = 2

The x port uses a 2D vector type. The first two ports use a floating-point scalar type.

OpType OP_TYPE_VECTOR_3D = 3

OpType OP_TYPE_VECTOR_3D_SCALAR = 4

The x port uses a 3D vector type. The first two ports use a floating-point scalar type.

OpType OP_TYPE_VECTOR_4D = 5

OpType OP_TYPE_VECTOR_4D_SCALAR = 6

The a and b ports use a 4D vector type. The weight port uses a scalar type.

OpType OP_TYPE_MAX = 7

Represents the size of the OpType enum.

void set_op_type(value: OpType)

A type of operands and returned value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeStep

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodestep.html

**Contents:**
- VisualShaderNodeStep
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Calculates a Step function within the visual shader graph.

Translates to step(edge, x) in the shader language.

Returns 0.0 if x is smaller than edge and 1.0 otherwise.

OpType OP_TYPE_SCALAR = 0

A floating-point scalar type.

OpType OP_TYPE_VECTOR_2D = 1

OpType OP_TYPE_VECTOR_2D_SCALAR = 2

The x port uses a 2D vector type, while the edge port uses a floating-point scalar type.

OpType OP_TYPE_VECTOR_3D = 3

OpType OP_TYPE_VECTOR_3D_SCALAR = 4

The x port uses a 3D vector type, while the edge port uses a floating-point scalar type.

OpType OP_TYPE_VECTOR_4D = 5

OpType OP_TYPE_VECTOR_4D_SCALAR = 6

The a and b ports use a 4D vector type. The weight port uses a scalar type.

OpType OP_TYPE_MAX = 7

Represents the size of the OpType enum.

void set_op_type(value: OpType)

A type of operands and returned value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeSwitch

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeswitch.html

**Contents:**
- VisualShaderNodeSwitch
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A selector function for use within the visual shader graph.

Returns an associated value of the op_type type if the provided boolean value is true or false.

OpType OP_TYPE_FLOAT = 0

A floating-point scalar.

OpType OP_TYPE_INT = 1

OpType OP_TYPE_UINT = 2

An unsigned integer scalar.

OpType OP_TYPE_VECTOR_2D = 3

OpType OP_TYPE_VECTOR_3D = 4

OpType OP_TYPE_VECTOR_4D = 5

OpType OP_TYPE_BOOLEAN = 6

OpType OP_TYPE_TRANSFORM = 7

OpType OP_TYPE_MAX = 8

Represents the size of the OpType enum.

void set_op_type(value: OpType)

A type of operands and returned value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShader

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshader.html

**Contents:**
- VisualShader
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Constants
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Shader < Resource < RefCounted < Object

A custom shader program with a visual editor.

This class provides a graph-like visual editor for creating a Shader. Although VisualShaders do not require coding, they share the same logic with script shaders. They use VisualShaderNodes that can be connected to each other to control the flow of the shader. The visual shader graph is converted to a script shader behind the scenes.

add_node(type: Type, node: VisualShaderNode, position: Vector2, id: int)

add_varying(name: String, mode: VaryingMode, type: VaryingType)

attach_node_to_frame(type: Type, id: int, frame: int)

can_connect_nodes(type: Type, from_node: int, from_port: int, to_node: int, to_port: int) const

connect_nodes(type: Type, from_node: int, from_port: int, to_node: int, to_port: int)

connect_nodes_forced(type: Type, from_node: int, from_port: int, to_node: int, to_port: int)

detach_node_from_frame(type: Type, id: int)

disconnect_nodes(type: Type, from_node: int, from_port: int, to_node: int, to_port: int)

get_node(type: Type, id: int) const

get_node_connections(type: Type) const

get_node_list(type: Type) const

get_node_position(type: Type, id: int) const

get_valid_node_id(type: Type) const

has_varying(name: String) const

is_node_connection(type: Type, from_node: int, from_port: int, to_node: int, to_port: int) const

remove_node(type: Type, id: int)

remove_varying(name: String)

replace_node(type: Type, id: int, new_class: StringName)

set_node_position(type: Type, id: int, position: Vector2)

A vertex shader, operating on vertices.

Type TYPE_FRAGMENT = 1

A fragment shader, operating on fragments (pixels).

A shader for light calculations.

A function for the "start" stage of particle shader.

Type TYPE_PROCESS = 4

A function for the "process" stage of particle shader.

Type TYPE_COLLIDE = 5

A function for the "collide" stage (particle collision handler) of particle shader.

Type TYPE_START_CUSTOM = 6

A function for the "start" stage of particle shader, with customized output.

Type TYPE_PROCESS_CUSTOM = 7

A function for the "process" stage of particle shader, with customized output.

A shader for 3D environment's sky.

A compute shader that runs for each froxel of the volumetric fog map.

Represents the size of the Type enum.

VaryingMode VARYING_MODE_VERTEX_TO_FRAG_LIGHT = 0

Varying is passed from Vertex function to Fragment and Light functions.

VaryingMode VARYING_MODE_FRAG_TO_LIGHT = 1

Varying is passed from Fragment function to Light function.

VaryingMode VARYING_MODE_MAX = 2

Represents the size of the VaryingMode enum.

VaryingType VARYING_TYPE_FLOAT = 0

Varying is of type float.

VaryingType VARYING_TYPE_INT = 1

Varying is of type int.

VaryingType VARYING_TYPE_UINT = 2

Varying is of type unsigned int.

VaryingType VARYING_TYPE_VECTOR_2D = 3

Varying is of type Vector2.

VaryingType VARYING_TYPE_VECTOR_3D = 4

Varying is of type Vector3.

VaryingType VARYING_TYPE_VECTOR_4D = 5

Varying is of type Vector4.

VaryingType VARYING_TYPE_BOOLEAN = 6

Varying is of type bool.

VaryingType VARYING_TYPE_TRANSFORM = 7

Varying is of type Transform3D.

VaryingType VARYING_TYPE_MAX = 8

Represents the size of the VaryingType enum.

NODE_ID_INVALID = -1 🔗

Indicates an invalid VisualShader node.

Indicates an output node of VisualShader.

Vector2 graph_offset 🔗

void set_graph_offset(value: Vector2)

Vector2 get_graph_offset()

Deprecated: This property does nothing and always equals to zero.

void add_node(type: Type, node: VisualShaderNode, position: Vector2, id: int) 🔗

Adds the specified node to the shader.

void add_varying(name: String, mode: VaryingMode, type: VaryingType) 🔗

Adds a new varying value node to the shader.

void attach_node_to_frame(type: Type, id: int, frame: int) 🔗

Attaches the given node to the given frame.

bool can_connect_nodes(type: Type, from_node: int, from_port: int, to_node: int, to_port: int) const 🔗

Returns true if the specified nodes and ports can be connected together.

Error connect_nodes(type: Type, from_node: int, from_port: int, to_node: int, to_port: int) 🔗

Connects the specified nodes and ports.

void connect_nodes_forced(type: Type, from_node: int, from_port: int, to_node: int, to_port: int) 🔗

Connects the specified nodes and ports, even if they can't be connected. Such connection is invalid and will not function properly.

void detach_node_from_frame(type: Type, id: int) 🔗

Detaches the given node from the frame it is attached to.

void disconnect_nodes(type: Type, from_node: int, from_port: int, to_node: int, to_port: int) 🔗

Connects the specified nodes and ports.

VisualShaderNode get_node(type: Type, id: int) const 🔗

Returns the shader node instance with specified type and id.

Array[Dictionary] get_node_connections(type: Type) const 🔗

Returns the list of connected nodes with the specified type.

PackedInt32Array get_node_list(type: Type) const 🔗

Returns the list of all nodes in the shader with the specified type.

Vector2 get_node_position(type: Type, id: int) const 🔗

Returns the position of the specified node within the shader graph.

int get_valid_node_id(type: Type) const 🔗

Returns next valid node ID that can be added to the shader graph.

bool has_varying(name: String) const 🔗

Returns true if the shader has a varying with the given name.

bool is_node_connection(type: Type, from_node: int, from_port: int, to_node: int, to_port: int) const 🔗

Returns true if the specified node and port connection exist.

void remove_node(type: Type, id: int) 🔗

Removes the specified node from the shader.

void remove_varying(name: String) 🔗

Removes a varying value node with the given name. Prints an error if a node with this name is not found.

void replace_node(type: Type, id: int, new_class: StringName) 🔗

Replaces the specified node with a node of new class type.

void set_mode(mode: Mode) 🔗

Sets the mode of this shader.

void set_node_position(type: Type, id: int, position: Vector2) 🔗

Sets the position of the specified node.

Please read the User-contributed notes policy before submitting a comment.

---

## When and how to avoid using nodes for everything

**URL:** https://docs.godotengine.org/en/stable/tutorials/best_practices/node_alternatives.html

**Contents:**
- When and how to avoid using nodes for everything
- User-contributed notes

Nodes are cheap to produce, but even they have their limits. A project may have tens of thousands of nodes all doing things. The more complex their behavior though, the larger the strain each one adds to a project's performance.

Godot provides more lightweight objects for creating APIs which nodes use. Be sure to keep these in mind as options when designing how you wish to build your project's features.

Object: The ultimate lightweight object, the original Object must use manual memory management. With that said, it isn't too difficult to create one's own custom data structures, even node structures, that are also lighter than the Node class.

Example: See the Tree node. It supports a high level of customization for a table of content with an arbitrary number of rows and columns. The data that it uses to generate its visualization though is actually a tree of TreeItem Objects.

Advantages: Simplifying one's API to smaller scoped objects helps improve its accessibility and improve iteration time. Rather than working with the entire Node library, one creates an abbreviated set of Objects from which a node can generate and manage the appropriate sub-nodes.

One should be careful when handling them. One can store an Object into a variable, but these references can become invalid without warning. For example, if the object's creator decides to delete it out of nowhere, this would trigger an error state when one next accesses it.

RefCounted: Only a little more complex than Object. They track references to themselves, only deleting loaded memory when no further references to themselves exist. These are useful in the majority of cases where one needs data in a custom class.

Example: See the FileAccess object. It functions just like a regular Object except that one need not delete it themselves.

Advantages: same as the Object.

Resource: Only slightly more complex than RefCounted. They have the innate ability to serialize/deserialize (i.e. save and load) their object properties to/from Godot resource files.

Example: Scripts, PackedScene (for scene files), and other types like each of the AudioEffect classes. Each of these can be saved and loaded, therefore they extend from Resource.

Advantages: Much has already been said on Resource's advantages over traditional data storage methods. In the context of using Resources over Nodes though, their main advantage is in Inspector-compatibility. While nearly as lightweight as Object/RefCounted, they can still display and export properties in the Inspector. This allows them to fulfill a purpose much like sub-Nodes on the usability front, but also improve performance if one plans to have many such Resources/Nodes in their scenes.

Please read the User-contributed notes policy before submitting a comment.

---

## When to use scenes versus scripts

**URL:** https://docs.godotengine.org/en/stable/tutorials/best_practices/scenes_versus_scripts.html

**Contents:**
- When to use scenes versus scripts
- Anonymous types
- Named types
- Performance of Script vs PackedScene
- Conclusion
- User-contributed notes

We've already covered how scenes and scripts are different. Scripts define an engine class extension with imperative code, scenes with declarative code.

Each system's capabilities are different as a result. Scenes can define how an extended class initializes, but not what its behavior actually is. Scenes are often used in conjunction with a script, the scene declaring a composition of nodes, and the script adding behavior with imperative code.

It is possible to completely define a scenes' contents using a script alone. This is, in essence, what the Godot Editor does, only in the C++ constructor of its objects.

But, choosing which one to use can be a dilemma. Creating script instances is identical to creating in-engine classes whereas handling scenes requires a change in API:

Also, scripts will operate a little slower than scenes due to the speed differences between engine and script code. The larger and more complex the node, the more reason there is to build it as a scene.

Scripts can be registered as a new type within the editor itself. This displays it as a new type in the node or resource creation dialog with an optional icon. This way, the user's ability to use the script is much more streamlined. Rather than having to...

Know the base type of the script they would like to use.

Create an instance of that base type.

Add the script to the node.

With a registered script, the scripted type instead becomes a creation option like the other nodes and resources in the system. The creation dialog even has a search bar to look up the type by name.

There are two systems for registering types:

Editor-only. Typenames are not accessible at runtime.

Does not support inherited custom types.

An initializer tool. Creates the node with the script. Nothing more.

Editor has no type-awareness of the script or its relationship to other engine types or scripts.

Allows users to define an icon.

Works for all scripting languages because it deals with Script resources in abstract.

Set up using EditorPlugin.add_custom_type.

Editor and runtime accessible.

Displays inheritance relationships in full.

Creates the node with the script, but can also change types or extend the type from the editor.

Editor is aware of inheritance relationships between scripts, script classes, and engine C++ classes.

Allows users to define an icon.

Engine developers must add support for languages manually (both name exposure and runtime accessibility).

The Editor scans project folders and registers any exposed names for all scripting languages. Each scripting language must implement its own support for exposing this information.

Both methodologies add names to the creation dialog, but script classes, in particular, also allow for users to access the typename without loading the script resource. Creating instances and accessing constants or static methods is viable from anywhere.

With features like these, one may wish their type to be a script without a scene due to the ease of use it grants users. Those developing plugins or creating in-house tools for designers to use will find an easier time of things this way.

On the downside, it also means having to use largely imperative programming.

One last aspect to consider when choosing scenes and scripts is execution speed.

As the size of objects increases, the scripts' necessary size to create and initialize them grows much larger. Creating node hierarchies demonstrates this. Each Node's logic could be several hundred lines of code in length.

The code example below creates a new Node, changes its name, assigns a script to it, sets its future parent as its owner so it gets saved to disk along with it, and finally adds it as a child of the Main node:

Script code like this is much slower than engine-side C++ code. Each instruction makes a call to the scripting API which leads to many "lookups" on the back-end to find the logic to execute.

Scenes help to avoid this performance issue. PackedScene, the base type that scenes inherit from, defines resources that use serialized data to create objects. The engine can process scenes in batches on the back-end and provide much better performance than scripts.

In the end, the best approach is to consider the following:

If one wishes to create a basic tool that is going to be re-used in several different projects and which people of all skill levels will likely use (including those who don't label themselves as "programmers"), then chances are that it should probably be a script, likely one with a custom name/icon.

If one wishes to create a concept that is particular to their game, then it should always be a scene. Scenes are easier to track/edit and provide more security than scripts.

If one would like to give a name to a scene, then they can still sort of do this by declaring a script class and giving it a scene as a constant. The script becomes, in effect, a namespace:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (javascript):
```javascript
const MyNode = preload("my_node.gd")
const MyScene = preload("my_scene.tscn")
var node = Node.new()
var my_node = MyNode.new() # Same method call.
var my_scene = MyScene.instantiate() # Different method call.
var my_inherited_scene = MyScene.instantiate(PackedScene.GEN_EDIT_STATE_MAIN) # Create scene inheriting from MyScene.
```

Example 2 (swift):
```swift
using Godot;

public partial class Game : Node
{
    public static CSharpScript MyNode { get; } =
        GD.Load<CSharpScript>("res://Path/To/MyNode.cs");
    public static PackedScene MyScene { get; } =
        GD.Load<PackedScene>("res://Path/To/MyScene.tscn");
    private Node _node;
    private Node _myNode;
    private Node _myScene;
    private Node _myInheritedScene;

    public Game()
    {
        _node = new Node();
        _myNode = MyNode.New().As<Node>();
        // Different than calling new() or MyNode.New(). Instantiated from a PackedScene.
        _myScene = MyScene.Instantiate();
        // Create scene inheriting from MyScene.
        _myInheritedScene = MyScene.Instantiate(PackedScene.GenEditState.Main);
    }
}
```

Example 3 (gdscript):
```gdscript
# main.gd
extends Node

func _init():
    var child = Node.new()
    child.name = "Child"
    child.script = preload("child.gd")
    add_child(child)
    child.owner = self
```

Example 4 (csharp):
```csharp
using Godot;

public partial class Main : Node
{
    public Node Child { get; set; }

    public Main()
    {
        Child = new Node();
        Child.Name = "Child";
        var childID = Child.GetInstanceId();
        Child.SetScript(GD.Load<Script>("res://Path/To/Child.cs"));
        // SetScript() causes the C# wrapper object to be disposed, so obtain a new
        // wrapper for the Child node using its instance ID before proceeding.
        Child = (Node)GodotObject.InstanceFromId(childID);
        AddChild(Child);
        Child.Owner = this;
    }
}
```

---

## World2D

**URL:** https://docs.godotengine.org/en/stable/classes/class_world2d.html

**Contents:**
- World2D
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

A resource that holds all components of a 2D world, such as a canvas and a physics space.

Class that has everything pertaining to a 2D world: A physics space, a canvas, and a sound space. 2D nodes register their resources into the current 2D world.

PhysicsDirectSpaceState2D

The RID of this world's canvas resource. Used by the RenderingServer for 2D drawing.

PhysicsDirectSpaceState2D direct_space_state 🔗

PhysicsDirectSpaceState2D get_direct_space_state()

Direct access to the world's physics 2D space state. Used for querying current and potential collisions. When using multi-threaded physics, access is limited to Node._physics_process() in the main thread.

RID get_navigation_map()

The RID of this world's navigation map. Used by the NavigationServer2D.

The RID of this world's physics space resource. Used by the PhysicsServer2D for 2D physics, treating it as both a space and an area.

Please read the User-contributed notes policy before submitting a comment.

---

## World3D

**URL:** https://docs.godotengine.org/en/stable/classes/class_world3d.html

**Contents:**
- World3D
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

A resource that holds all components of a 3D world, such as a visual scenario and a physics space.

Class that has everything pertaining to a world: A physics space, a visual scenario, and a sound space. 3D nodes register their resources into the current 3D world.

PhysicsDirectSpaceState3D

CameraAttributes camera_attributes 🔗

void set_camera_attributes(value: CameraAttributes)

CameraAttributes get_camera_attributes()

The default CameraAttributes resource to use if none set on the Camera3D.

PhysicsDirectSpaceState3D direct_space_state 🔗

PhysicsDirectSpaceState3D get_direct_space_state()

Direct access to the world's physics 3D space state. Used for querying current and potential collisions. When using multi-threaded physics, access is limited to Node._physics_process() in the main thread.

Environment environment 🔗

void set_environment(value: Environment)

Environment get_environment()

The World3D's Environment.

Environment fallback_environment 🔗

void set_fallback_environment(value: Environment)

Environment get_fallback_environment()

The World3D's fallback environment will be used if environment fails or is missing.

RID get_navigation_map()

The RID of this world's navigation map. Used by the NavigationServer3D.

The World3D's visual scenario.

The World3D's physics space.

Please read the User-contributed notes policy before submitting a comment.

---
