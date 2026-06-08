# Blender - Rendering

**Pages:** 4

---

## Camera View¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/navigate/camera_view.html

**Contents:**
- Camera View¶
- Viewing the Active Camera¶
- Setting the Active Camera¶
  - Animated Camera Switching¶
- Frame Camera Bounds¶
- Zoom Camera 1:1¶
- Camera Positioning¶
  - Align Active Camera to View¶
  - Camera Navigation¶
  - Roll, Pan, Dolly, and Track¶

Demonstration of camera view.¶

The Camera view shows the current scene from the active camera’s viewpoint.

The Camera view can be used to virtually compose shots and preview how the scene will look when rendered. The rendered image will contain everything within the dashed frame.

Camera Settings for details on how camera settings are used for display and rendering.

While in camera view, you can select the camera by clicking the dashed frame (assuming the camera object isn’t hidden).

View ‣ Cameras ‣ Active Camera, View ‣ Viewpoint ‣ Camera

This switches the view to the active camera.

View ‣ Cameras ‣ Set Active Object as Camera

Active camera (left) displayed with a solid triangle above it.¶

This sets the current active object as the active camera and switches to the camera view.

The active camera is the one that will be used for rendering, and which you’ll look through when choosing camera view.

Another way of setting the active camera is through the Scene tab of the Properties.

The active camera is normally defined on the scene level, so that it’s the same across all 3D Viewports. However, it’s also possible to make a camera the active one within one Viewport only. See Local Camera.

While a scene contains only one camera by default, it’s possible to have multiple. You can then bind the cameras to specific time points in your animation to create jump cuts showing different viewpoints. See Animating Cameras.

View ‣ Cameras ‣ Frame Camera Bounds

Centers the camera view inside the 3D Viewport’s screen area and resizes the view to fit within the area’s bounds.

View ‣ Navigation ‣ Zoom Camera 1:1

Zooms the view so that the camera frame has the exact same size as the output resolution. This allows you to preview exactly how large objects will be in the rendered image/animation.

There are several different ways to position the camera in your scene. Some of them are explained below.

The active “camera” might be any kind of object, meaning these actions can also be used to position and aim a light for example.

View ‣ Align View ‣ Align Active Camera to View

Moves and rotates the camera so it perfectly matches your current viewport view.

By enabling Lock Camera to View in Sidebar ‣ View and switching to camera view or toggle the lock navigation gizmo button when in camera view, the camera will become “glued” to the view and follow it around as you navigate.

Fly/Walk Navigation for first person navigation that moves the active camera too.

To perform these camera moves, the camera must first be selected so transform operations apply to it. The following actions also assume that you are in camera view. Having done so, you can now manipulate the camera using the same tools that are used to transform any object:

Press R to enter object rotation mode. The default will be to rotate the camera along its local Z axis (the axis orthogonal to the camera view), which is the definition of a camera “roll”.

This is just a rotation along the local X axis. Press R to enter object rotation mode, then X twice. (The first press selects the global axis, the second the local axis. This works with any axis; see Axis Locking).

This corresponds to a rotation around the camera’s local Y axis. Press R, then Y twice.

To dolly the camera, press G then MMB (or Z twice).

Press G and move the mouse (you can use X or Y twice to get purely horizontal or vertical tracking).

---

## System¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/system.html

**Contents:**
- System¶
- Cycles Render Devices¶
- Display Graphics¶
- Operating System Settings¶
- Network¶
- Memory & Limits¶
- Video Sequencer¶
- Sound¶

The System section allows you to set graphics card options, memory limits & sound settings.

If your hardware does not support some of the options described on this page, then they will either not be displayed or be corrected on startup.

Preferences System section.¶

Changes the Computing Device the Cycles render engine uses to render images. Cycles can use either the CPU or certain GPUs to render images, for more information see the GPU Rendering page.

When set to None or when the only option is None: the CPU will be used as the computing device for Cycles.

If the system has a compatible NVIDIA CUDA device, it will be available as an option for rendering with Cycles.

If the system has a compatible NVIDIA OptiX device, it will be available as an option for rendering with Cycles.

If the system has a compatible AMD HIP device, it will be available as an option for rendering with Cycles.

