# Blender - Animation

**Pages:** 107

---

## Actions¶

**URL:** https://docs.blender.org/manual/en/latest/animation/actions.html

**Contents:**
- Actions¶
- Action Slots¶
  - Slot Names and Associated Types¶
- F-Curves & Channels¶
- Working With Actions¶
  - Manually Assigning Actions and Slots¶
  - NLA¶
- Action Properties¶
  - Slot¶
  - Custom Properties¶

Actions are Blender’s container for animation data. For example, when you animate the location of an object, that animation is stored in an action rather than directly on the object itself. The object then uses the action to get animated, much the same way that a mesh uses a material to get shaded. All animatable data-blocks (objects, meshes, materials, etc.) are animated this way: they don’t store their own animation data, but instead use an action that stores the animation data for them.

Actions are also data-blocks themselves, and therefore can be easily appended or linked into other blend files. This lets actions be used not just for storage, but also for organizing and reusing animation data. For example, if you’re building a library of animations (run cycles, jumps, idling, etc.), each animation can go into its own action, which can then be conveniently linked or exported as a distinct animation.

The animation data inside an action is further organized into Slots. Each action has a set of slots and different animation data for each of those slots. An animated data-block then specifies both an action and a slot within that action, and that determines which animation data the data-block is animated by.

Action selector and its accompanying slot selector in the properties of an object, for seeing and selecting which action and slot animate the object.¶

The purpose of slots is to allow an action to store distinct animation data for multiple data-blocks. For example, you may have an animation of a bouncing ball that changes its color on each bounce, and that involves two data-blocks: the object and its material. Slots allow you to put both the object’s animation and the material’s animation in the same action by having a different slot for each.

Visualization of a ball and its material connected to different slots in an action.¶

In this example there is one slot for an object and one slot for a material, but you can have as many slots as you like for as many objects, materials, lights, etc. as you like. If you’re baking down a simulation of 100 bouncing balls, you could store that animation in single action with 100 slots.

Visualization of many balls all connected to different slots in an action.¶

Not all actions need to take advantage of slots: you are free to use 100 separate actions for all those bouncing balls if you prefer. Nevertheless, the animation data in an action is always organized into slots, and therefore you need at least one slot in an action in order to animate something.

Note that slots are not “for” any specific data-block: any data-block can use any slot. For example, you can have two different characters use the same slot in the same action, and they’ll both simply get animated by the same animation data. Slots are just a way to organize distinct animation data within an action, and don’t have any intrinsic attachment to anything in the scene.

Internally, the animation data in an action is further organized into layers and strips. This is not currently exposed in the UI and does not impact how you use actions right now. It is purely in preparation for future animation features that are not yet in Blender, and you can safely ignore it for now.

However, layers and strips are exposed in the Python API, so you will need to be aware of this when writing scripts and addons that work with actions. See the Python API documentation for more details.

Each slot in an action has a name, and you are free to name them whatever you like. By default, new slots are named after the last slot assigned to the data-block they were created for, or after the data-block itself if it’s never been assigned a slot before.

In addition to having a name, each slot also has an associated data-block type that it is intended for (for example, “material”, “object”, etc.). This is set automatically when a slot is first assigned to animate a data-block.

One of the places you can see a slot’s associated type is in the action editor’s channel list, where it’s displayed as an icon next to the slot’s name.

Slots displayed in the Action Editor’s channel list, with their associated type as an icon to the right of their name.¶

Within an action, a slot must have a unique combination of name + associated type. For example, you can have two slots named “Cube” in an action as long as one of them is for objects and the other is for materials, but not if they are both for objects. When they are both for objects, their associated type is the same, and thus they must have different names. In that case Blender will use the familiar approach and name them “Cube” and “Cube.001”.

Although it’s not useful, and Blender makes this difficult to do, it is nevertheless possible to cause slots to get assigned to a data-block of the wrong type. For example, assigning a slot intended for materials to an object. Nothing bad happens if you manage to do this, but the F-Curves of that slot are unlikely to match any properties on the mismatched data-block, and therefore won’t animate anything.

F-Curves are the fundamental unit of animation in Blender, and are the main kind of animation data that actions contain. Each F-Curve contains keyframes that define how a property (such as the X location of an object) should change over time.

Graph Editor, displaying three F-Curves for three different properties.¶

Blender’s animation editors (such as the dopesheet, graph editor, etc.) have a channel list on their left side that display animated properties. For actions, these channels correspond to the F-Curves that animate those properties.

The Dopesheet Editor’s channel list, with the animated channels of various bones grouped under their bone names.¶

Channels also support a limited form of organization called “channel groups”. For example, by default Blender creates a channel group for the channels of each bone. There are a few features in Blender that rely on the groups, but mostly they are just for your convenience.

When you first animate an object (or other data-block) in Blender, Blender tries to automatically find an appropriate action for it, or if it can’t find an appropriate action then it will create one. After an action has been assigned, it also creates and assigns a new slot for the data-block.

Blender uses heuristics to try to find an appropriate action, based on the idea that animation of closely related data-blocks should typically go in the same action. For example, an object and its data are considered closely related, so if a camera object is already animated and you insert keys for its focal length (which lives on the camera data, not the camera object), the action that’s assigned to the object will be reused for the camera data as well. These relationships go both ways, so the action will also be reused when keying the camera object if the camera data is already animated.

Some examples of other data-blocks that are considered closely related for this purpose are: materials and their embedded node trees, worlds and their embedded node trees, and meshes and their shape key data.

There is an exception to this “closely related” heuristic, which is when a data-block has more than one user. For example, if a single mesh data-block is used by multiple mesh objects, then the relationship is ignored and the mesh data and its users will get separate actions despite otherwise being considered closely related.

In addition to letting Blender automatically choose an action and slot for a data-block, you can also manually assign them. This can be used to assign existing animation to a data-block by selecting both the action and slot. It can also be used to specify an action for a data-block’s keys to go into, by assigning the action but leaving the slot blank, in which case a new slot will be created when the first key is set.

For each data-block in the properties editor there is an Animation panel with action and slot selectors. You can use these to assign actions and slots to a data-block.

The action and slot selector for Camera data in the Properties Editor.¶

For the active object you can also assign its action and slot in the action Editor’s header.

The action and slot selector for the active object (in this case a camera object) in the Action Editor.¶

Scene Animation Panel

Speaker Animation Panel

Movie Clip Animation Panel

Node Group Animation Panel

When selecting a slot for a data-block, you won’t necessarily see all the slots of an action listed in the dropdown. This is because Blender limits that dropdown to the slots with an associated type that matches the data-block.

When you select an action to animate a data-block, for convenience Blender attempts to automatically select an appropriate slot for you based on name and associated type. If no appropriate slot is found then the slot selector will remain empty, in which case you can manually select an existing slot, create a new one, or just start keying and let Blender automatically create a new slot for you. If Blender assigns a slot you didn’t want, you can select another slot manually or simply clear the slot selection.

Actions can also be assigned to NLA strips within a data-block’s NLA system. Please see the documentation for the NLA Editor for how to animate data-blocks via the NLA system.

Actions with and without a Manual Frame Range in Dope Sheet.¶

It is possible to manually specify the intended useful frame range of an action via a panel available in the Dope Sheet or the NLA Editor when a channel or NLA track is selected.

Manually specify the intended playback frame range for the action (this range is used by some tools, but does not affect animation evaluation). The manual frame range feature can be toggled with the checkbox.

When the range is set, it is used instead of the actual range occupied by key frames when adding a new track based on the action to NLA. It can also be used by exporters to determine the range of frames to export.

The range is displayed in the background of the editor as diagonal hash fill, to distinguish it from the solid fill of the current playback range.

The frame values are most commonly expected to be integers, but can be fractional.

Specifies that the action is intended to be cyclic over the specified range. The first and last frames of the range should represent the same pose of the cycle one loop apart, i.e. the range should include the duplicated initial key of the loop.

This option signifies intent and does not make the action cycle on its own. However, if Cycle-Aware Keying is enabled, it will automatically enable cyclic extrapolation and set up the loop period for curves newly added to the action.

The properties of the action slot that is used by the currently selected item in the channel list.

The name of the slot.

The data-block type that the slot is intended to animate.

Create and manage your own properties to store data in the action’s data block. See the Custom Properties page for more information.

---

## Action Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/relationship/action.html

**Contents:**
- Action Constraint¶
- Options¶
  - Target¶
  - Action¶
- Example¶

The Action constraint evaluates the location, rotation, and scale inside a certain Action at a certain frame, then applies those to an object or bone.

The frame can either be given directly, or it can be derived from a location coordinate, rotation angle, or scale factor of another object or bone. An example of the latter would be to use frame 0 of the Action if an Empty is at X = 0 and frame 100 if the Empty is at X = 10. If the Empty is then placed at X = 5, the constraint will interpolate this and evaluate frame 50.

The Copy Transforms Constraint may be a sufficient replacement if the Action is very simple.

Drivers allow defining more complex mathematical relationships, again without setting up an Action.

An alternative (if obscure) way of using this constraint is to reference an Action that animates properties of other constraints. The Action constraint will then apply these properties to the constraints that come after it, as long as their names match the ones in the Action.

The object or bone to use for calculating the Action frame. Not needed if Evaluation Time is used.

Allows specifying the Action frame through a number rather than through a transform property of a Target. A value of 0 corresponds to Frame Start while 1 corresponds to Frame End (see below).

Like other properties, the Evaluation Time can be fixed, keyframed, or controlled by a Driver. The latter can further make use of Custom Properties.

Specifies how the evaluated Action transformation is combined with the owner’s original transformation (from its preceding constraints).

The Action’s transformation replaces the owner’s.

The Action’s transformation is applied before the owner’s. The result is the same as the owner’s transformation if it were a child of the Action and there was no constraint.

If the “parent” is non-uniformly scaled and the “child” was originally rotated, the constraint will cause shearing, just like the default Inherit Scale Full setting for bones.

Prevents shearing by scaling the “child” along its own axes instead of the axes of the “parent,” just like the Inherit Scale Aligned setting for bones.

Calculates each transform “channel” – location, rotation, and scale – separately from the others. The difference with Before Original (Aligned) is that the child’s location is only affected by the parent’s location, not by its rotation and scale.

Like Before Original, except the result is the transformation of the Action if it were a child of the owner.

The page of the Copy Transforms Constraint demonstrates the Mix modes with screenshots.

For technical reasons, modes other than After Original (Full) and After Original (Aligned) may not work as expected on objects (not bones) without a parent.

How strongly the constraint affects the owner.

The transform property (location/rotation/scale) and axis to use for calculating the Action frame.

The space in which to evaluate the above Channel.

The values of the Channel that correspond to Frame Start/End. Despite the names, Range Max is allowed to be less than Range Min.

Target rotations are “wrapped around” so they’re always in the range -180° to 180°.

Negative scales don’t work (they are treated as positive scales instead).

Actions can be stored as Assets for reuse. See Pose Library for details.

The Slot inside the Action to use.

By default, the constraint finds Action keyframes for a bone with the same name. Checking Object Action will use the Action’s object keyframes instead.

The opposite – applying a bone animation to a constrained object – is not supported. Neither is applying all bone animations in an Action to all bones in an Armature.

The frames within the Action that correspond to Range Min/Max. Frame End is allowed to be less than Frame Start – this will play the animation in reverse.

---

## Action Editor¶

**URL:** https://docs.blender.org/manual/en/latest/editors/dope_sheet/modes/action.html

**Contents:**
- Action Editor¶
- Header¶
- Action Menu¶

While the Dope Sheet mode lets you work with keyframes of all animation in the scene at the same time, the Action Editor mode focuses on the keyframes inside a single action.

Actions are Blender’s container for animation data. Objects and other animatable data-blocks reference actions to get animated by the animation data inside. Data-blocks can reference one action as their active action and additional actions through Nonlinear Animation tracks.

The Previous/Next Layer (down/up arrows) operators have been removed from the UI in 4.4 and are slated to be removed completely in 5.0. See #119626.

A data-block menu that lets you change – or clear – the object’s active action.

Name of the slot, for display in the user interface. This name combined with the slot’s data-block type is unique within its Action.

The “Merge Animation” and “Separate Slots” operators will only work with directly-assigned actions, and will ignore actions referenced by NLA strips.

This operator merges the animation of all selected objects into the animation of the active object. Since the data is moved and not copied, the source Actions might end up empty and without users. Note that this will not only merge the object level Action, but Actions on related data-blocks as well (See Related data-blocks). As a result of that this operator can also be used to merge Actions of one Object. For example Translation & Rotation and animation on Shape Keys.

This splits all Slots of the Action on the active Object into separate Actions. All users of those Slots will be re-assigned to their respective Action and the newly created Actions are named after the Slot. The source Action will not be deleted, but might end up with 0 users if no Fake User is set.

This moves Slots selected in the Channels Region to a newly created Action. All users of those Slots are re-assigned to the new Action. If more than one Slot is selected, all Slots are moved into a single Action.

Creates a new NLA track below the Action Track and moves the active action into it. This is the same as clicking Push Down Action in the NLA editor.

Creates a new muted NLA track at the bottom of the NLA tracks and moves the active action into it. In effect, this sets the action aside for later use, disabling it so it no longer affects the animation. Later, you can choose to either unmute it again or delete it.

If you click New Action in the data-block menu for an object that already has an active action, that previous action will be stashed automatically.

Both Push Down and Stash leave the object without an active action (meaning the Action Editor becomes empty and the action can no longer be edited). If you still want to make changes to the action, you can select it in the NLA editor and press Tab to enter Tweak Mode.

---

## Add IK to Bone¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/editing/inverse_kinematics.html

**Contents:**
- Add IK to Bone¶
- Remove IK¶

Pose ‣ Inverse Kinematics ‣ Add IK to Bone

Adds an Inverse Kinematics Constraint to the active bone. The operator shows a menu for selecting the target of the constraint:

Creates the constraint without a Target. Only available when no other bone or object is selected.

Creates an Empty at the bone’s tail and uses it as the constraint target. Only available when no other bone or object is selected.

Sets the target to the selected bone that’s not active.

Sets the target to the selected object that’s not active. Either select the object before selecting the Armature and entering Pose Mode, or select it in the Outliner when already in Pose Mode.

The selected object or bone in this case means the first non-active object or bone. The order is determined by the order of creation, not the order of selection.

Pose ‣ Inverse Kinematics ‣ Remove IK

Removes the Inverse Kinematics Constraint from the selected bones.

---

## Animation¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/animation.html

**Contents:**
- Animation¶
- Timeline¶
- Keyframes¶
- F-Curves¶

The Animation section lets you manage settings related to Animation. This includes how editors look and also some different tools properties.

Blender Preferences Animation section.¶

Playback and animations can occur during negative frame ranges.

The minimum number of pixels between grid lines.

Format of timecodes displayed when not displaying timing in terms of frames.

Most compact representation, uses ‘+’ as separator for sub-second frame numbers, with left and right truncation of the timecode as necessary.

Full SMPTE timecode (format is HH:MM:SS:FF).

SMPTE timecode showing minutes, seconds, and frames only – hours are also shown if necessary, but not by default.

Similar to SMPTE (Compact), except that the decimal part of the second is shown instead of frames.

Direct conversion of frame numbers to seconds.

Defines what time range (around the cursor) will be displayed when the View Frame Numpad0 is performed.

The currently displayed time range is preserved.

The number of seconds specified in the Zoom Seconds field will be shown around the cursor.

The number of animation keyframes defined in the Zoom Keyframes field will be shown around the cursor.

These settings control Keyframes which are the building blocks for animations.

Which channels to insert keys at when no keying set is active.

Inset keyframes for an object’s Location.

Inset keyframes for an object’s Rotation.

Inset keyframes for an object’s Scale.

Inset keyframes for an object’s Rotation Mode.

Inset keyframes for Custom Properties.

This will only insert keyframes if the value of the property is different.

When keying manually, skip inserting keys that don’t affect the animation.

Auto-Keying will skip inserting keys that don’t affect the animation.

When an object is using constraints, the object property value does not actually change. Visual Keying will add keyframes to the object property, with a value based on the visual transformation from the constraint.

Enables Auto Keyframe by default for new scenes.

Displays a warning at the top right of the 3D Viewport, when moving objects, if Auto Keyframe is on.

This will only add keyframes to channels of F-Curves that already exist.

Learn more about Auto-Keyframing.

These settings control how F-Curves look and their default behavior.

Controls the opacity of unselected F-Curves against the background of the Graph Editor.

Controls the behavior of automatic curve handles for newly created F-Curves.

Controls the default Interpolation for newly created keyframes.

Controls the default Handle for newly created F-Curves.

Color for X, Y, or Z animation curves (location, scale or rotation) is the same as the color for the X, Y, and Z axis.

Display groups and channels with colors matching their corresponding groups.

Only shows the keyframes markers on the selected curves.

Display F-Curves using Anti-Aliasing and other effects (disable for a better performance).

---

## Animation Editors¶

**URL:** https://docs.blender.org/manual/en/latest/animation/animation_editors.html

**Contents:**
- Animation Editors¶
- Playhead¶
  - Snapping¶
- Playback Controls¶
  - Playback¶
  - Keying¶
  - Auto Keying¶
  - Transport Controls¶
  - Frame Controls¶

Blender provides a set of editors designed for creating, editing, and refining animation. These editors let you work with keyframes, curves, non-linear actions, drivers, video sequencing, and motion tracking as part of the animation pipeline.

Each editor serves a different purpose:

The Dope Sheet organizes and manipulates keyframes across multiple objects and data-blocks.

The Graph Editor provides fine control over F-Curves to refine motion and interpolation.

The Nonlinear Animation (NLA) Editor arranges and layers animation actions for complex sequencing.

The Drivers Editor links properties with expressions for procedural animation.

The Movie Clip Editor supports motion tracking, mask editing, and stabilization, which can be integrated into animation and compositing workflows.

The Video Sequence Editor (VSE) combines rendered animations, image sequences, audio, and effects into a final movie edit.

Together, these editors form the backbone of Blender’s animation system – from quick keyframe adjustments to advanced rigging, motion editing, visual effects integration, and final shot assembly.

This page describes features that are shared across the different animation focused editors.

The Playhead is the blue vertical line showing the current frame number.

It can be moved to a new position by clicking or dragging LMB in the scrubbing area at the top or by click and drag Shift-RMB anywhere in the timeline.

While dragging it can snap to elements of the editor in which it is dragged. - Seconds - Frames - Markers - Strips - Keys

It is only possible to snap to elements that are visible in the editor in which the playhead is dragged. For example having “Strips” enabled but dragging in the Graph Editor will do nothing. Snapping can be toggled during scrubbing by holding down Ctrl.

Snapping to seconds or frames can have a custom increment for example snapping to every third frame. This is always relative to the first frame of the scene and ignores the preview range. In contrast to the other snapping options, seconds and frames will always snap to the closest position, regardless of the snap distance set. When mixing options, the system will first try to snap to elements that are snapped by distance. Only if no element is close enough will it snap to seconds or frames.

You can also move it in single-frame increments by pressing Left or Right or Alt-Wheel. To jump to the beginning or end frame (of the ends of the preview range if that is active) press Shift-Left or Shift-Right.

Playhead snapping helps you position the playhead precisely when scrubbing the timeline by snapping it to specific elements like frames, markers, or keyframes.

Enables or disables snapping behavior when moving the playhead.

The maximum distance (in pixels) the playhead can be from a target before snapping to it.

Specifies which elements the playhead can snap to:

Snap to frame intervals.

Snap to second intervals.

Snap to timeline markers.

Snap to animation keyframes.

Snap to the start and end points of strips (e.g. in the Video Sequencer).

The interval in frames between each snap point when using the Frames target.

The interval in seconds between each snap point when using the Seconds target.

The Playback Controls region of the animation editors (such as the Timeline, Dope Sheet, Graph Editor, and NLA Editor) contains controls and options related to playback, keying, auto keyframing, and transport.

These settings allow you to:

Control how animations are previewed and synchronized with audio.

Insert and manage keyframes through keying sets and auto keying.

Navigate the timeline using playback and transport controls.

Adjust frame ranges and preview specific segments of the animation.

The footer is shared across animation editors to provide a consistent workflow for animators, whether they are editing keyframes, adjusting curves, or sequencing actions.

Properties for how animations are played.

3D Viewport red FPS.¶

If animation playback can’t keep up with the desired Frame Rate, the actual frame rate (shown in the top left corner of the 3D Viewport) will turn red, and the Sync option determines how the situation should be handled.

Play every frame, even if this results in the animation playing slower than intended.

Drop frames if playback becomes slower than the scene’s frame rate.

Drop frames if playback becomes too slow to remain synced with audio.

Play bits of the sound in the animation (if there is any) while you drag the Playhead around.

Uncheck to mute all sound.

Don’t allow moving the Playhead outside of the Frame Range using the mouse.

Automatically pan the view to catch up when the Playhead goes off screen.

Which editors to update on each animation frame. If an editor is unchecked, it’ll only be updated once playback stops (with some exceptions where it’ll update on each frame anyway). When starting playback in either the Graph Editor, Dope Sheet or the NLA Editor, all editors will play back regardless of the settings. This is a feature requested by animators to easily play back all views.

Display and allow setting fractional frame values for the current frame.

Set the scene’s start/end frame to the current frame. If the Preview Range is active (see Frame Controls), that one is changed instead.

The Keying popover contains options that affect keyframe insertion.

The name of this popover will change depending on the active keying set.

Timeline Keying Sets.¶

A Keying Set is a named collection of animatable properties. If you select one and then press I while not hovering over any input field, Blender will create keyframes for the properties in that keying set.

If you don’t have a keying set selected, you’ll get keyframes on a default set of properties instead (e.g. Location/Rotation/Scale for objects).

There are a number of predefined keying sets, but you can also create your own in the Keying Sets panel.

Insert keyframes on the current frame.

Delete keyframes on the current frame.

The keyframe type for newly created keyframes.

When inserting keyframes into trivially cyclic curves, special handling is applied to preserve the cycle integrity (most useful while tweaking an established cycle):

If a key insertion is attempted outside of the main time range of the cycle, it is remapped back inside the range.

When overwriting one of the end keys, the other one is updated accordingly.

In addition, when adding a new curve into an action with a Manual Frame Range and Cyclic Animation enabled, the curve is automatically made cyclic with the period matching the frame range. For convenience, this check and conversion is also done before adding the second keyframe to such a curve.

When the record button () is enabled, Blender will automatically create keyframes on the current frame whenever you transform an object or bone in the 3D Viewport (or change one of its transform properties in the Properties Editor).

One special use case is to record a camera path as you fly through the scene. See Fly/Walk Navigation.

Auto Keying only works for transform properties (Location, Rotation, Scale). It won’t create a keyframe if you change, say, the color of a material – you still have to do that manually.

Add or replace keyframes as needed.

Only replace existing keyframes.

By default, Auto Keying will create keyframes even for properties that are not in the active keying set. Use this checkbox to change that.

Adds a new NLA Track for every pass made over the animation to allow non-destructive tweaking.

These buttons are used to set the current frame and control playback.

Sets the Playhead to the start of the frame range.

Moves the Playhead to the previous keyframe.

Starts playing the animation in reverse.

Starts playing the animation.

Stops playing the animation.

Moves the Playhead to the next keyframe.

Sets the Playhead to the end of the frame range.

Jumps the playhead backwards by a user-configured delta.

Jumps the playhead forward by a user-configured delta.

Additionally, there is a menu accessible to the right of the Jump by Delta buttons where their delta can be set:

The number of the frame that’s currently being displayed in the 3D Viewport. This is also the location of the Playhead.

The Preview Range is an alternative Frame Range that you can use for focusing on a particular part of the animation. It lets you repeatedly play a short segment without having to manually rewind or change the frame range of the entire scene.

This range only affects the preview in the 3D Viewport; it doesn’t affect rendering.

The boundaries of the Preview Range are shown in dark orange. You can quickly configure and enable it by pressing P and dragging a box. To disable it, you can press Alt-P.

The start/end frame of the scene (or the preview range, if active).

---

## Apply¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/editing/apply.html

**Contents:**
- Apply¶

Conversely, you may define the current pose as the new rest pose (i.e. “apply” current transformations to the Edit Mode). When you do so, the skinned objects/geometry is also reset to its default, non-deformed state, which generally means you will have to skin it again.

Same as Pose as Rest Pose but only applies to selected bones.

Applies the position of the bone after Constraints; allowing the constraints to be deleted and the bones will remain in their constrained positions.

Assign the current values of custom properties as their defaults, for use as part of the rest pose state in NLA track mixing.

---

## Armature Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/relationship/armature.html

**Contents:**
- Armature Constraint¶
- Options¶
  - Bones¶

The Armature constraint transforms an “owner” object or bone based on the weighted pose transformations of one or more “target” bones. It’s similar to the Armature Modifier, which performs this operation for every vertex in a mesh.

Unlike the modifier, the constraint also uses bones whose Deform option is disabled.

The Child Of Constraint is an alternative if there’s only one parent. Unlike with the Armature constraint, this parent can also be an object.

Armature constraint.¶

Prevents the owner from shrinking when the target bones rotate relative to each other.

Uses Envelopes to weaken the influence of target bones that are further away. For best results, set the Weight of all bones to 1.0.

Unlike the modifier, the constraint does not automatically detect nearby bones. Every bone has to be added manually.

By default, the constraint uses the rest location of the owner bone to find nearby envelopes and B-Bone segments. This option uses the bone’s current location instead (so including the pose transformation and prior constraints).

Objects don’t have a rest location, so for them, the constraint always uses the current location.

Adds a new entry to the Bones list.

Normalizes the Weights in the Bones list so they add up to 1.0.

How strongly the constraint affects the owner.

The list of target bones used to transform the owner.

The armature object containing the bone. Unlike the modifier, the constraint can use bones from different armatures.

The name of the bone.

Removes the entry from the list.

Weight associated with the bone. With the modifier, this weight would come from a vertex group instead.

---

## Armature Deform Parent¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/skinning/parenting.html

**Contents:**
- Armature Deform Parent¶
- With Empty Groups¶
  - Example¶
- With Automatic Weights¶
- With Envelope Weights¶

Object Mode and Pose Mode

Object/Pose ‣ Parent ‣ Armature Deform

Armature Deform Parenting is a way of creating and setting up an Armature Modifier.

To use Armature Deform Parenting you must first select all the child objects that will be influenced by the armature and then lastly, select the armature object itself. Once all the child objects and the armature are selected, press Ctrl-P and select Armature Deform in the Set Parent To pop-up menu.

The armature will be the parent object of all the other child objects and each child object will have an Armature Modifier with the armature associated (Object field).

Bone associated with Mesh Object.¶

