# Blender - Shading

**Pages:** 2

---

## Shader Editor¶

**URL:** https://docs.blender.org/manual/en/latest/editors/shader_editor.html

**Contents:**
- Shader Editor¶
- Header¶
- Sidebar¶
  - Options¶

The Shader Editor is used to edit materials which are used for rendering. Materials used by Cycles and EEVEE are defined using a node tree. Therefore, the main window of the Shader editor is a node editor.

Shader Editor with the default material node tree.¶

A list of all shader nodes is available in the rendering section.

The type of data whose shader nodes are being edited:

Edit shader nodes for the active object’s Material.

Edit shader nodes for the World background.

Edit shader nodes for Freestyle Line Styles

Use shader nodes to define the texture for the freestyle line style.

The Slot menu can be used to select the active material slot on the active object. The material selector to the right of it can change the material that is in the selected slot.

Keeps the current material selection visible in the Shader editor even when another object or material is selected elsewhere.

The Options panel in the Sidebar region contains the same settings that are also available in the Material tab in the Properties. They differ depending on the selected render engine. The settings are duplicated to make it possible to edit the entire material from the Shader editor.

---

## Viewport Shading¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/display/shading.html

**Contents:**
- Viewport Shading¶
- – Wireframe¶
  - Options¶
- – Solid¶
  - Options¶
    - Cavity¶
- – Material Preview¶
  - Lighting¶
- – Rendered¶

Header ‣ Viewport Shading

Blender offers different shading modes for helping with different tasks. For example, Solid shading is well-suited for modeling, while Rendered is useful for setting up lighting.

The radio buttons let you change the shading mode, while the drop-down button opens a popover with additional options described below.

Pressing Z opens a pie menu for changing the shading mode. Pressing Shift-Z switches between the current shading mode and Wireframe.

Only displays the edges (wireframes) of the objects in the scene.

How wireframes are colored. This affects the Wireframe shading mode and overlay.

Use the Active Object, Wire, or Wire Edit theme color based on the object’s current state.

Use the color from the object’s Viewport Display settings.

Each object gets displayed in a random color.

How the background is displayed in the 3D Viewport.

Use the background of the theme. This can be configured in the Themes Preferences under 3D Viewport ‣ Theme Space ‣ Gradient Colors.

Use the color from the World’s Viewport Display options.

Select a custom color for the background of the 3D Viewport.

Make objects transparent, allowing you to see and select items that would otherwise be occluded. The slider controls object opacity.

Draw an outline around objects. The color of the outline can be adjusted.

This mode utilizes the Workbench Render Engine to render the 3D Viewport. It shows solid geometry but uses simplified shading and lighting without the use of shader nodes. Solid mode is good for modeling and sculpting, and is really useful with the multitude of options to emphasize certain geometric features.

How lights are computed.

Do not calculate any lighting. The base color of the scene will be rendered.

Use studio lights to light the objects. The studio lights can be configured in the preferences. Studio lights can follow the camera or be fixed. When fixed the angle of the lights can be adjusted.

Uses world space lighting so lights do not follow the view camera.

The rotation of the studio lights on the Z axis.

Use a material capture to light the objects in the scene. MatCaps can be flipped horizontally by clicking the Flip MatCap button.

Custom MatCaps can be loaded in the preferences.

The source to compute the color for objects in the viewport.

Use the color that can be set per material in the Viewport Display Material panel.

Use the color that can be set per object in the Viewport Display Object panel.

A random color will be selected for every object in the scene.

Display the active Color Attribute of an object. When an object has no active Color Attribute it will be rendered in the color set in the Viewport Display Object panel.

Show the texture from the active image texture node using the active UV map coordinates When an object has no active texture the object will be rendered with the settings in the Viewport Display Material panel.

Render the whole scene using a single color. The color can be chosen.

How the background is displayed in the 3D Viewport.

Use the background of the theme. This can be configured in the Themes Preferences under 3D Viewport ‣ Theme Space ‣ Gradient Colors.

Use the color from the World’s Viewport Display options.

Select a custom color for the background of the 3D Viewport.

Use backface culling to hide backsides of faces.

Render the outline of objects in the viewport. The color of the outline can be adjusted.

Render specular highlights.

Only available when Lighting is set to Studio lighting or when a MatCap has been selected that contains a specular pass.

Render the scene transparent. With the slider you can control how transparent the scene should appear.

Renders a sharp shadow in the scene.

Defines how dark the shadow should be rendered. This slider can be adjusted between 0 (shadow not visible) and 1 (shadow is black).

Controls the direction of the light source that casts the shadows.

Controls the Shadow termination angle. It can be used to limit self shadowing artifacts.

Controls the falloff near the edge of the shadow.

Use the Depth of Field settings of the active camera in the viewport. Only visible when looking through the camera.

The settings are located on Properties ‣ Camera ‣ Depth of Field panel.

Highlight ridges and valleys in the scene geometry.

Method how to calculate the cavity.

More precise but is slower to calculate.

Fast but does not take the size of the ridges and valleys into account.

Both will use both methods.

Control the visibility of ridges.

Control the visibility of valleys.

Render the 3D Viewport with EEVEE and an HDRI environment. This mode is particularly suited for previewing materials and painting textures. You can select different lighting conditions to test your materials.

The Material Preview shading mode is not available when the scene’s render engine is set to Workbench.

Use the lights in the scene. When disabled (or when the scene contains no lights), a virtual light is used instead.

Use the World of the scene. When disabled, a world will be constructed with the following options:

The environment map used to light the scene.

The rotation of the environment on the Z axis.

Makes the lighting rotation fixed and not follow the camera.

Light intensity of the environment.

Opacity of the HDRI as a background image in the viewport.

Factor to unfocus the HDRI. Note that this does not change the diffusion of the lighting, only the appearance of the background.

Instead of the combined render, show a specific render pass. Useful to analyze and debug geometry, materials and lighting.

When to preview the result of compositing in the 3D Viewport.

Never show the compositing output.

Only show the compositing output when in Camera View, which gives the best vantage point for previewing the final result.

Always show the compositing output.

Render the 3D Viewport using the scene’s Render Engine, for interactive rendering. This gives a preview of the final result before compositing, including scene lighting effects.

The options are the same as for Material Preview, except that the Render Pass selector will offer different passes if the scene uses the Cycles render engine.

---