If the system has a compatible Intel oneAPI device, it will be available as an option for rendering with Cycles.

If the system has a compatible Apple Metal device, it will be available as an option for rendering with Cycles.

Allocates resources across multiple GPUs rather than duplicating data, effectively freeing up space for larger scenes. Note that in order for this option to be available, the GPUs must be connected together with a high bandwidth communication protocol.

Currently only NVLink on NVIDIA GPUs is supported.

Enables the use of hardware ray tracing on Intel GPUs, providing better overall performance.

Only supported with oneAPI rendering devices.

Speeds up rendering by enabling AMD hardware ray tracing on RDNA2 and above.

This feature is only available when using a HIP render device.

MetalRT for ray tracing uses less memory for scenes which use curves extensively, and can give better performance in specific cases.

Disable MetalRT (uses BVH2 layout for intersection queries).

Enable MetalRT for intersection queries.

Automatically pick the fastest intersection method.

Settings that control how Blender draws its user interface and other display graphics. These options can influence performance and compatibility.

Selects the graphics API used for drawing the interface and rendering display content.

Changing the backend requires restarting Blender for the change to take effect.

Uses the OpenGL backend. This is the traditional backend, compatible with a wide range of systems.

Uses the Vulkan backend. Vulkan may offer improved performance and better support for modern GPU features, but compatibility may vary depending on the system and drivers.

Specifies which GPU device to use for display drawing operations.

This setting is useful for systems with multiple GPUs (e.g., integrated + discrete) where you want to force Blender to use a specific GPU for UI rendering.

Changing the backend requires restarting Blender for the change to take effect.

Automatically selects the most appropriate GPU based on system configuration and driver support.

Make this installation your default Blender (MS-Windows & Linux only).

On Linux, if Blender is installed from a package manager such as Snap, file association is handled by the package manager.

Make the currently in use Blender installation the default for generating thumbnails and the default for opening blend-files.

Remove file association & thumbnailer.

Register Blender for all users, requires escalated privileges.

Files are setup files under: /usr/local for all users, otherwise ~/.local is used.

A desktop file & icon is installed so the application is available in launchers.

A file association for *.blend is setup.

The thumbnailer is installed so blend-file thumbnails will be shown in file managers (For All Users only).

Allow Blender to access the internet.

Add-ons that follow this setting will only connect to the internet if enabled. However, Blender cannot prevent third-party add-ons from violating this rule.

The time (in seconds) that online operations may wait before timing out.

Use the systems default when zero.

The maximum number of simultaneous connections an online operation may make.

Do not limit the number of connections when zero.

Number of Undo steps available.

Maximum memory usage in Mb (0 is unlimited).

This enables Blender to save actions done when you are not in Edit Mode. For example, duplicating objects, changing panel settings or switching between modes.

While disabling this option does save memory, it stops the Adjust Last Operation panel from functioning, also preventing tool options from being changed in some cases. For typical usage, its best to keep this enabled.

Read more about Undo and Redo options.

The number of lines, buffered in memory of the console window. Useful for debugging purposes and command-line rendering.

Time since last access of a GL texture in seconds, after which it is freed. Set this to 0 to keep textures allocated.

Number of seconds between each run of the GL texture garbage collector.

Time since last access of a GL vertex buffer object (VBO) in seconds after which it is freed (set to 0 to keep VBO allocated).

Number of seconds between each run of the GL vertex buffer object garbage collector.

Defines the method used for compiling GPU shaders in parallel.

This option is not available on macOS and requires using OpenGL backend.

Changing this setting requires restarting Blender to take effect.

Uses multiple threads within a single process to compile shaders concurrently. This method is more memory-efficient but may be slower on some systems.

Uses multiple separate subprocesses to compile shaders in parallel. This can be faster, especially on systems with high core counts, but consumes significantly more RAM.

The number of shader compilation threads or subprocesses to use. The maximum value is limited by the number of logical CPU cores on the system.

Increasing the number can reduce shader compilation time at the cost of higher memory usage. A value of 0 lets Blender automatically choose a suitable number based on the system configuration.

This option is not available on macOS and requires using OpenGL backend.

Changing this setting requires restarting Blender to take effect.