When parenting it will create empty vertex groups on the child objects (if they do not already exist) for and named after each deforming bone in the armature. The newly created vertex groups will be empty. This means they will not have any weights assigned. Vertex groups will only be created for bones which are setup as deforming (Properties ‣ Bone ‣ Deform Panel).

You can then manually select the vertices and assign them to a particular vertex group of your choosing to have bones in the armature influence them.

Choose this option if you have already created (and weighted) all the vertex groups the mesh requires.

For example, if you have an armature which consists of three bones named “BoneA”, “BoneB” and “BoneC” and cube mesh called “Cube”. If you parent the cube to the armature, the cube will get three new vertex groups created on it called “BoneA”, “BoneB” and “BoneC”. Notice that each vertex group is empty.

Cube in Edit Mode using Armature Deform with empty groups.¶

With Automatic Weights parenting works similar to With Empty Groups, but it will not leave the vertex groups empty. It calculates how much influence a particular bone would have on vertices based on the distance from those vertices to a particular bone (“bone heat” algorithm). This influence will be assigned as weights in the vertex groups.

This method of parenting is certainly easier to setup, but it can often lead to armatures which do not deform child objects in ways you would want. Overlaps can occur when it comes to determining which bones should influence certain vertices when calculating influences for more complex armatures and child objects. Symptoms of this confusion are that when transforming the armature in Pose Mode, parts of the child objects do not deform as you expect; If Blender does not give you the results you require, you will have to manually alter the weights of vertices in relation to the vertex groups they belong to and have influence in.

Works in a similar way to With Automatic Weights. The difference is that the influences are calculated based on the Bone Envelopes settings. It will assign a weight to each vertex group the vertices that is inside its bone’s influence volume, depending on their distance to this bone.

This means newly included/excluded vertices or new envelope settings will not be taken into account. You will have to apply Armature Deform With Envelope Weights parenting again.

If you want the envelope setting to be used instantly, bind the Armature Modifier to Bone Envelopes.

Two sets of armatures, each with three bones.¶

If you had defined vertex groups using same names as skinned bones, their content will be completely overridden by both Automatic and Envelope Weights. In this case With Empty Groups could be used instead.

Vertex Groups for Bones.

---

## Armature Structure¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/structure.html

**Contents:**
- Armature Structure¶
- Chains of Bones¶

Example of a very basic armature.¶

Armatures mimic real skeletons. They are made out of bones, which are (by default) rigid elements. But you have more possibilities than with real skeletons: In addition to the “natural” rotation of bones, you can also move and even scale them! And your bones do not have to be connected to each other; they can be completely free if you want. However, the most natural and useful setups imply that some bones are related to others, forming so-called “chains of bones”, which create some sort of “limbs” in your armature, as detailed in Chains of Bones.

The bones inside an armature can be completely independent from each other (i.e. the modification of one bone does not affect the others). But this is not often a useful set up: To create a leg, all bones “after” the thigh bone should move “with” it in a well-coordinated manner. This is exactly what happens in armatures by parenting a bone to the next one in the limb, you create a “chains of bones”. These chains can be ramified. For example, five fingers attached to a single “hand” bone.

An armature with two chains of bones.¶

Bones are chained by linking the tip of the parent to the root of the child. Root and tip can be connected, i.e. they are always exactly at the same point; or they can be free, like in a standard parent-child object relationship.

A given bone can be the parent of several children, and hence be part of several chains at the same time.

The bone at the beginning of a chain is called its root bone, and the last bone of a chain is the tip bone (do not confuse them with similar names of bones’ joints!).

Chains of bones are a particularly important topic in posing (especially with the standard forward kinematics versus “automatic” inverse kinematics posing techniques). You create/edit them in Edit Mode, but except in case of connected bones, their relationships have no effect on bone transformations in this mode (i.e. transforming a parent bone will not affect its children).

The easiest way to manage bones relationships is to use the Relations panel in the Bone tab.

---

## Bendy Bones¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/properties/bendy_bones.html

**Contents:**
- Bendy Bones¶
- Technical Details¶
- Display¶
- Rest Pose¶
- Example¶
- Options¶
  - Custom Handles¶

Bendy Bones (B-Bones) are an easy way to replace long chains of many small rigid bones. A common use case for curved bones is to model spine columns or facial bones.

Blender treats the bone as a section of a Bézier curve passing through the bones’ joints. Each of the Segments will bend and roll to follow this invisible curve representing a tessellated point of the Bézier curve. The control points at each end of the curve are the endpoints of the bone. The shape of the B-Bones can be controlled using a series of properties or indirectly through the neighboring bones (i.e. first child and parent). The properties construct handles on either end of the bone to control the curvature.

When using the B-bone as a constraint target Data ID offers an option to follow the curvature.

However, if the bone is used as a target rather than to deform geometry, only Armature and Copy Transforms constraints will use the full transformation including roll and scale.

You can see these segments only if bones are visualized as B-bones.

When not visualized as B-Bones, bones are always shown as rigid sticks, even though the bone segments are still present and effective. This means that even in e.g. Octahedron visualization, if some bones in a chain have several segments, they will nonetheless smoothly deform their geometry.

The initial shape of a B-Bone can be defined in Edit Mode as a rest pose of that bone. This is useful for curved facial features like curved eyebrows or mouths.

B-Bones have two sets of the Bendy Bone properties – one for Edit Mode (i.e. the Rest Pose/Base Rig) and another for Pose Mode – adding or multiplying together their values to get the final transforms.

Bones with just one segment in Edit Mode.¶

The Bézier curve superposed to the chain, with its handles placed at bones’ joints.¶

The same armature in Object Mode.¶

In Fig. Bones with just one segment in Edit Mode. we connected three bones, each one made of five segments.

Look at Fig. The same armature in Object Mode., we can see how the bones’ segments smoothly “blend” into each other, even for roll.

An armature in Pose Mode, B-Bone visualization: Bone.003 has one segment, Bone.004 has four, and Bone.005 has sixteen.¶

The number of segments, which the given bone is subdivided into. Segments are small, rigid linked child bones that interpolate between the root and the tip. The higher this setting, the smoother “bends” the bone, but the heavier the pose calculations.

Controls the visible thickness of the bone segments when the armature is rendered in the B-Bones mode.

Controls how vertices are weighted to the individual segments of a B-Bone for deformations:

A fast mapping that works well for B-Bones with a straight or gently curved rest pose.

A slower mapping that improves deformations for B-Bones with a strongly curved rest pose. This should be used selectively when needed.

Straight vs Curved vertex mapping on a B-Bone with a strongly curved rest pose.¶

Applies offsets to the curve handle positions on the plane perpendicular to the bone’s primary (Y) axis. As a result, the handle moves per axis (XZ) further from its original location, causing the curve to bend.

The roll value (or twisting around the main Y axis of the bone) is interpolated per segment, between the start and end roll values. It is applied as a rotational offset on top of the rotation defined by the handle bones.

If enabled, the Roll Out value of the Start Handle bone (connected parent by default) will be implicitly added to the Roll In setting of the current bone.

Scaling factors that adjust the thickness of each segment for the X and Z axes, or introduce non-uniform spacing along the Y axis. Similar to Roll it is interpolated per segment.

Since all segments are still uniformly scaled in the Y direction to fit the actual length of the curve, only the ratio between Scale In Y and Scale Out Y actually matters.

The Ease In/Out number fields, change the “length” of the “auto” Bézier handle to control the “root handle” and “tip handle” of the bone, respectively. These values are proportional to the default length, which of course automatically varies depending on bone length, angle with the reference handle, and so on.

Although easing is a scale-like value, the Edit Mode and Pose Mode versions of the values are added, so they get corresponding start values of 1 and 0 by default.

Bone.004 with default In and Out (1.0).¶

Bone.004 with In at 2.0, and Out at 0.0.¶

If enabled, the final easing values are implicitly multiplied by the corresponding Scale Y values.

B-Bones can use custom bones as their reference bone handles, instead of only using the connected parent/child bones.

Specifies the type of the handle from the following choices:

The connected parent (or first connected child) of the bone is chosen as the handle. Calculations are done according to the Absolute handle type below.

The Bézier handle is controlled by the position of the head (tail) of the handle bone relative to the head (tail) of the current bone. Note that for this to work, there must be a nonzero distance between these bones. If the handle is also a B-Bone, additional processing is applied to further smooth the transition, assuming that the bones in effect form a chain.

The Bézier handle is controlled by the offset of the head (tail) of the handle bone from its rest pose. The use of this type is not recommended due to numerical stability issues near zero offset.

The Bézier handle is controlled by the orientation of the handle bone, independent of its location.

For types other than Automatic, a bone to use as handle has to be manually selected. Switching to a custom handle type without selecting a bone can be used to effectively disable the handle.

It is valid for two bones to refer to each other as handles – this correlation is applied in connected chains with Automatic handles.

If enabled, the final Scale and/or Ease values are multiplied by the corresponding local scale channels of the handle bone. This step is applied independently of Scale Easing and doesn’t interact with it, i.e. enabling Y and Scale Easing doesn’t replace the Ease toggle. These toggles are a more efficient replacement for up to eight trivial drivers passing segment scale data from the handle bones into the B-Bone option properties.

The “BBone Shape” Keying Set includes all Bendy Bones properties.

Visualization of the Bendy Bones properties.¶

From Left: 1) Curve X/Y offsets, 2) Scale In/Out, 3) Roll In/Out

---

## Bone Collections¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/bone_collections.html

**Contents:**
- Bone Collections¶
- Visibility¶
- Library Overrides¶
  - Limitations¶
  - How It Works¶
- Some history¶

Bone Collections group the bones of an Armature into named collections. The armature is the owner of these collections, so they are available in all modes. Bone Collections are identified by their name, which are unique within the Armature. Bone Collections can be nested inside other Bone Collections to create an organized hierarchy for complex rigs.

In the text below, “collection” is understood to refer to “bone collection”; Scene Collections are not described here.

Bone Collections can be managed via the Armature and Bone property panels.

Bone Collections can be shown & hidden via the list in the Armature properties, as well as via the list in the Bone properties. Bone visibility is determined by the visibility of its collections, its own ‘solo’ and ‘hidden’ properties:

If the bone itself is marked as ‘hidden’, it is invisible regardless of the bone collections.

If a parent collection is hidden, child collections will also be hidden; same is true for soloed collections.

A bone is visible when it is contained in any visible collection.

If a collection is soloed, it will be visible regardless of the collection’s ‘hidden’ property.

A bone that is not assigned to any bone collection is visible; otherwise it would be impossible to select it & assign it to a collection.

Bone collections can be added using library overrides. For this to work, both the armature Object and the Armature itself need to be overridden.

There are a few limitations when it comes to bone collections & overrides:

Only bone collections that are local to the current blend file can be edited.

Bone collections that already existed on the linked-in Armature are read-only, and only their visibility can be toggled. Those visibility changes won’t be saved, though.

Custom properties of overridden bone collections cannot be edited in the properties panel. Python access is fine; this is just a current limitation of Blender’s UI code.

Bone collections added via overrides are ‘anchored’ to the preceding collection, by name. Here is an example. The italic collections are defined on the linked Armature in armature.blend. The bold ones are added by overrides in armature_shot_47.blend.

Left Pinky (anchored to “IK Controls”)

Right Pinky (anchored to “Left Pinky”)

Now if the Armature in armature.blend gets updated with two more collections it might look like this:

After reloading armature_shot_47.blend, it will look like this:

Left Pinky (still anchored to “IK Controls”)

Right Pinky (still anchored to “Left Pinky”)

Bone Collections were introduced in Blender 4.0, as a replacement for armature layers and bone groups. Bone Collections are owned by the Armature, so they are available in all modes. To contrast, bone groups were stored on the object’s pose, and thus were not available in armature edit mode.

---

## Bone Collections¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/properties/bone_collections.html

**Contents:**
- Bone Collections¶
- Specials¶
- Assign & Select¶
- Moving Bones between Collections¶
- Custom Properties¶

Bone Collections were introduced in Blender 4.0 as replacement of Armature Layers and Bone Groups. Bone colors are now managed directly on the bone.

Object, Pose, and Edit Modes

Properties ‣ Armature ‣ Bone Collections

The Bone Collections panel in the Armature properties.¶

This panel contains a Tree View to manage Bone Collection From this panel, Bone Collections can be created, deleted, re-arranged, and more.

Collections can be renamed by double clicking on the name, or right clinking and selecting Rename. To nest a collection inside an existing collection, click and drag the name onto another collection’s name. Child collection can also be made by RMB and selecting “Add Child Collection”.

To the right of the name gives a few controls of the collection:

Bones in this collection will be visible in the 3D Viewport.

Show only this bone collection, and others also marked as “solo”.

Further more, collection that are not empty will have a dot to indicate the collection has bones assigned to it.

The Bone Properties panel gives a slightly different view on the bone’s collections. See Bone Relations.

Unhides any hidden bone collections.

Clear the ‘solo’ setting on all bone collections

Remove all bone collections that have neither bones nor children. This is done recursively, so bone collections that only have unused children are also removed.

Properties ‣ Armature ‣ Bone Collections

Pose ‣ Bone Collections ‣ …

Assigns the selected bones to the active bone collection.

Removes the selected bones from the active bone collection.

Selects the bones in the active bone collection.

Deselects the bones in the active bone collection.

Individual bones can also be unassigned from their collections via the Bone Relations panel.

For setting up custom selection sets of bones, take a look at the Selection Sets add-on. It is bundled with Blender.

Blender should be in Edit Mode or Pose Mode to move bones between collections. Note that as with objects, bones can be assigned to in several collections at once.

Shows a list of the Armature’s editable bone collections. Choosing a bone collection unassign the selected bones from all other bone collections, then assigns them to the chosen one.

Available as Pose ‣ Move to Collection (Pose Mode) Armature ‣ Move to Collection (Edit Mode), and M (either mode).

Shows a list of the Armature’s editable bone collections. The collections that the active bone is assigned to are prefixed with a -, and choosing those will unassign all selected bones from that collection. Similarly, choosing a bone collection prefixed with a + will assign all selected bones to that collection.

Available as Pose ‣ Bone Collections (Pose Mode) Armature ‣ Bone Collections (Edit Mode), and Shift-M (either mode).

The above operators will only show the editable bone collections. When the Armature is linked, its bone collections will be read-only. New bone collections can still be added via library overrides; only those will be editable.

See Library Overrides of Bone Collections.

Create and manage your own properties to store data in the Bone Collection’s data-block. See the Custom Properties page for more information.

---

## Bone Properties¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/properties/index.html

**Contents:**
- Bone Properties¶

Object Mode, Edit Mode and Pose Mode

When bones are selected (hence in Edit Mode and Pose Mode), their properties are shown in the Bone tab of the Properties. This shows different panels used to control features of each selected bone; the panels change depending on which mode you are working in.

---

## Bone Roll¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/bone_roll.html

**Contents:**
- Bone Roll¶
- Recalculate Roll¶
- Set Roll¶
- Clear Roll¶

The bone roll is a part of a bone’s rest pose defining its default rotation around the bone’s length. You can control the bone roll in Edit Mode.

Armature ‣ Bone Roll ‣ Recalculate Roll

Automatically align the roll of all selected bones to various points of reference.

Align the roll of the selected bones relative to the axis defined by the bones and their parent. If a bone has no parent, use the first child as a point of reference instead, even if that child is not connected and another one is. For bones with no parent and no children, this option does nothing.

Align the roll of the selected bones such that their Z axis points towards the chosen global axis.

Align the roll of the selected bones such that their Z axis points where the active bone’s Z axis is currently pointing.

Align the roll of the selected bones such that their Z axis points at the viewport’s forward/backward axis, basically the user’s eyes.

Align the roll of the selected bones such that their Z axis points at the 3D cursor.

Change the result by 180°.

Change the result by 180° when needed in order to force the absolute roll value below 90°. For example, for an initial result of 160°, this option will instead flip that to -20°.

Armature ‣ Bone Roll ‣ Set Roll

Tweak the roll of all selected bones.

Armature ‣ Bone Roll ‣ Clear Roll

Set the roll of all selected bones to 0°.

---

## Bone Structure¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/structure.html

**Contents:**
- Bone Structure¶
- Roll¶
- Bones Influence¶

The elements of a bone.¶

They have three elements:

The “start joint” named root or head.

And the “end joint” named tip or tail.

With the default armature in Edit Mode, you can select the root and the tip, and move them as you do with mesh vertices.

Both root and tip (the “joints”) define the bone by their respective position.

They also have a radius property, only useful for the envelope deformation method (see below).

Activating the Axes checkbox will show local axes for each bone’s tip. The Y axis is always aligned along the bone, oriented from root to tip, this is the “roll” axis of the bones.

A bone in Envelope visualization, in Edit Mode.¶

Basically, a bone controls a geometry when vertices “follow” the bone. This is like how the muscles and skin of your finger follow your finger-bone when you move a finger.

To do this, you have to define the strength of influences a bone has on a certain vertex.

The simplest way is to have each bone affecting those parts of the geometry that are within a given range from it. This is called the envelope technique, because each bone can control only the geometry “enveloped” by its own influence area.

If a bone is visualized as Envelope, in Edit Mode and in Pose Mode you can see the area of influence, which depends on:

The distance property and

the root’s radius and the tip’s radius.

Our armature in Envelope visualization, in Pose Mode.¶

All these influence parameters are further detailed in the skinning pages.

---

## Camera Solver Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/motion_tracking/camera_solver.html

**Contents:**
- Camera Solver Constraint¶
- Usage¶
- Options¶

The Camera Solver constraint makes a Blender camera imitate the motion of a real-world camera.

Start by loading a video file into the Movie Clip Editor and using motion tracking to track at least eight markers in the real-world scene. Then use Solve Camera/Object Motion to reconstruct the motion of the physical camera, and finally add this constraint to a Blender camera.

Camera Solver constraint.¶

Whether to follow the physical camera of the scene’s Active Clip. If unchecked, a selector appears for choosing another clip.

Replaces the constraint by a set of equivalent keyframes.

How strongly the constraint affects the Blender camera.

---

## Child Of Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/relationship/child_of.html

**Contents:**
- Child Of Constraint¶
- Options¶
- Example¶

The Child Of constraint transforms an object or bone as though it were a child of another object or bone.

The main advantage over a regular parent-child relationship is that the constraint has an animatable Influence, which makes it possible to switch to different parents over time.

This same Influence can also be used to mix multiple Child Of constraints and create a weighted average between multiple parents. However, if those parents are bones, the Armature Constraint may be a better choice.

While this constraint can “parent” a bone to another, it’s not very suited for creating chains of bones. Notably, it can’t emulate connected bones (where the tip of the parent always coincides with the base of the child).

Child Of constraint.¶

The parent object or bone.

The location axes of the child to affect.

The rotation axes of the child to affect.

The scale axes of the child to affect.

If the child’s transform is correct with the constraint disabled but incorrect with the constraint enabled, click this button to fix it.

Tells the constraint that the child’s current transform with the constraint disabled is its correct relative transform. Once the constraint is enabled again, this transform will be applied as an offset to the parent to determine the child’s final transform.

How strongly the constraint affects the owner.

---

## Clamp To Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/tracking/clamp_to.html

**Contents:**
- Clamp To Constraint¶
- Options¶
- Example¶

The Clamp To constraint snaps an object or bone to a Curve. Specifically, it works as follows:

If no explicit Main Axis is chosen, the constraint picks one automatically based on the longest side of the Curve’s bounding box.

Using this axis, it compares the original coordinate of the object or bone to the minimum and maximum coordinates of the Curve, and remaps it to the range 0-1 accordingly.

This remapped coordinate is then used as a “curve time” to determine the position along the Curve, where a value of 0 corresponds to the first control point and 1 to the last.

Unless the Curve is a perfectly straight line, the object’s/bone’s coordinate along the Main Axis will likely change.

If the object or bone moves along the Curve in the opposite direction than the expected one, use Switch Direction to flip the order of the Curve’s control points.

While the object’s/bone’s original coordinate is evaluated in world space, the Curve’s bounding box is evaluated in the Curve’s local space.

This means that, if the Curve originally stretched from -5 to 10 on the global X axis but was then moved, rotated, and scaled so that it now stretches from 20 to 90 on the global Z axis, the Main Axis will still be chosen as X, and the object/bone still needs to move from -5 to 10 on the global X axis to be successfully moved along the Curve.

For the most intuitive results, keep the Curve object at the default rotation.

Bézier handles and control point radii are included in the calculation of the bounding box.

The Follow Path Constraint can not just position an object/bone on a Curve, but also orient it along the Curve’s direction.

Clamp To constraint.¶

The Curve object to snap to.

The axis for determining the constraint owner’s coordinate and the Curve’s minimum/maximum coordinates.

When disabled, the constraint owner will stop at the start/end of the Curve when it leaves the range of the Curve’s bounding box. When enabled, it will jump to the opposite side and begin another run along the Curve.

This option is mainly useful for Curves that are also cyclic (closed).

How strongly the constraint affects the object.

---

## Clear Transform¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/editing/clear.html

**Contents:**
- Clear Transform¶

Pose ‣ Clear Transform

Once you have transformed some bones, if you want to return to their rest position, just clear their transformations.

Resets location, rotation, and scaling of selected bones to their default values.

Clears individual transforms.

Note that in Envelope visualization, Alt-S does not clear the scale, but rather scales the Distance influence area of the selected bones. (This is also available through the Pose ‣ Scale Envelope Distance menu entry, which is only effective in Envelope visualization, even though it is always available…)

Clears the transforms to their keyframe state.

Operate on just the selected or all bones.

---

## Constraints¶

**URL:** https://docs.blender.org/manual/en/latest/scene_layout/object/editing/constraints.html

**Contents:**
- Constraints¶
- Add Constraint (with Targets)¶
- Copy Constraints to Selected Objects¶
- Clear Object Constraints¶

Operators for working with an object’s Constraints.

Object Mode and Pose Mode

Object ‣ Constraint ‣ Add Constraint (with Targets)

Adds a constraint to the active object. The type of constraint must be chosen from a pop-up menu, though it can be changed later from the Add Constraint (with Targets) Adjust Last Operation panel. If there is an other object selected besides the active one, that object will be the constraint target (if the chosen constraint accepts targets).

When using a bone from another armature as the target for a constraint, the tool will look inside the non-active armature and use its active bone, provided that armature is in Pose Mode.

Object Mode and Pose Mode

Object ‣ Constraint ‣ Copy Constraints to Selected Objects

Copies the active object Constraints to the rest of the selected objects.

Object Mode and Pose Mode

Object ‣ Constraint ‣ Clear Object Constraints

Removes all Constraints of the selected object(s).

---

## Copy/Paste Pose¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/editing/copy_paste.html

**Contents:**
- Copy/Paste Pose¶

Pose ‣ Copy Pose, Pose ‣ Paste Pose, Pose ‣ Paste Pose Flipped

Ctrl-C, Ctrl-V, Shift-Ctrl-V

Blender allows you to copy and paste a pose, either through the Pose menu, or by using hotkeys.

Copy the current pose of selected bones into the pose buffer.

Paste the buffered pose to the currently posed armature.

Paste the X axis mirrored buffered pose to the currently posed armature.

Here are important points:

This tool works at the Blender session level, which means you can use it across armatures, scenes, and even files. However, the pose buffer is not saved, so you lose it when you close Blender.

There is only one pose buffer.

Only the selected bones are taken into account during copying (i.e. you copy only selected bones’ pose).

During pasting, on the other hand, bone selection has no importance. The copied pose is applied on a per-name basis (i.e. if you had a forearm bone selected when you copied the pose, the forearm bone of the current posed armature will get its pose when you paste it – and if there is no such named bone, nothing will happen…).

What is copied and pasted is in fact the position, rotation or scale of each bone, in its own space. This means that the resulting pasted pose might be very different from the originally copied one, depending on:

The rest position of the bones.

And the current pose of their parents.

The rest position of the original armature.¶

The rest position of the destination armature.¶

The first copied pose (note that only two bones are selected and hence copied).¶

The pose pasted on the destination armature.¶

The pose mirror-pasted on the destination armature.¶

The same pose as above is copied, but this time with all bones selected.¶

The pose pasted on the destination armature.¶

The pose mirror-pasted on the destination armature.¶

---

## Copy Location Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/transform/copy_location.html

**Contents:**
- Copy Location Constraint¶
- Options¶
- Examples¶
  - Bones and Vertex Groups¶
  - Solar System¶

The Copy Location constraint forces an object or bone to match the location of a target.

This constraint has no effect on connected bones as their position is determined by their parent bone.

Copy Location constraint.¶

The object or bone whose location to copy.

The axes for which to copy location coordinates.

The axes for which invert the sign (so a coordinate of 10 becomes -10 and vice versa).

When enabled, the target’s current position (from all its constraints) is not copied over, but added to the owner’s original position (from its preceding constraints).

The spaces for retrieving the coordinates from the target and for applying them to the owner.

How strongly the constraint affects the owner.

This video shows the effect of the Head/Tail setting when targeting a bone, as well as the Vertex Group setting when targeting a mesh.

In the animation below, the camera follows the moon as it orbits the Earth, switches to following the Earth as it orbits the Sun, and finally moves to a fixed location for showing the Sun. This is done using two Copy Location constraints – one for the moon and one for the Earth – with animated Influence values for smoothly disabling one while enabling the other.

---

## Copy Rotation Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/transform/copy_rotation.html

**Contents:**
- Copy Rotation Constraint¶
- Options¶
- Example¶

The Copy Rotation constraint forces an object or bone to match the rotation of a target.

Copy Rotation constraint.¶

The object or bone whose rotation to copy. If this target has a sheared transformation, this is first undone.

The Euler order to use during the copy operation. Defaults to the order of the owner.

The axes for which to copy rotation angles.

The axes for which invert the sign (so an angle of 10° becomes -10° and vice versa).

Specifies how the target’s current rotation (from all its constraints) is combined with the owner’s original rotation (from its preceding constraints).

The target’s angles replace the owner’s.

The target angles are added to the owner’s.

The target’s rotation is applied before the owner’s. The result is the same as the owner’s rotation if it were a child of the target and there was no constraint.

The target’s rotation is applied after the owner’s. The result is the same as the target’s rotation if it were a child of the owner and there was no constraint.

This replicates the behavior of the original Offset checkbox. It was intended to be similar to Before Original, but does not work correctly with multiple axes and is thus deprecated.

The spaces for retrieving the angles from the target and for applying them to the owner.

How strongly the constraint affects the owner.

---

## Copy Scale Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/transform/copy_scale.html

**Contents:**
- Copy Scale Constraint¶
- Options¶
- Example¶

The Copy Scale constraint forces an object or bone to match the scale of a target.

Copy Scale constraint.¶

The object or bone whose scale to copy.

The axes for which to copy scale factors.

Raises the target’s scales to the specified power. This is done before applying the Offset.

Instead of applying the scale for each individual axis, apply a uniform scale to all axes that achieves the same overall change in volume.

