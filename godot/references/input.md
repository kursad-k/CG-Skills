# Godot - Input

**Pages:** 19

---

## InputEventAction

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventaction.html

**Contents:**
- InputEventAction
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEvent < Resource < RefCounted < Object

An input event type for actions.

Contains a generic action which can be targeted from several types of inputs. Actions and their events can be set in the Input Map tab in Project > Project Settings, or with the InputMap class.

Note: Unlike the other InputEvent subclasses which map to unique physical events, this virtual one is not emitted by the engine. This class is useful to emit actions manually with Input.parse_input_event(), which are then received in Node._input(). To check if a physical event matches an action from the Input Map, use InputEvent.is_action() and InputEvent.is_action_pressed().

Using InputEvent: Actions

2D Dodge The Creeps Demo

StringName action = &"" 🔗

void set_action(value: StringName)

StringName get_action()

The action's name. This is usually the name of an existing action in the InputMap which you want this custom event to match.

int event_index = -1 🔗

void set_event_index(value: int)

int get_event_index()

The real event index in action this event corresponds to (from events defined for this action in the InputMap). If -1, a unique ID will be used and actions pressed with this ID will need to be released with another InputEventAction.

bool pressed = false 🔗

void set_pressed(value: bool)

If true, the action's state is pressed. If false, the action's state is released.

float strength = 1.0 🔗

void set_strength(value: float)

The action's strength between 0 and 1. This value is considered as equal to 0 if pressed is false. The event strength allows faking analog joypad motion events, by specifying how strongly the joypad axis is bent or pressed.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventFromWindow

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventfromwindow.html

**Contents:**
- InputEventFromWindow
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEvent < Resource < RefCounted < Object

Inherited By: InputEventScreenDrag, InputEventScreenTouch, InputEventWithModifiers

Abstract base class for Viewport-based input events.

InputEventFromWindow represents events specifically received by windows. This includes mouse events, keyboard events in focused windows or touch screen actions.

void set_window_id(value: int)

The ID of a Window that received this event.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventGesture

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventgesture.html

**Contents:**
- InputEventGesture
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEventWithModifiers < InputEventFromWindow < InputEvent < Resource < RefCounted < Object

Inherited By: InputEventMagnifyGesture, InputEventPanGesture

Abstract base class for touch gestures.

InputEventGestures are sent when a user performs a supported gesture on a touch screen. Gestures can't be emulated using mouse, because they typically require multi-touch.

Vector2 position = Vector2(0, 0) 🔗

void set_position(value: Vector2)

Vector2 get_position()

The local gesture position relative to the Viewport. If used in Control._gui_input(), the position is relative to the current Control that received this gesture.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventJoypadMotion

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventjoypadmotion.html

**Contents:**
- InputEventJoypadMotion
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEvent < Resource < RefCounted < Object

Represents axis motions (such as joystick or analog triggers) from a gamepad.

Stores information about joystick motions. One InputEventJoypadMotion represents one axis at a time. For gamepad buttons, see InputEventJoypadButton.

void set_axis(value: JoyAxis)

float axis_value = 0.0 🔗

void set_axis_value(value: float)

float get_axis_value()

Current position of the joystick on the given axis. The value ranges from -1.0 to 1.0. A value of 0 means the axis is in its resting position.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventKey

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventkey.html

**Contents:**
- InputEventKey
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: InputEventWithModifiers < InputEventFromWindow < InputEvent < Resource < RefCounted < Object

Represents a key on a keyboard being pressed or released.

An input event for keys on a keyboard. Supports key presses, key releases and echo events. It can also be received in Node._unhandled_key_input().

Note: Events received from the keyboard usually have all properties set. Event mappings should have only one of the keycode, physical_keycode or unicode set.

When events are compared, properties are checked in the following priority - keycode, physical_keycode and unicode. Events with the first matching value will be considered equal.

as_text_key_label() const

as_text_keycode() const

as_text_location() const

as_text_physical_keycode() const

get_key_label_with_modifiers() const

get_keycode_with_modifiers() const

get_physical_keycode_with_modifiers() const

void set_echo(value: bool)

If true, the key was already pressed before this event. An echo event is a repeated key event sent when the user is holding down the key.

Note: The rate at which echo events are sent is typically around 20 events per second (after holding down the key for roughly half a second). However, the key repeat delay/speed can be changed by the user or disabled entirely in the operating system settings. To ensure your project works correctly on all configurations, do not assume the user has a specific key repeat configuration in your project's behavior.

void set_key_label(value: Key)

Represents the localized label printed on the key in the current keyboard layout, which corresponds to one of the Key constants or any valid Unicode character.

For keyboard layouts with a single label on the key, it is equivalent to keycode.

To get a human-readable representation of the InputEventKey, use OS.get_keycode_string(event.key_label) where event is the InputEventKey.

void set_keycode(value: Key)

Latin label printed on the key in the current keyboard layout, which corresponds to one of the Key constants.

To get a human-readable representation of the InputEventKey, use OS.get_keycode_string(event.keycode) where event is the InputEventKey.

KeyLocation location = 0 🔗

void set_location(value: KeyLocation)

KeyLocation get_location()

Represents the location of a key which has both left and right versions, such as Shift or Alt.

Key physical_keycode = 0 🔗

void set_physical_keycode(value: Key)

Key get_physical_keycode()

Represents the physical location of a key on the 101/102-key US QWERTY keyboard, which corresponds to one of the Key constants.

To get a human-readable representation of the InputEventKey, use OS.get_keycode_string() in combination with DisplayServer.keyboard_get_keycode_from_physical():

bool pressed = false 🔗

void set_pressed(value: bool)

If true, the key's state is pressed. If false, the key's state is released.

void set_unicode(value: int)

The key Unicode character code (when relevant), shifted by modifier keys. Unicode character codes for composite characters and complex scripts may not be available unless IME input mode is active. See Window.set_ime_active() for more information.

String as_text_key_label() const 🔗

Returns a String representation of the event's key_label and modifiers.

String as_text_keycode() const 🔗

