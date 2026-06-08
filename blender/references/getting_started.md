# Blender - Getting Started

**Pages:** 97

---

## About Blender¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/about/index.html

**Contents:**
- About Blender¶
- Who uses Blender?¶
- Key Features¶
- Further Reading¶

Blender is the free and open-source 3D creation suite. It supports the entirety of the 3D pipeline: modeling, rigging, animation, simulation, rendering, compositing, motion tracking and video editing.

Blender provides a consistent experience across Linux, macOS, and Windows operating systems via OpenGL.

Blender has a wide variety of tools making it suitable for almost any sort of media production. Professionals, hobbyists, and studios around the world use it for creating animations, game assets, motion graphics, TV shows, concept art, story-boarding, commercials, and feature films.

Check out the User Stories page on the Blender website for more examples.

Blender is a fully integrated 3D content creation suite, offering a broad range of essential tools, including Modeling, Rendering, Animation & Rigging, Video Editing, VFX, Compositing, Texturing, and many types of Simulations.

It is cross platform, with an OpenGL GUI that is uniform on all major platforms (and customizable with Python scripts).

It has a high-quality 3D architecture, enabling fast and efficient creation workflow.

It boasts active community support. See blender.org/community for an extensive list of sites.

It can be installed into and run from any directory without modifying the system.

You can download the latest version of Blender here.

A rendered image being post-processed.¶

Blender makes it possible to perform a wide range of tasks, and it may seem daunting when first trying to grasp the basics. However, with a bit of motivation and the right learning material, it is possible to familiarize yourself with Blender after a few hours of practice.

This manual is a good start, though it serves more as a reference. There are also many online video tutorials from specialized websites.

Despite everything Blender can do, it remains a tool. Great artists do not create masterpieces by pressing buttons or manipulating brushes, but by learning and practicing subjects such as human anatomy, composition, lighting, animation principles, etc.

3D creation software such as Blender have an added technical complexity and jargon associated with the underlying technologies. Terms like UV maps, materials, shaders, meshes, and “subdivs” are the media of the digital artist, and understanding them, even broadly, will help you to use Blender to its best.

So keep reading this manual, learn the great tool that Blender is, and keep your mind open to other artistic and technological areas – and you, too, can become a great artist.

---

## About Free Software and the GPL¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/about/license.html

**Contents:**
- About Free Software and the GPL¶

When one hears about “free software”, the first thing that comes to mind might be “no cost”. While this is often true, the term “free software” as used by the Free Software Foundation (originators of the GNU Project and creators of the GNU General Public License) is intended to mean “free as in freedom” rather than in the sense of “no cost” (which is usually referred to as “free as in free beer” or gratis). Free software in this sense is software which you are free to use, copy, modify, redistribute, with no limit. Contrast this with the licensing of most commercial software packages, where you are allowed to load the software on a single computer, are allowed to make no copies, and never see the source code. Free software allows incredible freedom to the end user. Since the source code is universally available, there are also many more chances for bugs to be caught and fixed.

When a program is licensed under the GNU General Public License (the GPL):

You have the right to use the program for any purpose.

You have the right to modify the program and have access to the source codes.

You have the right to copy and distribute the program.

You have the right to improve the program, and release your own versions.

In return for these rights, you have some responsibilities if you distribute a GPL’d program. These responsibilities are designed to protect your freedoms and the freedoms of others:

You must provide a copy of the GPL with the program, so that recipients are aware of their rights under the license.

You must include the source code or make the source code freely available.

If you modify the code and distribute the modified version, you must license your modifications available under the GPL (or a compatible license).

You may not restrict the licensing of the program beyond the terms of the GPL (you may not turn a GPL’d program into a proprietary product).

For more on the GPL, check its page on the GNU Project website.

The GPL only applies to the Blender application and not the artwork you create with it; for more info see the Blender License.

---

## Adaptive Resolution¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/introduction/adaptive.html

**Contents:**
- Adaptive Resolution¶
- Voxel Remesher¶
- Dyntopo¶
- Multiresolution¶

In order for sculpting to give accurate and predictable results, Blender needs enough geometry. Instead of starting out with a highly subdivided mesh, add geometry dynamically by using either of the following adaptive sculpting methods.

“Voxel remeshing” rebuilds the geometry with a perfectly even distributed topology. Depending on the set voxel size, this will lead to a lower or higher resolution.

This technique is especially useful to block out the initial shape of an object. It also has the advantage of removing any overlapping geometry and creating a manifold volume as a result.

Any currently used mask, face sets and color attributes will be re-projected on the remeshed result. Reaching high vertex counts should still be achievable with this technique, depending on the used hardware.

This technique will not work on objects that do not have an enclosed volume. Make sure to fill any holes in the mesh before remeshing. Or avoid any holes in the mesh/volume that are larger than the defined voxel size.

If in doubt, you can fill all holes in edit mode or by using the Mask Slice and Fill Holes operation to fill all holes in the mesh. If nothing is masked, it only fills any holes.

To more easily access this feature, use the shortcuts R to define the resolution, and Ctrl-R to execute the remeshing.

More information at Remesh.

Dynamic topology (aka Dyntopo) is a dynamic tessellation sculpting method that automatically adds and removes topology under the brush.

Unlike the Voxel Remesher, this makes it possible to sculpt complex shapes without thinking about the resolution or topology. It also allows to define a different resolution wherever necessary. Much more complex base mesh sculpting is especially useful with this technique.

The disadvantages of this technique are a slower performance and limited support for some sculpt mode features. Custom attributes like Color Attributes, UV Maps and Face Sets are also lost or corrupted when using Dyntopo.

This feature shares the same shortcuts with voxel remeshing when enabled. Use R to define the resolution and Ctrl-R to flood fill the resolution (if Constant Detail is used).

Because Dyntopo and the Voxel Remesher are mutually exclusive and cannot be used at the same time, both use the same shortcut to define the remeshing resolution.

Brushes like Density, Snake Hook and Clay Strips work especially well with this feature.

More information at Dyntopo.

The Multiresolution Modifier can be used for subdivision based sculpting. This means the object will be subdivided, similar to the Subdivision Surface Modifier, only that the subdivisions can be freely sculpted for very high resolution detailing.

For this technique it is highly recommended to use on a clean topology base mesh. This means the base mesh should be only made of quads and avoid non-manifold faces, as well as poles with two connected edges. More information at Quad Remeshing for an automatic retopology method.

This technique has the advantage of sculpting with multiple resolutions, meaning you have the ability to sculpt on any level of subdivision. This allows to add a much higher resolution of details for rendering and sculpting, while displaying lower resolutions for better viewport performance. It also allows sculpting on lower resolutions any time for broader changes.

As an example, you can sculpt general proportions in subdivision level 1, add high resolution details in level 4 and switch back to subdivision 1 to correct the shape further.

The disadvantages are that you may end up with some mesh distortions because the topology is not dynamic like voxel remeshing and dyntopo. The topology should also not be changed once already subdivided, since any edits to the base mesh will result in corrupted subdivision details.

Pay attention to the topology that you sculpt and how much it gets stretched. If more resolution is needed you can always subdivide another time, but there will be worse performance and slower level switching once more than 5 subdivisions are used. Alternatively use the Slide Relax brush to slide topology to where it is needed.

Additional brushes like the Multires Eraser and Multires Smear are recommended for adjustments.

Here are general shortcuts to use the feature.

Step up one multires level Alt-2

Step down one multires level Alt-1

Set multires level / Create multires modifier Ctrl-0 to Ctrl-5

More information at Multiresolution Modifier.

---

## Blender’s History¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/about/history.html

**Contents:**
- Blender’s History¶
- The Beginning¶
- Blender Goes Open Source¶
- Blender Makes Open Movies¶
- Blender Landmarks¶
- Blender: Present And Future¶
- Version/Revision Milestones¶

Blender was created by Ton Roosendaal, a Dutch art director and self-taught software developer. Attracted to all things technical and creative, Roosendaal began a degree in Industrial Design, but dropped out in order to start his own 3D animation studio, NeoGeo, in 1989 (the video game console of the same name appeared a year later). Initially based in Roosendaal’s attic, NeoGeo grew rapidly, garnering awards and becoming the biggest company of its type in the Netherlands.

Roosendaal wrote the first source files titled “Blender” on the 2nd of January, 1994, still considered Blender’s official birthday. Originally, Blender was planned as an in-house application for NeoGeo; it grew from a series of pre-existing tools, including a ray-tracer built for the Amiga. This early version of Blender was intended to address a perennial frustration among creatives: when a difficult client requires multiple changes to a project, how do you implement those changes painlessly? Thanks to its highly configurable approach, Blender aimed at providing an answer. (As an aside: the name refers to a song by a Swiss electronic band, Yello).

Roosendaal invested his savings in a Silicon Graphics workstation. Costing the equivalent of thirty thousand US dollars, this computer led to Blender 1.0. Launched in January 1995, this first iteration of Blender proper incorporated then innovative ideas, including a single window which could be subdivided as the user saw fit.

At the time, 3D was considered commercially uninteresting. However, Roosendaal had fallen in love with what he describes as its “magical ability to create a whole world in a computer.” So when NeoGeo closed, he and partner Frank van Beek founded a new company focused on further developing and marketing Blender. Not a Number (NaN) opened its doors in June 1998, distributing Blender under a freemium pricing strategy: the software was free to download, with NaN selling keys to unlock more advanced features.

Thanks to this business model, NaN was able to fund a booth at a renowned computer graphics conference in Los Angeles, SIGGRAPH (Special Interest Group on Computer Graphics and Interactive Techniques). As a consequence, Blender attracted two rounds of funding totaling some five and a half million US dollars. Despite this investment, a harsh economic climate, excess spending, and troubled relations between NaN and its investors meant that the company closed in early 2002.

With NaN’s demise, Blender’s development ceased. Unable to buy the rights from NaN’s backers, Roosendaal opted for a novel plan. In May of 2002, he started a non-profit, the Blender Foundation, with the intention of making Blender open-source. His hope was to create a public monument to Blender, and give everyone who had worked on the Blender project the chance to use it for their portfolios. In July of the same year, he launched the first-ever crowdfunding campaign: Free Blender. Thanks to Blender’s community of 250,000 users, the Blender Foundation was able to raise one hundred and ten thousand euros in just seven weeks — sufficient to regain Blender from its investors.

On Sunday, October 13th, 2002, Blender was released under the terms of the GNU General Public License, the strictest possible open-source contract. Not only would Blender be free, but its source code would remain free, forever, to be used for any purpose whatsoever.

The success of Free Blender cleared the way for a style of development that has become Blender’s defining strength. While Blender’s evolution is partly driven by grant-funded developers and guided by a core team at the Blender Foundation, Amsterdam, its greatest advantage is a global community of dedicated volunteers. Thanks to their efforts, Blender is able to iterate rapidly and respond to the needs of artists and makers. Such nimbleness and creativity would be much harder within the confines of a traditional business model.

As a way to stress-test Blender’s increasing power, the Blender Foundation challenged its community’s most talented artists to make an animated 3D short film. The only criterion was that they had to use open source tools, with Blender prime among them.

Under the codename “Project Orange,” this project began in 2005, resulting in Elephants Dream, a surreal adventure through a gigantic machine. The film and all its assets were made freely available under a Creative Commons license.

After the success of Elephants Dream, the Blender Institute was established in the summer of 2007. As well as helping to define the Blender Foundation’s goals, the Blender Institute comprised a permanent office and studio, with the express intention of generating Open Projects related to 3D movies, games or visual effects. As part of its output, the Blender Institute has created a series of Open Movies in collaboration with leading artists. They include the comedy Big Buck Bunny (2008), science fiction thriller Tears of Steel (2012), a poetic fantasy Spring (2019), and horror-comedy Sprite Fright (2021).

Each Open Project places new demands on Blender as a 3D creation suite, which in turn leads to further upgrades. While a complete list of updates is beyond the scope of this article, some milestones are worth noting.

Early 2008 saw the start of the Blender 2.5 project. This combined a major User Interface overhaul, with new tool definitions, a data access system, event handling, and a new animation system. For 2.5, the primary goal was to bring the interface standards and input methods up to date.

Cycles is Blender’s production-capable path-tracing render engine, first incorporated into release 2.61, back in 2011. Over the years, Cycles has introduced support for a wide range of rendering possibilities, including AMD and NVIDIA. Similarly, it’s grown to include support for many features including hair, motion blur, smoke and fire, major shaders and materials, adaptive subdivisions, and much more.

With its watershed 2.8 release in July, 2019, Blender broke into the 3D mainstream. Starting with a drastically revamped User Interface, the 2.8 series included a multitude of innovations, from EEVEE (a real-time render engine), to new remeshing options for sculptors, to the integration of Mantaflow, to a fully functioning 2D animation workspace that also offered the possibility of a 2D/3D hybrid workflow.

Although industry recognition for Blender had grown over the decades, 2.8 marked the moment when it was widely accepted as a legitimate alternative to paid competitors. As well as using Blender in their own projects, some of the world’s largest and most recognized companies became regular contributors to the Blender Development Fund, ensuring that Blender can continue to innovate.

As well as Blender and Open Projects made with Blender, there’s Blender Cloud. This subscription-based Open Production platform provides rolling updates on current Open Movie projects, as well as an archive of film assets in .blend file form, animation and shot breakdowns, shaders and textures, and comprehensive training videos from professional artists and developers, often those employed at Blender HQ in Amsterdam.

In total, the Blender organization numbers some twenty-eight employees, working from Amsterdam, remotely, and on a grant basis. For Blender, this team represents only a small part of a much wider community, which it defines as everyone who contributes to Blender’s development, earns their living from Blender, or simply downloads it.

The Blender mission can be summed up as “get the world’s best 3d technology in the hands of artists as open-source, and make amazing things with it.”

Going forward, Blender hopes to become a sustainable, future proof organization, dedicated to furthering its open-source philosophy, its values of curiosity and innovation, a commitment to technical excellence, and increasingly ambitious creative goals.

1.00 – January 1994: Blender in development at animation studio NeoGeo.

1.23 – January 1998: SGI version published on the web, IrisGL.

1.30 – April 1998: Linux and FreeBSD version, port to OpenGL and X11.

1.3x – June 1998: NaN founded.

1.4x – September 1998: Sun and Linux Alpha version released.

1.50 – November 1998: First Manual published.

1.60 – April 1999: C-key (new features behind a lock, $95), Windows version released.

1.6x – June 1999: BeOS and PPC version released.

1.80 – June 2000: End of C-key, Blender full freeware again.

2.00 – August 2000: Interactive 3D and real-time engine.

2.10 – December 2000: New engine, physics, and Python.

2.20 – August 2001: Character animation system.

2.21 – October 2001: Blender Publisher launch.

2.2x – December 2001: macOS version.

Blender goes Open Source

Blender goes Open Source, 1st Blender Conference.

Blender Publisher becomes freely available, and the experimental tree of Blender is created, a coder’s playground.

The first truly open source Blender release.

The second open source Blender release.

First of the 2.28x series.

Preview release of the 2.3x UI makeover presented at the 2nd Blender Conference.

Upgrade to stable 2.3x UI project.

A major overhaul of internal rendering capabilities.

Game Engine returns, ambient occlusion, new procedural textures.

Particle interactions, LSCM UV mapping, functional YafRay integration, weighted creases in subdivision surfaces, ramp shaders, full OSA, and many (many) more.

Another version full of improvements: object hooks, curve deforms and curve tapers, particle duplicators and much more.

A stabilization version, much work behind the scenes, normal and displacement mapping improvements.

Transformation tools and widgets, soft bodies, force fields, deflections, incremental subdivision surfaces, transparent shadows, and multi-threaded rendering.

Full rework of armature system, shape keys, fur with particles, fluids, and rigid bodies.

Lots of fixes, and some Game Engine features.

The nodes release, Array modifier, vector blur, new physics engine, rendering, lip sync, and many other features. This was the release following Project Orange.

Multiresolution meshes, multi-layer UV textures, multi-layer images and multi-pass rendering and baking, sculpting, retopology, multiple additional mattes, distort and filter nodes, modeling and animation improvements, better painting with multiple brushes, fluid particles, proxy objects, Sequencer rewrite, and post-production UV texturing.

The big news, in addition to two new modifiers and re-awakening the 64-bit OS support, was the addition of subsurface scattering, which simulates light scattering beneath the surface of organic and soft objects.

Serious bug fixes, with some performance issues addressed.

The Peach release was the result of a huge effort of over 70 developers providing enhancements to provide hair and fur, a new particle system, enhanced image browsing, cloth, a seamless and non-intrusive physics cache, rendering improvements in reflections, AO, and render baking, a Mesh Deform modifier for muscles and such, better animation support via armature tools and drawing, skinning, constraints and a colorful Action Editor, and much more. It contained the results of Project Peach.

The Apricot release, cool GLSL shaders, lights and GE improvements, snap, sky simulator, Shrinkwrap modifier, and Python editing improvements. This contained the results of Project Apricot.

Node-based textures, armature sketching (called Etch-a-Ton), Boolean mesh operation improvements, JPEG2000 support, projection painting for direct transfer of images to models, and a significant Python script catalog. GE enhancements included video textures, where you can play movies in-game, upgrades to the Bullet physics engine, dome (fisheye) rendering, and more API GE calls made available.

Blender 2.5x – The Recode!

This series released four pre-version (from Alpha 0 in November 2009 to Beta in July 2010) and three stable versions (from 2.57 - April 2011 to 2.59 - August 2011). It was one of the most important development projects, with a total refactor of the software with new functions, redesign of the internal window manager and event/tool/data handling system, and new Python API. The final version of this project was Blender 2.59 in August 2011.

Blender 2.6x to 2.7x – Improvements & Stabilizing

Internationalization of the UI, improvements in the animation system and the GE, vertex weight groups modifiers, 3D audio and video, and bug fixes.

The Cycles renderer was added to the trunk, the camera tracker was added, dynamic paint for modifying textures with mesh contact/approximation, the Ocean modifier to simulate ocean and foam, new add-ons, bug fixes, and more extensions added for the Python API.

The Carve library was added to improve Boolean operations, support for object tracking was added, the Remesh modifier was added, many improvements in the GE, matrices and vectors in the Python API were improved, plus new add-ons, and many bug fixes.

Bmesh was merged with the trunk, with full support for n-sided polygons, sculpt hiding, a panoramic camera for Cycles, mirror ball environment textures and float precision textures, render layer mask layers, ambient occlusion and viewport display of background images and render layers. New import and export add-ons were added, and 150 bug fixes.

A mask editor was added, along with an improved motion tracker, OpenColorIO, Cycles improvements, Sequencer improvements, better mesh tools (Inset and Bevel were improved), new keying nodes, sculpt masking, COLLADA improvements, a new Skin modifier, a new compositing nodes backend, and the fixing of many bugs.

Fire and smoke improvements, anisotropic shader for Cycles, modifier improvements, the Bevel tool now includes rounding, new add-ons, and over 200 bug fixes.

Dynamic topology, rigid body simulation, improvements in UI and usability (including retina display support), Cycles now supports hair, the Bevel tool now supports individual vertex beveling, new Mesh Cache modifier and the new UV Warp modifier, new SPH particle fluid solver. More than 250 bug fixes.

Freestyle was added, paint system improvements, subsurface scattering for Cycles, Ceres library in the motion tracker, new custom Python nodes, new mesh modeling tools, better support for UTF-8 text and improvements in Text editors, new add-ons for 3D printing, over 260 bug fixes.

New and improved modeling tools, three new Cycles nodes, big improvements in the motion tracker, Python scripts and drivers are disabled by default when loading files for security reasons, and over 280 bug fixes.

Even more modeling tools, Cycles improved in many areas, plane tracking is added to the motion tracker, better support for FBX import/export, and over 270 bugs fixed.

Cycles gets basic volumetric support on the CPU, more improvements to the motion tracker, two new modeling modifiers, some UI consistency improvements, and more than 560 bug fixes.

Deformation motion blur and fire/smoke support is added to Cycles, UI pop-ups are now draggable. There are performance optimizations for sculpting mode, new interpolation types for animation, many improvements to the GE, and over 400 bug fixes.

Cycles gets volume and SSS support on the GPU, pie menus are added and tooltips greatly improved, the Intersection modeling tool is added, new Sun Beam node for the Compositor, Freestyle now works with Cycles, texture painting workflow is improved, and more than 220 bug fixes.

Cycles gets improved volumetric support, major upgrade to Grease Pencil, Windows gets Input Method Editors (IMEs) and general improvements to painting, Freestyle, Sequencer and add-ons.

Support for custom normals, viewport compositing and improvements to hair dynamics.

Integrated stereo/multi-view pipeline, Smooth Corrective modifier and new developmental dependency graph.

Pixar OpenSubdiv support, Viewport and File Browser performance boost, node auto-offset, and a text effect strip for the Sequencer.

OpenVDB support for caching of smoke/volumetric simulations, improved Cycles subsurface scattering, Grease Pencil stroke sculpting and improved workflow, and reworked library handling to manage missing and deleted data-blocks.

Cycles support for spherical stereo images for VR, Grease Pencil works more similar to other 2D drawing software, Alembic import and export support, and improvements to Bendy Bones for easier and simpler rigging.

New Cycles features: Denoising, Shadow catcher, and new Principled shader. Other improvements were made to Grease Pencil and Alembic. Support was also added for application templates.

Blender 2.8 – Revamped UI

A totally redesigned UI for easier navigation; improved viewport, gizmos, and tools. With EEVEE a new physically based real-time render engine was created. The Grease Pencil got a big overhaul and is now a full 2D drawing and animation system. Replacing the old layers, collections are a powerful way to organize objects. Other improvements: Cycles, Modeling, Animation, Import/Export, Dependency Graph.

Revamped sculpting tools, Cycles OptiX accelerated rendering, denoising, many EEVEE improvements, library overrides, UI improvements and much more.

UDIM and USD support, Mantaflow for fluids and smoke simulation, AI denoising, Grease Pencil improvements, and much more.

3D Viewport virtual reality scene inspection, new volume object type, Cycles adaptive sampling, Cycles viewport denoising, sculpting improvements, and much more. First LTS release intended to support studio and long lifecycle project use.

Blender 2.9 – Refining 2.8

Improved sky texture, EEVEE motion blur, sculpting improvements, revamped modifier UI, improved modeling tools, and faster motion blur in Cycles.

Outliner improvements, property search, improved mesh Boolean operations, animation curves, volume object and display improvements, and more refined sculpting tools.

Geometry nodes, primitive add tool, sculpting improvements, Grease Pencil curve editing, Cycles Color Attribute baking, APIC fluid simulations, Video Sequencer improvements, and much more.

New geometry nodes, sculpting improvements, Grease Pencil Line Art modifier along with other improvements, an improved DOF for the EEVEE render engine, redesigned Cryptomatte workflow, and more. LTS release for the 2.9 series.

Blender 3.0 – Optimizing Performance

Asset Browser added, Cycles X, EEVEE Attributes, New geometry nodes, animation update, Grease Pencil Line Art improvements, pose library, Open Image Denoising 2-8x faster, additional support for AMD on linux.

Major point clouds improvements, Cycles Apple Metal GPU support, Subdivision GPU support, image editor handles larger images, Major performance gains for geometry nodes, context aware search for geometry nodes.

Light groups for Cycles, true Shadow caustics, volume motion blur, GLTF improvements, AMD GPU Rendering on Linux, painting in sculpt mode, WEBp image support.

New hair object, procedural UV nodes, Line Art shadow and contour, Intel GPU rendering support via oneAPI, and improvements to library overrides. First LTS release of the 3.0 series.

Cycles path guiding, sculpting auto masking improvements, even more geometry nodes, UV Editing improvements and Wayland support on Linux.

New generative hair assets, vector displacement maps for sculpting, viewport compositor, and Cycle’s light trees.

Simulation nodes added to Geometry Nodes, Cycles hardware ray-tracing for AMD and Intel, UV island packing, asset bundle from Blender Studio and community artists included, new retopology overlay. Final LTS of the 3.0 series.

Blender 4.0 – A Major Leap For Rendering, Creating Tools, and More

A new Principled BSDF shader with coat and sheen layers, AgX view transform, Voronoi Texture fractal noise, light linking for selective lighting, run Geometry Nodes as Node Tools, snapping improvements including Snap Base, menu and modifier type-to-search, new Inter typeface, streamlined keymap, bone collections, Hydra Storm USD renderer, larger asset library, alignment to the VFX Reference Platform 2023.

Geometry Nodes baking support, Menu Switch node, OpenImageDenoise GPU acceleration, more realtime viewport compositor functions, simpler animation keyframe insertion, hierarchical bone collections, graph editor click-and-slide, video sequencer performance and color scope improvements, alignment to the VFX Reference Platform 2024, armature and shape key export to USD.