When enabled, the target’s current scale (from all its constraints) is not copied over, but multiplied with the owner’s original scale (from its preceding constraints).

When Offset is enabled, don’t use multiplication, but add the owner’s scales minus 1. This option is kept for backwards compatibility, but generally makes no sense and should not be used.

The spaces for retrieving the scales from the target and for applying them to the owner.

How strongly the constraint affects the owner.

Depending on the settings, Power can be used instead of Influence to get a better-looking result.

To copy the scale from one axis of the target to all axes of the owner, disable the other axes, enable Make Uniform, and set Power to 3.

---

## Copy Transforms Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/transform/copy_transforms.html

**Contents:**
- Copy Transforms Constraint¶
- Options¶
- Example¶

The Copy Transforms constraint forces an object or bone to match the location, rotation, and scale of a target.

Copy Transforms constraint.¶

The object or bone whose transforms to copy.

Removes shearing from the Target’s transformation before Mixing, ensuring it consists purely of translation, rotation, and scale.

If a child bone is rotated and its parent is non-uniformly scaled, it will get sheared, and so will any object that copies its transformation (middle cube). Use Remove Target Shear to fix this (right cube).¶

Specifies how the target’s current transformation (from all its constraints) is combined with the owner’s original transformation (from its preceding constraints).

The target’s transformation replaces the owner’s.

The target’s transformation is applied before the owner’s. The result is the same as the owner’s transformation if it were a child of the target and there was no constraint.

If the “parent” is non-uniformly scaled and the “child” was originally rotated, the constraint will cause shearing, just like the default Inherit Scale Full setting for bones.

Prevents shearing by scaling the “child” along its own axes instead of the axes of the “parent,” just like the Inherit Scale Aligned setting for bones.

Calculates each transform “channel” – location, rotation, and scale – separately from the others. This is the same as having a Copy Location constraint, a Copy Rotation constraint, and a Copy Scale constraint (all using Offset/Before Original). The result may be slightly different with sheared inputs, however.

The difference with Before Original (Aligned) is that the child’s location is only affected by the parent’s location, not by its rotation and scale.

Like Before Original, except the result is the transformation of the target if it were a child of the owner.

With Before Original (Full), the cone is scaled along the cube’s Y axis, causing shearing.¶

With Before Original (Aligned), the cone is scaled along its own Y axis, preventing shearing.¶

With Before Original (Split Channels), the cone’s location is independent of the cube’s rotation and scale.¶

The spaces for retrieving the transforms from the target and for applying them to the owner.

How strongly the constraint affects the owner.

---

## Custom Properties¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/properties/custom_properties.html

**Contents:**
- Custom Properties¶

Bone ‣ Custom Properties

See the Custom Properties page for more information.

---

## Damped Track Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/tracking/damped_track.html

**Contents:**
- Damped Track Constraint¶
- Options¶
- Example¶

The Damped Track constraint makes an object or bone point towards a certain target. It’s typically called “Look At” or “Aim” in other 3D software.

The word “damped” means that the constraint uses a pure swing rotation to minimize rolling around the tracking axis. This is in contrast to the Track To Constraint which applies an “Up” axis in addition to the tracking.

Damped Track constraint.¶

The object or bone to point towards.

The local axis of the owner that should point at the target. For bones, this should typically be Y.

A negative axis will make the owner point away from the target instead.

How strongly the constraint affects the owner.

---

## Deform¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/properties/deform.html

**Contents:**
- Deform¶
- Envelope¶

In this panel you can set deformation options for each bone.

Toggling the checkbox in the panel header off, prevents the bone from deforming the geometry at all, overriding any weights that it might have been assigned before; it mutes its influence.

It also excludes the active bone in the automatic weight calculation when the mesh is parented to the armature using the Armature Deform tool with the With Automatic Weights option.

Bone influence areas for envelopes method.¶

Envelopes is the most general skinning method. It works with all available object types for skinning (meshes, lattices, curves, surfaces and texts). It is based on proximity between bones and their geometry, each bone having two different areas of influence, shown in the Envelope visualization:

The inside area, materialized by the “solid” part of the bone, and controlled by both root and tip radius.

The outside area, materialized by the lighter part around the bone, and controlled by the Distance setting.

The editing pages for how to edit these properties.

The Distance defines a volume which is the range within the bone has an influence on vertices of the deformed object. The geometry is less and less affected by the bone as it goes away by following a quadratic decay.

Single bone with various envelope sizes.¶

A bone property, that controls the global influence of the bone over the deformed object, when using the envelopes method.

It is only useful for the parts of geometry that are “shared”, influenced by more than one bone (generally, at the joints…) – a bone with a high weight will have more influence on the result than one with a low weight… Note that when set to 0.0, it has the same effect as disabling the Deform option.

This option controls how the two deforming methods interact, when they are both enabled. By default, when they are both active, all vertices belonging to at least one vertex group are only deformed through the vertex groups method. The other “orphan” vertices being handled by the envelopes one. When you enable this option, the “deformation influence” that this bone would have on a vertex (based from its envelope settings) is multiplied with this vertex’s weight in the corresponding vertex group. In other words, the vertex groups method is further “weighted” by the envelopes method.

Set the radius for the head and the tail of envelope bones. Inside this volume, the geometry if fully affected by the bone.

Three Armature Bones all using Envelope Weight.¶

The 1st with a default radius value, the two others with differing Tail and Head radius values.

---

## Delete¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/delete.html

**Contents:**
- Delete¶
- Bones¶
- Dissolve¶

Armature ‣ Delete ‣ Bones

This tool delete selected bones, selected joints are ignored.

If you delete a bone in a chain, its child(ren) will be automatically re-parented to its own parent, but not connected, to avoid deforming the whole armature.

An armature with two selected bones, just before deletion.¶

The two bones have been deleted. Note that Bone.002, previously connected to the deleted Bone.001, is now parented but not connected to Bone.¶

Armature ‣ Delete ‣ Dissolve

---

## Dope Sheet Overlays¶

**URL:** https://docs.blender.org/manual/en/latest/editors/dope_sheet/display/overlays.html

**Contents:**
- Dope Sheet Overlays¶

Clicking (Show Overlays) toggles all overlays in the Dope Sheet.

The drop-down button displays a popover with more detailed settings, which are described below.

When using scene time synchronization in the Sequence Editor, display the range of the current scene strip.

---

## Drivers Editor¶

**URL:** https://docs.blender.org/manual/en/latest/editors/drivers_editor.html

**Contents:**
- Drivers Editor¶

This editor lets you set up Drivers, which calculate the value for a property based on other properties. In other words, they make a set of source properties “drive” the target property, and can thus serve as an alternative to animating the property by hand.

The Drivers Editor, showing how you might drive a cube’s rotation based on its position.¶

The user interface is largely the same as that of the Graph Editor, with two important differences:

The Sidebar has an additional Drivers tab. This is where the source properties are brought together to calculate an intermediate value for the target property.

The curve doesn’t represent the property’s value over time, but a mapping from the above intermediate value (X axis) to the final value (Y axis).

---

## Drivers Panel¶

**URL:** https://docs.blender.org/manual/en/latest/animation/drivers/drivers_panel.html

**Contents:**
- Drivers Panel¶
- Driver Settings¶
  - Type¶
  - Driver Value¶
  - Variables¶
  - Update Dependencies¶
  - Show in Drivers Editor¶
- Driver Variables¶
  - Rotation Channel Modes¶
- Expressions¶

Edit Driver popover.¶

Sidebar region ‣ Drivers

Context menu ‣ Edit Driver

This panel is visible in Sidebar of the Drivers Editor or as a popover when adding a driver to a property.

It shows the property that is being driven, followed by a series of settings that determine how the driver works.

There are two categories of drivers:

Built-in functions (Average, Sum, Min and Max)

The driven property will have the value of the average, sum, lowest or highest (respectively) of the values of the referenced Driver Variables. If there is only one driver variable, these functions will yield the same result.

Custom (Scripted Expression).

An arbitrary Python expression that can refer to the Driver Variables by name. See Expressions.

The current result of the driver setup. Useful for debug purposes.

See Driver Variables.

Forces an update for the Driver Value dependencies.

Opens the fully featured Drivers Editor. This button only appears in the popover version of the Drivers panel.

Variables are references to properties, transformation channels, or the result of a comparison between transformations of two objects.

Drivers should access object data via Driver Variables, rather than direct references in the Python expression, in order for dependencies to be correctly tracked.

Add, Copy, Paste buttons.¶

Adds a new Driver Variable.

Copies the current variable list so it can be pasted into another driver’s variable list.

Name for use in scripted expressions. The name must start with a letter, and only contain letters, digits, or underscores.

The type of variable to use.

Retrieves the value of an RNA property, specified by a data-block reference and a path string.

In case of transform properties, this will return the exact value of the UI property, while Transform Channel will take parenting and/or constraints into account as needed.

See also Custom Properties.

The ID-block type. For example: Key, Image, Object, Material.

The ID of the ID-block type. For example: “Material.001”.

The RNA name of the property, based on a subset of Python attribute access syntax. For example: location.x or location[0] for the X location animation channel value (before parenting or constraints), or ["prop_name"] for a custom property.

If enabled, allows specifying a fallback value to use as the variable value if the RNA Path cannot be resolved, instead of causing a driver evaluation failure. For more info see Context Property below.

The easiest way to create a variable of this type is to use the Copy As New Driver context menu option of the input property, and paste the result into the driver via Paste Driver Variables.

Retrieves the value of a Transform channel from an object or bone.

ID of the object. For example: Cube, Armature, Camera.

For armatures, the name of the Armature bone. For example: “Bone”, “Bone.002”, “Arm.r”.

For example, X Location, X Rotation, X Scale.

The Average Scale option retrieves the combined scale value, computed as the cubic root of the total change in volume. Unlike X/Y/Z Scale, this value can be negative if the object is flipped by negative scaling.

For rotation channels, specifies the type of rotation data to use, including different explicit Euler orders. Defaults to using the Euler order of the target. See Rotation Channel Modes.

World Space, Transform Space, Local Space.

Provides the value of the rotational difference between two objects or bones, in radians.

For armatures, the name of the Armature bone. For example: “Bone”, “Bone.002”, “Arm.r”.

Provides the value of the distance between two objects or bones.

For armatures, the name of the Armature bone. For example: “Bone”, “Bone.002”, “Arm.r”.

World Space, Transform Space, Local Space.

Provides the value of a property that is implicitly referring to either a scene or a view layer of the currently evaluating animation system. This is a weak reference which does not lead to the scene or view layer referenced from the driver to be linked when linking animation data.

An example when such properties comes in play is referring to a transformation of the active camera. It is possible to set up a driver in a character file, and make the driver use the set camera when the character is linked into a set.

Active Scene, Active View Layer.

The RNA name of the property, based on a subset of Python attribute access syntax. For example: camera.location.x or camera.location[0] for the camera X location animation channel value (before parenting or constraints), or ["prop_name"] for a custom property.

If enabled, allows specifying a fallback value to use as the variable value if the RNA Path cannot be resolved, instead of causing a driver evaluation failure.

This feature can be very useful for making drivers more robust when implementing scene-global options using custom properties. When the object is linked into a different scene, these custom properties may not exist there, and the fallbacks can be used to provide sensible default values.

Fallbacks can also be used to emulate the lookup behavior of the View Layer mode of the material Attribute Node.

Although the values of the x/y/z animation channels for the camera location can be accessed via camera.location[0/1/2], retrieving its world space location and orientation after parenting and constraints currently requires using camera.matrix_world. This property can be understood easily by viewing the matrix as an array of four vectors in World space:

matrix_world[0][0/1/2] is the Screen Right direction vector (camera local X).

matrix_world[1][0/1/2] is the Screen Up direction vector (camera local Y).

matrix_world[2][0/1/2] is the opposite of the direction the camera is pointing.

matrix_world[3][0/1/2] is the location of the camera.

Shows the value of the variable.

Rotation Transform Channels support a number of operation modes, including:

Uses the Euler order of the target to decompose rotation into channels.

Explicitly specifies the Euler rotation order to use.

Provides the Quaternion representation of the rotation.

Decomposes the rotation into two parts: a Swing rotation that aims the specified axis in its final direction, followed by a Twist rotation around that axis. This is often necessary for driving corrective Shape Keys and bones for organic joint rotation.

This decomposition is often produced in rigs by using a helper bone with a Damped Track Constraint to extract the swing part, and its child with Copy Transforms to extract the twist component.

The channels values for Swing and Y Twist are:

Falloff curves for weighted angles.¶

True angle of the twist rotation.

True angle of the swing rotation, independent of its direction.

Weighted angles that represent the amount of swing around the X/Z axis.

The magnitude of the angle equals W Rotation when the rotation is purely around that axis, and fades out to zero as the direction changes toward the other axis, following the falloff curves from the graph on the right.

Mathematically, the swing angles are computed from quaternion components, using \(2 \arccos(w)\) for W and \(2 \arcsin(x)\) etc. for the others. The component of the swing rotation that corresponds to the twist axis is always 0, and is replaced by the twist angle.

A text field where you can enter an arbitrary Python expression that refers to Driver Variables by their names.

The expression has access to a set of standard constants and math functions from math, bl_math and other modules, provided in the Driver Namespace. For an example of adding a custom function to the namespace, see the driver namespace example.

For performance reasons it is best to use the Simple Expressions subset as much as possible.

If this option is enabled, the variable self can be used for drivers to reference their own data. Useful for objects and bones to avoid having creating a Driver Variable pointing to itself.

Example: self.location.x applied to the Y rotation property of the same object will make the object tumble when moving.

Note that dependencies for properties accessed via self may not be fully tracked.

Blender can evaluate a useful subset of Python driver expressions directly, which significantly improves performance, especially on multi-core systems. To take advantage of this, the driver expression must only use the following features:

Use only ASCII characters.

Floating-point and decimal integer.

+, -, *, /, ==, !=, <, <=, >, >=, and, or, not, conditional operator/ ternary if

min, max, radians, degrees, abs, fabs, floor, ceil, trunc, round, int, sin, cos, tan, asin, acos, atan, atan2, exp, log, sqrt, pow, fmod

lerp, clamp, smoothstep

Simple expressions are evaluated even when Python script execution is disabled.

When an expression outside of this subset is used, Blender displays a “Slow Python expression” warning. However, as long as the majority of drivers use simple expressions, using a complex expression in select few is OK.

Extending Blender with Python.

Python and its documentation.

functions.wolfram.com.

---

## Duplicate¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/duplicate.html

**Contents:**
- Duplicate¶

This tool works on selected bones; selected joints are ignored.

As in mesh editing, by pressing Shift-D the selected bones will be duplicated. The duplicates become the selected elements and they are placed in select mode, so you can move them wherever you like.

If you select part of a chain, by duplicating it you will get a copy of the selected chain, so the copied bones are interconnected exactly like the original ones.

The duplicate of a bone which is parented to another bone will also be parented to the same bone, even if the root bone is not selected for the duplication. Be aware, though, that if a bone is parented and connected to an unselected bone, its copy will be parented, but not connected to the unselected bone (see Fig. Duplication example.).

An armature with three selected bones and a selected single root.¶

The three duplicated bones. Note that the selected chain is preserved in the copy, and that Bone.006 is parented but not connected to Bone.001, as indicated by the black dashed line. Similarly, Bone.007 is parented but not connected to Bone.003.¶

---

## Editing Channels¶

**URL:** https://docs.blender.org/manual/en/latest/editors/graph_editor/channels/editing.html

**Contents:**
- Editing Channels¶
- Delete Channels¶
- Un/Group Channels¶
- Toggle/Enable/Disable Channel Settings¶
- Toggle Channel Editability¶
- Extrapolation Mode¶
- Add F-Curve Modifier¶
- Show/Hide¶
- Expand/Collapse Channels¶
- Move¶

Channel ‣ Delete Channels

Removes the selected channels from the current action.

Make sure the mouse cursor is hovering over the channel region before using the keyboard shortcuts. If it’s hovering over the main region, you’ll only delete the selected keyframes, not the full channels.

Channel ‣ Un/Group Channels

Un/Groups the selected channels into a collection that can be renamed by double-clicking its name. Grouping channels helps keep the view more organized.

Channel ‣ Toggle/Enable/Disable Channel Settings

Shift-W, Shift-Ctrl-W, Alt-W

Toggles, enables, or disables a certain setting for the selected channels:

When a channel is protected (closed padlock icon), it can’t be edited. Instead of pressing Shift-W and selecting Toggle, you can also simply press Tab.

When a channel is muted (empty checkbox), it doesn’t affect the animation.

Channel ‣ Toggle Channel Editability

Locks or unlocks a channel for editing.

Channel ‣ Extrapolation Mode

Changes how the curve behaves before its first keyframe and after its last keyframe.

Constant extrapolation.¶

Continue in a straight line, keeping the same value as the first/last keyframe. This is the default.

Linear extrapolation.¶

Continue in a straight line, keeping the same slope as on the first/last keyframe.

Repeat the whole curve. This works by adding a Cycles modifier.

Remove the above modifier, making the curve non-repeating again.

Channel ‣ Add F-Curve Modifier

Shows a submenu from where you can add a modifier to the active curve. Settings for these modifiers can be found in Sidebar ‣ Modifiers.

Hides the selected curves.

Hides all curves except the selected ones.

Shows all previous hidden curves.

Channel ‣ Expand/Collapse Channels

NumpadPlus, NumpadMinus

Expands or collapses the selected headers.

Lets you reorder the selected channels or slots in the list:

To the top Shift-PageUp

Down one line PageDown

To the bottom Shift-PageDown

Channel ‣ Revive Disabled F-Curves

Clears the “disabled” tag from all F-Curves to get broken F-Curves working again. (A curve is broken if it references a property that doesn’t exist.)

Channel ‣ Keys to Samples

Switches the selected curves from interpolating between a set of keyframes to using a sampled value at each full frame. This is a destructive process that removes the ability to edit the curve. It’s mainly used to reduce the file size with large datasets, as samples take up less space than keyframes.

Between samples (on subframes), the curve interpolates linearly.

Channel ‣ Samples to Keys

Switches the selected curves from using samples to using keyframes, making them editable. Note that this creates a keyframe on every frame.

Channel ‣ Sound to Samples

Creates a sampled curve based on a sound file. Use Samples to Keys if you need to edit it.

Cutoff frequency of a high-pass filter that is applied to the audio data.

Cutoff frequency of a low-pass filter that is applied to the audio data.

Value for the hull curve calculation that tells how fast the hull curve can rise. The lower the value, the steeper it can rise.

Value for the hull curve calculation that tells how fast the hull curve can fall. The lower the value, the steeper it can fall.

Minimum amplitude value needed to influence the hull curve.

Only the positive differences of the hull curve amplitudes are summarized to produce the output.

The amplitudes of the hull curve are summarized. If Accumulate is enabled, both positive and negative differences are accumulated.

Gives the output as a square curve. Negative values always result in -1, and positive ones in 1.

All values lower than this threshold result in 0.

Channel ‣ Bake Channels

Generates new keyframes for the selected curves.

The range that will be baked. Defaults to the scene range or preview range.

Distance between keyframes. Can be used to create a keyframe every 10 frames or even every half frame.

Removes existing keys outside the specified baking range.

The interpolation type for the new keys.

If enabled, the new keyframes are based on the modified curve, and the modifiers get deleted.

If disabled, the new keyframes are based on the original curve, and the modifiers stay applied.

Channel ‣ Discontinuity (Euler) Filter

Cleans up Euler rotation channels that suffer from Gimbal Lock. The channels of all three euler rotation axes need to be selected for this to work.

Channel ‣ Frame Selected Channels

Pans and zooms the view to show all keyframes of the selected curves. You can also click a channel with Alt-MMB.

---

## Editing Dopesheet Data¶

**URL:** https://docs.blender.org/manual/en/latest/editors/dope_sheet/editing.html

**Contents:**
- Editing Dopesheet Data¶
- Select Menu¶
- Marker Menu¶
- Channel Menu¶
- Key Menu¶
- Snap¶
- Proportional Editing¶

Selects all keyframes.

Deselects all keyframes.

Inverts the selection.

Lets you drag a box and selects the keyframes inside it.

Lets you drag a box and selects the keyframes inside the corresponding time range, even if they’re above or below the box.

Displays a circle around the cursor, which you can drag over keyframes to select them.

Lets you draw a freehand shape and selects the keyframes inside it.

Expand the selection to include the neighbors (in time) of the currently selected keys.

Deselect keyframes with fewer than two selected neighbors.

Select keys that are on the same channel as a key that’s already selected.

Selects keys that are on the same frame as a key that’s already selected.

Selects all the keys that are on the current frame.

Selects keys that are on the same frame as a selected marker.

Selects keys that lie between the leftmost and rightmost selected markers.

Select the keys that lie before (or on) the current frame. You can also click Shift-Ctrl-LMB anywhere to the left of the Playhead.

Select the keys that lie after (or on) the current frame. You can also click Shift-Ctrl-LMB anywhere to the right of the Playhead.

Markers are used to denote frames with key points or significant events within an animation. Like with most animation editors, they’re shown at the bottom.

Markers in animation editor.¶

There are some options that are exclusive to the Dope Sheet editor:

Whether to also move the selected markers when moving the selected keyframes.

Instead of showing the global scene markers, show the local pose markers (which only exist inside the action). While this option is active, the Add Marker menu item will also create pose markers instead of scene markers.

Converts the selected scene markers into pose markers, making them only visible inside the currently selected action.

For information about the other marker tools, see Editing Markers.

See Graph Editor Channels.

Most items in this menu are documented on the Graph Editor’s Editing F-Curves page. One important difference is that scaling keyframes in the Dope Sheet Editor only moves them along the time axis (with the Playhead serving as the pivot point); it doesn’t change their values.

The Dope Sheet editor has the following additional menu items:

Lets you stretch one set of keyframes across time while compressing an adjacent set to compensate, leaving the combined duration the same.

To use this operator, first select a range of three or more keyframes, then place the mouse cursor somewhere in the middle and press Shift-T. The range will be temporarily split in two at the location of the cursor, indicated by a dashed vertical line. If you now move the mouse, the two halves of the range will change in length, and the keyframes within them will move accordingly. Click LMB to confirm or RMB to cancel.

Sets the type of the selected keyframes.

The toggle button enables/disables automatic keyframe snapping. The dropdown button shows a popover with the following options:

Type of element to snap to.

Snap to the nearest Marker.

When disabled, keyframes will move in increments of Snap To. For example, if you selected Second and have a keyframe that’s currently on 0:06+5, dragging it to the right will snap it to 0:07+5. Its time increases by a second, and its subsecond offset of 5 frames remains the same.

When enabled, keyframes will snap to multiples of Snap To. Taking the above example, the keyframe would snap to 0:07+0, removing the subsecond offset.

See Proportional Editing.

---

## Editing Keyframes¶

**URL:** https://docs.blender.org/manual/en/latest/animation/keyframes/editing.html

**Contents:**
- Editing Keyframes¶
- Insert Keyframe¶
  - Auto Keyframe¶
- Insert Keyframe with Keying Set¶
- Delete Keyframes¶
- Clear Keyframes¶
- Editing Keyframes¶
- Examples¶
  - Keyframe Animation¶

Object Mode, Pose Mode, Video Sequencer Preview

Object/Pose/Strip ‣ Animation ‣ Insert Keyframe

There are several methods of adding new keys. Namely:

In the 3D Viewport and Video Sequencer Preview, pressing I will key properties based on the Default Key Channels User Preferences.

When a Keying Set is active, it is used instead of reading the User Preferences.

Hovering over a property and pressing I or with the context menu by RMB a property and choose Insert Keyframe from the menu.

With the User Preference “Pie Menu on Drag” enabled, holding down I and moving the cursor will bring up a pie menu to insert one of Location, Rotation, Scale, and Available.

Timeline Auto Keyframe.¶

Auto Keyframe is the record button in the Timeline header. Auto Keyframe adds keyframes automatically to the set frame if the value for transform type properties changes.

See Timeline Keyframe Control for more info.

Object Mode, Pose Mode, Video Sequencer Preview

Object/Pose/Strip ‣ Animation ‣ Insert Keyframe with Keying Set

Insert Keyframes for specified Keying Set, with menu of available Keying Sets.

Object Mode, Pose Mode, Video Sequencer Preview

Object/Pose/Strip ‣ Animation ‣ Delete Keyframes…

There are several methods of removing keyframes:

In the 3D Viewport or Video Sequencer Preview press Alt-I to remove keys from selected objects, bones or strips on the current frame.

When the mouse is over a value, press Alt-I.

RMB a value and choose Delete Keyframe from the menu.

Object Mode, Pose Mode, Video Sequencer Preview

Object/Pose/Strip ‣ Animation ‣ Clear Keyframes…

Removes all keyframes from the selected object, bone or strip.

Keyframes can be edited in two editors. To do so go to either the Graph Editor or the Dope Sheet.

This example shows you how to animate a cube’s location, rotation, and scale.

First, in the Timeline, or other animation editors, set the frame to 1.

With the cube selected in Object Mode, press I in the 3D Viewport. This will record the location, rotation, and scale, for the cube on frame 1.

Set the frame to 100.

Use Move G, Rotate R, Scale S, to transform the cube.

Press I in the 3D Viewport.

To test the animation, press Spacebar to play.

The animation on frames 1, 50 and 100.¶

---

## Editing Strips¶

**URL:** https://docs.blender.org/manual/en/latest/editors/nla/editing/strip.html

**Contents:**
- Editing Strips¶
- Transform¶
  - Swap¶
  - Move Up¶
  - Move Down¶
- Snap¶
- Split¶
- Duplicate¶
- Linked Duplicate¶
- Delete¶

Move the selected strips in time or to a different track.

Lets you quickly move the selected strips that are on a certain side of the Playhead. This is handy if you need to, say, move all the strips after a certain time point to the right to make space for new ones.

To use this operator, first select some or all strips and place your mouse cursor to the left or right of the Playhead. Then, press E, move the mouse to move (only) the strips on that side of the Playhead, and press LMB to confirm (or RMB to cancel).

If a strip straddles the Playhead, only its starting/ending point will be moved (again depending on the position of the mouse cursor).

Scales the selected strips, using the Playhead as the pivot point.

Strip ‣ Transform ‣ Swap

Swap the order of the selected strips in their track.

Strip ‣ Transform ‣ Move Up

Move selected strips up a track if there is room.

Strip ‣ Transform ‣ Move Down

Move selected strips down a track if there is room.

Move the start of the selected strips to the current frame.

Move the start of the selected strips to the nearest full frame.

Move the start of the selected strips to the nearest second.

Move the start of the selected strips to the nearest marker.

Split the selected strips in two at the current frame.

Creates copies of the selected strips, duplicating any actions they reference. Editing the keyframes in a copied strip therefore doesn’t affect the original.

