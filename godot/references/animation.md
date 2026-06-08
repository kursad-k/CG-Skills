# Godot - Animation

**Pages:** 35

---

## Animating thousands of objects

**URL:** https://docs.godotengine.org/en/stable/tutorials/performance/vertex_animation/index.html

**Contents:**
- Animating thousands of objects

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

---

## AnimationMixer

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationmixer.html

**Contents:**
- AnimationMixer
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

Inherited By: AnimationPlayer, AnimationTree

Base class for AnimationPlayer and AnimationTree.

Base class for AnimationPlayer and AnimationTree to manage animation lists. It also has general properties and methods for playback and blending.

After instantiating the playback information data within the extended class, the blending is processed by the AnimationMixer.

Migrating Animations from Godot 4.0 to 4.3

AnimationCallbackModeDiscrete

callback_mode_discrete

AnimationCallbackModeMethod

AnimationCallbackModeProcess

callback_mode_process

_post_process_key_value(animation: Animation, track: int, value: Variant, object_id: int, object_sub_idx: int) virtual const

add_animation_library(name: StringName, library: AnimationLibrary)

advance(delta: float)

capture(name: StringName, duration: float, trans_type: TransitionType = 0, ease_type: EaseType = 0)

find_animation(animation: Animation) const

find_animation_library(animation: Animation) const

get_animation(name: StringName) const

get_animation_library(name: StringName) const

get_animation_library_list() const

get_animation_list() const

get_root_motion_position() const

get_root_motion_position_accumulator() const

get_root_motion_rotation() const

get_root_motion_rotation_accumulator() const

get_root_motion_scale() const

get_root_motion_scale_accumulator() const

has_animation(name: StringName) const

has_animation_library(name: StringName) const

remove_animation_library(name: StringName)

rename_animation_library(name: StringName, newname: StringName)

animation_finished(anim_name: StringName) 

Notifies when an animation finished playing.

Note: This signal is not emitted if an animation is looping.

animation_libraries_updated() 

Notifies when the animation libraries have changed.

animation_list_changed() 

Notifies when an animation list is changed.

animation_started(anim_name: StringName) 

Notifies when an animation starts playing.

Note: This signal is not emitted if an animation is looping.

Notifies when the caches have been cleared, either automatically, or manually via clear_caches().

Notifies when the blending result related have been applied to the target objects.

Notifies when the property related process have been updated.

enum AnimationCallbackModeProcess: 

AnimationCallbackModeProcess ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS = 0

Process animation during physics frames (see Node.NOTIFICATION_INTERNAL_PHYSICS_PROCESS). This is especially useful when animating physics bodies.

AnimationCallbackModeProcess ANIMATION_CALLBACK_MODE_PROCESS_IDLE = 1

Process animation during process frames (see Node.NOTIFICATION_INTERNAL_PROCESS).

AnimationCallbackModeProcess ANIMATION_CALLBACK_MODE_PROCESS_MANUAL = 2

Do not process animation. Use advance() to process the animation manually.

enum AnimationCallbackModeMethod: 

AnimationCallbackModeMethod ANIMATION_CALLBACK_MODE_METHOD_DEFERRED = 0

Batch method calls during the animation process, then do the calls after events are processed. This avoids bugs involving deleting nodes or modifying the AnimationPlayer while playing.

AnimationCallbackModeMethod ANIMATION_CALLBACK_MODE_METHOD_IMMEDIATE = 1

Make method calls immediately when reached in the animation.

enum AnimationCallbackModeDiscrete: 

AnimationCallbackModeDiscrete ANIMATION_CALLBACK_MODE_DISCRETE_DOMINANT = 0

An Animation.UPDATE_DISCRETE track value takes precedence when blending Animation.UPDATE_CONTINUOUS or Animation.UPDATE_CAPTURE track values and Animation.UPDATE_DISCRETE track values.

AnimationCallbackModeDiscrete ANIMATION_CALLBACK_MODE_DISCRETE_RECESSIVE = 1

An Animation.UPDATE_CONTINUOUS or Animation.UPDATE_CAPTURE track value takes precedence when blending the Animation.UPDATE_CONTINUOUS or Animation.UPDATE_CAPTURE track values and the Animation.UPDATE_DISCRETE track values. This is the default behavior for AnimationPlayer.

AnimationCallbackModeDiscrete ANIMATION_CALLBACK_MODE_DISCRETE_FORCE_CONTINUOUS = 2

Always treat the Animation.UPDATE_DISCRETE track value as Animation.UPDATE_CONTINUOUS with Animation.INTERPOLATION_NEAREST. This is the default behavior for AnimationTree.

If a value track has un-interpolatable type key values, it is internally converted to use ANIMATION_CALLBACK_MODE_DISCRETE_RECESSIVE with Animation.UPDATE_DISCRETE.

Un-interpolatable type list:

@GlobalScope.TYPE_NIL

@GlobalScope.TYPE_NODE_PATH

@GlobalScope.TYPE_RID

@GlobalScope.TYPE_OBJECT

@GlobalScope.TYPE_CALLABLE

@GlobalScope.TYPE_SIGNAL

@GlobalScope.TYPE_DICTIONARY

@GlobalScope.TYPE_PACKED_BYTE_ARRAY

@GlobalScope.TYPE_BOOL and @GlobalScope.TYPE_INT are treated as @GlobalScope.TYPE_FLOAT during blending and rounded when the result is retrieved.

It is same for arrays and vectors with them such as @GlobalScope.TYPE_PACKED_INT32_ARRAY or @GlobalScope.TYPE_VECTOR2I, they are treated as @GlobalScope.TYPE_PACKED_FLOAT32_ARRAY or @GlobalScope.TYPE_VECTOR2. Also note that for arrays, the size is also interpolated.

@GlobalScope.TYPE_STRING and @GlobalScope.TYPE_STRING_NAME are interpolated between character codes and lengths, but note that there is a difference in algorithm between interpolation between keys and interpolation by blending.

void set_active(value: bool)

If true, the AnimationMixer will be processing.

int audio_max_polyphony = 32 

void set_audio_max_polyphony(value: int)

int get_audio_max_polyphony()

The number of possible simultaneous sounds for each of the assigned AudioStreamPlayers.

For example, if this value is 32 and the animation has two audio tracks, the two AudioStreamPlayers assigned can play simultaneously up to 32 voices each.

AnimationCallbackModeDiscrete callback_mode_discrete = 1 

void set_callback_mode_discrete(value: AnimationCallbackModeDiscrete)

AnimationCallbackModeDiscrete get_callback_mode_discrete()

Ordinarily, tracks can be set to Animation.UPDATE_DISCRETE to update infrequently, usually when using nearest interpolation.

However, when blending with Animation.UPDATE_CONTINUOUS several results are considered. The callback_mode_discrete specify it explicitly. See also AnimationCallbackModeDiscrete.

To make the blended results look good, it is recommended to set this to ANIMATION_CALLBACK_MODE_DISCRETE_FORCE_CONTINUOUS to update every frame during blending. Other values exist for compatibility and they are fine if there is no blending, but not so, may produce artifacts.

AnimationCallbackModeMethod callback_mode_method = 0 

void set_callback_mode_method(value: AnimationCallbackModeMethod)

AnimationCallbackModeMethod get_callback_mode_method()

The call mode used for "Call Method" tracks.

AnimationCallbackModeProcess callback_mode_process = 1 

void set_callback_mode_process(value: AnimationCallbackModeProcess)

AnimationCallbackModeProcess get_callback_mode_process()

The process notification in which to update animations.

bool deterministic = false 

void set_deterministic(value: bool)

bool is_deterministic()

If true, the blending uses the deterministic algorithm. The total weight is not normalized and the result is accumulated with an initial value (0 or a "RESET" animation if present).

This means that if the total amount of blending is 0.0, the result is equal to the "RESET" animation.

If the number of tracks between the blended animations is different, the animation with the missing track is treated as if it had the initial value.

If false, The blend does not use the deterministic algorithm. The total weight is normalized and always 1.0. If the number of tracks between the blended animations is different, nothing is done about the animation that is missing a track.

Note: In AnimationTree, the blending with AnimationNodeAdd2, AnimationNodeAdd3, AnimationNodeSub2 or the weight greater than 1.0 may produce unexpected results.

For example, if AnimationNodeAdd2 blends two nodes with the amount 1.0, then total weight is 2.0 but it will be normalized to make the total amount 1.0 and the result will be equal to AnimationNodeBlend2 with the amount 0.5.

bool reset_on_save = true 

void set_reset_on_save_enabled(value: bool)

bool is_reset_on_save_enabled()

This is used by the editor. If set to true, the scene will be saved with the effects of the reset animation (the animation with the key "RESET") applied as if it had been seeked to time 0, with the editor keeping the values that the scene had before saving.

This makes it more convenient to preview and edit animations in the editor, as changes to the scene will not be saved as long as they are set in the reset animation.

bool root_motion_local = false 

void set_root_motion_local(value: bool)

bool is_root_motion_local()

If true, get_root_motion_position() value is extracted as a local translation value before blending. In other words, it is treated like the translation is done after the rotation.

NodePath root_motion_track = NodePath("") 

void set_root_motion_track(value: NodePath)

NodePath get_root_motion_track()

The path to the Animation track used for root motion. Paths must be valid scene-tree paths to a node, and must be specified starting from the parent node of the node that will reproduce the animation. The root_motion_track uses the same format as Animation.track_set_path(), but note that a bone must be specified.

If the track has type Animation.TYPE_POSITION_3D, Animation.TYPE_ROTATION_3D, or Animation.TYPE_SCALE_3D the transformation will be canceled visually, and the animation will appear to stay in place. See also get_root_motion_position(), get_root_motion_rotation(), get_root_motion_scale(), and RootMotionView.

NodePath root_node = NodePath("..") 

void set_root_node(value: NodePath)

NodePath get_root_node()

The node which node path references will travel from.

Variant _post_process_key_value(animation: Animation, track: int, value: Variant, object_id: int, object_sub_idx: int) virtual const 

A virtual function for processing after getting a key during playback.

Error add_animation_library(name: StringName, library: AnimationLibrary) 

Adds library to the animation player, under the key name.

AnimationMixer has a global library by default with an empty string as key. For adding an animation to the global library:

void advance(delta: float) 

Manually advance the animations by the specified time (in seconds).

void capture(name: StringName, duration: float, trans_type: TransitionType = 0, ease_type: EaseType = 0) 

If the animation track specified by name has an option Animation.UPDATE_CAPTURE, stores current values of the objects indicated by the track path as a cache. If there is already a captured cache, the old cache is discarded.

After this it will interpolate with current animation blending result during the playback process for the time specified by duration, working like a crossfade.

You can specify trans_type as the curve for the interpolation. For better results, it may be appropriate to specify Tween.TRANS_LINEAR for cases where the first key of the track begins with a non-zero value or where the key value does not change, and Tween.TRANS_QUAD for cases where the key value changes linearly.

void clear_caches() 

AnimationMixer caches animated nodes. It may not notice if a node disappears; clear_caches() forces it to update the cache again.

StringName find_animation(animation: Animation) const 

Returns the key of animation or an empty StringName if not found.

StringName find_animation_library(animation: Animation) const 

Returns the key for the AnimationLibrary that contains animation or an empty StringName if not found.

Animation get_animation(name: StringName) const 

Returns the Animation with the key name. If the animation does not exist, null is returned and an error is logged.

AnimationLibrary get_animation_library(name: StringName) const 

Returns the first AnimationLibrary with key name or null if not found.

To get the AnimationMixer's global animation library, use get_animation_library("").

Array[StringName] get_animation_library_list() const 

Returns the list of stored library keys.

PackedStringArray get_animation_list() const 

Returns the list of stored animation keys.

Vector3 get_root_motion_position() const 

Retrieve the motion delta of position with the root_motion_track as a Vector3 that can be used elsewhere.

If root_motion_track is not a path to a track of type Animation.TYPE_POSITION_3D, returns Vector3(0, 0, 0).

See also root_motion_track and RootMotionView.

The most basic example is applying position to CharacterBody3D:

By using this in combination with get_root_motion_rotation_accumulator(), you can apply the root motion position more correctly to account for the rotation of the node.

If root_motion_local is true, returns the pre-multiplied translation value with the inverted rotation.

In this case, the code can be written as follows:

Vector3 get_root_motion_position_accumulator() const 

Retrieve the blended value of the position tracks with the root_motion_track as a Vector3 that can be used elsewhere.

This is useful in cases where you want to respect the initial key values of the animation.

For example, if an animation with only one key Vector3(0, 0, 0) is played in the previous frame and then an animation with only one key Vector3(1, 0, 1) is played in the next frame, the difference can be calculated as follows:

However, if the animation loops, an unintended discrete change may occur, so this is only useful for some simple use cases.

Quaternion get_root_motion_rotation() const 

Retrieve the motion delta of rotation with the root_motion_track as a Quaternion that can be used elsewhere.

If root_motion_track is not a path to a track of type Animation.TYPE_ROTATION_3D, returns Quaternion(0, 0, 0, 1).

See also root_motion_track and RootMotionView.

The most basic example is applying rotation to CharacterBody3D:

Quaternion get_root_motion_rotation_accumulator() const 

Retrieve the blended value of the rotation tracks with the root_motion_track as a Quaternion that can be used elsewhere.

This is necessary to apply the root motion position correctly, taking rotation into account. See also get_root_motion_position().

Also, this is useful in cases where you want to respect the initial key values of the animation.

For example, if an animation with only one key Quaternion(0, 0, 0, 1) is played in the previous frame and then an animation with only one key Quaternion(0, 0.707, 0, 0.707) is played in the next frame, the difference can be calculated as follows:

However, if the animation loops, an unintended discrete change may occur, so this is only useful for some simple use cases.

Vector3 get_root_motion_scale() const 

Retrieve the motion delta of scale with the root_motion_track as a Vector3 that can be used elsewhere.

If root_motion_track is not a path to a track of type Animation.TYPE_SCALE_3D, returns Vector3(0, 0, 0).

See also root_motion_track and RootMotionView.

The most basic example is applying scale to CharacterBody3D:

Vector3 get_root_motion_scale_accumulator() const 

Retrieve the blended value of the scale tracks with the root_motion_track as a Vector3 that can be used elsewhere.

For example, if an animation with only one key Vector3(1, 1, 1) is played in the previous frame and then an animation with only one key Vector3(2, 2, 2) is played in the next frame, the difference can be calculated as follows:

However, if the animation loops, an unintended discrete change may occur, so this is only useful for some simple use cases.

bool has_animation(name: StringName) const 

Returns true if the AnimationMixer stores an Animation with key name.

bool has_animation_library(name: StringName) const 

Returns true if the AnimationMixer stores an AnimationLibrary with key name.

void remove_animation_library(name: StringName) 

Removes the AnimationLibrary associated with the key name.

void rename_animation_library(name: StringName, newname: StringName) 

Moves the AnimationLibrary associated with the key name to the key newname.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var global_library = mixer.get_animation_library("")
global_library.add_animation("animation_name", animation_resource)
```

Example 2 (gdscript):
```gdscript
var current_rotation

func _process(delta):
    if Input.is_action_just_pressed("animate"):
        current_rotation = get_quaternion()
        state_machine.travel("Animate")
    var velocity = current_rotation * animation_tree.get_root_motion_position() / delta
    set_velocity(velocity)
    move_and_slide()
```

Example 3 (gdscript):
```gdscript
func _process(delta):
    if Input.is_action_just_pressed("animate"):
        state_machine.travel("Animate")
    set_quaternion(get_quaternion() * animation_tree.get_root_motion_rotation())
    var velocity = (animation_tree.get_root_motion_rotation_accumulator().inverse() * get_quaternion()) * animation_tree.get_root_motion_position() / delta
    set_velocity(velocity)
    move_and_slide()
```

Example 4 (gdscript):
```gdscript
func _process(delta):
    if Input.is_action_just_pressed("animate"):
        state_machine.travel("Animate")
    set_quaternion(get_quaternion() * animation_tree.get_root_motion_rotation())
    var velocity = get_quaternion() * animation_tree.get_root_motion_position() / delta
    set_velocity(velocity)
    move_and_slide()
