# Godot - Api

**Pages:** 12

---

## AcceptDialog — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/classes/class_acceptdialog.html

**Contents:**
- AcceptDialog
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions
- User-contributed notes

Inherits: Window < Viewport < Node < Object

Inherited By: ConfirmationDialog

A base dialog used for user notification.

The default use of AcceptDialog is to allow it to only be accepted or closed, with the same result. However, the confirmed and canceled signals allow to make the two actions different, and the add_button() method allows to add custom buttons and actions.

dialog_close_on_escape

true (overrides Window)

true (overrides Window)

true (overrides Window)

true (overrides Window)

"Alert!" (overrides Window)

true (overrides Window)

false (overrides Window)

true (overrides Window)

add_button(text: String, right: bool = false, action: String = "")

add_cancel_button(name: String)

register_text_enter(line_edit: LineEdit)

remove_button(button: Button)

Emitted when the dialog is closed or the button created with add_cancel_button() is pressed.

Emitted when the dialog is accepted, i.e. the OK button is pressed.

custom_action(action: StringName) 🔗

Emitted when a custom button with an action is pressed. See add_button().

bool dialog_autowrap = false 🔗

void set_autowrap(value: bool)

Sets autowrapping for the text in the dialog.

bool dialog_close_on_escape = true 🔗

void set_close_on_escape(value: bool)

bool get_close_on_escape()

If true, the dialog will be hidden when the ui_cancel action is pressed (by default, this action is bound to @GlobalScope.KEY_ESCAPE).

bool dialog_hide_on_ok = true 🔗

void set_hide_on_ok(value: bool)

bool get_hide_on_ok()

If true, the dialog is hidden when the OK button is pressed. You can set it to false if you want to do e.g. input validation when receiving the confirmed signal, and handle hiding the dialog in your own logic.

Note: Some nodes derived from this class can have a different default value, and potentially their own built-in logic overriding this setting. For example FileDialog defaults to false, and has its own input validation code that is called when you press OK, which eventually hides the dialog if the input is valid. As such, this property can't be used in FileDialog to disable hiding the dialog when pressing OK.

String dialog_text = "" 🔗

void set_text(value: String)

The text displayed by the dialog.

String ok_button_text = "" 🔗

void set_ok_button_text(value: String)

String get_ok_button_text()

The text displayed by the OK button (see get_ok_button()). If empty, a default text will be used.

Button add_button(text: String, right: bool = false, action: String = "") 🔗

Adds a button with label text and a custom action to the dialog and returns the created button.

If action is not empty, pressing the button will emit the custom_action signal with the specified action string.

If true, right will place the button to the right of any sibling buttons.

You can use remove_button() method to remove a button created with this method from the dialog.

Button add_cancel_button(name: String) 🔗

Adds a button with label name and a cancel action to the dialog and returns the created button.

You can use remove_button() method to remove a button created with this method from the dialog.

Returns the label used for built-in text.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their CanvasItem.visible property.

Button get_ok_button() 🔗

Returns the OK Button instance.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their CanvasItem.visible property.

void register_text_enter(line_edit: LineEdit) 🔗

Registers a LineEdit in the dialog. When the enter key is pressed, the dialog will be accepted.

void remove_button(button: Button) 🔗

Removes the button from the dialog. Does NOT free the button. The button must be a Button added with add_button() or add_cancel_button() method. After removal, pressing the button will no longer emit this dialog's custom_action or canceled signals.

int buttons_min_height = 0 🔗

The minimum height of each button in the bottom row (such as OK/Cancel) in pixels. This can be increased to make buttons with short texts easier to click/tap.

int buttons_min_width = 0 🔗

The minimum width of each button in the bottom row (such as OK/Cancel) in pixels. This can be increased to make buttons with short texts easier to click/tap.

int buttons_separation = 10 🔗

The size of the vertical space between the dialog's content and the button row.

The panel that fills the background of the window.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## AnimatableBody2D — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/classes/class_animatablebody2d.html

**Contents:**
- AnimatableBody2D
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: StaticBody2D < PhysicsBody2D < CollisionObject2D < Node2D < CanvasItem < Node < Object

A 2D physics body that can't be moved by external forces. When moved manually, it affects other bodies in its path.

An animatable 2D physics body. It can't be moved by external forces or contacts, but can be moved manually by other means such as code, AnimationMixers (with AnimationMixer.callback_mode_process set to AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS), and RemoteTransform2D.

When AnimatableBody2D is moved, its linear and angular velocity are estimated and used to affect other physics bodies in its path. This makes it useful for moving platforms, doors, and other moving objects.

Troubleshooting physics issues

bool sync_to_physics = true 🔗

void set_sync_to_physics(value: bool)

bool is_sync_to_physics_enabled()

If true, the body's movement will be synchronized to the physics frame. This is useful when animating movement via AnimationPlayer, for example on moving platforms. Do not use together with PhysicsBody2D.move_and_collide().

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## AnimatedSprite2D — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/classes/class_animatedsprite2d.html

**Contents:**
- AnimatedSprite2D
- Description
- Tutorials
- Properties
- Methods
- Signals
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Node2D < CanvasItem < Node < Object

Sprite node that contains multiple textures as frames to play for animation.

AnimatedSprite2D is similar to the Sprite2D node, except it carries multiple textures as animation frames. Animations are created using a SpriteFrames resource, which allows you to import image files (or a folder containing said files) to provide the animation frames for the sprite. The SpriteFrames resource can be configured in the editor via the SpriteFrames bottom panel.

2D Dodge The Creeps Demo

get_playing_speed() const

play(name: StringName = &"", custom_speed: float = 1.0, from_end: bool = false)

play_backwards(name: StringName = &"")

set_frame_and_progress(frame: int, progress: float)

animation_changed() 🔗

Emitted when animation changes.

animation_finished() 🔗

Emitted when the animation reaches the end, or the start if it is played in reverse. When the animation finishes, it pauses the playback.

Note: This signal is not emitted if an animation is looping.

Emitted when the animation loops.

Emitted when frame changes.

sprite_frames_changed() 🔗

Emitted when sprite_frames changes.

StringName animation = &"default" 🔗

void set_animation(value: StringName)

StringName get_animation()

The current animation from the sprite_frames resource. If this value is changed, the frame counter and the frame_progress are reset.

String autoplay = "" 🔗

void set_autoplay(value: String)

String get_autoplay()

The key of the animation to play when the scene loads.

bool centered = true 🔗

void set_centered(value: bool)

If true, texture will be centered.

Note: For games with a pixel art aesthetic, textures may appear deformed when centered. This is caused by their position being between pixels. To prevent this, set this property to false, or consider enabling ProjectSettings.rendering/2d/snap/snap_2d_vertices_to_pixel and ProjectSettings.rendering/2d/snap/snap_2d_transforms_to_pixel.

bool flip_h = false 🔗

void set_flip_h(value: bool)

If true, texture is flipped horizontally.

bool flip_v = false 🔗

void set_flip_v(value: bool)

If true, texture is flipped vertically.

void set_frame(value: int)

The displayed animation frame's index. Setting this property also resets frame_progress. If this is not desired, use set_frame_and_progress().

float frame_progress = 0.0 🔗

void set_frame_progress(value: float)

float get_frame_progress()

The progress value between 0.0 and 1.0 until the current frame transitions to the next frame. If the animation is playing backwards, the value transitions from 1.0 to 0.0.

Vector2 offset = Vector2(0, 0) 🔗

void set_offset(value: Vector2)

The texture's drawing offset.

float speed_scale = 1.0 🔗

void set_speed_scale(value: float)

float get_speed_scale()

The speed scaling ratio. For example, if this value is 1, then the animation plays at normal speed. If it's 0.5, then it plays at half speed. If it's 2, then it plays at double speed.

If set to a negative value, the animation is played in reverse. If set to 0, the animation will not advance.

SpriteFrames sprite_frames 🔗

void set_sprite_frames(value: SpriteFrames)

SpriteFrames get_sprite_frames()

The SpriteFrames resource containing the animation(s). Allows you the option to load, edit, clear, make unique and save the states of the SpriteFrames resource.

float get_playing_speed() const 🔗

Returns the actual playing speed of current animation or 0 if not playing. This speed is the speed_scale property multiplied by custom_speed argument specified when calling the play() method.

Returns a negative value if the current animation is playing backwards.

bool is_playing() const 🔗

Returns true if an animation is currently playing (even if speed_scale and/or custom_speed are 0).

Pauses the currently playing animation. The frame and frame_progress will be kept and calling play() or play_backwards() without arguments will resume the animation from the current playback position.

void play(name: StringName = &"", custom_speed: float = 1.0, from_end: bool = false) 🔗

Plays the animation with key name. If custom_speed is negative and from_end is true, the animation will play backwards (which is equivalent to calling play_backwards()).

If this method is called with that same animation name, or with no name parameter, the assigned animation will resume playing if it was paused.

void play_backwards(name: StringName = &"") 🔗

Plays the animation with key name in reverse.

This method is a shorthand for play() with custom_speed = -1.0 and from_end = true, so see its description for more information.

void set_frame_and_progress(frame: int, progress: float) 🔗

Sets frame and frame_progress to the given values. Unlike setting frame, this method does not reset the frame_progress to 0.0 implicitly.

Example: Change the animation while keeping the same frame and frame_progress:

Stops the currently playing animation. The animation position is reset to 0 and the custom_speed is reset to 1.0. See also pause().

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## AnimationMixer — Godot Engine (stable) documentation in English

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

animation_finished(anim_name: StringName) 🔗

Notifies when an animation finished playing.

Note: This signal is not emitted if an animation is looping.

animation_libraries_updated() 🔗

Notifies when the animation libraries have changed.

animation_list_changed() 🔗

Notifies when an animation list is changed.

animation_started(anim_name: StringName) 🔗

Notifies when an animation starts playing.

Note: This signal is not emitted if an animation is looping.

Notifies when the caches have been cleared, either automatically, or manually via clear_caches().

Notifies when the blending result related have been applied to the target objects.

Notifies when the property related process have been updated.

enum AnimationCallbackModeProcess: 🔗

AnimationCallbackModeProcess ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS = 0

Process animation during physics frames (see Node.NOTIFICATION_INTERNAL_PHYSICS_PROCESS). This is especially useful when animating physics bodies.

AnimationCallbackModeProcess ANIMATION_CALLBACK_MODE_PROCESS_IDLE = 1

Process animation during process frames (see Node.NOTIFICATION_INTERNAL_PROCESS).

AnimationCallbackModeProcess ANIMATION_CALLBACK_MODE_PROCESS_MANUAL = 2

Do not process animation. Use advance() to process the animation manually.

enum AnimationCallbackModeMethod: 🔗

AnimationCallbackModeMethod ANIMATION_CALLBACK_MODE_METHOD_DEFERRED = 0

Batch method calls during the animation process, then do the calls after events are processed. This avoids bugs involving deleting nodes or modifying the AnimationPlayer while playing.

AnimationCallbackModeMethod ANIMATION_CALLBACK_MODE_METHOD_IMMEDIATE = 1

Make method calls immediately when reached in the animation.

enum AnimationCallbackModeDiscrete: 🔗

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

int audio_max_polyphony = 32 🔗

void set_audio_max_polyphony(value: int)

int get_audio_max_polyphony()

The number of possible simultaneous sounds for each of the assigned AudioStreamPlayers.

For example, if this value is 32 and the animation has two audio tracks, the two AudioStreamPlayers assigned can play simultaneously up to 32 voices each.

AnimationCallbackModeDiscrete callback_mode_discrete = 1 🔗

void set_callback_mode_discrete(value: AnimationCallbackModeDiscrete)

AnimationCallbackModeDiscrete get_callback_mode_discrete()

Ordinarily, tracks can be set to Animation.UPDATE_DISCRETE to update infrequently, usually when using nearest interpolation.

However, when blending with Animation.UPDATE_CONTINUOUS several results are considered. The callback_mode_discrete specify it explicitly. See also AnimationCallbackModeDiscrete.

To make the blended results look good, it is recommended to set this to ANIMATION_CALLBACK_MODE_DISCRETE_FORCE_CONTINUOUS to update every frame during blending. Other values exist for compatibility and they are fine if there is no blending, but not so, may produce artifacts.

AnimationCallbackModeMethod callback_mode_method = 0 🔗

void set_callback_mode_method(value: AnimationCallbackModeMethod)

AnimationCallbackModeMethod get_callback_mode_method()

The call mode used for "Call Method" tracks.

AnimationCallbackModeProcess callback_mode_process = 1 🔗

void set_callback_mode_process(value: AnimationCallbackModeProcess)

AnimationCallbackModeProcess get_callback_mode_process()

The process notification in which to update animations.

bool deterministic = false 🔗

void set_deterministic(value: bool)

bool is_deterministic()

If true, the blending uses the deterministic algorithm. The total weight is not normalized and the result is accumulated with an initial value (0 or a "RESET" animation if present).

This means that if the total amount of blending is 0.0, the result is equal to the "RESET" animation.

If the number of tracks between the blended animations is different, the animation with the missing track is treated as if it had the initial value.

If false, The blend does not use the deterministic algorithm. The total weight is normalized and always 1.0. If the number of tracks between the blended animations is different, nothing is done about the animation that is missing a track.

Note: In AnimationTree, the blending with AnimationNodeAdd2, AnimationNodeAdd3, AnimationNodeSub2 or the weight greater than 1.0 may produce unexpected results.

For example, if AnimationNodeAdd2 blends two nodes with the amount 1.0, then total weight is 2.0 but it will be normalized to make the total amount 1.0 and the result will be equal to AnimationNodeBlend2 with the amount 0.5.

bool reset_on_save = true 🔗

void set_reset_on_save_enabled(value: bool)

bool is_reset_on_save_enabled()

This is used by the editor. If set to true, the scene will be saved with the effects of the reset animation (the animation with the key "RESET") applied as if it had been seeked to time 0, with the editor keeping the values that the scene had before saving.

This makes it more convenient to preview and edit animations in the editor, as changes to the scene will not be saved as long as they are set in the reset animation.

bool root_motion_local = false 🔗

void set_root_motion_local(value: bool)

bool is_root_motion_local()

If true, get_root_motion_position() value is extracted as a local translation value before blending. In other words, it is treated like the translation is done after the rotation.

NodePath root_motion_track = NodePath("") 🔗

void set_root_motion_track(value: NodePath)

NodePath get_root_motion_track()

The path to the Animation track used for root motion. Paths must be valid scene-tree paths to a node, and must be specified starting from the parent node of the node that will reproduce the animation. The root_motion_track uses the same format as Animation.track_set_path(), but note that a bone must be specified.

If the track has type Animation.TYPE_POSITION_3D, Animation.TYPE_ROTATION_3D, or Animation.TYPE_SCALE_3D the transformation will be canceled visually, and the animation will appear to stay in place. See also get_root_motion_position(), get_root_motion_rotation(), get_root_motion_scale(), and RootMotionView.

NodePath root_node = NodePath("..") 🔗

void set_root_node(value: NodePath)

NodePath get_root_node()

The node which node path references will travel from.

Variant _post_process_key_value(animation: Animation, track: int, value: Variant, object_id: int, object_sub_idx: int) virtual const 🔗

A virtual function for processing after getting a key during playback.

Error add_animation_library(name: StringName, library: AnimationLibrary) 🔗

Adds library to the animation player, under the key name.

AnimationMixer has a global library by default with an empty string as key. For adding an animation to the global library:

void advance(delta: float) 🔗

Manually advance the animations by the specified time (in seconds).

void capture(name: StringName, duration: float, trans_type: TransitionType = 0, ease_type: EaseType = 0) 🔗

If the animation track specified by name has an option Animation.UPDATE_CAPTURE, stores current values of the objects indicated by the track path as a cache. If there is already a captured cache, the old cache is discarded.

After this it will interpolate with current animation blending result during the playback process for the time specified by duration, working like a crossfade.

You can specify trans_type as the curve for the interpolation. For better results, it may be appropriate to specify Tween.TRANS_LINEAR for cases where the first key of the track begins with a non-zero value or where the key value does not change, and Tween.TRANS_QUAD for cases where the key value changes linearly.

void clear_caches() 🔗

AnimationMixer caches animated nodes. It may not notice if a node disappears; clear_caches() forces it to update the cache again.

StringName find_animation(animation: Animation) const 🔗

Returns the key of animation or an empty StringName if not found.

StringName find_animation_library(animation: Animation) const 🔗

Returns the key for the AnimationLibrary that contains animation or an empty StringName if not found.

Animation get_animation(name: StringName) const 🔗

Returns the Animation with the key name. If the animation does not exist, null is returned and an error is logged.

AnimationLibrary get_animation_library(name: StringName) const 🔗

Returns the first AnimationLibrary with key name or null if not found.

To get the AnimationMixer's global animation library, use get_animation_library("").

Array[StringName] get_animation_library_list() const 🔗

Returns the list of stored library keys.

PackedStringArray get_animation_list() const 🔗

Returns the list of stored animation keys.

Vector3 get_root_motion_position() const 🔗

Retrieve the motion delta of position with the root_motion_track as a Vector3 that can be used elsewhere.

If root_motion_track is not a path to a track of type Animation.TYPE_POSITION_3D, returns Vector3(0, 0, 0).

See also root_motion_track and RootMotionView.

The most basic example is applying position to CharacterBody3D:

By using this in combination with get_root_motion_rotation_accumulator(), you can apply the root motion position more correctly to account for the rotation of the node.

If root_motion_local is true, returns the pre-multiplied translation value with the inverted rotation.

In this case, the code can be written as follows:

Vector3 get_root_motion_position_accumulator() const 🔗

Retrieve the blended value of the position tracks with the root_motion_track as a Vector3 that can be used elsewhere.

This is useful in cases where you want to respect the initial key values of the animation.

For example, if an animation with only one key Vector3(0, 0, 0) is played in the previous frame and then an animation with only one key Vector3(1, 0, 1) is played in the next frame, the difference can be calculated as follows:

However, if the animation loops, an unintended discrete change may occur, so this is only useful for some simple use cases.

Quaternion get_root_motion_rotation() const 🔗

Retrieve the motion delta of rotation with the root_motion_track as a Quaternion that can be used elsewhere.

If root_motion_track is not a path to a track of type Animation.TYPE_ROTATION_3D, returns Quaternion(0, 0, 0, 1).

See also root_motion_track and RootMotionView.

The most basic example is applying rotation to CharacterBody3D:

Quaternion get_root_motion_rotation_accumulator() const 🔗

Retrieve the blended value of the rotation tracks with the root_motion_track as a Quaternion that can be used elsewhere.

This is necessary to apply the root motion position correctly, taking rotation into account. See also get_root_motion_position().

Also, this is useful in cases where you want to respect the initial key values of the animation.

For example, if an animation with only one key Quaternion(0, 0, 0, 1) is played in the previous frame and then an animation with only one key Quaternion(0, 0.707, 0, 0.707) is played in the next frame, the difference can be calculated as follows:

However, if the animation loops, an unintended discrete change may occur, so this is only useful for some simple use cases.

Vector3 get_root_motion_scale() const 🔗

Retrieve the motion delta of scale with the root_motion_track as a Vector3 that can be used elsewhere.

If root_motion_track is not a path to a track of type Animation.TYPE_SCALE_3D, returns Vector3(0, 0, 0).

See also root_motion_track and RootMotionView.

The most basic example is applying scale to CharacterBody3D:

Vector3 get_root_motion_scale_accumulator() const 🔗

Retrieve the blended value of the scale tracks with the root_motion_track as a Vector3 that can be used elsewhere.

For example, if an animation with only one key Vector3(1, 1, 1) is played in the previous frame and then an animation with only one key Vector3(2, 2, 2) is played in the next frame, the difference can be calculated as follows:

However, if the animation loops, an unintended discrete change may occur, so this is only useful for some simple use cases.

bool has_animation(name: StringName) const 🔗

Returns true if the AnimationMixer stores an Animation with key name.

bool has_animation_library(name: StringName) const 🔗

Returns true if the AnimationMixer stores an AnimationLibrary with key name.

void remove_animation_library(name: StringName) 🔗

Removes the AnimationLibrary associated with the key name.

void rename_animation_library(name: StringName, newname: StringName) 🔗

Moves the AnimationLibrary associated with the key name to the key newname.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## AnimationPlayer — Godot Engine (stable) documentation in English

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

animation_changed(old_name: StringName, new_name: StringName) 🔗

Emitted when a queued animation plays after the previous animation finished. See also queue().

Note: The signal is not emitted when the animation is changed via play() or by an AnimationTree.

current_animation_changed(name: String) 🔗

Emitted when current_animation changes.

enum AnimationProcessCallback: 🔗

AnimationProcessCallback ANIMATION_PROCESS_PHYSICS = 0

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS.

AnimationProcessCallback ANIMATION_PROCESS_IDLE = 1

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_IDLE.

AnimationProcessCallback ANIMATION_PROCESS_MANUAL = 2

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_MANUAL.

enum AnimationMethodCallMode: 🔗

AnimationMethodCallMode ANIMATION_METHOD_CALL_DEFERRED = 0

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_METHOD_DEFERRED.

AnimationMethodCallMode ANIMATION_METHOD_CALL_IMMEDIATE = 1

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_METHOD_IMMEDIATE.

String assigned_animation 🔗

void set_assigned_animation(value: String)

String get_assigned_animation()

If playing, the current animation's key, otherwise, the animation last played. When set, this changes the animation, but will not play it unless already playing. See also current_animation.

String autoplay = "" 🔗

void set_autoplay(value: String)

String get_autoplay()

The key of the animation to play when the scene loads.

String current_animation = "" 🔗

void set_current_animation(value: String)

String get_current_animation()

The key of the currently playing animation. If no animation is playing, the property's value is an empty string. Changing this value does not restart the animation. See play() for more information on playing animations.

Note: While this property appears in the Inspector, it's not meant to be edited, and it's not saved in the scene. This property is mainly used to get the currently playing animation, and internally for animation playback tracks. For more information, see Animation.

float current_animation_length 🔗

float get_current_animation_length()

The length (in seconds) of the currently playing animation.

float current_animation_position 🔗

float get_current_animation_position()

The position (in seconds) of the currently playing animation.

bool movie_quit_on_finish = false 🔗

void set_movie_quit_on_finish_enabled(value: bool)

bool is_movie_quit_on_finish_enabled()

If true and the engine is running in Movie Maker mode (see MovieWriter), exits the engine with SceneTree.quit() as soon as an animation is done playing in this AnimationPlayer. A message is printed when the engine quits for this reason.

Note: This obeys the same logic as the AnimationMixer.animation_finished signal, so it will not quit the engine if the animation is set to be looping.

bool playback_auto_capture = true 🔗

void set_auto_capture(value: bool)

bool is_auto_capture()

If true, performs AnimationMixer.capture() before playback automatically. This means just play_with_capture() is executed with default arguments instead of play().

Note: Capture interpolation is only performed if the animation contains a capture track. See also Animation.UPDATE_CAPTURE.

float playback_auto_capture_duration = -1.0 🔗

void set_auto_capture_duration(value: float)

float get_auto_capture_duration()

See also play_with_capture() and AnimationMixer.capture().

If playback_auto_capture_duration is negative value, the duration is set to the interval between the current position and the first key.

EaseType playback_auto_capture_ease_type = 0 🔗

void set_auto_capture_ease_type(value: EaseType)

EaseType get_auto_capture_ease_type()

The ease type of the capture interpolation. See also EaseType.

TransitionType playback_auto_capture_transition_type = 0 🔗

void set_auto_capture_transition_type(value: TransitionType)

TransitionType get_auto_capture_transition_type()

The transition type of the capture interpolation. See also TransitionType.

float playback_default_blend_time = 0.0 🔗

void set_default_blend_time(value: float)

float get_default_blend_time()

The default time in which to blend animations. Ranges from 0 to 4096 with 0.01 precision.

float speed_scale = 1.0 🔗

void set_speed_scale(value: float)

float get_speed_scale()

The speed scaling ratio. For example, if this value is 1, then the animation plays at normal speed. If it's 0.5, then it plays at half speed. If it's 2, then it plays at double speed.

If set to a negative value, the animation is played in reverse. If set to 0, the animation will not advance.

StringName animation_get_next(animation_from: StringName) const 🔗

Returns the key of the animation which is queued to play after the animation_from animation.

void animation_set_next(animation_from: StringName, animation_to: StringName) 🔗

Triggers the animation_to animation when the animation_from animation completes.

Clears all queued, unplayed animations.

float get_blend_time(animation_from: StringName, animation_to: StringName) const 🔗

Returns the blend time (in seconds) between two animations, referenced by their keys.

AnimationMethodCallMode get_method_call_mode() const 🔗

Deprecated: Use AnimationMixer.callback_mode_method instead.

Returns the call mode used for "Call Method" tracks.

float get_playing_speed() const 🔗

Returns the actual playing speed of current animation or 0 if not playing. This speed is the speed_scale property multiplied by custom_speed argument specified when calling the play() method.

Returns a negative value if the current animation is playing backwards.

AnimationProcessCallback get_process_callback() const 🔗

Deprecated: Use AnimationMixer.callback_mode_process instead.

Returns the process notification in which to update animations.

PackedStringArray get_queue() 🔗

Returns a list of the animation keys that are currently queued to play.

NodePath get_root() const 🔗

Deprecated: Use AnimationMixer.root_node instead.

Returns the node which node path references will travel from.

float get_section_end_time() const 🔗

Returns the end time of the section currently being played.

float get_section_start_time() const 🔗

Returns the start time of the section currently being played.

bool has_section() const 🔗

Returns true if an animation is currently playing with a section.

bool is_playing() const 🔗

Returns true if an animation is currently playing (even if speed_scale and/or custom_speed are 0).

Pauses the currently playing animation. The current_animation_position will be kept and calling play() or play_backwards() without arguments or with the same animation name as assigned_animation will resume the animation.

void play(name: StringName = &"", custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false) 🔗

Plays the animation with key name. Custom blend times and speed can be set.

The from_end option only affects when switching to a new animation track, or if the same track but at the start or end. It does not affect resuming playback that was paused in the middle of an animation. If custom_speed is negative and from_end is true, the animation will play backwards (which is equivalent to calling play_backwards()).

The AnimationPlayer keeps track of its current or last played animation with assigned_animation. If this method is called with that same animation name, or with no name parameter, the assigned animation will resume playing if it was paused.

Note: The animation will be updated the next time the AnimationPlayer is processed. If other variables are updated at the same time this is called, they may be updated too early. To perform the update immediately, call advance(0).

void play_backwards(name: StringName = &"", custom_blend: float = -1) 🔗

Plays the animation with key name in reverse.

This method is a shorthand for play() with custom_speed = -1.0 and from_end = true, so see its description for more information.

void play_section(name: StringName = &"", start_time: float = -1, end_time: float = -1, custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false) 🔗

Plays the animation with key name and the section starting from start_time and ending on end_time. See also play().

Setting start_time to a value outside the range of the animation means the start of the animation will be used instead, and setting end_time to a value outside the range of the animation means the end of the animation will be used instead. start_time cannot be equal to end_time.