Strip ‣ Linked Duplicate

Creates copies of the selected strips, reusing any actions they reference. Editing the keyframes in a copied strip therefore also affects the original (and vice versa). Blender warns you about this by highlighting the other strip in red.

Linked duplicated strip being edited.¶

Deletes the selected NLA-Strips.

Groups the selected NLA-strips into a meta strip.

Select two or more strips.¶

Combine them into a meta strip.¶

Ungroups the selected meta strips, replacing them by their contents.

Strip ‣ Toggle Muting

Mutes or unmutes the selected strips. Muted strips have a dotted border and don’t influence the animation.

Object and Pose Modes

Header ‣ Object ‣ Animation ‣ Bake Action…

The final motion of objects and bones depends not only on the keyframed animation, but also on F-Curve modifiers, drivers, and constraints. The Bake Action operator computes this final motion and creates a corresponding keyframe on every scene frame.

This can be useful for adding deviation to a cyclic action like a Walk Cycle, or to create a keyframe animation from drivers or constraints.

Start frame for baking.

End frame for baking.

Number of frames to skip forward while baking each frame.

Only key selected bones (Pose baking only).

Keyframe from the final transformations (with constraints applied).

Remove all constraints from keyed object/bones, and do ‘visual’ keying.

Bake animation onto the object then clear parents (objects only).

Bake animation into the current action instead of creating a new one (useful for baking only part of bones in an armature).

After baking curves, remove redundant keys.

Which data transformations to bake.

Bake bone transformations.

Bake object transformations.

Which channels to bake.

Bake location channels.

Bake rotation channels.

Bake B-Bone channels.

Bake custom properties.

Applies the scale of the selected strips to their referenced actions.

Resets the scale of the selected strips.

Strip ‣ Sync Action Length

Resets the strip’s length to that of its underlying action, ensuring that it (only) plays from the action’s first keyframe to its last.

The Sync Length Now button in the Sidebar, which does the same thing.

Strip ‣ Make Single User

Duplicates actions where necessary so that each selected strip has its own action that’s not used by any others. This way, you can edit the keyframes in the selected strips knowing that you won’t affect any other part of the animation.

This does not recursively go inside meta strips.

Strip ‣ Start Editing Stashed Action

Enters Tweak Mode for the selected strip’s action, making its keyframes available for editing in e.g. the Graph Editor. In addition, marks the strip’s track as Solo, muting all the other tracks – this way, they no longer influence the animation and you can focus exclusively on the action you’re editing.

While the menu item refers to stashed (muted) actions, this only reflects the typical use case. It works on unmuted actions as well.

When you’re done editing, click Strip ‣ Stop Editing Stashed Action or press Shift-Tab again.

Strip in Tweak mode.¶

Strip ‣ Start Tweaking Strips Actions (Full Stack)

Enters Tweak Mode for the selected strip’s action, making its keyframes available for editing. Leaves all the other tracks enabled so that you can still see their effects while making changes.

When you’re done, click Strip ‣ Stop Tweaking Strips Actions or press Tab again.

For transitions above the tweaked strip, keyframe remapping will fail for channel values that are affected by the transition. A workaround is to tweak the active strip without evaluating the upper NLA stack.

Strip ‣ Start Tweaking Strips Actions (Lower Stack)

Enters Tweak Mode for the selected strip’s action, making its keyframes available for editing. Mutes any tracks above the current one so that they don’t influence the animation while making changes.

When you’re done, click Strip ‣ Stop Tweaking Strips Actions or press Tab.

---

## Extrude¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/extrude.html

**Contents:**
- Extrude¶
- Mouse Clicks¶

When you press E, for each selected tip (either explicitly or implicitly), a new bone is created. This bone will be the child of “its” tip owner, and connected to it. As usual, once extrusion is done, only the new bones’ tips are selected, and in select mode, so you can place them to your liking. See Fig. Extrusion example..

An armature with three selected tips.¶

The three extruded bones.¶

You also can use the rotating/scaling extrusions, as with meshes, by pressing respectively E R and E S – as well as locked extrusion along a global or local axis.

A single selected bone’s tip.¶

The two mirror-extruded bones.¶

Bones have an extra “mirror extruding” tool, called by pressing Shift-E. By default, it behaves exactly like the standard extrusion. But once you have enabled X-Axis Mirror editing option, each extruded tip will produce two new bones, having the same name except for the “_L”/ “_R” suffix (for left/right, see the naming conventions). The “_L” bone behaves like the single one produced by the default extrusion – you can move, rotate or scale it exactly the same way. The “_R” bone is its mirror counterpart (along the armature’s local X axis), see Fig. Mirror extrusion example..

Canceling the extrude action causes the newly created bones to snap back to the source position, (creating zero length bones). These will be removed when exiting Edit Mode, however, they can cause confusion and it’s unlikely you want to keep them. If you realize the problem immediately, undo the extrude action.

In case you are wondering, you cannot just press X to solve this as you would in mesh editing, because extrusion selects the newly created tips, and as explained below the Delete tool ignores bones’ joints. To get rid of these extruded bones without undoing, you would have to move the tips, then select the bones and delete them.

If at least one bone is selected, Ctrl-RMB-clicking adds a new bone.

About the new bone’s tip:

After you Ctrl-RMB-clicked it becomes the active element in the armature, it appears to be right where you clicked, but (as in mesh editing) it will be on the plane parallel to the view and passing through the 3D cursor.

The position of the root and the parenting of the new bone depends on the active element:

Ctrl-clicking when the active element is a bone.¶

If the active element is a bone:

The new bone’s root is placed on the active bone’s tip.

The new bone is parented and connected to the active bone (check the Outliner in Fig. Ctrl-clicking when the active element is a tip.).

Ctrl-clicking when the active element is a tip.¶

If the active element is a tip:

The new bone’s root is placed on the active tip.

The new bone is parented and connected to the bone owning the active tip (check the Outliner in Fig. Ctrl-clicking when the active element is a tip.).

Ctrl-clicking when the active element is a disconnected root.¶

If the active element is a disconnected root:

The new bone’s root is placed on the active root.

The new bone is not parented to the bone owning the active root (check the Outliner in Fig. Ctrl-clicking when the active element is a disconnected root.).

And hence the new bone will not be connected to any bone.

Ctrl-clicking when the active element is a connected root.¶

If the active element is a connected root:

The new bone’s root is placed on the active root.

The new bone is parented and connected to the parent of the bone owning the active root (check the Outliner in Fig. Ctrl-clicking when the active element is a connected root.).

This should be obvious because if the active element is a connected root then the active element will be also the tip of the parent bone, so it is the same as the second case.

As the tip of the new bone becomes the active element, you can repeat these Ctrl-RMB clicks several times, to consecutively add several bones to the end of the same chain.

---

## Fill Between Joints¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/fill_between_joints.html

**Contents:**
- Fill Between Joints¶

Armature ‣ Fill Between Joints

The main use of this tool is to create one bone between two selected joints by pressing F, similar to how in mesh editing you can “create edges/faces”.

If you have one root and one tip selected, the new bone:

Will have the root placed on the selected tip.

Will have the tip placed on the selected root.

Will be parented and connected to the bone owning the selected tip.

Active tip on the left.¶

Active tip on the right.¶

If you have two tips selected, the new bone:

Will have the root placed on the selected tip closest to the 3D cursor.

Will have the tip placed on the other selected tip.

Will be parented and connected to the bone owning the tip used as the new bone’s root.

3D cursor on the left.¶

3D cursor on the right.¶

If you have two roots selected, you will face a small problem due to the event system in Blender not updating the interface in real-time.

When clicking F, similar to the previous case, you will see a new bone:

With the root placed on the selected root closest to the 3D cursor.

With the tip placed on the other selected root.

Parented and connected to the bone owning the root used as the new bone’s root.

If you try to move the new bone, Blender will update the interface and you will see that the new bone’s root moves to the tip of the parent bone.

Before UI update (3D cursor on the left).¶

After UI update, correct visualization.¶

Clicking F with only one bone joint selected will create a bone from the selected joint to the 3D cursor position, and it will not parent it to any bone in the armature.

Fill with only one tip selected.¶

Fill with only one root selected.¶

You will get an error when:

Trying to fill two joints of the same bone.

Trying to fill more than two bone joints.

---

## Fixed Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/constraints/types/fixed.html

**Contents:**
- Fixed Constraint¶

Physics ‣ Rigid Body Constraint

This constraint cause the two objects to move as one. Since the physics system does have a tiny bit of slop in it, the objects do not move as rigidly as they would if they were part of the same mesh.

Fixed constraint options.¶

---

## Flip Quats¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/editing/flip_quats.html

**Contents:**
- Flip Quats¶

Flip quaternion values to achieve desired rotations, while maintaining the same orientations.

---

## Floor Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/relationship/floor.html

**Contents:**
- Floor Constraint¶
- Options¶
- Example¶

The Floor constraint sets up a flat and infinitely large floor (or wall, or ceiling) which the constrained object or bone cannot pass through.

Like other constraints, the Floor constraint only looks at the origin for objects; their geometry is not taken into account. This means that, if a cube’s origin is at its center and a Floor constraint is added targeting a floor plane, the cube will still be able to sink halfway into the plane. The Offset can be used to mitigate this.

Limit Location Constraint

The object or bone that defines the location, and optionally the rotation, of the floor.

Moves the virtual floor “up” or “down” by a certain distance. This makes it possible to, say, make foot bones stay a certain distance above the floor geometry to leave room for the actual feet.

The axis that’s perpendicular to the floor and points towards its “walkable” area. Setting this to Z creates a floor; X or Y creates a wall; and -Z creates a ceiling.

By default, these axes correspond to the global axes.

Use the Target’s local axes for Min/Max instead of the global axes.

The spaces for evaluating and limiting the coordinates of the target and owner.

How strongly the constraint affects the owner.

---

## Follow Path Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/relationship/follow_path.html

**Contents:**
- Follow Path Constraint¶
- Position Offsetting¶
- Options¶
- Example¶

The Follow Path constraint positions an object or bone on a Curve. The desired position can be specified in two ways:

Using a frame number, namely the Evaluation Time of the Curve with an optional Offset in the constraint.

Using a number between 0 and 1, namely the Offset Factor in the constraint.

By animating these properties, the object or bone can be made to move along the Curve. It’s also possible to make it rotate to match the Curve’s direction. Use cases include cameras on rails, vehicles on roads, boxes on conveyor belts, and so on.

To set up the constraint more quickly, select the object, add the Curve to the selection, press Ctrl-P, and click Path Constraint.

The Follow Path constraint can be combined with a tracking constraint to, for example, keep a moving camera pointed at an object.

The Clamp To Constraint snaps an object or bone to a Curve based on its location.

The constraint uses its owner’s position and rotation in World Space as offsets to the position and rotation on the Curve. If Follow Curve is disabled, the offsets are added in the Curve’s Local Space. If it’s enabled, the offsets are added in the space of the current curve point, with the global Y axis corresponding to the tangent direction.

In both cases, the Curve’s scale acts as a multiplier for the position offset.

Before adding the constraint, the cone is offset along the world Y axis.¶

After adding the constraint, the cone is offset along the Curve’s local Y axis.¶

When enabling Follow Curve, the cone is offset along the curve point’s tangent.¶

To have the owner perfectly positioned and aligned on the Curve, ensure its world position and rotation are both zero. This can be done by pressing Alt-G and Alt-R respectively.

Follow Path constraint.¶

The Curve object to follow.

The number of frames to subtract from the Curve’s Evaluation Time. A positive value will move the owner to an earlier point on the Curve, while a negative value will move it to a later point.

Relative position along the Curve, independent of its Evaluation Time. A value of 0 corresponds to the start of the Curve while a value of 1 corresponds to the end.

The local axis of the owner that should be aligned to the Curve’s tangent direction. Requires that Follow Curve is enabled.

A negative axis will make the owner point in the opposite direction.

The local axis of the owner that should be aligned (as much as possible) to the global Z axis. Requires that Follow Curve is enabled.

The Forward Axis and the Up Axis must be different. If they are the same, the constraint will stop working and its icon will turn red.

Ignore the Curve’s Evaluation Time and position the owner using only the Offset Factor.

Despite the name of this property, the owner can still be moved over time by animating the Offset Factor.

Scale the owner based on the radii of the Curve’s control points.

Rotate the owner according to the Forward Axis and the Up Axis.

By default, the Curve’s Evaluation Time is static and the constraint owner doesn’t move. Clicking this button will animate the Evaluation Time so that it’s always equal to the current scene frame.

Of course, it’s also possible to skip this button and animate the Evaluation Time by hand.

How strongly the constraint affects the owner.

---

## Follow Track Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/motion_tracking/follow_track.html

**Contents:**
- Follow Track Constraint¶
- Options¶
- Example¶

The Follow Track constraint makes an object imitate the movement of a motion tracking marker. This makes the object appear at the same position in the render as where the marker appears in the motion-tracked video.

By default, the object follows the 2D motion of the marker in the video on a plane in the 3D world. However, it’s also possible to make the object follow the reconstructed 3D position of the marker. The latter requires setting up at least eight markers and clicking Solve Camera/Object Motion.

The Link Empty to Track button in the Movie Clip Editor creates an Empty and assigns it this constraint in one click.

Follow Track constraint.¶

Whether the tracking marker is in the scene’s Active Clip. If unchecked, a selector appears for choosing another clip.

Whether to use the tracking marker’s reconstructed world position (instead of its position in the flat video).

Whether to use the tracking marker’s video position after compensating for lens distortion (see Lens settings). Not available when 3D Position is checked.

How to handle a difference in aspect ratio between the tracked video footage and the rendered image.

The object is positioned as though the video were stretched to exactly match the size of the rendered image.

The object is positioned as though the video were made as large as possible while still keeping its original aspect ratio and fitting inside the rendered image along both axes.

The object is positioned as though the video were made as large as possible while still keeping its original aspect ratio and fitting inside the rendered image along one axis.

The Set as Background button in the Movie Clip Editor sets the video as the background for the camera. This background can then be resized by setting the same Frame Method in the Background Images panel of the camera’s properties.

The physical object containing the tracking marker to follow. See the Objects Panel in the Movie Clip Editor. If left empty, Track will list the markers used to reconstruct the physical camera.

The tracking marker to follow.

The Blender camera in whose field of view the constrained object should appear. If left empty, the scene’s active camera is used.

If this object is set, the constrained object will be projected onto its surface. This can be used to create a facial makeup effect, for example. Not available when 3D Position is checked.

Replaces the constraint by a set of equivalent keyframes.

How strongly the constraint affects its owner.

Follow Track Example Video

---

## Generic Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/constraints/types/generic.html

**Contents:**
- Generic Constraint¶
- Options¶

Physics ‣ Rigid Body Constraint

The generic constraint has a lot of available parameters.

The X, Y, and Z axis constraints can be used to limit the amount of translation between the objects. Clamping the min/max to zero has the same effect as the Point constraint.

Clamping the relative rotation to zero keeps the objects in alignment. Combining an absolute rotation and translation clamp would behave much like the Fixed constraint.

Using a nonzero spread on any parameter allows it to oscillate in that range throughout the course of the simulation.

Enables/disables limit rotation around X, Y or Z axis respectively.

Lower limit of rotation for X, Y or Z axis respectively.

Upper limit of rotation for X, Y or Z axis respectively.

Enables/disables limit translation on X, Y or Z axis respectively.

Lower limit of translation for X, Y or Z axis respectively.

Upper limit of translation for X, Y or Z axis respectively.

---

## Generic Spring Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/constraints/types/generic_spring.html

**Contents:**
- Generic Spring Constraint¶
- Options¶

Physics ‣ Rigid Body Constraint

The generic spring constraint adds some spring parameters for the X/Y/Z axes to all the options available on the Generic constraint. Using the spring alone allows the objects to bounce around as if attached with a spring anchored at the constraint object. This is usually a little too much freedom, so most applications will benefit from enabling translation or rotation constraints.

If the damping on the springs is set to 1, then the spring forces are prevented from realigning the anchor points, leading to strange behavior. If your springs are acting weird, check the damping.

Generic Spring constraint options.¶

Enables/disables limit translation on X, Y or Z axis respectively.

Lower limit of translation for X, Y or Z axis respectively.

Upper limit of translation for X, Y or Z axis respectively.

Enables/disables limit rotation around the X, Y or Z axis respectively.

Lower limit of rotation for X, Y or Z axis respectively.

Upper limit of rotation for X, Y or Z axis respectively.

Enables/disables springs translation on X, Y or Z axis respectively.

Spring Stiffness of the translation on X, Y or Z axis respectively. Specifies how “bendy” the spring is.

Spring Damping of the translation on X, Y or Z axis respectively. Amount of damping the spring has.

Enables/disables springs rotation around the X, Y or Z axis respectively.

Spring Stiffness of the rotation around the X, Y or Z axis respectively. Specifies how “bendy” the spring is.

Spring Damping of the rotation around the X, Y or Z axis respectively. Amount of damping the spring has.

---

## Global Transform¶

**URL:** https://docs.blender.org/manual/en/latest/editors/3dview/animation/copy_global_transform.html

**Contents:**
- Global Transform¶
- Mirror¶
- Relative¶
- Fix to Camera¶
  - Limitations¶

Copy and paste object and bone transforms with ease.

When copying, the global (World Space) transform is placed on the clipboard. This can then be pasted onto any object or bone, at the current frame or at another one.

3D Viewport ‣ Sidebar ‣ Animation ‣ Global Transform

The figure on the right shows the main functionality of the Copy Global Transform panel. The collapsed panels are described each in their own section below.

Inspects the active Object (in Object mode) or Bone (in Pose mode) and places its current global transform onto the clipboard as a matrix.

Takes the copied global transform and applies it to the active Object or Bone. This is done by adjusting its location, rotation, and scale properties.

Same as ‘Paste’ above, but then mirrored relative to some other object or bone. This can be useful, for example, to copy the foot position of one foot to the other. See Mirror below.

Paste as described above and additionally use auto-keying to update one or more frames. The key selection is used to tell Blender which frames this should happen on; it does not influence which parts of the transform are keyed. What is keyed is determined by the active keying set.

Almost the same as Paste to Selected Keys. Instead of only pasting on the selected keys, Paste and Bake will paste & auto-key on every frame between the first and last selected keys.

The copied transform can be mirrored relative to an object or a Bone. This requires choosing that object or bone first.

This will just mirror relative to the chosen object.

Choosing an Armature object as mirror object will show the bone selector. You can use that to pick the bone to use as mirror. This will always use the named bone on that specific armature object.

When you choose no mirror object at all, you can still choose a bone name. This is used for mirroring against a bone in the active armature. This can be useful to mirror bone transforms relative to the ‘chest’ bone of the active character.

After pasting with ‘Paste Mirrored’, the mirror axes can be chosen in the redo panel.

The “Relative” panel has copy/paste buttons that work relative to a chosen object. When copying, the world-space transform is determined, and then adjusted to become relative to the world-space transform of the chosen object. When pasting, this happens in reverse.

If no object is chosen, the copy/paste will happen relative to the active scene camera. What is the active scene camera is determined for every action, so when you paste it can be different from when you copied. This can help to keep an object visually in the same place when switching cameras, or when switching between scenes.

Also known as “bake to camera”, this operator will ensure selected objects/bones remain static (relative to the camera) on unkeyed frames.

This is done by generating new keys. These keys will be of type ‘Generated’ so that it remains clear which keys were manually created, and which were generated. This way the tool can be re-run to re-generate the keys.

Ensure your animation is keyed using constant interpolation. If this is not the case yet, bake your animation (at least the transform channels). This tool does _not_ work with the “Stepped” F-Curve modifier

Choose which of the Location/Rotation/Scale channels you want to fix to the camera. When unsure, make sure they are all checked.

Press the “Fix to Camera” button.

To undo the effect of the “Fix to Camera” operator, click on the trash bin button. That will remove all the generated keys in either the scene range or the frame range.

The tool operates on the scene frame range, or on the preview range if that is active. Keys outside that range are ignored, both when fixing to the camera and when removing generated keys.

This tool assumes that all keys with type ‘Generated’ are equal. It will overwrite them (or remove them, depending on which button you press).

Pasting a transform adjusts the Object/Bone’s location, rotation, and scale. This means that when copying a skewed transform, this skew is lost.

If there are constraints on the Object/Bone, the resulting visual transformation may not be the same as the pasted one. To give a concrete example: if you have a constraint that adds a rotation, it will always add that rotation on top of the pasted transform.

Pose Library for a way to manage and share entire poses.

---

## Goal¶

**URL:** https://docs.blender.org/manual/en/latest/physics/soft_body/settings/goal.html

**Contents:**
- Goal¶
- Settings¶
- Strengths¶

Physics ‣ Soft Body ‣ Goal

Enabling this tells Blender to use the motion from animations (F-Curves, armatures, parents, lattices, etc.) in the simulation. The “goal” is the desired end position for vertices based on this animation.

See exterior forces for details.

Use a vertex group to allow per-vertex goal weights (multiplied by the Default goal).

The spring stiffness for Goal. A low value creates very weak springs (more flexible “attachment” to the goal), a high value creates a strong spring (a stiffer “attachment” to the goal).

The friction coefficient for Goal. Higher values give damping of the spring effect (little jiggle), and the movement will soon come to an end.

Goal weight/strength for all vertices when no Vertex Group is assigned. If you use a vertex group the weight of a vertex defines its goal.

When you use a vertex group, you can use the Minimum and Maximum to fine-tune (clamp) the weight values. The lowest vertex weight will become Minimum, the highest value becomes Maximum.

---

## Hinge Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/constraints/types/hinge.html

**Contents:**
- Hinge Constraint¶
- Options¶

Physics ‣ Rigid Body Constraint

The hinge permits one degree of freedom between two objects. Translation is completely constrained. Rotation is permitted about the Z axis of the object hosting the Physics constraint (usually an Empty, distinct from the two objects that are being linked). Adjusting the position and rotation of the object hosting the constraint allows you to control the anchor and axis of the hinge.

The Hinge is the only single-axis rotational constraint that uses the Z axis instead of the X axis. If something is wrong with your hinge, check your other constraints to see if this might be the problem.

Hinge constraint options.¶

Enables/disables limit rotation around Z axis.

Lower limit of Z axis rotation.

Upper limit of Z axis rotation.

---

## Inverse Kinematics¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/properties/inverse_kinematics.html

**Contents:**
- Inverse Kinematics¶

Bone ‣ Inverse Kinematics

The Inverse Kinematics panel.¶

This panel controls the way a bone or set of bones behave when linked in an inverse kinematic chain.

---

## Inverse Kinematics Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/tracking/ik_solver.html

**Contents:**
- Inverse Kinematics Constraint¶
- Options¶
  - iTaSC Solver¶
- Example¶

The Inverse Kinematics constraint makes not just one bone, but a whole chain of bones rotate to follow a target. A common example is automatically rotating the bones in a character’s arm to achieve a desired hand position. See Inverse Kinematics for details.

The constraint can be added quickly using the shortcut Shift-I. See Add IK to Bone.

The IK constraints are special in that they modify multiple bones. For this reason, they ignore their position in the stack and always run after all other constraints on the affected bones. To apply constraints after IK, it is necessary to first copy the final transformation to a new bone chain, e.g. using Copy Transforms.

Inverse Kinematics constraint.¶

The object or bone which the IK chain should point towards.

Unlike other constraints which require a valid Target, the Inverse Kinematics constraint can work without one. In this case, the “chain tip” bone can be moved and rotated freely, and only its ancestors will be constrained.

The object or bone that determines the roll of the IK chain. For example, when applying IK to a character’s arm and using the Target to determine the position of the hand, the Pole Target determines the rotation of the arm, or put differently, the position of the elbow.

Maximum number of solving iterations.

The number of bones affected by the constraint, starting with the owner bone and walking up its chain of ancestors. A value of 1 will only rotate the bone itself, a value of 2 will rotate the bone and its parent, and so on.

A value of 0 will include all of the bone’s ancestors (up to the root).

Use the bone’s tail as the end of the chain. Unchecking this will use the bone’s head instead.

Whether bones are allowed to scale up or down in order to reach the Target. This only applies to bones with an IK Stretch value that’s greater than 0.

The checkbox determines whether the end of the chain should (try to) match the position of the Target.

The slider determines how strongly this chain affects its bones, compared to other IK chains that affect those same bones. This kind of structure is called a “tree”, likening the chain tip bones to branches and their shared parents to a trunk. If a branch bone has a Weight of 1, it will “pull” on the trunk twice as hard as a branch with a Weight of 0.5.

The checkbox determines whether the end of the chain should match the rotation of the Target.

The slider determines how strongly this chain affects its bones, compared to other IK chains that affect those same bones.

How strongly the constraint affects the bone.

If the armature is configured to use the iTaSC IK Solver, the constraint has the following additional parameters:

Just as with the Standard IK solver, the chain tip matches the location and/or rotation of the Target.

The meaning of the axes in the Lock settings below.

The chain tip should be positioned (or rotated) so that the Target has an X/Y/Z coordinate (or angle) of 0 in the space of the bone.

The chain tip should be positioned (or rotated) so that it has an X/Y/Z coordinate (or angle) of 0 in the space of the Target.

Whether the chain tip is constrained to match the Target along each axis.

Despite their name, these settings do not lock the bones to a fixed pose. For that, see the Lock settings in the bones’ Inverse Kinematics properties.

The end of the chain stays inside, on the surface of, or outside a sphere centered on the Target.

The chain tip stays close to the target.

The chain tip stays away from the target.

The chain tip stays at an exact distance from the target.

The distance to maintain.

---

## In-Betweens¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/editing/in_betweens.html

**Contents:**
- In-Betweens¶
- Push Pose from Rest Pose¶
- Relax Pose to Rest Pose¶
- Push Pose from Breakdown¶
- Relax Pose to Breakdown¶
- Pose Breakdowner¶
- Blend to Neighbor¶

There are several tools for editing poses in an animation.

There are also in Pose Mode a bunch of armature-specific editing options/tools, like auto-bones naming, properties switching/enabling/disabling, etc., that were already described in the armature editing pages. See the links above…

Pose ‣ In-Betweens ‣ Push Pose from Rest Pose

Similar to Push Pose from Breakdown but interpolates the pose to the rest position instead. Only one keyframe is needed for this tool unlike two for the other.

Pose ‣ In-Betweens ‣ Relax Pose to Rest Pose

Similar to Relax Pose to Breakdown but works to bring the pose back to the rest position instead. Only one keyframe is needed for this tool unlike two for the other.

Toolbar ‣ In-Betweens Tools ‣ Push

Pose ‣ In-Betweens ‣ Push Pose from Breakdown

Push Pose interpolates the current pose by making it closer to the next keyframed position.

Toolbar ‣ In-Betweens Tools ‣ Relax