```

---

## AnimationNodeAdd2

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodeadd2.html

**Contents:**
- AnimationNodeAdd2
- Description
- Tutorials
- User-contributed notes

Inherits: AnimationNodeSync < AnimationNode < Resource < RefCounted < Object

Blends two animations additively inside of an AnimationNodeBlendTree.

A resource to add to an AnimationNodeBlendTree. Blends two animations additively based on the amount value.

If the amount is greater than 1.0, the animation connected to "in" port is blended with the amplified animation connected to "add" port.

If the amount is less than 0.0, the animation connected to "in" port is blended with the inverted animation connected to "add" port.

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeAdd3

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodeadd3.html

**Contents:**
- AnimationNodeAdd3
- Description
- Tutorials
- User-contributed notes

Inherits: AnimationNodeSync < AnimationNode < Resource < RefCounted < Object

Blends two of three animations additively inside of an AnimationNodeBlendTree.

A resource to add to an AnimationNodeBlendTree. Blends two animations out of three additively out of three based on the amount value.

This animation node has three inputs:

The base animation to add to

A "-add" animation to blend with when the blend amount is negative

A "+add" animation to blend with when the blend amount is positive

If the absolute value of the amount is greater than 1.0, the animation connected to "in" port is blended with the amplified animation connected to "-add"/"+add" port.

Third Person Shooter (TPS) Demo

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeAnimation

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodeanimation.html

**Contents:**
- AnimationNodeAnimation
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: AnimationRootNode < AnimationNode < Resource < RefCounted < Object

An input animation for an AnimationNodeBlendTree.

A resource to add to an AnimationNodeBlendTree. Only has one output port using the animation property. Used as an input for AnimationNodes that blend animations together.

Third Person Shooter (TPS) Demo

PlayMode PLAY_MODE_FORWARD = 0

Plays animation in forward direction.

PlayMode PLAY_MODE_BACKWARD = 1

Plays animation in backward direction.

bool advance_on_start = false 

void set_advance_on_start(value: bool)

bool is_advance_on_start()

If true, on receiving a request to play an animation from the start, the first frame is not drawn, but only processed, and playback starts from the next frame.

See also the notes of AnimationPlayer.play().

StringName animation = &"" 

void set_animation(value: StringName)

StringName get_animation()

Animation to use as an output. It is one of the animations provided by AnimationTree.anim_player.

void set_loop_mode(value: LoopMode)

LoopMode get_loop_mode()

If use_custom_timeline is true, override the loop settings of the original Animation resource with the value.

Note: If the Animation.loop_mode isn't set to looping, the Animation.track_set_interpolation_loop_wrap() option will not be respected. If you cannot get the expected behavior, consider duplicating the Animation resource and changing the loop settings.

PlayMode play_mode = 0 

void set_play_mode(value: PlayMode)

PlayMode get_play_mode()

Determines the playback direction of the animation.

void set_start_offset(value: float)

float get_start_offset()

If use_custom_timeline is true, offset the start position of the animation.

This is useful for adjusting which foot steps first in 3D walking animations.

bool stretch_time_scale 

void set_stretch_time_scale(value: bool)

bool is_stretching_time_scale()

If true, scales the time so that the length specified in timeline_length is one cycle.

This is useful for matching the periods of walking and running animations.

If false, the original animation length is respected. If you set the loop to loop_mode, the animation will loop in timeline_length.

float timeline_length 

void set_timeline_length(value: float)

float get_timeline_length()

If use_custom_timeline is true, offset the start position of the animation.

bool use_custom_timeline = false 

void set_use_custom_timeline(value: bool)

bool is_using_custom_timeline()

If true, AnimationNode provides an animation based on the Animation resource with some parameters adjusted.

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeBlend2

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodeblend2.html

**Contents:**
- AnimationNodeBlend2
- Description
- Tutorials
- User-contributed notes

Inherits: AnimationNodeSync < AnimationNode < Resource < RefCounted < Object

Blends two animations linearly inside of an AnimationNodeBlendTree.

A resource to add to an AnimationNodeBlendTree. Blends two animations linearly based on the amount value.

In general, the blend value should be in the [0.0, 1.0] range. Values outside of this range can blend amplified or inverted animations, however, AnimationNodeAdd2 works better for this purpose.

Third Person Shooter (TPS) Demo

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeBlend3

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodeblend3.html

**Contents:**
- AnimationNodeBlend3
- Description
- Tutorials
- User-contributed notes

Inherits: AnimationNodeSync < AnimationNode < Resource < RefCounted < Object

Blends two of three animations linearly inside of an AnimationNodeBlendTree.

A resource to add to an AnimationNodeBlendTree. Blends two animations out of three linearly out of three based on the amount value.

This animation node has three inputs:

The base animation to blend with

A "-blend" animation to blend with when the blend amount is negative value

A "+blend" animation to blend with when the blend amount is positive value

In general, the blend value should be in the [-1.0, 1.0] range. Values outside of this range can blend amplified animations, however, AnimationNodeAdd3 works better for this purpose.

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeBlendSpace1D

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodeblendspace1d.html

**Contents:**
- AnimationNodeBlendSpace1D
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AnimationRootNode < AnimationNode < Resource < RefCounted < Object

A set of AnimationRootNodes placed on a virtual axis, crossfading between the two adjacent ones. Used by AnimationTree.

A resource used by AnimationNodeBlendTree.

AnimationNodeBlendSpace1D represents a virtual axis on which any type of AnimationRootNodes can be added using add_blend_point(). Outputs the linear blend of the two AnimationRootNodes adjacent to the current value.

You can set the extents of the axis with min_space and max_space.

add_blend_point(node: AnimationRootNode, pos: float, at_index: int = -1)

get_blend_point_count() const

get_blend_point_node(point: int) const

get_blend_point_position(point: int) const

remove_blend_point(point: int)

set_blend_point_node(point: int, node: AnimationRootNode)

set_blend_point_position(point: int, pos: float)

BlendMode BLEND_MODE_INTERPOLATED = 0

The interpolation between animations is linear.

BlendMode BLEND_MODE_DISCRETE = 1

The blend space plays the animation of the animation node which blending position is closest to. Useful for frame-by-frame 2D animations.

BlendMode BLEND_MODE_DISCRETE_CARRY = 2

Similar to BLEND_MODE_DISCRETE, but starts the new animation at the last animation's playback position.

BlendMode blend_mode = 0 

void set_blend_mode(value: BlendMode)

BlendMode get_blend_mode()

Controls the interpolation between animations.

float max_space = 1.0 

void set_max_space(value: float)

float get_max_space()

The blend space's axis's upper limit for the points' position. See add_blend_point().

float min_space = -1.0 

void set_min_space(value: float)

float get_min_space()

The blend space's axis's lower limit for the points' position. See add_blend_point().

void set_snap(value: float)

Position increment to snap to when moving a point on the axis.

void set_use_sync(value: bool)

If false, the blended animations' frame are stopped when the blend value is 0.

If true, forcing the blended animations to advance frame.

String value_label = "value" 

void set_value_label(value: String)

String get_value_label()

Label of the virtual axis of the blend space.

void add_blend_point(node: AnimationRootNode, pos: float, at_index: int = -1) 

Adds a new point that represents a node on the virtual axis at a given position set by pos. You can insert it at a specific index using the at_index argument. If you use the default value for at_index, the point is inserted at the end of the blend points array.

int get_blend_point_count() const 

Returns the number of points on the blend axis.

AnimationRootNode get_blend_point_node(point: int) const 

Returns the AnimationNode referenced by the point at index point.

float get_blend_point_position(point: int) const 

Returns the position of the point at index point.

void remove_blend_point(point: int) 

Removes the point at index point from the blend axis.

void set_blend_point_node(point: int, node: AnimationRootNode) 

Changes the AnimationNode referenced by the point at index point.

void set_blend_point_position(point: int, pos: float) 

Updates the position of the point at index point on the blend axis.

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeBlendTree

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodeblendtree.html

**Contents:**
- AnimationNodeBlendTree
- Description
- Tutorials
- Properties
- Methods
- Signals
- Constants
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AnimationRootNode < AnimationNode < Resource < RefCounted < Object

A sub-tree of many type AnimationNodes used for complex animations. Used by AnimationTree.

This animation node may contain a sub-tree of any other type animation nodes, such as AnimationNodeTransition, AnimationNodeBlend2, AnimationNodeBlend3, AnimationNodeOneShot, etc. This is one of the most commonly used animation node roots.

An AnimationNodeOutput node named output is created by default.

add_node(name: StringName, node: AnimationNode, position: Vector2 = Vector2(0, 0))

connect_node(input_node: StringName, input_index: int, output_node: StringName)

disconnect_node(input_node: StringName, input_index: int)

get_node(name: StringName) const

get_node_list() const

get_node_position(name: StringName) const

has_node(name: StringName) const

remove_node(name: StringName)

rename_node(name: StringName, new_name: StringName)

set_node_position(name: StringName, position: Vector2)

node_changed(node_name: StringName) 

Emitted when the input port information is changed.

The connection was successful.

CONNECTION_ERROR_NO_INPUT = 1 

The input node is null.

CONNECTION_ERROR_NO_INPUT_INDEX = 2 

The specified input port is out of range.

CONNECTION_ERROR_NO_OUTPUT = 3 

The output node is null.

CONNECTION_ERROR_SAME_NODE = 4 

Input and output nodes are the same.

CONNECTION_ERROR_CONNECTION_EXISTS = 5 

The specified connection already exists.

Vector2 graph_offset = Vector2(0, 0) 

void set_graph_offset(value: Vector2)

Vector2 get_graph_offset()

The global offset of all sub animation nodes.

void add_node(name: StringName, node: AnimationNode, position: Vector2 = Vector2(0, 0)) 

Adds an AnimationNode at the given position. The name is used to identify the created sub animation node later.

void connect_node(input_node: StringName, input_index: int, output_node: StringName) 

Connects the output of an AnimationNode as input for another AnimationNode, at the input port specified by input_index.

void disconnect_node(input_node: StringName, input_index: int) 

Disconnects the animation node connected to the specified input.

AnimationNode get_node(name: StringName) const 

Returns the sub animation node with the specified name.

Array[StringName] get_node_list() const 

Returns a list containing the names of all sub animation nodes in this blend tree.

Vector2 get_node_position(name: StringName) const 

Returns the position of the sub animation node with the specified name.

bool has_node(name: StringName) const 

Returns true if a sub animation node with specified name exists.

void remove_node(name: StringName) 

Removes a sub animation node.

void rename_node(name: StringName, new_name: StringName) 

Changes the name of a sub animation node.

void set_node_position(name: StringName, position: Vector2) 

Modifies the position of a sub animation node.

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeExtension

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodeextension.html

**Contents:**
- AnimationNodeExtension
- Description
- Methods
- Method Descriptions
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: AnimationNode < Resource < RefCounted < Object

Base class for extending AnimationRootNodes from GDScript, C#, or C++.

AnimationNodeExtension exposes the APIs of AnimationRootNode to allow users to extend it from GDScript, C#, or C++. This class is not meant to be used directly, but to be extended by other classes. It is used to create custom nodes for the AnimationTree system.

_process_animation_node(playback_info: PackedFloat64Array, test_only: bool) virtual required

get_remaining_time(node_info: PackedFloat32Array, break_loop: bool) static

is_looping(node_info: PackedFloat32Array) static

PackedFloat32Array _process_animation_node(playback_info: PackedFloat64Array, test_only: bool) virtual required 

A version of the AnimationNode._process() method that is meant to be overridden by custom nodes. It returns a PackedFloat32Array with the processed animation data.

The PackedFloat64Array parameter contains the playback information, containing the following values encoded as floating point numbers (in order): playback time and delta, start and end times, whether a seek was requested (encoded as a float greater than 0), whether the seek request was externally requested (encoded as a float greater than 0), the current LoopedFlag (encoded as a float), and the current blend weight.

The function must return a PackedFloat32Array of the node's time info, containing the following values (in order): animation length, time position, delta, LoopMode (encoded as a float), whether the animation is about to end (encoded as a float greater than 0) and whether the animation is infinite (encoded as a float greater than 0). All values must be included in the returned array.

float get_remaining_time(node_info: PackedFloat32Array, break_loop: bool) static 

Returns the animation's remaining time for the given node info. For looping animations, it will only return the remaining time if break_loop is true, a large integer value will be returned otherwise.

bool is_looping(node_info: PackedFloat32Array) static 

Returns true if the animation for the given node_info is looping.

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeOneShot

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodeoneshot.html

**Contents:**
- AnimationNodeOneShot
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: AnimationNodeSync < AnimationNode < Resource < RefCounted < Object

Plays an animation once in an AnimationNodeBlendTree.

A resource to add to an AnimationNodeBlendTree. This animation node will execute a sub-animation and return once it finishes. Blend times for fading in and out can be customized, as well as filters.

After setting the request and changing the animation playback, the one-shot node automatically clears the request on the next process frame by setting its request value to ONE_SHOT_REQUEST_NONE.

Third Person Shooter (TPS) Demo

autorestart_random_delay

enum OneShotRequest: 

OneShotRequest ONE_SHOT_REQUEST_NONE = 0

The default state of the request. Nothing is done.

OneShotRequest ONE_SHOT_REQUEST_FIRE = 1

The request to play the animation connected to "shot" port.

OneShotRequest ONE_SHOT_REQUEST_ABORT = 2

The request to stop the animation connected to "shot" port.

OneShotRequest ONE_SHOT_REQUEST_FADE_OUT = 3

The request to fade out the animation connected to "shot" port.

MixMode MIX_MODE_BLEND = 0

Blends two animations. See also AnimationNodeBlend2.

MixMode MIX_MODE_ADD = 1

Blends two animations additively. See also AnimationNodeAdd2.

bool autorestart = false 

void set_autorestart(value: bool)

bool has_autorestart()

If true, the sub-animation will restart automatically after finishing.

In other words, to start auto restarting, the animation must be played once with the ONE_SHOT_REQUEST_FIRE request. The ONE_SHOT_REQUEST_ABORT request stops the auto restarting, but it does not disable the autorestart itself. So, the ONE_SHOT_REQUEST_FIRE request will start auto restarting again.

float autorestart_delay = 1.0 

void set_autorestart_delay(value: float)

float get_autorestart_delay()

The delay after which the automatic restart is triggered, in seconds.

float autorestart_random_delay = 0.0 

void set_autorestart_random_delay(value: float)

float get_autorestart_random_delay()

If autorestart is true, a random additional delay (in seconds) between 0 and this value will be added to autorestart_delay.

bool break_loop_at_end = false 

void set_break_loop_at_end(value: bool)

bool is_loop_broken_at_end()

If true, breaks the loop at the end of the loop cycle for transition, even if the animation is looping.

void set_fadein_curve(value: Curve)

Curve get_fadein_curve()

Determines how cross-fading between animations is eased. If empty, the transition will be linear. Should be a unit Curve.

float fadein_time = 0.0 

void set_fadein_time(value: float)

float get_fadein_time()

The fade-in duration. For example, setting this to 1.0 for a 5 second length animation will produce a cross-fade that starts at 0 second and ends at 1 second during the animation.

Note: AnimationNodeOneShot transitions the current state after the fading has finished.

Curve fadeout_curve 

void set_fadeout_curve(value: Curve)

Curve get_fadeout_curve()

Determines how cross-fading between animations is eased. If empty, the transition will be linear. Should be a unit Curve.

float fadeout_time = 0.0 

void set_fadeout_time(value: float)

float get_fadeout_time()

The fade-out duration. For example, setting this to 1.0 for a 5 second length animation will produce a cross-fade that starts at 4 second and ends at 5 second during the animation.

Note: AnimationNodeOneShot transitions the current state after the fading has finished.

MixMode mix_mode = 0 

void set_mix_mode(value: MixMode)

MixMode get_mix_mode()

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (markdown):
```markdown
# Play child animation connected to "shot" port.
animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_FIRE)
# Alternative syntax (same result as above).
animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_FIRE

# Abort child animation connected to "shot" port.
animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_ABORT)
# Alternative syntax (same result as above).
animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_ABORT

# Abort child animation with fading out connected to "shot" port.
animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_FADE_OUT)
# Alternative syntax (same result as above).
animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_FADE_OUT

# Get current state (read-only).
animation_tree.get("parameters/OneShot/active")
# Alternative syntax (same result as above).
animation_tree["parameters/OneShot/active"]

# Get current internal state (read-only).
animation_tree.get("parameters/OneShot/internal_active")
# Alternative syntax (same result as above).
animation_tree["parameters/OneShot/internal_active"]
```

Example 2 (swift):
```swift
// Play child animation connected to "shot" port.
animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.Fire);

// Abort child animation connected to "shot" port.
animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.Abort);

// Abort child animation with fading out connected to "shot" port.
animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.FadeOut);

// Get current state (read-only).
animationTree.Get("parameters/OneShot/active");

// Get current internal state (read-only).
animationTree.Get("parameters/OneShot/internal_active");
```

---

## AnimationNodeOutput

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodeoutput.html

**Contents:**
- AnimationNodeOutput
- Description
- Tutorials
- User-contributed notes

Inherits: AnimationNode < Resource < RefCounted < Object

The animation output node of an AnimationNodeBlendTree.

A node created automatically in an AnimationNodeBlendTree that outputs the final animation.

Third Person Shooter (TPS) Demo

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeTimeScale

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodetimescale.html

**Contents:**
- AnimationNodeTimeScale
- Description
- Tutorials
- User-contributed notes

Inherits: AnimationNode < Resource < RefCounted < Object

A time-scaling animation node used in AnimationTree.

Allows to scale the speed of the animation (or reverse it) in any child AnimationNodes. Setting it to 0.0 will pause the animation.

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationNodeTimeSeek

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodetimeseek.html

**Contents:**
- AnimationNodeTimeSeek
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: AnimationNode < Resource < RefCounted < Object

A time-seeking animation node used in AnimationTree.

This animation node can be used to cause a seek command to happen to any sub-children of the animation graph. Use to play an Animation from the start or a certain playback position inside the AnimationNodeBlendTree.

After setting the time and changing the animation playback, the time seek node automatically goes into sleep mode on the next process frame by setting its seek_request value to -1.0.

bool explicit_elapse = true 

void set_explicit_elapse(value: bool)

bool is_explicit_elapse()

If true, some processes are executed to handle keys between seeks, such as calculating root motion and finding the nearest discrete key.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (sql):
```sql
# Play child animation from the start.
animation_tree.set("parameters/TimeSeek/seek_request", 0.0)
# Alternative syntax (same result as above).
animation_tree["parameters/TimeSeek/seek_request"] = 0.0

# Play child animation from 12 second timestamp.
animation_tree.set("parameters/TimeSeek/seek_request", 12.0)
# Alternative syntax (same result as above).
animation_tree["parameters/TimeSeek/seek_request"] = 12.0
```

Example 2 (sql):
```sql
// Play child animation from the start.
animationTree.Set("parameters/TimeSeek/seek_request", 0.0);

// Play child animation from 12 second timestamp.
animationTree.Set("parameters/TimeSeek/seek_request", 12.0);
```

---

## AnimationNodeTransition

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnodetransition.html

**Contents:**
- AnimationNodeTransition
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AnimationNodeSync < AnimationNode < Resource < RefCounted < Object

A transition within an AnimationTree connecting two AnimationNodes.

Simple state machine for cases which don't require a more advanced AnimationNodeStateMachine. Animations can be connected to the inputs and transition times can be specified.

After setting the request and changing the animation playback, the transition node automatically clears the request on the next process frame by setting its transition_request value to empty.

Note: When using a cross-fade, current_state and current_index change to the next state immediately after the cross-fade begins.

Third Person Shooter (TPS) Demo

allow_transition_to_self

is_input_loop_broken_at_end(input: int) const

is_input_reset(input: int) const

is_input_set_as_auto_advance(input: int) const

set_input_as_auto_advance(input: int, enable: bool)

set_input_break_loop_at_end(input: int, enable: bool)

set_input_reset(input: int, enable: bool)

bool allow_transition_to_self = false 

void set_allow_transition_to_self(value: bool)

bool is_allow_transition_to_self()

If true, allows transition to the self state. When the reset option is enabled in input, the animation is restarted. If false, nothing happens on the transition to the self state.

int input_count = 0 

void set_input_count(value: int)

int get_input_count()

The number of enabled input ports for this animation node.

void set_xfade_curve(value: Curve)

Curve get_xfade_curve()

Determines how cross-fading between animations is eased. If empty, the transition will be linear. Should be a unit Curve.

float xfade_time = 0.0 

void set_xfade_time(value: float)

float get_xfade_time()

Cross-fading time (in seconds) between each animation connected to the inputs.

Note: AnimationNodeTransition transitions the current state immediately after the start of the fading. The precise remaining time can only be inferred from the main animation. When AnimationNodeOutput is considered as the most upstream, so the xfade_time is not scaled depending on the downstream delta. See also AnimationNodeOneShot.fadeout_time.

bool is_input_loop_broken_at_end(input: int) const 

Returns whether the animation breaks the loop at the end of the loop cycle for transition.

bool is_input_reset(input: int) const 

Returns whether the animation restarts when the animation transitions from the other animation.

bool is_input_set_as_auto_advance(input: int) const 

Returns true if auto-advance is enabled for the given input index.

void set_input_as_auto_advance(input: int, enable: bool) 

Enables or disables auto-advance for the given input index. If enabled, state changes to the next input after playing the animation once. If enabled for the last input state, it loops to the first.

void set_input_break_loop_at_end(input: int, enable: bool) 

If true, breaks the loop at the end of the loop cycle for transition, even if the animation is looping.

void set_input_reset(input: int, enable: bool) 

If true, the destination animation is restarted when the animation transitions.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (markdown):
```markdown
# Play child animation connected to "state_2" port.
animation_tree.set("parameters/Transition/transition_request", "state_2")
# Alternative syntax (same result as above).
animation_tree["parameters/Transition/transition_request"] = "state_2"

# Get current state name (read-only).
animation_tree.get("parameters/Transition/current_state")
# Alternative syntax (same result as above).
animation_tree["parameters/Transition/current_state"]

# Get current state index (read-only).
animation_tree.get("parameters/Transition/current_index")
# Alternative syntax (same result as above).
animation_tree["parameters/Transition/current_index"]
```

Example 2 (unknown):
```unknown
// Play child animation connected to "state_2" port.
animationTree.Set("parameters/Transition/transition_request", "state_2");

// Get current state name (read-only).
animationTree.Get("parameters/Transition/current_state");

