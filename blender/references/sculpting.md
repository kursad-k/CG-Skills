# Blender - Sculpting

**Pages:** 60

---

## Blob¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/blob.html

**Contents:**
- Blob¶
- Brush Settings¶
  - General¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Similar to Draw, but vertices are pushed outwards like an inverted pinching effect. This will lead to a more consistent spherical curvature and thickening of strokes.

By default at 0.5 to push out the mesh during the stoke. More info at Pinch/Magnify

More info at General brush settings and on Advanced brush settings.

---

## Boundary¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/boundary.html

**Contents:**
- Boundary¶
- Brush Settings¶
  - General¶
  - Unique¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Similar to the Pose brush but deforms the open boundaries of a mesh. The tool detects the mesh boundary closest to the active vertex and propagates the deformation using the brush Falloff into the mesh.

The main use cases of this brush are the Bend and Expand geometry, which leads to the best results on evenly distributed quad based topology. Use the Inflate, Grab, Twist, and Smooth deformation modes, to further adjustments and tweaks to the result (which do not depend that much on a clean topology).

Boundaries to hidden geometry will also be counted as an open boundary.

The boundary origin is displayed via a white line, which indicates the reach of the deformation. The targeted boundary that will be deformed is highlighted in the brush cursor color.

If the Deformation Target is changed, the brush can also be used for cloth sculpting.

Evenly distributed and quad based topology will lead to much better results. Triangles and N-gons are also supported but may lead to unpredictable outcomes.

More info at General brush settings and on Advanced brush settings.

Deformation type that is used by the brush.

Rotates the boundary around the local Y axis. Useful for creating folding shapes, like sleeves.

Moves/extends the mesh boundary in the local X direction. Useful for extending the boundaries along the surface.

Works similar to the Inflate tool but, the vertices that are inflated are constrained to the mesh boundary.

Works similar to the Grab tool but, the vertices that are grabbed are constrained to the mesh boundary.

Rotates the active boundary around the local Z axis. Useful for creating folds like on a skirt.

Works similar to the Grab tool but, the vertices that are smoothed are constrained to the mesh boundary.

How the brush Falloff is applied across the boundary.

Applies the same deformation in the entire boundary.

Applies the deformation only within the brush radius.

Applies the brush falloff in a loop pattern along the boundary.

Applies the falloff radius in a loop pattern, inverting the direction back & forth.

Offset of the boundary origin in relation to the brush radius.

---

## Brushes¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/index.html

**Contents:**
- Brushes¶

Brushes for Sculpt Mode bundled in the Essentials library.

---

## Brushes¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/brushes/index.html

**Contents:**
- Brushes¶
- Draw Brushes¶
- Fill Brushes¶
- Erase Brushes¶

There are a number of brushes for draw mode bundled in the Essentials asset library. This is an overview of all of them.

Draw brushes are the special type of brushes that uses Grease Pencil for drawing tools. The brush can be changed in the Tool Settings. The different draw brushes (pencil, Ink, marker, etc.) are settings variations of the same Draw Brush. You can create many brushes, each with unique settings to get different artistic result while drawing.

Fill brushes are the special type of brushes that uses Grease Pencil for the Fill tools. The brush can be changed in the Tool Settings. The different fill brushes are settings variations of the same Fill Brush. You can create many brushes, each with unique settings to get different result when filling areas.

Erase brushes are the special types of brushes that uses Grease Pencil for Erase tools. The brush can be changed in the Tool Settings. Soft and hard eraser brushes are settings variations of the same Erase Brush. You can create many brushes, each with unique settings to get different effects while erasing. The Erase Brush has also other two special eraser types: point and stroke.

---

## Brushes¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/weight_paint/brushes.html

**Contents:**
- Brushes¶
- Brush Types¶

Available brush types are listed here, together with brushes from the Essentials asset library using them.

Paints a specified weight over the object.

The brush Blend Modes defines in which way the weight value is applied to the vertex group while painting.

In this Blending mode the Weight value defines the target weight that will eventually be reached when you paint long enough on the same location of the mesh. And the strength determines how many strokes you need to place at the target weight. Note that for strength = 1.0 the target weight is painted immediately and for Weight = 0.0 the brush just does nothing.

In this Blending mode the specified weight value is added to the vertex weights. The strength determines which fraction of the weight gets added per stroke. However, the brush will not paint weight values above 1.0.

In this Blending mode the specified weight value is subtracted from the vertex weights. The strength determines which fraction of the weight gets removed per stroke. However, the brush will not paint weight values below 0.0.

In this Blending mode the specified weight value is interpreted as the target weight. Very similar to the Mix Blending mode, but only weights below the target weight are affected. Weights above the target weight remain unchanged.

This Blending mode is very similar to the Lighten Blending mode. But only weights above the target weight are affected. Weights below the target weight remain unchanged.

Multiplies the vertex weights with the specified weight value. This is somewhat like subtract, but the amount of removed weight is now dependent on the Weight value itself.

Smooths out the weighting of adjacent vertices. In this mode the Weight Value is ignored. The strength defines how much the smoothing is applied.

Smooths out the weighting of adjacent vertices. In this mode the Weight Value is ignored. The strength defines how much the smoothing is applied.

Smooths weights by painting the average resulting weight from all weights under the brush.

Smudges weights by grabbing the weights under the brush and “dragging” them. This can be imagined as a finger painting tool.

---

## Brushes¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/vertex_paint/brushes.html

**Contents:**
- Brushes¶
- Brush Types¶

Available brush types are listed here, together with brushes from the Essentials asset library using them.

Brushes: Paint Hard, Paint Soft, Paint Hard Pressure, Paint Soft Pressure, Airbrush

Paints a specified color over the object.

Smooths out the colors of adjacent vertices. In this mode the Color Value is ignored. The strength defines how much the colors are blurred.

Smooths color by painting the average resulting color from all colors under the brush.

Smudges colors by grabbing the colors under the brush and “dragging” them. This can be imagined as a finger painting tool.

---

## Brushes¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/brushes.html

**Contents:**
- Brushes¶
- Add/Subtract Brushes¶
- Contrast Brushes¶
- Transform Brushes¶
- Utility Brushes¶
- Painting Brushes¶
- Simulation Brushes¶

This is a list of all provided ‘Essentials’ brush assets that come with Blender. These are based on various Brush Types which are mentioned for each brush..

These brushes generally push vertices outwards and inwards and are the most customizable to achieve a wide variety of effects. They typically don’t use a color in their thumbnail.

The standard brush for pushing vertices inwards and outwards from the surface direction.

Same as Draw but with a much sharper Falloff. Useful for creating creases and sharp angles.

Similar to the Draw brush but with a flattening effect and subtle smoothing. Useful for polishing and building volumes.

The same as the Clay brush, but more aggressive with a square falloff. A common standard for building rough volumes.

The same as the Clay brush, but specifically for emulating the effect of running your thumb over surfaces. Pushes geometry in and sideways.

Draw with a fixed height. Useful for adding flat layers to a surface.

Moves the mesh in multiple direction. Useful for inflating or shrinking surfaces and volumes.

Magnifies the mesh as you draw. Useful for an additional inflation effect on the stroke.

A Draw brush with a pinching effect. Useful for polishing existing creases or carefully creating new ones.

Much sharper and stronger Crease brush. Great for creating thin and deep pinches.

Recognizable by their red thumbnail and cursor. These brushes generally flatten or heighten the contrast of the surface.

Smooths out irregularities in the surface and shrinks volumes by averaging the vertices positions. An essential brush that is frequently used.

Pushes vertices to an average height to create a flat surfaces. Alternatively pushes them away from the center for more contrast.

Similar to Flatten but with a locked orientation and depth to create a consistently flat surface.

Pushes surfaces upwards towards a flat plane. Useful for filling in holes and crevices. Alternatively deepens existing holes when holding ‘Ctrl’.

Pushes surfaces inwards. Alternatively fills surfaces while holding ‘Ctrl’. This is the most common brush for flattening meshes.

Pushes surfaces inwards toward a locked direction. The depth can be defined by going deeper towards surfaces along the stroke.

Brush Type: Scrape Multiplane

Scrapes the mesh with two angled planes at the same time, producing a sharp edge between them.

Recognizable by their yellow icon and cursor. These brushes generally move, pinch and magnify the mesh.

Pulls vertices towards the center of the brush. Useful for polishing angles and creases. Alternatively pushes them away from the center.

Moves vertices along with the mouse. An essential brush for building shapes and adjusting proportions.

Similar to Grab but with an infinitely projected falloff. Useful for grabbing broader shapes and giving a similar feel to using Liquify tools in image painting applications.

Similar to Grab but only affects vertices with the normal facing sideways away from the view. Very useful for adjusting outer silhouettes of thin objects.

Brush Type: Elastic Deform

Used to simulate realistic deformations from grabbing of Elastic objects.

Brush Type: Snake Hook

Similar to Elastic Grab but rotates affected geometry based on the stroke direction.

Pulls vertices along with the stroke to create long, snake-like forms. Geometry is rotated and magnified to allow continuous pulling. Much more useful while having Dyntopo enabled.

Brush Type: Snake Hook

Iteratively picks up and lets go of geometry like the Snake Hook, but much softer. Useful for subtle small scale deforming over longer strokes.

Same as Grab but moves vertices along the surface direction. Useful for preserving specific surfaces.

Simulating an armature-like deformations. Useful for quick posing and transformations.

Similar as Thumb but dynamically picks up vertices like the Snake Hook. Useful for nudging something along the mesh surface.

Rotates vertices within the brush in the direction the cursor is moved.

Brush Type: Relax Slide

Slides the topology of the mesh in the direction of the stroke while preserving the geometrical shape of the mesh. Alternatively smooths the mesh on ‘Shift’. Also useful for redistributing topology where it is needed.

Brush Type: Relax Slide

Similar to the Relax Slide brush but pinches/relaxes geometry instead.

Transform specifically mesh boundaries with various deformations.

No clear color assignment. These brushes are general purpose brushes or specific.

Cleans up geometry by collapsing short edges. Specifically for use with Dyntopo.

Paints a selection on parts of the mesh to be unaffected by other brushes.

Brush Type: Draw Face Sets

Paint new, smooth or extend existing Face Sets.

Brush Type: Erase Multires Displacement

Remove displacement information on a Multiresolution modifier.

Brush Type: Smear Multires Displacement

Smear displacement information on a Multiresolution modifier.

Recognizable by their blue thumbnails. These brushes are used for painting color attributes within sculpt mode.

A simple hard round falloff.

A soft round falloff with pressure sensitivity for only the strength.

A hard round falloff with pressure sensitivity for the brush size.

A soft round falloff with pressure sensitivity for both size and strength.

A hard square brush falloff.

A soft round brush that builds up over time instead of stroke distance.

Similar to Average brushes in other modes with a hard round falloff. Used to blend colors along the stroke.

Same as Blend Hard but with a soft round falloff.

Same as Blend Hard but with a hard square falloff.

A mix of a Paint and Blend brush. On low pen pressure the brush averages colors and with high pen pressure it paints colors.

Smears colors along the stroke.

Pinches the colors inwards to create sharp edges or points.

Paint specific pixels (Only supported in the Image Editor).

Erase pixels in the alpha channel of the texture (Only supported in the Image Editor).

These brushes are similar to regular brushes but with an additional cloth simulation applied. These are ideally used on a relatively low resolution, since the mesh density defines the size of cloth dynamics.

Nudges the geometry along the surface while minimally affecting the overall shape of the object.

Pushes geometry inwards or outwards.

Grabs geometry within the brush radius firmly, while surrounding geometry is being simulated to follow.

Similar to Grab Cloth but with a line as the brush radius instead of a circle.

Similar to Grab Cloth but with a noise texture applied to create more random variation.

Inflates the geometry outwards or inwards.

Creates compression or stretching on geometry.

Pinches geometry to the center point of the radius, creating folds from all sides.

Pinches only from two perpendicular sides along the stroke direction, creating parallel folds along the stroke.

A pose brush that rotates geometry.

A pose brush that translates and scales geometry.

Bend only open boundaries of the mesh, folding the surrounding geometry in the process.

