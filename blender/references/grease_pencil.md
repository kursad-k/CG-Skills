# Blender - Grease Pencil

**Pages:** 27

---

## Blur Visual Effect¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/visual_effects/blur.html

**Contents:**
- Blur Visual Effect¶
- Options¶
- Example¶

The Blur Visual Effect applies a Gaussian blur to the object.

Number of blur samples (0 disabled the blur effect).

When enabled, the blur effect uses the focal plane distance of the actual camera to calculate the object blur. Only available in camera view.

Control the blur scale in pixels on the X and Y axis.

Control the Rotation of the blur.

---

## Colorize Visual Effect¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/visual_effects/colorize.html

**Contents:**
- Colorize Visual Effect¶
- Options¶
- Example¶

The Colorize Visual Effect applies different preset colorizing effects to the object.

Converts to a grayscale image.

Converts to a sepia tone image.

Converts to a posterize image with high contrast and brightness.

Add color transparency.

Allows to define a tint custom color.

Control the mix value.

---

## Color¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tool_settings/color.html

**Contents:**
- Color¶
- Palette¶

Controls the source of the stroke color. The mode can be pinned to the brush by enabling the Pin icon in the Tool Settings header.

Use the stroke/fill base color material.

Sets the primary brush color.

The color of the brush. See Color Picker.

The color transformation will be applied on the stroke and/or the fill color.

Only paint over strokes.

Only paint over fill areas.

Paint over strokes and fill areas.

Mixing factor between the selected color and the base material color.

Active Color Palette. See Color Palette.

---

## Data Properties¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/properties/data.html

**Contents:**
- Data Properties¶
- Layers¶
- Onion Skinning¶
- Settings¶
- Attributes¶
- Vertex Groups¶
- Custom Properties¶

Grease Pencil Object Data.¶

The Grease Pencil data-block menu can be used to link the data between objects.

Strokes can be grouped in 2D layers, a special Grease Pencil layers that help to organize the drawing order and visibility of the strokes. Layers can be organized into layer groups.

Onion skinning is used in animation to see several frames at once and make decisions or edits based on how the previous/next frames are drawn.

General settings for Grease Pencil strokes.

Layers can store Custom Attributes. The attributes are stored on the Layer domain.

For example, the Layer Adjustments are stored as layer attributes.

List view of all the attributes stored on the layers.

Name of the layer attribute.

The Data Type of the attribute.

Vertex groups can be used to assign a group or weighted group to some operator. An object can have several weight groups and can be assigned in Weight Paint Mode.

Create and manage your own properties to store data in the Grease Pencil’s data-block.

---

## Drawing Operations¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/editing.html

**Contents:**
- Drawing Operations¶
- Active Layer¶
- Animation¶
- Interpolate Sequence¶
- Erase Lasso¶
- Box Erase¶

Select the active layer.

The stroke animation operations are described in the Animation section.

Draw ‣ Interpolate Sequence

See Interpolate Sequence.

The Erase Lasso operator erases all Grease Pencil strokes within a freeform selection.

Press and hold Ctrl-Alt-RMB, then draw a lasso shape around the area you want to erase.

Release the mouse button to apply the eraser.

Only points within the lasso region are removed.

The Box Erase operator erases all Grease Pencil strokes within a rectangular selection.

Press B, then click and drag to define a rectangular area.

Release the mouse button to apply the eraser.

All points of strokes within the box are removed.

---

## Drawing Plane¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/drawing_planes.html

**Contents:**
- Drawing Plane¶

Draw Mode and Sculpt Mode

Drawing Planes pop-over.¶

The Drawing Planes selector helps to select the plane in which strokes are drawn.

To see which plane you are using when drawing strokes, you can enable Canvas in Viewport Overlays. See Viewport Display to know more about Canvas settings.

The Drawing Plane only affects new strokes and does not affect existing strokes.

Strokes are drawn with the current 3D Viewport orientation.

Strokes are drawn on the plane determined by the XZ axes (front view).

Strokes are drawn on the plane determined by the YZ axes (side view).

Strokes are drawn on the plane determined by the XY axes (top view).

Strokes are drawn with the current 3D cursor orientation.

---

## Flip Visual Effect¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/visual_effects/flip.html

**Contents:**
- Flip Visual Effect¶
- Options¶

The Flip Visual Effect shows the object flipped horizontally and/or vertically.

Which axis or axes to flip the object about.

When enabled, shows the object flipped horizontally.

When enabled, shows the object flipped vertically.