void play_section_backwards(name: StringName = &"", start_time: float = -1, end_time: float = -1, custom_blend: float = -1) 🔗

Plays the animation with key name and the section starting from start_time and ending on end_time in reverse.

This method is a shorthand for play_section() with custom_speed = -1.0 and from_end = true, see its description for more information.

void play_section_with_markers(name: StringName = &"", start_marker: StringName = &"", end_marker: StringName = &"", custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false) 🔗

Plays the animation with key name and the section starting from start_marker and ending on end_marker.

If the start marker is empty, the section starts from the beginning of the animation. If the end marker is empty, the section ends on the end of the animation. See also play().

void play_section_with_markers_backwards(name: StringName = &"", start_marker: StringName = &"", end_marker: StringName = &"", custom_blend: float = -1) 🔗

Plays the animation with key name and the section starting from start_marker and ending on end_marker in reverse.

This method is a shorthand for play_section_with_markers() with custom_speed = -1.0 and from_end = true, see its description for more information.

void play_with_capture(name: StringName = &"", duration: float = -1.0, custom_blend: float = -1, custom_speed: float = 1.0, from_end: bool = false, trans_type: TransitionType = 0, ease_type: EaseType = 0) 🔗

See also AnimationMixer.capture().

You can use this method to use more detailed options for capture than those performed by playback_auto_capture. When playback_auto_capture is false, this method is almost the same as the following:

If name is blank, it specifies assigned_animation.

If duration is a negative value, the duration is set to the interval between the current position and the first key, when from_end is true, uses the interval between the current position and the last key instead.

Note: The duration takes speed_scale into account, but custom_speed does not, because the capture cache is interpolated with the blend result and the result may contain multiple animations.

void queue(name: StringName) 🔗

Queues an animation for playback once the current animation and all previously queued animations are done.

Note: If a looped animation is currently playing, the queued animation will never play unless the looped animation is stopped somehow.

void reset_section() 🔗

Resets the current section. Does nothing if a section has not been set.

void seek(seconds: float, update: bool = false, update_only: bool = false) 🔗

Seeks the animation to the seconds point in time (in seconds). If update is true, the animation updates too, otherwise it updates at process time. Events between the current frame and seconds are skipped.

If update_only is true, the method / audio / animation playback tracks will not be processed.

Note: Seeking to the end of the animation doesn't emit AnimationMixer.animation_finished. If you want to skip animation and emit the signal, use AnimationMixer.advance().

void set_blend_time(animation_from: StringName, animation_to: StringName, sec: float) 🔗

Specifies a blend time (in seconds) between two animations, referenced by their keys.

void set_method_call_mode(mode: AnimationMethodCallMode) 🔗

Deprecated: Use AnimationMixer.callback_mode_method instead.

Sets the call mode used for "Call Method" tracks.

void set_process_callback(mode: AnimationProcessCallback) 🔗

Deprecated: Use AnimationMixer.callback_mode_process instead.

Sets the process notification in which to update animations.

void set_root(path: NodePath) 🔗

Deprecated: Use AnimationMixer.root_node instead.

Sets the node which node path references will travel from.

void set_section(start_time: float = -1, end_time: float = -1) 🔗

Changes the start and end times of the section being played. The current playback position will be clamped within the new section. See also play_section().

void set_section_with_markers(start_marker: StringName = &"", end_marker: StringName = &"") 🔗

Changes the start and end markers of the section being played. The current playback position will be clamped within the new section. See also play_section_with_markers().

If the argument is empty, the section uses the beginning or end of the animation. If both are empty, it means that the section is not set.

void stop(keep_state: bool = false) 🔗

Stops the currently playing animation. The animation position is reset to 0 and the custom_speed is reset to 1.0. See also pause().

If keep_state is true, the animation state is not updated visually.

Note: The method / audio / animation playback tracks will not be processed by this method.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## AnimationTree — Godot Engine (stable) documentation in English

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

animation_player_changed() 🔗

Emitted when the anim_player is changed.

enum AnimationProcessCallback: 🔗

AnimationProcessCallback ANIMATION_PROCESS_PHYSICS = 0

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS.

AnimationProcessCallback ANIMATION_PROCESS_IDLE = 1

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_IDLE.

AnimationProcessCallback ANIMATION_PROCESS_MANUAL = 2

Deprecated: See AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_MANUAL.

NodePath advance_expression_base_node = NodePath(".") 🔗

void set_advance_expression_base_node(value: NodePath)

NodePath get_advance_expression_base_node()

The path to the Node used to evaluate the AnimationNode Expression if one is not explicitly specified internally.

NodePath anim_player = NodePath("") 🔗

void set_animation_player(value: NodePath)

NodePath get_animation_player()

The path to the AnimationPlayer used for animating.

AnimationRootNode tree_root 🔗

void set_tree_root(value: AnimationRootNode)

AnimationRootNode get_tree_root()

The root animation node of this AnimationTree. See AnimationRootNode.

AnimationProcessCallback get_process_callback() const 🔗

Deprecated: Use AnimationMixer.callback_mode_process instead.

Returns the process notification in which to update animations.

void set_process_callback(mode: AnimationProcessCallback) 🔗

Deprecated: Use AnimationMixer.callback_mode_process instead.

Sets the process notification in which to update animations.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Area2D — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/classes/class_area2d.html

**Contents:**
- Area2D
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: CollisionObject2D < Node2D < CanvasItem < Node < Object

A region of 2D space that detects other CollisionObject2Ds entering or exiting it.

Area2D is a region of 2D space defined by one or multiple CollisionShape2D or CollisionPolygon2D child nodes. It detects when other CollisionObject2Ds enter or exit it, and it also keeps track of which collision objects haven't exited it yet (i.e. which one are overlapping it).

This node can also locally alter or override physics parameters (gravity, damping) and route audio to custom audio buses.

Note: Areas and bodies created with PhysicsServer2D might not interact as expected with Area2Ds, and might not emit signals or track objects correctly.

2D Dodge The Creeps Demo

angular_damp_space_override

gravity_point_unit_distance

gravity_space_override

linear_damp_space_override

get_overlapping_areas() const

get_overlapping_bodies() const

has_overlapping_areas() const

has_overlapping_bodies() const

overlaps_area(area: Node) const

overlaps_body(body: Node) const

area_entered(area: Area2D) 🔗

Emitted when the received area enters this area. Requires monitoring to be set to true.

area_exited(area: Area2D) 🔗

Emitted when the received area exits this area. Requires monitoring to be set to true.

area_shape_entered(area_rid: RID, area: Area2D, area_shape_index: int, local_shape_index: int) 🔗

Emitted when a Shape2D of the received area enters a shape of this area. Requires monitoring to be set to true.

local_shape_index and area_shape_index contain indices of the interacting shapes from this area and the other area, respectively. area_rid contains the RID of the other area. These values can be used with the PhysicsServer2D.

Example: Get the CollisionShape2D node from the shape index:

area_shape_exited(area_rid: RID, area: Area2D, area_shape_index: int, local_shape_index: int) 🔗

Emitted when a Shape2D of the received area exits a shape of this area. Requires monitoring to be set to true.

See also area_shape_entered.

body_entered(body: Node2D) 🔗

Emitted when the received body enters this area. body can be a PhysicsBody2D or a TileMap. TileMaps are detected if their TileSet has collision shapes configured. Requires monitoring to be set to true.

body_exited(body: Node2D) 🔗

Emitted when the received body exits this area. body can be a PhysicsBody2D or a TileMap. TileMaps are detected if their TileSet has collision shapes configured. Requires monitoring to be set to true.

body_shape_entered(body_rid: RID, body: Node2D, body_shape_index: int, local_shape_index: int) 🔗

Emitted when a Shape2D of the received body enters a shape of this area. body can be a PhysicsBody2D or a TileMap. TileMaps are detected if their TileSet has collision shapes configured. Requires monitoring to be set to true.

local_shape_index and body_shape_index contain indices of the interacting shapes from this area and the interacting body, respectively. body_rid contains the RID of the body. These values can be used with the PhysicsServer2D.

Example: Get the CollisionShape2D node from the shape index:

body_shape_exited(body_rid: RID, body: Node2D, body_shape_index: int, local_shape_index: int) 🔗

Emitted when a Shape2D of the received body exits a shape of this area. body can be a PhysicsBody2D or a TileMap. TileMaps are detected if their TileSet has collision shapes configured. Requires monitoring to be set to true.

See also body_shape_entered.

enum SpaceOverride: 🔗

SpaceOverride SPACE_OVERRIDE_DISABLED = 0

This area does not affect gravity/damping.

SpaceOverride SPACE_OVERRIDE_COMBINE = 1

This area adds its gravity/damping values to whatever has been calculated so far (in priority order).

SpaceOverride SPACE_OVERRIDE_COMBINE_REPLACE = 2

This area adds its gravity/damping values to whatever has been calculated so far (in priority order), ignoring any lower priority areas.

SpaceOverride SPACE_OVERRIDE_REPLACE = 3

This area replaces any gravity/damping, even the defaults, ignoring any lower priority areas.

SpaceOverride SPACE_OVERRIDE_REPLACE_COMBINE = 4

This area replaces any gravity/damping calculated so far (in priority order), but keeps calculating the rest of the areas.

float angular_damp = 1.0 🔗

void set_angular_damp(value: float)

float get_angular_damp()

The rate at which objects stop spinning in this area. Represents the angular velocity lost per second.

See ProjectSettings.physics/2d/default_angular_damp for more details about damping.

SpaceOverride angular_damp_space_override = 0 🔗

void set_angular_damp_space_override_mode(value: SpaceOverride)

SpaceOverride get_angular_damp_space_override_mode()

Override mode for angular damping calculations within this area.

StringName audio_bus_name = &"Master" 🔗

void set_audio_bus_name(value: StringName)

StringName get_audio_bus_name()

The name of the area's audio bus.

bool audio_bus_override = false 🔗

void set_audio_bus_override(value: bool)

bool is_overriding_audio_bus()

If true, the area's audio bus overrides the default audio bus.

float gravity = 980.0 🔗

void set_gravity(value: float)

The area's gravity intensity (in pixels per second squared). This value multiplies the gravity direction. This is useful to alter the force of gravity without altering its direction.

Vector2 gravity_direction = Vector2(0, 1) 🔗

void set_gravity_direction(value: Vector2)

Vector2 get_gravity_direction()

The area's gravity vector (not normalized).

bool gravity_point = false 🔗

void set_gravity_is_point(value: bool)

bool is_gravity_a_point()

If true, gravity is calculated from a point (set via gravity_point_center). See also gravity_space_override.

Vector2 gravity_point_center = Vector2(0, 1) 🔗

void set_gravity_point_center(value: Vector2)

Vector2 get_gravity_point_center()

If gravity is a point (see gravity_point), this will be the point of attraction.

float gravity_point_unit_distance = 0.0 🔗

void set_gravity_point_unit_distance(value: float)

float get_gravity_point_unit_distance()

The distance at which the gravity strength is equal to gravity. For example, on a planet 100 pixels in radius with a surface gravity of 4.0 px/s², set the gravity to 4.0 and the unit distance to 100.0. The gravity will have falloff according to the inverse square law, so in the example, at 200 pixels from the center the gravity will be 1.0 px/s² (twice the distance, 1/4th the gravity), at 50 pixels it will be 16.0 px/s² (half the distance, 4x the gravity), and so on.

The above is true only when the unit distance is a positive number. When this is set to 0.0, the gravity will be constant regardless of distance.

SpaceOverride gravity_space_override = 0 🔗

void set_gravity_space_override_mode(value: SpaceOverride)

SpaceOverride get_gravity_space_override_mode()

Override mode for gravity calculations within this area.

float linear_damp = 0.1 🔗

void set_linear_damp(value: float)

float get_linear_damp()

The rate at which objects stop moving in this area. Represents the linear velocity lost per second.

See ProjectSettings.physics/2d/default_linear_damp for more details about damping.

SpaceOverride linear_damp_space_override = 0 🔗

void set_linear_damp_space_override_mode(value: SpaceOverride)

SpaceOverride get_linear_damp_space_override_mode()

Override mode for linear damping calculations within this area.

bool monitorable = true 🔗

void set_monitorable(value: bool)

bool is_monitorable()

If true, other monitoring areas can detect this area.

bool monitoring = true 🔗

void set_monitoring(value: bool)

If true, the area detects bodies or areas entering and exiting it.

void set_priority(value: int)

The area's priority. Higher priority areas are processed first. The World2D's physics is always processed last, after all areas.

Array[Area2D] get_overlapping_areas() const 🔗

Returns a list of intersecting Area2Ds. The overlapping area's CollisionObject2D.collision_layer must be part of this area's CollisionObject2D.collision_mask in order to be detected.

For performance reasons (collisions are all processed at the same time) this list is modified once during the physics step, not immediately after objects are moved. Consider using signals instead.

Array[Node2D] get_overlapping_bodies() const 🔗

Returns a list of intersecting PhysicsBody2Ds and TileMaps. The overlapping body's CollisionObject2D.collision_layer must be part of this area's CollisionObject2D.collision_mask in order to be detected.

For performance reasons (collisions are all processed at the same time) this list is modified once during the physics step, not immediately after objects are moved. Consider using signals instead.

bool has_overlapping_areas() const 🔗

Returns true if intersecting any Area2Ds, otherwise returns false. The overlapping area's CollisionObject2D.collision_layer must be part of this area's CollisionObject2D.collision_mask in order to be detected.

For performance reasons (collisions are all processed at the same time) the list of overlapping areas is modified once during the physics step, not immediately after objects are moved. Consider using signals instead.

bool has_overlapping_bodies() const 🔗

Returns true if intersecting any PhysicsBody2Ds or TileMaps, otherwise returns false. The overlapping body's CollisionObject2D.collision_layer must be part of this area's CollisionObject2D.collision_mask in order to be detected.

For performance reasons (collisions are all processed at the same time) the list of overlapping bodies is modified once during the physics step, not immediately after objects are moved. Consider using signals instead.

bool overlaps_area(area: Node) const 🔗

Returns true if the given Area2D intersects or overlaps this Area2D, false otherwise.

Note: The result of this test is not immediate after moving objects. For performance, the list of overlaps is updated once per frame and before the physics step. Consider using signals instead.

bool overlaps_body(body: Node) const 🔗

Returns true if the given physics body intersects or overlaps this Area2D, false otherwise.

Note: The result of this test is not immediate after moving objects. For performance, list of overlaps is updated once per frame and before the physics step. Consider using signals instead.

The body argument can either be a PhysicsBody2D or a TileMap instance. While TileMaps are not physics bodies themselves, they register their tiles with collision shapes as a virtual physics body.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## AspectRatioContainer — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/classes/class_aspectratiocontainer.html

**Contents:**
- AspectRatioContainer
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: Container < Control < CanvasItem < Node < Object

A container that preserves the proportions of its child controls.

A container type that arranges its child controls in a way that preserves their proportions automatically when the container is resized. Useful when a container has a dynamic size and the child nodes must adjust their sizes accordingly without losing their aspect ratios.

StretchMode STRETCH_WIDTH_CONTROLS_HEIGHT = 0

The height of child controls is automatically adjusted based on the width of the container.

StretchMode STRETCH_HEIGHT_CONTROLS_WIDTH = 1

The width of child controls is automatically adjusted based on the height of the container.

StretchMode STRETCH_FIT = 2

The bounding rectangle of child controls is automatically adjusted to fit inside the container while keeping the aspect ratio.

StretchMode STRETCH_COVER = 3

The width and height of child controls is automatically adjusted to make their bounding rectangle cover the entire area of the container while keeping the aspect ratio.

When the bounding rectangle of child controls exceed the container's size and Control.clip_contents is enabled, this allows to show only the container's area restricted by its own bounding rectangle.

enum AlignmentMode: 🔗

AlignmentMode ALIGNMENT_BEGIN = 0

Aligns child controls with the beginning (left or top) of the container.

AlignmentMode ALIGNMENT_CENTER = 1

Aligns child controls with the center of the container.

AlignmentMode ALIGNMENT_END = 2

Aligns child controls with the end (right or bottom) of the container.

AlignmentMode alignment_horizontal = 1 🔗

void set_alignment_horizontal(value: AlignmentMode)

AlignmentMode get_alignment_horizontal()

Specifies the horizontal relative position of child controls.

AlignmentMode alignment_vertical = 1 🔗

void set_alignment_vertical(value: AlignmentMode)

AlignmentMode get_alignment_vertical()

Specifies the vertical relative position of child controls.

void set_ratio(value: float)

The aspect ratio to enforce on child controls. This is the width divided by the height. The ratio depends on the stretch_mode.

StretchMode stretch_mode = 2 🔗

void set_stretch_mode(value: StretchMode)

StretchMode get_stretch_mode()

The stretch mode used to align child controls.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Documentation changelog — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/about/docs_changelog.html

**Contents:**
- Documentation changelog
- New pages since version 4.3
  - 2D
  - 3D
  - Debug
  - Editor
  - Performance
  - Physics
  - Rendering
  - Shaders

The documentation is continually being improved. New releases include new pages, fixes and updates to existing pages, and many updates to the class reference. Below is a list of new pages added since version 3.0.

This document only contains new pages so not all changes are reflected, many pages have been substantially updated but are not reflected in this document.

Third-person camera with spring arm

Reducing stutter from shader (pipeline) compilations

Physics Interpolation

Using physics interpolation

Advanced physics interpolation

2D and 3D physics interpolation

Overview of renderers

Handling compatibility breakages

The .gdextension file

Upgrading from Godot 4.2 to Godot 4.3

A better XR start script

Where to go from here

OpenXR composition layers

2D coordinate systems and 2D transforms

Upgrading from Godot 4.1 to Godot 4.2

Runtime file loading and saving

Godot Android library

Internal rendering architecture

Upgrading from Godot 4.0 to Godot 4.1

Troubleshooting physics issues

Faking global illumination

Introduction to global illumination

Mesh level of detail (LOD)

Signed distance field global illumination (SDFGI)

Visibility ranges (HLOD)

Volumetric fog and fog volumes

Variable rate shading

Physical light and camera units

Retargeting 3D Skeletons

Custom platform ports

Upgrading from Godot 3 to Godot 4

Large world coordinates

Custom performance monitors

Using compute shaders

Managing editor features

GDScript documentation comments

3D rendering limitations

Version control systems

Configuring an IDE: Code::Blocks

Default editor shortcuts

Exporting for dedicated servers

Controllers, gamepads, and joysticks

Random number generation

HTML5 shell class reference

Collision shapes (2D)

Collision shapes (3D)

Creating script templates

Evaluating expressions

GDScript warning system (split from Static typing in GDScript)

Gradle builds for Android

Recording with microphone

Sync the gameplay with audio and music

Beziers, curves and paths

Localization using gettext (PO files)

Introduction to shaders

Your second 3D shader

Godot Android plugins

Visual Shader plugins

Using multiple threads

Using the SurfaceTool

Using the MeshDataTool

Optimization using MultiMeshes

Optimization using Servers

Complying with licenses

Static typing in GDScript

Applying object-oriented principles in Godot

When to use scenes versus scripts

Autoloads versus regular nodes

When and how to avoid using nodes for everything

2D lights and shadows

Prototyping levels with CSG

Animating thousands of fish with MultiMeshInstance3D

Controlling thousands of fish with Particles

Using a SubViewport as a texture

Custom post-processing

Converting GLSL to Godot shaders

Advanced post-processing

Introduction to shaders

Making main screen plugins

Custom HTML page for Web export

Fixing jitter, stutter and input lag

Running code in the editor

Change scenes manually

Optimizing a build for size

Compiling with PCK encryption key

Binding to external libraries

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## @GDScript — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/classes/class_%40gdscript.html

**Contents:**
- @GDScript
- Description
- Tutorials
- Methods
- Constants
- Annotations
- Method Descriptions
- User-contributed notes

Built-in GDScript constants, functions, and annotations.

A list of utility functions and annotations accessible from any script written in GDScript.

For the list of global functions and constants that can be accessed in any scripting language, see @GlobalScope.

Color8(r8: int, g8: int, b8: int, a8: int = 255)

assert(condition: bool, message: String = "")

convert(what: Variant, type: Variant.Type)

dict_to_inst(dictionary: Dictionary)

inst_to_dict(instance: Object)

is_instance_of(value: Variant, type: Variant)

preload(path: String)

print_debug(...) vararg

type_exists(type: StringName)

PI = 3.14159265358979 🔗

Constant that represents how many times the diameter of a circle fits around its perimeter. This is equivalent to TAU / 2, or 180 degrees in rotations.

TAU = 6.28318530717959 🔗

The circle constant, the circumference of the unit circle in radians. This is equivalent to PI * 2, or 360 degrees in rotations.

Positive floating-point infinity. This is the result of floating-point division when the divisor is 0.0. For negative infinity, use -INF. Dividing by -0.0 will result in negative infinity if the numerator is positive, so dividing by 0.0 is not the same as dividing by -0.0 (despite 0.0 == -0.0 returning true).

Warning: Numeric infinity is only a concept with floating-point numbers, and has no equivalent for integers. Dividing an integer number by 0 will not result in INF and will result in a run-time error instead.

"Not a Number", an invalid floating-point value. It is returned by some invalid operations, such as dividing floating-point 0.0 by 0.0.

NAN has special properties, including that != always returns true, while other comparison operators always return false. This is true even when comparing with itself (NAN == NAN returns false and NAN != NAN returns true). Due to this, you must use @GlobalScope.is_nan() to check whether a number is equal to NAN.

Warning: "Not a Number" is only a concept with floating-point numbers, and has no equivalent for integers. Dividing an integer 0 by 0 will not result in NAN and will result in a run-time error instead.

Marks a class or a method as abstract.

An abstract class is a class that cannot be instantiated directly. Instead, it is meant to be inherited by other classes. Attempting to instantiate an abstract class will result in an error.

An abstract method is a method that has no implementation. Therefore, a newline or a semicolon is expected after the function header. This defines a contract that inheriting classes must conform to, because the method signature must be compatible when overriding.

Inheriting classes must either provide implementations for all abstract methods, or the inheriting class must be marked as abstract. If a class has at least one abstract method (either its own or an unimplemented inherited one), then it must also be marked as abstract. However, the reverse is not true: an abstract class is allowed to have no abstract methods.

Mark the following property as exported (editable in the Inspector dock and saved to disk). To control the type of the exported property, use the type hint notation.

Note: Custom resources and nodes should be registered as global classes using class_name, since the Inspector currently only supports global classes. Otherwise, a less specific type will be exported instead.

Note: Node export is only supported in Node-derived classes and has a number of other limitations.

@export_category(name: String) 🔗

Define a new category for the following exported properties. This helps to organize properties in the Inspector dock.

See also @GlobalScope.PROPERTY_USAGE_CATEGORY.

Note: Categories in the Inspector dock's list usually divide properties coming from different classes (Node, Node2D, Sprite, etc.). For better clarity, it's recommended to use @export_group and @export_subgroup, instead.

@export_color_no_alpha() 🔗

Export a Color, Array[Color], or PackedColorArray property without allowing its transparency (Color.a) to be edited.

See also @GlobalScope.PROPERTY_HINT_COLOR_NO_ALPHA.

@export_custom(hint: PropertyHint, hint_string: String, usage: BitField[PropertyUsageFlags] = 6) 🔗

Allows you to set a custom hint, hint string, and usage flags for the exported property. Note that there's no validation done in GDScript, it will just pass the parameters to the editor.

Note: Regardless of the usage value, the @GlobalScope.PROPERTY_USAGE_SCRIPT_VARIABLE flag is always added, as with any explicitly declared script variable.

Export a String, Array[String], or PackedStringArray property as a path to a directory. The path will be limited to the project folder and its subfolders. See @export_global_dir to allow picking from the entire filesystem.

See also @GlobalScope.PROPERTY_HINT_DIR.

@export_enum(names: String, ...) vararg 🔗

Export an int, String, Array[int], Array[String], PackedByteArray, PackedInt32Array, PackedInt64Array, or PackedStringArray property as an enumerated list of options (or an array of options). If the property is an int, then the index of the value is stored, in the same order the values are provided. You can add explicit values using a colon. If the property is a String, then the value is stored.

See also @GlobalScope.PROPERTY_HINT_ENUM.

If you want to set an initial value, you must specify it explicitly:

If you want to use named GDScript enums, then use @export instead:

@export_exp_easing(hints: String = "", ...) vararg 🔗

Export a floating-point property with an easing editor widget. Additional hints can be provided to adjust the behavior of the widget. "attenuation" flips the curve, which makes it more intuitive for editing attenuation properties. "positive_only" limits values to only be greater than or equal to zero.

See also @GlobalScope.PROPERTY_HINT_EXP_EASING.

@export_file(filter: String = "", ...) vararg 🔗

Export a String, Array[String], or PackedStringArray property as a path to a file. The path will be limited to the project folder and its subfolders. See @export_global_file to allow picking from the entire filesystem.

If filter is provided, only matching files will be available for picking.

See also @GlobalScope.PROPERTY_HINT_FILE.

Note: The file will be stored and referenced as UID, if available. This ensures that the reference is valid even when the file is moved. You can use ResourceUID methods to convert it to path.

@export_file_path(filter: String = "", ...) vararg 🔗

Same as @export_file, except the file will be stored as a raw path. This means that it may become invalid when the file is moved. If you are exporting a Resource path, consider using @export_file instead.

@export_flags(names: String, ...) vararg 🔗

Export an integer property as a bit flag field. This allows to store several "checked" or true values with one property, and comfortably select them from the Inspector dock.

See also @GlobalScope.PROPERTY_HINT_FLAGS.

You can add explicit values using a colon:

You can also combine several flags:

Note: A flag value must be at least 1 and at most 2 ** 32 - 1.

Note: Unlike @export_enum, the previous explicit value is not taken into account. In the following example, A is 16, B is 2, C is 4.

You can also use the annotation on Array[int], PackedByteArray, PackedInt32Array, and PackedInt64Array

@export_flags_2d_navigation() 🔗

Export an integer property as a bit flag field for 2D navigation layers. The widget in the Inspector dock will use the layer names defined in ProjectSettings.layer_names/2d_navigation/layer_1.

See also @GlobalScope.PROPERTY_HINT_LAYERS_2D_NAVIGATION.

@export_flags_2d_physics() 🔗

Export an integer property as a bit flag field for 2D physics layers. The widget in the Inspector dock will use the layer names defined in ProjectSettings.layer_names/2d_physics/layer_1.

See also @GlobalScope.PROPERTY_HINT_LAYERS_2D_PHYSICS.

@export_flags_2d_render() 🔗

Export an integer property as a bit flag field for 2D render layers. The widget in the Inspector dock will use the layer names defined in ProjectSettings.layer_names/2d_render/layer_1.

See also @GlobalScope.PROPERTY_HINT_LAYERS_2D_RENDER.

@export_flags_3d_navigation() 🔗