Pose ‣ In-Betweens ‣ Relax Pose to Breakdown

Relax pose is somewhat related to the above topic, but it is only useful with keyframed bones. When you edit such a bone (and hence take it “away” from its “keyed position”), using this tool will progressively “bring it back” to its “keyed position”, with smaller and smaller steps as it comes near it.

Toolbar region ‣ In-Betweens Tools ‣ Breakdowner

Pose ‣ In-Betweens ‣ Pose Breakdowner

Creates a suitable breakdown pose on the current frame.

The Breakdowner tool can be constrained to work on specific transforms and axes, by pressing the following keys while the tool is active:

G, R, S: move, rotate, scale

X, Y, Z: to the corresponding axes

Pose ‣ In-Betweens ‣ Blend to Neighbor

Transitions the current pose with the neighboring keyframes in the timeline. In order for this operator to work, there must be a keyframe before and after the current frame.

---

## Keying Sets¶

**URL:** https://docs.blender.org/manual/en/latest/animation/keyframes/keying_sets.html

**Contents:**
- Keying Sets¶
- Keying Set Panel¶
  - Active Keying Set Panel¶
  - Keyframing Settings¶
- Adding Properties to a Keying Set¶
- Set Active Keying Set¶
- Whole Character Keying Set¶

The Active Keying Sets data ID in the Timeline.¶

Keying Sets are a collection of animated properties that are used to animate and keyframe multiple properties at the same time. For example, pressing K in the 3D Viewport will bring up the available Keying Sets. Blender will then add keyframes for whichever Keying Set is chosen. There are some built-in Keying Sets and also custom Keying Sets called “Absolute Keying Sets”.

This panel is used to add, select, manage “Absolute Keying Sets”.

The Keying Set panel.¶

A List View of Keying Sets in the active scene. Selecting a keying set makes it active

Adds an empty Keying Set.

Removes the active keying set.

A short description of the Keying Set.

Export Keying Set to a Python script File.py. To re-add the Keying Set from the File.py, open then run the File.py from the Text Editor.

Scene ‣ Active Keying Set

This panel is used to add properties to the active Keying Set.

The Active Keying Set panel.¶

A collection of paths in a List View each with a Data Path to a property to add to the active Keying Set.

Removes the selected path.

Set the ID Type and the Object IDs data path for the property.

Set the rest of the Data Path for the property.

Use All Items from the Data Path or select the array index for a specific property.

This controls what group to add the channels to.

Keying Set Name, None, Named Group

These options control all properties in the Keying Set. Note that the same settings in Preferences override these settings if enabled.

These options control individual properties in the Keying Set.

Only insert keyframes where they are needed in the relevant F-Curves.

Insert keyframes based on the visual transformation.

Context menu ‣ Add All/Single to Keying Set

Some ways to add properties to Keying Sets.

RMB the property in the User Interface, then select Add Single to Keying Set or Add All to Keying Set. This will add the properties to the active Keying Set, or to a new Keying Set if none exist.

Hover the mouse over the properties, then press K, to add Add All to Keying Set.

There are several ways to designate the active keying set:

Press Shift-K in the 3D Viewport.

Select a keying set in the Keying Set panel.

Select a keying set in the Keying popover in the Timeline header,

The built-in Whole Character Keying Set is made to keyframe all properties that are likely to get animated in a character rig.

This keying set ignores bones whose name starts with one of the following prefixes, as it assumes these are technical bones that are not meant to be animated directly. The built-in Rigify addon generates such bones, for example.

ORG (Original from meta rig)

---

## Lattice¶

**URL:** https://docs.blender.org/manual/en/latest/animation/lattice.html

**Contents:**
- Lattice¶
- Editing¶
- Properties¶
  - Lattice¶
- Usage¶

Lattice – or commonly called deformation cage outside of Blender. A lattice consists of a three-dimensional non-renderable grid of vertices. Its main use is to apply a deformation to the object it controls with a Lattice Modifier. If the object is parented with Lattice Deform a Lattice Modifier is automatically applied.

Mirrors the vertices displacement from their base position.

Resets the whole lattice to a regular grid, where the cells are scaled to one cubic unit.

Rate of subdivision in the axes:

Selector for each axis. See Different types of interpolation..

Linear, Cardinal, Catmull-Rom, B-Spline

Takes only the vertices on the surface of the lattice into account.

The strength of the influence assigned as a weight to the individual vertices in the selected vertex group.

The lattice should be scaled and moved to fit around your object in Object Mode. Any scaling applied to the object in Edit Mode will result in the object deforming. This includes applying its scale with Ctrl-A as this will achieve the same result as scaling the lattice in Edit Mode, and therefore the object.

Lattice around the cube object in Object Mode.¶

---

## Limit Distance Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/transform/limit_distance.html

**Contents:**
- Limit Distance Constraint¶
- Options¶
- Example¶

The Limit Distance constraint forces an object or bone to stay further from, nearer to, or exactly at a given distance from a target. In other words, the owner’s location is constrained to be either outside, inside, or on the surface of a sphere centered on the target.

This constraint has no effect on connected bones as their position is determined by their parent bone.

Limit Distance constraint.¶

The object or bone to stay close to/keep away from.

The limit distance, i.e. the radius of the constraining sphere. It’s calculated automatically when selecting the first target.

Set the Distance to the current distance between owner and target.

How to constrain the owner relative to the spherical boundary:

Keep the owner trapped within the sphere.

Prevent the owner from entering the sphere.

Constrain the owner to the surface of the sphere.

When the owner is manually moved around, restrict not just its visual position but also its Location in the Properties Editor’s Transform panel.

The spaces for retrieving the position of the target and for applying the constrained result to the owner.

How strongly the constraint affects the owner.

Evaluating both owner and target in a Custom Space will automatically scale the Distance according to the scale of the space’s object/bone.

---

## Limit Location Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/transform/limit_location.html

**Contents:**
- Limit Location Constraint¶
- Options¶
- Example¶

The Limit Location constraint forces an object or bone to stay above a coordinate, below a coordinate, or between two coordinates along one or more axes.

Like other constraints, Limit Location only looks at the origin for objects; their geometry is not taken into account. This means that, if a cube’s origin is at its center and a Limit Location constraint is added for the coordinates of a floor plane, the cube will still be able to sink halfway into the plane.

This constraint has no effect on connected bones as their position is determined by their parent bone.

Limit Location constraint.¶

The number fields determine the boundaries for each axis. The checkboxes determine whether each boundary applies.

If a Minimum is higher than the corresponding Maximum, the constraint uses the Maximum for both.

When the owner is manually moved around, restrict not just its visual position but also its Location in the Properties Editor’s Transform panel.

The space for determining and limiting the position of the owner.

How strongly the constraint affects the owner.

---

## Limit Rotation Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/transform/limit_rotation.html

**Contents:**
- Limit Rotation Constraint¶
- Options¶
- Example¶

The Limit Rotation constraint limits the Euler rotation angle for each axis to a certain range.

Angles outside a range are clamped to whichever boundary is closer on a circle. For example, if an axis is limited to the range 0°-90° and the original rotation is 340°, the constraint changes this to 0°, not 90°.

This constraint doesn’t work for bones that are affected by Inverse Kinematics. Please use the Limit settings in the bone’s IK panel instead.

Limit Rotation constraint.¶

The number fields determine the angle range for each axis. The checkboxes determine whether each range applies.

Even if all limits are disabled, the constraint still removes shearing as a side effect.

The Euler order to use when applying the limits. Defaults to the order of the owner, or XYZ if the owner uses a non-Euler rotation.

When the owner is manually rotated, restrict not just its visual rotation but also its Rotation in the Properties Editor’s Transform panel.

For backwards compatibility: make the constraint behave in the semi-broken way it did prior to Blender 4.2. This old behavior does not properly account for the looping nature of rotations, and therefore causes unpredictable/erratic rotation snapping. However, this behavior can still be useful in some specific circumstances when Owner is set to Local Space, and some older rig setups utilize that. However, that behavior is better and more robustly accomplished with drivers directly on the object/bone’s rotation properties, so new rigs should favor that approach over using this option.

The space for determining and limiting the rotation of the owner.

How strongly the constraint affects the owner.

---

## Limit Scale Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/transform/limit_scale.html

**Contents:**
- Limit Scale Constraint¶
- Options¶
- Example¶

The Limit Scale constraint applies a lower and/or upper bound to an object or bone’s scale along each axis.

While it’s possible to set limits of 0 or less, these will not work correctly and should be avoided.

Limit Scale constraint.¶

The number fields determine the boundaries for each axis. The checkboxes determine whether each boundary applies.

If a Minimum is higher than the corresponding Maximum, the constraint uses the Maximum for both.

When the owner is manually scaled, restrict not just its visual scale but also its Scale in the Properties Editor’s Transform panel.

The space for determining and limiting the scale of the owner.

How strongly the constraint affects the owner.

---

## Locked Track Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/tracking/locked_track.html

**Contents:**
- Locked Track Constraint¶
- Options¶
- Example¶

The Locked Track constraint makes an object or bone point towards a certain target. It’s typically called “Look At” or “Aim” in other 3D software.

The word “locked” means that the object or bone can only rotate around one axis. The orientation of this axis always stays the same, and the other two axes always stay in their original plane.

One example use case is distant tree billboards, which should turn to face the camera while also staying upright. Another example is a compass on a table with a nearby magnet: the needle spins horizontally to point at the magnet, but it can never point up or down.

This constraint can be used in combination with other Track constraints. For example, first add a Damped Track constraint to orient the X/Y plane based on one target, then add a Locked Track constraint to rotate within that plane towards another target.

Locked Track constraint.¶

The object or bone to point towards.

The local axis of the owner that should point at the target. For bones, this should typically be Y.

A negative axis will make the owner point away from the target instead.

The local axis of the owner that should keep its orientation. In other words, the only axis which the owner can rotate around.

The Track Axis and the Locked Axis must be different. If they are the same, the constraint will stop working and its icon will turn red.

How strongly the constraint affects the owner.

---

## Markers¶

**URL:** https://docs.blender.org/manual/en/latest/animation/markers.html

**Contents:**
- Markers¶
- Types¶
- Visualization¶
  - Standard¶
  - 3D Viewport¶
  - Pose Markers¶
- Add Marker¶
  - Pose Markers¶
- Selecting¶
- Editing¶

Markers are used to denote frames with key points or significant events within an animation. E.g. it could be that a character’s animation starts, the camera changes position, or a door opens. Markers can be given names to make them more meaningful at a quick glance. They are available in many of Blender’s editors.

Unlike keyframes, markers are always placed at a whole frame number, you cannot set a marker at frame 2.5.

Markers can be created and edited in the following editors:

Video Sequence Editor

A marker created in one of these editors will also appear in all others that support them.

Besides standard markers, pose markers are another type of markers, which are specific to armatures and shape keys. They are used to denote poses in the Action Editor mode and Shape Keys Editor of Dope Sheet.

In the supported editors, if at least one is created, markers are visualized in a separate row at their bottom. This area can be disabled per editor via the View ‣ Show Markers menu option.

While the markers area is disabled, markers operators are not available in that editor, and in the header the Marker menu is hidden.

Regular markers are shown as small white triangles, empty if unselected or filled if selected, and with a dashed line that covers the editor height at the corresponding frame. If they have a name, this is shown to their right in white.

The 3D Viewport does not allow you to create, edit or remove markers, but it shows their name in the Object Info in the upper left corner, when on their frame.

Pose markers show a diamond-shaped icon in the Dope Sheet. In the NLA editor pose markers are shown as a red dashed line inside the relative action strip.

The simplest way to add a marker is to move to the frame where you would like it to appear, and press M.

Markers can also be added during playback.

If Show Pose Markers is enabled, a pose marker is added.

Click LMB on the marker’s triangle to select it. Use Shift-LMB to select multiple markers.

In the Graph Editor, Dope Sheet, NLA Editor, Timeline, and Video Sequence Editor, you can also select all markers with A while hovering the mouse over the marker row, and apply selection tools on them like Box Select, etc. (as usual, LMB to select, RMB to deselect). The corresponding options are found in the Select menu of these editors.

Marker ‣ Duplicate Marker

You can duplicate the selected markers by pressing Shift-D. Once duplicated, the new ones are automatically placed in select mode, so you can move them to the desired location.

Note that unlike most other duplications in Blender, the names of the duplicated markers are not altered at all (no .001 numeric counter append).

Marker ‣ Duplicate Marker to Scene…

Duplicates the selected markers into another scene.

Marker ‣ Delete Marker

To delete the selected markers simply press X, and confirm the pop-up message with LMB.

Marker ‣ Rename Marker

Having dozens of markers scattered throughout your scene’s time will not help you much unless you know what they stand for. You can name a marker by selecting it, pressing F2, typing the name, and press Return

Once you have one or more markers selected, press G, while hovering with the mouse over the marker bar, to move them, and confirm the move with LMB or Return (as usual, cancel the move with RMB, or Esc). Or drag them with the LMB.

By default, you move the markers in one-frame steps, but if you hold Ctrl, the markers will move in steps corresponding to 1 second (according to the scene’s FPS).

Convenient operators for selecting Marks; see Selecting for more information on selecting Markers.

Deselects any already selected Markers.

Select all unselected Markers and deselects all selected Markers.

Selects all Markers to the left of the current frame and the Marker on the current frame if it exists.

Selects all Markers to the Right of the current frame and the Marker on the current frame if it exists.

Action Editor or Shape Keys Editor mode

Marker ‣ Show Pose Markers

Shows markers belonging to the active action instead of scene markers.

Marker ‣ Make Markers Local

It is possible to convert standard markers into pose markers with Marker ‣ Make Markers Local. Note that the original marker will be gone. If you want to keep it, make a duplicate before you convert.

Marker ‣ Jump to Next/Previous Marker

Moves the Playhead to the next/previous marker relative to the current frame.

Marker ‣ Bind Camera to Markers

Bind Camera to Markers allows markers to be used to set the active object as the active camera.

To use this operator, select the object to become the active camera and select a marker to bind the active camera to. If no marker is selected when the operator is applied, a marker will be added. When an object is bound to a marker, the marker will be renamed to the name of the active object. These markers also have a camera icon next to the left of the name to easily distinguish them from other informative markers.

These markers can be moved to change the frame at which the active camera is changed to the object the marker is bound to.

---

## Mask¶

**URL:** https://docs.blender.org/manual/en/latest/editors/dope_sheet/modes/mask.html

**Contents:**
- Mask¶

This mode shows all the masks in the blend-file (that have at least one layer) and lets you adjust their keyframes.

The Mask mode of the Dope Sheet Editor.¶

---

## Motion Paths¶

**URL:** https://docs.blender.org/manual/en/latest/animation/motion_paths.html

**Contents:**
- Motion Paths¶
- Options¶
  - Display¶
- Example¶

3D Viewport, Properties

Properties ‣ Object Properties ‣ Motion Paths

3D Viewport, Properties

Properties ‣ Armature ‣ Motion Paths

An animated cube with its motion path displayed.¶

The Motion Paths tool allows you to visualize the motion of points as paths over a series of frames. These points can be object origins and bone joints.

To create or remove motion paths, it is necessary to first select the bones. Then:

To show the paths (or update them, if needed), click on the Calculate Path button.

To hide the paths, click on the Clear Paths button.

Remember that only selected bones and their paths are affected by these actions!

The paths are shown in red for the section in the past and green for the section in the future. These colors follow the user preference options “Before Current Frame” and “After Current Frame”, which can be found in the 3D Viewport section. Each frame is displayed by a small dot on the paths.

The paths are automatically updated when you edit your poses/keyframes, and they are also active during animation playback. Playing the animation affects the paths only when using the Around Frame type.

The Motion Paths panel in the Armature tab.¶

Type of range to show for Motion Paths.

Display paths of points within a fixed number of frames around the current frame. When you enable this button, you get paths for a given number of frames before and after the current one

Display paths of points within specified range.

The range of the motion path. Only active when Paths Type is set to In Range. Changing this option only takes effect when updating the path, via the Update Path or Update All Paths buttons.

Generate a motion path ranging from the first keyframe to the last. Only the keys of the active object / bone are considered.

Same as All Keys except that it ranges from the first to the last selected keyframe.

Use the start & end frames of the scene, or the preview range if active.

Manually set the start and end frame.

Starting and Ending frame of range of paths to display/calculate (not for the Around Frame type).

Although the start and end frame are always editable, updating the motion path will change these according to the Calculation Range setting. To ensure your chosen frame range is maintained, choose Manual Range there.

Number of frames to show before and after the current frame (only for the Around Frame type).

Allows displaying one point for every n frames on the path. Mostly useful when you enable the frame number display (see below), to avoid cluttering the 3D Viewport.

When enabled the motion path is calculated in screen space for the active scene camera. Note that the resulting motion path will only be useful for that single camera. Switching cameras using markers is not supported. It will only bake to the camera that is active when the bake was started.

These are the start/end frames of the range in which motion paths are shown. You cannot modify this range without deleting the motion path first.

If no paths have been calculated, Calculate Paths will create a new motion path in cache based on the options specified in the pop-up menu or the Adjust Last Operation panel. Note, if the current context is an Armature calculating the objects motion paths, and not the bones, this operator will calculate the motion paths for all the bones within the armature as well.

These are the start/end frames of the range in which motion paths are shown. The start frame is inclusive, so if you set Start to 1, you will really see the frame 1 as starting point of the paths…

Which point on the bones is used when calculating paths. Only available for bones while in Pose Mode.

Calculates the path position of the bone’s heads.

Calculates the path position of the bone’s heads.

In the case a path has already been calculated, this operator will update the path shape to the current animation. To change the frame range of the calculated path, you need to delete the path and calculate it again.

Clears paths on all objects/bones or just the selected ones when holding Shift.

Recalculates the motion paths for all visible objects and poses.

When enabled, a small number appears next to each frame dot on the path, which is of course the number of the corresponding frame.

When enabled, big yellow square dots are displayed on motion paths, showing the keyframes of their bones (i.e. only the paths of keyed bones at a given frame get a yellow dot at this frame).

For bone motion paths, it searches the whole Action for keyframes instead of in groups with matching name only (this is slower).

When enabled, you will see the numbers of the displayed keyframes, so this option is obviously only valid when Show Keys is enabled.

Toggles whether the lines between the points are shown.

Line thickness for motion path.

Use custom color for this motion path. The custom color can be modified for time before and after the current frame.

An example of a motion path of an armature.¶

---

## Motor Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/constraints/types/motor.html

**Contents:**
- Motor Constraint¶
- Options¶

Physics ‣ Rigid Body Constraint

The motor constraint causes translation and/or rotation between two entities. It can drive two objects apart or together. It can drive simple rotation, or rotation and translation (although it will not be constrained like a screw since the translation can be blocked by other physics without preventing rotation).

The rotation axis is the X axis of the object hosting the constraint. This is in contrast with the Hinge which uses the Z axis. Since the Motor is vulnerable to confusing perturbations without a matching Hinge constraint, special care must be taken to align the axes. Without proper alignment, the motor will appear to have no effect (because the hinge is preventing the motion of the motor).

Motor constraint options.¶

Enable linear or angular motor respectively.

Target linear or angular motor velocity respectively.

Maximum linear or angular motor impulse respectively.

---

## Naming¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/naming.html

**Contents:**
- Naming¶
- Naming Conventions¶
- Auto-Name¶
- Flip Names¶

Properties ‣ Bone Properties

You can rename your bones, either using the Name field in the Bones Properties. It is also possible to rename by double-clicking bones in the Outliner.

Blender also provides you some tools that take advantage of bones named in a left/right symmetry fashion, and others that automatically name the bones of an armature.

Naming conventions in Blender are not only useful for you in finding the right bone, but also to tell Blender when any two of them are counterparts.

In case your armature can be mirrored in half (i.e. it is bilaterally symmetrical), it is worthwhile to stick to a left/right naming convention. This will enable you to use some tools that will probably save you time and effort (like the X-Axis Mirror editing tool).

An example of left/right bone naming in a simple rig.¶

First you should give your bones meaningful base-names, like “leg”, “arm”, “finger”, “back”, “foot”, etc.

If you have a bone that has a copy on the other side (a pair), like an arm, give it one of the following separators:

Left/right separators can be either the second position “L_calf_bone” or last-but-one “calf_bone.R”.

If there is a lower or upper case “L”, “R”, “left” or “right”, Blender handles the counterpart correctly. See below for a list of valid separators. Pick one and stick to it as close as possible when rigging; it will pay off.

Examples of valid separators:

(nothing): handLeft –> handRight

“_” (underscore): hand_L –> hand_R

“.” (dot): hand.l –> hand.r

“-” (dash): hand-l –> hand-r

“ “ (space): hand LEFT –> hand RIGHT

Note that all examples above are also valid with the left/right part placed before the name. You can only use the short “L”/ “R” code if you use a separator (e.g. “handL”/ “handR” will not work!).

Before Blender handles an armature for mirroring or flipping, it first removes the number extension, e.g. “.001”.

You can copy a bone named “blah.L” and flip it over using Flip Names. Blender will name the copy “blah.L.001” and flipping the name will give you “blah.R”.

Armature ‣ Names ‣ Auto-Name Left/Right, Front/Back, Top/Bottom

The three AutoName entries of the Armature ‣ Names menu allow you to automatically add a suffix to all selected bones, based on the position of their root relative to the armature’s origin and its local coordinates:

Will add the “.L” suffix to all bones with a positive X coordinate root, and the “.R” suffix to all bones with a negative X coordinate root. If the root is exactly at 0.0 on the X axis, the X coordinate of the tip is used. If both joints are at 0.0 on the X axis, the bone will just get a period suffix, with no “L”/ “R” (as Blender cannot decide whether it is a left or right bone…).

Will add the “.Bk” suffix to all bones with a positive Y coordinate root, and the “.Fr” suffix to all bones with a negative Y coordinate root. The same as with AutoName Left-Right goes for 0.0 Y coordinate bones…

Will add the “.Top” suffix to all bones with a positive Z coordinate root, and the “.Bot” suffix to all bones with a negative Z coordinate root. The same as with AutoName Left-Right goes for 0.0 Z coordinate bones…

Armature ‣ Names ‣ Flip Names

You can flip left/right markers (see above) in selected bone names. This can be useful if you have constructed half of a symmetrical rig (marked for a left or right side) and duplicated and mirrored it, and want to update the names for the new side. Blender will swap text in bone names according to the above naming conventions, and remove number extensions if possible.

---

## Navigating¶

**URL:** https://docs.blender.org/manual/en/latest/editors/dope_sheet/navigating.html

**Contents:**
- Navigating¶
- View Menu¶
- Filters¶
- Playback Controls¶

As with most editors, you can:

Pan the view vertically (channels) and horizontally (time) by dragging MMB.

Zoom in and out by rolling Wheel or dragging Ctrl-MMB.

You can also use the scrollbars for this.

Shows or hides the Sidebar Region.

Displays a pop-up panel to alter the properties of the last completed operation. See Adjust Last Operation.

Shows or hides the Channels region (the list of animated property names on the left).

Show or hide the Playback Controls.

Pans and zooms the view to focus on the selected keyframes.

Pans and zooms the view to show all keyframes.

Reset the horizontal view to the current scene frame range, taking the preview range into account if it is active.

Pans the view so the Playhead is in the center.

Lets you filter by multiple search terms instead of just one (in the search textbox above the channel list and in the Filters popover). The terms are space-separated, so you can for example type “loc rot” to find all channels that have “loc” or “rot” in their name. If this option were disabled, the list would only show channels containing the text “loc rot”, of which there are likely none.

Whether to update other views (such as the 3D Viewport) while you’re moving keyframes around. If disabled, the other views only get updated once you finish the move.

Shows a value slider next to each channel. Adjusting such a slider automatically creates a keyframe.

Displays keyframes using shapes that represent their Bézier handle type. In addition, if a keyframe uses a non-default interpolation type for the curve segment that comes after it, this is indicated by a green line.

See Handles & Interpolation Display.

Detects keys where the curve changes direction, and marks them by displaying an arrow inside their shape. Local maxima (hills) are shown as up arrows, while local minima (valleys) are shown as down arrows.

A keyframe may show both arrows, namely when it’s part of a summary row containing a channel with a maximum and one with a minimum.

Automatically merge keyframes that end up on the same frame after transformation.

Shows the marker region (provided any markers have been defined). When disabled, the Marker menu is also hidden and marker operators are not available in this editor.

Shows timing in seconds instead of frames.

Synchronizes the horizontal panning and scale of the editor with other time-based editors that also have this option enabled. That way, they always show the same section of time.

Lets you drag a box to define a time range for previewing. As long as this range is active, playback will be limited to it, letting you repeatedly view a segment of the animation without having to manually rewind each time.

You can change the start or end frame using the corresponding button in the Timeline editor’s Playback popover. Alternatively, you can simply run Set Preview Range again.

Clears the preview range.

Applies a preview range that encompasses the selected keyframes.

Changes the area’s editor to the Graph Editor.

Which simulation caches to show on the timeline.

Baked simulations will be shown as fully opaque, cached simulations will be slightly transparent, and invalid caches will be slightly transparent with dark diagonal stripes.

Area controls. See the user interface documentation for more information.

These filters are available in the funnel dropdown button in the header.

Toggles the “Summary” row at the top of the Channels region. This row shows the union of all keyframes across all channels.

Only show keyframes belonging to objects/bones/… that are selected.

If this option is enabled, the Dope Sheet may not show all material keyframes of the selected objects. Instead, it only shows the keyframes belonging to the selected nodes in the Shader Editor.

Show keyframes from objects/bones/… that are hidden.

Only show channels that have errors (for example, because they try to animate a property that doesn’t exist on the object).

Filters the channel list by a search term (or multiple search terms if Multi-Word Match Search is enabled).

Select a collection to only show keyframes from objects in that collection.

Filter curves by property type.

Sorts data-blocks alphabetically to make them easier to find.

If your playback speed suffers because of this (should only really be an issue when working with lots of objects), you can turn it off.

The Playback Controls region contains controls and options related to playback, keying, auto keyframing, and transport.

These settings allow you to:

Control how animations are previewed and synchronized with audio.

Insert and manage keyframes through keying sets and auto keying.

Navigate the timeline using playback and transport controls.

Adjust frame ranges and preview specific segments of the animation.

For a detailed description of all properties and controls commonly found in the footer, see the Playback Controls documentation.

---

## Object Solver Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/motion_tracking/object_solver.html

**Contents:**
- Object Solver Constraint¶
- Usage¶
- Options¶

The Object Solver constraint makes a Blender object imitate the motion of a real-world object.

Start by loading a video file into the Movie Clip Editor, registering the physical object in the Objects Panel, and using motion tracking to track at least eight markers on that physical object. Then use Solve Camera/Object Motion to reconstruct the motion of the physical object, and finally add this constraint to a Blender object.

Object Solver constraint.¶