// Get current state index (read-only).
animationTree.Get("parameters/Transition/current_index");
```

---

## AnimationNode

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationnode.html

**Contents:**
- AnimationNode
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: AnimationNodeExtension, AnimationNodeOutput, AnimationNodeSync, AnimationNodeTimeScale, AnimationNodeTimeSeek, AnimationRootNode

Base class for AnimationTree nodes. Not related to scene nodes.

Base resource for AnimationTree nodes. In general, it's not used directly, but you can create custom ones with custom blending formulas.

Inherit this when creating animation nodes mainly for use in AnimationNodeBlendTree, otherwise AnimationRootNode should be used instead.

You can access the time information as read-only parameter which is processed and stored in the previous frame for all nodes except AnimationNodeOutput.

Note: If multiple inputs exist in the AnimationNode, which time information takes precedence depends on the type of AnimationNode.

_get_caption() virtual const

_get_child_by_name(name: StringName) virtual const

_get_child_nodes() virtual const

_get_parameter_default_value(parameter: StringName) virtual const

_get_parameter_list() virtual const

_has_filter() virtual const

_is_parameter_read_only(parameter: StringName) virtual const

_process(time: float, seek: bool, is_external_seeking: bool, test_only: bool) virtual

add_input(name: String)

blend_animation(animation: StringName, time: float, delta: float, seeked: bool, is_external_seeking: bool, blend: float, looped_flag: LoopedFlag = 0)

blend_input(input_index: int, time: float, seek: bool, is_external_seeking: bool, blend: float, filter: FilterAction = 0, sync: bool = true, test_only: bool = false)

blend_node(name: StringName, node: AnimationNode, time: float, seek: bool, is_external_seeking: bool, blend: float, filter: FilterAction = 0, sync: bool = true, test_only: bool = false)

find_input(name: String) const

get_input_count() const

get_input_name(input: int) const

get_parameter(name: StringName) const

get_processing_animation_tree_instance_id() const

is_path_filtered(path: NodePath) const

is_process_testing() const

remove_input(index: int)

set_filter_path(path: NodePath, enable: bool)

set_input_name(input: int, name: String)

set_parameter(name: StringName, value: Variant)

animation_node_removed(object_id: int, name: String) 

Emitted by nodes that inherit from this class and that have an internal tree when one of their animation nodes removes. The animation nodes that emit this signal are AnimationNodeBlendSpace1D, AnimationNodeBlendSpace2D, AnimationNodeStateMachine, and AnimationNodeBlendTree.

animation_node_renamed(object_id: int, old_name: String, new_name: String) 

Emitted by nodes that inherit from this class and that have an internal tree when one of their animation node names changes. The animation nodes that emit this signal are AnimationNodeBlendSpace1D, AnimationNodeBlendSpace2D, AnimationNodeStateMachine, and AnimationNodeBlendTree.

Emitted by nodes that inherit from this class and that have an internal tree when one of their animation nodes changes. The animation nodes that emit this signal are AnimationNodeBlendSpace1D, AnimationNodeBlendSpace2D, AnimationNodeStateMachine, AnimationNodeBlendTree and AnimationNodeTransition.

FilterAction FILTER_IGNORE = 0

Do not use filtering.

FilterAction FILTER_PASS = 1

Paths matching the filter will be allowed to pass.

FilterAction FILTER_STOP = 2

Paths matching the filter will be discarded.

FilterAction FILTER_BLEND = 3

Paths matching the filter will be blended (by the blend value).

bool filter_enabled 

void set_filter_enabled(value: bool)

bool is_filter_enabled()

If true, filtering is enabled.

String _get_caption() virtual const 

When inheriting from AnimationRootNode, implement this virtual method to override the text caption for this animation node.

AnimationNode _get_child_by_name(name: StringName) virtual const 

When inheriting from AnimationRootNode, implement this virtual method to return a child animation node by its name.

Dictionary _get_child_nodes() virtual const 

When inheriting from AnimationRootNode, implement this virtual method to return all child animation nodes in order as a name: node dictionary.

Variant _get_parameter_default_value(parameter: StringName) virtual const 

When inheriting from AnimationRootNode, implement this virtual method to return the default value of a parameter. Parameters are custom local memory used for your animation nodes, given a resource can be reused in multiple trees.

Array _get_parameter_list() virtual const 

When inheriting from AnimationRootNode, implement this virtual method to return a list of the properties on this animation node. Parameters are custom local memory used for your animation nodes, given a resource can be reused in multiple trees. Format is similar to Object.get_property_list().

bool _has_filter() virtual const 

When inheriting from AnimationRootNode, implement this virtual method to return whether the blend tree editor should display filter editing on this animation node.

bool _is_parameter_read_only(parameter: StringName) virtual const 

When inheriting from AnimationRootNode, implement this virtual method to return whether the parameter is read-only. Parameters are custom local memory used for your animation nodes, given a resource can be reused in multiple trees.

float _process(time: float, seek: bool, is_external_seeking: bool, test_only: bool) virtual 

Deprecated: Currently this is mostly useless as there is a lack of many APIs to extend AnimationNode by GDScript. It is planned that a more flexible API using structures will be provided in the future.

When inheriting from AnimationRootNode, implement this virtual method to run some code when this animation node is processed. The time parameter is a relative delta, unless seek is true, in which case it is absolute.

Here, call the blend_input(), blend_node() or blend_animation() functions. You can also use get_parameter() and set_parameter() to modify local memory.

This function should return the delta.

bool add_input(name: String) 

Adds an input to the animation node. This is only useful for animation nodes created for use in an AnimationNodeBlendTree. If the addition fails, returns false.

void blend_animation(animation: StringName, time: float, delta: float, seeked: bool, is_external_seeking: bool, blend: float, looped_flag: LoopedFlag = 0) 

Blends an animation by blend amount (name must be valid in the linked AnimationPlayer). A time and delta may be passed, as well as whether seeked happened.

A looped_flag is used by internal processing immediately after the loop.

float blend_input(input_index: int, time: float, seek: bool, is_external_seeking: bool, blend: float, filter: FilterAction = 0, sync: bool = true, test_only: bool = false) 

Blends an input. This is only useful for animation nodes created for an AnimationNodeBlendTree. The time parameter is a relative delta, unless seek is true, in which case it is absolute. A filter mode may be optionally passed.

float blend_node(name: StringName, node: AnimationNode, time: float, seek: bool, is_external_seeking: bool, blend: float, filter: FilterAction = 0, sync: bool = true, test_only: bool = false) 

Blend another animation node (in case this animation node contains child animation nodes). This function is only useful if you inherit from AnimationRootNode instead, otherwise editors will not display your animation node for addition.

int find_input(name: String) const 

Returns the input index which corresponds to name. If not found, returns -1.

int get_input_count() const 

Amount of inputs in this animation node, only useful for animation nodes that go into AnimationNodeBlendTree.

String get_input_name(input: int) const 

Gets the name of an input by index.

Variant get_parameter(name: StringName) const 

Gets the value of a parameter. Parameters are custom local memory used for your animation nodes, given a resource can be reused in multiple trees.

int get_processing_animation_tree_instance_id() const 

Returns the object id of the AnimationTree that owns this node.

Note: This method should only be called from within the AnimationNodeExtension._process_animation_node() method, and will return an invalid id otherwise.

bool is_path_filtered(path: NodePath) const 

Returns true if the given path is filtered.

bool is_process_testing() const 

Returns true if this animation node is being processed in test-only mode.

void remove_input(index: int) 

Removes an input, call this only when inactive.

void set_filter_path(path: NodePath, enable: bool) 

Adds or removes a path for the filter.

bool set_input_name(input: int, name: String) 

Sets the name of the input at the given input index. If the setting fails, returns false.

void set_parameter(name: StringName, value: Variant) 

Sets a custom parameter. These are used as local memory, because resources can be reused across the tree or scenes.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var current_length = $AnimationTree["parameters/AnimationNodeName/current_length"]
var current_position = $AnimationTree["parameters/AnimationNodeName/current_position"]
var current_delta = $AnimationTree["parameters/AnimationNodeName/current_delta"]
```

---

## AnimationPlayer

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationplayer.html

**Contents:**
- AnimationPlayer
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AnimationMixer < Node < Object

A node used for animation playback.

An animation player is used for general-purpose playback of animations. It contains a dictionary of AnimationLibrary resources and custom blend times between animation transitions.

Some methods and properties use a single key to reference an animation directly. These keys are formatted as the key for the library, followed by a forward slash, then the key for the animation within the library, for example "movement/run". If the library's key is an empty string (known as the default library), the forward slash is omitted, being the same key used by the library.

AnimationPlayer is better-suited than Tween for more complex animations, for example ones with non-trivial timings. It can also be used over Tween if the animation track editor is more convenient than doing it in code.

Updating the target properties of animations occurs at the process frame.

Animation documentation index

Third Person Shooter (TPS) Demo

current_animation_length

current_animation_position

playback_auto_capture

playback_auto_capture_duration

playback_auto_capture_ease_type

playback_auto_capture_transition_type

playback_default_blend_time

animation_get_next(animation_from: StringName) const

animation_set_next(animation_from: StringName, animation_to: StringName)

get_blend_time(animation_from: StringName, animation_to: StringName) const

AnimationMethodCallMode

get_method_call_mode() const

get_playing_speed() const

AnimationProcessCallback

get_process_callback() const

get_section_end_time() const

get_section_start_time() const

play(name: StringName = &"", custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false)

play_backwards(name: StringName = &"", custom_blend: float = -1)

play_section(name: StringName = &"", start_time: float = -1, end_time: float = -1, custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false)

play_section_backwards(name: StringName = &"", start_time: float = -1, end_time: float = -1, custom_blend: float = -1)

play_section_with_markers(name: StringName = &"", start_marker: StringName = &"", end_marker: StringName = &"", custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false)

play_section_with_markers_backwards(name: StringName = &"", start_marker: StringName = &"", end_marker: StringName = &"", custom_blend: float = -1)

play_with_capture(name: StringName = &"", duration: float = -1.0, custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false, trans_type: TransitionType = 0, ease_type: EaseType = 0)

queue(name: StringName)

seek(seconds: float, update: bool = false, update_only: bool = false)

set_blend_time(animation_from: StringName, animation_to: StringName, sec: float)

set_method_call_mode(mode: AnimationMethodCallMode)

set_process_callback(mode: AnimationProcessCallback)

set_root(path: NodePath)

set_section(start_time: float = -1, end_time: float = -1)

set_section_with_markers(start_marker: StringName = &"", end_marker: StringName = &"")

stop(keep_state: bool = false)

animation_changed(old_name: StringName, new_name: StringName) 

Emitted when a queued animation plays after the previous animation finished. See also queue().

Note: The signal is not emitted when the animation is changed via play() or by an AnimationTree.

current_animation_changed(name: String) 

Emitted when current_animation changes.

enum AnimationProcessCallback: 

AnimationProcessCallback ANIMATION_PROCESS_PHYSICS = 0

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS.

AnimationProcessCallback ANIMATION_PROCESS_IDLE = 1

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_IDLE.

AnimationProcessCallback ANIMATION_PROCESS_MANUAL = 2

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_MANUAL.

enum AnimationMethodCallMode: 

AnimationMethodCallMode ANIMATION_METHOD_CALL_DEFERRED = 0

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_METHOD_DEFERRED.

AnimationMethodCallMode ANIMATION_METHOD_CALL_IMMEDIATE = 1

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_METHOD_IMMEDIATE.

String assigned_animation 

void set_assigned_animation(value: String)

String get_assigned_animation()

If playing, the current animation's key, otherwise, the animation last played. When set, this changes the animation, but will not play it unless already playing. See also current_animation.

String autoplay = "" 

void set_autoplay(value: String)

String get_autoplay()

The key of the animation to play when the scene loads.

String current_animation = "" 

void set_current_animation(value: String)

String get_current_animation()

The key of the currently playing animation. If no animation is playing, the property's value is an empty string. Changing this value does not restart the animation. See play() for more information on playing animations.

Note: While this property appears in the Inspector, it's not meant to be edited, and it's not saved in the scene. This property is mainly used to get the currently playing animation, and internally for animation playback tracks. For more information, see Animation.

float current_animation_length 

float get_current_animation_length()

The length (in seconds) of the currently playing animation.

float current_animation_position 

float get_current_animation_position()

The position (in seconds) of the currently playing animation.

bool movie_quit_on_finish = false 

void set_movie_quit_on_finish_enabled(value: bool)

bool is_movie_quit_on_finish_enabled()

If true and the engine is running in Movie Maker mode (see MovieWriter), exits the engine with SceneTree.quit() as soon as an animation is done playing in this AnimationPlayer. A message is printed when the engine quits for this reason.

Note: This obeys the same logic as the AnimationMixer.animation_finished signal, so it will not quit the engine if the animation is set to be looping.

bool playback_auto_capture = true 

void set_auto_capture(value: bool)

bool is_auto_capture()

If true, performs AnimationMixer.capture() before playback automatically. This means just play_with_capture() is executed with default arguments instead of play().

Note: Capture interpolation is only performed if the animation contains a capture track. See also Animation.UPDATE_CAPTURE.

float playback_auto_capture_duration = -1.0 

void set_auto_capture_duration(value: float)

float get_auto_capture_duration()

See also play_with_capture() and AnimationMixer.capture().

If playback_auto_capture_duration is negative value, the duration is set to the interval between the current position and the first key.

EaseType playback_auto_capture_ease_type = 0 

void set_auto_capture_ease_type(value: EaseType)

EaseType get_auto_capture_ease_type()

The ease type of the capture interpolation. See also EaseType.

TransitionType playback_auto_capture_transition_type = 0 

void set_auto_capture_transition_type(value: TransitionType)

TransitionType get_auto_capture_transition_type()

The transition type of the capture interpolation. See also TransitionType.

float playback_default_blend_time = 0.0 

void set_default_blend_time(value: float)

float get_default_blend_time()

The default time in which to blend animations. Ranges from 0 to 4096 with 0.01 precision.

float speed_scale = 1.0 

void set_speed_scale(value: float)

float get_speed_scale()

The speed scaling ratio. For example, if this value is 1, then the animation plays at normal speed. If it's 0.5, then it plays at half speed. If it's 2, then it plays at double speed.

If set to a negative value, the animation is played in reverse. If set to 0, the animation will not advance.

StringName animation_get_next(animation_from: StringName) const 

Returns the key of the animation which is queued to play after the animation_from animation.

void animation_set_next(animation_from: StringName, animation_to: StringName) 

Triggers the animation_to animation when the animation_from animation completes.

Clears all queued, unplayed animations.

float get_blend_time(animation_from: StringName, animation_to: StringName) const 

Returns the blend time (in seconds) between two animations, referenced by their keys.

AnimationMethodCallMode get_method_call_mode() const 

Deprecated: Use AnimationMixer.callback_mode_method instead.

Returns the call mode used for "Call Method" tracks.

float get_playing_speed() const 

Returns the actual playing speed of current animation or 0 if not playing. This speed is the speed_scale property multiplied by custom_speed argument specified when calling the play() method.

Returns a negative value if the current animation is playing backwards.

AnimationProcessCallback get_process_callback() const 

Deprecated: Use AnimationMixer.callback_mode_process instead.

Returns the process notification in which to update animations.

PackedStringArray get_queue() 

Returns a list of the animation keys that are currently queued to play.

NodePath get_root() const 

Deprecated: Use AnimationMixer.root_node instead.

Returns the node which node path references will travel from.

float get_section_end_time() const 

Returns the end time of the section currently being played.

float get_section_start_time() const 

Returns the start time of the section currently being played.

bool has_section() const 

Returns true if an animation is currently playing with a section.

bool is_playing() const 

Returns true if an animation is currently playing (even if speed_scale and/or custom_speed are 0).

Pauses the currently playing animation. The current_animation_position will be kept and calling play() or play_backwards() without arguments or with the same animation name as assigned_animation will resume the animation.

void play(name: StringName = &"", custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false) 

Plays the animation with key name. Custom blend times and speed can be set.

The from_end option only affects when switching to a new animation track, or if the same track but at the start or end. It does not affect resuming playback that was paused in the middle of an animation. If custom_speed is negative and from_end is true, the animation will play backwards (which is equivalent to calling play_backwards()).

The AnimationPlayer keeps track of its current or last played animation with assigned_animation. If this method is called with that same animation name, or with no name parameter, the assigned animation will resume playing if it was paused.

Note: The animation will be updated the next time the AnimationPlayer is processed. If other variables are updated at the same time this is called, they may be updated too early. To perform the update immediately, call advance(0).

void play_backwards(name: StringName = &"", custom_blend: float = -1) 

Plays the animation with key name in reverse.

This method is a shorthand for play() with custom_speed = -1.0 and from_end = true, so see its description for more information.

void play_section(name: StringName = &"", start_time: float = -1, end_time: float = -1, custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false) 

Plays the animation with key name and the section starting from start_time and ending on end_time. See also play().

Setting start_time to a value outside the range of the animation means the start of the animation will be used instead, and setting end_time to a value outside the range of the animation means the end of the animation will be used instead. start_time cannot be equal to end_time.

void play_section_backwards(name: StringName = &"", start_time: float = -1, end_time: float = -1, custom_blend: float = -1) 

Plays the animation with key name and the section starting from start_time and ending on end_time in reverse.

This method is a shorthand for play_section() with custom_speed = -1.0 and from_end = true, see its description for more information.

void play_section_with_markers(name: StringName = &"", start_marker: StringName = &"", end_marker: StringName = &"", custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false) 

Plays the animation with key name and the section starting from start_marker and ending on end_marker.

If the start marker is empty, the section starts from the beginning of the animation. If the end marker is empty, the section ends on the end of the animation. See also play().

void play_section_with_markers_backwards(name: StringName = &"", start_marker: StringName = &"", end_marker: StringName = &"", custom_blend: float = -1) 

Plays the animation with key name and the section starting from start_marker and ending on end_marker in reverse.

This method is a shorthand for play_section_with_markers() with custom_speed = -1.0 and from_end = true, see its description for more information.

void play_with_capture(name: StringName = &"", duration: float = -1.0, custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false, trans_type: TransitionType = 0, ease_type: EaseType = 0) 

See also AnimationMixer.capture().

You can use this method to use more detailed options for capture than those performed by playback_auto_capture. When playback_auto_capture is false, this method is almost the same as the following:

If name is blank, it specifies assigned_animation.

If duration is a negative value, the duration is set to the interval between the current position and the first key, when from_end is true, uses the interval between the current position and the last key instead.

Note: The duration takes speed_scale into account, but custom_speed does not, because the capture cache is interpolated with the blend result and the result may contain multiple animations.

void queue(name: StringName) 

Queues an animation for playback once the current animation and all previously queued animations are done.

Note: If a looped animation is currently playing, the queued animation will never play unless the looped animation is stopped somehow.

void reset_section() 

Resets the current section. Does nothing if a section has not been set.

void seek(seconds: float, update: bool = false, update_only: bool = false) 

Seeks the animation to the seconds point in time (in seconds). If update is true, the animation updates too, otherwise it updates at process time. Events between the current frame and seconds are skipped.

If update_only is true, the method / audio / animation playback tracks will not be processed.

Note: Seeking to the end of the animation doesn't emit AnimationMixer.animation_finished. If you want to skip animation and emit the signal, use AnimationMixer.advance().

void set_blend_time(animation_from: StringName, animation_to: StringName, sec: float) 

Specifies a blend time (in seconds) between two animations, referenced by their keys.

void set_method_call_mode(mode: AnimationMethodCallMode) 

Deprecated: Use AnimationMixer.callback_mode_method instead.

Sets the call mode used for "Call Method" tracks.

void set_process_callback(mode: AnimationProcessCallback) 

Deprecated: Use AnimationMixer.callback_mode_process instead.

Sets the process notification in which to update animations.

void set_root(path: NodePath) 

Deprecated: Use AnimationMixer.root_node instead.

Sets the node which node path references will travel from.

void set_section(start_time: float = -1, end_time: float = -1) 

Changes the start and end times of the section being played. The current playback position will be clamped within the new section. See also play_section().

void set_section_with_markers(start_marker: StringName = &"", end_marker: StringName = &"") 

Changes the start and end markers of the section being played. The current playback position will be clamped within the new section. See also play_section_with_markers().

If the argument is empty, the section uses the beginning or end of the animation. If both are empty, it means that the section is not set.

void stop(keep_state: bool = false) 

Stops the currently playing animation. The animation position is reset to 0 and the custom_speed is reset to 1.0. See also pause().

If keep_state is true, the animation state is not updated visually.