Twist open boundaries of the mesh, creating twisting folds.

---

## Brush Asset¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tool_settings/brushes.html

**Contents:**
- Brush Asset¶
- Brush Types¶
  - Draw Brushes¶
  - Fill Brushes¶
  - Erase Brushes¶

Brush data-block panel.¶

The Data-Block Menu to select a preset brush type or a custom brush.

When you add a brush, the new brush is a clone of the current one.

Reset the current brush to its default settings.

Reset all brushes to their default settings.

Allows definition of a custom brush icon.

Defines the path to the image to use as custom icon.

In order to save a custom brush in a blend-user, enable Fake User.

Draw brushes are the special type of brushes that uses Grease Pencil for drawing tools. The brush can be changed in the Tool Settings. The different draw brushes (pencil, Ink, marker, etc.) are settings variations of the same Draw Brush. You can create many brushes, each with unique settings to get different artistic result while drawing.

Fill brushes are the special type of brushes that uses Grease Pencil for the Fill tools. The brush can be changed in the Tool Settings. The different fill brushes are settings variations of the same Fill Brush. You can create many brushes, each with unique settings to get different result when filling areas.

Erase brushes are the special types of brushes that uses Grease Pencil for Erase tools. The brush can be changed in the Tool Settings. Soft and hard eraser brushes are settings variations of the same Erase Brush. You can create many brushes, each with unique settings to get different effects while erasing. The Erase Brush has also other two special eraser types: point and stroke.

---

## Brush Settings¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/vertex_paint/tool_settings/brush.html

**Contents:**
- Brush Settings¶
- Color Picker¶
- Color Palette¶
- Falloff¶

Painting needs paint brushes and Blender provides a Brush panel within the Toolbar when in Vertex Paint Mode.

In the Data-Block menu you find predefined Brush presets. And you can create your own custom presets as needed.

This option controls the radius of the brush, measured in pixels. F allows you to change the brush size interactively by dragging the mouse and then LMB (the texture of the brush should be visible inside the circle). Typing a number then enter while using F allows you to enter the size numerically.

Adjusts the brush radius based on the stylus pressure when using a Graphics Tablet.

How powerful the brush is when applied.

Adjusts the brush strength based on the stylus pressure when using a Graphics Tablet.

Only paint over strokes.

Only paint over fill areas.

Paint over strokes and fill areas.

See the global brush settings for Cursor settings.

The color of the brush. See Color Picker.

Note that Vertex Paint works in sRGB space and the RGB representation of the same colors will be different between the paint tools and the materials that are in linear space.

The active Color Palette. See Color Palette.

See the global brush settings for Falloff settings.

---

## Brush Settings¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/weight_paint/tool_settings/brush_settings.html

**Contents:**
- Brush Settings¶

Brush settings panel.¶

Information on brush settings for every mode can be found in these pages:

General and advanced settings.

Stroke methods and settings.

Falloff curves and settings.

Cursor and appearance settings.

---

## Brush Settings¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/tool_settings/brush_settings.html

**Contents:**
- Brush Settings¶

Data-block selector for the material. Except for the Erase tool of course.

Pin the material to the brush.

The final appearance of the strokes is a combination of the brush and material used, binding the material to the brush gives more control and avoids a lack of coordination between the two.

---

## Brush Settings¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/weight_paint/tool_settings/brush.html

**Contents:**
- Brush Settings¶

Painting needs paint brushes and Blender provides a Brush panel within the Toolbar when in Weight Paint Mode.

In the Data-Block menu you find predefined Brush presets. And you can create your own custom presets as needed.

The radius defines the area of influence of the brush.

Adjusts the radius based on the stylus pressure when using a Graphics Tablet.

This is the amount of paint to be applied per brush stroke.

Adjusts the strength based on the stylus pressure when using a Graphics Tablet.

When enabled, use Strength falloff for the brush. Brush Strength decays with the distance from the center of the brush.

The weight (visualized as a color) to be used by the brush.

Using Ctrl-RMB you can set the weight to the value that’s under the cursor.

Brush direction toggle, Add adds weight value while Subtract removes weight value. This setting can be toggled with D.

---

## Brush Settings¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/sculpting/tool_settings/brush.html

**Contents:**
- Brush Settings¶
- Cursor¶

Sidebar ‣ Tool ‣ Brush Settings

This option controls the radius of the brush, measured in pixels. F allows you to change the brush size interactively by dragging the mouse and then LMB (the texture of the brush should be visible inside the circle). Typing a number then enter while using F allows you to enter the size numerically.

Adjusts the radius based on the stylus pressure when using a Graphics Tablet.

Controls how much each application of the brush affects the model. For example, higher values cause the Randomize brush to add noise to the strokes more quickly, and cause the Smooth brush to soften the strokes more quickly.

You can change the brush strength interactively by pressing Shift-F in the 3D Viewport and then moving the brush and then LMB. You can enter the size numerically also while in Shift-F sizing.

Adjusts the strength based on the stylus pressure when using a Graphics Tablet.

When enabled, use Strength falloff for the brush. Brush Strength decays with the distance from the center of the brush.

Filters the effect of the brush over the strokes. Applies to Smooth and Randomize brushes only.

If there is no filter selected Affect Position is the default behavior.

Toggles the brush effect on the position of the stroke points.

Toggles the brush effect on the strength (alpha) of the stroke points.

Toggles the brush effect on the thickness of the stroke points.

Toggles the brush effect on the UV rotation of the stroke points.

The influence direction of the brush. This can be Add or Subtract.

The cursor can be disabled by toggling the checkbox in the Cursor header.

Set the color of the brush ring. Depending on the current mode there will be options to set a single Color or a Color for Adding/Subtracting.

---

## Brush Settings¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/brush/brush_settings.html

**Contents:**
- Brush Settings¶
- Unified Settings¶
- General¶
- Advanced¶
- Color Picker¶
  - Randomize Color¶
- Color Palette¶

Each mode and brush has unique brush settings. But there is also a lot of overlap or similar settings. This page explains general and mode specific settings that are used across various brushes in more detail.

Changes to the settings of a brush asset are temporary and will be discarded when Blender is closed. To preserve settings, save them to the currently active brush asset using Save Changes to Asset, or create a new brush asset using Duplicate Asset, see Asset Operators. Loading a different file while Blender remains open does not discard the settings.

Some settings (e.g. size, strength, color), indicated with , allow for using a per-mode setting instead of the individual brush setting. These settings are shared across all brushes of a given mode (e.g. Sculpt Mode) but do not overwrite the individual brush value.

This option controls the size of the brush, measured in pixels. F allows you to change the brush size interactively by dragging the mouse from left to right and then LMB to accept. Meanwhile the texture of the brush will be visible inside the circle. You can also enter the size numerically with the number keys.

The size can be decreased/increased using [ and ] respectfully.

Adjusts the size based on the stylus pressure when using a Graphics Tablet.

Use the same brush Size across all brushes.

Show or hide the customizable pressure curve.

By default this is a straight line with positive slope such that increased pressure results in a larger brush size.

For the curve controls see: Curve widget.

Controls how the brush Size is measured.

The Size is measured based on how the cursor appears on the monitor i.e. “screen space”.

The Size is measured based on real world units. This means that the brush size stays consistent, independently from zooming in and out in the viewport. The unit type and scaling can be configured in the Scene Units.

For painting brushes the Strength defines the maximum effect of each brush stroke. For example, higher values cause a Paint brush to give each stroke a higher opacity. The opacity is never stronger than the set Strength, no matter how often the same surface is painted during the same stroke.

For sculpting brushes on the other hand the Strength relates to how strong each step of the stroke is, resulting in a slower/faster buildup towards the full brush effect during the stroke.

You can change the brush strength interactively by pressing Shift-F and then moving the brush and then LMB. You can also enter the strength numerically with the number keys.

Adjusts the strength based on the stylus pressure when using a Graphics Tablet.

Use the same brush Strength across all brushes.

Show or hide the customizable pressure curve.

By default this is a straight line with positive slope such that increased pressure results in a stronger brush deformation.

For the curve controls see: Curve widget.

Set the way the color or value is applied over the targeted Color Attribute, Vertex Group or Image Texture. See Color Blend Modes.

Add Alpha: makes the image more opaque where painted.

Erase Alpha: makes the image transparent where painted, allowing background colors and lower-level textures to show through. As you “paint”, the false checkerboard background will be revealed. Using a tablet pen’s eraser end will toggle on this mode.

In order to see the effects of the Erase and Add Alpha mix modes in the Image Editor, the Display Channels must be set to Color & Alpha or Alpha. Transparent (no alpha) areas will then show a checkered background.

The weight value that is applied to the vertex group.

Use Shift-X to sample the weight value of clicked vertex. Shift-Ctrl-X lets you select the group from which to sample from.

Brush direction toggle, Add raises geometry towards the brush, Subtract lowers geometry away from the brush. This setting can be toggled with Ctrl while sculpting.

Determines the ratio of how much the brush radius is used to sample the normal direction of the sculpt plane of the brush. For example, a smaller Normal Radius will lead to drastic changes in the brush orientation, like for following the contours of hard surface meshes more closely. A large Normal Radius will lead to smoother changes in orientation, like for building overall forms on organic sculptures.

The ratio between the brush radius and the radius that is going to be used to sample the area plane depth.

Determines how much the tilt of the user’s tablet pen affects the brush normal. Negative values correspond to inverting the direction of the tilt.

How close the brush falloff starts from the edge of the brush.

The factor to control how round the brush is. A value of zero will make the brush square. Note, the Brush Falloff is only applied to the rounded portions of the brush.

Sets the amount of smoothing to be applied to each stroke.

The higher this setting is set, the more Dyntopo aligns mesh edges to the brush direction while tessellating the surface. This generates cleaner edge flow to help define sharp features. Topology Rake can have a severe performance impact so it works best on low-poly meshes.

Constrains brush movement along the surface normal. Especially useful with the Grab brush, can be temporarily enabled by holding Ctrl. E.g. Grab brush can be used to push a depression (hole) into the mesh when Normal Weight is set.

Applies to Grab and Snake Hook brushes.

Offset for planar brushes (Clay, Fill, Flatten, Scrape), shifts the plane that is found by averaging the faces above or below.

Ability to limit the distance that planar brushes act. If trim is enabled vertices that are further away from the offset plane than the trim distance are ignored during sculpting.

Pushes the mesh towards/away from the brush center during the stroke.

How the deformation of the brush will affect the object.

Deform the geometry directly.

Deform the mesh while a cloth simulation is applied to it at the same time.

Defines the basic behavior and the available settings. Through the settings of a brush type, brushes can be created that produce vastly different effects.

The Essentials asset library contains brushes for each of the brush types. Their preview image and description should give a good idea of the effect the brush produces, with the particular combination of brush type and settings. Because of this, they are usually the more useful starting point for custom brushes than the mere brush type is, which is why the brush type is part of the Advanced brush settings.

Brushes and Brush Types of each mode:

Causes stroke dabs to accumulate on top of each other.

When enabled, the brush only affects vertices that are facing the viewer.

When this is disabled, it prevents changes to the alpha channel while painting (Only in 3D Viewport).

Toggles Anti-Aliasing around the brush, this is useful if you are working with pixel art or low resolution textures.

The auto-masking toggles in the brush settings are the same as the sculpt mode auto-masking settings. The difference is that these toggles can be customized per brush to create specific brush behaviors.

For more information on the Auto-Masking toggles, see Auto-Masking.

Use this menu to set the plane in which the sculpting takes place. In other words, the primary direction that the vertices will move.

The movement takes place in the direction of average normal for all active vertices within the brush area. Essentially, this means that the direction is dependent on the surface beneath the brush.

Sculpting in the plane of the current 3D Viewport.

The movement takes place in the positive direction of one of the global axes.

When locked it keeps using the normal of the surface where stroke was initiated, instead of the surface normal currently under the cursor.

When locked keep using the plane origin of surface where stroke was initiated, instead of the surface plane currently under the cursor.

Brushes have two colors that can be set using the Color Picker:

Primary Color: The active color used for painting by default.

