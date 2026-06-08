# Blender - Other

**Pages:** 28

---

## 3D Cursor¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/3d_cursor.html

**Contents:**
- 3D Cursor¶
- Placement¶
  - Direct Placement with the Mouse¶
  - Sidebar¶
  - Snapping¶

The 3D Cursor is a point in space that has both a location and a rotation. It’s used for a number of purposes. For example, it defines where newly added objects are placed, and can also be used to manually position and orient the transform gizmo (see Pivot Point and Transform Orientation). Some tools, such as Bend, also use the Cursor.

There are a few methods to position the 3D Cursor.

Object, Edit, and Pose Mode

Positioning the 3D Cursor with two orthogonal views.¶

The Cursor tool offers the most flexibility. Simply select it in the Toolbar and click a point in the scene with LMB to place the 3D Cursor there. In the tool settings, you can choose how it should be oriented: by default, it matches the view orientation, but you can also make it match the surface normal of a piece of geometry, or the transform orientation.

Alternatively, you can press Shift-RMB with any tool selected. In this case, the 3D Cursor will always be aligned to the view orientation.

For accuracy you should use two perpendicular orthogonal 3D Viewports, i.e. any combination of top Numpad7, front Numpad1 and side Numpad3. That way you can control the positioning along two axes in one view and determine the depth in the other.

By default, the depth of the geometry under the cursor is used. This can be disabled using the Cursor Surface Project toggle in the Preferences.

Sidebar region ‣ View ‣ 3D Cursor

The 3D Cursor panel of the Sidebar region.¶

The 3D Cursor can also be positioned and oriented by editing the respective values in the Sidebar.

Object, Edit, and Pose Mode

Object/Mesh/… ‣ Snap ‣ Cursor to …

One more way of positioning the 3D Cursor is through the Snap menu, which allows you to move the Cursor to the origin of the selected object for example.

---

## Aligning¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/navigate/align.html

**Contents:**
- Aligning¶

These options allow you to align and orient the view.

Aligns the view to a certain local axis of the active object, bone, or (in Edit Mode) the normal of the active face. The view also becomes orthographic.

To return to the regular (untilted) perspective view, you can first press Numpad3 to align to the global X axis, then orbit with MMB.

Moves and rotates the active camera so it matches the current viewpoint.

Moves the active camera (without changing its orientation) so that its view frames the selected objects.

Moves the 3D Cursor back to the world origin and changes the view so that you can see everything in your scene.

Centers the view on the 3D Cursor.

Centers the view on the active object and makes it the point of interest. The view will continue orbiting around the object even if you pan to a different location. In addition, it will follow the object if it moves.

Returns the view to how it was before using View Lock to Active.

---

## Clip Display¶

**URL:** https://docs.blender.org/manual/en/latest/editors/clip/display/clip_display.html

**Contents:**
- Clip Display¶
- Marker Display¶

This pop-over contains various display settings for both Tracking mode and Mask mode.

Controls the color channels used for the frame preview. The tracking algorithm works with grayscale images, and with these options, you can check which combination of enabled and disabled channels will yield the best contrast and the least noise.

Note that this only affects the preview. To select which channels to use for the actual tracking, use the Track tab in the Toolbar to set a default for newly created markers, or the Track tab in the Sidebar to configure existing markers.

Shows the whole frame as a grayscale image.

Hides the movie clip and displays a black image instead. This helps to find markers that are tracked inaccurately or not at all.

Applies the Lens settings to the video preview to undo lens distortion. Does not change the footage itself.

Applies the 2D stabilization settings to the video preview. Does not change the footage itself.

Displays a grid which is originally orthographic, but is distorted by the Lens settings. This can be used for manual calibration: the distorted grid lines should match lines in the footage that are meant to be straight.

Applies the Lens settings to annotation strokes. Like the Grid, this option also helps to perform manual calibration.

Changes the aspect ratio for displaying only. It does not affect the tracking or solving process.

Determines how markers are displayed in the editor.

Whether to show the pattern areas of tracks. Can be used to reduce clutter and check how good tracking is.

Whether to show the search areas of selected tracks. Can be used to reduce clutter and check how good tracking is.

Shows past (red) and future (blue) positions of tracks relative to the current frame, visualizing how they move. This makes it easier to spot irregularities.

Length (in frames) of the Path.

When unchecked, hides the tracks that are disabled on the current frame (except for the active track, i.e. the one that was selected last). This helps to make the view more clear and see if the tracking is accurate enough.

Displays the name and status of each selected track. The status can be “keyframed,” “tracked,” “disabled” and so on.

Shows the result of solving the markers’ 3D locations based on their 2D movement. Each 3D location is projected back to the movie clip and displayed as a small point, which is colored green if it’s close to the original 2D marker (meaning a good solve) or red if it’s far away (meaning it needs to be tweaked).

By default, marker areas are displayed as bright boxes with a black outline. This option displays them using thin dashed lines instead.

---

## Editing¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/editing.html

**Contents:**
- Editing¶
- Objects¶
  - New Objects¶
  - Copy on Duplicate¶
- 3D Cursor¶
- Annotations¶
- Weight Paint¶
- Grease Pencil¶
- Text Editor¶
- Node Editor¶

These preferences control how several tools will interact with your input.

To understand this option properly, you need to understand how Blender works with Objects. Almost everything in Blender is organized in a hierarchy of data-blocks. A data-block can be thought of as containers for certain pieces of information. For example, the Object data-block contains information about the Object’s location, rotation, and scale while the associated linked Object Data’s data-block contains information about the mesh.

A material may be linked in two different ways:

Any created material will be created as part of the Object Data’s data-block.

Any created material will be created as part of the Object’s data-block.

A material linked to Object Data (left) and Object (right).¶

Read more about Blender’s Data System.

New objects align with world coordinates.

New object align with view coordinates.

New objects align to the 3D cursor’s orientation.

If selected, Edit Mode is automatically activated when you create a new object.

The display size for empties when a new collection instance is created.

The checkboxes define what data is copied with a duplicated object and what data remains linked. Any boxes that are checked will have their data copied along with the duplication of the object. Any boxes that are not checked will instead have their data linked from the source object that was duplicated.

For example, if you have Mesh checked, then a full copy of the mesh data is created with the new object, and each mesh will behave independently of the duplicate. If you leave the mesh box unchecked then when you change the mesh of one object, the change will be mirrored in the duplicate object.

The same rules apply to each of the checkboxes in the data-block list.

When placing the cursor by clicking, the cursor is projected onto the surface under the cursor.

When the viewport is locked to the cursor, moving the cursor avoids the view jumping based on the new offset.

The default color for new Annotate layers.

The size of the eraser used with the Annotate Tool.

Read more about Annotations.

Mesh skin weighting is used to control how much a bone deforms the mesh of a character. To visualize and paint these weights, Blender uses a color ramp (from blue to green, and from yellow to red). Enabling the checkbox will enable an alternate map using a ramp starting with an empty range. Now you can create your custom map using the common color ramp options. For detailed information see the Color ramps page.

The minimum number of pixels the mouse should have moved either horizontally or vertically before the movement is recorded. Decreasing this should work better for curvy lines.

The minimum distance that mouse has to travel before movement is recorded.

Read more about Grease Pencil.

Automatically insert the corresponding character to close an expression when typing characters such as quotes, brackets, braces, or parentheses.

Automatically offset the following or previous nodes in a chain when inserting a new node. See Auto-Offset for more information.

Margin to use for offsetting nodes.

Defines a color to be used in the inner part of the brushes circle when in Sculpt Mode, and it is placed as an overlay to the brush, representing the focal point of the brush influence. The overlay color is visible only when the overlay visibility is selected (clicking at the eye to set its visibility), and the transparency of the overlay is controlled by the alpha slider located at the Tool tab ‣ Display panel in the Sidebar.