Note: The method / audio / animation playback tracks will not be processed by this method.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
capture(name, duration, trans_type, ease_type)
play(name, custom_blend, custom_speed, from_end)
```

---

## AnimationRootNode

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationrootnode.html

**Contents:**
- AnimationRootNode
- Description
- Tutorials
- User-contributed notes

Inherits: AnimationNode < Resource < RefCounted < Object

Inherited By: AnimationNodeAnimation, AnimationNodeBlendSpace1D, AnimationNodeBlendSpace2D, AnimationNodeBlendTree, AnimationNodeStateMachine

Base class for AnimationNodes that hold one or multiple composite animations. Usually used for AnimationTree.tree_root.

AnimationRootNode is a base class for AnimationNodes that hold a complete animation. A complete animation refers to the output of an AnimationNodeOutput in an AnimationNodeBlendTree or the output of another AnimationRootNode. Used for AnimationTree.tree_root or in other AnimationRootNodes.

Examples of built-in root nodes include AnimationNodeBlendTree (allows blending nodes between each other using various modes), AnimationNodeStateMachine (allows to configure blending and transitions between nodes using a state machine pattern), AnimationNodeBlendSpace2D (allows linear blending between three AnimationNodes), AnimationNodeBlendSpace1D (allows linear blending only between two AnimationNodes).

Please read the User-contributed notes policy before submitting a comment.

---

## AnimationTree

**URL:** https://docs.godotengine.org/en/stable/classes/class_animationtree.html

**Contents:**
- AnimationTree
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AnimationMixer < Node < Object

A node used for advanced animation transitions in an AnimationPlayer.

A node used for advanced animation transitions in an AnimationPlayer.

Note: When linked with an AnimationPlayer, several properties and methods of the corresponding AnimationPlayer will not function as expected. Playback and transitions should be handled using only the AnimationTree and its constituent AnimationNode(s). The AnimationPlayer node should be used solely for adding, deleting, and editing animations.

Third Person Shooter (TPS) Demo

advance_expression_base_node

AnimationCallbackModeDiscrete

callback_mode_discrete

2 (overrides AnimationMixer)

true (overrides AnimationMixer)

AnimationProcessCallback

get_process_callback() const

set_process_callback(mode: AnimationProcessCallback)

animation_player_changed() 

Emitted when the anim_player is changed.

enum AnimationProcessCallback: 

AnimationProcessCallback ANIMATION_PROCESS_PHYSICS = 0

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS.

AnimationProcessCallback ANIMATION_PROCESS_IDLE = 1

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_IDLE.

AnimationProcessCallback ANIMATION_PROCESS_MANUAL = 2

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_MANUAL.

NodePath advance_expression_base_node = NodePath(".") 

void set_advance_expression_base_node(value: NodePath)

NodePath get_advance_expression_base_node()

The path to the Node used to evaluate the AnimationNode Expression if one is not explicitly specified internally.

NodePath anim_player = NodePath("") 

void set_animation_player(value: NodePath)

NodePath get_animation_player()

The path to the AnimationPlayer used for animating.

AnimationRootNode tree_root 

void set_tree_root(value: AnimationRootNode)

AnimationRootNode get_tree_root()

The root animation node of this AnimationTree. See AnimationRootNode.

AnimationProcessCallback get_process_callback() const 

Deprecated: Use AnimationMixer.callback_mode_process instead.

Returns the process notification in which to update animations.

void set_process_callback(mode: AnimationProcessCallback) 

Deprecated: Use AnimationMixer.callback_mode_process instead.

Sets the process notification in which to update animations.

Please read the User-contributed notes policy before submitting a comment.

---

## Animation

**URL:** https://docs.godotengine.org/en/stable/classes/class_animation.html

**Contents:**
- Animation
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Holds data that can be used to animate anything in the engine.

This resource holds data that can be used to animate anything in the engine. Animations are divided into tracks and each track must be linked to a node. The state of that node can be changed through time, by adding timed keys (events) to the track.

Animations are just data containers, and must be added to nodes such as an AnimationPlayer to be played back. Animation tracks have different types, each with its own set of dedicated methods. Check TrackType to see available types.

Note: For 3D position/rotation/scale, using the dedicated TYPE_POSITION_3D, TYPE_ROTATION_3D and TYPE_SCALE_3D track types instead of TYPE_VALUE is recommended for performance reasons.

Animation documentation index

add_marker(name: StringName, time: float)

add_track(type: TrackType, at_position: int = -1)

animation_track_get_key_animation(track_idx: int, key_idx: int) const

animation_track_insert_key(track_idx: int, time: float, animation: StringName)

animation_track_set_key_animation(track_idx: int, key_idx: int, animation: StringName)

audio_track_get_key_end_offset(track_idx: int, key_idx: int) const

audio_track_get_key_start_offset(track_idx: int, key_idx: int) const

audio_track_get_key_stream(track_idx: int, key_idx: int) const

audio_track_insert_key(track_idx: int, time: float, stream: Resource, start_offset: float = 0, end_offset: float = 0)

audio_track_is_use_blend(track_idx: int) const

audio_track_set_key_end_offset(track_idx: int, key_idx: int, offset: float)

audio_track_set_key_start_offset(track_idx: int, key_idx: int, offset: float)

audio_track_set_key_stream(track_idx: int, key_idx: int, stream: Resource)

audio_track_set_use_blend(track_idx: int, enable: bool)

bezier_track_get_key_in_handle(track_idx: int, key_idx: int) const

bezier_track_get_key_out_handle(track_idx: int, key_idx: int) const

bezier_track_get_key_value(track_idx: int, key_idx: int) const

bezier_track_insert_key(track_idx: int, time: float, value: float, in_handle: Vector2 = Vector2(0, 0), out_handle: Vector2 = Vector2(0, 0))

bezier_track_interpolate(track_idx: int, time: float) const

bezier_track_set_key_in_handle(track_idx: int, key_idx: int, in_handle: Vector2, balanced_value_time_ratio: float = 1.0)

bezier_track_set_key_out_handle(track_idx: int, key_idx: int, out_handle: Vector2, balanced_value_time_ratio: float = 1.0)

bezier_track_set_key_value(track_idx: int, key_idx: int, value: float)

blend_shape_track_insert_key(track_idx: int, time: float, amount: float)

blend_shape_track_interpolate(track_idx: int, time_sec: float, backward: bool = false) const

compress(page_size: int = 8192, fps: int = 120, split_tolerance: float = 4.0)

copy_track(track_idx: int, to_animation: Animation)

find_track(path: NodePath, type: TrackType) const

get_marker_at_time(time: float) const

get_marker_color(name: StringName) const

get_marker_names() const

get_marker_time(name: StringName) const

get_next_marker(time: float) const

get_prev_marker(time: float) const

get_track_count() const

has_marker(name: StringName) const

method_track_get_name(track_idx: int, key_idx: int) const

method_track_get_params(track_idx: int, key_idx: int) const

optimize(allowed_velocity_err: float = 0.01, allowed_angular_err: float = 0.01, precision: int = 3)

position_track_insert_key(track_idx: int, time: float, position: Vector3)

position_track_interpolate(track_idx: int, time_sec: float, backward: bool = false) const

remove_marker(name: StringName)

remove_track(track_idx: int)

rotation_track_insert_key(track_idx: int, time: float, rotation: Quaternion)

rotation_track_interpolate(track_idx: int, time_sec: float, backward: bool = false) const

scale_track_insert_key(track_idx: int, time: float, scale: Vector3)

scale_track_interpolate(track_idx: int, time_sec: float, backward: bool = false) const

set_marker_color(name: StringName, color: Color)

track_find_key(track_idx: int, time: float, find_mode: FindMode = 0, limit: bool = false, backward: bool = false) const

track_get_interpolation_loop_wrap(track_idx: int) const

track_get_interpolation_type(track_idx: int) const

track_get_key_count(track_idx: int) const

track_get_key_time(track_idx: int, key_idx: int) const

track_get_key_transition(track_idx: int, key_idx: int) const

track_get_key_value(track_idx: int, key_idx: int) const

track_get_path(track_idx: int) const

track_get_type(track_idx: int) const

track_insert_key(track_idx: int, time: float, key: Variant, transition: float = 1)

track_is_compressed(track_idx: int) const

track_is_enabled(track_idx: int) const

track_is_imported(track_idx: int) const

track_move_down(track_idx: int)

track_move_to(track_idx: int, to_idx: int)

track_move_up(track_idx: int)

track_remove_key(track_idx: int, key_idx: int)

track_remove_key_at_time(track_idx: int, time: float)

track_set_enabled(track_idx: int, enabled: bool)

track_set_imported(track_idx: int, imported: bool)

track_set_interpolation_loop_wrap(track_idx: int, interpolation: bool)

track_set_interpolation_type(track_idx: int, interpolation: InterpolationType)

track_set_key_time(track_idx: int, key_idx: int, time: float)

track_set_key_transition(track_idx: int, key_idx: int, transition: float)

track_set_key_value(track_idx: int, key: int, value: Variant)

track_set_path(track_idx: int, path: NodePath)

track_swap(track_idx: int, with_idx: int)

value_track_get_update_mode(track_idx: int) const

value_track_interpolate(track_idx: int, time_sec: float, backward: bool = false) const

value_track_set_update_mode(track_idx: int, mode: UpdateMode)

TrackType TYPE_VALUE = 0

Value tracks set values in node properties, but only those which can be interpolated. For 3D position/rotation/scale, using the dedicated TYPE_POSITION_3D, TYPE_ROTATION_3D and TYPE_SCALE_3D track types instead of TYPE_VALUE is recommended for performance reasons.

TrackType TYPE_POSITION_3D = 1

3D position track (values are stored in Vector3s).

TrackType TYPE_ROTATION_3D = 2

3D rotation track (values are stored in Quaternions).

TrackType TYPE_SCALE_3D = 3

3D scale track (values are stored in Vector3s).

TrackType TYPE_BLEND_SHAPE = 4

TrackType TYPE_METHOD = 5

Method tracks call functions with given arguments per key.

TrackType TYPE_BEZIER = 6

Bezier tracks are used to interpolate a value using custom curves. They can also be used to animate sub-properties of vectors and colors (e.g. alpha value of a Color).

TrackType TYPE_AUDIO = 7

Audio tracks are used to play an audio stream with either type of AudioStreamPlayer. The stream can be trimmed and previewed in the animation.

TrackType TYPE_ANIMATION = 8

Animation tracks play animations in other AnimationPlayer nodes.

enum InterpolationType: 

InterpolationType INTERPOLATION_NEAREST = 0

No interpolation (nearest value).

InterpolationType INTERPOLATION_LINEAR = 1

Linear interpolation.

InterpolationType INTERPOLATION_CUBIC = 2

Cubic interpolation. This looks smoother than linear interpolation, but is more expensive to interpolate. Stick to INTERPOLATION_LINEAR for complex 3D animations imported from external software, even if it requires using a higher animation framerate in return.

InterpolationType INTERPOLATION_LINEAR_ANGLE = 3

Linear interpolation with shortest path rotation.

Note: The result value is always normalized and may not match the key value.

InterpolationType INTERPOLATION_CUBIC_ANGLE = 4

Cubic interpolation with shortest path rotation.

Note: The result value is always normalized and may not match the key value.

UpdateMode UPDATE_CONTINUOUS = 0

Update between keyframes and hold the value.

UpdateMode UPDATE_DISCRETE = 1

Update at the keyframes.

UpdateMode UPDATE_CAPTURE = 2

Same as UPDATE_CONTINUOUS but works as a flag to capture the value of the current object and perform interpolation in some methods. See also AnimationMixer.capture(), AnimationPlayer.playback_auto_capture, and AnimationPlayer.play_with_capture().

LoopMode LOOP_NONE = 0

At both ends of the animation, the animation will stop playing.

LoopMode LOOP_LINEAR = 1

At both ends of the animation, the animation will be repeated without changing the playback direction.

LoopMode LOOP_PINGPONG = 2

Repeats playback and reverse playback at both ends of the animation.

LoopedFlag LOOPED_FLAG_NONE = 0

This flag indicates that the animation proceeds without any looping.

LoopedFlag LOOPED_FLAG_END = 1

This flag indicates that the animation has reached the end of the animation and just after loop processed.

LoopedFlag LOOPED_FLAG_START = 2

This flag indicates that the animation has reached the start of the animation and just after loop processed.

FindMode FIND_MODE_NEAREST = 0

Finds the nearest time key.

FindMode FIND_MODE_APPROX = 1

Finds only the key with approximating the time.

FindMode FIND_MODE_EXACT = 2

Finds only the key with matching the time.

bool capture_included = false 

bool is_capture_included()

Returns true if the capture track is included. This is a cached readonly value for performance.

void set_length(value: float)

The total length of the animation (in seconds).

Note: Length is not delimited by the last key, as this one may be before or after the end to ensure correct interpolation and looping.

LoopMode loop_mode = 0 

void set_loop_mode(value: LoopMode)

LoopMode get_loop_mode()

Determines the behavior of both ends of the animation timeline during animation playback. This indicates whether and how the animation should be restarted, and is also used to correctly interpolate animation cycles.

float step = 0.033333335 

void set_step(value: float)

The animation step value.

void add_marker(name: StringName, time: float) 

Adds a marker to this Animation.

int add_track(type: TrackType, at_position: int = -1) 

Adds a track to the Animation.

StringName animation_track_get_key_animation(track_idx: int, key_idx: int) const 

Returns the animation name at the key identified by key_idx. The track_idx must be the index of an Animation Track.

int animation_track_insert_key(track_idx: int, time: float, animation: StringName) 

Inserts a key with value animation at the given time (in seconds). The track_idx must be the index of an Animation Track.

void animation_track_set_key_animation(track_idx: int, key_idx: int, animation: StringName) 

Sets the key identified by key_idx to value animation. The track_idx must be the index of an Animation Track.

float audio_track_get_key_end_offset(track_idx: int, key_idx: int) const 

Returns the end offset of the key identified by key_idx. The track_idx must be the index of an Audio Track.

End offset is the number of seconds cut off at the ending of the audio stream.

float audio_track_get_key_start_offset(track_idx: int, key_idx: int) const 

Returns the start offset of the key identified by key_idx. The track_idx must be the index of an Audio Track.

Start offset is the number of seconds cut off at the beginning of the audio stream.

Resource audio_track_get_key_stream(track_idx: int, key_idx: int) const 

Returns the audio stream of the key identified by key_idx. The track_idx must be the index of an Audio Track.

int audio_track_insert_key(track_idx: int, time: float, stream: Resource, start_offset: float = 0, end_offset: float = 0) 

Inserts an Audio Track key at the given time in seconds. The track_idx must be the index of an Audio Track.

stream is the AudioStream resource to play. start_offset is the number of seconds cut off at the beginning of the audio stream, while end_offset is at the ending.

bool audio_track_is_use_blend(track_idx: int) const 

Returns true if the track at track_idx will be blended with other animations.

void audio_track_set_key_end_offset(track_idx: int, key_idx: int, offset: float) 

Sets the end offset of the key identified by key_idx to value offset. The track_idx must be the index of an Audio Track.

void audio_track_set_key_start_offset(track_idx: int, key_idx: int, offset: float) 

Sets the start offset of the key identified by key_idx to value offset. The track_idx must be the index of an Audio Track.

void audio_track_set_key_stream(track_idx: int, key_idx: int, stream: Resource) 

Sets the stream of the key identified by key_idx to value stream. The track_idx must be the index of an Audio Track.

void audio_track_set_use_blend(track_idx: int, enable: bool) 

Sets whether the track will be blended with other animations. If true, the audio playback volume changes depending on the blend value.

Vector2 bezier_track_get_key_in_handle(track_idx: int, key_idx: int) const 

Returns the in handle of the key identified by key_idx. The track_idx must be the index of a Bezier Track.

Vector2 bezier_track_get_key_out_handle(track_idx: int, key_idx: int) const 

Returns the out handle of the key identified by key_idx. The track_idx must be the index of a Bezier Track.

float bezier_track_get_key_value(track_idx: int, key_idx: int) const 

Returns the value of the key identified by key_idx. The track_idx must be the index of a Bezier Track.

int bezier_track_insert_key(track_idx: int, time: float, value: float, in_handle: Vector2 = Vector2(0, 0), out_handle: Vector2 = Vector2(0, 0)) 

Inserts a Bezier Track key at the given time in seconds. The track_idx must be the index of a Bezier Track.

in_handle is the left-side weight of the added Bezier curve point, out_handle is the right-side one, while value is the actual value at this point.

float bezier_track_interpolate(track_idx: int, time: float) const 

Returns the interpolated value at the given time (in seconds). The track_idx must be the index of a Bezier Track.

void bezier_track_set_key_in_handle(track_idx: int, key_idx: int, in_handle: Vector2, balanced_value_time_ratio: float = 1.0) 

Sets the in handle of the key identified by key_idx to value in_handle. The track_idx must be the index of a Bezier Track.

void bezier_track_set_key_out_handle(track_idx: int, key_idx: int, out_handle: Vector2, balanced_value_time_ratio: float = 1.0) 

Sets the out handle of the key identified by key_idx to value out_handle. The track_idx must be the index of a Bezier Track.

void bezier_track_set_key_value(track_idx: int, key_idx: int, value: float) 

Sets the value of the key identified by key_idx to the given value. The track_idx must be the index of a Bezier Track.

int blend_shape_track_insert_key(track_idx: int, time: float, amount: float) 

Inserts a key in a given blend shape track. Returns the key index.

float blend_shape_track_interpolate(track_idx: int, time_sec: float, backward: bool = false) const 

Returns the interpolated blend shape value at the given time (in seconds). The track_idx must be the index of a blend shape track.

Clear the animation (clear all tracks and reset all).

void compress(page_size: int = 8192, fps: int = 120, split_tolerance: float = 4.0) 

Compress the animation and all its tracks in-place. This will make track_is_compressed() return true once called on this Animation. Compressed tracks require less memory to be played, and are designed to be used for complex 3D animations (such as cutscenes) imported from external 3D software. Compression is lossy, but the difference is usually not noticeable in real world conditions.

Note: Compressed tracks have various limitations (such as not being editable from the editor), so only use compressed animations if you actually need them.

void copy_track(track_idx: int, to_animation: Animation) 

Adds a new track to to_animation that is a copy of the given track from this animation.

int find_track(path: NodePath, type: TrackType) const 

Returns the index of the specified track. If the track is not found, return -1.

StringName get_marker_at_time(time: float) const 

Returns the name of the marker located at the given time.

Color get_marker_color(name: StringName) const 

Returns the given marker's color.

PackedStringArray get_marker_names() const 

Returns every marker in this Animation, sorted ascending by time.

float get_marker_time(name: StringName) const 

Returns the given marker's time.

StringName get_next_marker(time: float) const 

Returns the closest marker that comes after the given time. If no such marker exists, an empty string is returned.

StringName get_prev_marker(time: float) const 

Returns the closest marker that comes before the given time. If no such marker exists, an empty string is returned.

int get_track_count() const 

Returns the amount of tracks in the animation.

bool has_marker(name: StringName) const 

Returns true if this Animation contains a marker with the given name.

StringName method_track_get_name(track_idx: int, key_idx: int) const 

Returns the method name of a method track.

Array method_track_get_params(track_idx: int, key_idx: int) const 

Returns the arguments values to be called on a method track for a given key in a given track.

void optimize(allowed_velocity_err: float = 0.01, allowed_angular_err: float = 0.01, precision: int = 3) 

Optimize the animation and all its tracks in-place. This will preserve only as many keys as are necessary to keep the animation within the specified bounds.

int position_track_insert_key(track_idx: int, time: float, position: Vector3) 

Inserts a key in a given 3D position track. Returns the key index.

Vector3 position_track_interpolate(track_idx: int, time_sec: float, backward: bool = false) const 

Returns the interpolated position value at the given time (in seconds). The track_idx must be the index of a 3D position track.

void remove_marker(name: StringName) 

Removes the marker with the given name from this Animation.

void remove_track(track_idx: int) 

Removes a track by specifying the track index.

int rotation_track_insert_key(track_idx: int, time: float, rotation: Quaternion) 

Inserts a key in a given 3D rotation track. Returns the key index.

Quaternion rotation_track_interpolate(track_idx: int, time_sec: float, backward: bool = false) const 

Returns the interpolated rotation value at the given time (in seconds). The track_idx must be the index of a 3D rotation track.

int scale_track_insert_key(track_idx: int, time: float, scale: Vector3) 

Inserts a key in a given 3D scale track. Returns the key index.

Vector3 scale_track_interpolate(track_idx: int, time_sec: float, backward: bool = false) const 

Returns the interpolated scale value at the given time (in seconds). The track_idx must be the index of a 3D scale track.

void set_marker_color(name: StringName, color: Color) 

Sets the given marker's color.

int track_find_key(track_idx: int, time: float, find_mode: FindMode = 0, limit: bool = false, backward: bool = false) const 

Finds the key index by time in a given track. Optionally, only find it if the approx/exact time is given.

If limit is true, it does not return keys outside the animation range.

If backward is true, the direction is reversed in methods that rely on one directional processing.

For example, in case find_mode is FIND_MODE_NEAREST, if there is no key in the current position just after seeked, the first key found is retrieved by searching before the position, but if backward is true, the first key found is retrieved after the position.

bool track_get_interpolation_loop_wrap(track_idx: int) const 

Returns true if the track at track_idx wraps the interpolation loop. New tracks wrap the interpolation loop by default.

InterpolationType track_get_interpolation_type(track_idx: int) const 

Returns the interpolation type of a given track.

int track_get_key_count(track_idx: int) const 

Returns the number of keys in a given track.

float track_get_key_time(track_idx: int, key_idx: int) const 

Returns the time at which the key is located.

float track_get_key_transition(track_idx: int, key_idx: int) const 

Returns the transition curve (easing) for a specific key (see the built-in math function @GlobalScope.ease()).

Variant track_get_key_value(track_idx: int, key_idx: int) const 

Returns the value of a given key in a given track.

NodePath track_get_path(track_idx: int) const 

Gets the path of a track. For more information on the path format, see track_set_path().

TrackType track_get_type(track_idx: int) const 

Gets the type of a track.

int track_insert_key(track_idx: int, time: float, key: Variant, transition: float = 1) 

Inserts a generic key in a given track. Returns the key index.

bool track_is_compressed(track_idx: int) const 

Returns true if the track is compressed, false otherwise. See also compress().

bool track_is_enabled(track_idx: int) const 

Returns true if the track at index track_idx is enabled.

bool track_is_imported(track_idx: int) const 

Returns true if the given track is imported. Else, return false.

void track_move_down(track_idx: int) 

void track_move_to(track_idx: int, to_idx: int) 

Changes the index position of track track_idx to the one defined in to_idx.

void track_move_up(track_idx: int) 

void track_remove_key(track_idx: int, key_idx: int) 

Removes a key by index in a given track.

void track_remove_key_at_time(track_idx: int, time: float) 

Removes a key at time in a given track.

void track_set_enabled(track_idx: int, enabled: bool) 

Enables/disables the given track. Tracks are enabled by default.

void track_set_imported(track_idx: int, imported: bool) 

Sets the given track as imported or not.

void track_set_interpolation_loop_wrap(track_idx: int, interpolation: bool) 

If true, the track at track_idx wraps the interpolation loop.

void track_set_interpolation_type(track_idx: int, interpolation: InterpolationType) 

Sets the interpolation type of a given track.

void track_set_key_time(track_idx: int, key_idx: int, time: float) 

Sets the time of an existing key.

void track_set_key_transition(track_idx: int, key_idx: int, transition: float) 

Sets the transition curve (easing) for a specific key (see the built-in math function @GlobalScope.ease()).

void track_set_key_value(track_idx: int, key: int, value: Variant) 

Sets the value of an existing key.

void track_set_path(track_idx: int, path: NodePath) 

Sets the path of a track. Paths must be valid scene-tree paths to a node and must be specified starting from the AnimationMixer.root_node that will reproduce the animation. Tracks that control properties or bones must append their name after the path, separated by ":".

For example, "character/skeleton:ankle" or "character/mesh:transform/local".

void track_swap(track_idx: int, with_idx: int) 

Swaps the track track_idx's index position with the track with_idx.

UpdateMode value_track_get_update_mode(track_idx: int) const 

Returns the update mode of a value track.

Variant value_track_interpolate(track_idx: int, time_sec: float, backward: bool = false) const 

Returns the interpolated value at the given time (in seconds). The track_idx must be the index of a value track.

A backward mainly affects the direction of key retrieval of the track with UPDATE_DISCRETE converted by AnimationMixer.ANIMATION_CALLBACK_MODE_DISCRETE_FORCE_CONTINUOUS to match the result with track_find_key().

void value_track_set_update_mode(track_idx: int, mode: UpdateMode) 

Sets the update mode of a value track.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
# This creates an animation that makes the node "Enemy" move to the right by
# 100 pixels in 2.0 seconds.
var animation = Animation.new()
var track_index = animation.add_track(Animation.TYPE_VALUE)
animation.track_set_path(track_index, "Enemy:position:x")
animation.track_insert_key(track_index, 0.0, 0)
animation.track_insert_key(track_index, 2.0, 100)
animation.length = 2.0
```

Example 2 (gdscript):
```gdscript
// This creates an animation that makes the node "Enemy" move to the right by
// 100 pixels in 2.0 seconds.
var animation = new Animation();
int trackIndex = animation.AddTrack(Animation.TrackType.Value);
animation.TrackSetPath(trackIndex, "Enemy:position:x");
animation.TrackInsertKey(trackIndex, 0.0f, 0);
animation.TrackInsertKey(trackIndex, 2.0f, 100);
animation.Length = 2.0f;
```