Secondary Color: An alternate color that can be quickly accessed.

By default, painting uses the primary color. The secondary color can be used temporarily by holding Ctrl while painting. The two colors can also be swapped at any time using Swap Colors.

Press Shift-X to sample a color from the image and set it as the primary brush color.

In Texture Paint, Shift-Ctrl-X samples the merged viewport color, while Shift-X samples only the currently active texture.

Swaps the primary and secondary colors.

Use the same brush color across all brushes.

Note that Vertex Paint works in sRGB space, and the RGB representation of the same colors will be different between the paint tools and the materials that are in linear space.

A gradient can be used as a color source.

The Color Ramp Widget to define the gradient colors.

Will choose a color from the color ramp according to the stylus pressure.

Will alter the color along the stroke and as specified by Gradient Spacing option. With Clamp it uses the last color of the color ramp after the specified gradient.

Similar to Clamp. After the last color it resets the color to the first color in the color ramp and repeats the pattern.

Applies random variation to the brush color for more natural and varied strokes. Useful for hand-painting textures or adding subtle irregularities.

The randomness can affect hue, saturation, and value independently. Each channel also supports pressure sensitivity and stroke-based randomness.

Amount of random variation applied to the hue of the brush color.

Apply a single random hue per stroke instead of varying continuously during the stroke.

Modulate hue variation based on pen pressure.

Amount of random variation applied to the saturation of the brush color.

Apply a single random saturation per stroke instead of varying continuously during the stroke.

Modulate saturation variation based on pen pressure.

Amount of random variation applied to the value (brightness) of the brush color.

Apply a single random value per stroke instead of varying continuously during the stroke.

Modulate value variation based on pen pressure.

Color Palettes are a way of storing a brush’s color so that it can be used at a later time. This is useful when working with several colors at once.

A Data-Block Menu to select a palette.

Adds the current brush’s primary Color to the palette.

Removes the currently selected color from the palette.

Moves the selected color up/down one position.

Sort Colors by Hue, Saturation, Value, Luminance.

Each color that belongs to the palette is presented in a list. Clicking on a color will change the brush’s primary Color to that color.

---

## Clay Thumb¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/clay_thumb.html

**Contents:**
- Clay Thumb¶
- Brush Settings¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Similar to the Clay brush. It imitates the effect of deforming clay with the finger, accumulating material during the stroke. The sculpt plane tilts during the stroke in the front part of the brush to achieve this effect.

More info at General brush settings and on Advanced brush settings.

---

## Cloth¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/cloth.html

**Contents:**
- Cloth¶
- Brush Settings¶
  - General¶
  - Unique¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

This brush simulates cloth physics on the mesh under the brush cursor. There are various deformation types and settings to customize the brush.

It’s also easy to sculpt the mesh with other brushes and tools in between using the cloth brushes.

Using a relatively small brush size makes the calculations much faster, while larger brush sizes might be too slow to get a usable brush.

More info at General brush settings and on Advanced brush settings.

Allows the cloth brush to not accumulate deformation after each stroke. This is convenient to always simulate the cloth based on the same initial shape, but applying different forces to it.

When disabled, deformations accumulate after each stroke.

Resets the base mesh so that you can add another layer of deformations.

Selects the part of the mesh that is going to be simulated when the stroke is active. This can greatly affect performance depending on the complexity of the mesh.

Simulates only a specific area around the brush limited by a fixed radius.

Simulates the entire mesh.

The active simulation area moves with the brush while still being limited by a fixed radius.

The Factor added relative to the size of the radius to limit the cloth simulation effects.

The area to apply deformation falloff to the effects of the simulation. This setting is a factor of the Simulation Limit and is shown as a dashed line around the cursor.

Lock the position of the vertices in the simulation falloff area to avoid artifacts and create a softer transition with unaffected areas.

The type of cloth deformation that is used by the brush.

Simulates pulling the cloth to the cursor, similar to placing a finger on a table cloth and pulling.

Simulates pushing the cloth away from the cursor, similar to placing a finger on a table cloth and pushing.

Simulates pulling the cloth into a point.

Simulates pulling the brush into a line.

Simulates air being blown under the cloth so that the cloth lifts up.

Simulates picking up and moving the cloth.

Simulates stretching the cloth out.

Simulates moving the cloth without producing any artifacts in the surface and creates more natural looking folds than any of the other deformation modes. This is accomplished by adjusting the strength of the deformation constraints per brush step to avoid affecting the results of the simulation as much as possible.

Shape used in the brush to apply force to the cloth.

Applies the force as a sphere.

Applies the force as a plane.

Mass of each simulation particle.

How much the applied forces are propagated through the cloth.

The amount the cloth preserves its original shape, acting as a Soft Body.

Enables the detection of collisions with other objects during the simulation. In order for the sculpt object to collide with objects, the collision object must have Collision Physics activated.

---

## Crease¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/crease.html

**Contents:**
- Crease¶
- Brush Settings¶
  - General¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Create sharp indents or ridges by pushing or pulling the mesh, while pinching the vertices together.

Crease can also be used to sharpen and polish existing creases. Enable pressure sensitivity on Strength to regulate the add/subtract effect while pinching creases.

Adds a consistent pinching effect to your stroke. If set to 0 it the brush will behave like the Draw brush. If set to 1 and the brush strength set to 0, the brush will behave like a Pinch brush.

More info at General brush settings and on Advanced brush settings.

---

## Cursor¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/brush/cursor.html

**Contents:**
- Cursor¶

Tool Settings ‣ Brush Settings ‣ Cursor

Sidebar ‣ Tool ‣ Brush Settings ‣ Cursor

While painting or sculpting a special cursor is shown to display information about the active brush. The cursor is shown as a circle in the 3D Viewport, the radius of the circle matches the size of the brush.

The cursor can be disabled by toggling the checkbox in the panel’s header.

Set the color of the brush ring while performing an add/positive stroke.

In some paint/sculpt modes the brush can be negative and subtract information from the paint target; these brushes can be given a separate color.

Depending on the paint or sculpt mode different overlays are shown within the cursor to give information on how the brush is textured. This is most commonly used to show the brush falloff with a gradient from the circle center to the perimeter.

You can change the amount of transparency used when showing the texture using the slider.

Allows you to turn off the viewport overlay during strokes.

Toggles whether to show or hide the given brush texture overlay.

---

## Draw Brushes¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/brushes/draw.html

**Contents:**
- Draw Brushes¶
- Brush Settings¶
  - Advanced¶
  - Stroke¶
    - Post-Processing¶
    - Randomize¶
    - Stabilize Stroke¶
  - Cursor¶

The Draw brush allows you to draw free-hand strokes.

Data-block selector for the material.

The radius of the brush in pixels.

F allows you to change the brush size interactively by dragging the pointer or by typing a number then confirm.

Adjusts the radius based on the stylus pressure when using a Graphics Tablet. The gradient of the pressure can be customized using the curve widget.

Control the stroke transparency (alpha). From fully transparent (0.0) to fully opaque (1.0).

You can change the brush strength interactively by pressing Shift-F in the 3D Viewport and then moving the pointer and then LMB. You can also enter the size numerically.

Adjusts the strength based on the stylus pressure when using a Graphics Tablet. The gradient of the pressure can be customized using the curve widget.

The shape of the start and end of the stroke.

Strokes start and stop with a curved shape.

Strokes start and stop with a straight cutoff.

Controls the minimum spacing between points in the stroke as a percentage of the brush size.

A lower spacing is useful when doing fast movements. Normally this would generate less samples and lead to a larger spacing between points. When the spacing percentage is lowered, more points are generated to ensure the minimum spacing.

When drawing slowly, the point density is usually already high. In this case the spacing setting doesn’t add new points. It only ensures a minimum spacing and won’t remove points.

The number of smoothing iterations to apply to the stroke while drawing.

Direction of the input device that gives the maximum thickness to the stroke (0° for horizontal).

Amount of thickness reduction when the stroke is perpendicular to the Angle value.

Amount of transparency (alpha) to apply from the border of the point to the center. Works only when the brush is using stroke materials of Dot or Box style.

Controls the width and height of the alpha gradient.

Post-processing methods that are executed on the strokes when you finished drawing, right after releasing the LMB or Pen tip. You can toggle the use of post-processing using the checkbox in the section panel header.

Strength of smoothing process on the points location along the stroke.

The number of smoothing iterations to apply to the stroke.

Number of subdivisions to apply to newly created strokes.

Reduces final points numbers in the stroke with an adaptive algorithm.

Automatically trim intersection strokes ends.

Activate the conversion of the newly created stroke to its outline.

Material used for outline stroke.

Thickness used for outline stroke.

Adds randomness to the position of the points along the stroke. You can toggle the use of Randomize using the checkbox in the section panel header.

The amount of randomness to apply using the pressure of the input device.

The amount of randomness to apply to the stroke strength value (alpha).

The amount of randomness to apply to the UV rotation.

Randomizes the hue, saturation, and value of the stroke’s Color.

The amount of jittering to add to the stroke.

Use randomness only at stroke level.

Uses the stylus pressure to control how strong the effect is. The gradient of the pressure can be customized using the curve widget.

Stabilize Stroke helps to reduce jitter of the strokes while drawing by delaying and correcting the location of points. You can toggle the use of Stabilize Stroke using the checkbox in the section panel header.

Minimum distance from the last point before the stroke continues.

A smooth factor, where higher values result in smoother strokes but the drawing sensation feels like as if you were pulling the stroke.

The cursor can be disabled by toggling the checkbox in the Cursor header.

Shows the brush linked material color in the viewport.

---

## Draw¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/draw.html

**Contents:**
- Draw¶
- Brush Settings¶
- VDM Displacement¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Moves vertices inward or outward, based the average vertex normals within the brush radius. This is a very default behavior for sculpting and can be used in most cases.

It is common to use this particular brush with heavy customization for creating many custom brushes.

More info at General brush settings and on Advanced brush settings.

Vector Displacement Maps are supported for the Draw brush to insert complex & overhanging shapes. Unlike regular displacement, this uses all 3 color channels of the image to displace geometry in three directions instead of just one.

An example of various VDM brushes used on a smooth head from the official demo file.¶

Download the demo file for more information and to try the feature out.

To use this feature, enable Vector Displacement in the texture panel. All stroke methods are supported, but the recommended behavior is Anchored.

Ideal images for vector displacement are open EXR files with color clamping disabled.

This feature is only supported with Area Plane mapping.

---

## Draw Face Sets¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/draw_facesets.html

**Contents:**
- Draw Face Sets¶
- Brush Settings¶
  - General¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Draw new or extend existing Face Sets with each stroke.

Holding Ctrl will continue drawing the same face set as the one under the cursor. Holding Shift will relax or smooth the edges of the face sets by modifying the underlying topology so edges flow along the perimeter of the face sets. This will remove the jagged lines visible after drawing or creating a face set.

More information in the Face Set Introduction.

While a lot of the general brush settings are supported, it’s not needed to change them from the default, as the brush purpose is very simple.

More info at General brush settings and on Advanced brush settings.

---

## Dyntopo¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tool_settings/dyntopo.html

**Contents:**
- Dyntopo¶

Sidebar ‣ Tool ‣ Dyntopo

Dynamic Topology (aka Dyntopo) can be toggled with the checkbox. With dynamic topology active, most brushes will subdivide the mesh during the stroke.

For a general explanation of dynamic topology, visit the Introduction.

Each Detail Type’s detail is set here. Depending on the Detail Type being used this property will rather show as a pixel count (px), or percentage.

R allows you to interactively set the detail, with a preview of the detail’s density in the 3D Viewport.

When using Constant Detail, it is possible to sample the detail value of a certain mesh area by clicking the pipette icon next to the detail setting and then clicking on the area.

Setting the option will determine which of the methods will be used when altering the topology.

Just like the Subdivide tool, this method will only subdivide topology to match the detail given.

When topology is too dense, and is smaller than the detail given, edges will be collapsed to fit the detail size appropriately.

This method combines the two methods, subdividing edges smaller than the detail size, and collapsing topology.

Dyntopo uses the following different detail methods to create dynamic detail on an object.

