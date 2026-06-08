# Godot - Ui

**Pages:** 108

---

## Applying object-oriented principles in Godot

**URL:** https://docs.godotengine.org/en/stable/tutorials/best_practices/what_are_godot_classes.html

**Contents:**
- Applying object-oriented principles in Godot
- How scripts work in the engine
- Scenes
- User-contributed notes

The engine offers two main ways to create reusable objects: scripts and scenes. Neither of these technically define classes under the hood.

Still, many best practices using Godot involve applying object-oriented programming principles to the scripts and scenes that compose your game. That is why it's useful to understand how we can think of them as classes.

This guide briefly explains how scripts and scenes work in the engine's core to help you understand how they work under the hood.

The engine provides built-in classes like Node. You can extend those to create derived types using a script.

These scripts are not technically classes. Instead, they are resources that tell the engine a sequence of initializations to perform on one of the engine's built-in classes.

Godot's internal classes have methods that register a class's data with a ClassDB. This database provides runtime access to class information. ClassDB contains information about classes like:

This ClassDB is what objects check against when performing an operation like accessing a property or calling a method. It checks the database's records and the object's base types' records to see if the object supports the operation.

Attaching a Script to your object extends the methods, properties, and signals available from the ClassDB.

Even scripts that don't use the extends keyword implicitly inherit from the engine's base RefCounted class. As a result, you can instantiate scripts without the extends keyword from code. Since they extend RefCounted though, you cannot attach them to a Node.

The behavior of scenes has many similarities to classes, so it can make sense to think of a scene as a class. Scenes are reusable, instantiable, and inheritable groups of nodes. Creating a scene is similar to having a script that creates nodes and adds them as children using add_child().

We often pair a scene with a scripted root node that makes use of the scene's nodes. As such, the script extends the scene by adding behavior through imperative code.

The content of a scene helps to define:

What nodes are available to the script.

How they are organized.

How they are initialized.

What signal connections they have with each other.

Why is any of this important to scene organization? Because instances of scenes are objects. As a result, many object-oriented principles that apply to written code also apply to scenes: single responsibility, encapsulation, and others.

The scene is always an extension of the script attached to its root node, so you can interpret it as part of a class.

Most of the techniques explained in this best practices series build on this point.

Please read the User-contributed notes policy before submitting a comment.

---

## AspectRatioContainer

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

---

## BaseButton

**URL:** https://docs.godotengine.org/en/stable/classes/class_basebutton.html

**Contents:**
- BaseButton
- Description
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Control < CanvasItem < Node < Object

Inherited By: Button, LinkButton, TextureButton

Abstract base class for GUI buttons.

BaseButton is an abstract base class for GUI buttons. It doesn't display anything by itself.

BitField[MouseButtonMask]

2 (overrides Control)

_toggled(toggled_on: bool) virtual

get_draw_mode() const

set_pressed_no_signal(pressed: bool)

Emitted when the button starts being held down.

Emitted when the button stops being held down.

Emitted when the button is toggled or pressed. This is on button_down if action_mode is ACTION_MODE_BUTTON_PRESS and on button_up otherwise.

If you need to know the button's pressed state (and toggle_mode is active), use toggled instead.

toggled(toggled_on: bool) 🔗

Emitted when the button was just toggled between pressed and normal states (only if toggle_mode is active). The new state is contained in the toggled_on argument.

DrawMode DRAW_NORMAL = 0

The normal state (i.e. not pressed, not hovered, not toggled and enabled) of buttons.

DrawMode DRAW_PRESSED = 1

The state of buttons are pressed.

DrawMode DRAW_HOVER = 2

The state of buttons are hovered.

DrawMode DRAW_DISABLED = 3

The state of buttons are disabled.

DrawMode DRAW_HOVER_PRESSED = 4

The state of buttons are both hovered and pressed.

ActionMode ACTION_MODE_BUTTON_PRESS = 0

Require just a press to consider the button clicked.

ActionMode ACTION_MODE_BUTTON_RELEASE = 1

Require a press and a subsequent release before considering the button clicked.

ActionMode action_mode = 1 🔗

void set_action_mode(value: ActionMode)

ActionMode get_action_mode()

Determines when the button is considered clicked.

ButtonGroup button_group 🔗

void set_button_group(value: ButtonGroup)

ButtonGroup get_button_group()

The ButtonGroup associated with the button. Not to be confused with node groups.

Note: The button will be configured as a radio button if a ButtonGroup is assigned to it.

BitField[MouseButtonMask] button_mask = 1 🔗

void set_button_mask(value: BitField[MouseButtonMask])

BitField[MouseButtonMask] get_button_mask()

Binary mask to choose which mouse buttons this button will respond to.

To allow both left-click and right-click, use MOUSE_BUTTON_MASK_LEFT | MOUSE_BUTTON_MASK_RIGHT.

bool button_pressed = false 🔗

void set_pressed(value: bool)

If true, the button's state is pressed. Means the button is pressed down or toggled (if toggle_mode is active). Only works if toggle_mode is true.

Note: Changing the value of button_pressed will result in toggled to be emitted. If you want to change the pressed state without emitting that signal, use set_pressed_no_signal().

bool disabled = false 🔗

void set_disabled(value: bool)

If true, the button is in disabled state and can't be clicked or toggled.

Note: If the button is disabled while held down, button_up will be emitted.

bool keep_pressed_outside = false 🔗

void set_keep_pressed_outside(value: bool)

bool is_keep_pressed_outside()

If true, the button stays pressed when moving the cursor outside the button while pressing it.

Note: This property only affects the button's visual appearance. Signals will be emitted at the same moment regardless of this property's value.

void set_shortcut(value: Shortcut)

Shortcut get_shortcut()

Shortcut associated to the button.

bool shortcut_feedback = true 🔗

void set_shortcut_feedback(value: bool)

bool is_shortcut_feedback()

If true, the button will highlight for a short amount of time when its shortcut is activated. If false and toggle_mode is false, the shortcut will activate without any visual feedback.

bool shortcut_in_tooltip = true 🔗

void set_shortcut_in_tooltip(value: bool)

bool is_shortcut_in_tooltip_enabled()

If true, the button will add information about its shortcut in the tooltip.

Note: This property does nothing when the tooltip control is customized using Control._make_custom_tooltip().

bool toggle_mode = false 🔗

void set_toggle_mode(value: bool)

bool is_toggle_mode()

If true, the button is in toggle mode. Makes the button flip state between pressed and unpressed each time its area is clicked.

void _pressed() virtual 🔗

Called when the button is pressed. If you need to know the button's pressed state (and toggle_mode is active), use _toggled() instead.

void _toggled(toggled_on: bool) virtual 🔗

Called when the button is toggled (only if toggle_mode is active).

DrawMode get_draw_mode() const 🔗

Returns the visual state used to draw the button. This is useful mainly when implementing your own draw code by either overriding _draw() or connecting to "draw" signal. The visual state of the button is defined by the DrawMode enum.

bool is_hovered() const 🔗

Returns true if the mouse has entered the button and has not left it yet.

void set_pressed_no_signal(pressed: bool) 🔗

Changes the button_pressed state of the button, without emitting toggled. Use when you just want to change the state of the button without sending the pressed event (e.g. when initializing scene). Only works if toggle_mode is true.

Note: This method doesn't unpress other buttons in button_group.

Please read the User-contributed notes policy before submitting a comment.

---

## BBCode in RichTextLabel

**URL:** https://docs.godotengine.org/en/stable/tutorials/ui/bbcode_in_richtextlabel.html

**Contents:**
- BBCode in RichTextLabel
- Introduction
- Using BBCode
- Handling user input safely
- Stripping BBCode tags
- Performance
- Using push_[tag]() and pop() functions instead of BBCode
- Reference
  - Paragraph options
  - Handling [url] tag clicks

Label nodes are great for displaying basic text, but they have limitations. If you want to change the color of the text, or its alignment, you can only do that to the entire label. You can't make a part of the text have another color, or have a part of the text centered. To get around these limitations, you would use a RichTextLabel.

RichTextLabel allows for complex formatting of text using a markup syntax or the built-in API. It uses BBCodes for the markup syntax, a system of tags that designate formatting rules for a part of the text. You may be familiar with them if you ever used forums (also known as bulletin boards, hence the "BB" in "BBCode").

Unlike Label, RichTextLabel also comes with its own vertical scrollbar. This scrollbar is automatically displayed if the text does not fit within the control's size. The scrollbar can be disabled by unchecking the Scroll Active property in the RichTextLabel inspector.

Note that the BBCode tags can also be used to some extent for other use cases:

BBCode can be used to format comments in the XML source of the class reference.

BBCode can be used in GDScript documentation comments.

BBCode can be used when printing rich text to the Output bottom panel.

You can see how BBCode in RichTextLabel works in action using the Rich Text Label with BBCode demo project.

By default, RichTextLabel functions like a normal Label. It has the property_text property, which you can edit to have uniformly formatted text. To be able to use BBCode for rich text formatting, you need to turn on the BBCode mode by setting bbcode_enabled. After that, you can edit the text property using available tags. Both properties are located at the top of the inspector after selecting a RichTextLabel node.

For example, BBCode [color=green]test[/color] would render the word "test" with a green color.

Most BBCodes consist of 3 parts: the opening tag, the content and the closing tag. The opening tag delimits the start of the formatted part, and can also carry some configuration options. Some opening tags, like the color one shown above, also require a value to work. Other opening tags may accept multiple options (separated by spaces within the opening tag). The closing tag delimits the end of the formatted part. In some cases, both the closing tag and the content can be omitted.

Unlike BBCode in HTML, leading/trailing whitespace is not removed by a RichTextLabel upon display. Duplicate spaces are also displayed as-is in the final output. This means that when displaying a code block in a RichTextLabel, you don't need to use a preformatted text tag.

RichTextLabel doesn't support entangled BBCode tags. For example, instead of using:

In a scenario where users may freely input text (such as chat in a multiplayer game), you should make sure users cannot use arbitrary BBCode tags that will be parsed by RichTextLabel. This is to avoid inappropriate use of formatting, which can be problematic if [url] tags are handled by your RichTextLabel (as players may be able to create clickable links to phishing sites or similar).

Using RichTextLabel's [lb] and/or [rb] tags, we can replace the opening and/or closing brackets of any BBCode tag in a message with those escaped tags. This prevents users from using BBCode that will be parsed as tags – instead, the BBCode will be displayed as text.

Example of unescaped user input resulting in BBCode injection (2nd line) and escaped user input (3rd line)

The above image was created using the following script:

For certain use cases, it can be desired to remove BBCode tags from the string. This is useful when displaying the RichTextLabel's text in another Control that does not support BBCode (such as a tooltip):

Removing BBCode tags entirely isn't advised for user input, as it can modify the displayed text without users understanding why part of their message was removed. Escaping user input should be preferred instead.

In most cases, you can use BBCode directly as-is since text formatting is rarely a heavy task. However, with particularly large RichTextLabels (such as console logs spanning thousands of lines), you may encounter stuttering during gameplay when the RichTextLabel's text is updated.

There are several ways to alleviate this:

Use the append_text() function instead of appending to the text property. This function will only parse BBCode for the added text, rather than parsing BBCode from the entire text property.

Use push_[tag]() and pop() functions to add tags to RichTextLabel instead of using BBCode.

Enable the Threading > Threaded property in RichTextLabel. This won't speed up processing, but it will prevent the main thread from blocking, which avoids stuttering during gameplay. Only enable threading if it's actually needed in your project, as threading has some overhead.

If you don't want to use BBCode for performance reasons, you can use functions provided by RichTextLabel to create formatting tags without writing BBCode in the text.

Every BBCode tag (including effects) has a push_[tag]() function (where [tag] is the tag's name). There are also a few convenience functions available, such as push_bold_italics() that combines both push_bold() and push_italics() into a single tag. See the RichTextLabel class reference for a complete list of push_[tag]() functions.

The pop() function is used to end any tag. Since BBCode is a tag stack, using pop() will close the most recently started tags first.

The following script will result in the same visual output as using BBCode [color=green]test [i]example[/i][/color]:

Do not set the text property directly when using formatting functions. Appending to the text property will erase all modifications made to the RichTextLabel using the append_text(), push_[tag]() and pop() functions.

Some of these BBCode tags can be used in tooltips for @export script variables as well as in the XML source of the class reference. For more information, see Class reference BBCode.

[center]{text}[/center]

[right]{text}[/right]

[indent]{text}[/indent]

[font_size={size}]{text}[/font_size]

[dropcap font={font} font_size={size} color={color} outline_size={size} outline_color={color} margins={left},{top},{right},{bottom}]{text}[/dropcap]

[lang={code}]{text}[/lang]

[color={code/name}]{text}[/color]

[bgcolor={code/name}]{text}[/bgcolor]

[fgcolor={code/name}]{text}[/fgcolor]

[ol type={type}]{items}[/ol]

Tags for bold ([b]) and italics ([i]) formatting work best if the appropriate custom fonts are set up in the RichTextLabelNode's theme overrides. If no custom bold or italic fonts are defined, faux bold and italic fonts will be generated by Godot. These fonts rarely look good in comparison to hand-made bold/italic font variants.

The monospaced ([code]) tag only works if a custom font is set up in the RichTextLabel node's theme overrides. Otherwise, monospaced text will use the regular font.

There are no BBCode tags to control vertical centering of text yet.

Options can be skipped for all tags.

left (or l), center (or c), right (or r), fill (or f)

Text horizontal alignment.

default (of d), uri (or u), file (or f), email (or e), list (or l), none (or n), custom (or c)

Structured text override.

justification_flags, jst

Comma-separated list of the following values (no space after each comma): kashida (or k), word (or w), trim (or tr), after_last_tab (or lt), skip_last (or sl), skip_last_with_chars (or sv), do_not_skip_single (or ns).

word,kashida,skip_last,do_not_skip_single

Justification (fill alignment) option. See TextServer for more details.

ltr (or l), rtl (or r), auto (or a)

ISO language codes. See Locale codes

Locale override. Some font files may contain script-specific substitutes, in which case they will be used.

List of floating-point numbers, e.g. 10.0,30.0

Width of the space character in the font

Overrides the horizontal offsets for each tab character. When the end of the list is reached, the tab stops will loop over. For example, if you set tab_stops to 10.0,30.0, the first tab will be at 10 pixels, the second tab will be at 10 + 30 = 40 pixels, and the third tab will be at 10 + 30 + 10 = 50 pixels from the origin of the RichTextLabel.

By default, [url] tags do nothing when clicked. This is to allow flexible use of [url] tags rather than limiting them to opening URLs in a web browser.

To handle clicked [url] tags, connect the RichTextLabel node's meta_clicked signal to a script function.

For example, the following method can be connected to meta_clicked to open clicked URLs using the user's default web browser:

For more advanced use cases, it's also possible to store JSON in a [url] tag's option and parse it in the function that handles the meta_clicked signal. For example:

Color name or color in HEX format

Color tint of the rule (modulation).

Target height of the rule in pixels, add % to the end of value to specify it as percentages of the control width instead of pixels.

Target width of the rule in pixels, add % to the end of value to specify it as percentages of the control width instead of pixels.

left (or l), center (or c), right (or r)

Horizontal alignment.

Color name or color in HEX format

Color tint of the image (modulation).

Target height of the image in pixels, add % to the end of value to specify it as percentages of the control width instead of pixels.

Target width of the image in pixels, add % to the end of value to specify it as percentages of the control width instead of pixels.

x,y,width,height in pixels

Region rect of the image. This can be used to display a single image from a spritesheet.

If set to true, and the image is smaller than the size specified by width and height, the image padding is added to match the size instead of upscaling.

When a vertical alignment value is provided with the [img] or [table] tag the image/table will try to align itself against the surrounding text. Alignment is performed using a vertical point of the image and a vertical point of the text. There are 3 possible points on the image (top, center, and bottom) and 4 possible points on the text and table (top, center, baseline, and bottom), which can be used in any combination.

To specify both points, use their full or short names as a value of the image/table tag:

You can also specify just one value (top, center, or bottom) to make use of a corresponding preset (top-top, center-center, and bottom-bottom respectively).

Short names for the values are t (top), c (center), l (baseline), and b (bottom).

A valid Font resource path.

Extra spacing for each glyph.

Extra spacing for the space character.

Extra spacing at the top of the line.

Extra spacing at the bottom of the line.

Floating-point number.

Font embolden strength, if it is not equal to zero, emboldens the font outlines. Negative values reduce the outline thickness.

An active face index in the TrueType / OpenType collection.

Floating-point number.

Font slant strength, positive values slant glyphs to the right. Negative values to the left.

opentype_variation, otv

Comma-separated list of the OpenType variation tags (no space after each comma).

Font OpenType variation coordinates. See OpenType variation tags.

Note: The value should be enclosed in " to allow using = inside it:

opentype_features, otf

Comma-separated list of the OpenType feature tags (no space after each comma).

Font OpenType features. See OpenType features tags.

Note: The value should be enclosed in " to allow using = inside it:

For tags that allow specifying a color by name, you can use names of the constants from the built-in Color class. Named classes can be specified in a number of styles using different casings: DARK_RED, DarkRed, and darkred will give the same exact result.

See this image for a list of color constants:

For opaque RGB colors, any valid 6-digit hexadecimal code is supported, e.g. [color=#ffffff]white[/color]. Shorthand RGB color codes such as #6f2 (equivalent to #66ff22) are also supported.

For transparent RGB colors, any RGBA 8-digit hexadecimal code can be used, e.g. [color=#ffffff88]translucent white[/color]. Note that the alpha channel is the last component of the color code, not the first one. Short RGBA color codes such as #6f28 (equivalent to #66ff2288) are supported as well.

Cell expansion ratio. This defines which cells will try to expand to proportionally to other cells and their expansion ratios.

Color name or color in HEX format

Color name or color in HEX format

Cell background color. For alternating odd/even row backgrounds, you can use bg=odd_color,even_color.

4 comma-separated floating-point numbers (no space after each comma)

Left, top, right, and bottom cell padding.

By default, the [ul] tag uses the U+2022 "Bullet" Unicode glyph as the bullet character. This behavior is similar to web browsers. The bullet character can be customized using [ul bullet={bullet}]. If provided, this {bullet} parameter must be a string with no enclosing quotes (for example, [bullet=*]). You can add trailing spaces after the bullet character to increase the spacing between the bullet and the list item text.

See Bullet (typography) on Wikipedia for a list of common bullet characters that you can paste directly in the bullet parameter.

Ordered lists can be used to automatically mark items with numbers or letters in ascending order. This tag supports the following type options:

1 - Numbers, using language specific numbering system if possible.

a, A - Lower and upper case Latin letters.

i, I - Lower and upper case Roman numerals.

BBCode can also be used to create different text effects that can optionally be animated. Five customizable effects are provided out of the box, and you can easily create your own. By default, animated effects will pause when the SceneTree is paused. You can change this behavior by adjusting the RichTextLabel's Process > Mode property.

All examples below mention the default values for options in the listed tag format.

Text effects that move characters' positions may result in characters being clipped by the RichTextLabel node bounds.

You can resolve this by disabling Control > Layout > Clip Contents in the inspector after selecting the RichTextLabel node, or ensuring there is enough margin added around the text by using line breaks above and below the line using the effect.

Pulse creates an animated pulsing effect that multiplies each character's opacity and color. It can be used to bring attention to specific text. Its tag format is [pulse freq=1.0 color=#ffffff40 ease=-2.0]{text}[/pulse].

freq controls the frequency of the half-pulsing cycle (higher is faster). A full pulsing cycle takes 2 * (1.0 / freq) seconds. color is the target color multiplier for blinking. The default mostly fades out text, but not entirely. ease is the easing function exponent to use. Negative values provide in-out easing, which is why the default is -2.0.

Wave makes the text go up and down. Its tag format is [wave amp=50.0 freq=5.0 connected=1]{text}[/wave].

amp controls how high and low the effect goes, and freq controls how fast the text goes up and down. A freq value of 0 will result in no visible waves, and negative freq values won't display any waves either. If connected is 1 (default), glyphs with ligatures will be moved together. If connected is 0, each glyph is moved individually even if they are joined by ligatures. This can work around certain rendering issues with font ligatures.

Tornado makes the text move around in a circle. Its tag format is [tornado radius=10.0 freq=1.0 connected=1]{text}[/tornado].

radius is the radius of the circle that controls the offset, freq is how fast the text moves in a circle. A freq value of 0 will pause the animation, while negative freq will play the animation backwards. If connected is 1 (default), glyphs with ligatures will be moved together. If connected is 0, each glyph is moved individually even if they are joined by ligatures. This can work around certain rendering issues with font ligatures.

Shake makes the text shake. Its tag format is [shake rate=20.0 level=5 connected=1]{text}[/shake].

rate controls how fast the text shakes, level controls how far the text is offset from the origin. If connected is 1 (default), glyphs with ligatures will be moved together. If connected is 0, each glyph is moved individually even if they are joined by ligatures. This can work around certain rendering issues with font ligatures.

Fade creates a static fade effect that multiplies each character's opacity. Its tag format is [fade start=4 length=14]{text}[/fade].

start controls the starting position of the falloff relative to where the fade command is inserted, length controls over how many characters should the fade out take place.

Rainbow gives the text a rainbow color that changes over time. Its tag format is [rainbow freq=1.0 sat=0.8 val=0.8 speed=1.0]{text}[/rainbow].

freq determines how many letters the rainbow extends over before it repeats itself, sat is the saturation of the rainbow, val is the value of the rainbow. speed is the number of full rainbow cycles per second. A positive speed value will play the animation forwards, a value of 0 will pause the animation, and a negative speed value will play the animation backwards.

Font outlines are not affected by the rainbow effect (they keep their original color). Existing font colors are overridden by the rainbow effect. However, CanvasItem's Modulate and Self Modulate properties will affect how the rainbow effect looks, as modulation multiplies its final colors.

You can extend the RichTextEffect resource type to create your own custom BBCode tags. Create a new script file that extends the RichTextEffect resource type and give the script a class_name so that the effect can be selected in the inspector. Add the @tool annotation to your GDScript file if you wish to have these custom effects run within the editor itself. The RichTextLabel does not need to have a script attached, nor does it need to be running in tool mode. The new effect can be registered in the Inspector by adding it to the Markup > Custom Effects array, or in code with the install_effect() method:

Selecting a custom RichTextEffect after saving a script that extends RichTextEffect with a class_name

If the custom effect is not registered within the RichTextLabel's Markup > Custom Effects property, no effect will be visible and the original tag will be left as-is.

There is only one function that you need to extend: _process_custom_fx(char_fx). Optionally, you can also provide a custom BBCode identifier by adding a member name bbcode. The code will check the bbcode property automatically or will use the name of the file to determine what the BBCode tag should be.

This is where the logic of each effect takes place and is called once per glyph during the draw phase of text rendering. This passes in a CharFXTransform object, which holds a few variables to control how the associated glyph is rendered:

outline is true if effect is called for drawing text outline.

range tells you how far into a given custom effect block you are in as an index.

elapsed_time is the total amount of time the text effect has been running.

visible will tell you whether the glyph is visible or not and will also allow you to hide a given portion of text.

offset is an offset position relative to where the given glyph should render under normal circumstances.

color is the color of a given glyph.

glyph_index and font is glyph being drawn and font data resource used to draw it.

Finally, env is a Dictionary of parameters assigned to a given custom effect. You can use get() with an optional default value to retrieve each parameter, if specified by the user. For example [custom_fx spread=0.5 color=#FFFF00]test[/custom_fx] would have a float spread and Color color parameters in its env Dictionary. See below for more usage examples.

The last thing to note about this function is that it is necessary to return a boolean true value to verify that the effect processed correctly. This way, if there's a problem with rendering a given glyph, it will back out of rendering custom effects entirely until the user fixes whatever error cropped up in their custom effect logic.

Here are some examples of custom effects:

This will add a few new BBCode commands, which can be used like so:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (json):
```json
[tag]content[/tag]
[tag=value]content[/tag]
[tag option1=value1 option2=value2]content[/tag]
[tag][/tag]
[tag]
```

Example 2 (json):
```json
[b]bold[i]bold italic[/b]italic[/i]
```

Example 3 (json):
```json
[b]bold[i]bold italic[/i][/b][i]italic[/i]
```

Example 4 (gdscript):
```gdscript
extends RichTextLabel

func _ready():
    append_chat_line("Player 1", "Hello world!")
    append_chat_line("Player 2", "Hello [color=red]BBCode injection[/color] (no escaping)!")
    append_chat_line_escaped("Player 2", "Hello [color=red]BBCode injection[/color] (with escaping)!")


# Returns escaped BBCode that won't be parsed by RichTextLabel as tags.
func escape_bbcode(bbcode_text):
    # We only need to replace opening brackets to prevent tags from being parsed.
    return bbcode_text.replace("[", "[lb]")


# Appends the user's message as-is, without escaping. This is dangerous!
func append_chat_line(username, message):
    append_text("%s: [color=green]%s[/color]\n" % [username, message])


# Appends the user's message with escaping.
# Remember to escape both the player name and message contents.
func append_chat_line_escaped(username, message):
    append_text("%s: [color=green]%s[/color]\n" % [escape_bbcode(username), escape_bbcode(message)])
```

---

## BoxContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_boxcontainer.html

**Contents:**
- BoxContainer
- Description
- Tutorials
- Properties
- Methods
- Theme Properties
- Enumerations
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions

Inherits: Container < Control < CanvasItem < Node < Object

Inherited By: HBoxContainer, VBoxContainer

A container that arranges its child controls horizontally or vertically.

A container that arranges its child controls horizontally or vertically, rearranging them automatically when their minimum size changes.

add_spacer(begin: bool)

enum AlignmentMode: 🔗

AlignmentMode ALIGNMENT_BEGIN = 0

The child controls will be arranged at the beginning of the container, i.e. top if orientation is vertical, left if orientation is horizontal (right for RTL layout).

AlignmentMode ALIGNMENT_CENTER = 1

The child controls will be centered in the container.

AlignmentMode ALIGNMENT_END = 2

The child controls will be arranged at the end of the container, i.e. bottom if orientation is vertical, right if orientation is horizontal (left for RTL layout).

AlignmentMode alignment = 0 🔗

void set_alignment(value: AlignmentMode)

AlignmentMode get_alignment()

The alignment of the container's children (must be one of ALIGNMENT_BEGIN, ALIGNMENT_CENTER, or ALIGNMENT_END).

bool vertical = false 🔗

void set_vertical(value: bool)

If true, the BoxContainer will arrange its children vertically, rather than horizontally.

Can't be changed when using HBoxContainer and VBoxContainer.

Control add_spacer(begin: bool) 🔗

Adds a Control node to the box as a spacer. If begin is true, it will insert the Control node in front of all other children.

The space between the BoxContainer's elements, in pixels.

Please read the User-contributed notes policy before submitting a comment.

---

## Built-in functions

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/shader_reference/shader_functions.html

**Contents:**
- Built-in functions
- Trigonometric functions
  - Trigonometric function descriptions
- Exponential and math functions
  - Exponential and math function descriptions
- Geometric functions
  - Geometric function descriptions
- Comparison functions
  - Comparison function descriptions
- Texture functions

Godot supports a large number of built-in functions, conforming roughly to the GLSL ES 3.0 specification.

The following type aliases only used in documentation to reduce repetitive function declarations. They can each refer to any of several actual types.

glsl documentation alias

float, vec2, vec3, or vec4

int, ivec2, ivec3, or ivec4

uint, uvec2, uvec3, or uvec4

bool, bvec2, bvec3, or bvec4

vec4, ivec4, or uvec4

sampler2D, isampler2D, or uSampler2D

sampler2DArray, isampler2DArray, or uSampler2DArray

sampler3D, isampler3D, or uSampler3D

If any of these are specified for multiple parameters, they must all be the same type unless otherwise noted.

Many functions that accept one or more vectors or matrices perform the described function on each component of the vector/matrix. Some examples:

Equivalent Scalar Operation

vec2(sqrt(4), sqrt(64))

vec2(min(3, 1), min(4, 1))

min(vec3(1, 2, 3),vec3(5, 1, 3))

vec3(min(1, 5), min(2, 1), min(3, 3))

pow(vec3(3, 8, 5 ), 2)

vec3(pow(3, 2), pow(8, 2), pow(5, 2))

pow(vec3(3, 8, 5), vec3(1, 2, 4))

vec3(pow(3, 1), pow(8, 2), pow(5, 4))

The GLSL Language Specification says under section 5.10 Vector and Matrix Operations:

With a few exceptions, operations are component-wise. Usually, when an operator operates on a vector or matrix, it is operating independently on each component of the vector or matrix, in a component-wise fashion. [...] The exceptions are matrix multiplied by vector, vector multiplied by matrix, and matrix multiplied by matrix. These do not operate component-wise, but rather perform the correct linear algebraic multiply.

These function descriptions are adapted and modified from official OpenGL documentation originally published by Khronos Group under the Open Publication License. Each function description links to the corresponding official OpenGL documentation. Modification history for this page can be found on GitHub.

Description / Return value

radians(vec_type degrees)

Convert degrees to radians.

degrees(vec_type radians)

Convert radians to degrees.

Arc hyperbolic cosine.

Arc hyperbolic tangent.

vec_type radians(vec_type degrees) 🔗

Component-wise Function.

Converts a quantity specified in degrees into radians, with the formula degrees * (PI / 180).

The quantity, in degrees, to be converted to radians.

The input degrees converted to radians.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/radians.xhtml

vec_type degrees(vec_type radians) 🔗

Component-wise Function.

Converts a quantity specified in radians into degrees, with the formula radians * (180 / PI)

The quantity, in radians, to be converted to degrees.

The input radians converted to degrees.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/degrees.xhtml

vec_type sin(vec_type angle) 🔗

Component-wise Function.

Returns the trigonometric sine of angle.

The quantity, in radians, of which to return the sine.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/sin.xhtml

vec_type cos(vec_type angle) 🔗

Component-wise Function.

Returns the trigonometric cosine of angle.

The quantity, in radians, of which to return the cosine.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/cos.xhtml

vec_type tan(vec_type angle) 🔗

Component-wise Function.

Returns the trigonometric tangent of angle.

The quantity, in radians, of which to return the tangent.

The tangent of angle.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/tan.xhtml

vec_type asin(vec_type x) 🔗

Component-wise Function.

Arc sine, or inverse sine. Calculates the angle whose sine is x and is in the range [-PI/2, PI/2]. The result is undefined if x < -1 or x > 1.

The value whose arc sine to return.

The angle whose trigonometric sine is x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/asin.xhtml

vec_type acos(vec_type x) 🔗

Component-wise Function.

Arc cosine, or inverse cosine. Calculates the angle whose cosine is x and is in the range [0, PI].

The result is undefined if x < -1 or x > 1.

The value whose arc cosine to return.

The angle whose trigonometric cosine is x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/acos.xhtml

vec_type atan(vec_type y_over_x) 🔗

Component-wise Function.

Calculates the arc tangent given a tangent value of y/x.

Because of the sign ambiguity, the function cannot determine with certainty in which quadrant the angle falls only by its tangent value. If you need to know the quadrant, use atan(vec_type y, vec_type x).

The fraction whose arc tangent to return.

The trigonometric arc-tangent of y_over_x and is in the range [-PI/2, PI/2].

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/atan.xhtml

vec_type atan(vec_type y, vec_type x) 🔗

Component-wise Function.

Calculates the arc tangent given a numerator and denominator. The signs of y and x are used to determine the quadrant that the angle lies in. The result is undefined if x == 0.

Equivalent to atan2() in GDScript.

The numerator of the fraction whose arc tangent to return.

The denominator of the fraction whose arc tangent to return.

The trigonometric arc tangent of y/x and is in the range [-PI, PI].

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/atan.xhtml

vec_type sinh(vec_type x) 🔗

Component-wise Function.

Calculates the hyperbolic sine using (e^x - e^-x)/2.

The value whose hyperbolic sine to return.

The hyperbolic sine of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/sinh.xhtml

vec_type cosh(vec_type x) 🔗

Component-wise Function.

Calculates the hyperbolic cosine using (e^x + e^-x)/2.

The value whose hyperbolic cosine to return.

The hyperbolic cosine of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/cosh.xhtml

vec_type tanh(vec_type x) 🔗

Component-wise Function.

Calculates the hyperbolic tangent using sinh(x)/cosh(x).

The value whose hyperbolic tangent to return.

The hyperbolic tangent of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/tanh.xhtml

vec_type asinh(vec_type x) 🔗

Component-wise Function.

Calculates the arc hyperbolic sine of x, or the inverse of sinh.

The value whose arc hyperbolic sine to return.

The arc hyperbolic sine of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/asinh.xhtml

vec_type acosh(vec_type x) 🔗

Component-wise Function.

Calculates the arc hyperbolic cosine of x, or the non-negative inverse of cosh. The result is undefined if x < 1.

The value whose arc hyperbolic cosine to return.

The arc hyperbolic cosine of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/acosh.xhtml

vec_type atanh(vec_type x) 🔗

Component-wise Function.

Calculates the arc hyperbolic tangent of x, or the inverse of tanh. The result is undefined if abs(x) > 1.

The value whose arc hyperbolic tangent to return.

The arc hyperbolic tangent of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/atanh.xhtml

Description / Return value

pow(vec_type x, vec_type y)

Power (undefined if x < 0 or if x == 0 and y <= 0).

Natural (base-e) logarithm.

inversesqrt(vec_type x)

Absolute value (returns positive value if negative).

Returns 1.0 if positive, -1.0 if negative, 0.0 otherwise.

Returns 1 if positive, -1 if negative, 0 otherwise.

Rounds to the integer below.

Rounds to the nearest integer.

roundEven(vec_type x)

Rounds to the nearest even integer.

Rounds to the integer above.

Fractional (returns x - floor(x)).

Modulo (division remainder).

modf(vec_type x, out vec_type i)

Fractional of x, with i as integer part.

Lowest value between a and b.

Highest value between a and b.

Clamps x between min and max (inclusive).

Linear interpolate between a and b by c.

fma(vec_type a, vec_type b, vec_type c)

Fused multiply-add operation: (a * b + c)

Hermite interpolate between a and b by c.

Returns true if scalar or vector component is NaN.

Returns true if scalar or vector component is INF.

floatBitsToInt(vec_type x)

float to int bit copying, no conversion.

floatBitsToUint(vec_type x)

float to uint bit copying, no conversion.

intBitsToFloat(vec_int_type x)

int to float bit copying, no conversion.

uintBitsToFloat(vec_uint_type x)

uint to float bit copying, no conversion.

vec_type pow(vec_type x, vec_type y) 🔗

Component-wise Function.

Raises x to the power of y.

The result is undefined if x < 0 or if x == 0 and y <= 0.

The value to be raised to the power y.

The power to which x will be raised.

The value of x raised to the y power.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/pow.xhtml

vec_type exp(vec_type x) 🔗

Component-wise Function.

Raises e to the power of x, or the the natural exponentiation.

Equivalent to pow(e, x).

The value to exponentiate.

The natural exponentiation of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/exp.xhtml

vec_type exp2(vec_type x) 🔗

Component-wise Function.

Raises 2 to the power of x.

Equivalent to pow(2.0, x).

The value of the power to which 2 will be raised.

2 raised to the power of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/exp2.xhtml

vec_type log(vec_type x) 🔗

Component-wise Function.

Returns the natural logarithm of x, i.e. the value y which satisfies x == pow(e, y). The result is undefined if x <= 0.

The value of which to take the natural logarithm.

The natural logarithm of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/log.xhtml

vec_type log2(vec_type x) 🔗

Component-wise Function.

Returns the base-2 logarithm of x, i.e. the value y which satisfies x == pow(2, y). The result is undefined if x <= 0.

The value of which to take the base-2 logarithm.

The base-2 logarithm of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/log2.xhtml

vec_type sqrt(vec_type x) 🔗

Component-wise Function.

Returns the square root of x. The result is undefined if x < 0.

The value of which to take the square root.

The square root of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/sqrt.xhtml

vec_type inversesqrt(vec_type x) 🔗

Component-wise Function.

Returns the inverse of the square root of x, or 1.0 / sqrt(x). The result is undefined if x <= 0.

The value of which to take the inverse of the square root.

The inverse of the square root of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/inversesqrt.xhtml

vec_type abs(vec_type x) 🔗

vec_int_type abs(vec_int_type x) 🔗

Component-wise Function.

Returns the absolute value of x. Returns x if x is positive, otherwise returns -1 * x.

The value of which to return the absolute.

The absolute value of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/abs.xhtml

vec_type sign(vec_type x) 🔗

vec_int_type sign(vec_int_type x) 🔗

Component-wise Function.

Returns -1 if x < 0, 0 if x == 0, and 1 if x > 0.

The value from which to extract the sign.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/sign.xhtml

vec_type floor(vec_type x) 🔗

Component-wise Function.

Returns a value equal to the nearest integer that is less than or equal to x.

The nearest integer that is less than or equal to x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/floor.xhtml

vec_type round(vec_type x) 🔗

Component-wise Function.

Rounds x to the nearest integer.

Rounding of values with a fractional part of 0.5 is implementation-dependent. This includes the possibility that round(x) returns the same value as roundEven(x)``for all values of ``x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/round.xhtml

vec_type roundEven(vec_type x) 🔗

Component-wise Function.

Rounds x to the nearest integer. A value with a fractional part of 0.5 will always round toward the nearest even integer. For example, both 3.5 and 4.5 will round to 4.0.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/roundEven.xhtml

vec_type trunc(vec_type x) 🔗

Component-wise Function.

Truncates x. Returns a value equal to the nearest integer to x whose absolute value is not larger than the absolute value of x.

The value to evaluate.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/trunc.xhtml

vec_type ceil(vec_type x) 🔗

Component-wise Function.

Returns a value equal to the nearest integer that is greater than or equal to x.

The value to evaluate.

The ceiling-ed value.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/ceil.xhtml

vec_type fract(vec_type x) 🔗

Component-wise Function.

Returns the fractional part of x.

This is calculated as x - floor(x).

The value to evaluate.

The fractional part of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/fract.xhtml

vec_type mod(vec_type x, vec_type y) 🔗

vec_type mod(vec_type x, float y) 🔗

Component-wise Function.

Returns the value of x modulo y. This is also sometimes called the remainder.

This is computed as x - y * floor(x/y).

The value to evaluate.

The value of x modulo y.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/mod.xhtml

vec_type modf(vec_type x, out vec_type i) 🔗

Component-wise Function.

Separates a floating-point value x into its integer and fractional parts.

The fractional part of the number is returned from the function. The integer part (as a floating-point quantity) is returned in the output parameter i.

The value to separate.

A variable that receives the integer part of x.

The fractional part of the number.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/modf.xhtml

vec_type min(vec_type a, vec_type b) 🔗

vec_type min(vec_type a, float b) 🔗

vec_int_type min(vec_int_type a, vec_int_type b) 🔗

vec_int_type min(vec_int_type a, int b) 🔗

vec_uint_type min(vec_uint_type a, vec_uint_type b) 🔗

vec_uint_type min(vec_uint_type a, uint b) 🔗

Component-wise Function.

Returns the minimum of two values a and b.

Returns b if b < a, otherwise returns a.

The first value to compare.

The second value to compare.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/min.xhtml

vec_type max(vec_type a, vec_type b) 🔗

vec_type max(vec_type a, float b) 🔗

vec_uint_type max(vec_uint_type a, vec_uint_type b) 🔗

vec_uint_type max(vec_uint_type a, uint b) 🔗

vec_int_type max(vec_int_type a, vec_int_type b) 🔗

vec_int_type max(vec_int_type a, int b) 🔗

Component-wise Function.

Returns the maximum of two values a and b.

It returns b if b > a, otherwise it returns a.

The first value to compare.

The second value to compare.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/max.xhtml

vec_type clamp(vec_type x, vec_type minVal, vec_type maxVal) 🔗

vec_type clamp(vec_type x, float minVal, float maxVal) 🔗

vec_int_type clamp(vec_int_type x, vec_int_type minVal, vec_int_type maxVal) 🔗

vec_int_type clamp(vec_int_type x, int minVal, int maxVal) 🔗

vec_uint_type clamp(vec_uint_type x, vec_uint_type minVal, vec_uint_type maxVal) 🔗

vec_uint_type clamp(vec_uint_type x, uint minVal, uint maxVal) 🔗

Component-wise Function.

Returns the value of x constrained to the range minVal to maxVal.

The returned value is computed as min(max(x, minVal), maxVal).

The value to constrain.

The lower end of the range into which to constrain x.

The upper end of the range into which to constrain x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/clamp.xhtml

vec_type mix(vec_type a, vec_type b, vec_type c) 🔗

vec_type mix(vec_type a, vec_type b, float c) 🔗

Component-wise Function.

Performs a linear interpolation between a and b using c to weight between them.

Computed as a * (1 - c) + b * c.

Equivalent to lerp() in GDScript.

The start of the range in which to interpolate.

The end of the range in which to interpolate.

The value to use to interpolate between a and b.

The interpolated value.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/mix.xhtml

vec_type mix(vec_type a, vec_type b, vec_bool_type c) 🔗

Selects either value a or value b based on the value of c. For a component of c that is false, the corresponding component of a is returned. For a component of c that is true, the corresponding component of b is returned. Components of a and b that are not selected are allowed to be invalid floating-point values and will have no effect on the results.

If a, b, and c are vector types the operation is performed component-wise. ie. mix(vec2(42, 314), vec2(9.8, 6e23), bvec2(true, false))) will return vec2(9.8, 314).

Value returned when c is false.

Value returned when c is true.

The value used to select between a and b.

The interpolated value.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/mix.xhtml

vec_type fma(vec_type a, vec_type b, vec_type c) 🔗

Component-wise Function.

Performs, where possible, a fused multiply-add operation, returning a * b + c. In use cases where the return value is eventually consumed by a variable declared as precise:

fma() is considered a single operation, whereas the expression a * b + c consumed by a variable declared as precise is considered two operations.

The precision of fma() can differ from the precision of the expression a * b + c.

fma() will be computed with the same precision as any other fma() consumed by a precise variable, giving invariant results for the same input values of a, b and c.

Otherwise, in the absence of precise consumption, there are no special constraints on the number of operations or difference in precision between fma() and the expression a * b + c.

The first value to be multiplied.

The second value to be multiplied.

The value to be added to the result.

The value of a * b + c.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/fma.xhtml

vec_type step(vec_type a, vec_type b) 🔗

vec_type step(float a, vec_type b) 🔗

Component-wise Function.

Generates a step function by comparing b to a.

Equivalent to if (b < a) { return 0.0; } else { return 1.0; }. For element i of the return value, 0.0 is returned if b[i] < a[i], and 1.0 is returned otherwise.

The location of the edge of the step function.

The value to be used to generate the step function.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/step.xhtml

vec_type smoothstep(vec_type a, vec_type b, vec_type c) 🔗

vec_type smoothstep(float a, float b, vec_type c) 🔗

Component-wise Function.

Performs smooth Hermite interpolation between 0 and 1 when a < c < b. This is useful in cases where a threshold function with a smooth transition is desired.

Smoothstep is equivalent to:

Results are undefined if a >= b.

The value of the lower edge of the Hermite function.

The value of the upper edge of the Hermite function.

The source value for interpolation.

The interpolated value.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/smoothstep.xhtml

vec_bool_type isnan(vec_type x) 🔗

Component-wise Function.

For each element i of the result, returns true if x[i] is positive or negative floating-point NaN (Not a Number) and false otherwise.

The value to test for NaN.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/isnan.xhtml

vec_bool_type isinf(vec_type x) 🔗

Component-wise Function.

For each element i of the result, returns true if x[i] is positive or negative floating-point infinity and false otherwise.

The value to test for infinity.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/isinf.xhtml

vec_int_type floatBitsToInt(vec_type x) 🔗

Component-wise Function.

Returns the encoding of the floating-point parameters as int.

The floating-point bit-level representation is preserved.

The value whose floating-point encoding to return.

The floating-point encoding of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/floatBitsToInt.xhtml

vec_uint_type floatBitsToUint(vec_type x) 🔗

Component-wise Function.

Returns the encoding of the floating-point parameters as uint.

The floating-point bit-level representation is preserved.

The value whose floating-point encoding to return.

The floating-point encoding of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/floatBitsToInt.xhtml

vec_type intBitsToFloat(vec_int_type x) 🔗

Component-wise Function.

Converts a bit encoding to a floating-point value. Opposite of floatBitsToInt<shader_func_floatBitsToInt>

If the encoding of a NaN is passed in x, it will not signal and the resulting value will be undefined.

If the encoding of a floating-point infinity is passed in parameter x, the resulting floating-point value is the corresponding (positive or negative) floating-point infinity.

The bit encoding to return as a floating-point value.

A floating-point value.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/intBitsToFloat.xhtml

vec_type uintBitsToFloat(vec_uint_type x) 🔗

Component-wise Function.

Converts a bit encoding to a floating-point value. Opposite of floatBitsToUint<shader_func_floatBitsToUint>

If the encoding of a NaN is passed in x, it will not signal and the resulting value will be undefined.

If the encoding of a floating-point infinity is passed in parameter x, the resulting floating-point value is the corresponding (positive or negative) floating-point infinity.

The bit encoding to return as a floating-point value.

A floating-point value.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/intBitsToFloat.xhtml

distance(vec_type a, vec_type b)

Distance between vectors i.e length(a - b).

dot(vec_type a, vec_type b)

cross(vec3 a, vec3 b)

normalize(vec_type x)

Normalize to unit length.

reflect(vec3 I, vec3 N)

refract(vec3 I, vec3 N, float eta)

faceforward(vec_type N, vec_type I, vec_type Nref)

If dot(Nref, I) < 0, return N, otherwise -N.

matrixCompMult(mat_type x, mat_type y)

Matrix component multiplication.

outerProduct(vec_type column, vec_type row)

Matrix outer product.

transpose(mat_type m)

determinant(mat_type m)

float length(vec_type x) 🔗

Returns the length of the vector. ie. sqrt(x[0] * x[0] + x[1] * x[1] + ... + x[n] * x[n])

The length of the vector.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/length.xhtml

float distance(vec_type a, vec_type b) 🔗

Returns the distance between the two points a and b.

The scalar distance between the points

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/distance.xhtml

float dot(vec_type a, vec_type b) 🔗

Returns the dot product of two vectors, a and b. i.e., a.x * b.x + a.y * b.y + ...

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/dot.xhtml

vec3 cross(vec3 a, vec3 b) 🔗

Returns the cross product of two vectors. i.e.:

The cross product of a and b.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/cross.xhtml

vec_type normalize(vec_type x) 🔗

Returns a vector with the same direction as x but with length 1.0.

The vector to normalize.

The normalized vector.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/normalize.xhtml

vec3 reflect(vec3 I, vec3 N) 🔗

Calculate the reflection direction for an incident vector.

For a given incident vector I and surface normal N reflect returns the reflection direction calculated as I - 2.0 * dot(N, I) * N.

N should be normalized in order to achieve the desired result.

The reflection vector.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/reflect.xhtml

vec3 refract(vec3 I, vec3 N, float eta) 🔗

Calculate the refraction direction for an incident vector.

For a given incident vector I, surface normal N and ratio of indices of refraction, eta, refract returns the refraction vector, R.

The input parameters I and N should be normalized in order to achieve the desired result.

The ratio of indices of refraction.

The refraction vector.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/refract.xhtml

vec_type faceforward(vec_type N, vec_type I, vec_type Nref) 🔗

Returns a vector pointing in the same direction as another.

Orients a vector to point away from a surface as defined by its normal. If dot(Nref, I) < 0 faceforward returns N, otherwise it returns -N.

The vector to orient.

The reference vector.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/faceforward.xhtml

mat_type matrixCompMult(mat_type x, mat_type y) 🔗

Perform a component-wise multiplication of two matrices.

Performs a component-wise multiplication of two matrices, yielding a result matrix where each component, result[i][j] is computed as the scalar product of x[i][j] and y[i][j].

The first matrix multiplicand.

The second matrix multiplicand.

The resultant matrix.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/matrixCompMult.xhtml

mat_type outerProduct(vec_type column, vec_type row) 🔗

Calculate the outer product of a pair of vectors.

Does a linear algebraic matrix multiply column * row, yielding a matrix whose number of rows is the number of components in column and whose number of columns is the number of components in row.

The column vector for multiplication.

The row vector for multiplication.

The outer product matrix.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/outerProduct.xhtml

mat_type transpose(mat_type m) 🔗

Calculate the transpose of a matrix.

The matrix to transpose.

A new matrix that is the transpose of the input matrix m.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/transpose.xhtml

float determinant(mat_type m) 🔗

Calculate the determinant of a matrix.

The determinant of the input matrix m.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/determinant.xhtml

mat_type inverse(mat_type m) 🔗

Calculate the inverse of a matrix.

The values in the returned matrix are undefined if m is singular or poorly-conditioned (nearly singular).

The matrix of which to take the inverse.

A new matrix which is the inverse of the input matrix m.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/inverse.xhtml

lessThan(vec_type x, vec_type y)

Bool vector comparison on < int/uint/float vectors.

greaterThan(vec_type x, vec_type y)

Bool vector comparison on > int/uint/float vectors.

lessThanEqual(vec_type x, vec_type y)

Bool vector comparison on <= int/uint/float vectors.

greaterThanEqual( vec_type x, vec_type y)

Bool vector comparison on >= int/uint/float vectors.

equal(vec_type x, vec_type y)

Bool vector comparison on == int/uint/float vectors.

notEqual(vec_type x, vec_type y)

Bool vector comparison on != int/uint/float vectors.

true if any component is true, false otherwise.

true if all components are true, false otherwise.

Invert boolean vector.

vec_bool_type lessThan(vec_type x, vec_type y) 🔗

Performs a component-wise less-than comparison of two vectors.

The first vector to compare.

The second vector to compare.

A boolean vector in which each element i is computed as x[i] < y[i].

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/lessThan.xhtml

vec_bool_type greaterThan(vec_type x, vec_type y) 🔗

Performs a component-wise greater-than comparison of two vectors.

The first vector to compare.

The second vector to compare.

A boolean vector in which each element i is computed as x[i] > y[i].

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/greaterThan.xhtml

vec_bool_type lessThanEqual(vec_type x, vec_type y) 🔗

Performs a component-wise less-than-or-equal comparison of two vectors.

The first vector to compare.

The second vector to compare.

A boolean vector in which each element i is computed as x[i] <= y[i].

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/lessThanEqual.xhtml

vec_bool_type greaterThanEqual(vec_type x, vec_type y) 🔗

Performs a component-wise greater-than-or-equal comparison of two vectors.

The first vector to compare.

The second vector to compare.

A boolean vector in which each element i is computed as x[i] >= y[i].

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/greaterThanEqual.xhtml

vec_bool_type equal(vec_type x, vec_type y) 🔗

Performs a component-wise equal-to comparison of two vectors.

The first vector to compare.

The second vector to compare.

A boolean vector in which each element i is computed as x[i] == y[i].

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/equal.xhtml

vec_bool_type notEqual(vec_type x, vec_type y) 🔗

Performs a component-wise not-equal-to comparison of two vectors.

The first vector for comparison.

The second vector for comparison.

A boolean vector in which each element i is computed as x[i] != y[i].

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/notEqual.xhtml

bool any(vec_bool_type x) 🔗

Returns true if any element of a boolean vector is true, false otherwise.

Functionally equivalent to:

The vector to be tested for truth.

True if any element of x is true and false otherwise.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/any.xhtml

bool all(vec_bool_type x) 🔗

Returns true if all elements of a boolean vector are true, false otherwise.

Functionally equivalent to:

The vector to be tested for truth.

true if all elements of x are true and false otherwise.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/all.xhtml

vec_bool_type not(vec_bool_type x) 🔗

Logically invert a boolean vector.

The vector to be inverted.

A new boolean vector for which each element i is computed as !x[i].

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/not.xhtml

Get the size of a texture.

Compute the level-of-detail that would be used to sample from a texture.

Get the number of accessible mipmap levels of a texture.

Performs a texture read.

Performs a texture read with projection.

Performs a texture read at custom mipmap.

Performs a texture read with projection/LOD.

Performs a texture read with explicit gradients.

Performs a texture read with projection/LOD and with explicit

Fetches a single texel using integer coordinates.

Gathers four texels from a texture.

Derivative with respect to x window coordinate, automatic granularity.

dFdxCoarse(vec_type p)

Derivative with respect to x window coordinate, course granularity.

Not available when using the Compatibility renderer.

Derivative with respect to x window coordinate, fine granularity.

Not available when using the Compatibility renderer.

Derivative with respect to y window coordinate, automatic granularity.

dFdyCoarse(vec_type p)

Derivative with respect to y window coordinate, course granularity.

Not available when using the Compatibility renderer.

Derivative with respect to y window coordinate, fine granularity.

Not available when using the Compatibility renderer.

Sum of absolute derivative in x and y.

fwidthCoarse(vec_type p)

Sum of absolute derivative in x and y.

Not available when using the Compatibility renderer.

fwidthFine(vec_type p)

Sum of absolute derivative in x and y.

Not available when using the Compatibility renderer.

ivec2 textureSize(gsampler2D s, int lod) 🔗

ivec2 textureSize(samplerCube s, int lod) 🔗

ivec2 textureSize(samplerCubeArray s, int lod) 🔗

ivec3 textureSize(gsampler2DArray s, int lod) 🔗

ivec3 textureSize(gsampler3D s, int lod) 🔗

Retrieves the dimensions of a level of a texture.

Returns the dimensions of level lod (if present) of the texture bound to sampler.

The components in the return value are filled in, in order, with the width, height and depth of the texture. For the array forms, the last component of the return value is the number of layers in the texture array.

The sampler to which the texture whose dimensions to retrieve is bound.

The level of the texture for which to retrieve the dimensions.

The dimensions of level lod (if present) of the texture bound to sampler.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureSize.xhtml

vec2 textureQueryLod(gsampler2D s, vec2 p) 🔗

vec2 textureQueryLod(gsampler2DArray s, vec2 p) 🔗

vec2 textureQueryLod(gsampler3D s, vec3 p) 🔗

vec2 textureQueryLod(samplerCube s, vec3 p) 🔗

Available only in the fragment shader.

Compute the level-of-detail that would be used to sample from a texture.

The mipmap array(s) that would be accessed is returned in the x component of the return value. The computed level-of-detail relative to the base level is returned in the y component of the return value.

If called on an incomplete texture, the result of the operation is undefined.

The sampler to which the texture whose level-of-detail will be queried is bound.

The texture coordinates at which the level-of-detail will be queried.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureQueryLod.xhtml

int textureQueryLevels(gsampler2D s) 🔗

int textureQueryLevels(gsampler2DArray s) 🔗

int textureQueryLevels(gsampler3D s) 🔗

int textureQueryLevels(samplerCube s) 🔗

Compute the number of accessible mipmap levels of a texture.

If called on an incomplete texture, or if no texture is associated with sampler, 0 is returned.

The sampler to which the texture whose mipmap level count will be queried is bound.

The number of accessible mipmap levels in the texture, or 0.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureQueryLevels.xhtml

gvec4_type texture(gsampler2D s, vec2 p [, float bias] ) 🔗

gvec4_type texture(gsampler2DArray s, vec3 p [, float bias] ) 🔗

gvec4_type texture(gsampler3D s, vec3 p [, float bias] ) 🔗

vec4 texture(samplerCube s, vec3 p [, float bias] ) 🔗

vec4 texture(samplerCubeArray s, vec4 p [, float bias] ) 🔗

vec4 texture(samplerExternalOES s, vec2 p [, float bias] ) 🔗

Retrieves texels from a texture.

Samples texels from the texture bound to s at texture coordinate p. An optional bias, specified in bias is included in the level-of-detail computation that is used to choose mipmap(s) from which to sample.

For shadow forms, the last component of p is used as Dsub and the array layer is specified in the second to last component of p. (The second component of p is unused for 1D shadow lookups.)

For non-shadow variants, the array layer comes from the last component of P.

The sampler to which the texture from which texels will be retrieved is bound.

The texture coordinates at which texture will be sampled.

An optional bias to be applied during level-of-detail computation.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/texture.xhtml

gvec4_type textureProj(gsampler2D s, vec3 p [, float bias] ) 🔗

gvec4_type textureProj(gsampler2D s, vec4 p [, float bias] ) 🔗

gvec4_type textureProj(gsampler3D s, vec4 p [, float bias] ) 🔗

Perform a texture lookup with projection.

The texture coordinates consumed from p, not including the last component of p, are divided by the last component of p. The resulting 3rd component of p in the shadow forms is used as Dref. After these values are computed, the texture lookup proceeds as in texture.

The sampler to which the texture from which texels will be retrieved is bound.

The texture coordinates at which texture will be sampled.

Optional bias to be applied during level-of-detail computation.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureProj.xhtml

gvec4_type textureLod(gsampler2D s, vec2 p, float lod) 🔗

gvec4_type textureLod(gsampler2DArray s, vec3 p, float lod) 🔗

gvec4_type textureLod(gsampler3D s, vec3 p, float lod) 🔗

vec4 textureLod(samplerCube s, vec3 p, float lod) 🔗

vec4 textureLod(samplerCubeArray s, vec4 p, float lod) 🔗

Performs a texture lookup at coordinate p from the texture bound to sampler with an explicit level-of-detail as specified in lod. lod specifies λbase and sets the partial derivatives as follows:

The sampler to which the texture from which texels will be retrieved is bound.

The texture coordinates at which texture will be sampled.

The explicit level-of-detail.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureLod.xhtml

gvec4_type textureProjLod(gsampler2D s, vec3 p, float lod) 🔗

gvec4_type textureProjLod(gsampler2D s, vec4 p, float lod) 🔗

gvec4_type textureProjLod(gsampler3D s, vec4 p, float lod) 🔗

Performs a texture lookup with projection from an explicitly specified level-of-detail.

The texture coordinates consumed from P, not including the last component of p, are divided by the last component of p. The resulting 3rd component of p in the shadow forms is used as Dref. After these values are computed, the texture lookup proceeds as in textureLod<shader_func_textureLod>, with lod used to specify the level-of-detail from which the texture will be sampled.

The sampler to which the texture from which texels will be retrieved is bound.

The texture coordinates at which texture will be sampled.

The explicit level-of-detail from which to fetch texels.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureProjLod.xhtml

gvec4_type textureGrad(gsampler2D s, vec2 p, vec2 dPdx, vec2 dPdy) 🔗

gvec4_type textureGrad(gsampler2DArray s, vec3 p, vec2 dPdx, vec2 dPdy) 🔗

gvec4_type textureGrad(gsampler3D s, vec3 p, vec2 dPdx, vec2 dPdy) 🔗

vec4 textureGrad(samplerCube s, vec3 p, vec3 dPdx, vec3 dPdy) 🔗

vec4 textureGrad(samplerCubeArray s, vec3 p, vec3 dPdx, vec3 dPdy) 🔗

δs/δx=δp/δx for a 1D texture, δp.s/δx otherwise

δs/δy=δp/δy for a 1D texture, δp.s/δy otherwise

δt/δx=0.0 for a 1D texture, δp.t/δx otherwise

δt/δy=0.0 for a 1D texture, δp.t/δy otherwise

δr/δx=0.0 for a 1D or 2D texture, δp.p/δx otherwise

δr/δy=0.0 for a 1D or 2D texture, δp.p/δy otherwise

For the cube version, the partial derivatives of p are assumed to be in the coordinate system used before texture coordinates are projected onto the appropriate cube face.

The sampler to which the texture from which texels will be retrieved is bound.

The texture coordinates at which texture will be sampled.

The partial derivative of P with respect to window x.

The partial derivative of P with respect to window y.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureGrad.xhtml

gvec4_type textureProjGrad(gsampler2D s, vec3 p, vec2 dPdx, vec2 dPdy) 🔗

gvec4_type textureProjGrad(gsampler2D s, vec4 p, vec2 dPdx, vec2 dPdy) 🔗

gvec4_type textureProjGrad(gsampler3D s, vec4 p, vec3 dPdx, vec3 dPdy) 🔗

Perform a texture lookup with projection and explicit gradients.

The texture coordinates consumed from p, not including the last component of p, are divided by the last component of p. After these values are computed, the texture lookup proceeds as in textureGrad<shader_func_textureGrad>, passing dPdx and dPdy as gradients.

The sampler to which the texture from which texels will be retrieved is bound.

The texture coordinates at which texture will be sampled.

The partial derivative of p with respect to window x.

The partial derivative of p with respect to window y.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureProjGrad.xhtml

gvec4_type texelFetch(gsampler2D s, ivec2 p, int lod) 🔗

gvec4_type texelFetch(gsampler2DArray s, ivec3 p, int lod) 🔗

gvec4_type texelFetch(gsampler3D s, ivec3 p, int lod) 🔗

Performs a lookup of a single texel from texture coordinate p in the texture bound to sampler.

The sampler to which the texture from which texels will be retrieved is bound.

The texture coordinates at which texture will be sampled.

Specifies the level-of-detail within the texture from which the texel will be fetched.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/texelFetch.xhtml

gvec4_type textureGather(gsampler2D s, vec2 p [, int comps] ) 🔗

gvec4_type textureGather(gsampler2DArray s, vec3 p [, int comps] ) 🔗

vec4 textureGather(samplerCube s, vec3 p [, int comps] ) 🔗

Gathers four texels from a texture.

The sampler to which the texture from which texels will be retrieved is bound.

The texture coordinates at which texture will be sampled.

optional the component of the source texture (0 -> x, 1 -> y, 2 -> z, 3 -> w) that will be used to generate the resulting vector. Zero if not specified.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureGather.xhtml

vec_type dFdx(vec_type p) 🔗

Available only in the fragment shader.

Returns the partial derivative of p with respect to the window x coordinate using local differencing.

Returns either dFdxCoarse or dFdxFine. The implementation may choose which calculation to perform based upon factors such as performance or the value of the API GL_FRAGMENT_SHADER_DERIVATIVE_HINT hint.

Expressions that imply higher order derivatives such as dFdx(dFdx(n)) have undefined results, as do mixed-order derivatives such as dFdx(dFdy(n)).

The expression of which to take the partial derivative.

It is assumed that the expression p is continuous and therefore expressions evaluated via non-uniform control flow may be undefined.

The partial derivative of p.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/dFdx.xhtml

vec_type dFdxCoarse(vec_type p) 🔗

Available only in the fragment shader. Not available when using the Compatibility renderer.

Returns the partial derivative of p with respect to the window x coordinate.

Calculates derivatives using local differencing based on the value of p for the current fragment's neighbors, and will possibly, but not necessarily, include the value for the current fragment. That is, over a given area, the implementation can compute derivatives in fewer unique locations than would be allowed for the corresponding dFdxFine function.

Expressions that imply higher order derivatives such as dFdx(dFdx(n)) have undefined results, as do mixed-order derivatives such as dFdx(dFdy(n)).

The expression of which to take the partial derivative.

It is assumed that the expression p is continuous and therefore expressions evaluated via non-uniform control flow may be undefined.

The partial derivative of p.

https://registry.khronos.org/OpenGL-Refpages/gl4/html/dFdx.xhtml

vec_type dFdxFine(vec_type p) 🔗

Available only in the fragment shader. Not available when using the Compatibility renderer.

Returns the partial derivative of p with respect to the window x coordinate.

Calculates derivatives using local differencing based on the value of p for the current fragment and its immediate neighbor(s).

Expressions that imply higher order derivatives such as dFdx(dFdx(n)) have undefined results, as do mixed-order derivatives such as dFdx(dFdy(n)).

The expression of which to take the partial derivative.

It is assumed that the expression p is continuous and therefore expressions evaluated via non-uniform control flow may be undefined.

The partial derivative of p.

https://registry.khronos.org/OpenGL-Refpages/gl4/html/dFdx.xhtml

vec_type dFdy(vec_type p) 🔗

Available only in the fragment shader.

Returns the partial derivative of p with respect to the window y coordinate using local differencing.

Returns either dFdyCoarse or dFdyFine. The implementation may choose which calculation to perform based upon factors such as performance or the value of the API GL_FRAGMENT_SHADER_DERIVATIVE_HINT hint.

Expressions that imply higher order derivatives such as dFdx(dFdx(n)) have undefined results, as do mixed-order derivatives such as dFdx(dFdy(n)).

The expression of which to take the partial derivative.

It is assumed that the expression p is continuous and therefore expressions evaluated via non-uniform control flow may be undefined.

The partial derivative of p.

https://registry.khronos.org/OpenGL-Refpages/gl4/html/dFdx.xhtml

vec_type dFdyCoarse(vec_type p) 🔗

Available only in the fragment shader. Not available when using the Compatibility renderer.

Returns the partial derivative of p with respect to the window y coordinate.

Calculates derivatives using local differencing based on the value of p for the current fragment's neighbors, and will possibly, but not necessarily, include the value for the current fragment. That is, over a given area, the implementation can compute derivatives in fewer unique locations than would be allowed for the corresponding dFdyFine and dFdyFine functions.

Expressions that imply higher order derivatives such as dFdx(dFdx(n)) have undefined results, as do mixed-order derivatives such as dFdx(dFdy(n)).

The expression of which to take the partial derivative.

It is assumed that the expression p is continuous and therefore expressions evaluated via non-uniform control flow may be undefined.

The partial derivative of p.

https://registry.khronos.org/OpenGL-Refpages/gl4/html/dFdx.xhtml

vec_type dFdyFine(vec_type p) 🔗

Available only in the fragment shader. Not available when using the Compatibility renderer.

Returns the partial derivative of p with respect to the window y coordinate.

Calculates derivatives using local differencing based on the value of p for the current fragment and its immediate neighbor(s).

Expressions that imply higher order derivatives such as dFdx(dFdx(n)) have undefined results, as do mixed-order derivatives such as dFdx(dFdy(n)).

The expression of which to take the partial derivative.

It is assumed that the expression p is continuous and therefore expressions evaluated via non-uniform control flow may be undefined.

The partial derivative of p.

https://registry.khronos.org/OpenGL-Refpages/gl4/html/dFdx.xhtml

vec_type fwidth(vec_type p) 🔗

Returns the sum of the absolute value of derivatives in x and y.

Uses local differencing for the input argument p.

Equivalent to abs(dFdx(p)) + abs(dFdy(p)).

The expression of which to take the partial derivative.

The partial derivative.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/fwidth.xhtml

vec_type fwidthCoarse(vec_type p) 🔗

Available only in the fragment shader. Not available when using the Compatibility renderer.

Returns the sum of the absolute value of derivatives in x and y.

Uses local differencing for the input argument p.

Equivalent to abs(dFdxCoarse(p)) + abs(dFdyCoarse(p)).

The expression of which to take the partial derivative.

The partial derivative.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/fwidth.xhtml

vec_type fwidthFine(vec_type p) 🔗

Available only in the fragment shader. Not available when using the Compatibility renderer.

Returns the sum of the absolute value of derivatives in x and y.

Uses local differencing for the input argument p.

Equivalent to abs(dFdxFine(p)) + abs(dFdyFine(p)).

The expression of which to take the partial derivative.

The partial derivative.

https://registry.khronos.org/OpenGL-Refpages/gl4/html/fwidth.xhtml

These functions convert floating-point numbers into various sized integers and then pack those integers into a single 32bit unsigned integer. The 'unpack' functions perform the opposite operation, returning the original floating-point numbers.

Convert two 32-bit floats to 16 bit floats and pack them.

Convert two normalized (range 0..1) 32-bit floats to 16-bit unsigned ints and pack them.

Convert two signed normalized (range -1..1) 32-bit floats to 16-bit signed ints and pack them.

Convert four normalized (range 0..1) 32-bit floats into 8-bit unsigned ints and pack them.

Convert four signed normalized (range -1..1) 32-bit floats into 8-bit signed ints and pack them.

uint packHalf2x16(vec2 v) 🔗

Converts two 32-bit floating-point quantities to 16-bit floating-point quantities and packs them into a single 32-bit integer.

Returns an unsigned integer obtained by converting the components of a two-component floating-point vector to the 16-bit floating-point representation found in the OpenGL Specification, and then packing these two 16-bit integers into a 32-bit unsigned integer. The first vector component specifies the 16 least-significant bits of the result; the second component specifies the 16 most-significant bits.

A vector of two 32-bit floating-point values that are to be converted to 16-bit representation and packed into the result.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/packHalf2x16.xhtml

vec2 unpackHalf2x16(uint v) 🔗

Inverse of packHalf2x16.

Unpacks a 32-bit integer into two 16-bit floating-point values, converts them to 32-bit floating-point values, and puts them into a vector. The first component of the vector is obtained from the 16 least-significant bits of v; the second component is obtained from the 16 most-significant bits of v.

A single 32-bit unsigned integer containing 2 packed 16-bit floating-point values.

Two unpacked floating-point values.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/unpackHalf2x16.xhtml

uint packUnorm2x16(vec2 v) 🔗

Pack floating-point values into an unsigned integer.

Converts each component of the normalized floating-point value v into 16-bit integer values and then packs the results into a 32-bit unsigned integer.

The conversion for component c of v to fixed-point is performed as follows:

The first component of the vector will be written to the least significant bits of the output; the last component will be written to the most significant bits.

A vector of values to be packed into an unsigned integer.

Unsigned 32 bit integer containing the packed encoding of the vector.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/packUnorm.xhtml

vec2 unpackUnorm2x16(uint v) 🔗

Unpack floating-point values from an unsigned integer.

Unpack single 32-bit unsigned integers into a pair of 16-bit unsigned integers. Then, each component is converted to a normalized floating-point value to generate the returned two-component vector.

The conversion for unpacked fixed point value f to floating-point is performed as follows:

The first component of the returned vector will be extracted from the least significant bits of the input; the last component will be extracted from the most significant bits.

An unsigned integer containing packed floating-point values.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/unpackUnorm.xhtml

uint packSnorm2x16(vec2 v) 🔗

Packs floating-point values into an unsigned integer.

Convert each component of the normalized floating-point value v into 16-bit integer values and then packs the results into a 32-bit unsigned integer.

The conversion for component c of v to fixed-point is performed as follows:

The first component of the vector will be written to the least significant bits of the output; the last component will be written to the most significant bits.

A vector of values to be packed into an unsigned integer.

Unsigned 32 bit integer containing the packed encoding of the vector.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/packUnorm.xhtml

vec2 unpackSnorm2x16(uint v) 🔗

Unpacks floating-point values from an unsigned integer.

Unpacks single 32-bit unsigned integers into a pair of 16-bit signed integers. Then, each component is converted to a normalized floating-point value to generate the returned two-component vector.

The conversion for unpacked fixed point value f to floating-point is performed as follows:

clamp(f / 32727.0, -1.0, 1.0)

The first component of the returned vector will be extracted from the least significant bits of the input; the last component will be extracted from the most significant bits.

An unsigned integer containing packed floating-point values.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/unpackUnorm.xhtml

uint packUnorm4x8(vec4 v) 🔗

Packs floating-point values into an unsigned integer.

Converts each component of the normalized floating-point value v into 16-bit integer values and then packs the results into a 32-bit unsigned integer.

The conversion for component c of v to fixed-point is performed as follows:

The first component of the vector will be written to the least significant bits of the output; the last component will be written to the most significant bits.

A vector of values to be packed into an unsigned integer.

Unsigned 32 bit integer containing the packed encoding of the vector.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/packUnorm.xhtml

vec4 unpackUnorm4x8(uint v) 🔗

Unpacks floating-point values from an unsigned integer.

Unpacks single 32-bit unsigned integers into four 8-bit unsigned integers. Then, each component is converted to a normalized floating-point value to generate the returned four-component vector.

The conversion for unpacked fixed point value f to floating-point is performed as follows:

The first component of the returned vector will be extracted from the least significant bits of the input; the last component will be extracted from the most significant bits.

An unsigned integer containing packed floating-point values.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/unpackUnorm.xhtml

uint packSnorm4x8(vec4 v) 🔗

Packs floating-point values into an unsigned integer.

Convert each component of the normalized floating-point value v into 16-bit integer values and then packs the results into a 32-bit unsigned integer.

The conversion for component c of v to fixed-point is performed as follows:

The first component of the vector will be written to the least significant bits of the output; the last component will be written to the most significant bits.

A vector of values to be packed into an unsigned integer.

Unsigned 32 bit integer containing the packed encoding of the vector.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/packUnorm.xhtml

vec4 unpackSnorm4x8(uint v) 🔗

Unpack floating-point values from an unsigned integer.

Unpack single 32-bit unsigned integers into four 8-bit signed integers. Then, each component is converted to a normalized floating-point value to generate the returned four-component vector.

The conversion for unpacked fixed point value f to floating-point is performed as follows:

clamp(f / 127.0, -1.0, 1.0)

The first component of the returned vector will be extracted from the least significant bits of the input; the last component will be extracted from the most significant bits.

An unsigned integer containing packed floating-point values.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/unpackUnorm.xhtml

Extracts a range of bits from an integer.

Insert a range of bits into an integer.

Reverse the order of bits in an integer.

Counts the number of 1 bits in an integer.

Find the index of the least significant bit set to 1 in an integer.

Find the index of the most significant bit set to 1 in an integer.

Multiplies two 32-bit numbers and produce a 64-bit result.

uaddCarry(vec_uint_type x, vec_uint_type y, out vec_uint_type carry)

Adds two unsigned integers and generates carry.

usubBorrow(vec_uint_type x, vec_uint_type y, out vec_uint_type borrow)

Subtracts two unsigned integers and generates borrow.

ldexp(vec_type x, out vec_int_type exp)

Assemble a floating-point number from a value and exponent.

frexp(vec_type x, out vec_int_type exp)

Splits a floating-point number (x) into significand integral components

vec_int_type bitfieldExtract(vec_int_type value, int offset, int bits) 🔗

Extracts a subset of the bits of value and returns it in the least significant bits of the result. The range of bits extracted is [offset, offset + bits - 1].

The most significant bits of the result will be set to zero.

If bits is zero, the result will be zero.

The result will be undefined if:

offset or bits is negative.

if the sum of offset and bits is greater than the number of bits used to store the operand.

The integer from which to extract bits.

The index of the first bit to extract.

The number of bits to extract.

Integer with the requested bits.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/bitfieldExtract.xhtml

vec_uint_type bitfieldExtract(vec_uint_type value, int offset, int bits) 🔗

Component-wise Function.

Extracts a subset of the bits of value and returns it in the least significant bits of the result. The range of bits extracted is [offset, offset + bits - 1].

The most significant bits will be set to the value of offset + base - 1 (i.e., it is sign extended to the width of the return type).

If bits is zero, the result will be zero.

The result will be undefined if:

offset or bits is negative.

if the sum of offset and bits is greater than the number of bits used to store the operand.

The integer from which to extract bits.

The index of the first bit to extract.

The number of bits to extract.

Integer with the requested bits.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/bitfieldExtract.xhtml

vec_uint_type bitfieldExtract(vec_uint_type value, int offset, int bits) 🔗

vec_uint_type bitfieldInsert(vec_uint_type base, vec_uint_type insert, int offset, int bits) 🔗

Component-wise Function.

Inserts the bits least significant bits of insert into base at offset offset.

The returned value will have bits [offset, offset + bits + 1] taken from [0, bits - 1] of insert and all other bits taken directly from the corresponding bits of base.

If bits is zero, the result will be the original value of base.

The result will be undefined if:

offset or bits is negative.

if the sum of offset and bits is greater than the number of bits used to store the operand.

The integer into which to insert insert.

The value of the bits to insert.

The index of the first bit to insert.

The number of bits to insert.

base with inserted bits.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/bitfieldInsert.xhtml

vec_int_type bitfieldReverse(vec_int_type value) 🔗

vec_uint_type bitfieldReverse(vec_uint_type value) 🔗

Component-wise Function.

Reverse the order of bits in an integer.

The bit numbered n will be taken from bit (bits - 1) - n of value, where bits is the total number of bits used to represent value.

The value whose bits to reverse.

value but with its bits reversed.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/bitfieldReverse.xhtml

vec_int_type bitCount(vec_int_type value) 🔗

vec_uint_type bitCount(vec_uint_type value) 🔗

Component-wise Function.

Counts the number of 1 bits in an integer.

The value whose bits to count.

The number of bits that are set to 1 in the binary representation of value.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/bitCount.xhtml

vec_int_type findLSB(vec_int_type value) 🔗

vec_uint_type findLSB(vec_uint_type value) 🔗

Component-wise Function.

Find the index of the least significant bit set to 1.

If value is zero, -1 will be returned.

The value whose bits to scan.

The bit number of the least significant bit that is set to 1 in the binary representation of value.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/findLSB.xhtml

vec_int_type findMSB(vec_int_type value) 🔗

vec_uint_type findMSB(vec_uint_type value) 🔗

Component-wise Function.

Find the index of the most significant bit set to 1.

For positive integers, the result will be the bit number of the most significant bit that is set to 1.

For negative integers, the result will be the bit number of the most significant bit set to 0.

For a value of zero or negative 1, -1 will be returned.

The value whose bits to scan.

The bit number of the most significant bit that is set to 1 in the binary representation of value.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/findMSB.xhtml

void imulExtended(vec_int_type x, vec_int_type y, out vec_int_type msb, out vec_int_type lsb) 🔗

Component-wise Function.

Perform 32-bit by 32-bit signed multiplication to produce a 64-bit result.

The 32 least significant bits of this product are returned in lsb and the 32 most significant bits are returned in msb.

The first multiplicand.

The second multiplicand.

The variable to receive the most significant word of the product.

The variable to receive the least significant word of the product.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/umulExtended.xhtml

void umulExtended(vec_uint_type x, vec_uint_type y, out vec_uint_type msb, out vec_uint_type lsb) 🔗

Component-wise Function.

Perform 32-bit by 32-bit unsigned multiplication to produce a 64-bit result.

The 32 least significant bits of this product are returned in lsb and the 32 most significant bits are returned in msb.

The first multiplicand.

The second multiplicand.

The variable to receive the most significant word of the product.

The variable to receive the least significant word of the product.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/umulExtended.xhtml

vec_uint_type uaddCarry(vec_uint_type x, vec_uint_type y, out vec_uint_type carry) 🔗

Component-wise Function.

Add unsigned integers and generate carry.

adds two 32-bit unsigned integer variables (scalars or vectors) and generates a 32-bit unsigned integer result, along with a carry output. The value carry is .

0 if the sum is less than 232, otherwise 1.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/uaddCarry.xhtml

vec_uint_type usubBorrow(vec_uint_type x, vec_uint_type y, out vec_uint_type borrow) 🔗

Component-wise Function.

Subtract unsigned integers and generate borrow.

0 if x >= y, otherwise 1.

The difference of x and y if non-negative, or 232 plus that difference otherwise.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/usubBorrow.xhtml

vec_type ldexp(vec_type x, out vec_int_type exp) 🔗

Component-wise Function.

Assembles a floating-point number from a value and exponent.

If this product is too large to be represented in the floating-point type, the result is undefined.

The value to be used as a source of significand.

The value to be used as a source of exponent.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/ldexp.xhtml

vec_type frexp(vec_type x, out vec_int_type exp) 🔗

Component-wise Function.

Extracts x into a floating-point significand in the range [0.5, 1.0) and in integral exponent of two, such that:

For a floating-point value of zero, the significand and exponent are both zero.

For a floating-point value that is an infinity or a floating-point NaN, the results are undefined.

The value from which significand and exponent are to be extracted.

The variable into which to place the exponent of x.

The significand of x.

https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/frexp.xhtml

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
vec_type t;
t = clamp((c - a) / (b - a), 0.0, 1.0);
return t * t * (3.0 - 2.0 * t);
```

Example 2 (unknown):
```unknown
vec2( a.y * b.z - b.y * a.z,
      a.z * b.x - b.z * a.x,
      a.x * b.z - b.x * a.y)
```

Example 3 (unknown):
```unknown
k = 1.0 - eta * eta * (1.0 - dot(N, I) * dot(N, I));
if (k < 0.0)
    R = genType(0.0);       // or genDType(0.0)
else
    R = eta * I - (eta * dot(N, I) + sqrt(k)) * N;
```

Example 4 (unknown):
```unknown
bool any(bvec x) {     // bvec can be bvec2, bvec3 or bvec4
    bool result = false;
    int i;
    for (i = 0; i < x.length(); ++i) {
        result |= x[i];
    }
    return result;
}
```

---

## ButtonGroup

**URL:** https://docs.godotengine.org/en/stable/classes/class_buttongroup.html

**Contents:**
- ButtonGroup
- Description
- Properties
- Methods
- Signals
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

A group of buttons that doesn't allow more than one button to be pressed at a time.

A group of BaseButton-derived buttons. The buttons in a ButtonGroup are treated like radio buttons: No more than one button can be pressed at a time. Some types of buttons (such as CheckBox) may have a special appearance in this state.

Every member of a ButtonGroup should have BaseButton.toggle_mode set to true.

resource_local_to_scene

true (overrides Resource)

pressed(button: BaseButton) 🔗

Emitted when one of the buttons of the group is pressed.

bool allow_unpress = false 🔗

void set_allow_unpress(value: bool)

bool is_allow_unpress()

If true, it is possible to unpress all buttons in this ButtonGroup.

Array[BaseButton] get_buttons() 🔗

Returns an Array of Buttons who have this as their ButtonGroup (see BaseButton.button_group).

BaseButton get_pressed_button() 🔗

Returns the current pressed button.

Please read the User-contributed notes policy before submitting a comment.

---

## Button

**URL:** https://docs.godotengine.org/en/stable/classes/class_button.html

**Contents:**
- Button
- Description
- Tutorials
- Properties
- Theme Properties
- Property Descriptions
- Theme Property Descriptions
- User-contributed notes

Inherits: BaseButton < Control < CanvasItem < Node < Object

Inherited By: CheckBox, CheckButton, ColorPickerButton, MenuButton, OptionButton

A themed button that can contain text and an icon.

Button is the standard themed button. It can contain text and an icon, and it will display them according to the current Theme.

Example: Create a button and connect a method that will be called when the button is pressed:

See also BaseButton which contains common properties and methods associated with this node.

Note: Buttons do not detect touch input and therefore don't support multitouch, since mouse emulation can only press one button at a given time. Use TouchScreenButton for buttons that trigger gameplay movement or actions.

2D Dodge The Creeps Demo

Operating System Testing Demo

BitField[LineBreakFlag]

text_overrun_behavior

vertical_icon_alignment

Color(0.875, 0.875, 0.875, 1)

Color(0.875, 0.875, 0.875, 0.5)

Color(0.95, 0.95, 0.95, 1)

Color(0.95, 0.95, 0.95, 1)

font_hover_pressed_color

icon_hover_pressed_color

align_to_largest_stylebox

hover_pressed_mirrored

HorizontalAlignment alignment = 1 🔗

void set_text_alignment(value: HorizontalAlignment)

HorizontalAlignment get_text_alignment()

Text alignment policy for the button's text.

AutowrapMode autowrap_mode = 0 🔗

void set_autowrap_mode(value: AutowrapMode)

AutowrapMode get_autowrap_mode()

If set to something other than TextServer.AUTOWRAP_OFF, the text gets wrapped inside the node's bounding rectangle.

BitField[LineBreakFlag] autowrap_trim_flags = 128 🔗

void set_autowrap_trim_flags(value: BitField[LineBreakFlag])

BitField[LineBreakFlag] get_autowrap_trim_flags()

Autowrap space trimming flags. See TextServer.BREAK_TRIM_START_EDGE_SPACES and TextServer.BREAK_TRIM_END_EDGE_SPACES for more info.

bool clip_text = false 🔗

void set_clip_text(value: bool)

If true, text that is too large to fit the button is clipped horizontally. If false, the button will always be wide enough to hold the text. The text is not vertically clipped, and the button's height is not affected by this property.

bool expand_icon = false 🔗

void set_expand_icon(value: bool)

bool is_expand_icon()

When enabled, the button's icon will expand/shrink to fit the button's size while keeping its aspect. See also icon_max_width.

void set_flat(value: bool)

Flat buttons don't display decoration.

void set_button_icon(value: Texture2D)

Texture2D get_button_icon()

Button's icon, if text is present the icon will be placed before the text.

To edit margin and spacing of the icon, use h_separation theme property and content_margin_* properties of the used StyleBoxes.

HorizontalAlignment icon_alignment = 0 🔗

void set_icon_alignment(value: HorizontalAlignment)

HorizontalAlignment get_icon_alignment()

Specifies if the icon should be aligned horizontally to the left, right, or center of a button. Uses the same HorizontalAlignment constants as the text alignment. If centered horizontally and vertically, text will draw on top of the icon.

String language = "" 🔗

void set_language(value: String)

String get_language()

Language code used for line-breaking and text shaping algorithms, if left empty current locale is used instead.

void set_text(value: String)

The button's text that will be displayed inside the button's area.

TextDirection text_direction = 0 🔗

void set_text_direction(value: TextDirection)

TextDirection get_text_direction()

Base text writing direction.

OverrunBehavior text_overrun_behavior = 0 🔗

void set_text_overrun_behavior(value: OverrunBehavior)

OverrunBehavior get_text_overrun_behavior()

Sets the clipping behavior when the text exceeds the node's bounding rectangle.

VerticalAlignment vertical_icon_alignment = 1 🔗

void set_vertical_icon_alignment(value: VerticalAlignment)

VerticalAlignment get_vertical_icon_alignment()

Specifies if the icon should be aligned vertically to the top, bottom, or center of a button. Uses the same VerticalAlignment constants as the text alignment. If centered horizontally and vertically, text will draw on top of the icon.

Color font_color = Color(0.875, 0.875, 0.875, 1) 🔗

Default text Color of the Button.

Color font_disabled_color = Color(0.875, 0.875, 0.875, 0.5) 🔗

Text Color used when the Button is disabled.

Color font_focus_color = Color(0.95, 0.95, 0.95, 1) 🔗

Text Color used when the Button is focused. Only replaces the normal text color of the button. Disabled, hovered, and pressed states take precedence over this color.

Color font_hover_color = Color(0.95, 0.95, 0.95, 1) 🔗

Text Color used when the Button is being hovered.

Color font_hover_pressed_color = Color(1, 1, 1, 1) 🔗

Text Color used when the Button is being hovered and pressed.

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The tint of text outline of the Button.

Color font_pressed_color = Color(1, 1, 1, 1) 🔗

Text Color used when the Button is being pressed.

Color icon_disabled_color = Color(1, 1, 1, 0.4) 🔗

Icon modulate Color used when the Button is disabled.

Color icon_focus_color = Color(1, 1, 1, 1) 🔗

Icon modulate Color used when the Button is focused. Only replaces the normal modulate color of the button. Disabled, hovered, and pressed states take precedence over this color.

Color icon_hover_color = Color(1, 1, 1, 1) 🔗

Icon modulate Color used when the Button is being hovered.

Color icon_hover_pressed_color = Color(1, 1, 1, 1) 🔗

Icon modulate Color used when the Button is being hovered and pressed.

Color icon_normal_color = Color(1, 1, 1, 1) 🔗

Default icon modulate Color of the Button.

Color icon_pressed_color = Color(1, 1, 1, 1) 🔗

Icon modulate Color used when the Button is being pressed.

int align_to_largest_stylebox = 0 🔗

This constant acts as a boolean. If true, the minimum size of the button and text/icon alignment is always based on the largest stylebox margins, otherwise it's based on the current button state stylebox margins.

int h_separation = 4 🔗

The horizontal space between Button's icon and text. Negative values will be treated as 0 when used.

int icon_max_width = 0 🔗

The maximum allowed width of the Button's icon. This limit is applied on top of the default size of the icon, or its expanded size if expand_icon is true. The height is adjusted according to the icon's ratio. If the button has additional icons (e.g. CheckBox), they will also be limited.

int line_spacing = 0 🔗

Additional vertical spacing between lines (in pixels), spacing is added to line descent. This value can be negative.

int outline_size = 0 🔗

The size of the text outline.

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

Font of the Button's text.

Font size of the Button's text.

Default icon for the Button. Appears only if icon is not assigned.

StyleBox used when the Button is disabled.

StyleBox disabled_mirrored 🔗

StyleBox used when the Button is disabled (for right-to-left layouts).

StyleBox used when the Button is focused. The focus StyleBox is displayed over the base StyleBox, so a partially transparent StyleBox should be used to ensure the base StyleBox remains visible. A StyleBox that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a StyleBoxEmpty resource. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

StyleBox used when the Button is being hovered.

StyleBox hover_mirrored 🔗

StyleBox used when the Button is being hovered (for right-to-left layouts).

StyleBox hover_pressed 🔗

StyleBox used when the Button is being pressed and hovered at the same time.

StyleBox hover_pressed_mirrored 🔗

StyleBox used when the Button is being pressed and hovered at the same time (for right-to-left layouts).

Default StyleBox for the Button.

StyleBox normal_mirrored 🔗

Default StyleBox for the Button (for right-to-left layouts).

StyleBox used when the Button is being pressed.

StyleBox pressed_mirrored 🔗

StyleBox used when the Button is being pressed (for right-to-left layouts).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    var button = Button.new()
    button.text = "Click me"
    button.pressed.connect(_button_pressed)
    add_child(button)

func _button_pressed():
    print("Hello world!")
```

Example 2 (gdscript):
```gdscript
public override void _Ready()
{
    var button = new Button();
    button.Text = "Click me";
    button.Pressed += ButtonPressed;
    AddChild(button);
}

private void ButtonPressed()
{
    GD.Print("Hello world!");
}
```

---

## CanvasItem

**URL:** https://docs.godotengine.org/en/stable/classes/class_canvasitem.html

**Contents:**
- CanvasItem
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Constants
- Property Descriptions
- Method Descriptions

Inherits: Node < Object

Inherited By: Control, Node2D

Abstract base class for everything in 2D space.

Abstract base class for everything in 2D space. Canvas items are laid out in a tree; children inherit and extend their parent's transform. CanvasItem is extended by Control for GUI-related nodes, and by Node2D for 2D game objects.

Any CanvasItem can draw. For this, queue_redraw() is called by the engine, then NOTIFICATION_DRAW will be received on idle time to request a redraw. Because of this, canvas items don't need to be redrawn on every frame, improving the performance significantly. Several functions for drawing on the CanvasItem are provided (see draw_* functions). However, they can only be used inside _draw(), its corresponding Object._notification() or methods connected to the draw signal.

Canvas items are drawn in tree order on their canvas layer. By default, children are on top of their parents, so a root CanvasItem will be drawn behind everything. This behavior can be changed on a per-item basis.

A CanvasItem can be hidden, which will also hide its children. By adjusting various other properties of a CanvasItem, you can also modulate its color (via modulate or self_modulate), change its Z-index, blend mode, and more.

Note that properties like transform, modulation, and visibility are only propagated to direct CanvasItem child nodes. If there is a non-CanvasItem node in between, like Node or AnimationPlayer, the CanvasItem nodes below will have an independent position and modulate chain. See also top_level.

Viewport and canvas transforms

Audio Spectrum Visualizer Demo

draw_animation_slice(animation_length: float, slice_begin: float, slice_end: float, offset: float = 0.0)

draw_arc(center: Vector2, radius: float, start_angle: float, end_angle: float, point_count: int, color: Color, width: float = -1.0, antialiased: bool = false)

draw_char(font: Font, pos: Vector2, char: String, font_size: int = 16, modulate: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const

draw_char_outline(font: Font, pos: Vector2, char: String, font_size: int = 16, size: int = -1, modulate: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const

draw_circle(position: Vector2, radius: float, color: Color, filled: bool = true, width: float = -1.0, antialiased: bool = false)

draw_colored_polygon(points: PackedVector2Array, color: Color, uvs: PackedVector2Array = PackedVector2Array(), texture: Texture2D = null)

draw_dashed_line(from: Vector2, to: Vector2, color: Color, width: float = -1.0, dash: float = 2.0, aligned: bool = true, antialiased: bool = false)

draw_lcd_texture_rect_region(texture: Texture2D, rect: Rect2, src_rect: Rect2, modulate: Color = Color(1, 1, 1, 1))

draw_line(from: Vector2, to: Vector2, color: Color, width: float = -1.0, antialiased: bool = false)

draw_mesh(mesh: Mesh, texture: Texture2D, transform: Transform2D = Transform2D(1, 0, 0, 1, 0, 0), modulate: Color = Color(1, 1, 1, 1))

draw_msdf_texture_rect_region(texture: Texture2D, rect: Rect2, src_rect: Rect2, modulate: Color = Color(1, 1, 1, 1), outline: float = 0.0, pixel_range: float = 4.0, scale: float = 1.0)

draw_multiline(points: PackedVector2Array, color: Color, width: float = -1.0, antialiased: bool = false)

draw_multiline_colors(points: PackedVector2Array, colors: PackedColorArray, width: float = -1.0, antialiased: bool = false)

draw_multiline_string(font: Font, pos: Vector2, text: String, alignment: HorizontalAlignment = 0, width: float = -1, font_size: int = 16, max_lines: int = -1, modulate: Color = Color(1, 1, 1, 1), brk_flags: BitField[LineBreakFlag] = 3, justification_flags: BitField[JustificationFlag] = 3, direction: Direction = 0, orientation: Orientation = 0, oversampling: float = 0.0) const

draw_multiline_string_outline(font: Font, pos: Vector2, text: String, alignment: HorizontalAlignment = 0, width: float = -1, font_size: int = 16, max_lines: int = -1, size: int = 1, modulate: Color = Color(1, 1, 1, 1), brk_flags: BitField[LineBreakFlag] = 3, justification_flags: BitField[JustificationFlag] = 3, direction: Direction = 0, orientation: Orientation = 0, oversampling: float = 0.0) const

draw_multimesh(multimesh: MultiMesh, texture: Texture2D)

draw_polygon(points: PackedVector2Array, colors: PackedColorArray, uvs: PackedVector2Array = PackedVector2Array(), texture: Texture2D = null)

draw_polyline(points: PackedVector2Array, color: Color, width: float = -1.0, antialiased: bool = false)

draw_polyline_colors(points: PackedVector2Array, colors: PackedColorArray, width: float = -1.0, antialiased: bool = false)

draw_primitive(points: PackedVector2Array, colors: PackedColorArray, uvs: PackedVector2Array, texture: Texture2D = null)

draw_rect(rect: Rect2, color: Color, filled: bool = true, width: float = -1.0, antialiased: bool = false)

draw_set_transform(position: Vector2, rotation: float = 0.0, scale: Vector2 = Vector2(1, 1))

draw_set_transform_matrix(xform: Transform2D)

draw_string(font: Font, pos: Vector2, text: String, alignment: HorizontalAlignment = 0, width: float = -1, font_size: int = 16, modulate: Color = Color(1, 1, 1, 1), justification_flags: BitField[JustificationFlag] = 3, direction: Direction = 0, orientation: Orientation = 0, oversampling: float = 0.0) const

draw_string_outline(font: Font, pos: Vector2, text: String, alignment: HorizontalAlignment = 0, width: float = -1, font_size: int = 16, size: int = 1, modulate: Color = Color(1, 1, 1, 1), justification_flags: BitField[JustificationFlag] = 3, direction: Direction = 0, orientation: Orientation = 0, oversampling: float = 0.0) const

draw_style_box(style_box: StyleBox, rect: Rect2)

draw_texture(texture: Texture2D, position: Vector2, modulate: Color = Color(1, 1, 1, 1))

draw_texture_rect(texture: Texture2D, rect: Rect2, tile: bool, modulate: Color = Color(1, 1, 1, 1), transpose: bool = false)

draw_texture_rect_region(texture: Texture2D, rect: Rect2, src_rect: Rect2, modulate: Color = Color(1, 1, 1, 1), transpose: bool = false, clip_uv: bool = true)

force_update_transform()

get_canvas_item() const

get_canvas_layer_node() const

get_canvas_transform() const

get_global_mouse_position() const

get_global_transform() const

get_global_transform_with_canvas() const

get_instance_shader_parameter(name: StringName) const

get_local_mouse_position() const

get_screen_transform() const

get_transform() const

get_viewport_rect() const

get_viewport_transform() const

get_visibility_layer_bit(layer: int) const

is_local_transform_notification_enabled() const

is_transform_notification_enabled() const

is_visible_in_tree() const

make_canvas_position_local(viewport_point: Vector2) const

make_input_local(event: InputEvent) const

set_instance_shader_parameter(name: StringName, value: Variant)

set_notify_local_transform(enable: bool)

set_notify_transform(enable: bool)

set_visibility_layer_bit(layer: int, enabled: bool)

Emitted when the CanvasItem must redraw, after the related NOTIFICATION_DRAW notification, and before _draw() is called.

Note: Deferred connections do not allow drawing through the draw_* methods.

Emitted when this node becomes hidden, i.e. it's no longer visible in the tree (see is_visible_in_tree()).

item_rect_changed() 🔗

Emitted when the CanvasItem's boundaries (position or size) change, or when an action took place that may have affected these boundaries (e.g. changing Sprite2D.texture).

visibility_changed() 🔗

Emitted when the CanvasItem's visibility changes, either because its own visible property changed or because its visibility in the tree changed (see is_visible_in_tree()).

This signal is emitted after the related NOTIFICATION_VISIBILITY_CHANGED notification.

enum TextureFilter: 🔗

TextureFilter TEXTURE_FILTER_PARENT_NODE = 0

The CanvasItem will inherit the filter from its parent.

TextureFilter TEXTURE_FILTER_NEAREST = 1

The texture filter reads from the nearest pixel only. This makes the texture look pixelated from up close, and grainy from a distance (due to mipmaps not being sampled).

TextureFilter TEXTURE_FILTER_LINEAR = 2

The texture filter blends between the nearest 4 pixels. This makes the texture look smooth from up close, and grainy from a distance (due to mipmaps not being sampled).

TextureFilter TEXTURE_FILTER_NEAREST_WITH_MIPMAPS = 3

The texture filter reads from the nearest pixel and blends between the nearest 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true). This makes the texture look pixelated from up close, and smooth from a distance.

Use this for non-pixel art textures that may be viewed at a low scale (e.g. due to Camera2D zoom or sprite scaling), as mipmaps are important to smooth out pixels that are smaller than on-screen pixels.

TextureFilter TEXTURE_FILTER_LINEAR_WITH_MIPMAPS = 4

The texture filter blends between the nearest 4 pixels and between the nearest 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true). This makes the texture look smooth from up close, and smooth from a distance.

Use this for non-pixel art textures that may be viewed at a low scale (e.g. due to Camera2D zoom or sprite scaling), as mipmaps are important to smooth out pixels that are smaller than on-screen pixels.

TextureFilter TEXTURE_FILTER_NEAREST_WITH_MIPMAPS_ANISOTROPIC = 5

The texture filter reads from the nearest pixel and blends between 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true) based on the angle between the surface and the camera view. This makes the texture look pixelated from up close, and smooth from a distance. Anisotropic filtering improves texture quality on surfaces that are almost in line with the camera, but is slightly slower. The anisotropic filtering level can be changed by adjusting ProjectSettings.rendering/textures/default_filters/anisotropic_filtering_level.

Note: This texture filter is rarely useful in 2D projects. TEXTURE_FILTER_NEAREST_WITH_MIPMAPS is usually more appropriate in this case.

TextureFilter TEXTURE_FILTER_LINEAR_WITH_MIPMAPS_ANISOTROPIC = 6

The texture filter blends between the nearest 4 pixels and blends between 2 mipmaps (or uses the nearest mipmap if ProjectSettings.rendering/textures/default_filters/use_nearest_mipmap_filter is true) based on the angle between the surface and the camera view. This makes the texture look smooth from up close, and smooth from a distance. Anisotropic filtering improves texture quality on surfaces that are almost in line with the camera, but is slightly slower. The anisotropic filtering level can be changed by adjusting ProjectSettings.rendering/textures/default_filters/anisotropic_filtering_level.

Note: This texture filter is rarely useful in 2D projects. TEXTURE_FILTER_LINEAR_WITH_MIPMAPS is usually more appropriate in this case.

TextureFilter TEXTURE_FILTER_MAX = 7

Represents the size of the TextureFilter enum.

enum TextureRepeat: 🔗

TextureRepeat TEXTURE_REPEAT_PARENT_NODE = 0

The CanvasItem will inherit the filter from its parent.

TextureRepeat TEXTURE_REPEAT_DISABLED = 1

The texture does not repeat. Sampling the texture outside its extents will result in "stretching" of the edge pixels. You can avoid this by ensuring a 1-pixel fully transparent border on each side of the texture.

TextureRepeat TEXTURE_REPEAT_ENABLED = 2

The texture repeats when exceeding the texture's size.

TextureRepeat TEXTURE_REPEAT_MIRROR = 3

The texture repeats when the exceeding the texture's size in a "2×2 tiled mode". Repeated textures at even positions are mirrored.

TextureRepeat TEXTURE_REPEAT_MAX = 4

Represents the size of the TextureRepeat enum.

enum ClipChildrenMode: 🔗

ClipChildrenMode CLIP_CHILDREN_DISABLED = 0

Children are drawn over this node and are not clipped.

ClipChildrenMode CLIP_CHILDREN_ONLY = 1

This node is used as a mask and is not drawn. The mask is based on this node's alpha channel: Opaque pixels are kept, transparent pixels are discarded, and semi-transparent pixels are blended in according to their opacity. Children are clipped to this node's drawn area.

ClipChildrenMode CLIP_CHILDREN_AND_DRAW = 2

This node is used as a mask and is also drawn. The mask is based on this node's alpha channel: Opaque pixels are kept, transparent pixels are discarded, and semi-transparent pixels are blended in according to their opacity. Children are clipped to the parent's drawn area.

ClipChildrenMode CLIP_CHILDREN_MAX = 3

Represents the size of the ClipChildrenMode enum.

NOTIFICATION_TRANSFORM_CHANGED = 2000 🔗

Notification received when this node's global transform changes, if is_transform_notification_enabled() is true. See also set_notify_transform() and get_transform().

Note: Many canvas items such as Camera2D or CollisionObject2D automatically enable this in order to function correctly.

NOTIFICATION_LOCAL_TRANSFORM_CHANGED = 35 🔗

Notification received when this node's transform changes, if is_local_transform_notification_enabled() is true. This is not received when a parent Node2D's transform changes. See also set_notify_local_transform().

Note: Many canvas items such as Camera2D or CollisionShape2D automatically enable this in order to function correctly.

NOTIFICATION_DRAW = 30 🔗

The CanvasItem is requested to draw (see _draw()).

NOTIFICATION_VISIBILITY_CHANGED = 31 🔗

Notification received when this node's visibility changes (see visible and is_visible_in_tree()).

This notification is received before the related visibility_changed signal.

NOTIFICATION_ENTER_CANVAS = 32 🔗

The CanvasItem has entered the canvas.

NOTIFICATION_EXIT_CANVAS = 33 🔗

The CanvasItem has exited the canvas.

NOTIFICATION_WORLD_2D_CHANGED = 36 🔗

Notification received when this CanvasItem is registered to a new World2D (see get_world_2d()).

ClipChildrenMode clip_children = 0 🔗

void set_clip_children_mode(value: ClipChildrenMode)

ClipChildrenMode get_clip_children_mode()

The mode in which this node clips its children, acting as a mask.

Note: Clipping nodes cannot be nested or placed within a CanvasGroup. If an ancestor of this node clips its children or is a CanvasGroup, then this node's clip mode should be set to CLIP_CHILDREN_DISABLED to avoid unexpected behavior.

void set_light_mask(value: int)

The rendering layers in which this CanvasItem responds to Light2D nodes.

void set_material(value: Material)

Material get_material()

The material applied to this CanvasItem.

Color modulate = Color(1, 1, 1, 1) 🔗

void set_modulate(value: Color)

The color applied to this CanvasItem. This property does affect child CanvasItems, unlike self_modulate which only affects the node itself.

Color self_modulate = Color(1, 1, 1, 1) 🔗

void set_self_modulate(value: Color)

Color get_self_modulate()

The color applied to this CanvasItem. This property does not affect child CanvasItems, unlike modulate which affects both the node itself and its children.

Note: Internal children are also not affected by this property (see the include_internal parameter in Node.add_child()). For built-in nodes this includes sliders in ColorPicker, and the tab bar in TabContainer.

bool show_behind_parent = false 🔗

void set_draw_behind_parent(value: bool)

bool is_draw_behind_parent_enabled()

If true, this node draws behind its parent.

TextureFilter texture_filter = 0 🔗

void set_texture_filter(value: TextureFilter)

TextureFilter get_texture_filter()

The filtering mode used to render this CanvasItem's texture(s).

TextureRepeat texture_repeat = 0 🔗

void set_texture_repeat(value: TextureRepeat)

TextureRepeat get_texture_repeat()

The repeating mode used to render this CanvasItem's texture(s). It affects what happens when the texture is sampled outside its extents, for example by setting a Sprite2D.region_rect that is larger than the texture or assigning Polygon2D UV points outside the texture.

Note: TextureRect is not affected by texture_repeat, as it uses its own texture repeating implementation.

bool top_level = false 🔗

void set_as_top_level(value: bool)

bool is_set_as_top_level()

If true, this CanvasItem will not inherit its transform from parent CanvasItems. Its draw order will also be changed to make it draw on top of other CanvasItems that do not have top_level set to true. The CanvasItem will effectively act as if it was placed as a child of a bare Node.

bool use_parent_material = false 🔗

void set_use_parent_material(value: bool)

bool get_use_parent_material()

If true, the parent CanvasItem's material is used as this node's material.

int visibility_layer = 1 🔗

void set_visibility_layer(value: int)

int get_visibility_layer()

The rendering layer in which this CanvasItem is rendered by Viewport nodes. A Viewport will render a CanvasItem if it and all its parents share a layer with the Viewport's canvas cull mask.

bool visible = true 🔗

void set_visible(value: bool)

If true, this CanvasItem may be drawn. Whether this CanvasItem is actually drawn depends on the visibility of all of its CanvasItem ancestors. In other words: this CanvasItem will be drawn when is_visible_in_tree() returns true and all CanvasItem ancestors share at least one visibility_layer with this CanvasItem.

Note: For controls that inherit Popup, the correct way to make them visible is to call one of the multiple popup*() functions instead.

bool y_sort_enabled = false 🔗

void set_y_sort_enabled(value: bool)

bool is_y_sort_enabled()

If true, this and child CanvasItem nodes with a higher Y position are rendered in front of nodes with a lower Y position. If false, this and child CanvasItem nodes are rendered normally in scene tree order.

With Y-sorting enabled on a parent node ('A') but disabled on a child node ('B'), the child node ('B') is sorted but its children ('C1', 'C2', etc.) render together on the same Y position as the child node ('B'). This allows you to organize the render order of a scene without changing the scene tree.

Nodes sort relative to each other only if they are on the same z_index.

bool z_as_relative = true 🔗

void set_z_as_relative(value: bool)

If true, this node's final Z index is relative to its parent's Z index.

For example, if z_index is 2 and its parent's final Z index is 3, then this node's final Z index will be 5 (2 + 3).

void set_z_index(value: int)

The order in which this node is drawn. A node with a higher Z index will display in front of others. Must be between RenderingServer.CANVAS_ITEM_Z_MIN and RenderingServer.CANVAS_ITEM_Z_MAX (inclusive).

Note: The Z index does not affect the order in which CanvasItem nodes are processed or the way input events are handled. This is especially important to keep in mind for Control nodes.

void _draw() virtual 🔗

Called when CanvasItem has been requested to redraw (after queue_redraw() is called, either manually or by the engine).

Corresponds to the NOTIFICATION_DRAW notification in Object._notification().

void draw_animation_slice(animation_length: float, slice_begin: float, slice_end: float, offset: float = 0.0) 🔗

Subsequent drawing commands will be ignored unless they fall within the specified animation slice. This is a faster way to implement animations that loop on background rather than redrawing constantly.

void draw_arc(center: Vector2, radius: float, start_angle: float, end_angle: float, point_count: int, color: Color, width: float = -1.0, antialiased: bool = false) 🔗

Draws an unfilled arc between the given angles with a uniform color and width and optional antialiasing (supported only for positive width). The larger the value of point_count, the smoother the curve. center is defined in local space. See also draw_circle().

If width is negative, it will be ignored and the arc will be drawn using RenderingServer.PRIMITIVE_LINE_STRIP. This means that when the CanvasItem is scaled, the arc will remain thin. If this behavior is not desired, then pass a positive width like 1.0.

The arc is drawn from start_angle towards the value of end_angle so in clockwise direction if start_angle < end_angle and counter-clockwise otherwise. Passing the same angles but in reversed order will produce the same arc. If absolute difference of start_angle and end_angle is greater than @GDScript.TAU radians, then a full circle arc is drawn (i.e. arc will not overlap itself).

void draw_char(font: Font, pos: Vector2, char: String, font_size: int = 16, modulate: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const 🔗

Draws a string first character using a custom font. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used. pos is defined in local space.

void draw_char_outline(font: Font, pos: Vector2, char: String, font_size: int = 16, size: int = -1, modulate: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const 🔗

Draws a string first character outline using a custom font. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used. pos is defined in local space.

void draw_circle(position: Vector2, radius: float, color: Color, filled: bool = true, width: float = -1.0, antialiased: bool = false) 🔗

Draws a circle, with position defined in local space. See also draw_arc(), draw_polyline(), and draw_polygon().

If filled is true, the circle will be filled with the color specified. If filled is false, the circle will be drawn as a stroke with the color and width specified.

If width is negative, then two-point primitives will be drawn instead of a four-point ones. This means that when the CanvasItem is scaled, the lines will remain thin. If this behavior is not desired, then pass a positive width like 1.0.

If antialiased is true, half transparent "feathers" will be attached to the boundary, making outlines smooth.

Note: width is only effective if filled is false.

void draw_colored_polygon(points: PackedVector2Array, color: Color, uvs: PackedVector2Array = PackedVector2Array(), texture: Texture2D = null) 🔗

Draws a colored polygon of any number of points, convex or concave. The points in the points array are defined in local space. Unlike draw_polygon(), a single color must be specified for the whole polygon.

Note: If you frequently redraw the same polygon with a large number of vertices, consider pre-calculating the triangulation with Geometry2D.triangulate_polygon() and using draw_mesh(), draw_multimesh(), or RenderingServer.canvas_item_add_triangle_array().

void draw_dashed_line(from: Vector2, to: Vector2, color: Color, width: float = -1.0, dash: float = 2.0, aligned: bool = true, antialiased: bool = false) 🔗

Draws a dashed line from a 2D point to another, with a given color and width. The from and to positions are defined in local space. See also draw_line(), draw_multiline(), and draw_polyline().

If width is negative, then a two-point primitives will be drawn instead of a four-point ones. This means that when the CanvasItem is scaled, the line parts will remain thin. If this behavior is not desired, then pass a positive width like 1.0.

dash is the length of each dash in pixels, with the gap between each dash being the same length. If aligned is true, the length of the first and last dashes may be shortened or lengthened to allow the line to begin and end at the precise points defined by from and to. Both ends are always symmetrical when aligned is true. If aligned is false, all dashes will have the same length, but the line may appear incomplete at the end due to the dash length not dividing evenly into the line length. Only full dashes are drawn when aligned is false.

If antialiased is true, half transparent "feathers" will be attached to the boundary, making outlines smooth.

Note: antialiased is only effective if width is greater than 0.0.

void draw_end_animation() 🔗

After submitting all animations slices via draw_animation_slice(), this function can be used to revert drawing to its default state (all subsequent drawing commands will be visible). If you don't care about this particular use case, usage of this function after submitting the slices is not required.

void draw_lcd_texture_rect_region(texture: Texture2D, rect: Rect2, src_rect: Rect2, modulate: Color = Color(1, 1, 1, 1)) 🔗

Draws a textured rectangle region of the font texture with LCD subpixel anti-aliasing at a given position, optionally modulated by a color. The rect is defined in local space.

Texture is drawn using the following blend operation, blend mode of the CanvasItemMaterial is ignored:

void draw_line(from: Vector2, to: Vector2, color: Color, width: float = -1.0, antialiased: bool = false) 🔗

Draws a line from a 2D point to another, with a given color and width. It can be optionally antialiased. The from and to positions are defined in local space. See also draw_dashed_line(), draw_multiline(), and draw_polyline().

If width is negative, then a two-point primitive will be drawn instead of a four-point one. This means that when the CanvasItem is scaled, the line will remain thin. If this behavior is not desired, then pass a positive width like 1.0.

void draw_mesh(mesh: Mesh, texture: Texture2D, transform: Transform2D = Transform2D(1, 0, 0, 1, 0, 0), modulate: Color = Color(1, 1, 1, 1)) 🔗

Draws a Mesh in 2D, using the provided texture. See MeshInstance2D for related documentation. The transform is defined in local space.

void draw_msdf_texture_rect_region(texture: Texture2D, rect: Rect2, src_rect: Rect2, modulate: Color = Color(1, 1, 1, 1), outline: float = 0.0, pixel_range: float = 4.0, scale: float = 1.0) 🔗

Draws a textured rectangle region of the multichannel signed distance field texture at a given position, optionally modulated by a color. The rect is defined in local space. See FontFile.multichannel_signed_distance_field for more information and caveats about MSDF font rendering.

If outline is positive, each alpha channel value of pixel in region is set to maximum value of true distance in the outline radius.

Value of the pixel_range should the same that was used during distance field texture generation.

void draw_multiline(points: PackedVector2Array, color: Color, width: float = -1.0, antialiased: bool = false) 🔗

Draws multiple disconnected lines with a uniform width and color. Each line is defined by two consecutive points from points array in local space, i.e. i-th segment consists of points[2 * i], points[2 * i + 1] endpoints. When drawing large amounts of lines, this is faster than using individual draw_line() calls. To draw interconnected lines, use draw_polyline() instead.

If width is negative, then two-point primitives will be drawn instead of a four-point ones. This means that when the CanvasItem is scaled, the lines will remain thin. If this behavior is not desired, then pass a positive width like 1.0.

Note: antialiased is only effective if width is greater than 0.0.

void draw_multiline_colors(points: PackedVector2Array, colors: PackedColorArray, width: float = -1.0, antialiased: bool = false) 🔗

Draws multiple disconnected lines with a uniform width and segment-by-segment coloring. Each segment is defined by two consecutive points from points array in local space and a corresponding color from colors array, i.e. i-th segment consists of points[2 * i], points[2 * i + 1] endpoints and has colors[i] color. When drawing large amounts of lines, this is faster than using individual draw_line() calls. To draw interconnected lines, use draw_polyline_colors() instead.

If width is negative, then two-point primitives will be drawn instead of a four-point ones. This means that when the CanvasItem is scaled, the lines will remain thin. If this behavior is not desired, then pass a positive width like 1.0.

Note: antialiased is only effective if width is greater than 0.0.

void draw_multiline_string(font: Font, pos: Vector2, text: String, alignment: HorizontalAlignment = 0, width: float = -1, font_size: int = 16, max_lines: int = -1, modulate: Color = Color(1, 1, 1, 1), brk_flags: BitField[LineBreakFlag] = 3, justification_flags: BitField[JustificationFlag] = 3, direction: Direction = 0, orientation: Orientation = 0, oversampling: float = 0.0) const 🔗

Breaks text into lines and draws it using the specified font at the pos in local space (top-left corner). The text will have its color multiplied by modulate. If width is greater than or equal to 0, the text will be clipped if it exceeds the specified width. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used.

void draw_multiline_string_outline(font: Font, pos: Vector2, text: String, alignment: HorizontalAlignment = 0, width: float = -1, font_size: int = 16, max_lines: int = -1, size: int = 1, modulate: Color = Color(1, 1, 1, 1), brk_flags: BitField[LineBreakFlag] = 3, justification_flags: BitField[JustificationFlag] = 3, direction: Direction = 0, orientation: Orientation = 0, oversampling: float = 0.0) const 🔗

Breaks text to the lines and draws text outline using the specified font at the pos in local space (top-left corner). The text will have its color multiplied by modulate. If width is greater than or equal to 0, the text will be clipped if it exceeds the specified width. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used.

void draw_multimesh(multimesh: MultiMesh, texture: Texture2D) 🔗

Draws a MultiMesh in 2D with the provided texture. See MultiMeshInstance2D for related documentation.

void draw_polygon(points: PackedVector2Array, colors: PackedColorArray, uvs: PackedVector2Array = PackedVector2Array(), texture: Texture2D = null) 🔗

Draws a solid polygon of any number of points, convex or concave. Unlike draw_colored_polygon(), each point's color can be changed individually. The points array is defined in local space. See also draw_polyline() and draw_polyline_colors(). If you need more flexibility (such as being able to use bones), use RenderingServer.canvas_item_add_triangle_array() instead.

Note: If you frequently redraw the same polygon with a large number of vertices, consider pre-calculating the triangulation with Geometry2D.triangulate_polygon() and using draw_mesh(), draw_multimesh(), or RenderingServer.canvas_item_add_triangle_array().

void draw_polyline(points: PackedVector2Array, color: Color, width: float = -1.0, antialiased: bool = false) 🔗

Draws interconnected line segments with a uniform color and width and optional antialiasing (supported only for positive width). The points array is defined in local space. When drawing large amounts of lines, this is faster than using individual draw_line() calls. To draw disconnected lines, use draw_multiline() instead. See also draw_polygon().

If width is negative, it will be ignored and the polyline will be drawn using RenderingServer.PRIMITIVE_LINE_STRIP. This means that when the CanvasItem is scaled, the polyline will remain thin. If this behavior is not desired, then pass a positive width like 1.0.

void draw_polyline_colors(points: PackedVector2Array, colors: PackedColorArray, width: float = -1.0, antialiased: bool = false) 🔗

Draws interconnected line segments with a uniform width, point-by-point coloring, and optional antialiasing (supported only for positive width). Colors assigned to line points match by index between points and colors, i.e. each line segment is filled with a gradient between the colors of the endpoints. The points array is defined in local space. When drawing large amounts of lines, this is faster than using individual draw_line() calls. To draw disconnected lines, use draw_multiline_colors() instead. See also draw_polygon().

If width is negative, it will be ignored and the polyline will be drawn using RenderingServer.PRIMITIVE_LINE_STRIP. This means that when the CanvasItem is scaled, the polyline will remain thin. If this behavior is not desired, then pass a positive width like 1.0.

void draw_primitive(points: PackedVector2Array, colors: PackedColorArray, uvs: PackedVector2Array, texture: Texture2D = null) 🔗

Draws a custom primitive. 1 point for a point, 2 points for a line, 3 points for a triangle, and 4 points for a quad. If 0 points or more than 4 points are specified, nothing will be drawn and an error message will be printed. The points array is defined in local space. See also draw_line(), draw_polyline(), draw_polygon(), and draw_rect().

void draw_rect(rect: Rect2, color: Color, filled: bool = true, width: float = -1.0, antialiased: bool = false) 🔗

Draws a rectangle. If filled is true, the rectangle will be filled with the color specified. If filled is false, the rectangle will be drawn as a stroke with the color and width specified. The rect is specified in local space. See also draw_texture_rect().

If width is negative, then two-point primitives will be drawn instead of a four-point ones. This means that when the CanvasItem is scaled, the lines will remain thin. If this behavior is not desired, then pass a positive width like 1.0.

If antialiased is true, half transparent "feathers" will be attached to the boundary, making outlines smooth.

Note: width is only effective if filled is false.

Note: Unfilled rectangles drawn with a negative width may not display perfectly. For example, corners may be missing or brighter due to overlapping lines (for a translucent color).

void draw_set_transform(position: Vector2, rotation: float = 0.0, scale: Vector2 = Vector2(1, 1)) 🔗

Sets a custom local transform for drawing via components. Anything drawn afterwards will be transformed by this.

Note: FontFile.oversampling does not take scale into account. This means that scaling up/down will cause bitmap fonts and rasterized (non-MSDF) dynamic fonts to appear blurry or pixelated. To ensure text remains crisp regardless of scale, you can enable MSDF font rendering by enabling ProjectSettings.gui/theme/default_font_multichannel_signed_distance_field (applies to the default project font only), or enabling Multichannel Signed Distance Field in the import options of a DynamicFont for custom fonts. On system fonts, SystemFont.multichannel_signed_distance_field can be enabled in the inspector.

void draw_set_transform_matrix(xform: Transform2D) 🔗

Sets a custom local transform for drawing via matrix. Anything drawn afterwards will be transformed by this.

void draw_string(font: Font, pos: Vector2, text: String, alignment: HorizontalAlignment = 0, width: float = -1, font_size: int = 16, modulate: Color = Color(1, 1, 1, 1), justification_flags: BitField[JustificationFlag] = 3, direction: Direction = 0, orientation: Orientation = 0, oversampling: float = 0.0) const 🔗

Draws text using the specified font at the pos in local space (bottom-left corner using the baseline of the font). The text will have its color multiplied by modulate. If width is greater than or equal to 0, the text will be clipped if it exceeds the specified width. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used.

Example: Draw "Hello world", using the project's default font:

See also Font.draw_string().

void draw_string_outline(font: Font, pos: Vector2, text: String, alignment: HorizontalAlignment = 0, width: float = -1, font_size: int = 16, size: int = 1, modulate: Color = Color(1, 1, 1, 1), justification_flags: BitField[JustificationFlag] = 3, direction: Direction = 0, orientation: Orientation = 0, oversampling: float = 0.0) const 🔗

Draws text outline using the specified font at the pos in local space (bottom-left corner using the baseline of the font). The text will have its color multiplied by modulate. If width is greater than or equal to 0, the text will be clipped if it exceeds the specified width. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used.

void draw_style_box(style_box: StyleBox, rect: Rect2) 🔗

Draws a styled rectangle. The rect is defined in local space.

void draw_texture(texture: Texture2D, position: Vector2, modulate: Color = Color(1, 1, 1, 1)) 🔗

Draws a texture at a given position. The position is defined in local space.

void draw_texture_rect(texture: Texture2D, rect: Rect2, tile: bool, modulate: Color = Color(1, 1, 1, 1), transpose: bool = false) 🔗

Draws a textured rectangle at a given position, optionally modulated by a color. The rect is defined in local space. If transpose is true, the texture will have its X and Y coordinates swapped. See also draw_rect() and draw_texture_rect_region().

void draw_texture_rect_region(texture: Texture2D, rect: Rect2, src_rect: Rect2, modulate: Color = Color(1, 1, 1, 1), transpose: bool = false, clip_uv: bool = true) 🔗

Draws a textured rectangle from a texture's region (specified by src_rect) at a given position in local space, optionally modulated by a color. If transpose is true, the texture will have its X and Y coordinates swapped. See also draw_texture_rect().

void force_update_transform() 🔗

Forces the node's transform to update. Fails if the node is not inside the tree. See also get_transform().

Note: For performance reasons, transform changes are usually accumulated and applied once at the end of the frame. The update propagates through CanvasItem children, as well. Therefore, use this method only when you need an up-to-date transform (such as during physics operations).

RID get_canvas() const 🔗

Returns the RID of the World2D canvas where this node is registered to, used by the RenderingServer.

RID get_canvas_item() const 🔗

Returns the internal canvas item RID used by the RenderingServer for this node.

CanvasLayer get_canvas_layer_node() const 🔗

Returns the CanvasLayer that contains this node, or null if the node is not in any CanvasLayer.

Transform2D get_canvas_transform() const 🔗

Returns the transform of this node, converted from its registered canvas's coordinate system to its viewport's coordinate system. See also Node.get_viewport().

Vector2 get_global_mouse_position() const 🔗

Returns mouse cursor's global position relative to the CanvasLayer that contains this node.

Note: For screen-space coordinates (e.g. when using a non-embedded Popup), you can use DisplayServer.mouse_get_position().

Transform2D get_global_transform() const 🔗

Returns the global transform matrix of this item, i.e. the combined transform up to the topmost CanvasItem node. The topmost item is a CanvasItem that either has no parent, has non-CanvasItem parent or it has top_level enabled.

Transform2D get_global_transform_with_canvas() const 🔗

Returns the transform from the local coordinate system of this CanvasItem to the Viewports coordinate system.

Variant get_instance_shader_parameter(name: StringName) const 🔗

Get the value of a shader parameter as set on this instance.

Vector2 get_local_mouse_position() const 🔗

Returns the mouse's position in this CanvasItem using the local coordinate system of this CanvasItem.

Transform2D get_screen_transform() const 🔗

Returns the transform of this CanvasItem in global screen coordinates (i.e. taking window position into account). Mostly useful for editor plugins.

Equals to get_global_transform() if the window is embedded (see Viewport.gui_embed_subwindows).

Transform2D get_transform() const 🔗

Returns the transform matrix of this CanvasItem.

Rect2 get_viewport_rect() const 🔗

Returns this node's viewport boundaries as a Rect2. See also Node.get_viewport().

Transform2D get_viewport_transform() const 🔗

Returns the transform of this node, converted from its registered canvas's coordinate system to its viewport embedder's coordinate system. See also Viewport.get_final_transform() and Node.get_viewport().

bool get_visibility_layer_bit(layer: int) const 🔗

Returns true if the layer at the given index is set in visibility_layer.

World2D get_world_2d() const 🔗

Returns the World2D this node is registered to.

Usually, this is the same as this node's viewport (see Node.get_viewport() and Viewport.find_world_2d()).

Hide the CanvasItem if it's currently visible. This is equivalent to setting visible to false.

bool is_local_transform_notification_enabled() const 🔗

Returns true if the node receives NOTIFICATION_LOCAL_TRANSFORM_CHANGED whenever its local transform changes. This is enabled with set_notify_local_transform().

bool is_transform_notification_enabled() const 🔗

Returns true if the node receives NOTIFICATION_TRANSFORM_CHANGED whenever its global transform changes. This is enabled with set_notify_transform().

bool is_visible_in_tree() const 🔗

Returns true if the node is present in the SceneTree, its visible property is true and all its ancestors are also visible. If any ancestor is hidden, this node will not be visible in the scene tree, and is therefore not drawn (see _draw()).

Visibility is checked only in parent nodes that inherit from CanvasItem, CanvasLayer, and Window. If the parent is of any other type (such as Node, AnimationPlayer, or Node3D), it is assumed to be visible.

Note: This method does not take visibility_layer into account, so even if this method returns true, the node might end up not being rendered.

Vector2 make_canvas_position_local(viewport_point: Vector2) const 🔗

Transforms viewport_point from the viewport's coordinates to this node's local coordinates.

For the opposite operation, use get_global_transform_with_canvas().

InputEvent make_input_local(event: InputEvent) const 🔗

Returns a copy of the given event with its coordinates converted from global space to this CanvasItem's local space. If not possible, returns the same InputEvent unchanged.

void move_to_front() 🔗

Moves this node below its siblings, usually causing the node to draw on top of its siblings. Does nothing if this node does not have a parent. See also Node.move_child().

void queue_redraw() 🔗

Queues the CanvasItem to redraw. During idle time, if CanvasItem is visible, NOTIFICATION_DRAW is sent and _draw() is called. This only occurs once per frame, even if this method has been called multiple times.

void set_instance_shader_parameter(name: StringName, value: Variant) 🔗

Set the value of a shader uniform for this instance only (per-instance uniform). See also ShaderMaterial.set_shader_parameter() to assign a uniform on all instances using the same ShaderMaterial.

Note: For a shader uniform to be assignable on a per-instance basis, it must be defined with instance uniform ... rather than uniform ... in the shader code.

Note: name is case-sensitive and must match the name of the uniform in the code exactly (not the capitalized name in the inspector).

void set_notify_local_transform(enable: bool) 🔗

If true, the node will receive NOTIFICATION_LOCAL_TRANSFORM_CHANGED whenever its local transform changes.

Note: Many canvas items such as Bone2D or CollisionShape2D automatically enable this in order to function correctly.

void set_notify_transform(enable: bool) 🔗

If true, the node will receive NOTIFICATION_TRANSFORM_CHANGED whenever global transform changes.

Note: Many canvas items such as Camera2D or Light2D automatically enable this in order to function correctly.

void set_visibility_layer_bit(layer: int, enabled: bool) 🔗

Set/clear individual bits on the rendering visibility layer. This simplifies editing this CanvasItem's visibility layer.

Show the CanvasItem if it's currently hidden. This is equivalent to setting visible to true.

Note: For controls that inherit Popup, the correct way to make them visible is to call one of the multiple popup*() functions instead.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
dst.r = texture.r * modulate.r * modulate.a + dst.r * (1.0 - texture.r * modulate.a);
dst.g = texture.g * modulate.g * modulate.a + dst.g * (1.0 - texture.g * modulate.a);
dst.b = texture.b * modulate.b * modulate.a + dst.b * (1.0 - texture.b * modulate.a);
dst.a = modulate.a + dst.a * (1.0 - modulate.a);
```

Example 2 (gdscript):
```gdscript
# If using this method in a script that redraws constantly, move the
# `default_font` declaration to a member variable assigned in `_ready()`
# so the Control is only created once.
var default_font = ThemeDB.fallback_font
var default_font_size = ThemeDB.fallback_font_size
draw_string(default_font, Vector2(64, 64), "Hello world", HORIZONTAL_ALIGNMENT_LEFT, -1, default_font_size)
```

Example 3 (gdscript):
```gdscript
// If using this method in a script that redraws constantly, move the
// `default_font` declaration to a member variable assigned in `_Ready()`
// so the Control is only created once.
Font defaultFont = ThemeDB.FallbackFont;
int defaultFontSize = ThemeDB.FallbackFontSize;
DrawString(defaultFont, new Vector2(64, 64), "Hello world", HORIZONTAL_ALIGNMENT_LEFT, -1, defaultFontSize);
```

Example 4 (gdscript):
```gdscript
var viewport_point = get_global_transform_with_canvas() * local_point
```

---

## CenterContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_centercontainer.html

**Contents:**
- CenterContainer
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Container < Control < CanvasItem < Node < Object

A container that keeps child controls in its center.

CenterContainer is a container that keeps all of its child controls in its center at their minimum size.

bool use_top_left = false 🔗

void set_use_top_left(value: bool)

bool is_using_top_left()

If true, centers children relative to the CenterContainer's top left corner.

Please read the User-contributed notes policy before submitting a comment.

---

## CharFXTransform

**URL:** https://docs.godotengine.org/en/stable/classes/class_charfxtransform.html

**Contents:**
- CharFXTransform
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Controls how an individual character will be displayed in a RichTextEffect.

By setting various properties on this object, you can control how individual characters will be displayed in a RichTextEffect.

BBCode in RichTextLabel

Transform2D(1, 0, 0, 1, 0, 0)

Color color = Color(0, 0, 0, 1) 🔗

void set_color(value: Color)

The color the character will be drawn with.

float elapsed_time = 0.0 🔗

void set_elapsed_time(value: float)

float get_elapsed_time()

The time elapsed since the RichTextLabel was added to the scene tree (in seconds). Time stops when the RichTextLabel is paused (see Node.process_mode). Resets when the text in the RichTextLabel is changed.

Note: Time still passes while the RichTextLabel is hidden.

Dictionary env = {} 🔗

void set_environment(value: Dictionary)

Dictionary get_environment()

Contains the arguments passed in the opening BBCode tag. By default, arguments are strings; if their contents match a type such as bool, int or float, they will be converted automatically. Color codes in the form #rrggbb or #rgb will be converted to an opaque Color. String arguments may not contain spaces, even if they're quoted. If present, quotes will also be present in the final string.

For example, the opening BBCode tag [example foo=hello bar=true baz=42 color=#ffffff] will map to the following Dictionary:

void set_font(value: RID)

TextServer RID of the font used to render glyph, this value can be used with TextServer.font_* methods to retrieve font information.

Note: Read-only. Setting this property won't affect drawing.

int glyph_count = 0 🔗

void set_glyph_count(value: int)

int get_glyph_count()

Number of glyphs in the grapheme cluster. This value is set in the first glyph of a cluster.

Note: Read-only. Setting this property won't affect drawing.

int glyph_flags = 0 🔗

void set_glyph_flags(value: int)

int get_glyph_flags()

Glyph flags. See GraphemeFlag for more info.

Note: Read-only. Setting this property won't affect drawing.

int glyph_index = 0 🔗

void set_glyph_index(value: int)

int get_glyph_index()

Glyph index specific to the font. If you want to replace this glyph, use TextServer.font_get_glyph_index() with font to get a new glyph index for a single character.

Vector2 offset = Vector2(0, 0) 🔗

void set_offset(value: Vector2)

The position offset the character will be drawn with (in pixels).

bool outline = false 🔗

void set_outline(value: bool)

If true, FX transform is called for outline drawing.

Note: Read-only. Setting this property won't affect drawing.

Vector2i range = Vector2i(0, 0) 🔗

void set_range(value: Vector2i)

Absolute character range in the string, corresponding to the glyph.

Note: Read-only. Setting this property won't affect drawing.

int relative_index = 0 🔗

void set_relative_index(value: int)

int get_relative_index()

The character offset of the glyph, relative to the current RichTextEffect custom block.

Note: Read-only. Setting this property won't affect drawing.

Transform2D transform = Transform2D(1, 0, 0, 1, 0, 0) 🔗

void set_transform(value: Transform2D)

Transform2D get_transform()

The current transform of the current glyph. It can be overridden (for example, by driving the position and rotation from a curve). You can also alter the existing value to apply transforms on top of other effects.

bool visible = true 🔗

void set_visibility(value: bool)

If true, the character will be drawn. If false, the character will be hidden. Characters around hidden characters will reflow to take the space of hidden characters. If this is not desired, set their color to Color(1, 1, 1, 0) instead.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (json):
```json
{"foo": "hello", "bar": true, "baz": 42, "color": Color(1, 1, 1, 1)}
```

---

## CheckBox

**URL:** https://docs.godotengine.org/en/stable/classes/class_checkbox.html

**Contents:**
- CheckBox
- Description
- Properties
- Theme Properties
- Theme Property Descriptions
- User-contributed notes

Inherits: Button < BaseButton < Control < CanvasItem < Node < Object

A button that represents a binary choice.

CheckBox allows the user to choose one of only two possible options. It's similar to CheckButton in functionality, but it has a different appearance. To follow established UX patterns, it's recommended to use CheckBox when toggling it has no immediate effect on something. For example, it could be used when toggling it will only do something once a confirmation button is pressed.

See also BaseButton which contains common properties and methods associated with this node.

When BaseButton.button_group specifies a ButtonGroup, CheckBox changes its appearance to that of a radio button and uses the various radio_* theme properties.

true (overrides BaseButton)

checkbox_checked_color

checkbox_unchecked_color

radio_checked_disabled

radio_unchecked_disabled

Color checkbox_checked_color = Color(1, 1, 1, 1) 🔗

The color of the checked icon when the checkbox is pressed.

Color checkbox_unchecked_color = Color(1, 1, 1, 1) 🔗

The color of the unchecked icon when the checkbox is not pressed.

int check_v_offset = 0 🔗

The vertical offset used when rendering the check icons (in pixels).

The check icon to display when the CheckBox is checked.

Texture2D checked_disabled 🔗

The check icon to display when the CheckBox is checked and is disabled.

Texture2D radio_checked 🔗

The check icon to display when the CheckBox is configured as a radio button and is checked.

Texture2D radio_checked_disabled 🔗

The check icon to display when the CheckBox is configured as a radio button, is disabled, and is unchecked.

Texture2D radio_unchecked 🔗

The check icon to display when the CheckBox is configured as a radio button and is unchecked.

Texture2D radio_unchecked_disabled 🔗

The check icon to display when the CheckBox is configured as a radio button, is disabled, and is unchecked.

Texture2D unchecked 🔗

The check icon to display when the CheckBox is unchecked.

Texture2D unchecked_disabled 🔗

The check icon to display when the CheckBox is unchecked and is disabled.

Please read the User-contributed notes policy before submitting a comment.

---

## CheckButton

**URL:** https://docs.godotengine.org/en/stable/classes/class_checkbutton.html

**Contents:**
- CheckButton
- Description
- Properties
- Theme Properties
- Theme Property Descriptions
- User-contributed notes

Inherits: Button < BaseButton < Control < CanvasItem < Node < Object

A button that represents a binary choice.

CheckButton is a toggle button displayed as a check field. It's similar to CheckBox in functionality, but it has a different appearance. To follow established UX patterns, it's recommended to use CheckButton when toggling it has an immediate effect on something. For example, it can be used when pressing it shows or hides advanced settings, without asking the user to confirm this action.

See also BaseButton which contains common properties and methods associated with this node.

true (overrides BaseButton)

button_unchecked_color

checked_disabled_mirrored

unchecked_disabled_mirrored

Color button_checked_color = Color(1, 1, 1, 1) 🔗

The color of the checked icon when the checkbox is pressed.

Color button_unchecked_color = Color(1, 1, 1, 1) 🔗

The color of the unchecked icon when the checkbox is not pressed.

int check_v_offset = 0 🔗

The vertical offset used when rendering the toggle icons (in pixels).

The icon to display when the CheckButton is checked (for left-to-right layouts).

Texture2D checked_disabled 🔗

The icon to display when the CheckButton is checked and disabled (for left-to-right layouts).

Texture2D checked_disabled_mirrored 🔗

The icon to display when the CheckButton is checked and disabled (for right-to-left layouts).

Texture2D checked_mirrored 🔗

The icon to display when the CheckButton is checked (for right-to-left layouts).

Texture2D unchecked 🔗

The icon to display when the CheckButton is unchecked (for left-to-right layouts).

Texture2D unchecked_disabled 🔗

The icon to display when the CheckButton is unchecked and disabled (for left-to-right layouts).

Texture2D unchecked_disabled_mirrored 🔗

The icon to display when the CheckButton is unchecked and disabled (for right-to-left layouts).

Texture2D unchecked_mirrored 🔗

The icon to display when the CheckButton is unchecked (for right-to-left layouts).

Please read the User-contributed notes policy before submitting a comment.

---

## ColorPalette

**URL:** https://docs.godotengine.org/en/stable/classes/class_colorpalette.html

**Contents:**
- ColorPalette
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

A resource class for managing a palette of colors, which can be loaded and saved using ColorPicker.

The ColorPalette resource is designed to store and manage a collection of colors. This resource is useful in scenarios where a predefined set of colors is required, such as for creating themes, designing user interfaces, or managing game assets. The built-in ColorPicker control can also make use of ColorPalette without additional code.

PackedColorArray colors = PackedColorArray() 🔗

void set_colors(value: PackedColorArray)

PackedColorArray get_colors()

A PackedColorArray containing the colors in the palette.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedColorArray for more details.

Please read the User-contributed notes policy before submitting a comment.

---

## ColorPickerButton

**URL:** https://docs.godotengine.org/en/stable/classes/class_colorpickerbutton.html

**Contents:**
- ColorPickerButton
- Description
- Tutorials
- Properties
- Methods
- Theme Properties
- Signals
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions

Inherits: Button < BaseButton < Control < CanvasItem < Node < Object

A button that brings up a ColorPicker when pressed.

Encapsulates a ColorPicker, making it accessible by pressing a button. Pressing the button will toggle the ColorPicker's visibility.

See also BaseButton which contains common properties and methods associated with this node.

Note: By default, the button may not be wide enough for the color preview swatch to be visible. Make sure to set Control.custom_minimum_size to a big enough value to give the button enough space.

GUI Drag And Drop Demo

true (overrides BaseButton)

color_changed(color: Color) 🔗

Emitted when the color changes.

Emitted when the ColorPicker is created (the button is pressed for the first time).

Emitted when the ColorPicker is closed.

Color color = Color(0, 0, 0, 1) 🔗

void set_pick_color(value: Color)

Color get_pick_color()

The currently selected color.

bool edit_alpha = true 🔗

void set_edit_alpha(value: bool)

bool is_editing_alpha()

If true, the alpha channel in the displayed ColorPicker will be visible.

bool edit_intensity = true 🔗

void set_edit_intensity(value: bool)

bool is_editing_intensity()

If true, the intensity slider in the displayed ColorPicker will be visible.

ColorPicker get_picker() 🔗

Returns the ColorPicker that this node toggles.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their CanvasItem.visible property.

PopupPanel get_popup() 🔗

Returns the control's PopupPanel which allows you to connect to popup signals. This allows you to handle events when the ColorPicker is shown or hidden.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their Window.visible property.

The background of the color preview rect on the button.

Please read the User-contributed notes policy before submitting a comment.

---

## ColorPicker

**URL:** https://docs.godotengine.org/en/stable/classes/class_colorpicker.html

**Contents:**
- ColorPicker
- Description
- Tutorials
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions

Inherits: VBoxContainer < BoxContainer < Container < Control < CanvasItem < Node < Object

A widget that provides an interface for selecting or modifying a color.

A widget that provides an interface for selecting or modifying a color. It can optionally provide functionalities like a color sampler (eyedropper), color modes, and presets.

Note: This control is the color picker widget itself. You can use a ColorPickerButton instead if you need a button that brings up a ColorPicker in a popup.

Tween Interpolation Demo

add_preset(color: Color)

add_recent_preset(color: Color)

erase_preset(color: Color)

erase_recent_preset(color: Color)

get_recent_presets() const

focused_not_editing_cursor_color

Color(1, 1, 1, 0.275)

center_slider_grabbers

picker_focus_rectangle

color_changed(color: Color) 🔗

Emitted when the color is changed.

preset_added(color: Color) 🔗

Emitted when a preset is added.

preset_removed(color: Color) 🔗

Emitted when a preset is removed.

enum ColorModeType: 🔗

ColorModeType MODE_RGB = 0

Allows editing the color with Red/Green/Blue sliders in sRGB color space.

ColorModeType MODE_HSV = 1

Allows editing the color with Hue/Saturation/Value sliders.

ColorModeType MODE_RAW = 2

Deprecated: This is replaced by MODE_LINEAR.

ColorModeType MODE_LINEAR = 2

Allows editing the color with Red/Green/Blue sliders in linear color space.

ColorModeType MODE_OKHSL = 3

Allows editing the color with Hue/Saturation/Lightness sliders.

OKHSL is a new color space similar to HSL but that better match perception by leveraging the Oklab color space which is designed to be simple to use, while doing a good job at predicting perceived lightness, chroma and hue.

Okhsv and Okhsl color spaces

enum PickerShapeType: 🔗

PickerShapeType SHAPE_HSV_RECTANGLE = 0

HSV Color Model rectangle color space.

PickerShapeType SHAPE_HSV_WHEEL = 1

HSV Color Model rectangle color space with a wheel.

PickerShapeType SHAPE_VHS_CIRCLE = 2

HSV Color Model circle color space. Use Saturation as a radius.

PickerShapeType SHAPE_OKHSL_CIRCLE = 3

HSL OK Color Model circle color space.

PickerShapeType SHAPE_NONE = 4

The color space shape and the shape select button are hidden. Can't be selected from the shapes popup.

PickerShapeType SHAPE_OK_HS_RECTANGLE = 5

OKHSL Color Model rectangle with constant lightness.

PickerShapeType SHAPE_OK_HL_RECTANGLE = 6

OKHSL Color Model rectangle with constant saturation.

bool can_add_swatches = true 🔗

void set_can_add_swatches(value: bool)

bool are_swatches_enabled()

If true, it's possible to add presets under Swatches. If false, the button to add presets is disabled.

Color color = Color(1, 1, 1, 1) 🔗

void set_pick_color(value: Color)

Color get_pick_color()

The currently selected color.

ColorModeType color_mode = 0 🔗

void set_color_mode(value: ColorModeType)

ColorModeType get_color_mode()

The currently selected color mode.

bool color_modes_visible = true 🔗

void set_modes_visible(value: bool)

bool are_modes_visible()

If true, the color mode buttons are visible.

bool deferred_mode = false 🔗

void set_deferred_mode(value: bool)

bool is_deferred_mode()

If true, the color will apply only after the user releases the mouse button, otherwise it will apply immediately even in mouse motion event (which can cause performance issues).

bool edit_alpha = true 🔗

void set_edit_alpha(value: bool)

bool is_editing_alpha()

If true, shows an alpha channel slider (opacity).

bool edit_intensity = true 🔗

void set_edit_intensity(value: bool)

bool is_editing_intensity()

If true, shows an intensity slider. The intensity is applied as follows: multiply the color by 2 ** intensity in linear RGB space, and then convert it back to sRGB.

bool hex_visible = true 🔗

void set_hex_visible(value: bool)

bool is_hex_visible()

If true, the hex color code input field is visible.

PickerShapeType picker_shape = 0 🔗

void set_picker_shape(value: PickerShapeType)

PickerShapeType get_picker_shape()

The shape of the color space view.

bool presets_visible = true 🔗

void set_presets_visible(value: bool)

bool are_presets_visible()

If true, the Swatches and Recent Colors presets are visible.

bool sampler_visible = true 🔗

void set_sampler_visible(value: bool)

bool is_sampler_visible()

If true, the color sampler and color preview are visible.

bool sliders_visible = true 🔗

void set_sliders_visible(value: bool)

bool are_sliders_visible()

If true, the color sliders are visible.

void add_preset(color: Color) 🔗

Adds the given color to a list of color presets. The presets are displayed in the color picker and the user will be able to select them.

Note: The presets list is only for this color picker.

void add_recent_preset(color: Color) 🔗

Adds the given color to a list of color recent presets so that it can be picked later. Recent presets are the colors that were picked recently, a new preset is automatically created and added to recent presets when you pick a new color.

Note: The recent presets list is only for this color picker.

void erase_preset(color: Color) 🔗

Removes the given color from the list of color presets of this color picker.

void erase_recent_preset(color: Color) 🔗

Removes the given color from the list of color recent presets of this color picker.

PackedColorArray get_presets() const 🔗

Returns the list of colors in the presets of the color picker.

PackedColorArray get_recent_presets() const 🔗

Returns the list of colors in the recent presets of the color picker.

Color focused_not_editing_cursor_color = Color(1, 1, 1, 0.275) 🔗

Color of rectangle or circle drawn when a picker shape part is focused but not editable via keyboard or joypad. Displayed over the picker shape, so a partially transparent color should be used to ensure the picker shape remains visible.

int center_slider_grabbers = 1 🔗

Overrides the Slider.center_grabber theme property of the sliders.

The width of the hue selection slider.

int label_width = 10 🔗

The minimum width of the color labels next to sliders.

The margin around the ColorPicker.

int sv_height = 256 🔗

The height of the saturation-value selection box.

The width of the saturation-value selection box.

Texture2D add_preset 🔗

The icon for the "Add Preset" button.

Texture2D bar_arrow 🔗

The texture for the arrow grabber.

Texture2D color_hue 🔗

Custom texture for the hue selection slider on the right.

Texture2D color_script 🔗

The icon for the button that switches color text to hexadecimal.

Texture2D expanded_arrow 🔗

The icon for color preset drop down menu when expanded.

Texture2D folded_arrow 🔗

The icon for color preset drop down menu when folded.

Texture2D menu_option 🔗

The icon for color preset option menu.

Texture2D overbright_indicator 🔗

The indicator used to signalize that the color value is outside the 0-1 range.

Texture2D picker_cursor 🔗

The image displayed over the color box/circle (depending on the picker_shape), marking the currently selected color.

Texture2D picker_cursor_bg 🔗

The fill image displayed behind the picker cursor.

Texture2D sample_bg 🔗

Background panel for the color preview box (visible when the color is translucent).

Texture2D sample_revert 🔗

The icon for the revert button (visible on the middle of the "old" color when it differs from the currently selected color). This icon is modulated with a dark color if the "old" color is bright enough, so the icon should be bright to ensure visibility in both scenarios.

Texture2D screen_picker 🔗

The icon for the screen color picker button.

Texture2D shape_circle 🔗

The icon for circular picker shapes.

Texture2D shape_rect 🔗

The icon for rectangular picker shapes.

Texture2D shape_rect_wheel 🔗

The icon for rectangular wheel picker shapes.

StyleBox picker_focus_circle 🔗

The StyleBox used when the circle-shaped part of the picker is focused. Displayed over the picker shape, so a partially transparent StyleBox should be used to ensure the picker shape remains visible. A StyleBox that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a StyleBoxEmpty resource. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

StyleBox picker_focus_rectangle 🔗

The StyleBox used when the rectangle-shaped part of the picker is focused. Displayed over the picker shape, so a partially transparent StyleBox should be used to ensure the picker shape remains visible. A StyleBox that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a StyleBoxEmpty resource. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

StyleBox sample_focus 🔗

The StyleBox used for the old color sample part when it is focused. Displayed over the sample, so a partially transparent StyleBox should be used to ensure the picker shape remains visible. A StyleBox that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a StyleBoxEmpty resource. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

Please read the User-contributed notes policy before submitting a comment.

---

## Container

**URL:** https://docs.godotengine.org/en/stable/classes/class_container.html

**Contents:**
- Container
- Description
- Tutorials
- Properties
- Methods
- Signals
- Constants
- Method Descriptions
- User-contributed notes

Inherits: Control < CanvasItem < Node < Object

Inherited By: AspectRatioContainer, BoxContainer, CenterContainer, EditorProperty, FlowContainer, FoldableContainer, GraphElement, GridContainer, MarginContainer, PanelContainer, ScrollContainer, SplitContainer, SubViewportContainer, TabContainer

Base class for all GUI containers.

Base class for all GUI containers. A Container automatically arranges its child controls in a certain way. This class can be inherited to make custom container types.

1 (overrides Control)

_get_allowed_size_flags_horizontal() virtual const

_get_allowed_size_flags_vertical() virtual const

fit_child_in_rect(child: Control, rect: Rect2)

pre_sort_children() 🔗

Emitted when children are going to be sorted.

Emitted when sorting the children is needed.

NOTIFICATION_PRE_SORT_CHILDREN = 50 🔗

Notification just before children are going to be sorted, in case there's something to process beforehand.

NOTIFICATION_SORT_CHILDREN = 51 🔗

Notification for when sorting the children, it must be obeyed immediately.

PackedInt32Array _get_allowed_size_flags_horizontal() virtual const 🔗

Implement to return a list of allowed horizontal SizeFlags for child nodes. This doesn't technically prevent the usages of any other size flags, if your implementation requires that. This only limits the options available to the user in the Inspector dock.

Note: Having no size flags is equal to having Control.SIZE_SHRINK_BEGIN. As such, this value is always implicitly allowed.

PackedInt32Array _get_allowed_size_flags_vertical() virtual const 🔗

Implement to return a list of allowed vertical SizeFlags for child nodes. This doesn't technically prevent the usages of any other size flags, if your implementation requires that. This only limits the options available to the user in the Inspector dock.

Note: Having no size flags is equal to having Control.SIZE_SHRINK_BEGIN. As such, this value is always implicitly allowed.

void fit_child_in_rect(child: Control, rect: Rect2) 🔗

Fit a child control in a given rect. This is mainly a helper for creating custom container classes.

Queue resort of the contained children. This is called automatically anyway, but can be called upon request.

Please read the User-contributed notes policy before submitting a comment.

---

## Controllers, gamepads, and joysticks

**URL:** https://docs.godotengine.org/en/stable/tutorials/inputs/controllers_gamepads_joysticks.html

**Contents:**
- Controllers, gamepads, and joysticks
- Supporting universal input
  - Which Input singleton method should I use?
- Vibration
- Differences between keyboard/mouse and controller input
  - Dead zone
  - "Echo" events
  - Window focus
  - Power saving prevention
- Troubleshooting

Godot supports hundreds of controller models out of the box. Controllers are supported on Windows, macOS, Linux, Android, iOS, and Web.

Since Godot 4.5, the engine relies on SDL 3 for controller support on Windows, macOS, and Linux. This means the list of supported controllers and their behavior should closely match what is available in other games and engines using SDL 3. Note that SDL is only used for input, not for windowing or sound.

Prior to Godot 4.5, the engine used its own controller support code. This can cause certain controllers to behave incorrectly. This custom code is still used to support controllers on Android, iOS, and Web, so it may result in issues appearing only on those platforms.

Note that more specialized devices such as steering wheels, rudder pedals and HOTAS are less tested and may not always work as expected. Overriding force feedback for those devices is also not implemented yet. If you have access to one of those devices, don't hesitate to report bugs on GitHub.

In this guide, you will learn:

How to write your input logic to support both keyboard and controller inputs.

How controllers can behave differently from keyboard/mouse input.

Troubleshooting issues with controllers in Godot.

Thanks to Godot's input action system, Godot makes it possible to support both keyboard and controller input without having to write separate code paths. Instead of hardcoding keys or controller buttons in your scripts, you should create input actions in the Project Settings which will then refer to specified key and controller inputs.

Input actions are explained in detail on the Using InputEvent page.

Unlike keyboard input, supporting both mouse and controller input for an action (such as looking around in a first-person game) will require different code paths since these have to be handled separately.

There are 3 ways to get input in an analog-aware way:

When you have two axes (such as joystick or WASD movement) and want both axes to behave as a single input, use Input.get_vector():

When you have one axis that can go both ways (such as a throttle on a flight stick), or when you want to handle separate axes individually, use Input.get_axis():

For other types of analog input, such as handling a trigger or handling one direction at a time, use Input.get_action_strength():

For non-analog digital/boolean input (only "pressed" or "not pressed" values), such as controller buttons, mouse buttons or keyboard keys, use Input.is_action_pressed():

If you need to know whether an input was just pressed in the previous frame, use Input.is_action_just_pressed() instead of Input.is_action_pressed(). Unlike Input.is_action_pressed() which returns true as long as the input is held, Input.is_action_just_pressed() will only return true for one frame after the button has been pressed.

Vibration (also called haptic feedback) can be used to enhance the feel of a game. For instance, in a racing game, you can convey the surface the car is currently driving on through vibration, or create a sudden vibration on a crash.

Use the Input singleton's start_joy_vibration method to start vibrating a gamepad. Use stop_joy_vibration to stop vibration early (useful if no duration was specified when starting).

On mobile devices, you can also use vibrate_handheld to vibrate the device itself (independently from the gamepad). On Android, this requires the VIBRATE permission to be enabled in the Android export preset before exporting the project.

Vibration can be uncomfortable for certain players. Make sure to provide an in-game slider to disable vibration or reduce its intensity.

If you're used to handling keyboard and mouse input, you may be surprised by how controllers handle specific situations.

Unlike keyboards and mice, controllers offer axes with analog inputs. The upside of analog inputs is that they offer additional flexibility for actions. Unlike digital inputs which can only provide strengths of 0.0 and 1.0, an analog input can provide any strength between 0.0 and 1.0. The downside is that without a deadzone system, an analog axis' strength will never be equal to 0.0 due to how the controller is physically built. Instead, it will linger at a low value such as 0.062. This phenomenon is known as drifting and can be more noticeable on old or faulty controllers.

Let's take a racing game as a real-world example. Thanks to analog inputs, we can steer the car slowly in one direction or another. However, without a deadzone system, the car would slowly steer by itself even if the player isn't touching the joystick. This is because the directional axis strength won't be equal to 0.0 when we expect it to. Since we don't want our car to steer by itself in this case, we define a "dead zone" value of 0.2 which will ignore all input whose strength is lower than 0.2. An ideal dead zone value is high enough to ignore the input caused by joystick drifting, but is low enough to not ignore actual input from the player.

Godot features a built-in deadzone system to tackle this problem. The default value is 0.5, but you can adjust it on a per-action basis in the Project Settings' Input Map tab. For Input.get_vector(), the deadzone can be specified as an optional 5th parameter. If not specified, it will calculate the average deadzone value from all of the actions in the vector.

Unlike keyboard input, holding down a controller button such as a D-pad direction will not generate repeated input events at fixed intervals (also known as "echo" events). This is because the operating system never sends "echo" events for controller input in the first place.

If you want controller buttons to send echo events, you will have to generate InputEvent objects by code and parse them using Input.parse_input_event() at regular intervals. This can be accomplished with the help of a Timer node.

Unlike keyboard input, controller inputs can be seen by all windows on the operating system, including unfocused windows.

While this is useful for third-party split screen functionality, it can also have adverse effects. Players may accidentally send controller inputs to the running project while interacting with another window.

If you wish to ignore events when the project window isn't focused, you will need to create an autoload called Focus with the following script and use it to check all your inputs:

Then, instead of using Input.is_action_pressed(action), use Focus.input_is_action_pressed(action) where action is the name of the input action. Also, instead of using event.is_action_pressed(action), use Focus.event_is_action_pressed(event, action) where event is an InputEvent reference and action is the name of the input action.

Unlike keyboard and mouse input, controller inputs do not inhibit sleep and power saving measures (such as turning off the screen after a certain amount of time has passed).

To combat this, Godot enables power saving prevention by default when a project is running. If you notice the system is turning off its display when playing with a gamepad, check the value of Display > Window > Energy Saving > Keep Screen On in the Project Settings.

On Linux, power saving prevention requires the engine to be able to use D-Bus. Check whether D-Bus is installed and reachable if running the project within a Flatpak, as sandboxing restrictions may make this impossible by default.

You can view a list of known issues with controller support on GitHub.

First, check that your controller is recognized by other applications. You can use the Gamepad Tester website to confirm that your controller is recognized.

On Windows Godot only supports up to 4 controllers at a time. This is because Godot uses the XInput API, which is limited to supporting 4 controllers at once. Additional controllers above this limit are ignored by Godot.

First, if your controller provides some kind of firmware update utility, make sure to run it to get the latest fixes from the manufacturer. For instance, Xbox One and Xbox Series controllers can have their firmware updated using the Xbox Accessories app. (This application only runs on Windows, so you have to use a Windows machine or a Windows virtual machine with USB support to update the controller's firmware.) After updating the controller's firmware, unpair the controller and pair it again with your PC if you are using the controller in wireless mode.

If buttons are incorrectly mapped, this may be due to an erroneous mapping from the SDL game controller database used by Godot or the Godot game controller database. In this case, you will need to create a custom mapping for your controller.

There are many ways to create mappings. One option is to use the mapping wizard in the official Joypads demo. Once you have a working mapping for your controller, you can test it by defining the SDL_GAMECONTROLLERCONFIG environment variable before running Godot:

To test mappings on non-desktop platforms or to distribute your project with additional controller mappings, you can add them by calling Input.add_joy_mapping() as early as possible in a script's _ready() function.

Once you are satisfied with the custom mapping, you can contribute it for the next Godot version by opening a pull request on the Godot game controller database.

If you're using a self-compiled engine binary, make sure it was compiled with udev support. This is enabled by default, but it is possible to disable udev support by specifying udev=no on the SCons command line. If you're using an engine binary supplied by a Linux distribution, double-check whether it was compiled with udev support.

Controllers can still work without udev support, but it is less reliable as regular polling must be used to check for controllers being connected or disconnected during gameplay (hotplugging).

As described at the top of the page, controller support on mobile platforms relies on a custom implementation instead of using SDL for input. This means controller support may be less reliable than on desktop platforms.

Support for SDL-based controller input on mobile platforms is planned in a future release.

Web controller support is often less reliable compared to "native" platforms. The quality of controller support tends to vary wildly across browsers. As a result, you may have to instruct your players to use a different browser if they can't get their controller to work.

Like for mobile platforms, support for SDL-based controller input on the web platform is planned in a future release.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
# `velocity` will be a Vector2 between `Vector2(-1.0, -1.0)` and `Vector2(1.0, 1.0)`.
# This handles deadzone in a correct way for most use cases.
# The resulting deadzone will have a circular shape as it generally should.
var velocity = Input.get_vector("move_left", "move_right", "move_forward", "move_back")

# The line below is similar to `get_vector()`, except that it handles
# the deadzone in a less optimal way. The resulting deadzone will have
# a square-ish shape when it should ideally have a circular shape.
var velocity = Vector2(
        Input.get_action_strength("move_right") - Input.get_action_strength("move_left"),
        Input.get_action_strength("move_back") - Input.get_action_strength("move_forward")
).limit_length(1.0)
```

Example 2 (csharp):
```csharp
// `velocity` will be a Vector2 between `Vector2(-1.0, -1.0)` and `Vector2(1.0, 1.0)`.
// This handles deadzone in a correct way for most use cases.
// The resulting deadzone will have a circular shape as it generally should.
Vector2 velocity = Input.GetVector("move_left", "move_right", "move_forward", "move_back");

// The line below is similar to `get_vector()`, except that it handles
// the deadzone in a less optimal way. The resulting deadzone will have
// a square-ish shape when it should ideally have a circular shape.
Vector2 velocity = new Vector2(
        Input.GetActionStrength("move_right") - Input.GetActionStrength("move_left"),
        Input.GetActionStrength("move_back") - Input.GetActionStrength("move_forward")
).LimitLength(1.0);
```

Example 3 (csharp):
```csharp
# `walk` will be a floating-point number between `-1.0` and `1.0`.
var walk = Input.get_axis("move_left", "move_right")

# The line above is a shorter form of:
var walk = Input.get_action_strength("move_right") - Input.get_action_strength("move_left")
```

Example 4 (csharp):
```csharp
// `walk` will be a floating-point number between `-1.0` and `1.0`.
float walk = Input.GetAxis("move_left", "move_right");

// The line above is a shorter form of:
float walk = Input.GetActionStrength("move_right") - Input.GetActionStrength("move_left");
```

---

## Control

**URL:** https://docs.godotengine.org/en/stable/classes/class_control.html

**Contents:**
- Control
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Constants
- Property Descriptions
- Method Descriptions

Inherits: CanvasItem < Node < Object

Inherited By: BaseButton, ColorRect, Container, GraphEdit, ItemList, Label, LineEdit, MenuBar, NinePatchRect, Panel, Range, ReferenceRect, RichTextLabel, Separator, TabBar, TextEdit, TextureRect, Tree, VideoStreamPlayer

Base class for all GUI controls. Adapts its position and size based on its parent control.

Base class for all UI-related nodes. Control features a bounding rectangle that defines its extents, an anchor position relative to its parent control or the current viewport, and offsets relative to the anchor. The offsets update automatically when the node, any of its parents, or the screen size change.

For more information on Godot's UI system, anchors, offsets, and containers, see the related tutorials in the manual. To build flexible UIs, you'll need a mix of UI elements that inherit from Control and Container nodes.

Note: Since both Node2D and Control inherit from CanvasItem, they share several concepts from the class such as the CanvasItem.z_index and CanvasItem.visible properties.

User Interface nodes and input

Godot propagates input events via viewports. Each Viewport is responsible for propagating InputEvents to their child nodes. As the SceneTree.root is a Window, this already happens automatically for all UI elements in your game.

Input events are propagated through the SceneTree from the root node to all child nodes by calling Node._input(). For UI elements specifically, it makes more sense to override the virtual method _gui_input(), which filters out unrelated input events, such as by checking z-order, mouse_filter, focus, or if the event was inside of the control's bounding box.

Call accept_event() so no other node receives the event. Once you accept an input, it becomes handled so Node._unhandled_input() will not process it.

Only one Control node can be in focus. Only the node in focus will receive events. To get the focus, call grab_focus(). Control nodes lose focus when another node grabs it, or if you hide the node in focus.

Sets mouse_filter to MOUSE_FILTER_IGNORE to tell a Control node to ignore mouse or touch events. You'll need it if you place an icon on top of a button.

Theme resources change the control's appearance. The theme of a Control node affects all of its direct and indirect children (as long as a chain of controls is uninterrupted). To override some of the theme items, call one of the add_theme_*_override methods, like add_theme_font_override(). You can also override theme items in the Inspector.

Note: Theme items are not Object properties. This means you can't access their values using Object.get() and Object.set(). Instead, use the get_theme_* and add_theme_*_override methods provided by this class.

GUI documentation index

accessibility_controls_nodes

accessibility_described_by_nodes

accessibility_description

accessibility_flow_to_nodes

accessibility_labeled_by_nodes

AccessibilityLiveMode

FocusBehaviorRecursive

focus_behavior_recursive

focus_neighbor_bottom

localize_numeral_system

MouseBehaviorRecursive

mouse_behavior_recursive

mouse_default_cursor_shape

mouse_force_pass_scroll_events

PhysicsInterpolationMode

physics_interpolation_mode

size_flags_horizontal

size_flags_stretch_ratio

tooltip_auto_translate_mode

_accessibility_get_contextual_info() virtual const

_can_drop_data(at_position: Vector2, data: Variant) virtual const

_drop_data(at_position: Vector2, data: Variant) virtual

_get_accessibility_container_name(node: Node) virtual const

_get_drag_data(at_position: Vector2) virtual

_get_minimum_size() virtual const

_get_tooltip(at_position: Vector2) virtual const

_gui_input(event: InputEvent) virtual

_has_point(point: Vector2) virtual const

_make_custom_tooltip(for_text: String) virtual const

_structured_text_parser(args: Array, text: String) virtual const

add_theme_color_override(name: StringName, color: Color)

add_theme_constant_override(name: StringName, constant: int)

add_theme_font_override(name: StringName, font: Font)

add_theme_font_size_override(name: StringName, font_size: int)

add_theme_icon_override(name: StringName, texture: Texture2D)

add_theme_stylebox_override(name: StringName, stylebox: StyleBox)

begin_bulk_theme_override()

end_bulk_theme_override()

find_next_valid_focus() const

find_prev_valid_focus() const

find_valid_focus_neighbor(side: Side) const

force_drag(data: Variant, preview: Control)

get_anchor(side: Side) const

get_combined_minimum_size() const

get_cursor_shape(position: Vector2 = Vector2(0, 0)) const

get_focus_mode_with_override() const

get_focus_neighbor(side: Side) const

get_global_rect() const

get_minimum_size() const

get_mouse_filter_with_override() const

get_offset(offset: Side) const

get_parent_area_size() const

get_parent_control() const

get_screen_position() const

get_theme_color(name: StringName, theme_type: StringName = &"") const

get_theme_constant(name: StringName, theme_type: StringName = &"") const

get_theme_default_base_scale() const

get_theme_default_font() const

get_theme_default_font_size() const

get_theme_font(name: StringName, theme_type: StringName = &"") const

get_theme_font_size(name: StringName, theme_type: StringName = &"") const

get_theme_icon(name: StringName, theme_type: StringName = &"") const

get_theme_stylebox(name: StringName, theme_type: StringName = &"") const

get_tooltip(at_position: Vector2 = Vector2(0, 0)) const

has_theme_color(name: StringName, theme_type: StringName = &"") const

has_theme_color_override(name: StringName) const

has_theme_constant(name: StringName, theme_type: StringName = &"") const

has_theme_constant_override(name: StringName) const

has_theme_font(name: StringName, theme_type: StringName = &"") const

has_theme_font_override(name: StringName) const

has_theme_font_size(name: StringName, theme_type: StringName = &"") const

has_theme_font_size_override(name: StringName) const

has_theme_icon(name: StringName, theme_type: StringName = &"") const

has_theme_icon_override(name: StringName) const

has_theme_stylebox(name: StringName, theme_type: StringName = &"") const

has_theme_stylebox_override(name: StringName) const

is_drag_successful() const

is_layout_rtl() const

remove_theme_color_override(name: StringName)

remove_theme_constant_override(name: StringName)

remove_theme_font_override(name: StringName)

remove_theme_font_size_override(name: StringName)

remove_theme_icon_override(name: StringName)

remove_theme_stylebox_override(name: StringName)

set_anchor(side: Side, anchor: float, keep_offset: bool = false, push_opposite_anchor: bool = true)

set_anchor_and_offset(side: Side, anchor: float, offset: float, push_opposite_anchor: bool = false)

set_anchors_and_offsets_preset(preset: LayoutPreset, resize_mode: LayoutPresetMode = 0, margin: int = 0)

set_anchors_preset(preset: LayoutPreset, keep_offsets: bool = false)

set_begin(position: Vector2)

set_drag_forwarding(drag_func: Callable, can_drop_func: Callable, drop_func: Callable)

set_drag_preview(control: Control)

set_end(position: Vector2)

set_focus_neighbor(side: Side, neighbor: NodePath)

set_global_position(position: Vector2, keep_offsets: bool = false)

set_offset(side: Side, offset: float)

set_offsets_preset(preset: LayoutPreset, resize_mode: LayoutPresetMode = 0, margin: int = 0)

set_position(position: Vector2, keep_offsets: bool = false)

set_size(size: Vector2, keep_offsets: bool = false)

update_minimum_size()

warp_mouse(position: Vector2)

Emitted when the node gains focus.

Emitted when the node loses focus.

gui_input(event: InputEvent) 🔗

Emitted when the node receives an InputEvent.

minimum_size_changed() 🔗

Emitted when the node's minimum size changes.

Emitted when the mouse cursor enters the control's (or any child control's) visible area, that is not occluded behind other Controls or Windows, provided its mouse_filter lets the event reach it and regardless if it's currently focused or not.

Note: CanvasItem.z_index doesn't affect, which Control receives the signal.

Emitted when the mouse cursor leaves the control's (and all child control's) visible area, that is not occluded behind other Controls or Windows, provided its mouse_filter lets the event reach it and regardless if it's currently focused or not.

Note: CanvasItem.z_index doesn't affect, which Control receives the signal.

Note: If you want to check whether the mouse truly left the area, ignoring any top nodes, you can use code like this:

Emitted when the control changes size.

size_flags_changed() 🔗

Emitted when one of the size flags changes. See size_flags_horizontal and size_flags_vertical.

Emitted when the NOTIFICATION_THEME_CHANGED notification is sent.

FocusMode FOCUS_NONE = 0

The node cannot grab focus. Use with focus_mode.

FocusMode FOCUS_CLICK = 1

The node can only grab focus on mouse clicks. Use with focus_mode.

FocusMode FOCUS_ALL = 2

The node can grab focus on mouse click, using the arrows and the Tab keys on the keyboard, or using the D-pad buttons on a gamepad. Use with focus_mode.

FocusMode FOCUS_ACCESSIBILITY = 3

The node can grab focus only when screen reader is active. Use with focus_mode.

enum FocusBehaviorRecursive: 🔗

FocusBehaviorRecursive FOCUS_BEHAVIOR_INHERITED = 0

Inherits the focus_behavior_recursive from the parent control. If there is no parent control, this is the same as FOCUS_BEHAVIOR_ENABLED.

FocusBehaviorRecursive FOCUS_BEHAVIOR_DISABLED = 1

Prevents the control from getting focused. get_focus_mode_with_override() will return FOCUS_NONE.

FocusBehaviorRecursive FOCUS_BEHAVIOR_ENABLED = 2

Allows the control to be focused, depending on the focus_mode. This can be used to ignore the parent's focus_behavior_recursive. get_focus_mode_with_override() will return the focus_mode.

enum MouseBehaviorRecursive: 🔗

MouseBehaviorRecursive MOUSE_BEHAVIOR_INHERITED = 0

Inherits the mouse_behavior_recursive from the parent control. If there is no parent control, this is the same as MOUSE_BEHAVIOR_ENABLED.

MouseBehaviorRecursive MOUSE_BEHAVIOR_DISABLED = 1

Prevents the control from receiving mouse input. get_mouse_filter_with_override() will return MOUSE_FILTER_IGNORE.

MouseBehaviorRecursive MOUSE_BEHAVIOR_ENABLED = 2

Allows the control to be receive mouse input, depending on the mouse_filter. This can be used to ignore the parent's mouse_behavior_recursive. get_mouse_filter_with_override() will return the mouse_filter.

CursorShape CURSOR_ARROW = 0

Show the system's arrow mouse cursor when the user hovers the node. Use with mouse_default_cursor_shape.

CursorShape CURSOR_IBEAM = 1

Show the system's I-beam mouse cursor when the user hovers the node. The I-beam pointer has a shape similar to "I". It tells the user they can highlight or insert text.

CursorShape CURSOR_POINTING_HAND = 2

Show the system's pointing hand mouse cursor when the user hovers the node.

CursorShape CURSOR_CROSS = 3

Show the system's cross mouse cursor when the user hovers the node.

CursorShape CURSOR_WAIT = 4

Show the system's wait mouse cursor when the user hovers the node. Often an hourglass.

CursorShape CURSOR_BUSY = 5

Show the system's busy mouse cursor when the user hovers the node. Often an arrow with a small hourglass.

CursorShape CURSOR_DRAG = 6

Show the system's drag mouse cursor, often a closed fist or a cross symbol, when the user hovers the node. It tells the user they're currently dragging an item, like a node in the Scene dock.

CursorShape CURSOR_CAN_DROP = 7

Show the system's drop mouse cursor when the user hovers the node. It can be an open hand. It tells the user they can drop an item they're currently grabbing, like a node in the Scene dock.

CursorShape CURSOR_FORBIDDEN = 8

Show the system's forbidden mouse cursor when the user hovers the node. Often a crossed circle.

CursorShape CURSOR_VSIZE = 9

Show the system's vertical resize mouse cursor when the user hovers the node. A double-headed vertical arrow. It tells the user they can resize the window or the panel vertically.

CursorShape CURSOR_HSIZE = 10

Show the system's horizontal resize mouse cursor when the user hovers the node. A double-headed horizontal arrow. It tells the user they can resize the window or the panel horizontally.

CursorShape CURSOR_BDIAGSIZE = 11

Show the system's window resize mouse cursor when the user hovers the node. The cursor is a double-headed arrow that goes from the bottom left to the top right. It tells the user they can resize the window or the panel both horizontally and vertically.

CursorShape CURSOR_FDIAGSIZE = 12

Show the system's window resize mouse cursor when the user hovers the node. The cursor is a double-headed arrow that goes from the top left to the bottom right, the opposite of CURSOR_BDIAGSIZE. It tells the user they can resize the window or the panel both horizontally and vertically.

CursorShape CURSOR_MOVE = 13

Show the system's move mouse cursor when the user hovers the node. It shows 2 double-headed arrows at a 90 degree angle. It tells the user they can move a UI element freely.

CursorShape CURSOR_VSPLIT = 14

Show the system's vertical split mouse cursor when the user hovers the node. On Windows, it's the same as CURSOR_VSIZE.

CursorShape CURSOR_HSPLIT = 15

Show the system's horizontal split mouse cursor when the user hovers the node. On Windows, it's the same as CURSOR_HSIZE.

CursorShape CURSOR_HELP = 16

Show the system's help mouse cursor when the user hovers the node, a question mark.

LayoutPreset PRESET_TOP_LEFT = 0

Snap all 4 anchors to the top-left of the parent control's bounds. Use with set_anchors_preset().

LayoutPreset PRESET_TOP_RIGHT = 1

Snap all 4 anchors to the top-right of the parent control's bounds. Use with set_anchors_preset().

LayoutPreset PRESET_BOTTOM_LEFT = 2

Snap all 4 anchors to the bottom-left of the parent control's bounds. Use with set_anchors_preset().

LayoutPreset PRESET_BOTTOM_RIGHT = 3

Snap all 4 anchors to the bottom-right of the parent control's bounds. Use with set_anchors_preset().

LayoutPreset PRESET_CENTER_LEFT = 4

Snap all 4 anchors to the center of the left edge of the parent control's bounds. Use with set_anchors_preset().

LayoutPreset PRESET_CENTER_TOP = 5

Snap all 4 anchors to the center of the top edge of the parent control's bounds. Use with set_anchors_preset().

LayoutPreset PRESET_CENTER_RIGHT = 6

Snap all 4 anchors to the center of the right edge of the parent control's bounds. Use with set_anchors_preset().

LayoutPreset PRESET_CENTER_BOTTOM = 7

Snap all 4 anchors to the center of the bottom edge of the parent control's bounds. Use with set_anchors_preset().

LayoutPreset PRESET_CENTER = 8

Snap all 4 anchors to the center of the parent control's bounds. Use with set_anchors_preset().

LayoutPreset PRESET_LEFT_WIDE = 9

Snap all 4 anchors to the left edge of the parent control. The left offset becomes relative to the left edge and the top offset relative to the top left corner of the node's parent. Use with set_anchors_preset().

LayoutPreset PRESET_TOP_WIDE = 10

Snap all 4 anchors to the top edge of the parent control. The left offset becomes relative to the top left corner, the top offset relative to the top edge, and the right offset relative to the top right corner of the node's parent. Use with set_anchors_preset().

LayoutPreset PRESET_RIGHT_WIDE = 11

Snap all 4 anchors to the right edge of the parent control. The right offset becomes relative to the right edge and the top offset relative to the top right corner of the node's parent. Use with set_anchors_preset().

LayoutPreset PRESET_BOTTOM_WIDE = 12

Snap all 4 anchors to the bottom edge of the parent control. The left offset becomes relative to the bottom left corner, the bottom offset relative to the bottom edge, and the right offset relative to the bottom right corner of the node's parent. Use with set_anchors_preset().

LayoutPreset PRESET_VCENTER_WIDE = 13

Snap all 4 anchors to a vertical line that cuts the parent control in half. Use with set_anchors_preset().

LayoutPreset PRESET_HCENTER_WIDE = 14

Snap all 4 anchors to a horizontal line that cuts the parent control in half. Use with set_anchors_preset().

LayoutPreset PRESET_FULL_RECT = 15

Snap all 4 anchors to the respective corners of the parent control. Set all 4 offsets to 0 after you applied this preset and the Control will fit its parent control. Use with set_anchors_preset().

enum LayoutPresetMode: 🔗

LayoutPresetMode PRESET_MODE_MINSIZE = 0

The control will be resized to its minimum size.

LayoutPresetMode PRESET_MODE_KEEP_WIDTH = 1

The control's width will not change.

LayoutPresetMode PRESET_MODE_KEEP_HEIGHT = 2

The control's height will not change.

LayoutPresetMode PRESET_MODE_KEEP_SIZE = 3

The control's size will not change.

SizeFlags SIZE_SHRINK_BEGIN = 0

Tells the parent Container to align the node with its start, either the top or the left edge. It is mutually exclusive with SIZE_FILL and other shrink size flags, but can be used with SIZE_EXPAND in some containers. Use with size_flags_horizontal and size_flags_vertical.

Note: Setting this flag is equal to not having any size flags.

SizeFlags SIZE_FILL = 1

Tells the parent Container to expand the bounds of this node to fill all the available space without pushing any other node. It is mutually exclusive with shrink size flags. Use with size_flags_horizontal and size_flags_vertical.

SizeFlags SIZE_EXPAND = 2

Tells the parent Container to let this node take all the available space on the axis you flag. If multiple neighboring nodes are set to expand, they'll share the space based on their stretch ratio. See size_flags_stretch_ratio. Use with size_flags_horizontal and size_flags_vertical.

SizeFlags SIZE_EXPAND_FILL = 3

Sets the node's size flags to both fill and expand. See SIZE_FILL and SIZE_EXPAND for more information.

SizeFlags SIZE_SHRINK_CENTER = 4

Tells the parent Container to center the node in the available space. It is mutually exclusive with SIZE_FILL and other shrink size flags, but can be used with SIZE_EXPAND in some containers. Use with size_flags_horizontal and size_flags_vertical.

SizeFlags SIZE_SHRINK_END = 8

Tells the parent Container to align the node with its end, either the bottom or the right edge. It is mutually exclusive with SIZE_FILL and other shrink size flags, but can be used with SIZE_EXPAND in some containers. Use with size_flags_horizontal and size_flags_vertical.

MouseFilter MOUSE_FILTER_STOP = 0

The control will receive mouse movement input events and mouse button input events if clicked on through _gui_input(). The control will also receive the mouse_entered and mouse_exited signals. These events are automatically marked as handled, and they will not propagate further to other controls. This also results in blocking signals in other controls.

MouseFilter MOUSE_FILTER_PASS = 1

The control will receive mouse movement input events and mouse button input events if clicked on through _gui_input(). The control will also receive the mouse_entered and mouse_exited signals.

If this control does not handle the event, the event will propagate up to its parent control if it has one. The event is bubbled up the node hierarchy until it reaches a non-CanvasItem, a control with MOUSE_FILTER_STOP, or a CanvasItem with CanvasItem.top_level enabled. This will allow signals to fire in all controls it reaches. If no control handled it, the event will be passed to Node._shortcut_input() for further processing.

MouseFilter MOUSE_FILTER_IGNORE = 2

The control will not receive any mouse movement input events nor mouse button input events through _gui_input(). The control will also not receive the mouse_entered nor mouse_exited signals. This will not block other controls from receiving these events or firing the signals. Ignored events will not be handled automatically. If a child has MOUSE_FILTER_PASS and an event was passed to this control, the event will further propagate up to the control's parent.

Note: If the control has received mouse_entered but not mouse_exited, changing the mouse_filter to MOUSE_FILTER_IGNORE will cause mouse_exited to be emitted.

enum GrowDirection: 🔗

GrowDirection GROW_DIRECTION_BEGIN = 0

The control will grow to the left or top to make up if its minimum size is changed to be greater than its current size on the respective axis.

GrowDirection GROW_DIRECTION_END = 1

The control will grow to the right or bottom to make up if its minimum size is changed to be greater than its current size on the respective axis.

GrowDirection GROW_DIRECTION_BOTH = 2

The control will grow in both directions equally to make up if its minimum size is changed to be greater than its current size.

Anchor ANCHOR_BEGIN = 0

Snaps one of the 4 anchor's sides to the origin of the node's Rect, in the top left. Use it with one of the anchor_* member variables, like anchor_left. To change all 4 anchors at once, use set_anchors_preset().

Anchor ANCHOR_END = 1

Snaps one of the 4 anchor's sides to the end of the node's Rect, in the bottom right. Use it with one of the anchor_* member variables, like anchor_left. To change all 4 anchors at once, use set_anchors_preset().

enum LayoutDirection: 🔗

LayoutDirection LAYOUT_DIRECTION_INHERITED = 0

Automatic layout direction, determined from the parent control layout direction.

LayoutDirection LAYOUT_DIRECTION_APPLICATION_LOCALE = 1

Automatic layout direction, determined from the current locale. Right-to-left layout direction is automatically used for languages that require it such as Arabic and Hebrew, but only if a valid translation file is loaded for the given language (unless said language is configured as a fallback in ProjectSettings.internationalization/locale/fallback). For all other languages (or if no valid translation file is found by Godot), left-to-right layout direction is used. If using TextServerFallback (ProjectSettings.internationalization/rendering/text_driver), left-to-right layout direction is always used regardless of the language. Right-to-left layout direction can also be forced using ProjectSettings.internationalization/rendering/force_right_to_left_layout_direction.

LayoutDirection LAYOUT_DIRECTION_LTR = 2

Left-to-right layout direction.

LayoutDirection LAYOUT_DIRECTION_RTL = 3

Right-to-left layout direction.

LayoutDirection LAYOUT_DIRECTION_SYSTEM_LOCALE = 4

Automatic layout direction, determined from the system locale. Right-to-left layout direction is automatically used for languages that require it such as Arabic and Hebrew, but only if a valid translation file is loaded for the given language. For all other languages (or if no valid translation file is found by Godot), left-to-right layout direction is used. If using TextServerFallback (ProjectSettings.internationalization/rendering/text_driver), left-to-right layout direction is always used regardless of the language.

LayoutDirection LAYOUT_DIRECTION_MAX = 5

Represents the size of the LayoutDirection enum.

LayoutDirection LAYOUT_DIRECTION_LOCALE = 1

Deprecated: Use LAYOUT_DIRECTION_APPLICATION_LOCALE instead.

enum TextDirection: 🔗

TextDirection TEXT_DIRECTION_INHERITED = 3

Text writing direction is the same as layout direction.

TextDirection TEXT_DIRECTION_AUTO = 0

Automatic text writing direction, determined from the current locale and text content.

TextDirection TEXT_DIRECTION_LTR = 1

Left-to-right text writing direction.

TextDirection TEXT_DIRECTION_RTL = 2

Right-to-left text writing direction.

NOTIFICATION_RESIZED = 40 🔗

Sent when the node changes size. Use size to get the new size.

NOTIFICATION_MOUSE_ENTER = 41 🔗

Sent when the mouse cursor enters the control's (or any child control's) visible area, that is not occluded behind other Controls or Windows, provided its mouse_filter lets the event reach it and regardless if it's currently focused or not.

Note: CanvasItem.z_index doesn't affect which Control receives the notification.

See also NOTIFICATION_MOUSE_ENTER_SELF.

NOTIFICATION_MOUSE_EXIT = 42 🔗

Sent when the mouse cursor leaves the control's (and all child control's) visible area, that is not occluded behind other Controls or Windows, provided its mouse_filter lets the event reach it and regardless if it's currently focused or not.

Note: CanvasItem.z_index doesn't affect which Control receives the notification.

See also NOTIFICATION_MOUSE_EXIT_SELF.

NOTIFICATION_MOUSE_ENTER_SELF = 60 🔗

Experimental: The reason this notification is sent may change in the future.

Sent when the mouse cursor enters the control's visible area, that is not occluded behind other Controls or Windows, provided its mouse_filter lets the event reach it and regardless if it's currently focused or not.

Note: CanvasItem.z_index doesn't affect which Control receives the notification.

See also NOTIFICATION_MOUSE_ENTER.

NOTIFICATION_MOUSE_EXIT_SELF = 61 🔗

Experimental: The reason this notification is sent may change in the future.

Sent when the mouse cursor leaves the control's visible area, that is not occluded behind other Controls or Windows, provided its mouse_filter lets the event reach it and regardless if it's currently focused or not.

Note: CanvasItem.z_index doesn't affect which Control receives the notification.

See also NOTIFICATION_MOUSE_EXIT.

NOTIFICATION_FOCUS_ENTER = 43 🔗

Sent when the node grabs focus.

NOTIFICATION_FOCUS_EXIT = 44 🔗

Sent when the node loses focus.

NOTIFICATION_THEME_CHANGED = 45 🔗

Sent when the node needs to refresh its theme items. This happens in one of the following cases:

The theme property is changed on this node or any of its ancestors.

The theme_type_variation property is changed on this node.

One of the node's theme property overrides is changed.

The node enters the scene tree.

Note: As an optimization, this notification won't be sent from changes that occur while this node is outside of the scene tree. Instead, all of the theme item updates can be applied at once when the node enters the scene tree.

Note: This notification is received alongside Node.NOTIFICATION_ENTER_TREE, so if you are instantiating a scene, the child nodes will not be initialized yet. You can use it to setup theming for this node, child nodes created from script, or if you want to access child nodes added in the editor, make sure the node is ready using Node.is_node_ready().

NOTIFICATION_SCROLL_BEGIN = 47 🔗

Sent when this node is inside a ScrollContainer which has begun being scrolled when dragging the scrollable area with a touch event. This notification is not sent when scrolling by dragging the scrollbar, scrolling with the mouse wheel or scrolling with keyboard/gamepad events.

Note: This signal is only emitted on Android or iOS, or on desktop/web platforms when ProjectSettings.input_devices/pointing/emulate_touch_from_mouse is enabled.

NOTIFICATION_SCROLL_END = 48 🔗

Sent when this node is inside a ScrollContainer which has stopped being scrolled when dragging the scrollable area with a touch event. This notification is not sent when scrolling by dragging the scrollbar, scrolling with the mouse wheel or scrolling with keyboard/gamepad events.

Note: This signal is only emitted on Android or iOS, or on desktop/web platforms when ProjectSettings.input_devices/pointing/emulate_touch_from_mouse is enabled.

NOTIFICATION_LAYOUT_DIRECTION_CHANGED = 49 🔗

Sent when the control layout direction is changed from LTR or RTL or vice versa. This notification is propagated to child Control nodes as result of a change to layout_direction.

Array[NodePath] accessibility_controls_nodes = [] 🔗

void set_accessibility_controls_nodes(value: Array[NodePath])

Array[NodePath] get_accessibility_controls_nodes()

The paths to the nodes which are controlled by this node.

Array[NodePath] accessibility_described_by_nodes = [] 🔗

void set_accessibility_described_by_nodes(value: Array[NodePath])

Array[NodePath] get_accessibility_described_by_nodes()

The paths to the nodes which are describing this node.

String accessibility_description = "" 🔗

void set_accessibility_description(value: String)

String get_accessibility_description()

The human-readable node description that is reported to assistive apps.

Array[NodePath] accessibility_flow_to_nodes = [] 🔗

void set_accessibility_flow_to_nodes(value: Array[NodePath])

Array[NodePath] get_accessibility_flow_to_nodes()

The paths to the nodes which this node flows into.

Array[NodePath] accessibility_labeled_by_nodes = [] 🔗

void set_accessibility_labeled_by_nodes(value: Array[NodePath])

Array[NodePath] get_accessibility_labeled_by_nodes()

The paths to the nodes which label this node.

AccessibilityLiveMode accessibility_live = 0 🔗

void set_accessibility_live(value: AccessibilityLiveMode)

AccessibilityLiveMode get_accessibility_live()

The mode with which a live region updates. A live region is a Node that is updated as a result of an external event when the user's focus may be elsewhere.

String accessibility_name = "" 🔗

void set_accessibility_name(value: String)

String get_accessibility_name()

The human-readable node name that is reported to assistive apps.

float anchor_bottom = 0.0 🔗

float get_anchor(side: Side) const

Anchors the bottom edge of the node to the origin, the center, or the end of its parent control. It changes how the bottom offset updates when the node moves or changes size. You can use one of the Anchor constants for convenience.

float anchor_left = 0.0 🔗

float get_anchor(side: Side) const

Anchors the left edge of the node to the origin, the center or the end of its parent control. It changes how the left offset updates when the node moves or changes size. You can use one of the Anchor constants for convenience.

float anchor_right = 0.0 🔗

float get_anchor(side: Side) const

Anchors the right edge of the node to the origin, the center or the end of its parent control. It changes how the right offset updates when the node moves or changes size. You can use one of the Anchor constants for convenience.

float anchor_top = 0.0 🔗

float get_anchor(side: Side) const

Anchors the top edge of the node to the origin, the center or the end of its parent control. It changes how the top offset updates when the node moves or changes size. You can use one of the Anchor constants for convenience.

bool auto_translate 🔗

void set_auto_translate(value: bool)

bool is_auto_translating()

Deprecated: Use Node.auto_translate_mode and Node.can_auto_translate() instead.

Toggles if any text should automatically change to its translated version depending on the current locale.

bool clip_contents = false 🔗

void set_clip_contents(value: bool)

bool is_clipping_contents()

Enables whether rendering of CanvasItem based children should be clipped to this control's rectangle. If true, parts of a child which would be visibly outside of this control's rectangle will not be rendered and won't receive input.

Vector2 custom_minimum_size = Vector2(0, 0) 🔗

void set_custom_minimum_size(value: Vector2)

Vector2 get_custom_minimum_size()

The minimum size of the node's bounding rectangle. If you set it to a value greater than (0, 0), the node's bounding rectangle will always have at least this size. Note that Control nodes have their internal minimum size returned by get_minimum_size(). It depends on the control's contents, like text, textures, or style boxes. The actual minimum size is the maximum value of this property and the internal minimum size (see get_combined_minimum_size()).

FocusBehaviorRecursive focus_behavior_recursive = 0 🔗

void set_focus_behavior_recursive(value: FocusBehaviorRecursive)

FocusBehaviorRecursive get_focus_behavior_recursive()

Determines which controls can be focused together with focus_mode. See get_focus_mode_with_override(). Since the default behavior is FOCUS_BEHAVIOR_INHERITED, this can be used to prevent all children controls from getting focused.

FocusMode focus_mode = 0 🔗

void set_focus_mode(value: FocusMode)

FocusMode get_focus_mode()

Determines which controls can be focused. Only one control can be focused at a time, and the focused control will receive keyboard, gamepad, and mouse events in _gui_input(). Use get_focus_mode_with_override() to determine if a control can grab focus, since focus_behavior_recursive also affects it. See also grab_focus().

NodePath focus_neighbor_bottom = NodePath("") 🔗

void set_focus_neighbor(side: Side, neighbor: NodePath)

NodePath get_focus_neighbor(side: Side) const

Tells Godot which node it should give focus to if the user presses the down arrow on the keyboard or down on a gamepad by default. You can change the key by editing the ProjectSettings.input/ui_down input action. The node must be a Control. If this property is not set, Godot will give focus to the closest Control to the bottom of this one.

NodePath focus_neighbor_left = NodePath("") 🔗

void set_focus_neighbor(side: Side, neighbor: NodePath)

NodePath get_focus_neighbor(side: Side) const

Tells Godot which node it should give focus to if the user presses the left arrow on the keyboard or left on a gamepad by default. You can change the key by editing the ProjectSettings.input/ui_left input action. The node must be a Control. If this property is not set, Godot will give focus to the closest Control to the left of this one.

NodePath focus_neighbor_right = NodePath("") 🔗

void set_focus_neighbor(side: Side, neighbor: NodePath)

NodePath get_focus_neighbor(side: Side) const

Tells Godot which node it should give focus to if the user presses the right arrow on the keyboard or right on a gamepad by default. You can change the key by editing the ProjectSettings.input/ui_right input action. The node must be a Control. If this property is not set, Godot will give focus to the closest Control to the right of this one.

NodePath focus_neighbor_top = NodePath("") 🔗

void set_focus_neighbor(side: Side, neighbor: NodePath)

NodePath get_focus_neighbor(side: Side) const

Tells Godot which node it should give focus to if the user presses the top arrow on the keyboard or top on a gamepad by default. You can change the key by editing the ProjectSettings.input/ui_up input action. The node must be a Control. If this property is not set, Godot will give focus to the closest Control to the top of this one.

NodePath focus_next = NodePath("") 🔗

void set_focus_next(value: NodePath)

NodePath get_focus_next()

Tells Godot which node it should give focus to if the user presses Tab on a keyboard by default. You can change the key by editing the ProjectSettings.input/ui_focus_next input action.

If this property is not set, Godot will select a "best guess" based on surrounding nodes in the scene tree.

NodePath focus_previous = NodePath("") 🔗

void set_focus_previous(value: NodePath)

NodePath get_focus_previous()

Tells Godot which node it should give focus to if the user presses Shift + Tab on a keyboard by default. You can change the key by editing the ProjectSettings.input/ui_focus_prev input action.

If this property is not set, Godot will select a "best guess" based on surrounding nodes in the scene tree.

Vector2 global_position 🔗

Vector2 get_global_position()

The node's global position, relative to the world (usually to the CanvasLayer).

GrowDirection grow_horizontal = 1 🔗

void set_h_grow_direction(value: GrowDirection)

GrowDirection get_h_grow_direction()

Controls the direction on the horizontal axis in which the control should grow if its horizontal minimum size is changed to be greater than its current size, as the control always has to be at least the minimum size.

GrowDirection grow_vertical = 1 🔗

void set_v_grow_direction(value: GrowDirection)

GrowDirection get_v_grow_direction()

Controls the direction on the vertical axis in which the control should grow if its vertical minimum size is changed to be greater than its current size, as the control always has to be at least the minimum size.

LayoutDirection layout_direction = 0 🔗

void set_layout_direction(value: LayoutDirection)

LayoutDirection get_layout_direction()

Controls layout direction and text writing direction. Right-to-left layouts are necessary for certain languages (e.g. Arabic and Hebrew). See also is_layout_rtl().

bool localize_numeral_system = true 🔗

void set_localize_numeral_system(value: bool)

bool is_localizing_numeral_system()

If true, automatically converts code line numbers, list indices, SpinBox and ProgressBar values from the Western Arabic (0..9) to the numeral systems used in current locale.

Note: Numbers within the text are not automatically converted, it can be done manually, using TextServer.format_number().

MouseBehaviorRecursive mouse_behavior_recursive = 0 🔗

void set_mouse_behavior_recursive(value: MouseBehaviorRecursive)

MouseBehaviorRecursive get_mouse_behavior_recursive()

Determines which controls can receive mouse input together with mouse_filter. See get_mouse_filter_with_override(). Since the default behavior is MOUSE_BEHAVIOR_INHERITED, this can be used to prevent all children controls from receiving mouse input.

CursorShape mouse_default_cursor_shape = 0 🔗

void set_default_cursor_shape(value: CursorShape)

CursorShape get_default_cursor_shape()

The default cursor shape for this control. Useful for Godot plugins and applications or games that use the system's mouse cursors.

Note: On Linux, shapes may vary depending on the cursor theme of the system.

MouseFilter mouse_filter = 0 🔗

void set_mouse_filter(value: MouseFilter)

MouseFilter get_mouse_filter()

Determines which controls will be able to receive mouse button input events through _gui_input() and the mouse_entered, and mouse_exited signals. Also determines how these events should be propagated. See the constants to learn what each does. Use get_mouse_filter_with_override() to determine if a control can receive mouse input, since mouse_behavior_recursive also affects it.

bool mouse_force_pass_scroll_events = true 🔗

void set_force_pass_scroll_events(value: bool)

bool is_force_pass_scroll_events()

When enabled, scroll wheel events processed by _gui_input() will be passed to the parent control even if mouse_filter is set to MOUSE_FILTER_STOP.

You should disable it on the root of your UI if you do not want scroll events to go to the Node._unhandled_input() processing.

Note: Because this property defaults to true, this allows nested scrollable containers to work out of the box.

float offset_bottom = 0.0 🔗

void set_offset(side: Side, offset: float)

float get_offset(offset: Side) const

Distance between the node's bottom edge and its parent control, based on anchor_bottom.

Offsets are often controlled by one or multiple parent Container nodes, so you should not modify them manually if your node is a direct child of a Container. Offsets update automatically when you move or resize the node.

float offset_left = 0.0 🔗

void set_offset(side: Side, offset: float)

float get_offset(offset: Side) const

Distance between the node's left edge and its parent control, based on anchor_left.

Offsets are often controlled by one or multiple parent Container nodes, so you should not modify them manually if your node is a direct child of a Container. Offsets update automatically when you move or resize the node.

float offset_right = 0.0 🔗

void set_offset(side: Side, offset: float)

float get_offset(offset: Side) const

Distance between the node's right edge and its parent control, based on anchor_right.

Offsets are often controlled by one or multiple parent Container nodes, so you should not modify them manually if your node is a direct child of a Container. Offsets update automatically when you move or resize the node.

float offset_top = 0.0 🔗

void set_offset(side: Side, offset: float)

float get_offset(offset: Side) const

Distance between the node's top edge and its parent control, based on anchor_top.

Offsets are often controlled by one or multiple parent Container nodes, so you should not modify them manually if your node is a direct child of a Container. Offsets update automatically when you move or resize the node.

Vector2 pivot_offset = Vector2(0, 0) 🔗

void set_pivot_offset(value: Vector2)

Vector2 get_pivot_offset()

By default, the node's pivot is its top-left corner. When you change its rotation or scale, it will rotate or scale around this pivot. Set this property to size / 2 to pivot around the Control's center.

Vector2 position = Vector2(0, 0) 🔗

Vector2 get_position()

The node's position, relative to its containing node. It corresponds to the rectangle's top-left corner. The property is not affected by pivot_offset.

float rotation = 0.0 🔗

void set_rotation(value: float)

The node's rotation around its pivot, in radians. See pivot_offset to change the pivot's position.

Note: This property is edited in the inspector in degrees. If you want to use degrees in a script, use rotation_degrees.

float rotation_degrees 🔗

void set_rotation_degrees(value: float)

float get_rotation_degrees()

Helper property to access rotation in degrees instead of radians.

Vector2 scale = Vector2(1, 1) 🔗

void set_scale(value: Vector2)

The node's scale, relative to its size. Change this property to scale the node around its pivot_offset. The Control's tooltip will also scale according to this value.

Note: This property is mainly intended to be used for animation purposes. To support multiple resolutions in your project, use an appropriate viewport stretch mode as described in the documentation instead of scaling Controls individually.

Note: FontFile.oversampling does not take Control scale into account. This means that scaling up/down will cause bitmap fonts and rasterized (non-MSDF) dynamic fonts to appear blurry or pixelated. To ensure text remains crisp regardless of scale, you can enable MSDF font rendering by enabling ProjectSettings.gui/theme/default_font_multichannel_signed_distance_field (applies to the default project font only), or enabling Multichannel Signed Distance Field in the import options of a DynamicFont for custom fonts. On system fonts, SystemFont.multichannel_signed_distance_field can be enabled in the inspector.

Note: If the Control node is a child of a Container node, the scale will be reset to Vector2(1, 1) when the scene is instantiated. To set the Control's scale when it's instantiated, wait for one frame using await get_tree().process_frame then set its scale property.

Node shortcut_context 🔗

void set_shortcut_context(value: Node)

Node get_shortcut_context()

The Node which must be a parent of the focused Control for the shortcut to be activated. If null, the shortcut can be activated when any control is focused (a global shortcut). This allows shortcuts to be accepted only when the user has a certain area of the GUI focused.

Vector2 size = Vector2(0, 0) 🔗

The size of the node's bounding rectangle, in the node's coordinate system. Container nodes update this property automatically.

BitField[SizeFlags] size_flags_horizontal = 1 🔗

void set_h_size_flags(value: BitField[SizeFlags])

BitField[SizeFlags] get_h_size_flags()

Tells the parent Container nodes how they should resize and place the node on the X axis. Use a combination of the SizeFlags constants to change the flags. See the constants to learn what each does.

float size_flags_stretch_ratio = 1.0 🔗

void set_stretch_ratio(value: float)

float get_stretch_ratio()

If the node and at least one of its neighbors uses the SIZE_EXPAND size flag, the parent Container will let it take more or less space depending on this property. If this node has a stretch ratio of 2 and its neighbor a ratio of 1, this node will take two thirds of the available space.

BitField[SizeFlags] size_flags_vertical = 1 🔗

void set_v_size_flags(value: BitField[SizeFlags])

BitField[SizeFlags] get_v_size_flags()

Tells the parent Container nodes how they should resize and place the node on the Y axis. Use a combination of the SizeFlags constants to change the flags. See the constants to learn what each does.

void set_theme(value: Theme)

The Theme resource this node and all its Control and Window children use. If a child node has its own Theme resource set, theme items are merged with child's definitions having higher priority.

Note: Window styles will have no effect unless the window is embedded.

StringName theme_type_variation = &"" 🔗

void set_theme_type_variation(value: StringName)

StringName get_theme_type_variation()

The name of a theme type variation used by this Control to look up its own theme items. When empty, the class name of the node is used (e.g. Button for the Button control), as well as the class names of all parent classes (in order of inheritance).

When set, this property gives the highest priority to the type of the specified name. This type can in turn extend another type, forming a dependency chain. See Theme.set_type_variation(). If the theme item cannot be found using this type or its base types, lookup falls back on the class names.

Note: To look up Control's own items use various get_theme_* methods without specifying theme_type.

Note: Theme items are looked for in the tree order, from branch to root, where each Control node is checked for its theme property. The earliest match against any type/class name is returned. The project-level Theme and the default Theme are checked last.

AutoTranslateMode tooltip_auto_translate_mode = 0 🔗

void set_tooltip_auto_translate_mode(value: AutoTranslateMode)

AutoTranslateMode get_tooltip_auto_translate_mode()

Defines if tooltip text should automatically change to its translated version depending on the current locale. Uses the same auto translate mode as this control when set to Node.AUTO_TRANSLATE_MODE_INHERIT.

Note: Tooltips customized using _make_custom_tooltip() do not use this auto translate mode automatically.

String tooltip_text = "" 🔗

void set_tooltip_text(value: String)

String get_tooltip_text()

The default tooltip text. The tooltip appears when the user's mouse cursor stays idle over this control for a few moments, provided that the mouse_filter property is not MOUSE_FILTER_IGNORE. The time required for the tooltip to appear can be changed with the ProjectSettings.gui/timers/tooltip_delay_sec setting.

This string is the default return value of get_tooltip(). Override _get_tooltip() to generate tooltip text dynamically. Override _make_custom_tooltip() to customize the tooltip interface and behavior.

The tooltip popup will use either a default implementation, or a custom one that you can provide by overriding _make_custom_tooltip(). The default tooltip includes a PopupPanel and Label whose theme properties can be customized using Theme methods with the "TooltipPanel" and "TooltipLabel" respectively. For example:

String _accessibility_get_contextual_info() virtual const 🔗

Return the description of the keyboard shortcuts and other contextual help for this control.

bool _can_drop_data(at_position: Vector2, data: Variant) virtual const 🔗

Godot calls this method to test if data from a control's _get_drag_data() can be dropped at at_position. at_position is local to this control.

This method should only be used to test the data. Process the data in _drop_data().

Note: If the drag was initiated by a keyboard shortcut or accessibility_drag(), at_position is set to Vector2.INF, and the currently selected item/text position should be used as the drop position.

void _drop_data(at_position: Vector2, data: Variant) virtual 🔗

Godot calls this method to pass you the data from a control's _get_drag_data() result. Godot first calls _can_drop_data() to test if data is allowed to drop at at_position where at_position is local to this control.

Note: If the drag was initiated by a keyboard shortcut or accessibility_drag(), at_position is set to Vector2.INF, and the currently selected item/text position should be used as the drop position.

String _get_accessibility_container_name(node: Node) virtual const 🔗

Override this method to return a human-readable description of the position of the child node in the custom container, added to the accessibility_name.

Variant _get_drag_data(at_position: Vector2) virtual 🔗

Godot calls this method to get data that can be dragged and dropped onto controls that expect drop data. Returns null if there is no data to drag. Controls that want to receive drop data should implement _can_drop_data() and _drop_data(). at_position is local to this control. Drag may be forced with force_drag().

A preview that will follow the mouse that should represent the data can be set with set_drag_preview(). A good time to set the preview is in this method.

Note: If the drag was initiated by a keyboard shortcut or accessibility_drag(), at_position is set to Vector2.INF, and the currently selected item/text position should be used as the drag position.

Vector2 _get_minimum_size() virtual const 🔗

Virtual method to be implemented by the user. Returns the minimum size for this control. Alternative to custom_minimum_size for controlling minimum size via code. The actual minimum size will be the max value of these two (in each axis separately).

If not overridden, defaults to Vector2.ZERO.

Note: This method will not be called when the script is attached to a Control node that already overrides its minimum size (e.g. Label, Button, PanelContainer etc.). It can only be used with most basic GUI nodes, like Control, Container, Panel etc.

String _get_tooltip(at_position: Vector2) virtual const 🔗

Virtual method to be implemented by the user. Returns the tooltip text for the position at_position in control's local coordinates, which will typically appear when the cursor is resting over this control. See get_tooltip().

Note: If this method returns an empty String and _make_custom_tooltip() is not overridden, no tooltip is displayed.

void _gui_input(event: InputEvent) virtual 🔗

Virtual method to be implemented by the user. Override this method to handle and accept inputs on UI elements. See also accept_event().

Example: Click on the control to print a message:

If the event inherits InputEventMouse, this method will not be called when:

the control's mouse_filter is set to MOUSE_FILTER_IGNORE;

the control is obstructed by another control on top, that doesn't have mouse_filter set to MOUSE_FILTER_IGNORE;

the control's parent has mouse_filter set to MOUSE_FILTER_STOP or has accepted the event;

the control's parent has clip_contents enabled and the event's position is outside the parent's rectangle;

the event's position is outside the control (see _has_point()).

Note: The event's position is relative to this control's origin.

bool _has_point(point: Vector2) virtual const 🔗

Virtual method to be implemented by the user. Returns whether the given point is inside this control.

If not overridden, default behavior is checking if the point is within control's Rect.

Note: If you want to check if a point is inside the control, you can use Rect2(Vector2.ZERO, size).has_point(point).

Object _make_custom_tooltip(for_text: String) virtual const 🔗

Virtual method to be implemented by the user. Returns a Control node that should be used as a tooltip instead of the default one. for_text is the return value of get_tooltip().

The returned node must be of type Control or Control-derived. It can have child nodes of any type. It is freed when the tooltip disappears, so make sure you always provide a new instance (if you want to use a pre-existing node from your scene tree, you can duplicate it and pass the duplicated instance). When null or a non-Control node is returned, the default tooltip will be used instead.

The returned node will be added as child to a PopupPanel, so you should only provide the contents of that panel. That PopupPanel can be themed using Theme.set_stylebox() for the type "TooltipPanel" (see tooltip_text for an example).

Note: The tooltip is shrunk to minimal size. If you want to ensure it's fully visible, you might want to set its custom_minimum_size to some non-zero value.

Note: The node (and any relevant children) should have their CanvasItem.visible set to true when returned, otherwise, the viewport that instantiates it will not be able to calculate its minimum size reliably.

Note: If overridden, this method is called even if get_tooltip() returns an empty string. When this happens with the default tooltip, it is not displayed. To copy this behavior, return null in this method when for_text is empty.

Example: Use a constructed node as a tooltip:

Example: Usa a scene instance as a tooltip:

Array[Vector3i] _structured_text_parser(args: Array, text: String) virtual const 🔗

User defined BiDi algorithm override function.

Returns an Array of Vector3i text ranges and text base directions, in the left-to-right order. Ranges should cover full source text without overlaps. BiDi algorithm will be used on each range separately.

void accept_event() 🔗

Marks an input event as handled. Once you accept an input event, it stops propagating, even to nodes listening to Node._unhandled_input() or Node._unhandled_key_input().

Note: This does not affect the methods in Input, only the way events are propagated.

void accessibility_drag() 🔗

Starts drag-and-drop operation without using a mouse.

void accessibility_drop() 🔗

Ends drag-and-drop operation without using a mouse.

void add_theme_color_override(name: StringName, color: Color) 🔗

Creates a local override for a theme Color with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_color_override().

See also get_theme_color().

Example: Override a Label's color and reset it later:

void add_theme_constant_override(name: StringName, constant: int) 🔗

Creates a local override for a theme constant with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_constant_override().

See also get_theme_constant().

void add_theme_font_override(name: StringName, font: Font) 🔗

Creates a local override for a theme Font with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_font_override().

See also get_theme_font().

void add_theme_font_size_override(name: StringName, font_size: int) 🔗

Creates a local override for a theme font size with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_font_size_override().

See also get_theme_font_size().

void add_theme_icon_override(name: StringName, texture: Texture2D) 🔗

Creates a local override for a theme icon with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_icon_override().

See also get_theme_icon().

void add_theme_stylebox_override(name: StringName, stylebox: StyleBox) 🔗

Creates a local override for a theme StyleBox with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_stylebox_override().

See also get_theme_stylebox().

Example: Modify a property in a StyleBox by duplicating it:

void begin_bulk_theme_override() 🔗

Prevents *_theme_*_override methods from emitting NOTIFICATION_THEME_CHANGED until end_bulk_theme_override() is called.

void end_bulk_theme_override() 🔗

Ends a bulk theme override update. See begin_bulk_theme_override().

Control find_next_valid_focus() const 🔗

Finds the next (below in the tree) Control that can receive the focus.

Control find_prev_valid_focus() const 🔗

Finds the previous (above in the tree) Control that can receive the focus.

Control find_valid_focus_neighbor(side: Side) const 🔗

Finds the next Control that can receive the focus on the specified Side.

Note: This is different from get_focus_neighbor(), which returns the path of a specified focus neighbor.

void force_drag(data: Variant, preview: Control) 🔗

Forces drag and bypasses _get_drag_data() and set_drag_preview() by passing data and preview. Drag will start even if the mouse is neither over nor pressed on this control.

The methods _can_drop_data() and _drop_data() must be implemented on controls that want to receive drop data.

float get_anchor(side: Side) const 🔗

Returns the anchor for the specified Side. A getter method for anchor_bottom, anchor_left, anchor_right and anchor_top.

Vector2 get_begin() const 🔗

Returns offset_left and offset_top. See also position.

Vector2 get_combined_minimum_size() const 🔗

Returns combined minimum size from custom_minimum_size and get_minimum_size().

CursorShape get_cursor_shape(position: Vector2 = Vector2(0, 0)) const 🔗

Returns the mouse cursor shape for this control when hovered over position in local coordinates. For most controls, this is the same as mouse_default_cursor_shape, but some built-in controls implement more complex logic.

Vector2 get_end() const 🔗

Returns offset_right and offset_bottom.

FocusMode get_focus_mode_with_override() const 🔗

Returns the focus_mode, but takes the focus_behavior_recursive into account. If focus_behavior_recursive is set to FOCUS_BEHAVIOR_DISABLED, or it is set to FOCUS_BEHAVIOR_INHERITED and its ancestor is set to FOCUS_BEHAVIOR_DISABLED, then this returns FOCUS_NONE.

NodePath get_focus_neighbor(side: Side) const 🔗

Returns the focus neighbor for the specified Side. A getter method for focus_neighbor_bottom, focus_neighbor_left, focus_neighbor_right and focus_neighbor_top.

Note: To find the next Control on the specific Side, even if a neighbor is not assigned, use find_valid_focus_neighbor().

Rect2 get_global_rect() const 🔗

Returns the position and size of the control relative to the containing canvas. See global_position and size.

Note: If the node itself or any parent CanvasItem between the node and the canvas have a non default rotation or skew, the resulting size is likely not meaningful.

Note: Setting Viewport.gui_snap_controls_to_pixels to true can lead to rounding inaccuracies between the displayed control and the returned Rect2.

Vector2 get_minimum_size() const 🔗

Returns the minimum size for this control. See custom_minimum_size.

MouseFilter get_mouse_filter_with_override() const 🔗

Returns the mouse_filter, but takes the mouse_behavior_recursive into account. If mouse_behavior_recursive is set to MOUSE_BEHAVIOR_DISABLED, or it is set to MOUSE_BEHAVIOR_INHERITED and its ancestor is set to MOUSE_BEHAVIOR_DISABLED, then this returns MOUSE_FILTER_IGNORE.

float get_offset(offset: Side) const 🔗

Returns the offset for the specified Side. A getter method for offset_bottom, offset_left, offset_right and offset_top.

Vector2 get_parent_area_size() const 🔗

Returns the width/height occupied in the parent control.

Control get_parent_control() const 🔗

Returns the parent control node.

Rect2 get_rect() const 🔗

Returns the position and size of the control in the coordinate system of the containing node. See position, scale and size.

Note: If rotation is not the default rotation, the resulting size is not meaningful.

Note: Setting Viewport.gui_snap_controls_to_pixels to true can lead to rounding inaccuracies between the displayed control and the returned Rect2.

Vector2 get_screen_position() const 🔗

Returns the position of this Control in global screen coordinates (i.e. taking window position into account). Mostly useful for editor plugins.

Equals to global_position if the window is embedded (see Viewport.gui_embed_subwindows).

Example: Show a popup at the mouse position:

Color get_theme_color(name: StringName, theme_type: StringName = &"") const 🔗

Returns a Color from the first matching Theme in the tree if that Theme has a color item with the specified name and theme_type. If theme_type is omitted the class name of the current control is used as the type, or theme_type_variation if it is defined. If the type is a class name its parent classes are also checked, in order of inheritance. If the type is a variation its base types are checked, in order of dependency, then the control's class name and its parent classes are checked.

For the current control its local overrides are considered first (see add_theme_color_override()), then its assigned theme. After the current control, each parent control and its assigned theme are considered; controls without a theme assigned are skipped. If no matching Theme is found in the tree, the custom project Theme (see ProjectSettings.gui/theme/custom) and the default Theme are used (see ThemeDB).

int get_theme_constant(name: StringName, theme_type: StringName = &"") const 🔗

Returns a constant from the first matching Theme in the tree if that Theme has a constant item with the specified name and theme_type.

See get_theme_color() for details.

float get_theme_default_base_scale() const 🔗

Returns the default base scale value from the first matching Theme in the tree if that Theme has a valid Theme.default_base_scale value.

See get_theme_color() for details.

Font get_theme_default_font() const 🔗

Returns the default font from the first matching Theme in the tree if that Theme has a valid Theme.default_font value.

See get_theme_color() for details.

int get_theme_default_font_size() const 🔗

Returns the default font size value from the first matching Theme in the tree if that Theme has a valid Theme.default_font_size value.

See get_theme_color() for details.

Font get_theme_font(name: StringName, theme_type: StringName = &"") const 🔗

Returns a Font from the first matching Theme in the tree if that Theme has a font item with the specified name and theme_type.

See get_theme_color() for details.

int get_theme_font_size(name: StringName, theme_type: StringName = &"") const 🔗

Returns a font size from the first matching Theme in the tree if that Theme has a font size item with the specified name and theme_type.

See get_theme_color() for details.

Texture2D get_theme_icon(name: StringName, theme_type: StringName = &"") const 🔗

Returns an icon from the first matching Theme in the tree if that Theme has an icon item with the specified name and theme_type.

See get_theme_color() for details.

StyleBox get_theme_stylebox(name: StringName, theme_type: StringName = &"") const 🔗

Returns a StyleBox from the first matching Theme in the tree if that Theme has a stylebox item with the specified name and theme_type.

See get_theme_color() for details.

String get_tooltip(at_position: Vector2 = Vector2(0, 0)) const 🔗

Returns the tooltip text for the position at_position in control's local coordinates, which will typically appear when the cursor is resting over this control. By default, it returns tooltip_text.

This method can be overridden to customize its behavior. See _get_tooltip().

Note: If this method returns an empty String and _make_custom_tooltip() is not overridden, no tooltip is displayed.

void grab_click_focus() 🔗

Creates an InputEventMouseButton that attempts to click the control. If the event is received, the control gains focus.

Steal the focus from another control and become the focused control (see focus_mode).

Note: Using this method together with Callable.call_deferred() makes it more reliable, especially when called inside Node._ready().

bool has_focus() const 🔗

Returns true if this is the current focused control. See focus_mode.

bool has_theme_color(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has a color item with the specified name and theme_type.

See get_theme_color() for details.

bool has_theme_color_override(name: StringName) const 🔗

Returns true if there is a local override for a theme Color with the specified name in this Control node.

See add_theme_color_override().

bool has_theme_constant(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has a constant item with the specified name and theme_type.

See get_theme_color() for details.

bool has_theme_constant_override(name: StringName) const 🔗

Returns true if there is a local override for a theme constant with the specified name in this Control node.

See add_theme_constant_override().

bool has_theme_font(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has a font item with the specified name and theme_type.

See get_theme_color() for details.

bool has_theme_font_override(name: StringName) const 🔗

Returns true if there is a local override for a theme Font with the specified name in this Control node.

See add_theme_font_override().

bool has_theme_font_size(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has a font size item with the specified name and theme_type.

See get_theme_color() for details.

bool has_theme_font_size_override(name: StringName) const 🔗

Returns true if there is a local override for a theme font size with the specified name in this Control node.

See add_theme_font_size_override().

bool has_theme_icon(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has an icon item with the specified name and theme_type.

See get_theme_color() for details.

bool has_theme_icon_override(name: StringName) const 🔗

Returns true if there is a local override for a theme icon with the specified name in this Control node.

See add_theme_icon_override().

bool has_theme_stylebox(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has a stylebox item with the specified name and theme_type.

See get_theme_color() for details.

bool has_theme_stylebox_override(name: StringName) const 🔗

Returns true if there is a local override for a theme StyleBox with the specified name in this Control node.

See add_theme_stylebox_override().

bool is_drag_successful() const 🔗

Returns true if a drag operation is successful. Alternative to Viewport.gui_is_drag_successful().

Best used with Node.NOTIFICATION_DRAG_END.

bool is_layout_rtl() const 🔗

Returns true if the layout is right-to-left. See also layout_direction.

void release_focus() 🔗

Give up the focus. No other control will be able to receive input.

void remove_theme_color_override(name: StringName) 🔗

Removes a local override for a theme Color with the specified name previously added by add_theme_color_override() or via the Inspector dock.

void remove_theme_constant_override(name: StringName) 🔗

Removes a local override for a theme constant with the specified name previously added by add_theme_constant_override() or via the Inspector dock.

void remove_theme_font_override(name: StringName) 🔗

Removes a local override for a theme Font with the specified name previously added by add_theme_font_override() or via the Inspector dock.

void remove_theme_font_size_override(name: StringName) 🔗

Removes a local override for a theme font size with the specified name previously added by add_theme_font_size_override() or via the Inspector dock.

void remove_theme_icon_override(name: StringName) 🔗

Removes a local override for a theme icon with the specified name previously added by add_theme_icon_override() or via the Inspector dock.

void remove_theme_stylebox_override(name: StringName) 🔗

Removes a local override for a theme StyleBox with the specified name previously added by add_theme_stylebox_override() or via the Inspector dock.

Resets the size to get_combined_minimum_size(). This is equivalent to calling set_size(Vector2()) (or any size below the minimum).

void set_anchor(side: Side, anchor: float, keep_offset: bool = false, push_opposite_anchor: bool = true) 🔗

Sets the anchor for the specified Side to anchor. A setter method for anchor_bottom, anchor_left, anchor_right and anchor_top.

If keep_offset is true, offsets aren't updated after this operation.

If push_opposite_anchor is true and the opposite anchor overlaps this anchor, the opposite one will have its value overridden. For example, when setting left anchor to 1 and the right anchor has value of 0.5, the right anchor will also get value of 1. If push_opposite_anchor was false, the left anchor would get value 0.5.

void set_anchor_and_offset(side: Side, anchor: float, offset: float, push_opposite_anchor: bool = false) 🔗

Works the same as set_anchor(), but instead of keep_offset argument and automatic update of offset, it allows to set the offset yourself (see set_offset()).

void set_anchors_and_offsets_preset(preset: LayoutPreset, resize_mode: LayoutPresetMode = 0, margin: int = 0) 🔗

Sets both anchor preset and offset preset. See set_anchors_preset() and set_offsets_preset().

void set_anchors_preset(preset: LayoutPreset, keep_offsets: bool = false) 🔗

Sets the anchors to a preset from LayoutPreset enum. This is the code equivalent to using the Layout menu in the 2D editor.

If keep_offsets is true, control's position will also be updated.

void set_begin(position: Vector2) 🔗

Sets offset_left and offset_top at the same time. Equivalent of changing position.

void set_drag_forwarding(drag_func: Callable, can_drop_func: Callable, drop_func: Callable) 🔗

Sets the given callables to be used instead of the control's own drag-and-drop virtual methods. If a callable is empty, its respective virtual method is used as normal.

The arguments for each callable should be exactly the same as their respective virtual methods, which would be:

drag_func corresponds to _get_drag_data() and requires a Vector2;

can_drop_func corresponds to _can_drop_data() and requires both a Vector2 and a Variant;

drop_func corresponds to _drop_data() and requires both a Vector2 and a Variant.

void set_drag_preview(control: Control) 🔗

Shows the given control at the mouse pointer. A good time to call this method is in _get_drag_data(). The control must not be in the scene tree. You should not free the control, and you should not keep a reference to the control beyond the duration of the drag. It will be deleted automatically after the drag has ended.

void set_end(position: Vector2) 🔗

Sets offset_right and offset_bottom at the same time.

void set_focus_neighbor(side: Side, neighbor: NodePath) 🔗

Sets the focus neighbor for the specified Side to the Control at neighbor node path. A setter method for focus_neighbor_bottom, focus_neighbor_left, focus_neighbor_right and focus_neighbor_top.

void set_global_position(position: Vector2, keep_offsets: bool = false) 🔗

Sets the global_position to given position.

If keep_offsets is true, control's anchors will be updated instead of offsets.

void set_offset(side: Side, offset: float) 🔗

Sets the offset for the specified Side to offset. A setter method for offset_bottom, offset_left, offset_right and offset_top.

void set_offsets_preset(preset: LayoutPreset, resize_mode: LayoutPresetMode = 0, margin: int = 0) 🔗

Sets the offsets to a preset from LayoutPreset enum. This is the code equivalent to using the Layout menu in the 2D editor.

Use parameter resize_mode with constants from LayoutPresetMode to better determine the resulting size of the Control. Constant size will be ignored if used with presets that change size, e.g. PRESET_LEFT_WIDE.

Use parameter margin to determine the gap between the Control and the edges.

void set_position(position: Vector2, keep_offsets: bool = false) 🔗

Sets the position to given position.

If keep_offsets is true, control's anchors will be updated instead of offsets.

void set_size(size: Vector2, keep_offsets: bool = false) 🔗

Sets the size (see size).

If keep_offsets is true, control's anchors will be updated instead of offsets.

void update_minimum_size() 🔗

Invalidates the size cache in this node and in parent nodes up to top level. Intended to be used with get_minimum_size() when the return value is changed. Setting custom_minimum_size directly calls this method automatically.

void warp_mouse(position: Vector2) 🔗

Moves the mouse cursor to position, relative to position of this Control.

Note: warp_mouse() is only supported on Windows, macOS and Linux. It has no effect on Android, iOS and Web.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
func _on_mouse_exited():
    if not Rect2(Vector2(), size).has_point(get_local_mouse_position()):
        # Not hovering over area.
```

Example 2 (go):
```go
func _notification(what):
    if what == NOTIFICATION_THEME_CHANGED:
        if not is_node_ready():
            await ready # Wait until ready signal.
        $Label.add_theme_color_override("font_color", Color.YELLOW)
```

Example 3 (gdscript):
```gdscript
var style_box = StyleBoxFlat.new()
style_box.set_bg_color(Color(1, 1, 0))
style_box.set_border_width_all(2)
# We assume here that the `theme` property has been assigned a custom Theme beforehand.
theme.set_stylebox("panel", "TooltipPanel", style_box)
theme.set_color("font_color", "TooltipLabel", Color(0, 1, 1))
```

Example 4 (gdscript):
```gdscript
var styleBox = new StyleBoxFlat();
styleBox.SetBgColor(new Color(1, 1, 0));
styleBox.SetBorderWidthAll(2);
// We assume here that the `Theme` property has been assigned a custom Theme beforehand.
Theme.SetStyleBox("panel", "TooltipPanel", styleBox);
Theme.SetColor("font_color", "TooltipLabel", new Color(0, 1, 1));
```

---

## Control node gallery

**URL:** https://docs.godotengine.org/en/stable/tutorials/ui/control_node_gallery.html

**Contents:**
- Control node gallery
- User-contributed notes

Here is a list of common Control nodes with their name next to them:

The Control Gallery demo pictured above can be found on GitHub.

Please read the User-contributed notes policy before submitting a comment.

---

## Custom GUI controls

**URL:** https://docs.godotengine.org/en/stable/tutorials/ui/custom_gui_controls.html

**Contents:**
- Custom GUI controls
- So many controls...
- Drawing
  - Checking control size
  - Checking focus
- Sizing
- Input
  - Input events
  - Notifications
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

Yet there are never enough. Creating your own custom controls that act just the way you want them to is an obsession of almost every GUI programmer. Godot provides plenty of them, but they may not work exactly the way you want. Before contacting the developers with a pull-request to support diagonal scrollbars, at least it will be good to know how to create these controls easily from script.

For drawing, it is recommended to check the Custom drawing in 2D tutorial. The same applies. Some functions are worth mentioning due to their usefulness when drawing, so they will be detailed next:

Unlike 2D nodes, "size" is important with controls, as it helps to organize them in proper layouts. For this, the Control.size property is provided. Checking it during _draw() is vital to ensure everything is kept in-bounds.

Some controls (such as buttons or text editors) might provide input focus for keyboard or joypad input. Examples of this are entering text or pressing a button. This is controlled with the Control.focus_mode property. When drawing, and if the control supports input focus, it is always desired to show some sort of indicator (highlight, box, etc.) to indicate that this is the currently focused control. To check for this status, the Control.has_focus() method exists. Example

As mentioned before, size is important to controls. This allows them to lay out properly, when set into grids, containers, or anchored. Controls, most of the time, provide a minimum size to help properly lay them out. For example, if controls are placed vertically on top of each other using a VBoxContainer, the minimum size will make sure your custom control is not squished by the other controls in the container.

To provide this callback, just override Control._get_minimum_size(), for example:

Alternatively, set it using a function:

Controls provide a few helpers to make managing input events much easier than regular nodes.

There are a few tutorials about input before this one, but it's worth mentioning that controls have a special input method that only works when:

The mouse pointer is over the control.

The button was pressed over this control (control always captures input until button is released)

Control provides keyboard/joypad focus via Control.focus_mode.

This function is Control._gui_input(). To use it, override it in your control. No processing needs to be set.

For more information about events themselves, check the Using InputEvent tutorial.

Controls also have many useful notifications for which no dedicated callback exists, but which can be checked with the _notification callback:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (go):
```go
func _draw():
    if has_focus():
         draw_selected()
    else:
         draw_normal()
```

Example 2 (json):
```json
public override void _Draw()
{
    if (HasFocus())
    {
        DrawSelected()
    }
    else
    {
        DrawNormal();
    }
}
```

Example 3 (csharp):
```csharp
func _get_minimum_size():
    return Vector2(30, 30)
```

Example 4 (csharp):
```csharp
public override Vector2 _GetMinimumSize()
{
    return new Vector2(20, 20);
}
```

---

## Dictionary

**URL:** https://docs.godotengine.org/en/stable/classes/class_dictionary.html

**Contents:**
- Dictionary
- Description
- Tutorials
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A built-in data structure that holds key-value pairs.

Dictionaries are associative containers that contain values referenced by unique keys. Dictionaries will preserve the insertion order when adding new entries. In other programming languages, this data structure is often referred to as a hash map or an associative array.

You can define a dictionary by placing a comma-separated list of key: value pairs inside curly braces {}.

Creating a dictionary:

You can access a dictionary's value by referencing its corresponding key. In the above example, points_dict["White"] will return 50. You can also write points_dict.White, which is equivalent. However, you'll have to use the bracket syntax if the key you're accessing the dictionary with isn't a fixed string (such as a number or variable).

In the above code, points will be assigned the value that is paired with the appropriate color selected in my_color.

Dictionaries can contain more complex data:

To add a key to an existing dictionary, access it like an existing key and assign to it:

Finally, untyped dictionaries can contain different types of keys and values in the same dictionary:

The keys of a dictionary can be iterated with the for keyword:

To enforce a certain type for keys and values, you can create a typed dictionary. Typed dictionaries can only contain keys and values of the given types, or that inherit from the given classes:

Note: Dictionaries are always passed by reference. To get a copy of a dictionary which can be modified independently of the original dictionary, use duplicate().

Note: Erasing elements while iterating over dictionaries is not supported and will result in unpredictable behavior.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

GDScript basics: Dictionary

Operating System Testing Demo

Dictionary(base: Dictionary, key_type: int, key_class_name: StringName, key_script: Variant, value_type: int, value_class_name: StringName, value_script: Variant)

Dictionary(from: Dictionary)

assign(dictionary: Dictionary)

duplicate(deep: bool = false) const

duplicate_deep(deep_subresources_mode: int = 1) const

find_key(value: Variant) const

get(key: Variant, default: Variant = null) const

get_or_add(key: Variant, default: Variant = null)

get_typed_key_builtin() const

get_typed_key_class_name() const

get_typed_key_script() const

get_typed_value_builtin() const

get_typed_value_class_name() const

get_typed_value_script() const

has(key: Variant) const

has_all(keys: Array) const

is_same_typed(dictionary: Dictionary) const

is_same_typed_key(dictionary: Dictionary) const

is_same_typed_value(dictionary: Dictionary) const

is_typed_value() const

merge(dictionary: Dictionary, overwrite: bool = false)

merged(dictionary: Dictionary, overwrite: bool = false) const

recursive_equal(dictionary: Dictionary, recursion_count: int) const

set(key: Variant, value: Variant)

operator !=(right: Dictionary)

operator ==(right: Dictionary)

operator [](key: Variant)

Dictionary Dictionary() 🔗

Constructs an empty Dictionary.

Dictionary Dictionary(base: Dictionary, key_type: int, key_class_name: StringName, key_script: Variant, value_type: int, value_class_name: StringName, value_script: Variant)

Creates a typed dictionary from the base dictionary. A typed dictionary can only contain keys and values of the given types, or that inherit from the given classes, as described by this constructor's parameters.

Dictionary Dictionary(from: Dictionary)

Returns the same dictionary as from. If you need a copy of the dictionary, use duplicate().

void assign(dictionary: Dictionary) 🔗

Assigns elements of another dictionary into the dictionary. Resizes the dictionary to match dictionary. Performs type conversions if the dictionary is typed.

Clears the dictionary, removing all entries from it.

Dictionary duplicate(deep: bool = false) const 🔗

Returns a new copy of the dictionary.

By default, a shallow copy is returned: all nested Array, Dictionary, and Resource keys and values are shared with the original dictionary. Modifying any of those in one dictionary will also affect them in the other.

If deep is true, a deep copy is returned: all nested arrays and dictionaries are also duplicated (recursively). Any Resource is still shared with the original dictionary, though.

Dictionary duplicate_deep(deep_subresources_mode: int = 1) const 🔗

Duplicates this dictionary, deeply, like duplicate()(true), with extra control over how subresources are handled.

deep_subresources_mode must be one of the values from DeepDuplicateMode. By default, only internal resources will be duplicated (recursively).

bool erase(key: Variant) 🔗

Removes the dictionary entry by key, if it exists. Returns true if the given key existed in the dictionary, otherwise false.

Note: Do not erase entries while iterating over the dictionary. You can iterate over the keys() array instead.

Variant find_key(value: Variant) const 🔗

Finds and returns the first key whose associated value is equal to value, or null if it is not found.

Note: null is also a valid key. If inside the dictionary, find_key() may give misleading results.

Variant get(key: Variant, default: Variant = null) const 🔗

Returns the corresponding value for the given key in the dictionary. If the key does not exist, returns default, or null if the parameter is omitted.

Variant get_or_add(key: Variant, default: Variant = null) 🔗

Gets a value and ensures the key is set. If the key exists in the dictionary, this behaves like get(). Otherwise, the default value is inserted into the dictionary and returned.

int get_typed_key_builtin() const 🔗

Returns the built-in Variant type of the typed dictionary's keys as a Variant.Type constant. If the keys are not typed, returns @GlobalScope.TYPE_NIL. See also is_typed_key().

StringName get_typed_key_class_name() const 🔗

Returns the built-in class name of the typed dictionary's keys, if the built-in Variant type is @GlobalScope.TYPE_OBJECT. Otherwise, returns an empty StringName. See also is_typed_key() and Object.get_class().

Variant get_typed_key_script() const 🔗

Returns the Script instance associated with this typed dictionary's keys, or null if it does not exist. See also is_typed_key().

int get_typed_value_builtin() const 🔗

Returns the built-in Variant type of the typed dictionary's values as a Variant.Type constant. If the values are not typed, returns @GlobalScope.TYPE_NIL. See also is_typed_value().

StringName get_typed_value_class_name() const 🔗

Returns the built-in class name of the typed dictionary's values, if the built-in Variant type is @GlobalScope.TYPE_OBJECT. Otherwise, returns an empty StringName. See also is_typed_value() and Object.get_class().

Variant get_typed_value_script() const 🔗

Returns the Script instance associated with this typed dictionary's values, or null if it does not exist. See also is_typed_value().

bool has(key: Variant) const 🔗

Returns true if the dictionary contains an entry with the given key.

In GDScript, this is equivalent to the in operator:

Note: This method returns true as long as the key exists, even if its corresponding value is null.

bool has_all(keys: Array) const 🔗

Returns true if the dictionary contains all keys in the given keys array.

Returns a hashed 32-bit integer value representing the dictionary contents.

Note: Dictionaries with the same entries but in a different order will not have the same hash.

Note: Dictionaries with equal hash values are not guaranteed to be the same, because of hash collisions. On the contrary, dictionaries with different hash values are guaranteed to be different.

bool is_empty() const 🔗

Returns true if the dictionary is empty (its size is 0). See also size().

bool is_read_only() const 🔗

Returns true if the dictionary is read-only. See make_read_only(). Dictionaries are automatically read-only if declared with const keyword.

bool is_same_typed(dictionary: Dictionary) const 🔗

Returns true if the dictionary is typed the same as dictionary.

bool is_same_typed_key(dictionary: Dictionary) const 🔗

Returns true if the dictionary's keys are typed the same as dictionary's keys.

bool is_same_typed_value(dictionary: Dictionary) const 🔗

Returns true if the dictionary's values are typed the same as dictionary's values.

bool is_typed() const 🔗

Returns true if the dictionary is typed. Typed dictionaries can only store keys/values of their associated type and provide type safety for the [] operator. Methods of typed dictionary still return Variant.

bool is_typed_key() const 🔗

Returns true if the dictionary's keys are typed.

bool is_typed_value() const 🔗

Returns true if the dictionary's values are typed.

Returns the list of keys in the dictionary.

void make_read_only() 🔗

Makes the dictionary read-only, i.e. disables modification of the dictionary's contents. Does not apply to nested content, e.g. content of nested dictionaries.

void merge(dictionary: Dictionary, overwrite: bool = false) 🔗

Adds entries from dictionary to this dictionary. By default, duplicate keys are not copied over, unless overwrite is true.

Note: merge() is not recursive. Nested dictionaries are considered as keys that can be overwritten or not depending on the value of overwrite, but they will never be merged together.

Dictionary merged(dictionary: Dictionary, overwrite: bool = false) const 🔗

Returns a copy of this dictionary merged with the other dictionary. By default, duplicate keys are not copied over, unless overwrite is true. See also merge().

This method is useful for quickly making dictionaries with default values:

bool recursive_equal(dictionary: Dictionary, recursion_count: int) const 🔗

Returns true if the two dictionaries contain the same keys and values, inner Dictionary and Array keys and values are compared recursively.

bool set(key: Variant, value: Variant) 🔗

Sets the value of the element at the given key to the given value. This is the same as using the [] operator (array[index] = value).

Returns the number of entries in the dictionary. Empty dictionaries ({ }) always return 0. See also is_empty().

Sorts the dictionary in ascending order, by key. The final order is dependent on the "less than" (<) comparison between keys.

This method ensures that the dictionary's entries are ordered consistently when keys() or values() are called, or when the dictionary needs to be converted to a string through @GlobalScope.str() or JSON.stringify().

Array values() const 🔗

Returns the list of values in this dictionary.

bool operator !=(right: Dictionary) 🔗

Returns true if the two dictionaries do not contain the same keys and values.

bool operator ==(right: Dictionary) 🔗

Returns true if the two dictionaries contain the same keys and values. The order of the entries does not matter.

Note: In C#, by convention, this operator compares by reference. If you need to compare by value, iterate over both dictionaries.

Variant operator [](key: Variant) 🔗

Returns the corresponding value for the given key in the dictionary. If the entry does not exist, fails and returns null. For safe access, use get() or has().

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (json):
```json
var my_dict = {} # Creates an empty dictionary.

var dict_variable_key = "Another key name"
var dict_variable_value = "value2"
var another_dict = {
    "Some key name": "value1",
    dict_variable_key: dict_variable_value,
}

var points_dict = { "White": 50, "Yellow": 75, "Orange": 100 }

# Alternative Lua-style syntax.
# Doesn't require quotes around keys, but only string constants can be used as key names.
# Additionally, key names must start with a letter or an underscore.
# Here, `some_key` is a string literal, not a variable!
another_dict = {
    some_key = 42,
}
```

Example 2 (gdscript):
```gdscript
var myDict = new Godot.Collections.Dictionary(); // Creates an empty dictionary.
var pointsDict = new Godot.Collections.Dictionary
{
    { "White", 50 },
    { "Yellow", 75 },
    { "Orange", 100 },
};
```

Example 3 (gdscript):
```gdscript
@export_enum("White", "Yellow", "Orange") var my_color: String
var points_dict = { "White": 50, "Yellow": 75, "Orange": 100 }
func _ready():
    # We can't use dot syntax here as `my_color` is a variable.
    var points = points_dict[my_color]
```

Example 4 (json):
```json
[Export(PropertyHint.Enum, "White,Yellow,Orange")]
public string MyColor { get; set; }
private Godot.Collections.Dictionary _pointsDict = new Godot.Collections.Dictionary
{
    { "White", 50 },
    { "Yellow", 75 },
    { "Orange", 100 },
};

public override void _Ready()
{
    int points = (int)_pointsDict[MyColor];
}
```

---

## FlowContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_flowcontainer.html

**Contents:**
- FlowContainer
- Description
- Tutorials
- Properties
- Methods
- Theme Properties
- Enumerations
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions

Inherits: Container < Control < CanvasItem < Node < Object

Inherited By: HFlowContainer, VFlowContainer

A container that arranges its child controls horizontally or vertically and wraps them around at the borders.

A container that arranges its child controls horizontally or vertically and wraps them around at the borders. This is similar to how text in a book wraps around when no more words can fit on a line.

LastWrapAlignmentMode

get_line_count() const

enum AlignmentMode: 🔗

AlignmentMode ALIGNMENT_BEGIN = 0

The child controls will be arranged at the beginning of the container, i.e. top if orientation is vertical, left if orientation is horizontal (right for RTL layout).

AlignmentMode ALIGNMENT_CENTER = 1

The child controls will be centered in the container.

AlignmentMode ALIGNMENT_END = 2

The child controls will be arranged at the end of the container, i.e. bottom if orientation is vertical, right if orientation is horizontal (left for RTL layout).

enum LastWrapAlignmentMode: 🔗

LastWrapAlignmentMode LAST_WRAP_ALIGNMENT_INHERIT = 0

The last partially filled row or column will wrap aligned to the previous row or column in accordance with alignment.

LastWrapAlignmentMode LAST_WRAP_ALIGNMENT_BEGIN = 1

The last partially filled row or column will wrap aligned to the beginning of the previous row or column.

LastWrapAlignmentMode LAST_WRAP_ALIGNMENT_CENTER = 2

The last partially filled row or column will wrap aligned to the center of the previous row or column.

LastWrapAlignmentMode LAST_WRAP_ALIGNMENT_END = 3

The last partially filled row or column will wrap aligned to the end of the previous row or column.

AlignmentMode alignment = 0 🔗

void set_alignment(value: AlignmentMode)

AlignmentMode get_alignment()

The alignment of the container's children (must be one of ALIGNMENT_BEGIN, ALIGNMENT_CENTER, or ALIGNMENT_END).

LastWrapAlignmentMode last_wrap_alignment = 0 🔗

void set_last_wrap_alignment(value: LastWrapAlignmentMode)

LastWrapAlignmentMode get_last_wrap_alignment()

The wrap behavior of the last, partially filled row or column (must be one of LAST_WRAP_ALIGNMENT_INHERIT, LAST_WRAP_ALIGNMENT_BEGIN, LAST_WRAP_ALIGNMENT_CENTER, or LAST_WRAP_ALIGNMENT_END).

bool reverse_fill = false 🔗

void set_reverse_fill(value: bool)

bool is_reverse_fill()

If true, reverses fill direction. Horizontal FlowContainers will fill rows bottom to top, vertical FlowContainers will fill columns right to left.

When using a vertical FlowContainer with a right to left Control.layout_direction, columns will fill left to right instead.

bool vertical = false 🔗

void set_vertical(value: bool)

If true, the FlowContainer will arrange its children vertically, rather than horizontally.

Can't be changed when using HFlowContainer and VFlowContainer.

int get_line_count() const 🔗

Returns the current line count.

int h_separation = 4 🔗

The horizontal separation of child nodes.

int v_separation = 4 🔗

The vertical separation of child nodes.

Please read the User-contributed notes policy before submitting a comment.

---

## FoldableContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_foldablecontainer.html

**Contents:**
- FoldableContainer
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions

Inherits: Container < Control < CanvasItem < Node < Object

A container that can be expanded/collapsed.

A container that can be expanded/collapsed, with a title that can be filled with controls, such as buttons.

The title can be positioned at the top or bottom of the container.

The container can be expanded or collapsed by clicking the title or by pressing ui_accept when focused.

Child control nodes are hidden when the container is collapsed. Ignores non-control children.

Can allow grouping with other FoldableContainers, check foldable_group and FoldableGroup.

2 (overrides Control)

0 (overrides Control)

title_text_overrun_behavior

add_title_bar_control(control: Control)

remove_title_bar_control(control: Control)

Color(0.875, 0.875, 0.875, 1)

Color(0.95, 0.95, 0.95, 1)

expanded_arrow_mirrored

folded_arrow_mirrored

title_collapsed_hover_panel

title_collapsed_panel

folding_changed(is_folded: bool) 🔗

Emitted when the container is folded/expanded.

enum TitlePosition: 🔗

TitlePosition POSITION_TOP = 0

Makes the title appear at the top of the container.

TitlePosition POSITION_BOTTOM = 1

Makes the title appear at the bottom of the container. Also makes all StyleBoxes flipped vertically.

FoldableGroup foldable_group 🔗

void set_foldable_group(value: FoldableGroup)

FoldableGroup get_foldable_group()

The FoldableGroup associated with the container. When multiple FoldableContainer nodes share the same group, only one of them is allowed to be unfolded.

bool folded = false 🔗

void set_folded(value: bool)

If true, the container will becomes folded and will hide all its children.

String language = "" 🔗

void set_language(value: String)

String get_language()

Language code used for text shaping algorithms. If left empty, current locale is used instead.

void set_title(value: String)

The container's title text.

HorizontalAlignment title_alignment = 0 🔗

void set_title_alignment(value: HorizontalAlignment)

HorizontalAlignment get_title_alignment()

Title's horizontal text alignment.

TitlePosition title_position = 0 🔗

void set_title_position(value: TitlePosition)

TitlePosition get_title_position()

TextDirection title_text_direction = 0 🔗

void set_title_text_direction(value: TextDirection)

TextDirection get_title_text_direction()

Title text writing direction.

OverrunBehavior title_text_overrun_behavior = 0 🔗

void set_title_text_overrun_behavior(value: OverrunBehavior)

OverrunBehavior get_title_text_overrun_behavior()

Defines the behavior of the title when the text is longer than the available space.

void add_title_bar_control(control: Control) 🔗

Adds a Control that will be placed next to the container's title, obscuring the clickable area. Prime usage is adding Button nodes, but it can be any Control.

The control will be added as a child of this container and removed from previous parent if necessary. The controls will be placed aligned to the right, with the first added control being the leftmost one.

Expands the container and emits folding_changed.

Folds the container and emits folding_changed.

void remove_title_bar_control(control: Control) 🔗

Removes a Control added with add_title_bar_control(). The node is not freed automatically, you need to use Node.queue_free().

Color collapsed_font_color = Color(1, 1, 1, 1) 🔗

The title's font color when collapsed.

Color font_color = Color(0.875, 0.875, 0.875, 1) 🔗

The title's font color when expanded.

Color font_outline_color = Color(1, 1, 1, 1) 🔗

The title's font outline color.

Color hover_font_color = Color(0.95, 0.95, 0.95, 1) 🔗

The title's font hover color.

int h_separation = 2 🔗

The horizontal separation between the title's icon and text, and between title bar controls.

int outline_size = 0 🔗

The title's font outline size.

The title's font size.

Texture2D expanded_arrow 🔗

The title's icon used when expanded.

Texture2D expanded_arrow_mirrored 🔗

The title's icon used when expanded (for bottom title).

Texture2D folded_arrow 🔗

The title's icon used when folded (for left-to-right layouts).

Texture2D folded_arrow_mirrored 🔗

The title's icon used when collapsed (for right-to-left layouts).

Background used when FoldableContainer has GUI focus. The focus StyleBox is displayed over the base StyleBox, so a partially transparent StyleBox should be used to ensure the base StyleBox remains visible. A StyleBox that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a StyleBoxEmpty resource. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

Default background for the FoldableContainer.

StyleBox title_collapsed_hover_panel 🔗

Background used when the mouse cursor enters the title's area when collapsed.

StyleBox title_collapsed_panel 🔗

Default background for the FoldableContainer's title when collapsed.

StyleBox title_hover_panel 🔗

Background used when the mouse cursor enters the title's area when expanded.

StyleBox title_panel 🔗

Default background for the FoldableContainer's title when expanded.

Please read the User-contributed notes policy before submitting a comment.

---

## Gradle builds for Android

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/android_gradle_build.html

**Contents:**
- Gradle builds for Android
- Set up the gradle build environment
- Enabling the gradle build and exporting
- User-contributed notes

Godot provides the option to build using the gradle buildsystem. Instead of using the already pre-built template that ships with Godot, an Android Java project gets installed into your project folder. Godot will then build it and use it as an export template every time you export the project.

There are some reasons why you may want to do this:

Modify the project before it's built.

Add external SDKs that build with your project.

Configuring the gradle build is a fairly straightforward process. But first you need to follow the steps in exporting for android up to Setting it up in Godot. After doing that, follow the steps below.

Go to the Project menu, and install the Gradle Build template:

Make sure export templates are downloaded. If not, this menu will help you download them.

A Gradle-based Android project will be created under res://android/build. Editing these files is not needed unless you really need to modify the project.

When setting up the Android project in the Project > Export dialog, Gradle Build needs to be enabled:

From now on, attempting to export the project or one-click deploy will call the Gradle build system to generate fresh templates (this window will appear every time):

The templates built will be used automatically afterwards, so no further configuration is needed.

When using the gradle Android build system, assets that are placed within a folder whose name begins with an underscore will not be included in the generated APK. This does not apply to assets whose file name begins with an underscore.

For example, _example/image.png will not be included as an asset, but _image.png will.

Please read the User-contributed notes policy before submitting a comment.

---

## GraphEdit

**URL:** https://docs.godotengine.org/en/stable/classes/class_graphedit.html

**Contents:**
- GraphEdit
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions

Experimental: This class may be changed or removed in future versions.

Inherits: Control < CanvasItem < Node < Object

An editor for graph-like structures, using GraphNodes.

GraphEdit provides tools for creation, manipulation, and display of various graphs. Its main purpose in the engine is to power the visual programming systems, such as visual shaders, but it is also available for use in user projects.

GraphEdit by itself is only an empty container, representing an infinite grid where GraphNodes can be placed. Each GraphNode represents a node in the graph, a single unit of data in the connected scheme. GraphEdit, in turn, helps to control various interactions with nodes and between nodes. When the user attempts to connect, disconnect, or delete a GraphNode, a signal is emitted in the GraphEdit, but no action is taken by default. It is the responsibility of the programmer utilizing this control to implement the necessary logic to determine how each request should be handled.

Performance: It is greatly advised to enable low-processor usage mode (see OS.low_processor_usage_mode) when using GraphEdits.

Note: Keep in mind that Node.get_children() will also return the connection layer node named _connection_layer due to technical limitations. This behavior may change in future releases.

true (overrides Control)

connection_lines_antialiased

connection_lines_curvature

connection_lines_thickness

2 (overrides Control)

_get_connection_line(from_position: Vector2, to_position: Vector2) virtual const

_is_in_input_hotzone(in_node: Object, in_port: int, mouse_position: Vector2) virtual

_is_in_output_hotzone(in_node: Object, in_port: int, mouse_position: Vector2) virtual

_is_node_hover_valid(from_node: StringName, from_port: int, to_node: StringName, to_port: int) virtual

add_valid_connection_type(from_type: int, to_type: int)

add_valid_left_disconnect_type(type: int)

add_valid_right_disconnect_type(type: int)

attach_graph_element_to_frame(element: StringName, frame: StringName)

connect_node(from_node: StringName, from_port: int, to_node: StringName, to_port: int, keep_alive: bool = false)

detach_graph_element_from_frame(element: StringName)

disconnect_node(from_node: StringName, from_port: int, to_node: StringName, to_port: int)

force_connection_drag_end()

get_attached_nodes_of_frame(frame: StringName)

get_closest_connection_at_point(point: Vector2, max_distance: float = 4.0) const

get_connection_count(from_node: StringName, from_port: int)

get_connection_line(from_node: Vector2, to_node: Vector2) const

get_connection_list_from_node(node: StringName) const

get_connections_intersecting_with_rect(rect: Rect2) const

get_element_frame(element: StringName)

is_node_connected(from_node: StringName, from_port: int, to_node: StringName, to_port: int)

is_valid_connection_type(from_type: int, to_type: int) const

remove_valid_connection_type(from_type: int, to_type: int)

remove_valid_left_disconnect_type(type: int)

remove_valid_right_disconnect_type(type: int)

set_connection_activity(from_node: StringName, from_port: int, to_node: StringName, to_port: int, amount: float)

set_selected(node: Node)

connection_hover_tint_color

Color(0.1, 0.1, 0.1, 0.6)

connection_valid_target_tint_color

connection_hover_thickness

port_hotzone_inner_extent

port_hotzone_outer_extent

Emitted at the beginning of a GraphElement's movement.

connection_drag_ended() 🔗

Emitted at the end of a connection drag.

connection_drag_started(from_node: StringName, from_port: int, is_output: bool) 🔗

Emitted at the beginning of a connection drag.

connection_from_empty(to_node: StringName, to_port: int, release_position: Vector2) 🔗

Emitted when user drags a connection from an input port into the empty space of the graph.

connection_request(from_node: StringName, from_port: int, to_node: StringName, to_port: int) 🔗

Emitted to the GraphEdit when the connection between the from_port of the from_node GraphNode and the to_port of the to_node GraphNode is attempted to be created.

connection_to_empty(from_node: StringName, from_port: int, release_position: Vector2) 🔗

Emitted when user drags a connection from an output port into the empty space of the graph.

copy_nodes_request() 🔗

Emitted when this GraphEdit captures a ui_copy action (Ctrl + C by default). In general, this signal indicates that the selected GraphElements should be copied.

cut_nodes_request() 🔗

Emitted when this GraphEdit captures a ui_cut action (Ctrl + X by default). In general, this signal indicates that the selected GraphElements should be cut.

delete_nodes_request(nodes: Array[StringName]) 🔗

Emitted when this GraphEdit captures a ui_graph_delete action (Delete by default).

nodes is an array of node names that should be removed. These usually include all selected nodes.

disconnection_request(from_node: StringName, from_port: int, to_node: StringName, to_port: int) 🔗

Emitted to the GraphEdit when the connection between from_port of from_node GraphNode and to_port of to_node GraphNode is attempted to be removed.

duplicate_nodes_request() 🔗

Emitted when this GraphEdit captures a ui_graph_duplicate action (Ctrl + D by default). In general, this signal indicates that the selected GraphElements should be duplicated.

Emitted at the end of a GraphElement's movement.

frame_rect_changed(frame: GraphFrame, new_rect: Rect2) 🔗

Emitted when the GraphFrame frame is resized to new_rect.

graph_elements_linked_to_frame_request(elements: Array, frame: StringName) 🔗

Emitted when one or more GraphElements are dropped onto the GraphFrame named frame, when they were not previously attached to any other one.

elements is an array of GraphElements to be attached.

node_deselected(node: Node) 🔗

Emitted when the given GraphElement node is deselected.

node_selected(node: Node) 🔗

Emitted when the given GraphElement node is selected.

paste_nodes_request() 🔗

Emitted when this GraphEdit captures a ui_paste action (Ctrl + V by default). In general, this signal indicates that previously copied GraphElements should be pasted.

popup_request(at_position: Vector2) 🔗

Emitted when a popup is requested. Happens on right-clicking in the GraphEdit. at_position is the position of the mouse pointer when the signal is sent.

scroll_offset_changed(offset: Vector2) 🔗

Emitted when the scroll offset is changed by the user. It will not be emitted when changed in code.

enum PanningScheme: 🔗

PanningScheme SCROLL_ZOOMS = 0

Mouse Wheel will zoom, Ctrl + Mouse Wheel will move the view.

PanningScheme SCROLL_PANS = 1

Mouse Wheel will move the view, Ctrl + Mouse Wheel will zoom.

GridPattern GRID_PATTERN_LINES = 0

Draw the grid using solid lines.

GridPattern GRID_PATTERN_DOTS = 1

Draw the grid using dots.

bool connection_lines_antialiased = true 🔗

void set_connection_lines_antialiased(value: bool)

bool is_connection_lines_antialiased()

If true, the lines between nodes will use antialiasing.

float connection_lines_curvature = 0.5 🔗

void set_connection_lines_curvature(value: float)

float get_connection_lines_curvature()

The curvature of the lines between the nodes. 0 results in straight lines.

float connection_lines_thickness = 4.0 🔗

void set_connection_lines_thickness(value: float)

float get_connection_lines_thickness()

The thickness of the lines between the nodes.

Array[Dictionary] connections = [] 🔗

void set_connections(value: Array[Dictionary])

Array[Dictionary] get_connection_list()

The connections between GraphNodes.

A connection is represented as a Dictionary in the form of:

Connections with keep_alive set to false may be deleted automatically if invalid during a redraw.

GridPattern grid_pattern = 0 🔗

void set_grid_pattern(value: GridPattern)

GridPattern get_grid_pattern()

The pattern used for drawing the grid.

bool minimap_enabled = true 🔗

void set_minimap_enabled(value: bool)

bool is_minimap_enabled()

If true, the minimap is visible.

float minimap_opacity = 0.65 🔗

void set_minimap_opacity(value: float)

float get_minimap_opacity()

The opacity of the minimap rectangle.

Vector2 minimap_size = Vector2(240, 160) 🔗

void set_minimap_size(value: Vector2)

Vector2 get_minimap_size()

The size of the minimap rectangle. The map itself is based on the size of the grid area and is scaled to fit this rectangle.

PanningScheme panning_scheme = 0 🔗

void set_panning_scheme(value: PanningScheme)

PanningScheme get_panning_scheme()

Defines the control scheme for panning with mouse wheel.

bool right_disconnects = false 🔗

void set_right_disconnects(value: bool)

bool is_right_disconnects_enabled()

If true, enables disconnection of existing connections in the GraphEdit by dragging the right end.

Vector2 scroll_offset = Vector2(0, 0) 🔗

void set_scroll_offset(value: Vector2)

Vector2 get_scroll_offset()

bool show_arrange_button = true 🔗

void set_show_arrange_button(value: bool)

bool is_showing_arrange_button()

If true, the button to automatically arrange graph nodes is visible.

bool show_grid = true 🔗

void set_show_grid(value: bool)

bool is_showing_grid()

If true, the grid is visible.

bool show_grid_buttons = true 🔗

void set_show_grid_buttons(value: bool)

bool is_showing_grid_buttons()

If true, buttons that allow to configure grid and snapping options are visible.

bool show_menu = true 🔗

void set_show_menu(value: bool)

bool is_showing_menu()

If true, the menu toolbar is visible.

bool show_minimap_button = true 🔗

void set_show_minimap_button(value: bool)

bool is_showing_minimap_button()

If true, the button to toggle the minimap is visible.

bool show_zoom_buttons = true 🔗

void set_show_zoom_buttons(value: bool)

bool is_showing_zoom_buttons()

If true, buttons that allow to change and reset the zoom level are visible.

bool show_zoom_label = false 🔗

void set_show_zoom_label(value: bool)

bool is_showing_zoom_label()

If true, the label with the current zoom level is visible. The zoom level is displayed in percents.

int snapping_distance = 20 🔗

void set_snapping_distance(value: int)

int get_snapping_distance()

The snapping distance in pixels, also determines the grid line distance.

bool snapping_enabled = true 🔗

void set_snapping_enabled(value: bool)

bool is_snapping_enabled()

If true, enables snapping.

Dictionary type_names = {} 🔗

void set_type_names(value: Dictionary)

Dictionary get_type_names()

Dictionary of human readable port type names.

void set_zoom(value: float)

The current zoom value.

float zoom_max = 2.0736003 🔗

void set_zoom_max(value: float)

The upper zoom limit.

float zoom_min = 0.23256795 🔗

void set_zoom_min(value: float)

The lower zoom limit.

float zoom_step = 1.2 🔗

void set_zoom_step(value: float)

float get_zoom_step()

The step of each zoom level.

PackedVector2Array _get_connection_line(from_position: Vector2, to_position: Vector2) virtual const 🔗

Virtual method which can be overridden to customize how connections are drawn.

bool _is_in_input_hotzone(in_node: Object, in_port: int, mouse_position: Vector2) virtual 🔗

Returns whether the mouse_position is in the input hot zone.

By default, a hot zone is a Rect2 positioned such that its center is at in_node.GraphNode.get_input_port_position()(in_port) (For output's case, call GraphNode.get_output_port_position() instead). The hot zone's width is twice the Theme Property port_grab_distance_horizontal, and its height is twice the port_grab_distance_vertical.

Below is a sample code to help get started:

bool _is_in_output_hotzone(in_node: Object, in_port: int, mouse_position: Vector2) virtual 🔗

Returns whether the mouse_position is in the output hot zone. For more information on hot zones, see _is_in_input_hotzone().

Below is a sample code to help get started:

bool _is_node_hover_valid(from_node: StringName, from_port: int, to_node: StringName, to_port: int) virtual 🔗

This virtual method can be used to insert additional error detection while the user is dragging a connection over a valid port.

Return true if the connection is indeed valid or return false if the connection is impossible. If the connection is impossible, no snapping to the port and thus no connection request to that port will happen.

In this example a connection to same node is suppressed:

void add_valid_connection_type(from_type: int, to_type: int) 🔗

Allows the connection between two different port types. The port type is defined individually for the left and the right port of each slot with the GraphNode.set_slot() method.

See also is_valid_connection_type() and remove_valid_connection_type().

void add_valid_left_disconnect_type(type: int) 🔗

Allows to disconnect nodes when dragging from the left port of the GraphNode's slot if it has the specified type. See also remove_valid_left_disconnect_type().

void add_valid_right_disconnect_type(type: int) 🔗

Allows to disconnect nodes when dragging from the right port of the GraphNode's slot if it has the specified type. See also remove_valid_right_disconnect_type().

void arrange_nodes() 🔗

Rearranges selected nodes in a layout with minimum crossings between connections and uniform horizontal and vertical gap between nodes.

void attach_graph_element_to_frame(element: StringName, frame: StringName) 🔗

Attaches the element GraphElement to the frame GraphFrame.

void clear_connections() 🔗

Removes all connections between nodes.

Error connect_node(from_node: StringName, from_port: int, to_node: StringName, to_port: int, keep_alive: bool = false) 🔗

Create a connection between the from_port of the from_node GraphNode and the to_port of the to_node GraphNode. If the connection already exists, no connection is created.

Connections with keep_alive set to false may be deleted automatically if invalid during a redraw.

void detach_graph_element_from_frame(element: StringName) 🔗

Detaches the element GraphElement from the GraphFrame it is currently attached to.

void disconnect_node(from_node: StringName, from_port: int, to_node: StringName, to_port: int) 🔗

Removes the connection between the from_port of the from_node GraphNode and the to_port of the to_node GraphNode. If the connection does not exist, no connection is removed.

void force_connection_drag_end() 🔗

Ends the creation of the current connection. In other words, if you are dragging a connection you can use this method to abort the process and remove the line that followed your cursor.

This is best used together with connection_drag_started and connection_drag_ended to add custom behavior like node addition through shortcuts.

Note: This method suppresses any other connection request signals apart from connection_drag_ended.

Array[StringName] get_attached_nodes_of_frame(frame: StringName) 🔗

Returns an array of node names that are attached to the GraphFrame with the given name.

Dictionary get_closest_connection_at_point(point: Vector2, max_distance: float = 4.0) const 🔗

Returns the closest connection to the given point in screen space. If no connection is found within max_distance pixels, an empty Dictionary is returned.

A connection is represented as a Dictionary in the form of:

For example, getting a connection at a given mouse position can be achieved like this:

int get_connection_count(from_node: StringName, from_port: int) 🔗

Returns the number of connections from from_port of from_node.

PackedVector2Array get_connection_line(from_node: Vector2, to_node: Vector2) const 🔗

Returns the points which would make up a connection between from_node and to_node.

Array[Dictionary] get_connection_list_from_node(node: StringName) const 🔗

Returns an Array containing a list of all connections for node.

A connection is represented as a Dictionary in the form of:

Example: Get all connections on a specific port:

Array[Dictionary] get_connections_intersecting_with_rect(rect: Rect2) const 🔗

Returns an Array containing the list of connections that intersect with the given Rect2.

A connection is represented as a Dictionary in the form of:

GraphFrame get_element_frame(element: StringName) 🔗

Returns the GraphFrame that contains the GraphElement with the given name.

HBoxContainer get_menu_hbox() 🔗

Gets the HBoxContainer that contains the zooming and grid snap controls in the top left of the graph. You can use this method to reposition the toolbar or to add your own custom controls to it.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their CanvasItem.visible property.

bool is_node_connected(from_node: StringName, from_port: int, to_node: StringName, to_port: int) 🔗

Returns true if the from_port of the from_node GraphNode is connected to the to_port of the to_node GraphNode.

bool is_valid_connection_type(from_type: int, to_type: int) const 🔗

Returns whether it's possible to make a connection between two different port types. The port type is defined individually for the left and the right port of each slot with the GraphNode.set_slot() method.

See also add_valid_connection_type() and remove_valid_connection_type().

void remove_valid_connection_type(from_type: int, to_type: int) 🔗

Disallows the connection between two different port types previously allowed by add_valid_connection_type(). The port type is defined individually for the left and the right port of each slot with the GraphNode.set_slot() method.

See also is_valid_connection_type().

void remove_valid_left_disconnect_type(type: int) 🔗

Disallows to disconnect nodes when dragging from the left port of the GraphNode's slot if it has the specified type. Use this to disable disconnection previously allowed with add_valid_left_disconnect_type().

void remove_valid_right_disconnect_type(type: int) 🔗

Disallows to disconnect nodes when dragging from the right port of the GraphNode's slot if it has the specified type. Use this to disable disconnection previously allowed with add_valid_right_disconnect_type().

void set_connection_activity(from_node: StringName, from_port: int, to_node: StringName, to_port: int, amount: float) 🔗

Sets the coloration of the connection between from_node's from_port and to_node's to_port with the color provided in the activity theme property. The color is linearly interpolated between the connection color and the activity color using amount as weight.

void set_selected(node: Node) 🔗

Sets the specified node as the one selected.

Color activity = Color(1, 1, 1, 1) 🔗

Color the connection line is interpolated to based on the activity value of a connection (see set_connection_activity()).

Color connection_hover_tint_color = Color(0, 0, 0, 0.3) 🔗

Color which is blended with the connection line when the mouse is hovering over it.

Color connection_rim_color = Color(0.1, 0.1, 0.1, 0.6) 🔗

Color of the rim around each connection line used for making intersecting lines more distinguishable.

Color connection_valid_target_tint_color = Color(1, 1, 1, 0.4) 🔗

Color which is blended with the connection line when the currently dragged connection is hovering over a valid target port.

Color grid_major = Color(1, 1, 1, 0.2) 🔗

Color of major grid lines/dots.

Color grid_minor = Color(1, 1, 1, 0.05) 🔗

Color of minor grid lines/dots.

Color selection_fill = Color(1, 1, 1, 0.3) 🔗

The fill color of the selection rectangle.

Color selection_stroke = Color(1, 1, 1, 0.8) 🔗

The outline color of the selection rectangle.

int connection_hover_thickness = 0 🔗

Widen the line of the connection when the mouse is hovering over it by a percentage factor. A value of 0 disables the highlight. A value of 100 doubles the line width.

int port_hotzone_inner_extent = 22 🔗

The horizontal range within which a port can be grabbed (inner side).

int port_hotzone_outer_extent = 26 🔗

The horizontal range within which a port can be grabbed (outer side).

Texture2D grid_toggle 🔗

The icon for the grid toggle button.

The icon for the layout button for auto-arranging the graph.

Texture2D minimap_toggle 🔗

The icon for the minimap toggle button.

Texture2D snapping_toggle 🔗

The icon for the snapping toggle button.

The icon for the zoom in button.

The icon for the zoom out button.

Texture2D zoom_reset 🔗

The icon for the zoom reset button.

StyleBox menu_panel 🔗

There is currently no description for this theme property. Please help us by contributing one!

The background drawn under the grid.

StyleBox panel_focus 🔗

StyleBox used when the GraphEdit is focused (when used with assistive apps).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (css):
```css
{
    from_node: StringName,
    from_port: int,
    to_node: StringName,
    to_port: int,
    keep_alive: bool
}
```

Example 2 (gdscript):
```gdscript
func _is_in_input_hotzone(in_node, in_port, mouse_position):
    var port_size = Vector2(get_theme_constant("port_grab_distance_horizontal"), get_theme_constant("port_grab_distance_vertical"))
    var port_pos = in_node.get_position() + in_node.get_input_port_position(in_port) - port_size / 2
    var rect = Rect2(port_pos, port_size)

    return rect.has_point(mouse_position)
```

Example 3 (gdscript):
```gdscript
func _is_in_output_hotzone(in_node, in_port, mouse_position):
    var port_size = Vector2(get_theme_constant("port_grab_distance_horizontal"), get_theme_constant("port_grab_distance_vertical"))
    var port_pos = in_node.get_position() + in_node.get_output_port_position(in_port) - port_size / 2
    var rect = Rect2(port_pos, port_size)

    return rect.has_point(mouse_position)
```

Example 4 (go):
```go
func _is_node_hover_valid(from, from_port, to, to_port):
    return from != to
```

---

## GraphElement

**URL:** https://docs.godotengine.org/en/stable/classes/class_graphelement.html

**Contents:**
- GraphElement
- Description
- Properties
- Theme Properties
- Signals
- Property Descriptions
- Theme Property Descriptions
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: Container < Control < CanvasItem < Node < Object

Inherited By: GraphFrame, GraphNode

A container that represents a basic element that can be placed inside a GraphEdit control.

GraphElement allows to create custom elements for a GraphEdit graph. By default such elements can be selected, resized, and repositioned, but they cannot be connected. For a graph element that allows for connections see GraphNode.

Emitted when removing the GraphElement is requested.

dragged(from: Vector2, to: Vector2) 🔗

Emitted when the GraphElement is dragged.

Emitted when the GraphElement is deselected.

Emitted when the GraphElement is selected.

position_offset_changed() 🔗

Emitted when the GraphElement is moved.

Emitted when displaying the GraphElement over other ones is requested. Happens on focusing (clicking into) the GraphElement.

resize_end(new_size: Vector2) 🔗

Emitted when releasing the mouse button after dragging the resizer handle (see resizable).

resize_request(new_size: Vector2) 🔗

Emitted when resizing the GraphElement is requested. Happens on dragging the resizer handle (see resizable).

bool draggable = true 🔗

void set_draggable(value: bool)

If true, the user can drag the GraphElement.

Vector2 position_offset = Vector2(0, 0) 🔗

void set_position_offset(value: Vector2)

Vector2 get_position_offset()

The offset of the GraphElement, relative to the scroll offset of the GraphEdit.

bool resizable = false 🔗

void set_resizable(value: bool)

If true, the user can resize the GraphElement.

Note: Dragging the handle will only emit the resize_request and resize_end signals, the GraphElement needs to be resized manually.

bool selectable = true 🔗

void set_selectable(value: bool)

If true, the user can select the GraphElement.

bool selected = false 🔗

void set_selected(value: bool)

If true, the GraphElement is selected.

The icon used for the resizer, visible when resizable is enabled.

Please read the User-contributed notes policy before submitting a comment.

---

## GraphFrame

**URL:** https://docs.godotengine.org/en/stable/classes/class_graphframe.html

**Contents:**
- GraphFrame
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: GraphElement < Container < Control < CanvasItem < Node < Object

GraphFrame is a special GraphElement that can be used to organize other GraphElements inside a GraphEdit.

GraphFrame is a special GraphElement to which other GraphElements can be attached. It can be configured to automatically resize to enclose all attached GraphElements. If the frame is moved, all the attached GraphElements inside it will be moved as well.

A GraphFrame is always kept behind the connection layer and other GraphElements inside a GraphEdit.

0 (overrides Control)

Color(0.3, 0.3, 0.3, 0.75)

Color(0.875, 0.875, 0.875, 1)

autoshrink_changed() 🔗

Emitted when autoshrink_enabled or autoshrink_margin changes.

bool autoshrink_enabled = true 🔗

void set_autoshrink_enabled(value: bool)

bool is_autoshrink_enabled()

If true, the frame's rect will be adjusted automatically to enclose all attached GraphElements.

int autoshrink_margin = 40 🔗

void set_autoshrink_margin(value: int)

int get_autoshrink_margin()

The margin around the attached nodes that is used to calculate the size of the frame when autoshrink_enabled is true.

int drag_margin = 16 🔗

void set_drag_margin(value: int)

int get_drag_margin()

The margin inside the frame that can be used to drag the frame.

Color tint_color = Color(0.3, 0.3, 0.3, 0.75) 🔗

void set_tint_color(value: Color)

Color get_tint_color()

The color of the frame when tint_color_enabled is true.

bool tint_color_enabled = false 🔗

void set_tint_color_enabled(value: bool)

bool is_tint_color_enabled()

If true, the tint color will be used to tint the frame.

void set_title(value: String)

HBoxContainer get_titlebar_hbox() 🔗

Returns the HBoxContainer used for the title bar, only containing a Label for displaying the title by default.

This can be used to add custom controls to the title bar such as option or close buttons.

Color resizer_color = Color(0.875, 0.875, 0.875, 1) 🔗

The color modulation applied to the resizer icon.

The default StyleBox used for the background of the GraphFrame.

StyleBox panel_selected 🔗

The StyleBox used for the background of the GraphFrame when it is selected.

The StyleBox used for the title bar of the GraphFrame.

StyleBox titlebar_selected 🔗

The StyleBox used for the title bar of the GraphFrame when it is selected.

Please read the User-contributed notes policy before submitting a comment.

---

## GraphNode

**URL:** https://docs.godotengine.org/en/stable/classes/class_graphnode.html

**Contents:**
- GraphNode
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: GraphElement < Container < Control < CanvasItem < Node < Object

A container with connection ports, representing a node in a GraphEdit.

GraphNode allows to create nodes for a GraphEdit graph with customizable content based on its child controls. GraphNode is derived from Container and it is responsible for placing its children on screen. This works similar to VBoxContainer. Children, in turn, provide GraphNode with so-called slots, each of which can have a connection port on either side.

Each GraphNode slot is defined by its index and can provide the node with up to two ports: one on the left, and one on the right. By convention the left port is also referred to as the input port and the right port is referred to as the output port. Each port can be enabled and configured individually, using different type and color. The type is an arbitrary value that you can define using your own considerations. The parent GraphEdit will receive this information on each connect and disconnect request.

Slots can be configured in the Inspector dock once you add at least one child Control. The properties are grouped by each slot's index in the "Slot" section.

Note: While GraphNode is set up using slots and slot indices, connections are made between the ports which are enabled. Because of that GraphEdit uses the port's index and not the slot's index. You can use get_input_port_slot() and get_output_port_slot() to get the slot index from the port index.

3 (overrides Control)

ignore_invalid_connection_type

0 (overrides Control)

_draw_port(slot_index: int, position: Vector2i, left: bool, color: Color) virtual

clear_slot(slot_index: int)

get_input_port_color(port_idx: int)

get_input_port_count()

get_input_port_position(port_idx: int)

get_input_port_slot(port_idx: int)

get_input_port_type(port_idx: int)

get_output_port_color(port_idx: int)

get_output_port_count()

get_output_port_position(port_idx: int)

get_output_port_slot(port_idx: int)

get_output_port_type(port_idx: int)

get_slot_color_left(slot_index: int) const

get_slot_color_right(slot_index: int) const

get_slot_custom_icon_left(slot_index: int) const

get_slot_custom_icon_right(slot_index: int) const

get_slot_type_left(slot_index: int) const

get_slot_type_right(slot_index: int) const

is_slot_draw_stylebox(slot_index: int) const

is_slot_enabled_left(slot_index: int) const

is_slot_enabled_right(slot_index: int) const

set_slot(slot_index: int, enable_left_port: bool, type_left: int, color_left: Color, enable_right_port: bool, type_right: int, color_right: Color, custom_icon_left: Texture2D = null, custom_icon_right: Texture2D = null, draw_stylebox: bool = true)

set_slot_color_left(slot_index: int, color: Color)

set_slot_color_right(slot_index: int, color: Color)

set_slot_custom_icon_left(slot_index: int, custom_icon: Texture2D)

set_slot_custom_icon_right(slot_index: int, custom_icon: Texture2D)

set_slot_draw_stylebox(slot_index: int, enable: bool)

set_slot_enabled_left(slot_index: int, enable: bool)

set_slot_enabled_right(slot_index: int, enable: bool)

set_slot_type_left(slot_index: int, type: int)

set_slot_type_right(slot_index: int, type: int)

Color(0.875, 0.875, 0.875, 1)

slot_sizes_changed() 🔗

Emitted when any slot's size might have changed.

slot_updated(slot_index: int) 🔗

Emitted when any GraphNode's slot is updated.

bool ignore_invalid_connection_type = false 🔗

void set_ignore_invalid_connection_type(value: bool)

bool is_ignoring_valid_connection_type()

If true, you can connect ports with different types, even if the connection was not explicitly allowed in the parent GraphEdit.

FocusMode slots_focus_mode = 3 🔗

void set_slots_focus_mode(value: FocusMode)

FocusMode get_slots_focus_mode()

Determines how connection slots can be focused.

If set to Control.FOCUS_CLICK, connections can only be made with the mouse.

If set to Control.FOCUS_ALL, slots can also be focused using the ProjectSettings.input/ui_up and ProjectSettings.input/ui_down and connected using ProjectSettings.input/ui_left and ProjectSettings.input/ui_right input actions.

If set to Control.FOCUS_ACCESSIBILITY, slot input actions are only enabled when the screen reader is active.

void set_title(value: String)

The text displayed in the GraphNode's title bar.

void _draw_port(slot_index: int, position: Vector2i, left: bool, color: Color) virtual 🔗

There is currently no description for this method. Please help us by contributing one!

void clear_all_slots() 🔗

Disables all slots of the GraphNode. This will remove all input/output ports from the GraphNode.

void clear_slot(slot_index: int) 🔗

Disables the slot with the given slot_index. This will remove the corresponding input and output port from the GraphNode.

Color get_input_port_color(port_idx: int) 🔗

Returns the Color of the input port with the given port_idx.

int get_input_port_count() 🔗

Returns the number of slots with an enabled input port.

Vector2 get_input_port_position(port_idx: int) 🔗

Returns the position of the input port with the given port_idx.

int get_input_port_slot(port_idx: int) 🔗

Returns the corresponding slot index of the input port with the given port_idx.

int get_input_port_type(port_idx: int) 🔗

Returns the type of the input port with the given port_idx.

Color get_output_port_color(port_idx: int) 🔗

Returns the Color of the output port with the given port_idx.

int get_output_port_count() 🔗

Returns the number of slots with an enabled output port.

Vector2 get_output_port_position(port_idx: int) 🔗

Returns the position of the output port with the given port_idx.

int get_output_port_slot(port_idx: int) 🔗

Returns the corresponding slot index of the output port with the given port_idx.

int get_output_port_type(port_idx: int) 🔗

Returns the type of the output port with the given port_idx.

Color get_slot_color_left(slot_index: int) const 🔗

Returns the left (input) Color of the slot with the given slot_index.

Color get_slot_color_right(slot_index: int) const 🔗

Returns the right (output) Color of the slot with the given slot_index.

Texture2D get_slot_custom_icon_left(slot_index: int) const 🔗

Returns the left (input) custom Texture2D of the slot with the given slot_index.

Texture2D get_slot_custom_icon_right(slot_index: int) const 🔗

Returns the right (output) custom Texture2D of the slot with the given slot_index.

int get_slot_type_left(slot_index: int) const 🔗

Returns the left (input) type of the slot with the given slot_index.

int get_slot_type_right(slot_index: int) const 🔗

Returns the right (output) type of the slot with the given slot_index.

HBoxContainer get_titlebar_hbox() 🔗

Returns the HBoxContainer used for the title bar, only containing a Label for displaying the title by default. This can be used to add custom controls to the title bar such as option or close buttons.

bool is_slot_draw_stylebox(slot_index: int) const 🔗

Returns true if the background StyleBox of the slot with the given slot_index is drawn.

bool is_slot_enabled_left(slot_index: int) const 🔗

Returns true if left (input) side of the slot with the given slot_index is enabled.

bool is_slot_enabled_right(slot_index: int) const 🔗

Returns true if right (output) side of the slot with the given slot_index is enabled.

void set_slot(slot_index: int, enable_left_port: bool, type_left: int, color_left: Color, enable_right_port: bool, type_right: int, color_right: Color, custom_icon_left: Texture2D = null, custom_icon_right: Texture2D = null, draw_stylebox: bool = true) 🔗

Sets properties of the slot with the given slot_index.

If enable_left_port/enable_right_port is true, a port will appear and the slot will be able to be connected from this side.

With type_left/type_right an arbitrary type can be assigned to each port. Two ports can be connected if they share the same type, or if the connection between their types is allowed in the parent GraphEdit (see GraphEdit.add_valid_connection_type()). Keep in mind that the GraphEdit has the final say in accepting the connection. Type compatibility simply allows the GraphEdit.connection_request signal to be emitted.

Ports can be further customized using color_left/color_right and custom_icon_left/custom_icon_right. The color parameter adds a tint to the icon. The custom icon can be used to override the default port dot.

Additionally, draw_stylebox can be used to enable or disable drawing of the background stylebox for each slot. See slot.

Individual properties can also be set using one of the set_slot_* methods.

Note: This method only sets properties of the slot. To create the slot itself, add a Control-derived child to the GraphNode.

void set_slot_color_left(slot_index: int, color: Color) 🔗

Sets the Color of the left (input) side of the slot with the given slot_index to color.

void set_slot_color_right(slot_index: int, color: Color) 🔗

Sets the Color of the right (output) side of the slot with the given slot_index to color.

void set_slot_custom_icon_left(slot_index: int, custom_icon: Texture2D) 🔗

Sets the custom Texture2D of the left (input) side of the slot with the given slot_index to custom_icon.

void set_slot_custom_icon_right(slot_index: int, custom_icon: Texture2D) 🔗

Sets the custom Texture2D of the right (output) side of the slot with the given slot_index to custom_icon.

void set_slot_draw_stylebox(slot_index: int, enable: bool) 🔗

Toggles the background StyleBox of the slot with the given slot_index.

void set_slot_enabled_left(slot_index: int, enable: bool) 🔗

Toggles the left (input) side of the slot with the given slot_index. If enable is true, a port will appear on the left side and the slot will be able to be connected from this side.

void set_slot_enabled_right(slot_index: int, enable: bool) 🔗

Toggles the right (output) side of the slot with the given slot_index. If enable is true, a port will appear on the right side and the slot will be able to be connected from this side.

void set_slot_type_left(slot_index: int, type: int) 🔗

Sets the left (input) type of the slot with the given slot_index to type. If the value is negative, all connections will be disallowed to be created via user inputs.

void set_slot_type_right(slot_index: int, type: int) 🔗

Sets the right (output) type of the slot with the given slot_index to type. If the value is negative, all connections will be disallowed to be created via user inputs.

Color resizer_color = Color(0.875, 0.875, 0.875, 1) 🔗

The color modulation applied to the resizer icon.

int port_h_offset = 0 🔗

Horizontal offset for the ports.

The vertical distance between ports.

The icon used for representing ports.

The default background for the slot area of the GraphNode.

StyleBox panel_focus 🔗

StyleBox used when the GraphNode is focused (when used with assistive apps).

StyleBox panel_selected 🔗

The StyleBox used for the slot area when selected.

The StyleBox used for each slot of the GraphNode.

StyleBox slot_selected 🔗

StyleBox used when the slot is focused (when used with assistive apps).

The StyleBox used for the title bar of the GraphNode.

StyleBox titlebar_selected 🔗

The StyleBox used for the title bar of the GraphNode when it is selected.

Please read the User-contributed notes policy before submitting a comment.

---

## GridContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_gridcontainer.html

**Contents:**
- GridContainer
- Description
- Tutorials
- Properties
- Theme Properties
- Property Descriptions
- Theme Property Descriptions
- User-contributed notes

Inherits: Container < Control < CanvasItem < Node < Object

A container that arranges its child controls in a grid layout.

GridContainer arranges its child controls in a grid layout. The number of columns is specified by the columns property, whereas the number of rows depends on how many are needed for the child controls. The number of rows and columns is preserved for every size of the container.

Note: GridContainer only works with child nodes inheriting from Control. It won't rearrange child nodes inheriting from Node2D.

Operating System Testing Demo

void set_columns(value: int)

The number of columns in the GridContainer. If modified, GridContainer reorders its Control-derived children to accommodate the new layout.

int h_separation = 4 🔗

The horizontal separation of child nodes.

int v_separation = 4 🔗

The vertical separation of child nodes.

Please read the User-contributed notes policy before submitting a comment.

---

## Handling quit requests

**URL:** https://docs.godotengine.org/en/stable/tutorials/inputs/handling_quit_requests.html

**Contents:**
- Handling quit requests
- Quitting
- Handling the notification
- On mobile devices
- Sending your own quit notification
- User-contributed notes

Most platforms have the option to request the application to quit. On desktops, this is usually done with the "x" icon on the window title bar. On mobile devices, the app can quit at any time while it is suspended to the background.

On desktop and web platforms, Node receives a special NOTIFICATION_WM_CLOSE_REQUEST notification when quitting is requested from the window manager.

Handling the notification is done as follows (on any node):

It is important to note that by default, Godot apps have the built-in behavior to quit when quit is requested from the window manager. This can be changed, so that the user can take care of the complete quitting procedure:

There is no direct equivalent to NOTIFICATION_WM_CLOSE_REQUEST on mobile platforms. Due to the nature of mobile operating systems, the only place that you can run code prior to quitting is when the app is being suspended to the background. On both Android and iOS, the app can be killed while suspended at any time by either the user or the OS. A way to plan ahead for this possibility is to utilize NOTIFICATION_APPLICATION_PAUSED in order to perform any needed actions as the app is being suspended.

On iOS, you only have approximately 5 seconds to finish a task started by this signal. If you go over this allotment, iOS will kill the app instead of pausing it.

On Android, pressing the Back button will exit the application if Application > Config > Quit On Go Back is checked in the Project Settings (which is the default). This will fire NOTIFICATION_WM_GO_BACK_REQUEST.

While forcing the application to close can be done by calling SceneTree.quit, doing so will not send the NOTIFICATION_WM_CLOSE_REQUEST to the nodes in the scene tree. Quitting by calling SceneTree.quit will not allow custom actions to complete (such as saving, confirming the quit, or debugging), even if you try to delay the line that forces the quit.

Instead, if you want to notify the nodes in the scene tree about the upcoming program termination, you should send the notification yourself:

Sending this notification will inform all nodes about the program termination, but will not terminate the program itself unlike in 3.X. In order to achieve the previous behavior, SceneTree.quit should be called after the notification.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (go):
```go
func _notification(what):
    if what == NOTIFICATION_WM_CLOSE_REQUEST:
        get_tree().quit() # default behavior
```

Example 2 (json):
```json
public override void _Notification(int what)
{
    if (what == NotificationWMCloseRequest)
    {
        GetTree().Quit(); // default behavior
    }
}
```

Example 3 (unknown):
```unknown
get_tree().set_auto_accept_quit(false)
```

Example 4 (unknown):
```unknown
GetTree().AutoAcceptQuit = false;
```

---

## HBoxContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_hboxcontainer.html

**Contents:**
- HBoxContainer
- Description
- Tutorials
- User-contributed notes

Inherits: BoxContainer < Container < Control < CanvasItem < Node < Object

Inherited By: EditorResourcePicker, EditorToaster, OpenXRInteractionProfileEditorBase

A container that arranges its child controls horizontally.

A variant of BoxContainer that can only arrange its child controls horizontally. Child controls are rearranged automatically when their minimum size changes.

Please read the User-contributed notes policy before submitting a comment.

---

## HFlowContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_hflowcontainer.html

**Contents:**
- HFlowContainer
- Description
- Tutorials
- User-contributed notes

Inherits: FlowContainer < Container < Control < CanvasItem < Node < Object

A container that arranges its child controls horizontally and wraps them around at the borders.

A variant of FlowContainer that can only arrange its child controls horizontally, wrapping them around at the borders. This is similar to how text in a book wraps around when no more words can fit on a line.

Please read the User-contributed notes policy before submitting a comment.

---

## HSeparator

**URL:** https://docs.godotengine.org/en/stable/classes/class_hseparator.html

**Contents:**
- HSeparator
- Description
- User-contributed notes

Inherits: Separator < Control < CanvasItem < Node < Object

A horizontal line used for separating other controls.

A horizontal separator used for separating other controls that are arranged vertically. HSeparator is purely visual and normally drawn as a StyleBoxLine.

Please read the User-contributed notes policy before submitting a comment.

---

## HSplitContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_hsplitcontainer.html

**Contents:**
- HSplitContainer
- Description
- Tutorials
- User-contributed notes

Inherits: SplitContainer < Container < Control < CanvasItem < Node < Object

A container that splits two child controls horizontally and provides a grabber for adjusting the split ratio.

A container that accepts only two child controls, then arranges them horizontally and creates a divisor between them. The divisor can be dragged around to change the size relation between the child controls.

Please read the User-contributed notes policy before submitting a comment.

---

## HTML5 shell class reference

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/web/html5_shell_classref.html

**Contents:**
- HTML5 shell class reference
- Engine
  - Static Methods
  - Instance Methods
- Engine configuration
  - Properties
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

Projects exported for the Web expose the Engine() class to the JavaScript environment, that allows fine control over the engine's start-up process.

This API is built in an asynchronous manner and requires basic understanding of Promises.

The Engine class provides methods for loading and starting exported projects on the Web. For default export settings, this is already part of the exported HTML page. To understand practical use of the Engine class, see Custom HTML page for Web export.

load ( string basePath )

isWebGLAvailable ( [ number majorVersion=1 ] )

init ( [ string basePath ] )

preloadFile ( string|ArrayBuffer file [, string path ] )

start ( EngineConfig override )

startGame ( EngineConfig override )

copyToFS ( string path, ArrayBuffer buffer )

Create a new Engine instance with the given configuration.

initConfig (EngineConfig()) -- The initial config for this instance.

Load the engine from the specified base path.

basePath (string()) -- Base path of the engine to load.

A Promise that resolves once the engine is loaded.

Unload the engine to free memory.

This method will be called automatically depending on the configuration. See unloadAfterInit.

Check whether WebGL is available. Optionally, specify a particular version of WebGL to check for.

majorVersion (number()) -- The major WebGL version to check for.

If the given major version of WebGL is available.

Initialize the engine instance. Optionally, pass the base path to the engine to load it, if it hasn't been loaded yet. See Engine.load().

basePath (string()) -- Base path of the engine to load.

A Promise that resolves once the engine is loaded and initialized.

Load a file so it is available in the instance's file system once it runs. Must be called before starting the instance.

If not provided, the path is derived from the URL of the loaded file.

file (string|ArrayBuffer()) -- The file to preload. If a string the file will be loaded from that path. If an ArrayBuffer or a view on one, the buffer will used as the content of the file.

If a string the file will be loaded from that path.

If an ArrayBuffer or a view on one, the buffer will used as the content of the file.

path (string()) -- Path by which the file will be accessible. Required, if file is not a string.

A Promise that resolves once the file is loaded.

Start the engine instance using the given override configuration (if any). startGame can be used in typical cases instead.

This will initialize the instance if it is not initialized. For manual initialization, see init. The engine must be loaded beforehand.

Fails if a canvas cannot be found on the page, or not specified in the configuration.

override (EngineConfig()) -- An optional configuration override.

Promise that resolves once the engine started.

Start the game instance using the given configuration override (if any).

This will initialize the instance if it is not initialized. For manual initialization, see init.

This will load the engine if it is not loaded, and preload the main pck.

This method expects the initial config (or the override) to have both the executable and mainPack properties set (normally done by the editor during export).

override (EngineConfig()) -- An optional configuration override.

Promise that resolves once the game started.

Create a file at the specified path with the passed as buffer in the instance's file system.

path (string()) -- The location where the file will be created.

buffer (ArrayBuffer()) -- The content of the file.

Request that the current instance quit.

This is akin the user pressing the close button in the window manager, and will have no effect if the engine has crashed, or is stuck in a loop.

An object used to configure the Engine instance based on godot export options, and to override those in custom HTML templates if needed.

The Engine configuration object. This is just a typedef, create it like a regular object, e.g.:

const MyConfig = { executable: 'godot', unloadAfterInit: false }

Property Descriptions

Whether the unload the engine automatically after the instance is initialized.

The HTML DOM Canvas object to use.

By default, the first canvas element in the document will be used is none is specified.

The name of the WASM file without the extension. (Set by Godot Editor export process).

An alternative name for the game pck to load. The executable name is used otherwise.

Specify a language code to select the proper localization for the game.

The browser locale will be used if none is specified. See complete list of supported locales.

The canvas resize policy determines how the canvas should be resized by Godot.

0 means Godot won't do any resizing. This is useful if you want to control the canvas size from javascript code in your template.

1 means Godot will resize the canvas on start, and when changing window size via engine functions.

2 means Godot will adapt the canvas size to match the whole browser window.

The arguments to be passed as command line arguments on startup.

See command line tutorial.

Note: startGame will always add the --main-pack argument.

A callback function for handling Godot's OS.execute calls.

This is for example used in the Web Editor template to switch between Project Manager and editor, and for running the game.

path (string()) -- The path that Godot's wants executed.

args (Array.) -- The arguments of the "command" to execute.

A callback function for being notified when the Godot instance quits.

Note: This function will not be called if the engine crashes or become unresponsive.

status_code (number()) -- The status code returned by Godot on exit.

A callback function for displaying download progress.

The function is called once per frame while downloading files, so the usage of requestAnimationFrame() is not necessary.

If the callback function receives a total amount of bytes as 0, this means that it is impossible to calculate. Possible reasons include:

Files are delivered with server-side chunked compression

Files are delivered with server-side compression on Chromium

Not all file downloads have started yet (usually on servers without multi-threading)

current (number()) -- The current amount of downloaded bytes so far.

total (number()) -- The total amount of bytes to be downloaded.

A callback function for handling the standard output stream. This method should usually only be used in debug pages.

By default, console.log() is used.

var_args (*()) -- A variadic number of arguments to be printed.

A callback function for handling the standard error stream. This method should usually only be used in debug pages.

By default, console.error() is used.

var_args (*()) -- A variadic number of arguments to be printed as errors.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventJoypadButton

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventjoypadbutton.html

**Contents:**
- InputEventJoypadButton
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEvent < Resource < RefCounted < Object

Represents a gamepad button being pressed or released.

Input event type for gamepad buttons. For gamepad analog sticks and joysticks, see InputEventJoypadMotion.

JoyButton button_index = 0 🔗

void set_button_index(value: JoyButton)

JoyButton get_button_index()

Button identifier. One of the JoyButton button constants.

bool pressed = false 🔗

void set_pressed(value: bool)

If true, the button's state is pressed. If false, the button's state is released.

float pressure = 0.0 🔗

void set_pressure(value: float)

Deprecated: This property is never set by the engine and is always 0.

Please read the User-contributed notes policy before submitting a comment.

---

## InputEventMouseButton

**URL:** https://docs.godotengine.org/en/stable/classes/class_inputeventmousebutton.html

**Contents:**
- InputEventMouseButton
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: InputEventMouse < InputEventWithModifiers < InputEventFromWindow < InputEvent < Resource < RefCounted < Object

Represents a mouse button being pressed or released.

Stores information about mouse click events. See Node._input().

Note: On Wear OS devices, rotary input is mapped to @GlobalScope.MOUSE_BUTTON_WHEEL_UP and @GlobalScope.MOUSE_BUTTON_WHEEL_DOWN. This can be changed to @GlobalScope.MOUSE_BUTTON_WHEEL_LEFT and @GlobalScope.MOUSE_BUTTON_WHEEL_RIGHT with the ProjectSettings.input_devices/pointing/android/rotary_input_scroll_axis setting.

Mouse and input coordinates

MouseButton button_index = 0 🔗

void set_button_index(value: MouseButton)

MouseButton get_button_index()

The mouse button identifier, one of the MouseButton button or button wheel constants.

bool canceled = false 🔗

void set_canceled(value: bool)

If true, the mouse button event has been canceled.

bool double_click = false 🔗

void set_double_click(value: bool)

bool is_double_click()

If true, the mouse button's state is a double-click.

void set_factor(value: float)

The amount (or delta) of the event. When used for high-precision scroll events, this indicates the scroll amount (vertical or horizontal). This is only supported on some platforms; the reported sensitivity varies depending on the platform. May be 0 if not supported.

bool pressed = false 🔗

void set_pressed(value: bool)

If true, the mouse button's state is pressed. If false, the mouse button's state is released.

Please read the User-contributed notes policy before submitting a comment.

---

## Input

**URL:** https://docs.godotengine.org/en/stable/classes/class_input.html

**Contents:**
- Input
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

A singleton for handling inputs.

The Input singleton handles key presses, mouse buttons and movement, gamepads, and input actions. Actions and their events can be set in the Input Map tab in Project > Project Settings, or with the InputMap class.

Note: Input's methods reflect the global input state and are not affected by Control.accept_event() or Viewport.set_input_as_handled(), as those methods only deal with the way input is propagated in the SceneTree.

Inputs documentation index

2D Dodge The Creeps Demo

emulate_mouse_from_touch

emulate_touch_from_mouse

use_accumulated_input

action_press(action: StringName, strength: float = 1.0)

action_release(action: StringName)

add_joy_mapping(mapping: String, update_existing: bool = false)

flush_buffered_events()

get_accelerometer() const

get_action_raw_strength(action: StringName, exact_match: bool = false) const

get_action_strength(action: StringName, exact_match: bool = false) const

get_axis(negative_action: StringName, positive_action: StringName) const

get_connected_joypads()

get_current_cursor_shape() const

get_gyroscope() const

get_joy_axis(device: int, axis: JoyAxis) const

get_joy_guid(device: int) const

get_joy_info(device: int) const

get_joy_name(device: int)

get_joy_vibration_duration(device: int)

get_joy_vibration_strength(device: int)

get_last_mouse_screen_velocity()

get_last_mouse_velocity()

get_magnetometer() const

BitField[MouseButtonMask]

get_mouse_button_mask() const

get_vector(negative_x: StringName, positive_x: StringName, negative_y: StringName, positive_y: StringName, deadzone: float = -1.0) const

is_action_just_pressed(action: StringName, exact_match: bool = false) const

is_action_just_pressed_by_event(action: StringName, event: InputEvent, exact_match: bool = false) const

is_action_just_released(action: StringName, exact_match: bool = false) const

is_action_just_released_by_event(action: StringName, event: InputEvent, exact_match: bool = false) const

is_action_pressed(action: StringName, exact_match: bool = false) const

is_anything_pressed() const

is_joy_button_pressed(device: int, button: JoyButton) const

is_joy_known(device: int)

is_key_label_pressed(keycode: Key) const

is_key_pressed(keycode: Key) const

is_mouse_button_pressed(button: MouseButton) const

is_physical_key_pressed(keycode: Key) const

parse_input_event(event: InputEvent)

remove_joy_mapping(guid: String)

set_accelerometer(value: Vector3)

set_custom_mouse_cursor(image: Resource, shape: CursorShape = 0, hotspot: Vector2 = Vector2(0, 0))

set_default_cursor_shape(shape: CursorShape = 0)

set_gravity(value: Vector3)

set_gyroscope(value: Vector3)

set_magnetometer(value: Vector3)

should_ignore_device(vendor_id: int, product_id: int) const

start_joy_vibration(device: int, weak_magnitude: float, strong_magnitude: float, duration: float = 0)

stop_joy_vibration(device: int)

vibrate_handheld(duration_ms: int = 500, amplitude: float = -1.0)

warp_mouse(position: Vector2)

joy_connection_changed(device: int, connected: bool) 🔗

Emitted when a joypad device has been connected or disconnected.

MouseMode MOUSE_MODE_VISIBLE = 0

Makes the mouse cursor visible if it is hidden.

MouseMode MOUSE_MODE_HIDDEN = 1

Makes the mouse cursor hidden if it is visible.

MouseMode MOUSE_MODE_CAPTURED = 2

Captures the mouse. The mouse will be hidden and its position locked at the center of the window manager's window.

Note: If you want to process the mouse's movement in this mode, you need to use InputEventMouseMotion.relative.

MouseMode MOUSE_MODE_CONFINED = 3

Confines the mouse cursor to the game window, and make it visible.

MouseMode MOUSE_MODE_CONFINED_HIDDEN = 4

Confines the mouse cursor to the game window, and make it hidden.

MouseMode MOUSE_MODE_MAX = 5

Max value of the MouseMode.

CursorShape CURSOR_ARROW = 0

Arrow cursor. Standard, default pointing cursor.

CursorShape CURSOR_IBEAM = 1

I-beam cursor. Usually used to show where the text cursor will appear when the mouse is clicked.

CursorShape CURSOR_POINTING_HAND = 2

Pointing hand cursor. Usually used to indicate the pointer is over a link or other interactable item.

CursorShape CURSOR_CROSS = 3

Cross cursor. Typically appears over regions in which a drawing operation can be performed or for selections.

CursorShape CURSOR_WAIT = 4

Wait cursor. Indicates that the application is busy performing an operation, and that it cannot be used during the operation (e.g. something is blocking its main thread).

CursorShape CURSOR_BUSY = 5

Busy cursor. Indicates that the application is busy performing an operation, and that it is still usable during the operation.

CursorShape CURSOR_DRAG = 6

Drag cursor. Usually displayed when dragging something.

Note: Windows lacks a dragging cursor, so CURSOR_DRAG is the same as CURSOR_MOVE for this platform.

CursorShape CURSOR_CAN_DROP = 7

Can drop cursor. Usually displayed when dragging something to indicate that it can be dropped at the current position.

CursorShape CURSOR_FORBIDDEN = 8

Forbidden cursor. Indicates that the current action is forbidden (for example, when dragging something) or that the control at a position is disabled.

CursorShape CURSOR_VSIZE = 9

Vertical resize mouse cursor. A double-headed vertical arrow. It tells the user they can resize the window or the panel vertically.

CursorShape CURSOR_HSIZE = 10

Horizontal resize mouse cursor. A double-headed horizontal arrow. It tells the user they can resize the window or the panel horizontally.

CursorShape CURSOR_BDIAGSIZE = 11

Window resize mouse cursor. The cursor is a double-headed arrow that goes from the bottom left to the top right. It tells the user they can resize the window or the panel both horizontally and vertically.

CursorShape CURSOR_FDIAGSIZE = 12

Window resize mouse cursor. The cursor is a double-headed arrow that goes from the top left to the bottom right, the opposite of CURSOR_BDIAGSIZE. It tells the user they can resize the window or the panel both horizontally and vertically.

CursorShape CURSOR_MOVE = 13

Move cursor. Indicates that something can be moved.

CursorShape CURSOR_VSPLIT = 14

Vertical split mouse cursor. On Windows, it's the same as CURSOR_VSIZE.

CursorShape CURSOR_HSPLIT = 15

Horizontal split mouse cursor. On Windows, it's the same as CURSOR_HSIZE.

CursorShape CURSOR_HELP = 16

Help cursor. Usually a question mark.

bool emulate_mouse_from_touch 🔗

void set_emulate_mouse_from_touch(value: bool)

bool is_emulating_mouse_from_touch()

If true, sends mouse input events when tapping or swiping on the touchscreen. See also ProjectSettings.input_devices/pointing/emulate_mouse_from_touch.

bool emulate_touch_from_mouse 🔗

void set_emulate_touch_from_mouse(value: bool)

bool is_emulating_touch_from_mouse()

If true, sends touch input events when clicking or dragging the mouse. See also ProjectSettings.input_devices/pointing/emulate_touch_from_mouse.

MouseMode mouse_mode 🔗

void set_mouse_mode(value: MouseMode)

MouseMode get_mouse_mode()

Controls the mouse mode.

bool use_accumulated_input 🔗

void set_use_accumulated_input(value: bool)

bool is_using_accumulated_input()

If true, similar input events sent by the operating system are accumulated. When input accumulation is enabled, all input events generated during a frame will be merged and emitted when the frame is done rendering. Therefore, this limits the number of input method calls per second to the rendering FPS.

Input accumulation can be disabled to get slightly more precise/reactive input at the cost of increased CPU usage. In applications where drawing freehand lines is required, input accumulation should generally be disabled while the user is drawing the line to get results that closely follow the actual input.

Note: Input accumulation is enabled by default.

void action_press(action: StringName, strength: float = 1.0) 🔗

This will simulate pressing the specified action.

The strength can be used for non-boolean actions, it's ranged between 0 and 1 representing the intensity of the given action.

Note: This method will not cause any Node._input() calls. It is intended to be used with is_action_pressed() and is_action_just_pressed(). If you want to simulate _input, use parse_input_event() instead.

void action_release(action: StringName) 🔗

If the specified action is already pressed, this will release it.

void add_joy_mapping(mapping: String, update_existing: bool = false) 🔗

Adds a new mapping entry (in SDL2 format) to the mapping database. Optionally update already connected devices.

void flush_buffered_events() 🔗

Sends all input events which are in the current buffer to the game loop. These events may have been buffered as a result of accumulated input (use_accumulated_input) or agile input flushing (ProjectSettings.input_devices/buffering/agile_event_flushing).

The engine will already do this itself at key execution points (at least once per frame). However, this can be useful in advanced cases where you want precise control over the timing of event handling.

Vector3 get_accelerometer() const 🔗

Returns the acceleration in m/s² of the device's accelerometer sensor, if the device has one. Otherwise, the method returns Vector3.ZERO.

Note this method returns an empty Vector3 when running from the editor even when your device has an accelerometer. You must export your project to a supported device to read values from the accelerometer.

Note: This method only works on Android and iOS. On other platforms, it always returns Vector3.ZERO.

Note: For Android, ProjectSettings.input_devices/sensors/enable_accelerometer must be enabled.

float get_action_raw_strength(action: StringName, exact_match: bool = false) const 🔗

Returns a value between 0 and 1 representing the raw intensity of the given action, ignoring the action's deadzone. In most cases, you should use get_action_strength() instead.

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

float get_action_strength(action: StringName, exact_match: bool = false) const 🔗

Returns a value between 0 and 1 representing the intensity of the given action. In a joypad, for example, the further away the axis (analog sticks or L2, R2 triggers) is from the dead zone, the closer the value will be to 1. If the action is mapped to a control that has no axis such as the keyboard, the value returned will be 0 or 1.

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

float get_axis(negative_action: StringName, positive_action: StringName) const 🔗

Get axis input by specifying two actions, one negative and one positive.

This is a shorthand for writing Input.get_action_strength("positive_action") - Input.get_action_strength("negative_action").

Array[int] get_connected_joypads() 🔗

Returns an Array containing the device IDs of all currently connected joypads.

CursorShape get_current_cursor_shape() const 🔗

Returns the currently assigned cursor shape.

Vector3 get_gravity() const 🔗

Returns the gravity in m/s² of the device's accelerometer sensor, if the device has one. Otherwise, the method returns Vector3.ZERO.

Note: This method only works on Android and iOS. On other platforms, it always returns Vector3.ZERO.

Note: For Android, ProjectSettings.input_devices/sensors/enable_gravity must be enabled.

Vector3 get_gyroscope() const 🔗

Returns the rotation rate in rad/s around a device's X, Y, and Z axes of the gyroscope sensor, if the device has one. Otherwise, the method returns Vector3.ZERO.

Note: This method only works on Android and iOS. On other platforms, it always returns Vector3.ZERO.

Note: For Android, ProjectSettings.input_devices/sensors/enable_gyroscope must be enabled.

float get_joy_axis(device: int, axis: JoyAxis) const 🔗

Returns the current value of the joypad axis at index axis.

String get_joy_guid(device: int) const 🔗

Returns an SDL2-compatible device GUID on platforms that use gamepad remapping, e.g. 030000004c050000c405000000010000. Returns an empty string if it cannot be found. Godot uses the SDL2 game controller database to determine gamepad names and mappings based on this GUID.

On Windows, all XInput joypad GUIDs will be overridden by Godot to __XINPUT_DEVICE__, because their mappings are the same.

Dictionary get_joy_info(device: int) const 🔗

Returns a dictionary with extra platform-specific information about the device, e.g. the raw gamepad name from the OS or the Steam Input index.

On Windows, Linux, and macOS, the dictionary contains the following fields:

raw_name: The name of the controller as it came from the OS, before getting renamed by the controller database.

vendor_id: The USB vendor ID of the device.

product_id: The USB product ID of the device.

steam_input_index: The Steam Input gamepad index, if the device is not a Steam Input device this key won't be present.

On Windows, the dictionary can have an additional field:

xinput_index: The index of the controller in the XInput system. This key won't be present for devices not handled by XInput.

Note: The returned dictionary is always empty on Android, iOS, visionOS, and Web.

String get_joy_name(device: int) 🔗

Returns the name of the joypad at the specified device index, e.g. PS4 Controller. Godot uses the SDL2 game controller database to determine gamepad names.

float get_joy_vibration_duration(device: int) 🔗

Returns the duration of the current vibration effect in seconds.

Vector2 get_joy_vibration_strength(device: int) 🔗

Returns the strength of the joypad vibration: x is the strength of the weak motor, and y is the strength of the strong motor.

Vector2 get_last_mouse_screen_velocity() 🔗

Returns the last mouse velocity in screen coordinates. To provide a precise and jitter-free velocity, mouse velocity is only calculated every 0.1s. Therefore, mouse velocity will lag mouse movements.

Vector2 get_last_mouse_velocity() 🔗

Returns the last mouse velocity. To provide a precise and jitter-free velocity, mouse velocity is only calculated every 0.1s. Therefore, mouse velocity will lag mouse movements.

Vector3 get_magnetometer() const 🔗

Returns the magnetic field strength in micro-Tesla for all axes of the device's magnetometer sensor, if the device has one. Otherwise, the method returns Vector3.ZERO.

Note: This method only works on Android and iOS. On other platforms, it always returns Vector3.ZERO.

Note: For Android, ProjectSettings.input_devices/sensors/enable_magnetometer must be enabled.

BitField[MouseButtonMask] get_mouse_button_mask() const 🔗

Returns mouse buttons as a bitmask. If multiple mouse buttons are pressed at the same time, the bits are added together. Equivalent to DisplayServer.mouse_get_button_state().

Vector2 get_vector(negative_x: StringName, positive_x: StringName, negative_y: StringName, positive_y: StringName, deadzone: float = -1.0) const 🔗

Gets an input vector by specifying four actions for the positive and negative X and Y axes.

This method is useful when getting vector input, such as from a joystick, directional pad, arrows, or WASD. The vector has its length limited to 1 and has a circular deadzone, which is useful for using vector input as movement.

By default, the deadzone is automatically calculated from the average of the action deadzones. However, you can override the deadzone to be whatever you want (on the range of 0 to 1).

bool is_action_just_pressed(action: StringName, exact_match: bool = false) const 🔗

Returns true when the user has started pressing the action event in the current frame or physics tick. It will only return true on the frame or tick that the user pressed down the button.

This is useful for code that needs to run only once when an action is pressed, instead of every frame while it's pressed.

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

Note: Returning true does not imply that the action is still pressed. An action can be pressed and released again rapidly, and true will still be returned so as not to miss input.

Note: Due to keyboard ghosting, is_action_just_pressed() may return false even if one of the action's keys is pressed. See Input examples in the documentation for more information.

Note: During input handling (e.g. Node._input()), use InputEvent.is_action_pressed() instead to query the action state of the current event. See also is_action_just_pressed_by_event().

bool is_action_just_pressed_by_event(action: StringName, event: InputEvent, exact_match: bool = false) const 🔗

Returns true when the user has started pressing the action event in the current frame or physics tick, and the first event that triggered action press in the current frame/physics tick was event. It will only return true on the frame or tick that the user pressed down the button.

This is useful for code that needs to run only once when an action is pressed, and the action is processed during input handling (e.g. Node._input()).

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

Note: Returning true does not imply that the action is still pressed. An action can be pressed and released again rapidly, and true will still be returned so as not to miss input.

Note: Due to keyboard ghosting, is_action_just_pressed() may return false even if one of the action's keys is pressed. See Input examples in the documentation for more information.

bool is_action_just_released(action: StringName, exact_match: bool = false) const 🔗

Returns true when the user stops pressing the action event in the current frame or physics tick. It will only return true on the frame or tick that the user releases the button.

Note: Returning true does not imply that the action is still not pressed. An action can be released and pressed again rapidly, and true will still be returned so as not to miss input.

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

Note: During input handling (e.g. Node._input()), use InputEvent.is_action_released() instead to query the action state of the current event. See also is_action_just_released_by_event().

bool is_action_just_released_by_event(action: StringName, event: InputEvent, exact_match: bool = false) const 🔗

Returns true when the user stops pressing the action event in the current frame or physics tick, and the first event that triggered action release in the current frame/physics tick was event. It will only return true on the frame or tick that the user releases the button.

This is useful when an action is processed during input handling (e.g. Node._input()).

Note: Returning true does not imply that the action is still not pressed. An action can be released and pressed again rapidly, and true will still be returned so as not to miss input.

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

bool is_action_pressed(action: StringName, exact_match: bool = false) const 🔗

Returns true if you are pressing the action event.

If exact_match is false, it ignores additional input modifiers for InputEventKey and InputEventMouseButton events, and the direction for InputEventJoypadMotion events.

Note: Due to keyboard ghosting, is_action_pressed() may return false even if one of the action's keys is pressed. See Input examples in the documentation for more information.

bool is_anything_pressed() const 🔗

Returns true if any action, key, joypad button, or mouse button is being pressed. This will also return true if any action is simulated via code by calling action_press().

bool is_joy_button_pressed(device: int, button: JoyButton) const 🔗

Returns true if you are pressing the joypad button at index button.

bool is_joy_known(device: int) 🔗

Returns true if the system knows the specified device. This means that it sets all button and axis indices. Unknown joypads are not expected to match these constants, but you can still retrieve events from them.

bool is_key_label_pressed(keycode: Key) const 🔗

Returns true if you are pressing the key with the keycode printed on it. You can pass a Key constant or any Unicode character code.

bool is_key_pressed(keycode: Key) const 🔗

Returns true if you are pressing the Latin key in the current keyboard layout. You can pass a Key constant.

is_key_pressed() is only recommended over is_physical_key_pressed() in non-game applications. This ensures that shortcut keys behave as expected depending on the user's keyboard layout, as keyboard shortcuts are generally dependent on the keyboard layout in non-game applications. If in doubt, use is_physical_key_pressed().

Note: Due to keyboard ghosting, is_key_pressed() may return false even if one of the action's keys is pressed. See Input examples in the documentation for more information.

bool is_mouse_button_pressed(button: MouseButton) const 🔗

Returns true if you are pressing the mouse button specified with MouseButton.

bool is_physical_key_pressed(keycode: Key) const 🔗

Returns true if you are pressing the key in the physical location on the 101/102-key US QWERTY keyboard. You can pass a Key constant.

is_physical_key_pressed() is recommended over is_key_pressed() for in-game actions, as it will make W/A/S/D layouts work regardless of the user's keyboard layout. is_physical_key_pressed() will also ensure that the top row number keys work on any keyboard layout. If in doubt, use is_physical_key_pressed().

Note: Due to keyboard ghosting, is_physical_key_pressed() may return false even if one of the action's keys is pressed. See Input examples in the documentation for more information.

void parse_input_event(event: InputEvent) 🔗

Feeds an InputEvent to the game. Can be used to artificially trigger input events from code. Also generates Node._input() calls.

Note: Calling this function has no influence on the operating system. So for example sending an InputEventMouseMotion will not move the OS mouse cursor to the specified position (use warp_mouse() instead) and sending Alt/Cmd + Tab as InputEventKey won't toggle between active windows.

void remove_joy_mapping(guid: String) 🔗

Removes all mappings from the internal database that match the given GUID. All currently connected joypads that use this GUID will become unmapped.

On Android, Godot will map to an internal fallback mapping.

void set_accelerometer(value: Vector3) 🔗

Sets the acceleration value of the accelerometer sensor. Can be used for debugging on devices without a hardware sensor, for example in an editor on a PC.

Note: This value can be immediately overwritten by the hardware sensor value on Android and iOS.

void set_custom_mouse_cursor(image: Resource, shape: CursorShape = 0, hotspot: Vector2 = Vector2(0, 0)) 🔗

Sets a custom mouse cursor image, which is only visible inside the game window, for the given mouse shape. The hotspot can also be specified. Passing null to the image parameter resets to the system cursor.

image can be either Texture2D or Image and its size must be lower than or equal to 256×256. To avoid rendering issues, sizes lower than or equal to 128×128 are recommended.

hotspot must be within image's size.

Note: AnimatedTextures aren't supported as custom mouse cursors. If using an AnimatedTexture, only the first frame will be displayed.

Note: The Lossless, Lossy or Uncompressed compression modes are recommended. The Video RAM compression mode can be used, but it will be decompressed on the CPU, which means loading times are slowed down and no memory is saved compared to lossless modes.

Note: On the web platform, the maximum allowed cursor image size is 128×128. Cursor images larger than 32×32 will also only be displayed if the mouse cursor image is entirely located within the page for security reasons.

void set_default_cursor_shape(shape: CursorShape = 0) 🔗

Sets the default cursor shape to be used in the viewport instead of CURSOR_ARROW.

Note: If you want to change the default cursor shape for Control's nodes, use Control.mouse_default_cursor_shape instead.

Note: This method generates an InputEventMouseMotion to update cursor immediately.

void set_gravity(value: Vector3) 🔗

Sets the gravity value of the accelerometer sensor. Can be used for debugging on devices without a hardware sensor, for example in an editor on a PC.

Note: This value can be immediately overwritten by the hardware sensor value on Android and iOS.

void set_gyroscope(value: Vector3) 🔗

Sets the value of the rotation rate of the gyroscope sensor. Can be used for debugging on devices without a hardware sensor, for example in an editor on a PC.

Note: This value can be immediately overwritten by the hardware sensor value on Android and iOS.

void set_magnetometer(value: Vector3) 🔗

Sets the value of the magnetic field of the magnetometer sensor. Can be used for debugging on devices without a hardware sensor, for example in an editor on a PC.

Note: This value can be immediately overwritten by the hardware sensor value on Android and iOS.

bool should_ignore_device(vendor_id: int, product_id: int) const 🔗

Queries whether an input device should be ignored or not. Devices can be ignored by setting the environment variable SDL_GAMECONTROLLER_IGNORE_DEVICES. Read the SDL documentation for more information.

Note: Some 3rd party tools can contribute to the list of ignored devices. For example, SteamInput creates virtual devices from physical devices for remapping purposes. To avoid handling the same input device twice, the original device is added to the ignore list.

void start_joy_vibration(device: int, weak_magnitude: float, strong_magnitude: float, duration: float = 0) 🔗

Starts to vibrate the joypad. Joypads usually come with two rumble motors, a strong and a weak one. weak_magnitude is the strength of the weak motor (between 0 and 1) and strong_magnitude is the strength of the strong motor (between 0 and 1). duration is the duration of the effect in seconds (a duration of 0 will try to play the vibration indefinitely). The vibration can be stopped early by calling stop_joy_vibration().

Note: Not every hardware is compatible with long effect durations; it is recommended to restart an effect if it has to be played for more than a few seconds.

Note: For macOS, vibration is only supported in macOS 11 and later.

void stop_joy_vibration(device: int) 🔗

Stops the vibration of the joypad started with start_joy_vibration().

void vibrate_handheld(duration_ms: int = 500, amplitude: float = -1.0) 🔗

Vibrate the handheld device for the specified duration in milliseconds.

amplitude is the strength of the vibration, as a value between 0.0 and 1.0. If set to -1.0, the default vibration strength of the device is used.

Note: This method is implemented on Android, iOS, and Web. It has no effect on other platforms.

Note: For Android, vibrate_handheld() requires enabling the VIBRATE permission in the export preset. Otherwise, vibrate_handheld() will have no effect.

Note: For iOS, specifying the duration is only supported in iOS 13 and later.

Note: For Web, the amplitude cannot be changed.

Note: Some web browsers such as Safari and Firefox for Android do not support vibrate_handheld().

void warp_mouse(position: Vector2) 🔗

Sets the mouse position to the specified vector, provided in pixels and relative to an origin at the upper left corner of the currently focused Window Manager game window.

Mouse position is clipped to the limits of the screen resolution, or to the limits of the game window if MouseMode is set to MOUSE_MODE_CONFINED or MOUSE_MODE_CONFINED_HIDDEN.

Note: warp_mouse() is only supported on Windows, macOS and Linux. It has no effect on Android, iOS and Web.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var cancel_event = InputEventAction.new()
cancel_event.action = "ui_cancel"
cancel_event.pressed = true
Input.parse_input_event(cancel_event)
```

Example 2 (gdscript):
```gdscript
var cancelEvent = new InputEventAction();
cancelEvent.Action = "ui_cancel";
cancelEvent.Pressed = true;
Input.ParseInputEvent(cancelEvent);
```

---

## ItemList

**URL:** https://docs.godotengine.org/en/stable/classes/class_itemlist.html

**Contents:**
- ItemList
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions

Inherits: Control < CanvasItem < Node < Object

A vertical list of selectable items with one or multiple columns.

This control provides a vertical list of selectable items that may be in a single or in multiple columns, with each item having options for text and an icon. Tooltips are supported and may be different for every item in the list.

Selectable items in the list may be selected or deselected and multiple selection may be enabled. Selection with right mouse button may also be enabled to allow use of popup context menus. Items may also be "activated" by double-clicking them or by pressing Enter.

Item text only supports single-line strings. Newline characters (e.g. \n) in the string won't produce a newline. Text wrapping is enabled in ICON_MODE_TOP mode, but the column's width is adjusted to fully fit its content by default. You need to set fixed_column_width greater than zero to wrap the text.

All set_* methods allow negative item indices, i.e. -1 to access the last item, -2 to select the second-to-last item, and so on.

Incremental search: Like PopupMenu and Tree, ItemList supports searching within the list while the control is focused. Press a key that matches the first letter of an item's name to select the first item starting with the given letter. After that point, there are two ways to perform incremental search: 1) Press the same key again before the timeout duration to select the next item starting with the same letter. 2) Press letter keys that match the rest of the word before the timeout duration to match to select the item in question directly. Both of these actions will be reset to the beginning of the list if the timeout duration has passed since the last keystroke was registered. You can adjust the timeout duration by changing ProjectSettings.gui/timers/incremental_search_max_interval_msec.

true (overrides Control)

2 (overrides Control)

text_overrun_behavior

add_icon_item(icon: Texture2D, selectable: bool = true)

add_item(text: String, icon: Texture2D = null, selectable: bool = true)

ensure_current_is_visible()

force_update_list_size()

get_item_at_position(position: Vector2, exact: bool = false) const

get_item_auto_translate_mode(idx: int) const

get_item_custom_bg_color(idx: int) const

get_item_custom_fg_color(idx: int) const

get_item_icon(idx: int) const

get_item_icon_modulate(idx: int) const

get_item_icon_region(idx: int) const

get_item_language(idx: int) const

get_item_metadata(idx: int) const

get_item_rect(idx: int, expand: bool = true) const

get_item_text(idx: int) const

get_item_text_direction(idx: int) const

get_item_tooltip(idx: int) const

is_anything_selected()

is_item_disabled(idx: int) const

is_item_icon_transposed(idx: int) const

is_item_selectable(idx: int) const

is_item_tooltip_enabled(idx: int) const

is_selected(idx: int) const

move_item(from_idx: int, to_idx: int)

remove_item(idx: int)

select(idx: int, single: bool = true)

set_item_auto_translate_mode(idx: int, mode: AutoTranslateMode)

set_item_custom_bg_color(idx: int, custom_bg_color: Color)

set_item_custom_fg_color(idx: int, custom_fg_color: Color)

set_item_disabled(idx: int, disabled: bool)

set_item_icon(idx: int, icon: Texture2D)

set_item_icon_modulate(idx: int, modulate: Color)

set_item_icon_region(idx: int, rect: Rect2)

set_item_icon_transposed(idx: int, transposed: bool)

set_item_language(idx: int, language: String)

set_item_metadata(idx: int, metadata: Variant)

set_item_selectable(idx: int, selectable: bool)

set_item_text(idx: int, text: String)

set_item_text_direction(idx: int, direction: TextDirection)

set_item_tooltip(idx: int, tooltip: String)

set_item_tooltip_enabled(idx: int, enable: bool)

Color(0.65, 0.65, 0.65, 1)

Color(0.95, 0.95, 0.95, 1)

font_hovered_selected_color

Color(0.7, 0.7, 0.7, 0.25)

hovered_selected_focus

empty_clicked(at_position: Vector2, mouse_button_index: int) 🔗

Emitted when any mouse click is issued within the rect of the list but on empty space.

at_position is the click position in this control's local coordinate system.

item_activated(index: int) 🔗

Emitted when specified list item is activated via double-clicking or by pressing Enter.

item_clicked(index: int, at_position: Vector2, mouse_button_index: int) 🔗

Emitted when specified list item has been clicked with any mouse button.

at_position is the click position in this control's local coordinate system.

item_selected(index: int) 🔗

Emitted when specified item has been selected. Only applicable in single selection mode.

allow_reselect must be enabled to reselect an item.

multi_selected(index: int, selected: bool) 🔗

Emitted when a multiple selection is altered on a list allowing multiple selection.

IconMode ICON_MODE_TOP = 0

Icon is drawn above the text.

IconMode ICON_MODE_LEFT = 1

Icon is drawn to the left of the text.

SelectMode SELECT_SINGLE = 0

Only allow selecting a single item.

SelectMode SELECT_MULTI = 1

Allows selecting multiple items by holding Ctrl or Shift.

SelectMode SELECT_TOGGLE = 2

Allows selecting multiple items by toggling them on and off.

bool allow_reselect = false 🔗

void set_allow_reselect(value: bool)

bool get_allow_reselect()

If true, the currently selected item can be selected again.

bool allow_rmb_select = false 🔗

void set_allow_rmb_select(value: bool)

bool get_allow_rmb_select()

If true, right mouse button click can select items.

bool allow_search = true 🔗

void set_allow_search(value: bool)

bool get_allow_search()

If true, allows navigating the ItemList with letter keys through incremental search.

bool auto_height = false 🔗

void set_auto_height(value: bool)

bool has_auto_height()

If true, the control will automatically resize the height to fit its content.

bool auto_width = false 🔗

void set_auto_width(value: bool)

bool has_auto_width()

If true, the control will automatically resize the width to fit its content.

int fixed_column_width = 0 🔗

void set_fixed_column_width(value: int)

int get_fixed_column_width()

The width all columns will be adjusted to.

A value of zero disables the adjustment, each item will have a width equal to the width of its content and the columns will have an uneven width.

Vector2i fixed_icon_size = Vector2i(0, 0) 🔗

void set_fixed_icon_size(value: Vector2i)

Vector2i get_fixed_icon_size()

The size all icons will be adjusted to.

If either X or Y component is not greater than zero, icon size won't be affected.

IconMode icon_mode = 1 🔗

void set_icon_mode(value: IconMode)

IconMode get_icon_mode()

The icon position, whether above or to the left of the text. See the IconMode constants.

float icon_scale = 1.0 🔗

void set_icon_scale(value: float)

float get_icon_scale()

The scale of icon applied after fixed_icon_size and transposing takes effect.

void set_item_count(value: int)

The number of items currently in the list.

int max_columns = 1 🔗

void set_max_columns(value: int)

int get_max_columns()

Maximum columns the list will have.

If greater than zero, the content will be split among the specified columns.

A value of zero means unlimited columns, i.e. all items will be put in the same row.

int max_text_lines = 1 🔗

void set_max_text_lines(value: int)

int get_max_text_lines()

Maximum lines of text allowed in each item. Space will be reserved even when there is not enough lines of text to display.

Note: This property takes effect only when icon_mode is ICON_MODE_TOP. To make the text wrap, fixed_column_width should be greater than zero.

bool same_column_width = false 🔗

void set_same_column_width(value: bool)

bool is_same_column_width()

Whether all columns will have the same width.

If true, the width is equal to the largest column width of all columns.

SelectMode select_mode = 0 🔗

void set_select_mode(value: SelectMode)

SelectMode get_select_mode()

Allows single or multiple item selection. See the SelectMode constants.

OverrunBehavior text_overrun_behavior = 3 🔗

void set_text_overrun_behavior(value: OverrunBehavior)

OverrunBehavior get_text_overrun_behavior()

The clipping behavior when the text exceeds an item's bounding rectangle.

bool wraparound_items = true 🔗

void set_wraparound_items(value: bool)

bool has_wraparound_items()

If true, the control will automatically move items into a new row to fit its content. See also HFlowContainer for this behavior.

If false, the control will add a horizontal scrollbar to make all items visible.

int add_icon_item(icon: Texture2D, selectable: bool = true) 🔗

Adds an item to the item list with no text, only an icon. Returns the index of an added item.

int add_item(text: String, icon: Texture2D = null, selectable: bool = true) 🔗

Adds an item to the item list with specified text. Returns the index of an added item.

Specify an icon, or use null as the icon for a list item with no icon.

If selectable is true, the list item will be selectable.

Removes all items from the list.

void deselect(idx: int) 🔗

Ensures the item associated with the specified index is not selected.

void deselect_all() 🔗

Ensures there are no items selected.

void ensure_current_is_visible() 🔗

Ensure current selection is visible, adjusting the scroll position as necessary.

void force_update_list_size() 🔗

Forces an update to the list size based on its items. This happens automatically whenever size of the items, or other relevant settings like auto_height, change. The method can be used to trigger the update ahead of next drawing pass.

HScrollBar get_h_scroll_bar() 🔗

Returns the horizontal scrollbar.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their CanvasItem.visible property.

int get_item_at_position(position: Vector2, exact: bool = false) const 🔗

Returns the item index at the given position.

When there is no item at that point, -1 will be returned if exact is true, and the closest item index will be returned otherwise.

Note: The returned value is unreliable if called right after modifying the ItemList, before it redraws in the next frame.

AutoTranslateMode get_item_auto_translate_mode(idx: int) const 🔗

Returns item's auto translate mode.

Color get_item_custom_bg_color(idx: int) const 🔗

Returns the custom background color of the item specified by idx index.

Color get_item_custom_fg_color(idx: int) const 🔗

Returns the custom foreground color of the item specified by idx index.

Texture2D get_item_icon(idx: int) const 🔗

Returns the icon associated with the specified index.

Color get_item_icon_modulate(idx: int) const 🔗

Returns a Color modulating item's icon at the specified index.

Rect2 get_item_icon_region(idx: int) const 🔗

Returns the region of item's icon used. The whole icon will be used if the region has no area.

String get_item_language(idx: int) const 🔗

Returns item's text language code.

Variant get_item_metadata(idx: int) const 🔗

Returns the metadata value of the specified index.

Rect2 get_item_rect(idx: int, expand: bool = true) const 🔗

Returns the position and size of the item with the specified index, in the coordinate system of the ItemList node. If expand is true the last column expands to fill the rest of the row.

Note: The returned value is unreliable if called right after modifying the ItemList, before it redraws in the next frame.

String get_item_text(idx: int) const 🔗

Returns the text associated with the specified index.

TextDirection get_item_text_direction(idx: int) const 🔗

Returns item's text base writing direction.

String get_item_tooltip(idx: int) const 🔗

Returns the tooltip hint associated with the specified index.

PackedInt32Array get_selected_items() 🔗

Returns an array with the indexes of the selected items.

VScrollBar get_v_scroll_bar() 🔗

Returns the vertical scrollbar.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their CanvasItem.visible property.

bool is_anything_selected() 🔗

Returns true if one or more items are selected.

bool is_item_disabled(idx: int) const 🔗

Returns true if the item at the specified index is disabled.

bool is_item_icon_transposed(idx: int) const 🔗

Returns true if the item icon will be drawn transposed, i.e. the X and Y axes are swapped.

bool is_item_selectable(idx: int) const 🔗

Returns true if the item at the specified index is selectable.

bool is_item_tooltip_enabled(idx: int) const 🔗

Returns true if the tooltip is enabled for specified item index.

bool is_selected(idx: int) const 🔗

Returns true if the item at the specified index is currently selected.

void move_item(from_idx: int, to_idx: int) 🔗

Moves item from index from_idx to to_idx.

void remove_item(idx: int) 🔗

Removes the item specified by idx index from the list.

void select(idx: int, single: bool = true) 🔗

Select the item at the specified index.

Note: This method does not trigger the item selection signal.

void set_item_auto_translate_mode(idx: int, mode: AutoTranslateMode) 🔗

Sets the auto translate mode of the item associated with the specified index.

Items use Node.AUTO_TRANSLATE_MODE_INHERIT by default, which uses the same auto translate mode as the ItemList itself.

void set_item_custom_bg_color(idx: int, custom_bg_color: Color) 🔗

Sets the background color of the item specified by idx index to the specified Color.

void set_item_custom_fg_color(idx: int, custom_fg_color: Color) 🔗

Sets the foreground color of the item specified by idx index to the specified Color.

void set_item_disabled(idx: int, disabled: bool) 🔗

Disables (or enables) the item at the specified index.

Disabled items cannot be selected and do not trigger activation signals (when double-clicking or pressing Enter).

void set_item_icon(idx: int, icon: Texture2D) 🔗

Sets (or replaces) the icon's Texture2D associated with the specified index.

void set_item_icon_modulate(idx: int, modulate: Color) 🔗

Sets a modulating Color of the item associated with the specified index.

void set_item_icon_region(idx: int, rect: Rect2) 🔗

Sets the region of item's icon used. The whole icon will be used if the region has no area.

void set_item_icon_transposed(idx: int, transposed: bool) 🔗

Sets whether the item icon will be drawn transposed.

void set_item_language(idx: int, language: String) 🔗

Sets language code of item's text used for line-breaking and text shaping algorithms, if left empty current locale is used instead.

void set_item_metadata(idx: int, metadata: Variant) 🔗

Sets a value (of any type) to be stored with the item associated with the specified index.

void set_item_selectable(idx: int, selectable: bool) 🔗

Allows or disallows selection of the item associated with the specified index.

void set_item_text(idx: int, text: String) 🔗

Sets text of the item associated with the specified index.

void set_item_text_direction(idx: int, direction: TextDirection) 🔗

Sets item's text base writing direction.

void set_item_tooltip(idx: int, tooltip: String) 🔗

Sets the tooltip hint for the item associated with the specified index.

void set_item_tooltip_enabled(idx: int, enable: bool) 🔗

Sets whether the tooltip hint is enabled for specified item index.

void sort_items_by_text() 🔗

Sorts items in the list by their text.

Color font_color = Color(0.65, 0.65, 0.65, 1) 🔗

Default text Color of the item.

Color font_hovered_color = Color(0.95, 0.95, 0.95, 1) 🔗

Text Color used when the item is hovered and not selected yet.

Color font_hovered_selected_color = Color(1, 1, 1, 1) 🔗

Text Color used when the item is hovered and selected.

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The tint of text outline of the item.

Color font_selected_color = Color(1, 1, 1, 1) 🔗

Text Color used when the item is selected, but not hovered.

Color guide_color = Color(0.7, 0.7, 0.7, 0.25) 🔗

Color of the guideline. The guideline is a line drawn between each row of items.

int h_separation = 4 🔗

The horizontal spacing between items.

int icon_margin = 4 🔗

The spacing between item's icon and text.

int line_separation = 2 🔗

The vertical spacing between each line of text.

int outline_size = 0 🔗

The size of the item text outline.

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

int v_separation = 4 🔗

The vertical spacing between items.

Font of the item's text.

Font size of the item's text.

StyleBox used for the cursor, when the ItemList is being focused.

StyleBox cursor_unfocused 🔗

StyleBox used for the cursor, when the ItemList is not being focused.

The focused style for the ItemList, drawn on top of the background, but below everything else.

StyleBox for the hovered, but not selected items.

StyleBox hovered_selected 🔗

StyleBox for the hovered and selected items, used when the ItemList is not being focused.

StyleBox hovered_selected_focus 🔗

StyleBox for the hovered and selected items, used when the ItemList is being focused.

The background style for the ItemList.

StyleBox for the selected items, used when the ItemList is not being focused.

StyleBox selected_focus 🔗

StyleBox for the selected items, used when the ItemList is being focused.

Please read the User-contributed notes policy before submitting a comment.

---

## Keyboard/Controller Navigation and Focus

**URL:** https://docs.godotengine.org/en/stable/tutorials/ui/gui_navigation.html

**Contents:**
- Keyboard/Controller Navigation and Focus
- Node settings
- Necessary code
- User-contributed notes

It is a common requirement for a user interface to have full keyboard and controller support for navigation and interaction. There are two main reasons why this is beneficial for projects: improved accessibility (not everyone can use mouse or touch controls for interactions), and getting your project ready for consoles (or just for people who prefer to game with a controller on PC).

Navigating between UI elements with keyboard or controller is done by changing which node is actively selected. This is also called changing UI focus. Every Control node in Godot is capable of having focus. By default, some control nodes have the ability to automatically grab focus reacting to built-in UI actions such as ui_up, ui_down, ui_focus_next, etc. These actions can be seen in the project settings in the input map and can be modified.

Because these actions are used for focus they should not be used for any gameplay code.

In addition to the built-in logic, you can define what is known as focus neighbors for each individual control node. This allows to finely tune the path the UI focus takes across the user interface of your project. The settings for individual nodes can be found in the Inspector dock, under the "Focus" category of the "Control" section.

Neighbor options are used to define nodes for 4-directional navigation, such as using arrow keys or a D-pad on a controller. For example, the bottom neighbor will be used when navigating down with the down arrow or by pushing down on the D-pad. The "Next" and "Previous" options are used with the focus shift button, such as Tab on desktop operating systems.

A node can lose focus if it becomes hidden.

The mode setting defines how a node can be focused. All means a node can be focused by clicking on it with the mouse, or selecting it with a keyboard or controller. Click means it can only be focused on by clicking on it. Finally, None means it can't be focused at all. Different control nodes have different default settings for this based on how they are typically used, for example, Label nodes are set to "None" by default, while buttons are set to "All".

Make sure to properly configure your scenes for focus and navigation. If a node has no focus neighbor configured, the engine will try to guess the next control automatically. This may result in unintended behavior, especially in a complex user interface that doesn't have well-defined vertical or horizontal navigation flow.

For keyboard and controller navigation to work correctly, any node must be focused by using code when the scene starts. Without doing this, pressing buttons or keys won't do anything.

You can use the Control.grab_focus() method to focus a control. Here is a basic example of setting initial focus with code:

Now when the scene starts, the "Start Button" node will be focused, and the keyboard or a controller can be used to navigate between it and other UI elements.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    $StartButton.grab_focus.call_deferred()
```

Example 2 (gdscript):
```gdscript
public override void _Ready()
{
    GetNode<Button>("StartButton").GrabFocus.CallDeferred();
}
```

---

## LabelSettings

**URL:** https://docs.godotengine.org/en/stable/classes/class_labelsettings.html

**Contents:**
- LabelSettings
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Provides common settings to customize the text in a Label.

LabelSettings is a resource that provides common settings to customize the text in a Label. It will take priority over the properties defined in Control.theme. The resource can be shared between multiple labels and changed on the fly, so it's convenient and flexible way to setup text style.

stacked_outline_count

add_stacked_outline(index: int = -1)

add_stacked_shadow(index: int = -1)

get_stacked_outline_color(index: int) const

get_stacked_outline_size(index: int) const

get_stacked_shadow_color(index: int) const

get_stacked_shadow_offset(index: int) const

get_stacked_shadow_outline_size(index: int) const

move_stacked_outline(from_index: int, to_position: int)

move_stacked_shadow(from_index: int, to_position: int)

remove_stacked_outline(index: int)

remove_stacked_shadow(index: int)

set_stacked_outline_color(index: int, color: Color)

set_stacked_outline_size(index: int, size: int)

set_stacked_shadow_color(index: int, color: Color)

set_stacked_shadow_offset(index: int, offset: Vector2)

set_stacked_shadow_outline_size(index: int, size: int)

void set_font(value: Font)

Font used for the text.

Color font_color = Color(1, 1, 1, 1) 🔗

void set_font_color(value: Color)

Color get_font_color()

void set_font_size(value: int)

float line_spacing = 3.0 🔗

void set_line_spacing(value: float)

float get_line_spacing()

Additional vertical spacing between lines (in pixels), spacing is added to line descent. This value can be negative.

Color outline_color = Color(1, 1, 1, 1) 🔗

void set_outline_color(value: Color)

Color get_outline_color()

The color of the outline.

int outline_size = 0 🔗

void set_outline_size(value: int)

int get_outline_size()

float paragraph_spacing = 0.0 🔗

void set_paragraph_spacing(value: float)

float get_paragraph_spacing()

Vertical space between paragraphs. Added on top of line_spacing.

Color shadow_color = Color(0, 0, 0, 0) 🔗

void set_shadow_color(value: Color)

Color get_shadow_color()

Color of the shadow effect. If alpha is 0, no shadow will be drawn.

Vector2 shadow_offset = Vector2(1, 1) 🔗

void set_shadow_offset(value: Vector2)

Vector2 get_shadow_offset()

Offset of the shadow effect, in pixels.

int shadow_size = 1 🔗

void set_shadow_size(value: int)

int get_shadow_size()

Size of the shadow effect.

int stacked_outline_count = 0 🔗

void set_stacked_outline_count(value: int)

int get_stacked_outline_count()

The number of stacked outlines.

int stacked_shadow_count = 0 🔗

void set_stacked_shadow_count(value: int)

int get_stacked_shadow_count()

The number of stacked shadows.

void add_stacked_outline(index: int = -1) 🔗

Adds a new stacked outline to the label at the given index. If index is -1, the new stacked outline will be added at the end of the list.

void add_stacked_shadow(index: int = -1) 🔗

Adds a new stacked shadow to the label at the given index. If index is -1, the new stacked shadow will be added at the end of the list.

Color get_stacked_outline_color(index: int) const 🔗

Returns the color of the stacked outline at index.

int get_stacked_outline_size(index: int) const 🔗

Returns the size of the stacked outline at index.

Color get_stacked_shadow_color(index: int) const 🔗

Returns the color of the stacked shadow at index.

Vector2 get_stacked_shadow_offset(index: int) const 🔗

Returns the offset of the stacked shadow at index.

int get_stacked_shadow_outline_size(index: int) const 🔗

Returns the outline size of the stacked shadow at index.

void move_stacked_outline(from_index: int, to_position: int) 🔗

Moves the stacked outline at index from_index to the given position to_position in the array.

void move_stacked_shadow(from_index: int, to_position: int) 🔗

Moves the stacked shadow at index from_index to the given position to_position in the array.

void remove_stacked_outline(index: int) 🔗

Removes the stacked outline at index index.

void remove_stacked_shadow(index: int) 🔗

Removes the stacked shadow at index index.

void set_stacked_outline_color(index: int, color: Color) 🔗

Sets the color of the stacked outline identified by the given index to color.

void set_stacked_outline_size(index: int, size: int) 🔗

Sets the size of the stacked outline identified by the given index to size.

void set_stacked_shadow_color(index: int, color: Color) 🔗

Sets the color of the stacked shadow identified by the given index to color.

void set_stacked_shadow_offset(index: int, offset: Vector2) 🔗

Sets the offset of the stacked shadow identified by the given index to offset.

void set_stacked_shadow_outline_size(index: int, size: int) 🔗

Sets the outline size of the stacked shadow identified by the given index to size.

Please read the User-contributed notes policy before submitting a comment.

---

## Label

**URL:** https://docs.godotengine.org/en/stable/classes/class_label.html

**Contents:**
- Label
- Description
- Tutorials
- Properties
- Methods
- Theme Properties
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions
- User-contributed notes

Inherits: Control < CanvasItem < Node < Object

A control for displaying plain text.

A control for displaying plain text. It gives you control over the horizontal and vertical alignment and can wrap the text inside the node's bounding rectangle. It doesn't support bold, italics, or other rich text formatting. For that, use RichTextLabel instead.

2D Dodge The Creeps Demo

BitField[LineBreakFlag]

BitField[JustificationFlag]

2 (overrides Control)

4 (overrides Control)

structured_text_bidi_override

structured_text_bidi_override_options

text_overrun_behavior

VisibleCharactersBehavior

visible_characters_behavior

get_character_bounds(pos: int) const

get_line_count() const

get_line_height(line: int = -1) const

get_total_character_count() const

get_visible_line_count() const

AutowrapMode autowrap_mode = 0 🔗

void set_autowrap_mode(value: AutowrapMode)

AutowrapMode get_autowrap_mode()

If set to something other than TextServer.AUTOWRAP_OFF, the text gets wrapped inside the node's bounding rectangle. If you resize the node, it will change its height automatically to show all the text.

BitField[LineBreakFlag] autowrap_trim_flags = 192 🔗

void set_autowrap_trim_flags(value: BitField[LineBreakFlag])

BitField[LineBreakFlag] get_autowrap_trim_flags()

Autowrap space trimming flags. See TextServer.BREAK_TRIM_START_EDGE_SPACES and TextServer.BREAK_TRIM_END_EDGE_SPACES for more info.

bool clip_text = false 🔗

void set_clip_text(value: bool)

bool is_clipping_text()

If true, the Label only shows the text that fits inside its bounding rectangle and will clip text horizontally.

String ellipsis_char = "…" 🔗

void set_ellipsis_char(value: String)

String get_ellipsis_char()

Ellipsis character used for text clipping.

HorizontalAlignment horizontal_alignment = 0 🔗

void set_horizontal_alignment(value: HorizontalAlignment)

HorizontalAlignment get_horizontal_alignment()

Controls the text's horizontal alignment. Supports left, center, right, and fill (also known as justify).

BitField[JustificationFlag] justification_flags = 163 🔗

void set_justification_flags(value: BitField[JustificationFlag])

BitField[JustificationFlag] get_justification_flags()

Line fill alignment rules.

LabelSettings label_settings 🔗

void set_label_settings(value: LabelSettings)

LabelSettings get_label_settings()

A LabelSettings resource that can be shared between multiple Label nodes. Takes priority over theme properties.

String language = "" 🔗

void set_language(value: String)

String get_language()

Language code used for line-breaking and text shaping algorithms, if left empty current locale is used instead.

int lines_skipped = 0 🔗

void set_lines_skipped(value: int)

int get_lines_skipped()

The number of the lines ignored and not displayed from the start of the text value.

int max_lines_visible = -1 🔗

void set_max_lines_visible(value: int)

int get_max_lines_visible()

Limits the lines of text the node shows on screen.

String paragraph_separator = "\\n" 🔗

void set_paragraph_separator(value: String)

String get_paragraph_separator()

String used as a paragraph separator. Each paragraph is processed independently, in its own BiDi context.

StructuredTextParser structured_text_bidi_override = 0 🔗

void set_structured_text_bidi_override(value: StructuredTextParser)

StructuredTextParser get_structured_text_bidi_override()

Set BiDi algorithm override for the structured text.

Array structured_text_bidi_override_options = [] 🔗

void set_structured_text_bidi_override_options(value: Array)

Array get_structured_text_bidi_override_options()

Set additional options for BiDi override.

PackedFloat32Array tab_stops = PackedFloat32Array() 🔗

void set_tab_stops(value: PackedFloat32Array)

PackedFloat32Array get_tab_stops()

Aligns text to the given tab-stops.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedFloat32Array for more details.

void set_text(value: String)

The text to display on screen.

TextDirection text_direction = 0 🔗

void set_text_direction(value: TextDirection)

TextDirection get_text_direction()

Base text writing direction.

OverrunBehavior text_overrun_behavior = 0 🔗

void set_text_overrun_behavior(value: OverrunBehavior)

OverrunBehavior get_text_overrun_behavior()

The clipping behavior when the text exceeds the node's bounding rectangle.

bool uppercase = false 🔗

void set_uppercase(value: bool)

If true, all the text displays as UPPERCASE.

VerticalAlignment vertical_alignment = 0 🔗

void set_vertical_alignment(value: VerticalAlignment)

VerticalAlignment get_vertical_alignment()

Controls the text's vertical alignment. Supports top, center, bottom, and fill.

int visible_characters = -1 🔗

void set_visible_characters(value: int)

int get_visible_characters()

The number of characters to display. If set to -1, all characters are displayed. This can be useful when animating the text appearing in a dialog box.

Note: Setting this property updates visible_ratio accordingly.

Note: Characters are counted as Unicode codepoints. A single visible grapheme may contain multiple codepoints (e.g. certain emoji use three codepoints). A single codepoint may contain two UTF-16 characters, which are used in C# strings.

VisibleCharactersBehavior visible_characters_behavior = 0 🔗

void set_visible_characters_behavior(value: VisibleCharactersBehavior)

VisibleCharactersBehavior get_visible_characters_behavior()

The clipping behavior when visible_characters or visible_ratio is set.

float visible_ratio = 1.0 🔗

void set_visible_ratio(value: float)

float get_visible_ratio()

The fraction of characters to display, relative to the total number of characters (see get_total_character_count()). If set to 1.0, all characters are displayed. If set to 0.5, only half of the characters will be displayed. This can be useful when animating the text appearing in a dialog box.

Note: Setting this property updates visible_characters accordingly.

Rect2 get_character_bounds(pos: int) const 🔗

Returns the bounding rectangle of the character at position pos in the label's local coordinate system. If the character is a non-visual character or pos is outside the valid range, an empty Rect2 is returned. If the character is a part of a composite grapheme, the bounding rectangle of the whole grapheme is returned.

int get_line_count() const 🔗

Returns the number of lines of text the Label has.

int get_line_height(line: int = -1) const 🔗

Returns the height of the line line.

If line is set to -1, returns the biggest line height.

If there are no lines, returns font size in pixels.

int get_total_character_count() const 🔗

Returns the total number of printable characters in the text (excluding spaces and newlines).

int get_visible_line_count() const 🔗

Returns the number of lines shown. Useful if the Label's height cannot currently display all lines.

Color font_color = Color(1, 1, 1, 1) 🔗

Default text Color of the Label.

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The color of text outline.

Color font_shadow_color = Color(0, 0, 0, 0) 🔗

Color of the text's shadow effect.

int line_spacing = 3 🔗

Additional vertical spacing between lines (in pixels), spacing is added to line descent. This value can be negative.

int outline_size = 0 🔗

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

Note: Using a value that is larger than half the font size is not recommended, as the font outline may fail to be fully closed in this case.

int paragraph_spacing = 0 🔗

Vertical space between paragraphs. Added on top of line_spacing.

int shadow_offset_x = 1 🔗

The horizontal offset of the text's shadow.

int shadow_offset_y = 1 🔗

The vertical offset of the text's shadow.

int shadow_outline_size = 1 🔗

The size of the shadow outline.

Font used for the Label's text.

Font size of the Label's text.

StyleBox used when the Label is focused (when used with assistive apps).

Background StyleBox for the Label.

Please read the User-contributed notes policy before submitting a comment.

---

## LineEdit

**URL:** https://docs.godotengine.org/en/stable/classes/class_lineedit.html

**Contents:**
- LineEdit
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions

Inherits: Control < CanvasItem < Node < Object

An input field for single-line text.

LineEdit provides an input field for editing a single line of text.

When the LineEdit control is focused using the keyboard arrow keys, it will only gain focus and not enter edit mode.

To enter edit mode, click on the control with the mouse, see also keep_editing_on_text_submit.

To exit edit mode, press ui_text_submit or ui_cancel (by default Escape) actions.

Check edit(), unedit(), is_editing(), and editing_toggled for more information.

While entering text, it is possible to insert special characters using Unicode, OEM or Windows alt codes:

To enter Unicode codepoints, hold Alt and type the codepoint on the numpad. For example, to enter the character á (U+00E1), hold Alt and type +E1 on the numpad (the leading zeroes can be omitted).

To enter OEM codepoints, hold Alt and type the code on the numpad. For example, to enter the character á (OEM 160), hold Alt and type 160 on the numpad.

To enter Windows codepoints, hold Alt and type the code on the numpad. For example, to enter the character á (Windows 0225), hold Alt and type 0, 2, 2, 5 on the numpad. The leading zero here must not be omitted, as this is how Windows codepoints are distinguished from OEM codepoints.

Focusing the LineEdit with ui_focus_next (by default Tab) or ui_focus_prev (by default Shift + Tab) or Control.grab_focus() still enters edit mode (for compatibility).

LineEdit features many built-in shortcuts that are always available (Ctrl here maps to Cmd on macOS):

Ctrl + V or Ctrl + Y: Paste/"yank"

Ctrl + ~: Swap input direction.

Ctrl + Shift + Z: Redo

Ctrl + U: Delete text from the caret position to the beginning of the line

Ctrl + K: Delete text from the caret position to the end of the line

Ctrl + A: Select all text

Up Arrow/Down Arrow: Move the caret to the beginning/end of the line

On macOS, some extra keyboard shortcuts are available:

Cmd + F: Same as Right Arrow, move the caret one character right

Cmd + B: Same as Left Arrow, move the caret one character left

Cmd + P: Same as Up Arrow, move the caret to the previous line

Cmd + N: Same as Down Arrow, move the caret to the next line

Cmd + D: Same as Delete, delete the character on the right side of caret

Cmd + H: Same as Backspace, delete the character on the left side of the caret

Cmd + A: Same as Home, move the caret to the beginning of the line

Cmd + E: Same as End, move the caret to the end of the line

Cmd + Left Arrow: Same as Home, move the caret to the beginning of the line

Cmd + Right Arrow: Same as End, move the caret to the end of the line

Note: Caret movement shortcuts listed above are not affected by shortcut_keys_enabled.

backspace_deletes_composite_character_enabled

caret_force_displayed

deselect_on_focus_loss_enabled

drag_and_drop_selection_enabled

expand_to_text_length

2 (overrides Control)

keep_editing_on_text_submit

middle_mouse_paste_enabled

mouse_default_cursor_shape

1 (overrides Control)

shortcut_keys_enabled

structured_text_bidi_override

structured_text_bidi_override_options

virtual_keyboard_enabled

virtual_keyboard_show_on_focus

virtual_keyboard_type

delete_char_at_caret()

delete_text(from_column: int, to_column: int)

get_next_composite_character_column(column: int) const

get_previous_composite_character_column(column: int) const

get_scroll_offset() const

get_selection_from_column() const

get_selection_to_column() const

has_selection() const

insert_text_at_caret(text: String)

is_menu_visible() const

menu_option(option: int)

select(from: int = 0, to: int = -1)

Color(0.95, 0.95, 0.95, 1)

Color(0.875, 0.875, 0.875, 1)

clear_button_color_pressed

Color(0.875, 0.875, 0.875, 1)

font_placeholder_color

Color(0.875, 0.875, 0.875, 0.6)

font_uneditable_color

Color(0.875, 0.875, 0.875, 0.5)

Color(0.5, 0.5, 0.5, 1)

minimum_character_width

editing_toggled(toggled_on: bool) 🔗

Emitted when the LineEdit switches in or out of edit mode.

text_change_rejected(rejected_substring: String) 🔗

Emitted when appending text that overflows the max_length. The appended text is truncated to fit max_length, and the part that couldn't fit is passed as the rejected_substring argument.

text_changed(new_text: String) 🔗

Emitted when the text changes.

text_submitted(new_text: String) 🔗

Emitted when the user presses the ui_text_submit action (by default: Enter or Kp Enter) while the LineEdit has focus.

MenuItems MENU_CUT = 0

Cuts (copies and clears) the selected text.

MenuItems MENU_COPY = 1

Copies the selected text.

MenuItems MENU_PASTE = 2

Pastes the clipboard text over the selected text (or at the caret's position).

Non-printable escape characters are automatically stripped from the OS clipboard via String.strip_escapes().

MenuItems MENU_CLEAR = 3

Erases the whole LineEdit text.

MenuItems MENU_SELECT_ALL = 4

Selects the whole LineEdit text.

MenuItems MENU_UNDO = 5

Undoes the previous action.

MenuItems MENU_REDO = 6

Reverse the last undo action.

MenuItems MENU_SUBMENU_TEXT_DIR = 7

ID of "Text Writing Direction" submenu.

MenuItems MENU_DIR_INHERITED = 8

Sets text direction to inherited.

MenuItems MENU_DIR_AUTO = 9

Sets text direction to automatic.

MenuItems MENU_DIR_LTR = 10

Sets text direction to left-to-right.

MenuItems MENU_DIR_RTL = 11

Sets text direction to right-to-left.

MenuItems MENU_DISPLAY_UCC = 12

Toggles control character display.

MenuItems MENU_SUBMENU_INSERT_UCC = 13

ID of "Insert Control Character" submenu.

MenuItems MENU_INSERT_LRM = 14

Inserts left-to-right mark (LRM) character.

MenuItems MENU_INSERT_RLM = 15

Inserts right-to-left mark (RLM) character.

MenuItems MENU_INSERT_LRE = 16

Inserts start of left-to-right embedding (LRE) character.

MenuItems MENU_INSERT_RLE = 17

Inserts start of right-to-left embedding (RLE) character.

MenuItems MENU_INSERT_LRO = 18

Inserts start of left-to-right override (LRO) character.

MenuItems MENU_INSERT_RLO = 19

Inserts start of right-to-left override (RLO) character.

MenuItems MENU_INSERT_PDF = 20

Inserts pop direction formatting (PDF) character.

MenuItems MENU_INSERT_ALM = 21

Inserts Arabic letter mark (ALM) character.

MenuItems MENU_INSERT_LRI = 22

Inserts left-to-right isolate (LRI) character.

MenuItems MENU_INSERT_RLI = 23

Inserts right-to-left isolate (RLI) character.

MenuItems MENU_INSERT_FSI = 24

Inserts first strong isolate (FSI) character.

MenuItems MENU_INSERT_PDI = 25

Inserts pop direction isolate (PDI) character.

MenuItems MENU_INSERT_ZWJ = 26

Inserts zero width joiner (ZWJ) character.

MenuItems MENU_INSERT_ZWNJ = 27

Inserts zero width non-joiner (ZWNJ) character.

MenuItems MENU_INSERT_WJ = 28

Inserts word joiner (WJ) character.

MenuItems MENU_INSERT_SHY = 29

Inserts soft hyphen (SHY) character.

MenuItems MENU_EMOJI_AND_SYMBOL = 30

Opens system emoji and symbol picker.

MenuItems MENU_MAX = 31

Represents the size of the MenuItems enum.

enum VirtualKeyboardType: 🔗

VirtualKeyboardType KEYBOARD_TYPE_DEFAULT = 0

Default text virtual keyboard.

VirtualKeyboardType KEYBOARD_TYPE_MULTILINE = 1

Multiline virtual keyboard.

VirtualKeyboardType KEYBOARD_TYPE_NUMBER = 2

Virtual number keypad, useful for PIN entry.

VirtualKeyboardType KEYBOARD_TYPE_NUMBER_DECIMAL = 3

Virtual number keypad, useful for entering fractional numbers.

VirtualKeyboardType KEYBOARD_TYPE_PHONE = 4

Virtual phone number keypad.

VirtualKeyboardType KEYBOARD_TYPE_EMAIL_ADDRESS = 5

Virtual keyboard with additional keys to assist with typing email addresses.

VirtualKeyboardType KEYBOARD_TYPE_PASSWORD = 6

Virtual keyboard for entering a password. On most platforms, this should disable autocomplete and autocapitalization.

Note: This is not supported on Web. Instead, this behaves identically to KEYBOARD_TYPE_DEFAULT.

VirtualKeyboardType KEYBOARD_TYPE_URL = 7

Virtual keyboard with additional keys to assist with typing URLs.

HorizontalAlignment alignment = 0 🔗

void set_horizontal_alignment(value: HorizontalAlignment)

HorizontalAlignment get_horizontal_alignment()

Text alignment as defined in the HorizontalAlignment enum.

bool backspace_deletes_composite_character_enabled = false 🔗

void set_backspace_deletes_composite_character_enabled(value: bool)

bool is_backspace_deletes_composite_character_enabled()

If true and caret_mid_grapheme is false, backspace deletes an entire composite character such as ❤️‍🩹, instead of deleting part of the composite character.

bool caret_blink = false 🔗

void set_caret_blink_enabled(value: bool)

bool is_caret_blink_enabled()

If true, makes the caret blink.

float caret_blink_interval = 0.65 🔗

void set_caret_blink_interval(value: float)

float get_caret_blink_interval()

The interval at which the caret blinks (in seconds).

int caret_column = 0 🔗

void set_caret_column(value: int)

int get_caret_column()

The caret's column position inside the LineEdit. When set, the text may scroll to accommodate it.

bool caret_force_displayed = false 🔗

void set_caret_force_displayed(value: bool)

bool is_caret_force_displayed()

If true, the LineEdit will always show the caret, even if not editing or focus is lost.

bool caret_mid_grapheme = false 🔗

void set_caret_mid_grapheme_enabled(value: bool)

bool is_caret_mid_grapheme_enabled()

Allow moving caret, selecting and removing the individual composite character components.

Note: Backspace is always removing individual composite character components.

bool clear_button_enabled = false 🔗

void set_clear_button_enabled(value: bool)

bool is_clear_button_enabled()

If true, the LineEdit will show a clear button if text is not empty, which can be used to clear the text quickly.

bool context_menu_enabled = true 🔗

void set_context_menu_enabled(value: bool)

bool is_context_menu_enabled()

If true, the context menu will appear when right-clicked.

bool deselect_on_focus_loss_enabled = true 🔗

void set_deselect_on_focus_loss_enabled(value: bool)

bool is_deselect_on_focus_loss_enabled()

If true, the selected text will be deselected when focus is lost.

bool drag_and_drop_selection_enabled = true 🔗

void set_drag_and_drop_selection_enabled(value: bool)

bool is_drag_and_drop_selection_enabled()

If true, allow drag and drop of selected text.

bool draw_control_chars = false 🔗

void set_draw_control_chars(value: bool)

bool get_draw_control_chars()

If true, control characters are displayed.

bool editable = true 🔗

void set_editable(value: bool)

If false, existing text cannot be modified and new text cannot be added.

bool emoji_menu_enabled = true 🔗

void set_emoji_menu_enabled(value: bool)

bool is_emoji_menu_enabled()

If true, "Emoji and Symbols" menu is enabled.

bool expand_to_text_length = false 🔗

void set_expand_to_text_length_enabled(value: bool)

bool is_expand_to_text_length_enabled()

If true, the LineEdit width will increase to stay longer than the text. It will not compress if the text is shortened.

void set_flat(value: bool)

If true, the LineEdit doesn't display decoration.

bool keep_editing_on_text_submit = false 🔗

void set_keep_editing_on_text_submit(value: bool)

bool is_editing_kept_on_text_submit()

If true, the LineEdit will not exit edit mode when text is submitted by pressing ui_text_submit action (by default: Enter or Kp Enter).

String language = "" 🔗

void set_language(value: String)

String get_language()

Language code used for line-breaking and text shaping algorithms. If left empty, current locale is used instead.

void set_max_length(value: int)

Maximum number of characters that can be entered inside the LineEdit. If 0, there is no limit.

When a limit is defined, characters that would exceed max_length are truncated. This happens both for existing text contents when setting the max length, or for new text inserted in the LineEdit, including pasting.

If any input text is truncated, the text_change_rejected signal is emitted with the truncated substring as a parameter:

bool middle_mouse_paste_enabled = true 🔗

void set_middle_mouse_paste_enabled(value: bool)

bool is_middle_mouse_paste_enabled()

If false, using middle mouse button to paste clipboard will be disabled.

Note: This method is only implemented on Linux.

String placeholder_text = "" 🔗

void set_placeholder(value: String)

String get_placeholder()

Text shown when the LineEdit is empty. It is not the LineEdit's default value (see text).

Texture2D right_icon 🔗

void set_right_icon(value: Texture2D)

Texture2D get_right_icon()

Sets the icon that will appear in the right end of the LineEdit if there's no text, or always, if clear_button_enabled is set to false.

bool secret = false 🔗

void set_secret(value: bool)

If true, every character is replaced with the secret character (see secret_character).

String secret_character = "•" 🔗

void set_secret_character(value: String)

String get_secret_character()

The character to use to mask secret input. Only a single character can be used as the secret character. If it is longer than one character, only the first one will be used. If it is empty, a space will be used instead.

bool select_all_on_focus = false 🔗

void set_select_all_on_focus(value: bool)

bool is_select_all_on_focus()

If true, the LineEdit will select the whole text when it gains focus.

bool selecting_enabled = true 🔗

void set_selecting_enabled(value: bool)

bool is_selecting_enabled()

If false, it's impossible to select the text using mouse nor keyboard.

bool shortcut_keys_enabled = true 🔗

void set_shortcut_keys_enabled(value: bool)

bool is_shortcut_keys_enabled()

If true, shortcut keys for context menu items are enabled, even if the context menu is disabled.

StructuredTextParser structured_text_bidi_override = 0 🔗

void set_structured_text_bidi_override(value: StructuredTextParser)

StructuredTextParser get_structured_text_bidi_override()

Set BiDi algorithm override for the structured text.

Array structured_text_bidi_override_options = [] 🔗

void set_structured_text_bidi_override_options(value: Array)

Array get_structured_text_bidi_override_options()

Set additional options for BiDi override.

void set_text(value: String)

String value of the LineEdit.

Note: Changing text using this property won't emit the text_changed signal.

TextDirection text_direction = 0 🔗

void set_text_direction(value: TextDirection)

TextDirection get_text_direction()

Base text writing direction.

bool virtual_keyboard_enabled = true 🔗

void set_virtual_keyboard_enabled(value: bool)

bool is_virtual_keyboard_enabled()

If true, the native virtual keyboard is enabled on platforms that support it.

bool virtual_keyboard_show_on_focus = true 🔗

void set_virtual_keyboard_show_on_focus(value: bool)

bool get_virtual_keyboard_show_on_focus()

If true, the native virtual keyboard is shown on focus events on platforms that support it.

VirtualKeyboardType virtual_keyboard_type = 0 🔗

void set_virtual_keyboard_type(value: VirtualKeyboardType)

VirtualKeyboardType get_virtual_keyboard_type()

Specifies the type of virtual keyboard to show.

Applies text from the Input Method Editor (IME) and closes the IME if it is open.

Closes the Input Method Editor (IME) if it is open. Any text in the IME will be lost.

Erases the LineEdit's text.

void delete_char_at_caret() 🔗

Deletes one character at the caret's current position (equivalent to pressing Delete).

void delete_text(from_column: int, to_column: int) 🔗

Deletes a section of the text going from position from_column to to_column. Both parameters should be within the text's length.

Clears the current selection.

Allows entering edit mode whether the LineEdit is focused or not.

See also keep_editing_on_text_submit.

PopupMenu get_menu() const 🔗

Returns the PopupMenu of this LineEdit. By default, this menu is displayed when right-clicking on the LineEdit.

You can add custom menu items or remove standard ones. Make sure your IDs don't conflict with the standard ones (see MenuItems). For example:

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their Window.visible property.

int get_next_composite_character_column(column: int) const 🔗

Returns the correct column at the end of a composite character like ❤️‍🩹 (mending heart; Unicode: U+2764 U+FE0F U+200D U+1FA79) which is comprised of more than one Unicode code point, if the caret is at the start of the composite character. Also returns the correct column with the caret at mid grapheme and for non-composite characters.

Note: To check at caret location use get_next_composite_character_column(get_caret_column())

int get_previous_composite_character_column(column: int) const 🔗

Returns the correct column at the start of a composite character like ❤️‍🩹 (mending heart; Unicode: U+2764 U+FE0F U+200D U+1FA79) which is comprised of more than one Unicode code point, if the caret is at the end of the composite character. Also returns the correct column with the caret at mid grapheme and for non-composite characters.

Note: To check at caret location use get_previous_composite_character_column(get_caret_column())

float get_scroll_offset() const 🔗

Returns the scroll offset due to caret_column, as a number of characters.

String get_selected_text() 🔗

Returns the text inside the selection.

int get_selection_from_column() const 🔗

Returns the selection begin column.

int get_selection_to_column() const 🔗

Returns the selection end column.

bool has_ime_text() const 🔗

Returns true if the user has text in the Input Method Editor (IME).

bool has_redo() const 🔗

Returns true if a "redo" action is available.

bool has_selection() const 🔗

Returns true if the user has selected text.

bool has_undo() const 🔗

Returns true if an "undo" action is available.

void insert_text_at_caret(text: String) 🔗

Inserts text at the caret. If the resulting value is longer than max_length, nothing happens.

bool is_editing() const 🔗

Returns whether the LineEdit is being edited.

bool is_menu_visible() const 🔗

Returns whether the menu is visible. Use this instead of get_menu().visible to improve performance (so the creation of the menu is avoided).

void menu_option(option: int) 🔗

Executes a given action as defined in the MenuItems enum.

void select(from: int = 0, to: int = -1) 🔗

Selects characters inside LineEdit between from and to. By default, from is at the beginning and to at the end.

Selects the whole String.

Allows exiting edit mode while preserving focus.

Color caret_color = Color(0.95, 0.95, 0.95, 1) 🔗

Color of the LineEdit's caret (text cursor). This can be set to a fully transparent color to hide the caret entirely.

Color clear_button_color = Color(0.875, 0.875, 0.875, 1) 🔗

Color used as default tint for the clear button.

Color clear_button_color_pressed = Color(1, 1, 1, 1) 🔗

Color used for the clear button when it's pressed.

Color font_color = Color(0.875, 0.875, 0.875, 1) 🔗

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The tint of text outline of the LineEdit.

Color font_placeholder_color = Color(0.875, 0.875, 0.875, 0.6) 🔗

Font color for placeholder_text.

Color font_selected_color = Color(1, 1, 1, 1) 🔗

Font color for selected text (inside the selection rectangle).

Color font_uneditable_color = Color(0.875, 0.875, 0.875, 0.5) 🔗

Font color when editing is disabled.

Color selection_color = Color(0.5, 0.5, 0.5, 1) 🔗

Color of the selection rectangle.

int caret_width = 1 🔗

The caret's width in pixels. Greater values can be used to improve accessibility by ensuring the caret is easily visible, or to ensure consistency with a large font size.

int minimum_character_width = 4 🔗

Minimum horizontal space for the text (not counting the clear button and content margins). This value is measured in count of 'M' characters (i.e. this number of 'M' characters can be displayed without scrolling).

int outline_size = 0 🔗

The size of the text outline.

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

Font used for the text.

Font size of the LineEdit's text.

Texture for the clear button. See clear_button_enabled.

Background used when LineEdit has GUI focus. The focus StyleBox is displayed over the base StyleBox, so a partially transparent StyleBox should be used to ensure the base StyleBox remains visible. A StyleBox that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a StyleBoxEmpty resource. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

Default background for the LineEdit.

Background used when LineEdit is in read-only mode (editable is set to false).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (markdown):
```markdown
text = "Hello world"
max_length = 5
# `text` becomes "Hello".
max_length = 10
text += " goodbye"
# `text` becomes "Hello good".
# `text_change_rejected` is emitted with "bye" as a parameter.
```

Example 2 (typescript):
```typescript
Text = "Hello world";
MaxLength = 5;
// `Text` becomes "Hello".
MaxLength = 10;
Text += " goodbye";
// `Text` becomes "Hello good".
// `text_change_rejected` is emitted with "bye" as a parameter.
```

Example 3 (gdscript):
```gdscript
func _ready():
    var menu = get_menu()
    # Remove all items after "Redo".
    menu.item_count = menu.get_item_index(MENU_REDO) + 1
    # Add custom items.
    menu.add_separator()
    menu.add_item("Insert Date", MENU_MAX + 1)
    # Connect callback.
    menu.id_pressed.connect(_on_item_pressed)

func _on_item_pressed(id):
    if id == MENU_MAX + 1:
        insert_text_at_caret(Time.get_date_string_from_system())
```

Example 4 (gdscript):
```gdscript
public override void _Ready()
{
    var menu = GetMenu();
    // Remove all items after "Redo".
    menu.ItemCount = menu.GetItemIndex(LineEdit.MenuItems.Redo) + 1;
    // Add custom items.
    menu.AddSeparator();
    menu.AddItem("Insert Date", LineEdit.MenuItems.Max + 1);
    // Add event handler.
    menu.IdPressed += OnItemPressed;
}

public void OnItemPressed(int id)
{
    if (id == LineEdit.MenuItems.Max + 1)
    {
        InsertTextAtCaret(Time.GetDateStringFromSystem());
    }
}
```

---

## LinkButton

**URL:** https://docs.godotengine.org/en/stable/classes/class_linkbutton.html

**Contents:**
- LinkButton
- Description
- Properties
- Theme Properties
- Enumerations
- Property Descriptions
- Theme Property Descriptions
- User-contributed notes

Inherits: BaseButton < Control < CanvasItem < Node < Object

A button that represents a link.

A button that represents a link. This type of button is primarily used for interactions that cause a context change (like linking to a web page).

See also BaseButton which contains common properties and methods associated with this node.

3 (overrides Control)

mouse_default_cursor_shape

2 (overrides Control)

structured_text_bidi_override

structured_text_bidi_override_options

Color(0.875, 0.875, 0.875, 1)

Color(0.95, 0.95, 0.95, 1)

Color(0.95, 0.95, 0.95, 1)

font_hover_pressed_color

enum UnderlineMode: 🔗

UnderlineMode UNDERLINE_MODE_ALWAYS = 0

The LinkButton will always show an underline at the bottom of its text.

UnderlineMode UNDERLINE_MODE_ON_HOVER = 1

The LinkButton will show an underline at the bottom of its text when the mouse cursor is over it.

UnderlineMode UNDERLINE_MODE_NEVER = 2

The LinkButton will never show an underline at the bottom of its text.

String language = "" 🔗

void set_language(value: String)

String get_language()

Language code used for line-breaking and text shaping algorithms, if left empty current locale is used instead.

StructuredTextParser structured_text_bidi_override = 0 🔗

void set_structured_text_bidi_override(value: StructuredTextParser)

StructuredTextParser get_structured_text_bidi_override()

Set BiDi algorithm override for the structured text.

Array structured_text_bidi_override_options = [] 🔗

void set_structured_text_bidi_override_options(value: Array)

Array get_structured_text_bidi_override_options()

Set additional options for BiDi override.

void set_text(value: String)

The button's text that will be displayed inside the button's area.

TextDirection text_direction = 0 🔗

void set_text_direction(value: TextDirection)

TextDirection get_text_direction()

Base text writing direction.

UnderlineMode underline = 0 🔗

void set_underline_mode(value: UnderlineMode)

UnderlineMode get_underline_mode()

The underline mode to use for the text.

void set_uri(value: String)

The URI for this LinkButton. If set to a valid URI, pressing the button opens the URI using the operating system's default program for the protocol (via OS.shell_open()). HTTP and HTTPS URLs open the default web browser.

Color font_color = Color(0.875, 0.875, 0.875, 1) 🔗

Default text Color of the LinkButton.

Color font_disabled_color = Color(0, 0, 0, 1) 🔗

Text Color used when the LinkButton is disabled.

Color font_focus_color = Color(0.95, 0.95, 0.95, 1) 🔗

Text Color used when the LinkButton is focused. Only replaces the normal text color of the button. Disabled, hovered, and pressed states take precedence over this color.

Color font_hover_color = Color(0.95, 0.95, 0.95, 1) 🔗

Text Color used when the LinkButton is being hovered.

Color font_hover_pressed_color = Color(0, 0, 0, 1) 🔗

Text Color used when the LinkButton is being hovered and pressed.

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The tint of text outline of the LinkButton.

Color font_pressed_color = Color(1, 1, 1, 1) 🔗

Text Color used when the LinkButton is being pressed.

int outline_size = 0 🔗

The size of the text outline.

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

int underline_spacing = 2 🔗

The vertical space between the baseline of text and the underline.

Font of the LinkButton's text.

Font size of the LinkButton's text.

StyleBox used when the LinkButton is focused. The focus StyleBox is displayed over the base StyleBox, so a partially transparent StyleBox should be used to ensure the base StyleBox remains visible. A StyleBox that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a StyleBoxEmpty resource. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
uri = "https://godotengine.org"  # Opens the URL in the default web browser.
uri = "C:\SomeFolder"  # Opens the file explorer at the given path.
uri = "C:\SomeImage.png"  # Opens the given image in the default viewing app.
```

Example 2 (unknown):
```unknown
Uri = "https://godotengine.org"; // Opens the URL in the default web browser.
Uri = "C:\SomeFolder"; // Opens the file explorer at the given path.
Uri = "C:\SomeImage.png"; // Opens the given image in the default viewing app.
```

---

## Localization using gettext (PO files)

**URL:** https://docs.godotengine.org/en/stable/tutorials/i18n/localization_using_gettext.html

**Contents:**
- Localization using gettext (PO files)
- Advantages
- Disadvantages
- Installing gettext tools
- Creating the PO template
  - Automatic generation using the editor
  - Manual creation
- Creating a messages file from a PO template
- Loading a messages file in Godot
- Updating message files to follow the PO template

In addition to importing translations in CSV format, Godot also supports loading translation files written in the GNU gettext format (text-based .po and compiled .mo since Godot 4.0).

For an introduction to gettext, check out A Quick Gettext Tutorial. It's written with C projects in mind, but much of the advice also applies to Godot (with the exception of xgettext).

For the complete documentation, see GNU Gettext.

gettext is a standard format, which can be edited using any text editor or GUI editors such as Poedit. This can be significant as it provides a lot of tools for translators, such as marking outdated strings, finding strings that haven't been translated etc.

gettext supports plurals and context.

gettext is supported by translation platforms such as Transifex and Weblate, which makes it easier for people to collaborate to localization.

Compared to CSV, gettext files work better with version control systems like Git, as each locale has its own messages file.

Multiline strings are more convenient to edit in gettext PO files compared to CSV files.

gettext PO files have a more complex format than CSV and can be harder to grasp for people new to software localization.

People who maintain localization files will have to install gettext tools on their system. However, as Godot supports using text-based message files (.po), translators can test their work without having to install gettext tools.

gettext PO files usually use English as the base language. Translators will use this base language to translate to other languages. You could still user other languages as the base language, but this is not common.

The command line gettext tools are required to perform maintenance operations, such as updating message files. Therefore, it's strongly recommended to install them.

Windows: Download an installer from this page. Any architecture and binary type (shared or static) works; if in doubt, choose the 64-bit static installer.

macOS: Install gettext either using Homebrew with the brew install gettext command, or using MacPorts with the sudo port install gettext command.

Linux: On most distributions, install the gettext package from your distribution's package manager.

For a GUI tool you can get Poedit from its Official website. The basic version is open source and available under the MIT license.

Since Godot 4.0, the editor can generate a PO template automatically from specified scene and GDScript files. This POT generation also supports translation contexts and pluralization if used in a script, with the optional second argument of tr() and the tr_n() method.

Open the Project Settings' Localization > POT Generation tab, then use the Add… button to specify the path to your project's scenes and scripts that contain localizable strings:

Creating a PO template in the Localization > POT Generation tab of the Project Settings

After adding at least one scene or script, click Generate POT in the top-right corner, then specify the path to the output file. This file can be placed anywhere in the project directory, but it's recommended to keep it in a subdirectory such as locale, as each locale will be defined in its own file.

See below for how to add comments for translators or exclude some strings from being added to the PO template for GDScript files.

You can then move over to creating a messages file from a PO template.

Remember to regenerate the PO template after making any changes to localizable strings, or after adding new scenes or scripts. Otherwise, newly added strings will not be localizable and translators won't be able to update translations for outdated strings.

If the automatic generation approach doesn't work out for your needs, you can create a PO template by hand in a text editor. This file can be placed anywhere in the project directory, but it's recommended to keep it in a subdirectory, as each locale will be defined in its own file.

Create a directory named locale in the project directory. In this directory, save a file named messages.pot with the following contents:

Messages in gettext are made of msgid and msgstr pairs. msgid is the source string (usually in English), msgstr will be the translated string.

The msgstr value in PO template files (.pot) should always be empty. Localization will be done in the generated .po files instead.

The msginit command is used to turn a PO template into a messages file. For instance, to create a French localization file, use the following command while in the locale directory:

The command above will create a file named fr.po in the same directory as the PO template.

Alternatively, you can do that graphically using Poedit, or by uploading the POT file to your web platform of choice.

To register a messages file as a translation in a project, open the Project Settings, then go to the Localization tab. In Translations, click Add… then choose the .po or .mo file in the file dialog. The locale will be inferred from the "Language: <code>\n" property in the messages file.

See Internationalizing games for more information on importing and testing translations in Godot.

After updating the PO template, you will have to update message files so that they contain new strings, while removing strings that are no longer present in the PO template. This can be done automatically using the msgmerge tool:

If you want to keep a backup of the original message file (which would be saved as fr.po~ in this example), remove the --backup=none argument.

After running msgmerge, strings which were modified in the source language will have a "fuzzy" comment added before them in the .po file. This comment denotes that the translation should be updated to match the new source string, as the translation will most likely be inaccurate until it's updated.

Strings with "fuzzy" comments will not be read by Godot until the translation is updated and the "fuzzy" comment is removed.

It is possible to check whether a gettext file's syntax is valid.

If you open with Poeditor, it will display the appropriate warnings if there's some syntax errors. You can also verify by running the gettext command below:

If there are syntax errors or warnings, they will be displayed in the console. Otherwise, msgfmt won't output anything.

For large projects with several thousands of strings to translate or more, it can be worth it to use binary (compiled) MO message files instead of text-based PO files. Binary MO files are smaller and faster to read than the equivalent PO files.

You can generate an MO file with the command below:

If the PO file is valid, this command will create an fr.mo file besides the PO file. This MO file can then be loaded in Godot as described above.

The original PO file should be kept in version control so you can update your translation in the future. In case you lose the original PO file and wish to decompile an MO file into a text-based PO file, you can do so with:

The decompiled file will not include comments or fuzzy strings, as these are never compiled in the MO file in the first place.

The built-in editor plugin recognizes a variety of patterns in source code to extract localizable strings from GDScript files, including but not limited to the following:

tr(), tr_n(), atr(), and atr_n() calls;

assigning properties text, placeholder_text, and tooltip_text;

add_tab(), add_item(), set_tab_title(), and other calls;

FileDialog filters like "*.png ; PNG Images".

The argument or right operand must be a constant string, otherwise the plugin will not be able to evaluate the expression and will ignore it.

If the plugin extracts unnecessary strings, you can ignore them with the NO_TRANSLATE comment. You can also provide additional information for translators using the TRANSLATORS: comment. These comments must be placed either on the same line as the recognized pattern or precede it.

The context parameter can be used to differentiate the situation where a translation is used, or to differentiate polysemic words (words with multiple meanings).

Some time or later, you'll add new content to our game, and there will be new strings that need to be translated. When this happens, you'll need to update the existing PO files to include the new strings.

First, generate a new POT file containing all the existing strings plus the newly added strings. After that, merge the existing PO files with the new POT file. There are two ways to do this:

Use a gettext editor, and it should have an option to update a PO file from a POT file.

Use the gettext msgmerge tool:

If you want to keep a backup of the original message file (which would be saved as fr.po~ in this example), remove the --backup=none argument.

If you have any extra file format to deal with, you could write a custom plugin to parse and and extract the strings from the custom file. This custom plugin will extract the strings and write into the POT file when you hit Generate POT. To learn more about how to create the translation parser plugin, see EditorTranslationParserPlugin.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (markdown):
```markdown
# Don't remove the two lines below, they're required for gettext to work correctly.
msgid ""
msgstr ""

# Example of a regular string.
msgid "Hello world!"
msgstr ""

# Example of a string with pluralization.
msgid "There is %d apple."
msgid_plural "There are %d apples."
msgstr[0] ""
msgstr[1] ""

# Example of a string with a translation context.
msgctxt "Actions"
msgid "Close"
msgstr ""
```

Example 2 (unknown):
```unknown
msginit --no-translator --input=messages.pot --locale=fr
```

Example 3 (sql):
```sql
# The order matters: specify the message file *then* the PO template!
msgmerge --update --backup=none fr.po messages.pot
```

Example 4 (unknown):
```unknown
msgfmt fr.po --check
```

---

## Localization using spreadsheets

**URL:** https://docs.godotengine.org/en/stable/tutorials/i18n/localization_using_spreadsheets.html

**Contents:**
- Localization using spreadsheets
- Formatting
- CSV importer
- User-contributed notes

Spreadsheets are one of the most common formats for localizing games. In Godot, spreadsheets are supported through the CSV format. This guide explains how to work with CSVs.

The CSV files must be saved with UTF-8 encoding without a byte order mark.

By default, Microsoft Excel will always save CSV files with ANSI encoding rather than UTF-8. There is no built-in way to do this, but there are workarounds as described here.

We recommend using LibreOffice or Google Sheets instead.

CSV files must be formatted as follows:

The "lang" tags must represent a language, which must be one of the valid locales supported by the engine, or they must start with an underscore (_), which means the related column is served as comment and won't be imported. The "KEY" tags must be unique and represent a string universally (they are usually in uppercase, to differentiate from other strings). These keys will be replaced at runtime by the matching translated string. Note that the case is important, "KEY1" and "Key1" will be different keys. The top-left cell is ignored and can be left empty or having any content. Here's an example:

"Hello" said the man.

"Hola" dijo el hombre.

The same example is shown below as a comma-separated plain text file, which should be the result of editing the above in a spreadsheet. When editing the plain text version, be sure to enclose with double quotes any message that contains commas, line breaks or double quotes, so that commas are not parsed as delimiters, line breaks don't create new entries and double quotes are not parsed as enclosing characters. Be sure to escape any double quotes a message may contain by preceding them with another double quote. Alternatively, you can select another delimiter than comma in the import options.

Godot will treat CSV files as translations by default. It will import them and generate one or more compressed translation resource files next to it.

Importing will also add the translation to the list of translations to load when the game runs, specified in project.godot (or the project settings). Godot allows loading and removing translations at runtime as well.

Select the .csv file and access the Import dock to define import options. You can toggle the compression of the imported translations, and select the delimiter to use when parsing the CSV file.

Be sure to click Reimport after any change to these options.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
keys,en,es,ja
GREET,"Hello, friend!","Hola, amigo!",こんにちは
ASK,How are you?,Cómo está?,元気ですか
BYE,Goodbye,Adiós,さようなら
QUOTE,"""Hello"" said the man.","""Hola"" dijo el hombre.",「こんにちは」男は言いました
```

---

## MarginContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_margincontainer.html

**Contents:**
- MarginContainer
- Description
- Tutorials
- Theme Properties
- Theme Property Descriptions
- User-contributed notes

Inherits: Container < Control < CanvasItem < Node < Object

A container that keeps a margin around its child controls.

MarginContainer adds an adjustable margin on each side of its child controls. The margins are added around all children, not around each individual one. To control the MarginContainer's margins, use the margin_* theme properties listed below.

Note: The margin sizes are theme overrides, not normal properties. This is an example of how to change them in code:

int margin_bottom = 0 🔗

Offsets towards the inside direct children of the container by this amount of pixels from the bottom.

int margin_left = 0 🔗

Offsets towards the inside direct children of the container by this amount of pixels from the left.

int margin_right = 0 🔗

Offsets towards the inside direct children of the container by this amount of pixels from the right.

Offsets towards the inside direct children of the container by this amount of pixels from the top.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
# This code sample assumes the current script is extending MarginContainer.
var margin_value = 100
add_theme_constant_override("margin_top", margin_value)
add_theme_constant_override("margin_left", margin_value)
add_theme_constant_override("margin_bottom", margin_value)
add_theme_constant_override("margin_right", margin_value)
```

Example 2 (unknown):
```unknown
// This code sample assumes the current script is extending MarginContainer.
int marginValue = 100;
AddThemeConstantOverride("margin_top", marginValue);
AddThemeConstantOverride("margin_left", marginValue);
AddThemeConstantOverride("margin_bottom", marginValue);
AddThemeConstantOverride("margin_right", marginValue);
```

---

## Matrices and transforms

**URL:** https://docs.godotengine.org/en/stable/tutorials/math/matrices_and_transforms.html

**Contents:**
- Matrices and transforms
- Introduction
  - Matrix components and the Identity matrix
  - Scaling the transformation matrix
  - Rotating the transformation matrix
  - Basis of the transformation matrix
  - Translating the transformation matrix
  - Putting it all together
  - Shearing the transformation matrix (advanced)
- Practical applications of transforms

Before reading this tutorial, we recommend that you thoroughly read and understand the Vector math tutorial, as this tutorial requires a knowledge of vectors.

This tutorial is about transformations and how we represent them in Godot using matrices. It is not a full in-depth guide to matrices. Transformations are most of the time applied as translation, rotation, and scale, so we will focus on how to represent those with matrices.

Most of this guide focuses on 2D, using Transform2D and Vector2, but the way things work in 3D is very similar.

As mentioned in the previous tutorial, it is important to remember that in Godot, the Y axis points down in 2D. This is the opposite of how most schools teach linear algebra, with the Y axis pointing up.

The convention is that the X axis is red, the Y axis is green, and the Z axis is blue. This tutorial is color-coded to match these conventions, but we will also represent the origin vector with a blue color.

The identity matrix represents a transform with no translation, no rotation, and no scale. Let's start by looking at the identity matrix and how its components relate to how it visually appears.

Matrices have rows and columns, and a transformation matrix has specific conventions on what each does.

In the image above, we can see that the red X vector is represented by the first column of the matrix, and the green Y vector is likewise represented by the second column. A change to the columns will change these vectors. We will see how they can be manipulated in the next few examples.

You should not worry about manipulating rows directly, as we usually work with columns. However, you can think of the rows of the matrix as showing which vectors contribute to moving in a given direction.

When we refer to a value such as t.x.y, that's the Y component of the X column vector. In other words, the bottom-left of the matrix. Similarly, t.x.x is top-left, t.y.x is top-right, and t.y.y is bottom-right, where t is the Transform2D.

Applying a scale is one of the easiest operations to understand. Let's start by placing the Godot logo underneath our vectors so that we can visually see the effects on an object:

Now, to scale the matrix, all we need to do is multiply each component by the scale we want. Let's scale it up by 2. 1 times 2 becomes 2, and 0 times 2 becomes 0, so we end up with this:

To do this in code, we multiply each of the vectors:

If we wanted to return it to its original scale, we can multiply each component by 0.5. That's pretty much all there is to scaling a transformation matrix.

To calculate the object's scale from an existing transformation matrix, you can use length() on each of the column vectors.

In actual projects, you can use the scaled() method to perform scaling.

We'll start the same way as earlier, with the Godot logo underneath the identity matrix:

As an example, let's say we want to rotate our Godot logo clockwise by 90 degrees. Right now the X axis points right and the Y axis points down. If we rotate these in our head, we would logically see that the new X axis should point down and the new Y axis should point left.

You can imagine that you grab both the Godot logo and its vectors, and then spin it around the center. Wherever you finish spinning, the orientation of the vectors determines what the matrix is.

We need to represent "down" and "left" in normal coordinates, so means we'll set X to (0, 1) and Y to (-1, 0). These are also the values of Vector2.DOWN and Vector2.LEFT. When we do this, we get the desired result of rotating the object:

If you have trouble understanding the above, try this exercise: Cut a square of paper, draw X and Y vectors on top of it, place it on graph paper, then rotate it and note the endpoints.

To perform rotation in code, we need to be able to calculate the values programmatically. This image shows the formulas needed to calculate the transformation matrix from a rotation angle. Don't worry if this part seems complicated, I promise it's the hardest thing you need to know.

Godot represents all rotations with radians, not degrees. A full turn is TAU or PI*2 radians, and a quarter turn of 90 degrees is TAU/4 or PI/2 radians. Working with TAU usually results in more readable code.

Fun fact: In addition to Y being down in Godot, rotation is represented clockwise. This means that all the math and trig functions behave the same as a Y-is-up CCW system, since these differences "cancel out". You can think of rotations in both systems being "from X to Y".

In order to perform a rotation of 0.5 radians (about 28.65 degrees), we plug in a value of 0.5 to the formula above and evaluate to find what the actual values should be:

Here's how that would be done in code (place the script on a Node2D):

To calculate the object's rotation from an existing transformation matrix, you can use atan2(t.x.y, t.x.x), where t is the Transform2D.

In actual projects, you can use the rotated() method to perform rotations.

So far we have only been working with the x and y, vectors, which are in charge of representing rotation, scale, and/or shearing (advanced, covered at the end). The X and Y vectors are together called the basis of the transformation matrix. The terms "basis" and "basis vectors" are important to know.

You might have noticed that Transform2D actually has three Vector2 values: x, y, and origin. The origin value is not part of the basis, but it is part of the transform, and we need it to represent position. From now on we'll keep track of the origin vector in all examples. You can think of origin as another column, but it's often better to think of it as completely separate.

Note that in 3D, Godot has a separate Basis structure for holding the three Vector3 values of the basis, since the code can get complex and it makes sense to separate it from Transform3D (which is composed of one Basis and one extra Vector3 for the origin).

Changing the origin vector is called translating the transformation matrix. Translating is basically a technical term for "moving" the object, but it explicitly does not involve any rotation.

Let's work through an example to help understand this. We will start with the identity transform like last time, except we will keep track of the origin vector this time.

If we want to move the object to a position of (1, 2), we need to set its origin vector to (1, 2):

There is also a translated_local() method, which performs a different operation to adding or changing origin directly. The translated_local() method will translate the object relative to its own rotation. For example, an object rotated 90 degrees clockwise will move to the right when translated_local() with Vector2.UP. To translate relative to the global/parent frame use translated() instead.

Godot's 2D uses coordinates based on pixels, so in actual projects you will want to translate by hundreds of units.

We're going to apply everything we mentioned so far onto one transform. To follow along, create a project with a Sprite2D node and use the Godot logo for the texture resource.

Let's set the translation to (350, 150), rotate by -0.5 rad, and scale by 3. I've posted a screenshot, and the code to reproduce it, but I encourage you to try and reproduce the screenshot without looking at the code!

If you are only looking for how to use transformation matrices, feel free to skip this section of the tutorial. This section explores an uncommonly used aspect of transformation matrices for the purpose of building an understanding of them.

Node2D provides a shearing property out of the box.

You may have noticed that a transform has more degrees of freedom than the combination of the above actions. The basis of a 2D transformation matrix has four total numbers in two Vector2 values, while a rotation value and a Vector2 for scale only has 3 numbers. The high-level concept for the missing degree of freedom is called shearing.

Normally, you will always have the basis vectors perpendicular to each other. However, shearing can be useful in some situations, and understanding shearing helps you understand how transforms work.

To show you visually how it will look, let's overlay a grid onto the Godot logo:

Each point on this grid is obtained by adding the basis vectors together. The bottom-right corner is X + Y, while the top-right corner is X - Y. If we change the basis vectors, the entire grid moves with it, as the grid is composed of the basis vectors. All lines on the grid that are currently parallel will remain parallel no matter what changes we make to the basis vectors.

As an example, let's set Y to (1, 1):

You can't set the raw values of a Transform2D in the editor, so you must use code if you want to shear the object.

Due to the vectors no longer being perpendicular, the object has been sheared. The bottom-center of the grid, which is (0, 1) relative to itself, is now located at a world position of (1, 1).

The intra-object coordinates are called UV coordinates in textures, so let's borrow that terminology for here. To find the world position from a relative position, the formula is U * X + V * Y, where U and V are numbers and X and Y are the basis vectors.

The bottom-right corner of the grid, which is always at the UV position of (1, 1), is at the world position of (2, 1), which is calculated from X*1 + Y*1, which is (1, 0) + (1, 1), or (1 + 1, 0 + 1), or (2, 1). This matches up with our observation of where the bottom-right corner of the image is.

Similarly, the top-right corner of the grid, which is always at the UV position of (1, -1), is at the world position of (0, -1), which is calculated from X*1 + Y*-1, which is (1, 0) - (1, 1), or (1 - 1, 0 - 1), or (0, -1). This matches up with our observation of where the top-right corner of the image is.

Hopefully you now fully understand how a transformation matrix affects the object, and the relationship between the basis vectors and how the object's "UV" or "intra-coordinates" have their world position changed.

In Godot, all transform math is done relative to the parent node. When we refer to "world position", that would be relative to the node's parent instead, if the node had a parent.

If you would like additional explanation, you should check out 3Blue1Brown's excellent video about linear transformations: https://www.youtube.com/watch?v=kYB8IZa5AuE

In actual projects, you will usually be working with transforms inside transforms by having multiple Node2D or Node3D nodes parented to each other.

However, it's useful to understand how to manually calculate the values we need. We will go over how you could use Transform2D or Transform3D to manually calculate transforms of nodes.

There are many cases where you'd want to convert a position in and out of a transform. For example, if you have a position relative to the player and would like to find the world (parent-relative) position, or if you have a world position and want to know where it is relative to the player.

We can find what a vector relative to the player would be defined in world space as using the * operator:

And we can use the * operator in the opposite order to find a what world space position would be if it was defined relative to the player:

If you know in advance that the transform is positioned at (0, 0), you can use the "basis_xform" or "basis_xform_inv" methods instead, which skip dealing with translation.

A common operation, especially in 3D games, is to move an object relative to itself. For example, in first-person shooter games, you would want the character to move forward (-Z axis) when you press W.

Since the basis vectors are the orientation relative to the parent, and the origin vector is the position relative to the parent, we can add multiples of the basis vectors to move an object relative to itself.

This code moves an object 100 units to its own right:

For moving in 3D, you would need to replace "x" with "basis.x".

In actual projects, you can use translate_object_local in 3D or move_local_x and move_local_y in 2D to do this.

One of the most important things to know about transforms is how you can use several of them together. A parent node's transform affects all of its children. Let's dissect an example.

In this image, the child node has a "2" after the component names to distinguish them from the parent node. It might look a bit overwhelming with so many numbers, but remember that each number is displayed twice (next to the arrows and also in the matrices), and that almost half of the numbers are zero.

The only transformations going on here are that the parent node has been given a scale of (2, 1), the child has been given a scale of (0.5, 0.5), and both nodes have been given positions.

All child transformations are affected by the parent transformations. The child has a scale of (0.5, 0.5), so you would expect it to be a 1:1 ratio square, and it is, but only relative to the parent. The child's X vector ends up being (1, 0) in world space, because it is scaled by the parent's basis vectors. Similarly, the child node's origin vector is set to (1, 1), but this actually moves it (2, 1) in world space, due to the parent node's basis vectors.

To calculate a child transform's world space transform manually, this is the code we would use:

In actual projects, we can find the world transform of the child by applying one transform onto another using the * operator:

When multiplying matrices, order matters! Don't mix them up.

Lastly, applying the identity transform will always do nothing.

If you would like additional explanation, you should check out 3Blue1Brown's excellent video about matrix composition: https://www.youtube.com/watch?v=XkY2DOUCWMU

The "affine_inverse" function returns a transform that "undoes" the previous transform. This can be useful in some situations. Let's take a look at a few examples.

Multiplying an inverse transform by the normal transform undoes all transformations:

Transforming a position by a transform and its inverse results in the same position:

One of the great things about transformation matrices is that they work very similarly between 2D and 3D transformations. All the code and formulas used above for 2D work the same in 3D, with 3 exceptions: the addition of a third axis, that each axis is of type Vector3, and also that Godot stores the Basis separately from the Transform3D, since the math can get complex and it makes sense to separate it.

All of the concepts for how translation, rotation, scale, and shearing work in 3D are all the same compared to 2D. To scale, we take each component and multiply it; to rotate, we change where each basis vector is pointing; to translate, we manipulate the origin; and to shear, we change the basis vectors to be non-perpendicular.

If you would like, it's a good idea to play around with transforms to get an understanding of how they work. Godot allows you to edit 3D transform matrices directly from the inspector. You can download this project which has colored lines and cubes to help visualize the Basis vectors and the origin in both 2D and 3D: https://github.com/godotengine/godot-demo-projects/tree/master/misc/matrix_transform

You cannot edit Node2D's transform matrix directly in Godot 4.0's inspector. This may be changed in a future release of Godot.

If you would like additional explanation, you should check out 3Blue1Brown's excellent video about 3D linear transformations: https://www.youtube.com/watch?v=rHLEWRxRGiM

The biggest difference between 2D and 3D transformation matrices is how you represent rotation by itself without the basis vectors.

With 2D, we have an easy way (atan2) to switch between a transformation matrix and an angle. In 3D, rotation is too complex to represent as one number. There is something called Euler angles, which can represent rotations as a set of 3 numbers, however, they are limited and not very useful, except for trivial cases.

In 3D we do not typically use angles, we either use a transformation basis (used pretty much everywhere in Godot), or we use quaternions. Godot can represent quaternions using the Quaternion struct. My suggestion to you is to completely ignore how they work under-the-hood, because they are very complicated and unintuitive.

However, if you really must know how it works, here are some great resources, which you can follow in order:

https://www.youtube.com/watch?v=mvmuCPvRoWQ

https://www.youtube.com/watch?v=d4EgbgTm0Bg

https://eater.net/quaternions

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
var t = Transform2D()
# Scale
t.x *= 2
t.y *= 2
transform = t # Change the node's transform to what we calculated.
```

Example 2 (csharp):
```csharp
Transform2D t = Transform2D.Identity;
// Scale
t.X *= 2;
t.Y *= 2;
Transform = t; // Change the node's transform to what we calculated.
```

Example 3 (csharp):
```csharp
var rot = 0.5 # The rotation to apply.
var t = Transform2D()
t.x.x = cos(rot)
t.y.y = cos(rot)
t.x.y = sin(rot)
t.y.x = -sin(rot)
transform = t # Change the node's transform to what we calculated.
```

Example 4 (csharp):
```csharp
float rot = 0.5f; // The rotation to apply.
Transform2D t = Transform2D.Identity;
t.X.X = t.Y.Y = Mathf.Cos(rot);
t.X.Y = t.Y.X = Mathf.Sin(rot);
t.Y.X *= -1;
Transform = t; // Change the node's transform to what we calculated.
```

---

## MenuBar

**URL:** https://docs.godotengine.org/en/stable/classes/class_menubar.html

**Contents:**
- MenuBar
- Description
- Properties
- Methods
- Theme Properties
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions
- User-contributed notes

Inherits: Control < CanvasItem < Node < Object

A horizontal menu bar that creates a menu for each PopupMenu child.

A horizontal menu bar that creates a menu for each PopupMenu child. New items are created by adding PopupMenus to this node. Item title is determined by Window.title, or node name if Window.title is empty. Item title can be overridden using set_menu_title().

3 (overrides Control)

get_menu_count() const

get_menu_popup(menu: int) const

get_menu_title(menu: int) const

get_menu_tooltip(menu: int) const

is_menu_disabled(menu: int) const

is_menu_hidden(menu: int) const

is_native_menu() const

set_disable_shortcuts(disabled: bool)

set_menu_disabled(menu: int, disabled: bool)

set_menu_hidden(menu: int, hidden: bool)

set_menu_title(menu: int, title: String)

set_menu_tooltip(menu: int, tooltip: String)

Color(0.875, 0.875, 0.875, 1)

Color(0.875, 0.875, 0.875, 0.5)

Color(0.95, 0.95, 0.95, 1)

Color(0.95, 0.95, 0.95, 1)

font_hover_pressed_color

hover_pressed_mirrored

void set_flat(value: bool)

Flat MenuBar don't display item decoration.

String language = "" 🔗

void set_language(value: String)

String get_language()

Language code used for line-breaking and text shaping algorithms, if left empty current locale is used instead.

bool prefer_global_menu = true 🔗

void set_prefer_global_menu(value: bool)

bool is_prefer_global_menu()

If true, MenuBar will use system global menu when supported.

Note: If true and global menu is supported, this node is not displayed, has zero size, and all its child nodes except PopupMenus are inaccessible.

Note: This property overrides the value of the PopupMenu.prefer_native_menu property of the child nodes.

int start_index = -1 🔗

void set_start_index(value: int)

int get_start_index()

Position order in the global menu to insert MenuBar items at. All menu items in the MenuBar are always inserted as a continuous range. Menus with lower start_index are inserted first. Menus with start_index equal to -1 are inserted last.

bool switch_on_hover = true 🔗

void set_switch_on_hover(value: bool)

bool is_switch_on_hover()

If true, when the cursor hovers above menu item, it will close the current PopupMenu and open the other one.

TextDirection text_direction = 0 🔗

void set_text_direction(value: TextDirection)

TextDirection get_text_direction()

Base text writing direction.

int get_menu_count() const 🔗

Returns number of menu items.

PopupMenu get_menu_popup(menu: int) const 🔗

Returns PopupMenu associated with menu item.

String get_menu_title(menu: int) const 🔗

Returns menu item title.

String get_menu_tooltip(menu: int) const 🔗

Returns menu item tooltip.

bool is_menu_disabled(menu: int) const 🔗

Returns true, if menu item is disabled.

bool is_menu_hidden(menu: int) const 🔗

Returns true, if menu item is hidden.

bool is_native_menu() const 🔗

Returns true, if system global menu is supported and used by this MenuBar.

void set_disable_shortcuts(disabled: bool) 🔗

If true, shortcuts are disabled and cannot be used to trigger the button.

void set_menu_disabled(menu: int, disabled: bool) 🔗

If true, menu item is disabled.

void set_menu_hidden(menu: int, hidden: bool) 🔗

If true, menu item is hidden.

void set_menu_title(menu: int, title: String) 🔗

Sets menu item title.

void set_menu_tooltip(menu: int, tooltip: String) 🔗

Sets menu item tooltip.

Color font_color = Color(0.875, 0.875, 0.875, 1) 🔗

Default text Color of the menu item.

Color font_disabled_color = Color(0.875, 0.875, 0.875, 0.5) 🔗

Text Color used when the menu item is disabled.

Color font_focus_color = Color(0.95, 0.95, 0.95, 1) 🔗

Text Color used when the menu item is focused. Only replaces the normal text color of the menu item. Disabled, hovered, and pressed states take precedence over this color.

Color font_hover_color = Color(0.95, 0.95, 0.95, 1) 🔗

Text Color used when the menu item is being hovered.

Color font_hover_pressed_color = Color(1, 1, 1, 1) 🔗

Text Color used when the menu item is being hovered and pressed.

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The tint of text outline of the menu item.

Color font_pressed_color = Color(1, 1, 1, 1) 🔗

Text Color used when the menu item is being pressed.

int h_separation = 4 🔗

The horizontal space between menu items.

int outline_size = 0 🔗

The size of the text outline.

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

Font of the menu item's text.

Font size of the menu item's text.

StyleBox used when the menu item is disabled.

StyleBox disabled_mirrored 🔗

StyleBox used when the menu item is disabled (for right-to-left layouts).

StyleBox used when the menu item is being hovered.

StyleBox hover_mirrored 🔗

StyleBox used when the menu item is being hovered (for right-to-left layouts).

StyleBox hover_pressed 🔗

StyleBox used when the menu item is being pressed and hovered at the same time.

StyleBox hover_pressed_mirrored 🔗

StyleBox used when the menu item is being pressed and hovered at the same time (for right-to-left layouts).

Default StyleBox for the menu item.

StyleBox normal_mirrored 🔗

Default StyleBox for the menu item (for right-to-left layouts).

StyleBox used when the menu item is being pressed.

StyleBox pressed_mirrored 🔗

StyleBox used when the menu item is being pressed (for right-to-left layouts).

Please read the User-contributed notes policy before submitting a comment.

---

## MovieWriter

**URL:** https://docs.godotengine.org/en/stable/classes/class_moviewriter.html

**Contents:**
- MovieWriter
- Description
- Methods
- Method Descriptions
- User-contributed notes

Abstract class for non-real-time video recording encoders.

Godot can record videos with non-real-time simulation. Like the --fixed-fps command line argument, this forces the reported delta in Node._process() functions to be identical across frames, regardless of how long it actually took to render the frame. This can be used to record high-quality videos with perfect frame pacing regardless of your hardware's capabilities.

Godot has 3 built-in MovieWriters:

OGV container with Theora for video and Vorbis for audio (.ogv file extension). Lossy compression, medium file sizes, fast encoding. The lossy compression quality can be adjusted by changing ProjectSettings.editor/movie_writer/video_quality and ProjectSettings.editor/movie_writer/ogv/audio_quality. The resulting file can be viewed in Godot with VideoStreamPlayer and most video players, but not web browsers as they don't support Theora.

AVI container with MJPEG for video and uncompressed audio (.avi file extension). Lossy compression, medium file sizes, fast encoding. The lossy compression quality can be adjusted by changing ProjectSettings.editor/movie_writer/video_quality. The resulting file can be viewed in most video players, but it must be converted to another format for viewing on the web or by Godot with VideoStreamPlayer. MJPEG does not support transparency. AVI output is currently limited to a file of 4 GB in size at most.

PNG image sequence for video and WAV for audio (.png file extension). Lossless compression, large file sizes, slow encoding. Designed to be encoded to a video file with another tool such as FFmpeg after recording. Transparency is currently not supported, even if the root viewport is set to be transparent.

If you need to encode to a different format or pipe a stream through third-party software, you can extend the MovieWriter class to create your own movie writers. This should typically be done using GDExtension for performance reasons.

Editor usage: A default movie file path can be specified in ProjectSettings.editor/movie_writer/movie_file. Alternatively, for running single scenes, a movie_file metadata can be added to the root node, specifying the path to a movie file that will be used when recording that scene. Once a path is set, click the video reel icon in the top-right corner of the editor to enable Movie Maker mode, then run any scene as usual. The engine will start recording as soon as the splash screen is finished, and it will only stop recording when the engine quits. Click the video reel icon again to disable Movie Maker mode. Note that toggling Movie Maker mode does not affect project instances that are already running.

Note: MovieWriter is available for use in both the editor and exported projects, but it is not designed for use by end users to record videos while playing. Players wishing to record gameplay videos should install tools such as OBS Studio or SimpleScreenRecorder instead.

Note: MJPEG support (.avi file extension) depends on the jpg module being enabled at compile time (default behavior).

Note: OGV support (.ogv file extension) depends on the theora module being enabled at compile time (default behavior). Theora compression is only available in editor binaries.

_get_audio_mix_rate() virtual required const

_get_audio_speaker_mode() virtual required const

_handles_file(path: String) virtual required const

_write_begin(movie_size: Vector2i, fps: int, base_path: String) virtual required

_write_end() virtual required

_write_frame(frame_image: Image, audio_frame_block: const void*) virtual required

add_writer(writer: MovieWriter) static

int _get_audio_mix_rate() virtual required const 🔗

Called when the audio sample rate used for recording the audio is requested by the engine. The value returned must be specified in Hz. Defaults to 48000 Hz if _get_audio_mix_rate() is not overridden.

SpeakerMode _get_audio_speaker_mode() virtual required const 🔗

Called when the audio speaker mode used for recording the audio is requested by the engine. This can affect the number of output channels in the resulting audio file/stream. Defaults to AudioServer.SPEAKER_MODE_STEREO if _get_audio_speaker_mode() is not overridden.

bool _handles_file(path: String) virtual required const 🔗

Called when the engine determines whether this MovieWriter is able to handle the file at path. Must return true if this MovieWriter is able to handle the given file path, false otherwise. Typically, _handles_file() is overridden as follows to allow the user to record a file at any path with a given file extension:

Error _write_begin(movie_size: Vector2i, fps: int, base_path: String) virtual required 🔗

Called once before the engine starts writing video and audio data. movie_size is the width and height of the video to save. fps is the number of frames per second specified in the project settings or using the --fixed-fps <fps> command line argument.

void _write_end() virtual required 🔗

Called when the engine finishes writing. This occurs when the engine quits by pressing the window manager's close button, or when SceneTree.quit() is called.

Note: Pressing Ctrl + C on the terminal running the editor/project does not result in _write_end() being called.

Error _write_frame(frame_image: Image, audio_frame_block: const void*) virtual required 🔗

Called at the end of every rendered frame. The frame_image and audio_frame_block function arguments should be written to.

void add_writer(writer: MovieWriter) static 🔗

Adds a writer to be usable by the engine. The supported file extensions can be set by overriding _handles_file().

Note: add_writer() must be called early enough in the engine initialization to work, as movie writing is designed to start at the same time as the rest of the engine.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (go):
```go
func _handles_file(path):
    # Allows specifying an output file with a `.mkv` file extension (case-insensitive),
    # either in the Project Settings or with the `--write-movie <path>` command line argument.
    return path.get_extension().to_lower() == "mkv"
```

---

## NativeMenu

**URL:** https://docs.godotengine.org/en/stable/classes/class_nativemenu.html

**Contents:**
- NativeMenu
- Description
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

A server interface for OS native menus.

NativeMenu handles low-level access to the OS native global menu bar and popup menus.

Note: This is low-level API, consider using MenuBar with MenuBar.prefer_global_menu set to true, and PopupMenu with PopupMenu.prefer_native_menu set to true.

To create a menu, use create_menu(), add menu items using add_*_item methods. To remove a menu, use free_menu().

add_check_item(rid: RID, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1)

add_icon_check_item(rid: RID, icon: Texture2D, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1)

add_icon_item(rid: RID, icon: Texture2D, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1)

add_icon_radio_check_item(rid: RID, icon: Texture2D, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1)

add_item(rid: RID, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1)

add_multistate_item(rid: RID, label: String, max_states: int, default_state: int, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1)

add_radio_check_item(rid: RID, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1)

add_separator(rid: RID, index: int = -1)

add_submenu_item(rid: RID, label: String, submenu_rid: RID, tag: Variant = null, index: int = -1)

find_item_index_with_submenu(rid: RID, submenu_rid: RID) const

find_item_index_with_tag(rid: RID, tag: Variant) const

find_item_index_with_text(rid: RID, text: String) const

get_item_accelerator(rid: RID, idx: int) const

get_item_callback(rid: RID, idx: int) const

get_item_count(rid: RID) const

get_item_icon(rid: RID, idx: int) const

get_item_indentation_level(rid: RID, idx: int) const

get_item_key_callback(rid: RID, idx: int) const

get_item_max_states(rid: RID, idx: int) const

get_item_state(rid: RID, idx: int) const

get_item_submenu(rid: RID, idx: int) const

get_item_tag(rid: RID, idx: int) const

get_item_text(rid: RID, idx: int) const

get_item_tooltip(rid: RID, idx: int) const

get_minimum_width(rid: RID) const

get_popup_close_callback(rid: RID) const

get_popup_open_callback(rid: RID) const

get_size(rid: RID) const

get_system_menu(menu_id: SystemMenus) const

get_system_menu_name(menu_id: SystemMenus) const

has_feature(feature: Feature) const

has_menu(rid: RID) const

has_system_menu(menu_id: SystemMenus) const

is_item_checkable(rid: RID, idx: int) const

is_item_checked(rid: RID, idx: int) const

is_item_disabled(rid: RID, idx: int) const

is_item_hidden(rid: RID, idx: int) const

is_item_radio_checkable(rid: RID, idx: int) const

is_opened(rid: RID) const

is_system_menu(rid: RID) const

popup(rid: RID, position: Vector2i)

remove_item(rid: RID, idx: int)

set_interface_direction(rid: RID, is_rtl: bool)

set_item_accelerator(rid: RID, idx: int, keycode: Key)

set_item_callback(rid: RID, idx: int, callback: Callable)

set_item_checkable(rid: RID, idx: int, checkable: bool)

set_item_checked(rid: RID, idx: int, checked: bool)

set_item_disabled(rid: RID, idx: int, disabled: bool)

set_item_hidden(rid: RID, idx: int, hidden: bool)

set_item_hover_callbacks(rid: RID, idx: int, callback: Callable)

set_item_icon(rid: RID, idx: int, icon: Texture2D)

set_item_indentation_level(rid: RID, idx: int, level: int)

set_item_key_callback(rid: RID, idx: int, key_callback: Callable)

set_item_max_states(rid: RID, idx: int, max_states: int)

set_item_radio_checkable(rid: RID, idx: int, checkable: bool)

set_item_state(rid: RID, idx: int, state: int)

set_item_submenu(rid: RID, idx: int, submenu_rid: RID)

set_item_tag(rid: RID, idx: int, tag: Variant)

set_item_text(rid: RID, idx: int, text: String)

set_item_tooltip(rid: RID, idx: int, tooltip: String)

set_minimum_width(rid: RID, width: float)

set_popup_close_callback(rid: RID, callback: Callable)

set_popup_open_callback(rid: RID, callback: Callable)

Feature FEATURE_GLOBAL_MENU = 0

NativeMenu supports native global main menu.

Feature FEATURE_POPUP_MENU = 1

NativeMenu supports native popup menus.

Feature FEATURE_OPEN_CLOSE_CALLBACK = 2

NativeMenu supports menu open and close callbacks.

Feature FEATURE_HOVER_CALLBACK = 3

NativeMenu supports menu item hover callback.

Feature FEATURE_KEY_CALLBACK = 4

NativeMenu supports menu item accelerator/key callback.

SystemMenus INVALID_MENU_ID = 0

Invalid special system menu ID.

SystemMenus MAIN_MENU_ID = 1

SystemMenus APPLICATION_MENU_ID = 2

Application (first menu after "Apple" menu on macOS) menu ID.

SystemMenus WINDOW_MENU_ID = 3

"Window" menu ID (on macOS this menu includes standard window control items and a list of open windows).

SystemMenus HELP_MENU_ID = 4

"Help" menu ID (on macOS this menu includes help search bar).

SystemMenus DOCK_MENU_ID = 5

Dock icon right-click menu ID (on macOS this menu include standard application control items and a list of open windows).

int add_check_item(rid: RID, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1) 🔗

Adds a new checkable item with text label to the global menu rid.

Returns index of the inserted item, it's not guaranteed to be the same as index value.

An accelerator can optionally be defined, which is a keyboard shortcut that can be pressed to trigger the menu button even if it's not currently open. The accelerator is generally a combination of KeyModifierMasks and Keys using bitwise OR such as KEY_MASK_CTRL | KEY_A (Ctrl + A).

Note: The callback and key_callback Callables need to accept exactly one Variant parameter, the parameter passed to the Callables will be the value passed to tag.

Note: This method is implemented on macOS and Windows.

Note: On Windows, accelerator and key_callback are ignored.

int add_icon_check_item(rid: RID, icon: Texture2D, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1) 🔗

Adds a new checkable item with text label and icon icon to the global menu rid.

Returns index of the inserted item, it's not guaranteed to be the same as index value.

An accelerator can optionally be defined, which is a keyboard shortcut that can be pressed to trigger the menu button even if it's not currently open. The accelerator is generally a combination of KeyModifierMasks and Keys using bitwise OR such as KEY_MASK_CTRL | KEY_A (Ctrl + A).

Note: The callback and key_callback Callables need to accept exactly one Variant parameter, the parameter passed to the Callables will be the value passed to tag.

Note: This method is implemented on macOS and Windows.

Note: On Windows, accelerator and key_callback are ignored.

int add_icon_item(rid: RID, icon: Texture2D, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1) 🔗

Adds a new item with text label and icon icon to the global menu rid.

Returns index of the inserted item, it's not guaranteed to be the same as index value.

An accelerator can optionally be defined, which is a keyboard shortcut that can be pressed to trigger the menu button even if it's not currently open. The accelerator is generally a combination of KeyModifierMasks and Keys using bitwise OR such as KEY_MASK_CTRL | KEY_A (Ctrl + A).

Note: The callback and key_callback Callables need to accept exactly one Variant parameter, the parameter passed to the Callables will be the value passed to tag.

Note: This method is implemented on macOS and Windows.

Note: On Windows, accelerator and key_callback are ignored.

int add_icon_radio_check_item(rid: RID, icon: Texture2D, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1) 🔗

Adds a new radio-checkable item with text label and icon icon to the global menu rid.

Returns index of the inserted item, it's not guaranteed to be the same as index value.

An accelerator can optionally be defined, which is a keyboard shortcut that can be pressed to trigger the menu button even if it's not currently open. The accelerator is generally a combination of KeyModifierMasks and Keys using bitwise OR such as KEY_MASK_CTRL | KEY_A (Ctrl + A).

Note: Radio-checkable items just display a checkmark, but don't have any built-in checking behavior and must be checked/unchecked manually. See set_item_checked() for more info on how to control it.

Note: The callback and key_callback Callables need to accept exactly one Variant parameter, the parameter passed to the Callables will be the value passed to tag.

Note: This method is implemented on macOS and Windows.

Note: On Windows, accelerator and key_callback are ignored.

int add_item(rid: RID, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1) 🔗

Adds a new item with text label to the global menu rid.

Returns index of the inserted item, it's not guaranteed to be the same as index value.

An accelerator can optionally be defined, which is a keyboard shortcut that can be pressed to trigger the menu button even if it's not currently open. The accelerator is generally a combination of KeyModifierMasks and Keys using bitwise OR such as KEY_MASK_CTRL | KEY_A (Ctrl + A).

Note: The callback and key_callback Callables need to accept exactly one Variant parameter, the parameter passed to the Callables will be the value passed to tag.

Note: This method is implemented on macOS and Windows.

Note: On Windows, accelerator and key_callback are ignored.

int add_multistate_item(rid: RID, label: String, max_states: int, default_state: int, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1) 🔗

Adds a new item with text label to the global menu rid.

Contrarily to normal binary items, multistate items can have more than two states, as defined by max_states. Each press or activate of the item will increase the state by one. The default value is defined by default_state.

Returns index of the inserted item, it's not guaranteed to be the same as index value.

An accelerator can optionally be defined, which is a keyboard shortcut that can be pressed to trigger the menu button even if it's not currently open. The accelerator is generally a combination of KeyModifierMasks and Keys using bitwise OR such as KEY_MASK_CTRL | KEY_A (Ctrl + A).

Note: By default, there's no indication of the current item state, it should be changed manually.

Note: The callback and key_callback Callables need to accept exactly one Variant parameter, the parameter passed to the Callables will be the value passed to tag.

Note: This method is implemented on macOS and Windows.

Note: On Windows, accelerator and key_callback are ignored.

int add_radio_check_item(rid: RID, label: String, callback: Callable = Callable(), key_callback: Callable = Callable(), tag: Variant = null, accelerator: Key = 0, index: int = -1) 🔗

Adds a new radio-checkable item with text label to the global menu rid.

Returns index of the inserted item, it's not guaranteed to be the same as index value.

An accelerator can optionally be defined, which is a keyboard shortcut that can be pressed to trigger the menu button even if it's not currently open. The accelerator is generally a combination of KeyModifierMasks and Keys using bitwise OR such as KEY_MASK_CTRL | KEY_A (Ctrl + A).

Note: Radio-checkable items just display a checkmark, but don't have any built-in checking behavior and must be checked/unchecked manually. See set_item_checked() for more info on how to control it.

Note: The callback and key_callback Callables need to accept exactly one Variant parameter, the parameter passed to the Callables will be the value passed to tag.

Note: This method is implemented on macOS and Windows.

Note: On Windows, accelerator and key_callback are ignored.

int add_separator(rid: RID, index: int = -1) 🔗

Adds a separator between items to the global menu rid. Separators also occupy an index.

Returns index of the inserted item, it's not guaranteed to be the same as index value.

Note: This method is implemented on macOS and Windows.

int add_submenu_item(rid: RID, label: String, submenu_rid: RID, tag: Variant = null, index: int = -1) 🔗

Adds an item that will act as a submenu of the global menu rid. The submenu_rid argument is the RID of the global menu that will be shown when the item is clicked.

Returns index of the inserted item, it's not guaranteed to be the same as index value.

Note: This method is implemented on macOS and Windows.

void clear(rid: RID) 🔗

Removes all items from the global menu rid.

Note: This method is implemented on macOS and Windows.

Creates a new global menu object.

Note: This method is implemented on macOS and Windows.

int find_item_index_with_submenu(rid: RID, submenu_rid: RID) const 🔗

Returns the index of the item with the submenu specified by submenu_rid. Indices are automatically assigned to each item by the engine, and cannot be set manually.

Note: This method is implemented on macOS and Windows.

int find_item_index_with_tag(rid: RID, tag: Variant) const 🔗

Returns the index of the item with the specified tag. Indices are automatically assigned to each item by the engine, and cannot be set manually.

Note: This method is implemented on macOS and Windows.

int find_item_index_with_text(rid: RID, text: String) const 🔗

Returns the index of the item with the specified text. Indices are automatically assigned to each item by the engine, and cannot be set manually.

Note: This method is implemented on macOS and Windows.

void free_menu(rid: RID) 🔗

Frees a global menu object created by this NativeMenu.

Note: This method is implemented on macOS and Windows.

Key get_item_accelerator(rid: RID, idx: int) const 🔗

Returns the accelerator of the item at index idx. Accelerators are special combinations of keys that activate the item, no matter which control is focused.

Note: This method is implemented only on macOS.

Callable get_item_callback(rid: RID, idx: int) const 🔗

Returns the callback of the item at index idx.

Note: This method is implemented on macOS and Windows.

int get_item_count(rid: RID) const 🔗

Returns number of items in the global menu rid.

Note: This method is implemented on macOS and Windows.

Texture2D get_item_icon(rid: RID, idx: int) const 🔗

Returns the icon of the item at index idx.

Note: This method is implemented on macOS and Windows.

int get_item_indentation_level(rid: RID, idx: int) const 🔗

Returns the horizontal offset of the item at the given idx.

Note: This method is implemented only on macOS.

Callable get_item_key_callback(rid: RID, idx: int) const 🔗

Returns the callback of the item accelerator at index idx.

Note: This method is implemented only on macOS.

int get_item_max_states(rid: RID, idx: int) const 🔗

Returns number of states of a multistate item. See add_multistate_item() for details.

Note: This method is implemented on macOS and Windows.

int get_item_state(rid: RID, idx: int) const 🔗

Returns the state of a multistate item. See add_multistate_item() for details.

Note: This method is implemented on macOS and Windows.

RID get_item_submenu(rid: RID, idx: int) const 🔗

Returns the submenu ID of the item at index idx. See add_submenu_item() for more info on how to add a submenu.

Note: This method is implemented on macOS and Windows.

Variant get_item_tag(rid: RID, idx: int) const 🔗

Returns the metadata of the specified item, which might be of any type. You can set it with set_item_tag(), which provides a simple way of assigning context data to items.

Note: This method is implemented on macOS and Windows.

String get_item_text(rid: RID, idx: int) const 🔗

Returns the text of the item at index idx.

Note: This method is implemented on macOS and Windows.

String get_item_tooltip(rid: RID, idx: int) const 🔗

Returns the tooltip associated with the specified index idx.

Note: This method is implemented only on macOS.

float get_minimum_width(rid: RID) const 🔗

Returns global menu minimum width.

Note: This method is implemented only on macOS.

Callable get_popup_close_callback(rid: RID) const 🔗

Returns global menu close callback.

Note: This method is implemented on macOS and Windows.

Callable get_popup_open_callback(rid: RID) const 🔗

Returns global menu open callback.

Note: This method is implemented only on macOS.

Vector2 get_size(rid: RID) const 🔗

Returns global menu size.

Note: This method is implemented on macOS and Windows.

RID get_system_menu(menu_id: SystemMenus) const 🔗

Returns RID of a special system menu.

Note: This method is implemented only on macOS.

String get_system_menu_name(menu_id: SystemMenus) const 🔗

Returns readable name of a special system menu.

Note: This method is implemented only on macOS.

bool has_feature(feature: Feature) const 🔗

Returns true if the specified feature is supported by the current NativeMenu, false otherwise.

Note: This method is implemented on macOS and Windows.

bool has_menu(rid: RID) const 🔗

Returns true if rid is valid global menu.

Note: This method is implemented on macOS and Windows.

bool has_system_menu(menu_id: SystemMenus) const 🔗

Returns true if a special system menu is supported.

Note: This method is implemented only on macOS.

bool is_item_checkable(rid: RID, idx: int) const 🔗

Returns true if the item at index idx is checkable in some way, i.e. if it has a checkbox or radio button.

Note: This method is implemented on macOS and Windows.

bool is_item_checked(rid: RID, idx: int) const 🔗

Returns true if the item at index idx is checked.

Note: This method is implemented on macOS and Windows.

bool is_item_disabled(rid: RID, idx: int) const 🔗

Returns true if the item at index idx is disabled. When it is disabled it can't be selected, or its action invoked.

See set_item_disabled() for more info on how to disable an item.

Note: This method is implemented on macOS and Windows.

bool is_item_hidden(rid: RID, idx: int) const 🔗

Returns true if the item at index idx is hidden.

See set_item_hidden() for more info on how to hide an item.

Note: This method is implemented only on macOS.

bool is_item_radio_checkable(rid: RID, idx: int) const 🔗

Returns true if the item at index idx has radio button-style checkability.

Note: This is purely cosmetic; you must add the logic for checking/unchecking items in radio groups.

Note: This method is implemented on macOS and Windows.

bool is_opened(rid: RID) const 🔗

Returns true if the menu is currently opened.

Note: This method is implemented only on macOS.

bool is_system_menu(rid: RID) const 🔗

Return true is global menu is a special system menu.

Note: This method is implemented only on macOS.

void popup(rid: RID, position: Vector2i) 🔗

Shows the global menu at position in the screen coordinates.

Note: This method is implemented on macOS and Windows.

void remove_item(rid: RID, idx: int) 🔗

Removes the item at index idx from the global menu rid.

Note: The indices of items after the removed item will be shifted by one.

Note: This method is implemented on macOS and Windows.

void set_interface_direction(rid: RID, is_rtl: bool) 🔗

Sets the menu text layout direction from right-to-left if is_rtl is true.

Note: This method is implemented on macOS and Windows.

void set_item_accelerator(rid: RID, idx: int, keycode: Key) 🔗

Sets the accelerator of the item at index idx. keycode can be a single Key, or a combination of KeyModifierMasks and Keys using bitwise OR such as KEY_MASK_CTRL | KEY_A (Ctrl + A).

Note: This method is implemented only on macOS.

void set_item_callback(rid: RID, idx: int, callback: Callable) 🔗

Sets the callback of the item at index idx. Callback is emitted when an item is pressed.

Note: The callback Callable needs to accept exactly one Variant parameter, the parameter passed to the Callable will be the value passed to the tag parameter when the menu item was created.

Note: This method is implemented on macOS and Windows.

void set_item_checkable(rid: RID, idx: int, checkable: bool) 🔗

Sets whether the item at index idx has a checkbox. If false, sets the type of the item to plain text.

Note: This method is implemented on macOS and Windows.

void set_item_checked(rid: RID, idx: int, checked: bool) 🔗

Sets the checkstate status of the item at index idx.

Note: This method is implemented on macOS and Windows.

void set_item_disabled(rid: RID, idx: int, disabled: bool) 🔗

Enables/disables the item at index idx. When it is disabled, it can't be selected and its action can't be invoked.

Note: This method is implemented on macOS and Windows.

void set_item_hidden(rid: RID, idx: int, hidden: bool) 🔗

Hides/shows the item at index idx. When it is hidden, an item does not appear in a menu and its action cannot be invoked.

Note: This method is implemented only on macOS.

void set_item_hover_callbacks(rid: RID, idx: int, callback: Callable) 🔗

Sets the callback of the item at index idx. The callback is emitted when an item is hovered.

Note: The callback Callable needs to accept exactly one Variant parameter, the parameter passed to the Callable will be the value passed to the tag parameter when the menu item was created.

Note: This method is implemented only on macOS.

void set_item_icon(rid: RID, idx: int, icon: Texture2D) 🔗

Replaces the Texture2D icon of the specified idx.

Note: This method is implemented on macOS and Windows.

Note: This method is not supported by macOS Dock menu items.

void set_item_indentation_level(rid: RID, idx: int, level: int) 🔗

Sets the horizontal offset of the item at the given idx.

Note: This method is implemented only on macOS.

void set_item_key_callback(rid: RID, idx: int, key_callback: Callable) 🔗

Sets the callback of the item at index idx. Callback is emitted when its accelerator is activated.

Note: The key_callback Callable needs to accept exactly one Variant parameter, the parameter passed to the Callable will be the value passed to the tag parameter when the menu item was created.

Note: This method is implemented only on macOS.

void set_item_max_states(rid: RID, idx: int, max_states: int) 🔗

Sets number of state of a multistate item. See add_multistate_item() for details.

Note: This method is implemented on macOS and Windows.

void set_item_radio_checkable(rid: RID, idx: int, checkable: bool) 🔗

Sets the type of the item at the specified index idx to radio button. If false, sets the type of the item to plain text.

Note: This is purely cosmetic; you must add the logic for checking/unchecking items in radio groups.

Note: This method is implemented on macOS and Windows.

void set_item_state(rid: RID, idx: int, state: int) 🔗

Sets the state of a multistate item. See add_multistate_item() for details.

Note: This method is implemented on macOS and Windows.

void set_item_submenu(rid: RID, idx: int, submenu_rid: RID) 🔗

Sets the submenu RID of the item at index idx. The submenu is a global menu that would be shown when the item is clicked.

Note: This method is implemented on macOS and Windows.

void set_item_tag(rid: RID, idx: int, tag: Variant) 🔗

Sets the metadata of an item, which may be of any type. You can later get it with get_item_tag(), which provides a simple way of assigning context data to items.

Note: This method is implemented on macOS and Windows.

void set_item_text(rid: RID, idx: int, text: String) 🔗

Sets the text of the item at index idx.

Note: This method is implemented on macOS and Windows.

void set_item_tooltip(rid: RID, idx: int, tooltip: String) 🔗

Sets the String tooltip of the item at the specified index idx.

Note: This method is implemented only on macOS.

void set_minimum_width(rid: RID, width: float) 🔗

Sets the minimum width of the global menu.

Note: This method is implemented only on macOS.

void set_popup_close_callback(rid: RID, callback: Callable) 🔗

Registers callable to emit when the menu is about to show.

Note: The OS can simulate menu opening to track menu item changes and global shortcuts, in which case the corresponding close callback is not triggered. Use is_opened() to check if the menu is currently opened.

Note: This method is implemented on macOS and Windows.

void set_popup_open_callback(rid: RID, callback: Callable) 🔗

Registers callable to emit after the menu is closed.

Note: This method is implemented only on macOS.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (typescript):
```typescript
var menu

func _menu_callback(item_id):
    if item_id == "ITEM_CUT":
        cut()
    elif item_id == "ITEM_COPY":
        copy()
    elif item_id == "ITEM_PASTE":
        paste()

func _enter_tree():
    # Create new menu and add items:
    menu = NativeMenu.create_menu()
    NativeMenu.add_item(menu, "Cut", _menu_callback, Callable(), "ITEM_CUT")
    NativeMenu.add_item(menu, "Copy", _menu_callback, Callable(), "ITEM_COPY")
    NativeMenu.add_separator(menu)
    NativeMenu.add_item(menu, "Paste", _menu_callback, Callable(), "ITEM_PASTE")

func _on_button_pressed():
    # Show popup menu at mouse position:
    NativeMenu.popup(menu, DisplayServer.mouse_get_position())

func _exit_tree():
    # Remove menu when it's no longer needed:
    NativeMenu.free_menu(menu)
```

---

## OpenXRCompositionLayerEquirect

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrcompositionlayerequirect.html

**Contents:**
- OpenXRCompositionLayerEquirect
- Description
- Properties
- Property Descriptions
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: OpenXRCompositionLayer < Node3D < Node < Object

An OpenXR composition layer that is rendered as an internal slice of a sphere.

An OpenXR composition layer that allows rendering a SubViewport on an internal slice of a sphere.

central_horizontal_angle

float central_horizontal_angle = 1.5707964 🔗

void set_central_horizontal_angle(value: float)

float get_central_horizontal_angle()

The central horizontal angle of the sphere. Used to set the width.

int fallback_segments = 10 🔗

void set_fallback_segments(value: int)

int get_fallback_segments()

The number of segments to use in the fallback mesh.

float lower_vertical_angle = 0.7853982 🔗

void set_lower_vertical_angle(value: float)

float get_lower_vertical_angle()

The lower vertical angle of the sphere. Used (together with upper_vertical_angle) to set the height.

void set_radius(value: float)

The radius of the sphere.

float upper_vertical_angle = 0.7853982 🔗

void set_upper_vertical_angle(value: float)

float get_upper_vertical_angle()

The upper vertical angle of the sphere. Used (together with lower_vertical_angle) to set the height.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRIPBinding

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxripbinding.html

**Contents:**
- OpenXRIPBinding
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Defines a binding between an OpenXRAction and an XR input or output.

This binding resource binds an OpenXRAction to an input or output. As most controllers have left hand and right versions that are handled by the same interaction profile we can specify multiple bindings. For instance an action "Fire" could be bound to both "/user/hand/left/input/trigger" and "/user/hand/right/input/trigger". This would require two binding entries.

add_path(path: String)

OpenXRActionBindingModifier

get_binding_modifier(index: int) const

get_binding_modifier_count() const

get_path_count() const

has_path(path: String) const

remove_path(path: String)

OpenXRAction action 🔗

void set_action(value: OpenXRAction)

OpenXRAction get_action()

OpenXRAction that is bound to binding_path.

Array binding_modifiers = [] 🔗

void set_binding_modifiers(value: Array)

Array get_binding_modifiers()

Binding modifiers for this binding.

String binding_path = "" 🔗

void set_binding_path(value: String)

String get_binding_path()

Binding path that defines the input or output bound to action.

Note: Binding paths are suggestions, an XR runtime may choose to bind the action to a different input or output emulating this input or output.

PackedStringArray paths 🔗

void set_paths(value: PackedStringArray)

PackedStringArray get_paths()

Deprecated: Use binding_path instead.

Paths that define the inputs or outputs bound on the device.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedStringArray for more details.

void add_path(path: String) 🔗

Deprecated: Binding is for a single path.

Add an input/output path to this binding.

OpenXRActionBindingModifier get_binding_modifier(index: int) const 🔗

Get the OpenXRBindingModifier at this index.

int get_binding_modifier_count() const 🔗

Get the number of binding modifiers for this binding.

int get_path_count() const 🔗

Deprecated: Binding is for a single path.

Get the number of input/output paths in this binding.

bool has_path(path: String) const 🔗

Deprecated: Binding is for a single path.

Returns true if this input/output path is part of this binding.

void remove_path(path: String) 🔗

Deprecated: Binding is for a single path.

Removes this input/output path from this binding.

Please read the User-contributed notes policy before submitting a comment.

---

## OptionButton

**URL:** https://docs.godotengine.org/en/stable/classes/class_optionbutton.html

**Contents:**
- OptionButton
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions
- User-contributed notes

Inherits: Button < BaseButton < Control < CanvasItem < Node < Object

A button that brings up a dropdown with selectable options when pressed.

OptionButton is a type of button that brings up a dropdown with selectable items when pressed. The item selected becomes the "current" item and is displayed as the button text.

See also BaseButton which contains common properties and methods associated with this node.

Note: The IDs used for items are limited to signed 32-bit integers, not the full 64 bits of int. These have a range of -2^31 to 2^31 - 1, that is, -2147483648 to 2147483647.

Note: The Button.text and Button.icon properties are set automatically based on the selected item. They shouldn't be changed manually.

0 (overrides BaseButton)

true (overrides BaseButton)

add_icon_item(texture: Texture2D, label: String, id: int = -1)

add_item(label: String, id: int = -1)

add_separator(text: String = "")

get_item_auto_translate_mode(idx: int) const

get_item_icon(idx: int) const

get_item_id(idx: int) const

get_item_index(id: int) const

get_item_metadata(idx: int) const

get_item_text(idx: int) const

get_item_tooltip(idx: int) const

get_selectable_item(from_last: bool = false) const

get_selected_id() const

get_selected_metadata() const

has_selectable_items() const

is_item_disabled(idx: int) const

is_item_separator(idx: int) const

remove_item(idx: int)

set_disable_shortcuts(disabled: bool)

set_item_auto_translate_mode(idx: int, mode: AutoTranslateMode)

set_item_disabled(idx: int, disabled: bool)

set_item_icon(idx: int, texture: Texture2D)

set_item_id(idx: int, id: int)

set_item_metadata(idx: int, metadata: Variant)

set_item_text(idx: int, text: String)

set_item_tooltip(idx: int, tooltip: String)

item_focused(index: int) 🔗

Emitted when the user navigates to an item using the ProjectSettings.input/ui_up or ProjectSettings.input/ui_down input actions. The index of the item selected is passed as argument.

item_selected(index: int) 🔗

Emitted when the current item has been changed by the user. The index of the item selected is passed as argument.

allow_reselect must be enabled to reselect an item.

bool allow_reselect = false 🔗

void set_allow_reselect(value: bool)

bool get_allow_reselect()

If true, the currently selected item can be selected again.

bool fit_to_longest_item = true 🔗

void set_fit_to_longest_item(value: bool)

bool is_fit_to_longest_item()

If true, minimum size will be determined by the longest item's text, instead of the currently selected one's.

Note: For performance reasons, the minimum size doesn't update immediately when adding, removing or modifying items.

void set_item_count(value: int)

The number of items to select from.

The index of the currently selected item, or -1 if no item is selected.

void add_icon_item(texture: Texture2D, label: String, id: int = -1) 🔗

Adds an item, with a texture icon, text label and (optionally) id. If no id is passed, the item index will be used as the item's ID. New items are appended at the end.

Note: The item will be selected if there are no other items.

void add_item(label: String, id: int = -1) 🔗

Adds an item, with text label and (optionally) id. If no id is passed, the item index will be used as the item's ID. New items are appended at the end.

Note: The item will be selected if there are no other items.

void add_separator(text: String = "") 🔗

Adds a separator to the list of items. Separators help to group items, and can optionally be given a text header. A separator also gets an index assigned, and is appended at the end of the item list.

Clears all the items in the OptionButton.

AutoTranslateMode get_item_auto_translate_mode(idx: int) const 🔗

Returns the auto translate mode of the item at index idx.

Texture2D get_item_icon(idx: int) const 🔗

Returns the icon of the item at index idx.

int get_item_id(idx: int) const 🔗

Returns the ID of the item at index idx.

int get_item_index(id: int) const 🔗

Returns the index of the item with the given id.

Variant get_item_metadata(idx: int) const 🔗

Retrieves the metadata of an item. Metadata may be any type and can be used to store extra information about an item, such as an external string ID.

String get_item_text(idx: int) const 🔗

Returns the text of the item at index idx.

String get_item_tooltip(idx: int) const 🔗

Returns the tooltip of the item at index idx.

PopupMenu get_popup() const 🔗

Returns the PopupMenu contained in this button.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their Window.visible property.

int get_selectable_item(from_last: bool = false) const 🔗

Returns the index of the first item which is not disabled, or marked as a separator. If from_last is true, the items will be searched in reverse order.

Returns -1 if no item is found.

int get_selected_id() const 🔗

Returns the ID of the selected item, or -1 if no item is selected.

Variant get_selected_metadata() const 🔗

Gets the metadata of the selected item. Metadata for items can be set using set_item_metadata().

bool has_selectable_items() const 🔗

Returns true if this button contains at least one item which is not disabled, or marked as a separator.

bool is_item_disabled(idx: int) const 🔗

Returns true if the item at index idx is disabled.

bool is_item_separator(idx: int) const 🔗

Returns true if the item at index idx is marked as a separator.

void remove_item(idx: int) 🔗

Removes the item at index idx.

void select(idx: int) 🔗

Selects an item by index and makes it the current item. This will work even if the item is disabled.

Passing -1 as the index deselects any currently selected item.

void set_disable_shortcuts(disabled: bool) 🔗

If true, shortcuts are disabled and cannot be used to trigger the button.

void set_item_auto_translate_mode(idx: int, mode: AutoTranslateMode) 🔗

Sets the auto translate mode of the item at index idx.

Items use Node.AUTO_TRANSLATE_MODE_INHERIT by default, which uses the same auto translate mode as the OptionButton itself.

void set_item_disabled(idx: int, disabled: bool) 🔗

Sets whether the item at index idx is disabled.

Disabled items are drawn differently in the dropdown and are not selectable by the user. If the current selected item is set as disabled, it will remain selected.

void set_item_icon(idx: int, texture: Texture2D) 🔗

Sets the icon of the item at index idx.

void set_item_id(idx: int, id: int) 🔗

Sets the ID of the item at index idx.

void set_item_metadata(idx: int, metadata: Variant) 🔗

Sets the metadata of an item. Metadata may be of any type and can be used to store extra information about an item, such as an external string ID.

void set_item_text(idx: int, text: String) 🔗

Sets the text of the item at index idx.

void set_item_tooltip(idx: int, tooltip: String) 🔗

Sets the tooltip of the item at index idx.

Adjusts popup position and sizing for the OptionButton, then shows the PopupMenu. Prefer this over using get_popup().popup().

int arrow_margin = 4 🔗

The horizontal space between the arrow icon and the right edge of the button.

int modulate_arrow = 0 🔗

If different than 0, the arrow icon will be modulated to the font color.

The arrow icon to be drawn on the right end of the button.

Please read the User-contributed notes policy before submitting a comment.

---

## PackedDataContainerRef

**URL:** https://docs.godotengine.org/en/stable/classes/class_packeddatacontainerref.html

**Contents:**
- PackedDataContainerRef
- Description
- Methods
- Method Descriptions
- User-contributed notes

Deprecated: Use @GlobalScope.var_to_bytes() or FileAccess.store_var() instead. To enable data compression, use PackedByteArray.compress() or FileAccess.open_compressed().

Inherits: RefCounted < Object

An internal class used by PackedDataContainer to pack nested arrays and dictionaries.

When packing nested containers using PackedDataContainer, they are recursively packed into PackedDataContainerRef (only applies to Array and Dictionary). Their data can be retrieved the same way as from PackedDataContainer.

Returns the size of the packed container (see Array.size() and Dictionary.size()).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var packed = PackedDataContainer.new()
packed.pack([1, 2, 3, ["nested1", "nested2"], 4, 5, 6])

for element in packed:
    if element is PackedDataContainerRef:
        for subelement in element:
            print("::", subelement)
    else:
        print(element)
```

Example 2 (julia):
```julia
1
2
3
::nested1
::nested2
4
5
6
```

---

## PackedDataContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_packeddatacontainer.html

**Contents:**
- PackedDataContainer
- Description
- Methods
- Method Descriptions
- User-contributed notes

Deprecated: Use @GlobalScope.var_to_bytes() or FileAccess.store_var() instead. To enable data compression, use PackedByteArray.compress() or FileAccess.open_compressed().

Inherits: Resource < RefCounted < Object

Efficiently packs and serializes Array or Dictionary.

PackedDataContainer can be used to efficiently store data from untyped containers. The data is packed into raw bytes and can be saved to file. Only Array and Dictionary can be stored this way.

You can retrieve the data by iterating on the container, which will work as if iterating on the packed data itself. If the packed container is a Dictionary, the data can be retrieved by key names (String/StringName only).

Nested containers will be packed recursively. While iterating, they will be returned as PackedDataContainerRef.

Error pack(value: Variant) 🔗

Packs the given container into a binary representation. The value must be either Array or Dictionary, any other type will result in invalid data error.

Note: Subsequent calls to this method will overwrite the existing data.

Returns the size of the packed container (see Array.size() and Dictionary.size()).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (json):
```json
var data = { "key": "value", "another_key": 123, "lock": Vector2() }
var packed = PackedDataContainer.new()
packed.pack(data)
ResourceSaver.save(packed, "packed_data.res")
```

Example 2 (gdscript):
```gdscript
var container = load("packed_data.res")
for key in container:
    prints(key, container[key])
```

Example 3 (unknown):
```unknown
key value
lock (0, 0)
another_key 123
```

---

## PanelContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_panelcontainer.html

**Contents:**
- PanelContainer
- Description
- Tutorials
- Properties
- Theme Properties
- Theme Property Descriptions
- User-contributed notes

Inherits: Container < Control < CanvasItem < Node < Object

Inherited By: OpenXRBindingModifierEditor, ScriptEditor

A container that keeps its child controls within the area of a StyleBox.

A container that keeps its child controls within the area of a StyleBox. Useful for giving controls an outline.

2D Role Playing Game (RPG) Demo

0 (overrides Control)

The style of PanelContainer's background.

Please read the User-contributed notes policy before submitting a comment.

---

## Panel

**URL:** https://docs.godotengine.org/en/stable/classes/class_panel.html

**Contents:**
- Panel
- Description
- Tutorials
- Theme Properties
- Theme Property Descriptions
- User-contributed notes

Inherits: Control < CanvasItem < Node < Object

A GUI control that displays a StyleBox.

Panel is a GUI control that displays a StyleBox. See also PanelContainer.

2D Role Playing Game (RPG) Demo

Hierarchical Finite State Machine Demo

The StyleBox of this control.

Please read the User-contributed notes policy before submitting a comment.

---

## PopupMenu

**URL:** https://docs.godotengine.org/en/stable/classes/class_popupmenu.html

**Contents:**
- PopupMenu
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions
- User-contributed notes

Inherits: Popup < Window < Viewport < Node < Object

A modal window used to display a list of options.

PopupMenu is a modal window used to display a list of options. Useful for toolbars and context menus.

The size of a PopupMenu can be limited by using Window.max_size. If the height of the list of items is larger than the maximum height of the PopupMenu, a ScrollContainer within the popup will allow the user to scroll the contents. If no maximum size is set, or if it is set to 0, the PopupMenu height will be limited by its parent rect.

All set_* methods allow negative item indices, i.e. -1 to access the last item, -2 to select the second-to-last item, and so on.

Incremental search: Like ItemList and Tree, PopupMenu supports searching within the list while the control is focused. Press a key that matches the first letter of an item's name to select the first item starting with the given letter. After that point, there are two ways to perform incremental search: 1) Press the same key again before the timeout duration to select the next item starting with the same letter. 2) Press letter keys that match the rest of the word before the timeout duration to match to select the item in question directly. Both of these actions will be reset to the beginning of the list if the timeout duration has passed since the last keystroke was registered. You can adjust the timeout duration by changing ProjectSettings.gui/timers/incremental_search_max_interval_msec.

Note: The ID values used for items are limited to 32 bits, not full 64 bits of int. This has a range of -2^32 to 2^32 - 1, i.e. -2147483648 to 2147483647.

hide_on_checkable_item_selection

hide_on_item_selection

hide_on_state_item_selection

true (overrides Window)

true (overrides Viewport)

activate_item_by_event(event: InputEvent, for_global_only: bool = false)

add_check_item(label: String, id: int = -1, accel: Key = 0)

add_check_shortcut(shortcut: Shortcut, id: int = -1, global: bool = false)

add_icon_check_item(texture: Texture2D, label: String, id: int = -1, accel: Key = 0)

add_icon_check_shortcut(texture: Texture2D, shortcut: Shortcut, id: int = -1, global: bool = false)

add_icon_item(texture: Texture2D, label: String, id: int = -1, accel: Key = 0)

add_icon_radio_check_item(texture: Texture2D, label: String, id: int = -1, accel: Key = 0)

add_icon_radio_check_shortcut(texture: Texture2D, shortcut: Shortcut, id: int = -1, global: bool = false)

add_icon_shortcut(texture: Texture2D, shortcut: Shortcut, id: int = -1, global: bool = false, allow_echo: bool = false)

add_item(label: String, id: int = -1, accel: Key = 0)

add_multistate_item(label: String, max_states: int, default_state: int = 0, id: int = -1, accel: Key = 0)

add_radio_check_item(label: String, id: int = -1, accel: Key = 0)

add_radio_check_shortcut(shortcut: Shortcut, id: int = -1, global: bool = false)

add_separator(label: String = "", id: int = -1)

add_shortcut(shortcut: Shortcut, id: int = -1, global: bool = false, allow_echo: bool = false)

add_submenu_item(label: String, submenu: String, id: int = -1)

add_submenu_node_item(label: String, submenu: PopupMenu, id: int = -1)

clear(free_submenus: bool = false)

get_focused_item() const

get_item_accelerator(index: int) const

get_item_auto_translate_mode(index: int) const

get_item_icon(index: int) const

get_item_icon_max_width(index: int) const

get_item_icon_modulate(index: int) const

get_item_id(index: int) const

get_item_indent(index: int) const

get_item_index(id: int) const

get_item_language(index: int) const

get_item_metadata(index: int) const

get_item_multistate(index: int) const

get_item_multistate_max(index: int) const

get_item_shortcut(index: int) const

get_item_submenu(index: int) const

get_item_submenu_node(index: int) const

get_item_text(index: int) const

get_item_text_direction(index: int) const

get_item_tooltip(index: int) const

is_item_checkable(index: int) const

is_item_checked(index: int) const

is_item_disabled(index: int) const

is_item_radio_checkable(index: int) const

is_item_separator(index: int) const

is_item_shortcut_disabled(index: int) const

is_native_menu() const

is_system_menu() const

remove_item(index: int)

scroll_to_item(index: int)

set_focused_item(index: int)

set_item_accelerator(index: int, accel: Key)

set_item_as_checkable(index: int, enable: bool)

set_item_as_radio_checkable(index: int, enable: bool)

set_item_as_separator(index: int, enable: bool)

set_item_auto_translate_mode(index: int, mode: AutoTranslateMode)

set_item_checked(index: int, checked: bool)

set_item_disabled(index: int, disabled: bool)

set_item_icon(index: int, icon: Texture2D)

set_item_icon_max_width(index: int, width: int)

set_item_icon_modulate(index: int, modulate: Color)

set_item_id(index: int, id: int)

set_item_indent(index: int, indent: int)

set_item_language(index: int, language: String)

set_item_metadata(index: int, metadata: Variant)

set_item_multistate(index: int, state: int)

set_item_multistate_max(index: int, max_states: int)

set_item_shortcut(index: int, shortcut: Shortcut, global: bool = false)

set_item_shortcut_disabled(index: int, disabled: bool)

set_item_submenu(index: int, submenu: String)

set_item_submenu_node(index: int, submenu: PopupMenu)

set_item_text(index: int, text: String)

set_item_text_direction(index: int, direction: TextDirection)

set_item_tooltip(index: int, tooltip: String)

toggle_item_checked(index: int)

toggle_item_multistate(index: int)

font_accelerator_color

Color(0.7, 0.7, 0.7, 0.8)

Color(0.875, 0.875, 0.875, 1)

Color(0.4, 0.4, 0.4, 0.8)

Color(0.875, 0.875, 0.875, 1)

Color(0.875, 0.875, 0.875, 1)

font_separator_outline_color

separator_outline_size

radio_checked_disabled

radio_unchecked_disabled

labeled_separator_left

labeled_separator_right

id_focused(id: int) 🔗

Emitted when the user navigated to an item of some id using the ProjectSettings.input/ui_up or ProjectSettings.input/ui_down input action.

id_pressed(id: int) 🔗

Emitted when an item of some id is pressed or its accelerator is activated.

Note: If id is negative (either explicitly or due to overflow), this will return the corresponding index instead.

index_pressed(index: int) 🔗

Emitted when an item of some index is pressed or its accelerator is activated.

Emitted when any item is added, modified or removed.

bool allow_search = true 🔗

void set_allow_search(value: bool)

bool get_allow_search()

If true, allows navigating PopupMenu with letter keys.

bool hide_on_checkable_item_selection = true 🔗

void set_hide_on_checkable_item_selection(value: bool)

bool is_hide_on_checkable_item_selection()

If true, hides the PopupMenu when a checkbox or radio button is selected.

bool hide_on_item_selection = true 🔗

void set_hide_on_item_selection(value: bool)

bool is_hide_on_item_selection()

If true, hides the PopupMenu when an item is selected.

bool hide_on_state_item_selection = false 🔗

void set_hide_on_state_item_selection(value: bool)

bool is_hide_on_state_item_selection()

If true, hides the PopupMenu when a state item is selected.

void set_item_count(value: int)

The number of items currently in the list.

bool prefer_native_menu = false 🔗

void set_prefer_native_menu(value: bool)

bool is_prefer_native_menu()

If true, MenuBar will use native menu when supported.

Note: If PopupMenu is linked to StatusIndicator, MenuBar, or another PopupMenu item it can use native menu regardless of this property, use is_native_menu() to check it.

float submenu_popup_delay = 0.3 🔗

void set_submenu_popup_delay(value: float)

float get_submenu_popup_delay()

Sets the delay time in seconds for the submenu item to popup on mouse hovering. If the popup menu is added as a child of another (acting as a submenu), it will inherit the delay time of the parent menu item.

SystemMenus system_menu_id = 0 🔗

void set_system_menu(value: SystemMenus)

SystemMenus get_system_menu()

If set to one of the values of SystemMenus, this PopupMenu is bound to the special system menu. Only one PopupMenu can be bound to each special menu at a time.

bool activate_item_by_event(event: InputEvent, for_global_only: bool = false) 🔗

Checks the provided event against the PopupMenu's shortcuts and accelerators, and activates the first item with matching events. If for_global_only is true, only shortcuts and accelerators with global set to true will be called.

Returns true if an item was successfully activated.

Note: Certain Controls, such as MenuButton, will call this method automatically.

void add_check_item(label: String, id: int = -1, accel: Key = 0) 🔗

Adds a new checkable item with text label.

An id can optionally be provided, as well as an accelerator (accel). If no id is provided, one will be created from the index. If no accel is provided, then the default value of 0 (corresponding to @GlobalScope.KEY_NONE) will be assigned to the item (which means it won't have any accelerator). See get_item_accelerator() for more info on accelerators.

Note: Checkable items just display a checkmark, but don't have any built-in checking behavior and must be checked/unchecked manually. See set_item_checked() for more info on how to control it.

void add_check_shortcut(shortcut: Shortcut, id: int = -1, global: bool = false) 🔗

Adds a new checkable item and assigns the specified Shortcut to it. Sets the label of the checkbox to the Shortcut's name.

An id can optionally be provided. If no id is provided, one will be created from the index.

Note: Checkable items just display a checkmark, but don't have any built-in checking behavior and must be checked/unchecked manually. See set_item_checked() for more info on how to control it.

void add_icon_check_item(texture: Texture2D, label: String, id: int = -1, accel: Key = 0) 🔗

Adds a new checkable item with text label and icon texture.

An id can optionally be provided, as well as an accelerator (accel). If no id is provided, one will be created from the index. If no accel is provided, then the default value of 0 (corresponding to @GlobalScope.KEY_NONE) will be assigned to the item (which means it won't have any accelerator). See get_item_accelerator() for more info on accelerators.

Note: Checkable items just display a checkmark, but don't have any built-in checking behavior and must be checked/unchecked manually. See set_item_checked() for more info on how to control it.

void add_icon_check_shortcut(texture: Texture2D, shortcut: Shortcut, id: int = -1, global: bool = false) 🔗

Adds a new checkable item and assigns the specified Shortcut and icon texture to it. Sets the label of the checkbox to the Shortcut's name.

An id can optionally be provided. If no id is provided, one will be created from the index.

Note: Checkable items just display a checkmark, but don't have any built-in checking behavior and must be checked/unchecked manually. See set_item_checked() for more info on how to control it.

void add_icon_item(texture: Texture2D, label: String, id: int = -1, accel: Key = 0) 🔗

Adds a new item with text label and icon texture.

An id can optionally be provided, as well as an accelerator (accel). If no id is provided, one will be created from the index. If no accel is provided, then the default value of 0 (corresponding to @GlobalScope.KEY_NONE) will be assigned to the item (which means it won't have any accelerator). See get_item_accelerator() for more info on accelerators.

void add_icon_radio_check_item(texture: Texture2D, label: String, id: int = -1, accel: Key = 0) 🔗

Same as add_icon_check_item(), but uses a radio check button.

void add_icon_radio_check_shortcut(texture: Texture2D, shortcut: Shortcut, id: int = -1, global: bool = false) 🔗

Same as add_icon_check_shortcut(), but uses a radio check button.

void add_icon_shortcut(texture: Texture2D, shortcut: Shortcut, id: int = -1, global: bool = false, allow_echo: bool = false) 🔗

Adds a new item and assigns the specified Shortcut and icon texture to it. Sets the label of the checkbox to the Shortcut's name.

An id can optionally be provided. If no id is provided, one will be created from the index.

If allow_echo is true, the shortcut can be activated with echo events.

void add_item(label: String, id: int = -1, accel: Key = 0) 🔗

Adds a new item with text label.

An id can optionally be provided, as well as an accelerator (accel). If no id is provided, one will be created from the index. If no accel is provided, then the default value of 0 (corresponding to @GlobalScope.KEY_NONE) will be assigned to the item (which means it won't have any accelerator). See get_item_accelerator() for more info on accelerators.

Note: The provided id is used only in id_pressed and id_focused signals. It's not related to the index arguments in e.g. set_item_checked().

void add_multistate_item(label: String, max_states: int, default_state: int = 0, id: int = -1, accel: Key = 0) 🔗

Adds a new multistate item with text label.

Contrarily to normal binary items, multistate items can have more than two states, as defined by max_states. The default value is defined by default_state.

An id can optionally be provided, as well as an accelerator (accel). If no id is provided, one will be created from the index. If no accel is provided, then the default value of 0 (corresponding to @GlobalScope.KEY_NONE) will be assigned to the item (which means it won't have any accelerator). See get_item_accelerator() for more info on accelerators.

Note: Multistate items don't update their state automatically and must be done manually. See toggle_item_multistate(), set_item_multistate() and get_item_multistate() for more info on how to control it.

void add_radio_check_item(label: String, id: int = -1, accel: Key = 0) 🔗

Adds a new radio check button with text label.

An id can optionally be provided, as well as an accelerator (accel). If no id is provided, one will be created from the index. If no accel is provided, then the default value of 0 (corresponding to @GlobalScope.KEY_NONE) will be assigned to the item (which means it won't have any accelerator). See get_item_accelerator() for more info on accelerators.

Note: Checkable items just display a checkmark, but don't have any built-in checking behavior and must be checked/unchecked manually. See set_item_checked() for more info on how to control it.

void add_radio_check_shortcut(shortcut: Shortcut, id: int = -1, global: bool = false) 🔗

Adds a new radio check button and assigns a Shortcut to it. Sets the label of the checkbox to the Shortcut's name.

An id can optionally be provided. If no id is provided, one will be created from the index.

Note: Checkable items just display a checkmark, but don't have any built-in checking behavior and must be checked/unchecked manually. See set_item_checked() for more info on how to control it.

void add_separator(label: String = "", id: int = -1) 🔗

Adds a separator between items. Separators also occupy an index, which you can set by using the id parameter.

A label can optionally be provided, which will appear at the center of the separator.

void add_shortcut(shortcut: Shortcut, id: int = -1, global: bool = false, allow_echo: bool = false) 🔗

An id can optionally be provided. If no id is provided, one will be created from the index.

If allow_echo is true, the shortcut can be activated with echo events.

void add_submenu_item(label: String, submenu: String, id: int = -1) 🔗

Deprecated: Prefer using add_submenu_node_item() instead.

Adds an item that will act as a submenu of the parent PopupMenu node when clicked. The submenu argument must be the name of an existing PopupMenu that has been added as a child to this node. This submenu will be shown when the item is clicked, hovered for long enough, or activated using the ui_select or ui_right input actions.

An id can optionally be provided. If no id is provided, one will be created from the index.

void add_submenu_node_item(label: String, submenu: PopupMenu, id: int = -1) 🔗

Adds an item that will act as a submenu of the parent PopupMenu node when clicked. This submenu will be shown when the item is clicked, hovered for long enough, or activated using the ui_select or ui_right input actions.

submenu must be either child of this PopupMenu or has no parent node (in which case it will be automatically added as a child). If the submenu popup has another parent, this method will fail.

An id can optionally be provided. If no id is provided, one will be created from the index.

void clear(free_submenus: bool = false) 🔗

Removes all items from the PopupMenu. If free_submenus is true, the submenu nodes are automatically freed.

int get_focused_item() const 🔗

Returns the index of the currently focused item. Returns -1 if no item is focused.

Key get_item_accelerator(index: int) const 🔗

Returns the accelerator of the item at the given index. An accelerator is a keyboard shortcut that can be pressed to trigger the menu button even if it's not currently open. The return value is an integer which is generally a combination of KeyModifierMasks and Keys using bitwise OR such as KEY_MASK_CTRL | KEY_A (Ctrl + A). If no accelerator is defined for the specified index, get_item_accelerator() returns 0 (corresponding to @GlobalScope.KEY_NONE).

AutoTranslateMode get_item_auto_translate_mode(index: int) const 🔗

Returns the auto translate mode of the item at the given index.

Texture2D get_item_icon(index: int) const 🔗

Returns the icon of the item at the given index.

int get_item_icon_max_width(index: int) const 🔗

Returns the maximum allowed width of the icon for the item at the given index.

Color get_item_icon_modulate(index: int) const 🔗

Returns a Color modulating the item's icon at the given index.

int get_item_id(index: int) const 🔗

Returns the ID of the item at the given index. id can be manually assigned, while index can not.

int get_item_indent(index: int) const 🔗

Returns the horizontal offset of the item at the given index.

int get_item_index(id: int) const 🔗

Returns the index of the item containing the specified id. Index is automatically assigned to each item by the engine and can not be set manually.

String get_item_language(index: int) const 🔗

Returns item's text language code.

Variant get_item_metadata(index: int) const 🔗

Returns the metadata of the specified item, which might be of any type. You can set it with set_item_metadata(), which provides a simple way of assigning context data to items.

int get_item_multistate(index: int) const 🔗

Returns the state of the item at the given index.

int get_item_multistate_max(index: int) const 🔗

Returns the max states of the item at the given index.

Shortcut get_item_shortcut(index: int) const 🔗

Returns the Shortcut associated with the item at the given index.

String get_item_submenu(index: int) const 🔗

Deprecated: Prefer using get_item_submenu_node() instead.

Returns the submenu name of the item at the given index. See add_submenu_item() for more info on how to add a submenu.

PopupMenu get_item_submenu_node(index: int) const 🔗

Returns the submenu of the item at the given index, or null if no submenu was added. See add_submenu_node_item() for more info on how to add a submenu.

String get_item_text(index: int) const 🔗

Returns the text of the item at the given index.

TextDirection get_item_text_direction(index: int) const 🔗

Returns item's text base writing direction.

String get_item_tooltip(index: int) const 🔗

Returns the tooltip associated with the item at the given index.

bool is_item_checkable(index: int) const 🔗

Returns true if the item at the given index is checkable in some way, i.e. if it has a checkbox or radio button.

Note: Checkable items just display a checkmark or radio button, but don't have any built-in checking behavior and must be checked/unchecked manually.

bool is_item_checked(index: int) const 🔗

Returns true if the item at the given index is checked.

bool is_item_disabled(index: int) const 🔗

Returns true if the item at the given index is disabled. When it is disabled it can't be selected, or its action invoked.

See set_item_disabled() for more info on how to disable an item.

bool is_item_radio_checkable(index: int) const 🔗

Returns true if the item at the given index has radio button-style checkability.

Note: This is purely cosmetic; you must add the logic for checking/unchecking items in radio groups.

bool is_item_separator(index: int) const 🔗

Returns true if the item is a separator. If it is, it will be displayed as a line. See add_separator() for more info on how to add a separator.

bool is_item_shortcut_disabled(index: int) const 🔗

Returns true if the specified item's shortcut is disabled.

bool is_native_menu() const 🔗

Returns true if the system native menu is supported and currently used by this PopupMenu.

bool is_system_menu() const 🔗

Returns true if the menu is bound to the special system menu.

void remove_item(index: int) 🔗

Removes the item at the given index from the menu.

Note: The indices of items after the removed item will be shifted by one.

void scroll_to_item(index: int) 🔗

Moves the scroll view to make the item at the given index visible.

void set_focused_item(index: int) 🔗

Sets the currently focused item as the given index.

Passing -1 as the index makes so that no item is focused.

void set_item_accelerator(index: int, accel: Key) 🔗

Sets the accelerator of the item at the given index. An accelerator is a keyboard shortcut that can be pressed to trigger the menu button even if it's not currently open. accel is generally a combination of KeyModifierMasks and Keys using bitwise OR such as KEY_MASK_CTRL | KEY_A (Ctrl + A).

void set_item_as_checkable(index: int, enable: bool) 🔗

Sets whether the item at the given index has a checkbox. If false, sets the type of the item to plain text.

Note: Checkable items just display a checkmark, but don't have any built-in checking behavior and must be checked/unchecked manually.

void set_item_as_radio_checkable(index: int, enable: bool) 🔗

Sets the type of the item at the given index to radio button. If false, sets the type of the item to plain text.

void set_item_as_separator(index: int, enable: bool) 🔗

Mark the item at the given index as a separator, which means that it would be displayed as a line. If false, sets the type of the item to plain text.

void set_item_auto_translate_mode(index: int, mode: AutoTranslateMode) 🔗

Sets the auto translate mode of the item at the given index.

Items use Node.AUTO_TRANSLATE_MODE_INHERIT by default, which uses the same auto translate mode as the PopupMenu itself.

void set_item_checked(index: int, checked: bool) 🔗

Sets the checkstate status of the item at the given index.

void set_item_disabled(index: int, disabled: bool) 🔗

Enables/disables the item at the given index. When it is disabled, it can't be selected and its action can't be invoked.

void set_item_icon(index: int, icon: Texture2D) 🔗

Replaces the Texture2D icon of the item at the given index.

void set_item_icon_max_width(index: int, width: int) 🔗

Sets the maximum allowed width of the icon for the item at the given index. This limit is applied on top of the default size of the icon and on top of icon_max_width. The height is adjusted according to the icon's ratio.

void set_item_icon_modulate(index: int, modulate: Color) 🔗

Sets a modulating Color of the item's icon at the given index.

void set_item_id(index: int, id: int) 🔗

Sets the id of the item at the given index.

The id is used in id_pressed and id_focused signals.

void set_item_indent(index: int, indent: int) 🔗

Sets the horizontal offset of the item at the given index.

void set_item_language(index: int, language: String) 🔗

Sets language code of item's text used for line-breaking and text shaping algorithms, if left empty current locale is used instead.

void set_item_metadata(index: int, metadata: Variant) 🔗

Sets the metadata of an item, which may be of any type. You can later get it with get_item_metadata(), which provides a simple way of assigning context data to items.

void set_item_multistate(index: int, state: int) 🔗

Sets the state of a multistate item. See add_multistate_item() for details.

void set_item_multistate_max(index: int, max_states: int) 🔗

Sets the max states of a multistate item. See add_multistate_item() for details.

void set_item_shortcut(index: int, shortcut: Shortcut, global: bool = false) 🔗

Sets a Shortcut for the item at the given index.

void set_item_shortcut_disabled(index: int, disabled: bool) 🔗

Disables the Shortcut of the item at the given index.

void set_item_submenu(index: int, submenu: String) 🔗

Deprecated: Prefer using set_item_submenu_node() instead.

Sets the submenu of the item at the given index. The submenu is the name of a child PopupMenu node that would be shown when the item is clicked.

void set_item_submenu_node(index: int, submenu: PopupMenu) 🔗

Sets the submenu of the item at the given index. The submenu is a PopupMenu node that would be shown when the item is clicked. It must either be a child of this PopupMenu or has no parent (in which case it will be automatically added as a child). If the submenu popup has another parent, this method will fail.

void set_item_text(index: int, text: String) 🔗

Sets the text of the item at the given index.

void set_item_text_direction(index: int, direction: TextDirection) 🔗

Sets item's text base writing direction.

void set_item_tooltip(index: int, tooltip: String) 🔗

Sets the String tooltip of the item at the given index.

void toggle_item_checked(index: int) 🔗

Toggles the check state of the item at the given index.

void toggle_item_multistate(index: int) 🔗

Cycle to the next state of a multistate item. See add_multistate_item() for details.

Color font_accelerator_color = Color(0.7, 0.7, 0.7, 0.8) 🔗

The text Color used for shortcuts and accelerators that show next to the menu item name when defined. See get_item_accelerator() for more info on accelerators.

Color font_color = Color(0.875, 0.875, 0.875, 1) 🔗

The default text Color for menu items' names.

Color font_disabled_color = Color(0.4, 0.4, 0.4, 0.8) 🔗

Color used for disabled menu items' text.

Color font_hover_color = Color(0.875, 0.875, 0.875, 1) 🔗

Color used for the hovered text.

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The tint of text outline of the menu item.

Color font_separator_color = Color(0.875, 0.875, 0.875, 1) 🔗

Color used for labeled separators' text. See add_separator().

Color font_separator_outline_color = Color(0, 0, 0, 1) 🔗

The tint of text outline of the labeled separator.

int h_separation = 4 🔗

The horizontal space between the item's elements.

int icon_max_width = 0 🔗

The maximum allowed width of the item's icon. This limit is applied on top of the default size of the icon, but before the value set with set_item_icon_max_width(). The height is adjusted according to the icon's ratio.

Width of the single indentation level.

int item_end_padding = 2 🔗

Horizontal padding to the right of the items (or left, in RTL layout).

int item_start_padding = 2 🔗

Horizontal padding to the left of the items (or right, in RTL layout).

int outline_size = 0 🔗

The size of the item text outline.

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

int separator_outline_size = 0 🔗

The size of the labeled separator text outline.

int v_separation = 4 🔗

The vertical space between each menu item.

Font used for the menu items.

Font font_separator 🔗

Font used for the labeled separator.

int font_separator_size 🔗

Font size of the labeled separator.

Font size of the menu items.

Texture2D icon for the checked checkbox items.

Texture2D checked_disabled 🔗

Texture2D icon for the checked checkbox items when they are disabled.

Texture2D radio_checked 🔗

Texture2D icon for the checked radio button items.

Texture2D radio_checked_disabled 🔗

Texture2D icon for the checked radio button items when they are disabled.

Texture2D radio_unchecked 🔗

Texture2D icon for the unchecked radio button items.

Texture2D radio_unchecked_disabled 🔗

Texture2D icon for the unchecked radio button items when they are disabled.

Texture2D icon for the submenu arrow (for left-to-right layouts).

Texture2D submenu_mirrored 🔗

Texture2D icon for the submenu arrow (for right-to-left layouts).

Texture2D unchecked 🔗

Texture2D icon for the unchecked checkbox items.

Texture2D unchecked_disabled 🔗

Texture2D icon for the unchecked checkbox items when they are disabled.

StyleBox displayed when the PopupMenu item is hovered.

StyleBox labeled_separator_left 🔗

StyleBox for the left side of labeled separator. See add_separator().

StyleBox labeled_separator_right 🔗

StyleBox for the right side of labeled separator. See add_separator().

StyleBox for the background panel.

StyleBox used for the separators. See add_separator().

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    add_multistate_item("Item", 3, 0)

    index_pressed.connect(func(index: int):
            toggle_item_multistate(index)
            match get_item_multistate(index):
                0:
                    print("First state")
                1:
                    print("Second state")
                2:
                    print("Third state")
        )
```

---

## PopupPanel

**URL:** https://docs.godotengine.org/en/stable/classes/class_popuppanel.html

**Contents:**
- PopupPanel
- Description
- Properties
- Theme Properties
- Theme Property Descriptions
- User-contributed notes

Inherits: Popup < Window < Viewport < Node < Object

A popup with a panel background.

A popup with a configurable panel background. Any child controls added to this node will be stretched to fit the panel's size (similar to how PanelContainer works). If you are making windows, see Window.

true (overrides Window)

true (overrides Viewport)

StyleBox for the background panel.

Please read the User-contributed notes policy before submitting a comment.

---

## Popup

**URL:** https://docs.godotengine.org/en/stable/classes/class_popup.html

**Contents:**
- Popup
- Description
- Properties
- Signals
- User-contributed notes

Inherits: Window < Viewport < Node < Object

Inherited By: PopupMenu, PopupPanel

Base class for contextual windows and panels with fixed position.

Popup is a base class for contextual windows and panels with fixed position. It's a modal by default (see Window.popup_window) and provides methods for implementing custom popup behavior.

true (overrides Window)

true (overrides Window)

true (overrides Window)

true (overrides Window)

true (overrides Window)

true (overrides Window)

true (overrides Window)

false (overrides Window)

true (overrides Window)

Emitted when the popup is hidden.

Please read the User-contributed notes policy before submitting a comment.

---

## Random number generation

**URL:** https://docs.godotengine.org/en/stable/tutorials/math/random_number_generation.html

**Contents:**
- Random number generation
- Global scope versus RandomNumberGenerator class
- The randomize() method
- Getting a random number
- Get a random array element
- Get a random dictionary value
- Weighted random probability
- "Better" randomness using shuffle bags
- Random noise
- Cryptographically secure pseudorandom number generation

Many games rely on randomness to implement core game mechanics. This page guides you through common types of randomness and how to implement them in Godot.

After giving you a brief overview of useful functions that generate random numbers, you will learn how to get random elements from arrays, dictionaries, and how to use a noise generator in GDScript. Lastly, we'll take a look at cryptographically secure random number generation and how it differs from typical random number generation.

Computers cannot generate "true" random numbers. Instead, they rely on pseudorandom number generators (PRNGs).

Godot internally uses the PCG Family of pseudorandom number generators.

Godot exposes two ways to generate random numbers: via global scope methods or using the RandomNumberGenerator class.

Global scope methods are easier to set up, but they don't offer as much control.

RandomNumberGenerator requires more code to use, but allows creating multiple instances, each with their own seed and state.

This tutorial uses global scope methods, except when the method only exists in the RandomNumberGenerator class.

Since Godot 4.0, the random seed is automatically set to a random value when the project starts. This means you don't need to call randomize() in _ready() anymore to ensure that results are random across project runs. However, you can still use randomize() if you want to use a specific seed number, or generate it using a different method.

In global scope, you can find a randomize() method. This method should be called only once when your project starts to initialize the random seed. Calling it multiple times is unnecessary and may impact performance negatively.

Putting it in your main scene script's _ready() method is a good choice:

You can also set a fixed random seed instead using seed(). Doing so will give you deterministic results across runs:

When using the RandomNumberGenerator class, you should call randomize() on the instance since it has its own seed:

Let's look at some of the most commonly used functions and methods to generate random numbers in Godot.

The function randi() returns a random number between 0 and 2^32 - 1. Since the maximum value is huge, you most likely want to use the modulo operator (%) to bound the result between 0 and the denominator:

randf() returns a random floating-point number between 0 and 1. This is useful to implement a Weighted random probability system, among other things.

randfn() returns a random floating-point number following a normal distribution. This means the returned value is more likely to be around the mean (0.0 by default), varying by the deviation (1.0 by default):

randf_range() takes two arguments from and to, and returns a random floating-point number between from and to:

randi_range() takes two arguments from and to, and returns a random integer between from and to:

We can use random integer generation to get a random element from an array, or use the Array.pick_random method to do it for us:

To prevent the same fruit from being picked more than once in a row, we can add more logic to the above method. In this case, we can't use Array.pick_random since it lacks a way to prevent repetition:

This approach can be useful to make random number generation feel less repetitive. Still, it doesn't prevent results from "ping-ponging" between a limited set of values. To prevent this, use the shuffle bag pattern instead.

We can apply similar logic from arrays to dictionaries as well:

The randf() method returns a floating-point number between 0.0 and 1.0. We can use this to create a "weighted" probability where different outcomes have different likelihoods:

You can also get a weighted random index using the rand_weighted() method on a RandomNumberGenerator instance. This returns a random integer between 0 and the size of the array that is passed as a parameter. Each value in the array is a floating-point number that represents the relative likelihood that it will be returned as an index. A higher value means the value is more likely to be returned as an index, while a value of 0 means it will never be returned as an index.

For example, if [0.5, 1, 1, 2] is passed as a parameter, then the method is twice as likely to return 3 (the index of the value 2) and twice as unlikely to return 0 (the index of the value 0.5) compared to the indices 1 and 2.

Since the returned value matches the array's size, it can be used as an index to get a value from another array as follows:

Taking the same example as above, we would like to pick fruits at random. However, relying on random number generation every time a fruit is selected can lead to a less uniform distribution. If the player is lucky (or unlucky), they could get the same fruit three or more times in a row.

You can accomplish this using the shuffle bag pattern. It works by removing an element from the array after choosing it. After multiple selections, the array ends up empty. When that happens, you reinitialize it to its default value:

When running the above code, there is a chance to get the same fruit twice in a row. Once we picked a fruit, it will no longer be a possible return value unless the array is now empty. When the array is empty, we reset it back to its default value, making it possible to have the same fruit again, but only once.

The random number generation shown above can show its limits when you need a value that slowly changes depending on the input. The input can be a position, time, or anything else.

To achieve this, you can use random noise functions. Noise functions are especially popular in procedural generation to generate realistic-looking terrain. Godot provides FastNoiseLite for this, which supports 1D, 2D and 3D noise. Here's an example with 1D noise:

So far, the approaches mentioned above are not suitable for cryptographically secure pseudorandom number generation (CSPRNG). This is fine for games, but this is not sufficient for scenarios where encryption, authentication or signing is involved.

Godot offers a Crypto class for this. This class can perform asymmetric key encryption/decryption, signing/verification, while also generating cryptographically secure random bytes, RSA keys, HMAC digests, and self-signed X509Certificates.

The downside of CSPRNG is that it's much slower than standard pseudorandom number generation. Its API is also less convenient to use. As a result, CSPRNG should be avoided for gameplay elements.

Example of using the Crypto class to generate 2 random integers between 0 and 2^32 - 1 (inclusive):

See PackedByteArray's documentation for other methods you can use to decode the generated bytes into various types of data, such as integers or floats.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    randomize()
```

Example 2 (gdscript):
```gdscript
public override void _Ready()
{
    GD.Randomize();
}
```

Example 3 (gdscript):
```gdscript
func _ready():
    seed(12345)
    # To use a string as a seed, you can hash it to a number.
    seed("Hello world".hash())
```

Example 4 (gdscript):
```gdscript
public override void _Ready()
{
    GD.Seed(12345);
    // To use a string as a seed, you can hash it to a number.
    GD.Seed("Hello world".Hash());
}
```

---

## ReferenceRect

**URL:** https://docs.godotengine.org/en/stable/classes/class_referencerect.html

**Contents:**
- ReferenceRect
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Control < CanvasItem < Node < Object

A rectangular box for designing UIs.

A rectangular box that displays only a colored border around its rectangle (see Control.get_rect()). It can be used to visualize the extents of a Control node, for testing purposes.

Color border_color = Color(1, 0, 0, 1) 🔗

void set_border_color(value: Color)

Color get_border_color()

Sets the border color of the ReferenceRect.

float border_width = 1.0 🔗

void set_border_width(value: float)

float get_border_width()

Sets the border width of the ReferenceRect. The border grows both inwards and outwards with respect to the rectangle box.

bool editor_only = true 🔗

void set_editor_only(value: bool)

bool get_editor_only()

If true, the ReferenceRect will only be visible while in editor. Otherwise, ReferenceRect will be visible in the running project.

Please read the User-contributed notes policy before submitting a comment.

---

## ResourceUID

**URL:** https://docs.godotengine.org/en/stable/classes/class_resourceuid.html

**Contents:**
- ResourceUID
- Description
- Methods
- Constants
- Method Descriptions
- User-contributed notes

A singleton that manages the unique identifiers of all resources within a project.

Resource UIDs (Unique IDentifiers) allow the engine to keep references between resources intact, even if files are renamed or moved. They can be accessed with uid://.

ResourceUID keeps track of all registered resource UIDs in a project, generates new UIDs, and converts between their string and integer representations.

add_id(id: int, path: String)

create_id_for_path(path: String)

ensure_path(path_or_uid: String) static

get_id_path(id: int) const

has_id(id: int) const

id_to_text(id: int) const

path_to_uid(path: String) static

set_id(id: int, path: String)

text_to_id(text_id: String) const

uid_to_path(uid: String) static

The value to use for an invalid UID, for example if the resource could not be loaded.

Its text representation is uid://<invalid>.

void add_id(id: int, path: String) 🔗

Adds a new UID value which is mapped to the given resource path.

Fails with an error if the UID already exists, so be sure to check has_id() beforehand, or use set_id() instead.

Generates a random resource UID which is guaranteed to be unique within the list of currently loaded UIDs.

In order for this UID to be registered, you must call add_id() or set_id().

int create_id_for_path(path: String) 🔗

Like create_id(), but the UID is seeded with the provided path and project name. UIDs generated for that path will be always the same within the current project.

String ensure_path(path_or_uid: String) static 🔗

Returns a path, converting path_or_uid if necessary. Prints an error if provided an invalid UID.

String get_id_path(id: int) const 🔗

Returns the path that the given UID value refers to.

Fails with an error if the UID does not exist, so be sure to check has_id() beforehand.

bool has_id(id: int) const 🔗

Returns whether the given UID value is known to the cache.

String id_to_text(id: int) const 🔗

Converts the given UID to a uid:// string value.

String path_to_uid(path: String) static 🔗

Converts the provided resource path to a UID. Returns the unchanged path if it has no associated UID.

void remove_id(id: int) 🔗

Removes a loaded UID value from the cache.

Fails with an error if the UID does not exist, so be sure to check has_id() beforehand.

void set_id(id: int, path: String) 🔗

Updates the resource path of an existing UID.

Fails with an error if the UID does not exist, so be sure to check has_id() beforehand, or use add_id() instead.

int text_to_id(text_id: String) const 🔗

Extracts the UID value from the given uid:// string.

String uid_to_path(uid: String) static 🔗

Converts the provided uid to a path. Prints an error if the UID is invalid.

Please read the User-contributed notes policy before submitting a comment.

---

## RichTextLabel

**URL:** https://docs.godotengine.org/en/stable/classes/class_richtextlabel.html

**Contents:**
- RichTextLabel
- Description
- Tutorials
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions

Inherits: Control < CanvasItem < Node < Object

A control for displaying text that can contain different font styles, images, and basic formatting.

A control for displaying text that can contain custom fonts, images, and basic formatting. RichTextLabel manages these as an internal tag stack. It also adapts itself to given width/heights.

Note: newline(), push_paragraph(), "\n", "\r\n", p tag, and alignment tags start a new paragraph. Each paragraph is processed independently, in its own BiDi context. If you want to force line wrapping within paragraph, any other line breaking character can be used, for example, Form Feed (U+000C), Next Line (U+0085), Line Separator (U+2028).

Note: Assignments to text clear the tag stack and reconstruct it from the property's contents. Any edits made to text will erase previous edits made from other manual sources such as append_text() and the push_* / pop() methods.

Note: RichTextLabel doesn't support entangled BBCode tags. For example, instead of using [b]bold[i]bold italic[/b]italic[/i], use [b]bold[i]bold italic[/i][/b][i]italic[/i].

Note: push_*/pop_* functions won't affect BBCode.

Note: While bbcode_enabled is enabled, alignment tags such as [center] will take priority over the horizontal_alignment setting which determines the default text alignment.

BBCode in RichTextLabel

Rich Text Label with BBCode Demo

Operating System Testing Demo

BitField[LineBreakFlag]

true (overrides Control)

deselect_on_focus_loss_enabled

drag_and_drop_selection_enabled

3 (overrides Control)

BitField[JustificationFlag]

scroll_following_visible_characters

shortcut_keys_enabled

structured_text_bidi_override

structured_text_bidi_override_options

VisibleCharactersBehavior

visible_characters_behavior

add_hr(width: int = 90, height: int = 2, color: Color = Color(1, 1, 1, 1), alignment: HorizontalAlignment = 1, width_in_percent: bool = true, height_in_percent: bool = false)

add_image(image: Texture2D, width: int = 0, height: int = 0, color: Color = Color(1, 1, 1, 1), inline_align: InlineAlignment = 5, region: Rect2 = Rect2(0, 0, 0, 0), key: Variant = null, pad: bool = false, tooltip: String = "", width_in_percent: bool = false, height_in_percent: bool = false, alt_text: String = "")

add_text(text: String)

append_text(bbcode: String)

get_character_line(character: int)

get_character_paragraph(character: int)

get_content_height() const

get_content_width() const

get_line_count() const

get_line_height(line: int) const

get_line_offset(line: int)

get_line_range(line: int)

get_line_width(line: int) const

get_paragraph_count() const

get_paragraph_offset(paragraph: int)

get_parsed_text() const

get_selected_text() const

get_selection_from() const

get_selection_line_offset() const

get_selection_to() const

get_total_character_count() const

get_visible_content_rect() const

get_visible_line_count() const

get_visible_paragraph_count() const

install_effect(effect: Variant)

invalidate_paragraph(paragraph: int)

is_menu_visible() const

menu_option(option: int)

parse_bbcode(bbcode: String)

parse_expressions_for_values(expressions: PackedStringArray)

push_bgcolor(bgcolor: Color)

push_color(color: Color)

push_customfx(effect: RichTextEffect, env: Dictionary)

push_dropcap(string: String, font: Font, size: int, dropcap_margins: Rect2 = Rect2(0, 0, 0, 0), color: Color = Color(1, 1, 1, 1), outline_size: int = 0, outline_color: Color = Color(0, 0, 0, 0))

push_fgcolor(fgcolor: Color)

push_font(font: Font, font_size: int = 0)

push_font_size(font_size: int)

push_hint(description: String)

push_indent(level: int)

push_language(language: String)

push_list(level: int, type: ListType, capitalize: bool, bullet: String = "•")

push_meta(data: Variant, underline_mode: MetaUnderline = 1, tooltip: String = "")

push_outline_color(color: Color)

push_outline_size(outline_size: int)

push_paragraph(alignment: HorizontalAlignment, base_direction: TextDirection = 0, language: String = "", st_parser: StructuredTextParser = 0, justification_flags: BitField[JustificationFlag] = 163, tab_stops: PackedFloat32Array = PackedFloat32Array())

push_strikethrough(color: Color = Color(0, 0, 0, 0))

push_table(columns: int, inline_align: InlineAlignment = 0, align_to_row: int = -1, name: String = "")

push_underline(color: Color = Color(0, 0, 0, 0))

remove_paragraph(paragraph: int, no_invalidate: bool = false)

scroll_to_line(line: int)

scroll_to_paragraph(paragraph: int)

scroll_to_selection()

set_cell_border_color(color: Color)

set_cell_padding(padding: Rect2)

set_cell_row_background_color(odd_row_bg: Color, even_row_bg: Color)

set_cell_size_override(min_size: Vector2, max_size: Vector2)

set_table_column_expand(column: int, expand: bool, ratio: int = 1, shrink: bool = true)

set_table_column_name(column: int, name: String)

update_image(key: Variant, mask: BitField[ImageUpdateMask], image: Texture2D, width: int = 0, height: int = 0, color: Color = Color(1, 1, 1, 1), inline_align: InlineAlignment = 5, region: Rect2 = Rect2(0, 0, 0, 0), pad: bool = false, tooltip: String = "", width_in_percent: bool = false, height_in_percent: bool = false)

Color(0.1, 0.1, 1, 0.8)

text_highlight_h_padding

text_highlight_v_padding

bold_italics_font_size

Triggered when the document is fully loaded.

Note: This can happen before the text is processed for drawing. Scrolling values may not be valid until the document is drawn for the first time after this signal.

meta_clicked(meta: Variant) 🔗

Triggered when the user clicks on content between meta (URL) tags. If the meta is defined in BBCode, e.g. [url={"key": "value"}]Text[/url], then the parameter for this signal will always be a String type. If a particular type or an object is desired, the push_meta() method must be used to manually insert the data into the tag stack. Alternatively, you can convert the String input to the desired type based on its contents (such as calling JSON.parse() on it).

For example, the following method can be connected to meta_clicked to open clicked URLs using the user's default web browser:

meta_hover_ended(meta: Variant) 🔗

Triggers when the mouse exits a meta tag.

meta_hover_started(meta: Variant) 🔗

Triggers when the mouse enters a meta tag.

ListType LIST_NUMBERS = 0

Each list item has a number marker.

ListType LIST_LETTERS = 1

Each list item has a letter marker.

ListType LIST_ROMAN = 2

Each list item has a roman number marker.

ListType LIST_DOTS = 3

Each list item has a filled circle marker.

MenuItems MENU_COPY = 0

Copies the selected text.

MenuItems MENU_SELECT_ALL = 1

Selects the whole RichTextLabel text.

MenuItems MENU_MAX = 2

Represents the size of the MenuItems enum.

enum MetaUnderline: 🔗

MetaUnderline META_UNDERLINE_NEVER = 0

Meta tag does not display an underline, even if meta_underlined is true.

MetaUnderline META_UNDERLINE_ALWAYS = 1

If meta_underlined is true, meta tag always display an underline.

MetaUnderline META_UNDERLINE_ON_HOVER = 2

If meta_underlined is true, meta tag display an underline when the mouse cursor is over it.

flags ImageUpdateMask: 🔗

ImageUpdateMask UPDATE_TEXTURE = 1

If this bit is set, update_image() changes image texture.

ImageUpdateMask UPDATE_SIZE = 2

If this bit is set, update_image() changes image size.

ImageUpdateMask UPDATE_COLOR = 4

If this bit is set, update_image() changes image color.

ImageUpdateMask UPDATE_ALIGNMENT = 8

If this bit is set, update_image() changes image inline alignment.

ImageUpdateMask UPDATE_REGION = 16

If this bit is set, update_image() changes image texture region.

ImageUpdateMask UPDATE_PAD = 32

If this bit is set, update_image() changes image padding.

ImageUpdateMask UPDATE_TOOLTIP = 64

If this bit is set, update_image() changes image tooltip.

ImageUpdateMask UPDATE_WIDTH_IN_PERCENT = 128

If this bit is set, update_image() changes image width from/to percents.

AutowrapMode autowrap_mode = 3 🔗

void set_autowrap_mode(value: AutowrapMode)

AutowrapMode get_autowrap_mode()

If set to something other than TextServer.AUTOWRAP_OFF, the text gets wrapped inside the node's bounding rectangle.

BitField[LineBreakFlag] autowrap_trim_flags = 192 🔗

void set_autowrap_trim_flags(value: BitField[LineBreakFlag])

BitField[LineBreakFlag] get_autowrap_trim_flags()

Autowrap space trimming flags. See TextServer.BREAK_TRIM_START_EDGE_SPACES and TextServer.BREAK_TRIM_END_EDGE_SPACES for more info.

bool bbcode_enabled = false 🔗

void set_use_bbcode(value: bool)

bool is_using_bbcode()

If true, the label uses BBCode formatting.

Note: This only affects the contents of text, not the tag stack.

bool context_menu_enabled = false 🔗

void set_context_menu_enabled(value: bool)

bool is_context_menu_enabled()

If true, a right-click displays the context menu.

Array custom_effects = [] 🔗

void set_effects(value: Array)

The currently installed custom effects. This is an array of RichTextEffects.

To add a custom effect, it's more convenient to use install_effect().

bool deselect_on_focus_loss_enabled = true 🔗

void set_deselect_on_focus_loss_enabled(value: bool)

bool is_deselect_on_focus_loss_enabled()

If true, the selected text will be deselected when focus is lost.

bool drag_and_drop_selection_enabled = true 🔗

void set_drag_and_drop_selection_enabled(value: bool)

bool is_drag_and_drop_selection_enabled()

If true, allow drag and drop of selected text.

bool fit_content = false 🔗

void set_fit_content(value: bool)

bool is_fit_content_enabled()

If true, the label's minimum size will be automatically updated to fit its content, matching the behavior of Label.

bool hint_underlined = true 🔗

void set_hint_underline(value: bool)

bool is_hint_underlined()

If true, the label underlines hint tags such as [hint=description]{text}[/hint].

HorizontalAlignment horizontal_alignment = 0 🔗

void set_horizontal_alignment(value: HorizontalAlignment)

HorizontalAlignment get_horizontal_alignment()

Controls the text's horizontal alignment. Supports left, center, right, and fill, or justify.

BitField[JustificationFlag] justification_flags = 163 🔗

void set_justification_flags(value: BitField[JustificationFlag])

BitField[JustificationFlag] get_justification_flags()

Line fill alignment rules.

String language = "" 🔗

void set_language(value: String)

String get_language()

Language code used for line-breaking and text shaping algorithms, if left empty current locale is used instead.

bool meta_underlined = true 🔗

void set_meta_underline(value: bool)

bool is_meta_underlined()

If true, the label underlines meta tags such as [url]{text}[/url]. These tags can call a function when clicked if meta_clicked is connected to a function.

int progress_bar_delay = 1000 🔗

void set_progress_bar_delay(value: int)

int get_progress_bar_delay()

The delay after which the loading progress bar is displayed, in milliseconds. Set to -1 to disable progress bar entirely.

Note: Progress bar is displayed only if threaded is enabled.

bool scroll_active = true 🔗

void set_scroll_active(value: bool)

bool is_scroll_active()

If true, the scrollbar is visible. Setting this to false does not block scrolling completely. See scroll_to_line().

bool scroll_following = false 🔗

void set_scroll_follow(value: bool)

bool is_scroll_following()

If true, the window scrolls down to display new content automatically.

bool scroll_following_visible_characters = false 🔗

void set_scroll_follow_visible_characters(value: bool)

bool is_scroll_following_visible_characters()

If true, the window scrolls to display the last visible line when visible_characters or visible_ratio is changed.

bool selection_enabled = false 🔗

void set_selection_enabled(value: bool)

bool is_selection_enabled()

If true, the label allows text selection.

bool shortcut_keys_enabled = true 🔗

void set_shortcut_keys_enabled(value: bool)

bool is_shortcut_keys_enabled()

If true, shortcut keys for context menu items are enabled, even if the context menu is disabled.

StructuredTextParser structured_text_bidi_override = 0 🔗

void set_structured_text_bidi_override(value: StructuredTextParser)

StructuredTextParser get_structured_text_bidi_override()

Set BiDi algorithm override for the structured text.

Array structured_text_bidi_override_options = [] 🔗

void set_structured_text_bidi_override_options(value: Array)

Array get_structured_text_bidi_override_options()

Set additional options for BiDi override.

void set_tab_size(value: int)

The number of spaces associated with a single tab length. Does not affect \t in text tags, only indent tags.

PackedFloat32Array tab_stops = PackedFloat32Array() 🔗

void set_tab_stops(value: PackedFloat32Array)

PackedFloat32Array get_tab_stops()

Aligns text to the given tab-stops.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedFloat32Array for more details.

void set_text(value: String)

The label's text in BBCode format. Is not representative of manual modifications to the internal tag stack. Erases changes made by other methods when edited.

Note: If bbcode_enabled is true, it is unadvised to use the += operator with text (e.g. text += "some string") as it replaces the whole text and can cause slowdowns. It will also erase all BBCode that was added to stack using push_* methods. Use append_text() for adding text instead, unless you absolutely need to close a tag that was opened in an earlier method call.

TextDirection text_direction = 0 🔗

void set_text_direction(value: TextDirection)

TextDirection get_text_direction()

Base text writing direction.

bool threaded = false 🔗

void set_threaded(value: bool)

If true, text processing is done in a background thread.

VerticalAlignment vertical_alignment = 0 🔗

void set_vertical_alignment(value: VerticalAlignment)

VerticalAlignment get_vertical_alignment()

Controls the text's vertical alignment. Supports top, center, bottom, and fill.

int visible_characters = -1 🔗

void set_visible_characters(value: int)

int get_visible_characters()

The number of characters to display. If set to -1, all characters are displayed. This can be useful when animating the text appearing in a dialog box.

Note: Setting this property updates visible_ratio accordingly.

Note: Characters are counted as Unicode codepoints. A single visible grapheme may contain multiple codepoints (e.g. certain emoji use three codepoints). A single codepoint may contain two UTF-16 characters, which are used in C# strings.

VisibleCharactersBehavior visible_characters_behavior = 0 🔗

void set_visible_characters_behavior(value: VisibleCharactersBehavior)

VisibleCharactersBehavior get_visible_characters_behavior()

The clipping behavior when visible_characters or visible_ratio is set.

float visible_ratio = 1.0 🔗

void set_visible_ratio(value: float)

float get_visible_ratio()

The fraction of characters to display, relative to the total number of characters (see get_total_character_count()). If set to 1.0, all characters are displayed. If set to 0.5, only half of the characters will be displayed. This can be useful when animating the text appearing in a dialog box.

Note: Setting this property updates visible_characters accordingly.

void add_hr(width: int = 90, height: int = 2, color: Color = Color(1, 1, 1, 1), alignment: HorizontalAlignment = 1, width_in_percent: bool = true, height_in_percent: bool = false) 🔗

Adds a horizontal rule that can be used to separate content.

If width_in_percent is set, width values are percentages of the control width instead of pixels.

If height_in_percent is set, height values are percentages of the control width instead of pixels.

void add_image(image: Texture2D, width: int = 0, height: int = 0, color: Color = Color(1, 1, 1, 1), inline_align: InlineAlignment = 5, region: Rect2 = Rect2(0, 0, 0, 0), key: Variant = null, pad: bool = false, tooltip: String = "", width_in_percent: bool = false, height_in_percent: bool = false, alt_text: String = "") 🔗

Adds an image's opening and closing tags to the tag stack, optionally providing a width and height to resize the image, a color to tint the image and a region to only use parts of the image.

If width or height is set to 0, the image size will be adjusted in order to keep the original aspect ratio.

If width and height are not set, but region is, the region's rect will be used.

key is an optional identifier, that can be used to modify the image via update_image().

If pad is set, and the image is smaller than the size specified by width and height, the image padding is added to match the size instead of upscaling.

If width_in_percent is set, width values are percentages of the control width instead of pixels.

If height_in_percent is set, height values are percentages of the control width instead of pixels.

alt_text is used as the image description for assistive apps.

void add_text(text: String) 🔗

Adds raw non-BBCode-parsed text to the tag stack.

void append_text(bbcode: String) 🔗

Parses bbcode and adds tags to the tag stack as needed.

Note: Using this method, you can't close a tag that was opened in a previous append_text() call. This is done to improve performance, especially when updating large RichTextLabels since rebuilding the whole BBCode every time would be slower. If you absolutely need to close a tag in a future method call, append the text instead of using append_text().

Clears the tag stack, causing the label to display nothing.

Note: This method does not affect text, and its contents will show again if the label is redrawn. However, setting text to an empty String also clears the stack.

Clears the current selection.

int get_character_line(character: int) 🔗

Returns the line number of the character position provided. Line and character numbers are both zero-indexed.

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether document is fully loaded.

int get_character_paragraph(character: int) 🔗

Returns the paragraph number of the character position provided. Paragraph and character numbers are both zero-indexed.

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether document is fully loaded.

int get_content_height() const 🔗

Returns the height of the content.

Note: This method always returns the full content size, and is not affected by visible_ratio and visible_characters. To get the visible content size, use get_visible_content_rect().

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether document is fully loaded.

int get_content_width() const 🔗

Returns the width of the content.

Note: This method always returns the full content size, and is not affected by visible_ratio and visible_characters. To get the visible content size, use get_visible_content_rect().

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether document is fully loaded.

int get_line_count() const 🔗

Returns the total number of lines in the text. Wrapped text is counted as multiple lines.

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether document is fully loaded.

int get_line_height(line: int) const 🔗

Returns the height of the line found at the provided index.

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether the document is fully loaded.

float get_line_offset(line: int) 🔗

Returns the vertical offset of the line found at the provided index.

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether document is fully loaded.

Vector2i get_line_range(line: int) 🔗

Returns the indexes of the first and last visible characters for the given line, as a Vector2i.

Note: If visible_characters_behavior is set to TextServer.VC_CHARS_BEFORE_SHAPING only visible wrapped lines are counted.

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether document is fully loaded.

int get_line_width(line: int) const 🔗

Returns the width of the line found at the provided index.

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether the document is fully loaded.

PopupMenu get_menu() const 🔗

Returns the PopupMenu of this RichTextLabel. By default, this menu is displayed when right-clicking on the RichTextLabel.

You can add custom menu items or remove standard ones. Make sure your IDs don't conflict with the standard ones (see MenuItems). For example:

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their Window.visible property.

int get_paragraph_count() const 🔗

Returns the total number of paragraphs (newlines or p tags in the tag stack's text tags). Considers wrapped text as one paragraph.

float get_paragraph_offset(paragraph: int) 🔗

Returns the vertical offset of the paragraph found at the provided index.

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether document is fully loaded.

String get_parsed_text() const 🔗

Returns the text without BBCode mark-up.

String get_selected_text() const 🔗

Returns the current selection text. Does not include BBCodes.

int get_selection_from() const 🔗

Returns the current selection first character index if a selection is active, -1 otherwise. Does not include BBCodes.

float get_selection_line_offset() const 🔗

Returns the current selection vertical line offset if a selection is active, -1.0 otherwise.

int get_selection_to() const 🔗

Returns the current selection last character index if a selection is active, -1 otherwise. Does not include BBCodes.

int get_total_character_count() const 🔗

Returns the total number of characters from text tags. Does not include BBCodes.

VScrollBar get_v_scroll_bar() 🔗

Returns the vertical scrollbar.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their CanvasItem.visible property.

Rect2i get_visible_content_rect() const 🔗

Returns the bounding rectangle of the visible content.

Note: This method returns a correct value only after the label has been drawn.

int get_visible_line_count() const 🔗

Returns the number of visible lines.

Note: This method returns a correct value only after the label has been drawn.

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether document is fully loaded.

int get_visible_paragraph_count() const 🔗

Returns the number of visible paragraphs. A paragraph is considered visible if at least one of its lines is visible.

Note: This method returns a correct value only after the label has been drawn.

Note: If threaded is enabled, this method returns a value for the loaded part of the document. Use is_finished() or finished to determine whether document is fully loaded.

void install_effect(effect: Variant) 🔗

Installs a custom effect. This can also be done in the Inspector through the custom_effects property. effect should be a valid RichTextEffect.

Example: With the following script extending from RichTextEffect:

The above effect can be installed in RichTextLabel from a script:

bool invalidate_paragraph(paragraph: int) 🔗

Invalidates paragraph and all subsequent paragraphs cache.

bool is_finished() const 🔗

If threaded is enabled, returns true if the background thread has finished text processing, otherwise always return true.

bool is_menu_visible() const 🔗

Returns whether the menu is visible. Use this instead of get_menu().visible to improve performance (so the creation of the menu is avoided).

bool is_ready() const 🔗

Deprecated: Use is_finished() instead.

If threaded is enabled, returns true if the background thread has finished text processing, otherwise always return true.

void menu_option(option: int) 🔗

Executes a given action as defined in the MenuItems enum.

Adds a newline tag to the tag stack.

void parse_bbcode(bbcode: String) 🔗

The assignment version of append_text(). Clears the tag stack and inserts the new content.

Dictionary parse_expressions_for_values(expressions: PackedStringArray) 🔗

Parses BBCode parameter expressions into a dictionary.

Terminates the current tag. Use after push_* methods to close BBCodes manually. Does not need to follow add_* methods.

Terminates all tags opened by push_* methods.

Terminates tags opened after the last push_context() call (including context marker), or all tags if there's no context marker on the stack.

void push_bgcolor(bgcolor: Color) 🔗

Adds a [bgcolor] tag to the tag stack.

Note: The background color has padding applied by default, which is controlled using text_highlight_h_padding and text_highlight_v_padding. This can lead to overlapping highlights if background colors are placed on neighboring lines/columns, so consider setting those theme items to 0 if you want to avoid this.

Adds a [font] tag with a bold font to the tag stack. This is the same as adding a [b] tag if not currently in a [i] tag.

void push_bold_italics() 🔗

Adds a [font] tag with a bold italics font to the tag stack.

Adds a [cell] tag to the tag stack. Must be inside a [table] tag. See push_table() for details. Use set_table_column_expand() to set column expansion ratio, set_cell_border_color() to set cell border, set_cell_row_background_color() to set cell background, set_cell_size_override() to override cell size, and set_cell_padding() to set padding.

void push_color(color: Color) 🔗

Adds a [color] tag to the tag stack.

void push_context() 🔗

Adds a context marker to the tag stack. See pop_context().

void push_customfx(effect: RichTextEffect, env: Dictionary) 🔗

Adds a custom effect tag to the tag stack. The effect does not need to be in custom_effects. The environment is directly passed to the effect.

void push_dropcap(string: String, font: Font, size: int, dropcap_margins: Rect2 = Rect2(0, 0, 0, 0), color: Color = Color(1, 1, 1, 1), outline_size: int = 0, outline_color: Color = Color(0, 0, 0, 0)) 🔗

Adds a [dropcap] tag to the tag stack. Drop cap (dropped capital) is a decorative element at the beginning of a paragraph that is larger than the rest of the text.

void push_fgcolor(fgcolor: Color) 🔗

Adds a [fgcolor] tag to the tag stack.

Note: The foreground color has padding applied by default, which is controlled using text_highlight_h_padding and text_highlight_v_padding. This can lead to overlapping highlights if foreground colors are placed on neighboring lines/columns, so consider setting those theme items to 0 if you want to avoid this.

void push_font(font: Font, font_size: int = 0) 🔗

Adds a [font] tag to the tag stack. Overrides default fonts for its duration.

Passing 0 to font_size will use the existing default font size.

void push_font_size(font_size: int) 🔗

Adds a [font_size] tag to the tag stack. Overrides default font size for its duration.

void push_hint(description: String) 🔗

Adds a [hint] tag to the tag stack. Same as BBCode [hint=something]{text}[/hint].

void push_indent(level: int) 🔗

Adds an [indent] tag to the tag stack. Multiplies level by current tab_size to determine new margin length.

void push_italics() 🔗

Adds a [font] tag with an italics font to the tag stack. This is the same as adding an [i] tag if not currently in a [b] tag.

void push_language(language: String) 🔗

Adds language code used for text shaping algorithm and Open-Type font features.

void push_list(level: int, type: ListType, capitalize: bool, bullet: String = "•") 🔗

Adds [ol] or [ul] tag to the tag stack. Multiplies level by current tab_size to determine new margin length.

void push_meta(data: Variant, underline_mode: MetaUnderline = 1, tooltip: String = "") 🔗

Adds a meta tag to the tag stack. Similar to the BBCode [url=something]{text}[/url], but supports non-String metadata types.

If meta_underlined is true, meta tags display an underline. This behavior can be customized with underline_mode.

Note: Meta tags do nothing by default when clicked. To assign behavior when clicked, connect meta_clicked to a function that is called when the meta tag is clicked.

Adds a [font] tag with a monospace font to the tag stack.

Adds a [font] tag with a normal font to the tag stack.

void push_outline_color(color: Color) 🔗

Adds a [outline_color] tag to the tag stack. Adds text outline for its duration.

void push_outline_size(outline_size: int) 🔗

Adds a [outline_size] tag to the tag stack. Overrides default text outline size for its duration.

void push_paragraph(alignment: HorizontalAlignment, base_direction: TextDirection = 0, language: String = "", st_parser: StructuredTextParser = 0, justification_flags: BitField[JustificationFlag] = 163, tab_stops: PackedFloat32Array = PackedFloat32Array()) 🔗

Adds a [p] tag to the tag stack.

void push_strikethrough(color: Color = Color(0, 0, 0, 0)) 🔗

Adds a [s] tag to the tag stack. If color alpha value is zero, current font color with alpha multiplied by strikethrough_alpha is used.

void push_table(columns: int, inline_align: InlineAlignment = 0, align_to_row: int = -1, name: String = "") 🔗

Adds a [table=columns,inline_align] tag to the tag stack. Use set_table_column_expand() to set column expansion ratio. Use push_cell() to add cells. name is used as the table name for assistive apps.

void push_underline(color: Color = Color(0, 0, 0, 0)) 🔗

Adds a [u] tag to the tag stack. If color alpha value is zero, current font color with alpha multiplied by underline_alpha is used.

void reload_effects() 🔗

Reloads custom effects. Useful when custom_effects is modified manually.

bool remove_paragraph(paragraph: int, no_invalidate: bool = false) 🔗

Removes a paragraph of content from the label. Returns true if the paragraph exists.

The paragraph argument is the index of the paragraph to remove, it can take values in the interval [0, get_paragraph_count() - 1].

If no_invalidate is set to true, cache for the subsequent paragraphs is not invalidated. Use it for faster updates if deleted paragraph is fully self-contained (have no unclosed tags), or this call is part of the complex edit operation and invalidate_paragraph() will be called at the end of operation.

void scroll_to_line(line: int) 🔗

Scrolls the window's top line to match line.

void scroll_to_paragraph(paragraph: int) 🔗

Scrolls the window's top line to match first line of the paragraph.

void scroll_to_selection() 🔗

Scrolls to the beginning of the current selection.

If selection_enabled is false, no selection will occur.

void set_cell_border_color(color: Color) 🔗

Sets color of a table cell border.

void set_cell_padding(padding: Rect2) 🔗

Sets inner padding of a table cell.

void set_cell_row_background_color(odd_row_bg: Color, even_row_bg: Color) 🔗

Sets color of a table cell. Separate colors for alternating rows can be specified.

void set_cell_size_override(min_size: Vector2, max_size: Vector2) 🔗

Sets minimum and maximum size overrides for a table cell.

void set_table_column_expand(column: int, expand: bool, ratio: int = 1, shrink: bool = true) 🔗

Edits the selected column's expansion options. If expand is true, the column expands in proportion to its expansion ratio versus the other columns' ratios.

For example, 2 columns with ratios 3 and 4 plus 70 pixels in available width would expand 30 and 40 pixels, respectively.

If expand is false, the column will not contribute to the total ratio.

void set_table_column_name(column: int, name: String) 🔗

Sets table column name for assistive apps.

void update_image(key: Variant, mask: BitField[ImageUpdateMask], image: Texture2D, width: int = 0, height: int = 0, color: Color = Color(1, 1, 1, 1), inline_align: InlineAlignment = 5, region: Rect2 = Rect2(0, 0, 0, 0), pad: bool = false, tooltip: String = "", width_in_percent: bool = false, height_in_percent: bool = false) 🔗

Updates the existing images with the key key. Only properties specified by mask bits are updated. See add_image().

Color default_color = Color(1, 1, 1, 1) 🔗

The default text color.

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The default tint of text outline.

Color font_selected_color = Color(0, 0, 0, 0) 🔗

The color of selected text, used when selection_enabled is true. If equal to Color(0, 0, 0, 0), it will be ignored.

Color font_shadow_color = Color(0, 0, 0, 0) 🔗

The color of the font's shadow.

Color selection_color = Color(0.1, 0.1, 1, 0.8) 🔗

The color of the selection box.

Color table_border = Color(0, 0, 0, 0) 🔗

The default cell border color.

Color table_even_row_bg = Color(0, 0, 0, 0) 🔗

The default background color for even rows.

Color table_odd_row_bg = Color(0, 0, 0, 0) 🔗

The default background color for odd rows.

int line_separation = 0 🔗

Additional vertical spacing between lines (in pixels), spacing is added to line descent. This value can be negative.

int outline_size = 0 🔗

The size of the text outline.

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

int paragraph_separation = 0 🔗

Additional vertical spacing between paragraphs (in pixels). Spacing is added after the last line. This value can be negative.

int shadow_offset_x = 1 🔗

The horizontal offset of the font's shadow.

int shadow_offset_y = 1 🔗

The vertical offset of the font's shadow.

int shadow_outline_size = 1 🔗

The size of the shadow outline.

int strikethrough_alpha = 50 🔗

The default strikethrough color transparency (percent). For strikethroughs with a custom color, this theme item is only used if the custom color's alpha is 0.0 (fully transparent).

int table_h_separation = 3 🔗

The horizontal separation of elements in a table.

int table_v_separation = 3 🔗

The vertical separation of elements in a table.

int text_highlight_h_padding = 3 🔗

The horizontal padding around boxes drawn by the [fgcolor] and [bgcolor] tags. This does not affect the appearance of text selection. To avoid any risk of neighboring highlights overlapping each other, set this to 0 to disable padding.

int text_highlight_v_padding = 3 🔗

The vertical padding around boxes drawn by the [fgcolor] and [bgcolor] tags. This does not affect the appearance of text selection. To avoid any risk of neighboring highlights overlapping each other, set this to 0 to disable padding.

int underline_alpha = 50 🔗

The default underline color transparency (percent). For underlines with a custom color, this theme item is only used if the custom color's alpha is 0.0 (fully transparent).

The font used for bold text.

Font bold_italics_font 🔗

The font used for bold italics text.

The font used for italics text.

The font used for monospace text.

The default text font.

The font size used for bold text.

int bold_italics_font_size 🔗

The font size used for bold italics text.

int italics_font_size 🔗

The font size used for italics text.

The font size used for monospace text.

int normal_font_size 🔗

The default text font size.

Texture2D horizontal_rule 🔗

The horizontal rule texture.

The background used when the RichTextLabel is focused. The focus StyleBox is displayed over the base StyleBox, so a partially transparent StyleBox should be used to ensure the base StyleBox remains visible. A StyleBox that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a StyleBoxEmpty resource. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

The normal background for the RichTextLabel.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (go):
```go
# This assumes RichTextLabel's `meta_clicked` signal was connected to
# the function below using the signal connection dialog.
func _richtextlabel_on_meta_clicked(meta):
    # `meta` is of Variant type, so convert it to a String to avoid script errors at run-time.
    OS.shell_open(str(meta))
```

Example 2 (gdscript):
```gdscript
func _ready():
    var menu = get_menu()
    # Remove "Select All" item.
    menu.remove_item(MENU_SELECT_ALL)
    # Add custom items.
    menu.add_separator()
    menu.add_item("Duplicate Text", MENU_MAX + 1)
    # Connect callback.
    menu.id_pressed.connect(_on_item_pressed)

func _on_item_pressed(id):
    if id == MENU_MAX + 1:
        add_text("\n" + get_parsed_text())
```

Example 3 (gdscript):
```gdscript
public override void _Ready()
{
    var menu = GetMenu();
    // Remove "Select All" item.
    menu.RemoveItem(RichTextLabel.MenuItems.SelectAll);
    // Add custom items.
    menu.AddSeparator();
    menu.AddItem("Duplicate Text", RichTextLabel.MenuItems.Max + 1);
    // Add event handler.
    menu.IdPressed += OnItemPressed;
}

public void OnItemPressed(int id)
{
    if (id == TextEdit.MenuItems.Max + 1)
    {
        AddText("\n" + GetParsedText());
    }
}
```

Example 4 (gdscript):
```gdscript
extends RichTextLabel

@export var background_panel: Panel

func _ready():
    await draw
    background_panel.position = get_visible_content_rect().position
    background_panel.size = get_visible_content_rect().size
```

---

## ScriptCreateDialog

**URL:** https://docs.godotengine.org/en/stable/classes/class_scriptcreatedialog.html

**Contents:**
- ScriptCreateDialog
- Description
- Properties
- Methods
- Signals
- Method Descriptions
- User-contributed notes

Inherits: ConfirmationDialog < AcceptDialog < Window < Viewport < Node < Object

Godot editor's popup dialog for creating new Script files.

The ScriptCreateDialog creates script files according to a given template for a given scripting language. The standard use is to configure its fields prior to calling one of the Window.popup() methods.

false (overrides AcceptDialog)

"Create" (overrides AcceptDialog)

"Attach Node Script" (overrides Window)

config(inherits: String, path: String, built_in_enabled: bool = true, load_enabled: bool = true)

script_created(script: Script) 🔗

Emitted when the user clicks the OK button.

void config(inherits: String, path: String, built_in_enabled: bool = true, load_enabled: bool = true) 🔗

Prefills required fields to configure the ScriptCreateDialog for use.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    var dialog = ScriptCreateDialog.new();
    dialog.config("Node", "res://new_node.gd") # For in-engine types.
    dialog.config("\"res://base_node.gd\"", "res://derived_node.gd") # For script types.
    dialog.popup_centered()
```

Example 2 (gdscript):
```gdscript
public override void _Ready()
{
    var dialog = new ScriptCreateDialog();
    dialog.Config("Node", "res://NewNode.cs"); // For in-engine types.
    dialog.Config("\"res://BaseNode.cs\"", "res://DerivedNode.cs"); // For script types.
    dialog.PopupCentered();
}
```

---

## Separator

**URL:** https://docs.godotengine.org/en/stable/classes/class_separator.html

**Contents:**
- Separator
- Description
- Theme Properties
- Theme Property Descriptions
- User-contributed notes

Inherits: Control < CanvasItem < Node < Object

Inherited By: HSeparator, VSeparator

Abstract base class for separators.

Abstract base class for separators, used for separating other controls. Separators are purely visual and normally drawn as a StyleBoxLine.

The size of the area covered by the separator. Effectively works like a minimum width/height.

The style for the separator line. Works best with StyleBoxLine (remember to enable StyleBoxLine.vertical for VSeparator).

Please read the User-contributed notes policy before submitting a comment.

---

## Shading language

**URL:** https://docs.godotengine.org/en/stable/tutorials/shaders/shader_reference/shading_language.html

**Contents:**
- Shading language
- Introduction
- Data types
  - Comments
  - Casting
  - Members
  - Constructing
  - Swizzling
  - Precision
- Arrays

Godot uses a shading language similar to GLSL ES 3.0. Most datatypes and functions are supported, and the few remaining ones will likely be added over time.

If you are already familiar with GLSL, the Godot Shader Migration Guide is a resource that will help you transition from regular GLSL to Godot's shading language.

Most GLSL ES 3.0 datatypes are supported:

Void datatype, useful only for functions that return nothing.

Boolean datatype, can only contain true or false.

Two-component vector of booleans.

Three-component vector of booleans.

Four-component vector of booleans.

32 bit signed scalar integer.

Two-component vector of signed integers.

Three-component vector of signed integers.

Four-component vector of signed integers.

Unsigned scalar integer; can't contain negative numbers.

Two-component vector of unsigned integers.

Three-component vector of unsigned integers.

Four-component vector of unsigned integers.

32 bit floating-point scalar.

Two-component vector of floating-point values.

Three-component vector of floating-point values.

Four-component vector of floating-point values.

2x2 matrix, in column major order.

3x3 matrix, in column major order.

4x4 matrix, in column major order.

Sampler type for binding 2D textures, which are read as float.

Sampler type for binding 2D textures, which are read as signed integer.

Sampler type for binding 2D textures, which are read as unsigned integer.

Sampler type for binding 2D texture arrays, which are read as float.

Sampler type for binding 2D texture arrays, which are read as signed integer.

Sampler type for binding 2D texture arrays, which are read as unsigned integer.

Sampler type for binding 3D textures, which are read as float.

Sampler type for binding 3D textures, which are read as signed integer.

Sampler type for binding 3D textures, which are read as unsigned integer.

Sampler type for binding Cubemaps, which are read as float.

Sampler type for binding Cubemap arrays, which are read as float. Only supported in Forward+ and Mobile, not Compatibility.

External sampler type. Only supported in Compatibility/Android platform.

Local variables are not initialized to a default value such as 0.0. If you use a variable without assigning it first, it will contain whatever value was already present at that memory location, and unpredictable visual glitches will appear. However, uniforms and varyings are initialized to a default value.

The shading language supports the same comment syntax as used in C# and C++, using // for single-line comments and /* */ for multi-line comments:

Additionally, you can use documentation comments that are displayed in the inspector when hovering a shader parameter. Documentation comments are currently only supported when placed immediately above a uniform declaration. These documentation comments only support the multiline comment syntax and must use two leading asterisks (/**) instead of just one (/*):

The asterisks on the follow-up lines are not required, but are recommended as per the Shaders style guide. These asterisks are automatically stripped by the inspector, so they won't appear in the tooltip.

Just like GLSL ES 3.0, implicit casting between scalars and vectors of the same size but different type is not allowed. Casting of types of different size is also not allowed. Conversion must be done explicitly via constructors.

Default integer constants are signed, so casting is always needed to convert to unsigned:

Individual scalar members of vector types are accessed via the "x", "y", "z" and "w" members. Alternatively, using "r", "g", "b" and "a" also works and is equivalent. Use whatever fits best for your needs.

For matrices, use the m[column][row] indexing syntax to access each scalar, or m[column] to access a vector by column index. For example, for accessing the y-component of the translation from a mat4 transform matrix (4th column, 2nd line) you use m[3][1] or m[3].y.

Construction of vector types must always pass:

Construction of matrix types requires vectors of the same dimension as the matrix, interpreted as columns. You can also build a diagonal matrix using matx(float) syntax. Accordingly, mat4(1.0) is an identity matrix.

Matrices can also be built from a matrix of another dimension. There are two rules:

1. If a larger matrix is constructed from a smaller matrix, the additional rows and columns are set to the values they would have in an identity matrix. 2. If a smaller matrix is constructed from a larger matrix, the top, left submatrix of the larger matrix is used.

It is possible to obtain any combination of components in any order, as long as the result is another vector type (or scalar). This is easier shown than explained:

It is possible to add precision modifiers to datatypes; use them for uniforms, variables, arguments and varyings:

Using lower precision for some operations can speed up the math involved (at the cost of less precision). This is rarely needed in the vertex processor function (where full precision is needed most of the time), but is often useful in the fragment processor.

Some architectures (mainly mobile) can benefit significantly from this, but there are downsides such as the additional overhead of conversion between precisions. Refer to the documentation of the target architecture for further information. In many cases, mobile drivers cause inconsistent or unexpected behavior and it is best to avoid specifying precision unless necessary.

Arrays are containers for multiple variables of a similar type.

Local arrays are declared in functions. They can use all of the allowed datatypes, except samplers. The array declaration follows a C-style syntax: [const] + [precision] + typename + identifier + [array size].

They can be initialized at the beginning like:

You can declare multiple arrays (even with different sizes) in one expression:

To access an array element, use the indexing syntax:

Arrays also have a built-in function .length() (not to be confused with the built-in length() function). It doesn't accept any parameters and will return the array's size.

If you use an index either below 0 or greater than array size - the shader will crash and break rendering. To prevent this, use length(), if, or clamp() functions to ensure the index is between 0 and the array's length. Always carefully test and check your code. If you pass a constant expression or a number, the editor will check its bounds to prevent this crash.

You can declare arrays in global space as either const or uniform:

Global arrays use the same syntax as local arrays, except with a const or uniform added to their declaration. Note that uniform arrays can't have a default value.

Use the const keyword before the variable declaration to make that variable immutable, which means that it cannot be modified. All basic types, except samplers can be declared as constants. Accessing and using a constant value is slightly faster than using a uniform. Constants must be initialized at their declaration.

Constants cannot be modified and additionally cannot have hints, but multiple of them (if they have the same type) can be declared in a single expression e.g

Similar to variables, arrays can also be declared with const.

Constants can be declared both globally (outside of any function) or locally (inside a function). Global constants are useful when you want to have access to a value throughout your shader that does not need to be modified. Like uniforms, global constants are shared between all shader stages, but they are not accessible outside of the shader.

Constants of the float type must be initialized using . notation after the decimal part or by using the scientific notation. The optional f post-suffix is also supported.

Constants of the uint (unsigned int) type must have a u suffix to differentiate them from signed integers. Alternatively, this can be done by using the uint(x) built-in conversion function.

Structs are compound types which can be used for better abstraction of shader code. You can declare them at the global scope like:

After declaration, you can instantiate and initialize them like:

Or use struct constructor for same purpose:

Structs may contain other struct or array, you can also instance them as global constant:

You can also pass them to functions:

Godot shading language supports the same set of operators as GLSL ES 3.0. Below is the list of them in precedence order:

parenthetical grouping

bit-wise exclusive OR

bit-wise inclusive OR

Most operators that accept vectors or matrices (multiplication, division, etc) operate component-wise, meaning the function is applied to the first value of each vector and then on the second value of each vector, etc. Some examples:

Equivalent Scalar Operation

vec3(4 + 2, 5 + 2, 6 + 2)

vec2(3, 4) * vec2(10, 20)

mat2(vec2(1, 2), vec2(3, 4)) + 10

mat2(vec2(1 + 10, 2 + 10), vec2(3 + 10, 4 + 10))

The GLSL Language Specification says under section 5.10 Vector and Matrix Operations:

With a few exceptions, operations are component-wise. Usually, when an operator operates on a vector or matrix, it is operating independently on each component of the vector or matrix, in a component-wise fashion. [...] The exceptions are matrix multiplied by vector, vector multiplied by matrix, and matrix multiplied by matrix. These do not operate component-wise, but rather perform the correct linear algebraic multiply.

Godot Shading language supports the most common types of flow control:

Keep in mind that in modern GPUs, an infinite loop can exist and can freeze your application (including editor). Godot can't protect you from this, so be careful not to make this mistake!

Also, when comparing floating-point values against a number, make sure to compare them against a range instead of an exact number.

A comparison like if (value == 0.3) may not evaluate to true. Floating-point math is often approximate and can defy expectations. It can also behave differently depending on the hardware.

Instead, always perform a range comparison with an epsilon value. The larger the floating-point number (and the less precise the floating-point number), the larger the epsilon value should be.

See floating-point-gui.de for more information.

Fragment, light, and custom functions (called from fragment or light) can use the discard keyword. If used, the fragment is discarded and nothing is written.

Beware that discard has a performance cost when used, as it will prevent the depth prepass from being effective on any surfaces using the shader. Also, a discarded pixel still needs to be rendered in the vertex shader, which means a shader that uses discard on all of its pixels is still more expensive to render compared to not rendering any object in the first place.

It is possible to define functions in a Godot shader. They use the following syntax:

You can only use functions that have been defined above (higher in the editor) the function from which you are calling them. Redefining a function that has already been defined above (or is a built-in function name) will cause an error.

Function arguments can have special qualifiers:

in: Means the argument is only for reading (default).

out: Means the argument is only for writing.

inout: Means the argument is fully passed via reference.

const: Means the argument is a constant and cannot be changed, may be combined with in qualifier.

Function overloading is supported. You can define multiple functions with the same name, but different arguments. Note that implicit casting in overloaded function calls is not allowed, such as from int to float (1 to 1.0).

To send data from the vertex to the fragment (or light) processor function, varyings are used. They are set for every primitive vertex in the vertex processor, and the value is interpolated for every pixel in the fragment processor.

Varying can also be an array:

It's also possible to send data from fragment to light processors using varying keyword. To do so you can assign it in the fragment and later use it in the light function.

Note that varying may not be assigned in custom functions or a light processor function like:

This limitation was introduced to prevent incorrect usage before initialization.

Certain values are interpolated during the shading pipeline. You can modify how these interpolations are done by using interpolation qualifiers.

There are two possible interpolation qualifiers:

The value is not interpolated.

The value is interpolated in a perspective-correct fashion. This is the default.

Passing values to shaders is possible with uniforms, which are defined in the global scope of the shader, outside of functions. When a shader is later assigned to a material, the uniforms will appear as editable parameters in the material's inspector. Uniforms can't be written from within the shader. Any data type except for void can be a uniform.

You can set uniforms in the editor in the material's inspector. Alternately, you can set them from code.

Godot provides optional uniform hints to make the compiler understand what the uniform is used for, and how the editor should allow users to modify it.

Uniforms can also be assigned default values:

Note that when adding a default value and a hint, the default value goes after the hint.

Full list of uniform hints below:

hint_enum("String1", "String2")

Displays int input as a dropdown widget in the editor.

hint_range(min, max[, step])

Restricted to values in a range (with min/max/step).

Used as albedo color.

As value or albedo color, default to opaque white.

As value or albedo color, default to opaque black.

hint_default_transparent

As value or albedo color, default to transparent black.

As flowmap, default to right.

hint_roughness[_r, _g, _b, _a, _normal, _gray]

Used for roughness limiter on import (attempts reducing specular aliasing). _normal is a normal map that guides the roughness limiter, with roughness increasing in areas that have high-frequency detail.

filter[_nearest, _linear][_mipmap][_anisotropic]

Enabled specified texture filtering.

repeat[_enable, _disable]

Enabled texture repeating.

Texture is the screen texture.

Texture is the depth texture.

hint_normal_roughness_texture

Texture is the normal roughness texture (only supported in Forward+).

You can access int values as a readable dropdown widget using the hint_enum uniform:

You can assign explicit values to the hint_enum uniform using colon syntax similar to GDScript:

The value will be stored as an integer, corresponding to the index of the selected option (i.e. 0, 1, or 2) or the value assigned by colon syntax (i.e. 30, 60, or 200). When setting the value with set_shader_parameter(), you must use the integer value, not the String name.

Any texture which contains sRGB color data requires a source_color hint in order to be correctly sampled. This is because Godot renders in linear color space, but some textures contain sRGB color data. If this hint is not used, the texture will appear washed out.

Albedo and color textures should typically have a source_color hint. Normal, roughness, metallic, and height textures typically do not need a source_color hint.

Using source_color hint is required in the Forward+ and Mobile renderers, and in canvas_item shaders when HDR 2D is enabled. The source_color hint is optional for the Compatibility renderer, and for canvas_item shaders if HDR 2D is disabled. However, it is recommended to always use the source_color hint, because it works even if you change renderers or disable HDR 2D.

To group multiple uniforms in a section in the inspector, you can use a group_uniform keyword like this:

You can close the group by using:

The syntax also supports subgroups (it's not mandatory to declare the base group before this):

Sometimes, you want to modify a parameter in many different shaders at once. With a regular uniform, this takes a lot of work as all these shaders need to be tracked and the uniform needs to be set for each of them. Global uniforms allow you to create and update uniforms that will be available in all shaders, in every shader type (canvas_item, spatial, particles, sky and fog).

Global uniforms are especially useful for environmental effects that affect many objects in a scene, like having foliage bend when the player is nearby, or having objects move with the wind.

Global uniforms are not the same as global scope for an individual shader. While regular uniforms are defined outside of shader functions and are therefore the global scope of the shader, global uniforms are global to all shaders in the entire project (but within each shader, are also in the global scope).

To create a global uniform, open the Project Settings then go to the Shader Globals tab. Specify a name for the uniform (case-sensitive) and a type, then click Add in the top-right corner of the dialog. You can then edit the value assigned to the uniform by clicking the value in the list of uniforms:

Adding a global uniform in the Shader Globals tab of the Project Settings

After creating a global uniform, you can use it in a shader as follows:

Note that the global uniform must exist in the Project Settings at the time the shader is saved, or compilation will fail. While you can assign a default value using global uniform vec4 my_color = ... in the shader code, it will be ignored as the global uniform must always be defined in the Project Settings anyway.

To change the value of a global uniform at runtime, use the RenderingServer.global_shader_parameter_set method in a script:

Assigning global uniform values can be done as many times as desired without impacting performance, as setting data doesn't require synchronization between the CPU and GPU.

You can also add or remove global uniforms at runtime:

Adding or removing global uniforms at runtime has a performance cost, although it's not as pronounced compared to getting global uniform values from a script (see the warning below).

While you can query the value of a global uniform at runtime in a script using RenderingServer.global_shader_parameter_get("uniform_name"), this has a large performance penalty as the rendering thread needs to synchronize with the calling thread.

Therefore, it's not recommended to read global shader uniform values continuously in a script. If you need to read values in a script after setting them, consider creating an autoload where you store the values you need to query at the same time you're setting them as global uniforms.

Per-instance uniforms are available in both canvas_item (2D) and spatial (3D) shaders.

Sometimes, you want to modify a parameter on each node using the material. As an example, in a forest full of trees, when you want each tree to have a slightly different color that is editable by hand. Without per-instance uniforms, this requires creating a unique material for each tree (each with a slightly different hue). This makes material management more complex, and also has a performance overhead due to the scene requiring more unique material instances. Vertex colors could also be used here, but they'd require creating unique copies of the mesh for each different color, which also has a performance overhead.

Per-instance uniforms are set on each GeometryInstance3D, rather than on each Material instance. Take this into account when working with meshes that have multiple materials assigned to them, or MultiMesh setups.

After saving the shader, you can change the per-instance uniform's value using the inspector:

Setting a per-instance uniform's value in the GeometryInstance3D section of the inspector

Per-instance uniform values can also be set at runtime using set_instance_shader_parameter method on a node that inherits from GeometryInstance3D:

When using per-instance uniforms, there are some restrictions you should be aware of:

Per-instance uniforms do not support textures or arrays, only regular scalar and vector types.

Due to GLSL limitations, you cannot directly index a texture array using a per-instance uniform. Sampler arrays can only be indexed by compile-time constant expressions.

As a workaround, pass a texture array as a regular uniform and the desired texture index as a per-instance uniform. Then use a switch statement to select the texture:

There is a practical maximum limit of 16 instance uniforms per shader.

If your mesh uses multiple materials, the parameters for the first mesh material found will "win" over the subsequent ones, unless they have the same name, index and type. In this case, all parameters are affected correctly.

If you run into the above situation, you can avoid clashes by manually specifying the index (0-15) of the instance uniform by using the instance_index hint:

You can set uniforms from GDScript using the set_shader_parameter() method:

The first argument to set_shader_parameter() is the name of the uniform in the shader. It must match exactly to the name of the uniform in the shader or else it will not be recognized.

GDScript uses different variable types than GLSL does, so when passing variables from GDScript to shaders, Godot converts the type automatically. Below is a table of the corresponding types:

Bitwise packed int where bit 0 (LSB) corresponds to x.

For example, a bvec2 of (bx, by) could be created in the following way:

Bitwise packed int where bit 0 (LSB) corresponds to x.

Bitwise packed int where bit 0 (LSB) corresponds to x.

When Color is used, it will be interpreted as (r, g, b).

Vector4, Color, Rect2, Plane, Quaternion

When Color is used, it will be interpreted as (r, g, b, a).

When Rect2 is used, it will be interpreted as (position.x, position.y, size.x, size.y).

When Plane is used it will be interpreted as (normal.x, normal.y, normal.z, d).

Projection, Transform3D

When a Transform3D is used, the w Vector is set to the identity.

See Changing import type for instructions on importing cubemaps for use in Godot.

Only supported in Forward+ and Mobile, not Compatibility.

Only supported in Compatibility/Android platform.

Be careful when setting shader uniforms from GDScript, since no error will be thrown if the type does not match. Your shader will just exhibit undefined behavior. Specifically, this includes setting a GDScript int/float (64 bit) into a Godot shader language int/float (32 bit). This may lead to unintended consequences in cases where high precision is required.

There is a limit to the total size of shader uniforms that you can use in a single shader. On most desktop platforms, this limit is 65536 bytes, or 4096 vec4 uniforms. On mobile platforms, the limit is typically 16384 bytes, or 1024 vec4 uniforms. Vector uniforms smaller than a vec4, such as vec2 or vec3, are padded to the size of a vec4. Scalar uniforms such as int or float are not padded, and bool is padded to the size of an int.

Arrays count as the total size of their contents. If you need a uniform array that is larger than this limit, consider packing the data into a texture instead, since the contents of a texture do not count towards this limit, only the size of the sampler uniform.

A large number of built-in variables are available, like UV, COLOR and VERTEX. What variables are available depends on the type of shader (spatial, canvas_item, particle, etc) and the function used (vertex, fragment, light, start, process, sky, or fog). For a list of the built-in variables that are available, please see the corresponding pages:

A large number of built-in functions are supported, conforming to GLSL ES 3.0. See the Built-in functions page for details.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
// Single-line comment.
int a = 2;  // Another single-line comment.

/*
Multi-line comment.
The comment ends when the ending delimiter is found
(here, it's on the line below).
*/
int b = 3;
```

Example 2 (markdown):
```markdown
/**
 * This is a documentation comment.
 * These lines will appear in the inspector when hovering the shader parameter
 * named "Something".
 * You can use [b]BBCode[/b] [i]formatting[/i] in the comment.
 */
uniform int something = 1;
```

Example 3 (unknown):
```unknown
float a = 2; // invalid
float a = 2.0; // valid
float a = float(2); // valid
```

Example 4 (unknown):
```unknown
int a = 2; // valid
uint a = 2; // invalid
uint a = uint(2); // valid
```

---

## Shortcut

**URL:** https://docs.godotengine.org/en/stable/classes/class_shortcut.html

**Contents:**
- Shortcut
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

A shortcut for binding input.

Shortcuts (also known as hotkeys) are containers of InputEvent resources. They are commonly used to interact with a Control element from an InputEvent.

One shortcut can contain multiple InputEvent resources, making it possible to trigger one action with multiple different inputs.

Example: Capture the Ctrl + S shortcut using a Shortcut resource:

has_valid_event() const

matches_event(event: InputEvent) const

void set_events(value: Array)

The shortcut's InputEvent array.

Generally the InputEvent used is an InputEventKey, though it can be any InputEvent, including an InputEventAction.

String get_as_text() const 🔗

Returns the shortcut's first valid InputEvent as a String.

bool has_valid_event() const 🔗

Returns whether events contains an InputEvent which is valid.

bool matches_event(event: InputEvent) const 🔗

Returns whether any InputEvent in events equals event. This uses InputEvent.is_match() to compare events.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Node

var save_shortcut = Shortcut.new()
func _ready():
    var key_event = InputEventKey.new()
    key_event.keycode = KEY_S
    key_event.ctrl_pressed = true
    key_event.command_or_control_autoremap = true # Swaps Ctrl for Command on Mac.
    save_shortcut.events = [key_event]

func _input(event):
    if save_shortcut.matches_event(event) and event.is_pressed() and not event.is_echo():
        print("Save shortcut pressed!")
        get_viewport().set_input_as_handled()
```

Example 2 (swift):
```swift
using Godot;

public partial class MyNode : Node
{
    private readonly Shortcut _saveShortcut = new Shortcut();

    public override void _Ready()
    {
        InputEventKey keyEvent = new InputEventKey
        {
            Keycode = Key.S,
            CtrlPressed = true,
            CommandOrControlAutoremap = true, // Swaps Ctrl for Command on Mac.
        };

        _saveShortcut.Events = [keyEvent];
    }

    public override void _Input(InputEvent @event)
    {
        if (@event is InputEventKey keyEvent &&
            _saveShortcut.MatchesEvent(@event) &&
            keyEvent.Pressed && !keyEvent.Echo)
        {
            GD.Print("Save shortcut pressed!");
            GetViewport().SetInputAsHandled();
        }
    }
}
```

---

## Size and anchors

**URL:** https://docs.godotengine.org/en/stable/tutorials/ui/size_and_anchors.html

**Contents:**
- Size and anchors
- Centering a control
- Anchor Presets
- User-contributed notes

If a game was always going to be run on the same device and at the same resolution, positioning controls would be a simple matter of setting the position and size of each one of them. Unfortunately, that is rarely the case.

While some configurations may be more common than others, devices like phones, tablets and portable gaming consoles can vary greatly. Therefore, we often have to account for different aspect ratios, resolutions and user scaling.

There are several ways to account for this, but for now, let's just imagine that the screen resolution has changed and the controls need to be re-positioned. Some will need to follow the bottom of the screen, others the top of the screen, or maybe the right or left margins.

This is done by editing the anchor offsets of controls, which behave similar to a margin. To access these settings, you will first need to select the Custom anchor preset.

Each control has four anchor offsets: left, right, bottom, and top, which correspond to the respective edges of the control. By default, all of them represent a distance in pixels relative to the top-left corner of the parent control or (in case there is no parent control) the viewport.

So to make the control wider you can make the right offset larger and/or make the left offset smaller. This lets you set the exact placement and shape of the control.

The anchor properties adjust where the offsets are relative to. Each offset has an individual anchor that can be adjusted from the beginning to the end of the parent. So the vertical (top, bottom) anchors adjust from 0.0 (top of parent) to 1.0 (bottom of parent) with 0.5 being the center, and the control offsets will be placed relative to that point. The horizontal (left, right) anchors similarly adjust from left to right of the parent.

Note that when you wish the edge of a control to be above or left of the anchor point, you must change the offset value to be negative.

For example: when horizontal anchors are changed to 1.0, the offset values become relative to the top-right corner of the parent control or viewport.

Adjusting the two horizontal or the two vertical anchors to different values will make the control change size when the parent control does. Here, the control is set to anchor its bottom-right corner to the parent's bottom-right, while the top-left control offsets are still anchored to the top-left of the parent, so when re-sizing the parent, the control will always cover it, leaving a 20 pixel offset:

To center a control in its parent, set its anchors to 0.5 and each offset to half of its relevant dimension. For example, the code below shows how a TextureRect can be centered in its parent:

Setting each anchor to 0.5 moves the reference point for the offsets to the center of its parent. From there, we set negative offsets so that the control gets its natural size.

Instead of manually adjusting the offset and anchor values, you can use the toolbar's Anchor menu, above the viewport. Besides centering, it gives you many options to align and resize control nodes.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var rect = TextureRect.new()
rect.texture = load("res://icon.png")
rect.anchor_left = 0.5
rect.anchor_right = 0.5
rect.anchor_top = 0.5
rect.anchor_bottom = 0.5
var texture_size = rect.texture.get_size()
rect.offset_left = -texture_size.x / 2
rect.offset_right = texture_size.x / 2
rect.offset_top = -texture_size.y / 2
rect.offset_bottom = texture_size.y / 2
add_child(rect)
```

Example 2 (gdscript):
```gdscript
var rect = new TextureRect();

rect.Texture = ResourceLoader.Load<Texture>("res://icon.png");
rect.AnchorLeft = 0.5f;
rect.AnchorRight = 0.5f;
rect.AnchorTop = 0.5f;
rect.AnchorBottom = 0.5f;

var textureSize = rect.Texture.GetSize();

rect.OffsetLeft = -textureSize.X / 2;
rect.OffsetRight = textureSize.X / 2;
rect.OffsetTop = -textureSize.Y / 2;
rect.OffsetBottom = textureSize.Y / 2;
AddChild(rect);
```

---

## SpinBox

**URL:** https://docs.godotengine.org/en/stable/classes/class_spinbox.html

**Contents:**
- SpinBox
- Description
- Properties
- Methods
- Theme Properties
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions
- User-contributed notes

Inherits: Range < Control < CanvasItem < Node < Object

An input field for numbers.

SpinBox is a numerical input text field. It allows entering integers and floating-point numbers. The SpinBox also has up and down buttons that can be clicked increase or decrease the value. The value can also be changed by dragging the mouse up or down over the SpinBox's arrows.

Additionally, mathematical expressions can be entered. These are evaluated when the user presses Enter while editing the SpinBox's text field. This uses the Expression class to parse and evaluate the expression. The result of the expression is then set as the value of the SpinBox. Some examples of valid expressions are 5 + 2 * 3, pow(2, 4), and PI + sin(0.5). Expressions are case-sensitive.

Example: Create a SpinBox, disable its context menu and set its text alignment to right.

See Range class for more options over the SpinBox.

Note: With the SpinBox's context menu disabled, you can right-click the bottom half of the spinbox to set the value to its minimum, while right-clicking the top half sets the value to its maximum.

Note: SpinBox relies on an underlying LineEdit node. To theme a SpinBox's background, add theme items for LineEdit and customize them. The LineEdit has the SpinBoxInnerLineEdit theme variation, so that you can give it a distinct appearance from regular LineEdits.

Note: If you want to implement drag and drop for the underlying LineEdit, you can use Control.set_drag_forwarding() on the node returned by get_line_edit().

1 (overrides Control)

1.0 (overrides Range)

update_on_text_changed

down_disabled_icon_modulate

Color(0.875, 0.875, 0.875, 0.5)

down_hover_icon_modulate

Color(0.95, 0.95, 0.95, 1)

Color(0.875, 0.875, 0.875, 1)

down_pressed_icon_modulate

Color(0.95, 0.95, 0.95, 1)

up_disabled_icon_modulate

Color(0.875, 0.875, 0.875, 0.5)

up_hover_icon_modulate

Color(0.95, 0.95, 0.95, 1)

Color(0.875, 0.875, 0.875, 1)

up_pressed_icon_modulate

Color(0.95, 0.95, 0.95, 1)

buttons_vertical_separation

field_and_buttons_separation

set_min_buttons_width_from_icons

down_background_disabled

down_background_hovered

down_background_pressed

field_and_buttons_separator

up_background_disabled

up_background_hovered

up_background_pressed

up_down_buttons_separator

HorizontalAlignment alignment = 0 🔗

void set_horizontal_alignment(value: HorizontalAlignment)

HorizontalAlignment get_horizontal_alignment()

Changes the alignment of the underlying LineEdit.

float custom_arrow_step = 0.0 🔗

void set_custom_arrow_step(value: float)

float get_custom_arrow_step()

If not 0, sets the step when interacting with the arrow buttons of the SpinBox.

Note: Range.value will still be rounded to a multiple of Range.step.

bool editable = true 🔗

void set_editable(value: bool)

If true, the SpinBox will be editable. Otherwise, it will be read only.

void set_prefix(value: String)

Adds the specified prefix string before the numerical value of the SpinBox.

bool select_all_on_focus = false 🔗

void set_select_all_on_focus(value: bool)

bool is_select_all_on_focus()

If true, the SpinBox will select the whole text when the LineEdit gains focus. Clicking the up and down arrows won't trigger this behavior.

void set_suffix(value: String)

Adds the specified suffix string after the numerical value of the SpinBox.

bool update_on_text_changed = false 🔗

void set_update_on_text_changed(value: bool)

bool get_update_on_text_changed()

Sets the value of the Range for this SpinBox when the LineEdit text is changed instead of submitted. See LineEdit.text_changed and LineEdit.text_submitted.

Note: If set to true, this will interfere with entering mathematical expressions in the SpinBox. The SpinBox will try to evaluate the expression as you type, which means symbols like a trailing + are removed immediately by the expression being evaluated.

Applies the current value of this SpinBox. This is equivalent to pressing Enter while editing the LineEdit used by the SpinBox. This will cause LineEdit.text_submitted to be emitted and its currently contained expression to be evaluated.

LineEdit get_line_edit() 🔗

Returns the LineEdit instance from this SpinBox. You can use it to access properties and methods of LineEdit.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their CanvasItem.visible property.

Color down_disabled_icon_modulate = Color(0.875, 0.875, 0.875, 0.5) 🔗

Down button icon modulation color, when the button is disabled.

Color down_hover_icon_modulate = Color(0.95, 0.95, 0.95, 1) 🔗

Down button icon modulation color, when the button is hovered.

Color down_icon_modulate = Color(0.875, 0.875, 0.875, 1) 🔗

Down button icon modulation color.

Color down_pressed_icon_modulate = Color(0.95, 0.95, 0.95, 1) 🔗

Down button icon modulation color, when the button is being pressed.

Color up_disabled_icon_modulate = Color(0.875, 0.875, 0.875, 0.5) 🔗

Up button icon modulation color, when the button is disabled.

Color up_hover_icon_modulate = Color(0.95, 0.95, 0.95, 1) 🔗

Up button icon modulation color, when the button is hovered.

Color up_icon_modulate = Color(0.875, 0.875, 0.875, 1) 🔗

Up button icon modulation color.

Color up_pressed_icon_modulate = Color(0.95, 0.95, 0.95, 1) 🔗

Up button icon modulation color, when the button is being pressed.

int buttons_vertical_separation = 0 🔗

Vertical separation between the up and down buttons.

int buttons_width = 16 🔗

Width of the up and down buttons. If smaller than any icon set on the buttons, the respective icon may overlap neighboring elements. If smaller than 0, the width is automatically adjusted from the icon size.

int field_and_buttons_separation = 2 🔗

Width of the horizontal separation between the text input field (LineEdit) and the buttons.

int set_min_buttons_width_from_icons = 1 🔗

If not 0, the minimum button width corresponds to the widest of all icons set on those buttons, even if buttons_width is smaller.

Down button icon, displayed in the middle of the down (value-decreasing) button.

Texture2D down_disabled 🔗

Down button icon when the button is disabled.

Texture2D down_hover 🔗

Down button icon when the button is hovered.

Texture2D down_pressed 🔗

Down button icon when the button is being pressed.

Up button icon, displayed in the middle of the up (value-increasing) button.

Texture2D up_disabled 🔗

Up button icon when the button is disabled.

Up button icon when the button is hovered.

Texture2D up_pressed 🔗

Up button icon when the button is being pressed.

Single texture representing both the up and down buttons icons. It is displayed in the middle of the buttons and does not change upon interaction. If a valid icon is assigned, it will replace up and down.

StyleBox down_background 🔗

Background style of the down button.

StyleBox down_background_disabled 🔗

Background style of the down button when disabled.

StyleBox down_background_hovered 🔗

Background style of the down button when hovered.

StyleBox down_background_pressed 🔗

Background style of the down button when being pressed.

StyleBox field_and_buttons_separator 🔗

StyleBox drawn in the space occupied by the separation between the input field and the buttons.

StyleBox up_background 🔗

Background style of the up button.

StyleBox up_background_disabled 🔗

Background style of the up button when disabled.

StyleBox up_background_hovered 🔗

Background style of the up button when hovered.

StyleBox up_background_pressed 🔗

Background style of the up button when being pressed.

StyleBox up_down_buttons_separator 🔗

StyleBox drawn in the space occupied by the separation between the up and down buttons.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var spin_box = SpinBox.new()
add_child(spin_box)
var line_edit = spin_box.get_line_edit()
line_edit.context_menu_enabled = false
spin_box.horizontal_alignment = LineEdit.HORIZONTAL_ALIGNMENT_RIGHT
```

Example 2 (gdscript):
```gdscript
var spinBox = new SpinBox();
AddChild(spinBox);
var lineEdit = spinBox.GetLineEdit();
lineEdit.ContextMenuEnabled = false;
spinBox.AlignHorizontal = LineEdit.HorizontalAlignEnum.Right;
```

---

## SplitContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_splitcontainer.html

**Contents:**
- SplitContainer
- Description
- Tutorials
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions

Inherits: Container < Control < CanvasItem < Node < Object

Inherited By: HSplitContainer, VSplitContainer

A container that splits two child controls horizontally or vertically and provides a grabber for adjusting the split ratio.

A container that accepts only two child controls, then arranges them horizontally or vertically and creates a divisor between them. The divisor can be dragged around to change the size relation between the child controls.

drag_area_highlight_in_editor

drag_area_margin_begin

touch_dragger_enabled

get_drag_area_control()

touch_dragger_hover_color

touch_dragger_pressed_color

minimum_grab_thickness

Emitted when the user ends dragging.

Emitted when the user starts dragging.

dragged(offset: int) 🔗

Emitted when the dragger is dragged by user.

enum DraggerVisibility: 🔗

DraggerVisibility DRAGGER_VISIBLE = 0

The split dragger icon is always visible when autohide is false, otherwise visible only when the cursor hovers it.

The size of the grabber icon determines the minimum separation.

The dragger icon is automatically hidden if the length of the grabber icon is longer than the split bar.

DraggerVisibility DRAGGER_HIDDEN = 1

The split dragger icon is never visible regardless of the value of autohide.

The size of the grabber icon determines the minimum separation.

DraggerVisibility DRAGGER_HIDDEN_COLLAPSED = 2

The split dragger icon is not visible, and the split bar is collapsed to zero thickness.

bool collapsed = false 🔗

void set_collapsed(value: bool)

If true, the dragger will be disabled and the children will be sized as if the split_offset was 0.

bool drag_area_highlight_in_editor = false 🔗

void set_drag_area_highlight_in_editor(value: bool)

bool is_drag_area_highlight_in_editor_enabled()

Highlights the drag area Rect2 so you can see where it is during development. The drag area is gold if dragging_enabled is true, and red if false.

int drag_area_margin_begin = 0 🔗

void set_drag_area_margin_begin(value: int)

int get_drag_area_margin_begin()

Reduces the size of the drag area and split bar split_bar_background at the beginning of the container.

int drag_area_margin_end = 0 🔗

void set_drag_area_margin_end(value: int)

int get_drag_area_margin_end()

Reduces the size of the drag area and split bar split_bar_background at the end of the container.

int drag_area_offset = 0 🔗

void set_drag_area_offset(value: int)

int get_drag_area_offset()

Shifts the drag area in the axis of the container to prevent the drag area from overlapping the ScrollBar or other selectable Control of a child node.

DraggerVisibility dragger_visibility = 0 🔗

void set_dragger_visibility(value: DraggerVisibility)

DraggerVisibility get_dragger_visibility()

Determines the dragger's visibility. This property does not determine whether dragging is enabled or not. Use dragging_enabled for that.

bool dragging_enabled = true 🔗

void set_dragging_enabled(value: bool)

bool is_dragging_enabled()

Enables or disables split dragging.

int split_offset = 0 🔗

void set_split_offset(value: int)

int get_split_offset()

The initial offset of the splitting between the two Controls, with 0 being at the end of the first Control.

bool touch_dragger_enabled = false 🔗

void set_touch_dragger_enabled(value: bool)

bool is_touch_dragger_enabled()

If true, a touch-friendly drag handle will be enabled for better usability on smaller screens. Unlike the standard grabber, this drag handle overlaps the SplitContainer's children and does not affect their minimum separation. The standard grabber will no longer be drawn when this option is enabled.

bool vertical = false 🔗

void set_vertical(value: bool)

If true, the SplitContainer will arrange its children vertically, rather than horizontally.

Can't be changed when using HSplitContainer and VSplitContainer.

void clamp_split_offset() 🔗

Clamps the split_offset value to not go outside the currently possible minimal and maximum values.

Control get_drag_area_control() 🔗

Returns the drag area Control. For example, you can move a pre-configured button into the drag area Control so that it rides along with the split bar. Try setting the Button anchors to center prior to the reparent() call.

Note: The drag area Control is drawn over the SplitContainer's children, so CanvasItem draw objects called from the Control and children added to the Control will also appear over the SplitContainer's children. Try setting Control.mouse_filter of custom children to Control.MOUSE_FILTER_IGNORE to prevent blocking the mouse from dragging if desired.

Warning: This is a required internal node, removing and freeing it may cause a crash.

Color touch_dragger_color = Color(1, 1, 1, 0.3) 🔗

The color of the touch dragger.

Color touch_dragger_hover_color = Color(1, 1, 1, 0.6) 🔗

The color of the touch dragger when hovered.

Color touch_dragger_pressed_color = Color(1, 1, 1, 1) 🔗

The color of the touch dragger when pressed.

Boolean value. If 1 (true), the grabber will hide automatically when it isn't under the cursor. If 0 (false), it's always visible. The dragger_visibility must be DRAGGER_VISIBLE.

int minimum_grab_thickness = 6 🔗

The minimum thickness of the area users can click on to grab the split bar. This ensures that the split bar can still be dragged if separation or h_grabber / v_grabber's size is too narrow to easily select.

int separation = 12 🔗

The split bar thickness, i.e., the gap between the two children of the container. This is overridden by the size of the grabber icon if dragger_visibility is set to DRAGGER_VISIBLE, or DRAGGER_HIDDEN, and separation is smaller than the size of the grabber icon in the same axis.

Note: To obtain separation values less than the size of the grabber icon, for example a 1 px hairline, set h_grabber or v_grabber to a new ImageTexture, which effectively sets the grabber icon size to 0 px.

The icon used for the grabber drawn in the middle area. This is only used in HSplitContainer and VSplitContainer. For SplitContainer, see h_grabber and v_grabber instead.

Texture2D h_grabber 🔗

The icon used for the grabber drawn in the middle area when vertical is false.

Texture2D h_touch_dragger 🔗

The icon used for the drag handle when touch_dragger_enabled is true and vertical is false.

Texture2D touch_dragger 🔗

The icon used for the drag handle when touch_dragger_enabled is true. This is only used in HSplitContainer and VSplitContainer. For SplitContainer, see h_touch_dragger and v_touch_dragger instead.

Texture2D v_grabber 🔗

The icon used for the grabber drawn in the middle area when vertical is true.

Texture2D v_touch_dragger 🔗

The icon used for the drag handle when touch_dragger_enabled is true and vertical is true.

StyleBox split_bar_background 🔗

Determines the background of the split bar if its thickness is greater than zero.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (bash):
```bash
$BarnacleButton.reparent($SplitContainer.get_drag_area_control())
```

---

## StatusIndicator

**URL:** https://docs.godotengine.org/en/stable/classes/class_statusindicator.html

**Contents:**
- StatusIndicator
- Properties
- Methods
- Signals
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Node < Object

Application status indicator (aka notification area icon).

Note: Status indicator is implemented on macOS and Windows.

pressed(mouse_button: int, mouse_position: Vector2i) 🔗

Emitted when the status indicator is pressed.

void set_icon(value: Texture2D)

Status indicator icon.

NodePath menu = NodePath("") 🔗

void set_menu(value: NodePath)

Status indicator native popup menu. If this is set, the pressed signal is not emitted.

Note: Native popup is only supported if NativeMenu supports NativeMenu.FEATURE_POPUP_MENU feature.

String tooltip = "" 🔗

void set_tooltip(value: String)

Status indicator tooltip.

bool visible = true 🔗

void set_visible(value: bool)

If true, the status indicator is visible.

Rect2 get_rect() const 🔗

Returns the status indicator rectangle in screen coordinates. If this status indicator is not visible, returns an empty Rect2.

Please read the User-contributed notes policy before submitting a comment.

---

## StyleBoxEmpty

**URL:** https://docs.godotengine.org/en/stable/classes/class_styleboxempty.html

**Contents:**
- StyleBoxEmpty
- Description
- User-contributed notes

Inherits: StyleBox < Resource < RefCounted < Object

An empty StyleBox (does not display anything).

An empty StyleBox that can be used to display nothing instead of the default style (e.g. it can "disable" focus styles).

Please read the User-contributed notes policy before submitting a comment.

---

## StyleBoxFlat

**URL:** https://docs.godotengine.org/en/stable/classes/class_styleboxflat.html

**Contents:**
- StyleBoxFlat
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: StyleBox < Resource < RefCounted < Object

A customizable StyleBox that doesn't use a texture.

By configuring various properties of this style box, you can achieve many common looks without the need of a texture. This includes optionally rounded borders, antialiasing, shadows, and skew.

Setting corner radius to high values is allowed. As soon as corners overlap, the stylebox will switch to a relative system:

The relative system now would take the 1:2 ratio of the two left corners to calculate the actual corner width. Both corners added will never be more than the height. Result:

Color(0.6, 0.6, 0.6, 1)

Color(0.8, 0.8, 0.8, 1)

corner_radius_bottom_left

corner_radius_bottom_right

corner_radius_top_left

corner_radius_top_right

get_border_width(margin: Side) const

get_border_width_min() const

get_corner_radius(corner: Corner) const

get_expand_margin(margin: Side) const

set_border_width(margin: Side, width: int)

set_border_width_all(width: int)

set_corner_radius(corner: Corner, radius: int)

set_corner_radius_all(radius: int)

set_expand_margin(margin: Side, size: float)

set_expand_margin_all(size: float)

bool anti_aliasing = true 🔗

void set_anti_aliased(value: bool)

bool is_anti_aliased()

Antialiasing draws a small ring around the edges, which fades to transparency. As a result, edges look much smoother. This is only noticeable when using rounded corners or skew.

Note: When using beveled corners with 45-degree angles (corner_detail = 1), it is recommended to set anti_aliasing to false to ensure crisp visuals and avoid possible visual glitches.

float anti_aliasing_size = 1.0 🔗

void set_aa_size(value: float)

This changes the size of the antialiasing effect. 1.0 is recommended for an optimal result at 100% scale, identical to how rounded rectangles are rendered in web browsers and most vector drawing software.

Note: Higher values may produce a blur effect but can also create undesired artifacts on small boxes with large-radius corners.

Color bg_color = Color(0.6, 0.6, 0.6, 1) 🔗

void set_bg_color(value: Color)

The background color of the stylebox.

bool border_blend = false 🔗

void set_border_blend(value: bool)

bool get_border_blend()

If true, the border will fade into the background color.

Color border_color = Color(0.8, 0.8, 0.8, 1) 🔗

void set_border_color(value: Color)

Color get_border_color()

Sets the color of the border.

int border_width_bottom = 0 🔗

void set_border_width(margin: Side, width: int)

int get_border_width(margin: Side) const

Border width for the bottom border.

int border_width_left = 0 🔗

void set_border_width(margin: Side, width: int)

int get_border_width(margin: Side) const

Border width for the left border.

int border_width_right = 0 🔗

void set_border_width(margin: Side, width: int)

int get_border_width(margin: Side) const

Border width for the right border.

int border_width_top = 0 🔗

void set_border_width(margin: Side, width: int)

int get_border_width(margin: Side) const

Border width for the top border.

int corner_detail = 8 🔗

void set_corner_detail(value: int)

int get_corner_detail()

This sets the number of vertices used for each corner. Higher values result in rounder corners but take more processing power to compute. When choosing a value, you should take the corner radius (set_corner_radius_all()) into account.

For corner radii less than 10, 4 or 5 should be enough. For corner radii less than 30, values between 8 and 12 should be enough.

A corner detail of 1 will result in chamfered corners instead of rounded corners, which is useful for some artistic effects.

int corner_radius_bottom_left = 0 🔗

void set_corner_radius(corner: Corner, radius: int)

int get_corner_radius(corner: Corner) const

The bottom-left corner's radius. If 0, the corner is not rounded.

int corner_radius_bottom_right = 0 🔗

void set_corner_radius(corner: Corner, radius: int)

int get_corner_radius(corner: Corner) const

The bottom-right corner's radius. If 0, the corner is not rounded.

int corner_radius_top_left = 0 🔗

void set_corner_radius(corner: Corner, radius: int)

int get_corner_radius(corner: Corner) const

The top-left corner's radius. If 0, the corner is not rounded.

int corner_radius_top_right = 0 🔗

void set_corner_radius(corner: Corner, radius: int)

int get_corner_radius(corner: Corner) const

The top-right corner's radius. If 0, the corner is not rounded.

bool draw_center = true 🔗

void set_draw_center(value: bool)

bool is_draw_center_enabled()

Toggles drawing of the inner part of the stylebox.

float expand_margin_bottom = 0.0 🔗

void set_expand_margin(margin: Side, size: float)

float get_expand_margin(margin: Side) const

Expands the stylebox outside of the control rect on the bottom edge. Useful in combination with border_width_bottom to draw a border outside the control rect.

Note: Unlike StyleBox.content_margin_bottom, expand_margin_bottom does not affect the size of the clickable area for Controls. This can negatively impact usability if used wrong, as the user may try to click an area of the StyleBox that cannot actually receive clicks.

float expand_margin_left = 0.0 🔗

void set_expand_margin(margin: Side, size: float)

float get_expand_margin(margin: Side) const

Expands the stylebox outside of the control rect on the left edge. Useful in combination with border_width_left to draw a border outside the control rect.

Note: Unlike StyleBox.content_margin_left, expand_margin_left does not affect the size of the clickable area for Controls. This can negatively impact usability if used wrong, as the user may try to click an area of the StyleBox that cannot actually receive clicks.

float expand_margin_right = 0.0 🔗

void set_expand_margin(margin: Side, size: float)

float get_expand_margin(margin: Side) const

Expands the stylebox outside of the control rect on the right edge. Useful in combination with border_width_right to draw a border outside the control rect.

Note: Unlike StyleBox.content_margin_right, expand_margin_right does not affect the size of the clickable area for Controls. This can negatively impact usability if used wrong, as the user may try to click an area of the StyleBox that cannot actually receive clicks.

float expand_margin_top = 0.0 🔗

void set_expand_margin(margin: Side, size: float)

float get_expand_margin(margin: Side) const

Expands the stylebox outside of the control rect on the top edge. Useful in combination with border_width_top to draw a border outside the control rect.

Note: Unlike StyleBox.content_margin_top, expand_margin_top does not affect the size of the clickable area for Controls. This can negatively impact usability if used wrong, as the user may try to click an area of the StyleBox that cannot actually receive clicks.

Color shadow_color = Color(0, 0, 0, 0.6) 🔗

void set_shadow_color(value: Color)

Color get_shadow_color()

The color of the shadow. This has no effect if shadow_size is lower than 1.

Vector2 shadow_offset = Vector2(0, 0) 🔗

void set_shadow_offset(value: Vector2)

Vector2 get_shadow_offset()

The shadow offset in pixels. Adjusts the position of the shadow relatively to the stylebox.

int shadow_size = 0 🔗

void set_shadow_size(value: int)

int get_shadow_size()

The shadow size in pixels.

Vector2 skew = Vector2(0, 0) 🔗

void set_skew(value: Vector2)

If set to a non-zero value on either axis, skew distorts the StyleBox horizontally and/or vertically. This can be used for "futuristic"-style UIs. Positive values skew the StyleBox towards the right (X axis) and upwards (Y axis), while negative values skew the StyleBox towards the left (X axis) and downwards (Y axis).

Note: To ensure text does not touch the StyleBox's edges, consider increasing the StyleBox's content margin (see StyleBox.content_margin_bottom). It is preferable to increase the content margin instead of the expand margin (see expand_margin_bottom), as increasing the expand margin does not increase the size of the clickable area for Controls.

int get_border_width(margin: Side) const 🔗

Returns the specified Side's border width.

int get_border_width_min() const 🔗

Returns the smallest border width out of all four borders.

int get_corner_radius(corner: Corner) const 🔗

Returns the given corner's radius.

float get_expand_margin(margin: Side) const 🔗

Returns the size of the specified Side's expand margin.

void set_border_width(margin: Side, width: int) 🔗

Sets the specified Side's border width to width pixels.

void set_border_width_all(width: int) 🔗

Sets the border width to width pixels for all sides.

void set_corner_radius(corner: Corner, radius: int) 🔗

Sets the corner radius to radius pixels for the given corner.

void set_corner_radius_all(radius: int) 🔗

Sets the corner radius to radius pixels for all corners.

void set_expand_margin(margin: Side, size: float) 🔗

Sets the expand margin to size pixels for the specified Side.

void set_expand_margin_all(size: float) 🔗

Sets the expand margin to size pixels for all sides.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
height = 30
corner_radius_top_left = 50
corner_radius_bottom_left = 100
```

Example 2 (yaml):
```yaml
corner_radius_top_left: 10
corner_radius_bottom_left: 20
```

---

## StyleBoxLine

**URL:** https://docs.godotengine.org/en/stable/classes/class_styleboxline.html

**Contents:**
- StyleBoxLine
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: StyleBox < Resource < RefCounted < Object

A StyleBox that displays a single line of a given color and thickness.

A StyleBox that displays a single line of a given color and thickness. The line can be either horizontal or vertical. Useful for separators.

Color color = Color(0, 0, 0, 1) 🔗

void set_color(value: Color)

float grow_begin = 1.0 🔗

void set_grow_begin(value: float)

float get_grow_begin()

The number of pixels the line will extend before the StyleBoxLine's bounds. If set to a negative value, the line will begin inside the StyleBoxLine's bounds.

float grow_end = 1.0 🔗

void set_grow_end(value: float)

The number of pixels the line will extend past the StyleBoxLine's bounds. If set to a negative value, the line will end inside the StyleBoxLine's bounds.

void set_thickness(value: int)

The line's thickness in pixels.

bool vertical = false 🔗

void set_vertical(value: bool)

If true, the line will be vertical. If false, the line will be horizontal.

Please read the User-contributed notes policy before submitting a comment.

---

## StyleBoxTexture

**URL:** https://docs.godotengine.org/en/stable/classes/class_styleboxtexture.html

**Contents:**
- StyleBoxTexture
- Description
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: StyleBox < Resource < RefCounted < Object

A texture-based nine-patch StyleBox.

A texture-based nine-patch StyleBox, in a way similar to NinePatchRect. This stylebox performs a 3×3 scaling of a texture, where only the center cell is fully stretched. This makes it possible to design bordered styles regardless of the stylebox's size.

axis_stretch_horizontal

axis_stretch_vertical

texture_margin_bottom

get_expand_margin(margin: Side) const

get_texture_margin(margin: Side) const

set_expand_margin(margin: Side, size: float)

set_expand_margin_all(size: float)

set_texture_margin(margin: Side, size: float)

set_texture_margin_all(size: float)

enum AxisStretchMode: 🔗

AxisStretchMode AXIS_STRETCH_MODE_STRETCH = 0

Stretch the stylebox's texture. This results in visible distortion unless the texture size matches the stylebox's size perfectly.

AxisStretchMode AXIS_STRETCH_MODE_TILE = 1

Repeats the stylebox's texture to match the stylebox's size according to the nine-patch system.

AxisStretchMode AXIS_STRETCH_MODE_TILE_FIT = 2

Repeats the stylebox's texture to match the stylebox's size according to the nine-patch system. Unlike AXIS_STRETCH_MODE_TILE, the texture may be slightly stretched to make the nine-patch texture tile seamlessly.

AxisStretchMode axis_stretch_horizontal = 0 🔗

void set_h_axis_stretch_mode(value: AxisStretchMode)

AxisStretchMode get_h_axis_stretch_mode()

Controls how the stylebox's texture will be stretched or tiled horizontally.

AxisStretchMode axis_stretch_vertical = 0 🔗

void set_v_axis_stretch_mode(value: AxisStretchMode)

AxisStretchMode get_v_axis_stretch_mode()

Controls how the stylebox's texture will be stretched or tiled vertically.

bool draw_center = true 🔗

void set_draw_center(value: bool)

bool is_draw_center_enabled()

If true, the nine-patch texture's center tile will be drawn.

float expand_margin_bottom = 0.0 🔗

void set_expand_margin(margin: Side, size: float)

float get_expand_margin(margin: Side) const

Expands the bottom margin of this style box when drawing, causing it to be drawn larger than requested.

float expand_margin_left = 0.0 🔗

void set_expand_margin(margin: Side, size: float)

float get_expand_margin(margin: Side) const

Expands the left margin of this style box when drawing, causing it to be drawn larger than requested.

float expand_margin_right = 0.0 🔗

void set_expand_margin(margin: Side, size: float)

float get_expand_margin(margin: Side) const

Expands the right margin of this style box when drawing, causing it to be drawn larger than requested.

float expand_margin_top = 0.0 🔗

void set_expand_margin(margin: Side, size: float)

float get_expand_margin(margin: Side) const

Expands the top margin of this style box when drawing, causing it to be drawn larger than requested.

Color modulate_color = Color(1, 1, 1, 1) 🔗

void set_modulate(value: Color)

Modulates the color of the texture when this style box is drawn.

Rect2 region_rect = Rect2(0, 0, 0, 0) 🔗

void set_region_rect(value: Rect2)

Rect2 get_region_rect()

The region to use from the texture.

This is equivalent to first wrapping the texture in an AtlasTexture with the same region.

If empty (Rect2(0, 0, 0, 0)), the whole texture is used.

void set_texture(value: Texture2D)

Texture2D get_texture()

The texture to use when drawing this style box.

float texture_margin_bottom = 0.0 🔗

void set_texture_margin(margin: Side, size: float)

float get_texture_margin(margin: Side) const

Increases the bottom margin of the 3×3 texture box.

A higher value means more of the source texture is considered to be part of the bottom border of the 3×3 box.

This is also the value used as fallback for StyleBox.content_margin_bottom if it is negative.

float texture_margin_left = 0.0 🔗

void set_texture_margin(margin: Side, size: float)

float get_texture_margin(margin: Side) const

Increases the left margin of the 3×3 texture box.

A higher value means more of the source texture is considered to be part of the left border of the 3×3 box.

This is also the value used as fallback for StyleBox.content_margin_left if it is negative.

float texture_margin_right = 0.0 🔗

void set_texture_margin(margin: Side, size: float)

float get_texture_margin(margin: Side) const

Increases the right margin of the 3×3 texture box.

A higher value means more of the source texture is considered to be part of the right border of the 3×3 box.

This is also the value used as fallback for StyleBox.content_margin_right if it is negative.

float texture_margin_top = 0.0 🔗

void set_texture_margin(margin: Side, size: float)

float get_texture_margin(margin: Side) const

Increases the top margin of the 3×3 texture box.

A higher value means more of the source texture is considered to be part of the top border of the 3×3 box.

This is also the value used as fallback for StyleBox.content_margin_top if it is negative.

float get_expand_margin(margin: Side) const 🔗

Returns the expand margin size of the specified Side.

float get_texture_margin(margin: Side) const 🔗

Returns the margin size of the specified Side.

void set_expand_margin(margin: Side, size: float) 🔗

Sets the expand margin to size pixels for the specified Side.

void set_expand_margin_all(size: float) 🔗

Sets the expand margin to size pixels for all sides.

void set_texture_margin(margin: Side, size: float) 🔗

Sets the margin to size pixels for the specified Side.

void set_texture_margin_all(size: float) 🔗

Sets the margin to size pixels for all sides.

Please read the User-contributed notes policy before submitting a comment.

---

## StyleBox

**URL:** https://docs.godotengine.org/en/stable/classes/class_stylebox.html

**Contents:**
- StyleBox
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: StyleBoxEmpty, StyleBoxFlat, StyleBoxLine, StyleBoxTexture

Abstract base class for defining stylized boxes for UI elements.

StyleBox is an abstract base class for drawing stylized boxes for UI elements. It is used for panels, buttons, LineEdit backgrounds, Tree backgrounds, etc. and also for testing a transparency mask for pointer signals. If mask test fails on a StyleBox assigned as mask to a control, clicks and motion signals will go through it to the one below.

Note: For control nodes that have Theme Properties, the focus StyleBox is displayed over the normal, hover or pressed StyleBox. This makes the focus StyleBox more reusable across different nodes.

content_margin_bottom

_draw(to_canvas_item: RID, rect: Rect2) virtual required const

_get_draw_rect(rect: Rect2) virtual const

_get_minimum_size() virtual const

_test_mask(point: Vector2, rect: Rect2) virtual const

draw(canvas_item: RID, rect: Rect2) const

get_content_margin(margin: Side) const

get_current_item_drawn() const

get_margin(margin: Side) const

get_minimum_size() const

set_content_margin(margin: Side, offset: float)

set_content_margin_all(offset: float)

test_mask(point: Vector2, rect: Rect2) const

float content_margin_bottom = -1.0 🔗

void set_content_margin(margin: Side, offset: float)

float get_content_margin(margin: Side) const

The bottom margin for the contents of this style box. Increasing this value reduces the space available to the contents from the bottom.

If this value is negative, it is ignored and a child-specific margin is used instead. For example, for StyleBoxFlat, the border thickness (if any) is used instead.

It is up to the code using this style box to decide what these contents are: for example, a Button respects this content margin for the textual contents of the button.

get_margin() should be used to fetch this value as consumer instead of reading these properties directly. This is because it correctly respects negative values and the fallback mentioned above.

float content_margin_left = -1.0 🔗

void set_content_margin(margin: Side, offset: float)

float get_content_margin(margin: Side) const

The left margin for the contents of this style box. Increasing this value reduces the space available to the contents from the left.

Refer to content_margin_bottom for extra considerations.

float content_margin_right = -1.0 🔗

void set_content_margin(margin: Side, offset: float)

float get_content_margin(margin: Side) const

The right margin for the contents of this style box. Increasing this value reduces the space available to the contents from the right.

Refer to content_margin_bottom for extra considerations.

float content_margin_top = -1.0 🔗

void set_content_margin(margin: Side, offset: float)

float get_content_margin(margin: Side) const

The top margin for the contents of this style box. Increasing this value reduces the space available to the contents from the top.

Refer to content_margin_bottom for extra considerations.

void _draw(to_canvas_item: RID, rect: Rect2) virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

Rect2 _get_draw_rect(rect: Rect2) virtual const 🔗

There is currently no description for this method. Please help us by contributing one!

Vector2 _get_minimum_size() virtual const 🔗

Virtual method to be implemented by the user. Returns a custom minimum size that the stylebox must respect when drawing. By default get_minimum_size() only takes content margins into account. This method can be overridden to add another size restriction. A combination of the default behavior and the output of this method will be used, to account for both sizes.

bool _test_mask(point: Vector2, rect: Rect2) virtual const 🔗

There is currently no description for this method. Please help us by contributing one!

void draw(canvas_item: RID, rect: Rect2) const 🔗

Draws this stylebox using a canvas item identified by the given RID.

The RID value can either be the result of CanvasItem.get_canvas_item() called on an existing CanvasItem-derived node, or directly from creating a canvas item in the RenderingServer with RenderingServer.canvas_item_create().

float get_content_margin(margin: Side) const 🔗

Returns the default margin of the specified Side.

CanvasItem get_current_item_drawn() const 🔗

Returns the CanvasItem that handles its CanvasItem.NOTIFICATION_DRAW or CanvasItem._draw() callback at this moment.

float get_margin(margin: Side) const 🔗

Returns the content margin offset for the specified Side.

Positive values reduce size inwards, unlike Control's margin values.

Vector2 get_minimum_size() const 🔗

Returns the minimum size that this stylebox can be shrunk to.

Vector2 get_offset() const 🔗

Returns the "offset" of a stylebox. This helper function returns a value equivalent to Vector2(style.get_margin(MARGIN_LEFT), style.get_margin(MARGIN_TOP)).

void set_content_margin(margin: Side, offset: float) 🔗

Sets the default value of the specified Side to offset pixels.

void set_content_margin_all(offset: float) 🔗

Sets the default margin to offset pixels for all sides.

bool test_mask(point: Vector2, rect: Rect2) const 🔗

Test a position in a rectangle, return whether it passes the mask test.

Please read the User-contributed notes policy before submitting a comment.

---

## SubViewportContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_subviewportcontainer.html

**Contents:**
- SubViewportContainer
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Container < Control < CanvasItem < Node < Object

A container used for displaying the contents of a SubViewport.

A container that displays the contents of underlying SubViewport child nodes. It uses the combined size of the SubViewports as minimum size, unless stretch is enabled.

Note: Changing a SubViewportContainer's Control.scale will cause its contents to appear distorted. To change its visual size without causing distortion, adjust the node's margins instead (if it's not already in a container).

Note: The SubViewportContainer forwards mouse-enter and mouse-exit notifications to its sub-viewports.

1 (overrides Control)

_propagate_input_event(event: InputEvent) virtual const

bool mouse_target = false 🔗

void set_mouse_target(value: bool)

bool is_mouse_target_enabled()

Configure, if either the SubViewportContainer or alternatively the Control nodes of its SubViewport children should be available as targets of mouse-related functionalities, like identifying the drop target in drag-and-drop operations or cursor shape of hovered Control node.

If false, the Control nodes inside its SubViewport children are considered as targets.

If true, the SubViewportContainer itself will be considered as a target.

bool stretch = false 🔗

void set_stretch(value: bool)

bool is_stretch_enabled()

If true, the sub-viewport will be automatically resized to the control's size.

Note: If true, this will prohibit changing SubViewport.size of its children manually.

int stretch_shrink = 1 🔗

void set_stretch_shrink(value: int)

int get_stretch_shrink()

Divides the sub-viewport's effective resolution by this value while preserving its scale. This can be used to speed up rendering.

For example, a 1280×720 sub-viewport with stretch_shrink set to 2 will be rendered at 640×360 while occupying the same size in the container.

Note: stretch must be true for this property to work.

bool _propagate_input_event(event: InputEvent) virtual const 🔗

Experimental: This method may be changed or removed in future versions.

Virtual method to be implemented by the user. If it returns true, the event is propagated to SubViewport children. Propagation doesn't happen if it returns false. If the function is not implemented, all events are propagated to SubViewports.

Please read the User-contributed notes policy before submitting a comment.

---

## SubViewport

**URL:** https://docs.godotengine.org/en/stable/classes/class_subviewport.html

**Contents:**
- SubViewport
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: Viewport < Node < Object

An interface to a game world that doesn't create a window or draw to the screen directly.

SubViewport Isolates a rectangular region of a scene to be displayed independently. This can be used, for example, to display UI in 3D space.

Note: SubViewport is a Viewport that isn't a Window, i.e. it doesn't draw anything by itself. To display anything, SubViewport must have a non-zero size and be either put inside a SubViewportContainer or assigned to a ViewportTexture.

Note: InputEvents are not passed to a standalone SubViewport by default. To ensure InputEvent propagation, a SubViewport can be placed inside of a SubViewportContainer.

Viewport and canvas transforms

GUI in 3D Viewport Demo

3D in 2D Viewport Demo

2D in 3D Viewport Demo

Dynamic Split Screen Demo

3D Resolution Scaling Demo

render_target_clear_mode

render_target_update_mode

size_2d_override_stretch

ClearMode CLEAR_MODE_ALWAYS = 0

Always clear the render target before drawing.

ClearMode CLEAR_MODE_NEVER = 1

Never clear the render target.

ClearMode CLEAR_MODE_ONCE = 2

Clear the render target on the next frame, then switch to CLEAR_MODE_NEVER.

UpdateMode UPDATE_DISABLED = 0

Do not update the render target.

UpdateMode UPDATE_ONCE = 1

Update the render target once, then switch to UPDATE_DISABLED.

UpdateMode UPDATE_WHEN_VISIBLE = 2

Update the render target only when it is visible. This is the default value.

UpdateMode UPDATE_WHEN_PARENT_VISIBLE = 3

Update the render target only when its parent is visible.

UpdateMode UPDATE_ALWAYS = 4

Always update the render target.

ClearMode render_target_clear_mode = 0 🔗

void set_clear_mode(value: ClearMode)

ClearMode get_clear_mode()

The clear mode when the sub-viewport is used as a render target.

Note: This property is intended for 2D usage.

UpdateMode render_target_update_mode = 2 🔗

void set_update_mode(value: UpdateMode)

UpdateMode get_update_mode()

The update mode when the sub-viewport is used as a render target.

Vector2i size = Vector2i(512, 512) 🔗

void set_size(value: Vector2i)

The width and height of the sub-viewport. Must be set to a value greater than or equal to 2 pixels on both dimensions. Otherwise, nothing will be displayed.

Note: If the parent node is a SubViewportContainer and its SubViewportContainer.stretch is true, the viewport size cannot be changed manually.

Vector2i size_2d_override = Vector2i(0, 0) 🔗

void set_size_2d_override(value: Vector2i)

Vector2i get_size_2d_override()

The 2D size override of the sub-viewport. If either the width or height is 0, the override is disabled.

bool size_2d_override_stretch = false 🔗

void set_size_2d_override_stretch(value: bool)

bool is_size_2d_override_stretch_enabled()

If true, the 2D size override affects stretch as well.

Please read the User-contributed notes policy before submitting a comment.

---

## Support different actor types

**URL:** https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_different_actor_types.html

**Contents:**
- Support different actor types
- User-contributed notes

To support different actor types due to e.g. their sizes each type requires its own navigation map and navigation mesh baked with an appropriated agent radius and height. The same approach can be used to distinguish between e.g. landwalking, swimming or flying agents.

Agents are exclusively defined by a radius and height value for baking navigation meshes, pathfinding and avoidance. More complex shapes are not supported.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
# Create a navigation mesh resource for each actor size.
var navigation_mesh_standard_size: NavigationMesh = NavigationMesh.new()
var navigation_mesh_small_size: NavigationMesh = NavigationMesh.new()
var navigation_mesh_huge_size: NavigationMesh = NavigationMesh.new()

# Set appropriated agent parameters.
navigation_mesh_standard_size.agent_radius = 0.5
navigation_mesh_standard_size.agent_height = 1.8
navigation_mesh_small_size.agent_radius = 0.25
navigation_mesh_small_size.agent_height = 0.7
navigation_mesh_huge_size.agent_radius = 1.5
navigation_mesh_huge_size.agent_height = 2.5

# Get the root node to parse geometry for the baking.
var root_node: Node3D = get_node("NavigationMeshBakingRootNode")

# Create the source geometry resource that will hold the parsed geometry data.
var source_geometry_data: NavigationMeshSourceGeometryData3D = NavigationMeshSourceGeometryData3D.new()

# Parse the source geometry from the scene tree on the main thread.
# The navigation mesh is only required for the parse settings so any of the three will do.
NavigationServer3D.parse_source_geometry_data(navigation_mesh_standard_size, source_geometry_data, root_node)

# Bake the navigation geometry for each agent size from the same source geometry.
# If required for performance this baking step could also be done on background threads.
NavigationServer3D.bake_from_source_geometry_data(navigation_mesh_standard_size, source_geometry_data)
NavigationServer3D.bake_from_source_geometry_data(navigation_mesh_small_size, source_geometry_data)
NavigationServer3D.bake_from_source_geometry_data(navigation_mesh_huge_size, source_geometry_data)

# Create different navigation maps on the NavigationServer.
var navigation_map_standard: RID = NavigationServer3D.map_create()
var navigation_map_small: RID = NavigationServer3D.map_create()
var navigation_map_huge: RID = NavigationServer3D.map_create()

# Set the new navigation maps as active.
NavigationServer3D.map_set_active(navigation_map_standard, true)
NavigationServer3D.map_set_active(navigation_map_small, true)
NavigationServer3D.map_set_active(navigation_map_huge, true)

# Create a region for each map.
var navigation_region_standard: RID = NavigationServer3D.region_create()
var navigation_region_small: RID = NavigationServer3D.region_create()
var navigation_region_huge: RID = NavigationServer3D.region_create()

# Add the regions to the maps.
NavigationServer3D.region_set_map(navigation_region_standard, navigation_map_standard)
NavigationServer3D.region_set_map(navigation_region_small, navigation_map_small)
NavigationServer3D.region_set_map(navigation_region_huge, navigation_map_huge)

# Set navigation mesh for each region.
NavigationServer3D.region_set_navigation_mesh(navigation_region_standard, navigation_mesh_standard_size)
NavigationServer3D.region_set_navigation_mesh(navigation_region_small, navigation_mesh_small_size)
NavigationServer3D.region_set_navigation_mesh(navigation_region_huge, navigation_mesh_huge_size)

# Create start and end position for the navigation path query.
var start_pos: Vector3 = Vector3(0.0, 0.0, 0.0)
var end_pos: Vector3 = Vector3(2.0, 0.0, 0.0)
var use_corridorfunnel: bool = true

# Query paths for each agent size.
var path_standard_agent = NavigationServer3D.map_get_path(navigation_map_standard, start_pos, end_pos, use_corridorfunnel)
var path_small_agent = NavigationServer3D.map_get_path(navigation_map_small, start_pos, end_pos, use_corridorfunnel)
var path_huge_agent = NavigationServer3D.map_get_path(navigation_map_huge, start_pos, end_pos, use_corridorfunnel)
```

Example 2 (swift):
```swift
// Create a navigation mesh resource for each actor size.
NavigationMesh navigationMeshStandardSize = new NavigationMesh();
NavigationMesh navigationMeshSmallSize = new NavigationMesh();
NavigationMesh navigationMeshHugeSize = new NavigationMesh();

// Set appropriated agent parameters.
navigationMeshStandardSize.AgentRadius = 0.5f;
navigationMeshStandardSize.AgentHeight = 1.8f;
navigationMeshSmallSize.AgentRadius = 0.25f;
navigationMeshSmallSize.AgentHeight = 0.7f;
navigationMeshHugeSize.AgentRadius = 1.5f;
navigationMeshHugeSize.AgentHeight = 2.5f;

// Get the root node to parse geometry for the baking.
Node3D rootNode = GetNode<Node3D>("NavigationMeshBakingRootNode");

// Create the source geometry resource that will hold the parsed geometry data.
NavigationMeshSourceGeometryData3D sourceGeometryData = new NavigationMeshSourceGeometryData3D();

// Parse the source geometry from the scene tree on the main thread.
// The navigation mesh is only required for the parse settings so any of the three will do.
NavigationServer3D.ParseSourceGeometryData(navigationMeshStandardSize, sourceGeometryData, rootNode);

// Bake the navigation geometry for each agent size from the same source geometry.
// If required for performance this baking step could also be done on background threads.
NavigationServer3D.BakeFromSourceGeometryData(navigationMeshStandardSize, sourceGeometryData);
NavigationServer3D.BakeFromSourceGeometryData(navigationMeshSmallSize, sourceGeometryData);
NavigationServer3D.BakeFromSourceGeometryData(navigationMeshHugeSize, sourceGeometryData);

// Create different navigation maps on the NavigationServer.
Rid navigationMapStandard = NavigationServer3D.MapCreate();
Rid navigationMapSmall = NavigationServer3D.MapCreate();
Rid navigationMapHuge = NavigationServer3D.MapCreate();

// Set the new navigation maps as active.
NavigationServer3D.MapSetActive(navigationMapStandard, true);
NavigationServer3D.MapSetActive(navigationMapSmall, true);
NavigationServer3D.MapSetActive(navigationMapHuge, true);

// Create a region for each map.
Rid navigationRegionStandard = NavigationServer3D.RegionCreate();
Rid navigationRegionSmall = NavigationServer3D.RegionCreate();
Rid navigationRegionHuge = NavigationServer3D.RegionCreate();

// Add the regions to the maps.
NavigationServer3D.RegionSetMap(navigationRegionStandard, navigationMapStandard);
NavigationServer3D.RegionSetMap(navigationRegionSmall, navigationMapSmall);
NavigationServer3D.RegionSetMap(navigationRegionHuge, navigationMapHuge);

// Set navigation mesh for each region.
NavigationServer3D.RegionSetNavigationMesh(navigationRegionStandard, navigationMeshStandardSize);
NavigationServer3D.RegionSetNavigationMesh(navigationRegionSmall, navigationMeshSmallSize);
NavigationServer3D.RegionSetNavigationMesh(navigationRegionHuge, navigationMeshHugeSize);

// Create start and end position for the navigation path query.
Vector3 startPos = new Vector3(0.0f, 0.0f, 0.0f);
Vector3 endPos = new Vector3(2.0f, 0.0f, 0.0f);
bool useCorridorFunnel = true;

// Query paths for each agent size.
var pathStandardAgent = NavigationServer3D.MapGetPath(navigationMapStandard, startPos, endPos, useCorridorFunnel);
var pathSmallAgent = NavigationServer3D.MapGetPath(navigationMapSmall, startPos, endPos, useCorridorFunnel);
var pathHugeAgent = NavigationServer3D.MapGetPath(navigationMapHuge, startPos, endPos, useCorridorFunnel);
```

---

## TabBar

**URL:** https://docs.godotengine.org/en/stable/classes/class_tabbar.html

**Contents:**
- TabBar
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions

Inherits: Control < CanvasItem < Node < Object

A control that provides a horizontal bar with tabs.

A control that provides a horizontal bar with tabs. Similar to TabContainer but is only in charge of drawing tabs, not interacting with children.

close_with_middle_mouse

drag_to_rearrange_enabled

2 (overrides Control)

CloseButtonDisplayPolicy

tab_close_display_policy

add_tab(title: String = "", icon: Texture2D = null)

ensure_tab_visible(idx: int)

get_offset_buttons_visible() const

get_previous_tab() const

get_tab_button_icon(tab_idx: int) const

get_tab_icon(tab_idx: int) const

get_tab_icon_max_width(tab_idx: int) const

get_tab_idx_at_point(point: Vector2) const

get_tab_language(tab_idx: int) const

get_tab_metadata(tab_idx: int) const

get_tab_offset() const

get_tab_rect(tab_idx: int) const

get_tab_text_direction(tab_idx: int) const

get_tab_title(tab_idx: int) const

get_tab_tooltip(tab_idx: int) const

is_tab_disabled(tab_idx: int) const

is_tab_hidden(tab_idx: int) const

move_tab(from: int, to: int)

remove_tab(tab_idx: int)

select_next_available()

select_previous_available()

set_tab_button_icon(tab_idx: int, icon: Texture2D)

set_tab_disabled(tab_idx: int, disabled: bool)

set_tab_hidden(tab_idx: int, hidden: bool)

set_tab_icon(tab_idx: int, icon: Texture2D)

set_tab_icon_max_width(tab_idx: int, width: int)

set_tab_language(tab_idx: int, language: String)

set_tab_metadata(tab_idx: int, metadata: Variant)

set_tab_text_direction(tab_idx: int, direction: TextDirection)

set_tab_title(tab_idx: int, title: String)

set_tab_tooltip(tab_idx: int, tooltip: String)

Color(0.875, 0.875, 0.875, 0.5)

Color(0.95, 0.95, 0.95, 1)

Color(0.95, 0.95, 0.95, 1)

font_unselected_color

Color(0.7, 0.7, 0.7, 1)

active_tab_rearranged(idx_to: int) 🔗

Emitted when the active tab is rearranged via mouse drag. See drag_to_rearrange_enabled.

tab_button_pressed(tab: int) 🔗

Emitted when a tab's right button is pressed. See set_tab_button_icon().

tab_changed(tab: int) 🔗

Emitted when switching to another tab.

tab_clicked(tab: int) 🔗

Emitted when a tab is clicked, even if it is the current tab.

tab_close_pressed(tab: int) 🔗

Emitted when a tab's close button is pressed or when middle-clicking on a tab, if close_with_middle_mouse is enabled.

Note: Tabs are not removed automatically once the close button is pressed, this behavior needs to be programmed manually. For example:

tab_hovered(tab: int) 🔗

Emitted when a tab is hovered by the mouse.

tab_rmb_clicked(tab: int) 🔗

Emitted when a tab is right-clicked. select_with_rmb must be enabled.

tab_selected(tab: int) 🔗

Emitted when a tab is selected via click, directional input, or script, even if it is the current tab.

enum AlignmentMode: 🔗

AlignmentMode ALIGNMENT_LEFT = 0

Places tabs to the left.

AlignmentMode ALIGNMENT_CENTER = 1

Places tabs in the middle.

AlignmentMode ALIGNMENT_RIGHT = 2

Places tabs to the right.

AlignmentMode ALIGNMENT_MAX = 3

Represents the size of the AlignmentMode enum.

enum CloseButtonDisplayPolicy: 🔗

CloseButtonDisplayPolicy CLOSE_BUTTON_SHOW_NEVER = 0

Never show the close buttons.

CloseButtonDisplayPolicy CLOSE_BUTTON_SHOW_ACTIVE_ONLY = 1

Only show the close button on the currently active tab.

CloseButtonDisplayPolicy CLOSE_BUTTON_SHOW_ALWAYS = 2

Show the close button on all tabs.

CloseButtonDisplayPolicy CLOSE_BUTTON_MAX = 3

Represents the size of the CloseButtonDisplayPolicy enum.

bool clip_tabs = true 🔗

void set_clip_tabs(value: bool)

If true, tabs overflowing this node's width will be hidden, displaying two navigation buttons instead. Otherwise, this node's minimum size is updated so that all tabs are visible.

bool close_with_middle_mouse = true 🔗

void set_close_with_middle_mouse(value: bool)

bool get_close_with_middle_mouse()

If true, middle clicking on the mouse will fire the tab_close_pressed signal.

int current_tab = -1 🔗

void set_current_tab(value: int)

int get_current_tab()

The index of the current selected tab. A value of -1 means that no tab is selected and can only be set when deselect_enabled is true or if all tabs are hidden or disabled.

bool deselect_enabled = false 🔗

void set_deselect_enabled(value: bool)

bool get_deselect_enabled()

If true, all tabs can be deselected so that no tab is selected. Click on the current tab to deselect it.

bool drag_to_rearrange_enabled = false 🔗

void set_drag_to_rearrange_enabled(value: bool)

bool get_drag_to_rearrange_enabled()

If true, tabs can be rearranged with mouse drag.

int max_tab_width = 0 🔗

void set_max_tab_width(value: int)

int get_max_tab_width()

Sets the maximum width which all tabs should be limited to. Unlimited if set to 0.

bool scroll_to_selected = true 🔗

void set_scroll_to_selected(value: bool)

bool get_scroll_to_selected()

If true, the tab offset will be changed to keep the currently selected tab visible.

bool scrolling_enabled = true 🔗

void set_scrolling_enabled(value: bool)

bool get_scrolling_enabled()

if true, the mouse's scroll wheel can be used to navigate the scroll view.

bool select_with_rmb = false 🔗

void set_select_with_rmb(value: bool)

bool get_select_with_rmb()

If true, enables selecting a tab with the right mouse button.

AlignmentMode tab_alignment = 0 🔗

void set_tab_alignment(value: AlignmentMode)

AlignmentMode get_tab_alignment()

The position at which tabs will be placed.

CloseButtonDisplayPolicy tab_close_display_policy = 0 🔗

void set_tab_close_display_policy(value: CloseButtonDisplayPolicy)

CloseButtonDisplayPolicy get_tab_close_display_policy()

When the close button will appear on the tabs.

void set_tab_count(value: int)

The number of tabs currently in the bar.

int tabs_rearrange_group = -1 🔗

void set_tabs_rearrange_group(value: int)

int get_tabs_rearrange_group()

TabBars with the same rearrange group ID will allow dragging the tabs between them. Enable drag with drag_to_rearrange_enabled.

Setting this to -1 will disable rearranging between TabBars.

void add_tab(title: String = "", icon: Texture2D = null) 🔗

void ensure_tab_visible(idx: int) 🔗

Moves the scroll view to make the tab visible.

bool get_offset_buttons_visible() const 🔗

Returns true if the offset buttons (the ones that appear when there's not enough space for all tabs) are visible.

int get_previous_tab() const 🔗

Returns the previously active tab index.

Texture2D get_tab_button_icon(tab_idx: int) const 🔗

Returns the icon for the right button of the tab at index tab_idx or null if the right button has no icon.

Texture2D get_tab_icon(tab_idx: int) const 🔗

Returns the icon for the tab at index tab_idx or null if the tab has no icon.

int get_tab_icon_max_width(tab_idx: int) const 🔗

Returns the maximum allowed width of the icon for the tab at index tab_idx.

int get_tab_idx_at_point(point: Vector2) const 🔗

Returns the index of the tab at local coordinates point. Returns -1 if the point is outside the control boundaries or if there's no tab at the queried position.

String get_tab_language(tab_idx: int) const 🔗

Returns tab title language code.

Variant get_tab_metadata(tab_idx: int) const 🔗

Returns the metadata value set to the tab at index tab_idx using set_tab_metadata(). If no metadata was previously set, returns null by default.

int get_tab_offset() const 🔗

Returns the number of hidden tabs offsetted to the left.

Rect2 get_tab_rect(tab_idx: int) const 🔗

Returns tab Rect2 with local position and size.

TextDirection get_tab_text_direction(tab_idx: int) const 🔗

Returns tab title text base writing direction.

String get_tab_title(tab_idx: int) const 🔗

Returns the title of the tab at index tab_idx.

String get_tab_tooltip(tab_idx: int) const 🔗

Returns the tooltip text of the tab at index tab_idx.

bool is_tab_disabled(tab_idx: int) const 🔗

Returns true if the tab at index tab_idx is disabled.

bool is_tab_hidden(tab_idx: int) const 🔗

Returns true if the tab at index tab_idx is hidden.

void move_tab(from: int, to: int) 🔗

Moves a tab from from to to.

void remove_tab(tab_idx: int) 🔗

Removes the tab at index tab_idx.

bool select_next_available() 🔗

Selects the first available tab with greater index than the currently selected. Returns true if tab selection changed.

bool select_previous_available() 🔗

Selects the first available tab with lower index than the currently selected. Returns true if tab selection changed.

void set_tab_button_icon(tab_idx: int, icon: Texture2D) 🔗

Sets an icon for the button of the tab at index tab_idx (located to the right, before the close button), making it visible and clickable (See tab_button_pressed). Giving it a null value will hide the button.

void set_tab_disabled(tab_idx: int, disabled: bool) 🔗

If disabled is true, disables the tab at index tab_idx, making it non-interactable.

void set_tab_hidden(tab_idx: int, hidden: bool) 🔗

If hidden is true, hides the tab at index tab_idx, making it disappear from the tab area.

void set_tab_icon(tab_idx: int, icon: Texture2D) 🔗

Sets an icon for the tab at index tab_idx.

void set_tab_icon_max_width(tab_idx: int, width: int) 🔗

Sets the maximum allowed width of the icon for the tab at index tab_idx. This limit is applied on top of the default size of the icon and on top of icon_max_width. The height is adjusted according to the icon's ratio.

void set_tab_language(tab_idx: int, language: String) 🔗

Sets language code of tab title used for line-breaking and text shaping algorithms, if left empty current locale is used instead.

void set_tab_metadata(tab_idx: int, metadata: Variant) 🔗

Sets the metadata value for the tab at index tab_idx, which can be retrieved later using get_tab_metadata().

void set_tab_text_direction(tab_idx: int, direction: TextDirection) 🔗

Sets tab title base writing direction.

void set_tab_title(tab_idx: int, title: String) 🔗

Sets a title for the tab at index tab_idx.

void set_tab_tooltip(tab_idx: int, tooltip: String) 🔗

Sets a tooltip for tab at index tab_idx.

Note: By default, if the tooltip is empty and the tab text is truncated (not all characters fit into the tab), the title will be displayed as a tooltip. To hide the tooltip, assign " " as the tooltip text.

Color drop_mark_color = Color(1, 1, 1, 1) 🔗

Modulation color for the drop_mark icon.

Color font_disabled_color = Color(0.875, 0.875, 0.875, 0.5) 🔗

Font color of disabled tabs.

Color font_hovered_color = Color(0.95, 0.95, 0.95, 1) 🔗

Font color of the currently hovered tab. Does not apply to the selected tab.

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The tint of text outline of the tab name.

Color font_selected_color = Color(0.95, 0.95, 0.95, 1) 🔗

Font color of the currently selected tab.

Color font_unselected_color = Color(0.7, 0.7, 0.7, 1) 🔗

Font color of the other, unselected tabs.

int h_separation = 4 🔗

The horizontal separation between the elements inside tabs.

int icon_max_width = 0 🔗

The maximum allowed width of the tab's icon. This limit is applied on top of the default size of the icon, but before the value set with set_tab_icon_max_width(). The height is adjusted according to the icon's ratio.

int outline_size = 0 🔗

The size of the tab text outline.

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

int tab_separation = 0 🔗

The space between tabs in the tab bar.

The font used to draw tab names.

Font size of the tab names.

The icon for the close button (see tab_close_display_policy).

Texture2D decrement 🔗

Icon for the left arrow button that appears when there are too many tabs to fit in the container width. When the button is disabled (i.e. the first tab is visible), it appears semi-transparent.

Texture2D decrement_highlight 🔗

Icon for the left arrow button that appears when there are too many tabs to fit in the container width. Used when the button is being hovered with the cursor.

Texture2D drop_mark 🔗

Icon shown to indicate where a dragged tab is gonna be dropped (see drag_to_rearrange_enabled).

Texture2D increment 🔗

Icon for the right arrow button that appears when there are too many tabs to fit in the container width. When the button is disabled (i.e. the last tab is visible) it appears semi-transparent.

Texture2D increment_highlight 🔗

Icon for the right arrow button that appears when there are too many tabs to fit in the container width. Used when the button is being hovered with the cursor.

StyleBox button_highlight 🔗

Background of the tab and close buttons when they're being hovered with the cursor.

StyleBox button_pressed 🔗

Background of the tab and close buttons when it's being pressed.

StyleBox tab_disabled 🔗

The style of disabled tabs.

StyleBox used when the TabBar is focused. The tab_focus StyleBox is displayed over the base StyleBox of the selected tab, so a partially transparent StyleBox should be used to ensure the base StyleBox remains visible. A StyleBox that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a StyleBoxEmpty resource. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

StyleBox tab_hovered 🔗

The style of the currently hovered tab. Does not apply to the selected tab.

Note: This style will be drawn with the same width as tab_unselected at minimum.

StyleBox tab_selected 🔗

The style of the currently selected tab.

StyleBox tab_unselected 🔗

The style of the other, unselected tabs.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (bash):
```bash
$TabBar.tab_close_pressed.connect($TabBar.remove_tab)
```

Example 2 (typescript):
```typescript
GetNode<TabBar>("TabBar").TabClosePressed += GetNode<TabBar>("TabBar").RemoveTab;
```

---

## TabContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_tabcontainer.html

**Contents:**
- TabContainer
- Description
- Tutorials
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions

Inherits: Container < Control < CanvasItem < Node < Object

A container that creates a tab for each child control, displaying only the active tab's control.

Arranges child controls into a tabbed view, creating a tab for each one. The active tab's corresponding control is made visible, while all other child controls are hidden. Ignores non-control children.

Note: The drawing of the clickable tabs is handled by this node; TabBar is not needed.

drag_to_rearrange_enabled

use_hidden_tabs_for_min_size

get_current_tab_control() const

get_previous_tab() const

get_tab_button_icon(tab_idx: int) const

get_tab_control(tab_idx: int) const

get_tab_count() const

get_tab_icon(tab_idx: int) const

get_tab_icon_max_width(tab_idx: int) const

get_tab_idx_at_point(point: Vector2) const

get_tab_idx_from_control(control: Control) const

get_tab_metadata(tab_idx: int) const

get_tab_title(tab_idx: int) const

get_tab_tooltip(tab_idx: int) const

is_tab_disabled(tab_idx: int) const

is_tab_hidden(tab_idx: int) const

select_next_available()

select_previous_available()

set_popup(popup: Node)

set_tab_button_icon(tab_idx: int, icon: Texture2D)

set_tab_disabled(tab_idx: int, disabled: bool)

set_tab_hidden(tab_idx: int, hidden: bool)

set_tab_icon(tab_idx: int, icon: Texture2D)

set_tab_icon_max_width(tab_idx: int, width: int)

set_tab_metadata(tab_idx: int, metadata: Variant)

set_tab_title(tab_idx: int, title: String)

set_tab_tooltip(tab_idx: int, tooltip: String)

Color(0.875, 0.875, 0.875, 0.5)

Color(0.95, 0.95, 0.95, 1)

Color(0.95, 0.95, 0.95, 1)

font_unselected_color

Color(0.7, 0.7, 0.7, 1)

active_tab_rearranged(idx_to: int) 🔗

Emitted when the active tab is rearranged via mouse drag. See drag_to_rearrange_enabled.

pre_popup_pressed() 🔗

Emitted when the TabContainer's Popup button is clicked. See set_popup() for details.

tab_button_pressed(tab: int) 🔗

Emitted when the user clicks on the button icon on this tab.

tab_changed(tab: int) 🔗

Emitted when switching to another tab.

tab_clicked(tab: int) 🔗

Emitted when a tab is clicked, even if it is the current tab.

tab_hovered(tab: int) 🔗

Emitted when a tab is hovered by the mouse.

tab_selected(tab: int) 🔗

Emitted when a tab is selected via click, directional input, or script, even if it is the current tab.

TabPosition POSITION_TOP = 0

Places the tab bar at the top.

TabPosition POSITION_BOTTOM = 1

Places the tab bar at the bottom. The tab bar's StyleBox will be flipped vertically.

TabPosition POSITION_MAX = 2

Represents the size of the TabPosition enum.

bool all_tabs_in_front = false 🔗

void set_all_tabs_in_front(value: bool)

bool is_all_tabs_in_front()

If true, all tabs are drawn in front of the panel. If false, inactive tabs are drawn behind the panel.

bool clip_tabs = true 🔗

void set_clip_tabs(value: bool)

If true, tabs overflowing this node's width will be hidden, displaying two navigation buttons instead. Otherwise, this node's minimum size is updated so that all tabs are visible.

int current_tab = -1 🔗

void set_current_tab(value: int)

int get_current_tab()

The current tab index. When set, this index's Control node's visible property is set to true and all others are set to false.

A value of -1 means that no tab is selected.

bool deselect_enabled = false 🔗

void set_deselect_enabled(value: bool)

bool get_deselect_enabled()

If true, all tabs can be deselected so that no tab is selected. Click on the current_tab to deselect it.

Only the tab header will be shown if no tabs are selected.

bool drag_to_rearrange_enabled = false 🔗

void set_drag_to_rearrange_enabled(value: bool)

bool get_drag_to_rearrange_enabled()

If true, tabs can be rearranged with mouse drag.

AlignmentMode tab_alignment = 0 🔗

void set_tab_alignment(value: AlignmentMode)

AlignmentMode get_tab_alignment()

The position at which tabs will be placed.

FocusMode tab_focus_mode = 2 🔗

void set_tab_focus_mode(value: FocusMode)

FocusMode get_tab_focus_mode()

The focus access mode for the internal TabBar node.

TabPosition tabs_position = 0 🔗

void set_tabs_position(value: TabPosition)

TabPosition get_tabs_position()

The position of the tab bar.

int tabs_rearrange_group = -1 🔗

void set_tabs_rearrange_group(value: int)

int get_tabs_rearrange_group()

TabContainers with the same rearrange group ID will allow dragging the tabs between them. Enable drag with drag_to_rearrange_enabled.

Setting this to -1 will disable rearranging between TabContainers.

bool tabs_visible = true 🔗

void set_tabs_visible(value: bool)

bool are_tabs_visible()

If true, tabs are visible. If false, tabs' content and titles are hidden.

bool use_hidden_tabs_for_min_size = false 🔗

void set_use_hidden_tabs_for_min_size(value: bool)

bool get_use_hidden_tabs_for_min_size()

If true, child Control nodes that are hidden have their minimum size take into account in the total, instead of only the currently visible one.

Control get_current_tab_control() const 🔗

Returns the child Control node located at the active tab index.

Popup get_popup() const 🔗

Returns the Popup node instance if one has been set already with set_popup().

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their Window.visible property.

int get_previous_tab() const 🔗

Returns the previously active tab index.

TabBar get_tab_bar() const 🔗

Returns the TabBar contained in this container.

Warning: This is a required internal node, removing and freeing it or editing its tabs may cause a crash. If you wish to edit the tabs, use the methods provided in TabContainer.

Texture2D get_tab_button_icon(tab_idx: int) const 🔗

Returns the button icon from the tab at index tab_idx.

Control get_tab_control(tab_idx: int) const 🔗

Returns the Control node from the tab at index tab_idx.

int get_tab_count() const 🔗

Returns the number of tabs.

Texture2D get_tab_icon(tab_idx: int) const 🔗

Returns the Texture2D for the tab at index tab_idx or null if the tab has no Texture2D.

int get_tab_icon_max_width(tab_idx: int) const 🔗

Returns the maximum allowed width of the icon for the tab at index tab_idx.

int get_tab_idx_at_point(point: Vector2) const 🔗

Returns the index of the tab at local coordinates point. Returns -1 if the point is outside the control boundaries or if there's no tab at the queried position.

int get_tab_idx_from_control(control: Control) const 🔗

Returns the index of the tab tied to the given control. The control must be a child of the TabContainer.

Variant get_tab_metadata(tab_idx: int) const 🔗

Returns the metadata value set to the tab at index tab_idx using set_tab_metadata(). If no metadata was previously set, returns null by default.

String get_tab_title(tab_idx: int) const 🔗

Returns the title of the tab at index tab_idx. Tab titles default to the name of the indexed child node, but this can be overridden with set_tab_title().

String get_tab_tooltip(tab_idx: int) const 🔗

Returns the tooltip text of the tab at index tab_idx.

bool is_tab_disabled(tab_idx: int) const 🔗

Returns true if the tab at index tab_idx is disabled.

bool is_tab_hidden(tab_idx: int) const 🔗

Returns true if the tab at index tab_idx is hidden.

bool select_next_available() 🔗

Selects the first available tab with greater index than the currently selected. Returns true if tab selection changed.

bool select_previous_available() 🔗

Selects the first available tab with lower index than the currently selected. Returns true if tab selection changed.

void set_popup(popup: Node) 🔗

If set on a Popup node instance, a popup menu icon appears in the top-right corner of the TabContainer (setting it to null will make it go away). Clicking it will expand the Popup node.

void set_tab_button_icon(tab_idx: int, icon: Texture2D) 🔗

Sets the button icon from the tab at index tab_idx.

void set_tab_disabled(tab_idx: int, disabled: bool) 🔗

If disabled is true, disables the tab at index tab_idx, making it non-interactable.

void set_tab_hidden(tab_idx: int, hidden: bool) 🔗

If hidden is true, hides the tab at index tab_idx, making it disappear from the tab area.

void set_tab_icon(tab_idx: int, icon: Texture2D) 🔗

Sets an icon for the tab at index tab_idx.

void set_tab_icon_max_width(tab_idx: int, width: int) 🔗

Sets the maximum allowed width of the icon for the tab at index tab_idx. This limit is applied on top of the default size of the icon and on top of icon_max_width. The height is adjusted according to the icon's ratio.

void set_tab_metadata(tab_idx: int, metadata: Variant) 🔗

Sets the metadata value for the tab at index tab_idx, which can be retrieved later using get_tab_metadata().

void set_tab_title(tab_idx: int, title: String) 🔗

Sets a custom title for the tab at index tab_idx (tab titles default to the name of the indexed child node). Set it back to the child's name to make the tab default to it again.

void set_tab_tooltip(tab_idx: int, tooltip: String) 🔗

Sets a custom tooltip text for tab at index tab_idx.

Note: By default, if the tooltip is empty and the tab text is truncated (not all characters fit into the tab), the title will be displayed as a tooltip. To hide the tooltip, assign " " as the tooltip text.

Color drop_mark_color = Color(1, 1, 1, 1) 🔗

Modulation color for the drop_mark icon.

Color font_disabled_color = Color(0.875, 0.875, 0.875, 0.5) 🔗

Font color of disabled tabs.

Color font_hovered_color = Color(0.95, 0.95, 0.95, 1) 🔗

Font color of the currently hovered tab.

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The tint of text outline of the tab name.

Color font_selected_color = Color(0.95, 0.95, 0.95, 1) 🔗

Font color of the currently selected tab.

Color font_unselected_color = Color(0.7, 0.7, 0.7, 1) 🔗

Font color of the other, unselected tabs.

int icon_max_width = 0 🔗

The maximum allowed width of the tab's icon. This limit is applied on top of the default size of the icon, but before the value set with TabBar.set_tab_icon_max_width(). The height is adjusted according to the icon's ratio.

int icon_separation = 4 🔗

Space between tab's name and its icon.

int outline_size = 0 🔗

The size of the tab text outline.

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

int side_margin = 8 🔗

The space at the left or right edges of the tab bar, accordingly with the current tab_alignment.

The margin is ignored with TabBar.ALIGNMENT_RIGHT if the tabs are clipped (see clip_tabs) or a popup has been set (see set_popup()). The margin is always ignored with TabBar.ALIGNMENT_CENTER.

int tab_separation = 0 🔗

The space between tabs in the tab bar.

The font used to draw tab names.

Font size of the tab names.

Texture2D decrement 🔗

Icon for the left arrow button that appears when there are too many tabs to fit in the container width. When the button is disabled (i.e. the first tab is visible), it appears semi-transparent.

Texture2D decrement_highlight 🔗

Icon for the left arrow button that appears when there are too many tabs to fit in the container width. Used when the button is being hovered with the cursor.

Texture2D drop_mark 🔗

Icon shown to indicate where a dragged tab is gonna be dropped (see drag_to_rearrange_enabled).

Texture2D increment 🔗

Icon for the right arrow button that appears when there are too many tabs to fit in the container width. When the button is disabled (i.e. the last tab is visible) it appears semi-transparent.

Texture2D increment_highlight 🔗

Icon for the right arrow button that appears when there are too many tabs to fit in the container width. Used when the button is being hovered with the cursor.

The icon for the menu button (see set_popup()).

Texture2D menu_highlight 🔗

The icon for the menu button (see set_popup()) when it's being hovered with the cursor.

The style for the background fill.

StyleBox tab_disabled 🔗

The style of disabled tabs.

StyleBox used when the TabBar is focused. The tab_focus StyleBox is displayed over the base StyleBox of the selected tab, so a partially transparent StyleBox should be used to ensure the base StyleBox remains visible. A StyleBox that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a StyleBoxEmpty resource. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

StyleBox tab_hovered 🔗

The style of the currently hovered tab.

Note: This style will be drawn with the same width as tab_unselected at minimum.

StyleBox tab_selected 🔗

The style of the currently selected tab.

StyleBox tab_unselected 🔗

The style of the other, unselected tabs.

StyleBox tabbar_background 🔗

The style for the background fill of the TabBar area.

Please read the User-contributed notes policy before submitting a comment.

---

## TextServerDummy

**URL:** https://docs.godotengine.org/en/stable/classes/class_textserverdummy.html

**Contents:**
- TextServerDummy
- Description
- User-contributed notes

Inherits: TextServerExtension < TextServer < RefCounted < Object

A dummy text server that can't render text or manage fonts.

A dummy TextServer interface that doesn't do anything. Useful for freeing up memory when rendering text is not needed, as text servers are resource-intensive. It can also be used for performance comparisons in complex GUIs to check the impact of text rendering.

A dummy text server is always available at the start of a project. Here's how to access it:

The command line argument --text-driver Dummy (case-sensitive) can be used to force the "Dummy" TextServer on any project.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var dummy_text_server = TextServerManager.find_interface("Dummy")
if dummy_text_server != null:
    TextServerManager.set_primary_interface(dummy_text_server)
    # If the other text servers are unneeded, they can be removed:
    for i in TextServerManager.get_interface_count():
        var text_server = TextServerManager.get_interface(i)
        if text_server != dummy_text_server:
            TextServerManager.remove_interface(text_server)
```

---

## TextServerManager

**URL:** https://docs.godotengine.org/en/stable/classes/class_textservermanager.html

**Contents:**
- TextServerManager
- Description
- Methods
- Signals
- Method Descriptions
- User-contributed notes

A singleton for managing TextServer implementations.

TextServerManager is the API backend for loading, enumerating, and switching TextServers.

Note: Switching text server at runtime is possible, but will invalidate all fonts and text buffers. Make sure to unload all controls, fonts, and themes before doing so.

add_interface(interface: TextServer)

find_interface(name: String) const

get_interface(idx: int) const

get_interface_count() const

get_interfaces() const

get_primary_interface() const

remove_interface(interface: TextServer)

set_primary_interface(index: TextServer)

interface_added(interface_name: StringName) 🔗

Emitted when a new interface has been added.

interface_removed(interface_name: StringName) 🔗

Emitted when an interface is removed.

void add_interface(interface: TextServer) 🔗

Registers a TextServer interface.

TextServer find_interface(name: String) const 🔗

Finds an interface by its name.

TextServer get_interface(idx: int) const 🔗

Returns the interface registered at a given index.

int get_interface_count() const 🔗

Returns the number of interfaces currently registered.

Array[Dictionary] get_interfaces() const 🔗

Returns a list of available interfaces, with the index and name of each interface.

TextServer get_primary_interface() const 🔗

Returns the primary TextServer interface currently in use.

void remove_interface(interface: TextServer) 🔗

Removes an interface. All fonts and shaped text caches should be freed before removing an interface.

void set_primary_interface(index: TextServer) 🔗

Sets the primary TextServer interface.

Please read the User-contributed notes policy before submitting a comment.

---

## TextureButton

**URL:** https://docs.godotengine.org/en/stable/classes/class_texturebutton.html

**Contents:**
- TextureButton
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: BaseButton < Control < CanvasItem < Node < Object

Texture-based button. Supports Pressed, Hover, Disabled and Focused states.

TextureButton has the same functionality as Button, except it uses sprites instead of Godot's Theme resource. It is faster to create, but it doesn't support localization like more complex Controls.

See also BaseButton which contains common properties and methods associated with this node.

Note: Setting a texture for the "normal" state (texture_normal) is recommended. If texture_normal is not set, the TextureButton will still receive input events and be clickable, but the user will not be able to see it unless they activate another one of its states with a texture assigned (e.g., hover over it to show texture_hover).

StretchMode STRETCH_SCALE = 0

Scale to fit the node's bounding rectangle.

StretchMode STRETCH_TILE = 1

Tile inside the node's bounding rectangle.

StretchMode STRETCH_KEEP = 2

The texture keeps its original size and stays in the bounding rectangle's top-left corner.

StretchMode STRETCH_KEEP_CENTERED = 3

The texture keeps its original size and stays centered in the node's bounding rectangle.

StretchMode STRETCH_KEEP_ASPECT = 4

Scale the texture to fit the node's bounding rectangle, but maintain the texture's aspect ratio.

StretchMode STRETCH_KEEP_ASPECT_CENTERED = 5

Scale the texture to fit the node's bounding rectangle, center it, and maintain its aspect ratio.

StretchMode STRETCH_KEEP_ASPECT_COVERED = 6

Scale the texture so that the shorter side fits the bounding rectangle. The other side clips to the node's limits.

bool flip_h = false 🔗

void set_flip_h(value: bool)

If true, texture is flipped horizontally.

bool flip_v = false 🔗

void set_flip_v(value: bool)

If true, texture is flipped vertically.

bool ignore_texture_size = false 🔗

void set_ignore_texture_size(value: bool)

bool get_ignore_texture_size()

If true, the size of the texture won't be considered for minimum size calculation, so the TextureButton can be shrunk down past the texture size.

StretchMode stretch_mode = 2 🔗

void set_stretch_mode(value: StretchMode)

StretchMode get_stretch_mode()

Controls the texture's behavior when you resize the node's bounding rectangle. See the StretchMode constants for available options.

BitMap texture_click_mask 🔗

void set_click_mask(value: BitMap)

BitMap get_click_mask()

Pure black and white BitMap image to use for click detection. On the mask, white pixels represent the button's clickable area. Use it to create buttons with curved shapes.

Texture2D texture_disabled 🔗

void set_texture_disabled(value: Texture2D)

Texture2D get_texture_disabled()

Texture to display when the node is disabled. See BaseButton.disabled. If not assigned, the TextureButton displays texture_normal instead.

Texture2D texture_focused 🔗

void set_texture_focused(value: Texture2D)

Texture2D get_texture_focused()

Texture to overlay on the base texture when the node has mouse or keyboard focus. Because texture_focused is displayed on top of the base texture, a partially transparent texture should be used to ensure the base texture remains visible. A texture that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a fully transparent texture of any size. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

Texture2D texture_hover 🔗

void set_texture_hover(value: Texture2D)

Texture2D get_texture_hover()

Texture to display when the mouse hovers over the node. If not assigned, the TextureButton displays texture_normal instead when hovered over.

Texture2D texture_normal 🔗

void set_texture_normal(value: Texture2D)

Texture2D get_texture_normal()

Texture to display by default, when the node is not in the disabled, hover or pressed state. This texture is still displayed in the focused state, with texture_focused drawn on top.

Texture2D texture_pressed 🔗

void set_texture_pressed(value: Texture2D)

Texture2D get_texture_pressed()

Texture to display on mouse down over the node, if the node has keyboard focus and the player presses the Enter key or if the player presses the BaseButton.shortcut key. If not assigned, the TextureButton displays texture_hover instead when pressed.

Please read the User-contributed notes policy before submitting a comment.

---

## TextureProgressBar

**URL:** https://docs.godotengine.org/en/stable/classes/class_textureprogressbar.html

**Contents:**
- TextureProgressBar
- Description
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Range < Control < CanvasItem < Node < Object

Texture-based progress bar. Useful for loading screens and life or stamina bars.

TextureProgressBar works like ProgressBar, but uses up to 3 textures instead of Godot's Theme resource. It can be used to create horizontal, vertical and radial progress bars.

1 (overrides Control)

1 (overrides Control)

1.0 (overrides Range)

stretch_margin_bottom

texture_progress_offset

get_stretch_margin(margin: Side) const

set_stretch_margin(margin: Side, value: int)

FillMode FILL_LEFT_TO_RIGHT = 0

The texture_progress fills from left to right.

FillMode FILL_RIGHT_TO_LEFT = 1

The texture_progress fills from right to left.

FillMode FILL_TOP_TO_BOTTOM = 2

The texture_progress fills from top to bottom.

FillMode FILL_BOTTOM_TO_TOP = 3

The texture_progress fills from bottom to top.

FillMode FILL_CLOCKWISE = 4

Turns the node into a radial bar. The texture_progress fills clockwise. See radial_center_offset, radial_initial_angle and radial_fill_degrees to control the way the bar fills up.

FillMode FILL_COUNTER_CLOCKWISE = 5

Turns the node into a radial bar. The texture_progress fills counterclockwise. See radial_center_offset, radial_initial_angle and radial_fill_degrees to control the way the bar fills up.

FillMode FILL_BILINEAR_LEFT_AND_RIGHT = 6

The texture_progress fills from the center, expanding both towards the left and the right.

FillMode FILL_BILINEAR_TOP_AND_BOTTOM = 7

The texture_progress fills from the center, expanding both towards the top and the bottom.

FillMode FILL_CLOCKWISE_AND_COUNTER_CLOCKWISE = 8

Turns the node into a radial bar. The texture_progress fills radially from the center, expanding both clockwise and counterclockwise. See radial_center_offset, radial_initial_angle and radial_fill_degrees to control the way the bar fills up.

void set_fill_mode(value: int)

The fill direction. See FillMode for possible values.

bool nine_patch_stretch = false 🔗

void set_nine_patch_stretch(value: bool)

bool get_nine_patch_stretch()

If true, Godot treats the bar's textures like in NinePatchRect. Use the stretch_margin_* properties like stretch_margin_bottom to set up the nine patch's 3×3 grid. When using a radial fill_mode, this setting will only enable stretching for texture_progress, while texture_under and texture_over will be treated like in NinePatchRect.

Vector2 radial_center_offset = Vector2(0, 0) 🔗

void set_radial_center_offset(value: Vector2)

Vector2 get_radial_center_offset()

Offsets texture_progress if fill_mode is FILL_CLOCKWISE, FILL_COUNTER_CLOCKWISE, or FILL_CLOCKWISE_AND_COUNTER_CLOCKWISE.

Note: The effective radial center always stays within the texture_progress bounds. If you need to move it outside the texture's bounds, modify the texture_progress to contain additional empty space where needed.

float radial_fill_degrees = 360.0 🔗

void set_fill_degrees(value: float)

float get_fill_degrees()

Upper limit for the fill of texture_progress if fill_mode is FILL_CLOCKWISE, FILL_COUNTER_CLOCKWISE, or FILL_CLOCKWISE_AND_COUNTER_CLOCKWISE. When the node's value is equal to its max_value, the texture fills up to this angle.

See Range.value, Range.max_value.

float radial_initial_angle = 0.0 🔗

void set_radial_initial_angle(value: float)

float get_radial_initial_angle()

Starting angle for the fill of texture_progress if fill_mode is FILL_CLOCKWISE, FILL_COUNTER_CLOCKWISE, or FILL_CLOCKWISE_AND_COUNTER_CLOCKWISE. When the node's value is equal to its min_value, the texture doesn't show up at all. When the value increases, the texture fills and tends towards radial_fill_degrees.

Note: radial_initial_angle is wrapped between 0 and 360 degrees (inclusive).

int stretch_margin_bottom = 0 🔗

void set_stretch_margin(margin: Side, value: int)

int get_stretch_margin(margin: Side) const

The height of the 9-patch's bottom row. A margin of 16 means the 9-slice's bottom corners and side will have a height of 16 pixels. You can set all 4 margin values individually to create panels with non-uniform borders. Only effective if nine_patch_stretch is true.

int stretch_margin_left = 0 🔗

void set_stretch_margin(margin: Side, value: int)

int get_stretch_margin(margin: Side) const

The width of the 9-patch's left column. Only effective if nine_patch_stretch is true.

int stretch_margin_right = 0 🔗

void set_stretch_margin(margin: Side, value: int)

int get_stretch_margin(margin: Side) const

The width of the 9-patch's right column. Only effective if nine_patch_stretch is true.

int stretch_margin_top = 0 🔗

void set_stretch_margin(margin: Side, value: int)

int get_stretch_margin(margin: Side) const

The height of the 9-patch's top row. Only effective if nine_patch_stretch is true.

Texture2D texture_over 🔗

void set_over_texture(value: Texture2D)

Texture2D get_over_texture()

Texture2D that draws over the progress bar. Use it to add highlights or an upper-frame that hides part of texture_progress.

Texture2D texture_progress 🔗

void set_progress_texture(value: Texture2D)

Texture2D get_progress_texture()

Texture2D that clips based on the node's value and fill_mode. As value increased, the texture fills up. It shows entirely when value reaches max_value. It doesn't show at all if value is equal to min_value.

The value property comes from Range. See Range.value, Range.min_value, Range.max_value.

Vector2 texture_progress_offset = Vector2(0, 0) 🔗

void set_texture_progress_offset(value: Vector2)

Vector2 get_texture_progress_offset()

The offset of texture_progress. Useful for texture_over and texture_under with fancy borders, to avoid transparent margins in your progress texture.

Texture2D texture_under 🔗

void set_under_texture(value: Texture2D)

Texture2D get_under_texture()

Texture2D that draws under the progress bar. The bar's background.

Color tint_over = Color(1, 1, 1, 1) 🔗

void set_tint_over(value: Color)

Color get_tint_over()

Multiplies the color of the bar's texture_over texture. The effect is similar to CanvasItem.modulate, except it only affects this specific texture instead of the entire node.

Color tint_progress = Color(1, 1, 1, 1) 🔗

void set_tint_progress(value: Color)

Color get_tint_progress()

Multiplies the color of the bar's texture_progress texture.

Color tint_under = Color(1, 1, 1, 1) 🔗

void set_tint_under(value: Color)

Color get_tint_under()

Multiplies the color of the bar's texture_under texture.

int get_stretch_margin(margin: Side) const 🔗

Returns the stretch margin with the specified index. See stretch_margin_bottom and related properties.

void set_stretch_margin(margin: Side, value: int) 🔗

Sets the stretch margin with the specified index. See stretch_margin_bottom and related properties.

Please read the User-contributed notes policy before submitting a comment.

---

## TextureRect

**URL:** https://docs.godotengine.org/en/stable/classes/class_texturerect.html

**Contents:**
- TextureRect
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: Control < CanvasItem < Node < Object

A control that displays a texture.

A control that displays a texture, for example an icon inside a GUI. The texture's placement can be controlled with the stretch_mode property. It can scale, tile, or stay centered inside its bounding rectangle.

1 (overrides Control)

ExpandMode EXPAND_KEEP_SIZE = 0

The minimum size will be equal to texture size, i.e. TextureRect can't be smaller than the texture.

ExpandMode EXPAND_IGNORE_SIZE = 1

The size of the texture won't be considered for minimum size calculation, so the TextureRect can be shrunk down past the texture size.

ExpandMode EXPAND_FIT_WIDTH = 2

The height of the texture will be ignored. Minimum width will be equal to the current height. Useful for horizontal layouts, e.g. inside HBoxContainer.

ExpandMode EXPAND_FIT_WIDTH_PROPORTIONAL = 3

Same as EXPAND_FIT_WIDTH, but keeps texture's aspect ratio.

ExpandMode EXPAND_FIT_HEIGHT = 4

The width of the texture will be ignored. Minimum height will be equal to the current width. Useful for vertical layouts, e.g. inside VBoxContainer.

ExpandMode EXPAND_FIT_HEIGHT_PROPORTIONAL = 5

Same as EXPAND_FIT_HEIGHT, but keeps texture's aspect ratio.

StretchMode STRETCH_SCALE = 0

Scale to fit the node's bounding rectangle.

StretchMode STRETCH_TILE = 1

Tile inside the node's bounding rectangle.

StretchMode STRETCH_KEEP = 2

The texture keeps its original size and stays in the bounding rectangle's top-left corner.

StretchMode STRETCH_KEEP_CENTERED = 3

The texture keeps its original size and stays centered in the node's bounding rectangle.

StretchMode STRETCH_KEEP_ASPECT = 4

Scale the texture to fit the node's bounding rectangle, but maintain the texture's aspect ratio.

StretchMode STRETCH_KEEP_ASPECT_CENTERED = 5

Scale the texture to fit the node's bounding rectangle, center it and maintain its aspect ratio.

StretchMode STRETCH_KEEP_ASPECT_COVERED = 6

Scale the texture so that the shorter side fits the bounding rectangle. The other side clips to the node's limits.

ExpandMode expand_mode = 0 🔗

void set_expand_mode(value: ExpandMode)

ExpandMode get_expand_mode()

Experimental: Using EXPAND_FIT_WIDTH, EXPAND_FIT_WIDTH_PROPORTIONAL, EXPAND_FIT_HEIGHT, or EXPAND_FIT_HEIGHT_PROPORTIONAL may result in unstable behavior in some Container controls. This behavior may be re-evaluated and changed in the future.

Defines how minimum size is determined based on the texture's size.

bool flip_h = false 🔗

void set_flip_h(value: bool)

If true, texture is flipped horizontally.

bool flip_v = false 🔗

void set_flip_v(value: bool)

If true, texture is flipped vertically.

StretchMode stretch_mode = 0 🔗

void set_stretch_mode(value: StretchMode)

StretchMode get_stretch_mode()

Controls the texture's behavior when resizing the node's bounding rectangle.

void set_texture(value: Texture2D)

Texture2D get_texture()

The node's Texture2D resource.

Please read the User-contributed notes policy before submitting a comment.

---

## ThemeDB

**URL:** https://docs.godotengine.org/en/stable/classes/class_themedb.html

**Contents:**
- ThemeDB
- Description
- Properties
- Methods
- Signals
- Property Descriptions
- Method Descriptions
- User-contributed notes

A singleton that provides access to static information about Theme resources used by the engine and by your project.

This singleton provides access to static information about Theme resources used by the engine and by your projects. You can fetch the default engine theme, as well as your project configured theme.

ThemeDB also contains fallback values for theme properties.

Emitted when one of the fallback values had been changed. Use it to refresh the look of controls that may rely on the fallback theme items.

float fallback_base_scale = 1.0 🔗

void set_fallback_base_scale(value: float)

float get_fallback_base_scale()

The fallback base scale factor of every Control node and Theme resource. Used when no other value is available to the control.

See also Theme.default_base_scale.

void set_fallback_font(value: Font)

Font get_fallback_font()

The fallback font of every Control node and Theme resource. Used when no other value is available to the control.

See also Theme.default_font.

int fallback_font_size = 16 🔗

void set_fallback_font_size(value: int)

int get_fallback_font_size()

The fallback font size of every Control node and Theme resource. Used when no other value is available to the control.

See also Theme.default_font_size.

Texture2D fallback_icon 🔗

void set_fallback_icon(value: Texture2D)

Texture2D get_fallback_icon()

The fallback icon of every Control node and Theme resource. Used when no other value is available to the control.

StyleBox fallback_stylebox 🔗

void set_fallback_stylebox(value: StyleBox)

StyleBox get_fallback_stylebox()

The fallback stylebox of every Control node and Theme resource. Used when no other value is available to the control.

Theme get_default_theme() 🔗

Returns a reference to the default engine Theme. This theme resource is responsible for the out-of-the-box look of Control nodes and cannot be overridden.

Theme get_project_theme() 🔗

Returns a reference to the custom project Theme. This theme resources allows to override the default engine theme for every control node in the project.

To set the project theme, see ProjectSettings.gui/theme/custom.

Please read the User-contributed notes policy before submitting a comment.

---

## Theme type variations

**URL:** https://docs.godotengine.org/en/stable/tutorials/ui/gui_theme_type_variations.html

**Contents:**
- Theme type variations
- Creating a type variation
- Using a type variation
- User-contributed notes

When designing a user interface there may be times when a Control node needs to have a different look than what is normally defined by a Theme. Every control node has theme property overrides, which allow you to redefine the styling for each individual UI element.

This approach quickly becomes hard to manage, if you need to share the same custom look between several controls. Imagine that you use gray, blue, and red variants of Button throughout your project. Setting it up every time you add a new button element to your interface is a tedious task.

To help with the organization and to better utilize the power of themes you can use theme type variations. These work like normal theme types, but instead of being self-sufficient and standalone they extend another, base type.

Following the previous example, your theme can have some styles, colors, and fonts defined for the Button type, customizing the looks of every button element in your UI. To then have a gray, red, or blue button you would create a new type, e.g. GrayButton, and mark it as a variation of the base Button type.

Type variations can replace some aspects of the base type, but keep others. They can also define properties that the base style hasn't defined. For example, your GrayButton can override the normal style from the base Button and add font_color that Button has never defined. The control will use a combination of both types giving priority to the type variation.

The way controls resolve what theme items they use from each type and each theme is better described in the Customizing a project section of the "Introduction to GUI skinning" article.

To create a type variation open the theme editor, then click the plus icon next to the Type dropdown on the right side of the editor. Type in what you want to name your theme type variation in the text box, then click Add Type.

Below the Type dropdown are the property tabs. Switch to the tab with a wrench and screwdriver icon.

Click on the plus icon next to the Base Type field. You can select the base type there, which would typically be the name of a control node class (e.g., Button, Label, etc). Type variations can also chain and extend other type variations. This works in the same way control nodes inherit styling of their base class. For example, CheckButton inherits styles from Button because corresponding node types extend each other.

After you select the base type, you should now be able to see its properties on the other tabs in the theme editor. You can edit them as usual.

Now that a type variation has been created you can apply it to your nodes. In the inspector dock, under the Theme property of a control node, you can find the Theme Type Variation property. It is empty by default, which means that only the base type has an effect on this node.

You can either select a type variation from a dropdown list, or input its name manually. Variations appear on the list only if the type variation belongs to the project-wide theme, which you can configure in the project settings. For any other case you have to input the name of the variation manually. Click on the pencil icon to the right. Then type in the name of the type variation and click the check mark icon or press enter. If a type variation with that name exists it will now be used by the node.

Please read the User-contributed notes policy before submitting a comment.

---

## The XR action map

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/xr_action_map.html

**Contents:**
- The XR action map
- The default action map
- Action sets
- Actions
- Profiles
- Our first controller binding
- The simple controller
- Binding Modifiers
  - Binding modifiers on an interaction profile
    - Dpad Binding modifier

Godot has an action map feature as part of the XR system. At this point in time this system is part of the OpenXR module. There are plans to encompass WebXR into this in the near future hence we call it the XR action map system in this document. It implements the built-in action map system of OpenXR mostly exactly as it is offered.

The XR action map system exposes input, positional data and output for XR controllers to your game/application. It does this by exposing named actions that can be tailored to your game/application and binding these to the actual inputs and outputs on your XR devices.

As the XR action map is currently part of the OpenXR module, OpenXR needs to be enabled in your project settings to expose it:

You will then find the XR Action Map interface in the bottom of the screen:

Godot's built-in input system has many things in common with the XR action map system. In fact our original idea was to add functionality to the existing input system and expose the data to the OpenXR action map system. We may revisit that idea at some point but as it turns out there were just too many problems to overcome. To name a few:

Godot's input system mainly centers around button inputs, XR adds triggers, axis, poses and haptics (output) into the mix. This would greatly complicate the input system with features that won't work for normal controllers or contrast with the current approach. It was felt this would lead to confusion for the majority of Godot users.

Godot's input system works with raw input data that is parsed and triggers emitting actions. This input data is made available to the end user. OpenXR completely hides raw data and does all the parsing for us, we only get access to already parsed action data. This inconsistency is likely to lead to bugs when an unsuspecting user tries to use an XR device as a normal input device.

Godot's input system allows changes to what inputs are bound to actions in runtime, OpenXR does not.

Godot's input system is based on device ids which are meaningless in OpenXR.

This does mean that a game/application that mixes traditional inputs with XR controllers will have a separation. For most applications either one or the other is used and this is not seen as a problem. In the end, it's a limitation of the system.

Godot will automatically create a default action map if no action map file is found.

This default map was designed to help developers port their XR games/applications from Godot 3 to Godot 4. As a result this map essentially binds all known inputs on all controllers supported by default, to actions one on one. This is not a good example of setting up an action map. It does allow a new developer to have a starting point when they want to become familiar with Godot XR. It prevents having to design a proper action map for their game/application first.

For this walkthrough we're going to start with a blank action map. You can delete the "Godot action set" entry at the top by pressing the trash can icon. This will clear out all actions. You might also want to remove the controllers that you do not wish to setup, more on this later.

Before we dive in, you will see the term XR runtime used throughout this document. With XR runtime we mean the software that is controlling and interacting with the AR or VR headset. The XR runtime then exposes this to us through an API such as OpenXR. So:

for Steam this is SteamVR,

for Meta on desktop this is the Oculus Client (including when using Quest link),

for Meta on Quest this is the Quest's native OpenXR client,

on Linux this could be Monado, etc.

The action map allows us to organize our actions in sets. Each set can be enabled or disabled on its own.

The concept here is that you could have different sets that provide bindings in different scenarios. You could have:

a Character control set for when you're walking around,

a Vehicle control set for when you're operating a vehicle,

a Menu set for when a menu is open.

Only the action set applicable to the current state of your game/application can then be enabled.

This is especially important if you wish to bind the same input on a controller to a different action. For instance:

in your Character control set you may have an action Jump,

in your Vehicle control set you may have an action Accelerate,

in your Menu set you may have an action Select.

All are bound to the trigger on your controller.

OpenXR will only bind an input or output to a single action. If the same input or output is bound to multiple actions the one in the active action set with the highest priority will be the one updated/used. So in our above example it will thus be important that only one action set is active.

For your first XR game/application we highly recommend starting with just a single action set and to not over-engineer things.

For our walkthrough in this document we will thus create a single action set called my_first_action_set. We do this by pressing the Add action set button:

The columns in our table are as follows:

This is the internal name of the action set. OpenXR doesn't specify specific restrictions on this name other then size, however some XR runtimes will not like spaces or special characters.

This is a human-readable name for the action set. Some XR runtimes will display this name to the end user, for example in configuration dialogs.

This is the priority of the action set. If multiple active action sets have actions bound to the same controller's inputs or outputs, the action set with the highest priority value will determine the action that is updated.

In the XR action map, actions are the entities that your game/application will interact with. For instance, we can define an action Shoot and the input bound to that action will trigger the button_pressed signal on the relevant XRController3D node in your scene with Shoot as the name parameter of the signal.

You can also poll the current state of an action. XRController3D for instance has an is_button_pressed method.

Actions can be used for both input and output and each action has a type that defines its behavior.

The Bool type is used for discrete input like buttons.

The Float type is used for analogue input like triggers.

These two are special as they are the only ones that are interchangeable. OpenXR will handle conversions between Bool and Float inputs and actions. You can get the value of a Float type action by calling the method get_float on your XRController3D node. It emits the input_float_changed signal when changed.

Where analogue inputs are queried as buttons a threshold is applied. This threshold is currently managed exclusively by the XR runtime. There are plans to extend Godot to provide some level of control over these thresholds in the future.

The Vector2 type defines the input as an axis input. Touchpads, thumbsticks and similar inputs are exposed as vectors. You can get the value of a Vector2 type action by calling the method get_vector2 on your XRController3D node. It emits the input_vector2_changed signal when changed.

The Pose type defines a spatially tracked input. Multiple "pose" inputs are available in OpenXR: aim, grip and palm. Your XRController3D node is automatically positioned based on the pose action assigned to pose property of this node. More about poses later.

The OpenXR implementation in Godot also exposes a special pose called Skeleton. This is part of the hand tracking implementation. This pose is exposed through the skeleton action that is supported outside of the action map system. It is thus always present if hand tracking is supported. You don't need to bind actions to this pose to use it.

Finally, the only output type is Haptic and it allows us to set the intensity of haptic feedback, such as controller vibration. Controllers can have multiple haptic outputs and support for haptic vests is coming to OpenXR.

So lets add an action for our aim pose, we do this by clicking on the + button for our action set:

The columns in our table are as follows:

This is the internal name of the action. OpenXR doesn't specify specific restrictions on this name other then size, however some XR runtimes will not like spaces or special characters.

This is a human-readable name for the action. Some XR runtimes will display this name to the end user, for example in configuration dialogs.

The type of this action.

OpenXR defines a number of bindable input poses that are commonly available for controllers. There are no rules for which poses are supported for different controllers. The poses OpenXR currently defines are:

The aim pose on most controllers is positioned slightly in front of the controller and aims forward. This is a great pose to use for laser pointers or to align the muzzle of a weapon with.

The grip pose on most controllers is positioned where the grip button is placed on the controller. The orientation of this pose differs between controllers and can differ for the same controller on different XR runtimes.

The palm pose on most controllers is positioned in the center of the palm of the hand holding the controller. This is a new pose that is not available on all XR runtimes.

If hand tracking is used, there are currently big differences in implementations between the different XR runtimes. As a result the action map is currently not suitable for hand tracking. Work is being done on this so stay tuned.

Let's complete our list of actions for a very simple shooting game/application:

The actions we have added are:

movement, which allows the user to move around outside of normal room scale tracking.

grab, which detects that the user wants to hold something.

shoot, which detects that the user wants to fire the weapon they are holding.

haptic, which allows us to output haptic feedback.

Now note that we don't distinguish between the left and right hand. This is something that is determined at the next stage. We've implemented the action system in such a way that you can bind the same action to both hands. The appropriate XRController3D node will emit the signal.

For both grab and shoot we've used the Bool type. As mentioned before, OpenXR does automatic conversions from an analogue controls however not all XR Runtimes currently apply sensible thresholds.

We recommend as a workaround to use the Float type when interacting with triggers and grip buttons and apply your own threshold.

For buttons like A/B/X/Y and similar where there is no analogue option, the Bool type works fine.

You can bind the same action to multiple inputs for the same controller on the same profile. In this case the XR runtime will attempt to combine the inputs.

For Bool inputs, this will perform an OR operation between the buttons.

For Float inputs, this will take the highest value of the bound inputs.

The behavior for Pose inputs is undefined, but the first bound input is likely to be used.

You shouldn't bind multiple actions of the same action set to the same controller input. If you do this, or if actions are bound from multiple action sets but they have overlapping priorities, the behavior is undefined. The XR runtime may simply not accept your action map, or it may take this on a first come first serve basis.

We are still investigating the restrictions around binding multiple actions to the same output as this scenario makes sense. The OpenXR specification seems to not allow this.

Now that we have our basic actions defined, it's time to hook them up.

In OpenXR controller bindings are captured in so-called "Interaction Profiles". We've shortened it to "Profiles" because it takes up less space.

This generic name is chosen because controllers don't cover the entire system. Currently there are also profiles for trackers, remotes and tracked pens. There are also provisions for devices such as treadmills, haptic vests and such even though those are not part of the specification yet.

It is important to know that OpenXR has strict checking on supported devices. The core specification identifies a number of controllers and similar devices with their supported inputs and outputs. Every XR runtime must accept these interaction profiles even if they aren't applicable.

New devices are added through extensions and XR runtimes must specify which ones they support. XR runtimes that do not support a device added through extensions will not accept these profiles. XR runtimes that do not support added input or output types will often crash if supplied.

As such Godot keeps meta data of all available devices, their inputs and outputs and which extension adds support for them. You can create interaction profiles for all devices you wish to support. Godot will filter out those not supported by the XR runtime the user is using.

This does mean that in order to support new devices, you might need to update to a more recent version of Godot.

It is however also important to note that the action map has been designed with this in mind. When new devices enter the market, or when your users use devices that you do not have access to, the action map system relies on the XR runtime. It is the XR runtime's job to choose the best fitting interaction profile that has been specified and adapt it for the controller the user is using.

How the XR runtime does this is left to the implementation of the runtime and there are thus vast differences between the runtimes. Some runtimes might even permit users to edit the bindings themselves.

A common approach for a runtime is to look for a matching interaction profile first. If this is not found it will check the most common profiles such as that of the "Touch controller" and do a conversion. If all else fails, it will check the generic "Simple controller".

There is an important conclusion to be made here: When a controller is found, and the action map is applied to it, the XR runtime is not limited to the exact configurations you set up in Godot's action map editor. While the runtime will generally choose a suitable mapping based on one of the bindings you set up in the action map, it can deviate from it.

For example, when the Touch controller profile is used any of the following scenarios could be true:

we could be using a Quest 1 controller,

we could be using a Quest 2 controller,

we could be using a Quest Pro controller but no Quest Pro profile was given or the XR runtime being used does not support the Quest Pro controller,

it could be a completely different controller for which no profile was given but the XR runtime is using the touch bindings as a base.

Ergo, there currently is no way to know with certainty, which controller the user is actually using.

Finally, and this trips up a lot of people, the bindings aren't set in stone. It is fully allowed, and even expected, that an XR runtime allows a user to customise the bindings.

At the moment none of the XR runtimes offer this functionality though SteamVR has an existing UI from OpenVRs action map system that is still accessible. This is actively being worked on however.

Let's set up our first controller binding, using the Touch controller as an example.

Press "Add profile", find the Touch controller, and add it. If it is not in the list, then it may already have been added.

Our UI now shows panels for both the left and right controllers. The panels contain all of the possible inputs and outputs for each controller. We can use the + next to each entry to bind it to an action:

Let's finish our configuration:

Each action is bound the given input or output for both controllers to indicate that we support the action on either controller. The exception is the movement action which is bound only to the right hand controller. It is likely that we would want to use the left hand thumbstick for a different purpose, say a teleport function.

In developing your game/application you have to account for the possibility that the user changes the binding and binds the movement to the left hand thumbstick.

Also note that our shoot and grab boolean actions are linked to inputs of type Float. As mentioned before OpenXR will do conversions between the two, but do read the warning given on that subject earlier in this document.

Some of the inputs seem to appear in our list multiple times.

For instance we can find the X button twice, once as X click and then as X touch. This is due to the Touch controller having a capacitive sensor.

X touch will be true if the user is merely touching the X button.

X click will be true when the user is actually pressing down on the button.

Similarly for the thumbstick we have:

Thumbstick touch which will be true if the user is touching the thumbstick.

Thumbstick which gives a value for the direction the thumbstick is pushed to.

Thumbstick click which is true when the user is pressing down on the thumbstick.

It is important to note that only a select number of XR controllers support touch sensors or have click features on thumbsticks. Keep that in mind when designing your game/application. Make sure these are used for optional features of your game/application.

The "Simple controller" is a generic controller that OpenXR offers as a fallback. We'll apply our mapping:

As becomes painfully clear, the simple controller is often far too simple and falls short for anything but the simplest of VR games/applications.

This is why many XR runtimes only use it as a last resort and will attempt to use bindings from one of the more popular systems as a fallback first.

Due to the simple controller likely not covering the needs of your game, it is tempting to provide bindings for every controller supported by OpenXR. The default action map seems to suggest this as a valid course of action. As mentioned before, the default action map was designed for ease of migration from Godot 3.

It is the recommendation from the OpenXR Working Group that only bindings for controllers actually tested by the developer are setup. The XR runtimes are designed with this in mind. They can perform a better job of rebinding a provided binding than a developer can make educated guesses. Especially as the developer can't test if this leads to a comfortable experience for the end user.

This is our advice as well: limit your action map to the interaction profiles for devices you have actually tested your game with. The Oculus Touch controller is widely used as a fallback controller by many runtimes. If you are able to test your game using a Meta Rift or Quest and add this profile there is a high probability your game will work with other headsets.

One of the main goals of the action map is to remove the need for the application to know the hardware used. However, sometimes the hardware has physical differences that require inputs to be altered in ways other than how they are bound to actions. This need ranges from setting thresholds, to altering the inputs available on a controller.

Binding modifiers are not enabled by default and require enabling in the OpenXR project settings. Also there is no guarantee that these modifiers are supported by every runtime. You will need to consult the support for the runtimes you are targeting and decide whether to rely on the modifiers or implement some form of fallback mechanism.

If you are targeting multiple runtimes that have support for the same controllers, you may need to create separate action maps for each runtime. You can control which action map Godot uses by using different export templates for each runtime and using a custom feature tag to set the action map.

In Godot, binding modifiers are divided into two groups: modifiers that work on the interaction profile level, and modifiers that work on individual bindings.

Binding modifiers that are applied to the whole interaction profile can be accessed through the modifier button on the right side of the interaction profile editor.

You can add a new modifier by pressing the Add binding modifier button.

As Godot doesn't know which controllers and runtimes support a modifier, there is no restriction to adding modifiers. Unsupported modifiers will be ignored.

The dpad binding modifier adds new inputs to an interaction profile for each joystick and thumbpad input on this controller. It turns the input into a dpad with separate up, down, left and right inputs that are exposed as buttons:

Inputs related to extensions are denoted with an asterix.

In order to use the dpad binding modifier you need to enable the dpad binding modifier extension in project settings:

Enabling the extension is enough to make this functionality work using default settings.

Adding the modifier is optional and allows you to fine tune the way the dpad functionality behaves. You can add the modifier multiple times to set different settings for different inputs.

These settings are used as follows:

Action Set defines the action set to which these settings are applied.

Input Path defines the original input that is mapped to the new dpad inputs.

Threshold specifies the threshold value that will enable a dpad action, e.g. a value of 0.6 means that if the distance from center goes above 0.6 the dpad action is pressed.

Threshold Released specifies the threshold value that will disable a dpad action, e.g. a value of 0.4 means that if the distance from center goes below 0.4 the dpad action is released.

Center Region specifies the distance from center that enabled the center action, this is only supported for trackpads.

Wedge Angle specifies the angle of each wedge. A value of 90 degrees or lower means that up, down, left and right each have a separate slice in which they are in the pressed state. A value above 90 degrees means that the slices overlap and that multiple actions can be in the pressed state.

Is Sticky, when enabled means that an action stays in the pressed state until the thumbstick or trackpad moves into another wedge even if it has left the wedge for that action.

On Haptic lets us define a haptic output that is automatically activated when an action becomes pressed.

Off Haptic lets us define a haptic output that is automatically activated when an action is released.

Binding modifiers that are applied to individual bindings can be accessed through the binding modifier button next to action attached to an input:

You can add a new modifier by pressing the Add binding modifier button.

As Godot doesn't know which inputs on each runtime support a modifier, there is no restriction to adding modifiers. If the modifier extension is unsupported, modifiers will be filtered out at runtime. Modifiers added to the wrong input may result in a runtime error.

You should test your action map on the actual hardware and runtime to verify the proper setup.

The analog threshold modifier allows you to specify the thresholds used for any analog input, like the trigger, that has a boolean input. This controls when the input is in the pressed state.

In order to use this modifier you must enable the analog threshold extension in the project settings:

The analog threshold modifier has the following settings:

These are defined as follows:

On Threshold specifies the threshold value that will enable the action, e.g. a value of 0.6 means that when the analog value gets above 0.6 the action is set to the pressed state.

Off Threshold specifies the threshold value that will disable the action, e.g. a value of 0.4 means that when the analog value goes below 0.4 the action is set in to the released state.

On Haptic lets us define a haptic output that is automatically activated when the input is pressed.

Off Haptic lets us define a haptic output that is automatically activated when the input is released.

Modifiers can support automatic haptic output that is triggered when thresholds are reached.

Currently both available modifiers support this feature however there is no rule future modifiers also have this capability. Only one type of haptic feedback is supported but in the future other options may become available.

The haptic vibration allows us to specify a simple haptic pulse:

It has the following options:

Duration is the duration of the pulse in nanoseconds. -1 lets the runtime choose an optimal value for a short pulse suitable for the current hardware.

Frequency is the frequency of the pulse in Hz. 0 lets the runtime choose an optimal frequency for a short pulse suitable for the current hardware.

Amplitude is the amplitude of the pulse.

Please read the User-contributed notes policy before submitting a comment.

---

## TouchScreenButton

**URL:** https://docs.godotengine.org/en/stable/classes/class_touchscreenbutton.html

**Contents:**
- TouchScreenButton
- Description
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Node2D < CanvasItem < Node < Object

Button for touch screen devices for gameplay use.

TouchScreenButton allows you to create on-screen buttons for touch devices. It's intended for gameplay use, such as a unit you have to touch to move. Unlike Button, TouchScreenButton supports multitouch out of the box. Several TouchScreenButtons can be pressed at the same time with touch input.

This node inherits from Node2D. Unlike with Control nodes, you cannot set anchors on it. If you want to create menus or user interfaces, you may want to use Button nodes instead. To make button nodes react to touch events, you can enable ProjectSettings.input_devices/pointing/emulate_mouse_from_touch in the Project Settings.

You can configure TouchScreenButton to be visible only on touch devices, helping you develop your game both for desktop and mobile devices.

Emitted when the button is pressed (down).

Emitted when the button is released (up).

enum VisibilityMode: 🔗

VisibilityMode VISIBILITY_ALWAYS = 0

VisibilityMode VISIBILITY_TOUCHSCREEN_ONLY = 1

Visible on touch screens only.

void set_action(value: String)

The button's action. Actions can be handled with InputEventAction.

void set_bitmask(value: BitMap)

The button's bitmask.

bool passby_press = false 🔗

void set_passby_press(value: bool)

bool is_passby_press_enabled()

If true, the pressed and released signals are emitted whenever a pressed finger goes in and out of the button, even if the pressure started outside the active area of the button.

Note: This is a "pass-by" (not "bypass") press mode.

void set_shape(value: Shape2D)

bool shape_centered = true 🔗

void set_shape_centered(value: bool)

bool is_shape_centered()

If true, the button's shape is centered in the provided texture. If no texture is used, this property has no effect.

bool shape_visible = true 🔗

void set_shape_visible(value: bool)

bool is_shape_visible()

If true, the button's shape is visible in the editor.

Texture2D texture_normal 🔗

void set_texture_normal(value: Texture2D)

Texture2D get_texture_normal()

The button's texture for the normal state.

Texture2D texture_pressed 🔗

void set_texture_pressed(value: Texture2D)

Texture2D get_texture_pressed()

The button's texture for the pressed state.

VisibilityMode visibility_mode = 0 🔗

void set_visibility_mode(value: VisibilityMode)

VisibilityMode get_visibility_mode()

The button's visibility mode.

bool is_pressed() const 🔗

Returns true if this button is currently pressed.

Please read the User-contributed notes policy before submitting a comment.

---

## TreeItem

**URL:** https://docs.godotengine.org/en/stable/classes/class_treeitem.html

**Contents:**
- TreeItem
- Description
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

An internal control for a single item inside Tree.

A single item of a Tree control. It can contain other TreeItems as children, which allows it to create a hierarchy. It can also contain text and buttons. TreeItem is not a Node, it is internal to the Tree.

To create a TreeItem, use Tree.create_item() or create_child(). To remove a TreeItem, use Object.free().

Note: The ID values used for buttons are 32-bit, unlike int which is always 64-bit. They go from -2147483648 to 2147483647.

custom_minimum_height

add_button(column: int, button: Texture2D, id: int = -1, disabled: bool = false, tooltip_text: String = "", description: String = "")

add_child(child: TreeItem)

call_recursive(method: StringName, ...) vararg

clear_custom_bg_color(column: int)

clear_custom_color(column: int)

create_child(index: int = -1)

deselect(column: int)

erase_button(column: int, button_index: int)

get_auto_translate_mode(column: int) const

get_autowrap_mode(column: int) const

get_button(column: int, button_index: int) const

get_button_by_id(column: int, id: int) const

get_button_color(column: int, id: int) const

get_button_count(column: int) const

get_button_id(column: int, button_index: int) const

get_button_tooltip_text(column: int, button_index: int) const

get_cell_mode(column: int) const

get_child(index: int)

get_custom_bg_color(column: int) const

get_custom_color(column: int) const

get_custom_draw_callback(column: int) const

get_custom_font(column: int) const

get_custom_font_size(column: int) const

get_description(column: int) const

get_expand_right(column: int) const

get_first_child() const

get_icon(column: int) const

get_icon_max_width(column: int) const

get_icon_modulate(column: int) const

get_icon_overlay(column: int) const

get_icon_region(column: int) const

get_language(column: int) const

get_metadata(column: int) const

get_next_in_tree(wrap: bool = false)

get_next_visible(wrap: bool = false)

get_prev_in_tree(wrap: bool = false)

get_prev_visible(wrap: bool = false)

get_range(column: int) const

get_range_config(column: int)

get_structured_text_bidi_override(column: int) const

get_structured_text_bidi_override_options(column: int) const

get_suffix(column: int) const

get_text(column: int) const

get_text_alignment(column: int) const

get_text_direction(column: int) const

get_text_overrun_behavior(column: int) const

get_tooltip_text(column: int) const

is_any_collapsed(only_visible: bool = false)

is_button_disabled(column: int, button_index: int) const

is_checked(column: int) const

is_custom_set_as_button(column: int) const

is_edit_multiline(column: int) const

is_editable(column: int)

is_indeterminate(column: int) const

is_selectable(column: int) const

is_selected(column: int)

is_visible_in_tree() const

move_after(item: TreeItem)

move_before(item: TreeItem)

propagate_check(column: int, emit_signal: bool = true)

remove_child(child: TreeItem)

set_auto_translate_mode(column: int, mode: AutoTranslateMode)

set_autowrap_mode(column: int, autowrap_mode: AutowrapMode)

set_button(column: int, button_index: int, button: Texture2D)

set_button_color(column: int, button_index: int, color: Color)

set_button_description(column: int, button_index: int, description: String)

set_button_disabled(column: int, button_index: int, disabled: bool)

set_button_tooltip_text(column: int, button_index: int, tooltip: String)

set_cell_mode(column: int, mode: TreeCellMode)

set_checked(column: int, checked: bool)

set_collapsed_recursive(enable: bool)

set_custom_as_button(column: int, enable: bool)

set_custom_bg_color(column: int, color: Color, just_outline: bool = false)

set_custom_color(column: int, color: Color)

set_custom_draw(column: int, object: Object, callback: StringName)

set_custom_draw_callback(column: int, callback: Callable)

set_custom_font(column: int, font: Font)

set_custom_font_size(column: int, font_size: int)

set_description(column: int, description: String)

set_edit_multiline(column: int, multiline: bool)

set_editable(column: int, enabled: bool)

set_expand_right(column: int, enable: bool)

set_icon(column: int, texture: Texture2D)

set_icon_max_width(column: int, width: int)

set_icon_modulate(column: int, modulate: Color)

set_icon_overlay(column: int, texture: Texture2D)

set_icon_region(column: int, region: Rect2)

set_indeterminate(column: int, indeterminate: bool)

set_language(column: int, language: String)

set_metadata(column: int, meta: Variant)

set_range(column: int, value: float)

set_range_config(column: int, min: float, max: float, step: float, expr: bool = false)

set_selectable(column: int, selectable: bool)

set_structured_text_bidi_override(column: int, parser: StructuredTextParser)

set_structured_text_bidi_override_options(column: int, args: Array)

set_suffix(column: int, text: String)

set_text(column: int, text: String)

set_text_alignment(column: int, text_alignment: HorizontalAlignment)

set_text_direction(column: int, direction: TextDirection)

set_text_overrun_behavior(column: int, overrun_behavior: OverrunBehavior)

set_tooltip_text(column: int, tooltip: String)

TreeCellMode CELL_MODE_STRING = 0

Cell shows a string label, optionally with an icon. When editable, the text can be edited using a LineEdit, or a TextEdit popup if set_edit_multiline() is used.

TreeCellMode CELL_MODE_CHECK = 1

Cell shows a checkbox, optionally with text and an icon. The checkbox can be pressed, released, or indeterminate (via set_indeterminate()). The checkbox can't be clicked unless the cell is editable.

TreeCellMode CELL_MODE_RANGE = 2

Cell shows a numeric range. When editable, it can be edited using a range slider. Use set_range() to set the value and set_range_config() to configure the range.

This cell can also be used in a text dropdown mode when you assign a text with set_text(). Separate options with a comma, e.g. "Option1,Option2,Option3".

TreeCellMode CELL_MODE_ICON = 3

Cell shows an icon. It can't be edited nor display text. The icon is always centered within the cell.

TreeCellMode CELL_MODE_CUSTOM = 4

Cell shows as a clickable button. It will display an arrow similar to OptionButton, but doesn't feature a dropdown (for that you can use CELL_MODE_RANGE). Clicking the button emits the Tree.item_edited signal. The button is flat by default, you can use set_custom_as_button() to display it with a StyleBox.

This mode also supports custom drawing using set_custom_draw_callback().

void set_collapsed(value: bool)

If true, the TreeItem is collapsed.

int custom_minimum_height 🔗

void set_custom_minimum_height(value: int)

int get_custom_minimum_height()

The custom minimum height.

bool disable_folding 🔗

void set_disable_folding(value: bool)

bool is_folding_disabled()

If true, folding is disabled for this TreeItem.

void set_visible(value: bool)

If true, the TreeItem is visible (default).

Note that if a TreeItem is set to not be visible, none of its children will be visible either.

void add_button(column: int, button: Texture2D, id: int = -1, disabled: bool = false, tooltip_text: String = "", description: String = "") 🔗

Adds a button with Texture2D button to the end of the cell at column column. The id is used to identify the button in the according Tree.button_clicked signal and can be different from the buttons index. If not specified, the next available index is used, which may be retrieved by calling get_button_count() immediately before this method. Optionally, the button can be disabled and have a tooltip_text. description is used as the button description for assistive apps.

void add_child(child: TreeItem) 🔗

Adds a previously unparented TreeItem as a direct child of this one. The child item must not be a part of any Tree or parented to any TreeItem. See also remove_child().

void call_recursive(method: StringName, ...) vararg 🔗

Calls the method on the actual TreeItem and its children recursively. Pass parameters as a comma separated list.

void clear_buttons() 🔗

Removes all buttons from all columns of this item.

void clear_custom_bg_color(column: int) 🔗

Resets the background color for the given column to default.

void clear_custom_color(column: int) 🔗

Resets the color for the given column to default.

TreeItem create_child(index: int = -1) 🔗

Creates an item and adds it as a child.

The new item will be inserted as position index (the default value -1 means the last position), or it will be the last child if index is higher than the child count.

void deselect(column: int) 🔗

Deselects the given column.

void erase_button(column: int, button_index: int) 🔗

Removes the button at index button_index in column column.

AutoTranslateMode get_auto_translate_mode(column: int) const 🔗

Returns the column's auto translate mode.

AutowrapMode get_autowrap_mode(column: int) const 🔗

Returns the text autowrap mode in the given column. By default it is TextServer.AUTOWRAP_OFF.

Texture2D get_button(column: int, button_index: int) const 🔗

Returns the Texture2D of the button at index button_index in column column.

int get_button_by_id(column: int, id: int) const 🔗

Returns the button index if there is a button with ID id in column column, otherwise returns -1.

Color get_button_color(column: int, id: int) const 🔗

Returns the color of the button with ID id in column column. If the specified button does not exist, returns Color.BLACK.

int get_button_count(column: int) const 🔗

Returns the number of buttons in column column.

int get_button_id(column: int, button_index: int) const 🔗

Returns the ID for the button at index button_index in column column.

String get_button_tooltip_text(column: int, button_index: int) const 🔗

Returns the tooltip text for the button at index button_index in column column.

TreeCellMode get_cell_mode(column: int) const 🔗

Returns the column's cell mode.

TreeItem get_child(index: int) 🔗

Returns a child item by its index (see get_child_count()). This method is often used for iterating all children of an item.

Negative indices access the children from the last one.

int get_child_count() 🔗

Returns the number of child items.

Array[TreeItem] get_children() 🔗

Returns an array of references to the item's children.

Color get_custom_bg_color(column: int) const 🔗

Returns the custom background color of column column.

Color get_custom_color(column: int) const 🔗

Returns the custom color of column column.

Callable get_custom_draw_callback(column: int) const 🔗

Returns the custom callback of column column.

Font get_custom_font(column: int) const 🔗

Returns custom font used to draw text in the column column.

int get_custom_font_size(column: int) const 🔗

Returns custom font size used to draw text in the column column.

String get_description(column: int) const 🔗

Returns the given column's description for assistive apps.

bool get_expand_right(column: int) const 🔗

Returns true if expand_right is set.

TreeItem get_first_child() const 🔗

Returns the TreeItem's first child.

Texture2D get_icon(column: int) const 🔗

Returns the given column's icon Texture2D. Error if no icon is set.

int get_icon_max_width(column: int) const 🔗

Returns the maximum allowed width of the icon in the given column.

Color get_icon_modulate(column: int) const 🔗

Returns the Color modulating the column's icon.

Texture2D get_icon_overlay(column: int) const 🔗

Returns the given column's icon overlay Texture2D.

Rect2 get_icon_region(column: int) const 🔗

Returns the icon Texture2D region as Rect2.

Returns the node's order in the tree. For example, if called on the first child item the position is 0.

String get_language(column: int) const 🔗

Returns item's text language code.

Variant get_metadata(column: int) const 🔗

Returns the metadata value that was set for the given column using set_metadata().

TreeItem get_next() const 🔗

Returns the next sibling TreeItem in the tree or a null object if there is none.

TreeItem get_next_in_tree(wrap: bool = false) 🔗

Returns the next TreeItem in the tree (in the context of a depth-first search) or a null object if there is none.

If wrap is enabled, the method will wrap around to the first element in the tree when called on the last element, otherwise it returns null.

TreeItem get_next_visible(wrap: bool = false) 🔗

Returns the next visible TreeItem in the tree (in the context of a depth-first search) or a null object if there is none.

If wrap is enabled, the method will wrap around to the first visible element in the tree when called on the last visible element, otherwise it returns null.

TreeItem get_parent() const 🔗

Returns the parent TreeItem or a null object if there is none.

TreeItem get_prev() 🔗

Returns the previous sibling TreeItem in the tree or a null object if there is none.

TreeItem get_prev_in_tree(wrap: bool = false) 🔗

Returns the previous TreeItem in the tree (in the context of a depth-first search) or a null object if there is none.

If wrap is enabled, the method will wrap around to the last element in the tree when called on the first visible element, otherwise it returns null.

TreeItem get_prev_visible(wrap: bool = false) 🔗

Returns the previous visible sibling TreeItem in the tree (in the context of a depth-first search) or a null object if there is none.

If wrap is enabled, the method will wrap around to the last visible element in the tree when called on the first visible element, otherwise it returns null.

float get_range(column: int) const 🔗

Returns the value of a CELL_MODE_RANGE column.

Dictionary get_range_config(column: int) 🔗

Returns a dictionary containing the range parameters for a given column. The keys are "min", "max", "step", and "expr".

StructuredTextParser get_structured_text_bidi_override(column: int) const 🔗

Returns the BiDi algorithm override set for this cell.

Array get_structured_text_bidi_override_options(column: int) const 🔗

Returns the additional BiDi options set for this cell.

String get_suffix(column: int) const 🔗

Gets the suffix string shown after the column value.

String get_text(column: int) const 🔗

Returns the given column's text.

HorizontalAlignment get_text_alignment(column: int) const 🔗

Returns the given column's text alignment.

TextDirection get_text_direction(column: int) const 🔗

Returns item's text base writing direction.

OverrunBehavior get_text_overrun_behavior(column: int) const 🔗

Returns the clipping behavior when the text exceeds the item's bounding rectangle in the given column. By default it is TextServer.OVERRUN_TRIM_ELLIPSIS.

String get_tooltip_text(column: int) const 🔗

Returns the given column's tooltip text.

Tree get_tree() const 🔗

Returns the Tree that owns this TreeItem.

bool is_any_collapsed(only_visible: bool = false) 🔗

Returns true if this TreeItem, or any of its descendants, is collapsed.

If only_visible is true it ignores non-visible TreeItems.

bool is_button_disabled(column: int, button_index: int) const 🔗

Returns true if the button at index button_index for the given column is disabled.

bool is_checked(column: int) const 🔗

Returns true if the given column is checked.

bool is_custom_set_as_button(column: int) const 🔗

Returns true if the cell was made into a button with set_custom_as_button().

bool is_edit_multiline(column: int) const 🔗

Returns true if the given column is multiline editable.

bool is_editable(column: int) 🔗

Returns true if the given column is editable.

bool is_indeterminate(column: int) const 🔗

Returns true if the given column is indeterminate.

bool is_selectable(column: int) const 🔗

Returns true if the given column is selectable.

bool is_selected(column: int) 🔗

Returns true if the given column is selected.

bool is_visible_in_tree() const 🔗

Returns true if visible is true and all its ancestors are also visible.

void move_after(item: TreeItem) 🔗

Moves this TreeItem right after the given item.

Note: You can't move to the root or move the root.

void move_before(item: TreeItem) 🔗

Moves this TreeItem right before the given item.

Note: You can't move to the root or move the root.

void propagate_check(column: int, emit_signal: bool = true) 🔗

Propagates this item's checked status to its children and parents for the given column. It is possible to process the items affected by this method call by connecting to Tree.check_propagated_to_item. The order that the items affected will be processed is as follows: the item invoking this method, children of that item, and finally parents of that item. If emit_signal is false, then Tree.check_propagated_to_item will not be emitted.

void remove_child(child: TreeItem) 🔗

Removes the given child TreeItem and all its children from the Tree. Note that it doesn't free the item from memory, so it can be reused later (see add_child()). To completely remove a TreeItem use Object.free().

Note: If you want to move a child from one Tree to another, then instead of removing and adding it manually you can use move_before() or move_after().

void select(column: int) 🔗

Selects the given column.

void set_auto_translate_mode(column: int, mode: AutoTranslateMode) 🔗

Sets the given column's auto translate mode to mode.

All columns use Node.AUTO_TRANSLATE_MODE_INHERIT by default, which uses the same auto translate mode as the Tree itself.

void set_autowrap_mode(column: int, autowrap_mode: AutowrapMode) 🔗

Sets the autowrap mode in the given column. If set to something other than TextServer.AUTOWRAP_OFF, the text gets wrapped inside the cell's bounding rectangle.

void set_button(column: int, button_index: int, button: Texture2D) 🔗

Sets the given column's button Texture2D at index button_index to button.

void set_button_color(column: int, button_index: int, color: Color) 🔗

Sets the given column's button color at index button_index to color.

void set_button_description(column: int, button_index: int, description: String) 🔗

Sets the given column's button description at index button_index for assistive apps.

void set_button_disabled(column: int, button_index: int, disabled: bool) 🔗

If true, disables the button at index button_index in the given column.

void set_button_tooltip_text(column: int, button_index: int, tooltip: String) 🔗

Sets the tooltip text for the button at index button_index in the given column.

void set_cell_mode(column: int, mode: TreeCellMode) 🔗

Sets the given column's cell mode to mode. This determines how the cell is displayed and edited.

void set_checked(column: int, checked: bool) 🔗

If checked is true, the given column is checked. Clears column's indeterminate status.

void set_collapsed_recursive(enable: bool) 🔗

Collapses or uncollapses this TreeItem and all the descendants of this item.

void set_custom_as_button(column: int, enable: bool) 🔗

Makes a cell with CELL_MODE_CUSTOM display as a non-flat button with a StyleBox.

void set_custom_bg_color(column: int, color: Color, just_outline: bool = false) 🔗

Sets the given column's custom background color and whether to just use it as an outline.

void set_custom_color(column: int, color: Color) 🔗

Sets the given column's custom color.

void set_custom_draw(column: int, object: Object, callback: StringName) 🔗

Deprecated: Use set_custom_draw_callback() instead.

Sets the given column's custom draw callback to the callback method on object.

The method named callback should accept two arguments: the TreeItem that is drawn and its position and size as a Rect2.

void set_custom_draw_callback(column: int, callback: Callable) 🔗

Sets the given column's custom draw callback. Use an empty Callable (Callable()) to clear the custom callback. The cell has to be in CELL_MODE_CUSTOM to use this feature.

The callback should accept two arguments: the TreeItem that is drawn and its position and size as a Rect2.

void set_custom_font(column: int, font: Font) 🔗

Sets custom font used to draw text in the given column.

void set_custom_font_size(column: int, font_size: int) 🔗

Sets custom font size used to draw text in the given column.

void set_description(column: int, description: String) 🔗

Sets the given column's description for assistive apps.

void set_edit_multiline(column: int, multiline: bool) 🔗

If multiline is true, the given column is multiline editable.

Note: This option only affects the type of control (LineEdit or TextEdit) that appears when editing the column. You can set multiline values with set_text() even if the column is not multiline editable.

void set_editable(column: int, enabled: bool) 🔗

If enabled is true, the given column is editable.

void set_expand_right(column: int, enable: bool) 🔗

If enable is true, the given column is expanded to the right.

void set_icon(column: int, texture: Texture2D) 🔗

Sets the given cell's icon Texture2D. If the cell is in CELL_MODE_ICON mode, the icon is displayed in the center of the cell. Otherwise, the icon is displayed before the cell's text. CELL_MODE_RANGE does not display an icon.

void set_icon_max_width(column: int, width: int) 🔗

Sets the maximum allowed width of the icon in the given column. This limit is applied on top of the default size of the icon and on top of Tree.icon_max_width. The height is adjusted according to the icon's ratio.

void set_icon_modulate(column: int, modulate: Color) 🔗

Modulates the given column's icon with modulate.

void set_icon_overlay(column: int, texture: Texture2D) 🔗

Sets the given cell's icon overlay Texture2D. The cell has to be in CELL_MODE_ICON mode, and icon has to be set. Overlay is drawn on top of icon, in the bottom left corner.

void set_icon_region(column: int, region: Rect2) 🔗

Sets the given column's icon's texture region.

void set_indeterminate(column: int, indeterminate: bool) 🔗

If indeterminate is true, the given column is marked indeterminate.

Note: If set true from false, then column is cleared of checked status.

void set_language(column: int, language: String) 🔗

Sets language code of item's text used for line-breaking and text shaping algorithms, if left empty current locale is used instead.

void set_metadata(column: int, meta: Variant) 🔗

Sets the metadata value for the given column, which can be retrieved later using get_metadata(). This can be used, for example, to store a reference to the original data.

void set_range(column: int, value: float) 🔗

Sets the value of a CELL_MODE_RANGE column.

void set_range_config(column: int, min: float, max: float, step: float, expr: bool = false) 🔗

Sets the range of accepted values for a column. The column must be in the CELL_MODE_RANGE mode.

If expr is true, the edit mode slider will use an exponential scale as with Range.exp_edit.

void set_selectable(column: int, selectable: bool) 🔗

If selectable is true, the given column is selectable.

void set_structured_text_bidi_override(column: int, parser: StructuredTextParser) 🔗

Set BiDi algorithm override for the structured text. Has effect for cells that display text.

void set_structured_text_bidi_override_options(column: int, args: Array) 🔗

Set additional options for BiDi override. Has effect for cells that display text.

void set_suffix(column: int, text: String) 🔗

Sets a string to be shown after a column's value (for example, a unit abbreviation).

void set_text(column: int, text: String) 🔗

Sets the given column's text value.

void set_text_alignment(column: int, text_alignment: HorizontalAlignment) 🔗

Sets the given column's text alignment to text_alignment.

void set_text_direction(column: int, direction: TextDirection) 🔗

Sets item's text base writing direction.

void set_text_overrun_behavior(column: int, overrun_behavior: OverrunBehavior) 🔗

Sets the clipping behavior when the text exceeds the item's bounding rectangle in the given column.

void set_tooltip_text(column: int, tooltip: String) 🔗

Sets the given column's tooltip text.

void uncollapse_tree() 🔗

Uncollapses all TreeItems necessary to reveal this TreeItem, i.e. all ancestor TreeItems.

Please read the User-contributed notes policy before submitting a comment.

---

## Tree

**URL:** https://docs.godotengine.org/en/stable/classes/class_tree.html

**Contents:**
- Tree
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions

Inherits: Control < CanvasItem < Node < Object

A control used to show a set of internal TreeItems in a hierarchical structure.

A control used to show a set of internal TreeItems in a hierarchical structure. The tree items can be selected, expanded and collapsed. The tree can have multiple columns with custom controls like LineEdits, buttons and popups. It can be useful for structured displays and interactions.

Trees are built via code, using TreeItem objects to create the structure. They have a single root, but multiple roots can be simulated with hide_root:

To iterate over all the TreeItem objects in a Tree object, use TreeItem.get_next() and TreeItem.get_first_child() after getting the root through get_root(). You can use Object.free() on a TreeItem to remove it from the Tree.

Incremental search: Like ItemList and PopupMenu, Tree supports searching within the list while the control is focused. Press a key that matches the first letter of an item's name to select the first item starting with the given letter. After that point, there are two ways to perform incremental search: 1) Press the same key again before the timeout duration to select the next item starting with the same letter. 2) Press letter keys that match the rest of the word before the timeout duration to match to select the item in question directly. Both of these actions will be reset to the beginning of the list if the timeout duration has passed since the last keystroke was registered. You can adjust the timeout duration by changing ProjectSettings.gui/timers/incremental_search_max_interval_msec.

true (overrides Control)

column_titles_visible

enable_recursive_folding

2 (overrides Control)

scroll_horizontal_enabled

scroll_vertical_enabled

create_item(parent: TreeItem = null, index: int = -1)

edit_selected(force_edit: bool = false)

ensure_cursor_is_visible()

get_button_id_at_position(position: Vector2) const

get_column_at_position(position: Vector2) const

get_column_expand_ratio(column: int) const

get_column_title(column: int) const

get_column_title_alignment(column: int) const

get_column_title_direction(column: int) const

get_column_title_language(column: int) const

get_column_width(column: int) const

get_custom_popup_rect() const

get_drop_section_at_position(position: Vector2) const

get_edited_column() const

get_item_area_rect(item: TreeItem, column: int = -1, button_index: int = -1) const

get_item_at_position(position: Vector2) const

get_next_selected(from: TreeItem)

get_pressed_button() const

get_selected_column() const

is_column_clipping_content(column: int) const

is_column_expanding(column: int) const

scroll_to_item(item: TreeItem, center_on_item: bool = false)

set_column_clip_content(column: int, enable: bool)

set_column_custom_minimum_width(column: int, min_width: int)

set_column_expand(column: int, expand: bool)

set_column_expand_ratio(column: int, ratio: int)

set_column_title(column: int, title: String)

set_column_title_alignment(column: int, title_alignment: HorizontalAlignment)

set_column_title_direction(column: int, direction: TextDirection)

set_column_title_language(column: int, language: String)

set_selected(item: TreeItem, column: int)

children_hl_line_color

Color(0.27, 0.27, 0.27, 1)

custom_button_font_highlight

Color(0.95, 0.95, 0.95, 1)

Color(0.7, 0.7, 0.7, 1)

Color(0.875, 0.875, 0.875, 0.5)

Color(0.95, 0.95, 0.95, 1)

font_hovered_dimmed_color

Color(0.875, 0.875, 0.875, 1)

font_hovered_selected_color

Color(0.7, 0.7, 0.7, 0.25)

Color(0.27, 0.27, 0.27, 1)

relationship_line_color

Color(0.27, 0.27, 0.27, 1)

Color(0.875, 0.875, 0.875, 1)

children_hl_line_width

draw_relationship_lines

inner_item_margin_bottom

inner_item_margin_left

inner_item_margin_right

inner_item_margin_top

parent_hl_line_margin

relationship_line_width

scrollbar_h_separation

scrollbar_margin_bottom

scrollbar_margin_left

scrollbar_margin_right

scrollbar_v_separation

title_button_font_size

arrow_collapsed_mirrored

indeterminate_disabled

custom_button_pressed

hovered_selected_focus

button_clicked(item: TreeItem, column: int, id: int, mouse_button_index: int) 🔗

Emitted when a button on the tree was pressed (see TreeItem.add_button()).

Emitted when a cell is selected.

check_propagated_to_item(item: TreeItem, column: int) 🔗

Emitted when TreeItem.propagate_check() is called. Connect to this signal to process the items that are affected when TreeItem.propagate_check() is invoked. The order that the items affected will be processed is as follows: the item that invoked the method, children of that item, and finally parents of that item.

column_title_clicked(column: int, mouse_button_index: int) 🔗

Emitted when a column's title is clicked with either @GlobalScope.MOUSE_BUTTON_LEFT or @GlobalScope.MOUSE_BUTTON_RIGHT.

custom_item_clicked(mouse_button_index: int) 🔗

Emitted when an item with TreeItem.CELL_MODE_CUSTOM is clicked with a mouse button.

custom_popup_edited(arrow_clicked: bool) 🔗

Emitted when a cell with the TreeItem.CELL_MODE_CUSTOM is clicked to be edited.

empty_clicked(click_position: Vector2, mouse_button_index: int) 🔗

Emitted when a mouse button is clicked in the empty space of the tree.

Emitted when an item is double-clicked, or selected with a ui_accept input event (e.g. using Enter or Space on the keyboard).

item_collapsed(item: TreeItem) 🔗

Emitted when an item is expanded or collapsed by clicking on the folding arrow or through code.

Note: Despite its name, this signal is also emitted when an item is expanded.

Emitted when an item is edited.

item_icon_double_clicked() 🔗

Emitted when an item's icon is double-clicked. For a signal that emits when any part of the item is double-clicked, see item_activated.

item_mouse_selected(mouse_position: Vector2, mouse_button_index: int) 🔗

Emitted when an item is selected with a mouse button.

Emitted when an item is selected.

multi_selected(item: TreeItem, column: int, selected: bool) 🔗

Emitted instead of item_selected if select_mode is set to SELECT_MULTI.

Emitted when a left mouse button click does not select any item.

SelectMode SELECT_SINGLE = 0

Allows selection of a single cell at a time. From the perspective of items, only a single item is allowed to be selected. And there is only one column selected in the selected item.

The focus cursor is always hidden in this mode, but it is positioned at the current selection, making the currently selected item the currently focused item.

SelectMode SELECT_ROW = 1

Allows selection of a single row at a time. From the perspective of items, only a single items is allowed to be selected. And all the columns are selected in the selected item.

The focus cursor is always hidden in this mode, but it is positioned at the first column of the current selection, making the currently selected item the currently focused item.

SelectMode SELECT_MULTI = 2

Allows selection of multiple cells at the same time. From the perspective of items, multiple items are allowed to be selected. And there can be multiple columns selected in each selected item.

The focus cursor is visible in this mode, the item or column under the cursor is not necessarily selected.

enum DropModeFlags: 🔗

DropModeFlags DROP_MODE_DISABLED = 0

Disables all drop sections, but still allows to detect the "on item" drop section by get_drop_section_at_position().

Note: This is the default flag, it has no effect when combined with other flags.

DropModeFlags DROP_MODE_ON_ITEM = 1

Enables the "on item" drop section. This drop section covers the entire item.

When combined with DROP_MODE_INBETWEEN, this drop section halves the height and stays centered vertically.

DropModeFlags DROP_MODE_INBETWEEN = 2

Enables "above item" and "below item" drop sections. The "above item" drop section covers the top half of the item, and the "below item" drop section covers the bottom half.

When combined with DROP_MODE_ON_ITEM, these drop sections halves the height and stays on top / bottom accordingly.

bool allow_reselect = false 🔗

void set_allow_reselect(value: bool)

bool get_allow_reselect()

If true, the currently selected cell may be selected again.

bool allow_rmb_select = false 🔗

void set_allow_rmb_select(value: bool)

bool get_allow_rmb_select()

If true, a right mouse button click can select items.

bool allow_search = true 🔗

void set_allow_search(value: bool)

bool get_allow_search()

If true, allows navigating the Tree with letter keys through incremental search.

bool auto_tooltip = true 🔗

void set_auto_tooltip(value: bool)

bool is_auto_tooltip_enabled()

If true, tree items with no tooltip assigned display their text as their tooltip. See also TreeItem.get_tooltip_text() and TreeItem.get_button_tooltip_text().

bool column_titles_visible = false 🔗

void set_column_titles_visible(value: bool)

bool are_column_titles_visible()

If true, column titles are visible.

void set_columns(value: int)

The number of columns.

int drop_mode_flags = 0 🔗

void set_drop_mode_flags(value: int)

int get_drop_mode_flags()

The drop mode as an OR combination of flags. See DropModeFlags constants. Once dropping is done, reverts to DROP_MODE_DISABLED. Setting this during Control._can_drop_data() is recommended.

This controls the drop sections, i.e. the decision and drawing of possible drop locations based on the mouse position.

bool enable_recursive_folding = true 🔗

void set_enable_recursive_folding(value: bool)

bool is_recursive_folding_enabled()

If true, recursive folding is enabled for this Tree. Holding down Shift while clicking the fold arrow or using ui_right/ui_left shortcuts collapses or uncollapses the TreeItem and all its descendants.

bool hide_folding = false 🔗

void set_hide_folding(value: bool)

bool is_folding_hidden()

If true, the folding arrow is hidden.

bool hide_root = false 🔗

void set_hide_root(value: bool)

bool is_root_hidden()

If true, the tree's root is hidden.

bool scroll_horizontal_enabled = true 🔗

void set_h_scroll_enabled(value: bool)

bool is_h_scroll_enabled()

If true, enables horizontal scrolling.

bool scroll_vertical_enabled = true 🔗

void set_v_scroll_enabled(value: bool)

bool is_v_scroll_enabled()

If true, enables vertical scrolling.

SelectMode select_mode = 0 🔗

void set_select_mode(value: SelectMode)

SelectMode get_select_mode()

Allows single or multiple selection. See the SelectMode constants.

Clears the tree. This removes all items.

TreeItem create_item(parent: TreeItem = null, index: int = -1) 🔗

Creates an item in the tree and adds it as a child of parent, which can be either a valid TreeItem or null.

If parent is null, the root item will be the parent, or the new item will be the root itself if the tree is empty.

The new item will be the index-th child of parent, or it will be the last child if there are not enough siblings.

void deselect_all() 🔗

Deselects all tree items (rows and columns). In SELECT_MULTI mode also removes selection cursor.

bool edit_selected(force_edit: bool = false) 🔗

Edits the selected tree item as if it was clicked.

Either the item must be set editable with TreeItem.set_editable() or force_edit must be true.

Returns true if the item could be edited. Fails if no item is selected.

void ensure_cursor_is_visible() 🔗

Makes the currently focused cell visible.

This will scroll the tree if necessary. In SELECT_ROW mode, this will not do horizontal scrolling, as all the cells in the selected row is focused logically.

Note: Despite the name of this method, the focus cursor itself is only visible in SELECT_MULTI mode.

int get_button_id_at_position(position: Vector2) const 🔗

Returns the button ID at position, or -1 if no button is there.

int get_column_at_position(position: Vector2) const 🔗

Returns the column index at position, or -1 if no item is there.

int get_column_expand_ratio(column: int) const 🔗

Returns the expand ratio assigned to the column.

String get_column_title(column: int) const 🔗

Returns the column's title.

HorizontalAlignment get_column_title_alignment(column: int) const 🔗

Returns the column title alignment.

TextDirection get_column_title_direction(column: int) const 🔗

Returns column title base writing direction.

String get_column_title_language(column: int) const 🔗

Returns column title language code.

int get_column_width(column: int) const 🔗

Returns the column's width in pixels.

Rect2 get_custom_popup_rect() const 🔗

Returns the rectangle for custom popups. Helper to create custom cell controls that display a popup. See TreeItem.set_cell_mode().

int get_drop_section_at_position(position: Vector2) const 🔗

Returns the drop section at position, or -100 if no item is there.

Values -1, 0, or 1 will be returned for the "above item", "on item", and "below item" drop sections, respectively. See DropModeFlags for a description of each drop section.

To get the item which the returned drop section is relative to, use get_item_at_position().

TreeItem get_edited() const 🔗

Returns the currently edited item. Can be used with item_edited to get the item that was modified.

int get_edited_column() const 🔗

Returns the column for the currently edited item.

Rect2 get_item_area_rect(item: TreeItem, column: int = -1, button_index: int = -1) const 🔗

Returns the rectangle area for the specified TreeItem. If column is specified, only get the position and size of that column, otherwise get the rectangle containing all columns. If a button index is specified, the rectangle of that button will be returned.

TreeItem get_item_at_position(position: Vector2) const 🔗

Returns the tree item at the specified position (relative to the tree origin position).

TreeItem get_next_selected(from: TreeItem) 🔗

Returns the next selected TreeItem after the given one, or null if the end is reached.

If from is null, this returns the first selected item.

int get_pressed_button() const 🔗

Returns the last pressed button's index.

TreeItem get_root() const 🔗

Returns the tree's root item, or null if the tree is empty.

Vector2 get_scroll() const 🔗

Returns the current scrolling position.

TreeItem get_selected() const 🔗

Returns the currently focused item, or null if no item is focused.

In SELECT_ROW and SELECT_SINGLE modes, the focused item is same as the selected item. In SELECT_MULTI mode, the focused item is the item under the focus cursor, not necessarily selected.

To get the currently selected item(s), use get_next_selected().

int get_selected_column() const 🔗

Returns the currently focused column, or -1 if no column is focused.

In SELECT_SINGLE mode, the focused column is the selected column. In SELECT_ROW mode, the focused column is always 0 if any item is selected. In SELECT_MULTI mode, the focused column is the column under the focus cursor, and there are not necessarily any column selected.

To tell whether a column of an item is selected, use TreeItem.is_selected().

bool is_column_clipping_content(column: int) const 🔗

Returns true if the column has enabled clipping (see set_column_clip_content()).

bool is_column_expanding(column: int) const 🔗

Returns true if the column has enabled expanding (see set_column_expand()).

void scroll_to_item(item: TreeItem, center_on_item: bool = false) 🔗

Causes the Tree to jump to the specified TreeItem.

void set_column_clip_content(column: int, enable: bool) 🔗

Allows to enable clipping for column's content, making the content size ignored.

void set_column_custom_minimum_width(column: int, min_width: int) 🔗

Overrides the calculated minimum width of a column. It can be set to 0 to restore the default behavior. Columns that have the "Expand" flag will use their "min_width" in a similar fashion to Control.size_flags_stretch_ratio.

void set_column_expand(column: int, expand: bool) 🔗

If true, the column will have the "Expand" flag of Control. Columns that have the "Expand" flag will use their expand ratio in a similar fashion to Control.size_flags_stretch_ratio (see set_column_expand_ratio()).

void set_column_expand_ratio(column: int, ratio: int) 🔗

Sets the relative expand ratio for a column. See set_column_expand().

void set_column_title(column: int, title: String) 🔗

Sets the title of a column.

void set_column_title_alignment(column: int, title_alignment: HorizontalAlignment) 🔗

Sets the column title alignment. Note that @GlobalScope.HORIZONTAL_ALIGNMENT_FILL is not supported for column titles.

void set_column_title_direction(column: int, direction: TextDirection) 🔗

Sets column title base writing direction.

void set_column_title_language(column: int, language: String) 🔗

Sets language code of column title used for line-breaking and text shaping algorithms, if left empty current locale is used instead.

void set_selected(item: TreeItem, column: int) 🔗

Selects the specified TreeItem and column.

Color children_hl_line_color = Color(0.27, 0.27, 0.27, 1) 🔗

The Color of the relationship lines between the selected TreeItem and its children.

Color custom_button_font_highlight = Color(0.95, 0.95, 0.95, 1) 🔗

Text Color for a TreeItem.CELL_MODE_CUSTOM mode cell when it's hovered.

Color drop_position_color = Color(1, 1, 1, 1) 🔗

Color used to draw possible drop locations. See DropModeFlags constants for further description of drop locations.

Color font_color = Color(0.7, 0.7, 0.7, 1) 🔗

Default text Color of the item.

Color font_disabled_color = Color(0.875, 0.875, 0.875, 0.5) 🔗

Text Color for a TreeItem.CELL_MODE_CHECK mode cell when it's non-editable (see TreeItem.set_editable()).

Color font_hovered_color = Color(0.95, 0.95, 0.95, 1) 🔗

Text Color used when the item is hovered and not selected yet.

Color font_hovered_dimmed_color = Color(0.875, 0.875, 0.875, 1) 🔗

Text Color used when the item is hovered, while a button of the same item is hovered as the same time.

Color font_hovered_selected_color = Color(1, 1, 1, 1) 🔗

Text Color used when the item is hovered and selected.

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The tint of text outline of the item.

Color font_selected_color = Color(1, 1, 1, 1) 🔗

Text Color used when the item is selected.

Color guide_color = Color(0.7, 0.7, 0.7, 0.25) 🔗

Color of the guideline.

Color parent_hl_line_color = Color(0.27, 0.27, 0.27, 1) 🔗

The Color of the relationship lines between the selected TreeItem and its parents.

Color relationship_line_color = Color(0.27, 0.27, 0.27, 1) 🔗

The default Color of the relationship lines.

Color title_button_color = Color(0.875, 0.875, 0.875, 1) 🔗

Default text Color of the title button.

int button_margin = 4 🔗

The horizontal space between each button in a cell.

int children_hl_line_width = 1 🔗

The width of the relationship lines between the selected TreeItem and its children.

int draw_guides = 1 🔗

Draws the guidelines if not zero, this acts as a boolean. The guideline is a horizontal line drawn at the bottom of each item.

int draw_relationship_lines = 0 🔗

Draws the relationship lines if not zero, this acts as a boolean. Relationship lines are drawn at the start of child items to show hierarchy.

int h_separation = 4 🔗

The horizontal space between item cells. This is also used as the margin at the start of an item when folding is disabled.

int icon_max_width = 0 🔗

The maximum allowed width of the icon in item's cells. This limit is applied on top of the default size of the icon, but before the value set with TreeItem.set_icon_max_width(). The height is adjusted according to the icon's ratio.

int inner_item_margin_bottom = 0 🔗

The inner bottom margin of a cell.

int inner_item_margin_left = 0 🔗

The inner left margin of a cell.

int inner_item_margin_right = 0 🔗

The inner right margin of a cell.

int inner_item_margin_top = 0 🔗

The inner top margin of a cell.

int item_margin = 16 🔗

The horizontal margin at the start of an item. This is used when folding is enabled for the item.

int outline_size = 0 🔗

The size of the text outline.

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

int parent_hl_line_margin = 0 🔗

The space between the parent relationship lines for the selected TreeItem and the relationship lines to its siblings that are not selected.

int parent_hl_line_width = 1 🔗

The width of the relationship lines between the selected TreeItem and its parents.

int relationship_line_width = 1 🔗

The default width of the relationship lines.

int scroll_border = 4 🔗

The maximum distance between the mouse cursor and the control's border to trigger border scrolling when dragging.

int scroll_speed = 12 🔗

The speed of border scrolling.

int scrollbar_h_separation = 4 🔗

The horizontal separation of tree content and scrollbar.

int scrollbar_margin_bottom = -1 🔗

The bottom margin of the scrollbars. When negative, uses panel bottom margin.

int scrollbar_margin_left = -1 🔗

The left margin of the horizontal scrollbar. When negative, uses panel left margin.

int scrollbar_margin_right = -1 🔗

The right margin of the scrollbars. When negative, uses panel right margin.

int scrollbar_margin_top = -1 🔗

The top margin of the vertical scrollbar. When negative, uses panel top margin.

int scrollbar_v_separation = 4 🔗

The vertical separation of tree content and scrollbar.

int v_separation = 4 🔗

The vertical padding inside each item, i.e. the distance between the item's content and top/bottom border.

Font of the item's text.

Font title_button_font 🔗

Font of the title button's text.

Font size of the item's text.

int title_button_font_size 🔗

Font size of the title button's text.

The arrow icon used when a foldable item is not collapsed.

Texture2D arrow_collapsed 🔗

The arrow icon used when a foldable item is collapsed (for left-to-right layouts).

Texture2D arrow_collapsed_mirrored 🔗

The arrow icon used when a foldable item is collapsed (for right-to-left layouts).

The check icon to display when the TreeItem.CELL_MODE_CHECK mode cell is checked and editable (see TreeItem.set_editable()).

Texture2D checked_disabled 🔗

The check icon to display when the TreeItem.CELL_MODE_CHECK mode cell is checked and non-editable (see TreeItem.set_editable()).

Texture2D indeterminate 🔗

The check icon to display when the TreeItem.CELL_MODE_CHECK mode cell is indeterminate and editable (see TreeItem.set_editable()).

Texture2D indeterminate_disabled 🔗

The check icon to display when the TreeItem.CELL_MODE_CHECK mode cell is indeterminate and non-editable (see TreeItem.set_editable()).

Texture2D select_arrow 🔗

The arrow icon to display for the TreeItem.CELL_MODE_RANGE mode cell.

Texture2D unchecked 🔗

The check icon to display when the TreeItem.CELL_MODE_CHECK mode cell is unchecked and editable (see TreeItem.set_editable()).

Texture2D unchecked_disabled 🔗

The check icon to display when the TreeItem.CELL_MODE_CHECK mode cell is unchecked and non-editable (see TreeItem.set_editable()).

The updown arrow icon to display for the TreeItem.CELL_MODE_RANGE mode cell.

StyleBox button_hover 🔗

StyleBox used when a button in the tree is hovered.

StyleBox button_pressed 🔗

StyleBox used when a button in the tree is pressed.

StyleBox used for the cursor, when the Tree is being focused.

StyleBox cursor_unfocused 🔗

StyleBox used for the cursor, when the Tree is not being focused.

StyleBox custom_button 🔗

Default StyleBox for a TreeItem.CELL_MODE_CUSTOM mode cell when button is enabled with TreeItem.set_custom_as_button().

StyleBox custom_button_hover 🔗

StyleBox for a TreeItem.CELL_MODE_CUSTOM mode button cell when it's hovered.

StyleBox custom_button_pressed 🔗

StyleBox for a TreeItem.CELL_MODE_CUSTOM mode button cell when it's pressed.

The focused style for the Tree, drawn on top of everything.

StyleBox for the item being hovered, but not selected.

StyleBox hovered_dimmed 🔗

StyleBox for the item being hovered, while a button of the same item is hovered as the same time.

StyleBox hovered_selected 🔗

StyleBox for the hovered and selected items, used when the Tree is not being focused.

StyleBox hovered_selected_focus 🔗

StyleBox for the hovered and selected items, used when the Tree is being focused.

The background style for the Tree.

StyleBox for the selected items, used when the Tree is not being focused.

StyleBox selected_focus 🔗

StyleBox for the selected items, used when the Tree is being focused.

StyleBox title_button_hover 🔗

StyleBox used when the title button is being hovered.

StyleBox title_button_normal 🔗

Default StyleBox for the title button.

StyleBox title_button_pressed 🔗

StyleBox used when the title button is being pressed.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    var tree = Tree.new()
    var root = tree.create_item()
    tree.hide_root = true
    var child1 = tree.create_item(root)
    var child2 = tree.create_item(root)
    var subchild1 = tree.create_item(child1)
    subchild1.set_text(0, "Subchild1")
```

Example 2 (gdscript):
```gdscript
public override void _Ready()
{
    var tree = new Tree();
    TreeItem root = tree.CreateItem();
    tree.HideRoot = true;
    TreeItem child1 = tree.CreateItem(root);
    TreeItem child2 = tree.CreateItem(root);
    TreeItem subchild1 = tree.CreateItem(child1);
    subchild1.SetText(0, "Subchild1");
}
```

Example 3 (gdscript):
```gdscript
func _ready():
    $Tree.item_edited.connect(on_Tree_item_edited)

func on_Tree_item_edited():
    print($Tree.get_edited()) # This item just got edited (e.g. checked).
```

Example 4 (gdscript):
```gdscript
public override void _Ready()
{
    GetNode<Tree>("Tree").ItemEdited += OnTreeItemEdited;
}

public void OnTreeItemEdited()
{
    GD.Print(GetNode<Tree>("Tree").GetEdited()); // This item just got edited (e.g. checked).
}
```

---

## Using Containers

**URL:** https://docs.godotengine.org/en/stable/tutorials/ui/gui_containers.html

**Contents:**
- Using Containers
- Container layout
- Sizing options
- Container types
  - Box Containers
  - Grid Container
  - Margin Container
  - Tab Container
  - Split Container
  - PanelContainer

Anchors are an efficient way to handle different aspect ratios for basic multiple resolution handling in GUIs.

For more complex user interfaces, they can become difficult to use.

This is often the case of games, such as RPGs, online chats, tycoons or simulations. Another common case where more advanced layout features may be required is in-game tools (or simply just tools).

All these situations require a more capable OS-like user interface, with advanced layout and formatting. For that, Containers are more useful.

Containers provide a huge amount of layout power (as an example, the Godot editor user interface is entirely done using them):

When a Container-derived node is used, all children Control nodes give up their own positioning ability. This means the Container will control their positioning and any attempt to manually alter these nodes will be either ignored or invalidated the next time their parent is resized.

Likewise, when a Container derived node is resized, all its children will be re-positioned according to it, with a behavior based on the type of container used:

Example of HBoxContainer resizing children buttons.

The real strength of containers is that they can be nested (as nodes), allowing the creation of very complex layouts that resize effortlessly.

When adding a node to a container, the way the container treats each child depends mainly on their container sizing options. These options can be found by inspecting the layout of any Control that is a child of a Container.

Sizing options are independent for vertical and horizontal sizing and not all containers make use of them (but most do):

Fill: Ensures the control fills the designated area within the container. No matter if a control expands or not (see below), it will only fill the designated area when this is toggled on (it is by default).

Expand: Attempts to use as much space as possible in the parent container (in each axis). Controls that don't expand will be pushed away by those that do. Between expanding controls, the amount of space they take from each other is determined by the Stretch Ratio (see below). This option is only available when the parent Container is of the right type, for example the HBoxContainer has this option for horizontal sizing.

Shrink Begin When expanding, try to remain at the left or top of the expanded area.

Shrink Center When expanding, try to remain at the center of the expanded area.

Shrink End When expanding, try to remain at the right or bottom of the expanded area.

Stretch Ratio: The ratio of how much expanded controls take up the available space in relation to each other. A control with "2", will take up twice as much available space as one with "1".

Experimenting with these flags and different containers is recommended to get a better grasp on how they work.

Godot provides several container types out of the box as they serve different purposes:

Arranges child controls vertically or horizontally (via HBoxContainer and VBoxContainer). In the opposite of the designated direction (as in, vertical for a horizontal container), it just expands the children.

These containers make use of the Stretch Ratio property for children with the Expand flag set.

Arranges child controls in a grid layout (via GridContainer, amount of columns must be specified). Uses both the vertical and horizontal expand flags.

Child controls are expanded towards the bounds of this control (via MarginContainer). Padding will be added on the margins depending on the theme configuration.

Again, keep in mind that the margins are a Theme value, so they need to be edited from the constants overrides section of each control:

Allows you to place several child controls stacked on top of each other (via TabContainer), with only the current one visible.

Changing the current one is done via tabs located at the top of the container, via clicking:

The titles are generated from the node names by default (although they can be overridden via TabContainer API).

Settings such as tab placement and StyleBox can be modified in the TabContainer theme overrides.

Accepts only one or two children controls, then places them side to side with a divisor (via HSplitContainer and VSplitContainer). Respects both horizontal and vertical flags, as well as Ratio.

The divisor can be dragged around to change the size relation between both children:

A container that draws a StyleBox, then expands children to cover its whole area (via PanelContainer, respecting the StyleBox margins). It respects both the horizontal and vertical sizing options.

This container is useful as a top-level control, or just to add custom backgrounds to sections of a layout.

A container that can be expanded/collapsed (via FoldableContainer). Child controls are hidden when it is collapsed.

Accepts a single child node. If the child node is bigger than the container, scrollbars will be added to allow panning the node around (via ScrollContainer). Both vertical and horizontal size options are respected, and the behavior can be turned on or off per axis in the properties.

Mouse wheel and touch drag (when touch is available) are also valid ways to pan the child control around.

As in the example above, one of the most common ways to use this container is together with a VBoxContainer as child.

A container type that arranges its child controls in a way that preserves their proportions automatically when the container is resized. (via AspectRatioContainer). It has multiple stretch modes, providing options for adjusting the child controls' sizes concerning the container: "fill," "width control height," "height control width," and "cover."

It is useful when you have a container that needs to be dynamic and responsive to different screen sizes, and you want the child elements to scale proportionally without losing their intended shapes.

FlowContainer is a container that arranges its child controls either horizontally or vertically (via HFlowContainer and via VFlowContainer). When the available space runs out, it wraps the children to the next line or column, similar to how text wraps in a book.

It is useful for creating flexible layouts where the child controls adjust automatically to the available space without overlapping.

CenterContainer is a container that automatically keeps all of its child controls centered within it at their minimum size. It ensures that the child controls are always aligned to the center, making it easier to create centered layouts without manual positioning (via CenterContainer).

This is a special control that will only accept a single Viewport node as child, and it will display it as if it was an image (via SubViewportContainer).

It is possible to create a custom container using a script. Here is an example of a container that fits children to its size:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Container

func _notification(what):
    if what == NOTIFICATION_SORT_CHILDREN:
        # Must re-sort the children
        for c in get_children():
            # Fit to own size
            fit_child_in_rect(c, Rect2(Vector2(), size))

func set_some_setting():
    # Some setting changed, ask for children re-sort.
    queue_sort()
```

Example 2 (swift):
```swift
using Godot;

public partial class CustomContainer : Container
{
    public override void _Notification(int what)
    {
        if (what == NotificationSortChildren)
        {
            // Must re-sort the children
            foreach (Control c in GetChildren())
            {
                // Fit to own size
                FitChildInRect(c, new Rect2(new Vector2(), Size));
            }
        }
    }

    public void SetSomeSetting()
    {
        // Some setting changed, ask for children re-sort.
        QueueSort();
    }
}
```

---

## Version control systems

**URL:** https://docs.godotengine.org/en/stable/tutorials/best_practices/version_control_systems.html

**Contents:**
- Version control systems
- Introduction
- Version control plugins
  - Official Git plugin
- Files to exclude from VCS
- Working with Git on Windows
- Git LFS
- User-contributed notes

Godot aims to be VCS-friendly and generate mostly readable and mergeable files.

Godot also supports the use of version control systems in the editor itself. However, version control in the editor requires a plugin for the specific VCS you're using.

As of July 2023, there is only a Git plugin available, but the community may create additional VCS plugins.

Using Git from inside the editor is supported with an official plugin. You can find the latest releases on GitHub.

Documentation on how to use the Git plugin can be found on its wiki.

This lists files and folders that should be ignored from version control in Godot 4.1 and later.

The list of files of folders that should be ignored from version control in Godot 3.x and Godot 4.0 is entirely different. This is important, as Godot 3.x and 4.0 may store sensitive credentials in export_presets.cfg (unlike Godot 4.1 and later).

If you are using Godot 3, check the 3.5 version of this documentation page instead.

There are some files and folders Godot automatically creates when opening a project in the editor for the first time. To avoid bloating your version control repository with generated data, you should add them to your VCS ignore:

.godot/: This folder stores various project cache data.

*.translation: These files are binary imported translations generated from CSV files.

You can make the Godot project manager generate version control metadata for you automatically when creating a project. When choosing the Git option, this creates .gitignore and .gitattributes files in the project root:

Creating version control metadata in the project manager's New Project dialog

In existing projects, select the Project menu at the top of the editor, then choose Version Control > Generate Version Control Metadata. This creates the same files as if the operation was performed in the project manager.

Most Git for Windows clients are configured with the core.autocrlf set to true. This can lead to files unnecessarily being marked as modified by Git due to their line endings being converted from LF to CRLF automatically.

It is better to set this option as:

Creating version control metadata using the project manager or editor will automatically enforce LF line endings using the .gitattributes file. In this case, you don't need to change your Git configuration.

Git LFS (Large File Storage) is a Git extension that allows you to manage large files in your repository. It replaces large files with text pointers inside Git, while storing the file contents on a remote server. This is useful for managing large assets, such as textures, audio files, and 3D models, without bloating your Git repository.

When using Git LFS you will want to ensure it is setup before you commit any files to your repository. If you have already committed files to your repository, you will need to remove them from the repository and re-add them after setting up Git LFS.

It is possible to use git lfs migrate to convert existing files in your repository, but this is more in-depth and requires a good understanding of Git.

A common approach is setting up a new repository with Git LFS (and a proper .gitattributes), then copying the files from the old repository to the new one. This way, you can ensure that all files are tracked by LFS from the start.

To use Git LFS with Godot, you need to install the Git LFS extension and configure it to track the file types you want to manage. You can do this by running the following command in your terminal:

This will create a .gitattributes file in your repository that tells Git to use LFS for the specified file types. You can add more file types by modifying the .gitattributes file. For example, to track all GLB files, you can do this by running the following command in your terminal:

When you add or modify files that are tracked by LFS, Git will automatically store them in LFS instead of the regular Git history. You can push and pull LFS files just like regular Git files, but keep in mind that LFS files are stored separately from the rest of your Git history. This means that you may need to install Git LFS on any machine that you clone the repository to in order to access the LFS files.

Below is an example .gitattributes file that you can use as a starting point for Git LFS. These file types were chosen because they are commonly used, but you can modify the list to include any binary types you may have in your project.

For more information on Git LFS, check the official documentation: https://git-lfs.github.com/ and https://docs.github.com/en/repositories/working-with-files/managing-large-files.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
git config --global core.autocrlf input
```

Example 2 (unknown):
```unknown
git lfs install
```

Example 3 (unknown):
```unknown
git lfs track "*.glb"
```

Example 4 (markdown):
```markdown
# Normalize EOL for all files that Git considers text files.
* text=auto eol=lf

# Git LFS Tracking (Assets)

# 3D Models
*.fbx filter=lfs diff=lfs merge=lfs -text
*.gltf filter=lfs diff=lfs merge=lfs -text
*.glb filter=lfs diff=lfs merge=lfs -text
*.blend filter=lfs diff=lfs merge=lfs -text
*.obj filter=lfs diff=lfs merge=lfs -text

# Images
*.png filter=lfs diff=lfs merge=lfs -text
*.svg filter=lfs diff=lfs merge=lfs -text
*.jpg filter=lfs diff=lfs merge=lfs -text
*.jpeg filter=lfs diff=lfs merge=lfs -text
*.gif filter=lfs diff=lfs merge=lfs -text
*.tga filter=lfs diff=lfs merge=lfs -text
*.webp filter=lfs diff=lfs merge=lfs -text
*.exr filter=lfs diff=lfs merge=lfs -text
*.hdr filter=lfs diff=lfs merge=lfs -text
*.dds filter=lfs diff=lfs merge=lfs -text

# Audio
*.mp3 filter=lfs diff=lfs merge=lfs -text
*.wav filter=lfs diff=lfs merge=lfs -text
*.ogg filter=lfs diff=lfs merge=lfs -text

# Font & Icon
*.ttf filter=lfs diff=lfs merge=lfs -text
*.otf filter=lfs diff=lfs merge=lfs -text
*.ico filter=lfs diff=lfs merge=lfs -text

# Godot LFS Specific
*.scn filter=lfs diff=lfs merge=lfs -text
*.res filter=lfs diff=lfs merge=lfs -text
*.material filter=lfs diff=lfs merge=lfs -text
*.anim filter=lfs diff=lfs merge=lfs -text
*.mesh filter=lfs diff=lfs merge=lfs -text
*.lmbake filter=lfs diff=lfs merge=lfs -text
```

---

## VFlowContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_vflowcontainer.html

**Contents:**
- VFlowContainer
- Description
- Tutorials
- User-contributed notes

Inherits: FlowContainer < Container < Control < CanvasItem < Node < Object

A container that arranges its child controls vertically and wraps them around at the borders.

A variant of FlowContainer that can only arrange its child controls vertically, wrapping them around at the borders. This is similar to how text in a book wraps around when no more words can fit on a line, except vertically.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeUIntConstant

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeuintconstant.html

**Contents:**
- VisualShaderNodeUIntConstant
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeConstant < VisualShaderNode < Resource < RefCounted < Object

An unsigned scalar integer constant to be used within the visual shader graph.

Translated to uint in the shader language.

void set_constant(value: int)

An unsigned integer constant which represents a state of this node.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeUIntFunc

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeuintfunc.html

**Contents:**
- VisualShaderNodeUIntFunc
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

An unsigned scalar integer function to be used within the visual shader graph.

Accept an unsigned integer scalar (x) to the input port and transform it according to function.

Function FUNC_NEGATE = 0

Negates the x using -(x).

Function FUNC_BITWISE_NOT = 1

Returns the result of bitwise NOT operation on the integer. Translates to ~a in the Godot Shader Language.

Function FUNC_MAX = 2

Represents the size of the Function enum.

Function function = 0 🔗

void set_function(value: Function)

Function get_function()

A function to be applied to the scalar.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeUIntOp

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeuintop.html

**Contents:**
- VisualShaderNodeUIntOp
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNode < Resource < RefCounted < Object

An unsigned integer scalar operator to be used within the visual shader graph.

Applies operator to two unsigned integer inputs: a and b.

Sums two numbers using a + b.

Subtracts two numbers using a - b.

Multiplies two numbers using a * b.

Divides two numbers using a / b.

Calculates the remainder of two numbers using a % b.

Returns the greater of two numbers. Translates to max(a, b) in the Godot Shader Language.

Returns the lesser of two numbers. Translates to max(a, b) in the Godot Shader Language.

Operator OP_BITWISE_AND = 7

Returns the result of bitwise AND operation on the integer. Translates to a & b in the Godot Shader Language.

Operator OP_BITWISE_OR = 8

Returns the result of bitwise OR operation for two integers. Translates to a | b in the Godot Shader Language.

Operator OP_BITWISE_XOR = 9

Returns the result of bitwise XOR operation for two integers. Translates to a ^ b in the Godot Shader Language.

Operator OP_BITWISE_LEFT_SHIFT = 10

Returns the result of bitwise left shift operation on the integer. Translates to a << b in the Godot Shader Language.

Operator OP_BITWISE_RIGHT_SHIFT = 11

Returns the result of bitwise right shift operation on the integer. Translates to a >> b in the Godot Shader Language.

Operator OP_ENUM_SIZE = 12

Represents the size of the Operator enum.

Operator operator = 0 🔗

void set_operator(value: Operator)

Operator get_operator()

An operator to be applied to the inputs.

Please read the User-contributed notes policy before submitting a comment.

---

## VisualShaderNodeUIntParameter

**URL:** https://docs.godotengine.org/en/stable/classes/class_visualshadernodeuintparameter.html

**Contents:**
- VisualShaderNodeUIntParameter
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: VisualShaderNodeParameter < VisualShaderNode < Resource < RefCounted < Object

A visual shader node for shader parameter (uniform) of type unsigned int.

A VisualShaderNodeParameter of type unsigned int. Offers additional customization for range of accepted values.

default_value_enabled

int default_value = 0 🔗

void set_default_value(value: int)

int get_default_value()

Default value of this parameter, which will be used if not set externally. default_value_enabled must be enabled; defaults to 0 otherwise.

bool default_value_enabled = false 🔗

void set_default_value_enabled(value: bool)

bool is_default_value_enabled()

If true, the node will have a custom default value.

Please read the User-contributed notes policy before submitting a comment.

---

## VSeparator

**URL:** https://docs.godotengine.org/en/stable/classes/class_vseparator.html

**Contents:**
- VSeparator
- Description
- User-contributed notes

Inherits: Separator < Control < CanvasItem < Node < Object

A vertical line used for separating other controls.

A vertical separator used for separating other controls that are arranged horizontally. VSeparator is purely visual and normally drawn as a StyleBoxLine.

Please read the User-contributed notes policy before submitting a comment.

---

## VSplitContainer

**URL:** https://docs.godotengine.org/en/stable/classes/class_vsplitcontainer.html

**Contents:**
- VSplitContainer
- Description
- Tutorials
- User-contributed notes

Inherits: SplitContainer < Container < Control < CanvasItem < Node < Object

A container that splits two child controls vertically and provides a grabber for adjusting the split ratio.

A container that accepts only two child controls, then arranges them vertically and creates a divisor between them. The divisor can be dragged around to change the size relation between the child controls.

Please read the User-contributed notes policy before submitting a comment.

---

## WebRTCDataChannelExtension

**URL:** https://docs.godotengine.org/en/stable/classes/class_webrtcdatachannelextension.html

**Contents:**
- WebRTCDataChannelExtension
- Methods
- Method Descriptions
- User-contributed notes

Inherits: WebRTCDataChannel < PacketPeer < RefCounted < Object

There is currently no description for this class. Please help us by contributing one!

_close() virtual required

_get_available_packet_count() virtual required const

_get_buffered_amount() virtual required const

_get_id() virtual required const

_get_label() virtual required const

_get_max_packet_life_time() virtual required const

_get_max_packet_size() virtual required const

_get_max_retransmits() virtual required const

_get_packet(r_buffer: const uint8_t **, r_buffer_size: int32_t*) virtual

_get_protocol() virtual required const

_get_ready_state() virtual required const

_get_write_mode() virtual required const

_is_negotiated() virtual required const

_is_ordered() virtual required const

_poll() virtual required

_put_packet(p_buffer: const uint8_t*, p_buffer_size: int) virtual

_set_write_mode(p_write_mode: WriteMode) virtual required

_was_string_packet() virtual required const

void _close() virtual required 🔗

There is currently no description for this method. Please help us by contributing one!

int _get_available_packet_count() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

int _get_buffered_amount() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

int _get_id() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

String _get_label() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

int _get_max_packet_life_time() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

int _get_max_packet_size() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

int _get_max_retransmits() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

Error _get_packet(r_buffer: const uint8_t **, r_buffer_size: int32_t*) virtual 🔗

There is currently no description for this method. Please help us by contributing one!

String _get_protocol() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

ChannelState _get_ready_state() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

WriteMode _get_write_mode() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

bool _is_negotiated() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

bool _is_ordered() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

Error _poll() virtual required 🔗

There is currently no description for this method. Please help us by contributing one!

Error _put_packet(p_buffer: const uint8_t*, p_buffer_size: int) virtual 🔗

There is currently no description for this method. Please help us by contributing one!

void _set_write_mode(p_write_mode: WriteMode) virtual required 🔗

There is currently no description for this method. Please help us by contributing one!

bool _was_string_packet() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

Please read the User-contributed notes policy before submitting a comment.

---

## WebRTCPeerConnectionExtension

**URL:** https://docs.godotengine.org/en/stable/classes/class_webrtcpeerconnectionextension.html

**Contents:**
- WebRTCPeerConnectionExtension
- Methods
- Method Descriptions
- User-contributed notes

Inherits: WebRTCPeerConnection < RefCounted < Object

There is currently no description for this class. Please help us by contributing one!

_add_ice_candidate(p_sdp_mid_name: String, p_sdp_mline_index: int, p_sdp_name: String) virtual required

_close() virtual required

_create_data_channel(p_label: String, p_config: Dictionary) virtual required

_create_offer() virtual required

_get_connection_state() virtual required const

_get_gathering_state() virtual required const

_get_signaling_state() virtual required const

_initialize(p_config: Dictionary) virtual required

_poll() virtual required

_set_local_description(p_type: String, p_sdp: String) virtual required

_set_remote_description(p_type: String, p_sdp: String) virtual required

Error _add_ice_candidate(p_sdp_mid_name: String, p_sdp_mline_index: int, p_sdp_name: String) virtual required 🔗

There is currently no description for this method. Please help us by contributing one!

void _close() virtual required 🔗

There is currently no description for this method. Please help us by contributing one!

WebRTCDataChannel _create_data_channel(p_label: String, p_config: Dictionary) virtual required 🔗

There is currently no description for this method. Please help us by contributing one!

Error _create_offer() virtual required 🔗

There is currently no description for this method. Please help us by contributing one!

ConnectionState _get_connection_state() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

GatheringState _get_gathering_state() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

SignalingState _get_signaling_state() virtual required const 🔗

There is currently no description for this method. Please help us by contributing one!

Error _initialize(p_config: Dictionary) virtual required 🔗

There is currently no description for this method. Please help us by contributing one!

Error _poll() virtual required 🔗

There is currently no description for this method. Please help us by contributing one!

Error _set_local_description(p_type: String, p_sdp: String) virtual required 🔗

There is currently no description for this method. Please help us by contributing one!

Error _set_remote_description(p_type: String, p_sdp: String) virtual required 🔗

There is currently no description for this method. Please help us by contributing one!

Please read the User-contributed notes policy before submitting a comment.

---

## Window

**URL:** https://docs.godotengine.org/en/stable/classes/class_window.html

**Contents:**
- Window
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Constants
- Property Descriptions
- Method Descriptions

Inherits: Viewport < Node < Object

Inherited By: AcceptDialog, Popup

Base class for all windows, dialogs, and popups.

A node that creates a window. The window can either be a native system window or embedded inside another Window (see Viewport.gui_embed_subwindows).

At runtime, Windows will not close automatically when requested. You need to handle it manually using the close_requested signal (this applies both to pressing the close button and clicking outside of a popup).

accessibility_description

content_scale_stretch

WindowInitialPosition

mouse_passthrough_polygon

_get_contents_minimum_size() virtual const

add_theme_color_override(name: StringName, color: Color)

add_theme_constant_override(name: StringName, constant: int)

add_theme_font_override(name: StringName, font: Font)

add_theme_font_size_override(name: StringName, font_size: int)

add_theme_icon_override(name: StringName, texture: Texture2D)

add_theme_stylebox_override(name: StringName, stylebox: StyleBox)

begin_bulk_theme_override()

child_controls_changed()

end_bulk_theme_override()

get_contents_minimum_size() const

get_flag(flag: Flags) const

get_focused_window() static

get_layout_direction() const

get_position_with_decorations() const

get_size_with_decorations() const

get_theme_color(name: StringName, theme_type: StringName = &"") const

get_theme_constant(name: StringName, theme_type: StringName = &"") const

get_theme_default_base_scale() const

get_theme_default_font() const

get_theme_default_font_size() const

get_theme_font(name: StringName, theme_type: StringName = &"") const

get_theme_font_size(name: StringName, theme_type: StringName = &"") const

get_theme_icon(name: StringName, theme_type: StringName = &"") const

get_theme_stylebox(name: StringName, theme_type: StringName = &"") const

get_window_id() const

has_theme_color(name: StringName, theme_type: StringName = &"") const

has_theme_color_override(name: StringName) const

has_theme_constant(name: StringName, theme_type: StringName = &"") const

has_theme_constant_override(name: StringName) const

has_theme_font(name: StringName, theme_type: StringName = &"") const

has_theme_font_override(name: StringName) const

has_theme_font_size(name: StringName, theme_type: StringName = &"") const

has_theme_font_size_override(name: StringName) const

has_theme_icon(name: StringName, theme_type: StringName = &"") const

has_theme_icon_override(name: StringName) const

has_theme_stylebox(name: StringName, theme_type: StringName = &"") const

has_theme_stylebox_override(name: StringName) const

is_layout_rtl() const

is_maximize_allowed() const

is_using_font_oversampling() const

popup(rect: Rect2i = Rect2i(0, 0, 0, 0))

popup_centered(minsize: Vector2i = Vector2i(0, 0))

popup_centered_clamped(minsize: Vector2i = Vector2i(0, 0), fallback_ratio: float = 0.75)

popup_centered_ratio(ratio: float = 0.8)

popup_exclusive(from_node: Node, rect: Rect2i = Rect2i(0, 0, 0, 0))

popup_exclusive_centered(from_node: Node, minsize: Vector2i = Vector2i(0, 0))

popup_exclusive_centered_clamped(from_node: Node, minsize: Vector2i = Vector2i(0, 0), fallback_ratio: float = 0.75)

popup_exclusive_centered_ratio(from_node: Node, ratio: float = 0.8)

popup_exclusive_on_parent(from_node: Node, parent_rect: Rect2i)

popup_on_parent(parent_rect: Rect2i)

remove_theme_color_override(name: StringName)

remove_theme_constant_override(name: StringName)

remove_theme_font_override(name: StringName)

remove_theme_font_size_override(name: StringName)

remove_theme_icon_override(name: StringName)

remove_theme_stylebox_override(name: StringName)

set_flag(flag: Flags, enabled: bool)

set_ime_active(active: bool)

set_ime_position(position: Vector2i)

set_layout_direction(direction: LayoutDirection)

set_unparent_when_invisible(unparent: bool)

set_use_font_oversampling(enable: bool)

start_resize(edge: WindowResizeEdge)

Color(0.875, 0.875, 0.875, 1)

title_outline_modulate

embedded_unfocused_border

Emitted right after popup() call, before the Window appears or does anything.

Emitted when the Window's close button is pressed or when popup_window is enabled and user clicks outside the window.

This signal can be used to handle window closing, e.g. by connecting it to hide().

Emitted when the Window's DPI changes as a result of OS-level changes (e.g. moving the window from a Retina display to a lower resolution one).

Note: Only implemented on macOS and Linux (Wayland).

files_dropped(files: PackedStringArray) 🔗

Emitted when files are dragged from the OS file manager and dropped in the game window. The argument is a list of file paths.

Note: This signal only works with native windows, i.e. the main window and Window-derived nodes when Viewport.gui_embed_subwindows is disabled in the main viewport.

Emitted when the Window gains focus.

Emitted when the Window loses its focus.

go_back_requested() 🔗

Emitted when a go back request is sent (e.g. pressing the "Back" button on Android), right after Node.NOTIFICATION_WM_GO_BACK_REQUEST.

Emitted when the mouse cursor enters the Window's visible area, that is not occluded behind other Controls or windows, provided its Viewport.gui_disable_input is false and regardless if it's currently focused or not.

Emitted when the mouse cursor leaves the Window's visible area, that is not occluded behind other Controls or windows, provided its Viewport.gui_disable_input is false and regardless if it's currently focused or not.

Emitted when the NOTIFICATION_THEME_CHANGED notification is sent.

Emitted when window title bar text is changed.

Emitted when window title bar decorations are changed, e.g. macOS window enter/exit full screen mode, or extend-to-title flag is changed.

visibility_changed() 🔗

Emitted when Window is made visible or disappears.

window_input(event: InputEvent) 🔗

Emitted when the Window is currently focused and receives any input, passing the received event as an argument. The event's position, if present, is in the embedder's coordinate system.

Mode MODE_WINDOWED = 0

Windowed mode, i.e. Window doesn't occupy the whole screen (unless set to the size of the screen).

Mode MODE_MINIMIZED = 1

Minimized window mode, i.e. Window is not visible and available on window manager's window list. Normally happens when the minimize button is pressed.

Mode MODE_MAXIMIZED = 2

Maximized window mode, i.e. Window will occupy whole screen area except task bar and still display its borders. Normally happens when the maximize button is pressed.

Mode MODE_FULLSCREEN = 3

Full screen mode with full multi-window support.

Full screen window covers the entire display area of a screen and has no decorations. The display's video mode is not changed.

On Android: This enables immersive mode.

On macOS: A new desktop is used to display the running project.

Note: Regardless of the platform, enabling full screen will change the window size to match the monitor's size. Therefore, make sure your project supports multiple resolutions when enabling full screen mode.

Mode MODE_EXCLUSIVE_FULLSCREEN = 4

A single window full screen mode. This mode has less overhead, but only one window can be open on a given screen at a time (opening a child window or application switching will trigger a full screen transition).

Full screen window covers the entire display area of a screen and has no border or decorations. The display's video mode is not changed.

Note: This mode might not work with screen recording software.

On Android: This enables immersive mode.

On Windows: Depending on video driver, full screen transition might cause screens to go black for a moment.

On macOS: A new desktop is used to display the running project. Exclusive full screen mode prevents Dock and Menu from showing up when the mouse pointer is hovering the edge of the screen.

On Linux (X11): Exclusive full screen mode bypasses compositor.

On Linux (Wayland): Equivalent to MODE_FULLSCREEN.

Note: Regardless of the platform, enabling full screen will change the window size to match the monitor's size. Therefore, make sure your project supports multiple resolutions when enabling full screen mode.

Flags FLAG_RESIZE_DISABLED = 0

The window can't be resized by dragging its resize grip. It's still possible to resize the window using size. This flag is ignored for full screen windows. Set with unresizable.

Flags FLAG_BORDERLESS = 1

The window do not have native title bar and other decorations. This flag is ignored for full-screen windows. Set with borderless.

Flags FLAG_ALWAYS_ON_TOP = 2

The window is floating on top of all other windows. This flag is ignored for full-screen windows. Set with always_on_top.

Flags FLAG_TRANSPARENT = 3

The window background can be transparent. Set with transparent.

Note: This flag has no effect if either ProjectSettings.display/window/per_pixel_transparency/allowed, or the window's Viewport.transparent_bg is set to false.

Flags FLAG_NO_FOCUS = 4

The window can't be focused. No-focus window will ignore all input, except mouse clicks. Set with unfocusable.

Window is part of menu or OptionButton dropdown. This flag can't be changed when the window is visible. An active popup window will exclusively receive all input, without stealing focus from its parent. Popup windows are automatically closed when uses click outside it, or when an application is switched. Popup window must have transient parent set (see transient).

Note: This flag has no effect in embedded windows (unless said window is a Popup).

Flags FLAG_EXTEND_TO_TITLE = 6

Window content is expanded to the full size of the window. Unlike borderless window, the frame is left intact and can be used to resize the window, title bar is transparent, but have minimize/maximize/close buttons. Set with extend_to_title.

Note: This flag is implemented only on macOS.

Note: This flag has no effect in embedded windows.

Flags FLAG_MOUSE_PASSTHROUGH = 7

All mouse events are passed to the underlying window of the same application.

Note: This flag has no effect in embedded windows.

Flags FLAG_SHARP_CORNERS = 8

Window style is overridden, forcing sharp corners.

Note: This flag has no effect in embedded windows.

Note: This flag is implemented only on Windows (11).

Flags FLAG_EXCLUDE_FROM_CAPTURE = 9

Windows is excluded from screenshots taken by DisplayServer.screen_get_image(), DisplayServer.screen_get_image_rect(), and DisplayServer.screen_get_pixel().

Note: This flag has no effect in embedded windows.

Note: This flag is implemented on macOS and Windows (10, 20H1).

Note: Setting this flag will prevent standard screenshot methods from capturing a window image, but does NOT guarantee that other apps won't be able to capture an image. It should not be used as a DRM or security measure.

Flags FLAG_POPUP_WM_HINT = 10

Signals the window manager that this window is supposed to be an implementation-defined "popup" (usually a floating, borderless, untileable and immovable child window).

Flags FLAG_MINIMIZE_DISABLED = 11

Window minimize button is disabled.

Note: This flag is implemented on macOS and Windows.

Flags FLAG_MAXIMIZE_DISABLED = 12

Window maximize button is disabled.

Note: This flag is implemented on macOS and Windows.

Max value of the Flags.

enum ContentScaleMode: 🔗

ContentScaleMode CONTENT_SCALE_MODE_DISABLED = 0

The content will not be scaled to match the Window's size.

ContentScaleMode CONTENT_SCALE_MODE_CANVAS_ITEMS = 1

The content will be rendered at the target size. This is more performance-expensive than CONTENT_SCALE_MODE_VIEWPORT, but provides better results.

ContentScaleMode CONTENT_SCALE_MODE_VIEWPORT = 2

The content will be rendered at the base size and then scaled to the target size. More performant than CONTENT_SCALE_MODE_CANVAS_ITEMS, but results in pixelated image.

enum ContentScaleAspect: 🔗

ContentScaleAspect CONTENT_SCALE_ASPECT_IGNORE = 0

The aspect will be ignored. Scaling will simply stretch the content to fit the target size.

ContentScaleAspect CONTENT_SCALE_ASPECT_KEEP = 1

The content's aspect will be preserved. If the target size has different aspect from the base one, the image will be centered and black bars will appear on left and right sides.

ContentScaleAspect CONTENT_SCALE_ASPECT_KEEP_WIDTH = 2

The content can be expanded vertically. Scaling horizontally will result in keeping the width ratio and then black bars on left and right sides.

ContentScaleAspect CONTENT_SCALE_ASPECT_KEEP_HEIGHT = 3

The content can be expanded horizontally. Scaling vertically will result in keeping the height ratio and then black bars on top and bottom sides.

ContentScaleAspect CONTENT_SCALE_ASPECT_EXPAND = 4

The content's aspect will be preserved. If the target size has different aspect from the base one, the content will stay in the top-left corner and add an extra visible area in the stretched space.

enum ContentScaleStretch: 🔗

ContentScaleStretch CONTENT_SCALE_STRETCH_FRACTIONAL = 0

The content will be stretched according to a fractional factor. This fills all the space available in the window, but allows "pixel wobble" to occur due to uneven pixel scaling.

ContentScaleStretch CONTENT_SCALE_STRETCH_INTEGER = 1

The content will be stretched only according to an integer factor, preserving sharp pixels. This may leave a black background visible on the window's edges depending on the window size.

enum LayoutDirection: 🔗

LayoutDirection LAYOUT_DIRECTION_INHERITED = 0

Automatic layout direction, determined from the parent window layout direction.

LayoutDirection LAYOUT_DIRECTION_APPLICATION_LOCALE = 1

Automatic layout direction, determined from the current locale.

LayoutDirection LAYOUT_DIRECTION_LTR = 2

Left-to-right layout direction.

LayoutDirection LAYOUT_DIRECTION_RTL = 3

Right-to-left layout direction.

LayoutDirection LAYOUT_DIRECTION_SYSTEM_LOCALE = 4

Automatic layout direction, determined from the system locale.

LayoutDirection LAYOUT_DIRECTION_MAX = 5

Represents the size of the LayoutDirection enum.

LayoutDirection LAYOUT_DIRECTION_LOCALE = 1

Deprecated: Use LAYOUT_DIRECTION_APPLICATION_LOCALE instead.

enum WindowInitialPosition: 🔗

WindowInitialPosition WINDOW_INITIAL_POSITION_ABSOLUTE = 0

Initial window position is determined by position.

WindowInitialPosition WINDOW_INITIAL_POSITION_CENTER_PRIMARY_SCREEN = 1

Initial window position is the center of the primary screen.

WindowInitialPosition WINDOW_INITIAL_POSITION_CENTER_MAIN_WINDOW_SCREEN = 2

Initial window position is the center of the main window screen.

WindowInitialPosition WINDOW_INITIAL_POSITION_CENTER_OTHER_SCREEN = 3

Initial window position is the center of current_screen screen.

WindowInitialPosition WINDOW_INITIAL_POSITION_CENTER_SCREEN_WITH_MOUSE_FOCUS = 4

Initial window position is the center of the screen containing the mouse pointer.

WindowInitialPosition WINDOW_INITIAL_POSITION_CENTER_SCREEN_WITH_KEYBOARD_FOCUS = 5

Initial window position is the center of the screen containing the window with the keyboard focus.

NOTIFICATION_VISIBILITY_CHANGED = 30 🔗

Emitted when Window's visibility changes, right before visibility_changed.

NOTIFICATION_THEME_CHANGED = 32 🔗

Sent when the node needs to refresh its theme items. This happens in one of the following cases:

The theme property is changed on this node or any of its ancestors.

The theme_type_variation property is changed on this node.

The node enters the scene tree.

Note: As an optimization, this notification won't be sent from changes that occur while this node is outside of the scene tree. Instead, all of the theme item updates can be applied at once when the node enters the scene tree.

String accessibility_description = "" 🔗

void set_accessibility_description(value: String)

String get_accessibility_description()

The human-readable node description that is reported to assistive apps.

String accessibility_name = "" 🔗

void set_accessibility_name(value: String)

String get_accessibility_name()

The human-readable node name that is reported to assistive apps.

bool always_on_top = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the window will be on top of all other windows. Does not work if transient is enabled.

bool auto_translate 🔗

void set_auto_translate(value: bool)

bool is_auto_translating()

Deprecated: Use Node.auto_translate_mode and Node.can_auto_translate() instead.

Toggles if any text should automatically change to its translated version depending on the current locale.

bool borderless = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the window will have no borders.

ContentScaleAspect content_scale_aspect = 0 🔗

void set_content_scale_aspect(value: ContentScaleAspect)

ContentScaleAspect get_content_scale_aspect()

Specifies how the content's aspect behaves when the Window is resized. The base aspect is determined by content_scale_size.

float content_scale_factor = 1.0 🔗

void set_content_scale_factor(value: float)

float get_content_scale_factor()

Specifies the base scale of Window's content when its size is equal to content_scale_size. See also Viewport.get_stretch_transform().

ContentScaleMode content_scale_mode = 0 🔗

void set_content_scale_mode(value: ContentScaleMode)

ContentScaleMode get_content_scale_mode()

Specifies how the content is scaled when the Window is resized.

Vector2i content_scale_size = Vector2i(0, 0) 🔗

void set_content_scale_size(value: Vector2i)

Vector2i get_content_scale_size()

Base size of the content (i.e. nodes that are drawn inside the window). If non-zero, Window's content will be scaled when the window is resized to a different size.

ContentScaleStretch content_scale_stretch = 0 🔗

void set_content_scale_stretch(value: ContentScaleStretch)

ContentScaleStretch get_content_scale_stretch()

The policy to use to determine the final scale factor for 2D elements. This affects how content_scale_factor is applied, in addition to the automatic scale factor determined by content_scale_size.

void set_current_screen(value: int)

int get_current_screen()

The screen the window is currently on.

bool exclude_from_capture = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the Window is excluded from screenshots taken by DisplayServer.screen_get_image(), DisplayServer.screen_get_image_rect(), and DisplayServer.screen_get_pixel().

Note: This property is implemented on macOS and Windows.

Note: Enabling this setting will prevent standard screenshot methods from capturing a window image, but does NOT guarantee that other apps won't be able to capture an image. It should not be used as a DRM or security measure.

bool exclusive = false 🔗

void set_exclusive(value: bool)

If true, the Window will be in exclusive mode. Exclusive windows are always on top of their parent and will block all input going to the parent Window.

Needs transient enabled to work.

bool extend_to_title = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the Window contents is expanded to the full size of the window, window title bar is transparent.

Note: This property is implemented only on macOS.

Note: This property only works with native windows.

bool force_native = false 🔗

void set_force_native(value: bool)

bool get_force_native()

If true, native window will be used regardless of parent viewport and project settings.

WindowInitialPosition initial_position = 0 🔗

void set_initial_position(value: WindowInitialPosition)

WindowInitialPosition get_initial_position()

Specifies the initial type of position for the Window.

bool keep_title_visible = false 🔗

void set_keep_title_visible(value: bool)

bool get_keep_title_visible()

If true, the Window width is expanded to keep the title bar text fully visible.

Vector2i max_size = Vector2i(0, 0) 🔗

void set_max_size(value: Vector2i)

Vector2i get_max_size()

If non-zero, the Window can't be resized to be bigger than this size.

Note: This property will be ignored if the value is lower than min_size.

bool maximize_disabled = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the Window's maximize button is disabled.

Note: If both minimize and maximize buttons are disabled, buttons are fully hidden, and only close button is visible.

Note: This property is implemented only on macOS and Windows.

Vector2i min_size = Vector2i(0, 0) 🔗

void set_min_size(value: Vector2i)

Vector2i get_min_size()

If non-zero, the Window can't be resized to be smaller than this size.

Note: This property will be ignored in favor of get_contents_minimum_size() if wrap_controls is enabled and if its size is bigger.

bool minimize_disabled = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the Window's minimize button is disabled.

Note: If both minimize and maximize buttons are disabled, buttons are fully hidden, and only close button is visible.

Note: This property is implemented only on macOS and Windows.

void set_mode(value: Mode)

Set's the window's current mode.

Note: Fullscreen mode is not exclusive full screen on Windows and Linux.

Note: This method only works with native windows, i.e. the main window and Window-derived nodes when Viewport.gui_embed_subwindows is disabled in the main viewport.

bool mouse_passthrough = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, all mouse events will be passed to the underlying window of the same application. See also mouse_passthrough_polygon.

Note: This property is implemented on Linux (X11), macOS and Windows.

Note: This property only works with native windows.

PackedVector2Array mouse_passthrough_polygon = PackedVector2Array() 🔗

void set_mouse_passthrough_polygon(value: PackedVector2Array)

PackedVector2Array get_mouse_passthrough_polygon()

Sets a polygonal region of the window which accepts mouse events. Mouse events outside the region will be passed through.

Passing an empty array will disable passthrough support (all mouse events will be intercepted by the window, which is the default behavior).

Note: This property is ignored if mouse_passthrough is set to true.

Note: On Windows, the portion of a window that lies outside the region is not drawn, while on Linux (X11) and macOS it is.

Note: This property is implemented on Linux (X11), macOS and Windows.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedVector2Array for more details.

bool popup_window = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the Window will be considered a popup. Popups are sub-windows that don't show as separate windows in system's window manager's window list and will send close request when anything is clicked outside of them (unless exclusive is enabled).

bool popup_wm_hint = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the Window will signal to the window manager that it is supposed to be an implementation-defined "popup" (usually a floating, borderless, untileable and immovable child window).

Vector2i position = Vector2i(0, 0) 🔗

void set_position(value: Vector2i)

Vector2i get_position()

The window's position in pixels.

If ProjectSettings.display/window/subwindows/embed_subwindows is false, the position is in absolute screen coordinates. This typically applies to editor plugins. If the setting is true, the window's position is in the coordinates of its parent Viewport.

Note: This property only works if initial_position is set to WINDOW_INITIAL_POSITION_ABSOLUTE.

bool sharp_corners = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the Window will override the OS window style to display sharp corners.

Note: This property is implemented only on Windows (11).

Note: This property only works with native windows.

Vector2i size = Vector2i(100, 100) 🔗

void set_size(value: Vector2i)

The window's size in pixels.

void set_theme(value: Theme)

The Theme resource this node and all its Control and Window children use. If a child node has its own Theme resource set, theme items are merged with child's definitions having higher priority.

Note: Window styles will have no effect unless the window is embedded.

StringName theme_type_variation = &"" 🔗

void set_theme_type_variation(value: StringName)

StringName get_theme_type_variation()

The name of a theme type variation used by this Window to look up its own theme items. See Control.theme_type_variation for more details.

void set_title(value: String)

The window's title. If the Window is native, title styles set in Theme will have no effect.

bool transient = false 🔗

void set_transient(value: bool)

If true, the Window is transient, i.e. it's considered a child of another Window. The transient window will be destroyed with its transient parent and will return focus to their parent when closed. The transient window is displayed on top of a non-exclusive full-screen parent window. Transient windows can't enter full-screen mode.

Note that behavior might be different depending on the platform.

bool transient_to_focused = false 🔗

void set_transient_to_focused(value: bool)

bool is_transient_to_focused()

If true, and the Window is transient, this window will (at the time of becoming visible) become transient to the currently focused window instead of the immediate parent window in the hierarchy. Note that the transient parent is assigned at the time this window becomes visible, so changing it afterwards has no effect until re-shown.

bool transparent = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the Window's background can be transparent. This is best used with embedded windows.

Note: Transparency support is implemented on Linux, macOS and Windows, but availability might vary depending on GPU driver, display manager, and compositor capabilities.

Note: This property has no effect if ProjectSettings.display/window/per_pixel_transparency/allowed is set to false.

bool unfocusable = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the Window can't be focused nor interacted with. It can still be visible.

bool unresizable = false 🔗

void set_flag(flag: Flags, enabled: bool)

bool get_flag(flag: Flags) const

If true, the window can't be resized.

bool visible = true 🔗

void set_visible(value: bool)

If true, the window is visible.

bool wrap_controls = false 🔗

void set_wrap_controls(value: bool)

bool is_wrapping_controls()

If true, the window's size will automatically update when a child node is added or removed, ignoring min_size if the new size is bigger.

If false, you need to call child_controls_changed() manually.

Vector2 _get_contents_minimum_size() virtual const 🔗

Virtual method to be implemented by the user. Overrides the value returned by get_contents_minimum_size().

void add_theme_color_override(name: StringName, color: Color) 🔗

Creates a local override for a theme Color with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_color_override().

See also get_theme_color() and Control.add_theme_color_override() for more details.

void add_theme_constant_override(name: StringName, constant: int) 🔗

Creates a local override for a theme constant with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_constant_override().

See also get_theme_constant().

void add_theme_font_override(name: StringName, font: Font) 🔗

Creates a local override for a theme Font with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_font_override().

See also get_theme_font().

void add_theme_font_size_override(name: StringName, font_size: int) 🔗

Creates a local override for a theme font size with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_font_size_override().

See also get_theme_font_size().

void add_theme_icon_override(name: StringName, texture: Texture2D) 🔗

Creates a local override for a theme icon with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_icon_override().

See also get_theme_icon().

void add_theme_stylebox_override(name: StringName, stylebox: StyleBox) 🔗

Creates a local override for a theme StyleBox with the specified name. Local overrides always take precedence when fetching theme items for the control. An override can be removed with remove_theme_stylebox_override().

See also get_theme_stylebox() and Control.add_theme_stylebox_override() for more details.

void begin_bulk_theme_override() 🔗

Prevents *_theme_*_override methods from emitting NOTIFICATION_THEME_CHANGED until end_bulk_theme_override() is called.

bool can_draw() const 🔗

Returns whether the window is being drawn to the screen.

void child_controls_changed() 🔗

Requests an update of the Window size to fit underlying Control nodes.

void end_bulk_theme_override() 🔗

Ends a bulk theme override update. See begin_bulk_theme_override().

Vector2 get_contents_minimum_size() const 🔗

Returns the combined minimum size from the child Control nodes of the window. Use child_controls_changed() to update it when child nodes have changed.

The value returned by this method can be overridden with _get_contents_minimum_size().

bool get_flag(flag: Flags) const 🔗

Returns true if the flag is set.

Window get_focused_window() static 🔗

Returns the focused window.

LayoutDirection get_layout_direction() const 🔗

Returns layout direction and text writing direction.

Vector2i get_position_with_decorations() const 🔗

Returns the window's position including its border.

Note: If visible is false, this method returns the same value as position.

Vector2i get_size_with_decorations() const 🔗

Returns the window's size including its border.

Note: If visible is false, this method returns the same value as size.

Color get_theme_color(name: StringName, theme_type: StringName = &"") const 🔗

Returns a Color from the first matching Theme in the tree if that Theme has a color item with the specified name and theme_type.

See Control.get_theme_color() for more details.

int get_theme_constant(name: StringName, theme_type: StringName = &"") const 🔗

Returns a constant from the first matching Theme in the tree if that Theme has a constant item with the specified name and theme_type.

See Control.get_theme_color() for more details.

float get_theme_default_base_scale() const 🔗

Returns the default base scale value from the first matching Theme in the tree if that Theme has a valid Theme.default_base_scale value.

See Control.get_theme_color() for details.

Font get_theme_default_font() const 🔗

Returns the default font from the first matching Theme in the tree if that Theme has a valid Theme.default_font value.

See Control.get_theme_color() for details.

int get_theme_default_font_size() const 🔗

Returns the default font size value from the first matching Theme in the tree if that Theme has a valid Theme.default_font_size value.

See Control.get_theme_color() for details.

Font get_theme_font(name: StringName, theme_type: StringName = &"") const 🔗

Returns a Font from the first matching Theme in the tree if that Theme has a font item with the specified name and theme_type.

See Control.get_theme_color() for details.

int get_theme_font_size(name: StringName, theme_type: StringName = &"") const 🔗

Returns a font size from the first matching Theme in the tree if that Theme has a font size item with the specified name and theme_type.

See Control.get_theme_color() for details.

Texture2D get_theme_icon(name: StringName, theme_type: StringName = &"") const 🔗

Returns an icon from the first matching Theme in the tree if that Theme has an icon item with the specified name and theme_type.

See Control.get_theme_color() for details.

StyleBox get_theme_stylebox(name: StringName, theme_type: StringName = &"") const 🔗

Returns a StyleBox from the first matching Theme in the tree if that Theme has a stylebox item with the specified name and theme_type.

See Control.get_theme_color() for details.

int get_window_id() const 🔗

Returns the ID of the window.

Causes the window to grab focus, allowing it to receive user input.

bool has_focus() const 🔗

Returns true if the window is focused.

bool has_theme_color(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has a color item with the specified name and theme_type.

See Control.get_theme_color() for details.

bool has_theme_color_override(name: StringName) const 🔗

Returns true if there is a local override for a theme Color with the specified name in this Control node.

See add_theme_color_override().

bool has_theme_constant(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has a constant item with the specified name and theme_type.

See Control.get_theme_color() for details.

bool has_theme_constant_override(name: StringName) const 🔗

Returns true if there is a local override for a theme constant with the specified name in this Control node.

See add_theme_constant_override().

bool has_theme_font(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has a font item with the specified name and theme_type.

See Control.get_theme_color() for details.

bool has_theme_font_override(name: StringName) const 🔗

Returns true if there is a local override for a theme Font with the specified name in this Control node.

See add_theme_font_override().

bool has_theme_font_size(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has a font size item with the specified name and theme_type.

See Control.get_theme_color() for details.

bool has_theme_font_size_override(name: StringName) const 🔗

Returns true if there is a local override for a theme font size with the specified name in this Control node.

See add_theme_font_size_override().

bool has_theme_icon(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has an icon item with the specified name and theme_type.

See Control.get_theme_color() for details.

bool has_theme_icon_override(name: StringName) const 🔗

Returns true if there is a local override for a theme icon with the specified name in this Control node.

See add_theme_icon_override().

bool has_theme_stylebox(name: StringName, theme_type: StringName = &"") const 🔗

Returns true if there is a matching Theme in the tree that has a stylebox item with the specified name and theme_type.

See Control.get_theme_color() for details.

bool has_theme_stylebox_override(name: StringName) const 🔗

Returns true if there is a local override for a theme StyleBox with the specified name in this Control node.

See add_theme_stylebox_override().

Hides the window. This is not the same as minimized state. Hidden window can't be interacted with and needs to be made visible with show().

bool is_embedded() const 🔗

Returns true if the window is currently embedded in another window.

bool is_layout_rtl() const 🔗

Returns true if the layout is right-to-left.

bool is_maximize_allowed() const 🔗

Returns true if the window can be maximized (the maximize button is enabled).

bool is_using_font_oversampling() const 🔗

Returns true if font oversampling is enabled. See set_use_font_oversampling().

void move_to_center() 🔗

Centers a native window on the current screen and an embedded window on its embedder Viewport.

void move_to_foreground() 🔗

Deprecated: Use grab_focus() instead.

Causes the window to grab focus, allowing it to receive user input.

void popup(rect: Rect2i = Rect2i(0, 0, 0, 0)) 🔗

Shows the Window and makes it transient (see transient). If rect is provided, it will be set as the Window's size. Fails if called on the main window.

If ProjectSettings.display/window/subwindows/embed_subwindows is true (single-window mode), rect's coordinates are global and relative to the main window's top-left corner (excluding window decorations). If rect's position coordinates are negative, the window will be located outside the main window and may not be visible as a result.

If ProjectSettings.display/window/subwindows/embed_subwindows is false (multi-window mode), rect's coordinates are global and relative to the top-left corner of the leftmost screen. If rect's position coordinates are negative, the window will be placed at the top-left corner of the screen.

Note: rect must be in global coordinates if specified.

void popup_centered(minsize: Vector2i = Vector2i(0, 0)) 🔗

Popups the Window at the center of the current screen, with optionally given minimum size. If the Window is embedded, it will be centered in the parent Viewport instead.

Note: Calling it with the default value of minsize is equivalent to calling it with size.

void popup_centered_clamped(minsize: Vector2i = Vector2i(0, 0), fallback_ratio: float = 0.75) 🔗

Popups the Window centered inside its parent Window. fallback_ratio determines the maximum size of the Window, in relation to its parent.

Note: Calling it with the default value of minsize is equivalent to calling it with size.

void popup_centered_ratio(ratio: float = 0.8) 🔗

If Window is embedded, popups the Window centered inside its embedder and sets its size as a ratio of embedder's size.

If Window is a native window, popups the Window centered inside the screen of its parent Window and sets its size as a ratio of the screen size.

void popup_exclusive(from_node: Node, rect: Rect2i = Rect2i(0, 0, 0, 0)) 🔗

Attempts to parent this dialog to the last exclusive window relative to from_node, and then calls popup() on it. The dialog must have no current parent, otherwise the method fails.

See also set_unparent_when_invisible() and Node.get_last_exclusive_window().

void popup_exclusive_centered(from_node: Node, minsize: Vector2i = Vector2i(0, 0)) 🔗

Attempts to parent this dialog to the last exclusive window relative to from_node, and then calls popup_centered() on it. The dialog must have no current parent, otherwise the method fails.

See also set_unparent_when_invisible() and Node.get_last_exclusive_window().

void popup_exclusive_centered_clamped(from_node: Node, minsize: Vector2i = Vector2i(0, 0), fallback_ratio: float = 0.75) 🔗

Attempts to parent this dialog to the last exclusive window relative to from_node, and then calls popup_centered_clamped() on it. The dialog must have no current parent, otherwise the method fails.

See also set_unparent_when_invisible() and Node.get_last_exclusive_window().

void popup_exclusive_centered_ratio(from_node: Node, ratio: float = 0.8) 🔗

Attempts to parent this dialog to the last exclusive window relative to from_node, and then calls popup_centered_ratio() on it. The dialog must have no current parent, otherwise the method fails.

See also set_unparent_when_invisible() and Node.get_last_exclusive_window().

void popup_exclusive_on_parent(from_node: Node, parent_rect: Rect2i) 🔗

Attempts to parent this dialog to the last exclusive window relative to from_node, and then calls popup_on_parent() on it. The dialog must have no current parent, otherwise the method fails.

See also set_unparent_when_invisible() and Node.get_last_exclusive_window().

void popup_on_parent(parent_rect: Rect2i) 🔗

Popups the Window with a position shifted by parent Window's position. If the Window is embedded, has the same effect as popup().

void remove_theme_color_override(name: StringName) 🔗

Removes a local override for a theme Color with the specified name previously added by add_theme_color_override() or via the Inspector dock.

void remove_theme_constant_override(name: StringName) 🔗

Removes a local override for a theme constant with the specified name previously added by add_theme_constant_override() or via the Inspector dock.

void remove_theme_font_override(name: StringName) 🔗

Removes a local override for a theme Font with the specified name previously added by add_theme_font_override() or via the Inspector dock.

void remove_theme_font_size_override(name: StringName) 🔗

Removes a local override for a theme font size with the specified name previously added by add_theme_font_size_override() or via the Inspector dock.

void remove_theme_icon_override(name: StringName) 🔗

Removes a local override for a theme icon with the specified name previously added by add_theme_icon_override() or via the Inspector dock.

void remove_theme_stylebox_override(name: StringName) 🔗

Removes a local override for a theme StyleBox with the specified name previously added by add_theme_stylebox_override() or via the Inspector dock.

void request_attention() 🔗

Tells the OS that the Window needs an attention. This makes the window stand out in some way depending on the system, e.g. it might blink on the task bar.

Resets the size to the minimum size, which is the max of min_size and (if wrap_controls is enabled) get_contents_minimum_size(). This is equivalent to calling set_size(Vector2i()) (or any size below the minimum).

void set_flag(flag: Flags, enabled: bool) 🔗

Sets a specified window flag.

void set_ime_active(active: bool) 🔗

If active is true, enables system's native IME (Input Method Editor).

void set_ime_position(position: Vector2i) 🔗

Moves IME to the given position.

void set_layout_direction(direction: LayoutDirection) 🔗

Sets layout direction and text writing direction. Right-to-left layouts are necessary for certain languages (e.g. Arabic and Hebrew).

void set_unparent_when_invisible(unparent: bool) 🔗

If unparent is true, the window is automatically unparented when going invisible.

Note: Make sure to keep a reference to the node, otherwise it will be orphaned. You also need to manually call Node.queue_free() to free the window if it's not parented.

void set_use_font_oversampling(enable: bool) 🔗

Enables font oversampling. This makes fonts look better when they are scaled up.

Makes the Window appear. This enables interactions with the Window and doesn't change any of its property other than visibility (unlike e.g. popup()).

Starts an interactive drag operation on the window, using the current mouse position. Call this method when handling a mouse button being pressed to simulate a pressed event on the window's title bar. Using this method allows the window to participate in space switching, tiling, and other system features.

void start_resize(edge: WindowResizeEdge) 🔗

Starts an interactive resize operation on the window, using the current mouse position. Call this method when handling a mouse button being pressed to simulate a pressed event on the window's edge.

Color title_color = Color(0.875, 0.875, 0.875, 1) 🔗

The color of the title's text.

Color title_outline_modulate = Color(0, 0, 0, 1) 🔗

The color of the title's text outline.

int close_h_offset = 18 🔗

Horizontal position offset of the close button, relative to the end of the title bar, towards the beginning of the title bar.

int close_v_offset = 24 🔗

Vertical position offset of the close button, relative to the bottom of the title bar, towards the top of the title bar.

int resize_margin = 4 🔗

Defines the outside margin at which the window border can be grabbed with mouse and resized.

int title_height = 36 🔗

Height of the title bar.

int title_outline_size = 0 🔗

The size of the title outline.

The font used to draw the title.

int title_font_size 🔗

The size of the title font.

The icon for the close button.

Texture2D close_pressed 🔗

The icon for the close button when it's being pressed.

StyleBox embedded_border 🔗

The background style used when the Window is embedded. Note that this is drawn only under the window's content, excluding the title. For proper borders and title bar style, you can use expand_margin_* properties of StyleBoxFlat.

Note: The content background will not be visible unless transparent is enabled.

StyleBox embedded_unfocused_border 🔗

The background style used when the Window is embedded and unfocused.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    get_window().files_dropped.connect(on_files_dropped)

func on_files_dropped(files):
    print(files)
```

Example 2 (julia):
```julia
# Set region, using Path2D node.
$Window.mouse_passthrough_polygon = $Path2D.curve.get_baked_points()

# Set region, using Polygon2D node.
$Window.mouse_passthrough_polygon = $Polygon2D.polygon

# Reset region to default.
$Window.mouse_passthrough_polygon = []
```

Example 3 (julia):
```julia
// Set region, using Path2D node.
GetNode<Window>("Window").MousePassthroughPolygon = GetNode<Path2D>("Path2D").Curve.GetBakedPoints();

// Set region, using Polygon2D node.
GetNode<Window>("Window").MousePassthroughPolygon = GetNode<Polygon2D>("Polygon2D").Polygon;

// Reset region to default.
GetNode<Window>("Window").MousePassthroughPolygon = [];
```

---

## XRControllerTracker

**URL:** https://docs.godotengine.org/en/stable/classes/class_xrcontrollertracker.html

**Contents:**
- XRControllerTracker
- Description
- Tutorials
- Properties
- User-contributed notes

Inherits: XRPositionalTracker < XRTracker < RefCounted < Object

A tracked controller.

An instance of this object represents a controller that is tracked.

As controllers are turned on and the XRInterface detects them, instances of this object are automatically added to this list of active tracking objects accessible through the XRServer.

The XRController3D consumes objects of this type and should be used in your project.

XR documentation index

2 (overrides XRTracker)

Please read the User-contributed notes policy before submitting a comment.

---