---

## Editing Images¶

**URL:** https://docs.blender.org/manual/en/latest/editors/image/editing.html

**Contents:**
- Editing Images¶
- New¶
- Open¶
- Open Cached Render¶
- Replace¶
- Reload¶
- Edit Externally¶
- Copy/Paste¶
- Save¶
- Save As¶

Create a new Generated Image.

Opens a file browser to select an image for loading into the editor. Images can also be opened by dragging and dropping them directly into the editor.

When opening an image, the following options are available:

Sets the file path to be relative to the currently opened blend-file.

Automatically looks for image sequences in the selected images (based on the file name). Disable this when you do want to get single images that are part of a sequence. See Opening an Image Sequence for more information.

Automatically looks for UDIM tiles in the directory of the selected image; if matches are found they are loaded into Blender as UDIMs. This works by detecting if the filename has a .xxxx (four digit number) before the file extension.

Image ‣ Open Cached Render

Find the render cache file for the current scene and load it into the Render Result. This way, you can restore the last render from a previous Blender session and continue working in the Compositor without having to render the scene again.

Note that Blender doesn’t create these cache files by default. You have to enable Cache Result in the scene’s Output options and then render it at least once.

Replace the current image by another.

Reload the image from the file on drive.

Image ‣ Edit Externally

Open the image in the Image Editor program specified in the File Paths Preferences.

Allows copying and pasting images between Blender and the operating system’s clipboard.

Note, only PNG files are supported for direct clipboard copying and pasting.

Platform specific behavior:

Windows: Supports pasting images by copying the image’s file path. This method allows all supported image formats.

Linux: Requires Wayland for clipboard image support.

Save the image to its current path.

While animation renders are automatically saved, still renders are not. These have to be saved manually.

Save the image to a separate file of any type. The image output settings can be configured and are the same as the Render Output Properties.

Save the file under a specified name, but keep the old one open in the Image editor.

Image ‣ Save All Images

Save all modified images. Packed images will be repacked.

Invert the colors of an image.

Invert a single color channel.

Adjusts the image dimensions by scaling its pixel resolution. This is useful for various tasks, such as:

Reducing texture resolution to optimize performance and memory usage.

Increasing image resolution for more detailed painting or editing.

Defines the new width and height of the image in pixels.

Applies the resizing operation to all UDIM tiles in the image.

Mirrors the image so the left side becomes the right side.

Mirrors the image so the top becomes the bottom.

Rotates the image clockwise 90°.

Rotates the image counter-clockwise 90°.

Rotates the image 180°.

Pack the image into the blend-file. See Packed Data.

Unpack the image to a drive.

Image ‣ Extract Palette

Extract a Color Palette from the image for use by painting tools.

---

## Editors¶

**URL:** https://docs.blender.org/manual/en/latest/editors/index.html

**Contents:**
- Editors¶
- General¶
- Animation¶
- Scripting¶
- Data¶

Blender provides a number of different editors for displaying and modifying different aspects of data. An Editor is contained inside an Area which determines its size and placement within the Blender window. Every area may contain any type of editor.

The Editor Type selector, the first button at the left side of a header, allows you to change the Editor in that area. It is also possible to open the same Editor type in different areas at the same time.

See User Interface for documentation on the general interface.

The Editor Type selector.¶

---

## Experimental¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/experimental.html

**Contents:**
- Experimental¶

These preferences are reserved for features that are currently being worked on and are not yet complete. Experimental features are only available in Daily Builds.

Blender Preferences Experimental section.¶

---

## File Paths¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/file_paths.html

**Contents:**
- File Paths¶
- Data¶
  - Render¶
- Asset Libraries¶
- Script Directories¶
- Applications¶
  - Text Editor¶
- Development¶
- Known Limitations¶
  - Permissions on Windows¶

The File section in Preferences allows you to configure auto-save preferences and set default file paths for blend-files, rendered images, and more.

Locations for various external files can be set for the following options:

Preferences File Paths section.¶

The default path // refers to the folder of the currently open blend-file (see Relative Paths for details).

Default location to browse for text object font files.

Default location to browse for image textures.

Default location to browse for sound files.

The directory for storing temporary save files. The path must reference an existing directory or it will be ignored and the systems temporary directory will be used instead. When left blank, the systems temporary directory will be used (see Temporary Directory for details).

Where rendered images/videos are saved.

The location where cached render images are stored.

Name and on-drive directory paths of asset libraries. To make Blender aware of an asset library, add it to this list. The name is for your reference only, and will appear in asset library selectors. The path should point to the location of the asset library.

Name and Location of asset libraries in the Preferences.¶

To create a new asset library, just create an empty directory and add it to the List View. Any asset from any blend-file contained in that directory (or subdirectories thereof) will appear in the Asset Browser.

Determines how data is managed when an asset is imported, unless overridden by the Asset Browser.

The asset will be linked to the current blend-file, and thus be read-only. Later changes to the asset file will be reflected in all files that link it in.

All of the asset and all its dependencies will be appended to the current file. Dragging a material into the scene three times will result in three independent copies. Dragging an object into the scene three times will also result in three independent copies.

“Dependencies” in this case means everything the asset refers to. For an object, this can be its mesh and materials, but also other objects used by modifiers, constraints, or drivers.

Since the file now has its own copy of the asset, later changes to the asset file will not be reflected in the file it’s appended to.

Specific to the Asset Browser.

The first time an asset is used, it will be appended, including its dependencies, just like described previously. However, Blender will keep track of where it originated, and the next time the asset is used, as much data as possible will be reused. Dragging a material into the scene three times will only load it once, and just assign the same material three times. Dragging an object into the scene three times will create three copies of the object, but all copies will share their mesh data, materials, etc.

Since the file now has its own copy of the asset, later changes to the asset file will not be reflected in the file it’s appended to.

Imports the asset as linked data and immediately packs it into the current blend-file. This ensures that the asset remains available even if the original library data is modified or becomes unavailable.

Useful for maintaining self-contained files that do not rely on external asset library paths.

Use relative path when linking assets from this asset library.

Additional locations to search for Python scripts.

Each path can be given a Name to signify to purpose of that script directory.

By default, Blender looks in several directories (platform dependent) for scripts. By adding a user script path in the preferences an additional directory is used. This can be used to store your own scripts and add-ons independently of the current Blender version.

You will need to create specific subfolders in this path which match the structure of the scripts folder found in Blender’s installation directory.

The following subdirectories will be used when present:

Modules in this folder will be imported on startup.

Legacy add-ons located here will be listed in the add-ons preferences.

Modules in this folder can be imported by other scripts.

Presets in this folder will be added to existing presets.

For add-ons it is now recommended to use a local extension repository if you wish to define additional locations to install and manage them.

To make use of these you will need to define them as extensions.

You have to restart Blender for all changes to the users scripts to take effect.

The path to an external program to use for image editing.

The program used for playing back rendered animations via View Animation.

By default this is set to Internal which uses Blender’s built-in animation player.

This has the advantage that all image formats supported by Blender can be played back and no 3rd party application needs to be installed.

Command to launch the text editor when using Edit Externally, either a full path or a command in $PATH. Use the internal editor when left blank.

Defines the specific format of the arguments with which the text editor opens files.

The supported expansions are as follows:

$filepath: The absolute path of the file.

$line: The line to open at (Optional).

$column: The column to open from the beginning of the line (Optional).

$line0 & $column0 similar to the above but they start at zero.

Example: -f $filepath -l $line -c $column

Only visible when Developer Extras are enabled.

The path to the /branches directory of your local SVN translation copy, to allow translating from the UI.

Be sure that you have the right privileges for running the executable accessing the path defined. On Windows for instance, if the option “Run this program as an administrator” is enabled for the executable, it will lead to a failure to open the editor due to a limitation within the OS User Account Control. Running a program with elevated privileges is potentially dangerous!