Export an integer property as a bit flag field for 3D navigation layers. The widget in the Inspector dock will use the layer names defined in ProjectSettings.layer_names/3d_navigation/layer_1.

See also @GlobalScope.PROPERTY_HINT_LAYERS_3D_NAVIGATION.

@export_flags_3d_physics() 🔗

Export an integer property as a bit flag field for 3D physics layers. The widget in the Inspector dock will use the layer names defined in ProjectSettings.layer_names/3d_physics/layer_1.

See also @GlobalScope.PROPERTY_HINT_LAYERS_3D_PHYSICS.

@export_flags_3d_render() 🔗

Export an integer property as a bit flag field for 3D render layers. The widget in the Inspector dock will use the layer names defined in ProjectSettings.layer_names/3d_render/layer_1.

See also @GlobalScope.PROPERTY_HINT_LAYERS_3D_RENDER.

@export_flags_avoidance() 🔗

Export an integer property as a bit flag field for navigation avoidance layers. The widget in the Inspector dock will use the layer names defined in ProjectSettings.layer_names/avoidance/layer_1.

See also @GlobalScope.PROPERTY_HINT_LAYERS_AVOIDANCE.

@export_global_dir() 🔗

Export a String, Array[String], or PackedStringArray property as an absolute path to a directory. The path can be picked from the entire filesystem. See @export_dir to limit it to the project folder and its subfolders.

See also @GlobalScope.PROPERTY_HINT_GLOBAL_DIR.

@export_global_file(filter: String = "", ...) vararg 🔗

Export a String, Array[String], or PackedStringArray property as an absolute path to a file. The path can be picked from the entire filesystem. See @export_file to limit it to the project folder and its subfolders.

If filter is provided, only matching files will be available for picking.

See also @GlobalScope.PROPERTY_HINT_GLOBAL_FILE.

@export_group(name: String, prefix: String = "") 🔗

Define a new group for the following exported properties. This helps to organize properties in the Inspector dock. Groups can be added with an optional prefix, which would make group to only consider properties that have this prefix. The grouping will break on the first property that doesn't have a prefix. The prefix is also removed from the property's name in the Inspector dock.

If no prefix is provided, then every following property will be added to the group. The group ends when then next group or category is defined. You can also force end a group by using this annotation with empty strings for parameters, @export_group("", "").

Groups cannot be nested, use @export_subgroup to add subgroups within groups.

See also @GlobalScope.PROPERTY_USAGE_GROUP.

@export_multiline() 🔗

Export a String, Array[String], PackedStringArray, Dictionary or Array[Dictionary] property with a large TextEdit widget instead of a LineEdit. This adds support for multiline content and makes it easier to edit large amount of text stored in the property.

See also @GlobalScope.PROPERTY_HINT_MULTILINE_TEXT.

@export_node_path(type: String = "", ...) vararg 🔗

Export a NodePath or Array[NodePath] property with a filter for allowed node types.

See also @GlobalScope.PROPERTY_HINT_NODE_PATH_VALID_TYPES.

Note: The type must be a native class or a globally registered script (using the class_name keyword) that inherits Node.

@export_placeholder(placeholder: String) 🔗

Export a String, Array[String], or PackedStringArray property with a placeholder text displayed in the editor widget when no value is present.

See also @GlobalScope.PROPERTY_HINT_PLACEHOLDER_TEXT.

@export_range(min: float, max: float, step: float = 1.0, extra_hints: String = "", ...) vararg 🔗

Export an int, float, Array[int], Array[float], PackedByteArray, PackedInt32Array, PackedInt64Array, PackedFloat32Array, or PackedFloat64Array property as a range value. The range must be defined by min and max, as well as an optional step and a variety of extra hints. The step defaults to 1 for integer properties. For floating-point numbers this value depends on your EditorSettings.interface/inspector/default_float_step setting.

If hints "or_greater" and "or_less" are provided, the editor widget will not cap the value at range boundaries. The "exp" hint will make the edited values on range to change exponentially. The "hide_slider" hint will hide the slider element of the editor widget.

Hints also allow to indicate the units for the edited value. Using "radians_as_degrees" you can specify that the actual value is in radians, but should be displayed in degrees in the Inspector dock (the range values are also in degrees). "degrees" allows to add a degree sign as a unit suffix (the value is unchanged). Finally, a custom suffix can be provided using "suffix:unit", where "unit" can be any string.

See also @GlobalScope.PROPERTY_HINT_RANGE.

Export a property with @GlobalScope.PROPERTY_USAGE_STORAGE flag. The property is not displayed in the editor, but it is serialized and stored in the scene or resource file. This can be useful for @tool scripts. Also the property value is copied when Resource.duplicate() or Node.duplicate() is called, unlike non-exported variables.

@export_subgroup(name: String, prefix: String = "") 🔗

Define a new subgroup for the following exported properties. This helps to organize properties in the Inspector dock. Subgroups work exactly like groups, except they need a parent group to exist. See @export_group.

See also @GlobalScope.PROPERTY_USAGE_SUBGROUP.

Note: Subgroups cannot be nested, but you can use the slash separator (/) to achieve the desired effect:

@export_tool_button(text: String, icon: String = "") 🔗

Export a Callable property as a clickable button with the label text. When the button is pressed, the callable is called.

If icon is specified, it is used to fetch an icon for the button via Control.get_theme_icon(), from the "EditorIcons" theme type. If icon is omitted, the default "Callable" icon is used instead.

Consider using the EditorUndoRedoManager to allow the action to be reverted safely.

See also @GlobalScope.PROPERTY_HINT_TOOL_BUTTON.

Note: The property is exported without the @GlobalScope.PROPERTY_USAGE_STORAGE flag because a Callable cannot be properly serialized and stored in a file.

Note: In an exported project neither EditorInterface nor EditorUndoRedoManager exist, which may cause some scripts to break. To prevent this, you can use Engine.get_singleton() and omit the static type from the variable declaration:

Note: Avoid storing lambda callables in member variables of RefCounted-based classes (e.g. resources), as this can lead to memory leaks. Use only method callables and optionally Callable.bind() or Callable.unbind().

@icon(icon_path: String) 🔗

Add a custom icon to the current script. The icon specified at icon_path is displayed in the Scene dock for every node of that class, as well as in various editor dialogs.

Note: Only the script can have a custom icon. Inner classes are not supported.

Note: As annotations describe their subject, the @icon annotation must be placed before the class definition and inheritance.

Note: Unlike most other annotations, the argument of the @icon annotation must be a string literal (constant expressions are not supported).

Mark the following property as assigned when the Node is ready. Values for these properties are not assigned immediately when the node is initialized (Object._init()), and instead are computed and stored right before Node._ready().

@rpc(mode: String = "authority", sync: String = "call_remote", transfer_mode: String = "unreliable", transfer_channel: int = 0) 🔗

Mark the following method for remote procedure calls. See High-level multiplayer.

If mode is set as "any_peer", allows any peer to call this RPC function. Otherwise, only the authority peer is allowed to call it and mode should be kept as "authority". When configuring functions as RPCs with Node.rpc_config(), each of these modes respectively corresponds to the MultiplayerAPI.RPC_MODE_AUTHORITY and MultiplayerAPI.RPC_MODE_ANY_PEER RPC modes. See RPCMode. If a peer that is not the authority tries to call a function that is only allowed for the authority, the function will not be executed. If the error can be detected locally (when the RPC configuration is consistent between the local and the remote peer), an error message will be displayed on the sender peer. Otherwise, the remote peer will detect the error and print an error there.

If sync is set as "call_remote", the function will only be executed on the remote peer, but not locally. To run this function locally too, set sync to "call_local". When configuring functions as RPCs with Node.rpc_config(), this is equivalent to setting call_local to true.

The transfer_mode accepted values are "unreliable", "unreliable_ordered", or "reliable". It sets the transfer mode of the underlying MultiplayerPeer. See MultiplayerPeer.transfer_mode.

The transfer_channel defines the channel of the underlying MultiplayerPeer. See MultiplayerPeer.transfer_channel.

The order of mode, sync and transfer_mode does not matter, but values related to the same argument must not be used more than once. transfer_channel always has to be the 4th argument (you must specify 3 preceding arguments).

Note: Methods annotated with @rpc cannot receive objects which define required parameters in Object._init(). See Object._init() for more details.

Make a script with static variables to not persist after all references are lost. If the script is loaded again the static variables will revert to their default values.

Note: As annotations describe their subject, the @static_unload annotation must be placed before the class definition and inheritance.

Warning: Currently, due to a bug, scripts are never freed, even if @static_unload annotation is used.

Mark the current script as a tool script, allowing it to be loaded and executed by the editor. See Running code in the editor.

Note: As annotations describe their subject, the @tool annotation must be placed before the class definition and inheritance.

@warning_ignore(warning: String, ...) vararg 🔗

Mark the following statement to ignore the specified warning. See GDScript warning system.

See also @warning_ignore_start and @warning_ignore_restore.

@warning_ignore_restore(warning: String, ...) vararg 🔗

Stops ignoring the listed warning types after @warning_ignore_start. Ignoring the specified warning types will be reset to Project Settings. This annotation can be omitted to ignore the warning types until the end of the file.

Note: Unlike most other annotations, arguments of the @warning_ignore_restore annotation must be string literals (constant expressions are not supported).

@warning_ignore_start(warning: String, ...) vararg 🔗

Starts ignoring the listed warning types until the end of the file or the @warning_ignore_restore annotation with the given warning type.

Note: To suppress a single warning, use @warning_ignore instead.

Note: Unlike most other annotations, arguments of the @warning_ignore_start annotation must be string literals (constant expressions are not supported).

Color Color8(r8: int, g8: int, b8: int, a8: int = 255) 🔗

Deprecated: Use Color.from_rgba8() instead.

Returns a Color constructed from red (r8), green (g8), blue (b8), and optionally alpha (a8) integer channels, each divided by 255.0 for their final value. Using Color8() instead of the standard Color constructor is useful when you need to match exact color values in an Image.

Note: Due to the lower precision of Color8() compared to the standard Color constructor, a color created with Color8() will generally not be equal to the same color created with the standard Color constructor. Use Color.is_equal_approx() for comparisons to avoid issues with floating-point precision error.

void assert(condition: bool, message: String = "") 🔗

Asserts that the condition is true. If the condition is false, an error is generated. When running from the editor, the running project will also be paused until you resume it. This can be used as a stronger form of @GlobalScope.push_error() for reporting errors to project developers or add-on users.

An optional message can be shown in addition to the generic "Assertion failed" message. You can use this to provide additional details about why the assertion failed.

Warning: For performance reasons, the code inside assert() is only executed in debug builds or when running the project from the editor. Don't include code that has side effects in an assert() call. Otherwise, the project will behave differently when exported in release mode.

Note: assert() is a keyword, not a function. So you cannot access it as a Callable or use it inside expressions.

String char(code: int) 🔗

Returns a single character (as a String of length 1) of the given Unicode code point code.

This is the inverse of ord(). See also String.chr() and String.unicode_at().

Variant convert(what: Variant, type: Variant.Type) 🔗

Deprecated: Use @GlobalScope.type_convert() instead.

Converts what to type in the best way possible. The type uses the Variant.Type values.

Object dict_to_inst(dictionary: Dictionary) 🔗

Deprecated: Consider using JSON.to_native() or Object.get_property_list() instead.

Converts a dictionary (created with inst_to_dict()) back to an Object instance. Can be useful for deserializing.

Returns an array of dictionaries representing the current call stack.

Starting from _ready(), bar() would print:

See also print_debug(), print_stack(), and Engine.capture_script_backtraces().

Note: By default, backtraces are only available in editor builds and debug builds. To enable them for release builds as well, you need to enable ProjectSettings.debug/settings/gdscript/always_track_call_stacks.

Dictionary inst_to_dict(instance: Object) 🔗

Deprecated: Consider using JSON.from_native() or Object.get_property_list() instead.

Returns the passed instance converted to a Dictionary. Can be useful for serializing.

Note: This function can only be used to serialize objects with an attached GDScript stored in a separate file. Objects without an attached script, with a script written in another language, or with a built-in script are not supported.

Note: This function is not recursive, which means that nested objects will not be represented as dictionaries. Also, properties passed by reference (Object, Dictionary, Array, and packed arrays) are copied by reference, not duplicated.

bool is_instance_of(value: Variant, type: Variant) 🔗

Returns true if value is an instance of type. The type value must be one of the following:

A constant from the Variant.Type enumeration, for example @GlobalScope.TYPE_INT.

An Object-derived class which exists in ClassDB, for example Node.

A Script (you can use any class, including inner one).

Unlike the right operand of the is operator, type can be a non-constant value. The is operator supports more features (such as typed arrays). Use the operator instead of this method if you do not need to check the type dynamically.

Note: If value and/or type are freed objects (see @GlobalScope.is_instance_valid()), or type is not one of the above options, this method will raise a runtime error.

See also @GlobalScope.typeof(), type_exists(), Array.is_same_typed() (and other Array methods).

int len(var: Variant) 🔗

Returns the length of the given Variant var. The length can be the character count of a String or StringName, the element count of any array type, or the size of a Dictionary. For every other Variant type, a run-time error is generated and execution is stopped.

Resource load(path: String) 🔗

Returns a Resource from the filesystem located at the absolute path. Unless it's already referenced elsewhere (such as in another script or in the scene), the resource is loaded from disk on function call, which might cause a slight delay, especially when loading large scenes. To avoid unnecessary delays when loading something multiple times, either store the resource in a variable or use preload(). This method is equivalent of using ResourceLoader.load() with ResourceLoader.CACHE_MODE_REUSE.

Note: Resource paths can be obtained by right-clicking on a resource in the FileSystem dock and choosing "Copy Path", or by dragging the file from the FileSystem dock into the current script.

Important: Relative paths are not relative to the script calling this method, instead it is prefixed with "res://". Loading from relative paths might not work as expected.

This function is a simplified version of ResourceLoader.load(), which can be used for more advanced scenarios.

Note: Files have to be imported into the engine first to load them using this function. If you want to load Images at run-time, you may use Image.load(). If you want to import audio files, you can use the snippet described in AudioStreamMP3.data.

Note: If ProjectSettings.editor/export/convert_text_resources_to_binary is true, load() will not be able to read converted files in an exported project. If you rely on run-time loading of files present within the PCK, set ProjectSettings.editor/export/convert_text_resources_to_binary to false.

int ord(char: String) 🔗

Returns an integer representing the Unicode code point of the given character char, which should be a string of length 1.

This is the inverse of char(). See also String.chr() and String.unicode_at().

Resource preload(path: String) 🔗

Returns a Resource from the filesystem located at path. During run-time, the resource is loaded when the script is being parsed. This function effectively acts as a reference to that resource. Note that this function requires path to be a constant String. If you want to load a resource from a dynamic/variable path, use load().

Note: Resource paths can be obtained by right-clicking on a resource in the Assets Panel and choosing "Copy Path", or by dragging the file from the FileSystem dock into the current script.

Note: preload() is a keyword, not a function. So you cannot access it as a Callable.

void print_debug(...) vararg 🔗

Like @GlobalScope.print(), but includes the current stack frame when running with the debugger turned on.

The output in the console may look like the following:

See also print_stack(), get_stack(), and Engine.capture_script_backtraces().

Note: By default, backtraces are only available in editor builds and debug builds. To enable them for release builds as well, you need to enable ProjectSettings.debug/settings/gdscript/always_track_call_stacks.

Prints a stack trace at the current code location.

The output in the console may look like the following:

See also print_debug(), get_stack(), and Engine.capture_script_backtraces().

Note: By default, backtraces are only available in editor builds and debug builds. To enable them for release builds as well, you need to enable ProjectSettings.debug/settings/gdscript/always_track_call_stacks.

Array range(...) vararg 🔗

Returns an array with the given range. range() can be called in three ways:

range(n: int): Starts from 0, increases by steps of 1, and stops before n. The argument n is exclusive.

range(b: int, n: int): Starts from b, increases by steps of 1, and stops before n. The arguments b and n are inclusive and exclusive, respectively.

range(b: int, n: int, s: int): Starts from b, increases/decreases by steps of s, and stops before n. The arguments b and n are inclusive and exclusive, respectively. The argument s can be negative, but not 0. If s is 0, an error message is printed.

range() converts all arguments to int before processing.

Note: Returns an empty array if no value meets the value constraint (e.g. range(2, 5, -1) or range(5, 5, 1)).

To iterate over an Array backwards, use:

To iterate over float, convert them in the loop.

bool type_exists(type: StringName) 🔗

Returns true if the given Object-derived class exists in ClassDB. Note that Variant data types are not registered in ClassDB.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## @GlobalScope — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/classes/class_%40globalscope.html

**Contents:**
- @GlobalScope
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Global scope constants and functions.

A list of global scope enumerated constants and built-in functions. This is all that resides in the globals, constants regarding error codes, keycodes, property hints, etc.

Singletons are also documented here, since they can be accessed from anywhere.

For the entries that can only be accessed from scripts written in GDScript, see @GDScript.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

Random number generation

NavigationMeshGenerator

NavigationMeshGenerator

PhysicsServer2DManager

PhysicsServer2DManager

PhysicsServer3DManager

PhysicsServer3DManager

angle_difference(from: float, to: float)

atan2(y: float, x: float)

bezier_derivative(start: float, control_1: float, control_2: float, end: float, t: float)

bezier_interpolate(start: float, control_1: float, control_2: float, end: float, t: float)

bytes_to_var(bytes: PackedByteArray)

bytes_to_var_with_objects(bytes: PackedByteArray)

clamp(value: Variant, min: Variant, max: Variant)

clampf(value: float, min: float, max: float)

clampi(value: int, min: int, max: int)

cos(angle_rad: float)

cubic_interpolate(from: float, to: float, pre: float, post: float, weight: float)

cubic_interpolate_angle(from: float, to: float, pre: float, post: float, weight: float)

cubic_interpolate_angle_in_time(from: float, to: float, pre: float, post: float, weight: float, to_t: float, pre_t: float, post_t: float)

cubic_interpolate_in_time(from: float, to: float, pre: float, post: float, weight: float, to_t: float, pre_t: float, post_t: float)

db_to_linear(db: float)

deg_to_rad(deg: float)

ease(x: float, curve: float)

error_string(error: int)

fmod(x: float, y: float)

fposmod(x: float, y: float)

hash(variable: Variant)

instance_from_id(instance_id: int)

inverse_lerp(from: float, to: float, weight: float)

is_equal_approx(a: float, b: float)

is_instance_id_valid(id: int)

is_instance_valid(instance: Variant)

is_same(a: Variant, b: Variant)

is_zero_approx(x: float)

lerp(from: Variant, to: Variant, weight: Variant)

lerp_angle(from: float, to: float, weight: float)

lerpf(from: float, to: float, weight: float)

linear_to_db(lin: float)

maxf(a: float, b: float)

minf(a: float, b: float)

move_toward(from: float, to: float, delta: float)

nearest_po2(value: int)

pingpong(value: float, length: float)

posmod(x: int, y: int)

pow(base: float, exp: float)

print_rich(...) vararg

print_verbose(...) vararg

push_error(...) vararg

push_warning(...) vararg

rad_to_deg(rad: float)

rand_from_seed(seed: int)

randf_range(from: float, to: float)

randfn(mean: float, deviation: float)

randi_range(from: int, to: int)

remap(value: float, istart: float, istop: float, ostart: float, ostop: float)

rid_from_int64(base: int)

rotate_toward(from: float, to: float, delta: float)

sin(angle_rad: float)

smoothstep(from: float, to: float, x: float)

snapped(x: Variant, step: Variant)

snappedf(x: float, step: float)

snappedi(x: float, step: int)

step_decimals(x: float)

str_to_var(string: String)

tan(angle_rad: float)

type_convert(variant: Variant, type: int)

type_string(type: int)

typeof(variable: Variant)

var_to_bytes(variable: Variant)

var_to_bytes_with_objects(variable: Variant)

var_to_str(variable: Variant)

weakref(obj: Variant)

wrap(value: Variant, min: Variant, max: Variant)

wrapf(value: float, min: float, max: float)

wrapi(value: int, min: int, max: int)

Left side, usually used for Control or StyleBox-derived classes.

Top side, usually used for Control or StyleBox-derived classes.

Right side, usually used for Control or StyleBox-derived classes.

Bottom side, usually used for Control or StyleBox-derived classes.

Corner CORNER_TOP_LEFT = 0

Corner CORNER_TOP_RIGHT = 1

Corner CORNER_BOTTOM_RIGHT = 2

Corner CORNER_BOTTOM_LEFT = 3

Orientation VERTICAL = 1

General vertical alignment, usually used for Separator, ScrollBar, Slider, etc.

Orientation HORIZONTAL = 0

General horizontal alignment, usually used for Separator, ScrollBar, Slider, etc.

enum ClockDirection: 🔗

ClockDirection CLOCKWISE = 0

Clockwise rotation. Used by some methods (e.g. Image.rotate_90()).

ClockDirection COUNTERCLOCKWISE = 1

Counter-clockwise rotation. Used by some methods (e.g. Image.rotate_90()).

enum HorizontalAlignment: 🔗

HorizontalAlignment HORIZONTAL_ALIGNMENT_LEFT = 0

Horizontal left alignment, usually for text-derived classes.

HorizontalAlignment HORIZONTAL_ALIGNMENT_CENTER = 1

Horizontal center alignment, usually for text-derived classes.

HorizontalAlignment HORIZONTAL_ALIGNMENT_RIGHT = 2

Horizontal right alignment, usually for text-derived classes.

HorizontalAlignment HORIZONTAL_ALIGNMENT_FILL = 3

Expand row to fit width, usually for text-derived classes.

enum VerticalAlignment: 🔗

VerticalAlignment VERTICAL_ALIGNMENT_TOP = 0

Vertical top alignment, usually for text-derived classes.

VerticalAlignment VERTICAL_ALIGNMENT_CENTER = 1

Vertical center alignment, usually for text-derived classes.

VerticalAlignment VERTICAL_ALIGNMENT_BOTTOM = 2

Vertical bottom alignment, usually for text-derived classes.

VerticalAlignment VERTICAL_ALIGNMENT_FILL = 3

Expand rows to fit height, usually for text-derived classes.

enum InlineAlignment: 🔗

InlineAlignment INLINE_ALIGNMENT_TOP_TO = 0

Aligns the top of the inline object (e.g. image, table) to the position of the text specified by INLINE_ALIGNMENT_TO_* constant.

InlineAlignment INLINE_ALIGNMENT_CENTER_TO = 1

Aligns the center of the inline object (e.g. image, table) to the position of the text specified by INLINE_ALIGNMENT_TO_* constant.

InlineAlignment INLINE_ALIGNMENT_BASELINE_TO = 3

Aligns the baseline (user defined) of the inline object (e.g. image, table) to the position of the text specified by INLINE_ALIGNMENT_TO_* constant.

InlineAlignment INLINE_ALIGNMENT_BOTTOM_TO = 2

Aligns the bottom of the inline object (e.g. image, table) to the position of the text specified by INLINE_ALIGNMENT_TO_* constant.

InlineAlignment INLINE_ALIGNMENT_TO_TOP = 0

Aligns the position of the inline object (e.g. image, table) specified by INLINE_ALIGNMENT_*_TO constant to the top of the text.

InlineAlignment INLINE_ALIGNMENT_TO_CENTER = 4

Aligns the position of the inline object (e.g. image, table) specified by INLINE_ALIGNMENT_*_TO constant to the center of the text.

InlineAlignment INLINE_ALIGNMENT_TO_BASELINE = 8

Aligns the position of the inline object (e.g. image, table) specified by INLINE_ALIGNMENT_*_TO constant to the baseline of the text.

InlineAlignment INLINE_ALIGNMENT_TO_BOTTOM = 12

Aligns inline object (e.g. image, table) to the bottom of the text.

InlineAlignment INLINE_ALIGNMENT_TOP = 0

Aligns top of the inline object (e.g. image, table) to the top of the text. Equivalent to INLINE_ALIGNMENT_TOP_TO | INLINE_ALIGNMENT_TO_TOP.

InlineAlignment INLINE_ALIGNMENT_CENTER = 5

Aligns center of the inline object (e.g. image, table) to the center of the text. Equivalent to INLINE_ALIGNMENT_CENTER_TO | INLINE_ALIGNMENT_TO_CENTER.

InlineAlignment INLINE_ALIGNMENT_BOTTOM = 14

Aligns bottom of the inline object (e.g. image, table) to the bottom of the text. Equivalent to INLINE_ALIGNMENT_BOTTOM_TO | INLINE_ALIGNMENT_TO_BOTTOM.

InlineAlignment INLINE_ALIGNMENT_IMAGE_MASK = 3

A bit mask for INLINE_ALIGNMENT_*_TO alignment constants.

InlineAlignment INLINE_ALIGNMENT_TEXT_MASK = 12

A bit mask for INLINE_ALIGNMENT_TO_* alignment constants.

EulerOrder EULER_ORDER_XYZ = 0

Specifies that Euler angles should be in XYZ order. When composing, the order is X, Y, Z. When decomposing, the order is reversed, first Z, then Y, and X last.

EulerOrder EULER_ORDER_XZY = 1

Specifies that Euler angles should be in XZY order. When composing, the order is X, Z, Y. When decomposing, the order is reversed, first Y, then Z, and X last.

EulerOrder EULER_ORDER_YXZ = 2

Specifies that Euler angles should be in YXZ order. When composing, the order is Y, X, Z. When decomposing, the order is reversed, first Z, then X, and Y last.

EulerOrder EULER_ORDER_YZX = 3

Specifies that Euler angles should be in YZX order. When composing, the order is Y, Z, X. When decomposing, the order is reversed, first X, then Z, and Y last.

EulerOrder EULER_ORDER_ZXY = 4

Specifies that Euler angles should be in ZXY order. When composing, the order is Z, X, Y. When decomposing, the order is reversed, first Y, then X, and Z last.

EulerOrder EULER_ORDER_ZYX = 5

Specifies that Euler angles should be in ZYX order. When composing, the order is Z, Y, X. When decomposing, the order is reversed, first X, then Y, and Z last.

Enum value which doesn't correspond to any key. This is used to initialize Key properties with a generic state.

Key KEY_SPECIAL = 4194304

Keycodes with this bit applied are non-printable.

Key KEY_ESCAPE = 4194305

Key KEY_TAB = 4194306

Key KEY_BACKTAB = 4194307

Key KEY_BACKSPACE = 4194308

Key KEY_ENTER = 4194309

Return key (on the main keyboard).

Key KEY_KP_ENTER = 4194310

Enter key on the numeric keypad.

Key KEY_INSERT = 4194311

Key KEY_DELETE = 4194312

Key KEY_PAUSE = 4194313

Key KEY_PRINT = 4194314

Key KEY_SYSREQ = 4194315

Key KEY_CLEAR = 4194316

Key KEY_HOME = 4194317

Key KEY_END = 4194318

Key KEY_LEFT = 4194319

Key KEY_RIGHT = 4194321

Key KEY_DOWN = 4194322