---

## Glow Visual Effect¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/visual_effects/glow.html

**Contents:**
- Glow Visual Effect¶
- Options¶
- Example¶

The Glow Visual Effect add a glowing rim around the object.

Determines the mode for the glow effect.

The glow light illuminates the entire object.

The glow light only affect a single color.

Allows to select a single color to apply the glow light.

Limits the colors affected by the glow light. (A value of 1 means no colors affected.)

Defines the glow color.

The mask blending operation to perform. See Color Blend Modes.

Control the Opacity of the glow over the object.

Control the glow scale in pixels on the X and Y axis.

Control the Rotation of the glow.

Number of Blur samples (0 disabled the blur effect).

When enabled, glow only affects alpha areas.

Mode: Luminance (Glow Under).¶

Mode: Color (Black lines).¶

---

## Grease Pencil¶

**URL:** https://docs.blender.org/manual/en/latest/editors/dope_sheet/modes/grease_pencil.html

**Contents:**
- Grease Pencil¶
- Channels Region¶
- Header¶
  - Insert Keyframe¶
  - Copying Frames¶
- Main Region¶
- Sidebar¶

This mode lets you adjust the timing of a Grease Pencil object’s animation frames. It is especially useful for blocking out shots.

The Channels region shows the Grease Pencil object in light blue and its layers in gray. Layers have the following settings:

Toggle the layer’s masks on or off.

Toggle onion skinning.

Toggle layer visibility in the viewport and in render.

When unchecked, the layer gets frozen in its current state, and moving to a different keyframe will no longer change its appearance.

Locked layers can’t be edited.

Removes the active layer.

Moves the active layer down/up.

Toggle whether the active layer is the only one that can be edited and is visible.

Toggle whether the active layer is the only one that can be edited.

You can press I while hovering over the Dope Sheet Editor to insert a keyframe. It’ll create a copy of the active frame if Additive Drawing is enabled, and a blank frame otherwise.

It is possible to copy frames from one layer to another, or from object to object, using the Copy and Paste tools in the Key menu. Note that keyframes will be pasted into selected layers, so make sure you have a destination layer selected.

The keyframes can be manipulated like any other data in the Dope Sheet. Interpolated keyframes (alias breakdowns) are visualized as smaller light blue points.

The Sidebar contains a copy of the Grease Pencil Layer Properties.

---

## Grease Pencil Materials¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/materials/index.html

**Contents:**
- Grease Pencil Materials¶
- Material Shader¶
- Setting Up Materials¶
- Properties¶
  - Material Slots¶
  - Surface¶
  - Settings¶

Materials control the appearance of the Grease Pencil object. They define the base color and texture of the strokes and filled areas.

There is always only one active material in the list (the selected one). When you draw, the new strokes use the active material.

You can override the base material color using the tools in Vertex Mode or the Draw and Tint tool in Draw Mode.

The material always remains linked to the strokes, this means that any change in a material will change the look of already drawn strokes.

Same stroke linked to different materials.¶

Grease Pencil materials use a special shader that define the appearance of the surface of the stroke and fill.

Stroke and fill components has it own section panel and they can be enabled with a checkbox on the panel header.

Stroke only has effect on the lines and Fill only on the areas determined by closed lines (by connecting the lines start and end points).

The shader is not a BSDF capable shader and can only be setting up on the Material Properties panel (it is not a shader node).

Material ‣ Material Slots

Grease Pencil materials can be created in the Material properties as any other materials in Blender. See Material assignment for more information.

The 3D Viewport can be set to Material Preview or Rendered shading, to interactively preview how the material looks in the scene.

Grease Pencil materials are data-blocks that can be assigned to one or more objects, and different materials can be assigned to different strokes.

In Grease Pencil the brush settings together with the material used will define the look and feel of the final strokes.

Materials slots also have some extra controls that help to work with materials while drawing or editing lines.

---

## Grease Pencil Material Properties¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/materials/properties.html

**Contents:**
- Grease Pencil Material Properties¶
- Material Slots¶
  - Specials¶
  - Lock & Visibility Controls¶
- Surface¶
  - Stroke¶
  - Fill¶
- Settings¶

Grease Pencil material slots panel.¶

Next to the material name there are three icons buttons that control common properties of the material:

Toggle the use of the material for Onion Skinning.

Toggle whether the active material is the only one that can be edited and is visible.

Toggle whether the active material is the only one that can be edited.

Turns on the visibility of every material in the list.

Turns off the visibility of every material in the list except the active one.