Whether the physical object is in the scene’s Active Clip. If unchecked, a selector appears for choosing another clip.

The physical object whose motion to imitate. See the Objects Panel in the Movie Clip Editor’s Sidebar for setting this up.

The Blender camera matching the physical camera that recorded the object. If left empty, the scene’s active camera is used.

If the physical camera was in motion, the Blender camera should have a Camera Solver Constraint. This constraint is useful even if the physical camera was stationary, because it makes the tracking markers appear at their reconstructed world positions in the 3D Viewport (if the Motion Tracking overlay is enabled).

Tell the constraint that the current Location of the Blender object (that is, its position with the constraint disabled) is the correct position for the current frame. Once this information is saved, the object will also be in the correct position for the other frames.

When initially adding the constraint:

Bring the object into position for the current frame.

When tweaking the object’s position at a later point:

Run Apply Visual Transform. (This may move the object to a different position.)

Disable the constraint. (This will bring the object back to its previous position.)

Tweak the object’s position as desired.

Enable the constraint.

Resets the relative transformation that was stored by Set Inverse.

Replaces the constraint by a set of equivalent keyframes.

How strongly the constraint affects its owner.

---

## Parenting¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/parenting.html

**Contents:**
- Parenting¶
- Bone Collections¶

Properties ‣ Bones ‣ Relations

You can edit the relationships between bones (and hence create/modify the chains of bones) both from the 3D Viewport and the Properties. Whatever method you prefer, it’s always a matter of deciding, for each bone, if it has to be parented to another one, and if so, if it should be connected to it.

To parent and/or connect bones, you can:

In the 3D Viewport, select the bone and then its future parent, and press Ctrl-P (or Armature ‣ Parent ‣ Make Parent…). In the small Make Parent menu that pops up, choose Connected if you want the child to be connected to its parent, else click on Keep Offset. If you have selected more than two bones, they will all be parented to the last selected one. If you only select one already-parented bone, or all selected bones are already parented to the last selected one, your only choice is to connect them, if not already done. If you select only one non-parented bone, you will get the Need selected bone(s) error message…

With this method, the newly-children bones will not be scaled nor rotated – they will just be moved if you choose to connect them to their parent’s tip.

In the Properties, Bones tab, for each selected bone, you can select its parent in the Parent data ID to the upper right corner of its Relations panel. If you want them to be connected, just enable the checkbox to the right of the list.

With this method, the tip of the child bone will never be moved – so if Connected is enabled, the child bone will be completely transformed by the operation.

The starting armature, with Bone.005 parented and connected to Bone.004.¶

Bone.005 re-parented to Bone.002, but not connected to it (same result, using either Ctrl-P 2 in 3D Viewport, or the Bones tab settings).¶

Bone.005 parented and connected to Bone.002, using Ctrl-P 1 in 3D Viewport.¶

Bone.005 parented and connected to Bone.002.¶

Using the Parent data ID of Bone.005 Relations panel.

To disconnect and/or free bones, you can:

In a 3D Viewport, select the desired bones, and press Alt-P (or Armature ‣ Parent ‣ Clear Parent…). In the small Clear Parent menu that pops up, choose Clear Parent to completely free all selected bones, or Disconnect Bone if you just want to break their connections.

In the Properties, Bones tab, for each selected bone, you can select no parent in the Parent data ID of its Relations panel, to free it completely. If you just want to disconnect it from its parent, disable the Connected checkbox.

Note that relationships with non-selected children are never modified.

Armature ‣ Bone Collections, Pose ‣ Bone Collections

Manages the Bone Collections the bone is assigned to.

Move bones to a collection.

Assign all selected bones to a collection, or unassign them, depending on whether the active bone is already assigned or not.

Unhides any hidden bone collections.

Assigns the selected bones to a new collection named “New Collection”. This collection can be renamed in the Bone Collections panel of the Armature properties.

---

## Piston Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/constraints/types/piston.html

**Contents:**
- Piston Constraint¶
- Options¶

Physics ‣ Rigid Body Constraint

A piston permits translation along the X axis of the constraint object. It also allows rotation around the X axis of the constraint object. It is like a combination of the freedoms of a slider with the freedoms of a hinge (neither of which is very free alone).

Enables/disables limit translation around X axis.

Lower limit of X axis translation.

Upper limit of X axis translation.

Enables/disables limit rotation around X axis.

Lower limit of X axis rotation.

Upper limit of X axis rotation.

---

## Pivot Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/relationship/pivot.html

**Contents:**
- Pivot Constraint¶
- Options¶
- Example¶

The Pivot constraint makes an object or bone rotate around a point other than its origin. This can be a point that’s relative to the same or another object/bone, or a point that’s fixed in space.

The object or bone to use as the pivot point. Can be left empty, in which case the pivot point is either relative to the constraint owner itself or not relative to anything (fixed in space).

Whether the Pivot Point coordinates are relative to the constraint owner or absolute in the world. If a Target is set, the coordinates are always relative.

The coordinates of the pivot point.

Euler axis and direction for which the constraint should be active.

Apply pivoting for every possible owner rotation.

Only apply pivoting if the owner’s X/Y/Z rotation is negative or zero.

Only apply pivoting if the owner’s X/Y/Z rotation is positive or zero.

How strongly the constraint affects the owner.

---

## Point Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/constraints/types/point.html

**Contents:**
- Point Constraint¶

Physics ‣ Rigid Body Constraint

The objects are linked by a point bearing allowing any kind of rotation around the location of the constraint object, but no relative translation is permitted. The physics engine will do its best to make sure that the two points designated by the constraint object on the two constrained objects are coincident.

Point constraint options.¶

---

## Propagate¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/editing/propagate.html

**Contents:**
- Propagate¶

The Propagate tool copies the pose of the selected bones on the current frame over to the keyframes delimited by the Termination Mode. It automates the process of copying and pasting.

Modes which determine how it decides when to stop overwriting keyframes.

Simply copies the pose to the first keyframe after (but not including any keyframe on) the current frame.

Will simply replace the last keyframe (i.e. making action cyclic).

To all keyframes between current frame and the End frame option. This option is best suited for use from scripts due to the difficulties in setting this frame value, though it is possible to set this manually via the Adjust Last Operation panel if necessary.

To all keyframes from current frame until no more are found.

Will apply the pose of the selected bones to all selected keyframes.

To all keyframes occurring on frames with Scene Markers after the current frame.

Defines the upper-bound for the frame range within which keyframes will be affected (with the lower bound being the current frame).

---

## Properties¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/properties.html

**Contents:**
- Properties¶

Armature ‣ Bone Settings ‣ …

Shift-W, Shift-Ctrl-W, Alt-W

Most bones’ properties (except the transform ones) are regrouped in each bone’s panels, in the Bones tab in Edit Mode. Let us detail them.

Note that some of them are also available in the 3D Viewport, through the three pop-up menus within the same entry:

Toggle Setting: Shift-W or Armature ‣ Bone Settings ‣ Toggle a Setting

Enable Setting: Shift-Ctrl-W or Armature ‣ Bone Settings ‣ Enable a Setting

Disable Setting: Alt-W or Armature ‣ Bone Settings ‣ Disable a Setting

Always display the bone as wireframe.

(also Shift-W ‣ (Deform, …)).

(also Shift-W ‣ (Multiply Vertex Group by Envelope, …)).

These settings control how the bone influences its geometry, along with the bones’ joints radius. This will be detailed in the skinning part.

The bone automatically rotates together with its parent in Pose Mode. For more details, see the relations page.

(also Shift-W ‣ (Locked, …)) This will prevent all editing of the bone in Edit Mode; see bone locking.

---

## Relations¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/properties/relations.html

**Contents:**
- Relations¶
- Parenting¶
  - Transformations¶
- Bone Collections¶

Bone Relations panel.¶

In this panel you can manage the relationship of this bone with its parent bone. It also shows the bone collections the bone is assigned to.

A Data ID to select the bone to set as a parent.

Changes how transformation of the bone is applied to its child Objects.

The Connected checkbox set the head of the bone to be connected with its parent root.

Bones relationships have effects on transformations behavior.

By default, children bones inherit:

Their parent position, with their own offset of course.

Their parent rotation (i.e. they keep a constant rotation relatively to their parent).

Their parent scale, here again with their own offset.

The armature in its rest position.¶

Rotation of a root bone.¶

Scaling of a root bone.¶

Exactly like standard children objects. You can modify this behavior on a per-bone basis, using the Relations panel in the Bones tab:

When disabled, the location transform property is evaluated in the parent bone’s local space, rather than using the bone’s own rest pose local space orientation.

When disabled, this will “break” the rotation relationship to the bone’s parent. This means that the child will keep its rotation in the armature object space when its parent is rotated.

Specifies which effects of parent scaling the bone inherits:

These inheriting behaviors propagate along the bones’ hierarchy. So when you scale down a bone, all its descendants are by default scaled down accordingly. However, if you disable one bone’s Inherit Scale or Inherit Rotation property in this “family”, this will break the scaling propagation, i.e. this bone and all its descendants will no longer be affected when you scale one of its ancestors.

The bone inherits all effects of parent scaling and shear.

Full parent effects are applied to the rest state of the child, after which any shear is removed in a way that preserves the bone direction, length and volume, and minimally affects roll on average. The result is combined with the local transformation of the child.

If the inherited scale is non-uniform, this does not prevent shear from reappearing due to local rotation of the child bone, or of its children.

Parent scaling is inherited as if the child was oriented the same as the parent, always applying parent X scale over child X scale, and so on.

Inherits a uniform scaling factor that is the total change in the volume of the parent.

Ignores all scaling and shear of the parent.

Ignores all scaling, provided the parent is not sheared. If it is, there are no guarantees.

This choice replicates the behavior of the old Inherit Scale checkbox, and may be removed in a future release.

The various Inherit Scale options are provided as tools in avoiding shear that is caused by non-uniform scaling combined with parenting and rotation. There is no obvious best way to achieve that, so different options are useful for different situations.

None – Useful for gaining full control over the scaling of the child in order to e.g. manually overwrite it with constraints.

Average – Useful to block squash and stretch propagation between sub-rigs, while allowing uniform changes in the size and volume to pass through.

Aligned – Can be used within bone chains, e.g. tentacles, in order to propagate lengthwise scaling as lengthwise, and sideways as sideways, no matter how the tentacle bends. Similar to using None with Copy Scale from parent.

Fix Shear – May be useful at the base of an appendage in order to reallocate squash and stretch between axes based on the difference in rest pose orientations of the parent and child. It behaves closest to Full while suppressing shear.

The yellow outlined Inherit Rotation disabled bone in the armature.¶

Rotation of a bone with an Inherit Rotation disabled bone among its descendants.¶

Scaling of a bone with an Inherit Rotation disabled bone among its descendants.¶

Connected bones have another specificity: they cannot be moved. Indeed, as their root must be at their parent’s tip, if you do not move the parent, you cannot move the child’s root, but only its tip, which leads to a child rotation. This is exactly what happens, when you press G with a connected bone selected, Blender automatically switches to rotation operation.

Bones relationships also have important consequences on how selections of multiple bones behave when transformed. There are many different situations which may not be included on this list, however, this should give a good idea of the problem:

Non-related selected bones are transformed independently, as usual.

When several bones of the same “family” are selected, only the “most parent” ones are really transformed – the descendants are just handled through the parent relationship process, as if they were not selected (see Fig. Scaling bones, some of them related. the third tip bone, outlined in yellow, was only scaled down through the parent relationship, exactly as the unselected ones, even though it is selected and active. Otherwise, it should have been twice smaller!)

Scaling bones, some of them related.¶

When connected and unconnected bones are selected, and you start a move operation, only the unconnected bones are affected.

When a child connected hinge bone is in the selection, and the “most parent” selected one is connected, when you press G, nothing happens, because Blender remains in move operation, which of course has no effect on a connected bone.

So, when posing a chain of bones, you should always edit its elements from the root bone to the tip bone. This process is known as Forward Kinematics (FK). We will see in a later page that Blender features another pose method, called Inverse Kinematics (IK), which allows you to pose a whole chain just by moving its tip.

This feature is somewhat extended/completed by the pose library.

This list shows the bone collections the bone is assigned to. Press the eye icon to show or hide the entire bone collection. Press the star icon to show only this bone collection, and others also marked as ‘solo’ Press the X icon to remove the bone from that particular collection.

To assign the bone to other bone collections, either use the M or Shift-M shortcuts (see Moving Bones Between Collections) or go to the Armature properties panel.

---

## Selecting Bones¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/selecting.html

**Contents:**
- Selecting Bones¶
- All¶
- None¶
- Invert¶
- Box Select¶
- Circle Select¶
- Lasso Select¶
- Select Mirror¶
- Select More/Less¶
- Select Grouped¶

Selection in Pose Mode is very similar to the one in Edit Mode, with a few deviations: You can only select whole bones in Pose Mode, not roots/tips…

Select all selectable bones.

Deselect all bones, but the active bone stays the same.

Toggle the selection state of all visible bones.

Interactive box selection.

Select ‣ Circle Select

Interactive circle selection.

Select ‣ Lasso Select

Select ‣ Select Mirror

Flip the selection from one side to another.

You can deselect the active bone and select its immediate parent or one of its children.

Similar to Parent/Child but it keeps the active bone in the selection.

Select ‣ Select Grouped

You can select bones, based on various properties, through the Select Grouped pop-up menu Shift-G:

Selects all bones that are share at least one bone collection with the active bone.

Selects all bones that have the same color as the active bone.

All bones affected by active Keying Set

Select all children of currently selected bones.

Select direct children of currently selected bones.

Select the parents of currently selected bones.

Select all bones that have the same parent as currently selected bones.

Select ‣ Select Linked

Selects all the bones in the chain which the active (last selected) bone belongs to.

Selects all bones connected to the active bone even if the branch off from the current bone.

A single selected bone.¶

Its whole chain selected with Linked.¶

Select ‣ Select Pattern…

Selects all bones whose name matches a given pattern. Supported wild-cards: * matches everything, ? matches any single character, [abc] matches characters in “abc”, and [!abc] match any character not in “abc”. As an example *house* matches any name that contains “house”, while floor* matches any name starting with “floor”.

The matching can be chosen to be case sensitive or not.

When Extend checkbox is checked the selection is extended instead of generating a new one.

Select ‣ Constraint Target

Select bones used as targets for the currently selected bones

---

## Selecting Bones¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/selecting.html

**Contents:**
- Selecting Bones¶
- Selecting Bone Joints¶
  - Inverse Selection¶
  - Selecting Connected Bone Joints¶
- Selecting Bones¶
  - Deselecting Connected Bones¶
- Select Mirror¶
- More/Less¶
- Select Linked¶
- Select Similar¶

You can select and edit bones of armatures in Edit Mode and in Pose Mode. Here, we will see how to select bones in Edit Mode. Selecting bones in Pose Mode is similar to selecting in Edit Mode with a few specific differences that will be detailed in the posing part.

Similar to vertex/edge selection in meshes, there are two ways to select whole bones in Edit Mode:

Directly, by selecting the bone’s body.

Selecting both of its joints (root and tip).

This is an important point to understand, because selecting bones’ joints only might lead to non-obvious behavior, with respect to which bone you actually select.

Note that unlike the mesh display type, the armature display type has no effect on selection behavior. In other words, you can select a bone’s joint or body the same way regardless of the bone visualization chosen.

To select bones’ joints you have the standard selection methods.

As stated above, you have to remember that these selection tools are for bones’ joints only, not the bones’ bodies.

For example, the Inverse selection option Ctrl-I inverts the selection of bones’ joints, not of bones (see Inverse selection).

Remember that a bone is selected only if both its joints are selected. So, when the selection status of bones’ joints is inverted, a new set of bones is selected.

The result of the inverse selection Ctrl-I: The bones joints selection has been inverted, and not the bones selection.¶

Another example is: when you select the root of a bone connected to its parent, you also implicitly select the tip of its parent (and vice versa).

Remember that when selecting bones’ joints, the tip of the parent bone is the “same thing” as the root of its children bones.

By clicking on a bone’s body, you will select it (and hence you will implicitly select its root and tip).

Using Shift-click, you can add to/remove from the selection.

You also have some advanced selection options, based on their relations.

Selects the path from the active bone to the bone under the mouse.

There is a subtlety regarding connected bones.

When you have several connected bones selected, if you deselect one bone, its tip will be deselected, but not its root, if it is also the tip of another selected bone.

To understand this, look at Fig. Bone deselection in a selected chain..

After Shift-clicking “Bone.003”:

“Bone.003” ‘s tip (which is same as “Bone.004” ‘s root) is deselected.

“Bone” is “Bone.003” ‘s parent. Therefore, “Bone.003” ‘s root is the same as the tip of “Bone”. Since “Bone” is still selected, its tip is selected. Thus the root of “Bone.003” remains selected.

Select ‣ Select Mirror

Flip the selection from one side to another.

Expand the current selection to the connected bones.

Contrast the selection, deselect bones at the boundaries of each selection region.

Select ‣ Select Linked

Selects all the bones in the chain which the active (last selected) bone belongs to.

Selects all bones connected to the active bone even if the branch off from the current bone.

A single selected bone.¶

Its whole chain selected with Linked.¶

Select ‣ Select Similar

Extends the selection to all hierarchical descendant bones.

Extends the selection to all direct child bones.

Selects bones that have the same parent as the active bone.

Selects bones with a similar bone length under the specified Threshold.

Select bones aligned on the Y axis (along the bone’s length).

Select bones with matching name prefix (separated by .).

Select bones with matching name suffix (separated by .).

Select bones that share one or more bone collections with the active bone.

Select bones that have the same color as the active bone.

Select bones using the same shape object (in Pose Mode).

Pose & Armature Edit Modes

Select ‣ Select Pattern…

Select bones by names, see Object Select Pattern for details.

You can deselect the active bone and select its immediate parent or one of its children.

Similar to Parent/Child but it keeps the active bone in the selection.

---

## Selection Sets¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/properties/selection_sets.html

**Contents:**
- Selection Sets¶

Armature ‣ Selection Sets

Selection Sets are a feature that allows the definition of sets of bones for easy selection while animating. The sets can be created in local and linked armature overrides.

A List View listing all selection sets for the selected armature. Here, selection sets can be renamed by double clicking on the name.

To the right of the name is a check box to include that selection set when copying to the clipboard.

Removes all selection sets from the list.

Removes the selected bones from all selection sets.

Copies the selected set to Blender’s clipboard.

Pastes a selection set from Blender’s clipboard.

Assigns the selected bones to the active selection set.

Removes the selected bones to the active selection set.

Selects all the bones in the active selection set.

Deselects all the bones in the active selection set.

---

## Separate Bones¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/separate_bones.html

**Contents:**
- Separate Bones¶

Armature ‣ Separate Bones

You can, as with meshes, separate the selected bones in a new armature object Armature ‣ Separate, Ctrl-Alt-P and of course, in Object Mode, you can join all selected armatures in one Object ‣ Join Objects, Ctrl-J.

---

## Shape Keys Panel¶

**URL:** https://docs.blender.org/manual/en/latest/animation/shape_keys/shape_keys_panel.html

**Contents:**
- Shape Keys Panel¶
- Relative Shape Keys¶
- Absolute Shape Keys¶

Object Data ‣ Shape Keys

The Shape Keys panel is used to create, organize, and manage shape keys. It presents a tree view where shape keys can be reordered by click-dragging.

In Relative mode: Value is the current influence of the shape key used for blending between the shape (value=1.0) and its reference key (value=0.0). The reference key is usually the Basis shape. The weight of the blend can be extrapolated above 1.0 and below 0.0.

In Absolute mode: Value is the Evaluation Time at which the shape will have maximum influence.

If unchecked, the shape key will not be taken into consideration when mixing the shape key stack into the result visible in the 3D Viewport.

Shape keys can be locked to protect them from accidental modification due to inadvertently selecting the wrong key for editing in the list. Most common sculpt and edit mode operators and tools that move vertices abort with an error if the active shape key is locked.

Operators that always modify all shape keys in exactly the same way, like Apply Object Transforms, don’t check shape key locks. Neither currently do most edit mode operators that modify topology, because the topology is expected to usually be finalized before shape keys are created.

Add a new shape key with the current deformed shape of the object. This differs from the button of the list, as that one always copies the Basis shape independently of the current mix.

Creates a copy of the active shape key.

Add the vertex positions of selected objects as new shape keys, or update existing shape keys with matching names.

To use, select the object(s) to copy shape data from, then the target object to copy shape data to, and perform the operation.

Creates new shape keys from selected objects while mirroring the vertex positions across the local X axis. This is typically used when creating symmetrical shape keys (for example, generating a Left Smile from a Right Smile shape).

The operation requires the topology of all involved meshes to match.

Updates existing shape keys of the active object with the vertex positions of selected objects that have shape keys with matching names.

To use, select the object(s) to update shape data from, then the target object to update into, and perform the operation.

Similar to Update from Objects, but applies a mirrored update across the local X axis. This is useful for updating symmetrical shape keys when working with mirrored geometry or pose-corrective shapes.

If your mesh is symmetrical, in Object Mode, you can mirror the shape keys on the X axis.

This will not work unless the mesh vertices are perfectly symmetrical. Use the Mesh ‣ Symmetrize tool in Edit Mode.

Same as Mirror Shape Key though it detects the mirrored vertices based on the topology of the mesh. The mesh vertices do not have to be perfectly symmetrical for this action to work.

Makes the selected shape key the new Basis shape key. The vertex positions of the active shape key are applied to the base mesh, and all other shape keys are adjusted relative to this new basis.

This operation is useful when a corrective or edited shape key should become the default shape of the mesh instead of the original basis.

Saves the current visible shape to the mesh data and deletes all Shape Keys.

Removes all Shape Keys and any effect that they had on the mesh.

Set the shape keys to Relative or Absolute. See Relative or Absolute Shape Keys.

Show the active shape in the 3D Viewport without blending. Shape Key Lock gets automatically enabled while the object is in Edit Mode.

If enabled, when entering Edit Mode the active shape key will not take maximum influence as is default. Instead, the current blend of shape keys will be visible and can be edited from that state.

Creates an Attribute in the vertex domain called rest_position which is a copy of the position attribute before shape keys and modifiers are evaluated. Only mesh objects support this option.

Relative Shape Keys options.¶

See Relative or Absolute Shape Keys.

With relative shape keys, the value shown for each shape in the list represents the current weight or influence of that shape in the current Mix.

Set all influence values, or weights, to zero. Useful to quickly guarantee that the result shown in the 3D Viewport is not affected by shapes.

The weight of the blend between the shape key and its reference key (usually the Basis shape).

A value of 0.0 denotes 100% influence of the reference key and 1.0 of the shape key.

Minimum and maximum range for the influence value of the active shape key. Blender can extrapolate results when the Value goes lower than 0.0 or above 1.0.

Limit the active shape key deformation to a vertex group. Useful to break down a complex shape into components by assigning temporary vertex groups to the complex shape and copying the result into new simpler shapes.

Select the shape key to deform from. This is called the Reference Key for that shape.

Rather than storing offsets directly, internally relative keys are stored as snapshots of the mesh shape. The relative deformation offsets are computed by subtracting Reference Key from that snapshot.

Therefore, replacing the Reference Key has the effect of subtracting the difference between the new and old reference from the relative deformation of the current key.

Absolute Shape Keys options.¶

See Relative or Absolute Shape Keys.

With absolute shape keys, the value shown for each shape in the list represents the Evaluation Time at which that shape key will be active.

Absolute shape keys are timed, by order in the list, at a constant interval. This button resets the timing for the keys. Useful if keys were removed or re-ordered.

Controls the interpolation between shape keys.

Linear, Cardinal, Catmull-Rom, B-Spline

Different types of interpolation.¶

The red line represents interpolated values between keys (black dots).

Controls the shape key influence. Scrub to see the effect of the current configuration. Typically, this property is keyed for animation or rigged with a driver.

---

## Shape Key Editor¶

**URL:** https://docs.blender.org/manual/en/latest/editors/dope_sheet/modes/shape_key.html

**Contents:**
- Shape Key Editor¶
- Usage¶

The Shape Key Editor displays the shape keys of the active object and allows you to create and adjust keyframes for their influence values. This editor is a specialized mode of the Dope Sheet, focused specifically on shape key animation.

Each row represents a shape key, and each keyframe marker corresponds to a point where the shape key’s value changes over time. This provides an efficient way to time and refine facial expressions, morph targets, and other mesh deformations driven by shape keys.

Additional shape key properties, such as names, values, and relative settings, can be viewed and edited in the Sidebar.

The Shape Key Editor.¶

Use the Shape Key Editor to keyframe shape key influences over time.

Adjust timing by moving or scaling keyframes directly in the timeline.

Combine with other Dope Sheet modes (such as the Action Editor) for complex character animation workflows.

See also: Shape Key Basics for details on creating and managing shape keys.

---

## Show/Hide¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/editing/show_hide.html

**Contents:**
- Show/Hide¶

Properties ‣ Bone ‣ Viewport Display

You do not have to use bone layers to show/hide some bones. As with objects, vertices or control points, you can use H:

H will hide the selected bone(s).

Shift-H will hide all bones but the selected one(s).

Alt-H will show all hidden bones.

You can also use the Hide checkbox of the Bone tab ‣ Viewport Display panel.

Note that hidden bones are specific to a mode, i.e. you can hide some bones in Edit Mode, they will still be visible in Pose Mode, and vice versa. Hidden bones in Pose Mode are also invisible in Object Mode. And in Edit Mode, the bone to hide must be fully selected, not just its root or tip.

---

## Sidebar¶

**URL:** https://docs.blender.org/manual/en/latest/editors/dope_sheet/sidebar.html

**Contents:**
- Sidebar¶
- Action Panel¶
- Custom Properties¶

Actions with and without a Manual Frame Range in Dope Sheet.¶

When the editor is in Action Editor mode, or in Dope Sheet mode with a channel selected that belongs to an action, this panel allows changing some settings of that action. See Action Properties for details.

Create and manage your own properties to store data in the action’s data block. See the Custom Properties page for more information.

---

## Sidebar¶

**URL:** https://docs.blender.org/manual/en/latest/editors/nla/sidebar.html

**Contents:**
- Sidebar¶
- Edited Action¶
- Strip¶
  - Active Strip¶
    - Animated Influence¶
    - Animated Strip Time¶
  - Action Clip¶
  - Action¶
- Modifiers¶

Sidebar ‣ Edited Action

Edited Action panel.¶

Contains settings for the object’s active action. Only visible if the Action Track is selected.

A data-block menu where you can see, change, and clear the active action. See also the Action Editor’s Action.

The slot within the active action to use.

Determines whether the action will influence the frames before/after its boundaries once it has been pushed down into a strip. (As long as it’s still the active action, Hold is used regardless of the choice.)