Next generation of EEVEE with major upgrades to lighting, sun lights, displacement, subsurface, volumetrics, and motion blur, Cycles gains Ray Portal BSDF and Thin-Film Interference, better soft volume rendering with reduced noise, blue noise-based sampling, Blender Extensions platform launched, Khronos PBR Neutral Tone Mapper, sculpting selection improvements, Node inputs support matrices, Node Tools can use mouse position and viewport, video sequencer graphical overhaul, additional USD export options, native portable installation support. First LTS of the 4.0 series.

Light linking and shadow linking in EEVEE, Metallic BSDF, Gabor noise texture, EEVEE render passes in the compositor, minimum stretch (SLIM) UV unwrapping, numerous Geometry Nodes updates including for…each zone, physics nodes, Grease Pencil engine rewritten for speed and features, over 100 default brushes now included for painting and sculpting, UI area docking.

---

## Cloth Sculpting¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/introduction/cloth_sculpting.html

**Contents:**
- Cloth Sculpting¶

Instead of sculpting cloth manually or creating complex physics simulation setups, there are various tools directly in sculpt mode that offer a simplified Cloth Physics Simulation.

This has various advantages but is especially useful for base mesh creation and larger clothing folds and draping. Detailing is possible, but the slower performance on high resolution meshes and simplified cloth physics might not lead to desirable results.

The resolution of the topology is mainly responsible for the size of the folds and detail level of the simulation. So an optimal and evenly distributed topology is important.

Many sculpting features are supported, so for example Masked vertices are pinned in the simulation. Another example is with auto-masked face set boundaries. The sculpt mode gravity factor is also applied on the cloth physics.

The main brushes and tools for this feature are the Cloth Brush and Cloth Filter, but other transform brushes like Pose and Boundary also support cloth sculpting in the brush settings.

A demo file for trying out the various brushes and tools is available here.

---

## Configuring Peripherals¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/configuration/hardware.html

**Contents:**
- Configuring Peripherals¶
- Displays¶
- Input Devices¶
  - Mouse¶
    - Mouse Button Emulation¶
  - Keyboard¶
    - Numpad Emulation¶
    - Non-English Keyboards¶
  - Touch Screens¶
  - Graphic Tablet¶

A full HD display (1920x1080) or higher is recommended. Multi-monitor setups are supported, and workspaces can be configured to span multiple monitors.

Example of Blender’s multi-monitor support.¶

Blender supports various types of input devices:

Keyboard (recommended: keyboard with numeric keypad, English layout works best)

Mouse (recommended: three button mouse with scroll wheel)

NDOF Device (also known as 3D Mouse)

If you don’t have a middle mouse button or numeric keypad, you can emulate these in the Input Preferences. However, be aware that these emulations may cause the loss of some shortcut keys. Where possible, it is suggested to use the recommended hardware.

A number of Blender interactions utilize the middle button (clicking the scroll wheel), or the use of the scroll wheel. This is why the recommendation for a mouse is a two-button mouse with an added scroll wheel that acts as a middle button (effectively a 3-button mouse). This will allow for the most efficient workflow within all of Blender’s modules.

If you do not have a 3 button mouse, you will need to emulate it by checking the option in the Preferences.

The following table shows the combinations used:

A number of Blender interactions utilize the keyboard’s number pad (or numpad). This is the set of 10 numeric keys plus mathematical functions that appears on the right side of a traditional 104-key full-sized keyboard. This will allow for the most efficient workflow within all of Blender’s modules.

If you do not have a number pad on the side of your keyboard, you may want to emulate one. You can then use the number row at the top of the keyboard instead, but will no longer have access to these keys’ original functions (such as switching between vertex/edge/face selection in Edit Mode).

Read more about Numpad Emulation in the Preferences.

If you use a keyboard with a non-English layout, you may still benefit from switching to the UK or US layout while working with Blender.

You can also change the keymap from the Preferences. However, this manual assumes you are using the default keymap.

Blender has several settings that can be enabled to improve the experience on touch-enabled devices. These options make it easier to manage areas, menus, and interactions without relying on precise mouse input.

Enable Show Handles to simplify resizing and rearranging Areas.

Increase the Border Width to make area edges easier to select with a finger.

Graphics tablets can be used to provide a more traditional method of controlling the mouse cursor using a pen. This can help provide a more familiar experience for artists who are used to painting and drawing with similar tools, as well as provide additional controls such as pressure sensitivity.

If you are using a graphic tablet instead of a mouse and pressure sensitivity does not work properly, try to place the mouse pointer in the Blender window and then disconnect/reconnect your graphic tablet. This might help.

Touchpad controls are available on Windows, macOS and Linux with Wayland. If you are working from a laptop without a mouse, you can emulate controls using multi-touch gestures with the trackpad from Preferences.

Hold the Shift key while dragging two fingers on the pad.

Hold the Ctrl or OSKey key while dragging two fingers on the pad.

Drag two fingers on the pad.

Tap two fingers on the pad.

3D mice or NDOF devices are hardware that you can use to navigate a scene in Blender. Currently only devices made by 3Dconnexion, such as the SpaceMouse™, are supported. These devices allow you to explore a scene, and make Fly/Walk Navigation easier to control. The NDOF device can be configured in the Preferences. These settings can also be accessed directly from the viewport using the NDOFMenu button on the NDOF device.

See Input Preference for more information on configuring peripherals.

HMDs make it possible to place users in an interactive, virtual environment. Attached to the head, they track head movements to project a seemingly surrounding world onto small screens in front of the user’s eyes. If the system works well, they experience the virtual environment as if they were really inside of it.

Virtual reality support in Blender is implemented through the multi-platform OpenXR standard. This standard is new and therefore support for it is still limited.

Not recommended for general use yet.

Meta (formerly Oculus) (Rift and Quest)

Requires Oculus v31 Software Update. Oculus Link required for Quest.

Requires SteamVR 1.16 or greater.

Windows Mixed Reality

Requires Windows 10 May 2019 Update (1903).

The following subsections describe how an HMD can be set up for usage with the supported platforms. If this is not done, Blender will report an error when trying to start a virtual reality session.

The dedicated platform for the HTC Vive Cosmos is currently targeted at developers and may lack features found in other platforms.

Follow the steps from the Vive Developer Forums.

Enable the VR Scene Inspection add-on in Blender.

The dedicated platform for the HTC Vive Focus 3 is currently targeted at developers and may lack features found in other platforms.

Follow the steps from the Vive Developer Forums.

Enable the VR Scene Inspection add-on in Blender.

Monado is a free and open source XR platform for Linux. It is not yet ready for production usage and should only be used for testing purposes.

Packages are available for the following distributions:

Debian (bullseye, sid)

For other systems, it has to be compiled from source, which in this case is not recommended for people with little experience in compiling software. Follow the Getting Started Guides from Monado to do so nevertheless.

Enable the VR Scene Inspection add-on in Blender.

Meta (formerly Oculus) provides full support for OpenXR as of the Oculus v31 Software Update.

Download and install the Oculus Rift/Oculus Link software.

Set Oculus as the active OpenXR runtime via the General tab in the Oculus App Settings.

Enable the VR Scene Inspection add-on in Blender.

Currently, passthrough support over OpenXR is disabled by default in the Quest Link app, and must be manually enabled in it’s settings to use this feature.

The performance of the passthrough render varies with the quality of the connection between the headset and the computer. For better results, connecting the headset directly through USB to the PC, or at least connecting the computer to the local network over Ethernet, is recommended.

SteamVR provides full support for OpenXR as of SteamVR 1.16.

Set SteamVR as the active OpenXR runtime via the Developer tab in the SteamVR Settings.

Enable the VR Scene Inspection add-on in Blender.

The SteamVR runtime can also be used for HTC Vive Cosmos, Oculus, and Windows Mixed Reality HMDs.

Varjo includes full OpenXR support with its required Varjo Base software.

Enable the VR Scene Inspection add-on in Blender.

Windows Mixed Reality provides full support for OpenXR. To check if a PC meets the requirements to run the software, Microsoft offers the Windows Mixed Reality PC Check application.

Make sure the Windows 10 May 2019 Update (1903) is installed.

If the system meets all requirements, the Mixed Reality Portal should already be installed. It is also available in the Microsoft Store.

Launch the Mixed Reality Portal. Click the menu button ... in the lower left corner. In the menu it opens, select the Set up OpenXR.

Enable the VR Scene Inspection add-on in Blender.

To switch to Windows Mixed Reality from another OpenXR runtime (e.g. SteamVR), download the OpenXR Developer Tools from the Microsoft Store and set Windows Mixed Reality as the active runtime.

---

## Defaults¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/configuration/defaults.html

**Contents:**
- Defaults¶
- Import Preferences From Previous Version¶
- Create New Preferences¶
- Saving Defaults¶
- Loading Factory Settings¶

When you start Blender for the first time or update to a new version, the interactive region of the Splash Screen is replaced with a few initial preferences to configure how you interact with Blender.

The initial preferences dialog.¶

These options can always be changed later in the Preferences.

Selecting this option will copy preferences from an older version of Blender. Doing so will copy preferences and startup files from the previous version of Blender and load them. This will include installed add-ons and extensions.

The preferences need to be imported from previous versions because the configuration files of each Blender version are stored in separate folders. Refer to the Blender’s Directory Layout page for the location of these folders.

If you would like to start fresh with the new version, continue to Create New Preferences.

Some previous Blender add-ons and extensions may not be compatible with a new version of Blender, and choosing this option may lead to errors on startup. If this occurs, the recommended first step is to try Loading Factory Settings.

The language used in the user interface. The list is broken up into categories determining how complete the translations are. More language preferences can be set in the Translation Preferences.

Choose between a light or dark theme for Blender. Themes can be customized more in the Preferences. Additional themes can be installed by visiting the Blender Extensions Platform. This is optional, and will require internet access.

Presets for the default keymap for Blender. Note that this manual assumes that you use the default “Blender” keymap.

This is the default keymap. Read more about this keymap here.

This keymap is intended to match an older series of Blender versions and is designed for people upgrading who do not want to learn the updated keymap.

This keymap is intended to match common commercial creation software and is intended for people who use many different such applications. Read more about this keymap here.

Controls which mouse button, either right or left, is used to select items in Blender. The default is for selection to use the left button.

Controls the action of Spacebar. These and other shortcuts can be modified in the keymap preferences.

Starts/stops animation playback. This option is good for animation or video editing work.

Opens the Toolbar underneath the cursor to quickly change the active tool. This option is good if doing a lot of modeling or rigging.

Opens up the Menu Search. This option is good for someone who is new to Blender and is unfamiliar with its menus and shortcuts.

Saves the preferences set above and opens the regular Splash Screen.

The preferences are automatically saved when changed. This behavior can be changed by following the instructions under Auto-Save Preferences

Changing the default startup file can be done via File ‣ Defaults ‣ Save Startup File. See Startup File.

There are two areas where Blender’s defaults are stored:

The Preferences file stores keymap, add-ons theme and other options.

The Startup File stores the scene and UI setup which are displayed at startup and when creating a new file (File ‣ New).

You can revert your customizations to Blender’s defaults:

The Preferences Load Factory Settings.

File ‣ Defaults ‣ Load Factory Settings.

After loading the factory settings, the preferences won’t be auto-saved.

See Managing Preferences for details.

---

## Filters¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/introduction/filters.html

**Contents:**
- Filters¶

Filters are tools which provide an alternative way of sculpting, because they do not rely on a brush radius. Instead they will affect any vertices that are visible and not masked.

The strength is controlled by click & dragging from left to right. The position of the cursor can be used to only affect specific areas, if auto-masking is used.

Many of the same brush types are also available as a filter type. This way much of the mesh can simultaneously be smoothed, colored or have some cloth simulation applied.

A common example for using the Mesh Filter is to smooth everything after increasing the resolution with the Voxel Remesher or Dyntopo.

More information at Mesh Filter, Cloth Filter, Color Filter and Mask Filters.

---

## General¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/introduction/general.html

**Contents:**
- General¶

Sculpt Mode is similar to Edit Mode in that it is used to alter the shape of a model, but Sculpt Mode uses a very different workflow: instead of dealing with individual elements (vertices, edges, and faces), an area of the model is primarily changed using brushes.

Sculpting Mode Example.¶

Sculpt Mode is accessed from the mode menu of the 3D Viewport header or with the pie menu via Ctrl-Tab. Once inside Sculpt Mode, the Toolbar and Tool Settings of the 3D Viewport will change to Sculpt Mode specific panels. The cursor will change to a circle, to indicate the size of the brush.

To have predictable brush behavior, make sure to apply the scale of your mesh.

The following pages will briefly explain the fundamental features and concepts of Sculpt Mode, including various links to other pages for more details.

---

## Gesture Tools¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/introduction/gesture_tools.html

**Contents:**
- Gesture Tools¶
- Box Gestures¶
  - Controls¶
- Lasso Gestures¶
  - Controls¶
  - Tool Settings¶
- Line Gestures¶
  - Controls¶
  - Tool Settings¶
- Polyline Gestures¶

Separate from brushes and filters, Sculpt mode also has a set of tools that perform actions to a drawn selection area. These tools are similar to the selection tools (e.g. box selection and lasso selection in other areas of Blender).

These tools do not provide a selection of elements that are then modified, they directly modify the underlying mesh.

Dragging creates a rectangular area defined by where LMB was pressed and where LMB is released.

Hold to reposition the selection area.

Dragging creates a freeform area that follows the cursor defined by where LMB was pressed and where LMB is released.

Hold to reposition the selection area.

Helps to reduce jitter of the strokes while drawing by delaying and correcting the location of points.

Minimum distance from the last point before the stroke continues.

A smooth factor, where higher values result in smoother strokes but the drawing sensation feels as if you were pulling the stroke.

Dragging creates a line. The resulting action acts upon everything on the highlighted side of the line. The area acted upon is extended in both directions of the viewport.

Toggles the side of the line that the tool affects.

Hold to constrain the rotation of the line to user-specified intervals. Defaults to 5 degree increments, customizable via the Snapping menu indicated by the magnet icon in the header.

Hold to reposition the line.

The affected area will not extend the length of the drawn line. This helps defining a smaller area instead of extending the line infinitely long.

Clicking places a point in the viewport. Each time LMB is pressed, a new point of the polygon is created. Pressing LMB on the starting point, pressing LMB twice, or pressing Return closes the selection area.

Hold to reposition the selection area.

---

## Help System¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/help.html

**Contents:**
- Help System¶
- Tooltips¶
  - Elements¶
- Context-Sensitive Manual Access¶
- Help Menu¶
  - Web Links¶
  - Save System Info¶

Blender has a range of built-in and web-based help options.

Tooltip of the Renderer selector in the Info Editor.¶

After hovering the mouse cursor over a button or setting for a few moments, a tooltip will appear.

The context-sensitive tooltip might contain some of these elements:

Related details depending on the control.

A keyboard or mouse shortcut associated to the tool.

The value of the property.

Hovering over a color property will display a large swatch preview of the color and the color’s hexadecimal, RGBA, and HSVA values.

Tooltip showing color information.¶

Source file of the active object. See also Linked Libraries.

The reason why the value is not editable.

When Python Tooltips are enabled, a Python expression is displayed for scripting (usually an operator or property).

Context menu ‣ Online Manual

You may want to access help for a tool or area from within Blender.

To do so, hover the cursor over the tool or button you need help with and use the keyboard shortcut or context menu item to visit pages of this reference manual from within Blender. This opens a web page relating to the button under the cursor, supporting both tool and value buttons.

We do not currently have 100% coverage. You may see an alert in the info header if a tool does not have a link to the manual.

In other cases, buttons may link to more general sections of the documentation.

The first options of this menu provide direct links to Blender-related websites. The same links can also be found in the Splash Screen.

This is a link to the Official Blender Manual (which you are now reading).

Links to various sites, providing both community and professional support.

Lists of many different community sites and support venues.

Learn how to give back to the Blender community by contributing to projects or donating.

Link to the release notes for the current Blender version.

The Blender Bug Tracker (registration needed). For more information on bug reporting, please see Reporting a Bug.

This extracts system information which can be useful for including in bug reports, inspecting the configuration, or diagnosing problems.

You will be prompted to save a text file called system-info.txt.

It contains the following sections:

This section shows you the Blender version, details about the build configuration, and the path in which Blender is running.

The version and path of your Python installation.

Paths used for scripts, data files, presets and temporary files.

Those directories are configured using the Preferences Editor.

The version of the installed FFmpeg components and codecs.

The version of other libraries used by Blender such as OpenColorIO, Alembic, USD, etc.

Shows the GPU vendor, version and the capabilities of your hardware and driver.

Specific limits on GPU functions related to how the current version of Blender was compiled.

The instruction sets and capabilities of each hardware render device available for use with Cycles.

Lists add-ons currently in use along with their versions and paths.

---

## Installing Blender¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/installing/index.html

**Contents:**
- Installing Blender¶
- System Requirements¶
- Download Blender¶
- Installation Guides¶

Blender is released approximately every three months. You can keep up to date with the latest changes through the release notes.

Blender is available for download on Windows, macOS, and Linux. Always check that your graphics drivers are up to date and that OpenGL is properly supported. Blender has a set of minimum and recommended requirements; so make sure these are met before trying to install Blender.

Support for other hardware such as graphic tablets and 3D mice are covered later in Configuring Hardware.

Blender offers a variety of different binary packages to choose from depending on their level of stability. Each package has the trade off of newest features versus stability. The package that is right for you depends on your requirements for those two. A studio, for example, might want to have long-term support, while a hobbyist may want newer features, while others may just want to test upcoming features. Each package described below has something just right for everyone.

A package that contains the latest features and is considered stable without regressions. A new stable version is available roughly every three months.

A package designed for long-lasting projects requiring a very stable version of Blender. LTS releases are supported for two years and will not have any new features, API changes or improvements. A new long-term support version is available every year. These LTS releases will occasionally have minor patches (such as 4.2.6) which improve stability or fix critical bugs.

A package updated daily to include the newest changes in development. These versions are automatically built on a schedule. They are not as thoroughly tested as the release types above, and might break or crash. Builds marked as Alpha are still undergoing major changes and feature additions, while those marked Beta are feature-complete and are under development for refinement and stability.

Stability can be expected to increase from Alpha to Beta to Release Candidate (RC) to a final release.

Blender’s source code is available for free to either reference or to build and use. While normal users are not expected to compile Blender, it does have advantages:

Blender is always up to date.

It allows access to any version or branch where a feature is being developed.

It can be freely customized.

Curious users can look through the source code and make small changes to see the effects to better understand how Blender works.

The procedure for installing a binary, either the latest stable release or a daily build, is the same. Follow the steps for your platform listed below.

Blender is designed to not require an internet connection, so it doesn’t have a built-in update system. This means you will need to update Blender yourself by following the platform-specific upgrade steps described in the sections below.

---

## Installing from Steam¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/installing/steam.html

**Contents:**
- Installing from Steam¶
- Updating with Steam¶

Steam is a software distribution platform. Blender can be downloaded and updated using the Steam client by following the steps described below on Linux, macOS, or Windows.

Download and install the Steam client for your operating system.

Once it is installed, open the client and login to your Steam account, or create an account if you don’t already have one. After logging in, navigate to the Store tab, search for “Blender”, and press the green Install button. Blender should now be available in the Library tab of the Steam client, where it can be launched. Optionally, a shortcut can be added to your desktop by right-clicking on it in your library list.

When installing Blender from Steam on Linux and Windows, the .blend filename extension will not be automatically associated with Blender. To associate blend-files with Blender, see the processes described on the Linux and Windows installation pages.

When an update for Blender is available on Steam, Steam will automatically download and apply the update for you.

---

## Installing on Linux¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/installing/linux.html

**Contents:**
- Installing on Linux¶
- Install from blender.org¶
- Install from a Package Manager¶
- Install from Snap¶
- Running from the Terminal¶
- Graphics System (X11 & Wayland)¶
- Avoiding Alt-Mouse Conflict¶
- Updating on Linux¶
  - Updating from blender.org¶
  - Updating with a Package Manager¶

Check the Downloading Blender page to find the minimum requirements and the different versions that are available for Blender (if you have not done so yet).

Download the Linux version for your architecture and decompress the file to the desired location (e.g. ~/software or /usr/local).

Blender can now be launched by double-clicking the executable.

When using this method of installation, it is possible to have multiple versions of Blender installed.

For ease of access, you may wish to add a menu entry and create blend-file associations for the file-browser. This can be done by Registering Blender.

To make the installation and configuration fully self-contained, set up a Portable Installation.

Some Linux distributions may have a specific package for Blender in their repositories.

Installing Blender via the distribution’s native mechanisms ensures consistency with other packages on the system and may provide other features (given by the package manager), such as listing of packages, update notifications and automatic menu configuration. Be aware, though, that the package may be outdated compared to the latest official release, or not include some features of Blender. For example, some distributions do not build Blender with Cycles GPU rendering support, for licensing or other reasons.

If there is a specific package for your distribution, you may choose what is preferable and most convenient. Otherwise, the official binary is available on blender.org.

Snap is a universal package manager designed to work across a range of distributions. Assuming snap is already installed, Blender can be installed through snap with:

Installing from this method has a benefit that updates to Blender are automatically installed. Blender from Snap should have a more consistent distribution than individual package managers.

See Launching from the terminal.

Blender supports both X11 and Wayland. See Linux Windowing Environment for details.

Some window managers default to Alt-LMB and Alt-RMB for moving and resizing windows.

Blender uses these for various operations, notably:

Emulate 3 Button Mouse.

Changing multiple properties at once.

To access Blender’s full feature set, you can change the window manager settings to use the Meta key instead (also called Super or Windows key):

Enter the following in a command line (effective at next login):

System Settings ‣ Window Management ‣ Window Behavior ‣ Window Actions, Switch from ‘Alt’ to ‘Meta’ key.

On Linux there are two ways to update Blender. This section covers the most common approaches.

When an update for Blender is released, it can be downloaded directly from the Blender website and installed using the steps described in the section Install from blender.org.

Many Linux distributions have packages for Blender available, which can be installed using the distribution’s package manager. After installation, Blender can be updated using the same steps as updating any other application.

The Splash screen Defaults page for information about importing settings from previous Blender versions and other quick settings.

Extracting Blender’s archive using 7-zip is not supported. TAR must be used instead. For more details, see issue #104070.

**Examples:**

Example 1 (unknown):
```unknown
snap install blender --classic
```

Example 2 (typescript):
```typescript
gsettings set org.gnome.desktop.wm.preferences mouse-button-modifier '<Super>'
```

---

## Installing on macOS¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/installing/macos.html

**Contents:**
- Installing on macOS¶
- Install from a DMG¶
- Updating on macOS¶
  - Updating from a DMG¶

Check the Downloading Blender page to find the minimum requirements and the different versions that are available for Blender (if you have not done so yet).

Blender supports both Intel and Apple Silicon architectures on macOS. Make sure to download a variant that is compatible with your CPU’s architecture.

Blender for macOS is distributed as disk images (dmg-files). To mount the disk image, double-click on the dmg-file. Then drag Blender.app into the Applications folder.

Depending on the Security and Privacy preferences of your Mac, macOS will request your approval before opening Blender for the first time.

To make the installation and configuration fully self-contained, set up a Portable Installation.

On macOS there is one main way to update Blender. This section covers that approach.

When an update for Blender is released, it can be downloaded directly from the Blender website. Install the new version by overwriting the current Blender.app in the Applications folder. You can rename Blender.app or place it in a different folder to have more than one version at a time.

The Splash screen Defaults page for information about importing settings from previous Blender versions and other quick settings.

---

## Installing on Windows¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/installing/windows.html

**Contents:**
- Installing on Windows¶
- Install from Windows Installer File¶
- Install from Zip¶
- Install from Microsoft Store¶
- Updating on Windows¶
  - Updating from a Windows Installer File¶
  - Updating from a Zip¶
  - Updating from the Microsoft Store¶

Check the Downloading Blender page to find the minimum requirements and the different versions that are available for Blender (if you have not done so yet).

Download the zip-file or Windows Installer File.

Blender supports both x64 and arm64 architectures on Windows. Make sure to download a variant that is compatible with your CPU’s architecture.

The Windows installer will let you choose an installation folder, and will create an entry in the start menu as well as associate blend-files with Blender. It requires administrator rights.

When choosing the zip-file, you have to manually extract Blender to the desired folder, where you can double-click the executable to run Blender.

No start menu item will be created and no blend-file association will be registered, but there is also no need for administrator rights. You can register the file association manually by clicking Register on the System tab of the Preferences. Alternatively, you can run blender -r from the Command Line.

To make the installation and configuration fully self-contained, set up a Portable Installation.

Blender can be installed from the Microsoft Store by searching for Blender in the Microsoft Store and installing it.

After installation, Blender can now be launched from the Windows Start menu.

On Windows there are a few ways to update Blender. This section covers the most common approaches.

When an update for Blender is released, it can be downloaded directly from the Blender website. The Windows installer can then be run to install the updated version of Blender. To remove a previously installed version of Blender, use Windows settings or control panel to uninstall the desired version.