Locks editing of all the materials in the list.

Unlocks editing of all the materials in the list.

Locks all materials not used in the selected strokes.

Locks and hides all unused materials.

Copy the active material to the selected Grease Pencil object.

Copy all materials to the selected Grease Pencil object.

Remove all unused materials.

Toggle whether the active material is the only one that can be edited.

Toggle whether the active material is the only one that can be edited and is visible.

Shader panel with only Stroke component activated.¶

When enabled, the shader use the stroke component. The Stroke component controls how to render the edit lines.

Defines how to display or distribute the output material over the stroke.

Connects every points in the strokes showing a continuous line.

Use a disk shape at each point in the stroke. The dots are not connected.

Use a square shape at each point in the stroke. The squares are not connected.

The type of the material.

Use an image texture.

The image data-block used as an image source.

Texture and Base Color mixing amount.

The image size along the stroke.

The base color of the stroke.

Removes the color from strokes underneath the current by using it as a mask.

Defines how to align the Dots and Squares along the drawing path and with the object’s rotation.

Aligns to the drawing path and the object’s rotation.

Aligns to the object’s rotation; ignoring the drawing path.

Aligns to the screen space; ignoring the drawing path and the object’s rotation.

Rotates the points of Dot and Square strokes.

The Rotation option is limited to a range of -90 to 90 degrees.

Disables stencil and overlap self-intersections with alpha materials.

Mode Type: Line, Style: Solid.¶

Mode Type: Line, Style: Texture.¶

Mode Type: Dot, Style: Solid.¶

Mode Type: Dot, Style: Texture.¶

When enabled, the shader use the fill component. The Fill component control how to render the filled areas determined by closed edit lines.

The type of material.

Use a color gradient.

Mix the colors along a single axis.

Mix the colors radiating from a center point.

Use an image texture.

The image data-block used as an image source.

Style: Gradient (Linear).¶

Style: Gradient (Radial).¶

The base color of the fill.

Removes the color from strokes underneath the current by using it as a mask.

The amount that the Secondary Color (for Gradient Style) or image texture (for Texture Style) mixes with the Base Color.

Flips the gradient, inverting the Base Color and Secondary Color.

Shifts the position of gradient or image texture.

Rotates the gradient or image texture.

Scales the gradient or image texture.

When enabled, show one image instance only (do not repeat).

This index can be used with some modifiers to restrict changes to only a certain material. See Modifiers for more information.

---

## Grease Pencil Menu¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/edit/grease_pencil_menu.html

**Contents:**
- Grease Pencil Menu¶
- Transform¶
  - Move, Rotate & Scale¶
  - Transform Snapping¶
  - Tools¶
- Mirror¶
- Snap¶
- Active Layer¶
- Animation¶
- Interpolate Sequence¶

Strokes can be edited by transforming the locations of points.

Toolbar ‣ Move, Rotate, Scale

Grease Pencil ‣ Transform ‣ Move, Rotate, Scale

Like other elements in Blender, points and strokes can be moved G, rotated R or scaled S as described in the Basic Transformations section. When in Edit Mode, Proportional Editing is also available for the transformation actions.

Basic move, rotate and scale transformations for selected points/strokes. See Move, Rotate, Scale Basics for more information.

Grease Pencil ‣ Transform

The Bend, Shear, To Sphere, Extrude and Shrink Fatten transform tools are described in the Editing tools section.

Grease Pencil ‣ Mirror

The Mirror tool is also available, behaving exactly the same as with mesh vertices.

Mesh snapping also works with Grease Pencil components.

Grease Pencil ‣ Active Layer

Select the active layer.

Grease Pencil ‣ Animation

The stroke animation operations are described in the Animation section.

Grease Pencil ‣ Interpolate Sequence

See Interpolate Sequence.

Grease Pencil ‣ Duplicate

Duplicates the selected elements, without creating any connections with the rest of the strokes (unlike Extrude, for example), and places the duplicate at the location of the original elements.

Grease Pencil ‣ Split

The Split operator separates the selected portion of a curve from the rest, creating a new, independent curve segment. This curve can then be moved or altered without affecting the other curve.

If a segment of the curve is selected, it will be split off as a new curve that can be moved or edited independently.

If only a single control point is selected, it will be duplicated as a loose control point, while the original remains attached to the rest of the curve.

Copy the selected points/strokes to the clipboard.

Grease Pencil ‣ Paste

Paste Grease Pencil points or strokes from the internal clipboard to the active layer.