Key KEY_PAGEUP = 4194323

Key KEY_PAGEDOWN = 4194324

Key KEY_SHIFT = 4194325

Key KEY_CTRL = 4194326

Key KEY_META = 4194327

Key KEY_ALT = 4194328

Key KEY_CAPSLOCK = 4194329

Key KEY_NUMLOCK = 4194330

Key KEY_SCROLLLOCK = 4194331

Key KEY_F10 = 4194341

Key KEY_F11 = 4194342

Key KEY_F12 = 4194343

Key KEY_F13 = 4194344

Key KEY_F14 = 4194345

Key KEY_F15 = 4194346

Key KEY_F16 = 4194347

Key KEY_F17 = 4194348

Key KEY_F18 = 4194349

Key KEY_F19 = 4194350

Key KEY_F20 = 4194351

Key KEY_F21 = 4194352

Key KEY_F22 = 4194353

Key KEY_F23 = 4194354

Key KEY_F24 = 4194355

Key KEY_F25 = 4194356

F25 key. Only supported on macOS and Linux due to a Windows limitation.

Key KEY_F26 = 4194357

F26 key. Only supported on macOS and Linux due to a Windows limitation.

Key KEY_F27 = 4194358

F27 key. Only supported on macOS and Linux due to a Windows limitation.

Key KEY_F28 = 4194359

F28 key. Only supported on macOS and Linux due to a Windows limitation.

Key KEY_F29 = 4194360

F29 key. Only supported on macOS and Linux due to a Windows limitation.

Key KEY_F30 = 4194361

F30 key. Only supported on macOS and Linux due to a Windows limitation.

Key KEY_F31 = 4194362

F31 key. Only supported on macOS and Linux due to a Windows limitation.

Key KEY_F32 = 4194363

F32 key. Only supported on macOS and Linux due to a Windows limitation.

Key KEY_F33 = 4194364

F33 key. Only supported on macOS and Linux due to a Windows limitation.

Key KEY_F34 = 4194365

F34 key. Only supported on macOS and Linux due to a Windows limitation.

Key KEY_F35 = 4194366

F35 key. Only supported on macOS and Linux due to a Windows limitation.

Key KEY_KP_MULTIPLY = 4194433

Multiply (*) key on the numeric keypad.

Key KEY_KP_DIVIDE = 4194434

Divide (/) key on the numeric keypad.

Key KEY_KP_SUBTRACT = 4194435

Subtract (-) key on the numeric keypad.

Key KEY_KP_PERIOD = 4194436

Period (.) key on the numeric keypad.

Key KEY_KP_ADD = 4194437

Add (+) key on the numeric keypad.

Key KEY_KP_0 = 4194438

Number 0 on the numeric keypad.

Key KEY_KP_1 = 4194439

Number 1 on the numeric keypad.

Key KEY_KP_2 = 4194440

Number 2 on the numeric keypad.

Key KEY_KP_3 = 4194441

Number 3 on the numeric keypad.

Key KEY_KP_4 = 4194442

Number 4 on the numeric keypad.

Key KEY_KP_5 = 4194443

Number 5 on the numeric keypad.

Key KEY_KP_6 = 4194444

Number 6 on the numeric keypad.

Key KEY_KP_7 = 4194445

Number 7 on the numeric keypad.

Key KEY_KP_8 = 4194446

Number 8 on the numeric keypad.

Key KEY_KP_9 = 4194447

Number 9 on the numeric keypad.

Key KEY_MENU = 4194370

Key KEY_HYPER = 4194371

Hyper key. (On Linux/X11 only).

Key KEY_HELP = 4194373

Key KEY_BACK = 4194376

Key KEY_FORWARD = 4194377

Key KEY_STOP = 4194378

Key KEY_REFRESH = 4194379

Key KEY_VOLUMEDOWN = 4194380

Key KEY_VOLUMEMUTE = 4194381

Key KEY_VOLUMEUP = 4194382

Key KEY_MEDIAPLAY = 4194388

Key KEY_MEDIASTOP = 4194389

Key KEY_MEDIAPREVIOUS = 4194390

Key KEY_MEDIANEXT = 4194391

Key KEY_MEDIARECORD = 4194392

Key KEY_HOMEPAGE = 4194393

Key KEY_FAVORITES = 4194394

Key KEY_SEARCH = 4194395

Key KEY_STANDBY = 4194396

Key KEY_OPENURL = 4194397

Open URL / Launch Browser key.

Key KEY_LAUNCHMAIL = 4194398

Key KEY_LAUNCHMEDIA = 4194399

Key KEY_LAUNCH0 = 4194400

Launch Shortcut 0 key.

Key KEY_LAUNCH1 = 4194401

Launch Shortcut 1 key.

Key KEY_LAUNCH2 = 4194402

Launch Shortcut 2 key.

Key KEY_LAUNCH3 = 4194403

Launch Shortcut 3 key.

Key KEY_LAUNCH4 = 4194404

Launch Shortcut 4 key.

Key KEY_LAUNCH5 = 4194405

Launch Shortcut 5 key.

Key KEY_LAUNCH6 = 4194406

Launch Shortcut 6 key.

Key KEY_LAUNCH7 = 4194407

Launch Shortcut 7 key.

Key KEY_LAUNCH8 = 4194408

Launch Shortcut 8 key.

Key KEY_LAUNCH9 = 4194409

Launch Shortcut 9 key.

Key KEY_LAUNCHA = 4194410

Launch Shortcut A key.

Key KEY_LAUNCHB = 4194411

Launch Shortcut B key.

Key KEY_LAUNCHC = 4194412

Launch Shortcut C key.

Key KEY_LAUNCHD = 4194413

Launch Shortcut D key.

Key KEY_LAUNCHE = 4194414

Launch Shortcut E key.

Key KEY_LAUNCHF = 4194415

Launch Shortcut F key.

Key KEY_GLOBE = 4194416

"Globe" key on Mac / iPad keyboard.

Key KEY_KEYBOARD = 4194417

"On-screen keyboard" key on iPad keyboard.

Key KEY_JIS_EISU = 4194418

英数 key on Mac keyboard.

Key KEY_JIS_KANA = 4194419

かな key on Mac keyboard.

Key KEY_UNKNOWN = 8388607

Exclamation mark (!) key.

Key KEY_QUOTEDBL = 34