When an update for Blender is released, it can be downloaded directly from the Blender website and extracted to the desired folder, where you can double-click the executable to run Blender. For more information on creating a portable version of Blender, see the section Install from Zip.

Note, you do not have to overwrite your existing Blender installation. It’s perfectly possible to have multiple versions installed side by side.

When an update for Blender is available on the Microsoft Store, it will be downloaded and installed automatically.

The Splash screen Defaults page for information about importing settings from previous Blender versions and other quick settings.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/graph_editor/introduction.html

**Contents:**
- Introduction¶
- Main Region¶
  - Navigation¶
  - Playhead & 2D Cursor¶
- Header¶
  - View Menu¶
  - Select Menu¶
  - Marker Menu¶
  - Channel Menu¶
  - Key Menu¶

The Graph Editor lets you edit animation curves, which determine how properties change over time.

The curve view allows you to view and edit F-Curves. An F-Curve has several key parts:

The curve describes how the value of a property (Y axis) evolves over time (X axis).

Keyframes are user-defined values on certain frames and are represented by little black discs that become orange when selected. The values on the other frames are calculated automatically by interpolating between these keyframes.

Each keyframe has two handles – points that can be dragged around to influence the shape of the curve around it.

A simple curve. The discs are keyframes, and the circles are their handles.¶

See F-Curves for more info.

As with most editors, you can:

Pan the view by dragging with MMB.

Zoom in and out with the mouse Wheel.

Scale the view horizontally or vertically by dragging with Ctrl-MMB.

You can also use the scrollbars.

You can focus the view on the curve of an animated property by right clicking it and choosing View in Graph Editor. If you want to set up a hotkey for this, you need to open the Keymap preferences, open the User Interface category, click Add New, fill in the operator name anim.view_curve_in_graph_editor, and finally choose a shortcut. Normally this can be done more easily by right clicking the context menu item and choosing Assign Shortcut, but in this case, the shortcut would be added to the wrong category and not work.

Graph Editor 2D Cursor.¶

The current frame is represented by a vertical blue line called the Playhead. Like other Animation Editors, you can move it by clicking or dragging with LMB in the scrubbing area at the top.

Combined with the horizontal blue line, the Playhead forms the 2D Cursor which can be used as a pivot point for rotating and scaling. You can disable the horizontal line using View ‣ Show Cursor or Sidebar ‣ View ‣ Show Cursor.

The 2D Cursor can be moved by clicking or dragging with Shift-RMB or by adjusting its coordinates in the View tab of the Sidebar.

Shows or hides the Sidebar Region.

Displays a pop-up panel to alter properties of the last completed operation. See Adjust Last Operation.

Shows or hides the Channels Region.

Show or hide the Playback Controls.

Pans and zooms the view to focus on the selected keyframes.

Pans and zooms the view to show all keyframes.

Reset the horizontal view to the current scene frame range, taking the preview range into account if it is active.

Centers the area to the Playhead.

Whether to update other views (such as the 3D Viewport) while you’re moving keyframes around. If disabled, the other views only get updated once you finish the move.

Shows a value slider next to each channel. Adjusting such a slider automatically creates a keyframe.

Automatically merge keyframes that end up on the same frame after transformation.

Automatically locks the movement of keyframes to the axis that best matches the direction of the mouse cursor.

Shows the marker region. When disabled, the Marker Menu is also hidden and marker operators are not available in this editor.

Toggles the visibility of the horizontal blue line (see Playhead & 2D Cursor).

Show timing in seconds instead of frames. As an example, the timestamp 01:03+02 means “1 minute, 3 seconds, 2 frames.”

Synchronizes the horizontal panning and scale of the editor with other time-based editors that also have this option enabled. That way, they always show the same section of time.

Toggles the visibility of the extrapolated portion of curves.

Toggles the display of keyframe handles.

Only shows the handles for the selected keyframes.

Lets you drag a box to define a time range for previewing. As long as this range is active, playback will be limited to it, letting you repeatedly view a segment of the animation without having to manually rewind each time.

You can change the start or end frame using the corresponding button in the Timeline editor’s Playback popover. Alternatively, you can simply run Set Preview Range again.

Clears the preview range.

Applies a preview range that encompasses the selected keyframes.

Changes the area’s editor to the Dope Sheet Editor.

Area controls. See the user interface documentation for more information.

Selects all keyframes and handles.

Clears the selection.

Inverts the selection.

Lets you drag a box and selects the keyframes and handles inside it.

Lets you drag a box and selects the keyframes and handles inside the corresponding time range, even if they’re above or below the box.

Selects keyframes and their handles inside the defined box.

Displays a circle around the cursor, which you can drag over keyframes and handles to select them.

Lets you draw a freehand shape and selects the keyframes and handles inside it.

Selects keys that are on the same frame as a key that’s already selected.

Selects all the keys that are on the current frame.

Selects keys that are on the same frame as a selected marker.

Selects keys that lie between the leftmost and rightmost selected markers.

Select the keys that lie before (or on) the current frame. You can also click Shift-Ctrl-LMB anywhere to the left of the Playhead.

Select the keys that lie after (or on) the current frame. You can also click Shift-Ctrl-LMB anywhere to the right of the Playhead.

Selects the handles of the currently selected keyframes.

Selects the keyframes of the currently selected handles.

Expands the selection to include the neighbors (in time) of the currently selected keys.

Deselects keyframes with fewer than two selected neighbors.

Selects keys that are on the same curve as a key that’s already selected.

Markers are used to denote frames with key points or significant events within an animation. Like with most animation editors, they’re shown at the bottom.

Markers in animation editor.¶

For descriptions of the different marker tools, see Editing Markers.

See Editing Channels.

See Editing F-Curves.

Scales the display of each curve so that they all (appear to) occupy the same value range, going from -1 to 1. This can make editing easier when you’re working with curves whose value ranges are far apart.

When you enable this option, the view is zoomed accordingly and the area outside the normalized value range is darkened.

If a preview range is defined, keyframes within the range are normalized, while the others are scaled proportionally.

Automatically recalculate curve normalization on every curve edit.

Only show curves belonging to objects/bones/… that are selected.

Show keyframes from objects/bones/… that are hidden.

Only show channels that have errors (for example, because they try to animate a property that doesn’t exist on the object).

Creates a snapshot of the current curves and shows it in the background so that you can use it as a reference. Click the button again to clear the snapshot.

Filters the channel list by a search term.

Select a collection to only show keyframes from objects in that collection.

Filter curves by property type.

Sorts data-blocks alphabetically to make them easier to find.

If your playback speed suffers because of this (should only really be an issue when working with lots of objects), you can turn it off.

Pivot point for rotating and scaling.

Center of the smallest possible box around the selected keyframes.

The intersection between the Playhead and the horizontal Cursor line.

Rotate/scale each handle around its keyframe.

The icon toggles snapping on or off. The dropdown offers the following options:

Type of element to snap to.

Snap to the nearest Marker.

When disabled, keyframes will move in increments of Snap To. For example, if you selected Second and have a keyframe that’s currently on 0:06+5, dragging it to the right will snap it to 0:07+5. Its time increases by a second, and its subsecond offset of 5 frames remains the same.

When enabled, keyframes will snap to multiples of Snap To. Taking the above example, the keyframe would snap to 0:07+0, removing the subsecond offset.

See Proportional Editing.

The Playback Controls region contains controls and options related to playback, keying, auto keyframing, and transport.

These settings allow you to:

Control how animations are previewed and synchronized with audio.

Insert and manage keyframes through keying sets and auto keying.

Navigate the timeline using playback and transport controls.

Adjust frame ranges and preview specific segments of the animation.

For a detailed description of all properties and controls commonly found in the footer, see the Playback Controls documentation.

Toggles the visibility of the 2D Cursor’s horizontal line.

Shows, and lets you change, the X coordinate (current frame) and Y coordinate (value) of the 2D Cursor.

Places the 2D Cursor at the average time and value of the selected keyframes.

Places the 2D Cursor at the average value of the selected keyframes, leaving its time unchanged.

See F-Curve Properties.

See F-Curve Modifiers.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/surfaces/introduction.html

**Contents:**
- Introduction¶

A Surface is a smooth sheet that’s defined by a set of control points. It’s an extension of a Curve, which is a smooth line.

Surface in Edit Mode.¶

The control points are arranged in a grid with yellow lines indicating the rows (U direction) and pink lines the columns (V direction). The surface can be open or closed (cyclic) in either or both directions, which allows the creation of, say, a cylinder or a sphere.

A Surface can be converted to a mesh using the menu item Object ‣ Convert ‣ Mesh or the context menu item Convert To ‣ Mesh.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/introduction.html

**Contents:**
- Introduction¶

Particles are lots of items emitted from mesh objects, typically in the thousands. Each particle can be a point of light or a mesh, and be joined or dynamic. They may react to many different influences and forces, and have the notion of a lifespan. Dynamic particles can represent fire, smoke, mist, and other things such as dust or magic spells.

Hair type particles are a subset of regular particles. Hair systems form curves that can represent hair, fur, grass and bristles.

You see particles as a Particle Modifier, but all settings are done in the Particle tab.

Some fur made from particles.¶

Particles generally flow out from their mesh into space. Their movement can be affected by many things, including:

Initial velocity out from the mesh.

Movement of the emitter (vertex, face or object) itself.

Movement according to “gravity” or “air resistance”.

Influence of force fields like wind, vortexes or guided along a curve.

Interaction with other objects like collisions.

Partially intelligent members of a flock (herd, school, …), that react to other members of their flock, while trying to reach a target or avoid predators.

Smooth motion with soft body physics (only Hair particle systems).

Or even manual transformation with Lattices.

Particles may be rendered as:

Halos (for Flames, Smoke, Clouds).

Meshes which in turn may be animated (e.g. fish, bees, …). In these cases, each particle “carries” another object.

Hair curves, following the path of the particle. These hair curves can be manipulated in the 3D Viewport (combing, adding, cutting, moving, etc.).

Every object may carry many particle systems. Each particle system may contain up to 10,000,000 particles. Certain particle types (Hair and Keyed) may have up to 10,000 children for each particle (children move and emit more or less like their respective parents). The size of your memory and your patience are your practical boundaries.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/introduction.html

**Contents:**
- Introduction¶

Sculpting and painting offers a more freeform workflow of editing via brushes. There are several modes to do this, each with their own purpose.

Sculpting: Change and transform the topology of your mesh.

Vertex Paint: Change the color of vertices in the active Color Attribute.

Weight Paint: Change the weight of vertices in the active vertex group.

Texture Paint: Change the pixels of the active image texture.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/keyframes/introduction.html

**Contents:**
- Introduction¶
- Visualization¶
- Interpolation¶
- Keyframe Types¶
- Handles & Interpolation Mode Display¶

A Keyframe is simply a marker of time which stores the value of a property.

For example, a Keyframe might define that the horizontal position of a cube is at 3 m on frame 1.

The purpose of a Keyframe is to allow for interpolated animation, meaning, for example, that the user could then add another key on frame 10, specifying the cube’s horizontal position at 20 m, and Blender will automatically determine the correct position of the cube for all the frames between frame 1 and 10 depending on the chosen interpolation method (e.g. Linear, Bézier, Quadratic, etc.).

An overview of existing keyframes can be seen via the Dope Sheet editor.

There are some important visualization features in the 3D Viewport that can help animation.

When the current frame is a keyframe for the current active object, the name of this object (shown in the upper left corner of the 3D Viewport) turns yellow.

Top: Current frame is a keyframe for Cube. Bottom: Current frame isn’t a keyframe.¶

Keyframe interpolation is represented and controlled by animation curves, also known as F-Curves. These curves can be viewed and modified via the Graph Editor.

Constant, Linear, Quadratic and Bézier interpolation, with Linear extrapolation.¶

The X axis of the curve corresponds to time, while Y represents the value of the property. Keyframes themselves define points of the curve, while interpolation is controlled by additional parameters.

The Interpolation Mode is the main setting that specifies for each keyframe how the curve is interpolated from that key to the next one. There are a number of modes with fixed shapes, e.g. Constant, Linear, Quadratic etc, and a free form Bézier mode.

Extrapolation specifies how the curve extends before the first, and after the last keyframe. The main available choices are Constant and Linear; it is also possible to configure the curve to loop.

Bézier interpolation is controlled by handles, which have a handle type and position. The position of Free and Aligned handles must be set manually from the Graph editor, while Vector, Automatic and Auto Clamped handles are computed automatically from keyframe values.

Interpolation, Extrapolation and Handle Type can also be changed from the Dope Sheet editor.

Handle smoothing modes. Red: None, Green: Continuous Acceleration.¶

The method how the three automatic handle types are computed is controlled by the per-curve Auto Handle Smoothing setting. The None mode resembles how most other software works and only considers the values of the immediately adjacent keys. The Continuous Acceleration mode considers the shape of the whole curve, which produces smoother results out of the box, but means that changes in one key affect interpolation over a larger section of the curve; it also tends to overshoot more with Automatic handles.

For visually distinguishing regular keyframes from different animation events or states (extremes, breakdowns, or other in-betweens) there is the possibility of applying different colors on them for visualization.

Left: not selected; Right: selected.¶

Breakdown state. e.g. for transitions between key poses.

A keyframe that adds a small amount of motion around a holding pose. In the Dope Sheet it will also display a bar between them.

An ‘extreme’ state, or some other purpose as needed.

A filler or baked keyframe for keying on ones, or some other purpose as needed.

A key generated by some tool, for example Copy Global Transform: Fix to Camera. This keyframe type indicates to Blender and add-ons that it is safe to remove and re-generate them, so be careful when manually marking your hand-made animation with this type.

Dope Sheet can display the Bézier handle type associated with the keyframe, and mark segments with non-Bézier interpolation. This facilitates basic editing of interpolation without the use of the Graph Editor.

The icon shape represents the type of the Bézier Handles belonging to the keyframe.

From top: summary, Bézier, linear.¶

Auto Clamped (default)

If the handles of a keyframe have different types, or in case of summary rows representing multiple curves, out of the available choices the icon that is furthest down the list is used. This means that if a grouped row uses a circle icon, it is guaranteed that none of the grouped channels have a non-auto key.

Horizontal green lines mark the use of non-Bézier Interpolation. The line is dimmed in summary rows if not all grouped channels have the same interpolation.

Display of this information can be disabled via the Show Handles and Interpolation option of the Dope Sheet’s View Menu.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/shape_keys/introduction.html

**Contents:**
- Introduction¶
- Relative or Absolute Shape Keys¶
  - Relative¶
  - Absolute¶

Shape keys are used to deform objects into new shapes for animation. In other terminology, shape keys may be called morph targets or blend shapes.

The most common use cases for shape keys are in character facial animation (e.g. mouth positions, expressions, phonemes) and in refining a skeletal rig. They are particularly useful for modeling organic, soft body parts and muscles, where additional control over the resulting shape is needed beyond what can be achieved with transformations such as rotation or scale.

Shape keys can be applied to object types with vertices, such as meshes, curves, surfaces, and lattices.

Example of a mesh with different shape keys applied.¶

Every object with shape keys maintains a stack of keys. This stack may be of Relative or Absolute type.

Use Relative Shape Keys for animation scenarios where shapes need to be blended together, such as facial expressions or corrective poses.

Use Absolute Shape Keys for shape changes that progress in a sequence over time, such as morphing an object smoothly into different states.

Relative shape keys are mainly used for muscles, limb joints, and facial animation. Each shape is defined relative to the Basis or to another specified shape key.

The final result visible in the 3D Viewport, also called the Mix, is the cumulative effect of each shape key with its current value. Starting from the Basis shape, Blender applies each shape’s weighted offset relative to its reference key.

Controls the blend between a shape key and its reference key.

0.0 = 100% influence of the reference key

1.0 = 100% influence of the shape key

Blender can extrapolate blends above 1.0 and below 0.0, which may amplify or invert the deformation.

The Basis is the first (top-most) key in the stack.

Represents the object’s vertices in their original positions.

Has no weight value and cannot be keyed.

Serves as the default Reference Key when creating new shape keys.

Absolute shape keys are mainly used to deform an object into different shapes over time. Instead of being blended together, each key corresponds to a specific Evaluation Time.

The resulting shape, or Mix, is computed by interpolating between the previous and next keys according to the current Evaluation Time.

Represents the Evaluation Time (in frames) at which the shape key will be active.

The Basis is the first (top-most) key in the stack.

Represents the object’s vertices in their original positions.

Defines the starting shape for the absolute sequence.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/weight_paint/introduction.html

**Contents:**
- Introduction¶
- The Weighting Color Code¶
- Normalized Weight Workflow¶

Vertex Groups can potentially have a very large number of associated vertices and thus a large number of weights (one weight per assigned vertex). Weight Painting is a method to maintain large amounts of weight information in a very intuitive way.

It is primarily used for rigging meshes, where the vertex groups are used to define the relative bone influences on the mesh. But we use it also for controlling particle emission, hair density, many modifiers, shape keys, etc.

Vertex group in Weight Paint Mode.¶

You can enter Weight Paint Mode from the Mode selector Ctrl-Tab. The selected mesh object is displayed slightly shaded with a rainbow color spectrum. The color visualizes the weights associated to each vertex in the active vertex group. By default blue means unweighted and red means fully weighted.

You can assign weights to the vertices of the object by painting on it with weight brushes. Starting to paint on a mesh automatically adds weights to the active vertex group (a new vertex group is created if needed).

Vertex Groups can be managed in the pallette pop-over in the middle of the header.

Weights are visualized by a gradient using a cold/hot color system, such that areas of low value (with weights close to 0.0) are displayed as blue (cold) and areas of high value (with weights close to 1.0) are displayed as red (hot). And all in-between values are displayed as rainbow colors (blue, green, yellow, orange, red).

The color spectrum and their respective weights.¶

In addition to the above described color code, Blender has a special visual notation (as an option) for unreferenced vertices: They are displayed as black. Thus you can see the referenced areas (displayed as cold/hot colors) and the unreferenced areas (in black) at the same time. This is most useful when you look for weighting errors. See Viewport Overlays.

Unreferenced vertices example.¶

You can customize the colors in the weight gradient by enabling Custom Weight Paint Range in the Editing tab of the Preferences.

In order to be used for things like deformation, weights usually have to be normalized, so that all deforming weights assigned to a single vertex add up to 1. The Armature modifier in Blender does this automatically, so it is technically not necessary to ensure that weights are normalized at the painting stage.

However, while more complicated, working with normalized weights has certain advantages, because it allows use of certain tools designed for them, and because when weights are normalized, understanding the final influence of the current group does not require knowing weights in other groups on the same vertex.

These tools are provided to aid working with normalized weights:

In order to start working with normalized weights it is first necessary to normalize the existing weights. The Normalize All tool can be used for that. Make sure to select the right mode and disable Lock Active.

Once the weights are initially normalized, the Auto Normalize option can be enabled to automatically maintain normalization as you paint. This also tells certain tools that the weights are supposed to be already normalized.

Any vertex group can be locked to prevent changes to it. This can be done via the lock icon in the vertex group list, or using bone selection and the locks pie menu.

This setting prevents accidental edits to groups. However, since it is also respected by Auto Normalize, in the normalized weight workflow it has a more significant meaning of locking the current influence of chosen bones, so that when you paint other bones, the weight is redistributed only between the unlocked groups.

In locations affected by multiple bones, this allows more precise tweaking and re-balancing of weights by temporarily focusing on a subset of bones. This can also be aided by the Lock Relative option, which displays unlocked groups as though re-normalized with the locked groups deleted, thus making it appear as if the locked groups did not even exist.

Finally, the Multi-Paint option allows treating multiple selected bones as if they were one bone, so that the painting operations change the combined weight, preserving the ratio within the group. Combined with locking, this allows balancing between one set of bones versus the rest, excluding a third set that has its influence not affected in any way due to locks.

Technically, this option does not require the normalized workflow, but since non-normalized weights can add to more than 1, the weight display behaves best with Auto Normalize enabled.

For example, when dealing with a bone loop, e.g. mouth or an eye, selecting the loop with Multi-Paint exposes the falloff between the loop as a whole and surrounding bones, while locking the surrounding bones and using Lock Relative displays the falloff between bones within the loop. Thus the complex two-dimensional falloff of each bone can be viewed and edited as two independent one-dimensional gradients.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/skinning/introduction.html

**Contents:**
- Introduction¶

We have seen in previous pages how to design an armature, create chains of bones, etc. Now, having a good rig is not the final goal, unless you want to produce a “Dance Macabre” animation, you will likely want to put some flesh on your skeletons! Surprisingly, “linking” an armature to the object(s) it should transform and/or deform is called the “skinning” process…

The human mesh skinned on its armature.¶

In Blender, you have two main skinning types:

You can Parent/Constrain Objects to Bones – then, when you transform the bones in Pose Mode, their “children” objects are also transformed, exactly as with a standard parent/children relationship… The “children” are never deformed when using this method.

You can Use the Armature Modifier on entire Mesh, and then, some parts of this object to some bones inside this armature. This is the more complex and powerful method, and the only way to really deform the geometry of the object, i.e. to modify its vertices/control points relative positions.

Retargeting, which is a way to apply motion-capture data (acquired from real world) to a rig, is available through add-ons and importers.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/object/editing/transform/introduction.html

**Contents:**
- Introduction¶

Transformations refer to a number of operations that can be performed on a selected Object or Mesh that alters its position or characteristics.

Each object can be moved, rotated and scaled in Object Mode. However, not all of these transformations have an effect on all objects. For example, scaling a camera has no effect on the render dimensions.

Basic transformations include:

These three transforms are the three big ones. However, more advanced transformations can be found in the Advanced Transformations section.

For making other changes to the geometry of editable objects, you should use Edit Mode.

Once you have added a basic object, you remain in Object Mode. You can switch between Object Mode and Edit Mode by pressing Tab. The object’s wireframe should now appear orange. This means that the object is now selected and active.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/outliner/introduction.html

**Contents:**
- Introduction¶
- Example¶

The Outliner editor.¶

The Outliner shows the content of the blend-file in a tree. You can use it to:

Get an overview of the data in the scene.

Select and deselect objects.

Make objects unselectable or invisible in the 3D Viewport.

Exclude objects from rendering.

Manage parent/child relationships and collections.

Items with an arrow on the left can be expanded. Click it with LMB to expand a single item, drag LMB to expand multiple items, or click Shift-LMB to expand an item recursively.

The Outliner with different kinds of data.¶

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/curves/introduction.html

**Contents:**
- Introduction¶

Curves and Surfaces are particular types of Blender objects. They are expressed by mathematical functions (interpolation) rather than linear interpolation between a series of points.

Blender offers both Bézier and NURBS. Both Bézier curves and NURBS curves and surfaces are defined in terms of a set of “control points” (or “control vertices”) which define a “control polygon”.

Blender logo made from Bézier curves.¶

Both Bézier and NURBS curves are named after their mathematical definitions, and choosing between them is often more a matter of how they are computed behind the scenes than how they appear from a modeler’s perspective. Bézier curves are generally more intuitive because they start and end at the control points that you set, but NURBS curves are more efficient for the computer to calculate when there are many twists and turns in a curve.

The main advantage to using curves instead of polygonal meshes is that curves are defined by less data and so can produce results using less memory and storage space at modeling time. However, this procedural approach to surfaces can increase demands at render time.

Certain modeling techniques, such as extruding a profile along a path, are possible only using curves. On the other hand, when using curves, vertex-level control is more difficult and if fine control is necessary, mesh editing may be a better modeling option.

Bézier curves are the most commonly used curves for designing letters or logos.

They are also widely used in animation, both as for objects to move along (see constraints below) and as F-Curves to change the properties of objects as a function of time.

Modifiers & Constraints

Follow Path Constraint

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/introduction.html

**Contents:**
- Introduction¶
- Editor Layout¶
- View Types¶
- Performance¶

The Video Sequencer allows you to place images, videos, sounds, and scenes on a timeline and combine them into a new video. This section only describes its UI; to read more about its usage, see the Video Editing section.

The Video Sequencer is composed of multiple regions. They are described in more detail in the next sections. Figure 1 shows the combined Sequencer & Preview view type:

Figure 1: The Video Sequencer Editor shown in the Sequencer & Preview view type.¶

Contains menus and buttons for interacting with the editor. The header changes slightly depending on the selected view type (see below).

Contains menus and buttons for interacting with animation playback.

Shows the output of the Sequencer at the time of the Playhead.

Shows a timeline for managing the montage of strips.

Shows the properties of the active strip. It’s divided into panels and tabs. Toggle on or off with N.

Shows a list of tools. Toggle on or off with T.

The Video Sequencer has three view types which can be changed using the View Type selector (see figure 1; top left).

Figure 2: Three view types for the Video Sequence Editor¶

View timeline and strip properties.

View preview window and preview properties.

Combined view of preview and timeline and their properties.

Rather than having one Video Sequencer in the Sequencer & Preview mode, it can be more useful to have one in the Sequencer mode and another in the Preview mode, the reason being that Sequencer & Preview lacks most of the Preview tools. Blender’s default Video Editing workspace offers this layout.