Returns a String representation of the event's keycode and modifiers.

String as_text_location() const 🔗

Returns a String representation of the event's location. This will be a blank string if the event is not specific to a location.

String as_text_physical_keycode() const 🔗

Returns a String representation of the event's physical_keycode and modifiers.

Key get_key_label_with_modifiers() const 🔗

Returns the localized key label combined with modifier keys such as Shift or Alt. See also InputEventWithModifiers.

To get a human-readable representation of the InputEventKey with modifiers, use OS.get_keycode_string(event.get_key_label_with_modifiers()) where event is the InputEventKey.

Key get_keycode_with_modifiers() const 🔗

Returns the Latin keycode combined with modifier keys such as Shift or Alt. See also InputEventWithModifiers.

To get a human-readable representation of the InputEventKey with modifiers, use OS.get_keycode_string(event.get_keycode_with_modifiers()) where event is the InputEventKey.

Key get_physical_keycode_with_modifiers() const 🔗

Returns the physical keycode combined with modifier keys such as Shift or Alt. See also InputEventWithModifiers.

To get a human-readable representation of the InputEventKey with modifiers, use OS.get_keycode_string(event.get_physical_keycode_with_modifiers()) where event is the InputEventKey.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (yaml):
```yaml
+-----+ +-----+
| Q   | | Q   | - "Q" - keycode
|   Й | |  ض | - "Й" and "ض" - key_label
+-----+ +-----+
```

Example 2 (yaml):
```yaml
+-----+ +-----+
| Q   | | Q   | - "Q" - keycode
|   Й | |  ض | - "Й" and "ض" - key_label
+-----+ +-----+
```

Example 3 (gdscript):
```gdscript
func _input(event):
    if event is InputEventKey:
        var keycode = DisplayServer.keyboard_get_keycode_from_physical(event.physical_keycode)
        print(OS.get_keycode_string(keycode))
```

Example 4 (python):
```python
public override void _Input(InputEvent @event)
{
    if (@event is InputEventKey inputEventKey)
    {
        var keycode = DisplayServer.KeyboardGetKeycodeFromPhysical(inputEventKey.PhysicalKeycode);
        GD.Print(OS.GetKeycodeString(keycode));
    }
}
```

---

## InputEventMagnifyGesture

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventmagnifygesture.html

**Contents:**
- InputEventMagnifyGesture
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEventGesture < InputEventWithModifiers < InputEventFromWindow < InputEvent < Resource < RefCounted < Object

Represents a magnifying touch gesture.

Stores the factor of a magnifying touch gesture. This is usually performed when the user pinches the touch screen and used for zooming in/out.

Note: On Android, this requires the ProjectSettings.input_devices/pointing/android/enable_pan_and_scale_gestures project setting to be enabled.

void set_factor(value: float)

The amount (or delta) of the event. This value is closer to 1.0 the slower the gesture is performed.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventMIDI

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventmidi.html

**Contents:**
- InputEventMIDI
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEvent < Resource < RefCounted < Object

Represents a MIDI message from a MIDI device, such as a musical keyboard.

InputEventMIDI stores information about messages from MIDI (Musical Instrument Digital Interface) devices. These may include musical keyboards, synthesizers, and drum machines.

MIDI messages can be received over a 5-pin MIDI connector or over USB. If your device supports both be sure to check the settings in the device to see which output it is using.

By default, Godot does not detect MIDI devices. You need to call OS.open_midi_inputs(), first. You can check which devices are detected with OS.get_connected_midi_inputs(), and close the connection with OS.close_midi_inputs().

Note: Godot does not support MIDI output, so there is no way to emit MIDI messages from Godot. Only MIDI input is supported.

Note: On the Web platform, using MIDI input requires a browser permission to be granted first. This permission request is performed when calling OS.open_midi_inputs(). MIDI input will not work until the user accepts the permission request.

MIDI Message Status Byte List

Wikipedia General MIDI Instrument List

Wikipedia Piano Key Frequencies List

void set_channel(value: int)

The MIDI channel of this message, ranging from 0 to 15. MIDI channel 9 is reserved for percussion instruments.

int controller_number = 0 🔗

void set_controller_number(value: int)

int get_controller_number()

The unique number of the controller, if message is @GlobalScope.MIDI_MESSAGE_CONTROL_CHANGE, otherwise this is 0. This value can be used to identify sliders for volume, balance, and panning, as well as switches and pedals on the MIDI device. See the General MIDI specification for a small list.

int controller_value = 0 🔗

void set_controller_value(value: int)

int get_controller_value()

The value applied to the controller. If message is @GlobalScope.MIDI_MESSAGE_CONTROL_CHANGE, this value ranges from 0 to 127, otherwise it is 0. See also controller_value.

void set_instrument(value: int)

The instrument (also called program or preset) used on this MIDI message. This value ranges from 0 to 127.

To see what each value means, refer to the General MIDI's instrument list. Keep in mind that the list is off by 1 because it does not begin from 0. A value of 0 corresponds to the acoustic grand piano.

MIDIMessage message = 0 🔗

void set_message(value: MIDIMessage)

MIDIMessage get_message()

Represents the type of MIDI message (see the MIDIMessage enum).

For more information, see the MIDI message status byte list chart.

void set_pitch(value: int)

The pitch index number of this MIDI message. This value ranges from 0 to 127.

On a piano, the middle C is 60, followed by a C-sharp (61), then a D (62), and so on. Each octave is split in offsets of 12. See the "MIDI note number" column of the piano key frequency chart a full list.

void set_pressure(value: int)

The strength of the key being pressed. This value ranges from 0 to 127.

Note: For many devices, this value is always 0. Other devices such as musical keyboards may simulate pressure by changing the velocity, instead.

void set_velocity(value: int)

The velocity of the MIDI message. This value ranges from 0 to 127. For a musical keyboard, this corresponds to how quickly the key was pressed, and is rarely above 110 in practice.