---

## Image Overlays¶

**URL:** https://docs.blender.org/manual/en/latest/editors/image/overlays.html

**Contents:**
- Image Overlays¶
- Geometry¶
- Image¶
- Guides¶

The Overlays pop-over configures the overlays that are displayed on top of images. In the header, there is a button to turn off all overlays for the Image Editor. This option also toggles the visibility of UDIM tile information.

The options that are visible in the pop-over depend on the Image Editor mode. The following overlay categories are available:

Display selected and active object’s UVs.

Opacity of faces. Useful to differentiate between UV islands. Can also be reduced when texture painting to prevent faces from tinting the texture’s colors.

Displays metadata about the selected Render Result. See the Output tab’s Metadata panel to change what metadata to include.

The following properties are only available when displaying the Viewer Node image in the Image Editor set to View or Mask mode.

Displays overlay text showing information about the active Viewer node:

Render Size: The resolution of the final render output. This is defined in the Output Properties.

Image Size: The resolution of the image currently displayed in the Viewer node.

Displays a border showing the final render region defined in the scene. Space outside the render region appear shaded for reference.

Controls the opacity of the shaded area outside the render region. Higher values darken the outside area more, making the render region stand out.

---

## Image Settings¶

**URL:** https://docs.blender.org/manual/en/latest/editors/image/image_settings.html

**Contents:**
- Image Settings¶
- Source¶
  - Single Image¶
  - Image Sequence¶
  - Movie¶
  - Generated¶
- Common Options¶

Select the type of image to use. For images that come from files, see Supported Graphics Formats.

A single, static image.

An animation where each frame is stored in a separate file. See Opening an Image Sequence. For options, see Movie below.

A video file. Note that if you want to do motion tracking and video compositing rather than simply using the video as a texture, you should load it into the Movie Clip Editor instead.

The options below are for preview purposes only; they don’t affect the 3D Viewport or the render. For that, see the Image Texture Node.

Blender plays all videos at the scene frame rate, not their original frame rate, meaning they’ll be faster or slower than intended if these frame rates don’t match up. To work around this, see the Offset field of the Image Texture Node linked above.

How many frames of the video to play. Past this point, the video will be paused (unless Cyclic is enabled).

Sets the Frames to the number of frames in the video file.

Scene frame at which the video should start playing.

Number of frames to offset the video to an earlier point in time. (Put differently: how many frames at the start of the video to skip.)

Start over after the last frame to create a continuous loop.

Play the video in the Image Editor when the scene animation is playing. (The mouse cursor should be in the Image Editor or the Timeline when starting playback for this to work.)

Apply deinterlacing to interlaced (analog) video.

Image generated by Blender.

The width and height of the image in pixels.

Creates a 32-bit image. This has a larger file size, but holds much more color information than the standard 8-bit image. For close-ups and large gradients, it may be better to use a 32-bit image.

Creates a blank image of a single specified color.

Creates a checkerboard pattern with a colored cross (+) in each square.

Creates a more complex colored grid with letters and numbers denoting locations. It could be used to check for stretching or distortion in the UV mapping.

The fill color when creating a Blank image.

Used for replacing or packing files.

Embed the resource into the current blend-file. See Packed Data.

Path to the linked file.

Opens the File Browser to select a file from a drive.

Reloads the file. Useful when it has been reworked in an external application.

Specifies the Color Space that the image file was saved in. This information is used to correctly convert the image to Blender’s internal linear color space, which is used for all color computations and rendering.

Textures and final renders are often stored in sRGB, while OpenEXR images are stored in a linear color space. Some images such as normal, bump or stencil maps do not strictly contain “colors” and should never have a color conversion applied to them. For such images, the color space should be set to Non-Color.

The list of color spaces depends on the active OCIO config. The default supported color spaces are described in detail here: Default OpenColorIO Configuration.

How the image uses its Alpha Channel. This option is only available if the image format supports transparency.

Store RGB and alpha channels separately with alpha acting as a mask, also known as unassociated alpha. Commonly used by image editing applications and file formats like PNG. This preserves colors in parts of the image with zero alpha.

Store RGB channels with alpha multiplied in, also known as associated alpha. The natural format for renders and used by file formats like OpenEXR. This can represent purely emissive effects like fire correctly, unlike straight alpha.

Different images are packed in the RGB and alpha channels, and they should not affect each other. Channel packing is commonly used by game engines to save memory.

Ignore alpha channel from the file and make image fully opaque.

Load the image with a bit depth of only 16 bits per channel instead of 32, which saves memory.

Apply the color management settings when displaying this image on the screen.

The thickness of the margin around UV islands for texture painting to bleed into. This margin ensures that no unpainted pixels remain at the island border.

Painting a stroke across a seam in 3D space makes it extend past the UV island borders in the texture, until it gets cut off at the margin.¶

A higher value will result in a thicker margin, which can be useful if you intend to create mipmaps of the texture. However, this may also reduce painting performance.

This setting only affects Sculpt Mode, where texture painting support is currently experimental. In Texture Paint Mode, a fixed margin is used instead.

---

## Lights¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/lights.html

**Contents:**
- Lights¶
- Studio Lights¶
  - Editor¶
- MatCaps¶
- HDRIs¶

Blender Preferences Lights section.¶

Studio Lights are used to illuminate the 3D Viewport during Solid View and will not be rendered. Unlike lights in the scene, the lighting direction follows the viewport orientation.

There are up to four virtual light sources.

The Light toggles allow you to enable or disable individual lights. At least one of the four lights must remain enabled for the 3D Viewport. The lights are equal, except for their direction and color. You can control the direction of the lights, as well as their diffuse and specular colors.

Toggles the specific light.

This is the constant color of the light.

This is the highlight color of the light.

Smooth the shading from this light.

This has the effect of lighting to be less direct.

The direction of the light, (see Direction Buttons).

The direction of the light will be the same as shown at the sphere surface.

The color of unlit areas.

This panel manages MatCap image files which can used to light the view when MatCap shading is enabled.

Two kinds of images are supported for MatCaps. Regular image files and multilayered OpenEXR files. When using multilayered OpenEXR files, the layer named “diffuse” will be used as a diffuse pass, the layer named “specular” will be used as a specular pass. Regular images will be handled as “diffuse” and will not support specular highlighting.

The diffuse pass is multiplied with the base color of the objects and the specular pass is added on top. MatCaps, that only have a diffuse pass tend to look very metallic, with a separate specular pass it is possible to simulate a wider variety of materials.

This panel manages HDRI image files which can be used to light the view when Material Preview or Rendered shading is enabled.

---

## Mask Display¶

**URL:** https://docs.blender.org/manual/en/latest/editors/clip/display/mask_display.html

**Contents:**
- Mask Display¶

This popover controls how masks are displayed in Mask mode.

Toggles the display of the mask splines. Note that if they’re hidden, you won’t be able to edit them.

Line style of the splines.

Visualizes masks by shading the whole clip.

Displays just the masks as a grayscale image. Excluded areas are black, while included areas are white.

Displays the clip with excluded areas darkened.

How much excluded areas are darkened when using the “Combined” Overlay Mode.

---

## Measure¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/toolbar/measure.html

**Contents:**
- Measure¶
- Usage¶

The Measure tool is an interactive tool where you can drag lines in the scene to measure distances or angles. Snapping to geometry could be activated for better accuracy or to measure wall thickness. The Measure tool can be accessed from the Toolbar.

Examples of the Measure tool.¶

Here are some common steps for using the Measure tool:

Activate the Measure tool from the Toolbar.

Click and drag in the viewport to define the initial start and end point for the ruler. You can add multiple rulers in the viewport.

Drag either end of the ruler to move it.

Holding Ctrl while moving enables snapping to edges and vertices.