Playback performance can be improved in several ways.

The method with the most impact is to allow the Video Sequencer to cache generated frames. There are two levels of cache: a memory cache, which is enabled by default (and can be enlarged if RAM allows), and a disk cache, which is slower but has more capacity. Both of these can be configured in the Preferences.

Another way to improve performance is by using Strip Proxies. These are copies of source images and videos with a lower resolution and/or quality, making them faster to load than the originals.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/image/introduction.html

**Contents:**
- Introduction¶
- Toolbar¶
- Header¶
- Asset Shelf Region¶
- Main View¶

The Image Editor lets you create, view, and edit images, as well as see render results and intermediate Compositor output.

Image Editor with a test grid texture.¶

Used to sample the color of one or more pixels in the image. As long as you hold LMB, the footer will show the following:

X and Y coordinates of the mouse cursor.

Color in RGB after Color Management.

The dimensions of the square used to sample underlying pixels. If larger than 1, the resulting sample is an average of all underlying pixels.

See Annotations for more information.

Tools for controlling how the content is displayed in the editor. See Navigating.

Tools for opening and manipulating images. Shows an asterisk if the image has unsaved changes. See Editing Images.

A data-block menu used for selecting images. Once an image is selected, the Image tab appears in the Sidebar region.

Apart from loading existing images, you can also create new ones:

The pop-over that’s displayed when clicking “New Image” in the header.¶

The Tiled option creates an image with support for UDIMs. For the other options, see Generated Images.

In addition to images, the data-block selector includes the following items:

Render Result: displays renders. When this item is selected, the Slot, View Layer, and Render Pass selectors become available (see below).

Viewer Node: displays the image that’s fed into the Viewer Node in the Compositor.

Prevents the Image Editor from automatically switching to the texture of the selected object. (This switching only happens if the 3D Viewport is in Texture Paint mode).

This toggle is only visible on the Render Result if a Sequencer Scene exists, and it differs from the active scene in the window. After rendering, its state is chosen automatically from the render type.

The render slot to view (and render to). You can create new renders without losing previous ones by selecting an empty slot before rendering. Afterwards, you compare them by pressing J and Alt-J to cycle forwards and backwards. Alternatively, you can use the number keys 1, 2, 3 etc. to select the slot with the corresponding number.

Slots can be renamed by double clicking their name in the Image panel in the Sidebar.

The View Layer to display.

The Render Pass to display.

Lets you show/hide all gizmos using the toggle button, or specific gizmos using the drop-down arrow.

Enable/disable the gizmos used to pan or zoom the 2D viewport. See Navigation Gizmos for more information.

Select which color channels are displayed.

Enables transparency and shows a checkerboard behind the image.

Disables transparency.

Displays the alpha channel as a grayscale image. White areas are opaque, black areas are transparent.

Displays the depth from the camera, from Clip Start to Clip End, as specified in the Camera settings.

Single color channel visualized as a grayscale image.

Depending on the current mode, the asset shelf may be available, providing quick access to assets for this specific mode (for example brush assets in Paint mode).

See Asset Shelf for more information.

Holding RMB will sample the image just like the Sample tool, except it will always sample only one pixel.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/texture_node/introduction.html

**Contents:**
- Introduction¶
- Using Texture Nodes¶
- Header¶

The Texture Node Editor allows creating custom textures by combining colors, procedural patterns, and images in various ways. This is a step up from the built-in textures, where you can select a type from a list and not much more.

Textures – both built-in ones and node-based ones – are a legacy feature. For their original main purpose, which was of course texturing objects, they have been replaced by Materials which are set up in the Shader Editor.

Today, the use of Textures is limited to:

The Displace Modifier.

Influencing size, density etc. of particle systems.

Influencing emission locations of fire/smoke simulations.

In addition, the Displace modifier and fire/smoke simulations don’t support node-based textures, instead only working with the built-in ones.

Combined textures based on nodes.¶

The default Blender layout has no workspace containing the Texture Node Editor. You need to manually open it in an area of choice.

Once the editor is open, you first need to set the empty Texture Type selector to Brush, after which you can use the Data-Block Menu to start creating textures. Note that you need to enable Use Nodes in the header before you can add nodes.

See Nodes for the header items common to all node editors.

Deprecated – the scene’s World Environment is now defined using a Material rather than a Texture.

Show brush Textures in the data-block menu. Because the other two types are deprecated, this effectively shows all Textures.

Deprecated – Line Styles for the Freestyle renderer are now defined using Materials rather than Textures.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/texture_paint/introduction.html

**Contents:**
- Introduction¶
- Getting Started¶
- Texture Preview¶
- Saving¶
- Using an External Image Editor¶
- Known Limitations¶
  - UV Overlap¶
  - Perspective View & Faces Behind the View¶
  - Perspective View & Low Poly¶

A UV texture is a picture (image, sequence or movie) that is used to color the surface of a mesh. The UV texture is mapped to the mesh through one or more UV maps. There are three ways to establish the image used by the UV texture:

Use any image editing program to create an image. In the Image Editor, select the UV texture and load the image. Blender will then use that texture’s UV map to transfer the colors to the faces of the mesh.

Paint a flat image in the Image Editor onto the currently selected UV texture, using its UV map to transfer the colors to the faces of the mesh.

Paint the mesh in the 3D Viewport, and let Blender use the currently selected UV map to update the UV texture (as discussed below).

Blender features a built-in paint mode called Texture Paint which is designed specifically to help you edit your UV textures and images quickly and easily in either the Image Editor or the 3D Viewport. Since a UV texture is just a special-purpose image, you can also use any external paint program, like GIMP or Krita.

Texture painting in Blender.¶

Since a mesh can have layers of UV textures, there may be many images that color the mesh. However, each UV texture only has one image.

Texture Paint works in both a 3D Viewport and the Image Editor. In the 3D Viewport in Texture Paint Mode, you paint directly on the mesh by projecting onto the UVs.

Texture Paint is fast and responsive when working in the 3D Viewport and when your image is sized as a square where the side lengths are a power of two, e.g. 256×256, 512×512, 1024×1024, etc.

The object to be painted on must first be unwrapped. UVs can be added traditionally, with standard Unwrapping Tools, or by adding Simple UVs in Texture Paint mode.

When no UV layers can be detected, Blender will display a warning message.

Once you have unwrapped your model to a UV map, you can begin the texturing process. To use texture paint you may do any of the following:

Activate the Texture Paint workspace. Here the 3D Viewport has the Texture Paint Mode enabled and the Image Editor is already switched to Paint mode.

In the 3D Viewport, select Texture Paint Mode from the mode selector in the header, and you can paint directly onto the mesh.

In the Image Editor, switch the mode to Paint (shown in the image to the right).

Enabling Paint mode.¶

Once you enable Texture Painting, your mouse becomes a brush. As soon as you enable Texture Painting or switch to Texture Paint Mode, different tools become available in the Toolbar.

In the Image Editor, you paint on a flat canvas that is wrapped around the mesh using UV coordinates. Any changes made in the Image Editor show up immediately in the 3D Viewport, and vice versa.

To work with the UV layout (for example, to move coordinates) you must use the UV Editor.

A full complement of brushes and colors can be selected from the Sidebar region in the Image Editor. Brush changes made in either panel are immediately reflected in the other panel. However, the modified texture will not be saved automatically; you must explicitly do so with Save Image.

If your texture is already used to color, bump map, displace, alpha-transparent, etc., a surface of a model in your scene (in other technical words, is mapped to some aspect of a texture via a texture channel using UV as a map input), you can see the effects of your painting in the context of your scene as you paint.

To do this, set up side-by-side areas, one Area in 3D Viewport set to Texture shading option, and in the second Area the Image Editor loaded with your image. Position the 3D Viewport to show the object that is UV-mapped to the loaded image. In the image to the right, the texture being painted is mapped to the “Normal” attribute, and is called “bump mapping”, where the grayscale image is used to make the flat surface appear bumpy. See Texture Mapping Output for more information on bump mapping.

If the header menu item Image has an asterisk next to it means that the image has been changed, but not saved. Use Save Image or Save Image As to save your work with a different name or overwrite the original image.

Since images used as UV textures are functionally different from other images, you should keep them in a directory separate from other images.

The image format for saving is independent of the format for rendering. The format for saving a UV image is selected in the header of the File Browser, and defaults to PNG (.png).

If Packing is enabled in the File Browser’s header, or if you manually pack, saving your images to a separate file is not necessary.

If you use an external program to edit your UV texture, you must:

Run that paint program (GIMP, Krita, etc.).

Load the image or create a new one.

And re-save it within that program.

Back in Blender, you reload the image in the Image Editor.

You want to use an external program if you have teams of people using different programs that are developing the UV textures, or if you want to apply any special effects that Texture Paint does not feature, or if you are much more familiar with your favorite paint program.

In general overlapping UVs are not supported (as with texture baking).

However, this is only a problem when a single brush stroke paints onto multiple faces that share a texture.

When painting onto a face which is partially behind the view (in perspective mode), the face cannot be painted on. To avoid this, zoom out or use an orthographic viewport.

When painting onto a face in perspective mode onto a low-poly object with normals pointing away from the view, painting may fail; to workaround disable the Normal Falloff option in the stroke settings.