Add pasted strokes behind all strokes.

Keep the world transform of strokes from the clipboard unchanged.

Contains operators to adjust the visibility of points and strokes in the viewport.

Grease Pencil ‣ Show/Hide ‣ Show All Layers

Shows all Grease Pencil layers.

Grease Pencil ‣ Show/Hide ‣ Hide Active Layer

Hides the active Grease Pencil layers.

Grease Pencil ‣ Show/Hide ‣ Hide Active Layer

Hides the all Grease Pencil layers except the active layer.

Grease Pencil ‣ Separate

Separate different elements into new Grease Pencil objects based on specific criteria.

Separates the selected points or strokes into a new object.

Separates the geometry by creating a new object for each material.

Separates the geometry by creating a new object for each layer. See 2D Layers for more information.

These tools help to cleanup degenerate geometry on the strokes.

Grease Pencil ‣ Clean Up ‣ Delete Loose Points

Removes strokes with only a few points.

The number of points to consider a stroke as loose.

Grease Pencil ‣ Clean Up ‣ Delete Duplicate Frames

Removes any duplicate keyframes.

Grease Pencil ‣ Clean Up ‣ Merge by Distance

Simplifies a stroke by merging the selected points that are closer than a specified distance to each other. Note, unless using Unselected, selected points must be contiguous, else they will not be merged.

Sets the distance threshold for merging points.

Allows points in selection to be merged with unselected points. When disabled, selected points will only be merged with other selected ones.

Grease Pencil ‣ Clean Up ‣ Reproject

Sometimes you may have drawn strokes unintentionally in different locations in the 3D space but they look right from a certain plane or from the camera view. You can use Reproject to flatten all the selected strokes from a certain viewpoint.

Reproject selected strokes onto the front plane (XZ).

Reproject selected strokes onto the side plane (YZ).

Reproject selected strokes onto the top plane (XY).

Reproject selected strokes onto the current view.

Reproject selected strokes onto the mesh surfaces.

When Surface Mode is activated controls the stroke offset from the object.

Reproject selected strokes onto 3D cursor rotation.

Maintains the original strokes after applying the tool.

Original drawing from the front view.¶

Original drawing in the 3D Viewport.¶

Strokes reprojected onto the front plane to fix strokes misalignment.¶

Drawing after reprojection operation from the front view.¶

Grease Pencil ‣ Outline

The Outline operator converts selected Grease Pencil strokes into closed perimeter shapes. It creates new strokes around the outer boundary of the original stroke, effectively generating a filled outline with adjustable thickness.

Defines the projection method used to generate the outline:

Use the current viewport perspective as the projection plane.

Use the X-Z axes as the projection plane (front view).

Use the Y-Z axes as the projection plane (side view).

Use the X-Y axes as the projection plane (top view).

Use the active camera’s perspective as the projection plane.

Sets the thickness of the outline on both sides of the original stroke. Higher values result in a wider perimeter.

Scales the stroke outline inward or outward. - Positive values push the perimeter outward. - Negative values pull it inward. - A value of 0 centers the perimeter on the original stroke.

Number of subdivisions used to smooth corners at stroke endpoints and joints. Higher values result in smoother corners but increase stroke complexity.

Stroke after applying the Outline operator.¶

Grease Pencil ‣ Delete

Opens a pop-up menu with operators to remove geometry from the Grease Pencil object.

Deletes all the strokes at the current frame and in the current layer/channel.

Grease Pencil ‣ Delete ‣ Delete

Deletes the selected points. When only one point remains, there is no more visible stroke, and when all points are deleted, the stroke itself is deleted.

Grease Pencil ‣ Delete ‣ Dissolve

Dissolving removes points between other points and connect the remaining points.

Ctrl-X Opens a pop-up to choose the dissolve type.

Deletes the selected points without splitting the stroke. The remaining points in the strokes stay connected.

Deletes all the points between the selected points without splitting the stroke. The remaining points in the strokes stay connected.

Deletes all the points that are not selected in the stroke without splitting the stroke. The remaining points in the strokes stay connected.

Grease Pencil ‣ Delete ‣ Delete Active Keyframe (Active Layer)

Deletes all the strokes at the current frame in the active layer.

Grease Pencil ‣ Delete ‣ Delete Active Keyframes (All Layers)

Deletes all the strokes at the current frame in all layer.

---

## Grease Pencil Primitives¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/primitives.html