This method uses a detail size based on the number of pixels, and in turn will create topology in that size. Zoom out big details, zoom in small fine details.

To keep detail uniform across the entire object, Constant Detail can be used. The detail is a divisor of a Blender unit - higher values mean finer details.

Giving more control over the topology, with this method you can create topology based on the brush size. You can increase and lower topology by resizing the brush itself. The detail size is based the size of the brush itself, where full detail will create topology the size of the brush radius itself.

Similar to constant detail, this value sets a percentage value uniform across the object, but only applies detailing changes when using Flood Fill.

When using Constant or Manual Detailing, this option is made available, allowing you to fill the entire object with a uniform detail, based on the resolution.

---

## Editing Vertex Paint Colors¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/vertex_paint/editing.html

**Contents:**
- Editing Vertex Paint Colors¶
- Smooth Vertex Colors¶
- Dirty Vertex Colors¶
- Vertex Color from Weight¶
- Invert¶
- Levels¶
- Hue/Saturation/Value¶
- Brightness/Contrast¶
- Set Vertex Colors¶
- Sample Color¶

Paint ‣ Smooth Vertex Colors

Smooth colors across vertices.

Paint ‣ Dirty Vertex Colors

Generate a dirt map gradient based on cavity.

Blur strength per iteration.

Number of times to blur the colors (higher blurs more).

Clamps the angle for convex areas of the mesh. Lower values increase the contrast but can result in clamping. 90 means flat, 180 means infinitely pointed.

Clamps the angle for concave areas of the mesh. Higher values increase the contrast but can result in clamping. 90 means flat, 0 means infinitely deep.

When active it won’t calculate cleans for convex areas.

Choose optimal contrast by effectively lowering Highlight Angle and increasing Dirt Angle automatically. Disabling Normalize allows getting consistent results across multiple objects.

Paint ‣ Vertex Color from Weight

Converts the active weight into grayscale colors.

Adjust the levels of the selected vertices.

Paint ‣ Hue/Saturation/Value

Adjust the HSV values of the selected vertices.

Paint ‣ Brightness/Contrast

Adjust the brightness/contrast of the selected vertices.

Paint ‣ Set Vertex Colors

Fill the active Color Attribute with the current paint color.

Set color completely opaque instead of reusing existing alpha.

Adjust the brush color of the Draw tool to the color under the mouse cursor.

---

## Editing Vertex Paint Colors¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/vertex_paint/editing.html

**Contents:**
- Editing Vertex Paint Colors¶
- Set Color Attribute¶
- Reset Vertex Color¶
- Invert¶
- Levels¶
- Hue/Saturation/Value¶
- Brightness/Contrast¶

Paint ‣ Set Color Attribute

Sets the active color to all selected vertices.

Paint ‣ Reset Vertex Color

Removes the Color Attribute information of the active strokes, if no strokes are selected, all strokes are reset.

Adjust the levels of Color Attributes.

Paint ‣ Hue/Saturation/Value

Adjust the color’s HSV values.

Paint ‣ Brightness/Contrast

Adjust the color’s brightness/contrast.

---

## Editing Weight Paint¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/weight_paint/editing.html

**Contents:**
- Editing Weight Paint¶
- Assign from Bone Envelopes¶
- Assign Automatic from Bone¶
- Normalize All¶
- Normalize¶
- Mirror¶
- Invert¶
- Clean¶
- Quantize¶
- Levels¶

Edit Mode and Weight Paint Mode

Blender provides a set of helper tools for Weight Painting.

Some of the tools also provide a Subset filter to restrict their functionality to only specific vertex groups (in the Adjust Last Operation panel, displayed after the tool is called) with following options:

All tools also work with Vertex Selection Masking and Face Selection Masking. In these modes the tools operate only on selected vertices or faces.

Apply the envelope weight of the selected bone(s) to the selected vertex group.

Apply from the selected bone(s) to the vertex group the same “auto-weighting” methods as available in the Parent armature menu.

For each vertex, this tool makes sure that the sum of the weights across all vertex groups is equal to 1. This tool normalizes all of the vertex groups, except for locked groups, which keep their weight values untouched.

Keep the values of the active group while normalizing all the others.

This tool only works on the active vertex group. All vertices keep their relative weights, but the entire set of weights is scaled up such that the highest weight value is 1.0.

The Mirror Vertex Group tool mirrors the weights from one side of a perfectly symmetrical mesh to the opposite side. Those vertices that have no corresponding vertex on the other side will not be affected. But note, the weights are not transferred to the corresponding opposite bone weight group.

Mirroring only works when the object’s rest pose is perfectly symmetrical across the X axis.

With this option checked, every selected vertex receives the weight information of its symmetrical counterpart. If both vertices are selected, it will be a weight information exchange; if only one is selected, information from the unselected will overwrite the selected one. Information on weight is passed for the active group only, unless All Groups is checked, in which case it is passed for all groups.

Works with selected vertices that belong to vertex groups with “symmetrical names” (with components like “L”, “R”, “right”, “left”). All selected vertices that belong to the active group, or to the symmetrical of the active group, will have their assignation to that group replaced by an assignation to the symmetrical one; however, its weight will be preserved. If All Groups is checked, all assignations to these kind of groups will be replaced by the symmetrical counterpart, also keeping the old weights.

Operate on all vertex groups, instead of the active one.

Mirror for meshes which are not fully symmetric (approximate mirror). See here for more information.

Mirror to Opposite Bone

If you want to create a mirrored weight group for the opposite bone (of a symmetric character), then you can do this:

Delete the target vertex group (where the mirrored weights will be placed).

Create a copy of the source bone vertex group (the group containing the weights which you want to copy).

Rename the new vertex group to the name of the target vertex group (the group you deleted above).

Select the target vertex group and call the Mirror tool (use only Mirror Weights and optionally Topology Mirror if your mesh is not symmetric).

Replaces each Weight of the selected weight group by × -1.0 weight.

Original 1.0 converts to 0.0

Original 0.5 remains 0.5

Original 0.0 converts to 1.0

Restrict the tool to a subset. See above The Subset Option about how subsets are defined.

Add vertices that have no weight before inverting (these weights will all be set to 1.0).

Remove vertices from the vertex group if they are 0.0 after inverting.

Locked vertex groups are not affected.

Clean Vertex Group Weights unassigns vertices from Vertex Groups whose weights are below the Limit. Removes weights below a given threshold. This tool is useful for clearing your weight groups of very low (or zero) weights.

In the example shown, a cutoff value of 0.2 is used (see operator options below) so all blue parts are cleaned out.

Note, the images use the Show Zero weights Active option so that unreferenced Weights are shown in Black.

Restrict the tool to a subset. See above The Subset Option for how subsets are defined.

This is the minimum weight value that will be kept in the group. Weights below this value will be removed from the group.

Ensure that the Clean tool will not create completely unreferenced vertices (vertices which are not assigned to any vertex group), so each vertex will keep at least one weight, even if it is below the limit value!

This operator uses a process known as Quantization which takes the input weights and clamps each weight to a number of steps between (0 - 1), so there is no longer a smooth gradient between values.

Quantize example (Steps = 2).¶

The number of steps between 0 and 1 to quantize the weights into. For example 5 would allow the following weights [0.0, 0.2, 0.4, 0.6, 0.8, 1.0].

Adds an offset and a scale to all weights of the selected weight groups. with this tool you can raise or lower the overall “heat” of the weight group.

No weight will ever be set to values above 1.0 or below 0.0 regardless of the settings.

Restrict the tool to a subset. See above The Subset Option for how subsets are defined.

A value from the range (-1.0 - 1.0) to be added to all weights in the vertex group.

All weights in the Subset are multiplied with the gain.

Whichever Gain and Offset you choose, in all cases the final value of each weight will be clamped to the range (0.0 - 1.0). So you will never get negative weights or overheated areas (weight > 1.0) with this tool.

The Smooth operator blends the weights of selected vertices based on the average of adjacent vertices, creating smoother transitions in weight painting. This operator is useful for refining weight distributions, improving deformation in rigging, and eliminating abrupt transitions between vertex weights.

This operator requires vertex selection to be enabled; otherwise, it will be unavailable.

Restrict the tool to a subset. See above The Subset Option about how subsets are defined.

Controls the amount of blending toward the average weight of connected vertices.

A Factor of 0.0 preserves the original weights.

A Factor of 1.0 fully adopts the calculated average weight.

Values between 0.0 and 1.0 blend the weights proportionally.

Sets how many times the smoothing operation is repeated. Higher values produce smoother results but may introduce unwanted artifacts in fine details.

Adjusts the smoothing influence by expanding or contracting the selection:

Positive values expand the selection to include neighboring vertices.

Negative values contract the selection to focus on a smaller subset of vertices.

Example: Single Selected Vertex

Consider a single selected vertex connected to four unselected vertices. The unselected vertices have weights: 1, 0, 0, and 0. The average weight of the unselected vertices is: \((1 + 0 + 0 + 0) / 4 = 0.25\)

0.0: The selected vertex retains its original weight.

1.0: The selected vertex adopts the calculated average weight (0.25).

Between 0 and 1: The vertex’s weight gradually shifts toward 0.25, blending proportionally.

Single vertex select with a Factor of 1.0.¶

Example: Multiple Selected Vertices

When multiple vertices are selected, the Smooth operator applies calculations to each vertex based on its adjacent unselected vertices.

A vertex connected to three unselected vertices with weights \((1, 0, 0)\) averages to \(0.333\).

A vertex connected to one unselected vertex with weight 1 averages to \(1.0\).

A vertex connected only to unselected vertices with weights \((0, 0, 0)\) remains unchanged with an average weight of \(0.0\).

These blended results depend on the Factor value.

Three selected vertices with a Factor of 1.0.¶

Example: Edge Loop Smoothing

In a practical use case, selecting a middle edge loop allows the operator to blend weights between adjacent areas. For example:

The edge loop has two unselected adjacent vertices on either side, with weights \(1\) and \(0\).

The average weight is \((1 + 0) / 2 = 0.5\).

Applying the Smooth operator with Factor set to 1.0 will turn the edge loop green, creating a smooth blend between the “hot” (left) and “cold” (right) sides.

Center edge loop of vertices selected with a Factor of 1.0.¶

Copy weights from other objects to the vertex groups of the active object.

By default this tool copies only the active (selected) vertex group of the source object to the active vertex group of target object or creates a new one if the group does not exist. However, you can change the tool’s behavior in the Adjust Last Operation panel.

For example, to transfer all existing vertex groups from the source objects to the target, change the Source Layers Selection option to By Name.

This tool uses the generic “data transfer”, but transfers from all selected objects to active one. Please refer to the Data Transfer docs for options details and explanations.

You first select all source objects, and finally the target object (the target object must be the active object).

It is important that the source objects and the target object are at the same location. If they are placed side-by-side, then the weight transfer will not work. (See the Vertex Mapping option.) You can place the objects on different layers, but you have to ensure that all objects are visible when you call the tool.

Now ensure that the target object is in Weight Paint Mode. Open the Toolbar and call the Transfer Weights tool in the Weight Tools panel.

You may notice that the Adjust Last Operation panel stays available after the weight transfer is done. The panel only disappears when you call another Operator that has its own Adjust Last Operation panel. This can lead to confusion when you use Transfer weights repeatedly after you changed your vertex groups. If you then use the still-visible Adjust Last Operation panel, then Blender will reset your work to its state right before you initially called the Transfer Weights tool.

So when you want to call the Transfer Weights tool again after you made some changes to your vertex groups, then always use the Transfer Weights button, even if the Adjust Last Operation panel is still available. Unless you really want to reset your changes to the initial call of the tool.

Reduce the number of weight groups per vertex to the specified Limit. The tool removes lowest weights first until the limit is reached.

The tool can only work reasonably when more than one weight group is selected.

Restrict the tool to a subset. See above The Subset Option for how subsets are defined.

Maximum number of weights allowed on each vertex.

Fill the active vertex group with the current paint weight.

Weight ‣ Sample Weight

Adjust the Weight of the Draw tool to the weight of the vertex under the mouse cursor.