Holding Shift while moving lets you measure the distance between faces. This only works well with parallel faces, e.g. walls.

You can always navigate (pan, zoom, …) or change the view (orthogonal, perspective) in the viewport to have better access to the ruler.

Click on the midpoint of a created ruler to convert it to a protractor. The midpoint can then be dragged just like the endpoints.

A selected ruler can be deleted with Delete or X. To delete all measurements, delete the “RulerData3D” layer in the Sidebar ‣ View ‣ Annotations panel (see image above).

All measurements are hidden when another tool is selected. They are shown when the Measure tool is selected again. However, you can do editing operations while the ruler is active. For example, you can edit the rotation or scale of the selected object in the Sidebar.

Measurements do not appear in the Render output.

Unit settings and scale from the scene are used for displaying dimensions. Changing the unit system (metric, imperial), or the units of length (cm, m, …) or angle (degrees, radians) will update the measurements.

In Edit Mode only, there is also a Measurement group in the Viewport Overlays popover. Using the settings in this group, you can have the viewport automatically display measurements for selected edges and faces, without the need to manually create a ruler.

---

## Navigating¶

**URL:** https://docs.blender.org/manual/en/latest/editors/image/navigating.html

**Contents:**
- Navigating¶
- Gizmos¶
- View Menu¶

Panning can be done by dragging with MMB.

Zooming can be done using Wheel or NumpadPlus/NumpadMinus.

Next to the Sidebar region at the top, there are gizmos that allow panning and zooming more comfortably when e.g. no mouse wheel is available.

Show or hide the Toolbar.

Show or hide the Sidebar.

Show or hide the settings for the currently selected tool.

Toggle the visibility of the Asset Shelf.

Displays a pop-up panel to alter properties of the last completed operation. See Adjust Last Operation.

Instantly update any other editors that are affected by changes in this Image Editor. When disabled, the other editors may display outdated information until they’re manually refreshed (e.g. by orbiting for the 3D Viewport).

Displays metadata about the selected Render Result. See the Output tab’s Metadata panel to change what metadata to include.

Menu with convenient zoom levels and operations. The zoom levels are calculated based on the images resolution compared to the screen resolution.

12.5% (1:8) Numpad8 zoom out to a factor of 12.5%.

25% (1:4) Numpad4 zoom out to a factor of 25%.

50% (1:2) Numpad2 zoom out to a factor of 50%.

100% (1:1) Numpad1 resets the zoom to 100%.

200% (2:1) Ctrl-Numpad2 zoom in to a factor of 200%.

400% (4:1) Ctrl-Numpad4 zoom in to a factor of 400%.

800% (8:1) Ctrl-Numpad8 zoom in to a factor of 800%.

Zooms the view in or out.

Like Frame All, but uses as much space in the editor as possible.

Zoom in the view to the nearest item contained in the border.

Pans and zooms the view so that the image is centered and fully visible.

Pan the view so that the 2D cursor is at the center of the editor.

Only available when viewing the Render Result. See Render Region.

Only available when viewing the Render Result. See Render Region.

Switch to the next/previous render slot (that contains a render).

Adjust the area the Image Editor is in.

---

## Navigating¶

**URL:** https://docs.blender.org/manual/en/latest/editors/uv/navigating.html

**Contents:**
- Navigating¶
- 2D Viewport¶
- Gizmos¶
- View Menu¶
- 2D Cursor¶

Panning can be done by dragging with MMB.

Zooming can be done using Wheel or NumpadPlus/NumpadMinus.

Next to the Sidebar region at the top, there are gizmos that allow panning and zooming more comfortably when e.g. no mouse wheel is available.

Also see Navigating in the Image Editor.

Change the view so that all selected UV vertices are visible.

Just like the 3D Viewport, the UV Editor has a Cursor that you can jump to (View ‣ Center View to Cursor). It can also serve as a pivot point and a snapping target.

To change the Cursor’s position, either press LMB with the Cursor tool selected, or Shift-RMB with any tool selected. You can also change the “Location X/Y” fields in the View tab of the Sidebar, in either relative coordinates (0 to 1) or pixel coordinates. In both cases, the lower left corner of the image serves as the origin (0, 0).

You can press Shift-C to move the Cursor to the center.

---

## Save & Load¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/save_load.html

**Contents:**
- Save & Load¶
- Blend Files¶
  - Auto Run Python Scripts¶
- File Browser¶

Preferences Save/Load section.¶

Asks for confirmation before closing or opening a new blend-file if the current file has unsaved changes.

Number of versions created (for backup) when saving newer versions of a file.

This option keeps saved versions of your file in the same directory, using extensions: .blend1, .blend2, etc., with the number increasing to the number of versions you specify.

Older files will be named with a higher number. E.g. with the default setting of 2, you will have three versions of your file:

*.blend – last saved.

*.blend1 – second last saved.

*.blend2 – third last saved.

Number of files displayed in File ‣ Open Recent.

Enables Blender’s Auto Save feature, which periodically saves a temporary backup of the current file to the Temporary Directory.

This is useful for recovering work after a crash or unexpected shutdown.

Specifies the interval, in minutes, between automatic saves. Shorter intervals provide better protection but may increase disk writes slightly, which could cause performance issues for larger files.

Select how blend-file preview are generated. These previews are used both in the File Browser and for previews shown in the operating system’s file browser.

Do not generate any blend-file previews.

If there is no camera in the 3D Viewport a preview using a screenshot of the active Workspace is generated. If a camera is in the scene, a preview of the viewport from the camera view is used.

Generate a preview by taking a screenshot of the active Workspace.

Generate a preview of a Workbench render from the camera’s point of view.

Default value for Relative Paths when loading external files such as images, sounds, and linked libraries. It will be ignored if a path is already set.

Default value for Compress file when saving blend-files.

Default value for Load UI when loading blend-files.

Entering Tab in the Text Editor adds the appropriate number of spaces instead of using characters.

Python scripts (including driver expressions) are not executed by default for security reasons. You may be working on projects where you only load files from trusted sources, making it more convenient to allow scripts to be executed automatically.

Blend-files in these folders will not automatically run Python scripts. This can be used to define where blend-files from untrusted sources are kept.

Hide the Recent panel of the File Browser which displays recently accessed folders.

Hide System Bookmarks in the File Browser.

By activating this, the file region in the File Browser will only show appropriate files (i.e. blend-files when loading a complete Blender setting). The selection of file types may be changed in the file region.

Unhide files and data-blocks with names that start with . in File Browsers and data IDs.

Data-blocks with names beginning with a . can be selected by typing in a search string that also starts with the . character, even if this setting is disabled.

---

## Selecting UVs¶

**URL:** https://docs.blender.org/manual/en/latest/editors/uv/selecting.html

**Contents:**
- Selecting UVs¶
- Sync Selection¶
- Selection Mode¶
- UV Island Selection¶
- Sticky Selection Mode¶
- Select Menu¶
- Shortest Path¶
- Select Edge Loop¶
- Select Edge Ring¶

Much like the 3D Viewport, the UV Editor has selection mode buttons in the header, as well as a Select menu.

When enabled (the default), the UV Editor and 3D Viewport share a synchronized selection state. Selecting components (vertices, edges, or faces) in one editor will automatically select the corresponding elements in the other.

With Sync Selection enabled, all faces are visible in the UV Editor at all times. Selecting a vertex, edge, or face in the 3D Viewport selects its corresponding UV elements. However, when a single 3D vertex or edge corresponds to multiple UV vertices or edges (for example, along a UV seam), you cannot select them individually—selecting one selects all of them.

When disabled, only the UVs belonging to the currently selected faces in the 3D Viewport are shown. Selections in the UV Editor are independent, allowing individual UV vertices and edges to be selected even if they correspond to the same mesh vertex or edge. Selecting in one editor no longer affects the other.