**Contents:**
- Grease Pencil Primitives¶
- Blank¶
- Stroke¶
- Monkey¶
- Scene Line Art¶
- Collection Line Art¶
- Object Line Art¶

Object Mode and Edit Mode

In Object Mode, the Add menu provides three different Grease Pencil primitives with preset materials and 2D layers:

Grease Pencil primitives.¶

Adds a Grease Pencil object without any stroke.

Adds a Grease Pencil object with a simple stroke as a reference.

It creates a 2D monkey head. The Monkey’s name is “Suzanne” and is Blender’s mascot. 2D Suzanne is very useful as a standard test.

Sets up a Line Art Modifier for the active scene by creating an “empty” Grease Pencil object with a Line Art modifier referencing each object in the scene.

Sets up a Line Art Modifier for the active collection by creating an “empty” Grease Pencil object with a Line Art modifier referencing each object in the collection.

Sets up a Line Art Modifier for the active object by creating an “empty” Grease Pencil object with a Line Art modifier referencing the active object.

---

## Interpolation¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/animation/interpolation.html

**Contents:**
- Interpolation¶
- Interpolate¶
- Interpolate Sequence¶

Toolbar ‣ Interpolate

When you are animating simple shapes you can use the interpolate tool to automatically add new breakdown keyframes.

See Interpolate tool for more details.

Interpolate strokes between the previous and next keyframe by adding multiple keyframes. When you are on a frame between two keyframes and click the sequence button a breakdown keyframe will be added on every frame between the previous and next keyframe.

The number of frames between generated interpolated frames.

Restrict the interpolation to Active or All layers.

When enabled, only selected strokes will be interpolated.

Exclude existing Breakdowns keyframes as interpolation extremes.

Invert strokes start and end. Automatic will try to found the right mode for every stroke.

Amount of smoothing to apply to interpolated strokes for reducing jitter/noise.

Number of time to smooth newly created strokes.

Interpolation method to use for the sequence.

---

## Layers¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/properties/layers.html

**Contents:**
- Layers¶
- Masks¶
- Transform¶
- Adjustments¶
- Relations¶
- Display¶

Object Data tab ‣ Layers

Grease Pencil Layers panel.¶

Grease Pencil objects can be organized into a tree known as the layer tree for grouping and arranging strokes.

Any stroke can only belong to a single 2D layer. The selected layer is the active layer. Only one layer or group can be active at a time. When you draw, the new strokes are added to the active layer. By default the view order of the layers in the viewport is top to bottom.

Layers can be grouped using Layer Groups. A layer can only be in one group at a time. Layers can be moved into groups using drag-and-drop. Groups can be color coded with a color tag.

Every layer correspond to a channel in the Dope Sheet editor (in Grease Pencil mode). See Dope Sheet for more information.

Layers can also be used together with Modifiers to only affects part of your drawing. See Modifiers for more information.

Layers can mask other layers by enabling Use Mask (mask icon) or using the checkbox in the Masks panel header. See Masks for more information.

Sometimes the layers you are not working on can be a distraction in the 3D Viewport. Activate the Fade Inactive Layers overlay to control the opacity of the non-active layers.

Tree view of all layers and groups for the Grease Pencil object.

Next to the layer name there are four icons buttons that control common properties of the layer:

Toggle the affect of Masks on the layer.

Toggle using the layer for Onion Skinning.

Toggle layer visibility in the viewport and in render.

Toggle layer from being editable.

Adds a new layer to the active object.

Adds a new layer group to the active object. Note, layer groups cannot be added from the Dopesheet; they must be added from the Properties editor.

Removes the active layer or layer group.

Operators for working with layers.

Makes an exact copy of the selected layer appending a number to differentiate its name.

Makes a copy of the selected layer but with empty keyframes. Useful to easily have empty keyframes preset to work on the cleanup or filling process.

Turns on the visibility of every layer in the list.

Turns off the visibility of every layer in the list except the active one.

Locks editing of all the layers in the list.

Unlocks editing of all the layers in the list.

Automatically locks the editing of every layer in the list except the active one. This way you avoid making unwanted changes in other layers without the need to lock them every time.

Allow editing strokes even if they use locked materials.

Combine the selected layer with the layer below, the new layer keeps the name of the lower layer.

Combine layers in the active layer group into a single layer.

Combine all layers into the active layer.

Adds a mask to the active layer with layer above or below.

Copy the active layer to the selected Grease Pencil object.

Copy all layers to the selected Grease Pencil object.

Moves the active layer or layer group up/down in the tree.