Weight ‣ Sample Group

Select one of the vertex groups available under current mouse position.

Weights ‣ Gradient (Linear)

Applies a linear weight gradient; this is useful at times when painting gradual changes in weight becomes difficult. Blends the weights of selected vertices with unselected vertices.

Example of the Gradient tool being used with selected vertices.¶

The gradient starts at the current selected weight value, blending out to nothing.

Lower values can be used so the gradient mixes in with the existing weights (just like with the brush).

The shape of the gradient.

Create gradient that forms a straight line.

Create gradient that forms a circle.

Weights ‣ Gradient (Radial)

Applies a radial weight gradient; this is useful at times when painting gradual changes in weight becomes difficult. Blends the weights of selected vertices with unselected vertices.

The gradient starts at the current selected weight value, blending out to nothing.

Lower values can be used so the gradient mixes in with the existing weights (just like with the brush).

The shape of the gradient.

Create gradient that forms a straight line.

Create gradient that forms a circle.

Edit Mode and Weight Paint Mode

Vertex groups can be locked to prevent undesired edits to a particular vertex group.

Bones that belong to a locked vertex group are displayed in red the 3D Viewport.

Locks all vertex groups.

Locks selected vertex groups.

Locks unselected vertex groups.

Lock selected and unlock selected vertex groups.

Unlock selected and lock unselected vertex groups.

Unlocks all vertex groups.

Unlocks selected vertex groups.

Unlocks Unselected vertex groups.

Inverts the locks on all vertex groups.

---

## Face Sets¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/editing/face_sets.html

**Contents:**
- Face Sets¶
- Face Set from Masked¶
- Face Set from Visible¶
- Face Set from Edit Mode Selection¶
- Initialize Face Sets¶
- Grow/Shrink Face Sets¶
- Expand Face Set¶
- Extract Face Set¶
- Randomize Colors¶
- Display Settings¶

This page details the face set related hotkey operators and menu operators in sculpt mode.

There is a face set pie menu that can be accessed with Alt-W.

Face Sets ‣ Face Set from Masked

Creates a new face set from Masked Geometry.

Face Sets ‣ Face Set from Visible

Creates a new face set from all visible geometry.

Face Sets ‣ Face Set from Edit Mode Selection

Creates a new face set corresponding to the Edit Mode face selection.

Face Sets ‣ Initialize Face Sets

Initializes all face sets on the mesh at once based off one of several mesh attribute properties.

The mesh data attribute used to define the boundaries for the face sets.

Creates a new face set per discontinuous part of the mesh.

Creates a face set for each isolated face set. This mode is useful for splitting the patterns created by Face Set Expand into individual Face Sets for further editing.

Creates a face set per Material Slot.

Creates face sets for Faces that have similar Normals.

Creates face sets using UV Seams as boundaries.

Creates face sets using Edge Creases as boundaries.

Creates face sets using Bevel Weights as boundaries.

Creates face sets using Sharp Edges as boundaries.

The minimum value to consider a certain attribute a boundary when creating the face sets.

Face Sets ‣ Grow/Shrink Face Sets

Expands or contracts the face set under the cursor by adding or removing surrounding faces.

More info on Face Set Expand at the Expand page.

Face Sets ‣ Extract Face Set

Creates a new mesh based on the selected face set. Once the operator is initiated, hover over the face set and LMB to create the new mesh. After the operator is finished the new mesh will be selected in Object Mode.

Face Sets ‣ Randomize Colors

Generates a new set of random colors to render the face sets in the 3D Viewport.

Viewport Overlays – Sculpt ‣ Face Sets

The face sets display can be toggled as a viewport overlay. In the overlay popover, the opacity of the face sets overlay can be adjusted to make it more or less visible on the mesh.

---

## Falloff¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/brush/falloff.html

**Contents:**
- Falloff¶

The Falloff is a curve that determines how the strength of the brush decreases with increasing distance from the center. You can set up a custom curve or choose a predefined one.

Brush falloff example.¶

Shows a Curve Widget for configuring a custom falloff. The left side of the curve corresponds to the center of the brush while the right side corresponds to the edge.

The predefined falloff curves look as follows:

Determines how the falloff distance is calculated.

The falloff is calculated using a sphere in three-dimensional world space. If two points on the mesh appear near each other in the 3D Viewport but are far away in the world, painting one will not affect the other.

The falloff is calculated using a circle in two-dimensional screen space. If two points on the mesh appear near each other in the 3D Viewport, painting one will also affect the other, no matter their distance in the world.

Texture Paint Mode does not have this option – it always uses Projected.

Weakens the brush strength for faces whose normal points towards the screen edges instead of the camera.

This feature is not available in Sculpt Mode.

The minimum angle between the face normal and the viewing direction for the falloff to start.

---

## Grab¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/grab.html

**Contents:**
- Grab¶
- Brush Settings¶
  - General¶
  - Unique¶
- Additional Workflows¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Drag geometry across the screen, following the cursor. Grab only moves the vertices that are under the brush radius at the start of the stroke. This is an essential sculpting brush to be used frequently to build shapes and adjust proportions.

The effect is similar to moving geometry in Edit Mode with Proportional Editing enabled, except that Grab can make use of other Sculpt Mode options and brush settings.

Pressure Sensitivity is not supported for this brush type. More info at Size.

Pressure Sensitivity is not supported for this brush type. More info at Strength.

For this brush, this setting is a purely visual change. It does not alter the brush behavior. More info at Normal Radius.

This setting is not supported. More info at Auto-Smooth.

More info at General brush settings and on Advanced brush settings.

Applies the maximum strength of the brush to the highlighted active vertex, making it easier to manipulate low-poly models or meshes with modifiers.

Enabling this option also enables a white wireframe overlay within the brush radius. This helps to visualize the real base geometry that is being manipulated while sculpting with Modifiers.

Preserves the object’s silhouette shape by only grabbing vertices on one side of the mesh curvature. The shape of the silhouette is determined by the orientation of the 3D Viewport and the start of the stroke.

Note how in the image only the bottom side of the leg is pulled down, despite the size of the brush.

This setting is also useful for grabbing a single side of a crease and pushing it further inwards, creating a more pinched crease.

If the Falloff Shape is set to Projected, the brush can grab infinitely deep into the viewport. This is especially useful for much broader changes to a sculpt.

The stroke can also be started outside of the mesh (like in empty 3D space) and grab the vertices within the brush radius. This can be useful for sculpting flat and tube-like meshes.

---

## Grease Pencil Object Modes¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/index.html

**Contents:**
- Grease Pencil Object Modes¶

Object Modes allow editing different aspects of Grease Pencil objects. These modes are specifically tailored to the Grease Pencil object, unlike the more general modes, which work for other object types (with the exception of object mode which is the same for all objects).

Draw Mode is where new strokes are created. Strokes are directly sketched on a canvas, using different tools and brushes.

Sculpt Mode can be used to deform and shape existing strokes more organically. Strokes can be smoothed, deformed, or reshaped, adding fluidity and dynamism to drawings.

Edit Mode allows modifying individual strokes and points of Grease Pencil objects. This mode is ideal for fine-tuning linework, adjusting shapes, and refining details.

Vertex Paint Mode allows adding color the vertices of strokes directly. This mode is useful for adding shading, gradients, or detailed color effects providing finer control over the drawing’s appearance.

Weight Paint Mode allows assigning vertex weights to strokes. This is crucial for rigging and animating characters, ensuring smooth, and precise deformations based on the painted weights.

This mode allows working with the entire Grease Pencil object as a whole. It’s used for overall transformations and managing the placement of the object within the scene.

---

## Inflate¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/inflate.html

**Contents:**
- Inflate¶
- Brush Settings¶
  - General¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Similar to Draw, except that vertices are moved in the direction of their own normals. Especially useful when sculpting meshes with a lot of curvature.

Also available as a Mesh Filter to inflate all unmasked areas at once.

Either Inflate or Deflate sculpted areas. This is different from the typical Add & Subtract.

More info at General brush settings and on Advanced brush settings.

---

## Layer¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/layer.html

**Contents:**
- Layer¶
- Brush Settings¶
  - General¶
  - Unique¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

This brush is similar to Draw, except that the height capped. This creates the appearance of a flat layer.

It is recommended to use the Persistent setting and regularly Set Persistent Base, so that multiple strokes to not add on top of each other.

Higher by default to ensure the profile of layers is more noticeable. More info at Hardness

More info at General brush settings and on Advanced brush settings.

The fixed height of each stroke. This is measured using the scene scale, so it is consistent no matter the amount of zoom or object size.

This will ensure that multiple strokes use the same height, as if sculpting a single layer.

This button resets a new base so that you can sculpt new layer.

---

## Manage Brushes¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/brush/brush_management.html

**Contents:**
- Manage Brushes¶
- Asset Operators¶
- Manual Storage¶

Brush assets are stored in asset libraries to make them accessible from any Blender session. There are two ways of managing brush assets:

Using asset operators: Create and update brush assets using utility operators from any Blender file. Storage is managed by Blender. Convenient for simple “on the fly” management of personal brush asset libraries.

Using manual storage: Create and update brush assets by opening blend files within asset libraries, and managing brush asset data-blocks in there. Useful for careful curation of asset libraries, especially to prepare them for sharing with others.

Brushes can be managed through a few operators that let Blender handle the act of saving and updating the brushes in asset libraries for you. Assets managed this way will be saved in special asset system files using a .asset.blend file extension.

Note that only brush assets created via Duplicate Asset can be edited further using these asset operators. For others, these operations will be grayed out, and manual management is necessary.

Brushes from the Essentials asset library cannot be edited.

Sidebar ‣ Tool ‣ Brush Asset Properties ‣ Tool ‣ Brush Asset

Asset Shelf ‣ Context Menu

Brush Asset panel in the Sidebar showing asset operators.¶

Creates a copy of the currently active brush as asset, and activates it. A popup is spawned to input some settings to use:

A custom name to use for the new brush.

Choose an Asset Library to store the new brush asset in. The available asset libraries are configured in the Preferences.

Choose an Asset Catalog to assign the brush asset to. Entering a non-existent name/path will create a new catalog accordingly.

Permanently remove this brush asset from the Asset Library it is stored in. This cannot be undone, so a popup will ask for confirmation.

Spawns a popup to change some of the available asset metadata fields:

Choose an Asset Catalog to assign the brush asset to. Entering a non-existent name/path will create a new catalog accordingly.

See Asset Description.

Opens a window with the File Browser to select an image for the asset preview.

Saves any changes made to the active brush to the asset library.

Discards any unsaved changes made to the brush asset.

Complete description of the manual asset create, edit, share and use workflow.

It is also possible to manually manage brushes in blend-files like any other asset data-block. By marking brushes as assets and saving the file in an asset library, they become available from any Blender session. This gives full control over how assets are stored, and is particularly useful for curating asset libraries that can be shared with others.

The Mark as Asset operator used on a brush in the Outliner.¶

Brushes can be imported as normal data-blocks from other files (including from .asset.blend files from an asset library) through appending. In the Blender File mode of the Outliner, the brush will be listed under Brushes. Right-click the brush and select Mark as Asset. By saving the file inside of an asset library directory, the asset becomes available from all Blender sessions. If necessary, configure an asset library directory in the Preferences.

---

## Mask¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/editing/mask.html

**Contents:**
- Mask¶
- Invert Mask¶
- Fill Mask¶
- Clear Mask¶
- Box Mask¶
- Lasso Mask¶
- Mask Filters¶
- Expand Mask¶
- Mask Extract¶
- Mask Slice¶

This page details the mask related shortcut operators and menu operators in sculpt mode. Other related information to masks can also be found at the bottom of the page.

Masks can be edited across all visible faces. Using A opens a pie menu to choose the most common operations.

Inverts the visible mask. This is often useful when the masked vertices are the surfaces you want to sculpt/paint. In that case create a mask and then invert it.

Fully masks the visible geometry. Alternatively it is common to clear and then invert a mask via A to achieve the same effect.

Removes the mask on all visible vertices. To completely remove the mask data, see Clear Sculpt-Mask Data.