Typically this happens when painting onto the side of a cube (see Blender bug #34665).

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/geometry_nodes/introduction.html

**Contents:**
- Introduction¶

Geometry Nodes is a system for modifying the geometry of an object with node-based operations. It can be accessed by adding a Geometry Nodes Modifier and setting up the nodes in the Geometry Node Editor.

The properties of a Geometry Nodes modifier in the modifier stack.¶

The geometry node tree connected to a modifier is a Node Group. The geometry from the state before the modifier (the original geometry or the result of the previous modifier) will be passed to the Group Input node. Then the node group can operate on the geometry and pass an output to the Group Output node, where it will be passed to the next modifier.

Geometry nodes can modify different types of geometry:

The interface of the modifier is described in the Modifier page.

To expand Blender with node-group operators, see the Node-Based Tools page.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/emitter/physics/introduction.html

**Contents:**
- Introduction¶
- Common Physics Settings¶
- No Physics¶

The movement of particles may be controlled in a multitude of ways. Here we will discuss only the particle physics in the narrower sense, i.e. the settings in the Physics panel.

Additional ways of moving particles are:

By soft body animation (only for Hair particle systems).

By force fields and along curves.

Sets the size of the particles.

Give the particles a random size variation.

Specify the mass of the particles.

Causes larger particles to have larger masses.

The particles will be given no motion, which makes them belong to no physics system. At first a physics type that makes the particles to be static could seem a bit strange, but it can be very useful at times. None physics make the particles stick to their emitter their whole life time. The initial velocities here are for example used to give a velocity to particles that are affected by a harmonic effector with this physics type when the effect of the effector ends.

Moreover, it can be very convenient to have particles at disposal (whose both Unborn and Died are visible on render) to groom vegetation and/or ecosystems using Object or Group types of visualization.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/properties/introduction.html

**Contents:**
- Introduction¶
- Pose¶
- Bone Collections¶
- Motion Paths¶
- Inverse Kinematics¶
- Custom Properties¶

The Armature tab in Properties contains various panels gathering the armature settings.

The Armature tab in the Properties.¶

A radio button to switch between Pose Position and Rest Position.

In Edit Mode, you always see armatures in their rest position, in Object Mode and Pose Mode, by default, you see them in Pose Position (i.e. as it was transformed in the Pose Mode). If you want to see it in the rest position in all modes, select Rest Position.

See Bone Collections.

Armature ‣ Motion Paths

In the Motion Paths panel you can enable visualization of the motion path your skeleton leaves when animated.

Armature ‣ Inverse Kinematics

The Inverse Kinematics panel.¶

Defines the type of IK solver used in your animation.

Armature ‣ Custom Properties

See the Custom Properties page for more information.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/scene/introduction.html

**Contents:**
- Introduction¶
- Scenes as Assets¶
- Scenes in the Video Sequencer¶
- Controls¶

Scenes are a way to organize your work. Each blend-file can contain multiple scenes, which may share other data such as objects, materials, and collections.

A scene defines the visible objects, camera view, lighting setup, and render settings that make up a specific part of a project. For example, a single blend-file may include multiple scenes for different shots, lighting setups, or stages of a production pipeline.

Scene management and library linking are based on Blender’s Library and Data System. If you are not familiar with the concepts of data-blocks, linking, and appending, it is recommended to read that page first.

Scenes can also be marked and used as Assets. This allows them to appear in the Asset Browser for reuse across projects.

Scene assets are a convenient way to manage pre-built scene templates, lighting rigs, or shot setups. They store all relevant data (such as cameras, lights, and render settings) and can be dragged into any open Blender file.

When a scene asset is dragged into another window (except the Asset Browser itself), Blender performs one of the following actions:

Link or Append: Imports the scene into the current blend-file as a linked or appended data-block.

Activate: Sets the imported (or linked) scene as the active one in the window.

Scene assets generate preview images automatically by rendering from the active camera in Solid View mode. For this to work, the scene must contain an active camera.

Typical uses for scene assets include:

Creating reusable lighting or studio setups.

Storing shot layouts for multi-shot projects.

Maintaining consistent render settings across files.

Building base templates for new projects or departments.

Scenes can also be used as Scene Strips in the Video Sequencer. This allows you to composite or edit multiple scenes together in one timeline.

For example, each shot of an animation can be stored in its own scene, and then combined in a master scene that uses scene strips to sequence them in order. This workflow is useful for multi-shot projects, trailers, or layout editing without the need to render intermediate files.

When used as strips, scenes are rendered dynamically during playback or rendering, and they share the same data-blocks unless they were created as full copies.

You can select and create scenes with the Scene data-block menu in the Topbar.

Scene data-block menu.¶

A list of available scenes in the current blend-file.

Creates an empty scene with default values.

Creates an empty scene but copies render and world settings from the active scene.

Creates a new scene that shares all data with the current one. The new scene contains links to the same collections, objects, and data-blocks as the original. Changes made in one scene automatically affect the other, since they reference the same data.

Creates a fully independent scene with unique copies of all objects and their data. This is useful for variations or alternate versions of a scene that should not affect the original.

The Add Scene options determine which data are copied and which are shared (linked). Objects reference Object Data such as meshes or lights, and scenes can share or duplicate this relationship.

Deletes the current scene data-block. Note that Blender always requires at least one scene in a file; you cannot delete the last remaining one.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/introduction.html

**Contents:**
- Introduction¶
- Quick Start¶
  - Create and Use Grease Pencil¶
  - 2D Animation Template¶

Grease Pencil is a Blender object. It accepts the drawing information from a mouse or pressure-sensitive stylus and places it in 3D space as a collection of points, which are defined as a stroke.

The Grease Pencil object can be used to make traditional 2D animation, cut-out animation, motion graphics, or used it as storyboard tool, among other things.

An illustration in 3D space using the Grease Pencil object.¶

Strokes are created in Draw Mode, which requires a new keyframe in the animation timeline for the Grease Pencil object. Existing strokes can then be adjusted in Edit Mode and Sculpt Mode. Finally, artists can apply materials, modifiers, lighting, and visual effects to strokes.

Artists can add Grease Pencil to any existing Blender scene, or start with a 2D Animation template. The template offers some pre-configured options that are helpful for animation and storyboarding.

From Object Mode, Add ‣ Grease Pencil ‣ Blank.

Create a new keyframe or turn on Auto Key. (See Keyframe Editing)

Click and drag across the viewport to add strokes to the Grease Pencil object.

To create a new Blender file using the “2D Animation” project template use: File ‣ New ‣ 2D Animation.

Note the following pre-configured setup for the 2D Animation template:

2D Animation is the default active workspace.

World Properties ‣ Surface (Background) ‣ Color is set to white.

Color management Views is set to Standard.

The drawing plane is set to Front (X-Z).

Line and Fill layers, along with some stroke materials, are configured for Grease Pencil.

The animation timeline will automatically create a new keyframe when Grease Pencil is used on empty frames.

Grease Pencil can read pressure-sensitivity information from a Graphics Tablet or stylus.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/introduction.html

**Contents:**
- Introduction¶
- Header Region¶
  - Mode & Menus¶
  - Transform Controls¶
  - Display & Shading¶
- Toolbar Region¶
- Sidebar Region¶
- Asset Shelf Region¶

The 3D Viewport is used to interact with the 3D scene for a variety of purposes, such as modeling, animating, texture painting, etc.

The header contains various menus and controls based on the current mode. Its items are split into three groups:

The 3D Viewport has several modes used for editing different kinds of data. For example, the default Object Mode would let you place a character in the scene, while Pose Mode would allow you to pose it.

The shortcut Ctrl-Tab brings up a pie menu for quick mode switching. If you have an Armature selected, it’ll instead switch between Object Mode and Pose Mode.

Pressing Tab will switch between Object Mode and Edit Mode for objects that support it.

This menu offers tools for navigating in 3D space.

The other menus depend on the current mode, Object Mode menus listed below:

Contains tools for selecting objects.

Contains a list of different objects types that can be added to the scene.

Contains tools for operating on objects, such as duplicating them. A subset of these tools can also be accessed by right-clicking in the 3D Viewport.

Used to change the Transform Orientation, which affects the rotation of the transform gizmo.

Used to change the Pivot Point, which affects the location of the transform gizmo.

Offers options for snapping items to others that are nearby. You can hold Ctrl to toggle snapping on/off temporarily (as long as the key is held).

Used to smoothly transform unselected items that are near the selected ones. See Proportional Editing.

Change which types of objects are visible/selectable in the 3D Viewport. See Object Type Visibility.

Change how gizmos are displayed in the 3D Viewport.

Change how overlays are displayed in the 3D Viewport.

Make the whole scene transparent, allowing you to see and select items that would otherwise be occluded. This is a shortcut to the X-Ray option which can be found inside the Viewport Shading popover (see below).

In Pose Mode, this same button controls a different setting with its own separate on/off state. Rather than making the scene transparent, it shows the armature in front of any geometry.

Change the shading of the 3D Viewport.

The Toolbar contains tools depending on the current mode (for example, modeling tools in Edit Mode, brush tools in Sculpt Mode…).

See Tools for more information.

The Sidebar region contains properties of the active object and tool, as well as of the viewport itself.

See Sidebar for more information.

Depending on the current mode, the asset shelf may be available, providing quick access to assets for this specific mode (for example pose assets in Pose Mode, brush assets in Sculpt Mode).

See Asset Shelf for more information.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/introduction.html

**Contents:**
- Introduction¶
- Animation¶
  - State Colors¶
- Rigging¶
  - Examples¶

Animation is making an object move or change shape over time. Objects can be animated in many ways:

Changing their position, orientation or size in time;

Animating their vertices or control points;

Causing the object to move based on the movement of another object (e.g. its parent, hook, armature, etc.).

In this chapter, we will cover the first two, but the basics given here are actually vital for understanding the following chapters as well.

Animation is typically achieved with the use of keyframes.

State colors of properties.¶

Properties have different colors and menu items for different states.

Keyframed on the current frame

Keyframed on a different frame

Changed from the keyframed value

Controlled by a driver

The changed value highlight currently doesn’t work with NLA.

Rigging is a general term used for adding controls to objects, typically for the purpose of animation.

Rigging often involves using one or more of the following features:

This allows mesh objects to have flexible joints and is often used for skeletal animation.

To control the kinds of motions that make sense and add functionality to the rig.

Mesh deformation can be quite involved, there are multiple modifiers that help control this.

To support different target shapes (such as facial expressions) to be controlled.

So your rig can control many different values at once, as well as making some properties automatically update based on changes elsewhere.

Rigging can be as advanced as your project requires. Rigs effective define a user interface for the animator to use, without being concerned with the underlying mechanisms

An armature is often used with a modifier to deform a mesh for character animation.

A camera rig can be used instead of animating the camera object directly to simulate real-world camera rigs (with a boom arm, mounted on a rotating pedestal for example, effects such as camera jitter can be added too).

The content of this chapter is simply a reference to how rigging is accomplished in Blender. It should be paired with additional resources such as Nathan Vegdahl’s excellent introduction to the fundamental concepts of character rigging, Humane Rigging.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/metas/introduction.html

**Contents:**
- Introduction¶
- Visualization¶

Metaball objects (short meta) are implicit surfaces, meaning that they are not explicitly defined by vertices (as meshes are) or control points (as surfaces are): they exist procedurally. Meta objects are literally mathematical formulas that are calculated on-the-fly by Blender.

A very distinct visual characteristic of metas is that they are fluid mercurial, or clay-like forms that have a “rounded” shape. Furthermore, when two meta objects get close to one another, they begin to interact with one another. They “blend” or “merge”, as water droplets do, especially in zero-g (which, by the way, makes them very handy for modeling streams of water when you do not want to do a fluid simulation). If they subsequently move away from one another, they restore their original shape.

Each of these is defined by its own underlying mathematical structure, and you can at any time switch between them using the Active Element panel.

Typically Meta objects are used for special effects or as a basis for modeling. For example, you could use a collection of metas to form the initial shape of your model and then convert it to a mesh for further modeling or sculpting. Meta objects are also very efficient for ray tracing.

Names of Meta objects are very important, as they define families, and only objects within a same family interact with each other. Unlike other object types, even editing (transformations) in Object Mode will affect the generated geometry within the edited families.

In Object Mode, the calculated mesh is shown, along with a black “selection ring”.

Meta Ball in Edit Mode.¶

In Edit Mode (Fig. Meta Ball in Edit Mode.), a meta is displayed as a mesh (either shaded or as black wireframe, but without any vertex of course), with two colored circles: a red one for selection (pink when selected), and a green one for a direct control of the meta’s stiffness (light green when active). Note that except for the scale transformation, having the green circle highlighted is equivalent to having the red one.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/physics/particles/hair/introduction.html

**Contents:**
- Introduction¶
- Growing¶
- Styling¶
- Animating¶
- Rendering¶

Hair type particle system can be used for strand-like objects, such as hair, fur, grass, quills, etc.

Particle hair systems example. Used for the grass and fur.¶

The first step is to create the hair, specifying the amount of hair strands and their lengths.

The complete path of the particles is calculated in advance. So everything a particle does a hair may do also. A hair is as long as the particle path would be for a particle with a lifetime of 100 frames. Instead of rendering every frame of the particle animation point by point there are calculated control points with an interpolation, the segments.

The next step is to style the hair. You can change the look of base hairs by changing the Physics Settings.

A more advanced way of changing the hair appearance is to use Children. This adds child hairs to the original ones, and has settings for giving them different types of shapes.

You can also interactively style hairs in Particle Edit Mode. In this mode, the particle settings become disabled, and you can comb, trim, lengthen, etc. the hair curves.

Hair can be made dynamic using the cloth solver. This is covered in the Hair Dynamics page.

With Cycles you can render hair with specialized hair BSDFs Hair BSDF or Principled Hair BSDF.

Hair can also be used as a basis for the Particle Instance Modifier, which allows you to have a mesh be deformed along the curves, which is useful for thicker strands, or things like grass, or feathers, which may have a more specific look.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/volumes/introduction.html

**Contents:**
- Introduction¶
- Rendering¶
- Limitations¶

Volume objects are containers used to represent OpenVDB files in Blender. OpenVDB is a library and file format for the interoperability and storage of volumetric data. OpenVDB files may be generated by other software such as Houdini, or from Blender’s fluid simulation cache.

Volume objects can be created from the Add menu in the 3D Viewport, or by dragging and dropping vdb-files into Blender. For animations, a frame sequence of OpenVDB files can be imported.

WDAS cloud data set rendered in wireframe, Workbench, and Cycles.¶

Rendering volumes works the same as rendering smoke simulations. By default, the Principled Volume shader is used for rendering volume objects. It will use grids named density, color and temperature by default. If these are not available, another grid name must be chosen in the shader nodes.

OpenVDB excels at representing sparse volumes, that aren’t necessarily concentrated within a tight bounding box but may be spread out through space. However, in Blender, these are still rendered as dense volumes which is not ideal for performance and memory usage. This will be improved in future releases.

OpenVDB files can also store level sets and points. While level set grids can be read, there is no current support for rendering them as surfaces. Importing OpenVDB points is not supported.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/object/introduction.html

**Contents:**
- Introduction¶

The geometry of a scene is constructed from one or more objects. These objects can range from lights to illuminate your scene, basic 2D and 3D shapes to fill it with models, armatures to animate those models, to cameras to take pictures or make video of it all.

Each Blender object type (mesh, light, curve, camera, etc.) is composed from two parts: an Object and Object Data (sometimes abbreviated to “ObData”):

Holds information about the position, rotation and size of a particular element.

Holds everything else. For example:

Store geometry, material list, vertex groups, etc.

Store focal length, depth of field, sensor size, etc.

Each object has a link to its associated object-data, and a single object-data may be shared by many objects.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/animation/introduction.html

**Contents:**
- Introduction¶
- Animating with Grease Pencil¶
- 2D Traditional Animation¶
  - Keyframes¶
  - Onion Skinning¶
- Animation Options¶
  - Draw Mode¶
  - Edit Mode¶
- Examples¶
  - Traditional Animation¶

The main goal of Grease Pencil is to offer a 2D animation tool full immersed in a 3D environment.

Sample animation showing Grease Pencil object keyframes in the Dope Sheet with onion skinning enabled.¶

In Blender, Grease Pencil objects can be animated in many ways:

Changing their position, orientation or size in time;

Drawing one frame at a time (traditional animation).

Animating their points;

Causing the object to move based on the movement of another object (e.g. its parent, hook, armature, etc.). Useful for cut-out animation for example.

For a complete overview of animation in Blender please refer to the Animation & Rigging chapter.

Traditional animation in Grease Pencil is achieved with the use of keyframes that hold the strokes information at a particular frame or frame range.

With Auto keyframe activated, every time you create a stroke in Grease Pencil object Draw Mode a new keyframe is added at the current frame on the active channel. With Auto keyframe deactivated, you will have to add manually a new keyframe or your new strokes will be added on the active keyframe.

See Keyframe Editing for more information.

The channels in the Dope Sheet correspond to the active 2D layer of the Grease Pencil object.

Grease Pencil has its own mode in the Dope Sheet to work with keyframes. See Grease Pencil mode in the Dope Sheet section for more information. There are also several tools on the Stroke menu to work with keyframes and strokes. See Animation tools for more information.

One key element in traditional animation is the use of onion skinning. Grease Pencil offer a lot of flexibility and options for this tool. See Onion Skinning for more information.

In Draw Mode there are three options related to the animation workflow that you can use.

General drawing/animation options.¶

When enabled, new strokes weight data is added according to the current vertex group and weights. If there is no vertex group selected, no weight data is added.

This is useful for example in cut-out animation for adding new drawing on the same vertex group without the need to creating it afterwards.

See Weight Paint Mode for more information.

When creating new frames, the strokes from the previous/active frame are include as a basis for the new one.

If you need to add new strokes to your animation on several frames you can use multiframe drawing.

You can activate multiframe drawing with the Multiframe button next to the modes selector (faded lines icon). See Multiframe for more information.

In Edit Mode there is an option related to the animation workflow that you can use.

Sometimes you may need to modify several frames at the same time with edit tools, for example to repositioning drawings in an animation.

You can activate multiframe editing with the Multiframe button next to the modes selector (faded lines icon). See Multiframe for more information.

This example shows you how to animate a bouncing ball with a traditional 2D animation technique and Grease Pencil.

First, go to menu File ‣ New ‣ 2D Animation to start with a new 2D animation template. The template is ready to quick start your animation with a Grease Pencil object already created, Onion Skinning activated, Auto Keyframe enabled and in camera view.

Set the range of the animation in the Timeline from 1 to 24.

In the 3D Viewport draw a ball on the upper left corner with the Draw Tool (extreme).

Move to frame 12 and draw a squashed ball in the bottom center (breakdown).

Move to frame 24 and draw a ball in the top right corner of the 3D Viewport (extreme).

Keep drawing all the in-between frames you want using the onion skinning ghost as a reference.

To test the animation, press Spacebar to play.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/uv/introduction.html

**Contents:**
- Introduction¶
- UVs Explained¶
  - Example¶
- Interface¶
  - Header¶

The UV Editor is used for editing UV maps, which describe how a 2D image should be mapped onto a 3D object.

UV Editor with a UV map and a test grid texture.¶

Image textures are typically needed when the desired look is hard to achieve with procedural textures, or if the texture is not uniform. For example, a car would only have scratches in a few places where they make sense, not in random places all over its body.

Blender offers a number of projections (Box, Sphere…) that automatically apply a 2D image to a 3D object, but these tend to only work for simple meshes. For more complex ones, you need to create a UV map instead. This is a flat area where each face of the 3D object is laid out on the 2D image, specifying which part of the image it should be textured with. This gives you complete control over the mapping process.

The name “UV” refers to the axes of the map: U for horizontal, V for vertical. These letters were chosen to avoid confusion with “X” and “Y”, which refer to axes in 3D space instead.

The best analogy to understand UV mapping is cutting up a cardboard box. If you were to take a pair of scissors and cut along its edges, you would be able to spread it out flat on a tabletop. As you are looking down at the table, we could say that U is the left-right direction, and V is the up-down direction.

As a next step, you could put the spread-out box on top of a poster, cut the poster to match its shape, glue the poster to the box, and finally reassemble the box. You now have a 3D box textured with a 2D image.

A UV map thus describes how the mesh’s faces are laid out on the texture. You have complete freedom in how to do this: if you wanted to, you could cut each face loose and position, rotate, scale, and even skew it on the texture independently of the others. What’s more, faces can overlap in the UV map, making them share the same part of the texture.

3D space (XYZ) versus UV space.¶

In the above image, a dome in 3D space is flattened into a disc in UV space. Each 3D face is then textured with the part of the image it covers in the UV map.

The image also demonstrates a common problem in UV maps: distortion. Notice how, even though the checkered squares in the 2D texture are all the same size, they get different sizes when applied to the 3D dome (they’re smaller at the base than at the top). This is because the faces in the UV map have different relative sizes than in 3D space, which is a result of the flattening process.

You’ll typically want to minimize this distortion by manually guiding and tweaking the flattening, using seams for example. However, it’s not always possible to eliminate it completely.

The header contains several menus and options for working with UVs.

Synchronizes the selection between the UV Editor and the 3D Viewport. See Sync Selection for more details.

The UV element type to select. See Selection Mode for more details.

Which other vertices to select automatically. See Sticky Selection Mode for more details.

Tools for controlling how the content is displayed in the editor. See Navigating.

Tools for selecting UVs.

Tools for opening and manipulating images. See Editing Images.

Contains tools for Unwrapping Meshes and Editing UVs.

See Transform Pivot Point.

See Proportional Editing.

A data-block menu used for selecting images. When an image has been loaded or created in the UV Editor, the Image panel appears in the Sidebar region.

When enabled the current image remains visible regardless of the object selection. This switching only happens if the 3D Viewport is in Edit Mode or Texture Paint Mode.

This can be useful to enable when an image is used as a reference.

Lets you show/hide all gizmos using the toggle button, or specific gizmos using the drop-down arrow.

Enable/disable the gizmos used to pan or zoom the 2D viewport. See Navigation Gizmos for more information.

Lets you show/hide all overlays using the toggle button, or specific overlays using the drop-down arrow. See UV Overlays.

Select which UV map to use.

Select what color channels are displayed.

Enables transparency and shows a checkerboard behind the image.

Displays the colored image, without alpha channel.

Displays the alpha channel as a grayscale image. White areas are opaque, black areas are transparent.

Displays the depth from the camera, from Clip Start to Clip End, as specified in the Camera settings.

Single color channel visualized as a grayscale image.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/introduction.html

**Contents:**
- Introduction¶
- Adding & Removing Constraints¶
- Visual Transform¶

Constraints are a way of automatically controlling the location, rotation, and scale of an object or bone. For example, they can attach a sword to a knight’s hand, or make a tennis player’s eyes point towards the ball.

Each object or bone can have a stack of constraints that’s evaluated from top to bottom. In addition, each constraint has an Influence factor for weakening it or mixing it with other constraints. What’s more, this Influence can be keyframed, which makes it possible to turn constraints on and off over the course of an animation.

To add a constraint, click on Add Object/Bone Constraint in the Properties Editor and choose a constraint type.

To remove a constraint, click its button.

To move a constraint to a different position in the stack, drag its handle .

The Constraints menu in the 3D Viewport offers further options such as copying constraints and deleting all constraints in one go. The Track menu allows quickly adding a “track” (point at) constraint.

Constraints give their owning object or bone a new location, rotation, and/or scale which together are called the visual transform. This transform is separate from the “base” transform found in the Transform panel of the Properties Editor, and as its name implies, it determines where the owner really appears in the world.

For example, even when an object’s Transform panel still shows the original Location of (0, 0, 0), a constraint could have placed it somewhere else entirely. What’s more, attempting to move or even animate that object won’t work: its Location numbers will change, but visually, it will remain stuck in place. The only way to “free” the object is to disable or delete the constraint, or to set its Influence to zero.

Of course, transform properties that are not constrained can still be changed as usual.

While the visual transform is not shown in the UI, it can be copied to the base transform:

By running Apply Visual Transform.

By applying the constraint. This also deletes the constraint.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/transform/introduction.html

**Contents:**
- Introduction¶
- Operators¶
  - Move¶
  - Rotate¶
  - Scale¶
  - Align to View¶
  - Mirror¶

Transform is the modality of operations that perform transformations in 2D and 3D elements. Transformations can include things like moving, rotating, scaling, and applying other operations to objects in the scene.

They work by changing the geometry which you can edit directly.

There are several transformation operations included in Blender. Here are some of the main operations available:

This operations allows you to move elements along the X, Y, and Z axes in the scene.

You can use this function to rotate elements around the X, Y, and Z axes.

Scaling allows you to increase or decrease the size of an object along the X, Y, and Z axes.

This is useful for aligning objects with the view from the camera or another specific viewpoint.

Mirrors objects along one or more axes.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/selecting/introduction.html

**Contents:**
- Introduction¶
- Selection Modes¶
  - Multiple Selection Modes¶
  - Switching Select Mode¶
    - Expand/Contract Selection¶
- X-Ray¶
- Select Menu¶
- Known Issues¶
  - Dense Meshes¶
  - N-Gons in Face Select Mode¶

There are many ways to select elements, and it depends on what Mesh Select Mode you are in as to what selection tools are available. First we will go through these modes and after that a look is taken at basic selection tools.

3D Viewport Header ‣ Select Mode

1, 2, 3 (Shift Multiple Selection Modes, Ctrl Expand/Contract Selection).

In Edit Mode there are three different selection modes. You can enter the different modes by selecting one of the three buttons in the header.

Edit Mode selection buttons from right to left: Vertex, Edge, Face.¶

In this mode vertices are shown as points. Selected vertices are displayed in orange, unselected vertices in black, and the active or last selected vertex in white.

In this mode the vertices are not shown. Instead the selected edges are displayed in orange, unselected edges black, and the active or last selected edge in white.

In this mode the faces are displayed with a selection point in the middle which is used for selecting a face. Selected faces and their selection point are displayed in orange, unselected faces are displayed in black, and the active or last selected face is highlighted in white.

When using these buttons, you can make use of modifier keys, see: Switching Select Mode.

Almost all tools are available in all three mesh selection modes. So you can Rotate, Scale, Extrude, etc. in all modes. Of course rotating and scaling a single vertex will not do anything useful (without setting the pivot point to another location), so some tools are more or less applicable in some modes.

See Fig. Selection modes. for examples of the different modes.

By holding Shift-LMB when selecting a selection mode, you can enable multiple Selection Modes at once. This allows you to quickly select vertices, edges, or faces, without first having to switch mode.

Vertex mode example.¶

When switching modes in an “ascendant” way (i.e. from simpler to more complex), from Vertices to Edges and from Edges to Faces, the selected parts will still be selected if they form a complete element in the new mode.

For example, if all four edges in a face are selected, switching from Edges mode to Faces mode will keep the face selected. All selected parts that do not form a complete set in the new mode will be unselected.

Edge mode, the initial selection.¶

Switching to Face mode.¶

Hence, switching in a “descendant” way (i.e. from more complex to simpler), all elements defining the “high-level” element (like a face) will be selected (the four vertices or edges of a quadrangle, for example).

By holding Ctrl when selecting a higher selection mode, all elements touching the current selection will be added, even if the selection does not form a complete higher element. Or contracting the selection when switching to a lower mode.

Vertex mode, the initial selection.¶

Expanding to Edge mode.¶

The X-Ray setting is not just for shading, it impacts selection too. When enabled, selection isn’t occluded by the objects geometry (as if the object was solid).

Selects all the geometry that is not selected, and deselect currently selected components.

Interactive box selection.

Interactive circle selection.

Interactive free-form selection.

Select mesh items at the mirrored location across the chosen axis.

Selects a random group of vertices, edges, or faces, based on a percentage value.

Deselect alternate elements relative to the active item.

Expands the selection to the adjacent elements of the selection type.

Contracts the selection from the adjacent elements of the selection type.

This uses selection history to select the next vertex, edge, or face based on surrounding topology.

Select previous just removes the last selected element.

Select elements similar to the current selection.

Select geometry by querying its characteristics.

Selects all components that are connected to the current selection.

Path between two selected elements.

Select connected faces based on a threshold of the angle between them. This is useful for selecting faces that are planar.

Select connected edges.

Select connected faces.

Select connected edge ring.

This tool selects all edges between two faces forming an angle greater than the angle value, where an increasing angle selects sharper edges.

Selects all vertices on the mesh in a single axis relative to the active vertex. In Vertex selection mode only.

Selecting dense meshes with X-Ray disabled, has a limitation where dense meshes may not have all the elements selected. When selecting regions with Box, Circle and Lasso select, vertices may overlap each other causing some vertices not to be selected. This is a limitation with the current selection method, you may workaround this by zooming in or enabling X-Ray.

N-gon face having its center dot inside another face.¶

As already noted, in X-Ray and Wireframe mode faces are marked with a dot in the middle. With n-gons that can lead in certain cases to a confusing display. The example shows the center dot of the U-shaped n-gon being inside of the oblong face inside the “U”. It is not easy to identify which dot belongs to which face (the orange dot in the image is the object origin).

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/introduction.html

**Contents:**
- Introduction¶
- Typical Scenarios for using Soft Bodies¶
- Creating a Soft Body¶
- Interaction in Real-Time¶
- Tips¶

Soft body simulation is used for simulating soft deformable objects. It was designed primarily for adding secondary motion to animation, like jiggle for body parts of a moving character.

It also works for simulating more general soft objects that bend, deform and react to forces like gravity and wind, or collide with other objects.

While it can simulate cloth and other stiff types of deformable objects to an extent, the Cloth Simulation can do it better with a solver specifically designed for this purpose.

The simulation works by combining existing animation on the object with forces acting on it. There are exterior forces like gravity or force fields and interior forces that hold the vertices together. This way you can simulate the shapes that an object would take on in reality if it had volume, was filled with something, and was acted on by real forces.

Soft bodies can interact with other objects through Collision. They can interact with themselves through Self-Collision.

The result of the soft body simulation can be converted to a static object. You can also bake edit the simulation, i.e. edit intermediate results and run the simulation from there.

The wind cone is a soft body, as the suspension.¶

Soft bodies are well suited for:

Jiggle on moving characters.

Elastic and deformable objects made of materials like rubber or gelatin.

Tree branches moving in the wind, swinging ropes, and the like.

Flags, wide sleeves, cushions or other simple fabric reacting to forces.

Soft body simulation works for all objects that have vertices or control points (meshes, curves, surfaces, and lattices).

To add a soft body simulation to an object, go to the Physics tab in the Properties and activate the Soft Body button. For a reference of all the settings see this page.

You start a soft body simulation by playback animation with Alt-A, and stop the simulation with Esc or Alt-A.

To work with a soft body simulation, you will find it handy to use the Timeline editor. You can change between frames and the simulation will always be shown in the actual state. You can interact in real-time with the simulation, e.g. by moving collision objects or shaking a soft body object.

You can then select the soft body object while running the simulation and Apply the modifier in the Modifiers tab of the Properties. This makes the deformation permanent.

Soft bodies work especially well if the objects have an even vertex distribution. You need enough vertices for good collisions. You change the deformation (the stiffness) if you add more vertices in a certain region.

The calculation of collisions may take a long time. If something is not visible, why calculate it?

To speed up the collision calculation it is often useful to collide with an additional, simpler, invisible, somewhat larger object.

Use soft bodies only where it makes sense. If you try to cover a body mesh with a tight piece of cloth and animate solely with soft body, you will have no success. Self-collision of soft body hair may be activated, but that is a path that you have to wander alone. We will deal with Collisions in detail later.

Try and use a Lattice or a Curve Guide soft body instead of the object itself. This may be magnitudes faster.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/texts/introduction.html

**Contents:**
- Introduction¶

Text objects contain some text, and are in the same object type family as curves and surfaces ones, as fonts are vector data (they are made of curves).

Blender uses a “Font System” to manage mapping letter codes to geometry representing them in the 3D Viewport. This font system has its own built-in font, but it can use external fonts too, including PostScript Type 1, OpenType and TrueType fonts. And moreover, it can use any objects existing in the current blend-file as letters.

An example of an extruded text.¶

Text objects allow you to create and render 2D or 3D text, with various advanced layout options, like justifying and frames. By default, letters are just flat filled surfaces, exactly like any closed 2D curve. But, just like curves, you can extrude them, and apply modifiers to them (e.g. to make them follow a curve).

Text in Blender can be laid out in some relatively advanced ways, defining columns or blocks of text, using different alignments, and so on.

Those features are similar in concept to what you can find in DTP software (like Scribus), although at a very basic level currently.

You can convert a text object, either to a curve, or directly to a mesh, using Convert in Object Mode.

A maximum of 50,000 characters is allowed per text object. However, be forewarned that the more characters a single text object has, the slower the object will respond interactively.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/introduction.html

**Contents:**
- Introduction¶
- Your First Armature¶
- The Armature Object¶

An armature in Blender can be thought of as similar to the armature of a real skeleton, and just like a real skeleton an armature can consist of many bones. These bones can be moved around and anything that they are attached to or associated with will move and deform in a similar way.

An “armature” is a type of object used for rigging. A rig is the controls and strings that move a marionette (puppet). Armature object borrows many ideas from real-world skeletons.

In order to see what we are talking about, let us try to add the default armature in Blender.

(Note that armature editing details are explained in the armatures editing section.)

Open a default scene, then:

Delete all objects in the scene.

Make sure the cursor is in the world origin with Shift-C.

Press Numpad1 to see the world in Front view.

Add a Single Bone (Add ‣ Armature).

Press NumpadPeriod to see the armature at maximum zoom.

The default armature.¶

As you can see, an armature is like any other object type in Blender:

It has an origin, a position, a rotation and a scale factor.

It has an Object Data data-block, that can be edited in Edit Mode.

It can be linked to other scenes, and the same armature data can be reused on multiple objects.

All animation you do in Object Mode is only working on the whole object, not the armature’s bones (use the Pose Mode to do this).

As armatures are designed to be posed, either for a static or animated scene, they have a specific state, called “rest position”. This is the armature’s default “shape”, the default position/rotation/scale of its bones, as set in Edit Mode.

In Edit Mode, you will always see your armature in rest position, whereas in Object Mode and Pose Mode, you usually get the current “pose” of the armature (unless you enable the Rest Position button of the Armature panel).

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/configuration/introduction.html

**Contents:**
- Introduction¶
- Auto-Save Preferences¶
- Language¶
- Input¶
- File and Paths¶
- Save & Load¶

Here are some preferences that you may wish to set initially. See the section Preferences for the complete list of available settings. The shortcut Ctrl-Comma can be used to quickly open the Preferences editor.

By default, a new Blender installation is set to auto-save changes to preferences, so you don’t accidentally lose a change you have made. To disable this behavior, perform these steps:

Open the Preferences dialog

Click on the small menu at the lower left (shown by 3 lines)

Uncheck the box next to “Auto-Save Preferences”

Click the “Save Preferences” button that will appear in the lower left of the dialog. Don’t forget this step, as the change will not be saved otherwise.

To enable auto-save once again, simply follow steps 1-3 above and check the box in step 3.

Enable Edit ‣ Preferences ‣ Interface ‣ Translation, and choose the Language and what to translate from Interface, Tooltips and New Data.

See Language for details.

If you have a compact keyboard without a separate number pad, enable Preferences ‣ Input ‣ Keyboard ‣ Emulate Numpad. This gives you the 3D view shortcuts regularly used on the number pad.

If you do not have a middle mouse button, you can enable Preferences ‣ Input ‣ Mouse ‣ Emulate 3 Button Mouse. This allows you to hold the Alt or OSKey key while dragging with the mouse, to orbit.

See Configuring Peripherals for more information about these options, and see Input Preferences for details on configuring their settings.

At Preferences ‣ File Paths you can set options such as what Image Editor (GIMP, Krita…) and Animation Player to use.

The Temporary Directory sets where to store files such as temporary renders and auto-saves.

The // at the start of each path in Blender means the directory of the currently opened blend-file, used to reference relative paths.

See File Preferences for details.

If you trust the source of your blend-files, you can enable Auto Run Python Scripts. This option is meant to protect you from malicious Python scripts in blend-files that you got from someone else. Many users turn this option on, as advanced rigs tend to use scripts of some sort. Use caution, as this is a global setting, and may allow potentially malicious Python code from an untrusted source to run.

See Save & Load Auto Run Python Scripts Preference.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/editing/introduction.html

**Contents:**
- Introduction¶
- Basic Posing¶

In Pose Mode, bones behave like objects. So the transform actions (move, rotate, scale, etc.) are very similar to the same ones in Object Mode (all available ones are regrouped in the Pose ‣ Transform submenu). However, there are some important specifics:

Bones’ relationships are crucial (see Bone Parenting).

The “transform center” of a given bone (i.e. its default pivot point, when it is the only selected one) is its root. Note by the way that some pivot point options seem to not work properly. In fact, except for the 3D Cursor one, all others appear to always use the median point of the selection (and not e.g. the active bone’s root when Active Object is selected, etc.).

As previously noted, bones’ transformations are performed based on the Rest Position of the armature, which is its state as defined in Edit Mode. This means that in rest position, in Pose Mode, each bone has a scale of 1.0, and null rotation and position (as you can see it in the Transform panel, in the 3D Viewport’s Sidebar).

An example of a rotation locked to the local Y axis, with two bones selected.¶

Note that the two green lines materializing the axes are centered on the armature’s center, and not each bone’s root…

Moreover, the local space for these actions is the bone’s own one (visible when you enable the Axes option of the Armature panel). This is especially important when using axis locking, for example, there is no specific “bone roll” tool in Pose Mode, as you can rotate around the bone’s main axis just by locking on the local Y axis R Y Y… This also works with several bones selected; each one is locked to its own local axis!

When you pose your armature, you are supposed to have one or more objects skinned on it! And obviously, when you transform a bone in Pose Mode, its related objects or object’s shape is moved/deformed accordingly, in real-time. Unfortunately, if you have a complex rig set-up and/or a heavy skin object, this might produce lag during interactive editing. If you experience such troubles, try enabling the Delay Deform button in the Armature panel the skin objects will only be updated once you confirm the transform operation.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/edit/introduction.html

**Contents:**
- Introduction¶
- Accessing Stroke Editing Tools¶
  - Toolbar¶
  - Menus¶
  - Context Menu¶

Blender provides a variety of tools for editing Grease Pencil strokes. These are tools used to add, duplicate, move and delete elements.

Editing multiple Grease Pencil objects at once is currently not supported.

These are available through the different tools in the Toolbar, the Stroke menu in the 3D Viewport header, and context menus in the 3D Viewport, as well as individual shortcut keys.

When you select a stroke and Tab into Edit Mode, the Toolbar changes from Object Tools to Stroke editing Tools. These are only some of the stroke editing tools.

The Stroke Menu is located in the header.

RMB brings up the complete Stroke Menu.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/sculpting/introduction.html

**Contents:**
- Introduction¶
- Sculpt Mode¶
- Sculpting Options¶
- Auto-Masking¶
- Keyboard Shortcuts¶

Sculpt Mode is similar to Edit Mode in that it is used to alter the shape of a drawing, but Sculpt Mode uses a very different workflow: Instead of dealing with individual elements (points and edit lines), an area of the model is altered using a brush. In other words, instead of selecting a group of points, Sculpt Mode manipulates the drawing in the brush region of influence.

3D Viewport Mode selector: Sculpt Mode.¶

Sculpt Mode is selected from the Mode menu in the 3D Viewport header. Once Sculpt Mode is activated, the Toolbar of the 3D Viewport will change to Sculpt Mode specific panels. A red circle will appear and follow the location of the cursor in the 3D Viewport.

Sculpt Mode in Grease Pencil allows you to select points or strokes to restrict the effect of the sculpting tools to only a certain areas of your drawing.

You can use the selection tools in the Toolbar for a quick selection. You can restrict sculpting only on the selected points or strokes with the Selection mode buttons. The three modes can be toggled with 1, 2, or 3 respectively.

Sometimes you may need to modify several frames at the same time with the sculpting tools.

You can activate multiframe editing with the Multiframe button next to the modes selector (faded lines icon). See Multiframe for more information.

Header ‣ Auto-Masking

Auto-Masking settings.¶

These properties automatically mask geometry based on stroke, layers and materials under the cursor. It’s an quick alternative to frequent manual masking. These masks are initialized on every new tool usage. They are also never visible as an overlay.

These properties can be accessed via a Pie Menus by pressing Shift-Alt-A.

All auto-masking modes can be combined, which makes the generated auto-mask more specific. For example it’s possible to auto-mask strokes that use specific layer and material while excluding others.

Only strokes that are under the cursor when you started the tool are affected.

Only strokes on the same layers that are under the cursor when you started the tool are affected.

Only materials with the same material that are under the cursor when you started the tool are affected.

Only the strokes on the active layer are affected.

Only the strokes with the active material are affected.

Invert stroke toggle Ctrl

Change active material U

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/draw/introduction.html

**Contents:**
- Introduction¶
- Strokes Location & Orientation Controls¶
  - Stroke Placement¶
  - Drawing Planes¶
- Drawing Options¶

Draw Mode is the mode in Grease Pencil that allows you to draw in the 3D Viewport. This mode is actually the only one in which new strokes can be created.

Already made strokes can not be selected in Draw Mode, for editing strokes you must use the Edit Mode or Sculpt Mode.

3D Viewport Mode selector: Draw Mode.¶

Draw Mode is selected with the Mode menu in the 3D Viewport header. Once Draw Mode is activated, the Toolbar of the 3D Viewport will change to Draw Mode specific panels. Also a circle with the same color as the active material will appear and follow the location of the cursor in the 3D Viewport.

To create new strokes you have to select one of the drawing tools in the Toolbar. The most common one is the Draw tool for free-hand drawings but there are many other tools for drawing, filling areas and erasing strokes. There are also some tools to create primitives shapes like lines, arcs, curves, boxes and circles.

See Toolbar for more details.

Drawing in a 3D space is not the same as drawing on a flat canvas. When drawing with Grease Pencil you have to define the location and orientation of the new strokes in the 3D space.

3D Viewport header Controls for strokes.¶

The Stroke Placement selector defines the new strokes location in 3D space.

See Stroke Placement for more information.

The Drawing Planes selector defines the plane (orientation) to which the new strokes will be restricted.

See Drawing Planes for more information.

General drawing options.¶

Allows to draw on several frames at the same time.

See Multiframe for more information.

When creating new frames adding strokes with drawing tools, the strokes from the previous/active frame are include as a basis for the new one. When erasing existing strokes using Additive Drawing a new keyframe will be added.

Joins new strokes with the beginning or end of previously drawn strokes in the active layer.

When enabled, weight data is added to new strokes according to the current vertex group and weight. If there is no vertex group selected, no weight data is added.

Useful for example in cut-out animation for adding new drawing on the same vertex group without the need to creating it afterwards.

See Weight Paint Mode for more information.

When enabled, new strokes are drawn below of all strokes in the layer. For example when you want to paint with a fill material below line strokes on a character and they are on the same layer.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/weight_paint/introduction.html

**Contents:**
- Introduction¶
- Weight Paint¶
- Weight Options¶

Assigning weight to the points is primarily used for rigging strokes in cut-out animation, where the vertex groups are used to define the relative bone influences on the strokes. See Using Vertex Group for more information.

A vertex in Grease Pencil is called point. Point and vertex names are equivalent.

Weight Painting is a method to maintain large amounts of weight information in an intuitive way. The selected Grease Pencil object is displayed slightly shaded with a rainbow color spectrum. The color visualizes the weights associated to each point in the active vertex group. By default blue means unweighted and red means fully weighted.

You assign weights to the points of the object by painting on it with weight brushes. Starting to paint on a strokes automatically adds weights to the active vertex group (a new vertex group is created if needed).

3D Viewport Mode selector: Weight Paint Mode.¶

Weight Paint Mode is selected from the Mode menu in the 3D Viewport header. Once Weight Paint Mode is activated, the Toolbar of the 3D Viewport will change to Weight Paint Mode specific panels. A red circle will appear and follow the location of the cursor in the 3D Viewport.

Sometimes you may need to assign weight to several frames at the same time with the Weight Paint tools.

You can activate multiframe editing with the Multiframe button next to the modes selector (faded lines icon). See Multiframe for more information.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/uv/unwrapping/introduction.html

**Contents:**
- Introduction¶
- About UVs¶
- Getting Started¶
  - Workflow¶

The first step is to unwrap your mesh. Generally, it is recommended to start unwrapping when only minor adjustments to the geometry of your model are required. If you do add faces or subdivide existing faces when a model is already unwrapped, Blender will add those new faces for you, but you may need to do additional mapping or editing. In this fashion, you can use the UV texture image to guide additional geometry changes.

Every point in the UV map corresponds to a vertex in the mesh. The lines joining the UVs correspond to edges in the mesh. Each face in the UV map corresponds to a mesh face. Think of a UV map as projecting the surface of your 3D model onto a 2D image.

Each face of a mesh can have many UV textures. Each UV texture can have an individual image assigned to it. When you unwrap a face to a UV texture in the UV Editor, each face of the mesh is automatically assigned four UV coordinates: These coordinates define the way an image or a texture is mapped onto the face. To distinguish from XYZ coordinates, the U and V axes are used to mark the coordinates of each point. Hence the name, UV unwrapping. These coordinates can be used for rendering or for real-time viewport display as well.

Every face in Blender can have a link to a different image. The UV coordinates define how this image is mapped onto the face. This image then can be rendered or displayed in real-time. A 3D Viewport has to be in “Face Select” mode to be able to assign Images or change UV coordinates of the active mesh object. This allows a face to participate in many UV textures. A face at the hairline of a character might participate in the facial UV texture, and in the scalp/hair UV texture.

These are described more fully in the next sections.

Default UV editing workspace.¶

By default, meshes are not created with UVs. First you must map the faces, then you can edit them. The process of unwrapping your model is done within Edit Mode in the 3D Viewport. This process creates one or more UV Islands in the UV Editor.

To begin, choose the UV Editing workspace from the selection list at the top of your screen in the Preferences header. This sets one of the areas to show you the UV Editor, and the other area to the 3D Viewport.

Enter Edit Mode, as all unwrapping is done in Edit Mode. You can be in vertex, face, or edge selection mode.

The general workflow is as follows, but know that different models may require different approaches to unwrapping:

Mark Seams if necessary. See more about marking seams.

Select mesh faces in the 3D Viewport.

Select a UV mapping method from the UV ‣ Unwrap menu or the UV menu in the 3D Viewport.

Adjust the unwrap settings in the Adjust Last Operation panel.

Add a test image to see if there will be any distortion. See Applying Images to UVs.

Adjust UVs in the UV editor. See Editing UVs.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/brush/introduction.html

**Contents:**
- Introduction¶
- Accessing Brushes¶
- Brush Control¶
- Custom Brush Shortcuts¶
- Brush Assets¶
- Brush Tool¶

Brushes are the main way of interacting with any painting and sculpting mode. By click & dragging in the 3D Viewport (or the Image Editor when using Texture Paint), the active brush creates a stroke with a certain effect, depending on the used brush settings. Brushes are used as brush assets and stored in asset libraries, which makes it easy to reuse and share them. Typically they have a preview image and a name that indicate the effect they create.

It is highly recommended to use a Graphics Tablet for a better brush feel and additional features.

In modes that use painting or sculpting functionality, the Asset Shelf of the 3D Viewport and Image Editor displays brush assets that can be used in that mode. Clicking a brush asset will activate the Brush Tool if necessary, with the clicked brush set.

The Asset Shelf of the 3D Viewport, providing access to brush assets.¶

This asset shelf is also available as popup in the Tool Settings, the Sidebar, Properties and using a shortcut.

Sidebar ‣ Tool ‣ Brush Asset, Properties ‣ Tool ‣ Brush Asset

These are the most common hotkeys for controlling the brush.

Set brush strength Shift-F

Rotate brush texture / Set brush weight Ctrl-F

After pressing these hotkeys, you can then either adjust the value interactively or by typing in numbers. Move the mouse right or left to increase/reduce the value (additionally with precision (Shift) and/or snapping (Ctrl) activated). Finally confirm (LMB, Return) or cancel (RMB, Esc).

You can also invert the brush direction/effect by holding Ctrl.

To give a brush a shortcut, simply right click it in the asset shelf or brush selector popup, and select Assign Shortcut. To modify or remove an existing shortcut, select Change Shortcut or Remove Shortcut accordingly.

Brushes are used as assets, and stored in asset libraries. This makes the brushes shared across project files. All available brush assets can be displayed in the Asset Browser, which also provides ways to organize them.

Blender comes bundled with a number of brushes in the Essentials asset library. These can be customized into all kinds of custom brushes by duplicating them (see Brush Editing).

While it’s possible to have brush data-blocks that are local to the file and not marked as assets, such brushes cannot be activated for actual painting or sculpting. Use the Mark as Asset operator to make them brush assets that can be activated.

Painting or sculpting with brushes requires the brush tool to be active. Activating a brush from an asset shelf or brush selector also activates the brush tool for convenience.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/constraints/introduction.html

**Contents:**
- Introduction¶
- Connect¶
- Physics Menu¶
- Common Options¶
  - Settings¶
  - Limits¶
  - Objects¶
  - Override Iterations¶

Constraints (also known as joints) for rigid bodies connect two rigid bodies. The physics constraints are meant to be attached to an Empty object. The constraint then has fields which can be pointed at the two physics-enabled object which will be bound by the constraint. The empty object provides a location and axis for the constraint distinct from the two constrained objects. The location of the entity hosting the physics constraint marks a location and set of axes on each of the two constrained objects. These two anchor points are calculated at the beginning of the animation and their position and orientation remain fixed in the local coordinate system of the object for the duration of the animation. The objects can move far from the constraint object, but the constraint anchor moves with the object. If this feature seems limiting, consider using multiple objects with a non-physics Child of constraint and animate the relative location of the child.

The quickest way to constrain two objects is to select both and click the Connect button in Object ‣ Rigid Body. This creates a new empty object (named “Constraint”) with a physics constraint already attached and pointing at the two selected objects.

Also you can create Rigid Body Constraint on one of the two constrained objects with Rigid Body Constraint button of the Physics tab in the Properties. This constraint is dependent on the object location and rotation on which it was created. This way, there are no empty object created for the constraint. The role of the empty object is put on this object. The constrained object can be then be set as a Passive type for better driving of the constraint.

Additional parameters appear in the Rigid Body Constraint panel of the Physics tab in the Properties for the selected empty object or the one of the two constrained objects with the created constraint.

Physics ‣ Rigid Body Constraint

Specifies whether the constraint is active during the simulation.

Allows constrained objects to pass through one another.

Allows constraint to break during simulation. Disabled for the Motor constraint. This can be used to simulate destruction.

Impulse strength that needs to be reached before the constraint breaks.

By using limits you can constrain objects even more by specifying a translation/rotation range on/around respectively one axis (see below for each one individually). To lock one axis, set both limits to 0.

First object to be constrained.

Second object to be constrained.

Allows making constraints stronger (more iterations) or weaker (less iterations) than specified in the rigid body world.

Number of constraint solver iterations made per simulation step for this constraint.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/curves_sculpting/introduction.html

**Contents:**
- Introduction¶
- Curves Menu¶
- Selection Modes¶
- Select Menu¶
- Controls¶
- Display¶
  - Overlays¶

Curves Sculpt Mode allows working with curves using various brushes. It is commonly used for hair grooming, but can be used with all kinds of curves.

The curves’ surface object plays an important role in many curves sculpting brushes. Most brushes such as Add Curves require the surface to be set already.

Curves Sculpt tools only use the original mesh of the surface object and don’t take its modifiers into account.

Re-attach curves to a deformed surface using the existing attachment information. This only works when the topology of the surface mesh has not changed.

Find the closest point on the surface for the root point of every curve and move the root there. This needs to be run after the surface mesh topology changed

Add a new hair particle system, or update an system on the surface object. The operator is used for backwards compatibility with the old hair type particle system.

3D Viewport Header ‣ Select Mode

Selection modes limits selection operators to certain curve domains. This feature is makes it easy to select whole segments at once, or to give more granular control over editing.

Allows selection of individual control points.

Limits selection to whole curve segments.

Select all control points or curves.

Deselect all control points or curves.

Invert the selection.

Randomizes inside the existing selection or create new random selection if nothing is selected already.

Select endpoints of curves. Only supported in the Control Point selection mode.

Number of points to select from the front or back of the curve.

Select points or curves which are close to already selected elements.

Sculpt mode provides several properties that give advanced control of the tool’s behavior. These options can be found in the right-hand side of the 3D Viewport’s Header.

Allows tools to affect curves symmetrically according to the chosen axis.

Prevents the curve segments from passing through the Surface Object.

Shows the original curves that are currently being edited which is useful with when procedural deformations or child curves are used.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/physics/fluid/introduction.html

**Contents:**
- Introduction¶
- Liquid Simulations¶
- Gas Simulations¶
- Workflow¶

Fluid physics are used to simulate physical properties of liquids especially water. While creating a scene in Blender, certain objects can be marked to become a part of the fluid simulation. For a fluid simulation you have to have a domain to define the space that the simulation takes up. In the domain settings you will be able to define the global simulation parameters (such as viscosity and gravity).

Example of a liquid simulation.¶

Gas or smoke simulations are a subset of the fluids system, and can be used for simulating collections of airborne solids, liquid particulates and gases, such as those that make up smoke. It simulates the fluid movement of air and generates animated Voxel textures representing the density, heat, and velocity of other fluids or suspended particles (e.g. smoke) which can be used for rendering.

Example of a fire simulation.¶

Gases or smoke are emitted inside of a Domain from a mesh object or particle system. The smoke movement is controlled by airflow inside the domain, which can be influenced by Effector objects. Smoke will also be affected by the scene’s gravity and force fields. Airflow inside the domain can affect other physics simulations via the Fluid Flow force field.

At least a Domain object and one Flow object are required to create a fluid simulation.

Create a Domain object that defines the bounds of the simulation volume.

Set up Flow objects which will emit fluid.

Set up Effector objects to make the fluid interact with objects in the scene.

Assign a material to the domain object.

Bake the Cache for the simulation.

There are Quick Liquid and Quick Smoke tools which will automatically create a domain object with a basic liquid or smoke and fire material.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modifiers/introduction.html

**Contents:**
- Introduction¶
- Interface¶
  - Applying Modifiers¶
  - Influence Filters¶

Properties ‣ Modifiers

Grease Pencil has their own set of modifiers. Modifiers are automatic operations that affect an object in a non-destructive way. With modifiers, you can perform many effects automatically that would otherwise be too tedious to do manually and without affecting the base geometry of your object.

With Geometry Nodes, it is possible to create custom Grease Pencil modifiers.

They work by changing how an object is displayed and rendered, but not the geometry which you can edit directly. You can add several modifiers to a single object forming the modifier stack and Apply a modifier if you wish to make its changes permanent.

There are four types of modifiers for Grease Pencil:

These are tools similar to the Deform ones (see below), however, they usually do not directly affect the geometry of the object, but some other data, such as vertex groups.

The Generate group of modifiers includes constructive tools that either change the general appearance of or automatically add new geometry to an object.

The Deform group of modifiers only changes the shape of an object without adding new geometry,

The Color group of modifiers change the object color output.

Panel layout (Thickness modifier as an example).¶

Each modifier’s interface shares the same basic components like modifiers for meshes.

See Modifiers Interface for more information.

Applying a modifier makes the effects of the modifier “real”; converts the strokes to match the applied modifier’s results, and deletes the modifier.

When applying a modifier to an object that shares Object Data between multiple objects, the object must first be made a Single User which can be performed by confirming the pop-up message.

Applying a modifier that is not first in the stack will ignore the stack order (it will be applied as if it was the first one), and may produce undesired results.

Properties ‣ Modifiers ‣ Modifier Header ‣ Specials

Applies the modifier for the current keyframe.

Applies the modifier for all keyframes.

With Geometry Nodes it is possible to add new layers to the geometry. When applying, this will create a single keyframe on the first frame of evaluation. Layers with duplicated names in evaluated geometry will be deduplicated.

It is also possible to have layers with empty names. When applying these get renamed to Layer (and Layer.001 etc. when such a layer already exists in the original geometry).

Most Grease Pencil modifiers share a set of options that control where the modifier is applied. These filters restrict the modifier’s effect to specific layers, materials, or geometry components.

For each filter, you can invert the selection by clicking the (Invert) icon next to the control.

Restricts the effect to points or strokes of the specified layer. Alternatively, to filter by layer groups, click the icon.

Restricts the effect to points or strokes in layers with a matching Pass Index.

Restricts the effect to points or strokes using the specified material.

Restricts the effect to points or strokes whose material has a matching Pass Index.

Restricts the effect to points or strokes assigned to a specific vertex group.

When enabled, applies a custom falloff curve to control how the modifier’s influence varies along each stroke from start to end.

The availability of each filter depends on the specific modifier. Not all modifiers support all filters.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/drivers/introduction.html

**Contents:**
- Introduction¶
- Graph View¶
- Driver Configuration¶
- Notes on Scripted Expressions¶

Drivers are a way to control values of properties by means of a function, or a mathematical expression.

Effectively, drivers consist of:

A driver configuration that specifies zero, one, or more input values using other properties or object transformation channels, and combines them using a predefined mathematical function or a custom Python expression.

An animation F-Curve that maps the output of the driver configuration to the final value to apply to the driven property.

As an example, the rotation of Object 1 can be controlled by the scale of Object 2. It is then said that the scale of Object 2 drives the rotation of Object 1.

Not only can drivers directly set the value of a property to the value of a different one, they can also combine multiple values using a fixed function or a Python expression and further modulate it with a manually defined curve and/or a modifier stack.

Drivers are an extremely powerful tool for building rigs and are typically used to drive bone transforms and the influence of shape keys, action constraints and modifiers, often using custom properties as inputs.

Driver curve in the Drivers editor.¶

The main area of the Drivers editor shows an F-Curve that represents the driver function.

The X axis maps to the output value of the driver configuration. The units depend on the setup.

The Y axis shows the value applied to the target property. The units depend on the property.

In the example image, if the driver value is 2.0 the property value will be 0.5.

The default F-Curve is an identity map, i.e. the value produced by the driver configuration is applied to the driven property unchanged. If the driver output value is 2.0, the property will be 2.0.

The driver function can be defined artistically with Bézier curve handles or mathematically with trigonometric functions or polynomial expressions such as \(y = a + bx\). Furthermore, the function can also be procedurally modulated with noise or cyclic repetitions. See Modifiers for more details.

The Drivers panel shows the setup for a driver.

A driver can have zero, one, or more variables. Variables specify which properties, object transformation channels, or relative distances between objects, are used as inputs by the driver.

The driver type determines how the variables are used. The type can be:

a built-in function: for example, the sum of the variables’ values, or

a scripted expression: an arbitrary Python expression that refers to the variables by their names.

This driver configuration outputs a single value which changes when the variables change. This value is then evaluated through the driver function curve to produce the result to be applied to the driven property.

When a driver uses a Scripted Expression, Blender can evaluate it without using the fully featured Python interpreter if it is simple enough. This means that drivers are fast to evaluate with simple divisions, additions and other “simple” expressions. The built-in functions are always evaluated natively.

See Simple Expressions for a comprehensive list of expressions that can be evaluated natively.

When the expression is not simple, it will be evaluated using Python. As a consequence, the driver will be slower and there is a security risk if the author of the Python code is unknown. This is an important thing to take into consideration for heavy scenes and when sharing files with other people. See also: Auto run.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/clip/introduction.html

**Contents:**
- Introduction¶
- Header¶
  - Mode¶
  - View Type¶
  - View Menu¶
  - Select Menu¶
  - Clip Menu¶
  - Track Menu¶
  - Reconstruction Menu¶
  - Add Menu¶

The Movie Clip Editor is used for tracking and masking movies.

Movie Clip Editor interface.¶

The Movie Clip Editor header in Mask mode.¶

For placing markers in a video and tracking their movement.

For creating and animating masks.

The default view, for placing and tracking markers.

Plots the movement speed of the markers on a graph.

Shows an overview of marker keyframes on a timeline.

Show or hide the tab panel on the left for creating and manipulating markers and masks.

Show or hide the Sidebar.

Display a pop-up panel to alter the properties of the last completed operation.

Displays metadata encoded in the video, if available.

Zooms and pans the view so that the whole video is visible.

Zooms and pans the view to focus on the selected items.

Pans the view so that the 2D Cursor is in the center.

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

Area controls. See the user interface documentation for more information.

Menu for selecting markers and masks.

Menu for loading movie clips and creating proxies.

Menu for performing tracking operations.

Menu for setting up the reconstruction of 3D information from the tracked points in the 2D video.

Use to add primitive mask shapes.

Adds a circle-shaped mask.

Adds a square-shaped mask.

Menu for operators used to Edit masks.

A data-block menu used for loading and selecting movies. Both video files and image sequences can be used. When a movie clip is loaded into the Clip editor, extra panels are displayed in the interface.

See Proportional Editing.

A data-block menu for creating and selecting masks.

Automatically pans the view to follow the selected markers, so that they remain in the same location on screen during tracking and playback.

This option “locks the view onto the selection” and is not to be confused with the Lock option in the Sidebar, which instead prevents you from changing the active marker.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/physics/cloth/introduction.html

**Contents:**
- Introduction¶
- Workflow¶
- Springs¶

Cloth simulation is one of the hardest aspects of computer graphics, it is a deceptively simple real-world item that is taken for granted, but it actually has very complex internal and environmental interactions. Cloth is commonly modeled as 2D mesh to simulate real world objects such as fabrics, flags, banners. And yet cloth can also be used to model 3D objects such as teddy bears, pillows, balloons, or balls.

Cloth interacts with and is affected by other moving objects, the wind and other forces, as well as a general aerodynamic model, all of which is under your control.

Cloth on carved wooden men (made by motorsep).¶

Once Cloth physics have been added to a mesh, a Cloth Modifier will be added to the object’s modifier stack. As a modifier then, it can interact with other modifiers, such as Armature and Smooth. In these cases, the ultimate shape of the mesh is computed in accordance with the order of the modifier stack. For example, you should smooth the cloth after the modifier computes the shape of the cloth.

You can Apply the Cloth Modifier to freeze, or lock in, the shape of the mesh at that frame, which removes the modifier. For example, you can drape a flat cloth over a table, let the simulation run, and then apply the modifier. In this sense, you are using the simulator to save yourself a lot of modeling time.

Results of the simulation are saved in a cache, so that the shape of the mesh, once calculated for a frame in an animation, does not have to be recomputed again. If changes to the simulation are made, you have full control over clearing the cache and re-running the simulation. Running the simulation for the first time is fully automatic and no baking or separate step interrupts the workflow.

Computation of the shape of the cloth at every frame is automatic and done in the background; thus you can continue working while the simulation is computed. However, it is CPU-intensive and depending on the power of your PC and the complexity of the simulation, the amount of CPU needed to compute the mesh varies, as does the lag you might notice.

If you set up a cloth simulation but Blender has not computed the shapes for the duration of the simulation, and if you jump ahead a lot of frames forward in your animation, the cloth simulator may not be able to compute or show you an accurate mesh shape for that frame, if it has not previously computed the shape for the previous frame(s).

A general process for working with cloth is to:

Model the cloth object as a general starting shape.

Designate the object as a “cloth” in the Physics tab of the Properties.

Model other deflection objects that will interact with the cloth. Ensure the Deflection modifier is last on the modifier stack, after any other mesh deforming modifiers.

Light the cloth and assign materials and textures, UV unwrapping if desired.

If desired, give the object particles, such as steam coming off the surface.

Run the simulation and adjust settings to obtain satisfactory results. The Timeline editors playback controls are great for this step.

Optionally age the mesh to some point in the simulation to obtain a new default starting shape.

Make minor edits to the mesh on a frame-by-frame basis to correct minor tears.

To avoid unstable simulation, make sure that the cloth object does not penetrate any of the deflection objects.

Internally, cloth physics is simulated with virtual springs that connect the vertices of a mesh. There are four types of springs that control how the cloth bends. These four types are defined below and illustrated in the following image:

Illustration of cloth springs; tension springs (blue), compression springs (red), shear springs (cyan), and angular bending springs (green).¶

Control the stiffness of the cloth.

Control the amount of force required to collapse or compress the cloth.

Like compression springs but it controls the angular deformation.

Control how resilient the cloth is to folding or crumpling.

All four of these spring types can be controlled independently in the Physical Properties panel. While these settings control surface springs, optionally, internal springs can be used for 3D meshes and behave similarly to Soft Bodies.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/modes/vertex_paint/introduction.html

**Contents:**
- Introduction¶
- Vertex Paint Mode¶
- Vertex Paint Options¶

Vertex Painting is a simple way of painting color onto a Grease Pencil object, by directly manipulating the color of points/vertices, rather than use only the materials base color.

Stroke with original base material color (left) and with vertex painting (right).¶

When a point is painted, the color of the points is mixing with the base material color according to the settings of the brush.

A vertex in Grease Pencil is called point. Point and vertex names are equivalent.

Vertex Paint Mode is selected from the Mode menu in the 3D Viewport header. Once Vertex Paint Mode is activated, the Toolbar of the 3D Viewport will change to Vertex Paint Mode specific panels.

3D Viewport Mode selector set to Vertex Paint Mode.¶

Vertex Paint Mode in Grease Pencil allows you to select points or strokes to restrict the effect of the painting tools to only a certain areas of your drawing.

You can use the selection tools in the Toolbar for a quick selections.

You can restrict painting only on the selected points or strokes with the Selection mode toggle. The three modes can be toggled with 1, 2, or 3 respectively.

Sometimes you may need to modify several frames at the same time with the painting tools.

You can activate multiframe editing with the Multiframe button next to the modes selector (faded lines icon). See Multiframe for more information.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/introduction.html

**Contents:**
- Introduction¶
- Modeling Modes¶

Mesh Modeling typically begins with a Mesh Primitive shape (e.g. circle, cube, cylinder…). From there you might begin editing to create a larger, more complex shape.

The 3D Viewport has three principal modes that allow for the creation, editing and manipulation of the mesh models. Each of the three modes has a variety of tools. Some tools may be found in one or more of the modes.

Modes that used for modeling:

Supports basic operations such as object creation, joining objects, managing shape keys, UV/color layers.

Used for the majority of mesh editing operations.

Instead of dealing with individual mesh elements, supports sculpting with brushes (not covered in this chapter).

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/physics/introduction.html

**Contents:**
- Introduction¶
- Quick Effects¶
  - Quick Fur¶

Blender’s physics system allows you to simulate a number of different real-world physical phenomena. You can use these systems to create a variety of static and dynamic effects such as:

Hair, grass, and flocks

Object ‣ Quick Effects

Sets up a basic simulation scene or effect including the selected objects. The tool will add essential objects like domains or particle systems both with predefined settings, so that there will be instant viewable result.

Adds a fur setup to the selected objects. The fur setup is based on Geometry Nodes and built with Hair Node Groups that come with Blender as bundled assets.

Surface density of generated hair curves.

Length of the generated hair curves.

The width of the hair, used for rendering engines.

Factor applied on the density for the viewport.

Applies the modifier that uses the Generate Hair Curves node group.

Deforms hair curves using a noise texture. See the Hair Curves Noise node group for more information.

Deforms hair curves using a random vector per point to frizz them. See the Frizz Hair Curves node group for more information.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/grease_pencil/visual_effects/introduction.html

**Contents:**
- Introduction¶
- Interface¶

Properties ‣ Visual Effects

Grease Pencil has a special set of viewport real-time visual effects that can be apply to the object.

These effects treat the object as if it was just an image, for that reason they have effect on the whole object and cannot limit their influence on certain parts like layers, materials or vertex group as with modifiers. Also unlike modifiers, they can not be applied to the object.

Their main purpose is to have a quick way to apply visual effects on your drawings like blurring, pixelation, wave distortion, among others.

Visual Effects best fit for quick viewport visualization. You can use it for final renders but if you want more precision with effects it is still recommended to use the Compositor.

Panel layout (Blur effect as an example).¶

The visual effects panels and interface are similar to modifiers. Each effect shares the same basic interface components similar to modifiers for meshes.

See Modifiers Interface for more information.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/dope_sheet/introduction.html

**Contents:**
- Introduction¶
- Dope Sheet Modes¶
- Main Region¶

The Dope Sheet offers a bird’s-eye view of the keyframes inside the scene. It’s inspired by classical hand-drawn animation, where animators make use of a chart showing exactly when each drawing, sound, and camera move will occur, and for how long. It is also possible to show Playback Controls to control the playhead.

The editor has several different modes that can be selected from a dropdown in the header. The default Dope Sheet mode gives an overview of most types of animatable data. For others, such as masks, you need to switch to a more specific mode.

The modes are as follows:

Cache File: originally meant to show the baked animation data in Alembic files, but never implemented.

The Dope Sheet Editor shows a stack of channels (animatable properties), and for each channel, a series of keyframes laid out along the time axis.

The Dope Sheet Editor with object channels.¶

Keyframes can take on various colors and shapes:

Custom keyframe tag set by the user (Key ‣ Keyframe Type)

Free Keyframe Handle (Key ‣ Handle Type)

Auto-Clamped Keyframe Handle

Automatic Keyframe Handle

Vector Keyframe Handle

Aligned Keyframe Handle

Gray bar between keys

Held key (the two keyframes are identical)

Green line between keys

The curve segment uses custom interpolation (Key ‣ Interpolation Mode)

Local maximum in curve (visible if View ‣ Show Curve Extremes is enabled)

Local minimum in curve

Keyframes can be selected by clicking and moved by dragging. See the Select and Key menus for more options.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/graph_editor/fcurves/introduction.html

**Contents:**
- Introduction¶
- Direction of Time¶

Blender lets you animate almost any property, going from the X coordinate of an object to the transparency of a material. The evolution of a property’s value over time is described by a function curve, or F-Curve for short.

An important aspect of F-Curves is that they can interpolate. This saves you the effort of manually configuring a value on every single frame, which would be highly impractical. Instead, you define just a few values on key frames, and let the curve calculate the values on all the other frames.

Example of interpolation.¶

The example curve on the right has two such keyframes (indicated by black dots): one on frame 0 with value 0, and another on frame 25 with value 10. The curve automatically calculates the values for the other frames, such as for frame 5 where the value is 2.

F-Curves are similar to Curve objects in that they interpolate between a set of user-defined control points. However, because their purpose is to define a single value on every frame, there’s an important difference: F-curves can’t be closed or otherwise made to turn back on themselves. They always continue going further to the right.

If you try to make a curve go left by dragging one control point past another, it switches the order of the points to prevent this.

Before moving the second keyframe.¶

After moving the second keyframe.¶

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/sequencer/introduction.html

**Contents:**
- Introduction¶

The Sequencer view is where most of the video editing happens. It shows a stack of channels, in which you can create strips.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/bone_constraints/introduction.html

**Contents:**
- Introduction¶

The Bone Constraints Properties in Pose Mode, with an Inverse Kinematics constraint added to the active bone.¶

As bones behave like objects in Pose Mode, they can also be constrained. This is why the Constraints tab is shown in both Object Mode and Edit Mode. This panel contains the constraints of the active bone (its name is displayed at the top of the panel, in the To Bone:… static text field).

Constraining bones can be used to control their degree of freedom in their pose transformations, using e.g. the Limit constraints. You can also use constraints to make a bone track another object/bone (inside the same object, or in another armature), etc. And the inverse kinematics feature is also mainly available through the IK Solver constraint, which is specific to bones.

For example, a human elbow cannot rotate backward (unless the character has broken their arm), nor to the sides, and its forward and roll rotations are limited in a given range. (E.g. depending on the rest position of your elbow, it may be from (0 to 160) or from (-45 to 135).)

So you should apply a Limit Rotation constraint to the forearm bone (as the elbow movement is the result of rotating the forearm bone around its root).

Using bones in constraints, either as owners or as targets, is discussed in detail in the constraints pages.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/modifiers/introduction.html

**Contents:**
- Introduction¶
- Categories¶
- Interface¶
  - The Modifier Stack¶
    - Active Modifier¶
- Example¶

Modifiers are automatic operations that affect an object’s geometry in a non-destructive way. With modifiers, you can perform many effects automatically that would otherwise be too tedious to do manually (such as subdivision surfaces) and without affecting the base geometry of your object.

They work by changing how an object is displayed and rendered, but not the geometry which you can edit directly. You can add several modifiers to a single object to form The Modifier Stack and Apply a modifier if you wish to make its changes permanent.

They can be added to the active object using the Add Modifier operator, the “Add Modifier” button at the top of Modifiers tab in the Properties Editor, or using Shift-A in the same tab. New modifiers are always added at the bottom of the stack (i.e. will be applied last).

There are many built-in modifiers but Blender also allows users to make their own modifiers through Geometry Nodes.

There are four categories of built-in modifiers:

Similar to the Deform modifiers (see below), however, they usually do not directly affect the geometry of the object, but some other data, such as vertex groups.

Constructive/destructive modifiers that will affect the whole Topology of the mesh. They can change the general appearance of the object, or add new geometry to it…

Unlike Generate ones above, these modifiers only change the shape of an object, without altering its topology.

Represent physics simulations. In most cases, they are automatically added to the modifiers stack whenever a Particle System or Physics simulation is enabled. Their only role is to define the position in the modifier stack from which is taken the base data for the simulation they represent. As such, they typically have no properties, and are controlled by settings exposed in separate sections of the Properties Editor.

You will also notice a category called “Hair”, this category comes from a bundled Asset Library that is distributed with Blender. See Hair Nodes for more information.

Users can make their own categories by making geometry node groups assets and assigning them to a Asset Catalog. This catalog name will be the category name. If a user creates a catalog with the same name as one of the built-in categories the node group will be added to the bottom of the corresponding menu.

Node Groups that are non-assets or that do not belong to a category will be available in the “Unassigned” sub-menu.

Geometry Node Groups must have the Modifier property enabled for the node group to show up in the Add Modifier menu.

Each modifier’s interface shares the same basic components, see Fig. Panel layout (Subdivision Surface as an example)..

Panel layout (Subdivision Surface as an example).¶

At the top is the panel header. The icons each represent different settings for the modifier (left to right):

Collapse modifier to show only the header and not its options.

An icon as a quick visual reference of the modifier’s type.

Every modifier has a unique name per object. Two modifiers on one object must have unique names, but two modifiers on different objects can have the same name. The default name is based on the modifier type.

Depends on the previous setting, if enabled, the modified geometry can also be edited directly, instead of the original one.

While it shows edited items in their final, modified positions, you are still editing original data.

In situations where the positions diverge it can lead to confusing behavior, so you may wish to disable it in those cases.

It’s also worth noting that some features don’t use the cage positions including:

Snap targets, such as snapping to vertex.

The transform gizmo uses the original positions.

Apply the whole modifier stack up to and including that one on the curve or surface control points, instead of their tessellated geometry.

By default, curves, texts and surfaces are always converted to mesh-like geometry before that the modifier stack is evaluated on them.

Display the modified geometry in Edit Mode, as well as the original geometry which you can edit.

Toggle visibility of the modifier’s effect in the 3D Viewport.

Toggle visibility of the modifier’s effect in the render.

The Square, Triangle and Surface icons may not be available, depending on the type of object and modifier.

Makes the modifier “real”: converts the object’s geometry to match the applied modifier’s results, and deletes the modifier.

When applying a modifier to an object that shares Object Data between multiple objects, the object must first be made a Single User which can be performed by confirming the pop-up message.

Applying a modifier that is not first in the stack will ignore the stack order (it will be applied as if it was the first one), and may produce undesired results.

Stores the result of that modifier in a new relative shape key and then deletes the modifier from the modifier stack. This is only available with modifiers that do not affect the topology (typically, Deform modifiers only).

Even though it should work with any geometry type that supports shape keys, currently it will only work with meshes.

Stores the result of that modifier in a new relative shape key and keeps the modifier in the modifier stack. This is only available with modifiers that do not affect the topology (typically, Deform modifiers only).

Creates a duplicate of the modifier just below current one in the stack.

Copies the modifier from the Active object to all selected objects.

Moves the modifier to the first or last position in the modifier stack.

Keeps the modifier at the end of the modifier stack. When a modifier is pinned, a pin icon will be displayed on the right side of the panel’s header.

Converts the existing Geometry Nodes Modifier node tree to a group node to be reused in other node trees. See Move to Nodes Operator for more information.

This operator is only available for the Geometry Nodes Modifier.

Move the modifier up/down in the stack, changing the evaluation order of the modifiers.

A modifier is not movable if Pin to Last is enabled.

Below this header, all of the options unique to each modifier will be displayed.

Use Alt to affect all selected objects at once when performing operators such as add, apply, remove, and move to index.

See Multi-Object Editing for more information.

Modifiers are a series of non-destructive operations which can be applied on top of an object’s geometry. You can be apply them in almost any order. This kind of functionality is often referred to as a “modifier stack” and is also found in several other 3D applications.

In a modifier stack, the order in which modifiers are applied has an effect on the result. Therefore the modifiers can be re-arranged by clicking (grip icon) in the top right, and moving the selected modifier up or down. For example, the image below shows Subdivision Surface and Mirror modifiers that have switched places.

The Mirror modifier is the last item in the stack and the result looks like two surfaces.¶

The Subdivision Surface modifier is the last item in the stack and the result is a single merged surface.¶

Modifiers are calculated from top to bottom in the stack. In this example, the desired result (on right) is achieved by first mirroring the object, and then calculating the subdivision surface.

A modifier in the stack can be selected to mark in as Active, the active modifier displays an outline around the modifier’s panel. To set an active modifier, select an area of the modifier’s panel background, the modifier’s icon, or, select a modifier in the Outliner.

The active modifier is used by the Geometry Node Editor to determine which node group is being modified.

In this example a simple subdivided cube has been transformed into a rather complex object using a stack of modifiers.¶

Download example file.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/graph_editor/channels/introduction.html

**Contents:**
- Introduction¶
- Channels Region¶
  - Channels¶
  - Selection¶
  - Editing¶
    - Sliders¶

The Channels region.¶

This region is found on the left side of time-based editors like the Dope Sheet Editor and the Graph Editor. It shows a tree of items (objects, bones…) and their animated properties, with the latter also being called “channels.” Each channel has an associated F-curve describing how its value changes over time.

The rows are color-coded as follows:

Dark blue: scenes, objects

Light blue: actions, shape keys etc.

Green: channel groups

Lets you filter the channels by typing a part of their name. Click the Invert button to instead show channels that don’t include the search text.

The headers contain the following toggle buttons:

Keep the row and its children visible even when selecting a different object.

Hides the keyframes and curve associated with the channel.

Deactivates the modifiers of the curve.

Deactivates the curve, making the animation behave as though it doesn’t exist.

Prevent the curve from being edited.

This also works in the Nonlinear Animation Editor, but note that it only locks the strips there, not the underlying F-curves.

Select single header: click LMB

Add/Remove single header to/from selection: click Ctrl-LMB

Select range: click Shift-LMB

Deselect All: press Alt-A or double-tap A

Box Add: drag Shift-LMB

Box Remove: drag Ctrl-LMB

Select all keyframes in the channel: double-click LMB on its header.

Rename (anything but a channel): double-click LMB

Delete selected: X or Delete

The Action editor showing sliders.¶

If you enable View ‣ Show Sliders, the region will show a value slider next to each channel. Changing such a slider will change the value of the curve at the current frame, creating a keyframe if one doesn’t already exist.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/preview/introduction.html

**Contents:**
- Introduction¶
- Playback Controls¶

The Preview mode shows how the final edited video will look like. It also offers tools for moving, rotating, and scaling images, as well as scopes for analyzing color distribution.

Preview mode of the Video Sequencer.¶

You can pan around the view with MMB and zoom with Wheel or NumpadPlus/ NumpadMinus. Alternatively, you can use the gizmos.

Pressing Home resets the view, maximizing the size of the preview within the editor’s area.

The Playback Controls region contains controls and options related to playback, keying, auto keyframing, and transport.

These settings allow you to:

Control how animations are previewed and synchronized with audio.

Insert and manage keyframes through keying sets and auto keying.

Navigate the timeline using playback and transport controls.

Adjust frame ranges and preview specific segments of the animation.

For a detailed description of all properties and controls commonly found in the footer, see the Playback Controls documentation.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/introduction.html

**Contents:**
- Introduction¶
- Add Menu¶
- Locking Bones¶

As with any other object, you edit your armature in Edit Mode Tab.

The set of bone editing tools is quite similar to the one for mesh editing.

One important thing to understand about armature editing is that you edit the rest position of your armature, i.e. its “default state”. An armature in its rest position has all bones with no rotation and scaled to 1.0 in their own local space.

The different poses you might create afterwards are based on this rest position. So if you modify it in Edit Mode, all the poses already existing will also be modified. Thus you should in general be sure that your armature is definitive before starting to skin and pose it!

Please note that some tools work on bones’ joints, while others work on bones themselves. Be careful not to get confused.

In the 3D Viewport, Shift-A to add a new bone to your armature.

Of one unit of length.

Oriented towards the global Z axis.

With its root placed at the 3D cursor position.

With no relationship with any other bone of the armature.

You can prevent a bone from being transformed in Edit Mode in several ways:

All bones can be locked clicking on the Lock checkbox of their Transform panel in the Bones tab;

Press Shift-W Toggle Bone Options ‣ Locked

Select Armature ‣ Bone Settings ‣ Toggle a Setting.

If the root of a locked bone is connected to the tip of an unlocked bone, it will not be locked, i.e. you will be able to move it to your liking. This means that in a chain of connected bones, when you lock one bone, you only really lock its tip. With unconnected bones, the locking is effective on both joints of the bone.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/navigate/introduction.html

**Contents:**
- Introduction¶
- Navigation Gizmo¶

To be able to work in the three-dimensional space that Blender uses, you must be able to change your viewpoint as well as the viewing direction of the scene. While we will describe the 3D Viewport editor, most of the other editors have similar functions. For example, it is possible to pan and zoom in the Image editor.

Some navigation tools require a middle mouse button or numpad. If you don’t have one of these, see the Keyboard and Mouse page of the manual to learn how to work around this.

The navigation gizmo can be found in the top right of the editor.

The Orbit gizmo at the top shows the current orientation of the view. Dragging it with LMB will orbit the view. Clicking any of the axis labels will align the view to that axis. Clicking the same axis again switches to the opposite side of that same axis.

The four buttons below the orbit gizmo do the following:

Toggle the Camera View

Toggle the Projection / Toggle Lock Camera to View (in camera view)

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/properties/vertex_groups/introduction.html

**Contents:**
- Introduction¶
- Usage¶

The Vertex Groups panel.¶

Vertex groups are primarily used to tag vertices that belong to specific parts of a mesh or Lattice object. For example, they can represent the legs of a chair, the hinges of a door, or the arms, hands, and head of a character.

Each vertex group can store a weight value for each vertex it includes. These weights are in the range of 0 to 1 and are used by many operators, tools, and modifiers, which is why vertex groups are sometimes also referred to as “weight groups”.

Vertex groups can be created manually or generated automatically. They are most commonly used for armature-based deformation (also called skinning), but they are also used in many other areas of Blender, such as:

Skinning Mesh Objects

Vertex groups are only available for mesh and lattice objects.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/introduction.html

**Contents:**
- Introduction¶
- Visualization¶
  - Bone State Colors¶

Once an armature is skinned by the needed object(s), you need a way to configure the armature into positions known as poses. Basically, by transforming the bones, you deform or transform the skinned object(s). However, you will notice that you cannot do this in Edit Mode – remember that Edit Mode is used to edit the default, base, or “rest” position of an armature. You may also notice that you cannot use Object Mode either, as here you can only transform whole objects.

So, armatures have a third mode dedicated to the process of posing known as Pose Mode. In rest position (as edited in Edit Mode), each bone has its own position/rotation/scale to neutral values (i.e. 0.0 for position and rotation, and 1.0 for scale). Hence, when you edit a bone in Pose Mode, you create an offset in the transform properties, from its rest position. This may seem quite similar if you have worked with relative shape keys or Delta Transformations.

Even though it might be used for completely static purposes, posing is heavily connected with animation features and techniques. So if you are not familiar at all with animation in Blender, it might be a good idea to read the animation chapter first, and then come back here.

The color of the bones are based on their state. There are six different color codes, ordered here by precedence (i.e. the bone will be of the color of the bottom-most valid state):

Blue wire-frame: in Pose Mode.

Green: with Constraint.

Yellow: with IK Solver constraint.

Orange: with Targetless Solver constraint.

When bone colors are enabled, the state colors will be overridden.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/collections/introduction.html

**Contents:**
- Introduction¶
- Collections¶
- Naming and Nesting¶
- Color Tagging¶

In Blender, objects are not directly part of the scenes. Instead, they all get stored in a main database (basically the blend-file).

The blend-file and its stored data.¶

From there they are referenced into as many Scenes as you would like to see them.

When they are stored in a scene, they are part of a so-called scene collection. So ultimately all the scene objects belong to this special collection.

The scene collection.¶

While the scene collection contains all the Scene’s objects, the user can also make their own collections to better organize these objects.

It works like a Venn diagram, where all the objects are part of the scene collection, but can also be part of multiple collections.

The result is a clear and flexible way to arrange objects together on the Scene level.

Collections can be named and sorted hierarchically. Just like folders can have subfolders in any operating system, collections can have nested collections too.

For example: a house collection can contain a bedroom collection, which in turn contains a furniture collection referencing a bed, a cabinet and other objects.

Collections can have a color group assigned to them; helping organize and group different collections. This color tag is displayed as part of the collection icon in the Outliner and various other menus. The available colors are defined by Blender’s interface Theme.

To assign a color to a collection, use the Set Color Tag tool in the Outliner.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/nla/introduction.html

**Contents:**
- Introduction¶
- Main Region¶
- Header¶
  - View Menu¶
  - Select Menu¶
  - Marker Menu¶
  - Add Menu¶
  - Track Menu¶
  - Strip Menu¶
  - Filters¶

The NonLinear Animation editor, or NLA editor for short, lets you animate on a higher level. Instead of working with individual keyframes, it works with actions, which are named, reusable animation segments.

The editor displays a stack of tracks which work like layers in an image editing program. Higher tracks take precedence over lower ones, although you can also choose to blend them.

Each track can contain any number of strips – typically Action Strips, which are instances of actions.

The top track highlighted in orange is special: this is the Action Track. Unlike the other tracks, it doesn’t contain strips – instead, it contains the object’s active action, which is where new keyframes are added to by default.

Editors like the Dope Sheet Editor normally only show the keyframes of this active action. If you want to edit another action, you can select it in the NLA editor and press Tab to enter Tweak Mode.

Tweaking an action. Notice that it’s shown in both its original track and the Action Track. The active action is temporarily hidden.¶

Shows or hides the Sidebar Region.

Displays a pop-up panel to alter properties of the last completed operation. See Adjust Last Operation.

Shows or hides the Track Region.

Show or hide the Playback Controls.

Pans and zooms the view to focus on the selected strips.

Pans and zooms the view to show all strips.

Reset the horizontal view to the current scene frame range, taking the preview range into account if it is active.

Centers the view on the Playhead.

Whether to update other views (such as the 3D Viewport) while you’re moving strips around. If disabled, the other views only get updated once you finish the move.

Shows a graph on top of each strip that uses Animated Influence.

Shows the marker region (provided any markers have been defined). When disabled, the Marker Menu is also hidden and marker operators are not available in this editor.

Shows action-local markers (which you can create in the Action Editor). This can be useful to align strips to each other.

Local markers shown in the NLA Editor (top) and the Action Editor (bottom).¶

Shows timing in seconds instead of frames.

Synchronizes the horizontal panning and scale of the editor with other time-based editors that also have this option enabled. That way, they always show the same section of time.

Lets you drag a box to define a time range for previewing. As long as this range is active, playback will be limited to it, letting you repeatedly view a segment of the animation without having to manually rewind each time.

You can change the start or end frame using the corresponding button in the Timeline editor’s Playback popover. Alternatively, you can simply run Set Preview Range again.

Clears the preview range.

Applies a preview range that encompasses the selected strips.

Area controls. See the user interface documentation for more information.

Deselects all strips.

Inverts the current selection.

Lets you drag a box and selects the strips that are partially or completely inside it.

Lets you drag a box and selects the strips that overlap the corresponding time range, even if they’re above or below the box.

Selects all the strips that start before (or on) the current frame.

Selects all the strips that end after (or on) the current frame.

Markers are used to denote frames with key points or significant events within an animation. Like with most animation editors, they’re shown at the bottom.

Markers in animation editor.¶

For descriptions of the different marker tools, see Editing Markers.

Adds a strip referencing an action to the active track.

Adds a transition strip between the two selected action strips.

Adds a strip that controls when the Speaker Objects object plays its sound clip.

Makes the selected objects appear in the NLA Editor without adding an action or track to them.

See Strips for details on the various strip types.

Contains tools for working with NLA tracks. See Editing Tracks for details.

Contains tools for working with NLA strips. See Editing Strips for details.

Only shows tracks belonging to objects that are selected.

Shows tracks from objects that are hidden.

Shows the Action Track even if there is no action in it.

Filters the track list by a search term.

Select a collection to only show tracks from objects in that collection.

Filter tracks by target type.

Sorts data-blocks alphabetically to make them easier to find.

If your playback speed suffers because of this (should only really be an issue when working with lots of objects), you can turn it off.

The toggle button enables/disables automatic strip snapping. The dropdown button shows a popover with the following options:

Type of element to snap to.

Snap to the nearest Marker.

When disabled, strips will move in increments of Snap To. For example, if you selected Second and have a strip that currently starts on 0:06+5, dragging it to the right will snap it to 0:07+5. Its time increases by a second, and its subsecond offset of 5 frames remains the same.

When enabled, strips will snap to multiples of Snap To. Taking the above example, the strip would snap to 0:07+0, removing the subsecond offset.

The Playback Controls region contains controls and options related to playback, keying, auto keyframing, and transport.

These settings allow you to:

Control how animations are previewed and synchronized with audio.

Insert and manage keyframes through keying sets and auto keying.

Navigate the timeline using playback and transport controls.

Adjust frame ranges and preview specific segments of the animation.

For a detailed description of all properties and controls commonly found in the footer, see the Playback Controls documentation.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/introduction.html

**Contents:**
- Introduction¶
- Classification¶
  - Deforming Bones¶
  - Control Bones¶

Much like in real-life skeletons, Bones are the building blocks of Armatures. Each bone has a resting position, orientation, and length – and all of these can be changed while posing or animating.

You can change the way bones are displayed in the armature’s Viewport Display settings.

Bones can be classified into two types depending on their Deform setting:

Bones that have the Deform setting enabled will drag vertices along with them. For example, you could have a bone in a character’s upper arm and another in the lower arm, and then rotate and flex the arm by transforming these bones.

Bones that have the Deform setting disabled do not drag any vertices along. Instead, they’re typically used to control other bones.

A common use case is inverse kinematics: rotating the above two arm bones manually is a bit of a pain, so instead, you can add a control bone and configure the arm bones to automatically orient themselves towards it. This way, you can simply position the control bone where the character’s hand should be, which is much easier.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/introduction.html

**Contents:**
- Introduction¶
- Managing Preferences¶

This chapter explains how to change Blender’s default configuration with the Preferences editor.

The Blender Preferences contains settings to control how Blender behaves. At the left of the editor, the available options are grouped into sections.

Blender Preferences window.¶

Default preferences are managed from the ☰ menu in the preferences window.

The following items are available in this menu:

By default changes to preferences are saved on exit, this allows changes to the keymap and Quick Favorites menu to be stored and used between Blender Sessions.

When disabled, a Save Preferences button is shown to manually perform the operation.

Undoes any unsaved modifications, loading the previously saved state.

Completely undo all the modifications made to the preferences, resetting to the state used before making customizations.

After running Load Factory Preferences, auto-save will be disabled for the current session.

This allows you to switch back to the factory settings for testing or following tutorials for example, without the risk of accidentally auto-saving over the preferences you have manually configured.

If you wish to save these as your preferences, run Save Preferences manually.

This only resets the preferences and will not affect settings stored in the startup file. This includes app templates, area locations, and any Blender properties not part of the preferences.

These must be reverted though File ‣ Defaults.

It can be valuable to make a backup of your preferences in the event that you lose your configuration.

See the directory layout section to see where your preferences are stored.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/meshes/editing/introduction.html

**Contents:**
- Introduction¶
- Accessing Mesh Operators¶
  - Menus¶

Blender provides a variety of operators for editing meshes. These operators are used to add, duplicate, move and delete elements.

These are available through the Menus in the 3D Viewport header, and context menus in the 3D Viewport, as well as individual shortcut keys.

All the “transform precision/snap” keys Ctrl and/or Shift also work for all these advanced operations, but most of them do not have axis locking possibilities, and some of them do not take into account the pivot point and/or transform orientation either.

These transform operators are available in the Transform section of the Mesh menu in the header. Note that, some of these can also be used on other editable objects, like curves, surfaces, and lattices.

The mesh editing operations are found in various places, and available through shortcuts as well.

These menus are located in the header. Some of the menus can be accessed with shortcuts:

Ctrl-F brings up the Face operators menu

Ctrl-E brings up the Edge operators menu

Ctrl-V brings up the Vertex operators menu

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/introduction.html

**Contents:**
- Introduction¶
- Creating a Rigid Body¶
- Working with Rigid Bodies¶

The rigid body simulation can be used to simulate the motion of solid objects. It affects the position and orientation of objects and does not deform them.

Unlike the other simulations in Blender, the rigid body simulation works closer with the animation system. This means that rigid bodies can be used like regular objects and be part of parent-child relationships, animation constraints and drivers.

Properties ‣ Physics ‣ Rigid Body

Only mesh objects can be part of a rigid body simulation. To create rigid bodies, either click on the Rigid Body button in the Physics tab of the Properties or use Add Active/Add Passive in the Object ‣ Rigid Body menu.

There are two types of rigid bodies: active and passive. Active bodies are dynamically simulated, while passive bodies remain static. Both types can be driven by the animation system when using the Animated option.

During the simulation, the rigid body system will override the position and orientation of dynamic rigid body objects. Note however, that the location and rotation of the objects are not changed, so the rigid body simulation acts similar to a constraint. To apply the rigid body transformations you can use the Apply Object Transform operator.

The scale of the rigid body object also influences the simulation, but is always controlled by the animation system.

Rigid body physics on the object can be removed with the Rigid Body button in the Physics tab in the Properties or in the Object ‣ Rigid Body menu.

Several object operators exist for working with rigid bodies, these operators can be found in the Rigid Body object menu. These operators include functions to add/remove rigid bodies, modify their properties, and add Rigid Body Constraints.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/vertex_paint/introduction.html

**Contents:**
- Introduction¶
- Viewing Color Attributes¶

Vertex Painting is a simple way of painting color onto an object, by directly manipulating the color of vertices, rather than textures, and is fairly straightforward. Vertex Painting stores the color information as a Color Attribute which can be used by different render engines.

Color attribute’s can be managed in the pallette pop-over in the middle of the header.

Vertex Painting Mode.¶

When a vertex is painted, the color of the vertex is modified according to the settings of the brush. The color of all visible planes and edges attached to the vertex are then modified with a gradient to the color of the other connected vertices. Note that the color of occluded faces is not modified.

Dynamic Paint can create Color Attribute information while using physics or animation.

Color Attributes can be used in a material node tree using the Color Attribute Node.

Color Attributes can be viewed in the 3D viewport using the Workbench render engine. To use such feature, set the 3D Viewport to Solid Shading and select the Attribute Color option.

---

## Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/modeling/introduction.html

**Contents:**
- Introduction¶
- Modes¶
  - Edit Mode¶

The creation of a 3D scene needs at least three key components: Models, materials and lights. In this part, the first of these is covered, that being modeling. Modeling is simply the art and science of creating a surface that either mimics the shape of a real-world object or expresses your imagination of abstract objects.

Depending on the type of object you are trying to model, there are different types of modeling modes. Since modes are not specific to modeling they are covered in different parts of the manual.

Switching between modes while modeling is common. Some tools may be available in more than one mode while others may be unique to a particular mode.

Edit Mode is the main mode where modeling takes place. Edit Mode is used to edit the following types of objects:

You can only modify the mesh of the objects you are editing. To modify other objects you can leave Edit Mode, select another object and enter Edit Mode, or use Multi-Object Editing.

---

## Inverse Kinematics¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/bone_constraints/inverse_kinematics/introduction.html

**Contents:**
- Inverse Kinematics¶
- Armature IK Panel¶
  - Standard¶
  - iTaSC¶
    - Animation¶
    - Simulation¶
- Bone IK Panel¶
  - iTaSC Solver¶
- Arm Rig Example¶

Inverse Kinematics (IK) simplifies the animation process, and makes it possible to make more advanced animations with lesser effort.

Inverse Kinematics allow you to position the last bone in a bone chain and the other bones are positioned automatically. This is like how moving someone’s finger would cause their arm to follow it. By normal posing techniques, you would have to start from the root bone, and set bones sequentially until you reach the tip bone: When each parent bone is moved, its child bone would inherit its location and rotation. Thus making tiny precise changes in poses becomes harder farther down the chain, as you may have to adjust all the parent bones first.

This effort is effectively avoided by use of IK.

IK is mostly done with bone constraints although there is also a simple Auto IK feature in Pose Mode. They work by the same method but the constraints offer more options and control. Please refer to the following pages for details about these constraints:

Inverse Kinematics Constraint

Properties ‣ Armature ‣ Inverse Kinematics

This panel is used to select the IK Solver type for the armature: Standard or iTaSC. Most the time people will use the Standard IK solver.

The armature IK panel.¶

iTaSC stands for instantaneous Task Specification using Constraints.

iTaSC uses a different method to compute the Jacobian, which makes it able to handle other constraints than just end effectors position and orientation: iTaSC is a generic multi-constraint IK solver. However, this capability is not yet fully exploited in the current implementation, only two other types of constraints can be handled: Distance in the Cartesian space, and Joint Rotation in the joint space. The first one allows maintaining an end effector inside, at, or outside a sphere centered on a target position, the second one is the capability to control directly the rotation of a bone relative to its parent. Those interested in the mathematics can find a short description of the method used to build the Jacobian here.

iTaSC accepts a mix of constraints, and multiple constraints per bone: the solver computes the optimal pose according to the respective weights of each constraint. This is a major improvement from the current constraint system where constraints are solved one by one in order of definition so that conflicting constraints overwrite each other.

The maximum variation of the end effector between two successive iterations at which a pose is obtained that is stable enough and the solver should stop the iterations. Lower values means higher precision on the end effector position.

The upper bound for the number of iterations.

Selects the inverse Jacobian solver that iTaSC will use.

Computes the damping automatically by estimating the level of ‘cancellation’ in the armature kinematics. This method works well with the Copy Pose constraint but has the drawback of damping more than necessary around the singular pose, which means slower movements. Of course, this is only noticeable in Simulation mode.

Computes the damping manually which can provide more reactivity and more precision.

Maximum amount of damping. Smaller values means less damping, hence more velocity and better precision but also more risk of oscillation at singular pose. 0 means no damping at all.

Range of the damping zone around singular pose. Smaller values means a smaller zone of control and greater risk of passing over the singular pose, which means oscillation.

Damping and Epsilon must be tuned for each armature. You should use the smallest values that preserve stability.

The SDLS solver does not work together with a Distance constraint. You must use the DLS solver if you are going to have a singular pose in your animation with the Distance constraint.

Both solvers perform well if you do not have a singular pose.

In Animation mode, iTaSC operates like an IK solver: it is stateless and uses the pose from F-Curves interpolation as the start pose before the IK convergence. The target velocity is ignored and the solver converges until the given precision is obtained. Still the new solver is usually faster than the old one and provides features that are inherent to iTaSC: multiple targets per bone and multiple types of constraints.

The Simulation mode is the stateful mode of the solver: it estimates the target’s velocity, operates in a ‘true time’ context, ignores rotation from keyframes (except via a joint rotation constraint) and builds up a state cache automatically.

The solver starts from the rest pose and does not reiterate (converges) even for the first frame. This means that it will take a few frames to get to the target at the start of the animation.

The solver starts from the rest pose and re-iterates until the given precision is achieved, but only on the first frame (i.e. a frame which doesn’t have any previous frame in the cache). This option basically allows you to choose a different start pose than the rest pose and it is the default value. For the subsequent frames, the solver will track the target by integrating the joint velocity computed by the Jacobian solver over the time interval that the frame represents. The precision of the tracking depends on the feedback coefficient, number of substeps and velocity of the target.

The solver re-iterates on each frame until the given precision is achieved. This option omits most of the iTaSC dynamic behavior: the maximum joint velocity and the continuity between frames is not guaranteed anymore in compensation of better precision on the end effector positions. It is an intermediate mode between Animation and real-time Simulation.

Use this option if you want to let the solver set how many substeps should be executed for each frame. A substep is a subdivision on the time between two frames for which the solver evaluates the IK equation and updates the joint position. More substeps means more processing but better precision on tracking the targets. The auto step algorithm estimates the optimal number of steps to get the best trade-off between processing and precision. It works by estimation of the nonlinearity of the pose and by limiting the amplitude of joint variation during a substep. It can be configured with next two parameters:

Proposed minimum substep duration (in second). The auto step algorithm may reduce the substep further based on joint velocity.

Maximum substep duration (in second). The auto step algorithm will not allow substep longer than this value.

If Auto Step is disabled, you can choose a fixed number of substeps with this parameter. Substep should not be longer than 10 ms, which means the number of steps is 4 for a 25 fps animation. If the armature seems unstable (vibrates) between frames, you can improve the stability by increasing the number of steps.

Coefficient on end effector position error to set corrective joint velocity. The time constant of the error correction is the inverse of this value. However, this parameter has little effect on the dynamic of the armature since the algorithm evaluates the target velocity in any case. Setting this parameter to 0 means ‘opening the loop’: the solver tracks the velocity but not the position; the error will accumulate rapidly. Setting this value too high means an excessive amount of correction and risk of instability. The value should be in the range 20-100. Default value is 20, which means that tracking errors are corrected in a typical time of 100-200 ms. The feedback coefficient is the reason why the armature continues to move slightly in Simulation mode even if the target has stopped moving: the residual error is progressively suppressed frame after frame.

Indicative maximum joint velocity in radian per second. This parameter has an important effect on the armature dynamic. Smaller value will cause the armature to move slowly and lag behind if the targets are moving rapidly. You can simulate an inertia by setting this parameter to a low value.

Properties ‣ Bone ‣ Inverse Kinematics

This panel is used to control how the Pose Bones work in the IK chain.

Stretch influence to IK target.

Disallow movement around the axis.

Stiffness around the axis. Influence disabled if using Lock.

Limit movement around the axis.

If the iTaSC IK Solver is used, the bone IK panel changes to add these additional parameters.

Activates a joint rotation constraint on that bone. The pose rotation computed from Action or UI interaction will be converted into a joint value and passed to the solver as target for the joint. This will give you control over the joint while the solver still tracks the other IK targets. You can use this feature to give a preferred pose for joints (e.g. rest pose) or to animate a joint angle by playing an action on it.

The importance of the joint rotation constraint based on the constraints weight in case all constraints cannot be achieved at the same time. For example, if you want to enforce strongly the joint rotation, set a high weight on the joint rotation constraint and a low weight on the IK constraints.

This arm uses two bones to overcome the twist problem for the forearm. IK locking is used to stop the forearm from bending, but the forearm can still be twisted manually by pressing R Y Y in Pose Mode, or by using other constraints.

Note that, if a Pole Target is used, IK locking will not work on the root bone.

---

## Painting¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/introduction/painting.html

**Contents:**
- Painting¶

Sculpt Mode also allows painting your geometry via Color Attributes such as Vertex Colors. This ensures that the most common actions related to the sculpting workflow are contained in the same mode, to avoid unnecessary mode switching.

Other sculpt mode features such as face sets, masking and filters can also be used with painting tools.

The painting functionality in Sculpt Mode is limited to a Paint and Smear brush, as well as a Color Filter and Mask by Color tool.

Just like any other brush, Shift can be used to smooth. In the case of painting brushes it will blur the colors within the brush radius instead.

Once any painting tool is executed, the viewport color shading is switched to “Attribute”. This ensures that color attributes are shown on all objects once painting is needed.

---

## Remesh¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/tool_settings/remesh.html

**Contents:**
- Remesh¶
- Known Limitations¶

Tool Settings ‣ Remesh

Sidebar ‣ Tool ‣ Remesh

For a general explanation to remeshing, visit the Introduction.

The resolution or the amount of detail the remeshed mesh will have. The value is used to define the size, in object space, of the Voxel. These voxels are assembled around the mesh and are used to determine the new geometry. For example a value of 0.5m will create topological patches that are about 0.5m (assuming Preserve Volume is enabled). Lower values preserve finer details but will result in a mesh with a much more dense topology.

The voxel size also be adjusted from the 3D Viewport using R. Using the shortcut displays an interactive grid overlay showing the resulting voxel size. Moving the mouse closer to center of the grid decreases the voxel size while moving away from the center increase the voxel size. Holding Shift increases the precision; adjusting the voxel size in small increments.

Used to adjust the Voxel Size by picking an area of the mesh to match the denseness of polygons after the remesh operation.

Reduces the final face count by simplifying geometry where detail is not needed. This introduce triangulation to faces that do not need as much detail. Note, an Adaptivity value greater than zero disables Fix Poles.

Tries to produce less poles at the cost of some performance to produce a better topological flow.

Tells the algorithm to try to preserve the original volume of the mesh. Enabling this could make the operator slower depending on the complexity of the mesh.

Reprojects the paint mask onto the new mesh.

Reprojects Face Sets onto the new mesh.

Reprojects the Color Attributes onto the new mesh.

Performs the remeshing operation to create a new manifold mesh based on the volume of the current mesh. Performing this will lose all mesh object data layers associated with the original mesh.

Remeshing only works on the original mesh data and ignores generated geometry from modifiers, shape keys, rigging, etc.

Remeshing will not work with the Multiresolution Modifier.

---

## The Blender Community¶

**URL:** https://docs.blender.org/manual/en/latest/getting_started/about/community.html

**Contents:**
- The Blender Community¶
- Independent Sites¶
- Getting Support¶
- Development¶
- Chat¶
- Other Useful Links¶

Being freely available from the start, even while it was closed source, considerably helped Blender’s adoption by the community. A large, stable, and active community of users has gathered around Blender since 1998. The community showed its support for Blender in 2002 when they helped raise €100,000 in seven weeks to enable Blender to go Open Source under the GNU GPL License.

There are several independent websites such as forums, blogs, news, and tutorial sites dedicated to Blender.

One of the largest community forums is Blender Artists, where Blender users gather to show off their creations, get feedback, ask and offer help and, in general, discuss Blender.

Blender’s community is one of its greatest features, so apart from this user manual, there are many different ways to get support from other users, such as Chat, Stack Exchange, and Reddit.

For studios and organizations there is Enterprise support, and for studios looking to add Blender to their pipeline, Blender Studio contains documentation and training material around this topic. If you think you have found an issue with Blender, please report a bug.

More details about support can be found on the support page.

Being open source, Blender welcomes development from volunteers. Communication between developers is done mostly through three platforms:

The projects.blender.org system

Online Chat (see below)

If you are interested in helping develop Blender, see the Get Involved page.

For real-time discussion, we have chat.blender.org which uses Blender ID for authentication.

You can join these channels:

#general For general chat with the community.

#blender-coders For developers to discuss Blender development.

#python For support for developers using the Python API.

#docs For discussion related to Blender’s documentation.

#translations For discussion related to translating Blender and its documentation.

Blender FAQ (Can I use Blender commercially? What is GPL/GNU? …)

Demo and benchmark files

Developer’s Ask Us Anything!

---

## The Brush¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/introduction/brush.html

**Contents:**
- The Brush¶
- Common Brushes¶

Sculpt Mode is very recognizable by the behavior and visualization of the brush. All the usual brush controls still apply, yet the brush for sculpting is displayed in 3D. This means that the brush will follow the curvature of the surface by orienting the radius to match the topology Normal.

The inner ring of the brush cursor is used to visualize the strength of the brush.

How closely the cursor follows the curvature of the mesh can be changed in the Brush Settings with “Normal Radius”. This can make hard surface sculpting easier, for example with the Plane brush.

The brush is also used for other tools in the toolbar to better display how that tool works. For example, the Box Trim and Lasso Trim tools are able to use the current brush radius for how deep geometry is trimmed or added.

There are many brushes to choose from but these are the most common brushes to be used during sculpting. More information on sculpting brushes in the Toolbar.

Block out broad shapes and build up volumes before refining them further.

Move geometry across the screen for general shaping.

Smooth and shrink surfaces to remove noise or flatten shapes.

Generic adding and subtracting on surfaces. This brush is often customized with different stroke methods and textures for various effects.

Scrape and fill surfaces either for hard surface sculpting or more aggressive smoothing.

Inflate or shrink volumes or surfaces. Especially useful for controlling the thickness of cylindrical shapes.

Same as Draw but with a much sharper falloff. Useful for adding creases, cracks and other sharp edges.

A mix of the Draw and Pinch brushes. Useful for creating detailed creases or sharpening existing creases for additional polish.

Similar to Grab but this brush will dynamically let go and pick up geometry during the stroke. The dragged geometry is also following the angle of the stroke, making it very useful for pulling geometry out. Ideally used together with Dyntopo.

---

## Transforming¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/introduction/transforming.html

**Contents:**
- Transforming¶

Transform tools to move, rotate and scale are also available in Sculpt Mode, but with an important difference to other modes. Sculpt Mode uses its own pivot point, which can be manually positioned Shift-RMB or automatically positioned with Mask Expand. This ensures that the pivot point can be more freely placed and always moves with the transformed geometry.

Optionally instead of keeping the transform tools active, you can enable the viewport gizmos to have access to the gizmo at all times.

The gizmo can in some cases block areas from being sculpted on. In that case move the pivot point somewhere else to be able to click on the desired surface.

Apart from the transform tools there are also special brushes to move, rotate and scale the topology like Pose, Boundary and Elastic Deform.

---

## Visibility, Masking & Face Sets¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/introduction/visibility_masking_face_sets.html

**Contents:**
- Visibility, Masking & Face Sets¶
- Visibility Control¶
- Masks¶
  - Clear & Invert¶
- Face Sets¶
- Auto-Masking¶
- Display Settings¶

Parts of the mesh can be hidden in Sculpt Mode. Because hidden faces cannot be sculpted, hiding makes it easier to isolate what you want to work on. Hiding geometry also improves the viewport performance.

Hiding is shared between all modes, except Object Mode (i.e. hiding/showing of faces in one mode will hide the same faces in other modes too).

Unlike Selection Masking in other painting modes, Sculpt Mode primarily uses Masks and Face Sets to easily control the mesh visibility and which faces can currently be edited. The exception is the Clipping Region, which can be used in any mode.

The most common shortcuts are H to hide the face set under the cursor and Shift-H to isolate the face set under the cursor (or show everything).

Inverting the visibility and showing all is also available in the Alt-W pie menu.

Modifying visibility can also be done via the Hide Gesture Tools.

More information for controlling the visibility at Show & Hide.

A mask is used to control which vertices of the mesh are influenced by sculpting and painting. The mask can for example be created/edited via the Mask Gesture Tools and Mask by Color tool.

Internally, masks are stored using the sculpt_mask Attributes.

Creating masks follows a slightly different mental model than selecting in other modes. For example Shift-LMB is used for smoothing instead of adding to a mask.

Masking is also conceptually inverted to selection (i.e. You cannot edit masked vertices. But you can edit selected vertices).

Instead a mask is typically always added to the current mask with LMB and subtracted with Ctrl-LMB. So if you wish to edit the masked surfaces, you’ll need to use the Invert operator, In the case of masking everything that is visible, the best workflow is to first Clear and then Invert the mask.

Both these operators can be quickly accessed in the A pie menu.

More information about editing and using masks at the Mask Menu

Face sets are used to group your mesh into differently colored faces, which can then be quickly hidden or shown like mentioned above. They can also be used for fast mask creation via the Mask Expand. Face Set Expand is also useful for creating, editing and joining face sets.

More options can be found in the Alt-W pie menu.

Otherwise Face Sets can be created/edited with the Draw Face Sets brush, Mask Gesture Tools. They can also be edited with the Edit Face Set tool.

More information about editing and using face sets at the Face Sets Menu

Internally, face sets are stored using the sculpt_face_set Attributes.

Auto-Masking is also a fast way of only editing specific geometry without having to manually create a new mask or hide geometry. This feature is especially useful in combination with face sets.

The mask and face sets display can be toggled and adjusted in the Display Settings.

---

## Window System Introduction¶

**URL:** https://docs.blender.org/manual/en/latest/interface/window_system/introduction.html

**Contents:**
- Window System Introduction¶
- Customization¶

After starting Blender and closing the Splash Screen, the Blender window should look similar to the image below.

The default startup Blender window.¶

Blender’s interface is separated into three main parts:

The Topbar at the very top, consists of the main menu, which is used for saving, importing and exporting files, configuring settings, and rendering among other functions.

Areas in the middle, which is the main workspace.

The Status Bar at the bottom, which displays shortcut suggestions and relevant statistics.

Blender’s default Screen Layout. Topbar (blue), Areas (green) and Status Bar (red).¶

Blender makes heavy use of keyboard shortcuts to speed up work. These can be customized in the Keymap Editor.

Blender allows for most of its interface colors to be changed to suit the needs of the user. If you find that the colors you see on screen do not match those in the Manual, it could be that your default theme has been altered. Creating a new theme or selecting/altering a preexisting one can be done by opening the Preferences and clicking on the Themes tab.

Blender has several options for visibility customization, including resolution scale, and the ability to load custom fonts. These settings can be configured in the Interface Preferences.

---

## Working with Multiple Objects¶

**URL:** https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/introduction/multiple_objects.html

**Contents:**
- Working with Multiple Objects¶

Unlike Edit Mode, there is no multi-object editing supported for Sculpt Mode. Since sculpting often involves editing many separate objects, it is recommended to use the shortcut Alt Q while pointing at other objects, for Switching Objects quickly.

The advantage of using multiple objects is that each can have its own origin and modifiers. Splitting the geometry among multiple objects can also improve the sculpt mode performance. Alternatively objects can also be joined so there is no need to switch objects.

In the case that Face Sets were already used, joining objects or creating new geometry in Edit Mode will automatically assign new Face Sets. This makes it immediately possible to target each new geometry, for example via auto-masking. If no Face Sets are created, use the Initialize Face Sets operator to create them.

Face Sets and Masked geometry can also be extracted via Mask Extract or sliced into a new object via Mask Slice.

---