---

## BoneMap

**URL:** https://docs.godotengine.org/en/stable/classes/class_bonemap.html

**Contents:**
- BoneMap
- Description
- Tutorials
- Properties
- Methods
- Signals
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Describes a mapping of bone names for retargeting Skeleton3D into common names defined by a SkeletonProfile.

This class contains a dictionary that uses a list of bone names in SkeletonProfile as key names.

By assigning the actual Skeleton3D bone name as the key value, it maps the Skeleton3D to the SkeletonProfile.

Retargeting 3D Skeletons

find_profile_bone_name(skeleton_bone_name: StringName) const

get_skeleton_bone_name(profile_bone_name: StringName) const

set_skeleton_bone_name(profile_bone_name: StringName, skeleton_bone_name: StringName)

This signal is emitted when change the key value in the BoneMap. This is used to validate mapping and to update BoneMap editor.

This signal is emitted when change the value in profile or change the reference of profile. This is used to update key names in the BoneMap and to redraw the BoneMap editor.

SkeletonProfile profile 

void set_profile(value: SkeletonProfile)

SkeletonProfile get_profile()

A SkeletonProfile of the mapping target. Key names in the BoneMap are synchronized with it.

StringName find_profile_bone_name(skeleton_bone_name: StringName) const 

Returns a profile bone name having skeleton_bone_name. If not found, an empty StringName will be returned.

In the retargeting process, the returned bone name is the bone name of the target skeleton.

StringName get_skeleton_bone_name(profile_bone_name: StringName) const 

Returns a skeleton bone name is mapped to profile_bone_name.

In the retargeting process, the returned bone name is the bone name of the source skeleton.

void set_skeleton_bone_name(profile_bone_name: StringName, skeleton_bone_name: StringName) 

Maps a skeleton bone name to profile_bone_name.

In the retargeting process, the setting bone name is the bone name of the source skeleton.

Please read the User-contributed notes policy before submitting a comment.

---

## CallbackTweener

**URL:** https://docs.godotengine.org/en/stable/classes/class_callbacktweener.html

**Contents:**
- CallbackTweener
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: Tweener < RefCounted < Object

Calls the specified method after optional delay.

CallbackTweener is used to call a method in a tweening sequence. See Tween.tween_callback() for more usage information.

The tweener will finish automatically if the callback's target object is freed.

Note: Tween.tween_callback() is the only correct way to create CallbackTweener. Any CallbackTweener created manually will not function correctly.

set_delay(delay: float)

CallbackTweener set_delay(delay: float) 

Makes the callback call delayed by given time in seconds.

Example: Call Node.queue_free() after 2 seconds:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var tween = get_tree().create_tween()
tween.tween_callback(queue_free).set_delay(2)
```

---

## Creating movies

**URL:** https://docs.godotengine.org/en/stable/tutorials/animation/creating_movies.html

**Contents:**
- Creating movies
- Enabling Movie Maker mode
  - Command line usage
- Choosing an output format
  - OGV (recommended)
  - AVI
  - PNG
  - Custom
- Configuration
- Quitting Movie Maker mode

Godot can record non-real-time video and audio from any 2D or 3D project. This kind of recording is also called offline rendering. There are many scenarios where this is useful:

Recording game trailers for promotional use.

Recording cutscenes that will be displayed as pre-recorded videos in the final game. This allows for using higher quality settings (at the cost of file size), regardless of the player's hardware.

Recording procedurally generated animations or motion design. User interaction remains possible during video recording, and audio can be included as well (although you won't be able to hear it while the video is recording).

Comparing the visual output of graphics settings, shaders, or rendering techniques in an animated scene.

With Godot's animation features such as the AnimationPlayer node, Tweeners, particles and shaders, it can effectively be used to create any kind of 2D and 3D animations (and still images).

If you are already used to Godot's workflow, you may find yourself more productive by using Godot for video rendering compared to Blender. That said, renderers designed for non-real-time usage such as Cycles and Eevee can result in better visuals (at the cost of longer rendering times).

Compared to real-time video recording, some advantages of non-real-time recording include:

Use any graphics settings (including extremely demanding settings) regardless of your hardware's capabilities. The output video will always have perfect frame pacing; it will never exhibit dropped frames or stuttering. Faster hardware will allow you to render a given animation in less time, but the visual output remains identical.

Render at a higher resolution than the screen resolution, without having to rely on driver-specific tools such as NVIDIA's Dynamic Super Resolution or AMD's Virtual Super Resolution.

Render at a higher framerate than the video's target framerate, then post-process to generate high-quality motion blur. This also makes effects that converge over several frames (such as temporal antialiasing, SDFGI and volumetric fog) look better.

This feature is not designed for capturing real-time footage during gameplay.

Players should use something like OBS Studio or SimpleScreenRecorder to record gameplay videos, as they do a much better job at intercepting the compositor than Godot can do using Vulkan or OpenGL natively.

That said, if your game runs at near-real-time speeds when capturing, you can still use this feature (but it will lack audible sound playback, as sound is saved directly to the video file).

To enable Movie Maker mode, click the "movie reel" button in the top-right corner of the editor before running the project:

Movie Maker mode is disabled, click the "movie reel" icon to enable

A menu will be displayed with options to enable Movie Maker mode and to go to the settings. The icon gets a background matching the accent color when Movie Maker mode is enabled:

Movie Maker mode is enabled, click the "movie reel" icon again to disable

Movie Maker status is not persisted when the editor quits, so you must re-enable Movie Maker mode again after restarting the editor if needed.

Toggling Movie Maker mode while running the project will not have any effect until the project is restarted.

Before you can record video by running the project, you still need to configure the output file path. This path can be set for all scenes in the Project Settings:

Movie Maker project settings (with Advanced toggle enabled)

Alternatively, you can set the output file path on a per-scene basis by adding a String metadata with the name movie_file to the scene's root node. This is only used when the main scene is set to the scene in question, or when running the scene directly by pressing F6 (Cmd + R on macOS).

Inspector view after creating a movie_file metadata of type String

The path specified in the project settings or metadata can be either absolute, or relative to the project root.

Once you've configured and enabled Movie Maker mode, it will be automatically used when running the project from the editor.

Movie Maker can also be enabled from the command line:

If the output path is relative, then it is relative to the project folder, not the current working directory. In the above example, the file will be written to /path/to/your_project/output.avi. This behavior is similar to the --export-release command line argument.

Since Movie Maker's output resolution is set by the viewport size, you can adjust the window size on startup to override it if the project uses the disabled or canvas_items stretch mode:

Note that the window size is clamped by your display's resolution. See Rendering at a higher resolution than the screen resolution if you need to record a video at a higher resolution than the screen resolution.

The recording FPS can also be overridden on the command line, without having to edit the Project Settings:

The --write-movie and --fixed-fps command line arguments are both available in exported projects. Movie Maker mode cannot be toggled while the project is running, but you can use the OS.execute() method to run a second instance of the exported project that will record a video file.

Output formats are provided by the MovieWriter class. Godot has 3 built-in MovieWriters, and more can be implemented by extensions:

OGV container with Theora for video and Vorbis for audio. Features lossy video and audio compression with a good balance of file size and encoding speed, with a better image quality than MJPEG. It has 4 speed levels that can be adjusted by changing Editor > Movie Writer > Encoding Speed with the fastest one being around as fast as AVI with better compression. At slower speed levels, it can compress even better while keeping the same image quality. The lossy compression quality can be adjusted by changing Editor > Movie Writer > Video Quality for video and Editor > Movie Writer > Audio Quality for audio.

The Keyframe Interval can be adjusted by changing Editor > Movie Writer > Keyframe Interval. In some cases, increasing this setting can improve compression efficiency without downsides.

The resulting file can be viewed in Godot with VideoStreamPlayer and most video players but not web browsers. OGV does not support transparency.

To use OGV, specify a path to a .ogv file to be created in the Editor > Movie Writer > Movie File project setting.

OGV can only be recorded in editor builds. On the other hand, OGV playback is possible in both editor and export template builds.

AVI container with MJPEG for video and uncompressed audio. Features lossy video compression, resulting in medium file sizes and fast encoding. The lossy compression quality can be adjusted by changing Editor > Movie Writer > Video Quality.

The resulting file can be viewed in most video players, but it must be converted to another format for viewing on the web or by Godot with the VideoStreamPlayer node. MJPEG does not support transparency. AVI output is currently limited to a file of 4 GB in size at most.

To use AVI, specify a path to a .avi file to be created in the Editor > Movie Writer > Movie File project setting.

PNG image sequence for video and WAV for audio. Features lossless video compression, at the cost of large file sizes and slow encoding. This is designed to be encoded to a video file with an external tool after recording.

Transparency is supported, but the root viewport must have its transparent_bg property set to true for transparency to be visible on the output image. This can be achieved by enabling the Rendering > Transparent Background advanced project setting. Display > Window > Size > Transparent and Display > Window > Per Pixel Transparency > Enabled can optionally be enabled to allow transparency to be previewed while recording the video, but they do not have to be enabled for the output image to contain transparency.

To use PNG, specify a .png file to be created in the Editor > Movie Writer > Movie File project setting. The generated .wav file will have the same name as the .png file (minus the extension).

If you need to encode directly to a different format or pipe a stream through third-party software, you can extend the MovieWriter class to create your own movie writers. This should typically be done using GDExtension for performance reasons.

In the Editor > Movie Writer section of the Project Settings, there are several options you can configure. Some of them are only visible after enabling the Advanced toggle in the top-right corner of the Project Settings dialog.

Mix Rate Hz: The audio mix rate to use in the recorded audio when writing a movie. This can be different from the project's mix rate, but this value must be divisible by the recorded FPS to prevent audio from desynchronizing over time.

Speaker Mode: The speaker mode to use in the recorded audio when writing a movie (stereo, 5.1 surround or 7.1 surround).

Video Quality: The image quality to use when writing a video to an OGV or AVI file, between 0.01 and 1.0 (inclusive). Higher quality values result in better-looking output at the cost of larger file sizes. Recommended quality values are between 0.75 and 0.9. Even at quality 1.0, compression remains lossy. This setting does not affect audio quality and is ignored when writing to a PNG image sequence.

Movie File: The output path for the movie. This can be absolute or relative to the project root.

Disable V-Sync: If enabled, requests V-Sync to be disabled when writing a movie. This can speed up video writing if the hardware is fast enough to render, encode and save the video at a framerate higher than the monitor's refresh rate. This setting has no effect if the operating system or graphics driver forces V-Sync with no way for applications to disable it.

FPS: The rendered frames per second in the output movie. Higher values result in smoother animation, at the cost of longer rendering times and larger output file sizes. Most video hosting platforms do not support FPS values higher than 60, but you can use a higher value and use that to generate motion blur.

Audio Quality: The audio quality to use when writing a video to an OGV file, between -0.1 and 1.0 (inclusive). Higher quality values result in better audio quality at the cost of very slightly larger file sizes. Recommended quality values are between 0.3 and 0.5. Even at quality 1.0, compression remains lossy.

Encoding Speed: The speed level to use when writing a video to an OGV file. Faster speed levels have less compression efficiency. The image quality stays barely the same.

Keyframe Interval: Also known as GOP (Group Of Pictures), the maximum number of inter-frames to use when writing to an OGV file. Higher values can improve compression efficiency without quality loss but at the cost of slower video seeks.

When using the disabled or 2d stretch modes, the output file's resolution is set by the window size. Make sure to resize the window before the splash screen has ended. For this purpose, it's recommended to adjust the Display > Window > Size > Window Width Override and Window Height Override advanced project settings.

See also Rendering at a higher resolution than the screen resolution.

To safely quit a project that is using Movie Maker mode, use the X button at the top of the window, or call get_tree().quit() in a script. You can also use the --quit-after N command line argument where N is the number of frames to render before quitting.

Pressing F8 (Cmd + . on macOS) or pressing Ctrl + C on the terminal running Godot is not recommended, as it will result in an improperly formatted AVI file with no duration information. For PNG image sequences, PNG images will not be negatively altered, but the associated WAV file will still lack duration information. OGV files might end up with slightly different duration video and audio tracks but still valid.

Some video players may still be able to play the AVI or WAV file with working video and audio. However, software that makes use of the AVI or WAV file such as video editors may not be able to open the file. Using a video converter program can help in those cases.

If you're using an AnimationPlayer to control a "main action" in the scene (such as camera movement), you can enable the Movie Quit On Finish property on the AnimationPlayer node in question. When enabled, this property will make Godot quit on its own when an animation is done playing and the engine is running in Movie Maker mode. Note that this property has no effect on looping animations. Therefore, you need to make sure that the animation is set as non-looping.

The movie feature tag can be used to override specific project settings. This is useful to enable high-quality graphics settings that wouldn't be fast enough to run in real-time speeds on your hardware. Remember that putting every setting to its maximum value can still slow down movie saving speed, especially when recording at higher resolutions. Therefore, it's still recommended to only increase graphics settings if they make a meaningful difference in the output image.

This feature tag can also be queried in a script to increase quality settings that are set in the Environment resource. For example, to further improve SDFGI detail and reduce light leaking:

The overall rendering quality can be improved significantly by rendering at high resolutions such as 4K or 8K.

For 3D rendering, Godot provides a Rendering > Scaling 3D > Scale advanced project setting, which can be set above 1.0 to obtain supersample antialiasing. The 3D rendering is then downsampled when it's drawn on the viewport. This provides an expensive but high-quality form of antialiasing, without increasing the final output resolution.

Consider using this project setting first, as it avoids slowing down movie writing speeds and increasing output file size compared to actually increasing the output resolution.

If you wish to render 2D at a higher resolution, or if you actually need the higher raw pixel output for 3D rendering, you can increase the resolution above what the screen allows.

By default, Godot uses the disabled stretch modes in projects. If using disabled or canvas_items stretch mode, the window size dictates the output video resolution.

On the other hand, if the project is configured to use the viewport stretch mode, the viewport resolution dictates the output video resolution. The viewport resolution is set using the Display > Window > Size > Viewport Width and Viewport Height project settings. This can be used to render a video at a higher resolution than the screen resolution.

To make the window smaller during recording without affecting the output video resolution, you can set the Display > Window > Size > Window Width Override and Window Height Override advanced project settings to values greater than 0.

To apply a resolution override only when recording a movie, you can override those settings with the movie feature tag.

Some common post-processing steps are listed below.

When using several post-processing steps, try to perform all of them in a single FFmpeg command. This will save encoding time and improve quality by avoiding multiple lossy encoding steps.

While some platforms such as YouTube support uploading the AVI file directly, many others will require a conversion step beforehand. HandBrake (GUI) and FFmpeg (CLI) are popular open source tools for this purpose. FFmpeg has a steeper learning curve, but it's more powerful.

The command below converts an OGV/AVI video to an MP4 (H.264) video with a Constant Rate Factor (CRF) of 15. This results in a relatively large file, but is well-suited for platforms that will re-encode your videos to reduce their size (such as most video sharing websites):

To get a smaller file at the cost of quality, increase the CRF value in the above command.

To get a file with a better size/quality ratio (at the cost of slower encoding times), add -preset veryslow before -crf 15 in the above command. On the contrary, -preset veryfast can be used to achieve faster encoding at the cost of a worse size/quality ratio.

If you chose to record a PNG image sequence with a WAV file beside it, you need to convert it to a video before you can use it elsewhere.

The filename for the PNG image sequence generated by Godot always contains 8 digits, starting at 0 with zero-padded numbers. If you specify an output path folder/example.png, Godot will write folder/example00000000.png, folder/example00000001.png, and so on in that folder. The audio will be saved at folder/example.wav.

The FPS is specified using the -r argument. It should match the FPS specified during recording. Otherwise, the video will appear to be slowed down or sped up, and audio will be out of sync with the video.

If you recorded a PNG image sequence with transparency enabled, you need to use a video format that supports storing transparency. MP4/H.264 doesn't support storing transparency, so you can use WebM/VP9 as an alternative:

You can trim parts of the video you don't want to keep after the video is recorded. For example, to discard everything before 12.1 seconds and keep only 5.2 seconds of video after that point:

Cutting videos can also be done with the GUI tool LosslessCut.

The following command resizes a video to be 1080 pixels tall (1080p), while preserving its existing aspect ratio:

The following command changes a video's framerate to 30 FPS, dropping some of the original frames if there are more in the input video:

Godot does not have built-in support for motion blur, but it can still be created in recorded videos.

If you record the video at a multiple of the original framerate, you can blend the frames together then reduce the frameate to produce a video with accumulation motion blur. This motion blur can look very good, but it can take a long time to generate since you have to render many more frames per second (on top of the time spent on post-processing).

Example with a 240 FPS source video, generating 4× motion blur and decreasing its output framerate to 60 FPS:

This also makes effects that converge over several frames (such as temporal antialiasing, SDFGI and volumetric fog) converge faster and therefore look better, since they'll be able to work with more data at a given time. See Reducing framerate if you want to get this benefit without adding motion blur.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
godot --path /path/to/your_project --write-movie output.avi
```

Example 2 (unknown):
```unknown
godot --path /path/to/your_project --write-movie output.avi --resolution 1280x720
```

Example 3 (unknown):
```unknown
godot --path /path/to/your_project --write-movie output.avi --fixed-fps 30
```

Example 4 (gdscript):
```gdscript
extends Node3D

func _ready():
    if OS.has_feature("movie"):
        # When recording a movie, improve SDFGI cell density
        # without decreasing its maximum distance.
        get_viewport().world_3d.environment.sdfgi_min_cell_size *= 0.25
        get_viewport().world_3d.environment.sdfgi_cascades = 8
```

---

## Cutout animation

**URL:** https://docs.godotengine.org/en/stable/tutorials/animation/cutout_animation.html

**Contents:**
- Cutout animation
- What is it?
- Cutout animation in Godot
- Making of GBot
- Setting up the rig
- Adjusting the pivot
- RemoteTransform2D node
- Completing the skeleton
- Skeletons
- IK chains

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

Traditionally, cutout animation is a type of stop motion animation in which pieces of paper (or other thin material) are cut into special shapes and arranged in two-dimensional representations of characters and objects. Characters' bodies are usually made out of several pieces. The pieces are arranged and photographed once for each frame of the film. The animator moves and rotates the parts in small increments between each shot to create the illusion of movement when the images are played back quickly in sequence.

Simulations of cutout animation can now be created using software as seen in South Park and Jake and the Never Land Pirates.

In video games, this technique has also become popular. Examples of this are Paper Mario or Rayman Origins .

Godot provides tools for working with cutout rigs, and is ideal for the workflow:

The animation system is fully integrated with the engine: This means animations can control much more than just motion of objects. Textures, sprite sizes, pivots, opacity, color modulation, and more, can all be animated and blended.

Combine animation styles: AnimatedSprite2D allows traditional cel animation to be used alongside cutout animation. In cel animation different animation frames use entirely different drawings rather than the same pieces positioned differently. In an otherwise cutout-based animation, cel animation can be used selectively for complex parts such as hands, feet, changing facial expressions, etc.

Custom Shaped Elements: Custom shapes can be created with Polygon2D allowing UV animation, deformations, etc.

Particle Systems: A cutout animation rig can be combined with particle systems. This can be useful for magic effects, jetpacks, etc.

Custom Colliders: Set colliders and influence areas in different parts of the skeletons, great for bosses and fighting games.

Animation Tree: Allows complex combinations and blending between several animations, the same way it works in 3D.

For this tutorial, we will use as demo content the pieces of the GBot character, created by Andreas Esau.

Get your assets: cutout_animation_assets.zip.

Create an empty Node2D as root of the scene, we will work under it:

The first node of the model is the hip. Generally, both in 2D and 3D, the hip is the root of the skeleton. This makes it easier to animate:

Next will be the torso. The torso needs to be a child of the hip, so create a child sprite and load the torso texture, later accommodate it properly:

This looks good. Let's see if our hierarchy works as a skeleton by rotating the torso. We can do this be pressing E to enter rotate mode, and dragging with the left mouse button. To exit rotate mode hit ESC.

The rotation pivot is wrong and needs to be adjusted.

This small cross in the middle of the Sprite2D is the rotation pivot:

The pivot can be adjusted by changing the offset property in the Sprite2D:

The pivot can also be adjusted visually. While hovering over the desired pivot point, press V to move the pivot there for the selected Sprite2D. There is also a tool in the tool bar that has a similar function.

Continue adding body pieces, starting with the right arm. Make sure to put each sprite in its correct place in the hierarchy, so its rotations and translations are relative to its parent:

With the left arm there's a problem. In 2D, child nodes appear in front of their parents:

We want the left arm to appear behind the hip and the torso. We could move the left arm nodes behind the hip (above the hip node in the scene hierarchy), but then the left arm is no longer in its proper place in the hierarchy. This means it wouldn't be affected by the movement of the torso. We'll fix this problem with RemoteTransform2D nodes.

You can also fix depth ordering problems by adjusting the Z property of any node inheriting from Node2D.