Double quotation mark (") key.

Key KEY_NUMBERSIGN = 35

Number sign or hash (#) key.

Percent sign (%) key.

Key KEY_AMPERSAND = 38

Key KEY_APOSTROPHE = 39

Key KEY_PARENLEFT = 40

Left parenthesis (() key.

Key KEY_PARENRIGHT = 41

Right parenthesis (``)``) key.

Key KEY_ASTERISK = 42

Key KEY_SEMICOLON = 59

Less-than sign (<) key.

Greater-than sign (>) key.

Key KEY_QUESTION = 63

Question mark (?) key.

Key KEY_BRACKETLEFT = 91

Left bracket ([lb]) key.

Key KEY_BACKSLASH = 92

Key KEY_BRACKETRIGHT = 93

Right bracket ([rb]) key.

Key KEY_ASCIICIRCUM = 94

Key KEY_UNDERSCORE = 95

Key KEY_QUOTELEFT = 96

Key KEY_BRACELEFT = 123

Vertical bar or pipe (|) key.

Key KEY_BRACERIGHT = 125

Key KEY_ASCIITILDE = 126

Key KEY_SECTION = 167

Section sign (§) key.

flags KeyModifierMask: 🔗

KeyModifierMask KEY_CODE_MASK = 8388607

KeyModifierMask KEY_MODIFIER_MASK = 2130706432

KeyModifierMask KEY_MASK_CMD_OR_CTRL = 16777216

Automatically remapped to KEY_META on macOS and KEY_CTRL on other platforms, this mask is never set in the actual events, and should be used for key mapping only.

KeyModifierMask KEY_MASK_SHIFT = 33554432

KeyModifierMask KEY_MASK_ALT = 67108864

Alt or Option (on macOS) key mask.

KeyModifierMask KEY_MASK_META = 134217728

Command (on macOS) or Meta/Windows key mask.

KeyModifierMask KEY_MASK_CTRL = 268435456

KeyModifierMask KEY_MASK_KPAD = 536870912

KeyModifierMask KEY_MASK_GROUP_SWITCH = 1073741824

Group Switch key mask.

KeyLocation KEY_LOCATION_UNSPECIFIED = 0

Used for keys which only appear once, or when a comparison doesn't need to differentiate the LEFT and RIGHT versions.

For example, when using InputEvent.is_match(), an event which has KEY_LOCATION_UNSPECIFIED will match any KeyLocation on the passed event.

KeyLocation KEY_LOCATION_LEFT = 1

A key which is to the left of its twin.

KeyLocation KEY_LOCATION_RIGHT = 2

A key which is to the right of its twin.

MouseButton MOUSE_BUTTON_NONE = 0

Enum value which doesn't correspond to any mouse button. This is used to initialize MouseButton properties with a generic state.

MouseButton MOUSE_BUTTON_LEFT = 1

Primary mouse button, usually assigned to the left button.

MouseButton MOUSE_BUTTON_RIGHT = 2

Secondary mouse button, usually assigned to the right button.

MouseButton MOUSE_BUTTON_MIDDLE = 3

MouseButton MOUSE_BUTTON_WHEEL_UP = 4

Mouse wheel scrolling up.

MouseButton MOUSE_BUTTON_WHEEL_DOWN = 5

Mouse wheel scrolling down.

MouseButton MOUSE_BUTTON_WHEEL_LEFT = 6

Mouse wheel left button (only present on some mice).

MouseButton MOUSE_BUTTON_WHEEL_RIGHT = 7

Mouse wheel right button (only present on some mice).

MouseButton MOUSE_BUTTON_XBUTTON1 = 8

Extra mouse button 1. This is sometimes present, usually to the sides of the mouse.

MouseButton MOUSE_BUTTON_XBUTTON2 = 9

Extra mouse button 2. This is sometimes present, usually to the sides of the mouse.

flags MouseButtonMask: 🔗

MouseButtonMask MOUSE_BUTTON_MASK_LEFT = 1

Primary mouse button mask, usually for the left button.

MouseButtonMask MOUSE_BUTTON_MASK_RIGHT = 2

Secondary mouse button mask, usually for the right button.

MouseButtonMask MOUSE_BUTTON_MASK_MIDDLE = 4

Middle mouse button mask.

MouseButtonMask MOUSE_BUTTON_MASK_MB_XBUTTON1 = 128

Extra mouse button 1 mask.

MouseButtonMask MOUSE_BUTTON_MASK_MB_XBUTTON2 = 256

Extra mouse button 2 mask.

JoyButton JOY_BUTTON_INVALID = -1

An invalid game controller button.

JoyButton JOY_BUTTON_A = 0

Game controller SDL button A. Corresponds to the bottom action button: Sony Cross, Xbox A, Nintendo B.

JoyButton JOY_BUTTON_B = 1

Game controller SDL button B. Corresponds to the right action button: Sony Circle, Xbox B, Nintendo A.

JoyButton JOY_BUTTON_X = 2

Game controller SDL button X. Corresponds to the left action button: Sony Square, Xbox X, Nintendo Y.

JoyButton JOY_BUTTON_Y = 3

Game controller SDL button Y. Corresponds to the top action button: Sony Triangle, Xbox Y, Nintendo X.

JoyButton JOY_BUTTON_BACK = 4

Game controller SDL back button. Corresponds to the Sony Select, Xbox Back, Nintendo - button.

JoyButton JOY_BUTTON_GUIDE = 5

Game controller SDL guide button. Corresponds to the Sony PS, Xbox Home button.

JoyButton JOY_BUTTON_START = 6

Game controller SDL start button. Corresponds to the Sony Options, Xbox Menu, Nintendo + button.

JoyButton JOY_BUTTON_LEFT_STICK = 7

Game controller SDL left stick button. Corresponds to the Sony L3, Xbox L/LS button.

JoyButton JOY_BUTTON_RIGHT_STICK = 8

Game controller SDL right stick button. Corresponds to the Sony R3, Xbox R/RS button.

JoyButton JOY_BUTTON_LEFT_SHOULDER = 9

Game controller SDL left shoulder button. Corresponds to the Sony L1, Xbox LB button.

JoyButton JOY_BUTTON_RIGHT_SHOULDER = 10

Game controller SDL right shoulder button. Corresponds to the Sony R1, Xbox RB button.

JoyButton JOY_BUTTON_DPAD_UP = 11

Game controller D-pad up button.

JoyButton JOY_BUTTON_DPAD_DOWN = 12

Game controller D-pad down button.

JoyButton JOY_BUTTON_DPAD_LEFT = 13

Game controller D-pad left button.

JoyButton JOY_BUTTON_DPAD_RIGHT = 14

Game controller D-pad right button.

JoyButton JOY_BUTTON_MISC1 = 15

Game controller SDL miscellaneous button. Corresponds to Xbox share button, PS5 microphone button, Nintendo Switch capture button.

JoyButton JOY_BUTTON_PADDLE1 = 16

Game controller SDL paddle 1 button.

JoyButton JOY_BUTTON_PADDLE2 = 17

Game controller SDL paddle 2 button.

JoyButton JOY_BUTTON_PADDLE3 = 18

Game controller SDL paddle 3 button.

JoyButton JOY_BUTTON_PADDLE4 = 19

Game controller SDL paddle 4 button.

JoyButton JOY_BUTTON_TOUCHPAD = 20

Game controller SDL touchpad button.

JoyButton JOY_BUTTON_SDL_MAX = 21

The number of SDL game controller buttons.

JoyButton JOY_BUTTON_MAX = 128

The maximum number of game controller buttons supported by the engine. The actual limit may be lower on specific platforms:

Android: Up to 36 buttons.

Linux: Up to 80 buttons.

Windows and macOS: Up to 128 buttons.

JoyAxis JOY_AXIS_INVALID = -1

An invalid game controller axis.

JoyAxis JOY_AXIS_LEFT_X = 0

Game controller left joystick x-axis.

JoyAxis JOY_AXIS_LEFT_Y = 1

Game controller left joystick y-axis.

JoyAxis JOY_AXIS_RIGHT_X = 2

Game controller right joystick x-axis.

JoyAxis JOY_AXIS_RIGHT_Y = 3

Game controller right joystick y-axis.

JoyAxis JOY_AXIS_TRIGGER_LEFT = 4

Game controller left trigger axis.

JoyAxis JOY_AXIS_TRIGGER_RIGHT = 5

Game controller right trigger axis.

JoyAxis JOY_AXIS_SDL_MAX = 6

The number of SDL game controller axes.

JoyAxis JOY_AXIS_MAX = 10

The maximum number of game controller axes: OpenVR supports up to 5 Joysticks making a total of 10 axes.

MIDIMessage MIDI_MESSAGE_NONE = 0

Does not correspond to any MIDI message. This is the default value of InputEventMIDI.message.

MIDIMessage MIDI_MESSAGE_NOTE_OFF = 8

MIDI message sent when a note is released.

Note: Not all MIDI devices send this message; some may send MIDI_MESSAGE_NOTE_ON with InputEventMIDI.velocity set to 0.

MIDIMessage MIDI_MESSAGE_NOTE_ON = 9

MIDI message sent when a note is pressed.

MIDIMessage MIDI_MESSAGE_AFTERTOUCH = 10

MIDI message sent to indicate a change in pressure while a note is being pressed down, also called aftertouch.

MIDIMessage MIDI_MESSAGE_CONTROL_CHANGE = 11

MIDI message sent when a controller value changes. In a MIDI device, a controller is any input that doesn't play notes. These may include sliders for volume, balance, and panning, as well as switches and pedals. See the General MIDI specification for a small list.

MIDIMessage MIDI_MESSAGE_PROGRAM_CHANGE = 12

MIDI message sent when the MIDI device changes its current instrument (also called program or preset).

MIDIMessage MIDI_MESSAGE_CHANNEL_PRESSURE = 13

MIDI message sent to indicate a change in pressure for the whole channel. Some MIDI devices may send this instead of MIDI_MESSAGE_AFTERTOUCH.

MIDIMessage MIDI_MESSAGE_PITCH_BEND = 14

MIDI message sent when the value of the pitch bender changes, usually a wheel on the MIDI device.

MIDIMessage MIDI_MESSAGE_SYSTEM_EXCLUSIVE = 240

MIDI system exclusive (SysEx) message. This type of message is not standardized and it's highly dependent on the MIDI device sending it.

Note: Getting this message's data from InputEventMIDI is not implemented.

MIDIMessage MIDI_MESSAGE_QUARTER_FRAME = 241

MIDI message sent every quarter frame to keep connected MIDI devices synchronized. Related to MIDI_MESSAGE_TIMING_CLOCK.

Note: Getting this message's data from InputEventMIDI is not implemented.

MIDIMessage MIDI_MESSAGE_SONG_POSITION_POINTER = 242

MIDI message sent to jump onto a new position in the current sequence or song.

Note: Getting this message's data from InputEventMIDI is not implemented.

MIDIMessage MIDI_MESSAGE_SONG_SELECT = 243

MIDI message sent to select a sequence or song to play.

Note: Getting this message's data from InputEventMIDI is not implemented.

MIDIMessage MIDI_MESSAGE_TUNE_REQUEST = 246

MIDI message sent to request a tuning calibration. Used on analog synthesizers. Most modern MIDI devices do not need this message.

MIDIMessage MIDI_MESSAGE_TIMING_CLOCK = 248

MIDI message sent 24 times after MIDI_MESSAGE_QUARTER_FRAME, to keep connected MIDI devices synchronized.

MIDIMessage MIDI_MESSAGE_START = 250

MIDI message sent to start the current sequence or song from the beginning.

MIDIMessage MIDI_MESSAGE_CONTINUE = 251

MIDI message sent to resume from the point the current sequence or song was paused.

MIDIMessage MIDI_MESSAGE_STOP = 252

MIDI message sent to pause the current sequence or song.

MIDIMessage MIDI_MESSAGE_ACTIVE_SENSING = 254

MIDI message sent repeatedly while the MIDI device is idle, to tell the receiver that the connection is alive. Most MIDI devices do not send this message.

MIDIMessage MIDI_MESSAGE_SYSTEM_RESET = 255

MIDI message sent to reset a MIDI device to its default state, as if it was just turned on. It should not be sent when the MIDI device is being turned on.

Methods that return Error return OK when no error occurred.

Since OK has value 0, and all other error constants are positive integers, it can also be used in boolean checks.

Note: Many functions do not return an error code, but will print error messages to standard output.

Error ERR_UNAVAILABLE = 2

Error ERR_UNCONFIGURED = 3

Error ERR_UNAUTHORIZED = 4

Error ERR_PARAMETER_RANGE_ERROR = 5

Parameter range error.

Error ERR_OUT_OF_MEMORY = 6

Out of memory (OOM) error.

Error ERR_FILE_NOT_FOUND = 7

File: Not found error.

Error ERR_FILE_BAD_DRIVE = 8

File: Bad drive error.

Error ERR_FILE_BAD_PATH = 9

File: Bad path error.

Error ERR_FILE_NO_PERMISSION = 10

File: No permission error.

Error ERR_FILE_ALREADY_IN_USE = 11

File: Already in use error.

Error ERR_FILE_CANT_OPEN = 12

File: Can't open error.

Error ERR_FILE_CANT_WRITE = 13

File: Can't write error.

Error ERR_FILE_CANT_READ = 14

File: Can't read error.

Error ERR_FILE_UNRECOGNIZED = 15

File: Unrecognized error.

Error ERR_FILE_CORRUPT = 16

Error ERR_FILE_MISSING_DEPENDENCIES = 17

File: Missing dependencies error.

Error ERR_FILE_EOF = 18

File: End of file (EOF) error.

Error ERR_CANT_OPEN = 19

Error ERR_CANT_CREATE = 20

Error ERR_QUERY_FAILED = 21

Error ERR_ALREADY_IN_USE = 22

Already in use error.

Error ERR_LOCKED = 23

Error ERR_TIMEOUT = 24

Error ERR_CANT_CONNECT = 25

Error ERR_CANT_RESOLVE = 26

Error ERR_CONNECTION_ERROR = 27

Error ERR_CANT_ACQUIRE_RESOURCE = 28

Can't acquire resource error.

Error ERR_CANT_FORK = 29

Can't fork process error.

Error ERR_INVALID_DATA = 30

Error ERR_INVALID_PARAMETER = 31

Invalid parameter error.

Error ERR_ALREADY_EXISTS = 32

Already exists error.

Error ERR_DOES_NOT_EXIST = 33

Does not exist error.

Error ERR_DATABASE_CANT_READ = 34

Database: Read error.

Error ERR_DATABASE_CANT_WRITE = 35

Database: Write error.

Error ERR_COMPILATION_FAILED = 36

Compilation failed error.

Error ERR_METHOD_NOT_FOUND = 37

Method not found error.

Error ERR_LINK_FAILED = 38

Linking failed error.

Error ERR_SCRIPT_FAILED = 39

Error ERR_CYCLIC_LINK = 40

Cycling link (import cycle) error.

Error ERR_INVALID_DECLARATION = 41

Invalid declaration error.

Error ERR_DUPLICATE_SYMBOL = 42

Duplicate symbol error.

Error ERR_PARSE_ERROR = 43

Help error. Used internally when passing --version or --help as executable options.

Bug error, caused by an implementation issue in the method.

Note: If a built-in method returns this code, please open an issue on the GitHub Issue Tracker.

Error ERR_PRINTER_ON_FIRE = 48

Printer on fire error (This is an easter egg, no built-in methods return this error code).

PropertyHint PROPERTY_HINT_NONE = 0

The property has no hint for the editor.

PropertyHint PROPERTY_HINT_RANGE = 1

Hints that an int or float property should be within a range specified via the hint string "min,max" or "min,max,step". The hint string can optionally include "or_greater" and/or "or_less" to allow manual input going respectively above the max or below the min values.

Example: "-360,360,1,or_greater,or_less".

Additionally, other keywords can be included: "exp" for exponential range editing, "radians_as_degrees" for editing radian angles in degrees (the range values are also in degrees), "degrees" to hint at an angle and "hide_slider" to hide the slider.

PropertyHint PROPERTY_HINT_ENUM = 2

Hints that an int or String property is an enumerated value to pick in a list specified via a hint string.

The hint string is a comma separated list of names such as "Hello,Something,Else". Whitespaces are not removed from either end of a name. For integer properties, the first name in the list has value 0, the next 1, and so on. Explicit values can also be specified by appending :integer to the name, e.g. "Zero,One,Three:3,Four,Six:6".

PropertyHint PROPERTY_HINT_ENUM_SUGGESTION = 3

Hints that a String property can be an enumerated value to pick in a list specified via a hint string such as "Hello,Something,Else".

Unlike PROPERTY_HINT_ENUM, a property with this hint still accepts arbitrary values and can be empty. The list of values serves to suggest possible values.

PropertyHint PROPERTY_HINT_EXP_EASING = 4

Hints that a float property should be edited via an exponential easing function. The hint string can include "attenuation" to flip the curve horizontally and/or "positive_only" to exclude in/out easing and limit values to be greater than or equal to zero.

PropertyHint PROPERTY_HINT_LINK = 5

Hints that a vector property should allow its components to be linked. For example, this allows Vector2.x and Vector2.y to be edited together.

PropertyHint PROPERTY_HINT_FLAGS = 6

Hints that an int property is a bitmask with named bit flags.

The hint string is a comma separated list of names such as "Bit0,Bit1,Bit2,Bit3". Whitespaces are not removed from either end of a name. The first name in the list has value 1, the next 2, then 4, 8, 16 and so on. Explicit values can also be specified by appending :integer to the name, e.g. "A:4,B:8,C:16". You can also combine several flags ("A:4,B:8,AB:12,C:16").

Note: A flag value must be at least 1 and at most 2 ** 32 - 1.

Note: Unlike PROPERTY_HINT_ENUM, the previous explicit value is not taken into account. For the hint "A:16,B,C", A is 16, B is 2, C is 4.

PropertyHint PROPERTY_HINT_LAYERS_2D_RENDER = 7

Hints that an int property is a bitmask using the optionally named 2D render layers.

PropertyHint PROPERTY_HINT_LAYERS_2D_PHYSICS = 8

Hints that an int property is a bitmask using the optionally named 2D physics layers.

PropertyHint PROPERTY_HINT_LAYERS_2D_NAVIGATION = 9

Hints that an int property is a bitmask using the optionally named 2D navigation layers.

PropertyHint PROPERTY_HINT_LAYERS_3D_RENDER = 10

Hints that an int property is a bitmask using the optionally named 3D render layers.

PropertyHint PROPERTY_HINT_LAYERS_3D_PHYSICS = 11

Hints that an int property is a bitmask using the optionally named 3D physics layers.

PropertyHint PROPERTY_HINT_LAYERS_3D_NAVIGATION = 12

Hints that an int property is a bitmask using the optionally named 3D navigation layers.

PropertyHint PROPERTY_HINT_LAYERS_AVOIDANCE = 37

Hints that an integer property is a bitmask using the optionally named avoidance layers.

PropertyHint PROPERTY_HINT_FILE = 13

Hints that a String property is a path to a file. Editing it will show a file dialog for picking the path. The hint string can be a set of filters with wildcards like "*.png,*.jpg". By default the file will be stored as UID whenever available. You can use ResourceUID methods to convert it back to path. For storing a raw path, use PROPERTY_HINT_FILE_PATH.

PropertyHint PROPERTY_HINT_DIR = 14

Hints that a String property is a path to a directory. Editing it will show a file dialog for picking the path.

PropertyHint PROPERTY_HINT_GLOBAL_FILE = 15

Hints that a String property is an absolute path to a file outside the project folder. Editing it will show a file dialog for picking the path. The hint string can be a set of filters with wildcards, like "*.png,*.jpg".

PropertyHint PROPERTY_HINT_GLOBAL_DIR = 16

Hints that a String property is an absolute path to a directory outside the project folder. Editing it will show a file dialog for picking the path.

PropertyHint PROPERTY_HINT_RESOURCE_TYPE = 17

Hints that a property is an instance of a Resource-derived type, optionally specified via the hint string (e.g. "Texture2D"). Editing it will show a popup menu of valid resource types to instantiate.

PropertyHint PROPERTY_HINT_MULTILINE_TEXT = 18

Hints that a String property is text with line breaks. Editing it will show a text input field where line breaks can be typed.

PropertyHint PROPERTY_HINT_EXPRESSION = 19

Hints that a String property is an Expression.

PropertyHint PROPERTY_HINT_PLACEHOLDER_TEXT = 20

Hints that a String property should show a placeholder text on its input field, if empty. The hint string is the placeholder text to use.

PropertyHint PROPERTY_HINT_COLOR_NO_ALPHA = 21

Hints that a Color property should be edited without affecting its transparency (Color.a is not editable).

PropertyHint PROPERTY_HINT_OBJECT_ID = 22

Hints that the property's value is an object encoded as object ID, with its type specified in the hint string. Used by the debugger.

PropertyHint PROPERTY_HINT_TYPE_STRING = 23

If a property is String, hints that the property represents a particular type (class). This allows to select a type from the create dialog. The property will store the selected type as a string.

If a property is Array, hints the editor how to show elements. The hint_string must encode nested types using ":" and "/".

If a property is Dictionary, hints the editor how to show elements. The hint_string is the same as Array, with a ";" separating the key and value.

Note: The trailing colon is required for properly detecting built-in types.

PropertyHint PROPERTY_HINT_NODE_PATH_TO_EDITED_NODE = 24

Deprecated: This hint is not used by the engine.

PropertyHint PROPERTY_HINT_OBJECT_TOO_BIG = 25

Hints that an object is too big to be sent via the debugger.

PropertyHint PROPERTY_HINT_NODE_PATH_VALID_TYPES = 26

Hints that the hint string specifies valid node types for property of type NodePath.

PropertyHint PROPERTY_HINT_SAVE_FILE = 27

Hints that a String property is a path to a file. Editing it will show a file dialog for picking the path for the file to be saved at. The dialog has access to the project's directory. The hint string can be a set of filters with wildcards like "*.png,*.jpg". See also FileDialog.filters.

PropertyHint PROPERTY_HINT_GLOBAL_SAVE_FILE = 28

Hints that a String property is a path to a file. Editing it will show a file dialog for picking the path for the file to be saved at. The dialog has access to the entire filesystem. The hint string can be a set of filters with wildcards like "*.png,*.jpg". See also FileDialog.filters.

PropertyHint PROPERTY_HINT_INT_IS_OBJECTID = 29

Deprecated: This hint is not used by the engine.

PropertyHint PROPERTY_HINT_INT_IS_POINTER = 30

Hints that an int property is a pointer. Used by GDExtension.

PropertyHint PROPERTY_HINT_ARRAY_TYPE = 31

Hints that a property is an Array with the stored type specified in the hint string. The hint string contains the type of the array (e.g. "String").

Use the hint string format from PROPERTY_HINT_TYPE_STRING for more control over the stored type.

PropertyHint PROPERTY_HINT_DICTIONARY_TYPE = 38

Hints that a property is a Dictionary with the stored types specified in the hint string. The hint string contains the key and value types separated by a semicolon (e.g. "int;String").

Use the hint string format from PROPERTY_HINT_TYPE_STRING for more control over the stored types.

PropertyHint PROPERTY_HINT_LOCALE_ID = 32

Hints that a string property is a locale code. Editing it will show a locale dialog for picking language and country.

PropertyHint PROPERTY_HINT_LOCALIZABLE_STRING = 33

Hints that a dictionary property is string translation map. Dictionary keys are locale codes and, values are translated strings.

PropertyHint PROPERTY_HINT_NODE_TYPE = 34

Hints that a property is an instance of a Node-derived type, optionally specified via the hint string (e.g. "Node2D"). Editing it will show a dialog for picking a node from the scene.

PropertyHint PROPERTY_HINT_HIDE_QUATERNION_EDIT = 35

Hints that a quaternion property should disable the temporary euler editor.

PropertyHint PROPERTY_HINT_PASSWORD = 36

Hints that a string property is a password, and every character is replaced with the secret character.

PropertyHint PROPERTY_HINT_TOOL_BUTTON = 39

Hints that a Callable property should be displayed as a clickable button. When the button is pressed, the callable is called. The hint string specifies the button text and optionally an icon from the "EditorIcons" theme type.

Note: A Callable cannot be properly serialized and stored in a file, so it is recommended to use PROPERTY_USAGE_EDITOR instead of PROPERTY_USAGE_DEFAULT.

PropertyHint PROPERTY_HINT_ONESHOT = 40

Hints that a property will be changed on its own after setting, such as AudioStreamPlayer.playing or GPUParticles3D.emitting.

PropertyHint PROPERTY_HINT_GROUP_ENABLE = 42

Hints that a boolean property will enable the feature associated with the group that it occurs in. The property will be displayed as a checkbox on the group header. Only works within a group or subgroup.

By default, disabling the property hides all properties in the group. Use the optional hint string "checkbox_only" to disable this behavior.

PropertyHint PROPERTY_HINT_INPUT_NAME = 43

Hints that a String or StringName property is the name of an input action. This allows the selection of any action name from the Input Map in the Project Settings. The hint string may contain two options separated by commas:

If it contains "show_builtin", built-in input actions are included in the selection.

If it contains "loose_mode", loose mode is enabled. This allows inserting any action name even if it's not present in the input map.

PropertyHint PROPERTY_HINT_FILE_PATH = 44

Like PROPERTY_HINT_FILE, but the property is stored as a raw path, not UID. That means the reference will be broken if you move the file. Consider using PROPERTY_HINT_FILE when possible.

PropertyHint PROPERTY_HINT_MAX = 45

Represents the size of the PropertyHint enum.

flags PropertyUsageFlags: 🔗

PropertyUsageFlags PROPERTY_USAGE_NONE = 0

The property is not stored, and does not display in the editor. This is the default for non-exported properties.

PropertyUsageFlags PROPERTY_USAGE_STORAGE = 2

The property is serialized and saved in the scene file (default for exported properties).

PropertyUsageFlags PROPERTY_USAGE_EDITOR = 4

The property is shown in the EditorInspector (default for exported properties).

PropertyUsageFlags PROPERTY_USAGE_INTERNAL = 8

The property is excluded from the class reference.

PropertyUsageFlags PROPERTY_USAGE_CHECKABLE = 16

The property can be checked in the EditorInspector.

PropertyUsageFlags PROPERTY_USAGE_CHECKED = 32

The property is checked in the EditorInspector.

PropertyUsageFlags PROPERTY_USAGE_GROUP = 64

Used to group properties together in the editor. See EditorInspector.

PropertyUsageFlags PROPERTY_USAGE_CATEGORY = 128

Used to categorize properties together in the editor.

PropertyUsageFlags PROPERTY_USAGE_SUBGROUP = 256

Used to group properties together in the editor in a subgroup (under a group). See EditorInspector.

PropertyUsageFlags PROPERTY_USAGE_CLASS_IS_BITFIELD = 512

The property is a bitfield, i.e. it contains multiple flags represented as bits.

PropertyUsageFlags PROPERTY_USAGE_NO_INSTANCE_STATE = 1024

The property does not save its state in PackedScene.

PropertyUsageFlags PROPERTY_USAGE_RESTART_IF_CHANGED = 2048

Editing the property prompts the user for restarting the editor.

PropertyUsageFlags PROPERTY_USAGE_SCRIPT_VARIABLE = 4096

The property is a script variable. PROPERTY_USAGE_SCRIPT_VARIABLE can be used to distinguish between exported script variables from built-in variables (which don't have this usage flag). By default, PROPERTY_USAGE_SCRIPT_VARIABLE is not applied to variables that are created by overriding Object._get_property_list() in a script.

PropertyUsageFlags PROPERTY_USAGE_STORE_IF_NULL = 8192

The property value of type Object will be stored even if its value is null.

PropertyUsageFlags PROPERTY_USAGE_UPDATE_ALL_IF_MODIFIED = 16384

If this property is modified, all inspector fields will be refreshed.

PropertyUsageFlags PROPERTY_USAGE_SCRIPT_DEFAULT_VALUE = 32768

Deprecated: This flag is not used by the engine.

PropertyUsageFlags PROPERTY_USAGE_CLASS_IS_ENUM = 65536

The property is a variable of enum type, i.e. it only takes named integer constants from its associated enumeration.

PropertyUsageFlags PROPERTY_USAGE_NIL_IS_VARIANT = 131072

If property has nil as default value, its type will be Variant.

PropertyUsageFlags PROPERTY_USAGE_ARRAY = 262144

The property is an array.

PropertyUsageFlags PROPERTY_USAGE_ALWAYS_DUPLICATE = 524288

When duplicating a resource with Resource.duplicate(), and this flag is set on a property of that resource, the property should always be duplicated, regardless of the subresources bool parameter.

PropertyUsageFlags PROPERTY_USAGE_NEVER_DUPLICATE = 1048576

When duplicating a resource with Resource.duplicate(), and this flag is set on a property of that resource, the property should never be duplicated, regardless of the subresources bool parameter.

PropertyUsageFlags PROPERTY_USAGE_HIGH_END_GFX = 2097152

The property is only shown in the editor if modern renderers are supported (the Compatibility rendering method is excluded).

PropertyUsageFlags PROPERTY_USAGE_NODE_PATH_FROM_SCENE_ROOT = 4194304

The NodePath property will always be relative to the scene's root. Mostly useful for local resources.

PropertyUsageFlags PROPERTY_USAGE_RESOURCE_NOT_PERSISTENT = 8388608

Use when a resource is created on the fly, i.e. the getter will always return a different instance. ResourceSaver needs this information to properly save such resources.

PropertyUsageFlags PROPERTY_USAGE_KEYING_INCREMENTS = 16777216

Inserting an animation key frame of this property will automatically increment the value, allowing to easily keyframe multiple values in a row.

PropertyUsageFlags PROPERTY_USAGE_DEFERRED_SET_RESOURCE = 33554432

Deprecated: This flag is not used by the engine.

PropertyUsageFlags PROPERTY_USAGE_EDITOR_INSTANTIATE_OBJECT = 67108864

When this property is a Resource and base object is a Node, a resource instance will be automatically created whenever the node is created in the editor.

PropertyUsageFlags PROPERTY_USAGE_EDITOR_BASIC_SETTING = 134217728

The property is considered a basic setting and will appear even when advanced mode is disabled. Used for project settings.

PropertyUsageFlags PROPERTY_USAGE_READ_ONLY = 268435456

The property is read-only in the EditorInspector.

PropertyUsageFlags PROPERTY_USAGE_SECRET = 536870912

An export preset property with this flag contains confidential information and is stored separately from the rest of the export preset configuration.

PropertyUsageFlags PROPERTY_USAGE_DEFAULT = 6

Default usage (storage and editor).

PropertyUsageFlags PROPERTY_USAGE_NO_EDITOR = 2

Default usage but without showing the property in the editor (storage).

MethodFlags METHOD_FLAG_NORMAL = 1

Flag for a normal method.

MethodFlags METHOD_FLAG_EDITOR = 2

Flag for an editor method.

MethodFlags METHOD_FLAG_CONST = 4

Flag for a constant method.

MethodFlags METHOD_FLAG_VIRTUAL = 8

Flag for a virtual method.

MethodFlags METHOD_FLAG_VARARG = 16

Flag for a method with a variable number of arguments.

MethodFlags METHOD_FLAG_STATIC = 32

Flag for a static method.

MethodFlags METHOD_FLAG_OBJECT_CORE = 64

Used internally. Allows to not dump core virtual methods (such as Object._notification()) to the JSON API.

MethodFlags METHOD_FLAG_VIRTUAL_REQUIRED = 128

Flag for a virtual method that is required. In GDScript, this flag is set for abstract functions.

MethodFlags METHOD_FLAGS_DEFAULT = 1

Default method flags (normal).

Variant.Type TYPE_NIL = 0

Variant.Type TYPE_BOOL = 1

Variable is of type bool.

Variant.Type TYPE_INT = 2

Variable is of type int.

Variant.Type TYPE_FLOAT = 3

Variable is of type float.

Variant.Type TYPE_STRING = 4

Variable is of type String.

Variant.Type TYPE_VECTOR2 = 5

Variable is of type Vector2.

Variant.Type TYPE_VECTOR2I = 6

Variable is of type Vector2i.

Variant.Type TYPE_RECT2 = 7

Variable is of type Rect2.

Variant.Type TYPE_RECT2I = 8

Variable is of type Rect2i.

Variant.Type TYPE_VECTOR3 = 9

Variable is of type Vector3.

Variant.Type TYPE_VECTOR3I = 10

Variable is of type Vector3i.

Variant.Type TYPE_TRANSFORM2D = 11

Variable is of type Transform2D.

Variant.Type TYPE_VECTOR4 = 12

Variable is of type Vector4.

Variant.Type TYPE_VECTOR4I = 13

Variable is of type Vector4i.

Variant.Type TYPE_PLANE = 14

Variable is of type Plane.

Variant.Type TYPE_QUATERNION = 15

Variable is of type Quaternion.

Variant.Type TYPE_AABB = 16

Variable is of type AABB.

Variant.Type TYPE_BASIS = 17

Variable is of type Basis.

Variant.Type TYPE_TRANSFORM3D = 18

Variable is of type Transform3D.

Variant.Type TYPE_PROJECTION = 19

Variable is of type Projection.

Variant.Type TYPE_COLOR = 20

Variable is of type Color.

Variant.Type TYPE_STRING_NAME = 21

Variable is of type StringName.

Variant.Type TYPE_NODE_PATH = 22

Variable is of type NodePath.

Variant.Type TYPE_RID = 23

Variable is of type RID.

Variant.Type TYPE_OBJECT = 24

Variable is of type Object.

Variant.Type TYPE_CALLABLE = 25

Variable is of type Callable.

Variant.Type TYPE_SIGNAL = 26

Variable is of type Signal.

Variant.Type TYPE_DICTIONARY = 27

Variable is of type Dictionary.

Variant.Type TYPE_ARRAY = 28

Variable is of type Array.

Variant.Type TYPE_PACKED_BYTE_ARRAY = 29

Variable is of type PackedByteArray.

Variant.Type TYPE_PACKED_INT32_ARRAY = 30

Variable is of type PackedInt32Array.

Variant.Type TYPE_PACKED_INT64_ARRAY = 31

Variable is of type PackedInt64Array.

Variant.Type TYPE_PACKED_FLOAT32_ARRAY = 32

Variable is of type PackedFloat32Array.

Variant.Type TYPE_PACKED_FLOAT64_ARRAY = 33

Variable is of type PackedFloat64Array.

Variant.Type TYPE_PACKED_STRING_ARRAY = 34

Variable is of type PackedStringArray.

Variant.Type TYPE_PACKED_VECTOR2_ARRAY = 35

Variable is of type PackedVector2Array.

Variant.Type TYPE_PACKED_VECTOR3_ARRAY = 36

Variable is of type PackedVector3Array.

Variant.Type TYPE_PACKED_COLOR_ARRAY = 37

Variable is of type PackedColorArray.

Variant.Type TYPE_PACKED_VECTOR4_ARRAY = 38

Variable is of type PackedVector4Array.

Variant.Type TYPE_MAX = 39

Represents the size of the Variant.Type enum.

enum Variant.Operator: 🔗

Variant.Operator OP_EQUAL = 0

Equality operator (==).

Variant.Operator OP_NOT_EQUAL = 1

Inequality operator (!=).

Variant.Operator OP_LESS = 2

Less than operator (<).

Variant.Operator OP_LESS_EQUAL = 3

Less than or equal operator (<=).

Variant.Operator OP_GREATER = 4

Greater than operator (>).

Variant.Operator OP_GREATER_EQUAL = 5

Greater than or equal operator (>=).

Variant.Operator OP_ADD = 6

Addition operator (+).

Variant.Operator OP_SUBTRACT = 7

Subtraction operator (-).

Variant.Operator OP_MULTIPLY = 8

Multiplication operator (*).

Variant.Operator OP_DIVIDE = 9

Division operator (/).

Variant.Operator OP_NEGATE = 10

Unary negation operator (-).

Variant.Operator OP_POSITIVE = 11

Unary plus operator (+).

Variant.Operator OP_MODULE = 12

Remainder/modulo operator (%).

Variant.Operator OP_POWER = 13

Variant.Operator OP_SHIFT_LEFT = 14

Left shift operator (<<).

Variant.Operator OP_SHIFT_RIGHT = 15

Right shift operator (>>).

Variant.Operator OP_BIT_AND = 16

Bitwise AND operator (&).

Variant.Operator OP_BIT_OR = 17

Bitwise OR operator (|).

Variant.Operator OP_BIT_XOR = 18

Bitwise XOR operator (^).

Variant.Operator OP_BIT_NEGATE = 19

Bitwise NOT operator (~).

Variant.Operator OP_AND = 20

Logical AND operator (and or &&).

Variant.Operator OP_OR = 21

Logical OR operator (or or ||).

Variant.Operator OP_XOR = 22

Logical XOR operator (not implemented in GDScript).

Variant.Operator OP_NOT = 23

Logical NOT operator (not or !).

Variant.Operator OP_IN = 24

Logical IN operator (in).

Variant.Operator OP_MAX = 25

Represents the size of the Variant.Operator enum.

AudioServer AudioServer 🔗

The AudioServer singleton.

CameraServer CameraServer 🔗

The CameraServer singleton.

The ClassDB singleton.

DisplayServer DisplayServer 🔗

The DisplayServer singleton.

EditorInterface EditorInterface 🔗

The EditorInterface singleton.

Note: Only available in editor builds.

The Engine singleton.

EngineDebugger EngineDebugger 🔗

The EngineDebugger singleton.

GDExtensionManager GDExtensionManager 🔗

The GDExtensionManager singleton.

Geometry2D Geometry2D 🔗

The Geometry2D singleton.

Geometry3D Geometry3D 🔗

The Geometry3D singleton.

The InputMap singleton.

JavaClassWrapper JavaClassWrapper 🔗

The JavaClassWrapper singleton.

Note: Only implemented on Android.

JavaScriptBridge JavaScriptBridge 🔗

The JavaScriptBridge singleton.

Note: Only implemented on the Web platform.

Marshalls Marshalls 🔗

The Marshalls singleton.

NativeMenu NativeMenu 🔗

The NativeMenu singleton.

Note: Only implemented on macOS.

NavigationMeshGenerator NavigationMeshGenerator 🔗

The NavigationMeshGenerator singleton.

NavigationServer2D NavigationServer2D 🔗

The NavigationServer2D singleton.

NavigationServer3D NavigationServer3D 🔗

The NavigationServer3D singleton.

Performance Performance 🔗

The Performance singleton.

PhysicsServer2D PhysicsServer2D 🔗

The PhysicsServer2D singleton.

PhysicsServer2DManager PhysicsServer2DManager 🔗

The PhysicsServer2DManager singleton.

PhysicsServer3D PhysicsServer3D 🔗

The PhysicsServer3D singleton.

PhysicsServer3DManager PhysicsServer3DManager 🔗

The PhysicsServer3DManager singleton.

ProjectSettings ProjectSettings 🔗

The ProjectSettings singleton.

RenderingServer RenderingServer 🔗

The RenderingServer singleton.

ResourceLoader ResourceLoader 🔗

The ResourceLoader singleton.

ResourceSaver ResourceSaver 🔗

The ResourceSaver singleton.

ResourceUID ResourceUID 🔗

The ResourceUID singleton.

TextServerManager TextServerManager 🔗

The TextServerManager singleton.

The ThemeDB singleton.

TranslationServer TranslationServer 🔗

The TranslationServer singleton.

WorkerThreadPool WorkerThreadPool 🔗

The WorkerThreadPool singleton.

The XRServer singleton.

Variant abs(x: Variant) 🔗

Returns the absolute value of a Variant parameter x (i.e. non-negative value). Supported types: int, float, Vector2, Vector2i, Vector3, Vector3i, Vector4, Vector4i.

Note: For better type safety, use absf(), absi(), Vector2.abs(), Vector2i.abs(), Vector3.abs(), Vector3i.abs(), Vector4.abs(), or Vector4i.abs().

float absf(x: float) 🔗

Returns the absolute value of float parameter x (i.e. positive value).

Returns the absolute value of int parameter x (i.e. positive value).

float acos(x: float) 🔗

Returns the arc cosine of x in radians. Use to get the angle of cosine x. x will be clamped between -1.0 and 1.0 (inclusive), in order to prevent acos() from returning @GDScript.NAN.

float acosh(x: float) 🔗

Returns the hyperbolic arc (also called inverse) cosine of x, returning a value in radians. Use it to get the angle from an angle's cosine in hyperbolic space if x is larger or equal to 1. For values of x lower than 1, it will return 0, in order to prevent acosh() from returning @GDScript.NAN.

float angle_difference(from: float, to: float) 🔗

Returns the difference between the two angles (in radians), in the range of [-PI, +PI]. When from and to are opposite, returns -PI if from is smaller than to, or PI otherwise.

float asin(x: float) 🔗

Returns the arc sine of x in radians. Use to get the angle of sine x. x will be clamped between -1.0 and 1.0 (inclusive), in order to prevent asin() from returning @GDScript.NAN.

float asinh(x: float) 🔗

Returns the hyperbolic arc (also called inverse) sine of x, returning a value in radians. Use it to get the angle from an angle's sine in hyperbolic space.

float atan(x: float) 🔗

Returns the arc tangent of x in radians. Use it to get the angle from an angle's tangent in trigonometry.

The method cannot know in which quadrant the angle should fall. See atan2() if you have both y and x.

If x is between -PI / 2 and PI / 2 (inclusive), atan(tan(x)) is equal to x.

float atan2(y: float, x: float) 🔗

Returns the arc tangent of y/x in radians. Use to get the angle of tangent y/x. To compute the value, the method takes into account the sign of both arguments in order to determine the quadrant.

Important note: The Y coordinate comes first, by convention.

float atanh(x: float) 🔗

Returns the hyperbolic arc (also called inverse) tangent of x, returning a value in radians. Use it to get the angle from an angle's tangent in hyperbolic space if x is between -1 and 1 (non-inclusive).

In mathematics, the inverse hyperbolic tangent is only defined for -1 < x < 1 in the real set, so values equal or lower to -1 for x return negative @GDScript.INF and values equal or higher than 1 return positive @GDScript.INF in order to prevent atanh() from returning @GDScript.NAN.

float bezier_derivative(start: float, control_1: float, control_2: float, end: float, t: float) 🔗

Returns the derivative at the given t on a one-dimensional Bézier curve defined by the given control_1, control_2, and end points.

float bezier_interpolate(start: float, control_1: float, control_2: float, end: float, t: float) 🔗

Returns the point at the given t on a one-dimensional Bézier curve defined by the given control_1, control_2, and end points.

Variant bytes_to_var(bytes: PackedByteArray) 🔗

Decodes a byte array back to a Variant value, without decoding objects.

Note: If you need object deserialization, see bytes_to_var_with_objects().

Variant bytes_to_var_with_objects(bytes: PackedByteArray) 🔗

Decodes a byte array back to a Variant value. Decoding objects is allowed.

Warning: Deserialized object can contain code which gets executed. Do not use this option if the serialized object comes from untrusted sources to avoid potential security threats (remote code execution).

Variant ceil(x: Variant) 🔗

Rounds x upward (towards positive infinity), returning the smallest whole number that is not less than x. Supported types: int, float, Vector2, Vector2i, Vector3, Vector3i, Vector4, Vector4i.

See also floor(), round(), and snapped().

Note: For better type safety, use ceilf(), ceili(), Vector2.ceil(), Vector3.ceil(), or Vector4.ceil().

float ceilf(x: float) 🔗

Rounds x upward (towards positive infinity), returning the smallest whole number that is not less than x.

A type-safe version of ceil(), returning a float.

int ceili(x: float) 🔗

Rounds x upward (towards positive infinity), returning the smallest whole number that is not less than x.

A type-safe version of ceil(), returning an int.

Variant clamp(value: Variant, min: Variant, max: Variant) 🔗

Clamps the value, returning a Variant not less than min and not more than max. Any values that can be compared with the less than and greater than operators will work.

Note: For better type safety, use clampf(), clampi(), Vector2.clamp(), Vector2i.clamp(), Vector3.clamp(), Vector3i.clamp(), Vector4.clamp(), Vector4i.clamp(), or Color.clamp() (not currently supported by this method).

Note: When using this on vectors it will not perform component-wise clamping, and will pick min if value < min or max if value > max. To perform component-wise clamping use the methods listed above.

float clampf(value: float, min: float, max: float) 🔗

Clamps the value, returning a float not less than min and not more than max.

int clampi(value: int, min: int, max: int) 🔗

Clamps the value, returning an int not less than min and not more than max.

float cos(angle_rad: float) 🔗

Returns the cosine of angle angle_rad in radians.

float cosh(x: float) 🔗

Returns the hyperbolic cosine of x in radians.

float cubic_interpolate(from: float, to: float, pre: float, post: float, weight: float) 🔗

Cubic interpolates between two values by the factor defined in weight with pre and post values.

float cubic_interpolate_angle(from: float, to: float, pre: float, post: float, weight: float) 🔗

Cubic interpolates between two rotation values with shortest path by the factor defined in weight with pre and post values. See also lerp_angle().

float cubic_interpolate_angle_in_time(from: float, to: float, pre: float, post: float, weight: float, to_t: float, pre_t: float, post_t: float) 🔗

Cubic interpolates between two rotation values with shortest path by the factor defined in weight with pre and post values. See also lerp_angle().

It can perform smoother interpolation than cubic_interpolate() by the time values.

float cubic_interpolate_in_time(from: float, to: float, pre: float, post: float, weight: float, to_t: float, pre_t: float, post_t: float) 🔗

Cubic interpolates between two values by the factor defined in weight with pre and post values.

It can perform smoother interpolation than cubic_interpolate() by the time values.

float db_to_linear(db: float) 🔗

Converts from decibels to linear energy (audio).

float deg_to_rad(deg: float) 🔗

Converts an angle expressed in degrees to radians.

float ease(x: float, curve: float) 🔗

Returns an "eased" value of x based on an easing function defined with curve. This easing function is based on an exponent. The curve can be any floating-point number, with specific values leading to the following behaviors:

ease() curve values cheatsheet

See also smoothstep(). If you need to perform more advanced transitions, use Tween.interpolate_value().

String error_string(error: int) 🔗

Returns a human-readable name for the given Error code.

float exp(x: float) 🔗

The natural exponential function. It raises the mathematical constant e to the power of x and returns it.

e has an approximate value of 2.71828, and can be obtained with exp(1).

For exponents to other bases use the method pow().

Variant floor(x: Variant) 🔗

Rounds x downward (towards negative infinity), returning the largest whole number that is not more than x. Supported types: int, float, Vector2, Vector2i, Vector3, Vector3i, Vector4, Vector4i.

See also ceil(), round(), and snapped().

Note: For better type safety, use floorf(), floori(), Vector2.floor(), Vector3.floor(), or Vector4.floor().

float floorf(x: float) 🔗

Rounds x downward (towards negative infinity), returning the largest whole number that is not more than x.

A type-safe version of floor(), returning a float.

int floori(x: float) 🔗

Rounds x downward (towards negative infinity), returning the largest whole number that is not more than x.

A type-safe version of floor(), returning an int.

Note: This function is not the same as int(x), which rounds towards 0.

float fmod(x: float, y: float) 🔗

Returns the floating-point remainder of x divided by y, keeping the sign of x.

For the integer remainder operation, use the % operator.

float fposmod(x: float, y: float) 🔗

Returns the floating-point modulus of x divided by y, wrapping equally in positive and negative.

int hash(variable: Variant) 🔗

Returns the integer hash of the passed variable.

Object instance_from_id(instance_id: int) 🔗

Returns the Object that corresponds to instance_id. All Objects have a unique instance ID. See also Object.get_instance_id().

float inverse_lerp(from: float, to: float, weight: float) 🔗

Returns an interpolation or extrapolation factor considering the range specified in from and to, and the interpolated value specified in weight. The returned value will be between 0.0 and 1.0 if weight is between from and to (inclusive). If weight is located outside this range, then an extrapolation factor will be returned (return value lower than 0.0 or greater than 1.0). Use clamp() on the result of inverse_lerp() if this is not desired.

See also lerp(), which performs the reverse of this operation, and remap() to map a continuous series of values to another.

bool is_equal_approx(a: float, b: float) 🔗

Returns true if a and b are approximately equal to each other.

Here, "approximately equal" means that a and b are within a small internal epsilon of each other, which scales with the magnitude of the numbers.

Infinity values of the same sign are considered equal.

bool is_finite(x: float) 🔗

Returns whether x is a finite value, i.e. it is not @GDScript.NAN, positive infinity, or negative infinity. See also is_inf() and is_nan().

bool is_inf(x: float) 🔗

Returns true if x is either positive infinity or negative infinity. See also is_finite() and is_nan().

bool is_instance_id_valid(id: int) 🔗

Returns true if the Object that corresponds to id is a valid object (e.g. has not been deleted from memory). All Objects have a unique instance ID.

bool is_instance_valid(instance: Variant) 🔗

Returns true if instance is a valid Object (e.g. has not been deleted from memory).

bool is_nan(x: float) 🔗

Returns true if x is a NaN ("Not a Number" or invalid) value. This method is needed as @GDScript.NAN is not equal to itself, which means x == NAN can't be used to check whether a value is a NaN.

bool is_same(a: Variant, b: Variant) 🔗

Returns true, for value types, if a and b share the same value. Returns true, for reference types, if the references of a and b are the same.

These are Variant value types: null, bool, int, float, String, StringName, Vector2, Vector2i, Vector3, Vector3i, Vector4, Vector4i, Rect2, Rect2i, Transform2D, Transform3D, Plane, Quaternion, AABB, Basis, Projection, Color, NodePath, RID, Callable and Signal.

These are Variant reference types: Object, Dictionary, Array, PackedByteArray, PackedInt32Array, PackedInt64Array, PackedFloat32Array, PackedFloat64Array, PackedStringArray, PackedVector2Array, PackedVector3Array, PackedVector4Array, and PackedColorArray.

bool is_zero_approx(x: float) 🔗

Returns true if x is zero or almost zero. The comparison is done using a tolerance calculation with a small internal epsilon.

This function is faster than using is_equal_approx() with one value as zero.

Variant lerp(from: Variant, to: Variant, weight: Variant) 🔗

Linearly interpolates between two values by the factor defined in weight. To perform interpolation, weight should be between 0.0 and 1.0 (inclusive). However, values outside this range are allowed and can be used to perform extrapolation. If this is not desired, use clampf() to limit weight.

Both from and to must be the same type. Supported types: int, float, Vector2, Vector3, Vector4, Color, Quaternion, Basis, Transform2D, Transform3D.

See also inverse_lerp() which performs the reverse of this operation. To perform eased interpolation with lerp(), combine it with ease() or smoothstep(). See also remap() to map a continuous series of values to another.

Note: For better type safety, use lerpf(), Vector2.lerp(), Vector3.lerp(), Vector4.lerp(), Color.lerp(), Quaternion.slerp(), Basis.slerp(), Transform2D.interpolate_with(), or Transform3D.interpolate_with().

float lerp_angle(from: float, to: float, weight: float) 🔗

Linearly interpolates between two angles (in radians) by a weight value between 0.0 and 1.0.

Similar to lerp(), but interpolates correctly when the angles wrap around @GDScript.TAU. To perform eased interpolation with lerp_angle(), combine it with ease() or smoothstep().

Note: This function lerps through the shortest path between from and to. However, when these two angles are approximately PI + k * TAU apart for any integer k, it's not obvious which way they lerp due to floating-point precision errors. For example, lerp_angle(0, PI, weight) lerps counter-clockwise, while lerp_angle(0, PI + 5 * TAU, weight) lerps clockwise.

float lerpf(from: float, to: float, weight: float) 🔗

Linearly interpolates between two values by the factor defined in weight. To perform interpolation, weight should be between 0.0 and 1.0 (inclusive). However, values outside this range are allowed and can be used to perform extrapolation. If this is not desired, use clampf() on the result of this function.

See also inverse_lerp() which performs the reverse of this operation. To perform eased interpolation with lerp(), combine it with ease() or smoothstep().

float linear_to_db(lin: float) 🔗

Converts from linear energy to decibels (audio). Since volume is not normally linear, this can be used to implement volume sliders that behave as expected.

Example: Change the Master bus's volume through a Slider node, which ranges from 0.0 to 1.0:

float log(x: float) 🔗

Returns the natural logarithm of x (base [i]e[/i], with e being approximately 2.71828). This is the amount of time needed to reach a certain level of continuous growth.

Note: This is not the same as the "log" function on most calculators, which uses a base 10 logarithm. To use base 10 logarithm, use log(x) / log(10).

Note: The logarithm of 0 returns -inf, while negative values return -nan.

Variant max(...) vararg 🔗

Returns the maximum of the given numeric values. This function can take any number of arguments.

Note: When using this on vectors it will not perform component-wise maximum, and will pick the largest value when compared using x < y. To perform component-wise maximum, use Vector2.max(), Vector2i.max(), Vector3.max(), Vector3i.max(), Vector4.max(), and Vector4i.max().

float maxf(a: float, b: float) 🔗

Returns the maximum of two float values.

int maxi(a: int, b: int) 🔗

Returns the maximum of two int values.

Variant min(...) vararg 🔗

Returns the minimum of the given numeric values. This function can take any number of arguments.

Note: When using this on vectors it will not perform component-wise minimum, and will pick the smallest value when compared using x < y. To perform component-wise minimum, use Vector2.min(), Vector2i.min(), Vector3.min(), Vector3i.min(), Vector4.min(), and Vector4i.min().

float minf(a: float, b: float) 🔗

Returns the minimum of two float values.

int mini(a: int, b: int) 🔗

Returns the minimum of two int values.

float move_toward(from: float, to: float, delta: float) 🔗

Moves from toward to by the delta amount. Will not go past to.

Use a negative delta value to move away.

int nearest_po2(value: int) 🔗

Returns the smallest integer power of 2 that is greater than or equal to value.

Warning: Due to its implementation, this method returns 0 rather than 1 for values less than or equal to 0, with an exception for value being the smallest negative 64-bit integer (-9223372036854775808) in which case the value is returned unchanged.

float pingpong(value: float, length: float) 🔗

Wraps value between 0 and the length. If the limit is reached, the next value the function returns is decreased to the 0 side or increased to the length side (like a triangle wave). If length is less than zero, it becomes positive.

int posmod(x: int, y: int) 🔗

Returns the integer modulus of x divided by y that wraps equally in positive and negative.

float pow(base: float, exp: float) 🔗

Returns the result of base raised to the power of exp.

In GDScript, this is the equivalent of the ** operator.

void print(...) vararg 🔗

Converts one or more arguments of any type to string in the best way possible and prints them to the console.

Note: Consider using push_error() and push_warning() to print error and warning messages instead of print() or print_rich(). This distinguishes them from print messages used for debugging purposes, while also displaying a stack trace when an error or warning is printed. See also Engine.print_to_stdout and ProjectSettings.application/run/disable_stdout.

void print_rich(...) vararg 🔗

Converts one or more arguments of any type to string in the best way possible and prints them to the console.

The following BBCode tags are supported: b, i, u, s, indent, code, url, center, right, color, bgcolor, fgcolor.

URL tags only support URLs wrapped by a URL tag, not URLs with a different title.

When printing to standard output, the supported subset of BBCode is converted to ANSI escape codes for the terminal emulator to display. Support for ANSI escape codes varies across terminal emulators, especially for italic and strikethrough. In standard output, code is represented with faint text but without any font change. Unsupported tags are left as-is in standard output.

Note: Consider using push_error() and push_warning() to print error and warning messages instead of print() or print_rich(). This distinguishes them from print messages used for debugging purposes, while also displaying a stack trace when an error or warning is printed.

Note: Output displayed in the editor supports clickable [url=address]text[/url] tags. The [url] tag's address value is handled by OS.shell_open() when clicked.

void print_verbose(...) vararg 🔗

If verbose mode is enabled (OS.is_stdout_verbose() returning true), converts one or more arguments of any type to string in the best way possible and prints them to the console.

void printerr(...) vararg 🔗

Prints one or more arguments to strings in the best way possible to standard error line.

void printraw(...) vararg 🔗

Prints one or more arguments to strings in the best way possible to the OS terminal. Unlike print(), no newline is automatically added at the end.

Note: The OS terminal is not the same as the editor's Output dock. The output sent to the OS terminal can be seen when running Godot from a terminal. On Windows, this requires using the console.exe executable.

void prints(...) vararg 🔗

Prints one or more arguments to the console with a space between each argument.

void printt(...) vararg 🔗

Prints one or more arguments to the console with a tab between each argument.

void push_error(...) vararg 🔗

Pushes an error message to Godot's built-in debugger and to the OS terminal.

Note: This function does not pause project execution. To print an error message and pause project execution in debug builds, use assert(false, "test error") instead.

void push_warning(...) vararg 🔗

Pushes a warning message to Godot's built-in debugger and to the OS terminal.

float rad_to_deg(rad: float) 🔗

Converts an angle expressed in radians to degrees.

PackedInt64Array rand_from_seed(seed: int) 🔗

Given a seed, returns a PackedInt64Array of size 2, where its first element is the randomized int value, and the second element is the same as seed. Passing the same seed consistently returns the same array.

Note: "Seed" here refers to the internal state of the pseudo random number generator, currently implemented as a 64 bit integer.

Returns a random floating-point value between 0.0 and 1.0 (inclusive).

float randf_range(from: float, to: float) 🔗

Returns a random floating-point value between from and to (inclusive).

float randfn(mean: float, deviation: float) 🔗

Returns a normally-distributed, pseudo-random floating-point value from the specified mean and a standard deviation. This is also known as a Gaussian distribution.

Note: This method uses the Box-Muller transform algorithm.

Returns a random unsigned 32-bit integer. Use remainder to obtain a random value in the interval [0, N - 1] (where N is smaller than 2^32).

int randi_range(from: int, to: int) 🔗

Returns a random signed 32-bit integer between from and to (inclusive). If to is lesser than from, they are swapped.

Randomizes the seed (or the internal state) of the random number generator. The current implementation uses a number based on the device's time.

Note: This function is called automatically when the project is run. If you need to fix the seed to have consistent, reproducible results, use seed() to initialize the random number generator.

float remap(value: float, istart: float, istop: float, ostart: float, ostop: float) 🔗

Maps a value from range [istart, istop] to [ostart, ostop]. See also lerp() and inverse_lerp(). If value is outside [istart, istop], then the resulting value will also be outside [ostart, ostop]. If this is not desired, use clamp() on the result of this function.

For complex use cases where multiple ranges are needed, consider using Curve or Gradient instead.

Note: If istart == istop, the return value is undefined (most likely NaN, INF, or -INF).

int rid_allocate_id() 🔗

Allocates a unique ID which can be used by the implementation to construct an RID. This is used mainly from native extensions to implement servers.

RID rid_from_int64(base: int) 🔗

Creates an RID from a base. This is used mainly from native extensions to build servers.

float rotate_toward(from: float, to: float, delta: float) 🔗

Rotates from toward to by the delta amount. Will not go past to.

Similar to move_toward(), but interpolates correctly when the angles wrap around @GDScript.TAU.

If delta is negative, this function will rotate away from to, toward the opposite angle, and will not go past the opposite angle.

Variant round(x: Variant) 🔗

Rounds x to the nearest whole number, with halfway cases rounded away from 0. Supported types: int, float, Vector2, Vector2i, Vector3, Vector3i, Vector4, Vector4i.

See also floor(), ceil(), and snapped().

Note: For better type safety, use roundf(), roundi(), Vector2.round(), Vector3.round(), or Vector4.round().

float roundf(x: float) 🔗

Rounds x to the nearest whole number, with halfway cases rounded away from 0.

A type-safe version of round(), returning a float.

int roundi(x: float) 🔗

Rounds x to the nearest whole number, with halfway cases rounded away from 0.

A type-safe version of round(), returning an int.

void seed(base: int) 🔗

Sets the seed for the random number generator to base. Setting the seed manually can ensure consistent, repeatable results for most random functions.

Variant sign(x: Variant) 🔗

Returns the same type of Variant as x, with -1 for negative values, 1 for positive values, and 0 for zeros. For nan values it returns 0.

Supported types: int, float, Vector2, Vector2i, Vector3, Vector3i, Vector4, Vector4i.

Note: For better type safety, use signf(), signi(), Vector2.sign(), Vector2i.sign(), Vector3.sign(), Vector3i.sign(), Vector4.sign(), or Vector4i.sign().

float signf(x: float) 🔗

Returns -1.0 if x is negative, 1.0 if x is positive, and 0.0 if x is zero. For nan values of x it returns 0.0.

Returns -1 if x is negative, 1 if x is positive, and 0 if x is zero.

float sin(angle_rad: float) 🔗

Returns the sine of angle angle_rad in radians.

float sinh(x: float) 🔗

Returns the hyperbolic sine of x.

float smoothstep(from: float, to: float, x: float) 🔗

Returns a smooth cubic Hermite interpolation between 0 and 1.

For positive ranges (when from <= to) the return value is 0 when x <= from, and 1 when x >= to. If x lies between from and to, the return value follows an S-shaped curve that smoothly transitions from 0 to 1.

For negative ranges (when from > to) the function is mirrored and returns 1 when x <= to and 0 when x >= from.

This S-shaped curve is the cubic Hermite interpolator, given by f(y) = 3*y^2 - 2*y^3 where y = (x-from) / (to-from).

Compared to ease() with a curve value of -1.6521, smoothstep() returns the smoothest possible curve with no sudden changes in the derivative. If you need to perform more advanced transitions, use Tween or AnimationPlayer.

Comparison between smoothstep() and ease(x, -1.6521) return values

Smoothstep() return values with positive, zero, and negative ranges

Variant snapped(x: Variant, step: Variant) 🔗

Returns the multiple of step that is the closest to x. This can also be used to round a floating-point number to an arbitrary number of decimals.

The returned value is the same type of Variant as step. Supported types: int, float, Vector2, Vector2i, Vector3, Vector3i, Vector4, Vector4i.

See also ceil(), floor(), and round().

Note: For better type safety, use snappedf(), snappedi(), Vector2.snapped(), Vector2i.snapped(), Vector3.snapped(), Vector3i.snapped(), Vector4.snapped(), or Vector4i.snapped().

float snappedf(x: float, step: float) 🔗

Returns the multiple of step that is the closest to x. This can also be used to round a floating-point number to an arbitrary number of decimals.

A type-safe version of snapped(), returning a float.

int snappedi(x: float, step: int) 🔗

Returns the multiple of step that is the closest to x.

A type-safe version of snapped(), returning an int.

float sqrt(x: float) 🔗

Returns the square root of x, where x is a non-negative number.

Note: Negative values of x return NaN ("Not a Number"). In C#, if you need negative inputs, use System.Numerics.Complex.

int step_decimals(x: float) 🔗

Returns the position of the first non-zero digit, after the decimal point. Note that the maximum return value is 10, which is a design decision in the implementation.

String str(...) vararg 🔗

Converts one or more arguments of any Variant type to a String in the best way possible.

Variant str_to_var(string: String) 🔗

Converts a formatted string that was returned by var_to_str() to the original Variant.

float tan(angle_rad: float) 🔗

Returns the tangent of angle angle_rad in radians.

float tanh(x: float) 🔗

Returns the hyperbolic tangent of x.

Variant type_convert(variant: Variant, type: int) 🔗

Converts the given variant to the given type, using the Variant.Type values. This method is generous with how it handles types, it can automatically convert between array types, convert numeric Strings to int, and converting most things to String.

If the type conversion cannot be done, this method will return the default value for that type, for example converting Rect2 to Vector2 will always return Vector2.ZERO. This method will never show error messages as long as type is a valid Variant type.

The returned value is a Variant, but the data inside and its type will be the same as the requested type.

String type_string(type: int) 🔗

Returns a human-readable name of the given type, using the Variant.Type values.

int typeof(variable: Variant) 🔗

Returns the internal type of the given variable, using the Variant.Type values.

See also type_string().

PackedByteArray var_to_bytes(variable: Variant) 🔗

Encodes a Variant value to a byte array, without encoding objects. Deserialization can be done with bytes_to_var().

Note: If you need object serialization, see var_to_bytes_with_objects().

Note: Encoding Callable is not supported and will result in an empty value, regardless of the data.

PackedByteArray var_to_bytes_with_objects(variable: Variant) 🔗

Encodes a Variant value to a byte array. Encoding objects is allowed (and can potentially include executable code). Deserialization can be done with bytes_to_var_with_objects().

Note: Encoding Callable is not supported and will result in an empty value, regardless of the data.

String var_to_str(variable: Variant) 🔗

Converts a Variant variable to a formatted String that can then be parsed using str_to_var().

Note: Converting Signal or Callable is not supported and will result in an empty value for these types, regardless of their data.

Variant weakref(obj: Variant) 🔗

Returns a WeakRef instance holding a weak reference to obj. Returns an empty WeakRef instance if obj is null. Prints an error and returns null if obj is neither Object-derived nor null.

A weak reference to an object is not enough to keep the object alive: when the only remaining references to a referent are weak references, garbage collection is free to destroy the referent and reuse its memory for something else. However, until the object is actually destroyed the weak reference may return the object even if there are no strong references to it.

Variant wrap(value: Variant, min: Variant, max: Variant) 🔗

Wraps the Variant value between min and max. min is inclusive while max is exclusive. This can be used for creating loop-like behavior or infinite surfaces.

Variant types int and float are supported. If any of the arguments is float, this function returns a float, otherwise it returns an int.

float wrapf(value: float, min: float, max: float) 🔗

Wraps the float value between min and max. min is inclusive while max is exclusive. This can be used for creating loop-like behavior or infinite surfaces.

Note: If min is 0, this is equivalent to fposmod(), so prefer using that instead. wrapf() is more flexible than using the fposmod() approach by giving the user control over the minimum value.

int wrapi(value: int, min: int, max: int) 🔗

Wraps the integer value between min and max. min is inclusive while max is exclusive. This can be used for creating loop-like behavior or infinite surfaces.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Node — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/classes/class_node.html

**Contents:**
- Node
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Constants
- Property Descriptions
- Method Descriptions

Inherited By: AnimationMixer, AudioStreamPlayer, CanvasItem, CanvasLayer, EditorFileSystem, EditorPlugin, EditorResourcePreview, HTTPRequest, InstancePlaceholder, MissingNode, MultiplayerSpawner, MultiplayerSynchronizer, NavigationAgent2D, NavigationAgent3D, Node3D, ResourcePreloader, ShaderGlobalsOverride, StatusIndicator, Timer, Viewport, WorldEnvironment

Base class for all scene objects.

Nodes are Godot's building blocks. They can be assigned as the child of another node, resulting in a tree arrangement. A given node can contain any number of nodes as children with the requirement that all siblings (direct children of a node) should have unique names.

A tree of nodes is called a scene. Scenes can be saved to the disk and then instantiated into other scenes. This allows for very high flexibility in the architecture and data model of Godot projects.

Scene tree: The SceneTree contains the active tree of nodes. When a node is added to the scene tree, it receives the NOTIFICATION_ENTER_TREE notification and its _enter_tree() callback is triggered. Child nodes are always added after their parent node, i.e. the _enter_tree() callback of a parent node will be triggered before its child's.

Once all nodes have been added in the scene tree, they receive the NOTIFICATION_READY notification and their respective _ready() callbacks are triggered. For groups of nodes, the _ready() callback is called in reverse order, starting with the children and moving up to the parent nodes.

This means that when adding a node to the scene tree, the following order will be used for the callbacks: _enter_tree() of the parent, _enter_tree() of the children, _ready() of the children and finally _ready() of the parent (recursively for the entire scene tree).

Processing: Nodes can override the "process" state, so that they receive a callback on each frame requesting them to process (do something). Normal processing (callback _process(), toggled with set_process()) happens as fast as possible and is dependent on the frame rate, so the processing time delta (in seconds) is passed as an argument. Physics processing (callback _physics_process(), toggled with set_physics_process()) happens a fixed number of times per second (60 by default) and is useful for code related to the physics engine.

Nodes can also process input events. When present, the _input() function will be called for each input that the program receives. In many cases, this can be overkill (unless used for simple projects), and the _unhandled_input() function might be preferred; it is called when the input event was not handled by anyone else (typically, GUI Control nodes), ensuring that the node only receives the events that were meant for it.

To keep track of the scene hierarchy (especially when instantiating scenes into other scenes), an "owner" can be set for the node with the owner property. This keeps track of who instantiated what. This is mostly useful when writing editors and tools, though.

Finally, when a node is freed with Object.free() or queue_free(), it will also free all its children.

Groups: Nodes can be added to as many groups as you want to be easy to manage, you could create groups like "enemies" or "collectables" for example, depending on your game. See add_to_group(), is_in_group() and remove_from_group(). You can then retrieve all nodes in these groups, iterate them and even call methods on groups via the methods on SceneTree.

Networking with nodes: After connecting to a server (or making one, see ENetMultiplayerPeer), it is possible to use the built-in RPC (remote procedure call) system to communicate over the network. By calling rpc() with a method name, it will be called locally and in all connected peers (peers = clients and the server that accepts connections). To identify which node receives the RPC call, Godot will use its NodePath (make sure node names are the same on all peers). Also, take a look at the high-level networking tutorial and corresponding demos.

Note: The script property is part of the Object class, not Node. It isn't exposed like most properties but does have a setter and getter (see Object.set_script() and Object.get_script()).

PhysicsInterpolationMode

physics_interpolation_mode

process_physics_priority

process_thread_group_order

BitField[ProcessThreadMessages]

process_thread_messages

_enter_tree() virtual

_get_accessibility_configuration_warnings() virtual const

_get_configuration_warnings() virtual const

_get_focused_accessibility_element() virtual const

_input(event: InputEvent) virtual

_physics_process(delta: float) virtual

_process(delta: float) virtual

_shortcut_input(event: InputEvent) virtual

_unhandled_input(event: InputEvent) virtual

_unhandled_key_input(event: InputEvent) virtual

add_child(node: Node, force_readable_name: bool = false, internal: InternalMode = 0)

add_sibling(sibling: Node, force_readable_name: bool = false)

add_to_group(group: StringName, persistent: bool = false)

atr(message: String, context: StringName = "") const

atr_n(message: String, plural_message: StringName, n: int, context: StringName = "") const

call_deferred_thread_group(method: StringName, ...) vararg

call_thread_safe(method: StringName, ...) vararg

can_auto_translate() const

duplicate(flags: int = 15) const

find_child(pattern: String, recursive: bool = true, owned: bool = true) const

find_children(pattern: String, type: String = "", recursive: bool = true, owned: bool = true) const

find_parent(pattern: String) const

get_accessibility_element() const

get_child(idx: int, include_internal: bool = false) const

get_child_count(include_internal: bool = false) const

get_children(include_internal: bool = false) const

get_index(include_internal: bool = false) const

get_last_exclusive_window() const

get_multiplayer_authority() const

get_node(path: NodePath) const

get_node_and_resource(path: NodePath)

get_node_or_null(path: NodePath) const

get_node_rpc_config() const

get_orphan_node_ids() static

get_path_to(node: Node, use_unique_path: bool = false) const

get_physics_process_delta_time() const

get_process_delta_time() const

get_scene_instance_load_placeholder() const

get_tree_string_pretty()

has_node(path: NodePath) const

has_node_and_resource(path: NodePath) const

is_ancestor_of(node: Node) const

is_displayed_folded() const

is_editable_instance(node: Node) const

is_greater_than(node: Node) const

is_in_group(group: StringName) const

is_inside_tree() const

is_multiplayer_authority() const

is_node_ready() const

is_part_of_edited_scene() const

is_physics_interpolated() const

is_physics_interpolated_and_enabled() const

is_physics_processing() const

is_physics_processing_internal() const

is_processing() const

is_processing_input() const

is_processing_internal() const

is_processing_shortcut_input() const

is_processing_unhandled_input() const

is_processing_unhandled_key_input() const

move_child(child_node: Node, to_index: int)

notify_deferred_thread_group(what: int)

notify_thread_safe(what: int)

print_orphan_nodes() static

propagate_call(method: StringName, args: Array = [], parent_first: bool = false)

propagate_notification(what: int)

queue_accessibility_update()

remove_child(node: Node)

remove_from_group(group: StringName)

reparent(new_parent: Node, keep_global_transform: bool = true)

replace_by(node: Node, keep_groups: bool = false)

reset_physics_interpolation()

rpc(method: StringName, ...) vararg

rpc_config(method: StringName, config: Variant)

rpc_id(peer_id: int, method: StringName, ...) vararg

set_deferred_thread_group(property: StringName, value: Variant)

set_display_folded(fold: bool)

set_editable_instance(node: Node, is_editable: bool)

set_multiplayer_authority(id: int, recursive: bool = true)

set_physics_process(enable: bool)

set_physics_process_internal(enable: bool)

set_process(enable: bool)

set_process_input(enable: bool)

set_process_internal(enable: bool)

set_process_shortcut_input(enable: bool)

set_process_unhandled_input(enable: bool)

set_process_unhandled_key_input(enable: bool)

set_scene_instance_load_placeholder(load_placeholder: bool)

set_thread_safe(property: StringName, value: Variant)

set_translation_domain_inherited()

update_configuration_warnings()

child_entered_tree(node: Node) 🔗

Emitted when the child node enters the SceneTree, usually because this node entered the tree (see tree_entered), or add_child() has been called.

This signal is emitted after the child node's own NOTIFICATION_ENTER_TREE and tree_entered.

child_exiting_tree(node: Node) 🔗

Emitted when the child node is about to exit the SceneTree, usually because this node is exiting the tree (see tree_exiting), or because the child node is being removed or freed.

When this signal is received, the child node is still accessible inside the tree. This signal is emitted after the child node's own tree_exiting and NOTIFICATION_EXIT_TREE.

child_order_changed() 🔗

Emitted when the list of children is changed. This happens when child nodes are added, moved or removed.

editor_description_changed(node: Node) 🔗

Emitted when the node's editor description field changed.

editor_state_changed() 🔗

Emitted when an attribute of the node that is relevant to the editor is changed. Only emitted in the editor.

Emitted when the node is considered ready, after _ready() is called.

Emitted when the node's name is changed, if the node is inside the tree.

replacing_by(node: Node) 🔗

Emitted when this node is being replaced by the node, see replace_by().

This signal is emitted after node has been added as a child of the original parent node, but before all original child nodes have been reparented to node.

Emitted when the node enters the tree.

This signal is emitted after the related NOTIFICATION_ENTER_TREE notification.

Emitted after the node exits the tree and is no longer active.

This signal is emitted after the related NOTIFICATION_EXIT_TREE notification.

Emitted when the node is just about to exit the tree. The node is still valid. As such, this is the right place for de-initialization (or a "destructor", if you will).

This signal is emitted after the node's _exit_tree(), and before the related NOTIFICATION_EXIT_TREE.

ProcessMode PROCESS_MODE_INHERIT = 0

Inherits process_mode from the node's parent. This is the default for any newly created node.

ProcessMode PROCESS_MODE_PAUSABLE = 1

Stops processing when SceneTree.paused is true. This is the inverse of PROCESS_MODE_WHEN_PAUSED, and the default for the root node.

ProcessMode PROCESS_MODE_WHEN_PAUSED = 2

Process only when SceneTree.paused is true. This is the inverse of PROCESS_MODE_PAUSABLE.

ProcessMode PROCESS_MODE_ALWAYS = 3

Always process. Keeps processing, ignoring SceneTree.paused. This is the inverse of PROCESS_MODE_DISABLED.

ProcessMode PROCESS_MODE_DISABLED = 4

Never process. Completely disables processing, ignoring SceneTree.paused. This is the inverse of PROCESS_MODE_ALWAYS.

enum ProcessThreadGroup: 🔗

ProcessThreadGroup PROCESS_THREAD_GROUP_INHERIT = 0

Process this node based on the thread group mode of the first parent (or grandparent) node that has a thread group mode that is not inherit. See process_thread_group for more information.

ProcessThreadGroup PROCESS_THREAD_GROUP_MAIN_THREAD = 1

Process this node (and child nodes set to inherit) on the main thread. See process_thread_group for more information.

ProcessThreadGroup PROCESS_THREAD_GROUP_SUB_THREAD = 2

Process this node (and child nodes set to inherit) on a sub-thread. See process_thread_group for more information.

flags ProcessThreadMessages: 🔗

ProcessThreadMessages FLAG_PROCESS_THREAD_MESSAGES = 1

Allows this node to process threaded messages created with call_deferred_thread_group() right before _process() is called.

ProcessThreadMessages FLAG_PROCESS_THREAD_MESSAGES_PHYSICS = 2

Allows this node to process threaded messages created with call_deferred_thread_group() right before _physics_process() is called.

ProcessThreadMessages FLAG_PROCESS_THREAD_MESSAGES_ALL = 3

Allows this node to process threaded messages created with call_deferred_thread_group() right before either _process() or _physics_process() are called.

enum PhysicsInterpolationMode: 🔗

PhysicsInterpolationMode PHYSICS_INTERPOLATION_MODE_INHERIT = 0

Inherits physics_interpolation_mode from the node's parent. This is the default for any newly created node.

PhysicsInterpolationMode PHYSICS_INTERPOLATION_MODE_ON = 1

Enables physics interpolation for this node and for children set to PHYSICS_INTERPOLATION_MODE_INHERIT. This is the default for the root node.

PhysicsInterpolationMode PHYSICS_INTERPOLATION_MODE_OFF = 2

Disables physics interpolation for this node and for children set to PHYSICS_INTERPOLATION_MODE_INHERIT.

enum DuplicateFlags: 🔗

DuplicateFlags DUPLICATE_SIGNALS = 1

Duplicate the node's signal connections that are connected with the Object.CONNECT_PERSIST flag.

DuplicateFlags DUPLICATE_GROUPS = 2

Duplicate the node's groups.

DuplicateFlags DUPLICATE_SCRIPTS = 4

Duplicate the node's script (also overriding the duplicated children's scripts, if combined with DUPLICATE_USE_INSTANTIATION).

DuplicateFlags DUPLICATE_USE_INSTANTIATION = 8

Duplicate using PackedScene.instantiate(). If the node comes from a scene saved on disk, reuses PackedScene.instantiate() as the base for the duplicated node and its children.

InternalMode INTERNAL_MODE_DISABLED = 0

The node will not be internal.

InternalMode INTERNAL_MODE_FRONT = 1

The node will be placed at the beginning of the parent's children, before any non-internal sibling.

InternalMode INTERNAL_MODE_BACK = 2

The node will be placed at the end of the parent's children, after any non-internal sibling.

enum AutoTranslateMode: 🔗

AutoTranslateMode AUTO_TRANSLATE_MODE_INHERIT = 0

Inherits auto_translate_mode from the node's parent. This is the default for any newly created node.

AutoTranslateMode AUTO_TRANSLATE_MODE_ALWAYS = 1

Always automatically translate. This is the inverse of AUTO_TRANSLATE_MODE_DISABLED, and the default for the root node.

AutoTranslateMode AUTO_TRANSLATE_MODE_DISABLED = 2

Never automatically translate. This is the inverse of AUTO_TRANSLATE_MODE_ALWAYS.

String parsing for POT generation will be skipped for this node and children that are set to AUTO_TRANSLATE_MODE_INHERIT.

NOTIFICATION_ENTER_TREE = 10 🔗

Notification received when the node enters a SceneTree. See _enter_tree().

This notification is received before the related tree_entered signal.

NOTIFICATION_EXIT_TREE = 11 🔗

Notification received when the node is about to exit a SceneTree. See _exit_tree().

This notification is received after the related tree_exiting signal.

NOTIFICATION_MOVED_IN_PARENT = 12 🔗

Deprecated: This notification is no longer sent by the engine. Use NOTIFICATION_CHILD_ORDER_CHANGED instead.

NOTIFICATION_READY = 13 🔗

Notification received when the node is ready. See _ready().

NOTIFICATION_PAUSED = 14 🔗

Notification received when the node is paused. See process_mode.

NOTIFICATION_UNPAUSED = 15 🔗

Notification received when the node is unpaused. See process_mode.

NOTIFICATION_PHYSICS_PROCESS = 16 🔗

Notification received from the tree every physics frame when is_physics_processing() returns true. See _physics_process().

NOTIFICATION_PROCESS = 17 🔗

Notification received from the tree every rendered frame when is_processing() returns true. See _process().

NOTIFICATION_PARENTED = 18 🔗

Notification received when the node is set as a child of another node (see add_child() and add_sibling()).

Note: This does not mean that the node entered the SceneTree.

NOTIFICATION_UNPARENTED = 19 🔗

Notification received when the parent node calls remove_child() on this node.

Note: This does not mean that the node exited the SceneTree.

NOTIFICATION_SCENE_INSTANTIATED = 20 🔗

Notification received only by the newly instantiated scene root node, when PackedScene.instantiate() is completed.

NOTIFICATION_DRAG_BEGIN = 21 🔗

Notification received when a drag operation begins. All nodes receive this notification, not only the dragged one.

Can be triggered either by dragging a Control that provides drag data (see Control._get_drag_data()) or using Control.force_drag().

Use Viewport.gui_get_drag_data() to get the dragged data.

NOTIFICATION_DRAG_END = 22 🔗

Notification received when a drag operation ends.

Use Viewport.gui_is_drag_successful() to check if the drag succeeded.

NOTIFICATION_PATH_RENAMED = 23 🔗

Notification received when the node's name or one of its ancestors' name is changed. This notification is not received when the node is removed from the SceneTree.

NOTIFICATION_CHILD_ORDER_CHANGED = 24 🔗

Notification received when the list of children is changed. This happens when child nodes are added, moved or removed.

NOTIFICATION_INTERNAL_PROCESS = 25 🔗

Notification received from the tree every rendered frame when is_processing_internal() returns true.

NOTIFICATION_INTERNAL_PHYSICS_PROCESS = 26 🔗

Notification received from the tree every physics frame when is_physics_processing_internal() returns true.

NOTIFICATION_POST_ENTER_TREE = 27 🔗

Notification received when the node enters the tree, just before NOTIFICATION_READY may be received. Unlike the latter, it is sent every time the node enters tree, not just once.

NOTIFICATION_DISABLED = 28 🔗

Notification received when the node is disabled. See PROCESS_MODE_DISABLED.

NOTIFICATION_ENABLED = 29 🔗

Notification received when the node is enabled again after being disabled. See PROCESS_MODE_DISABLED.

NOTIFICATION_RESET_PHYSICS_INTERPOLATION = 2001 🔗

Notification received when reset_physics_interpolation() is called on the node or its ancestors.

NOTIFICATION_EDITOR_PRE_SAVE = 9001 🔗

Notification received right before the scene with the node is saved in the editor. This notification is only sent in the Godot editor and will not occur in exported projects.

NOTIFICATION_EDITOR_POST_SAVE = 9002 🔗

Notification received right after the scene with the node is saved in the editor. This notification is only sent in the Godot editor and will not occur in exported projects.

NOTIFICATION_WM_MOUSE_ENTER = 1002 🔗

Notification received when the mouse enters the window.

Implemented for embedded windows and on desktop and web platforms.

NOTIFICATION_WM_MOUSE_EXIT = 1003 🔗

Notification received when the mouse leaves the window.

Implemented for embedded windows and on desktop and web platforms.

NOTIFICATION_WM_WINDOW_FOCUS_IN = 1004 🔗

Notification received from the OS when the node's Window ancestor is focused. This may be a change of focus between two windows of the same engine instance, or from the OS desktop or a third-party application to a window of the game (in which case NOTIFICATION_APPLICATION_FOCUS_IN is also received).

A Window node receives this notification when it is focused.

NOTIFICATION_WM_WINDOW_FOCUS_OUT = 1005 🔗

Notification received from the OS when the node's Window ancestor is defocused. This may be a change of focus between two windows of the same engine instance, or from a window of the game to the OS desktop or a third-party application (in which case NOTIFICATION_APPLICATION_FOCUS_OUT is also received).

A Window node receives this notification when it is defocused.

NOTIFICATION_WM_CLOSE_REQUEST = 1006 🔗

Notification received from the OS when a close request is sent (e.g. closing the window with a "Close" button or Alt + F4).

Implemented on desktop platforms.

NOTIFICATION_WM_GO_BACK_REQUEST = 1007 🔗

Notification received from the OS when a go back request is sent (e.g. pressing the "Back" button on Android).

Implemented only on Android.

NOTIFICATION_WM_SIZE_CHANGED = 1008 🔗

Notification received when the window is resized.

Note: Only the resized Window node receives this notification, and it's not propagated to the child nodes.

NOTIFICATION_WM_DPI_CHANGE = 1009 🔗

Notification received from the OS when the screen's dots per inch (DPI) scale is changed. Only implemented on macOS.

NOTIFICATION_VP_MOUSE_ENTER = 1010 🔗

Notification received when the mouse cursor enters the Viewport's visible area, that is not occluded behind other Controls or Windows, provided its Viewport.gui_disable_input is false and regardless if it's currently focused or not.

NOTIFICATION_VP_MOUSE_EXIT = 1011 🔗

Notification received when the mouse cursor leaves the Viewport's visible area, that is not occluded behind other Controls or Windows, provided its Viewport.gui_disable_input is false and regardless if it's currently focused or not.

NOTIFICATION_WM_POSITION_CHANGED = 1012 🔗

Notification received when the window is moved.

NOTIFICATION_OS_MEMORY_WARNING = 2009 🔗

Notification received from the OS when the application is exceeding its allocated memory.

Implemented only on iOS.

NOTIFICATION_TRANSLATION_CHANGED = 2010 🔗

Notification received when translations may have changed. Can be triggered by the user changing the locale, changing auto_translate_mode or when the node enters the scene tree. Can be used to respond to language changes, for example to change the UI strings on the fly. Useful when working with the built-in translation support, like Object.tr().

Note: This notification is received alongside NOTIFICATION_ENTER_TREE, so if you are instantiating a scene, the child nodes will not be initialized yet. You can use it to setup translations for this node, child nodes created from script, or if you want to access child nodes added in the editor, make sure the node is ready using is_node_ready().

NOTIFICATION_WM_ABOUT = 2011 🔗

Notification received from the OS when a request for "About" information is sent.

Implemented only on macOS.

NOTIFICATION_CRASH = 2012 🔗

Notification received from Godot's crash handler when the engine is about to crash.

Implemented on desktop platforms, if the crash handler is enabled.

NOTIFICATION_OS_IME_UPDATE = 2013 🔗

Notification received from the OS when an update of the Input Method Engine occurs (e.g. change of IME cursor position or composition string).

Implemented only on macOS.

NOTIFICATION_APPLICATION_RESUMED = 2014 🔗

Notification received from the OS when the application is resumed.

Specific to the Android and iOS platforms.

NOTIFICATION_APPLICATION_PAUSED = 2015 🔗

Notification received from the OS when the application is paused.

Specific to the Android and iOS platforms.

Note: On iOS, you only have approximately 5 seconds to finish a task started by this signal. If you go over this allotment, iOS will kill the app instead of pausing it.

NOTIFICATION_APPLICATION_FOCUS_IN = 2016 🔗

Notification received from the OS when the application is focused, i.e. when changing the focus from the OS desktop or a thirdparty application to any open window of the Godot instance.

Implemented on desktop and mobile platforms.

NOTIFICATION_APPLICATION_FOCUS_OUT = 2017 🔗

Notification received from the OS when the application is defocused, i.e. when changing the focus from any open window of the Godot instance to the OS desktop or a thirdparty application.

Implemented on desktop and mobile platforms.

NOTIFICATION_TEXT_SERVER_CHANGED = 2018 🔗

Notification received when the TextServer is changed.

NOTIFICATION_ACCESSIBILITY_UPDATE = 3000 🔗

Notification received when an accessibility information update is required.

NOTIFICATION_ACCESSIBILITY_INVALIDATE = 3001 🔗

Notification received when accessibility elements are invalidated. All node accessibility elements are automatically deleted after receiving this message, therefore all existing references to such elements should be discarded.

AutoTranslateMode auto_translate_mode = 0 🔗

void set_auto_translate_mode(value: AutoTranslateMode)

AutoTranslateMode get_auto_translate_mode()

Defines if any text should automatically change to its translated version depending on the current locale (for nodes such as Label, RichTextLabel, Window, etc.). Also decides if the node's strings should be parsed for POT generation.

Note: For the root node, auto translate mode can also be set via ProjectSettings.internationalization/rendering/root_node_auto_translate.

String editor_description = "" 🔗

void set_editor_description(value: String)

String get_editor_description()

An optional description to the node. It will be displayed as a tooltip when hovering over the node in the editor's Scene dock.

MultiplayerAPI multiplayer 🔗

MultiplayerAPI get_multiplayer()

The MultiplayerAPI instance associated with this node. See SceneTree.get_multiplayer().

Note: Renaming the node, or moving it in the tree, will not move the MultiplayerAPI to the new path, you will have to update this manually.

void set_name(value: StringName)

StringName get_name()

The name of the node. This name must be unique among the siblings (other child nodes from the same parent). When set to an existing sibling's name, the node is automatically renamed.

Note: When changing the name, the following characters will be replaced with an underscore: (. : @ / " %). In particular, the @ character is reserved for auto-generated names. See also String.validate_node_name().

void set_owner(value: Node)

The owner of this node. The owner must be an ancestor of this node. When packing the owner node in a PackedScene, all the nodes it owns are also saved with it. See also unique_name_in_owner.

Note: In the editor, nodes not owned by the scene root are usually not displayed in the Scene dock, and will not be saved. To prevent this, remember to set the owner after calling add_child().

PhysicsInterpolationMode physics_interpolation_mode = 0 🔗

void set_physics_interpolation_mode(value: PhysicsInterpolationMode)

PhysicsInterpolationMode get_physics_interpolation_mode()

The physics interpolation mode to use for this node. Only effective if ProjectSettings.physics/common/physics_interpolation or SceneTree.physics_interpolation is true.

By default, nodes inherit the physics interpolation mode from their parent. This property can enable or disable physics interpolation individually for each node, regardless of their parents' physics interpolation mode.

Note: Some node types like VehicleWheel3D have physics interpolation disabled by default, as they rely on their own custom solution.

Note: When teleporting a node to a distant position, it's recommended to temporarily disable interpolation with reset_physics_interpolation() after moving the node. This avoids creating a visual streak between the old and new positions.

ProcessMode process_mode = 0 🔗

void set_process_mode(value: ProcessMode)

ProcessMode get_process_mode()

The node's processing behavior. To check if the node can process in its current mode, use can_process().

int process_physics_priority = 0 🔗

void set_physics_process_priority(value: int)

int get_physics_process_priority()

Similar to process_priority but for NOTIFICATION_PHYSICS_PROCESS, _physics_process(), or NOTIFICATION_INTERNAL_PHYSICS_PROCESS.

int process_priority = 0 🔗

void set_process_priority(value: int)

int get_process_priority()

The node's execution order of the process callbacks (_process(), NOTIFICATION_PROCESS, and NOTIFICATION_INTERNAL_PROCESS). Nodes whose priority value is lower call their process callbacks first, regardless of tree order.

ProcessThreadGroup process_thread_group = 0 🔗

void set_process_thread_group(value: ProcessThreadGroup)

ProcessThreadGroup get_process_thread_group()

Set the process thread group for this node (basically, whether it receives NOTIFICATION_PROCESS, NOTIFICATION_PHYSICS_PROCESS, _process() or _physics_process() (and the internal versions) on the main thread or in a sub-thread.

By default, the thread group is PROCESS_THREAD_GROUP_INHERIT, which means that this node belongs to the same thread group as the parent node. The thread groups means that nodes in a specific thread group will process together, separate to other thread groups (depending on process_thread_group_order). If the value is set is PROCESS_THREAD_GROUP_SUB_THREAD, this thread group will occur on a sub thread (not the main thread), otherwise if set to PROCESS_THREAD_GROUP_MAIN_THREAD it will process on the main thread. If there is not a parent or grandparent node set to something other than inherit, the node will belong to the default thread group. This default group will process on the main thread and its group order is 0.

During processing in a sub-thread, accessing most functions in nodes outside the thread group is forbidden (and it will result in an error in debug mode). Use Object.call_deferred(), call_thread_safe(), call_deferred_thread_group() and the likes in order to communicate from the thread groups to the main thread (or to other thread groups).

To better understand process thread groups, the idea is that any node set to any other value than PROCESS_THREAD_GROUP_INHERIT will include any child (and grandchild) nodes set to inherit into its process thread group. This means that the processing of all the nodes in the group will happen together, at the same time as the node including them.

int process_thread_group_order 🔗

void set_process_thread_group_order(value: int)

int get_process_thread_group_order()

Change the process thread group order. Groups with a lesser order will process before groups with a greater order. This is useful when a large amount of nodes process in sub thread and, afterwards, another group wants to collect their result in the main thread, as an example.

BitField[ProcessThreadMessages] process_thread_messages 🔗

void set_process_thread_messages(value: BitField[ProcessThreadMessages])

BitField[ProcessThreadMessages] get_process_thread_messages()

Set whether the current thread group will process messages (calls to call_deferred_thread_group() on threads), and whether it wants to receive them during regular process or physics process callbacks.

String scene_file_path 🔗

void set_scene_file_path(value: String)

String get_scene_file_path()

The original scene's file path, if the node has been instantiated from a PackedScene file. Only scene root nodes contains this.

bool unique_name_in_owner = false 🔗

void set_unique_name_in_owner(value: bool)

bool is_unique_name_in_owner()

If true, the node can be accessed from any node sharing the same owner or from the owner itself, with special %Name syntax in get_node().

Note: If another node with the same owner shares the same name as this node, the other node will no longer be accessible as unique.

void _enter_tree() virtual 🔗

Called when the node enters the SceneTree (e.g. upon instantiating, scene changing, or after calling add_child() in a script). If the node has children, its _enter_tree() callback will be called first, and then that of the children.

Corresponds to the NOTIFICATION_ENTER_TREE notification in Object._notification().

void _exit_tree() virtual 🔗

Called when the node is about to leave the SceneTree (e.g. upon freeing, scene changing, or after calling remove_child() in a script). If the node has children, its _exit_tree() callback will be called last, after all its children have left the tree.

Corresponds to the NOTIFICATION_EXIT_TREE notification in Object._notification() and signal tree_exiting. To get notified when the node has already left the active tree, connect to the tree_exited.

PackedStringArray _get_accessibility_configuration_warnings() virtual const 🔗

The elements in the array returned from this method are displayed as warnings in the Scene dock if the script that overrides it is a tool script, and accessibility warnings are enabled in the editor settings.

Returning an empty array produces no warnings.

PackedStringArray _get_configuration_warnings() virtual const 🔗

The elements in the array returned from this method are displayed as warnings in the Scene dock if the script that overrides it is a tool script.

Returning an empty array produces no warnings.

Call update_configuration_warnings() when the warnings need to be updated for this node.

RID _get_focused_accessibility_element() virtual const 🔗

Called during accessibility information updates to determine the currently focused sub-element, should return a sub-element RID or the value returned by get_accessibility_element().

void _input(event: InputEvent) virtual 🔗

Called when there is an input event. The input event propagates up through the node tree until a node consumes it.

It is only called if input processing is enabled, which is done automatically if this method is overridden, and can be toggled with set_process_input().

To consume the input event and stop it propagating further to other nodes, Viewport.set_input_as_handled() can be called.

For gameplay input, _unhandled_input() and _unhandled_key_input() are usually a better fit as they allow the GUI to intercept the events first.

Note: This method is only called if the node is present in the scene tree (i.e. if it's not an orphan).

void _physics_process(delta: float) virtual 🔗

Called once on each physics tick, and allows Nodes to synchronize their logic with physics ticks. delta is the logical time between physics ticks in seconds and is equal to Engine.time_scale / Engine.physics_ticks_per_second.

It is only called if physics processing is enabled for this Node, which is done automatically if this method is overridden, and can be toggled with set_physics_process().

Processing happens in order of process_physics_priority, lower priority values are called first. Nodes with the same priority are processed in tree order, or top to bottom as seen in the editor (also known as pre-order traversal).

Corresponds to the NOTIFICATION_PHYSICS_PROCESS notification in Object._notification().

Note: This method is only called if the node is present in the scene tree (i.e. if it's not an orphan).

Note: Accumulated delta may diverge from real world seconds.

void _process(delta: float) virtual 🔗

Called on each idle frame, prior to rendering, and after physics ticks have been processed. delta is the time between frames in seconds.

It is only called if processing is enabled for this Node, which is done automatically if this method is overridden, and can be toggled with set_process().

Processing happens in order of process_priority, lower priority values are called first. Nodes with the same priority are processed in tree order, or top to bottom as seen in the editor (also known as pre-order traversal).

Corresponds to the NOTIFICATION_PROCESS notification in Object._notification().

Note: This method is only called if the node is present in the scene tree (i.e. if it's not an orphan).

Note: When the engine is struggling and the frame rate is lowered, delta will increase. When delta is increased, it's capped at a maximum of Engine.time_scale * Engine.max_physics_steps_per_frame / Engine.physics_ticks_per_second. As a result, accumulated delta may not represent real world time.

Note: When --fixed-fps is enabled or the engine is running in Movie Maker mode (see MovieWriter), process delta will always be the same for every frame, regardless of how much time the frame took to render.

Note: Frame delta may be post-processed by OS.delta_smoothing if this is enabled for the project.

void _ready() virtual 🔗

Called when the node is "ready", i.e. when both the node and its children have entered the scene tree. If the node has children, their _ready() callbacks get triggered first, and the parent node will receive the ready notification afterwards.

Corresponds to the NOTIFICATION_READY notification in Object._notification(). See also the @onready annotation for variables.

Usually used for initialization. For even earlier initialization, Object._init() may be used. See also _enter_tree().

Note: This method may be called only once for each node. After removing a node from the scene tree and adding it again, _ready() will not be called a second time. This can be bypassed by requesting another call with request_ready(), which may be called anywhere before adding the node again.

void _shortcut_input(event: InputEvent) virtual 🔗

Called when an InputEventKey, InputEventShortcut, or InputEventJoypadButton hasn't been consumed by _input() or any GUI Control item. It is called before _unhandled_key_input() and _unhandled_input(). The input event propagates up through the node tree until a node consumes it.

It is only called if shortcut processing is enabled, which is done automatically if this method is overridden, and can be toggled with set_process_shortcut_input().

To consume the input event and stop it propagating further to other nodes, Viewport.set_input_as_handled() can be called.

This method can be used to handle shortcuts. For generic GUI events, use _input() instead. Gameplay events should usually be handled with either _unhandled_input() or _unhandled_key_input().

Note: This method is only called if the node is present in the scene tree (i.e. if it's not orphan).

void _unhandled_input(event: InputEvent) virtual 🔗

Called when an InputEvent hasn't been consumed by _input() or any GUI Control item. It is called after _shortcut_input() and after _unhandled_key_input(). The input event propagates up through the node tree until a node consumes it.

It is only called if unhandled input processing is enabled, which is done automatically if this method is overridden, and can be toggled with set_process_unhandled_input().

To consume the input event and stop it propagating further to other nodes, Viewport.set_input_as_handled() can be called.

For gameplay input, this method is usually a better fit than _input(), as GUI events need a higher priority. For keyboard shortcuts, consider using _shortcut_input() instead, as it is called before this method. Finally, to handle keyboard events, consider using _unhandled_key_input() for performance reasons.

Note: This method is only called if the node is present in the scene tree (i.e. if it's not an orphan).

void _unhandled_key_input(event: InputEvent) virtual 🔗

Called when an InputEventKey hasn't been consumed by _input() or any GUI Control item. It is called after _shortcut_input() but before _unhandled_input(). The input event propagates up through the node tree until a node consumes it.

It is only called if unhandled key input processing is enabled, which is done automatically if this method is overridden, and can be toggled with set_process_unhandled_key_input().

To consume the input event and stop it propagating further to other nodes, Viewport.set_input_as_handled() can be called.

This method can be used to handle Unicode character input with Alt, Alt + Ctrl, and Alt + Shift modifiers, after shortcuts were handled.

For gameplay input, this and _unhandled_input() are usually a better fit than _input(), as GUI events should be handled first. This method also performs better than _unhandled_input(), since unrelated events such as InputEventMouseMotion are automatically filtered. For shortcuts, consider using _shortcut_input() instead.

Note: This method is only called if the node is present in the scene tree (i.e. if it's not an orphan).

void add_child(node: Node, force_readable_name: bool = false, internal: InternalMode = 0) 🔗

Adds a child node. Nodes can have any number of children, but every child must have a unique name. Child nodes are automatically deleted when the parent node is deleted, so an entire scene can be removed by deleting its topmost node.

If force_readable_name is true, improves the readability of the added node. If not named, the node is renamed to its type, and if it shares name with a sibling, a number is suffixed more appropriately. This operation is very slow. As such, it is recommended leaving this to false, which assigns a dummy name featuring @ in both situations.

If internal is different than INTERNAL_MODE_DISABLED, the child will be added as internal node. These nodes are ignored by methods like get_children(), unless their parameter include_internal is true. It also prevents these nodes being duplicated with their parent. The intended usage is to hide the internal nodes from the user, so the user won't accidentally delete or modify them. Used by some GUI nodes, e.g. ColorPicker.

Note: If node already has a parent, this method will fail. Use remove_child() first to remove node from its current parent. For example:

If you need the child node to be added below a specific node in the list of children, use add_sibling() instead of this method.

Note: If you want a child to be persisted to a PackedScene, you must set owner in addition to calling add_child(). This is typically relevant for tool scripts and editor plugins. If add_child() is called without setting owner, the newly added Node will not be visible in the scene tree, though it will be visible in the 2D/3D view.

void add_sibling(sibling: Node, force_readable_name: bool = false) 🔗

Adds a sibling node to this node's parent, and moves the added sibling right below this node.

If force_readable_name is true, improves the readability of the added sibling. If not named, the sibling is renamed to its type, and if it shares name with a sibling, a number is suffixed more appropriately. This operation is very slow. As such, it is recommended leaving this to false, which assigns a dummy name featuring @ in both situations.

Use add_child() instead of this method if you don't need the child node to be added below a specific node in the list of children.

Note: If this node is internal, the added sibling will be internal too (see add_child()'s internal parameter).

void add_to_group(group: StringName, persistent: bool = false) 🔗

Adds the node to the group. Groups can be helpful to organize a subset of nodes, for example "enemies" or "collectables". See notes in the description, and the group methods in SceneTree.

If persistent is true, the group will be stored when saved inside a PackedScene. All groups created and displayed in the Node dock are persistent.

Note: To improve performance, the order of group names is not guaranteed and may vary between project runs. Therefore, do not rely on the group order.

Note: SceneTree's group methods will not work on this node if not inside the tree (see is_inside_tree()).

String atr(message: String, context: StringName = "") const 🔗

Translates a message, using the translation catalogs configured in the Project Settings. Further context can be specified to help with the translation. Note that most Control nodes automatically translate their strings, so this method is mostly useful for formatted strings or custom drawn text.

This method works the same as Object.tr(), with the addition of respecting the auto_translate_mode state.

If Object.can_translate_messages() is false, or no translation is available, this method returns the message without changes. See Object.set_message_translation().

For detailed examples, see Internationalizing games.

String atr_n(message: String, plural_message: StringName, n: int, context: StringName = "") const 🔗

Translates a message or plural_message, using the translation catalogs configured in the Project Settings. Further context can be specified to help with the translation.

This method works the same as Object.tr_n(), with the addition of respecting the auto_translate_mode state.

If Object.can_translate_messages() is false, or no translation is available, this method returns message or plural_message, without changes. See Object.set_message_translation().

The n is the number, or amount, of the message's subject. It is used by the translation system to fetch the correct plural form for the current language.

For detailed examples, see Localization using gettext.

Note: Negative and float numbers may not properly apply to some countable subjects. It's recommended to handle these cases with atr().

Variant call_deferred_thread_group(method: StringName, ...) vararg 🔗

This function is similar to Object.call_deferred() except that the call will take place when the node thread group is processed. If the node thread group processes in sub-threads, then the call will be done on that thread, right before NOTIFICATION_PROCESS or NOTIFICATION_PHYSICS_PROCESS, the _process() or _physics_process() or their internal versions are called.

Variant call_thread_safe(method: StringName, ...) vararg 🔗

This function ensures that the calling of this function will succeed, no matter whether it's being done from a thread or not. If called from a thread that is not allowed to call the function, the call will become deferred. Otherwise, the call will go through directly.

bool can_auto_translate() const 🔗

Returns true if this node can automatically translate messages depending on the current locale. See auto_translate_mode, atr(), and atr_n().

bool can_process() const 🔗

Returns true if the node can receive processing notifications and input callbacks (NOTIFICATION_PROCESS, _input(), etc.) from the SceneTree and Viewport. The returned value depends on process_mode:

If set to PROCESS_MODE_PAUSABLE, returns true when the game is processing, i.e. SceneTree.paused is false;

If set to PROCESS_MODE_WHEN_PAUSED, returns true when the game is paused, i.e. SceneTree.paused is true;

If set to PROCESS_MODE_ALWAYS, always returns true;

If set to PROCESS_MODE_DISABLED, always returns false;

If set to PROCESS_MODE_INHERIT, use the parent node's process_mode to determine the result.

If the node is not inside the tree, returns false no matter the value of process_mode.

Tween create_tween() 🔗

Creates a new Tween and binds it to this node.

This is the equivalent of doing:

The Tween will start automatically on the next process frame or physics frame (depending on TweenProcessMode). See Tween.bind_node() for more info on Tweens bound to nodes.

Note: The method can still be used when the node is not inside SceneTree. It can fail in an unlikely case of using a custom MainLoop.

Node duplicate(flags: int = 15) const 🔗

Duplicates the node, returning a new node with all of its properties, signals, groups, and children copied from the original. The behavior can be tweaked through the flags (see DuplicateFlags). Internal nodes are not duplicated.

Note: For nodes with a Script attached, if Object._init() has been defined with required parameters, the duplicated node will not have a Script.

Node find_child(pattern: String, recursive: bool = true, owned: bool = true) const 🔗

Finds the first descendant of this node whose name matches pattern, returning null if no match is found. The matching is done against node names, not their paths, through String.match(). As such, it is case-sensitive, "*" matches zero or more characters, and "?" matches any single character.

If recursive is false, only this node's direct children are checked. Nodes are checked in tree order, so this node's first direct child is checked first, then its own direct children, etc., before moving to the second direct child, and so on. Internal children are also included in the search (see internal parameter in add_child()).

If owned is true, only descendants with a valid owner node are checked.

Note: This method can be very slow. Consider storing a reference to the found node in a variable. Alternatively, use get_node() with unique names (see unique_name_in_owner).

Note: To find all descendant nodes matching a pattern or a class type, see find_children().

Array[Node] find_children(pattern: String, type: String = "", recursive: bool = true, owned: bool = true) const 🔗

Finds all descendants of this node whose names match pattern, returning an empty Array if no match is found. The matching is done against node names, not their paths, through String.match(). As such, it is case-sensitive, "*" matches zero or more characters, and "?" matches any single character.

If type is not empty, only ancestors inheriting from type are included (see Object.is_class()).

If recursive is false, only this node's direct children are checked. Nodes are checked in tree order, so this node's first direct child is checked first, then its own direct children, etc., before moving to the second direct child, and so on. Internal children are also included in the search (see internal parameter in add_child()).

If owned is true, only descendants with a valid owner node are checked.

Note: This method can be very slow. Consider storing references to the found nodes in a variable.

Note: To find a single descendant node matching a pattern, see find_child().

Node find_parent(pattern: String) const 🔗

Finds the first ancestor of this node whose name matches pattern, returning null if no match is found. The matching is done through String.match(). As such, it is case-sensitive, "*" matches zero or more characters, and "?" matches any single character. See also find_child() and find_children().

Note: As this method walks upwards in the scene tree, it can be slow in large, deeply nested nodes. Consider storing a reference to the found node in a variable. Alternatively, use get_node() with unique names (see unique_name_in_owner).

RID get_accessibility_element() const 🔗

Returns main accessibility element RID.

Note: This method should be called only during accessibility information updates (NOTIFICATION_ACCESSIBILITY_UPDATE).

Node get_child(idx: int, include_internal: bool = false) const 🔗

Fetches a child node by its index. Each child node has an index relative to its siblings (see get_index()). The first child is at index 0. Negative values can also be used to start from the end of the list. This method can be used in combination with get_child_count() to iterate over this node's children. If no child exists at the given index, this method returns null and an error is generated.

If include_internal is false, internal children are ignored (see add_child()'s internal parameter).

Note: To fetch a node by NodePath, use get_node().

int get_child_count(include_internal: bool = false) const 🔗

Returns the number of children of this node.

If include_internal is false, internal children are not counted (see add_child()'s internal parameter).

Array[Node] get_children(include_internal: bool = false) const 🔗

Returns all children of this node inside an Array.

If include_internal is false, excludes internal children from the returned array (see add_child()'s internal parameter).

Array[StringName] get_groups() const 🔗

Returns an Array of group names that the node has been added to.

Note: To improve performance, the order of group names is not guaranteed and may vary between project runs. Therefore, do not rely on the group order.

Note: This method may also return some group names starting with an underscore (_). These are internally used by the engine. To avoid conflicts, do not use custom groups starting with underscores. To exclude internal groups, see the following code snippet:

int get_index(include_internal: bool = false) const 🔗

Returns this node's order among its siblings. The first node's index is 0. See also get_child().

If include_internal is false, returns the index ignoring internal children. The first, non-internal child will have an index of 0 (see add_child()'s internal parameter).

Window get_last_exclusive_window() const 🔗

Returns the Window that contains this node, or the last exclusive child in a chain of windows starting with the one that contains this node.

int get_multiplayer_authority() const 🔗

Returns the peer ID of the multiplayer authority for this node. See set_multiplayer_authority().

Node get_node(path: NodePath) const 🔗

Fetches a node. The NodePath can either be a relative path (from this node), or an absolute path (from the SceneTree.root) to a node. If path does not point to a valid node, generates an error and returns null. Attempts to access methods on the return value will result in an "Attempt to call <method> on a null instance." error.

Note: Fetching by absolute path only works when the node is inside the scene tree (see is_inside_tree()).

Example: Assume this method is called from the Character node, inside the following tree:

The following calls will return a valid node:

Array get_node_and_resource(path: NodePath) 🔗

Fetches a node and its most nested resource as specified by the NodePath's subname. Returns an Array of size 3 where:

Element 0 is the Node, or null if not found;

Element 1 is the subname's last nested Resource, or null if not found;

Element 2 is the remaining NodePath, referring to an existing, non-Resource property (see Object.get_indexed()).

Example: Assume that the child's Sprite2D.texture has been assigned an AtlasTexture:

Node get_node_or_null(path: NodePath) const 🔗

Fetches a node by NodePath. Similar to get_node(), but does not generate an error if path does not point to a valid node.

Variant get_node_rpc_config() const 🔗

Returns a Dictionary mapping method names to their RPC configuration defined for this node using rpc_config().

Note: This method only returns the RPC configuration assigned via rpc_config(). See Script.get_rpc_config() to retrieve the RPCs defined by the Script.

Array[int] get_orphan_node_ids() static 🔗

Returns object IDs of all orphan nodes (nodes outside the SceneTree). Used for debugging.

Note: get_orphan_node_ids() only works in debug builds. When called in a project exported in release mode, get_orphan_node_ids() will return an empty array.

Node get_parent() const 🔗

Returns this node's parent node, or null if the node doesn't have a parent.

NodePath get_path() const 🔗

Returns the node's absolute path, relative to the SceneTree.root. If the node is not inside the scene tree, this method fails and returns an empty NodePath.

NodePath get_path_to(node: Node, use_unique_path: bool = false) const 🔗

Returns the relative NodePath from this node to the specified node. Both nodes must be in the same SceneTree or scene hierarchy, otherwise this method fails and returns an empty NodePath.

If use_unique_path is true, returns the shortest path accounting for this node's unique name (see unique_name_in_owner).

Note: If you get a relative path which starts from a unique node, the path may be longer than a normal relative path, due to the addition of the unique node's name.

float get_physics_process_delta_time() const 🔗

Returns the time elapsed (in seconds) since the last physics callback. This value is identical to _physics_process()'s delta parameter, and is often consistent at run-time, unless Engine.physics_ticks_per_second is changed. See also NOTIFICATION_PHYSICS_PROCESS.

Note: The returned value will be larger than expected if running at a framerate lower than Engine.physics_ticks_per_second / Engine.max_physics_steps_per_frame FPS. This is done to avoid "spiral of death" scenarios where performance would plummet due to an ever-increasing number of physics steps per frame. This behavior affects both _process() and _physics_process(). As a result, avoid using delta for time measurements in real-world seconds. Use the Time singleton's methods for this purpose instead, such as Time.get_ticks_usec().

float get_process_delta_time() const 🔗

Returns the time elapsed (in seconds) since the last process callback. This value is identical to _process()'s delta parameter, and may vary from frame to frame. See also NOTIFICATION_PROCESS.

Note: The returned value will be larger than expected if running at a framerate lower than Engine.physics_ticks_per_second / Engine.max_physics_steps_per_frame FPS. This is done to avoid "spiral of death" scenarios where performance would plummet due to an ever-increasing number of physics steps per frame. This behavior affects both _process() and _physics_process(). As a result, avoid using delta for time measurements in real-world seconds. Use the Time singleton's methods for this purpose instead, such as Time.get_ticks_usec().

bool get_scene_instance_load_placeholder() const 🔗

Returns true if this node is an instance load placeholder. See InstancePlaceholder and set_scene_instance_load_placeholder().

SceneTree get_tree() const 🔗

Returns the SceneTree that contains this node. If this node is not inside the tree, generates an error and returns null. See also is_inside_tree().

String get_tree_string() 🔗

Returns the tree as a String. Used mainly for debugging purposes. This version displays the path relative to the current node, and is good for copy/pasting into the get_node() function. It also can be used in game UI/UX.

May print, for example:

String get_tree_string_pretty() 🔗

Similar to get_tree_string(), this returns the tree as a String. This version displays a more graphical representation similar to what is displayed in the Scene Dock. It is useful for inspecting larger trees.

May print, for example:

Viewport get_viewport() const 🔗

Returns the node's closest Viewport ancestor, if the node is inside the tree. Otherwise, returns null.

Window get_window() const 🔗

Returns the Window that contains this node. If the node is in the main window, this is equivalent to getting the root node (get_tree().get_root()).

bool has_node(path: NodePath) const 🔗

Returns true if the path points to a valid node. See also get_node().

bool has_node_and_resource(path: NodePath) const 🔗

Returns true if path points to a valid node and its subnames point to a valid Resource, e.g. Area2D/CollisionShape2D:shape. Properties that are not Resource types (such as nodes or other Variant types) are not considered. See also get_node_and_resource().

bool is_ancestor_of(node: Node) const 🔗

Returns true if the given node is a direct or indirect child of this node.

bool is_displayed_folded() const 🔗

Returns true if the node is folded (collapsed) in the Scene dock. This method is intended to be used in editor plugins and tools. See also set_display_folded().

bool is_editable_instance(node: Node) const 🔗

Returns true if node has editable children enabled relative to this node. This method is intended to be used in editor plugins and tools. See also set_editable_instance().

bool is_greater_than(node: Node) const 🔗

Returns true if the given node occurs later in the scene hierarchy than this node. A node occurring later is usually processed last.

bool is_in_group(group: StringName) const 🔗

Returns true if this node has been added to the given group. See add_to_group() and remove_from_group(). See also notes in the description, and the SceneTree's group methods.

bool is_inside_tree() const 🔗

Returns true if this node is currently inside a SceneTree. See also get_tree().

bool is_multiplayer_authority() const 🔗

Returns true if the local system is the multiplayer authority of this node.

bool is_node_ready() const 🔗

Returns true if the node is ready, i.e. it's inside scene tree and all its children are initialized.

request_ready() resets it back to false.

bool is_part_of_edited_scene() const 🔗

Returns true if the node is part of the scene currently opened in the editor.

bool is_physics_interpolated() const 🔗

Returns true if physics interpolation is enabled for this node (see physics_interpolation_mode).

Note: Interpolation will only be active if both the flag is set and physics interpolation is enabled within the SceneTree. This can be tested using is_physics_interpolated_and_enabled().

bool is_physics_interpolated_and_enabled() const 🔗

Returns true if physics interpolation is enabled (see physics_interpolation_mode) and enabled in the SceneTree.

This is a convenience version of is_physics_interpolated() that also checks whether physics interpolation is enabled globally.

See SceneTree.physics_interpolation and ProjectSettings.physics/common/physics_interpolation.

bool is_physics_processing() const 🔗

Returns true if physics processing is enabled (see set_physics_process()).

bool is_physics_processing_internal() const 🔗

Returns true if internal physics processing is enabled (see set_physics_process_internal()).

bool is_processing() const 🔗

Returns true if processing is enabled (see set_process()).

bool is_processing_input() const 🔗

Returns true if the node is processing input (see set_process_input()).

bool is_processing_internal() const 🔗

Returns true if internal processing is enabled (see set_process_internal()).

bool is_processing_shortcut_input() const 🔗

Returns true if the node is processing shortcuts (see set_process_shortcut_input()).

bool is_processing_unhandled_input() const 🔗

Returns true if the node is processing unhandled input (see set_process_unhandled_input()).

bool is_processing_unhandled_key_input() const 🔗

Returns true if the node is processing unhandled key input (see set_process_unhandled_key_input()).

void move_child(child_node: Node, to_index: int) 🔗

Moves child_node to the given index. A node's index is the order among its siblings. If to_index is negative, the index is counted from the end of the list. See also get_child() and get_index().

Note: The processing order of several engine callbacks (_ready(), _process(), etc.) and notifications sent through propagate_notification() is affected by tree order. CanvasItem nodes are also rendered in tree order. See also process_priority.

void notify_deferred_thread_group(what: int) 🔗

Similar to call_deferred_thread_group(), but for notifications.

void notify_thread_safe(what: int) 🔗

Similar to call_thread_safe(), but for notifications.

void print_orphan_nodes() static 🔗

Prints all orphan nodes (nodes outside the SceneTree). Useful for debugging.

Note: This method only works in debug builds. Does nothing in a project exported in release mode.

Prints the node and its children to the console, recursively. The node does not have to be inside the tree. This method outputs NodePaths relative to this node, and is good for copy/pasting into get_node(). See also print_tree_pretty().

May print, for example:

void print_tree_pretty() 🔗

Prints the node and its children to the console, recursively. The node does not have to be inside the tree. Similar to print_tree(), but the graphical representation looks like what is displayed in the editor's Scene dock. It is useful for inspecting larger trees.

May print, for example:

void propagate_call(method: StringName, args: Array = [], parent_first: bool = false) 🔗

Calls the given method name, passing args as arguments, on this node and all of its children, recursively.

If parent_first is true, the method is called on this node first, then on all of its children. If false, the children's methods are called first.

void propagate_notification(what: int) 🔗

Calls Object.notification() with what on this node and all of its children, recursively.

void queue_accessibility_update() 🔗

Queues an accessibility information update for this node.

Queues this node to be deleted at the end of the current frame. When deleted, all of its children are deleted as well, and all references to the node and its children become invalid.

Unlike with Object.free(), the node is not deleted instantly, and it can still be accessed before deletion. It is also safe to call queue_free() multiple times. Use Object.is_queued_for_deletion() to check if the node will be deleted at the end of the frame.

Note: The node will only be freed after all other deferred calls are finished. Using this method is not always the same as calling Object.free() through Object.call_deferred().

void remove_child(node: Node) 🔗

Removes a child node. The node, along with its children, are not deleted. To delete a node, see queue_free().

Note: When this node is inside the tree, this method sets the owner of the removed node (or its descendants) to null, if their owner is no longer an ancestor (see is_ancestor_of()).

void remove_from_group(group: StringName) 🔗

Removes the node from the given group. Does nothing if the node is not in the group. See also notes in the description, and the SceneTree's group methods.

void reparent(new_parent: Node, keep_global_transform: bool = true) 🔗

Changes the parent of this Node to the new_parent. The node needs to already have a parent. The node's owner is preserved if its owner is still reachable from the new location (i.e., the node is still a descendant of the new parent after the operation).

If keep_global_transform is true, the node's global transform will be preserved if supported. Node2D, Node3D and Control support this argument (but Control keeps only position).

void replace_by(node: Node, keep_groups: bool = false) 🔗

Replaces this node by the given node. All children of this node are moved to node.

If keep_groups is true, the node is added to the same groups that the replaced node is in (see add_to_group()).

Warning: The replaced node is removed from the tree, but it is not deleted. To prevent memory leaks, store a reference to the node in a variable, or use Object.free().

void request_ready() 🔗

Requests _ready() to be called again the next time the node enters the tree. Does not immediately call _ready().

Note: This method only affects the current node. If the node's children also need to request ready, this method needs to be called for each one of them. When the node and its children enter the tree again, the order of _ready() callbacks will be the same as normal.

void reset_physics_interpolation() 🔗

When physics interpolation is active, moving a node to a radically different transform (such as placement within a level) can result in a visible glitch as the object is rendered moving from the old to new position over the physics tick.

That glitch can be prevented by calling this method, which temporarily disables interpolation until the physics tick is complete.

The notification NOTIFICATION_RESET_PHYSICS_INTERPOLATION will be received by the node and all children recursively.

Note: This function should be called after moving the node, rather than before.

Error rpc(method: StringName, ...) vararg 🔗

Sends a remote procedure call request for the given method to peers on the network (and locally), sending additional arguments to the method called by the RPC. The call request will only be received by nodes with the same NodePath, including the exact same name. Behavior depends on the RPC configuration for the given method (see rpc_config() and @GDScript.@rpc). By default, methods are not exposed to RPCs.

May return @GlobalScope.OK if the call is successful, @GlobalScope.ERR_INVALID_PARAMETER if the arguments passed in the method do not match, @GlobalScope.ERR_UNCONFIGURED if the node's multiplayer cannot be fetched (such as when the node is not inside the tree), @GlobalScope.ERR_CONNECTION_ERROR if multiplayer's connection is not available.

Note: You can only safely use RPCs on clients after you received the MultiplayerAPI.connected_to_server signal from the MultiplayerAPI. You also need to keep track of the connection state, either by the MultiplayerAPI signals like MultiplayerAPI.server_disconnected or by checking (get_multiplayer().peer.get_connection_status() == CONNECTION_CONNECTED).

void rpc_config(method: StringName, config: Variant) 🔗

Changes the RPC configuration for the given method. config should either be null to disable the feature (as by default), or a Dictionary containing the following entries:

rpc_mode: see RPCMode;

transfer_mode: see TransferMode;

call_local: if true, the method will also be called locally;

channel: an int representing the channel to send the RPC on.

Note: In GDScript, this method corresponds to the @GDScript.@rpc annotation, with various parameters passed (@rpc(any), @rpc(authority)...). See also the high-level multiplayer tutorial.

Error rpc_id(peer_id: int, method: StringName, ...) vararg 🔗

Sends a rpc() to a specific peer identified by peer_id (see MultiplayerPeer.set_target_peer()).

May return @GlobalScope.OK if the call is successful, @GlobalScope.ERR_INVALID_PARAMETER if the arguments passed in the method do not match, @GlobalScope.ERR_UNCONFIGURED if the node's multiplayer cannot be fetched (such as when the node is not inside the tree), @GlobalScope.ERR_CONNECTION_ERROR if multiplayer's connection is not available.

void set_deferred_thread_group(property: StringName, value: Variant) 🔗

Similar to call_deferred_thread_group(), but for setting properties.

void set_display_folded(fold: bool) 🔗

If set to true, the node appears folded in the Scene dock. As a result, all of its children are hidden. This method is intended to be used in editor plugins and tools, but it also works in release builds. See also is_displayed_folded().

void set_editable_instance(node: Node, is_editable: bool) 🔗

Set to true to allow all nodes owned by node to be available, and editable, in the Scene dock, even if their owner is not the scene root. This method is intended to be used in editor plugins and tools, but it also works in release builds. See also is_editable_instance().

void set_multiplayer_authority(id: int, recursive: bool = true) 🔗

Sets the node's multiplayer authority to the peer with the given peer id. The multiplayer authority is the peer that has authority over the node on the network. Defaults to peer ID 1 (the server). Useful in conjunction with rpc_config() and the MultiplayerAPI.

If recursive is true, the given peer is recursively set as the authority for all children of this node.

Warning: This does not automatically replicate the new authority to other peers. It is the developer's responsibility to do so. You may replicate the new authority's information using MultiplayerSpawner.spawn_function, an RPC, or a MultiplayerSynchronizer. Furthermore, the parent's authority does not propagate to newly added children.

void set_physics_process(enable: bool) 🔗

If set to true, enables physics (fixed framerate) processing. When a node is being processed, it will receive a NOTIFICATION_PHYSICS_PROCESS at a fixed (usually 60 FPS, see Engine.physics_ticks_per_second to change) interval (and the _physics_process() callback will be called if it exists).

Note: If _physics_process() is overridden, this will be automatically enabled before _ready() is called.

void set_physics_process_internal(enable: bool) 🔗

If set to true, enables internal physics for this node. Internal physics processing happens in isolation from the normal _physics_process() calls and is used by some nodes internally to guarantee proper functioning even if the node is paused or physics processing is disabled for scripting (set_physics_process()).

Warning: Built-in nodes rely on internal processing for their internal logic. Disabling it is unsafe and may lead to unexpected behavior. Use this method if you know what you are doing.

void set_process(enable: bool) 🔗

If set to true, enables processing. When a node is being processed, it will receive a NOTIFICATION_PROCESS on every drawn frame (and the _process() callback will be called if it exists).

Note: If _process() is overridden, this will be automatically enabled before _ready() is called.

Note: This method only affects the _process() callback, i.e. it has no effect on other callbacks like _physics_process(). If you want to disable all processing for the node, set process_mode to PROCESS_MODE_DISABLED.

void set_process_input(enable: bool) 🔗

If set to true, enables input processing.

Note: If _input() is overridden, this will be automatically enabled before _ready() is called. Input processing is also already enabled for GUI controls, such as Button and TextEdit.

void set_process_internal(enable: bool) 🔗

If set to true, enables internal processing for this node. Internal processing happens in isolation from the normal _process() calls and is used by some nodes internally to guarantee proper functioning even if the node is paused or processing is disabled for scripting (set_process()).

Warning: Built-in nodes rely on internal processing for their internal logic. Disabling it is unsafe and may lead to unexpected behavior. Use this method if you know what you are doing.

void set_process_shortcut_input(enable: bool) 🔗

If set to true, enables shortcut processing for this node.

Note: If _shortcut_input() is overridden, this will be automatically enabled before _ready() is called.

void set_process_unhandled_input(enable: bool) 🔗

If set to true, enables unhandled input processing. It enables the node to receive all input that was not previously handled (usually by a Control).

Note: If _unhandled_input() is overridden, this will be automatically enabled before _ready() is called. Unhandled input processing is also already enabled for GUI controls, such as Button and TextEdit.

void set_process_unhandled_key_input(enable: bool) 🔗

If set to true, enables unhandled key input processing.

Note: If _unhandled_key_input() is overridden, this will be automatically enabled before _ready() is called.

void set_scene_instance_load_placeholder(load_placeholder: bool) 🔗

If set to true, the node becomes an InstancePlaceholder when packed and instantiated from a PackedScene. See also get_scene_instance_load_placeholder().

void set_thread_safe(property: StringName, value: Variant) 🔗

Similar to call_thread_safe(), but for setting properties.

void set_translation_domain_inherited() 🔗

Makes this node inherit the translation domain from its parent node. If this node has no parent, the main translation domain will be used.

This is the default behavior for all nodes. Calling Object.set_translation_domain() disables this behavior.

void update_configuration_warnings() 🔗

Refreshes the warnings displayed for this node in the Scene dock. Use _get_configuration_warnings() to customize the warning messages to display.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---