Note: Some MIDI devices may send a @GlobalScope.MIDI_MESSAGE_NOTE_ON message with 0 velocity and expect it to be treated the same as a @GlobalScope.MIDI_MESSAGE_NOTE_OFF message. If necessary, this can be handled with a few lines of code:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    OS.open_midi_inputs()
    print(OS.get_connected_midi_inputs())

func _input(input_event):
    if input_event is InputEventMIDI:
        _print_midi_info(input_event)

func _print_midi_info(midi_event):
    print(midi_event)
    print("Channel ", midi_event.channel)
    print("Message ", midi_event.message)
    print("Pitch ", midi_event.pitch)
    print("Velocity ", midi_event.velocity)
    print("Instrument ", midi_event.instrument)
    print("Pressure ", midi_event.pressure)
    print("Controller number: ", midi_event.controller_number)
    print("Controller value: ", midi_event.controller_value)
```

Example 2 (json):
```json
public override void _Ready()
{
    OS.OpenMidiInputs();
    GD.Print(OS.GetConnectedMidiInputs());
}

public override void _Input(InputEvent inputEvent)
{
    if (inputEvent is InputEventMidi midiEvent)
    {
        PrintMIDIInfo(midiEvent);
    }
}

private void PrintMIDIInfo(InputEventMidi midiEvent)
{
    GD.Print(midiEvent);
    GD.Print($"Channel {midiEvent.Channel}");
    GD.Print($"Message {midiEvent.Message}");
    GD.Print($"Pitch {midiEvent.Pitch}");
    GD.Print($"Velocity {midiEvent.Velocity}");
    GD.Print($"Instrument {midiEvent.Instrument}");
    GD.Print($"Pressure {midiEvent.Pressure}");
    GD.Print($"Controller number: {midiEvent.ControllerNumber}");
    GD.Print($"Controller value: {midiEvent.ControllerValue}");
}
```

Example 3 (go):
```go
func _input(event):
    if event is InputEventMIDI:
        if event.message == MIDI_MESSAGE_NOTE_ON and event.velocity > 0:
            print("Note pressed!")
