# Godot - Rendering

**Pages:** 156

---

## Advanced post-processing

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/advanced_postprocessing.html

**Contents:**
- Advanced post-processing
- Introduction
- Full screen quad
- Depth texture
- Example shader
- An optimization
- User-contributed notes

This tutorial describes an advanced method for post-processing in Godot. In particular, it will explain how to write a post-processing shader that uses the depth buffer. You should already be familiar with post-processing generally and, in particular, with the methods outlined in the custom post-processing tutorial.

One way to make custom post-processing effects is by using a viewport. However, there are two main drawbacks of using a Viewport:

The depth buffer cannot be accessed

The effect of the post-processing shader is not visible in the editor

To get around the limitation on using the depth buffer, use a MeshInstance3D with a QuadMesh primitive. This allows us to use a shader and to access the depth texture of the scene. Next, use a vertex shader to make the quad cover the screen at all times so that the post-processing effect will be applied at all times, including in the editor.

First, create a new MeshInstance3D and set its mesh to a QuadMesh. This creates a quad centered at position (0, 0, 0) with a width and height of 1. Set the width and height to 2 and enable Flip Faces. Right now, the quad occupies a position in world space at the origin. However, we want it to move with the camera so that it always covers the entire screen. To do this, we will bypass the coordinate transforms that translate the vertex positions through the difference coordinate spaces and treat the vertices as if they were already in clip space.

The vertex shader expects coordinates to be output in clip space, which are coordinates ranging from -1 at the left and bottom of the screen to 1 at the top and right of the screen. This is why the QuadMesh needs to have height and width of 2. Godot handles the transform from model to view space to clip space behind the scenes, so we need to nullify the effects of Godot's transformations. We do this by setting the POSITION built-in to our desired position. POSITION bypasses the built-in transformations and sets the vertex position in clip space directly.

In versions of Godot earlier than 4.3, this code recommended using POSITION = vec4(VERTEX, 1.0); which implicitly assumed the clip-space near plane was at 0.0. That code is now incorrect and will not work in versions 4.3+ as we use a "reversed-z" depth buffer now where the near plane is at 1.0.

Even with this vertex shader, the quad keeps disappearing. This is due to frustum culling, which is done on the CPU. Frustum culling uses the camera matrix and the AABBs of Meshes to determine if the Mesh will be visible before passing it to the GPU. The CPU has no knowledge of what we are doing with the vertices, so it assumes the coordinates specified refer to world positions, not clip space positions, which results in Godot culling the quad when we turn away from the center of the scene. In order to keep the quad from being culled, there are a few options:

Add the QuadMesh as a child to the camera, so the camera is always pointed at it

Set the Geometry property extra_cull_margin as large as possible in the QuadMesh

The second option ensures that the quad is visible in the editor, while the first option guarantees that it will still be visible even if the camera moves outside the cull margin. You can also use both options.

To read from the depth texture, we first need to create a texture uniform set to the depth buffer by using hint_depth_texture.

Once defined, the depth texture can be read with the texture() function.

Similar to accessing the screen texture, accessing the depth texture is only possible when reading from the current viewport. The depth texture cannot be accessed from another viewport to which you have rendered.

The values returned by depth_texture are between 1.0 and 0.0 (corresponding to the near and far plane, respectively, because of using a "reverse-z" depth buffer) and are nonlinear. When displaying depth directly from the depth_texture, everything will look almost black unless it is very close due to that nonlinearity. In order to make the depth value align with world or model coordinates, we need to linearize the value. When we apply the projection matrix to the vertex position, the z value is made nonlinear, so to linearize it, we multiply it by the inverse of the projection matrix, which in Godot, is accessible with the variable INV_PROJECTION_MATRIX.

Firstly, take the screen space coordinates and transform them into normalized device coordinates (NDC). NDC run -1.0 to 1.0 in x and y directions and from 0.0 to 1.0 in the z direction when using the Vulkan backend. Reconstruct the NDC using SCREEN_UV for the x and y axis, and the depth value for z.

This tutorial assumes the use of the Forward+ or Mobile renderers, which both use Vulkan NDCs with a Z-range of [0.0, 1.0]. In contrast, the Compatibility renderer uses OpenGL NDCs with a Z-range of [-1.0, 1.0]. For the Compatibility renderer, replace the NDC calculation with this instead:

You can also use the CURRENT_RENDERER and RENDERER_COMPATIBILITY built-in defines for a shader that will work in all renderers:

Convert NDC to view space by multiplying the NDC by INV_PROJECTION_MATRIX. Recall that view space gives positions relative to the camera, so the z value will give us the distance to the point.

Because the camera is facing the negative z direction, the position will have a negative z value. In order to get a usable depth value, we have to negate view.z.

The world position can be constructed from the depth buffer using the following code, using the INV_VIEW_MATRIX to transform the position from view space into world space.

Once we add a line to output to ALBEDO, we have a complete shader that looks something like this. This shader lets you visualize the linear depth or world space coordinates, depending on which line is commented out.

You can benefit from using a single large triangle rather than using a full screen quad. The reason for this is explained here. However, the benefit is quite small and only beneficial when running especially complex fragment shaders.

Set the Mesh in the MeshInstance3D to an ArrayMesh. An ArrayMesh is a tool that allows you to easily construct a Mesh from Arrays for vertices, normals, colors, etc.

Now, attach a script to the MeshInstance3D and use the following code:

The triangle is specified in normalized device coordinates. Recall, NDC run from -1.0 to 1.0 in both the x and y directions. This makes the screen 2 units wide and 2 units tall. In order to cover the entire screen with a single triangle, use a triangle that is 4 units wide and 4 units tall, double its height and width.

Assign the same vertex shader from above and everything should look exactly the same.

The one drawback to using an ArrayMesh over using a QuadMesh is that the ArrayMesh is not visible in the editor because the triangle is not constructed until the scene is run. To get around that, construct a single triangle Mesh in a modeling program and use that in the MeshInstance3D instead.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (sql):
```sql
shader_type spatial;
// Prevent the quad from being affected by lighting and fog. This also improves performance.
render_mode unshaded, fog_disabled;

void vertex() {
  POSITION = vec4(VERTEX.xy, 1.0, 1.0);
}
```

Example 2 (unknown):
```unknown
uniform sampler2D depth_texture : hint_depth_texture;
```

Example 3 (unknown):
```unknown
float depth = texture(depth_texture, SCREEN_UV).x;
```

Example 4 (cpp):
```cpp
void fragment() {
  float depth = texture(depth_texture, SCREEN_UV).x;
  vec3 ndc = vec3(SCREEN_UV * 2.0 - 1.0, depth);
}
```

---

## CameraAttributesPhysical

**URL:** https://docs.godotengine.org/en/stable/classes/class_cameraattributesphysical.html

**Contents:**
- CameraAttributesPhysical
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: CameraAttributes < Resource < RefCounted < Object

Physically-based camera settings.

CameraAttributesPhysical is used to set rendering settings based on a physically-based camera's settings. It is responsible for exposure, auto-exposure, and depth of field.

When used in a WorldEnvironment it provides default settings for exposure, auto-exposure, and depth of field that will be used by all cameras without their own CameraAttributes, including the editor camera. When used in a Camera3D it will override any CameraAttributes set in the WorldEnvironment and will override the Camera3Ds Camera3D.far, Camera3D.near, Camera3D.fov, and Camera3D.keep_aspect properties. When used in VoxelGI or LightmapGI, only the exposure settings will be used.

The default settings are intended for use in an outdoor environment, tips for settings for use in an indoor environment can be found in each setting's documentation.

Note: Depth of field blur is only supported in the Forward+ and Mobile rendering methods, not Compatibility.

Physical light and camera units

auto_exposure_max_exposure_value

auto_exposure_min_exposure_value

exposure_shutter_speed

frustum_focus_distance

float auto_exposure_max_exposure_value = 10.0 🔗

void set_auto_exposure_max_exposure_value(value: float)

float get_auto_exposure_max_exposure_value()

The maximum luminance (in EV100) used when calculating auto exposure. When calculating scene average luminance, color values will be clamped to at least this value. This limits the auto-exposure from exposing below a certain brightness, resulting in a cut off point where the scene will remain bright.

float auto_exposure_min_exposure_value = -8.0 🔗

void set_auto_exposure_min_exposure_value(value: float)

float get_auto_exposure_min_exposure_value()

The minimum luminance (in EV100) used when calculating auto exposure. When calculating scene average luminance, color values will be clamped to at least this value. This limits the auto-exposure from exposing above a certain brightness, resulting in a cut off point where the scene will remain dark.

float exposure_aperture = 16.0 🔗

void set_aperture(value: float)

Size of the aperture of the camera, measured in f-stops. An f-stop is a unitless ratio between the focal length of the camera and the diameter of the aperture. A high aperture setting will result in a smaller aperture which leads to a dimmer image and sharper focus. A low aperture results in a wide aperture which lets in more light resulting in a brighter, less-focused image. Default is appropriate for outdoors at daytime (i.e. for use with a default DirectionalLight3D), for indoor lighting, a value between 2 and 4 is more appropriate.

Only available when ProjectSettings.rendering/lights_and_shadows/use_physical_light_units is enabled.

float exposure_shutter_speed = 100.0 🔗

void set_shutter_speed(value: float)

float get_shutter_speed()

Time for shutter to open and close, evaluated as 1 / shutter_speed seconds. A higher value will allow less light (leading to a darker image), while a lower value will allow more light (leading to a brighter image).

Only available when ProjectSettings.rendering/lights_and_shadows/use_physical_light_units is enabled.

float frustum_far = 4000.0 🔗

void set_far(value: float)

Override value for Camera3D.far. Used internally when calculating depth of field. When attached to a Camera3D as its Camera3D.attributes, it will override the Camera3D.far property.

float frustum_focal_length = 35.0 🔗

void set_focal_length(value: float)

float get_focal_length()

Distance between camera lens and camera aperture, measured in millimeters. Controls field of view and depth of field. A larger focal length will result in a smaller field of view and a narrower depth of field meaning fewer objects will be in focus. A smaller focal length will result in a wider field of view and a larger depth of field meaning more objects will be in focus. When attached to a Camera3D as its Camera3D.attributes, it will override the Camera3D.fov property and the Camera3D.keep_aspect property.

float frustum_focus_distance = 10.0 🔗

void set_focus_distance(value: float)

float get_focus_distance()

Distance from camera of object that will be in focus, measured in meters. Internally this will be clamped to be at least 1 millimeter larger than frustum_focal_length.

float frustum_near = 0.05 🔗

void set_near(value: float)

Override value for Camera3D.near. Used internally when calculating depth of field. When attached to a Camera3D as its Camera3D.attributes, it will override the Camera3D.near property.

float get_fov() const 🔗

Returns the vertical field of view that corresponds to the frustum_focal_length. This value is calculated internally whenever frustum_focal_length is changed.

Please read the User-contributed notes policy before submitting a comment.

---

## CameraFeed

**URL:** https://docs.godotengine.org/en/stable/classes/class_camerafeed.html

**Contents:**
- CameraFeed
- Description
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

A camera feed gives you access to a single physical camera attached to your device.

A camera feed gives you access to a single physical camera attached to your device. When enabled, Godot will start capturing frames from the camera which can then be used. See also CameraServer.

Note: Many cameras will return YCbCr images which are split into two textures and need to be combined in a shader. Godot does this automatically for you if you set the environment to show the camera image in the background.

Note: This class is currently only implemented on Linux, Android, macOS, and iOS. On other platforms no CameraFeeds will be available. To get a CameraFeed on iOS, the camera plugin from godot-ios-plugins is required.

Transform2D(1, 0, 0, -1, 0, 1)

_activate_feed() virtual

_deactivate_feed() virtual

get_texture_tex_id(feed_image_type: FeedImage)

set_external(width: int, height: int)

set_format(index: int, parameters: Dictionary)

set_name(name: String)

set_position(position: FeedPosition)

set_rgb_image(rgb_image: Image)

set_ycbcr_image(ycbcr_image: Image)

Emitted when the format has changed.

Emitted when a new frame is available.

FeedDataType FEED_NOIMAGE = 0

No image set for the feed.

FeedDataType FEED_RGB = 1

Feed supplies RGB images.

FeedDataType FEED_YCBCR = 2

Feed supplies YCbCr images that need to be converted to RGB.

FeedDataType FEED_YCBCR_SEP = 3

Feed supplies separate Y and CbCr images that need to be combined and converted to RGB.

FeedDataType FEED_EXTERNAL = 4

Feed supplies external image.

FeedPosition FEED_UNSPECIFIED = 0

Unspecified position.

FeedPosition FEED_FRONT = 1

Camera is mounted at the front of the device.

FeedPosition FEED_BACK = 2

Camera is mounted at the back of the device.

bool feed_is_active = false 🔗

void set_active(value: bool)

If true, the feed is active.

Transform2D feed_transform = Transform2D(1, 0, 0, -1, 0, 1) 🔗

void set_transform(value: Transform2D)

Transform2D get_transform()

The transform applied to the camera's image.

Formats supported by the feed. Each entry is a Dictionary describing format parameters.

bool _activate_feed() virtual 🔗

Called when the camera feed is activated.

void _deactivate_feed() virtual 🔗

Called when the camera feed is deactivated.

FeedDataType get_datatype() const 🔗

Returns feed image data type.

Returns the unique ID for this feed.

String get_name() const 🔗

Returns the camera's name.

FeedPosition get_position() const 🔗

Returns the position of camera on the device.

int get_texture_tex_id(feed_image_type: FeedImage) 🔗

Returns the texture backend ID (usable by some external libraries that need a handle to a texture to write data).

void set_external(width: int, height: int) 🔗

Sets the feed as external feed provided by another library.

bool set_format(index: int, parameters: Dictionary) 🔗

Sets the feed format parameters for the given index in the formats array. Returns true on success. By default, the YUYV encoded stream is transformed to FEED_RGB. The YUYV encoded stream output format can be changed by setting parameters's output entry to one of the following:

"separate" will result in FEED_YCBCR_SEP;

"grayscale" will result in desaturated FEED_RGB;

"copy" will result in FEED_YCBCR.

void set_name(name: String) 🔗

Sets the camera's name.

void set_position(position: FeedPosition) 🔗

Sets the position of this camera.

void set_rgb_image(rgb_image: Image) 🔗

Sets RGB image for this feed.

void set_ycbcr_image(ycbcr_image: Image) 🔗

Sets YCbCr image for this feed.

Please read the User-contributed notes policy before submitting a comment.

---

## CanvasGroup

**URL:** https://docs.godotengine.org/en/stable/classes/class_canvasgroup.html

**Contents:**
- CanvasGroup
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Node2D < CanvasItem < Node < Object

Merges several 2D nodes into a single draw operation.

Child CanvasItem nodes of a CanvasGroup are drawn as a single object. It allows to e.g. draw overlapping translucent 2D nodes without blending (set CanvasItem.self_modulate property of CanvasGroup to achieve this effect).

Note: The CanvasGroup uses a custom shader to read from the backbuffer to draw its children. Assigning a Material to the CanvasGroup overrides the builtin shader. To duplicate the behavior of the builtin shader in a custom Shader use the following:

Note: Since CanvasGroup and CanvasItem.clip_children both utilize the backbuffer, children of a CanvasGroup who have their CanvasItem.clip_children set to anything other than CanvasItem.CLIP_CHILDREN_DISABLED will not function correctly.

float clear_margin = 10.0 🔗

void set_clear_margin(value: float)

float get_clear_margin()

Sets the size of the margin used to expand the clearing rect of this CanvasGroup. This expands the area of the backbuffer that will be used by the CanvasGroup. A smaller margin will reduce the area of the backbuffer used which can increase performance, however if use_mipmaps is enabled, a small margin may result in mipmap errors at the edge of the CanvasGroup. Accordingly, this should be left as small as possible, but should be increased if artifacts appear along the edges of the canvas group.

float fit_margin = 10.0 🔗

void set_fit_margin(value: float)

float get_fit_margin()

Sets the size of a margin used to expand the drawable rect of this CanvasGroup. The size of the CanvasGroup is determined by fitting a rect around its children then expanding that rect by fit_margin. This increases both the backbuffer area used and the area covered by the CanvasGroup both of which can reduce performance. This should be kept as small as possible and should only be expanded when an increased size is needed (e.g. for custom shader effects).

bool use_mipmaps = false 🔗

void set_use_mipmaps(value: bool)

bool is_using_mipmaps()

If true, calculates mipmaps for the backbuffer before drawing the CanvasGroup so that mipmaps can be used in a custom ShaderMaterial attached to the CanvasGroup. Generating mipmaps has a performance cost so this should not be enabled unless required.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (cpp):
```cpp
shader_type canvas_item;
render_mode unshaded;

uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

void fragment() {
    vec4 c = textureLod(screen_texture, SCREEN_UV, 0.0);

    if (c.a > 0.0001) {
        c.rgb /= c.a;
    }

    COLOR *= c;
}
```

---

## CanvasItemMaterial

**URL:** https://docs.godotengine.org/en/stable/classes/class_canvasitemmaterial.html

**Contents:**
- CanvasItemMaterial
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: Material < Resource < RefCounted < Object

A material for CanvasItems.

CanvasItemMaterials provide a means of modifying the textures associated with a CanvasItem. They specialize in describing blend and lighting behaviors for textures. Use a ShaderMaterial to more fully customize a material's interactions with a CanvasItem.

particles_anim_h_frames

particles_anim_v_frames

BlendMode BLEND_MODE_MIX = 0

Mix blending mode. Colors are assumed to be independent of the alpha (opacity) value.

BlendMode BLEND_MODE_ADD = 1

Additive blending mode.

BlendMode BLEND_MODE_SUB = 2

Subtractive blending mode.

BlendMode BLEND_MODE_MUL = 3

Multiplicative blending mode.

BlendMode BLEND_MODE_PREMULT_ALPHA = 4

Mix blending mode. Colors are assumed to be premultiplied by the alpha (opacity) value.

LightMode LIGHT_MODE_NORMAL = 0

Render the material using both light and non-light sensitive material properties.

LightMode LIGHT_MODE_UNSHADED = 1

Render the material as if there were no light.

LightMode LIGHT_MODE_LIGHT_ONLY = 2

Render the material as if there were only light.

BlendMode blend_mode = 0 🔗

void set_blend_mode(value: BlendMode)

BlendMode get_blend_mode()

The manner in which a material's rendering is applied to underlying textures.

LightMode light_mode = 0 🔗

void set_light_mode(value: LightMode)

LightMode get_light_mode()

The manner in which material reacts to lighting.

int particles_anim_h_frames 🔗

void set_particles_anim_h_frames(value: int)

int get_particles_anim_h_frames()

The number of columns in the spritesheet assigned as Texture2D for a GPUParticles2D or CPUParticles2D.

Note: This property is only used and visible in the editor if particles_animation is true.

bool particles_anim_loop 🔗

void set_particles_anim_loop(value: bool)

bool get_particles_anim_loop()

If true, the particles animation will loop.

Note: This property is only used and visible in the editor if particles_animation is true.

int particles_anim_v_frames 🔗

void set_particles_anim_v_frames(value: int)

int get_particles_anim_v_frames()

The number of rows in the spritesheet assigned as Texture2D for a GPUParticles2D or CPUParticles2D.

Note: This property is only used and visible in the editor if particles_animation is true.

bool particles_animation = false 🔗

void set_particles_animation(value: bool)

bool get_particles_animation()

If true, enable spritesheet-based animation features when assigned to GPUParticles2D and CPUParticles2D nodes. The ParticleProcessMaterial.anim_speed_max or CPUParticles2D.anim_speed_max should also be set to a positive value for the animation to play.

This property (and other particles_anim_* properties that depend on it) has no effect on other types of nodes.

Please read the User-contributed notes policy before submitting a comment.

---

## CompositorEffect

**URL:** https://docs.godotengine.org/en/stable/classes/class_compositoreffect.html

**Contents:**
- CompositorEffect
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Experimental: The implementation may change as more of the rendering internals are exposed over time.

Inherits: Resource < RefCounted < Object

This resource allows for creating a custom rendering effect.

This resource defines a custom rendering effect that can be applied to Viewports through the viewports' Environment. You can implement a callback that is called during rendering at a given stage of the rendering pipeline and allows you to insert additional passes. Note that this callback happens on the rendering thread. CompositorEffect is an abstract base class and must be extended to implement specific rendering logic.

access_resolved_color

access_resolved_depth

needs_normal_roughness

needs_separate_specular

_render_callback(effect_callback_type: int, render_data: RenderData) virtual

enum EffectCallbackType: 🔗

EffectCallbackType EFFECT_CALLBACK_TYPE_PRE_OPAQUE = 0

The callback is called before our opaque rendering pass, but after depth prepass (if applicable).

EffectCallbackType EFFECT_CALLBACK_TYPE_POST_OPAQUE = 1

The callback is called after our opaque rendering pass, but before our sky is rendered.

EffectCallbackType EFFECT_CALLBACK_TYPE_POST_SKY = 2

The callback is called after our sky is rendered, but before our back buffers are created (and if enabled, before subsurface scattering and/or screen space reflections).

EffectCallbackType EFFECT_CALLBACK_TYPE_PRE_TRANSPARENT = 3

The callback is called before our transparent rendering pass, but after our sky is rendered and we've created our back buffers.

EffectCallbackType EFFECT_CALLBACK_TYPE_POST_TRANSPARENT = 4

The callback is called after our transparent rendering pass, but before any built-in post-processing effects and output to our render target.

EffectCallbackType EFFECT_CALLBACK_TYPE_MAX = 5

Represents the size of the EffectCallbackType enum.

bool access_resolved_color 🔗

void set_access_resolved_color(value: bool)

bool get_access_resolved_color()

If true and MSAA is enabled, this will trigger a color buffer resolve before the effect is run.

Note: In _render_callback(), to access the resolved buffer use:

bool access_resolved_depth 🔗

void set_access_resolved_depth(value: bool)

bool get_access_resolved_depth()

If true and MSAA is enabled, this will trigger a depth buffer resolve before the effect is run.

Note: In _render_callback(), to access the resolved buffer use:

EffectCallbackType effect_callback_type 🔗

void set_effect_callback_type(value: EffectCallbackType)

EffectCallbackType get_effect_callback_type()

The type of effect that is implemented, determines at what stage of rendering the callback is called.

void set_enabled(value: bool)

If true this rendering effect is applied to any viewport it is added to.

bool needs_motion_vectors 🔗

void set_needs_motion_vectors(value: bool)

bool get_needs_motion_vectors()

If true this triggers motion vectors being calculated during the opaque render state.

Note: In _render_callback(), to access the motion vector buffer use:

bool needs_normal_roughness 🔗

void set_needs_normal_roughness(value: bool)

bool get_needs_normal_roughness()

If true this triggers normal and roughness data to be output during our depth pre-pass, only applicable for the Forward+ renderer.

Note: In _render_callback(), to access the roughness buffer use:

The raw normal and roughness buffer is stored in an optimized format, different than the one available in Spatial shaders. When sampling the buffer, a conversion function must be applied. Use this function, copied from here:

bool needs_separate_specular 🔗

void set_needs_separate_specular(value: bool)

bool get_needs_separate_specular()

If true this triggers specular data being rendered to a separate buffer and combined after effects have been applied, only applicable for the Forward+ renderer.

void _render_callback(effect_callback_type: int, render_data: RenderData) virtual 🔗

Implement this function with your custom rendering code. effect_callback_type should always match the effect callback type you've specified in effect_callback_type. render_data provides access to the rendering state, it is only valid during rendering and should not be stored.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var render_scene_buffers = render_data.get_render_scene_buffers()
var color_buffer = render_scene_buffers.get_texture("render_buffers", "color")
```

Example 2 (gdscript):
```gdscript
var render_scene_buffers = render_data.get_render_scene_buffers()
var depth_buffer = render_scene_buffers.get_texture("render_buffers", "depth")
```

Example 3 (gdscript):
```gdscript
var render_scene_buffers = render_data.get_render_scene_buffers()
var motion_buffer = render_scene_buffers.get_velocity_texture()
```

Example 4 (gdscript):
```gdscript
var render_scene_buffers = render_data.get_render_scene_buffers()
var roughness_buffer = render_scene_buffers.get_texture("forward_clustered", "normal_roughness")
```

---

## Compositor

**URL:** https://docs.godotengine.org/en/stable/classes/class_compositor.html

**Contents:**
- Compositor
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Experimental: More customization of the rendering pipeline will be added in the future.

Inherits: Resource < RefCounted < Object

Stores attributes used to customize how a Viewport is rendered.

The compositor resource stores attributes used to customize how a Viewport is rendered.

Array[CompositorEffect]

Array[CompositorEffect] compositor_effects = [] 🔗

void set_compositor_effects(value: Array[CompositorEffect])

Array[CompositorEffect] get_compositor_effects()

The custom CompositorEffects that are applied during rendering of viewports using this compositor.

Please read the User-contributed notes policy before submitting a comment.

---

## Converting GLSL to Godot shaders

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/converting_glsl_to_godot_shaders.html

**Contents:**
- Converting GLSL to Godot shaders
- GLSL
  - Shader programs
  - Vertex attributes
  - gl_Position
  - Varyings
  - Main
  - Macros
  - Variables
  - Coordinates

This document explains the differences between Godot's shading language and GLSL and gives practical advice on how to migrate shaders from other sources, such as Shadertoy and The Book of Shaders, into Godot shaders.

For detailed information on Godot's shading language, please refer to the Shading Language reference.

Godot uses a shading language based on GLSL with the addition of a few quality-of-life features. Accordingly, most features available in GLSL are available in Godot's shading language.

In GLSL, each shader uses a separate program. You have one program for the vertex shader and one for the fragment shader. In Godot, you have a single shader that contains a vertex and/or a fragment function. If you only choose to write one, Godot will supply the other.

Godot allows uniform variables and functions to be shared by defining the fragment and vertex shaders in one file. In GLSL, the vertex and fragment programs cannot share variables except when varyings are used.

In GLSL, you can pass in per-vertex information using attributes and have the flexibility to pass in as much or as little as you want. In Godot, you have a set number of input attributes, including VERTEX (position), COLOR, UV, UV2, NORMAL. Each shaders' page in the shader reference section of the documentation comes with a complete list of its vertex attributes.

gl_Position receives the final position of a vertex specified in the vertex shader. It is specified by the user in clip space. Typically, in GLSL, the model space vertex position is passed in using a vertex attribute called position and you handle the conversion from model space to clip space manually.

In Godot, VERTEX specifies the vertex position in model space at the beginning of the vertex function. Godot also handles the final conversion to clip space after the user-defined vertex function is run. If you want to skip the conversion from model to view space, you can set the render_mode to skip_vertex_transform. If you want to skip all transforms, set render_mode to skip_vertex_transform and set the PROJECTION_MATRIX to mat4(1.0) in order to nullify the final transform from view space to clip space.

Varyings are a type of variable that can be passed from the vertex shader to the fragment shader. In modern GLSL (3.0 and up), varyings are defined with the in and out keywords. A variable going out of the vertex shader is defined with out in the vertex shader and in inside the fragment shader.

In GLSL, each shader program looks like a self-contained C-style program. Accordingly, the main entry point is main. If you are copying a vertex shader, rename main to vertex and if you are copying a fragment shader, rename main to fragment.

The Godot shader preprocessor supports the following macros:

#if, #elif, #else, #endif, defined(), #ifdef, #ifndef

#include (only .gdshaderinc files and with a maximum depth of 25)

#pragma disable_preprocessor, which disables preprocessing for the rest of the file

GLSL has many built-in variables that are hard-coded. These variables are not uniforms, so they are not editable from the main program.

Output color for each pixel.

For full screen quads. For smaller quads, use UV.

Position of Vertex, output from Vertex Shader.

Size of Point primitive.

Position on point when drawing Point primitives.

True if front face of primitive.

gl_FragCoord in GLSL and FRAGCOORD in the Godot shading language use the same coordinate system. If using UV in Godot, the y-coordinate will be flipped upside down.

In GLSL, you can define the precision of a given type (float or int) at the top of the shader with the precision keyword. In Godot, you can set the precision of individual variables as you need by placing precision qualifiers lowp, mediump, and highp before the type when defining the variable. For more information, see the Shading Language reference.

Shadertoy is a website that makes it easy to write fragment shaders and create pure magic.

Shadertoy does not give the user full control over the shader. It handles all the input and uniforms and only lets the user write the fragment shader.

Shadertoy uses the webgl spec, so it runs a slightly different version of GLSL. However, it still has the regular types, including constants and macros.

The main point of entry to a Shadertoy shader is the mainImage function. mainImage has two parameters, fragColor and fragCoord, which correspond to COLOR and FRAGCOORD in Godot, respectively. These parameters are handled automatically in Godot, so you do not need to include them as parameters yourself. Anything in the mainImage function should be copied into the fragment function when porting to Godot.

In order to make writing fragment shaders straightforward and easy, Shadertoy handles passing a lot of helpful information from the main program into the fragment shader for you. A few of these have no equivalents in Godot because Godot has chosen not to make them available by default. This is okay because Godot gives you the ability to make your own uniforms. For variables whose equivalents are listed as "Provide with Uniform", users are responsible for creating that uniform themselves. The description gives the reader a hint about what they can pass in as a substitute.

Output color for each pixel.

For full screen quads. For smaller quads, use UV.

1.0 / SCREEN_PIXEL_SIZE

Can also pass in manually.

Time since shader started.

Time to render previous frame.

Time since that particular texture started.

Mouse position in pixel coordinates.

Current date, expressed in seconds.

iChannelResolution[4]

1.0 / TEXTURE_PIXEL_SIZE

Resolution of particular texture.

Godot provides only one built-in; user can make more.

fragCoord behaves the same as gl_FragCoord in GLSL and FRAGCOORD in Godot.

Similar to Shadertoy, The Book of Shaders provides access to a fragment shader in the web browser, with which the user may interact. The user is restricted to writing fragment shader code with a set list of uniforms passed in and with no ability to add additional uniforms.

For further help on porting shaders to various frameworks generally, The Book of Shaders provides a page on running shaders in various frameworks.

The Book of Shaders uses the webgl spec, so it runs a slightly different version of GLSL. However, it still has the regular types, including constants and macros.

The entry point for a Book of Shaders fragment shader is main, just like in GLSL. Everything written in a Book of Shaders main function should be copied into Godot's fragment function.

The Book of Shaders sticks closer to plain GLSL than Shadertoy does. It also implements fewer uniforms than Shadertoy.

Output color for each pixel.

For full screen quads. For smaller quads, use UV.

1.0 / SCREEN_PIXEL_SIZE

Can also pass in manually.

Time since shader started.

Mouse position in pixel coordinates.

The Book of Shaders uses the same coordinate system as GLSL.

Please read the User-contributed notes policy before submitting a comment.

---

## Cubemap

**URL:** https://docs.godotengine.org/en/stable/classes/class_cubemap.html

**Contents:**
- Cubemap
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: ImageTextureLayered < TextureLayered < Texture < Resource < RefCounted < Object

Six square textures representing the faces of a cube. Commonly used as a skybox.

A cubemap is made of 6 textures organized in layers. They are typically used for faking reflections in 3D rendering (see ReflectionProbe). It can be used to make an object look as if it's reflecting its surroundings. This usually delivers much better performance than other reflection methods.

This resource is typically used as a uniform in custom shaders. Few core Godot methods make use of Cubemap resources.

To create such a texture file yourself, reimport your image files using the Godot Editor import presets. To create a Cubemap from code, use ImageTextureLayered.create_from_images() on an instance of the Cubemap class.

The expected image order is X+, X-, Y+, Y-, Z+, Z- (in Godot's coordinate system, so Y+ is "up" and Z- is "forward"). You can use one of the following templates as a base:

2×3 cubemap template (default layout option)

Note: Godot doesn't support using cubemaps in a PanoramaSkyMaterial. To use a cubemap as a skybox, convert the default PanoramaSkyMaterial to a ShaderMaterial using the Convert to ShaderMaterial resource dropdown option, then replace its code with the following:

After replacing the shader code and saving, specify the imported Cubemap resource in the Shader Parameters section of the ShaderMaterial in the inspector.

Alternatively, you can use this tool to convert a cubemap to an equirectangular sky map and use PanoramaSkyMaterial as usual.

create_placeholder() const

Resource create_placeholder() const 🔗

Creates a placeholder version of this resource (PlaceholderCubemap).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (sql):
```sql
shader_type sky;

uniform samplerCube source_panorama : filter_linear, source_color, hint_default_black;
uniform float exposure : hint_range(0, 128) = 1.0;

void sky() {
    // If importing a cubemap from another engine, you may need to flip one of the `EYEDIR` components below
    // by replacing it with `-EYEDIR`.
    vec3 eyedir = vec3(EYEDIR.x, EYEDIR.y, EYEDIR.z);
    COLOR = texture(source_panorama, eyedir).rgb * exposure;
}
```

---

## Custom post-processing

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/custom_postprocessing.html

**Contents:**
- Custom post-processing
- Introduction
- Single pass post-processing
- Multi-pass post-processing
- User-contributed notes

Godot provides many post-processing effects out of the box, including Bloom, DOF, and SSAO, which are described in Environment and post-processing. However, advanced use cases may require custom effects. This article explains how to write your own custom effects.

The easiest way to implement a custom post-processing shader is to use Godot's built-in ability to read from the screen texture. If you're not familiar with this, you should read the Screen Reading Shaders Tutorial first.

Post-processing effects are shaders applied to a frame after Godot has rendered it. To apply a shader to a frame, create a CanvasLayer, and give it a ColorRect. Assign a new ShaderMaterial to the newly created ColorRect, and set the ColorRect's anchor preset to Full Rect:

Setting the anchor preset to Full Rect on the ColorRect node

Your scene tree will look something like this:

Another more efficient method is to use a BackBufferCopy to copy a region of the screen to a buffer and to access it in a shader script through a sampler2D using hint_screen_texture.

As of the time of writing, Godot does not support rendering to multiple buffers at the same time. Your post-processing shader will not have access to other render passes and buffers not exposed by Godot (such as depth or normal/roughness). You only have access to the rendered frame and buffers exposed by Godot as samplers.

For this demo, we will use this Sprite of a sheep.

Assign a new Shader to the ColorRect's ShaderMaterial. You can access the frame's texture and UV with a sampler2D using hint_screen_texture and the built-in SCREEN_UV uniforms.

Copy the following code to your shader. The code below is a hex pixelization shader by arlez80,

The sheep will look something like this:

Some post-processing effects like blurs are resource intensive. You can make them run a lot faster if you break them down in multiple passes. In a multipass material, each pass takes the result from the previous pass as an input and processes it.

To produce a multi-pass post-processing shader, you stack CanvasLayer and ColorRect nodes. In the example above, you use a CanvasLayer object to render a shader using the frame on the layer below. Apart from the node structure, the steps are the same as with the single-pass post-processing shader.

Your scene tree will look something like this:

As an example, you could write a full screen Gaussian blur effect by attaching the following pieces of code to each of the ColorRect nodes. The order in which you apply the shaders depends on the position of the CanvasLayer in the scene tree, higher means sooner. For this blur shader, the order does not matter.

Using the above code, you should end up with a full screen blur effect like below.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (sql):
```sql
shader_type canvas_item;

uniform vec2 size = vec2(32.0, 28.0);
// If you intend to read from mipmaps with `textureLod()` LOD values greater than `0.0`,
// use `filter_nearest_mipmap` instead. This shader doesn't require it.
uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

void fragment() {
        vec2 norm_size = size * SCREEN_PIXEL_SIZE;
        bool less_than_half = mod(SCREEN_UV.y / 2.0, norm_size.y) / norm_size.y < 0.5;
        vec2 uv = SCREEN_UV + vec2(norm_size.x * 0.5 * float(less_than_half), 0.0);
        vec2 center_uv = floor(uv / norm_size) * norm_size;
        vec2 norm_uv = mod(uv, norm_size) / norm_size;
        center_uv += mix(vec2(0.0, 0.0),
                         mix(mix(vec2(norm_size.x, -norm_size.y),
                                 vec2(0.0, -norm_size.y),
                                 float(norm_uv.x < 0.5)),
                             mix(vec2(0.0, -norm_size.y),
                                 vec2(-norm_size.x, -norm_size.y),
                                 float(norm_uv.x < 0.5)),
                             float(less_than_half)),
                         float(norm_uv.y < 0.3333333) * float(norm_uv.y / 0.3333333 < (abs(norm_uv.x - 0.5) * 2.0)));

        COLOR = textureLod(screen_texture, center_uv, 0.0);
}
```

Example 2 (cpp):
```cpp
shader_type canvas_item;

uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

// Blurs the screen in the X-direction.
void fragment() {
    vec3 col = texture(screen_texture, SCREEN_UV).xyz * 0.16;
    col += texture(screen_texture, SCREEN_UV + vec2(SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.15;
    col += texture(screen_texture, SCREEN_UV + vec2(-SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.15;
    col += texture(screen_texture, SCREEN_UV + vec2(2.0 * SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.12;
    col += texture(screen_texture, SCREEN_UV + vec2(2.0 * -SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.12;
    col += texture(screen_texture, SCREEN_UV + vec2(3.0 * SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.09;
    col += texture(screen_texture, SCREEN_UV + vec2(3.0 * -SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.09;
    col += texture(screen_texture, SCREEN_UV + vec2(4.0 * SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.05;
    col += texture(screen_texture, SCREEN_UV + vec2(4.0 * -SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.05;
    COLOR.xyz = col;
}
```

Example 3 (cpp):
```cpp
shader_type canvas_item;

uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

// Blurs the screen in the Y-direction.
void fragment() {
    vec3 col = texture(screen_texture, SCREEN_UV).xyz * 0.16;
    col += texture(screen_texture, SCREEN_UV + vec2(0.0, SCREEN_PIXEL_SIZE.y)).xyz * 0.15;
    col += texture(screen_texture, SCREEN_UV + vec2(0.0, -SCREEN_PIXEL_SIZE.y)).xyz * 0.15;
    col += texture(screen_texture, SCREEN_UV + vec2(0.0, 2.0 * SCREEN_PIXEL_SIZE.y)).xyz * 0.12;
    col += texture(screen_texture, SCREEN_UV + vec2(0.0, 2.0 * -SCREEN_PIXEL_SIZE.y)).xyz * 0.12;
    col += texture(screen_texture, SCREEN_UV + vec2(0.0, 3.0 * SCREEN_PIXEL_SIZE.y)).xyz * 0.09;
    col += texture(screen_texture, SCREEN_UV + vec2(0.0, 3.0 * -SCREEN_PIXEL_SIZE.y)).xyz * 0.09;
    col += texture(screen_texture, SCREEN_UV + vec2(0.0, 4.0 * SCREEN_PIXEL_SIZE.y)).xyz * 0.05;
    col += texture(screen_texture, SCREEN_UV + vec2(0.0, 4.0 * -SCREEN_PIXEL_SIZE.y)).xyz * 0.05;
    COLOR.xyz = col;
}
```

---

## Environment

**URL:** https://docs.godotengine.org/en/stable/classes/class_environment.html

**Contents:**
- Environment
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Resource for environment nodes (like WorldEnvironment) that define multiple rendering options.

Resource for environment nodes (like WorldEnvironment) that define multiple environment operations (such as background Sky or Color, ambient light, fog, depth-of-field...). These parameters affect the final render of the scene. The order of these operations is:

Tonemap (Auto Exposure)

Environment and post-processing

High dynamic range lighting

3D Material Testers Demo

Third Person Shooter (TPS) Demo

adjustment_brightness

adjustment_color_correction

adjustment_saturation

ambient_light_sky_contribution

background_camera_feed_id

background_canvas_max_layer

background_energy_multiplier

fog_aerial_perspective

Color(0.518, 0.553, 0.608, 1)

glow_hdr_luminance_cap

reflected_light_source

sdfgi_bounce_feedback

sdfgi_cascade0_distance

ssao_ao_channel_affect

ssil_normal_rejection

volumetric_fog_albedo

volumetric_fog_ambient_inject

volumetric_fog_anisotropy

volumetric_fog_density

volumetric_fog_detail_spread

volumetric_fog_emission

volumetric_fog_emission_energy

volumetric_fog_enabled

volumetric_fog_gi_inject

volumetric_fog_length

volumetric_fog_sky_affect

volumetric_fog_temporal_reprojection_amount

volumetric_fog_temporal_reprojection_enabled

get_glow_level(idx: int) const

set_glow_level(idx: int, intensity: float)

BGMode BG_CLEAR_COLOR = 0

Clears the background using the clear color defined in ProjectSettings.rendering/environment/defaults/default_clear_color.

Clears the background using a custom clear color.

Displays a user-defined sky in the background.

Displays a CanvasLayer in the background.

Keeps on screen every pixel drawn in the background. This is the fastest background mode, but it can only be safely used in fully-interior scenes (no visible sky or sky reflections). If enabled in a scene where the background is visible, "ghost trail" artifacts will be visible when moving the camera.

BGMode BG_CAMERA_FEED = 5

Displays a camera feed in the background.

Represents the size of the BGMode enum.

enum AmbientSource: 🔗

AmbientSource AMBIENT_SOURCE_BG = 0

Gather ambient light from whichever source is specified as the background.

AmbientSource AMBIENT_SOURCE_DISABLED = 1

Disable ambient light. This provides a slight performance boost over AMBIENT_SOURCE_SKY.

AmbientSource AMBIENT_SOURCE_COLOR = 2

Specify a specific Color for ambient light. This provides a slight performance boost over AMBIENT_SOURCE_SKY.

AmbientSource AMBIENT_SOURCE_SKY = 3

Gather ambient light from the Sky regardless of what the background is.

enum ReflectionSource: 🔗

ReflectionSource REFLECTION_SOURCE_BG = 0

Use the background for reflections.

ReflectionSource REFLECTION_SOURCE_DISABLED = 1

Disable reflections. This provides a slight performance boost over other options.

ReflectionSource REFLECTION_SOURCE_SKY = 2

Use the Sky for reflections regardless of what the background is.

ToneMapper TONE_MAPPER_LINEAR = 0

Does not modify color data, resulting in a linear tonemapping curve which unnaturally clips bright values, causing bright lighting to look blown out. The simplest and fastest tonemapper.

ToneMapper TONE_MAPPER_REINHARDT = 1

A simple tonemapping curve that rolls off bright values to prevent clipping. This results in an image that can appear dull and low contrast. Slower than TONE_MAPPER_LINEAR.

Note: When tonemap_white is left at the default value of 1.0, TONE_MAPPER_REINHARDT produces an identical image to TONE_MAPPER_LINEAR.

ToneMapper TONE_MAPPER_FILMIC = 2

Uses a film-like tonemapping curve to prevent clipping of bright values and provide better contrast than TONE_MAPPER_REINHARDT. Slightly slower than TONE_MAPPER_REINHARDT.

ToneMapper TONE_MAPPER_ACES = 3

Uses a high-contrast film-like tonemapping curve and desaturates bright values for a more realistic appearance. Slightly slower than TONE_MAPPER_FILMIC.

Note: This tonemapping operator is called "ACES Fitted" in Godot 3.x.

ToneMapper TONE_MAPPER_AGX = 4

Uses a film-like tonemapping curve and desaturates bright values for a more realistic appearance. Better than other tonemappers at maintaining the hue of colors as they become brighter. The slowest tonemapping option.

Note: tonemap_white is fixed at a value of 16.29, which makes TONE_MAPPER_AGX unsuitable for use with the Mobile rendering method.

enum GlowBlendMode: 🔗

GlowBlendMode GLOW_BLEND_MODE_ADDITIVE = 0

Additive glow blending mode. Mostly used for particles, glows (bloom), lens flare, bright sources.

GlowBlendMode GLOW_BLEND_MODE_SCREEN = 1

Screen glow blending mode. Increases brightness, used frequently with bloom.

GlowBlendMode GLOW_BLEND_MODE_SOFTLIGHT = 2

Soft light glow blending mode. Modifies contrast, exposes shadows and highlights (vivid bloom).

GlowBlendMode GLOW_BLEND_MODE_REPLACE = 3

Replace glow blending mode. Replaces all pixels' color by the glow value. This can be used to simulate a full-screen blur effect by tweaking the glow parameters to match the original image's brightness.

GlowBlendMode GLOW_BLEND_MODE_MIX = 4

Mixes the glow with the underlying color to avoid increasing brightness as much while still maintaining a glow effect.

FogMode FOG_MODE_EXPONENTIAL = 0

Use a physically-based fog model defined primarily by fog density.

FogMode FOG_MODE_DEPTH = 1

Use a simple fog model defined by start and end positions and a custom curve. While not physically accurate, this model can be useful when you need more artistic control.

SDFGIYScale SDFGI_Y_SCALE_50_PERCENT = 0

Use 50% scale for SDFGI on the Y (vertical) axis. SDFGI cells will be twice as short as they are wide. This allows providing increased GI detail and reduced light leaking with thin floors and ceilings. This is usually the best choice for scenes that don't feature much verticality.

SDFGIYScale SDFGI_Y_SCALE_75_PERCENT = 1

Use 75% scale for SDFGI on the Y (vertical) axis. This is a balance between the 50% and 100% SDFGI Y scales.

SDFGIYScale SDFGI_Y_SCALE_100_PERCENT = 2

Use 100% scale for SDFGI on the Y (vertical) axis. SDFGI cells will be as tall as they are wide. This is usually the best choice for highly vertical scenes. The downside is that light leaking may become more noticeable with thin floors and ceilings.

float adjustment_brightness = 1.0 🔗

void set_adjustment_brightness(value: float)

float get_adjustment_brightness()

The global brightness value of the rendered scene. Effective only if adjustment_enabled is true.

Texture adjustment_color_correction 🔗

void set_adjustment_color_correction(value: Texture)

Texture get_adjustment_color_correction()

The Texture2D or Texture3D lookup table (LUT) to use for the built-in post-process color grading. Can use a GradientTexture1D for a 1-dimensional LUT, or a Texture3D for a more complex LUT. Effective only if adjustment_enabled is true.

float adjustment_contrast = 1.0 🔗

void set_adjustment_contrast(value: float)

float get_adjustment_contrast()

The global contrast value of the rendered scene (default value is 1). Effective only if adjustment_enabled is true.

bool adjustment_enabled = false 🔗

void set_adjustment_enabled(value: bool)

bool is_adjustment_enabled()

If true, enables the adjustment_* properties provided by this resource. If false, modifications to the adjustment_* properties will have no effect on the rendered scene.

float adjustment_saturation = 1.0 🔗

void set_adjustment_saturation(value: float)

float get_adjustment_saturation()

The global color saturation value of the rendered scene (default value is 1). Effective only if adjustment_enabled is true.

Color ambient_light_color = Color(0, 0, 0, 1) 🔗

void set_ambient_light_color(value: Color)

Color get_ambient_light_color()

The ambient light's Color. Only effective if ambient_light_sky_contribution is lower than 1.0 (exclusive).

float ambient_light_energy = 1.0 🔗

void set_ambient_light_energy(value: float)

float get_ambient_light_energy()

The ambient light's energy. The higher the value, the stronger the light. Only effective if ambient_light_sky_contribution is lower than 1.0 (exclusive).

float ambient_light_sky_contribution = 1.0 🔗

void set_ambient_light_sky_contribution(value: float)

float get_ambient_light_sky_contribution()

Defines the amount of light that the sky brings on the scene. A value of 0.0 means that the sky's light emission has no effect on the scene illumination, thus all ambient illumination is provided by the ambient light. On the contrary, a value of 1.0 means that all the light that affects the scene is provided by the sky, thus the ambient light parameter has no effect on the scene.

Note: ambient_light_sky_contribution is internally clamped between 0.0 and 1.0 (inclusive).

AmbientSource ambient_light_source = 0 🔗

void set_ambient_source(value: AmbientSource)

AmbientSource get_ambient_source()

The ambient light source to use for rendering materials and global illumination.

int background_camera_feed_id = 1 🔗

void set_camera_feed_id(value: int)

int get_camera_feed_id()

The ID of the camera feed to show in the background.

int background_canvas_max_layer = 0 🔗

void set_canvas_max_layer(value: int)

int get_canvas_max_layer()

The maximum layer ID to display. Only effective when using the BG_CANVAS background mode.

Color background_color = Color(0, 0, 0, 1) 🔗

void set_bg_color(value: Color)

The Color displayed for clear areas of the scene. Only effective when using the BG_COLOR background mode.

float background_energy_multiplier = 1.0 🔗

void set_bg_energy_multiplier(value: float)

float get_bg_energy_multiplier()

Multiplier for background energy. Increase to make background brighter, decrease to make background dimmer.

float background_intensity = 30000.0 🔗

void set_bg_intensity(value: float)

float get_bg_intensity()

Luminance of background measured in nits (candela per square meter). Only used when ProjectSettings.rendering/lights_and_shadows/use_physical_light_units is enabled. The default value is roughly equivalent to the sky at midday.

BGMode background_mode = 0 🔗

void set_background(value: BGMode)

BGMode get_background()

float fog_aerial_perspective = 0.0 🔗

void set_fog_aerial_perspective(value: float)

float get_fog_aerial_perspective()

If set above 0.0 (exclusive), blends between the fog's color and the color of the background Sky, as read from the radiance cubemap. This has a small performance cost when set above 0.0. Must have background_mode set to BG_SKY.

This is useful to simulate aerial perspective in large scenes with low density fog. However, it is not very useful for high-density fog, as the sky will shine through. When set to 1.0, the fog color comes completely from the Sky. If set to 0.0, aerial perspective is disabled.

Notice that this does not sample the Sky directly, but rather the radiance cubemap. The cubemap is sampled at a mipmap level depending on the depth of the rendered pixel; the farther away, the higher the resolution of the sampled mipmap. This results in the actual color being a blurred version of the sky, with more blur closer to the camera. The highest mipmap resolution is used at a depth of Camera3D.far.

float fog_density = 0.01 🔗

void set_fog_density(value: float)

float get_fog_density()

The fog density to be used. This is demonstrated in different ways depending on the fog_mode mode chosen:

Exponential Fog Mode: Higher values result in denser fog. The fog rendering is exponential like in real life.

Depth Fog mode: The maximum intensity of the deep fog, effect will appear in the distance (relative to the camera). At 1.0 the fog will fully obscure the scene, at 0.0 the fog will not be visible.

float fog_depth_begin = 10.0 🔗

void set_fog_depth_begin(value: float)

float get_fog_depth_begin()

The fog's depth starting distance from the camera. Only available when fog_mode is set to FOG_MODE_DEPTH.

float fog_depth_curve = 1.0 🔗

void set_fog_depth_curve(value: float)

float get_fog_depth_curve()

The fog depth's intensity curve. A number of presets are available in the Inspector by right-clicking the curve. Only available when fog_mode is set to FOG_MODE_DEPTH.

float fog_depth_end = 100.0 🔗

void set_fog_depth_end(value: float)

float get_fog_depth_end()

The fog's depth end distance from the camera. If this value is set to 0, it will be equal to the current camera's Camera3D.far value. Only available when fog_mode is set to FOG_MODE_DEPTH.

bool fog_enabled = false 🔗

void set_fog_enabled(value: bool)

bool is_fog_enabled()

If true, fog effects are enabled.

float fog_height = 0.0 🔗

void set_fog_height(value: float)

float get_fog_height()

The height at which the height fog effect begins.

float fog_height_density = 0.0 🔗

void set_fog_height_density(value: float)

float get_fog_height_density()

The density used to increase fog as height decreases. To make fog increase as height increases, use a negative value.

Color fog_light_color = Color(0.518, 0.553, 0.608, 1) 🔗

void set_fog_light_color(value: Color)

Color get_fog_light_color()

float fog_light_energy = 1.0 🔗

void set_fog_light_energy(value: float)

float get_fog_light_energy()

The fog's brightness. Higher values result in brighter fog.

FogMode fog_mode = 0 🔗

void set_fog_mode(value: FogMode)

FogMode get_fog_mode()

float fog_sky_affect = 1.0 🔗

void set_fog_sky_affect(value: float)

float get_fog_sky_affect()

The factor to use when affecting the sky with non-volumetric fog. 1.0 means that fog can fully obscure the sky. Lower values reduce the impact of fog on sky rendering, with 0.0 not affecting sky rendering at all.

Note: fog_sky_affect has no visual effect if fog_aerial_perspective is 1.0.

float fog_sun_scatter = 0.0 🔗

void set_fog_sun_scatter(value: float)

float get_fog_sun_scatter()

If set above 0.0, renders the scene's directional light(s) in the fog color depending on the view angle. This can be used to give the impression that the sun is "piercing" through the fog.

GlowBlendMode glow_blend_mode = 2 🔗

void set_glow_blend_mode(value: GlowBlendMode)

GlowBlendMode get_glow_blend_mode()

The glow blending mode.

Note: glow_blend_mode has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

float glow_bloom = 0.0 🔗

void set_glow_bloom(value: float)

float get_glow_bloom()

The bloom's intensity. If set to a value higher than 0, this will make glow visible in areas darker than the glow_hdr_threshold.

bool glow_enabled = false 🔗

void set_glow_enabled(value: bool)

bool is_glow_enabled()

If true, the glow effect is enabled. This simulates real world eye/camera behavior where bright pixels bleed onto surrounding pixels.

Note: When using the Mobile rendering method, glow looks different due to the lower dynamic range available in the Mobile rendering method.

Note: When using the Compatibility rendering method, glow uses a different implementation with some properties being unavailable and hidden from the inspector: glow_levels/*, glow_normalized, glow_strength, glow_blend_mode, glow_mix, glow_map, and glow_map_strength. This implementation is optimized to run on low-end devices and is less flexible as a result.

float glow_hdr_luminance_cap = 12.0 🔗

void set_glow_hdr_luminance_cap(value: float)

float get_glow_hdr_luminance_cap()

The higher threshold of the HDR glow. Areas brighter than this threshold will be clamped for the purposes of the glow effect.

float glow_hdr_scale = 2.0 🔗

void set_glow_hdr_bleed_scale(value: float)

float get_glow_hdr_bleed_scale()

The bleed scale of the HDR glow.

float glow_hdr_threshold = 1.0 🔗

void set_glow_hdr_bleed_threshold(value: float)

float get_glow_hdr_bleed_threshold()

The lower threshold of the HDR glow. When using the Mobile rendering method (which only supports a lower dynamic range up to 2.0), this may need to be below 1.0 for glow to be visible. A value of 0.9 works well in this case. This value also needs to be decreased below 1.0 when using glow in 2D, as 2D rendering is performed in SDR.

float glow_intensity = 0.8 🔗

void set_glow_intensity(value: float)

float get_glow_intensity()

The overall brightness multiplier of the glow effect. When using the Mobile rendering method (which only supports a lower dynamic range up to 2.0), this should be increased to 1.5 to compensate.

float glow_levels/1 = 0.0 🔗

void set_glow_level(idx: int, intensity: float)

float get_glow_level(idx: int) const

The intensity of the 1st level of glow. This is the most "local" level (least blurry).

Note: glow_levels/1 has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

float glow_levels/2 = 0.0 🔗

void set_glow_level(idx: int, intensity: float)

float get_glow_level(idx: int) const

The intensity of the 2nd level of glow.

Note: glow_levels/2 has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

float glow_levels/3 = 1.0 🔗

void set_glow_level(idx: int, intensity: float)

float get_glow_level(idx: int) const

The intensity of the 3rd level of glow.

Note: glow_levels/3 has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

float glow_levels/4 = 0.0 🔗

void set_glow_level(idx: int, intensity: float)

float get_glow_level(idx: int) const

The intensity of the 4th level of glow.

Note: glow_levels/4 has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

float glow_levels/5 = 1.0 🔗

void set_glow_level(idx: int, intensity: float)

float get_glow_level(idx: int) const

The intensity of the 5th level of glow.

Note: glow_levels/5 has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

float glow_levels/6 = 0.0 🔗

void set_glow_level(idx: int, intensity: float)

float get_glow_level(idx: int) const

The intensity of the 6th level of glow.

Note: glow_levels/6 has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

float glow_levels/7 = 0.0 🔗

void set_glow_level(idx: int, intensity: float)

float get_glow_level(idx: int) const

The intensity of the 7th level of glow. This is the most "global" level (blurriest).

Note: glow_levels/7 has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

void set_glow_map(value: Texture)

Texture get_glow_map()

The texture that should be used as a glow map to multiply the resulting glow color according to glow_map_strength. This can be used to create a "lens dirt" effect. The texture's RGB color channels are used for modulation, but the alpha channel is ignored.

Note: The texture will be stretched to fit the screen. Therefore, it's recommended to use a texture with an aspect ratio that matches your project's base aspect ratio (typically 16:9).

Note: glow_map has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

float glow_map_strength = 0.8 🔗

void set_glow_map_strength(value: float)

float get_glow_map_strength()

How strong of an influence the glow_map should have on the overall glow effect. A strength of 0.0 means the glow map has no influence, while a strength of 1.0 means the glow map has full influence.

Note: If the glow map has black areas, a value of 1.0 can also turn off the glow effect entirely in specific areas of the screen.

Note: glow_map_strength has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

float glow_mix = 0.05 🔗

void set_glow_mix(value: float)

When using the GLOW_BLEND_MODE_MIX glow_blend_mode, this controls how much the source image is blended with the glow layer. A value of 0.0 makes the glow rendering invisible, while a value of 1.0 is equivalent to GLOW_BLEND_MODE_REPLACE.

Note: glow_mix has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

bool glow_normalized = false 🔗

void set_glow_normalized(value: bool)

bool is_glow_normalized()

If true, glow levels will be normalized so that summed together their intensities equal 1.0.

Note: glow_normalized has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

float glow_strength = 1.0 🔗

void set_glow_strength(value: float)

float get_glow_strength()

The strength of the glow effect. This applies as the glow is blurred across the screen and increases the distance and intensity of the blur. When using the Mobile rendering method, this should be increased to compensate for the lower dynamic range.

Note: glow_strength has no effect when using the Compatibility rendering method, due to this rendering method using a simpler glow implementation optimized for low-end devices.

ReflectionSource reflected_light_source = 0 🔗

void set_reflection_source(value: ReflectionSource)

ReflectionSource get_reflection_source()

The reflected (specular) light source.

float sdfgi_bounce_feedback = 0.5 🔗

void set_sdfgi_bounce_feedback(value: float)

float get_sdfgi_bounce_feedback()

The energy multiplier applied to light every time it bounces from a surface when using SDFGI. Values greater than 0.0 will simulate multiple bounces, resulting in a more realistic appearance. Increasing sdfgi_bounce_feedback generally has no performance impact. See also sdfgi_energy.

Note: Values greater than 0.5 can cause infinite feedback loops and should be avoided in scenes with bright materials.

Note: If sdfgi_bounce_feedback is 0.0, indirect lighting will not be represented in reflections as light will only bounce one time.

float sdfgi_cascade0_distance = 12.8 🔗

void set_sdfgi_cascade0_distance(value: float)

float get_sdfgi_cascade0_distance()

Note: This property is linked to sdfgi_min_cell_size and sdfgi_max_distance. Changing its value will automatically change those properties as well.

int sdfgi_cascades = 4 🔗

void set_sdfgi_cascades(value: int)

int get_sdfgi_cascades()

The number of cascades to use for SDFGI (between 1 and 8). A higher number of cascades allows displaying SDFGI further away while preserving detail up close, at the cost of performance. When using SDFGI on small-scale levels, sdfgi_cascades can often be decreased between 1 and 4 to improve performance.

bool sdfgi_enabled = false 🔗

void set_sdfgi_enabled(value: bool)

bool is_sdfgi_enabled()

If true, enables signed distance field global illumination for meshes that have their GeometryInstance3D.gi_mode set to GeometryInstance3D.GI_MODE_STATIC. SDFGI is a real-time global illumination technique that works well with procedurally generated and user-built levels, including in situations where geometry is created during gameplay. The signed distance field is automatically generated around the camera as it moves. Dynamic lights are supported, but dynamic occluders and emissive surfaces are not.

Note: SDFGI is only supported in the Forward+ rendering method, not Mobile or Compatibility.

Performance: SDFGI is relatively demanding on the GPU and is not suited to low-end hardware such as integrated graphics (consider LightmapGI instead). To improve SDFGI performance, enable ProjectSettings.rendering/global_illumination/gi/use_half_resolution in the Project Settings.

Note: Meshes should have sufficiently thick walls to avoid light leaks (avoid one-sided walls). For interior levels, enclose your level geometry in a sufficiently large box and bridge the loops to close the mesh.

float sdfgi_energy = 1.0 🔗

void set_sdfgi_energy(value: float)

float get_sdfgi_energy()

The energy multiplier to use for SDFGI. Higher values will result in brighter indirect lighting and reflections. See also sdfgi_bounce_feedback.

float sdfgi_max_distance = 204.8 🔗

void set_sdfgi_max_distance(value: float)

float get_sdfgi_max_distance()

The maximum distance at which SDFGI is visible. Beyond this distance, environment lighting or other sources of GI such as ReflectionProbe will be used as a fallback.

Note: This property is linked to sdfgi_min_cell_size and sdfgi_cascade0_distance. Changing its value will automatically change those properties as well.

float sdfgi_min_cell_size = 0.2 🔗

void set_sdfgi_min_cell_size(value: float)

float get_sdfgi_min_cell_size()

The cell size to use for the closest SDFGI cascade (in 3D units). Lower values allow SDFGI to be more precise up close, at the cost of making SDFGI updates more demanding. This can cause stuttering when the camera moves fast. Higher values allow SDFGI to cover more ground, while also reducing the performance impact of SDFGI updates.

Note: This property is linked to sdfgi_max_distance and sdfgi_cascade0_distance. Changing its value will automatically change those properties as well.

float sdfgi_normal_bias = 1.1 🔗

void set_sdfgi_normal_bias(value: float)

float get_sdfgi_normal_bias()

The normal bias to use for SDFGI probes. Increasing this value can reduce visible streaking artifacts on sloped surfaces, at the cost of increased light leaking.

float sdfgi_probe_bias = 1.1 🔗

void set_sdfgi_probe_bias(value: float)

float get_sdfgi_probe_bias()

The constant bias to use for SDFGI probes. Increasing this value can reduce visible streaking artifacts on sloped surfaces, at the cost of increased light leaking.

bool sdfgi_read_sky_light = true 🔗

void set_sdfgi_read_sky_light(value: bool)

bool is_sdfgi_reading_sky_light()

If true, SDFGI takes the environment lighting into account. This should be set to false for interior scenes.

bool sdfgi_use_occlusion = false 🔗

void set_sdfgi_use_occlusion(value: bool)

bool is_sdfgi_using_occlusion()

If true, SDFGI uses an occlusion detection approach to reduce light leaking. Occlusion may however introduce dark blotches in certain spots, which may be undesired in mostly outdoor scenes. sdfgi_use_occlusion has a performance impact and should only be enabled when needed.

SDFGIYScale sdfgi_y_scale = 1 🔗

void set_sdfgi_y_scale(value: SDFGIYScale)

SDFGIYScale get_sdfgi_y_scale()

The Y scale to use for SDFGI cells. Lower values will result in SDFGI cells being packed together more closely on the Y axis. This is used to balance between quality and covering a lot of vertical ground. sdfgi_y_scale should be set depending on how vertical your scene is (and how fast your camera may move on the Y axis).

void set_sky(value: Sky)

The Sky resource used for this Environment.

float sky_custom_fov = 0.0 🔗

void set_sky_custom_fov(value: float)

float get_sky_custom_fov()

If set to a value greater than 0.0, overrides the field of view to use for sky rendering. If set to 0.0, the same FOV as the current Camera3D is used for sky rendering.

Vector3 sky_rotation = Vector3(0, 0, 0) 🔗

void set_sky_rotation(value: Vector3)

Vector3 get_sky_rotation()

The rotation to use for sky rendering.

float ssao_ao_channel_affect = 0.0 🔗

void set_ssao_ao_channel_affect(value: float)

float get_ssao_ao_channel_affect()

The screen-space ambient occlusion intensity on materials that have an AO texture defined. Values higher than 0 will make the SSAO effect visible in areas darkened by AO textures.

float ssao_detail = 0.5 🔗

void set_ssao_detail(value: float)

float get_ssao_detail()

Sets the strength of the additional level of detail for the screen-space ambient occlusion effect. A high value makes the detail pass more prominent, but it may contribute to aliasing in your final image.

bool ssao_enabled = false 🔗

void set_ssao_enabled(value: bool)

bool is_ssao_enabled()

If true, the screen-space ambient occlusion effect is enabled. This darkens objects' corners and cavities to simulate ambient light not reaching the entire object as in real life. This works well for small, dynamic objects, but baked lighting or ambient occlusion textures will do a better job at displaying ambient occlusion on large static objects. Godot uses a form of SSAO called Adaptive Screen Space Ambient Occlusion which is itself a form of Horizon Based Ambient Occlusion.

Note: SSAO is only supported in the Forward+ rendering method, not Mobile or Compatibility.

float ssao_horizon = 0.06 🔗

void set_ssao_horizon(value: float)

float get_ssao_horizon()

The threshold for considering whether a given point on a surface is occluded or not represented as an angle from the horizon mapped into the 0.0-1.0 range. A value of 1.0 results in no occlusion.

float ssao_intensity = 2.0 🔗

void set_ssao_intensity(value: float)

float get_ssao_intensity()

The primary screen-space ambient occlusion intensity. Acts as a multiplier for the screen-space ambient occlusion effect. A higher value results in darker occlusion.

float ssao_light_affect = 0.0 🔗

void set_ssao_direct_light_affect(value: float)

float get_ssao_direct_light_affect()

The screen-space ambient occlusion intensity in direct light. In real life, ambient occlusion only applies to indirect light, which means its effects can't be seen in direct light. Values higher than 0 will make the SSAO effect visible in direct light.

float ssao_power = 1.5 🔗

void set_ssao_power(value: float)

float get_ssao_power()

The distribution of occlusion. A higher value results in darker occlusion, similar to ssao_intensity, but with a sharper falloff.

float ssao_radius = 1.0 🔗

void set_ssao_radius(value: float)

float get_ssao_radius()

The distance at which objects can occlude each other when calculating screen-space ambient occlusion. Higher values will result in occlusion over a greater distance at the cost of performance and quality.

float ssao_sharpness = 0.98 🔗

void set_ssao_sharpness(value: float)

float get_ssao_sharpness()

The amount that the screen-space ambient occlusion effect is allowed to blur over the edges of objects. Setting too high will result in aliasing around the edges of objects. Setting too low will make object edges appear blurry.

bool ssil_enabled = false 🔗

void set_ssil_enabled(value: bool)

bool is_ssil_enabled()

If true, the screen-space indirect lighting effect is enabled. Screen space indirect lighting is a form of indirect lighting that allows diffuse light to bounce between nearby objects. Screen-space indirect lighting works very similarly to screen-space ambient occlusion, in that it only affects a limited range. It is intended to be used along with a form of proper global illumination like SDFGI or VoxelGI. Screen-space indirect lighting is not affected by individual light's Light3D.light_indirect_energy.

Note: SSIL is only supported in the Forward+ rendering method, not Mobile or Compatibility.

float ssil_intensity = 1.0 🔗

void set_ssil_intensity(value: float)

float get_ssil_intensity()

The brightness multiplier for the screen-space indirect lighting effect. A higher value will result in brighter light.

float ssil_normal_rejection = 1.0 🔗

void set_ssil_normal_rejection(value: float)

float get_ssil_normal_rejection()

Amount of normal rejection used when calculating screen-space indirect lighting. Normal rejection uses the normal of a given sample point to reject samples that are facing away from the current pixel. Normal rejection is necessary to avoid light leaking when only one side of an object is illuminated. However, normal rejection can be disabled if light leaking is desirable, such as when the scene mostly contains emissive objects that emit light from faces that cannot be seen from the camera.

float ssil_radius = 5.0 🔗

void set_ssil_radius(value: float)

float get_ssil_radius()

The distance that bounced lighting can travel when using the screen space indirect lighting effect. A larger value will result in light bouncing further in a scene, but may result in under-sampling artifacts which look like long spikes surrounding light sources.

float ssil_sharpness = 0.98 🔗

void set_ssil_sharpness(value: float)

float get_ssil_sharpness()

The amount that the screen-space indirect lighting effect is allowed to blur over the edges of objects. Setting too high will result in aliasing around the edges of objects. Setting too low will make object edges appear blurry.

float ssr_depth_tolerance = 0.2 🔗

void set_ssr_depth_tolerance(value: float)

float get_ssr_depth_tolerance()

The depth tolerance for screen-space reflections.

bool ssr_enabled = false 🔗

void set_ssr_enabled(value: bool)

bool is_ssr_enabled()

If true, screen-space reflections are enabled. Screen-space reflections are more accurate than reflections from VoxelGIs or ReflectionProbes, but are slower and can't reflect surfaces occluded by others.

Note: SSR is only supported in the Forward+ rendering method, not Mobile or Compatibility.

Note: SSR is not supported on viewports that have a transparent background (where Viewport.transparent_bg is true).

float ssr_fade_in = 0.15 🔗

void set_ssr_fade_in(value: float)

float get_ssr_fade_in()

The fade-in distance for screen-space reflections. Affects the area from the reflected material to the screen-space reflection. Only positive values are valid (negative values will be clamped to 0.0).

float ssr_fade_out = 2.0 🔗

void set_ssr_fade_out(value: float)

float get_ssr_fade_out()

The fade-out distance for screen-space reflections. Affects the area from the screen-space reflection to the "global" reflection. Only positive values are valid (negative values will be clamped to 0.0).

int ssr_max_steps = 64 🔗

void set_ssr_max_steps(value: int)

int get_ssr_max_steps()

The maximum number of steps for screen-space reflections. Higher values are slower.

float tonemap_exposure = 1.0 🔗

void set_tonemap_exposure(value: float)

float get_tonemap_exposure()

Adjusts the brightness of values before they are provided to the tonemapper. Higher tonemap_exposure values result in a brighter image. See also tonemap_white.

Note: Values provided to the tonemapper will also be multiplied by 2.0 and 1.8 for TONE_MAPPER_FILMIC and TONE_MAPPER_ACES respectively to produce a similar apparent brightness as TONE_MAPPER_LINEAR.

ToneMapper tonemap_mode = 0 🔗

void set_tonemapper(value: ToneMapper)

ToneMapper get_tonemapper()

The tonemapping mode to use. Tonemapping is the process that "converts" HDR values to be suitable for rendering on an LDR display. (Godot doesn't support rendering on HDR displays yet.)

float tonemap_white = 1.0 🔗

void set_tonemap_white(value: float)

float get_tonemap_white()

The white reference value for tonemapping, which indicates where bright white is located in the scale of values provided to the tonemapper. For photorealistic lighting, recommended values are between 6.0 and 8.0. Higher values result in less blown out highlights, but may make the scene appear lower contrast. See also tonemap_exposure.

Note: tonemap_white is ignored when using TONE_MAPPER_LINEAR or TONE_MAPPER_AGX.

Color volumetric_fog_albedo = Color(1, 1, 1, 1) 🔗

void set_volumetric_fog_albedo(value: Color)

Color get_volumetric_fog_albedo()

The Color of the volumetric fog when interacting with lights. Mist and fog have an albedo close to Color(1, 1, 1, 1) while smoke has a darker albedo.

float volumetric_fog_ambient_inject = 0.0 🔗

void set_volumetric_fog_ambient_inject(value: float)

float get_volumetric_fog_ambient_inject()

Scales the strength of ambient light used in the volumetric fog. A value of 0.0 means that ambient light will not impact the volumetric fog. volumetric_fog_ambient_inject has a small performance cost when set above 0.0.

Note: This has no visible effect if volumetric_fog_density is 0.0 or if volumetric_fog_albedo is a fully black color.

float volumetric_fog_anisotropy = 0.2 🔗

void set_volumetric_fog_anisotropy(value: float)

float get_volumetric_fog_anisotropy()

The direction of scattered light as it goes through the volumetric fog. A value close to 1.0 means almost all light is scattered forward. A value close to 0.0 means light is scattered equally in all directions. A value close to -1.0 means light is scattered mostly backward. Fog and mist scatter light slightly forward, while smoke scatters light equally in all directions.

float volumetric_fog_density = 0.05 🔗

void set_volumetric_fog_density(value: float)

float get_volumetric_fog_density()

The base exponential density of the volumetric fog. Set this to the lowest density you want to have globally. FogVolumes can be used to add to or subtract from this density in specific areas. Fog rendering is exponential as in real life.

A value of 0.0 disables global volumetric fog while allowing FogVolumes to display volumetric fog in specific areas.

To make volumetric fog work as a volumetric lighting solution, set volumetric_fog_density to the lowest non-zero value (0.0001) then increase lights' Light3D.light_volumetric_fog_energy to values between 10000 and 100000 to compensate for the very low density.

float volumetric_fog_detail_spread = 2.0 🔗

void set_volumetric_fog_detail_spread(value: float)

float get_volumetric_fog_detail_spread()

The distribution of size down the length of the froxel buffer. A higher value compresses the froxels closer to the camera and places more detail closer to the camera.

Color volumetric_fog_emission = Color(0, 0, 0, 1) 🔗

void set_volumetric_fog_emission(value: Color)

Color get_volumetric_fog_emission()

The emitted light from the volumetric fog. Even with emission, volumetric fog will not cast light onto other surfaces. Emission is useful to establish an ambient color. As the volumetric fog effect uses single-scattering only, fog tends to need a little bit of emission to soften the harsh shadows.

float volumetric_fog_emission_energy = 1.0 🔗

void set_volumetric_fog_emission_energy(value: float)

float get_volumetric_fog_emission_energy()

The brightness of the emitted light from the volumetric fog.

bool volumetric_fog_enabled = false 🔗

void set_volumetric_fog_enabled(value: bool)

bool is_volumetric_fog_enabled()

Enables the volumetric fog effect. Volumetric fog uses a screen-aligned froxel buffer to calculate accurate volumetric scattering in the short to medium range. Volumetric fog interacts with FogVolumes and lights to calculate localized and global fog. Volumetric fog uses a PBR single-scattering model based on extinction, scattering, and emission which it exposes to users as density, albedo, and emission.

Note: Volumetric fog is only supported in the Forward+ rendering method, not Mobile or Compatibility.

float volumetric_fog_gi_inject = 1.0 🔗

void set_volumetric_fog_gi_inject(value: float)

float get_volumetric_fog_gi_inject()

Scales the strength of Global Illumination used in the volumetric fog's albedo color. A value of 0.0 means that Global Illumination will not impact the volumetric fog. volumetric_fog_gi_inject has a small performance cost when set above 0.0.

Note: This has no visible effect if volumetric_fog_density is 0.0 or if volumetric_fog_albedo is a fully black color.

Note: Only VoxelGI and SDFGI (sdfgi_enabled) are taken into account when using volumetric_fog_gi_inject. Global illumination from LightmapGI, ReflectionProbe and SSIL (see ssil_enabled) will be ignored by volumetric fog.

float volumetric_fog_length = 64.0 🔗

void set_volumetric_fog_length(value: float)

float get_volumetric_fog_length()

The distance over which the volumetric fog is computed. Increase to compute fog over a greater range, decrease to add more detail when a long range is not needed. For best quality fog, keep this as low as possible. See also ProjectSettings.rendering/environment/volumetric_fog/volume_depth.

float volumetric_fog_sky_affect = 1.0 🔗

void set_volumetric_fog_sky_affect(value: float)

float get_volumetric_fog_sky_affect()

The factor to use when affecting the sky with volumetric fog. 1.0 means that volumetric fog can fully obscure the sky. Lower values reduce the impact of volumetric fog on sky rendering, with 0.0 not affecting sky rendering at all.

Note: volumetric_fog_sky_affect also affects FogVolumes, even if volumetric_fog_density is 0.0. If you notice FogVolumes are disappearing when looking towards the sky, set volumetric_fog_sky_affect to 1.0.

float volumetric_fog_temporal_reprojection_amount = 0.9 🔗

void set_volumetric_fog_temporal_reprojection_amount(value: float)

float get_volumetric_fog_temporal_reprojection_amount()

The amount by which to blend the last frame with the current frame. A higher number results in smoother volumetric fog, but makes "ghosting" much worse. A lower value reduces ghosting but can result in the per-frame temporal jitter becoming visible.

bool volumetric_fog_temporal_reprojection_enabled = true 🔗

void set_volumetric_fog_temporal_reprojection_enabled(value: bool)

bool is_volumetric_fog_temporal_reprojection_enabled()

Enables temporal reprojection in the volumetric fog. Temporal reprojection blends the current frame's volumetric fog with the last frame's volumetric fog to smooth out jagged edges. The performance cost is minimal; however, it leads to moving FogVolumes and Light3Ds "ghosting" and leaving a trail behind them. When temporal reprojection is enabled, try to avoid moving FogVolumes or Light3Ds too fast. Short-lived dynamic lighting effects should have Light3D.light_volumetric_fog_energy set to 0.0 to avoid ghosting.

float get_glow_level(idx: int) const 🔗

Returns the intensity of the glow level idx.

void set_glow_level(idx: int, intensity: float) 🔗

Sets the intensity of the glow level idx. A value above 0.0 enables the level. Each level relies on the previous level. This means that enabling higher glow levels will slow down the glow effect rendering, even if previous levels aren't enabled.

Please read the User-contributed notes policy before submitting a comment.

---

## Fixing jitter, stutter and input lag

**URL:** https://docs.godotengine.org/en/stable/tutorials/rendering/jitter_stutter.html

**Contents:**
- Fixing jitter, stutter and input lag
- What is jitter, stutter and input lag?
- Distinguishing between jitter and stutter
- Jitter
- Stutter
  - Windows
  - Linux
  - macOS
  - Android
  - iOS

Jitter and stutter are two different alterations to visible motion of objects on screen that may affect a game, even when running at full speed. These effects are mostly visible in games where the world moves at a constant speed in a fixed direction, like runners or platformers.

Input lag is unrelated to jitter and stutter, but is sometimes discussed alongside. Input lag refers to visible on-screen delay when performing actions with the mouse, keyboard, controller or touchscreen. It can be related to game code, engine code or external factors (such as hardware). Input lag is most noticeable in games that use the mouse to aim, such as first-person games. Input lag can't be completely eliminated, but it can be reduced in several ways.

A game running at a normal framerate without exhibiting any effect will appear smooth:

A game exhibiting jitter will shake constantly in a very subtle way:

Finally, a game exhibiting stutter will appear smooth, but appear to stop or roll back a frame every few seconds:

There can be many causes of jitter. The most typical one happens when the game physics frequency (usually 60 Hz) runs at a different resolution than the monitor refresh rate. Check whether your monitor refresh rate is different from 60 Hz.

Sometimes, only some objects appear to jitter (character or background). This happens when they are processed in different time sources (one is processed in the physics step while another is processed in the idle step).

This cause of jitter can be alleviated by enabling physics interpolation in the Project Settings. Physics interpolation will smooth out physics updates by interpolating the transforms of physics objects between physics frames. This way, the visual representation of physics objects will always look smooth no matter the framerate and physics tick rate.

Enabling physics interpolation has some caveats you should be aware of. For example, care should be taken when teleporting objects so that they don't visibly interpolate between the old position and new position when it's not intended. See the Physics Interpolation documentation for details.

Enabling physics interpolation will increase input lag for behavior that depends on the physics tick, such as player movement. In most games, this is generally preferable to jitter, but consider this carefully for games that operate on a fixed framerate (like fighting or rhythm games). This increase in input lag can be compensated by increasing the physics tick rate as described in the Input lag section.

Stutter may happen due to several different reasons. One reason is the game not being able to keep full framerate performance due to a CPU or GPU bottleneck. Solving this is game-specific and will require optimization.

Another common reason for stuttering is shader compilation stutter. This occurs when a shader needs to be compiled when a new material or particle effect is spawned for the first time in a game. This kind of stuttering generally only happens on the first playthrough, or after a graphics driver update when the shader cache is invalidated.

Since Godot 4.4, when using the Forward+ or Mobile renderers, the engine tries to avoid shader compilation stutter using an ubershader approach. For this approach to be most effective, care must be taken when designing scenes and resources so that Godot can gather as much information as possible when the scene/resource is loaded, as opposed as to when it's being drawn for the first time. See Reducing stutter from shader (pipeline) compilations for more information.

However, when using the Compatibility renderer, it is not possible to use this ubershader approach due to technical limitations in OpenGL. Therefore, to avoid shader compilation stutter in the Compatibility renderer, you need to spawn every mesh and visual effect in front of the camera for a single frame when the level is loading. This will ensure the shader is compiled when the level is loaded, as opposed to occurring during gameplay. This can be done behind solid 2D UI (such as a fullscreen ColorRect node) so that it's not visible to the player.

On platforms that support disabling V-Sync, stuttering can be made less noticeable by disabling V-Sync in the project settings. This will however cause tearing to appear, especially on monitors with low refresh rates. If your monitor supports it, consider enabling variable refresh rate (G-Sync/FreeSync) while leaving V-Sync enabled. This allows mitigating some forms of stuttering without introducing tearing. However, it will not help with large stutters, such as the ones caused by shader compilation stutter.

Forcing your graphics card to use the maximum performance profile can also help reduce stuttering, at the cost of increased GPU power draw.

Additionally, stutter may be induced by the underlying operating system. Here is some information regarding stutter on different OSes:

Windows is known to cause stutter in windowed games. This mostly depends on the hardware installed, drivers version and processes running in parallel (e.g. having many browser tabs open may cause stutter in a running game). To avoid this, Godot raises the game priority to "Above Normal". This helps considerably, but may not completely eliminate stutter.

Eliminating this completely requires giving your game full privileges to become "Time Critical", which is not advised. Some games may do it, but it is advised to learn to live with this problem, as it is common for Windows games and most users won't play games windowed (games that are played in a window, e.g. puzzle games, will usually not exhibit this problem anyway).

For fullscreen, Windows gives special priority to the game so stutter is no longer visible and very rare. This is how most games are played.

When using a mouse with a polling rate of 1,000 Hz or more, consider using a fully up-to-date Windows 11 installation which comes with fixes related to high CPU utilization with high polling rate mice. These fixes are not available in Windows 10 and older versions.

Games should use the Exclusive Fullscreen window mode, as opposed to Fullscreen which is designed to prevent Windows from automatically treating the window as if it was exclusive fullscreen.

Fullscreen is meant to be used by GUI applications that want to use per-pixel transparency without a risk of having it disabled by the OS. It achieves this by leaving a 1-pixel line at the bottom of the screen. By contrast, Exclusive Fullscreen uses the actual screen size and allows Windows to reduce jitter and input lag for fullscreen games.

Stutter may be visible on desktop Linux, but this is usually associated with different video drivers and compositors. Some compositors may also trigger this problem (e.g. KWin), so it is advised to try using a different one to rule it out as the cause. Some window managers such as KWin and Xfwm allow you to manually disable compositing, which can improve performance (at the cost of tearing).

There is no workaround for driver or compositor stuttering, other than reporting it as an issue to the driver or compositor developers. Stutter may be more present when playing in windowed mode as opposed to fullscreen, even with compositing disabled.

Feral GameMode can be used to automatically apply optimizations (such as forcing the GPU performance profile) when running specific processes.

Generally, macOS is stutter-free, although recently some bugs were reported when running on fullscreen (this is a macOS bug). If you have a machine exhibiting this behavior, please let us know.

Generally, Android is stutter and jitter-free because the running activity gets all the priority. That said, there may be problematic devices (older Kindle Fire is known to be one). If you see this problem on Android, please let us know.

iOS devices are generally stutter-free, but older devices running newer versions of the operating system may exhibit problems. This is generally unavoidable.

On platforms that support disabling V-Sync, input lag can be made less noticeable by disabling V-Sync in the project settings. This will however cause tearing to appear, especially on monitors with low refresh rates. It's suggested to make V-Sync available as an option for players to toggle.

When using the Forward+ or Mobile rendering methods, another way to reduce visual latency when V-Sync is enabled is to use double-buffered V-Sync instead of the default triple-buffered V-Sync. Since Godot 4.3, this can be achieved by reducing the Display > Window > V-Sync > Swapchain Image Count project setting to 2. The downside of using double buffering is that framerate will be less stable if the display refresh rate can't be reached due to a CPU or GPU bottleneck. For instance, on a 60 Hz display, if the framerate would normally drop to 55 FPS during gameplay with triple buffering, it will have to drop down to 30 FPS momentarily with double buffering (and then go back to 60 FPS when possible). As a result, double-buffered V-Sync is only recommended if you can consistently reach the display refresh rate on the target hardware.

Increasing the number of physics iterations per second can also reduce physics-induced input latency. This is especially noticeable when using physics interpolation (which improves smoothness but increases latency). To do so, set Physics > Common > Physics Ticks Per Second to a value higher than the default 60, or set Engine.physics_ticks_per_second at runtime in a script. Values that are a multiple of the monitor refresh rate (typically 60) work best when physics interpolation is disabled, as they will avoid jitter. This means values such as 120, 180 and 240 are good starting points. As a bonus, higher physics FPSes make tunneling and physics instability issues less likely to occur.

The downside of increasing physics FPS is that CPU usage will increase, which can lead to performance bottlenecks in games that have heavy physics simulation code. This can be alleviated by increasing physics FPS only in situations where low latency is critical, or by letting players adjust physics FPS to match their hardware. However, different physics FPS will lead to different outcomes in physics simulation, even when delta is consistently used in your game logic. This can give certain players an advantage over others. Therefore, allowing the player to change the physics FPS themselves should be avoided for competitive multiplayer games.

Lastly, you can disable input buffering on a per-rendered frame basis by calling Input.set_use_accumulated_input(false) in a script. This will make it so the _input() and _unhandled_input() functions in your scripts are called on every input, rather than accumulating inputs and waiting for a frame to be rendered. Disabling input accumulation will increase CPU usage, so it should be done with caution.

On any Godot project, you can use the --disable-vsync command line argument to forcibly disable V-Sync. Since Godot 4.2, --max-fps <fps> can also be used to set an FPS limit (0 is unlimited). These arguments can be used at the same time.

If your monitor supports it, consider enabling variable refresh rate (G-Sync/FreeSync) while leaving V-Sync enabled, then cap the framerate in the project settings to a slightly lower value than your monitor's maximum refresh rate as per this page. For example, on a 144 Hz monitor, you can set the project's framerate cap to 141. This may be counterintuitive at first, but capping the FPS below the maximum refresh rate range ensures that the OS never has to wait for vertical blanking to finish. This leads to similar input lag as V-Sync disabled with the same framerate cap (usually less than 1 ms greater), but without any tearing.

This can be done by changing the Application > Run > Max FPS project setting or assigning Engine.max_fps at runtime in a script.

On some platforms, you can also opt into a low-latency mode in the graphics driver options (such as the NVIDIA Control Panel on Windows). The Ultra setting will give you the lowest possible latency, at the cost of slightly lower average framerates. Forcing the GPU to use the maximum performance profile can also further reduce input lag, at the cost of higher power consumption (and resulting heat/fan noise).

Finally, make sure your monitor is running at its highest possible refresh rate in the OS' display settings.

Also, ensure that your mouse is configured to use its highest polling rate (typically 1,000 Hz for gaming mice, sometimes more). High USB polling rates can however result in high CPU usage, so 500 Hz may be a safer bet on low-end CPUs. If your mouse offers multiple DPI settings, consider also using the highest possible setting and reducing in-game sensitivity to reduce mouse latency.

On Linux when using X11, disabling compositing in window managers that allow it (such as KWin or Xfwm) can reduce input lag significantly.

If you are reporting a stutter or jitter problem (opening an issue) not caused by any of the above reasons, please specify very clearly all the information possible about device, operating system, driver versions, etc. This may help to better troubleshoot it.

If you are reporting input lag problems, please include a capture made with a high speed camera (such as your phone's slow motion video mode). The capture must have both the screen and the input device visible so that the number of frames between an input and the on-screen result can be counted. Also, make sure to mention your monitor's refresh rate and your input device's polling rate (especially for mice).

Also, make sure to use the correct term (jitter, stutter, input lag) based on the exhibited behavior. This will help understand your issue much faster. Provide a project that can be used to reproduce the issue, and if possible, include a screen capture demonstrating the bug.

Please read the User-contributed notes policy before submitting a comment.

---

## FogMaterial

**URL:** https://docs.godotengine.org/en/stable/classes/class_fogmaterial.html

**Contents:**
- FogMaterial
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Material < Resource < RefCounted < Object

A material that controls how volumetric fog is rendered, to be assigned to a FogVolume.

A Material resource that can be used by FogVolumes to draw volumetric effects.

If you need more advanced effects, use a custom fog shader.

Color albedo = Color(1, 1, 1, 1) 🔗

void set_albedo(value: Color)

The single-scattering Color of the FogVolume. Internally, albedo is converted into single-scattering, which is additively blended with other FogVolumes and the Environment.volumetric_fog_albedo.

float density = 1.0 🔗

void set_density(value: float)

The density of the FogVolume. Denser objects are more opaque, but may suffer from under-sampling artifacts that look like stripes. Negative values can be used to subtract fog from other FogVolumes or global volumetric fog.

Note: Due to limited precision, density values between -0.001 and 0.001 (exclusive) act like 0.0. This does not apply to Environment.volumetric_fog_density.

Texture3D density_texture 🔗

void set_density_texture(value: Texture3D)

Texture3D get_density_texture()

The 3D texture that is used to scale the density of the FogVolume. This can be used to vary fog density within the FogVolume with any kind of static pattern. For animated effects, consider using a custom fog shader.

float edge_fade = 0.1 🔗

void set_edge_fade(value: float)

float get_edge_fade()

The hardness of the edges of the FogVolume. A higher value will result in softer edges, while a lower value will result in harder edges.

Color emission = Color(0, 0, 0, 1) 🔗

void set_emission(value: Color)

The Color of the light emitted by the FogVolume. Emitted light will not cast light or shadows on other objects, but can be useful for modulating the Color of the FogVolume independently from light sources.

float height_falloff = 0.0 🔗

void set_height_falloff(value: float)

float get_height_falloff()

The rate by which the height-based fog decreases in density as height increases in world space. A high falloff will result in a sharp transition, while a low falloff will result in a smoother transition. A value of 0.0 results in uniform-density fog. The height threshold is determined by the height of the associated FogVolume.

Please read the User-contributed notes policy before submitting a comment.

---

## FogVolume

**URL:** https://docs.godotengine.org/en/stable/classes/class_fogvolume.html

**Contents:**
- FogVolume
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualInstance3D < Node3D < Node < Object

A region that contributes to the default volumetric fog from the world environment.

FogVolumes are used to add localized fog into the global volumetric fog effect. FogVolumes can also remove volumetric fog from specific areas if using a FogMaterial with a negative FogMaterial.density.

Performance of FogVolumes is directly related to their relative size on the screen and the complexity of their attached FogMaterial. It is best to keep FogVolumes relatively small and simple where possible.

Note: FogVolumes only have a visible effect if Environment.volumetric_fog_enabled is true. If you don't want fog to be globally visible (but only within FogVolume nodes), set Environment.volumetric_fog_density to 0.0.

Volumetric fog and fog volumes

void set_material(value: Material)

Material get_material()

The Material used by the FogVolume. Can be either a built-in FogMaterial or a custom ShaderMaterial.

FogVolumeShape shape = 3 🔗

void set_shape(value: FogVolumeShape)

FogVolumeShape get_shape()

The shape of the FogVolume. This can be set to either RenderingServer.FOG_VOLUME_SHAPE_ELLIPSOID, RenderingServer.FOG_VOLUME_SHAPE_CONE, RenderingServer.FOG_VOLUME_SHAPE_CYLINDER, RenderingServer.FOG_VOLUME_SHAPE_BOX or RenderingServer.FOG_VOLUME_SHAPE_WORLD.

Vector3 size = Vector3(2, 2, 2) 🔗

void set_size(value: Vector3)

The size of the FogVolume when shape is RenderingServer.FOG_VOLUME_SHAPE_ELLIPSOID, RenderingServer.FOG_VOLUME_SHAPE_CONE, RenderingServer.FOG_VOLUME_SHAPE_CYLINDER or RenderingServer.FOG_VOLUME_SHAPE_BOX.

Note: Thin fog volumes may appear to flicker when the camera moves or rotates. This can be alleviated by increasing ProjectSettings.rendering/environment/volumetric_fog/volume_depth (at a performance cost) or by decreasing Environment.volumetric_fog_length (at no performance cost, but at the cost of lower fog range). Alternatively, the FogVolume can be made thicker and use a lower density in the material.

Note: If shape is RenderingServer.FOG_VOLUME_SHAPE_CONE or RenderingServer.FOG_VOLUME_SHAPE_CYLINDER, the cone/cylinder will be adjusted to fit within the size. Non-uniform scaling of cone/cylinder shapes via the size property is not supported, but you can scale the FogVolume node instead.

Please read the User-contributed notes policy before submitting a comment.

---

## Fog shaders

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/shader_reference/fog_shader.html

**Contents:**
- Fog shaders
- Built-ins
- Global built-ins
- Fog built-ins
- User-contributed notes

Fog shaders are used to define how fog is added (or subtracted) from a scene in a given area. Fog shaders are always used together with FogVolumes and volumetric fog. Fog shaders only have one processing function, the fog() function.

The resolution of the fog shaders depends on the resolution of the volumetric fog froxel grid. Accordingly, the level of detail that a fog shader can add depends on how close the FogVolume is to the camera.

Fog shaders are a special form of compute shader that is called once for every froxel that is touched by an axis aligned bounding box of the associated FogVolume. This means that froxels that just barely touch a given FogVolume will still be used.

Values marked as in are read-only. Values marked as out can optionally be written to and will not necessarily contain sensible values. Samplers cannot be written to so they are not marked.

Global built-ins are available everywhere, including in custom functions.

Global time since the engine has started, in seconds. It repeats after every 3,600 seconds (which can be changed with the rollover setting). It's affected by time_scale but not by pausing. If you need a TIME variable that is not affected by time scale, add your own global shader uniform and update it each frame.

A PI constant (3.141592). A ratio of a circle's circumference to its diameter and amount of radians in half turn.

A TAU constant (6.283185). An equivalent of PI * 2 and amount of radians in full turn.

An E constant (2.718281). Euler's number and a base of the natural logarithm.

All of the output values of fog volumes overlap one another. This allows FogVolumes to be rendered efficiently as they can all be drawn at once.

in vec3 WORLD_POSITION

Position of current froxel cell in world space.

in vec3 OBJECT_POSITION

Position of the center of the current FogVolume in world space.

3-dimensional UV, used to map a 3D texture to the current FogVolume.

Size of the current FogVolume when its shape has a size.

Signed distance field to the surface of the FogVolume. Negative if inside volume, positive otherwise.

Output base color value, interacts with light to produce final color. Only written to fog volume if used.

Output density value. Can be negative to allow subtracting one volume from another. Density must be used for fog shader to write anything at all.

Output emission color value, added to color during light pass to produce final color. Only written to fog volume if used.

Please read the User-contributed notes policy before submitting a comment.

---

## LightmapperRD

**URL:** https://docs.godotengine.org/en/stable/classes/class_lightmapperrd.html

**Contents:**
- LightmapperRD
- Description
- User-contributed notes

Inherits: Lightmapper < RefCounted < Object

The built-in GPU-based lightmapper for use with LightmapGI.

LightmapperRD ("RD" stands for RenderingDevice) is the built-in GPU-based lightmapper for use with LightmapGI. On most dedicated GPUs, it can bake lightmaps much faster than most CPU-based lightmappers. LightmapperRD uses compute shaders to bake lightmaps, so it does not require CUDA or OpenCL libraries to be installed to be usable.

Note: Only usable when using the RenderingDevice backend (Forward+ or Mobile renderers), not Compatibility.

Please read the User-contributed notes policy before submitting a comment.

---

## Making trees

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/making_trees.html

**Contents:**
- Making trees
- Start with a tree
- Paint with vertex colors
- Write a custom shader for the leaves
- Improving the shader
- User-contributed notes

This is a short tutorial on how to make trees and other types of vegetation from scratch.

The aim is to not focus on the modeling techniques (there are plenty of tutorials about that), but how to make them look good in Godot.

I took this tree from SketchFab:

https://sketchfab.com/models/ea5e6ed7f9d6445ba69589d503e8cebf

and opened it in Blender.

The first thing you may want to do is to use the vertex colors to paint how much the tree will sway when there is wind. Just use the vertex color painting tool of your favorite 3D modeling program and paint something like this:

This is a bit exaggerated, but the idea is that color indicates how much sway affects every part of the tree. This scale here represents it better:

This is an example of a shader for leaves:

This is a spatial shader. There is no front/back culling (so leaves can be seen from both sides), and alpha prepass is used, so there are less depth artifacts that result from using transparency (and leaves cast shadow). Finally, for the sway effect, world coordinates are recommended, so the tree can be duplicated, moved, etc. and it will still work together with other trees.

Here, the texture is read, as well as a transmission color, which is used to add some back-lighting to the leaves, simulating subsurface scattering.

This is the code to create the sway of the leaves. It's basic (just uses a sinewave multiplying by the time and axis position, but works well). Notice that the strength is multiplied by the color. Every axis uses a different small near 1.0 multiplication factor so axes don't appear in sync.

Finally, all that's left is the fragment shader:

And this is pretty much it.

The trunk shader is similar, except it does not write to the alpha channel (thus no alpha prepass is needed) and does not require transmission to work. Both shaders can be improved by adding normal mapping, AO and other maps.

There are many more resources on how to do this that you can read. Now that you know the basics, a recommended read is the chapter from GPU Gems3 about how Crysis does this (focus mostly on the sway code, as many other techniques shown there are obsolete):

https://developer.nvidia.com/gpugems/GPUGems3/gpugems3_ch16.html

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
shader_type spatial;
render_mode depth_prepass_alpha, cull_disabled, world_vertex_coords;
```

Example 2 (unknown):
```unknown
uniform sampler2D texture_albedo : source_color;
uniform vec4 transmission : source_color;
```

Example 3 (cpp):
```cpp
uniform float sway_speed = 1.0;
uniform float sway_strength = 0.05;
uniform float sway_phase_len = 8.0;

void vertex() {
    float strength = COLOR.r * sway_strength;
    VERTEX.x += sin(VERTEX.x * sway_phase_len * 1.123 + TIME * sway_speed) * strength;
    VERTEX.y += sin(VERTEX.y * sway_phase_len + TIME * sway_speed * 1.12412) * strength;
    VERTEX.z += sin(VERTEX.z * sway_phase_len * 0.9123 + TIME * sway_speed * 1.3123) * strength;
}
```

Example 4 (cpp):
```cpp
void fragment() {
    vec4 albedo_tex = texture(texture_albedo, UV);
    ALBEDO = albedo_tex.rgb;
    ALPHA = albedo_tex.a;
    METALLIC = 0.0;
    ROUGHNESS = 1.0;
    SSS_TRANSMITTANCE_COLOR = transmission.rgba;
}
```

---

## Material

**URL:** https://docs.godotengine.org/en/stable/classes/class_material.html

**Contents:**
- Material
- Description
- Tutorials
- Properties
- Methods
- Constants
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: BaseMaterial3D, CanvasItemMaterial, FogMaterial, PanoramaSkyMaterial, ParticleProcessMaterial, PhysicalSkyMaterial, PlaceholderMaterial, ProceduralSkyMaterial, ShaderMaterial

Virtual base class for applying visual properties to an object, such as color and roughness.

Material is a base resource used for coloring and shading geometry. All materials inherit from it and almost all VisualInstance3D derived nodes carry a Material. A few flags and parameters are shared between all material types and are configured here.

Importantly, you can inherit from Material to create your own custom material type in script or in GDExtension.

3D Material Testers Demo

Third Person Shooter (TPS) Demo

_can_do_next_pass() virtual const

_can_use_render_priority() virtual const

_get_shader_mode() virtual required const

_get_shader_rid() virtual required const

create_placeholder() const

inspect_native_shader_code()

RENDER_PRIORITY_MAX = 127 🔗

Maximum value for the render_priority parameter.

RENDER_PRIORITY_MIN = -128 🔗

Minimum value for the render_priority parameter.

void set_next_pass(value: Material)

Material get_next_pass()

Sets the Material to be used for the next pass. This renders the object again using a different material.

Note: next_pass materials are not necessarily drawn immediately after the source Material. Draw order is determined by material properties, render_priority, and distance to camera.

Note: This only applies to StandardMaterial3Ds and ShaderMaterials with type "Spatial".

int render_priority 🔗

void set_render_priority(value: int)

int get_render_priority()

Sets the render priority for objects in 3D scenes. Higher priority objects will be sorted in front of lower priority objects. In other words, all objects with render_priority 1 will render on top of all objects with render_priority 0.

Note: This only applies to StandardMaterial3Ds and ShaderMaterials with type "Spatial".

Note: This will not impact how transparent objects are sorted relative to opaque objects or how dynamic meshes will be sorted relative to other opaque meshes. This is because all transparent objects are drawn after all opaque objects and all dynamic opaque meshes are drawn before other opaque meshes.

bool _can_do_next_pass() virtual const 🔗

Only exposed for the purpose of overriding. You cannot call this function directly. Used internally to determine if next_pass should be shown in the editor or not.

bool _can_use_render_priority() virtual const 🔗

Only exposed for the purpose of overriding. You cannot call this function directly. Used internally to determine if render_priority should be shown in the editor or not.

Mode _get_shader_mode() virtual required const 🔗

Only exposed for the purpose of overriding. You cannot call this function directly. Used internally by various editor tools.

RID _get_shader_rid() virtual required const 🔗

Only exposed for the purpose of overriding. You cannot call this function directly. Used internally by various editor tools. Used to access the RID of the Material's Shader.

Resource create_placeholder() const 🔗

Creates a placeholder version of this resource (PlaceholderMaterial).

void inspect_native_shader_code() 🔗

Only available when running in the editor. Opens a popup that visualizes the generated shader code, including all variants and internal shader code. See also Shader.inspect_native_shader_code().

Please read the User-contributed notes policy before submitting a comment.

---

## Multiple resolutions

**URL:** https://docs.godotengine.org/en/stable/tutorials/rendering/multiple_resolutions.html

**Contents:**
- Multiple resolutions
- The problem of multiple resolutions
- One size fits all
- Base size
- Resizing
- Stretch settings
  - Stretch Mode
  - Stretch Aspect
  - Stretch Scale
  - Stretch Scale Mode

Developers often have trouble understanding how to best support multiple resolutions in their games. For desktop and console games, this is more or less straightforward, as most screen aspect ratios are 16:9 and resolutions are standard (720p, 1080p, 1440p, 4K, …).

For mobile games, at first, it was easy. For many years, the iPhone and iPad used the same resolution. When Retina was implemented, they just doubled the pixel density; most developers had to supply assets in default and double resolutions.

Nowadays, this is no longer the case, as there are plenty of different screen sizes, densities, and aspect ratios. Non-conventional sizes are also becoming increasingly popular, such as ultrawide displays.

For 3D rendering, there is not much of a need to support multiple resolutions. Thanks to its vector-based nature, 3D geometry will just fill the screen based on the viewport size. For 2D and game UIs, this is a different matter, as art needs to be created using specific pixel sizes in software such as Photoshop, GIMP or Krita.

Since layouts, aspect ratios, resolutions, and pixel densities can change so much, it is no longer possible to design UIs for every specific screen. Another method must be used.

The most common approach is to use a single base resolution and then fit it to everything else. This resolution is how most players are expected to play the game (given their hardware). For mobile, Google has useful stats online, and for desktop, Steam also does.

As an example, Steam shows that the most common primary display resolution is 1920×1080, so a sensible approach is to develop a game for this resolution, then handle scaling for different sizes and aspect ratios.

Godot provides several useful tools to do this easily.

You can see how Godot's support for multiple resolutions works in action using the Multiple Resolutions and Aspect Ratios demo project.

A base size for the window can be specified in the Project Settings under Display → Window.

However, what it does is not completely obvious; the engine will not attempt to switch the monitor to this resolution. Rather, think of this setting as the "design size", i.e. the size of the area that you work with in the editor. This setting corresponds directly to the size of the blue rectangle in the 2D editor.

There is often a need to support devices with screen and window sizes that are different from this base size. Godot offers many ways to control how the viewport will be resized and stretched to different screen sizes.

On this page, window refers to the screen area allotted to your game by the system, while viewport refers to the root object (accessible from get_tree().root) which the game controls to fill this screen area. This viewport is a Window instance. Recall from the introduction that all Window objects are viewports.

To configure the stretch base size at runtime from a script, use the get_tree().root.content_scale_size property (see Window.content_scale_size). Changing this value can indirectly change the size of 2D elements. However, to provide a user-accessible scaling option, using Stretch Scale is recommended as it's easier to adjust.

Godot follows a modern approach to multiple resolutions. The engine will never change the monitor's resolution on its own. While changing the monitor's resolution is the most efficient approach, it's also the least reliable approach as it can leave the monitor stuck on a low resolution if the game crashes. This is especially common on macOS or Linux which don't handle resolution changes as well as Windows.

Changing the monitor's resolution also removes any control from the game developer over filtering and aspect ratio stretching, which can be important to ensure correct display for pixel art games.

On top of that, changing the monitor's resolution makes alt-tabbing in and out of a game much slower since the monitor has to change resolutions every time this is done.

There are several types of devices, with several types of screens, which in turn have different pixel density and resolutions. Handling all of them can be a lot of work, so Godot tries to make the developer's life a little easier. The Viewport node has several functions to handle resizing, and the root node of the scene tree is always a viewport (scenes loaded are instanced as a child of it, and it can always be accessed by calling get_tree().root or get_node("/root")).

In any case, while changing the root Viewport params is probably the most flexible way to deal with the problem, it can be a lot of work, code and guessing, so Godot provides a set of parameters in the project settings to handle multiple resolutions.

To render 3D at a lower resolution than 2D elements (without needing separate viewports), you can use Godot's resolution scaling support. This is a good way to improve performance significantly in GPU-bottlenecked scenarios. This works with any stretch mode and stretch aspect combination.

Stretch settings are located in the project settings and provide several options:

The Stretch Mode setting defines how the base size is stretched to fit the resolution of the window or screen. The animations below use a "base size" of just 16×9 pixels to demonstrate the effect of different stretch modes. A single sprite, also 16×9 pixels in size, covers the entire viewport, and a diagonal Line2D is added on top of it:

Stretch Mode = Disabled (default): No stretching happens. One unit in the scene corresponds to one pixel on the screen. In this mode, the Stretch Aspect setting has no effect.

Stretch Mode = Canvas Items: In this mode, the base size specified in width and height in the project settings is stretched to cover the whole screen (taking the Stretch Aspect setting into account). This means that everything is rendered directly at the target resolution. 3D is unaffected, while in 2D, there is no longer a 1:1 correspondence between sprite pixels and screen pixels, which may result in scaling artifacts.

Stretch Mode = Viewport: Viewport scaling means that the size of the root Viewport is set precisely to the base size specified in the Project Settings' Display section. The scene is rendered to this viewport first. Finally, this viewport is scaled to fit the screen (taking the Stretch Aspect setting into account).

To configure the stretch mode at runtime from a script, use the get_tree().root.content_scale_mode property (see Window.content_scale_mode and the ContentScaleMode enum).

The second setting is the stretch aspect. Note that this only takes effect if Stretch Mode is set to something other than Disabled.

In the animations below, you will notice gray and black areas. The black areas are added by the engine and cannot be drawn into. The gray areas are part of your scene, and can be drawn to. The gray areas correspond to the region outside the blue frame you see in the 2D editor.

Stretch Aspect = Ignore: Ignore the aspect ratio when stretching the screen. This means that the original resolution will be stretched to exactly fill the screen, even if it's wider or narrower. This may result in nonuniform stretching: things looking wider or taller than designed.

Stretch Aspect = Keep: Keep aspect ratio when stretching the screen. This means that the viewport retains its original size regardless of the screen resolution, and black bars will be added to the top/bottom of the screen ("letterboxing") or the sides ("pillarboxing").

This is a good option if you know the aspect ratio of your target devices in advance, or if you don't want to handle different aspect ratios.

Stretch Aspect = Keep Width: Keep aspect ratio when stretching the screen. If the screen is wider than the base size, black bars are added at the left and right (pillarboxing). But if the screen is taller than the base resolution, the viewport will be grown in the vertical direction (and more content will be visible to the bottom). You can also think of this as "Expand Vertically".

This is usually the best option for creating GUIs or HUDs that scale, so some controls can be anchored to the bottom (Size and anchors).

Stretch Aspect = Keep Height: Keep aspect ratio when stretching the screen. If the screen is taller than the base size, black bars are added at the top and bottom (letterboxing). But if the screen is wider than the base resolution, the viewport will be grown in the horizontal direction (and more content will be visible to the right). You can also think of this as "Expand Horizontally".

This is usually the best option for 2D games that scroll horizontally (like runners or platformers).

Stretch Aspect = Expand: Keep aspect ratio when stretching the screen, but keep neither the base width nor height. Depending on the screen aspect ratio, the viewport will either be larger in the horizontal direction (if the screen is wider than the base size) or in the vertical direction (if the screen is taller than the original size).

To support both portrait and landscape mode with a similar automatically determined scale factor, set your project's base resolution to be a square (1:1 aspect ratio) instead of a rectangle. For instance, if you wish to design for 1280×720 as the base resolution but wish to support both portrait and landscape mode, use 720×720 as the project's base window size in the Project Settings.

To allow the user to choose their preferred screen orientation at runtime, remember to set Display > Window > Handheld > Orientation to sensor.

To configure the stretch aspect at runtime from a script, use the get_tree().root.content_scale_aspect property (see Window.content_scale_aspect and the ContentScaleAspect enum).

The Scale setting allows you to add an extra scaling factor on top of what the Stretch options above already provide. The default value of 1.0 means that no additional scaling occurs.

For example, if you set Scale to 2.0 and leave Stretch Mode on Disabled, each unit in your scene will correspond to 2×2 pixels on the screen. This is a good way to provide scaling options for non-game applications.

If Stretch Mode is set to canvas_items, 2D elements will be scaled relative to the base window size, then multiplied by the Scale setting. This can be exposed to players to allow them to adjust the automatically determined scale to their liking, for better accessibility.

If Stretch Mode is set to viewport, the viewport's resolution is divided by Scale. This makes pixels look larger and reduces rendering resolution (with a given window size), which can improve performance.

To configure the stretch scale at runtime from a script, use the get_tree().root.content_scale_factor property (see Window.content_scale_factor).

You can also adjust the scale at which the default project theme is generated using the GUI > Theme > Default Theme Scale project setting. This can be used to create more logically-sized UIs at base resolutions that are significantly higher or lower than the default. However, this project setting cannot be changed at runtime, as its value is only read once when the project starts.

Since Godot 4.2, the Stretch Scale Mode setting allows you to constrain the automatically determined scale factor (as well as the manually specified Stretch Scale setting) to integer values. By default, this setting is set to fractional, which allows any scale factor to be applied (including fractional values such as 2.5). When set to integer, the value is rounded down to the nearest integer. For example, instead of using a scale factor of 2.5, it would be rounded down to 2.0. This is useful to prevent distortion when displaying pixel art.

Compare this pixel art which is displayed with the viewport stretch mode, with the stretch scale mode set to fractional:

Checkerboard doesn't look "even". Line widths in the logo and text varies wildly.

This pixel art is also displayed with the viewport stretch mode, but the stretch scale mode is set to integer this time:

Checkerboard looks perfectly even. Line widths are consistent.

For example, if your viewport base size is 640×360 and the window size is 1366×768:

When using fractional, the viewport is displayed at a resolution of 1366×768 (scale factor is roughly 2.133×). The entire window space is used. Each pixel in the viewport corresponds to 2.133×2.133 pixels in the displayed area. However, since displays can only display "whole" pixels, this will lead to uneven pixel scaling which results in incorrect appearance of pixel art.

When using integer, the viewport is displayed at a resolution of 1280×720 (scale factor is 2×). The remaining space is filled with black bars on all four sides, so that each pixel in the viewport corresponds to 2×2 pixels in the displayed area.

This setting is effective with any stretch mode. However, when using the disabled stretch mode, it will only affect the Stretch Scale setting by rounding it down to the nearest integer value. This can be used for 3D games that have a pixel art UI, so that the visible area in the 3D viewport doesn't reduce in size (which occurs when using canvas_items or viewport stretch mode with the integer scale mode).

Games should use the Exclusive Fullscreen window mode, as opposed to Fullscreen which is designed to prevent Windows from automatically treating the window as if it was exclusive fullscreen.

Fullscreen is meant to be used by GUI applications that want to use per-pixel transparency without a risk of having it disabled by the OS. It achieves this by leaving a 1-pixel line at the bottom of the screen. By contrast, Exclusive Fullscreen uses the actual screen size and allows Windows to reduce jitter and input lag for fullscreen games.

When using integer scaling, this is particularly important as the 1-pixel height reduction from the Fullscreen mode can cause integer scaling to use a smaller scale factor than expected.

The following settings are recommended to support multiple resolutions and aspect ratios well.

Set the base window width to 1920 and window height to 1080. If you have a display smaller than 1920×1080, set Window Width Override and Window Height Override to lower values to make the window smaller when the project starts.

Alternatively, if you're targeting high-end devices primarily, set the base window width to 3840 and window height to 2160. This allows you to provide higher resolution 2D assets, resulting in crisper visuals at the cost of higher memory usage and file sizes. You'll also want to increase GUI > Theme > Default Theme Scale to a value between 2.0 and 3.0 to ensure UI elements remain readable.

Note that this will make non-mipmapped textures grainy on low resolution devices, so make sure to follow the instructions described in Reducing aliasing on downsampling.

Set the stretch mode to canvas_items.

Set the stretch aspect to expand. This allows for supporting multiple aspect ratios and makes better use of tall smartphone displays (such as 18:9 or 19:9 aspect ratios).

Configure Control nodes' anchors to snap to the correct corners using the Layout menu.

For 3D games, consider exposing Resolution scaling in the game's options menu to allow players to adjust the 3D rendering resolution separately from UI elements. This is useful for performance tuning, especially on lower-end hardware.

Set the base window size to the viewport size you intend to use. Most pixel art games use viewport sizes between 256×224 and 640×480. 640×360 is a good baseline, as it scales to 1280×720, 1920×1080, 2560×1440, and 3840×2160 without any black bars when using integer scaling. Higher viewport sizes will require using higher resolution artwork, unless you intend to show more of the game world at a given time.

Set the stretch mode to viewport.

Set the stretch aspect to keep to enforce a single aspect ratio (with black bars). As an alternative, you can set the stretch aspect to expand to support multiple aspect ratios.

If using the expand stretch aspect, Configure Control nodes' anchors to snap to the correct corners using the Layout menu.

Set the stretch scale mode to integer. This prevents uneven pixel scaling from occurring, which makes pixel art not display as intended.

The viewport stretch mode provides low-resolution rendering that is then stretched to the final window size. If you are OK with sprites being able to move or rotate in "sub-pixel" positions or wish to have a high resolution 3D viewport, you should use the canvas_items stretch mode instead of the viewport stretch mode.

Godot is configured to use landscape mode by default. This means you don't need to change the display orientation project setting.

Set the base window width to 1280 and window height to 720.

Alternatively, if you're targeting high-end devices primarily, set the base window width to 1920 and window height to 1080. This allows you to provide higher resolution 2D assets, resulting in crisper visuals at the cost of higher memory usage and file sizes. Many devices have even higher resolution displays (1440p), but the difference with 1080p is barely visible given the small size of smartphone displays. You'll also want to increase GUI > Theme > Default Theme Scale to a value between 1.5 and 2.0 to ensure UI elements remain readable.

Note that this will make non-mipmapped textures grainy on low resolution devices, so make sure to follow the instructions described in Reducing aliasing on downsampling.

Set the stretch mode to canvas_items.

Set the stretch aspect to expand. This allows for supporting multiple aspect ratios and makes better use of tall smartphone displays (such as 18:9 or 19:9 aspect ratios).

Configure Control nodes' anchors to snap to the correct corners using the Layout menu.

To better support tablets and foldable phones (which frequently feature displays with aspect ratios close to 4:3), consider using a base resolution that has a 4:3 aspect ratio while following the rest of the instructions here. For instance, you can set the base window width to 1280 and the base window height to 960.

Set the base window width to 720 and window height to 1280.

Alternatively, if you're targeting high-end devices primarily, set the base window width to 1080 and window height to 1920. This allows you to provide higher resolution 2D assets, resulting in crisper visuals at the cost of higher memory usage and file sizes. Many devices have even higher resolution displays (1440p), but the difference with 1080p is barely visible given the small size of smartphone displays. You'll also want to increase GUI > Theme > Default Theme Scale to a value between 1.5 and 2.0 to ensure UI elements remain readable.

Note that this will make non-mipmapped textures grainy on low resolution devices, so make sure to follow the instructions described in Reducing aliasing on downsampling.

Set Display > Window > Handheld > Orientation to portrait.

Set the stretch mode to canvas_items.

Set the stretch aspect to expand. This allows for supporting multiple aspect ratios and makes better use of tall smartphone displays (such as 18:9 or 19:9 aspect ratios).

Configure Control nodes' anchors to snap to the correct corners using the Layout menu.

To better support tablets and foldable phones (which frequently feature displays with aspect ratios close to 4:3), consider using a base resolution that has a 3:4 aspect ratio while following the rest of the instructions here. For instance, you can set the base window width to 960 and the base window height to 1280.

Set the base window width and height to the smallest window size that you intend to target. This is not required, but this ensures that you design your UI with small window sizes in mind.

Keep the stretch mode to its default value, disabled.

Keep the stretch aspect to its default value, ignore (its value won't be used since the stretch mode is disabled).

You can define a minimum window size by calling get_window().set_min_size() in a script's _ready() function. This prevents the user from resizing the application below a certain size, which could break the UI layout.

Add a setting in the application's settings to change the root viewport's stretch scale, so that the UI can be made larger to account for hiDPI displays. See also the section on hiDPI support below.

By default, Godot projects are considered DPI-aware by the operating system. This is controlled by the Display > Window > DPI > Allow hiDPI project setting, which should be left enabled whenever possible. Disabling DPI awareness can break fullscreen behavior on Windows.

Since Godot projects are DPI-aware, they may appear at a very small window size when launching on an hiDPI display (proportionally to the screen resolution). For a game, the most common way to work around this issue is to make them fullscreen by default. Alternatively, you could set the window size in an autoload's _ready() function according to the screen size.

To ensure 2D elements don't appear too small on hiDPI displays:

For games, use the canvas_items or viewport stretch modes so that 2D elements are automatically resized according to the current window size.

For non-game applications, use the disabled stretch mode and set the stretch scale to a value corresponding to the display scale factor in an autoload's _ready() function. The display scale factor is set in the operating system's settings and can be queried using screen_get_scale. This method is currently implemented on Android, iOS, Linux (Wayland only), macOS and Web. On other platforms, you'll have to implement a method to guess the display scale factor based on the screen resolution (with a setting to let the user override this if needed). This is the approach currently used by the Godot editor.

The Allow hiDPI setting is only effective on Windows and macOS. It's ignored on all other platforms.

The Godot editor itself is always marked as DPI-aware. Running the project from the editor will only be DPI-aware if Allow hiDPI is enabled in the Project Settings.

If the game has a very high base resolution (e.g. 3840×2160), aliasing might appear when downsampling to something considerably lower like 1280×720.

To resolve this, you can enable mipmaps on all your 2D textures. However, enabling mipmaps will increase memory usage which can be an issue on low-end mobile devices.

Once scaling for different resolutions is accounted for, make sure that your user interface also scales for different aspect ratios. This can be done using anchors and/or containers.

The 3D Camera node's Keep Aspect property defaults to the Keep Height scaling mode (also called Hor+). This is usually the best value for desktop games and mobile games in landscape mode, as widescreen displays will automatically use a wider field of view.

However, if your 3D game is intended to be played in portrait mode, it may make more sense to use Keep Width instead (also called Vert-). This way, smartphones with an aspect ratio taller than 16:9 (e.g. 19:9) will use a taller field of view, which is more logical here.

To render 3D at a different resolution from 2D elements (such as the UI), use Godot's resolution scaling functionality. This allows you to control the resolution scale factor used for 3D without needing to use a separate Viewport node. This can either be used to improve performance by rendering 3D at a lower resolution, or improve quality via supersampling.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRCompositionLayerCylinder

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrcompositionlayercylinder.html

**Contents:**
- OpenXRCompositionLayerCylinder
- Description
- Properties
- Property Descriptions
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: OpenXRCompositionLayer < Node3D < Node < Object

An OpenXR composition layer that is rendered as an internal slice of a cylinder.

An OpenXR composition layer that allows rendering a SubViewport on an internal slice of a cylinder.

float aspect_ratio = 1.0 🔗

void set_aspect_ratio(value: float)

float get_aspect_ratio()

The aspect ratio of the slice. Used to set the height relative to the width.

float central_angle = 1.5707964 🔗

void set_central_angle(value: float)

float get_central_angle()

The central angle of the cylinder. Used to set the width.

int fallback_segments = 10 🔗

void set_fallback_segments(value: int)

int get_fallback_segments()

The number of segments to use in the fallback mesh.

void set_radius(value: float)

The radius of the cylinder.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRCompositionLayerQuad

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrcompositionlayerquad.html

**Contents:**
- OpenXRCompositionLayerQuad
- Description
- Properties
- Property Descriptions
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: OpenXRCompositionLayer < Node3D < Node < Object

An OpenXR composition layer that is rendered as a quad.

An OpenXR composition layer that allows rendering a SubViewport on a quad.

Vector2 quad_size = Vector2(1, 1) 🔗

void set_quad_size(value: Vector2)

Vector2 get_quad_size()

The dimensions of the quad.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRCompositionLayer

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrcompositionlayer.html

**Contents:**
- OpenXRCompositionLayer
- Description
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: Node3D < Node < Object

Inherited By: OpenXRCompositionLayerCylinder, OpenXRCompositionLayerEquirect, OpenXRCompositionLayerQuad

The parent class of all OpenXR composition layer nodes.

Composition layers allow 2D viewports to be displayed inside of the headset by the XR compositor through special projections that retain their quality. This allows for rendering clear text while keeping the layer at a native resolution.

Note: If the OpenXR runtime doesn't support the given composition layer type, a fallback mesh can be generated with a ViewportTexture, in order to emulate the composition layer.

swapchain_state_alpha_swizzle

swapchain_state_blue_swizzle

swapchain_state_border_color

swapchain_state_green_swizzle

swapchain_state_horizontal_wrap

swapchain_state_mag_filter

swapchain_state_max_anisotropy

swapchain_state_min_filter

swapchain_state_mipmap_mode

swapchain_state_red_swizzle

swapchain_state_vertical_wrap

get_android_surface()

intersects_ray(origin: Vector3, direction: Vector3) const

is_natively_supported() const

Filter FILTER_NEAREST = 0

Perform nearest-neighbor filtering when sampling the texture.

Filter FILTER_LINEAR = 1

Perform linear filtering when sampling the texture.

Filter FILTER_CUBIC = 2

Perform cubic filtering when sampling the texture.

MipmapMode MIPMAP_MODE_DISABLED = 0

Note: Mipmapping can only be disabled in the Compatibility renderer.

MipmapMode MIPMAP_MODE_NEAREST = 1

Use the mipmap of the nearest resolution.

MipmapMode MIPMAP_MODE_LINEAR = 2

Use linear interpolation of the two mipmaps of the nearest resolution.

Wrap WRAP_CLAMP_TO_BORDER = 0

Clamp the texture to its specified border color.

Wrap WRAP_CLAMP_TO_EDGE = 1

Clamp the texture to its edge color.

Repeat the texture infinitely.

Wrap WRAP_MIRRORED_REPEAT = 3

Repeat the texture infinitely, mirroring it on each repeat.

Wrap WRAP_MIRROR_CLAMP_TO_EDGE = 4

Mirror the texture once and then clamp the texture to its edge color.

Note: This wrap mode is not available in the Compatibility renderer.

Swizzle SWIZZLE_RED = 0

Maps a color channel to the value of the red channel.

Swizzle SWIZZLE_GREEN = 1

Maps a color channel to the value of the green channel.

Swizzle SWIZZLE_BLUE = 2

Maps a color channel to the value of the blue channel.

Swizzle SWIZZLE_ALPHA = 3

Maps a color channel to the value of the alpha channel.

Swizzle SWIZZLE_ZERO = 4

Maps a color channel to the value of zero.

Swizzle SWIZZLE_ONE = 5

Maps a color channel to the value of one.

bool alpha_blend = false 🔗

void set_alpha_blend(value: bool)

bool get_alpha_blend()

Enables the blending the layer using its alpha channel.

Can be combined with Viewport.transparent_bg to give the layer a transparent background.

Vector2i android_surface_size = Vector2i(1024, 1024) 🔗

void set_android_surface_size(value: Vector2i)

Vector2i get_android_surface_size()

The size of the Android surface to create if use_android_surface is enabled.

bool enable_hole_punch = false 🔗

void set_enable_hole_punch(value: bool)

bool get_enable_hole_punch()

Enables a technique called "hole punching", which allows putting the composition layer behind the main projection layer (i.e. setting sort_order to a negative value) while "punching a hole" through everything rendered by Godot so that the layer is still visible.

This can be used to create the illusion that the composition layer exists in the same 3D space as everything rendered by Godot, allowing objects to appear to pass both behind or in front of the composition layer.

SubViewport layer_viewport 🔗

void set_layer_viewport(value: SubViewport)

SubViewport get_layer_viewport()

The SubViewport to render on the composition layer.

void set_sort_order(value: int)

The sort order for this composition layer. Higher numbers will be shown in front of lower numbers.

Note: This will have no effect if a fallback mesh is being used.

Swizzle swapchain_state_alpha_swizzle = 3 🔗

void set_alpha_swizzle(value: Swizzle)

Swizzle get_alpha_swizzle()

The swizzle value for the alpha channel of the swapchain state.

Note: This property only has an effect on devices that support the OpenXR XR_FB_swapchain_update_state OpenGLES/Vulkan extensions.

Swizzle swapchain_state_blue_swizzle = 2 🔗

void set_blue_swizzle(value: Swizzle)

Swizzle get_blue_swizzle()

The swizzle value for the blue channel of the swapchain state.

Note: This property only has an effect on devices that support the OpenXR XR_FB_swapchain_update_state OpenGLES/Vulkan extensions.

Color swapchain_state_border_color = Color(0, 0, 0, 0) 🔗

void set_border_color(value: Color)

Color get_border_color()

The border color of the swapchain state that is used when the wrap mode clamps to the border.

Note: This property only has an effect on devices that support the OpenXR XR_FB_swapchain_update_state OpenGLES/Vulkan extensions.

Swizzle swapchain_state_green_swizzle = 1 🔗

void set_green_swizzle(value: Swizzle)

Swizzle get_green_swizzle()

The swizzle value for the green channel of the swapchain state.

Note: This property only has an effect on devices that support the OpenXR XR_FB_swapchain_update_state OpenGLES/Vulkan extensions.

Wrap swapchain_state_horizontal_wrap = 0 🔗

void set_horizontal_wrap(value: Wrap)

Wrap get_horizontal_wrap()

The horizontal wrap mode of the swapchain state.

Note: This property only has an effect on devices that support the OpenXR XR_FB_swapchain_update_state OpenGLES/Vulkan extensions.

Filter swapchain_state_mag_filter = 1 🔗

void set_mag_filter(value: Filter)

Filter get_mag_filter()

The magnification filter of the swapchain state.

Note: This property only has an effect on devices that support the OpenXR XR_FB_swapchain_update_state OpenGLES/Vulkan extensions.

float swapchain_state_max_anisotropy = 1.0 🔗

void set_max_anisotropy(value: float)

float get_max_anisotropy()

The max anisotropy of the swapchain state.

Note: This property only has an effect on devices that support the OpenXR XR_FB_swapchain_update_state OpenGLES/Vulkan extensions.

Filter swapchain_state_min_filter = 1 🔗

void set_min_filter(value: Filter)

Filter get_min_filter()

The minification filter of the swapchain state.

Note: This property only has an effect on devices that support the OpenXR XR_FB_swapchain_update_state OpenGLES/Vulkan extensions.

MipmapMode swapchain_state_mipmap_mode = 2 🔗

void set_mipmap_mode(value: MipmapMode)

MipmapMode get_mipmap_mode()

The mipmap mode of the swapchain state.

Note: This property only has an effect on devices that support the OpenXR XR_FB_swapchain_update_state OpenGLES/Vulkan extensions.

Swizzle swapchain_state_red_swizzle = 0 🔗

void set_red_swizzle(value: Swizzle)

Swizzle get_red_swizzle()

The swizzle value for the red channel of the swapchain state.

Note: This property only has an effect on devices that support the OpenXR XR_FB_swapchain_update_state OpenGLES/Vulkan extensions.

Wrap swapchain_state_vertical_wrap = 0 🔗

void set_vertical_wrap(value: Wrap)

Wrap get_vertical_wrap()

The vertical wrap mode of the swapchain state.

Note: This property only has an effect on devices that support the OpenXR XR_FB_swapchain_update_state OpenGLES/Vulkan extensions.

bool use_android_surface = false 🔗

void set_use_android_surface(value: bool)

bool get_use_android_surface()

If enabled, an Android surface will be created (with the dimensions from android_surface_size) which will provide the 2D content for the composition layer, rather than using layer_viewport.

See get_android_surface() for information about how to get the surface so that your application can draw to it.

Note: This will only work in Android builds.

JavaObject get_android_surface() 🔗

Returns a JavaObject representing an android.view.Surface if use_android_surface is enabled and OpenXR has created the surface. Otherwise, this will return null.

Note: The surface can only be created during an active OpenXR session. So, if use_android_surface is enabled outside of an OpenXR session, it won't be created until a new session fully starts.

Vector2 intersects_ray(origin: Vector3, direction: Vector3) const 🔗

Returns UV coordinates where the given ray intersects with the composition layer. origin and direction must be in global space.

Returns Vector2(-1.0, -1.0) if the ray doesn't intersect.

bool is_natively_supported() const 🔗

Returns true if the OpenXR runtime natively supports this composition layer type.

Note: This will only return an accurate result after the OpenXR session has started.

Please read the User-contributed notes policy before submitting a comment.

---

## PanoramaSkyMaterial

**URL:** https://docs.godotengine.org/en/stable/classes/class_panoramaskymaterial.html

**Contents:**
- PanoramaSkyMaterial
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Material < Resource < RefCounted < Object

A material that provides a special texture to a Sky, usually an HDR panorama.

A resource referenced in a Sky that is used to draw a background. PanoramaSkyMaterial functions similar to skyboxes in other engines, except it uses an equirectangular sky map instead of a Cubemap.

Using an HDR panorama is strongly recommended for accurate, high-quality reflections. Godot supports the Radiance HDR (.hdr) and OpenEXR (.exr) image formats for this purpose.

You can use this tool to convert a cubemap to an equirectangular sky map.

float energy_multiplier = 1.0 🔗

void set_energy_multiplier(value: float)

float get_energy_multiplier()

The sky's overall brightness multiplier. Higher values result in a brighter sky.

void set_filtering_enabled(value: bool)

bool is_filtering_enabled()

A boolean value to determine if the background texture should be filtered or not.

void set_panorama(value: Texture2D)

Texture2D get_panorama()

Texture2D to be applied to the PanoramaSkyMaterial.

Please read the User-contributed notes policy before submitting a comment.

---

## ParticleProcessMaterial

**URL:** https://docs.godotengine.org/en/stable/classes/class_particleprocessmaterial.html

**Contents:**
- ParticleProcessMaterial
- Description
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Material < Resource < RefCounted < Object

Holds a particle configuration for GPUParticles2D or GPUParticles3D nodes.

ParticleProcessMaterial defines particle properties and behavior. It is used in the process_material of the GPUParticles2D and GPUParticles3D nodes. Some of this material's properties are applied to each particle when emitted, while others can have a CurveTexture or a GradientTexture1D applied to vary numerical or color values over the lifetime of the particle.

angular_velocity_curve

attractor_interaction_enabled

directional_velocity_curve

directional_velocity_max

directional_velocity_min

emission_color_texture

emission_normal_texture

emission_point_texture

emission_ring_cone_angle

emission_ring_inner_radius

emission_shape_offset

emission_sphere_radius

inherit_velocity_ratio

particle_flag_align_y

particle_flag_damping_as_friction

particle_flag_disable_z

particle_flag_rotate_y

radial_velocity_curve

scale_over_velocity_curve

scale_over_velocity_max

scale_over_velocity_min

sub_emitter_amount_at_collision

sub_emitter_amount_at_end

sub_emitter_amount_at_start

sub_emitter_frequency

sub_emitter_keep_velocity

tangential_accel_curve

turbulence_influence_max

turbulence_influence_min

turbulence_influence_over_life

turbulence_initial_displacement_max

turbulence_initial_displacement_min

turbulence_noise_scale

turbulence_noise_speed

turbulence_noise_speed_random

turbulence_noise_strength

get_param(param: Parameter) const

get_param_max(param: Parameter) const

get_param_min(param: Parameter) const

get_param_texture(param: Parameter) const

get_particle_flag(particle_flag: ParticleFlags) const

set_param(param: Parameter, value: Vector2)

set_param_max(param: Parameter, value: float)

set_param_min(param: Parameter, value: float)

set_param_texture(param: Parameter, texture: Texture2D)

set_particle_flag(particle_flag: ParticleFlags, enable: bool)

emission_shape_changed() 🔗

Emitted when this material's emission shape is changed in any way. This includes changes to emission_shape, emission_shape_scale, or emission_sphere_radius, and any other property that affects the emission shape's offset, size, scale, or orientation.

Note: This signal is only emitted inside the editor for performance reasons.

Parameter PARAM_INITIAL_LINEAR_VELOCITY = 0

Use with set_param_min(), set_param_max(), and set_param_texture() to set initial velocity properties.

Parameter PARAM_ANGULAR_VELOCITY = 1

Use with set_param_min(), set_param_max(), and set_param_texture() to set angular velocity properties.

Parameter PARAM_ORBIT_VELOCITY = 2

Use with set_param_min(), set_param_max(), and set_param_texture() to set orbital velocity properties.

Parameter PARAM_LINEAR_ACCEL = 3

Use with set_param_min(), set_param_max(), and set_param_texture() to set linear acceleration properties.

Parameter PARAM_RADIAL_ACCEL = 4

Use with set_param_min(), set_param_max(), and set_param_texture() to set radial acceleration properties.

Parameter PARAM_TANGENTIAL_ACCEL = 5

Use with set_param_min(), set_param_max(), and set_param_texture() to set tangential acceleration properties.

Parameter PARAM_DAMPING = 6

Use with set_param_min(), set_param_max(), and set_param_texture() to set damping properties.

Parameter PARAM_ANGLE = 7

Use with set_param_min(), set_param_max(), and set_param_texture() to set angle properties.

Parameter PARAM_SCALE = 8

Use with set_param_min(), set_param_max(), and set_param_texture() to set scale properties.

Parameter PARAM_HUE_VARIATION = 9

Use with set_param_min(), set_param_max(), and set_param_texture() to set hue variation properties.

Parameter PARAM_ANIM_SPEED = 10

Use with set_param_min(), set_param_max(), and set_param_texture() to set animation speed properties.

Parameter PARAM_ANIM_OFFSET = 11

Use with set_param_min(), set_param_max(), and set_param_texture() to set animation offset properties.

Parameter PARAM_RADIAL_VELOCITY = 15

Use with set_param_min(), set_param_max(), and set_param_texture() to set radial velocity properties.

Parameter PARAM_DIRECTIONAL_VELOCITY = 16

Use with set_param_min(), set_param_max(), and set_param_texture() to set directional velocity properties.

Parameter PARAM_SCALE_OVER_VELOCITY = 17

Use with set_param_min(), set_param_max(), and set_param_texture() to set scale over velocity properties.

Parameter PARAM_MAX = 18

Represents the size of the Parameter enum.

Parameter PARAM_TURB_VEL_INFLUENCE = 13

Use with set_param_min() and set_param_max() to set the turbulence minimum und maximum influence on each particles velocity.

Parameter PARAM_TURB_INIT_DISPLACEMENT = 14

Use with set_param_min() and set_param_max() to set the turbulence minimum and maximum displacement of the particles spawn position.

Parameter PARAM_TURB_INFLUENCE_OVER_LIFE = 12

Use with set_param_texture() to set the turbulence influence over the particles life time.

enum ParticleFlags: 🔗

ParticleFlags PARTICLE_FLAG_ALIGN_Y_TO_VELOCITY = 0

Use with set_particle_flag() to set particle_flag_align_y.

ParticleFlags PARTICLE_FLAG_ROTATE_Y = 1

Use with set_particle_flag() to set particle_flag_rotate_y.

ParticleFlags PARTICLE_FLAG_DISABLE_Z = 2

Use with set_particle_flag() to set particle_flag_disable_z.

ParticleFlags PARTICLE_FLAG_DAMPING_AS_FRICTION = 3

There is currently no description for this enum. Please help us by contributing one!

ParticleFlags PARTICLE_FLAG_MAX = 4

Represents the size of the ParticleFlags enum.

enum EmissionShape: 🔗

EmissionShape EMISSION_SHAPE_POINT = 0

All particles will be emitted from a single point.

EmissionShape EMISSION_SHAPE_SPHERE = 1

Particles will be emitted in the volume of a sphere.

EmissionShape EMISSION_SHAPE_SPHERE_SURFACE = 2

Particles will be emitted on the surface of a sphere.

EmissionShape EMISSION_SHAPE_BOX = 3

Particles will be emitted in the volume of a box.

EmissionShape EMISSION_SHAPE_POINTS = 4

Particles will be emitted at a position determined by sampling a random point on the emission_point_texture. Particle color will be modulated by emission_color_texture.

EmissionShape EMISSION_SHAPE_DIRECTED_POINTS = 5

Particles will be emitted at a position determined by sampling a random point on the emission_point_texture. Particle velocity and rotation will be set based on emission_normal_texture. Particle color will be modulated by emission_color_texture.

EmissionShape EMISSION_SHAPE_RING = 6

Particles will be emitted in a ring or cylinder.

EmissionShape EMISSION_SHAPE_MAX = 7

Represents the size of the EmissionShape enum.

enum SubEmitterMode: 🔗

SubEmitterMode SUB_EMITTER_DISABLED = 0

There is currently no description for this enum. Please help us by contributing one!

SubEmitterMode SUB_EMITTER_CONSTANT = 1

There is currently no description for this enum. Please help us by contributing one!

SubEmitterMode SUB_EMITTER_AT_END = 2

There is currently no description for this enum. Please help us by contributing one!

SubEmitterMode SUB_EMITTER_AT_COLLISION = 3

There is currently no description for this enum. Please help us by contributing one!

SubEmitterMode SUB_EMITTER_AT_START = 4

There is currently no description for this enum. Please help us by contributing one!

SubEmitterMode SUB_EMITTER_MAX = 5

Represents the size of the SubEmitterMode enum.

enum CollisionMode: 🔗

CollisionMode COLLISION_DISABLED = 0

No collision for particles. Particles will go through GPUParticlesCollision3D nodes.

CollisionMode COLLISION_RIGID = 1

RigidBody3D-style collision for particles using GPUParticlesCollision3D nodes.

CollisionMode COLLISION_HIDE_ON_CONTACT = 2

Hide particles instantly when colliding with a GPUParticlesCollision3D node. This can be combined with a subemitter that uses the COLLISION_RIGID collision mode to "replace" the parent particle with the subemitter on impact.

CollisionMode COLLISION_MAX = 3

Represents the size of the CollisionMode enum.

Texture2D alpha_curve 🔗

void set_alpha_curve(value: Texture2D)

Texture2D get_alpha_curve()

The alpha value of each particle's color will be multiplied by this CurveTexture over its lifetime.

Note: alpha_curve multiplies the particle mesh's vertex colors. To have a visible effect on a BaseMaterial3D, BaseMaterial3D.vertex_color_use_as_albedo must be true. For a ShaderMaterial, ALBEDO *= COLOR.rgb; must be inserted in the shader's fragment() function. Otherwise, alpha_curve will have no visible effect.

Texture2D angle_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Each particle's rotation will be animated along this CurveTexture.

float angle_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum initial rotation applied to each particle, in degrees.

Only applied when particle_flag_disable_z or particle_flag_rotate_y are true or the BaseMaterial3D being used to draw the particle is using BaseMaterial3D.BILLBOARD_PARTICLES.

float angle_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of angle_max.

Texture2D angular_velocity_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Each particle's angular velocity (rotation speed) will vary along this CurveTexture over its lifetime.

float angular_velocity_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum initial angular velocity (rotation speed) applied to each particle in degrees per second.

Only applied when particle_flag_disable_z or particle_flag_rotate_y are true or the BaseMaterial3D being used to draw the particle is using BaseMaterial3D.BILLBOARD_PARTICLES.

float angular_velocity_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of angular_velocity_max.

Texture2D anim_offset_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Each particle's animation offset will vary along this CurveTexture.

float anim_offset_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum animation offset that corresponds to frame index in the texture. 0 is the first frame, 1 is the last one. See CanvasItemMaterial.particles_animation.

float anim_offset_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of anim_offset_max.

Texture2D anim_speed_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Each particle's animation speed will vary along this CurveTexture.

float anim_speed_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum particle animation speed. Animation speed of 1 means that the particles will make full 0 to 1 offset cycle during lifetime, 2 means 2 cycles etc.

With animation speed greater than 1, remember to enable CanvasItemMaterial.particles_anim_loop property if you want the animation to repeat.

float anim_speed_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of anim_speed_max.

bool attractor_interaction_enabled = true 🔗

void set_attractor_interaction_enabled(value: bool)

bool is_attractor_interaction_enabled()

If true, interaction with particle attractors is enabled. In 3D, attraction only occurs within the area defined by the GPUParticles3D node's GPUParticles3D.visibility_aabb.

float collision_bounce 🔗

void set_collision_bounce(value: float)

float get_collision_bounce()

The particles' bounciness. Values range from 0 (no bounce) to 1 (full bounciness). Only effective if collision_mode is COLLISION_RIGID.

float collision_friction 🔗

void set_collision_friction(value: float)

float get_collision_friction()

The particles' friction. Values range from 0 (frictionless) to 1 (maximum friction). Only effective if collision_mode is COLLISION_RIGID.

CollisionMode collision_mode = 0 🔗

void set_collision_mode(value: CollisionMode)

CollisionMode get_collision_mode()

The particles' collision mode.

Note: 3D Particles can only collide with GPUParticlesCollision3D nodes, not PhysicsBody3D nodes. To make particles collide with various objects, you can add GPUParticlesCollision3D nodes as children of PhysicsBody3D nodes. In 3D, collisions only occur within the area defined by the GPUParticles3D node's GPUParticles3D.visibility_aabb.

Note: 2D Particles can only collide with LightOccluder2D nodes, not PhysicsBody2D nodes.

bool collision_use_scale = false 🔗

void set_collision_use_scale(value: bool)

bool is_collision_using_scale()

If true, GPUParticles3D.collision_base_size is multiplied by the particle's effective scale (see scale_min, scale_max, scale_curve, and scale_over_velocity_curve).

Color color = Color(1, 1, 1, 1) 🔗

void set_color(value: Color)

Each particle's initial color. If the GPUParticles2D's texture is defined, it will be multiplied by this color.

Note: color multiplies the particle mesh's vertex colors. To have a visible effect on a BaseMaterial3D, BaseMaterial3D.vertex_color_use_as_albedo must be true. For a ShaderMaterial, ALBEDO *= COLOR.rgb; must be inserted in the shader's fragment() function. Otherwise, color will have no visible effect.

Texture2D color_initial_ramp 🔗

void set_color_initial_ramp(value: Texture2D)

Texture2D get_color_initial_ramp()

Each particle's initial color will vary along this GradientTexture1D (multiplied with color).

Note: color_initial_ramp multiplies the particle mesh's vertex colors. To have a visible effect on a BaseMaterial3D, BaseMaterial3D.vertex_color_use_as_albedo must be true. For a ShaderMaterial, ALBEDO *= COLOR.rgb; must be inserted in the shader's fragment() function. Otherwise, color_initial_ramp will have no visible effect.

Texture2D color_ramp 🔗

void set_color_ramp(value: Texture2D)

Texture2D get_color_ramp()

Each particle's color will vary along this GradientTexture1D over its lifetime (multiplied with color).

Note: color_ramp multiplies the particle mesh's vertex colors. To have a visible effect on a BaseMaterial3D, BaseMaterial3D.vertex_color_use_as_albedo must be true. For a ShaderMaterial, ALBEDO *= COLOR.rgb; must be inserted in the shader's fragment() function. Otherwise, color_ramp will have no visible effect.

Texture2D damping_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Damping will vary along this CurveTexture.

float damping_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

The maximum rate at which particles lose velocity. For example value of 100 means that the particle will go from 100 velocity to 0 in 1 second.

float damping_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of damping_max.

Vector3 direction = Vector3(1, 0, 0) 🔗

void set_direction(value: Vector3)

Vector3 get_direction()

Unit vector specifying the particles' emission direction.

Texture2D directional_velocity_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

A curve that specifies the velocity along each of the axes of the particle system along its lifetime.

Note: Animated velocities will not be affected by damping, use velocity_limit_curve instead.

float directional_velocity_max 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum directional velocity value, which is multiplied by directional_velocity_curve.

Note: Animated velocities will not be affected by damping, use velocity_limit_curve instead.

float directional_velocity_min 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum directional velocity value, which is multiplied by directional_velocity_curve.

Note: Animated velocities will not be affected by damping, use velocity_limit_curve instead.

Vector3 emission_box_extents 🔗

void set_emission_box_extents(value: Vector3)

Vector3 get_emission_box_extents()

The box's extents if emission_shape is set to EMISSION_SHAPE_BOX.

Note: emission_box_extents starts from the center point and applies the X, Y, and Z values in both directions. The size is twice the area of the extents.

Texture2D emission_color_texture 🔗

void set_emission_color_texture(value: Texture2D)

Texture2D get_emission_color_texture()

Particle color will be modulated by color determined by sampling this texture at the same point as the emission_point_texture.

Note: emission_color_texture multiplies the particle mesh's vertex colors. To have a visible effect on a BaseMaterial3D, BaseMaterial3D.vertex_color_use_as_albedo must be true. For a ShaderMaterial, ALBEDO *= COLOR.rgb; must be inserted in the shader's fragment() function. Otherwise, emission_color_texture will have no visible effect.

Texture2D emission_curve 🔗

void set_emission_curve(value: Texture2D)

Texture2D get_emission_curve()

Each particle's color will be multiplied by this CurveTexture over its lifetime.

Note: emission_curve multiplies the particle mesh's vertex colors. To have a visible effect on a BaseMaterial3D, BaseMaterial3D.vertex_color_use_as_albedo must be true. For a ShaderMaterial, ALBEDO *= COLOR.rgb; must be inserted in the shader's fragment() function. Otherwise, emission_curve will have no visible effect.

Texture2D emission_normal_texture 🔗

void set_emission_normal_texture(value: Texture2D)

Texture2D get_emission_normal_texture()

Particle velocity and rotation will be set by sampling this texture at the same point as the emission_point_texture. Used only in EMISSION_SHAPE_DIRECTED_POINTS. Can be created automatically from mesh or node by selecting "Create Emission Points from Mesh/Node" under the "Particles" tool in the toolbar.

int emission_point_count 🔗

void set_emission_point_count(value: int)

int get_emission_point_count()

The number of emission points if emission_shape is set to EMISSION_SHAPE_POINTS or EMISSION_SHAPE_DIRECTED_POINTS.

Texture2D emission_point_texture 🔗

void set_emission_point_texture(value: Texture2D)

Texture2D get_emission_point_texture()

Particles will be emitted at positions determined by sampling this texture at a random position. Used with EMISSION_SHAPE_POINTS and EMISSION_SHAPE_DIRECTED_POINTS. Can be created automatically from mesh or node by selecting "Create Emission Points from Mesh/Node" under the "Particles" tool in the toolbar.

Vector3 emission_ring_axis 🔗

void set_emission_ring_axis(value: Vector3)

Vector3 get_emission_ring_axis()

The axis of the ring when using the emitter EMISSION_SHAPE_RING.

float emission_ring_cone_angle 🔗

void set_emission_ring_cone_angle(value: float)

float get_emission_ring_cone_angle()

The angle of the cone when using the emitter EMISSION_SHAPE_RING. The default angle of 90 degrees results in a ring, while an angle of 0 degrees results in a cone. Intermediate values will result in a ring where one end is larger than the other.

Note: Depending on emission_ring_height, the angle may be clamped if the ring's end is reached to form a perfect cone.

float emission_ring_height 🔗

void set_emission_ring_height(value: float)

float get_emission_ring_height()

The height of the ring when using the emitter EMISSION_SHAPE_RING.

float emission_ring_inner_radius 🔗

void set_emission_ring_inner_radius(value: float)

float get_emission_ring_inner_radius()

The inner radius of the ring when using the emitter EMISSION_SHAPE_RING.

float emission_ring_radius 🔗

void set_emission_ring_radius(value: float)

float get_emission_ring_radius()

The radius of the ring when using the emitter EMISSION_SHAPE_RING.

EmissionShape emission_shape = 0 🔗

void set_emission_shape(value: EmissionShape)

EmissionShape get_emission_shape()

Particles will be emitted inside this region.

Vector3 emission_shape_offset = Vector3(0, 0, 0) 🔗

void set_emission_shape_offset(value: Vector3)

Vector3 get_emission_shape_offset()

The offset for the emission_shape, in local space.

Vector3 emission_shape_scale = Vector3(1, 1, 1) 🔗

void set_emission_shape_scale(value: Vector3)

Vector3 get_emission_shape_scale()

The scale of the emission_shape, in local space.

float emission_sphere_radius 🔗

void set_emission_sphere_radius(value: float)

float get_emission_sphere_radius()

The sphere's radius if emission_shape is set to EMISSION_SHAPE_SPHERE.

float flatness = 0.0 🔗

void set_flatness(value: float)

Amount of spread along the Y axis.

Vector3 gravity = Vector3(0, -9.8, 0) 🔗

void set_gravity(value: Vector3)

Vector3 get_gravity()

Gravity applied to every particle.

Texture2D hue_variation_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Each particle's hue will vary along this CurveTexture.

float hue_variation_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum initial hue variation applied to each particle. It will shift the particle color's hue.

float hue_variation_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of hue_variation_max.

float inherit_velocity_ratio = 0.0 🔗

void set_inherit_velocity_ratio(value: float)

float get_inherit_velocity_ratio()

Percentage of the velocity of the respective GPUParticles2D or GPUParticles3D inherited by each particle when spawning.

float initial_velocity_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum initial velocity magnitude for each particle. Direction comes from direction and spread.

float initial_velocity_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of initial_velocity_max.

float lifetime_randomness = 0.0 🔗

void set_lifetime_randomness(value: float)

float get_lifetime_randomness()

Particle lifetime randomness ratio. The equation for the lifetime of a particle is lifetime * (1.0 - randf() * lifetime_randomness). For example, a lifetime_randomness of 0.4 scales the lifetime between 0.6 to 1.0 of its original value.

Texture2D linear_accel_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Each particle's linear acceleration will vary along this CurveTexture.

float linear_accel_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum linear acceleration applied to each particle in the direction of motion.

float linear_accel_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of linear_accel_max.

Texture2D orbit_velocity_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Each particle's orbital velocity will vary along this CurveTexture.

Note: For 3D orbital velocity, use a CurveXYZTexture.

Note: Animated velocities will not be affected by damping, use velocity_limit_curve instead.

float orbit_velocity_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum orbital velocity applied to each particle. Makes the particles circle around origin. Specified in number of full rotations around origin per second.

Note: Animated velocities will not be affected by damping, use velocity_limit_curve instead.

float orbit_velocity_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of orbit_velocity_max.

Note: Animated velocities will not be affected by damping, use velocity_limit_curve instead.

bool particle_flag_align_y = false 🔗

void set_particle_flag(particle_flag: ParticleFlags, enable: bool)

bool get_particle_flag(particle_flag: ParticleFlags) const

Align Y axis of particle with the direction of its velocity.

bool particle_flag_damping_as_friction = false 🔗

void set_particle_flag(particle_flag: ParticleFlags, enable: bool)

bool get_particle_flag(particle_flag: ParticleFlags) const

Changes the behavior of the damping properties from a linear deceleration to a deceleration based on speed percentage.

bool particle_flag_disable_z = false 🔗

void set_particle_flag(particle_flag: ParticleFlags, enable: bool)

bool get_particle_flag(particle_flag: ParticleFlags) const

If true, particles will not move on the z axis.

bool particle_flag_rotate_y = false 🔗

void set_particle_flag(particle_flag: ParticleFlags, enable: bool)

bool get_particle_flag(particle_flag: ParticleFlags) const

If true, particles rotate around Y axis by angle_min.

Texture2D radial_accel_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Each particle's radial acceleration will vary along this CurveTexture.

float radial_accel_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum radial acceleration applied to each particle. Makes particle accelerate away from the origin or towards it if negative.

float radial_accel_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of radial_accel_max.

Texture2D radial_velocity_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

A CurveTexture that defines the velocity over the particle's lifetime away (or toward) the velocity_pivot.

Note: Animated velocities will not be affected by damping, use velocity_limit_curve instead.

float radial_velocity_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum radial velocity applied to each particle. Makes particles move away from the velocity_pivot, or toward it if negative.

Note: Animated velocities will not be affected by damping, use velocity_limit_curve instead.

float radial_velocity_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum radial velocity applied to each particle. Makes particles move away from the velocity_pivot, or toward it if negative.

Note: Animated velocities will not be affected by damping, use velocity_limit_curve instead.

Texture2D scale_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Each particle's scale will vary along this CurveTexture over its lifetime. If a CurveXYZTexture is supplied instead, the scale will be separated per-axis.

float scale_max = 1.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum initial scale applied to each particle.

float scale_min = 1.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of scale_max.

Texture2D scale_over_velocity_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Either a CurveTexture or a CurveXYZTexture that scales each particle based on its velocity.

float scale_over_velocity_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum velocity value reference for scale_over_velocity_curve.

scale_over_velocity_curve will be interpolated between scale_over_velocity_min and scale_over_velocity_max.

float scale_over_velocity_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum velocity value reference for scale_over_velocity_curve.

scale_over_velocity_curve will be interpolated between scale_over_velocity_min and scale_over_velocity_max.

float spread = 45.0 🔗

void set_spread(value: float)

Each particle's initial direction range from +spread to -spread degrees.

int sub_emitter_amount_at_collision 🔗

void set_sub_emitter_amount_at_collision(value: int)

int get_sub_emitter_amount_at_collision()

The amount of particles to spawn from the subemitter node when a collision occurs. When combined with COLLISION_HIDE_ON_CONTACT on the main particles material, this can be used to achieve effects such as raindrops hitting the ground.

Note: This value shouldn't exceed GPUParticles2D.amount or GPUParticles3D.amount defined on the subemitter node (not the main node), relative to the subemitter's particle lifetime. If the number of particles is exceeded, no new particles will spawn from the subemitter until enough particles have expired.

int sub_emitter_amount_at_end 🔗

void set_sub_emitter_amount_at_end(value: int)

int get_sub_emitter_amount_at_end()

The amount of particles to spawn from the subemitter node when the particle expires.

Note: This value shouldn't exceed GPUParticles2D.amount or GPUParticles3D.amount defined on the subemitter node (not the main node), relative to the subemitter's particle lifetime. If the number of particles is exceeded, no new particles will spawn from the subemitter until enough particles have expired.

int sub_emitter_amount_at_start 🔗

void set_sub_emitter_amount_at_start(value: int)

int get_sub_emitter_amount_at_start()

The amount of particles to spawn from the subemitter node when the particle spawns.

Note: This value shouldn't exceed GPUParticles2D.amount or GPUParticles3D.amount defined on the subemitter node (not the main node), relative to the subemitter's particle lifetime. If the number of particles is exceeded, no new particles will spawn from the subemitter until enough particles have expired.

float sub_emitter_frequency 🔗

void set_sub_emitter_frequency(value: float)

float get_sub_emitter_frequency()

The frequency at which particles should be emitted from the subemitter node. One particle will be spawned every sub_emitter_frequency seconds.

Note: This value shouldn't exceed GPUParticles2D.amount or GPUParticles3D.amount defined on the subemitter node (not the main node), relative to the subemitter's particle lifetime. If the number of particles is exceeded, no new particles will spawn from the subemitter until enough particles have expired.

bool sub_emitter_keep_velocity = false 🔗

void set_sub_emitter_keep_velocity(value: bool)

bool get_sub_emitter_keep_velocity()

If true, the subemitter inherits the parent particle's velocity when it spawns.

SubEmitterMode sub_emitter_mode = 0 🔗

void set_sub_emitter_mode(value: SubEmitterMode)

SubEmitterMode get_sub_emitter_mode()

The particle subemitter mode (see GPUParticles2D.sub_emitter and GPUParticles3D.sub_emitter).

Texture2D tangential_accel_curve 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Each particle's tangential acceleration will vary along this CurveTexture.

float tangential_accel_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum tangential acceleration applied to each particle. Tangential acceleration is perpendicular to the particle's velocity giving the particles a swirling motion.

float tangential_accel_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum equivalent of tangential_accel_max.

bool turbulence_enabled = false 🔗

void set_turbulence_enabled(value: bool)

bool get_turbulence_enabled()

If true, enables turbulence for the particle system. Turbulence can be used to vary particle movement according to its position (based on a 3D noise pattern). In 3D, GPUParticlesAttractorVectorField3D with NoiseTexture3D can be used as an alternative to turbulence that works in world space and with multiple particle systems reacting in the same way.

Note: Enabling turbulence has a high performance cost on the GPU. Only enable turbulence on a few particle systems at once at most, and consider disabling it when targeting mobile/web platforms.

float turbulence_influence_max = 0.1 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum turbulence influence on each particle.

The actual amount of turbulence influence on each particle is calculated as a random value between turbulence_influence_min and turbulence_influence_max and multiplied by the amount of turbulence influence from turbulence_influence_over_life.

float turbulence_influence_min = 0.1 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum turbulence influence on each particle.

The actual amount of turbulence influence on each particle is calculated as a random value between turbulence_influence_min and turbulence_influence_max and multiplied by the amount of turbulence influence from turbulence_influence_over_life.

Texture2D turbulence_influence_over_life 🔗

void set_param_texture(param: Parameter, texture: Texture2D)

Texture2D get_param_texture(param: Parameter) const

Each particle's amount of turbulence will be influenced along this CurveTexture over its life time.

float turbulence_initial_displacement_max = 0.0 🔗

void set_param_max(param: Parameter, value: float)

float get_param_max(param: Parameter) const

Maximum displacement of each particle's spawn position by the turbulence.

The actual amount of displacement will be a factor of the underlying turbulence multiplied by a random value between turbulence_initial_displacement_min and turbulence_initial_displacement_max.

float turbulence_initial_displacement_min = 0.0 🔗

void set_param_min(param: Parameter, value: float)

float get_param_min(param: Parameter) const

Minimum displacement of each particle's spawn position by the turbulence.

The actual amount of displacement will be a factor of the underlying turbulence multiplied by a random value between turbulence_initial_displacement_min and turbulence_initial_displacement_max.

float turbulence_noise_scale = 9.0 🔗

void set_turbulence_noise_scale(value: float)

float get_turbulence_noise_scale()

This value controls the overall scale/frequency of the turbulence noise pattern.

A small scale will result in smaller features with more detail while a high scale will result in smoother noise with larger features.

Vector3 turbulence_noise_speed = Vector3(0, 0, 0) 🔗

void set_turbulence_noise_speed(value: Vector3)

Vector3 get_turbulence_noise_speed()

A scrolling velocity for the turbulence field. This sets a directional trend for the pattern to move in over time.

The default value of Vector3(0, 0, 0) turns off the scrolling.

float turbulence_noise_speed_random = 0.2 🔗

void set_turbulence_noise_speed_random(value: float)

float get_turbulence_noise_speed_random()

The in-place rate of change of the turbulence field. This defines how quickly the noise pattern varies over time.

A value of 0.0 will result in a fixed pattern.

float turbulence_noise_strength = 1.0 🔗

void set_turbulence_noise_strength(value: float)

float get_turbulence_noise_strength()

The turbulence noise strength. Increasing this will result in a stronger, more contrasting, flow pattern.

Texture2D velocity_limit_curve 🔗

void set_velocity_limit_curve(value: Texture2D)

Texture2D get_velocity_limit_curve()

A CurveTexture that defines the maximum velocity of a particle during its lifetime.

Vector3 velocity_pivot = Vector3(0, 0, 0) 🔗

void set_velocity_pivot(value: Vector3)

Vector3 get_velocity_pivot()

A pivot point used to calculate radial and orbital velocity of particles.

Vector2 get_param(param: Parameter) const 🔗

Returns the minimum and maximum values of the given param as a vector.

The x component of the returned vector corresponds to minimum and the y component corresponds to maximum.

float get_param_max(param: Parameter) const 🔗

Returns the maximum value range for the given parameter.

float get_param_min(param: Parameter) const 🔗

Returns the minimum value range for the given parameter.

Texture2D get_param_texture(param: Parameter) const 🔗

Returns the Texture2D used by the specified parameter.

bool get_particle_flag(particle_flag: ParticleFlags) const 🔗

Returns true if the specified particle flag is enabled.

void set_param(param: Parameter, value: Vector2) 🔗

Sets the minimum and maximum values of the given param.

The x component of the argument vector corresponds to minimum and the y component corresponds to maximum.

void set_param_max(param: Parameter, value: float) 🔗

Sets the maximum value range for the given parameter.

void set_param_min(param: Parameter, value: float) 🔗

Sets the minimum value range for the given parameter.

void set_param_texture(param: Parameter, texture: Texture2D) 🔗

Sets the Texture2D for the specified Parameter.

void set_particle_flag(particle_flag: ParticleFlags, enable: bool) 🔗

Sets the particle_flag to enable.

Please read the User-contributed notes policy before submitting a comment.

---

## PhysicalSkyMaterial

**URL:** https://docs.godotengine.org/en/stable/classes/class_physicalskymaterial.html

**Contents:**
- PhysicalSkyMaterial
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Material < Resource < RefCounted < Object

A material that defines a sky for a Sky resource by a set of physical properties.

The PhysicalSkyMaterial uses the Preetham analytic daylight model to draw a sky based on physical properties. This results in a substantially more realistic sky than the ProceduralSkyMaterial, but it is slightly slower and less flexible.

The PhysicalSkyMaterial only supports one sun. The color, energy, and direction of the sun are taken from the first DirectionalLight3D in the scene tree.

Color(0.1, 0.07, 0.034, 1)

Color(0.69, 0.729, 0.812, 1)

Color(0.3, 0.405, 0.6, 1)

float energy_multiplier = 1.0 🔗

void set_energy_multiplier(value: float)

float get_energy_multiplier()

The sky's overall brightness multiplier. Higher values result in a brighter sky.

Color ground_color = Color(0.1, 0.07, 0.034, 1) 🔗

void set_ground_color(value: Color)

Color get_ground_color()

Modulates the Color on the bottom half of the sky to represent the ground.

float mie_coefficient = 0.005 🔗

void set_mie_coefficient(value: float)

float get_mie_coefficient()

Controls the strength of Mie scattering for the sky. Mie scattering results from light colliding with larger particles (like water). On earth, Mie scattering results in a whitish color around the sun and horizon.

Color mie_color = Color(0.69, 0.729, 0.812, 1) 🔗

void set_mie_color(value: Color)

Color get_mie_color()

Controls the Color of the Mie scattering effect. While not physically accurate, this allows for the creation of alien-looking planets.

float mie_eccentricity = 0.8 🔗

void set_mie_eccentricity(value: float)

float get_mie_eccentricity()

Controls the direction of the Mie scattering. A value of 1 means that when light hits a particle it's passing through straight forward. A value of -1 means that all light is scatter backwards.

Texture2D night_sky 🔗

void set_night_sky(value: Texture2D)

Texture2D get_night_sky()

Texture2D for the night sky. This is added to the sky, so if it is bright enough, it may be visible during the day.

float rayleigh_coefficient = 2.0 🔗

void set_rayleigh_coefficient(value: float)

float get_rayleigh_coefficient()

Controls the strength of the Rayleigh scattering. Rayleigh scattering results from light colliding with small particles. It is responsible for the blue color of the sky.

Color rayleigh_color = Color(0.3, 0.405, 0.6, 1) 🔗

void set_rayleigh_color(value: Color)

Color get_rayleigh_color()

Controls the Color of the Rayleigh scattering. While not physically accurate, this allows for the creation of alien-looking planets. For example, setting this to a red Color results in a Mars-looking atmosphere with a corresponding blue sunset.

float sun_disk_scale = 1.0 🔗

void set_sun_disk_scale(value: float)

float get_sun_disk_scale()

Sets the size of the sun disk. Default value is based on Sol's perceived size from Earth.

float turbidity = 10.0 🔗

void set_turbidity(value: float)

float get_turbidity()

Sets the thickness of the atmosphere. High turbidity creates a foggy-looking atmosphere, while a low turbidity results in a clearer atmosphere.

bool use_debanding = true 🔗

void set_use_debanding(value: bool)

bool get_use_debanding()

If true, enables debanding. Debanding adds a small amount of noise which helps reduce banding that appears from the smooth changes in color in the sky.

Please read the User-contributed notes policy before submitting a comment.

---

## PlaceholderMaterial

**URL:** https://docs.godotengine.org/en/stable/classes/class_placeholdermaterial.html

**Contents:**
- PlaceholderMaterial
- Description
- User-contributed notes

Inherits: Material < Resource < RefCounted < Object

Placeholder class for a material.

This class is used when loading a project that uses a Material subclass in 2 conditions:

When running the project exported in dedicated server mode, only the texture's dimensions are kept (as they may be relied upon for gameplay purposes or positioning of other elements). This allows reducing the exported PCK's size significantly.

When this subclass is missing due to using a different engine version or build (e.g. modules disabled).

Please read the User-contributed notes policy before submitting a comment.

---

## ProceduralSkyMaterial

**URL:** https://docs.godotengine.org/en/stable/classes/class_proceduralskymaterial.html

**Contents:**
- ProceduralSkyMaterial
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Material < Resource < RefCounted < Object

A material that defines a simple sky for a Sky resource.

ProceduralSkyMaterial provides a way to create an effective background quickly by defining procedural parameters for the sun, the sky and the ground. The sky and ground are defined by a main color, a color at the horizon, and an easing curve to interpolate between them. Suns are described by a position in the sky, a color, and a max angle from the sun at which the easing curve ends. The max angle therefore defines the size of the sun in the sky.

ProceduralSkyMaterial supports up to 4 suns, using the color, and energy, direction, and angular distance of the first four DirectionalLight3D nodes in the scene. This means that the suns are defined individually by the properties of their corresponding DirectionalLight3Ds and globally by sun_angle_max and sun_curve.

ProceduralSkyMaterial uses a lightweight shader to draw the sky and is therefore suited for real-time updates. This makes it a great option for a sky that is simple and computationally cheap, but unrealistic. If you need a more realistic procedural option, use PhysicalSkyMaterial.

Color(0.2, 0.169, 0.133, 1)

ground_energy_multiplier

Color(0.6463, 0.6558, 0.6708, 1)

sky_energy_multiplier

Color(0.6463, 0.6558, 0.6708, 1)

Color(0.385, 0.454, 0.55, 1)

float energy_multiplier = 1.0 🔗

void set_energy_multiplier(value: float)

float get_energy_multiplier()

The sky's overall brightness multiplier. Higher values result in a brighter sky.

Color ground_bottom_color = Color(0.2, 0.169, 0.133, 1) 🔗

void set_ground_bottom_color(value: Color)

Color get_ground_bottom_color()

Color of the ground at the bottom. Blends with ground_horizon_color.

float ground_curve = 0.02 🔗

void set_ground_curve(value: float)

float get_ground_curve()

How quickly the ground_horizon_color fades into the ground_bottom_color.

float ground_energy_multiplier = 1.0 🔗

void set_ground_energy_multiplier(value: float)

float get_ground_energy_multiplier()

Multiplier for ground color. A higher value will make the ground brighter.

Color ground_horizon_color = Color(0.6463, 0.6558, 0.6708, 1) 🔗

void set_ground_horizon_color(value: Color)

Color get_ground_horizon_color()

Color of the ground at the horizon. Blends with ground_bottom_color.

Texture2D sky_cover 🔗

void set_sky_cover(value: Texture2D)

Texture2D get_sky_cover()

The sky cover texture to use. This texture must use an equirectangular projection (similar to PanoramaSkyMaterial). The texture's colors will be added to the existing sky color, and will be multiplied by sky_energy_multiplier and sky_cover_modulate. This is mainly suited to displaying stars at night, but it can also be used to display clouds at day or night (with a non-physically-accurate look).

Color sky_cover_modulate = Color(1, 1, 1, 1) 🔗

void set_sky_cover_modulate(value: Color)

Color get_sky_cover_modulate()

The tint to apply to the sky_cover texture. This can be used to change the sky cover's colors or opacity independently of the sky energy, which is useful for day/night or weather transitions. Only effective if a texture is defined in sky_cover.

float sky_curve = 0.15 🔗

void set_sky_curve(value: float)

float get_sky_curve()

How quickly the sky_horizon_color fades into the sky_top_color.

float sky_energy_multiplier = 1.0 🔗

void set_sky_energy_multiplier(value: float)

float get_sky_energy_multiplier()

Multiplier for sky color. A higher value will make the sky brighter.

Color sky_horizon_color = Color(0.6463, 0.6558, 0.6708, 1) 🔗

void set_sky_horizon_color(value: Color)

Color get_sky_horizon_color()

Color of the sky at the horizon. Blends with sky_top_color.

Color sky_top_color = Color(0.385, 0.454, 0.55, 1) 🔗

void set_sky_top_color(value: Color)

Color get_sky_top_color()

Color of the sky at the top. Blends with sky_horizon_color.

float sun_angle_max = 30.0 🔗

void set_sun_angle_max(value: float)

float get_sun_angle_max()

Distance from center of sun where it fades out completely.

float sun_curve = 0.15 🔗

void set_sun_curve(value: float)

float get_sun_curve()

How quickly the sun fades away between the edge of the sun disk and sun_angle_max.

bool use_debanding = true 🔗

void set_use_debanding(value: bool)

bool get_use_debanding()

If true, enables debanding. Debanding adds a small amount of noise which helps reduce banding that appears from the smooth changes in color in the sky.

Please read the User-contributed notes policy before submitting a comment.

---

## RDPipelineSpecializationConstant

**URL:** https://docs.godotengine.org/en/stable/classes/class_rdpipelinespecializationconstant.html

**Contents:**
- RDPipelineSpecializationConstant
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Pipeline specialization constant (used by RenderingDevice).

A specialization constant is a way to create additional variants of shaders without actually increasing the number of shader versions that are compiled. This allows improving performance by reducing the number of shader versions and reducing if branching, while still allowing shaders to be flexible for different use cases.

This object is used by RenderingDevice.

int constant_id = 0 🔗

void set_constant_id(value: int)

int get_constant_id()

The identifier of the specialization constant. This is a value starting from 0 and that increments for every different specialization constant for a given shader.

void set_value(value: Variant)

The specialization constant's value. Only bool, int and float types are valid for specialization constants.

Please read the User-contributed notes policy before submitting a comment.

---

## RDShaderFile

**URL:** https://docs.godotengine.org/en/stable/classes/class_rdshaderfile.html

**Contents:**
- RDShaderFile
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Compiled shader file in SPIR-V form (used by RenderingDevice). Not to be confused with Godot's own Shader.

Compiled shader file in SPIR-V form.

See also RDShaderSource. RDShaderFile is only meant to be used with the RenderingDevice API. It should not be confused with Godot's own Shader resource, which is what Godot's various nodes use for high-level shader programming.

get_spirv(version: StringName = &"") const

get_version_list() const

set_bytecode(bytecode: RDShaderSPIRV, version: StringName = &"")

String base_error = "" 🔗

void set_base_error(value: String)

String get_base_error()

The base compilation error message, which indicates errors not related to a specific shader stage if non-empty. If empty, shader compilation is not necessarily successful (check RDShaderSPIRV's error message members).

RDShaderSPIRV get_spirv(version: StringName = &"") const 🔗

Returns the SPIR-V intermediate representation for the specified shader version.

Array[StringName] get_version_list() const 🔗

Returns the list of compiled versions for this shader.

void set_bytecode(bytecode: RDShaderSPIRV, version: StringName = &"") 🔗

Sets the SPIR-V bytecode that will be compiled for the specified version.

Please read the User-contributed notes policy before submitting a comment.

---

## RDShaderSource

**URL:** https://docs.godotengine.org/en/stable/classes/class_rdshadersource.html

**Contents:**
- RDShaderSource
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Shader source code (used by RenderingDevice).

Shader source code in text form.

See also RDShaderFile. RDShaderSource is only meant to be used with the RenderingDevice API. It should not be confused with Godot's own Shader resource, which is what Godot's various nodes use for high-level shader programming.

source_tesselation_control

source_tesselation_evaluation

get_stage_source(stage: ShaderStage) const

set_stage_source(stage: ShaderStage, source: String)

ShaderLanguage language = 0 🔗

void set_language(value: ShaderLanguage)

ShaderLanguage get_language()

The language the shader is written in.

String source_compute = "" 🔗

void set_stage_source(stage: ShaderStage, source: String)

String get_stage_source(stage: ShaderStage) const

Source code for the shader's compute stage.

String source_fragment = "" 🔗

void set_stage_source(stage: ShaderStage, source: String)

String get_stage_source(stage: ShaderStage) const

Source code for the shader's fragment stage.

String source_tesselation_control = "" 🔗

void set_stage_source(stage: ShaderStage, source: String)

String get_stage_source(stage: ShaderStage) const

Source code for the shader's tessellation control stage.

String source_tesselation_evaluation = "" 🔗

void set_stage_source(stage: ShaderStage, source: String)

String get_stage_source(stage: ShaderStage) const

Source code for the shader's tessellation evaluation stage.

String source_vertex = "" 🔗

void set_stage_source(stage: ShaderStage, source: String)

String get_stage_source(stage: ShaderStage) const

Source code for the shader's vertex stage.

String get_stage_source(stage: ShaderStage) const 🔗

Returns source code for the specified shader stage. Equivalent to getting one of source_compute, source_fragment, source_tesselation_control, source_tesselation_evaluation or source_vertex.

void set_stage_source(stage: ShaderStage, source: String) 🔗

Sets source code for the specified shader stage. Equivalent to setting one of source_compute, source_fragment, source_tesselation_control, source_tesselation_evaluation or source_vertex.

Note: If you set the compute shader source code using this method directly, remember to remove the Godot-specific hint #[compute].

Please read the User-contributed notes policy before submitting a comment.

---

## RDShaderSPIRV

**URL:** https://docs.godotengine.org/en/stable/classes/class_rdshaderspirv.html

**Contents:**
- RDShaderSPIRV
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

SPIR-V intermediate representation as part of an RDShaderFile (used by RenderingDevice).

RDShaderSPIRV represents an RDShaderFile's SPIR-V code for various shader stages, as well as possible compilation error messages. SPIR-V is a low-level intermediate shader representation. This intermediate representation is not used directly by GPUs for rendering, but it can be compiled into binary shaders that GPUs can understand. Unlike compiled shaders, SPIR-V is portable across GPU models and driver versions.

This object is used by RenderingDevice.

bytecode_tesselation_control

bytecode_tesselation_evaluation

compile_error_compute

compile_error_fragment

compile_error_tesselation_control

compile_error_tesselation_evaluation

get_stage_bytecode(stage: ShaderStage) const

get_stage_compile_error(stage: ShaderStage) const

set_stage_bytecode(stage: ShaderStage, bytecode: PackedByteArray)

set_stage_compile_error(stage: ShaderStage, compile_error: String)

PackedByteArray bytecode_compute = PackedByteArray() 🔗

void set_stage_bytecode(stage: ShaderStage, bytecode: PackedByteArray)

PackedByteArray get_stage_bytecode(stage: ShaderStage) const

The SPIR-V bytecode for the compute shader stage.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedByteArray for more details.

PackedByteArray bytecode_fragment = PackedByteArray() 🔗

void set_stage_bytecode(stage: ShaderStage, bytecode: PackedByteArray)

PackedByteArray get_stage_bytecode(stage: ShaderStage) const

The SPIR-V bytecode for the fragment shader stage.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedByteArray for more details.

PackedByteArray bytecode_tesselation_control = PackedByteArray() 🔗

void set_stage_bytecode(stage: ShaderStage, bytecode: PackedByteArray)

PackedByteArray get_stage_bytecode(stage: ShaderStage) const

The SPIR-V bytecode for the tessellation control shader stage.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedByteArray for more details.

PackedByteArray bytecode_tesselation_evaluation = PackedByteArray() 🔗

void set_stage_bytecode(stage: ShaderStage, bytecode: PackedByteArray)

PackedByteArray get_stage_bytecode(stage: ShaderStage) const

The SPIR-V bytecode for the tessellation evaluation shader stage.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedByteArray for more details.

PackedByteArray bytecode_vertex = PackedByteArray() 🔗

void set_stage_bytecode(stage: ShaderStage, bytecode: PackedByteArray)

PackedByteArray get_stage_bytecode(stage: ShaderStage) const

The SPIR-V bytecode for the vertex shader stage.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedByteArray for more details.

String compile_error_compute = "" 🔗

void set_stage_compile_error(stage: ShaderStage, compile_error: String)

String get_stage_compile_error(stage: ShaderStage) const

The compilation error message for the compute shader stage (set by the SPIR-V compiler and Godot). If empty, shader compilation was successful.

String compile_error_fragment = "" 🔗

void set_stage_compile_error(stage: ShaderStage, compile_error: String)

String get_stage_compile_error(stage: ShaderStage) const

The compilation error message for the fragment shader stage (set by the SPIR-V compiler and Godot). If empty, shader compilation was successful.

String compile_error_tesselation_control = "" 🔗

void set_stage_compile_error(stage: ShaderStage, compile_error: String)

String get_stage_compile_error(stage: ShaderStage) const

The compilation error message for the tessellation control shader stage (set by the SPIR-V compiler and Godot). If empty, shader compilation was successful.

String compile_error_tesselation_evaluation = "" 🔗

void set_stage_compile_error(stage: ShaderStage, compile_error: String)

String get_stage_compile_error(stage: ShaderStage) const

The compilation error message for the tessellation evaluation shader stage (set by the SPIR-V compiler and Godot). If empty, shader compilation was successful.

String compile_error_vertex = "" 🔗

void set_stage_compile_error(stage: ShaderStage, compile_error: String)

String get_stage_compile_error(stage: ShaderStage) const

The compilation error message for the vertex shader stage (set by the SPIR-V compiler and Godot). If empty, shader compilation was successful.

PackedByteArray get_stage_bytecode(stage: ShaderStage) const 🔗

Equivalent to getting one of bytecode_compute, bytecode_fragment, bytecode_tesselation_control, bytecode_tesselation_evaluation, bytecode_vertex.

String get_stage_compile_error(stage: ShaderStage) const 🔗

Returns the compilation error message for the given shader stage. Equivalent to getting one of compile_error_compute, compile_error_fragment, compile_error_tesselation_control, compile_error_tesselation_evaluation, compile_error_vertex.

void set_stage_bytecode(stage: ShaderStage, bytecode: PackedByteArray) 🔗

Sets the SPIR-V bytecode for the given shader stage. Equivalent to setting one of bytecode_compute, bytecode_fragment, bytecode_tesselation_control, bytecode_tesselation_evaluation, bytecode_vertex.

void set_stage_compile_error(stage: ShaderStage, compile_error: String) 🔗

Sets the compilation error message for the given shader stage to compile_error. Equivalent to setting one of compile_error_compute, compile_error_fragment, compile_error_tesselation_control, compile_error_tesselation_evaluation, compile_error_vertex.

Please read the User-contributed notes policy before submitting a comment.

---

## RDUniform

**URL:** https://docs.godotengine.org/en/stable/classes/class_rduniform.html

**Contents:**
- RDUniform
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Shader uniform (used by RenderingDevice).

This object is used by RenderingDevice.

void set_binding(value: int)

The uniform's binding.

UniformType uniform_type = 3 🔗

void set_uniform_type(value: UniformType)

UniformType get_uniform_type()

The uniform's data type.

void add_id(id: RID) 🔗

Binds the given id to the uniform. The data associated with the id is then used when the uniform is passed to a shader.

Unbinds all ids currently bound to the uniform.

Array[RID] get_ids() const 🔗

Returns an array of all ids currently bound to the uniform.

Please read the User-contributed notes policy before submitting a comment.

---

## RDVertexAttribute

**URL:** https://docs.godotengine.org/en/stable/classes/class_rdvertexattribute.html

**Contents:**
- RDVertexAttribute
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Vertex attribute (used by RenderingDevice).

This object is used by RenderingDevice.

DataFormat format = 232 🔗

void set_format(value: DataFormat)

DataFormat get_format()

The way that this attribute's data is interpreted when sent to a shader.

VertexFrequency frequency = 0 🔗

void set_frequency(value: VertexFrequency)

VertexFrequency get_frequency()

The rate at which this attribute is pulled from its vertex buffer.

void set_location(value: int)

The location in the shader that this attribute is bound to.

void set_offset(value: int)

The number of bytes between the start of the vertex buffer and the first instance of this attribute.

void set_stride(value: int)

The number of bytes between the starts of consecutive instances of this attribute.

Please read the User-contributed notes policy before submitting a comment.

---

## Reducing stutter from shader (pipeline) compilations

**URL:** https://docs.godotengine.org/en/stable/tutorials/performance/pipeline_compilations.html

**Contents:**
- Reducing stutter from shader (pipeline) compilations
- Pipeline precompilation monitors
- Pipeline precompilation features
- Pipeline precompilation instancing
- Shader baker
- User-contributed notes

Pipeline compilation, also commonly known as shader compilation, is an expensive operation required by the engine to be able to draw any kind of content with the GPU.

Shaders and materials in Godot go through several steps before they can be run by the GPU.

In more precise terms, shader compilation involves the translation of the GLSL code that Godot generates into an intermediate format that can be shared across systems (such as SPIR-V when using Vulkan). However, this format can't be used by the GPU directly.

Pipeline compilation is the step where the GPU driver converts the intermediate shader format (the result from shader compilation) to something the GPU can actually use for rendering. Drivers usually keep a cache of pipelines stored somewhere in the system to avoid repeating the process every time a game is run. This cache is usually deleted when the driver is updated.

Pipelines contain more information than just the shader code, which means that for each shader, there can be dozens of pipelines or more! This makes it difficult for an engine to compile them ahead of time, both because it would be very slow, and because it would take up a lot of memory. On top of that, this step can only be performed on the user's system and it is very tough to share the result between users unless they have the exact same hardware and driver version.

Before Godot 4.4, there was no solution to pipeline compilation other than generating them when an object shows up inside the camera's view, leading to the infamous shader stutter or hitches that only occur during the first playthrough. With Godot 4.4, new mechanisms have been introduced to mitigate stutters from pipeline compilation.

Ubershaders: Godot makes use of specialization constants, a feature that allows the driver to optimize a pipeline's code around a set of parameters such as lighting, shadow quality, etc. Specialization constants are used to optimize a shader by limiting unnecessary features. Changing a specialization constant requires recompiling the pipeline. Ubershaders are a special version of the shader that are able to change these constants while rendering, which means Godot can precompile just one pipeline ahead of time and compile the more optimized versions on the background during gameplay. This reduces the amount of pipelines that need to be created significantly.

Pipeline precompilation: By using ubershaders, the engine can precompile pipelines ahead of time in multiple places such as when meshes are loaded or when nodes are added to the scene. By being part of the resource loading process, pipelines can even be precompiled in multiple background threads if possible during loading screens or even gameplay.

Starting in Godot 4.4, Godot will detect which pipelines are needed and precompile them at load-time. This detection system is mostly automatic, but it relies on the RenderingServer seeing evidence of all shaders, meshes, or rendering features at load-time. For example, if you load a mesh and shader while the game is running, the pipeline for that mesh/shader combination won't be compiled until the mesh/shader is loaded. Similarly, things like enabling MSAA, or instancing a VoxelGI node while the game is running will trigger pipeline recompilations.

Compiling pipelines ahead of time is the main mechanism Godot uses to mitigate shader stutters, but it's not a perfect solution. Being aware of the situations that can lead to pipeline stutters can be very helpful, and the workarounds are pretty straightforward compared to previous versions. These workarounds may be less necessary over time with future versions of Godot as more detection techniques are implemented.

The Godot debugger offers monitors for tracking the amount of pipelines created by the game and the step that triggered their compilation. You can keep an eye on these monitors as the game runs to identify potential sources of shader stutters without having to wipe your driver cache every time you wish to test. Sudden increases of these values outside of loading screens can show up as hitches during gameplay the first time someone plays the game on their system. It is recommended you take a look at these monitors to identify possible sources of stutter for your players, as you might be unable to experience them yourself without deleting your driver cache or testing on a weaker system.

Pipeline compilations of one of the demo projects.

We can see the pipelines compiled during gameplay and verify which steps could possibly cause stuttters. Note that these values will only increase and never go down, as deleted pipelines are not tracked by these monitors and pipelines may be erased and recreated during gameplay.

Canvas: Compiled when drawing a 2D node. The engine does not currently feature precompilation for 2D elements and stutters will show up when the 2D node is drawn for the first time.

Mesh: Compiled as part of loading a 3D mesh and identifying what pipelines can be precompiled from its properties. These can lead to stutters if a mesh is loaded during gameplay, but they can be mitigated if the mesh is loaded by using a background thread. Modifiers that are part of nodes such as material overrides can't be compiled on this step.

Surface: Compiled when a frame is about to be drawn and 3D objects were instanced on the scene tree for the first time. This can also include compilation for nodes that aren't even visible on the scene tree. The stutter will occur only on the first frame the node is added to the scene, which won't result in an obvious stutter if it happens right after a loading screen.

Draw: Compiled on demand when a 3D object needs to be drawn and an ubershader was not precompiled ahead of time. The engine is unable to precompile this pipeline due to triggering a case that hasn't been covered yet or a modification that was done to the engine's code. Leads to stutters during gameplay. This is identical to Godot versions before 4.4. If you see compilations here, please let the developers know <https://github.com/godotengine/godot/issues> as this should never happen with the Ubershader system. Make sure to attach a minimal reproduction project when doing so.

Specialization: Compiled in the background during gameplay to optimize the framerate. Unable to cause stutters, but may result in reduced framerates if there are many happening per frame.

Godot offers a lot of rendering features that are not necessarily used by every game. Unfortunately, pipeline precompilation can't know ahead of time if a particular feature is used by a project. Some of these features can only be detected when a user adds a node to the scene or toggles a particular setting in the project or the environment. The pipeline precompilation system will keep track of these features as they're encountered for the first time and enable precompilation of them for any meshes or surfaces that are created afterwards.

If your game makes use of these features, make sure to have a scene that uses them as early as possible before loading the majority of the assets. This scene can be very simple and will do the job as long as it uses the features the game plans to use. It can even be rendered off-screen for at least one frame if necessary, e.g. by covering it with a ColorRect node or using a SubViewport located outside the window bounds.

You should also keep in mind that changing any of these features during gameplay will result in immediate stutters. Make sure to only change these features from configuration screens if necessary and insert loading screens and messages when the changes are applied.

MSAA Level: Enabled when the level of 3D MSAA is changed on the project settings. Unfortunately, different MSAA levels being used on different viewports will lead to stutters as the engine only keeps track of one level at a time to perform precompilation.

Reflection Probes: Enabled when a ReflectionProbe node is placed on the scene.

Separate Specular: Enabled when using effects like sub-surface scattering or a compositor effect that relies on sampling the specularity directly off the screen.

Motion Vectors: Enabled when using effects such as TAA, FSR2 or a compositor effect that requires motion vectors (such as motion blur).

Normal and Roughness: Enabled when using SDFGI, VoxelGI, screen-space reflections, SSAO, SSIL, or using the normal_roughness_buffer in a custom shader or CompositorEffect.

Lightmaps: Enabled when a LightmapGI node is placed on the scene and a node uses a baked lightmap.

VoxelGI: Enabled when a VoxelGI node is placed on the scene.

SDFGI: Enabled when the WorldEnvironment enables SDFGI.

Multiview: Enabled for XR projects.

16/32-bit Shadows: Enabled when the configuration of the depth precision of shadowmaps is changed on the project settings.

Omni Shadow Dual Paraboloid: Enabled when an omni light casts shadows and uses the dual paraboloid mode.

Omni Shadow Cubemap: Enabled when an omni light casts shadows and uses the cubemap mode (which is the default).

If you witness stutters during gameplay and the monitors report a sudden increase in compilations during the Surface step, it is very likely a feature was not enabled ahead of time. Ensuring that this effect is enabled while loading your game will likely mitigate the issue.

One common source of stutters in games is the fact that some effects are only instanced on the scene because of interactions that only happen during gameplay. For example, if you have a particle effect that is only added to the scene through a script when a player does an action. Even if the scene is preloaded, the engine might be unable to precompile the pipelines until the effect is added to the scene at least once.

Luckily, it's possible for Godot 4.4 and later to precompile these pipelines as long as the scene is instantiated at least once on the scene, even if it's completely invisible or outside of the camera's view.

Hidden bullet node attached to the player in one of the demo projects. This helps the engine precompile the effect's pipelines ahead of time.

If you're aware of any effects that are added to the scene dynamically during gameplay and are seeing sudden increases on the compilations monitor when these effects show up, a workaround is to attach a hidden version of the effect somewhere that is guaranteed to show up.

For example, if the player character is able to cause some sort of explosion, you can attach the effect as a child of the player as an invisible node. Make sure to disable the script attached to the hidden node or to hide any other nodes that could cause issues, which can be done by enabling Editable Children on the node.

Since Godot 4.5, you can choose to bake shaders on export to improve initial startup time. This will generally not resolve existing stutters, but it will reduce the time it takes to load the game for the first time. This is especially the case when using Direct3D 12 or Metal, which have significantly slower initial shader compilation times than Vulkan due to the conversion step required. Godot's own shaders use GLSL and SPIR-V, but Direct3D 12 and Metal use different formats.

The shader baker can only bake the source into the intermediate format (SPIR-V for Vulkan, DXIL for Direct3D 12, MIL for Metal). It cannot bake the intermediate format into the final pipeline, as this is dependent on the GPU driver and the hardware.

The shader baker is not a replacement for pipeline precompilation, but it aims to complement it.

When enabled, the shader baker will bundle compiled shader code into the PCK, which results in the shader compilation step being skipped entirely. The downside is that exporting will take slightly longer. The PCK file will be larger by a few megabytes.

The shader baker is disabled by default, but you can enable it in each export preset in the Export dialog by ticking the Shader Baker > Enabled export option.

Note that shader baking will only be able to export shaders for drivers supported by the platform the editor is currently running on:

The editor running on Windows can export shaders for Vulkan and Direct3D 12.

The editor running on macOS can export shaders for Vulkan and Metal.

The editor running on Linux can export shaders for Vulkan only.

The editor running on Android can export shaders for Vulkan only.

The shader baker will only export shaders that match the rendering/rendering_device/driver project setting for the target platform.

The shader baker is only supported for the Forward+ and Mobile renderers. It will have no effect if the project uses the Compatibility renderer, or for users who make use of the Compatibility fallback due to their hardware not supporting the Forward+ or Mobile renderer.

This also means the shader baker is not supported on the web platform, as the web platform only supports the Compatibility renderer.

Please read the User-contributed notes policy before submitting a comment.

---

## ReflectionProbe

**URL:** https://docs.godotengine.org/en/stable/classes/class_reflectionprobe.html

**Contents:**
- ReflectionProbe
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualInstance3D < Node3D < Node < Object

Captures its surroundings to create fast, accurate reflections from a given point.

Captures its surroundings as a cubemap, and stores versions of it with increasing levels of blur to simulate different material roughnesses.

The ReflectionProbe is used to create high-quality reflections at a low performance cost (when update_mode is UPDATE_ONCE). ReflectionProbes can be blended together and with the rest of the scene smoothly. ReflectionProbes can also be combined with VoxelGI, SDFGI (Environment.sdfgi_enabled) and screen-space reflections (Environment.ssr_enabled) to get more accurate reflections in specific areas. ReflectionProbes render all objects within their cull_mask, so updating them can be quite expensive. It is best to update them once with the important static objects and then leave them as-is.

Note: Unlike VoxelGI and SDFGI, ReflectionProbes only source their environment from a WorldEnvironment node. If you specify an Environment resource within a Camera3D node, it will be ignored by the ReflectionProbe. This can lead to incorrect lighting within the ReflectionProbe.

Note: When using the Mobile rendering method, only 8 reflection probes can be displayed on each mesh resource, while the Compatibility rendering method only supports up to 2 reflection probes on each mesh. Attempting to display more than 8 reflection probes on a single mesh resource using the Mobile renderer will result in reflection probes flickering in and out as the camera moves, while the Compatibility renderer will not render any additional probes if more than 2 reflection probes are being used.

Note: When using the Mobile rendering method, reflection probes will only correctly affect meshes whose visibility AABB intersects with the reflection probe's AABB. If using a shader to deform the mesh in a way that makes it go outside its AABB, GeometryInstance3D.extra_cull_margin must be increased on the mesh. Otherwise, the reflection probe may not be visible on the mesh.

UpdateMode UPDATE_ONCE = 0

Update the probe once on the next frame (recommended for most objects). The corresponding radiance map will be generated over the following six frames. This takes more time to update than UPDATE_ALWAYS, but it has a lower performance cost and can result in higher-quality reflections. The ReflectionProbe is updated when its transform changes, but not when nearby geometry changes. You can force a ReflectionProbe update by moving the ReflectionProbe slightly in any direction.

UpdateMode UPDATE_ALWAYS = 1

Update the probe every frame. This provides better results for fast-moving dynamic objects (such as cars). However, it has a significant performance cost. Due to the cost, it's recommended to only use one ReflectionProbe with UPDATE_ALWAYS at most per scene. For all other use cases, use UPDATE_ONCE.

AmbientMode AMBIENT_DISABLED = 0

Do not apply any ambient lighting inside the ReflectionProbe's box defined by its size.

AmbientMode AMBIENT_ENVIRONMENT = 1

Apply automatically-sourced environment lighting inside the ReflectionProbe's box defined by its size.

AmbientMode AMBIENT_COLOR = 2

Apply custom ambient lighting inside the ReflectionProbe's box defined by its size. See ambient_color and ambient_color_energy.

Color ambient_color = Color(0, 0, 0, 1) 🔗

void set_ambient_color(value: Color)

Color get_ambient_color()

The custom ambient color to use within the ReflectionProbe's box defined by its size. Only effective if ambient_mode is AMBIENT_COLOR.

float ambient_color_energy = 1.0 🔗

void set_ambient_color_energy(value: float)

float get_ambient_color_energy()

The custom ambient color energy to use within the ReflectionProbe's box defined by its size. Only effective if ambient_mode is AMBIENT_COLOR.

AmbientMode ambient_mode = 1 🔗

void set_ambient_mode(value: AmbientMode)

AmbientMode get_ambient_mode()

The ambient color to use within the ReflectionProbe's box defined by its size. The ambient color will smoothly blend with other ReflectionProbes and the rest of the scene (outside the ReflectionProbe's box defined by its size).

float blend_distance = 1.0 🔗

void set_blend_distance(value: float)

float get_blend_distance()

Defines the distance in meters over which a probe blends into the scene.

bool box_projection = false 🔗

void set_enable_box_projection(value: bool)

bool is_box_projection_enabled()

If true, enables box projection. This makes reflections look more correct in rectangle-shaped rooms by offsetting the reflection center depending on the camera's location.

Note: To better fit rectangle-shaped rooms that are not aligned to the grid, you can rotate the ReflectionProbe node.

int cull_mask = 1048575 🔗

void set_cull_mask(value: int)

Sets the cull mask which determines what objects are drawn by this probe. Every VisualInstance3D with a layer included in this cull mask will be rendered by the probe. It is best to only include large objects which are likely to take up a lot of space in the reflection in order to save on rendering cost.

This can also be used to prevent an object from reflecting upon itself (for instance, a ReflectionProbe centered on a vehicle).

bool enable_shadows = false 🔗

void set_enable_shadows(value: bool)

bool are_shadows_enabled()

If true, computes shadows in the reflection probe. This makes the reflection probe slower to render; you may want to disable this if using the UPDATE_ALWAYS update_mode.

float intensity = 1.0 🔗

void set_intensity(value: float)

float get_intensity()

Defines the reflection intensity. Intensity modulates the strength of the reflection.

bool interior = false 🔗

void set_as_interior(value: bool)

bool is_set_as_interior()

If true, reflections will ignore sky contribution.

float max_distance = 0.0 🔗

void set_max_distance(value: float)

float get_max_distance()

The maximum distance away from the ReflectionProbe an object can be before it is culled. Decrease this to improve performance, especially when using the UPDATE_ALWAYS update_mode.

Note: The maximum reflection distance is always at least equal to the probe's extents. This means that decreasing max_distance will not always cull objects from reflections, especially if the reflection probe's box defined by its size is already large.

float mesh_lod_threshold = 1.0 🔗

void set_mesh_lod_threshold(value: float)

float get_mesh_lod_threshold()

The automatic LOD bias to use for meshes rendered within the ReflectionProbe (this is analog to Viewport.mesh_lod_threshold). Higher values will use less detailed versions of meshes that have LOD variations generated. If set to 0.0, automatic LOD is disabled. Increase mesh_lod_threshold to improve performance at the cost of geometry detail, especially when using the UPDATE_ALWAYS update_mode.

Note: mesh_lod_threshold does not affect GeometryInstance3D visibility ranges (also known as "manual" LOD or hierarchical LOD).

Vector3 origin_offset = Vector3(0, 0, 0) 🔗

void set_origin_offset(value: Vector3)

Vector3 get_origin_offset()

Sets the origin offset to be used when this ReflectionProbe is in box_projection mode. This can be set to a non-zero value to ensure a reflection fits a rectangle-shaped room, while reducing the number of objects that "get in the way" of the reflection.

int reflection_mask = 1048575 🔗

void set_reflection_mask(value: int)

int get_reflection_mask()

Sets the reflection mask which determines what objects have reflections applied from this probe. Every VisualInstance3D with a layer included in this reflection mask will have reflections applied from this probe. See also cull_mask, which can be used to exclude objects from appearing in the reflection while still making them affected by the ReflectionProbe.

Vector3 size = Vector3(20, 20, 20) 🔗

void set_size(value: Vector3)

The size of the reflection probe. The larger the size, the more space covered by the probe, which will lower the perceived resolution. It is best to keep the size only as large as you need it.

Note: To better fit areas that are not aligned to the grid, you can rotate the ReflectionProbe node.

UpdateMode update_mode = 0 🔗

void set_update_mode(value: UpdateMode)

UpdateMode get_update_mode()

Sets how frequently the ReflectionProbe is updated. Can be UPDATE_ONCE or UPDATE_ALWAYS.

Please read the User-contributed notes policy before submitting a comment.

---

## RenderData

**URL:** https://docs.godotengine.org/en/stable/classes/class_renderdata.html

**Contents:**
- RenderData
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherited By: RenderDataExtension, RenderDataRD

Abstract render data object, holds frame data related to rendering a single frame of a viewport.

Abstract render data object, exists for the duration of rendering a single viewport.

Note: This is an internal rendering server object, do not instantiate this from script.

get_camera_attributes() const

get_environment() const

get_render_scene_buffers() const

get_render_scene_data() const

RID get_camera_attributes() const 🔗

Returns the RID of the camera attributes object in the RenderingServer being used to render this viewport.

RID get_environment() const 🔗

Returns the RID of the environment object in the RenderingServer being used to render this viewport.

RenderSceneBuffers get_render_scene_buffers() const 🔗

Returns the RenderSceneBuffers object managing the scene buffers for rendering this viewport.

RenderSceneData get_render_scene_data() const 🔗

Returns the RenderSceneData object managing this frames scene data.

Please read the User-contributed notes policy before submitting a comment.

---

## RenderingDevice

**URL:** https://docs.godotengine.org/en/stable/classes/class_renderingdevice.html

**Contents:**
- RenderingDevice
- Description
- Tutorials
- Methods
- Enumerations
- Constants
- Method Descriptions
- User-contributed notes

Abstraction for working with modern low-level graphics APIs.

RenderingDevice is an abstraction for working with modern low-level graphics APIs such as Vulkan. Compared to RenderingServer (which works with Godot's own rendering subsystems), RenderingDevice is much lower-level and allows working more directly with the underlying graphics APIs. RenderingDevice is used in Godot to provide support for several modern low-level graphics APIs while reducing the amount of code duplication required. RenderingDevice can also be used in your own projects to perform things that are not exposed by RenderingServer or high-level nodes, such as using compute shaders.

On startup, Godot creates a global RenderingDevice which can be retrieved using RenderingServer.get_rendering_device(). This global RenderingDevice performs drawing to the screen.

Local RenderingDevices: Using RenderingServer.create_local_rendering_device(), you can create "secondary" rendering devices to perform drawing and GPU compute operations on separate threads.

Note: RenderingDevice assumes intermediate knowledge of modern graphics APIs such as Vulkan, Direct3D 12, Metal or WebGPU. These graphics APIs are lower-level than OpenGL or Direct3D 11, requiring you to perform what was previously done by the graphics driver itself. If you have difficulty understanding the concepts used in this class, follow the Vulkan Tutorial or Vulkan Guide. It's recommended to have existing modern OpenGL or Direct3D 11 knowledge before attempting to learn a low-level graphics API.

Note: RenderingDevice is not available when running in headless mode or when using the Compatibility rendering method.

Using compute shaders

barrier(from: BitField[BarrierMask] = 32767, to: BitField[BarrierMask] = 32767)

buffer_clear(buffer: RID, offset: int, size_bytes: int)

buffer_copy(src_buffer: RID, dst_buffer: RID, src_offset: int, dst_offset: int, size: int)

buffer_get_data(buffer: RID, offset_bytes: int = 0, size_bytes: int = 0)

buffer_get_data_async(buffer: RID, callback: Callable, offset_bytes: int = 0, size_bytes: int = 0)

buffer_get_device_address(buffer: RID)

buffer_update(buffer: RID, offset: int, size_bytes: int, data: PackedByteArray)

capture_timestamp(name: String)

compute_list_add_barrier(compute_list: int)

compute_list_bind_compute_pipeline(compute_list: int, compute_pipeline: RID)

compute_list_bind_uniform_set(compute_list: int, uniform_set: RID, set_index: int)

compute_list_dispatch(compute_list: int, x_groups: int, y_groups: int, z_groups: int)

compute_list_dispatch_indirect(compute_list: int, buffer: RID, offset: int)

compute_list_set_push_constant(compute_list: int, buffer: PackedByteArray, size_bytes: int)

compute_pipeline_create(shader: RID, specialization_constants: Array[RDPipelineSpecializationConstant] = [])

compute_pipeline_is_valid(compute_pipeline: RID)

create_local_device()

draw_command_begin_label(name: String, color: Color)

draw_command_end_label()

draw_command_insert_label(name: String, color: Color)

draw_list_begin(framebuffer: RID, draw_flags: BitField[DrawFlags] = 0, clear_color_values: PackedColorArray = PackedColorArray(), clear_depth_value: float = 1.0, clear_stencil_value: int = 0, region: Rect2 = Rect2(0, 0, 0, 0), breadcrumb: int = 0)

draw_list_begin_for_screen(screen: int = 0, clear_color: Color = Color(0, 0, 0, 1))

draw_list_begin_split(framebuffer: RID, splits: int, initial_color_action: InitialAction, final_color_action: FinalAction, initial_depth_action: InitialAction, final_depth_action: FinalAction, clear_color_values: PackedColorArray = PackedColorArray(), clear_depth: float = 1.0, clear_stencil: int = 0, region: Rect2 = Rect2(0, 0, 0, 0), storage_textures: Array[RID] = [])

draw_list_bind_index_array(draw_list: int, index_array: RID)

draw_list_bind_render_pipeline(draw_list: int, render_pipeline: RID)

draw_list_bind_uniform_set(draw_list: int, uniform_set: RID, set_index: int)

draw_list_bind_vertex_array(draw_list: int, vertex_array: RID)

draw_list_disable_scissor(draw_list: int)

draw_list_draw(draw_list: int, use_indices: bool, instances: int, procedural_vertex_count: int = 0)

draw_list_draw_indirect(draw_list: int, use_indices: bool, buffer: RID, offset: int = 0, draw_count: int = 1, stride: int = 0)

draw_list_enable_scissor(draw_list: int, rect: Rect2 = Rect2(0, 0, 0, 0))

draw_list_set_blend_constants(draw_list: int, color: Color)

draw_list_set_push_constant(draw_list: int, buffer: PackedByteArray, size_bytes: int)

draw_list_switch_to_next_pass()

draw_list_switch_to_next_pass_split(splits: int)

framebuffer_create(textures: Array[RID], validate_with_format: int = -1, view_count: int = 1)

framebuffer_create_empty(size: Vector2i, samples: TextureSamples = 0, validate_with_format: int = -1)

framebuffer_create_multipass(textures: Array[RID], passes: Array[RDFramebufferPass], validate_with_format: int = -1, view_count: int = 1)

framebuffer_format_create(attachments: Array[RDAttachmentFormat], view_count: int = 1)

framebuffer_format_create_empty(samples: TextureSamples = 0)

framebuffer_format_create_multipass(attachments: Array[RDAttachmentFormat], passes: Array[RDFramebufferPass], view_count: int = 1)

framebuffer_format_get_texture_samples(format: int, render_pass: int = 0)

framebuffer_get_format(framebuffer: RID)

framebuffer_is_valid(framebuffer: RID) const

get_captured_timestamp_cpu_time(index: int) const

get_captured_timestamp_gpu_time(index: int) const

get_captured_timestamp_name(index: int) const

get_captured_timestamps_count() const

get_captured_timestamps_frame() const

get_device_allocation_count() const

get_device_allocs_by_object_type(type: int) const

get_device_memory_by_object_type(type: int) const

get_device_name() const

get_device_pipeline_cache_uuid() const

get_device_total_memory() const

get_device_vendor_name() const

get_driver_allocation_count() const

get_driver_allocs_by_object_type(type: int) const

get_driver_and_device_memory_report() const

get_driver_memory_by_object_type(type: int) const

get_driver_resource(resource: DriverResource, rid: RID, index: int)

get_driver_total_memory() const

get_frame_delay() const

get_memory_usage(type: MemoryType) const

get_perf_report() const

get_tracked_object_name(type_index: int) const

get_tracked_object_type_count() const

has_feature(feature: Features) const

index_array_create(index_buffer: RID, index_offset: int, index_count: int)

index_buffer_create(size_indices: int, format: IndexBufferFormat, data: PackedByteArray = PackedByteArray(), use_restart_indices: bool = false, creation_bits: BitField[BufferCreationBits] = 0)

limit_get(limit: Limit) const

render_pipeline_create(shader: RID, framebuffer_format: int, vertex_format: int, primitive: RenderPrimitive, rasterization_state: RDPipelineRasterizationState, multisample_state: RDPipelineMultisampleState, stencil_state: RDPipelineDepthStencilState, color_blend_state: RDPipelineColorBlendState, dynamic_state_flags: BitField[PipelineDynamicStateFlags] = 0, for_render_pass: int = 0, specialization_constants: Array[RDPipelineSpecializationConstant] = [])

render_pipeline_is_valid(render_pipeline: RID)

sampler_create(state: RDSamplerState)

sampler_is_format_supported_for_filter(format: DataFormat, sampler_filter: SamplerFilter) const

screen_get_framebuffer_format(screen: int = 0) const

screen_get_height(screen: int = 0) const

screen_get_width(screen: int = 0) const

set_resource_name(id: RID, name: String)

shader_compile_binary_from_spirv(spirv_data: RDShaderSPIRV, name: String = "")

shader_compile_spirv_from_source(shader_source: RDShaderSource, allow_cache: bool = true)

shader_create_from_bytecode(binary_data: PackedByteArray, placeholder_rid: RID = RID())

shader_create_from_spirv(spirv_data: RDShaderSPIRV, name: String = "")

shader_create_placeholder()

shader_get_vertex_input_attribute_mask(shader: RID)

storage_buffer_create(size_bytes: int, data: PackedByteArray = PackedByteArray(), usage: BitField[StorageBufferUsage] = 0, creation_bits: BitField[BufferCreationBits] = 0)

texture_buffer_create(size_bytes: int, format: DataFormat, data: PackedByteArray = PackedByteArray())

texture_clear(texture: RID, color: Color, base_mipmap: int, mipmap_count: int, base_layer: int, layer_count: int)

texture_copy(from_texture: RID, to_texture: RID, from_pos: Vector3, to_pos: Vector3, size: Vector3, src_mipmap: int, dst_mipmap: int, src_layer: int, dst_layer: int)

texture_create(format: RDTextureFormat, view: RDTextureView, data: Array[PackedByteArray] = [])

texture_create_from_extension(type: TextureType, format: DataFormat, samples: TextureSamples, usage_flags: BitField[TextureUsageBits], image: int, width: int, height: int, depth: int, layers: int, mipmaps: int = 1)

texture_create_shared(view: RDTextureView, with_texture: RID)

texture_create_shared_from_slice(view: RDTextureView, with_texture: RID, layer: int, mipmap: int, mipmaps: int = 1, slice_type: TextureSliceType = 0)

texture_get_data(texture: RID, layer: int)

texture_get_data_async(texture: RID, layer: int, callback: Callable)

texture_get_format(texture: RID)

texture_get_native_handle(texture: RID)

texture_is_discardable(texture: RID)

texture_is_format_supported_for_usage(format: DataFormat, usage_flags: BitField[TextureUsageBits]) const

texture_is_shared(texture: RID)

texture_is_valid(texture: RID)

texture_resolve_multisample(from_texture: RID, to_texture: RID)

texture_set_discardable(texture: RID, discardable: bool)

texture_update(texture: RID, layer: int, data: PackedByteArray)

uniform_buffer_create(size_bytes: int, data: PackedByteArray = PackedByteArray(), creation_bits: BitField[BufferCreationBits] = 0)

uniform_set_create(uniforms: Array[RDUniform], shader: RID, shader_set: int)

uniform_set_is_valid(uniform_set: RID)

vertex_array_create(vertex_count: int, vertex_format: int, src_buffers: Array[RID], offsets: PackedInt64Array = PackedInt64Array())

vertex_buffer_create(size_bytes: int, data: PackedByteArray = PackedByteArray(), creation_bits: BitField[BufferCreationBits] = 0)

vertex_format_create(vertex_descriptions: Array[RDVertexAttribute])

DeviceType DEVICE_TYPE_OTHER = 0

Rendering device type does not match any of the other enum values or is unknown.

DeviceType DEVICE_TYPE_INTEGRATED_GPU = 1

Rendering device is an integrated GPU, which is typically (but not always) slower than dedicated GPUs (DEVICE_TYPE_DISCRETE_GPU). On Android and iOS, the rendering device type is always considered to be DEVICE_TYPE_INTEGRATED_GPU.

DeviceType DEVICE_TYPE_DISCRETE_GPU = 2

Rendering device is a dedicated GPU, which is typically (but not always) faster than integrated GPUs (DEVICE_TYPE_INTEGRATED_GPU).

DeviceType DEVICE_TYPE_VIRTUAL_GPU = 3

Rendering device is an emulated GPU in a virtual environment. This is typically much slower than the host GPU, which means the expected performance level on a dedicated GPU will be roughly equivalent to DEVICE_TYPE_INTEGRATED_GPU. Virtual machine GPU passthrough (such as VFIO) will not report the device type as DEVICE_TYPE_VIRTUAL_GPU. Instead, the host GPU's device type will be reported as if the GPU was not emulated.

DeviceType DEVICE_TYPE_CPU = 4

Rendering device is provided by software emulation (such as Lavapipe or SwiftShader). This is the slowest kind of rendering device available; it's typically much slower than DEVICE_TYPE_INTEGRATED_GPU.

DeviceType DEVICE_TYPE_MAX = 5

Represents the size of the DeviceType enum.

enum DriverResource: 🔗

DriverResource DRIVER_RESOURCE_LOGICAL_DEVICE = 0

Specific device object based on a physical device (rid parameter is ignored).

Vulkan: Vulkan device driver resource (VkDevice).

D3D12: D3D12 device driver resource (ID3D12Device).

Metal: Metal device driver resource (MTLDevice).

DriverResource DRIVER_RESOURCE_PHYSICAL_DEVICE = 1

Physical device the specific logical device is based on (rid parameter is ignored).

Vulkan: VkPhysicalDevice.

DriverResource DRIVER_RESOURCE_TOPMOST_OBJECT = 2

Top-most graphics API entry object (rid parameter is ignored).

DriverResource DRIVER_RESOURCE_COMMAND_QUEUE = 3

The main graphics-compute command queue (rid parameter is ignored).

Metal: MTLCommandQueue.

DriverResource DRIVER_RESOURCE_QUEUE_FAMILY = 4

The specific family the main queue belongs to (rid parameter is ignored).

Vulkan: The queue family index, a uint32_t.

DriverResource DRIVER_RESOURCE_TEXTURE = 5

DriverResource DRIVER_RESOURCE_TEXTURE_VIEW = 6

The view of an owned or shared texture.

D3D12: ID3D12Resource.

DriverResource DRIVER_RESOURCE_TEXTURE_DATA_FORMAT = 7

The native id of the data format of the texture.

DriverResource DRIVER_RESOURCE_SAMPLER = 8

DriverResource DRIVER_RESOURCE_UNIFORM_SET = 9

Vulkan: VkDescriptorSet.

DriverResource DRIVER_RESOURCE_BUFFER = 10

Buffer of any kind of (storage, vertex, etc.).

D3D12: ID3D12Resource.

DriverResource DRIVER_RESOURCE_COMPUTE_PIPELINE = 11

Metal: MTLComputePipelineState.

DriverResource DRIVER_RESOURCE_RENDER_PIPELINE = 12

Metal: MTLRenderPipelineState.

DriverResource DRIVER_RESOURCE_VULKAN_DEVICE = 0

Deprecated: Use DRIVER_RESOURCE_LOGICAL_DEVICE instead.

DriverResource DRIVER_RESOURCE_VULKAN_PHYSICAL_DEVICE = 1

Deprecated: Use DRIVER_RESOURCE_PHYSICAL_DEVICE instead.

DriverResource DRIVER_RESOURCE_VULKAN_INSTANCE = 2

Deprecated: Use DRIVER_RESOURCE_TOPMOST_OBJECT instead.

DriverResource DRIVER_RESOURCE_VULKAN_QUEUE = 3

Deprecated: Use DRIVER_RESOURCE_COMMAND_QUEUE instead.

DriverResource DRIVER_RESOURCE_VULKAN_QUEUE_FAMILY_INDEX = 4

Deprecated: Use DRIVER_RESOURCE_QUEUE_FAMILY instead.

DriverResource DRIVER_RESOURCE_VULKAN_IMAGE = 5

Deprecated: Use DRIVER_RESOURCE_TEXTURE instead.

DriverResource DRIVER_RESOURCE_VULKAN_IMAGE_VIEW = 6

Deprecated: Use DRIVER_RESOURCE_TEXTURE_VIEW instead.

DriverResource DRIVER_RESOURCE_VULKAN_IMAGE_NATIVE_TEXTURE_FORMAT = 7

Deprecated: Use DRIVER_RESOURCE_TEXTURE_DATA_FORMAT instead.

DriverResource DRIVER_RESOURCE_VULKAN_SAMPLER = 8

Deprecated: Use DRIVER_RESOURCE_SAMPLER instead.

DriverResource DRIVER_RESOURCE_VULKAN_DESCRIPTOR_SET = 9

Deprecated: Use DRIVER_RESOURCE_UNIFORM_SET instead.

DriverResource DRIVER_RESOURCE_VULKAN_BUFFER = 10

Deprecated: Use DRIVER_RESOURCE_BUFFER instead.

DriverResource DRIVER_RESOURCE_VULKAN_COMPUTE_PIPELINE = 11

Deprecated: Use DRIVER_RESOURCE_COMPUTE_PIPELINE instead.

DriverResource DRIVER_RESOURCE_VULKAN_RENDER_PIPELINE = 12

Deprecated: Use DRIVER_RESOURCE_RENDER_PIPELINE instead.

DataFormat DATA_FORMAT_R4G4_UNORM_PACK8 = 0

4-bit-per-channel red/green channel data format, packed into 8 bits. Values are in the [0.0, 1.0] range.

Note: More information on all data formats can be found on the Identification of formats section of the Vulkan specification, as well as the VkFormat enum.

DataFormat DATA_FORMAT_R4G4B4A4_UNORM_PACK16 = 1

4-bit-per-channel red/green/blue/alpha channel data format, packed into 16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_B4G4R4A4_UNORM_PACK16 = 2

4-bit-per-channel blue/green/red/alpha channel data format, packed into 16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R5G6B5_UNORM_PACK16 = 3

Red/green/blue channel data format with 5 bits of red, 6 bits of green and 5 bits of blue, packed into 16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_B5G6R5_UNORM_PACK16 = 4

Blue/green/red channel data format with 5 bits of blue, 6 bits of green and 5 bits of red, packed into 16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R5G5B5A1_UNORM_PACK16 = 5

Red/green/blue/alpha channel data format with 5 bits of red, 6 bits of green, 5 bits of blue and 1 bit of alpha, packed into 16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_B5G5R5A1_UNORM_PACK16 = 6

Blue/green/red/alpha channel data format with 5 bits of blue, 6 bits of green, 5 bits of red and 1 bit of alpha, packed into 16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_A1R5G5B5_UNORM_PACK16 = 7

Alpha/red/green/blue channel data format with 1 bit of alpha, 5 bits of red, 6 bits of green and 5 bits of blue, packed into 16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R8_UNORM = 8

8-bit-per-channel unsigned floating-point red channel data format with normalized value. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R8_SNORM = 9

8-bit-per-channel signed floating-point red channel data format with normalized value. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_R8_USCALED = 10

8-bit-per-channel unsigned floating-point red channel data format with scaled value (value is converted from integer to float). Values are in the [0.0, 255.0] range.

DataFormat DATA_FORMAT_R8_SSCALED = 11

8-bit-per-channel signed floating-point red channel data format with scaled value (value is converted from integer to float). Values are in the [-127.0, 127.0] range.

DataFormat DATA_FORMAT_R8_UINT = 12

8-bit-per-channel unsigned integer red channel data format. Values are in the [0, 255] range.

DataFormat DATA_FORMAT_R8_SINT = 13

8-bit-per-channel signed integer red channel data format. Values are in the [-127, 127] range.

DataFormat DATA_FORMAT_R8_SRGB = 14

8-bit-per-channel unsigned floating-point red channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R8G8_UNORM = 15

8-bit-per-channel unsigned floating-point red/green channel data format with normalized value. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R8G8_SNORM = 16

8-bit-per-channel signed floating-point red/green channel data format with normalized value. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_R8G8_USCALED = 17

8-bit-per-channel unsigned floating-point red/green channel data format with scaled value (value is converted from integer to float). Values are in the [0.0, 255.0] range.

DataFormat DATA_FORMAT_R8G8_SSCALED = 18

8-bit-per-channel signed floating-point red/green channel data format with scaled value (value is converted from integer to float). Values are in the [-127.0, 127.0] range.

DataFormat DATA_FORMAT_R8G8_UINT = 19

8-bit-per-channel unsigned integer red/green channel data format. Values are in the [0, 255] range.

DataFormat DATA_FORMAT_R8G8_SINT = 20

8-bit-per-channel signed integer red/green channel data format. Values are in the [-127, 127] range.

DataFormat DATA_FORMAT_R8G8_SRGB = 21

8-bit-per-channel unsigned floating-point red/green channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R8G8B8_UNORM = 22

8-bit-per-channel unsigned floating-point red/green/blue channel data format with normalized value. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R8G8B8_SNORM = 23

8-bit-per-channel signed floating-point red/green/blue channel data format with normalized value. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_R8G8B8_USCALED = 24

8-bit-per-channel unsigned floating-point red/green/blue channel data format with scaled value (value is converted from integer to float). Values are in the [0.0, 255.0] range.

DataFormat DATA_FORMAT_R8G8B8_SSCALED = 25

8-bit-per-channel signed floating-point red/green/blue channel data format with scaled value (value is converted from integer to float). Values are in the [-127.0, 127.0] range.

DataFormat DATA_FORMAT_R8G8B8_UINT = 26

8-bit-per-channel unsigned integer red/green/blue channel data format. Values are in the [0, 255] range.

DataFormat DATA_FORMAT_R8G8B8_SINT = 27

8-bit-per-channel signed integer red/green/blue channel data format. Values are in the [-127, 127] range.

DataFormat DATA_FORMAT_R8G8B8_SRGB = 28

8-bit-per-channel unsigned floating-point red/green/blue channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_B8G8R8_UNORM = 29

8-bit-per-channel unsigned floating-point blue/green/red channel data format with normalized value. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_B8G8R8_SNORM = 30

8-bit-per-channel signed floating-point blue/green/red channel data format with normalized value. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_B8G8R8_USCALED = 31

8-bit-per-channel unsigned floating-point blue/green/red channel data format with scaled value (value is converted from integer to float). Values are in the [0.0, 255.0] range.

DataFormat DATA_FORMAT_B8G8R8_SSCALED = 32

8-bit-per-channel signed floating-point blue/green/red channel data format with scaled value (value is converted from integer to float). Values are in the [-127.0, 127.0] range.

DataFormat DATA_FORMAT_B8G8R8_UINT = 33

8-bit-per-channel unsigned integer blue/green/red channel data format. Values are in the [0, 255] range.

DataFormat DATA_FORMAT_B8G8R8_SINT = 34

8-bit-per-channel signed integer blue/green/red channel data format. Values are in the [-127, 127] range.

DataFormat DATA_FORMAT_B8G8R8_SRGB = 35

8-bit-per-channel unsigned floating-point blue/green/red data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R8G8B8A8_UNORM = 36

8-bit-per-channel unsigned floating-point red/green/blue/alpha channel data format with normalized value. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R8G8B8A8_SNORM = 37

8-bit-per-channel signed floating-point red/green/blue/alpha channel data format with normalized value. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_R8G8B8A8_USCALED = 38

8-bit-per-channel unsigned floating-point red/green/blue/alpha channel data format with scaled value (value is converted from integer to float). Values are in the [0.0, 255.0] range.

DataFormat DATA_FORMAT_R8G8B8A8_SSCALED = 39

8-bit-per-channel signed floating-point red/green/blue/alpha channel data format with scaled value (value is converted from integer to float). Values are in the [-127.0, 127.0] range.

DataFormat DATA_FORMAT_R8G8B8A8_UINT = 40

8-bit-per-channel unsigned integer red/green/blue/alpha channel data format. Values are in the [0, 255] range.

DataFormat DATA_FORMAT_R8G8B8A8_SINT = 41

8-bit-per-channel signed integer red/green/blue/alpha channel data format. Values are in the [-127, 127] range.

DataFormat DATA_FORMAT_R8G8B8A8_SRGB = 42

8-bit-per-channel unsigned floating-point red/green/blue/alpha channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_B8G8R8A8_UNORM = 43

8-bit-per-channel unsigned floating-point blue/green/red/alpha channel data format with normalized value. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_B8G8R8A8_SNORM = 44

8-bit-per-channel signed floating-point blue/green/red/alpha channel data format with normalized value. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_B8G8R8A8_USCALED = 45

8-bit-per-channel unsigned floating-point blue/green/red/alpha channel data format with scaled value (value is converted from integer to float). Values are in the [0.0, 255.0] range.

DataFormat DATA_FORMAT_B8G8R8A8_SSCALED = 46

8-bit-per-channel signed floating-point blue/green/red/alpha channel data format with scaled value (value is converted from integer to float). Values are in the [-127.0, 127.0] range.

DataFormat DATA_FORMAT_B8G8R8A8_UINT = 47

8-bit-per-channel unsigned integer blue/green/red/alpha channel data format. Values are in the [0, 255] range.

DataFormat DATA_FORMAT_B8G8R8A8_SINT = 48

8-bit-per-channel signed integer blue/green/red/alpha channel data format. Values are in the [-127, 127] range.

DataFormat DATA_FORMAT_B8G8R8A8_SRGB = 49

8-bit-per-channel unsigned floating-point blue/green/red/alpha channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_A8B8G8R8_UNORM_PACK32 = 50

8-bit-per-channel unsigned floating-point alpha/red/green/blue channel data format with normalized value, packed in 32 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_A8B8G8R8_SNORM_PACK32 = 51

8-bit-per-channel signed floating-point alpha/red/green/blue channel data format with normalized value, packed in 32 bits. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_A8B8G8R8_USCALED_PACK32 = 52

8-bit-per-channel unsigned floating-point alpha/red/green/blue channel data format with scaled value (value is converted from integer to float), packed in 32 bits. Values are in the [0.0, 255.0] range.

DataFormat DATA_FORMAT_A8B8G8R8_SSCALED_PACK32 = 53

8-bit-per-channel signed floating-point alpha/red/green/blue channel data format with scaled value (value is converted from integer to float), packed in 32 bits. Values are in the [-127.0, 127.0] range.

DataFormat DATA_FORMAT_A8B8G8R8_UINT_PACK32 = 54

8-bit-per-channel unsigned integer alpha/red/green/blue channel data format, packed in 32 bits. Values are in the [0, 255] range.

DataFormat DATA_FORMAT_A8B8G8R8_SINT_PACK32 = 55

8-bit-per-channel signed integer alpha/red/green/blue channel data format, packed in 32 bits. Values are in the [-127, 127] range.

DataFormat DATA_FORMAT_A8B8G8R8_SRGB_PACK32 = 56

8-bit-per-channel unsigned floating-point alpha/red/green/blue channel data format with normalized value and non-linear sRGB encoding, packed in 32 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_A2R10G10B10_UNORM_PACK32 = 57

Unsigned floating-point alpha/red/green/blue channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of red, 10 bits of green and 10 bits of blue. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_A2R10G10B10_SNORM_PACK32 = 58

Signed floating-point alpha/red/green/blue channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of red, 10 bits of green and 10 bits of blue. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_A2R10G10B10_USCALED_PACK32 = 59

Unsigned floating-point alpha/red/green/blue channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of red, 10 bits of green and 10 bits of blue. Values are in the [0.0, 1023.0] range for red/green/blue and [0.0, 3.0] for alpha.

DataFormat DATA_FORMAT_A2R10G10B10_SSCALED_PACK32 = 60

Signed floating-point alpha/red/green/blue channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of red, 10 bits of green and 10 bits of blue. Values are in the [-511.0, 511.0] range for red/green/blue and [-1.0, 1.0] for alpha.

DataFormat DATA_FORMAT_A2R10G10B10_UINT_PACK32 = 61

Unsigned integer alpha/red/green/blue channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of red, 10 bits of green and 10 bits of blue. Values are in the [0, 1023] range for red/green/blue and [0, 3] for alpha.

DataFormat DATA_FORMAT_A2R10G10B10_SINT_PACK32 = 62

Signed integer alpha/red/green/blue channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of red, 10 bits of green and 10 bits of blue. Values are in the [-511, 511] range for red/green/blue and [-1, 1] for alpha.

DataFormat DATA_FORMAT_A2B10G10R10_UNORM_PACK32 = 63

Unsigned floating-point alpha/blue/green/red channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of blue, 10 bits of green and 10 bits of red. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_A2B10G10R10_SNORM_PACK32 = 64

Signed floating-point alpha/blue/green/red channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of blue, 10 bits of green and 10 bits of red. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_A2B10G10R10_USCALED_PACK32 = 65

Unsigned floating-point alpha/blue/green/red channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of blue, 10 bits of green and 10 bits of red. Values are in the [0.0, 1023.0] range for blue/green/red and [0.0, 3.0] for alpha.

DataFormat DATA_FORMAT_A2B10G10R10_SSCALED_PACK32 = 66

Signed floating-point alpha/blue/green/red channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of blue, 10 bits of green and 10 bits of red. Values are in the [-511.0, 511.0] range for blue/green/red and [-1.0, 1.0] for alpha.

DataFormat DATA_FORMAT_A2B10G10R10_UINT_PACK32 = 67

Unsigned integer alpha/blue/green/red channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of blue, 10 bits of green and 10 bits of red. Values are in the [0, 1023] range for blue/green/red and [0, 3] for alpha.

DataFormat DATA_FORMAT_A2B10G10R10_SINT_PACK32 = 68

Signed integer alpha/blue/green/red channel data format with normalized value, packed in 32 bits. Format contains 2 bits of alpha, 10 bits of blue, 10 bits of green and 10 bits of red. Values are in the [-511, 511] range for blue/green/red and [-1, 1] for alpha.

DataFormat DATA_FORMAT_R16_UNORM = 69

16-bit-per-channel unsigned floating-point red channel data format with normalized value. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R16_SNORM = 70

16-bit-per-channel signed floating-point red channel data format with normalized value. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_R16_USCALED = 71

16-bit-per-channel unsigned floating-point red channel data format with scaled value (value is converted from integer to float). Values are in the [0.0, 65535.0] range.

DataFormat DATA_FORMAT_R16_SSCALED = 72

16-bit-per-channel signed floating-point red channel data format with scaled value (value is converted from integer to float). Values are in the [-32767.0, 32767.0] range.

DataFormat DATA_FORMAT_R16_UINT = 73

16-bit-per-channel unsigned integer red channel data format. Values are in the [0.0, 65535] range.

DataFormat DATA_FORMAT_R16_SINT = 74

16-bit-per-channel signed integer red channel data format. Values are in the [-32767, 32767] range.

DataFormat DATA_FORMAT_R16_SFLOAT = 75

16-bit-per-channel signed floating-point red channel data format with the value stored as-is.

DataFormat DATA_FORMAT_R16G16_UNORM = 76

16-bit-per-channel unsigned floating-point red/green channel data format with normalized value. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R16G16_SNORM = 77

16-bit-per-channel signed floating-point red/green channel data format with normalized value. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_R16G16_USCALED = 78

16-bit-per-channel unsigned floating-point red/green channel data format with scaled value (value is converted from integer to float). Values are in the [0.0, 65535.0] range.

DataFormat DATA_FORMAT_R16G16_SSCALED = 79

16-bit-per-channel signed floating-point red/green channel data format with scaled value (value is converted from integer to float). Values are in the [-32767.0, 32767.0] range.

DataFormat DATA_FORMAT_R16G16_UINT = 80

16-bit-per-channel unsigned integer red/green channel data format. Values are in the [0.0, 65535] range.

DataFormat DATA_FORMAT_R16G16_SINT = 81

16-bit-per-channel signed integer red/green channel data format. Values are in the [-32767, 32767] range.

DataFormat DATA_FORMAT_R16G16_SFLOAT = 82

16-bit-per-channel signed floating-point red/green channel data format with the value stored as-is.

DataFormat DATA_FORMAT_R16G16B16_UNORM = 83

16-bit-per-channel unsigned floating-point red/green/blue channel data format with normalized value. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R16G16B16_SNORM = 84

16-bit-per-channel signed floating-point red/green/blue channel data format with normalized value. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_R16G16B16_USCALED = 85

16-bit-per-channel unsigned floating-point red/green/blue channel data format with scaled value (value is converted from integer to float). Values are in the [0.0, 65535.0] range.

DataFormat DATA_FORMAT_R16G16B16_SSCALED = 86

16-bit-per-channel signed floating-point red/green/blue channel data format with scaled value (value is converted from integer to float). Values are in the [-32767.0, 32767.0] range.

DataFormat DATA_FORMAT_R16G16B16_UINT = 87

16-bit-per-channel unsigned integer red/green/blue channel data format. Values are in the [0.0, 65535] range.

DataFormat DATA_FORMAT_R16G16B16_SINT = 88

16-bit-per-channel signed integer red/green/blue channel data format. Values are in the [-32767, 32767] range.

DataFormat DATA_FORMAT_R16G16B16_SFLOAT = 89

16-bit-per-channel signed floating-point red/green/blue channel data format with the value stored as-is.

DataFormat DATA_FORMAT_R16G16B16A16_UNORM = 90

16-bit-per-channel unsigned floating-point red/green/blue/alpha channel data format with normalized value. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R16G16B16A16_SNORM = 91

16-bit-per-channel signed floating-point red/green/blue/alpha channel data format with normalized value. Values are in the [-1.0, 1.0] range.

DataFormat DATA_FORMAT_R16G16B16A16_USCALED = 92

16-bit-per-channel unsigned floating-point red/green/blue/alpha channel data format with scaled value (value is converted from integer to float). Values are in the [0.0, 65535.0] range.

DataFormat DATA_FORMAT_R16G16B16A16_SSCALED = 93

16-bit-per-channel signed floating-point red/green/blue/alpha channel data format with scaled value (value is converted from integer to float). Values are in the [-32767.0, 32767.0] range.

DataFormat DATA_FORMAT_R16G16B16A16_UINT = 94

16-bit-per-channel unsigned integer red/green/blue/alpha channel data format. Values are in the [0.0, 65535] range.

DataFormat DATA_FORMAT_R16G16B16A16_SINT = 95

16-bit-per-channel signed integer red/green/blue/alpha channel data format. Values are in the [-32767, 32767] range.

DataFormat DATA_FORMAT_R16G16B16A16_SFLOAT = 96

16-bit-per-channel signed floating-point red/green/blue/alpha channel data format with the value stored as-is.

DataFormat DATA_FORMAT_R32_UINT = 97

32-bit-per-channel unsigned integer red channel data format. Values are in the [0, 2^32 - 1] range.

DataFormat DATA_FORMAT_R32_SINT = 98

32-bit-per-channel signed integer red channel data format. Values are in the [2^31 + 1, 2^31 - 1] range.

DataFormat DATA_FORMAT_R32_SFLOAT = 99

32-bit-per-channel signed floating-point red channel data format with the value stored as-is.

DataFormat DATA_FORMAT_R32G32_UINT = 100

32-bit-per-channel unsigned integer red/green channel data format. Values are in the [0, 2^32 - 1] range.

DataFormat DATA_FORMAT_R32G32_SINT = 101

32-bit-per-channel signed integer red/green channel data format. Values are in the [2^31 + 1, 2^31 - 1] range.

DataFormat DATA_FORMAT_R32G32_SFLOAT = 102

32-bit-per-channel signed floating-point red/green channel data format with the value stored as-is.

DataFormat DATA_FORMAT_R32G32B32_UINT = 103

32-bit-per-channel unsigned integer red/green/blue channel data format. Values are in the [0, 2^32 - 1] range.

DataFormat DATA_FORMAT_R32G32B32_SINT = 104

32-bit-per-channel signed integer red/green/blue channel data format. Values are in the [2^31 + 1, 2^31 - 1] range.

DataFormat DATA_FORMAT_R32G32B32_SFLOAT = 105

32-bit-per-channel signed floating-point red/green/blue channel data format with the value stored as-is.

DataFormat DATA_FORMAT_R32G32B32A32_UINT = 106

32-bit-per-channel unsigned integer red/green/blue/alpha channel data format. Values are in the [0, 2^32 - 1] range.

DataFormat DATA_FORMAT_R32G32B32A32_SINT = 107

32-bit-per-channel signed integer red/green/blue/alpha channel data format. Values are in the [2^31 + 1, 2^31 - 1] range.

DataFormat DATA_FORMAT_R32G32B32A32_SFLOAT = 108

32-bit-per-channel signed floating-point red/green/blue/alpha channel data format with the value stored as-is.

DataFormat DATA_FORMAT_R64_UINT = 109

64-bit-per-channel unsigned integer red channel data format. Values are in the [0, 2^64 - 1] range.

DataFormat DATA_FORMAT_R64_SINT = 110

64-bit-per-channel signed integer red channel data format. Values are in the [2^63 + 1, 2^63 - 1] range.

DataFormat DATA_FORMAT_R64_SFLOAT = 111

64-bit-per-channel signed floating-point red channel data format with the value stored as-is.

DataFormat DATA_FORMAT_R64G64_UINT = 112

64-bit-per-channel unsigned integer red/green channel data format. Values are in the [0, 2^64 - 1] range.

DataFormat DATA_FORMAT_R64G64_SINT = 113

64-bit-per-channel signed integer red/green channel data format. Values are in the [2^63 + 1, 2^63 - 1] range.

DataFormat DATA_FORMAT_R64G64_SFLOAT = 114

64-bit-per-channel signed floating-point red/green channel data format with the value stored as-is.

DataFormat DATA_FORMAT_R64G64B64_UINT = 115

64-bit-per-channel unsigned integer red/green/blue channel data format. Values are in the [0, 2^64 - 1] range.

DataFormat DATA_FORMAT_R64G64B64_SINT = 116

64-bit-per-channel signed integer red/green/blue channel data format. Values are in the [2^63 + 1, 2^63 - 1] range.

DataFormat DATA_FORMAT_R64G64B64_SFLOAT = 117

64-bit-per-channel signed floating-point red/green/blue channel data format with the value stored as-is.

DataFormat DATA_FORMAT_R64G64B64A64_UINT = 118

64-bit-per-channel unsigned integer red/green/blue/alpha channel data format. Values are in the [0, 2^64 - 1] range.

DataFormat DATA_FORMAT_R64G64B64A64_SINT = 119

64-bit-per-channel signed integer red/green/blue/alpha channel data format. Values are in the [2^63 + 1, 2^63 - 1] range.

DataFormat DATA_FORMAT_R64G64B64A64_SFLOAT = 120

64-bit-per-channel signed floating-point red/green/blue/alpha channel data format with the value stored as-is.

DataFormat DATA_FORMAT_B10G11R11_UFLOAT_PACK32 = 121

Unsigned floating-point blue/green/red data format with the value stored as-is, packed in 32 bits. The format's precision is 10 bits of blue channel, 11 bits of green channel and 11 bits of red channel.

DataFormat DATA_FORMAT_E5B9G9R9_UFLOAT_PACK32 = 122

Unsigned floating-point exposure/blue/green/red data format with the value stored as-is, packed in 32 bits. The format's precision is 5 bits of exposure, 9 bits of blue channel, 9 bits of green channel and 9 bits of red channel.

DataFormat DATA_FORMAT_D16_UNORM = 123

16-bit unsigned floating-point depth data format with normalized value. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_X8_D24_UNORM_PACK32 = 124

24-bit unsigned floating-point depth data format with normalized value, plus 8 unused bits, packed in 32 bits. Values for depth are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_D32_SFLOAT = 125

32-bit signed floating-point depth data format with the value stored as-is.

DataFormat DATA_FORMAT_S8_UINT = 126

8-bit unsigned integer stencil data format.

DataFormat DATA_FORMAT_D16_UNORM_S8_UINT = 127

16-bit unsigned floating-point depth data format with normalized value, plus 8 bits of stencil in unsigned integer format. Values for depth are in the [0.0, 1.0] range. Values for stencil are in the [0, 255] range.

DataFormat DATA_FORMAT_D24_UNORM_S8_UINT = 128

24-bit unsigned floating-point depth data format with normalized value, plus 8 bits of stencil in unsigned integer format. Values for depth are in the [0.0, 1.0] range. Values for stencil are in the [0, 255] range.

DataFormat DATA_FORMAT_D32_SFLOAT_S8_UINT = 129

32-bit signed floating-point depth data format with the value stored as-is, plus 8 bits of stencil in unsigned integer format. Values for stencil are in the [0, 255] range.

DataFormat DATA_FORMAT_BC1_RGB_UNORM_BLOCK = 130

VRAM-compressed unsigned red/green/blue channel data format with normalized value. Values are in the [0.0, 1.0] range. The format's precision is 5 bits of red channel, 6 bits of green channel and 5 bits of blue channel. Using BC1 texture compression (also known as S3TC DXT1).

DataFormat DATA_FORMAT_BC1_RGB_SRGB_BLOCK = 131

VRAM-compressed unsigned red/green/blue channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range. The format's precision is 5 bits of red channel, 6 bits of green channel and 5 bits of blue channel. Using BC1 texture compression (also known as S3TC DXT1).

DataFormat DATA_FORMAT_BC1_RGBA_UNORM_BLOCK = 132

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value. Values are in the [0.0, 1.0] range. The format's precision is 5 bits of red channel, 6 bits of green channel, 5 bits of blue channel and 1 bit of alpha channel. Using BC1 texture compression (also known as S3TC DXT1).

DataFormat DATA_FORMAT_BC1_RGBA_SRGB_BLOCK = 133

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range. The format's precision is 5 bits of red channel, 6 bits of green channel, 5 bits of blue channel and 1 bit of alpha channel. Using BC1 texture compression (also known as S3TC DXT1).

DataFormat DATA_FORMAT_BC2_UNORM_BLOCK = 134

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value. Values are in the [0.0, 1.0] range. The format's precision is 5 bits of red channel, 6 bits of green channel, 5 bits of blue channel and 4 bits of alpha channel. Using BC2 texture compression (also known as S3TC DXT3).

DataFormat DATA_FORMAT_BC2_SRGB_BLOCK = 135

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range. The format's precision is 5 bits of red channel, 6 bits of green channel, 5 bits of blue channel and 4 bits of alpha channel. Using BC2 texture compression (also known as S3TC DXT3).

DataFormat DATA_FORMAT_BC3_UNORM_BLOCK = 136

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value. Values are in the [0.0, 1.0] range. The format's precision is 5 bits of red channel, 6 bits of green channel, 5 bits of blue channel and 8 bits of alpha channel. Using BC3 texture compression (also known as S3TC DXT5).

DataFormat DATA_FORMAT_BC3_SRGB_BLOCK = 137

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range. The format's precision is 5 bits of red channel, 6 bits of green channel, 5 bits of blue channel and 8 bits of alpha channel. Using BC3 texture compression (also known as S3TC DXT5).

DataFormat DATA_FORMAT_BC4_UNORM_BLOCK = 138

VRAM-compressed unsigned red channel data format with normalized value. Values are in the [0.0, 1.0] range. The format's precision is 8 bits of red channel. Using BC4 texture compression.

DataFormat DATA_FORMAT_BC4_SNORM_BLOCK = 139

VRAM-compressed signed red channel data format with normalized value. Values are in the [-1.0, 1.0] range. The format's precision is 8 bits of red channel. Using BC4 texture compression.

DataFormat DATA_FORMAT_BC5_UNORM_BLOCK = 140

VRAM-compressed unsigned red/green channel data format with normalized value. Values are in the [0.0, 1.0] range. The format's precision is 8 bits of red channel and 8 bits of green channel. Using BC5 texture compression (also known as S3TC RGTC).

DataFormat DATA_FORMAT_BC5_SNORM_BLOCK = 141

VRAM-compressed signed red/green channel data format with normalized value. Values are in the [-1.0, 1.0] range. The format's precision is 8 bits of red channel and 8 bits of green channel. Using BC5 texture compression (also known as S3TC RGTC).

DataFormat DATA_FORMAT_BC6H_UFLOAT_BLOCK = 142

VRAM-compressed unsigned red/green/blue channel data format with the floating-point value stored as-is. The format's precision is between 10 and 13 bits for the red/green/blue channels. Using BC6H texture compression (also known as BPTC HDR).

DataFormat DATA_FORMAT_BC6H_SFLOAT_BLOCK = 143

VRAM-compressed signed red/green/blue channel data format with the floating-point value stored as-is. The format's precision is between 10 and 13 bits for the red/green/blue channels. Using BC6H texture compression (also known as BPTC HDR).

DataFormat DATA_FORMAT_BC7_UNORM_BLOCK = 144

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value. Values are in the [0.0, 1.0] range. The format's precision is between 4 and 7 bits for the red/green/blue channels and between 0 and 8 bits for the alpha channel. Also known as BPTC LDR.

DataFormat DATA_FORMAT_BC7_SRGB_BLOCK = 145

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range. The format's precision is between 4 and 7 bits for the red/green/blue channels and between 0 and 8 bits for the alpha channel. Also known as BPTC LDR.

DataFormat DATA_FORMAT_ETC2_R8G8B8_UNORM_BLOCK = 146

VRAM-compressed unsigned red/green/blue channel data format with normalized value. Values are in the [0.0, 1.0] range. Using ETC2 texture compression.

DataFormat DATA_FORMAT_ETC2_R8G8B8_SRGB_BLOCK = 147

VRAM-compressed unsigned red/green/blue channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range. Using ETC2 texture compression.

DataFormat DATA_FORMAT_ETC2_R8G8B8A1_UNORM_BLOCK = 148

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value. Values are in the [0.0, 1.0] range. Red/green/blue use 8 bit of precision each, with alpha using 1 bit of precision. Using ETC2 texture compression.

DataFormat DATA_FORMAT_ETC2_R8G8B8A1_SRGB_BLOCK = 149

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range. Red/green/blue use 8 bit of precision each, with alpha using 1 bit of precision. Using ETC2 texture compression.

DataFormat DATA_FORMAT_ETC2_R8G8B8A8_UNORM_BLOCK = 150

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value. Values are in the [0.0, 1.0] range. Red/green/blue use 8 bits of precision each, with alpha using 8 bits of precision. Using ETC2 texture compression.

DataFormat DATA_FORMAT_ETC2_R8G8B8A8_SRGB_BLOCK = 151

VRAM-compressed unsigned red/green/blue/alpha channel data format with normalized value and non-linear sRGB encoding. Values are in the [0.0, 1.0] range. Red/green/blue use 8 bits of precision each, with alpha using 8 bits of precision. Using ETC2 texture compression.

DataFormat DATA_FORMAT_EAC_R11_UNORM_BLOCK = 152

11-bit VRAM-compressed unsigned red channel data format with normalized value. Values are in the [0.0, 1.0] range. Using ETC2 texture compression.

DataFormat DATA_FORMAT_EAC_R11_SNORM_BLOCK = 153

11-bit VRAM-compressed signed red channel data format with normalized value. Values are in the [-1.0, 1.0] range. Using ETC2 texture compression.

DataFormat DATA_FORMAT_EAC_R11G11_UNORM_BLOCK = 154

11-bit VRAM-compressed unsigned red/green channel data format with normalized value. Values are in the [0.0, 1.0] range. Using ETC2 texture compression.

DataFormat DATA_FORMAT_EAC_R11G11_SNORM_BLOCK = 155

11-bit VRAM-compressed signed red/green channel data format with normalized value. Values are in the [-1.0, 1.0] range. Using ETC2 texture compression.

DataFormat DATA_FORMAT_ASTC_4x4_UNORM_BLOCK = 156

VRAM-compressed unsigned floating-point data format with normalized value, packed in 4×4 blocks (highest quality). Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_4x4_SRGB_BLOCK = 157

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 4×4 blocks (highest quality). Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_5x4_UNORM_BLOCK = 158

VRAM-compressed unsigned floating-point data format with normalized value, packed in 5×4 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_5x4_SRGB_BLOCK = 159

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 5×4 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_5x5_UNORM_BLOCK = 160

VRAM-compressed unsigned floating-point data format with normalized value, packed in 5×5 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_5x5_SRGB_BLOCK = 161

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 5×5 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_6x5_UNORM_BLOCK = 162

VRAM-compressed unsigned floating-point data format with normalized value, packed in 6×5 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_6x5_SRGB_BLOCK = 163

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 6×5 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_6x6_UNORM_BLOCK = 164

VRAM-compressed unsigned floating-point data format with normalized value, packed in 6×6 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_6x6_SRGB_BLOCK = 165

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 6×6 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_8x5_UNORM_BLOCK = 166

VRAM-compressed unsigned floating-point data format with normalized value, packed in 8×5 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_8x5_SRGB_BLOCK = 167

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 8×5 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_8x6_UNORM_BLOCK = 168

VRAM-compressed unsigned floating-point data format with normalized value, packed in 8×6 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_8x6_SRGB_BLOCK = 169

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 8×6 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_8x8_UNORM_BLOCK = 170

VRAM-compressed unsigned floating-point data format with normalized value, packed in 8×8 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_8x8_SRGB_BLOCK = 171

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 8×8 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_10x5_UNORM_BLOCK = 172

VRAM-compressed unsigned floating-point data format with normalized value, packed in 10×5 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_10x5_SRGB_BLOCK = 173

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 10×5 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_10x6_UNORM_BLOCK = 174

VRAM-compressed unsigned floating-point data format with normalized value, packed in 10×6 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_10x6_SRGB_BLOCK = 175

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 10×6 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_10x8_UNORM_BLOCK = 176

VRAM-compressed unsigned floating-point data format with normalized value, packed in 10×8 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_10x8_SRGB_BLOCK = 177

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 10×8 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_10x10_UNORM_BLOCK = 178

VRAM-compressed unsigned floating-point data format with normalized value, packed in 10×10 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_10x10_SRGB_BLOCK = 179

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 10×10 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_12x10_UNORM_BLOCK = 180

VRAM-compressed unsigned floating-point data format with normalized value, packed in 12×10 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_12x10_SRGB_BLOCK = 181

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 12×10 blocks. Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_12x12_UNORM_BLOCK = 182

VRAM-compressed unsigned floating-point data format with normalized value, packed in 12 blocks (lowest quality). Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_ASTC_12x12_SRGB_BLOCK = 183

VRAM-compressed unsigned floating-point data format with normalized value and non-linear sRGB encoding, packed in 12 blocks (lowest quality). Values are in the [0.0, 1.0] range. Using ASTC compression.

DataFormat DATA_FORMAT_G8B8G8R8_422_UNORM = 184

8-bit-per-channel unsigned floating-point green/blue/red channel data format with normalized value. Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_B8G8R8G8_422_UNORM = 185

8-bit-per-channel unsigned floating-point blue/green/red channel data format with normalized value. Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G8_B8_R8_3PLANE_420_UNORM = 186

8-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, stored across 3 separate planes (green + blue + red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal and vertical resolution (i.e. 2×2 adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G8_B8R8_2PLANE_420_UNORM = 187

8-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, stored across 2 separate planes (green + blue/red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal and vertical resolution (i.e. 2×2 adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G8_B8_R8_3PLANE_422_UNORM = 188

8-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, stored across 2 separate planes (green + blue + red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G8_B8R8_2PLANE_422_UNORM = 189

8-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, stored across 2 separate planes (green + blue/red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G8_B8_R8_3PLANE_444_UNORM = 190

8-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, stored across 3 separate planes. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R10X6_UNORM_PACK16 = 191

10-bit-per-channel unsigned floating-point red channel data with normalized value, plus 6 unused bits, packed in 16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R10X6G10X6_UNORM_2PACK16 = 192

10-bit-per-channel unsigned floating-point red/green channel data with normalized value, plus 6 unused bits after each channel, packed in 2×16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R10X6G10X6B10X6A10X6_UNORM_4PACK16 = 193

10-bit-per-channel unsigned floating-point red/green/blue/alpha channel data with normalized value, plus 6 unused bits after each channel, packed in 4×16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_G10X6B10X6G10X6R10X6_422_UNORM_4PACK16 = 194

10-bit-per-channel unsigned floating-point green/blue/green/red channel data with normalized value, plus 6 unused bits after each channel, packed in 4×16 bits. Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel). The green channel is listed twice, but contains different values to allow it to be represented at full resolution.

DataFormat DATA_FORMAT_B10X6G10X6R10X6G10X6_422_UNORM_4PACK16 = 195

10-bit-per-channel unsigned floating-point blue/green/red/green channel data with normalized value, plus 6 unused bits after each channel, packed in 4×16 bits. Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel). The green channel is listed twice, but contains different values to allow it to be represented at full resolution.

DataFormat DATA_FORMAT_G10X6_B10X6_R10X6_3PLANE_420_UNORM_3PACK16 = 196

10-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Packed in 3×16 bits and stored across 2 separate planes (green + blue + red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal and vertical resolution (i.e. 2×2 adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G10X6_B10X6R10X6_2PLANE_420_UNORM_3PACK16 = 197

10-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Packed in 3×16 bits and stored across 2 separate planes (green + blue/red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal and vertical resolution (i.e. 2×2 adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G10X6_B10X6_R10X6_3PLANE_422_UNORM_3PACK16 = 198

10-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Packed in 3×16 bits and stored across 3 separate planes (green + blue + red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G10X6_B10X6R10X6_2PLANE_422_UNORM_3PACK16 = 199

10-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Packed in 3×16 bits and stored across 3 separate planes (green + blue/red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G10X6_B10X6_R10X6_3PLANE_444_UNORM_3PACK16 = 200

10-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Packed in 3×16 bits and stored across 3 separate planes (green + blue + red). Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R12X4_UNORM_PACK16 = 201

12-bit-per-channel unsigned floating-point red channel data with normalized value, plus 6 unused bits, packed in 16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R12X4G12X4_UNORM_2PACK16 = 202

12-bit-per-channel unsigned floating-point red/green channel data with normalized value, plus 6 unused bits after each channel, packed in 2×16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_R12X4G12X4B12X4A12X4_UNORM_4PACK16 = 203

12-bit-per-channel unsigned floating-point red/green/blue/alpha channel data with normalized value, plus 6 unused bits after each channel, packed in 4×16 bits. Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_G12X4B12X4G12X4R12X4_422_UNORM_4PACK16 = 204

12-bit-per-channel unsigned floating-point green/blue/green/red channel data with normalized value, plus 6 unused bits after each channel, packed in 4×16 bits. Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel). The green channel is listed twice, but contains different values to allow it to be represented at full resolution.

DataFormat DATA_FORMAT_B12X4G12X4R12X4G12X4_422_UNORM_4PACK16 = 205

12-bit-per-channel unsigned floating-point blue/green/red/green channel data with normalized value, plus 6 unused bits after each channel, packed in 4×16 bits. Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel). The green channel is listed twice, but contains different values to allow it to be represented at full resolution.

DataFormat DATA_FORMAT_G12X4_B12X4_R12X4_3PLANE_420_UNORM_3PACK16 = 206

12-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Packed in 3×16 bits and stored across 2 separate planes (green + blue + red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal and vertical resolution (i.e. 2×2 adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G12X4_B12X4R12X4_2PLANE_420_UNORM_3PACK16 = 207

12-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Packed in 3×16 bits and stored across 2 separate planes (green + blue/red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal and vertical resolution (i.e. 2×2 adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G12X4_B12X4_R12X4_3PLANE_422_UNORM_3PACK16 = 208

12-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Packed in 3×16 bits and stored across 3 separate planes (green + blue + red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G12X4_B12X4R12X4_2PLANE_422_UNORM_3PACK16 = 209

12-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Packed in 3×16 bits and stored across 3 separate planes (green + blue/red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G12X4_B12X4_R12X4_3PLANE_444_UNORM_3PACK16 = 210

12-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Packed in 3×16 bits and stored across 3 separate planes (green + blue + red). Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_G16B16G16R16_422_UNORM = 211

16-bit-per-channel unsigned floating-point green/blue/red channel data format with normalized value. Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_B16G16R16G16_422_UNORM = 212

16-bit-per-channel unsigned floating-point blue/green/red channel data format with normalized value. Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G16_B16_R16_3PLANE_420_UNORM = 213

16-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Stored across 2 separate planes (green + blue + red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal and vertical resolution (i.e. 2×2 adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G16_B16R16_2PLANE_420_UNORM = 214

16-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Stored across 2 separate planes (green + blue/red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal and vertical resolution (i.e. 2×2 adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G16_B16_R16_3PLANE_422_UNORM = 215

16-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Stored across 3 separate planes (green + blue + red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G16_B16R16_2PLANE_422_UNORM = 216

16-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Stored across 3 separate planes (green + blue/red). Values are in the [0.0, 1.0] range. Blue and red channel data is stored at halved horizontal resolution (i.e. 2 horizontally adjacent pixels will share the same value for the blue/red channel).

DataFormat DATA_FORMAT_G16_B16_R16_3PLANE_444_UNORM = 217

16-bit-per-channel unsigned floating-point green/blue/red channel data with normalized value, plus 6 unused bits after each channel. Stored across 3 separate planes (green + blue + red). Values are in the [0.0, 1.0] range.

DataFormat DATA_FORMAT_ASTC_4x4_SFLOAT_BLOCK = 218

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_5x4_SFLOAT_BLOCK = 219

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_5x5_SFLOAT_BLOCK = 220

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_6x5_SFLOAT_BLOCK = 221

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_6x6_SFLOAT_BLOCK = 222

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_8x5_SFLOAT_BLOCK = 223

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_8x6_SFLOAT_BLOCK = 224

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_8x8_SFLOAT_BLOCK = 225

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_10x5_SFLOAT_BLOCK = 226

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_10x6_SFLOAT_BLOCK = 227

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_10x8_SFLOAT_BLOCK = 228

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_10x10_SFLOAT_BLOCK = 229

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_12x10_SFLOAT_BLOCK = 230

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_ASTC_12x12_SFLOAT_BLOCK = 231

There is currently no description for this enum. Please help us by contributing one!

DataFormat DATA_FORMAT_MAX = 232

Represents the size of the DataFormat enum.

BarrierMask BARRIER_MASK_VERTEX = 1

Vertex shader barrier mask.

BarrierMask BARRIER_MASK_FRAGMENT = 8

Fragment shader barrier mask.

BarrierMask BARRIER_MASK_COMPUTE = 2

Compute barrier mask.

BarrierMask BARRIER_MASK_TRANSFER = 4

Transfer barrier mask.

BarrierMask BARRIER_MASK_RASTER = 9

Raster barrier mask (vertex and fragment). Equivalent to BARRIER_MASK_VERTEX | BARRIER_MASK_FRAGMENT.

BarrierMask BARRIER_MASK_ALL_BARRIERS = 32767

Barrier mask for all types (vertex, fragment, compute, transfer).

BarrierMask BARRIER_MASK_NO_BARRIER = 32768

No barrier for any type.

TextureType TEXTURE_TYPE_1D = 0

1-dimensional texture.

TextureType TEXTURE_TYPE_2D = 1

2-dimensional texture.

TextureType TEXTURE_TYPE_3D = 2

3-dimensional texture.

TextureType TEXTURE_TYPE_CUBE = 3

TextureType TEXTURE_TYPE_1D_ARRAY = 4

Array of 1-dimensional textures.

TextureType TEXTURE_TYPE_2D_ARRAY = 5

Array of 2-dimensional textures.

TextureType TEXTURE_TYPE_CUBE_ARRAY = 6

Array of Cubemap textures.

TextureType TEXTURE_TYPE_MAX = 7

Represents the size of the TextureType enum.

enum TextureSamples: 🔗

TextureSamples TEXTURE_SAMPLES_1 = 0

Perform 1 texture sample (this is the fastest but lowest-quality for antialiasing).

TextureSamples TEXTURE_SAMPLES_2 = 1

Perform 2 texture samples.

TextureSamples TEXTURE_SAMPLES_4 = 2

Perform 4 texture samples.

TextureSamples TEXTURE_SAMPLES_8 = 3

Perform 8 texture samples. Not supported on mobile GPUs (including Apple Silicon).

TextureSamples TEXTURE_SAMPLES_16 = 4

Perform 16 texture samples. Not supported on mobile GPUs and many desktop GPUs.

TextureSamples TEXTURE_SAMPLES_32 = 5

Perform 32 texture samples. Not supported on most GPUs.

TextureSamples TEXTURE_SAMPLES_64 = 6

Perform 64 texture samples (this is the slowest but highest-quality for antialiasing). Not supported on most GPUs.

TextureSamples TEXTURE_SAMPLES_MAX = 7

Represents the size of the TextureSamples enum.

flags TextureUsageBits: 🔗

TextureUsageBits TEXTURE_USAGE_SAMPLING_BIT = 1

Texture can be sampled.

TextureUsageBits TEXTURE_USAGE_COLOR_ATTACHMENT_BIT = 2

Texture can be used as a color attachment in a framebuffer.

TextureUsageBits TEXTURE_USAGE_DEPTH_STENCIL_ATTACHMENT_BIT = 4

Texture can be used as a depth/stencil attachment in a framebuffer.

TextureUsageBits TEXTURE_USAGE_STORAGE_BIT = 8

Texture can be used as a storage image.

TextureUsageBits TEXTURE_USAGE_STORAGE_ATOMIC_BIT = 16

Texture can be used as a storage image with support for atomic operations.

TextureUsageBits TEXTURE_USAGE_CPU_READ_BIT = 32

Texture can be read back on the CPU using texture_get_data() faster than without this bit, since it is always kept in the system memory.

TextureUsageBits TEXTURE_USAGE_CAN_UPDATE_BIT = 64

Texture can be updated using texture_update().

TextureUsageBits TEXTURE_USAGE_CAN_COPY_FROM_BIT = 128

Texture can be a source for texture_copy().

TextureUsageBits TEXTURE_USAGE_CAN_COPY_TO_BIT = 256

Texture can be a destination for texture_copy().

TextureUsageBits TEXTURE_USAGE_INPUT_ATTACHMENT_BIT = 512

Texture can be used as a input attachment in a framebuffer.

enum TextureSwizzle: 🔗

TextureSwizzle TEXTURE_SWIZZLE_IDENTITY = 0

Return the sampled value as-is.

TextureSwizzle TEXTURE_SWIZZLE_ZERO = 1

Always return 0.0 when sampling.

TextureSwizzle TEXTURE_SWIZZLE_ONE = 2

Always return 1.0 when sampling.

TextureSwizzle TEXTURE_SWIZZLE_R = 3

Sample the red color channel.

TextureSwizzle TEXTURE_SWIZZLE_G = 4

Sample the green color channel.

TextureSwizzle TEXTURE_SWIZZLE_B = 5

Sample the blue color channel.

TextureSwizzle TEXTURE_SWIZZLE_A = 6

Sample the alpha channel.

TextureSwizzle TEXTURE_SWIZZLE_MAX = 7

Represents the size of the TextureSwizzle enum.

enum TextureSliceType: 🔗

TextureSliceType TEXTURE_SLICE_2D = 0

2-dimensional texture slice.

TextureSliceType TEXTURE_SLICE_CUBEMAP = 1

Cubemap texture slice.

TextureSliceType TEXTURE_SLICE_3D = 2

3-dimensional texture slice.

enum SamplerFilter: 🔗

SamplerFilter SAMPLER_FILTER_NEAREST = 0

Nearest-neighbor sampler filtering. Sampling at higher resolutions than the source will result in a pixelated look.

SamplerFilter SAMPLER_FILTER_LINEAR = 1

Bilinear sampler filtering. Sampling at higher resolutions than the source will result in a blurry look.

enum SamplerRepeatMode: 🔗

SamplerRepeatMode SAMPLER_REPEAT_MODE_REPEAT = 0

Sample with repeating enabled.

SamplerRepeatMode SAMPLER_REPEAT_MODE_MIRRORED_REPEAT = 1

Sample with mirrored repeating enabled. When sampling outside the [0.0, 1.0] range, return a mirrored version of the sampler. This mirrored version is mirrored again if sampling further away, with the pattern repeating indefinitely.

SamplerRepeatMode SAMPLER_REPEAT_MODE_CLAMP_TO_EDGE = 2

Sample with repeating disabled. When sampling outside the [0.0, 1.0] range, return the color of the last pixel on the edge.

SamplerRepeatMode SAMPLER_REPEAT_MODE_CLAMP_TO_BORDER = 3

Sample with repeating disabled. When sampling outside the [0.0, 1.0] range, return the specified RDSamplerState.border_color.

SamplerRepeatMode SAMPLER_REPEAT_MODE_MIRROR_CLAMP_TO_EDGE = 4

Sample with mirrored repeating enabled, but only once. When sampling in the [-1.0, 0.0] range, return a mirrored version of the sampler. When sampling outside the [-1.0, 1.0] range, return the color of the last pixel on the edge.

SamplerRepeatMode SAMPLER_REPEAT_MODE_MAX = 5

Represents the size of the SamplerRepeatMode enum.

enum SamplerBorderColor: 🔗

SamplerBorderColor SAMPLER_BORDER_COLOR_FLOAT_TRANSPARENT_BLACK = 0

Return a floating-point transparent black color when sampling outside the [0.0, 1.0] range. Only effective if the sampler repeat mode is SAMPLER_REPEAT_MODE_CLAMP_TO_BORDER.

SamplerBorderColor SAMPLER_BORDER_COLOR_INT_TRANSPARENT_BLACK = 1

Return an integer transparent black color when sampling outside the [0.0, 1.0] range. Only effective if the sampler repeat mode is SAMPLER_REPEAT_MODE_CLAMP_TO_BORDER.

SamplerBorderColor SAMPLER_BORDER_COLOR_FLOAT_OPAQUE_BLACK = 2

Return a floating-point opaque black color when sampling outside the [0.0, 1.0] range. Only effective if the sampler repeat mode is SAMPLER_REPEAT_MODE_CLAMP_TO_BORDER.

SamplerBorderColor SAMPLER_BORDER_COLOR_INT_OPAQUE_BLACK = 3

Return an integer opaque black color when sampling outside the [0.0, 1.0] range. Only effective if the sampler repeat mode is SAMPLER_REPEAT_MODE_CLAMP_TO_BORDER.

SamplerBorderColor SAMPLER_BORDER_COLOR_FLOAT_OPAQUE_WHITE = 4

Return a floating-point opaque white color when sampling outside the [0.0, 1.0] range. Only effective if the sampler repeat mode is SAMPLER_REPEAT_MODE_CLAMP_TO_BORDER.

SamplerBorderColor SAMPLER_BORDER_COLOR_INT_OPAQUE_WHITE = 5

Return an integer opaque white color when sampling outside the [0.0, 1.0] range. Only effective if the sampler repeat mode is SAMPLER_REPEAT_MODE_CLAMP_TO_BORDER.

SamplerBorderColor SAMPLER_BORDER_COLOR_MAX = 6

Represents the size of the SamplerBorderColor enum.

enum VertexFrequency: 🔗

VertexFrequency VERTEX_FREQUENCY_VERTEX = 0

Vertex attribute addressing is a function of the vertex. This is used to specify the rate at which vertex attributes are pulled from buffers.

VertexFrequency VERTEX_FREQUENCY_INSTANCE = 1

Vertex attribute addressing is a function of the instance index. This is used to specify the rate at which vertex attributes are pulled from buffers.

enum IndexBufferFormat: 🔗

IndexBufferFormat INDEX_BUFFER_FORMAT_UINT16 = 0

Index buffer in 16-bit unsigned integer format. This limits the maximum index that can be specified to 65535.

IndexBufferFormat INDEX_BUFFER_FORMAT_UINT32 = 1

Index buffer in 32-bit unsigned integer format. This limits the maximum index that can be specified to 4294967295.

flags StorageBufferUsage: 🔗

StorageBufferUsage STORAGE_BUFFER_USAGE_DISPATCH_INDIRECT = 1

There is currently no description for this enum. Please help us by contributing one!

flags BufferCreationBits: 🔗

BufferCreationBits BUFFER_CREATION_DEVICE_ADDRESS_BIT = 1

Optionally, set this flag if you wish to use buffer_get_device_address() functionality. You must first check the GPU supports it:

BufferCreationBits BUFFER_CREATION_AS_STORAGE_BIT = 2

Set this flag so that it is created as storage. This is useful if Compute Shaders need access (for reading or writing) to the buffer, e.g. skeletal animations are processed in Compute Shaders which need access to vertex buffers, to be later consumed by vertex shaders as part of the regular rasterization pipeline.

UniformType UNIFORM_TYPE_SAMPLER = 0

UniformType UNIFORM_TYPE_SAMPLER_WITH_TEXTURE = 1

Sampler uniform with a texture.

UniformType UNIFORM_TYPE_TEXTURE = 2

UniformType UNIFORM_TYPE_IMAGE = 3

UniformType UNIFORM_TYPE_TEXTURE_BUFFER = 4

Texture buffer uniform.

UniformType UNIFORM_TYPE_SAMPLER_WITH_TEXTURE_BUFFER = 5

Sampler uniform with a texture buffer.

UniformType UNIFORM_TYPE_IMAGE_BUFFER = 6

Image buffer uniform.

UniformType UNIFORM_TYPE_UNIFORM_BUFFER = 7

Uniform buffer uniform.

UniformType UNIFORM_TYPE_STORAGE_BUFFER = 8

Storage buffer uniform.

UniformType UNIFORM_TYPE_INPUT_ATTACHMENT = 9

Input attachment uniform.

UniformType UNIFORM_TYPE_MAX = 10

Represents the size of the UniformType enum.

enum RenderPrimitive: 🔗

RenderPrimitive RENDER_PRIMITIVE_POINTS = 0

Point rendering primitive (with constant size, regardless of distance from camera).

RenderPrimitive RENDER_PRIMITIVE_LINES = 1

Line list rendering primitive. Lines are drawn separated from each other.

RenderPrimitive RENDER_PRIMITIVE_LINES_WITH_ADJACENCY = 2

Line list rendering primitive with adjacency.

Note: Adjacency is only useful with geometry shaders, which Godot does not expose.

RenderPrimitive RENDER_PRIMITIVE_LINESTRIPS = 3

Line strip rendering primitive. Lines drawn are connected to the previous vertex.

RenderPrimitive RENDER_PRIMITIVE_LINESTRIPS_WITH_ADJACENCY = 4

Line strip rendering primitive with adjacency.

Note: Adjacency is only useful with geometry shaders, which Godot does not expose.

RenderPrimitive RENDER_PRIMITIVE_TRIANGLES = 5

Triangle list rendering primitive. Triangles are drawn separated from each other.

RenderPrimitive RENDER_PRIMITIVE_TRIANGLES_WITH_ADJACENCY = 6

Triangle list rendering primitive with adjacency.

Note: Adjacency is only useful with geometry shaders, which Godot does not expose.

RenderPrimitive RENDER_PRIMITIVE_TRIANGLE_STRIPS = 7

Triangle strip rendering primitive. Triangles drawn are connected to the previous triangle.

RenderPrimitive RENDER_PRIMITIVE_TRIANGLE_STRIPS_WITH_AJACENCY = 8

Triangle strip rendering primitive with adjacency.

Note: Adjacency is only useful with geometry shaders, which Godot does not expose.

RenderPrimitive RENDER_PRIMITIVE_TRIANGLE_STRIPS_WITH_RESTART_INDEX = 9

Triangle strip rendering primitive with primitive restart enabled. Triangles drawn are connected to the previous triangle, but a primitive restart index can be specified before drawing to create a second triangle strip after the specified index.

Note: Only compatible with indexed draws.

RenderPrimitive RENDER_PRIMITIVE_TESSELATION_PATCH = 10

Tessellation patch rendering primitive. Only useful with tessellation shaders, which can be used to deform these patches.

RenderPrimitive RENDER_PRIMITIVE_MAX = 11

Represents the size of the RenderPrimitive enum.

enum PolygonCullMode: 🔗

PolygonCullMode POLYGON_CULL_DISABLED = 0

Do not use polygon front face or backface culling.

PolygonCullMode POLYGON_CULL_FRONT = 1

Use polygon frontface culling (faces pointing towards the camera are hidden).

PolygonCullMode POLYGON_CULL_BACK = 2

Use polygon backface culling (faces pointing away from the camera are hidden).

enum PolygonFrontFace: 🔗

PolygonFrontFace POLYGON_FRONT_FACE_CLOCKWISE = 0

Clockwise winding order to determine which face of a polygon is its front face.

PolygonFrontFace POLYGON_FRONT_FACE_COUNTER_CLOCKWISE = 1

Counter-clockwise winding order to determine which face of a polygon is its front face.

enum StencilOperation: 🔗

StencilOperation STENCIL_OP_KEEP = 0

Keep the current stencil value.

StencilOperation STENCIL_OP_ZERO = 1

Set the stencil value to 0.

StencilOperation STENCIL_OP_REPLACE = 2

Replace the existing stencil value with the new one.

StencilOperation STENCIL_OP_INCREMENT_AND_CLAMP = 3

Increment the existing stencil value and clamp to the maximum representable unsigned value if reached. Stencil bits are considered as an unsigned integer.

StencilOperation STENCIL_OP_DECREMENT_AND_CLAMP = 4

Decrement the existing stencil value and clamp to the minimum value if reached. Stencil bits are considered as an unsigned integer.

StencilOperation STENCIL_OP_INVERT = 5

Bitwise-invert the existing stencil value.

StencilOperation STENCIL_OP_INCREMENT_AND_WRAP = 6

Increment the stencil value and wrap around to 0 if reaching the maximum representable unsigned. Stencil bits are considered as an unsigned integer.

StencilOperation STENCIL_OP_DECREMENT_AND_WRAP = 7

Decrement the stencil value and wrap around to the maximum representable unsigned if reaching the minimum. Stencil bits are considered as an unsigned integer.

StencilOperation STENCIL_OP_MAX = 8

Represents the size of the StencilOperation enum.

enum CompareOperator: 🔗

CompareOperator COMPARE_OP_NEVER = 0

"Never" comparison (opposite of COMPARE_OP_ALWAYS).

CompareOperator COMPARE_OP_LESS = 1

"Less than" comparison.

CompareOperator COMPARE_OP_EQUAL = 2

CompareOperator COMPARE_OP_LESS_OR_EQUAL = 3

"Less than or equal" comparison.

CompareOperator COMPARE_OP_GREATER = 4

"Greater than" comparison.

CompareOperator COMPARE_OP_NOT_EQUAL = 5

"Not equal" comparison.

CompareOperator COMPARE_OP_GREATER_OR_EQUAL = 6

"Greater than or equal" comparison.

CompareOperator COMPARE_OP_ALWAYS = 7

"Always" comparison (opposite of COMPARE_OP_NEVER).

CompareOperator COMPARE_OP_MAX = 8

Represents the size of the CompareOperator enum.

enum LogicOperation: 🔗

LogicOperation LOGIC_OP_CLEAR = 0

Clear logic operation (result is always 0). See also LOGIC_OP_SET.

LogicOperation LOGIC_OP_AND = 1

LogicOperation LOGIC_OP_AND_REVERSE = 2

AND logic operation with the destination operand being inverted. See also LOGIC_OP_AND_INVERTED.

LogicOperation LOGIC_OP_COPY = 3

Copy logic operation (keeps the source value as-is). See also LOGIC_OP_COPY_INVERTED and LOGIC_OP_NO_OP.

LogicOperation LOGIC_OP_AND_INVERTED = 4

AND logic operation with the source operand being inverted. See also LOGIC_OP_AND_REVERSE.

LogicOperation LOGIC_OP_NO_OP = 5

No-op logic operation (keeps the destination value as-is). See also LOGIC_OP_COPY.

LogicOperation LOGIC_OP_XOR = 6

Exclusive or (XOR) logic operation.

LogicOperation LOGIC_OP_OR = 7

LogicOperation LOGIC_OP_NOR = 8

Not-OR (NOR) logic operation.

LogicOperation LOGIC_OP_EQUIVALENT = 9

Not-XOR (XNOR) logic operation.

LogicOperation LOGIC_OP_INVERT = 10

Invert logic operation.

LogicOperation LOGIC_OP_OR_REVERSE = 11

OR logic operation with the destination operand being inverted. See also LOGIC_OP_OR_REVERSE.

LogicOperation LOGIC_OP_COPY_INVERTED = 12

NOT logic operation (inverts the value). See also LOGIC_OP_COPY.

LogicOperation LOGIC_OP_OR_INVERTED = 13

OR logic operation with the source operand being inverted. See also LOGIC_OP_OR_REVERSE.

LogicOperation LOGIC_OP_NAND = 14

Not-AND (NAND) logic operation.

LogicOperation LOGIC_OP_SET = 15

SET logic operation (result is always 1). See also LOGIC_OP_CLEAR.

LogicOperation LOGIC_OP_MAX = 16

Represents the size of the LogicOperation enum.

BlendFactor BLEND_FACTOR_ZERO = 0

Constant 0.0 blend factor.

BlendFactor BLEND_FACTOR_ONE = 1

Constant 1.0 blend factor.

BlendFactor BLEND_FACTOR_SRC_COLOR = 2

Color blend factor is source color. Alpha blend factor is source alpha.

BlendFactor BLEND_FACTOR_ONE_MINUS_SRC_COLOR = 3

Color blend factor is 1.0 - source color. Alpha blend factor is 1.0 - source alpha.

BlendFactor BLEND_FACTOR_DST_COLOR = 4

Color blend factor is destination color. Alpha blend factor is destination alpha.

BlendFactor BLEND_FACTOR_ONE_MINUS_DST_COLOR = 5

Color blend factor is 1.0 - destination color. Alpha blend factor is 1.0 - destination alpha.

BlendFactor BLEND_FACTOR_SRC_ALPHA = 6

Color and alpha blend factor is source alpha.

BlendFactor BLEND_FACTOR_ONE_MINUS_SRC_ALPHA = 7

Color and alpha blend factor is 1.0 - source alpha.

BlendFactor BLEND_FACTOR_DST_ALPHA = 8

Color and alpha blend factor is destination alpha.

BlendFactor BLEND_FACTOR_ONE_MINUS_DST_ALPHA = 9

Color and alpha blend factor is 1.0 - destination alpha.

BlendFactor BLEND_FACTOR_CONSTANT_COLOR = 10

Color blend factor is blend constant color. Alpha blend factor is blend constant alpha (see draw_list_set_blend_constants()).

BlendFactor BLEND_FACTOR_ONE_MINUS_CONSTANT_COLOR = 11

Color blend factor is 1.0 - blend constant color. Alpha blend factor is 1.0 - blend constant alpha (see draw_list_set_blend_constants()).

BlendFactor BLEND_FACTOR_CONSTANT_ALPHA = 12

Color and alpha blend factor is blend constant alpha (see draw_list_set_blend_constants()).

BlendFactor BLEND_FACTOR_ONE_MINUS_CONSTANT_ALPHA = 13

Color and alpha blend factor is 1.0 - blend constant alpha (see draw_list_set_blend_constants()).

BlendFactor BLEND_FACTOR_SRC_ALPHA_SATURATE = 14

Color blend factor is min(source alpha, 1.0 - destination alpha). Alpha blend factor is 1.0.

BlendFactor BLEND_FACTOR_SRC1_COLOR = 15

Color blend factor is second source color. Alpha blend factor is second source alpha. Only relevant for dual-source blending.

BlendFactor BLEND_FACTOR_ONE_MINUS_SRC1_COLOR = 16

Color blend factor is 1.0 - second source color. Alpha blend factor is 1.0 - second source alpha. Only relevant for dual-source blending.

BlendFactor BLEND_FACTOR_SRC1_ALPHA = 17

Color and alpha blend factor is second source alpha. Only relevant for dual-source blending.

BlendFactor BLEND_FACTOR_ONE_MINUS_SRC1_ALPHA = 18

Color and alpha blend factor is 1.0 - second source alpha. Only relevant for dual-source blending.

BlendFactor BLEND_FACTOR_MAX = 19

Represents the size of the BlendFactor enum.

enum BlendOperation: 🔗

BlendOperation BLEND_OP_ADD = 0

Additive blending operation (source + destination).

BlendOperation BLEND_OP_SUBTRACT = 1

Subtractive blending operation (source - destination).

BlendOperation BLEND_OP_REVERSE_SUBTRACT = 2

Reverse subtractive blending operation (destination - source).

BlendOperation BLEND_OP_MINIMUM = 3

Minimum blending operation (keep the lowest value of the two).

BlendOperation BLEND_OP_MAXIMUM = 4

Maximum blending operation (keep the highest value of the two).

BlendOperation BLEND_OP_MAX = 5

Represents the size of the BlendOperation enum.

flags PipelineDynamicStateFlags: 🔗

PipelineDynamicStateFlags DYNAMIC_STATE_LINE_WIDTH = 1

Allows dynamically changing the width of rendering lines.

PipelineDynamicStateFlags DYNAMIC_STATE_DEPTH_BIAS = 2

Allows dynamically changing the depth bias.

PipelineDynamicStateFlags DYNAMIC_STATE_BLEND_CONSTANTS = 4

There is currently no description for this enum. Please help us by contributing one!

PipelineDynamicStateFlags DYNAMIC_STATE_DEPTH_BOUNDS = 8

There is currently no description for this enum. Please help us by contributing one!

PipelineDynamicStateFlags DYNAMIC_STATE_STENCIL_COMPARE_MASK = 16

There is currently no description for this enum. Please help us by contributing one!

PipelineDynamicStateFlags DYNAMIC_STATE_STENCIL_WRITE_MASK = 32

There is currently no description for this enum. Please help us by contributing one!

PipelineDynamicStateFlags DYNAMIC_STATE_STENCIL_REFERENCE = 64

There is currently no description for this enum. Please help us by contributing one!

enum InitialAction: 🔗

InitialAction INITIAL_ACTION_LOAD = 0

Deprecated: Initial actions are solved automatically by RenderingDevice.

Load the previous contents of the framebuffer.

InitialAction INITIAL_ACTION_CLEAR = 1

Deprecated: Initial actions are solved automatically by RenderingDevice.

Clear the whole framebuffer or its specified region.

InitialAction INITIAL_ACTION_DISCARD = 2

Deprecated: Initial actions are solved automatically by RenderingDevice.

Ignore the previous contents of the framebuffer. This is the fastest option if you'll overwrite all of the pixels and don't need to read any of them.

InitialAction INITIAL_ACTION_MAX = 3

Deprecated: Initial actions are solved automatically by RenderingDevice.

Represents the size of the InitialAction enum.

InitialAction INITIAL_ACTION_CLEAR_REGION = 1

Deprecated: Initial actions are solved automatically by RenderingDevice.

InitialAction INITIAL_ACTION_CLEAR_REGION_CONTINUE = 1

Deprecated: Initial actions are solved automatically by RenderingDevice.

InitialAction INITIAL_ACTION_KEEP = 0

Deprecated: Initial actions are solved automatically by RenderingDevice.

InitialAction INITIAL_ACTION_DROP = 2

Deprecated: Initial actions are solved automatically by RenderingDevice.

InitialAction INITIAL_ACTION_CONTINUE = 0

Deprecated: Initial actions are solved automatically by RenderingDevice.

FinalAction FINAL_ACTION_STORE = 0

Deprecated: Final actions are solved automatically by RenderingDevice.

Store the result of the draw list in the framebuffer. This is generally what you want to do.

FinalAction FINAL_ACTION_DISCARD = 1

Deprecated: Final actions are solved automatically by RenderingDevice.

Discard the contents of the framebuffer. This is the fastest option if you don't need to use the results of the draw list.

FinalAction FINAL_ACTION_MAX = 2

Deprecated: Final actions are solved automatically by RenderingDevice.

Represents the size of the FinalAction enum.

FinalAction FINAL_ACTION_READ = 0

Deprecated: Final actions are solved automatically by RenderingDevice.

FinalAction FINAL_ACTION_CONTINUE = 0

Deprecated: Final actions are solved automatically by RenderingDevice.

ShaderStage SHADER_STAGE_VERTEX = 0

Vertex shader stage. This can be used to manipulate vertices from a shader (but not create new vertices).

ShaderStage SHADER_STAGE_FRAGMENT = 1

Fragment shader stage (called "pixel shader" in Direct3D). This can be used to manipulate pixels from a shader.

ShaderStage SHADER_STAGE_TESSELATION_CONTROL = 2

Tessellation control shader stage. This can be used to create additional geometry from a shader.

ShaderStage SHADER_STAGE_TESSELATION_EVALUATION = 3

Tessellation evaluation shader stage. This can be used to create additional geometry from a shader.

ShaderStage SHADER_STAGE_COMPUTE = 4

Compute shader stage. This can be used to run arbitrary computing tasks in a shader, performing them on the GPU instead of the CPU.

ShaderStage SHADER_STAGE_MAX = 5

Represents the size of the ShaderStage enum.

ShaderStage SHADER_STAGE_VERTEX_BIT = 1

Vertex shader stage bit (see also SHADER_STAGE_VERTEX).

ShaderStage SHADER_STAGE_FRAGMENT_BIT = 2

Fragment shader stage bit (see also SHADER_STAGE_FRAGMENT).

ShaderStage SHADER_STAGE_TESSELATION_CONTROL_BIT = 4

Tessellation control shader stage bit (see also SHADER_STAGE_TESSELATION_CONTROL).

ShaderStage SHADER_STAGE_TESSELATION_EVALUATION_BIT = 8

Tessellation evaluation shader stage bit (see also SHADER_STAGE_TESSELATION_EVALUATION).

ShaderStage SHADER_STAGE_COMPUTE_BIT = 16

Compute shader stage bit (see also SHADER_STAGE_COMPUTE).

enum ShaderLanguage: 🔗

ShaderLanguage SHADER_LANGUAGE_GLSL = 0

Khronos' GLSL shading language (used natively by OpenGL and Vulkan). This is the language used for core Godot shaders.

ShaderLanguage SHADER_LANGUAGE_HLSL = 1

Microsoft's High-Level Shading Language (used natively by Direct3D, but can also be used in Vulkan).

enum PipelineSpecializationConstantType: 🔗

PipelineSpecializationConstantType PIPELINE_SPECIALIZATION_CONSTANT_TYPE_BOOL = 0

Boolean specialization constant.

PipelineSpecializationConstantType PIPELINE_SPECIALIZATION_CONSTANT_TYPE_INT = 1

Integer specialization constant.

PipelineSpecializationConstantType PIPELINE_SPECIALIZATION_CONSTANT_TYPE_FLOAT = 2

Floating-point specialization constant.

Features SUPPORTS_METALFX_SPATIAL = 3

Support for MetalFX spatial upscaling.

Features SUPPORTS_METALFX_TEMPORAL = 4

Support for MetalFX temporal upscaling.

Features SUPPORTS_BUFFER_DEVICE_ADDRESS = 6

Features support for buffer device address extension.

Features SUPPORTS_IMAGE_ATOMIC_32_BIT = 7

Support for 32-bit image atomic operations.

Limit LIMIT_MAX_BOUND_UNIFORM_SETS = 0

Maximum number of uniform sets that can be bound at a given time.

Limit LIMIT_MAX_FRAMEBUFFER_COLOR_ATTACHMENTS = 1

Maximum number of color framebuffer attachments that can be used at a given time.

Limit LIMIT_MAX_TEXTURES_PER_UNIFORM_SET = 2

Maximum number of textures that can be used per uniform set.

Limit LIMIT_MAX_SAMPLERS_PER_UNIFORM_SET = 3

Maximum number of samplers that can be used per uniform set.

Limit LIMIT_MAX_STORAGE_BUFFERS_PER_UNIFORM_SET = 4

Maximum number of storage buffers per uniform set.

Limit LIMIT_MAX_STORAGE_IMAGES_PER_UNIFORM_SET = 5

Maximum number of storage images per uniform set.

Limit LIMIT_MAX_UNIFORM_BUFFERS_PER_UNIFORM_SET = 6

Maximum number of uniform buffers per uniform set.

Limit LIMIT_MAX_DRAW_INDEXED_INDEX = 7

Maximum index for an indexed draw command.

Limit LIMIT_MAX_FRAMEBUFFER_HEIGHT = 8

Maximum height of a framebuffer (in pixels).

Limit LIMIT_MAX_FRAMEBUFFER_WIDTH = 9

Maximum width of a framebuffer (in pixels).

Limit LIMIT_MAX_TEXTURE_ARRAY_LAYERS = 10

Maximum number of texture array layers.

Limit LIMIT_MAX_TEXTURE_SIZE_1D = 11

Maximum supported 1-dimensional texture size (in pixels on a single axis).

Limit LIMIT_MAX_TEXTURE_SIZE_2D = 12

Maximum supported 2-dimensional texture size (in pixels on a single axis).

Limit LIMIT_MAX_TEXTURE_SIZE_3D = 13

Maximum supported 3-dimensional texture size (in pixels on a single axis).

Limit LIMIT_MAX_TEXTURE_SIZE_CUBE = 14

Maximum supported cubemap texture size (in pixels on a single axis of a single face).

Limit LIMIT_MAX_TEXTURES_PER_SHADER_STAGE = 15

Maximum number of textures per shader stage.

Limit LIMIT_MAX_SAMPLERS_PER_SHADER_STAGE = 16

Maximum number of samplers per shader stage.

Limit LIMIT_MAX_STORAGE_BUFFERS_PER_SHADER_STAGE = 17

Maximum number of storage buffers per shader stage.

Limit LIMIT_MAX_STORAGE_IMAGES_PER_SHADER_STAGE = 18

Maximum number of storage images per shader stage.

Limit LIMIT_MAX_UNIFORM_BUFFERS_PER_SHADER_STAGE = 19

Maximum number of uniform buffers per uniform set.

Limit LIMIT_MAX_PUSH_CONSTANT_SIZE = 20

Maximum size of a push constant. A lot of devices are limited to 128 bytes, so try to avoid exceeding 128 bytes in push constants to ensure compatibility even if your GPU is reporting a higher value.

Limit LIMIT_MAX_UNIFORM_BUFFER_SIZE = 21

Maximum size of a uniform buffer.

Limit LIMIT_MAX_VERTEX_INPUT_ATTRIBUTE_OFFSET = 22

Maximum vertex input attribute offset.

Limit LIMIT_MAX_VERTEX_INPUT_ATTRIBUTES = 23

Maximum number of vertex input attributes.

Limit LIMIT_MAX_VERTEX_INPUT_BINDINGS = 24

Maximum number of vertex input bindings.

Limit LIMIT_MAX_VERTEX_INPUT_BINDING_STRIDE = 25

Maximum vertex input binding stride.

Limit LIMIT_MIN_UNIFORM_BUFFER_OFFSET_ALIGNMENT = 26

Minimum uniform buffer offset alignment.

Limit LIMIT_MAX_COMPUTE_SHARED_MEMORY_SIZE = 27

Maximum shared memory size for compute shaders.

Limit LIMIT_MAX_COMPUTE_WORKGROUP_COUNT_X = 28

Maximum number of workgroups for compute shaders on the X axis.

Limit LIMIT_MAX_COMPUTE_WORKGROUP_COUNT_Y = 29

Maximum number of workgroups for compute shaders on the Y axis.

Limit LIMIT_MAX_COMPUTE_WORKGROUP_COUNT_Z = 30

Maximum number of workgroups for compute shaders on the Z axis.

Limit LIMIT_MAX_COMPUTE_WORKGROUP_INVOCATIONS = 31

Maximum number of workgroup invocations for compute shaders.

Limit LIMIT_MAX_COMPUTE_WORKGROUP_SIZE_X = 32

Maximum workgroup size for compute shaders on the X axis.

Limit LIMIT_MAX_COMPUTE_WORKGROUP_SIZE_Y = 33

Maximum workgroup size for compute shaders on the Y axis.

Limit LIMIT_MAX_COMPUTE_WORKGROUP_SIZE_Z = 34

Maximum workgroup size for compute shaders on the Z axis.

Limit LIMIT_MAX_VIEWPORT_DIMENSIONS_X = 35

Maximum viewport width (in pixels).

Limit LIMIT_MAX_VIEWPORT_DIMENSIONS_Y = 36

Maximum viewport height (in pixels).

Limit LIMIT_METALFX_TEMPORAL_SCALER_MIN_SCALE = 46

Returns the smallest value for ProjectSettings.rendering/scaling_3d/scale when using the MetalFX temporal upscaler.

Note: The returned value is multiplied by a factor of 1000000 to preserve 6 digits of precision. It must be divided by 1000000.0 to convert the value to a floating point number.

Limit LIMIT_METALFX_TEMPORAL_SCALER_MAX_SCALE = 47

Returns the largest value for ProjectSettings.rendering/scaling_3d/scale when using the MetalFX temporal upscaler.

Note: The returned value is multiplied by a factor of 1000000 to preserve 6 digits of precision. It must be divided by 1000000.0 to convert the value to a floating point number.

MemoryType MEMORY_TEXTURES = 0

Memory taken by textures.

MemoryType MEMORY_BUFFERS = 1

Memory taken by buffers.

MemoryType MEMORY_TOTAL = 2

Total memory taken. This is greater than the sum of MEMORY_TEXTURES and MEMORY_BUFFERS, as it also includes miscellaneous memory usage.

enum BreadcrumbMarker: 🔗

BreadcrumbMarker NONE = 0

No breadcrumb marker will be added.

BreadcrumbMarker REFLECTION_PROBES = 65536

During a GPU crash in dev or debug mode, Godot's error message will include "REFLECTION_PROBES" for added context as to when the crash occurred.

BreadcrumbMarker SKY_PASS = 131072

During a GPU crash in dev or debug mode, Godot's error message will include "SKY_PASS" for added context as to when the crash occurred.

BreadcrumbMarker LIGHTMAPPER_PASS = 196608

During a GPU crash in dev or debug mode, Godot's error message will include "LIGHTMAPPER_PASS" for added context as to when the crash occurred.

BreadcrumbMarker SHADOW_PASS_DIRECTIONAL = 262144

During a GPU crash in dev or debug mode, Godot's error message will include "SHADOW_PASS_DIRECTIONAL" for added context as to when the crash occurred.

BreadcrumbMarker SHADOW_PASS_CUBE = 327680

During a GPU crash in dev or debug mode, Godot's error message will include "SHADOW_PASS_CUBE" for added context as to when the crash occurred.

BreadcrumbMarker OPAQUE_PASS = 393216

During a GPU crash in dev or debug mode, Godot's error message will include "OPAQUE_PASS" for added context as to when the crash occurred.

BreadcrumbMarker ALPHA_PASS = 458752

During a GPU crash in dev or debug mode, Godot's error message will include "ALPHA_PASS" for added context as to when the crash occurred.

BreadcrumbMarker TRANSPARENT_PASS = 524288

During a GPU crash in dev or debug mode, Godot's error message will include "TRANSPARENT_PASS" for added context as to when the crash occurred.

BreadcrumbMarker POST_PROCESSING_PASS = 589824

During a GPU crash in dev or debug mode, Godot's error message will include "POST_PROCESSING_PASS" for added context as to when the crash occurred.

BreadcrumbMarker BLIT_PASS = 655360

During a GPU crash in dev or debug mode, Godot's error message will include "BLIT_PASS" for added context as to when the crash occurred.

BreadcrumbMarker UI_PASS = 720896

During a GPU crash in dev or debug mode, Godot's error message will include "UI_PASS" for added context as to when the crash occurred.

BreadcrumbMarker DEBUG_PASS = 786432

During a GPU crash in dev or debug mode, Godot's error message will include "DEBUG_PASS" for added context as to when the crash occurred.

DrawFlags DRAW_DEFAULT_ALL = 0

Do not clear or ignore any attachments.

DrawFlags DRAW_CLEAR_COLOR_0 = 1

Clear the first color attachment.

DrawFlags DRAW_CLEAR_COLOR_1 = 2

Clear the second color attachment.

DrawFlags DRAW_CLEAR_COLOR_2 = 4

Clear the third color attachment.

DrawFlags DRAW_CLEAR_COLOR_3 = 8

Clear the fourth color attachment.

DrawFlags DRAW_CLEAR_COLOR_4 = 16

Clear the fifth color attachment.

DrawFlags DRAW_CLEAR_COLOR_5 = 32

Clear the sixth color attachment.

DrawFlags DRAW_CLEAR_COLOR_6 = 64

Clear the seventh color attachment.

DrawFlags DRAW_CLEAR_COLOR_7 = 128

Clear the eighth color attachment.

DrawFlags DRAW_CLEAR_COLOR_MASK = 255

Mask for clearing all color attachments.

DrawFlags DRAW_CLEAR_COLOR_ALL = 255

Clear all color attachments.

DrawFlags DRAW_IGNORE_COLOR_0 = 256

Ignore the previous contents of the first color attachment.

DrawFlags DRAW_IGNORE_COLOR_1 = 512

Ignore the previous contents of the second color attachment.

DrawFlags DRAW_IGNORE_COLOR_2 = 1024

Ignore the previous contents of the third color attachment.

DrawFlags DRAW_IGNORE_COLOR_3 = 2048

Ignore the previous contents of the fourth color attachment.

DrawFlags DRAW_IGNORE_COLOR_4 = 4096

Ignore the previous contents of the fifth color attachment.

DrawFlags DRAW_IGNORE_COLOR_5 = 8192

Ignore the previous contents of the sixth color attachment.

DrawFlags DRAW_IGNORE_COLOR_6 = 16384

Ignore the previous contents of the seventh color attachment.

DrawFlags DRAW_IGNORE_COLOR_7 = 32768

Ignore the previous contents of the eighth color attachment.

DrawFlags DRAW_IGNORE_COLOR_MASK = 65280

Mask for ignoring all the previous contents of the color attachments.

DrawFlags DRAW_IGNORE_COLOR_ALL = 65280

Ignore the previous contents of all color attachments.

DrawFlags DRAW_CLEAR_DEPTH = 65536

Clear the depth attachment.

DrawFlags DRAW_IGNORE_DEPTH = 131072

Ignore the previous contents of the depth attachment.

DrawFlags DRAW_CLEAR_STENCIL = 262144

Clear the stencil attachment.

DrawFlags DRAW_IGNORE_STENCIL = 524288

Ignore the previous contents of the stencil attachment.

DrawFlags DRAW_CLEAR_ALL = 327935

Clear all attachments.

DrawFlags DRAW_IGNORE_ALL = 720640

Ignore the previous contents of all attachments.

Returned by functions that return an ID if a value is invalid.

INVALID_FORMAT_ID = -1 🔗

Returned by functions that return a format ID if a value is invalid.

void barrier(from: BitField[BarrierMask] = 32767, to: BitField[BarrierMask] = 32767) 🔗

Deprecated: Barriers are automatically inserted by RenderingDevice.

This method does nothing.

Error buffer_clear(buffer: RID, offset: int, size_bytes: int) 🔗

Clears the contents of the buffer, clearing size_bytes bytes, starting at offset.

the size isn't a multiple of four

the region specified by offset + size_bytes exceeds the buffer

a draw list is currently active (created by draw_list_begin())

a compute list is currently active (created by compute_list_begin())

Error buffer_copy(src_buffer: RID, dst_buffer: RID, src_offset: int, dst_offset: int, size: int) 🔗

Copies size bytes from the src_buffer at src_offset into dst_buffer at dst_offset.

size exceeds the size of either src_buffer or dst_buffer at their corresponding offsets

a draw list is currently active (created by draw_list_begin())

a compute list is currently active (created by compute_list_begin())

PackedByteArray buffer_get_data(buffer: RID, offset_bytes: int = 0, size_bytes: int = 0) 🔗

Returns a copy of the data of the specified buffer, optionally offset_bytes and size_bytes can be set to copy only a portion of the buffer.

Note: This method will block the GPU from working until the data is retrieved. Refer to buffer_get_data_async() for an alternative that returns the data in more performant way.

Error buffer_get_data_async(buffer: RID, callback: Callable, offset_bytes: int = 0, size_bytes: int = 0) 🔗

Asynchronous version of buffer_get_data(). RenderingDevice will call callback in a certain amount of frames with the data the buffer had at the time of the request.

Note: At the moment, the delay corresponds to the amount of frames specified by ProjectSettings.rendering/rendering_device/vsync/frame_queue_size.

Note: Downloading large buffers can have a prohibitive cost for real-time even when using the asynchronous method due to hardware bandwidth limitations. When dealing with large resources, you can adjust settings such as ProjectSettings.rendering/rendering_device/staging_buffer/block_size_kb to improve the transfer speed at the cost of extra memory.

int buffer_get_device_address(buffer: RID) 🔗

Returns the address of the given buffer which can be passed to shaders in any way to access underlying data. Buffer must have been created with this feature enabled.

Note: You must check that the GPU supports this functionality by calling has_feature() with SUPPORTS_BUFFER_DEVICE_ADDRESS as a parameter.

Error buffer_update(buffer: RID, offset: int, size_bytes: int, data: PackedByteArray) 🔗

Updates a region of size_bytes bytes, starting at offset, in the buffer, with the specified data.

the region specified by offset + size_bytes exceeds the buffer

a draw list is currently active (created by draw_list_begin())

a compute list is currently active (created by compute_list_begin())

void capture_timestamp(name: String) 🔗

Creates a timestamp marker with the specified name. This is used for performance reporting with the get_captured_timestamp_cpu_time(), get_captured_timestamp_gpu_time() and get_captured_timestamp_name() methods.

void compute_list_add_barrier(compute_list: int) 🔗

Raises a Vulkan compute barrier in the specified compute_list.

int compute_list_begin() 🔗

Starts a list of compute commands created with the compute_* methods. The returned value should be passed to other compute_list_* functions.

Multiple compute lists cannot be created at the same time; you must finish the previous compute list first using compute_list_end().

A simple compute operation might look like this (code is not a complete example):

void compute_list_bind_compute_pipeline(compute_list: int, compute_pipeline: RID) 🔗

Tells the GPU what compute pipeline to use when processing the compute list. If the shader has changed since the last time this function was called, Godot will unbind all descriptor sets and will re-bind them inside compute_list_dispatch().

void compute_list_bind_uniform_set(compute_list: int, uniform_set: RID, set_index: int) 🔗

Binds the uniform_set to this compute_list. Godot ensures that all textures in the uniform set have the correct Vulkan access masks. If Godot had to change access masks of textures, it will raise a Vulkan image memory barrier.

void compute_list_dispatch(compute_list: int, x_groups: int, y_groups: int, z_groups: int) 🔗

Submits the compute list for processing on the GPU. This is the compute equivalent to draw_list_draw().

void compute_list_dispatch_indirect(compute_list: int, buffer: RID, offset: int) 🔗

Submits the compute list for processing on the GPU with the given group counts stored in the buffer at offset. Buffer must have been created with STORAGE_BUFFER_USAGE_DISPATCH_INDIRECT flag.

void compute_list_end() 🔗

Finishes a list of compute commands created with the compute_* methods.

void compute_list_set_push_constant(compute_list: int, buffer: PackedByteArray, size_bytes: int) 🔗

Sets the push constant data to buffer for the specified compute_list. The shader determines how this binary data is used. The buffer's size in bytes must also be specified in size_bytes (this can be obtained by calling the PackedByteArray.size() method on the passed buffer).

RID compute_pipeline_create(shader: RID, specialization_constants: Array[RDPipelineSpecializationConstant] = []) 🔗

Creates a new compute pipeline. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

bool compute_pipeline_is_valid(compute_pipeline: RID) 🔗

Returns true if the compute pipeline specified by the compute_pipeline RID is valid, false otherwise.

RenderingDevice create_local_device() 🔗

Create a new local RenderingDevice. This is most useful for performing compute operations on the GPU independently from the rest of the engine.

void draw_command_begin_label(name: String, color: Color) 🔗

Create a command buffer debug label region that can be displayed in third-party tools such as RenderDoc. All regions must be ended with a draw_command_end_label() call. When viewed from the linear series of submissions to a single queue, calls to draw_command_begin_label() and draw_command_end_label() must be matched and balanced.

The VK_EXT_DEBUG_UTILS_EXTENSION_NAME Vulkan extension must be available and enabled for command buffer debug label region to work. See also draw_command_end_label().

void draw_command_end_label() 🔗

Ends the command buffer debug label region started by a draw_command_begin_label() call.

void draw_command_insert_label(name: String, color: Color) 🔗

Deprecated: Inserting labels no longer applies due to command reordering.

This method does nothing.

int draw_list_begin(framebuffer: RID, draw_flags: BitField[DrawFlags] = 0, clear_color_values: PackedColorArray = PackedColorArray(), clear_depth_value: float = 1.0, clear_stencil_value: int = 0, region: Rect2 = Rect2(0, 0, 0, 0), breadcrumb: int = 0) 🔗

Starts a list of raster drawing commands created with the draw_* methods. The returned value should be passed to other draw_list_* functions.

Multiple draw lists cannot be created at the same time; you must finish the previous draw list first using draw_list_end().

A simple drawing operation might look like this (code is not a complete example):

The draw_flags indicates if the texture attachments of the framebuffer should be cleared or ignored. Only one of the two flags can be used for each individual attachment. Ignoring an attachment means that any contents that existed before the draw list will be completely discarded, reducing the memory bandwidth used by the render pass but producing garbage results if the pixels aren't replaced. The default behavior allows the engine to figure out the right operation to use if the texture is discardable, which can result in increased performance. See RDTextureFormat or texture_set_discardable().

The breadcrumb parameter can be an arbitrary 32-bit integer that is useful to diagnose GPU crashes. If Godot is built in dev or debug mode; when the GPU crashes Godot will dump all shaders that were being executed at the time of the crash and the breadcrumb is useful to diagnose what passes did those shaders belong to.

It does not affect rendering behavior and can be set to 0. It is recommended to use BreadcrumbMarker enumerations for consistency but it's not required. It is also possible to use bitwise operations to add extra data. e.g.

int draw_list_begin_for_screen(screen: int = 0, clear_color: Color = Color(0, 0, 0, 1)) 🔗

High-level variant of draw_list_begin(), with the parameters automatically being adjusted for drawing onto the window specified by the screen ID.

Note: Cannot be used with local RenderingDevices, as these don't have a screen. If called on a local RenderingDevice, draw_list_begin_for_screen() returns INVALID_ID.

PackedInt64Array draw_list_begin_split(framebuffer: RID, splits: int, initial_color_action: InitialAction, final_color_action: FinalAction, initial_depth_action: InitialAction, final_depth_action: FinalAction, clear_color_values: PackedColorArray = PackedColorArray(), clear_depth: float = 1.0, clear_stencil: int = 0, region: Rect2 = Rect2(0, 0, 0, 0), storage_textures: Array[RID] = []) 🔗

Deprecated: Split draw lists are used automatically by RenderingDevice.

This method does nothing and always returns an empty PackedInt64Array.

void draw_list_bind_index_array(draw_list: int, index_array: RID) 🔗

Binds index_array to the specified draw_list.

void draw_list_bind_render_pipeline(draw_list: int, render_pipeline: RID) 🔗

Binds render_pipeline to the specified draw_list.

void draw_list_bind_uniform_set(draw_list: int, uniform_set: RID, set_index: int) 🔗

Binds uniform_set to the specified draw_list. A set_index must also be specified, which is an identifier starting from 0 that must match the one expected by the draw list.

void draw_list_bind_vertex_array(draw_list: int, vertex_array: RID) 🔗

Binds vertex_array to the specified draw_list.

void draw_list_disable_scissor(draw_list: int) 🔗

Removes and disables the scissor rectangle for the specified draw_list. See also draw_list_enable_scissor().

void draw_list_draw(draw_list: int, use_indices: bool, instances: int, procedural_vertex_count: int = 0) 🔗

Submits draw_list for rendering on the GPU. This is the raster equivalent to compute_list_dispatch().

void draw_list_draw_indirect(draw_list: int, use_indices: bool, buffer: RID, offset: int = 0, draw_count: int = 1, stride: int = 0) 🔗

Submits draw_list for rendering on the GPU with the given parameters stored in the buffer at offset. Parameters being integers: vertex count, instance count, first vertex, first instance. And when using indices: index count, instance count, first index, vertex offset, first instance. Buffer must have been created with STORAGE_BUFFER_USAGE_DISPATCH_INDIRECT flag.

void draw_list_enable_scissor(draw_list: int, rect: Rect2 = Rect2(0, 0, 0, 0)) 🔗

Creates a scissor rectangle and enables it for the specified draw_list. Scissor rectangles are used for clipping by discarding fragments that fall outside a specified rectangular portion of the screen. See also draw_list_disable_scissor().

Note: The specified rect is automatically intersected with the screen's dimensions, which means it cannot exceed the screen's dimensions.

void draw_list_end() 🔗

Finishes a list of raster drawing commands created with the draw_* methods.

void draw_list_set_blend_constants(draw_list: int, color: Color) 🔗

Sets blend constants for the specified draw_list to color. Blend constants are used only if the graphics pipeline is created with DYNAMIC_STATE_BLEND_CONSTANTS flag set.

void draw_list_set_push_constant(draw_list: int, buffer: PackedByteArray, size_bytes: int) 🔗

Sets the push constant data to buffer for the specified draw_list. The shader determines how this binary data is used. The buffer's size in bytes must also be specified in size_bytes (this can be obtained by calling the PackedByteArray.size() method on the passed buffer).

int draw_list_switch_to_next_pass() 🔗

Switches to the next draw pass.

PackedInt64Array draw_list_switch_to_next_pass_split(splits: int) 🔗

Deprecated: Split draw lists are used automatically by RenderingDevice.

This method does nothing and always returns an empty PackedInt64Array.

RID framebuffer_create(textures: Array[RID], validate_with_format: int = -1, view_count: int = 1) 🔗

Creates a new framebuffer. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

RID framebuffer_create_empty(size: Vector2i, samples: TextureSamples = 0, validate_with_format: int = -1) 🔗

Creates a new empty framebuffer. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

RID framebuffer_create_multipass(textures: Array[RID], passes: Array[RDFramebufferPass], validate_with_format: int = -1, view_count: int = 1) 🔗

Creates a new multipass framebuffer. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

int framebuffer_format_create(attachments: Array[RDAttachmentFormat], view_count: int = 1) 🔗

Creates a new framebuffer format with the specified attachments and view_count. Returns the new framebuffer's unique framebuffer format ID.

If view_count is greater than or equal to 2, enables multiview which is used for VR rendering. This requires support for the Vulkan multiview extension.

int framebuffer_format_create_empty(samples: TextureSamples = 0) 🔗

Creates a new empty framebuffer format with the specified number of samples and returns its ID.

int framebuffer_format_create_multipass(attachments: Array[RDAttachmentFormat], passes: Array[RDFramebufferPass], view_count: int = 1) 🔗

Creates a multipass framebuffer format with the specified attachments, passes and view_count and returns its ID. If view_count is greater than or equal to 2, enables multiview which is used for VR rendering. This requires support for the Vulkan multiview extension.

TextureSamples framebuffer_format_get_texture_samples(format: int, render_pass: int = 0) 🔗

Returns the number of texture samples used for the given framebuffer format ID (returned by framebuffer_get_format()).

int framebuffer_get_format(framebuffer: RID) 🔗

Returns the format ID of the framebuffer specified by the framebuffer RID. This ID is guaranteed to be unique for the same formats and does not need to be freed.

bool framebuffer_is_valid(framebuffer: RID) const 🔗

Returns true if the framebuffer specified by the framebuffer RID is valid, false otherwise.

void free_rid(rid: RID) 🔗

Tries to free an object in the RenderingDevice. To avoid memory leaks, this should be called after using an object as memory management does not occur automatically when using RenderingDevice directly.

void full_barrier() 🔗

Deprecated: Barriers are automatically inserted by RenderingDevice.

This method does nothing.

int get_captured_timestamp_cpu_time(index: int) const 🔗

Returns the timestamp in CPU time for the rendering step specified by index (in microseconds since the engine started). See also get_captured_timestamp_gpu_time() and capture_timestamp().

int get_captured_timestamp_gpu_time(index: int) const 🔗

Returns the timestamp in GPU time for the rendering step specified by index (in microseconds since the engine started). See also get_captured_timestamp_cpu_time() and capture_timestamp().

String get_captured_timestamp_name(index: int) const 🔗

Returns the timestamp's name for the rendering step specified by index. See also capture_timestamp().

int get_captured_timestamps_count() const 🔗

Returns the total number of timestamps (rendering steps) available for profiling.

int get_captured_timestamps_frame() const 🔗

Returns the index of the last frame rendered that has rendering timestamps available for querying.

int get_device_allocation_count() const 🔗

Returns how many allocations the GPU has performed for internal driver structures.

This is only used by Vulkan in debug builds and can return 0 when this information is not tracked or unknown.

int get_device_allocs_by_object_type(type: int) const 🔗

Same as get_device_allocation_count() but filtered for a given object type.

The type argument must be in range [0; get_tracked_object_type_count - 1]. If get_tracked_object_type_count() is 0, then type argument is ignored and always returns 0.

This is only used by Vulkan in debug builds and can return 0 when this information is not tracked or unknown.

int get_device_memory_by_object_type(type: int) const 🔗

Same as get_device_total_memory() but filtered for a given object type.

The type argument must be in range [0; get_tracked_object_type_count - 1]. If get_tracked_object_type_count() is 0, then type argument is ignored and always returns 0.

This is only used by Vulkan in debug builds and can return 0 when this information is not tracked or unknown.

String get_device_name() const 🔗

Returns the name of the video adapter (e.g. "GeForce GTX 1080/PCIe/SSE2"). Equivalent to RenderingServer.get_video_adapter_name(). See also get_device_vendor_name().

String get_device_pipeline_cache_uuid() const 🔗

Returns the universally unique identifier for the pipeline cache. This is used to cache shader files on disk, which avoids shader recompilations on subsequent engine runs. This UUID varies depending on the graphics card model, but also the driver version. Therefore, updating graphics drivers will invalidate the shader cache.

int get_device_total_memory() const 🔗

Returns how much bytes the GPU is using.

This is only used by Vulkan in debug builds and can return 0 when this information is not tracked or unknown.

String get_device_vendor_name() const 🔗

Returns the vendor of the video adapter (e.g. "NVIDIA Corporation"). Equivalent to RenderingServer.get_video_adapter_vendor(). See also get_device_name().

int get_driver_allocation_count() const 🔗

Returns how many allocations the GPU driver has performed for internal driver structures.

This is only used by Vulkan in debug builds and can return 0 when this information is not tracked or unknown.

int get_driver_allocs_by_object_type(type: int) const 🔗

Same as get_driver_allocation_count() but filtered for a given object type.

The type argument must be in range [0; get_tracked_object_type_count - 1]. If get_tracked_object_type_count() is 0, then type argument is ignored and always returns 0.

This is only used by Vulkan in debug builds and can return 0 when this information is not tracked or unknown.

String get_driver_and_device_memory_report() const 🔗

Returns string report in CSV format using the following methods:

get_tracked_object_name()

get_tracked_object_type_count()

get_driver_total_memory()

get_driver_allocation_count()

get_driver_memory_by_object_type()

get_driver_allocs_by_object_type()

get_device_total_memory()

get_device_allocation_count()

get_device_memory_by_object_type()

get_device_allocs_by_object_type()

This is only used by Vulkan in debug builds. Godot must also be started with the --extra-gpu-memory-tracking command line argument.

int get_driver_memory_by_object_type(type: int) const 🔗

Same as get_driver_total_memory() but filtered for a given object type.

The type argument must be in range [0; get_tracked_object_type_count - 1]. If get_tracked_object_type_count() is 0, then type argument is ignored and always returns 0.

This is only used by Vulkan in debug builds and can return 0 when this information is not tracked or unknown.

int get_driver_resource(resource: DriverResource, rid: RID, index: int) 🔗

Returns the unique identifier of the driver resource for the specified rid. Some driver resource types ignore the specified rid. index is always ignored but must be specified anyway.

int get_driver_total_memory() const 🔗

Returns how much bytes the GPU driver is using for internal driver structures.

This is only used by Vulkan in debug builds and can return 0 when this information is not tracked or unknown.

int get_frame_delay() const 🔗

Returns the frame count kept by the graphics API. Higher values result in higher input lag, but with more consistent throughput. For the main RenderingDevice, frames are cycled (usually 3 with triple-buffered V-Sync enabled). However, local RenderingDevices only have 1 frame.

int get_memory_usage(type: MemoryType) const 🔗

Returns the memory usage in bytes corresponding to the given type. When using Vulkan, these statistics are calculated by Vulkan Memory Allocator.

String get_perf_report() const 🔗

Returns a string with a performance report from the past frame. Updates every frame.

String get_tracked_object_name(type_index: int) const 🔗

Returns the name of the type of object for the given type_index. This value must be in range [0; get_tracked_object_type_count - 1]. If get_tracked_object_type_count() is 0, then type argument is ignored and always returns the same string.

The return value is important because it gives meaning to the types passed to get_driver_memory_by_object_type(), get_driver_allocs_by_object_type(), get_device_memory_by_object_type(), and get_device_allocs_by_object_type(). Examples of strings it can return (not exhaustive):

Thus if e.g. get_tracked_object_name(5) returns "COMMAND_POOL", then get_device_memory_by_object_type(5) returns the bytes used by the GPU for command pools.

This is only used by Vulkan in debug builds. Godot must also be started with the --extra-gpu-memory-tracking command line argument.

int get_tracked_object_type_count() const 🔗

Returns how many types of trackable objects there are.

This is only used by Vulkan in debug builds. Godot must also be started with the --extra-gpu-memory-tracking command line argument.

bool has_feature(feature: Features) const 🔗

Returns true if the feature is supported by the GPU.

RID index_array_create(index_buffer: RID, index_offset: int, index_count: int) 🔗

Creates a new index array. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

RID index_buffer_create(size_indices: int, format: IndexBufferFormat, data: PackedByteArray = PackedByteArray(), use_restart_indices: bool = false, creation_bits: BitField[BufferCreationBits] = 0) 🔗

Creates a new index buffer. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

int limit_get(limit: Limit) const 🔗

Returns the value of the specified limit. This limit varies depending on the current graphics hardware (and sometimes the driver version). If the given limit is exceeded, rendering errors will occur.

Limits for various graphics hardware can be found in the Vulkan Hardware Database.

RID render_pipeline_create(shader: RID, framebuffer_format: int, vertex_format: int, primitive: RenderPrimitive, rasterization_state: RDPipelineRasterizationState, multisample_state: RDPipelineMultisampleState, stencil_state: RDPipelineDepthStencilState, color_blend_state: RDPipelineColorBlendState, dynamic_state_flags: BitField[PipelineDynamicStateFlags] = 0, for_render_pass: int = 0, specialization_constants: Array[RDPipelineSpecializationConstant] = []) 🔗

Creates a new render pipeline. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

bool render_pipeline_is_valid(render_pipeline: RID) 🔗

Returns true if the render pipeline specified by the render_pipeline RID is valid, false otherwise.

RID sampler_create(state: RDSamplerState) 🔗

Creates a new sampler. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

bool sampler_is_format_supported_for_filter(format: DataFormat, sampler_filter: SamplerFilter) const 🔗

Returns true if implementation supports using a texture of format with the given sampler_filter.

int screen_get_framebuffer_format(screen: int = 0) const 🔗

Returns the framebuffer format of the given screen.

Note: Only the main RenderingDevice returned by RenderingServer.get_rendering_device() has a format. If called on a local RenderingDevice, this method prints an error and returns INVALID_ID.

int screen_get_height(screen: int = 0) const 🔗

Returns the window height matching the graphics API context for the given window ID (in pixels). Despite the parameter being named screen, this returns the window size. See also screen_get_width().

Note: Only the main RenderingDevice returned by RenderingServer.get_rendering_device() has a height. If called on a local RenderingDevice, this method prints an error and returns INVALID_ID.

int screen_get_width(screen: int = 0) const 🔗

Returns the window width matching the graphics API context for the given window ID (in pixels). Despite the parameter being named screen, this returns the window size. See also screen_get_height().

Note: Only the main RenderingDevice returned by RenderingServer.get_rendering_device() has a width. If called on a local RenderingDevice, this method prints an error and returns INVALID_ID.

void set_resource_name(id: RID, name: String) 🔗

Sets the resource name for id to name. This is used for debugging with third-party tools such as RenderDoc.

The following types of resources can be named: texture, sampler, vertex buffer, index buffer, uniform buffer, texture buffer, storage buffer, uniform set buffer, shader, render pipeline and compute pipeline. Framebuffers cannot be named. Attempting to name an incompatible resource type will print an error.

Note: Resource names are only set when the engine runs in verbose mode (OS.is_stdout_verbose() = true), or when using an engine build compiled with the dev_mode=yes SCons option. The graphics driver must also support the VK_EXT_DEBUG_UTILS_EXTENSION_NAME Vulkan extension for named resources to work.

PackedByteArray shader_compile_binary_from_spirv(spirv_data: RDShaderSPIRV, name: String = "") 🔗

Compiles a binary shader from spirv_data and returns the compiled binary data as a PackedByteArray. This compiled shader is specific to the GPU model and driver version used; it will not work on different GPU models or even different driver versions. See also shader_compile_spirv_from_source().

name is an optional human-readable name that can be given to the compiled shader for organizational purposes.

RDShaderSPIRV shader_compile_spirv_from_source(shader_source: RDShaderSource, allow_cache: bool = true) 🔗

Compiles a SPIR-V from the shader source code in shader_source and returns the SPIR-V as an RDShaderSPIRV. This intermediate language shader is portable across different GPU models and driver versions, but cannot be run directly by GPUs until compiled into a binary shader using shader_compile_binary_from_spirv().

If allow_cache is true, make use of the shader cache generated by Godot. This avoids a potentially lengthy shader compilation step if the shader is already in cache. If allow_cache is false, Godot's shader cache is ignored and the shader will always be recompiled.

RID shader_create_from_bytecode(binary_data: PackedByteArray, placeholder_rid: RID = RID()) 🔗

Creates a new shader instance from a binary compiled shader. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method. See also shader_compile_binary_from_spirv() and shader_create_from_spirv().

RID shader_create_from_spirv(spirv_data: RDShaderSPIRV, name: String = "") 🔗

Creates a new shader instance from SPIR-V intermediate code. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method. See also shader_compile_spirv_from_source() and shader_create_from_bytecode().

RID shader_create_placeholder() 🔗

Create a placeholder RID by allocating an RID without initializing it for use in shader_create_from_bytecode(). This allows you to create an RID for a shader and pass it around, but defer compiling the shader to a later time.

int shader_get_vertex_input_attribute_mask(shader: RID) 🔗

Returns the internal vertex input mask. Internally, the vertex input mask is an unsigned integer consisting of the locations (specified in GLSL via. layout(location = ...)) of the input variables (specified in GLSL by the in keyword).

RID storage_buffer_create(size_bytes: int, data: PackedByteArray = PackedByteArray(), usage: BitField[StorageBufferUsage] = 0, creation_bits: BitField[BufferCreationBits] = 0) 🔗

Creates a storage buffer with the specified data and usage. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

Pushes the frame setup and draw command buffers then marks the local device as currently processing (which allows calling sync()).

Note: Only available in local RenderingDevices.

Forces a synchronization between the CPU and GPU, which may be required in certain cases. Only call this when needed, as CPU-GPU synchronization has a performance cost.

Note: Only available in local RenderingDevices.

Note: sync() can only be called after a submit().

RID texture_buffer_create(size_bytes: int, format: DataFormat, data: PackedByteArray = PackedByteArray()) 🔗

Creates a new texture buffer. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

Error texture_clear(texture: RID, color: Color, base_mipmap: int, mipmap_count: int, base_layer: int, layer_count: int) 🔗

Clears the specified texture by replacing all of its pixels with the specified color. base_mipmap and mipmap_count determine which mipmaps of the texture are affected by this clear operation, while base_layer and layer_count determine which layers of a 3D texture (or texture array) are affected by this clear operation. For 2D textures (which only have one layer by design), base_layer must be 0 and layer_count must be 1.

Note: texture can't be cleared while a draw list that uses it as part of a framebuffer is being created. Ensure the draw list is finalized (and that the color/depth texture using it is not set to FINAL_ACTION_CONTINUE) to clear this texture.

Error texture_copy(from_texture: RID, to_texture: RID, from_pos: Vector3, to_pos: Vector3, size: Vector3, src_mipmap: int, dst_mipmap: int, src_layer: int, dst_layer: int) 🔗

Copies the from_texture to to_texture with the specified from_pos, to_pos and size coordinates. The Z axis of the from_pos, to_pos and size must be 0 for 2-dimensional textures. Source and destination mipmaps/layers must also be specified, with these parameters being 0 for textures without mipmaps or single-layer textures. Returns @GlobalScope.OK if the texture copy was successful or @GlobalScope.ERR_INVALID_PARAMETER otherwise.

Note: from_texture texture can't be copied while a draw list that uses it as part of a framebuffer is being created. Ensure the draw list is finalized (and that the color/depth texture using it is not set to FINAL_ACTION_CONTINUE) to copy this texture.

Note: from_texture texture requires the TEXTURE_USAGE_CAN_COPY_FROM_BIT to be retrieved.

Note: to_texture can't be copied while a draw list that uses it as part of a framebuffer is being created. Ensure the draw list is finalized (and that the color/depth texture using it is not set to FINAL_ACTION_CONTINUE) to copy this texture.

Note: to_texture requires the TEXTURE_USAGE_CAN_COPY_TO_BIT to be retrieved.

Note: from_texture and to_texture must be of the same type (color or depth).

RID texture_create(format: RDTextureFormat, view: RDTextureView, data: Array[PackedByteArray] = []) 🔗

Creates a new texture. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

Note: data takes an Array of PackedByteArrays. For TEXTURE_TYPE_1D, TEXTURE_TYPE_2D, and TEXTURE_TYPE_3D types, this array should only have one element, a PackedByteArray containing all the data for the texture. For _ARRAY and _CUBE types, the length should be the same as the number of RDTextureFormat.array_layers in format.

Note: Not to be confused with RenderingServer.texture_2d_create(), which creates the Godot-specific Texture2D resource as opposed to the graphics API's own texture type.

RID texture_create_from_extension(type: TextureType, format: DataFormat, samples: TextureSamples, usage_flags: BitField[TextureUsageBits], image: int, width: int, height: int, depth: int, layers: int, mipmaps: int = 1) 🔗

Returns an RID for an existing image (VkImage) with the given type, format, samples, usage_flags, width, height, depth, layers, and mipmaps. This can be used to allow Godot to render onto foreign images.

RID texture_create_shared(view: RDTextureView, with_texture: RID) 🔗

Creates a shared texture using the specified view and the texture information from with_texture.

RID texture_create_shared_from_slice(view: RDTextureView, with_texture: RID, layer: int, mipmap: int, mipmaps: int = 1, slice_type: TextureSliceType = 0) 🔗

Creates a shared texture using the specified view and the texture information from with_texture's layer and mipmap. The number of included mipmaps from the original texture can be controlled using the mipmaps parameter. Only relevant for textures with multiple layers, such as 3D textures, texture arrays and cubemaps. For single-layer textures, use texture_create_shared().

For 2D textures (which only have one layer), layer must be 0.

Note: Layer slicing is only supported for 2D texture arrays, not 3D textures or cubemaps.

PackedByteArray texture_get_data(texture: RID, layer: int) 🔗

Returns the texture data for the specified layer as raw binary data. For 2D textures (which only have one layer), layer must be 0.

Note: texture can't be retrieved while a draw list that uses it as part of a framebuffer is being created. Ensure the draw list is finalized (and that the color/depth texture using it is not set to FINAL_ACTION_CONTINUE) to retrieve this texture. Otherwise, an error is printed and an empty PackedByteArray is returned.

Note: texture requires the TEXTURE_USAGE_CAN_COPY_FROM_BIT to be retrieved. Otherwise, an error is printed and an empty PackedByteArray is returned.

Note: This method will block the GPU from working until the data is retrieved. Refer to texture_get_data_async() for an alternative that returns the data in more performant way.

Error texture_get_data_async(texture: RID, layer: int, callback: Callable) 🔗

Asynchronous version of texture_get_data(). RenderingDevice will call callback in a certain amount of frames with the data the texture had at the time of the request.

Note: At the moment, the delay corresponds to the amount of frames specified by ProjectSettings.rendering/rendering_device/vsync/frame_queue_size.

Note: Downloading large textures can have a prohibitive cost for real-time even when using the asynchronous method due to hardware bandwidth limitations. When dealing with large resources, you can adjust settings such as ProjectSettings.rendering/rendering_device/staging_buffer/texture_download_region_size_px and ProjectSettings.rendering/rendering_device/staging_buffer/block_size_kb to improve the transfer speed at the cost of extra memory.

RDTextureFormat texture_get_format(texture: RID) 🔗

Returns the data format used to create this texture.

int texture_get_native_handle(texture: RID) 🔗

Deprecated: Use get_driver_resource() with DRIVER_RESOURCE_TEXTURE instead.

Returns the internal graphics handle for this texture object. For use when communicating with third-party APIs mostly with GDExtension.

Note: This function returns a uint64_t which internally maps to a GLuint (OpenGL) or VkImage (Vulkan).

bool texture_is_discardable(texture: RID) 🔗

Returns true if the texture is discardable, false otherwise. See RDTextureFormat or texture_set_discardable().

bool texture_is_format_supported_for_usage(format: DataFormat, usage_flags: BitField[TextureUsageBits]) const 🔗

Returns true if the specified format is supported for the given usage_flags, false otherwise.

bool texture_is_shared(texture: RID) 🔗

Returns true if the texture is shared, false otherwise. See RDTextureView.

bool texture_is_valid(texture: RID) 🔗

Returns true if the texture is valid, false otherwise.

Error texture_resolve_multisample(from_texture: RID, to_texture: RID) 🔗

Resolves the from_texture texture onto to_texture with multisample antialiasing enabled. This must be used when rendering a framebuffer for MSAA to work. Returns @GlobalScope.OK if successful, @GlobalScope.ERR_INVALID_PARAMETER otherwise.

Note: from_texture and to_texture textures must have the same dimension, format and type (color or depth).

Note: from_texture can't be copied while a draw list that uses it as part of a framebuffer is being created. Ensure the draw list is finalized (and that the color/depth texture using it is not set to FINAL_ACTION_CONTINUE) to resolve this texture.

Note: from_texture requires the TEXTURE_USAGE_CAN_COPY_FROM_BIT to be retrieved.

Note: from_texture must be multisampled and must also be 2D (or a slice of a 3D/cubemap texture).

Note: to_texture can't be copied while a draw list that uses it as part of a framebuffer is being created. Ensure the draw list is finalized (and that the color/depth texture using it is not set to FINAL_ACTION_CONTINUE) to resolve this texture.

Note: to_texture texture requires the TEXTURE_USAGE_CAN_COPY_TO_BIT to be retrieved.

Note: to_texture texture must not be multisampled and must also be 2D (or a slice of a 3D/cubemap texture).

void texture_set_discardable(texture: RID, discardable: bool) 🔗

Updates the discardable property of texture.

If a texture is discardable, its contents do not need to be preserved between frames. This flag is only relevant when the texture is used as target in a draw list.

This information is used by RenderingDevice to figure out if a texture's contents can be discarded, eliminating unnecessary writes to memory and boosting performance.

Error texture_update(texture: RID, layer: int, data: PackedByteArray) 🔗

Updates texture data with new data, replacing the previous data in place. The updated texture data must have the same dimensions and format. For 2D textures (which only have one layer), layer must be 0. Returns @GlobalScope.OK if the update was successful, @GlobalScope.ERR_INVALID_PARAMETER otherwise.

Note: Updating textures is forbidden during creation of a draw or compute list.

Note: The existing texture can't be updated while a draw list that uses it as part of a framebuffer is being created. Ensure the draw list is finalized (and that the color/depth texture using it is not set to FINAL_ACTION_CONTINUE) to update this texture.

Note: The existing texture requires the TEXTURE_USAGE_CAN_UPDATE_BIT to be updatable.

RID uniform_buffer_create(size_bytes: int, data: PackedByteArray = PackedByteArray(), creation_bits: BitField[BufferCreationBits] = 0) 🔗

Creates a new uniform buffer. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

RID uniform_set_create(uniforms: Array[RDUniform], shader: RID, shader_set: int) 🔗

Creates a new uniform set. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

bool uniform_set_is_valid(uniform_set: RID) 🔗

Checks if the uniform_set is valid, i.e. is owned.

RID vertex_array_create(vertex_count: int, vertex_format: int, src_buffers: Array[RID], offsets: PackedInt64Array = PackedInt64Array()) 🔗

Creates a vertex array based on the specified buffers. Optionally, offsets (in bytes) may be defined for each buffer.

RID vertex_buffer_create(size_bytes: int, data: PackedByteArray = PackedByteArray(), creation_bits: BitField[BufferCreationBits] = 0) 🔗

Creates a new vertex buffer. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingDevice's free_rid() method.

int vertex_format_create(vertex_descriptions: Array[RDVertexAttribute]) 🔗

Creates a new vertex format with the specified vertex_descriptions. Returns a unique vertex format ID corresponding to the newly created vertex format.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (typescript):
```typescript
rd = RenderingServer.get_rendering_device()

if rd.has_feature(RenderingDevice.SUPPORTS_BUFFER_DEVICE_ADDRESS):
    storage_buffer = rd.storage_buffer_create(bytes.size(), bytes, RenderingDevice.STORAGE_BUFFER_USAGE_SHADER_DEVICE_ADDRESS)
    storage_buffer_address = rd.buffer_get_device_address(storage_buffer)
```

Example 2 (typescript):
```typescript
func _buffer_get_data_callback(array):
    value = array.decode_u32(0)

...

rd.buffer_get_data_async(buffer, _buffer_get_data_callback)
```

Example 3 (gdscript):
```gdscript
var rd = RenderingDevice.new()
var compute_list = rd.compute_list_begin()

rd.compute_list_bind_compute_pipeline(compute_list, compute_shader_dilate_pipeline)
rd.compute_list_bind_uniform_set(compute_list, compute_base_uniform_set, 0)
rd.compute_list_bind_uniform_set(compute_list, dilate_uniform_set, 1)

for i in atlas_slices:
    rd.compute_list_set_push_constant(compute_list, push_constant, push_constant.size())
    rd.compute_list_dispatch(compute_list, group_size.x, group_size.y, group_size.z)
    # No barrier, let them run all together.

rd.compute_list_end()
```

Example 4 (gdscript):
```gdscript
var rd = RenderingDevice.new()
var clear_colors = PackedColorArray([Color(0, 0, 0, 0), Color(0, 0, 0, 0), Color(0, 0, 0, 0)])
var draw_list = rd.draw_list_begin(framebuffers[i], RenderingDevice.CLEAR_COLOR_ALL, clear_colors, true, 1.0f, true, 0, Rect2(), RenderingDevice.OPAQUE_PASS)

# Draw opaque.
rd.draw_list_bind_render_pipeline(draw_list, raster_pipeline)
rd.draw_list_bind_uniform_set(draw_list, raster_base_uniform, 0)
rd.draw_list_set_push_constant(draw_list, raster_push_constant, raster_push_constant.size())
rd.draw_list_draw(draw_list, false, 1, slice_triangle_count[i] * 3)
# Draw wire.
rd.draw_list_bind_render_pipeline(draw_list, raster_pipeline_wire)
rd.draw_list_bind_uniform_set(draw_list, raster_base_uniform, 0)
rd.draw_list_set_push_constant(draw_list, raster_push_constant, raster_push_constant.size())
rd.draw_list_draw(draw_list, false, 1, slice_triangle_count[i] * 3)

rd.draw_list_end()
```

---

## RenderingServer

**URL:** https://docs.godotengine.org/en/stable/classes/class_renderingserver.html

**Contents:**
- RenderingServer
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Constants
- Property Descriptions
- Method Descriptions

Server for anything visible.

The rendering server is the API backend for everything visible. The whole scene system mounts on it to display. The rendering server is completely opaque: the internals are entirely implementation-specific and cannot be accessed.

The rendering server can be used to bypass the scene/Node system entirely. This can improve performance in cases where the scene system is the bottleneck, but won't improve performance otherwise (for instance, if the GPU is already fully utilized).

Resources are created using the *_create functions. These functions return RIDs which are not references to the objects themselves, but opaque pointers towards these objects.

All objects are drawn to a viewport. You can use the Viewport attached to the SceneTree or you can create one yourself with viewport_create(). When using a custom scenario or canvas, the scenario or canvas needs to be attached to the viewport using viewport_set_scenario() or viewport_attach_canvas().

Scenarios: In 3D, all visual objects must be associated with a scenario. The scenario is a visual representation of the world. If accessing the rendering server from a running game, the scenario can be accessed from the scene tree from any Node3D node with Node3D.get_world_3d(). Otherwise, a scenario can be created with scenario_create().

Similarly, in 2D, a canvas is needed to draw all canvas items.

3D: In 3D, all visible objects are comprised of a resource and an instance. A resource can be a mesh, a particle system, a light, or any other 3D object. In order to be visible resources must be attached to an instance using instance_set_base(). The instance must also be attached to the scenario using instance_set_scenario() in order to be visible. RenderingServer methods that don't have a prefix are usually 3D-specific (but not always).

2D: In 2D, all visible objects are some form of canvas item. In order to be visible, a canvas item needs to be the child of a canvas attached to a viewport, or it needs to be the child of another canvas item that is eventually attached to the canvas. 2D-specific RenderingServer methods generally start with canvas_*.

Headless mode: Starting the engine with the --headless command line argument disables all rendering and window management functions. Most functions from RenderingServer will return dummy values in this case.

Optimization using Servers

bake_render_uv2(base: RID, material_overrides: Array[RID], image_size: Vector2i)

call_on_render_thread(callable: Callable)

camera_attributes_create()

camera_attributes_set_auto_exposure(camera_attributes: RID, enable: bool, min_sensitivity: float, max_sensitivity: float, speed: float, scale: float)

camera_attributes_set_dof_blur(camera_attributes: RID, far_enable: bool, far_distance: float, far_transition: float, near_enable: bool, near_distance: float, near_transition: float, amount: float)

camera_attributes_set_dof_blur_bokeh_shape(shape: DOFBokehShape)

camera_attributes_set_dof_blur_quality(quality: DOFBlurQuality, use_jitter: bool)

camera_attributes_set_exposure(camera_attributes: RID, multiplier: float, normalization: float)

camera_set_camera_attributes(camera: RID, effects: RID)

camera_set_compositor(camera: RID, compositor: RID)

camera_set_cull_mask(camera: RID, layers: int)

camera_set_environment(camera: RID, env: RID)

camera_set_frustum(camera: RID, size: float, offset: Vector2, z_near: float, z_far: float)

camera_set_orthogonal(camera: RID, size: float, z_near: float, z_far: float)

camera_set_perspective(camera: RID, fovy_degrees: float, z_near: float, z_far: float)

camera_set_transform(camera: RID, transform: Transform3D)

camera_set_use_vertical_aspect(camera: RID, enable: bool)

canvas_item_add_animation_slice(item: RID, animation_length: float, slice_begin: float, slice_end: float, offset: float = 0.0)

canvas_item_add_circle(item: RID, pos: Vector2, radius: float, color: Color, antialiased: bool = false)

canvas_item_add_clip_ignore(item: RID, ignore: bool)

canvas_item_add_lcd_texture_rect_region(item: RID, rect: Rect2, texture: RID, src_rect: Rect2, modulate: Color)

canvas_item_add_line(item: RID, from: Vector2, to: Vector2, color: Color, width: float = -1.0, antialiased: bool = false)

canvas_item_add_mesh(item: RID, mesh: RID, transform: Transform2D = Transform2D(1, 0, 0, 1, 0, 0), modulate: Color = Color(1, 1, 1, 1), texture: RID = RID())

canvas_item_add_msdf_texture_rect_region(item: RID, rect: Rect2, texture: RID, src_rect: Rect2, modulate: Color = Color(1, 1, 1, 1), outline_size: int = 0, px_range: float = 1.0, scale: float = 1.0)

canvas_item_add_multiline(item: RID, points: PackedVector2Array, colors: PackedColorArray, width: float = -1.0, antialiased: bool = false)

canvas_item_add_multimesh(item: RID, mesh: RID, texture: RID = RID())

canvas_item_add_nine_patch(item: RID, rect: Rect2, source: Rect2, texture: RID, topleft: Vector2, bottomright: Vector2, x_axis_mode: NinePatchAxisMode = 0, y_axis_mode: NinePatchAxisMode = 0, draw_center: bool = true, modulate: Color = Color(1, 1, 1, 1))

canvas_item_add_particles(item: RID, particles: RID, texture: RID)

canvas_item_add_polygon(item: RID, points: PackedVector2Array, colors: PackedColorArray, uvs: PackedVector2Array = PackedVector2Array(), texture: RID = RID())

canvas_item_add_polyline(item: RID, points: PackedVector2Array, colors: PackedColorArray, width: float = -1.0, antialiased: bool = false)

canvas_item_add_primitive(item: RID, points: PackedVector2Array, colors: PackedColorArray, uvs: PackedVector2Array, texture: RID)

canvas_item_add_rect(item: RID, rect: Rect2, color: Color, antialiased: bool = false)

canvas_item_add_set_transform(item: RID, transform: Transform2D)

canvas_item_add_texture_rect(item: RID, rect: Rect2, texture: RID, tile: bool = false, modulate: Color = Color(1, 1, 1, 1), transpose: bool = false)

canvas_item_add_texture_rect_region(item: RID, rect: Rect2, texture: RID, src_rect: Rect2, modulate: Color = Color(1, 1, 1, 1), transpose: bool = false, clip_uv: bool = true)

canvas_item_add_triangle_array(item: RID, indices: PackedInt32Array, points: PackedVector2Array, colors: PackedColorArray, uvs: PackedVector2Array = PackedVector2Array(), bones: PackedInt32Array = PackedInt32Array(), weights: PackedFloat32Array = PackedFloat32Array(), texture: RID = RID(), count: int = -1)

canvas_item_attach_skeleton(item: RID, skeleton: RID)

canvas_item_clear(item: RID)

canvas_item_get_instance_shader_parameter(instance: RID, parameter: StringName) const

canvas_item_get_instance_shader_parameter_default_value(instance: RID, parameter: StringName) const

canvas_item_get_instance_shader_parameter_list(instance: RID) const

canvas_item_reset_physics_interpolation(item: RID)

canvas_item_set_canvas_group_mode(item: RID, mode: CanvasGroupMode, clear_margin: float = 5.0, fit_empty: bool = false, fit_margin: float = 0.0, blur_mipmaps: bool = false)

canvas_item_set_clip(item: RID, clip: bool)

canvas_item_set_copy_to_backbuffer(item: RID, enabled: bool, rect: Rect2)

canvas_item_set_custom_rect(item: RID, use_custom_rect: bool, rect: Rect2 = Rect2(0, 0, 0, 0))

canvas_item_set_default_texture_filter(item: RID, filter: CanvasItemTextureFilter)

canvas_item_set_default_texture_repeat(item: RID, repeat: CanvasItemTextureRepeat)

canvas_item_set_distance_field_mode(item: RID, enabled: bool)

canvas_item_set_draw_behind_parent(item: RID, enabled: bool)

canvas_item_set_draw_index(item: RID, index: int)

canvas_item_set_instance_shader_parameter(instance: RID, parameter: StringName, value: Variant)

canvas_item_set_interpolated(item: RID, interpolated: bool)

canvas_item_set_light_mask(item: RID, mask: int)

canvas_item_set_material(item: RID, material: RID)

canvas_item_set_modulate(item: RID, color: Color)

canvas_item_set_parent(item: RID, parent: RID)

canvas_item_set_self_modulate(item: RID, color: Color)

canvas_item_set_sort_children_by_y(item: RID, enabled: bool)

canvas_item_set_transform(item: RID, transform: Transform2D)

canvas_item_set_use_parent_material(item: RID, enabled: bool)

canvas_item_set_visibility_layer(item: RID, visibility_layer: int)

canvas_item_set_visibility_notifier(item: RID, enable: bool, area: Rect2, enter_callable: Callable, exit_callable: Callable)

canvas_item_set_visible(item: RID, visible: bool)

canvas_item_set_z_as_relative_to_parent(item: RID, enabled: bool)

canvas_item_set_z_index(item: RID, z_index: int)

canvas_item_transform_physics_interpolation(item: RID, transform: Transform2D)

canvas_light_attach_to_canvas(light: RID, canvas: RID)

canvas_light_create()

canvas_light_occluder_attach_to_canvas(occluder: RID, canvas: RID)

canvas_light_occluder_create()

canvas_light_occluder_reset_physics_interpolation(occluder: RID)

canvas_light_occluder_set_as_sdf_collision(occluder: RID, enable: bool)

canvas_light_occluder_set_enabled(occluder: RID, enabled: bool)

canvas_light_occluder_set_interpolated(occluder: RID, interpolated: bool)

canvas_light_occluder_set_light_mask(occluder: RID, mask: int)

canvas_light_occluder_set_polygon(occluder: RID, polygon: RID)

canvas_light_occluder_set_transform(occluder: RID, transform: Transform2D)

canvas_light_occluder_transform_physics_interpolation(occluder: RID, transform: Transform2D)

canvas_light_reset_physics_interpolation(light: RID)

canvas_light_set_blend_mode(light: RID, mode: CanvasLightBlendMode)

canvas_light_set_color(light: RID, color: Color)

canvas_light_set_enabled(light: RID, enabled: bool)

canvas_light_set_energy(light: RID, energy: float)

canvas_light_set_height(light: RID, height: float)

canvas_light_set_interpolated(light: RID, interpolated: bool)

canvas_light_set_item_cull_mask(light: RID, mask: int)

canvas_light_set_item_shadow_cull_mask(light: RID, mask: int)

canvas_light_set_layer_range(light: RID, min_layer: int, max_layer: int)

canvas_light_set_mode(light: RID, mode: CanvasLightMode)

canvas_light_set_shadow_color(light: RID, color: Color)

canvas_light_set_shadow_enabled(light: RID, enabled: bool)

canvas_light_set_shadow_filter(light: RID, filter: CanvasLightShadowFilter)

canvas_light_set_shadow_smooth(light: RID, smooth: float)

canvas_light_set_texture(light: RID, texture: RID)

canvas_light_set_texture_offset(light: RID, offset: Vector2)

canvas_light_set_texture_scale(light: RID, scale: float)

canvas_light_set_transform(light: RID, transform: Transform2D)

canvas_light_set_z_range(light: RID, min_z: int, max_z: int)

canvas_light_transform_physics_interpolation(light: RID, transform: Transform2D)

canvas_occluder_polygon_create()

canvas_occluder_polygon_set_cull_mode(occluder_polygon: RID, mode: CanvasOccluderPolygonCullMode)

canvas_occluder_polygon_set_shape(occluder_polygon: RID, shape: PackedVector2Array, closed: bool)

canvas_set_disable_scale(disable: bool)

canvas_set_item_mirroring(canvas: RID, item: RID, mirroring: Vector2)

canvas_set_item_repeat(item: RID, repeat_size: Vector2, repeat_times: int)

canvas_set_modulate(canvas: RID, color: Color)

canvas_set_shadow_texture_size(size: int)

canvas_texture_create()

canvas_texture_set_channel(canvas_texture: RID, channel: CanvasTextureChannel, texture: RID)

canvas_texture_set_shading_parameters(canvas_texture: RID, base_color: Color, shininess: float)

canvas_texture_set_texture_filter(canvas_texture: RID, filter: CanvasItemTextureFilter)

canvas_texture_set_texture_repeat(canvas_texture: RID, repeat: CanvasItemTextureRepeat)

compositor_effect_create()

compositor_effect_set_callback(effect: RID, callback_type: CompositorEffectCallbackType, callback: Callable)

compositor_effect_set_enabled(effect: RID, enabled: bool)

compositor_effect_set_flag(effect: RID, flag: CompositorEffectFlags, set: bool)

compositor_set_compositor_effects(compositor: RID, effects: Array[RID])

create_local_rendering_device() const

debug_canvas_item_get_rect(item: RID)

decal_set_albedo_mix(decal: RID, albedo_mix: float)

decal_set_cull_mask(decal: RID, mask: int)

decal_set_distance_fade(decal: RID, enabled: bool, begin: float, length: float)

decal_set_emission_energy(decal: RID, energy: float)

decal_set_fade(decal: RID, above: float, below: float)

decal_set_modulate(decal: RID, color: Color)

decal_set_normal_fade(decal: RID, fade: float)

decal_set_size(decal: RID, size: Vector3)

decal_set_texture(decal: RID, type: DecalTexture, texture: RID)

decals_set_filter(filter: DecalFilter)

directional_light_create()

directional_shadow_atlas_set_size(size: int, is_16bits: bool)

directional_soft_shadow_filter_set_quality(quality: ShadowQuality)

environment_bake_panorama(environment: RID, bake_irradiance: bool, size: Vector2i)

environment_glow_set_use_bicubic_upscale(enable: bool)

environment_set_adjustment(env: RID, enable: bool, brightness: float, contrast: float, saturation: float, use_1d_color_correction: bool, color_correction: RID)

environment_set_ambient_light(env: RID, color: Color, ambient: EnvironmentAmbientSource = 0, energy: float = 1.0, sky_contribution: float = 0.0, reflection_source: EnvironmentReflectionSource = 0)

environment_set_background(env: RID, bg: EnvironmentBG)

environment_set_bg_color(env: RID, color: Color)

environment_set_bg_energy(env: RID, multiplier: float, exposure_value: float)

environment_set_camera_id(env: RID, id: int)

environment_set_canvas_max_layer(env: RID, max_layer: int)

environment_set_fog(env: RID, enable: bool, light_color: Color, light_energy: float, sun_scatter: float, density: float, height: float, height_density: float, aerial_perspective: float, sky_affect: float, fog_mode: EnvironmentFogMode = 0)

environment_set_fog_depth(env: RID, curve: float, begin: float, end: float)

environment_set_glow(env: RID, enable: bool, levels: PackedFloat32Array, intensity: float, strength: float, mix: float, bloom_threshold: float, blend_mode: EnvironmentGlowBlendMode, hdr_bleed_threshold: float, hdr_bleed_scale: float, hdr_luminance_cap: float, glow_map_strength: float, glow_map: RID)

environment_set_sdfgi(env: RID, enable: bool, cascades: int, min_cell_size: float, y_scale: EnvironmentSDFGIYScale, use_occlusion: bool, bounce_feedback: float, read_sky: bool, energy: float, normal_bias: float, probe_bias: float)

environment_set_sdfgi_frames_to_converge(frames: EnvironmentSDFGIFramesToConverge)

environment_set_sdfgi_frames_to_update_light(frames: EnvironmentSDFGIFramesToUpdateLight)

environment_set_sdfgi_ray_count(ray_count: EnvironmentSDFGIRayCount)

environment_set_sky(env: RID, sky: RID)

environment_set_sky_custom_fov(env: RID, scale: float)

environment_set_sky_orientation(env: RID, orientation: Basis)

environment_set_ssao(env: RID, enable: bool, radius: float, intensity: float, power: float, detail: float, horizon: float, sharpness: float, light_affect: float, ao_channel_affect: float)

environment_set_ssao_quality(quality: EnvironmentSSAOQuality, half_size: bool, adaptive_target: float, blur_passes: int, fadeout_from: float, fadeout_to: float)

environment_set_ssil_quality(quality: EnvironmentSSILQuality, half_size: bool, adaptive_target: float, blur_passes: int, fadeout_from: float, fadeout_to: float)

environment_set_ssr(env: RID, enable: bool, max_steps: int, fade_in: float, fade_out: float, depth_tolerance: float)

environment_set_ssr_roughness_quality(quality: EnvironmentSSRRoughnessQuality)

environment_set_tonemap(env: RID, tone_mapper: EnvironmentToneMapper, exposure: float, white: float)

environment_set_volumetric_fog(env: RID, enable: bool, density: float, albedo: Color, emission: Color, emission_energy: float, anisotropy: float, length: float, p_detail_spread: float, gi_inject: float, temporal_reprojection: bool, temporal_reprojection_amount: float, ambient_inject: float, sky_affect: float)

environment_set_volumetric_fog_filter_active(active: bool)

environment_set_volumetric_fog_volume_size(size: int, depth: int)

fog_volume_set_material(fog_volume: RID, material: RID)

fog_volume_set_shape(fog_volume: RID, shape: FogVolumeShape)

fog_volume_set_size(fog_volume: RID, size: Vector3)

force_draw(swap_buffers: bool = true, frame_step: float = 0.0)

get_current_rendering_driver_name() const

get_current_rendering_method() const

get_default_clear_color()

get_frame_setup_time_cpu() const

get_rendering_device() const

get_rendering_info(info: RenderingInfo)

get_shader_parameter_list(shader: RID) const

get_video_adapter_api_version() const

get_video_adapter_name() const

get_video_adapter_type() const

get_video_adapter_vendor() const

gi_set_use_half_resolution(half_resolution: bool)

global_shader_parameter_add(name: StringName, type: GlobalShaderParameterType, default_value: Variant)

global_shader_parameter_get(name: StringName) const

global_shader_parameter_get_list() const

GlobalShaderParameterType

global_shader_parameter_get_type(name: StringName) const

global_shader_parameter_remove(name: StringName)

global_shader_parameter_set(name: StringName, value: Variant)

global_shader_parameter_set_override(name: StringName, value: Variant)

has_feature(feature: Features) const

has_os_feature(feature: String) const

instance_attach_object_instance_id(instance: RID, id: int)

instance_attach_skeleton(instance: RID, skeleton: RID)

instance_create2(base: RID, scenario: RID)

instance_geometry_get_shader_parameter(instance: RID, parameter: StringName) const

instance_geometry_get_shader_parameter_default_value(instance: RID, parameter: StringName) const

instance_geometry_get_shader_parameter_list(instance: RID) const

instance_geometry_set_cast_shadows_setting(instance: RID, shadow_casting_setting: ShadowCastingSetting)

instance_geometry_set_flag(instance: RID, flag: InstanceFlags, enabled: bool)

instance_geometry_set_lightmap(instance: RID, lightmap: RID, lightmap_uv_scale: Rect2, lightmap_slice: int)

instance_geometry_set_lod_bias(instance: RID, lod_bias: float)

instance_geometry_set_material_overlay(instance: RID, material: RID)

instance_geometry_set_material_override(instance: RID, material: RID)

instance_geometry_set_shader_parameter(instance: RID, parameter: StringName, value: Variant)

instance_geometry_set_transparency(instance: RID, transparency: float)

instance_geometry_set_visibility_range(instance: RID, min: float, max: float, min_margin: float, max_margin: float, fade_mode: VisibilityRangeFadeMode)

instance_set_base(instance: RID, base: RID)

instance_set_blend_shape_weight(instance: RID, shape: int, weight: float)

instance_set_custom_aabb(instance: RID, aabb: AABB)

instance_set_extra_visibility_margin(instance: RID, margin: float)

instance_set_ignore_culling(instance: RID, enabled: bool)

instance_set_layer_mask(instance: RID, mask: int)

instance_set_pivot_data(instance: RID, sorting_offset: float, use_aabb_center: bool)

instance_set_scenario(instance: RID, scenario: RID)

instance_set_surface_override_material(instance: RID, surface: int, material: RID)

instance_set_transform(instance: RID, transform: Transform3D)

instance_set_visibility_parent(instance: RID, parent: RID)

instance_set_visible(instance: RID, visible: bool)

instance_teleport(instance: RID)

instances_cull_aabb(aabb: AABB, scenario: RID = RID()) const

instances_cull_convex(convex: Array[Plane], scenario: RID = RID()) const

instances_cull_ray(from: Vector3, to: Vector3, scenario: RID = RID()) const

is_on_render_thread()

light_directional_set_blend_splits(light: RID, enable: bool)

light_directional_set_shadow_mode(light: RID, mode: LightDirectionalShadowMode)

light_directional_set_sky_mode(light: RID, mode: LightDirectionalSkyMode)

light_omni_set_shadow_mode(light: RID, mode: LightOmniShadowMode)

light_projectors_set_filter(filter: LightProjectorFilter)

light_set_bake_mode(light: RID, bake_mode: LightBakeMode)

light_set_color(light: RID, color: Color)

light_set_cull_mask(light: RID, mask: int)

light_set_distance_fade(decal: RID, enabled: bool, begin: float, shadow: float, length: float)

light_set_max_sdfgi_cascade(light: RID, cascade: int)

light_set_negative(light: RID, enable: bool)

light_set_param(light: RID, param: LightParam, value: float)

light_set_projector(light: RID, texture: RID)

light_set_reverse_cull_face_mode(light: RID, enabled: bool)

light_set_shadow(light: RID, enabled: bool)

light_set_shadow_caster_mask(light: RID, mask: int)

lightmap_get_probe_capture_bsp_tree(lightmap: RID) const

lightmap_get_probe_capture_points(lightmap: RID) const

lightmap_get_probe_capture_sh(lightmap: RID) const

lightmap_get_probe_capture_tetrahedra(lightmap: RID) const

lightmap_set_baked_exposure_normalization(lightmap: RID, baked_exposure: float)

lightmap_set_probe_bounds(lightmap: RID, bounds: AABB)

lightmap_set_probe_capture_data(lightmap: RID, points: PackedVector3Array, point_sh: PackedColorArray, tetrahedra: PackedInt32Array, bsp_tree: PackedInt32Array)

lightmap_set_probe_capture_update_speed(speed: float)

lightmap_set_probe_interior(lightmap: RID, interior: bool)

lightmap_set_textures(lightmap: RID, light: RID, uses_sh: bool)

lightmaps_set_bicubic_filter(enable: bool)

make_sphere_mesh(latitudes: int, longitudes: int, radius: float)

material_get_param(material: RID, parameter: StringName) const

material_set_next_pass(material: RID, next_material: RID)

material_set_param(material: RID, parameter: StringName, value: Variant)

material_set_render_priority(material: RID, priority: int)

material_set_shader(shader_material: RID, shader: RID)

mesh_add_surface(mesh: RID, surface: Dictionary)

mesh_add_surface_from_arrays(mesh: RID, primitive: PrimitiveType, arrays: Array, blend_shapes: Array = [], lods: Dictionary = {}, compress_format: BitField[ArrayFormat] = 0)

mesh_clear(mesh: RID)

mesh_create_from_surfaces(surfaces: Array[Dictionary], blend_shape_count: int = 0)

mesh_get_blend_shape_count(mesh: RID) const

mesh_get_blend_shape_mode(mesh: RID) const

mesh_get_custom_aabb(mesh: RID) const

mesh_get_surface(mesh: RID, surface: int)

mesh_get_surface_count(mesh: RID) const

mesh_set_blend_shape_mode(mesh: RID, mode: BlendShapeMode)

mesh_set_custom_aabb(mesh: RID, aabb: AABB)

mesh_set_shadow_mesh(mesh: RID, shadow_mesh: RID)

mesh_surface_get_arrays(mesh: RID, surface: int) const

mesh_surface_get_blend_shape_arrays(mesh: RID, surface: int) const

mesh_surface_get_format_attribute_stride(format: BitField[ArrayFormat], vertex_count: int) const

mesh_surface_get_format_index_stride(format: BitField[ArrayFormat], vertex_count: int) const

mesh_surface_get_format_normal_tangent_stride(format: BitField[ArrayFormat], vertex_count: int) const

mesh_surface_get_format_offset(format: BitField[ArrayFormat], vertex_count: int, array_index: int) const

mesh_surface_get_format_skin_stride(format: BitField[ArrayFormat], vertex_count: int) const

mesh_surface_get_format_vertex_stride(format: BitField[ArrayFormat], vertex_count: int) const

mesh_surface_get_material(mesh: RID, surface: int) const

mesh_surface_remove(mesh: RID, surface: int)

mesh_surface_set_material(mesh: RID, surface: int, material: RID)

mesh_surface_update_attribute_region(mesh: RID, surface: int, offset: int, data: PackedByteArray)

mesh_surface_update_index_region(mesh: RID, surface: int, offset: int, data: PackedByteArray)

mesh_surface_update_skin_region(mesh: RID, surface: int, offset: int, data: PackedByteArray)

mesh_surface_update_vertex_region(mesh: RID, surface: int, offset: int, data: PackedByteArray)

multimesh_allocate_data(multimesh: RID, instances: int, transform_format: MultimeshTransformFormat, color_format: bool = false, custom_data_format: bool = false, use_indirect: bool = false)

multimesh_get_aabb(multimesh: RID) const

multimesh_get_buffer(multimesh: RID) const

multimesh_get_buffer_rd_rid(multimesh: RID) const

multimesh_get_command_buffer_rd_rid(multimesh: RID) const

multimesh_get_custom_aabb(multimesh: RID) const

multimesh_get_instance_count(multimesh: RID) const

multimesh_get_mesh(multimesh: RID) const

multimesh_get_visible_instances(multimesh: RID) const

multimesh_instance_get_color(multimesh: RID, index: int) const

multimesh_instance_get_custom_data(multimesh: RID, index: int) const

multimesh_instance_get_transform(multimesh: RID, index: int) const

multimesh_instance_get_transform_2d(multimesh: RID, index: int) const

multimesh_instance_reset_physics_interpolation(multimesh: RID, index: int)

multimesh_instance_set_color(multimesh: RID, index: int, color: Color)

multimesh_instance_set_custom_data(multimesh: RID, index: int, custom_data: Color)

multimesh_instance_set_transform(multimesh: RID, index: int, transform: Transform3D)

multimesh_instance_set_transform_2d(multimesh: RID, index: int, transform: Transform2D)

multimesh_set_buffer(multimesh: RID, buffer: PackedFloat32Array)

multimesh_set_buffer_interpolated(multimesh: RID, buffer: PackedFloat32Array, buffer_previous: PackedFloat32Array)

multimesh_set_custom_aabb(multimesh: RID, aabb: AABB)

multimesh_set_mesh(multimesh: RID, mesh: RID)

multimesh_set_physics_interpolated(multimesh: RID, interpolated: bool)

multimesh_set_physics_interpolation_quality(multimesh: RID, quality: MultimeshPhysicsInterpolationQuality)

multimesh_set_visible_instances(multimesh: RID, visible: int)

occluder_set_mesh(occluder: RID, vertices: PackedVector3Array, indices: PackedInt32Array)

particles_collision_create()

particles_collision_height_field_update(particles_collision: RID)

particles_collision_set_attractor_attenuation(particles_collision: RID, curve: float)

particles_collision_set_attractor_directionality(particles_collision: RID, amount: float)

particles_collision_set_attractor_strength(particles_collision: RID, strength: float)

particles_collision_set_box_extents(particles_collision: RID, extents: Vector3)

particles_collision_set_collision_type(particles_collision: RID, type: ParticlesCollisionType)

particles_collision_set_cull_mask(particles_collision: RID, mask: int)

particles_collision_set_field_texture(particles_collision: RID, texture: RID)

particles_collision_set_height_field_mask(particles_collision: RID, mask: int)

particles_collision_set_height_field_resolution(particles_collision: RID, resolution: ParticlesCollisionHeightfieldResolution)

particles_collision_set_sphere_radius(particles_collision: RID, radius: float)

particles_emit(particles: RID, transform: Transform3D, velocity: Vector3, color: Color, custom: Color, emit_flags: int)

particles_get_current_aabb(particles: RID)

particles_get_emitting(particles: RID)

particles_is_inactive(particles: RID)

particles_request_process(particles: RID)

particles_request_process_time(particles: RID, time: float)

particles_restart(particles: RID)

particles_set_amount(particles: RID, amount: int)

particles_set_amount_ratio(particles: RID, ratio: float)

particles_set_collision_base_size(particles: RID, size: float)

particles_set_custom_aabb(particles: RID, aabb: AABB)

particles_set_draw_order(particles: RID, order: ParticlesDrawOrder)

particles_set_draw_pass_mesh(particles: RID, pass: int, mesh: RID)

particles_set_draw_passes(particles: RID, count: int)

particles_set_emission_transform(particles: RID, transform: Transform3D)

particles_set_emitter_velocity(particles: RID, velocity: Vector3)

particles_set_emitting(particles: RID, emitting: bool)

particles_set_explosiveness_ratio(particles: RID, ratio: float)

particles_set_fixed_fps(particles: RID, fps: int)

particles_set_fractional_delta(particles: RID, enable: bool)

particles_set_interp_to_end(particles: RID, factor: float)

particles_set_interpolate(particles: RID, enable: bool)

particles_set_lifetime(particles: RID, lifetime: float)

particles_set_mode(particles: RID, mode: ParticlesMode)

particles_set_one_shot(particles: RID, one_shot: bool)

particles_set_pre_process_time(particles: RID, time: float)

particles_set_process_material(particles: RID, material: RID)

particles_set_randomness_ratio(particles: RID, ratio: float)

particles_set_speed_scale(particles: RID, scale: float)

particles_set_subemitter(particles: RID, subemitter_particles: RID)

particles_set_trail_bind_poses(particles: RID, bind_poses: Array[Transform3D])

particles_set_trails(particles: RID, enable: bool, length_sec: float)

particles_set_transform_align(particles: RID, align: ParticlesTransformAlign)

particles_set_use_local_coordinates(particles: RID, enable: bool)

positional_soft_shadow_filter_set_quality(quality: ShadowQuality)

reflection_probe_create()

reflection_probe_set_ambient_color(probe: RID, color: Color)

reflection_probe_set_ambient_energy(probe: RID, energy: float)

reflection_probe_set_ambient_mode(probe: RID, mode: ReflectionProbeAmbientMode)

reflection_probe_set_as_interior(probe: RID, enable: bool)

reflection_probe_set_blend_distance(probe: RID, blend_distance: float)

reflection_probe_set_cull_mask(probe: RID, layers: int)

reflection_probe_set_enable_box_projection(probe: RID, enable: bool)

reflection_probe_set_enable_shadows(probe: RID, enable: bool)

reflection_probe_set_intensity(probe: RID, intensity: float)

reflection_probe_set_max_distance(probe: RID, distance: float)

reflection_probe_set_mesh_lod_threshold(probe: RID, pixels: float)

reflection_probe_set_origin_offset(probe: RID, offset: Vector3)

reflection_probe_set_reflection_mask(probe: RID, layers: int)

reflection_probe_set_resolution(probe: RID, resolution: int)

reflection_probe_set_size(probe: RID, size: Vector3)

reflection_probe_set_update_mode(probe: RID, mode: ReflectionProbeUpdateMode)

request_frame_drawn_callback(callable: Callable)

scenario_set_camera_attributes(scenario: RID, effects: RID)

scenario_set_compositor(scenario: RID, compositor: RID)

scenario_set_environment(scenario: RID, environment: RID)

scenario_set_fallback_environment(scenario: RID, environment: RID)

screen_space_roughness_limiter_set_active(enable: bool, amount: float, limit: float)

set_boot_image(image: Image, color: Color, scale: bool, use_filter: bool = true)

set_debug_generate_wireframes(generate: bool)

set_default_clear_color(color: Color)

shader_get_code(shader: RID) const

shader_get_default_texture_parameter(shader: RID, name: StringName, index: int = 0) const

shader_get_parameter_default(shader: RID, name: StringName) const

shader_set_code(shader: RID, code: String)

shader_set_default_texture_parameter(shader: RID, name: StringName, texture: RID, index: int = 0)

shader_set_path_hint(shader: RID, path: String)

skeleton_allocate_data(skeleton: RID, bones: int, is_2d_skeleton: bool = false)

skeleton_bone_get_transform(skeleton: RID, bone: int) const

skeleton_bone_get_transform_2d(skeleton: RID, bone: int) const

skeleton_bone_set_transform(skeleton: RID, bone: int, transform: Transform3D)

skeleton_bone_set_transform_2d(skeleton: RID, bone: int, transform: Transform2D)

skeleton_get_bone_count(skeleton: RID) const

skeleton_set_base_transform_2d(skeleton: RID, base_transform: Transform2D)

sky_bake_panorama(sky: RID, energy: float, bake_irradiance: bool, size: Vector2i)

sky_set_material(sky: RID, material: RID)

sky_set_mode(sky: RID, mode: SkyMode)

sky_set_radiance_size(sky: RID, radiance_size: int)

sub_surface_scattering_set_quality(quality: SubSurfaceScatteringQuality)

sub_surface_scattering_set_scale(scale: float, depth_scale: float)

texture_2d_create(image: Image)

texture_2d_get(texture: RID) const

texture_2d_layer_get(texture: RID, layer: int) const

texture_2d_layered_create(layers: Array[Image], layered_type: TextureLayeredType)

texture_2d_layered_placeholder_create(layered_type: TextureLayeredType)

texture_2d_placeholder_create()

texture_2d_update(texture: RID, image: Image, layer: int)

texture_3d_create(format: Format, width: int, height: int, depth: int, mipmaps: bool, data: Array[Image])

texture_3d_get(texture: RID) const

texture_3d_placeholder_create()

texture_3d_update(texture: RID, data: Array[Image])

texture_create_from_native_handle(type: TextureType, format: Format, native_handle: int, width: int, height: int, depth: int, layers: int = 1, layered_type: TextureLayeredType = 0)

texture_get_format(texture: RID) const

texture_get_native_handle(texture: RID, srgb: bool = false) const

texture_get_path(texture: RID) const

texture_get_rd_texture(texture: RID, srgb: bool = false) const

texture_proxy_create(base: RID)

texture_proxy_update(texture: RID, proxy_to: RID)

texture_rd_create(rd_texture: RID, layer_type: TextureLayeredType = 0)

texture_replace(texture: RID, by_texture: RID)

texture_set_force_redraw_if_visible(texture: RID, enable: bool)

texture_set_path(texture: RID, path: String)

texture_set_size_override(texture: RID, width: int, height: int)

viewport_attach_camera(viewport: RID, camera: RID)

viewport_attach_canvas(viewport: RID, canvas: RID)

viewport_attach_to_screen(viewport: RID, rect: Rect2 = Rect2(0, 0, 0, 0), screen: int = 0)

viewport_get_measured_render_time_cpu(viewport: RID) const

viewport_get_measured_render_time_gpu(viewport: RID) const

viewport_get_render_info(viewport: RID, type: ViewportRenderInfoType, info: ViewportRenderInfo)

viewport_get_render_target(viewport: RID) const

viewport_get_texture(viewport: RID) const

viewport_get_update_mode(viewport: RID) const

viewport_remove_canvas(viewport: RID, canvas: RID)

viewport_set_active(viewport: RID, active: bool)

viewport_set_anisotropic_filtering_level(viewport: RID, anisotropic_filtering_level: ViewportAnisotropicFiltering)

viewport_set_canvas_cull_mask(viewport: RID, canvas_cull_mask: int)

viewport_set_canvas_stacking(viewport: RID, canvas: RID, layer: int, sublayer: int)

viewport_set_canvas_transform(viewport: RID, canvas: RID, offset: Transform2D)

viewport_set_clear_mode(viewport: RID, clear_mode: ViewportClearMode)

viewport_set_debug_draw(viewport: RID, draw: ViewportDebugDraw)

viewport_set_default_canvas_item_texture_filter(viewport: RID, filter: CanvasItemTextureFilter)

viewport_set_default_canvas_item_texture_repeat(viewport: RID, repeat: CanvasItemTextureRepeat)

viewport_set_disable_2d(viewport: RID, disable: bool)

viewport_set_disable_3d(viewport: RID, disable: bool)

viewport_set_environment_mode(viewport: RID, mode: ViewportEnvironmentMode)

viewport_set_fsr_sharpness(viewport: RID, sharpness: float)

viewport_set_global_canvas_transform(viewport: RID, transform: Transform2D)

viewport_set_measure_render_time(viewport: RID, enable: bool)

viewport_set_msaa_2d(viewport: RID, msaa: ViewportMSAA)

viewport_set_msaa_3d(viewport: RID, msaa: ViewportMSAA)

viewport_set_occlusion_culling_build_quality(quality: ViewportOcclusionCullingBuildQuality)

viewport_set_occlusion_rays_per_thread(rays_per_thread: int)

viewport_set_parent_viewport(viewport: RID, parent_viewport: RID)

viewport_set_positional_shadow_atlas_quadrant_subdivision(viewport: RID, quadrant: int, subdivision: int)

viewport_set_positional_shadow_atlas_size(viewport: RID, size: int, use_16_bits: bool = false)

viewport_set_render_direct_to_screen(viewport: RID, enabled: bool)

viewport_set_scaling_3d_mode(viewport: RID, scaling_3d_mode: ViewportScaling3DMode)

viewport_set_scaling_3d_scale(viewport: RID, scale: float)

viewport_set_scenario(viewport: RID, scenario: RID)

viewport_set_screen_space_aa(viewport: RID, mode: ViewportScreenSpaceAA)

viewport_set_sdf_oversize_and_scale(viewport: RID, oversize: ViewportSDFOversize, scale: ViewportSDFScale)

viewport_set_size(viewport: RID, width: int, height: int)

viewport_set_snap_2d_transforms_to_pixel(viewport: RID, enabled: bool)

viewport_set_snap_2d_vertices_to_pixel(viewport: RID, enabled: bool)

viewport_set_texture_mipmap_bias(viewport: RID, mipmap_bias: float)

viewport_set_transparent_background(viewport: RID, enabled: bool)

viewport_set_update_mode(viewport: RID, update_mode: ViewportUpdateMode)

viewport_set_use_debanding(viewport: RID, enable: bool)

viewport_set_use_hdr_2d(viewport: RID, enabled: bool)

viewport_set_use_occlusion_culling(viewport: RID, enable: bool)

viewport_set_use_taa(viewport: RID, enable: bool)

viewport_set_use_xr(viewport: RID, use_xr: bool)

viewport_set_vrs_mode(viewport: RID, mode: ViewportVRSMode)

viewport_set_vrs_texture(viewport: RID, texture: RID)

viewport_set_vrs_update_mode(viewport: RID, mode: ViewportVRSUpdateMode)

visibility_notifier_create()

visibility_notifier_set_aabb(notifier: RID, aabb: AABB)

visibility_notifier_set_callbacks(notifier: RID, enter_callable: Callable, exit_callable: Callable)

voxel_gi_allocate_data(voxel_gi: RID, to_cell_xform: Transform3D, aabb: AABB, octree_size: Vector3i, octree_cells: PackedByteArray, data_cells: PackedByteArray, distance_field: PackedByteArray, level_counts: PackedInt32Array)

voxel_gi_get_data_cells(voxel_gi: RID) const

voxel_gi_get_distance_field(voxel_gi: RID) const

voxel_gi_get_level_counts(voxel_gi: RID) const

voxel_gi_get_octree_cells(voxel_gi: RID) const

voxel_gi_get_octree_size(voxel_gi: RID) const

voxel_gi_get_to_cell_xform(voxel_gi: RID) const

voxel_gi_set_baked_exposure_normalization(voxel_gi: RID, baked_exposure: float)

voxel_gi_set_bias(voxel_gi: RID, bias: float)

voxel_gi_set_dynamic_range(voxel_gi: RID, range: float)

voxel_gi_set_energy(voxel_gi: RID, energy: float)

voxel_gi_set_interior(voxel_gi: RID, enable: bool)

voxel_gi_set_normal_bias(voxel_gi: RID, bias: float)

voxel_gi_set_propagation(voxel_gi: RID, amount: float)

voxel_gi_set_quality(quality: VoxelGIQuality)

voxel_gi_set_use_two_bounces(voxel_gi: RID, enable: bool)

Emitted at the end of the frame, after the RenderingServer has finished updating all the Viewports.

Emitted at the beginning of the frame, before the RenderingServer updates all the Viewports.

TextureType TEXTURE_TYPE_2D = 0

TextureType TEXTURE_TYPE_LAYERED = 1

TextureType TEXTURE_TYPE_3D = 2

enum TextureLayeredType: 🔗

TextureLayeredType TEXTURE_LAYERED_2D_ARRAY = 0

Array of 2-dimensional textures (see Texture2DArray).

TextureLayeredType TEXTURE_LAYERED_CUBEMAP = 1

Cubemap texture (see Cubemap).

TextureLayeredType TEXTURE_LAYERED_CUBEMAP_ARRAY = 2

Array of cubemap textures (see CubemapArray).

CubeMapLayer CUBEMAP_LAYER_LEFT = 0

Left face of a Cubemap.

CubeMapLayer CUBEMAP_LAYER_RIGHT = 1

Right face of a Cubemap.

CubeMapLayer CUBEMAP_LAYER_BOTTOM = 2

Bottom face of a Cubemap.

CubeMapLayer CUBEMAP_LAYER_TOP = 3

Top face of a Cubemap.

CubeMapLayer CUBEMAP_LAYER_FRONT = 4

Front face of a Cubemap.

CubeMapLayer CUBEMAP_LAYER_BACK = 5

Back face of a Cubemap.

ShaderMode SHADER_SPATIAL = 0

Shader is a 3D shader.

ShaderMode SHADER_CANVAS_ITEM = 1

Shader is a 2D shader.

ShaderMode SHADER_PARTICLES = 2

Shader is a particle shader (can be used in both 2D and 3D).

ShaderMode SHADER_SKY = 3

Shader is a 3D sky shader.

ShaderMode SHADER_FOG = 4

Shader is a 3D fog shader.

ShaderMode SHADER_MAX = 5

Represents the size of the ShaderMode enum.

ArrayType ARRAY_VERTEX = 0

Array is a vertex position array.

ArrayType ARRAY_NORMAL = 1

Array is a normal array.

ArrayType ARRAY_TANGENT = 2

Array is a tangent array.

ArrayType ARRAY_COLOR = 3

Array is a vertex color array.

ArrayType ARRAY_TEX_UV = 4

Array is a UV coordinates array.

ArrayType ARRAY_TEX_UV2 = 5

Array is a UV coordinates array for the second set of UV coordinates.

ArrayType ARRAY_CUSTOM0 = 6

Array is a custom data array for the first set of custom data.

ArrayType ARRAY_CUSTOM1 = 7

Array is a custom data array for the second set of custom data.

ArrayType ARRAY_CUSTOM2 = 8

Array is a custom data array for the third set of custom data.

ArrayType ARRAY_CUSTOM3 = 9

Array is a custom data array for the fourth set of custom data.

ArrayType ARRAY_BONES = 10

Array contains bone information.

ArrayType ARRAY_WEIGHTS = 11

Array is weight information.

ArrayType ARRAY_INDEX = 12

Array is an index array.

ArrayType ARRAY_MAX = 13

Represents the size of the ArrayType enum.

enum ArrayCustomFormat: 🔗

ArrayCustomFormat ARRAY_CUSTOM_RGBA8_UNORM = 0

Custom data array contains 8-bit-per-channel red/green/blue/alpha color data. Values are normalized, unsigned floating-point in the [0.0, 1.0] range.

ArrayCustomFormat ARRAY_CUSTOM_RGBA8_SNORM = 1

Custom data array contains 8-bit-per-channel red/green/blue/alpha color data. Values are normalized, signed floating-point in the [-1.0, 1.0] range.

ArrayCustomFormat ARRAY_CUSTOM_RG_HALF = 2

Custom data array contains 16-bit-per-channel red/green color data. Values are floating-point in half precision.

ArrayCustomFormat ARRAY_CUSTOM_RGBA_HALF = 3

Custom data array contains 16-bit-per-channel red/green/blue/alpha color data. Values are floating-point in half precision.

ArrayCustomFormat ARRAY_CUSTOM_R_FLOAT = 4

Custom data array contains 32-bit-per-channel red color data. Values are floating-point in single precision.

ArrayCustomFormat ARRAY_CUSTOM_RG_FLOAT = 5

Custom data array contains 32-bit-per-channel red/green color data. Values are floating-point in single precision.

ArrayCustomFormat ARRAY_CUSTOM_RGB_FLOAT = 6

Custom data array contains 32-bit-per-channel red/green/blue color data. Values are floating-point in single precision.

ArrayCustomFormat ARRAY_CUSTOM_RGBA_FLOAT = 7

Custom data array contains 32-bit-per-channel red/green/blue/alpha color data. Values are floating-point in single precision.

ArrayCustomFormat ARRAY_CUSTOM_MAX = 8

Represents the size of the ArrayCustomFormat enum.

ArrayFormat ARRAY_FORMAT_VERTEX = 1

Flag used to mark a vertex position array.

ArrayFormat ARRAY_FORMAT_NORMAL = 2

Flag used to mark a normal array.

ArrayFormat ARRAY_FORMAT_TANGENT = 4

Flag used to mark a tangent array.

ArrayFormat ARRAY_FORMAT_COLOR = 8

Flag used to mark a vertex color array.

ArrayFormat ARRAY_FORMAT_TEX_UV = 16

Flag used to mark a UV coordinates array.

ArrayFormat ARRAY_FORMAT_TEX_UV2 = 32

Flag used to mark a UV coordinates array for the second UV coordinates.

ArrayFormat ARRAY_FORMAT_CUSTOM0 = 64

Flag used to mark an array of custom per-vertex data for the first set of custom data.

ArrayFormat ARRAY_FORMAT_CUSTOM1 = 128

Flag used to mark an array of custom per-vertex data for the second set of custom data.

ArrayFormat ARRAY_FORMAT_CUSTOM2 = 256

Flag used to mark an array of custom per-vertex data for the third set of custom data.

ArrayFormat ARRAY_FORMAT_CUSTOM3 = 512

Flag used to mark an array of custom per-vertex data for the fourth set of custom data.

ArrayFormat ARRAY_FORMAT_BONES = 1024

Flag used to mark a bone information array.

ArrayFormat ARRAY_FORMAT_WEIGHTS = 2048

Flag used to mark a weights array.

ArrayFormat ARRAY_FORMAT_INDEX = 4096

Flag used to mark an index array.

ArrayFormat ARRAY_FORMAT_BLEND_SHAPE_MASK = 7

Mask of mesh channels permitted in blend shapes.

ArrayFormat ARRAY_FORMAT_CUSTOM_BASE = 13

Shift of first custom channel.

ArrayFormat ARRAY_FORMAT_CUSTOM_BITS = 3

Number of format bits per custom channel. See ArrayCustomFormat.

ArrayFormat ARRAY_FORMAT_CUSTOM0_SHIFT = 13

Amount to shift ArrayCustomFormat for custom channel index 0.

ArrayFormat ARRAY_FORMAT_CUSTOM1_SHIFT = 16

Amount to shift ArrayCustomFormat for custom channel index 1.

ArrayFormat ARRAY_FORMAT_CUSTOM2_SHIFT = 19

Amount to shift ArrayCustomFormat for custom channel index 2.

ArrayFormat ARRAY_FORMAT_CUSTOM3_SHIFT = 22

Amount to shift ArrayCustomFormat for custom channel index 3.

ArrayFormat ARRAY_FORMAT_CUSTOM_MASK = 7

Mask of custom format bits per custom channel. Must be shifted by one of the SHIFT constants. See ArrayCustomFormat.

ArrayFormat ARRAY_COMPRESS_FLAGS_BASE = 25

Shift of first compress flag. Compress flags should be passed to ArrayMesh.add_surface_from_arrays() and SurfaceTool.commit().

ArrayFormat ARRAY_FLAG_USE_2D_VERTICES = 33554432

Flag used to mark that the array contains 2D vertices.

ArrayFormat ARRAY_FLAG_USE_DYNAMIC_UPDATE = 67108864

Flag used to mark that the mesh data will use GL_DYNAMIC_DRAW on GLES. Unused on Vulkan.

ArrayFormat ARRAY_FLAG_USE_8_BONE_WEIGHTS = 134217728

Flag used to mark that the array uses 8 bone weights instead of 4.

ArrayFormat ARRAY_FLAG_USES_EMPTY_VERTEX_ARRAY = 268435456

Flag used to mark that the mesh does not have a vertex array and instead will infer vertex positions in the shader using indices and other information.

ArrayFormat ARRAY_FLAG_COMPRESS_ATTRIBUTES = 536870912

Flag used to mark that a mesh is using compressed attributes (vertices, normals, tangents, UVs). When this form of compression is enabled, vertex positions will be packed into an RGBA16UNORM attribute and scaled in the vertex shader. The normal and tangent will be packed into an RG16UNORM representing an axis, and a 16-bit float stored in the A-channel of the vertex. UVs will use 16-bit normalized floats instead of full 32-bit signed floats. When using this compression mode you must use either vertices, normals, and tangents or only vertices. You cannot use normals without tangents. Importers will automatically enable this compression if they can.

ArrayFormat ARRAY_FLAG_FORMAT_VERSION_BASE = 35

Flag used to mark the start of the bits used to store the mesh version.

ArrayFormat ARRAY_FLAG_FORMAT_VERSION_SHIFT = 35

Flag used to shift a mesh format int to bring the version into the lowest digits.

ArrayFormat ARRAY_FLAG_FORMAT_VERSION_1 = 0

Flag used to record the format used by prior mesh versions before the introduction of a version.

ArrayFormat ARRAY_FLAG_FORMAT_VERSION_2 = 34359738368

Flag used to record the second iteration of the mesh version flag. The primary difference between this and ARRAY_FLAG_FORMAT_VERSION_1 is that this version supports ARRAY_FLAG_COMPRESS_ATTRIBUTES and in this version vertex positions are de-interleaved from normals and tangents.

ArrayFormat ARRAY_FLAG_FORMAT_CURRENT_VERSION = 34359738368

Flag used to record the current version that the engine expects. Currently this is the same as ARRAY_FLAG_FORMAT_VERSION_2.

ArrayFormat ARRAY_FLAG_FORMAT_VERSION_MASK = 255

Flag used to isolate the bits used for mesh version after using ARRAY_FLAG_FORMAT_VERSION_SHIFT to shift them into place.

enum PrimitiveType: 🔗

PrimitiveType PRIMITIVE_POINTS = 0

Primitive to draw consists of points.

PrimitiveType PRIMITIVE_LINES = 1

Primitive to draw consists of lines.

PrimitiveType PRIMITIVE_LINE_STRIP = 2

Primitive to draw consists of a line strip from start to end.

PrimitiveType PRIMITIVE_TRIANGLES = 3

Primitive to draw consists of triangles.

PrimitiveType PRIMITIVE_TRIANGLE_STRIP = 4

Primitive to draw consists of a triangle strip (the last 3 vertices are always combined to make a triangle).

PrimitiveType PRIMITIVE_MAX = 5

Represents the size of the PrimitiveType enum.

enum BlendShapeMode: 🔗

BlendShapeMode BLEND_SHAPE_MODE_NORMALIZED = 0

Blend shapes are normalized.

BlendShapeMode BLEND_SHAPE_MODE_RELATIVE = 1

Blend shapes are relative to base weight.

enum MultimeshTransformFormat: 🔗

MultimeshTransformFormat MULTIMESH_TRANSFORM_2D = 0

Use Transform2D to store MultiMesh transform.

MultimeshTransformFormat MULTIMESH_TRANSFORM_3D = 1

Use Transform3D to store MultiMesh transform.

enum MultimeshPhysicsInterpolationQuality: 🔗

MultimeshPhysicsInterpolationQuality MULTIMESH_INTERP_QUALITY_FAST = 0

MultiMesh physics interpolation favors speed over quality.

MultimeshPhysicsInterpolationQuality MULTIMESH_INTERP_QUALITY_HIGH = 1

MultiMesh physics interpolation favors quality over speed.

enum LightProjectorFilter: 🔗

LightProjectorFilter LIGHT_PROJECTOR_FILTER_NEAREST = 0

Nearest-neighbor filter for light projectors (use for pixel art light projectors). No mipmaps are used for rendering, which means light projectors at a distance will look sharp but grainy. This has roughly the same performance cost as using mipmaps.

LightProjectorFilter LIGHT_PROJECTOR_FILTER_LINEAR = 1

Linear filter for light projectors (use for non-pixel art light projectors). No mipmaps are used for rendering, which means light projectors at a distance will look smooth but blurry. This has roughly the same performance cost as using mipmaps.

LightProjectorFilter LIGHT_PROJECTOR_FILTER_NEAREST_MIPMAPS = 2

Nearest-neighbor filter for light projectors (use for pixel art light projectors). Isotropic mipmaps are used for rendering, which means light projectors at a distance will look smooth but blurry. This has roughly the same performance cost as not using mipmaps.

LightProjectorFilter LIGHT_PROJECTOR_FILTER_LINEAR_MIPMAPS = 3

Linear filter for light projectors (use for non-pixel art light projectors). Isotropic mipmaps are used for rendering, which means light projectors at a distance will look smooth but blurry. This has roughly the same performance cost as not using mipmaps.

LightProjectorFilter LIGHT_PROJECTOR_FILTER_NEAREST_MIPMAPS_ANISOTROPIC = 4

Nearest-neighbor filter for light projectors (use for pixel art light projectors). Anisotropic mipmaps are used for rendering, which means light projectors at a distance will look smooth and sharp when viewed from oblique angles. This looks better compared to isotropic mipmaps, but is slower. The level of anisotropic filtering is defined by ProjectSettings.rendering/textures/default_filters/anisotropic_filtering_level.

LightProjectorFilter LIGHT_PROJECTOR_FILTER_LINEAR_MIPMAPS_ANISOTROPIC = 5

Linear filter for light projectors (use for non-pixel art light projectors). Anisotropic mipmaps are used for rendering, which means light projectors at a distance will look smooth and sharp when viewed from oblique angles. This looks better compared to isotropic mipmaps, but is slower. The level of anisotropic filtering is defined by ProjectSettings.rendering/textures/default_filters/anisotropic_filtering_level.

LightType LIGHT_DIRECTIONAL = 0

Directional (sun/moon) light (see DirectionalLight3D).

LightType LIGHT_OMNI = 1

Omni light (see OmniLight3D).

LightType LIGHT_SPOT = 2

Spot light (see SpotLight3D).

LightParam LIGHT_PARAM_ENERGY = 0

The light's energy multiplier.

LightParam LIGHT_PARAM_INDIRECT_ENERGY = 1

The light's indirect energy multiplier (final indirect energy is LIGHT_PARAM_ENERGY * LIGHT_PARAM_INDIRECT_ENERGY).

LightParam LIGHT_PARAM_VOLUMETRIC_FOG_ENERGY = 2

The light's volumetric fog energy multiplier (final volumetric fog energy is LIGHT_PARAM_ENERGY * LIGHT_PARAM_VOLUMETRIC_FOG_ENERGY).

LightParam LIGHT_PARAM_SPECULAR = 3

The light's influence on specularity.

LightParam LIGHT_PARAM_RANGE = 4

LightParam LIGHT_PARAM_SIZE = 5

The size of the light when using spot light or omni light. The angular size of the light when using directional light.

LightParam LIGHT_PARAM_ATTENUATION = 6

The light's attenuation.

LightParam LIGHT_PARAM_SPOT_ANGLE = 7

The spotlight's angle.

LightParam LIGHT_PARAM_SPOT_ATTENUATION = 8

The spotlight's attenuation.

LightParam LIGHT_PARAM_SHADOW_MAX_DISTANCE = 9

The maximum distance for shadow splits. Increasing this value will make directional shadows visible from further away, at the cost of lower overall shadow detail and performance (since more objects need to be included in the directional shadow rendering).

LightParam LIGHT_PARAM_SHADOW_SPLIT_1_OFFSET = 10

Proportion of shadow atlas occupied by the first split.

LightParam LIGHT_PARAM_SHADOW_SPLIT_2_OFFSET = 11

Proportion of shadow atlas occupied by the second split.

LightParam LIGHT_PARAM_SHADOW_SPLIT_3_OFFSET = 12

Proportion of shadow atlas occupied by the third split. The fourth split occupies the rest.

LightParam LIGHT_PARAM_SHADOW_FADE_START = 13

Proportion of shadow max distance where the shadow will start to fade out.

LightParam LIGHT_PARAM_SHADOW_NORMAL_BIAS = 14

Normal bias used to offset shadow lookup by object normal. Can be used to fix self-shadowing artifacts.

LightParam LIGHT_PARAM_SHADOW_BIAS = 15

Bias for the shadow lookup to fix self-shadowing artifacts.

LightParam LIGHT_PARAM_SHADOW_PANCAKE_SIZE = 16

Sets the size of the directional shadow pancake. The pancake offsets the start of the shadow's camera frustum to provide a higher effective depth resolution for the shadow. However, a high pancake size can cause artifacts in the shadows of large objects that are close to the edge of the frustum. Reducing the pancake size can help. Setting the size to 0 turns off the pancaking effect.

LightParam LIGHT_PARAM_SHADOW_OPACITY = 17

The light's shadow opacity. Values lower than 1.0 make the light appear through shadows. This can be used to fake global illumination at a low performance cost.

LightParam LIGHT_PARAM_SHADOW_BLUR = 18

Blurs the edges of the shadow. Can be used to hide pixel artifacts in low resolution shadow maps. A high value can make shadows appear grainy and can cause other unwanted artifacts. Try to keep as near default as possible.

LightParam LIGHT_PARAM_TRANSMITTANCE_BIAS = 19

There is currently no description for this enum. Please help us by contributing one!

LightParam LIGHT_PARAM_INTENSITY = 20

Constant representing the intensity of the light, measured in Lumens when dealing with a SpotLight3D or OmniLight3D, or measured in Lux with a DirectionalLight3D. Only used when ProjectSettings.rendering/lights_and_shadows/use_physical_light_units is true.

LightParam LIGHT_PARAM_MAX = 21

Represents the size of the LightParam enum.

enum LightBakeMode: 🔗

LightBakeMode LIGHT_BAKE_DISABLED = 0

Light is ignored when baking. This is the fastest mode, but the light will be taken into account when baking global illumination. This mode should generally be used for dynamic lights that change quickly, as the effect of global illumination is less noticeable on those lights.

LightBakeMode LIGHT_BAKE_STATIC = 1

Light is taken into account in static baking (VoxelGI, LightmapGI, SDFGI (Environment.sdfgi_enabled)). The light can be moved around or modified, but its global illumination will not update in real-time. This is suitable for subtle changes (such as flickering torches), but generally not large changes such as toggling a light on and off.

LightBakeMode LIGHT_BAKE_DYNAMIC = 2

Light is taken into account in dynamic baking (VoxelGI and SDFGI (Environment.sdfgi_enabled) only). The light can be moved around or modified with global illumination updating in real-time. The light's global illumination appearance will be slightly different compared to LIGHT_BAKE_STATIC. This has a greater performance cost compared to LIGHT_BAKE_STATIC. When using SDFGI, the update speed of dynamic lights is affected by ProjectSettings.rendering/global_illumination/sdfgi/frames_to_update_lights.

enum LightOmniShadowMode: 🔗

LightOmniShadowMode LIGHT_OMNI_SHADOW_DUAL_PARABOLOID = 0

Use a dual paraboloid shadow map for omni lights.

LightOmniShadowMode LIGHT_OMNI_SHADOW_CUBE = 1

Use a cubemap shadow map for omni lights. Slower but better quality than dual paraboloid.

enum LightDirectionalShadowMode: 🔗

LightDirectionalShadowMode LIGHT_DIRECTIONAL_SHADOW_ORTHOGONAL = 0

Use orthogonal shadow projection for directional light.

LightDirectionalShadowMode LIGHT_DIRECTIONAL_SHADOW_PARALLEL_2_SPLITS = 1

Use 2 splits for shadow projection when using directional light.

LightDirectionalShadowMode LIGHT_DIRECTIONAL_SHADOW_PARALLEL_4_SPLITS = 2

Use 4 splits for shadow projection when using directional light.

enum LightDirectionalSkyMode: 🔗

LightDirectionalSkyMode LIGHT_DIRECTIONAL_SKY_MODE_LIGHT_AND_SKY = 0

Use DirectionalLight3D in both sky rendering and scene lighting.

LightDirectionalSkyMode LIGHT_DIRECTIONAL_SKY_MODE_LIGHT_ONLY = 1

Only use DirectionalLight3D in scene lighting.

LightDirectionalSkyMode LIGHT_DIRECTIONAL_SKY_MODE_SKY_ONLY = 2

Only use DirectionalLight3D in sky rendering.

enum ShadowQuality: 🔗

ShadowQuality SHADOW_QUALITY_HARD = 0

Lowest shadow filtering quality (fastest). Soft shadows are not available with this quality setting, which means the Light3D.shadow_blur property is ignored if Light3D.light_size and Light3D.light_angular_distance is 0.0.

Note: The variable shadow blur performed by Light3D.light_size and Light3D.light_angular_distance is still effective when using hard shadow filtering. In this case, Light3D.shadow_blur is taken into account. However, the results will not be blurred, instead the blur amount is treated as a maximum radius for the penumbra.

ShadowQuality SHADOW_QUALITY_SOFT_VERY_LOW = 1

Very low shadow filtering quality (faster). When using this quality setting, Light3D.shadow_blur is automatically multiplied by 0.75× to avoid introducing too much noise. This division only applies to lights whose Light3D.light_size or Light3D.light_angular_distance is 0.0).

ShadowQuality SHADOW_QUALITY_SOFT_LOW = 2

Low shadow filtering quality (fast).

ShadowQuality SHADOW_QUALITY_SOFT_MEDIUM = 3

Medium low shadow filtering quality (average).

ShadowQuality SHADOW_QUALITY_SOFT_HIGH = 4

High low shadow filtering quality (slow). When using this quality setting, Light3D.shadow_blur is automatically multiplied by 1.5× to better make use of the high sample count. This increased blur also improves the stability of dynamic object shadows. This multiplier only applies to lights whose Light3D.light_size or Light3D.light_angular_distance is 0.0).

ShadowQuality SHADOW_QUALITY_SOFT_ULTRA = 5

Highest low shadow filtering quality (slowest). When using this quality setting, Light3D.shadow_blur is automatically multiplied by 2× to better make use of the high sample count. This increased blur also improves the stability of dynamic object shadows. This multiplier only applies to lights whose Light3D.light_size or Light3D.light_angular_distance is 0.0).

ShadowQuality SHADOW_QUALITY_MAX = 6

Represents the size of the ShadowQuality enum.

enum ReflectionProbeUpdateMode: 🔗

ReflectionProbeUpdateMode REFLECTION_PROBE_UPDATE_ONCE = 0

Reflection probe will update reflections once and then stop.

ReflectionProbeUpdateMode REFLECTION_PROBE_UPDATE_ALWAYS = 1

Reflection probe will update each frame. This mode is necessary to capture moving objects.

enum ReflectionProbeAmbientMode: 🔗

ReflectionProbeAmbientMode REFLECTION_PROBE_AMBIENT_DISABLED = 0

Do not apply any ambient lighting inside the reflection probe's box defined by its size.

ReflectionProbeAmbientMode REFLECTION_PROBE_AMBIENT_ENVIRONMENT = 1

Apply automatically-sourced environment lighting inside the reflection probe's box defined by its size.

ReflectionProbeAmbientMode REFLECTION_PROBE_AMBIENT_COLOR = 2

Apply custom ambient lighting inside the reflection probe's box defined by its size. See reflection_probe_set_ambient_color() and reflection_probe_set_ambient_energy().

DecalTexture DECAL_TEXTURE_ALBEDO = 0

Albedo texture slot in a decal (Decal.texture_albedo).

DecalTexture DECAL_TEXTURE_NORMAL = 1

Normal map texture slot in a decal (Decal.texture_normal).

DecalTexture DECAL_TEXTURE_ORM = 2

Occlusion/Roughness/Metallic texture slot in a decal (Decal.texture_orm).

DecalTexture DECAL_TEXTURE_EMISSION = 3

Emission texture slot in a decal (Decal.texture_emission).

DecalTexture DECAL_TEXTURE_MAX = 4

Represents the size of the DecalTexture enum.

DecalFilter DECAL_FILTER_NEAREST = 0

Nearest-neighbor filter for decals (use for pixel art decals). No mipmaps are used for rendering, which means decals at a distance will look sharp but grainy. This has roughly the same performance cost as using mipmaps.

DecalFilter DECAL_FILTER_LINEAR = 1

Linear filter for decals (use for non-pixel art decals). No mipmaps are used for rendering, which means decals at a distance will look smooth but blurry. This has roughly the same performance cost as using mipmaps.

DecalFilter DECAL_FILTER_NEAREST_MIPMAPS = 2

Nearest-neighbor filter for decals (use for pixel art decals). Isotropic mipmaps are used for rendering, which means decals at a distance will look smooth but blurry. This has roughly the same performance cost as not using mipmaps.

DecalFilter DECAL_FILTER_LINEAR_MIPMAPS = 3

Linear filter for decals (use for non-pixel art decals). Isotropic mipmaps are used for rendering, which means decals at a distance will look smooth but blurry. This has roughly the same performance cost as not using mipmaps.

DecalFilter DECAL_FILTER_NEAREST_MIPMAPS_ANISOTROPIC = 4

Nearest-neighbor filter for decals (use for pixel art decals). Anisotropic mipmaps are used for rendering, which means decals at a distance will look smooth and sharp when viewed from oblique angles. This looks better compared to isotropic mipmaps, but is slower. The level of anisotropic filtering is defined by ProjectSettings.rendering/textures/default_filters/anisotropic_filtering_level.

DecalFilter DECAL_FILTER_LINEAR_MIPMAPS_ANISOTROPIC = 5

Linear filter for decals (use for non-pixel art decals). Anisotropic mipmaps are used for rendering, which means decals at a distance will look smooth and sharp when viewed from oblique angles. This looks better compared to isotropic mipmaps, but is slower. The level of anisotropic filtering is defined by ProjectSettings.rendering/textures/default_filters/anisotropic_filtering_level.

enum VoxelGIQuality: 🔗

VoxelGIQuality VOXEL_GI_QUALITY_LOW = 0

Low VoxelGI rendering quality using 4 cones.

VoxelGIQuality VOXEL_GI_QUALITY_HIGH = 1

High VoxelGI rendering quality using 6 cones.

enum ParticlesMode: 🔗

ParticlesMode PARTICLES_MODE_2D = 0

ParticlesMode PARTICLES_MODE_3D = 1

enum ParticlesTransformAlign: 🔗

ParticlesTransformAlign PARTICLES_TRANSFORM_ALIGN_DISABLED = 0

There is currently no description for this enum. Please help us by contributing one!

ParticlesTransformAlign PARTICLES_TRANSFORM_ALIGN_Z_BILLBOARD = 1

There is currently no description for this enum. Please help us by contributing one!

ParticlesTransformAlign PARTICLES_TRANSFORM_ALIGN_Y_TO_VELOCITY = 2

There is currently no description for this enum. Please help us by contributing one!

ParticlesTransformAlign PARTICLES_TRANSFORM_ALIGN_Z_BILLBOARD_Y_TO_VELOCITY = 3

There is currently no description for this enum. Please help us by contributing one!

enum ParticlesDrawOrder: 🔗

ParticlesDrawOrder PARTICLES_DRAW_ORDER_INDEX = 0

Draw particles in the order that they appear in the particles array.

ParticlesDrawOrder PARTICLES_DRAW_ORDER_LIFETIME = 1

Sort particles based on their lifetime. In other words, the particle with the highest lifetime is drawn at the front.

ParticlesDrawOrder PARTICLES_DRAW_ORDER_REVERSE_LIFETIME = 2

Sort particles based on the inverse of their lifetime. In other words, the particle with the lowest lifetime is drawn at the front.

ParticlesDrawOrder PARTICLES_DRAW_ORDER_VIEW_DEPTH = 3

Sort particles based on their distance to the camera.

enum ParticlesCollisionType: 🔗

ParticlesCollisionType PARTICLES_COLLISION_TYPE_SPHERE_ATTRACT = 0

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionType PARTICLES_COLLISION_TYPE_BOX_ATTRACT = 1

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionType PARTICLES_COLLISION_TYPE_VECTOR_FIELD_ATTRACT = 2

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionType PARTICLES_COLLISION_TYPE_SPHERE_COLLIDE = 3

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionType PARTICLES_COLLISION_TYPE_BOX_COLLIDE = 4

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionType PARTICLES_COLLISION_TYPE_SDF_COLLIDE = 5

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionType PARTICLES_COLLISION_TYPE_HEIGHTFIELD_COLLIDE = 6

There is currently no description for this enum. Please help us by contributing one!

enum ParticlesCollisionHeightfieldResolution: 🔗

ParticlesCollisionHeightfieldResolution PARTICLES_COLLISION_HEIGHTFIELD_RESOLUTION_256 = 0

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionHeightfieldResolution PARTICLES_COLLISION_HEIGHTFIELD_RESOLUTION_512 = 1

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionHeightfieldResolution PARTICLES_COLLISION_HEIGHTFIELD_RESOLUTION_1024 = 2

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionHeightfieldResolution PARTICLES_COLLISION_HEIGHTFIELD_RESOLUTION_2048 = 3

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionHeightfieldResolution PARTICLES_COLLISION_HEIGHTFIELD_RESOLUTION_4096 = 4

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionHeightfieldResolution PARTICLES_COLLISION_HEIGHTFIELD_RESOLUTION_8192 = 5

There is currently no description for this enum. Please help us by contributing one!

ParticlesCollisionHeightfieldResolution PARTICLES_COLLISION_HEIGHTFIELD_RESOLUTION_MAX = 6

Represents the size of the ParticlesCollisionHeightfieldResolution enum.

enum FogVolumeShape: 🔗

FogVolumeShape FOG_VOLUME_SHAPE_ELLIPSOID = 0

FogVolume will be shaped like an ellipsoid (stretched sphere).

FogVolumeShape FOG_VOLUME_SHAPE_CONE = 1

FogVolume will be shaped like a cone pointing upwards (in local coordinates). The cone's angle is set automatically to fill the size. The cone will be adjusted to fit within the size. Rotate the FogVolume node to reorient the cone. Non-uniform scaling via size is not supported (scale the FogVolume node instead).

FogVolumeShape FOG_VOLUME_SHAPE_CYLINDER = 2

FogVolume will be shaped like an upright cylinder (in local coordinates). Rotate the FogVolume node to reorient the cylinder. The cylinder will be adjusted to fit within the size. Non-uniform scaling via size is not supported (scale the FogVolume node instead).

FogVolumeShape FOG_VOLUME_SHAPE_BOX = 3

FogVolume will be shaped like a box.

FogVolumeShape FOG_VOLUME_SHAPE_WORLD = 4

FogVolume will have no shape, will cover the whole world and will not be culled.

FogVolumeShape FOG_VOLUME_SHAPE_MAX = 5

Represents the size of the FogVolumeShape enum.

enum ViewportScaling3DMode: 🔗

ViewportScaling3DMode VIEWPORT_SCALING_3D_MODE_BILINEAR = 0

Use bilinear scaling for the viewport's 3D buffer. The amount of scaling can be set using Viewport.scaling_3d_scale. Values less than 1.0 will result in undersampling while values greater than 1.0 will result in supersampling. A value of 1.0 disables scaling.

ViewportScaling3DMode VIEWPORT_SCALING_3D_MODE_FSR = 1

Use AMD FidelityFX Super Resolution 1.0 upscaling for the viewport's 3D buffer. The amount of scaling can be set using Viewport.scaling_3d_scale. Values less than 1.0 will result in the viewport being upscaled using FSR. Values greater than 1.0 are not supported and bilinear downsampling will be used instead. A value of 1.0 disables scaling.

ViewportScaling3DMode VIEWPORT_SCALING_3D_MODE_FSR2 = 2

Use AMD FidelityFX Super Resolution 2.2 upscaling for the viewport's 3D buffer. The amount of scaling can be set using Viewport.scaling_3d_scale. Values less than 1.0 will result in the viewport being upscaled using FSR2. Values greater than 1.0 are not supported and bilinear downsampling will be used instead. A value of 1.0 will use FSR2 at native resolution as a TAA solution.

ViewportScaling3DMode VIEWPORT_SCALING_3D_MODE_METALFX_SPATIAL = 3

Use MetalFX spatial upscaling for the viewport's 3D buffer. The amount of scaling can be set using Viewport.scaling_3d_scale. Values less than 1.0 will result in the viewport being upscaled using MetalFX. Values greater than 1.0 are not supported and bilinear downsampling will be used instead. A value of 1.0 disables scaling.

Note: Only supported when the Metal rendering driver is in use, which limits this scaling mode to macOS and iOS.

ViewportScaling3DMode VIEWPORT_SCALING_3D_MODE_METALFX_TEMPORAL = 4

Use MetalFX temporal upscaling for the viewport's 3D buffer. The amount of scaling can be set using Viewport.scaling_3d_scale. Values less than 1.0 will result in the viewport being upscaled using MetalFX. Values greater than 1.0 are not supported and bilinear downsampling will be used instead. A value of 1.0 will use MetalFX at native resolution as a TAA solution.

Note: Only supported when the Metal rendering driver is in use, which limits this scaling mode to macOS and iOS.

ViewportScaling3DMode VIEWPORT_SCALING_3D_MODE_MAX = 5

Represents the size of the ViewportScaling3DMode enum.

enum ViewportUpdateMode: 🔗

ViewportUpdateMode VIEWPORT_UPDATE_DISABLED = 0

Do not update the viewport's render target.

ViewportUpdateMode VIEWPORT_UPDATE_ONCE = 1

Update the viewport's render target once, then switch to VIEWPORT_UPDATE_DISABLED.

ViewportUpdateMode VIEWPORT_UPDATE_WHEN_VISIBLE = 2

Update the viewport's render target only when it is visible. This is the default value.

ViewportUpdateMode VIEWPORT_UPDATE_WHEN_PARENT_VISIBLE = 3

Update the viewport's render target only when its parent is visible.

ViewportUpdateMode VIEWPORT_UPDATE_ALWAYS = 4

Always update the viewport's render target.

enum ViewportClearMode: 🔗

ViewportClearMode VIEWPORT_CLEAR_ALWAYS = 0

Always clear the viewport's render target before drawing.

ViewportClearMode VIEWPORT_CLEAR_NEVER = 1

Never clear the viewport's render target.

ViewportClearMode VIEWPORT_CLEAR_ONLY_NEXT_FRAME = 2

Clear the viewport's render target on the next frame, then switch to VIEWPORT_CLEAR_NEVER.

enum ViewportEnvironmentMode: 🔗

ViewportEnvironmentMode VIEWPORT_ENVIRONMENT_DISABLED = 0

Disable rendering of 3D environment over 2D canvas.

ViewportEnvironmentMode VIEWPORT_ENVIRONMENT_ENABLED = 1

Enable rendering of 3D environment over 2D canvas.

ViewportEnvironmentMode VIEWPORT_ENVIRONMENT_INHERIT = 2

Inherit enable/disable value from parent. If the topmost parent is also set to VIEWPORT_ENVIRONMENT_INHERIT, then this has the same behavior as VIEWPORT_ENVIRONMENT_ENABLED.

ViewportEnvironmentMode VIEWPORT_ENVIRONMENT_MAX = 3

Represents the size of the ViewportEnvironmentMode enum.

enum ViewportSDFOversize: 🔗

ViewportSDFOversize VIEWPORT_SDF_OVERSIZE_100_PERCENT = 0

Do not oversize the 2D signed distance field. Occluders may disappear when touching the viewport's edges, and GPUParticles3D collision may stop working earlier than intended. This has the lowest GPU requirements.

ViewportSDFOversize VIEWPORT_SDF_OVERSIZE_120_PERCENT = 1

2D signed distance field covers 20% of the viewport's size outside the viewport on each side (top, right, bottom, left).

ViewportSDFOversize VIEWPORT_SDF_OVERSIZE_150_PERCENT = 2

2D signed distance field covers 50% of the viewport's size outside the viewport on each side (top, right, bottom, left).

ViewportSDFOversize VIEWPORT_SDF_OVERSIZE_200_PERCENT = 3

2D signed distance field covers 100% of the viewport's size outside the viewport on each side (top, right, bottom, left). This has the highest GPU requirements.

ViewportSDFOversize VIEWPORT_SDF_OVERSIZE_MAX = 4

Represents the size of the ViewportSDFOversize enum.

enum ViewportSDFScale: 🔗

ViewportSDFScale VIEWPORT_SDF_SCALE_100_PERCENT = 0

Full resolution 2D signed distance field scale. This has the highest GPU requirements.

ViewportSDFScale VIEWPORT_SDF_SCALE_50_PERCENT = 1

Half resolution 2D signed distance field scale on each axis (25% of the viewport pixel count).

ViewportSDFScale VIEWPORT_SDF_SCALE_25_PERCENT = 2

Quarter resolution 2D signed distance field scale on each axis (6.25% of the viewport pixel count). This has the lowest GPU requirements.

ViewportSDFScale VIEWPORT_SDF_SCALE_MAX = 3

Represents the size of the ViewportSDFScale enum.

ViewportMSAA VIEWPORT_MSAA_DISABLED = 0

Multisample antialiasing for 3D is disabled. This is the default value, and also the fastest setting.

ViewportMSAA VIEWPORT_MSAA_2X = 1

Multisample antialiasing uses 2 samples per pixel for 3D. This has a moderate impact on performance.

ViewportMSAA VIEWPORT_MSAA_4X = 2

Multisample antialiasing uses 4 samples per pixel for 3D. This has a high impact on performance.

ViewportMSAA VIEWPORT_MSAA_8X = 3

Multisample antialiasing uses 8 samples per pixel for 3D. This has a very high impact on performance. Likely unsupported on low-end and older hardware.

ViewportMSAA VIEWPORT_MSAA_MAX = 4

Represents the size of the ViewportMSAA enum.

enum ViewportAnisotropicFiltering: 🔗

ViewportAnisotropicFiltering VIEWPORT_ANISOTROPY_DISABLED = 0

Anisotropic filtering is disabled.

ViewportAnisotropicFiltering VIEWPORT_ANISOTROPY_2X = 1

Use 2× anisotropic filtering.

ViewportAnisotropicFiltering VIEWPORT_ANISOTROPY_4X = 2

Use 4× anisotropic filtering. This is the default value.

ViewportAnisotropicFiltering VIEWPORT_ANISOTROPY_8X = 3

Use 8× anisotropic filtering.

ViewportAnisotropicFiltering VIEWPORT_ANISOTROPY_16X = 4

Use 16× anisotropic filtering.

ViewportAnisotropicFiltering VIEWPORT_ANISOTROPY_MAX = 5

Represents the size of the ViewportAnisotropicFiltering enum.

enum ViewportScreenSpaceAA: 🔗

ViewportScreenSpaceAA VIEWPORT_SCREEN_SPACE_AA_DISABLED = 0

Do not perform any antialiasing in the full screen post-process.

ViewportScreenSpaceAA VIEWPORT_SCREEN_SPACE_AA_FXAA = 1

Use fast approximate antialiasing. FXAA is a popular screen-space antialiasing method, which is fast but will make the image look blurry, especially at lower resolutions. It can still work relatively well at large resolutions such as 1440p and 4K.

ViewportScreenSpaceAA VIEWPORT_SCREEN_SPACE_AA_SMAA = 2

Use subpixel morphological antialiasing. SMAA may produce clearer results than FXAA, but at a slightly higher performance cost.

ViewportScreenSpaceAA VIEWPORT_SCREEN_SPACE_AA_MAX = 3

Represents the size of the ViewportScreenSpaceAA enum.

enum ViewportOcclusionCullingBuildQuality: 🔗

ViewportOcclusionCullingBuildQuality VIEWPORT_OCCLUSION_BUILD_QUALITY_LOW = 0

Low occlusion culling BVH build quality (as defined by Embree). Results in the lowest CPU usage, but least effective culling.

ViewportOcclusionCullingBuildQuality VIEWPORT_OCCLUSION_BUILD_QUALITY_MEDIUM = 1

Medium occlusion culling BVH build quality (as defined by Embree).

ViewportOcclusionCullingBuildQuality VIEWPORT_OCCLUSION_BUILD_QUALITY_HIGH = 2

High occlusion culling BVH build quality (as defined by Embree). Results in the highest CPU usage, but most effective culling.

enum ViewportRenderInfo: 🔗

ViewportRenderInfo VIEWPORT_RENDER_INFO_OBJECTS_IN_FRAME = 0

Number of objects drawn in a single frame.

ViewportRenderInfo VIEWPORT_RENDER_INFO_PRIMITIVES_IN_FRAME = 1

Number of points, lines, or triangles drawn in a single frame.

ViewportRenderInfo VIEWPORT_RENDER_INFO_DRAW_CALLS_IN_FRAME = 2

Number of draw calls during this frame.

ViewportRenderInfo VIEWPORT_RENDER_INFO_MAX = 3

Represents the size of the ViewportRenderInfo enum.

enum ViewportRenderInfoType: 🔗

ViewportRenderInfoType VIEWPORT_RENDER_INFO_TYPE_VISIBLE = 0

Visible render pass (excluding shadows).

ViewportRenderInfoType VIEWPORT_RENDER_INFO_TYPE_SHADOW = 1

Shadow render pass. Objects will be rendered several times depending on the number of amounts of lights with shadows and the number of directional shadow splits.

ViewportRenderInfoType VIEWPORT_RENDER_INFO_TYPE_CANVAS = 2

Canvas item rendering. This includes all 2D rendering.

ViewportRenderInfoType VIEWPORT_RENDER_INFO_TYPE_MAX = 3

Represents the size of the ViewportRenderInfoType enum.

enum ViewportDebugDraw: 🔗

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_DISABLED = 0

Debug draw is disabled. Default setting.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_UNSHADED = 1

Objects are displayed without light information.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_LIGHTING = 2

Objects are displayed with only light information.

Note: When using this debug draw mode, custom shaders are ignored since all materials in the scene temporarily use a debug material. This means the result from custom shader functions (such as vertex displacement) won't be visible anymore when using this debug draw mode.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_OVERDRAW = 3

Objects are displayed semi-transparent with additive blending so you can see where they are drawing over top of one another. A higher overdraw (represented by brighter colors) means you are wasting performance on drawing pixels that are being hidden behind others.

Note: When using this debug draw mode, custom shaders are ignored since all materials in the scene temporarily use a debug material. This means the result from custom shader functions (such as vertex displacement) won't be visible anymore when using this debug draw mode.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_WIREFRAME = 4

Debug draw draws objects in wireframe.

Note: set_debug_generate_wireframes() must be called before loading any meshes for wireframes to be visible when using the Compatibility renderer.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_NORMAL_BUFFER = 5

Normal buffer is drawn instead of regular scene so you can see the per-pixel normals that will be used by post-processing effects.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_VOXEL_GI_ALBEDO = 6

Objects are displayed with only the albedo value from VoxelGIs. Requires at least one visible VoxelGI node that has been baked to have a visible effect.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_VOXEL_GI_LIGHTING = 7

Objects are displayed with only the lighting value from VoxelGIs. Requires at least one visible VoxelGI node that has been baked to have a visible effect.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_VOXEL_GI_EMISSION = 8

Objects are displayed with only the emission color from VoxelGIs. Requires at least one visible VoxelGI node that has been baked to have a visible effect.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_SHADOW_ATLAS = 9

Draws the shadow atlas that stores shadows from OmniLight3Ds and SpotLight3Ds in the upper left quadrant of the Viewport.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_DIRECTIONAL_SHADOW_ATLAS = 10

Draws the shadow atlas that stores shadows from DirectionalLight3Ds in the upper left quadrant of the Viewport.

The slice of the camera frustum related to the shadow map cascade is superimposed to visualize coverage. The color of each slice matches the colors used for VIEWPORT_DEBUG_DRAW_PSSM_SPLITS. When shadow cascades are blended the overlap is taken into account when drawing the frustum slices.

The last cascade shows all frustum slices to illustrate the coverage of all slices.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_SCENE_LUMINANCE = 11

Draws the estimated scene luminance. This is a 1×1 texture that is generated when autoexposure is enabled to control the scene's exposure.

Note: Only supported when using the Forward+ or Mobile rendering methods.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_SSAO = 12

Draws the screen space ambient occlusion texture instead of the scene so that you can clearly see how it is affecting objects. In order for this display mode to work, you must have Environment.ssao_enabled set in your WorldEnvironment.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_SSIL = 13

Draws the screen space indirect lighting texture instead of the scene so that you can clearly see how it is affecting objects. In order for this display mode to work, you must have Environment.ssil_enabled set in your WorldEnvironment.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_PSSM_SPLITS = 14

Colors each PSSM split for the DirectionalLight3Ds in the scene a different color so you can see where the splits are. In order (from closest to furthest from the camera), they are colored red, green, blue, and yellow.

Note: When using this debug draw mode, custom shaders are ignored since all materials in the scene temporarily use a debug material. This means the result from custom shader functions (such as vertex displacement) won't be visible anymore when using this debug draw mode.

Note: Only supported when using the Forward+ or Mobile rendering methods.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_DECAL_ATLAS = 15

Draws the decal atlas that stores decal textures from Decals.

Note: Only supported when using the Forward+ or Mobile rendering methods.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_SDFGI = 16

Draws SDFGI cascade data. This is the data structure that is used to bounce lighting against and create reflections.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_SDFGI_PROBES = 17

Draws SDFGI probe data. This is the data structure that is used to give indirect lighting dynamic objects moving within the scene.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_GI_BUFFER = 18

Draws the global illumination buffer from VoxelGI or SDFGI. Requires VoxelGI (at least one visible baked VoxelGI node) or SDFGI (Environment.sdfgi_enabled) to be enabled to have a visible effect.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_DISABLE_LOD = 19

Disable mesh LOD. All meshes are drawn with full detail, which can be used to compare performance.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_CLUSTER_OMNI_LIGHTS = 20

Draws the OmniLight3D cluster. Clustering determines where lights are positioned in screen-space, which allows the engine to only process these portions of the screen for lighting.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_CLUSTER_SPOT_LIGHTS = 21

Draws the SpotLight3D cluster. Clustering determines where lights are positioned in screen-space, which allows the engine to only process these portions of the screen for lighting.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_CLUSTER_DECALS = 22

Draws the Decal cluster. Clustering determines where decals are positioned in screen-space, which allows the engine to only process these portions of the screen for decals.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_CLUSTER_REFLECTION_PROBES = 23

Draws the ReflectionProbe cluster. Clustering determines where reflection probes are positioned in screen-space, which allows the engine to only process these portions of the screen for reflection probes.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_OCCLUDERS = 24

Draws the occlusion culling buffer. This low-resolution occlusion culling buffer is rasterized on the CPU and is used to check whether instances are occluded by other objects.

Note: Only supported when using the Forward+ or Mobile rendering methods.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_MOTION_VECTORS = 25

Draws the motion vectors buffer. This is used by temporal antialiasing to correct for motion that occurs during gameplay.

Note: Only supported when using the Forward+ rendering method.

ViewportDebugDraw VIEWPORT_DEBUG_DRAW_INTERNAL_BUFFER = 26

Internal buffer is drawn instead of regular scene so you can see the per-pixel output that will be used by post-processing effects.

Note: Only supported when using the Forward+ or Mobile rendering methods.

enum ViewportVRSMode: 🔗

ViewportVRSMode VIEWPORT_VRS_DISABLED = 0

Variable rate shading is disabled.

ViewportVRSMode VIEWPORT_VRS_TEXTURE = 1

Variable rate shading uses a texture. Note, for stereoscopic use a texture atlas with a texture for each view.

ViewportVRSMode VIEWPORT_VRS_XR = 2

Variable rate shading texture is supplied by the primary XRInterface. Note that this may override the update mode.

ViewportVRSMode VIEWPORT_VRS_MAX = 3

Represents the size of the ViewportVRSMode enum.

enum ViewportVRSUpdateMode: 🔗

ViewportVRSUpdateMode VIEWPORT_VRS_UPDATE_DISABLED = 0

The input texture for variable rate shading will not be processed.

ViewportVRSUpdateMode VIEWPORT_VRS_UPDATE_ONCE = 1

The input texture for variable rate shading will be processed once.

ViewportVRSUpdateMode VIEWPORT_VRS_UPDATE_ALWAYS = 2

The input texture for variable rate shading will be processed each frame.

ViewportVRSUpdateMode VIEWPORT_VRS_UPDATE_MAX = 3

Represents the size of the ViewportVRSUpdateMode enum.

SkyMode SKY_MODE_AUTOMATIC = 0

Automatically selects the appropriate process mode based on your sky shader. If your shader uses TIME or POSITION, this will use SKY_MODE_REALTIME. If your shader uses any of the LIGHT_* variables or any custom uniforms, this uses SKY_MODE_INCREMENTAL. Otherwise, this defaults to SKY_MODE_QUALITY.

SkyMode SKY_MODE_QUALITY = 1

Uses high quality importance sampling to process the radiance map. In general, this results in much higher quality than SKY_MODE_REALTIME but takes much longer to generate. This should not be used if you plan on changing the sky at runtime. If you are finding that the reflection is not blurry enough and is showing sparkles or fireflies, try increasing ProjectSettings.rendering/reflections/sky_reflections/ggx_samples.

SkyMode SKY_MODE_INCREMENTAL = 2

Uses the same high quality importance sampling to process the radiance map as SKY_MODE_QUALITY, but updates over several frames. The number of frames is determined by ProjectSettings.rendering/reflections/sky_reflections/roughness_layers. Use this when you need highest quality radiance maps, but have a sky that updates slowly.

SkyMode SKY_MODE_REALTIME = 3

Uses the fast filtering algorithm to process the radiance map. In general this results in lower quality, but substantially faster run times. If you need better quality, but still need to update the sky every frame, consider turning on ProjectSettings.rendering/reflections/sky_reflections/fast_filter_high_quality.

Note: The fast filtering algorithm is limited to 256×256 cubemaps, so sky_set_radiance_size() must be set to 256. Otherwise, a warning is printed and the overridden radiance size is ignored.

enum CompositorEffectFlags: 🔗

CompositorEffectFlags COMPOSITOR_EFFECT_FLAG_ACCESS_RESOLVED_COLOR = 1

The rendering effect requires the color buffer to be resolved if MSAA is enabled.

CompositorEffectFlags COMPOSITOR_EFFECT_FLAG_ACCESS_RESOLVED_DEPTH = 2

The rendering effect requires the depth buffer to be resolved if MSAA is enabled.

CompositorEffectFlags COMPOSITOR_EFFECT_FLAG_NEEDS_MOTION_VECTORS = 4

The rendering effect requires motion vectors to be produced.

CompositorEffectFlags COMPOSITOR_EFFECT_FLAG_NEEDS_ROUGHNESS = 8

The rendering effect requires normals and roughness g-buffer to be produced (Forward+ only).

CompositorEffectFlags COMPOSITOR_EFFECT_FLAG_NEEDS_SEPARATE_SPECULAR = 16

The rendering effect requires specular data to be separated out (Forward+ only).

enum CompositorEffectCallbackType: 🔗

CompositorEffectCallbackType COMPOSITOR_EFFECT_CALLBACK_TYPE_PRE_OPAQUE = 0

The callback is called before our opaque rendering pass, but after depth prepass (if applicable).

CompositorEffectCallbackType COMPOSITOR_EFFECT_CALLBACK_TYPE_POST_OPAQUE = 1

The callback is called after our opaque rendering pass, but before our sky is rendered.

CompositorEffectCallbackType COMPOSITOR_EFFECT_CALLBACK_TYPE_POST_SKY = 2

The callback is called after our sky is rendered, but before our back buffers are created (and if enabled, before subsurface scattering and/or screen space reflections).

CompositorEffectCallbackType COMPOSITOR_EFFECT_CALLBACK_TYPE_PRE_TRANSPARENT = 3

The callback is called before our transparent rendering pass, but after our sky is rendered and we've created our back buffers.

CompositorEffectCallbackType COMPOSITOR_EFFECT_CALLBACK_TYPE_POST_TRANSPARENT = 4

The callback is called after our transparent rendering pass, but before any built-in post-processing effects and output to our render target.

CompositorEffectCallbackType COMPOSITOR_EFFECT_CALLBACK_TYPE_ANY = -1

There is currently no description for this enum. Please help us by contributing one!

enum EnvironmentBG: 🔗

EnvironmentBG ENV_BG_CLEAR_COLOR = 0

Use the clear color as background.

EnvironmentBG ENV_BG_COLOR = 1

Use a specified color as the background.

EnvironmentBG ENV_BG_SKY = 2

Use a sky resource for the background.

EnvironmentBG ENV_BG_CANVAS = 3

Use a specified canvas layer as the background. This can be useful for instantiating a 2D scene in a 3D world.

EnvironmentBG ENV_BG_KEEP = 4

Do not clear the background, use whatever was rendered last frame as the background.

EnvironmentBG ENV_BG_CAMERA_FEED = 5

Displays a camera feed in the background.

EnvironmentBG ENV_BG_MAX = 6

Represents the size of the EnvironmentBG enum.

enum EnvironmentAmbientSource: 🔗

EnvironmentAmbientSource ENV_AMBIENT_SOURCE_BG = 0

Gather ambient light from whichever source is specified as the background.

EnvironmentAmbientSource ENV_AMBIENT_SOURCE_DISABLED = 1

Disable ambient light.

EnvironmentAmbientSource ENV_AMBIENT_SOURCE_COLOR = 2

Specify a specific Color for ambient light.

EnvironmentAmbientSource ENV_AMBIENT_SOURCE_SKY = 3

Gather ambient light from the Sky regardless of what the background is.

enum EnvironmentReflectionSource: 🔗

EnvironmentReflectionSource ENV_REFLECTION_SOURCE_BG = 0

Use the background for reflections.

EnvironmentReflectionSource ENV_REFLECTION_SOURCE_DISABLED = 1

EnvironmentReflectionSource ENV_REFLECTION_SOURCE_SKY = 2

Use the Sky for reflections regardless of what the background is.

enum EnvironmentGlowBlendMode: 🔗

EnvironmentGlowBlendMode ENV_GLOW_BLEND_MODE_ADDITIVE = 0

Additive glow blending mode. Mostly used for particles, glows (bloom), lens flare, bright sources.

EnvironmentGlowBlendMode ENV_GLOW_BLEND_MODE_SCREEN = 1

Screen glow blending mode. Increases brightness, used frequently with bloom.

EnvironmentGlowBlendMode ENV_GLOW_BLEND_MODE_SOFTLIGHT = 2

Soft light glow blending mode. Modifies contrast, exposes shadows and highlights (vivid bloom).

EnvironmentGlowBlendMode ENV_GLOW_BLEND_MODE_REPLACE = 3

Replace glow blending mode. Replaces all pixels' color by the glow value. This can be used to simulate a full-screen blur effect by tweaking the glow parameters to match the original image's brightness.

EnvironmentGlowBlendMode ENV_GLOW_BLEND_MODE_MIX = 4

Mixes the glow with the underlying color to avoid increasing brightness as much while still maintaining a glow effect.

enum EnvironmentFogMode: 🔗

EnvironmentFogMode ENV_FOG_MODE_EXPONENTIAL = 0

Use a physically-based fog model defined primarily by fog density.

EnvironmentFogMode ENV_FOG_MODE_DEPTH = 1

Use a simple fog model defined by start and end positions and a custom curve. While not physically accurate, this model can be useful when you need more artistic control.

enum EnvironmentToneMapper: 🔗

EnvironmentToneMapper ENV_TONE_MAPPER_LINEAR = 0

Does not modify color data, resulting in a linear tonemapping curve which unnaturally clips bright values, causing bright lighting to look blown out. The simplest and fastest tonemapper.

EnvironmentToneMapper ENV_TONE_MAPPER_REINHARD = 1

A simple tonemapping curve that rolls off bright values to prevent clipping. This results in an image that can appear dull and low contrast. Slower than ENV_TONE_MAPPER_LINEAR.

Note: When Environment.tonemap_white is left at the default value of 1.0, ENV_TONE_MAPPER_REINHARD produces an identical image to ENV_TONE_MAPPER_LINEAR.

EnvironmentToneMapper ENV_TONE_MAPPER_FILMIC = 2

Uses a film-like tonemapping curve to prevent clipping of bright values and provide better contrast than ENV_TONE_MAPPER_REINHARD. Slightly slower than ENV_TONE_MAPPER_REINHARD.

EnvironmentToneMapper ENV_TONE_MAPPER_ACES = 3

Uses a high-contrast film-like tonemapping curve and desaturates bright values for a more realistic appearance. Slightly slower than ENV_TONE_MAPPER_FILMIC.

Note: This tonemapping operator is called "ACES Fitted" in Godot 3.x.

EnvironmentToneMapper ENV_TONE_MAPPER_AGX = 4

Uses a film-like tonemapping curve and desaturates bright values for a more realistic appearance. Better than other tonemappers at maintaining the hue of colors as they become brighter. The slowest tonemapping option.

Note: Environment.tonemap_white is fixed at a value of 16.29, which makes ENV_TONE_MAPPER_AGX unsuitable for use with the Mobile rendering method.

enum EnvironmentSSRRoughnessQuality: 🔗

EnvironmentSSRRoughnessQuality ENV_SSR_ROUGHNESS_QUALITY_DISABLED = 0

Lowest quality of roughness filter for screen-space reflections. Rough materials will not have blurrier screen-space reflections compared to smooth (non-rough) materials. This is the fastest option.

EnvironmentSSRRoughnessQuality ENV_SSR_ROUGHNESS_QUALITY_LOW = 1

Low quality of roughness filter for screen-space reflections.

EnvironmentSSRRoughnessQuality ENV_SSR_ROUGHNESS_QUALITY_MEDIUM = 2

Medium quality of roughness filter for screen-space reflections.

EnvironmentSSRRoughnessQuality ENV_SSR_ROUGHNESS_QUALITY_HIGH = 3

High quality of roughness filter for screen-space reflections. This is the slowest option.

enum EnvironmentSSAOQuality: 🔗

EnvironmentSSAOQuality ENV_SSAO_QUALITY_VERY_LOW = 0

Lowest quality of screen-space ambient occlusion.

EnvironmentSSAOQuality ENV_SSAO_QUALITY_LOW = 1

Low quality screen-space ambient occlusion.

EnvironmentSSAOQuality ENV_SSAO_QUALITY_MEDIUM = 2

Medium quality screen-space ambient occlusion.

EnvironmentSSAOQuality ENV_SSAO_QUALITY_HIGH = 3

High quality screen-space ambient occlusion.

EnvironmentSSAOQuality ENV_SSAO_QUALITY_ULTRA = 4

Highest quality screen-space ambient occlusion. Uses the adaptive target setting which can be dynamically adjusted to smoothly balance performance and visual quality.

enum EnvironmentSSILQuality: 🔗

EnvironmentSSILQuality ENV_SSIL_QUALITY_VERY_LOW = 0

Lowest quality of screen-space indirect lighting.

EnvironmentSSILQuality ENV_SSIL_QUALITY_LOW = 1

Low quality screen-space indirect lighting.

EnvironmentSSILQuality ENV_SSIL_QUALITY_MEDIUM = 2

High quality screen-space indirect lighting.

EnvironmentSSILQuality ENV_SSIL_QUALITY_HIGH = 3

High quality screen-space indirect lighting.

EnvironmentSSILQuality ENV_SSIL_QUALITY_ULTRA = 4

Highest quality screen-space indirect lighting. Uses the adaptive target setting which can be dynamically adjusted to smoothly balance performance and visual quality.

enum EnvironmentSDFGIYScale: 🔗

EnvironmentSDFGIYScale ENV_SDFGI_Y_SCALE_50_PERCENT = 0

Use 50% scale for SDFGI on the Y (vertical) axis. SDFGI cells will be twice as short as they are wide. This allows providing increased GI detail and reduced light leaking with thin floors and ceilings. This is usually the best choice for scenes that don't feature much verticality.

EnvironmentSDFGIYScale ENV_SDFGI_Y_SCALE_75_PERCENT = 1

Use 75% scale for SDFGI on the Y (vertical) axis. This is a balance between the 50% and 100% SDFGI Y scales.

EnvironmentSDFGIYScale ENV_SDFGI_Y_SCALE_100_PERCENT = 2

Use 100% scale for SDFGI on the Y (vertical) axis. SDFGI cells will be as tall as they are wide. This is usually the best choice for highly vertical scenes. The downside is that light leaking may become more noticeable with thin floors and ceilings.

enum EnvironmentSDFGIRayCount: 🔗

EnvironmentSDFGIRayCount ENV_SDFGI_RAY_COUNT_4 = 0

Throw 4 rays per frame when converging SDFGI. This has the lowest GPU requirements, but creates the most noisy result.

EnvironmentSDFGIRayCount ENV_SDFGI_RAY_COUNT_8 = 1

Throw 8 rays per frame when converging SDFGI.

EnvironmentSDFGIRayCount ENV_SDFGI_RAY_COUNT_16 = 2

Throw 16 rays per frame when converging SDFGI.

EnvironmentSDFGIRayCount ENV_SDFGI_RAY_COUNT_32 = 3

Throw 32 rays per frame when converging SDFGI.

EnvironmentSDFGIRayCount ENV_SDFGI_RAY_COUNT_64 = 4

Throw 64 rays per frame when converging SDFGI.

EnvironmentSDFGIRayCount ENV_SDFGI_RAY_COUNT_96 = 5

Throw 96 rays per frame when converging SDFGI. This has high GPU requirements.

EnvironmentSDFGIRayCount ENV_SDFGI_RAY_COUNT_128 = 6

Throw 128 rays per frame when converging SDFGI. This has very high GPU requirements, but creates the least noisy result.

EnvironmentSDFGIRayCount ENV_SDFGI_RAY_COUNT_MAX = 7

Represents the size of the EnvironmentSDFGIRayCount enum.

enum EnvironmentSDFGIFramesToConverge: 🔗

EnvironmentSDFGIFramesToConverge ENV_SDFGI_CONVERGE_IN_5_FRAMES = 0

Converge SDFGI over 5 frames. This is the most responsive, but creates the most noisy result with a given ray count.

EnvironmentSDFGIFramesToConverge ENV_SDFGI_CONVERGE_IN_10_FRAMES = 1

Configure SDFGI to fully converge over 10 frames.

EnvironmentSDFGIFramesToConverge ENV_SDFGI_CONVERGE_IN_15_FRAMES = 2

Configure SDFGI to fully converge over 15 frames.

EnvironmentSDFGIFramesToConverge ENV_SDFGI_CONVERGE_IN_20_FRAMES = 3

Configure SDFGI to fully converge over 20 frames.

EnvironmentSDFGIFramesToConverge ENV_SDFGI_CONVERGE_IN_25_FRAMES = 4

Configure SDFGI to fully converge over 25 frames.

EnvironmentSDFGIFramesToConverge ENV_SDFGI_CONVERGE_IN_30_FRAMES = 5

Configure SDFGI to fully converge over 30 frames. This is the least responsive, but creates the least noisy result with a given ray count.

EnvironmentSDFGIFramesToConverge ENV_SDFGI_CONVERGE_MAX = 6

Represents the size of the EnvironmentSDFGIFramesToConverge enum.

enum EnvironmentSDFGIFramesToUpdateLight: 🔗

EnvironmentSDFGIFramesToUpdateLight ENV_SDFGI_UPDATE_LIGHT_IN_1_FRAME = 0

Update indirect light from dynamic lights in SDFGI over 1 frame. This is the most responsive, but has the highest GPU requirements.

EnvironmentSDFGIFramesToUpdateLight ENV_SDFGI_UPDATE_LIGHT_IN_2_FRAMES = 1

Update indirect light from dynamic lights in SDFGI over 2 frames.

EnvironmentSDFGIFramesToUpdateLight ENV_SDFGI_UPDATE_LIGHT_IN_4_FRAMES = 2

Update indirect light from dynamic lights in SDFGI over 4 frames.

EnvironmentSDFGIFramesToUpdateLight ENV_SDFGI_UPDATE_LIGHT_IN_8_FRAMES = 3

Update indirect light from dynamic lights in SDFGI over 8 frames.

EnvironmentSDFGIFramesToUpdateLight ENV_SDFGI_UPDATE_LIGHT_IN_16_FRAMES = 4

Update indirect light from dynamic lights in SDFGI over 16 frames. This is the least responsive, but has the lowest GPU requirements.

EnvironmentSDFGIFramesToUpdateLight ENV_SDFGI_UPDATE_LIGHT_MAX = 5

Represents the size of the EnvironmentSDFGIFramesToUpdateLight enum.

enum SubSurfaceScatteringQuality: 🔗

SubSurfaceScatteringQuality SUB_SURFACE_SCATTERING_QUALITY_DISABLED = 0

Disables subsurface scattering entirely, even on materials that have BaseMaterial3D.subsurf_scatter_enabled set to true. This has the lowest GPU requirements.

SubSurfaceScatteringQuality SUB_SURFACE_SCATTERING_QUALITY_LOW = 1

Low subsurface scattering quality.

SubSurfaceScatteringQuality SUB_SURFACE_SCATTERING_QUALITY_MEDIUM = 2

Medium subsurface scattering quality.

SubSurfaceScatteringQuality SUB_SURFACE_SCATTERING_QUALITY_HIGH = 3

High subsurface scattering quality. This has the highest GPU requirements.

enum DOFBokehShape: 🔗

DOFBokehShape DOF_BOKEH_BOX = 0

Calculate the DOF blur using a box filter. The fastest option, but results in obvious lines in blur pattern.

DOFBokehShape DOF_BOKEH_HEXAGON = 1

Calculates DOF blur using a hexagon shaped filter.

DOFBokehShape DOF_BOKEH_CIRCLE = 2

Calculates DOF blur using a circle shaped filter. Best quality and most realistic, but slowest. Use only for areas where a lot of performance can be dedicated to post-processing (e.g. cutscenes).

enum DOFBlurQuality: 🔗

DOFBlurQuality DOF_BLUR_QUALITY_VERY_LOW = 0

Lowest quality DOF blur. This is the fastest setting, but you may be able to see filtering artifacts.

DOFBlurQuality DOF_BLUR_QUALITY_LOW = 1

Low quality DOF blur.

DOFBlurQuality DOF_BLUR_QUALITY_MEDIUM = 2

Medium quality DOF blur.

DOFBlurQuality DOF_BLUR_QUALITY_HIGH = 3

Highest quality DOF blur. Results in the smoothest looking blur by taking the most samples, but is also significantly slower.

InstanceType INSTANCE_NONE = 0

The instance does not have a type.

InstanceType INSTANCE_MESH = 1

The instance is a mesh.

InstanceType INSTANCE_MULTIMESH = 2

The instance is a multimesh.

InstanceType INSTANCE_PARTICLES = 3

The instance is a particle emitter.

InstanceType INSTANCE_PARTICLES_COLLISION = 4

The instance is a GPUParticles collision shape.

InstanceType INSTANCE_LIGHT = 5

The instance is a light.

InstanceType INSTANCE_REFLECTION_PROBE = 6

The instance is a reflection probe.

InstanceType INSTANCE_DECAL = 7

The instance is a decal.

InstanceType INSTANCE_VOXEL_GI = 8

The instance is a VoxelGI.

InstanceType INSTANCE_LIGHTMAP = 9

The instance is a lightmap.

InstanceType INSTANCE_OCCLUDER = 10

The instance is an occlusion culling occluder.

InstanceType INSTANCE_VISIBLITY_NOTIFIER = 11

The instance is a visible on-screen notifier.

InstanceType INSTANCE_FOG_VOLUME = 12

The instance is a fog volume.

InstanceType INSTANCE_MAX = 13

Represents the size of the InstanceType enum.

InstanceType INSTANCE_GEOMETRY_MASK = 14

A combination of the flags of geometry instances (mesh, multimesh, immediate and particles).

enum InstanceFlags: 🔗

InstanceFlags INSTANCE_FLAG_USE_BAKED_LIGHT = 0

Allows the instance to be used in baked lighting.

InstanceFlags INSTANCE_FLAG_USE_DYNAMIC_GI = 1

Allows the instance to be used with dynamic global illumination.

InstanceFlags INSTANCE_FLAG_DRAW_NEXT_FRAME_IF_VISIBLE = 2

When set, manually requests to draw geometry on next frame.

InstanceFlags INSTANCE_FLAG_IGNORE_OCCLUSION_CULLING = 3

Always draw, even if the instance would be culled by occlusion culling. Does not affect view frustum culling.

InstanceFlags INSTANCE_FLAG_MAX = 4

Represents the size of the InstanceFlags enum.

enum ShadowCastingSetting: 🔗

ShadowCastingSetting SHADOW_CASTING_SETTING_OFF = 0

Disable shadows from this instance.

ShadowCastingSetting SHADOW_CASTING_SETTING_ON = 1

Cast shadows from this instance.

ShadowCastingSetting SHADOW_CASTING_SETTING_DOUBLE_SIDED = 2

Disable backface culling when rendering the shadow of the object. This is slightly slower but may result in more correct shadows.

ShadowCastingSetting SHADOW_CASTING_SETTING_SHADOWS_ONLY = 3

Only render the shadows from the object. The object itself will not be drawn.

enum VisibilityRangeFadeMode: 🔗

VisibilityRangeFadeMode VISIBILITY_RANGE_FADE_DISABLED = 0

Disable visibility range fading for the given instance.

VisibilityRangeFadeMode VISIBILITY_RANGE_FADE_SELF = 1

Fade-out the given instance when it approaches its visibility range limits.

VisibilityRangeFadeMode VISIBILITY_RANGE_FADE_DEPENDENCIES = 2

Fade-in the given instance's dependencies when reaching its visibility range limits.

BakeChannels BAKE_CHANNEL_ALBEDO_ALPHA = 0

Index of Image in array of Images returned by bake_render_uv2(). Image uses Image.FORMAT_RGBA8 and contains albedo color in the .rgb channels and alpha in the .a channel.

BakeChannels BAKE_CHANNEL_NORMAL = 1

Index of Image in array of Images returned by bake_render_uv2(). Image uses Image.FORMAT_RGBA8 and contains the per-pixel normal of the object in the .rgb channels and nothing in the .a channel. The per-pixel normal is encoded as normal * 0.5 + 0.5.

BakeChannels BAKE_CHANNEL_ORM = 2

Index of Image in array of Images returned by bake_render_uv2(). Image uses Image.FORMAT_RGBA8 and contains ambient occlusion (from material and decals only) in the .r channel, roughness in the .g channel, metallic in the .b channel and sub surface scattering amount in the .a channel.

BakeChannels BAKE_CHANNEL_EMISSION = 3

Index of Image in array of Images returned by bake_render_uv2(). Image uses Image.FORMAT_RGBAH and contains emission color in the .rgb channels and nothing in the .a channel.

enum CanvasTextureChannel: 🔗

CanvasTextureChannel CANVAS_TEXTURE_CHANNEL_DIFFUSE = 0

Diffuse canvas texture (CanvasTexture.diffuse_texture).

CanvasTextureChannel CANVAS_TEXTURE_CHANNEL_NORMAL = 1

Normal map canvas texture (CanvasTexture.normal_texture).

CanvasTextureChannel CANVAS_TEXTURE_CHANNEL_SPECULAR = 2

Specular map canvas texture (CanvasTexture.specular_texture).

enum NinePatchAxisMode: 🔗

NinePatchAxisMode NINE_PATCH_STRETCH = 0

The nine patch gets stretched where needed.

NinePatchAxisMode NINE_PATCH_TILE = 1

The nine patch gets filled with tiles where needed.

NinePatchAxisMode NINE_PATCH_TILE_FIT = 2

The nine patch gets filled with tiles where needed and stretches them a bit if needed.

enum CanvasItemTextureFilter: 🔗

CanvasItemTextureFilter CANVAS_ITEM_TEXTURE_FILTER_DEFAULT = 0

Uses the default filter mode for this Viewport.

CanvasItemTextureFilter CANVAS_ITEM_TEXTURE_FILTER_NEAREST = 1

The texture filter reads from the nearest pixel only. This makes the texture look pixelated from up close, and grainy from a distance (due to mipmaps not being sampled).

CanvasItemTextureFilter CANVAS_ITEM_TEXTURE_FILTER_LINEAR = 2

The texture filter blends between the nearest 4 pixels. This makes the texture look smooth from up close, and grainy from a distance (due to mipmaps not being sampled).

CanvasItemTextureFilter CANVAS_ITEM_TEXTURE_FILTER_NEAREST_WITH_MIPMAPS = 3

The texture filter reads from the nearest pixel and blends between the nearest 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true). This makes the texture look pixelated from up close, and smooth from a distance.

Use this for non-pixel art textures that may be viewed at a low scale (e.g. due to Camera2D zoom or sprite scaling), as mipmaps are important to smooth out pixels that are smaller than on-screen pixels.

CanvasItemTextureFilter CANVAS_ITEM_TEXTURE_FILTER_LINEAR_WITH_MIPMAPS = 4

The texture filter blends between the nearest 4 pixels and between the nearest 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true). This makes the texture look smooth from up close, and smooth from a distance.

Use this for non-pixel art textures that may be viewed at a low scale (e.g. due to Camera2D zoom or sprite scaling), as mipmaps are important to smooth out pixels that are smaller than on-screen pixels.

CanvasItemTextureFilter CANVAS_ITEM_TEXTURE_FILTER_NEAREST_WITH_MIPMAPS_ANISOTROPIC = 5

The texture filter reads from the nearest pixel and blends between 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true) based on the angle between the surface and the camera view. This makes the texture look pixelated from up close, and smooth from a distance. Anisotropic filtering improves texture quality on surfaces that are almost in line with the camera, but is slightly slower. The anisotropic filtering level can be changed by adjusting ProjectSettings.rendering/textures/default_filters/anisotropic_filtering_level.

Note: This texture filter is rarely useful in 2D projects. CANVAS_ITEM_TEXTURE_FILTER_NEAREST_WITH_MIPMAPS is usually more appropriate in this case.

CanvasItemTextureFilter CANVAS_ITEM_TEXTURE_FILTER_LINEAR_WITH_MIPMAPS_ANISOTROPIC = 6

The texture filter blends between the nearest 4 pixels and blends between 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true) based on the angle between the surface and the camera view. This makes the texture look smooth from up close, and smooth from a distance. Anisotropic filtering improves texture quality on surfaces that are almost in line with the camera, but is slightly slower. The anisotropic filtering level can be changed by adjusting ProjectSettings.rendering/textures/default_filters/anisotropic_filtering_level.

Note: This texture filter is rarely useful in 2D projects. CANVAS_ITEM_TEXTURE_FILTER_LINEAR_WITH_MIPMAPS is usually more appropriate in this case.

CanvasItemTextureFilter CANVAS_ITEM_TEXTURE_FILTER_MAX = 7

Max value for CanvasItemTextureFilter enum.

enum CanvasItemTextureRepeat: 🔗

CanvasItemTextureRepeat CANVAS_ITEM_TEXTURE_REPEAT_DEFAULT = 0

Uses the default repeat mode for this Viewport.

CanvasItemTextureRepeat CANVAS_ITEM_TEXTURE_REPEAT_DISABLED = 1

Disables textures repeating. Instead, when reading UVs outside the 0-1 range, the value will be clamped to the edge of the texture, resulting in a stretched out look at the borders of the texture.

CanvasItemTextureRepeat CANVAS_ITEM_TEXTURE_REPEAT_ENABLED = 2

Enables the texture to repeat when UV coordinates are outside the 0-1 range. If using one of the linear filtering modes, this can result in artifacts at the edges of a texture when the sampler filters across the edges of the texture.

CanvasItemTextureRepeat CANVAS_ITEM_TEXTURE_REPEAT_MIRROR = 3

Flip the texture when repeating so that the edge lines up instead of abruptly changing.

CanvasItemTextureRepeat CANVAS_ITEM_TEXTURE_REPEAT_MAX = 4

Max value for CanvasItemTextureRepeat enum.

enum CanvasGroupMode: 🔗

CanvasGroupMode CANVAS_GROUP_MODE_DISABLED = 0

Child draws over parent and is not clipped.

CanvasGroupMode CANVAS_GROUP_MODE_CLIP_ONLY = 1

Parent is used for the purposes of clipping only. Child is clipped to the parent's visible area, parent is not drawn.

CanvasGroupMode CANVAS_GROUP_MODE_CLIP_AND_DRAW = 2

Parent is used for clipping child, but parent is also drawn underneath child as normal before clipping child to its visible area.

CanvasGroupMode CANVAS_GROUP_MODE_TRANSPARENT = 3

There is currently no description for this enum. Please help us by contributing one!

enum CanvasLightMode: 🔗

CanvasLightMode CANVAS_LIGHT_MODE_POINT = 0

2D point light (see PointLight2D).

CanvasLightMode CANVAS_LIGHT_MODE_DIRECTIONAL = 1

2D directional (sun/moon) light (see DirectionalLight2D).

enum CanvasLightBlendMode: 🔗

CanvasLightBlendMode CANVAS_LIGHT_BLEND_MODE_ADD = 0

Adds light color additive to the canvas.

CanvasLightBlendMode CANVAS_LIGHT_BLEND_MODE_SUB = 1

Adds light color subtractive to the canvas.

CanvasLightBlendMode CANVAS_LIGHT_BLEND_MODE_MIX = 2

The light adds color depending on transparency.

enum CanvasLightShadowFilter: 🔗

CanvasLightShadowFilter CANVAS_LIGHT_FILTER_NONE = 0

Do not apply a filter to canvas light shadows.

CanvasLightShadowFilter CANVAS_LIGHT_FILTER_PCF5 = 1

Use PCF5 filtering to filter canvas light shadows.

CanvasLightShadowFilter CANVAS_LIGHT_FILTER_PCF13 = 2

Use PCF13 filtering to filter canvas light shadows.

CanvasLightShadowFilter CANVAS_LIGHT_FILTER_MAX = 3

Max value of the CanvasLightShadowFilter enum.

enum CanvasOccluderPolygonCullMode: 🔗

CanvasOccluderPolygonCullMode CANVAS_OCCLUDER_POLYGON_CULL_DISABLED = 0

Culling of the canvas occluder is disabled.

CanvasOccluderPolygonCullMode CANVAS_OCCLUDER_POLYGON_CULL_CLOCKWISE = 1

Culling of the canvas occluder is clockwise.

CanvasOccluderPolygonCullMode CANVAS_OCCLUDER_POLYGON_CULL_COUNTER_CLOCKWISE = 2

Culling of the canvas occluder is counterclockwise.

enum GlobalShaderParameterType: 🔗

GlobalShaderParameterType GLOBAL_VAR_TYPE_BOOL = 0

Boolean global shader parameter (global uniform bool ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_BVEC2 = 1

2-dimensional boolean vector global shader parameter (global uniform bvec2 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_BVEC3 = 2

3-dimensional boolean vector global shader parameter (global uniform bvec3 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_BVEC4 = 3

4-dimensional boolean vector global shader parameter (global uniform bvec4 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_INT = 4

Integer global shader parameter (global uniform int ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_IVEC2 = 5

2-dimensional integer vector global shader parameter (global uniform ivec2 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_IVEC3 = 6

3-dimensional integer vector global shader parameter (global uniform ivec3 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_IVEC4 = 7

4-dimensional integer vector global shader parameter (global uniform ivec4 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_RECT2I = 8

2-dimensional integer rectangle global shader parameter (global uniform ivec4 ...). Equivalent to GLOBAL_VAR_TYPE_IVEC4 in shader code, but exposed as a Rect2i in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_UINT = 9

Unsigned integer global shader parameter (global uniform uint ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_UVEC2 = 10

2-dimensional unsigned integer vector global shader parameter (global uniform uvec2 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_UVEC3 = 11

3-dimensional unsigned integer vector global shader parameter (global uniform uvec3 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_UVEC4 = 12

4-dimensional unsigned integer vector global shader parameter (global uniform uvec4 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_FLOAT = 13

Single-precision floating-point global shader parameter (global uniform float ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_VEC2 = 14

2-dimensional floating-point vector global shader parameter (global uniform vec2 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_VEC3 = 15

3-dimensional floating-point vector global shader parameter (global uniform vec3 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_VEC4 = 16

4-dimensional floating-point vector global shader parameter (global uniform vec4 ...).

GlobalShaderParameterType GLOBAL_VAR_TYPE_COLOR = 17

Color global shader parameter (global uniform vec4 ...). Equivalent to GLOBAL_VAR_TYPE_VEC4 in shader code, but exposed as a Color in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_RECT2 = 18

2-dimensional floating-point rectangle global shader parameter (global uniform vec4 ...). Equivalent to GLOBAL_VAR_TYPE_VEC4 in shader code, but exposed as a Rect2 in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_MAT2 = 19

2×2 matrix global shader parameter (global uniform mat2 ...). Exposed as a PackedInt32Array in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_MAT3 = 20

3×3 matrix global shader parameter (global uniform mat3 ...). Exposed as a Basis in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_MAT4 = 21

4×4 matrix global shader parameter (global uniform mat4 ...). Exposed as a Projection in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_TRANSFORM_2D = 22

2-dimensional transform global shader parameter (global uniform mat2x3 ...). Exposed as a Transform2D in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_TRANSFORM = 23

3-dimensional transform global shader parameter (global uniform mat3x4 ...). Exposed as a Transform3D in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_SAMPLER2D = 24

2D sampler global shader parameter (global uniform sampler2D ...). Exposed as a Texture2D in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_SAMPLER2DARRAY = 25

2D sampler array global shader parameter (global uniform sampler2DArray ...). Exposed as a Texture2DArray in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_SAMPLER3D = 26

3D sampler global shader parameter (global uniform sampler3D ...). Exposed as a Texture3D in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_SAMPLERCUBE = 27

Cubemap sampler global shader parameter (global uniform samplerCube ...). Exposed as a Cubemap in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_SAMPLEREXT = 28

External sampler global shader parameter (global uniform samplerExternalOES ...). Exposed as an ExternalTexture in the editor UI.

GlobalShaderParameterType GLOBAL_VAR_TYPE_MAX = 29

Represents the size of the GlobalShaderParameterType enum.

enum RenderingInfo: 🔗

RenderingInfo RENDERING_INFO_TOTAL_OBJECTS_IN_FRAME = 0

Number of objects rendered in the current 3D scene. This varies depending on camera position and rotation.

RenderingInfo RENDERING_INFO_TOTAL_PRIMITIVES_IN_FRAME = 1

Number of points, lines, or triangles rendered in the current 3D scene. This varies depending on camera position and rotation.

RenderingInfo RENDERING_INFO_TOTAL_DRAW_CALLS_IN_FRAME = 2

Number of draw calls performed to render in the current 3D scene. This varies depending on camera position and rotation.

RenderingInfo RENDERING_INFO_TEXTURE_MEM_USED = 3

Texture memory used (in bytes).

RenderingInfo RENDERING_INFO_BUFFER_MEM_USED = 4

Buffer memory used (in bytes). This includes vertex data, uniform buffers, and many miscellaneous buffer types used internally.

RenderingInfo RENDERING_INFO_VIDEO_MEM_USED = 5

Video memory used (in bytes). When using the Forward+ or Mobile renderers, this is always greater than the sum of RENDERING_INFO_TEXTURE_MEM_USED and RENDERING_INFO_BUFFER_MEM_USED, since there is miscellaneous data not accounted for by those two metrics. When using the Compatibility renderer, this is equal to the sum of RENDERING_INFO_TEXTURE_MEM_USED and RENDERING_INFO_BUFFER_MEM_USED.

RenderingInfo RENDERING_INFO_PIPELINE_COMPILATIONS_CANVAS = 6

Number of pipeline compilations that were triggered by the 2D canvas renderer.

RenderingInfo RENDERING_INFO_PIPELINE_COMPILATIONS_MESH = 7

Number of pipeline compilations that were triggered by loading meshes. These compilations will show up as longer loading times the first time a user runs the game and the pipeline is required.

RenderingInfo RENDERING_INFO_PIPELINE_COMPILATIONS_SURFACE = 8

Number of pipeline compilations that were triggered by building the surface cache before rendering the scene. These compilations will show up as a stutter when loading a scene the first time a user runs the game and the pipeline is required.

RenderingInfo RENDERING_INFO_PIPELINE_COMPILATIONS_DRAW = 9

Number of pipeline compilations that were triggered while drawing the scene. These compilations will show up as stutters during gameplay the first time a user runs the game and the pipeline is required.

RenderingInfo RENDERING_INFO_PIPELINE_COMPILATIONS_SPECIALIZATION = 10

Number of pipeline compilations that were triggered to optimize the current scene. These compilations are done in the background and should not cause any stutters whatsoever.

enum PipelineSource: 🔗

PipelineSource PIPELINE_SOURCE_CANVAS = 0

Pipeline compilation that was triggered by the 2D canvas renderer.

PipelineSource PIPELINE_SOURCE_MESH = 1

Pipeline compilation that was triggered by loading a mesh.

PipelineSource PIPELINE_SOURCE_SURFACE = 2

Pipeline compilation that was triggered by building the surface cache before rendering the scene.

PipelineSource PIPELINE_SOURCE_DRAW = 3

Pipeline compilation that was triggered while drawing the scene.

PipelineSource PIPELINE_SOURCE_SPECIALIZATION = 4

Pipeline compilation that was triggered to optimize the current scene.

PipelineSource PIPELINE_SOURCE_MAX = 5

Represents the size of the PipelineSource enum.

Features FEATURE_SHADERS = 0

Deprecated: This constant has not been used since Godot 3.0.

Features FEATURE_MULTITHREADED = 1

Deprecated: This constant has not been used since Godot 3.0.

NO_INDEX_ARRAY = -1 🔗

Marks an error that shows that the index array is empty.

ARRAY_WEIGHTS_SIZE = 4 🔗

Number of weights/bones per vertex.

CANVAS_ITEM_Z_MIN = -4096 🔗

The minimum Z-layer for canvas items.

CANVAS_ITEM_Z_MAX = 4096 🔗

The maximum Z-layer for canvas items.

CANVAS_LAYER_MIN = -2147483648 🔗

The minimum canvas layer.

CANVAS_LAYER_MAX = 2147483647 🔗

The maximum canvas layer.

MAX_GLOW_LEVELS = 7 🔗

The maximum number of glow levels that can be used with the glow post-processing effect.

Deprecated: This constant is not used by the engine.

MAX_2D_DIRECTIONAL_LIGHTS = 8 🔗

The maximum number of directional lights that can be rendered at a given time in 2D.

MAX_MESH_SURFACES = 256 🔗

The maximum number of surfaces a mesh can have.

MATERIAL_RENDER_PRIORITY_MIN = -128 🔗

The minimum renderpriority of all materials.

MATERIAL_RENDER_PRIORITY_MAX = 127 🔗

The maximum renderpriority of all materials.

ARRAY_CUSTOM_COUNT = 4 🔗

The number of custom data arrays available (ARRAY_CUSTOM0, ARRAY_CUSTOM1, ARRAY_CUSTOM2, ARRAY_CUSTOM3).

PARTICLES_EMIT_FLAG_POSITION = 1 🔗

There is currently no description for this constant. Please help us by contributing one!

PARTICLES_EMIT_FLAG_ROTATION_SCALE = 2 🔗

There is currently no description for this constant. Please help us by contributing one!

PARTICLES_EMIT_FLAG_VELOCITY = 4 🔗

There is currently no description for this constant. Please help us by contributing one!

PARTICLES_EMIT_FLAG_COLOR = 8 🔗

There is currently no description for this constant. Please help us by contributing one!

PARTICLES_EMIT_FLAG_CUSTOM = 16 🔗

There is currently no description for this constant. Please help us by contributing one!

bool render_loop_enabled 🔗

void set_render_loop_enabled(value: bool)

bool is_render_loop_enabled()

If false, disables rendering completely, but the engine logic is still being processed. You can call force_draw() to draw a frame even with rendering disabled.

Array[Image] bake_render_uv2(base: RID, material_overrides: Array[RID], image_size: Vector2i) 🔗

Bakes the material data of the Mesh passed in the base parameter with optional material_overrides to a set of Images of size image_size. Returns an array of Images containing material properties as specified in BakeChannels.

void call_on_render_thread(callable: Callable) 🔗

As the RenderingServer actual logic may run on a separate thread, accessing its internals from the main (or any other) thread will result in errors. To make it easier to run code that can safely access the rendering internals (such as RenderingDevice and similar RD classes), push a callable via this function so it will be executed on the render thread.

RID camera_attributes_create() 🔗

Creates a camera attributes object and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all camera_attributes_ RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent resource is CameraAttributes.

void camera_attributes_set_auto_exposure(camera_attributes: RID, enable: bool, min_sensitivity: float, max_sensitivity: float, speed: float, scale: float) 🔗

Sets the parameters to use with the auto-exposure effect. These parameters take on the same meaning as their counterparts in CameraAttributes and CameraAttributesPractical.

void camera_attributes_set_dof_blur(camera_attributes: RID, far_enable: bool, far_distance: float, far_transition: float, near_enable: bool, near_distance: float, near_transition: float, amount: float) 🔗

Sets the parameters to use with the DOF blur effect. These parameters take on the same meaning as their counterparts in CameraAttributesPractical.

void camera_attributes_set_dof_blur_bokeh_shape(shape: DOFBokehShape) 🔗

Sets the shape of the DOF bokeh pattern to shape. Different shapes may be used to achieve artistic effect, or to meet performance targets.

void camera_attributes_set_dof_blur_quality(quality: DOFBlurQuality, use_jitter: bool) 🔗

Sets the quality level of the DOF blur effect to quality. use_jitter can be used to jitter samples taken during the blur pass to hide artifacts at the cost of looking more fuzzy.

void camera_attributes_set_exposure(camera_attributes: RID, multiplier: float, normalization: float) 🔗

Sets the exposure values that will be used by the renderers. The normalization amount is used to bake a given Exposure Value (EV) into rendering calculations to reduce the dynamic range of the scene.

The normalization factor can be calculated from exposure value (EV100) as follows:

The exposure value can be calculated from aperture (in f-stops), shutter speed (in seconds), and sensitivity (in ISO) as follows:

RID camera_create() 🔗

Creates a 3D camera and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all camera_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent node is Camera3D.

void camera_set_camera_attributes(camera: RID, effects: RID) 🔗

Sets the camera_attributes created with camera_attributes_create() to the given camera.

void camera_set_compositor(camera: RID, compositor: RID) 🔗

Sets the compositor used by this camera. Equivalent to Camera3D.compositor.

void camera_set_cull_mask(camera: RID, layers: int) 🔗

Sets the cull mask associated with this camera. The cull mask describes which 3D layers are rendered by this camera. Equivalent to Camera3D.cull_mask.

void camera_set_environment(camera: RID, env: RID) 🔗

Sets the environment used by this camera. Equivalent to Camera3D.environment.

void camera_set_frustum(camera: RID, size: float, offset: Vector2, z_near: float, z_far: float) 🔗

Sets camera to use frustum projection. This mode allows adjusting the offset argument to create "tilted frustum" effects.

void camera_set_orthogonal(camera: RID, size: float, z_near: float, z_far: float) 🔗

Sets camera to use orthogonal projection, also known as orthographic projection. Objects remain the same size on the screen no matter how far away they are.

void camera_set_perspective(camera: RID, fovy_degrees: float, z_near: float, z_far: float) 🔗

Sets camera to use perspective projection. Objects on the screen becomes smaller when they are far away.

void camera_set_transform(camera: RID, transform: Transform3D) 🔗

Sets Transform3D of camera.

void camera_set_use_vertical_aspect(camera: RID, enable: bool) 🔗

If true, preserves the horizontal aspect ratio which is equivalent to Camera3D.KEEP_WIDTH. If false, preserves the vertical aspect ratio which is equivalent to Camera3D.KEEP_HEIGHT.

RID canvas_create() 🔗

Creates a canvas and returns the assigned RID. It can be accessed with the RID that is returned. This RID will be used in all canvas_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Canvas has no Resource or Node equivalent.

void canvas_item_add_animation_slice(item: RID, animation_length: float, slice_begin: float, slice_end: float, offset: float = 0.0) 🔗

Subsequent drawing commands will be ignored unless they fall within the specified animation slice. This is a faster way to implement animations that loop on background rather than redrawing constantly.

void canvas_item_add_circle(item: RID, pos: Vector2, radius: float, color: Color, antialiased: bool = false) 🔗

Draws a circle on the CanvasItem pointed to by the item RID. See also CanvasItem.draw_circle().

void canvas_item_add_clip_ignore(item: RID, ignore: bool) 🔗

If ignore is true, ignore clipping on items drawn with this canvas item until this is called again with ignore set to false.

void canvas_item_add_lcd_texture_rect_region(item: RID, rect: Rect2, texture: RID, src_rect: Rect2, modulate: Color) 🔗

See also CanvasItem.draw_lcd_texture_rect_region().

void canvas_item_add_line(item: RID, from: Vector2, to: Vector2, color: Color, width: float = -1.0, antialiased: bool = false) 🔗

Draws a line on the CanvasItem pointed to by the item RID. See also CanvasItem.draw_line().

void canvas_item_add_mesh(item: RID, mesh: RID, transform: Transform2D = Transform2D(1, 0, 0, 1, 0, 0), modulate: Color = Color(1, 1, 1, 1), texture: RID = RID()) 🔗

Draws a mesh created with mesh_create() with given transform, modulate color, and texture. This is used internally by MeshInstance2D.

void canvas_item_add_msdf_texture_rect_region(item: RID, rect: Rect2, texture: RID, src_rect: Rect2, modulate: Color = Color(1, 1, 1, 1), outline_size: int = 0, px_range: float = 1.0, scale: float = 1.0) 🔗

See also CanvasItem.draw_msdf_texture_rect_region().

void canvas_item_add_multiline(item: RID, points: PackedVector2Array, colors: PackedColorArray, width: float = -1.0, antialiased: bool = false) 🔗

Draws a 2D multiline on the CanvasItem pointed to by the item RID. See also CanvasItem.draw_multiline() and CanvasItem.draw_multiline_colors().

void canvas_item_add_multimesh(item: RID, mesh: RID, texture: RID = RID()) 🔗

Draws a 2D MultiMesh on the CanvasItem pointed to by the item RID. See also CanvasItem.draw_multimesh().

void canvas_item_add_nine_patch(item: RID, rect: Rect2, source: Rect2, texture: RID, topleft: Vector2, bottomright: Vector2, x_axis_mode: NinePatchAxisMode = 0, y_axis_mode: NinePatchAxisMode = 0, draw_center: bool = true, modulate: Color = Color(1, 1, 1, 1)) 🔗

Draws a nine-patch rectangle on the CanvasItem pointed to by the item RID.

void canvas_item_add_particles(item: RID, particles: RID, texture: RID) 🔗

Draws particles on the CanvasItem pointed to by the item RID.

void canvas_item_add_polygon(item: RID, points: PackedVector2Array, colors: PackedColorArray, uvs: PackedVector2Array = PackedVector2Array(), texture: RID = RID()) 🔗

Draws a 2D polygon on the CanvasItem pointed to by the item RID. If you need more flexibility (such as being able to use bones), use canvas_item_add_triangle_array() instead. See also CanvasItem.draw_polygon().

Note: If you frequently redraw the same polygon with a large number of vertices, consider pre-calculating the triangulation with Geometry2D.triangulate_polygon() and using CanvasItem.draw_mesh(), CanvasItem.draw_multimesh(), or canvas_item_add_triangle_array().

void canvas_item_add_polyline(item: RID, points: PackedVector2Array, colors: PackedColorArray, width: float = -1.0, antialiased: bool = false) 🔗

Draws a 2D polyline on the CanvasItem pointed to by the item RID. See also CanvasItem.draw_polyline() and CanvasItem.draw_polyline_colors().

void canvas_item_add_primitive(item: RID, points: PackedVector2Array, colors: PackedColorArray, uvs: PackedVector2Array, texture: RID) 🔗

Draws a 2D primitive on the CanvasItem pointed to by the item RID. See also CanvasItem.draw_primitive().

void canvas_item_add_rect(item: RID, rect: Rect2, color: Color, antialiased: bool = false) 🔗

Draws a rectangle on the CanvasItem pointed to by the item RID. See also CanvasItem.draw_rect().

void canvas_item_add_set_transform(item: RID, transform: Transform2D) 🔗

Sets a Transform2D that will be used to transform subsequent canvas item commands.

void canvas_item_add_texture_rect(item: RID, rect: Rect2, texture: RID, tile: bool = false, modulate: Color = Color(1, 1, 1, 1), transpose: bool = false) 🔗

Draws a 2D textured rectangle on the CanvasItem pointed to by the item RID. See also CanvasItem.draw_texture_rect() and Texture2D.draw_rect().

void canvas_item_add_texture_rect_region(item: RID, rect: Rect2, texture: RID, src_rect: Rect2, modulate: Color = Color(1, 1, 1, 1), transpose: bool = false, clip_uv: bool = true) 🔗

Draws the specified region of a 2D textured rectangle on the CanvasItem pointed to by the item RID. See also CanvasItem.draw_texture_rect_region() and Texture2D.draw_rect_region().

void canvas_item_add_triangle_array(item: RID, indices: PackedInt32Array, points: PackedVector2Array, colors: PackedColorArray, uvs: PackedVector2Array = PackedVector2Array(), bones: PackedInt32Array = PackedInt32Array(), weights: PackedFloat32Array = PackedFloat32Array(), texture: RID = RID(), count: int = -1) 🔗

Draws a triangle array on the CanvasItem pointed to by the item RID. This is internally used by Line2D and StyleBoxFlat for rendering. canvas_item_add_triangle_array() is highly flexible, but more complex to use than canvas_item_add_polygon().

Note: If count is set to a non-negative value, only the first count * 3 indices (corresponding to count triangles) will be drawn. Otherwise, all indices are drawn.

void canvas_item_attach_skeleton(item: RID, skeleton: RID) 🔗

Attaches a skeleton to the CanvasItem. Removes the previous skeleton.

void canvas_item_clear(item: RID) 🔗

Clears the CanvasItem and removes all commands in it.

RID canvas_item_create() 🔗

Creates a new CanvasItem instance and returns its RID. It can be accessed with the RID that is returned. This RID will be used in all canvas_item_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent node is CanvasItem.

Variant canvas_item_get_instance_shader_parameter(instance: RID, parameter: StringName) const 🔗

Returns the value of the per-instance shader uniform from the specified canvas item instance. Equivalent to CanvasItem.get_instance_shader_parameter().

Variant canvas_item_get_instance_shader_parameter_default_value(instance: RID, parameter: StringName) const 🔗

Returns the default value of the per-instance shader uniform from the specified canvas item instance. Equivalent to CanvasItem.get_instance_shader_parameter().

Array[Dictionary] canvas_item_get_instance_shader_parameter_list(instance: RID) const 🔗

Returns a dictionary of per-instance shader uniform names of the per-instance shader uniform from the specified canvas item instance.

The returned dictionary is in PropertyInfo format, with the keys name, class_name, type, hint, hint_string, and usage.

void canvas_item_reset_physics_interpolation(item: RID) 🔗

Prevents physics interpolation for the current physics tick.

This is useful when moving a canvas item to a new location, to give an instantaneous change rather than interpolation from the previous location.

void canvas_item_set_canvas_group_mode(item: RID, mode: CanvasGroupMode, clear_margin: float = 5.0, fit_empty: bool = false, fit_margin: float = 0.0, blur_mipmaps: bool = false) 🔗

Sets the canvas group mode used during 2D rendering for the canvas item specified by the item RID. For faster but more limited clipping, use canvas_item_set_clip() instead.

Note: The equivalent node functionality is found in CanvasGroup and CanvasItem.clip_children.

void canvas_item_set_clip(item: RID, clip: bool) 🔗

If clip is true, makes the canvas item specified by the item RID not draw anything outside of its rect's coordinates. This clipping is fast, but works only with axis-aligned rectangles. This means that rotation is ignored by the clipping rectangle. For more advanced clipping shapes, use canvas_item_set_canvas_group_mode() instead.

Note: The equivalent node functionality is found in Label.clip_text, RichTextLabel (always enabled) and more.

void canvas_item_set_copy_to_backbuffer(item: RID, enabled: bool, rect: Rect2) 🔗

Sets the CanvasItem to copy a rect to the backbuffer.

void canvas_item_set_custom_rect(item: RID, use_custom_rect: bool, rect: Rect2 = Rect2(0, 0, 0, 0)) 🔗

If use_custom_rect is true, sets the custom visibility rectangle (used for culling) to rect for the canvas item specified by item. Setting a custom visibility rect can reduce CPU load when drawing lots of 2D instances. If use_custom_rect is false, automatically computes a visibility rectangle based on the canvas item's draw commands.

void canvas_item_set_default_texture_filter(item: RID, filter: CanvasItemTextureFilter) 🔗

Sets the default texture filter mode for the canvas item specified by the item RID. Equivalent to CanvasItem.texture_filter.

void canvas_item_set_default_texture_repeat(item: RID, repeat: CanvasItemTextureRepeat) 🔗

Sets the default texture repeat mode for the canvas item specified by the item RID. Equivalent to CanvasItem.texture_repeat.

void canvas_item_set_distance_field_mode(item: RID, enabled: bool) 🔗

If enabled is true, enables multichannel signed distance field rendering mode for the canvas item specified by the item RID. This is meant to be used for font rendering, or with specially generated images using msdfgen.

void canvas_item_set_draw_behind_parent(item: RID, enabled: bool) 🔗

If enabled is true, draws the canvas item specified by the item RID behind its parent. Equivalent to CanvasItem.show_behind_parent.

void canvas_item_set_draw_index(item: RID, index: int) 🔗

Sets the index for the CanvasItem.

void canvas_item_set_instance_shader_parameter(instance: RID, parameter: StringName, value: Variant) 🔗

Sets the per-instance shader uniform on the specified canvas item instance. Equivalent to CanvasItem.set_instance_shader_parameter().

void canvas_item_set_interpolated(item: RID, interpolated: bool) 🔗

If interpolated is true, turns on physics interpolation for the canvas item.

void canvas_item_set_light_mask(item: RID, mask: int) 🔗

Sets the light mask for the canvas item specified by the item RID. Equivalent to CanvasItem.light_mask.

void canvas_item_set_material(item: RID, material: RID) 🔗

Sets a new material to the canvas item specified by the item RID. Equivalent to CanvasItem.material.

void canvas_item_set_modulate(item: RID, color: Color) 🔗

Multiplies the color of the canvas item specified by the item RID, while affecting its children. See also canvas_item_set_self_modulate(). Equivalent to CanvasItem.modulate.

void canvas_item_set_parent(item: RID, parent: RID) 🔗

Sets a parent CanvasItem to the CanvasItem. The item will inherit transform, modulation and visibility from its parent, like CanvasItem nodes in the scene tree.

void canvas_item_set_self_modulate(item: RID, color: Color) 🔗

Multiplies the color of the canvas item specified by the item RID, without affecting its children. See also canvas_item_set_modulate(). Equivalent to CanvasItem.self_modulate.

void canvas_item_set_sort_children_by_y(item: RID, enabled: bool) 🔗

If enabled is true, child nodes with the lowest Y position are drawn before those with a higher Y position. Y-sorting only affects children that inherit from the canvas item specified by the item RID, not the canvas item itself. Equivalent to CanvasItem.y_sort_enabled.

void canvas_item_set_transform(item: RID, transform: Transform2D) 🔗

Sets the transform of the canvas item specified by the item RID. This affects where and how the item will be drawn. Child canvas items' transforms are multiplied by their parent's transform. Equivalent to Node2D.transform.

void canvas_item_set_use_parent_material(item: RID, enabled: bool) 🔗

Sets if the CanvasItem uses its parent's material.

void canvas_item_set_visibility_layer(item: RID, visibility_layer: int) 🔗

Sets the rendering visibility layer associated with this CanvasItem. Only Viewport nodes with a matching rendering mask will render this CanvasItem.

void canvas_item_set_visibility_notifier(item: RID, enable: bool, area: Rect2, enter_callable: Callable, exit_callable: Callable) 🔗

Sets the given CanvasItem as visibility notifier. area defines the area of detecting visibility. enter_callable is called when the CanvasItem enters the screen, exit_callable is called when the CanvasItem exits the screen. If enable is false, the item will no longer function as notifier.

This method can be used to manually mimic VisibleOnScreenNotifier2D.

void canvas_item_set_visible(item: RID, visible: bool) 🔗

Sets the visibility of the CanvasItem.

void canvas_item_set_z_as_relative_to_parent(item: RID, enabled: bool) 🔗

If this is enabled, the Z index of the parent will be added to the children's Z index.

void canvas_item_set_z_index(item: RID, z_index: int) 🔗

Sets the CanvasItem's Z index, i.e. its draw order (lower indexes are drawn first).

void canvas_item_transform_physics_interpolation(item: RID, transform: Transform2D) 🔗

Transforms both the current and previous stored transform for a canvas item.

This allows transforming a canvas item without creating a "glitch" in the interpolation, which is particularly useful for large worlds utilizing a shifting origin.

void canvas_light_attach_to_canvas(light: RID, canvas: RID) 🔗

Attaches the canvas light to the canvas. Removes it from its previous canvas.

RID canvas_light_create() 🔗

Creates a canvas light and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all canvas_light_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent node is Light2D.

void canvas_light_occluder_attach_to_canvas(occluder: RID, canvas: RID) 🔗

Attaches a light occluder to the canvas. Removes it from its previous canvas.

RID canvas_light_occluder_create() 🔗

Creates a light occluder and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all canvas_light_occluder_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent node is LightOccluder2D.

void canvas_light_occluder_reset_physics_interpolation(occluder: RID) 🔗

Prevents physics interpolation for the current physics tick.

This is useful when moving an occluder to a new location, to give an instantaneous change rather than interpolation from the previous location.

void canvas_light_occluder_set_as_sdf_collision(occluder: RID, enable: bool) 🔗

There is currently no description for this method. Please help us by contributing one!

void canvas_light_occluder_set_enabled(occluder: RID, enabled: bool) 🔗

Enables or disables light occluder.

void canvas_light_occluder_set_interpolated(occluder: RID, interpolated: bool) 🔗

If interpolated is true, turns on physics interpolation for the light occluder.

void canvas_light_occluder_set_light_mask(occluder: RID, mask: int) 🔗

The light mask. See LightOccluder2D for more information on light masks.

void canvas_light_occluder_set_polygon(occluder: RID, polygon: RID) 🔗

Sets a light occluder's polygon.

void canvas_light_occluder_set_transform(occluder: RID, transform: Transform2D) 🔗

Sets a light occluder's Transform2D.

void canvas_light_occluder_transform_physics_interpolation(occluder: RID, transform: Transform2D) 🔗

Transforms both the current and previous stored transform for a light occluder.

This allows transforming an occluder without creating a "glitch" in the interpolation, which is particularly useful for large worlds utilizing a shifting origin.

void canvas_light_reset_physics_interpolation(light: RID) 🔗

Prevents physics interpolation for the current physics tick.

This is useful when moving a canvas item to a new location, to give an instantaneous change rather than interpolation from the previous location.

void canvas_light_set_blend_mode(light: RID, mode: CanvasLightBlendMode) 🔗

Sets the blend mode for the given canvas light to mode. Equivalent to Light2D.blend_mode.

void canvas_light_set_color(light: RID, color: Color) 🔗

Sets the color for a light.

void canvas_light_set_enabled(light: RID, enabled: bool) 🔗

Enables or disables a canvas light.

void canvas_light_set_energy(light: RID, energy: float) 🔗

Sets a canvas light's energy.

void canvas_light_set_height(light: RID, height: float) 🔗

Sets a canvas light's height.

void canvas_light_set_interpolated(light: RID, interpolated: bool) 🔗

If interpolated is true, turns on physics interpolation for the canvas light.

void canvas_light_set_item_cull_mask(light: RID, mask: int) 🔗

The light mask. See LightOccluder2D for more information on light masks.

void canvas_light_set_item_shadow_cull_mask(light: RID, mask: int) 🔗

The binary mask used to determine which layers this canvas light's shadows affects. See LightOccluder2D for more information on light masks.

void canvas_light_set_layer_range(light: RID, min_layer: int, max_layer: int) 🔗

The layer range that gets rendered with this light.

void canvas_light_set_mode(light: RID, mode: CanvasLightMode) 🔗

Sets the mode of the canvas light.

void canvas_light_set_shadow_color(light: RID, color: Color) 🔗

Sets the color of the canvas light's shadow.

void canvas_light_set_shadow_enabled(light: RID, enabled: bool) 🔗

Enables or disables the canvas light's shadow.

void canvas_light_set_shadow_filter(light: RID, filter: CanvasLightShadowFilter) 🔗

Sets the canvas light's shadow's filter.

void canvas_light_set_shadow_smooth(light: RID, smooth: float) 🔗

Smoothens the shadow. The lower, the smoother.

void canvas_light_set_texture(light: RID, texture: RID) 🔗

Sets the texture to be used by a PointLight2D. Equivalent to PointLight2D.texture.

void canvas_light_set_texture_offset(light: RID, offset: Vector2) 🔗

Sets the offset of a PointLight2D's texture. Equivalent to PointLight2D.offset.

void canvas_light_set_texture_scale(light: RID, scale: float) 🔗

Sets the scale factor of a PointLight2D's texture. Equivalent to PointLight2D.texture_scale.

void canvas_light_set_transform(light: RID, transform: Transform2D) 🔗

Sets the canvas light's Transform2D.

void canvas_light_set_z_range(light: RID, min_z: int, max_z: int) 🔗

Sets the Z range of objects that will be affected by this light. Equivalent to Light2D.range_z_min and Light2D.range_z_max.

void canvas_light_transform_physics_interpolation(light: RID, transform: Transform2D) 🔗

Transforms both the current and previous stored transform for a canvas light.

This allows transforming a light without creating a "glitch" in the interpolation, which is particularly useful for large worlds utilizing a shifting origin.

RID canvas_occluder_polygon_create() 🔗

Creates a new light occluder polygon and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all canvas_occluder_polygon_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent resource is OccluderPolygon2D.

void canvas_occluder_polygon_set_cull_mode(occluder_polygon: RID, mode: CanvasOccluderPolygonCullMode) 🔗

Sets an occluder polygon's cull mode.

void canvas_occluder_polygon_set_shape(occluder_polygon: RID, shape: PackedVector2Array, closed: bool) 🔗

Sets the shape of the occluder polygon.

void canvas_set_disable_scale(disable: bool) 🔗

There is currently no description for this method. Please help us by contributing one!

void canvas_set_item_mirroring(canvas: RID, item: RID, mirroring: Vector2) 🔗

A copy of the canvas item will be drawn with a local offset of the mirroring.

Note: This is equivalent to calling canvas_set_item_repeat() like canvas_set_item_repeat(item, mirroring, 1), with an additional check ensuring canvas is a parent of item.

void canvas_set_item_repeat(item: RID, repeat_size: Vector2, repeat_times: int) 🔗

A copy of the canvas item will be drawn with a local offset of the repeat_size by the number of times of the repeat_times. As the repeat_times increases, the copies will spread away from the origin texture.

void canvas_set_modulate(canvas: RID, color: Color) 🔗

Modulates all colors in the given canvas.

void canvas_set_shadow_texture_size(size: int) 🔗

Sets the ProjectSettings.rendering/2d/shadow_atlas/size to use for Light2D shadow rendering (in pixels). The value is rounded up to the nearest power of 2.

RID canvas_texture_create() 🔗

Creates a canvas texture and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all canvas_texture_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method. See also texture_2d_create().

Note: The equivalent resource is CanvasTexture and is only meant to be used in 2D rendering, not 3D.

void canvas_texture_set_channel(canvas_texture: RID, channel: CanvasTextureChannel, texture: RID) 🔗

Sets the channel's texture for the canvas texture specified by the canvas_texture RID. Equivalent to CanvasTexture.diffuse_texture, CanvasTexture.normal_texture and CanvasTexture.specular_texture.

void canvas_texture_set_shading_parameters(canvas_texture: RID, base_color: Color, shininess: float) 🔗

Sets the base_color and shininess to use for the canvas texture specified by the canvas_texture RID. Equivalent to CanvasTexture.specular_color and CanvasTexture.specular_shininess.

void canvas_texture_set_texture_filter(canvas_texture: RID, filter: CanvasItemTextureFilter) 🔗

Sets the texture filter mode to use for the canvas texture specified by the canvas_texture RID.

void canvas_texture_set_texture_repeat(canvas_texture: RID, repeat: CanvasItemTextureRepeat) 🔗

Sets the texture repeat mode to use for the canvas texture specified by the canvas_texture RID.

RID compositor_create() 🔗

Creates a new compositor and adds it to the RenderingServer. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

RID compositor_effect_create() 🔗

Creates a new rendering effect and adds it to the RenderingServer. It can be accessed with the RID that is returned.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

void compositor_effect_set_callback(effect: RID, callback_type: CompositorEffectCallbackType, callback: Callable) 🔗

Sets the callback type (callback_type) and callback method(callback) for this rendering effect.

void compositor_effect_set_enabled(effect: RID, enabled: bool) 🔗

Enables/disables this rendering effect.

void compositor_effect_set_flag(effect: RID, flag: CompositorEffectFlags, set: bool) 🔗

Sets the flag (flag) for this rendering effect to true or false (set).

void compositor_set_compositor_effects(compositor: RID, effects: Array[RID]) 🔗

Sets the compositor effects for the specified compositor RID. effects should be an array containing RIDs created with compositor_effect_create().

RenderingDevice create_local_rendering_device() const 🔗

Creates a RenderingDevice that can be used to do draw and compute operations on a separate thread. Cannot draw to the screen nor share data with the global RenderingDevice.

Note: When using the OpenGL rendering driver or when running in headless mode, this function always returns null.

Rect2 debug_canvas_item_get_rect(item: RID) 🔗

Returns the bounding rectangle for a canvas item in local space, as calculated by the renderer. This bound is used internally for culling.

Warning: This function is intended for debugging in the editor, and will pass through and return a zero Rect2 in exported projects.

Creates a decal and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all decal_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

To place in a scene, attach this decal to an instance using instance_set_base() using the returned RID.

Note: The equivalent node is Decal.

void decal_set_albedo_mix(decal: RID, albedo_mix: float) 🔗

Sets the albedo_mix in the decal specified by the decal RID. Equivalent to Decal.albedo_mix.

void decal_set_cull_mask(decal: RID, mask: int) 🔗

Sets the cull mask in the decal specified by the decal RID. Equivalent to Decal.cull_mask.

void decal_set_distance_fade(decal: RID, enabled: bool, begin: float, length: float) 🔗

Sets the distance fade parameters in the decal specified by the decal RID. Equivalent to Decal.distance_fade_enabled, Decal.distance_fade_begin and Decal.distance_fade_length.

void decal_set_emission_energy(decal: RID, energy: float) 🔗

Sets the emission energy in the decal specified by the decal RID. Equivalent to Decal.emission_energy.

void decal_set_fade(decal: RID, above: float, below: float) 🔗

Sets the upper fade (above) and lower fade (below) in the decal specified by the decal RID. Equivalent to Decal.upper_fade and Decal.lower_fade.

void decal_set_modulate(decal: RID, color: Color) 🔗

Sets the color multiplier in the decal specified by the decal RID to color. Equivalent to Decal.modulate.

void decal_set_normal_fade(decal: RID, fade: float) 🔗

Sets the normal fade in the decal specified by the decal RID. Equivalent to Decal.normal_fade.

void decal_set_size(decal: RID, size: Vector3) 🔗

Sets the size of the decal specified by the decal RID. Equivalent to Decal.size.

void decal_set_texture(decal: RID, type: DecalTexture, texture: RID) 🔗

Sets the texture in the given texture type slot for the specified decal. Equivalent to Decal.set_texture().

void decals_set_filter(filter: DecalFilter) 🔗

Sets the texture filter mode to use when rendering decals. This parameter is global and cannot be set on a per-decal basis.

RID directional_light_create() 🔗

Creates a directional light and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID can be used in most light_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

To place in a scene, attach this directional light to an instance using instance_set_base() using the returned RID.

Note: The equivalent node is DirectionalLight3D.

void directional_shadow_atlas_set_size(size: int, is_16bits: bool) 🔗

Sets the size of the directional light shadows in 3D. See also ProjectSettings.rendering/lights_and_shadows/directional_shadow/size. This parameter is global and cannot be set on a per-viewport basis.

void directional_soft_shadow_filter_set_quality(quality: ShadowQuality) 🔗

Sets the filter quality for directional light shadows in 3D. See also ProjectSettings.rendering/lights_and_shadows/directional_shadow/soft_shadow_filter_quality. This parameter is global and cannot be set on a per-viewport basis.

Image environment_bake_panorama(environment: RID, bake_irradiance: bool, size: Vector2i) 🔗

Generates and returns an Image containing the radiance map for the specified environment RID's sky. This supports built-in sky material and custom sky shaders. If bake_irradiance is true, the irradiance map is saved instead of the radiance map. The radiance map is used to render reflected light, while the irradiance map is used to render ambient light. See also sky_bake_panorama().

Note: The image is saved in linear color space without any tonemapping performed, which means it will look too dark if viewed directly in an image editor.

Note: size should be a 2:1 aspect ratio for the generated panorama to have square pixels. For radiance maps, there is no point in using a height greater than Sky.radiance_size, as it won't increase detail. Irradiance maps only contain low-frequency data, so there is usually no point in going past a size of 128×64 pixels when saving an irradiance map.

RID environment_create() 🔗

Creates an environment and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all environment_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent resource is Environment.

void environment_glow_set_use_bicubic_upscale(enable: bool) 🔗

If enable is true, enables bicubic upscaling for glow which improves quality at the cost of performance. Equivalent to ProjectSettings.rendering/environment/glow/upscale_mode.

Note: This setting is only effective when using the Forward+ or Mobile rendering methods, as Compatibility uses a different glow implementation.

void environment_set_adjustment(env: RID, enable: bool, brightness: float, contrast: float, saturation: float, use_1d_color_correction: bool, color_correction: RID) 🔗

Sets the values to be used with the "adjustments" post-process effect. See Environment for more details.

void environment_set_ambient_light(env: RID, color: Color, ambient: EnvironmentAmbientSource = 0, energy: float = 1.0, sky_contribution: float = 0.0, reflection_source: EnvironmentReflectionSource = 0) 🔗

Sets the values to be used for ambient light rendering. See Environment for more details.

void environment_set_background(env: RID, bg: EnvironmentBG) 🔗

Sets the environment's background mode. Equivalent to Environment.background_mode.

void environment_set_bg_color(env: RID, color: Color) 🔗

Color displayed for clear areas of the scene. Only effective if using the ENV_BG_COLOR background mode.

void environment_set_bg_energy(env: RID, multiplier: float, exposure_value: float) 🔗

Sets the intensity of the background color.

void environment_set_camera_id(env: RID, id: int) 🔗

Sets the camera ID to be used as environment background.

void environment_set_canvas_max_layer(env: RID, max_layer: int) 🔗

Sets the maximum layer to use if using Canvas background mode.

void environment_set_fog(env: RID, enable: bool, light_color: Color, light_energy: float, sun_scatter: float, density: float, height: float, height_density: float, aerial_perspective: float, sky_affect: float, fog_mode: EnvironmentFogMode = 0) 🔗

Configures fog for the specified environment RID. See fog_* properties in Environment for more information.

void environment_set_fog_depth(env: RID, curve: float, begin: float, end: float) 🔗

Configures fog depth for the specified environment RID. Only has an effect when the fog mode of the environment is ENV_FOG_MODE_DEPTH. See fog_depth_* properties in Environment for more information.

void environment_set_glow(env: RID, enable: bool, levels: PackedFloat32Array, intensity: float, strength: float, mix: float, bloom_threshold: float, blend_mode: EnvironmentGlowBlendMode, hdr_bleed_threshold: float, hdr_bleed_scale: float, hdr_luminance_cap: float, glow_map_strength: float, glow_map: RID) 🔗

Configures glow for the specified environment RID. See glow_* properties in Environment for more information.

void environment_set_sdfgi(env: RID, enable: bool, cascades: int, min_cell_size: float, y_scale: EnvironmentSDFGIYScale, use_occlusion: bool, bounce_feedback: float, read_sky: bool, energy: float, normal_bias: float, probe_bias: float) 🔗

Configures signed distance field global illumination for the specified environment RID. See sdfgi_* properties in Environment for more information.

void environment_set_sdfgi_frames_to_converge(frames: EnvironmentSDFGIFramesToConverge) 🔗

Sets the number of frames to use for converging signed distance field global illumination. Equivalent to ProjectSettings.rendering/global_illumination/sdfgi/frames_to_converge.

void environment_set_sdfgi_frames_to_update_light(frames: EnvironmentSDFGIFramesToUpdateLight) 🔗

Sets the update speed for dynamic lights' indirect lighting when computing signed distance field global illumination. Equivalent to ProjectSettings.rendering/global_illumination/sdfgi/frames_to_update_lights.

void environment_set_sdfgi_ray_count(ray_count: EnvironmentSDFGIRayCount) 🔗

Sets the number of rays to throw per frame when computing signed distance field global illumination. Equivalent to ProjectSettings.rendering/global_illumination/sdfgi/probe_ray_count.

void environment_set_sky(env: RID, sky: RID) 🔗

Sets the Sky to be used as the environment's background when using BGMode sky. Equivalent to Environment.sky.

void environment_set_sky_custom_fov(env: RID, scale: float) 🔗

Sets a custom field of view for the background Sky. Equivalent to Environment.sky_custom_fov.

void environment_set_sky_orientation(env: RID, orientation: Basis) 🔗

Sets the rotation of the background Sky expressed as a Basis. Equivalent to Environment.sky_rotation, where the rotation vector is used to construct the Basis.

void environment_set_ssao(env: RID, enable: bool, radius: float, intensity: float, power: float, detail: float, horizon: float, sharpness: float, light_affect: float, ao_channel_affect: float) 🔗

Sets the variables to be used with the screen-space ambient occlusion (SSAO) post-process effect. See Environment for more details.

void environment_set_ssao_quality(quality: EnvironmentSSAOQuality, half_size: bool, adaptive_target: float, blur_passes: int, fadeout_from: float, fadeout_to: float) 🔗

Sets the quality level of the screen-space ambient occlusion (SSAO) post-process effect. See Environment for more details.

void environment_set_ssil_quality(quality: EnvironmentSSILQuality, half_size: bool, adaptive_target: float, blur_passes: int, fadeout_from: float, fadeout_to: float) 🔗

Sets the quality level of the screen-space indirect lighting (SSIL) post-process effect. See Environment for more details.

void environment_set_ssr(env: RID, enable: bool, max_steps: int, fade_in: float, fade_out: float, depth_tolerance: float) 🔗

Sets the variables to be used with the screen-space reflections (SSR) post-process effect. See Environment for more details.

void environment_set_ssr_roughness_quality(quality: EnvironmentSSRRoughnessQuality) 🔗

There is currently no description for this method. Please help us by contributing one!

void environment_set_tonemap(env: RID, tone_mapper: EnvironmentToneMapper, exposure: float, white: float) 🔗

Sets the variables to be used with the "tonemap" post-process effect. See Environment for more details.

void environment_set_volumetric_fog(env: RID, enable: bool, density: float, albedo: Color, emission: Color, emission_energy: float, anisotropy: float, length: float, p_detail_spread: float, gi_inject: float, temporal_reprojection: bool, temporal_reprojection_amount: float, ambient_inject: float, sky_affect: float) 🔗

Sets the variables to be used with the volumetric fog post-process effect. See Environment for more details.

void environment_set_volumetric_fog_filter_active(active: bool) 🔗

Enables filtering of the volumetric fog scattering buffer. This results in much smoother volumes with very few under-sampling artifacts.

void environment_set_volumetric_fog_volume_size(size: int, depth: int) 🔗

Sets the resolution of the volumetric fog's froxel buffer. size is modified by the screen's aspect ratio and then used to set the width and height of the buffer. While depth is directly used to set the depth of the buffer.

RID fog_volume_create() 🔗

Creates a new fog volume and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all fog_volume_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent node is FogVolume.

void fog_volume_set_material(fog_volume: RID, material: RID) 🔗

Sets the Material of the fog volume. Can be either a FogMaterial or a custom ShaderMaterial.

void fog_volume_set_shape(fog_volume: RID, shape: FogVolumeShape) 🔗

Sets the shape of the fog volume to either FOG_VOLUME_SHAPE_ELLIPSOID, FOG_VOLUME_SHAPE_CONE, FOG_VOLUME_SHAPE_CYLINDER, FOG_VOLUME_SHAPE_BOX or FOG_VOLUME_SHAPE_WORLD.

void fog_volume_set_size(fog_volume: RID, size: Vector3) 🔗

Sets the size of the fog volume when shape is FOG_VOLUME_SHAPE_ELLIPSOID, FOG_VOLUME_SHAPE_CONE, FOG_VOLUME_SHAPE_CYLINDER or FOG_VOLUME_SHAPE_BOX.

void force_draw(swap_buffers: bool = true, frame_step: float = 0.0) 🔗

Forces redrawing of all viewports at once. Must be called from the main thread.

Forces a synchronization between the CPU and GPU, which may be required in certain cases. Only call this when needed, as CPU-GPU synchronization has a performance cost.

void free_rid(rid: RID) 🔗

Tries to free an object in the RenderingServer. To avoid memory leaks, this should be called after using an object as memory management does not occur automatically when using RenderingServer directly.

String get_current_rendering_driver_name() const 🔗

Returns the name of the current rendering driver. This can be vulkan, d3d12, metal, opengl3, opengl3_es, or opengl3_angle. See also get_current_rendering_method().

When ProjectSettings.rendering/renderer/rendering_method is forward_plus or mobile, the rendering driver is determined by ProjectSettings.rendering/rendering_device/driver.

When ProjectSettings.rendering/renderer/rendering_method is gl_compatibility, the rendering driver is determined by ProjectSettings.rendering/gl_compatibility/driver.

The rendering driver is also determined by the --rendering-driver command line argument that overrides this project setting, or an automatic fallback that is applied depending on the hardware.

String get_current_rendering_method() const 🔗

Returns the name of the current rendering method. This can be forward_plus, mobile, or gl_compatibility. See also get_current_rendering_driver_name().

The rendering method is determined by ProjectSettings.rendering/renderer/rendering_method, the --rendering-method command line argument that overrides this project setting, or an automatic fallback that is applied depending on the hardware.

Color get_default_clear_color() 🔗

Returns the default clear color which is used when a specific clear color has not been selected. See also set_default_clear_color().

float get_frame_setup_time_cpu() const 🔗

Returns the time taken to setup rendering on the CPU in milliseconds. This value is shared across all viewports and does not require viewport_set_measure_render_time() to be enabled on a viewport to be queried. See also viewport_get_measured_render_time_cpu().

RenderingDevice get_rendering_device() const 🔗

Returns the global RenderingDevice.

Note: When using the OpenGL rendering driver or when running in headless mode, this function always returns null.

int get_rendering_info(info: RenderingInfo) 🔗

Returns a statistic about the rendering engine which can be used for performance profiling. See also viewport_get_render_info(), which returns information specific to a viewport.

Note: Only 3D rendering is currently taken into account by some of these values, such as the number of draw calls.

Note: Rendering information is not available until at least 2 frames have been rendered by the engine. If rendering information is not available, get_rendering_info() returns 0. To print rendering information in _ready() successfully, use the following:

Array[Dictionary] get_shader_parameter_list(shader: RID) const 🔗

Returns the parameters of a shader.

RID get_test_cube() 🔗

Returns the RID of the test cube. This mesh will be created and returned on the first call to get_test_cube(), then it will be cached for subsequent calls. See also make_sphere_mesh().

RID get_test_texture() 🔗

Returns the RID of a 256×256 texture with a testing pattern on it (in Image.FORMAT_RGB8 format). This texture will be created and returned on the first call to get_test_texture(), then it will be cached for subsequent calls. See also get_white_texture().

Example: Get the test texture and apply it to a Sprite2D node:

String get_video_adapter_api_version() const 🔗

Returns the version of the graphics video adapter currently in use (e.g. "1.2.189" for Vulkan, "3.3.0 NVIDIA 510.60.02" for OpenGL). This version may be different from the actual latest version supported by the hardware, as Godot may not always request the latest version. See also OS.get_video_adapter_driver_info().

Note: When running a headless or server binary, this function returns an empty string.

String get_video_adapter_name() const 🔗

Returns the name of the video adapter (e.g. "GeForce GTX 1080/PCIe/SSE2").

Note: When running a headless or server binary, this function returns an empty string.

Note: On the web platform, some browsers such as Firefox may report a different, fixed GPU name such as "GeForce GTX 980" (regardless of the user's actual GPU model). This is done to make fingerprinting more difficult.

DeviceType get_video_adapter_type() const 🔗

Returns the type of the video adapter. Since dedicated graphics cards from a given generation will usually be significantly faster than integrated graphics made in the same generation, the device type can be used as a basis for automatic graphics settings adjustment. However, this is not always true, so make sure to provide users with a way to manually override graphics settings.

Note: When using the OpenGL rendering driver or when running in headless mode, this function always returns RenderingDevice.DEVICE_TYPE_OTHER.

String get_video_adapter_vendor() const 🔗

Returns the vendor of the video adapter (e.g. "NVIDIA Corporation").

Note: When running a headless or server binary, this function returns an empty string.

RID get_white_texture() 🔗

Returns the ID of a 4×4 white texture (in Image.FORMAT_RGB8 format). This texture will be created and returned on the first call to get_white_texture(), then it will be cached for subsequent calls. See also get_test_texture().

Example: Get the white texture and apply it to a Sprite2D node:

void gi_set_use_half_resolution(half_resolution: bool) 🔗

If half_resolution is true, renders VoxelGI and SDFGI (Environment.sdfgi_enabled) buffers at halved resolution on each axis (e.g. 960×540 when the viewport size is 1920×1080). This improves performance significantly when VoxelGI or SDFGI is enabled, at the cost of artifacts that may be visible on polygon edges. The loss in quality becomes less noticeable as the viewport resolution increases. LightmapGI rendering is not affected by this setting. Equivalent to ProjectSettings.rendering/global_illumination/gi/use_half_resolution.

void global_shader_parameter_add(name: StringName, type: GlobalShaderParameterType, default_value: Variant) 🔗

Creates a new global shader uniform.

Note: Global shader parameter names are case-sensitive.

Variant global_shader_parameter_get(name: StringName) const 🔗

Returns the value of the global shader uniform specified by name.

Note: global_shader_parameter_get() has a large performance penalty as the rendering thread needs to synchronize with the calling thread, which is slow. Do not use this method during gameplay to avoid stuttering. If you need to read values in a script after setting them, consider creating an autoload where you store the values you need to query at the same time you're setting them as global parameters.

Array[StringName] global_shader_parameter_get_list() const 🔗

Returns the list of global shader uniform names.

Note: global_shader_parameter_get() has a large performance penalty as the rendering thread needs to synchronize with the calling thread, which is slow. Do not use this method during gameplay to avoid stuttering. If you need to read values in a script after setting them, consider creating an autoload where you store the values you need to query at the same time you're setting them as global parameters.

GlobalShaderParameterType global_shader_parameter_get_type(name: StringName) const 🔗

Returns the type associated to the global shader uniform specified by name.

Note: global_shader_parameter_get() has a large performance penalty as the rendering thread needs to synchronize with the calling thread, which is slow. Do not use this method during gameplay to avoid stuttering. If you need to read values in a script after setting them, consider creating an autoload where you store the values you need to query at the same time you're setting them as global parameters.

void global_shader_parameter_remove(name: StringName) 🔗

Removes the global shader uniform specified by name.

void global_shader_parameter_set(name: StringName, value: Variant) 🔗

Sets the global shader uniform name to value.

void global_shader_parameter_set_override(name: StringName, value: Variant) 🔗

Overrides the global shader uniform name with value. Equivalent to the ShaderGlobalsOverride node.

bool has_changed() const 🔗

Returns true if changes have been made to the RenderingServer's data. force_draw() is usually called if this happens.

bool has_feature(feature: Features) const 🔗

Deprecated: This method has not been used since Godot 3.0.

This method does nothing and always returns false.

bool has_os_feature(feature: String) const 🔗

Returns true if the OS supports a certain feature. Features might be s3tc, etc, and etc2.

void instance_attach_object_instance_id(instance: RID, id: int) 🔗

Attaches a unique Object ID to instance. Object ID must be attached to instance for proper culling with instances_cull_aabb(), instances_cull_convex(), and instances_cull_ray().

void instance_attach_skeleton(instance: RID, skeleton: RID) 🔗

Attaches a skeleton to an instance. Removes the previous skeleton from the instance.

RID instance_create() 🔗

Creates a visual instance and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all instance_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

An instance is a way of placing a 3D object in the scenario. Objects like particles, meshes, reflection probes and decals need to be associated with an instance to be visible in the scenario using instance_set_base().

Note: The equivalent node is VisualInstance3D.

RID instance_create2(base: RID, scenario: RID) 🔗

Creates a visual instance, adds it to the RenderingServer, and sets both base and scenario. It can be accessed with the RID that is returned. This RID will be used in all instance_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method. This is a shorthand for using instance_create() and setting the base and scenario manually.

Variant instance_geometry_get_shader_parameter(instance: RID, parameter: StringName) const 🔗

Returns the value of the per-instance shader uniform from the specified 3D geometry instance. Equivalent to GeometryInstance3D.get_instance_shader_parameter().

Note: Per-instance shader parameter names are case-sensitive.

Variant instance_geometry_get_shader_parameter_default_value(instance: RID, parameter: StringName) const 🔗

Returns the default value of the per-instance shader uniform from the specified 3D geometry instance. Equivalent to GeometryInstance3D.get_instance_shader_parameter().

Array[Dictionary] instance_geometry_get_shader_parameter_list(instance: RID) const 🔗

Returns a dictionary of per-instance shader uniform names of the per-instance shader uniform from the specified 3D geometry instance. The returned dictionary is in PropertyInfo format, with the keys name, class_name, type, hint, hint_string and usage. Equivalent to GeometryInstance3D.get_instance_shader_parameter().

void instance_geometry_set_cast_shadows_setting(instance: RID, shadow_casting_setting: ShadowCastingSetting) 🔗

Sets the shadow casting setting. Equivalent to GeometryInstance3D.cast_shadow.

void instance_geometry_set_flag(instance: RID, flag: InstanceFlags, enabled: bool) 🔗

Sets the flag for a given instance to enabled.

void instance_geometry_set_lightmap(instance: RID, lightmap: RID, lightmap_uv_scale: Rect2, lightmap_slice: int) 🔗

Sets the lightmap GI instance to use for the specified 3D geometry instance. The lightmap UV scale for the specified instance (equivalent to GeometryInstance3D.gi_lightmap_scale) and lightmap atlas slice must also be specified.

void instance_geometry_set_lod_bias(instance: RID, lod_bias: float) 🔗

Sets the level of detail bias to use when rendering the specified 3D geometry instance. Higher values result in higher detail from further away. Equivalent to GeometryInstance3D.lod_bias.

void instance_geometry_set_material_overlay(instance: RID, material: RID) 🔗

Sets a material that will be rendered for all surfaces on top of active materials for the mesh associated with this instance. Equivalent to GeometryInstance3D.material_overlay.

void instance_geometry_set_material_override(instance: RID, material: RID) 🔗

Sets a material that will override the material for all surfaces on the mesh associated with this instance. Equivalent to GeometryInstance3D.material_override.

void instance_geometry_set_shader_parameter(instance: RID, parameter: StringName, value: Variant) 🔗

Sets the per-instance shader uniform on the specified 3D geometry instance. Equivalent to GeometryInstance3D.set_instance_shader_parameter().

void instance_geometry_set_transparency(instance: RID, transparency: float) 🔗

Sets the transparency for the given geometry instance. Equivalent to GeometryInstance3D.transparency.

A transparency of 0.0 is fully opaque, while 1.0 is fully transparent. Values greater than 0.0 (exclusive) will force the geometry's materials to go through the transparent pipeline, which is slower to render and can exhibit rendering issues due to incorrect transparency sorting. However, unlike using a transparent material, setting transparency to a value greater than 0.0 (exclusive) will not disable shadow rendering.

In spatial shaders, 1.0 - transparency is set as the default value of the ALPHA built-in.

Note: transparency is clamped between 0.0 and 1.0, so this property cannot be used to make transparent materials more opaque than they originally are.

void instance_geometry_set_visibility_range(instance: RID, min: float, max: float, min_margin: float, max_margin: float, fade_mode: VisibilityRangeFadeMode) 🔗

Sets the visibility range values for the given geometry instance. Equivalent to GeometryInstance3D.visibility_range_begin and related properties.

void instance_set_base(instance: RID, base: RID) 🔗

Sets the base of the instance. A base can be any of the 3D objects that are created in the RenderingServer that can be displayed. For example, any of the light types, mesh, multimesh, particle system, reflection probe, decal, lightmap, voxel GI and visibility notifiers are all types that can be set as the base of an instance in order to be displayed in the scenario.

void instance_set_blend_shape_weight(instance: RID, shape: int, weight: float) 🔗

Sets the weight for a given blend shape associated with this instance.

void instance_set_custom_aabb(instance: RID, aabb: AABB) 🔗

Sets a custom AABB to use when culling objects from the view frustum. Equivalent to setting GeometryInstance3D.custom_aabb.

void instance_set_extra_visibility_margin(instance: RID, margin: float) 🔗

Sets a margin to increase the size of the AABB when culling objects from the view frustum. This allows you to avoid culling objects that fall outside the view frustum. Equivalent to GeometryInstance3D.extra_cull_margin.

void instance_set_ignore_culling(instance: RID, enabled: bool) 🔗

If true, ignores both frustum and occlusion culling on the specified 3D geometry instance. This is not the same as GeometryInstance3D.ignore_occlusion_culling, which only ignores occlusion culling and leaves frustum culling intact.

void instance_set_layer_mask(instance: RID, mask: int) 🔗

Sets the render layers that this instance will be drawn to. Equivalent to VisualInstance3D.layers.

void instance_set_pivot_data(instance: RID, sorting_offset: float, use_aabb_center: bool) 🔗

Sets the sorting offset and switches between using the bounding box or instance origin for depth sorting.

void instance_set_scenario(instance: RID, scenario: RID) 🔗

Sets the scenario that the instance is in. The scenario is the 3D world that the objects will be displayed in.

void instance_set_surface_override_material(instance: RID, surface: int, material: RID) 🔗

Sets the override material of a specific surface. Equivalent to MeshInstance3D.set_surface_override_material().

void instance_set_transform(instance: RID, transform: Transform3D) 🔗

Sets the world space transform of the instance. Equivalent to Node3D.global_transform.

void instance_set_visibility_parent(instance: RID, parent: RID) 🔗

Sets the visibility parent for the given instance. Equivalent to Node3D.visibility_parent.

void instance_set_visible(instance: RID, visible: bool) 🔗

Sets whether an instance is drawn or not. Equivalent to Node3D.visible.

void instance_teleport(instance: RID) 🔗

Resets motion vectors and other interpolated values. Use this after teleporting a mesh from one position to another to avoid ghosting artifacts.

PackedInt64Array instances_cull_aabb(aabb: AABB, scenario: RID = RID()) const 🔗

Returns an array of object IDs intersecting with the provided AABB. Only 3D nodes that inherit from VisualInstance3D are considered, such as MeshInstance3D or DirectionalLight3D. Use @GlobalScope.instance_from_id() to obtain the actual nodes. A scenario RID must be provided, which is available in the World3D you want to query. This forces an update for all resources queued to update.

Warning: This function is primarily intended for editor usage. For in-game use cases, prefer physics collision.

PackedInt64Array instances_cull_convex(convex: Array[Plane], scenario: RID = RID()) const 🔗

Returns an array of object IDs intersecting with the provided convex shape. Only 3D nodes that inherit from VisualInstance3D are considered, such as MeshInstance3D or DirectionalLight3D. Use @GlobalScope.instance_from_id() to obtain the actual nodes. A scenario RID must be provided, which is available in the World3D you want to query. This forces an update for all resources queued to update.

Warning: This function is primarily intended for editor usage. For in-game use cases, prefer physics collision.

PackedInt64Array instances_cull_ray(from: Vector3, to: Vector3, scenario: RID = RID()) const 🔗

Returns an array of object IDs intersecting with the provided 3D ray. Only 3D nodes that inherit from VisualInstance3D are considered, such as MeshInstance3D or DirectionalLight3D. Use @GlobalScope.instance_from_id() to obtain the actual nodes. A scenario RID must be provided, which is available in the World3D you want to query. This forces an update for all resources queued to update.

Warning: This function is primarily intended for editor usage. For in-game use cases, prefer physics collision.

bool is_on_render_thread() 🔗

Returns true if our code is currently executing on the rendering thread.

void light_directional_set_blend_splits(light: RID, enable: bool) 🔗

If true, this directional light will blend between shadow map splits resulting in a smoother transition between them. Equivalent to DirectionalLight3D.directional_shadow_blend_splits.

void light_directional_set_shadow_mode(light: RID, mode: LightDirectionalShadowMode) 🔗

Sets the shadow mode for this directional light. Equivalent to DirectionalLight3D.directional_shadow_mode.

void light_directional_set_sky_mode(light: RID, mode: LightDirectionalSkyMode) 🔗

If true, this light will not be used for anything except sky shaders. Use this for lights that impact your sky shader that you may want to hide from affecting the rest of the scene. For example, you may want to enable this when the sun in your sky shader falls below the horizon.

void light_omni_set_shadow_mode(light: RID, mode: LightOmniShadowMode) 🔗

Sets whether to use a dual paraboloid or a cubemap for the shadow map. Dual paraboloid is faster but may suffer from artifacts. Equivalent to OmniLight3D.omni_shadow_mode.

void light_projectors_set_filter(filter: LightProjectorFilter) 🔗

Sets the texture filter mode to use when rendering light projectors. This parameter is global and cannot be set on a per-light basis.

void light_set_bake_mode(light: RID, bake_mode: LightBakeMode) 🔗

Sets the bake mode to use for the specified 3D light. Equivalent to Light3D.light_bake_mode.

void light_set_color(light: RID, color: Color) 🔗

Sets the color of the light. Equivalent to Light3D.light_color.

void light_set_cull_mask(light: RID, mask: int) 🔗

Sets the cull mask for this 3D light. Lights only affect objects in the selected layers. Equivalent to Light3D.light_cull_mask.

void light_set_distance_fade(decal: RID, enabled: bool, begin: float, shadow: float, length: float) 🔗

Sets the distance fade for this 3D light. This acts as a form of level of detail (LOD) and can be used to improve performance. Equivalent to Light3D.distance_fade_enabled, Light3D.distance_fade_begin, Light3D.distance_fade_shadow, and Light3D.distance_fade_length.

void light_set_max_sdfgi_cascade(light: RID, cascade: int) 🔗

Sets the maximum SDFGI cascade in which the 3D light's indirect lighting is rendered. Higher values allow the light to be rendered in SDFGI further away from the camera.

void light_set_negative(light: RID, enable: bool) 🔗

If true, the 3D light will subtract light instead of adding light. Equivalent to Light3D.light_negative.

void light_set_param(light: RID, param: LightParam, value: float) 🔗

Sets the specified 3D light parameter. Equivalent to Light3D.set_param().

void light_set_projector(light: RID, texture: RID) 🔗

Sets the projector texture to use for the specified 3D light. Equivalent to Light3D.light_projector.

void light_set_reverse_cull_face_mode(light: RID, enabled: bool) 🔗

If true, reverses the backface culling of the mesh. This can be useful when you have a flat mesh that has a light behind it. If you need to cast a shadow on both sides of the mesh, set the mesh to use double-sided shadows with instance_geometry_set_cast_shadows_setting(). Equivalent to Light3D.shadow_reverse_cull_face.

void light_set_shadow(light: RID, enabled: bool) 🔗

If true, light will cast shadows. Equivalent to Light3D.shadow_enabled.

void light_set_shadow_caster_mask(light: RID, mask: int) 🔗

Sets the shadow caster mask for this 3D light. Shadows will only be cast using objects in the selected layers. Equivalent to Light3D.shadow_caster_mask.

RID lightmap_create() 🔗

Creates a new lightmap global illumination instance and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all lightmap_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent node is LightmapGI.

PackedInt32Array lightmap_get_probe_capture_bsp_tree(lightmap: RID) const 🔗

There is currently no description for this method. Please help us by contributing one!

PackedVector3Array lightmap_get_probe_capture_points(lightmap: RID) const 🔗

There is currently no description for this method. Please help us by contributing one!

PackedColorArray lightmap_get_probe_capture_sh(lightmap: RID) const 🔗

There is currently no description for this method. Please help us by contributing one!

PackedInt32Array lightmap_get_probe_capture_tetrahedra(lightmap: RID) const 🔗

There is currently no description for this method. Please help us by contributing one!

void lightmap_set_baked_exposure_normalization(lightmap: RID, baked_exposure: float) 🔗

Used to inform the renderer what exposure normalization value was used while baking the lightmap. This value will be used and modulated at run time to ensure that the lightmap maintains a consistent level of exposure even if the scene-wide exposure normalization is changed at run time. For more information see camera_attributes_set_exposure().

void lightmap_set_probe_bounds(lightmap: RID, bounds: AABB) 🔗

There is currently no description for this method. Please help us by contributing one!

void lightmap_set_probe_capture_data(lightmap: RID, points: PackedVector3Array, point_sh: PackedColorArray, tetrahedra: PackedInt32Array, bsp_tree: PackedInt32Array) 🔗

There is currently no description for this method. Please help us by contributing one!

void lightmap_set_probe_capture_update_speed(speed: float) 🔗

There is currently no description for this method. Please help us by contributing one!

void lightmap_set_probe_interior(lightmap: RID, interior: bool) 🔗

There is currently no description for this method. Please help us by contributing one!

void lightmap_set_textures(lightmap: RID, light: RID, uses_sh: bool) 🔗

Set the textures on the given lightmap GI instance to the texture array pointed to by the light RID. If the lightmap texture was baked with LightmapGI.directional set to true, then uses_sh must also be true.

void lightmaps_set_bicubic_filter(enable: bool) 🔗

Toggles whether a bicubic filter should be used when lightmaps are sampled. This smoothens their appearance at a performance cost.

RID make_sphere_mesh(latitudes: int, longitudes: int, radius: float) 🔗

Returns a mesh of a sphere with the given number of horizontal subdivisions, vertical subdivisions and radius. See also get_test_cube().

RID material_create() 🔗

Creates an empty material and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all material_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent resource is Material.

Variant material_get_param(material: RID, parameter: StringName) const 🔗

Returns the value of a certain material's parameter.

void material_set_next_pass(material: RID, next_material: RID) 🔗

Sets an object's next material.

void material_set_param(material: RID, parameter: StringName, value: Variant) 🔗

Sets a material's parameter.

void material_set_render_priority(material: RID, priority: int) 🔗

Sets a material's render priority.

void material_set_shader(shader_material: RID, shader: RID) 🔗

Sets a shader material's shader.

void mesh_add_surface(mesh: RID, surface: Dictionary) 🔗

There is currently no description for this method. Please help us by contributing one!

void mesh_add_surface_from_arrays(mesh: RID, primitive: PrimitiveType, arrays: Array, blend_shapes: Array = [], lods: Dictionary = {}, compress_format: BitField[ArrayFormat] = 0) 🔗

There is currently no description for this method. Please help us by contributing one!

void mesh_clear(mesh: RID) 🔗

Removes all surfaces from a mesh.

Creates a new mesh and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all mesh_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

To place in a scene, attach this mesh to an instance using instance_set_base() using the returned RID.

Note: The equivalent resource is Mesh.

RID mesh_create_from_surfaces(surfaces: Array[Dictionary], blend_shape_count: int = 0) 🔗

There is currently no description for this method. Please help us by contributing one!

int mesh_get_blend_shape_count(mesh: RID) const 🔗

Returns a mesh's blend shape count.

BlendShapeMode mesh_get_blend_shape_mode(mesh: RID) const 🔗

Returns a mesh's blend shape mode.

AABB mesh_get_custom_aabb(mesh: RID) const 🔗

Returns a mesh's custom aabb.

Dictionary mesh_get_surface(mesh: RID, surface: int) 🔗

There is currently no description for this method. Please help us by contributing one!

int mesh_get_surface_count(mesh: RID) const 🔗

Returns a mesh's number of surfaces.

void mesh_set_blend_shape_mode(mesh: RID, mode: BlendShapeMode) 🔗

Sets a mesh's blend shape mode.

void mesh_set_custom_aabb(mesh: RID, aabb: AABB) 🔗

Sets a mesh's custom aabb.

void mesh_set_shadow_mesh(mesh: RID, shadow_mesh: RID) 🔗

There is currently no description for this method. Please help us by contributing one!

Array mesh_surface_get_arrays(mesh: RID, surface: int) const 🔗

Returns a mesh's surface's buffer arrays.

Array[Array] mesh_surface_get_blend_shape_arrays(mesh: RID, surface: int) const 🔗

Returns a mesh's surface's arrays for blend shapes.

int mesh_surface_get_format_attribute_stride(format: BitField[ArrayFormat], vertex_count: int) const 🔗

Returns the stride of the attribute buffer for a mesh with given format.

int mesh_surface_get_format_index_stride(format: BitField[ArrayFormat], vertex_count: int) const 🔗

Returns the stride of the index buffer for a mesh with the given format.

int mesh_surface_get_format_normal_tangent_stride(format: BitField[ArrayFormat], vertex_count: int) const 🔗

Returns the stride of the combined normals and tangents for a mesh with given format. Note importantly that, while normals and tangents are in the vertex buffer with vertices, they are only interleaved with each other and so have a different stride than vertex positions.

int mesh_surface_get_format_offset(format: BitField[ArrayFormat], vertex_count: int, array_index: int) const 🔗

Returns the offset of a given attribute by array_index in the start of its respective buffer.

int mesh_surface_get_format_skin_stride(format: BitField[ArrayFormat], vertex_count: int) const 🔗

Returns the stride of the skin buffer for a mesh with given format.

int mesh_surface_get_format_vertex_stride(format: BitField[ArrayFormat], vertex_count: int) const 🔗

Returns the stride of the vertex positions for a mesh with given format. Note importantly that vertex positions are stored consecutively and are not interleaved with the other attributes in the vertex buffer (normals and tangents).

RID mesh_surface_get_material(mesh: RID, surface: int) const 🔗

Returns a mesh's surface's material.

void mesh_surface_remove(mesh: RID, surface: int) 🔗

Removes the surface at the given index from the Mesh, shifting surfaces with higher index down by one.

void mesh_surface_set_material(mesh: RID, surface: int, material: RID) 🔗

Sets a mesh's surface's material.

void mesh_surface_update_attribute_region(mesh: RID, surface: int, offset: int, data: PackedByteArray) 🔗

There is currently no description for this method. Please help us by contributing one!

void mesh_surface_update_index_region(mesh: RID, surface: int, offset: int, data: PackedByteArray) 🔗

Updates the index buffer of the mesh surface with the given data. The expected data are 16 or 32-bit unsigned integers, which can be determined with mesh_surface_get_format_index_stride().

void mesh_surface_update_skin_region(mesh: RID, surface: int, offset: int, data: PackedByteArray) 🔗

There is currently no description for this method. Please help us by contributing one!

void mesh_surface_update_vertex_region(mesh: RID, surface: int, offset: int, data: PackedByteArray) 🔗

There is currently no description for this method. Please help us by contributing one!

void multimesh_allocate_data(multimesh: RID, instances: int, transform_format: MultimeshTransformFormat, color_format: bool = false, custom_data_format: bool = false, use_indirect: bool = false) 🔗

There is currently no description for this method. Please help us by contributing one!

RID multimesh_create() 🔗

Creates a new multimesh on the RenderingServer and returns an RID handle. This RID will be used in all multimesh_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

To place in a scene, attach this multimesh to an instance using instance_set_base() using the returned RID.

Note: The equivalent resource is MultiMesh.

AABB multimesh_get_aabb(multimesh: RID) const 🔗

Calculates and returns the axis-aligned bounding box that encloses all instances within the multimesh.

PackedFloat32Array multimesh_get_buffer(multimesh: RID) const 🔗

Returns the MultiMesh data (such as instance transforms, colors, etc.). See multimesh_set_buffer() for details on the returned data.

Note: If the buffer is in the engine's internal cache, it will have to be fetched from GPU memory and possibly decompressed. This means multimesh_get_buffer() is potentially a slow operation and should be avoided whenever possible.

RID multimesh_get_buffer_rd_rid(multimesh: RID) const 🔗

Returns the RenderingDevice RID handle of the MultiMesh, which can be used as any other buffer on the Rendering Device.

RID multimesh_get_command_buffer_rd_rid(multimesh: RID) const 🔗

Returns the RenderingDevice RID handle of the MultiMesh command buffer. This RID is only valid if use_indirect is set to true when allocating data through multimesh_allocate_data(). It can be used to directly modify the instance count via buffer.

The data structure is dependent on both how many surfaces the mesh contains and whether it is indexed or not, the buffer has 5 integers in it, with the last unused if the mesh is not indexed.

Each of the values in the buffer correspond to these options:

AABB multimesh_get_custom_aabb(multimesh: RID) const 🔗

Returns the custom AABB defined for this MultiMesh resource.

int multimesh_get_instance_count(multimesh: RID) const 🔗

Returns the number of instances allocated for this multimesh.

RID multimesh_get_mesh(multimesh: RID) const 🔗

Returns the RID of the mesh that will be used in drawing this multimesh.

int multimesh_get_visible_instances(multimesh: RID) const 🔗

Returns the number of visible instances for this multimesh.

Color multimesh_instance_get_color(multimesh: RID, index: int) const 🔗

Returns the color by which the specified instance will be modulated.

Color multimesh_instance_get_custom_data(multimesh: RID, index: int) const 🔗

Returns the custom data associated with the specified instance.

Transform3D multimesh_instance_get_transform(multimesh: RID, index: int) const 🔗

Returns the Transform3D of the specified instance.

Transform2D multimesh_instance_get_transform_2d(multimesh: RID, index: int) const 🔗

Returns the Transform2D of the specified instance. For use when the multimesh is set to use 2D transforms.

void multimesh_instance_reset_physics_interpolation(multimesh: RID, index: int) 🔗

Prevents physics interpolation for the specified instance during the current physics tick.

This is useful when moving an instance to a new location, to give an instantaneous change rather than interpolation from the previous location.

void multimesh_instance_set_color(multimesh: RID, index: int, color: Color) 🔗

Sets the color by which this instance will be modulated. Equivalent to MultiMesh.set_instance_color().

void multimesh_instance_set_custom_data(multimesh: RID, index: int, custom_data: Color) 🔗

Sets the custom data for this instance. Custom data is passed as a Color, but is interpreted as a vec4 in the shader. Equivalent to MultiMesh.set_instance_custom_data().

void multimesh_instance_set_transform(multimesh: RID, index: int, transform: Transform3D) 🔗

Sets the Transform3D for this instance. Equivalent to MultiMesh.set_instance_transform().

void multimesh_instance_set_transform_2d(multimesh: RID, index: int, transform: Transform2D) 🔗

Sets the Transform2D for this instance. For use when multimesh is used in 2D. Equivalent to MultiMesh.set_instance_transform_2d().

void multimesh_set_buffer(multimesh: RID, buffer: PackedFloat32Array) 🔗

Set the entire data to use for drawing the multimesh at once to buffer (such as instance transforms and colors). buffer's size must match the number of instances multiplied by the per-instance data size (which depends on the enabled MultiMesh fields). Otherwise, an error message is printed and nothing is rendered. See also multimesh_get_buffer().

The per-instance data size and expected data order is:

Instance transforms are in row-major order. Specifically:

For Transform2D the float-order is: (x.x, y.x, padding_float, origin.x, x.y, y.y, padding_float, origin.y).

For Transform3D the float-order is: (basis.x.x, basis.y.x, basis.z.x, origin.x, basis.x.y, basis.y.y, basis.z.y, origin.y, basis.x.z, basis.y.z, basis.z.z, origin.z).

void multimesh_set_buffer_interpolated(multimesh: RID, buffer: PackedFloat32Array, buffer_previous: PackedFloat32Array) 🔗

Alternative version of multimesh_set_buffer() for use with physics interpolation.

Takes both an array of current data and an array of data for the previous physics tick.

void multimesh_set_custom_aabb(multimesh: RID, aabb: AABB) 🔗

Sets the custom AABB for this MultiMesh resource.

void multimesh_set_mesh(multimesh: RID, mesh: RID) 🔗

Sets the mesh to be drawn by the multimesh. Equivalent to MultiMesh.mesh.

void multimesh_set_physics_interpolated(multimesh: RID, interpolated: bool) 🔗

Turns on and off physics interpolation for this MultiMesh resource.

void multimesh_set_physics_interpolation_quality(multimesh: RID, quality: MultimeshPhysicsInterpolationQuality) 🔗

Sets the physics interpolation quality for the MultiMesh.

A value of MULTIMESH_INTERP_QUALITY_FAST gives fast but low quality interpolation, a value of MULTIMESH_INTERP_QUALITY_HIGH gives slower but higher quality interpolation.

void multimesh_set_visible_instances(multimesh: RID, visible: int) 🔗

Sets the number of instances visible at a given time. If -1, all instances that have been allocated are drawn. Equivalent to MultiMesh.visible_instance_count.

RID occluder_create() 🔗

Creates an occluder instance and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all occluder_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent resource is Occluder3D (not to be confused with the OccluderInstance3D node).

void occluder_set_mesh(occluder: RID, vertices: PackedVector3Array, indices: PackedInt32Array) 🔗

Sets the mesh data for the given occluder RID, which controls the shape of the occlusion culling that will be performed.

RID omni_light_create() 🔗

Creates a new omni light and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID can be used in most light_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

To place in a scene, attach this omni light to an instance using instance_set_base() using the returned RID.

Note: The equivalent node is OmniLight3D.

RID particles_collision_create() 🔗

Creates a new 3D GPU particle collision or attractor and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID can be used in most particles_collision_* RenderingServer functions.

Note: The equivalent nodes are GPUParticlesCollision3D and GPUParticlesAttractor3D.

void particles_collision_height_field_update(particles_collision: RID) 🔗

Requests an update for the 3D GPU particle collision heightfield. This may be automatically called by the 3D GPU particle collision heightfield depending on its GPUParticlesCollisionHeightField3D.update_mode.

void particles_collision_set_attractor_attenuation(particles_collision: RID, curve: float) 🔗

Sets the attenuation curve for the 3D GPU particles attractor specified by the particles_collision RID. Only used for attractors, not colliders. Equivalent to GPUParticlesAttractor3D.attenuation.

void particles_collision_set_attractor_directionality(particles_collision: RID, amount: float) 🔗

Sets the directionality amount for the 3D GPU particles attractor specified by the particles_collision RID. Only used for attractors, not colliders. Equivalent to GPUParticlesAttractor3D.directionality.

void particles_collision_set_attractor_strength(particles_collision: RID, strength: float) 🔗

Sets the strength for the 3D GPU particles attractor specified by the particles_collision RID. Only used for attractors, not colliders. Equivalent to GPUParticlesAttractor3D.strength.

void particles_collision_set_box_extents(particles_collision: RID, extents: Vector3) 🔗

Sets the extents for the 3D GPU particles collision by the particles_collision RID. Equivalent to GPUParticlesCollisionBox3D.size, GPUParticlesCollisionSDF3D.size, GPUParticlesCollisionHeightField3D.size, GPUParticlesAttractorBox3D.size or GPUParticlesAttractorVectorField3D.size depending on the particles_collision type.

void particles_collision_set_collision_type(particles_collision: RID, type: ParticlesCollisionType) 🔗

Sets the collision or attractor shape type for the 3D GPU particles collision or attractor specified by the particles_collision RID.

void particles_collision_set_cull_mask(particles_collision: RID, mask: int) 🔗

Sets the cull mask for the 3D GPU particles collision or attractor specified by the particles_collision RID. Equivalent to GPUParticlesCollision3D.cull_mask or GPUParticlesAttractor3D.cull_mask depending on the particles_collision type.

void particles_collision_set_field_texture(particles_collision: RID, texture: RID) 🔗

Sets the signed distance field texture for the 3D GPU particles collision specified by the particles_collision RID. Equivalent to GPUParticlesCollisionSDF3D.texture or GPUParticlesAttractorVectorField3D.texture depending on the particles_collision type.

void particles_collision_set_height_field_mask(particles_collision: RID, mask: int) 🔗

Sets the heightfield mask for the 3D GPU particles heightfield collision specified by the particles_collision RID. Equivalent to GPUParticlesCollisionHeightField3D.heightfield_mask.

void particles_collision_set_height_field_resolution(particles_collision: RID, resolution: ParticlesCollisionHeightfieldResolution) 🔗

Sets the heightmap resolution for the 3D GPU particles heightfield collision specified by the particles_collision RID. Equivalent to GPUParticlesCollisionHeightField3D.resolution.

void particles_collision_set_sphere_radius(particles_collision: RID, radius: float) 🔗

Sets the radius for the 3D GPU particles sphere collision or attractor specified by the particles_collision RID. Equivalent to GPUParticlesCollisionSphere3D.radius or GPUParticlesAttractorSphere3D.radius depending on the particles_collision type.

RID particles_create() 🔗

Creates a GPU-based particle system and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all particles_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

To place in a scene, attach these particles to an instance using instance_set_base() using the returned RID.

Note: The equivalent nodes are GPUParticles2D and GPUParticles3D.

Note: All particles_* methods only apply to GPU-based particles, not CPU-based particles. CPUParticles2D and CPUParticles3D do not have equivalent RenderingServer functions available, as these use MultiMeshInstance2D and MultiMeshInstance3D under the hood (see multimesh_* methods).

void particles_emit(particles: RID, transform: Transform3D, velocity: Vector3, color: Color, custom: Color, emit_flags: int) 🔗

Manually emits particles from the particles instance.

AABB particles_get_current_aabb(particles: RID) 🔗

Calculates and returns the axis-aligned bounding box that contains all the particles. Equivalent to GPUParticles3D.capture_aabb().

bool particles_get_emitting(particles: RID) 🔗

Returns true if particles are currently set to emitting.

bool particles_is_inactive(particles: RID) 🔗

Returns true if particles are not emitting and particles are set to inactive.

void particles_request_process(particles: RID) 🔗

Add particle system to list of particle systems that need to be updated. Update will take place on the next frame, or on the next call to instances_cull_aabb(), instances_cull_convex(), or instances_cull_ray().

void particles_request_process_time(particles: RID, time: float) 🔗

Requests particles to process for extra process time during a single frame.

void particles_restart(particles: RID) 🔗

Reset the particles on the next update. Equivalent to GPUParticles3D.restart().

void particles_set_amount(particles: RID, amount: int) 🔗

Sets the number of particles to be drawn and allocates the memory for them. Equivalent to GPUParticles3D.amount.

void particles_set_amount_ratio(particles: RID, ratio: float) 🔗

Sets the amount ratio for particles to be emitted. Equivalent to GPUParticles3D.amount_ratio.

void particles_set_collision_base_size(particles: RID, size: float) 🔗

There is currently no description for this method. Please help us by contributing one!

void particles_set_custom_aabb(particles: RID, aabb: AABB) 🔗

Sets a custom axis-aligned bounding box for the particle system. Equivalent to GPUParticles3D.visibility_aabb.

void particles_set_draw_order(particles: RID, order: ParticlesDrawOrder) 🔗

Sets the draw order of the particles. Equivalent to GPUParticles3D.draw_order.

void particles_set_draw_pass_mesh(particles: RID, pass: int, mesh: RID) 🔗

Sets the mesh to be used for the specified draw pass. Equivalent to GPUParticles3D.draw_pass_1, GPUParticles3D.draw_pass_2, GPUParticles3D.draw_pass_3, and GPUParticles3D.draw_pass_4.

void particles_set_draw_passes(particles: RID, count: int) 🔗

Sets the number of draw passes to use. Equivalent to GPUParticles3D.draw_passes.

void particles_set_emission_transform(particles: RID, transform: Transform3D) 🔗

Sets the Transform3D that will be used by the particles when they first emit.

void particles_set_emitter_velocity(particles: RID, velocity: Vector3) 🔗

Sets the velocity of a particle node, that will be used by ParticleProcessMaterial.inherit_velocity_ratio.

void particles_set_emitting(particles: RID, emitting: bool) 🔗

If true, particles will emit over time. Setting to false does not reset the particles, but only stops their emission. Equivalent to GPUParticles3D.emitting.

void particles_set_explosiveness_ratio(particles: RID, ratio: float) 🔗

Sets the explosiveness ratio. Equivalent to GPUParticles3D.explosiveness.

void particles_set_fixed_fps(particles: RID, fps: int) 🔗

Sets the frame rate that the particle system rendering will be fixed to. Equivalent to GPUParticles3D.fixed_fps.

void particles_set_fractional_delta(particles: RID, enable: bool) 🔗

If true, uses fractional delta which smooths the movement of the particles. Equivalent to GPUParticles3D.fract_delta.

void particles_set_interp_to_end(particles: RID, factor: float) 🔗

Sets the value that informs a ParticleProcessMaterial to rush all particles towards the end of their lifetime.

void particles_set_interpolate(particles: RID, enable: bool) 🔗

There is currently no description for this method. Please help us by contributing one!

void particles_set_lifetime(particles: RID, lifetime: float) 🔗

Sets the lifetime of each particle in the system. Equivalent to GPUParticles3D.lifetime.

void particles_set_mode(particles: RID, mode: ParticlesMode) 🔗

Sets whether the GPU particles specified by the particles RID should be rendered in 2D or 3D according to mode.

void particles_set_one_shot(particles: RID, one_shot: bool) 🔗

If true, particles will emit once and then stop. Equivalent to GPUParticles3D.one_shot.

void particles_set_pre_process_time(particles: RID, time: float) 🔗

Sets the preprocess time for the particles' animation. This lets you delay starting an animation until after the particles have begun emitting. Equivalent to GPUParticles3D.preprocess.

void particles_set_process_material(particles: RID, material: RID) 🔗

Sets the material for processing the particles.

Note: This is not the material used to draw the materials. Equivalent to GPUParticles3D.process_material.

void particles_set_randomness_ratio(particles: RID, ratio: float) 🔗

Sets the emission randomness ratio. This randomizes the emission of particles within their phase. Equivalent to GPUParticles3D.randomness.

void particles_set_speed_scale(particles: RID, scale: float) 🔗

Sets the speed scale of the particle system. Equivalent to GPUParticles3D.speed_scale.

void particles_set_subemitter(particles: RID, subemitter_particles: RID) 🔗

There is currently no description for this method. Please help us by contributing one!

void particles_set_trail_bind_poses(particles: RID, bind_poses: Array[Transform3D]) 🔗

There is currently no description for this method. Please help us by contributing one!

void particles_set_trails(particles: RID, enable: bool, length_sec: float) 🔗

If enable is true, enables trails for the particles with the specified length_sec in seconds. Equivalent to GPUParticles3D.trail_enabled and GPUParticles3D.trail_lifetime.

void particles_set_transform_align(particles: RID, align: ParticlesTransformAlign) 🔗

There is currently no description for this method. Please help us by contributing one!

void particles_set_use_local_coordinates(particles: RID, enable: bool) 🔗

If true, particles use local coordinates. If false they use global coordinates. Equivalent to GPUParticles3D.local_coords.

void positional_soft_shadow_filter_set_quality(quality: ShadowQuality) 🔗

Sets the filter quality for omni and spot light shadows in 3D. See also ProjectSettings.rendering/lights_and_shadows/positional_shadow/soft_shadow_filter_quality. This parameter is global and cannot be set on a per-viewport basis.

RID reflection_probe_create() 🔗

Creates a reflection probe and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all reflection_probe_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

To place in a scene, attach this reflection probe to an instance using instance_set_base() using the returned RID.

Note: The equivalent node is ReflectionProbe.

void reflection_probe_set_ambient_color(probe: RID, color: Color) 🔗

Sets the reflection probe's custom ambient light color. Equivalent to ReflectionProbe.ambient_color.

void reflection_probe_set_ambient_energy(probe: RID, energy: float) 🔗

Sets the reflection probe's custom ambient light energy. Equivalent to ReflectionProbe.ambient_color_energy.

void reflection_probe_set_ambient_mode(probe: RID, mode: ReflectionProbeAmbientMode) 🔗

Sets the reflection probe's ambient light mode. Equivalent to ReflectionProbe.ambient_mode.

void reflection_probe_set_as_interior(probe: RID, enable: bool) 🔗

If true, reflections will ignore sky contribution. Equivalent to ReflectionProbe.interior.

void reflection_probe_set_blend_distance(probe: RID, blend_distance: float) 🔗

Sets the distance in meters over which a probe blends into the scene.

void reflection_probe_set_cull_mask(probe: RID, layers: int) 🔗

Sets the render cull mask for this reflection probe. Only instances with a matching layer will be reflected by this probe. Equivalent to ReflectionProbe.cull_mask.

void reflection_probe_set_enable_box_projection(probe: RID, enable: bool) 🔗

If true, uses box projection. This can make reflections look more correct in certain situations. Equivalent to ReflectionProbe.box_projection.

void reflection_probe_set_enable_shadows(probe: RID, enable: bool) 🔗

If true, computes shadows in the reflection probe. This makes the reflection much slower to compute. Equivalent to ReflectionProbe.enable_shadows.

void reflection_probe_set_intensity(probe: RID, intensity: float) 🔗

Sets the intensity of the reflection probe. Intensity modulates the strength of the reflection. Equivalent to ReflectionProbe.intensity.

void reflection_probe_set_max_distance(probe: RID, distance: float) 🔗

Sets the max distance away from the probe an object can be before it is culled. Equivalent to ReflectionProbe.max_distance.

void reflection_probe_set_mesh_lod_threshold(probe: RID, pixels: float) 🔗

Sets the mesh level of detail to use in the reflection probe rendering. Higher values will use less detailed versions of meshes that have LOD variations generated, which can improve performance. Equivalent to ReflectionProbe.mesh_lod_threshold.

void reflection_probe_set_origin_offset(probe: RID, offset: Vector3) 🔗

Sets the origin offset to be used when this reflection probe is in box project mode. Equivalent to ReflectionProbe.origin_offset.

void reflection_probe_set_reflection_mask(probe: RID, layers: int) 🔗

Sets the render reflection mask for this reflection probe. Only instances with a matching layer will have reflections applied from this probe. Equivalent to ReflectionProbe.reflection_mask.

void reflection_probe_set_resolution(probe: RID, resolution: int) 🔗

Sets the resolution to use when rendering the specified reflection probe. The resolution is specified for each cubemap face: for instance, specifying 512 will allocate 6 faces of 512×512 each (plus mipmaps for roughness levels).

void reflection_probe_set_size(probe: RID, size: Vector3) 🔗

Sets the size of the area that the reflection probe will capture. Equivalent to ReflectionProbe.size.

void reflection_probe_set_update_mode(probe: RID, mode: ReflectionProbeUpdateMode) 🔗

Sets how often the reflection probe updates. Can either be once or every frame.

void request_frame_drawn_callback(callable: Callable) 🔗

Schedules a callback to the given callable after a frame has been drawn.

RID scenario_create() 🔗

Creates a scenario and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all scenario_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

The scenario is the 3D world that all the visual instances exist in.

void scenario_set_camera_attributes(scenario: RID, effects: RID) 🔗

Sets the camera attributes (effects) that will be used with this scenario. See also CameraAttributes.

void scenario_set_compositor(scenario: RID, compositor: RID) 🔗

Sets the compositor (compositor) that will be used with this scenario. See also Compositor.

void scenario_set_environment(scenario: RID, environment: RID) 🔗

Sets the environment that will be used with this scenario. See also Environment.

void scenario_set_fallback_environment(scenario: RID, environment: RID) 🔗

Sets the fallback environment to be used by this scenario. The fallback environment is used if no environment is set. Internally, this is used by the editor to provide a default environment.

void screen_space_roughness_limiter_set_active(enable: bool, amount: float, limit: float) 🔗

Sets the screen-space roughness limiter parameters, such as whether it should be enabled and its thresholds. Equivalent to ProjectSettings.rendering/anti_aliasing/screen_space_roughness_limiter/enabled, ProjectSettings.rendering/anti_aliasing/screen_space_roughness_limiter/amount and ProjectSettings.rendering/anti_aliasing/screen_space_roughness_limiter/limit.

void set_boot_image(image: Image, color: Color, scale: bool, use_filter: bool = true) 🔗

Sets a boot image. The color defines the background color. If scale is true, the image will be scaled to fit the screen size. If use_filter is true, the image will be scaled with linear interpolation. If use_filter is false, the image will be scaled with nearest-neighbor interpolation.

void set_debug_generate_wireframes(generate: bool) 🔗

If generate is true, generates debug wireframes for all meshes that are loaded when using the Compatibility renderer. By default, the engine does not generate debug wireframes at runtime, since they slow down loading of assets and take up VRAM.

Note: You must call this method before loading any meshes when using the Compatibility renderer, otherwise wireframes will not be used.

void set_default_clear_color(color: Color) 🔗

Sets the default clear color which is used when a specific clear color has not been selected. See also get_default_clear_color().

RID shader_create() 🔗

Creates an empty shader and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all shader_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent resource is Shader.

String shader_get_code(shader: RID) const 🔗

Returns a shader's source code as a string.

RID shader_get_default_texture_parameter(shader: RID, name: StringName, index: int = 0) const 🔗

Returns a default texture from a shader searched by name.

Note: If the sampler array is used use index to access the specified texture.

Variant shader_get_parameter_default(shader: RID, name: StringName) const 🔗

Returns the default value for the specified shader uniform. This is usually the value written in the shader source code.

void shader_set_code(shader: RID, code: String) 🔗

Sets the shader's source code (which triggers recompilation after being changed).

void shader_set_default_texture_parameter(shader: RID, name: StringName, texture: RID, index: int = 0) 🔗

Sets a shader's default texture. Overwrites the texture given by name.

Note: If the sampler array is used use index to access the specified texture.

void shader_set_path_hint(shader: RID, path: String) 🔗

Sets the path hint for the specified shader. This should generally match the Shader resource's Resource.resource_path.

void skeleton_allocate_data(skeleton: RID, bones: int, is_2d_skeleton: bool = false) 🔗

There is currently no description for this method. Please help us by contributing one!

Transform3D skeleton_bone_get_transform(skeleton: RID, bone: int) const 🔗

Returns the Transform3D set for a specific bone of this skeleton.

Transform2D skeleton_bone_get_transform_2d(skeleton: RID, bone: int) const 🔗

Returns the Transform2D set for a specific bone of this skeleton.

void skeleton_bone_set_transform(skeleton: RID, bone: int, transform: Transform3D) 🔗

Sets the Transform3D for a specific bone of this skeleton.

void skeleton_bone_set_transform_2d(skeleton: RID, bone: int, transform: Transform2D) 🔗

Sets the Transform2D for a specific bone of this skeleton.

RID skeleton_create() 🔗

Creates a skeleton and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all skeleton_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

int skeleton_get_bone_count(skeleton: RID) const 🔗

Returns the number of bones allocated for this skeleton.

void skeleton_set_base_transform_2d(skeleton: RID, base_transform: Transform2D) 🔗

There is currently no description for this method. Please help us by contributing one!

Image sky_bake_panorama(sky: RID, energy: float, bake_irradiance: bool, size: Vector2i) 🔗

Generates and returns an Image containing the radiance map for the specified sky RID. This supports built-in sky material and custom sky shaders. If bake_irradiance is true, the irradiance map is saved instead of the radiance map. The radiance map is used to render reflected light, while the irradiance map is used to render ambient light. See also environment_bake_panorama().

Note: The image is saved in linear color space without any tonemapping performed, which means it will look too dark if viewed directly in an image editor. energy values above 1.0 can be used to brighten the resulting image.

Note: size should be a 2:1 aspect ratio for the generated panorama to have square pixels. For radiance maps, there is no point in using a height greater than Sky.radiance_size, as it won't increase detail. Irradiance maps only contain low-frequency data, so there is usually no point in going past a size of 128×64 pixels when saving an irradiance map.

Creates an empty sky and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all sky_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

void sky_set_material(sky: RID, material: RID) 🔗

Sets the material that the sky uses to render the background, ambient and reflection maps.

void sky_set_mode(sky: RID, mode: SkyMode) 🔗

Sets the process mode of the sky specified by the sky RID. Equivalent to Sky.process_mode.

void sky_set_radiance_size(sky: RID, radiance_size: int) 🔗

Sets the radiance_size of the sky specified by the sky RID (in pixels). Equivalent to Sky.radiance_size.

RID spot_light_create() 🔗

Creates a spot light and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID can be used in most light_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

To place in a scene, attach this spot light to an instance using instance_set_base() using the returned RID.

void sub_surface_scattering_set_quality(quality: SubSurfaceScatteringQuality) 🔗

Sets ProjectSettings.rendering/environment/subsurface_scattering/subsurface_scattering_quality to use when rendering materials that have subsurface scattering enabled.

void sub_surface_scattering_set_scale(scale: float, depth_scale: float) 🔗

Sets the ProjectSettings.rendering/environment/subsurface_scattering/subsurface_scattering_scale and ProjectSettings.rendering/environment/subsurface_scattering/subsurface_scattering_depth_scale to use when rendering materials that have subsurface scattering enabled.

RID texture_2d_create(image: Image) 🔗

Creates a 2-dimensional texture and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all texture_2d_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent resource is Texture2D.

Note: Not to be confused with RenderingDevice.texture_create(), which creates the graphics API's own texture type as opposed to the Godot-specific Texture2D resource.

Image texture_2d_get(texture: RID) const 🔗

Returns an Image instance from the given texture RID.

Example: Get the test texture from get_test_texture() and apply it to a Sprite2D node:

Image texture_2d_layer_get(texture: RID, layer: int) const 🔗

Returns an Image instance from the given texture RID and layer.

RID texture_2d_layered_create(layers: Array[Image], layered_type: TextureLayeredType) 🔗

Creates a 2-dimensional layered texture and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all texture_2d_layered_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent resource is TextureLayered.

RID texture_2d_layered_placeholder_create(layered_type: TextureLayeredType) 🔗

Creates a placeholder for a 2-dimensional layered texture and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all texture_2d_layered_* RenderingServer functions, although it does nothing when used. See also texture_2d_placeholder_create().

Note: The equivalent resource is PlaceholderTextureLayered.

RID texture_2d_placeholder_create() 🔗

Creates a placeholder for a 2-dimensional layered texture and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all texture_2d_layered_* RenderingServer functions, although it does nothing when used. See also texture_2d_layered_placeholder_create().

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent resource is PlaceholderTexture2D.

void texture_2d_update(texture: RID, image: Image, layer: int) 🔗

Updates the texture specified by the texture RID with the data in image. A layer must also be specified, which should be 0 when updating a single-layer texture (Texture2D).

Note: The image must have the same width, height and format as the current texture data. Otherwise, an error will be printed and the original texture won't be modified. If you need to use different width, height or format, use texture_replace() instead.

RID texture_3d_create(format: Format, width: int, height: int, depth: int, mipmaps: bool, data: Array[Image]) 🔗

Note: The equivalent resource is Texture3D.

Array[Image] texture_3d_get(texture: RID) const 🔗

Returns 3D texture data as an array of Images for the specified texture RID.

RID texture_3d_placeholder_create() 🔗

Creates a placeholder for a 3-dimensional texture and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all texture_3d_* RenderingServer functions, although it does nothing when used.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent resource is PlaceholderTexture3D.

void texture_3d_update(texture: RID, data: Array[Image]) 🔗

Updates the texture specified by the texture RID's data with the data in data. All the texture's layers must be replaced at once.

Note: The texture must have the same width, height, depth and format as the current texture data. Otherwise, an error will be printed and the original texture won't be modified. If you need to use different width, height, depth or format, use texture_replace() instead.

RID texture_create_from_native_handle(type: TextureType, format: Format, native_handle: int, width: int, height: int, depth: int, layers: int = 1, layered_type: TextureLayeredType = 0) 🔗

Creates a texture based on a native handle that was created outside of Godot's renderer.

Note: If using only the rendering device renderer, it's recommend to use RenderingDevice.texture_create_from_extension() together with texture_rd_create(), rather than this method. It will give you much more control over the texture's format and usage.

Format texture_get_format(texture: RID) const 🔗

Returns the format for the texture.

int texture_get_native_handle(texture: RID, srgb: bool = false) const 🔗

Returns the internal graphics handle for this texture object. For use when communicating with third-party APIs mostly with GDExtension.

Note: This function returns a uint64_t which internally maps to a GLuint (OpenGL) or VkImage (Vulkan).

String texture_get_path(texture: RID) const 🔗

There is currently no description for this method. Please help us by contributing one!

RID texture_get_rd_texture(texture: RID, srgb: bool = false) const 🔗

Returns a texture RID that can be used with RenderingDevice.

RID texture_proxy_create(base: RID) 🔗

Deprecated: ProxyTexture was removed in Godot 4.

This method does nothing and always returns an invalid RID.

void texture_proxy_update(texture: RID, proxy_to: RID) 🔗

Deprecated: ProxyTexture was removed in Godot 4.

This method does nothing.

RID texture_rd_create(rd_texture: RID, layer_type: TextureLayeredType = 0) 🔗

Creates a new texture object based on a texture created directly on the RenderingDevice. If the texture contains layers, layer_type is used to define the layer type.

void texture_replace(texture: RID, by_texture: RID) 🔗

Replaces texture's texture data by the texture specified by the by_texture RID, without changing texture's RID.

void texture_set_force_redraw_if_visible(texture: RID, enable: bool) 🔗

There is currently no description for this method. Please help us by contributing one!

void texture_set_path(texture: RID, path: String) 🔗

There is currently no description for this method. Please help us by contributing one!

void texture_set_size_override(texture: RID, width: int, height: int) 🔗

There is currently no description for this method. Please help us by contributing one!

void viewport_attach_camera(viewport: RID, camera: RID) 🔗

Sets a viewport's camera.

void viewport_attach_canvas(viewport: RID, canvas: RID) 🔗

Sets a viewport's canvas.

void viewport_attach_to_screen(viewport: RID, rect: Rect2 = Rect2(0, 0, 0, 0), screen: int = 0) 🔗

Copies the viewport to a region of the screen specified by rect. If viewport_set_render_direct_to_screen() is true, then the viewport does not use a framebuffer and the contents of the viewport are rendered directly to screen. However, note that the root viewport is drawn last, therefore it will draw over the screen. Accordingly, you must set the root viewport to an area that does not cover the area that you have attached this viewport to.

For example, you can set the root viewport to not render at all with the following code:

Using this can result in significant optimization, especially on lower-end devices. However, it comes at the cost of having to manage your viewports manually. For further optimization, see viewport_set_render_direct_to_screen().

RID viewport_create() 🔗

Creates an empty viewport and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all viewport_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent node is Viewport.

float viewport_get_measured_render_time_cpu(viewport: RID) const 🔗

Returns the CPU time taken to render the last frame in milliseconds. This only includes time spent in rendering-related operations; scripts' _process functions and other engine subsystems are not included in this readout. To get a complete readout of CPU time spent to render the scene, sum the render times of all viewports that are drawn every frame plus get_frame_setup_time_cpu(). Unlike Engine.get_frames_per_second(), this method will accurately reflect CPU utilization even if framerate is capped via V-Sync or Engine.max_fps. See also viewport_get_measured_render_time_gpu().

Note: Requires measurements to be enabled on the specified viewport using viewport_set_measure_render_time(). Otherwise, this method returns 0.0.

float viewport_get_measured_render_time_gpu(viewport: RID) const 🔗

Returns the GPU time taken to render the last frame in milliseconds. To get a complete readout of GPU time spent to render the scene, sum the render times of all viewports that are drawn every frame. Unlike Engine.get_frames_per_second(), this method accurately reflects GPU utilization even if framerate is capped via V-Sync or Engine.max_fps. See also viewport_get_measured_render_time_cpu().

Note: Requires measurements to be enabled on the specified viewport using viewport_set_measure_render_time(). Otherwise, this method returns 0.0.

Note: When GPU utilization is low enough during a certain period of time, GPUs will decrease their power state (which in turn decreases core and memory clock speeds). This can cause the reported GPU time to increase if GPU utilization is kept low enough by a framerate cap (compared to what it would be at the GPU's highest power state). Keep this in mind when benchmarking using viewport_get_measured_render_time_gpu(). This behavior can be overridden in the graphics driver settings at the cost of higher power usage.

int viewport_get_render_info(viewport: RID, type: ViewportRenderInfoType, info: ViewportRenderInfo) 🔗

Returns a statistic about the rendering engine which can be used for performance profiling. This is separated into render pass types, each of them having the same infos you can query (different passes will return different values).

See also get_rendering_info(), which returns global information across all viewports.

Note: Viewport rendering information is not available until at least 2 frames have been rendered by the engine. If rendering information is not available, viewport_get_render_info() returns 0. To print rendering information in _ready() successfully, use the following:

RID viewport_get_render_target(viewport: RID) const 🔗

Returns the render target for the viewport.

RID viewport_get_texture(viewport: RID) const 🔗

Returns the viewport's last rendered frame.

ViewportUpdateMode viewport_get_update_mode(viewport: RID) const 🔗

Returns the viewport's update mode.

Warning: Calling this from any thread other than the rendering thread will be detrimental to performance.

void viewport_remove_canvas(viewport: RID, canvas: RID) 🔗

Detaches a viewport from a canvas.

void viewport_set_active(viewport: RID, active: bool) 🔗

If true, sets the viewport active, else sets it inactive.

void viewport_set_anisotropic_filtering_level(viewport: RID, anisotropic_filtering_level: ViewportAnisotropicFiltering) 🔗

Sets the maximum number of samples to take when using anisotropic filtering on textures (as a power of two). A higher sample count will result in sharper textures at oblique angles, but is more expensive to compute. A value of 0 forcibly disables anisotropic filtering, even on materials where it is enabled.

The anisotropic filtering level also affects decals and light projectors if they are configured to use anisotropic filtering. See ProjectSettings.rendering/textures/decals/filter and ProjectSettings.rendering/textures/light_projectors/filter.

Note: In 3D, for this setting to have an effect, set BaseMaterial3D.texture_filter to BaseMaterial3D.TEXTURE_FILTER_LINEAR_WITH_MIPMAPS_ANISOTROPIC or BaseMaterial3D.TEXTURE_FILTER_NEAREST_WITH_MIPMAPS_ANISOTROPIC on materials.

Note: In 2D, for this setting to have an effect, set CanvasItem.texture_filter to CanvasItem.TEXTURE_FILTER_LINEAR_WITH_MIPMAPS_ANISOTROPIC or CanvasItem.TEXTURE_FILTER_NEAREST_WITH_MIPMAPS_ANISOTROPIC on the CanvasItem node displaying the texture (or in CanvasTexture). However, anisotropic filtering is rarely useful in 2D, so only enable it for textures in 2D if it makes a meaningful visual difference.

void viewport_set_canvas_cull_mask(viewport: RID, canvas_cull_mask: int) 🔗

Sets the rendering mask associated with this Viewport. Only CanvasItem nodes with a matching rendering visibility layer will be rendered by this Viewport.

void viewport_set_canvas_stacking(viewport: RID, canvas: RID, layer: int, sublayer: int) 🔗

Sets the stacking order for a viewport's canvas.

layer is the actual canvas layer, while sublayer specifies the stacking order of the canvas among those in the same layer.

Note: layer should be between CANVAS_LAYER_MIN and CANVAS_LAYER_MAX (inclusive). Any other value will wrap around.

void viewport_set_canvas_transform(viewport: RID, canvas: RID, offset: Transform2D) 🔗

Sets the transformation of a viewport's canvas.

void viewport_set_clear_mode(viewport: RID, clear_mode: ViewportClearMode) 🔗

Sets the clear mode of a viewport.

void viewport_set_debug_draw(viewport: RID, draw: ViewportDebugDraw) 🔗

Sets the debug draw mode of a viewport.

void viewport_set_default_canvas_item_texture_filter(viewport: RID, filter: CanvasItemTextureFilter) 🔗

Sets the default texture filtering mode for the specified viewport RID.

void viewport_set_default_canvas_item_texture_repeat(viewport: RID, repeat: CanvasItemTextureRepeat) 🔗

Sets the default texture repeat mode for the specified viewport RID.

void viewport_set_disable_2d(viewport: RID, disable: bool) 🔗

If true, the viewport's canvas (i.e. 2D and GUI elements) is not rendered.

void viewport_set_disable_3d(viewport: RID, disable: bool) 🔗

If true, the viewport's 3D elements are not rendered.

void viewport_set_environment_mode(viewport: RID, mode: ViewportEnvironmentMode) 🔗

Sets the viewport's environment mode which allows enabling or disabling rendering of 3D environment over 2D canvas. When disabled, 2D will not be affected by the environment. When enabled, 2D will be affected by the environment if the environment background mode is ENV_BG_CANVAS. The default behavior is to inherit the setting from the viewport's parent. If the topmost parent is also set to VIEWPORT_ENVIRONMENT_INHERIT, then the behavior will be the same as if it was set to VIEWPORT_ENVIRONMENT_ENABLED.

void viewport_set_fsr_sharpness(viewport: RID, sharpness: float) 🔗

Determines how sharp the upscaled image will be when using the FSR upscaling mode. Sharpness halves with every whole number. Values go from 0.0 (sharpest) to 2.0. Values above 2.0 won't make a visible difference.

void viewport_set_global_canvas_transform(viewport: RID, transform: Transform2D) 🔗

Sets the viewport's global transformation matrix.

void viewport_set_measure_render_time(viewport: RID, enable: bool) 🔗

Sets the measurement for the given viewport RID (obtained using Viewport.get_viewport_rid()). Once enabled, viewport_get_measured_render_time_cpu() and viewport_get_measured_render_time_gpu() will return values greater than 0.0 when queried with the given viewport.

void viewport_set_msaa_2d(viewport: RID, msaa: ViewportMSAA) 🔗

Sets the multisample antialiasing mode for 2D/Canvas on the specified viewport RID. Equivalent to ProjectSettings.rendering/anti_aliasing/quality/msaa_2d or Viewport.msaa_2d.

void viewport_set_msaa_3d(viewport: RID, msaa: ViewportMSAA) 🔗

Sets the multisample antialiasing mode for 3D on the specified viewport RID. Equivalent to ProjectSettings.rendering/anti_aliasing/quality/msaa_3d or Viewport.msaa_3d.

void viewport_set_occlusion_culling_build_quality(quality: ViewportOcclusionCullingBuildQuality) 🔗

Sets the ProjectSettings.rendering/occlusion_culling/bvh_build_quality to use for occlusion culling. This parameter is global and cannot be set on a per-viewport basis.

void viewport_set_occlusion_rays_per_thread(rays_per_thread: int) 🔗

Sets the ProjectSettings.rendering/occlusion_culling/occlusion_rays_per_thread to use for occlusion culling. This parameter is global and cannot be set on a per-viewport basis.

void viewport_set_parent_viewport(viewport: RID, parent_viewport: RID) 🔗

Sets the viewport's parent to the viewport specified by the parent_viewport RID.

void viewport_set_positional_shadow_atlas_quadrant_subdivision(viewport: RID, quadrant: int, subdivision: int) 🔗

Sets the number of subdivisions to use in the specified shadow atlas quadrant for omni and spot shadows. See also Viewport.set_positional_shadow_atlas_quadrant_subdiv().

void viewport_set_positional_shadow_atlas_size(viewport: RID, size: int, use_16_bits: bool = false) 🔗

Sets the size of the shadow atlas's images (used for omni and spot lights) on the viewport specified by the viewport RID. The value is rounded up to the nearest power of 2. If use_16_bits is true, use 16 bits for the omni/spot shadow depth map. Enabling this results in shadows having less precision and may result in shadow acne, but can lead to performance improvements on some devices.

Note: If this is set to 0, no positional shadows will be visible at all. This can improve performance significantly on low-end systems by reducing both the CPU and GPU load (as fewer draw calls are needed to draw the scene without shadows).

void viewport_set_render_direct_to_screen(viewport: RID, enabled: bool) 🔗

If true, render the contents of the viewport directly to screen. This allows a low-level optimization where you can skip drawing a viewport to the root viewport. While this optimization can result in a significant increase in speed (especially on older devices), it comes at a cost of usability. When this is enabled, you cannot read from the viewport or from the screen_texture. You also lose the benefit of certain window settings, such as the various stretch modes. Another consequence to be aware of is that in 2D the rendering happens in window coordinates, so if you have a viewport that is double the size of the window, and you set this, then only the portion that fits within the window will be drawn, no automatic scaling is possible, even if your game scene is significantly larger than the window size.

void viewport_set_scaling_3d_mode(viewport: RID, scaling_3d_mode: ViewportScaling3DMode) 🔗

Sets the 3D resolution scaling mode. Bilinear scaling renders at different resolution to either undersample or supersample the viewport. FidelityFX Super Resolution 1.0, abbreviated to FSR, is an upscaling technology that produces high quality images at fast framerates by using a spatially aware upscaling algorithm. FSR is slightly more expensive than bilinear, but it produces significantly higher image quality. FSR should be used where possible.

void viewport_set_scaling_3d_scale(viewport: RID, scale: float) 🔗

Scales the 3D render buffer based on the viewport size uses an image filter specified in ViewportScaling3DMode to scale the output image to the full viewport size. Values lower than 1.0 can be used to speed up 3D rendering at the cost of quality (undersampling). Values greater than 1.0 are only valid for bilinear mode and can be used to improve 3D rendering quality at a high performance cost (supersampling). See also ViewportMSAA for multi-sample antialiasing, which is significantly cheaper but only smoothens the edges of polygons.

When using FSR upscaling, AMD recommends exposing the following values as preset options to users "Ultra Quality: 0.77", "Quality: 0.67", "Balanced: 0.59", "Performance: 0.5" instead of exposing the entire scale.

void viewport_set_scenario(viewport: RID, scenario: RID) 🔗

Sets a viewport's scenario. The scenario contains information about environment information, reflection atlas, etc.

void viewport_set_screen_space_aa(viewport: RID, mode: ViewportScreenSpaceAA) 🔗

Sets the viewport's screen-space antialiasing mode. Equivalent to ProjectSettings.rendering/anti_aliasing/quality/screen_space_aa or Viewport.screen_space_aa.

void viewport_set_sdf_oversize_and_scale(viewport: RID, oversize: ViewportSDFOversize, scale: ViewportSDFScale) 🔗

Sets the viewport's 2D signed distance field ProjectSettings.rendering/2d/sdf/oversize and ProjectSettings.rendering/2d/sdf/scale. This is used when sampling the signed distance field in CanvasItem shaders as well as GPUParticles2D collision. This is not used by SDFGI in 3D rendering.

void viewport_set_size(viewport: RID, width: int, height: int) 🔗

Sets the viewport's width and height in pixels.

void viewport_set_snap_2d_transforms_to_pixel(viewport: RID, enabled: bool) 🔗

If true, canvas item transforms (i.e. origin position) are snapped to the nearest pixel when rendering. This can lead to a crisper appearance at the cost of less smooth movement, especially when Camera2D smoothing is enabled. Equivalent to ProjectSettings.rendering/2d/snap/snap_2d_transforms_to_pixel.

void viewport_set_snap_2d_vertices_to_pixel(viewport: RID, enabled: bool) 🔗

If true, canvas item vertices (i.e. polygon points) are snapped to the nearest pixel when rendering. This can lead to a crisper appearance at the cost of less smooth movement, especially when Camera2D smoothing is enabled. Equivalent to ProjectSettings.rendering/2d/snap/snap_2d_vertices_to_pixel.

void viewport_set_texture_mipmap_bias(viewport: RID, mipmap_bias: float) 🔗

Affects the final texture sharpness by reading from a lower or higher mipmap (also called "texture LOD bias"). Negative values make mipmapped textures sharper but grainier when viewed at a distance, while positive values make mipmapped textures blurrier (even when up close). To get sharper textures at a distance without introducing too much graininess, set this between -0.75 and 0.0. Enabling temporal antialiasing (ProjectSettings.rendering/anti_aliasing/quality/use_taa) can help reduce the graininess visible when using negative mipmap bias.

Note: When the 3D scaling mode is set to FSR 1.0, this value is used to adjust the automatic mipmap bias which is calculated internally based on the scale factor. The formula for this is -log2(1.0 / scale) + mipmap_bias.

void viewport_set_transparent_background(viewport: RID, enabled: bool) 🔗

If true, the viewport renders its background as transparent.

void viewport_set_update_mode(viewport: RID, update_mode: ViewportUpdateMode) 🔗

Sets when the viewport should be updated.

void viewport_set_use_debanding(viewport: RID, enable: bool) 🔗

Equivalent to Viewport.use_debanding. See also ProjectSettings.rendering/anti_aliasing/quality/use_debanding.

void viewport_set_use_hdr_2d(viewport: RID, enabled: bool) 🔗

If true, 2D rendering will use a high dynamic range (HDR) format framebuffer matching the bit depth of the 3D framebuffer. When using the Forward+ or Compatibility renderer, this will be an RGBA16 framebuffer. When using the Mobile renderer, it will be an RGB10_A2 framebuffer.

Additionally, 2D rendering will take place in linear color space and will be converted to sRGB space immediately before blitting to the screen (if the Viewport is attached to the screen).

Practically speaking, this means that the end result of the Viewport will not be clamped to the 0-1 range and can be used in 3D rendering without color space adjustments. This allows 2D rendering to take advantage of effects requiring high dynamic range (e.g. 2D glow) as well as substantially improves the appearance of effects requiring highly detailed gradients. This setting has the same effect as Viewport.use_hdr_2d.

void viewport_set_use_occlusion_culling(viewport: RID, enable: bool) 🔗

If true, enables occlusion culling on the specified viewport. Equivalent to ProjectSettings.rendering/occlusion_culling/use_occlusion_culling.

void viewport_set_use_taa(viewport: RID, enable: bool) 🔗

If true, use temporal antialiasing. Equivalent to ProjectSettings.rendering/anti_aliasing/quality/use_taa or Viewport.use_taa.

void viewport_set_use_xr(viewport: RID, use_xr: bool) 🔗

If true, the viewport uses augmented or virtual reality technologies. See XRInterface.

void viewport_set_vrs_mode(viewport: RID, mode: ViewportVRSMode) 🔗

Sets the Variable Rate Shading (VRS) mode for the viewport. If the GPU does not support VRS, this property is ignored. Equivalent to ProjectSettings.rendering/vrs/mode.

void viewport_set_vrs_texture(viewport: RID, texture: RID) 🔗

The texture to use when the VRS mode is set to VIEWPORT_VRS_TEXTURE. Equivalent to ProjectSettings.rendering/vrs/texture.

void viewport_set_vrs_update_mode(viewport: RID, mode: ViewportVRSUpdateMode) 🔗

Sets the update mode for Variable Rate Shading (VRS) for the viewport. VRS requires the input texture to be converted to the format usable by the VRS method supported by the hardware. The update mode defines how often this happens. If the GPU does not support VRS, or VRS is not enabled, this property is ignored.

If set to VIEWPORT_VRS_UPDATE_ONCE, the input texture is copied once and the mode is changed to VIEWPORT_VRS_UPDATE_DISABLED.

RID visibility_notifier_create() 🔗

Creates a new 3D visibility notifier object and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all visibility_notifier_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

To place in a scene, attach this notifier to an instance using instance_set_base() using the returned RID.

Note: The equivalent node is VisibleOnScreenNotifier3D.

void visibility_notifier_set_aabb(notifier: RID, aabb: AABB) 🔗

There is currently no description for this method. Please help us by contributing one!

void visibility_notifier_set_callbacks(notifier: RID, enter_callable: Callable, exit_callable: Callable) 🔗

There is currently no description for this method. Please help us by contributing one!

void voxel_gi_allocate_data(voxel_gi: RID, to_cell_xform: Transform3D, aabb: AABB, octree_size: Vector3i, octree_cells: PackedByteArray, data_cells: PackedByteArray, distance_field: PackedByteArray, level_counts: PackedInt32Array) 🔗

There is currently no description for this method. Please help us by contributing one!

RID voxel_gi_create() 🔗

Creates a new voxel-based global illumination object and adds it to the RenderingServer. It can be accessed with the RID that is returned. This RID will be used in all voxel_gi_* RenderingServer functions.

Once finished with your RID, you will want to free the RID using the RenderingServer's free_rid() method.

Note: The equivalent node is VoxelGI.

PackedByteArray voxel_gi_get_data_cells(voxel_gi: RID) const 🔗

There is currently no description for this method. Please help us by contributing one!

PackedByteArray voxel_gi_get_distance_field(voxel_gi: RID) const 🔗

There is currently no description for this method. Please help us by contributing one!

PackedInt32Array voxel_gi_get_level_counts(voxel_gi: RID) const 🔗

There is currently no description for this method. Please help us by contributing one!

PackedByteArray voxel_gi_get_octree_cells(voxel_gi: RID) const 🔗

There is currently no description for this method. Please help us by contributing one!

Vector3i voxel_gi_get_octree_size(voxel_gi: RID) const 🔗

There is currently no description for this method. Please help us by contributing one!

Transform3D voxel_gi_get_to_cell_xform(voxel_gi: RID) const 🔗

There is currently no description for this method. Please help us by contributing one!

void voxel_gi_set_baked_exposure_normalization(voxel_gi: RID, baked_exposure: float) 🔗

Used to inform the renderer what exposure normalization value was used while baking the voxel gi. This value will be used and modulated at run time to ensure that the voxel gi maintains a consistent level of exposure even if the scene-wide exposure normalization is changed at run time. For more information see camera_attributes_set_exposure().

void voxel_gi_set_bias(voxel_gi: RID, bias: float) 🔗

Sets the VoxelGIData.bias value to use on the specified voxel_gi's RID.

void voxel_gi_set_dynamic_range(voxel_gi: RID, range: float) 🔗

Sets the VoxelGIData.dynamic_range value to use on the specified voxel_gi's RID.

void voxel_gi_set_energy(voxel_gi: RID, energy: float) 🔗

Sets the VoxelGIData.energy value to use on the specified voxel_gi's RID.

void voxel_gi_set_interior(voxel_gi: RID, enable: bool) 🔗

Sets the VoxelGIData.interior value to use on the specified voxel_gi's RID.

void voxel_gi_set_normal_bias(voxel_gi: RID, bias: float) 🔗

Sets the VoxelGIData.normal_bias value to use on the specified voxel_gi's RID.

void voxel_gi_set_propagation(voxel_gi: RID, amount: float) 🔗

Sets the VoxelGIData.propagation value to use on the specified voxel_gi's RID.

void voxel_gi_set_quality(quality: VoxelGIQuality) 🔗

Sets the ProjectSettings.rendering/global_illumination/voxel_gi/quality value to use when rendering. This parameter is global and cannot be set on a per-VoxelGI basis.

void voxel_gi_set_use_two_bounces(voxel_gi: RID, enable: bool) 🔗

Sets the VoxelGIData.use_two_bounces value to use on the specified voxel_gi's RID.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (go):
```go
func get_exposure_normalization(ev100: float):
    return 1.0 / (pow(2.0, ev100) * 1.2)
```

Example 2 (go):
```go
func get_exposure(aperture: float, shutter_speed: float, sensitivity: float):
    return log((aperture * aperture) / shutter_speed * (100.0 / sensitivity)) / log(2)
```

Example 3 (gdscript):
```gdscript
func _ready():
    for _i in 2:
        await get_tree().process_frame

    print(RenderingServer.get_rendering_info(RENDERING_INFO_TOTAL_DRAW_CALLS_IN_FRAME))
```

Example 4 (gdscript):
```gdscript
var texture_rid = RenderingServer.get_test_texture()
var texture = ImageTexture.create_from_image(RenderingServer.texture_2d_get(texture_rid))
$Sprite2D.texture = texture
```

---

## Rendering

**URL:** https://docs.godotengine.org/en/stable/tutorials/rendering/index.html

**Contents:**
- Rendering

Most rendering topics are covered in 2D rendering and 3D rendering.

---

## RenderSceneBuffersRD

**URL:** https://docs.godotengine.org/en/stable/classes/class_renderscenebuffersrd.html

**Contents:**
- RenderSceneBuffersRD
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: RenderSceneBuffers < RefCounted < Object

Render scene buffer implementation for the RenderingDevice based renderers.

This object manages all 3D rendering buffers for the rendering device based renderers. An instance of this object is created for every viewport that has 3D rendering enabled.

All buffers are organized in contexts. The default context is called render_buffers and can contain amongst others the color buffer, depth buffer, velocity buffers, VRS density map and MSAA variants of these buffers.

Buffers are only guaranteed to exist during rendering of the viewport.

Note: This is an internal rendering server object, do not instantiate this from script.

clear_context(context: StringName)

create_texture(context: StringName, name: StringName, data_format: DataFormat, usage_bits: int, texture_samples: TextureSamples, size: Vector2i, layers: int, mipmaps: int, unique: bool, discardable: bool)

create_texture_from_format(context: StringName, name: StringName, format: RDTextureFormat, view: RDTextureView, unique: bool)

create_texture_view(context: StringName, name: StringName, view_name: StringName, view: RDTextureView)

get_color_layer(layer: int, msaa: bool = false)

get_color_texture(msaa: bool = false)

get_depth_layer(layer: int, msaa: bool = false)

get_depth_texture(msaa: bool = false)

get_fsr_sharpness() const

get_internal_size() const

get_render_target() const

ViewportScaling3DMode

get_scaling_3d_mode() const

ViewportScreenSpaceAA

get_screen_space_aa() const

get_target_size() const

get_texture(context: StringName, name: StringName) const

get_texture_format(context: StringName, name: StringName) const

get_texture_samples() const

get_texture_slice(context: StringName, name: StringName, layer: int, mipmap: int, layers: int, mipmaps: int)

get_texture_slice_size(context: StringName, name: StringName, mipmap: int)

get_texture_slice_view(context: StringName, name: StringName, layer: int, mipmap: int, layers: int, mipmaps: int, view: RDTextureView)

get_use_debanding() const

get_velocity_layer(layer: int, msaa: bool = false)

get_velocity_texture(msaa: bool = false)

get_view_count() const

has_texture(context: StringName, name: StringName) const

void clear_context(context: StringName) 🔗

Frees all buffers related to this context.

RID create_texture(context: StringName, name: StringName, data_format: DataFormat, usage_bits: int, texture_samples: TextureSamples, size: Vector2i, layers: int, mipmaps: int, unique: bool, discardable: bool) 🔗

Create a new texture with the given definition and cache this under the given name. Will return the existing texture if it already exists.

RID create_texture_from_format(context: StringName, name: StringName, format: RDTextureFormat, view: RDTextureView, unique: bool) 🔗

Create a new texture using the given format and view and cache this under the given name. Will return the existing texture if it already exists.

RID create_texture_view(context: StringName, name: StringName, view_name: StringName, view: RDTextureView) 🔗

Create a new texture view for an existing texture and cache this under the given view_name. Will return the existing texture view if it already exists. Will error if the source texture doesn't exist.

RID get_color_layer(layer: int, msaa: bool = false) 🔗

Returns the specified layer from the color texture we are rendering 3D content to.

If msaa is true and MSAA is enabled, this returns the MSAA variant of the buffer.

RID get_color_texture(msaa: bool = false) 🔗

Returns the color texture we are rendering 3D content to. If multiview is used this will be a texture array with all views.

If msaa is true and MSAA is enabled, this returns the MSAA variant of the buffer.

RID get_depth_layer(layer: int, msaa: bool = false) 🔗

Returns the specified layer from the depth texture we are rendering 3D content to.

If msaa is true and MSAA is enabled, this returns the MSAA variant of the buffer.

RID get_depth_texture(msaa: bool = false) 🔗

Returns the depth texture we are rendering 3D content to. If multiview is used this will be a texture array with all views.

If msaa is true and MSAA is enabled, this returns the MSAA variant of the buffer.

float get_fsr_sharpness() const 🔗

Returns the FSR sharpness value used while rendering the 3D content (if get_scaling_3d_mode() is an FSR mode).

Vector2i get_internal_size() const 🔗

Returns the internal size of the render buffer (size before upscaling) with which textures are created by default.

ViewportMSAA get_msaa_3d() const 🔗

Returns the applied 3D MSAA mode for this viewport.

RID get_render_target() const 🔗

Returns the render target associated with this buffers object.

ViewportScaling3DMode get_scaling_3d_mode() const 🔗

Returns the scaling mode used for upscaling.

ViewportScreenSpaceAA get_screen_space_aa() const 🔗

Returns the screen-space antialiasing method applied.

Vector2i get_target_size() const 🔗

Returns the target size of the render buffer (size after upscaling).

RID get_texture(context: StringName, name: StringName) const 🔗

Returns a cached texture with this name.

RDTextureFormat get_texture_format(context: StringName, name: StringName) const 🔗

Returns the texture format information with which a cached texture was created.

TextureSamples get_texture_samples() const 🔗

Returns the number of MSAA samples used.

RID get_texture_slice(context: StringName, name: StringName, layer: int, mipmap: int, layers: int, mipmaps: int) 🔗

Returns a specific slice (layer or mipmap) for a cached texture.

Vector2i get_texture_slice_size(context: StringName, name: StringName, mipmap: int) 🔗

Returns the texture size of a given slice of a cached texture.

RID get_texture_slice_view(context: StringName, name: StringName, layer: int, mipmap: int, layers: int, mipmaps: int, view: RDTextureView) 🔗

Returns a specific view of a slice (layer or mipmap) for a cached texture.

bool get_use_debanding() const 🔗

Returns true if debanding is enabled.

bool get_use_taa() const 🔗

Returns true if TAA is enabled.

RID get_velocity_layer(layer: int, msaa: bool = false) 🔗

Returns the specified layer from the velocity texture we are rendering 3D content to.

RID get_velocity_texture(msaa: bool = false) 🔗

Returns the velocity texture we are rendering 3D content to. If multiview is used this will be a texture array with all views.

If msaa is true and MSAA is enabled, this returns the MSAA variant of the buffer.

int get_view_count() const 🔗

Returns the view count for the associated viewport.

bool has_texture(context: StringName, name: StringName) const 🔗

Returns true if a cached texture exists for this name.

Please read the User-contributed notes policy before submitting a comment.

---

## RenderSceneBuffers

**URL:** https://docs.godotengine.org/en/stable/classes/class_renderscenebuffers.html

**Contents:**
- RenderSceneBuffers
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Inherited By: RenderSceneBuffersExtension, RenderSceneBuffersRD

Abstract scene buffers object, created for each viewport for which 3D rendering is done.

Abstract scene buffers object, created for each viewport for which 3D rendering is done. It manages any additional buffers used during rendering and will discard buffers when the viewport is resized.

Note: This is an internal rendering server object, do not instantiate this from script.

configure(config: RenderSceneBuffersConfiguration)

void configure(config: RenderSceneBuffersConfiguration) 🔗

This method is called by the rendering server when the associated viewport's configuration is changed. It will discard the old buffers and recreate the internal buffers used.

Please read the User-contributed notes policy before submitting a comment.

---

## RenderSceneDataRD

**URL:** https://docs.godotengine.org/en/stable/classes/class_renderscenedatard.html

**Contents:**
- RenderSceneDataRD
- Description
- User-contributed notes

Inherits: RenderSceneData < Object

Render scene data implementation for the RenderingDevice based renderers.

Object holds scene data related to rendering a single frame of a viewport.

Note: This is an internal rendering server object, do not instantiate this from script.

Please read the User-contributed notes policy before submitting a comment.

---

## RenderSceneData

**URL:** https://docs.godotengine.org/en/stable/classes/class_renderscenedata.html

**Contents:**
- RenderSceneData
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherited By: RenderSceneDataExtension, RenderSceneDataRD

Abstract render data object, holds scene data related to rendering a single frame of a viewport.

Abstract scene data object, exists for the duration of rendering a single viewport.

Note: This is an internal rendering server object, do not instantiate this from script.

get_cam_projection() const

get_cam_transform() const

get_uniform_buffer() const

get_view_count() const

get_view_eye_offset(view: int) const

get_view_projection(view: int) const

Projection get_cam_projection() const 🔗

Returns the camera projection used to render this frame.

Note: If more than one view is rendered, this will return a combined projection.

Transform3D get_cam_transform() const 🔗

Returns the camera transform used to render this frame.

Note: If more than one view is rendered, this will return a centered transform.

RID get_uniform_buffer() const 🔗

Return the RID of the uniform buffer containing the scene data as a UBO.

int get_view_count() const 🔗

Returns the number of views being rendered.

Vector3 get_view_eye_offset(view: int) const 🔗

Returns the eye offset per view used to render this frame. This is the offset between our camera transform and the eye transform.

Projection get_view_projection(view: int) const 🔗

Returns the view projection per view used to render this frame.

Note: If a single view is rendered, this returns the camera projection. If more than one view is rendered, this will return a projection for the given view including the eye offset.

Please read the User-contributed notes policy before submitting a comment.

---

## ResourceImporterLayeredTexture

**URL:** https://docs.godotengine.org/en/stable/classes/class_resourceimporterlayeredtexture.html

**Contents:**
- ResourceImporterLayeredTexture
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: ResourceImporter < RefCounted < Object

Imports a 3-dimensional texture (Texture3D), a Texture2DArray, a Cubemap or a CubemapArray.

This imports a 3-dimensional texture, which can then be used in custom shaders, as a FogMaterial density map or as a GPUParticlesAttractorVectorField3D. See also ResourceImporterTexture and ResourceImporterTextureAtlas.

compress/channel_pack

compress/hdr_compression

compress/high_quality

compress/lossy_quality

compress/rdo_quality_loss

int compress/channel_pack = 0 🔗

Controls how color channels should be used in the imported texture.

sRGB Friendly:, prevents the RG color format from being used, as it does not support sRGB color.

Optimized:, allows the RG color format to be used if the texture does not use the blue channel. This reduces memory usage if the texture's blue channel can be discarded (all pixels must have a blue value of 0).

Normal Map (RG Channels): This forces all layers from the texture to be imported with the RG color format, with only the red and green channels preserved. RGTC (Red-Green Texture Compression) compression is able to preserve its detail much better, while using the same amount of memory as a standard RGBA VRAM-compressed texture. This only has an effect on textures with the VRAM Compressed or Basis Universal compression modes. This mode is only available in layered textures (Cubemap, CubemapArray, Texture2DArray and Texture3D).

int compress/hdr_compression = 1 🔗

Controls how VRAM compression should be performed for HDR images.

Disabled: Never use VRAM compression for HDR textures, regardless of whether they're opaque or transparent. Instead, the texture is converted to RGBE9995 (9-bits per channel + 5-bit exponent = 32 bits per pixel) to reduce memory usage compared to a half-float or single-precision float image format.

Opaque Only: Only uses VRAM compression for opaque HDR textures. This is due to a limitation of HDR formats, as there is no VRAM-compressed HDR format that supports transparency at the same time.

Always: Force VRAM compression even for HDR textures with an alpha channel. To perform this, the alpha channel is discarded on import.

Note: Only effective on Radiance HDR (.hdr) and OpenEXR (.exr) images.

bool compress/high_quality = false 🔗

If true, uses BPTC compression on desktop platforms and ASTC compression on mobile platforms. When using BPTC, BC7 is used for SDR textures and BC6H is used for HDR textures.

If false, uses the faster but lower-quality S3TC compression on desktop platforms and ETC2 on mobile/web platforms. When using S3TC, DXT1 (BC1) is used for opaque textures and DXT5 (BC3) is used for transparent or normal map (RGTC) textures.

BPTC and ASTC support VRAM compression for HDR textures, but S3TC and ETC2 do not (see compress/hdr_compression).

float compress/lossy_quality = 0.7 🔗

The quality to use when using the Lossy compression mode. Higher values result in better quality, at the cost of larger file sizes. Lossy quality does not affect memory usage of the imported texture, only its file size on disk.

int compress/mode = 1 🔗

The compression mode to use. Each compression mode provides a different tradeoff:

Lossless: Original quality, high memory usage, high size on disk, fast import.

Lossy: Reduced quality, high memory usage, low size on disk, fast import.

VRAM Compressed: Reduced quality, low memory usage, low size on disk, slowest import. Only use for textures in 3D scenes, not for 2D elements.

VRAM Uncompressed: Original quality, high memory usage, highest size on disk, fastest import.

Basis Universal: Reduced quality, low memory usage, lowest size on disk, slow import. Only use for textures in 3D scenes, not for 2D elements.

See Compress mode in the manual for more details.

float compress/rdo_quality_loss = 0.0 🔗

If greater than or equal to 0.01, enables Rate-Distortion Optimization (RDO) to reduce file size. Higher values result in smaller file sizes but lower quality.

Note: Enabling RDO makes encoding times significantly longer, especially when the image is large.

See also ProjectSettings.rendering/textures/basis_universal/rdo_dict_size and ProjectSettings.rendering/textures/basis_universal/zstd_supercompression_level if you want to reduce the file size further.

int compress/uastc_level = 0 🔗

The UASTC encoding level. Higher values result in better quality but make encoding times longer.

bool mipmaps/generate = true 🔗

If true, smaller versions of the texture are generated on import. For example, a 64×64 texture will generate 6 mipmaps (32×32, 16×16, 8×8, 4×4, 2×2, 1×1). This has several benefits:

Textures will not become grainy in the distance (in 3D), or if scaled down due to Camera2D zoom or CanvasItem scale (in 2D).

Performance will improve if the texture is displayed in the distance, since sampling smaller versions of the original texture is faster and requires less memory bandwidth.

The downside of mipmaps is that they increase memory usage by roughly 33% (for Texture2DArray, Cubemap and CubemapArray) or 14% (for Texture3D).

It's recommended to enable mipmaps in 3D. However, in 2D, this should only be enabled if your project visibly benefits from having mipmaps enabled. If the camera never zooms out significantly, there won't be a benefit to enabling mipmaps but memory usage will increase.

int mipmaps/limit = -1 🔗

Unimplemented. This currently has no effect when changed.

int slices/arrangement = 1 🔗

Controls how the cubemap's texture is internally laid out. When using high-resolution cubemaps, 2×3 and 3×2 are less prone to exceeding hardware texture size limits compared to 1×6 and 6×1.

Please read the User-contributed notes policy before submitting a comment.

---

## ResourceImporterShaderFile

**URL:** https://docs.godotengine.org/en/stable/classes/class_resourceimportershaderfile.html

**Contents:**
- ResourceImporterShaderFile
- Description
- User-contributed notes

Inherits: ResourceImporter < RefCounted < Object

Imports native GLSL shaders (not Godot shaders) as an RDShaderFile.

This imports native GLSL shaders as RDShaderFile resources, for use with low-level RenderingDevice operations. This importer does not handle .gdshader files.

Please read the User-contributed notes policy before submitting a comment.

---

## Screen-reading shaders

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/screen-reading_shaders.html

**Contents:**
- Screen-reading shaders
- Introduction
- Screen texture
- Screen texture example
- Behind the scenes
- Back-buffer logic
- Depth texture
- Normal-roughness texture
- Redefining screen textures
- User-contributed notes

It is often desired to make a shader that reads from the same screen to which it's writing. 3D APIs, such as OpenGL or DirectX, make this very difficult because of internal hardware limitations. GPUs are extremely parallel, so reading and writing causes all sorts of cache and coherency problems. As a result, not even the most modern hardware supports this properly.

The workaround is to make a copy of the screen, or a part of the screen, to a back-buffer and then read from it while drawing. Godot provides a few tools that make this process easy.

Godot Shading language has a special texture to access the already rendered contents of the screen. It is used by specifying a hint when declaring a sampler2D uniform: hint_screen_texture. A special built-in varying SCREEN_UV can be used to obtain the UV relative to the screen for the current fragment. As a result, this canvas_item fragment shader results in an invisible object, because it only shows what lies behind:

textureLod is used here as we only want to read from the bottom mipmap. If you want to read from a blurred version of the texture instead, you can increase the third argument to textureLod and change the hint filter_nearest to filter_nearest_mipmap (or any other filter with mipmaps enabled). If using a filter with mipmaps, Godot will automatically calculate the blurred texture for you.

If the filter mode is not changed to a filter mode that contains mipmap in its name, textureLod with an LOD parameter greater than 0.0 will have the same appearance as with the 0.0 LOD parameter.

The screen texture can be used for many things. There is a special demo for Screen Space Shaders, that you can download to see and learn. One example is a simple shader to adjust brightness, contrast and saturation:

While this seems magical, it's not. In 2D, when hint_screen_texture is first found in a node that is about to be drawn, Godot does a full-screen copy to a back-buffer. Subsequent nodes that use it in shaders will not have the screen copied for them, because this ends up being inefficient. In 3D, the screen is copied after the opaque geometry pass, but before the transparent geometry pass, so transparent objects will not be captured in the screen texture.

As a result, in 2D, if shaders that use hint_screen_texture overlap, the second one will not use the result of the first one, resulting in unexpected visuals:

In the above image, the second sphere (top right) is using the same source for the screen texture as the first one below, so the first one "disappears", or is not visible.

In 2D, this can be corrected via the BackBufferCopy node, which can be instantiated between both spheres. BackBufferCopy can work by either specifying a screen region or the whole screen:

With correct back-buffer copying, the two spheres blend correctly:

In 3D, materials that use hint_screen_texture are considered transparent themselves and will not appear in the resulting screen texture of other materials. If you plan to instance a scene that uses a material with hint_screen_texture, you will need to use a BackBufferCopy node.

In 3D, there is less flexibility to solve this particular issue because the screen texture is only captured once. Be careful when using the screen texture in 3D as it won't capture transparent objects and may capture some opaque objects that are in front of the object using the screen texture.

You can reproduce the back-buffer logic in 3D by creating a Viewport with a camera in the same position as your object, and then use the Viewport's texture instead of the screen texture.

So, to make it clearer, here's how the backbuffer copying logic works in 2D in Godot:

If a node uses hint_screen_texture, the entire screen is copied to the back buffer before drawing that node. This only happens the first time; subsequent nodes do not trigger this.

If a BackBufferCopy node was processed before the situation in the point above (even if hint_screen_texture was not used), the behavior described in the point above does not happen. In other words, automatic copying of the entire screen only happens if hint_screen_texture is used in a node for the first time and no BackBufferCopy node (not disabled) was found before in tree-order.

BackBufferCopy can copy either the entire screen or a region. If set to only a region (not the whole screen) and your shader uses pixels not in the region copied, the result of that read is undefined (most likely garbage from previous frames). In other words, it's possible to use BackBufferCopy to copy back a region of the screen and then read the screen texture from a different region. Avoid this behavior!

For 3D shaders, it's also possible to access the screen depth buffer. For this, the hint_depth_texture hint is used. This texture is not linear; it must be converted using the inverse projection matrix.

The following code retrieves the 3D position below the pixel being drawn:

Normal-roughness texture is only supported in the Forward+ rendering method, not Mobile or Compatibility.

Similarly, the normal-roughness texture can be used to read the normals and roughness of objects rendered in the depth prepass. The normal is stored in the .xyz channels (mapped to the 0-1 range) while the roughness is stored in the .w channel.

The screen texture hints (hint_screen_texture, hint_depth_texture, and hint_normal_roughness_texture) can be used with multiple uniforms. For example, you may want to read from the texture multiple times with a different repeat flag or filter flag.

The following example shows a shader that reads the screen space normal with linear filtering, but reads the screen space roughness using nearest neighbor filtering.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (cpp):
```cpp
shader_type canvas_item;

uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

void fragment() {
    COLOR = textureLod(screen_texture, SCREEN_UV, 0.0);
}
```

Example 2 (cpp):
```cpp
shader_type canvas_item;

uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

uniform float brightness = 1.0;
uniform float contrast = 1.0;
uniform float saturation = 1.0;

void fragment() {
    vec3 c = textureLod(screen_texture, SCREEN_UV, 0.0).rgb;

    c.rgb = mix(vec3(0.0), c.rgb, brightness);
    c.rgb = mix(vec3(0.5), c.rgb, contrast);
    c.rgb = mix(vec3(dot(vec3(1.0), c.rgb) * 0.33333), c.rgb, saturation);

    COLOR.rgb = c;
}
```

Example 3 (cpp):
```cpp
uniform sampler2D depth_texture : hint_depth_texture, repeat_disable, filter_nearest;

void fragment() {
    float depth = textureLod(depth_texture, SCREEN_UV, 0.0).r;
    vec4 upos = INV_PROJECTION_MATRIX * vec4(SCREEN_UV * 2.0 - 1.0, depth, 1.0);
    vec3 pixel_position = upos.xyz / upos.w;
}
```

Example 4 (cpp):
```cpp
uniform sampler2D normal_roughness_texture : hint_normal_roughness_texture, repeat_disable, filter_nearest;

void fragment() {
    float screen_roughness = texture(normal_roughness_texture, SCREEN_UV).w;
    vec3 screen_normal = texture(normal_roughness_texture, SCREEN_UV).xyz;
    screen_normal = screen_normal * 2.0 - 1.0;
```

---

## ShaderGlobalsOverride

**URL:** https://docs.godotengine.org/en/stable/classes/class_shaderglobalsoverride.html

**Contents:**
- ShaderGlobalsOverride
- Description
- Tutorials
- User-contributed notes

Inherits: Node < Object

A node used to override global shader parameters' values in a scene.

Similar to how a WorldEnvironment node can be used to override the environment while a specific scene is loaded, ShaderGlobalsOverride can be used to override global shader parameters temporarily. Once the node is removed, the project-wide values for the global shader parameters are restored. See the RenderingServer global_shader_parameter_* methods for more information.

Note: Only one ShaderGlobalsOverride can be used per scene. If there is more than one ShaderGlobalsOverride node in the scene tree, only the first node (in tree order) will be taken into account.

Note: All ShaderGlobalsOverride nodes are made part of a "shader_overrides_group" group when they are added to the scene tree. The currently active ShaderGlobalsOverride node also has a "shader_overrides_group_active" group added to it. You can use this to check which ShaderGlobalsOverride node is currently active.

Please read the User-contributed notes policy before submitting a comment.

---

## ShaderIncludeDB

**URL:** https://docs.godotengine.org/en/stable/classes/class_shaderincludedb.html

**Contents:**
- ShaderIncludeDB
- Description
- Methods
- Method Descriptions
- User-contributed notes

Internal database of built in shader include files.

This object contains shader fragments from Godot's internal shaders. These can be used when access to internal uniform buffers and/or internal functions is required for instance when composing compositor effects or compute shaders. Only fragments for the current rendering device are loaded.

get_built_in_include_file(filename: String) static

has_built_in_include_file(filename: String) static

list_built_in_include_files() static

String get_built_in_include_file(filename: String) static 🔗

Returns the code for the built-in shader fragment. You can also access this in your shader code through #include "filename".

bool has_built_in_include_file(filename: String) static 🔗

Returns true if an include file with this name exists.

PackedStringArray list_built_in_include_files() static 🔗

Returns a list of built-in include files that are currently registered.

Please read the User-contributed notes policy before submitting a comment.

---

## ShaderInclude

**URL:** https://docs.godotengine.org/en/stable/classes/class_shaderinclude.html

**Contents:**
- ShaderInclude
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

A snippet of shader code to be included in a Shader with #include.

A shader include file, saved with the .gdshaderinc extension. This class allows you to define a custom shader snippet that can be included in a Shader by using the preprocessor directive #include, followed by the file path (e.g. #include "res://shader_lib.gdshaderinc"). The snippet doesn't have to be a valid shader on its own.

void set_code(value: String)

Returns the code of the shader include file. The returned text is what the user has written, not the full generated code used internally.

Please read the User-contributed notes policy before submitting a comment.

---

## ShaderMaterial

**URL:** https://docs.godotengine.org/en/stable/classes/class_shadermaterial.html

**Contents:**
- ShaderMaterial
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Material < Resource < RefCounted < Object

A material defined by a custom Shader program and the values of its shader parameters.

A material that uses a custom Shader program to render visual items (canvas items, meshes, skies, fog), or to process particles. Compared to other materials, ShaderMaterial gives deeper control over the generated shader code. For more information, see the shaders documentation index below.

Multiple ShaderMaterials can use the same shader and configure different values for the shader uniforms.

Note: For performance reasons, the Resource.changed signal is only emitted when the Resource.resource_name changes. Only in editor, it is also emitted for shader changes.

Shaders documentation index

get_shader_parameter(param: StringName) const

set_shader_parameter(param: StringName, value: Variant)

void set_shader(value: Shader)

The Shader program used to render this material.

Variant get_shader_parameter(param: StringName) const 🔗

Returns the current value set for this material of a uniform in the shader.

void set_shader_parameter(param: StringName, value: Variant) 🔗

Changes the value set for this material of a uniform in the shader.

Note: param is case-sensitive and must match the name of the uniform in the code exactly (not the capitalized name in the inspector).

Note: Changes to the shader uniform will be effective on all instances using this ShaderMaterial. To prevent this, use per-instance uniforms with GeometryInstance3D.set_instance_shader_parameter() or duplicate the ShaderMaterial resource using Resource.duplicate(). Per-instance uniforms allow for better shader reuse and are therefore faster, so they should be preferred over duplicating the ShaderMaterial when possible.

Please read the User-contributed notes policy before submitting a comment.

---

## Shader

**URL:** https://docs.godotengine.org/en/stable/classes/class_shader.html

**Contents:**
- Shader
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: VisualShader

A shader implemented in the Godot shading language.

A custom shader program implemented in the Godot shading language, saved with the .gdshader extension.

This class is used by a ShaderMaterial and allows you to write your own custom behavior for rendering visual items or updating particle information. For a detailed explanation and usage, please see the tutorials linked below.

Shaders documentation index

get_default_texture_parameter(name: StringName, index: int = 0) const

get_shader_uniform_list(get_groups: bool = false)

inspect_native_shader_code()

set_default_texture_parameter(name: StringName, texture: Texture, index: int = 0)

Mode MODE_SPATIAL = 0

Mode used to draw all 3D objects.

Mode MODE_CANVAS_ITEM = 1

Mode used to draw all 2D objects.

Mode MODE_PARTICLES = 2

Mode used to calculate particle information on a per-particle basis. Not used for drawing.

Mode used for drawing skies. Only works with shaders attached to Sky objects.

Mode used for setting the color and density of volumetric fog effect.

void set_code(value: String)

Returns the shader's code as the user has written it, not the full generated code used internally.

Texture get_default_texture_parameter(name: StringName, index: int = 0) const 🔗

Returns the texture that is set as default for the specified parameter.

Note: name must match the name of the uniform in the code exactly.

Note: If the sampler array is used use index to access the specified texture.

Mode get_mode() const 🔗

Returns the shader mode for the shader.

Array get_shader_uniform_list(get_groups: bool = false) 🔗

Returns the list of shader uniforms that can be assigned to a ShaderMaterial, for use with ShaderMaterial.set_shader_parameter() and ShaderMaterial.get_shader_parameter(). The parameters returned are contained in dictionaries in a similar format to the ones returned by Object.get_property_list().

If argument get_groups is true, parameter grouping hints are also included in the list.

void inspect_native_shader_code() 🔗

Only available when running in the editor. Opens a popup that visualizes the generated shader code, including all variants and internal shader code. See also Material.inspect_native_shader_code().

void set_default_texture_parameter(name: StringName, texture: Texture, index: int = 0) 🔗

Sets the default texture to be used with a texture uniform. The default is used if a texture is not set in the ShaderMaterial.

Note: name must match the name of the uniform in the code exactly.

Note: If the sampler array is used use index to access the specified texture.

Please read the User-contributed notes policy before submitting a comment.

---

## Shader preprocessor

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/shader_reference/shader_preprocessor.html

**Contents:**
- Shader preprocessor
- Why use a shader preprocessor?
- Directives
  - General syntax
  - #define
  - #undef
  - #if
  - #elif
  - #ifdef
  - #ifndef

In programming languages, a preprocessor allows changing the code before the compiler reads it. Unlike the compiler, the preprocessor does not care about whether the syntax of the preprocessed code is valid. The preprocessor always performs what the directives tell it to do. A directive is a statement starting with a hash symbol (#). It is not a keyword of the shader language (such as if or for), but a special kind of token within the language.

From Godot 4.0 onwards, you can use a shader preprocessor within text-based shaders. The syntax is similar to what most GLSL shader compilers support (which in turn is similar to the C/C++ preprocessor).

The shader preprocessor is not available in visual shaders. If you need to introduce preprocessor statements to a visual shader, you can convert it to a text-based shader using the Convert to Shader option in the VisualShader inspector resource dropdown. This conversion is a one-way operation; text shaders cannot be converted back to visual shaders.

Preprocessor directives do not use brackets ({}), but can use parentheses.

Preprocessor directives never end with semicolons (with the exception of #define, where this is allowed but potentially dangerous).

Preprocessor directives can span several lines by ending each line with a backslash (\). The first line break not featuring a backslash will end the preprocessor statement.

Syntax: #define <identifier> [replacement_code].

Defines the identifier after that directive as a macro, and replaces all successive occurrences of it with the replacement code given in the shader. Replacement is performed on a "whole words" basis, which means no replacement is performed if the string is part of another string (without any spaces or operators separating it).

Defines with replacements may also have one or more arguments, which can then be passed when referencing the define (similar to a function call).

If the replacement code is not defined, the identifier may only be used with #ifdef or #ifndef directives.

If the concatenation symbol (##) is present in the replacement code then it will be removed upon macro insertion, together with any space surrounding it, and join the surrounding words and arguments into a new token.

Compared to constants (const CONSTANT = value;), #define can be used anywhere within the shader (including in uniform hints). #define can also be used to insert arbitrary shader code at any location, while constants can't do that.

Defining a #define for an identifier that is already defined results in an error. To prevent this, use #undef <identifier>.

Syntax: #undef identifier

The #undef directive may be used to cancel a previously defined #define directive:

Without #undef in the above example, there would be a macro redefinition error.

Syntax: #if <condition>

The #if directive checks whether the condition passed. If it evaluates to a non-zero value, the code block is included, otherwise it is skipped.

To evaluate correctly, the condition must be an expression giving a simple floating-point, integer or boolean result. There may be multiple condition blocks connected by && (AND) or || (OR) operators. It may be continued by an #else block, but must be ended with the #endif directive.

Using the defined() preprocessor function, you can check whether the passed identifier is defined a by #define placed above that directive. This is useful for creating multiple shader versions in the same file. It may be continued by an #else block, but must be ended with the #endif directive.

The defined() function's result can be negated by using the ! (boolean NOT) symbol in front of it. This can be used to check whether a define is not set.

Be careful, as defined() must only wrap a single identifier within parentheses, never more:

In the shader editor, preprocessor branches that evaluate to false (and are therefore excluded from the final compiled shader) will appear grayed out. This does not apply to runtime if statements.

#if preprocessor versus if statement: Performance caveats

The shading language supports runtime if statements:

If the uniform is never changed, this behaves identical to the following usage of the #if preprocessor statement:

However, the #if variant can be faster in certain scenarios. This is because all runtime branches in a shader are still compiled and variables within those branches may still take up register space, even if they are never run in practice.

Modern GPUs are quite effective at performing "static" branching. "Static" branching refers to if statements where all pixels/vertices evaluate to the same result in a given shader invocation. However, high amounts of VGPRs (which can be caused by having too many branches) can still slow down shader execution significantly.

The #elif directive stands for "else if" and checks the condition passed if the above #if evaluated to false. #elif can only be used within an #if block. It is possible to use several #elif statements after an #if statement.

Like with #if, the defined() preprocessor function can be used:

Syntax: #ifdef <identifier>

This is a shorthand for #if defined(...). Checks whether the passed identifier is defined by #define placed above that directive. This is useful for creating multiple shader versions in the same file. It may be continued by an #else block, but must be ended with the #endif directive.

The processor does not support #elifdef as a shortcut for #elif defined(...). Instead, use the following series of #ifdef and #else when you need more than two branches:

Syntax: #ifndef <identifier>

This is a shorthand for #if !defined(...). Similar to #ifdef, but checks whether the passed identifier is not defined by #define before that directive.

This is the exact opposite of #ifdef; it will always match in situations where #ifdef would never match, and vice versa.

Defines the optional block which is included when the previously defined #if, #elif, #ifdef or #ifndef directive evaluates to false.

Used as terminator for the #if, #ifdef, #ifndef or subsequent #else directives.

Syntax: #error <message>

The #error directive forces the preprocessor to emit an error with optional message. For example, it's useful when used within #if block to provide a strict limitation of the defined value.

Syntax: #include "path"

The #include directive includes the entire content of a shader include file in a shader. "path" can be an absolute res:// path or relative to the current shader file. Relative paths are only allowed in shaders that are saved to .gdshader or .gdshaderinc files, while absolute paths can be used in shaders that are built into a scene/resource file.

You can create new shader includes by using the File > Create Shader Include menu option of the shader editor, or by creating a new ShaderInclude resource in the FileSystem dock.

Shader includes can be included from within any shader, or other shader include, at any point in the file.

When including shader includes in the global scope of a shader, it is recommended to do this after the initial shader_type statement.

You can also include shader includes from within the body a function. Please note that the shader editor is likely going to report errors for your shader include's code, as it may not be valid outside of the context that it was written for. You can either choose to ignore these errors (the shader will still compile fine), or you can wrap the include in an #ifdef block that checks for a define from your shader.

#include is useful for creating libraries of helper functions (or macros) and reducing code duplication. When using #include, be careful about naming collisions, as redefining functions or macros is not allowed.

#include is subject to several restrictions:

Only shader include resources (ending with .gdshaderinc) can be included. .gdshader files cannot be included by another shader, but a .gdshaderinc file can include other .gdshaderinc files.

Cyclic dependencies are not allowed and will result in an error.

To avoid infinite recursion, include depth is limited to 25 steps.

Example shader include file:

Example base shader (using the include file we created above):

Syntax: #pragma value

The #pragma directive provides additional information to the preprocessor or compiler.

Currently, it may have only one value: disable_preprocessor. If you don't need the preprocessor, use that directive to speed up shader compilation by excluding the preprocessor step.

Since Godot 4.4, you can check which renderer is currently used with the built-in defines CURRENT_RENDERER, RENDERER_COMPATIBILITY, RENDERER_MOBILE, and RENDERER_FORWARD_PLUS:

CURRENT_RENDERER is set to either 0, 1, or 2 depending on the current renderer.

RENDERER_COMPATIBILITY is always 0.

RENDERER_MOBILE is always 1.

RENDERER_FORWARD_PLUS is always 2.

As an example, this shader sets ALBEDO to a different color in each renderer:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (cpp):
```cpp
uniform sampler2D material0;

#define SAMPLE(N) vec4 tex##N = texture(material##N, UV)

void fragment() {
    SAMPLE(0);
    ALBEDO = tex0.rgb;
}
```

Example 2 (julia):
```julia
shader_type spatial;

// Notice the lack of semicolon at the end of the line, as the replacement text
// shouldn't insert a semicolon on its own.
// If the directive ends with a semicolon, the semicolon is inserted in every usage
// of the directive, even when this causes a syntax error.
#define USE_MY_COLOR
#define MY_COLOR vec3(1, 0, 0)

// Replacement with arguments.
// All arguments are required (no default values can be provided).
#define BRIGHTEN_COLOR(r, g, b) vec3(r + 0.5, g + 0.5, b + 0.5)

// Multiline replacement using backslashes for continuation:
#define SAMPLE(param1, param2, param3, param4) long_function_call( \
        param1, \
        param2, \
        param3, \
        param4 \
)

void fragment() {
#ifdef USE_MY_COLOR
    ALBEDO = MY_COLOR;
#endif
}
```

Example 3 (unknown):
```unknown
#define MY_COLOR vec3(1, 0, 0)

vec3 get_red_color() {
    return MY_COLOR;
}

#undef MY_COLOR
#define MY_COLOR vec3(0, 1, 0)

vec3 get_green_color() {
    return MY_COLOR;
}

// Like in most preprocessors, undefining a define that was not previously defined is allowed
// (and won't print any warning or error).
#undef THIS_DOES_NOT_EXIST
```

Example 4 (unknown):
```unknown
#define VAR 3
#define USE_LIGHT 0 // Evaluates to `false`.
#define USE_COLOR 1 // Evaluates to `true`.

#if VAR == 3 && (USE_LIGHT || USE_COLOR)
// Condition is `true`. Include this portion in the final shader.
#endif
```

---

## Sky

**URL:** https://docs.godotengine.org/en/stable/classes/class_sky.html

**Contents:**
- Sky
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Defines a 3D environment's background by using a Material.

The Sky class uses a Material to render a 3D environment's background and the light it emits by updating the reflection/radiance cubemaps.

RadianceSize RADIANCE_SIZE_32 = 0

Radiance texture size is 32×32 pixels.

RadianceSize RADIANCE_SIZE_64 = 1

Radiance texture size is 64×64 pixels.

RadianceSize RADIANCE_SIZE_128 = 2

Radiance texture size is 128×128 pixels.

RadianceSize RADIANCE_SIZE_256 = 3

Radiance texture size is 256×256 pixels.

RadianceSize RADIANCE_SIZE_512 = 4

Radiance texture size is 512×512 pixels.

RadianceSize RADIANCE_SIZE_1024 = 5

Radiance texture size is 1024×1024 pixels.

RadianceSize RADIANCE_SIZE_2048 = 6

Radiance texture size is 2048×2048 pixels.

RadianceSize RADIANCE_SIZE_MAX = 7

Represents the size of the RadianceSize enum.

ProcessMode PROCESS_MODE_AUTOMATIC = 0

Automatically selects the appropriate process mode based on your sky shader. If your shader uses TIME or POSITION, this will use PROCESS_MODE_REALTIME. If your shader uses any of the LIGHT_* variables or any custom uniforms, this uses PROCESS_MODE_INCREMENTAL. Otherwise, this defaults to PROCESS_MODE_QUALITY.

ProcessMode PROCESS_MODE_QUALITY = 1

Uses high quality importance sampling to process the radiance map. In general, this results in much higher quality than PROCESS_MODE_REALTIME but takes much longer to generate. This should not be used if you plan on changing the sky at runtime. If you are finding that the reflection is not blurry enough and is showing sparkles or fireflies, try increasing ProjectSettings.rendering/reflections/sky_reflections/ggx_samples.

ProcessMode PROCESS_MODE_INCREMENTAL = 2

Uses the same high quality importance sampling to process the radiance map as PROCESS_MODE_QUALITY, but updates over several frames. The number of frames is determined by ProjectSettings.rendering/reflections/sky_reflections/roughness_layers. Use this when you need highest quality radiance maps, but have a sky that updates slowly.

ProcessMode PROCESS_MODE_REALTIME = 3

Uses the fast filtering algorithm to process the radiance map. In general this results in lower quality, but substantially faster run times. If you need better quality, but still need to update the sky every frame, consider turning on ProjectSettings.rendering/reflections/sky_reflections/fast_filter_high_quality.

Note: The fast filtering algorithm is limited to 256×256 cubemaps, so radiance_size must be set to RADIANCE_SIZE_256. Otherwise, a warning is printed and the overridden radiance size is ignored.

ProcessMode process_mode = 0 🔗

void set_process_mode(value: ProcessMode)

ProcessMode get_process_mode()

The method for generating the radiance map from the sky. The radiance map is a cubemap with increasingly blurry versions of the sky corresponding to different levels of roughness. Radiance maps can be expensive to calculate.

RadianceSize radiance_size = 3 🔗

void set_radiance_size(value: RadianceSize)

RadianceSize get_radiance_size()

The Sky's radiance map size. The higher the radiance map size, the more detailed the lighting from the Sky will be.

Note: Some hardware will have trouble with higher radiance sizes, especially RADIANCE_SIZE_512 and above. Only use such high values on high-end hardware.

Material sky_material 🔗

void set_material(value: Material)

Material get_material()

Material used to draw the background. Can be PanoramaSkyMaterial, ProceduralSkyMaterial, PhysicalSkyMaterial, or even a ShaderMaterial if you want to use your own custom shader.

Please read the User-contributed notes policy before submitting a comment.

---

## Sky shaders

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/shader_reference/sky_shader.html

**Contents:**
- Sky shaders
- Render modes
- Built-ins
- Global built-ins
- Sky built-ins
- User-contributed notes

Sky shaders are a special type of shader used for drawing sky backgrounds and for updating radiance cubemaps which are used for image-based lighting (IBL). Sky shaders only have one processing function, the sky() function.

There are three places the sky shader is used.

First the sky shader is used to draw the sky when you have selected to use a Sky as the background in your scene.

Second, the sky shader is used to update the radiance cubemap when using the Sky for ambient color or reflections.

Third, the sky shader is used to draw the lower res subpasses which can be used in the high-res background or cubemap pass.

In total, this means the sky shader can run up to six times per frame, however, in practice it will be much less than that because the radiance cubemap does not need to be updated every frame, and not all subpasses will be used. You can change the behavior of the shader based on where it is called by checking the AT_*_PASS booleans. For example:

When using the sky shader to draw a background, the shader will be called for all non-occluded fragments on the screen. However, for the background's subpasses, the shader will be called for every pixel of the subpass.

When using the sky shader to update the radiance cubemap, the sky shader will be called for every pixel in the cubemap. On the other hand, the shader will only be called when the radiance cubemap needs to be updated. The radiance cubemap needs to be updated when any of the shader parameters are updated. For example, if TIME is used in the shader, then the radiance cubemap will update every frame. The following list of changes force an update of the radiance cubemap:

POSITION is used and the camera position changes.

If any LIGHTX_* properties are used and any DirectionalLight3D changes.

If any uniform is changed in the shader.

If the screen is resized and either of the subpasses are used.

Try to avoid updating the radiance cubemap needlessly. If you do need to update the radiance cubemap each frame, make sure your Sky process mode is set to PROCESS_MODE_REALTIME.

Note that the process mode only affects the rendering of the radiance cubemap. The visible sky is always rendered by calling the fragment shader for every pixel. With complex fragment shaders, this can result in a high rendering overhead. If the sky is static (the conditions listed above are met) or changes slowly, running the full fragment shader every frame is not needed. This can be avoided by rendering the full sky into the radiance cubemap, and reading from this cubemap when rendering the visible sky. With a completely static sky, this means that it needs to be rendered only once.

The following code renders the full sky into the radiance cubemap and reads from that cubemap for displaying the visible sky:

This way, the complex calculations happen only in the cubemap pass, which can be optimized by setting the sky's process mode and the radiance size to get the desired balance between performance and visual fidelity.

Subpasses allow you to do more expensive calculations at a lower resolution to speed up your shaders. For example the following code renders clouds at a lower resolution than the rest of the sky:

Allows the shader to write to and access the half resolution pass.

Allows the shader to write to and access the quarter resolution pass.

If used, fog will not affect the sky.

Values marked as in are read-only. Values marked as out can optionally be written to and will not necessarily contain sensible values. Samplers cannot be written to so they are not marked.

Global built-ins are available everywhere, including in custom functions.

There are 4 LIGHTX lights, accessed as LIGHT0, LIGHT1, LIGHT2, and LIGHT3.

Global time since the engine has started, in seconds. It repeats after every 3,600 seconds (which can be changed with the rollover setting). It's affected by time_scale but not by pausing. If you need a TIME variable that is not affected by time scale, add your own global shader uniform and update it each frame.

Camera position, in world space.

Radiance cubemap. Can only be read from during background pass. Check !AT_CUBEMAP_PASS before using.

in bool AT_HALF_RES_PASS

true when rendering to half resolution pass.

in bool AT_QUARTER_RES_PASS

true when rendering to quarter resolution pass.

in bool AT_CUBEMAP_PASS

true when rendering to radiance cubemap.

in bool LIGHTX_ENABLED

true if LIGHTX is visible and in the scene. If false, other light properties may be garbage.

in float LIGHTX_ENERGY

Energy multiplier for LIGHTX.

in vec3 LIGHTX_DIRECTION

Direction that LIGHTX is facing.

Angular diameter of LIGHTX in the sky. Expressed in radians. For reference, the sun from earth is about .0087 radians (0.5 degrees).

A PI constant (3.141592). A ratio of a circle's circumference to its diameter and amount of radians in half turn.

A TAU constant (6.283185). An equivalent of PI * 2 and amount of radians in full turn.

An E constant (2.718281). Euler's number and a base of the natural logarithm.

Normalized direction of current pixel. Use this as your basic direction for procedural effects.

Screen UV coordinate for current pixel. Used to map a texture to the full screen.

Sphere UV. Used to map a panorama texture to the sky.

in vec4 HALF_RES_COLOR

Color value of corresponding pixel from half resolution pass. Uses linear filter.

in vec4 QUARTER_RES_COLOR

Color value of corresponding pixel from quarter resolution pass. Uses linear filter.

Output alpha value, can only be used in subpasses.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (cpp):
```cpp
shader_type sky;

void sky() {
    if (AT_CUBEMAP_PASS) {
        // Sets the radiance cubemap to a nice shade of blue instead of doing
        // expensive sky calculations
        COLOR = vec3(0.2, 0.6, 1.0);
    } else {
        // Do expensive sky calculations for background sky only
        COLOR = get_sky_color(EYEDIR);
    }
}
```

Example 2 (cpp):
```cpp
shader_type sky;

void sky() {
    if (AT_CUBEMAP_PASS) {
        vec3 dir = EYEDIR;

        vec4 col = vec4(0.0);

        // Complex color calculation

        COLOR = col.xyz;
        ALPHA = 1.0;
    } else {
        COLOR = texture(RADIANCE, EYEDIR).rgb;
    }
}
```

Example 3 (cpp):
```cpp
shader_type sky;
render_mode use_half_res_pass;

void sky() {
    if (AT_HALF_RES_PASS) {
        // Run cloud calculation for 1/4 of the pixels
        vec4 color = generate_clouds(EYEDIR);
        COLOR = color.rgb;
        ALPHA = color.a;
    } else {
        // At full resolution pass, blend sky and clouds together
        vec3 color = generate_sky(EYEDIR);
        COLOR = color + HALF_RES_COLOR.rgb * HALF_RES_COLOR.a;
    }
}
```

---

## TextureCubemapArrayRD

**URL:** https://docs.godotengine.org/en/stable/classes/class_texturecubemaparrayrd.html

**Contents:**
- TextureCubemapArrayRD
- Description
- User-contributed notes

Inherits: TextureLayeredRD < TextureLayered < Texture < Resource < RefCounted < Object

Texture Array for Cubemaps that is bound to a texture created on the RenderingDevice.

This texture class allows you to use a cubemap array texture created directly on the RenderingDevice as a texture for materials, meshes, etc.

Please read the User-contributed notes policy before submitting a comment.

---

## TextureCubemapRD

**URL:** https://docs.godotengine.org/en/stable/classes/class_texturecubemaprd.html

**Contents:**
- TextureCubemapRD
- Description
- User-contributed notes

Inherits: TextureLayeredRD < TextureLayered < Texture < Resource < RefCounted < Object

Texture for Cubemap that is bound to a texture created on the RenderingDevice.

This texture class allows you to use a cubemap texture created directly on the RenderingDevice as a texture for materials, meshes, etc.

Please read the User-contributed notes policy before submitting a comment.

---

## The Compositor

**URL:** https://docs.godotengine.org/en/stable/tutorials/rendering/compositor.html

**Contents:**
- The Compositor
- Compositor effects
- User-contributed notes

The compositor is a new feature in Godot 4 that allows control over the rendering pipeline when rendering the contents of a Viewport.

It can be configured on a WorldEnvironment node where it applies to all Viewports, or it can be configured on a Camera3D and apply only to the Viewport using that camera.

The Compositor resource is used to configure the compositor. To get started, create a new compositor on the appropriate node:

The compositor is currently a feature that is only supported by the Mobile and Forward+ renderers.

Compositor effects allow you to insert additional logic into the rendering pipeline at various stages. This is an advanced feature that requires a high level of understanding of the rendering pipeline to use to its best advantage.

As the core logic of the compositor effect is called from the rendering pipeline it is important to note that this logic will thus run within the thread on which rendering takes place. Care needs to be taken to ensure we don't run into threading issues.

To illustrate how to use compositor effects we'll create a simple post processing effect that allows you to write your own shader code and apply this full screen through a compute shader. You can find the finished demo project here.

We start by creating a new script called post_process_shader.gd. We'll make this a tool script so we can see the compositor effect work in the editor. We need to extend our node from CompositorEffect. We must also give our script a class name.

Next we're going to define a constant for our shader template code. This is the boilerplate code that makes our compute shader work.

For more information on how compute shaders work, please check Using compute shaders.

The important bit here is that for every pixel on our screen, our main function is executed and inside of this we load the current color value of our pixel, execute our user code, and write our modified color back to our color image.

#COMPUTE_CODE gets replaced by our user code.

In order to set our user code, we need an export variable. We'll also define a few script variables we'll be using:

Note the use of a Mutex in our code. Most of our implementation gets called from the rendering engine and thus runs within our rendering thread.

We need to ensure that we set our new shader code, and mark our shader code as dirty, without our render thread accessing this data at the same time.

Next we initialize our effect.

The main thing here is setting our effect_callback_type which tells the rendering engine at what stage of the render pipeline to call our code.

Currently we only have access to the stages of the 3D rendering pipeline!

We also get a reference to our rendering device, which will come in very handy.

We also need to clean up after ourselves, for this we react to the NOTIFICATION_PREDELETE notification:

Note that we do not use our mutex here even though we create our shader inside of our render thread. The methods on our rendering server are thread safe and free_rid will be postponed cleaning up the shader until after any frames currently being rendered are finished.

Also note that we are not freeing our pipeline. The rendering device does dependency tracking and as the pipeline is dependent on the shader, it will be automatically freed when the shader is destructed.

From this point onwards our code will run on the rendering thread.

Our next step is a helper function that will recompile the shader if the user code was changed.

At the top of this method we again use our mutex to protect accessing our user shader code and our is dirty flag. We make a local copy of the user shader code if our user shader code is dirty.

If we don't have a new code fragment, we return true if we already have a valid pipeline.

If we do have a new code fragment we embed it in our template code and then compile it.

The code shown here compiles our new code in runtime. This is great for prototyping as we can immediately see the effect of the changed shader.

This prevents precompiling and caching this shader which may be an issues on some platforms such as consoles. Note that the demo project comes with an alternative example where a glsl file contains the entire compute shader and this is used. Godot is able to precompile and cache the shader with this approach.

Finally we need to implement our effect callback, the rendering engine will call this at the right stage of rendering.

At the start of this method we check if we have a rendering device, if our callback type is the correct one, and check if we have our shader.

The check for the effect type is only a safety mechanism. We've set this in our _init function, however it is possible for the user to change this in the UI.

Our p_render_data parameter gives us access to an object that holds data specific to the frame we're currently rendering. We're currently only interested in our render scene buffers, which provide us access to all the internal buffers used by the rendering engine. Note that we cast this to RenderSceneBuffersRD to expose the full API to this data.

Next we obtain our internal size which is the resolution of our 3D render buffers before they are upscaled (if applicable), upscaling happens after our post processes have run.

From our internal size we calculate our group size, see our local size in our template shader.

We also populate our push constant so our shader knows our size. Godot does not support structs here yet so we use a PackedFloat32Array to store this data into. Note that we have to pad this array with a 16 byte alignment. In other words, the length of our array needs to be a multiple of 4.

Now we loop through our views, this is in case we're using multiview rendering which is applicable for stereo rendering (XR). In most cases we will only have one view.

There is no performance benefit to use multiview for post processing here, handling the views separately like this will still enable the GPU to use parallelism if beneficial.

Next we obtain the color buffer for this view. This is the buffer into which our 3D scene has been rendered.

We then prepare a uniform set so we can communicate the color buffer to our shader.

Note the use of our UniformSetCacheRD cache which ensures we can check for our uniform set each frame. As our color buffer can change from frame to frame and our uniform cache will automatically clean up uniform sets when buffers are freed, this is the safe way to ensure we do not leak memory or use an outdated set.

Finally we build our compute list by binding our pipeline, binding our uniform set, pushing our push constant data, and calling dispatch for our groups.

With our compositor effect completed, we now need to add it to our compositor.

On our compositor we expand the compositor effects property and press Add Element.

Now we can add our compositor effect:

After selecting our PostProcessShader we need to set our user shader code:

With that all done, our output is in grayscale.

For a more advanced example of post effects, check out the Radial blur based sky rays example project created by Bastiaan Olij.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
@tool
extends CompositorEffect
class_name PostProcessShader
```

Example 2 (typescript):
```typescript
const template_shader: String = """
#version 450

// Invocations in the (x, y, z) dimension
layout(local_size_x = 8, local_size_y = 8, local_size_z = 1) in;

layout(rgba16f, set = 0, binding = 0) uniform image2D color_image;

// Our push constant
layout(push_constant, std430) uniform Params {
    vec2 raster_size;
    vec2 reserved;
} params;

// The code we want to execute in each invocation
void main() {
    ivec2 uv = ivec2(gl_GlobalInvocationID.xy);
    ivec2 size = ivec2(params.raster_size);

    if (uv.x >= size.x || uv.y >= size.y) {
        return;
    }

    vec4 color = imageLoad(color_image, uv);

    #COMPUTE_CODE

    imageStore(color_image, uv, color);
}
"""
```

Example 3 (swift):
```swift
@export_multiline var shader_code: String = "":
    set(value):
        mutex.lock()
        shader_code = value
        shader_is_dirty = true
        mutex.unlock()

var rd: RenderingDevice
var shader: RID
var pipeline: RID

var mutex: Mutex = Mutex.new()
var shader_is_dirty: bool = true
```

Example 4 (typescript):
```typescript
# Called when this resource is constructed.
func _init():
    effect_callback_type = EFFECT_CALLBACK_TYPE_POST_TRANSPARENT
    rd = RenderingServer.get_rendering_device()
```

---

## UniformSetCacheRD

**URL:** https://docs.godotengine.org/en/stable/classes/class_uniformsetcacherd.html

**Contents:**
- UniformSetCacheRD
- Description
- Methods
- Method Descriptions
- User-contributed notes

Uniform set cache manager for Rendering Device based renderers.

Uniform set cache manager for Rendering Device based renderers. Provides a way to create a uniform set and reuse it in subsequent calls for as long as the uniform set exists. Uniform set will automatically be cleaned up when dependent objects are freed.

get_cache(shader: RID, set: int, uniforms: Array[RDUniform]) static

RID get_cache(shader: RID, set: int, uniforms: Array[RDUniform]) static 🔗

Creates/returns a cached uniform set based on the provided uniforms for a given shader.

Please read the User-contributed notes policy before submitting a comment.

---

## Using compute shaders

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/compute_shaders.html

**Contents:**
- Using compute shaders
- Create a local RenderingDevice
- Provide input data
- Defining a compute pipeline
- Execute a compute shader
- Retrieving results
- Freeing memory
- User-contributed notes

This tutorial will walk you through the process of creating a minimal compute shader. But first, a bit of background on compute shaders and how they work with Godot.

This tutorial assumes you are familiar with shaders generally. If you are new to shaders please read Introduction to shaders and your first shader before proceeding with this tutorial.

A compute shader is a special type of shader program that is orientated towards general purpose programming. In other words, they are more flexible than vertex shaders and fragment shaders as they don't have a fixed purpose (i.e. transforming vertices or writing colors to an image). Unlike fragment shaders and vertex shaders, compute shaders have very little going on behind the scenes. The code you write is what the GPU runs and very little else. This can make them a very useful tool to offload heavy calculations to the GPU.

Now let's get started by creating a short compute shader.

First, in the external text editor of your choice, create a new file called compute_example.glsl in your project folder. When you write compute shaders in Godot, you write them in GLSL directly. The Godot shader language is based on GLSL. If you are familiar with normal shaders in Godot, the syntax below will look somewhat familiar.

Compute shaders can only be used from RenderingDevice-based renderers (the Forward+ or Mobile renderer). To follow along with this tutorial, ensure that you are using the Forward+ or Mobile renderer. The setting for which is located in the top right-hand corner of the editor.

Note that compute shader support is generally poor on mobile devices (due to driver bugs), even if they are technically supported.

Let's take a look at this compute shader code:

This code takes an array of floats, multiplies each element by 2 and store the results back in the buffer array. Now let's look at it line-by-line.

These two lines communicate two things:

The following code is a compute shader. This is a Godot-specific hint that is needed for the editor to properly import the shader file.

The code is using GLSL version 450.

You should never have to change these two lines for your custom compute shaders.

Next, we communicate the number of invocations to be used in each workgroup. Invocations are instances of the shader that are running within the same workgroup. When we launch a compute shader from the CPU, we tell it how many workgroups to run. Workgroups run in parallel to each other. While running one workgroup, you cannot access information in another workgroup. However, invocations in the same workgroup can have some limited access to other invocations.

Think about workgroups and invocations as a giant nested for loop.

Workgroups and invocations are an advanced topic. For now, remember that we will be running two invocations per workgroup.

Here we provide information about the memory that the compute shader will have access to. The layout property allows us to tell the shader where to look for the buffer, we will need to match these set and binding positions from the CPU side later.

The restrict keyword tells the shader that this buffer is only going to be accessed from one place in this shader. In other words, we won't bind this buffer in another set or binding index. This is important as it allows the shader compiler to optimize the shader code. Always use restrict when you can.

This is an unsized buffer, which means it can be any size. So we need to be careful not to read from an index larger than the size of the buffer.

Finally, we write the main function which is where all the logic happens. We access a position in the storage buffer using the gl_GlobalInvocationID built-in variables. gl_GlobalInvocationID gives you the global unique ID for the current invocation.

To continue, write the code above into your newly created compute_example.glsl file.

To interact with and execute a compute shader, we need a script. Create a new script in the language of your choice and attach it to any Node in your scene.

Now to execute our shader we need a local RenderingDevice which can be created using the RenderingServer:

After that, we can load the newly created shader file compute_example.glsl and create a precompiled version of it using this:

Local RenderingDevices cannot be debugged using tools such as RenderDoc.

As you might remember, we want to pass an input array to our shader, multiply each element by 2 and get the results.

We need to create a buffer to pass values to a compute shader. We are dealing with an array of floats, so we will use a storage buffer for this example. A storage buffer takes an array of bytes and allows the CPU to transfer data to and from the GPU.

So let's initialize an array of floats and create a storage buffer:

With the buffer in place we need to tell the rendering device to use this buffer. To do that we will need to create a uniform (like in normal shaders) and assign it to a uniform set which we can pass to our shader later.

The next step is to create a set of instructions our GPU can execute. We need a pipeline and a compute list for that.

The steps we need to do to compute our result are:

Create a new pipeline.

Begin a list of instructions for our GPU to execute.

Bind our compute list to our pipeline

Bind our buffer uniform to our pipeline

Specify how many workgroups to use

End the list of instructions

Note that we are dispatching the compute shader with 5 work groups in the X axis, and one in the others. Since we have 2 local invocations in the X axis (specified in our shader), 10 compute shader invocations will be launched in total. If you read or write to indices outside of the range of your buffer, you may access memory outside of your shaders control or parts of other variables which may cause issues on some hardware.

After all of this we are almost done, but we still need to execute our pipeline. So far we have only recorded what we would like the GPU to do; we have not actually run the shader program.

To execute our compute shader we need to submit the pipeline to the GPU and wait for the execution to finish:

Ideally, you would not call sync() to synchronize the RenderingDevice right away as it will cause the CPU to wait for the GPU to finish working. In our example, we synchronize right away because we want our data available for reading right away. In general, you will want to wait at least 2 or 3 frames before synchronizing so that the GPU is able to run in parallel with the CPU.

Long computations can cause Windows graphics drivers to "crash" due to TDR being triggered by Windows. This is a mechanism that reinitializes the graphics driver after a certain amount of time has passed without any activity from the graphics driver (usually 5 to 10 seconds).

Depending on the duration your compute shader takes to execute, you may need to split it into multiple dispatches to reduce the time each dispatch takes and reduce the chances of triggering a TDR. Given TDR is time-dependent, slower GPUs may be more prone to TDRs when running a given compute shader compared to a faster GPU.

You may have noticed that, in the example shader, we modified the contents of the storage buffer. In other words, the shader read from our array and stored the data in the same array again so our results are already there. Let's retrieve the data and print the results to our console.

The buffer, pipeline, and uniform_set variables we've been using are each an RID. Because RenderingDevice is meant to be a lower-level API, RIDs aren't freed automatically. This means that once you're done using buffer or any other RID, you are responsible for freeing its memory manually using the RenderingDevice's free_rid() method.

With that, you have everything you need to get started working with compute shaders.

The demo projects repository contains a Compute Shader Heightmap demo This project performs heightmap image generation on the CPU and GPU separately, which lets you compare how a similar algorithm can be implemented in two different ways (with the GPU implementation being faster in most cases).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (cpp):
```cpp
#[compute]
#version 450

// Invocations in the (x, y, z) dimension
layout(local_size_x = 2, local_size_y = 1, local_size_z = 1) in;

// A binding to the buffer we create in our script
layout(set = 0, binding = 0, std430) restrict buffer MyDataBuffer {
    float data[];
}
my_data_buffer;

// The code we want to execute in each invocation
void main() {
    // gl_GlobalInvocationID.x uniquely identifies this invocation across all work groups
    my_data_buffer.data[gl_GlobalInvocationID.x] *= 2.0;
}
```

Example 2 (unknown):
```unknown
#[compute]
#version 450
```

Example 3 (unknown):
```unknown
// Invocations in the (x, y, z) dimension
layout(local_size_x = 2, local_size_y = 1, local_size_z = 1) in;
```

Example 4 (unknown):
```unknown
for (int x = 0; x < workgroup_size_x; x++) {
  for (int y = 0; y < workgroup_size_y; y++) {
     for (int z = 0; z < workgroup_size_z; z++) {
        // Each workgroup runs independently and in parallel.
        for (int local_x = 0; local_x < invocation_size_x; local_x++) {
           for (int local_y = 0; local_y < invocation_size_y; local_y++) {
              for (int local_z = 0; local_z < invocation_size_z; local_z++) {
                 // Compute shader runs here.
              }
           }
        }
     }
  }
}
```

---

## Using Viewports

**URL:** https://docs.godotengine.org/en/stable/tutorials/rendering/viewports.html

**Contents:**
- Using Viewports
- Introduction
- Input
- Listener
- Cameras (2D & 3D)
- Scale & stretching
- Worlds
- Capture
- Viewport Container
- Rendering

Think of a Viewport as a screen onto which the game is projected. In order to see the game, we need to have a surface on which to draw it. That surface is the Root Viewport.

SubViewports are a kind of Viewport that can be added to the scene so that there are multiple surfaces to draw on. When we are drawing to a SubViewport, we call it a render target. We can access the contents of a render target by accessing its corresponding texture. By using a SubViewport as render target, we can either render multiple scenes simultaneously or we can render to a ViewportTexture which is applied to an object in the scene, for example a dynamic skybox.

SubViewports have a variety of use cases, including:

Rendering 3D objects within a 2D game

Rendering 2D elements in a 3D game

Rendering dynamic textures

Generating procedural textures at runtime

Rendering multiple cameras in the same scene

What all these use cases have in common is that you are given the ability to draw objects to a texture as if it were another screen and can then choose what to do with the resulting texture.

Another kind of Viewports in Godot are Windows. They allow their content to be projected onto a window. While the Root Viewport is a Window, they are less flexible. If you want to use the texture of a Viewport, you'll be working with SubViewports most of the time.

Viewports are also responsible for delivering properly adjusted and scaled input events to their children nodes. By default SubViewports don't automatically receive input, unless they receive it from their direct SubViewportContainer parent node. In this case, input can be disabled with the Disable Input property.

For more information on how Godot handles input, please read the Input Event Tutorial.

Godot supports 3D sound (in both 2D and 3D nodes). More on this can be found in the Audio Streams Tutorial. For this type of sound to be audible, the Viewport needs to be enabled as a listener (for 2D or 3D). If you are using a SubViewport to display your World3D or World2D, don't forget to enable this!

When using a Camera3D or Camera2D, it will always display on the closest parent Viewport (going towards the root). For example, in the following hierarchy:

CameraA will display on the Root Viewport and it will draw MeshA. CameraB will be captured by the SubViewport along with MeshB. Even though MeshB is in the scene hierarchy, it will still not be drawn to the Root Viewport. Similarly, MeshA will not be visible from the SubViewport because SubViewports only capture nodes below them in the hierarchy.

There can only be one active camera per Viewport, so if there is more than one, make sure that the desired one has the current property set, or make it the current camera by calling:

By default, cameras will render all objects in their world. In 3D, cameras can use their cull_mask property combined with the VisualInstance3D's layer property to restrict which objects are rendered.

SubViewports have a size property, which represents the size of the SubViewport in pixels. For SubViewports which are children of SubViewportContainers, these values are overridden, but for all others, this sets their resolution.

It is also possible to scale the 2D content and make the SubViewport resolution different from the one specified in size, by calling:

For information on scaling and stretching with the Root Viewport visit the Multiple Resolutions Tutorial

For 3D, a Viewport will contain a World3D. This is basically the universe that links physics and rendering together. Node3D-based nodes will register using the World3D of the closest Viewport. By default, newly created Viewports do not contain a World3D but use the same as their parent Viewport. The Root Viewport always contains a World3D, which is the one objects are rendered to by default.

A World3D can be set in a Viewport using the World 3D property, that will separate all children nodes of this Viewport and will prevent them from interacting with the parent Viewport's World3D. This is especially useful in scenarios where, for example, you might want to show a separate character in 3D imposed over the game (like in StarCraft).

As a helper for situations where you want to create Viewports that display single objects and don't want to create a World3D, Viewport has the option to use its Own World3D. This is useful when you want to instance 3D characters or objects in World2D.

For 2D, each Viewport always contains its own World2D. This suffices in most cases, but in case sharing them may be desired, it is possible to do so by setting world_2d on the Viewport through code.

For an example of how this works, see the demo projects 3D in 2D and 2D in 3D respectively.

It is possible to query a capture of the Viewport contents. For the Root Viewport, this is effectively a screen capture. This is done with the following code:

But if you use this in _ready() or from the first frame of the Viewport's initialization, you will get an empty texture because there is nothing to get as texture. You can deal with it using (for example):

If the SubViewport is a child of a SubViewportContainer, it will become active and display anything it has inside. The layout looks like this:

The SubViewport will cover the area of its parent SubViewportContainer completely if Stretch is set to true in the SubViewportContainer.

The size of the SubViewportContainer cannot be smaller than the size of the SubViewport.

Due to the fact that the Viewport is an entryway into another rendering surface, it exposes a few rendering properties that can be different from the project settings. You can choose to use a different level of MSAA for each Viewport. The default behavior is Disabled.

If you know that the Viewport is only going to be used for 2D, you can Disable 3D. Godot will then restrict how the Viewport is drawn. Disabling 3D is slightly faster and uses less memory compared to enabled 3D. It's a good idea to disable 3D if your viewport doesn't render anything in 3D.

If you need to render 3D shadows in the viewport, make sure to set the viewport's positional_shadow_atlas_size property to a value higher than 0. Otherwise, shadows won't be rendered. By default, the equivalent project setting is set to 4096 on desktop platforms and 2048 on mobile platforms.

Godot also provides a way of customizing how everything is drawn inside Viewports using Debug Draw. Debug Draw allows you to specify a mode which determines how the Viewport will display things drawn inside it. Debug Draw is Disabled by default. Some other options are Unshaded, Overdraw, and Wireframe. For a full list, refer to the Viewport Documentation.

Debug Draw = Disabled (default): The scene is drawn normally.

Debug Draw = Unshaded: Unshaded draws the scene without using lighting information so all the objects appear flatly colored in their albedo color.

Debug Draw = Overdraw: Overdraw draws the meshes semi-transparent with an additive blend so you can see how the meshes overlap.

Debug Draw = Wireframe: Wireframe draws the scene using only the edges of triangles in the meshes.

Debug Draw modes are currently not supported when using the Compatibility rendering method. They will appear as regular draw modes.

When rendering to a SubViewport, whatever is inside will not be visible in the scene editor. To display the contents, you have to draw the SubViewport's ViewportTexture somewhere. This can be requested via code using (for example):

Or it can be assigned in the editor by selecting "New ViewportTexture"

and then selecting the Viewport you want to use.

Every frame, the Viewport's texture is cleared away with the default clear color (or a transparent color if Transparent BG is set to true). This can be changed by setting Clear Mode to Never or Next Frame. As the name implies, Never means the texture will never be cleared, while next frame will clear the texture on the next frame and then set itself to Never.

By default, re-rendering of the SubViewport happens when its ViewportTexture has been drawn in a frame. If visible, it will be rendered, otherwise, it will not. This behavior can be changed by setting Update Mode to Never, Once, Always, or When Parent Visible. Never and Always will never or always re-render respectively. Once will re-render the next frame and change to Never afterwards. This can be used to manually update the Viewport. This flexibility allows users to render an image once and then use the texture without incurring the cost of rendering every frame.

Make sure to check the Viewport demos. They are available in the viewport folder of the demos archive, or at https://github.com/godotengine/godot-demo-projects/tree/master/viewport.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
camera.make_current()
```

Example 2 (unknown):
```unknown
camera.MakeCurrent();
```

Example 3 (unknown):
```unknown
sub_viewport.set_size_2d_override(Vector2i(width, height)) # Custom size for 2D.
sub_viewport.set_size_2d_override_stretch(true) # Enable stretch for custom size.
```

Example 4 (unknown):
```unknown
subViewport.Size2DOverride = new Vector2I(width, height); // Custom size for 2D.
subViewport.Size2DOverrideStretch = true; // Enable stretch for custom size.
```

---

## Using VisualShaders

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/visual_shaders.html

**Contents:**
- Using VisualShaders
- Creating a VisualShader
- Using the Visual Shader Editor
- Visual Shader node interface
- Visual Shader nodes
  - Expression node
  - Reroute node
  - Fresnel node
  - Boolean node
  - If node

VisualShaders are the visual alternative for creating shaders.

As shaders are inherently linked to visuals, the graph-based approach with previews of textures, materials, etc. offers a lot of additional convenience compared to purely script-based shaders. On the other hand, VisualShaders do not expose all features of the shader script and using both in parallel might be necessary for specific effects.

If you are not familiar with shaders, start by reading Introduction to shaders.

VisualShaders can be created in any ShaderMaterial. To begin using VisualShaders, create a new ShaderMaterial in an object of your choice.

Then assign a Shader resource to the Shader property.

Click on the new Shader resource and the Create Shader dialog will open automatically. Change the Type option to VisualShader in the dropdown, then give it a name.

Click on the visual shader you just created to open the Shader Editor. The layout of the Shader Editor comprises four parts, a file list on the left, the upper toolbar, the graph itself, and a material preview on the right that can be toggled off

From left to right in the toolbar:

The arrow can be used to toggle the files panel's visibility.

The File button opens a dropdown menu for saving, loading, and creating files.

The Add Node button displays a popup menu to let you add nodes to the shader graph.

The drop-down menu is the shader type: Vertex, Fragment and Light. Like for script shaders, it defines what built-in nodes will be available.

The following buttons and number input control the zooming level, grid snapping and distance between grid lines (in pixels).

The toggle controls if the graph minimap in the bottom right of the editor is visible or not.

The automatically arrange selected nodes button will try to organize any nodes you have selected as efficiently and cleanly as possible.

The Manage Varyings button opens a dropdown that lets you add or remove a varying.

The show generated code button shows shader code corresponding to your graph.

The toggle turns the material preview on or off.

The Online Docs button opens this documentation page in your web browser.

The last button allows you to put the shader editor in its own window, separate from the rest of the editor.

Although VisualShaders do not require coding, they share the same logic with script shaders. It is advised to learn the basics of both to have a good understanding of the shading pipeline.

The visual shader graph is converted to a script shader behind the scene, and you can see this code by pressing the last button in the toolbar. This can be convenient to understand what a given node does and how to reproduce it in scripts.

By default, every new VisualShader will have an output node. Every node connection ends at one of the output node's sockets. A node is the basic unit to create your shader. To add a new node, click on the Add Node button on the upper left corner or right click on any empty location in the graph, and a menu will pop up.

This popup has the following properties:

If you right-click on the graph, this menu will be called at the cursor position and the created node, in that case, will also be placed under that position; otherwise, it will be created at the graph's center.

It can be resized horizontally and vertically allowing more content to be shown. Size transform and tree content position are saved between the calls, so if you suddenly closed the popup you can easily restore its previous state.

The Expand All and Collapse All options in the drop-down option menu can be used to easily list the available nodes.

You can also drag and drop nodes from the popup onto the graph.

While the popup has nodes sorted in categories, it can seem overwhelming at first. Try to add some of the nodes, plug them in the output socket and observe what happens.

When connecting any scalar output to a vector input, all components of the vector will take the value of the scalar.

When connecting any vector output to a scalar input, the value of the scalar will be the average of the vector's components.

Visual shader nodes have input and output ports. The input ports are located on the left side of the node, and output ports are located on the right side of the node.

These ports are colored to differentiate type of port:

Scalar is a single value.

Vector is a set of values.

On or off, true or false.

A matrix, usually used to transform vertices.

A texture sampler. It can be used to sample textures.

All of the types are used in the calculations of vertices, fragments, and lights in the shader. For example: matrix multiplication, vector addition, or scalar division.

There are other types but these are the main ones.

Below are some special nodes that are worth knowing about. The list is not exhaustive and might be expanded with more nodes and examples.

The Expression node allows you to write Godot Shading Language (GLSL-like) expressions inside your visual shaders. The node has buttons to add any amount of required input and output ports and can be resized. You can also set up the name and type of each port. The expression you have entered will apply immediately to the material (once the focus leaves the expression text box). Any parsing or compilation errors will be printed to the Output tab. The outputs are initialized to their zero value by default. The node is located under the Special tab and can be used in all shader modes.

The possibilities of this node are almost limitless – you can write complex procedures, and use all the power of text-based shaders, such as loops, the discard keyword, extended types, etc. For example:

The Reroute node is used purely for organizational purposes. In a complicated shader with many nodes you may find that the paths between nodes can make things hard to read. Reroute, as its name suggests, allows you to adjust the path between nodes to make things easier to read. You can even have multiple reroute nodes for a single path, which can be used to make right angles.

To move a reroute node move your mouse cursor above it, and grab the handle that appears.

The Fresnel node is designed to accept normal and view vectors and produces a scalar which is the saturated dot product between them. Additionally, you can setup the inversion and the power of equation. The Fresnel node is great for adding a rim-like lighting effect to objects.

The Boolean node can be converted to Scalar or Vector to represent 0 or 1 and (0, 0, 0) or (1, 1, 1) respectively. This property can be used to enable or disable some effect parts with one click.

The If node allows you to setup a vector which will be returned the result of the comparison between a and b. There are three vectors which can be returned: a == b (in that case the tolerance parameter is provided as a comparison threshold – by default it is equal to the minimal value, i.e. 0.00001), a > b and a < b.

The Switch node returns a vector if the boolean condition is true or false. Boolean was introduced above. If you want to convert a vector to a true boolean, all components of the vector should be non-zero.

The Mesh Emitter node is used for emitting particles from mesh vertices. This is only available for shaders that are in Particles mode.

Keep in mind that not all 3D objects are mesh files. a glTF file can't be dragged and dropped into the graph. However, you can create an inherited scene from it, save the mesh in that scene as its own file, and use that.

You can also drag and drop obj files into the graph editor to add the node for that specific mesh, other mesh files will not work for this.

Please read the User-contributed notes policy before submitting a comment.

---

## Viewport

**URL:** https://docs.godotengine.org/en/stable/classes/class_viewport.html

**Contents:**
- Viewport
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Node < Object

Inherited By: SubViewport, Window

Abstract base class for viewports. Encapsulates drawing and interaction with a game world.

A Viewport creates a different view into the screen, or a sub-view inside another viewport. Child 2D nodes will display on it, and child Camera3D 3D nodes will render on it too.

Optionally, a viewport can have its own 2D or 3D world, so it doesn't share what it draws with other viewports.

Viewports can also choose to be audio listeners, so they generate positional audio depending on a 2D or 3D camera child of it.

Also, viewports can be assigned to different screens in case the devices have multiple screens.

Finally, viewports can also behave as render targets, in which case they will not be visible unless the associated texture is used to draw.

Viewport and canvas transforms

GUI in 3D Viewport Demo

3D in 2D Viewport Demo

2D in 3D Viewport Demo

Dynamic Split Screen Demo

3D Resolution Scaling Demo

anisotropic_filtering_level

audio_listener_enable_2d

audio_listener_enable_3d

DefaultCanvasItemTextureFilter

canvas_item_default_texture_filter

DefaultCanvasItemTextureRepeat

canvas_item_default_texture_repeat

global_canvas_transform

gui_snap_controls_to_pixels

oversampling_override

PhysicsInterpolationMode

physics_interpolation_mode

physics_object_picking

physics_object_picking_first_only

physics_object_picking_sort

positional_shadow_atlas_16_bits

PositionalShadowAtlasQuadrantSubdiv

positional_shadow_atlas_quad_0

PositionalShadowAtlasQuadrantSubdiv

positional_shadow_atlas_quad_1

PositionalShadowAtlasQuadrantSubdiv

positional_shadow_atlas_quad_2

PositionalShadowAtlasQuadrantSubdiv

positional_shadow_atlas_quad_3

positional_shadow_atlas_size

snap_2d_transforms_to_pixel

snap_2d_vertices_to_pixel

use_occlusion_culling

find_world_2d() const

find_world_3d() const

get_audio_listener_2d() const

get_audio_listener_3d() const

get_camera_2d() const

get_camera_3d() const

get_canvas_cull_mask_bit(layer: int) const

get_embedded_subwindows() const

get_final_transform() const

get_mouse_position() const

get_oversampling() const

PositionalShadowAtlasQuadrantSubdiv

get_positional_shadow_atlas_quadrant_subdiv(quadrant: int) const

get_render_info(type: RenderInfoType, info: RenderInfo)

get_screen_transform() const

get_stretch_transform() const

get_viewport_rid() const

get_visible_rect() const

gui_get_drag_data() const

gui_get_drag_description() const

gui_get_focus_owner() const

gui_get_hovered_control() const

gui_is_drag_successful() const

gui_is_dragging() const

gui_set_drag_description(description: String)

is_input_handled() const

notify_mouse_entered()

notify_mouse_exited()

push_input(event: InputEvent, in_local_coords: bool = false)

push_text_input(text: String)

push_unhandled_input(event: InputEvent, in_local_coords: bool = false)

set_canvas_cull_mask_bit(layer: int, enable: bool)

set_input_as_handled()

set_positional_shadow_atlas_quadrant_subdiv(quadrant: int, subdiv: PositionalShadowAtlasQuadrantSubdiv)

update_mouse_cursor_state()

warp_mouse(position: Vector2)

gui_focus_changed(node: Control) 🔗

Emitted when a Control node grabs keyboard focus.

Note: A Control node losing focus doesn't cause this signal to be emitted.

Emitted when the size of the viewport is changed, whether by resizing of window, or some other means.

enum PositionalShadowAtlasQuadrantSubdiv: 🔗

PositionalShadowAtlasQuadrantSubdiv SHADOW_ATLAS_QUADRANT_SUBDIV_DISABLED = 0

This quadrant will not be used.

PositionalShadowAtlasQuadrantSubdiv SHADOW_ATLAS_QUADRANT_SUBDIV_1 = 1

This quadrant will only be used by one shadow map.

PositionalShadowAtlasQuadrantSubdiv SHADOW_ATLAS_QUADRANT_SUBDIV_4 = 2

This quadrant will be split in 4 and used by up to 4 shadow maps.

PositionalShadowAtlasQuadrantSubdiv SHADOW_ATLAS_QUADRANT_SUBDIV_16 = 3

This quadrant will be split 16 ways and used by up to 16 shadow maps.

PositionalShadowAtlasQuadrantSubdiv SHADOW_ATLAS_QUADRANT_SUBDIV_64 = 4

This quadrant will be split 64 ways and used by up to 64 shadow maps.

PositionalShadowAtlasQuadrantSubdiv SHADOW_ATLAS_QUADRANT_SUBDIV_256 = 5

This quadrant will be split 256 ways and used by up to 256 shadow maps. Unless the positional_shadow_atlas_size is very high, the shadows in this quadrant will be very low resolution.

PositionalShadowAtlasQuadrantSubdiv SHADOW_ATLAS_QUADRANT_SUBDIV_1024 = 6

This quadrant will be split 1024 ways and used by up to 1024 shadow maps. Unless the positional_shadow_atlas_size is very high, the shadows in this quadrant will be very low resolution.

PositionalShadowAtlasQuadrantSubdiv SHADOW_ATLAS_QUADRANT_SUBDIV_MAX = 7

Represents the size of the PositionalShadowAtlasQuadrantSubdiv enum.

enum Scaling3DMode: 🔗

Scaling3DMode SCALING_3D_MODE_BILINEAR = 0

Use bilinear scaling for the viewport's 3D buffer. The amount of scaling can be set using scaling_3d_scale. Values less than 1.0 will result in undersampling while values greater than 1.0 will result in supersampling. A value of 1.0 disables scaling.

Scaling3DMode SCALING_3D_MODE_FSR = 1

Use AMD FidelityFX Super Resolution 1.0 upscaling for the viewport's 3D buffer. The amount of scaling can be set using scaling_3d_scale. Values less than 1.0 will result in the viewport being upscaled using FSR. Values greater than 1.0 are not supported and bilinear downsampling will be used instead. A value of 1.0 disables scaling.

Scaling3DMode SCALING_3D_MODE_FSR2 = 2

Use AMD FidelityFX Super Resolution 2.2 upscaling for the viewport's 3D buffer. The amount of scaling can be set using scaling_3d_scale. Values less than 1.0 will result in the viewport being upscaled using FSR2. Values greater than 1.0 are not supported and bilinear downsampling will be used instead. A value of 1.0 will use FSR2 at native resolution as a TAA solution.

Scaling3DMode SCALING_3D_MODE_METALFX_SPATIAL = 3

Use the MetalFX spatial upscaler for the viewport's 3D buffer.

The amount of scaling can be set using scaling_3d_scale.

Values less than 1.0 will result in the viewport being upscaled using MetalFX. Values greater than 1.0 are not supported and bilinear downsampling will be used instead. A value of 1.0 disables scaling.

More information: MetalFX.

Note: Only supported when the Metal rendering driver is in use, which limits this scaling mode to macOS and iOS.

Scaling3DMode SCALING_3D_MODE_METALFX_TEMPORAL = 4

Use the MetalFX temporal upscaler for the viewport's 3D buffer.

The amount of scaling can be set using scaling_3d_scale. To determine the minimum input scale, use the RenderingDevice.limit_get() method with RenderingDevice.LIMIT_METALFX_TEMPORAL_SCALER_MIN_SCALE.

Values less than 1.0 will result in the viewport being upscaled using MetalFX. Values greater than 1.0 are not supported and bilinear downsampling will be used instead. A value of 1.0 will use MetalFX at native resolution as a TAA solution.

More information: MetalFX.

Note: Only supported when the Metal rendering driver is in use, which limits this scaling mode to macOS and iOS.

Scaling3DMode SCALING_3D_MODE_MAX = 5

Represents the size of the Scaling3DMode enum.

MSAA MSAA_DISABLED = 0

Multisample antialiasing mode disabled. This is the default value, and is also the fastest setting.

Use 2× Multisample Antialiasing. This has a moderate performance cost. It helps reduce aliasing noticeably, but 4× MSAA still looks substantially better.

Use 4× Multisample Antialiasing. This has a significant performance cost, and is generally a good compromise between performance and quality.

Use 8× Multisample Antialiasing. This has a very high performance cost. The difference between 4× and 8× MSAA may not always be visible in real gameplay conditions. Likely unsupported on low-end and older hardware.

Represents the size of the MSAA enum.

enum AnisotropicFiltering: 🔗

AnisotropicFiltering ANISOTROPY_DISABLED = 0

Anisotropic filtering is disabled.

AnisotropicFiltering ANISOTROPY_2X = 1

Use 2× anisotropic filtering.

AnisotropicFiltering ANISOTROPY_4X = 2

Use 4× anisotropic filtering. This is the default value.

AnisotropicFiltering ANISOTROPY_8X = 3

Use 8× anisotropic filtering.

AnisotropicFiltering ANISOTROPY_16X = 4

Use 16× anisotropic filtering.

AnisotropicFiltering ANISOTROPY_MAX = 5

Represents the size of the AnisotropicFiltering enum.

enum ScreenSpaceAA: 🔗

ScreenSpaceAA SCREEN_SPACE_AA_DISABLED = 0

Do not perform any antialiasing in the full screen post-process.

ScreenSpaceAA SCREEN_SPACE_AA_FXAA = 1

Use fast approximate antialiasing. FXAA is a popular screen-space antialiasing method, which is fast but will make the image look blurry, especially at lower resolutions. It can still work relatively well at large resolutions such as 1440p and 4K.

ScreenSpaceAA SCREEN_SPACE_AA_SMAA = 2

Use subpixel morphological antialiasing. SMAA may produce clearer results than FXAA, but at a slightly higher performance cost.

ScreenSpaceAA SCREEN_SPACE_AA_MAX = 3

Represents the size of the ScreenSpaceAA enum.

RenderInfo RENDER_INFO_OBJECTS_IN_FRAME = 0

Amount of objects in frame.

RenderInfo RENDER_INFO_PRIMITIVES_IN_FRAME = 1

Amount of vertices in frame.

RenderInfo RENDER_INFO_DRAW_CALLS_IN_FRAME = 2

Amount of draw calls in frame.

RenderInfo RENDER_INFO_MAX = 3

Represents the size of the RenderInfo enum.

enum RenderInfoType: 🔗

RenderInfoType RENDER_INFO_TYPE_VISIBLE = 0

Visible render pass (excluding shadows).

RenderInfoType RENDER_INFO_TYPE_SHADOW = 1

Shadow render pass. Objects will be rendered several times depending on the number of amounts of lights with shadows and the number of directional shadow splits.

RenderInfoType RENDER_INFO_TYPE_CANVAS = 2

Canvas item rendering. This includes all 2D rendering.

RenderInfoType RENDER_INFO_TYPE_MAX = 3

Represents the size of the RenderInfoType enum.

DebugDraw DEBUG_DRAW_DISABLED = 0

Objects are displayed normally.

DebugDraw DEBUG_DRAW_UNSHADED = 1

Objects are displayed without light information.

DebugDraw DEBUG_DRAW_LIGHTING = 2

Objects are displayed without textures and only with lighting information.

Note: When using this debug draw mode, custom shaders are ignored since all materials in the scene temporarily use a debug material. This means the result from custom shader functions (such as vertex displacement) won't be visible anymore when using this debug draw mode.

DebugDraw DEBUG_DRAW_OVERDRAW = 3

Objects are displayed semi-transparent with additive blending so you can see where they are drawing over top of one another. A higher overdraw means you are wasting performance on drawing pixels that are being hidden behind others.

Note: When using this debug draw mode, custom shaders are ignored since all materials in the scene temporarily use a debug material. This means the result from custom shader functions (such as vertex displacement) won't be visible anymore when using this debug draw mode.

DebugDraw DEBUG_DRAW_WIREFRAME = 4

Objects are displayed as wireframe models.

Note: RenderingServer.set_debug_generate_wireframes() must be called before loading any meshes for wireframes to be visible when using the Compatibility renderer.

DebugDraw DEBUG_DRAW_NORMAL_BUFFER = 5

Objects are displayed without lighting information and their textures replaced by normal mapping.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_VOXEL_GI_ALBEDO = 6

Objects are displayed with only the albedo value from VoxelGIs. Requires at least one visible VoxelGI node that has been baked to have a visible effect.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_VOXEL_GI_LIGHTING = 7

Objects are displayed with only the lighting value from VoxelGIs. Requires at least one visible VoxelGI node that has been baked to have a visible effect.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_VOXEL_GI_EMISSION = 8

Objects are displayed with only the emission color from VoxelGIs. Requires at least one visible VoxelGI node that has been baked to have a visible effect.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_SHADOW_ATLAS = 9

Draws the shadow atlas that stores shadows from OmniLight3Ds and SpotLight3Ds in the upper left quadrant of the Viewport.

DebugDraw DEBUG_DRAW_DIRECTIONAL_SHADOW_ATLAS = 10

Draws the shadow atlas that stores shadows from DirectionalLight3Ds in the upper left quadrant of the Viewport.

DebugDraw DEBUG_DRAW_SCENE_LUMINANCE = 11

Draws the scene luminance buffer (if available) in the upper left quadrant of the Viewport.

Note: Only supported when using the Forward+ or Mobile rendering methods.

DebugDraw DEBUG_DRAW_SSAO = 12

Draws the screen-space ambient occlusion texture instead of the scene so that you can clearly see how it is affecting objects. In order for this display mode to work, you must have Environment.ssao_enabled set in your WorldEnvironment.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_SSIL = 13

Draws the screen-space indirect lighting texture instead of the scene so that you can clearly see how it is affecting objects. In order for this display mode to work, you must have Environment.ssil_enabled set in your WorldEnvironment.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_PSSM_SPLITS = 14

Colors each PSSM split for the DirectionalLight3Ds in the scene a different color so you can see where the splits are. In order (from closest to furthest from the camera), they are colored red, green, blue, and yellow.

Note: When using this debug draw mode, custom shaders are ignored since all materials in the scene temporarily use a debug material. This means the result from custom shader functions (such as vertex displacement) won't be visible anymore when using this debug draw mode.

Note: Only supported when using the Forward+ or Mobile rendering methods.

DebugDraw DEBUG_DRAW_DECAL_ATLAS = 15

Draws the decal atlas used by Decals and light projector textures in the upper left quadrant of the Viewport.

Note: Only supported when using the Forward+ or Mobile rendering methods.

DebugDraw DEBUG_DRAW_SDFGI = 16

Draws the cascades used to render signed distance field global illumination (SDFGI).

Does nothing if the current environment's Environment.sdfgi_enabled is false.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_SDFGI_PROBES = 17

Draws the probes used for signed distance field global illumination (SDFGI).

Does nothing if the current environment's Environment.sdfgi_enabled is false.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_GI_BUFFER = 18

Draws the buffer used for global illumination from VoxelGI or SDFGI. Requires VoxelGI (at least one visible baked VoxelGI node) or SDFGI (Environment.sdfgi_enabled) to be enabled to have a visible effect.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_DISABLE_LOD = 19

Draws all of the objects at their highest polycount regardless of their distance from the camera. No low level of detail (LOD) is applied.

DebugDraw DEBUG_DRAW_CLUSTER_OMNI_LIGHTS = 20

Draws the cluster used by OmniLight3D nodes to optimize light rendering.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_CLUSTER_SPOT_LIGHTS = 21

Draws the cluster used by SpotLight3D nodes to optimize light rendering.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_CLUSTER_DECALS = 22

Draws the cluster used by Decal nodes to optimize decal rendering.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_CLUSTER_REFLECTION_PROBES = 23

Draws the cluster used by ReflectionProbe nodes to optimize reflection probes.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_OCCLUDERS = 24

Draws the buffer used for occlusion culling.

Note: Only supported when using the Forward+ or Mobile rendering methods.

DebugDraw DEBUG_DRAW_MOTION_VECTORS = 25

Draws vector lines over the viewport to indicate the movement of pixels between frames.

Note: Only supported when using the Forward+ rendering method.

DebugDraw DEBUG_DRAW_INTERNAL_BUFFER = 26

Draws the internal resolution buffer of the scene in linear colorspace before tonemapping or post-processing is applied.

Note: Only supported when using the Forward+ or Mobile rendering methods.

enum DefaultCanvasItemTextureFilter: 🔗

DefaultCanvasItemTextureFilter DEFAULT_CANVAS_ITEM_TEXTURE_FILTER_NEAREST = 0

The texture filter reads from the nearest pixel only. This makes the texture look pixelated from up close, and grainy from a distance (due to mipmaps not being sampled).

DefaultCanvasItemTextureFilter DEFAULT_CANVAS_ITEM_TEXTURE_FILTER_LINEAR = 1

The texture filter blends between the nearest 4 pixels. This makes the texture look smooth from up close, and grainy from a distance (due to mipmaps not being sampled).

DefaultCanvasItemTextureFilter DEFAULT_CANVAS_ITEM_TEXTURE_FILTER_LINEAR_WITH_MIPMAPS = 2

The texture filter blends between the nearest 4 pixels and between the nearest 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true). This makes the texture look smooth from up close, and smooth from a distance.

Use this for non-pixel art textures that may be viewed at a low scale (e.g. due to Camera2D zoom or sprite scaling), as mipmaps are important to smooth out pixels that are smaller than on-screen pixels.

DefaultCanvasItemTextureFilter DEFAULT_CANVAS_ITEM_TEXTURE_FILTER_NEAREST_WITH_MIPMAPS = 3

The texture filter reads from the nearest pixel and blends between the nearest 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true). This makes the texture look pixelated from up close, and smooth from a distance.

Use this for non-pixel art textures that may be viewed at a low scale (e.g. due to Camera2D zoom or sprite scaling), as mipmaps are important to smooth out pixels that are smaller than on-screen pixels.

DefaultCanvasItemTextureFilter DEFAULT_CANVAS_ITEM_TEXTURE_FILTER_MAX = 4

Represents the size of the DefaultCanvasItemTextureFilter enum.

enum DefaultCanvasItemTextureRepeat: 🔗

DefaultCanvasItemTextureRepeat DEFAULT_CANVAS_ITEM_TEXTURE_REPEAT_DISABLED = 0

Disables textures repeating. Instead, when reading UVs outside the 0-1 range, the value will be clamped to the edge of the texture, resulting in a stretched out look at the borders of the texture.

DefaultCanvasItemTextureRepeat DEFAULT_CANVAS_ITEM_TEXTURE_REPEAT_ENABLED = 1

Enables the texture to repeat when UV coordinates are outside the 0-1 range. If using one of the linear filtering modes, this can result in artifacts at the edges of a texture when the sampler filters across the edges of the texture.

DefaultCanvasItemTextureRepeat DEFAULT_CANVAS_ITEM_TEXTURE_REPEAT_MIRROR = 2

Flip the texture when repeating so that the edge lines up instead of abruptly changing.

DefaultCanvasItemTextureRepeat DEFAULT_CANVAS_ITEM_TEXTURE_REPEAT_MAX = 3

Represents the size of the DefaultCanvasItemTextureRepeat enum.

SDFOversize SDF_OVERSIZE_100_PERCENT = 0

The signed distance field only covers the viewport's own rectangle.

SDFOversize SDF_OVERSIZE_120_PERCENT = 1

The signed distance field is expanded to cover 20% of the viewport's size around the borders.

SDFOversize SDF_OVERSIZE_150_PERCENT = 2

The signed distance field is expanded to cover 50% of the viewport's size around the borders.

SDFOversize SDF_OVERSIZE_200_PERCENT = 3

The signed distance field is expanded to cover 100% (double) of the viewport's size around the borders.

SDFOversize SDF_OVERSIZE_MAX = 4

Represents the size of the SDFOversize enum.

SDFScale SDF_SCALE_100_PERCENT = 0

The signed distance field is rendered at full resolution.

SDFScale SDF_SCALE_50_PERCENT = 1

The signed distance field is rendered at half the resolution of this viewport.

SDFScale SDF_SCALE_25_PERCENT = 2

The signed distance field is rendered at a quarter the resolution of this viewport.

SDFScale SDF_SCALE_MAX = 3

Represents the size of the SDFScale enum.

VRSMode VRS_DISABLED = 0

Variable Rate Shading is disabled.

VRSMode VRS_TEXTURE = 1

Variable Rate Shading uses a texture. Note, for stereoscopic use a texture atlas with a texture for each view.

Variable Rate Shading's texture is supplied by the primary XRInterface.

Represents the size of the VRSMode enum.

enum VRSUpdateMode: 🔗

VRSUpdateMode VRS_UPDATE_DISABLED = 0

The input texture for variable rate shading will not be processed.

VRSUpdateMode VRS_UPDATE_ONCE = 1

The input texture for variable rate shading will be processed once.

VRSUpdateMode VRS_UPDATE_ALWAYS = 2

The input texture for variable rate shading will be processed each frame.

VRSUpdateMode VRS_UPDATE_MAX = 3

Represents the size of the VRSUpdateMode enum.

AnisotropicFiltering anisotropic_filtering_level = 2 🔗

void set_anisotropic_filtering_level(value: AnisotropicFiltering)

AnisotropicFiltering get_anisotropic_filtering_level()

Sets the maximum number of samples to take when using anisotropic filtering on textures (as a power of two). A higher sample count will result in sharper textures at oblique angles, but is more expensive to compute. A value of 0 forcibly disables anisotropic filtering, even on materials where it is enabled.

The anisotropic filtering level also affects decals and light projectors if they are configured to use anisotropic filtering. See ProjectSettings.rendering/textures/decals/filter and ProjectSettings.rendering/textures/light_projectors/filter.

Note: In 3D, for this setting to have an effect, set BaseMaterial3D.texture_filter to BaseMaterial3D.TEXTURE_FILTER_LINEAR_WITH_MIPMAPS_ANISOTROPIC or BaseMaterial3D.TEXTURE_FILTER_NEAREST_WITH_MIPMAPS_ANISOTROPIC on materials.

Note: In 2D, for this setting to have an effect, set CanvasItem.texture_filter to CanvasItem.TEXTURE_FILTER_LINEAR_WITH_MIPMAPS_ANISOTROPIC or CanvasItem.TEXTURE_FILTER_NEAREST_WITH_MIPMAPS_ANISOTROPIC on the CanvasItem node displaying the texture (or in CanvasTexture). However, anisotropic filtering is rarely useful in 2D, so only enable it for textures in 2D if it makes a meaningful visual difference.

bool audio_listener_enable_2d = false 🔗

void set_as_audio_listener_2d(value: bool)

bool is_audio_listener_2d()

If true, the viewport will process 2D audio streams.

bool audio_listener_enable_3d = false 🔗

void set_as_audio_listener_3d(value: bool)

bool is_audio_listener_3d()

If true, the viewport will process 3D audio streams.

int canvas_cull_mask = 4294967295 🔗

void set_canvas_cull_mask(value: int)

int get_canvas_cull_mask()

The rendering layers in which this Viewport renders CanvasItem nodes.

DefaultCanvasItemTextureFilter canvas_item_default_texture_filter = 1 🔗

void set_default_canvas_item_texture_filter(value: DefaultCanvasItemTextureFilter)

DefaultCanvasItemTextureFilter get_default_canvas_item_texture_filter()

Sets the default filter mode used by CanvasItems in this Viewport.

DefaultCanvasItemTextureRepeat canvas_item_default_texture_repeat = 0 🔗

void set_default_canvas_item_texture_repeat(value: DefaultCanvasItemTextureRepeat)

DefaultCanvasItemTextureRepeat get_default_canvas_item_texture_repeat()

Sets the default repeat mode used by CanvasItems in this Viewport.

Transform2D canvas_transform 🔗

void set_canvas_transform(value: Transform2D)

Transform2D get_canvas_transform()

The canvas transform of the viewport, useful for changing the on-screen positions of all child CanvasItems. This is relative to the global canvas transform of the viewport.

DebugDraw debug_draw = 0 🔗

void set_debug_draw(value: DebugDraw)

DebugDraw get_debug_draw()

The overlay mode for test rendered geometry in debug purposes.

bool disable_3d = false 🔗

void set_disable_3d(value: bool)

bool is_3d_disabled()

Disable 3D rendering (but keep 2D rendering).

float fsr_sharpness = 0.2 🔗

void set_fsr_sharpness(value: float)

float get_fsr_sharpness()

Determines how sharp the upscaled image will be when using the FSR upscaling mode. Sharpness halves with every whole number. Values go from 0.0 (sharpest) to 2.0. Values above 2.0 won't make a visible difference.

To control this property on the root viewport, set the ProjectSettings.rendering/scaling_3d/fsr_sharpness project setting.

Transform2D global_canvas_transform 🔗

void set_global_canvas_transform(value: Transform2D)

Transform2D get_global_canvas_transform()

The global canvas transform of the viewport. The canvas transform is relative to this.

bool gui_disable_input = false 🔗

void set_disable_input(value: bool)

bool is_input_disabled()

If true, the viewport will not receive input events.

bool gui_embed_subwindows = false 🔗

void set_embedding_subwindows(value: bool)

bool is_embedding_subwindows()

If true, sub-windows (popups and dialogs) will be embedded inside application window as control-like nodes. If false, they will appear as separate windows handled by the operating system.

bool gui_snap_controls_to_pixels = true 🔗

void set_snap_controls_to_pixels(value: bool)

bool is_snap_controls_to_pixels_enabled()

If true, the GUI controls on the viewport will lay pixel perfectly.

bool handle_input_locally = true 🔗

void set_handle_input_locally(value: bool)

bool is_handling_input_locally()

If true, this viewport will mark incoming input events as handled by itself. If false, this is instead done by the first parent viewport that is set to handle input locally.

A SubViewportContainer will automatically set this property to false for the Viewport contained inside of it.

See also set_input_as_handled() and is_input_handled().

float mesh_lod_threshold = 1.0 🔗

void set_mesh_lod_threshold(value: float)

float get_mesh_lod_threshold()

The automatic LOD bias to use for meshes rendered within the Viewport (this is analogous to ReflectionProbe.mesh_lod_threshold). Higher values will use less detailed versions of meshes that have LOD variations generated. If set to 0.0, automatic LOD is disabled. Increase mesh_lod_threshold to improve performance at the cost of geometry detail.

To control this property on the root viewport, set the ProjectSettings.rendering/mesh_lod/lod_change/threshold_pixels project setting.

Note: mesh_lod_threshold does not affect GeometryInstance3D visibility ranges (also known as "manual" LOD or hierarchical LOD).

void set_msaa_2d(value: MSAA)

The multisample antialiasing mode for 2D/Canvas rendering. A higher number results in smoother edges at the cost of significantly worse performance. A value of MSAA_2X or MSAA_4X is best unless targeting very high-end systems. This has no effect on shader-induced aliasing or texture aliasing.

See also ProjectSettings.rendering/anti_aliasing/quality/msaa_2d and RenderingServer.viewport_set_msaa_2d().

void set_msaa_3d(value: MSAA)

The multisample antialiasing mode for 3D rendering. A higher number results in smoother edges at the cost of significantly worse performance. A value of MSAA_2X or MSAA_4X is best unless targeting very high-end systems. See also bilinear scaling 3D scaling_3d_mode for supersampling, which provides higher quality but is much more expensive. This has no effect on shader-induced aliasing or texture aliasing.

See also ProjectSettings.rendering/anti_aliasing/quality/msaa_3d and RenderingServer.viewport_set_msaa_3d().

bool oversampling = true 🔗

void set_use_oversampling(value: bool)

bool is_using_oversampling()

If true and one of the following conditions are true: SubViewport.size_2d_override_stretch and SubViewport.size_2d_override are set, Window.content_scale_factor is set and scaling is enabled, oversampling_override is set, font and DPITexture oversampling are enabled.

float oversampling_override = 0.0 🔗

void set_oversampling_override(value: float)

float get_oversampling_override()

If greater than zero, this value is used as the font oversampling factor, otherwise oversampling is equal to viewport scale.

bool own_world_3d = false 🔗

void set_use_own_world_3d(value: bool)

bool is_using_own_world_3d()

If true, the viewport will use a unique copy of the World3D defined in world_3d.

bool physics_object_picking = false 🔗

void set_physics_object_picking(value: bool)

bool get_physics_object_picking()

If true, the objects rendered by viewport become subjects of mouse picking process.

Note: The number of simultaneously pickable objects is limited to 64 and they are selected in a non-deterministic order, which can be different in each picking process.

bool physics_object_picking_first_only = false 🔗

void set_physics_object_picking_first_only(value: bool)

bool get_physics_object_picking_first_only()

If true, the input_event signal will only be sent to one physics object in the mouse picking process. If you want to get the top object only, you must also enable physics_object_picking_sort.

If false, an input_event signal will be sent to all physics objects in the mouse picking process.

This applies to 2D CanvasItem object picking only.

bool physics_object_picking_sort = false 🔗

void set_physics_object_picking_sort(value: bool)

bool get_physics_object_picking_sort()

If true, objects receive mouse picking events sorted primarily by their CanvasItem.z_index and secondarily by their position in the scene tree. If false, the order is undetermined.

Note: This setting is disabled by default because of its potential expensive computational cost.

Note: Sorting happens after selecting the pickable objects. Because of the limitation of 64 simultaneously pickable objects, it is not guaranteed that the object with the highest CanvasItem.z_index receives the picking event.

bool positional_shadow_atlas_16_bits = true 🔗

void set_positional_shadow_atlas_16_bits(value: bool)

bool get_positional_shadow_atlas_16_bits()

Use 16 bits for the omni/spot shadow depth map. Enabling this results in shadows having less precision and may result in shadow acne, but can lead to performance improvements on some devices.

PositionalShadowAtlasQuadrantSubdiv positional_shadow_atlas_quad_0 = 2 🔗

void set_positional_shadow_atlas_quadrant_subdiv(quadrant: int, subdiv: PositionalShadowAtlasQuadrantSubdiv)

PositionalShadowAtlasQuadrantSubdiv get_positional_shadow_atlas_quadrant_subdiv(quadrant: int) const

The subdivision amount of the first quadrant on the shadow atlas.

PositionalShadowAtlasQuadrantSubdiv positional_shadow_atlas_quad_1 = 2 🔗

void set_positional_shadow_atlas_quadrant_subdiv(quadrant: int, subdiv: PositionalShadowAtlasQuadrantSubdiv)

PositionalShadowAtlasQuadrantSubdiv get_positional_shadow_atlas_quadrant_subdiv(quadrant: int) const

The subdivision amount of the second quadrant on the shadow atlas.

PositionalShadowAtlasQuadrantSubdiv positional_shadow_atlas_quad_2 = 3 🔗

void set_positional_shadow_atlas_quadrant_subdiv(quadrant: int, subdiv: PositionalShadowAtlasQuadrantSubdiv)

PositionalShadowAtlasQuadrantSubdiv get_positional_shadow_atlas_quadrant_subdiv(quadrant: int) const

The subdivision amount of the third quadrant on the shadow atlas.

PositionalShadowAtlasQuadrantSubdiv positional_shadow_atlas_quad_3 = 4 🔗

void set_positional_shadow_atlas_quadrant_subdiv(quadrant: int, subdiv: PositionalShadowAtlasQuadrantSubdiv)

PositionalShadowAtlasQuadrantSubdiv get_positional_shadow_atlas_quadrant_subdiv(quadrant: int) const

The subdivision amount of the fourth quadrant on the shadow atlas.

int positional_shadow_atlas_size = 2048 🔗

void set_positional_shadow_atlas_size(value: int)

int get_positional_shadow_atlas_size()

The shadow atlas' resolution (used for omni and spot lights). The value is rounded up to the nearest power of 2.

Note: If this is set to 0, no positional shadows will be visible at all. This can improve performance significantly on low-end systems by reducing both the CPU and GPU load (as fewer draw calls are needed to draw the scene without shadows).

Scaling3DMode scaling_3d_mode = 0 🔗

void set_scaling_3d_mode(value: Scaling3DMode)

Scaling3DMode get_scaling_3d_mode()

Sets scaling 3D mode. Bilinear scaling renders at different resolution to either undersample or supersample the viewport. FidelityFX Super Resolution 1.0, abbreviated to FSR, is an upscaling technology that produces high quality images at fast framerates by using a spatially aware upscaling algorithm. FSR is slightly more expensive than bilinear, but it produces significantly higher image quality. FSR should be used where possible.

To control this property on the root viewport, set the ProjectSettings.rendering/scaling_3d/mode project setting.

float scaling_3d_scale = 1.0 🔗

void set_scaling_3d_scale(value: float)

float get_scaling_3d_scale()

Scales the 3D render buffer based on the viewport size uses an image filter specified in ProjectSettings.rendering/scaling_3d/mode to scale the output image to the full viewport size. Values lower than 1.0 can be used to speed up 3D rendering at the cost of quality (undersampling). Values greater than 1.0 are only valid for bilinear mode and can be used to improve 3D rendering quality at a high performance cost (supersampling). See also ProjectSettings.rendering/anti_aliasing/quality/msaa_3d for multi-sample antialiasing, which is significantly cheaper but only smooths the edges of polygons.

When using FSR upscaling, AMD recommends exposing the following values as preset options to users "Ultra Quality: 0.77", "Quality: 0.67", "Balanced: 0.59", "Performance: 0.5" instead of exposing the entire scale.

To control this property on the root viewport, set the ProjectSettings.rendering/scaling_3d/scale project setting.

ScreenSpaceAA screen_space_aa = 0 🔗

void set_screen_space_aa(value: ScreenSpaceAA)

ScreenSpaceAA get_screen_space_aa()

Sets the screen-space antialiasing method used. Screen-space antialiasing works by selectively blurring edges in a post-process shader. It differs from MSAA which takes multiple coverage samples while rendering objects. Screen-space AA methods are typically faster than MSAA and will smooth out specular aliasing, but tend to make scenes appear blurry.

See also ProjectSettings.rendering/anti_aliasing/quality/screen_space_aa and RenderingServer.viewport_set_screen_space_aa().

SDFOversize sdf_oversize = 1 🔗

void set_sdf_oversize(value: SDFOversize)

SDFOversize get_sdf_oversize()

Controls how much of the original viewport's size should be covered by the 2D signed distance field. This SDF can be sampled in CanvasItem shaders and is also used for GPUParticles2D collision. Higher values allow portions of occluders located outside the viewport to still be taken into account in the generated signed distance field, at the cost of performance. If you notice particles falling through LightOccluder2Ds as the occluders leave the viewport, increase this setting.

The percentage is added on each axis and on both sides. For example, with the default SDF_OVERSIZE_120_PERCENT, the signed distance field will cover 20% of the viewport's size outside the viewport on each side (top, right, bottom, left).

SDFScale sdf_scale = 1 🔗

void set_sdf_scale(value: SDFScale)

SDFScale get_sdf_scale()

The resolution scale to use for the 2D signed distance field. Higher values lead to a more precise and more stable signed distance field as the camera moves, at the cost of performance.

bool snap_2d_transforms_to_pixel = false 🔗

void set_snap_2d_transforms_to_pixel(value: bool)

bool is_snap_2d_transforms_to_pixel_enabled()

If true, CanvasItem nodes will internally snap to full pixels. Their position can still be sub-pixel, but the decimals will not have effect. This can lead to a crisper appearance at the cost of less smooth movement, especially when Camera2D smoothing is enabled.

bool snap_2d_vertices_to_pixel = false 🔗

void set_snap_2d_vertices_to_pixel(value: bool)

bool is_snap_2d_vertices_to_pixel_enabled()

If true, vertices of CanvasItem nodes will snap to full pixels. Only affects the final vertex positions, not the transforms. This can lead to a crisper appearance at the cost of less smooth movement, especially when Camera2D smoothing is enabled.

float texture_mipmap_bias = 0.0 🔗

void set_texture_mipmap_bias(value: float)

float get_texture_mipmap_bias()

Affects the final texture sharpness by reading from a lower or higher mipmap (also called "texture LOD bias"). Negative values make mipmapped textures sharper but grainier when viewed at a distance, while positive values make mipmapped textures blurrier (even when up close).

Enabling temporal antialiasing (use_taa) will automatically apply a -0.5 offset to this value, while enabling FXAA (screen_space_aa) will automatically apply a -0.25 offset to this value. If both TAA and FXAA are enabled at the same time, an offset of -0.75 is applied to this value.

Note: If scaling_3d_scale is lower than 1.0 (exclusive), texture_mipmap_bias is used to adjust the automatic mipmap bias which is calculated internally based on the scale factor. The formula for this is log2(scaling_3d_scale) + mipmap_bias.

To control this property on the root viewport, set the ProjectSettings.rendering/textures/default_filters/texture_mipmap_bias project setting.

bool transparent_bg = false 🔗

void set_transparent_background(value: bool)

bool has_transparent_background()

If true, the viewport should render its background as transparent.

Note: Due to technical limitations, certain rendering features are disabled when a viewport has a transparent background. This currently applies to screen-space reflections, subsurface scattering, and depth of field.

bool use_debanding = false 🔗

void set_use_debanding(value: bool)

bool is_using_debanding()

If true, uses a fast post-processing filter to make banding significantly less visible. If use_hdr_2d is false, 2D rendering is not affected by debanding unless the Environment.background_mode is Environment.BG_CANVAS. If use_hdr_2d is true, debanding will only be applied if this is the root Viewport and will affect all 2D and 3D rendering, including canvas items.

In some cases, debanding may introduce a slightly noticeable dithering pattern. It's recommended to enable debanding only when actually needed since the dithering pattern will make lossless-compressed screenshots larger.

See also ProjectSettings.rendering/anti_aliasing/quality/use_debanding and RenderingServer.viewport_set_use_debanding().

bool use_hdr_2d = false 🔗

void set_use_hdr_2d(value: bool)

bool is_using_hdr_2d()

If true, 2D rendering will use a high dynamic range (HDR) format framebuffer matching the bit depth of the 3D framebuffer. When using the Forward+ or Compatibility renderer, this will be an RGBA16 framebuffer. When using the Mobile renderer, it will be an RGB10_A2 framebuffer.

Additionally, 2D rendering will take place in linear color space and will be converted to sRGB space immediately before blitting to the screen (if the Viewport is attached to the screen).

Practically speaking, this means that the end result of the Viewport will not be clamped to the 0-1 range and can be used in 3D rendering without color space adjustments. This allows 2D rendering to take advantage of effects requiring high dynamic range (e.g. 2D glow) as well as substantially improves the appearance of effects requiring highly detailed gradients.

bool use_occlusion_culling = false 🔗

void set_use_occlusion_culling(value: bool)

bool is_using_occlusion_culling()

If true, OccluderInstance3D nodes will be usable for occlusion culling in 3D for this viewport. For the root viewport, ProjectSettings.rendering/occlusion_culling/use_occlusion_culling must be set to true instead.

Note: Enabling occlusion culling has a cost on the CPU. Only enable occlusion culling if you actually plan to use it, and think whether your scene can actually benefit from occlusion culling. Large, open scenes with few or no objects blocking the view will generally not benefit much from occlusion culling. Large open scenes generally benefit more from mesh LOD and visibility ranges (GeometryInstance3D.visibility_range_begin and GeometryInstance3D.visibility_range_end) compared to occlusion culling.

Note: Due to memory constraints, occlusion culling is not supported by default in Web export templates. It can be enabled by compiling custom Web export templates with module_raycast_enabled=yes.

bool use_taa = false 🔗

void set_use_taa(value: bool)

Enables temporal antialiasing for this viewport. TAA works by jittering the camera and accumulating the images of the last rendered frames, motion vector rendering is used to account for camera and object motion.

Note: The implementation is not complete yet, some visual instances such as particles and skinned meshes may show artifacts.

See also ProjectSettings.rendering/anti_aliasing/quality/use_taa and RenderingServer.viewport_set_use_taa().

bool use_xr = false 🔗

void set_use_xr(value: bool)

If true, the viewport will use the primary XR interface to render XR output. When applicable this can result in a stereoscopic image and the resulting render being output to a headset.

VRSMode vrs_mode = 0 🔗

void set_vrs_mode(value: VRSMode)

VRSMode get_vrs_mode()

The Variable Rate Shading (VRS) mode that is used for this viewport. Note, if hardware does not support VRS this property is ignored.

Texture2D vrs_texture 🔗

void set_vrs_texture(value: Texture2D)

Texture2D get_vrs_texture()

Texture to use when vrs_mode is set to VRS_TEXTURE.

The texture must use a lossless compression format so that colors can be matched precisely. The following VRS densities are mapped to various colors, with brighter colors representing a lower level of shading precision:

VRSUpdateMode vrs_update_mode = 1 🔗

void set_vrs_update_mode(value: VRSUpdateMode)

VRSUpdateMode get_vrs_update_mode()

Sets the update mode for Variable Rate Shading (VRS) for the viewport. VRS requires the input texture to be converted to the format usable by the VRS method supported by the hardware. The update mode defines how often this happens. If the GPU does not support VRS, or VRS is not enabled, this property is ignored.

void set_world_2d(value: World2D)

World2D get_world_2d()

The custom World2D which can be used as 2D environment source.

void set_world_3d(value: World3D)

World3D get_world_3d()

The custom World3D which can be used as 3D environment source.

World2D find_world_2d() const 🔗

Returns the first valid World2D for this viewport, searching the world_2d property of itself and any Viewport ancestor.

World3D find_world_3d() const 🔗

Returns the first valid World3D for this viewport, searching the world_3d property of itself and any Viewport ancestor.

AudioListener2D get_audio_listener_2d() const 🔗

Returns the currently active 2D audio listener. Returns null if there are no active 2D audio listeners, in which case the active 2D camera will be treated as listener.

AudioListener3D get_audio_listener_3d() const 🔗

Returns the currently active 3D audio listener. Returns null if there are no active 3D audio listeners, in which case the active 3D camera will be treated as listener.

Camera2D get_camera_2d() const 🔗

Returns the currently active 2D camera. Returns null if there are no active cameras.

Camera3D get_camera_3d() const 🔗

Returns the currently active 3D camera.

bool get_canvas_cull_mask_bit(layer: int) const 🔗

Returns an individual bit on the rendering layer mask.

Array[Window] get_embedded_subwindows() const 🔗

Returns a list of the visible embedded Windows inside the viewport.

Note: Windows inside other viewports will not be listed.

Transform2D get_final_transform() const 🔗

Returns the transform from the viewport's coordinate system to the embedder's coordinate system.

Vector2 get_mouse_position() const 🔗

Returns the mouse's position in this Viewport using the coordinate system of this Viewport.

float get_oversampling() const 🔗

Returns viewport oversampling factor.

PositionalShadowAtlasQuadrantSubdiv get_positional_shadow_atlas_quadrant_subdiv(quadrant: int) const 🔗

Returns the positional shadow atlas quadrant subdivision of the specified quadrant.

int get_render_info(type: RenderInfoType, info: RenderInfo) 🔗

Returns rendering statistics of the given type.

Transform2D get_screen_transform() const 🔗

Returns the transform from the Viewport's coordinates to the screen coordinates of the containing window manager window.

Transform2D get_stretch_transform() const 🔗

Returns the automatically computed 2D stretch transform, taking the Viewport's stretch settings into account. The final value is multiplied by Window.content_scale_factor, but only for the root viewport. If this method is called on a SubViewport (e.g., in a scene tree with SubViewportContainer and SubViewport), the scale factor of the root window will not be applied. Using Transform2D.get_scale() on the returned value, this can be used to compensate for scaling when zooming a Camera2D node, or to scale down a TextureRect to be pixel-perfect regardless of the automatically computed scale factor.

Note: Due to how pixel scaling works, the returned transform's X and Y scale may differ slightly, even when Window.content_scale_aspect is set to a mode that preserves the pixels' aspect ratio. If Window.content_scale_aspect is Window.CONTENT_SCALE_ASPECT_IGNORE, the X and Y scale may differ significantly.

ViewportTexture get_texture() const 🔗

Returns the viewport's texture.

Note: When trying to store the current texture (e.g. in a file), it might be completely black or outdated if used too early, especially when used in e.g. Node._ready(). To make sure the texture you get is correct, you can await RenderingServer.frame_post_draw signal.

Note: When use_hdr_2d is true the returned texture will be an HDR image encoded in linear space.

RID get_viewport_rid() const 🔗

Returns the viewport's RID from the RenderingServer.

Rect2 get_visible_rect() const 🔗

Returns the visible rectangle in global screen coordinates.

void gui_cancel_drag() 🔗

Cancels the drag operation that was previously started through Control._get_drag_data() or forced with Control.force_drag().

Variant gui_get_drag_data() const 🔗

Returns the drag data from the GUI, that was previously returned by Control._get_drag_data().

String gui_get_drag_description() const 🔗

Returns the drag data human-readable description.

Control gui_get_focus_owner() const 🔗

Returns the currently focused Control within this viewport. If no Control is focused, returns null.

Control gui_get_hovered_control() const 🔗

Returns the Control that the mouse is currently hovering over in this viewport. If no Control has the cursor, returns null.

Typically the leaf Control node or deepest level of the subtree which claims hover. This is very useful when used together with Node.is_ancestor_of() to find if the mouse is within a control tree.

bool gui_is_drag_successful() const 🔗

Returns true if the drag operation is successful.

bool gui_is_dragging() const 🔗

Returns true if a drag operation is currently ongoing and where the drop action could happen in this viewport.

Alternative to Node.NOTIFICATION_DRAG_BEGIN and Node.NOTIFICATION_DRAG_END when you prefer polling the value.

void gui_release_focus() 🔗

Removes the focus from the currently focused Control within this viewport. If no Control has the focus, does nothing.

void gui_set_drag_description(description: String) 🔗

Sets the drag data human-readable description.

bool is_input_handled() const 🔗

Returns whether the current InputEvent has been handled. Input events are not handled until set_input_as_handled() has been called during the lifetime of an InputEvent.

This is usually done as part of input handling methods like Node._input(), Control._gui_input() or others, as well as in corresponding signal handlers.

If handle_input_locally is set to false, this method will try finding the first parent viewport that is set to handle input locally, and return its value for is_input_handled() instead.

void notify_mouse_entered() 🔗

Inform the Viewport that the mouse has entered its area. Use this function before sending an InputEventMouseButton or InputEventMouseMotion to the Viewport with push_input(). See also notify_mouse_exited().

Note: In most cases, it is not necessary to call this function because SubViewport nodes that are children of SubViewportContainer are notified automatically. This is only necessary when interacting with viewports in non-default ways, for example as textures in TextureRect or with an Area3D that forwards input events.

void notify_mouse_exited() 🔗

Inform the Viewport that the mouse has left its area. Use this function when the node that displays the viewport notices the mouse has left the area of the displayed viewport. See also notify_mouse_entered().

Note: In most cases, it is not necessary to call this function because SubViewport nodes that are children of SubViewportContainer are notified automatically. This is only necessary when interacting with viewports in non-default ways, for example as textures in TextureRect or with an Area3D that forwards input events.

void push_input(event: InputEvent, in_local_coords: bool = false) 🔗

Triggers the given event in this Viewport. This can be used to pass an InputEvent between viewports, or to locally apply inputs that were sent over the network or saved to a file.

If in_local_coords is false, the event's position is in the embedder's coordinates and will be converted to viewport coordinates. If in_local_coords is true, the event's position is in viewport coordinates.

While this method serves a similar purpose as Input.parse_input_event(), it does not remap the specified event based on project settings like ProjectSettings.input_devices/pointing/emulate_touch_from_mouse.

Calling this method will propagate calls to child nodes for following methods in the given order:

Control._gui_input() for Control nodes

Node._shortcut_input()

Node._unhandled_key_input()

Node._unhandled_input()

If an earlier method marks the input as handled via set_input_as_handled(), any later method in this list will not be called.

If none of the methods handle the event and physics_object_picking is true, the event is used for physics object picking.

void push_text_input(text: String) 🔗

Helper method which calls the set_text() method on the currently focused Control, provided that it is defined (e.g. if the focused Control is Button or LineEdit).

void push_unhandled_input(event: InputEvent, in_local_coords: bool = false) 🔗

Deprecated: Use push_input() instead.

Triggers the given event in this Viewport. This can be used to pass an InputEvent between viewports, or to locally apply inputs that were sent over the network or saved to a file.

If in_local_coords is false, the event's position is in the embedder's coordinates and will be converted to viewport coordinates. If in_local_coords is true, the event's position is in viewport coordinates.

Calling this method will propagate calls to child nodes for following methods in the given order:

Node._shortcut_input()

Node._unhandled_key_input()

Node._unhandled_input()

If an earlier method marks the input as handled via set_input_as_handled(), any later method in this list will not be called.

If none of the methods handle the event and physics_object_picking is true, the event is used for physics object picking.

Note: This method doesn't propagate input events to embedded Windows or SubViewports.

void set_canvas_cull_mask_bit(layer: int, enable: bool) 🔗

Set/clear individual bits on the rendering layer mask. This simplifies editing this Viewport's layers.

void set_input_as_handled() 🔗

Stops the input from propagating further down the SceneTree.

Note: This does not affect the methods in Input, only the way events are propagated.

void set_positional_shadow_atlas_quadrant_subdiv(quadrant: int, subdiv: PositionalShadowAtlasQuadrantSubdiv) 🔗

Sets the number of subdivisions to use in the specified quadrant. A higher number of subdivisions allows you to have more shadows in the scene at once, but reduces the quality of the shadows. A good practice is to have quadrants with a varying number of subdivisions and to have as few subdivisions as possible.

void update_mouse_cursor_state() 🔗

Force instantly updating the display based on the current mouse cursor position. This includes updating the mouse cursor shape and sending necessary Control.mouse_entered, CollisionObject2D.mouse_entered, CollisionObject3D.mouse_entered and Window.mouse_entered signals and their respective mouse_exited counterparts.

void warp_mouse(position: Vector2) 🔗

Moves the mouse pointer to the specified position in this Viewport using the coordinate system of this Viewport.

Note: warp_mouse() is only supported on Windows, macOS and Linux. It has no effect on Android, iOS and Web.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (markdown):
```markdown
- 1×1 = rgb(0, 0, 0)     - #000000
- 1×2 = rgb(0, 85, 0)    - #005500
- 2×1 = rgb(85, 0, 0)    - #550000
- 2×2 = rgb(85, 85, 0)   - #555500
- 2×4 = rgb(85, 170, 0)  - #55aa00
- 4×2 = rgb(170, 85, 0)  - #aa5500
- 4×4 = rgb(170, 170, 0) - #aaaa00
- 4×8 = rgb(170, 255, 0) - #aaff00 - Not supported on most hardware
- 8×4 = rgb(255, 170, 0) - #ffaa00 - Not supported on most hardware
- 8×8 = rgb(255, 255, 0) - #ffff00 - Not supported on most hardware
```

Example 2 (gdscript):
```gdscript
func _ready():
    await RenderingServer.frame_post_draw
    $Viewport.get_texture().get_image().save_png("user://Screenshot.png")
```

Example 3 (gdscript):
```gdscript
public async override void _Ready()
{
    await ToSignal(RenderingServer.Singleton, RenderingServer.SignalName.FramePostDraw);
    var viewport = GetNode<Viewport>("Viewport");
    viewport.GetTexture().GetImage().SavePng("user://Screenshot.png");
}
```

---

## VisualShaderNodeBillboard

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodebillboard.html

**Contents:**
- VisualShaderNodeBillboard
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A node that controls how the object faces the camera to be used within the visual shader graph.

The output port of this node needs to be connected to Model View Matrix port of VisualShaderNodeOutput.

enum BillboardType: 🔗

BillboardType BILLBOARD_TYPE_DISABLED = 0

Billboarding is disabled and the node does nothing.

BillboardType BILLBOARD_TYPE_ENABLED = 1

A standard billboarding algorithm is enabled.

BillboardType BILLBOARD_TYPE_FIXED_Y = 2

A billboarding algorithm to rotate around Y-axis is enabled.

BillboardType BILLBOARD_TYPE_PARTICLES = 3

A billboarding algorithm designed to use on particles is enabled.

BillboardType BILLBOARD_TYPE_MAX = 4

Represents the size of the BillboardType enum.

BillboardType billboard_type = 1 🔗

void set_billboard_type(value: BillboardType)

BillboardType get_billboard_type()

Controls how the object faces the camera.

bool keep_scale = false 🔗

void set_keep_scale_enabled(value: bool)

bool is_keep_scale_enabled()

If true, the shader will keep the scale set for the mesh. Otherwise, the scale is lost when billboarding.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeBooleanConstant

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodebooleanconstant.html

**Contents:**
- VisualShaderNodeBooleanConstant
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeConstant < VisualShaderNode < Resource < RefCounted < Object

A boolean constant to be used within the visual shader graph.

Has only one output port and no inputs.

Translated to bool in the shader language.

bool constant = false 🔗

void set_constant(value: bool)

A boolean constant which represents a state of this node.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeBooleanParameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodebooleanparameter.html

**Contents:**
- VisualShaderNodeBooleanParameter
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

A boolean parameter to be used within the visual shader graph.

Translated to uniform bool in the shader language.

default_value_enabled

bool default_value = false 🔗

void set_default_value(value: bool)

bool get_default_value()

A default value to be assigned within the shader.

bool default_value_enabled = false 🔗

void set_default_value_enabled(value: bool)

bool is_default_value_enabled()

Enables usage of the default_value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeClamp

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeclamp.html

**Contents:**
- VisualShaderNodeClamp
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Clamps a value within the visual shader graph.

Constrains a value to lie between min and max values.

OpType OP_TYPE_FLOAT = 0

A floating-point scalar.

OpType OP_TYPE_INT = 1

OpType OP_TYPE_UINT = 2

An unsigned integer scalar.

OpType OP_TYPE_VECTOR_2D = 3

OpType OP_TYPE_VECTOR_3D = 4

OpType OP_TYPE_VECTOR_4D = 5

OpType OP_TYPE_MAX = 6

Represents the size of the OpType enum.

void set_op_type(value: OpType)

A type of operands and returned value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeColorConstant

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodecolorconstant.html

**Contents:**
- VisualShaderNodeColorConstant
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeConstant < VisualShaderNode < Resource < RefCounted < Object

A Color constant to be used within the visual shader graph.

Has two output ports representing RGB and alpha channels of Color.

Translated to vec3 rgb and float alpha in the shader language.

Color constant = Color(1, 1, 1, 1) 🔗

void set_constant(value: Color)

A Color constant which represents a state of this node.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeColorFunc

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodecolorfunc.html

**Contents:**
- VisualShaderNodeColorFunc
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A Color function to be used within the visual shader graph.

Accept a Color to the input port and transform it according to function.

Function FUNC_GRAYSCALE = 0

Converts the color to grayscale using the following formula:

Function FUNC_HSV2RGB = 1

Converts HSV vector to RGB equivalent.

Function FUNC_RGB2HSV = 2

Converts RGB vector to HSV equivalent.

Function FUNC_SEPIA = 3

Applies sepia tone effect using the following formula:

Function FUNC_LINEAR_TO_SRGB = 4

Converts color from linear color space to sRGB color space using the following formula:

The Compatibility renderer uses a simpler formula:

Function FUNC_SRGB_TO_LINEAR = 5

Converts color from sRGB color space to linear color space using the following formula:

The Compatibility renderer uses a simpler formula:

Function FUNC_MAX = 6

Represents the size of the Function enum.

Function function = 0 🔗

void set_function(value: Function)

Function get_function()

A function to be applied to the input color.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
vec3 c = input;
float max1 = max(c.r, c.g);
float max2 = max(max1, c.b);
float max3 = max(max1, max2);
return vec3(max3, max3, max3);
```

Example 2 (unknown):
```unknown
vec3 c = input;
float r = (c.r * 0.393) + (c.g * 0.769) + (c.b * 0.189);
float g = (c.r * 0.349) + (c.g * 0.686) + (c.b * 0.168);
float b = (c.r * 0.272) + (c.g * 0.534) + (c.b * 0.131);
return vec3(r, g, b);
```

Example 3 (unknown):
```unknown
vec3 c = clamp(c, vec3(0.0), vec3(1.0));
const vec3 a = vec3(0.055f);
return mix((vec3(1.0f) + a) * pow(c.rgb, vec3(1.0f / 2.4f)) - a, 12.92f * c.rgb, lessThan(c.rgb, vec3(0.0031308f)));
```

Example 4 (unknown):
```unknown
vec3 c = input;
return max(vec3(1.055) * pow(c, vec3(0.416666667)) - vec3(0.055), vec3(0.0));
```

---

## VisualShaderNodeColorOp

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodecolorop.html

**Contents:**
- VisualShaderNodeColorOp
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A Color operator to be used within the visual shader graph.

Applies operator to two color inputs.

Operator OP_SCREEN = 0

Produce a screen effect with the following formula:

Operator OP_DIFFERENCE = 1

Produce a difference effect with the following formula:

Operator OP_DARKEN = 2

Produce a darken effect with the following formula:

Operator OP_LIGHTEN = 3

Produce a lighten effect with the following formula:

Operator OP_OVERLAY = 4

Produce an overlay effect with the following formula:

Operator OP_DODGE = 5

Produce a dodge effect with the following formula:

Produce a burn effect with the following formula:

Operator OP_SOFT_LIGHT = 7

Produce a soft light effect with the following formula:

Operator OP_HARD_LIGHT = 8

Produce a hard light effect with the following formula:

Represents the size of the Operator enum.

Operator operator = 0 🔗

void set_operator(value: Operator)

Operator get_operator()

An operator to be applied to the inputs.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
result = vec3(1.0) - (vec3(1.0) - a) * (vec3(1.0) - b);
```

Example 2 (unknown):
```unknown
result = abs(a - b);
```

Example 3 (unknown):
```unknown
result = min(a, b);
```

Example 4 (unknown):
```unknown
result = max(a, b);
```

---

## VisualShaderNodeColorParameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodecolorparameter.html

**Contents:**
- VisualShaderNodeColorParameter
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

A Color parameter to be used within the visual shader graph.

Translated to uniform vec4 in the shader language.

default_value_enabled

Color default_value = Color(1, 1, 1, 1) 🔗

void set_default_value(value: Color)

Color get_default_value()

A default value to be assigned within the shader.

bool default_value_enabled = false 🔗

void set_default_value_enabled(value: bool)

bool is_default_value_enabled()

Enables usage of the default_value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeComment

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodecomment.html

**Contents:**
- VisualShaderNodeComment
- Description
- Properties
- Property Descriptions
- User-contributed notes

Deprecated: This class has no function anymore and only exists for compatibility.

Inherits: VisualShaderNodeFrame < VisualShaderNodeResizableBase < VisualShaderNode < Resource < RefCounted < Object

Only exists for compatibility. Use VisualShaderNodeFrame as a replacement.

This node was replaced by VisualShaderNodeFrame and only exists to preserve compatibility. In the VisualShader editor it behaves exactly like VisualShaderNodeFrame.

String description = "" 🔗

void set_description(value: String)

String get_description()

This property only exists to preserve data authored in earlier versions of Godot. It has currently no function.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeCompare

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodecompare.html

**Contents:**
- VisualShaderNodeCompare
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A comparison function for common types within the visual shader graph.

Compares a and b of type by function. Returns a boolean scalar. Translates to if instruction in shader code.

enum ComparisonType: 🔗

ComparisonType CTYPE_SCALAR = 0

A floating-point scalar.

ComparisonType CTYPE_SCALAR_INT = 1

ComparisonType CTYPE_SCALAR_UINT = 2

An unsigned integer scalar.

ComparisonType CTYPE_VECTOR_2D = 3

ComparisonType CTYPE_VECTOR_3D = 4

ComparisonType CTYPE_VECTOR_4D = 5

ComparisonType CTYPE_BOOLEAN = 6

ComparisonType CTYPE_TRANSFORM = 7

A transform (mat4) type.

ComparisonType CTYPE_MAX = 8

Represents the size of the ComparisonType enum.

Function FUNC_EQUAL = 0

Comparison for equality (a == b).

Function FUNC_NOT_EQUAL = 1

Comparison for inequality (a != b).

Function FUNC_GREATER_THAN = 2

Comparison for greater than (a > b). Cannot be used if type set to CTYPE_BOOLEAN or CTYPE_TRANSFORM.

Function FUNC_GREATER_THAN_EQUAL = 3

Comparison for greater than or equal (a >= b). Cannot be used if type set to CTYPE_BOOLEAN or CTYPE_TRANSFORM.

Function FUNC_LESS_THAN = 4

Comparison for less than (a < b). Cannot be used if type set to CTYPE_BOOLEAN or CTYPE_TRANSFORM.

Function FUNC_LESS_THAN_EQUAL = 5

Comparison for less than or equal (a <= b). Cannot be used if type set to CTYPE_BOOLEAN or CTYPE_TRANSFORM.

Function FUNC_MAX = 6

Represents the size of the Function enum.

Condition COND_ALL = 0

The result will be true if all components in the vector satisfy the comparison condition.

Condition COND_ANY = 1

The result will be true if any component in the vector satisfies the comparison condition.

Condition COND_MAX = 2

Represents the size of the Condition enum.

Condition condition = 0 🔗

void set_condition(value: Condition)

Condition get_condition()

Extra condition which is applied if type is set to CTYPE_VECTOR_3D.

Function function = 0 🔗

void set_function(value: Function)

Function get_function()

A comparison function.

ComparisonType type = 0 🔗

void set_comparison_type(value: ComparisonType)

ComparisonType get_comparison_type()

The type to be used in the comparison.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeConstant

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeconstant.html

**Contents:**
- VisualShaderNodeConstant
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeBooleanConstant, VisualShaderNodeColorConstant, VisualShaderNodeFloatConstant, VisualShaderNodeIntConstant, VisualShaderNodeTransformConstant, VisualShaderNodeUIntConstant, VisualShaderNodeVec2Constant, VisualShaderNodeVec3Constant, VisualShaderNodeVec4Constant

A base type for the constants within the visual shader graph.

This is an abstract class. See the derived types for descriptions of the possible values.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeCubemapParameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodecubemapparameter.html

**Contents:**
- VisualShaderNodeCubemapParameter
- Description
- User-contributed notes

Inherits: VisualShaderNodeTextureParameter < VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

A Cubemap parameter node to be used within the visual shader graph.

Translated to uniform samplerCube in the shader language. The output value can be used as port for VisualShaderNodeCubemap.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeCubemap

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodecubemap.html

**Contents:**
- VisualShaderNodeCubemap
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A Cubemap sampling node to be used within the visual shader graph.

Translated to texture(cubemap, vec3) in the shader language. Returns a color vector and alpha channel as scalar.

Source SOURCE_TEXTURE = 0

Use the Cubemap set via cube_map. If this is set to source, the samplerCube port is ignored.

Source SOURCE_PORT = 1

Use the Cubemap sampler reference passed via the samplerCube port. If this is set to source, the cube_map texture is ignored.

Source SOURCE_MAX = 2

Represents the size of the Source enum.

TextureType TYPE_DATA = 0

No hints are added to the uniform declaration.

TextureType TYPE_COLOR = 1

Adds source_color as hint to the uniform declaration for proper sRGB to linear conversion.

TextureType TYPE_NORMAL_MAP = 2

Adds hint_normal as hint to the uniform declaration, which internally converts the texture for proper usage as normal map.

TextureType TYPE_MAX = 3

Represents the size of the TextureType enum.

TextureLayered cube_map 🔗

void set_cube_map(value: TextureLayered)

TextureLayered get_cube_map()

The Cubemap texture to sample when using SOURCE_TEXTURE as source.

void set_source(value: Source)

Defines which source should be used for the sampling.

TextureType texture_type = 0 🔗

void set_texture_type(value: TextureType)

TextureType get_texture_type()

Defines the type of data provided by the source texture.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeCurveTexture

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodecurvetexture.html

**Contents:**
- VisualShaderNodeCurveTexture
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeResizableBase < VisualShaderNode < Resource < RefCounted < Object

Performs a CurveTexture lookup within the visual shader graph.

Comes with a built-in editor for texture's curves.

CurveTexture texture 🔗

void set_texture(value: CurveTexture)

CurveTexture get_texture()

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeCurveXYZTexture

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodecurvexyztexture.html

**Contents:**
- VisualShaderNodeCurveXYZTexture
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeResizableBase < VisualShaderNode < Resource < RefCounted < Object

Performs a CurveXYZTexture lookup within the visual shader graph.

Comes with a built-in editor for texture's curves.

CurveXYZTexture texture 🔗

void set_texture(value: CurveXYZTexture)

CurveXYZTexture get_texture()

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeCustom

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodecustom.html

**Contents:**
- VisualShaderNodeCustom
- Description
- Tutorials
- Methods
- Method Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Virtual class to define custom VisualShaderNodes for use in the Visual Shader Editor.

By inheriting this class you can create a custom VisualShader script addon which will be automatically added to the Visual Shader Editor. The VisualShaderNode's behavior is defined by overriding the provided virtual methods.

In order for the node to be registered as an editor addon, you must use the @tool annotation and provide a class_name for your custom script. For example:

Visual Shader plugins

_get_category() virtual const

_get_code(input_vars: Array[String], output_vars: Array[String], mode: Mode, type: Type) virtual const

_get_default_input_port(type: PortType) virtual const

_get_description() virtual const

_get_func_code(mode: Mode, type: Type) virtual const

_get_global_code(mode: Mode) virtual const

_get_input_port_count() virtual const

_get_input_port_default_value(port: int) virtual const

_get_input_port_name(port: int) virtual const

_get_input_port_type(port: int) virtual const

_get_name() virtual const

_get_output_port_count() virtual const

_get_output_port_name(port: int) virtual const

_get_output_port_type(port: int) virtual const

_get_property_count() virtual const

_get_property_default_index(index: int) virtual const

_get_property_name(index: int) virtual const

_get_property_options(index: int) virtual const

_get_return_icon_type() virtual const

_is_available(mode: Mode, type: Type) virtual const

_is_highend() virtual const

get_option_index(option: int) const

String _get_category() virtual const 🔗

Override this method to define the path to the associated custom node in the Visual Shader Editor's members dialog. The path may look like "MyGame/MyFunctions/Noise".

Defining this method is optional. If not overridden, the node will be filed under the "Addons" category.

String _get_code(input_vars: Array[String], output_vars: Array[String], mode: Mode, type: Type) virtual const 🔗

Override this method to define the actual shader code of the associated custom node. The shader code should be returned as a string, which can have multiple lines (the """ multiline string construct can be used for convenience).

The input_vars and output_vars arrays contain the string names of the various input and output variables, as defined by _get_input_* and _get_output_* virtual methods in this class.

The output ports can be assigned values in the shader code. For example, return output_vars[0] + " = " + input_vars[0] + ";".

You can customize the generated code based on the shader mode and/or type.

Defining this method is required.

int _get_default_input_port(type: PortType) virtual const 🔗

Override this method to define the input port which should be connected by default when this node is created as a result of dragging a connection from an existing node to the empty space on the graph.

Defining this method is optional. If not overridden, the connection will be created to the first valid port.

String _get_description() virtual const 🔗

Override this method to define the description of the associated custom node in the Visual Shader Editor's members dialog.

Defining this method is optional.

String _get_func_code(mode: Mode, type: Type) virtual const 🔗

Override this method to add a shader code to the beginning of each shader function (once). The shader code should be returned as a string, which can have multiple lines (the """ multiline string construct can be used for convenience).

If there are multiple custom nodes of different types which use this feature the order of each insertion is undefined.

You can customize the generated code based on the shader mode and/or type.

Defining this method is optional.

String _get_global_code(mode: Mode) virtual const 🔗

Override this method to add shader code on top of the global shader, to define your own standard library of reusable methods, varyings, constants, uniforms, etc. The shader code should be returned as a string, which can have multiple lines (the """ multiline string construct can be used for convenience).

Be careful with this functionality as it can cause name conflicts with other custom nodes, so be sure to give the defined entities unique names.

You can customize the generated code based on the shader mode.

Defining this method is optional.

int _get_input_port_count() virtual const 🔗

Override this method to define the number of input ports of the associated custom node.

Defining this method is required. If not overridden, the node has no input ports.

Variant _get_input_port_default_value(port: int) virtual const 🔗

Override this method to define the default value for the specified input port. Prefer use this over VisualShaderNode.set_input_port_default_value().

Defining this method is required. If not overridden, the node has no default values for their input ports.

String _get_input_port_name(port: int) virtual const 🔗

Override this method to define the names of input ports of the associated custom node. The names are used both for the input slots in the editor and as identifiers in the shader code, and are passed in the input_vars array in _get_code().

Defining this method is optional, but recommended. If not overridden, input ports are named as "in" + str(port).

PortType _get_input_port_type(port: int) virtual const 🔗

Override this method to define the returned type of each input port of the associated custom node.

Defining this method is optional, but recommended. If not overridden, input ports will return the VisualShaderNode.PORT_TYPE_SCALAR type.

String _get_name() virtual const 🔗

Override this method to define the name of the associated custom node in the Visual Shader Editor's members dialog and graph.

Defining this method is optional, but recommended. If not overridden, the node will be named as "Unnamed".

int _get_output_port_count() virtual const 🔗

Override this method to define the number of output ports of the associated custom node.

Defining this method is required. If not overridden, the node has no output ports.

String _get_output_port_name(port: int) virtual const 🔗

Override this method to define the names of output ports of the associated custom node. The names are used both for the output slots in the editor and as identifiers in the shader code, and are passed in the output_vars array in _get_code().

Defining this method is optional, but recommended. If not overridden, output ports are named as "out" + str(port).

PortType _get_output_port_type(port: int) virtual const 🔗

Override this method to define the returned type of each output port of the associated custom node.

Defining this method is optional, but recommended. If not overridden, output ports will return the VisualShaderNode.PORT_TYPE_SCALAR type.

int _get_property_count() virtual const 🔗

Override this method to define the number of the properties.

Defining this method is optional.

int _get_property_default_index(index: int) virtual const 🔗

Override this method to define the default index of the property of the associated custom node.

Defining this method is optional.

String _get_property_name(index: int) virtual const 🔗

Override this method to define the names of the property of the associated custom node.

Defining this method is optional.

PackedStringArray _get_property_options(index: int) virtual const 🔗

Override this method to define the options inside the drop-down list property of the associated custom node.

Defining this method is optional.

PortType _get_return_icon_type() virtual const 🔗

Override this method to define the return icon of the associated custom node in the Visual Shader Editor's members dialog.

Defining this method is optional. If not overridden, no return icon is shown.

bool _is_available(mode: Mode, type: Type) virtual const 🔗

Override this method to prevent the node to be visible in the member dialog for the certain mode and/or type.

Defining this method is optional. If not overridden, it's true.

bool _is_highend() virtual const 🔗

Override this method to enable high-end mark in the Visual Shader Editor's members dialog.

Defining this method is optional. If not overridden, it's false.

int get_option_index(option: int) const 🔗

Returns the selected index of the drop-down list option within a graph. You may use this function to define the specific behavior in the _get_code() or _get_global_code().

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
@tool
extends VisualShaderNodeCustom
class_name VisualShaderNodeNoise
```

---

## VisualShaderNodeDerivativeFunc

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodederivativefunc.html

**Contents:**
- VisualShaderNodeDerivativeFunc
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Calculates a derivative within the visual shader graph.

This node is only available in Fragment and Light visual shaders.

OpType OP_TYPE_SCALAR = 0

A floating-point scalar.

OpType OP_TYPE_VECTOR_2D = 1

OpType OP_TYPE_VECTOR_3D = 2

OpType OP_TYPE_VECTOR_4D = 3

OpType OP_TYPE_MAX = 4

Represents the size of the OpType enum.

Function FUNC_SUM = 0

Sum of absolute derivative in x and y.

Derivative in x using local differencing.

Derivative in y using local differencing.

Function FUNC_MAX = 3

Represents the size of the Function enum.

Precision PRECISION_NONE = 0

No precision is specified, the GPU driver is allowed to use whatever level of precision it chooses. This is the default option and is equivalent to using dFdx() or dFdy() in text shaders.

Precision PRECISION_COARSE = 1

The derivative will be calculated using the current fragment's neighbors (which may not include the current fragment). This tends to be faster than using PRECISION_FINE, but may not be suitable when more precision is needed. This is equivalent to using dFdxCoarse() or dFdyCoarse() in text shaders.

Precision PRECISION_FINE = 2

The derivative will be calculated using the current fragment and its immediate neighbors. This tends to be slower than using PRECISION_COARSE, but may be necessary when more precision is needed. This is equivalent to using dFdxFine() or dFdyFine() in text shaders.

Precision PRECISION_MAX = 3

Represents the size of the Precision enum.

Function function = 0 🔗

void set_function(value: Function)

Function get_function()

A derivative function type.

void set_op_type(value: OpType)

A type of operands and returned value.

Precision precision = 0 🔗

void set_precision(value: Precision)

Precision get_precision()

Sets the level of precision to use for the derivative function. When using the Compatibility renderer, this setting has no effect.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeDeterminant

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodedeterminant.html

**Contents:**
- VisualShaderNodeDeterminant
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Calculates the determinant of a Transform3D within the visual shader graph.

Translates to determinant(x) in the shader language.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeDistanceFade

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodedistancefade.html

**Contents:**
- VisualShaderNodeDistanceFade
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node representing distance fade effect.

The distance fade effect fades out each pixel based on its distance to another object.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeDotProduct

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodedotproduct.html

**Contents:**
- VisualShaderNodeDotProduct
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Calculates a dot product of two vectors within the visual shader graph.

Translates to dot(a, b) in the shader language.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeExpression

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeexpression.html

**Contents:**
- VisualShaderNodeExpression
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeGroupBase < VisualShaderNodeResizableBase < VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeGlobalExpression

A custom visual shader graph expression written in Godot Shading Language.

Custom Godot Shading Language expression, with a custom number of input and output ports.

The provided code is directly injected into the graph's matching shader function (vertex, fragment, or light), so it cannot be used to declare functions, varyings, uniforms, or global constants. See VisualShaderNodeGlobalExpression for such global definitions.

String expression = "" 🔗

void set_expression(value: String)

String get_expression()

An expression in Godot Shading Language, which will be injected at the start of the graph's matching shader function (vertex, fragment, or light), and thus cannot be used to declare functions, varyings, uniforms, or global constants.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeFaceForward

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodefaceforward.html

**Contents:**
- VisualShaderNodeFaceForward
- Description
- User-contributed notes

Inherits: VisualShaderNodeVectorBase < VisualShaderNode < Resource < RefCounted < Object

Returns the vector that points in the same direction as a reference vector within the visual shader graph.

Translates to faceforward(N, I, Nref) in the shader language. The function has three vector parameters: N, the vector to orient, I, the incident vector, and Nref, the reference vector. If the dot product of I and Nref is smaller than zero the return value is N. Otherwise, -N is returned.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeFloatConstant

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodefloatconstant.html

**Contents:**
- VisualShaderNodeFloatConstant
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeConstant < VisualShaderNode < Resource < RefCounted < Object

A scalar floating-point constant to be used within the visual shader graph.

Translated to float in the shader language.

float constant = 0.0 🔗

void set_constant(value: float)

A floating-point constant which represents a state of this node.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeFloatFunc

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodefloatfunc.html

**Contents:**
- VisualShaderNodeFloatFunc
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A scalar floating-point function to be used within the visual shader graph.

Accept a floating-point scalar (x) to the input port and transform it according to function.

Function FUNC_SIN = 0

Returns the sine of the parameter. Translates to sin(x) in the Godot Shader Language.

Function FUNC_COS = 1

Returns the cosine of the parameter. Translates to cos(x) in the Godot Shader Language.

Function FUNC_TAN = 2

Returns the tangent of the parameter. Translates to tan(x) in the Godot Shader Language.

Function FUNC_ASIN = 3

Returns the arc-sine of the parameter. Translates to asin(x) in the Godot Shader Language.

Function FUNC_ACOS = 4

Returns the arc-cosine of the parameter. Translates to acos(x) in the Godot Shader Language.

Function FUNC_ATAN = 5

Returns the arc-tangent of the parameter. Translates to atan(x) in the Godot Shader Language.

Function FUNC_SINH = 6

Returns the hyperbolic sine of the parameter. Translates to sinh(x) in the Godot Shader Language.

Function FUNC_COSH = 7

Returns the hyperbolic cosine of the parameter. Translates to cosh(x) in the Godot Shader Language.

Function FUNC_TANH = 8

Returns the hyperbolic tangent of the parameter. Translates to tanh(x) in the Godot Shader Language.

Function FUNC_LOG = 9

Returns the natural logarithm of the parameter. Translates to log(x) in the Godot Shader Language.

Function FUNC_EXP = 10

Returns the natural exponentiation of the parameter. Translates to exp(x) in the Godot Shader Language.

Function FUNC_SQRT = 11

Returns the square root of the parameter. Translates to sqrt(x) in the Godot Shader Language.

Function FUNC_ABS = 12

Returns the absolute value of the parameter. Translates to abs(x) in the Godot Shader Language.

Function FUNC_SIGN = 13

Extracts the sign of the parameter. Translates to sign(x) in the Godot Shader Language.

Function FUNC_FLOOR = 14

Finds the nearest integer less than or equal to the parameter. Translates to floor(x) in the Godot Shader Language.

Function FUNC_ROUND = 15

Finds the nearest integer to the parameter. Translates to round(x) in the Godot Shader Language.

Function FUNC_CEIL = 16

Finds the nearest integer that is greater than or equal to the parameter. Translates to ceil(x) in the Godot Shader Language.

Function FUNC_FRACT = 17

Computes the fractional part of the argument. Translates to fract(x) in the Godot Shader Language.

Function FUNC_SATURATE = 18

Clamps the value between 0.0 and 1.0 using min(max(x, 0.0), 1.0).

Function FUNC_NEGATE = 19

Negates the x using -(x).

Function FUNC_ACOSH = 20

Returns the arc-hyperbolic-cosine of the parameter. Translates to acosh(x) in the Godot Shader Language.

Function FUNC_ASINH = 21

Returns the arc-hyperbolic-sine of the parameter. Translates to asinh(x) in the Godot Shader Language.

Function FUNC_ATANH = 22

Returns the arc-hyperbolic-tangent of the parameter. Translates to atanh(x) in the Godot Shader Language.

Function FUNC_DEGREES = 23

Convert a quantity in radians to degrees. Translates to degrees(x) in the Godot Shader Language.

Function FUNC_EXP2 = 24

Returns 2 raised by the power of the parameter. Translates to exp2(x) in the Godot Shader Language.

Function FUNC_INVERSE_SQRT = 25

Returns the inverse of the square root of the parameter. Translates to inversesqrt(x) in the Godot Shader Language.

Function FUNC_LOG2 = 26

Returns the base 2 logarithm of the parameter. Translates to log2(x) in the Godot Shader Language.

Function FUNC_RADIANS = 27

Convert a quantity in degrees to radians. Translates to radians(x) in the Godot Shader Language.

Function FUNC_RECIPROCAL = 28

Finds reciprocal value of dividing 1 by x (i.e. 1 / x).

Function FUNC_ROUNDEVEN = 29

Finds the nearest even integer to the parameter. Translates to roundEven(x) in the Godot Shader Language.

Function FUNC_TRUNC = 30

Returns a value equal to the nearest integer to x whose absolute value is not larger than the absolute value of x. Translates to trunc(x) in the Godot Shader Language.

Function FUNC_ONEMINUS = 31

Subtracts scalar x from 1 (i.e. 1 - x).

Function FUNC_MAX = 32

Represents the size of the Function enum.

Function function = 13 🔗

void set_function(value: Function)

Function get_function()

A function to be applied to the scalar.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeFloatOp

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodefloatop.html

**Contents:**
- VisualShaderNodeFloatOp
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A floating-point scalar operator to be used within the visual shader graph.

Applies operator to two floating-point inputs: a and b.

Sums two numbers using a + b.

Subtracts two numbers using a - b.

Multiplies two numbers using a * b.

Divides two numbers using a / b.

Calculates the remainder of two numbers. Translates to mod(a, b) in the Godot Shader Language.

Raises the a to the power of b. Translates to pow(a, b) in the Godot Shader Language.

Returns the greater of two numbers. Translates to max(a, b) in the Godot Shader Language.

Returns the lesser of two numbers. Translates to min(a, b) in the Godot Shader Language.

Operator OP_ATAN2 = 8

Returns the arc-tangent of the parameters. Translates to atan(a, b) in the Godot Shader Language.

Generates a step function by comparing b(x) to a(edge). Returns 0.0 if x is smaller than edge and otherwise 1.0. Translates to step(a, b) in the Godot Shader Language.

Operator OP_ENUM_SIZE = 10

Represents the size of the Operator enum.

Operator operator = 0 🔗

void set_operator(value: Operator)

Operator get_operator()

An operator to be applied to the inputs.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeFloatParameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodefloatparameter.html

**Contents:**
- VisualShaderNodeFloatParameter
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

A scalar float parameter to be used within the visual shader graph.

Translated to uniform float in the shader language.

default_value_enabled

A range hint for scalar value, which limits possible input values between min and max. Translated to hint_range(min, max) in shader code.

Hint HINT_RANGE_STEP = 2

A range hint for scalar value with step, which limits possible input values between min and max, with a step (increment) of step). Translated to hint_range(min, max, step) in shader code.

Represents the size of the Hint enum.

float default_value = 0.0 🔗

void set_default_value(value: float)

float get_default_value()

A default value to be assigned within the shader.

bool default_value_enabled = false 🔗

void set_default_value_enabled(value: bool)

bool is_default_value_enabled()

Enables usage of the default_value.

void set_hint(value: Hint)

A hint applied to the uniform, which controls the values it can take when set through the Inspector.

void set_max(value: float)

Minimum value for range hints. Used if hint is set to HINT_RANGE or HINT_RANGE_STEP.

void set_min(value: float)

Maximum value for range hints. Used if hint is set to HINT_RANGE or HINT_RANGE_STEP.

void set_step(value: float)

Step (increment) value for the range hint with step. Used if hint is set to HINT_RANGE_STEP.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeFrame

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeframe.html

**Contents:**
- VisualShaderNodeFrame
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: VisualShaderNodeResizableBase < VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeComment

A frame other visual shader nodes can be attached to for better organization.

A rectangular frame that can be used to group visual shader nodes together to improve organization.

Nodes attached to the frame will move with it when it is dragged and it can automatically resize to enclose all attached nodes.

Its title, description and color can be customized.

Color(0.3, 0.3, 0.3, 0.75)

add_attached_node(node: int)

remove_attached_node(node: int)

PackedInt32Array attached_nodes = PackedInt32Array() 🔗

void set_attached_nodes(value: PackedInt32Array)

PackedInt32Array get_attached_nodes()

The list of nodes attached to the frame.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedInt32Array for more details.

bool autoshrink = true 🔗

void set_autoshrink_enabled(value: bool)

bool is_autoshrink_enabled()

If true, the frame will automatically resize to enclose all attached nodes.

Color tint_color = Color(0.3, 0.3, 0.3, 0.75) 🔗

void set_tint_color(value: Color)

Color get_tint_color()

The color of the frame when tint_color_enabled is true.

bool tint_color_enabled = false 🔗

void set_tint_color_enabled(value: bool)

bool is_tint_color_enabled()

If true, the frame will be tinted with the color specified in tint_color.

String title = "Title" 🔗

void set_title(value: String)

The title of the node.

void add_attached_node(node: int) 🔗

Adds a node to the list of nodes attached to the frame. Should not be called directly, use the VisualShader.attach_node_to_frame() method instead.

void remove_attached_node(node: int) 🔗

Removes a node from the list of nodes attached to the frame. Should not be called directly, use the VisualShader.detach_node_from_frame() method instead.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeFresnel

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodefresnel.html

**Contents:**
- VisualShaderNodeFresnel
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A Fresnel effect to be used within the visual shader graph.

Returns falloff based on the dot product of surface normal and view direction of camera (pass associated inputs to it).

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeGlobalExpression

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeglobalexpression.html

**Contents:**
- VisualShaderNodeGlobalExpression
- Description
- User-contributed notes

Inherits: VisualShaderNodeExpression < VisualShaderNodeGroupBase < VisualShaderNodeResizableBase < VisualShaderNode < Resource < RefCounted < Object

A custom global visual shader graph expression written in Godot Shading Language.

Custom Godot Shader Language expression, which is placed on top of the generated shader. You can place various function definitions inside to call later in VisualShaderNodeExpressions (which are injected in the main shader functions). You can also declare varyings, uniforms and global constants.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeGroupBase

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodegroupbase.html

**Contents:**
- VisualShaderNodeGroupBase
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: VisualShaderNodeResizableBase < VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeExpression

Base class for a family of nodes with variable number of input and output ports within the visual shader graph.

Currently, has no direct usage, use the derived classes instead.

add_input_port(id: int, type: int, name: String)

add_output_port(id: int, type: int, name: String)

get_free_input_port_id() const

get_free_output_port_id() const

get_input_port_count() const

get_output_port_count() const

has_input_port(id: int) const

has_output_port(id: int) const

is_valid_port_name(name: String) const

remove_input_port(id: int)

remove_output_port(id: int)

set_input_port_name(id: int, name: String)

set_input_port_type(id: int, type: int)

set_inputs(inputs: String)

set_output_port_name(id: int, name: String)

set_output_port_type(id: int, type: int)

set_outputs(outputs: String)

void add_input_port(id: int, type: int, name: String) 🔗

Adds an input port with the specified type (see PortType) and name.

void add_output_port(id: int, type: int, name: String) 🔗

Adds an output port with the specified type (see PortType) and name.

void clear_input_ports() 🔗

Removes all previously specified input ports.

void clear_output_ports() 🔗

Removes all previously specified output ports.

int get_free_input_port_id() const 🔗

Returns a free input port ID which can be used in add_input_port().

int get_free_output_port_id() const 🔗

Returns a free output port ID which can be used in add_output_port().

int get_input_port_count() const 🔗

Returns the number of input ports in use. Alternative for get_free_input_port_id().

String get_inputs() const 🔗

Returns a String description of the input ports as a colon-separated list using the format id,type,name; (see add_input_port()).

int get_output_port_count() const 🔗

Returns the number of output ports in use. Alternative for get_free_output_port_id().

String get_outputs() const 🔗

Returns a String description of the output ports as a colon-separated list using the format id,type,name; (see add_output_port()).

bool has_input_port(id: int) const 🔗

Returns true if the specified input port exists.

bool has_output_port(id: int) const 🔗

Returns true if the specified output port exists.

bool is_valid_port_name(name: String) const 🔗

Returns true if the specified port name does not override an existed port name and is valid within the shader.

void remove_input_port(id: int) 🔗

Removes the specified input port.

void remove_output_port(id: int) 🔗

Removes the specified output port.

void set_input_port_name(id: int, name: String) 🔗

Renames the specified input port.

void set_input_port_type(id: int, type: int) 🔗

Sets the specified input port's type (see PortType).

void set_inputs(inputs: String) 🔗

Defines all input ports using a String formatted as a colon-separated list: id,type,name; (see add_input_port()).

void set_output_port_name(id: int, name: String) 🔗

Renames the specified output port.

void set_output_port_type(id: int, type: int) 🔗

Sets the specified output port's type (see PortType).

void set_outputs(outputs: String) 🔗

Defines all output ports using a String formatted as a colon-separated list: id,type,name; (see add_output_port()).

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeIf

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeif.html

**Contents:**
- VisualShaderNodeIf
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Outputs a 3D vector based on the result of a floating-point comparison within the visual shader graph.

This visual shader node has six input ports:

Port 1 and 2 provide the two floating-point numbers a and b that will be compared.

Port 3 is the tolerance, which allows similar floating-point numbers to be considered equal.

Ports 4, 5, and 6 are the possible outputs, returned if a == b, a > b, or a < b respectively.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeInput

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeinput.html

**Contents:**
- VisualShaderNodeInput
- Description
- Tutorials
- Properties
- Methods
- Signals
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Represents the input shader parameter within the visual shader graph.

Gives access to input variables (built-ins) available for the shader. See the shading reference for the list of available built-ins for each shader type (check Tutorials section for link).

Shading reference index

get_input_real_name() const

input_type_changed() 🔗

Emitted when input is changed via input_name.

String input_name = "[None]" 🔗

void set_input_name(value: String)

String get_input_name()

One of the several input constants in lower-case style like: "vertex" (VERTEX) or "point_size" (POINT_SIZE).

String get_input_real_name() const 🔗

Returns a translated name of the current constant in the Godot Shader Language. E.g. "ALBEDO" if the input_name equal to "albedo".

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeIntConstant

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeintconstant.html

**Contents:**
- VisualShaderNodeIntConstant
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeConstant < VisualShaderNode < Resource < RefCounted < Object

A scalar integer constant to be used within the visual shader graph.

Translated to int in the shader language.

void set_constant(value: int)

An integer constant which represents a state of this node.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeIntFunc

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeintfunc.html

**Contents:**
- VisualShaderNodeIntFunc
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A scalar integer function to be used within the visual shader graph.

Accept an integer scalar (x) to the input port and transform it according to function.

Function FUNC_ABS = 0

Returns the absolute value of the parameter. Translates to abs(x) in the Godot Shader Language.

Function FUNC_NEGATE = 1

Negates the x using -(x).

Function FUNC_SIGN = 2

Extracts the sign of the parameter. Translates to sign(x) in the Godot Shader Language.

Function FUNC_BITWISE_NOT = 3

Returns the result of bitwise NOT operation on the integer. Translates to ~a in the Godot Shader Language.

Function FUNC_MAX = 4

Represents the size of the Function enum.

Function function = 2 🔗

void set_function(value: Function)

Function get_function()

A function to be applied to the scalar.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeIntOp

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeintop.html

**Contents:**
- VisualShaderNodeIntOp
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

An integer scalar operator to be used within the visual shader graph.

Applies operator to two integer inputs: a and b.

Sums two numbers using a + b.

Subtracts two numbers using a - b.

Multiplies two numbers using a * b.

Divides two numbers using a / b.

Calculates the remainder of two numbers using a % b.

Returns the greater of two numbers. Translates to max(a, b) in the Godot Shader Language.

Returns the lesser of two numbers. Translates to max(a, b) in the Godot Shader Language.

Operator OP_BITWISE_AND = 7

Returns the result of bitwise AND operation on the integer. Translates to a & b in the Godot Shader Language.

Operator OP_BITWISE_OR = 8

Returns the result of bitwise OR operation for two integers. Translates to a | b in the Godot Shader Language.

Operator OP_BITWISE_XOR = 9

Returns the result of bitwise XOR operation for two integers. Translates to a ^ b in the Godot Shader Language.

Operator OP_BITWISE_LEFT_SHIFT = 10

Returns the result of bitwise left shift operation on the integer. Translates to a << b in the Godot Shader Language.

Operator OP_BITWISE_RIGHT_SHIFT = 11

Returns the result of bitwise right shift operation on the integer. Translates to a >> b in the Godot Shader Language.

Operator OP_ENUM_SIZE = 12

Represents the size of the Operator enum.

Operator operator = 0 🔗

void set_operator(value: Operator)

Operator get_operator()

An operator to be applied to the inputs.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeIntParameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeintparameter.html

**Contents:**
- VisualShaderNodeIntParameter
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

A visual shader node for shader parameter (uniform) of type int.

A VisualShaderNodeParameter of type int. Offers additional customization for range of accepted values.

default_value_enabled

The parameter will not constrain its value.

The parameter's value must be within the specified min/max range.

Hint HINT_RANGE_STEP = 2

The parameter's value must be within the specified range, with the given step between values.

The parameter uses an enum to associate preset values to names in the editor.

Represents the size of the Hint enum.

int default_value = 0 🔗

void set_default_value(value: int)

int get_default_value()

Default value of this parameter, which will be used if not set externally. default_value_enabled must be enabled; defaults to 0 otherwise.

bool default_value_enabled = false 🔗

void set_default_value_enabled(value: bool)

bool is_default_value_enabled()

If true, the node will have a custom default value.

PackedStringArray enum_names = PackedStringArray() 🔗

void set_enum_names(value: PackedStringArray)

PackedStringArray get_enum_names()

The names used for the enum select in the editor. hint must be HINT_ENUM for this to take effect.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedStringArray for more details.

void set_hint(value: Hint)

Range hint of this node. Use it to customize valid parameter range.

void set_max(value: int)

The maximum value this parameter can take. hint must be either HINT_RANGE or HINT_RANGE_STEP for this to take effect.

void set_min(value: int)

The minimum value this parameter can take. hint must be either HINT_RANGE or HINT_RANGE_STEP for this to take effect.

void set_step(value: int)

The step between parameter's values. Forces the parameter to be a multiple of the given value. hint must be HINT_RANGE_STEP for this to take effect.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeIs

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeis.html

**Contents:**
- VisualShaderNodeIs
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A boolean comparison operator to be used within the visual shader graph.

Returns the boolean result of the comparison between INF or NaN and a scalar parameter.

Function FUNC_IS_INF = 0

Comparison with INF (Infinity).

Function FUNC_IS_NAN = 1

Comparison with NaN (Not a Number; indicates invalid numeric results, such as division by zero).

Function FUNC_MAX = 2

Represents the size of the Function enum.

Function function = 0 🔗

void set_function(value: Function)

Function get_function()

The comparison function.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeLinearSceneDepth

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodelinearscenedepth.html

**Contents:**
- VisualShaderNodeLinearSceneDepth
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node that returns the depth value of the DEPTH_TEXTURE node in a linear space.

This node can be used in fragment shaders.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeMix

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodemix.html

**Contents:**
- VisualShaderNodeMix
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Linearly interpolates between two values within the visual shader graph.

Translates to mix(a, b, weight) in the shader language.

OpType OP_TYPE_SCALAR = 0

A floating-point scalar.

OpType OP_TYPE_VECTOR_2D = 1

OpType OP_TYPE_VECTOR_2D_SCALAR = 2

The a and b ports use a 2D vector type. The weight port uses a scalar type.

OpType OP_TYPE_VECTOR_3D = 3

OpType OP_TYPE_VECTOR_3D_SCALAR = 4

The a and b ports use a 3D vector type. The weight port uses a scalar type.

OpType OP_TYPE_VECTOR_4D = 5

OpType OP_TYPE_VECTOR_4D_SCALAR = 6

The a and b ports use a 4D vector type. The weight port uses a scalar type.

OpType OP_TYPE_MAX = 7

Represents the size of the OpType enum.

void set_op_type(value: OpType)

A type of operands and returned value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeMultiplyAdd

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodemultiplyadd.html

**Contents:**
- VisualShaderNodeMultiplyAdd
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Performs a fused multiply-add operation within the visual shader graph.

Uses three operands to compute (a * b + c) expression.

OpType OP_TYPE_SCALAR = 0

A floating-point scalar type.

OpType OP_TYPE_VECTOR_2D = 1

OpType OP_TYPE_VECTOR_3D = 2

OpType OP_TYPE_VECTOR_4D = 3

OpType OP_TYPE_MAX = 4

Represents the size of the OpType enum.

void set_op_type(value: OpType)

A type of operands and returned value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeOuterProduct

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeouterproduct.html

**Contents:**
- VisualShaderNodeOuterProduct
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Calculates an outer product of two vectors within the visual shader graph.

OuterProduct treats the first parameter c as a column vector (matrix with one column) and the second parameter r as a row vector (matrix with one row) and does a linear algebraic matrix multiply c * r, yielding a matrix whose number of rows is the number of components in c and whose number of columns is the number of components in r.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeOutput

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeoutput.html

**Contents:**
- VisualShaderNodeOutput
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeParticleOutput

Represents the output shader parameters within the visual shader graph.

This visual shader node is present in all shader graphs in form of "Output" block with multiple output value ports.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParameterRef

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparameterref.html

**Contents:**
- VisualShaderNodeParameterRef
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A reference to an existing VisualShaderNodeParameter.

Creating a reference to a VisualShaderNodeParameter allows you to reuse this parameter in different shaders or shader stages easily.

String parameter_name = "[None]" 🔗

void set_parameter_name(value: String)

String get_parameter_name()

The name of the parameter which this reference points to.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparameter.html

**Contents:**
- VisualShaderNodeParameter
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeBooleanParameter, VisualShaderNodeColorParameter, VisualShaderNodeFloatParameter, VisualShaderNodeIntParameter, VisualShaderNodeTextureParameter, VisualShaderNodeTransformParameter, VisualShaderNodeUIntParameter, VisualShaderNodeVec2Parameter, VisualShaderNodeVec3Parameter, VisualShaderNodeVec4Parameter

A base type for the parameters within the visual shader graph.

A parameter represents a variable in the shader which is set externally, i.e. from the ShaderMaterial. Parameters are exposed as properties in the ShaderMaterial and can be assigned from the Inspector or from a script.

Qualifier QUAL_NONE = 0

The parameter will be tied to the ShaderMaterial using this shader.

Qualifier QUAL_GLOBAL = 1

The parameter will use a global value, defined in Project Settings.

Qualifier QUAL_INSTANCE = 2

The parameter will be tied to the node with attached ShaderMaterial using this shader.

Qualifier QUAL_MAX = 3

Represents the size of the Qualifier enum.

String parameter_name = "" 🔗

void set_parameter_name(value: String)

String get_parameter_name()

Name of the parameter, by which it can be accessed through the ShaderMaterial properties.

Qualifier qualifier = 0 🔗

void set_qualifier(value: Qualifier)

Qualifier get_qualifier()

Defines the scope of the parameter.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParticleAccelerator

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparticleaccelerator.html

**Contents:**
- VisualShaderNodeParticleAccelerator
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node that accelerates particles.

Particle accelerator can be used in "process" step of particle shader. It will accelerate the particles. Connect it to the Velocity output port.

The particles will be accelerated based on their velocity.

The particles will be accelerated towards or away from the center.

Mode MODE_TANGENTIAL = 2

The particles will be accelerated tangentially to the radius vector from center to their position.

Represents the size of the Mode enum.

void set_mode(value: Mode)

Defines in what manner the particles will be accelerated.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParticleBoxEmitter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparticleboxemitter.html

**Contents:**
- VisualShaderNodeParticleBoxEmitter
- Description
- User-contributed notes

Inherits: VisualShaderNodeParticleEmitter < VisualShaderNode < Resource < RefCounted < Object

A visual shader node that makes particles emitted in a box shape.

VisualShaderNodeParticleEmitter that makes the particles emitted in box shape with the specified extents.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParticleConeVelocity

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparticleconevelocity.html

**Contents:**
- VisualShaderNodeParticleConeVelocity
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node that makes particles move in a cone shape.

This node can be used in "start" step of particle shader. It defines the initial velocity of the particles, making them move in cone shape starting from the center, with a given spread.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParticleEmitter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparticleemitter.html

**Contents:**
- VisualShaderNodeParticleEmitter
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeParticleBoxEmitter, VisualShaderNodeParticleMeshEmitter, VisualShaderNodeParticleRingEmitter, VisualShaderNodeParticleSphereEmitter

A base class for particle emitters.

Particle emitter nodes can be used in "start" step of particle shaders and they define the starting position of the particles. Connect them to the Position output port.

bool mode_2d = false 🔗

void set_mode_2d(value: bool)

If true, the result of this emitter is projected to 2D space. By default it is false and meant for use in 3D space.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParticleEmit

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparticleemit.html

**Contents:**
- VisualShaderNodeParticleEmit
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node that forces to emit a particle from a sub-emitter.

This node internally calls emit_subparticle shader method. It will emit a particle from the configured sub-emitter and also allows to customize how its emitted. Requires a sub-emitter assigned to the particles node with this shader.

EmitFlags EMIT_FLAG_POSITION = 1

If enabled, the particle starts with the position defined by this node.

EmitFlags EMIT_FLAG_ROT_SCALE = 2

If enabled, the particle starts with the rotation and scale defined by this node.

EmitFlags EMIT_FLAG_VELOCITY = 4

If enabled,the particle starts with the velocity defined by this node.

EmitFlags EMIT_FLAG_COLOR = 8

If enabled, the particle starts with the color defined by this node.

EmitFlags EMIT_FLAG_CUSTOM = 16

If enabled, the particle starts with the CUSTOM data defined by this node.

EmitFlags flags = 31 🔗

void set_flags(value: EmitFlags)

EmitFlags get_flags()

Flags used to override the properties defined in the sub-emitter's process material.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParticleMultiplyByAxisAngle

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparticlemultiplybyaxisangle.html

**Contents:**
- VisualShaderNodeParticleMultiplyByAxisAngle
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader helper node for multiplying position and rotation of particles.

This node helps to multiply a position input vector by rotation using specific axis. Intended to work with emitters.

bool degrees_mode = true 🔗

void set_degrees_mode(value: bool)

bool is_degrees_mode()

If true, the angle will be interpreted in degrees instead of radians.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParticleOutput

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparticleoutput.html

**Contents:**
- VisualShaderNodeParticleOutput
- Description
- User-contributed notes

Inherits: VisualShaderNodeOutput < VisualShaderNode < Resource < RefCounted < Object

Visual shader node that defines output values for particle emitting.

This node defines how particles are emitted. It allows to customize e.g. position and velocity. Available ports are different depending on which function this node is inside (start, process, collision) and whether custom data is enabled.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParticleRandomness

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparticlerandomness.html

**Contents:**
- VisualShaderNodeParticleRandomness
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Visual shader node for randomizing particle values.

Randomness node will output pseudo-random values of the given type based on the specified minimum and maximum values.

OpType OP_TYPE_SCALAR = 0

A floating-point scalar.

OpType OP_TYPE_VECTOR_2D = 1

OpType OP_TYPE_VECTOR_3D = 2

OpType OP_TYPE_VECTOR_4D = 3

OpType OP_TYPE_MAX = 4

Represents the size of the OpType enum.

void set_op_type(value: OpType)

A type of operands and returned value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParticleRingEmitter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparticleringemitter.html

**Contents:**
- VisualShaderNodeParticleRingEmitter
- Description
- User-contributed notes

Inherits: VisualShaderNodeParticleEmitter < VisualShaderNode < Resource < RefCounted < Object

A visual shader node that makes particles emitted in a ring shape.

VisualShaderNodeParticleEmitter that makes the particles emitted in ring shape with the specified inner and outer radii and height.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeParticleSphereEmitter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeparticlesphereemitter.html

**Contents:**
- VisualShaderNodeParticleSphereEmitter
- Description
- User-contributed notes

Inherits: VisualShaderNodeParticleEmitter < VisualShaderNode < Resource < RefCounted < Object

A visual shader node that makes particles emitted in a sphere shape.

VisualShaderNodeParticleEmitter that makes the particles emitted in sphere shape with the specified inner and outer radii.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeProximityFade

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeproximityfade.html

**Contents:**
- VisualShaderNodeProximityFade
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node representing proximity fade effect.

The proximity fade effect fades out each pixel based on its distance to another object.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeRandomRange

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernoderandomrange.html

**Contents:**
- VisualShaderNodeRandomRange
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node that generates a pseudo-random scalar.

Random range node will output a pseudo-random scalar value in the specified range, based on the seed. The value is always the same for the given seed and range, so you should provide a changing input, e.g. by using time.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeRemap

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernoderemap.html

**Contents:**
- VisualShaderNodeRemap
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node for remap function.

Remap will transform the input range into output range, e.g. you can change a 0..1 value to -2..2 etc. See @GlobalScope.remap() for more details.

OpType OP_TYPE_SCALAR = 0

A floating-point scalar type.

OpType OP_TYPE_VECTOR_2D = 1

OpType OP_TYPE_VECTOR_2D_SCALAR = 2

The value port uses a 2D vector type, while the input min, input max, output min, and output max ports use a floating-point scalar type.

OpType OP_TYPE_VECTOR_3D = 3

OpType OP_TYPE_VECTOR_3D_SCALAR = 4

The value port uses a 3D vector type, while the input min, input max, output min, and output max ports use a floating-point scalar type.

OpType OP_TYPE_VECTOR_4D = 5

OpType OP_TYPE_VECTOR_4D_SCALAR = 6

The value port uses a 4D vector type, while the input min, input max, output min, and output max ports use a floating-point scalar type.

OpType OP_TYPE_MAX = 7

Represents the size of the OpType enum.

void set_op_type(value: OpType)

There is currently no description for this property. Please help us by contributing one!

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeReroute

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodereroute.html

**Contents:**
- VisualShaderNodeReroute
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A node that allows rerouting a connection within the visual shader graph.

Automatically adapts its port type to the type of the incoming connection and ensures valid connections.

get_port_type() const

PortType get_port_type() const 🔗

Returns the port type of the reroute node.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeResizableBase

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernoderesizablebase.html

**Contents:**
- VisualShaderNodeResizableBase
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeCurveTexture, VisualShaderNodeCurveXYZTexture, VisualShaderNodeFrame, VisualShaderNodeGroupBase

Base class for resizable nodes in a visual shader graph.

Resizable nodes have a handle that allows the user to adjust their size as needed.

Vector2 size = Vector2(0, 0) 🔗

void set_size(value: Vector2)

The size of the node in the visual shader graph.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeRotationByAxis

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernoderotationbyaxis.html

**Contents:**
- VisualShaderNodeRotationByAxis
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node that modifies the rotation of the object using a rotation matrix.

RotationByAxis node will transform the vertices of a mesh with specified axis and angle in radians. It can be used to rotate an object in an arbitrary axis.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTextureParameterTriplanar

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetextureparametertriplanar.html

**Contents:**
- VisualShaderNodeTextureParameterTriplanar
- Description
- User-contributed notes

Inherits: VisualShaderNodeTextureParameter < VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

Performs a uniform texture lookup with triplanar within the visual shader graph.

Performs a lookup operation on the texture provided as a uniform for the shader, with support for triplanar mapping.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTextureParameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetextureparameter.html

**Contents:**
- VisualShaderNodeTextureParameter
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeCubemapParameter, VisualShaderNodeTexture2DArrayParameter, VisualShaderNodeTexture2DParameter, VisualShaderNodeTexture3DParameter, VisualShaderNodeTextureParameterTriplanar

Performs a uniform texture lookup within the visual shader graph.

Performs a lookup operation on the texture provided as a uniform for the shader.

TextureType TYPE_DATA = 0

No hints are added to the uniform declaration.

TextureType TYPE_COLOR = 1

Adds source_color as hint to the uniform declaration for proper sRGB to linear conversion.

TextureType TYPE_NORMAL_MAP = 2

Adds hint_normal as hint to the uniform declaration, which internally converts the texture for proper usage as normal map.

TextureType TYPE_ANISOTROPY = 3

Adds hint_anisotropy as hint to the uniform declaration to use for a flowmap.

TextureType TYPE_MAX = 4

Represents the size of the TextureType enum.

ColorDefault COLOR_DEFAULT_WHITE = 0

Defaults to fully opaque white color.

ColorDefault COLOR_DEFAULT_BLACK = 1

Defaults to fully opaque black color.

ColorDefault COLOR_DEFAULT_TRANSPARENT = 2

Defaults to fully transparent black color.

ColorDefault COLOR_DEFAULT_MAX = 3

Represents the size of the ColorDefault enum.

enum TextureFilter: 🔗

TextureFilter FILTER_DEFAULT = 0

Sample the texture using the filter determined by the node this shader is attached to.

TextureFilter FILTER_NEAREST = 1

The texture filter reads from the nearest pixel only. This makes the texture look pixelated from up close, and grainy from a distance (due to mipmaps not being sampled).

TextureFilter FILTER_LINEAR = 2

The texture filter blends between the nearest 4 pixels. This makes the texture look smooth from up close, and grainy from a distance (due to mipmaps not being sampled).

TextureFilter FILTER_NEAREST_MIPMAP = 3

The texture filter reads from the nearest pixel and blends between the nearest 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true). This makes the texture look pixelated from up close, and smooth from a distance.

Use this for non-pixel art textures that may be viewed at a low scale (e.g. due to Camera2D zoom or sprite scaling), as mipmaps are important to smooth out pixels that are smaller than on-screen pixels.

TextureFilter FILTER_LINEAR_MIPMAP = 4

The texture filter blends between the nearest 4 pixels and between the nearest 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true). This makes the texture look smooth from up close, and smooth from a distance.

Use this for non-pixel art textures that may be viewed at a low scale (e.g. due to Camera2D zoom or sprite scaling), as mipmaps are important to smooth out pixels that are smaller than on-screen pixels.

TextureFilter FILTER_NEAREST_MIPMAP_ANISOTROPIC = 5

The texture filter reads from the nearest pixel and blends between 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true) based on the angle between the surface and the camera view. This makes the texture look pixelated from up close, and smooth from a distance. Anisotropic filtering improves texture quality on surfaces that are almost in line with the camera, but is slightly slower. The anisotropic filtering level can be changed by adjusting ProjectSettings.rendering/textures/default_filters/anisotropic_filtering_level.

Note: This texture filter is rarely useful in 2D projects. FILTER_NEAREST_MIPMAP is usually more appropriate in this case.

TextureFilter FILTER_LINEAR_MIPMAP_ANISOTROPIC = 6

The texture filter blends between the nearest 4 pixels and blends between 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true) based on the angle between the surface and the camera view. This makes the texture look smooth from up close, and smooth from a distance. Anisotropic filtering improves texture quality on surfaces that are almost in line with the camera, but is slightly slower. The anisotropic filtering level can be changed by adjusting ProjectSettings.rendering/textures/default_filters/anisotropic_filtering_level.

Note: This texture filter is rarely useful in 2D projects. FILTER_LINEAR_MIPMAP is usually more appropriate in this case.

TextureFilter FILTER_MAX = 7

Represents the size of the TextureFilter enum.

enum TextureRepeat: 🔗

TextureRepeat REPEAT_DEFAULT = 0

Sample the texture using the repeat mode determined by the node this shader is attached to.

TextureRepeat REPEAT_ENABLED = 1

Texture will repeat normally.

TextureRepeat REPEAT_DISABLED = 2

Texture will not repeat.

TextureRepeat REPEAT_MAX = 3

Represents the size of the TextureRepeat enum.

enum TextureSource: 🔗

TextureSource SOURCE_NONE = 0

The texture source is not specified in the shader.

TextureSource SOURCE_SCREEN = 1

The texture source is the screen texture which captures all opaque objects drawn this frame.

TextureSource SOURCE_DEPTH = 2

The texture source is the depth texture from the depth prepass.

TextureSource SOURCE_NORMAL_ROUGHNESS = 3

The texture source is the normal-roughness buffer from the depth prepass.

TextureSource SOURCE_MAX = 4

Represents the size of the TextureSource enum.

ColorDefault color_default = 0 🔗

void set_color_default(value: ColorDefault)

ColorDefault get_color_default()

Sets the default color if no texture is assigned to the uniform.

TextureFilter texture_filter = 0 🔗

void set_texture_filter(value: TextureFilter)

TextureFilter get_texture_filter()

Sets the texture filtering mode.

TextureRepeat texture_repeat = 0 🔗

void set_texture_repeat(value: TextureRepeat)

TextureRepeat get_texture_repeat()

Sets the texture repeating mode.

TextureSource texture_source = 0 🔗

void set_texture_source(value: TextureSource)

TextureSource get_texture_source()

Sets the texture source mode. Used for reading from the screen, depth, or normal_roughness texture.

TextureType texture_type = 0 🔗

void set_texture_type(value: TextureType)

TextureType get_texture_type()

Defines the type of data provided by the source texture.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTextureSDFNormal

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetexturesdfnormal.html

**Contents:**
- VisualShaderNodeTextureSDFNormal
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Performs an SDF (signed-distance field) normal texture lookup within the visual shader graph.

Translates to texture_sdf_normal(sdf_pos) in the shader language.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTextureSDF

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetexturesdf.html

**Contents:**
- VisualShaderNodeTextureSDF
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Performs an SDF (signed-distance field) texture lookup within the visual shader graph.

Translates to texture_sdf(sdf_pos) in the shader language.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTexture

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetexture.html

**Contents:**
- VisualShaderNodeTexture
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Performs a 2D texture lookup within the visual shader graph.

Performs a lookup operation on the provided texture, with support for multiple texture sources to choose from.

Source SOURCE_TEXTURE = 0

Use the texture given as an argument for this function.

Source SOURCE_SCREEN = 1

Use the current viewport's texture as the source.

Source SOURCE_2D_TEXTURE = 2

Use the texture from this shader's texture built-in (e.g. a texture of a Sprite2D).

Source SOURCE_2D_NORMAL = 3

Use the texture from this shader's normal map built-in.

Source SOURCE_DEPTH = 4

Use the depth texture captured during the depth prepass. Only available when the depth prepass is used (i.e. in spatial shaders and in the forward_plus or gl_compatibility renderers).

Source SOURCE_PORT = 5

Use the texture provided in the input port for this function.

Source SOURCE_3D_NORMAL = 6

Use the normal buffer captured during the depth prepass. Only available when the normal-roughness buffer is available (i.e. in spatial shaders and in the forward_plus renderer).

Source SOURCE_ROUGHNESS = 7

Use the roughness buffer captured during the depth prepass. Only available when the normal-roughness buffer is available (i.e. in spatial shaders and in the forward_plus renderer).

Source SOURCE_MAX = 8

Represents the size of the Source enum.

TextureType TYPE_DATA = 0

No hints are added to the uniform declaration.

TextureType TYPE_COLOR = 1

Adds source_color as hint to the uniform declaration for proper sRGB to linear conversion.

TextureType TYPE_NORMAL_MAP = 2

Adds hint_normal as hint to the uniform declaration, which internally converts the texture for proper usage as normal map.

TextureType TYPE_MAX = 3

Represents the size of the TextureType enum.

void set_source(value: Source)

Determines the source for the lookup.

void set_texture(value: Texture2D)

Texture2D get_texture()

The source texture, if needed for the selected source.

TextureType texture_type = 0 🔗

void set_texture_type(value: TextureType)

TextureType get_texture_type()

Specifies the type of the texture if source is set to SOURCE_TEXTURE.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTransformCompose

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetransformcompose.html

**Contents:**
- VisualShaderNodeTransformCompose
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Composes a Transform3D from four Vector3s within the visual shader graph.

Creates a 4×4 transform matrix using four vectors of type vec3. Each vector is one row in the matrix and the last column is a vec4(0, 0, 0, 1).

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTransformConstant

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetransformconstant.html

**Contents:**
- VisualShaderNodeTransformConstant
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeConstant < VisualShaderNode < Resource < RefCounted < Object

A Transform3D constant for use within the visual shader graph.

A constant Transform3D, which can be used as an input node.

Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)

Transform3D constant = Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0) 🔗

void set_constant(value: Transform3D)

Transform3D get_constant()

A Transform3D constant which represents the state of this node.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTransformDecompose

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetransformdecompose.html

**Contents:**
- VisualShaderNodeTransformDecompose
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Decomposes a Transform3D into four Vector3s within the visual shader graph.

Takes a 4×4 transform matrix and decomposes it into four vec3 values, one from each row of the matrix.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTransformFunc

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetransformfunc.html

**Contents:**
- VisualShaderNodeTransformFunc
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Computes a Transform3D function within the visual shader graph.

Computes an inverse or transpose function on the provided Transform3D.

Function FUNC_INVERSE = 0

Perform the inverse operation on the Transform3D matrix.

Function FUNC_TRANSPOSE = 1

Perform the transpose operation on the Transform3D matrix.

Function FUNC_MAX = 2

Represents the size of the Function enum.

Function function = 0 🔗

void set_function(value: Function)

Function get_function()

The function to be computed.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTransformOp

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetransformop.html

**Contents:**
- VisualShaderNodeTransformOp
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A Transform3D operator to be used within the visual shader graph.

Applies operator to two transform (4×4 matrices) inputs.

Multiplies transform a by the transform b.

Multiplies transform b by the transform a.

Operator OP_AxB_COMP = 2

Performs a component-wise multiplication of transform a by the transform b.

Operator OP_BxA_COMP = 3

Performs a component-wise multiplication of transform b by the transform a.

Operator OP_A_MINUS_B = 5

Subtracts the transform a from the transform b.

Operator OP_B_MINUS_A = 6

Subtracts the transform b from the transform a.

Operator OP_A_DIV_B = 7

Divides the transform a by the transform b.

Operator OP_B_DIV_A = 8

Divides the transform b by the transform a.

Represents the size of the Operator enum.

Operator operator = 0 🔗

void set_operator(value: Operator)

Operator get_operator()

The type of the operation to be performed on the transforms.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTransformParameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetransformparameter.html

**Contents:**
- VisualShaderNodeTransformParameter
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

A Transform3D parameter for use within the visual shader graph.

Translated to uniform mat4 in the shader language.

Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)

default_value_enabled

Transform3D default_value = Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0) 🔗

void set_default_value(value: Transform3D)

Transform3D get_default_value()

A default value to be assigned within the shader.

bool default_value_enabled = false 🔗

void set_default_value_enabled(value: bool)

bool is_default_value_enabled()

Enables usage of the default_value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeTransformVecMult

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodetransformvecmult.html

**Contents:**
- VisualShaderNodeTransformVecMult
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Multiplies a Transform3D and a Vector3 within the visual shader graph.

A multiplication operation on a transform (4×4 matrix) and a vector, with support for different multiplication operators.

Multiplies transform a by the vector b.

Multiplies vector b by the transform a.

Operator OP_3x3_AxB = 2

Multiplies transform a by the vector b, skipping the last row and column of the transform.

Operator OP_3x3_BxA = 3

Multiplies vector b by the transform a, skipping the last row and column of the transform.

Represents the size of the Operator enum.

Operator operator = 0 🔗

void set_operator(value: Operator)

Operator get_operator()

The multiplication type to be performed.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeUVFunc

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeuvfunc.html

**Contents:**
- VisualShaderNodeUVFunc
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Contains functions to modify texture coordinates (uv) to be used within the visual shader graph.

UV functions are similar to Vector2 functions, but the input port of this node uses the shader's UV value by default.

Function FUNC_PANNING = 0

Translates uv by using scale and offset values using the following formula: uv = uv + offset * scale. uv port is connected to UV built-in by default.

Function FUNC_SCALING = 1

Scales uv by using scale and pivot values using the following formula: uv = (uv - pivot) * scale + pivot. uv port is connected to UV built-in by default.

Function FUNC_MAX = 2

Represents the size of the Function enum.

Function function = 0 🔗

void set_function(value: Function)

Function get_function()

A function to be applied to the texture coordinates.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeUVPolarCoord

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeuvpolarcoord.html

**Contents:**
- VisualShaderNodeUVPolarCoord
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node that modifies the texture UV using polar coordinates.

UV polar coord node will transform UV values into polar coordinates, with specified scale, zoom strength and repeat parameters. It can be used to create various swirl distortions.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVaryingGetter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevaryinggetter.html

**Contents:**
- VisualShaderNodeVaryingGetter
- Description
- User-contributed notes

Inherits: VisualShaderNodeVarying < VisualShaderNode < Resource < RefCounted < Object

A visual shader node that gets a value of a varying.

Outputs a value of a varying defined in the shader. You need to first create a varying that can be used in the given function, e.g. varying getter in Fragment shader requires a varying with mode set to VisualShader.VARYING_MODE_VERTEX_TO_FRAG_LIGHT.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVaryingSetter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevaryingsetter.html

**Contents:**
- VisualShaderNodeVaryingSetter
- Description
- User-contributed notes

Inherits: VisualShaderNodeVarying < VisualShaderNode < Resource < RefCounted < Object

A visual shader node that sets a value of a varying.

Inputs a value to a varying defined in the shader. You need to first create a varying that can be used in the given function, e.g. varying setter in Fragment shader requires a varying with mode set to VisualShader.VARYING_MODE_FRAG_TO_LIGHT.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVarying

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevarying.html

**Contents:**
- VisualShaderNodeVarying
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeVaryingGetter, VisualShaderNodeVaryingSetter

A visual shader node that represents a "varying" shader value.

Varying values are shader variables that can be passed between shader functions, e.g. from Vertex shader to Fragment shader.

String varying_name = "[None]" 🔗

void set_varying_name(value: String)

String get_varying_name()

Name of the variable. Must be unique.

VaryingType varying_type = 0 🔗

void set_varying_type(value: VaryingType)

VaryingType get_varying_type()

Type of the variable. Determines where the variable can be accessed.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVec2Constant

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevec2constant.html

**Contents:**
- VisualShaderNodeVec2Constant
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeConstant < VisualShaderNode < Resource < RefCounted < Object

A Vector2 constant to be used within the visual shader graph.

A constant Vector2, which can be used as an input node.

Vector2 constant = Vector2(0, 0) 🔗

void set_constant(value: Vector2)

Vector2 get_constant()

A Vector2 constant which represents the state of this node.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVec2Parameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevec2parameter.html

**Contents:**
- VisualShaderNodeVec2Parameter
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

A Vector2 parameter to be used within the visual shader graph.

Translated to uniform vec2 in the shader language.

default_value_enabled

Vector2 default_value = Vector2(0, 0) 🔗

void set_default_value(value: Vector2)

Vector2 get_default_value()

A default value to be assigned within the shader.

bool default_value_enabled = false 🔗

void set_default_value_enabled(value: bool)

bool is_default_value_enabled()

Enables usage of the default_value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVec3Constant

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevec3constant.html

**Contents:**
- VisualShaderNodeVec3Constant
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeConstant < VisualShaderNode < Resource < RefCounted < Object

A Vector3 constant to be used within the visual shader graph.

A constant Vector3, which can be used as an input node.

Vector3 constant = Vector3(0, 0, 0) 🔗

void set_constant(value: Vector3)

Vector3 get_constant()

A Vector3 constant which represents the state of this node.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVec3Parameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevec3parameter.html

**Contents:**
- VisualShaderNodeVec3Parameter
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

A Vector3 parameter to be used within the visual shader graph.

Translated to uniform vec3 in the shader language.

default_value_enabled

Vector3 default_value = Vector3(0, 0, 0) 🔗

void set_default_value(value: Vector3)

Vector3 get_default_value()

A default value to be assigned within the shader.

bool default_value_enabled = false 🔗

void set_default_value_enabled(value: bool)

bool is_default_value_enabled()

Enables usage of the default_value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVec4Constant

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevec4constant.html

**Contents:**
- VisualShaderNodeVec4Constant
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeConstant < VisualShaderNode < Resource < RefCounted < Object

A 4D vector constant to be used within the visual shader graph.

A constant 4D vector, which can be used as an input node.

Quaternion(0, 0, 0, 1)

Quaternion constant = Quaternion(0, 0, 0, 1) 🔗

void set_constant(value: Quaternion)

Quaternion get_constant()

A 4D vector (represented as a Quaternion) constant which represents the state of this node.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVec4Parameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevec4parameter.html

**Contents:**
- VisualShaderNodeVec4Parameter
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

A 4D vector parameter to be used within the visual shader graph.

Translated to uniform vec4 in the shader language.

default_value_enabled

Vector4 default_value = Vector4(0, 0, 0, 0) 🔗

void set_default_value(value: Vector4)

Vector4 get_default_value()

A default value to be assigned within the shader.

bool default_value_enabled = false 🔗

void set_default_value_enabled(value: bool)

bool is_default_value_enabled()

Enables usage of the default_value.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVectorBase

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevectorbase.html

**Contents:**
- VisualShaderNodeVectorBase
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

Inherited By: VisualShaderNodeFaceForward, VisualShaderNodeVectorCompose, VisualShaderNodeVectorDecompose, VisualShaderNodeVectorDistance, VisualShaderNodeVectorFunc, VisualShaderNodeVectorLen, VisualShaderNodeVectorOp, VisualShaderNodeVectorRefract

A base type for the nodes that perform vector operations within the visual shader graph.

This is an abstract class. See the derived types for descriptions of the possible operations.

OpType OP_TYPE_VECTOR_2D = 0

OpType OP_TYPE_VECTOR_3D = 1

OpType OP_TYPE_VECTOR_4D = 2

OpType OP_TYPE_MAX = 3

Represents the size of the OpType enum.

void set_op_type(value: OpType)

A vector type that this operation is performed on.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVectorCompose

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevectorcompose.html

**Contents:**
- VisualShaderNodeVectorCompose
- Description
- User-contributed notes

Inherits: VisualShaderNodeVectorBase < VisualShaderNode < Resource < RefCounted < Object

Composes a Vector2, Vector3 or 4D vector (represented as a Quaternion) from scalars within the visual shader graph.

Creates a vec2, vec3 or vec4 using scalar values that can be provided from separate inputs.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVectorDecompose

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevectordecompose.html

**Contents:**
- VisualShaderNodeVectorDecompose
- Description
- User-contributed notes

Inherits: VisualShaderNodeVectorBase < VisualShaderNode < Resource < RefCounted < Object

Decomposes a Vector2, Vector3 or 4D vector (represented as a Quaternion) into scalars within the visual shader graph.

Takes a vec2, vec3 or vec4 and decomposes it into scalar values that can be used as separate outputs.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVectorDistance

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevectordistance.html

**Contents:**
- VisualShaderNodeVectorDistance
- Description
- User-contributed notes

Inherits: VisualShaderNodeVectorBase < VisualShaderNode < Resource < RefCounted < Object

Returns the distance between two points. To be used within the visual shader graph.

Calculates distance from point represented by vector p0 to vector p1.

Translated to distance(p0, p1) in the shader language.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVectorFunc

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevectorfunc.html

**Contents:**
- VisualShaderNodeVectorFunc
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeVectorBase < VisualShaderNode < Resource < RefCounted < Object

A vector function to be used within the visual shader graph.

A visual shader node able to perform different functions using vectors.

Function FUNC_NORMALIZE = 0

Normalizes the vector so that it has a length of 1 but points in the same direction.

Function FUNC_SATURATE = 1

Clamps the value between 0.0 and 1.0.

Function FUNC_NEGATE = 2

Returns the opposite value of the parameter.

Function FUNC_RECIPROCAL = 3

Function FUNC_ABS = 4

Returns the absolute value of the parameter.

Function FUNC_ACOS = 5

Returns the arc-cosine of the parameter.

Function FUNC_ACOSH = 6

Returns the inverse hyperbolic cosine of the parameter.

Function FUNC_ASIN = 7

Returns the arc-sine of the parameter.

Function FUNC_ASINH = 8

Returns the inverse hyperbolic sine of the parameter.

Function FUNC_ATAN = 9

Returns the arc-tangent of the parameter.

Function FUNC_ATANH = 10

Returns the inverse hyperbolic tangent of the parameter.

Function FUNC_CEIL = 11

Finds the nearest integer that is greater than or equal to the parameter.

Function FUNC_COS = 12

Returns the cosine of the parameter.

Function FUNC_COSH = 13

Returns the hyperbolic cosine of the parameter.

Function FUNC_DEGREES = 14

Converts a quantity in radians to degrees.

Function FUNC_EXP = 15

Function FUNC_EXP2 = 16

Function FUNC_FLOOR = 17

Finds the nearest integer less than or equal to the parameter.

Function FUNC_FRACT = 18

Computes the fractional part of the argument.

Function FUNC_INVERSE_SQRT = 19

Returns the inverse of the square root of the parameter.

Function FUNC_LOG = 20

Function FUNC_LOG2 = 21

Function FUNC_RADIANS = 22

Converts a quantity in degrees to radians.

Function FUNC_ROUND = 23

Finds the nearest integer to the parameter.

Function FUNC_ROUNDEVEN = 24

Finds the nearest even integer to the parameter.

Function FUNC_SIGN = 25

Extracts the sign of the parameter, i.e. returns -1 if the parameter is negative, 1 if it's positive and 0 otherwise.

Function FUNC_SIN = 26

Returns the sine of the parameter.

Function FUNC_SINH = 27

Returns the hyperbolic sine of the parameter.

Function FUNC_SQRT = 28

Returns the square root of the parameter.

Function FUNC_TAN = 29

Returns the tangent of the parameter.

Function FUNC_TANH = 30

Returns the hyperbolic tangent of the parameter.

Function FUNC_TRUNC = 31

Returns a value equal to the nearest integer to the parameter whose absolute value is not larger than the absolute value of the parameter.

Function FUNC_ONEMINUS = 32

Returns 1.0 - vector.

Function FUNC_MAX = 33

Represents the size of the Function enum.

Function function = 0 🔗

void set_function(value: Function)

Function get_function()

The function to be performed.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVectorLen

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevectorlen.html

**Contents:**
- VisualShaderNodeVectorLen
- Description
- User-contributed notes

Inherits: VisualShaderNodeVectorBase < VisualShaderNode < Resource < RefCounted < Object

Returns the length of a Vector3 within the visual shader graph.

Translated to length(p0) in the shader language.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVectorOp

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevectorop.html

**Contents:**
- VisualShaderNodeVectorOp
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeVectorBase < VisualShaderNode < Resource < RefCounted < Object

A vector operator to be used within the visual shader graph.

A visual shader node for use of vector operators. Operates on vector a and vector b.

Subtracts a vector from a vector.

Multiplies two vectors.

Divides vector by vector.

Returns the remainder of the two vectors.

Returns the value of the first parameter raised to the power of the second, for each component of the vectors.

Returns the greater of two values, for each component of the vectors.

Returns the lesser of two values, for each component of the vectors.

Operator OP_CROSS = 8

Calculates the cross product of two vectors.

Operator OP_ATAN2 = 9

Returns the arc-tangent of the parameters.

Operator OP_REFLECT = 10

Returns the vector that points in the direction of reflection. a is incident vector and b is the normal vector.

Operator OP_STEP = 11

Vector step operator. Returns 0.0 if a is smaller than b and 1.0 otherwise.

Operator OP_ENUM_SIZE = 12

Represents the size of the Operator enum.

Operator operator = 0 🔗

void set_operator(value: Operator)

Operator get_operator()

The operator to be used.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeVectorRefract

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodevectorrefract.html

**Contents:**
- VisualShaderNodeVectorRefract
- Description
- User-contributed notes

Inherits: VisualShaderNodeVectorBase < VisualShaderNode < Resource < RefCounted < Object

Returns the vector that points in the direction of refraction. For use within the visual shader graph.

Translated to refract(I, N, eta) in the shader language, where I is the incident vector, N is the normal vector and eta is the ratio of the indices of the refraction.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeWorldPositionFromDepth

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeworldpositionfromdepth.html

**Contents:**
- VisualShaderNodeWorldPositionFromDepth
- Description
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

A visual shader node that calculates the position of the pixel in world space using the depth texture.

The WorldPositionFromDepth node reconstructs the depth position of the pixel in world space. This can be used to obtain world space UVs for projection mapping like Caustics.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNode

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernode.html

**Contents:**
- VisualShaderNode
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: VisualShaderNodeBillboard, VisualShaderNodeClamp, VisualShaderNodeColorFunc, VisualShaderNodeColorOp, VisualShaderNodeCompare, VisualShaderNodeConstant, VisualShaderNodeCubemap, VisualShaderNodeCustom, VisualShaderNodeDerivativeFunc, VisualShaderNodeDeterminant, VisualShaderNodeDistanceFade, VisualShaderNodeDotProduct, VisualShaderNodeFloatFunc, VisualShaderNodeFloatOp, VisualShaderNodeFresnel, VisualShaderNodeIf, VisualShaderNodeInput, VisualShaderNodeIntFunc, VisualShaderNodeIntOp, VisualShaderNodeIs, VisualShaderNodeLinearSceneDepth, VisualShaderNodeMix, VisualShaderNodeMultiplyAdd, VisualShaderNodeOuterProduct, VisualShaderNodeOutput, VisualShaderNodeParameter, VisualShaderNodeParameterRef, VisualShaderNodeParticleAccelerator, VisualShaderNodeParticleConeVelocity, VisualShaderNodeParticleEmit, VisualShaderNodeParticleEmitter, VisualShaderNodeParticleMultiplyByAxisAngle, VisualShaderNodeParticleRandomness, VisualShaderNodeProximityFade, VisualShaderNodeRandomRange, VisualShaderNodeRemap, VisualShaderNodeReroute, VisualShaderNodeResizableBase, VisualShaderNodeRotationByAxis, VisualShaderNodeSample3D, VisualShaderNodeScreenNormalWorldSpace, VisualShaderNodeScreenUVToSDF, VisualShaderNodeSDFRaymarch, VisualShaderNodeSDFToScreenUV, VisualShaderNodeSmoothStep, VisualShaderNodeStep, VisualShaderNodeSwitch, VisualShaderNodeTexture, VisualShaderNodeTextureSDF, VisualShaderNodeTextureSDFNormal, VisualShaderNodeTransformCompose, VisualShaderNodeTransformDecompose, VisualShaderNodeTransformFunc, VisualShaderNodeTransformOp, VisualShaderNodeTransformVecMult, VisualShaderNodeUIntFunc, VisualShaderNodeUIntOp, VisualShaderNodeUVFunc, VisualShaderNodeUVPolarCoord, VisualShaderNodeVarying, VisualShaderNodeVectorBase, VisualShaderNodeWorldPositionFromDepth

Base class for VisualShader nodes. Not related to scene nodes.

Visual shader graphs consist of various nodes. Each node in the graph is a separate object and they are represented as a rectangular boxes with title and a set of properties. Each node also has connection ports that allow to connect it to another nodes and control the flow of the shader.

linked_parent_graph_frame

output_port_for_preview

clear_default_input_values()

get_default_input_port(type: PortType) const

get_default_input_values() const

get_input_port_default_value(port: int) const

remove_input_port_default_value(port: int)

set_default_input_values(values: Array)

set_input_port_default_value(port: int, value: Variant, prev_value: Variant = null)

PortType PORT_TYPE_SCALAR = 0

Floating-point scalar. Translated to float type in shader code.

PortType PORT_TYPE_SCALAR_INT = 1

Integer scalar. Translated to int type in shader code.

PortType PORT_TYPE_SCALAR_UINT = 2

Unsigned integer scalar. Translated to uint type in shader code.

PortType PORT_TYPE_VECTOR_2D = 3

2D vector of floating-point values. Translated to vec2 type in shader code.

PortType PORT_TYPE_VECTOR_3D = 4

3D vector of floating-point values. Translated to vec3 type in shader code.

PortType PORT_TYPE_VECTOR_4D = 5

4D vector of floating-point values. Translated to vec4 type in shader code.

PortType PORT_TYPE_BOOLEAN = 6

Boolean type. Translated to bool type in shader code.

PortType PORT_TYPE_TRANSFORM = 7

Transform type. Translated to mat4 type in shader code.

PortType PORT_TYPE_SAMPLER = 8

Sampler type. Translated to reference of sampler uniform in shader code. Can only be used for input ports in non-uniform nodes.

PortType PORT_TYPE_MAX = 9

Represents the size of the PortType enum.

int linked_parent_graph_frame = -1 🔗

void set_frame(value: int)

Represents the index of the frame this node is linked to. If set to -1 the node is not linked to any frame.

int output_port_for_preview = -1 🔗

void set_output_port_for_preview(value: int)

int get_output_port_for_preview()

Sets the output port index which will be showed for preview. If set to -1 no port will be open for preview.

void clear_default_input_values() 🔗

Clears the default input ports value.

int get_default_input_port(type: PortType) const 🔗

Returns the input port which should be connected by default when this node is created as a result of dragging a connection from an existing node to the empty space on the graph.

Array get_default_input_values() const 🔗

Returns an Array containing default values for all of the input ports of the node in the form [index0, value0, index1, value1, ...].

Variant get_input_port_default_value(port: int) const 🔗

Returns the default value of the input port.

void remove_input_port_default_value(port: int) 🔗

Removes the default value of the input port.

void set_default_input_values(values: Array) 🔗

Sets the default input ports values using an Array of the form [index0, value0, index1, value1, ...]. For example: [0, Vector3(0, 0, 0), 1, Vector3(0, 0, 0)].

void set_input_port_default_value(port: int, value: Variant, prev_value: Variant = null) 🔗

Sets the default value for the selected input port.

Please read the User-contributed notes policy before submitting a comment.

---

## WorldEnvironment

**URL:** https://docs.godotengine.org/en/stable/classes/class_worldenvironment.html

**Contents:**
- WorldEnvironment
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Node < Object

Default environment properties for the entire scene (post-processing effects, lighting and background settings).

The WorldEnvironment node is used to configure the default Environment for the scene.

The parameters defined in the WorldEnvironment can be overridden by an Environment node set on the current Camera3D. Additionally, only one WorldEnvironment may be instantiated in a given scene at a time.

The WorldEnvironment allows the user to specify default lighting parameters (e.g. ambient lighting), various post-processing effects (e.g. SSAO, DOF, Tonemapping), and how to draw the background (e.g. solid color, skybox). Usually, these are added in order to improve the realism/color balance of the scene.

Environment and post-processing

3D Material Testers Demo

Third Person Shooter (TPS) Demo

CameraAttributes camera_attributes 🔗

void set_camera_attributes(value: CameraAttributes)

CameraAttributes get_camera_attributes()

The default CameraAttributes resource to use if none set on the Camera3D.

Compositor compositor 🔗

void set_compositor(value: Compositor)

Compositor get_compositor()

The default Compositor resource to use if none set on the Camera3D.

Environment environment 🔗

void set_environment(value: Environment)

Environment get_environment()

The Environment resource used by this WorldEnvironment, defining the default properties.

Please read the User-contributed notes policy before submitting a comment.

---
