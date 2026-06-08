# Godot - File Io

**Pages:** 17

---

## Background loading

**URL:** https://docs.godotengine.org/en/stable/tutorials/io/background_loading.html

**Contents:**
- Background loading
- Using ResourceLoader
- Example
- User-contributed notes

Commonly, games need to load resources asynchronously. When switching the main scene of your game (e.g. going to a new level), you might want to show a loading screen with some indication that progress is being made, or you may want to load additional resources during gameplay.

The standard load method (ResourceLoader.load or GDScript's simpler load) blocks your thread, making your game appear unresponsive while the resource is being loaded.

One way around this is using ResourceLoader to load resources asynchronously in background threads.

Generally, you queue requests to load resources for a path using ResourceLoader.load_threaded_request, which will then be loaded in threads in the background.

You can check the status with ResourceLoader.load_threaded_get_status. Progress can be obtained by passing an array variable via progress which will return a one element array containing the percentage.

Finally, you retrieve loaded resources by calling ResourceLoader.load_threaded_get.

Once you call load_threaded_get(), either the resource finished loading in the background and will be returned instantly or the load will block at this point like load() would. If you want to guarantee this does not block, you either need to ensure there is enough time between requesting the load and retrieving the resource or you need to check the status manually.

This example demonstrates how to load a scene in the background. We will have a button spawn an enemy when pressed. The enemy will be Enemy.tscn which we will load on _ready and instantiate when pressed. The path will be "Enemy.tscn" which is located at res://Enemy.tscn.

First, we will start a request to load the resource and connect the button:

Now _on_button_pressed will be called when the button is pressed. This method will be used to spawn an enemy.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
const ENEMY_SCENE_PATH : String = "Enemy.tscn"

func _ready():
    ResourceLoader.load_threaded_request(ENEMY_SCENE_PATH)
    self.pressed.connect(_on_button_pressed)
```

Example 2 (gdscript):
```gdscript
using Godot;

public partial class MyButton : Button
{
    private const string EnemyScenePath = "Enemy.tscn";

    public override void _Ready()
    {
        ResourceLoader.LoadThreadedRequest(EnemyScenePath);
        Pressed += OnButtonPressed;
    }
}
```

Example 3 (gdscript):
```gdscript
func _on_button_pressed(): # Button was pressed.
    # Obtain the resource now that we need it.
    var enemy_scene = ResourceLoader.load_threaded_get(ENEMY_SCENE_PATH)
    # Instantiate the enemy scene and add it to the current scene.
    var enemy = enemy_scene.instantiate()
    add_child(enemy)
```

Example 4 (gdscript):
```gdscript
private void OnButtonPressed() // Button was pressed.
{
    // Obtain the resource now that we need it.
    var enemyScene = (PackedScene)ResourceLoader.LoadThreadedGet(EnemyScenePath);
    // Instantiate the enemy scene and add it to the current scene.
    var enemy = enemyScene.Instantiate();
    AddChild(enemy);
}
```

---

## Binary serialization API

**URL:** https://docs.godotengine.org/en/stable/tutorials/io/binary_serialization_api.html

**Contents:**
- Binary serialization API
- Introduction
- Full Objects vs Object instance IDs
- Packet specification
  - 0: null
  - 1: bool
  - 2: int
  - 3: float
  - 4: String
  - 5: Vector2

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

Godot has a serialization API based on Variant. It's used for converting data types to an array of bytes efficiently. This API is exposed via the global bytes_to_var() and var_to_bytes() functions, but it is also used in the get_var and store_var methods of FileAccess as well as the packet APIs for PacketPeer. This format is not used for binary scenes and resources.

If a variable is serialized with full_objects = true, then any Objects contained in the variable will be serialized and included in the result. This is recursive.

If full_objects = false, then only the instance IDs will be serialized for any Objects contained in the variable.

The packet is designed to be always padded to 4 bytes. All values are little-endian-encoded. All packets have a 4-byte header representing an integer, specifying the type of data.

The lowest value two bytes are used to determine the type, while the highest value two bytes contain flags:

Following this is the actual packet contents, which varies for each type of packet. Note that this assumes Godot is compiled with single-precision floats, which is the default. If Godot was compiled with double-precision floats, the length of "Float" fields within data structures should be 8, and the offset should be (offset - 4) * 2 + 4. The "float" type itself always uses double precision.

0 for False, 1 for True

If no flags are set (flags == 0), the integer is sent as a 32 bit integer:

32-bit signed integer

If flag ENCODE_FLAG_64 is set (flags & 1 == 1), the integer is sent as a 64-bit integer:

64-bit signed integer

If no flags are set (flags == 0), the float is sent as a 32 bit single precision:

IEEE 754 single-precision float

If flag ENCODE_FLAG_64 is set (flags & 1 == 1), the float is sent as a 64-bit double precision number:

IEEE 754 double-precision float

String length (in bytes)

This field is padded to 4 bytes.

The X component of the X column vector, accessed via [0][0]

The Y component of the X column vector, accessed via [0][1]

The X component of the Y column vector, accessed via [1][0]

The Y component of the Y column vector, accessed via [1][1]

The X component of the origin vector, accessed via [2][0]

The Y component of the origin vector, accessed via [2][1]

The X component of the X column vector, accessed via [0][0]

The Y component of the X column vector, accessed via [0][1]

The Z component of the X column vector, accessed via [0][2]

The X component of the Y column vector, accessed via [1][0]

The Y component of the Y column vector, accessed via [1][1]

The Z component of the Y column vector, accessed via [1][2]

The X component of the Z column vector, accessed via [2][0]

The Y component of the Z column vector, accessed via [2][1]

The Z component of the Z column vector, accessed via [2][2]

The X component of the X column vector, accessed via [0][0]

The Y component of the X column vector, accessed via [0][1]

The Z component of the X column vector, accessed via [0][2]

The X component of the Y column vector, accessed via [1][0]

The Y component of the Y column vector, accessed via [1][1]

The Z component of the Y column vector, accessed via [1][2]

The X component of the Z column vector, accessed via [2][0]

The Y component of the Z column vector, accessed via [2][1]

The Z component of the Z column vector, accessed via [2][2]

The X component of the origin vector, accessed via [3][0]

The Y component of the origin vector, accessed via [3][1]

The Z component of the origin vector, accessed via [3][2]

Red (typically 0..1, can be above 1 for overbright colors)

Green (typically 0..1, can be above 1 for overbright colors)

Blue (typically 0..1, can be above 1 for overbright colors)

String length, or new format (val&0x80000000!=0 and NameCount=val&0x7FFFFFFF)

Flags (absolute: val&1 != 0 )

For each Name and Sub-Name

Every name string is padded to 4 bytes.

An Object could be serialized in three different ways: as a null value, with full_objects = false, or with full_objects = true.

Zero (32-bit signed integer)

The Object instance ID (64-bit signed integer)

Class name (String length)

Class name (UTF-8 encoded string)

The number of properties that are serialized

Property name (String length)

Property name (UTF-8 encoded string)

Property value, using this same format

Not all properties are included. Only properties that are configured with the PROPERTY_USAGE_STORAGE flag set will be serialized. You can add a new usage flag to a property by overriding the _get_property_list method in your class. You can also check how property usage is configured by calling Object._get_property_list See PropertyUsageFlags for the possible usage flags.

val&0x7FFFFFFF = elements, val&0x80000000 = shared (bool)

Then what follows is, for amount of "elements", pairs of key and value, one after the other, using this same format.

val&0x7FFFFFFF = elements, val&0x80000000 = shared (bool)

Then what follows is, for amount of "elements", values one after the other, using this same format.

The array data is padded to 4 bytes.

Array length (Integers)

32-bit signed integer

Array length (Integers)

64-bit signed integer

Array length (Floats)

32-bit IEEE 754 single-precision float

Array length (Floats)

64-bit IEEE 754 double-precision float

Array length (Strings)

Every string is padded to 4 bytes.

Red (typically 0..1, can be above 1 for overbright colors)

Green (typically 0..1, can be above 1 for overbright colors)

Blue (typically 0..1, can be above 1 for overbright colors)

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
base_type = val & 0xFFFF;
flags = val >> 16;
```

---

## ConfigFile

**URL:** https://docs.godotengine.org/en/stable/classes/class_configfile.html

**Contents:**
- ConfigFile
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Helper class to handle INI-style files.

This helper class can be used to store Variant values on the filesystem using INI-style formatting. The stored values are identified by a section and a key:

The stored data can be saved to or parsed from a file, though ConfigFile objects can also be used directly without accessing the filesystem.

The following example shows how to create a simple ConfigFile and save it on disc:

This example shows how the above file could be loaded:

Any operation that mutates the ConfigFile such as set_value(), clear(), or erase_section(), only changes what is loaded in memory. If you want to write the change to a file, you have to save the changes with save(), save_encrypted(), or save_encrypted_pass().

Keep in mind that section and property names can't contain spaces. Anything after a space will be ignored on save and on load.

ConfigFiles can also contain manually written comment lines starting with a semicolon (;). Those lines will be ignored when parsing the file. Note that comments will be lost when saving the ConfigFile. This can still be useful for dedicated server configuration files, which are typically never overwritten without explicit user action.

Note: The file extension given to a ConfigFile does not have any impact on its formatting or behavior. By convention, the .cfg extension is used here, but any other extension such as .ini is also valid. Since neither .cfg nor .ini are standardized, Godot's ConfigFile formatting may differ from files written by other programs.

encode_to_text() const

erase_section(section: String)

erase_section_key(section: String, key: String)

get_section_keys(section: String) const

get_value(section: String, key: String, default: Variant = null) const

has_section(section: String) const

has_section_key(section: String, key: String) const

load_encrypted(path: String, key: PackedByteArray)

load_encrypted_pass(path: String, password: String)

save_encrypted(path: String, key: PackedByteArray)

save_encrypted_pass(path: String, password: String)

set_value(section: String, key: String, value: Variant)

Removes the entire contents of the config.

String encode_to_text() const 

Obtain the text version of this config file (the same text that would be written to a file).

void erase_section(section: String) 

Deletes the specified section along with all the key-value pairs inside. Raises an error if the section does not exist.

void erase_section_key(section: String, key: String) 

Deletes the specified key in a section. Raises an error if either the section or the key do not exist.

PackedStringArray get_section_keys(section: String) const 

Returns an array of all defined key identifiers in the specified section. Raises an error and returns an empty array if the section does not exist.

PackedStringArray get_sections() const 

Returns an array of all defined section identifiers.

Variant get_value(section: String, key: String, default: Variant = null) const 

Returns the current value for the specified section and key. If either the section or the key do not exist, the method returns the fallback default value. If default is not specified or set to null, an error is also raised.

bool has_section(section: String) const 

Returns true if the specified section exists.

bool has_section_key(section: String, key: String) const 

Returns true if the specified section-key pair exists.

Error load(path: String) 

Loads the config file specified as a parameter. The file's contents are parsed and loaded in the ConfigFile object which the method was called on.

Returns @GlobalScope.OK on success, or one of the other Error values if the operation failed.

Error load_encrypted(path: String, key: PackedByteArray) 

Loads the encrypted config file specified as a parameter, using the provided key to decrypt it. The file's contents are parsed and loaded in the ConfigFile object which the method was called on.

Returns @GlobalScope.OK on success, or one of the other Error values if the operation failed.

Error load_encrypted_pass(path: String, password: String) 

Loads the encrypted config file specified as a parameter, using the provided password to decrypt it. The file's contents are parsed and loaded in the ConfigFile object which the method was called on.

Returns @GlobalScope.OK on success, or one of the other Error values if the operation failed.

Error parse(data: String) 

Parses the passed string as the contents of a config file. The string is parsed and loaded in the ConfigFile object which the method was called on.

Returns @GlobalScope.OK on success, or one of the other Error values if the operation failed.

Error save(path: String) 

Saves the contents of the ConfigFile object to the file specified as a parameter. The output file uses an INI-style structure.

Returns @GlobalScope.OK on success, or one of the other Error values if the operation failed.

Error save_encrypted(path: String, key: PackedByteArray) 

Saves the contents of the ConfigFile object to the AES-256 encrypted file specified as a parameter, using the provided key to encrypt it. The output file uses an INI-style structure.

Returns @GlobalScope.OK on success, or one of the other Error values if the operation failed.

Error save_encrypted_pass(path: String, password: String) 

Saves the contents of the ConfigFile object to the AES-256 encrypted file specified as a parameter, using the provided password to encrypt it. The output file uses an INI-style structure.

Returns @GlobalScope.OK on success, or one of the other Error values if the operation failed.

void set_value(section: String, key: String, value: Variant) 

Assigns a value to the specified key of the specified section. If either the section or the key do not exist, they are created. Passing a null value deletes the specified key if it exists, and deletes the section if it ends up empty once the key has been removed.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
[section]
some_key=42
string_example="Hello World3D!"
a_vector=Vector3(1, 0, 2)
```

Example 2 (gdscript):
```gdscript
# Create new ConfigFile object.
var config = ConfigFile.new()

# Store some values.
config.set_value("Player1", "player_name", "Steve")
config.set_value("Player1", "best_score", 10)
config.set_value("Player2", "player_name", "V3geta")
config.set_value("Player2", "best_score", 9001)

# Save it to a file (overwrite if already exists).
config.save("user://scores.cfg")
```

Example 3 (gdscript):
```gdscript
// Create new ConfigFile object.
var config = new ConfigFile();

// Store some values.
config.SetValue("Player1", "player_name", "Steve");
config.SetValue("Player1", "best_score", 10);
config.SetValue("Player2", "player_name", "V3geta");
config.SetValue("Player2", "best_score", 9001);

// Save it to a file (overwrite if already exists).
config.Save("user://scores.cfg");
```

Example 4 (sql):
```sql
var score_data = {}
var config = ConfigFile.new()

# Load data from a file.
var err = config.load("user://scores.cfg")

# If the file didn't load, ignore it.
if err != OK:
    return

# Iterate over all sections.
for player in config.get_sections():
    # Fetch the data for each section.
    var player_name = config.get_value(player, "player_name")
    var player_score = config.get_value(player, "best_score")
    score_data[player_name] = player_score
```

---

## CurveTexture

**URL:** https://docs.godotengine.org/en/stable/classes/class_curvetexture.html

**Contents:**
- CurveTexture
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: Texture2D < Texture < Resource < RefCounted < Object

A 1D texture where pixel brightness corresponds to points on a curve.

A 1D texture where pixel brightness corresponds to points on a unit Curve resource, either in grayscale or in red. This visual representation simplifies the task of saving curves as image files.

If you need to store up to 3 curves within a single texture, use CurveXYZTexture instead. See also GradientTexture1D and GradientTexture2D.

resource_local_to_scene

false (overrides Resource)

TextureMode TEXTURE_MODE_RGB = 0

Store the curve equally across the red, green and blue channels. This uses more video memory, but is more compatible with shaders that only read the green and blue values.

TextureMode TEXTURE_MODE_RED = 1

Store the curve only in the red channel. This saves video memory, but some custom shaders may not be able to work with this.

void set_curve(value: Curve)

The Curve that is rendered onto the texture. Should be a unit Curve.

TextureMode texture_mode = 0 

void set_texture_mode(value: TextureMode)

TextureMode get_texture_mode()

The format the texture should be generated with. When passing a CurveTexture as an input to a Shader, this may need to be adjusted.

void set_width(value: int)

The width of the texture (in pixels). Higher values make it possible to represent high-frequency data better (such as sudden direction changes), at the cost of increased generation time and memory usage.

Please read the User-contributed notes policy before submitting a comment.

---

## CurveXYZTexture

**URL:** https://docs.godotengine.org/en/stable/classes/class_curvexyztexture.html

**Contents:**
- CurveXYZTexture
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: Texture2D < Texture < Resource < RefCounted < Object

A 1D texture where the red, green, and blue color channels correspond to points on 3 curves.

A 1D texture where the red, green, and blue color channels correspond to points on 3 unit Curve resources. Compared to using separate CurveTextures, this further simplifies the task of saving curves as image files.

If you only need to store one curve within a single texture, use CurveTexture instead. See also GradientTexture1D and GradientTexture2D.

resource_local_to_scene

false (overrides Resource)

void set_curve_x(value: Curve)

The Curve that is rendered onto the texture's red channel. Should be a unit Curve.

void set_curve_y(value: Curve)

The Curve that is rendered onto the texture's green channel. Should be a unit Curve.

void set_curve_z(value: Curve)

The Curve that is rendered onto the texture's blue channel. Should be a unit Curve.

void set_width(value: int)

The width of the texture (in pixels). Higher values make it possible to represent high-frequency data better (such as sudden direction changes), at the cost of increased generation time and memory usage.

Please read the User-contributed notes policy before submitting a comment.

---

## FileAccess

**URL:** https://docs.godotengine.org/en/stable/classes/class_fileaccess.html

**Contents:**
- FileAccess
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Provides methods for file reading and writing operations.

This class can be used to permanently store data in the user device's file system and to read from it. This is useful for storing game save data or player configuration files.

Example: How to write and read from a file. The file named "save_game.dat" will be stored in the user data folder, as specified in the Data paths documentation:

A FileAccess instance has its own file cursor, which is the position in bytes in the file where the next read/write operation will occur. Functions such as get_8(), get_16(), store_8(), and store_16() will move the file cursor forward by the number of bytes read/written. The file cursor can be moved to a specific position using seek() or seek_end(), and its position can be retrieved using get_position().

A FileAccess instance will close its file when the instance is freed. Since it inherits RefCounted, this happens automatically when it is no longer in use. close() can be called to close it earlier. In C#, the reference must be disposed manually, which can be done with the using statement or by calling the Dispose method directly.

Note: To access project resources once exported, it is recommended to use ResourceLoader instead of FileAccess, as some files are converted to engine-specific formats and their original source files might not be present in the exported PCK package. If using FileAccess, make sure the file is included in the export by changing its import mode to Keep File (exported as is) in the Import dock, or, for files where this option is not available, change the non-resource export filter in the Export dialog to include the file's extension (e.g. *.txt).

Note: Files are automatically closed only if the process exits "normally" (such as by clicking the window manager's close button or pressing Alt + F4). If you stop the project execution by pressing F8 while the project is running, the file won't be closed as the game process will be killed. You can work around this by calling flush() at regular intervals.

Runtime file loading and saving

Binary serialization API

create_temp(mode_flags: int, prefix: String = "", extension: String = "", keep: bool = false) static

file_exists(path: String) static

get_access_time(file: String) static

get_as_text(skip_cr: bool = false) const

get_buffer(length: int) const

get_csv_line(delim: String = ",") const

get_file_as_bytes(path: String) static

get_file_as_string(path: String) static

get_hidden_attribute(file: String) static

get_md5(path: String) static

get_modified_time(file: String) static

get_open_error() static

get_path_absolute() const

get_read_only_attribute(file: String) static

get_sha256(path: String) static

get_size(file: String) static

BitField[UnixPermissionFlags]

get_unix_permissions(file: String) static

get_var(allow_objects: bool = false) const

open(path: String, flags: ModeFlags) static

open_compressed(path: String, mode_flags: ModeFlags, compression_mode: CompressionMode = 0) static

open_encrypted(path: String, mode_flags: ModeFlags, key: PackedByteArray, iv: PackedByteArray = PackedByteArray()) static

open_encrypted_with_pass(path: String, mode_flags: ModeFlags, pass: String) static

seek_end(position: int = 0)

set_hidden_attribute(file: String, hidden: bool) static

set_read_only_attribute(file: String, ro: bool) static

set_unix_permissions(file: String, permissions: BitField[UnixPermissionFlags]) static

store_buffer(buffer: PackedByteArray)

store_csv_line(values: PackedStringArray, delim: String = ",")

store_double(value: float)

store_float(value: float)

store_half(value: float)

store_line(line: String)

store_pascal_string(string: String)

store_real(value: float)

store_string(string: String)

store_var(value: Variant, full_objects: bool = false)

Opens the file for read operations. The file cursor is positioned at the beginning of the file.

Opens the file for write operations. The file is created if it does not exist, and truncated if it does.

Note: When creating a file it must be in an already existing directory. To recursively create directories for a file path, see DirAccess.make_dir_recursive().

ModeFlags READ_WRITE = 3

Opens the file for read and write operations. Does not truncate the file. The file cursor is positioned at the beginning of the file.

ModeFlags WRITE_READ = 7

Opens the file for read and write operations. The file is created if it does not exist, and truncated if it does. The file cursor is positioned at the beginning of the file.

Note: When creating a file it must be in an already existing directory. To recursively create directories for a file path, see DirAccess.make_dir_recursive().

enum CompressionMode: 

CompressionMode COMPRESSION_FASTLZ = 0

Uses the FastLZ compression method.

CompressionMode COMPRESSION_DEFLATE = 1

Uses the DEFLATE compression method.

CompressionMode COMPRESSION_ZSTD = 2

Uses the Zstandard compression method.

CompressionMode COMPRESSION_GZIP = 3

Uses the gzip compression method.

CompressionMode COMPRESSION_BROTLI = 4

Uses the brotli compression method (only decompression is supported).

flags UnixPermissionFlags: 

UnixPermissionFlags UNIX_READ_OWNER = 256

UnixPermissionFlags UNIX_WRITE_OWNER = 128

UnixPermissionFlags UNIX_EXECUTE_OWNER = 64

Execute for owner bit.

UnixPermissionFlags UNIX_READ_GROUP = 32

UnixPermissionFlags UNIX_WRITE_GROUP = 16

UnixPermissionFlags UNIX_EXECUTE_GROUP = 8

Execute for group bit.

UnixPermissionFlags UNIX_READ_OTHER = 4

UnixPermissionFlags UNIX_WRITE_OTHER = 2

UnixPermissionFlags UNIX_EXECUTE_OTHER = 1

Execute for other bit.

UnixPermissionFlags UNIX_SET_USER_ID = 2048

Set user id on execution bit.

UnixPermissionFlags UNIX_SET_GROUP_ID = 1024

Set group id on execution bit.

UnixPermissionFlags UNIX_RESTRICTED_DELETE = 512

Restricted deletion (sticky) bit.

void set_big_endian(value: bool)

If true, the file is read with big-endian endianness. If false, the file is read with little-endian endianness. If in doubt, leave this to false as most files are written with little-endian endianness.

Note: This is always reset to system endianness, which is little-endian on all supported platforms, whenever you open the file. Therefore, you must set big_endian after opening the file, not before.

Closes the currently opened file and prevents subsequent read/write operations. Use flush() to persist the data to disk without closing the file.

Note: FileAccess will automatically close when it's freed, which happens when it goes out of scope or when it gets assigned with null. In C# the reference must be disposed after we are done using it, this can be done with the using statement or calling the Dispose method directly.

FileAccess create_temp(mode_flags: int, prefix: String = "", extension: String = "", keep: bool = false) static 

Creates a temporary file. This file will be freed when the returned FileAccess is freed.

If prefix is not empty, it will be prefixed to the file name, separated by a -.

If extension is not empty, it will be appended to the temporary file name.

If keep is true, the file is not deleted when the returned FileAccess is freed.

Returns null if opening the file failed. You can use get_open_error() to check the error that occurred.

bool eof_reached() const 

Returns true if the file cursor has already read past the end of the file.

Note: eof_reached() == false cannot be used to check whether there is more data available. To loop while there is more data available, use:

bool file_exists(path: String) static 

Returns true if the file exists in the given path.

Note: Many resources types are imported (e.g. textures or sound files), and their source asset will not be included in the exported game, as only the imported version is used. See ResourceLoader.exists() for an alternative approach that takes resource remapping into account.

For a non-static, relative equivalent, use DirAccess.file_exists().

Writes the file's buffer to disk. Flushing is automatically performed when the file is closed. This means you don't need to call flush() manually before closing a file. Still, calling flush() can be used to ensure the data is safe even if the project crashes instead of being closed gracefully.

Note: Only call flush() when you actually need it. Otherwise, it will decrease performance due to constant disk writes.

Returns the next 8 bits from the file as an integer. This advances the file cursor by 1 byte. See store_8() for details on what values can be stored and retrieved this way.

Returns the next 16 bits from the file as an integer. This advances the file cursor by 2 bytes. See store_16() for details on what values can be stored and retrieved this way.

Returns the next 32 bits from the file as an integer. This advances the file cursor by 4 bytes. See store_32() for details on what values can be stored and retrieved this way.

Returns the next 64 bits from the file as an integer. This advances the file cursor by 8 bytes. See store_64() for details on what values can be stored and retrieved this way.

int get_access_time(file: String) static 

Returns the last time the file was accessed in Unix timestamp format, or 0 on error. This Unix timestamp can be converted to another format using the Time singleton.

String get_as_text(skip_cr: bool = false) const 

Returns the whole file as a String. Text is interpreted as being UTF-8 encoded. This ignores the file cursor and does not affect it.

If skip_cr is true, carriage return characters (\r, CR) will be ignored when parsing the UTF-8, so that only line feed characters (\n, LF) represent a new line (Unix convention).

PackedByteArray get_buffer(length: int) const 

Returns next length bytes of the file as a PackedByteArray. This advances the file cursor by length bytes.

PackedStringArray get_csv_line(delim: String = ",") const 

Returns the next value of the file in CSV (Comma-Separated Values) format. You can pass a different delimiter delim to use other than the default "," (comma). This delimiter must be one-character long, and cannot be a double quotation mark.

Text is interpreted as being UTF-8 encoded. Text values must be enclosed in double quotes if they include the delimiter character. Double quotes within a text value can be escaped by doubling their occurrence. This advances the file cursor to after the newline character at the end of the line.

For example, the following CSV lines are valid and will be properly parsed as two strings each:

Note how the second line can omit the enclosing quotes as it does not include the delimiter. However it could very well use quotes, it was only written without for demonstration purposes. The third line must use "" for each quotation mark that needs to be interpreted as such instead of the end of a text value.

float get_double() const 

Returns the next 64 bits from the file as a floating-point number. This advances the file cursor by 8 bytes.

Error get_error() const 

Returns the last error that happened when trying to perform operations. Compare with the ERR_FILE_* constants from Error.

PackedByteArray get_file_as_bytes(path: String) static 

Returns the whole path file contents as a PackedByteArray without any decoding.

Returns an empty PackedByteArray if an error occurred while opening the file. You can use get_open_error() to check the error that occurred.

String get_file_as_string(path: String) static 

Returns the whole path file contents as a String. Text is interpreted as being UTF-8 encoded.

Returns an empty String if an error occurred while opening the file. You can use get_open_error() to check the error that occurred.

float get_float() const 

Returns the next 32 bits from the file as a floating-point number. This advances the file cursor by 4 bytes.

float get_half() const 

Returns the next 16 bits from the file as a half-precision floating-point number. This advances the file cursor by 2 bytes.

bool get_hidden_attribute(file: String) static 

Returns true, if file hidden attribute is set.

Note: This method is implemented on iOS, BSD, macOS, and Windows.

int get_length() const 

Returns the size of the file in bytes. For a pipe, returns the number of bytes available for reading from the pipe.

String get_line() const 

Returns the next line of the file as a String. The returned string doesn't include newline (\n) or carriage return (\r) characters, but does include any other leading or trailing whitespace. This advances the file cursor to after the newline character at the end of the line.

Text is interpreted as being UTF-8 encoded.

String get_md5(path: String) static 

Returns an MD5 String representing the file at the given path or an empty String on failure.

int get_modified_time(file: String) static 

Returns the last time the file was modified in Unix timestamp format, or 0 on error. This Unix timestamp can be converted to another format using the Time singleton.

Error get_open_error() static 

Returns the result of the last open() call in the current thread.

String get_pascal_string() 

Returns a String saved in Pascal format from the file, meaning that the length of the string is explicitly stored at the start. See store_pascal_string(). This may include newline characters. The file cursor is advanced after the bytes read.

Text is interpreted as being UTF-8 encoded.

String get_path() const 

Returns the path as a String for the current open file.

String get_path_absolute() const 

Returns the absolute path as a String for the current open file.

int get_position() const 

Returns the file cursor's position in bytes from the beginning of the file. This is the file reading/writing cursor set by seek() or seek_end() and advanced by read/write operations.

bool get_read_only_attribute(file: String) static 

Returns true, if file read only attribute is set.

Note: This method is implemented on iOS, BSD, macOS, and Windows.

float get_real() const 

Returns the next bits from the file as a floating-point number. This advances the file cursor by either 4 or 8 bytes, depending on the precision used by the Godot build that saved the file.

If the file was saved by a Godot build compiled with the precision=single option (the default), the number of read bits for that file is 32. Otherwise, if compiled with the precision=double option, the number of read bits is 64.

String get_sha256(path: String) static 

Returns an SHA-256 String representing the file at the given path or an empty String on failure.

int get_size(file: String) static 

Returns file size in bytes, or -1 on error.

BitField[UnixPermissionFlags] get_unix_permissions(file: String) static 

Returns file UNIX permissions.

Note: This method is implemented on iOS, Linux/BSD, and macOS.

Variant get_var(allow_objects: bool = false) const 

Returns the next Variant value from the file. If allow_objects is true, decoding objects is allowed. This advances the file cursor by the number of bytes read.

Internally, this uses the same decoding mechanism as the @GlobalScope.bytes_to_var() method, as described in the Binary serialization API documentation.

Warning: Deserialized objects can contain code which gets executed. Do not use this option if the serialized object comes from untrusted sources to avoid potential security threats such as remote code execution.

bool is_open() const 

Returns true if the file is currently opened.

FileAccess open(path: String, flags: ModeFlags) static 

Creates a new FileAccess object and opens the file for writing or reading, depending on the flags.

Returns null if opening the file failed. You can use get_open_error() to check the error that occurred.

FileAccess open_compressed(path: String, mode_flags: ModeFlags, compression_mode: CompressionMode = 0) static 

Creates a new FileAccess object and opens a compressed file for reading or writing.

Note: open_compressed() can only read files that were saved by Godot, not third-party compression formats. See GitHub issue #28999 for a workaround.

Returns null if opening the file failed. You can use get_open_error() to check the error that occurred.

FileAccess open_encrypted(path: String, mode_flags: ModeFlags, key: PackedByteArray, iv: PackedByteArray = PackedByteArray()) static 

Creates a new FileAccess object and opens an encrypted file in write or read mode. You need to pass a binary key to encrypt/decrypt it.

Note: The provided key must be 32 bytes long.

Returns null if opening the file failed. You can use get_open_error() to check the error that occurred.

FileAccess open_encrypted_with_pass(path: String, mode_flags: ModeFlags, pass: String) static 

Creates a new FileAccess object and opens an encrypted file in write or read mode. You need to pass a password to encrypt/decrypt it.

Returns null if opening the file failed. You can use get_open_error() to check the error that occurred.

Error resize(length: int) 

Resizes the file to a specified length. The file must be open in a mode that permits writing. If the file is extended, NUL characters are appended. If the file is truncated, all data from the end file to the original length of the file is lost.

void seek(position: int) 

Changes the file reading/writing cursor to the specified position (in bytes from the beginning of the file). This changes the value returned by get_position().

void seek_end(position: int = 0) 

Changes the file reading/writing cursor to the specified position (in bytes from the end of the file). This changes the value returned by get_position().

Note: This is an offset, so you should use negative numbers or the file cursor will be at the end of the file.

Error set_hidden_attribute(file: String, hidden: bool) static 

Sets file hidden attribute.

Note: This method is implemented on iOS, BSD, macOS, and Windows.

Error set_read_only_attribute(file: String, ro: bool) static 

Sets file read only attribute.

Note: This method is implemented on iOS, BSD, macOS, and Windows.

Error set_unix_permissions(file: String, permissions: BitField[UnixPermissionFlags]) static 

Sets file UNIX permissions.

Note: This method is implemented on iOS, Linux/BSD, and macOS.

bool store_8(value: int) 

Stores an integer as 8 bits in the file. This advances the file cursor by 1 byte. Returns true if the operation is successful.

Note: The value should lie in the interval [0, 255]. Any other value will overflow and wrap around.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

To store a signed integer, use store_64(), or convert it manually (see store_16() for an example).

bool store_16(value: int) 

Stores an integer as 16 bits in the file. This advances the file cursor by 2 bytes. Returns true if the operation is successful.

Note: The value should lie in the interval [0, 2^16 - 1]. Any other value will overflow and wrap around.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

To store a signed integer, use store_64() or store a signed integer from the interval [-2^15, 2^15 - 1] (i.e. keeping one bit for the signedness) and compute its sign manually when reading. For example:

bool store_32(value: int) 

Stores an integer as 32 bits in the file. This advances the file cursor by 4 bytes. Returns true if the operation is successful.

Note: The value should lie in the interval [0, 2^32 - 1]. Any other value will overflow and wrap around.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

To store a signed integer, use store_64(), or convert it manually (see store_16() for an example).

bool store_64(value: int) 

Stores an integer as 64 bits in the file. This advances the file cursor by 8 bytes. Returns true if the operation is successful.

Note: The value must lie in the interval [-2^63, 2^63 - 1] (i.e. be a valid int value).

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

bool store_buffer(buffer: PackedByteArray) 

Stores the given array of bytes in the file. This advances the file cursor by the number of bytes written. Returns true if the operation is successful.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

bool store_csv_line(values: PackedStringArray, delim: String = ",") 

Store the given PackedStringArray in the file as a line formatted in the CSV (Comma-Separated Values) format. You can pass a different delimiter delim to use other than the default "," (comma). This delimiter must be one-character long.

Text will be encoded as UTF-8. Returns true if the operation is successful.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

bool store_double(value: float) 

Stores a floating-point number as 64 bits in the file. This advances the file cursor by 8 bytes. Returns true if the operation is successful.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

bool store_float(value: float) 

Stores a floating-point number as 32 bits in the file. This advances the file cursor by 4 bytes. Returns true if the operation is successful.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

bool store_half(value: float) 

Stores a half-precision floating-point number as 16 bits in the file. This advances the file cursor by 2 bytes. Returns true if the operation is successful.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

bool store_line(line: String) 

Stores line in the file followed by a newline character (\n), encoding the text as UTF-8. This advances the file cursor by the length of the line, after the newline character. The amount of bytes written depends on the UTF-8 encoded bytes, which may be different from String.length() which counts the number of UTF-32 codepoints. Returns true if the operation is successful.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

bool store_pascal_string(string: String) 

Stores the given String as a line in the file in Pascal format (i.e. also store the length of the string). Text will be encoded as UTF-8. This advances the file cursor by the number of bytes written depending on the UTF-8 encoded bytes, which may be different from String.length() which counts the number of UTF-32 codepoints. Returns true if the operation is successful.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

bool store_real(value: float) 

Stores a floating-point number in the file. This advances the file cursor by either 4 or 8 bytes, depending on the precision used by the current Godot build.

If using a Godot build compiled with the precision=single option (the default), this method will save a 32-bit float. Otherwise, if compiled with the precision=double option, this will save a 64-bit float. Returns true if the operation is successful.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

bool store_string(string: String) 

Stores string in the file without a newline character (\n), encoding the text as UTF-8. This advances the file cursor by the length of the string in UTF-8 encoded bytes, which may be different from String.length() which counts the number of UTF-32 codepoints. Returns true if the operation is successful.

Note: This method is intended to be used to write text files. The string is stored as a UTF-8 encoded buffer without string length or terminating zero, which means that it can't be loaded back easily. If you want to store a retrievable string in a binary file, consider using store_pascal_string() instead. For retrieving strings from a text file, you can use get_buffer(length).get_string_from_utf8() (if you know the length) or get_as_text().

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

bool store_var(value: Variant, full_objects: bool = false) 

Stores any Variant value in the file. If full_objects is true, encoding objects is allowed (and can potentially include code). This advances the file cursor by the number of bytes written. Returns true if the operation is successful.

Internally, this uses the same encoding mechanism as the @GlobalScope.var_to_bytes() method, as described in the Binary serialization API documentation.

Note: Not all properties are included. Only properties that are configured with the @GlobalScope.PROPERTY_USAGE_STORAGE flag set will be serialized. You can add a new usage flag to a property by overriding the Object._get_property_list() method in your class. You can also check how property usage is configured by calling Object._get_property_list(). See PropertyUsageFlags for the possible usage flags.

Note: If an error occurs, the resulting value of the file position indicator is indeterminate.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func save_to_file(content):
    var file = FileAccess.open("user://save_game.dat", FileAccess.WRITE)
    file.store_string(content)

func load_from_file():
    var file = FileAccess.open("user://save_game.dat", FileAccess.READ)
    var content = file.get_as_text()
    return content
```

Example 2 (csharp):
```csharp
public void SaveToFile(string content)
{
    using var file = FileAccess.Open("user://save_game.dat", FileAccess.ModeFlags.Write);
    file.StoreString(content);
}

public string LoadFromFile()
{
    using var file = FileAccess.Open("user://save_game.dat", FileAccess.ModeFlags.Read);
    string content = file.GetAsText();
    return content;
}
```

Example 3 (unknown):
```unknown
while file.get_position() < file.get_length():
    # Read data
```

Example 4 (json):
```json
while (file.GetPosition() < file.GetLength())
{
    // Read data
}
```

---

## FileDialog

**URL:** https://docs.godotengine.org/en/stable/classes/class_filedialog.html

**Contents:**
- FileDialog
- Description
- Properties
- Methods
- Theme Properties
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- Theme Property Descriptions

Inherits: ConfirmationDialog < AcceptDialog < Window < Viewport < Node < Object

A dialog for selecting files or directories in the filesystem.

FileDialog is a preset dialog used to choose files and directories in the filesystem. It supports filter masks. FileDialog automatically sets its window title according to the file_mode. If you want to use a custom title, disable this by setting mode_overrides_title to false.

false (overrides AcceptDialog)

file_filter_toggle_enabled

file_sort_options_enabled

folder_creation_enabled

hidden_files_toggle_enabled

layout_toggle_enabled

Vector2i(640, 360) (overrides Window)

"Save a File" (overrides Window)

add_filter(filter: String, description: String = "")

add_option(name: String, values: PackedStringArray, default_value_index: int)

clear_filename_filter()

get_option_default(option: int) const

get_option_name(option: int) const

get_option_values(option: int) const

get_selected_options() const

is_customization_flag_enabled(flag: Customization) const

set_customization_flag_enabled(flag: Customization, enabled: bool)

set_option_default(option: int, default_value_index: int)

set_option_name(option: int, name: String)

set_option_values(option: int, values: PackedStringArray)

toggle_filename_filter

dir_selected(dir: String) 

Emitted when the user selects a directory.

file_selected(path: String) 

Emitted when the user selects a file by double-clicking it or pressing the OK button.

filename_filter_changed(filter: String) 

Emitted when the filter for file names changes.

files_selected(paths: PackedStringArray) 

Emitted when the user selects multiple files.

FileMode FILE_MODE_OPEN_FILE = 0

The dialog allows selecting one, and only one file.

FileMode FILE_MODE_OPEN_FILES = 1

The dialog allows selecting multiple files.

FileMode FILE_MODE_OPEN_DIR = 2

The dialog only allows selecting a directory, disallowing the selection of any file.

FileMode FILE_MODE_OPEN_ANY = 3

The dialog allows selecting one file or directory.

FileMode FILE_MODE_SAVE_FILE = 4

The dialog will warn when a file exists.

Access ACCESS_RESOURCES = 0

The dialog only allows accessing files under the Resource path (res://).

Access ACCESS_USERDATA = 1

The dialog only allows accessing files under user data path (user://).

Access ACCESS_FILESYSTEM = 2

The dialog allows accessing files on the whole file system.

DisplayMode DISPLAY_THUMBNAILS = 0

The dialog displays files as a grid of thumbnails. Use thumbnail_size to adjust their size.

DisplayMode DISPLAY_LIST = 1

The dialog displays files as a list of filenames.

enum Customization: 

Customization CUSTOMIZATION_HIDDEN_FILES = 0

Toggles visibility of the favorite button, and the favorite list on the left side of the dialog.

Equivalent to hidden_files_toggle_enabled.

Customization CUSTOMIZATION_CREATE_FOLDER = 1

If enabled, shows the button for creating new directories (when using FILE_MODE_OPEN_DIR, FILE_MODE_OPEN_ANY, or FILE_MODE_SAVE_FILE).

Equivalent to folder_creation_enabled.

Customization CUSTOMIZATION_FILE_FILTER = 2

If enabled, shows the toggle file filter button.

Equivalent to file_filter_toggle_enabled.

Customization CUSTOMIZATION_FILE_SORT = 3

If enabled, shows the file sorting options button.

Equivalent to file_sort_options_enabled.

Customization CUSTOMIZATION_FAVORITES = 4

If enabled, shows the toggle favorite button and favorite list on the left side of the dialog.

Equivalent to favorites_enabled.

Customization CUSTOMIZATION_RECENT = 5

If enabled, shows the recent directories list on the left side of the dialog.

Equivalent to recent_list_enabled.

Customization CUSTOMIZATION_LAYOUT = 6

If enabled, shows the layout switch buttons (list/thumbnails).

Equivalent to layout_toggle_enabled.

void set_access(value: Access)

The file system access scope.

Warning: In Web builds, FileDialog cannot access the host file system. In sandboxed Linux and macOS environments, use_native_dialog is automatically used to allow limited access to host file system.

void set_current_dir(value: String)

String get_current_dir()

The current working directory of the file dialog.

Note: For native file dialogs, this property is only treated as a hint and may not be respected by specific OS implementations.

String current_file 

void set_current_file(value: String)

String get_current_file()

The currently selected file of the file dialog.

String current_path 

void set_current_path(value: String)

String get_current_path()

The currently selected file path of the file dialog.

DisplayMode display_mode = 0 

void set_display_mode(value: DisplayMode)

DisplayMode get_display_mode()

Display mode of the dialog's file list.

bool favorites_enabled = true 

void set_customization_flag_enabled(flag: Customization, enabled: bool)

bool is_customization_flag_enabled(flag: Customization) const

If true, shows the toggle favorite button and favorite list on the left side of the dialog.

bool file_filter_toggle_enabled = true 

void set_customization_flag_enabled(flag: Customization, enabled: bool)

bool is_customization_flag_enabled(flag: Customization) const

If true, shows the toggle file filter button.

FileMode file_mode = 4 

void set_file_mode(value: FileMode)

FileMode get_file_mode()

The dialog's open or save mode, which affects the selection behavior.

bool file_sort_options_enabled = true 

void set_customization_flag_enabled(flag: Customization, enabled: bool)

bool is_customization_flag_enabled(flag: Customization) const

If true, shows the file sorting options button.

String filename_filter = "" 

void set_filename_filter(value: String)

String get_filename_filter()

The filter for file names (case-insensitive). When set to a non-empty string, only files that contains the substring will be shown. filename_filter can be edited by the user with the filter button at the top of the file dialog.

See also filters, which should be used to restrict the file types that can be selected instead of filename_filter which is meant to be set by the user.

PackedStringArray filters = PackedStringArray() 

void set_filters(value: PackedStringArray)

PackedStringArray get_filters()

The available file type filters. Each filter string in the array should be formatted like this: *.png,*.jpg,*.jpeg;Image Files;image/png,image/jpeg. The description text of the filter is optional and can be omitted. Both file extensions and MIME type should be always set.

Note: Embedded file dialog and Windows file dialog support only file extensions, while Android, Linux, and macOS file dialogs also support MIME types.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedStringArray for more details.

bool folder_creation_enabled = true 

void set_customization_flag_enabled(flag: Customization, enabled: bool)

bool is_customization_flag_enabled(flag: Customization) const

If true, shows the button for creating new directories (when using FILE_MODE_OPEN_DIR, FILE_MODE_OPEN_ANY, or FILE_MODE_SAVE_FILE).

bool hidden_files_toggle_enabled = true 

void set_customization_flag_enabled(flag: Customization, enabled: bool)

bool is_customization_flag_enabled(flag: Customization) const

If true, shows the toggle hidden files button.

bool layout_toggle_enabled = true 

void set_customization_flag_enabled(flag: Customization, enabled: bool)

bool is_customization_flag_enabled(flag: Customization) const

If true, shows the layout switch buttons (list/thumbnails).

bool mode_overrides_title = true 

void set_mode_overrides_title(value: bool)

bool is_mode_overriding_title()

If true, changing the file_mode property will set the window title accordingly (e.g. setting file_mode to FILE_MODE_OPEN_FILE will change the window title to "Open a File").

int option_count = 0 

void set_option_count(value: int)

int get_option_count()

The number of additional OptionButtons and CheckBoxes in the dialog.

bool recent_list_enabled = true 

void set_customization_flag_enabled(flag: Customization, enabled: bool)

bool is_customization_flag_enabled(flag: Customization) const

If true, shows the recent directories list on the left side of the dialog.

String root_subfolder = "" 

void set_root_subfolder(value: String)

String get_root_subfolder()

If non-empty, the given sub-folder will be "root" of this FileDialog, i.e. user won't be able to go to its parent directory.

Note: This property is ignored by native file dialogs.

bool show_hidden_files = false 

void set_show_hidden_files(value: bool)

bool is_showing_hidden_files()

If true, the dialog will show hidden files.

Note: This property is ignored by native file dialogs on Android and Linux.

bool use_native_dialog = false 

void set_use_native_dialog(value: bool)

bool get_use_native_dialog()

If true, and if supported by the current DisplayServer, OS native dialog will be used instead of custom one.

Note: On Android, it is only supported for Android 10+ devices and when using ACCESS_FILESYSTEM. For access mode ACCESS_RESOURCES and ACCESS_USERDATA, the system will fall back to custom FileDialog.

Note: On Linux and macOS, sandboxed apps always use native dialogs to access the host file system.

Note: On macOS, sandboxed apps will save security-scoped bookmarks to retain access to the opened folders across multiple sessions. Use OS.get_granted_permissions() to get a list of saved bookmarks.

Note: Native dialogs are isolated from the base process, file dialog properties can't be modified once the dialog is shown.

void add_filter(filter: String, description: String = "") 

Adds a comma-separated file name filter option to the FileDialog with an optional description, which restricts what files can be picked.

A filter should be of the form "filename.extension", where filename and extension can be * to match any string. Filters starting with . (i.e. empty filenames) are not allowed.

For example, a filter of "*.png, *.jpg" and a description of "Images" results in filter text "Images (*.png, *.jpg)".

void add_option(name: String, values: PackedStringArray, default_value_index: int) 

Adds an additional OptionButton to the file dialog. If values is empty, a CheckBox is added instead.

default_value_index should be an index of the value in the values. If values is empty it should be either 1 (checked), or 0 (unchecked).

void clear_filename_filter() 

Clear the filter for file names.

void clear_filters() 

Clear all the added filters in the dialog.

void deselect_all() 

Clear all currently selected items in the dialog.

LineEdit get_line_edit() 

Returns the LineEdit for the selected file.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their CanvasItem.visible property.

int get_option_default(option: int) const 

Returns the default value index of the OptionButton or CheckBox with index option.

String get_option_name(option: int) const 

Returns the name of the OptionButton or CheckBox with index option.

PackedStringArray get_option_values(option: int) const 

Returns an array of values of the OptionButton with index option.

Dictionary get_selected_options() const 

Returns a Dictionary with the selected values of the additional OptionButtons and/or CheckBoxes. Dictionary keys are names and values are selected value indices.

VBoxContainer get_vbox() 

Returns the vertical box container of the dialog, custom controls can be added to it.

Warning: This is a required internal node, removing and freeing it may cause a crash. If you wish to hide it or any of its children, use their CanvasItem.visible property.

Note: Changes to this node are ignored by native file dialogs, use add_option() to add custom elements to the dialog instead.

Invalidate and update the current dialog content list.

Note: This method does nothing on native file dialogs.

bool is_customization_flag_enabled(flag: Customization) const 

Returns true if the provided flag is enabled.

void set_customization_flag_enabled(flag: Customization, enabled: bool) 

Toggles the specified customization flag, allowing to customize features available in this FileDialog. See Customization for options.

void set_option_default(option: int, default_value_index: int) 

Sets the default value index of the OptionButton or CheckBox with index option.

void set_option_name(option: int, name: String) 

Sets the name of the OptionButton or CheckBox with index option.

void set_option_values(option: int, values: PackedStringArray) 

Sets the option values of the OptionButton with index option.

Color file_disabled_color = Color(1, 1, 1, 0.25) 

The color tint for disabled files (when the FileDialog is used in open folder mode).

Color file_icon_color = Color(1, 1, 1, 1) 

The color modulation applied to the file icon.

Color folder_icon_color = Color(1, 1, 1, 1) 

The color modulation applied to the folder icon.

int thumbnail_size = 64 

The size of thumbnail icons when DISPLAY_THUMBNAILS is enabled.

Texture2D back_folder 

Custom icon for the back arrow.

Texture2D create_folder 

Custom icon for the create folder button.

Custom icon for favorite folder button.

Texture2D favorite_down 

Custom icon for button to move down a favorite entry.

Texture2D favorite_up 

Custom icon for button to move up a favorite entry.

Custom icon for files.

Texture2D file_thumbnail 

Icon for files when in thumbnail mode.

Custom icon for folders.

Texture2D folder_thumbnail 

Icon for folders when in thumbnail mode.

Texture2D forward_folder 

Custom icon for the forward arrow.

Texture2D list_mode 

Icon for the button that enables list mode.

Texture2D parent_folder 

Custom icon for the parent folder arrow.

Custom icon for the reload button.

Custom icon for the sorting options menu.

Texture2D thumbnail_mode 

Icon for the button that enables thumbnail mode.

Texture2D toggle_filename_filter 

Custom icon for the toggle button for the filter for file names.

Texture2D toggle_hidden 

Custom icon for the toggle hidden button.

Please read the User-contributed notes policy before submitting a comment.

---

## File paths in Godot projects

**URL:** https://docs.godotengine.org/en/stable/tutorials/io/data_paths.html

**Contents:**
- File paths in Godot projects
- Path separators
- Accessing files in the project folder (res://)
- Accessing persistent user data (user://)
- File logging
- Converting paths to absolute paths or "local" paths
- Editor data paths
  - Self-contained mode
- User-contributed notes

This page explains how file paths work inside Godot projects. You will learn how to access paths in your projects using the res:// and user:// notations, and where Godot stores project and editor files on your and your users' systems.

To make supporting multiple platforms easier, Godot uses UNIX-style path separators (forward slash /). These work on all platforms, including Windows.

Instead of writing paths like C:\Projects\Game, in Godot, you should write C:/Projects/Game.

Windows-style path separators (backward slash \) are also supported in some path-related methods, but they need to be doubled (\\), as \ is normally used as an escape for characters with a special meaning.

This makes it possible to work with paths returned by other Windows applications. We still recommend using only forward slashes in your own code to guarantee that everything will work as intended.

The String class offers over a dozen methods to work with strings that represent file paths:

String.filecasecmp_to()

String.filenocasecmp_to()

String.get_base_dir()

String.get_basename()

String.get_extension()

String.is_absolute_path()

String.is_relative_path()

String.is_valid_filename()

String.simplify_path()

String.validate_filename()

Godot considers that a project exists in any folder that contains a project.godot text file, even if the file is empty. The folder that contains this file is your project's root folder.

You can access any file relative to it by writing paths starting with res://, which stands for resources. For example, you can access an image file character.png located in the project's root folder in code with the following path: res://character.png.

To store persistent data files, like the player's save or settings, you want to use user:// instead of res:// as your path's prefix. This is because when the game is running, the project's file system will likely be read-only.

The user:// prefix points to a different directory on the user's device. Unlike res://, the directory pointed at by user:// is created automatically and guaranteed to be writable to, even in an exported project.

The location of the user:// folder depends on what is configured in the Project Settings:

By default, the user:// folder is created within Godot's editor data path in the app_userdata/[project_name] folder. This is the default so that prototypes and test projects stay self-contained within Godot's data folder.

If application/config/use_custom_user_dir is enabled in the Project Settings, the user:// folder is created next to Godot's editor data path, i.e. in the standard location for applications data.

By default, the folder name will be inferred from the project name, but it can be further customized with application/config/custom_user_dir_name. This path can contain path separators, so you can use it e.g. to group projects of a given studio with a Studio Name/Game Name structure.

On desktop platforms, the actual directory paths for user:// are:

[project_name] is based on the application name defined in the Project Settings, but you can override it on a per-platform basis using feature tags.

On mobile platforms, this path is unique to the project and is not accessible by other applications for security reasons.

On HTML5 exports, user:// will refer to a virtual filesystem stored on the device via IndexedDB. (Interaction with the main filesystem can still be performed through the JavaScriptBridge singleton.)

Documentation on file logging has been moved to Logging.

You can use ProjectSettings.globalize_path() to convert a "local" path like res://path/to/file.txt to an absolute OS path. For example, ProjectSettings.globalize_path() can be used to open "local" paths in the OS file manager using OS.shell_open() since it only accepts native OS paths.

To convert an absolute OS path to a "local" path starting with res:// or user://, use ProjectSettings.localize_path(). This only works for absolute paths that point to files or folders in your project's root or user:// folders.

The editor uses different paths for editor data, editor settings, and cache, depending on the platform. By default, these paths are:

Editor data contains export templates and project-specific data.

Editor settings contains the main editor settings configuration file as well as various other user-specific customizations (editor layouts, feature profiles, script templates, etc.).

Cache contains data generated by the editor, or stored temporarily. It can safely be removed when Godot is closed.

Godot complies with the XDG Base Directory Specification on Linux/*BSD. You can override the XDG_DATA_HOME, XDG_CONFIG_HOME and XDG_CACHE_HOME environment variables to change the editor and project data paths.

If you use Godot packaged as a Flatpak, the editor data paths will be located in subfolders in ~/.var/app/org.godotengine.Godot/.

If you create a file called ._sc_ or _sc_ in the same directory as the editor binary (or in MacOS/Contents/ for a macOS editor .app bundle), Godot will enable self-contained mode. This mode makes Godot write all editor data, settings, and cache to a directory named editor_data/ in the same directory as the editor binary. You can use it to create a portable installation of the editor.

The Steam release of Godot uses self-contained mode by default.

Self-contained mode is not supported in exported projects yet. To read and write files relative to the executable path, use OS.get_executable_path(). Note that writing files in the executable path only works if the executable is placed in a writable location (i.e. not Program Files or another directory that is read-only for regular users).

Please read the User-contributed notes policy before submitting a comment.

---

## FontFile

**URL:** https://docs.godotengine.org/en/stable/classes/class_fontfile.html

**Contents:**
- FontFile
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Font < Resource < RefCounted < Object

Holds font source data and prerendered glyph cache, imported from a dynamic or a bitmap font.

FontFile contains a set of glyphs to represent Unicode characters imported from a font file, as well as a cache of rasterized glyphs, and a set of fallback Fonts to use.

Use FontVariation to access specific OpenType variation of the font, create simulated bold / slanted version, and draw lines of text.

For more complex text processing, use FontVariation in conjunction with TextLine or TextParagraph.

Supported font formats:

Dynamic font importer: TrueType (.ttf), TrueType collection (.ttc), OpenType (.otf), OpenType collection (.otc), WOFF (.woff), WOFF2 (.woff2), Type 1 (.pfb, .pfm).

Bitmap font importer: AngelCode BMFont (.fnt, .font), text and binary (version 3) format variants.

Monospace image font importer: All supported image formats.

Note: A character is a symbol that represents an item (letter, digit etc.) in an abstract way.

Note: A glyph is a bitmap or a shape used to draw one or more characters in a context-dependent manner. Glyph indices are bound to the specific font data source.

Note: If none of the font data sources contain glyphs for a character used in a string, the character in question will be replaced with a box displaying its hexadecimal code.

Runtime file loading and saving

allow_system_fallback

disable_embedded_bitmaps

fixed_size_scale_mode

keep_rounding_remainders

modulate_color_glyphs

multichannel_signed_distance_field

opentype_feature_overrides

clear_glyphs(cache_index: int, size: Vector2i)

clear_kerning_map(cache_index: int, size: int)

clear_size_cache(cache_index: int)

clear_textures(cache_index: int, size: Vector2i)

get_cache_ascent(cache_index: int, size: int) const

get_cache_count() const

get_cache_descent(cache_index: int, size: int) const

get_cache_scale(cache_index: int, size: int) const

get_cache_underline_position(cache_index: int, size: int) const

get_cache_underline_thickness(cache_index: int, size: int) const

get_char_from_glyph_index(size: int, glyph_index: int) const

get_embolden(cache_index: int) const

get_extra_baseline_offset(cache_index: int) const

get_extra_spacing(cache_index: int, spacing: SpacingType) const

get_face_index(cache_index: int) const

get_glyph_advance(cache_index: int, size: int, glyph: int) const

get_glyph_index(size: int, char: int, variation_selector: int) const

get_glyph_list(cache_index: int, size: Vector2i) const

get_glyph_offset(cache_index: int, size: Vector2i, glyph: int) const

get_glyph_size(cache_index: int, size: Vector2i, glyph: int) const

get_glyph_texture_idx(cache_index: int, size: Vector2i, glyph: int) const

get_glyph_uv_rect(cache_index: int, size: Vector2i, glyph: int) const

get_kerning(cache_index: int, size: int, glyph_pair: Vector2i) const

get_kerning_list(cache_index: int, size: int) const

get_language_support_override(language: String) const

get_language_support_overrides() const

get_script_support_override(script: String) const

get_script_support_overrides() const

get_size_cache_list(cache_index: int) const

get_texture_count(cache_index: int, size: Vector2i) const

get_texture_image(cache_index: int, size: Vector2i, texture_index: int) const

get_texture_offsets(cache_index: int, size: Vector2i, texture_index: int) const

get_transform(cache_index: int) const

get_variation_coordinates(cache_index: int) const

load_bitmap_font(path: String)

load_dynamic_font(path: String)

remove_cache(cache_index: int)

remove_glyph(cache_index: int, size: Vector2i, glyph: int)

remove_kerning(cache_index: int, size: int, glyph_pair: Vector2i)

remove_language_support_override(language: String)

remove_script_support_override(script: String)

remove_size_cache(cache_index: int, size: Vector2i)

remove_texture(cache_index: int, size: Vector2i, texture_index: int)

render_glyph(cache_index: int, size: Vector2i, index: int)

render_range(cache_index: int, size: Vector2i, start: int, end: int)

set_cache_ascent(cache_index: int, size: int, ascent: float)

set_cache_descent(cache_index: int, size: int, descent: float)

set_cache_scale(cache_index: int, size: int, scale: float)

set_cache_underline_position(cache_index: int, size: int, underline_position: float)

set_cache_underline_thickness(cache_index: int, size: int, underline_thickness: float)

set_embolden(cache_index: int, strength: float)

set_extra_baseline_offset(cache_index: int, baseline_offset: float)

set_extra_spacing(cache_index: int, spacing: SpacingType, value: int)

set_face_index(cache_index: int, face_index: int)

set_glyph_advance(cache_index: int, size: int, glyph: int, advance: Vector2)

set_glyph_offset(cache_index: int, size: Vector2i, glyph: int, offset: Vector2)

set_glyph_size(cache_index: int, size: Vector2i, glyph: int, gl_size: Vector2)

set_glyph_texture_idx(cache_index: int, size: Vector2i, glyph: int, texture_idx: int)

set_glyph_uv_rect(cache_index: int, size: Vector2i, glyph: int, uv_rect: Rect2)

set_kerning(cache_index: int, size: int, glyph_pair: Vector2i, kerning: Vector2)

set_language_support_override(language: String, supported: bool)

set_script_support_override(script: String, supported: bool)

set_texture_image(cache_index: int, size: Vector2i, texture_index: int, image: Image)

set_texture_offsets(cache_index: int, size: Vector2i, texture_index: int, offset: PackedInt32Array)

set_transform(cache_index: int, transform: Transform2D)

set_variation_coordinates(cache_index: int, variation_coordinates: Dictionary)

bool allow_system_fallback = true 

void set_allow_system_fallback(value: bool)

bool is_allow_system_fallback()

If set to true, system fonts can be automatically used as fallbacks.

FontAntialiasing antialiasing = 1 

void set_antialiasing(value: FontAntialiasing)

FontAntialiasing get_antialiasing()

Font anti-aliasing mode.

PackedByteArray data = PackedByteArray() 

void set_data(value: PackedByteArray)

PackedByteArray get_data()

Contents of the dynamic font source file.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedByteArray for more details.

bool disable_embedded_bitmaps = true 

void set_disable_embedded_bitmaps(value: bool)

bool get_disable_embedded_bitmaps()

If set to true, embedded font bitmap loading is disabled (bitmap-only and color fonts ignore this property).

void set_fixed_size(value: int)

Font size, used only for the bitmap fonts.

FixedSizeScaleMode fixed_size_scale_mode = 0 

void set_fixed_size_scale_mode(value: FixedSizeScaleMode)

FixedSizeScaleMode get_fixed_size_scale_mode()

Scaling mode, used only for the bitmap fonts with fixed_size greater than zero.

String font_name = "" 

void set_font_name(value: String)

String get_font_name()

int font_stretch = 100 

void set_font_stretch(value: int)

int get_font_stretch()

Font stretch amount, compared to a normal width. A percentage value between 50% and 200%.

BitField[FontStyle] font_style = 0 

void set_font_style(value: BitField[FontStyle])

BitField[FontStyle] get_font_style()

int font_weight = 400 

void set_font_weight(value: int)

int get_font_weight()

Weight (boldness) of the font. A value in the 100...999 range, normal font weight is 400, bold font weight is 700.

bool force_autohinter = false 

void set_force_autohinter(value: bool)

bool is_force_autohinter()

If set to true, auto-hinting is supported and preferred over font built-in hinting. Used by dynamic fonts only (MSDF fonts don't support hinting).

bool generate_mipmaps = false 

void set_generate_mipmaps(value: bool)

bool get_generate_mipmaps()

If set to true, generate mipmaps for the font textures.

Hinting hinting = 1 

void set_hinting(value: Hinting)

Hinting get_hinting()

Font hinting mode. Used by dynamic fonts only.

bool keep_rounding_remainders = true 

void set_keep_rounding_remainders(value: bool)

bool get_keep_rounding_remainders()

If set to true, when aligning glyphs to the pixel boundaries rounding remainders are accumulated to ensure more uniform glyph distribution. This setting has no effect if subpixel positioning is enabled.

bool modulate_color_glyphs = false 

void set_modulate_color_glyphs(value: bool)

bool is_modulate_color_glyphs()

If set to true, color modulation is applied when drawing colored glyphs, otherwise it's applied to the monochrome glyphs only.

int msdf_pixel_range = 16 

void set_msdf_pixel_range(value: int)

int get_msdf_pixel_range()

The width of the range around the shape between the minimum and maximum representable signed distance. If using font outlines, msdf_pixel_range must be set to at least twice the size of the largest font outline. The default msdf_pixel_range value of 16 allows outline sizes up to 8 to look correct.

void set_msdf_size(value: int)

Source font size used to generate MSDF textures. Higher values allow for more precision, but are slower to render and require more memory. Only increase this value if you notice a visible lack of precision in glyph rendering.

bool multichannel_signed_distance_field = false 

void set_multichannel_signed_distance_field(value: bool)

bool is_multichannel_signed_distance_field()

If set to true, glyphs of all sizes are rendered using single multichannel signed distance field (MSDF) generated from the dynamic font vector data. Since this approach does not rely on rasterizing the font every time its size changes, this allows for resizing the font in real-time without any performance penalty. Text will also not look grainy for Controls that are scaled down (or for Label3Ds viewed from a long distance). As a downside, font hinting is not available with MSDF. The lack of font hinting may result in less crisp and less readable fonts at small sizes.

Note: If using font outlines, msdf_pixel_range must be set to at least twice the size of the largest font outline.

Note: MSDF font rendering does not render glyphs with overlapping shapes correctly. Overlapping shapes are not valid per the OpenType standard, but are still commonly found in many font files, especially those converted by Google Fonts. To avoid issues with overlapping glyphs, consider downloading the font file directly from the type foundry instead of relying on Google Fonts.

Dictionary opentype_feature_overrides = {} 

void set_opentype_feature_overrides(value: Dictionary)

Dictionary get_opentype_feature_overrides()

Font OpenType feature set override.

float oversampling = 0.0 

void set_oversampling(value: float)

float get_oversampling()

If set to a positive value, overrides the oversampling factor of the viewport this font is used in. See Viewport.oversampling. This value doesn't override the oversampling parameter of draw_* methods.

String style_name = "" 

void set_font_style_name(value: String)

String get_font_style_name()

SubpixelPositioning subpixel_positioning = 1 

void set_subpixel_positioning(value: SubpixelPositioning)

SubpixelPositioning get_subpixel_positioning()

Font glyph subpixel positioning mode. Subpixel positioning provides shaper text and better kerning for smaller font sizes, at the cost of higher memory usage and lower font rasterization speed. Use TextServer.SUBPIXEL_POSITIONING_AUTO to automatically enable it based on the font size.

Removes all font cache entries.

void clear_glyphs(cache_index: int, size: Vector2i) 

Removes all rendered glyph information from the cache entry.

Note: This function will not remove textures associated with the glyphs, use remove_texture() to remove them manually.

void clear_kerning_map(cache_index: int, size: int) 

Removes all kerning overrides.

void clear_size_cache(cache_index: int) 

Removes all font sizes from the cache entry.

void clear_textures(cache_index: int, size: Vector2i) 

Removes all textures from font cache entry.

Note: This function will not remove glyphs associated with the texture, use remove_glyph() to remove them manually.

float get_cache_ascent(cache_index: int, size: int) const 

Returns the font ascent (number of pixels above the baseline).

int get_cache_count() const 

Returns number of the font cache entries.

float get_cache_descent(cache_index: int, size: int) const 

Returns the font descent (number of pixels below the baseline).

float get_cache_scale(cache_index: int, size: int) const 

Returns scaling factor of the color bitmap font.

float get_cache_underline_position(cache_index: int, size: int) const 

Returns pixel offset of the underline below the baseline.

float get_cache_underline_thickness(cache_index: int, size: int) const 

Returns thickness of the underline in pixels.

int get_char_from_glyph_index(size: int, glyph_index: int) const 

Returns character code associated with glyph_index, or 0 if glyph_index is invalid. See get_glyph_index().

float get_embolden(cache_index: int) const 

Returns embolden strength, if is not equal to zero, emboldens the font outlines. Negative values reduce the outline thickness.

float get_extra_baseline_offset(cache_index: int) const 

Returns extra baseline offset (as a fraction of font height).

int get_extra_spacing(cache_index: int, spacing: SpacingType) const 

Returns spacing for spacing in pixels (not relative to the font size).

int get_face_index(cache_index: int) const 

Returns an active face index in the TrueType / OpenType collection.

Vector2 get_glyph_advance(cache_index: int, size: int, glyph: int) const 

Returns glyph advance (offset of the next glyph).

Note: Advance for glyphs outlines is the same as the base glyph advance and is not saved.

int get_glyph_index(size: int, char: int, variation_selector: int) const 

Returns the glyph index of a char, optionally modified by the variation_selector.

PackedInt32Array get_glyph_list(cache_index: int, size: Vector2i) const 

Returns list of rendered glyphs in the cache entry.

Vector2 get_glyph_offset(cache_index: int, size: Vector2i, glyph: int) const 

Returns glyph offset from the baseline.

Vector2 get_glyph_size(cache_index: int, size: Vector2i, glyph: int) const 

int get_glyph_texture_idx(cache_index: int, size: Vector2i, glyph: int) const 

Returns index of the cache texture containing the glyph.

Rect2 get_glyph_uv_rect(cache_index: int, size: Vector2i, glyph: int) const 

Returns rectangle in the cache texture containing the glyph.

Vector2 get_kerning(cache_index: int, size: int, glyph_pair: Vector2i) const 

Returns kerning for the pair of glyphs.

Array[Vector2i] get_kerning_list(cache_index: int, size: int) const 

Returns list of the kerning overrides.

bool get_language_support_override(language: String) const 

Returns true if support override is enabled for the language.

PackedStringArray get_language_support_overrides() const 

Returns list of language support overrides.

bool get_script_support_override(script: String) const 

Returns true if support override is enabled for the script.

PackedStringArray get_script_support_overrides() const 

Returns list of script support overrides.

Array[Vector2i] get_size_cache_list(cache_index: int) const 

Returns list of the font sizes in the cache. Each size is Vector2i with font size and outline size.

int get_texture_count(cache_index: int, size: Vector2i) const 

Returns number of textures used by font cache entry.

Image get_texture_image(cache_index: int, size: Vector2i, texture_index: int) const 

Returns a copy of the font cache texture image.

PackedInt32Array get_texture_offsets(cache_index: int, size: Vector2i, texture_index: int) const 

Returns a copy of the array containing glyph packing data.

Transform2D get_transform(cache_index: int) const 

Returns 2D transform, applied to the font outlines, can be used for slanting, flipping and rotating glyphs.

Dictionary get_variation_coordinates(cache_index: int) const 

Returns variation coordinates for the specified font cache entry. See Font.get_supported_variation_list() for more info.

Error load_bitmap_font(path: String) 

Loads an AngelCode BMFont (.fnt, .font) bitmap font from file path.

Warning: This method should only be used in the editor or in cases when you need to load external fonts at run-time, such as fonts located at the user:// directory.

Error load_dynamic_font(path: String) 

Loads a TrueType (.ttf), OpenType (.otf), WOFF (.woff), WOFF2 (.woff2) or Type 1 (.pfb, .pfm) dynamic font from file path.

Warning: This method should only be used in the editor or in cases when you need to load external fonts at run-time, such as fonts located at the user:// directory.

void remove_cache(cache_index: int) 

Removes specified font cache entry.

void remove_glyph(cache_index: int, size: Vector2i, glyph: int) 

Removes specified rendered glyph information from the cache entry.

Note: This function will not remove textures associated with the glyphs, use remove_texture() to remove them manually.

void remove_kerning(cache_index: int, size: int, glyph_pair: Vector2i) 

Removes kerning override for the pair of glyphs.

void remove_language_support_override(language: String) 

Remove language support override.

void remove_script_support_override(script: String) 

Removes script support override.

void remove_size_cache(cache_index: int, size: Vector2i) 

Removes specified font size from the cache entry.

void remove_texture(cache_index: int, size: Vector2i, texture_index: int) 

Removes specified texture from the cache entry.

Note: This function will not remove glyphs associated with the texture. Remove them manually using remove_glyph().

void render_glyph(cache_index: int, size: Vector2i, index: int) 

Renders specified glyph to the font cache texture.

void render_range(cache_index: int, size: Vector2i, start: int, end: int) 

Renders the range of characters to the font cache texture.

void set_cache_ascent(cache_index: int, size: int, ascent: float) 

Sets the font ascent (number of pixels above the baseline).

void set_cache_descent(cache_index: int, size: int, descent: float) 

Sets the font descent (number of pixels below the baseline).

void set_cache_scale(cache_index: int, size: int, scale: float) 

Sets scaling factor of the color bitmap font.

void set_cache_underline_position(cache_index: int, size: int, underline_position: float) 

Sets pixel offset of the underline below the baseline.

void set_cache_underline_thickness(cache_index: int, size: int, underline_thickness: float) 

Sets thickness of the underline in pixels.

void set_embolden(cache_index: int, strength: float) 

Sets embolden strength, if is not equal to zero, emboldens the font outlines. Negative values reduce the outline thickness.

void set_extra_baseline_offset(cache_index: int, baseline_offset: float) 

Sets extra baseline offset (as a fraction of font height).

void set_extra_spacing(cache_index: int, spacing: SpacingType, value: int) 

Sets the spacing for spacing to value in pixels (not relative to the font size).

void set_face_index(cache_index: int, face_index: int) 

Sets an active face index in the TrueType / OpenType collection.

void set_glyph_advance(cache_index: int, size: int, glyph: int, advance: Vector2) 

Sets glyph advance (offset of the next glyph).

Note: Advance for glyphs outlines is the same as the base glyph advance and is not saved.

void set_glyph_offset(cache_index: int, size: Vector2i, glyph: int, offset: Vector2) 

Sets glyph offset from the baseline.

void set_glyph_size(cache_index: int, size: Vector2i, glyph: int, gl_size: Vector2) 

void set_glyph_texture_idx(cache_index: int, size: Vector2i, glyph: int, texture_idx: int) 

Sets index of the cache texture containing the glyph.

void set_glyph_uv_rect(cache_index: int, size: Vector2i, glyph: int, uv_rect: Rect2) 

Sets rectangle in the cache texture containing the glyph.

void set_kerning(cache_index: int, size: int, glyph_pair: Vector2i, kerning: Vector2) 

Sets kerning for the pair of glyphs.

void set_language_support_override(language: String, supported: bool) 

Adds override for Font.is_language_supported().

void set_script_support_override(script: String, supported: bool) 

Adds override for Font.is_script_supported().

void set_texture_image(cache_index: int, size: Vector2i, texture_index: int, image: Image) 

Sets font cache texture image.

void set_texture_offsets(cache_index: int, size: Vector2i, texture_index: int, offset: PackedInt32Array) 

Sets array containing glyph packing data.

void set_transform(cache_index: int, transform: Transform2D) 

Sets 2D transform, applied to the font outlines, can be used for slanting, flipping, and rotating glyphs.

void set_variation_coordinates(cache_index: int, variation_coordinates: Dictionary) 

Sets variation coordinates for the specified font cache entry. See Font.get_supported_variation_list() for more info.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var f = load("res://BarlowCondensed-Bold.ttf")
$Label.add_theme_font_override("font", f)
$Label.add_theme_font_size_override("font_size", 64)
```

Example 2 (gdscript):
```gdscript
var f = ResourceLoader.Load<FontFile>("res://BarlowCondensed-Bold.ttf");
GetNode("Label").AddThemeFontOverride("font", f);
GetNode("Label").AddThemeFontSizeOverride("font_size", 64);
```

---

## JSON

**URL:** https://docs.godotengine.org/en/stable/classes/class_json.html

**Contents:**
- JSON
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Helper class for creating and parsing JSON data.

The JSON class enables all data types to be converted to and from a JSON string. This is useful for serializing data, e.g. to save to a file or send over the network.

stringify() is used to convert any data type into a JSON string.

parse() is used to convert any existing JSON data into a Variant that can be used within Godot. If successfully parsed, use data to retrieve the Variant, and use @GlobalScope.typeof() to check if the Variant's type is what you expect. JSON Objects are converted into a Dictionary, but JSON data can be used to store Arrays, numbers, Strings and even just a boolean.

Alternatively, you can parse strings using the static parse_string() method, but it doesn't handle errors.

Note: Both parse methods do not fully comply with the JSON specification:

Trailing commas in arrays or objects are ignored, instead of causing a parser error.

New line and tab characters are accepted in string literals, and are treated like their corresponding escape sequences \n and \t.

Numbers are parsed using String.to_float() which is generally more lax than the JSON specification.

Certain errors, such as invalid Unicode sequences, do not cause a parser error. Instead, the string is cleaned up and an error is logged to the console.

from_native(variant: Variant, full_objects: bool = false) static

get_error_line() const

get_error_message() const

get_parsed_text() const

parse(json_text: String, keep_text: bool = false)

parse_string(json_string: String) static

stringify(data: Variant, indent: String = "", sort_keys: bool = true, full_precision: bool = false) static

to_native(json: Variant, allow_objects: bool = false) static

Variant data = null 

void set_data(value: Variant)

Contains the parsed JSON data in Variant form.

Variant from_native(variant: Variant, full_objects: bool = false) static 

Converts a native engine type to a JSON-compliant value.

By default, objects are ignored for security reasons, unless full_objects is true.

You can convert a native value to a JSON string like this:

int get_error_line() const 

Returns 0 if the last call to parse() was successful, or the line number where the parse failed.

String get_error_message() const 

Returns an empty string if the last call to parse() was successful, or the error message if it failed.

String get_parsed_text() const 

Return the text parsed by parse() (requires passing keep_text to parse()).

Error parse(json_text: String, keep_text: bool = false) 

Attempts to parse the json_text provided.

Returns an Error. If the parse was successful, it returns @GlobalScope.OK and the result can be retrieved using data. If unsuccessful, use get_error_line() and get_error_message() to identify the source of the failure.

Non-static variant of parse_string(), if you want custom error handling.

The optional keep_text argument instructs the parser to keep a copy of the original text. This text can be obtained later by using the get_parsed_text() function and is used when saving the resource (instead of generating new text from data).

Variant parse_string(json_string: String) static 

Attempts to parse the json_string provided and returns the parsed data. Returns null if parse failed.

String stringify(data: Variant, indent: String = "", sort_keys: bool = true, full_precision: bool = false) static 

Converts a Variant var to JSON text and returns the result. Useful for serializing data to store or send over the network.

Note: The JSON specification does not define integer or float types, but only a number type. Therefore, converting a Variant to JSON text will convert all numerical values to float types.

Note: If full_precision is true, when stringifying floats, the unreliable digits are stringified in addition to the reliable digits to guarantee exact decoding.

The indent parameter controls if and how something is indented; its contents will be used where there should be an indent in the output. Even spaces like " " will work. \t and \n can also be used for a tab indent, or to make a newline for each indent respectively.

Variant to_native(json: Variant, allow_objects: bool = false) static 

Converts a JSON-compliant value that was created with from_native() back to native engine types.

By default, objects are ignored for security reasons, unless allow_objects is true.

You can convert a JSON string back to a native value like this:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (yaml):
```yaml
var data_to_send = ["a", "b", "c"]
var json_string = JSON.stringify(data_to_send)
# Save data
# ...
# Retrieve data
var json = JSON.new()
var error = json.parse(json_string)
if error == OK:
    var data_received = json.data
    if typeof(data_received) == TYPE_ARRAY:
        print(data_received) # Prints the array.
    else:
        print("Unexpected data")
else:
    print("JSON Parse Error: ", json.get_error_message(), " in ", json_string, " at line ", json.get_error_line())
```

Example 2 (gdscript):
```gdscript
var data = JSON.parse_string(json_string) # Returns null if parsing failed.
```

Example 3 (go):
```go
func encode_data(value, full_objects = false):
    return JSON.stringify(JSON.from_native(value, full_objects))
```

Example 4 (json):
```json
## JSON.stringify(my_dictionary)
{"name":"my_dictionary","version":"1.0.0","entities":[{"name":"entity_0","value":"value_0"},{"name":"entity_1","value":"value_1"}]}

## JSON.stringify(my_dictionary, "\t")
{
    "name": "my_dictionary",
    "version": "1.0.0",
    "entities": [
        {
            "name": "entity_0",
            "value": "value_0"
        },
        {
            "name": "entity_1",
            "value": "value_1"
        }
    ]
}

## JSON.stringify(my_dictionary, "...")
{
..."name": "my_dictionary",
..."version": "1.0.0",
..."entities": [
......{
........."name": "entity_0",
........."value": "value_0"
......},
......{
........."name": "entity_1",
........."value": "value_1"
......}
...]
}
```

---

## OpenXRInteractionProfileMetadata

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrinteractionprofilemetadata.html

**Contents:**
- OpenXRInteractionProfileMetadata
- Description
- Methods
- Method Descriptions
- User-contributed notes

Meta class registering supported devices in OpenXR.

This class allows OpenXR core and extensions to register metadata relating to supported interaction devices such as controllers, trackers, haptic devices, etc. It is primarily used by the action map editor and to sanitize any action map by removing extension-dependent entries when applicable.

register_interaction_profile(display_name: String, openxr_path: String, openxr_extension_name: String)

register_io_path(interaction_profile: String, display_name: String, toplevel_path: String, openxr_path: String, openxr_extension_name: String, action_type: ActionType)

register_profile_rename(old_name: String, new_name: String)

register_top_level_path(display_name: String, openxr_path: String, openxr_extension_name: String)

void register_interaction_profile(display_name: String, openxr_path: String, openxr_extension_name: String) 

Registers an interaction profile using its OpenXR designation (e.g. /interaction_profiles/khr/simple_controller is the profile for OpenXR's simple controller profile).

display_name is the description shown to the user. openxr_path is the interaction profile path being registered. openxr_extension_name optionally restricts this profile to the given extension being enabled/available. If the extension is not available, the profile and all related entries used in an action map are filtered out.

void register_io_path(interaction_profile: String, display_name: String, toplevel_path: String, openxr_path: String, openxr_extension_name: String, action_type: ActionType) 

Registers an input/output path for the given interaction_profile. The profile should previously have been registered using register_interaction_profile(). display_name is the description shown to the user. toplevel_path specifies the bind path this input/output can be bound to (e.g. /user/hand/left or /user/hand/right). openxr_path is the action input/output being registered (e.g. /user/hand/left/input/aim/pose). openxr_extension_name restricts this input/output to an enabled/available extension, this doesn't need to repeat the extension on the profile but relates to overlapping extension (e.g. XR_EXT_palm_pose that introduces …/input/palm_ext/pose input paths). action_type defines the type of input or output provided by OpenXR.

void register_profile_rename(old_name: String, new_name: String) 

Allows for renaming old interaction profile paths to new paths to maintain backwards compatibility with older action maps.

void register_top_level_path(display_name: String, openxr_path: String, openxr_extension_name: String) 

Registers a top level path to which profiles can be bound. For instance /user/hand/left refers to the bind point for the player's left hand. Extensions can register additional top level paths, for instance a haptic vest extension might register /user/body/vest.

display_name is the name shown to the user. openxr_path is the top level path being registered. openxr_extension_name is optional and ensures the top level path is only used if the specified extension is available/enabled.

When a top level path ends up being bound by OpenXR, an XRPositionalTracker is instantiated to manage the state of the device.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRInteractionProfile

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrinteractionprofile.html

**Contents:**
- OpenXRInteractionProfile
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Suggested bindings object for OpenXR.

This object stores suggested bindings for an interaction profile. Interaction profiles define the metadata for a tracked XR device such as an XR controller.

For more information see the interaction profiles info in the OpenXR specification.

interaction_profile_path

get_binding(index: int) const

get_binding_count() const

OpenXRIPBindingModifier

get_binding_modifier(index: int) const

get_binding_modifier_count() const

Array binding_modifiers = [] 

void set_binding_modifiers(value: Array)

Array get_binding_modifiers()

Binding modifiers for this interaction profile.

Array bindings = [] 

void set_bindings(value: Array)

Action bindings for this interaction profile.

String interaction_profile_path = "" 

void set_interaction_profile_path(value: String)

String get_interaction_profile_path()

The interaction profile path identifying the XR device.

OpenXRIPBinding get_binding(index: int) const 

Retrieve the binding at this index.

int get_binding_count() const 

Get the number of bindings in this interaction profile.

OpenXRIPBindingModifier get_binding_modifier(index: int) const 

Get the OpenXRBindingModifier at this index.

int get_binding_modifier_count() const 

Get the number of binding modifiers in this interaction profile.

Please read the User-contributed notes policy before submitting a comment.

---

## PackedScene

**URL:** https://docs.godotengine.org/en/stable/classes/class_packedscene.html

**Contents:**
- PackedScene
- Description
- Tutorials
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

An abstraction of a serialized scene.

A simplified interface to a scene file. Provides access to operations and checks that can be performed on the scene resource itself.

Can be used to save a node to a file. When saving, the node as well as all the nodes it owns get saved (see Node.owner property).

Note: The node doesn't need to own itself.

Example: Load a saved scene:

Example: Save a node with different owners. The following example creates 3 objects: Node2D (node), RigidBody2D (body) and CollisionObject2D (collision). collision is a child of body which is a child of node. Only body is owned by node and pack() will therefore only save those two nodes, but not collision.

2D Role Playing Game (RPG) Demo

can_instantiate() const

instantiate(edit_state: GenEditState = 0) const

GenEditState GEN_EDIT_STATE_DISABLED = 0

If passed to instantiate(), blocks edits to the scene state.

GenEditState GEN_EDIT_STATE_INSTANCE = 1

If passed to instantiate(), provides local scene resources to the local scene.

Note: Only available in editor builds.

GenEditState GEN_EDIT_STATE_MAIN = 2

If passed to instantiate(), provides local scene resources to the local scene. Only the main scene should receive the main edit state.

Note: Only available in editor builds.

GenEditState GEN_EDIT_STATE_MAIN_INHERITED = 3

It's similar to GEN_EDIT_STATE_MAIN, but for the case where the scene is being instantiated to be the base of another one.

Note: Only available in editor builds.

bool can_instantiate() const 

Returns true if the scene file has nodes.

SceneState get_state() const 

Returns the SceneState representing the scene file contents.

Node instantiate(edit_state: GenEditState = 0) const 

Instantiates the scene's node hierarchy. Triggers child scene instantiation(s). Triggers a Node.NOTIFICATION_SCENE_INSTANTIATED notification on the root node.

Error pack(path: Node) 

Packs the path node, and all owned sub-nodes, into this PackedScene. Any existing data will be cleared. See Node.owner.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
# Use load() instead of preload() if the path isn't known at compile-time.
var scene = preload("res://scene.tscn").instantiate()
# Add the node as a child of the node the script is attached to.
add_child(scene)
```

Example 2 (typescript):
```typescript
// C# has no preload, so you have to always use ResourceLoader.Load<PackedScene>().
var scene = ResourceLoader.Load<PackedScene>("res://scene.tscn").Instantiate();
// Add the node as a child of the node the script is attached to.
AddChild(scene);
```

Example 3 (gdscript):
```gdscript
# Create the objects.
var node = Node2D.new()
var body = RigidBody2D.new()
var collision = CollisionShape2D.new()

# Create the object hierarchy.
body.add_child(collision)
node.add_child(body)

# Change owner of `body`, but not of `collision`.
body.owner = node
var scene = PackedScene.new()

# Only `node` and `body` are now packed.
var result = scene.pack(node)
if result == OK:
    var error = ResourceSaver.save(scene, "res://path/name.tscn")  # Or "user://..."
    if error != OK:
        push_error("An error occurred while saving the scene to disk.")
```

Example 4 (gdscript):
```gdscript
// Create the objects.
var node = new Node2D();
var body = new RigidBody2D();
var collision = new CollisionShape2D();

// Create the object hierarchy.
body.AddChild(collision);
node.AddChild(body);

// Change owner of `body`, but not of `collision`.
body.Owner = node;
var scene = new PackedScene();

// Only `node` and `body` are now packed.
Error result = scene.Pack(node);
if (result == Error.Ok)
{
    Error error = ResourceSaver.Save(scene, "res://path/name.tscn"); // Or "user://..."
    if (error != Error.Ok)
    {
        GD.PushError("An error occurred while saving the scene to disk.");
    }
}
```

---

## ResourceLoader

**URL:** https://docs.godotengine.org/en/stable/classes/class_resourceloader.html

**Contents:**
- ResourceLoader
- Description
- Tutorials
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

A singleton for loading resource files.

A singleton used to load resource files from the filesystem.

It uses the many ResourceFormatLoader classes registered in the engine (either built-in or from a plugin) to load files into memory and convert them to a format that can be used by the engine.

Note: You have to import the files into the engine first to load them using load(). If you want to load Images at run-time, you may use Image.load(). If you want to import audio files, you can use the snippet described in AudioStreamMP3.data.

Note: Non-resource files such as plain text files cannot be read using ResourceLoader. Use FileAccess for those files instead, and be aware that non-resource files are not exported by default (see notes in the FileAccess class description for instructions on exporting them).

Operating System Testing Demo

add_resource_format_loader(format_loader: ResourceFormatLoader, at_front: bool = false)

exists(path: String, type_hint: String = "")

get_cached_ref(path: String)

get_dependencies(path: String)

get_recognized_extensions_for_type(type: String)

get_resource_uid(path: String)

has_cached(path: String)

list_directory(directory_path: String)

load(path: String, type_hint: String = "", cache_mode: CacheMode = 1)

load_threaded_get(path: String)

load_threaded_get_status(path: String, progress: Array = [])

load_threaded_request(path: String, type_hint: String = "", use_sub_threads: bool = false, cache_mode: CacheMode = 1)

remove_resource_format_loader(format_loader: ResourceFormatLoader)

set_abort_on_missing_resources(abort: bool)

enum ThreadLoadStatus: 

ThreadLoadStatus THREAD_LOAD_INVALID_RESOURCE = 0

The resource is invalid, or has not been loaded with load_threaded_request().

ThreadLoadStatus THREAD_LOAD_IN_PROGRESS = 1

The resource is still being loaded.

ThreadLoadStatus THREAD_LOAD_FAILED = 2

Some error occurred during loading and it failed.

ThreadLoadStatus THREAD_LOAD_LOADED = 3

The resource was loaded successfully and can be accessed via load_threaded_get().

CacheMode CACHE_MODE_IGNORE = 0

Neither the main resource (the one requested to be loaded) nor any of its subresources are retrieved from cache nor stored into it. Dependencies (external resources) are loaded with CACHE_MODE_REUSE.

CacheMode CACHE_MODE_REUSE = 1

The main resource (the one requested to be loaded), its subresources, and its dependencies (external resources) are retrieved from cache if present, instead of loaded. Those not cached are loaded and then stored into the cache. The same rules are propagated recursively down the tree of dependencies (external resources).

CacheMode CACHE_MODE_REPLACE = 2

Like CACHE_MODE_REUSE, but the cache is checked for the main resource (the one requested to be loaded) as well as for each of its subresources. Those already in the cache, as long as the loaded and cached types match, have their data refreshed from storage into the already existing instances. Otherwise, they are recreated as completely new objects.

CacheMode CACHE_MODE_IGNORE_DEEP = 3

Like CACHE_MODE_IGNORE, but propagated recursively down the tree of dependencies (external resources).

CacheMode CACHE_MODE_REPLACE_DEEP = 4

Like CACHE_MODE_REPLACE, but propagated recursively down the tree of dependencies (external resources).

void add_resource_format_loader(format_loader: ResourceFormatLoader, at_front: bool = false) 

Registers a new ResourceFormatLoader. The ResourceLoader will use the ResourceFormatLoader as described in load().

This method is performed implicitly for ResourceFormatLoaders written in GDScript (see ResourceFormatLoader for more information).

bool exists(path: String, type_hint: String = "") 

Returns whether a recognized resource exists for the given path.

An optional type_hint can be used to further specify the Resource type that should be handled by the ResourceFormatLoader. Anything that inherits from Resource can be used as a type hint, for example Image.

Note: If you use Resource.take_over_path(), this method will return true for the taken path even if the resource wasn't saved (i.e. exists only in resource cache).

Resource get_cached_ref(path: String) 

Returns the cached resource reference for the given path.

Note: If the resource is not cached, the returned Resource will be invalid.

PackedStringArray get_dependencies(path: String) 

Returns the dependencies for the resource at the given path.

Each dependency is a string that can be divided into sections by ::. There can be either one section or three sections, with the second section always being empty. When there is one section, it contains the file path. When there are three sections, the first section contains the UID and the third section contains the fallback path.

PackedStringArray get_recognized_extensions_for_type(type: String) 

Returns the list of recognized extensions for a resource type.

int get_resource_uid(path: String) 

Returns the ID associated with a given resource path, or -1 when no such ID exists.

bool has_cached(path: String) 

Returns whether a cached resource is available for the given path.

Once a resource has been loaded by the engine, it is cached in memory for faster access, and future calls to the load() method will use the cached version. The cached resource can be overridden by using Resource.take_over_path() on a new resource for that same path.

PackedStringArray list_directory(directory_path: String) 

Lists a directory, returning all resources and subdirectories contained within. The resource files have the original file names as visible in the editor before exporting. The directories have "/" appended.

Note: The order of files and directories returned by this method is not deterministic, and can vary between operating systems.

Note: To normally traverse the filesystem, see DirAccess.

Resource load(path: String, type_hint: String = "", cache_mode: CacheMode = 1) 

Loads a resource at the given path, caching the result for further access.

The registered ResourceFormatLoaders are queried sequentially to find the first one which can handle the file's extension, and then attempt loading. If loading fails, the remaining ResourceFormatLoaders are also attempted.

An optional type_hint can be used to further specify the Resource type that should be handled by the ResourceFormatLoader. Anything that inherits from Resource can be used as a type hint, for example Image.

The cache_mode property defines whether and how the cache should be used or updated when loading the resource.

Returns an empty resource if no ResourceFormatLoader could handle the file, and prints an error if no file is found at the specified path.

GDScript has a simplified @GDScript.load() built-in method which can be used in most situations, leaving the use of ResourceLoader for more advanced scenarios.

Note: If ProjectSettings.editor/export/convert_text_resources_to_binary is true, @GDScript.load() will not be able to read converted files in an exported project. If you rely on run-time loading of files present within the PCK, set ProjectSettings.editor/export/convert_text_resources_to_binary to false.

Note: Relative paths will be prefixed with "res://" before loading, to avoid unexpected results make sure your paths are absolute.

Resource load_threaded_get(path: String) 

Returns the resource loaded by load_threaded_request().

If this is called before the loading thread is done (i.e. load_threaded_get_status() is not THREAD_LOAD_LOADED), the calling thread will be blocked until the resource has finished loading. However, it's recommended to use load_threaded_get_status() to known when the load has actually completed.

ThreadLoadStatus load_threaded_get_status(path: String, progress: Array = []) 

Returns the status of a threaded loading operation started with load_threaded_request() for the resource at path.

An array variable can optionally be passed via progress, and will return a one-element array containing the ratio of completion of the threaded loading (between 0.0 and 1.0).

Note: The recommended way of using this method is to call it during different frames (e.g., in Node._process(), instead of a loop).

Error load_threaded_request(path: String, type_hint: String = "", use_sub_threads: bool = false, cache_mode: CacheMode = 1) 

Loads the resource using threads. If use_sub_threads is true, multiple threads will be used to load the resource, which makes loading faster, but may affect the main thread (and thus cause game slowdowns).

The cache_mode parameter defines whether and how the cache should be used or updated when loading the resource.

void remove_resource_format_loader(format_loader: ResourceFormatLoader) 

Unregisters the given ResourceFormatLoader.

void set_abort_on_missing_resources(abort: bool) 

Changes the behavior on missing sub-resources. The default behavior is to abort loading.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (python):
```python
for dependency in ResourceLoader.get_dependencies(path):
    if dependency.contains("::"):
        print(dependency.get_slice("::", 0)) # Prints the UID.
        print(dependency.get_slice("::", 2)) # Prints the fallback path.
    else:
        print(dependency) # Prints the path.
```

Example 2 (markdown):
```markdown
# Prints ["extra_data/", "model.gltf", "model.tscn", "model_slime.png"]
print(ResourceLoader.list_directory("res://assets/enemies/slime"))
```

---

## Runtime file loading and saving

**URL:** https://docs.godotengine.org/en/stable/tutorials/io/runtime_file_loading_and_saving.html

**Contents:**
- Runtime file loading and saving
- Plain text and binary files
- Images
- Audio/video files
- 3D scenes
- Fonts
- ZIP archives
- User-contributed notes

See Saving games for information on saving and loading game progression.

Sometimes, exporting packs, patches, and mods is not ideal when you want players to be able to load user-generated content in your project. It requires users to generate a PCK or ZIP file through the Godot editor, which contains resources imported by Godot.

Example use cases for runtime file loading and saving include:

Loading texture packs designed for the game.

Loading user-provided audio tracks and playing them back in an in-game radio station.

Loading custom levels or 3D models that can be designed with any 3D DCC that can export to glTF or FBX (including glTF scenes saved by Godot at runtime).

Using user-provided fonts for menus and HUD.

Saving/loading a file format that can contain multiple files but can still easily be read by other applications (ZIP).

Loading files created by another game or program, or even game data files from another game not made with Godot.

Runtime file loading can be combined with HTTP requests to load resources from the Internet directly.

Do not use this runtime loading approach to load resources that are part of the project, as it's less efficient and doesn't allow benefiting from Godot's resource handling functionality (such as translation remaps). See Import process for details.

You can see how saving and loading works in action using the Run-time File Saving and Loading (Serialization) demo project.

Godot's FileAccess class provides methods to access files on the filesystem for reading and writing:

To handle custom binary formats (such as loading file formats not supported by Godot), FileAccess provides several methods to read/write integers, floats, strings and more. These FileAccess methods have names that start with get_ and store_.

If you need more control over reading binary files or need to read binary streams that are not part of a file, PackedByteArray provides several helper methods to decode/encode series of bytes to integers, floats, strings and more. These PackedByteArray methods have names that start with decode_ and encode_. See also Binary serialization API.

Image's Image.load_from_file static method handles everything, from format detection based on file extension to reading the file from disk.

If you need error handling or more control (such as changing the scale an SVG is loaded at), use one of the following methods depending on the file format:

Image.load_jpg_from_buffer

Image.load_ktx_from_buffer

Image.load_png_from_buffer

Image.load_svg_from_buffer or Image.load_svg_from_string

Image.load_tga_from_buffer

Image.load_webp_from_buffer

Several image formats can also be saved by Godot at runtime using the following methods:

Image.save_png or Image.save_png_to_buffer

Image.save_webp or Image.save_webp_to_buffer

Image.save_jpg or Image.save_jpg_to_buffer

Image.save_exr or Image.save_exr_to_buffer (only available in editor builds, cannot be used in exported projects)

The methods with the to_buffer suffix save the image to a PackedByteArray instead of the filesystem. This is useful to send the image over the network or into a ZIP archive without having to write it on the filesystem. This can increase performance by reducing I/O utilization.

If displaying the loaded image on a 3D surface, make sure to call Image.generate_mipmaps so that the texture doesn't look grainy when viewed at a distance. This is also useful in 2D when following instructions on reducing aliasing when downsampling.

Example of loading an image and displaying it in a TextureRect node (which requires conversion to ImageTexture):

Godot supports loading Ogg Vorbis, MP3, and WAV audio at runtime. Note that not all files with a .ogg extension are Ogg Vorbis files. Some may be Ogg Theora videos, or contain Opus audio within an Ogg container. These files will not load correctly as audio files in Godot.

Example of loading an Ogg Vorbis audio file in an AudioStreamPlayer node:

Example of loading an Ogg Theora video file in a VideoStreamPlayer node:

Godot has first-class support for glTF 2.0, both in the editor and exported projects. Using GLTFDocument and GLTFState together, Godot can load and save glTF files in exported projects, in both text (.gltf) and binary (.glb) formats. The binary format should be preferred as it's faster to write and smaller, but the text format is easier to debug.

Since Godot 4.3, FBX scenes can also be loaded (but not saved) at runtime using the FBXDocument and FBXState classes. The code to do so is the same as glTF, but you will need to replace all instances of GLTFDocument and GLTFState with FBXDocument and FBXState in the code samples below.

Example of loading a glTF scene and appending its root node to the scene:

When loading a glTF scene, a base path must be set so that external resources like textures can be loaded correctly. When loading from a file, the base path is automatically set to the folder containing the file. When loading from a buffer, this base path must be manually set as there is no way for Godot to infer this path.

To set the base path, set GLTFState.base_path on your GLTFState instance before calling GLTFDocument.append_from_buffer or GLTFDocument.append_from_file.

FontFile.load_dynamic_font supports the following font file formats: TTF, OTF, WOFF, WOFF2, PFB, PFM

On the other hand, FontFile.load_bitmap_font supports the BMFont format (.fnt or .font).

Additionally, it is possible to load any font that is installed on the system using Godot's support for System fonts.

Example of loading a font file automatically according to its file extension, then adding it as a theme override to a Label node:

Godot supports reading and writing ZIP archives using the ZIPReader and ZIPPacker classes. This supports any ZIP file, including files generated by Godot's "Export PCK/ZIP" functionality (although these will contain imported Godot resources rather than the original project files).

Use ProjectSettings.load_resource_pack to load PCK or ZIP files exported by Godot as additional data packs. That approach is preferred for DLCs, as it makes interacting with additional data packs seamless (virtual filesystem).

This ZIP archive support can be combined with runtime image, 3D scene and audio loading to provide a seamless modding experience without requiring users to go through the Godot editor to generate PCK/ZIP files.

Example that lists files in a ZIP archive in an ItemList node, then writes contents read from it to a new ZIP archive (essentially duplicating the archive):

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func save_file(content):
    var file = FileAccess.open("/path/to/file.txt", FileAccess.WRITE)
    file.store_string(content)

func load_file():
    var file = FileAccess.open("/path/to/file.txt", FileAccess.READ)
    var content = file.get_as_text()
    return content
```

Example 2 (csharp):
```csharp
private void SaveFile(string content)
{
    using var file = FileAccess.Open("/Path/To/File.txt", FileAccess.ModeFlags.Write);
    file.StoreString(content);
}

private string LoadFile()
{
    using var file = FileAccess.Open("/Path/To/File.txt", FileAccess.ModeFlags.Read);
    string content = file.GetAsText();
    return content;
}
```

Example 3 (sql):
```sql
# Load an image of any format supported by Godot from the filesystem.
var image = Image.load_from_file(path)
# Optionally, generate mipmaps if displaying the texture on a 3D surface
# so that the texture doesn't look grainy when viewed at a distance.
#image.generate_mipmaps()
$TextureRect.texture = ImageTexture.create_from_image(image)

# Save the loaded Image to a PNG image.
image.save_png("/path/to/file.png")

# Save the converted ImageTexture to a PNG image.
$TextureRect.texture.get_image().save_png("/path/to/file.png")
```

Example 4 (sql):
```sql
// Load an image of any format supported by Godot from the filesystem.
var image = Image.LoadFromFile(path);
// Optionally, generate mipmaps if displaying the texture on a 3D surface
// so that the texture doesn't look grainy when viewed at a distance.
// image.GenerateMipmaps();
GetNode<TextureRect>("TextureRect").Texture = ImageTexture.CreateFromImage(image);

// Save the loaded Image to a PNG image.
image.SavePng("/Path/To/File.png");

// Save the converted ImageTexture to a PNG image.
GetNode<TextureRect>("TextureRect").Texture.GetImage().SavePng("/Path/To/File.png");
```

---

## Saving games

**URL:** https://docs.godotengine.org/en/stable/tutorials/io/saving_games.html

**Contents:**
- Saving games
- Introduction
- Identify persistent objects
- Serializing
- Saving and reading data
- Some notes
- JSON vs binary serialization
  - JSON limitations
  - Binary serialization
- User-contributed notes

Save games can be complicated. For example, it may be desirable to store information from multiple objects across multiple levels. Advanced save game systems should allow for additional information about an arbitrary number of objects. This will allow the save function to scale as the game grows more complex.

If you're looking to save user configuration, you can use the ConfigFile class for this purpose.

You can see how saving and loading works in action using the Saving and Loading (Serialization) demo project.

Firstly, we should identify what objects we want to keep between game sessions and what information we want to keep from those objects. For this tutorial, we will use groups to mark and handle objects to be saved, but other methods are certainly possible.

We will start by adding objects we wish to save to the "Persist" group. We can do this through either the GUI or script. Let's add the relevant nodes using the GUI:

Once this is done, when we need to save the game, we can get all objects to save them and then tell them all to save with this script:

The next step is to serialize the data. This makes it much easier to read from and store to disk. In this case, we're assuming each member of group Persist is an instanced node and thus has a path. GDScript has the helper class JSON to convert between dictionary and string. Our node needs to contain a save function that returns this data. The save function will look like this:

This gives us a dictionary with the style { "variable_name":value_of_variable }, which will be useful when loading.

As covered in the File system tutorial, we'll need to open a file so we can write to it or read from it. Now that we have a way to call our groups and get their relevant data, let's use the class JSON to convert it into an easily stored string and store them in a file. Doing it this way ensures that each line is its own object, so we have an easy way to pull the data out of the file as well.

Game saved! Now, to load, we'll read each line. Use the parse method to read the JSON string back to a dictionary, and then iterate over the dict to read our values. But we'll need to first create the object and we can use the filename and parent values to achieve that. Here is our load function:

Now we can save and load an arbitrary number of objects laid out almost anywhere across the scene tree! Each object can store different data depending on what it needs to save.

We have glossed over setting up the game state for loading. It's ultimately up to the project creator where much of this logic goes. This is often complicated and will need to be heavily customized based on the needs of the individual project.

Additionally, our implementation assumes no Persist objects are children of other Persist objects. Otherwise, invalid paths would be created. To accommodate nested Persist objects, consider saving objects in stages. Load parent objects first so they are available for the add_child() call when child objects are loaded. You will also need a way to link children to parents as the NodePath will likely be invalid.

For simple game state, JSON may work and it generates human-readable files that are easy to debug.

But JSON has many limitations. If you need to store more complex game state or a lot of it, binary serialization may be a better approach.

Here are some important gotchas to know about when using JSON.

Filesize: JSON stores data in text format, which is much larger than binary formats.

Data types: JSON only offers a limited set of data types. If you have data types that JSON doesn't have, you will need to translate your data to and from types that JSON can handle. For example, some important types that JSON can't parse are: Vector2, Vector3, Color, Rect2, and Quaternion.

Custom logic needed for encoding/decoding: If you have any custom classes that you want to store with JSON, you will need to write your own logic for encoding and decoding those classes.

Binary serialization is an alternative approach for storing game state, and you can use it with the functions get_var and store_var of FileAccess.

Binary serialization should produce smaller files than JSON.

Binary serialization can handle most common data types.

Binary serialization requires less custom logic for encoding and decoding custom classes.

Note that not all properties are included. Only properties that are configured with the PROPERTY_USAGE_STORAGE flag set will be serialized. You can add a new usage flag to a property by overriding the _get_property_list method in your class. You can also check how property usage is configured by calling Object._get_property_list. See PropertyUsageFlags for the possible usage flags.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var save_nodes = get_tree().get_nodes_in_group("Persist")
for node in save_nodes:
    # Now, we can call our save function on each node.
```

Example 2 (swift):
```swift
var saveNodes = GetTree().GetNodesInGroup("Persist");
foreach (Node saveNode in saveNodes)
{
    // Now, we can call our save function on each node.
}
```

Example 3 (gdscript):
```gdscript
func save():
    var save_dict = {
        "filename" : get_scene_file_path(),
        "parent" : get_parent().get_path(),
        "pos_x" : position.x, # Vector2 is not supported by JSON
        "pos_y" : position.y,
        "attack" : attack,
        "defense" : defense,
        "current_health" : current_health,
        "max_health" : max_health,
        "damage" : damage,
        "regen" : regen,
        "experience" : experience,
        "tnl" : tnl,
        "level" : level,
        "attack_growth" : attack_growth,
        "defense_growth" : defense_growth,
        "health_growth" : health_growth,
        "is_alive" : is_alive,
        "last_attack" : last_attack
    }
    return save_dict
```

Example 4 (csharp):
```csharp
public Godot.Collections.Dictionary<string, Variant> Save()
{
    return new Godot.Collections.Dictionary<string, Variant>()
    {
        { "Filename", SceneFilePath },
        { "Parent", GetParent().GetPath() },
        { "PosX", Position.X }, // Vector2 is not supported by JSON
        { "PosY", Position.Y },
        { "Attack", Attack },
        { "Defense", Defense },
        { "CurrentHealth", CurrentHealth },
        { "MaxHealth", MaxHealth },
        { "Damage", Damage },
        { "Regen", Regen },
        { "Experience", Experience },
        { "Tnl", Tnl },
        { "Level", Level },
        { "AttackGrowth", AttackGrowth },
        { "DefenseGrowth", DefenseGrowth },
        { "HealthGrowth", HealthGrowth },
        { "IsAlive", IsAlive },
        { "LastAttack", LastAttack }
    };
}
```

---

## VideoStream

**URL:** https://docs.godotengine.org/en/stable/classes/class_videostream.html

**Contents:**
- VideoStream
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: VideoStreamTheora

Base resource for video streams.

Base resource type for all video streams. Classes that derive from VideoStream can all be used as resource types to play back videos in VideoStreamPlayer.

Runtime file loading and saving

_instantiate_playback() virtual

void set_file(value: String)

The video file path or URI that this VideoStream resource handles.

For VideoStreamTheora, this filename should be an Ogg Theora video file with the .ogv extension.

VideoStreamPlayback _instantiate_playback() virtual 

Called when the video starts playing, to initialize and return a subclass of VideoStreamPlayback.

Please read the User-contributed notes policy before submitting a comment.

---