```

---

## InputEventMouseMotion

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventmousemotion.html

**Contents:**
- InputEventMouseMotion
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEventMouse < InputEventWithModifiers < InputEventFromWindow < InputEvent < Resource < RefCounted < Object

Represents a mouse or a pen movement.

Stores information about a mouse or a pen motion. This includes relative position, absolute position, and velocity. See Node._input().

Note: By default, this event is only emitted once per frame rendered at most. If you need more precise input reporting, set Input.use_accumulated_input to false to make events emitted as often as possible. If you use InputEventMouseMotion to draw lines, consider using Geometry2D.bresenham_line() as well to avoid visible gaps in lines if the user is moving the mouse quickly.

Note: This event may be emitted even when the mouse hasn't moved, either by the operating system or by Godot itself. If you really need to know if the mouse has moved (e.g. to suppress displaying a tooltip), you should check that relative.is_zero_approx() is false.

Mouse and input coordinates

bool pen_inverted = false 🔗

void set_pen_inverted(value: bool)

bool get_pen_inverted()

Returns true when using the eraser end of a stylus pen.

Note: This property is implemented on Linux, macOS and Windows.

float pressure = 0.0 🔗

void set_pressure(value: float)

Represents the pressure the user puts on the pen. Ranges from 0.0 to 1.0.

Vector2 relative = Vector2(0, 0) 🔗

void set_relative(value: Vector2)

Vector2 get_relative()

The mouse position relative to the previous position (position at the last frame).

Note: Since InputEventMouseMotion may only be emitted when the mouse moves, it is not possible to reliably detect when the mouse has stopped moving by checking this property. A separate, short timer may be necessary.

Note: relative is automatically scaled according to the content scale factor, which is defined by the project's stretch mode settings. This means mouse sensitivity will appear different depending on resolution when using relative in a script that handles mouse aiming with the Input.MOUSE_MODE_CAPTURED mouse mode. To avoid this, use screen_relative instead.

Vector2 screen_relative = Vector2(0, 0) 🔗

void set_screen_relative(value: Vector2)

Vector2 get_screen_relative()

The unscaled mouse position relative to the previous position in the coordinate system of the screen (position at the last frame).

Note: Since InputEventMouseMotion may only be emitted when the mouse moves, it is not possible to reliably detect when the mouse has stopped moving by checking this property. A separate, short timer may be necessary.

Note: This coordinate is not scaled according to the content scale factor or calls to InputEvent.xformed_by(). This should be preferred over relative for mouse aiming when using the Input.MOUSE_MODE_CAPTURED mouse mode, regardless of the project's stretch mode.

Vector2 screen_velocity = Vector2(0, 0) 🔗

void set_screen_velocity(value: Vector2)

Vector2 get_screen_velocity()

The unscaled mouse velocity in pixels per second in screen coordinates. This velocity is not scaled according to the content scale factor or calls to InputEvent.xformed_by().

Note: Use screen_relative for mouse aiming using the Input.MOUSE_MODE_CAPTURED mouse mode.

Vector2 tilt = Vector2(0, 0) 🔗

void set_tilt(value: Vector2)

Represents the angles of tilt of the pen. Positive X-coordinate value indicates a tilt to the right. Positive Y-coordinate value indicates a tilt toward the user. Ranges from -1.0 to 1.0 for both axes.

Vector2 velocity = Vector2(0, 0) 🔗

void set_velocity(value: Vector2)

Vector2 get_velocity()

The mouse velocity in pixels per second.

Note: velocity is automatically scaled according to the content scale factor, which is defined by the project's stretch mode settings. That means mouse sensitivity may appear different depending on resolution.

Note: Use screen_relative for mouse aiming using the Input.MOUSE_MODE_CAPTURED mouse mode.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventMouse

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventmouse.html

**Contents:**
- InputEventMouse
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEventWithModifiers < InputEventFromWindow < InputEvent < Resource < RefCounted < Object

Inherited By: InputEventMouseButton, InputEventMouseMotion

Base input event type for mouse events.

Stores general information about mouse events.

BitField[MouseButtonMask]

BitField[MouseButtonMask] button_mask = 0 🔗

void set_button_mask(value: BitField[MouseButtonMask])

BitField[MouseButtonMask] get_button_mask()

The mouse button mask identifier, one of or a bitwise combination of the MouseButton button masks.

Vector2 global_position = Vector2(0, 0) 🔗

void set_global_position(value: Vector2)

Vector2 get_global_position()

When received in Node._input() or Node._unhandled_input(), returns the mouse's position in the root Viewport using the coordinate system of the root Viewport.

When received in Control._gui_input(), returns the mouse's position in the CanvasLayer that the Control is in using the coordinate system of the CanvasLayer.

Vector2 position = Vector2(0, 0) 🔗

void set_position(value: Vector2)

Vector2 get_position()

When received in Node._input() or Node._unhandled_input(), returns the mouse's position in the Viewport this Node is in using the coordinate system of this Viewport.

When received in Control._gui_input(), returns the mouse's position in the Control using the local coordinate system of the Control.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventPanGesture

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventpangesture.html

**Contents:**
- InputEventPanGesture
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEventGesture < InputEventWithModifiers < InputEventFromWindow < InputEvent < Resource < RefCounted < Object

Represents a panning touch gesture.

Stores information about pan gestures. A pan gesture is performed when the user swipes the touch screen with two fingers. It's typically used for panning/scrolling.

Note: On Android, this requires the ProjectSettings.input_devices/pointing/android/enable_pan_and_scale_gestures project setting to be enabled.

Vector2 delta = Vector2(0, 0) 🔗

void set_delta(value: Vector2)

Panning amount since last pan event.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventScreenDrag

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventscreendrag.html

**Contents:**
- InputEventScreenDrag
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEventFromWindow < InputEvent < Resource < RefCounted < Object

Represents a screen drag event.

Stores information about screen drag events. See Node._input().

void set_index(value: int)

The drag event index in the case of a multi-drag event.

bool pen_inverted = false 🔗

void set_pen_inverted(value: bool)

bool get_pen_inverted()

Returns true when using the eraser end of a stylus pen.

Vector2 position = Vector2(0, 0) 🔗

void set_position(value: Vector2)

Vector2 get_position()

The drag position in the viewport the node is in, using the coordinate system of this viewport.

float pressure = 0.0 🔗

void set_pressure(value: float)

Represents the pressure the user puts on the pen. Ranges from 0.0 to 1.0.

Vector2 relative = Vector2(0, 0) 🔗

void set_relative(value: Vector2)

Vector2 get_relative()

The drag position relative to the previous position (position at the last frame).

Note: relative is automatically scaled according to the content scale factor, which is defined by the project's stretch mode settings. This means touch sensitivity will appear different depending on resolution when using relative in a script that handles touch aiming. To avoid this, use screen_relative instead.

Vector2 screen_relative = Vector2(0, 0) 🔗

void set_screen_relative(value: Vector2)

Vector2 get_screen_relative()

The unscaled drag position relative to the previous position in screen coordinates (position at the last frame). This position is not scaled according to the content scale factor or calls to InputEvent.xformed_by(). This should be preferred over relative for touch aiming regardless of the project's stretch mode.

Vector2 screen_velocity = Vector2(0, 0) 🔗

void set_screen_velocity(value: Vector2)

Vector2 get_screen_velocity()

The unscaled drag velocity in pixels per second in screen coordinates. This velocity is not scaled according to the content scale factor or calls to InputEvent.xformed_by(). This should be preferred over velocity for touch aiming regardless of the project's stretch mode.

Vector2 tilt = Vector2(0, 0) 🔗

void set_tilt(value: Vector2)

Represents the angles of tilt of the pen. Positive X-coordinate value indicates a tilt to the right. Positive Y-coordinate value indicates a tilt toward the user. Ranges from -1.0 to 1.0 for both axes.

Vector2 velocity = Vector2(0, 0) 🔗

void set_velocity(value: Vector2)

Vector2 get_velocity()

Note: velocity is automatically scaled according to the content scale factor, which is defined by the project's stretch mode settings. This means touch sensitivity will appear different depending on resolution when using velocity in a script that handles touch aiming. To avoid this, use screen_velocity instead.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventScreenTouch

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventscreentouch.html

**Contents:**
- InputEventScreenTouch
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEventFromWindow < InputEvent < Resource < RefCounted < Object

Represents a screen touch event.

Stores information about multi-touch press/release input events. Supports touch press, touch release and index for multi-touch count and order.

bool canceled = false 🔗

void set_canceled(value: bool)

If true, the touch event has been canceled.

bool double_tap = false 🔗

void set_double_tap(value: bool)

If true, the touch's state is a double tap.

void set_index(value: int)

The touch index in the case of a multi-touch event. One index = one finger.

Vector2 position = Vector2(0, 0) 🔗

void set_position(value: Vector2)

Vector2 get_position()

The touch position in the viewport the node is in, using the coordinate system of this viewport.

bool pressed = false 🔗

void set_pressed(value: bool)

If true, the touch's state is pressed. If false, the touch's state is released.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventShortcut

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventshortcut.html

**Contents:**
- InputEventShortcut
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEvent < Resource < RefCounted < Object

Represents a triggered keyboard Shortcut.

InputEventShortcut is a special event that can be received in Node._input(), Node._shortcut_input(), and Node._unhandled_input(). It is typically sent by the editor's Command Palette to trigger actions, but can also be sent manually using Viewport.push_input().

void set_shortcut(value: Shortcut)

Shortcut get_shortcut()

The Shortcut represented by this event. Its Shortcut.matches_event() method will always return true for this event.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventWithModifiers

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventwithmodifiers.html

**Contents:**
- InputEventWithModifiers
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: InputEventFromWindow < InputEvent < Resource < RefCounted < Object

Inherited By: InputEventGesture, InputEventKey, InputEventMouse

Abstract base class for input events affected by modifier keys like Shift and Alt.

Stores information about mouse, keyboard, and touch gesture input events. This includes information about which modifier keys are pressed, such as Shift or Alt. See Node._input().

Note: Modifier keys are considered modifiers only when used in combination with another key. As a result, their corresponding member variables, such as ctrl_pressed, will return false if the key is pressed on its own.

command_or_control_autoremap

BitField[KeyModifierMask]

get_modifiers_mask() const

is_command_or_control_pressed() const

bool alt_pressed = false 🔗

void set_alt_pressed(value: bool)

bool is_alt_pressed()

State of the Alt modifier.

bool command_or_control_autoremap = false 🔗

void set_command_or_control_autoremap(value: bool)

bool is_command_or_control_autoremap()

Automatically use Meta (Cmd) on macOS and Ctrl on other platforms. If true, ctrl_pressed and meta_pressed cannot be set.

bool ctrl_pressed = false 🔗

void set_ctrl_pressed(value: bool)

bool is_ctrl_pressed()

State of the Ctrl modifier.

bool meta_pressed = false 🔗

void set_meta_pressed(value: bool)

bool is_meta_pressed()

State of the Meta modifier. On Windows and Linux, this represents the Windows key (sometimes called "meta" or "super" on Linux). On macOS, this represents the Command key.

bool shift_pressed = false 🔗

void set_shift_pressed(value: bool)

bool is_shift_pressed()

State of the Shift modifier.

BitField[KeyModifierMask] get_modifiers_mask() const 🔗

Returns the keycode combination of modifier keys.

bool is_command_or_control_pressed() const 🔗

On macOS, returns true if Meta (Cmd) is pressed.

On other platforms, returns true if Ctrl is pressed.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEvent

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputevent.html

**Contents:**
- InputEvent
- Description
- Tutorials
- Properties
- Methods
- Constants
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: InputEventAction, InputEventFromWindow, InputEventJoypadButton, InputEventJoypadMotion, InputEventMIDI, InputEventShortcut

Abstract base class for input events.

Abstract base class of all types of input events. See Node._input().

Viewport and canvas transforms

2D Dodge The Creeps Demo

accumulate(with_event: InputEvent)

get_action_strength(action: StringName, exact_match: bool = false) const

is_action(action: StringName, exact_match: bool = false) const

is_action_pressed(action: StringName, allow_echo: bool = false, exact_match: bool = false) const

is_action_released(action: StringName, exact_match: bool = false) const

is_action_type() const

is_match(event: InputEvent, exact_match: bool = true) const

xformed_by(xform: Transform2D, local_ofs: Vector2 = Vector2(0, 0)) const

DEVICE_ID_EMULATION = -1 🔗

Device ID used for emulated mouse input from a touchscreen, or for emulated touch input from a mouse. This can be used to distinguish emulated mouse input from physical mouse input, or emulated touch input from physical touch input.

void set_device(value: int)

The event's device ID.

Note: device can be negative for special use cases that don't refer to devices physically present on the system. See DEVICE_ID_EMULATION.

bool accumulate(with_event: InputEvent) 🔗

Returns true if the given input event and this input event can be added together (only for events of type InputEventMouseMotion).

The given input event's position, global position and speed will be copied. The resulting relative is a sum of both events. Both events' modifiers have to be identical.

String as_text() const 🔗

Returns a String representation of the event.

float get_action_strength(action: StringName, exact_match: bool = false) const 🔗

Returns a value between 0.0 and 1.0 depending on the given actions' state. Useful for getting the value of events of type InputEventJoypadMotion.

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

bool is_action(action: StringName, exact_match: bool = false) const 🔗

Returns true if this input event matches a pre-defined action of any type.

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

bool is_action_pressed(action: StringName, allow_echo: bool = false, exact_match: bool = false) const 🔗

Returns true if the given action matches this event and is being pressed (and is not an echo event for InputEventKey events, unless allow_echo is true). Not relevant for events of type InputEventMouseMotion or InputEventScreenDrag.

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

Note: Due to keyboard ghosting, is_action_pressed() may return false even if one of the action's keys is pressed. See Input examples in the documentation for more information.

bool is_action_released(action: StringName, exact_match: bool = false) const 🔗

Returns true if the given action matches this event and is released (i.e. not pressed). Not relevant for events of type InputEventMouseMotion or InputEventScreenDrag.

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

bool is_action_type() const 🔗

Returns true if this input event's type is one that can be assigned to an input action: InputEventKey, InputEventMouseButton, InputEventJoypadButton, InputEventJoypadMotion, InputEventAction. Returns false for all other input event types.

bool is_canceled() const 🔗

Returns true if this input event has been canceled.

bool is_echo() const 🔗

Returns true if this input event is an echo event (only for events of type InputEventKey). An echo event is a repeated key event sent when the user is holding down the key. Any other event type returns false.

Note: The rate at which echo events are sent is typically around 20 events per second (after holding down the key for roughly half a second). However, the key repeat delay/speed can be changed by the user or disabled entirely in the operating system settings. To ensure your project works correctly on all configurations, do not assume the user has a specific key repeat configuration in your project's behavior.

bool is_match(event: InputEvent, exact_match: bool = true) const 🔗

Returns true if the specified event matches this event. Only valid for action events, which include key (InputEventKey), button (InputEventMouseButton or InputEventJoypadButton), axis InputEventJoypadMotion, and action (InputEventAction) events.

If exact_match is false, the check ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

Note: This method only considers the event configuration (such as the keyboard key or the joypad axis), not state information like is_pressed(), is_released(), is_echo(), or is_canceled().

bool is_pressed() const 🔗

Returns true if this input event is pressed. Not relevant for events of type InputEventMouseMotion or InputEventScreenDrag.

Note: Due to keyboard ghosting, is_pressed() may return false even if one of the action's keys is pressed. See Input examples in the documentation for more information.

bool is_released() const 🔗

Returns true if this input event is released. Not relevant for events of type InputEventMouseMotion or InputEventScreenDrag.

InputEvent xformed_by(xform: Transform2D, local_ofs: Vector2 = Vector2(0, 0)) const 🔗

Returns a copy of the given input event which has been offset by local_ofs and transformed by xform. Relevant for events of type InputEventMouseButton, InputEventMouseMotion, InputEventScreenTouch, InputEventScreenDrag, InputEventMagnifyGesture and InputEventPanGesture.

Please read the User-contributed notes policy before submitting a comment.

---

## InputMap

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputmap.html

**Contents:**
- InputMap
- Description
- Tutorials
- Methods
- Method Descriptions
- User-contributed notes

A singleton that manages all InputEventActions.

Manages all InputEventAction which can be created/modified from the project settings menu Project > Project Settings > Input Map or in code with add_action() and action_add_event(). See Node._input().

Using InputEvent: InputMap

action_add_event(action: StringName, event: InputEvent)

action_erase_event(action: StringName, event: InputEvent)

action_erase_events(action: StringName)

action_get_deadzone(action: StringName)

action_get_events(action: StringName)

action_has_event(action: StringName, event: InputEvent)

action_set_deadzone(action: StringName, deadzone: float)

add_action(action: StringName, deadzone: float = 0.2)

erase_action(action: StringName)

event_is_action(event: InputEvent, action: StringName, exact_match: bool = false) const

get_action_description(action: StringName) const

has_action(action: StringName) const

load_from_project_settings()

void action_add_event(action: StringName, event: InputEvent) 🔗

Adds an InputEvent to an action. This InputEvent will trigger the action.

void action_erase_event(action: StringName, event: InputEvent) 🔗

Removes an InputEvent from an action.

void action_erase_events(action: StringName) 🔗

Removes all events from an action.

float action_get_deadzone(action: StringName) 🔗

Returns a deadzone value for the action.

Array[InputEvent] action_get_events(action: StringName) 🔗

Returns an array of InputEvents associated with a given action.

Note: When used in the editor (e.g. a tool script or EditorPlugin), this method will return events for the editor action. If you want to access your project's input binds from the editor, read the input/* settings from ProjectSettings.

bool action_has_event(action: StringName, event: InputEvent) 🔗

Returns true if the action has the given InputEvent associated with it.

void action_set_deadzone(action: StringName, deadzone: float) 🔗

Sets a deadzone value for the action.

void add_action(action: StringName, deadzone: float = 0.2) 🔗

Adds an empty action to the InputMap with a configurable deadzone.

An InputEvent can then be added to this action with action_add_event().

void erase_action(action: StringName) 🔗

Removes an action from the InputMap.

bool event_is_action(event: InputEvent, action: StringName, exact_match: bool = false) const 🔗

Returns true if the given event is part of an existing action. This method ignores keyboard modifiers if the given InputEvent is not pressed (for proper release detection). See action_has_event() if you don't want this behavior.

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

String get_action_description(action: StringName) const 🔗

Returns the human-readable description of the given action.

Array[StringName] get_actions() 🔗

Returns an array of all actions in the InputMap.

bool has_action(action: StringName) const 🔗

Returns true if the InputMap has a registered action with the given name.

void load_from_project_settings() 🔗

Clears all InputEventAction in the InputMap and load it anew from ProjectSettings.

Please read the User-contributed notes policy before submitting a comment.

---

## Input examples

**URL:** https://docs.godotengine.org/en/stable/tutorials/inputs/input_examples.html

**Contents:**
- Input examples
- Introduction
- Events versus polling
- Input events
- InputMap
  - Capturing actions
- Keyboard events
  - Keyboard modifiers
- Mouse events
  - Mouse buttons

In this tutorial, you'll learn how to use Godot's InputEvent system to capture player input. There are many different types of input your game may use - keyboard, gamepad, mouse, etc. - and many different ways to turn those inputs into actions in your game. This document will show you some of the most common scenarios, which you can use as starting points for your own projects.

For a detailed overview of how Godot's input event system works, see Using InputEvent.

Sometimes you want your game to respond to a certain input event - pressing the "jump" button, for example. For other situations, you might want something to happen as long as a key is pressed, such as movement. In the first case, you can use the _input() function, which will be called whenever an input event occurs. In the second case, Godot provides the Input singleton, which you can use to query the state of an input.

This gives you the flexibility to mix-and-match the type of input processing you do.

For the remainder of this tutorial, we'll focus on capturing individual events in _input().

Input events are objects that inherit from InputEvent. Depending on the event type, the object will contain specific properties related to that event. To see what events actually look like, add a Node and attach the following script:

As you press keys, move the mouse, and perform other inputs, you'll see each event scroll by in the output window. Here's an example of the output:

As you can see, the results are very different for the different types of input. Key events are even printed as their key symbols. For example, let's consider InputEventMouseButton. It inherits from the following classes:

InputEvent - the base class for all input events

InputEventWithModifiers - adds the ability to check if modifiers are pressed, such as Shift or Alt.

InputEventMouse - adds mouse event properties, such as position

InputEventMouseButton - contains the index of the button that was pressed, whether it was a double-click, etc.

It's a good idea to keep the class reference open while you're working with events so you can check the event type's available properties and methods.

You can encounter errors if you try to access a property on an input type that doesn't contain it - calling position on InputEventKey for example. To avoid this, make sure to test the event type first:

The InputMap is the most flexible way to handle a variety of inputs. You use this by creating named input actions, to which you can assign any number of input events, such as keypresses or mouse clicks. To see them, and to add your own, open Project -> Project Settings and select the InputMap tab:

A new Godot project includes a number of default actions already defined. To see them, turn on Show Built-in Actions in the InputMap dialog.

Once you've defined your actions, you can process them in your scripts using is_action_pressed() and is_action_released() by passing the name of the action you're looking for:

Keyboard events are captured in InputEventKey. While it's recommended to use input actions instead, there may be cases where you want to specifically look at key events. For this example, let's check for the T:

See @GlobalScope_Key for a list of keycode constants.

Due to keyboard ghosting, not all key inputs may be registered at a given time if you press too many keys at once. Due to their location on the keyboard, certain keys are more prone to ghosting than others. Some keyboards feature antighosting at a hardware level, but this feature is generally not present on low-end keyboards and laptop keyboards.

As a result, it's recommended to use a default keyboard layout that is designed to work well on a keyboard without antighosting. See this Gamedev Stack Exchange question for more information.

Modifier properties are inherited from InputEventWithModifiers. This allows you to check for modifier combinations using boolean properties. Let's imagine you want one thing to happen when the T is pressed, but something different when it's Shift + T:

See @GlobalScope_Key for a list of keycode constants.

Mouse events stem from the InputEventMouse class, and are separated into two types: InputEventMouseButton and InputEventMouseMotion. Note that this means that all mouse events will contain a position property.

Capturing mouse buttons is very similar to handling key events. @GlobalScope_MouseButton contains a list of MOUSE_BUTTON_* constants for each possible button, which will be reported in the event's button_index property. Note that the scrollwheel also counts as a button - two buttons, to be precise, with both MOUSE_BUTTON_WHEEL_UP and MOUSE_BUTTON_WHEEL_DOWN being separate events.

InputEventMouseMotion events occur whenever the mouse moves. You can find the move's distance with the relative property.

Here's an example using mouse events to drag-and-drop a Sprite2D node:

If you are using a touchscreen device, you can generate touch events. InputEventScreenTouch is equivalent to a mouse click event, and InputEventScreenDrag works much the same as mouse motion.

To test your touch events on a non-touchscreen device, open Project Settings and go to the "Input Devices/Pointing" section. Enable "Emulate Touch From Mouse" and your project will interpret mouse clicks and motion as touch events.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (go):
```go
func _input(event):
    if event.is_action_pressed("jump"):
        jump()