Below the layers list there are additional settings:

The layer blending operation to perform. See Color Blend Modes.

Used to set the opacity of the layer.

When enabled, the layer is affected by lights.

In Grease Pencil there are no special mask layers, any layer can act as a mask for other layers. The mask system is flexible enough to allow top-bottom and bottom-top masking.

Layers used as masks can use all the blend modes and different opacity values like any other layer.

If you want to make a full transparent masking you will have to set the mask layer’s opacity to 0.

The layer/s that will act as mask of the current layer could be added to the Mask list view.

In the Masks list next to the layers name there are two icons buttons that control common properties of the layer mask:

Toggle layer visibility in the viewport and in render.

Original image (Blend: Regular, Opacity: 1).¶

Blend: Hard Light, Opacity: 1.¶

Blend: Regular, Opacity: 1.¶

Allows per-layer location, rotation and scale transformations.

Layers adjustment panel.¶

Color that tint any material colors used in the layer.

Controls the amount of tint color to apply.

Thickness value that override the strokes thickness in the layer.

Select a Parent object to manipulate the layer. The layer will inherit the transformations of the parent, this is especially useful when rigging for cut-out animation.

The layer index number can be used with some modifiers to restrict changes to only certain areas.

See Modifiers for more information.

Defines the View Layer to use for the Grease Pencil layer. If empty, the layer will be included in all View Layers. This is useful to separate drawings parts for compositing.

If disabled, no masks on the layer are included in the view layer render.

Sets the color to use in the channel region of the Dope Sheet.

---

## Multiframe¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/multiframe.html

**Contents:**
- Multiframe¶
- Usage¶

Multiframe pop-over.¶

Multiframe allows you to draw, edit, sculpt, or weight painting on several frames at the same time. Extremely useful to avoid repeating a task one frame at a time when animating.

When enabled, the effects on the strokes start to falloff from the current frame as defined by a curve widget.

Select the desired keyframes to draw, edit or sculpt at the same time.

Activate the Multiframe tool in the 3D Viewport’s header with the toggle button (faded lines icon).

Once activated you can:

Select the points in all the selected keyframes and make your edits.

Start sculpting. The sculpt brushes will affects all the strokes in the selected keyframes.

Start weight painting. The weight paint brush will affect all the strokes in the selected keyframes.

Start Drawing. The new strokes will be added in all the selected keyframes. If you are using the Fill tool then it will be applied in all the selected keyframes.

When interpolating you can select the stroke from the different frames in the right order. Interpolate tool will use the selection order to calculate the correct stroke pairs.

Not all operators support Multiframe mode.

---

## Object Properties¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/properties/object.html

**Contents:**
- Object Properties¶
- Visibility¶

Object Properties ‣ Visibility

Enables the Grease Pencil object to be affected by lights.

This property affect the whole object, for more control with lights you can enable or disable the use of lights by layers. See Layers for more information.

Lights disabled (left) and enabled (right).¶

There are several other general visibility properties.

---

## Onion Skinning¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/properties/onion_skinning.html

**Contents:**
- Onion Skinning¶
- Options¶
- Custom Colors¶
- Display¶

Onion Skinning show ghosts of the keyframes before and after the current frame allowing animators to make decisions in the animation sequence.

The main switch to show/hide Onion Skinning is in the Viewport Overlays, but Grease Pencil Onion Skinning is per-layer and the visibility can be toggle in the layer list. See 2D Layers for more information.

Onion Skinning panel.¶

Shows Keyframes in the range determined by the Before/After settings.

Shows Frames in the range determined by the Before/After settings.

Shows only on the manually selected keyframes in the Dope Sheet.

Control the opacity of the ghost frames.

Filters what type of frames to show in the Onion Skinning range.

Sets how many frames or keyframes, depending on the Mode, to show before and after the current frame.

Color to use before and after the current frame on ghost frames.

Opacity of the ghosts frames decrease the further away from the current frame.

Help working on loop animations showing the first keyframe/frame as ghost when you are on the last frame of your animation.

An example of Onion Skinning activated.¶

---

## Pixelate Visual Effect¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/visual_effects/pixelate.html

**Contents:**
- Pixelate Visual Effect¶
- Options¶
- Example¶

The Pixelate Visual Effect shows the object as a pixelated image.

Pixelate Visual Effect.¶

Horizontal and vertical size of the final pixels to apply.

Applies an anti-aliasing effect to the resulting pixels.

---

## Point Menu¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/edit/point_menu.html