Currently, only some 3D Viewport selection operations preserve per-UV selection data, including basic picking, box, circle, and lasso selection. Other operators, such as Select Random or Select Similar, will reset the stored UV selection, causing all UVs connected to selected mesh elements to become selected. Support for additional operators may be added later.

Internally, UV selection data is stored per face corner and created on demand to avoid overhead. Python scripts that modify mesh selections can use the API functions to synchronize or clear the UV selection state as needed.

If Sync Selection is enabled, you can hold Shift while clicking a selection mode to activate multiple ones at the same time, or Ctrl to expand/contract the selection.

Header ‣ UV Island Selection

Select contiguous groups of faces that are connected in the UV map.

Options for automatically selecting additional UV vertices. Only available for Face select mode or if Sync Selection is disabled.

Each UV vertex can be selected independently of the others.

Automatically select UV vertices that correspond to the same mesh vertex and have the same UV coordinates. This is the default and gives the illusion that multiple faces in a UV map can share the same vertex; in reality, they have separate vertices that overlap.

Automatically select UV vertices that correspond to the same mesh vertex, even if they have different UV coordinates. This is also the behavior when Sync Selection is enabled.

Selects all UV elements.

Deselects all UV elements.

Inverts the current selection.

Like Box Select, but only selects pinned UV vertices.

Expands/contracts the selection to/from the adjacent elements.

Selects UV elements that are similar to the active one in some way. The Adjust Last Operation panel provides several options:

The property to compare. Which properties are available depends on the Selection Mode.

Selects vertices with the same pinned state.

Selects edges with a similar length in the UV map.

Selects edges with a similar length in the 3D mesh.

Selects edges with the same pinned state.

Selects faces with a similar area in the UV map.

Selects faces with a similar area in the 3D mesh.

Selects faces that have the same Material.

Selects faces that belong to the same object. This is useful when multiple objects are in Edit mode at once.

Selects faces with a similar number of edges.

Select faces that have the same orientation (facing upwards or downwards in the UV map).

Selects islands with a similar area in the UV map.

Selects islands with a similar area in the 3D mesh.

Selects islands with a similar number of faces.

The comparison operator.

Select elements whose value is equal.

Select elements whose value is greater or equal.

Select elements whose value is less or equal.

Tolerance for values that are almost, but not quite the same. A higher threshold will select more elements.

Selects all elements that are connected to the currently selected ones.

Selects the path between two selected elements. (See below)

Selects all pinned UVs.

“Detaches” the selected faces so they can be moved elsewhere without affecting their neighbors.

Unlike Split Selection for meshes, which physically disconnects faces, this is a pure selection operator. In UV space, the faces were never connected to begin with; it only seemed that way because Sticky Selection automatically selected the vertices of the neighboring faces. Select Split deselects those vertices again.

As an alternative to Select Split, you can set the Sticky Selection Mode to Disabled.

Selects all UV faces that overlap each other.

Select ‣ Select Linked ‣ Shortest Path

Selects all the UV elements along the shortest path between two elements: the two selected elements when activated using the menu, or the active one and the clicked one when activated using the shortcut.

For vertices: allows the path to step across faces, following their diagonal rather than their edges.

For edges: selects disconnected edges that are perpendicular to the path (edge ring), rather than connected edges along the path (edge loop).

For faces: allows the path to go through faces that only share a vertex, rather than an edge.

Calculates the distance by simply counting edges rather than measuring their lengths.

Selects all shortest paths (rather than just one).

Allows to only select elements at regular intervals, creating a “dashed line” rather than a continuous one.

The number of deselected elements in the repetitive sequence.

The number of selected elements in the repetitive sequence.

The number of elements to offset the sequence by.

Mesh edit Select Shortest Path.

Alt-LMB, or Shift-Alt-LMB for extending the existing selection.

Holding Alt while clicking an edge selects that edge and then expands the selection as far as possible in the two directions parallel to it. (While this of course works for selecting edge “loops” that go all the way around a mesh, it also works if there’s no loop.)

You can additionally hold Shift to extend the current selection rather than replacing it.

Mesh edit Select Edge Loops.

Ctrl-Alt-LMB, or Shift-Ctrl-Alt-LMB for extending the existing selection.

Holding Ctrl-Alt while clicking an edge selects that edge and then expands the selection as far as possible in the two directions perpendicular to it. (While this of course works for selecting edge “rings” that go all the way around a mesh, it also works if there’s no ring.)

You can additionally hold Shift to extend the current selection rather than replacing it.

Mesh edit Select Edge Rings.

---

## Sidebar¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/sidebar.html

**Contents:**
- Sidebar¶
- Item¶
- Tool¶
- View¶
  - View Panel¶
    - View Lock¶
  - 3D Cursor¶
  - Collections¶
  - Annotations¶
- Animation¶

Shows Transform settings of the active object.

Shows settings of the active tool and Workspace.

The View panel lets you change other settings regarding the 3D Viewport.

Control the focal length of the 3D Viewport camera.

Adjust the minimum and maximum distances for geometry to be visible. Geometry closer than Start or further away than End will not be shown.

In Orthographic view, the viewport uses negative End instead of Start.

A large clipping range will allow you to see both near and far objects, but reduces the depth precision resulting in artifacts.

In some cases, a very large range may cause operations that depend on the depth buffer to become unreliable, although this depends on the graphics card and drivers.

See Troubleshooting Depth Buffer Glitches for more information.

Allow this 3D Viewport to have its own active camera, separate from the global active camera that’s defined in the scene. The selector next to the checkbox lets you choose this camera.

Show camera passepartout when in camera view.

Use the Render Region. Defining the region with Ctrl-B will automatically enable this option.

Note that if you’re viewing the scene through the active camera, this option has no effect – in this case, you instead need to use the checkbox Output Properties ‣ Format ‣ Render Region in the Properties editor. This will affect not just the viewport, but also the final render.

Lets you select an object to become the point of interest of the viewpoint. The view will then orbit around, and zoom towards, that object. This option is not available when viewing the scene through the active camera.

Makes the 3D Cursor the point of interest of the viewpoint. This option is only available when Lock to Object is not active.

When looking through a camera, the camera becomes “glued” to the view and will follow it around as you navigate. The camera frame will be outlined with a red dashed line.

Prevent changes to the orientation and perspective of the 3D Viewport.

If the camera is parented to an object, you can choose to enable Camera Parent Lock in the camera’s properties. This will cause viewport navigation to transform the camera’s root parent rather than the camera itself.

The location of the 3D Cursor.

The rotation of the 3D Cursor.

Method for calculating rotations, additional information can be found in the manual’s appendix.

Coordinate axes are aligned to the Euler axis, allowing you to see the discreet XYZ axis underlying the Euler rotation, as well as possible Gimbal Lock.

The X, Y, and Z coordinates define a point relative to the object origin. This point and the origin define an axis around the W value defines the rotation.

X, Y, Z and W correspond to the Quaternion components.

The Collections panel shows a list of collections and can be used to control their visibility. If a collection contains objects, there is a circle to the left of its name.

Allows setting collection visibility per viewport rather than globally.

Shows or hides the collection.

You can also “isolate” a collection by clicking its name. This will show the collection as well as its ancestors and descendants, and hide all other collections.

See Annotations for more information.

---

## Sidebar¶

**URL:** https://docs.blender.org/manual/en/latest/editors/image/sidebar.html

**Contents:**
- Sidebar¶
- Tool¶
- Image¶
  - Image¶
  - Metadata¶
- View¶
  - Display¶
  - Annotations¶
- Scopes¶
  - Histogram¶

Displays the settings of the active tool.

Tools for working with images. See Image Settings.

Lists image metadata.

You can set the editor’s display options in this panel.

Display aspect for this image. Does not affect rendering.

Tile the image so it completely fills the editor.