func _physics_process(delta):
    if Input.is_action_pressed("move_right"):
        # Move as long as the key/button is pressed.
        position.x += speed * delta
```

Example 2 (json):
```json
public override void _Input(InputEvent @event)
{
    if (@event.IsActionPressed("jump"))
    {
        Jump();
    }
}

public override void _PhysicsProcess(double delta)
{
    if (Input.IsActionPressed("move_right"))
    {
        // Move as long as the key/button is pressed.
        position.X += speed * (float)delta;
    }
}
```

Example 3 (gdscript):
```gdscript
extends Node


func _input(event):
    print(event.as_text())
```

Example 4 (swift):
```swift
using Godot;

public partial class Node : Godot.Node
{
    public override void _Input(InputEvent @event)
    {
        GD.Print(@event.AsText());
    }
}
```

---

## Mouse and input coordinates

**URL:** https://docs.godotengine.org/en/stable/tutorials/inputs/mouse_and_input_coordinates.html

**Contents:**
- Mouse and input coordinates
- About
- Hardware display coordinates
- Viewport display coordinates
- User-contributed notes

The reason for this small tutorial is to clear up many common mistakes about input coordinates, obtaining mouse position and screen resolution, etc.

Using hardware coordinates makes sense in the case of writing complex UIs meant to run on PC, such as editors, MMOs, tools, etc. However, it does not make as much sense outside of that scope.

Godot uses viewports to display content, and viewports can be scaled by several options (see Multiple resolutions tutorial). Use, then, the functions in nodes to obtain the mouse coordinates and viewport size, for example:

Alternatively, it's possible to ask the viewport for the mouse position:

When the mouse mode is set to Input.MOUSE_MODE_CAPTURED, the event.position value from InputEventMouseMotion is the center of the screen. Use event.relative instead of event.position and event.velocity to process mouse movement and position changes.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (go):
```go
func _input(event):
    # Mouse in viewport coordinates.
    if event is InputEventMouseButton:
        print("Mouse Click/Unclick at: ", event.position)
    elif event is InputEventMouseMotion:
        print("Mouse Motion at: ", event.position)

    # Print the size of the viewport.
    print("Viewport Resolution is: ", get_viewport().get_visible_rect().size)