**Contents:**
- Point Menu¶
- Extrude¶
- Smooth¶
- Vertex Groups¶
- Set Handle Type¶
- Set Corner Type¶

Extrudes points by duplicating the selected points, which then can be moved. The new points stay connected with the original points of the edit line.

Since Grease Pencil strokes can only have one start an end point, a new stroke will be created when extrude intermediate points in the strokes.

Softens strokes by reducing the differences in the locations of the points along the line, while trying to maintain similar values that make the line fluid and smoother.

The number of times to repeat the procedure.

The amount of the smoothness to apply.

Smooths the stroke’s endpoints.

Preserves the strokes shape.

When enabled, the operator affect the points location.

When enabled, the operator affect the points thickness.

When enabled, the operator affect the points strength (alpha).

Operators for working with vertex groups.

Point ‣ Set Handle Type

Sets the handle type for the points on the Bézier curve that are in the selection.

The handle type to switch to.

This handle has a completely automatic length and direction which is set by Blender to ensure the smoothest result. These handles convert to Align handles when moved.

Both parts of a handle always point to the previous handle or the next handle which allows you to create curves or sections thereof made of straight lines or with sharp corners. Vector handles convert to Free handles when moved.

These handles always lie in a straight line, and give a continuous curve without sharp angles.

The handles are independent of each other.

Replaces Free handles with Align, and all Align with Free handles.

Point ‣ Set Corner Type

Sets how corners between strokes or segments are shaped when using stroke thickness or fills. This affects how the stroke geometry joins at sharp angles.

Defines the style of the corner for the selected points.

Smoothly rounds the corner, creating a curved transition between segments.

Cuts the corner flat, creating a beveled join.

Keeps the corner pointed, preserving the original angle between segments.

Specifies the angle threshold (in degrees) for flattening sharp corners. Any corner sharper than this angle will be cut flat when Corner Type is set to Flat or Round.

---

## Rim Visual Effect¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/visual_effects/rim.html

**Contents:**
- Rim Visual Effect¶
- Options¶
  - Blur¶
- Example¶

The Rim Visual Effect shows a simulated rim light on the object contour.

For simulating the rim light, a masked color silhouette of the object is displaced in horizontal and/or vertical direction.

Many blending modes can be applied to the resulting mask.

Defines the rim light color.

Defines a color to keep unaltered.

The mask blending operation to perform. See Color Blend Modes.

Control the color mask displacement in pixels on the X and Y axis.

Control the blur scale in pixels on the X and Y axis.

Number of blur samples (0 disabled the blur effect).

---

## Selecting Grease Pencil Elements¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/edit/selecting.html

**Contents:**
- Selecting Grease Pencil Elements¶
- Select Mode¶
- Select All/None/Invert¶
- Select Random¶
- Select Alternated¶
- Select More/Less¶
- Select Similar¶
- Select Linked¶
- Select First/Last¶

3D Viewport Header ‣ Select Mode

Edit Mode selection buttons.¶

In Edit Mode there are three different selection modes. You can enter the different modes by selecting one of the three buttons in the header.

To select individual points.

To select an entire stroke.

To select all points that are between other strokes.

Points, stroke and in between stroke selection sample.¶

All these options have the same meaning and behavior as in Object Mode.

Select ‣ Select Random

Randomly selects unselected points or strokes.

The likelihood of an unselected elements being selected. Note that, this is not the percentage amount of elements that will be selected.

Seed used by the pseudo-random number generator.

Selection or deselection of elements.

Select ‣ Select Alternated

Selects alternate points in the selected strokes.

Ctrl-NumpadPlus, Ctrl-NumpadMinus

The purpose of these operators is to reduce or enlarge the current selection within a stroke (i.e. they will never “go outside” of a stroke or “jump” to another stroke in the same object).

For each selected point, select all its linked points (i.e. one or two…).

For each selected point, if all points linked to this point are selected, keep this one selected. Otherwise, deselect it.

When all points of a stroke are selected, nothing will happen (as for Less, all linked points are always selected, and of course, More cannot add any). Conversely, the same goes when no points are selected.

Select ‣ Select Similar

Select all strokes with similar characteristics.

The characteristics to compare.

Selects all the points/strokes with a similar layer index.

Selects all the points/strokes with a similar material index.

Selects all the points/strokes with a similar vertex color.

Selects all the points/strokes with a similar stroke radius.

Selects all the points/strokes with a similar layer opacity

How similar the selection must be.

Select ‣ Select Linked