Works like the Box Mask tool, it creates a rectangular mask region. Hold Shift or press MMB to clear the mask of the selected region.

Can be used to create a free-form mask, similar to the Lasso Mask tool. This is very commonly used.

To clear the mask of areas with the Lasso Mask, first invert the mask, use Lasso Mask, and then invert the mask back.

Mask ‣ Smooth/Sharpen Mask, Grow/Shrink Mask, Increase/Decrease Contrast

Similarly to other Filter Tools, mask filters are operations that are applied to the whole mask.

Changes the sharpness of the mask edge. Using this can be faster and more consistent than smoothing the mask with the Mask brush.

Further grow or shrink the mask along the surface of the mesh.

Changes the contrast of the mask.

In the Adjust Last Operation panel there are further options to add iterations for a stronger effect.

The number of times the filter is applied.

Use an automatic number of iterations based on the number of vertices of the sculpt. Disable this option to set the Iterations manually.

An alternative to Iterations is to use Repeat Last via the shortcut Shift-R.

More info on Mask Expand along Topology at the Expand page.

Creates a duplicate mesh object based on masked geometry. The extracted geometry is also further processed by default for a cleaner result.

Minimum mask value to consider the vertex valid to extract a face from the original mesh.

Creates and extra boundary loop on the edges of the geometry, making it easier smooth the boundaries and apply additional modifiers.

Smooth iterations applied to the extracted mesh.

Project the extracted mesh on to the original sculpt object.

Adds a Solidify Modifier to the newly created mesh object.

Removes the masked vertices from the mesh.

Minimum mask value to consider the vertex valid to extract a face from the original mesh.

Fills concave holes with geometry that might have resulted from the Mask Slice operation.

If nothing is masked, this operation can be used to just fill all holes. Especially when using Trim Tools tools and the Voxel Remesher

Create a new object from the masked geometry.

Mask ‣ Mask from Cavity

Generates a mask based on the cavity of the surface. The settings of the operation can be changed in the Adjust Last Operation panel.

Choose how the newly created mask is mixed with the existing one. By default it will replace the old mask via “Mix”.

The factor of the mix effect. Choose how strong the new mask is applied on the existing one.

The same settings as the Auto-Masking settings are applied.

Same as Auto-Masking.

Same as Auto-Masking.

Same as Auto-Masking.

Same as Auto-Masking.

Mask ‣ Mask from Mesh Boundary

Generates a mask based on the topological islands of the mesh. The settings of the operation can be changed in the Adjust Last Operation panel.

Choose how the newly created mask is mixed with the existing one. By default it will replace the old mask via “Mix”.

The factor of the mix effect. Choose how strong the new mask is applied on the existing one.

The same settings as the Auto-Masking settings are applied.

Same as Auto-Masking.

Mask ‣ Mask from Face Sets Boundary

Generates a mask based on the face set islands of the mesh. The settings of the operation can be changed in the Adjust Last Operation panel.

Choose how the newly created mask is mixed with the existing one. By default it will replace the old mask via “Mix”.

The factor of the mix effect. Choose how strong the new mask is applied on the existing one.

The same settings as the Auto-Masking settings are applied.

Same as Auto-Masking.

Click on any color on the mesh to create a new mask (based on the active color attribute).

How much changes in color affect the mask generation. A smaller threshold includes fewer similar colors. A larger threshold includes much more similar colors.

Mask only contiguous color areas. Colors that don’t touch the one that you click on will not be masked.

Invert the generated mask.

Preserve previous mask and add or subtract the new one generated by the colors.

Generates a mask with random values for the entire object based on different mesh data.

Assigns a random mask value for each vertex.

Assigns a random mask value for each Face Set.

Assigns a random mask value for each disjoint part of the mesh.

Viewport Overlays – Sculpt ‣ Mask

The mask display can be toggled as a viewport overlay. In the overlay popover, the opacity of the mask overlay can be adjusted to make it more or less visible on the mesh.

Properties ‣ Object Data ‣ Geometry Data ‣ Clear Sculpt-Mask Data

Completely frees the mask data layer from the mesh. While not a huge benefit, this can speed-up sculpting if the mask is no longer being used.

---

## Mask¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/mask.html

**Contents:**
- Mask¶
- Brush Settings¶
  - General¶
  - Unique¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Paint a selection on parts of the mesh to be unaffected by other brushes & tools. The mask values are shown as a gray-scale overlay.

More information in the Masking Introduction.

More info at General brush settings and on Advanced brush settings.

The mask brush has two modes:

Holding Shift will instead smooth existing masks.

---

## Options¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/weight_paint/tool_settings/options.html

**Contents:**
- Options¶

Ensures that all deforming vertex groups add up to one while painting. When this option is turned off, then all weights of a point can have any value between 0 and 1. However, when vertex groups are used as deform groups for character animation then Blender always interprets the weight values relative to each other. That is, Blender always does a normalization over all deform bones. Hence in practice it is not necessary to maintain a strict normalization and further normalizing weights should not affect animation at all.

This option works most intuitively when used to maintain normalization while painting on top of weights that are already normalized with another tool.

---

## Options¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/weight_paint/tool_settings/options.html

**Contents:**
- Options¶

The weight paint options change the overall brush behavior.

Ensures that all deforming vertex groups add up to one while painting. When this option is turned off, then all weights of a vertex can have any value between 0 and 1. However, when vertex groups are used as deform groups for character animation then Blender always interprets the weight values relative to each other. That is, Blender always does a normalization over all deform bones. Hence in practice it is not necessary to maintain a strict normalization and further normalizing weights should not affect animation at all.

This option works most intuitively when used to maintain normalization while painting on top of weights that are already normalized with another tool.

Displays bone-deforming groups as if all locked deform groups were deleted, and the remaining ones were re-normalized. This is intended for use when balancing weights within a group of bones while all other bones are locked. With this option you can also temporarily view non-normalized weights as if they were normalized, without actually changing the values.

Paint on all selected vertex groups simultaneously, in a way that preserves their relative influence. This can be useful when tweaking weights in an area that is affected by more than three bones at once, e.g. certain areas on a character’s face.

This option is only useful in the Armature tab, where you can select multiple vertex groups by selecting multiple pose bones. Once at least two vertex groups are selected, viewport colors and paint logic switch to Multi-Paint mode, using the sum of the selected groups’ weights if Auto Normalize is enabled, and the average otherwise. Any paint operations aimed at this collective weight are applied to individual vertex group weights in such way that their ratio stays the same.

Since the ratio is undefined if all weights are zero, Multi-Paint cannot operate on vertices that do not have any weight assigned to the relevant vertex groups. For this reason it also does not allow reducing the weight all the way to zero. When used with X Mirror, it only guarantees completely a symmetrical result if weights are initially symmetrical.

While Multi-Paint cannot directly paint on zero-weight vertices, it is possible to use the Smooth Weight tool to copy a reasonable nonzero weight distribution from adjacent vertices without leaving Multi-Paint mode or changing bone selection.

To do that, enable vertex selection, select target vertices, and apply one iteration of the tool using vertex groups from Selected Pose Bones with low Factor. After that simply paint on top to set the desired collective weight.

This option limits the influence of painting to vertices (even with weight 0) belonging to the selected vertex group.

See the Brush Display options.

---

## Paint¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/paint.html

**Contents:**
- Paint¶
- Brush Settings¶
  - General¶
  - Unique¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Paints on the active color attribute. Hold Shift to blur painted colors instead.

Color attribute’s can be managed in the pallette pop-over in the middle of the header.

More information in the Painting Introduction.

This settings has a different effect on this brush. Instead of defining the strength of each individual step in the stroke, it determines the overall Opacity of the applied color.

Use the Flow setting instead for faster increasing of strength.

More info at General brush settings and on Advanced brush settings.

Amount of paint that is applied per stroke sample. Used to create fast/slow accumulation effect.

Amount of paint that is picked from the surface into the brush color. Can achieve the effect of a wet canvas.

Amount of wet paint that stays in the brush after applying paint to the surface.

Ratio between the brush radius and the radius that is going to be used to sample the color to blend in wet paint.

Amount of random elements that are going to be affected by this brush. Use this for a more detailed airbrush effect. This works best on a high resolution.

Scale of the brush tip in the X axis. This is useful for a achieving a painting stroke like a marker or paint roller.

---

## Pinch¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/pinch.html

**Contents:**
- Pinch¶
- Brush Settings¶
  - General¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Pulls geometry towards the center of the brush. When inverted via Ctrl it will Magnify geometry by pushing them away from the center of the brush.

More info at General brush settings and on Advanced brush settings.

---

## Plane¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/plane.html

**Contents:**
- Plane¶
- Brush Settings¶
  - General¶
  - Unique¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Moves vertices toward or away from the brush plane along its normal direction.

The Plane brush flattens geometry to a virtual plane or raises the surface relative to it, depending on brush settings. The Height and Depth parameters control the range of influence above and below the plane, allowing precise shaping of flat surfaces or plateaus.

More info at General brush settings and on Advanced brush settings.

Determines the range of influence of the brush above the brush plane. Increasing the height affects vertices farther above the plane.

Determines the range of influence of the brush below the brush plane. Increasing the depth affects vertices farther below the plane.

Determines the behavior of the brush when inverted.

When inverted, the brush displaces vertices away from the brush plane, resulting in increased contrast.

When inverted, the roles of the Height and Depth parameters are exchanged.

For example, if Height is set to 0.7 and Depth to 0.3, inverting the brush causes the roles of these parameters to be exchanged, resulting in an effective Height of 0.3 and Depth of 0.7.

Controls the stability of the brush plane’s orientation. The normal of the plane is averaged over the last few stroke steps, with the number of steps and blending factor determined by the parameter’s value.

When set to 0, the brush reacts immediately to changes in the in surface orientation.

When set to 1, the plane’s orientation remains constant throughout the stroke.

Intermediate values provide a gradual transition between these behaviors, resulting in a weighted moving average of plane normals.

Controls the stability of the brush plane’s position. Similar to Stabilize Normal, it works by averaging the position over the previous stroke steps.

Each position is calculated as the interpolated between the unstabilized position and its projection onto the plane of the previous stroke step.

---

## Pose¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/pose.html

**Contents:**
- Pose¶
- Brush Settings¶
  - General¶
  - Unique¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Deform a model simulating armature-like workflow. This can either be useful for posing a model without a rig, adjusting the proportions of a mesh or other fast deformations.

The brush will automatically determine an origin point, indicated with a while line on the brush cursor.

If the Deformation Target is changed, the brush can also be used for cloth sculpting.

Only Size and Auto-Masking has an impact on the brush behavior for this brush.

More info at General brush settings and on Advanced brush settings.

Deformation type that is used by the brush.

Rotates the mesh around the pose origin. When pressing Ctrl, the brush applies a twist rotation instead (and disables any IK segments that are used).

Scale the mesh based on the pose origin. While holding Ctrl the brush moves the mesh.

Works similar to Scale/Translate however, it applies different scale values along different axes to achieve the stretching effect.

Method to set the rotation origin for the pose origin or individual IK segments.

Sets the rotation origin automatically using the topology and shape of the mesh.

Creates a pose segment per Face Set, starting from the active face set. This can lead to the most accurate and desirable results.

Simulates a Forward Kinematics deformation using the Face Set under the cursor as control.

Offset of the pose origin in relation to the brush radius. This is useful to manipulate areas with a lot of complex shapes like fingers.

Controls the smoothness of the falloff of the deformation.

Controls how many IK segments are going to be created for posing. This can be seen by a divided white line on the cursor. This is also useful for making curved deformations with the pose brush, like hair clumps and tails.

When using Scale/Translate Deformation, do not rotate the segment; only scaling is applied.

Keeps the position of the last segment in the IK chain fixed. If this is disabled, the mesh can be dragged around more freely, creating snake like shapes.

The brush will only affect topologically connected elements. Disabling this will allow deforming multiple disconnected meshes at the same time, for example characters with clothing & shoes.

Disabling this setting can have a big impact on performance, as neighboring elements will be merged internally. Keeping the Max Element Distance as low as possible will help counteract the performance impact.