The property values at the action’s first keyframe also apply to the earlier frames (if the strip is the first in the track). The values at its last keyframe also apply to the later frames (up to the next strip).

The property values at the action’s last keyframe also apply to the later frames (up to the next strip).

The animated properties return to their default values outside of the strip boundaries.

How to combine the action’s property values with those of the tracks below.

Overwrites the values produced by the lower tracks. If Influence is less than 1, a linear interpolation between the previous and new values is used instead.

Blends the action’s values with those of the lower tracks using a simple calculation. If Influence is less than 1, a linear interpolation between the previous values and these calculated values is used.

\(result = mix(previous, previous (+-×) value, influence)\)

Depending on the type of each property, one of the following methods is automatically chosen:

\(result = previous + value × influence\)

This results in averaging the axis and adding the amount of rotation.

Quaternion math is applied to all four channels of the property at once:

\(result = {previous} × {value} ^ {influence}\)

\(result = previous × (value / default) ^ {influence}\)

\(result = previous + (value - default) × {influence}\)

Since this blending mode uses quaternion multiplication to calculate the Quaternion Rotation properties, it always drives all four channels during playback, and Insert Single Keyframe is forced to insert all four keys. Other types of channels can still be keyed individually.

How much the action contributes to the result of the NLA stack.

When unchecked, the strip will no longer contribute to the animation. It’s shown with a dotted outline to indicate this.

Sidebar ‣ Strip ‣ Active Strip

Contains common strip properties.

The frame where the strip begins. Changing this will move the strip while keeping its duration constant.

The frame where the strip ends. Changing this will also change the Action Clip Frame End, thereby cropping or extending the action. If you instead want to speed it up or slow it down, scale it by using Strip ‣ Transform ‣ Scale or adjusting the Playback Scale setting.

How many frames it takes for the strip’s influence to ramp up at the start and wind down at the end.

Two strips with Auto Blend enabled.¶

Calculates Blend In/Out automatically by looking at the strips in the track above or below that overlap the current strip in time.

Makes the strip play backwards.

Whether to wrap the Animated Strip Time back to the start if it exceeds the Action Clip Frame End.

Lets you manually specify, and animate, how strongly the strip affects the animation. This is an alternative to using the (Auto) Blend In/Out settings above.

To create an influence keyframe, first type a value, then either click Insert Keyframe in its context menu or press I while hovering over it. You can see the keyframes in e.g. the Graph Editor.

Lets you manually specify, and animate, the frame at which the underlying action is sampled.

Although the setting is called Strip Time, its value is a frame number inside the action, not inside the strip. If you have an action going from frame 1 to frame 50 that’s referenced by a strip going from frame 101 to 150, you’d set the Strip Time to 1 to see the first keyframe, not 101.

In combination with Cyclic Strip Time, this lets you play the action’s keyframes multiple times in a single strip. As an example, say that the action’s keyframes are between frames 1 and 50. If you animate the strip time to instead go from 1 to 100, the keyframes will play twice (at twice the speed).

In practice, however, it’s easier to use the Repeat setting described below.

Sidebar region ‣ Strip ‣ Action Clip

Contains properties specific to Action strips.

The action referenced by the strip.

The slot within the action to use.

How much of the action to use. By adjusting these, you can crop or extend the action (and the strip, as its Frame End will change accordingly). If you extend the action, F-Curve Extrapolation will kick in.

One case where these settings can be useful is in cyclic animation where the first and last keyframes of the action have the same value (meaning this value applies for two frames when the animation restarts). By reducing the Frame End, you can exclude the last keyframe and have the value apply for only one frame instead.

Automatically sets Frame Start/End to the action’s first/last keyframe when exiting Tweak Mode.

Sets Frame Start/End to the action’s first/last keyframe.

Makes the animation play more quickly (scale < 1) or slowly (scale > 1) than the original action.

Makes the action play multiple times.

Sidebar region ‣ Strip ‣ Action

See Action Properties.

Sidebar region ‣ Modifiers

Strip modifiers let you make non-destructive changes to all the curves inside the strip’s action.

See F-Curve Modifiers.

---

## Slider Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/constraints/types/slider.html

**Contents:**
- Slider Constraint¶
- Options¶

Physics ‣ Rigid Body Constraint

The Slider constraint allows relative translation along the X axis of the constraint object, but permits no relative rotation, or relative translation along other axes.

Enables/disables limit translation around X axis.

Lower limit of X axis translation.

Upper limit of X axis translation.

---

## Spline IK Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/tracking/spline_ik.html

**Contents:**
- Spline IK Constraint¶
- Options¶
  - Fitting¶
  - Chain Scaling¶
- Example¶

The Spline IK constraint fits a chain of bones to the shape of a Curve. It’s particularly well suited for rigging flexible body parts such as tails, tentacles, and spines, as well as inorganic objects such as ropes.

The IK constraints are special in that they modify multiple bones. For this reason, they ignore their position in the stack and always run after all other constraints on the affected bones. To apply constraints after IK, it is necessary to first copy the final transformation to a new bone chain, e.g. using Copy Transforms.

Spline IK constraint.¶

The Curve whose shape to match.

How strongly the constraint affects the bone chain.

The number of bones affected by the constraint, starting with the owner bone and walking up its chain of ancestors. A value of 1 will only fit the bone itself, a value of 2 will fit the bone and its parent, and so on.

When disabled, each bone will cover a distance along the curve relative to its rest length. When enabled, each bone will cover the same distance regardless of its rest length.

When disabled, the bone chain will move to match the position of the curve. When enabled, the bone chain will stay at its original starting location and mimic the shape of the curve from there.

Whether to use the radii of the curve control points as additional X and Z scaling factors for the bones.

How to stretch the bones along the length of the curve.

Reset the bones to their rest length.

Stretch the bones to cover the entire length of the curve.

Keep the bones’ original length (including their Pose Mode scale).

How to scale the bones along the normals of the curve (or in other words, how to determine the thickness of the bones).

Reset the bones’ X and Z scales to 1.

Keep the bones’ original X and Z scales from Pose Mode.

Set the X and Z scales to the inverse of the Y scale.

Similar to the Stretch To constraint.

Apply Inverse Scale or Volume Preservation on top of the Pose Mode bone scales, like in the Stretch To constraint.

This subject is seen in-depth in the Armature Posing section.

---

## Spline IK¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/bone_constraints/inverse_kinematics/spline_ik.html

**Contents:**
- Spline IK¶
- Basic Setup¶
- Settings and Controls¶
  - Roll Control¶
  - Offset Controls¶
  - Length Control¶
  - Thickness Controls¶
- Tips for Nice Setups¶

Spline IK is a constraint which aligns a chain of bones along a curve. By leveraging the ease and flexibility of achieving aesthetically pleasing shapes offered by curves and the predictability and well-integrated control offered by bones, Spline IK is an invaluable tool in the riggers’ toolbox. It is particularly well suited for rigging flexible body parts such as tails, tentacles, and spines, as well as inorganic items such as ropes.

Full description of the settings for the spline IK can be found on the Spline IK page.

The Spline IK Constraint is not strictly an Inverse Kinematics method (i.e. IK Constraint), but rather a Forward Kinematics method (i.e. normal bone posing). However, it still shares some characteristics of the IK Constraint, such as operating on multiple bones, not being usable for Objects, and being evaluated after all other constraints have been evaluated. It should be noted that if a Standard IK chain and a Spline IK chain both affect a bone at the same time the Standard IK chain takes priority. Such setups are best avoided though, since the results may be difficult to control.

To setup Spline IK, it is necessary to have a chain of connected bones and a curve to constrain these bones to:

With the last bone in the chain selected, add a Spline IK Constraint from the Bone Constraints tab in the Properties.

Set the Chain Length setting to the number of bones in the chain (starting from and including the selected bone) that should be influenced by the curve.

Finally, set the Target field to the curve that should control the curve.

Congratulations, the bone chain is now controlled by the curve.

For the precise list of options, see Spline IK constraint. This section is intended to introduce the workflow.

To control the Roll of the Spline IK chain, the standard methods of rotating the bones in the chain along their local Y axes still apply. For example, start at the farthest bone and simply rotate the bones in the chain around their local Y axes to adjust the roll of the chain from that point onward.

Applying Copy Rotation constraints on the bones also works.

There are a couple of limitations to consider:

Bones do not inherit a curve’s tilt value to control their roll.

There is no way of automatically creating a twisting effect where a dampened rotation is inherited up the chain. Consider using Bendy Bones instead.

The entire bone chain can be made to follow the shape of the curve while still being able to be placed at an arbitrary point in 3D space when the Chain Offset option is enabled. By default, this option is not enabled, and the bones will be made to follow the curve in its untransformed position.

The Y Scale Mode setting can be used to choose the way bones are scaled length-wise. The available options allow stretching the bone chain to fit the curve, using the pre-IK scaling, or doing neither. In addition, the scale of the curve Object affects the result.

The thickness of the bones in the chain is controlled using the constraint’s XZ Scale Mode setting. This setting determines the method used for determining the scaling on the X and Z axes of each bone in the chain.

The available modes are:

This option keeps the X and Z scaling factors as 1.0.

The X and Z scaling factors are taken as the inverse of the Y scaling factor (length of the bone), maintaining the ‘volume’ of the bone.

This options just uses the X and Z scaling factors the bone would have after being evaluated in the standard way.

In addition to these modes, there is an option, Use Curve Radius. When this option is enabled, the average radius of the radii of the points on the curve where the joints of each bone are placed, are used to derive X and Z scaling factors. This allows the scaling effects, determined using the modes above, to be tweaked as necessary for artistic control.

For optimal deformations, it is recommended that the bones are roughly the same length, and that they are not too long, to facilitate a better fit to the curve. Also, bones should ideally be created in a way that follows the shape of the curve in its ‘rest pose’ shape, to minimize the problems in areas where the curve has sharp bends which may be especially noticeable when stretching is disabled.

For control of the curve, it is recommended that hooks (in particular, Bone Hooks) are used to control the control points of the curve, with one hook per control point. In general, only a few control points should be needed for the curve (e.g. one for every 3-5 bones offers decent control).

The type of curve used does not really matter, as long as a path can be extracted from it that could also be used by the Follow Path Constraint. This really depends on the level of control required from the hooks.

---

## Split¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/split.html

**Contents:**
- Split¶

The Split operator disconnects selected bones from the rest of the armature, creating a new, unconnected bone chain.

This is useful for restructuring rigs, separating limbs, or preparing bone chains to be transformed independently.

This operator only affects bone connectivity; the bones remain within the same armature object. To move the split bone chain to a separate object, use Separate Bones.

---

## Stretch To Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/tracking/stretch_to.html

**Contents:**
- Stretch To Constraint¶
- Options¶
- Example¶

The Stretch To constraint makes an object or bone point at, and scale towards, a target. Unlike the other “track” constraints, it can only do this using the local Y axis, making it mainly useful for bones.

The constraint can also perform “volume preservation,” making the owner thinner when the target moves away and thicker when it comes closer. This is useful for stretching and squashing of stylized characters, for example. However, because it simply adjusts the X and Z scales according to the Y scale, it works for any type of object, not just meshes.

Stretch To constraint.¶

The object or bone to stretch towards.

The rest distance between owner and target, i.e. the distance at which there is no stretching of the owner.

Sets the Original Length to the current distance between owner and target.

Exponent that either exaggerates (> 1) or reduces (< 1) the thickness change caused by volume preservation. Setting this to 0 is the same as setting Maintain Volume to None.

Lower and upper limits for the thickness factor applied by volume preservation.

If Maintain Volume is set to XZ, the X and Z factors are each bound to the square root of these limits. For example, if Volume Max is set to 4, both the X and Z scale can grow to no more than twice their original value.

If Maintain Volume is set to X or Z, the factor for the chosen axis is bound to these limits. In the above example, the axis could grow to no more than 4 times its original value (while the other axis would not grow or shrink at all).

A higher value will slow down the thickness change as it approaches the limits. This prevents an abrupt stop once the limits are reached.

Whether to make the owner thicker/thinner as it contracts/stretches to meet the target.

Scale along both the X and Z axes.

Scale along the X axis only.

Scale along the Z axis only.

Don’t change the X and Z scales.

Maintain Volume Constraint

How the owner should be rotated to track the target with its Y axis.

Tries to keep the local X axis close to its original orientation.

Tries to keep the local Z axis close to its original orientation.

Uses a swing rotation, much like the Damped Track Constraint.

How strongly the constraint affects the owner.

---

## Strips¶

**URL:** https://docs.blender.org/manual/en/latest/editors/nla/strips.html

**Contents:**
- Strips¶
- Action Strips¶
- Transition Strips¶
- Sound Strips¶
- Meta Strips¶

A strip tells the animation when something happens and for how long. There are a few different types which are described below.

An action strip plays the keyframes inside an action. You can create one using Add ‣ Action. Another way is to click Push Down Action in the NLA’s Action Track – this will create a strip based on the object’s active action.

Multiple strips can reference the same action, so that you can potentially change multiple parts of the animation by editing a single set of keyframes.

A strip can be shorter than its underlying action, be it through cropping, speeding up, or both. It can also be longer than its underlying action, be it through extending, slowing down, or both. See the Sidebar for details.

A transition strip interpolates between two neighboring action strips. Select them and click Add ‣ Transition.

These strips control when a Speaker Objects starts to playback the audio. Playback continues the length of audio file and does not take into account the length of the sound strip.

A meta strip groups other strips together, letting you move, scale, and copy them as one combined unit.

---

## Subdivide¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/subdivide.html

**Contents:**
- Subdivide¶

You can subdivide bones, to get two or more bones where there was just one bone. The tool will subdivide all selected bones, preserving the existing relationships: the bones created from a subdivision always form a connected chain of bones.

To create an arbitrary number of bones from each selected bone in the Subdivide Multi Adjust Last Operation panel.

Specifies the number of cuts. As in mesh editing, if you set n cuts, you will get n + 1 bones for each selected bone.

An armature with one selected bone, just before multi-subdivision.¶

The selected bone has been “cut” two times, giving three sub-bones.¶

---

## Switch Direction¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/switch_direction.html

**Contents:**
- Switch Direction¶

Armature ‣ Switch Direction

This tool allows you to switch the direction of the selected bones (i.e. their root will become their tip, and vice versa).

Switching the direction of a bone will generally break the chain(s) it belongs to. However, if you switch a whole (part of a) chain, the switched bones will still be parented/connected, but in “reversed order”. See the Fig. Switching example..

An armature with one selected bone, and one selected chain of three bones, just before switching.¶

The selected bones have been switched. Bone.005 is no more connected nor parented to anything. The chain of switched bones still exists, but reversed (now Bone.002 is its root, and Bone is its tip). Bone.003 is now a free bone.¶

---

## Symmetrize¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/symmetrize.html

**Contents:**
- Symmetrize¶

Armature ‣ Symmetrize

The Symmetrize operator mirrors selected bones along the X axis using Blender’s bone naming convention for symmetrical armatures. Bones can be mirrored from left to right or right to left, depending on the selection.

If matching bones are selected on both sides, mirroring happens from right to left.

Bones with opposite names that don’t exist are created, and existing ones are overwritten.

Bones that cannot be determined as left or right are ignored.

Symmetrized bone and constraint properties are adjusted to mirror their behaviors. For bones with Action Constraints, keyframes are added to the target Action, ensuring symmetrical motion when the Action is activated.

Bone or constraint drivers are not created or affected during symmetrization.

Bone collection assignments are also symmetrized. Collections that follow the naming convention are mirrored. If a collection does not exist, it is created and parented to the same collection as the original.

Blender does not prevent left bones from being assigned to right collections. During symmetrization, the resulting right bone will be assigned to the left collection.

---

## Timeline¶

**URL:** https://docs.blender.org/manual/en/latest/editors/timeline.html

**Contents:**
- Timeline¶
- Main View¶
  - Adjusting the View¶
  - Frame Range¶
  - Keyframes¶
  - Markers¶
- Header¶
  - View Menu¶
  - Marker Menu¶

The Timeline editor is used to jump to different frames, manipulate keyframes, and control animation playback.

The X axis represents time, with the numbers 0/50/100/… being frame numbers. The blue line is the Playhead indicating the current frame, and the diamond shapes are Keyframes, points where you specified a certain value for a certain property at a certain time.

Panning is done by dragging MMB.

Zooming is done by dragging Ctrl-MMB, rolling the mouse Wheel, or pressing NumpadMinus/NumpadPlus.

You can also use the scrollbars located at the bottom and the right of the editor.

The Frame Range determines the length of the scene’s animation. By default, it’s set to start at frame 1 and end at frame 250. You can change this using the Start/End inputs in the Timeline header, or in the Output Properties.

By default, the timeline only shows keyframes for selected items. You can make it show all keyframes by unchecking View ‣ Only Show Selected.

You can click a keyframe to select it (and deselect all others), or click it while holding Shift to add it to the selection (or remove it if it was already selected). You can also drag a box to select multiple keyframes in one go.

To move the selected keyframes, simply drag one of them. Alternatively, you can press G, move the mouse, and click LMB to confirm (or RMB to cancel). You can also press S to scale the keyframes in relation to the Playhead.

See the Markers page for more information.

Popovers for Playback and Keying; transport controls; and frame controls¶

Displays a pop-up panel to alter properties of the last completed operation. See Adjust Last Operation.

Show or hide the Channels region (the tree of objects and animatable properties on the left).

Pans and zooms the view so that all keyframes are visible.

Reset the horizontal view to the current scene frame range, taking the preview range into account if it is active.

Centers the Timeline to the Playhead.

Shows the Markers region (if any markers are defined). When disabled, the Marker Menu is also hidden and marker operators are not available in this editor.

Shows the time on the X axis and the Playhead as timestamps instead of frame numbers. A timestamp such as 01:03+02 means “1 minute, 3 seconds, 2 frames.”

Synchronizes the horizontal panning and scale of the editor with other time-based editors that also have this option enabled. That way, they always show the same section of time.

Only show keyframes related to the selected items. This could be objects, bones, nodes, and so on.

If this option is enabled, the Timeline may not show all material keyframes of the selected objects. Instead, it only shows the keyframes belonging to the selected nodes in the Shader Editor.

Only show curves and drivers that are disabled or have errors. Useful for debugging.

Which simulation caches to show on the timeline. See Cache for more information.

Area controls. See the user interface documentation for more information.

Markers are used to denote frames with key points or significant events within an animation. Like in most animation editors, they’re shown at the bottom of the Timeline.

Markers in an animation editor.¶

For descriptions of the different marker tools, see Editing Markers.

Properties for how animations are played. See Playback for more information.

Properties for how keyframes are added. See Keying for more information.

Options for automatically adding keyframes. See Auto Keying for more information.

These buttons are used to control playback. See Transport Controls for more information.

Used to set the current frame and the start/end frame. See Frame Controls for more information.

---

## Tips¶

**URL:** https://docs.blender.org/manual/en/latest/physics/rigid_body/tips.html

**Contents:**
- Tips¶
- Animation¶
- Simulation Stability¶
- Combining Rigid Bodies with Other Simulations¶
- Scaling Rigid Bodies¶

As with all physics-enabled objects, pay close attention to the Animated checkbox in the Rigid Body panel of the Physics tab in the Properties. A common mistake is to use keyframe animation on a Passive physics object without checking the Animated box. The object will move, but the physics engine will behave as if the Passive is still in its starting place, leading to disappointment.

The most common trick is to Keyframe animate the location or rotation of an Active physics object as well as the Animated checkbox. When the curve on the Animated property switches to disabled, the physics engine takes over using the object’s last known location, rotation and velocities.

Animating the strengths of various other parameters (a Motor’s Target Velocity, a Hinge’s limits, etc.) can be used to accomplish a wide variety of interesting results.

Enabling a constraint during the physics simulation often has dramatic results as the physics engine tries to bring into alignment two objects which are often dramatically out of alignment. It is very common for the affected objects to build up enough kinetic energy to bounce themselves out of camera.

Rigid body dynamics can be baked to normal keyframes with Bake To Keyframes in the Object ‣ Rigid Body menu.

The simplest way of improving simulation stability is to increase the steps per second. However, care has to be taken since making too many steps can cause problems and make the simulation even less stable (if you need more than 1000 steps, you should look at other ways to improve stability).

Increasing the number of solver iterations helps making constraints stronger and also improves object stacking stability.

It is best to avoid small objects, as they are currently unstable. Ideally, objects should be at least 20 cm in diameter. If it is still necessary, setting the collision margin to 0, while generally not recommended, can help making small object behave more naturally.

When objects are small and/or move very fast, they can pass through each other. Besides what is mentioned above it’s also good to avoid using mesh shapes in this case. Mesh shapes consist of individual triangles and therefore do not really have any thickness, so objects can pass through more easily. You can give them some thickness by increasing the collision margin.

Since the rigid body simulation is part of the animation system, it can influence other simulations just like the animation system can.

In order for this to work, the rigid body object needs to have a Collision Modifier. Simply click on Collision in the Physics tab.

Rigid body objects can be scaled, also during the simulation. This work well in most cases, but can sometimes cause problems.

If dynamic scaling is not needed, rigid body objects should have the scale applied by using the Apply Scale tool Ctrl-A.

---

## Tool Settings¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/posing/tool_settings.html

**Contents:**
- Tool Settings¶
- Pose Options¶
  - Auto IK¶
  - X-Axis Mirror¶
  - Relative Mirror¶
- Known Limitations¶

Sidebar ‣ Tool ‣ Pose Options ‣ Auto IK

Automatic IK is a tool for quick posing, when enabled, translating a bone will activate inverse kinematics and rotate the parent bone, and the parent’s parent, and so on, to follow the selected bone. The IK chain can only extend from a child to a parent bone if the child is connected to it.

While moving bones, the length of the chain (the number of affected bones) can be increased or decreased using keyboard hotkeys. Pressing PageUp will increase in chain length by one and PageDown decreases the length by one. The chain length can also be controlled with WheelUp or WheelDown.

The initial chain length is 0, which effectively means follow the connections to parent bones as far as possible, with no length limit. So pressing increasing the chain length the first time sets the length to 1 (move only the selected bone), and at this point, decreasing the length point sets it back to 0 (unlimited) again. Thus, you have to increase the chain length more than once from the initial state to set a finite chain length greater than 1.

This is a more limited feature than using an IK constraint, which can be configured, but it can be useful for quick posing.

Sidebar ‣ Tool ‣ Options ‣ X-Axis Mirror

This option enables automatic mirroring of editing actions along the X axis. You can enable this option in the Tool tab ‣ Options panel, while the armature is selected in Edit Mode. When you have pairs of bones of the same name with just a different “side suffix” (e.g. “.R”/”.L”, or “_right”/”_left” …), once this option is enabled, each time you transform (move, rotate, scale…) a bone, its “other side” counterpart will be transformed accordingly, through a symmetry along the armature local X axis. As most rigs have at least one axis of symmetry (animals, humans, …), it is an easy way to keep the model symmetrical.

Sidebar ‣ Tool ‣ Options ‣ Relative Mirror

Accounts for any relative transformations when using X-Axis Mirror.

Relative Mirror is not supported with Auto IK enabled.

---

## Tracks¶

**URL:** https://docs.blender.org/manual/en/latest/editors/nla/tracks.html

**Contents:**
- Tracks¶
- Action Track¶

A track plays one or more actions in sequence. You can create multiple tracks to play several actions at the same time.

NLA Tracks and Strips.¶

The track region has the following properties:

When unchecked, mutes all the tracks except the Action Track.

Double-click to change. (Not possible for the Action Track, as this one simply displays the name of the action.)

When unchecked, the track stops contributing to the animation. Its strips receive a dotted outline to indicate this. Note that you can also mute individual strips.

Prevents changes from being made to this track. This is useful, for example, if you want to move the strips in all the tracks except for a few.

Mutes all other tracks, including the Action Track, so that only this track contributes to the animation. This is useful for inspecting the track without any distractions from others.

The topmost track with the orange header holds the action that’s being edited. Normally this is the object’s active action, but if you select a strip and press Tab to enter Tweak Mode, you can temporarily make that one editable instead – in the Action Editor or the Graph Editor, for example.

The Action Track has one of the following buttons:

Not available in Tweak Mode. Creates a new track below the Action Track and moves the active action into it as a strip, leaving the Action Track empty. (If you create a keyframe after this, Blender will automatically create a new active action to hold it.)

Push Down Action button.¶

Only available in Tweak Mode. When unchecked, the action’s keyframes are shown at their original time points, rather than their new time points resulting from the strip being moved and scaled.

Strip at its original time point.¶

Strip moved. Notice that the keyframes are now shown to start at frame 20, which is also how the animation will behave. Within the action, however, they still start at frame 1.¶

After unchecking the Pin icon, the keyframes are shown at their original time points.¶

---

## Track¶

**URL:** https://docs.blender.org/manual/en/latest/editors/nla/editing/track.html

**Contents:**
- Track¶
- Add¶
- Add Above Selected¶
- Delete Tracks¶
- Move¶
- Remove Empty Animation Data¶

Adds a new track below the Action Track.

Track ‣ Add Above Selected

Adds a new track above each selected one.

Deletes the selected tracks and the strips they contain.

When using the keyboard shortcuts, make sure the mouse cursor is hovering over the track region, as otherwise, Blender will only delete the selected strips.

Moves the selected tracks to the top.

Moves the selected tracks up by one.

Moves the selected tracks down by one.

Moves the selected tracks to the bottom.

When using the keyboard shortcuts, make sure the mouse cursor is hovering over the track region, as otherwise, Blender will move the selected strips to different tracks (rather than moving the tracks).

Track ‣ Remove Empty Animation Data

Removes objects that don’t have drivers, NLA tracks, or an active action from the NLA editor to reduce clutter. This essentially does the opposite of Add ‣ Selected Objects.

---

## Track To Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/tracking/track_to.html

**Contents:**
- Track To Constraint¶
- Options¶
- Example¶

The Track To constraint makes an object or bone point towards a certain target, then roll to make a certain local axis point upwards. It’s typically called “Look At” or “Aim” in other 3D software.

If the constraint owner is almost directly above the target, the roll around the tracking axis will become unstable. For this scenario, it’s recommended to use the Damped Track Constraint instead.

Track To constraint.¶

The object or bone to point towards.

The local axis of the owner that should point at the target. For bones, this should typically be Y.

A negative axis will make the owner point away from the target instead.

The local axis of the owner that should point upwards in the world.

The Track Axis and the Up axis must be different. If they are the same, the constraint will stop working and its icon will turn red.

Align the owner’s Up axis as closely as possible to the target’s Z axis instead of the global one.

The spaces for evaluating the target and owner transforms.

How strongly the constraint affects the owner.

---

## Transformation Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/transform/transformation.html

**Contents:**
- Transformation Constraint¶
- Options¶
  - Map From¶
  - Map To¶
- Example¶

