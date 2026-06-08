# Blender - Interface

**Pages:** 169

---

## 3D Cursor¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/controls/pivot_point/3d_cursor.html

**Contents:**
- 3D Cursor¶
- Example¶

Object Mode and Edit Mode

Header ‣ Transform Pivot Point ‣ 3D Cursor ()

Places the pivot point at the location of the 3D Cursor.

The image below shows the difference between rotating an object around the 3D Cursor (left) and rotating it around the Median Point (right).

Rotation around the 3D Cursor compared to the Median Point.¶

---

## Active Element¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/controls/pivot_point/active_element.html

**Contents:**
- Active Element¶
- In Object Mode¶
- In Edit Mode¶

Object Mode and Edit Mode

Header ‣ Transform Pivot Point ‣ Active Element ()

Places the pivot point at the active element, which is the element that was selected most recently.

When in Object Mode, rotation and scaling happen around the origin of the active object, which is the element with a lighter outline than the others.

The effect of the pivot point is shown in the image below, where the active object (the cube) remains in the same location while the others move.

Starting point, rotation, and scaling.¶

When in Edit Mode, rotation and scaling happen around the centerpoint of the active element, which is the element with a white outline. That centerpoint remains in the same location while everything else is transformed around it.

The image below illustrates rotation around the active vertex, edge, and face. Each time, the active element rotates in place, while the others “orbit” around it. In the case of vertices, the active vertex is not changed at all, as a vertex on its own is just a point that has no concept of rotation.

Left column: starting situation, right column: after rotation.¶

---

## Adaptive Domain¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/domain/gas/adaptive_domain.html

**Contents:**
- Adaptive Domain¶

Physics ‣ Fluid ‣ Adaptive Domain

When enabled, the domain will adaptively shrink to best fit the gas, saving computation time by leaving voxels without gas out of the simulation. Unless the Add Resolution is used, the adaptive domain will not exceed the bounds of the original domain.

Number of voxels to add around the outside of the domain.

Amount of extra space to leave around gas, measured in voxels. With very fast-moving gas larger margins may be required to prevent the gas from being cut off by the adaptive boundary, but note this will increase the number of voxels which need to be computed.

Smallest amount of gas a voxel can contain before it is considered empty and the adaptive domain is allowed to cut it out of the simulation.

---

## Animation Tools¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/animation/tools.html

**Contents:**
- Animation Tools¶
- Insert Blank Keyframe (Active Layer)¶
- Insert Blank Keyframe (All Layers)¶
- Duplicate Active Keyframe (Active Layer)¶
- Duplicate Active Keyframe (All Layers)¶
- Delete Active Keyframe (Active Layer)¶
- Delete Active Keyframe (All Layers)¶
- Interpolate Sequence¶
- Bake Object Transform to Grease Pencil¶

Draw Mode, Edit Mode, Sculpt Mode

Stroke ‣ Animation ‣ Insert Blank Keyframe (Active Layer)

Add a new blank keyframe to the active layer at the current frame. If there is already a keyframe at the current frame, a new blank keyframe will be added on the next frame.

When enabled, Blank keyframe will be created on all layers, not only the active one.

The number of blank frames to insert.

Draw Mode, Edit Mode, Sculpt Mode

Stroke ‣ Animation ‣ Insert Blank Keyframe (All Layers)

Same as Insert Blank Keyframe (Active Layer) but All Layers is enabled by default.

Draw Mode, Edit Mode, Sculpt Mode

Stroke ‣ Animation ‣ Duplicate Active Keyframe (Active Layer)

Duplicates the strokes on the last keyframe by copying them to the current frame.

Pick which layers to duplicate.

Duplicate only the active layer.

Duplicate all the layers.

Draw Mode, Edit Mode, Sculpt Mode

Stroke ‣ Animation ‣ Duplicate Active Keyframe (All Layers)

Same as Duplicate Active Keyframe (Active Layer) but the Mode is set to All by default.

Draw Mode, Edit Mode, Sculpt Mode

Stroke ‣ Animation ‣ Delete Active Keyframe (Active Layer)

Deletes the last keyframe in the Dope Sheet or the current keyframe if you are on one.

Pick which layer to delete keyframes.

Deletes current frame in the active layer.

Delete active frames for all layers.

Draw Mode, Edit Mode, Sculpt Mode

Stroke ‣ Animation ‣ Delete Active Keyframes (All Layers)

Same as Duplicate Active Keyframe (Active Layer) but the Type is set to All Active Frames by default.

Grease Pencil ‣ Interpolate Sequence

Interpolate strokes between the previous and next keyframe by adding multiple keyframes. A breakdown keyframe will be added on every frame between the previous and next keyframe.

Number of frames between generated interpolated frames.

Layers included in the interpolation.

Exclude existing Breakdowns keyframes as interpolation extremes.

Invert destination stroke to match start and end with source stroke.

Amount of smoothing to apply to interpolated strokes, to reduce jitter/noise.

Number of times to smooth newly created strokes.

Interpolation method to use the next time Interpolate Sequence is run.

Object ‣ Animation ‣ Bake Object Transform to Grease Pencil

Applies all transform animation at Object level within a selected frame range to Grease Pencil object keyframes.

Start/End frame for the baking process.

Frame steps for the baking process.

Convert only the selected keyframes.

Target destination frame for the baked animation.

Sets the projection type to use for the converted strokes.

---

## Annotations¶

**URL:** https://docs.blender.org/manual/en/latest/interface/annotate_tool.html

**Contents:**
- Annotations¶
- Annotation Tools¶
- Tool Settings¶
  - Common¶
  - Annotate Line¶
- Annotation Layers¶
  - Onion Skin¶

The annotation tool is available in multiple editors. It can be used to add notes to e.g. 3D objects or node setups. The arrow in the screenshot below is an annotation.

Annotations tool in a node editor.¶

The annotation tool can be activated in the Toolbar and has the following sub-tools:

Draw free-hand strokes in the main area.

Click and drag to create a line. Optionally, you can select the arrow style for the start and end of the line.

Click multiple times to create multiple connected lines, then press Return or Esc to confirm.

Click and drag to remove lines. The eraser has a Radius setting found in Tool Settings.

Adjust the color of existing and new strokes.

A pop-over menu, showing the name of the current layer, to access the Annotation Layers.

Determines where the annotations are drawn.

Only available in the 3D Viewport. The new annotations become part of the 3D scene; they’re drawn on an imaginary plane that goes through the 3D Cursor and is aligned to your view.

Only available in the 3D Viewport. The new annotations become part of the 3D scene; they’re drawn onto the surface of the object under the mouse. If there is no surface, you get the same behavior as 3D Cursor.

Only available in 2D editors such as the Image Editor. The annotations become part of the 2D space, meaning their position and size change as you pan and zoom in the editor.

The new annotations are 2D and get stuck to the screen. They keep the same position, rotation and size no matter how you pan, orbit or zoom in the editor.

Only use the first and last parts of the stroke for snapping.

Only project the strokes onto selected objects.

Helps to reduce jitter of the strokes while drawing by delaying and correcting the location of points.

Minimum distance from the last point before the stroke continues.

A smooth factor, where higher values result in smoother strokes but the drawing sensation feels like as if you were pulling the stroke.

The decoration to use at the beginning or end of the line segment. This can be used for example to create arrows to point out specific details in a scene.

When the annotation tool is enabled, the settings for managing multiple layers can be found in the Sidebar ‣ View ‣ Annotations panel.

Adjusts the opacity of existing and new strokes.

Adjusts the thickness of existing and new strokes.

Shows a ghosted image of strokes made in frames before and after the current frame. Onion skinning only works in the 3D Viewport and Sequencer. See the Grease Pencil documentation for an explanation of Onion Skinning.

Color to use before and after the current frame on ghost frames. The number defines how many frames to show before and after the current frame.

---

## Arc Tool¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/arc.html

**Contents:**
- Arc Tool¶
- Tool Settings¶
  - Brush Asset¶
  - Brush Settings¶
  - Color¶
- Usage¶
  - Selecting a Brush and Material¶
  - Creating Arcs¶
  - Extruding¶

The Arc tool create simple arcs using any of the Draw type brushes.

You can configure the brush main settings exposed on the Tool Settings for convenience. For the draw brushes configuration and settings see: Draw Brush.

The number of stroke points between each stroke edge.

Use a curve widget to define the stroke thickness from the start (left) to end (right) of the stroke.

When enabled, the stroke use a curve profile to control the thickness along the arc.

Picks the brush asset used by the tool.

See Brush Asset for more information.

See Draw Brushes for a detailed list of all draw brushes and their options.

Parameters to control to look of the stroke.

See Draw Brushes for details.

Settings to determine the color of strokes.

In the Tool Settings select the brush, material and color type to use with the tool. The Arc tool uses Draw Brush types. See Brush Settings for more information.

Click (LMB or the Pen tip) and drag the start point.

Release on the desired end point.

After releasing you can tweak the arc using a single cyan manipulator (hand icon).

Then confirm (Return/MMB) or cancel (Esc/RMB).

While dragging you can use Shift to make a perfect arc, use Alt to create the arc from a center point or M to flip.

NumpadPlus and NumpadMinus or using the mouse Wheel will increase or decrease the amount of points in the final arc.

F will adjust the line thickness and Shift-F will adjust the opacity of the strokes.

click and dragging the start point.¶

Tweaking arc with the manipulator.¶

The arc after confirming.¶

Before confirming you can use E to extrude the end point of the arc to generate multiple connected arcs.

End point extruding.¶

Tweaking the last arc with the manipulator.¶

The connected arcs after confirming.¶

---

## Areas¶

**URL:** https://docs.blender.org/manual/en/latest/interface/window_system/areas.html

**Contents:**
- Areas¶
- Resizing¶
- Docking¶
  - Joining¶
  - Splitting¶
- Area Options¶
- Swapping Contents¶
- Maximize Area¶
- Restore Area¶
- Focus Mode¶

Area boundaries are indicated by rounded corners (yellow highlights).¶

The Blender window is divided into a number of rectangles called Areas. Areas reserve screen space for Editors, such as the 3D Viewport or the Outliner. Each editor offers a specific piece of functionality.

Areas are grouped into Workspaces, which are geared towards particular tasks (modeling, animating and so on).

While some keyboard shortcuts in Blender are global (such as Ctrl-S for saving), many depend on which editor the mouse cursor is hovering over.

As an example, say you just selected two objects in the Outliner and want to join them. If you pressed the shortcut for this (Ctrl-J) while the cursor is still in the Outliner, nothing would happen as the shortcut isn’t valid there; you first need to move your cursor to the 3D Viewport.

The size of the border around areas can be adjusted in the user preferences with Border Width.

Handles can be enabled to always remain visible, which can help with area management on touch-enabled devices. See Show – Corner Handles:.

You can resize areas by dragging their borders with LMB. Move your mouse cursor over the border between two areas, so that the cursor changes to a double-headed arrow, and then click and drag. Hold Ctrl to snap the size of areas to convenient sizes.

Docking describes several ways an area a user can interactively manipulate the size and location of areas along with splitting an area into new areas.

To start the interactive process, placing the mouse cursor in an area corner will change the cursor to a cross (+). Once the cursor is a cross, press and hold LMB to preform any of the following actions:

If you press Esc or RMB before releasing the mouse, the operation will be canceled.

Properties is being joined to the Outliner.¶

Dragging from an area corner into the space of a second area will join two areas. The areas that will be joined will be displayed brighter.

Splitting an area will create a new area. Dragging from an area corner left/right will split the area vertically, to split the area horizontally drag up/down.

You can split and join areas at once by dragging a split operation into a separate area.

Dragging an area into the middle of an second area will replace the second area with the first area.

RMB on the border opens the Area Options.

Shows an indicator line that lets you select the area and position where to split. Tab switches between vertical/horizontal.

Shows the join direction overlay.

Swaps this area with the adjacent one.

You can swap the contents of two areas by pressing Ctrl-LMB on one of the corners of the initial area, dragging towards the target area, and releasing the mouse there. The two areas do not need to be side-by-side, though they must be inside the same window.

View ‣ Area ‣ Toggle Maximize Area

Expands the editor area so it fills the whole window, while keeping the Topbar and Status Bar visible. This is useful for focusing on a single editor (e.g. 3D Viewport, Shader Editor) without changing your workspace layout.

In the 3D Viewport, maximizing the area temporarily hides:

To return to normal size, use the shortcut again or click the Back to Previous button in the Topbar.

View ‣ Area ‣ Restore Area

Returns the maximized area back to its original size and restores the previous screen layout.

View ‣ Area ‣ Focus Mode

Expands the editor area so it fills the entire window, hiding:

Secondary regions (such as toolbars, sidebars, headers, etc.) of the editor itself.

This mode gives the maximum possible screen space for the active editor.

To return to normal size, use the shortcut again or click the icon in the top-right corner of the editor (visible only when hovering over the area).

View ‣ Area ‣ Duplicate Area into New Window

Creates a new floating window containing a duplicate of the current editor area. The new window is fully functional and part of the same Blender instance.

This is especially useful when working with multiple monitors.

You can also create a new window by holding Shift-LMB on an area corner and dragging outward slightly.

---

## Arranging Nodes¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/arranging.html

**Contents:**
- Arranging Nodes¶
- Snapping¶
- Auto-Offset¶

Snapping aligns the position and size of nodes to the background grid. This feature allows nodes to snap to a grid, ensuring that node layouts remain clean and visually aligned. Snapping can be toggling the snap icon (/) in the editor’s headers or toggled temporarily while transforming nodes by holding Ctrl.

When you drop a node with at least one input and one output socket onto an existing connection between two nodes, Auto-offset will, depending on the direction setting, automatically move the left or right node away to make room for the new node. Auto-offset is a feature that helps organizing node layouts interactively without interrupting the user workflow.

Auto-offset is enabled by default, but it can be disabled in the Preferences.

You can toggle the offset direction while you are moving the node by pressing T.

The offset margin can be changed using the Auto-offset Margin setting in the Editing section of the Preferences.

Auto-Offset. A workflow enhancement for Blender’s node editors.

---

## Asset Browser¶

**URL:** https://docs.blender.org/manual/en/latest/editors/asset_browser.html

**Contents:**
- Asset Browser¶
- Interface¶
  - Header¶
    - Import Settings¶
    - Display Settings¶
  - Main Region¶
  - Asset Library Region¶
  - Asset Details Region¶
    - Preview¶
    - Tags¶

The Asset Browser is the main interface for organizing and using assets. To access it, create a new area, click the Editor Type button in its top left corner, and choose Asset Browser.

For general information on Blender’s asset library system, including how to create and edit assets, and design choices.

For organizing assets.

Built on top of the Asset Browser.

Asset Browser, showing materials in an asset library.¶

Determines how data is managed when an asset is imported. This option can be found in the center of the Asset Browser header (when an asset library other than Current File or Essentials is selected):

Use the import method set in the File Path Preferences.

The asset will be linked to the current blend-file, and thus be read-only. Later changes to the asset file will be reflected in all files that link it.

The asset and all its dependencies will be Appended (copied) into the current file. Dragging a material into the scene three times will result in three independent copies. Dragging an object into the scene three times will also result in three independent copies.

“Dependencies” in this case means everything the asset refers to. For an object, this can be its mesh and materials, but also other objects used by modifiers, constraints, or drivers.

Since the file now has its own copy of the asset, later changes to the asset file will not be reflected in the file it’s appended from.

Imports the asset as linked data and immediately packs it into the current blend-file. This ensures that the asset remains available even if the original library data is modified or becomes unavailable.

Useful for maintaining self-contained files that do not rely on external asset library paths.

Mimics the Instance Collections option when appending from the file browser

Some asset types such as collections can be created as an instanced collection. This is done by enabling the Instance option after dragging collection assets into the 3D Viewport. By enabling these options, an empty object is added that uses an instance of the collection. If these option is disabled, the full collection hierarchy will be added to the scene.

Collection Assets from the current file will always be instanced.

Adjusts how assets are displayed in the asset list.

Control how files are displayed.

Displays files and folders in a horizontal list.

Change the size of thumbnails in list views.

The width of columns in horizontal list views.

Changes the size of the preview thumbnails.

Sort the asset list alphabetically.

Sort the asset list so that assets in the same catalog are kept together. Within a single catalog, assets are ordered by name. The catalogs are in order of the flattened catalog hierarchy.

The center region of the Asset Browser lists the assets contained in the selected catalog.

Click LMB to select a single asset. Additionally hold Ctrl to add/remove that asset to/from the selection, or Shift to select a range of assets. You can also drag LMB to perform a box select.

The region has a context menu with the following operations:

Opens the blend-file containing the asset.

Changes the size of the preview thumbnails.

The region on the left lets you select an asset library and shows its catalogs. You can show/hide this region by pressing T.

The asset library whose catalogs to show.

Show catalogs from all available libraries.

Show the catalogs in the current blend-file (even if that file is not yet part of an asset library). See The Current File Asset Library for more information.

Show the catalogs that come bundled with Blender.

Any libraries that you added in the File Path Preferences are listed here too.

Shown when Asset Library is set to Current File and the current blend-file is an asset bundle that’s not yet part of an asset library.

Lets you select a target asset library, then opens a File Browser in that library’s root folder so you can save the current blend-file there. Once saved, the assets in the blend-file become available as part of the library.

Tree view that shows the catalogs of the selected asset library. A catalog is a group of assets; when you select one, only the assets in that catalog and its child catalogs will be listed.

You can rename a catalog by double-clicking it, or assign it to a different parent catalog by dragging and dropping.

Add-ons and features like the Pose Library can show custom panels here.

The region on the right shows the metadata of the active asset. You can show/hide this region by pressing N or clicking the gear icon in the header.

Only metadata of assets contained in the current blend-file can be edited.

The asset’s name. Unique for the asset data type within the same blend-file.

The full path of the blend-file that contains the asset.

Opens the blend-file that contains the asset in a new Blender instance. When this instance is closed, the Asset Browser will be automatically refreshed.

Optional name of the license under which this asset is distributed. Not used by Blender itself.

Optional copyright notice. Not used by Blender itself.

Optional asset description. Not used by Blender itself.

Optional field for the asset author. Not used by Blender itself.

Shows the preview image of the asset. See Asset Previews.

Opens a File Browser where you can select a new image for the asset preview.

Autogenerate a new preview for the asset.

Menu of additional preview operators.

Generates a preview based on the 3D Viewport’s Active object. This is useful for node groups, which cannot automatically generate their own preview.

Remove the preview of the asset.

Drag-select a rectangle over an area of Blender to capture it as the preview image of the asset. See Screenshot Capture for Previews.

Panel for viewing and editing asset tags. These do not have any meaning to Blender and can be chosen freely. When using the search field to filter the assets, the assets whose tags (partially) match the search term will also be shown.

Depending on the current mode of the object and the selected asset types, more panels may be shown. For example, see Pose Library.

As a general rule, an asset can be used by dragging it from the Asset Browser to the desired location. Objects and worlds can be dragged from the Asset Browser into the scene. Materials can be dragged onto the object that should use them. Geometry nodes can also be dragged onto objects to add a Geometry Nodes Modifier. The use of pose assets is different, and is described in Pose Library.

When you drag a collection, it will be added as an instance – that is, a single object representing the entire collection, meaning the contents aren’t visible in the Outliner and can’t be edited. You can change this in the following ways:

Use Make Instances Real to replace the object by the collection contents.

Alternatively: delete the object, find the collection in the Outliner’s Blender File Display Mode, and click Link to Scene in its context menu.

There are several things that can happen when an asset is used, depending on the Import Method.

Note that all regular Blender operations are available after the asset has been added to the current file. For example, you could choose to link an object to the scene; this will also link its mesh and its materials. Then you can make the object itself local (Object ‣ Relations ‣ Make Local… ‣ Selected Objects), while keeping the mesh and materials linked to the asset files. This will result in a local, and thus editable, object, and keep the mesh and materials automatically up to date with any changes in the asset library.

Preview panel in the Asset Browser.¶

Preview images are typically generated automatically when you mark a data-block as an asset. Objects are captured from their local -Y axis, while collections are captured from the global -Y axis (as these don’t have a local axis).

If the auto-generated preview image isn’t sufficient, you can replace it by a custom one.

For previews of pose assets, see Controlling the Look of Preview Images.

In case a specific preview is needed, a fast way to create it is with a screenshot. The operator to do so is located under the Preview popover, see Capture Screenshot Preview. It is only possible to take screenshots for editable assets, so assets in the Current File and Asset System Files.

Once started, you can click and drag a rectangular area over any part of Blender to capture a preview image. During dragging it is possible to move the whole capture area or to unlock the aspect ratio. See the shortcut help in the status bar for information on which keys to press.

On a re-run of the operator, the previously captured area will be remembered. Simply clicking allows you to easily take the same screenshot again.

Selecting an area that is completely within a single 3D viewport will actually do a background render of that section. This allows the background to be transparent, but also means that UI elements can not be captured.

Asset bundles are blend-files that do not reference any other file, and whose name ends in _bundle.blend. Any textures and other external files need to be packed into the current blend-file.

Asset bundles can be copied to an asset library via the Asset Browser:

Open the asset bundle blend-file.

Switch its Asset Browser to Current File (if it’s not set to that already).

Click on Copy Bundle to Asset Library.

Choose the asset library to copy it to.

A File Browser will open at the root folder of the selected asset library. Choose the desired location of the blend-file, and click the Copy to Asset Library button.

The blend-file will be saved at the chosen location, and any catalogs of the asset bundle will be merged into the target asset library.

Both the word “asset” and the word “bundle” are commonly used, and not necessarily with the same meaning as described here. Not everything that’s presented as an “asset bundle” will have the Copy to Asset Library functionality available; for that, the bundle file needs to adhere to the definition above.

---

## Blender 5.0 Reference Manual¶

**URL:** https://docs.blender.org/manual/en/latest/

**Contents:**
- Blender 5.0 Reference Manual¶
- Getting Started¶
- Sections¶
- Get Involved¶

Welcome to the manual for Blender, the free and open source 3D creation suite.

This site can be used offline:

Download the manual as web pages (HTML)

Download the manual in an e-book format (EPUB)

An introduction to Blender’s window system, widgets and tools.

Overview of the interface and functionality of all editors.

Objects and their organization into scenes, view layers and collections.

Meshes, curves, metaballs, text, modeling tools, and modifiers.

Sculpting, texture painting and vertex painting.

2D drawing and animation with Grease Pencil.

Keyframes, drivers, constraints, armatures and shape keys.

Physics simulations, particle systems and dynamic paint.

Rendering and shading with EEVEE, Cycles and Freestyle.

Post-processing with the compositing nodes.

Video motion tracking & masking.

Video editing with the sequencer.

Data-block management and the structure of blend-files.

Additional functionality available as add-ons.

Python scripting, how to write add-ons and a reference for command-line arguments.

Solving crashes, graphics issues and Python errors, recovering data and reporting bugs.

A list of terms and definitions used in Blender and this manual.

A list of terms linked to the Glossary.

Help write Blender’s future! ✏️ Contribute to the Blender Manual and share your knowledge with creators worldwide. No matter your expertise, your contributions can make Blender easier to learn and use for everyone. Join the team and start documenting Blender today!

Help bring Blender to the world! 🌍 Join the translation effort to make the Blender accessible in more languages.

Translate Blender’s UI

Translate Blender’s User Manual

---

## Bounding Box Center¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/controls/pivot_point/bounding_box_center.html

**Contents:**
- Bounding Box Center¶
- In Object Mode¶
- In Edit Mode¶

Object Mode and Edit Mode

Header ‣ Transform Pivot Point ‣ Bounding Box Center ()

In this mode, the pivot point lies at the center of the bounding box, which is a box that’s wrapped as tightly as possible around the selection while still being aligned to the world axes.

The pivot point becomes the center of the bounding box around the selected objects’ origin points, not their geometry.

This means that, if you have a single object selected, the pivot point is the same as the object’s origin point – which can be customized and doesn’t have to be in the center. In the example below, the orange rectangle has it in a corner instead.

Single object rotation.¶

If you have multiple objects selected, the pivot point becomes the center of an imaginary box around their origins.

The image below shows the difference between Bounding Box Center and Median Point. The latter calculates the average position of the origins, meaning that the pivot point shifts towards the area with the most objects.

Difference between “Bounding Box Center” (left) and “Median Point” (right).¶

The pivot point becomes the center of the bounding box around the selected mesh elements.

The effects of rotation in different mesh selection modes. The pivot point is shown by a yellow circle.¶

Median Point may again give a different result.

Difference between “Bounding Box Center” (left) and “Median Point” (right).¶

---

## Box Tool¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/box.html

**Contents:**
- Box Tool¶
- Tool Settings¶
- Usage¶
  - Selecting a Brush and Material¶
  - Creating Boxes¶

The Box tool create rectangular shapes.

You can configure the brush main settings exposed on the Tool Settings for convenience. For the draw brushes configuration and settings see: Draw Brush.

The number of stroke points between each stroke edge.

Use a curve widget to define the stroke thickness from the start (left) to end (right) of the stroke.

When enabled, the stroke use a curve profile to control the thickness along the line.

In the Tool Settings select the brush, material and color type to use with the tool. The Box tool uses Draw Brush types. See Brush Settings for more information.

Click (LMB or the Pen tip) and drag the start point.

Release on the desired end point.

After releasing you can move the start and end point by clicking and dragging on the yellow manipulators.

Then confirm (Return/MMB) or cancel (Esc/RMB).

While dragging you can use Shift to make a perfect square or use Alt to create the box from a center point.

NumpadPlus and NumpadMinus or using the mouse Wheel will increase or decrease the amount of points in the final box.

F will adjust the line thickness and Shift-F will adjust the opacity of the strokes.

click and dragging the start point.¶

Moving start and end points with manipulators.¶

The box after confirming.¶

---

## Braid Hair Curves¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/hair/guides/braid_hair_curves.html

**Contents:**
- Braid Hair Curves¶
- Inputs¶
  - Shape Parameters¶
  - Hair Tie¶
  - Guide Map¶
- Outputs¶
  - Guide Map¶

The Braid Hair Curves node deforms existing hair curves into braided strands by grouping nearby curves around guide curves. The deformation creates a multi-strand braid pattern, with options for radius, twist frequency, strand thickness, and an optional flare or tied ending.

This node is designed for grooming workflows where a few curves act as braid guides, and surrounding curves are wrapped around them to form a structured braid.

The input geometry containing the hair curves to deform into braids.

Controls how strongly the braiding effect is applied. A value of 0.0 leaves the hair unchanged, while 1.0 applies the full braid deformation.

The number of subdivisions applied to curves before deformation. Higher values allow smoother braids at the cost of performance.

Controls where along each curve the braid effect begins, measured from the root. Lower values start the braid closer to the root, higher values leave more unbraided length.

The overall radius of the braid. Larger values create a thicker braid by moving the strands farther from the braid center.

Adjusts the radius profile along each curve. This can be used to taper or vary the braid width from root to tip.

Controls how quickly the curves twist around the center of the braid. Higher values create tighter, more frequent wrapping. This input can vary per point along a curve, allowing twists to tighten or loosen along the length.

Minimum radius factor for the braid cross-section. This determines how close strands can get to the braid center.

Maximum radius factor for the braid cross-section. This determines how far strands can move outward from the center.

The thickness of each strand of hair within the braid.

Adjusts how strand thickness changes along the length of the braid.

Introduces asymmetry in the strand shaping. This breaks perfect radial uniformity, helping the braid feel more organic.

The length of the flare at the end of the braid, where the strands loosen or fan out.

The radius of that flare at the tip of the braid. Higher values create a wider, more open flare.

Defines how the hair tie object (e.g. a band or wrap) is provided for instancing.

Use an object reference for the hair tie instance.

Use a geometry input directly.

The object or geometry used as the hair tie to cap or bind the end of the braid.

The scale of the hair tie instance.

A map that specifies which curve should act as the central “guide” for each braid group. If provided, this overrides any existing guide_curve_index attribute, and the Guide Distance and Guide Mask inputs are ignored.

The minimum spacing between selected guides when automatically generating a guide map. Larger values result in fewer guides, forming larger braid groups.

A mask that determines which curves are allowed to be considered as guides.

When enabled, use an existing guide map attribute (for example, guide_curve_index) if it is already present. If this is disabled and Guide Index is not provided, a new guide map is generated using Guide Distance and Guide Mask. Creating the guide map ahead of time, in a separate node or modifier, gives more precise control over which curves act as braid guides.

The resulting geometry with braided deformation applied.

A value from 0 to 1 indicating the position along the braid flare region. This can be used for shading or for adding effects (such as tying, binding, or loosening near the braid tip).

An index identifying which strand of the braid each curve belongs to within its braid group.

The guide index map actually used to generate the braid. If a new guide map was created by this node, it is provided here for reuse downstream.

---

## Brush¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/brush_tool.html

**Contents:**
- Brush¶

Tool to use for any of the Sculpt mode brushes. Activating a brush from an asset shelf or brush selector will also activate this tool for convenience.

See the list of Essentials Brushes (based on available Brush Types) for more details.

---

## Brush Tool¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/brush.html

**Contents:**
- Brush Tool¶
- Tool Settings¶
  - Brush Asset¶
  - Brush Settings¶
  - Eraser¶
  - Color¶
- Usage¶
  - Selecting a Brush and Material¶
  - Free-hand Drawing¶
  - Stabilize Stroke¶

Tool to free form draw Grease Pencil strokes using any of the Draw type brushes.

Activating a brush asset from an asset shelf or brush selector will also activate this tool for convenience.

Picks the brush asset used by the tool.

See Brush Asset for more information.

See Draw Brushes for a detailed list of all draw brushes and their options.

Parameters to control to look of the stroke.

See Draw Brushes for details.

Select a brush to use as eraser for quickly alternating with the main brush using Ctrl-LMB.

Settings to determine the color of strokes.

In the Tool Settings select the brush, material and color type to use with the tool. The Draw tool uses Draw Brush types. See Brush Settings for more information.

Click and hold LMB or use the pen tip to make free-hand drawing on the viewport.

Shift-LMB toggle the use of Stabilize Stroke on the brush to have more control while drawing and get smoother lines.

Alt-LMB Constrains the drawing of the strokes to horizontal or vertical straight lines.

Ctrl-LMB changes temporally to the active Erase tool. See Erase Tool for more information.

You can also use B to delete all the points in the selected drawing area.

---

## Build Modifier¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/modifiers/generate/build.html

**Contents:**
- Build Modifier¶
- Options¶
  - Randomize¶
- Example¶

The Build modifier causes the faces of the mesh object to appear or disappear one after the other over time.

By default, faces appear in the order in which they are stored in memory (by default, the order of creation). The face/vertex order can be altered in Edit Mode by using Sort Mesh Elements.

The start frame of the building process.

The number of frames over which to rebuild the object.

The modifier will operate in reverse, essentially allowing it to be used as a “deconstruction” effect. This is useful for making a set of instancing objects gradually disappear.

Randomizes the order in which the faces are built.

The random seed. Changing this value gives a different “random” order when Randomize is checked. This order is always the same for a given seed/mesh set.

The Build modifier can be used to make a large number of items to progressively appear, without resorting to animating the visibility of each one by one. Examples of this include a mesh containing vertices only, which is used as an Instancing Vertex emitter, and has the Build modifier on it. Such a setup is a workaround/technique for being able to art-direct a semi-random layout of a collection of objects (e.g. leaves/balls forming a carpet). This can be preferable to particles e.g. due to undesirable distribution of items leaving random gaps and overlapping in other places.

---

## Build Modifier¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modifiers/generate/build.html

**Contents:**
- Build Modifier¶
- Options¶
  - Custom Range¶
  - Fade¶
  - Influence Filters¶

The Build modifier make strokes appear or disappear in a frame range to create the effect of animating lines being drawn or erased.

This documentation refers to the Build Modifier specific to the Grease Pencil object. For uses with other object types refer to the general Build Modifier.

Determines how many strokes are being animated at a time.

Strokes appear/disappear one after the other, but only a single one changes at a time.

Multiple stroke appear/disappear at a time.

Builds only the strokes that are new compared to last keyframe. The assumption is Additive Drawing was used so that the shared strokes are the same.

Determines the animation type to build the strokes.

Shows points in the order they occur in each stroke, from first to last stroke. (Simulating lines being drawn.)

Hide points from the end of each stroke to the start, from last to first stroke. (Simulating lines being erased.)

Hide points in the order they occur in each stroke, from first to last stroke. (Simulating ink fading or vanishing after getting drawn.)

The way you want to time the building of the strokes.

Use the recorded speed of the stylus when the strokes were drawn. Only available in Sequential and Additive Mode.

The recorded speed is multiplied by this value.

The maximum gap between strokes in seconds.

Set a fixed maximum number of frames for the build animation. (Unless another Grease Pencil keyframe occurs before this time has elapsed.)

The maximum number of frames used.

Number of frames after each Grease Pencil keyframe before the modifier has any effects.

Manually set a percentage factor to control the amount of the strokes that are visible.

The factor from 0 to 1.

Only available in Concurrent Mode.

All stroke start at the same time (i.e. shorter strokes finish earlier).

All stroke end at the same time (i.e. shorter strokes start later).

Use the distance to an object to define the order in which strokes appear.

If enabled, only modify strokes during the specified frame range.

Determines the start and end frame for the build effect.

Defines how much the stroke is fading in/out.

How much strength fading is applied to the stroke’s thickness.

How much strength fading applies to the stroke’s opacity.

Assign a weight value to points that have started/finished the fade.

See Influence Filters.

---

## Buttons¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/buttons/buttons.html

**Contents:**
- Buttons¶
- Operator Buttons¶
- Checkboxes & Toggle Buttons¶
  - Dragging¶
- Direction Buttons¶
  - Shortcuts¶

Operator buttons execute an Operator which in summary execute an action when clicked with LMB. Operator buttons may be an icon, text, or text with an icon.

Checkboxes and Toggle buttons.¶

These controls are used to activate or deactivate options. Use LMB to change their state. A tick is shown on checkboxes when the option is activated. Active status on toggle buttons is indicated either by color on the icon background, or a change in icon graphics.

Use Ctrl-Wheel to cycle through on/off states.

To change many values at once on or off, you can press down LMB and drag over multiple buttons.

Clicking with LMB in the sphere and dragging the mouse cursor lets the user change the direction by rotating the sphere.

LMB (drag) rotates the direction.

Ctrl (while dragging) snaps to vertical & diagonal directions.

---

## Cache¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/domain/cache.html

**Contents:**
- Cache¶
- Volumetric Data¶

Physics ‣ Fluid ‣ Cache

The Cache panel is used to Bake the fluid simulation and stores the outcome of a simulation so it does not need to be recalculated.

Baking takes a lot of compute power (hence time). Depending on the scene, it is recommended to allocate enough time for the baking process.

If the mesh has modifiers, the rendering settings are used for exporting the mesh to the fluid solver. Depending on the setting, calculation times and memory use might exponentially increase. For example, when using a moving mesh with Subdivision Surface as an obstacle, it might help to decrease simulation time by switching it off, or to a low subdivision level. When the setup/rig is correct, you can always increase settings to yield a more realistic result.

Fluid simulations use their own cache. All other physics simulations make use of the General Baking operators.

Directory to store baked simulation files in. Inside this directory each simulation type (i.e. mesh, particles, noise) will have its own directory containing the simulation data.

The simulation starts on this frame, and this is the first one that is baked.

The simulation ends on this frame, and this is the last one to be baked.

The simulation is only calculated for positive frames between the Start and End frames of the Cache panel. So if you want a simulation that is longer than the default frame range you have to change the End frame.

Frame offset that is used when loading the simulation from the cache. It is not considered when baking the simulation, only when loading it.

The type of the cache determines how the cache can be baked.

The cache will be baked as the simulation is being played in the viewport.

The cache will be baked step by step: The bake operators for this type are spread across various panels within the domain settings (e.g. the bake tool for the mesh can be found in the Mesh panel).

The cache will be baked with a single tool. All selected settings will be considered during this bake. The bake tool for this type can be found in the Cache panel.

“Replay” only works when the Playback Sync mode is set to “Play Every Frame”. If you need to use “Frame Dropping” or “Sync to Audio”, consider using the “Modular” or “All” options below.

Extra data will be saved so that you can resumed baking after pausing. Since more data will be written to drive it is recommended to avoid enabling this option when baking at high resolutions.

This option is only available when using the Final cache type. Bake All will run the simulation considering all parameters from the settings (i.e. it will bake all steps that can be baked individually with the Modular cache type at once).

The progress will be displayed in the status bar. Pressing Esc will abort the simulation.

Once the simulation has been baked, the cache can be deleted by pressing Free All. It is not possible to pause or resume a Bake All process as only the most essential cache files are stored on drive.

File format for volume based simulation data (i.e. grids and particles).

Blender’s own caching format with some compression. Each simulation object is stored in its own .uni cache file.

Advanced and efficient storage format. All simulation objects (i.e. grids and particles) are stored in a single .vdb file per frame.

Compression method that is used when writing OpenVDB cache files.

Cache files will be written with Zip compression. Effective but slower than Blosc.

Cache files will be written with Blosc compression. Multithreaded compression, similar in size and quality to Zip compression.

Cache files will be written without any compression.

Precision level that is used when writing OpenVDB cache files.

Volumetric data (e.g. grids, particles) will be written with full precision (32-bit).

Volumetric data (e.g. grids, particles) will be written with half precision (16-bit).

Volumetric data (e.g. grids, particles) will be written with mini float precision (8-bit) where possible. For cache data where this is not possible, 16-bit floats will be used instead.

File format for the mesh cache files.

Binary Object: Mesh data files with some compression. Object: Simple, standard data format for mesh data.

Export the simulation as a standalone Mantaflow script when baking the scene (exported on “Bake Data”). Usually, only developers and advanced users who know how to use the Mantaflow GUI will make use of this functionality. Use a Debug Value of 3001 to enable.

---

## Circle Tool¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/circle.html

**Contents:**
- Circle Tool¶
- Tool Settings¶
  - Brush Asset¶
  - Brush Settings¶
  - Color¶
- Usage¶
  - Selecting a Brush and Material¶
  - Creating Circles¶

The Circle tool create oval shapes using any of the Draw type brushes.

You can configure the brush main settings exposed on the Tool Settings for convenience. For the draw brushes configuration and settings see: Draw Brush.

The number of stroke points between each stroke edge.

Use a curve widget to define the stroke thickness from the start (left) to end (right) of the stroke.

When enabled, the stroke use a curve profile to control the thickness along the line.

Picks the brush asset used by the tool.

See Brush Asset for more information.

See Draw Brushes for a detailed list of all draw brushes and their options.

Parameters to control to look of the stroke.

See Draw Brushes for details.

Settings to determine the color of strokes.

In the Tool Settings select the brush, material and color type to use with the tool. The Circle tool uses Draw Brush types. See Brush Settings for more information.

Click (LMB or the Pen tip) and drag the start point.

Release on the desired end point.

After releasing you can move the start and end point by clicking and dragging on the yellow manipulators.

Then confirm (Return/MMB) or cancel (Esc/RMB).

While dragging you can use Shift to make a perfect circle or use Alt to create the circle from a center point.

NumpadPlus and NumpadMinus or using the mouse Wheel will increase or decrease the amount of points in the final circle.

F will adjust the line thickness and Shift-F will adjust the opacity of the strokes.

Click and dragging the start point.¶

Moving start and end points with manipulators.¶

The circle after confirming.¶

---

## Closure¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/types/utilities/closure/closure.html

**Contents:**
- Closure¶
- Inputs¶
- Properties¶
  - Input Items¶
  - Output Items¶
- Outputs¶
- Usage¶
  - Using External Values¶
  - Example¶

The Closure node defines a zone that encapsulates a reusable section of nodes behaving like a function. It specifies inputs, outputs, and internal logic that can be executed elsewhere in the node tree using an Evaluate Closure node.

Closures allow users to pass custom procedural logic into node groups, making tools more modular and adaptable. Instead of duplicating or editing an existing group, a closure can expose user-defined behavior while preserving the structure of the main system.

An empty closure zone.¶

Closures define their own inputs, which act as parameters for the internal node logic. These inputs can be created by dragging the blank input socket into another socket or by adding sockets manually in the node’s properties. Each input defines a parameter that the closure can receive when it is evaluated elsewhere.

The Closure node does not have functional properties of its own, but its interface is configurable through the Node tab in the Sidebar. Inputs and outputs can be added, removed, and renamed to define the closure’s signature.

Updates the current node to match the socket signature of the connected nodes. Use this after renaming, adding, or removing sockets.

Marks the current zone as the source of a closure signature that other nodes can reference. This ensures consistent input and output definitions across multiple closure instances.

Displays one entry per socket defined in the closure. Double-click an entry to rename it.

Add a new input socket to the closure.

Delete the selected input socket.

Defines the data type for the selected socket (e.g. Float, Vector, Geometry, Object, Bundle). For value types, a default value control appears and is used when the socket is unlinked.

Defines the data structure supported by the input socket, such as a Single value, Field, or Grid. The shape determines how the data is evaluated and passed through the node network. See Socket Shape for more information.

Available when the closure’s output zone is selected.

Displays one entry per socket defined in the closure output. Double-click to rename.

Add a new output socket to the closure.

Delete the selected output socket.

Defines the data type for the selected socket (e.g. Float, Vector, Geometry, Object, Bundle). For value types, a default value control appears and is used when the socket is unlinked.

Defines the data structure supported by the input socket, such as a Single value, Field, or Grid. The shape determines how the data is evaluated and passed through the node network. See Socket Shape for more information.

Closures define outputs that return values to the node tree in which they are evaluated. Outputs can be created by dragging a socket from within the zone into the blank socket on the closure’s output, or by adding sockets manually in the node’s properties.

Closures define reusable logic that can be injected into another node tree. They are commonly used in procedural systems where part of the behavior should remain user-defined.

Typical use cases include:

Defining a custom scattering rule for a terrain generator.

Describing how to distribute or modify instances procedurally.

Providing adjustable mappings, field evaluations, or transformation logic.

Closures can capture values from outside their zone. A captured value is stored as part of the closure definition and remains available even when the closure is evaluated in a different context.

Captured values make it possible to preserve external parameters—such as scale, density, or color—without creating explicit input sockets. This makes closures cleaner and easier to reuse in different node trees.

Capturing an external input value inside a closure.¶

In a terrain generator node group, replace the tree distribution logic with an Evaluate Closure node.

Expose the closure input on the group’s interface.

In the main node tree, create a Closure Zone and connect it to that input.

Inside the closure zone, define the desired tree placement logic.

When the generator evaluates the closure, the custom distribution defined in the zone is executed instead of the default behavior.

A Closure Zone defining a custom distribution pattern for tree scattering.¶

---

## Cloth Filter¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/cloth_filter.html

**Contents:**
- Cloth Filter¶
- Tool Settings¶

Toolbar ‣ Cloth Filter

This tool works similar to the Cloth Brush, however, it applies a cloth simulation to all vertices in the mesh at the same time. Click and drag away from the object for a positive effect and towards for a negative effect.

Vertices can be “pinned” by masking vertices that should remain stationary, or by using Face Sets.

Operation that is going to be applied to the mesh.

Applies gravity to the simulation.

Expands the cloth’s dimensions.

Pinches the cloth to the point where the cursor was when the filter started.

Scales the mesh as a Soft Body using the distance to the origin of the object as scale. This creates filter produces folds in the surface. The orientation of the folds can be controlled using the Force Axis and Orientation.

The amount of effect the filter has on the mesh.

Apply the force along the selected axis.

Orientation of the axis to limit the filter force.

Use the local axis to limit the force and set the gravity direction.

Use the world axis to limit the force and set the gravity direction.

Use the view axis to limit the force and set the gravity direction.

Mass of each simulation particle.

How much the applied forces are propagated through the cloth.

Only applies the cloth forces to the vertices assigned to the Face Set that are under the mouse.

Enables the detection of collisions with other objects during the simulation. In order for the sculpt object to collide with object, the collision object must have Collision Physics activated.

---

## Clump Hair Curves¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/hair/guides/clump_hair_curves.html

**Contents:**
- Clump Hair Curves¶
- Inputs¶
  - Guide Map¶
- Outputs¶
  - Guide Map¶

The Clump Hair Curves node gathers nearby hair curves together around designated guide curves, creating clump formations commonly seen in real hair, fur, and grass. It is a key step in grooming workflows for adding realism and structure by simulating how strands naturally group due to moisture, product, or physical interaction.

The input geometry containing the hair curves to be clumped.

Controls the overall strength of the clumping effect. A value of 0.0 applies no clumping, while 1.0 fully pulls curves toward their guides.

Defines how the clumping influence changes along the length of each curve. A value of 0.0 applies a constant strength, while 0.5 results in a linear falloff from root to tip.

Adds random variation to the positions of curve tips, preventing perfect convergence and helping clumps look more natural.

Applies a random directional offset to entire clumps, introducing subtle variation between groups.

Defines how the influence of each guide curve decreases with distance. A value of 0.0 disables distance-based falloff, making all nearby curves equally affected.

Sets the maximum distance from a guide at which clumping has an effect. Curves farther than this threshold will not be influenced by that guide.

Controls the randomization used for offsets and variation. Changing this value alters the random distribution of clumping while keeping the same parameters.

When enabled, maintains the original length of each curve during deformation. When disabled, curves may stretch or shrink slightly as they are pulled toward guides.

A map that specifies which guide curve acts as the center for each clump. If provided, this takes priority over any existing guide_curve_index attribute, and the Guide Distance and Guide Mask inputs are ignored.

The minimum distance between selected guide curves when generating a new guide map. Larger values produce fewer, larger clumps.

Defines which curves can be used as guides during automatic guide map creation.

When enabled, uses the existing guide map attribute if it is already available. If disabled and Guide Index is not provided, a new guide map is generated using Guide Distance and Guide Mask. Creating the guide map separately allows for finer control over guide placement and grouping.

The resulting geometry with clumped hair curves.

The guide index map used for this operation. If a new guide map was generated by this node, it is stored and provided through this output for reuse in subsequent operations.

---

## Collections¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/domain/collections.html

**Contents:**
- Collections¶

Properties ‣ Physics ‣ Fluid ‣ Collections

If set, only objects in the specified Collection will be allowed to act as Flow objects in this domain.

If set, only objects in the specified Collection will be allowed to act as Effector objects in this domain.

---

## Color Filter¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/color_filter.html

**Contents:**
- Color Filter¶
- Tool Settings¶

Toolbar ‣ Color Filter

Apply color corrections or effects on the active color attribute on all vertices in the mesh at the same time.

To use this tool, click and drag away from left to right or from right to left for a negative effect.

Fills in a single color.

Shifts the Hue of each color.

Increases or decreases the saturation.

Increases or decreases the values.

Increases or decreases the brightness.

Increases or decreases the contrast.

Blurs or sharpens the colors.

Increases or decreases the red channel.

Increases or decreases the green channel.

Increases or decreases the blue channel.

Set a color that will be used for the fill filter type.

The amount of effect the filter has on the color attribute.

---

## Color Palette¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/templates/color_palette.html

**Contents:**
- Color Palette¶
- Shortcuts¶

Color Palettes are a way of storing a brush’s color so that it can be used at a later time. This is useful when working with several colors at once.

A Data-Block Menu to select a palette.

Adds the current brush’s primary Color to the palette.

Removes the currently selected color from the palette.

Moves the selected color up/down one position.

Sort Colors by Hue, Saturation, Value, Luminance.

Each color that belongs to the palette is presented in a list. Clicking on a color will change the brush’s primary Color to that color.

Ctrl-LMB open the color picker to change color. See Color Picker.

Backspace reset the value.

---

## Color Picker¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/templates/color_picker.html

**Contents:**
- Color Picker¶
- Interface¶
- Shortcuts¶
- Types¶
- Notes¶

Circle HSV color picker.¶

The Color Picker is a pop-up control that allows you to define and adjust color values. It appears when editing any color property in Blender, such as materials, lights, brushes, or interface themes.

The color picker provides multiple color models and interaction modes to suit different workflows, and can display or edit colors in both linear and perceptual (display-referred) color spaces.

The large color field lets you pick two color components at once, depending on the selected picker type. The third component (such as value or saturation) is controlled with a slider next to the color field.

The picker’s appearance and behavior depend on the type chosen in the Preferences; see Types below.

The vertical slider with a gradient background defines the brightness or lightness of the selected color. You can scroll the Wheel for fine adjustments or click and drag the handle.

Below the color picking widget are a few options, the first affects how the color component’s values are computed.

Displays color component values in the scene’s linear working color space used internally for rendering and compositing.

Displays color component values in the color picking space (sRGB by default), which matches the visual appearance of the color widgets and is more intuitive for user selection.

The next set of options change the Color Model that is used. The available options depend on the Color Picker Type.

Defines a color by directly mixing Red, Green, and Blue components.

Defines a color by adjusting Hue, Saturation, and Value (or Lightness). Useful for adjusting color tone and intensity independently.

The numeric fields below the picker show the component values (RGB or HSV/HSL). Blender expresses these in the range 0.0 to 1.0. For color inputs that include an Alpha Channel, an additional slider and field are shown.

Displays or accepts the color’s hexadecimal (hex) representation. Hex shorthand notation can be used (for example, FC0 for FFCC00).

Hex values are automatically Gamma-corrected for the sRGB Color Space. For more information, see Color Management.

Samples a color from anywhere inside the Blender window using the Eyedropper.

The sampled colors are read in linear color space, so they do not account for display transformations such as view or exposure adjustments. Sampling colors from overlays, reference images, or video preview regions may be inaccurate since those may be drawn after color management transforms.

Ctrl-LMB (drag): Snap hue to 30° intervals.

Shift-LMB (drag): Fine-tune color movement for precise adjustments.

Wheel: Adjust value or lightness.

Backspace: Reset the current value to its default.

The Color Picker Type determines how colors are visualized and selected. Different picker types offer alternative layouts for adjusting hue, saturation, and value components. The choice is a matter of personal preference and workflow.

You can choose the default picker type in the Preferences under Interface Preferences.

Blender internally works in linear color space; conversions from sRGB or other spaces happen automatically.

The color picker displays the color as it appears in the current view transform, but the stored value remains linear.

For consistent results across renders and display devices, see Color Management.

---

## Color Ramp Widget¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/templates/color_ramp.html

**Contents:**
- Color Ramp Widget¶
- Controls¶
  - Shortcuts¶

Color Ramps specify a color gradient based on color stops. Each stop has a position and a color. The gradient is then calculated as the interpolation between these stops using the chosen interpolation method.

Adds a new stop between the selected stop and the one before it.

Deletes the selected color stop.

Contains more operators for the color ramp.

Flips the gradient, mirroring the positions of the stops.

Distribute the stops so that every step has the same space to the right. This is mostly useful when used with Constant interpolation mode.

Distribute the stops so that all neighbors have the same space between them.

An Eyedropper to sample a color or gradient from the interface to be used in the color ramp.

Resets the color ramp to its default state.

Selection of the Color Model used for interpolation.

Blends color by mixing each color channel and combining.

Blends colors by first converting to HSV or HSL, mixing, then combining again. This has the advantage of maintaining saturation between different hues, where RGB would de-saturate. This allows for a richer gradient.

The interpolation method to use across the ramp.

Uses a B-spline interpolation for the color stops.

Uses a cardinal interpolation for the color stops.

Uses a linear interpolation for the color stops.

Uses an ease interpolation for the color stops.

Uses a constant interpolation for the color stops.

Clockwise interpolation around the HSV/HSL wheel.

Counterclockwise around the HSV/HSL wheel.

Nearest route around the wheel.

Furthest route around the wheel.

HSV and HSL interpolation options.¶

Index of the active color stop (shown as a dashed line). Offers an alternative way of selecting a stop in case it’s so close to others that it’s hard to select it directly.

This slider controls the position of the selected color stop in the range.

A color field where you can specify the color and alpha of the selected stop.

LMB (drag) moves color stops.

Ctrl-LMB (click) adds a new color stop.

---

## Combine Bundle Node¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/types/utilities/bundles/combine_bundle.html

**Contents:**
- Combine Bundle Node¶
- Inputs¶
- Properties¶
  - Bundle Items¶
- Outputs¶

The Combine Bundle node creates a new Bundle from multiple input values. Each input becomes an element of the bundle, identified by its socket name. Values can be accessed in other parts of the node tree using the Separate Bundle

The node can contain an arbitrary number of input sockets. Each socket can be given a custom name and type. Supported types include (but not limited to):

Values (e.g. float, integer, boolean, vector, color)

Properties are available in the Node tab of the Sidebar.

Updates the current node to match the socket signature of the connected nodes. Use this after renaming, adding, or removing sockets.

Locks the current item list and types to stabilize interfaces when publishing node groups. When enabled, adding/removing items is disabled until the option is turned off.

Displays one entry per element in the bundle. Double-click to rename.

Add a new socket to the bundle.

Delete the selected socket.

The data type for the selected item (e.g. Float, Vector, Geometry, Object, Bundle). For value types, a default value control is shown and used when the socket is unlinked.

The resulting bundle containing all defined inputs.

---

## Common¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/interface/common.html

**Contents:**
- Common¶
- Target¶
- Space¶
  - Space Types¶
- Influence¶

The Target is the object which the constraint should refer to. For example, the Copy Location Constraint copies the location of the target object to the constrained object.

Initially, the Target is empty and the constraint’s icon is red, indicating it’s inactive:

Once a target is selected, the icon will turn gray and the constraint will start working.

By default, the constraint uses the location of the target’s Origin, but if the target is a Mesh or Lattice, it’s possible to change this by selecting a Vertex Group. The constraint will then use the weighted average of the target’s vertex positions.

Alternatively, if the target is an Armature, it’s possible to select a Bone and choose an interpolated position between its Head and Tail. The button enables following the curved shape of Bendy Bones.

The Target Space is the reference frame for retrieving the location coordinates, rotation angles, and scale factors of the Target. The Owner Space is the reference frame for applying those numbers to the object or bone that owns the constraint.

Using World Space for both Target and Owner places the constrained object at the same location as the target regardless of their parents.¶

Use the transformation relative to the world axes.

Use the transformation relative to an arbitrary object or bone.

Use the transformation relative to the armature object.

For an object, use the transformation relative to its parent.

For a bone, use the transformation relative to its rest state, after that rest state was transformed by the bone’s ancestors. (If the bone has no other constraints, this is its transformation as shown in the Properties Editor while in Pose Mode.)

For objects without a parent, Local Space has a special meaning that’s kept for backwards compatibility. This behavior may be removed in the future and shouldn’t be relied on; use World Space instead.

Use the transformation relative to the bone’s rest state. Unlike Local Space, this includes the rotation and location difference caused by rotating any ancestor bone.

This space is intended to be used with the Owner set to Local Space. It retrieves the Local Space of the Target bone, adjusted to work with the rest orientation of the Owner bone. The result is that, if the parent bones of both the Target and the Owner are in their rest pose, the Owner will undergo the same transformation as the Target in armature space. The following image demonstrates this:

The left hand armature contains the Target bone which we rotate manually.

The middle armature has a constraint that copies the Local Space rotation of the Target bone. If the Target bone is rotated around its Y axis, this Owner bone rotates by the same amount around its own Y axis.

The right hand armature has a constraint that copies the Local Space (Owner Orientation) rotation of the Target bone. If the Target bone is rotated around its Y axis, the Owner bone rotates around that same axis in armature space. Initially this is the same as using Pose Space or even World Space, but if the parent bones are rotated as well, the result will be different.

The Influence is a strength multiplier for the constraint.

By default, it’s 1, meaning that (for example) a Copy Location constraint fully overrides the object’s original location.

Setting it to 0 is the same as disabling or even deleting the constraint.

Setting it between 0 and 1 will give an interpolated result. For example, a value of 0.5 would place the object halfway between its previous location and the location of the Target.

The Influence can be keyframed, meaning constraints can be turned on and off over the course of an animation.

Applies the result of the constraint to the object’s/bone’s own transformation, but instead of deleting the constraint, disables it by setting the Influence to 0. As with applying, this may not work perfectly if the constraint is not the first in the stack.

---

## Common Nodes¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/types/index.html

**Contents:**
- Common Nodes¶

These nodes are shared across different node tree types.

---

## Common Settings¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/curves_sculpting/tools_settings.html

**Contents:**
- Common Settings¶
- Brush¶
- Stroke¶
- Falloff¶
- Cursor¶

Information on brush settings for every mode can be found in these pages:

See general and advanced Brush here.

See the global brush settings for Stroke settings.

See the global brush settings for Falloff settings.

See the global brush settings for Cursor settings.

---

## Controls¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/controls.html

**Contents:**
- Controls¶
- Auto-Masking¶

Header ‣ Auto-Masking

These properties automatically mask geometry based on geometric features of the mesh. It’s an quick alternative to frequent manual masking. These masks are initialized on every new stroke or tool usage. They are also never visible as an overlay.

Note, these properties are applied across all sculpt brushes, however, they can also be configured per brush in the Advanced Brush Settings.

These properties can be accessed via a Pie Menus by pressing Alt-A.

All auto-masking modes can be combined, which makes the generated auto-mask more specific. For example it’s possible to auto-mask a specific face set, while excluding disconnected topology and face set boundaries, and only affect faces that are oriented towards the view via View Normal.

Only vertices that are topologically connected to where you started the stroke/tool on are affected. So loose geometry islands will be auto-masked.

Additionally for the Grab and Thumb brushes, anything that is not connected within the brush radius will be auto-masked. So even if geometry is connected somewhere, it is considered separate if the connection is not within the radius.

Only vertices that are part of the same face set that you started the stroke/tool on are affected.

If no topology or face set is visible under the cursor at the start of the stroke, the previously auto-masked area will be targeted. This is especially useful with the “Projected” falloff shape in the Falloff Settings.

Vertices that are part of open boundary edges are not affected. This also includes boundary edges to hidden faces.

Increases the soft gradient towards the auto-masked boundary edges. Each step iterates the distance one edge further. This setting is used for both Mesh Boundary and Face Sets Boundary.

This will execute the Mask From Mesh Boundary operator with the current auto-masking settings. This is very useful to visualize the current auto-mask, or to edit the mask further manually.

Vertices that are part of a boundary between face sets are not affected. This also includes boundary edges to hidden faces. Propagation Steps are shared with Mesh Boundary auto-masking.

This will execute the Mask From Face Sets Boundary operator with the current auto-masking settings. This is very useful to visualize the current auto-mask, or to edit the mask further manually.

Vertices that are the peaks of the surface curvature are not affected. While this auto-mask is primarily meant for painting, it can also be used for regular sculpting.

The overall contrast of how strong the cavity is applied. The value of 0.5 is the default, but better results can also be achieved on 0.2 if a Custom Curve is used as well.

The number of times the cavity mask is blurred. A value of 0 will give the pure cavity auto-mask. Anything higher than 6 will likely have a less visible effect and decrease performance. Even though the value is capped to 10, it can be increased up to 25 if typing in the value.

Use a custom curve to fine tweak the cavity auto-mask. This is very useful if only small crevices or flat surfaces should be affected. Or for example if the contrast should be increased/decreased in a specific way.

This will execute the Mask From Cavity operator with the current auto-masking settings. This is very useful to visualize the current auto-mask, or to edit the mask further manually.

This is the same as “Cavity”, but inverted. This means the valleys/crevices of the surface curvature will not be affected. It cannot be used at the same time as Cavity and shares all of its settings. Enable this to quickly invert the cavity auto-mask.

Only vertices with a Normal that face the viewer are affected. This is similar to the “Front Faces Only” toggle in the Brush Setting, to only affect visible geometry. The advantage of this auto-mask is that it has more options and works on sculpt mode as a whole.

Change the View Normal behavior to only affect vertices that are not occluded by other faces. This setting is incompatible with the other Limit and Falloff sliders. It also causes a much slower performance.

Determines the range of angles that will be affected. 90 degrees encompasses all that is visible.

Extends the angular range of the Limit slider with a soft falloff gradient. This falloff will visually extend the limit range further.

Very similar to the View Normal, but uses the Normal of the surface that you started the stroke/tool on. This way any direction can be chosen for what vertices will be affected. It has the same Limit and Falloff sliders as the View Normal auto-mask.

---

## Create Guide Index Map¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/hair/guides/create_guide_index_map.html

**Contents:**
- Create Guide Index Map¶
- Inputs¶
- Outputs¶

The Create Guide Index Map node generates an integer attribute named guide_curve_index that maps every hair curve to its nearest guide curve. Each non-guide curve is assigned the index of the guide curve it should follow.

This guide map is used by other hair grooming nodes (for example, Braid Hair Curves, Clump Hair Curves) to organize curves into logical groups around shared guides and apply effects consistently.

Other nodes in the Hair Guides Nodes category can generate a guide map internally for convenience, but the resulting attribute is equivalent to what this node produces.

The input geometry containing the hair curves to be grouped and, optionally, existing guide curves.

The curves or points that can act as guides. These are the candidates that other curves will be assigned to.

The minimum spacing between chosen guides. This prevents guides from being selected too close together and helps control how large each guide’s influence region will be.

A mask that restricts which curves are allowed to become guides. Curves with a mask value of 0 cannot be selected as guides.

An ID used to divide the curves into independent groups for guide assignment. A curve will only select a guide that has the same Group ID value. This is useful for ensuring that different regions (for example, left vs. right side of a groom) do not mix.

The input geometry with two additions:

A guide_curve_index attribute that stores, for every curve, the index of its assigned guide curve.

A anonymous attribute representing the guide selection. The resulting geometry still contains both normal curves and the chosen guide curves.

A geometry output that includes only the curves selected as guides.

An integer attribute giving, for each curve, the index of the closest guide curve with the same Group ID.

A boolean selection attribute that is true only for curves that were chosen as guides. This can be used to isolate, visualize, or further process the guide curves.

---

## Curl Hair Curves¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/hair/guides/curl_hair_curves.html

**Contents:**
- Curl Hair Curves¶
- Inputs¶
  - Guide Map¶
- Outputs¶
  - Guide Map¶

The Curl Hair Curves node deforms existing hair curves into curls by wrapping them around nearby guide curves. It is useful for creating coiled, spiral, or wavy hair patterns and for adding stylized variation or realism to a groom. The curls can vary in radius, frequency, and start position, with optional random offsets for natural variation.

The input geometry containing the hair curves to deform into curls.

Controls the overall strength of the curling effect. A value of 0.0 disables the effect, while 1.0 applies the full curl deformation.

The number of subdivisions applied to curves before deformation. Higher values produce smoother curls but increase processing time.

Defines the percentage along each curve (from root to tip) at which the curl effect begins. This allows keeping part of the strand straight before the curl starts.

The overall radius of the curls. Larger values produce looser curls, while smaller values create tighter spirals.

Multiplies the curl radius near the start of the curl region, allowing tapering or gradual buildup of curl tightness.

Multiplies the curl radius near the end of the curve, controlling how curls taper off or unwind toward the tip.

Controls how many full rotations occur along the length of the curve. Higher values produce more frequent curls. This input can vary per point along the curve, allowing complex wave patterns.

Adds random variation to the curl phase or starting angle per curve, creating a more natural, less uniform look.

Sets the random seed used for generating the random offsets. Changing this value produces different curl variations while maintaining the same parameters.

A map that specifies which curve should act as the guide or central reference for each group of curled curves. If provided, this overrides any existing guide_curve_index attribute, and the Guide Distance and Guide Mask inputs are ignored.

The minimum spacing between selected guides when generating a new guide map. Larger values result in fewer guide curves and broader curl groups.

A mask that determines which curves are eligible to be used as guides.

When enabled, uses the existing guide map attribute if one is already present. If disabled and Guide Index is not provided, a new guide map is created using Guide Distance and Guide Mask. Creating the guide map separately allows for more control and consistency across multiple grooming operations.

The resulting geometry with curled hair curves.

The guide index map used for the operation. If this node created a new guide map, it is stored and output here for use in subsequent nodes.

---

## Curve Pen¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/curves_new/tools/pen.html

**Contents:**
- Curve Pen¶
- Usage¶
- Hotkeys¶
- Tool Settings¶

The Curve Pen tool allows you to construct and edit curves rapidly.

LMB click to add a new point connected to the currently selected point. The new point will have handle type of Vector. Shift-LMB click will add point as type Auto. However, the handle type switches to Align when handles are moved (See Move Point).

Ctrl-LMB click on an existing point to delete it.

Ctrl-LMB click on a Curve Segment to insert a new control point between the two adjacent control points. Ctrl-LMB click and drag to control the handles of the inserted points.

LMB drag on a segment in between two control points to adjust the handles, changing the shape of the curve without affecting the location of any control points.

LMB click to select a single point or handle at a time.

LMB drag to move existing points or handles. With an endpoint of a stroke selected, click and drag on empty space to Extrude Point and move the handle at the same time.

Make the stroke Cyclic by clicking the endpoints.

Double LMB click on the control point to cycle through all handle types.

Hold LeftCtrl while dragging a handle to switch between Free and Align handle types. Can be used to create sharp corners along the curve.

Hold LeftAlt while dragging a handle to move the entire point.

Hold LeftShift while dragging a handle to limit the movement of the handle to multiples 45 degrees, so the handle can only be vertical, horizontal or diagonal.

Control newly added point’s radius.

---

## Curve Pen¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/curves/tools/pen.html

**Contents:**
- Curve Pen¶
- Usage¶
- Hotkeys¶

The Curve Pen tool allows you to construct and edit curves rapidly.

Curve Pen Preferences¶

The following preferences can be configured from: Preferences ‣ Keymap ‣ 3D View ‣ Curve ‣ 3D View Tool: Edit Curve, Curve Pen.

LMB click to add a new point connected to an existing point.

The handle type of the extruded points. Can be either Vector or Auto. However, the handle type switches to Align when handles are moved (See Move Point).

Ctrl-LMB click on an existing point to delete it.

Ctrl-LMB click on a Curve Segment to insert a new control point between the two adjacent control points. Ctrl-LMB click and drag to control the handles of the inserted points.

LMB drag on a segment in between two control points to adjust the handles, changing the shape of the curve without affecting the location of any control points.

LMB click to select a single point or handle at a time.

LMB drag to move existing points or handles. With an endpoint of a spline selected, click and drag on empty space to Extrude Point and move the handle at the same time.

Make the spline Cyclic by clicking the endpoints consecutively.

The condition for Close Spline to activate.

Turn off the Close Spline functionality.

Close the spline on mouse down. With this option, you may click and drag to adjust the handles of the endpoint.

Activate on mouse release. With this option, the Close Spline functionality will not be triggered on click and drag.

Double LMB click on a handle to switch handle between Vector and Auto handle types. Can be used to easily switch between sharp corners and smooth curves.

Double LMB click on the control point to cycle through all handle types.

Hold LeftShift while dragging a handle to switch between Free and Align handle types. Can be used to create sharp corners along the curve.

Hold LeftCtrl while dragging a handle to move the closer handle of the adjacent control point. Can be helpful to make adjustments to newly created curve segments.

Hold Spacebar while dragging a handle to move the entire point.

Press RightCtrl while dragging a handle to mirror its movement on the opposite handle of the same point.

Hold LeftAlt while dragging a handle to limit the movement of the handle to its current direction, so only its length can be adjusted.

---

## Curve Tool¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/curve.html

**Contents:**
- Curve Tool¶
- Tool Settings¶
  - Brush Asset¶
  - Brush Settings¶
  - Color¶
- Usage¶
  - Selecting a Brush and Material¶
  - Creating Curves¶
  - Extruding¶

The Curve tool create complex Bézier style curves using any of the Draw type brushes..

You can configure the brush main settings exposed on the Tool Settings for convenience. For the draw brushes configuration and settings see: Draw Brush.

The number of stroke points between each stroke edge.

Use a curve widget to define the stroke thickness from the start (left) to end (right) of the stroke.

When enabled, the stroke use a curve profile to control the thickness along the curve.

Picks the brush asset used by the tool.

See Brush Asset for more information.

See Draw Brushes for a detailed list of all draw brushes and their options.

Parameters to control to look of the stroke.

See Draw Brushes for details.

Settings to determine the color of strokes.

In the Tool Settings select the brush, material and color type to use with the tool. The Curve tool uses Draw Brush types. See Brush Settings for more information.

Click (LMB or the Pen tip) and drag the start point.

Release on the desired end point.

After releasing you can tweak the curve using two cyan Bézier like manipulators.

Then confirm (Return/MMB) or cancel (Esc/RMB).

While dragging you can hold Shift to use only one manipulator to tweak the curve (like the Arc tool), use Alt to create the arc from a center point.

NumpadPlus and NumpadMinus or using the mouse Wheel will increase or decrease the amount of points in the final curve.

F will adjust the line thickness and Shift-F will adjust the opacity of the strokes.

click and dragging the start point.¶

Tweaking curve with the manipulators.¶

The curve after confirming.¶

Before confirming you can use E to extrude the end point of the curve to generate multiple connected curves.

End point extruding.¶

Tweaking the last curve with the manipulators.¶

The connected curves after confirming.¶

---

## Curve Widget¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/templates/curve.html

**Contents:**
- Curve Widget¶
- Control Points¶
- Controls¶

This widget is used to edit two types of curves:

Profile curves that simply describe a two-dimensional shape.

Mapping curves that map an input value on the X axis to an output value on the Y axis.

The available options are slightly different depending on this type. Also, unlike profile curves, mapping curves can’t have overhang: each X value must correspond to exactly one Y value.

Like all curves in Blender, the curve in this widget is defined using control points.

Click LMB anywhere on the curve where there is not already a control point.

Drag the point with LMB.

Select the point and click the button at the bottom right. Alternatively, press X.

Zoom in to show more details and provide more accurate control. To navigate around the curve while zoomed in, click and drag with LMB in an empty area.

Zoom out to show fewer details and view the curve as a whole. You cannot zoom out further than the clipping region (see Clipping below).

Mirror the curve around the diagonal.

Force curve points to stay between the specified values.

Set the minimum and maximum bounds of the curve points.

Zoom the view all the way out.

Controls how the curve is extended before the first point and after the last point.

Causes the curve to “go flat.”

Causes the curve to maintain its direction.

Extend Extrapolated.¶

Resets the curve to the default (removes all added points).

The handle type of the selected control point. This determines the shape of the curve segments around it.

Results in a smooth curve without the need to manually set up handles.

Results in straight lines and a sharp corner.

Shows freely movable Bézier handles that are independent of each other. This can result in a sharp corner at the control point.

Shows freely movable Bézier handles that are locked together to always point in opposite directions. This ensures the curve is always smooth at the control point.

Like Auto Handle, but also prevents overshoot.

Auto Clamped Handles.¶

The coordinates of the selected control point.

Remove the selected control point. The first and last points cannot be deleted.

The whole curve can be copied from one Curve Widget to another by hovering over it and pressing Ctrl-C, Ctrl-V.

A number of preset curves that the curve can be set to. The exact shape depends on whether the default curve for the property has a positive or negative slope.

---

## Data-Block Menu¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/templates/data_block.html

**Contents:**
- Data-Block Menu¶
- Preview¶
- Data ID¶
  - ID Sub-Data¶

Lets you select a Data-Block (such as a material) in order to link it to something else (such as an object).

A data-block menu with a search field.¶

Shows an icon indicating the data-block type. Clicking the image or the down arrow opens the popup menu. Dragging the image lets you apply the data-block to something else. (For example, you can drag a material onto an object in the 3D Viewport to assign it. Dragging onto Data ID fields is also possible.)

A list of data-blocks available in the current blend-file, or a link to select an item from. The menu may show a preview besides the items and a search field to search the items in the list by name.

Data-blocks with names that begin with . are hidden from the list, unless a string that also starts with . is entered into the search field, or the Show Hidden Files/Data-Blocks user preference is enabled.

Displays, and allows editing of, the name of the selected data-block.

Displays the number of users of the data (if there’s more than one user). Clicking it will create a single-user copy.

As an example, if three separate objects referenced the same material, the material’s user count would be 3. Changing the material would affect all three objects. If you now selected an object and clicked the user count, the object would receive its very own copy of the material, which can be modified independently of the original that’s still used by the other two.

If a data-block has no real users, it’ll normally be cleaned up (deleted) when saving the blend-file. To prevent this, you can give it a fake user; that way, it’s guaranteed to “survive.” Data-blocks with a fake user have an “F” prefix in the drop-down list.

The Outliner can show an overview of all data-blocks without real users in the blend-file. Simply change its Display Mode to Orphan Data.

Creates a new data-block (or duplicates the current one) and selects it.

Opens the File Browser, for importing an image for example.

Unpack the file packed into the current blend-file to an external one.

Clears the link. Shift-LMB to set the users to zero allowing the data to be fully deleted from the blend-file.

Sometimes there is a list of applied data-blocks (such as a list of materials used on the object).

Data-blocks are discussed further in the Data System chapter.

A Data-Block menu with preview.¶

Some data-block menus have large preview images in their drop-down instead of just icons and names.

A Data ID field is similar to a Data Block Menu, but is only for selecting (and not for other features like creating new data or managing users).

It can show the following elements:

The icon on the left specifies the accepted data-block type.

The text field functions as a search field by matching elements in the list. Press Tab to auto-complete names up to the level where a match is found. If more than one match exists, you have to continue typing. If you type an invalid name, the value will remain unchanged.

Lets you select the data-block directly.

In some Data IDs there is an Eyedropper available through the pipette icon on the right side.

Click the button on the right to clear the reference.

Related types of ID sub-data may become available to select, depending on the data-block type and its intended usage.

If the selected Object in the Target field is a mesh or a lattice, an additional field may be displayed to select one of its vertex groups.

If the selected Object in the Target field is an armature, an additional field may be displayed to select one of its bones.

Once a bone is selected, a numeric field may become available for specifying a point along the bone. A value of 0.0 corresponds to the bone’s head, while a value of 1.0 corresponds to its tail. Any values between these will result in linear interpolation (so a value of 0.5 matches the bone’s center).

If the bone is a bendy bone, clicking on this button will make the point follow the curvature of the B-spline between head and tail, rather than simply going in a straight line.

---

## Decorators¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/buttons/decorators.html

**Contents:**
- Decorators¶

Decorators are small buttons that appear to the right of other buttons and show the state of the property. Decorators may appear next to number fields, menus, and checkboxes to indicate the property can be animated.

Decorators indicating different property states.¶

Clicking on the decorator dot icon will add a Keyframe to that property. Clicking the rhombus icon again will remove the keyframe. A solid rhombus icon indicates there is a keyframe on the current frame, while a non-solid rhombus icon indicates that the property has a keyframe on another frame. Clicking the non-solid rhombus icon will create a keyframe on the current frame with the current property value.

If a property is being driven by another, the decorator shows the driver icon.

Decorators make it quick and easy to glance over properties and see their state.

---

## Default Keymap¶

**URL:** https://docs.blender.org/manual/en/latest/interface/keymap/blender_default.html

**Contents:**
- Default Keymap¶
- Selecting¶
- Hovering¶
  - Properties¶
- Dragging¶
- General¶
- Common Editing Keys¶
- Common Editor Keys¶
- 3D Viewport Keys¶
- Animation¶

While this isn’t a comprehensive list, this page shows common keys used in Blender’s default keymap.

Blender has two main selection modes: left-click select and right-click select. See the Select with Mouse Button preference.

While left-click select is the default as it’s the most common in other applications, right-click select does have its advantages. See: Learn the benefits of right-click select.

The following shortcuts can be pressed while hovering the mouse cursor over an editable field.

Copy the (single) value of the field.

Paste the (single) value of the field.

Copy the entire vector or color of the field.

Paste the entire vector or color of the field.

Open the context menu.

Reset the value to its default.

Invert the value’s sign (multiply by -1.0).

Change the value in incremental steps.

For fields with a pop-up list of values, this cycles the value.

Activates menus and toggles checkboxes.

Hold while editing values to apply the change to all selected items (objects, bones, sequence-strips).

This can be used for number fields and toggles.

The following shortcuts can be used while moving/rotating/scaling an object in the 3D Viewport, dragging the slider of a value, and so on. Note that they should be pressed after starting the drag, not before.

Snap to coarse increments, making it easier to (say) rotate an object by exactly 90°.

Make the value change more slowly in response to mouse movement, giving you more precision.

Snap to fine increments.

Help (context sensitive).

Reserved for user actions.

Adjust Last Operation.

Reserved for user actions.

Render the current frame.

Quick access (favorites).

Toggle Maximize Area.

Ctrl-PageUp / Ctrl-PageDown

Next/previous Workspace.

User configurable; see Spacebar Action.

Playback animation (reverse).

Delete the selected item with a confirmation dialog.

Delete the selected item without a confirmation dialog.

These keys are shared across editors such as the 3D Viewport, UV and Graph editor.

Hide unselected items.

Toggle Pose mode for armatures, or show a mode switching pie menu for others.

In Edit Mode, switch between editing vertices (1), edges (2), or faces (3).

Hold Shift to toggle one of these without disabling the others.

Hold Ctrl to alter how the selection is transformed from the old mode to the new.

See Mesh Selection Modes for details.

Show 3D Viewport navigation pie menu.

Start Fly/Walk Navigation.

3D Viewport Navigation

Add the property to the current keying set.

Remove the property from the current keying set.

When pressed while hovering over an operator button, copies its Python command to the clipboard. This command can then be used in the Python Console or in the Text Editor when writing scripts.

When pressed while hovering over a field, copies its relative data path (also available from the context menu). Useful when writing drivers or scripts.

When pressed while hovering over a field, copies its full data path.

The Cmd key can be used instead of Ctrl on macOS for all but a few exceptions which conflict with the operating system.

List of additional macOS specific keys:

---

## Developer Tools¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/developer_tools.html

**Contents:**
- Developer Tools¶
- Debug¶

These preferences are reserved for features that aid Blender and add-on development. This category is hidden by default and is visible enabling Developer Extras.

Use legacy undo (slower than the new default one, but may be more stable in some cases).

Disables library overrides automatic resync detection and process on file load. Enable when dealing with older blend-files that need manual Resync (Enforce) handling.

Show the Cycles rendering debug panel.

Enable some extra fields in the Asset Browser to aid debugging.

Disabling the asset indexer forces every asset library refresh to completely reread assets from disk.

Enable viewport debugging options for developers in the overlays pop-over.

Enable EEVEE debugging options for developers.

---

## Diffusion¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/domain/liquid/diffusion.html

**Contents:**
- Diffusion¶
- High Viscosity Solver¶

Physics ‣ Fluid ‣ Diffusion

Liquid diffusion defines the physical properties of a liquid and in turn define how a liquid interacts with its environment. The main factors of diffusion are the Viscosity and Surface Tension. These properties can be adjusted to create virtual liquids that behave like water, oil, honey, or any other liquid. A couple presets exist to change the diffusion for different substances are predefined and can be changed in the preset menu. Fluid Diffusion settings can be enabled/disabled in the panel header.

The viscosity refers to the “thickness” of the fluid and actually the force needed to move an object of a certain surface area through it at a certain speed.

For manual entry, please note that real-world viscosity (the so-called dynamic viscosity) is normally measured in Pascal-seconds (\(Pa\cdot s\)), or in Poise units (P, equal to 0.1 \(Pa\cdot s\)), and commonly centiPoise units (cP, equal to 0.001 \(Pa\cdot s\)).

Blender, on the other hand, uses the kinematic viscosity which is the dynamic viscosity divided by the density, \(\frac{Pa\cdot s}{kg/m^{3}}\), which is \(m^{2}/s\). So for example, the viscosity of water at room temperature is 1.002 cP, or 0.001002 \(Pa\cdot s\); the density of water is about 1000 \(kg/m^{3}\), which gives a kinematic viscosity of 0.000001002 \(m^{2}/s\) – so the entry would be 1.002 times 10 to the minus six (1.002×10-6 in scientific notation).

The table below gives some examples of fluids together with their dynamic and kinematic viscosities.

Dynamic viscosity (in cP)

Kinematic viscosity (Blender, in \(m^{2}/s\))

1.002×10-6 (0.000001002)

You can find the kinematic viscosity of more materials in the proper units by asking Wolfram Alpha, e.g. “kinematic viscosity of alcohol in m^2/s”.

To simplify the input of these numbers, the viscosity is changed by entering values in scientific notation by entering a base value and the exponent of that number.

The base of the viscosity value (e.g. 1.002 in the case of water (20 °C)).

The exponent of the viscosity value that will be multiplied by 10-1 (e.g. 6 in the case of water (20 °C)).

The default values in Blender are considered typical for those types of fluids and “look right” when animated. However, actual viscosity of some fluids, especially sugar-laden fluids like chocolate syrup and honey, depend highly on temperature and concentration. Oil viscosity varies by SAE rating. Glass at room temperature is basically a solid, but glass at 1500 °C flows (nearly) like water.

The simulator is not suitable for non-fluids, such as materials that do not “flow”. Simply setting the viscosity to very large values will not result in rigid body behavior, but might cause instabilities.

Surface tension in grid units. Higher value will produce liquids with greater surface tension.

The high viscosity liquid solver can be used to simulate fluids with increased viscosity, replicating the behavior of substances like honey or molasses. This specialized solver enhances the accuracy of slow-moving and thick liquid simulations.

A Strength value of 0 will still apply some viscosity. Uncheck the High Viscosity Solver to disable the high viscosity liquid solver simulation step completely.

The viscosity of the liquid. Higher values result in more viscous fluids.

Strength of 0.2 (at frame 65).¶

Strength of 0.4 (at frame 200).¶

---

## Drawing Tools¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools.html

**Contents:**
- Drawing Tools¶

Change the location of the 3D Cursor.

Tool to use for any of the drawing brushes.

Automatic fill closed strokes areas.

Draw rectangular shapes.

Draw straight multiple lines.

Draw complex Bézier style curves.

Cut strokes in between others.

Eyedropper to create new materials or palette color based on sampled colors in the 3D Viewport.

Automatically create a breakdown keyframe between two normal keyframes.

---

## Draw¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/curves/tools/draw.html

**Contents:**
- Draw¶
- Tool Settings¶
- Options¶

The Curve draw tool allows you to free-hand draw curves.

Type of curve to use for drawing.

Bézier Curve with straight line segments (auto handles).

Lower values give a result that is closer to the drawing stroke, while higher values give more smoothed results.

Incrementally refits the curve (gives best results).

Splits the curve until the tolerance is met (gives a better drawing performance).

Detects corners while drawing based on a specified angle; Any angles above the specified value are considered corners. If a corner is detected, the curve uses non-aligned handles for the corner resulting in a more crisp corner.

Taper factor for the radius of the start and end points along the curve.

Minimum radius when the minimum pressure is applied (also the minimum when tapering).

Radius to use when the maximum pressure is applied (or when a tablet is not used).

Uses stylus pressure to control the radius of the curve.

Controls where and how the curves are drawn.

Uses the depth under the cursor to draw curves.

Used to draw on top of other objects.

Only project the strokes onto selected objects.

Distance to offset the curve from the surface.

Applies a fixed offset (does not scale by the curve radius).

Only uses the start of the stroke for the depth.

The orientation plane to draw on, available when Only First is enabled.

Draws aligned to the surface.

Draws perpendicular to the surface.

Draws aligned to the viewport.

After the tool is run, these options are available in the Adjust Last Operation panel.

Error distance in object units. This can be seen similar to a subdivision rate for the curve. Lower values give a result that is closer to the drawing stroke while higher values give more smoothed results.

Incrementally refits the curve (gives best results).

Splits the curve until the tolerance is met (gives a better drawing performance).

Any angles above this are considered corners.

Toggles whether or not the curve is Cyclic.

---

## Draw¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/curves_new/tools/draw.html

**Contents:**
- Draw¶
- Tool Settings¶
- Options¶

The Curve draw tool allows you to free-hand draw curves.

Type of curve to use for drawing.

Bézier Curve with straight line segments (auto handles).

Lower values give a result that is closer to the drawing stroke, while higher values give more smoothed results.

Incrementally refits the curve (gives best results).

Splits the curve until the tolerance is met (gives a better drawing performance).

Detects corners while drawing based on a specified angle; Any angles above the specified value are considered corners. If a corner is detected, the curve uses non-aligned handles for the corner resulting in a more crisp corner.

Taper factor for the radius of the start and end points along the curve.

Minimum radius when the minimum pressure is applied (also the minimum when tapering).

Radius to use when the maximum pressure is applied (or when a tablet is not used).

Uses stylus pressure to control the radius of the curve.

Controls where and how the curves are drawn.

Uses the depth under the cursor to draw curves.

Used to draw on top of other objects.

Only project the strokes onto selected objects.

Distance to offset the curve from the surface.

Applies a fixed offset (does not scale by the curve radius).

Only uses the start of the stroke for the depth.

The orientation plane to draw on, available when Only First is enabled.

Draws aligned to the surface.

Draws perpendicular to the surface.

Draws aligned to the viewport.

Project the curve on the Z axis.

Draw curves as a NURBS curve with Bézier knot mode, instead of a Bézier curve.

After the tool is run, these options are available in the Adjust Last Operation panel.

Error distance in object units. This can be seen similar to a subdivision rate for the curve. Lower values give a result that is closer to the drawing stroke while higher values give more smoothed results.

Incrementally refits the curve (gives best results).

Splits the curve until the tolerance is met (gives a better drawing performance).

Any angles above this are considered corners.

Toggles whether or not the curve is Cyclic.

---

## Editing Nodes¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/editing.html

**Contents:**
- Editing Nodes¶
- Transform¶
- Connecting Sockets¶
- Disconnecting Sockets¶
  - Interactively¶
  - Mute Links¶
  - Cut Links¶
- Copy/Paste¶
- Duplicate¶
- Duplicate Linked¶

Node ‣ Move, Rotate, Resize

You can move the selected node(s) by clicking and dragging any empty part of them. Alternatively, press G, move the mouse, and click LMB to confirm.

Dragging a node on top of an existing link will intelligently insert the selected node into the link path. This generally uses the first socket that matches the link type. The automatic node attachment feature can be toggled with Alt. When a node is automatically attached, the surrounding nodes will be offset to the right or left depending on the T toggle; see Auto-Offset for more information.

While dragging nodes, you can press F to toggle their parent Frame:

If the nodes are inside a frame, they will be detached from it.

If the nodes are not inside a frame and there is a frame under the cursor, they will be attached to that frame.

In general, it is recommended to arrange your nodes so that data flows from left to right, top to bottom.

The width of a node can be changed by dragging its left or right border.

Rotating (R) and scaling (S) only apply when multiple nodes are selected, and only affect their positions.

LMB-click on a socket and drag. “Connect to Output” will see a line coming out of it; this is called a link. Keep dragging and connect the link to an input socket of another node, then release the LMB.

While multiple links can route out of an output socket, typically a single link can be attached to an input socket, that is unless the input is a multi-socket input with looks like a pill shaped socket.

To swap multiple links of a similar type, press and hold Alt while moving a link. This feature also works when adding a new link into a pre-existing socket.

To reposition the outgoing links of a node, rather than adding a new one, hold Ctrl while dragging from an output socket. This works for single as well as for multiple outgoing links.

Nodes that have no connections can be inserted on a link by just move the node over the link and release when the link is highlighted.

Select multiple nodes with open sockets, then use the Make Links to create links between them. Use Make Links again if there are other nodes which can be connected.

Make and Replace Links works similarly to Make Links, but it will replace existing links if any exist.

Drag the link away from its input socket and let it go, keeping it unconnected.

Activate the menu item or hold the key combination, then draw a line across one or more links to mute/unmute them. A muted link acts as though it’s no longer there; this also means the input fields for specifying fixed values become visible again.

When muting links on the input side of a reroute node, the links on its output side will be muted too.

Activate the menu item or hold the key combination, then draw a line across one or more links to delete them.

The key combination is normally reserved for Lasso Select. In node editors, lasso selection is instead performed with Ctrl-Alt-LMB.

Use Detach Links to cut all the links attached to the selected nodes and move the nodes to a new location.

Node ‣ Copy, Node ‣ Paste

Not only the selected nodes but also the connections between them are copied to the clipboard.

The pasted node will be placed in the same position as when it was copied. Use the same cautions as when duplicating.

Select one or more nodes, activate the menu item or press the key combination, then move the mouse to a new location and click LMB (or press Return) to place the duplicated node(s).

When you duplicate a node, the new node will be positioned exactly on top of the node that was duplicated. If you leave it there (and it is quite easy to do so), you can not easily tell that there are two nodes there! When in doubt, select a node and move it slightly to see if something is hidden underneath.

Node ‣ Duplicate Linked

Duplicate selected nodes, but not their node trees (in the case of group nodes), and move them.

Deletes the selected node(s).

Deletes the selected node(s), then creates new links connecting their former input nodes to their former output nodes.

The Swap operator replaces the selected node with another node type chosen from the menu.

All existing links are automatically reconnected where possible, matching input and output sockets by name and type. If a connection cannot be matched, it is left unconnected.

Node ‣ Show/Hide ‣ Mute

Muting a node removes its contribution to the node tree, and makes all links pass through it without change. Links will appear red as an indicator of passing through the muted node.

Individual node links can be muted with Mute Links.

Node ‣ Show/Hide ‣ Node Preview

Shows/Hides a preview region on the node that displays the frame after that node’s operation has been applied. This can also be toggled by clicking the material ball icon in the node header.

This operator are only available in the Compositor.

Node ‣ Show/Hide ‣ Node Options

Shows/Hides all node properties.

Node ‣ Show/Hide ‣ Unconnected Sockets

Collapses/Expands any input or output sockets that have no other nodes connected to them.

Node ‣ Show/Hide ‣ Unconnected Sockets

Collapses the node so only the node header is visible. This can also be toggled by clicking the triangle on the left of the node header.

Node ‣ Show/Hide ‣ Unconnected Sockets

Applies both the Unconnected Sockets and Collapse operations.

Node ‣ Read View Layers

Reads all the current scene’s render layers from cache, as needed. This can be used to save RAM while rendering because the render layers do not have to be saved in RAM. And also for recovering some information from a failed render. For this to work, Cache Result must be enabled.

This operator are only available in the Compositor.

Connect the output of the selected node to the final output of the node tree (Material Output or World Output in Shader, the final Group Output in Geometry Nodes and Compositor, Output in Texture Nodes), or, if the node is inside a group, to the Group Output.

---

## Editing Point Cloud Objects¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/point_cloud/editing.html

**Contents:**
- Editing Point Cloud Objects¶
- Transform¶
- Duplicate¶
- Set Attribute¶
- Delete¶
- Separate¶

In Edit Mode, you can apply basic editing operations to point cloud objects.

Point clouds can be converted to or from mesh objects for workflows that require geometry-based editing or further processing.

Point Cloud ‣ Transform

Standard transformation operators such as Move, Rotate, and Scale can be used to manipulate selected points within the point cloud.

These operators are useful for repositioning, aligning, or reshaping clusters of points manually.

Point Cloud ‣ Duplicate

Creates a copy of the selected points and reposition the duplicated points.

Duplicated points inherit all attributes from the original points. - Can be used for manually scattering point clusters or duplicating specific regions for further modification.

Point Cloud ‣ Set Attribute

Opens a pop-up window showing the name of the active attribute as well as the value of that attribute for the selected points From there, you assign a new value to a selected attribute across all selected points.

This tool is useful for uniformly setting attribute values such as size, color, or velocity across selected points.

Removes selected points from the point cloud.

Point Cloud ‣ Separate

Creates a new point cloud object from the currently selected points.

This is useful for breaking a larger scan or dataset into manageable segments or organizing different regions of points into separate objects.

---

## Editing Tools¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/edit/tools/toolbar.html

**Contents:**
- Editing Tools¶

Select geometry by dragging a box.

Select geometry by painting on it.

Select geometry by drawing a lasso.

Change the location of the 3D Cursor.

Change the scale of an object by controlling its cage.

Tool to adjust the objects translation, rotations and scale.

Tool for creating and modifying Bézier strokes.

Expand or contract the thickness radius of the selected points.

Bend selected points between the 3D cursor and the pointer.

Shear selected points along the horizontal or vertical screen axis.

Move selected points outward in a spherical shape around the selected strokes’ center.

Automatically create a breakdown keyframe between two normal keyframes.

Draw a line to set the fill material gradient for the selected strokes.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

---

## Edit Face Set¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/edit_face_set.html

**Contents:**
- Edit Face Set¶
- Tool Settings¶

Toolbar ‣ Edit Face Set

Grow/Shrink Face Sets

Edits the Face Set under the cursor.

The operation to apply to the face set.

Grows the face sets boundary by one face based on mesh topology. This is also available as a shortcut operator via Ctrl-W.

Shrinks the face sets boundary by one face based on mesh topology. This is also available as a shortcut operator via Ctrl-Alt-W.

Deletes the faces that are assigned to the face set.

Creates a perfectly flat and smooth geometry patch from the face set. This is the ideal way to trim parts of your mesh if the vertex count is too high for other operations, or the vertex IDs must not be altered (Like when using Multires sculpting).

Creates a smooth as possible geometry patch from the face set by minimizing changes in vertex tangents. This is ideal for creating smooth curved surfaces on complex topology, where just using the smooth brush will not lead to desired results

After using Fair Positions.¶

After using Fair Tangency.¶

The amount of effect the filter has on the mesh. This setting is only available for the fairing operations.

Apply the edit operation to hidden face sets.

---

## Effector¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/effector.html

**Contents:**
- Effector¶
- Settings¶

Effector objects are used to deflect fluids and influence the fluid flow. To define any mesh object as an effector object, add fluid physics by clicking Fluid in Properties ‣ Physics. Then select Effector as the fluid Type.

Force Fields (such as wind or vortex) are supported, like in most physics systems. The influence individual force types have can be controlled per domain object.

Physics ‣ Fluid ‣ Settings

Objects of this type will collide with fluid.

The velocity of objects of this type will be used when baking the guiding. So fluid guiding objects should move and have some velocity.

Multiply the guiding object velocities by this factor. This is useful when working with multiple guiding objects and some of them should have higher or smaller velocities.

The mode describes how guiding velocities should be written into the global guiding velocity field of the domain.

The guiding object will compare the existing velocity in the global velocity field with its own velocity. If its absolute value is greater than the absolute value in the velocity field the guiding velocity will be kept.

A guiding object will compare the existing velocity in the global velocity field with its own velocity. If its absolute value is smaller than the absolute value in the velocity field the guiding velocity will be kept.

The most intuitive option. A guiding object will always write its own current velocity into the global guiding velocity field. Values in the velocity field from a previous frame or guiding object will be overridden.

A guiding object will write the average of its own current velocity and the existing guiding velocity at that cell into the global guiding velocity field.

Number of substeps used to reduce gaps in collision of fluid from fast-moving effectors.

Additional area around the effector that will be considered as an effector.

Enables or disables the effector object effect on the fluid, this property is useful for animations to selectively enable and disable when the effector affects the fluid.

Defines the effector as either a single dimension object i.e. a plane or the mesh is Non-manifold. This ensures that the fluid simulator will give the most accurate results for these types of meshes.

A Manifold mesh can also be declared as planar. The fluid solver will then ignore the volume inside the mesh and just emit fluid from the mesh sides.

---

## Enable Output Node¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/types/output/enable_output.html

**Contents:**
- Enable Output Node¶
- Inputs¶
- Properties¶
- Outputs¶

The Enable Output node toggles the visibility and value of a socket for a Node Group outputs. It can be used to conditionally show or hide outputs from a node group depending on an input value or condition.

A boolean field controlling whether the connected output socket is visible and active. When False, the corresponding output socket in the group is hidden.

The value to pass to the output when it is enabled. This input can be any supported data type depending on the node’s Data Type property.

The data type of the Value input and Value output. This determines what kind of data the node passes through (e.g. Float, Vector, Color, Geometry, etc.).

The same data as the Value input when Enable is True. When Enable is False, the output is disabled and not available to the group output.

---

## Erase Tool¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/erase.html

**Contents:**
- Erase Tool¶
- Tool Settings¶
  - Brush Asset¶
  - Brush Settings¶
    - Cursor¶
- Usage¶
  - Selecting a Brush¶
  - Dissolve Erasing¶
  - Point Erasing¶
  - Stroke Erasing¶

The Erase tool erases already drawn strokes.

The Erase tool uses any of the Grease Pencil Erase draw mode brushes. Activating a brush from an asset shelf or brush selector will also activate this tool for convenience.

The asset selector can be used to open a pop-up asset browser to select the active brush asset for the tool.

See Asset Operators for more information.

The radius of the brush in pixels.

F allows you to change the brush size interactively by dragging the pointer or by typing a number then confirm.

Adjusts the radius based on the stylus pressure when using a Graphics Tablet.

Control how much will affect the eraser has on the stroke transparency (alpha).

You can change the brush strength interactively by pressing Shift-F in the 3D Viewport and then moving the pointer and then LMB. You can also enter the size numerically.

Adjusts the strength based on the stylus pressure when using a Graphics Tablet.

Determines how the erase tool behaves.

To simulate a raster type eraser, this eraser type affects the strength and thickness of the strokes before actually delete a point.

Delete one point at a time.

Delete an entire stroke.

The cursor can be disabled by toggling the checkbox in the Cursor pop-over menu.

In the Tool Settings select the brush to use with the tool. The Erase tool uses Erase Brush types (soft, point and stroke).

Select an erase brush of type Soft/Hard.

Adjust brush settings.

Click and hold LMB or use the Pen tip to delete strokes on the viewport.

The eraser affect the transparency of the strokes.¶

Select an erase brush of type Point.

Adjust brush settings.

Click and hold LMB or use the Pen tip to delete strokes on the viewport.

The eraser delete one point at a time.¶

Select an erase brush of type Stroke.

Adjust brush settings.

Click and hold LMB or use the Pen tip to delete strokes on the viewport.

The eraser delete one stroke at a time.¶

---

## Evaluate Closure¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/types/utilities/closure/evaluate_closure.html

**Contents:**
- Evaluate Closure¶
- Inputs¶
  - Interface¶
- Properties¶
  - Input Items¶
  - Output Items¶
- Outputs¶
- Behavior¶
- Usage¶
- Socket Syncing¶

The Evaluate Closure node executes a connected Closure Zone. It acts as the call site of the closure, running its internal node graph and returning the resulting values.

Closures enable dynamic and customizable node groups by allowing users to pass procedural logic into another node tree. When the Evaluate Closure node runs, the connected closure is evaluated within the current context, matching its input and output sockets by name.

Common uses for the Evaluate Closure node include:

Allowing user-defined behaviors inside procedural systems (e.g. custom scattering, placement rules, or shading logic).

Injecting logic into reusable node groups for advanced effects.

Providing optional customization inputs for high-level node-based tools.

The closure to evaluate. This input expects a connection from a Closure Zone. If no closure is connected, the node operates in pass-through mode (see below).

The node can define additional inputs manually, which are matched by name to the corresponding inputs of the connected closure. When the closure is connected, these sockets automatically sync to reflect the closure’s defined interface.

The Evaluate Closure node does not have functional properties, but its input and output interface can be managed in the Node tab of the Sidebar.

Updates the current node to match the socket signature of the connected nodes. Use this after renaming, adding, or removing sockets.

Marks the node as defining a closure signature to be used by other closure nodes. Ensures consistent input and output definitions across related closures.

Displays one entry per socket defined in the closure. Double-click to rename.

Add a new input socket to the closure interface.

Delete the selected input socket.

The data type for the selected socket (e.g. Float, Vector, Geometry, Object, Bundle). For value types, a default value field appears and is used when the socket is unlinked.

Defines the data structure supported by the input socket, such as a Single value, Field, or Grid. The shape determines how the data is evaluated and passed through the node network. See Socket Shape for more information.

Displays one entry per output socket. Double-click to rename.

Add a new output socket to the node.

Delete the selected output socket.

The data type for the selected socket (e.g. Float, Vector, Geometry, Object, Bundle). For value types, a default value field appears and is used when the socket is unlinked.

The outputs of the Evaluate Closure node depend on its current configuration:

When a closure is connected – Each output corresponds to an output socket of the Closure Zone with the same name.

When no closure is connected – Outputs are defined manually through the Output Items section of the Sidebar.

When executed, this node evaluates the connected closure’s internal node graph. All input values are passed into the closure by name, and all resulting values are returned through the corresponding outputs.

If no closure is connected, or if the node is muted, Evaluate Closure automatically passes through any matching inputs and outputs by name. This pass-through mode makes closures optional and allows node groups to function even without one.

Evaluation occurs in the local context of the node tree where Evaluate Closure resides, inheriting relevant fields, attributes, and geometry data.

The Evaluate Closure node is typically used to make a node group partially customizable while maintaining a stable, reusable framework.

For example, a terrain generator might use Evaluate Closure to define how trees are distributed across a landscape:

Inside the generator group, replace the fixed tree placement logic with an Evaluate Closure node.

Expose the closure input on the group’s interface.

In the main node tree, connect a Closure Zone defining the desired tree distribution behavior.

Whenever the closure is evaluated, the connected node graph runs within the terrain generator’s context, producing a customized result.

Example: custom tree distribution using Evaluate Closure.¶

Closures rely on matching socket names to connect inputs and outputs correctly. If the connected Closure Zone and Evaluate Closure nodes have mismatched signatures, Blender can synchronize them automatically.

A sync icon appears when the socket layout differs.

Clicking the icon updates sockets to match the connected closure.

Automatic syncing occurs the first time a closure is connected.

Existing sockets are never modified automatically afterward to prevent data loss.

Viewer and inspection nodes may not display accurate values when closures are evaluated in multiple contexts.

Captured external values are read-only and cannot be modified inside the evaluation.

Closures currently cannot access attributes or data outside their evaluation context.

---

## Expand¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/editing/expand.html

**Contents:**
- Expand¶
- Expand Mask by Topology¶
  - Usage¶
  - Controls¶
- Expand Mask by Normals¶
- Expand Face Set by Topology¶
  - Usage¶
- Expand Active Face Set¶
  - Usage¶

This is a multi-purpose modal operator to intuitively create and edit masks/face sets. When executed, it uniformly expand outwards a pattern from the vertex under the cursor.

These operators are meant to be used interactively through the shortcut.

There is also a full showcase of the Expand features and use cases.

A preview of Expand Mask by Topology¶

Mask ‣ Expand Mask by Topology

Expands a mask from the active vertex.

Start the operator and expand a mask from an origin to your mouse cursor distance. Then confirm with LMB or Return

By default the expansion will use a Geodesic falloff 1 to create perfectly accurate distances along the surfaces. Use other falloff types via 2, 3 & 4 to expand via triangles, whole faces or scene distances instead.

The typical result when using the Diagonals falloff to expand along the quads of the face.¶

Start Expand while pointing at an open boundary to expand from the entire boundary loop. This will always use the Topology falloff mode.

Move your cursor outside of the boundaries of the mesh to mask the entire connected mesh. This can be done repeatedly to quickly mask separate meshes.

Hold Ctrl to snap to face sets under your cursor and fill them. Any face set that was already covered in the expansion will be filled as well.

While using any Transform tool, the pivot point will automatically snap the border of an Expand result. This way areas (Like limbs) can be masked and then immediately rotated or otherwise transformed.

The different falloff types can be used for circular, triangular and square patterns. More loops can also be added/removed via W & Q to repeat the pattern across the mesh.

An example of using expand with mirror options, loops and a recursion to create wood carving patterns.¶

Mirror options can also be combined with the expansion.

Linear gradients G or brush falloff gradients B will help to add slanted surfaces to the patterns.

A “Recursions” with R or Alt-R will start a new expansion along the border of the current expansion. Doing this multiple times, can help for increasingly random patterns or advanced pattern creation.

An example of using loops and gradients with multiple expanded masks.¶

Remember that Expand only affects visible geometry. So if a pattern should only be created on a part of the mesh, hide the other geometry first.

Use the Mesh Filter to deform the geometry and the Color Filter to add colors, to apply the patterns on the sculpt.

Textures can be used to affect the shape and gradients of the expanded mask. This feature can be combined with loops and recursion to create unique results.

To use a texture, you need to assign it to your currently active brush in the Texture Brush Settings. The texture can be edited/created in the Texture Properties.

This texture only works when the Mapping is set to 3D.

Use Y and T to increase or decrease the affect the texture has on the edge of the mask.

F Flips between expanding a positive mask (value of one) or a negative mask (value of zero). In the case of face sets, this option flips between including areas inside the masked area or areas outside the masked area. .. needs visual technical examples for both

E Accumulate the new mask on top of the previous one or replace it. For Face Sets, this will toggle between creating Face Sets boundaries or replacing the existing Face Sets.

Spacebar Moves the initial vertex used for calculating the falloff. .. needs visual technical example

1 Uses a falloff based on the Geodesic distances from the edge boundary to the active vertex.

2 Uses a falloff based on a flood fill using edges.

3 Uses a falloff based on a flood fill using polygon diagonals and edges.

4 Uses a falloff based on the Euclidean distances from the edge boundary to the active vertex. .. needs visual technical examples

G Enables linear gradient of values from the origin to the current active vertex.

B Similar to linear gradient but uses the current brush Falloff to define the shape of the falloff. .. needs visual technical examples

R Start a new expansion with a Geodesic falloff from the boundary of the current falloff.

Alt-R Start a new expansion with a topology falloff from the boundary of the current falloff. .. needs visual technical examples

Ctrl Isolates the expanded region to the boundary of the face set under the cursor.

W Increase the number of loops or iterations the operator is run; using four loops will split the mask into four parts.

Q Decrease the number of loops or iterations the operator is run; using four loops will split the mask into four parts. .. needs visual technical examples

Y Increases the falloff distance when using a texture to distort the mask shape.

T Decreases the falloff distance when using a texture to distort the mask shape. ..needs visual technical examples

Mask ‣ Expand Mask by Normals

Expand a mask, following the curvature of the surface. This operator uses the same internal operator as Expand meaning all the shortcuts and functionality works the same as that tool.

This operator is especially useful for hard surface sculpting.

If one expansion does not properly fill the entire desired surface, use the operator repeatedly with a different starting point.

Using any of the Falloff shortcuts 1-4 will replace the curvature falloff of this operator.

Face Sets ‣ Expand Face Set by Topology

Expands a face set from the active vertex. This operator uses the same internal operator as Expand meaning all the hotkeys and functionality works the same as that tool, with the gradient features as the exception.

Expanding Face Sets has all the same use cases as expanding masks. The advantage for this one is that they will be saved for repeated usage. Face sets can be filled any time with a mask, so assigning areas face sets will save you time. (And of course face sets can be used to hide face sets)

When using the Pose Brush it is most predictable when using it with Face Sets to define the face set boundaries as pivot point locations. Face Sets can be expanded from a point or from a boundary between hidden face sets to create them quickly. Alternatively Grow/Shrink Face Sets or use the Expand Active Face Set to dynamically grow/shrink them.

Tools like the Cloth Filter and Cloth Brush work especially well when only simulating small areas at a time. Face Sets can very easily be created with Expand to assign areas of action.

Face Sets ‣ Expand Face Set by Topology

Expands an existing face set with a geodesic falloff. This operator uses the same internal operator as Expand meaning all the hotkeys and functionality works the same as that tool.

Using any of the Falloff shortcuts 1-4 the operator to switch to Expand Face Set by Topology.

Resize a Face Set along the surface distances. It is an alternative to Grow/Shrink Face Sets which follows the topology instead of geodesic distances.

When holding Ctrl the expansion will instead snap to other Face Sets. This is a fast way of joining multiple face sets into one.

---

## Extrude Manifold¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/tools/extrude_manifold.html

**Contents:**
- Extrude Manifold¶
- Example¶

Toolbar ‣ Extrude Manifold

Mesh ‣ Extrude ‣ Extrude Manifold

This tool is very similar to Extrude Faces but enables Dissolve Orthogonal Edges by default. This causes the tool to automatically split and remove adjacent faces when extruding inwards.

Extrude Manifold Example.¶

---

## Extrude Region¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/tools/extrude_region.html

**Contents:**
- Extrude Region¶
- Details¶

Toolbar ‣ Extrude Region

Extrusion tools duplicate vertices, while keeping the new geometry connected with the original vertices. Vertices are turned into edges and edges will form faces.

Single vertex extruded.¶

Single edge extruded.¶

This tool is of paramount importance for creating new geometry. It allows you to create parallelepipeds from rectangles and cylinders from circles, as well as easily creating such things as tree limbs.

The axis on which vertices and edges are extruded along can be set interactively. Faces are extruded by default along their averaged normal. The extrusion can be limited to a single axis by specifying an axis; see Axis Locking.

The extrude tools differentiate in how the new geometry is connected in itself.

Only the border loop gets extruded. The inner region of the selection gets moved unchanged with the extrusion.

Although the process is quite intuitive, the principles behind Extrude are fairly elaborate as discussed below:

First, the algorithm determines the outside edge loop of the extrude; that is, which among the selected edges will be changed into faces. By default (see below), the algorithm considers edges belonging to two or more selected faces as internal, and hence not part of the loop.

The edges in the edge loop are then changed into faces.

If the edges in the edge loop belong to only one face in the complete mesh, then all of the selected faces are duplicated and linked to the newly created faces. For example, rectangles will result in parallelepipeds during this stage.

In other cases, the selected faces are linked to the newly created faces but not duplicated. This prevents undesired faces from being retained “inside” the resulting mesh. This distinction is extremely important since it ensures the construction of consistently coherent, closed volumes at all times when using Extrude.

When extruding completely closed volumes (like e.g. a cube with all its six faces), extrusion results merely in a duplication, as the volume is duplicated, without any link to the original one.

Edges not belonging to selected faces, which form an “open” edge loop, are duplicated and a new face is created between the new edge and the original one.

Single selected vertices which do not belong to selected edges are duplicated and a new edge is created between the two.

---

## Extrude to Cursor¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/tools/extrude_cursor.html

**Contents:**
- Extrude to Cursor¶
- Creating Faces¶

Interactively places new vertices with Ctrl-RMB at the mouse cursor position.

The most basic element, a vertex, can be added with a Ctrl-RMB click when no other vertices are selected. Because the camera space (computer screen) is two-dimensional, Blender cannot determine all three vertex coordinates from a single mouse click, so the new vertex is placed at the depth of the 3D cursor.

To create interconnected vertices, you can add a vertex and continuously make subsequent Ctrl-RMB operations with the last vertex selected. This will link the last selected vertex with the vertex created at the mouse position with an edge (see Fig. Adding vertices one by one.), and will continuously create and connect new vertices if you continue repeating this operation.

Adding vertices one by one.¶

Quad from an Edge with source automatically rotated.¶

If you have two vertices selected and already connected with an edge, Ctrl-RMB click will create a planar face, also known as a quad. Blender will follow your mouse cursor and will use the planar view from your viewport to create those quads.

For Ctrl-RMB, Blender will automatically rotate the last selected Edge (the source) for the subsequent operations if you have at least one face created, dividing the angles created between the newly created edge and the last two edges, creating a smooth angle between them. Blender will calculate this angle using the last positive and negative position of the last X and Y coordinates and the last connected unselected edge. If this angle exceeds a negative limit (following a quadrant rule) between the recently created edge and the last two, Blender will wrap the faces. But if you do not want Blender to rotate and smooth edges automatically when extruding from Ctrl-RMB, you can also inhibit Blender from rotating sources using the shortcut Shift-Ctrl-RMB. In this case, Blender will not rotate the source dividing the angle between those edges when creating a face.

If you have three or more vertices selected, and Ctrl-RMB click, you will also create planar faces, but along the vertices selected, following the direction of the cursor. This operation is similar to an extrude operation.

When adding objects with Ctrl-RMB, the extrusions of the selected elements, being vertices, edges and faces with the Ctrl-RMB, are viewport dependent. This means, once you change your viewport, for example, from top to left, bottom or right, the extrusion direction will also follow your viewport and align the extrusions with your planar view.

---

## Eyedropper¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/eyedropper.html

**Contents:**
- Eyedropper¶
- Tool Settings¶
- Usage¶

The Eyedropper tool is used to create materials or palette color based on sampled colors in the 3D Viewport.

Create a new material with the Stroke Base Color to be the sampled color.

The color transformation will be applied on the stroke and/or the fill color.

Only paint over strokes.

Only paint over fill areas.

Paint over strokes and fill areas

Add a new color to the color palette based on the sampled color.

Sets the brush color to the sampled color.

LMB Create a stroke material.

Shift-LMB Create a fill material.

Shift-Ctrl-LMB Create both a stroke and fill material.

Holding LMB and dragging accumulates the average color under the mouse cursor.

---

## Eyedropper¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/buttons/eyedropper.html

**Contents:**
- Eyedropper¶

The eyedropper (pipette icon) allows you to sample from anywhere in the Blender window. The eyedropper can be used to select different kinds of data:

This is the most common usage. The eyedropper is used to sample a pixel’s color from anywhere within Blender.

The View Transform of the color management affects the color. In order to get consistent results, it should be set to Standard. If it’s set to any other option, the eyedropper may return an inaccurate color.

Dragging the cursor over the window to sample a line which is converted into a color ramp.

This is used with object buttons (such as parent, constraints or modifiers) to select an object from the 3D Viewport or Outliner, rather than having to select it from a drop-down.

This is used when a subtarget to an armature can be chosen. It is possible to choose a bone from the 3D Viewport or from the outliner. Only bones that belong to the armature that was chosen as a target can be picked.

In the 3D Viewport, bones can only be picked if the armature is in Pose Mode or in Edit Mode.

Number fields effecting distance can also use the eyedropper.

This is used to set the camera’s depth of field so the depth chosen is in focus.

E will activate the eyedropper while hovering over a button.

LMB dragging will mix the colors you drag over, which can help when sampling noisy imagery.

Spacebar resets and starts mixing the colors again.

---

## Face Set Gesture Tools¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/face_set_tools.html

**Contents:**
- Face Set Gesture Tools¶
- Box Face Set¶
- Lasso Face Set¶
- Line Face Set¶
- Polyline Face Set¶
- Tool Settings¶

Face Set gesture tools apply a single new Face Set to all faces within the selection area.

All Face Set gesture tools can be activated in the Toolbar and are comprised of the following:

Toolbar ‣ Box Face Set

Creates a new Face Set based on a box gesture.

Toolbar ‣ Lasso Face Set

Creates a new Face Set based on a lasso gesture.

Toolbar ‣ Line Face Set

Creates a new Face Set based on a line gesture.

Toolbar ‣ Polyline Face Set

Creates a new Face Set based on a polyline gesture.

Only creates a face set on the faces that face towards the view.

---

## Field Weights¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/domain/field_weights.html

**Contents:**
- Field Weights¶

Properties ‣ Physics ‣ Fluid ‣ Field Weights

These settings determine how much gravity and Force Fields affect the fluid.

When set, fluid can only be influenced by force fields in the specified collection.

How much the fluid is affected by Gravity.

Overall influence of all force fields.

The other settings determine how much influence individual force field types have.

---

## Fill Tool¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/fill.html

**Contents:**
- Fill Tool¶
- Tool Settings¶
  - Brush Asset¶
  - Brush Settings¶
    - Advanced¶
      - Gap Closure¶
- Usage¶
  - Selecting a Brush and Material¶
  - Filling Areas¶
  - Fill Guides¶

The Fill tool is used to automatically fill closed strokes areas.

The Fill tool uses any of the Grease Pencil Fill draw mode brushes. Activating a brush from an asset shelf or brush selector will also activate this tool for convenience.

The asset selector can be used to open a pop-up asset browser to select the active brush asset for the tool.

See Asset Operators for more information.

You can also configure the brush main settings exposed on the Tool Settings for convenience.

The portion of area to fill.

Fills the area inside the shape under the cursor.

When clicking outside the drawing, fills all shapes touching the area under the cursor.

Multiplier for fill boundary accuracy. Higher values are more accurate but slower.

Size in pixels to expand or shrink the fill area from the strokes boundary.

The thickness radius of the boundary stroke in pixels.

Sets the type of fill boundary limits calculation to perform.

Use the thickness of the strokes and the editing lines together.

Use only the thickness of the strokes (ignore edit lines).

Use only the edit lines (ignore strokes).

Toggle show auxiliary lines to see the fill boundary.

Determines which Layers are used for boundary strokes.

Calculates boundaries based on all visible layers.

Calculates boundaries based on the active layer.

Calculates boundaries based on the layer above the active layer.

Calculates boundaries based on the layer below the active layer.

Calculates boundaries based on all layers above the active layer.

Calculates boundaries based on all layers below the active layer.

Number of simplify steps to apply to the boundary line. Higher values reduce the accuracy of the final filled area.

When enabled, strokes with transparency does not take into account on fill boundary calculations.

The value slider controls the threshold to consider a material transparent.

When enabled, fill only visible areas in the viewport.

When enabled, after creating a fill, automatically remove the fill guide strokes.

Gap closure lines are automatic temporarily lines that help to close gaps on the strokes.

Control the Size of the line extension or the circumference to use to calculate the lines that will close the gaps.

Sets the type of Gap closure method to use.

Uses the Radius of circumference of opened nearest points to calculate a line that close the gap.

Extends the opened strokes to close gaps.

Toggle show closure lines helper.

Check if extend lines collide with strokes, stopping the extension if a collision is detected.

In the Tool Settings select the brush, material and color type to use with the tool. The Fill tool uses Fill Brush types. See Brush Settings for more information.

Click LMB in a closed stroke area. The tool will automatically calculate the boundary and create a new closed stroke filled with the material selected.

Use the fill tool to leak materials on closed areas.¶

Final filled drawing.¶

If you have a large gap in an area that you want fill, you can add fill guides manually, a temporary auxiliary lines for closing open shapes. To create a fill guide stroke use Alt-LMB and draw a line to close the desired area.

Add fill guide to close open areas (red lines).¶

Use the Fill tool to leak material on the new closed area.¶

When you are satisfied with the fill result you can delete the fill guide using the Clean Up tool in the Grease Pencil Menu in Edit Mode.

A more automatic way to close gaps in an area that you want fill is using temporarily helper lines. There are two method to use “Radius” or “Extend”

Radius use temporary auxiliary lines calculated from the radius of nearby open points to close open shapes. Set the size more than zero to control the circle size over opened points (the circle will disappear when the line close the gap). Click over the area you want to be filled and change the length of the strokes using PageUp PageDown or Wheel. When you are satisfied with the length and you are sure the temporarily strokes cross each other, click again to fill the area.

Use Radius mode to close open areas (Red circles and cyan lines).¶

Use Fill Tool to leak material on the new closed area.¶

Extend use temporary auxiliary lines extending the actual strokes ends for closing open shapes. Set the size more than zero to use the extended lines, click over the area you want to be filled and change the length of the strokes using PageUp/PageDown, Wheel or a pen’s MMB. When you are satisfied with the length and you are sure the temporarily strokes cross each other, click again to fill the area.

Use Extend mode to close open areas (cyan lines).¶

Use Fill Tool to leak material on the new closed area.¶

---

## Flow¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/flow.html

**Contents:**
- Flow¶
- Settings¶
  - Flow Source¶
  - Initial Velocity¶
  - Texture¶

Fluid Flow types are used to add or remove fluid to a domain object. Flow objects should be contained within the domain’s Bounding Box in order to work.

To define any mesh object as a Flow object, add Fluid physics by clicking Fluid in Properties ‣ Physics. Then select Flow as the fluid Type. Now you should have a default fluid flow source object.

Physics ‣ Fluid ‣ Settings

Emit both fire and smoke.

Emit only fire. Note that the domain will automatically create some smoke to simulate smoke left by burnt fuel.

Controls if the Flow object either adds (Inflow), removes (Outflow), or turns the mesh itself into fluid (Geometry).

This object will emit fluid into the simulation, like a water tap or base of a fire.

Any fluid that enters the Bounding Box of this object will be removed from the domain (think of a drain or a black hole). This can be useful in combination with an inflow to prevent the whole domain from filling up. Outflow objects can be animated and the area where the fluid disappears will follow the object as it moves around.

All regions of this object that are inside the domain bounding box will be used as actual fluid in the simulation. You can place more than one fluid object inside the domain. Also make sure that the surface normals are pointing outwards or else they will not simulate properly. In contrast to domain objects, the actual mesh geometry is used for fluid objects.

Enables or disables the flow of fluid, this property is useful for animations to selectively enable and disable when fluid is being added to or removed from the domain.

Number of sub-steps used to reduce gaps in emission of fluid from fast-moving sources.

Sampling sub-steps: 0.¶

Sampling sub-steps: 3.¶

Sub-Steps occur at every simulation step and not per frame. The simulation step count is controlled by the adaptive time stepping.

The color of emitted smoke. When smoke of different colors are mixed they will blend together, eventually settling into a new combined color.

If this checkbox is enabled, the emitter will only produce more smoke or fire if there is space for it in the emitter region. Otherwise smoke or fire will always be produced and add up.

Difference between the temperature of emitted smoke and the domain’s ambient temperature. This setting’s effect on smoke depends on the domain’s Heat Buoyancy.

Amount of smoke to emit at once. Larger values result in more density being produced.

Amount of “fuel” being burned per second. Larger values result in larger flames, smaller values result in smaller flames:

When set, use the specified Vertex Group to control where smoke is emitted.

This setting defines the method used to emit fluid.

Emit fluid directly from the object’s mesh.

Defines the effector as either a single dimension object i.e. a plane or the mesh is Non-manifold. This ensures that the fluid simulator will give the most accurate results for these types of meshes.

Maximum distance in Voxels from the surface of the mesh in which fluid is emitted. Since this setting uses voxels to determine the distance, results will vary depending on the domain’s resolution.

Amount of fluid to emit inside the emitter mesh, where 0 is none and 1 is the full amount. Note that emitting fluid based on volume can have unpredictable results if your mesh is Non-manifold.

Fire or Smoke Only: Create smoke or fire from a particle system on the flow object.

The particle system can be selected with a Data ID.

Note that only Emitter type particle systems can add smoke. See Particles for information on how to create a particle system.

When this setting is enabled, it allows the Size setting to define the maximum distance in voxels at which particles can emit smoke, similar to the Surface Emission setting for mesh sources.

When disabled, particles will fill the nearest Voxel with smoke.

When enabled, the fluid will inherit the momentum of the flow source.

Factor for the inherited velocity. A value of 1 will emit fluid moving at the same speed as the source.

This option controls how much velocity fluid is given along a face Normal. Note that, initial velocities will always be applied along all face normals. Thus with a closed flow source mesh, fluid will always be emitted in more than one direction. To set initial velocities along only one direction all normals need to point in the same direction. This is can be achieved when using a plane as the flow object.

Initial velocity along X, Y, Z coordinates in world space. This can be used in addition to the initial velocity along the Normal.

Physics ‣ Fluid ‣ Settings ‣ Texture

When enabled, use the specified texture and settings to control where on the mesh smoke or fire can be emitted from. These settings have no effect on Outflow Flow Behavior.

A Data ID selector to choose the Texture.

Controls whether to use Generated UVs or manual UV mapping.

Overall texture scale.

Translates the texture along the Z axis.

---

## Fluid¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/physics/fluid.html

**Contents:**
- Fluid¶
- Options¶
  - Fluid Properties¶
  - Advanced¶
  - Springs¶

Particle System ‣ Physics

Fluid Physics settings.¶

Fluid particles are similar to Newtonian ones but this time particles are influenced by internal forces like pressure, surface tension, viscosity, springs, etc. From liquids to slime, goo to sand and wispy smoke the number of possible use cases is endless.

Blender particle fluids use the SPH techniques to solve the particles fluid equations. Smoothed-particle hydrodynamics (SPH) is a computational method used for simulating fluid flows. It has been used in many fields of research, including astrophysics, ballistics, vulcanology, and oceanography. It is a mesh-free Lagrangian method (where the coordinates move with the fluid), and the resolution of the method can easily be adjusted with respect to variables such as the density.

Fluid physics share options with Newtonian Physics. These are covered on that page.

How incompressible the fluid is.

Linear viscosity. Use lower viscosity for thicker fluids.

Artificial buoyancy force in negative gravity direction based on pressure differences inside the fluid.

Particle System ‣ Physics ‣ Advanced

How strongly the fluid tries to keep from clustering (factor of stiffness). Checkbox sets repulsion as a factor of stiffness.

Creates viscosity for expanding fluid. Checkbox sets this to be a factor of normal viscosity.

Fluid’s interaction radius. Checkbox sets this to be a factor of 4 × particle size.

Density of fluid when at rest. Checkbox sets this to be a factor of default density.

Particle System ‣ Physics ‣ Springs

Rest length of springs. Factor of particle radius. Checkbox sets this to be a factor of 2 × particle size.

Use viscoelastic springs instead of Hooke’s springs.

How much the spring has to be stretched/compressed in order to change its rest length.

How much the spring rest length can change after the elastic limit is crossed.

Use initial length as spring rest length instead of 2 × particle size.

Create springs for this number of frames since particle’s birth (0 is always).

---

## Fluid Modifier¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/modifiers/physics/fluid.html

**Contents:**
- Fluid Modifier¶
- Options¶
- Example¶

The Fluid modifier is a container for a Fluid Physics simulation. It can be useful for example, to simulate on a low-poly mesh then add a Subdivision Surface Modifier after the Fluid modifier to improve the visual quality of the fluid without drastically increasing simulation times.

As the modifier is only a container its actual options can be configured in the Physics Properties tab. See the Fluid Physics Properties for more information.

Example of a liquid simulation.¶

---

## Fly/Walk Navigation¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/navigate/walk_fly.html

**Contents:**
- Fly/Walk Navigation¶
- Walk Navigation¶
  - Usage¶
- Fly Navigation¶
  - Usage¶

The standard navigation controls are sometimes limiting, especially for large environments such as architectural models. In these cases, it may be preferable to use first person controls instead, where you can look around while “standing” in one place rather than orbiting around a central viewpoint.

Blender offers two such alternative navigation methods: Flying and Walking. You can initiate either method from the View ‣ Navigation menu. You can also initiate your preferred one (configured in the Preferences) by pressing Shift-AccentGrave.

Common use cases for Fly/Walk include:

This can be a quick way to navigate a large scene.

When activated from a camera view Numpad0, the camera will move along with you.

You can record the path you take by entering a camera view, enabling Auto Keying, starting animation playback, and finally activating Fly/Walk navigation. The path will be recorded as camera keyframes which can then be used for rendering.

Animation playback can’t be controlled while Fly/Walk navigation is active, so when you’re done recording, you first need to exit the navigation with LMB before you can stop playback.

View ‣ Navigation ‣ Walk Navigation

This navigation method behaves like a typical first person game. It works with a combination of keyboard keys and mouse movement.

Move the mouse in the direction you want to look and use the keys listed below to walk around the scene.

When you are happy with the new view, press LMB to confirm. In case you want to go back to where you started, press Esc or RMB.

All these keys are also listed in the Status Bar while navigating. Settings like mouse sensitivity and default speed can be adjusted in the Preferences.

Move up (global) – only available if Gravity is off.

Move down (global) – only available if Gravity is off.

Move up (local) – only available if Gravity is off.

Move down (local) – only available if Gravity is off.

Teleport to the location at the crosshair (offset by the Camera Height value set in the Preferences).

Increase the movement speed.

WheelDown/NumpadMinus

Decrease the movement speed.

Speed up the movement temporarily.

Slow down the movement temporarily.

Jump – only available if Gravity is on.

Correct the Z axis of the view (smoothly roll it to ensure it’s upright, not tilted to a side).

Increases the jump height.

Decreases the jump height.

View ‣ Navigation ‣ Fly Navigation

On activation, the cursor is centered inside a rectangle that defines a safe zone. When the cursor is outside this zone, the view will rotate/pan.

Move the mouse outside the safe zone in the direction you want to look.

Click LMB or press Spacebar to keep the current view and exit Fly navigation. In case you want to go back to where you started, press Esc or RMB.

Drag to pan the view. Flying will pause while you’re doing this.

Increase the acceleration in the direction of motion. If there is no motion, start accelerating forward.

WheelDown/NumpadMinus

Decrease the acceleration in the direction of motion. If there is no motion, start accelerating backward.

Slow down as long as the key is held, until the view eventually comes to a standstill.

Disable rotation – while held, the view rotation doesn’t influence the flight direction. This allows you to fly past an object, keeping it centered in the view even as you fly away from it.

Toggle X axis correction. If enabled, the view will smoothly pitch to look at the horizon when the cursor is in the safe zone.

Toggle Z axis correction. If enabled, the view will smoothly roll to an upright orientation.

---

## Frame Node¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/types/layout/frame.html

**Contents:**
- Frame Node¶
- Usage¶
- Properties¶
- Editing¶
  - Join in New Frame¶
  - Add to Frame¶
  - Remove from Frame¶

The Frame node is used to organize and group other nodes within the editor. It helps manage complex node trees by visually grouping related nodes together.

Frames are particularly useful when the setup is too large to view easily at once, or when you want to separate logical sections of a node tree without creating a reusable Node Group.

Example of a Frame node used to organize nodes.¶

Nodes can be added to a frame by dragging them inside it.

Moving the frame also moves all contained nodes.

Frames can be resized by dragging the corners or edges.

The frame can display a custom label, useful for naming sections of your node setup.

Font size of the label. For example, for subordinate frames to have smaller titles.

Once a node is placed in the Frame, the Frame shrinks around it so as to remove wasted space. At this point it is no longer possible to select the edge of the Frame to resize it, instead resizing occurs automatically when nodes within the Frame are rearranged. This behavior can be changed by disabling this option.

When you need to display more comprehensive text, frame nodes can display the contents of a text data-block. This is read-only, so you will need to use the Text Editor to modify the contents.

Node ‣ Join in new Frame

Creates a new Frame node around the selected nodes.

When called using the shortcut F, a popup appears allowing you to assign a custom Label to the new frame node. This label is shown as the title of the frame and can be used to describe its contents.

Once a frame node is placed, nodes can be added by dropping them onto the frame or by selecting the node(s) then the frame and using Ctrl-P. This can be thought of as Parenting the selection to the frame.

Node ‣ Remove from Frame

To remove nodes from a frame, select and use Alt-P. This can be thought of as unparenting the selection from the frame.

---

## Grab¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/uv/tools/grab.html

**Contents:**
- Grab¶
- Tool Settings¶

The Grab tool moves UVs around.

This option controls the radius of the brush, measured in pixels. F allows you to change the brush size interactively by dragging the mouse and then LMB. Typing a number then enter while using F allows you to enter the size numerically.

Controls how much each application of the brush affects the UVs. You can change the brush strength interactively by pressing Shift-F in the 3D Viewport and then moving the brush and then LMB. You can enter the size numerically also while in Shift-F sizing.

The Falloff allows you to control the Strength falloff of the brush. The falloff is mapped from the center of the brush (left part of the curve) towards its borders (right part of the curve). Changing the shape of the curve will make the brush softer or harder. Read more about using the Curve Widget.

You can choose how the strength of the falloff is determined from the center of the brush to the borders by manually manipulating the control points within the curve widget. There are also a couple of preset custom curves displayed at the bottom of the curve widget that can be used on their own or as a starting point for tweaking.

The center strength, the border strength, and the falloff transition between them are evenly distributed.

Similar to Smooth but produces a wider center point of the brush before tapering off.

The strength of the brush is predominately at its strongest point with a steep falloff near the border of the brush.

Similar to a Sphere but the center is a more concentrated point.

The center of the brush is the strongest point then exponentially tapers off to a lower strength, creating a fine point.

With the center being the strongest, the strength will consistently weaken as it reaches the border of the brush.

Similar to Sharp but the center point is more condensed.

A hybrid between Smooth and Sphere.

The strength of the brush remains unified across the entire brush. This will create a sharp edge at the border of the brush.

Locks the boundary of UV islands from being affected by the brush. This is useful to preserve the shape of UV islands.

To edit all islands and not only the island nearest to the brush center when the sculpt stroke was started.

---

## Guides¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/domain/guides.html

**Contents:**
- Guides¶

Physics ‣ Fluid ‣ Guides

Fluid guides are used to apply forces onto the simulation. They are like simple external forces but also seek to preserve the physically accurate flow of the fluid. The Guides panel allows you to adjust guiding forces globally, i.e. for the entire domain. Enabling the guides hints the fluid solver to use the more accurate, but also computationally more expensive pressure solving step.

Even when there are no guiding objects baked or there is no guiding domain attached, the fluid solver will still perform the more expensive pressure guiding algorithm if guiding is enabled. It is therefore recommended to only enable Guides when there is a clear intention to use guiding in the simulation.

Fluid guiding is an implementation of Primal-Dual Optimization for Fluids.

Controls the lag of the guiding. A larger value (also known as the ‘alpha’ guiding value) results in a greater lag.

This setting determines the size of the vortices that the guiding produces. A greater guiding size (also known as the blur radius or ‘beta’ guiding value) results in larger vortices.

All guiding velocities are multiplied by this factor. That is, every cell of the guiding grid, which has the same size as the domain object, is multiplied by this factor.

Guiding velocities can either come from objects that move inside the domain or from other fluid domains.

All effector objects inside the domain will be considered for the global guiding velocity grid. Once effector objects have been baked it is not possible to change the fluid domain resolution anymore.

When using another fluid domain as the guiding velocity source this domain may have a different resolution and may also be of a different type (e.g. the guiding domain is of type Gas while the actual domain with the guiding effect in it is of type Liquid).

In order to use a domain as the velocity source, this domain needs to be baked already.

When using Domain as the velocity source, this field serves to select the guiding domain object.

This option is only available when using the Modular cache type and when using Effector as the Velocity Source. Bake Guides writes vertex velocities of effector objects to drive. It is meant to be used before baking the fluid simulation.

The progress will be displayed in the status bar. Pressing Esc will pause the simulation.

Once the simulation has been baked, the cache can be deleted by pressing Free Guides. It is possible to pause or resume a Bake Guides process.

---

## Header¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/interface/header.html

**Contents:**
- Header¶

Every constraint has a header at the top:

Show or hide the settings of the constraint. Collapsed constraints remain active.

Icon representing the constraint’s type. If this icon is red, one or more settings are not correctly filled in and the constraint has no effect.

Initially this is simply the constraint type, but it can be customized to something more specific.

Enable or disable the constraint. Disabling a constraint turns off its effects while keeping its settings around for the future.

Another way of disabling a constraint is to set its Influence to zero. Unlike the Enabled setting, this can be animated.

Applies the constraint’s result to the object’s/bone’s own transformation, then deletes the constraint.

Applying a constraint that is not first in the stack will ignore the constraints before it, which may produce undesired results.

Apply Visual Transform to apply the combined result of all constraints without deleting them.

Creates a copy of the constraint just below current one.

Copies the constraint from the Active object to all selected objects.

Moves the constraint to the first or last position in the stack.

Delete the constraint from the stack. Its settings will be lost and it will no longer affect the object/bone.

Drag to move the constraint up or down in the stack. Since the stack is evaluated from top to bottom, moving a constraint can significantly affect the final outcome.

---

## Hide Gesture Tools¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/hide_tools.html

**Contents:**
- Hide Gesture Tools¶
- Box Hide¶
- Lasso Hide¶
- Line Hide¶
- Polyline Hide¶
- Tool Settings¶

Hide gesture tools hide all selected vertices within the selection area and any of their connected edges and faces. Holding Ctrl while performing the selection reveals the vertices, edges, and faces.

Pressing LMB with any of these tools without also dragging reveals all elements of a mesh.

All hide gesture tools can be activated in the Toolbar and are comprised of the following:

Hides vertices and connected edges and faces based on a box gesture.

Hides vertices and connected edges and faces based on a lasso gesture.

Hides vertices and connected edges and faces based on a line gesture.

Toolbar ‣ Polyline Mask

Hides vertices and connected edges and faces based on a polyline gesture.

The Polyline Hide tool does not support showing all vertices via pressing LMB.

Determines whether all vertices inside or outside the selected area should be affected.

All vertices and connected elements inside the selection area will be hidden.

All vertices and connected elements outside the selection area will be hidden.

---

## Individual Origins¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/controls/pivot_point/individual_origins.html

**Contents:**
- Individual Origins¶
- In Object Mode¶
- In Edit Mode¶

Object Mode and Edit Mode

Header ‣ Transform Pivot Point ‣ Individual Origins ()

While the other pivot point modes transform the whole selection around one point, Individual Origins transforms each item around itself.

Each object gets transformed around its origin, which is a point that can be chosen freely and doesn’t have to be in the center. In the example below, the orange rectangle has it in a corner instead.

Rotation around individual origins.¶

The images below compare Individual Origins to Median Point.

Starting situation, rotation around Individual Origins, rotation around Median Point.¶

Starting situation, scaling using Individual Origins, scaling using Median Point.¶

Each selected element is transformed around its own centerpoint.

Starting situation, rotation around Individual Origins, rotation around Median Point.¶

Starting situation, scaling using Individual Origins, scaling using Median Point.¶

When you transform adjacent faces or edges, they are treated as a single element (meaning they don’t become disconnected).

---

## Industry Compatible Keymap¶

**URL:** https://docs.blender.org/manual/en/latest/interface/keymap/industry_compatible.html

**Contents:**
- Industry Compatible Keymap¶
- General¶
- Common Editing Keys¶
- Viewport¶
- Selection¶
- Tools¶
- Edit Mode Tools¶
- Animation¶
- Platform Specific Keys¶
  - macOS¶

While this is not a comprehensive list, this page shows common keys used in the industry compatible keymap.

Switch Selection mode

Quick access (favorites)

Delete the selected item with a confirmation dialog

Delete the selected item without a confirmation dialog

Proportional Editing (a.k.a. Soft Selection)

Front/Side/Top/Camera Viewpoints

Set Location + Rotation + Scale keyframe

The Cmd key can be used instead of Ctrl on macOS for all but a few exceptions which conflict with the operating system.

---

## Info Editor¶

**URL:** https://docs.blender.org/manual/en/latest/editors/info_editor.html

**Contents:**
- Info Editor¶
- Interface¶
  - View Menu¶
  - Info Menu¶

The Info editor logs the executed operators as well as errors, warnings, and informational messages. You can select an entry by clicking it, optionally holding Shift to add it to the existing selection.

Area controls. See the user interface documentation for more information.

Deselects all entries.

Selects non-selected entries and deselects selected ones.

Selects all entries if there are currently no selected ones, and deselects them otherwise.

Lets you drag a box and adds the entries that overlap it to the selection.

Removes the selected entries from the log.

Copies the selected entries to the clipboard.

---

## Input¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/input.html

**Contents:**
- Input¶
- Keyboard¶
- Mouse¶
- Touchpad¶
- Tablet¶
- NDOF¶
  - Advanced¶

In the Input preferences, you can customize how Blender reacts to the mouse and keyboard as well as define your own keymap.

The Numpad keys are used quite often in Blender and are not assigned to the same action as the regular number keys. If you have a keyboard without a Numpad (e.g. on a laptop), you can tell Blender to treat the standard number keys as Numpad keys by checking Emulate Numpad.

For transform mode, default to Advanced Mode, otherwise Simple Mode is used.

Blender can be configured to work with pointing devices which do not have an MMB. The functionality of the three mouse buttons by holding Alt-LMB.

Mouse/Keyboard combinations referenced in this manual can be expressed with the combinations shown in the table. For example:

MMB drag becomes Alt-LMB drag for example.

This option prevents certain features from being accessed, since Alt-LMB is used for some operations.

Modifying multiple items values at once (objects, bones… etc).

Deselecting edge/face rings in Edit Mode.

Detaching node links.

Moving the Compositor background image.

Some touchpads support three-finger tap for middle mouse button, which may be an alternative to using this option.

The modifier key to press to emulate the middle mouse keybindings. This option is unsupported on Microsoft Windows.

Use the Alt key to emulate the middle mouse button.

Use the OSKey to emulate the middle mouse button.

This has the advantage that it doesn’t conflict with existing Alt-MMB shortcuts, noted above.

This feature is used to prevent the problem where an action such as moving objects or panning a view, is limited by your screen bounds.

This is done by warping the mouse within the view.

Cursor warping is only supported by relative input devices (mouse, trackball, trackpad).

Graphics tablets, however, typically use absolute positioning, this feature is disabled when a tablet is being used.

This is detected for each action, so the presence of a tablet will not disable Continuous Grab for mouse cursor input.

Dragging LMB on an object will move it. To confirm this (and other) transform, an LMB is necessary by default. When this option is activated, the release of LMB acts as confirmation of the transform.

The time in milliseconds to trigger a double click.

The number of pixels that a User Interface element has to be moved before it is recognized by Blender, values below this will be detected as click events.

The drag threshold for tablet events.

The drag threshold for non mouse/tablet events (keyboard or NDOF for example).

This affects Pie Menu on Drag keymap preference.

The number of pixels the cursor must be moved before the movement is registered. This is helpful for tablet pens that are a lot more difficult to keep still, then this could help to reduce stuttering of the cursor position.

Unlike the click/drag distinction, this is used to detect small movements for example, picking selection cycles through elements near the cursor. Once the cursor moves past this threshold, selection stops cycling and picks the closest item.

This panel is available on Windows, macOS, and Linux with Wayland.

Use multi-touch gestures for navigation with touchpad, instead of scroll wheel emulation. For more detail on supported gestures, see Configuring Peripherals.

The direction scrolling responds to the scroll gestures.

Only available on Linux using Wayland.

Scrolls content down when gestures move up.

Scrolls content up when gestures move up.

Select the native Windows Ink or older Wintab system for pressure sensitivity. Blender automatically selects the API for your operating system and tablet, however in case of problems this can be set manually. You may need to restart Blender for changes to take affect.

Amount of pressure required to achieve full intensity.

Controls how the softness of the low pressure response onset using a gamma curve.

These preferences control how an NDOF device (3D mouse) interacts with the 3D Viewport. These settings allow customization of navigation, orbit behavior, and motion sensitivity. They can also be accessed using the NDOFMenu button on supported devices, which opens a pop-up menu to adjust them directly in the viewport.

Sets how the 3D mouse navigates in the 3D Viewport.

Feels like holding the object in your hand. Moving the 3D mouse moves the object in that direction.

Moves the camera through the scene, like flying or piloting a helicopter. For example, pushing the 3D mouse up moves the camera up.

Keeps the view level by preventing horizon tilt during navigation.

Automatically determines the rotation center. If the full model is visible, its center of volume is used. When zoomed in, the rotation center shifts to the nearest visible object.

Limits the orbit center to the center of the currently selected objects.

Displays an axis overlay to indicate the current orbit rotation direction.

Displays a marker showing the current orbit center point.

Controls how quickly the view pans in response to NDOF input.

Controls how quickly the view orbits in response to NDOF input.

Sets the minimum threshold for motion detection. Helps avoid unintended movement from slight touches.

Determines which direction on the 3D mouse triggers zooming.

Zooms in or out by pushing or pulling the 3D mouse forward/backward.

Zooms in or out by pushing or pulling the 3D mouse upward/downward.

Inverts panning on the selected X, Y, or Z axis.

Inverts rotation direction on the selected X, Y, or Z axis.

When in camera view, pans or zooms the camera instead of exiting the view during orbiting.

---

## Input Fields¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/buttons/fields.html

**Contents:**
- Input Fields¶
- Text & Search Fields¶
- Number Fields¶
  - Multi-Value Editing¶
  - Value Limits¶
  - Expressions¶
    - Expressions as Drivers¶
  - Units¶
- Color Fields¶

A text and a search field.¶

Text fields show a rounded rectangular border, and optionally an icon and/or text inside the border. Text fields store text strings, and provide the means to edit text by standard text editing shortcuts:

Go to the start of the line.

Go to the end of the line.

Move the cursor a single character.

Ctrl-Left, Ctrl-Right

Move the cursor an entire word.

Ctrl-Backspace, Ctrl-Delete

Select while holding the key and moving the cursor.

Copy the selected text.

Cut the selected text.

Paste text at the cursor position.

For text fields with an icon and pop-ups, see Data ID.

Number fields store values and units.

The first type of number field shows triangles pointing left (<) and right (>) on the sides of the field when mouse pointer is over the field.

Sliders, a second type of number field, have a colored bar in the background to display values over a range, e.g. percentage values.

The value can be edited in several ways:

To change the value in unit steps, click LMB on the small triangles (not available for sliders). You can also use Ctrl-Wheel while hovering over the field to edit the value.

To change the value with the mouse, hold down LMB and drag to left or right.

Hold Ctrl to snap to the discrete steps while dragging or Shift for precision input.

Press LMB or Return to enter value by typing it with keyboard.

When entering values by keyboard, number fields work like text fields:

Press Return or LMB outside the field to apply the change.

Press Esc or RMB to cancel.

Press Tab to jump to the next field or Shift-Tab to go to the previous field.

Press Minus while hovering over a number field to negate the value.

Multi-value editing.¶

You can edit multiple number fields at once by pressing down LMB on the first field, and then dragging vertically over the fields you want to edit. Finally you can either drag left or right to adjust value with the mouse, or release the LMB and type in a value.

Most numerical values are restricted by “soft limit” and “hard limit” value ranges. Changing values by dragging with the mouse is restricted to the “soft limit” value range. Input via keyboard will allow the use of wider value ranges, but never wider than the “hard limit”.

You can enter mathematical expressions into any number field. For example, enter 3*2 or 10/5+4 instead of 6. Even constants like pi (3.142) or functions like sqrt(2) (square root of 2) may be used.

These expressions are evaluated by Python; for all available math expressions see: Math module reference.

You may want your expression to be re-evaluated after it is entered. Blender supports this using Drivers (a feature of the animation system).

Expressions beginning with # have a special use. Instead of evaluating the value and discarding the expression, a driver is added to the property with the expression entered.

The expression #frame is a quick way to map a value to the current frame, but more complex expressions like #fmod(frame, 24) / 24 are also supported.

This is simply a convenient shortcut to add drivers which can also be added via the RMB menu.

As well as expressions, you can specify numbers and units. If no unit is given, then a default unit is applied. The unit system can be changed in scene settings.

You can use either the unit abbreviation or the full name after the value.

Examples of valid usage of length units include:

2.2mm + 5' / 3" - 2yards

Decimal separator is optional.

You can mix units, e.g. metric and imperial even though you can only show one at a time.

Plurals of the names are recognized too, so meter and meters can both be used.

Color fields. With and without alpha.¶

The color field stores a color value. Clicking on it with LMB opens the Color Picker.

Color fields with an alpha channel are divided in half: on the left, the color is shown without an alpha channel, and on the right, it’s shown with an alpha channel over a checker pattern.

Colors can be copied to other color fields by dragging and dropping.

Hovering over a color property will display a large swatch preview of the color and the color’s hexadecimal, RGBA, and HSVA values.

---

## Inspection¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/inspection.html

**Contents:**
- Inspection¶
- Socket Inspection¶
- Attribute Search¶
- Viewer Node¶
- Node Warnings¶
- Node Timings Overlay¶
- Named Attributes Overlay¶
- Geometry Randomization¶

Inspecting intermediate values in a geometry node tree is useful while building/understanding one or when trying to figure out why something is not working. Blender provides multiple tools to understand how a node tree is working or why it is not working.

Generally, the inspection tools display data from the last time the node tree has been evaluated. If it has not been evaluated, no information is available.

Socket inspection shows information about the value in a socket during the last evaluation. For primitive data types such as integers, vectors, and strings the actual value is shown. For geometry sockets only some data about the geometry is stored, including the set of data types the geometry contains, and a count of their elements.

Socket values are only logged from when the node tree was executed, so a node must be connected to the Group Output to have a value for inspection. Values are not logged during rendering, to improve performance.

The attribute search is shown when clicking on an attribute input in the modifier. It contains a list of all the attributes that were available at that point in the modifier or node execution.

The Viewer node is used to display intermediate geometry in the Spreadsheet Editor and the Viewport. For more information see Viewer Node.

When the inputs to a node are invalid, it displays a warning in the title. Hovering over the warning icon shows the error message. These warnings are only generated when the node is executed, so a node must be connected to the Group Output to have a warning.

The node timings overlay.¶

Node timings show how long a node took to execute the last time the node group was evaluated. They can be turned on in the overlays popover on the top right of the node editor. When a node group is used in multiple places, the timings depend on the context of the node editor, which is displayed in the path on the top left.

Frame nodes display the total time from all of the contained nodes and the Group Output node displays the total time for the entire node group.

The displayed timings should only be considered an approximation, since they can also take into account actions like copying or deleting a geometry input that aren’t part of the node’s operation. Also, when a node uses multiple CPU cores, the evaluation system might work on other nodes at the same time. It’s also important to remember that field nodes generally don’t do work by themselves, so their execution time is only added to the data-flow nodes they are connected to.

The “Named Attributes” overlay allows displaying when a custom named attribute is used by a node or a node group. Named attributes can be used by the Capture Attribute Node, the Named Attribute Node, and the Remove Named Attribute Node, and can be written to, read, or removed.

Using named attributes (as opposed to Anonymous Attributes) can be problematic when the original geometry already has attributes with the specified names. In that case a geometry node group might mistakenly overwrite some essential data. The overlay helps to make detecting that situation easy.

The same data is also available in the Named Attributes panel in the modifier’s UI.

Many nodes don’t guarantee the order of elements in which they output things. For example, the order of edges coming out of the Triangulate node is deterministic but not well defined. The order may change between Blender versions. Therefor, if node setups depend on a specific order, they may break when the Blender implementation changes. Changing the order can often be necessary in order to fix bugs or improve performance.

“Geometry randomization” can be temporarily enabled to see if a blend-file depends on the indices in unstable ways. When enabled, various internal algorithms shuffle the result geometry elements so that any dependence on it would not work anymore. When building setups that are supposed to last a long time, it is recommended to check if they still work with randomization enabled.

To enable it, first enable Developer Extras in the preferences. Then search for Set Geometry Randomization. The popup allows enabling and disabling the randomization.

---

## Interface¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/interface.html

**Contents:**
- Interface¶
- Display¶
- Editors¶
  - Temporary Editors¶
  - Status Bar¶
- Language¶
- Accessibility¶
- Text Rendering¶
- Menus¶
  - Open on Mouse Over¶

Interface configuration lets you change how UI elements are displayed and how they react.

Adjusts the size of fonts and buttons relative to the automatically detected DPI. During typical usage, you may prefer to use zoom which is available in many parts of Blender interface.

Scale of lines and points in the interface e.g. button outlines, edges and vertex points in the 3D Viewport.

Display the Splash Screen when starting Blender.

Show settings and menu items which are intended to help developers, this includes:

Sequencer Cache Settings

To open the Python reference manual.

To copy the expression used when pressing the button.

To edit Python source code that defines the button.

The option to edit UI translations (only available when the Manage UI translations add-on is also enabled).

Work in progress features can be enabled here which are currently being tested.

When enabled, a tooltip will appear when your mouse pointer is over a control. This tip explains the function of what is under the pointer, shows the associated hotkey (if any). When disabled, you can still force the tooltip display by holding Alt then hovering the control.

Displays a property’s Python information below the tooltip.

Show most recently selected items at the top of search results, otherwise search results are sorted alphabetically.

This makes regions overlap the viewport. It means that the Toolbar and Sidebar regions, will be displayed overlapping the main area.

Displays small handles in the corners of each Areas. These can be used to split or join areas with a click-and-drag action.

This option is especially useful on touch-enabled devices, where precise right-click or edge selection is more difficult.

When enabled always display arrows in numeric input fields for increasing or decreasing values.

When disabled, arrows are shown when hovering over the property.

Show navigation controls at top right of the area. This impacts the 3D Viewport as well as image spaces.

If you are familiar with navigation key shortcuts, this can be disabled.

Sets the padding around each editor area. A larger value increases the hit zone for area controls, which can improve usability on pen tablets, touch screens, or for users with visual or physical accessibility issues.

Choose which type of Color Space you prefer for the Color picker. It will show when clicking LMB on any color field.

The default header position when opening a new editor.

Uses top for most editor types and the positions saved in the start-up file.

Always positions the header at the top or the bottom of the editor.

How factor value types are displayed in the user interface.

Values are displayed as float numbers between 0.0 and 1.0.

Values are expressed as a percentage between 0 and 100.

When performing certain operations, Blender will open a new window. The behavior of these operations can be configured here.

When rendering, the user interface can do any of:

The user interface does not change and the render is computed in the background.

A new Image editor is opened as a temporary window in full screen mode.

The area that is the largest on screen is replaced placed by a temporary Image editor.

A new Image editor is opened as a regularly sized temporary window.

When opening files from the computer, the user interface can do any of:

A new File Browser editor is opened as a temporary window in full screen mode.

A new File Browser editor is opened as a regularly sized temporary window.

Controls how the User Preferences editor is displayed when opened.

Opens the Preferences as a temporary full-screen editor within the current window.

Opens the Preferences in a new, separate window of regular size.

Preferences that affect the Status Bar.

Shows information about the data in the active scene.

Collection: The name of the active Collection.

Active Object: The name of the active selected object.

Geometry: Information about the current scene depending on the mode and object type. This can be the number of vertices, faces, triangles, or bones.

Objects: The number of selected objects and the total count of objects.

Shows the total amount of time of the playback along with the current frame number and total frame count. The format of the duration text is determined by the Timecode Style.

Shows an estimate of Blender’s RAM consumption. On a single-instance single-machine scenario, this estimate provides a measurement against the hardware limit of the machine.

Shows the number of extensions with available updates.

Shows the version number of Blender that is currently running.

The language used for translating the user interface (UI). The list is broken up into categories determining how complete the translations are.

Translates the descriptions when hovering over UI elements.

Translates all labels in menus, buttons, and panels.

Translates the names of new data-blocks.

Avoids interface animations and motion effects. This option helps reduce visual distractions and can improve comfort for users sensitive to motion or those who prefer a more static interface.

Enable interface text Anti-Aliasing. When disabled, texts are rendered using straight text rendering (filling only absolute pixels).

Render text for optimal horizontal placement.

Adjust font hinting, controls the spacing and crispness of text display.

Replacement for the default user interface font.

Replacement for the default mono-space interface font (used in the Text editor and Python Console).

Close menus when the mouse is moved out of the region.

Select this to have the menu open by placing the mouse pointer over the entry instead of clicking on it.

Time delay in 1/10 second before a menu opens (Open on Mouse Over needs to be enabled).

Same as above for sub menus (for example: File ‣ Open Recent).

Length of animation when opening Pie Menus.

Keystrokes held longer than this will dismiss the menu on release (in 1/100ths of a second).

The window system tries to keep the pie menu within the window borders. Pie menus will use the initial mouse position as center for this amount of time, measured in 1/100ths of a second. This allows for fast dragged selections.

The size of the Pie Menu set with the distance (in pixels) of the menu items from the center of the pie menu.

Distance from center before a selection can be made.

Distance threshold after which selection is made (zero disables).

---

## Interface¶

**URL:** https://docs.blender.org/manual/en/latest/editors/outliner/interface.html

**Contents:**
- Interface¶
- Header¶
  - Display Mode¶
  - Search¶
  - Filter¶
  - Miscellaneous¶
- Main Region¶
  - Object Interaction Mode¶
  - Restriction Toggles¶

This header dropdown lets you choose what the Outliner should show.

Shows the view layers, collections, and objects across all scenes.

Shows the collections and objects in the current view layer of the current scene.

Shows the images and videos that are used in the Video Sequencer.

Lists all data in the current blend-file. On the right side of the list, a shield icon shows the number of users – clicking it adds or removes a fake user.

Lists every data-block in the file along with any properties that it might have.

Shows the library overrides. Separated further into two view modes:

Shows the data-blocks that have overridden properties in a list grouped by type. You can expand each data-block to see and change these properties.

Shows the overridden data-blocks in a tree that visualizes their hierarchy. This includes parent data-blocks that were overridden implicitly. For example, if you created an override for a material, this tree would show the hierarchy object > mesh > material.

This view also shows a column of icons on the right that let you toggle whether each override is editable.

Lists the data-blocks that are unused or only have a fake user. You can add/remove a fake user by clicking the shield icon on the right.

Unused data-blocks are automatically deleted when saving and reloading the file. You can also delete them manually by clicking Purge in the header.

The textbox lets you filter the tree by typing a substring. You can focus it using Ctrl-F or clear it using Alt-F.

The funnel icon in the header offers further control over what is displayed in the editor. Depending on the Display Mode, some options are not available.

Set which Restriction Toggles should be visible.

Sort the entries alphabetically.

Whether to synchronize the Outliner selection to and from the 3D Viewport and Video Sequencer editors.

Show the column for toggling the object interaction mode.

Only show the items whose name fully matches the search text rather than only containing it as a substring.

Take lower/upper case into account when comparing the search text to the item names.

Show all the view layers in the scene instead of only the active one. Combined with disabling the Objects filter, this gives a compact overview of all the collections in relation to the view layers.

Show the collections in the scene hierarchy. Only the collections themselves are hidden when this option is disabled; the objects within them remain visible.

Show the objects in the scene hierarchy. Disabling this gives you an overview of just the collections.

List the objects based on their state or restrictions. The results can be inverted using the Invert toggle button.

Only show the objects that are visible in the 3D Viewport. This takes both the Hide in Viewports and Disable in Viewports settings into account; see Restriction Toggles.

Only show the object(s) that are currently selected in the 3D Viewport.

Only show the active object (typically the one that was selected last).

Only show the objects that can be selected in the 3D Viewport; see Restriction Toggles.

List relevant materials, modifiers, mesh data and so on as children of each object.

Show child objects as child nodes in the Outliner tree. When disabled, child objects are shown as sibling nodes instead (unless they’re in a different collection than their parent, in which case they’re not shown in the parent’s collection at all).

Lets you filter out objects by type.

Shows the data-block properties that are defined/controlled automatically (e.g. to make data-blocks point to overridden data instead of the original). Only available in the Library Overrides Display Mode.

Some options in the header will only show if compatible with the active Display Mode.

Add a new collection inside the selected one.

Restrict the type of the data-blocks shown in the Outliner.

Add/Remove the selected property to/from the active Keying Set.

Add/Remove Drivers to the selected item.

Opens a dialog to remove unused data-blocks from both the current blend-file or any Linked Data (cannot be undone).

Removes unused data-blocks from the current blend-file.

Removes unused data-blocks from Linked Data.

Removes data-blocks only used by unused data-blocks, ensuring that no orphaned data-blocks remain after execution.

Mode icons. Two objects are currently in Edit Mode; a third could be added.¶

If a selected object is in an interaction mode other than the default Object Mode, the Outliner shows an icon representing this mode on the left.

If the active object has such an icon, the Outliner also shows a dot next to objects of the same type. You can click such a dot to switch over to a different object while staying in the same mode.

If the mode supports Multi-Object Editing, you can also click a dot with Ctrl-LMB to add an object to the mode.

You can click the mode icon of the active object to switch it (and any other objects in case of Multi-Object Editing) back to Object Mode. You can also Ctrl-LMB the mode icon of a selected – but not active – object to switch only that object back to Object Mode.

Restriction toggles.¶

The right side of the Outliner shows a series of toggle icons for every collection, object, bone, modifier, and constraint. These can be used to make the item invisible, unselectable, and so on.

Only a few icons are shown by default. You can use the Filter pop-over to show additional ones.

Clicking an icon with Shift-LMB toggles it for the item and all its children.

Clicking a collection’s icon with Ctrl-LMB enables it for the collection (and its parent/child collections) and disables it for all others. Clicking again enables it for the others again.

Toggles the collections inclusion in the current View Layer. When excluded, contents will be hidden in the 3D Viewport, the render, and the Outliner. See Include for more information.

Toggles whether the object or collection can be selected in the 3D Viewport. This can be useful for, say, references images that you only want to display and never select/move.

See more information for:

Toggles the visibility of the object or collection in (only) the 3D Viewport, for the current view layer. The render is not affected.

As an alternative to clicking this icon, you can press H while hovering over the 3D Viewport to hide the selected objects, or Alt-H to unhide all objects.

This setting only applies within the current blend-file: when you Link or Append it to another blend-file, all collections and objects will be visible there.

Objects hidden this way are still part of the view layer, so they still get evaluated and affect playback performance.

Collections can be hidden for individual 3D Viewports; see Local Collections in the Sidebar.

Toggles the visibility of the object or collection in (only) the 3D Viewport, for all view layers. The render is not affected.

This setting is separate from Hide in Viewports. An object needs to have both settings enabled to be visible. You can use this one for “long-term invisibility,” keeping an object invisible even after pressing Alt-H.

This setting carries over to other blend-files when linking or appending.

Objects hidden this way are no longer part of the view layer, so they no longer get evaluated and don’t affect playback performance.

Toggles the visibility of the object or collection in (only) the render, for all view layers. The 3D Viewport is not affected.

This is typically used for supporting objects that help modeling and animation yet don’t belong in the final image.

Toggles the collection’s Holdout property, which makes the objects in the collection cut a fully transparent hole into the render output of the view layer.

Toggles the collection’s Indirect Only property, Objects inside this collection will only contribute to the final image indirectly through shadows and reflections.

---

## Interpolate¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/interpolate.html

**Contents:**
- Interpolate¶
- Usage¶
- Tool Settings¶

Toolbar ‣ Interpolate

The Interpolate tool creates an in-between keyframe by interpolating strokes between the previous and next Grease Pencil keyframes. When used on a frame between two keyframes, clicking and dragging will add a new breakdown keyframe, interpolating the stroke’s shape based on the drag distance.

This allows artists to manually control how strokes evolve between poses or drawings, providing fine control over the interpolation result.

When interpolating between curves of different types, a priority system determines which curve type is used. The priority from highest to lowest is: NURBS –> Bézier –> Catmull-Rom –> Polyline.

Place the timeline playhead between two existing Grease Pencil keyframes.

In the 3D Viewport, click and drag left to right to set the desired interpolation factor.

Release the mouse button to confirm and create a new breakdown keyframe.

The resulting keyframe contains strokes that are interpolated between the neighboring keyframes according to the chosen factor.

Restrict interpolation to either the Active Layer or All Layers.

When enabled, only selected strokes will be interpolated.

Exclude existing Breakdown keyframes from being used as interpolation extremes.

Reverses the interpolation direction, swapping the start and end strokes. Automatic mode attempts to determine the correct direction for each stroke automatically.

The amount of smoothing applied to interpolated strokes to reduce jitter or visual noise.

The number of times smoothing is applied to newly created strokes. Higher values result in smoother interpolation but may reduce shape fidelity.

---

## Is Spline Cyclic Node¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/curve/read/is_spline_cyclic.html

**Contents:**
- Is Spline Cyclic Node¶
- Inputs¶
- Outputs¶

The Is Spline Cyclic controls whether each of the curve splines start and endpoints form a connection. Its output corresponds to the built-in cyclic attribute on the curve spline domain.

The node to set this data is the Set Spline Cyclic Node.

This node has no inputs.

Whether the spline is cyclic.

---

## Join Bundle Node¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/types/utilities/bundles/join_bundle.html

**Contents:**
- Join Bundle Node¶
- Inputs¶
- Outputs¶

The Join Bundle node combines multiple bundles into a single output bundle. Each connected input bundle is merged together, producing one bundle that contains all items from the inputs.

One or more input bundles to combine. Each bundle’s contents are merged by name into the output bundle.

If multiple bundles contain sockets with the same name (duplicate keys), the value from the first occurrence is used. An information icon in the node header will indicate if duplicate keys are detected.

The resulting bundle that contains all items from the input bundles.

Use the Separate Bundle Node to access individual items from the combined bundle if needed.

---

## Keymap¶

**URL:** https://docs.blender.org/manual/en/latest/interface/keymap/index.html

**Contents:**
- Keymap¶
- Conventions Used in This Manual¶
  - Keyboard¶
  - Mouse¶
- Built-in Keymaps¶
- Customizing¶

Hotkeys are shown in this manual as they appear on a keyboard. For example:

The “G” key by itself (as though you were typing a lowercase “g”).

Keys pressed simultaneously.

The number keys on the row above the letters.

Numpad0 to Numpad9, NumpadPlus

The keys on the separate numeric keypad.

Other keys are referred to by name, such as Esc, Tab, and F1 through F12. Arrow keys are written as Left, Right, and so on.

Mouse buttons and wheel actions are referred to as:

Wheel, WheelUp, WheelDown

Scrolling the mouse wheel.

Blender provides two default keymaps:

The default keymap, used throughout this manual.

A keymap that more closely matches the shortcuts of other 3D editing applications.

You can customize keyboard and mouse shortcuts in the Preferences.

---

## Keymap¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/keymap.html

**Contents:**
- Keymap¶
- Presets¶
- Filtering¶
- Preferences¶
  - 3D Viewport¶
  - File Browser¶
- Editor¶
  - Restoring¶
- Known Limitations¶
  - Blender Versions¶

On this screen, you can configure keyboard and mouse shortcuts.

Blender Preferences Keymap section.¶

At the top of the window, you can select and manage presets.

The selector lets you choose from builtin presets:

Blender: the default keymap, which is the one used throughout this manual.

Blender 27x: legacy keymap as used in Blender 2.79 and before.

Industry Compatible: a keymap which more closely matches other 3D editing applications.

Add a custom keymap configuration.

Remove a custom keymap configuration.

Opens a File Browser to select a .py file containing a custom preset.

Saves the current keymap configuration as a preset others may use.

When disabled, only the shortcut assignments that have been modified will be exported. This exported file may be thought of as a “keymap delta” instead of a full export.

When enabled, the entire keymap is written.

Below the preset list, you can filter the list of operations so you can quickly find the one you need.

Filter the operations by their name (such as New File).

Filter the operations by their currently assigned shortcut (such as ctrl n).

The text to search (leave blank to show all operations).

These preferences only apply to the Blender keymap.

Controls which mouse button is used to select items.

LMB selects items while RMB opens the context menu.

RMB selects items while LMB places the 3D Cursor.

Controls the action of Spacebar.

Starts/stops animation playback. This option is good for animation or video editing work.

Opens the Toolbar underneath the cursor to quickly change the active tool. This option is good if you are doing a lot of modeling or rigging work.

You can select tools in multiple ways:

Press Spacebar, then click a tool with the mouse.

Hold Spacebar, move the mouse to a tool, and release Spacebar.

Press Spacebar, then press the key that’s shown in the popover (e.g. T for the Transform tool).

Press Spacebar and the tool’s key together, e.g. Spacebar-T to select the Transform tool in one go.

Opens up the Menu Search. This option is good for someone who is new to Blender and is unfamiliar with the menus and shortcuts. Even if you don’t select this option, however, you can still access the search with F3.

If you select something other than Play, you can instead use Shift-Spacebar to start/stop playback.

The activation event for gizmos that support drag motion. This option is only available when Select with Mouse Button is set to Left.

The gizmo’s operation gets initiated (and additional options become available in the Status Bar) the moment you press down the mouse button on the gizmo.

The operation only gets initiated once you start dragging the gizmo.

Determines the behavior of tool activation keyboard shortcuts.

The tool is immediately in use. For example, if you press Ctrl-B while editing a mesh, this will immediately initiate a Bevel: you can move the mouse to change the size and then click LMB to confirm.

The tool is only selected (same behavior as if you were to click on it in the Toolbar). For example, if you press Ctrl-B while editing a mesh, the Bevel tool will be selected and the gizmo will become visible in the viewport; to actually perform a bevel, you then need to drag this gizmo.

Tapping Alt shows a prompt in the status bar prompting a second keystroke to activate the tool. Note that this option is not available when using Emulate 3 Button Mouse.

Hold Alt to use the Active Tool when the gizmo would normally be required. (For example, with the Move tool selected, you can hold Alt and drag the mouse anywhere in the viewport to move the selected object, rather than having to drag its gizmo.) This option is only available when Select with Mouse Button is set to Left and Emulate 3 Button Mouse is disabled.

Causes the Select All shortcut A to deselect all when any selection exists.

N opens a pie menu to toggle Regions rather than always toggling the Sidebar region.

Viewpoint pie menu, useful on systems without a numeric keypad.

Transform gizmos pie menu, useful for quickly switching between transform gizmos. Note that this doesn’t apply to tools that force a certain gizmo (Move, Rotate, Scale and Transform); if you have such a tool selected, the gizmo will stay the same no matter what you choose in the pie menu.

The action when MMB dragging in the viewport. This also applies to trackpads.

Orbits the view around a central point. Shift-MMB is used for panning.

Pans the view. Shift-MMB is used for orbiting.

How to determine the new viewpoint when dragging Alt-MMB in the viewport.

The new viewpoint depends on both the mouse movement direction and the current viewpoint. For example, dragging the mouse horizontally rotates the viewpoint 90° around the view’s current vertical axis.

The new viewpoint only depends on the mouse movement direction. For example, dragging the mouse to the right always puts the viewpoint on the positive side of the global X axis.

By default, Tab toggles Edit Mode and Ctrl-Tab opens a pie menu for selecting from all modes. This option flips these two shortcuts around.

When enabled, certain keys get different behavior when tapped and show a pie menu when holding them and dragging the mouse.

Show Object Mode pie menu.

Toggle wireframe view.

Show Viewport Shading pie menu.

Start first person Fly/Walk Navigation.

Show viewpoint pie menu.

Show additional items in the shading menu (Z key).

Requires additionally holding Alt to navigate the view while transforming something. In return, you don’t need to hold Alt to perform certain other operations.

As an example: if this option is disabled, dragging MMB always orbits the view, and when you’re moving an object, you can drag with Alt-MMB to lock the movement to an axis. If this option is enabled, these shortcuts get inverted while moving: MMB does the axis lock, and you need to use Alt-MMB to orbit, Shift-Alt-MMB to pan, and Alt-Wheel to zoom.

This also applies to Proportional Editing (where Wheel controls the size of the influence area) and Auto IK (where Wheel controls the length of the temporary IK chain). If the option is disabled, Wheel will zoom the view instead, and you need to use Alt-Wheel to change these properties.

Navigate into folders by clicking on them once instead of twice.

The Keymap editor lets you change the default hotkeys for each of Blender’s editors.

Find the operation whose shortcut you want to change. Filtering can help with this.

Select whether the operation should be triggered by a keyboard key, a mouse button, or something else.

Click the button on the right and press the shortcut you want to assign.

Uncheck the checkbox to disable this keymap item.

Single hotkey or key combination.

Actions from mouse buttons, tablet or touchpad input.

Movement or button from a 3D mouse (NDOF) device.

Mouse click and drag (optionally map drag direction to different actions).

Use this function by entering a text.

For Blender internal use.

The identifier for the operator to call.

See bpy.ops for a list of operators (remove the bpy. prefix for the identifier).

The key or button that activates this keymap item (depending on the map type).

The action (such as press, release, click, drag, etc.), (depending on the map type).

Additional keys to hold (such as Ctrl, Shift, Alt).

Initial values for the operator-specific properties.

Keymap Customization for more information on keymap editing.

If you want to restore the default settings for a keymap, just click on the Restore button at the top right of this keymap.

Instead of changing the default keymap, you can also add a new one.

A problem with modifying your own keymap is that newer Blender versions may change the way tools are accessed, breaking your customized keymap.

While the keymap can be manually updated, the more customizations you make, the higher the chance of conflicts in newer Blender versions is.

---

## Line Project¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/line_project.html

**Contents:**
- Line Project¶
- Usage¶
- Controls¶
- Tool Settings¶

Toolbar ‣ Line Project

This tool flattens the geometry along a plane determined by the camera view and a drawn line. The region of the mesh being flattened is visualized by the side of the line that is shaded.

Before Line Project.¶

Orient the 3D Viewport to define the direction in depth.

LMB and hold while moving the cursor to define direction of the line projection.

Adjust the operation with extra Controls shortcuts.

Release LMB to confirm.

Changes the side of the line that the tool projects geometry.

Constrains the rotation of the line to 15 degree intervals.

The affected area will not extend the length of the drawn line. This helps defining a smaller area instead of extending the line infinitely long

---

## Line Tool¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/line.html

**Contents:**
- Line Tool¶
- Tool Settings¶
  - Brush Asset¶
  - Brush Settings¶
  - Color¶
- Usage¶
  - Selecting a Brush and Material¶
  - Creating Lines¶
  - Extruding¶

The Line tool create straight lines using any of the Draw type brushes.

You can configure the brush main settings exposed on the Tool Settings for convenience. For the draw brushes configuration and settings see: Draw Brush.

The number of stroke points between each stroke edge.

Use a curve widget to define the stroke thickness from the start (left) to end (right) of the stroke.

When enabled, the stroke use a curve profile to control the thickness along the line.

Picks the brush asset used by the tool.

See Brush Asset for more information.

See Draw Brushes for a detailed list of all draw brushes and their options.

Parameters to control to look of the stroke.

See Draw Brushes for details.

Settings to determine the color of strokes.

In the Tool Settings select the brush, material and color type to use with the tool. The Line tool uses Draw Brush types. See Brush Settings for more information.

Click (LMB or the Pen tip) and drag the start point.

Release on the desired end point.

After releasing you can move the start and end point by clicking and dragging on the yellow manipulators.

Then confirm (Return/MMB) or cancel (Esc/RMB).

While dragging you can use Shift to snapping the line to horizontal, vertical or 45° angle or use Alt to create the line from a center point.

NumpadPlus and NumpadMinus or using the mouse Wheel will increase or decrease the amount of points in the final line.

F will adjust the line thickness and Shift-F will adjust the opacity of the strokes.

click and dragging the start point.¶

Moving start and end points with manipulators.¶

The line after confirming.¶

Before confirming you can use E to extrude the end point of the line to generate multiple connected lines.

End point extruding.¶

Moving the end point of the last line with the manipulator.¶

The connected lines after confirming.¶

---

## List View¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/templates/list_view.html

**Contents:**
- List View¶

List view with expanded Filtering Options panel.¶

This control is useful for managing lists of items. In addition to the main list, there is a Filtering panel on the bottom (hidden by default) and modification buttons on the right.

To select an item, click LMB on it.

By double-clicking on an item, you can edit its name via a text field. This can also be achieved by clicking it with Ctrl-LMB.

The list view can be resized to show more or fewer items. Hover the mouse over the handle (::::), then click and drag to expand or shrink the list.

Click the Show filtering options button (triangle on bottom left) to show or hide the filter option panel.

Filters the list to only show items containing a certain term.

Toggle between including items that match the search term and those that do not contain the search term.

This button switches between alphabetical and non-alphabetical ordering.

Sort objects in ascending or descending order. This also applies to alphabetical sorting, if selected.

On the right of the list view are list modification buttons:

Removes the selected item.

A menu with operators to edit list entries.

Moves the selected item up/down one position.

---

## Loop Cut¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/tools/loop.html

**Contents:**
- Loop Cut¶
- Usage¶
- Tool Settings¶
- Options¶

The Loop Cut tool is a modal tool version of the Loop Cut and Slide operator. This tool splits a loop of faces by inserting new edge loops intersecting the chosen edge.

The tool is interactive and has two steps:

Pre-Visualizing the Cut

After the tool is activated, move the cursor over a desired edge. The cut to be made is marked with a magenta colored line as you move the mouse over the various edges. The to be created edge loop stops at the poles (triangles and n-gons) where the existing face loop terminates.

Once the desired location of the new edge loop is found, the edge loop can be created via LMB.

Mesh before inserting edge loop.¶

Preview of edge loop location.¶

Interactive placement of edge loop between adjacent loops.¶

Increases and decreases the number of cuts to create. These cuts are uniformly distributed in the original face loop, and you will not be able to control their positions.

Corrects the corresponding UV coordinates, if these exist, to avoid image distortions.

After the modal tool is run the Loop Cut and Slide Options are available in the Adjust Last Operation panel.

---

## Mask by Color¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/mask_by_color.html

**Contents:**
- Mask by Color¶
- Tool Settings¶

Toolbar ‣ Mask by Color

Click on any color on the mesh to create a new mask (based on the active color attribute).

How much changes in color affect the mask generation. A smaller threshold includes fewer similar colors. A larger threshold includes much more similar colors.

Mask only contiguous color areas. Colors that don’t touch the one that you click on will not be masked.

Invert the generated mask.

Preserve previous mask and add or subtract the new one generated by the colors.

---

## Mask Gesture Tools¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/mask_tools.html

**Contents:**
- Mask Gesture Tools¶
- Box Mask¶
- Lasso Mask¶
- Line Mask¶
- Polyline Mask¶
- Tool Settings¶

Mask gesture tools apply a constant value to all selected vertices within the selection area. By default, these tools fully mask each vertex. Holding Ctrl while performing the selection clears the mask.

All mask gesture tools can be activated in the Toolbar and are comprised of the following:

Creates a new Mask based on a box gesture.

Creates a new Mask based on a lasso gesture.

Creates a new Mask based on a line gesture.

Toolbar ‣ Polyline Mask

Creates a new Mask based on a polyline gesture.

Only creates a mask on the faces that face towards the view.

---

## Materials¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/material.html

**Contents:**
- Materials¶
- Smoke Material¶

Realistic smoke can be rendered with the Principled Volume shader.

Smoke Material Example Animation

---

## Median Point¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/controls/pivot_point/median_point.html

**Contents:**
- Median Point¶
- In Object Mode¶
- In Edit Mode¶

Object Mode and Edit Mode

Header ‣ Transform Pivot Point ‣ Median Point ()

Places the pivot point at the averaged-out position of the selected items.

In Object Mode, the Median Point is the averaged-out position of the origins of the selected objects. The shape and size of the objects is not taken into account.

Origins can be chosen freely and can even lie outside their object’s geometry, so that the Median Point is not always what you might expect.

Median points in Object Mode.¶

In Edit Mode, the Median Point is the averaged-out position of the selected vertices. This means that the pivot point will shift towards the area with the densest geometry.

In the example below, the pivot point lies perfectly in the middle if both cubes have the same number of vertices, but heavily leans towards the side if one cube is subdivided – even though both cubes still have the same size.

Median points in Edit Mode.¶

---

## Menus¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/buttons/menus.html

**Contents:**
- Menus¶
- Popup Menus¶
  - Collapsing Menus¶
- Select Menus¶
  - Expanded View¶
- Popover Menus¶
- Context Menu¶
- Pie Menus¶

Blender uses a variety of different menus for accessing options and Operators. Menus can be interacted with in the following ways:

LMB on the desired item.

You can use the number keys or numpad to input an item in the list to select. For example, Numpad1 will select the first item and so on.

If a menu is too large to fit on the screen, a small scrolling triangle appears on the top or bottom. Scrolling is done by moving the mouse above or below this triangle.

Use Wheel while hovering with the mouse.

Arrow keys can be used to navigate.

Each menu item has an underlined character which can be pressed to activate it.

Number keys or numpad can also be used to activate menu items. (1 for the first menu item, 2 for the second etc. For larger menus, Alt-1 activates the 11th and so on, up to Alt-0 for the 20th.)

Press Return to activate the selected menu item.

Press Esc to close the menu without activating any menu item. This can also be done by moving the mouse cursor far away from the menu, or by LMB clicking anywhere outside of it.

Image menu in the Header of the Image editor.¶

Popup menus list Operators which can be executed by selecting with LMB or using the generated shortcut indicated by the underlined character of the operator name. All menu entries show any relevant shortcut keys, which can be executed without opening the menu.

All popup menus can be searched by pressing Spacebar and typing the name of the operator in the menu. If a popup menu has “Search” as one of the items, the menu can be searched without having to press Spacebar first.

All popup menus of an editor can be searched using the Menu Search feature.

Sometimes it’s helpful to gain some extra horizontal space in the header by collapsing menus. This can be accessed from the header context menu: click RMB on the header and uncheck the Show Menus checkbox.

Right-click on any of the header menus.¶

Access the menu from the collapsed icon.¶

The 3D Viewport Mode Select menu.¶

A Select Menu (or “selector”) allows you to choose from a predefined list of options. It appears as a text label and/or icon with a down arrow on the right.

Click with LMB to open the menu and choose an option. The selected option will then appear inside the button. You can also cycle through options without opening the menu by scrolling on top of the button with Ctrl-Wheel.

Some select menus use an expanded layout to show all available options at once. In this view, the active option is highlighted with a colored background.

In certain cases, you can select multiple options by holding Shift and clicking with LMB.

The Transform Orientations popover menu.¶

Popover menus are similar to Select Menus, but can show more varied content such as a title, buttons, sliders, etc.

Context menus are pop-ups that can be opened with RMB. In most editors, it’s also possible to use the Menu key. The contents of the menu depend on the location of the mouse pointer.

When invoked in an editor, the menu contains a list of operators sensitive to the editor’s mode. When invoked over buttons and properties, common options include:

Apply the change to a single value of a set (e.g. only the X coordinate of an object’s Location).

Apply the change to all values in a set (e.g. all coordinates of an object’s Location).

Replaces the current value by the default.

Copies the Python property data path, relative to the data-block. Useful for Python scripting.

Copies the full Python property data path including any needed context information.

Creates a new driver using this property as input, and copies it to the clipboard. Use Paste Driver to add the driver to a different property, or Paste Driver Variables to extend an existing driver with a new input variable.

Copies the property value to the selected object’s corresponding property. A use case is if the Properties context is pinned.

Lets you define a keyboard or mouse shortcut for an operation. To define the shortcut you must first move the mouse cursor over the button that pops up. When “Press a key” appears you must press and/or click the desired shortcut. Press Esc to cancel.

Lets you redefine the shortcut.

Unlinks the existing shortcut.

Opens the containing folder using the operating system’s file manager.

Opens an online page of the Blender Manual in a web browser.

Context-sensitive access to the Python API Reference.

For UI development – Creates a text data-block with the source code associated with the control, in case the control is based on a Python script. In the Text Editor it points at the code line where the element is defined.

For UI development – Points at the translation code line.

A pie menu is a menu whose items are spread radially around the mouse.

The 3D Viewport Mode Pie menu.¶

The fastest way to operate a Pie menu is to press down the key(s) that invoke the menu, move the mouse slightly towards a selection, and release the key(s) to activate the selection.

Releasing the key without moving the mouse will keep the menu open so you can click the desired item. If you do move the mouse before releasing, the item closest to the mouse will be activated instantly.

An open disc widget at the center of the pie menu shows the current direction of the pie menu. The selected item is also highlighted. A pie menu will only have a valid direction for item selection if the mouse is touching or extending beyond the disc widget at the center of the menu.

Pie menu items support key accelerators, which are the letters underlined on each menu item. Number keys can also be used.

If there are sub-pies available, it is indicated by a plus icon.

---

## Mesh¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/domain/liquid/mesh.html

**Contents:**
- Mesh¶

The liquid mesh is, besides the liquid particles, another way to visualize the liquid simulation. It is generated directly from the liquid particles and often uses a higher resolution than the base Resolution Divisions.

Besides enabling parts of the interface, checking Mesh lets the cache know which simulation data to read. If, for example, Mesh is enabled but there is no mesh simulation data to read it will show the original domain. The checkbox does not reset the cache and can be used to switch the view between the original domain and the baked liquid mesh.

It is important to keep in mind that the shape of the mesh depends on a combination of all these parameters. E.g. changing the Particle Radius will lead to a different interpretation of the concavity values.

Factor by which to enhance the resolution of the mesh. The scaling factor is coupled to the Resolution Divisions (i.e. the mesh is this times bigger than the base simulation).

The radius of one liquid particle in grid cells units. This value describes how much area is covered by a particle and thus determines how much area around it can be considered as liquid. A greater radius will let particles cover more area. This will result in meshes covering more volume around liquid particles.

This property refers to the same Particle Radius described in the liquid domain settings. Yet for the mesh, it is useful to interpret the particle radius on its own. For one, the mesh can have a resolution different from the base resolution through the Upres Factor. For another, it is often desirable to be able to control the mesh size around a single liquid particle.

Creates a velocity Attribute which records the velocity of each vertex per frame. These will be used (automatically) when rendering with motion blur enabled.

In order to render motion blur with Cycles, Deformation Motion Blur must be enabled.

Motion blur enabled.¶

Motion blur disabled.¶

The mesh generator method determines the accuracy of the mesh. The Final option produces a higher quality mesh and provides more configuration option than the Preview option which in turn is faster but not as smooth.

Positive mesh smoothing iterations. Higher values will make the mesh outline increasingly smooth. Yet higher values can prevent small details (e.g. smaller liquid drops) from getting meshed.

Negative mesh smoothing iterations. Higher values will make the mesh outline sharper. High values will preserve details, however, the mesh outline will become more ragged (e.g. a single mesh particle will become less rounded and have more flat sides).

Comparison of a liquid drop hitting a surface (viewed from top) with varying smoothing values. Left: 1, 1 (Smoothing Positive, Smoothing Negative). Middle: 10, 1. Right: 1, 10. Note the slightly sharper corners in the right splash (compared to the left one).¶

Upper mesh concavity bound. High values tend to smoothen and fill out concave regions.

Lower mesh concavity bound. High values tend to smoothen and fill out concave regions.

Using a lower concavity which is greater the upper concavity can result in distorted, non-manifold meshes. Unless the artist sees value in this kind of mesh, such concavity value combinations should be avoided.

Upper: 1.0, Lower: 0.0.¶

Upper: 1.0, Lower: 0.5.¶

Upper: 1.0, Lower: 1.0.¶

Upper: 1.5, Lower: 0.0.¶

Upper: 1.5, Lower: 0.5.¶

Upper: 1.5, Lower: 1.0.¶

Upper: 2.0, Lower: 0.0.¶

Upper: 2.0, Lower: 0.5.¶

Upper: 2.0, Lower: 1.0.¶

This option is only available when using the Modular cache type.

The progress will be displayed in the status bar. Pressing Esc will abort the simulation.

Once the simulation has been baked, the cache can be deleted by pressing Free Mesh. It is possible to pause or resume a Bake Mesh process.

---

## Mesh Filter¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/mesh_filter.html

**Contents:**
- Mesh Filter¶
- Tool Settings¶

Toolbar ‣ Mesh Filter

Applies a deformation to all vertices in the mesh at the same time. Masking, auto-masking and visibility will be taken into account.

To use this tool, click and drag away from left to right or from right to left for a negative effect.

These are all of the available filter deformations.

Smooths the positions of the vertices to either polish surfaces or remove volume from larger shapes. Especially useful to fix most of the artifacts of the voxel remesher. This filter works similar to the Smooth brush.

Increases the size of the mesh. This filter works similar to the Scale Transform.

Displaces vertices uniformly along their normal. This filter works similar to the Inflate brush.

Morphs the mesh progressively into a sphere. This filter works similar to the To Sphere Transform.

Randomly moves vertices along the vertex normal. This filter works similar to the Randomize Transform.

Tries to create an even distribution of quads without deforming the volume of the mesh. This filter works the same as holding Shift with the Slide Relax brush.

This will remove the jagged lines visible after drawing or creating a face set. This filter works the same as holding Shift with the Draw Face Set brush.

Eliminates irregularities of the mesh by making the positions of the vertices more uniform while preserving the volume of the object. This filter works similar to the Surface deformation type of the Smooth brush.

How much of the original shape is preserved when smoothing.

How much the position of each individual vertex influences the final result.

Sharpens and smooths the mesh based on its curvature, resulting in pinching hard edges and polishing flat surfaces. Especially useful when sculpting hard surfaces and stylized models with creasing and flattening brushes.

How much smoothing is applied to polished surfaces.

Increases the high frequency surface details of the mesh by intensifying the difference between creases and valleys.

The number of times the smoothing operation is applied per brush step. Controls how much smooth the resulting shape is, ignoring high-frequency details.

Increases the high frequency surface details of the mesh by intensifying the difference between creases and valleys. This filter works similar to the inverted direction of the Smooth brush.

Deletes displacement information of the Multires Modifier, resetting the mesh to a regular subdivision surface result. This can be used to reset parts of the sculpt or to fix reprojection artifacts after applying a Shrinkwrap Modifier.

Negative strokes will intensify the displacement details, this method works similar to Enhance Details and can give better results in some circumstances.

The amount of effect the filter has on the mesh. At certain object scales it can be useful to change this value.

Apply the deformation only on the selected axis.

Orientation of the axis to limit the filter displacement.

Use the local axis to limit the displacement.

Use the global axis to limit the displacement.

Use the view axis to limit the displacement.

---

## Navigating in Paint Modes¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/navigation.html

**Contents:**
- Navigating in Paint Modes¶

There are different preferences for navigating the 3D Viewport in Blender. For painting and sculpting specific workflows it is recommended to use any of the following methods.

Center the View on the surface directly under the mouse position. This way the rotation point of the viewport can be manually changed to any point you wish to orbit around.

Center the View on the average position of the last stroke.

Various preferences can also make navigation more convenient. These can be found in the “Navigation” tab of the preferences.

Tumble the view based on the mouse position in your 3D Viewport while rotating. This makes it very easy to tilt the viewport freely, instead of having the Z axis of the viewport locked.

Use the mouse position to zoom towards and rotate around the surface that is pointed at. This can be an alternative to the repeated manual use of the Center View to Mouse operator.

The disadvantage is that this navigation preference can lead to accidental navigation around backfacing geometry or very distant geometry.

---

## Navigation¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/navigate/navigation.html

**Contents:**
- Navigation¶
- Orbit¶
- Roll¶
- Pan¶
- Zoom In/Out¶
- Zoom Region¶
- Dolly View¶
- Frame All¶
- Frame Selected¶
- Frame Last Stroke¶

View ‣ Navigation ‣ Orbit

MMB, Numpad2, Numpad4, Numpad6, Numpad8.

Rotate the view around the point of interest by clicking and dragging MMB on the viewport’s area.

RMB cancels the orbit operation.

The Alt key has several effects on orbiting:

Clicking a point with Alt-MMB will make it the point of interest: it becomes the central point which the view orbits around.

Holding Alt and then dragging with MMB in a certain direction will align the view to an axis and make it orthographic.

Dragging with MMB and then holding Alt will perform an orbit while also snapping to the world axes, as well as the diagonals between them.

To change the viewing angle in discrete steps, use Numpad8 and Numpad2 to go up and down, or Numpad4 and Numpad6 for left and right. You can also press Numpad9 to switch to the opposite side of the view (rotates the camera 180° around the Z axis).

Orbit Style Preference

Auto-Perspective Preference

View ‣ Navigation ‣ Roll

Shift-Numpad4, Shift-Numpad6

Rotate the viewport camera around its viewing direction in 15° discrete steps by default. See the rotation angle preference to configure.

To reset the roll, you can first align the view to the global X axis using Numpad3, then orbit to get back to the regular perspective view.

RMB cancels the roll operation.

View ‣ Navigation ‣ Pan

Shift-MMB, Ctrl-Numpad2, Ctrl-Numpad4, Ctrl-Numpad6, Ctrl-Numpad8

Pans the 3D Viewport by moving the view left, right, up, or down without rotating it. This is useful for repositioning your view without changing orientation.

Shift-MMB – Pan the view freely by dragging the mouse.

Shift-WheelUp / Shift-WheelDown – Pan the view vertically.

Shift-WheelLeft / Shift-WheelRight – Pan the view horizontally.

Ctrl-Numpad8 / Ctrl-Numpad2 – Pan the view up/down in fixed steps.

Ctrl-Numpad4 / Ctrl-Numpad6 – Pan the view left/right in fixed steps.

View ‣ Navigation ‣ Zoom In/Out

Ctrl-MMB, Wheel, NumpadPlus, NumpadMinus

Moves the view closer to, or further away from, the point of interest. You can zoom in and out by rolling the Wheel or dragging with Ctrl-MMB. To zoom with discrete steps, use the hotkeys NumpadPlus and NumpadMinus.

If you get lost in 3D space (which is not uncommon), Frame All and Frame Selected can be used to show the contents of your scene.

RMB cancels the zoom operation.

View ‣ Navigation ‣ Zoom Region…

The Zoom Region tool allows you to specify a rectangular region by dragging with LMB. The view will then zoom in on this region.

You can also drag with MMB to zoom out instead.

View ‣ Navigation ‣ Dolly View…

In most cases it’s sufficient to zoom the view to get a closer look at something. However, zooming only gets you up to the point of interest and no further. If you hit this point where zooming no longer works, you can instead Dolly by holding Shift-Ctrl and dragging up or down with MMB. This will move the point of interest (and the view along with it).

RMB cancels the dolly operation.

Dolly changes orthographic views to a perspective projection.

This is done because dolly doesn’t work well with an orthographic projection because moving forwards/backwards with an orthographic projection doesn’t have the effect of zooming.

Changes the view so that you can see all objects.

View ‣ Frame Selected

Changes the view so that you can see the selected object(s).

Texture Paint, Vertex Paint, Weight Paint, Sculpt

View ‣ Frame Last Stroke

Centers the view on the region of the last brush stroke.

---

## Navigation¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/navigation.html

**Contents:**
- Navigation¶
- Orbit & Pan¶
- Zoom¶
- Fly & Walk¶
  - Walk¶
  - Gravity¶

Blender Preferences navigation section.¶

Choose your preferred method of interactively rotating the 3D Viewport.

Rotates the view keeping the horizon horizontal.

This behaves like a potter’s wheel or record player where you have two axes of rotation available, and the world seems to have a better definition of what is “Up” and “Down” in it.

The drawback to using the Turntable style is that you lose some flexibility when working with your objects. However, you gain the sense of “Up” and “Down” which can help if you are feeling disoriented.

Is less restrictive, allowing any orientation.

Adjusts the reactivity/speed of orbiting in the 3D Viewport. This setting works differently depending on what Orbit Method is used:

Turntable: Orbit Sensitivity controls the amount of rotation per-pixel to control how fast the 3D Viewport rotates.

Trackball: Orbit Sensitivity as a simple factor for how fast the 3D Viewport rotates.

The selection center becomes the rotation center of the viewport. When there is no selection the last selection will be used.

The method used to calculate the center depends on the current mode:

Object mode uses the selections bounding box center.

Edit & pose mode use the selected elements center.

Paint modes use the center of the last brush stroke.

While this may seem like ideal behavior, it can be inconvenient for larger objects such as a terrain mesh, where the center is not necessarily a point of interest.

When enabled, the view switches to Perspective when orbiting the view, and to Orthographic when aligning to an axis (Top, Side, Front, Back, etc.).

When disabled, this switching needs to be done manually.

Use the depth under the mouse to improve view pan, rotate, zoom functionality. Useful in combination with Zoom To Mouse Position.

Time (in milliseconds) the animation takes when changing views (Top/Side/Front/Camera…). Reduce to zero to remove the animation.

Rotation step size in degrees, when Numpad4, Numpad6, Numpad8, or Numpad2 are used to rotate the 3D Viewport.

Choose your preferred style of zooming in and out, when using interactive zoom.

Scale zooming depends on where you first click in the view. To zoom out, move the cursor to the area center. To zoom in, move the cursor away from the area center.

The Continue zooming option allows you to control the speed (and not the value) of zooming by moving away from the initial cursor position.

Moving up from the initial click point or to the right will zoom out, moving down or to the left will zoom in. The further away you move, the faster the zoom movement will be. The directions can be altered by the Vertical and Horizontal radio buttons and the Invert Zoom Direction option.

Dolly zooming works similarly to Continue zooming except that zoom speed is constant.

The axis of the mouse to use for zooming.

Moving up zooms out and moving down zooms in.

Moving left zooms in and moving right zooms out.

When enabled, the mouse pointer position becomes the focus point of zooming instead of the 2D window center. Helpful to avoid panning if you are frequently zooming in and out.

This is useful in combination with Auto Depth to quickly zoom into the point under the cursor.

Inverts the Zoom direction for Dolly and Continue zooming.

Inverts the direction of the mouse wheel zoom.

The default mode for interactive first person navigation.

See Fly/Walk Navigation.

Inverts the mouse’s Y movement.

Speed factor for when looking around, high values mean faster mouse movement.

Interval of time warp when teleporting in navigation mode.

Base speed for walking and flying.

The multiplication factor for the speed boost.

Simulates the effect of gravity when walking.

The distance from the ground floor to the camera when walking.

The maximum height of a jump.

---

## Nodes¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/index.html

**Contents:**
- Nodes¶

Blender contains different node-based editors with different purposes, so this section only explains how to work with nodes in general. The list below shows the different types of nodes and where they’re documented.

Example of a node editor.¶

Used for procedural modeling.

Used to create materials for objects.

Used to edit rendered images.

Used to create custom textures.

---

## Node-Based Tools¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/tools.html

**Contents:**
- Node-Based Tools¶
- Tool Context¶
- Asset¶
- Tool Settings¶
- Supported Modes & Object Types¶
- Tool-specific Nodes¶
- Non-supported Nodes¶

Geometry node groups can not just be applied to an object using a modifier. It’s also possible to turn them into tools that can be invoked from the Blender menu.

You can create such tools in the Tool Context, after which they appear in the Non-Assets menu of the 3D Viewport. If you want to move them to a different menu, reuse them in other blend-files, or share them with someone else, you need to turn them into an asset as described below.

Node group tools integrated in the Curves menu.¶

Because tool node groups have different settings than modifier node groups, you need to change the Node Tree Sub-Type in the Geometry Node Editor’s header to Tool in order to edit them.

When this type is selected, the data-block menu in the editor’s header will only show the node groups that have the Tool Usage enabled.

If you create a new node group while in the Tool editor type, the Tool Usage will be enabled automatically.

If you want to convert an existing modifier node group, you need to manually enable the Tool Usage in the Sidebar (and optionally disable the Modifier Usage) before switching to the Tool editor type. Also make sure to set up the Supported Modes & Object Types.

The inspection features are not supported in the Tool context.

If you want to move a tool into a menu of your choice, reuse it in other blend-files, or share it with other people, you need to turn it into an asset. Simply right-click the node group name in the Geometry Node Editor’s header and choose Mark as Asset.

Once this is done, the node group will appear in the Asset Browser’s Unassigned catalog. You can then move it into a catalog named after a menu to make it appear at the end of that menu.

Finally, you can save the blend-file as an asset bundle and copy it into an asset library (described on linked page). From then on, the tool will be available in any blend-file you work with. You can also share the asset bundle file with others.

If your tool requires any input from the user apart from the geometry to transform, you can add sockets to the Group Input node. These will be exposed in the Adjust Last Operation panel when running the tool.

Node groups must specify which modes and object types they support. This can be configured using the popover menus in the header of the Geometry Node Editor.

For mesh objects, shape keys are not supported. They will be removed if you run a node tool on the object.

The following nodes are only supported in the Tool context:

Viewport Transform Node

The Self Object node returns the Active object when inside a Tool node group.

These nodes are only supported in the Modifier context:

---

## Node Bundles¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/types/utilities/bundles/index.html

**Contents:**
- Node Bundles¶
- Nodes¶
- Usage¶
- Socket Syncing¶

A bundle is a container that groups multiple values into one socket. This makes it possible to pass many values through a single link, similar to a struct in programming.

Bundles reduce the number of exposed inputs and outputs in a node group, and can contain mixed data types such as geometry, fields, values, objects, or even nested bundles.

A cube and cylinder combined into a bundle, then separated again.¶

The following nodes are provided for working with bundles:

Both nodes allow adding or removing an arbitrary number of sockets, with flexible type support.

Bundles are useful in many workflows:

Simplified interfaces – group inputs into a single socket for clarity.

Physics simulations – package all entities and constraints for a solver.

Declarative systems – store complex structured data for evaluation later.

Texture sets – combine PBR maps (Base Color, Roughness, Normal) into one socket.

Bundles use socket names to match their inputs and outputs. If two bundle nodes are connected but have mismatched signatures, Blender can offer to sync them automatically.

Sync happens automatically when a node is connected for the first time.

Existing sockets are never updated automatically to avoid overwriting data.

A button (Sync Sockets) button appears in the node header when a mismatch is detected, allowing manual synchronization.

---

## Node Closures¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/types/utilities/closure/index.html

**Contents:**
- Node Closures¶
- Overview¶
- Nodes¶
- Socket Syncing¶
- Example¶

A closure allows passing custom functionality into a node group. It acts like a function input, enabling user-defined behavior to be evaluated inside another node tree.

Closures make node groups more flexible and reusable by letting users inject part of a node network into another. This allows building higher-level tools where specific parts of a process can be customized without modifying the group itself.

Using a closure to customize tree scattering within a terrain generator.¶

Closures are a socket type that represent callable node graphs. They define a set of inputs and outputs that can be evaluated inside another node group through the Evaluate Closure node.

When a closure is connected, its internal node graph is injected into the evaluation of the node group where it is used. This allows procedural systems to remain flexible while exposing clear, customizable control points.

Closures can be thought of as function parameters for node groups. They let users define operations that can be executed in a controlled environment defined by the parent node tree.

Closures are created and evaluated with the following nodes:

Closure nodes use socket names to match their inputs and outputs. If two closure nodes are connected but have mismatched signatures, Blender can offer to sync them automatically.

Sync happens automatically when a node is connected for the first time.

Existing sockets are never changed automatically to avoid overwriting user data.

A button (Sync Sockets) button appears in the node header when a mismatch is detected, allowing manual synchronization.

Closures are useful when part of a node group’s logic should be user-defined. For example, a terrain generator can use a closure to define tree placement:

The Evaluate Closure node is placed where tree instances are distributed.

A closure input is exposed on the group’s interface.

A Closure node is connected defining any custom placement logic.

When the closure is evaluated, the contents of the connected node graph are executed inside the context of the terrain generator. This allows the generator to provide stable infrastructure (e.g., scattering, masks, attributes) while users supply their own functional behavior.

A terrain generator node group using closures for custom tree placement.¶

---

## Node Closures¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/utilities/closure/index.html

**Contents:**
- Node Closures¶
- Overview¶
- Nodes¶
- Socket Syncing¶
- Example¶

A closure allows passing custom functionality into a node group. It acts like a function input, enabling user-defined behavior to be evaluated inside another node tree.

Closures make node groups more flexible and reusable by letting users inject part of a node network into another. This allows building higher-level tools where specific parts of a process can be customized without modifying the group itself.

Using a closure to customize tree scattering within a terrain generator.¶

Closures are a socket type that represent callable node graphs. They define a set of inputs and outputs that can be evaluated inside another node group through the Evaluate Closure node.

When a closure is connected, its internal node graph is injected into the evaluation of the node group where it is used. This allows procedural systems to remain flexible while exposing clear, customizable control points.

Closures can be thought of as function parameters for node groups. They let users define operations that can be executed in a controlled environment defined by the parent node tree.

Closures are created and evaluated with the following nodes:

Closure nodes use socket names to match their inputs and outputs. If two closure nodes are connected but have mismatched signatures, Blender can offer to sync them automatically.

Sync happens automatically when a node is connected for the first time.

Existing sockets are never changed automatically to avoid overwriting user data.

A button (Sync Sockets) button appears in the node header when a mismatch is detected, allowing manual synchronization.

Closures are useful when part of a node group’s logic should be user-defined. For example, a terrain generator can use a closure to define tree placement:

The Evaluate Closure node is placed where tree instances are distributed.

A closure input is exposed on the group’s interface.

A Closure node is connected defining any custom placement logic.

When the closure is evaluated, the contents of the connected node graph are executed inside the context of the terrain generator. This allows the generator to provide stable infrastructure (e.g., scattering, masks, attributes) while users supply their own functional behavior.

A terrain generator node group using closures for custom tree placement.¶

---

## Node Editors¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/node_editors.html

**Contents:**
- Node Editors¶
- Header¶
- Overlays¶
- Toolbar¶
- Sidebar¶
  - Node¶
    - Node¶
      - Color¶
    - Properties¶
    - Custom Properties¶

The Header contains various menus, buttons and options, partially based on the current node tree type.

Common node editor header options.¶

This menu changes your view of the editor.

This menu allows you to select a node or groups of nodes.

This menu allows you to add nodes.

This menu allows you to do things with selected nodes.

When enabled, the editor always displays the currently selected node tree, regardless of changes in the active object or scene. This allows you to edit a material, texture, or compositor node tree independently of what is selected in the 3D Viewport or which scene is active. Useful when working across multiple objects or scenes but wanting to keep the editor focused on one specific node tree.

Leaves the current node group and returns to the parent node group/tree.

Change options for snapping node positions to achieve a cleaner node tree layout. See Arranging Nodes.

Overlays are information that is displayed on top of the nodes and node trees. There is a toggle to show or hide all overlays for the node editor next to the overlay popover.

Color node links based on their connected sockets.

Label Reroute Nodes based on the label of connected reroute nodes.

Display breadcrumbs in the upper left corner indicating the hierarchy location of the node tree/group that’s currently being displayed.

Displays Annotations in the preview region.

Display each node’s Preview if the node’s preview is also toggled.

Display each node’s last execution time. This option is only available for compositing and geometry nodes.

In the context of geometry nodes, see Node Timings Overlay.

The Toolbar contains a set of tools that can be used in the node editor.

Select or move nodes and links.

Select nodes or links by dragging a box around them.

Select nodes or links by clicking or dragging with a circular brush.

Select nodes or links by drawing a free-form lasso.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

Delete connections between nodes by drawing a line across the links. See Cut Links for more information.

Mute connections between nodes by drawing a line across the links. Muted links are kept in place but ignored in evaluation. See Mute Links for more information.

Insert a Reroute Node point on links by drawing a line across them. Reroute nodes help organize complex node trees by redirecting connections.

The Sidebar region contains properties for the currently selected node as well as node editor-specific settings.

Node tab with a compositing Render Layers node selected.¶

A unique node identifier inside this node tree.

Nodes can be given a title by modifying the text field.

Controls which warnings in this node will be propagated to the parent node group or modifier. This only exists for Geometry Nodes.

By default, the node’s background color is defined by the user theme. This color can be overridden by selecting a custom color in this panel. Custom node colors can be used to provide a visual cue to help distinguish some nodes from others. The button to the right of the checkbox lets you save colors as presets for reusing later on (much like a palette).

Color of the node background.

This menu contains Operators for working with nodes with custom colors.

Copies the color of the Active node and applies it to all selected nodes.

The properties that are shown depend on the type of node selected, e.g. a Mix node has different properties than a Mask node.

Create and manage your own properties to store data in the active node. See the Custom Properties page for more information.

Sidebar region ‣ Tool

The info in this panel changes with the selected tool.

Sidebar region ‣ View

You can select the Annotate tool in the Toolbar to make annotations in the node editor. See Annotate Tool for more info.

Navigating the node editors is done with the use of both mouse movement and keyboard shortcuts.

Move the view up, down, left and right.

Move the camera forwards and backwards.

Adjusts the zooms to fit only the selected nodes in the view.

Adjusts the zoom to fit all nodes in the view.

Nodes are added via the Add menu in the editor’s header or using a keyboard shortcut.

Nodes can also be added by dragging a connection from an existing node’s input or output socket and dropping the connection above an empty space instead of connecting to another socket. This action will open a search menu with a list of compatible nodes and their sockets that can be added and connected to the existing node. Confirming the menu selection will add the node which can then be moved and placed.

---

## Node Groups¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/groups.html

**Contents:**
- Node Groups¶
- Usage¶
  - Managing Inputs/Outputs¶
  - Reusing Node Groups¶
- Properties¶
  - Group¶
    - Usage Geometry Nodes¶
  - Group Sockets¶
  - Animation¶
- Make Group¶

Example of a node group.¶

Grouping nodes can simplify a node tree by hiding complexity and reusing common functionality. A node group is visually identified by its green title bar.

Conceptually, node groups allow you to treat a set of nodes as a single unit. They are similar to functions in programming: reusable, composable, and parametrizable.

For example, suppose you create a “Wood” material and want to use it in multiple colors. You could duplicate the entire node setup for each color, but maintaining those duplicates would be tedious if you later decide to change the wood grain detail. Instead, you can move the nodes that generate the wood pattern into a node group. Each material can then reuse this group and supply a custom color as input. Any updates to the grain detail need to be made only once—inside the node group.

Node groups can be nested; that is, a group can contain other groups.

Recursive node groups are prohibited to avoid infinite recursion. A group cannot contain itself, directly or indirectly.

Like other data-blocks, node groups with names that start with . are hidden from menus and lists and can only be accessed via search. This is useful for node asset authors who want to hide internal utility groups from end users.

Group Input and Group Output nodes are used to represent data flowing into and out of the group.

The Group Input node provides access to the group’s input sockets from within the node group. These sockets act as parameters that control the behavior of the group from the outside. You can connect them to internal nodes to drive values such as factors, colors, or geometry inputs.

Input values that do not affect the output will be grayed out.

The Group Output node defines the data that is passed out of the node group. Only sockets connected to this node will be available as outputs on the group itself.

Avoid using nodes output nodes such as Material Output inside node groups. These should be used on the top level node tree to improve re-usability of node groups.

Use Group Output to pass data out of a node group.

You can add, remove, and reorder input and output sockets in the Group panel in the Sidebar. New sockets can also be created directly by dragging a link to or from the hollow socket on the Group Input or Group Output node to another socket in the node editor.

Existing node groups can be placed again after they’re initially defined, be it in the same node tree or a different one. It’s also possible to import node groups from a different blend-file using File ‣ Link/Append.

When appending node groups from another blend-file, Blender does not distinguish between types such as material or compositing groups. To avoid confusion, it is recommended to adopt a naming convention, like using prefixes (Mat_, Comp_, Geo_, etc.), to indicate the group’s context.

Sidebar ‣ Group ‣ Group

This panel contains properties that relate the group node such as it’s name and look.

The name of node as displayed in the Title.

The message displayed when hovering over the Title or in add menus.

Color tag of the node group which influences the header color.

The width for newly created group nodes.

Set the width based on the parent group node in the current context

Enables displaying the Manage panel in Geometry Nodes modifiers when creating a modifier from a node group asset.

This panel is only visible in the Geometry Node Editor.

The node group is intended for use with the Geometry Nodes Modifier.

The node group is intended to be used as a tool.

The data-block menu in the header of the Geometry Node Editor only lists the node groups whose Usage matches the current Node Tree Sub-Type.

If you accidentally disable both Usages, the node group will not be accessible through the data-block menu anymore. To make it accessible again, you can add it as a node to a different node group (Add ‣ Group), select that node, and press Tab to enter it. From there, you can enable one of the Usages again.

Sidebar ‣ Group ‣ Group Sockets

The Group Sockets panel.¶

This panel is used to add, remove, reorder, and edit the user interface elements of a node group. It defines how sockets appear on the group node and organizes them for clarity and usability.

Available item types include:

Inputs: Define input sockets for the node group.

Outputs: Define output sockets for the node group.

Group and organize related sockets together. Useful for structuring complex node setups. Panels always appear at the bottom of the node interface. They can be nested by dragging one panel on top of another in the interface item list.

Adds a boolean checkbox to a panel’s header, allowing control over its contents. This option is only available when a panel is selected in the interface item list.

Panel toggles have their own options under the Panel Toggle subpanel. Note that toggle sockets are not listed directly in the interface list—panels with toggles instead show a boolean socket icon next to their name. To make the toggle socket visible again, it must be unlinked from the panel.

A panel toggle does not automatically disable or grey out its sockets. To visually and functionally disable sockets, use a Switch Node or similar logic and disconnect the socket manually.

A UI list view showing all input/output sockets and panels. Each item can be renamed and configured individually. The name appears in the node’s user interface.

Selecting a socket label on the node itself will also select that socket in the Interface Item List.

Duplicates the selected socket or panel.

Converts the selected boolean input into a toggle for its parent panel. Only available when a panel is selected and the active item is a boolean socket.

Removes the toggle relationship between a boolean socket and a panel, making it a regular stand-alone input again.

The properties available for sockets depend on several factors, including whether it is an input or output socket, the data type, and the type of node tree.

The type of Socket generated by this interface item.

The tooltip text displayed when hovering over the socket.

The type of geometry element the attribute corresponds to. See Attribute Domains for a complete list of attribute domains.

The attribute name used by default when the node group is used as a geometry nodes modifier.

Specifies how the data is interpreted and displayed in the user interface. The unit or behavior often depends on the Scene Units.

Standard integer values.

Displayed as a percentage. Typically, Min and Max values are set to 0 and 100.

A percentage or factor between a lower and upper bound.

Standard floating-point values.

Displayed as a percentage. Typically, Min and Max values are set to 0 and 100.

A percentage or factor between a lower and upper bound.

A measurement in degrees or radians, depending on scene units.

Time in frames, converted to seconds based on the scene frame rate.

A spatial distance measurement.

The distance between wave cycles, measured in millimeters (mm), micrometers (µm), nanometers (nm), or picometers (pm).

A temperature value (Kelvin) corresponding to the perceived color of a light source.

A rate of repetition per second (hertz).

Standard vector values.

Displayed as a percentage.

A factor between a lower and upper bound.

A displacement vector.

A geometric direction vector.

Vector representing speed and direction of motion.

Vector representing the change in velocity.

Euler Rotation angles.

Cartesian coordinates. A fourth component (W) may also be supported.

Standard text string.

The string is interpreted as a path to a file.

Sets the number of components for the vector socket: 2, 3, or 4. Changing the dimension affects how the socket is drawn and how data is passed through it.

2D: X and Y components only.

3D: X, Y, and Z components.

4D: X, Y, Z, and W components.

The value used when nothing is connected to the socket.

The minimum and maximum values for the UI control in the node interface.

This does not clamp the actual data flowing through the socket. If a higher value is passed into the socket, it will still be processed unchanged.

Displays the menu in an expanded layout, showing all options at once.

In node editors, only the expanded menu is shown, without a label.

In modifier and operator panels, both the label and the expanded menu are displayed.

The value used when the socket is unconnected. Requires Hide Value to be enabled.

Indicate that the label of this socket is not necessary to understand its meaning. This may result in the label being skipped in some cases.

Hides the socket’s default value control, even when it is not connected.

Takes a Grease Pencil Layer or Layer Group as a selection field.

Hides the input value in the Geometry Nodes modifier interface. This allows the socket to be used inside the node group, but not exposed to the modifier.

Available only for Geometry Nodes input sockets.

Specifies what kind of higher-order data the socket accepts. See Socket Shape for more information.

Automatically detect the most appropriate shape based on how the socket is used. This is the default option and works for most cases.

The socket can adapt to multiple shapes, making it flexible when used with different connections. Useful for generic node groups intended to handle various data types.

Only allows single values (constants) rather than structured data. Fields or grids cannot be connected.

The socket expects a field, meaning the value can vary depending on the geometry element or context.

The socket expects a grid data structure, which stores values sampled across a volume or 2D space.

The tooltip text displayed when hovering over the panel’s header.

When enabled, the panel is collapsed by default on new nodes.

Controls animation data for node group properties, including active Actions and their assigned Slot.

See Manually Assigning Actions and Slots for more information.

Creates a new node group that contains all selected nodes.

Group Input and Group Output nodes will be created to represent connections to unselected nodes outside the group. Inputs will be routed to the Group Input and outputs routed to the Group Output.

When grouping a single node, the resulting node group will:

Preserve the interface of the original node, including panels and default values.

Inherit the name of the original node

When grouping multiple nodes, the group is created with inputs and outputs sockets generated from the connections. In this case, a generic name such as “NodeGroup”, “NodeGroup.001”, etc. is used.

Node ‣ Insert Into Group

Moves the selected nodes into the active group node. To use, select a set of nodes, ending with the destination group node, then, running the operation will move those nodes into that group. The moved nodes are collected into a group of their own to preserve their connection context, having their own group input and output nodes. The group’s existing input and output nodes are updated with new sockets, if any, from the new nodes. The node group must be edited to contain a single Group Input and a single Group Output node.

Go to Parent Node Tree

With a node group selected, press Tab to move into it and see its content. Press Tab again (or Ctrl-Tab) to leave the group and go back to its parent, which could be the top-level node tree or another node group. You can refer to the breadcrumbs in the top left corner of the node editor to see where you are in the hierarchy.

Example of an expanded node group.¶

Removes the group and places the individual nodes into your editor workspace. No internal connections are lost, and now you can link internal nodes to other nodes in your workspace.

The Separate operator removes the selected nodes from a node group and places them in the parent node tree. This is useful when nodes need to be edited outside of a group for clarity or reuse.

Duplicates the selected nodes into the parent node tree, while keeping the originals inside the group. This is useful when you want to reuse nodes outside of the group but still preserve the group definition.

Moves the selected nodes to the parent node tree, removing them from the original group. This is useful when simplifying a group or exposing its contents directly.

Node ‣ Join Group Inputs

Merges multiple selected Group Input nodes into one consolidated Group Input node when possible. Existing links are preserved, and duplicate inputs are unified to reduce clutter and simplify the node tree.

This operation is useful for cleaning up node groups that have become disorganized or contain redundant input nodes.

---

## Node Parts¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/parts.html

**Contents:**
- Node Parts¶
- Title¶
  - Preview¶
- Sockets¶
  - Socket Shape¶
  - Inputs¶
  - Outputs¶
  - Conversion¶
- Properties¶

All nodes in Blender are based on a similar construction. This applies to any type of node. These parts include the title, sockets, properties and more.

The title shows the name/type of the node; it can be overridden by changing the node’s Label. On the left side of the title is the collapse toggle which can be used to collapse the node. This can also be done with H.

How a node appears when collapsed.¶

Previews are an overlay that shows a small image above the node displaying the node result. Not all nodes support previews, but the ones that do can be toggled using the / icons in the top right-hand corner of the node next to the title.

Previews can be disabled for the whole node tree by using Previews overlay toggle.

Sockets are input and output values for the node. They appear as little colored circles on either side of the node. Unused sockets can be hidden with Ctrl-H.

Each socket is color-coded depending on what type of data it handles.

Used for shaders in Cycles and EEVEE.

Used in Geometry Nodes.

Used for enum style inputs that show a dropdown menu or radio button in the UI.

Represents a generic bundle of multiple data types. Bundles can contain several values (e.g., geometry, vectors, or colors) grouped together, allowing compact data transfer between nodes.

Used in Shader Nodes and Geometry Nodes for logical or procedural encapsulation. A closure can store and pass groups of node inputs and logic, enabling reusable “callable” node behaviors.

Used to pass a true or false value.

Indicates that the socket accepts/produces color information. The colors may or may not have an alpha component depending on the node tree type.

Indicates that the socket accepts/produces floating-point numbers.

Used to pass an integer value (a number without a fractional component).

Used to pass a text value.

Represents vector data such as coordinates and normals. Vectors can have 2, 3, or 4 components:

2D: Shows and uses only X and Y components.

3D: Includes X, Y, and Z components.

4D: Includes X, Y, Z, and W components.

Indicates a rotation/quaternion.

Indicates a 4×4 matrix of float values, it is often used to represent a Transformation Matrix.

Used to pass a collection data-block.

Used to pass an object data-block.

Used to pass a material data-block.

Used to pass a texture data-block.

Used to pass an image data-block.

Data sockets can have different shapes, indicating the data structure use to transport data. The data structure determines how values are passed and interpreted. More complex structures allow passing multiple values through a single connection.

Automatically detects a good structure type based on how the socket is used.

Socket can work with multiple types of structures.

These sockets expects a single value, they are represented by a circular socket shape.

Represents a value that can vary per element (e.g. per point, edge, or face). You can think of a field as a “value map”, similar to how the brightness of pixels in a grayscale image represents varying values across space.

If a single value is connected to a field socket, it is implicitly broadcast all elements receive the same value.

Fields can have the following appearance:

Diamond: The socket can accept a field input, or it outputs a field. A constant single value can be connected to these sockets, but then the output will often not vary per element.

Diamond with Dot : The socket can be a field, but it is currently a single value. This is helpful because it allows tracking where single values are calculated, instead of a field with many different results. It also means that Socket Inspection will show the value instead of field input names.

Geometry Nodes Fields Documentation

Represents a grid data structure, which stores values sampled across a 2D surface or a 3D volume. Grids can represent data such as image pixels, voxel densities, or other sampled values in space. They allow complex operations where values are distributed continuously across space, rather than being attached to individual geometry elements.

The inputs are located on the bottom left side of the node, and provide the data the node needs to perform its function. Each input socket, except for the green shader input, when disconnected, has a default value which can be edited via a color, numeric, or vector interface input. In the screenshot of the node above, the second color option is set by a color interface input.

Some nodes have special sockets that can accept multiple inputs. These sockets will have an ellipsis shape rather than a circle to indicate their special behavior.

The outputs are located on the top right side of the node, and can be connected to the input of nodes further down the node tree.

Some socket types can be converted to others either implicitly or explicitly. Implicit conversion happens automatically without the need of a conversion node. For example, Float sockets and Color sockets can be linked to each other.

Once a socket conversion is made, data may be lost and cannot be retrieved later down the node tree. Implicit socket conversion can sometimes change the data units as well. When plugging a Value input node into an angle socket, it’ll default to use radians regardless of the scene’s Units. This happens because the Value node has no unit while the angle input does.

Between color and vector – mapping between color channels and vector components.

Between color and float – the color data is converted to its grayscale equivalent.

Color/float/vector to Shader – implicitly converts to color and gives the result of using an Emission node.

Between float and integer – integers simply become floats, floats are truncated.

Between float and vector – when a float becomes a vector the value is used for each component. When a vector becomes a float the average of the components is taken.

Between float and boolean – values greater than 0 are true, true maps to 1, and false maps to 0.

Between rotations and matrices.

Explicit conversion requires the use of a conversion node such as the Shader To RGB Node or the RGB to BW Node node. The Math Node node also contains some functions to convert between degrees and radians.

Many nodes have settings which can affect the way they interact with inputs and outputs. Node settings are located below the outputs and above any inputs.

An example of the controls on the Chroma Key node.¶

---

## Noise¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/domain/gas/noise.html

**Contents:**
- Noise¶

Physics ‣ Fluid ‣ Noise

Adding noise to the gas simulation creates a finer detailed looking simulation on top of the base. This makes it possible to add more details to gases (i.e. fire or smoke or both) without changing the overall fluid motion.

Fluid noise is an implementation of Wavelet Turbulence for Fluid Simulation.

Besides enabling parts of the interface, checking Noise lets the cache know which simulation data to read. If, for example, Noise is enabled but there is no noise simulation data to read it will show an empty domain. The checkbox does not reset the cache and can be used to switch the view between base resolution and noise view.

Factor by which to enhance the resolution of the noise. The scaling factor is coupled to the Resolution Divisions.

Strength of the noise. Higher values result in more turbulent vortices.

Scale of the noise. Greater values result in larger vortices.

Animation time of the noise. This value has an influence on where the noise field is evaluated. It can be used as a seed to give wavelet noise a slightly different look in two domains that are otherwise the same.

Animation Time: 10.0¶

Resolution Divisions and Upres Factor are not equivalent. By using different combinations of these resolution settings, you can obtain a variety of different styles of smoke.

Resolution Divisions: 200, without noise¶

Resolution Divisions: 100, Noise scale: 2.¶

Low division simulations with lots of Upres Factor divisions generally appear smaller in real-world scale and can be used to achieve pyroclastic plumes such as in the following image:

This option is only available when using the Modular cache type.

The progress will be displayed in the status bar. Pressing Esc will pause the simulation.

Once the simulation has been baked, the cache can be deleted by pressing Free Noise. It is possible to pause or resume a Bake Noise process.

---

## Operators¶

**URL:** https://docs.blender.org/manual/en/latest/interface/operators.html

**Contents:**
- Operators¶
- Operator Properties¶
- Modal Operators¶
  - Slider Operators¶
- Searching for Operators¶
  - Menu Search¶
  - Operator Search¶

Operators execute an action the moment they’re activated, which makes them different from tools (which require some sort of input). Operators can be started from Operator Buttons, Popup Menus, or Menu Search. Examples of operators include adding a new object, deleting it, or setting its shading to smooth.

Most operators have properties that can be adjusted to refine their result. First run the operator (which will use its default settings), then adjust the properties in the Adjust Last Operation region.

Modal operators exist as a concept in between Tools and regular operators. They require some sort of interactive input.

Cancels a modal operator.

Confirms the action of a modal operator.

Slider operators are used to interactively adjust a percentage value in the editor’s Header.

You can adjust the percentage by dragging the slider left or right. This can be made coarser (snapping in 10% increments) by holding Ctrl and more precise by holding Shift. For some sliders, you can toggle “overshoot” with E, which lets you go beyond the 0-100% range.

The Menu Search pop-up lets you search Blender’s interface for a certain operator and execute it. First narrow down the list by typing (part of) the operator’s name, then either click the operator with LMB, or navigate to it with Down and Up and activate it with Return.

Apart from the operator names, the pop-up also shows the menus where they’re located.

The Menu Search pop-up.¶

The Spacebar Action option in the Preferences.

Edit ‣ Operator Search

When Developer Extras are activated, the Operator Search can be accessed from the Edit menu in the Topbar. This menu searches all Operators within Blender, even if they are not exposed in a menu. This is useful for Python developers for testing purposes. Blender might also include a few advanced operators that are not exposed in a menu and can only be accessed via this search menu.

The User Preferences has an option to change how the search results are scored.

---

## Particles¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/domain/liquid/particles.html

**Contents:**
- Particles¶

Enabling a secondary particle type will also create a particle system for that type of particle. Disabling a particle type will delete this particle system including its settings. These particle systems are not part of the mesh generation. They will need to have geometry assigned in order to be rendered.

Create spray particles during the secondary particle simulation. Spray particles are those that appear to fly through the air above the liquid surface when there is a bigger splash.

Create foam particles during the secondary particle simulation. Foam particles are those that solely move on the liquid surface.

Create bubble particles during the secondary particle simulation. Bubble particles are those that move below the liquid surface.

Select particle types that should go into the same particle system. This option has no effect on the outcome of the simulation. It only changes the way particle systems are allocated in the particle settings.

Factor by which to enhance the resolution of the particle simulation. The scaling factor is coupled to the Resolution Divisions (i.e. the particle simulation is this times bigger than the base simulation).

Upper clamping threshold for marking fluid cells as wave crests. A higher value results in less marked cells.

Lower clamping threshold for marking fluid cells as wave crests. A lower value results in more marked cells.

Upper clamping threshold for marking fluid cells where air is trapped. A higher value results in less marked cells.

Lower clamping threshold for marking fluid cells where air is trapped. A lower value results in more marked cells.

Upper clamping threshold that indicates the fluid speed where cells start to emit particles. A higher value results in generally less particles.

Lower clamping threshold that indicates the fluid speed where cells start to emit particles. A lower value results in generally more particles.

Radius to compute potential for each cell. Higher values are slower but create smoother potential grids.

Radius to compute position update for each particle. Higher values are slower but particles move less chaotic.

Maximum number of particles generated per wave crest cell per frame.

Maximum number of particles generated per trapped air cell per frame.

Highest possible particle lifetime.

Lowest possible particle lifetime.

Amount of buoyancy force that rises bubbles. A high value results in bubble movement mainly upwards.

Amount of drag force that moves bubbles along with the fluid. A high value results in bubble movement mainly along with the fluid.

Delete secondary particles that are inside obstacles or left the domain.

Push secondary particles that left the domain back into the domain.

This option is only available when using the Modular cache type.

The progress will be displayed in the status bar. Pressing Esc will pause the simulation.

Once the simulation has been baked, the cache can be deleted by pressing Free Particles. It is possible to pause or resume a Bake Particles process.

---

## Pen¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/edit/tools/pen.html

**Contents:**
- Pen¶
- Usage¶
- Hotkeys¶
- Tool Settings¶

The Pen tool allows you to construct and edit Bézier curves.

LMB click to add a new point connected to the currently selected point. The new point will have handle type of Vector. Shift-LMB click will add point as type Auto. However, the handle type switches to Align when handles are moved (See Move Point).

Ctrl-LMB click on an existing point to delete it.

Ctrl-LMB click on a Curve Segment to insert a new control point between the two adjacent control points. Ctrl-LMB click and drag to control the handles of the inserted points.

LMB drag on a segment in between two control points to adjust the handles, changing the shape of the curve without affecting the location of any control points.

LMB click to select a single point or handle at a time.

LMB drag to move existing points or handles. With an endpoint of a stroke selected, click and drag on empty space to Extrude Point and move the handle at the same time.

Make the stroke Cyclic by clicking the endpoints.

Double LMB click on the control point to cycle through all handle types.

Hold LeftCtrl while dragging a handle to switch between Free and Align handle types. Can be used to create sharp corners along the curve.

Hold LeftAlt while dragging a handle to move the entire point.

Hold LeftShift while dragging a handle to limit the movement of the handle to multiples 45 degrees, so the handle can only be vertical, horizontal or diagonal.

Control newly added point’s radius.

The Stroke Placement of newly added points.

The Drawing Planes of newly added points.

---

## Pinch¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/uv/tools/pinch.html

**Contents:**
- Pinch¶
- Tool Settings¶

The Pinch tool moves UVs toward the brush’s center. The pinch tool can be inverted by pressing Ctrl-LMB.

This option controls the radius of the brush, measured in pixels. F allows you to change the brush size interactively by dragging the mouse and then LMB. Typing a number then enter while using F allows you to enter the size numerically.

Controls how much each application of the brush affects the UVs. You can change the brush strength interactively by pressing Shift-F in the 3D Viewport and then moving the brush and then LMB. You can enter the size numerically also while in Shift-F sizing.

The Falloff allows you to control the Strength falloff of the brush. The falloff is mapped from the center of the brush (left part of the curve) towards its borders (right part of the curve). Changing the shape of the curve will make the brush softer or harder. Read more about using the Curve Widget.

You can choose how the strength of the falloff is determined from the center of the brush to the borders by manually manipulating the control points within the curve widget. There are also a couple of preset custom curves displayed at the bottom of the curve widget that can be used on their own or as a starting point for tweaking.

The center strength, the border strength, and the falloff transition between them are evenly distributed.

Similar to Smooth but produces a wider center point of the brush before tapering off.

The strength of the brush is predominately at its strongest point with a steep falloff near the border of the brush.

Similar to a Sphere but the center is a more concentrated point.

The center of the brush is the strongest point then exponentially tapers off to a lower strength, creating a fine point.

With the center being the strongest, the strength will consistently weaken as it reaches the border of the brush.

Similar to Sharp but the center point is more condensed.

A hybrid between Smooth and Sphere.

The strength of the brush remains unified across the entire brush. This will create a sharp edge at the border of the brush.

Locks the boundary of UV islands from being affected by the brush. This is useful to preserve the shape of UV islands.

To edit all islands and not only the island nearest to the brush center when the sculpt stroke was started.

---

## Pivot Point¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/preview/controls/pivot_point.html

**Contents:**
- Pivot Point¶

The Pivot Point is the point around which images are rotated and scaled. It’s indicated by the position of the selected tool’s gizmo.

The Transform Pivot Point of the 3D Viewport

Use the center of the rectangle that’s wrapped as tightly as possible around the selected images’ origin points.

Use the averaged-out position of the selected images’ origin points.

Use the location of the 2D Cursor, for when you want to specify the pivot point by hand.

Rotate/scale each image around its own origin, rather than rotating/scaling all of them around the same single point like the other options do.

---

## Point Cloud Properties¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/point_cloud/properties.html

**Contents:**
- Point Cloud Properties¶
- Attributes¶
  - Attribute Types¶
- Custom Properties¶

The Attributes panel displays the available data fields associated with each point in the point cloud. These attributes define characteristics like point position, size, color, and motion.

Use the List View interface to browse, create, edit, or remove attributes.

The following are common built-in attributes supported by point cloud objects:

For more attribute types used across Blender’s geometry system, refer to Built-In Attributes.

Stores the 3D coordinates of each point in the object’s local space.

Defines the visual radius (size) of each point when rendered or displayed.

The display color of the point. Used in viewport rendering or shading.

A unique identifier assigned to each point. Useful for persistent referencing.

Indicates the directional movement and speed of the point (e.g., for simulations or motion blur).

Custom attribute can be given to particles to hold a custom characteristic.

The name of the attribute.

The type of data to store in the attribute.

3D vector with floating-point values

RGBA color with floating-point precision

RGBA color with 8-bit precision

The type of element the attribute is stored in. Currently, attributes can only be stored per Point.

Custom properties can also be assigned to point cloud objects themselves. These properties are stored at the object level and not per point.

See the Custom Properties documentation for more information on how to add and use them.

---

## Polyline Tool¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/polyline.html

**Contents:**
- Polyline Tool¶
- Tool Settings¶
  - Brush Asset¶
  - Brush Settings¶
  - Color¶
- Usage¶
  - Selecting a Brush and Material¶
  - Creating Polylines¶

The Polyline tool creates multiple straight lines using any of the Draw type brushes.

You can configure the brush main settings exposed on the Tool Settings for convenience. For the draw brushes configuration and settings see: Draw Brush.

The number of stroke points between each stroke edge.

Use a curve widget to define the stroke thickness from the start (left) to end (right) of the stroke.

When enabled, the stroke use a curve profile to control the thickness along the line.

Picks the brush asset used by the tool.

See Brush Asset for more information.

See Draw Brushes for a detailed list of all draw brushes and their options.

Parameters to control to look of the stroke.

See Draw Brushes for details.

Settings to determine the color of strokes.

In the Tool Settings select the brush, material and color type to use with the tool. The Line tool uses Draw Brush types. See Brush Settings for more information.

Click (LMB or the Pen tip) and drag the start point.

Release on the desired end point.

Click multiple times on different locations to create multiple connected lines.

Then confirm (Return/MMB) or cancel (Esc/RMB).

While dragging you can use Shift to snapping the line to horizontal, vertical or 45° angle.

NumpadPlus and NumpadMinus or using the mouse Wheel will increase or decrease the amount of points in the final line.

F will adjust the line thickness and Shift-F will adjust the opacity of the strokes.

click and dragging the start point.¶

Click multiple times to create multiple connected lines.¶

The polyline after confirming.¶

---

## Poly Build¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/tools/poly_build.html

**Contents:**
- Poly Build¶
- Tool Settings¶
- Controls¶

Poly Build combines several mesh editing tools into one, letting you work more quickly. It’s especially useful for retopology.

When creating a new triangle that shares an edge with an existing one, automatically dissolves this edge so you’re left with a quad.

Creates a new vertex at the mouse cursor, then creates a triangle using this new vertex and the nearest existing edge. If the existing edge already has two neighboring faces, instead creates a new edge using the new vertex and the nearest existing vertex. Holding Ctrl will preview the result in blue.

Dissolves the vertex/deletes the face under the mouse cursor. Holding Shift will highlight the target element in red.

You can move a vertex by dragging it.

You can extrude an edge into a quad by dragging it.

It is useful to enable Snapping and Auto Merge while tweaking vertices to combine them.

---

## Pose Library¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/editing/pose_library.html

**Contents:**
- Pose Library¶
- What is a Pose Asset?¶
- Creating a Pose Library¶
  - Pose Creation¶
  - Pose Creation by Copying from Other File¶
  - Controlling the Look of Preview Images¶
- Modifying a Pose Asset¶
- Using the Pose Library¶
  - Use from the Asset Browser¶
  - Use from 3D Viewport¶

This section describes the pose library, which is based on the Asset Browser. For an overview of the asset system, see the Asset Libraries section. The pose library is meant to be used in Pose Mode. In other words, it only works when posing an armature, and not for general object animation.

The pose library is implemented as an add-on. This add-on is enabled by default; disabling it will remove the pose library from Blender’s user interface.

The “building blocks” of the pose library are actually implemented in Blender itself. The add-on only contains the user interface and the logic that determines what is stored in a pose asset. This was intentionally put into an add-on, so that artists or studios who want to change the behavior can do so with an add-on of their own.

A pose asset is an action that has been marked as asset, and that contains exactly one frame of animation data. Usually these are created via the Create Pose Asset button (see below), but any action that is keyed on exactly one frame can be seen as pose asset.

Each pose in the library is stored in its own action data-block. This means that it can get its own name, its own preview image, and can be organized in Asset Catalogs.

Since a pose asset is just an action, it can also contain slots. That means a single pose asset can contain a pose for more than one armature. When applying the pose, the best matching slot for the given armature will be chosen to read the pose from. If no good match can be found it will fall back to the first slot. For generic pose assets, it is recommended to use single-slot actions. That way Blender always uses the first (and only) slot, regardless of which character the pose is applied to. If a pose is specific to two or more characters, they can be stored in the same asset for convenience. For info on how to create such multi-character pose assets see Pose Creation.

A pose library is a bunch of actions that exist in blend-files of an Asset Library. Such blend-files can either be created manually, or by exporting poses to a library. If a pose asset is created by exporting to a library, a .asset.blend file will be created for it which will contain just that one asset, and which cannot be opened as a normal blend file to modify it. Otherwise there is no restriction on how many pose assets can be contained in a blend-file. It is also possible to link in a character, props, etc., which can then not only be used to create the poses, but also for rendering previews.

Example pose library of the Sprite Fright character Ellie.¶

To create a pose in the library from the Action Editor, pose the character, select the relevant bones, and click the Create Pose Asset button. The same option is available in the 3D Viewport while in Pose Mode under the Pose menu. This will create the new pose action, which will contain keys for the current value of each bone’s location, rotation, scale, and Bendy Bone properties. It doesn’t matter if the character is animated or not, so you can easily create pose assets from existing animation. You can even create a pose asset containing bones of two or more different armatures. To do so, put the armatures in pose mode and select the bones you want to add to the asset. Clicking the Create Pose Asset button will then still create a single action, but with separate slots for each armature.

To create a new pose asset, use the Create Pose Asset button in the Action editor.¶

If the “Current File” library is chosen, the action is created in the current blend file and marked as an Asset. If another library is chosen, the pose is extracted and a new .asset.blend file is created containing the action.

In case the pose asset has been created in the current file, it can be renamed in the Asset Browser. There you can also right click on the thumbnail, then choose Assign Action to assign the action to the active Object (see description above).

The Create Pose Asset button creates a new asset. To make sure that this is actually visible in the user interface, so that you know that something happened, it tries to make sure that the Asset Shelf is visible in the 3D Viewport.

As described in Design Limitations, Blender only writes data to the currently open blend-file or to an .asset.blend file. To copy a pose from some other file into a pose library file, see the following steps:

Pose the character and select the relevant bones.

Click the Copy Pose as Asset button, which is available in the Action Editor. This will create the pose asset (including its thumbnail) and store it in a temporary file somewhere.

Choose an existing pose asset, and open its context menu. Click the Open Blend File option.

A new Blender process will start, and automatically open the asset library file that contains the chosen pose. By the way, this works for all assets, not just poses!

In the Asset Browser, click the Paste as New Asset button. This will load that temporary file, and load all the assets it can find in there. In our case, it will only find a single pose, but future versions of Blender may extend this for other asset types. This is why the button is named so generically – it is not pose-specific.

Give the pose a name, and click on the “refresh” button in the preview image panel to render a new preview if you want.

Save the file and quit Blender.

The original Blender is still running in the background and notices that the new Blender has quit. It automatically refreshes the Asset Browser to show the newly added pose.

The pose library preview images are rendered with the active Scene camera. This approach was preferred over rendering a specific 3D Viewport for two main reasons:

There is only one scene camera active at any time, making it predictable which camera is used.

The camera, as well as the rest of the scene, can be set up specifically for rendering the thumbnails. Pose library files are intended for that purpose: to contain the poses and render their preview images.

The preview images are rendered using the Workbench Engine. Switch the scene to use that as render engine, and you’ll see various options to influence the look. Select a pose asset and press the Generate Preview button to re-render the preview image with the current settings.

You can also animate settings such as MatCap rendering, light positions, and intensities, etc. Use this to your advantage!

A pose asset can be modified after it has been created. This is only possible for pose assets in the current file or that have been exported into an .asset.blend file. For that, an operator has been created which can be accessed by right clicking a pose asset. That operator works on the active object, so updating the asset from selected bones of multiple armatures won’t work. It will find the best matching slot, falling back to the first one. There are 4 modes.

Update existing channels in the pose asset from the selected bones, but don’t remove or add any channels.

Completely replace all channels in the pose asset with the channels of the selected bones.

Add channels of the selected bones to the pose asset. Existing channels will be updated.

Remove channels of the selected bones from the pose asset.

The pose library can be used to pose one or more characters. The current bone selection will be used to determine which bones are modified. When editing multiple armatures at once, a matching slot of the pose asset is determined for each armature. It is possible to either fully apply a pose or blend it into the character’s current pose interactively. How exactly these operations work depends on where you use them. This section will explain the use from both the Asset Browser and the 3D Viewport.

The pose library can be used directly from the Asset Browser. The Pose Library panels will appear when the active object is an armature and in Pose Mode. The catalog system and the filter bar at the top can be used to search for specific poses.

The following operators can be accessed by RMB on a pose:

Applies the pose to the character. If there are any bones selected, the pose will be applied only to those bones. This makes it possible to create a “finger guns” pose by applying a fist pose to the hand, and then an “open hand” pose for only the index finger and thumb. Double-clicking a pose will also apply it.

Will mirror the pose from left to right and vice versa. This makes it possible, for example, to apply a left-hand pose to the right hand, reducing the number of poses you have to put into the library. This can of course also be applied for asymmetrical facial expressions that depend on the camera angle. While blending (see below), keep Ctrl pressed to blend the flipped pose.

Allows you to gradually blend a pose from the library into the character’s pose. Click the button, then move the mouse left/right to determine the desired blend. A pose asset can be “subtracted” while blending. Drag to the right to blend as usual, drag to the left to subtract the pose. While blending, you can use Tab to toggle between the original and the blended pose. As usual in Blender, LMB or press Return to confirm; RMB or press Esc to cancel the operator. Blending can also exaggerate a pose, by pressing E (for Extrapolate) and applying a pose for more than 100%.

Select or deselect the bones that are used in the pose. This can be used to create a selection set, or simply show what was part of the pose and what wasn’t.

The pose library in use from the Asset Shelf.¶

The pose library previously lived in the Sidebar within the Pose Library panel. The panel still exists, but now contains a button to open the asset shelf.

In the 3D viewport, poses can be quickly applied from the Asset Shelf. Contrary to the Asset Browser, the shelf allows you to apply poses quicker.

Click on a pose to apply it. A single click is enough. You can also select and apply a pose via the cursor keys. This allows for fast exploration of the poses, to directly see the result on the active character.

Drag the pose thumbnail left to right to blend it into the character’s current pose. Just release the mouse button to confirm.

---

## Preview Snapping¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/preview/controls/snapping.html

**Contents:**
- Preview Snapping¶

The icon toggles snapping; you can also do this temporarily by holding Ctrl after starting to transform an image.

Images have multiple snap points; they can snap along their edges, corners, or center.

The drop-down arrow offers the following options:

Snap images to the edges of the render region.

Snap images to the horizontal and vertical center lines of the render region.

Snap images to the snap points of other images.

---

## Proportional Editing¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/controls/proportional_editing.html

**Contents:**
- Proportional Editing¶
- Controls¶
  - Proportional Size¶
  - Falloff¶
- Object Mode¶
- Edit Mode¶
  - Options¶
- Example¶

Header ‣ Proportional Editing

Proportional Editing popover.¶

Proportional Editing is a way of transforming selected elements while also affecting the nearby unselected elements. The farther away an unselected element is, the less it will be affected (hence the “proportional”). This feature is very useful for smoothly deforming dense meshes.

Blender also has a Sculpting workflow that contains brushes and tools for proportionally editing a mesh without seeing the individual vertices.

Proportional Editing is off, only selected vertices will be affected.

Vertices other than the selected vertex are affected, within a defined radius.

You can increase or decrease the radius of the tool’s influence during a transform operation from the Proportional Editing popover or with WheelUp/WheelDown, or PageUp/PageDown respectively. As you change the radius, the points surrounding your selection will adjust their positions accordingly.

While editing, you can change the curve profile by either clicking the Falloff icon in the header or pressing Shift-O to get a pie menu.

Constant, No Falloff.¶

Inverse Square Falloff.¶

Proportional Editing is typically used in Edit Mode, but it can also be used in Object Mode. The tool then works on entire objects rather than individual mesh components.

In the image below, the leftmost cylinder is being scaled up vertically, which also affects the cylinders near it.

Proportional Editing in Object Mode.¶

When working with dense geometry, it can become difficult to make subtle adjustments without causing visible lumps and creases in the model’s surface. When you face situations like this, Proportional Editing can help.

Proportional Editing in Edit Mode.¶

Rather than using a radius only, the proportional falloff spreads via connected geometry. This means that you can proportionally edit the vertices in a finger of a hand without affecting the other fingers. While the other vertices are physically close (in 3D space), they are far away following the topological edge connections of the mesh. The icon will have a blue center when Connected is active. This mode is only available in Edit Mode.

Depth along the view is ignored when applying the radius.

The difference between having “Projected from View” disabled (left) and enabled (right).¶

The image below shows the final render of a low-poly landscape obtained by moving up the vertices of a triangulated grid with Proportional Editing enabled.

A landscape obtained via Proportional Editing.¶

---

## Regions¶

**URL:** https://docs.blender.org/manual/en/latest/interface/window_system/regions.html

**Contents:**
- Regions¶
- Main Region¶
- Header¶
  - Context Menu¶
- Toolbar¶
- Tool Settings¶
- Adjust Last Operation¶
- Sidebar¶
- Footer¶
- Arranging¶

Every Editor in Blender is divided into Regions. Regions can have smaller structuring elements like tabs and panels with buttons, controls and widgets placed within them.

The regions of the 3D Viewport showing the Sidebar and the Adjust Last Operation panel after adding a Cube.¶

Header (green), Main region (yellow), Toolbar (blue), Sidebar (red) and Adjust Last Operation panel (pink).

At least one region is always visible. It is called the Main region and is the most prominent part of the editor.

Each editor has a specific purpose, so the main region and the availability of additional regions are different between editors. See specific documentation about each editor in the Editors chapter.

A header is a small horizontal strip, which sits either at the top or bottom of an area. All editors have a header acting as a container for menus and commonly used tools. Menus and buttons will change with the editor type and the selected object and mode.

The Header of the 3D Viewport.¶

RMB on a header reveals a context menu with a couple options:

Toggles the visibility of the header. If a header is hidden, it can be made visible again by clicking or dragging the small arrow that appears at the top/bottom right of the editor.

Toggles the visibility of the Tool Settings.

Toggles whether the Menus are collapsed or not.

Toggles whether the header or Tool Settings appear on the top or bottom of the editor.

Shows an indicator line that lets you select the area and position where to split. Tab switches between vertical/horizontal.

See Duplicate Area into New Window.

Closes the area and replaces it with the expansion of a neighboring area.

The Toolbar (on the left side of the editor area) contains a set of interactive tools. T toggles the visibility of the Toolbar.

A horizontal strip at the top or bottom of the editor (similar to the header) containing settings for the currently selected tool. Just like the header, it can be hidden and moved through its context menu.

Adjust Last Operation is a region that allows tweaking an operator after running it. For example, if you just added a cube, you can use this region to tweak its size.

The Sidebar (on the right side of the editor area) contains Panels with settings of objects within the editor and the editor itself. N toggles the visibility of the Sidebar.

Some editors show a bar (on top/bottom of the editor area) that displays information about for example the active tool or operator.

In animation editors, the footer contains controls and options related to playback, keying, auto keyframing, and transport.

These settings allow you to:

Control how animations are previewed and synchronized with audio.

Insert and manage keyframes through keying sets and auto keying.

Navigate the timeline using playback and transport controls.

Adjust frame ranges and preview specific segments of the animation.

For a detailed description of all properties and controls commonly found in the footer, see the Playback Controls documentation.

A region can be scrolled vertically and/or horizontally by dragging it with the MMB. If the region has no zoom level, it can also be scrolled by using the Wheel while the mouse hovers over it.

Some regions, in particular animation timelines, have scrollbars with added control points to adjust the vertical or horizontal range of the region. These special scrollbars will have added widgets at the ends, as shown in the following image:

Scrollbars with zoom widgets.¶

This can be used to stretch or compress the range to show more or less detail within the available screen space. Simply drag one of the dots to either increase or decrease the displayed range. You can also quickly adjust both the horizontal and vertical range by dragging in the editor with Ctrl-MMB.

Resizing regions works by dragging their border, the same way as Areas.

To hide a region, resize it down to nothing. A hidden region leaves a little arrow sign. LMB on this icon to make the region reappear.

The scale of certain regions (such as the Toolbar) can be changed by dragging inside them with Ctrl-MMB, or using NumpadPlus and NumpadMinus while hovering the mouse cursor over them. Press Home to reset the scale to the default.

The Asset Shelf of the 3D View, showing material assets.¶

To search for assets, hover your mouse over the Asset Shelf, then press Ctrl-F and type a search query. This will filter the poses to match what you typed.

The usage of catalogs as tabs.¶

Catalogs can be shown as individual tabs. Each tab will only show its content, and the content of its children. That makes it easy to filter down to a certain set of assets.

Display options available for the asset shelf.¶

It is possible to change the size of items on the shelf by using the size property.

By toggling on the “Names” checkbox, the asset names will be shown in the shelf. Alternatively it is also possible to hover over an item to show its name.

By default the shelf only has a height for one item row. To allow for more rows, drag it on the upper edge to increase its size.

Only show brushes applicable for the currently active tool in the asset shelf.

The value of this property is stored in the Preferences, which may have to be saved manually if Auto-Save Preferences is disabled.

---

## Relax¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/uv/tools/relax.html

**Contents:**
- Relax¶
- Tool Settings¶

The Relax tool can be used to distribute UVs more evenly. It works by pulling vertices along UV edges to bring the UV unwrap into balance.

The Relax tool can be compared with the Minimize Stretch tool which works directly on faces to reduce texture stretching and shearing. You may find that sometimes minimize stretch works better, sometimes the unwrap tool and other times the Relax tool.

First using Unwrap, then Minimize Stretch and touching up with the Relax tool often gives the best results. Remember, you can use “Undo” at any time to return to an earlier state.

This option controls the radius of the brush, measured in pixels. F allows you to change the brush size interactively by dragging the mouse and then LMB. Typing a number then enter while using F allows you to enter the size numerically.

Controls how much each application of the brush affects the UVs. You can change the strength interactively by pressing Shift-F in the 3D Viewport and then moving the brush and then LMB. You can enter the size numerically also while in Shift-F sizing.

The Falloff allows you to control the Strength falloff of the brush. The falloff is mapped from the center of the brush (left part of the curve) towards its borders (right part of the curve). Changing the shape of the curve will make the brush softer or harder. Read more about using the Curve Widget.

You can choose how the strength of the falloff is determined from the center of the brush to the borders by manually manipulating the control points within the curve widget. There are also a couple of preset custom curves displayed at the bottom of the curve widget that can be used on their own or as a starting point for tweaking.

The center strength, the border strength, and the falloff transition between them are evenly distributed.

Similar to Smooth but produces a wider center point of the brush before tapering off.

The strength of the brush is predominately at its strongest point with a steep falloff near the border of the brush.

Similar to a Sphere but the center is a more concentrated point.

The center of the brush is the strongest point then exponentially tapers off to a lower strength, creating a fine point.

With the center being the strongest, the strength will consistently weaken as it reaches the border of the brush.

Similar to Sharp but the center point is more condensed.

A hybrid between Smooth and Sphere.

The strength of the brush remains unified across the entire brush. This will create a sharp edge at the border of the brush.

Locks the boundary of UV islands from being affected by the brush. This is useful to preserve the shape of UV islands.

To edit all islands and not only the island nearest to the brush center when the sculpt stroke was started.

How to determine the edge weighting:

The classic discrete Laplace operator applied to the UV graph. Each edge has equal weighting, resulting in triangles which resemble a honeycomb shape, or quads aligned into square grid.

Similar to Laplacian, the HC method uses equal weighting while trying to preserve a gradient between dense regions of the mesh and regions with fewer edges.

Note, this method uses the “Humphrey’s Classes” operator as described in the paper: “Improved Laplacian Smoothing of Noisy Surface Meshes”.

Edges are weighted according to the discrete Laplace operator (cotangent formula) applied to the 3D geometry. This tries to bring the relative lengths of edges in UV closer to the relative lengths of edges in 3D, resulting in a UV unwrap with less distortion across edge boundaries.

---

## Remeshing¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/retopology.html

**Contents:**
- Remeshing¶
- Remeshing¶
  - Voxel¶
  - Quad¶
- Retopology¶

Blender offers several tools for regenerating a mesh so that it has (approximately) the same shape but fewer faces, more faces, or better topology.

Remeshing to clean up messy geometry.¶

Object Mode, Sculpt Mode

Properties ‣ Data ‣ Remesh

Remeshing automatically rebuilds the mesh with a uniform topology. You can run it with a high resolution to make a simple mesh denser, making it more suitable for sculpting. Alternatively, you can run it with a low resolution to simplify and clean up overly dense or messy geometry, such as from a sculpt or a 3D scan.

Remeshing only works on the original mesh data – it ignores modifiers, shape keys and so on.

Remeshing is not possible on objects with a Multiresolution Modifier.

The Remesh panel lets you choose between two different modes:

The Voxel remesher works by placing the mesh in a virtual 3D grid, seeing which points of the grid are closest to the mesh’s outer surface, and generating a new mesh with vertices at those points. This means the resulting mesh has uniform topology and has no inner (self-intersecting) geometry.

It’s useful for the following cases:

Changing the resolution of, or generally cleaning up, a mesh that you want to sculpt. Notably, by setting up the resolution before sculpting, you can leave Dyntopo disabled and avoid its performance impact.

Cleaning up a mesh for 3D printing.

Generating a simplified standin mesh for use with physics simulation.

However, because the topology is just a simple grid, the Voxel remesher should not be used for the following:

Creating topology for a mesh that will be deformed (e.g. a character that will be animated). Such topology has to follow the flow of the geometry, and no perfect automatic tools exist for this right now; it has to be done manually. See Retopology.

Generating a mesh for applying the Subdivision Surface Modifier or the Multiresolution Modifier. It’s better to use the Quad mode for this.

Reducing the face count of a mesh that otherwise has no problems with its geometry. It’s better to use Decimate Geometry for this.

Voxel remesh has the following settings:

The size of each voxel (3D grid cell). Use a low value to get a detailed but dense mesh, or a high value for a light but coarse one.

Reduces the final face count by simplifying geometry where detail is not needed. A value greater than zero disables Fix Poles and can introduce triangulation.

Tries to reduce the number of Poles at the cost of some performance, to produce a better topological flow.

Try to preserve the original volume of the mesh. Enabling this could make the operator slower depending on the complexity of the mesh.

Transfer attributes to the new mesh: the paint mask, any face sets, color attributes, and so on.

The Remesh Modifier can perform this operation non-destructively and offers more remeshing methods.

The Quad remesher uses the Quadriflow algorithm, which can produce better results but is also slower. It’s not a replacement for the Voxel remesher, however, because it doesn’t clean up intersecting geometry.

It’s useful for the following cases:

Generating a mesh for applying the Subdivision Surface Modifier or the Multiresolution Modifier.

However, it’s not recommended for the following:

Cleaning up a mesh for sculpting or 3D printing. The Voxel remesher is more suited for this.

Creating final topology for a mesh that will be deformed (e.g. a character that will be animated). Such topology has to follow the flow of the geometry, and no perfect automatic tools exist for this right now; it has to be done manually. See Retopology.

Reducing the face count of a mesh that otherwise has no problems with its geometry. It’s better to use Decimate Geometry for this.

Opens a pop-up to set parameters for the remesh operation.

Generates a symmetrical mesh using the Mesh Symmetry options.

Try to preserve sharp features of the mesh. Enabling this could make the operator slower depending on the complexity of the mesh.

Try to preserve the original volume of the mesh. Enabling this could make the operator slower depending on the complexity of the mesh.

Transfer attributes to the new mesh: the paint mask, any face sets, color attributes, and so on.

Apply Shade Smooth to the new mesh.

How to specify the amount of detail for the new mesh.

Specify target number of faces relative to the current mesh.

Specify target edge length in the new mesh.

Specify target number of faces in the new mesh.

Random Seed to use with the solver; different seeds will cause the remesher to generate different quad layouts on the mesh.

The automatic remesh tools generally don’t result in topology that lends itself to deformation. Therefore, if you have sculpted a character and want to simplify it for animation, you’ll typically have to do this manually in a process known as retopologizing.

To do this, you typically create a new mesh that overlaps the original one, then adjust it until it fully covers the original mesh and matches its shape.

The Retopology overlay of the 3D Viewport is useful here, as it lets you see the original mesh through the retopologized one and vice versa – without getting distracted by geometry on the other side as would be the case with X-Ray.

You can use the Poly Build tool to quickly add, change, and remove faces.

Use Snapping to align new vertices to the original mesh.

---

## Reroute Node¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/types/layout/reroute.html

**Contents:**
- Reroute Node¶
- Properties¶

A node used primarily for organization. Reroute looks and behaves much like a socket on other nodes in that it supports one input connection while allowing multiple output connections.

To quickly add a Reroute node into an existing connection, hold Shift and RMB while sweeping across the link to add a Reroute node.

Input value used for unconnected sockets.

---

## Rip¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/uv/tools/rip.html

**Contents:**
- Rip¶

The Rip tool interactively separates selected UV elements (vertices, edges, or faces) from connected components, creating a “rip” in the UV map. After the separation, the selection can be moved in the direction of the mouse pointer, allowing the detached elements to be repositioned interactively.

This is useful for isolating UV islands or unwrapping overlapping elements without affecting surrounding geometry.

The Rip tool is not compatible with Sync Selection. To use this tool, make sure Sync Selection is disabled in the UV Editor.

UV Rip Move Operator – operator version of the rip operator.

Mesh editing Rip – Similar functionality for mesh editing in the 3D Viewport.

---

## Scale Cage¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/object/tools/scale_cage.html

**Contents:**
- Scale Cage¶
- Tool Settings¶
- Options¶

Object and Edit Modes

Toolbar ‣ Scale ‣ Scale Cage

The Scale Cage tool is a bounding box around the object(s) which scales objects from a particular point or axis. The tool works by selecting a scale point and dragging inwards or outwards to adjust the scale accordingly. The origin for the scale will be from the point on the cube directly opposite from the point selected. Selecting points on the faces of the cube scales along one axis, selecting points on the edges of the cube scales along two axes, and selecting points on the vertices of the cube scales along all three axes.

Aligns the transformation axes to a specified orientation constraint. See Transform Orientations for more information.

The amount to resize the selection on their respected axis.

Aligns the transformation axes to a specified orientation constraint. See Transform Orientations for more information.

The extruded face will affect nearby geometry. See Proportional Editing for a full reference.

---

## Sculpting Tools¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/sculpting/tools.html

**Contents:**
- Sculpting Tools¶

Tool to use for any of the sculpting brushes.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

---

## Seams¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/uv/unwrapping/seams.html

**Contents:**
- Seams¶
- Mark Seam¶
  - Seams from Islands¶

For many cases, using the Unwrap calculations of Cube, Cylinder, Sphere, or the regular “Unwrap” operators will produce a good UV layout. But for more complex meshes, especially those with lots of indentations, you may want to define a seam to limit and guide the Unwrap operator.

Just like in sewing, a seam is where the ends of the image/cloth are sewn together. In unwrapping, the UV map is discontinuous at the seams. Think of this method as peeling an orange or skinning an animal. You make a series of cuts in the skin, then peel it off. You could then flatten it out, applying some amount of stretching. These cuts are the same as seams.

Simple seam on a cylinder.¶

When using this method, you need to be aware of how much stretching there is. The more seams there are, the less stretching there is, but this is often an issue for the texturing process. It is a good idea to have as few seams as possible while having the least amount of stretching. Try to hide seams where they will not be seen. In productions where 3D paint is used, this becomes less of an issue, as projection painting can easily deal with seams, as opposed to 2D texturing, where it is difficult to match the edges of different UV islands.

The workflow is the following:

Adjust seams and repeat.

Edge ‣ Mark/Clear Seam

To add an edge to a seam, simply select the edge and press Ctrl-E to Mark Seam, or to remove it, use Ctrl-E to Clear Seam.

In the example to the right, the back-most edge of the cylinder was selected as the seam (to hide the seam), and the default unwrap calculation was used. In the UV Editor, you can see that all the faces are nicely unwrapped, just as if you cut the seam with a scissors and spread out the fabric.

When marking seams, you can use Select Linked in Face Select Mode to check your work. This menu option selects all faces connected to the selected one, up to a seam. If faces outside your intended seam are selected, you know that your seam is not continuous. You do not need continuous seams, however, as long as they resolve regions that may stretch.

Just as there are many ways to skin a cat, there are many ways to go about deciding where seams should go. In general though, you should think as if you were holding the object in one hand, and a pair of sharp scissors in the other, and you want to cut it apart and spread it on the table with as little tearing as possible. Note that we seamed the outside edges of her ears, to separate the front from the back. Her eyes are disconnected sub-meshes, so they are automatically unwrapped by themselves. A seam runs along the back of her head vertically, so that each side of her head is flattened out.

Another use for seams is to limit the faces unwrapped. For example, when texturing a head, you do not really need to texture the scalp on the top and back of the head since it will be covered in hair. So define a seam at the hairline. Then, when you select a frontal face, and then select linked faces before unwrapping, the select will only go up to the hairline seam, and the scalp will not be unwrapped.

When unwrapping anything that is bilateral, like a head or a body, seam it along the mirror axis. For example, cleave a head or a whole body right down the middle in front view. When you unwrap, you will be able to overlay both halves onto the same Texture Space, so that the image pixels for the right hand will be shared with the left; the right side of the face will match the left, etc.

You do not have to come up with “one unwrapping that works perfectly for everything everywhere”. As we will discuss later, you can easily have multiple UV unwrappings, using different approaches in different areas of your mesh.

UV ‣ Seams from Islands

Adds seams at the boundaries of existing UV islands. This is useful when modifying the UVs of already unwrapped meshes.

---

## Selecting¶

**URL:** https://docs.blender.org/manual/en/latest/interface/selecting.html

**Contents:**
- Selecting¶
- Toolbar Selection Tools¶
  - Tweak¶
  - Select Box¶
  - Select Circle¶
  - Select Lasso¶
  - Selection Modes¶
- Menu Selection Tools¶
  - Box Select¶
  - Circle Select¶

By default, Blender uses LMB to select items. This can be changed to RMB in the Preferences.

Blender has several selection tools that can be used across the different editors.

Some editors deviate from the keyboard shortcuts shown below. For example, most editors use Shift-LMB to add a single item to the selection, but the Outliner uses Ctrl-LMB. Similarly, most editors use Ctrl-RMB for performing a Lasso Select, but node editors use Ctrl-Alt-LMB.

Most selection tools come in two variants, where one variant is available in the Toolbar and the other in the Select menu. While the variants’ names are almost identical (such as Select Box in the Toolbar versus Box Select in the menu), the way they work is a bit different. New users coming from other applications will find the Toolbar variants to be the most familiar.

All the Toolbar selection tools behave the same when clicking an item: they select it (and deselect any previously selected items). If you hold Shift while clicking, the item will be added to the selection (if it’s not selected) or removed from the selection (if it is selected).

What makes the tools different is what happens when you drag.

Dragging an item will move it around.

Dragging will create a rectangle, and select all the items that are partially or completely inside it once you release. (Any other items will be deselected.)

Holding Shift while dragging will add the items to the selection. Holding Ctrl will remove them.

While dragging, you can additionally hold Spacebar to move the rectangle around with the mouse.

Toolbar ‣ Select Circle

Dragging will select all the items which the circle passed over. Items which you didn’t pass over will be deselected.

Holding Shift while dragging will add the items to the selection. Holding Ctrl will remove them.

You can change the radius of the circle in the tool settings (which can be found in the area header, the Tool tab of the Sidebar N, or the Active Tool tab of the Properties editor).

In Object Mode: unlike Select Box, which selects objects as soon as the box covers any part of their geometry, Select Circle only selects objects if the circle passes over their origin point. The origin is shown as an orange dot for selected objects but is invisible for unselected ones, unless “Origins (All)” is enabled in the Viewport Overlays.

This difference in behavior does not apply to the other modes (like Edit Mode and Pose Mode).

Toolbar ‣ Select Lasso

Dragging will create a freeform shape, and select all the items inside it once you release. (Any other items will be deselected.)

Holding Shift while dragging will add the items to the selection. Holding Ctrl will remove them.

While dragging, you can additionally hold Spacebar to move the shape around with the mouse.

Select Lasso behaves the same as Select Circle in that it only looks at origin points in Object Mode.

Each of the Toolbar selection tools has a mode to configure how it interacts with existing selections. Note that not every tool supports all of these modes.

Sets a new selection (the previous selection is discarded). This is the default.

Adds newly selected items to the existing selection.

Removes newly selected items from the existing selection.

Inverts the selection (unselected items become selected and vice versa).

Selects items that intersect with the existing selection.

These tools are variants of the previously described ones. They’re available in the menu rather than the Toolbar and work slightly differently.

To use this tool, you first activate the menu item or keyboard shortcut and then drag a box as usual. Unlike Select Box, the default behavior here is to add the items inside the box to the selection. (The ones outside the box are not deselected.)

To remove the items inside the box from the selection, hold Shift, or drag with MMB instead.

While dragging, you can additionally hold Spacebar to move the box around with the mouse.

Select ‣ Circle Select

To use this tool, you first activate the menu item or keyboard shortcut and then drag a circle around as usual. Unlike Select Circle, the default behavior here is to add the items inside the circle to the selection. (The ones outside the circle are not deselected.)

To remove the items inside the circle from the selection, hold Shift, or drag with MMB instead.

You can change the radius of the circle by scrolling with the Wheel or using the NumpadPlus and NumpadMinus keys.

Once activated, Circle Select stays active: you can release the mouse button and start dragging somewhere else without having to press C again. At the same time, however, it blocks all other parts of Blender while it’s active. To deactivate the tool again, press RMB, Return, or Esc.

Select ‣ Lasso Select

To use this tool, you first activate the menu item and drag a freeform shape around the item(s) you want to select with LMB. The menu lets you choose whether to set, extend or reduce the selection.

Alternatively, you can immediately start dragging with Ctrl-RMB. Unlike Select Lasso, the default behavior then is to add the items inside the lasso to the selection. (The ones outside the lasso are not deselected.)

To remove the items inside the lasso from the selection, drag with Shift-Ctrl-RMB instead.

While dragging, you can additionally hold Spacebar to move the lasso around with the mouse.

---

## Selecting Curve Elements¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/curves/selecting.html

**Contents:**
- Selecting Curve Elements¶
- Select Menu¶
- All¶
- None¶
- Invert¶
- Box Select¶
- Circle Select¶
- Lasso Select¶
- Select Random¶
- Checker Deselect¶

This page discusses specific selecting tools for curve objects in Edit Mode. The Curve Edit more also uses the general select tools used which are described in the interface section.

Curve selection in Edit Mode has fewer options than with meshes. Mainly this is, because there is only one selectable element type, the control points (no select mode needed here…). These points are a bit more complex than simple vertices, however, especially for Bézier curves, as there is the central vertex, and its two handles…

The basic tools are the same as with meshes, so you can select a simple control point with the LMB, add to current selection with Shift-LMB, Box Select B, and so on.

One word about the Bézier control points: when you select the main central vertex, the two handles are automatically selected too, so you can move it as a whole, without creating an angle in the curve. However, when you select a handle, only this vertex is selected, allowing you to modify this control vector…

Note that, unlike mesh edges, you cannot directly select a segment. Instead, select all of the control points that make up the segment you want to edit.

With curves, all “advanced” selection options are grouped in the Select menu of the 3D Viewport header.

Select all selectable elements.

Deselect all elements, but the active element stays the same.

Selects all the geometry that are not selected, and deselect currently selected components.

Interactive box selection.

Select ‣ Circle Select

Interactive circle selection.

Select ‣ Lasso Select

Select ‣ Select Random

Select Random control points.

Selects the defined percentage of control points.

Seed used by the pseudo-random number generator.

Controls whether the operator Selects or Deselects control points.

Select ‣ Checker Deselect

This tool applies an alternating selected/deselected checker pattern. This only works if you already have more than one control point selected.

It works by changing the current selection so that only every Nth control points will remain selected, starting from the active one.

The number of deselected elements in each pattern repetition.

The number of selected elements in each pattern repetition.

Offset from the starting point.

Ctrl-NumpadPlus, Ctrl-NumpadMinus

Their purpose, based on the currently selected control points, is to reduce or enlarge this selection.

For each selected control point, select all its linked points (i.e. one or two…).

For each selected control point, if all points linked to this point are selected, keep this one selected. Otherwise, deselect it.

This implies two points:

When all control points of a curve are selected, nothing will happen (as for Less, all linked points are always selected, and of course, More cannot add any). Conversely, the same goes when no control points are selected.

Second, these tools will never “go outside” of a curve (they will never “jump” to another curve in the same object).

Select ‣ Select Linked

Selects all control points connected to the active control point.

This operator makes it easier to select or deselect entire segments of a curve, especially in dense or complex curves, where manually selecting each point would be time-consuming.

Selects (L) or deselects (Shift-L) control points connected to the control point nearest the mouse cursor.

For Bézier curves with a handle selected, this selection operator will select the whole control point and all the linked ones.

Select ‣ Select Similar

Selects control points that have certain similar properties to the active one. The Adjust Last Operation panel provides several selection options:

Selects splines that have the same spline Type i.e. Bézier, NURBS or Poly.

Selects control points that have a similar Radius value.

Selects all points that have a similar Weight value.

Selects control points that have a similar handles direction.

For quantitative properties, this property selects the type of comparison to between the two numerical values.

Select items with the same value as the active item’s chosen property.

Select items with a larger value as the active item’s chosen property.

Select items with a smaller value as the active item’s chosen property.

For quantitative properties, this property controls how close the property’s values have to be in the comparison.

Select ‣ (De)select First, Select ‣ (De)select Last

These operators will toggle the selection of the first or last control point(s) of the curve(s) in the object. This is useful to quickly find the start of a curve (e.g. when using it as path…).

Select ‣ Select Next, Select ‣ Select Previous

These operators will select the next or previous control point(s), based on the current selection (i.e. the control points following or preceding the selected ones along the curve). In case of a cyclic curve, the first and last points are not considered as neighbors.

Menu Search ‣ Pick Shortest Path

Selects the curve segments between two control points: the active and the one under the cursor. In the case of a closed curve, the shortest path will be selected.

---

## Selecting Curve Elements¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/curves_new/selecting.html

**Contents:**
- Selecting Curve Elements¶
- Selection Modes¶
- All¶
- None¶
- Invert¶
- Select Random¶
- Select More/Less¶
- Select Linked¶
  - Select Linked Pick¶
- Select Endpoints¶

Hair curves, while similar to regular curves are a bit different and have their own selection tools. Many of these match their regular curve tools but are implemented differently All hair curve selection operators are documented below for completeness.

These selection operators work in both Sculpt and Edit modes.

3D Viewport Header ‣ Select Mode

Note, this is only supported for “Hair Curves”.

Selection modes limits selection operators to certain curve domains. This feature is makes it easy to select whole segments at once, or to give more granular control over editing.

Allows selection of individual control points.

Limits selection to whole curve segments.

Select all selectable elements.

Deselect all elements, but the active element stays the same.

Selects all the geometry that are not selected, and deselect currently selected components.

Select ‣ Select Random

Select Random control points.

Seed used by the pseudo-random number generator.

Selects the defined percentage of control points.

Ctrl-NumpadPlus, Ctrl-NumpadMinus

Their purpose, based on the currently selected control points, is to reduce or enlarge this selection.

For each selected control point, select all its linked points (i.e. one or two…).

For each selected control point, if all points linked to this point are selected, keep this one selected. Otherwise, deselect it.

This implies two points:

When all control points of a curve are selected, nothing will happen (as for Less, all linked points are always selected, and of course, More cannot add any). Conversely, the same goes when no control points are selected.

Second, these tools will never “go outside” of a curve (they will never “jump” to another curve in the same object).

Select ‣ Select Linked

Selects all control points connected to the active control point.

This operator makes it easier to select or deselect entire segments of a curve, especially in dense or complex curves, where manually selecting each point would be time-consuming.

Selects (L) or deselects (Shift-L) control points connected to the control point nearest the mouse cursor.

For Bézier curves with a handle selected, this selection operator will select the whole control point and all the linked ones.

Select ‣ Select Endpoints

Select endpoints of curves.

Only supported in the Control Point selection mode.

---

## Selecting Nodes¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/selecting.html

**Contents:**
- Selecting Nodes¶
- All¶
- None¶
- Invert¶
- Box Select¶
- Circle Select¶
- Lasso Select¶
- Linked From¶
- Linked To¶
- Select Grouped¶

Nodes in the editor can be selected and manipulated. Selections determine which nodes can be moved, duplicated, or connected. The active node (last selected) is highlighted with a lighter outline. It serves as the reference for certain operations, such as grouping or linking, and also determines which properties are displayed in the Sidebar and Properties Editor.

Nodes are selected with LMB. Multiple nodes can be selected by holding Shift-LMB.

Blender also provides a variety of selection tools and shortcuts for quickly choosing nodes based on their type, connections, or layout.

Inverts the current selection, selecting all unselected nodes and deselecting the currently selected ones.

Click and drag to select nodes within a rectangular region. See Box Select for more details.

Select ‣ Circle Select

Click and drag with a circular brush to select nodes. See Circle Select.

Select ‣ Lasso Select

Draw a freeform lasso to select nodes within the region. See Lasso Select.

Expands the selection to all nodes connected to the inputs of the selected nodes.

Expands the selection to all nodes connected from the outputs of the selected nodes.

Select ‣ Select Grouped

Selects nodes that share similar properties with the active node.

Type: Select all nodes of the same type (e.g. all Math nodes).

Color: Select nodes with the same custom color. (This refers to user-assigned editor colors, not the color data processed by nodes.)

Prefix/Suffix: Select nodes whose names match the same starting or ending text.

Select ‣ Activate Same Type Previous/Next

Cycles through nodes of the same type, activating the previous or next node in the node tree and centering it in the view.

Opens a search pop-up to quickly locate and select a node within the current node tree. Nodes can be searched by name, socket label, or certain socket values such as strings and data-block references.

Once a match is selected, the editor view automatically pans and centers on the found node, highlighting it for easy access.

This operator is especially useful in large node trees for navigating complex networks efficiently.

---

## Selecting Objects¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/selecting.html

**Contents:**
- Selecting Objects¶
- Object Mode¶
- Edit Mode¶
- Pose Mode¶
- Particle Edit Mode¶

This page discusses selection tools that are specific to the 3D Viewport. The generic selection tools are described in the Interface section.

The 3D Viewport has two keys that affect selection:

Selects objects by their origin rather than their geometry.

Shows a menu in case there are multiple objects under the mouse cursor, making it easier to select the one you want.

These keys can be combined to get a selection menu based on object origins.

The mode-specific selection pages are listed below.

Grease Pencil Edit Mode

---

## Selecting Point Cloud Objects¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/point_cloud/selecting.html

**Contents:**
- Selecting Point Cloud Objects¶
- All¶
- Select None¶
- Select Invert¶
- Select Random¶

This section describes the available selection operators when working with point cloud objects in Edit Mode. These operators allow you to quickly select or deselect points for further editing or transformation.

Selects all points in the point cloud.

Deselects all currently selected points in the point cloud.

Inverts the selection state of each point in the point cloud:

Points that were selected become deselected.

Points that were not selected become selected.

This operator is useful for quickly selecting the opposite subset of points in your current selection.

Select ‣ Select Random

Selects a random subset of points in the point cloud.

The seed value used by the pseudo-random number generator. Adjusting this value changes which points are randomly selected.

A value between 0.0 and 1.0 that determines the percentage of points to be selected. For example, a value of 0.25 selects roughly 25% of the points.

This operator is useful for procedural modeling, scattering, or testing effects with a random distribution.

---

## Separate Bundle Node¶

**URL:** https://docs.blender.org/manual/en/latest/interface/controls/nodes/types/utilities/bundles/separate_bundle.html

**Contents:**
- Separate Bundle Node¶
- Inputs¶
- Properties¶
  - Bundle Items¶
- Outputs¶

The Separate Bundle node extracts individual values from a Bundle. Each output corresponds to an element in the bundle, identified by its socket name.

This node is the counterpart of the Combine Bundle node and is typically used to retrieve structured data that was previously grouped together.

The input bundle that contains all grouped values.

Properties are available in the Node tab of the Sidebar.

Updates the current node to match the socket signature of the connected nodes. Use this after renaming, adding, or removing sockets.

Locks the current item list and types to stabilize interfaces when publishing node groups. When enabled, adding/removing items is disabled until the option is turned off.

Displays one entry per element in the bundle. Double-click to rename.

Add a new socket to the bundle.

Delete the selected socket.

The data type for the selected item (e.g. Float, Vector, Geometry, Object, Bundle). For value types, a default value control is shown and used when the socket is unlinked.

This node has a dynamic set of output sockets. Each socket outputs the value of the corresponding bundle item, using the item’s name and type as defined in the bundle.

---

## Settings¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/domain/settings.html

**Contents:**
- Settings¶
- Border Collisions¶
- Gas¶
  - Dissolve¶
- Fire¶
- Liquid¶

Physics ‣ Fluid ‣ Settings

The domain object contains the entire simulation. Fluid simulations cannot leave the domain, it will either collide with the edge or disappear, depending on the domain’s settings.

Keep in mind that large domains need higher resolutions and longer bake times. You will want to make it just large enough that the simulation will fit inside it, but not so large that it takes too long to compute the simulation.

To create a domain, add a cube and transform it until it encloses the area where you want the simulation to take place. Translation, rotation, and scaling are all allowed. To turn it into a fluid domain, click Fluid in the Properties ‣ Physics tab, then select Domain as the fluid Type.

You can use other shapes of mesh objects as domain objects, but the fluid simulator will use the shape’s Bounding Box as the domain bounds. In other words, the actual shape of the domain will still be rectangular.

A fluid domain can control either liquid or gas flows. Liquid domains take all liquid flow objects that intersect with the domain into consideration. Gas domains consider all intersecting Smoke, Fire, and Smoke & Fire flow objects. It is not possible to change the domain type dynamically.

The fluid domain is subdivided into many “cells” called Voxels which make up “pixels” of fluid. This setting controls the number of subdivisions in the domain. Higher numbers of subdivisions are one way of creating higher resolution fluids.

Since the resolution is defined in terms of “subdivisions”, larger domains will need more divisions to get an equivalent resolution to a small domain. For example, a one meter cube with 64 Resolution Divisions will need 128 divisions to match a 2 meter cube. The dimension used as the base division is the longest dimension of the objects bounding box. To help visualize the voxel size, the Resolution Divisions can be previewed with a small cube shown in the 3D Viewport, to show the size of these divisions.

Controls the speed of the simulation. Low values result in a “slow motion” simulation, while higher values can be used to advance the simulation faster (good for generating fluids to be used in still renders).

Lets the solver automatically decide when to perform multiple simulation steps per frame. It takes into account the maximum and minimum number of time steps, the current Frame Rate, and the Time Scale.

Determines the maximum velocity per grid cell and is measured in grid cells per time step. Fluid is only allowed to move up to this velocity in one time step. If this threshold is exceeded the solver will subdivide the simulation step.

In general, greater CFL (Courant–Friedrichs–Lewy) numbers will minimize the number of simulation steps and the computation time. Yet it will yield less physically accurate behavior for fast fluid flows. Smaller CFL numbers result in more simulation steps per frame, longer simulation times but more accurate behavior at high velocities (e.g. fast fluid flow colliding with obstacle).

When lowering the CFL number it is recommended to increase the maximum number of time steps. Similarly, when increasing the CFL number the minimum number of time steps should be adjusted.

Maximum number of allowed time steps per frame. If needed, the solver will divide a simulation step up to this number of sub-steps.

Minimum number of allowed time steps per frame. The solver will always perform at least this number of simulation steps per frame.

By default the fluid solver will use the global scene gravity. This behavior can be disabled in the scene settings. Disabling the global gravity will enable the fluid gravity options.

Voxels with values under this value are considered empty space. More empty space optimizes rendering. With OpenVDB caching it also reduces cache sizes.

Remover any volume of fluid that intersects with an obstacle inside the domain.

Physics ‣ Fluid ‣ Settings ‣ Border Collisions

Controls which sides of the domain will allow fluid “pass through” the domain, making it disappear without influencing the rest of the simulation, and which sides will deflect fluids.

Physics ‣ Fluid ‣ Gas

Buoyant force based on gas density.

Values above 0 will cause the gas to rise (simulating gas which is lighter than ambient air).

Values below 0 will cause gas to sink (simulating gas which is heavier than ambient air).

Controls how much gas is affected by temperature. The effect this setting has on gas depends on the per flow object Initial Temperature:

Values above 0 will result in the gas rising when the flow object Initial Temperature is set to a positive value, and gas sinking when the flow object Initial Temperature is set to a negative value.

Values below 0 will result in the opposite of positive values, i.e. gas emitted from flow objects with a positive Initial Temperature will sink, and gas from flow objects with a negative Initial Temperature will rise.

Note that gas from multiple flow objects with different temperatures will mix and warm up or cool down until an equilibrium is reached.

Controls the amount of turbulence in the gas. Higher values will make lots of small swirls, while lower values make smoother shapes.

Domain with a vorticity of 0.0.¶

Domain with a vorticity of 0.2.¶

Allow gas to dissipate over time.

Speed of gas dissipation in frames.

Dissolve gas in a logarithmic fashion. Dissolves quickly at first, but lingers longer.

Physics ‣ Fluid ‣ Gas ‣ Fire

How fast fuel burns. Larger values result in smaller flames (fuel burns before it can go very far), smaller values result in larger flames (fuel has time to flow farther before being fully consumed).

Amount of extra smoke created automatically to simulate burnt fuel. This smoke is best visible when using a “Fire + Smoke” Flow Object.

Vorticity for flames in addition to the global fluid Vorticity.

Maximum temperature of flames. Larger values result in faster rising flames.

Minimum temperature of flames. Larger values result in faster rising flames.

Color of smoke emitted from burning fuel.

Physics ‣ Fluid ‣ Liquid

Liquid settings control the behavior of the particles which the simulation consists of. Enabling the liquid checkbox will automatically create a particle system for the simulation. This particle system visualizes the flow of the simulation. Visualizing the liquid particles is optional. The fluid simulation will make use of all the fields without an attached particle system too.

Disabling the liquid checkbox will delete the attached particle system and its settings.

Determines the liquid particle simulation method.

(FLuid Implicit Particle) Produces a very splashy simulation with lots of particles dispersed in the air.

(Affine Particle-In-Cell) Produces a very energetic but also more stable simulation. Vortices within the liquid will be preserved better than with FLIP.

How much FLIP velocity to use when updating liquid particle velocities. A value of 1.0 will result in a completely FLIP based simulation. Completely FLIP based simulations produce more chaotic splashes and are preferable when simulating greater quantities of liquid. When using smaller values the behavior will be less turbulent and splashes are more subtle. This is optimal when simulating scenes where the liquid is supposed to be on a small scale.

Maximum number of fluid particles that are allowed in the simulation. If this field is set to a nonzero value the simulation will never contain more than this number of fluid particles. Otherwise, with a value of zero the solver will always sample new particles when needed.

The radius of one liquid particle in grid cells units. This value describes how much area is covered by a particle and thus determines how much area around it can be considered as liquid. A greater radius will let particles cover more area. This will result in more grids cell being tagged as liquid instead of just being empty.

Whenever the simulation appears to leak or gain volume in an undesired, non physically accurate way it is a good idea to adjust this value. That is, when liquid seems to disappear this value needs to be increased. The inverse applies when too much liquid is being produced.

Factor that is used when sampling particles. A higher value will sample more particles. Note that particle resampling occurs at every single simulation step.

New particles are sampled with some randomness attached to their position which can be controlled by this field. Higher values will sample the liquid particles more randomly in inflow regions. With a value of 0.0 all new particles will be sampled uniformly inside their corresponding grid cells.

When trying to create a laminar inflow (with little randomness) or more turbulent flows (with greater randomness) this value can be useful.

The maximum number of liquid particles per grid cell. During a simulation the number of liquid particles in a cell can fluctuate: Particles can flow into other cells or can get deleted if they move outside the narrow band. Resampling will add new particles considering this maximum.

This value sets the upper threshold of particles per cell. It is also a good way to estimate how many particles there can be in your simulation (one needs to take grid resolution into account too). This can be useful before baking and when planning a simulation.

The minimum number of liquid particles per grid cell. Similarly to the maximum particle threshold, this value ensures that there are at least a certain amount of particles per cell.

Controls the width in grid cell units of the narrow band that liquid particles are allowed to flow in. A high value will result in a thicker band and can result in an inflow region completely filled with particles. Unless the goal of the simulation is to visualize the liquid particles it is recommended to not increase the band width significantly as more particles slow down the simulation.

In some situations increasing this value can help create volume when the simulation appears to leak. In all other cases it is best to keep the narrow band as thin as possible since the liquid surface contains most details and simulating particles inside the liquid is not an optimal use of computing resources.

The narrow band is an implementation of Narrow Band FLIP for Liquid Simulations.

Enables finer resolution in fluid / obstacle regions (second order obstacles). This option reduces the “stepping effect” that results when an obstacle lies inclined inside the domain. It also makes liquid flow more smoothly over an obstacle.

Determines how far apart fluid and obstacles are. This value can be used to achieve a more fluid motion over inclined obstacles: Depending on the slope of the obstacle increasing this value can help liquid particles flow better over an obstacle. Setting this field to a negative value will let fluid move towards the inside of an obstacle.

Value to control the smoothness of the fractional obstacle option. Smaller value reduce the “stepping effect” but may result particles sticking to the obstacle.

This option is only available when using the Modular cache type. Bake Data simulates and stores the base of the fluid simulation on drive. Both gas and liquid simulations can add refinements on top of this (e.g. gas simulations can add noise, liquid simulations can add a mesh or secondary particles or both).

The progress will be displayed in the status bar. Pressing Esc will pause the simulation.

Once the simulation has been baked, the cache can be deleted by pressing Free Data. It is possible to pause or resume a Bake All process.

---

## Snapping¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/controls/snapping.html

**Contents:**
- Snapping¶
- Snap Base¶
- Snap Target¶
- Snap Target for Individual Elements¶
- Target Selection¶
- Affect¶
- Rotation Increment¶

Object, Edit, and Pose Mode

Snapping lets you easily align objects and mesh elements to others. It can be toggled by clicking (Snap Off) / (Snap On) in the 3D Viewport’s header, or more temporarily by holding Ctrl.

Transform Modal Map for further keyboard shortcuts.

Object, Edit, and Pose Mode

Determines which point in the geometry is the snap base that will snap to the target.

Snaps using the origin (in Object Mode) or center (in Edit Mode) of the active element.

Snaps using the median of the selection.

Snaps using the current transformation center (another word for the pivot point). This option is especially useful in combination with the 3D Cursor for choosing the snapping point completely manually.

Snaps using the vertex that’s closest to the target.

Object, Edit, and Pose Mode

Snapping ‣ Snap Target

Determines the target which the selection will be snapped to.

Snaps to grid points. When in Orthographic view, the snapping increment changes depending on the zoom level.

This option snaps to an imaginary grid that starts at the selection’s original location and has the same resolution as the viewport grid. In other words, it lets you move the selection in “increments” of the grid cell size.

Snaps to the grid that’s displayed in the viewport.

Snaps to the vertex that’s closest to the mouse cursor.

Snaps to the edge that’s closest to the mouse cursor.

Snaps to the surfaces of faces in mesh objects; This is useful for retopologizing.

Snaps the selection to a depth that’s centered inside the object under the cursor. This is useful for positioning an Armature bone so it’s centered inside a character’s arm, for example; the other snapping options would place it on the arm’s surface instead.

While Blender also has Volume objects, this option is not related to those.

Snaps to the centerpoint of the edge that’s closest to the mouse cursor.

Snaps to a specific point on the edge so that the line from the selection’s original location (indicated by a white cross) to its new location is perpendicular to that edge.

Multiple snapping modes can be enabled at once using Shift-LMB.

Object, Edit, and Pose Mode

Snapping ‣ Snap Target for Individual Elements

Type of element for individual transformed elements to snap to.

Snaps to the face that’s under the mouse cursor. This can be used for bending a flat sheet so it snugly fits against a curved surface, for example.

This works similar to the Shrinkwrap Modifier.

Individually snaps each object (in Object Mode) or vertex (in Edit Mode) to the face that’s closest to its new location. This makes it possible to snap to occluded geometry.

Sets more detailed snapping options. The available options depend on the mode (Object/Edit) as well as the Snap Target.

Snap to other mesh elements of the active object.

This checkbox is ignored if Proportional Editing is enabled.

Snap to other objects that are also in Edit Mode.

Snap to other objects that are not in Edit Mode.

Snap only to objects that are selectable.

Rotates the selection so that its Z axis gets aligned to the normal of the target.

Exclude back-facing geometry from snapping.

Snap only to the object which the selection was nearest to before starting the transformation.

Breaks the overall transformation into multiple steps, performing a snap each time. This can give better results in certain cases.

If the target object is composed of several disconnected mesh islands that intersect each other, “Snap To Volume” will normally snap to the island which the mouse is hovering over, ignoring the other islands. By enabling “Snap Peel Object,” you can instead treat the target object as one connected whole.

Specifies which transformations are affected by snapping. By default, snapping only happens while moving something, but you can also enable it for rotating and scaling.

Angle used in incremental snapping for the rotation operator. The second value is the Rotation Precision Increment, used for finer transformations and activated by default with the Shift key.

---

## Snapping¶

**URL:** https://docs.blender.org/manual/en/latest/editors/uv/controls/snapping.html

**Contents:**
- Snapping¶
- Snap Target¶
- Additional Options¶
- Affect¶
- Rotation Increment¶

Snapping lets you easily align UV elements to others. It can be toggled by clicking the magnet icon in the UV Editor’s header, or more temporarily by holding Ctrl.

This page is about the Snap header button; for the Snap menu, see UV Editing.

Snaps to grid points.

This option snaps to an imaginary grid that starts at the selection’s original location and has the same resolution as the grid displayed in the editor. In other words, it lets you move the selection in “increments” of the grid cell size.

Snaps to grid points.

Snaps to the vertex that’s closest to the mouse cursor.

See 3D Viewport Snapping for more information.

Specifies which transformations are affected by snapping. By default, snapping only happens while moving something, but you can also enable it for rotating and scaling.

Angle used in incremental snapping for the rotation operator. The second value is the Rotation Precision Increment, used for finer transformations and activated by default with the Shift key.

---

## Spin¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/tools/spin.html

**Contents:**
- Spin¶
- Tool Settings¶
- Options¶
- Example¶
  - Angle¶
  - Duplicate¶
  - Merge Duplicates¶
  - Recalculate Normals¶

Mesh ‣ Extrude ‣ Spin

The Spin tool extrudes (or duplicates it if the selection is manifold) the selected elements, rotating around a specific point and axis.

Use the tool to create the sort of objects that you would produce on a lathe (this tool is often called “lathe” tool or “sweep” tool in the literature, for this reason). In fact, it does a sort of circular extrusion of your selected elements, centered on the 3D cursor, and around the axis perpendicular to the working view…

The point of view will determine around which axis the extrusion spins…

The position of the 3D cursor will be the center of the rotation.

Specifies how many copies will be extruded along the “sweep”.

When enabled, will keep the original selected elements as separated islands in the mesh (i.e. unlinked to the result of the spin extrusion).

Specifies the axis to use as the pivot of the spin operation.

Specifies how many copies will be extruded along the “sweep”.

Specifies the angle “swept” by this tool, in degrees (e.g. set it to 180 for half a turn).

Automatically merges the first a last duplicates, if they make a full revolution which results in overlapping geometry.

Reverses the Normal’s direction for any resulting geometry.

Specifies the center of the spin. By default it uses the cursor position.

Specify the spin axis as a vector. By default it uses the view axis (viewport).

First, create a mesh representing the profile of your object. If you are modeling a hollow object, it is a good idea to thicken the outline. Fig. Glass profile. shows the profile for a wine glass we will model as a demonstration.

We will be rotating the object around the cursor in the top view, so switch to the top view with Numpad7.

Glass profile, top view in Edit Mode, just before spinning.¶

Place the cursor along the center of the profile by entering Edit Mode and selecting one of the vertices along the center, and snapping the 3D cursor to that location with Mesh ‣ Snap ‣ Cursor to Selection. (Fig. Glass profile, top view in Edit Mode, just before spinning.) shows the wine glass profile from top view, with the cursor correctly positioned.

Select all the vertices with A and select the Spin tool from the Toolbar and use the Gizmo to spin the vertices. Fig. Spun profile. shows the result of a successful spin.

Spun profile using an angle of 360.¶

Spun profile using an angle of 120.¶

Result of spin operation.¶

Result of Duplicate enabled.¶

The spin operation leaves duplicate vertices along the profile. You can select all vertices at the seam with Box select B (shown in Fig. Duplicate vertices.) and perform a Merge by Distance operation.

Notice the selected vertex count before and after the Merge by Distance operation Vertex count after removing doubles. If all goes well, the final vertex count (38 in this example) should match the number of the original profile noted in Mesh data ‣ Vertex and face numbers. If not, some vertices were missed and you will need to weld them manually. Or, worse, too many vertices will have been merged.

Merging Two Vertices into One

To merge (weld) two vertices together, select both of them by Shift-LMB clicking on them. Press S to start scaling and hold down Ctrl while scaling to scale the points down to 0 units in the X, Y and Z axis. LMB to complete the scaling operation and click Mesh ‣ Merge ‣ By Distance to merge the vertices. Alternatively, you can use Context Menu ‣ Merge Vertices (or M). Then, in the new pop-up menu, choose to merge By Distance.

All that remains now is to recalculate the normals to the outside by selecting all vertices, pressing Alt-N and validating Recalculate Normals Outside in the pop-up menu.

---

## Splash Screen¶

**URL:** https://docs.blender.org/manual/en/latest/interface/window_system/splash.html

**Contents:**
- Splash Screen¶
- Splash Image¶
- Interactive Region¶

When starting Blender, the splash screen appears in the center of the window. It contains options to create new projects or open recent ones. A more detailed description can be found below.

Blender Splash Screen.¶

To close the splash screen and start a new project, click anywhere outside the splash screen (but inside the Blender window) or press Esc. The splash screen will disappear revealing the default screen. To reopen the splash screen, click on the Blender icon in the Topbar and select Splash Screen.

When starting Blender for the first time or updating to a new version, the “interactive region” contains a Quick Set Up Process.

The upper part of the splash screen contains the splash image with the Blender version in the top right.

The interactive region is the bottom half of the splash screen.

Start a new project based on a template.

Your most recently opened blend-files. This gives quick and easy access to your recent projects.

Allows opening an existing blend-file.

Blender will try to recover the last session based on temporary files. See Recovering Data.

Open the latest release notes.

Open Blender’s Development Fund website.

---

## Stack¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/interface/stack.html

**Contents:**
- Stack¶

The list of constraints affecting an object or bone is called the Constraint Stack. It’s evaluated from top to bottom, and reordering it can drastically change the outcome.

Moving constraints is done by dragging their handle with LMB.

---

## Status Bar¶

**URL:** https://docs.blender.org/manual/en/latest/interface/window_system/status_bar.html

**Contents:**
- Status Bar¶
- Keymap Information¶
- Status Messages¶
- Resource Information¶

The Status Bar is located at the bottom of the Blender window and displays contextual information such as keyboard shortcuts, messages, and statistical information. The Status Bar can be hidden by disabling Show Status Bar in Window menu or by dragging from the top edge down.

The left side of the Status Bar displays mouse button shortcuts and the keymap of the active tool. In editors with a Toolbar, tapping Alt (or Option on macOS) shows the hotkeys to change to a desired tool.

This functionality can be disabled with the Alt Click Tool Prompt preference in the Keymap Preferences).

The middle of the Status Bar displays information about in-progress operations.

Shows the progress of the currently running task (such as rendering or baking). Hovering the mouse pointer over the progress bar will display a time estimate. The task can be aborted by clicking the cancel button ().

Informational messages or warnings, such as after saving a file. They disappear after a short time. Click them to show the full message in the Info Editor.

The right side of the Status Bar displays information about the Blender instance. Which information is shown can be chosen by RMB on the Status Bar or in the Preferences.

Shows information about the data in the active scene.

Collection: The name of the active Collection.

Active Object: The name of the active selected object.

Geometry: Information about the current scene depending on the mode and object type. This can be the number of vertices, faces, triangles, or bones.

Objects: The number of selected objects and the total count of objects.

Shows the total amount of time of the playback along with the current frame number and total frame count. The format of the duration text is determined by the Timecode Style.

Shows an estimate of Blender’s RAM consumption. On a single-instance single-machine scenario, this estimate provides a measurement against the hardware limit of the machine.

Shows the number of extensions with available updates.

Shows the version number of Blender that is currently running.

---

## Tabs & Panels¶

**URL:** https://docs.blender.org/manual/en/latest/interface/window_system/tabs_panels.html

**Contents:**
- Tabs & Panels¶
- Tabs¶
  - Switching/Cycling¶
- Panels¶
  - Collapsing and Expanding¶
  - Position¶
  - Pinning¶
  - Presets¶

Top: Horizontal Tab header in the Topbar. Bottom: Vertical Tab header shows tab icons in the Properties.¶

Tabs are used to control overlapping sections in the user interface. The content of only one Tab is visible at a time. Tabs are listed in a Tab header, which can be horizontal or vertical.

Vertical tabs can be switched with Ctrl-Wheel from anywhere in the tab. You can also cycle through tabs with Ctrl-Tab and Shift-Ctrl-Tab, or press down LMB and move the mouse over the tab header icons. Pressing NumpadPeriod scrolls to the active tab in case it is out of view.

Note, these shortcuts does not apply to Workspace tabs; see Workspace controls.

Panels in Properties.¶

A panel is highlighted in yellow and a subpanel in red.

The smallest organizational unit in the user interface is a panel. The panel header shows the title of the panel. It is always visible. Some panels also include subpanels.

A panel can either be expanded to show its contents, or collapsed to hide its contents. An expanded panel is indicated by a down-arrow (▼) in the panel header, while a collapsed panel is shown with a right-arrow (►).

Clicking LMB on the panel header expands or collapses it.

Pressing A expands/collapses the panel under the mouse pointer.

Clicking Ctrl-LMB on the header of a collapsed panel will expand it and collapse all others.

Clicking Ctrl-LMB on the header of an expanded panel will expand/collapse all its subpanels.

Dragging with LMB over the headers will expand or collapse many at once.

You can change the position of a panel within its region by clicking and dragging the grip widget (::::) on the right side of its header.

Sometimes it is desirable to view panels from different tabs at the same time. Like, for instance, having access to a camera’s properties, while other objects are selected. This has been solved by making panels pinnable.

A pinned panel remains visible regardless of which tab has been selected. You can pin a panel by clicking on the pin icon in its header. Panels that do not have a pin icon can be pinned by RMB on the panel header and selecting Pin, or by pressing Shift-LMB.

Pinning is not available for all panels. For example, it’s available in the Sidebar but not in the Properties editor.

Panels in Blender provide a Presets menu () for quickly reusing common settings. Presets can save time by storing frequently used configurations, which can then be reapplied with a single click.

Example Presets menu.¶

A list of available presets. Selecting one will apply the stored values to the relevant properties.

The name to use when adding a new preset.

Create a new preset using the current settings, the preset is then saved and appears in the list for future reuse.

Deletes the selected preset.

Presets are stored as Python files in Blender’s configuration directory. Advanced users can edit these preset files directly to fine-tune settings or copy them to other systems.

---

## Themes¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/themes.html

**Contents:**
- Themes¶
- Preset Management¶

The Themes section allows you to customize interface appearance and colors.

The colors for each editor can be set separately by simply selecting the editor you wish to change in the multi-choice list at the left, and adjusting colors as required. Notice that changes appear in real-time on your screen. In addition, details such as the dot size in the 3D Viewport or the Graph Editor can also be changed.

Select the Theme from a list of predefined Themes.

Adds a custom theme to the preset list.

Removes a custom theme from the preset list.

Save a custom theme in the preset list.

This will save the theme to an XML file in the ./scripts/presets/interface_theme/ subdirectory of one of the configuration directories.

Load and apply a Blender XML theme file and add it to the list of theme presets.

Reset to the default theme colors.

Blender comes bundled with a small selection of themes.

This is an example of the theme Blender Light.¶

---

## Toolbar¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/tools/toolbar.html

**Contents:**
- Toolbar¶

Mesh Edit Mode tools:

Select geometry by dragging a box.

Select geometry by dragging a circle.

Select geometry by drawing a lasso.

Change the location of the 3D Cursor.

Change the scale of an object by controlling its cage.

Tool to adjust the objects translation, rotations and scale.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

Measure distances in the scene.

Rotates a bone around its local Y axis.

Creates a new bone connected to the last selected joint.

Creates a new bone between the last selected joint and the mouse position.

---

## Toolbar¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/curves/tools/toolbar.html

**Contents:**
- Toolbar¶

Curve Edit Mode tools:

Select objects by dragging a box.

All objects that intersect the box will be selected.

Select objects by dragging a circle. All objects that intersect the path of the circle will be selected.

Select objects by drawing a lasso.

Change the location of the 3D Cursor.

Change the scale of an object by controlling its cage.

Tool to adjust the objects translation, rotations and scale.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

Measure distances in the scene.

Free-hand drawing of new curves.

Construct and edit splines.

Extrude the curve by adding new control points.

Control the radius value of the control points.

Control the rotation value of the control points around the curve’s axis.

Move selected control points in pseudo-random directions.

---

## Toolbar¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/object/tools/toolbar.html

**Contents:**
- Toolbar¶

Select objects by dragging a box. All objects that intersect the box will be selected.

Select objects by dragging a circle. All objects that intersect the path of the circle will be selected.

Select objects by drawing a lasso.

Change the location of the 3D Cursor.

Change the scale of an object by controlling its cage.

Tool to adjust the objects translation, rotations and scale.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

Measure distances in the scene.

Interactively add a cube mesh object.

Interactively add a cone mesh object.

Interactively add a cylinder mesh object.

Interactively add a UV sphere mesh object.

Interactively add an icosphere mesh object.

---

## Toolbar¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/uv/tools/toolbar.html

**Contents:**
- Toolbar¶

Select UVs by dragging a box.

Select UVs by painting on it.

Select UVs by drawing a lasso.

Change the location of the 2D Cursor.

Tool to adjust the UVs translation, rotation and scale.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

The Rip tool separates UV faces from each other.

The Grab tool moves UVs around using a brush.

The Relax tool makes UVs more evenly distributed using a brush.

The Pinch tool moves UVs toward the brush’s center.

---

## Toolbar¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/curves_new/tools/toolbar.html

**Contents:**
- Toolbar¶

Curves Edit Mode tools:

Select objects by dragging a box.

All objects that intersect the box will be selected.

Select objects by dragging a circle. All objects that intersect the path of the circle will be selected.

Select objects by drawing a lasso.

Change the location of the 3D Cursor.

Change the scale of an object by controlling its cage.

Tool to adjust the objects translation, rotations and scale.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

Measure distances in the scene.

Free-hand drawing of new curves.

Control the radius value of the control points.

Control the rotation value of the control points around the curve’s axis.

---

## Toolbar¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/tools/toolbar.html

**Contents:**
- Toolbar¶

Mesh Edit Mode tools:

Select geometry by dragging a box.

Select geometry by dragging a circle.

Select geometry by drawing a lasso.

Change the location of the 3D Cursor.

Change the scale of an object by controlling its cage.

Tool to adjust the objects translation, rotations and scale.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

Measure distances in the scene.

Interactively add a cube mesh object.

Interactively add a cone mesh object.

Interactively add a cylinder mesh object.

Interactively add a UV sphere mesh object.

Interactively add an icosphere mesh object.

Extrude the selected region together freely or along an axis.

Extrudes region and dissolves overlapping geometry.

Extrude Region along their local normal.

Extrude each individual element along their local normal.

Extrude selected vertices, edges or faces towards the mouse cursor.

Inset selected faces.

Create a bevel from the selected elements.

Create a loop cut along the mesh.

Add two edge loops on either side of selected loops.

Create a knife cut in the mesh. Press enter to confirm the cut.

Create geometry by adding vertices one by one.

Create new geometry by extruding and rotating.

Flatten angles of selected vertices.

Randomize selected vertices.

Slide edge along a face.

Slide vertex along an edge.

Move the selected vertices along their normals.

Move the selected elements away from/towards the pivot point.

Shear selected elements.

Move vertices outwards in a spherical shape around object center.

Rip Polygons and move the result.

Extend vertices and move the result.

---

## Tools¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/point_cloud/tools.html

**Contents:**
- Tools¶

Select geometry by dragging a box.

Select geometry by dragging a circle.

Select geometry by drawing a lasso.

Change the location of the 3D Cursor.

Change the scale of an object by controlling its cage.

Tool to adjust the objects translation, rotations and scale.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

Measure distances in the scene.

---

## Tool Settings¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/object/tools/tool_settings.html

**Contents:**
- Tool Settings¶
- Options¶
  - Transform¶

Object Mode and Pose Mode

Sidebar ‣ Tool ‣ Options

Directly transforms the object’s origin. This only works for objects with data which can be transformed; i.e. it will not work on object lights.

When enabled, the object axes are displayed.

Take care using this option since it transforms the object-data which may cause linked duplicates to be moved unintentionally.

Changing the object location and the object-data may impact modifiers, constraints and keyframe animation.

If you are only temporarily setting the pivot point, use the 3D cursor instead.

Changes the position of the object’s origin relative to another point during transformation. In other words, the pivot point and the origin cannot share the same location. This will not affect the object local transforms, just its position in world space.

In the examples below, a comparison of the scaling and rotation of objects, when Location is enabled (middle) and disabled (right).

Transforms Parent Objects while leaving their children objects unaffected.

---

## Tool Settings¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/tools/tool_settings.html

**Contents:**
- Tool Settings¶
- Options¶
  - Transform¶
    - Mirror¶
    - Topology Mirror¶
    - Auto Merge¶
  - UVs¶

Sidebar ‣ Tool tab ‣ Options panel

Adjust geometry attributes like UVs and Color Attributes while transforming.

Merge attributes connected to the same vertex while using Correct Face Attributes.

Keeping UVs connected is useful for organic modeling, but not for architectural modeling.

The Mirror options enable symmetric transformations of mesh elements (vertices, edges, or faces) along the selected axis. When an element is transformed, its exact mirrored counterpart (in local space), if present, is transformed correspondingly to maintain symmetry.

For the Mirror tool to function correctly, mirrored vertices must be precisely aligned with their counterparts. If vertices are not accurately positioned at their mirror locations, the Mirror Axis will not recognize them as mirrored. For meshes with visual symmetry but differing topology, enabling Topology Mirror can address this limitation.

Strict alignment requirements can make Mirror challenging to use. The Mirror Modifier offers an alternative, automatically handling symmetry.

Topology Mirror determines mirrored vertices by analyzing their relationships with other vertices in the mesh, rather than relying solely on vertex positions. By evaluating the overall topology, this feature allows non-symmetrical vertices to be treated as mirrored.

Topology Mirror requires at least one Mirror Axis to be enabled.

Topology Mirror is most effective with detailed geometry. Simple meshes, such as cubes or UV spheres, may produce inconsistent results.

This example demonstrates how to use Topology Mirror effectively:

Open a new Blender scene. Delete the default cube and add a Monkey object in the 3D Viewport.

Press Tab to switch to Edit Mode.

Disable all Mirror axes and move one of the Monkey object’s vertices slightly.

Enable the X Axis Mirror option but leave Topology Mirror disabled. Move the same vertex again. The X Axis Mirror will not affect the mirrored vertices, as they are not perfectly aligned.

Enable Topology Mirror and move the same vertex once more. The X Axis Mirror will now mirror the other vertex, even though they are not perfectly positioned.

Sidebar ‣ Tool ‣ Options ‣ Auto Merge

When enabled, as soon as a vertex moves closer to another one than the Threshold setting, they are automatically merged. This option affects interactive operations only (tweaks made in the Adjust Last Operation panel are considered interactive too). If the exact spot where a vertex is moved contains more than one vertex, then the merge will be performed between the moved vertex and one of those.

Detects the intersection of each transformed edge, creating a new vertex in place and sectioning the edge and the face if any.

Defines the maximum distance between vertices that are merged.

Automatically recalculates the UV unwrapping every time an edge has its seam property changed. Note, this is different than the Live Unwrap option in the UV Editor.

---

## Tool System¶

**URL:** https://docs.blender.org/manual/en/latest/interface/tool_system.html

**Contents:**
- Tool System¶
- Toolbar¶
- Pop-Up Toolbar¶
- Quick Favorites¶
- Changing Tools¶
  - Fallback Tool¶
  - Cycling Tools¶
- Properties¶

Tools are accessed from the Toolbar.

This is a general introduction to tools. Individual tools have their own documentation.

There can only be one active tool per Workspace and mode. This tool is remembered: if you’re in Edit Mode and have the Extrude tool selected, then switch to Object Mode (which has no Extrude tool) and back to Edit Mode, the Extrude tool will still be active.

Most tools are controlled using just LMB, though some also have modifier keys (shown in the Status Bar while using the tool). This can all be customized in the Keymap Preferences.

Some tools define gizmos (Shear and Spin for example) to help control them.

Expanded tool group.¶

The Toolbar contains buttons for the various tools. Buttons with a small triangle in their bottom right corner are tool groups which can be opened by holding LMB on them for a moment (or dragging LMB to open them instantly).

Hovering your cursor over a tool for a short time will show its name, while hovering longer will show the full tooltip.

Resizing the Toolbar horizontally will display the icons with two columns. Expanding it further will display the icon and its text.

Pressing Shift-Spacebar will pop up a small toolbar right at your cursor for faster access. The shortcuts for selecting the tools are displayed on the right.

Alternatively, you can map this action to Spacebar in the Keymap Preferences. Then you’ll be able use Spacebar like a modifier key (similar to holding Ctrl or Shift). For example, you can press Spacebar T for Transform, Spacebar D for Annotate, Spacebar M for Measure and so on. See Spacebar Action.

The Quick Favorites menu gathers your favorite tools. Any tool or menu item can be added to this pop-up menu via its context menu.

If you have Alt Click Tool Prompt enabled in the Keymap Preferences, tapping Alt will display a tool prompt in the Status Bar. You can then press a key to select the corresponding tool, or tap Alt again to cancel the prompt.

The fallback tool is the one that’s selected by default (so the one at the top of the Toolbar). You can change it by either holding LMB on the toolbar button or pressing Alt-W to get a pie menu.

If you bind a key to a tool which is part of a group, you can enable the Cycle option in the keymap editor. Successive presses will then cycle through the tools in that group.

This is enabled by default for the selection tools in the 3D Viewport, for example: pressing W will cycle between Select Box, Select Circle and so on.

Tools can have their own settings, which are available from multiple places:

The Tool ‣ Active Tool panel in the Sidebar N.

The Active Tool tab in the Properties editor.

The Tool Settings region below the area header.

---

## Topbar¶

**URL:** https://docs.blender.org/manual/en/latest/interface/window_system/topbar.html

**Contents:**
- Topbar¶
- Menus¶
  - Blender Menu¶
  - File Menu¶
  - Edit Menu¶
  - Render Menu¶
  - Window Menu¶
  - Help Menu¶
- Workspaces¶
- Scenes & Layers¶

Open the Splash Screen.

Opens a menu displaying the following information about Blender:

Version: The Blender version.

Date: Date when Blender was compiled.

Hash: The Git Hash of the build. This can be useful to give to support personnel when diagnosing a problem.

Branch: Optional branch name.

Windowing Environment: On Linux, this will show either Wayland or X11 depending on the windowing environment that Blender is running on.

Donate: Open Blender’s Development Fund website.

What’s New: Open the latest release notes.

Credits: Open the credits webpage.

License: Open the license webpage.

Blender Store: Open the Blender Store website.

Blender Website: Open main Blender website.

Install a new application template.

The options to manage files are:

Clears the current scene and loads the selected application template.

Displays a list of the most recently opened blend-files. Hovering over items will show a preview, and information about the blend-file. Select any of the file names in the list to open that blend-file.

Removes items from the recent files list.

Reopens the current file to its last saved version.

Options to recover a blend-file from the accidentally closing Blender or a crash. See:

Save the current blend-file.

Opens the File Browser to specify file name and location of save.

Saves a copy of the current file.

Save the current Blender file with a numerically incremented name that does not overwrite any existing files.

Links data from an external blend-file (library) to the current one. The editing of that data is only possible in the external library. Link and Append are used to load in only selected parts from another file. See Linked Libraries.

Appends data from an external blend-file to the current one. The new data is copied from the external file, and completely unlinked from it.

Tools for managing data-block previews.

Blender can use information stored in a variety of other format files which are created by other graphics programs. See Import/Export.

Normally you save your work in a blend-file, but you can export some or all of your work to a format that can be processed by other graphics programs. See Import/Export.

Invokes all configured exporters for all collection.

External data, like texture images and other resources, can be stored inside the blend-file (packed) or as separate files (unpacked). Blender keeps track of all unpacked resources via a relative or absolute path. See pack or unpack external data.

Pack all currently used external files into the blend-file and automatically pack any files that are added later. Unchecking this option will only stop the automatic packing for new files; it won’t unpack existing ones.

Pack all used external files into the blend-file. After running this operator and saving the blend-file, the external files will no longer be used – any changes in them will no longer be reflected in the blend-file, and you are free to move or delete them.

Export previously packed files back to external ones. You can choose whether to reuse existing external files or overwrite them.

Pack data-blocks that are linked from an external blend-file into the current one.

Export previously packed data-blocks back to external blend-files. Existing blend-files are overwritten.

Make all paths to external files relative to the current blend-file.

Make all paths to external files absolute (= full path from the system’s root).

This option is useful to check if there are links to unpacked files that no longer exist. After selecting this option, a warning message will appear in the Info editor’s header. If no warning is shown, there are no missing external files.

In case you have broken links in a blend-file, this can help you to fix the problem. A File Browser will show up. Select the desired directory (or a file within that directory), and a search will be performed in it, recursively in all contained directories. Every missing file found in the search will be recovered. Those recoveries will be done as absolute paths, so if you want to have relative paths you will need to select Make Paths Relative.

Recovered files might need to be reloaded. You can do that one by one, or you can save the blend-file and reload it again, so that all external files are reloaded at once.

Opens a dialog to remove unused data-blocks from both the current blend-file or any Linked Data (cannot be undone). See the Outliner for more information.

Opens a pop-up window of the Outliner in Unused Data mode which lists data-blocks and other data that are unused and/or will be lost when the file is reloaded. It includes data-blocks which have only a fake user. You can add/remove the Fake User by clicking on cross/tick icon on the right side of the Outliner.

This menu manages the startup file which is used to store the default scene, workspace, and interface displayed when creating a new file.

Initially this contains the startup scene included with Blender. This can be replaced by your own customized setup.

Saves the current blend-file as the startup file.

Restores the default startup file and preferences.

When an Application Templates is in use the following operators are shown:

Loads the default settings to the original Blender settings without the changes made from the current application template.

Loads the default settings to the original application template.

Managing Preferences.

Closes Blender. The current scene is saved to a file called “quit.blend” in Blender’s temporary directory (which can be found on the “File Paths” tab of the Preferences).

Find a menu based on its name.

Execute an operator based on its name (Developer Extras only).

Rename the active object or node; see Rename tool for more information.

Renames multiple data types at once; see Batch Rename tool for more information.

Prevents selecting objects that are in a different mode than the current one.

This option can prevent accidental mode changes, such as when you’re trying to select a bone in Pose Mode to animate it, but instead click a piece of background scenery (which would normally select that piece and switch to Object Mode).

You may want to disable Lock Object Modes for example when weighting rigged objects or sculpting/painting where you intentionally want to switch between objects in different modes.

Open the Preferences window.

Render the active scene at the current frame.

Render the animation of the active scene.

Rendering Animations for details.

If a Sequencer Scene exists that differs from the active scene, render that scene instead.

Render the animation of the Sequencer Scene.

Both of the sequencer render options automatically set the Show Sequencer Scene toggle in the image editor Render Result after rendering.

Mix the scene’s audio to a sound file.

Rendering audio for details.

Show the Render window. (Press again to switch back to the main Blender window.)

Playback rendered animation in a separate player.

Animation player for details.

Preferences for selecting a different animation player than the default one.

Lock interface during rendering in favor of giving more memory to the renderer.

Create a new window by copying the current window.

Create a new window with its own workspace and scene selection.

Toggle the current window fullscreen.

Switch to the next workspace.

Switch to the previous workspace.

Choose whether the Status Bar at the bottom of the window should be displayed.

Capture a picture of the current Blender window. A File Browser will open to choose where the screenshot is saved.

Capture a picture of the selected Editor. Select the Editor by clicking LMB within its area after running the operator. A File Browser will open to choose where the screenshot is saved.

This set of tabs is used to switch between Workspaces, which are essentially predefined window layouts.

These data-block menus are used to select the current Scene and View Layer.

---

## Transforms¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/transforms.html

**Contents:**
- Transforms¶
- Move¶
- Rotate¶
- Scale¶
- Transform¶
- Tool Settings¶

Tool to adjust the objects translation, rotations and scale.

Each tool has the following settings to change how the unmasked mesh will be transformed.

How the transformation is going to be applied to the target.

Applies the transformation to all vertices in the mesh.

Applies the transformation while dynamically simulating elasticity. Instead of applying this to all vertices, it uses the radius of the cursor as the area of effect.

---

## Transform Orientation¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/controls/orientation.html

**Contents:**
- Transform Orientation¶
- Orientations¶
  - Examples¶
  - Custom Orientations¶
    - Create Orientation¶
    - Delete Orientation¶

Object and Edit Modes

Header ‣ Transform Orientation

The Transform Orientation determines the orientation of the Object Gizmo. Changing this orientation can make it easier to perform transformations in the direction you want.

With the default Global transform orientation (left) it’s tricky to move the plane in the direction it’s facing, but with Local (right) it’s easy.¶

The Transform Orientation can be changed using a selector in the 3D Viewport’s header:

Transform Orientation selector.¶

The orientation can also be changed temporarily while performing a hotkey-based transformation with axis locking. For example, if you first press G to start moving an object, then X to lock to the orientation’s X axis, and finally X a second time, you’ll get a lock to an alternative orientation: the Local orientation if it was Global previously, and the Global orientation otherwise.

In addition to the builtin orientations, you can also define your own (see Custom Orientations below).

Align the transformation axes to world space. The world axes are shown by the Navigation Gizmo in the top right corner of the viewport, as well as the Grid Floor.

Align the transformation axes to the active object’s orientation.

In Edit Mode, orient the transformation axes so that the Z axis of the gizmo matches the average Normal of the selected elements.

In Object Mode, this is equivalent to Local orientation.

Orient the transformation axes to visualize the workings of the object’s Rotation Mode. This is specifically useful for the Euler modes, where the object is rotated one axis at a time: the rotation axes don’t stay perpendicular to each other and might even overlap, a phenomenon known as gimbal lock that complicates animation.

Align the transformation axes to the view (meaning they change as you orbit around):

Z: Towards/Away from the screen

Align the transformation axes to the 3D Cursor.

Align the transformation axes to the Parent.

Default cube with Global transform orientation selected.¶

Rotated cube with Global orientation, gizmo has not changed.¶

Local orientation, gizmo matches the object’s rotation.¶

Normal orientation, in Edit Mode.¶

Gimbal transform orientation.¶

View transform orientation.¶

Parent transform orientation. Cube parented to rotated empty.¶

Object and Edit Modes

Header ‣ Transform Orientation

You can define custom transform orientations using objects or mesh elements. Custom orientations defined from an object use the Local orientation of that object, whereas those defined from mesh elements (vertices, edges, faces) use the average Normal orientation of those elements.

Transform Orientation panel.¶

The Transform Orientation panel, found in the header of the 3D Viewport, can be used to select, add, remove, and rename transform orientations.

The default name for these orientations is derived from the selection. If it’s an object it will take that object’s name, if it’s an edge it will be titled “Edge”, and so on.

To create a custom orientation, select an object or mesh element(s) and click the “+” button in the Transform Orientation panel.

Create Orientation Adjust Last Operation panel.¶

Right after creating the orientation, the Create Orientation Adjust Last Operation panel gives a few options:

Text field for naming the new orientation.

The new orientation will be aligned to the view space.

The new orientation stays selected.

If the new orientation is given an existing name, a suffix will be added to it’s name to avoid overwriting the existing orientation, unless Overwrite Previous is checked, in which case it will be overwritten.

To delete a custom orientation, simply select it and click the × button.

---

## Transform Pivot Point¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/controls/pivot_point/index.html

**Contents:**
- Transform Pivot Point¶
- Pivot Types¶

Object Mode and Edit Mode

Header ‣ Transform Pivot Point

The Pivot Point determines the location of the Object Gizmo. Changing this location can make it easier to perform transformations around the point you want.

With the default “Median Point” pivot point (left) it’s tricky to bring the second wheel spoke into place, but with “3D Cursor” (right) it’s easy.¶

The Pivot Point can be changed using a selector in the 3D Viewport’s header:

---

## Trim Gesture Tools¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tools/trim_tools.html

**Contents:**
- Trim Gesture Tools¶
- Box Trim¶
- Lasso Trim¶
- Line Trim¶
- Polyline Trim¶
- Tool Settings¶

Trim gesture tools add or remove geometry based on a selection area. This tool is especially useful for sketching an early base mesh for further sculpting with the voxel remesher.

Using Lasso Trim set to Join¶

The symmetrized mesh.¶

Sculpting with voxel remeshing.¶

New geometry is assigned to a new Face Set. When removing geometry, the new interior geometry along the selection will be assigned a new face set instead.

It is not recommended to use this tool on a mesh above 100k vertices when using Difference or Union as the Trim Mode with the Exact Solver. This tool is using a Boolean operation so it might take a long time to process. For higher resolution meshes it is recommended to instead use the Line Project tool or the Fair Positions mode of the Edit Face Set tool to trim geometry.

Performs a Boolean operation based on the area defined by a box gesture.

Performs a Boolean operation based on the area defined by a lasso gesture.

Performs a Boolean operation based on the area defined by a line gesture.

The Line Trim tool does not support adding geometry. Only Difference mode is supported.

Toolbar ‣ Polyline Trim

Performs a Boolean operation based on the area defined by a polyline gesture.

Algorithm used to calculate the Boolean intersections.

Uses a complex solver which offers the best results and has full support for overlapping geometry; however, this solver is much slower.

Uses a simple solver which offers the good performance; however, this solver lacks support for overlapping geometry.

Uses a solver that is usually fastest but only works on Manifold meshes, (plus the special case of Difference with a plane).

Geometry can be either added or removed by choosing one of these modes.

Removes geometry, filling any holes that are created.

Creates a geometry and joins any intersections with existing geometry.

Similar to Union but joins the mesh as separate geometry, without performing any Boolean operations with existing geometry.

The method used to orientate the trimming shape.

Use the view to orientate the trimming shape.

Use the surface normal to orientate the trimming shape.

Aligns new geometry orthogonally for 90 degree angles in depth.

Aligns new geometry with the perspective of the current view for a tapered result.

Use cursor location and radius for the dimensions and position of the trimming shape. If not set, the tool uses the full depth of the object from the camera view.

---

## Trim Tool¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tools/trim.html

**Contents:**
- Trim Tool¶
- Tool Settings¶
- Usage¶

The Trim tool delete points in between intersecting strokes.

Mark newly created End Caps as Flat.

Determine the threshold for stroke intersections.

Draw a dotted line around the strokes you want to trim. After releasing the mouse button all the points on the selected strokes will be deleted until another intersecting stroke is found.

Lasso Selecting the strokes to be trimmed.¶

---

## Undo & Redo¶

**URL:** https://docs.blender.org/manual/en/latest/interface/undo_redo.html

**Contents:**
- Undo & Redo¶
- Undo¶
- Redo¶
- Adjust Last Operation¶
- Undo History¶
- Repeat Last¶
- Repeat History¶

The tools listed below will let you roll back an accidental action, redo your last action, or let you choose to recover to a specific point, by picking from a list of recent actions recorded by Blender.

If you want to undo your last action, just press Ctrl-Z.

Memory & Limits Preferences to change undo settings.

To roll back the Undo action, press Shift-Ctrl-Z.

Edit ‣ Adjust Last Operation…

You can tweak the parameters of an operator after running it. In editors that support it, there is a “head-up display” panel in the bottom left based on the last performed operation. Alternatively, you can create a pop-up with F9 which does the same thing.

For example, if your last operation was a rotation in Object Mode, Blender will show you the last value changed for the angle (see Fig. Rotation (Object Mode, 60 degrees). left), where you can change your action back completely by typing Numpad0 in the Angle Field. There are other useful options, based on the operator, and you cannot only Undo actions, but change them completely using the available options.

If you are in Edit Mode, Blender will also change its contents based on your last action taken. In the second example (on the right), the last operation was a Move in Object Mode; but a Scale on a Face in Edit Mode, and, as you can see, the contents of Adjust Last Operation are different, because of the mode (Edit Mode) (See Fig. Scale (Edit Mode, Resize face). right).

Rotation (Object Mode, 60 degrees).¶

Scale (Edit Mode, Resize face).¶

Some operations produce particularly useful results by using Adjust Last Operation. For example, adding a Circle in the 3D Viewport; if you reduce the Vertices to three, you get a perfect equilateral triangle.

The Adjust Last Operation region can be hidden by View ‣ Adjust Last Operation.

The Undo History menu.¶

There is also an Undo History of the last actions taken, recorded by Blender.

The top of the list corresponds to the most recent actions. A small icon of a dot next to one of the entries indicates the current status. Rolling back actions using the Undo History feature will take you back to the action you choose. Much like how you can alternate between going backward in time with Undo and then forward with Redo, you can hop around on the Undo timeline as much as you want as long as you do not make a new change. Once you do make a new change, the Undo History is truncated at that point. Selecting one of the entries in the list takes the current status to that position.

The Repeat Last feature will repeat your last action when you press Shift-R.

In the example images below, we duplicated a Monkey mesh and moved it a bit. Using repeat Shift-R, the Monkey was duplicated and moved a second time.

After a Shift-D and move.¶

Edit ‣ Repeat History…

The Repeat History menu.¶

The Repeat History feature will present you a list of the last repeated actions, and you can choose the actions you want to repeat. It works in the same way as the Undo History, explained above, but the list contains only repeated actions.

When you quit Blender, the complete list of user actions will be lost, even if you save your file before quitting.

Troubleshooting section on Recovering your lost work.

---

## UV Operators¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/editing/uv.html

**Contents:**
- UV Operators¶
- Unwrap¶
  - Options¶
- Smart UV Project¶
  - Options¶
- Lightmap Pack¶
  - Options¶
- Follow Active Quads¶
  - Options¶
- Cube Projection¶

Blender offers several ways of mapping UVs, going from simple ones that merely project the mesh’s vertices onto a plane to more advanced ones.

UV ‣ Unwrap Angle Based, Unwrap Conformal, Unwrap Minimum Stretch

UV ‣ Unwrap ‣ Unwrap Angle Based, Unwrap Conformal, Unwrap Minimum Stretch

Cuts the selected faces along their seams, flattens them, and lays them out on the UV map. Previously existing UV coordinates are overwritten. Useful for organic shapes.

Result of unwrapping Suzanne.¶

The Adjust Last Operation panel allows fine control over how the mesh is unwrapped:

Uses Angle Based Flattening (ABF). This method gives a good 2D representation of a mesh.

Uses Least Squares Conformal Mapping (LSCM). This usually results in a less accurate UV mapping than Angle Based, but performs better on simpler objects.

Uses Scalable Locally Injective Mapping (SLIM). This tries to minimize distortion for both areas and angles.

Virtually fill holes in the mesh before unwrapping, to better avoid overlaps and preserve symmetry.

Use the new vertex positions that were calculated by the Subdivision Surface Modifier (rather than the original positions from before any modifiers are run).

Adjusts the UV mapping to account for the aspect ratio of the image associated with the material. This ensures that UVs are scaled correctly when unwrapping onto non-square textures.

For this option to work, the mesh must have a material with an Image Texture node, and this node must be selected in the Shader Editor.

Number of iterations for the Minimum Stretch method, where each iteration reduces the distortion further.

Disallow flipping faces. Allowing it sometimes results in less distortion when there are pins.

Lets you specify a vertex group to manually influence the size of certain faces in the UV map. Faces around high-weight vertices will take up more space in the UV map than ones around low-weight vertices.

When enabling this option, two more appear:

The name of the vertex group to use.

A global factor to multiply all the weights by. A bigger number will result in a more exaggerated difference between high-weight and low-weight areas.

The meaning of the Margin parameter, which determines the size of the empty space between UV islands.

The Margin is a more or less arbitrary measure with no direct relation to the sizes of the UV islands or the texture.

As above, but without the internally calculated scaling factor.

The Margin is a fraction of the UV bounds. This means that, if you have a 1024x1024 texture and set the Margin to 1/1024, each UV island will have a margin of 1 pixel around it (and islands will be no closer than 2 pixels to each other).

How much empty space to leave between islands. Controlled by Margin Method.

3D Viewport, UV Editor

UV ‣ Unwrap ‣ Smart UV Project

Examines the angles between the selected faces, cuts them along any sharp edges, then projects each separated group of faces along its average normal and lays it out on the UV map. You can also set up seams for additional cutting. This is a good method for, say, mechanical objects or architecture.

Smart UV project on a truncated pyramid.¶

The Adjust Last Operation panel allows fine control over how the mesh is unwrapped:

The maximum allowed angle between the normals of adjacent faces before they’re split off from each other. A low limit will create lots of small UV islands with little distortion, while a high limit will create a few large islands with potentially more distortion.

The meaning of the Island Margin parameter, which determines the size of the empty space between UV islands.

The Island Margin is a more or less arbitrary measure with no direct relation to the sizes of the UV islands or the texture.

As above, but without the internally calculated scaling factor.

The Island Margin is a fraction of the UV unit square. This means that, if you have a 1024x1024 texture and set the Island Margin to 1/1024, each UV island will have a margin of 1 pixel around it (and islands will be no closer than 2 pixels to each other).

Automatically rotate to avoid wasting space.

Rotate islands to be aligned horizontally.

Rotate islands to be aligned vertically.

How much empty space to leave between islands. Controlled by Margin Method.

With a value of 0, the projection vector of each face group is simply the average of its face normals. With a value of 1, it’s an average that’s weighted using the faces’ areas. Other values blend between the two.

Adjusts the UV mapping to account for the aspect ratio of the image associated with the material. This ensures that UVs are scaled correctly when unwrapping onto non-square textures.

For this option to work, the mesh must have a material with an Image Texture node, and this node must be selected in the Shader Editor.

Stretches the resulting UV map to fill the complete texture.

3D Viewport, UV Editor

UV ‣ Unwrap ‣ Lightmap Pack

Places each selected face separately on the UV map. Lightmaps are commonly used for baking lighting information into a texture for use in realtime rendering – as such, they prioritize using as much of the texture as possible, typically resulting in a disconnected and distorted UV map that would be unsuitable for manual texturing work.

The Adjust Last Operation panel allows fine control over how the mesh is unwrapped:

Only unwraps the selected faces.

Unwraps the whole mesh.

You can use Multi-Object Editing to generate UV maps for multiple meshes at the same time. When Share Texture Space is enabled, the UV maps won’t overlap each other, so that you can later use the same lightmap texture for all the meshes.

Creates a new UV map instead of overwriting the currently selected one. See UV Maps.

Higher values result in a UV map that wastes less space (but also takes longer to calculate).

How much empty space to leave between the faces in the UV map.

3D Viewport, UV Editor

UV ‣ Unwrap ‣ Follow Active Quads

Starts from the active quad and recursively attaches its neighboring, selected mesh quads to its pre-existing UV quad. Non-quad faces are ignored.

Because the active quad’s UV layout is left unchanged, you’ll typically want to make sure it has the same shape in the UV map as on the mesh before running this unwrap (e.g. by running another type of unwrap on just that face). Otherwise, the distortion will spread to all the other faces.

The resulting UV map may go out of bounds. You can fix this by manually scaling it down or by using Pack Islands.

The Adjust Last Operation panel allows fine control over how the mesh is unwrapped:

How to calculate the lengths of the UV edges for the newly attached quads.

Give each new UV edge the same length as the UV edge it’s extending, regardless of its length on the mesh.

Give each new UV edge a length that’s proportional to its length on the mesh.

Give each new UV edge a length that’s proportional to the average edge length in its edge ring on the mesh.

3D Viewport, UV Editor

UV ‣ Unwrap ‣ Cube Projection

Projects each selected face onto the most suitable side of a virtual cube, then places all these sides in the UV map, overlapping each other. If you don’t want them to overlap, you can use Pack Islands.

The cube is centered on the Transform Pivot Point and aligned to the mesh’s local axes.

The Adjust Last Operation panel allows fine control over how the mesh is unwrapped:

The size of the cube to project onto.

Adjusts the UV mapping to account for the aspect ratio of the image associated with the material. This ensures that UVs are scaled correctly when unwrapping onto non-square textures.

For this option to work, the mesh must have a material with an Image Texture node, and this node must be selected in the Shader Editor.

Moves any out-of-bounds UVs to the nearest border.

Stretches the resulting UV map to fill the complete texture.

3D Viewport, UV Editor

UV ‣ Unwrap ‣ Cylinder Projection

Projects the selected faces onto a virtual cylinder, then unrolls that cylinder. The cylinder is centered on the Transform Pivot Point, which is normally the averaged-out position of the selected faces; however, you can also move it to a different place using e.g. the 3D Cursor.

The Adjust Last Operation panel allows fine control over how the mesh is unwrapped:

The direction of the cylinder’s central axis.

Use an axis that’s perpendicular to the viewing direction in the 3D Viewport. If Align is Polar ZX, use the vertical axis of the viewing plane; if it’s Polar ZY, use the horizontal one.

Use an axis that’s parallel to the viewing direction in the 3D Viewport. Depending on Align, the cylinder will be rotated by 90° around its axis and the UV map will be shifted horizontally by a quarter.

Use the object’s local Z axis. Depending on Align, the cylinder will be rotated by 90° around its axis and the UV map will be shifted horizontally by a quarter.

How to handle vertices that lie on the cylinder’s central axis.

Place all UV versions of the vertex at the same U coordinate. This tends to result in heavily distorted UV faces.

Place each UV version of the vertex at a U coordinate that minimizes distortion.

Unwrapping the top of a dome.¶

Cut the mesh along its seams before projecting.

Half the height of the cylinder (i.e. not its radius; we’re only using the cylinder for projection, so its radius doesn’t matter).

Adjusts the UV mapping to account for the aspect ratio of the image associated with the material. This ensures that UVs are scaled correctly when unwrapping onto non-square textures.

For this option to work, the mesh must have a material with an Image Texture node, and this node must be selected in the Shader Editor.

Moves any out-of-bounds UVs to the nearest border.

Stretches the resulting UV map to fill the complete texture.

3D Viewport, UV Editor

UV ‣ Unwrap ‣ Sphere Projection

Projects the selected faces onto a virtual sphere, then flattens that sphere much like a world map: the latitude lines vertical and the longitude lines evenly spaced. This is useful for texturing spherical shapes such as eyes or planets.

The sphere is centered on the Transform Pivot Point, which is normally the averaged-out position of the selected faces; however, you can also move it to a different place using e.g. the 3D Cursor.

Using an equirectangular image with a Sphere Projection.¶

The Adjust Last Operation panel allows fine control over how the mesh is unwrapped:

The direction of the sphere’s vertical axis.

Use an axis that’s perpendicular to the viewing direction in the 3D Viewport. If Align is Polar ZX, use the vertical axis of the viewing plane; if it’s Polar ZY, use the horizontal one.

Use an axis that’s parallel to the viewing direction in the 3D Viewport. Depending on Align, the sphere will be rotated by 90° around its vertical axis and the UV map will be shifted horizontally by a quarter.

Use the object’s local Z axis. Depending on Align, the sphere will be rotated by 90° around its vertical axis and the UV map will be shifted horizontally by a quarter.

How to handle vertices that lie on the sphere’s vertical axis. (See Cylinder Projection for an example.)

Place all UV versions of the vertex at the same U coordinate. This tends to result in heavily distorted UV faces.

Place each UV version of the vertex at a U coordinate that minimizes distortion.

Cut the mesh along its seams before projecting.

Adjusts the UV mapping to account for the aspect ratio of the image associated with the material. This ensures that UVs are scaled correctly when unwrapping onto non-square textures.

For this option to work, the mesh must have a material with an Image Texture node, and this node must be selected in the Shader Editor.

Moves any out-of-bounds UVs to the nearest border.

Stretches the resulting UV map to fill the complete texture.

UV ‣ Project from View

Projects the selected faces onto the view plane. The UV map essentially becomes a wireframe picture of the mesh, taken in the 3D Viewport at the current viewing angle. Use this option if you are using a picture of a real object as a texture. You will get stretching in areas where the model recedes away from you.

The Adjust Last Operation panel allows fine control over how the mesh is unwrapped:

Use an Orthographic projection instead of Perspective.

Map the borders of the image that would be rendered through the current camera to the borders of the UV map. This option only has an effect when viewing the scene through the camera; see Viewing the Active Camera.

Adjusts the UV mapping to account for the aspect ratio of the image associated with the material. This ensures that UVs are scaled correctly when unwrapping onto non-square textures.

For this option to work, the mesh must have a material with an Image Texture node, and this node must be selected in the Shader Editor.

Moves any out-of-bounds UVs to the nearest border.

Stretches the resulting UV map to fill the complete texture.

UV ‣ Project from View (Bounds)

The same as Project from View, but with Scale to Bounds activated by default.

3D Viewport, UV Editor

Resets the UV layout of each selected face to fill the whole UV area.

---

## Vertex Paint Tools¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/vertex_paint/tools.html

**Contents:**
- Vertex Paint Tools¶

Tool to use for any of the vertex paint brushes.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

---

## Vertex Paint Tools¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/vertex_paint/tools.html

**Contents:**
- Vertex Paint Tools¶

Tool to use for any of the vertex paint brushes.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

---

## Viewport Display¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/type/domain/gas/viewport_display.html

**Contents:**
- Viewport Display¶
- Slice¶
- Grid Display¶
- Vector Display¶
- Advanced Gridlines Only¶

Factor that scales the thickness of the grid that is currently being displayed.

Interpolation method to use for the visualization of the fluid grid.

Linear interpolation between voxels. Gives good smoothness and speed.

Cubic interpolation between voxels. Gives smoothed high quality interpolation, but is slower.

No interpolation between voxels. Gives raw voxels.

Determines how many slices per voxel should be generated.

Renders only a single 2D section of the domain object.

Adjust slice direction according to the view direction.

Slice along the X/Y/Z axis.

Position of the slice relative to the length of the respective domain side.

Display gridlines to differentiate the underlying cells in the current slice of the fluid domain.

Use a specific color map for the visualization of the simulation field. This comes in handy during debugging or when making more advanced adjustments to the simulation. For instance, if the actual color of a fire simulation is barely visible in the viewport then changing the color profile can help to see the real size of the flame.

The simulation field used in the display options (e.g. density, fuel, heat).

Slice view of “fire” grid without color mapping.¶

Slice view of “fire” grid with color mapping.¶

Scale the selected simulation field by this value.

Visualization options for the vector fields.

Choose to display the vectors as “Streamlines”.

Choose to display the vectors as “Needles”.

Choose to display the vector field as “Marker-And-Cell Grid”.

Show an individual X/Y/Z component of the MAC grid.

Scale the display vectors by the magnitude of the vectors they represent.

The vector field represented by the display vectors (e.g. fluid velocity, external forces).

Scale the vectors by this size in the viewport.

Advanced coloring options for gridlines.

Color gridlines with flags.

Grid Display Only Highlight the cells with values of the displayed grid within the range. Values between the Lower Bound and Upper Bound (inclusive) are considered to be within the range.

Lower bound of the highlighting range.

Upper bound of the highlighting range.

Color used to highlight the cells.

Choose to highlight only a particular type of cells.

---

## Viewport Display¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/properties/display.html

**Contents:**
- Viewport Display¶

Armature ‣ Viewport Display

This controls the way the all the bones of the armature appear in the 3D Viewport. Individual bones can also can override this using bone Display Type.

Octahedral bone display.¶

B-Bone bone display.¶

Envelope bone display.¶

This is the default visualization, well suited for most of editing tasks. It materializes:

The bone root (“big” joint) and tip (“small” joint).

The bone “size” (its thickness is proportional to its length).

The bone roll (as it has a square section).

Note the 40° rolled Bone.001 bone.¶

This is the simplest and most non-intrusive visualization. It just materializes bones by sticks of constant (and small) thickness, so it gives you no information about root and tip, nor bone size or roll angle.

Note that Bone.001 roll angle is not visible (except by its XZ axes).¶

This visualization shows the curves of “smooth” multi-segmented bones; see the Bendy Bones for details.

An armature of B-Bones, in Edit Mode.¶

The same armature in Object Mode.¶

This visualization materializes the bone deformation influence. More on this in the bone page.

This simplest visualization shows the curves of “smooth” multi-segmented bones.

An armature of Wire, in Pose Mode.¶

The same armature in Edit Mode.¶

Displays the name of each bone.

When enabled, the default standard bone shape is replaced, in Object Mode and Pose Mode, by the shape of a chosen object (see Shaped Bones for details).

Draws bones in their configured colors. Disable to always draw bones in the default color. For more details see Bone Colors.

When enabled, the bones of the armature will always be shown on top of the solid objects (meshes, surfaces, …). I.e. they will always be visible and selectable (this is the same option as the one found in the Display panel of the Object data tab). Very useful when not in Wireframe mode.

When enabled, the (local) axes of each bone are displayed (only relevant for Edit Mode and Pose Mode).

The position for the axes display on the bone. Increasing the value moves it closer to the tip; decreasing moves it closer to the root.

Whether the Relationship Lines overlay should be drawn from each parent’s tail or head. The lines are always drawn towards the children’s heads.

---

## Weight Paint Tools¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/weight_paint/tools.html

**Contents:**
- Weight Paint Tools¶

For Grease Pencil Weight Paint modes each brush type is exposed as a tool, the brush can be changed in the Tool Settings. See Brush for more information.

Tool to use for any of the weight paint brushes.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

---

## Weight Paint Tools¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/weight_paint/tools.html

**Contents:**
- Weight Paint Tools¶

Tool to use for any of the weight paint brushes.

Applies a linear/radial weight gradient; this is useful at times when painting gradual changes in weight becomes difficult. Blends the weights of selected vertices with unselected vertices.

Example of the Gradient tool being used with selected vertices.¶

The gradient starts at the current selected weight value, blending out to nothing.

Lower values can be used so the gradient mixes in with the existing weights (just like with the brush).

The shape of the gradient.

Create gradient that forms a straight line.

Create gradient that forms a circle.

These are also available via shortcuts as the menu operators.

Sets the brush Weight as the weight selected under the cursor. The sampled weight is displayed in the tool settings.

Displays a list of possible vertex groups to select that are under the cursor.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

---

## Workspaces¶

**URL:** https://docs.blender.org/manual/en/latest/interface/window_system/workspaces.html

**Contents:**
- Workspaces¶
- Controls¶
- Default Workspaces¶
  - Additional Workspaces¶
- Save and Override¶
- Workspace Settings¶

Workspaces are essentially predefined window layouts. Each Workspace consists of a set of Areas containing Editors, and is geared towards a specific task such as modeling, animating, or scripting. You’ll typically switch between multiple Workspaces while working on a project.

Workspaces are located at the Topbar.¶

Click on the tabs to switch between workspaces. Double-click a tab to rename the workspace.

Adds a new workspace from a predefined template (e.g. Modeling, Sculpting, Compositing).

Makes a copy of the selected workspace, including its screen layout and editors.

Deletes the selected workspace. If it is the last workspace, it cannot be removed.

Moves the workspace tab to the first (front) or last (back) position in the tab list.

Activates the workspace immediately to the left of the current one.

Activates the workspace immediately to the right of the current one.

Removes all workspaces except the one that was right-clicked on.

Blender’s default startup shows the “Layout” workspace in the main area. This workspace is a general workspace to preview your scene and contains the following Editors:

3D Viewport on top left.

Outliner on top right.

Properties on bottom right.

Dopesheet on bottom left.

Blender’s ‘Layout’ Workspace with four editors.¶

3D Viewport (yellow), Outliner (green), Properties (blue) and Timeline (red).

Blender also has several other workspaces added by default:

For modification of geometry by modeling tools.

For modification of meshes by sculpting tools.

For mapping of image texture coordinates to 3D surfaces.

For coloring image textures in the 3D Viewport.

For specifying material properties for rendering.

For making properties of objects dependent on time.

For viewing and analyzing rendering results.

For combining and post-processing of images and rendering information.

For procedural modeling using Geometry Nodes.

For interacting with Blender’s Python API and writing scripts.

Blender has a couple additional Workspaces to choose from when adding a new Workspace:

General workspace to work with Grease Pencil.

Similar to “2D Animation” but contains a larger canvas.

For creating 2D masks for compositing or video editing.

For calculating camera motion and stabilizing video footage.

For sequencing together media into one video.

The workspaces are saved in the blend-file. When you open a file, enabling Load UI in the File Browser indicates that Blender should use the file’s screen layout rather than the current one.

A custom set of workspaces can be saved as a part of the Defaults.

When enabled, the current workspace will remember the currently selected scene. Then, whenever you activate the workspace, it’ll automatically switch back to that scene.

Switch to this Mode when activating the workspace.

The scene containing the edit that is used by the video sequence editor. See Sequencer Scene.

Sync the active scene and time based on the current scene strip in the video sequence editor. See Sequencer Scene.

Determines which add-ons are enabled in the active workspace. When unchecked, the global add-ons will be used. When checked, you can enable individual add-ons in the list below.

---