Maximum distance to search for disconnected loose parts in the mesh.

---

## Relax Slide¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/slide_relax.html

**Contents:**
- Relax Slide¶
- Brush Settings¶
  - General¶
  - Unique¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

This brush deforms the topology of the mesh while minimizing changes to the geometrical shape of the mesh. By default it will drag geometry, but this can be changed in the Deformation settings.

This brush is especially useful for redistributing topology to areas that require more detail, or sliding geometry to somewhere where they should be.

Holding Shift changes the brush effect to Relax geometry, creating an even distribution of topology.

More info at General brush settings and on Advanced brush settings.

Deformation type that is used by the brush.

Slides the topology of the mesh in the direction of the stroke.

Slides the topology of the mesh towards the center of the stroke.

Slides the topology of the mesh away from the center of the stroke.

---

## Rotate¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/rotate.html

**Contents:**
- Rotate¶
- Brush Settings¶
  - General¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Rotates geometry in the direction in which the cursor is moved. The initial drag direction is the zero angle and by rotating around the center you can create a vortex/swirl effect.

More info at General brush settings and on Advanced brush settings.

---

## Sculpting Brushes¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/sculpting/brushes.html

**Contents:**
- Sculpting Brushes¶

Brushes for Grease Pencil Sculpt mode bundled in the Essentials library. See Brush for more information.

Eliminates irregularities in the area of the drawing within the brush’s influence by smoothing the positions of the points.

Increase or decrease the points thickness in the area of the drawing within the brush’s influence.

Increase or decrease the points transparency (alpha) in the area of the drawing within the brush’s influence.

Add noise to the strokes in the area of the drawing within the brush’s influence by moving points location in a random way.

Used to drag a group of points around. Unlike the other brushes, Grab does not modify different points as the brush is dragged across the model. Instead, Grab selects a group of points on mouse-down, and pulls them to follow the mouse. The effect is similar to moving a group of points in Edit Mode with Proportional Editing enabled.

Moves points in the direction of the brush stroke.

Twist the points in counter-clockwise (CCW) or Clockwise (CW) rotation.

Pulls points towards the center of the brush. The inverse setting is Inflate, in which points are pushed away from the center of the brush.

Adds copies of the strokes in the clipboard in the center of the brush. You have to copy the selected strokes you want into the clipboard with Ctrl-C before using the tool.

---

## Sculpt¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/editing/sculpt.html

**Contents:**
- Sculpt¶
- Transform¶
- Show & Hide¶
- Fairing¶
- Trimming¶
- Mesh Filters¶
- Sample Color¶
- Set Pivot¶
- Rebuild BVH¶
- Dynamic Topology Toggle¶

This page details the general hotkey operators and menu operators in sculpt mode.

Change the position of the object.

Change the orientation of the mesh.

Increase/decrease the size of the mesh.

Morph the mesh to a spherical shape.

Some very common hotkey operators to control the visibility based on face sets. These are not part of any menu and have to be used via the shortcuts. More visibility operators can be found in the Face Sets Menu and the Pie Menu shortcut Alt-W. (Since visibility is often toggled via face sets.)

Draw a box to hide faces of a mesh.

Draw a box to reveal hidden faces. This works similar to the Box Select tool.

Hide all face sets except the active one (under the cursor). If face sets are already hidden, then this operator will show everything.

Hide the face set under the cursor. Press Shift-H afterwards to show everything.

Reveal all hidden geometry.

Hides all visible geometry and makes all hidden geometry visible.

Hides all masked vertices.

Grows or shrinks the visible area of the mesh along its surface.

For a more general introduction see Visibility, Masking & Face Sets.

These operators smooths geometry patches based of a Face set.

Creates a perfectly flat and smooth geometry patch from the face set. This is the ideal way to trim parts of your mesh if the vertex count is too high for other operations, or the vertex IDs must not be altered (Like when using Multires sculpting).

Creates a smooth as possible geometry patch from the face set by minimizing changes in vertex tangents. This is ideal for creating smooth curved surfaces on complex topology, where just using the smooth brush will not lead to desired results

The trimming operators add or remove geometry from the mesh based on a gesture input. These operators are especially useful for sketching an early base mesh for further sculpting with the voxel remesher.

Flattens the geometry along a plane determined by the camera view and a drawn line. The region of the mesh being flattened is visualized by the side of the line that is shaded.

Removes geometry based on a box selection.

Removes geometry based on a lasso selection.

Adds geometry based on a box selection.

Adds geometry based on a lasso selection.

Applies a deformation to all vertices in the mesh at the same time. Masking, auto-masking and visibility will be taken into account.

To use these operators, click and drag away from left to right or from right to left for a negative effect.

Smooths the positions of the vertices to either polish surfaces or remove volume from larger shapes. Especially useful to fix most of the artifacts of the voxel remesher. This filter works similar to the Smooth brush.

Eliminates irregularities of the mesh by making the positions of the vertices more uniform while preserving the volume of the object. This filter works similar to the Surface deformation type of the Smooth brush.

Displaces vertices uniformly along their normal. This filter works similar to the Inflate brush.

Tries to create an even distribution of quads without deforming the volume of the mesh. This filter works the same as holding Shift with the Slide Relax brush.

This will remove the jagged lines visible after drawing or creating a face set. This filter works the same as holding Shift with the Draw Face Set brush.

Sharpens and smooths the mesh based on its curvature, resulting in pinching hard edges and polishing flat surfaces. Especially useful when sculpting hard surfaces and stylized models with creasing and flattening brushes.

Increases the high frequency surface details of the mesh by intensifying the difference between creases and valleys. This filter works similar to the inverted direction of the Smooth brush.

Deletes displacement information of the Multires Modifier, resetting the mesh to a regular subdivision surface result. This can be used to reset parts of the sculpt or to fix reprojection artifacts after applying a Shrinkwrap Modifier.

Negative strokes will intensify the displacement details, this method works similar to Enhance Details and can give better results in some circumstances.

Randomly moves vertices along the vertex normal. This filter works similar to the Randomize Transform.

Sculpt ‣ Sample Color

Adjust the brush color of the Paint tool to the color under the mouse cursor.

Like Object and Edit Mode, Sculpt Mode also has a Pivot Point. This is because the basic move, rotate and scale transforms are also supported in Sculpt Mode. But the pivot point in Sculpt Mode is unique. It always moves together with the transformed mesh and can be both manually & automatically placed.

Sets the pivot to the origin of the sculpt.

Sets the pivot position to the average position of the unmasked vertices.

Sets the pivot position to the center of the mask’s border. This operation will automatically happen when using Expand.

Sets the pivot position to the active vertex position.

Sets the pivot position to the surface under the cursor.

For more convenient placement of the pivot point it’s recommended to use the shortcut assigned to Surface.

For a more general introduction see Transforming.

Recalculates the BVH used by Dyntopo to improve performance, which might degrade over time while using Dyntopo.

For a more general introduction see Adaptive Resolution.

Sculpt ‣ Transfer Sculpt Mode

Switches Sculpt Mode from the Active object to the object under the mouse. See Switching Objects for more information.

For a more general introduction see Working with Multiple Objects.

---

## Selection & Visibility¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/selection_visibility.html

**Contents:**
- Selection & Visibility¶
- Selection Masking¶
  - Details About Selecting¶
  - Vertex Selection Masking¶
  - Face Selection Masking¶
  - Hide/Unhide Faces¶
  - Hide/Unhide Vertices¶
  - The Clipping Region¶
- Select Linked¶

If you have a complex mesh, it is sometimes not easy to paint on the intended vertices. Suppose you only want to paint on a small area of the Mesh and keep the rest untouched. This is where “selection masking” comes into play. When this mode is enabled, a brush will only paint on the selected vertices or faces. The option is available from the header of the 3D Viewport (see icons surrounded by the yellow frame):

You can choose between Face Selection masking (left button), Vertex selection masking (middle button), and Bone selection (right button). The latter is only available when the mesh has an Armature modifier.¶

Selection masking has some advantages over the default paint mode:

The original mesh edges are shown, even when modifiers are active.

You can select and deselect faces instead without the need to switch to Edit Mode.

The following standard selection operations are supported:

Alt-LMB – Single faces

Shift-Alt-LMB – Select more or remove them from the selection.

A – All faces, A A to deselect.

C – Circle select with brush.

Ctrl-I – Invert selection.

L – Pick linked (under the mouse cursor).

Ctrl-L – Select linked.

Ctrl-NumpadPlus – Extend Selection

Ctrl-NumpadMinus – Shrink Selection

The following only work for face selection and with the selection tool active:

Alt-LMB – Loop Select

Vertex and Weight Paint Modes

In this mode you can select one or more vertices and then paint only on the selection. All unselected vertices are protected from unintentional changes.

Vertex Selection masking.¶

Texture, Vertex, and Weight Paint Modes

The Face Selection masking allows you to select faces and limit the paint tool to those faces, very similar to Vertex selection masking.

Face Selection masking.¶

You also can hide selected faces as in Edit Mode with the keyboard Shortcut H, then paint on the remaining visible faces and finally unhide the hidden faces again by using Alt-H.

You cannot specifically hide only selected faces in vertex mask selection mode. However, the selection is converted when switching selection modes. So a common trick is to:

Switch to Face selection mask mode to have the selection converted to faces.

Refine your selection next or just hide the faces.

Switch back to Vertex Selection mask mode.

Hiding faces will make sure that vertices that belong to visible faces remain visible.

To constrain the paint area further you can use the Clipping Region. Press Alt-B and LMB-drag a rectangular area. The selected area will be “cut out” as the area of interest. The rest of the 3D Viewport gets hidden.

The Clipping Region is used to select interesting parts for local painting.¶

You make the entire mesh visible again by pressing Alt-B a second time.

All paint tools that use the view respect this clipping, including box select, and of course brush strokes.

There are two helpful reminders that a Clipping Region is used:

The clipping region is drawn as a gray box in the 3D Viewport

The Text Info overlay will state that the perspective is “Clipped”

Select ‣ Select Linked ‣ Linked

Select geometry connected to already selected elements. This is often useful when a mesh has disconnected, overlapping parts, where isolating it any other way would be tedious. Pressing Shift-L will deselect linked any linked elements.

With L you can also select connected geometry directly under the cursor.

---

## Smear¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/smear.html

**Contents:**
- Smear¶
- Brush Settings¶
  - General¶
  - Unique¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Smears the painted colors of the active color attribute. It takes the colors under the cursor, and blends them in the direction of your stroke.

More info at General brush settings and on Advanced brush settings.

Smear colors along the direction of the stroke.

Smear colors inwards towards your brush center.

Smear colors outwards away from your brush center.

---

## Smear Multires Displacement¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/multires_displacement_smear.html

**Contents:**
- Smear Multires Displacement¶
- Brush Settings¶
  - General¶
  - Unique¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

This tool deforms displacement information of the Multires Modifier, moving the displaced vertices without affecting the base mesh.

Smearing effect can be used multiple times over the same area without generating any artifacts in the topology.

This brush works best after using Apply Base.

More info at General brush settings and on Advanced brush settings.

Deformation type that is used by the brush.

Pulls the displacement values in the direction of the brush.

Pulls the displacement values towards the center of the brush, creating hard surface effects without pinching the topology.

Pushes the displacement values away from the brush center, smoothing the displacement.

---

## Snake Hook¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/snake_hook.html

**Contents:**
- Snake Hook¶
- Brush Settings¶
  - General¶
  - Unique¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Pulls vertices along with the movement of the brush to create long, snake-like forms. During the stroke, geometry will be dynamically picked up & let go.

When the Rake setting is used, the brush can also be used to rotate geometry via dragging.

More info at General brush settings and on Advanced brush settings.

Pulled geometry tends to lose volume along the stroke. With Magnify value greater than 0.5 this is prevented. More info at Pinch/Magnify

Rotates geometry along the direction of the stroke.

Deformation type that is used by the brush.

Applies the brush falloff to the tip of the brush.

Modifies the entire mesh using an Elastic deformation. More info in the Elastic Deform brush.

---

## Stroke¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/brush/stroke.html