This constraint is more complex and versatile than the other “transform” constraints. It lets you set the location, rotation or scale of an object/bone based on the location, rotation or scale of another, mixing and matching axes as you see fit. An example could be to set a gear’s X rotation based on the Y coordinate of a rail next to it.

The constraint works with input and output value ranges, one for each axis. It first clamps the input value to the Map From range, then offsets and scales it to the corresponding Map To range. This lets you, say, map a Y coordinate in the range (-3m, 3m) to an X rotation in the range (0, 180°).

Transformation constraint.¶

The object or bone to retrieve the transformation from.

By default, the input and output values are clamped to the Min/Max values. When you enable Extrapolate, they’re allowed to go beyond these limits. This is illustrated with the graphs below, where the X axis represents the input (Map From set to Min = 1 and Max = 4) and the Y axis represents the output (Map To set to Min = 1 and Max = 2).

Extrapolate disabled: the output values are limited to the Map To range.¶

Extrapolate enabled: the output values can extend beyond the limits.¶

The spaces for retrieving the transformation from the target and for applying it to the owner.

How strongly the constraint affects the owner.

The transformation to read from the Target.

The type of transformation to read.

The type of rotation to use, including different Euler orders, Quaternion, and other Rotation Channel Modes. Defaults to using the Euler order of the constraint owner.

In the Quaternion mode, the channels are converted to weighted angles in the same way as the swing angles of the Swing and X/Y/Z Twist modes.

The input value range for each axis.

The transformation to apply to the owner.

The type of transformation to apply.

Which Euler order to use. Defaults to the order of the constraint owner.

For each of the three output axes, lets you choose the input axis that it should take its value from. You can select the same input axis multiple times.

The output value range for each axis.

Specifies how the result of the constraint is combined with the existing transformation. The set of available choices varies based on the type of transformation.

The result of the constraint replaces the existing transformation.

The new values are multiplied with the existing axis values.

The new values are added to the existing axis values.

The new rotation is added before the existing rotation, as if it were applied to a parent of the constraint owner.

The new rotation is added after the existing rotation, as if it were applied to a child of the constraint owner.

For historical reasons, the Mix mode defaults to Add for location and rotation, and Replace for scale.

When using the rotation of the target as input, whatever the real values are, the constraint will always “take them back” into the (-180 to 180) range. E.g. if the target has a rotation of 420 degrees around its X axis, the values used as X input by the constraint will be:

\(((420 + 180) modulo 360) - 180 = 60 - 180 = -120\)

As such, this constraint is not really suited for transforming an object based on a gear’s rotation. Rotating a gear based on an object’s transformation works fine, however.

Similarly, when using the scale transform properties of the target as input, whatever the real values are, the constraint will always take their absolute values (i.e. invert negative ones).

When a Min value is higher than its corresponding Max one, both are considered equal to the Max one. This means you cannot create “reversed” mappings.

In the following example, we add a constraint to a gear that sets its X rotation based on the Y position of a rail:

Before moving the rail.¶

After moving the rail.¶

By default, the gear will stop rotating if the rail goes outside the (-3m, 3m) range. You can enable Extrapolate to change this.

---

## Transform¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/properties/transform.html

**Contents:**
- Transform¶

Edit Mode and Pose Mode

When in Edit Mode you can use this panel to control position and roll of individual bones. Whereas in Pose Mode you can only set location for the main bone, and you can now set rotation and scale.

In addition, in Pose Mode it is possible to restrict changes in position, rotation and scale by axis on each bone in the armature.

Location of head end of the bone.

Location of tail end of the bone.

Bone rotation around head-tail axis.

The distance from the bone’s head to it’s tail. Changing the length moves the tail end.

Bone is not able to be transformed when in Edit Mode.

---

## Transform¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/editing/transform.html

**Contents:**
- Transform¶
- Scale Radius¶
- Scale Envelope Distance¶
- Align Bones¶

The Transform panel for armatures in Edit Mode.¶

We will not detail here the various transformations of bones, nor things like axis locking, pivot points, and so on, as they are common to most object editing, and already described in the mesh section. The same goes for mirroring, as it is nearly the same as with mesh editing. Just keep in mind that bones’ roots and tips behave more or less like meshes’ vertices, and bones themselves act like edges in a mesh.

As you know, bones can have two types of relationships: They can be parented, and in addition connected. Parented bones behave in Edit Mode exactly as if they had no relations. They can be moved, rotated, scaled, etc. without affecting their descendants. However, connected bones must always have parent’s tips connected to child’s roots, so by transforming a bone, you will affect all its connected parent/children/siblings.

While with other transform tools, the “local axes” means the object’s axes, here they are the bone’s own axes (when you lock to a local axis, by pressing the relevant key twice, the constraint is applied along the selected bone’s local axis, not the armature object’s axis).

Finally, you can edit in the Transform panel in the Sidebar region the positions and radius of both joints of the active selected bone, as well as its roll rotation.

Armature ‣ Transform ‣ Scale Radius

You can alter the radius that a bone has by selecting the head, body or tail of a bone, and then press Alt-S and move the mouse left or right. If the body is selected the mean radius will be scaled. And as usual, with connected bones, you scale at the same time the radius of the parent’s tip and of the children’s roots.

You can also alter the bone radius by selecting the tail or head of the bone you wish to alter, then navigate to Properties ‣ Bone ‣ Deform ‣ Radius Section and entering new values for the Tail and Head number fields.

A single selected bone in Octahedron visualization.¶

A single selected bone in Envelope visualization.¶

After Scaled Radius. Its length remains the same, but its joints’ radius are bigger.¶

Note that, when you resize a bone (either by directly scaling it, or by moving one of its joints), Blender automatically adjusts the end-radii of its envelope proportionally to the size of the modification. Therefore, it is advisable to place all the bones first, and only then edit their properties.

Edit Mode and Pose Mode

Armature ‣ Transform ‣ Scale Envelope Distance

You can alter the size of the Bone Envelope volume by clicking on the body of the bone you want to alter, Ctrl-Alt-S then drag your mouse left or right and the Bone Envelope volume will alter accordingly.

You can also alter the Bone Envelope volume by selecting the Bone you wish to alter and then navigate to Properties ‣ Bone ‣ Deform ‣ Envelope ‣ Distance then enter a new value into it.

Altering the Bone Envelope volume does not alter the size of the bone just the range within which it can influence vertices of child objects.

A single bone selected in Envelope visualization.¶

Its envelope distance scaled.¶

A single “default size” bone selected in B-Bone visualization.¶

Its envelope distance scaled.¶

The same armature in Object Mode and B-Bone visualization, with Bone.004’s size scaled up.¶

Armature ‣ Transform ‣ Align Bones

Rotates the selected bones to achieve the same orientation as the active one.

---

## Transform Cache Constraint¶

**URL:** https://docs.blender.org/manual/en/latest/animation/constraints/transform/transform_cache.html

**Contents:**
- Transform Cache Constraint¶
- Options¶

The Transform Cache Constraint streams an animation from an Alembic or USD file. For example, it can apply a baked rigid body simulation to an object.

The constraint is automatically added when importing such a file. However, it only applies to transforms (location/rotation/scale of the whole object). For animations that cause deformation, the Mesh Sequence Cache Modifier is used instead.

Transform Cache Constraint.¶

Data-block menu to select the Alembic or USD file.

Path to the Alembic or USD file.

Whether or not the cache is separated in a series of files.

Whether to use a custom frame for looking up data in the cache file, instead of using the current scene frame.

The Frame value is the time to use for looking up the data in the cache file, or to determine which to use in a file sequence.

Subtracted from the current frame to use for looking up the data in the cache file, or to determine which file to use in a file sequence.

Value by which to enlarge or shrink the object with respect to the world’s origin.

The name of the Alembic attribute used for generating motion blur data; by default, this is .velocities which is standard for most Alembic files.

The Velocity Attribute option is currently for Alembic files only.

Defines how the velocity vectors are interpreted with regard to time.

The velocity unit was encoded in frames and does not need to be scaled by scene FPS.

The velocity unit was encoded in seconds and needs to be scaled by the scene FPS (1 / FPS).

The Velocity Unit option is currently for Alembic files only.

The path to the Alembic or USD object inside the archive or stage.

How strongly the constraint affects the object.

---

## Troubleshooting¶

**URL:** https://docs.blender.org/manual/en/latest/animation/drivers/troubleshooting.html

**Contents:**
- Troubleshooting¶
- Scripted Expression¶
- Rotational Properties are Radians¶

Some common problems people may run into when using drivers.

A security warning in the Drivers panel.¶

An Auto-run warning in the Info editor’s header.¶

By default Blender will restrict execution of Python scripts.

If using a Scripted Expression Driver Type that doesn’t follow the Simple Expressions subset, you will have to open the file as Trusted Source, or set Auto Run Python Scripts in Preferences ‣ Save & Load ‣ Blender Files.

The Trusted Source checkbox in the File Browser.¶

The Auto Run Python Scripts checkbox in the Preferences.¶

Parts of the User Interface may use different units of measurements for angles, rotation. In the Graph Editor, while working with Drivers, all angles are Radians.

---

## Usage¶

**URL:** https://docs.blender.org/manual/en/latest/animation/drivers/usage.html

**Contents:**
- Usage¶
- Add Driver¶
- Edit Driver¶
- Open Drivers Editor¶
- Copy & Paste¶
- Copy Driver to Selected¶
- Copy As New Driver¶
- Expression¶
- Removing Drivers¶

Drivers can be added to properties via their context menu, a shortcut, copy-pasted, or by typing an expression directly into the property’s value.

After adding drivers, they are usually modified in the Drivers editor, or via a simplified Edit Driver popover invoked from the property context menu.

Context menu ‣ Add Driver

The usual way to add a driver to a property is to RMB click a property, then choose Add Driver in the context menu. Drivers can also be added by pressing Ctrl-D with the mouse over the property.

This operation adds a driver with a single variable (which needs to be filled in), and displays the Edit Driver popover.

Context menu ‣ Edit Driver

Displays a popover window that allows editing the custom expression and input variables of the driver without opening the full Drivers Editor.

Many drivers don’t use their F-Curve component, so this reduced interface is sufficient.

Context menu ‣ Open Drivers Editor

Opens a new window with the Drivers Editor and selects the driver associated with the property.

Context menu ‣ Copy Driver

Context menu ‣ Paste Driver

Drivers can be copied and pasted via the context menu. When adding drivers with the same settings, this can save time modifying settings.

Context menu ‣ Copy Drivers to Selected

Context menu ‣ Copy Driver to Selected

Context menu ‣ Copy All Drivers to Selected

Copy the property’s driver from the active item to the same property of all selected items, if the same property exists.

Context menu ‣ Copy As New Driver

A driver that sets the property value to the value of a different property can be quickly created by using the Copy As New Driver context menu option of the input property, and then pasting the result onto the output property via Paste Driver.

It is also possible to add the new driver variable to an existing driver using the Paste Driver Variables button in the editor panel.

This is a quick way to add drivers with a scripted expression. First click the property you want to add a driver to, then type a hash # and a scripted expression.

Context menu ‣ Delete Driver(s)

Context menu ‣ Delete Single Driver

Removes driver(s) associated with the property, either for the single selected property or sub-channel, or all components of a vector.

---

## Viewport Display¶

**URL:** https://docs.blender.org/manual/en/latest/animation/armatures/bones/properties/display.html

**Contents:**
- Viewport Display¶
- General¶
- Bone Colors¶
- Custom Shape¶

Object, Pose, and Edit Mode

Bone ‣ Viewport Display

This panel lets you customize the look of your bones.

Viewport Display panel in Object/Pose mode.¶

Viewport Display panel in Edit mode.¶

Hides the bone in the 3D Viewport. When this is unchecked, the bone’s visibility is determined by the visibility of its bone collections.

This controls the way the selected bones appear in the 3D Viewport. This overrides the Display Type of the armature.

Octahedral bone display.¶

B-Bone bone display.¶

Envelope bone display.¶

Use display mode from armature.

Display bones as octahedral shape.

Display bones as simple 2D lines with dots.

Display bones as boxes, showing subdivision and B-Splines.

Display bones as extruded spheres, showing deformation influence volume.

Display bones as thin wires, showing subdivision and B-Splines.

Bones can be individually colored. You can either choose a color set from the predefined theme list or define a custom one.

When selecting Custom Color Set, you need to define three colors: Regular (for when the bone is not selected), Selected, and Active.

You can temporarily disable all the color assignments by unchecking Bone Colors in the armature’s Viewport Display panel.

The bone’s primary color, affecting both Edit Mode and Pose Mode.

This color is stored on the armature data-block, so that if you have multiple armature objects that share this data-block, they will all use the same color.

Copy the bone color of the Active bone to all selected bones.

Lets you optionally override the above Bone Color in Pose Mode (by setting it to something else than Default Colors).

This color is stored on the Pose Bone, meaning it can be different in every armature object – even ones that reference the same data-block.

Copy the bone color of the Active bone to all selected bones.

Apart from custom colors, bones can also have custom shapes (in Object Mode and Pose Mode), using another object as a “template.”

A bone referencing a cone as its Custom Shape.¶

You can temporarily disable these shapes by unchecking Shapes in the armature’s Viewport Display panel.

Object that defines the custom shape of the selected bone.

Additional translation to apply to the custom shape.

Additional rotation to apply to the custom shape.

Additional scaling factor to apply to the custom shape.

A bone that defines the display transform of the custom shape. The shape defined in Custom Object will be placed at the location and orientation of that bone. This is only visual and does not affect the transform values of this bone.

The location and orientation of the Override Transform bone will be used for transform gizmos and for other transform operators in the 3D Viewport.

Transform the bone as if it was a child of the Override Transform bone. This is useful in special cases, where the mesh is deformed away from the bind pose by a separate mechanism, for example Shape Keys.

While this affects gizmo interaction, it does not change the transform values of the bone, or how they are interpolated. As such the interpolation may not work as expected.

Whether the custom shape should be scaled by a factor equal to the bone’s length.

When enabled, the bone is displayed in wireframe mode regardless of the viewport’s shading mode.

The line thickness of the wireframe for the custom shape.

Custom shapes will never be rendered. Like regular bones, they are only visible in the 3D Viewport.

The transforms of the template object are ignored. Moving, rotating, or scaling it will have no effect on its appearance in the armature.

The origin of each instanced shape object is at the root of the bone.

The rotation of each shape object is such that its Y axis lies along the direction of the bone.

For best results when Scale to Bone Length is enabled, make sure the template object is 1 unit in size along its Y axis. This will make it perfectly match the size of each bone.

---

## Workflow¶

**URL:** https://docs.blender.org/manual/en/latest/animation/shape_keys/workflow.html

**Contents:**
- Workflow¶
- Adding and Removing Vertices¶
- Adding Shape Keys¶
  - Relative Shape Keys¶
  - Absolute Shape Keys¶

Shape keys are created and managed in the Shape Keys panel, found in the Object Data tab of the Properties editor (for example, the Mesh tab for mesh objects).

A shape key is edited by selecting it in the panel and then moving the object’s vertices to new positions in the 3D Viewport.

The panel also contains controls to adjust the Value (influence or weight) of each shape key. This allows you to view a shape in isolation, or see how it combines with other active shape keys.

It is not possible to add or remove vertices in a shape key. The number of vertices and their connectivity is defined by the object’s topology (mesh, curve, surface, or lattice). A shape key only stores the positions of existing vertices, so all shape keys always include every vertex.

When new vertices are added, all existing shape keys will record them at their creation position. Although it is technically possible to add or delete vertices after creating shape keys, it is best practice to finalize the mesh topology before creating shape keys.

When adding a new shape key with the button next to the list, the new shape will be a copy of the Basis shape, regardless of the current visible result in the 3D Viewport.

When adding a new shape key via Specials ‣ New Shape from Mix, the new shape is created from the currently visible vertex configuration (including the influence of other shape keys).

For facial animation with relative shape keys, a common technique is to first create a shape key with a complex extreme pose (e.g. anger or surprise). You can then break it down into smaller components by applying a temporary vertex group to the complex shape and creating a copy with New Shape from Mix. This helps reduce conflicts between shape keys that would otherwise produce double effects.

In Object Mode, add a new shape key in the Shape Key panel ().

Basis is the rest shape. “Key 1”, “Key 2”, etc. will be the new shapes.

Switch to Edit Mode, select “Key 1” in the panel.

Modify the mesh as desired (do not add or remove vertices).

Select “Key 2”. The mesh resets to the Basis shape.

Modify “Key 2” as desired, then repeat for additional shape keys.

Switch back to Object Mode.

Adjust the Value sliders for “Key 1”, “Key 2”, etc. to blend between shapes.

The example below shows, from left to right: Basis, “Key 1”, “Key 2”, and a mix of “Key 1” (1.0) and “Key 2” (0.8) in Object Mode.

Relative shape keys example.¶

For practical examples, see Combining Shape Keys and Drivers.

Absolute shape keys workflow.¶

Add a sequence of shape keys as described above.

Disable the Relative checkbox.

Click the Reset Timing button.

Switch to Object Mode.

Drag Evaluation Time to scrub through the sequence of shapes.

By animating the Evaluation Time with a driver or keyframes, you can create shape key animations.

Shape key operators are available in Edit Mode which provide additional modeling tools for controlling shape keys:

---

## Workflow & Examples¶

**URL:** https://docs.blender.org/manual/en/latest/animation/drivers/workflow_examples.html

**Contents:**
- Workflow & Examples¶
- Transform Driver¶
- Scripted Expression - Orbit a Point¶
- Custom Function - Square Value¶
- View Layer Attribute Lookup¶
- Shape Key Drivers¶
  - Improved Mesh Deformation¶
  - Chained Relative Shape Keys¶

Simple Drivers can be configured from the pop-over that appears when adding a new Driver. When adding multiple Drivers or for more advanced configurations, it is useful to have open the Drivers Editor.

Control a property with an object’s transform. In this example, the Y rotation of Object 2 will be driven by the X position of Object 1. Starting from a simple setup with two objects:

Add a Driver to the Rotation Y property of the second object via the context menu or with Ctrl-D.

Open the Drivers Editor and select the Y Euler Rotation property in the channels region.

Open the Sidebar region and select the Drivers tab.

Configure the driver to be the Averaged Value of a Transform Channel of the first object.

Experiment with moving the first object and notice how it affects the Y rotation of the second object.

Orbit an object’s position around a point with a custom Scripted Expression. The object’s position will change when scrubbing the timeline. Using trigonometry, circular motion can be defined in 2D using the sine and cosine functions. (See Unit Circle.) In this example, the current frame is used as the variable that induces the motion. frame is a Simple Expression that corresponds to bpy.context.scene.frame_current.

Add a driver to the X Location property.

Set the Driver Type to Scripted Expression.

Add the expression 0 + (sin(frame / 8) * 4), where:

frame/8 : is the current frame of the animation, divided by 8 to slow the orbit down.

(sin( )*4) : multiplies the result of sin(frame/8) by 4 for a bigger circle.

0 + : is used to control the offset to the orbit center point.

Add a driver to the Y Location property with the expression 0 + (cos(frame / 8) * 4).

Scrub the timeline to see the effect. Experiment with the variables to control the size and center of the orbit.

Create a custom function to get the square of a value (i.e. value2). Adding the function to the Driver Namespace allows it to be used from driver expressions. The Driver Namespace has a list of built-in functions for use in driver expressions, as well as constants such as π and e. These can be inspected via the Python Console:

To add a new function to the Driver Namespace, the function itself needs to be implemented and then added to the bpy.app.driver_namespace.

Add the following to the Text Editor inside Blender and press Run Script.

Add a driver with a Scripted Expression such as square(frame).

Observe the effect when scrubbing the timeline.

There are more custom function examples available in Blender’s Text Editor Templates ‣ Python ‣ Driver Functions. Since Simple Expressions cannot access custom functions, using them only makes sense for complex computations.

Trying to replace built-in entries of the driver namespace may result in undefined behavior.

The material Attribute Node in the View Layer mode automatically searches for the attribute property in multiple locations. This, for example, can allow setting a certain value of the custom attribute at the Scene or World level, and then overriding it differently for one View Layer.

Context Properties of drivers don’t implement this behavior, so if necessary it has to be manually emulated via fallback values and a conditional expression (conditions are Simple Expressions).

For an attribute named attr, the node tries the following six RNA path lookups in order:

["attr"] in the active View Layer (custom property).

attr in the active View Layer (built-in property).

["attr"] in the active Scene.

attr in the active Scene.

world["attr"] in the active Scene.

world.attr in the active Scene.

Depending on the specific property it may be sufficient to check only a subset of these locations. For example, the image on the right shows how to access an attribute that is known to definitely be a custom property with a color value.

Driver variables accessing locations that are not final in the lookup chain should use fallback values that are invalid for the attribute (e.g. negative color values), which can then be checked by the conditional expression. The final variable should fallback to a valid default value to be used when the property is not set at all.

Fix intersection problems that happen when using armatures and weight painting, especially at joints. Shape keys can also be used to tweak and refine a rig, for example to suggest muscle formations. In this example, a shape key is used to improve the deformation at the elbow of a rudimentary arm.

Left: Skeletal mesh deformation without correction. Right: Corrective shape key applied¶

Add a mesh (in this example, a cylinder with loop cuts).

Add an armature with a chain of bones.

Skin the mesh to the armature using weight painting.

(Note: to parent the mesh to the armature: select the mesh first, then the armature and use Ctrl-P to parent with auto weights.)

Experiment with posing the armature and observe the deformation at the joint. To fix intersection problems or angles that look unsatisfactory, you can associate a Shape Key with a pose.

Pose the armature such that the problems are visible. Be sure to cover the extreme poses that you want to support for the rig.

With the mesh selected, add a new Shape Key in addition to the Basis key. Properties ‣ Mesh tab ‣ Shape Keys

In order to author the shape key on top of the armature deformation, enable both Edit Mode Display and Cage Editing in the Armature modifier. Properties ‣ Modifiers tab ‣ Armature Modifier ‣ Header

Enter Edit Mode and select the new shape key in the properties panel. Adjust the vertices as desired. Select the Basis key to toggle between the original mesh and your edits. (Note: be careful to apply edits only to your shape and not to the original mesh or other existing keys.)

Once you are satisfied with how the deformation looks for the problematic pose, you’ll need to configure a driver to activate the shape smoothly when entering that position.

Add a driver to the Value of the shape key you’ve created.

Open the Drivers Editor and select the driver.

A simple way to configure the driver is with a direct correspondence of the value of a bone’s rotation channel to the shape key activation Value. This method has the disadvantage of relying on a single channel of a bone’s rotation which might be insufficient to precisely express the condition under which the shape key should be activated.

In the Drivers tab, select the Averaged Value of the rotation of the bone you are posing.

Understand the rotation axis that you are interested in by enabling axes display in the armature or by observing the bone’s transform values in the Properties.

Select the rotation channel and set it to local, meaning, the bone’s rotation value relative to its parent bone.

Manually set points in the driver curve by selecting a handle and dragging it or inserting values in the F-Curve tab. The Y axis represents the shape key Value, which should go from 0.0 to 1.0. The X axis is usually the frame, but for this driver it represents the rotation value in radians. You can have more than two points in the curve and tweak the transitions with the handles in the curve view (G to move).

To verify that the driver behaves correctly, deselect the option to only show drivers for selected objects. This way, you can pose the armature and keep an eye on the driver.

This method requires an additional target or corrective bone, but it better expresses the spatial condition in 3D space of the bone that is causing the problem.

In armature Edit Mode, add a new bone extruded from Bone 1, in the position at which Bone 2 should have the shape key active. This type of bones usually follow a naming convention such as “TAR-” (target) or “COR-” (corrective).

In the Drivers tab, select the Averaged Value of the rotational difference between the bone you are rotating and the target bone. A rotational difference is the minimum angle between two objects in World Space. It is therefore important that the bones have the same root, so that the only thing affecting the angle between the bones is the rotation of one of them. When the deformation bone (Bone 2) reaches the target rotation (TAR-Bone 2) the rotational difference will be 0°.

Manually adjust the driver curve handles so that the shape key Value (Y axis) is 1.0 when the rotational difference (X axis) is 0°. The Value should be 0.0 when the arm is extended, at which point the rotational difference should be around 90° or more (in radians).

See the steps in Method 1 on how to adjust the curve handles and confirm that the functionality is working. Pose the armature to verify that the ranges are correct.

Activate different shape keys in succession. In this example, moving a single bone will activate first Key 1 and then Key 2. See also relative shape keys mix additively.

Add two shape keys to a mesh, besides the Basis.

Key 1: top faces moved up by 1 m.¶

Key 2: inner top moved up by 1 m.¶

Add an armature with a single bone to control the shape keys. The goal is to activate the keys in succession as this bone moves up.

As shown in the picture above, when the bone is halfway up, both Key 1 and Key 2 have an influence. It is a matter of preference if Key 1 should be at its maximum Value before Key 2 starts to become active, or how much they should overlap. This example shows a seamless blend.

For a seamless blend where there is overlap, Key 1 should have a Value of 0.0 when the bone is at the bottom and increase linearly to 1.0 until the bone is past the midpoint height. Key 2 should have a value of 0.0 before the midpoint height and then increase at the same rate than Key 1 until reaching Value 1.0 when the bone is at maximum height.

Add a driver to the Value of Key 1 and Key 2. In the Drivers tab, configure both drivers to be the Averaged Value of a variable with the bone’s Z location.

Determine the range of the bone’s motion in the World Z axis by moving it up so that it is aligned with the top of the mesh when both keys are active. Here we will use [0.0, 2.5].

Configure the driver functions so that the Value of the shape keys (Y axis) is as desired for the bone’s height (X axis).

The driver functions should be linear, therefore, they can be defined analytically with a function of type \(y = a + bx\), where \(a\) is an offset in \(y\) and \(b\) is the slope.

In the Modifiers tab, add a Generator of type Extended Polynomial for both drivers.

Play with the values of \(a\) and \(b\) so that the curves go from [0.0, 1.0] in the Y axis and from [0.0, 2.5] in the X axis. The curves should overlap in the mid area of the X axis and they should have the same slope (\(b\)).

Possible values are Key 1: \(y = 0.0 + 0.6x\) and Key 2: \(y = -0.5 + 0.6x\).

Note that the functions go outside the range [0.0, 1.0] for the shape keys’ Value, but that has no effect because Value is clamped in a Range in the Shape Keys panel.

**Examples:**

Example 1 (typescript):
```typescript
>>> bpy.app.driver_namespace[' <tab>
                              acos']
                              acosh']
                              asin']
                              asinh']
                              atan']
                              ...
```

Example 2 (python):
```python
import bpy

def square(val):
   """Returns the square of the given value"""
   return val * val

# Add function to driver_namespace.
bpy.app.driver_namespace['square'] = square
```

---