L (or Ctrl-L for all) will add to the selection the cursor’s nearest control point, and all the linked ones, i.e. all points belonging to the same stroke.

These operators will toggle the selection of the first or last point(s) of the stroke(s) in the object. This is useful to quickly find the start of a stroke.

---

## Settings¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/properties/strokes.html

**Contents:**
- Settings¶

General settings for Grease Pencil strokes.

Defines how the strokes are ordered in 3D space (for objects not displayed In Front).

The Strokes drawing order respect the order of the 2D layers list (top to bottom) and ignores the real position of the strokes in 3D space. See 2D Layers for more information.

The strokes drawing order is based on the stroke location in 3D space.

Blue, Green and Red strokes in three different layers using 2D Layers depth order.¶

Blue, Green and Red strokes in three different layers using 3D Location depth order.¶

---

## Shadow Visual Effect¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/visual_effects/shadow.html

**Contents:**
- Shadow Visual Effect¶
- Options¶
  - Blur¶
  - Wave Effect¶
- Example¶

The Shadow Visual Effect shows a simulated shadow casting by the object.

For simulating the shadow a color silhouette of the object is displaced in horizontal and/or vertical direction on the back of the object.

Shadow Visual Effect.¶

Defines the shadow color.

Control the shadow displacement in pixels on the X and Y axis.

Control the size of the shadow on the X and Y axis.

Sets the shadow rotation around the Grease Pencil object center or another object when Use Object As Pivot is enabled.

When enabled, an Object is used by the shadow as the center of rotation.

Control the blur scale in pixels on the X and Z axis.

Number of blur samples (0 disabled the blur effect).

When enabled, apply a wave distortion to the shadow.

Sets horizontal or vertical direction for the waves.

Controls the strength and the depth of the wave.

Controls the wave period. The time it takes to complete one cycle.

Shifts the wave pattern over the shadow.

Stretched shadow with an empty as center of rotation.¶

---

## Swirl Visual Effect¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/visual_effects/swirl.html

**Contents:**
- Swirl Visual Effect¶
- Options¶
- Example¶

The Swirl Visual Effect applies a swirling pattern to the object. The effect use an object as the center of the swirl.

Swirl Visual Effect.¶

Sets the object to use as the center of the swirl.

External radius size of the swirl.

Rotation angle of the swirl. A value of 0 shows no swirl.

---

## Trace Image to Grease Pencil¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/object/trace_image.html

**Contents:**
- Trace Image to Grease Pencil¶
- Usage¶
- Options¶

Object ‣ Convert ‣ Trace Image to Grease Pencil

The Trace Image to Grease Pencil tool traces a black and white image and generates Grease Pencil strokes. If the image is not black and white, it will be internally converted. For better results, convert the images manually to black and white. Also try to keep the resolution of the image small; high resolutions can produce very dense strokes.

Add an Image Empty to the scene.

Run Trace Image to Grease Pencil.

Determines if the image empty is kept or replaced.

New Object: Creates a new Grease Pencil object and keeps the image empty Selected Object: Replaces the image empty with the Grease Pencil object.

The thickness of the generated Grease Pencil strokes.

Determine the Luminance threshold above which strokes are generated.

Determines how to resolve ambiguities during decomposition of an image into paths.

Prioritizes to connect black (foreground) components.

Prioritizes to connect white (background) components.

Always take a left turn.

Always take a right turn.

Prioritizes to connect the color (black or white) that occurs least frequently in the local neighborhood of the current position.

Prioritizes to connect the color (black or white) that occurs most frequently in the local neighborhood of the current position.

Choose pseudo-randomly.

Determines if the image being traced is a single image or image sequence.

The image empty is a single image or the current frame of an image sequence.

The image empty is an Image Sequence.

When enabled, start the tracing process at the current image frame.

Used to trace only one frame of the image sequence, set to zero to trace all.

---

## Wave Distortion Visual Effect¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/visual_effects/wave_distortion.html

**Contents:**
- Wave Distortion Visual Effect¶
- Options¶
- Example¶

The Wave Distortion Visual applies a wavy effects to the object.

Wave Distortion Effect.¶

Sets horizontal or vertical direction for the waves.

Controls the strength and the depth of the wave.

Controls the wave period. The time it takes to complete one cycle.

Shifts the wave pattern over the Object.

Amplitude: 10 (horizontal).¶

Amplitude: 30 (horizontal).¶

Amplitude: 10 (vertical).¶

Amplitude: 30 (vertical).¶

---