Options for the annotation tool. See Annotations.

Scopes in the Image Editor.¶

Displays different kinds of statistical information about the colors in the image.

Note that the Scopes tab is not shown if the active object is in Edit Mode or Texture Paint Mode.

Displays a graph of the color distribution in the image. For each color value (such as Luminance) on the X axis, it shows the number of pixels with that value on the Y axis. A predominantly dark image would have the highest values toward the left side of the graph.

Use this mode to balance out the tonal range in an image. A well-balanced image should have a nice smooth distribution of color values.

You can drag LMB in the histogram to adjust its vertical zoom.

Shows a luminosity histogram.

Shows the RGB channels stacked on top of each other.

Shows a single color channel.

Displays lines rather than filled shapes.

Plots the color distribution for each vertical line of pixels in the image. The X axis of the Waveform corresponds to the X axis of the image, while the Y axis represents the range of a color component such as Luminance. The brighter a specific point is, the more pixels in that vertical line have that color value.

Opacity of the points.

Show a single Waveform plotting the luminosity distribution.

Show the Y, Cb and Cr Waveforms side by side.

Show the R, G and B Waveforms side by side.

Show the R, G and B Waveforms overlaid on top of each other.

Shows the color distribution in a radial fashion. The angle represents the hue, while the distance from the center represents the saturation.

Opacity of the points.

The Sample Line scope is the same as the Histogram but allows you to get the sample data from a line.

Used to draw a line to read the sample data from.

Proportion of image pixels to sample if Full Sample is disabled.

---

## Sidebar¶

**URL:** https://docs.blender.org/manual/en/latest/editors/uv/sidebar.html

**Contents:**
- Sidebar¶
- Image Tab¶
  - UV Vertex¶
  - Image¶
  - UDIM Tiles¶
- Tool Tab¶
- View Tab¶
  - Display¶
  - 2D Cursor¶
  - Annotations¶

The averaged-out position of the selected UV vertices.

Shows the settings for the active tool.

You can set the editor’s display options in this panel.

Display aspect for this image. Does not affect rendering.

Tile the image so it completely fills the editor.

Use pixel coordinates rather than relative coordinates (0 to 1) for the UV Vertex and 2D Cursor Location fields.

View and change the location of the 2D Cursor.

Options for the Annotate tool.

See Scopes in the Image Editor.

---

## Sidebar Region¶

**URL:** https://docs.blender.org/manual/en/latest/editors/clip/sidebar.html

**Contents:**
- Sidebar Region¶
- Footage¶
  - Proxy/Timecode¶
  - Footage Settings¶
  - Animation¶
- Track¶
- Stabilization¶
- View¶
  - 2D Cursor¶
  - Annotations¶

High-resolution video files can impact Blender’s performance, slowing down scrubbing and other operations. To counter this, you can generate one or more proxies, which are copies of the original footage stored at a lower resolution and/or quality. These proxies can then be used as a less resource-heavy stand-in while working on the scene.

The proxy resolution(s) to generate based on the original, distorted footage.

The proxy resolution(s) to generate based on the undistorted footage (that is, with the Lens settings applied to undo the distortion in the recording).

Controls the level of lossy compression applied to the image, expressed as a percentage. Lossy compression reduces file size by discarding some image data, which may result in a loss of detail.

0%: Maximum compression, producing the smallest file size but the most noticeable quality loss.

100%: No compression, preserving full image quality at the cost of a larger file size.

By default, proxies are stored to a BL_proxy subfolder next to the original file. Use this option to specify a different location.

Generates proxies based on the settings above, as well as timecode files. Instead of using this button, you can also click Clip ‣ Proxy ‣ Rebuild Proxy and Timecode Indices.

When you are working with footage directly copied from a camera without preprocessing it, there might be numerous artifacts, mostly due to seeking to a given frame in the sequence. This happens because such footage usually does not have correct frame rate values in the file header. This issue can still arise when the source clip has the same frame rate as the scene settings. In order for Blender to correctly calculate the frames and frame rate there are two possible solutions:

Preprocess your video with e.g. MEncoder to repair the file header and insert the correct keyframes.

Use the Timecode Index option in Blender.

Ignore generated timecodes, seek in movie stream based on calculated timestamp.

Seek based on timestamps read from movie stream, giving the best match between scene and movie times.

Effectively convert movie to an image sequence, ignoring incomplete or dropped frames, and changes in frame rate.

Record Run is the Timecode Index which usually is best to use, but if the source file is totally damaged, Record Run No Gaps will be the only chance of getting an acceptable result.

Which proxy size to use for display. Depending on the Render Undistorted setting, Blender will use either the Original proxy or the Undistorted proxy.

Controls animation data for movie clip properties, including active Actions and their assigned Slot.

See Manually Assigning Actions and Slots for more information.

See 2D Stabilization.

The 2D Cursor is the dashed crosshair in the main region. It can be used as a transformation pivot point by selecting the corresponding option in the editor’s header.

Note that the 2D Cursor is only available in Mask mode, not in Tracking mode.

The relative location of the 2D Cursor, going from (0, 0) for the bottom left corner to (1, 1) for the top right corner.

You can also position the 2D Cursor by clicking Shift-RMB in (or around) the video.

---

## UV Overlays¶

**URL:** https://docs.blender.org/manual/en/latest/editors/uv/overlays.html

**Contents:**
- UV Overlays¶
- Guides¶
- UV Editing¶
- Geometry¶
- Image¶

The Overlays pop-over.¶

In the header, there is a button to turn off all overlays for the UV Editor. This option also toggles the visibility of UDIM tile information.

The drop-down button opens a pop-over with more detailed settings. The following categories are available:

Show the grid on top of the image rather than behind it.

How the row and column counts are determined.

The grid starts at 8×8 cells that are automatically subdivided further as you zoom in.

The row and column counts are fixed and can be configured manually.

Each grid cell matches one image pixel.

Number of columns/rows in the grid.

The number of UDIM tile grids to display in each cardinal direction.

Show how much of a shape difference there is between UV space and 3D space. Blue means low distortion, red means high. You can choose whether to display the distortion based on Angle or Area.

Show the active UV map as an overlay in the UV Editor.

Adjust the opacity of face fill colors in UV overlays.

Opacity of edges and faces.

Control how edges are shown.

Display edges in gray with a black outline.

Display edges as dashed black-gray lines.

Display edges in black.

Display edges in white.

Additionally show the edges as they look after applying modifiers (in gray).

Display faces over the image.

Display metadata about the selected Render Result. See the Output tab’s Metadata panel to change what metadata to include.

---

## Viewpoint¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/navigate/viewpoint.html

**Contents:**
- Viewpoint¶

The menu View ‣ Viewpoint lets you align the viewing direction to a specific axis. This can also be done using the Navigation Gizmo or the following hotkeys:

The above hotkeys align the view to a global (world) axis. You can also align to a local axis of the selected item by additionally holding Shift. This way, you can for example view any mesh face head-on, no matter how it’s oriented. (To get out of this local viewpoint, simply align to a global axis again.)

The view can also be aligned by holding Alt-MMB and dragging the mouse in a certain direction.

---

## Viewport¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/viewport.html

**Contents:**
- Viewport¶
- Display¶
- Quality¶
- Textures¶
- Subdivision¶

Blender Preferences Viewport section.¶

Display the active Object name and frame number at the top left of the 3D Viewport.

Display the name and type of the current view in the top left corner of the 3D Viewport. For example: “User Perspective” or “Top Orthographic”.

Show the frames per second screen refresh rate while an animation is played back. It appears in the top left of the 3D Viewport, displaying red if the frame rate set cannot be reached.

Calculate the FPS displayed in the viewport based on an average of the current and previously displayed frames. A value of zero uses the number of frames in 1.0 second.