Upper limit of the Video Sequencer and Movie Clip Editor memory cache (in megabytes). For an optimal Clip editor and Sequencer performance, high values are recommended.

When and how Proxies are created.

Build proxies for added movie and image strips in each preview size.

Set up proxies manually.

Sequencer Cache Properties

This panel contains the sound settings for live playback within Blender and are only available with a device other than None. To control these settings for exporting sound see the Encoding Panel and Audio Panel.

Sets the audio engine to use to process and output audio.

No audio playback support (audio strips can still be loaded and rendered normally).

On macOS, CoreAudio is the native audio API. This is the default setting for macOS users and should be preferred.

PulseAudio is the most commonly used sound server on modern Linux distributions. If PulseAudio is available, this should be the preferred setting on Linux.

On Windows, WASAPI is the native audio API introduced with Windows Vista. This is the default setting for Windows users and should be preferred.

High quality professional audio engine that needs a properly configured server running on your system. Supports accurate synchronization with other professional audio applications using Jack.

Available on all platforms in case the native engines do not work. The played back 3D audio might sound different than when rendered.

Uses Simple Direct Media Layer API from libsdl.org which supports all platforms. Might be of lower quality and thus should only be used as backup.

The number of audio source “locations” to output.

Output a single audio channel.

Output two audio channels; typically a left and right channel.

Output a four audio channels.

Output a five audio channels with one LFE channel.

Output a seven audio channels with one LFE channel.

Sets the number of samples used by the audio mixing buffer. Higher buffer sizes can cause latency issues, but if you hear clicks or other problems, try to increase the size.

Sets the audio sampling rate.

Sets the audio sample format.

---

## Viewport Render¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/viewport_render.html

**Contents:**
- Viewport Render¶
- Settings¶
- Rendering¶

Viewport rendering lets you create quick preview renders from the current viewpoint (rather than from the active camera, as would be the case with a regular render).

You can use Viewport Render to render both images and animations.

Below is a comparison between the Viewport render and a final render using the Cycles Renderer.

Viewport render using Solid Mode.¶

Viewport render using Material Preview Mode.¶

Viewport rendering only works for the Workbench and EEVEE render engines. It’s not supported for Cycles.

Disable overlays to get a render without “clutter” like rigs, empties and so on.

For the most part, Viewport Render uses the current viewport settings. Some settings are located in the properties of the render engine that is used to render the view.

Solid mode uses the render settings of Workbench; Material Preview mode uses the render settings of EEVEE.

Additionally, some output settings are used too:

Activating Viewport Render will render from the current active view. This means that if you are not in an active camera view, a virtual camera is used to match the current perspective. To get an image from the camera point of view, enter the active camera view with Numpad0.

As with a normal render, you can abort it with Esc.

To render a still image, use 3D Viewport ‣ View ‣ Render Viewport Preview.

To render an animation, use 3D Viewport ‣ View ‣ Render Playblast.

To render an animation, but only those frames that have a keyframe, use 3D Viewport ‣ View ‣ Render Playblast on Keyframes. This only renders those frames for which the selected objects have an animation key. The other frames are still written to the output, but will simply repeat the last-rendered frame.

For example, when a six-frame animation is rendered, and the selected objects have a key on frames 3 and 5, the following frames will be output:

The 1st frame is always rendered.

The 1st frame is repeated because there is no key on this frame.

The 3rd frame is rendered.

The 3rd frame is repeated because there is no key on this frame.

The 5th frame is rendered.

The 5th frame is repeated because there is no key on this frame.

You can limit the viewport render to a particular region with Render Regions.

---

## Visibility¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/object/properties/visibility.html

**Contents:**
- Visibility¶

Properties ‣ Object Properties ‣ Visibility

The Visibility panel controls how objects are interacted with in the viewport and in the final render. These visibility options can also be set in the Outliner.

The object is able to be selected in the 3D Viewport.

The object will be displayed in the 3D Viewport.

The object is able to be in the final render, note that it will still be visible in rendered shading view.

Cycles has additional Visibility properties and also Grease Pencil objects have additional Visibility properties.

Render objects as a holdout or matte, creating a hole in the image with zero Alpha, to fill out in compositing with real footage or another render.

---