The RemoteTransform2D node transforms nodes somewhere else in the hierarchy. This node applies its own transform (including any transformation it inherits from its parents) to the remote node it targets.

This allows us to correct the visibility order of our elements, independently of the locations of those parts in the cutout hierarchy.

Create a RemoteTransform2D node as a child of the torso. Call it remote_arm_l. Create another RemoteTransform2D node inside the first and call it remote_hand_l. Use the Remote Path property of the two new nodes to target the arm_l and hand_l sprites respectively:

Moving the RemoteTransform2D nodes now moves the sprites. So we can create animations by adjusting the RemoteTransform2D transforms:

Complete the skeleton by following the same steps for the rest of the parts. The resulting scene should look similar to this:

The resulting rig will be easy to animate. By selecting the nodes and rotating them you can animate forward kinematics (FK) efficiently.

For simple objects and rigs this is fine, but there are limitations:

Selecting sprites in the main viewport can become difficult in complex rigs. The scene tree ends up being used to select parts instead, which can be slower.

Inverse Kinematics (IK) is useful for animating extremities like hands and feet, and can't be used with our rig in its current state.

To solve these problems we'll use Godot's skeletons.

In Godot there is a helper to create "bones" between nodes. The bone-linked nodes are called skeletons.

As an example, let's turn the right arm into a skeleton. To create a skeleton, a chain of nodes must be selected from top to bottom:

Then, click on the Skeleton menu and select Make Bones.

This will add bones covering the arm, but the result may be surprising.

Why does the hand lack a bone? In Godot, a bone connects a node with its parent. And there's currently no child of the hand node. With this knowledge let's try again.

The first step is creating an endpoint node. Any kind of node will do, but Marker2D is preferred because it's visible in the editor. The endpoint node will ensure that the last bone has orientation.

Now select the whole chain, from the endpoint to the arm and create bones:

The result resembles a skeleton a lot more, and now the arm and forearm can be selected and animated.

Create endpoints for all important extremities. Generate bones for all articulable parts of the cutout, with the hip as the ultimate connection between all of them.

You may notice that an extra bone is created when connecting the hip and torso. Godot has connected the hip node to the scene root with a bone, and we don't want that. To fix this, select the root and hip node, open the Skeleton menu, click clear bones.

Your final skeleton should look something like this:

You might have noticed a second set of endpoints in the hands. This will make sense soon.

Now that the whole figure is rigged, the next step is setting up the IK chains. IK chains allow for more natural control of extremities.

IK stands for inverse kinematics. It's a convenient technique for animating the position of hands, feet and other extremities of rigs like the one we've made. Imagine you want to pose a character's foot in a specific position on the ground. Without IK chains, each motion of the foot would require rotating and positioning several other bones (the shin and the thigh at least). This would be quite complex and lead to imprecise results. IK allows us to move the foot directly while the shin and thigh self-adjust.

IK chains in Godot currently work in the editor only, not at runtime. They are intended to ease the process of setting keyframes, and are not currently useful for techniques like procedural animation.

To create an IK chain, select a chain of bones from endpoint to the base for the chain. For example, to create an IK chain for the right leg, select the following:

Then enable this chain for IK. Go to Edit > Make IK Chain.

As a result, the base of the chain will turn Yellow.

Once the IK chain is set up, grab any child or grand-child of the base of the chain (e.g. a foot), and move it. You'll see the rest of the chain adjust as you adjust its position.

The following section will be a collection of tips for creating animation for your cutout rigs. For more information on how the animation system in Godot works, see Introduction to the animation features.

Special contextual elements appear in the top toolbar when the animation editor window is open:

The key button inserts location, rotation, and scale keyframes for the selected objects or bones at the current playhead position.

The "loc", "rot", and "scl" toggle buttons to the left of the key button modify its function, allowing you to specify which of the three properties keyframes will be created for.

Here's an illustration of how this can be useful: Imagine you have a node which already has two keyframes animating its scale only. You want to add an overlapping rotation movement to the same node. The rotation movement should begin and end at different times from the scale change that's already set up. You can use the toggle buttons to have only rotation information added when you add a new keyframe. This way, you can avoid adding unwanted scale keyframes which would disrupt the existing scale animation.

Think of a rest pose as a default pose that your cutout rig should be set to when no other pose is active in your game. Create a rest pose as follows:

1. Make sure the rig parts are positioned in what looks like a "resting" arrangement.

Create a new animation, rename it "rest".

Select all nodes in your rig (box selection should work fine).

4. Make sure the "loc", "rot", and "scl" toggle buttons are all active in the toolbar.

5. Press the key button. Keys will be inserted for all selected parts storing their current arrangement. This pose can now be recalled when necessary in your game by playing the "rest" animation you've created.

When animating a cutout rig, often it's only the rotation of the nodes that needs to change. Location and scale are rarely used.

So when inserting keys, you might find it convenient to have only the "rot" toggle active most of the time:

This will avoid the creation of unwanted animation tracks for position and scale.

When editing IK chains, it's not necessary to select the whole chain to add keyframes. Selecting the endpoint of the chain and inserting a keyframe will automatically insert keyframes for all other parts of the chain too.

Sometimes it is necessary to have a node change its visual depth relative to its parent node during an animation. Think of a character facing the camera, who pulls something out from behind his back and holds it out in front of him. During this animation the whole arm and the object in his hand would need to change their visual depth relative to the body of the character.

To help with this there's a keyframable "Behind Parent" property on all Node2D-inheriting nodes. When planning your rig, think about the movements it will need to perform and give some thought to how you'll use "Behind Parent" and/or RemoteTransform2D nodes. They provide overlapping functionality.

To apply the same easing curve to multiple keyframes at once:

Select the relevant keys.

Click on the pencil icon in the bottom right of the animation panel. This will open the transition editor.

In the transition editor, click on the desired curve to apply it.

Skeletal deform can be used to augment a cutout rig, allowing single pieces to deform organically (e.g. antennae that wobble as an insect character walks).

This process is described in a separate tutorial.

Please read the User-contributed notes policy before submitting a comment.

---

## IntervalTweener

**URL:** https://docs.godotengine.org/en/stable/classes/class_intervaltweener.html

**Contents:**
- IntervalTweener
- Description
- User-contributed notes

Inherits: Tweener < RefCounted < Object

Creates an idle interval in a Tween animation.

IntervalTweener is used to make delays in a tweening sequence. See Tween.tween_interval() for more usage information.

Note: Tween.tween_interval() is the only correct way to create IntervalTweener. Any IntervalTweener created manually will not function correctly.

Please read the User-contributed notes policy before submitting a comment.

---

## MethodTweener

**URL:** https://docs.godotengine.org/en/stable/classes/class_methodtweener.html

**Contents:**
- MethodTweener
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: Tweener < RefCounted < Object

Interpolates an abstract value and supplies it to a method called over time.

MethodTweener is similar to a combination of CallbackTweener and PropertyTweener. It calls a method providing an interpolated value as a parameter. See Tween.tween_method() for more usage information.

The tweener will finish automatically if the callback's target object is freed.

Note: Tween.tween_method() is the only correct way to create MethodTweener. Any MethodTweener created manually will not function correctly.

set_delay(delay: float)

set_ease(ease: EaseType)

set_trans(trans: TransitionType)

MethodTweener set_delay(delay: float) 

Sets the time in seconds after which the MethodTweener will start interpolating. By default there's no delay.

MethodTweener set_ease(ease: EaseType) 

Sets the type of used easing from EaseType. If not set, the default easing is used from the Tween that contains this Tweener.

MethodTweener set_trans(trans: TransitionType) 

Sets the type of used transition from TransitionType. If not set, the default transition is used from the Tween that contains this Tweener.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRHand

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrhand.html

**Contents:**
- OpenXRHand
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Deprecated: Use XRHandModifier3D instead.

Inherits: Node3D < Node < Object

Node supporting hand and finger tracking in OpenXR.