More samples represent the average FPS over a longer period of time, however sudden changes to performance result in a more gradual increase/decrease over time.

Fewer samples shows an FPS which more closely matches the actual performance, however the value may jitter - making the FPS difficult to comprehend.

Diameter of the gizmo.

Diameter of the HDRI sphere overlay.

Display the axis as an interactive gizmo. Click sets the viewport to display along this axis and dragging orbits the view.

Display simple, less intrusive axis in the viewport.

How vivid the colors of the simple axis are.

Disables the viewport axis.

Diameter of the 3D Viewport Axis widget.

Enable a fresnel effect on edit mesh overlays. It improves shape readability of very dense meshes, but increases eye fatigue when modeling lower poly.

Control the Anti-Aliasing for higher quality rendering.

Display overlays with smooth wire, without this wires will be rendered aliased. To increase the visibility you can disable this for Edit Mode specificity (see below), since edges do not blend into other shaded regions.

Display smooth wire in Edit Mode, without this wires will be rendered aliased.

Limit the maximum resolution for pictures used in textured display to save memory. The limit options are specified in a square of pixels (e.g: the option 256 means a texture of 256×256 pixels). This is useful for game engineers, whereas the texture limit matches paging blocks of the textures in the target graphic card memory.

Sets the level of anisotropic filtering. This improves the quality of textures that are rendered at the cost of performance.

Clip alpha below this threshold in the 3D Viewport. Note that, the default is set to a low value to prevent issues on some GPUs.

Method to render images; the following options are supported:

Automatically use GLSL which runs on the GPU for performance but falls back to the CPU for large images which might be slow when loaded with the GPU.

Uses CPU for display transform and render images as a 2D texture.

Fastest method using GLSL for display transform and render images as a 2D texture.

Under certain circumstances, the GPU will be used to subdivide a mesh with a Subdivision Surface modifier. This typically results in increased subdivision performance.

This feature is not supported on Qualcomm GPUs on Windows

---

## Viewport Gizmos¶

**URL:** https://docs.blender.org/manual/en/latest/editors/clip/display/gizmo.html

**Contents:**
- Viewport Gizmos¶
- Viewport Gizmos¶

Clicking (Show Gizmo) toggles all the gizmos in the Movie Clip Editor. The drop-down button displays a popover with more detailed settings, which are described below.

Toggle the visibility of the zooming and panning gizmos in the upper right corner.

---

## Viewport Gizmos¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/display/gizmo.html

**Contents:**
- Viewport Gizmos¶
- Viewport Gizmos¶
- Object Gizmos¶
- Empty¶
- Light¶
- Camera¶

Clicking (Show Gizmos) toggles all gizmos in the 3D Viewport. The drop-down button displays a popover with more detailed settings, which are described below.

Enable/disable the navigation gizmo.

Enable/disable the gizmo of the active tool.

Enable/disable the Object Gizmos for the active element (see below).

Object Gizmos allow mouse-controlled translation, rotation and scaling in the 3D Viewport. While they’re called “object” gizmos in the popover, they also apply to other transformable elements such as mesh vertices.

There is a separate gizmo for each operation. Each gizmo can be used separately or in combination with the others.

A gizmo always has three color-coded axes: X (red), Y (green), and Z (blue). You can drag an axis with LMB to transform along it. The Move and Scale gizmos additionally have small colored squares for transforming along two axes in one go.

Various modifier keys can be used:

Holding Ctrl at any time will toggle snapping and also make rotation and scaling work in coarse increments.

Holding Shift after pressing LMB will do the opposite of the above, “slowing down” the transformation relative to mouse movement to allow finer adjustments.

Holding Shift before pressing LMB will perform the transformation in the plane that’s perpendicular to the clicked axis. See Plane Locking.

The Gizmos popover has the following settings for object gizmos:

The orientation to use for the gizmo. Default means to use the viewport’s Transform Orientation. The other options override it.

Show the gizmo to control the location. Dragging the small white circle allows free movement in the viewing plane.

Show the gizmo to control the rotation. Dragging the large white circle allows rotation around the viewing direction. Dragging the translucent white disc within that circle (only visible when hovering over the gizmo) allows trackball rotation.

Show the gizmo to control the scale. Dragging the area between the small and large white circles scales along all three axes.

The latter three options are also available in a pie menu if you have the Grave Accent / Tilde Action in the Keymap Preferences set to Gizmos.

If you’re using a tool that’s tied to a particular gizmo setup (the Move, Rotate, Scale and Transform tools), the Move/Rotate/Scale checkboxes won’t have any effect.

The Gizmo Preferences.

Gizmo settings for empties.

Show the gizmo to adjust the image size and position.

Show the gizmo to adjust the force field.

Gizmo settings for lights.

Show the gizmo to adjust the Spot Size of spotlights.

Show the gizmo to adjust the direction of lights.

Gizmo settings for cameras.

Show the gizmo to adjust the focal length (for Perspective cameras) or orthographic scale (for Orthographic cameras).

Enable the gizmo for adjusting the focus distance. To see this gizmo, you need to enable the Viewport Display ‣ Limits checkbox in the camera’s properties (green camera icon).

---

## Viewport Overlays¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/display/overlays.html

**Contents:**
- Viewport Overlays¶
- General¶
  - Guides¶
  - Objects¶
  - Geometry¶
  - Viewer Node¶
  - Motion Tracking¶
- Mesh Edit Mode Overlays¶
  - Shading¶
  - Mesh Analysis¶

Clicking (Show Overlays) toggles all overlays in the 3D Viewport.

Cameras outline & passepartout are not considered Viewport overlays.

The drop-down button displays a popover with more detailed settings, which are described below.

Depending on the current object interaction mode, there may be a second button with yet more settings, which are also described here.

The following options are always present, independent of the current mode. Some of the overlays can be customized in the Viewport Preferences.

Show grid in orthographic side view.

Show the ground plane in perspective view.

Show the X, Y and/or Z axis lines.

The distance between lines in the grid/floor.

The number of subdivisions between grid lines.

Show various bits of information in the top left corner of the viewport.

View Perspective – Name of the View Perspective, such as “Top Orthographic” or “User Perspective.”

Playback Frame Rate (FPS) – Displays the Frames Per Second at which the animation is playing. By default, Blender goes through every single frame, which may result in an FPS that’s lower than intended (and the animation playing slower than realtime); the FPS turns red in this case. You can change this behavior in the Playback popover within an editors playback controls.

Object Info – Shows the current frame in parentheses, followed by the names of the selected Collection, the active object, and the active data-block’s name. When applicable, also shows the selected Shape Key and (in angle brackets) the Marker on the current frame. If the object has a keyframe on the current frame, the Object Info is displayed in yellow.

Grid Resolution – When the view is aligned to a world axis (see Viewpoint), the Text Info additionally shows the smallest distance between two parallel grid lines.

Show information about the amount of objects and geometry. Note that the counters depend on the current selection. For example, selecting a mesh gives info on the number of vertices, edges, and faces, while selecting a light shows the number of lights in the scene.

Objects – Number of the selected objects and the total count.

Geometry – Displays information about the current scene depending on the mode and object type. This can be the number of vertices, faces, triangles, or bones.

Show camera guides (Safe Areas & Composition Guides). Only available in camera view.

Show two spheres, one glossy and one diffuse, that react to lighting to assist in look development. Only available in Material Preview shading Shading Mode. The size of the spheres can be adjusted in the Viewport Preferences.

Show objects that don’t have geometry (such as empties, cameras and lights).

This also influences the display of:

Rigid Body Collision Shape

Shades the outline of light objects to the color the light produces.

Show dashed lines indicating parent or constraint relationships.

Show an outline around selected objects.

Show the motion path overlay.

Show the origins of the selected objects.

Show the origins of all objects.