```

Example 2 (json):
```json
public override void _Input(InputEvent @event)
{
    // Mouse in viewport coordinates.
    if (@event is InputEventMouseButton eventMouseButton)
    {
        GD.Print("Mouse Click/Unclick at: ", eventMouseButton.Position);
    }
    else if (@event is InputEventMouseMotion eventMouseMotion)
    {
        GD.Print("Mouse Motion at: ", eventMouseMotion.Position);
    }

    // Print the size of the viewport.
    GD.Print("Viewport Resolution is: ", GetViewport().GetVisibleRect().Size);
}
```

Example 3 (unknown):
```unknown
get_viewport().get_mouse_position()
```

Example 4 (unknown):
```unknown
GetViewport().GetMousePosition();
```

---

## Using InputEvent

**URL:** https://docs.godotengine.org/en/stable/tutorials/inputs/inputevent.html

**Contents:**
- Using InputEvent
- What is it?
- How does it work?
- Anatomy of an InputEvent
- Input actions
- InputMap
- User-contributed notes

Managing input is usually complex, no matter the OS or platform. To ease this a little, a special built-in type is provided, InputEvent. This datatype can be configured to contain several types of input events. Input events travel through the engine and can be received in multiple locations, depending on the purpose.

Here is a quick example, closing your game if the escape key is hit:

However, it is cleaner and more flexible to use the provided InputMap feature, which allows you to define input actions and assign them different keys. This way, you can define multiple keys for the same action (e.g. the keyboard escape key and the start button on a gamepad). You can then more easily change this mapping in the project settings without updating your code, and even build a key mapping feature on top of it to allow your game to change the key mapping at runtime!

You can set up your InputMap under Project > Project Settings > Input Map and then use those actions like this:

Every input event is originated from the user/player (though it's possible to generate an InputEvent and feed them back to the engine, which is useful for gestures). The DisplayServer for each platform will read events from the operating system, then feed them to the root Window.

The window's Viewport does quite a lot of stuff with the received input, in order:

If the Viewport is embedding Windows, the Viewport tries to interpret the event in its capability as a Window-Manager (e.g. for resizing or moving Windows).

Next if an embedded Window is focused, the event is sent to that Window and processed in the Window's Viewport and afterwards treated as handled. If no embedded Window is focused, the event is sent to the nodes of the current viewport in the following order.

First of all, the standard Node._input() function will be called in any node that overrides it (and hasn't disabled input processing with Node.set_process_input()). If any function consumes the event, it can call Viewport.set_input_as_handled(), and the event will not spread any more. This ensures that you can filter all events of interest, even before the GUI. For gameplay input, Node._unhandled_input() is generally a better fit, because it allows the GUI to intercept the events.

Second, it will try to feed the input to the GUI, and see if any control can receive it. If so, the Control will be called via the virtual function Control._gui_input() and the signal "gui_input" will be emitted (this function is re-implementable by script by inheriting from it). If the control wants to "consume" the event, it will call Control.accept_event() and the event will not spread any more. Use the Control.mouse_filter property to control whether a Control is notified of mouse events via Control._gui_input() callback, and whether these events are propagated further.

If so far no one consumed the event, the Node._shortcut_input() callback will be called if overridden (and not disabled with Node.set_process_shortcut_input()). This happens only for InputEventKey, InputEventShortcut and InputEventJoypadButton. If any function consumes the event, it can call Viewport.set_input_as_handled(), and the event will not spread any more. The shortcut input callback is ideal for treating events that are intended as shortcuts.

If so far no one consumed the event, the Node._unhandled_key_input() callback will be called if overridden (and not disabled with Node.set_process_unhandled_key_input()). This happens only if the event is an InputEventKey. If any function consumes the event, it can call Viewport.set_input_as_handled(), and the event will not spread any more. The unhandled key input callback is ideal for key events.

If so far no one consumed the event, the Node._unhandled_input() callback will be called if overridden (and not disabled with Node.set_process_unhandled_input()). If any function consumes the event, it can call Viewport.set_input_as_handled(), and the event will not spread any more. The unhandled input callback is ideal for full-screen gameplay events, so they are not received when a GUI is active.

If no one wanted the event so far, and Object Picking is turned on, the event is used for object picking. For the root viewport, this can also be enabled in Project Settings. In the case of a 3D scene if a Camera3D is assigned to the Viewport, a ray to the physics world (in the ray direction from the click) will be cast. If this ray hits an object, it will call the CollisionObject3D._input_event() function in the relevant physics object. In the case of a 2D scene, conceptually the same happens with CollisionObject2D._input_event().

When sending events to its child and descendant nodes, the viewport will do so, as depicted in the following graphic, in a reverse depth-first order, starting with the node at the bottom of the scene tree, and ending at the root node. Excluded from this process are Windows and SubViewports.

This order doesn't apply to Control._gui_input(), which uses a different method based on event location or focused Control. GUI mouse events also travel up the scene tree, subject to the Control.mouse_filter restrictions described above. However, since these events target specific Controls, only direct ancestors of the targeted Control node receive the event. GUI keyboard and joypad events do not travel up the scene tree, and can only be handled by the Control that received them. Otherwise, they will be propagated as non-GUI events through Node._unhandled_input().

Since Viewports don't send events to other SubViewports, one of the following methods has to be used:

Use a SubViewportContainer, which automatically sends events to its child SubViewports after Node._input() or Control._gui_input().

Implement event propagation based on the individual requirements.

In accordance with Godot's node-based design, this enables specialized child nodes to handle and consume particular events, while their ancestors, and ultimately the scene root, can provide more generalized behavior if needed.

InputEvent is just a base built-in type, it does not represent anything and only contains some basic information, such as event ID (which is increased for each event), device index, etc.

There are several specialized types of InputEvent, described in the table below:

Contains a keycode and Unicode value, as well as modifiers.

InputEventMouseButton

Contains click information, such as button, modifiers, etc.

InputEventMouseMotion

Contains motion information, such as relative and absolute positions and speed.

InputEventJoypadMotion

Contains Joystick/Joypad analog axis information.

InputEventJoypadButton

Contains Joystick/Joypad button information.

InputEventScreenTouch

Contains multi-touch press/release information. (only available on mobile devices)

Contains multi-touch drag information. (only available on mobile devices)

InputEventMagnifyGesture

Contains a position, a factor as well as modifiers.

Contains a position, a delta as well as modifiers.

Contains MIDI-related information.

Contains a generic action. These events are often generated by the programmer as feedback. (more on this below)

Input actions are a grouping of zero or more InputEvents into a commonly understood title (for example, the default "ui_left" action grouping both joypad-left input and a keyboard's left arrow key). They are not required to represent an InputEvent but are useful because they abstract various inputs when programming the game logic.

The same code to work on different devices with different inputs (e.g., keyboard on PC, Joypad on console).

Input to be reconfigured at runtime.

Actions to be triggered programmatically at runtime.

Actions can be created from the Project Settings menu in the Input Map tab and assigned input events.

Any event has the methods InputEvent.is_action(), InputEvent.is_pressed() and InputEvent.is_echo().

Alternatively, it may be desired to supply the game back with an action from the game code (a good example of this is detecting gestures). The Input singleton has a method for this: Input.parse_input_event(). You would normally use it like this:

See Creating input actions for a tutorial on adding input actions in the project settings.

Customizing and re-mapping input from code is often desired. If your whole workflow depends on actions, the InputMap singleton is ideal for reassigning or creating different actions at runtime. This singleton is not saved (must be modified manually) and its state is run from the project settings (project.godot). So any dynamic system of this type needs to store settings in the way the programmer best sees fit.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (go):
```go
func _unhandled_input(event):
    if event is InputEventKey:
        if event.pressed and event.keycode == KEY_ESCAPE:
            get_tree().quit()
```

Example 2 (json):
```json
public override void _UnhandledInput(InputEvent @event)
{
    if (@event is InputEventKey eventKey)
    {
        if (eventKey.Pressed && eventKey.Keycode == Key.Escape)
        {
            GetTree().Quit();
        }
    }
}
```

Example 3 (gdscript):
```gdscript
func _process(delta):
    if Input.is_action_pressed("ui_right"):
        # Move right.
```

Example 4 (gdscript):
```gdscript
public override void _Process(double delta)
{
    if (Input.IsActionPressed("ui_right"))
    {
        // Move right.
    }
}
```

---