**Contents:**
- Stroke¶
- Stabilize Stroke¶

The stroke settings define the behavior of the sculpted/painted stroke. Any other brush behavior and effect is applied on top of the stroke.

Defines the way brush strokes are applied to the canvas.

Apply paint on each mouse move step. This is regardless of their distance to each other, and instead depends on the stroke speed. This means that a slower stroke will have more accumulative strength applied.

Leaves only one dab on the canvas which can be placed by dragging.

Creates brush stroke as a series of dots, whose distance (spacing) is determined by the Spacing setting.

Limits brush application to the distance specified by the percentage of the brush radius.

Brush Spacing can be affected by enabling the pressure sensitivity icon, if you are using a Graphics Tablet.

Flow of the brush continues as long as the mouse click is held (spray), determined by the Rate setting.

Interval for how frequent the brush is applied during the stroke.

Creates a single dab at the brush location. Clicking and dragging will resize the dab diameter.

The brush location and orientation are determined by a two point circle, where the first click is one point, and dragging places the second point, opposite from the first.

Clicking and dragging lets you define a line in screen space. The line dabs are separated by Spacing, similar to space strokes. With Alt the line stroke is constrained to 45 degree increments.

Defines the stroke curve with a Bézier curve (dabs are separated according to Spacing). This Bézier curve is stored in Blender as a “Paint Curve” data-block.

Use Ctrl-RMB to create the initial control point of the curve.

Paint Curves are reusable and can be stored and selected by using the Data-Block Menu menu.

You can define additional curve control points by using Ctrl-RMB. The handles can be defined by dragging the mouse. The stroke flows in the direction of the first control point to the second control point, and so on.

The control points and handles can be dragged with RMB (In right click select with LMB). To make sure that the handles of a control point are symmetrical, drag them using Shift-RMB. A few transform operators are supported such as moving (G), rotating (R) and scaling (S).

The handles can be selected individually by using LMB (In right click select with RMB), extend the selection by Shift-LMB and deselect/select all by using A.

To delete a curve point, use X.

To confirm and execute the curved stroke, press Return or use the Draw Curve button. Alternativey, Ctrl-LMB can be used to execute the stroke (In right click select with LMB).

Method used to calculate the distance to generate a new brush step.

Calculates the brush spacing relative to the view.

Calculates the brush spacing relative to all three dimensions of the scene using the stroke location. This avoids artifacts when sculpting across curved surfaces and keeps the spacing much more consistent.

Keep the brush strength consistent, even if the spacing changes. Available for the Space, Line, and Curve stroke methods.

Ratio of samples in a cycle that the brush is enabled. This is useful to create dashed lines in texture paint or stitches in Sculpt Mode. Available for the Space, Line, and Curve stroke methods.

Length of a dash cycle measured in stroke samples. This is useful to create dashed lines in texture paint or stitches in Sculpt Mode. Available for the Space, Line, and Curve stroke methods.

Jitter the position of each step in the brush stroke.

Brush Jitter can be affected by enabling the pressure sensitivity icon, if you are using a Graphics Tablet.

Show or hide the customizable pressure curve.

By default this is a straight line with positive slope such that increased pressure results in more jitter of the brush positions.

For the curve controls see: Curve widget.

Controls how the brush Jitter is measured.

The Jitter is relative to the view direction i.e. “screen space”.

The Jitter is measured relative to all three dimensions of the scene. The unit type and scaling can be configured in the Scene Units.

Recent mouse locations (input samples) are averaged together to smooth brush strokes.

Use the same brush Input Samples across all brushes.

Stabilize Stroke makes the stroke lag behind the cursor and creates a smoothed curve to the path of the cursor. This can be enabled pressing Shift S or by clicking the checkbox found in the header.

Minimum distance from the last point before the stroke continues.

A smooth factor, where higher values result in smoother strokes but the drawing sensation feels like as if you were pulling the stroke.

---

## Symmetry¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/weight_paint/tool_settings/symmetry.html

**Contents:**
- Symmetry¶

Toolbar ‣ Tool ‣ Symmetry

Use this option for mirrored painting on groups that have symmetrical names, like with suffix “.R”/ “.L” or “_R” / “_L”. If a group has no mirrored counterpart, it will paint symmetrically on the active group itself. You can read more about the naming convention in Editing Armatures: Naming conventions. The conventions for armatures/bones apply here as well.

Mirror the brush strokes across the selected local axes. Note that if you want to alter the directions the axes point in, you must rotate the model in Edit Mode and not in Object Mode.

These settings allow for radial symmetry in the desired axes. The number determines how many times the stroke will be repeated within 360 degrees around the central axes.

Use topology-based mirroring, for when both sides of a mesh have matching mirrored topology. See here for more information.

---

## Symmetry¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tool_settings/symmetry.html

**Contents:**
- Symmetry¶

Toolbar ‣ Tool ‣ Symmetry

Mirror the brush strokes across the selected local axes. Note that if you want to alter the directions the axes point in, you must rotate the model in Edit Mode and not in Object Mode.

These three buttons allow you to block any modification/deformation of your model along selected local axes, while you are sculpting it.

Using this option allows you to seamlessly tile your strokes along the given axes. This allows to create repeating patterns.

Reduces the strength of the stroke where it overlaps the planes of symmetry.

These settings allow for radial symmetry in the desired axes. The number determines how many times the stroke will be repeated within 360 degrees around the central axes.

The offset allows the option to alter the tile size along all three axes. The default tile size is set to one unit.

Determines which direction the model will be symmetrized.

A parameter of the Symmetrize operator to control the distance within which symmetrical vertices are merged.

Uses direction orientation to symmetrize. Since Dyntopo adds details dynamically it may happen that the model becomes asymmetric, so this a good tool for that.

---

## Symmetry¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/vertex_paint/tool_settings/symmetry.html

**Contents:**
- Symmetry¶

Toolbar ‣ Tool ‣ Symmetry

Mirror the brush strokes across the selected local axes. Note that if you want to alter the directions the axes point in, you must rotate the model in Edit Mode and not in Object Mode.

---

## Thumb¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/brushes/thumb.html

**Contents:**
- Thumb¶
- Brush Settings¶
  - General¶

Sidebar ‣ Tool ‣ Brush Settings ‣ Advanced ‣ Brush Type

Similar to the Grab brush, but instead only moves the geometry along the surface (using the area plane). This is useful for grabbing surfaces with a very specific direction, or without making too impactful changes to the overall object shape.

More info at General brush settings and on Advanced brush settings.

---

## Tint Brush¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/brushes/tint.html

**Contents:**
- Tint Brush¶
- Brush Settings¶
- Usage¶
  - Selecting a Brush, Color & Mode¶
  - Painting¶

The Tint brush allows you to paint onto strokes point mixing the material base color with a selected color.

Defines how Color Attributes affect to the strokes.

Color Attributes affects both the Stroke and Fill materials.

Color Attributes affects the Stroke material only.

Color Attributes affects the Fill material only.

In the Tool Settings select the brush, color and mode to use with the tool.

You can configure the brush main settings included in the Tool Settings for convenience. For the vertex paint brushes configuration and settings see Vertex Paint Brush.

Ctrl-LMB erase the Color Attribute.

Click and hold LMB or use the pen tip to paint onto the stroke points.

---

## Toolbar¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/toolbar.html

**Contents:**
- Toolbar¶
- Sculpting Tools¶
- Gesture Tools¶
- Filter Tools¶
- Single Click Tools¶
- General Tools¶

The amount of tools in sculpt mode is very extensive. This is an overview of all of them, categorized by their general functions.

Tool to use for any of the Sculpt mode brushes.

General gesture tools to apply an operation via box, lasso, line and polyline shapes. See Gesture Tools for more information.

Create a mask via a gesture.

Hides/Shows geometry via a gesture.

Create a face set via a gesture.

Perform a Boolean operation via a gesture.

Flatten the geometry towards a drawn line.

Tools for applying effects on the entire unmasked and visible mesh.

Apply a deformation to all unmasked vertices.

Applies a cloth simulation to all unmasked vertices.

Changes the active color attribute on all unmasked vertices.

Simpler tools that apply an operation on surfaces that are clicked on.

Modifies the face set under the cursor.

Create a mask from any color from the color attribute by clicking on it.

General transform and annotate tools like in other modes.

Adjust the objects translation, rotations and scale.

Draw free-hand annotation.

Draw straight line annotation.

Draw a polygon annotation.

Erase previous drawn annotations.

---

## Toolbar¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/toolbar/index.html

**Contents:**
- Toolbar¶
- Object Mode¶
- Edit Mode¶
- Paint Modes¶
- Grease Pencil¶

The Toolbar contains a list of tools. Links to each mode’s Toolbar are listed below.

Grease Pencil Sculpting

Grease Pencil Weight Paint

---

## Using Vertex Groups¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/weight_paint/usage.html

**Contents:**
- Using Vertex Groups¶
- Vertex Groups for Bones¶
- Vertex Groups for Particles¶

This is one of the main uses of weight painting. While you can have Blender generate the weights automatically (see the skinning section), you may want to tweak them or even create them from scratch, especially around joints.

The process is as follows:

Select the armature and bring it into Pose Mode by pressing Ctrl-Tab.

Make sure that Edit ‣ Lock Object Modes is unchecked in the topbar.

Select the mesh and bring it into Weight Paint Mode.

Make sure that Bone Selection is checked in the 3D Viewport’s header.

Select a bone using Alt-LMB (or Shift-Ctrl-LMB). This will activate the bone’s vertex group and display its current weights on the mesh.

Paint weights for the bone using LMB.

You can only select one bone at a time in this mode.

The bones are likely embedded inside the mesh, making them invisible and unselectable. To get around this, you can enable In Front for the armature.

If a bone doesn’t have a vertex group yet when you start painting, Blender will create one automatically.

If you have a symmetrical mesh and a symmetrical armature, you can use Mirror Vertex Groups to automatically create vertex groups and weights for the other side.

Weight painted particle emission.¶

By selecting vertex groups in the Vertex Groups panel of a particle system’s properties, you can have different particle densities, hair lengths etc. across different areas of the mesh.

---

## Vertex Paint Brushes¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/vertex_paint/brushes.html

**Contents:**
- Vertex Paint Brushes¶

Brushes for Grease Pencil Vertex Paint mode bundled in the Essentials library.

Paints a specified color over the object.

Smooths out the colors of adjacent vertices. In this mode the Color Value is ignored. The strength defines how much the colors are blurred.

Smooths color by painting the average resulting color from all colors under the brush.

Smudges colors by grabbing the colors under the brush and “dragging” them. This can be imagined as a finger painting tool.

Change the color only to the stroke points that already have a color applied.

---

## Weights Menu¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/weight_paint/weights_menu.html

**Contents:**
- Weights Menu¶
- Normalize All¶
- Normalize¶
- Invert¶
- Smooth¶
- Sample Weight¶

This page covers many of the tools in the Weights menu.

Weights ‣ Normalize All

For each point, this tool makes sure that the sum of the weights across all vertex groups is equal to 1. It normalizes all of the vertex groups, except for locked groups, which keep their weight values untouched.

Keep the values of the active group while normalizing all the others.

This tool only works on the active vertex group. All points keep their relative weights, but the entire set of weights is scaled up such that the highest weight value is 1.0.

Replaces each weight of the selected vertex group by × -1.0 weight.

Original 1.0 converts to 0.0

Original 0.5 remains 0.5

Original 0.0 converts to 1.0

Smooths the weights of the active vertex group.

Weights ‣ Sample Weight

Adjust the Weight of the Draw tool to the weight of the vertex under the mouse cursor.

---

## Weight Paint Brushes¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/weight_paint/brushes.html

**Contents:**
- Weight Paint Brushes¶

Brushes for Grease Pencil Weight Paint mode bundled in the Essentials library.

Paints a specified weight over the strokes.

Smooths out the weighting of adjacent points. In this mode the Weight Value is ignored. The strength defines how much the smoothing is applied.

Smooths weights by painting the average resulting weight from all weights under the brush.

Smudges weights by grabbing the weights under the brush and “dragging” them. This can be imagined as a finger painting tool.

---