The maximum opacity used for bones drawn in the Wireframe shading mode (or in Solid shading mode with X-Ray active). This is helpful when it is necessary to reduce clutter and focus on the mesh rather than bones.

Display mesh edges. Similar to Wireframe Shading, but displays edges on top of existing shading. The value slider adjusts which edges to display: lower values hide edges on surfaces that are almost flat, while a value of 1 shows all edges.

The opacity of the displayed edges, from 0 (invisible) to 1 (fully opaque).

In modes other than Object Mode, fade out objects that you’re not working on. The slider controls how much they’re faded out.

Highlights the backside of faces in red. In general, if a face is shown in red on the outside of a mesh, it’s most likely oriented incorrectly and needs to have its normal flipped. This can be done with the Flip or Recalculate operators for meshes, and with the Switch Direction operator for Surface objects.

Visualizes Attributes connected to the Viewer Node.

Visualize the value of the attribute connected to the Viewer Node as a grayscale color.

Opacity of the attribute that is currently visualized.

Show attribute values as text in viewport.

Show the motion tracking overlay.

Show the reconstructed camera path.

Show the names of the reconstructed tracking markers.

Change the display of the tracking markers: plain axes, arrows and so on.

Change the display size of the tracking markers.

The following options are available when in Mesh Edit Mode.

Highlight selected faces. Affects all selection modes.

Show face center points in solid shading modes. (They’re always shown in wireframe shading mode.)

Only affects face selection mode.

Display edges marked with a crease for the Subdivision Surface Modifier.

Display sharp edges, used with the Edge Split modifier.

Display weights created for the Bevel Modifier.

Display the UV unwrapping seams.

Display the indices of selected vertices, edges, and faces.

This overlay is useful when you have a sculpted mesh with the desired shape and want to recreate it with better topology. It makes the edited mesh see-through (so that you can see the sculpted mesh underneath it) and optionally renders it in front of nearby geometry (so that you can see it underneath the sculpted mesh).

Distance to “move the edited mesh towards the camera.” Use this to display the mesh in front of other objects that would normally occlude it.

Visualize the weights of the active vertex group, much like in Weight Paint mode.

Display unreferenced and zero-weighted areas in black. This helps to identify areas with very low weights that have been painted onto.

Vertices are displayed in the usual way.

Vertices are shown in black if they have no weight in the active vertex group.

Vertices are shown in black if they have no weight in any vertex group.

Show the Mesh Analysis overlay.

Show numerical measures of the selected elements. The Units can be set in the Scene properties.

Show the length of selected edges.

Show the angle of selected edges between two faces.

Show the area of selected faces.

Show the angle of selected face corners.

Geometry connected to the selection is shown while transforming, allowing you to move a vertex and see the connected edge lengths for example.

These values respect the Transform Space in the Sidebar. Use Global if you want the object’s scale to be applied to the measurements.

The Measure tool for measuring arbitrary distances and angles.

Display vertex normals

Display face normals at vertices (split normals)

The size to show the selected normals.

Keep the size of normals constant in relation to the zoom level.

These settings apply to the Freestyle Line Art renderer.

Display Freestyle edge marks.

Display Freestyle face marks.

Show Masks as overlays on an object. The opacity of the overlay can be adjusted.

Show Face Sets as overlays on an object. The opacity of the overlay can be adjusted.

Does nothing. (Stencil masks are only available for texture painting.)

Display mesh edges in white (unlike the Wireframe overlay which shows them in black).

The opacity of the overlay.

Display unreferenced and zero-weighted areas in black. This helps to identify areas with very low weights that have been painted onto.

Vertices are displayed in the usual way.

Vertices are shown in black if they have no weight in the active vertex group.

Vertices are shown in black if they have no weight in any vertex group.

Show contour lines formed by points with the same interpolated weight.

This visualizes weight variations too small to be seen from colors and can be useful for judging the smoothness and consistency of gradients, e.g. when using smoothing tools and brushes.

Display mesh edges in white (unlike the Wireframe overlay which shows them in black).

Opacity of the stencil mask overlay.

Show the bones on top and face other geometry to the back. The opacity can be controlled with the slider. Only available in Pose Mode.

These overlays are available when a Grease Pencil object is selected.

Show ghosts of the keyframes before and after the current frame. If Multiframe is enabled, ghosts of the selected keyframes are shown instead. See Onion Skinning.

Show only the onion skins of the active object.

Decrease the opacity of all the layers in the object other than the active one. The opacity factor can be controlled with the slider.

Cover all of the viewport except the active Grease Pencil object with a full color layer to improve visibility while drawing over complex scenes.

Include or exclude Grease Pencil objects.

Shows a line between points on top of other geometry when editing strokes.

When Multiframe is enabled and keyframes other than the current frame are selected, strokes on those keyframes are displayed as just their edit lines – the strokes themselves are hidden. Note that this does not affect Onion Skinning.

Controls the visibility of Bézier curve handles in edit mode.

Hides all Bézier curve handles, providing an unobstructed view of the curve.

Displays the handles only for selected control points.

Displays the handles for all control points in the curve.

Toggle the display of the selected strokes’ start points (green) and end points (red) to visualize their direction.

Show material name next to the selected strokes.

The opacity of the vertex color overlay in Vertex Paint Mode and Draw Mode. Note that in Draw Mode, vertex paint is only visible in the Material Preview and Rendered shading modes by default. To see it in Solid mode, you either need to use Vertex Paint Mode, or set the Color shading setting to Attribute.

Display a grid over the Grease Pencil drawing plane.

The opacity of the grid.

Objects are drawn behind the canvas grid.

The number of subdivisions between grid lines.

The color of the grid lines.

The horizontal/vertical size of the grid.

The amount to shift the grid up/down and left/right.

---

## View Regions¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/navigate/regions.html

**Contents:**
- View Regions¶
- Clipping Region¶
  - Example¶
- Render Region¶

View ‣ View Regions ‣ Clipping Region…

Allows you to define a clipping region to limit the 3D Viewport display to a portion of 3D space. It can assist in the process of working with complex models and scenes.

Once activated, you have to draw a rectangle with the mouse. It becomes a clipping volume of four planes:

A right-angled parallelepiped (of infinite length) if your view is orthographic.

A rectangular-based pyramid (of infinite height) if your view is in perspective.

Once clipping is used, you will only see what’s inside the volume you defined. Tools such as paint, sculpt, selection, transform snapping, etc. will also ignore geometry outside the clipping bounds.

To delete this clipping, press Alt-B again.

The Region/Volume clipping image shows an example of using the clipping tool with a cube. Start by activating the tool with Alt-B. This will generate a dashed cross-hair cursor. Click with the LMB and drag out a rectangular region. Now clipping is applied against that region in 3D space. Use the MMB to rotate the view and you will see that only what is inside the clipping volume is visible. All the editing tools still function as normal, but only within the clipping volume.

The dark gray area is the clipping volume itself. Once clipping is deactivated with another Alt-B, all of 3D space will become visible again.

View ‣ View Regions ‣ Render Region… View ‣ View Regions ‣ Clear Render Region

Mark: Ctrl-B Clear: Ctrl-Alt-B

Allows you to limit rendering to a 2D rectangular area. If you’re busy tweaking just a small part of the scene, it can be quite wasteful to have the whole viewport in Rendered shading mode or make full-frame renders, so this feature lets you save time.

You can define Render Regions in two different contexts:

If you define one while in Camera View, it will apply not just to the viewport, but also to the final render. If you want to temporarily disable this region rather than clearing it entirely, you can do so in the Output tab of the Properties editor.

If you define one while not in Camera View, it will only apply to the viewport. If you want to temporarily disable this region rather than clearing it entirely, you can do so in the Sidebar.

Both Render Regions can exist at the same time.

Render regions only apply to the viewport when using Cycles, not when using EEVEE. However, they always affect the final render.

---