This node enables OpenXR's hand tracking functionality. The node should be a child node of an XROrigin3D node, tracking will update its position to the player's tracked hand Palm joint location (the center of the middle finger's metacarpal bone). This node also updates the skeleton of a properly skinned hand or avatar model.

If the skeleton is a hand (one of the hand bones is the root node of the skeleton), then the skeleton will be placed relative to the hand palm location and the hand mesh and skeleton should be children of the OpenXRHand node.

If the hand bones are part of a full skeleton, then the root of the hand will keep its location with the assumption that IK is used to position the hand and arm.

By default the skeleton hand bones are repositioned to match the size of the tracked hand. To preserve the modeled bone sizes change bone_update to apply rotation only.

Tracking the player's left hand.

Tracking the player's right hand.

Maximum supported hands.

MotionRange MOTION_RANGE_UNOBSTRUCTED = 0

When player grips, hand skeleton will form a full fist.

MotionRange MOTION_RANGE_CONFORM_TO_CONTROLLER = 1

When player grips, hand skeleton conforms to the controller the player is holding.

MotionRange MOTION_RANGE_MAX = 2

Maximum supported motion ranges.

SkeletonRig SKELETON_RIG_OPENXR = 0

An OpenXR compliant skeleton.

SkeletonRig SKELETON_RIG_HUMANOID = 1

A SkeletonProfileHumanoid compliant skeleton.

SkeletonRig SKELETON_RIG_MAX = 2

Maximum supported hands.

BoneUpdate BONE_UPDATE_FULL = 0

The skeletons bones are fully updated (both position and rotation) to match the tracked bones.

BoneUpdate BONE_UPDATE_ROTATION_ONLY = 1

The skeletons bones are only rotated to align with the tracked bones, preserving bone length.

BoneUpdate BONE_UPDATE_MAX = 2

Maximum supported bone update mode.

BoneUpdate bone_update = 0 

void set_bone_update(value: BoneUpdate)

BoneUpdate get_bone_update()

Specify the type of updates to perform on the bone.

void set_hand(value: Hands)

Specifies whether this node tracks the left or right hand of the player.

NodePath hand_skeleton = NodePath("") 

void set_hand_skeleton(value: NodePath)

NodePath get_hand_skeleton()

Set a Skeleton3D node for which the pose positions will be updated.

MotionRange motion_range = 0 

void set_motion_range(value: MotionRange)

MotionRange get_motion_range()

Set the motion range (if supported) limiting the hand motion.

SkeletonRig skeleton_rig = 0 

void set_skeleton_rig(value: SkeletonRig)

SkeletonRig get_skeleton_rig()

Set the type of skeleton rig the hand_skeleton is compliant with.

Please read the User-contributed notes policy before submitting a comment.

---

## Playing videos

**URL:** https://docs.godotengine.org/en/stable/tutorials/animation/playing_videos.html

**Contents:**
- Playing videos
- Supported playback formats
- Setting up VideoStreamPlayer
  - Handling resizing and different aspect ratios
  - Displaying a video on a 3D surface
  - Looping a video
- Video decoding conditions and recommended resolutions
- Playback limitations
- Recommended Theora encoding settings
  - Balancing quality and file size

Godot supports video playback with the VideoStreamPlayer node.

The only supported format in core is Ogg Theora (not to be confused with Ogg Vorbis audio) with optional Ogg Vorbis audio tracks. It's possible for extensions to bring support for additional formats.

H.264 and H.265 cannot be supported in core Godot, as they are both encumbered by software patents. AV1 is royalty-free, but it remains slow to decode on the CPU and hardware decoding support isn't readily available on all GPUs in use yet.

WebM was supported in core in Godot 3.x, but support for it was removed in 4.0 as it was too buggy and difficult to maintain.

You may find videos with a .ogg or .ogx extensions, which are generic extensions for data within an Ogg container.

Renaming these file extensions to .ogv may allow the videos to be imported in Godot. However, not all files with .ogg or .ogx extensions are videos - some of them may only contain audio.

Create a VideoStreamPlayer node using the Create New Node dialog.

Select the VideoStreamPlayer node in the scene tree dock, go to the inspector and load a .ogv file in the Stream property.

If you don't have your video in Ogg Theora format yet, jump to Recommended Theora encoding settings.

If you want the video to play as soon as the scene is loaded, check Autoplay in the inspector. If not, leave Autoplay disabled and call play() on the VideoStreamPlayer node in a script to start playback when desired.

By default in Godot 4.0, the VideoStreamPlayer will automatically be resized to match the video's resolution. You can make it follow usual Control sizing by enabling Expand on the VideoStreamPlayer node.

To adjust how the VideoStreamPlayer node resizes depending on window size, adjust the anchors using the Layout menu at the top of the 2D editor viewport. However, this setup may not be powerful enough to handle all use cases, such as playing fullscreen videos without distorting the video (but with empty space on the edges instead). For more control, you can use an AspectRatioContainer node, which is designed to handle this kind of use case:

Add an AspectRatioContainer node. Make sure it is not a child of any other container node. Select the AspectRatioContainer node, then set its Layout at the top of the 2D editor to Full Rect. Set Ratio in the AspectRatioContainer node to match your video's aspect ratio. You can use math formulas in the inspector to help yourself. Remember to make one of the operands a float. Otherwise, the division's result will always be an integer.

This will evaluate to (approximately) 1.777778

Once you've configured the AspectRatioContainer, reparent your VideoStreamPlayer node to be a child of the AspectRatioContainer node. Make sure Expand is enabled on the VideoStreamPlayer. Your video should now scale automatically to fit the whole screen while avoiding distortion.

See Multiple resolutions for more tips on supporting multiple aspect ratios in your project.

Using a VideoStreamPlayer node as a child of a SubViewport node, it's possible to display any 2D node on a 3D surface. For example, this can be used to display animated billboards when frame-by-frame animation would require too much memory.

This can be done with the following steps:

Create a SubViewport node. Set its size to match your video's size in pixels.

Create a VideoStreamPlayer node as a child of the SubViewport node and specify a video path in it. Make sure Expand is disabled, and enable Autoplay if needed.

Create a MeshInstance3D node with a PlaneMesh or QuadMesh resource in its Mesh property. Resize the mesh to match the video's aspect ratio (otherwise, it will appear distorted).

Create a new StandardMaterial3D resource in the Material Override property in the GeometryInstance3D section.

Enable Local To Scene in the StandardMaterial3D's Resource section (at the bottom). This is required before you can use a ViewportTexture in its Albedo Texture property.

In the StandardMaterial3D, set the Albedo > Texture property to New ViewportTexture. Edit the new resource by clicking it, then specify the path to the SubViewport node in the Viewport Path property.

Enable Albedo Texture Force sRGB in the StandardMaterial3D to prevent colors from being washed out.

If the billboard is supposed to emit its own light, set Shading Mode to Unshaded to improve rendering performance.

See Using Viewports and the GUI in 3D demo for more information on setting this up.

For looping a video, the Loop property can be enabled. This will seamlessly restart the video when it reaches its end.

Note that setting the project setting Video Delay Compensation to a non-zero value might cause your loop to not be seamless, because the synchronization of audio and video takes place at the start of each loop causing occasional missed frames. Set Video Delay Compensation in your project settings to 0 to avoid frame drop issues.

Video decoding is performed on the CPU, as GPUs don't have hardware acceleration for decoding Theora videos. Modern desktop CPUs can decode Ogg Theora videos at 1440p @ 60 FPS or more, but low-end mobile CPUs will likely struggle with high-resolution videos.

To ensure your videos decode smoothly on varied hardware:

When developing games for desktop platforms, it's recommended to encode in 1080p at most (preferably at 30 FPS). Most people are still using 1080p or lower resolution displays, so encoding higher-resolution videos may not be worth the increased file size and CPU requirements.

When developing games for mobile or web platforms, it's recommended to encode in 720p at most (preferably at 30 FPS or even lower). The visual difference between 720p and 1080p videos on a mobile device is usually not that noticeable.

There are some limitations with the current implementation of video playback in Godot:

Streaming a video from a URL is not supported.

Only mono and stereo audio output is supported. Videos with 4, 5.1 and 7.1 audio channels are supported but down-mixed to stereo.

A word of advice is to avoid relying on built-in Ogg Theora exporters (most of the time). There are 2 reasons you may want to favor using an external program to encode your video:

Some programs such as Blender can render to Ogg Theora. However, the default quality presets are usually very low by today's standards. You may be able to increase the quality options in the software you're using, but you may find the output quality to remain less than ideal (given the increased file size). This usually means that the software only supports encoding to constant bit rate (CBR), instead of variable bit rate (VBR). VBR encoding should be preferred in most scenarios as it provides a better quality to file size ratio.

Some other programs can't render to Ogg Theora at all.

In this case, you can render the video to an intermediate high-quality format (such as a high-bitrate H.264 video) then re-encode it to Ogg Theora. Ideally, you should use a lossless or uncompressed format as an intermediate format to maximize the quality of the output Ogg Theora video, but this can require a lot of disk space.

FFmpeg (CLI) is a popular open source tool for this purpose. FFmpeg has a steep learning curve, but it's a powerful tool.

Here are example FFmpeg commands to convert an MP4 video to Ogg Theora. Since FFmpeg supports a lot of input formats, you should be able to use the commands below with almost any input video format (AVI, MOV, WebM, …).

Make sure your copy of FFmpeg is compiled with libtheora and libvorbis support. You can check this by running ffmpeg without any arguments, then looking at the configuration: line in the command output.

Current official FFmpeg releases have some bugs in their Ogg/Theora multiplexer. It's highly recommended to use one of the latest static daily builds, or build from their master branch to get the latest fixes.

The video quality level (-q:v) must be between 1 and 10. Quality 6 is a good compromise between quality and file size. If encoding at a high resolution (such as 1440p or 4K), you will probably want to decrease -q:v to 5 to keep file sizes reasonable. Since pixel density is higher on a 1440p or 4K video, lower quality presets at higher resolutions will look as good or better compared to low-resolution videos.

The audio quality level (-q:a) must be between -1 and 10. Quality 6 provides a good compromise between quality and file size. In contrast to video quality, increasing audio quality doesn't increase the output file size nearly as much. Therefore, if you want the cleanest audio possible, you can increase this to 9 to get perceptually lossless audio. This is especially valuable if your input file already uses lossy audio compression. Higher quality audio does increase the CPU usage of the decoder, so it might lead to audio dropouts in case of high system load. See this page for a table listing Ogg Vorbis audio quality presets and their respective variable bitrates.

The GOP (Group of Pictures) size (-g:v) is the max interval between keyframes. Increasing this value can improve compression with almost no impact on quality. The default size (12) is too low for most types of content, it's therefore recommended using higher GOP values before reducing video quality. Compression benefits will fade away as the GOP size increases though. Values between 64 and 512 usually give the best compression.

Higher GOP sizes will increase max seek times with a sudden increase when going beyond powers of two starting at 64. Max seek times with GOP size 65 can be almost twice as long as with GOP size 64, depending on decoding speed.

The following command converts the video while keeping its original resolution. The video and audio's bitrate will be variable to maximize quality while saving space in parts of the video/audio that don't require a high bitrate (such as static scenes).

The following command resizes a video to be 720 pixels tall (720p), while preserving its existing aspect ratio. This helps decrease the file size significantly if the source is recorded at a higher resolution than 720p:

Chroma key, commonly known as the "green screen" or "blue screen" effect, allows you to remove a specific color from an image or video and replace it with another background. This effect is widely used in video production to composite different elements together seamlessly.

We will achieve the chroma key effect by writing a custom shader in GDScript and using a VideoStreamPlayer node to display the video content.

Ensure that the scene contains a VideoStreamPlayer node to play the video and a Control node to hold the UI elements for controlling the chroma key effect.

To implement the chroma key effect, follow these steps:

Select the VideoStreamPlayer node in the scene and go to its properties. Under CanvasItem > Material, create a new shader named "ChromaKeyShader.gdshader."

In the "ChromaKeyShader.gdshader" file, write the custom shader code as shown below:

The shader uses the distance calculation to identify pixels close to the chroma key color and discards them, effectively removing the selected color. Pixels that are slightly further away from the chroma key color are faded based on the fade_factor, blending them smoothly with the surrounding colors. This process creates the desired chroma key effect, making it appear as if the background has been replaced with another image or video.

The code above represents a simple demonstration of the Chroma Key shader, and users can customize it according to their specific requirements.

To allow users to manipulate the chroma key effect in real-time, we created sliders in the Control node. The Control node's script contains the following functions:

also make sure that the range of the sliders are appropriate, our settings are :

Connect the appropriate signal from the UI elements to the Control node's script. you created in the Control node's script to control the chroma key effect. These signal handlers will update the shader's uniform variables in response to user input.

Save and run the scene to see the chroma key effect in action! With the provided UI controls, you can now adjust the chroma key color, pickup range, and fade amount in real-time, achieving the desired chroma key functionality for your video content.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
ffmpeg -i input.mp4 -q:v 6 -q:a 6 -g:v 64 output.ogv
```

Example 2 (json):
```json
ffmpeg -i input.mp4 -vf "scale=-1:720" -q:v 6 -q:a 6 -g:v 64 output.ogv
```

Example 3 (typescript):
```typescript
shader_type canvas_item;

// Uniform variables for chroma key effect
uniform vec3 chroma_key_color : source_color = vec3(0.0, 1.0, 0.0);
uniform float pickup_range : hint_range(0.0, 1.0) = 0.1;
uniform float fade_amount : hint_range(0.0, 1.0) = 0.1;

void fragment() {
    // Get the color from the texture at the given UV coordinates
    vec4 color = texture(TEXTURE, UV);

    // Calculate the distance between the current color and the chroma key color
    float distance = length(color.rgb - chroma_key_color);

    // If the distance is within the pickup range, discard the pixel
    // the lesser the distance more likely the colors are
    if (distance <= pickup_range) {
        discard;
    }

    // Calculate the fade factor based on the pickup range and fade amount
    float fade_factor = smoothstep(pickup_range, pickup_range + fade_amount, distance);

    // Set the output color with the original RGB values and the calculated fade factor
    COLOR = vec4(color.rgb, fade_factor);
}
```

Example 4 (gdscript):
```gdscript
extends Control

 func _on_color_picker_button_color_changed(color):
     # Update the "chroma_key_color" shader parameter of the VideoStreamPlayer's material.
     $VideoStreamPlayer.material.set("shader_parameter/chroma_key_color", color)

 func _on_h_slider_value_changed(value):
     # Update the "pickup_range" shader parameter of the VideoStreamPlayer's material.
     $VideoStreamPlayer.material.set("shader_parameter/pickup_range", value)

 func _on_h_slider_2_value_changed(value):
     # Update the "fade_amount" shader parameter of the VideoStreamPlayer's material.
     $VideoStreamPlayer.material.set("shader_parameter/fade_amount", value)

func _on_video_stream_player_finished():
     # Restart the video playback when it's finished.
     $VideoStreamPlayer.play()
```

---

## PropertyTweener

**URL:** https://docs.godotengine.org/en/stable/classes/class_propertytweener.html

**Contents:**
- PropertyTweener
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: Tweener < RefCounted < Object

Interpolates an Object's property over time.

PropertyTweener is used to interpolate a property in an object. See Tween.tween_property() for more usage information.

The tweener will finish automatically if the target object is freed.

Note: Tween.tween_property() is the only correct way to create PropertyTweener. Any PropertyTweener created manually will not function correctly.

set_custom_interpolator(interpolator_method: Callable)

set_delay(delay: float)

set_ease(ease: EaseType)

set_trans(trans: TransitionType)

PropertyTweener as_relative() 

When called, the final value will be used as a relative value instead.

Example: Move the node by 100 pixels to the right.

PropertyTweener from(value: Variant) 

Sets a custom initial value to the PropertyTweener.

Example: Move the node from position (100, 100) to (200, 100).

PropertyTweener from_current() 

Makes the PropertyTweener use the current property value (i.e. at the time of creating this PropertyTweener) as a starting point. This is equivalent of using from() with the current value. These two calls will do the same:

PropertyTweener set_custom_interpolator(interpolator_method: Callable) 

Allows interpolating the value with a custom easing function. The provided interpolator_method will be called with a value ranging from 0.0 to 1.0 and is expected to return a value within the same range (values outside the range can be used for overshoot). The return value of the method is then used for interpolation between initial and final value. Note that the parameter passed to the method is still subject to the tweener's own easing.

PropertyTweener set_delay(delay: float) 

Sets the time in seconds after which the PropertyTweener will start interpolating. By default there's no delay.

PropertyTweener set_ease(ease: EaseType) 

Sets the type of used easing from EaseType. If not set, the default easing is used from the Tween that contains this Tweener.

PropertyTweener set_trans(trans: TransitionType) 

Sets the type of used transition from TransitionType. If not set, the default transition is used from the Tween that contains this Tweener.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
var tween = get_tree().create_tween()
tween.tween_property(self, "position", Vector2.RIGHT * 100, 1).as_relative()
```

Example 2 (csharp):
```csharp
Tween tween = GetTree().CreateTween();
tween.TweenProperty(this, "position", Vector2.Right * 100.0f, 1.0f).AsRelative();
```

Example 3 (csharp):
```csharp
var tween = get_tree().create_tween()
tween.tween_property(self, "position", Vector2(200, 100), 1).from(Vector2(100, 100))
```

Example 4 (csharp):
```csharp
Tween tween = GetTree().CreateTween();
tween.TweenProperty(this, "position", new Vector2(200.0f, 100.0f), 1.0f).From(new Vector2(100.0f, 100.0f));
```

---

## SkeletonProfileHumanoid

**URL:** https://docs.godotengine.org/en/stable/classes/class_skeletonprofilehumanoid.html

**Contents:**
- SkeletonProfileHumanoid
- Description
- Tutorials
- Properties
- User-contributed notes

Inherits: SkeletonProfile < Resource < RefCounted < Object

A humanoid SkeletonProfile preset.

A SkeletonProfile as a preset that is optimized for the human form. This exists for standardization, so all parameters are read-only.

A humanoid skeleton profile contains 54 bones divided in 4 groups: "Body", "Face", "LeftHand", and "RightHand". It is structured as follows:

Retargeting 3D Skeletons

56 (overrides SkeletonProfile)

4 (overrides SkeletonProfile)

&"Root" (overrides SkeletonProfile)

&"Hips" (overrides SkeletonProfile)

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
Root
└─ Hips
    ├─ LeftUpperLeg
    │  └─ LeftLowerLeg
    │     └─ LeftFoot
    │        └─ LeftToes
    ├─ RightUpperLeg
    │  └─ RightLowerLeg
    │     └─ RightFoot
    │        └─ RightToes
    └─ Spine
        └─ Chest
            └─ UpperChest
                ├─ Neck
                │   └─ Head
                │       ├─ Jaw
                │       ├─ LeftEye
                │       └─ RightEye
                ├─ LeftShoulder
                │  └─ LeftUpperArm
                │     └─ LeftLowerArm
                │        └─ LeftHand
                │           ├─ LeftThumbMetacarpal
                │           │  └─ LeftThumbProximal
                │           │    └─ LeftThumbDistal
                │           ├─ LeftIndexProximal
                │           │  └─ LeftIndexIntermediate
                │           │    └─ LeftIndexDistal
                │           ├─ LeftMiddleProximal
                │           │  └─ LeftMiddleIntermediate
                │           │    └─ LeftMiddleDistal
                │           ├─ LeftRingProximal
                │           │  └─ LeftRingIntermediate
                │           │    └─ LeftRingDistal
                │           └─ LeftLittleProximal
                │              └─ LeftLittleIntermediate
                │                └─ LeftLittleDistal
                └─ RightShoulder
                   └─ RightUpperArm
                      └─ RightLowerArm
                         └─ RightHand
                            ├─ RightThumbMetacarpal
                            │  └─ RightThumbProximal
                            │     └─ RightThumbDistal
                            ├─ RightIndexProximal
                            │  └─ RightIndexIntermediate
                            │     └─ RightIndexDistal
                            ├─ RightMiddleProximal
                            │  └─ RightMiddleIntermediate
                            │     └─ RightMiddleDistal
                            ├─ RightRingProximal
                            │  └─ RightRingIntermediate
                            │     └─ RightRingDistal
                            └─ RightLittleProximal
                               └─ RightLittleIntermediate
                                 └─ RightLittleDistal
```

---

## SkeletonProfile

**URL:** https://docs.godotengine.org/en/stable/classes/class_skeletonprofile.html

**Contents:**
- SkeletonProfile
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: SkeletonProfileHumanoid

Base class for a profile of a virtual skeleton used as a target for retargeting.

This resource is used in EditorScenePostImport. Some parameters are referring to bones in Skeleton3D, Skin, Animation, and some other nodes are rewritten based on the parameters of SkeletonProfile.

Note: These parameters need to be set only when creating a custom profile. In SkeletonProfileHumanoid, they are defined internally as read-only values.

Retargeting 3D Skeletons

find_bone(bone_name: StringName) const

get_bone_name(bone_idx: int) const

get_bone_parent(bone_idx: int) const

get_bone_tail(bone_idx: int) const

get_group(bone_idx: int) const

get_group_name(group_idx: int) const

get_handle_offset(bone_idx: int) const

get_reference_pose(bone_idx: int) const

get_tail_direction(bone_idx: int) const

get_texture(group_idx: int) const

is_required(bone_idx: int) const

set_bone_name(bone_idx: int, bone_name: StringName)

set_bone_parent(bone_idx: int, bone_parent: StringName)

set_bone_tail(bone_idx: int, bone_tail: StringName)

set_group(bone_idx: int, group: StringName)

set_group_name(group_idx: int, group_name: StringName)

set_handle_offset(bone_idx: int, handle_offset: Vector2)

set_reference_pose(bone_idx: int, bone_name: Transform3D)

set_required(bone_idx: int, required: bool)

set_tail_direction(bone_idx: int, tail_direction: TailDirection)

set_texture(group_idx: int, texture: Texture2D)

This signal is emitted when change the value in profile. This is used to update key name in the BoneMap and to redraw the BoneMap editor.

Note: This signal is not connected directly to editor to simplify the reference, instead it is passed on to editor through the BoneMap.

enum TailDirection: 

TailDirection TAIL_DIRECTION_AVERAGE_CHILDREN = 0

Direction to the average coordinates of bone children.

TailDirection TAIL_DIRECTION_SPECIFIC_CHILD = 1

Direction to the coordinates of specified bone child.

TailDirection TAIL_DIRECTION_END = 2

Direction is not calculated.

void set_bone_size(value: int)

The amount of bones in retargeting section's BoneMap editor. For example, SkeletonProfileHumanoid has 56 bones.

The size of elements in BoneMap updates when changing this property in it's assigned SkeletonProfile.

void set_group_size(value: int)

The amount of groups of bones in retargeting section's BoneMap editor. For example, SkeletonProfileHumanoid has 4 groups.

This property exists to separate the bone list into several sections in the editor.

StringName root_bone = &"" 

void set_root_bone(value: StringName)

StringName get_root_bone()

A bone name that will be used as the root bone in AnimationTree. This should be the bone of the parent of hips that exists at the world origin.

StringName scale_base_bone = &"" 

void set_scale_base_bone(value: StringName)

StringName get_scale_base_bone()

A bone name which will use model's height as the coefficient for normalization. For example, SkeletonProfileHumanoid defines it as Hips.

int find_bone(bone_name: StringName) const 

Returns the bone index that matches bone_name as its name.

StringName get_bone_name(bone_idx: int) const 

Returns the name of the bone at bone_idx that will be the key name in the BoneMap.

In the retargeting process, the returned bone name is the bone name of the target skeleton.

StringName get_bone_parent(bone_idx: int) const 

Returns the name of the bone which is the parent to the bone at bone_idx. The result is empty if the bone has no parent.

StringName get_bone_tail(bone_idx: int) const 

Returns the name of the bone which is the tail of the bone at bone_idx.

StringName get_group(bone_idx: int) const 

Returns the group of the bone at bone_idx.

StringName get_group_name(group_idx: int) const 

Returns the name of the group at group_idx that will be the drawing group in the BoneMap editor.

Vector2 get_handle_offset(bone_idx: int) const 

Returns the offset of the bone at bone_idx that will be the button position in the BoneMap editor.

This is the offset with origin at the top left corner of the square.

Transform3D get_reference_pose(bone_idx: int) const 

Returns the reference pose transform for bone bone_idx.

TailDirection get_tail_direction(bone_idx: int) const 

Returns the tail direction of the bone at bone_idx.

Texture2D get_texture(group_idx: int) const 

Returns the texture of the group at group_idx that will be the drawing group background image in the BoneMap editor.

bool is_required(bone_idx: int) const 

Returns whether the bone at bone_idx is required for retargeting.

This value is used by the bone map editor. If this method returns true, and no bone is assigned, the handle color will be red on the bone map editor.

void set_bone_name(bone_idx: int, bone_name: StringName) 

Sets the name of the bone at bone_idx that will be the key name in the BoneMap.

In the retargeting process, the setting bone name is the bone name of the target skeleton.

void set_bone_parent(bone_idx: int, bone_parent: StringName) 

Sets the bone with name bone_parent as the parent of the bone at bone_idx. If an empty string is passed, then the bone has no parent.

void set_bone_tail(bone_idx: int, bone_tail: StringName) 

Sets the bone with name bone_tail as the tail of the bone at bone_idx.

void set_group(bone_idx: int, group: StringName) 

Sets the group of the bone at bone_idx.

void set_group_name(group_idx: int, group_name: StringName) 

Sets the name of the group at group_idx that will be the drawing group in the BoneMap editor.

void set_handle_offset(bone_idx: int, handle_offset: Vector2) 

Sets the offset of the bone at bone_idx that will be the button position in the BoneMap editor.

This is the offset with origin at the top left corner of the square.

void set_reference_pose(bone_idx: int, bone_name: Transform3D) 

Sets the reference pose transform for bone bone_idx.

void set_required(bone_idx: int, required: bool) 

Sets the required status for bone bone_idx to required.

void set_tail_direction(bone_idx: int, tail_direction: TailDirection) 

Sets the tail direction of the bone at bone_idx.

Note: This only specifies the method of calculation. The actual coordinates required should be stored in an external skeleton, so the calculation itself needs to be done externally.

void set_texture(group_idx: int, texture: Texture2D) 

Sets the texture of the group at group_idx that will be the drawing group background image in the BoneMap editor.

Please read the User-contributed notes policy before submitting a comment.

---

## SubtweenTweener

**URL:** https://docs.godotengine.org/en/stable/classes/class_subtweentweener.html

**Contents:**
- SubtweenTweener
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: Tweener < RefCounted < Object

Runs a Tween nested within another Tween.

SubtweenTweener is used to execute a Tween as one step in a sequence defined by another Tween. See Tween.tween_subtween() for more usage information.

Note: Tween.tween_subtween() is the only correct way to create SubtweenTweener. Any SubtweenTweener created manually will not function correctly.

set_delay(delay: float)

SubtweenTweener set_delay(delay: float) 

Sets the time in seconds after which the SubtweenTweener will start running the subtween. By default there's no delay.

Please read the User-contributed notes policy before submitting a comment.

---

## Tweener

**URL:** https://docs.godotengine.org/en/stable/classes/class_tweener.html

**Contents:**
- Tweener
- Description
- Signals
- User-contributed notes

Inherits: RefCounted < Object

Inherited By: CallbackTweener, IntervalTweener, MethodTweener, PropertyTweener, SubtweenTweener

Abstract class for all Tweeners used by Tween.

Tweeners are objects that perform a specific animating task, e.g. interpolating a property or calling a method at a given time. A Tweener can't be created manually, you need to use a dedicated method from Tween.

Emitted when the Tweener has just finished its job or became invalid (e.g. due to a freed object).

Please read the User-contributed notes policy before submitting a comment.

---

## Tween

**URL:** https://docs.godotengine.org/en/stable/classes/class_tween.html

**Contents:**
- Tween
- Description
- Methods
- Signals
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Lightweight object used for general-purpose animation via script, using Tweeners.

Tweens are mostly useful for animations requiring a numerical property to be interpolated over a range of values. The name tween comes from in-betweening, an animation technique where you specify keyframes and the computer interpolates the frames that appear between them. Animating something with a Tween is called tweening.

Tween is more suited than AnimationPlayer for animations where you don't know the final values in advance. For example, interpolating a dynamically-chosen camera zoom value is best done with a Tween; it would be difficult to do the same thing with an AnimationPlayer node. Tweens are also more light-weight than AnimationPlayer, so they are very much suited for simple animations or general tasks that don't require visual tweaking provided by the editor. They can be used in a "fire-and-forget" manner for some logic that normally would be done by code. You can e.g. make something shoot periodically by using a looped CallbackTweener with a delay.

A Tween can be created by using either SceneTree.create_tween() or Node.create_tween(). Tweens created manually (i.e. by using Tween.new()) are invalid and can't be used for tweening values.

A tween animation is created by adding Tweeners to the Tween object, using tween_property(), tween_interval(), tween_callback() or tween_method():

This sequence will make the $Sprite node turn red, then shrink, before finally calling Node.queue_free() to free the sprite. Tweeners are executed one after another by default. This behavior can be changed using parallel() and set_parallel().

When a Tweener is created with one of the tween_* methods, a chained method call can be used to tweak the properties of this Tweener. For example, if you want to set a different transition type in the above example, you can use set_trans():

Most of the Tween methods can be chained this way too. In the following example the Tween is bound to the running script's node and a default transition is set for its Tweeners:

Another interesting use for Tweens is animating arbitrary sets of objects:

In the example above, all children of a node are moved one after another to position (0, 0).

You should avoid using more than one Tween per object's property. If two or more tweens animate one property at the same time, the last one created will take priority and assign the final value. If you want to interrupt and restart an animation, consider assigning the Tween to a variable:

Some Tweeners use transitions and eases. The first accepts a TransitionType constant, and refers to the way the timing of the animation is handled (see easings.net for some examples). The second accepts an EaseType constant, and controls where the trans_type is applied to the interpolation (in the beginning, the end, or both). If you don't know which transition and easing to pick, you can try different TransitionType constants with EASE_IN_OUT, and use the one that looks best.

Tween easing and transition types cheatsheet

Note: Tweens are not designed to be reused and trying to do so results in an undefined behavior. Create a new Tween for each animation and every time you replay an animation from start. Keep in mind that Tweens start immediately, so only create a Tween when you want to start animating.

Note: The tween is processed after all of the nodes in the current frame, i.e. node's Node._process() method would be called before the tween (or Node._physics_process() depending on the value passed to set_process_mode()).

bind_node(node: Node)

custom_step(delta: float)

get_loops_left() const

get_total_elapsed_time() const

interpolate_value(initial_value: Variant, delta_value: Variant, elapsed_time: float, duration: float, trans_type: TransitionType, ease_type: EaseType) static

set_ease(ease: EaseType)

set_ignore_time_scale(ignore: bool = true)

set_loops(loops: int = 0)

set_parallel(parallel: bool = true)

set_pause_mode(mode: TweenPauseMode)

set_process_mode(mode: TweenProcessMode)

set_speed_scale(speed: float)

set_trans(trans: TransitionType)

tween_callback(callback: Callable)

tween_interval(time: float)

tween_method(method: Callable, from: Variant, to: Variant, duration: float)

tween_property(object: Object, property: NodePath, final_val: Variant, duration: float)

tween_subtween(subtween: Tween)

Emitted when the Tween has finished all tweening. Never emitted when the Tween is set to infinite looping (see set_loops()).

loop_finished(loop_count: int) 

Emitted when a full loop is complete (see set_loops()), providing the loop index. This signal is not emitted after the final loop, use finished instead for this case.

step_finished(idx: int) 

Emitted when one step of the Tween is complete, providing the step index. One step is either a single Tweener or a group of Tweeners running in parallel.

enum TweenProcessMode: 

TweenProcessMode TWEEN_PROCESS_PHYSICS = 0

The Tween updates after each physics frame (see Node._physics_process()).

TweenProcessMode TWEEN_PROCESS_IDLE = 1

The Tween updates after each process frame (see Node._process()).

enum TweenPauseMode: 

TweenPauseMode TWEEN_PAUSE_BOUND = 0

If the Tween has a bound node, it will process when that node can process (see Node.process_mode). Otherwise it's the same as TWEEN_PAUSE_STOP.

TweenPauseMode TWEEN_PAUSE_STOP = 1

If SceneTree is paused, the Tween will also pause.

TweenPauseMode TWEEN_PAUSE_PROCESS = 2

The Tween will process regardless of whether SceneTree is paused.

enum TransitionType: 

TransitionType TRANS_LINEAR = 0

The animation is interpolated linearly.

TransitionType TRANS_SINE = 1

The animation is interpolated using a sine function.

TransitionType TRANS_QUINT = 2

The animation is interpolated with a quintic (to the power of 5) function.

TransitionType TRANS_QUART = 3

The animation is interpolated with a quartic (to the power of 4) function.

TransitionType TRANS_QUAD = 4

The animation is interpolated with a quadratic (to the power of 2) function.

TransitionType TRANS_EXPO = 5

The animation is interpolated with an exponential (to the power of x) function.

TransitionType TRANS_ELASTIC = 6

The animation is interpolated with elasticity, wiggling around the edges.

TransitionType TRANS_CUBIC = 7

The animation is interpolated with a cubic (to the power of 3) function.

TransitionType TRANS_CIRC = 8

The animation is interpolated with a function using square roots.

TransitionType TRANS_BOUNCE = 9

The animation is interpolated by bouncing at the end.

TransitionType TRANS_BACK = 10

The animation is interpolated backing out at ends.

TransitionType TRANS_SPRING = 11

The animation is interpolated like a spring towards the end.

The interpolation starts slowly and speeds up towards the end.

EaseType EASE_OUT = 1

The interpolation starts quickly and slows down towards the end.

EaseType EASE_IN_OUT = 2

A combination of EASE_IN and EASE_OUT. The interpolation is slowest at both ends.

EaseType EASE_OUT_IN = 3

A combination of EASE_IN and EASE_OUT. The interpolation is fastest at both ends.

Tween bind_node(node: Node) 

Binds this Tween with the given node. Tweens are processed directly by the SceneTree, so they run independently of the animated nodes. When you bind a Node with the Tween, the Tween will halt the animation when the object is not inside tree and the Tween will be automatically killed when the bound object is freed. Also TWEEN_PAUSE_BOUND will make the pausing behavior dependent on the bound node.

For a shorter way to create and bind a Tween, you can use Node.create_tween().

Used to chain two Tweeners after set_parallel() is called with true.

bool custom_step(delta: float) 

Processes the Tween by the given delta value, in seconds. This is mostly useful for manual control when the Tween is paused. It can also be used to end the Tween animation immediately, by setting delta longer than the whole duration of the Tween animation.

Returns true if the Tween still has Tweeners that haven't finished.

int get_loops_left() const 

Returns the number of remaining loops for this Tween (see set_loops()). A return value of -1 indicates an infinitely looping Tween, and a return value of 0 indicates that the Tween has already finished.

float get_total_elapsed_time() const 

Returns the total time in seconds the Tween has been animating (i.e. the time since it started, not counting pauses etc.). The time is affected by set_speed_scale(), and stop() will reset it to 0.

Note: As it results from accumulating frame deltas, the time returned after the Tween has finished animating will be slightly greater than the actual Tween duration.

Variant interpolate_value(initial_value: Variant, delta_value: Variant, elapsed_time: float, duration: float, trans_type: TransitionType, ease_type: EaseType) static 

This method can be used for manual interpolation of a value, when you don't want Tween to do animating for you. It's similar to @GlobalScope.lerp(), but with support for custom transition and easing.

initial_value is the starting value of the interpolation.

delta_value is the change of the value in the interpolation, i.e. it's equal to final_value - initial_value.

elapsed_time is the time in seconds that passed after the interpolation started and it's used to control the position of the interpolation. E.g. when it's equal to half of the duration, the interpolated value will be halfway between initial and final values. This value can also be greater than duration or lower than 0, which will extrapolate the value.

duration is the total time of the interpolation.

Note: If duration is equal to 0, the method will always return the final value, regardless of elapsed_time provided.

Returns whether the Tween is currently running, i.e. it wasn't paused and it's not finished.

Returns whether the Tween is valid. A valid Tween is a Tween contained by the scene tree (i.e. the array from SceneTree.get_processed_tweens() will contain this Tween). A Tween might become invalid when it has finished tweening, is killed, or when created with Tween.new(). Invalid Tweens can't have Tweeners appended.

Aborts all tweening operations and invalidates the Tween.

Makes the next Tweener run parallelly to the previous one.

All Tweeners in the example will run at the same time.

You can make the Tween parallel by default by using set_parallel().

Pauses the tweening. The animation can be resumed by using play().

Note: If a Tween is paused and not bound to any node, it will exist indefinitely until manually started or invalidated. If you lose a reference to such Tween, you can retrieve it using SceneTree.get_processed_tweens().

Resumes a paused or stopped Tween.

Tween set_ease(ease: EaseType) 

Sets the default ease type for PropertyTweeners and MethodTweeners appended after this method.

Before this method is called, the default ease type is EASE_IN_OUT.

Tween set_ignore_time_scale(ignore: bool = true) 

If ignore is true, the tween will ignore Engine.time_scale and update with the real, elapsed time. This affects all Tweeners and their delays. Default value is false.

Tween set_loops(loops: int = 0) 

Sets the number of times the tweening sequence will be repeated, i.e. set_loops(2) will run the animation twice.

Calling this method without arguments will make the Tween run infinitely, until either it is killed with kill(), the Tween's bound node is freed, or all the animated objects have been freed (which makes further animation impossible).

Warning: Make sure to always add some duration/delay when using infinite loops. To prevent the game freezing, 0-duration looped animations (e.g. a single CallbackTweener with no delay) are stopped after a small number of loops, which may produce unexpected results. If a Tween's lifetime depends on some node, always use bind_node().

Tween set_parallel(parallel: bool = true) 

If parallel is true, the Tweeners appended after this method will by default run simultaneously, as opposed to sequentially.

Note: Just like with parallel(), the tweener added right before this method will also be part of the parallel step.

Tween set_pause_mode(mode: TweenPauseMode) 

Determines the behavior of the Tween when the SceneTree is paused.

Default value is TWEEN_PAUSE_BOUND.

Tween set_process_mode(mode: TweenProcessMode) 

Determines whether the Tween should run after process frames (see Node._process()) or physics frames (see Node._physics_process()).

Default value is TWEEN_PROCESS_IDLE.

Tween set_speed_scale(speed: float) 

Scales the speed of tweening. This affects all Tweeners and their delays.

Tween set_trans(trans: TransitionType) 

Sets the default transition type for PropertyTweeners and MethodTweeners appended after this method.

Before this method is called, the default transition type is TRANS_LINEAR.

Stops the tweening and resets the Tween to its initial state. This will not remove any appended Tweeners.

Note: This does not reset targets of PropertyTweeners to their values when the Tween first started.

Note: If a Tween is stopped and not bound to any node, it will exist indefinitely until manually started or invalidated. If you lose a reference to such Tween, you can retrieve it using SceneTree.get_processed_tweens().

CallbackTweener tween_callback(callback: Callable) 

Creates and appends a CallbackTweener. This method can be used to call an arbitrary method in any object. Use Callable.bind() to bind additional arguments for the call.

Example: Object that keeps shooting every 1 second:

Example: Turning a sprite red and then blue, with 2 second delay:

IntervalTweener tween_interval(time: float) 

Creates and appends an IntervalTweener. This method can be used to create delays in the tween animation, as an alternative to using the delay in other Tweeners, or when there's no animation (in which case the Tween acts as a timer). time is the length of the interval, in seconds.

Example: Creating an interval in code execution:

Example: Creating an object that moves back and forth and jumps every few seconds:

MethodTweener tween_method(method: Callable, from: Variant, to: Variant, duration: float) 

Creates and appends a MethodTweener. This method is similar to a combination of tween_callback() and tween_property(). It calls a method over time with a tweened value provided as an argument. The value is tweened between from and to over the time specified by duration, in seconds. Use Callable.bind() to bind additional arguments for the call. You can use MethodTweener.set_ease() and MethodTweener.set_trans() to tweak the easing and transition of the value or MethodTweener.set_delay() to delay the tweening.

Example: Making a 3D object look from one point to another point:

Example: Setting the text of a Label, using an intermediate method and after a delay:

PropertyTweener tween_property(object: Object, property: NodePath, final_val: Variant, duration: float) 

Creates and appends a PropertyTweener. This method tweens a property of an object between an initial value and final_val in a span of time equal to duration, in seconds. The initial value by default is the property's value at the time the tweening of the PropertyTweener starts.

will move the sprite to position (100, 200) and then to (200, 300). If you use PropertyTweener.from() or PropertyTweener.from_current(), the starting position will be overwritten by the given value instead. See other methods in PropertyTweener to see how the tweening can be tweaked further.

Note: You can find the correct property name by hovering over the property in the Inspector. You can also provide the components of a property directly by using "property:component" (eg. position:x), where it would only apply to that particular component.

Example: Moving an object twice from the same position, with different transition types:

SubtweenTweener tween_subtween(subtween: Tween) 

Creates and appends a SubtweenTweener. This method can be used to nest subtween within this Tween, allowing for the creation of more complex and composable sequences.

Note: The methods pause(), stop(), and set_loops() can cause the parent Tween to get stuck on the subtween step; see the documentation for those methods for more information.

Note: The pause and process modes set by set_pause_mode() and set_process_mode() on subtween will be overridden by the parent Tween's settings.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
var tween = get_tree().create_tween()
tween.tween_property($Sprite, "modulate", Color.RED, 1.0)
tween.tween_property($Sprite, "scale", Vector2(), 1.0)
tween.tween_callback($Sprite.queue_free)
```

Example 2 (csharp):
```csharp
Tween tween = GetTree().CreateTween();
tween.TweenProperty(GetNode("Sprite"), "modulate", Colors.Red, 1.0f);
tween.TweenProperty(GetNode("Sprite"), "scale", Vector2.Zero, 1.0f);
tween.TweenCallback(Callable.From(GetNode("Sprite").QueueFree));
```

Example 3 (csharp):
```csharp
var tween = get_tree().create_tween()
tween.tween_property($Sprite, "modulate", Color.RED, 1.0).set_trans(Tween.TRANS_SINE)
tween.tween_property($Sprite, "scale", Vector2(), 1.0).set_trans(Tween.TRANS_BOUNCE)
tween.tween_callback($Sprite.queue_free)
```

Example 4 (csharp):
```csharp
Tween tween = GetTree().CreateTween();
tween.TweenProperty(GetNode("Sprite"), "modulate", Colors.Red, 1.0f).SetTrans(Tween.TransitionType.Sine);
tween.TweenProperty(GetNode("Sprite"), "scale", Vector2.Zero, 1.0f).SetTrans(Tween.TransitionType.Bounce);
tween.TweenCallback(Callable.From(GetNode("Sprite").QueueFree));
```

---

## Using AnimationTree

**URL:** https://docs.godotengine.org/en/stable/tutorials/animation/animation_tree.html

**Contents:**
- Using AnimationTree
- Introduction
- AnimationTree and AnimationPlayer
- Creating a tree
- Blend tree
  - Blend2 / Blend3
  - OneShot
  - TimeSeek
  - TimeScale
  - Transition

With AnimationPlayer, Godot has one of the most flexible animation systems that you can find in any game engine. It is pretty much unique in its ability to animate almost any property in any node or resource, and its dedicated transform, bezier, function calling, audio, and sub-animation tracks.

However, the support for blending those animations via AnimationPlayer is limited, as you can only set a fixed cross-fade transition time.

AnimationTree is a new node introduced in Godot 3.1 to deal with advanced transitions. It replaces the ancient AnimationTreePlayer, while adding a huge amount of features and flexibility.

Before starting, know that an AnimationTree node does not contain its own animations. Instead, it uses animations contained in an AnimationPlayer node. You create, edit, or import your animations in an AnimationPlayer and then use an AnimationTree to control the playback.

AnimationPlayer and AnimationTree can be used in both 2D and 3D scenes. When importing 3D scenes and their animations, you can use name suffixes to simplify the process and import with the correct properties. At the end, the imported Godot scene will contain the animations in an AnimationPlayer node. Since you rarely use imported scenes directly in Godot (they are either instantiated or inherited from), you can place the AnimationTree node in your new scene which contains the imported one. Afterwards, point the AnimationTree node to the AnimationPlayer that was created in the imported scene.

This is how it's done in the Third Person Shooter demo, for reference:

A new scene was created for the player with a CharacterBody3D as root. Inside this scene, the original .dae (Collada) file was instantiated and an AnimationTree node was created.

To use an AnimationTree, you have to set a root node. An animation root node is a class that contains and evaluates sub-nodes and outputs an animation. There are 3 types of sub-nodes:

Animation nodes, which reference an animation from the linked AnimationPlayer.

Animation Root nodes, which are used to blend sub-nodes and can be nested.

Animation Blend nodes, which are used in an AnimationNodeBlendTree, a 2D graph of nodes. Blend nodes take multiple input ports and give one output port.

A few types of root nodes are available:

AnimationNodeAnimation: Selects an animation from the list and plays it. This is the simplest root node, and generally not used as a root.

AnimationNodeBlendTree: Contains multiple nodes as children in a graph. Many blend nodes are available, such as mix, blend2, blend3, one shot, etc.

AnimationNodeBlendSpace1D: Allows linear blending between two animation nodes. Control the blend position in a 1D blend space to mix between animations.

AnimationNodeBlendSpace2D: Allows linear blending between three animation nodes. Control the blend position in a 2D blend space to mix between animations.

AnimationNodeStateMachine: Contains multiple nodes as children in a graph. Each node is used as a state, with multiple functions used to alternate between states.

When you make an AnimationNodeBlendTree, you get an empty 2d graph in the bottom panel, under the AnimationTree tab. It contains only an Output node by default.

In order for animations to play, a node has to be connected to the output. You can add nodes from the Add Node.. menu or by right clicking an empty space:

The simplest connection to make is to connect an Animation node to the output directly, which will just play back the animation.

Following is a description of the other available nodes:

These nodes will blend between two or three inputs by a user-specified blend value:

Blending can use filters to control individually which tracks get blended and which do not. This can be useful for layering animations on top of each other.

For more complex blending, it is recommended to use blend spaces instead.

This node will execute an animation once and return when it finishes. You can customize blend times for fading in and out, as well as filters.

This node allows you to seek to a time in the animation connected to its in input. Use this node to play an Animation starting from a certain playback position. Note that the seek request value is measured in seconds, so if you would like to play an animation from the beginning, set the value to 0.0, or if you would like to play an animation from 3 seconds in, set the value to 3.0.

This node allows you to scale the speed of the animation connected to its in input. The speed of the animation will be multiplied by the number in the scale parameter. Setting the scale to 0 will pause the animation. Setting the scale to a negative number will play the animation backwards.

This node is a simplified version of a StateMachine. You connect animations to the inputs, and the current state index determines which animation to play. You may specify a crossfade transition time. In the Inspector, you may change the number of input ports, rearrange inputs, or delete inputs.

When you make an AnimationNodeStateMachine, you get an empty 2d graph in the bottom panel, under the AnimationTree tab. It contains a Start and End state by default.

To add states, right click or use the create new nodes button, whose icon is a plus in a box. You can add animations, blendspaces, blendtrees, or even another StateMachine. To edit one of these more complex sub-nodes, click on the pencil icon on the right of the state. To return to the original StateMachine, click Root on the top left of the panel.

Before the StateMachine can do anything useful, the states must be connected with transitions. To add a transition, click the connect nodes button, which is a line with a right-facing arrow, and drag between two states. You can create 2 transitions between states, one going in each direction.

There are 3 types of transitions:

Immediate: Will switch to the next state immediately.

Sync: Will switch to the next state immediately, but will seek the new state to the playback position of the old state.

At End: Will wait for the current state playback to end, then switch to the beginning of the next state animation.

Transitions also have a few properties. Click a transition and it will be displayed in the inspector:

Xfade Time is the time to cross-fade between this state and the next.

Xfade Curve is a cross-fade following a curve rather than a linear blend.

Reset determines whether the state you are switching into plays from the beginning (true) or not (false).

Priority is used together with the travel() function from code (more on this later). Lower priority transitions are preferred when travelling through the tree.

Switch Mode is the transition type (see above). It can be changed after creation here.

Advance Mode determines the advance mode. If Disabled, the transition will not be used. If Enabled, the transition will only be used during travel(). If Auto, the transition will be used if the advance condition and expression are true, or if there are no advance conditions/expressions.

The last 2 properties in a StateMachine transition are Advance Condition and Advance Expression. When the Advance Mode is set to Auto, these determine if the transition will advance or not.

Advance Condition is a true/false check. You may put a custom variable name in the text field, and when the StateMachine reaches this transition, it will check if your variable is true. If so, the transition continues. Note that the advance condition only checks if a variable is true, and it cannot check for falseness.

This gives the Advance Condition a very limited capability. If you wanted to make a transition back and forth based on one property, you would need to make 2 variables that have opposite values, and check if either of them are true. This is why, in Godot 4, the Advance Expression was added.

The Advance Expression works similar to the Advance Condition, but instead of checking if one variable is true, it evaluates any expression. An expression is anything you could put in an if statement. These are all examples of expressions that would work in the Advance Expression:

is_walking && !is_idle

Here is an example of an improperly-set-up StateMachine transition using Advance Condition:

This is not working because there is a ! variable in the Advance Condition, which cannot be checked.

Here is the same example, set up properly, using two opposite variables:

Here is the same example, but using Advance Expression rather than Advance Condition, which eliminates the need for two variables:

In order to use Advance Expressions, the Advance Expression Base Node has to be set from the Inspector of the AnimationTree node. By default, it is set to the AnimationTree node itself, but it needs to point to whatever node contains the script with your animation variables.

One of the nice features in Godot's StateMachine implementation is the ability to travel. You can instruct the graph to go from the current state to another one, while visiting all the intermediate ones. This is done via the A* algorithm. If there is no path of transitions starting at the current state and finishing at the destination state, the graph teleports to the destination state.

To use the travel ability, you should first retrieve the AnimationNodeStateMachinePlayback object from the AnimationTree node (it is exported as a property), and then call one of its many functions:

The StateMachine must be running before you can travel. Make sure to either call start() or connect a node to Start.

BlendSpace2D is a node to do advanced blending in two dimensions. Points representing animations are added to a 2D space and then a position between them is controlled to determine the blending:

You may place these points anywhere on the graph by right clicking or using the add point button, whose icon is a pen and point. Wherever you place the points, the triangle between them will be generated automatically using Delaunay. You may also control and label the ranges in X and Y.

Finally, you may also change the blend mode. By default, blending happens by interpolating points inside the closest triangle. When dealing with 2D animations (frame by frame), you may want to switch to Discrete mode. Alternatively, if you want to keep the current play position when switching between discrete animations, there is a Carry mode. This mode can be changed in the Blend menu:

BlendSpace1D works just like BlendSpace2D, but in one dimension (a line). Triangles are not used.

In Godot 4.0+, in order for the blending results to be deterministic (reproducible and always consistent), the blended property values must have a specific initial value. For example, in the case of two animations to be blended, if one animation has a property track and the other does not, the blended animation is calculated as if the latter animation had a property track with the initial value.

When using Position/Rotation/Scale 3D tracks for Skeleton3D bones, the initial value is Bone Rest. For other properties, the initial value is 0 and if the track is present in the RESET animation, the value of its first keyframe is used instead.

For example, the following AnimationPlayer has two animations, but one of them lacks a Property track for Position.

This means that the animation lacking that will treat those Positions as Vector2(0, 0).

This problem can be solved by adding a Property track for Position as an initial value to the RESET animation.

Be aware that the RESET animation exists to define the default pose when loading an object originally. It is assumed to have only one frame and is not expected to be played back using the timeline.

Also keep in mind that the Rotation 3D tracks and the Property tracks for 2D rotation with Interpolation Type set to Linear Angle or Cubic Angle will prevent rotations greater than 180 degrees from the initial value as blended animation.

This can be useful for Skeleton3Ds to prevent the bones penetrating the body when blending animations. Therefore, Skeleton3D's Bone Rest values should be as close to the midpoint of the movable range as possible. This means that for humanoid models, it is preferable to import them in a T-pose.

You can see that the shortest rotation path from Bone Rests is prioritized rather than the shortest rotation path between animations.

If you need to rotate Skeleton3D itself more than 180 degrees by blend animations for movement, you can use Root Motion.

When working with 3D animations, a popular technique is for animators to use the root skeleton bone to give motion to the rest of the skeleton. This allows animating characters in a way where steps actually match the floor below. It also allows precise interaction with objects during cinematics.

When playing back the animation in Godot, it is possible to select this bone as the root motion track. Doing so will cancel the bone transformation visually (the animation will stay in place).

Afterwards, the actual motion can be retrieved via the AnimationTree API as a transform:

This can be fed to functions such as CharacterBody3D.move_and_slide to control the character movement.

There is also a tool node, RootMotionView, you can place a scene that will act as a custom floor for your character and animations (this node is disabled by default during the game).

After building the tree and previewing it, the only question remaining is "How is all this controlled from code?".

Keep in mind that the animation nodes are just resources, so they are shared between all instances using them. Setting values in the nodes directly will affect all instances of the scene that uses this AnimationTree. This is generally undesirable, but does have some cool use cases, e.g. you can copy and paste parts of your animation tree, or reuse nodes with a complex layout (such as a StateMachine or blend space) in different animation trees.

The actual animation data is contained in the AnimationTree node and is accessed via properties. Check the "Parameters" section of the AnimationTree node to see all the parameters that can be modified in real-time:

This is handy because it makes it possible to animate them from an AnimationPlayer, or even the AnimationTree itself, allowing very complex animation logic.

To modify these values from code, you must obtain the property path. You can find them by hovering your mouse over any of the parameters:

Then you can set or read them:

Advance Expressions from a StateMachine will not be found under the parameters. This is because they are held in another script rather than the AnimationTree itself. Advance Conditions will be found under parameters.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (markdown):
```markdown
# Play child animation connected to "shot" port.
animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_FIRE)
# Alternative syntax (same result).
animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_FIRE

# Abort child animation connected to "shot" port.
animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_ABORT)
# Alternative syntax (same result).
animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_ABORT

# Get current state (read-only).
animation_tree.get("parameters/OneShot/active"))
# Alternative syntax (same result).
animation_tree["parameters/OneShot/active"]
```

Example 2 (unknown):
```unknown
// Play child animation connected to "shot" port.
animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.Fire);

// Abort child animation connected to "shot" port.
animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.Abort);

// Get current state (read-only).
animationTree.Get("parameters/OneShot/active");
```

Example 3 (sql):
```sql
# Play child animation from the start.
animation_tree.set("parameters/TimeSeek/seek_request", 0.0)
# Alternative syntax (same result).
animation_tree["parameters/TimeSeek/seek_request"] = 0.0

# Play child animation from 12 second timestamp.
animation_tree.set("parameters/TimeSeek/seek_request", 12.0)
# Alternative syntax (same result).
animation_tree["parameters/TimeSeek/seek_request"] = 12.0
```

Example 4 (sql):
```sql
// Play child animation from the start.
animationTree.Set("parameters/TimeSeek/seek_request", 0.0);

// Play child animation from 12 second timestamp.
animationTree.Set("parameters/TimeSeek/seek_request", 12.0);
```

---
