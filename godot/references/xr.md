# Godot - Xr

**Pages:** 62

---

## Array

**URL:** https://docs.godotengine.org/en/stable/classes/class_array.html

**Contents:**
- Array
- Description
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A built-in data structure that holds a sequence of elements.

An array data structure that can contain a sequence of elements of any Variant type by default. Values can optionally be constrained to a specific type by creating a typed array. Elements are accessed by a numerical index starting at 0. Negative indices are used to count from the back (-1 is the last element, -2 is the second to last, etc.).

Note: Arrays are always passed by reference. To get a copy of an array that can be modified independently of the original array, use duplicate().

Note: Erasing elements while iterating over arrays is not supported and will result in unpredictable behavior.

Differences between packed arrays, typed arrays, and untyped arrays: Packed arrays are generally faster to iterate on and modify compared to a typed array of the same type (e.g. PackedInt64Array versus Array[int]). Also, packed arrays consume less memory. As a downside, packed arrays are less flexible as they don't offer as many convenience methods such as map(). Typed arrays are in turn faster to iterate on and modify than untyped arrays.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

Array(base: Array, type: int, class_name: StringName, script: Variant)

Array(from: PackedByteArray)

Array(from: PackedColorArray)

Array(from: PackedFloat32Array)

Array(from: PackedFloat64Array)

Array(from: PackedInt32Array)

Array(from: PackedInt64Array)

Array(from: PackedStringArray)

Array(from: PackedVector2Array)

Array(from: PackedVector3Array)

Array(from: PackedVector4Array)

all(method: Callable) const

any(method: Callable) const

append(value: Variant)

append_array(array: Array)

bsearch(value: Variant, before: bool = true) const

bsearch_custom(value: Variant, func: Callable, before: bool = true) const

count(value: Variant) const

duplicate(deep: bool = false) const

duplicate_deep(deep_subresources_mode: int = 1) const

erase(value: Variant)

filter(method: Callable) const

find(what: Variant, from: int = 0) const

find_custom(method: Callable, from: int = 0) const

get(index: int) const

get_typed_builtin() const

get_typed_class_name() const

get_typed_script() const

has(value: Variant) const

insert(position: int, value: Variant)

is_same_typed(array: Array) const

map(method: Callable) const

pop_at(position: int)

push_back(value: Variant)

push_front(value: Variant)

reduce(method: Callable, accum: Variant = null) const

remove_at(position: int)

rfind(what: Variant, from: int = -1) const

rfind_custom(method: Callable, from: int = -1) const

set(index: int, value: Variant)

slice(begin: int, end: int = 2147483647, step: int = 1, deep: bool = false) const

sort_custom(func: Callable)

operator !=(right: Array)

operator +(right: Array)

operator <(right: Array)

operator <=(right: Array)

operator ==(right: Array)

operator >(right: Array)

operator >=(right: Array)

operator [](index: int)

Constructs an empty Array.

Array Array(base: Array, type: int, class_name: StringName, script: Variant)

Creates a typed array from the base array. A typed array can only contain elements of the given type, or that inherit from the given class, as described by this constructor's parameters:

type is the built-in Variant type, as one the Variant.Type constants.

class_name is the built-in class name (see Object.get_class()).

script is the associated script. It must be a Script instance or null.

If type is not @GlobalScope.TYPE_OBJECT, class_name must be an empty StringName and script must be null.

The base array's elements are converted when necessary. If this is not possible or base is already typed, this constructor fails and returns an empty Array.

In GDScript, this constructor is usually not necessary, as it is possible to create a typed array through static typing:

Array Array(from: Array)

Returns the same array as from. If you need a copy of the array, use duplicate().

Array Array(from: PackedByteArray)

Constructs an array from a PackedByteArray.

Array Array(from: PackedColorArray)

Constructs an array from a PackedColorArray.

Array Array(from: PackedFloat32Array)

Constructs an array from a PackedFloat32Array.

Array Array(from: PackedFloat64Array)

Constructs an array from a PackedFloat64Array.

Array Array(from: PackedInt32Array)

Constructs an array from a PackedInt32Array.

Array Array(from: PackedInt64Array)

Constructs an array from a PackedInt64Array.

Array Array(from: PackedStringArray)

Constructs an array from a PackedStringArray.

Array Array(from: PackedVector2Array)

Constructs an array from a PackedVector2Array.

Array Array(from: PackedVector3Array)

Constructs an array from a PackedVector3Array.

Array Array(from: PackedVector4Array)

Constructs an array from a PackedVector4Array.

bool all(method: Callable) const 🔗

Calls the given Callable on each element in the array and returns true if the Callable returns true for all elements in the array. If the Callable returns false for one array element or more, this method returns false.

The method should take one Variant parameter (the current array element) and return a bool.

See also any(), filter(), map() and reduce().

Note: Unlike relying on the size of an array returned by filter(), this method will return as early as possible to improve performance (especially with large arrays).

Note: For an empty array, this method always returns true.

bool any(method: Callable) const 🔗

Calls the given Callable on each element in the array and returns true if the Callable returns true for one or more elements in the array. If the Callable returns false for all elements in the array, this method returns false.

The method should take one Variant parameter (the current array element) and return a bool.

See also all(), filter(), map() and reduce().

Note: Unlike relying on the size of an array returned by filter(), this method will return as early as possible to improve performance (especially with large arrays).

Note: For an empty array, this method always returns false.

void append(value: Variant) 🔗

Appends value at the end of the array (alias of push_back()).

void append_array(array: Array) 🔗

Appends another array at the end of this array.

void assign(array: Array) 🔗

Assigns elements of another array into the array. Resizes the array to match array. Performs type conversions if the array is typed.

Variant back() const 🔗

Returns the last element of the array. If the array is empty, fails and returns null. See also front().

Note: Unlike with the [] operator (array[-1]), an error is generated without stopping project execution.

int bsearch(value: Variant, before: bool = true) const 🔗

Returns the index of value in the sorted array. If it cannot be found, returns where value should be inserted to keep the array sorted. The algorithm used is binary search.

If before is true (as by default), the returned index comes before all existing elements equal to value in the array.

Note: Calling bsearch() on an unsorted array will result in unexpected behavior. Use sort() before calling this method.

int bsearch_custom(value: Variant, func: Callable, before: bool = true) const 🔗

Returns the index of value in the sorted array. If it cannot be found, returns where value should be inserted to keep the array sorted (using func for the comparisons). The algorithm used is binary search.

Similar to sort_custom(), func is called as many times as necessary, receiving one array element and value as arguments. The function should return true if the array element should be behind value, otherwise it should return false.

If before is true (as by default), the returned index comes before all existing elements equal to value in the array.

Note: Calling bsearch_custom() on an unsorted array will result in unexpected behavior. Use sort_custom() with func before calling this method.

Removes all elements from the array. This is equivalent to using resize() with a size of 0.

int count(value: Variant) const 🔗

Returns the number of times an element is in the array.

To count how many elements in an array satisfy a condition, see reduce().

Array duplicate(deep: bool = false) const 🔗

Returns a new copy of the array.

By default, a shallow copy is returned: all nested Array, Dictionary, and Resource elements are shared with the original array. Modifying any of those in one array will also affect them in the other.

If deep is true, a deep copy is returned: all nested arrays and dictionaries are also duplicated (recursively). Any Resource is still shared with the original array, though.

Array duplicate_deep(deep_subresources_mode: int = 1) const 🔗

Duplicates this array, deeply, like duplicate()(true), with extra control over how subresources are handled.

deep_subresources_mode must be one of the values from DeepDuplicateMode. By default, only internal resources will be duplicated (recursively).

void erase(value: Variant) 🔗

Finds and removes the first occurrence of value from the array. If value does not exist in the array, nothing happens. To remove an element by index, use remove_at() instead.

Note: This method shifts every element's index after the removed value back, which may have a noticeable performance cost, especially on larger arrays.

Note: Erasing elements while iterating over arrays is not supported and will result in unpredictable behavior.

void fill(value: Variant) 🔗

Assigns the given value to all elements in the array.

This method can often be combined with resize() to create an array with a given size and initialized elements:

Note: If value is a Variant passed by reference (Object-derived, Array, Dictionary, etc.), the array will be filled with references to the same value, which are not duplicates.

Array filter(method: Callable) const 🔗

Calls the given Callable on each element in the array and returns a new, filtered Array.

The method receives one of the array elements as an argument, and should return true to add the element to the filtered array, or false to exclude it.

See also any(), all(), map() and reduce().

int find(what: Variant, from: int = 0) const 🔗

Returns the index of the first occurrence of what in this array, or -1 if there are none. The search's start can be specified with from, continuing to the end of the array.

Note: If you just want to know whether the array contains what, use has() (Contains in C#). In GDScript, you may also use the in operator.

Note: For performance reasons, the search is affected by what's Variant.Type. For example, 7 (int) and 7.0 (float) are not considered equal for this method.

int find_custom(method: Callable, from: int = 0) const 🔗

Returns the index of the first element in the array that causes method to return true, or -1 if there are none. The search's start can be specified with from, continuing to the end of the array.

method is a callable that takes an element of the array, and returns a bool.

Note: If you just want to know whether the array contains anything that satisfies method, use any().

Variant front() const 🔗

Returns the first element of the array. If the array is empty, fails and returns null. See also back().

Note: Unlike with the [] operator (array[0]), an error is generated without stopping project execution.

Variant get(index: int) const 🔗

Returns the element at the given index in the array. If index out-of-bounds or negative, this method fails and returns null.

This method is similar (but not identical) to the [] operator. Most notably, when this method fails, it doesn't pause project execution if run from the editor.

int get_typed_builtin() const 🔗

Returns the built-in Variant type of the typed array as a Variant.Type constant. If the array is not typed, returns @GlobalScope.TYPE_NIL. See also is_typed().

StringName get_typed_class_name() const 🔗

Returns the built-in class name of the typed array, if the built-in Variant type @GlobalScope.TYPE_OBJECT. Otherwise, returns an empty StringName. See also is_typed() and Object.get_class().

Variant get_typed_script() const 🔗

Returns the Script instance associated with this typed array, or null if it does not exist. See also is_typed().

bool has(value: Variant) const 🔗

Returns true if the array contains the given value.

In GDScript, this is equivalent to the in operator:

Note: For performance reasons, the search is affected by the value's Variant.Type. For example, 7 (int) and 7.0 (float) are not considered equal for this method.

Returns a hashed 32-bit integer value representing the array and its contents.

Note: Arrays with equal hash values are not guaranteed to be the same, as a result of hash collisions. On the countrary, arrays with different hash values are guaranteed to be different.

int insert(position: int, value: Variant) 🔗

Inserts a new element (value) at a given index (position) in the array. position should be between 0 and the array's size(). If negative, position is considered relative to the end of the array.

Returns @GlobalScope.OK on success, or one of the other Error constants if this method fails.

Note: Every element's index after position needs to be shifted forward, which may have a noticeable performance cost, especially on larger arrays.

bool is_empty() const 🔗

Returns true if the array is empty ([]). See also size().

bool is_read_only() const 🔗

Returns true if the array is read-only. See make_read_only().

In GDScript, arrays are automatically read-only if declared with the const keyword.

bool is_same_typed(array: Array) const 🔗

Returns true if this array is typed the same as the given array. See also is_typed().

bool is_typed() const 🔗

Returns true if the array is typed. Typed arrays can only contain elements of a specific type, as defined by the typed array constructor. The methods of a typed array are still expected to return a generic Variant.

In GDScript, it is possible to define a typed array with static typing:

void make_read_only() 🔗

Makes the array read-only. The array's elements cannot be overridden with different values, and their order cannot change. Does not apply to nested elements, such as dictionaries.

In GDScript, arrays are automatically read-only if declared with the const keyword.

Array map(method: Callable) const 🔗

Calls the given Callable for each element in the array and returns a new array filled with values returned by the method.

The method should take one Variant parameter (the current array element) and can return any Variant.

See also filter(), reduce(), any() and all().

Variant max() const 🔗

Returns the maximum value contained in the array, if all elements can be compared. Otherwise, returns null. See also min().

To find the maximum value using a custom comparator, you can use reduce().

Variant min() const 🔗

Returns the minimum value contained in the array, if all elements can be compared. Otherwise, returns null. See also max().

Variant pick_random() const 🔗

Returns a random element from the array. Generates an error and returns null if the array is empty.

Note: Like many similar functions in the engine (such as @GlobalScope.randi() or shuffle()), this method uses a common, global random seed. To get a predictable outcome from this method, see @GlobalScope.seed().

Variant pop_at(position: int) 🔗

Removes and returns the element of the array at index position. If negative, position is considered relative to the end of the array. Returns null if the array is empty. If position is out of bounds, an error message is also generated.

Note: This method shifts every element's index after position back, which may have a noticeable performance cost, especially on larger arrays.

Removes and returns the last element of the array. Returns null if the array is empty, without generating an error. See also pop_front().

Variant pop_front() 🔗

Removes and returns the first element of the array. Returns null if the array is empty, without generating an error. See also pop_back().

Note: This method shifts every other element's index back, which may have a noticeable performance cost, especially on larger arrays.

void push_back(value: Variant) 🔗

Appends an element at the end of the array. See also push_front().

void push_front(value: Variant) 🔗

Adds an element at the beginning of the array. See also push_back().

Note: This method shifts every other element's index forward, which may have a noticeable performance cost, especially on larger arrays.

Variant reduce(method: Callable, accum: Variant = null) const 🔗

Calls the given Callable for each element in array, accumulates the result in accum, then returns it.

The method takes two arguments: the current value of accum and the current array element. If accum is null (as by default), the iteration will start from the second element, with the first one used as initial value of accum.

If max() is not desirable, this method may also be used to implement a custom comparator:

This method can also be used to count how many elements in an array satisfy a certain condition, similar to count():

See also map(), filter(), any(), and all().

void remove_at(position: int) 🔗

Removes the element from the array at the given index (position). If the index is out of bounds, this method fails. If the index is negative, position is considered relative to the end of the array.

If you need to return the removed element, use pop_at(). To remove an element by value, use erase() instead.

Note: This method shifts every element's index after position back, which may have a noticeable performance cost, especially on larger arrays.

Note: The position cannot be negative. To remove an element relative to the end of the array, use arr.remove_at(arr.size() - (i + 1)). To remove the last element from the array, use arr.resize(arr.size() - 1).

int resize(size: int) 🔗

Sets the array's number of elements to size. If size is smaller than the array's current size, the elements at the end are removed. If size is greater, new default elements (usually null) are added, depending on the array's type.

Returns @GlobalScope.OK on success, or one of the following Error constants if this method fails: @GlobalScope.ERR_LOCKED if the array is read-only, @GlobalScope.ERR_INVALID_PARAMETER if the size is negative, or @GlobalScope.ERR_OUT_OF_MEMORY if allocations fail. Use size() to find the actual size of the array after resize.

Note: Calling this method once and assigning the new values is faster than calling append() for every new element.

Reverses the order of all elements in the array.

int rfind(what: Variant, from: int = -1) const 🔗

Returns the index of the last occurrence of what in this array, or -1 if there are none. The search's start can be specified with from, continuing to the beginning of the array. This method is the reverse of find().

int rfind_custom(method: Callable, from: int = -1) const 🔗

Returns the index of the last element of the array that causes method to return true, or -1 if there are none. The search's start can be specified with from, continuing to the beginning of the array. This method is the reverse of find_custom().

void set(index: int, value: Variant) 🔗

Sets the value of the element at the given index to the given value. This will not change the size of the array, it only changes the value at an index already in the array. This is the same as using the [] operator (array[index] = value).

Shuffles all elements of the array in a random order.

Note: Like many similar functions in the engine (such as @GlobalScope.randi() or pick_random()), this method uses a common, global random seed. To get a predictable outcome from this method, see @GlobalScope.seed().

Returns the number of elements in the array. Empty arrays ([]) always return 0. See also is_empty().

Array slice(begin: int, end: int = 2147483647, step: int = 1, deep: bool = false) const 🔗

Returns a new Array containing this array's elements, from index begin (inclusive) to end (exclusive), every step elements.

If either begin or end are negative, their value is relative to the end of the array.

If step is negative, this method iterates through the array in reverse, returning a slice ordered backwards. For this to work, begin must be greater than end.

If deep is true, all nested Array and Dictionary elements in the slice are duplicated from the original, recursively. See also duplicate().

Sorts the array in ascending order. The final order is dependent on the "less than" (<) comparison between elements.

Note: The sorting algorithm used is not stable. This means that equivalent elements (such as 2 and 2.0) may have their order changed when calling sort().

void sort_custom(func: Callable) 🔗

Sorts the array using a custom Callable.

func is called as many times as necessary, receiving two array elements as arguments. The function should return true if the first element should be moved before the second one, otherwise it should return false.

It may also be necessary to use this method to sort strings by natural order, with String.naturalnocasecmp_to(), as in the following example:

Note: In C#, this method is not supported.

Note: The sorting algorithm used is not stable. This means that values considered equal may have their order changed when calling this method.

Note: You should not randomize the return value of func, as the heapsort algorithm expects a consistent result. Randomizing the return value will result in unexpected behavior.

bool operator !=(right: Array) 🔗

Returns true if the array's size or its elements are different than right's.

Array operator +(right: Array) 🔗

Appends the right array to the left operand, creating a new Array. This is also known as an array concatenation.

Note: For existing arrays, append_array() is much more efficient than concatenation and assignment with the += operator.

bool operator <(right: Array) 🔗

Compares the elements of both arrays in order, starting from index 0 and ending on the last index in common between both arrays. For each pair of elements, returns true if this array's element is less than right's, false if this element is greater. Otherwise, continues to the next pair.

If all searched elements are equal, returns true if this array's size is less than right's, otherwise returns false.

bool operator <=(right: Array) 🔗

Compares the elements of both arrays in order, starting from index 0 and ending on the last index in common between both arrays. For each pair of elements, returns true if this array's element is less than right's, false if this element is greater. Otherwise, continues to the next pair.

If all searched elements are equal, returns true if this array's size is less or equal to right's, otherwise returns false.

bool operator ==(right: Array) 🔗

Compares the left operand Array against the right Array. Returns true if the sizes and contents of the arrays are equal, false otherwise.

bool operator >(right: Array) 🔗

Compares the elements of both arrays in order, starting from index 0 and ending on the last index in common between both arrays. For each pair of elements, returns true if this array's element is greater than right's, false if this element is less. Otherwise, continues to the next pair.

If all searched elements are equal, returns true if this array's size is greater than right's, otherwise returns false.

bool operator >=(right: Array) 🔗

Compares the elements of both arrays in order, starting from index 0 and ending on the last index in common between both arrays. For each pair of elements, returns true if this array's element is greater than right's, false if this element is less. Otherwise, continues to the next pair.

If all searched elements are equal, returns true if this array's size is greater or equal to right's, otherwise returns false.

Variant operator [](index: int) 🔗

Returns the Variant element at the specified index. Arrays start at index 0. If index is greater or equal to 0, the element is fetched starting from the beginning of the array. If index is a negative value, the element is fetched starting from the end. Accessing an array out-of-bounds will cause a run-time error, pausing the project execution if run from the editor.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
var array = ["First", 2, 3, "Last"]
print(array[0])  # Prints "First"
print(array[2])  # Prints 3
print(array[-1]) # Prints "Last"

array[1] = "Second"
print(array[1])  # Prints "Second"
print(array[-3]) # Prints "Second"

# This typed array can only contain integers.
# Attempting to add any other type will result in an error.
var typed_array: Array[int] = [1, 2, 3]
```

Example 2 (typescript):
```typescript
Godot.Collections.Array array = ["First", 2, 3, "Last"];
GD.Print(array[0]); // Prints "First"
GD.Print(array[2]); // Prints 3
GD.Print(array[^1]); // Prints "Last"

array[1] = "Second";
GD.Print(array[1]); // Prints "Second"
GD.Print(array[^3]); // Prints "Second"

// This typed array can only contain integers.
// Attempting to add any other type will result in an error.
Godot.Collections.Array<int> typedArray = [1, 2, 3];
```

Example 3 (gdscript):
```gdscript
class_name Sword
extends Node

class Stats:
    pass

func _ready():
    var a = Array([], TYPE_INT, "", null)               # Array[int]
    var b = Array([], TYPE_OBJECT, "Node", null)        # Array[Node]
    var c = Array([], TYPE_OBJECT, "Node", Sword)       # Array[Sword]
    var d = Array([], TYPE_OBJECT, "RefCounted", Stats) # Array[Stats]
```

Example 4 (swift):
```swift
var numbers: Array[float] = []
var children: Array[Node] = [$Node, $Sprite2D, $RigidBody3D]

var integers: Array[int] = [0.2, 4.5, -2.0]
print(integers) # Prints [0, 4, -2]
```

---

## AR / Passthrough

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/ar_passthrough.html

**Contents:**
- AR / Passthrough
- Environment blend modes
- Configuring your background
- OpenXR specific
- Putting it together
- Shadow to opacity
- User-contributed notes

Augmented Reality is supported through various methods depending on the capabilities of the hardware.

Headsets such as the Magic Leap and glasses such as TiltFive show the rendered result on see-through displays allowing the user to see the real world.

Headsets such as the Quest, HTC Elite, and Lynx R1 implement this through a technique called video passthrough, where cameras record the real world and these images are used as the background on top of which our rendered result is used.

Passthrough is implemented very differently across platforms.

In Godot 4.3 we have implemented a unified approach that is explained on this help page so you don't need to worry about these differences, the XRInterface implementation is now responsible for applying the correct platform-dependent method [1].

For headsets such as the Meta Quest and HTC Elite you will need to use the OpenXR vendors plugin v3.0.0 or later to enable video passthrough.

For backwards compatibility the old API for passthrough is still available but it is recommended to follow the new instructions below.

The way we configure VR or AR functionality is through setting the environment blend mode. This mode determines how the (real world) environment is blended with the virtual world.

XR_ENV_BLEND_MODE_OPAQUE

The rendered image is opaque, we do not see the real world. We're in VR mode. This will turn off passthrough if video-passthrough is used.

XR_ENV_BLEND_MODE_ADDITIVE

The rendered image is added to the real world and will look semi transparent. This mode is generally used with see-through devices that are unable to obscure the real world. This will turn on passthrough if video-passthrough is used.

XR_ENV_BLEND_MODE_ALPHA_BLEND

The rendered image is alpha blended with the real world. On see-through devices that support this, the alpha will control the translucency of the optics. On video-passthrough devices alpha blending is applied with the video image. passthrough will also be enabled if applicable.

You can set the environment blend mode for your application through the environment_blend_mode property of the XRInterface instance.

You can query the supported blend modes on the hardware using the get_supported_environment_blend_modes property on the same instance.

When setting the blend mode to XR_ENV_BLEND_MODE_ALPHA_BLEND you must set the transparent_bg property on Viewport to true. When using the XR_ENV_BLEND_MODE_ADDITIVE blend mode you should set your background color to black.

Either solution will result in the background rendering not contributing to lighting. It is thus also recommended you adjust your environment settings accordingly and ensure there is adequate ambient light set to illuminate your scene.

Some AR SDKs do provide ambient lighting information or even provide a full radiance map to allow for real world reflections in your virtual objects. The core Godot XR functionality doesn't currently have support for this, however this functionality can be exposed through plugins.

In OpenXR you can configure the default blend mode you want to use. Godot will select this blend mode at startup if available. If not available Godot will default to the first supported blend mode provided by the XR runtime.

For passthrough devices OpenXR requires additional settings to be configured. These settings are platform-dependent and provided through the OpenXR vendors plugin.

For example, these are the settings required on Meta Quest:

The Passthrough setting defines whether passthrough is supported or even required.

The Boundary Mode allows you to define whether the guardian is needed, disabling this fully requires passthrough to be enabled at all times.

Putting the above together we can use the following code as a base:

Shadow to opacity is a render mode for Godot spatial shaders that was introduced in Godot 3 specifically for AR. It is a special render mode where the more a surface is in shadow, the more opaque the surface becomes. When a surface is fully lit, the surface becomes fully transparent and thus shows the real world.

However the surface is rendered during the opaque state effectively. This has two consequences:

As both the depth buffer and color buffer are written to, we occlude any geometry behind our surface even when fully transparent.

As we are making the surface opaque if in shadow, we can have virtual objects cast shadows on real world objects [2].

Image showing shadow to opacity being used to show the user's desk.

This enabled the following use cases:

You can render a box mesh around a real world table, this ensures the table remains visible even if a virtual object is placed underneath it. The virtual object will be correctly occluded. Placing a virtual object on top of the real world table, will result in a shadow being cast on the table.

You can use a shader with this render mode when render a hand mesh using the hand tracking functionality, and ensure your hands properly occlude virtual objects.

The following shader code is a good base for this functionality:

Restrictions may apply depending on XR interface implementation.

This feature is still being perfected.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
@onready var viewport : Viewport = get_viewport()
@onready var environment : Environment = $WorldEnvironment.environment

func switch_to_ar() -> bool:
    var xr_interface: XRInterface = XRServer.primary_interface
    if xr_interface:
        var modes = xr_interface.get_supported_environment_blend_modes()
        if XRInterface.XR_ENV_BLEND_MODE_ALPHA_BLEND in modes:
            xr_interface.environment_blend_mode = XRInterface.XR_ENV_BLEND_MODE_ALPHA_BLEND
            viewport.transparent_bg = true
        elif XRInterface.XR_ENV_BLEND_MODE_ADDITIVE in modes:
            xr_interface.environment_blend_mode = XRInterface.XR_ENV_BLEND_MODE_ADDITIVE
            viewport.transparent_bg = false
    else:
        return false

    environment.background_mode = Environment.BG_COLOR
    environment.background_color = Color(0.0, 0.0, 0.0, 0.0)
    environment.ambient_light_source = Environment.AMBIENT_SOURCE_COLOR
    return true

func switch_to_vr() -> bool:
    var xr_interface: XRInterface = XRServer.primary_interface
    if xr_interface:
        var modes = xr_interface.get_supported_environment_blend_modes()
        if XRInterface.XR_ENV_BLEND_MODE_OPAQUE in modes:
            xr_interface.environment_blend_mode = XRInterface.XR_ENV_BLEND_MODE_OPAQUE
        else:
            return false

    viewport.transparent_bg = false
    environment.background_mode = Environment.BG_SKY
    environment.ambient_light_source = Environment.AMBIENT_SOURCE_BG
    return true
```

Example 2 (cpp):
```cpp
shader_type spatial;
render_mode blend_mix, depth_draw_opaque, cull_back, shadow_to_opacity;

void fragment() {
    ALBEDO = vec3(0.0, 0.0, 0.0);
}
```

---

## A better XR start script

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/a_better_xr_start_script.html

**Contents:**
- A better XR start script
- Signals for our script
- Variables for our script
- Our updated ready function
- On session begun
- On visible state
- On focussed state
- On stopping state
- On pose recentered
- User-contributed notes

In Setting up XR we introduced a startup script that initialises our setup which we used as our script on our main node. This script performs the minimum steps required for any given interface.

When using OpenXR there are a number of improvements we should do here. For this we've created a more elaborate starting script. You will find these used in our demo projects.

Alternatively, if you are using XR Tools (see Introducing XR tools) it contains a version of this script updated with some features related to XR tools.

Below we will detail out the script used in our demos and explain the parts that are added.

We are introducing 3 signals to our script so that our game can add further logic:

focus_lost is emitted when the player takes off their headset or when the player enters the menu system of the headset.

focus_gained is emitted when the player puts their headset back on or exits the menu system and returns to the game.

pose_recentered is emitted when the headset requests the player's position to be reset.

Our game should react accordingly to these signals.

We introduce a few new variables to our script as well:

maximum_refresh_rate will control the headsets refresh rate if this is supported by the headset.

xr_interface holds a reference to our XR interface, this already existed but we now type it to get full access to our XRInterface API.

xr_is_focussed will be set to true whenever our game has focus.

We add a few things to the ready function.

If we're using the mobile or forward+ renderer we set the viewport's vrs_mode to VRS_XR. On platforms that support this, this will enable foveated rendering.

If we're using the compatibility renderer, we check if the OpenXR foveated rendering settings are configured and if not, we output a warning. See OpenXR Settings for further details.

We hook up a number of signals that will be emitted by the XRInterface. We'll provide more detail about these signals as we implement them.

We also quit our application if we couldn't successfully initialise OpenXR. Now this can be a choice. If you are making a mixed mode game you setup the VR mode of your game on success, and setup the non-VR mode of your game on failure. However, when running a VR only application on a standalone headset, it is nicer to exit on failure than to hang the system.

This signal is emitted by OpenXR when our session is setup. This means the headset has run through setting everything up and is ready to begin receiving content from us. Only at this time various information is properly available.

The main thing we do here is to check our headset's refresh rate. We also check the available refresh rates reported by the XR runtime to determine if we want to set our headset to a higher refresh rate.

Finally we match our physics update rate to our headset update rate. Godot runs at a physics update rate of 60 updates per second by default while headsets run at a minimum of 72, and for modern headsets often up to 144 frames per second. Not matching the physics update rate will cause stuttering as frames are rendered without objects moving.

This signal is emitted by OpenXR when our game becomes visible but is not focused. This is a bit of a weird description in OpenXR but it basically means that our game has just started and we're about to switch to the focused state next, that the user has opened a system menu or the user has just took their headset off.

On receiving this signal we'll update our focused state, we'll change the process mode of our node to disabled which will pause processing on this node and its children, and emit our focus_lost signal.

If you've added this script to your root node, this means your game will automatically pause when required. If you haven't, you can connect a method to the signal that performs additional changes.

While your game is in visible state because the user has opened a system menu, Godot will keep rendering frames and head tracking will remain active so your game will remain visible in the background. However controller and hand tracking will be disabled until the user exits the system menu.

This signal is emitted by OpenXR when our game gets focus. This is done at the completion of our startup, but it can also be emitted when the user exits a system menu, or put their headset back on.

Note also that when your game starts while the user is not wearing their headset, the game stays in 'visible' state until the user puts their headset on.

It is thus important to keep your game paused while in visible mode. If you don't the game will keep on running while your user isn't interacting with your game. Also when the game returns to the focused mode, suddenly all controller and hand tracking is re-enabled and could have game breaking consequences if you do not react to this accordingly. Be sure to test this behavior in your game!

While handling our signal we will update the focuses state, unpause our node and emit our focus_gained signal.

This signal is emitted by OpenXR when we enter our stop state. There are some differences between platforms when this happens. On some platforms this is only emitted when the game is being closed. But on other platforms this will also be emitted every time the player takes off their headset.

For now this method is only a place holder.

This signal is emitted by OpenXR when the user requests their view to be recentered. Basically this communicates to your game that the user is now facing forward and you should re-orient the player so they are facing forward in the virtual world.

As doing so is dependent on your game, your game needs to react accordingly.

All we do here is emit the pose_recentered signal. You can connect to this signal and implement the actual recenter code. Often it is enough to call center_on_hmd().

And that finished our script. It was written so that it can be re-used over multiple projects. Just add it as the script on your main node (and extend it if needed) or add it on a child node specific for this script.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Node3D

signal focus_lost
signal focus_gained
signal pose_recentered

...
```

Example 2 (json):
```json
using Godot;

public partial class MyNode3D : Node3D
{
    [Signal]
    public delegate void FocusLostEventHandler();

    [Signal]
    public delegate void FocusGainedEventHandler();

    [Signal]
    public delegate void PoseRecenteredEventHandler();

...
```

Example 3 (swift):
```swift
...

@export var maximum_refresh_rate : int = 90

var xr_interface : OpenXRInterface
var xr_is_focussed = false

...
```

Example 4 (csharp):
```csharp
...

    [Export]
    public int MaximumRefreshRate { get; set; } = 90;

    private OpenXRInterface _xrInterface;

    private bool _xrIsFocused;

...
```

---

## Basic XR Locomotion

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/basic_xr_locomotion.html

**Contents:**
- Basic XR Locomotion
- Adding our player body
- Adding a floor
- Direct movement
- Teleport
- More advanced movement features
- User-contributed notes

For basic locomotion we're going to continue using our Godot XR Tools library. The library contains both basic movement features as more advanced features.

The first step we need to do is to add a helper node to our XROrigin3D node. Because XR supports roomscale tracking you can't simply add your XR setup to a CharacterBody3D node and expect things to work. You will run into trouble when the user moves around their physical space and is no longer standing in the center of their room. Godot XR Tools embeds the needed logic into a helper node called PlayerBody.

Select your XROrigin3D node and click on the Instantiate Child Scene button to add a child scene. Select addons/godot-xr-tools/player/player_body.tscn and add this node.

This node governs the in game movement of your character and will immediately react to gravity. So to prevent our player from infinitely falling down we'll quickly add a floor to our scene.

We start by adding a StaticBody3D node to our root node and we rename this to Floor. We add a MeshInstance3D node as a child node for our Floor. Then create a new PlaneMesh as its mesh. For now we set the size of the mesh to 100 x 100 meters. Next we add a CollisionShape3D node as a child node for our Floor. Then create a BoxShape as our shape. We set the size of this box shape to 100 x 1 x 100 meters. We also need to move our collision shape down by 0.5 meters so the top of our box is flush with the floor.

To make it easier to see that we're actually moving around our world, a white floor isn't going to do it. Create a texture using Wahooneys excellent free texture generator. Once you've created the texture add it to your project. Then create a new material for the MeshInstance3D node, add your texture as the albedo, and enable Triplaner under UV1 in the material properties.

We're going to start adding some basic direct movement to our setup. This allows the user to move through the virtual world using joystick input.

It is important to note that moving through the virtual world while the player is standing still in the real world, can be nausea inducing especially for players who are new to VR. The default settings on our movement functions are fairly conservative. We advise you to stick to these defaults but offer features in game to enable less comfortable settings for more experienced users who are used to playing VR games.

We want to enable this on the right hand controller. We do this by adding a subscene to the right hand XRController3D node. Select addons/godot-xr-tools/functions/movement_direct.tscn as the scene to add.

This function adds forward and backwards movement to the player by using the joystick on the right hand controller. It has an option to also add left/right strafe but by default this is disabled.

Instead, we are going to add the ability for the player to also turn with this joystick. We will add another subscene to our controller node, select addons/godot-xr-tools/functions/movement_turn.tscn for this.

The turn system by default uses a snap turn approach. This means that turning happens in steps. This may seem jarring however it is a tried and tested method of combating motion sickness. You can easily switch to a mode that offers smooth turning by changing the mode property on the turn node.

If you run your game at this point in time you will find that you can move through the world freely using the right hand joystick.

An alternative to direct movement that some users find more pleasant is the ability to teleport to another location within your game world. Godot XR Tools supports this through the teleport function and we will be adding this to our left hand controller.

Add a new child scene to your left hand XRController3D node by selecting the addons/godot-xr-tools/functions/function_teleport.tscn scene.

With this scene added the player will be able to teleport around the world by pressing the trigger on the left hand controller, pointing where they want to go, and then releasing the trigger. The player can also adjust the orientation by using the left hand controller's joystick.

If you've followed all instructions correctly your scene should now look something like this:

Godot XR Tools adds many more movement features such as gliding, a grapple hook implementation, a jetpack, climbing mechanics, etc.

Most work similarly to the basic movement features we've handled so far, simply add the relevant subscene from the plugin to the controller that implements it.

We'll look at some of these in more detail later on in this tutorial where additional setup is required (such as climbing) but for others please look at Godot XR Tools own help pages for details.

Please read the User-contributed notes policy before submitting a comment.

---

## CompressedCubemapArray

**URL:** https://docs.godotengine.org/en/stable/classes/class_compressedcubemaparray.html

**Contents:**
- CompressedCubemapArray
- Description
- User-contributed notes

Inherits: CompressedTextureLayered < TextureLayered < Texture < Resource < RefCounted < Object

An optionally compressed CubemapArray.

A cubemap array that is loaded from a .ccubearray file. This file format is internal to Godot; it is created by importing other image formats with the import system. CompressedCubemapArray can use one of 4 compression methods:

Lossless (WebP or PNG, uncompressed on the GPU)

Lossy (WebP, uncompressed on the GPU)

VRAM Compressed (compressed on the GPU)

VRAM Uncompressed (uncompressed on the GPU)

Basis Universal (compressed on the GPU. Lower file sizes than VRAM Compressed, but slower to compress and lower quality than VRAM Compressed)

Only VRAM Compressed actually reduces the memory usage on the GPU. The Lossless and Lossy compression methods will reduce the required storage on disk, but they will not reduce memory usage on the GPU as the texture is sent to the GPU uncompressed.

Using VRAM Compressed also improves loading times, as VRAM-compressed textures are faster to load compared to textures using lossless or lossy compression. VRAM compression can exhibit noticeable artifacts and is intended to be used for 3D rendering, not 2D.

See CubemapArray for a general description of cubemap arrays.

Please read the User-contributed notes policy before submitting a comment.

---

## CSharpScript

**URL:** https://docs.godotengine.org/en/stable/classes/class_csharpscript.html

**Contents:**
- CSharpScript
- Description
- Tutorials
- Methods
- Method Descriptions
- User-contributed notes

Inherits: Script < Resource < RefCounted < Object

A script implemented in the C# programming language, saved with the .cs extension (Mono-enabled builds only).

This class represents a C# script. It is the C# equivalent of the GDScript class and is only available in Mono-enabled Godot builds.

C# documentation index

Variant new(...) vararg 🔗

Returns a new instance of the script.

Please read the User-contributed notes policy before submitting a comment.

---

## CubemapArray

**URL:** https://docs.godotengine.org/en/stable/classes/class_cubemaparray.html

**Contents:**
- CubemapArray
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: ImageTextureLayered < TextureLayered < Texture < Resource < RefCounted < Object

An array of Cubemaps, stored together and with a single reference.

CubemapArrays are made of an array of Cubemaps. Like Cubemaps, they are made of multiple textures, the amount of which must be divisible by 6 (one for each face of the cube).

The primary benefit of CubemapArrays is that they can be accessed in shader code using a single texture reference. In other words, you can pass multiple Cubemaps into a shader using a single CubemapArray. Cubemaps are allocated in adjacent cache regions on the GPU, which makes CubemapArrays the most efficient way to store multiple Cubemaps.

Godot uses CubemapArrays internally for many effects, including the Sky if you set ProjectSettings.rendering/reflections/sky_reflections/texture_array_reflections to true.

To create such a texture file yourself, reimport your image files using the Godot Editor import presets. To create a CubemapArray from code, use ImageTextureLayered.create_from_images() on an instance of the CubemapArray class.

The expected image order is X+, X-, Y+, Y-, Z+, Z- (in Godot's coordinate system, so Y+ is "up" and Z- is "forward"). You can use one of the following templates as a base:

2×3 cubemap template (default layout option)

Multiple layers are stacked on top of each other when using the default vertical import option (with the first layer at the top). Alternatively, you can choose a horizontal layout in the import options (with the first layer at the left).

Note: CubemapArray is not supported in the Compatibility renderer due to graphics API limitations.

create_placeholder() const

Resource create_placeholder() const 🔗

Creates a placeholder version of this resource (PlaceholderCubemapArray).

Please read the User-contributed notes policy before submitting a comment.

---

## Deploying to Android

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/deploying_to_android.html

**Contents:**
- Deploying to Android
- Setup
- Gradle Android build
- Installing the vendors plugin
- Creating the export presets
- Running on your device from the Godot editor
- User-contributed notes

Most standalone headsets run on Android and OpenXR support is making its way to these platforms.

Before following the OpenXR-specific instructions here, you'll need to first setup your system to export to Android in general, including:

Installing OpenJDK 17

Installing Android Studio

Configuring the location of the Android SDK in Godot

See Exporting for Android for the full details, and return here when you've finished these steps.

While the Mobile Vulkan renderer has many optimizations targeted at mobile devices, we're still working out the kinks. It is highly advisable to use the compatibility renderer (OpenGL) for the time being when targeting Android based XR devices.

Official support for the Android platform wasn't added to the OpenXR specification initially resulting in various vendors creating custom loaders to make OpenXR available on their headsets. While the long term expectation is that all vendors will adopt the official OpenXR loader, for now these loaders need to be added to your project.

In order to include the vendor-specific OpenXR loader into your project, you will need to setup a gradle Android build.

Select Install Android Build Template... from the Project menu:

This will create a folder called android inside of your project that contains all the runtime files needed on Android. You can now customize this installation. Godot won't show this in the editor but you can find it with a file browser.

You can read more about gradle builds here: Gradle builds for Android.

The vendors plugin can be downloaded from the asset library, search for "OpenXR vendors" and install the one named "Godot OpenXR Vendors plugin v4".

You will find the installed files inside the addons folder. Alternatively you can manually install the vendors plugin by downloading it from the release page here. You will need to copy the assets/addons/godotopenxrvendors folder from the zip file into your projects addons folder.

You can find the main repository of the vendors plugin here.

You will need to setup a separate export preset for each device, as each device will need its own loader included.

Open Project and select Export... Click on Add.. and select Android. Next change the name of the export preset for the device you're setting this up for, say Meta Quest. And enable Use Gradle Build. If you want to use one-click deploy (described below), ensure that Runnable is enabled.

If the vendors plugins were installed correctly you should find entries for the different headsets under XR Features. Change the XR Mode to OpenXR, then select the entry for your headset if you see one. If you don't see one enable the Khronos plugin.

Scroll to the bottom of the list and you'll find additional XR feature sections, currently only Meta XR Features, Pico XR Features, Magicleap XR Features and Khronos XR Features for HTC are available. You will need to select the appropriate settings if you wish to use these features.

If you've setup your export settings as described above, and your headset is connected to your computer and correctly recognized, you can launch it directly from the Godot editor using One-click deploy:

For some devices on some platforms, you may need to perform some extra steps in order for your device to be recognized correctly, so be sure to check the developer documentation from your headset vendor.

For example, with the Meta Quest 2, you need to enable developer mode on the headset, and if you're on Windows, you'll need to install special ADB drivers. See the official Meta Quest developer documentation for more details.

If you're having any issues with one-click deploy, check the Troubleshooting section.

Please read the User-contributed notes policy before submitting a comment.

---

## FontVariation

**URL:** https://docs.godotengine.org/en/stable/classes/class_fontvariation.html

**Contents:**
- FontVariation
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Font < Resource < RefCounted < Object

A variation of a font with additional settings.

Provides OpenType variations, simulated bold / slant, and additional font settings like OpenType features and extra spacing.

To use simulated bold font variant:

To set the coordinate of multiple variation axes:

Transform2D(1, 0, 0, 1, 0, 0)

set_spacing(spacing: SpacingType, value: int)

void set_base_font(value: Font)

Base font used to create a variation. If not set, default Theme font is used.

float baseline_offset = 0.0 🔗

void set_baseline_offset(value: float)

float get_baseline_offset()

Extra baseline offset (as a fraction of font height).

Dictionary opentype_features = {} 🔗

void set_opentype_features(value: Dictionary)

Dictionary get_opentype_features()

A set of OpenType feature tags. More info: OpenType feature tags.

int spacing_bottom = 0 🔗

void set_spacing(spacing: SpacingType, value: int)

Extra spacing at the bottom of the line in pixels.

int spacing_glyph = 0 🔗

void set_spacing(spacing: SpacingType, value: int)

Extra spacing between graphical glyphs.

int spacing_space = 0 🔗

void set_spacing(spacing: SpacingType, value: int)

Extra width of the space glyphs.

int spacing_top = 0 🔗

void set_spacing(spacing: SpacingType, value: int)

Extra spacing at the top of the line in pixels.

float variation_embolden = 0.0 🔗

void set_variation_embolden(value: float)

float get_variation_embolden()

If is not equal to zero, emboldens the font outlines. Negative values reduce the outline thickness.

Note: Emboldened fonts might have self-intersecting outlines, which will prevent MSDF fonts and TextMesh from working correctly.

int variation_face_index = 0 🔗

void set_variation_face_index(value: int)

int get_variation_face_index()

Active face index in the TrueType / OpenType collection file.

Dictionary variation_opentype = {} 🔗

void set_variation_opentype(value: Dictionary)

Dictionary get_variation_opentype()

Font OpenType variation coordinates. More info: OpenType variation tags.

Note: This Dictionary uses OpenType tags as keys. Variation axes can be identified both by tags (int, e.g. 0x77678674) and names (String, e.g. wght). Some axes might be accessible by multiple names. For example, wght refers to the same axis as weight. Tags on the other hand are unique. To convert between names and tags, use TextServer.name_to_tag() and TextServer.tag_to_name().

Note: To get available variation axes of a font, use Font.get_supported_variation_list().

Transform2D variation_transform = Transform2D(1, 0, 0, 1, 0, 0) 🔗

void set_variation_transform(value: Transform2D)

Transform2D get_variation_transform()

2D transform, applied to the font outlines, can be used for slanting, flipping and rotating glyphs.

For example, to simulate italic typeface by slanting, apply the following transform Transform2D(1.0, slant, 0.0, 1.0, 0.0, 0.0).

void set_spacing(spacing: SpacingType, value: int) 🔗

Sets the spacing for spacing to value in pixels (not relative to the font size).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var fv = FontVariation.new()
fv.base_font = load("res://BarlowCondensed-Regular.ttf")
fv.variation_embolden = 1.2
$Label.add_theme_font_override("font", fv)
$Label.add_theme_font_size_override("font_size", 64)
```

Example 2 (gdscript):
```gdscript
var fv = new FontVariation();
fv.SetBaseFont(ResourceLoader.Load<FontFile>("res://BarlowCondensed-Regular.ttf"));
fv.SetVariationEmbolden(1.2);
GetNode("Label").AddThemeFontOverride("font", fv);
GetNode("Label").AddThemeFontSizeOverride("font_size", 64);
```

Example 3 (gdscript):
```gdscript
var fv = FontVariation.new();
var ts = TextServerManager.get_primary_interface()
fv.base_font = load("res://BarlowCondensed-Regular.ttf")
fv.variation_opentype = { ts.name_to_tag("wght"): 900, ts.name_to_tag("custom_hght"): 900 }
```

---

## Godot Android library

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/android/android_library.html

**Contents:**
- Godot Android library
- Using the Godot Android library
- Godot Android plugins
- Embedding Godot in existing Android projects
  - 1. Create the Android app
  - 2. Create the Godot project
  - 3. Build and run the app
- User-contributed notes

The Godot Engine for Android platforms is designed to be used as an Android library. This architecture enables several key features on Android platforms:

Ability to integrate the Gradle build system within the Godot Editor, which provides the ability to leverage more components from the Android ecosystem such as libraries and tools

Ability to make the engine portable and embeddable:

Key in enabling the port of the Godot Editor to Android and mobile XR devices

Key in allowing the integration and reuse of Godot's capabilities within existing codebase

Below we describe some of the use-cases and scenarios this architecture enables.

The Godot Android library is packaged as an AAR archive file and hosted on MavenCentral along with its documentation.

It provides access to Godot APIs and capabilities on Android platforms for the following non-exhaustive use-cases.

Android plugins are powerful tools to extend the capabilities of the Godot Engine by tapping into the functionality provided by Android platforms and ecosystem.

An Android plugin is an Android library with a dependency on the Godot Android library which the plugin uses to integrate into the engine's lifecycle and to access Godot APIs, granting it powerful capabilities such as GDExtension support which allows to update / mod the engine behavior as needed.

For more information, see Godot Android plugins.

The Godot Engine can be embedded within existing Android applications or libraries, allowing developers to leverage mature and battle-tested code and libraries better suited to a specific task.

The hosting component is responsible for driving the engine lifecycle via Godot's Android APIs. These APIs can also be used to provide bidirectional communication between the host and the embedded Godot instance allowing for greater control over the desired experience.

We showcase how this is done using a sample Android app that embeds the Godot Engine as an Android view, and uses it to render 3D glTF models.

The GLTF Viewer sample app uses an Android RecyclerView component to create a list of glTF items, populated from Kenney's Food Kit pack. When an item on the list is selected, the app's logic interacts with the embedded Godot Engine to render the selected glTF item as a 3D model.

The sample app source code can be found on GitHub. Follow the instructions on its README to build and install it.

Below we break-down the steps used to create the GLTF Viewer app.

Currently only a single instance of the Godot Engine is supported per process. You can configure the process the Android Activity runs under using the android:process attribute.

Automatic resizing / orientation configuration events are not supported and may cause a crash. You can disable those events:

By locking to a specific orientation using the android:screenOrientation attribute.

By declaring that the Activity will handle these configuration events using the android:configChanges attribute.

The Android sample app was created using Android Studio and using Gradle as the build system.

The Android ecosystem provides multiple tools, IDEs, build systems for creating Android apps so feel free to use what you're familiar with, and update the steps below accordingly (contributions to this documentation are welcomed as well!).

Set up an Android application project. It may be a brand new empty project, or an existing project

Add the maven dependency for the Godot Android library

If using gradle, add the following to the dependency section of the app's gradle build file. Make sure to update <version> to the latest version of the Godot Android library:

If using gradle, include the following aaptOptions configuration under the android > defaultConfig section of the app's gradle build file. Doing so allows gradle to include Godot's hidden directories when building the app binary.

If your build system does not support including hidden directories, you can configure the Godot project to not use hidden directories by deselecting Application > Config > Use Hidden Project Data Directory in the Project Settings.

Create / update the application's Activity that will be hosting the Godot Engine instance. For the sample app, this is MainActivity

The host Activity should implement the GodotHost interface

The sample app uses Fragments to organize its UI, so it uses GodotFragment, a fragment component provided by the Godot Android library to automatically host and manage the Godot Engine instance.

The Godot Android library also provide GodotActivity, an Activity component that can be extended to automatically host and manage the Godot Engine instance.

Alternatively, applications can directly create a Godot instance, host and manage it themselves.

Using GodotHost#getHostPlugins(...), the sample app creates a runtime GodotPlugin instance that's used to send signals to the gdscript logic

The runtime GodotPlugin can also be used by gdscript logic to access JVM methods. For more information, see Godot Android plugins.

Add any additional logic that will be used by your application

For the sample app, this includes adding the ItemsSelectionFragment fragment (and related classes), a fragment used to build and show the list of glTF items

Open the AndroidManifest.xml file, and configure the orientation if needed using the android:screenOrientation attribute

If needed, disable automatic resizing / orientation configuration changes using the android:configChanges attribute

On Android, Godot's project files are exported to the assets directory of the generated apk binary.

We leverage that architecture to bind our Android app and Godot project together by creating the Godot project in the Android app's assets directory.

Note that it's also possible to create the Godot project in a separate directory and export it as a PCK or ZIP file to the Android app's assets directory. Using this approach requires passing the --main-pack <pck_or_zip_filepath_relative_to_assets_dir> argument to the hosted Godot Engine instance using GodotHost#getCommandLine().

The instructions below and the sample app follow the first approach of creating the Godot project in the Android app's assets directory.

As mentioned in the note above, open the Godot Editor and create a Godot project directly (no subfolder) in the assets directory of the Android application project

See the sample app's Godot project for reference

Configure the Godot project as desired

Make sure the orientation set for the Godot project matches the one set in the Android app's manifest

For Android, make sure textures/vram_compression/import_etc2_astc is set to true

Update the Godot project script logic as needed

For the sample app, the script logic queries for the runtime GodotPlugin instance and uses it to register for signals fired by the app logic

The app logic fires a signal every time an item is selected in the list. The signal contains the filepath of the glTF model, which is used by the gdscript logic to render the model.

Once you complete configuration of your Godot project, build and run the Android app. If set up correctly, the host Activity will initialize the embedded Godot Engine on startup. The Godot Engine will check the assets directory for project files to load (unless configured to look for a main pack), and will proceed to run the project.

While the app is running on device, you can check Android logcat to investigate any errors or crashes.

For reference, check the build and install instructions for the GLTF Viewer sample app.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (typescript):
```typescript
implementation("org.godotengine:godot:<version>")
```

Example 2 (typescript):
```typescript
android {

  defaultConfig {
      // The default ignore pattern for the 'assets' directory includes hidden files and
      // directories which are used by Godot projects, so we override it with the following.
      aaptOptions {
          ignoreAssetsPattern "!.svn:!.git:!.gitignore:!.ds_store:!*.scc:<dir>_*:!CVS:!thumbs.db:!picasa.ini:!*~"
      }
    ...
```

Example 3 (swift):
```swift
private var godotFragment: GodotFragment? = null

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)

    setContentView(R.layout.activity_main)

    val currentGodotFragment = supportFragmentManager.findFragmentById(R.id.godot_fragment_container)
    if (currentGodotFragment is GodotFragment) {
        godotFragment = currentGodotFragment
    } else {
        godotFragment = GodotFragment()
        supportFragmentManager.beginTransaction()
            .replace(R.id.godot_fragment_container, godotFragment!!)
            .commitNowAllowingStateLoss()
    }

    ...
```

Example 4 (jsx):
```jsx
<activity android:name=".MainActivity"
    android:screenOrientation="fullUser"
    android:configChanges="orientation|screenSize|smallestScreenSize|screenLayout"
    android:exported="true">

    ...
</activity>
```

---

## Godot Android plugins

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/android/android_plugin.html

**Contents:**
- Godot Android plugins
- Introduction
- Android plugin
  - v2 Architecture
  - v2 Packaging format
- Building a v2 Android plugin
  - Building a v2 Android plugin with GDExtension capabilities
  - Migrating a v1 Android plugin to v2
- Packaging a v2 Android plugin
  - Packaging a v2 Android plugin with GDExtension capabilities

Android plugins are powerful tools to extend the capabilities of the Godot engine by tapping into the functionality provided by Android platforms and ecosystem.

For example in Godot 4, Android plugins are used to support multiple Android-based XR platforms without encumbering the core codebase with vendor specific code or binaries.

Version 1 (v1) of the Android plugin system was introduced in Godot 3 and compatible with Godot 4.0 and 4.1. That version allowed developers to augment the Godot engine with Java, Kotlin and native functionality.

Starting in Godot 4.2, Android plugins built on the v1 architecture are now deprecated. Instead, Godot 4.2 introduces a new Version 2 (v2) architecture for Android plugins.

Godot Android plugin leverages the Gradle build system.

Building on the previous v1 architecture, Android plugins continue to be derived from the Android archive library.

At its core, a Godot Android plugin v2 is an Android library with a dependency on the Godot Android library, and a custom Android library manifest.

This architecture allows Android plugins to extend the functionality of the engine with:

Android platform APIs

Kotlin and Java libraries

Native libraries (via JNI)

GDExtension libraries

Each plugin has an init class extending from the GodotPlugin class which is provided by the Godot Android library.

The GodotPlugin class provides APIs to access the running Godot instance and hook into its lifecycle. It is loaded at runtime by the Godot engine.

v1 Android plugins required a custom gdap configuration file that was used by the Godot Editor to detect and load them. However this approach had several drawbacks, primary ones being that it lacked flexibility and departed from the existing Godot EditorExportPlugin format, delivery and installation flow.

This has been resolved for v2 Android plugins by deprecating the gdap packaging and configuration mechanism in favor of the existing Godot EditorExportPlugin packaging format. The EditorExportPlugin API in turn has been extended to properly support Android plugins.

A github project template is provided at https://github.com/m4gr3d/Godot-Android-Plugin-Template as a quickstart for building Godot Android plugins for Godot 4.2+. You can follow the template README to set up your own Godot Android plugin project.

To provide further understanding, here is a break-down of the steps used to create the project template:

Create an Android library module using these instructions

Add the Godot Android library as a dependency by updating the module's gradle build file:

The Godot Android library is hosted on MavenCentral, and updated for each release.

Create GodotAndroidPlugin, an init class for the plugin extending GodotPlugin.

If the plugin exposes Kotlin or Java methods to be called from GDScript, they must be annotated with @UsedByGodot. The name called from GDScript must match the method name exactly. There is no coercing snake_case to camelCase. For example, from GDScript:

If the plugin uses signals, the init class must return the set of signals used by overriding GodotPlugin::getPluginSignals(). To emit signals, the plugin can use the GodotPlugin::emitSignal(...) method.

Update the plugin AndroidManifest.xml file with the following meta-data:

PluginName is the name of the plugin

plugin.init.ClassFullName is the full component name (package + class name) of the plugin init class (e.g: org.godotengine.plugin.android.template.GodotAndroidPlugin).

Create the EditorExportPlugin configuration to package the plugin. The steps used to create the configuration can be seen in the Packaging a v2 Android plugin section.

Similar to GDNative support in v1 Android plugins, v2 Android plugins support the ability to integrate GDExtension capabilities.

A github project template is provided at https://github.com/m4gr3d/GDExtension-Android-Plugin-Template as a quickstart for building GDExtension Android plugins for Godot 4.2+. You can follow the template's README to set up your own Godot Android plugin project.

Use the following steps if you have a v1 Android plugin you want to migrate to v2:

Update the plugin's manifest file:

Change the org.godotengine.plugin.v1 prefix to org.godotengine.plugin.v2

Update the Godot Android library build dependency:

You can continue using the godot-lib.<version>.<status>.aar binary from Godot's download page if that's your preference. Make sure it's updated to the latest stable version.

Or you can switch to the MavenCentral provided dependency:

After updating the Godot Android library dependency, sync or build the plugin and resolve any compile errors:

The Godot instance provided by GodotPlugin::getGodot() no longer has access to an android.content.Context reference. Use GodotPlugin::getActivity() instead.

Delete the gdap configuration file(s) and follow the instructions in the Packaging a v2 Android plugin section to set up the plugin configuration.

As mentioned, a v2 Android plugin is now provided to the Godot Editor as an EditorExportPlugin plugin, so it shares a lot of the same packaging steps.

Add the plugin output binaries within the plugin directory (e.g: in addons/<plugin_name>/)

Add the tool script for the export functionality within the plugin directory (e.g: in addons/<plugin_name>/)

The created script must be a @tool script, or else it will not work properly

The export tool script is used to configure the Android plugin and hook it within the Godot Editor's export process. It should look something like this:

Create a plugin.cfg. This is an INI file with metadata about your plugin:

For reference, here is the folder structure for the Godot Android plugin project template. At build time, the contents of the export_scripts_template directory as well as the generated plugin binaries are copied to the addons/<plugin_name> directory:

For GDExtension, we follow the same steps as for Packaging a v2 Android plugin and add the GDExtension config file in the same location as plugin.cfg.

For reference, here is the folder structure for the GDExtension Android plugin project template. At build time, the contents of the export_scripts_template directory as well as the generated plugin binaries are copied to the addons/<plugin_name> directory:

Here is what the plugin.gdextension config file should look like:

Of note is the android_aar_plugin field that specifies this GDExtension module is provided as part of a v2 Android plugin. During the export process, this will indicate to the Godot Editor that the GDExtension native shared libraries are exported by the Android plugin AAR binaries.

For GDExtension Android plugins, the plugin init class must override GodotPlugin::getPluginGDExtensionLibrariesPaths(), and return the paths to the bundled GDExtension libraries config files (*.gdextension).

The paths must be relative to the Android library's assets directory. At runtime, the plugin will provide these paths to the Godot engine which will use them to load and initialize the bundled GDExtension libraries.

Godot 4.2 or higher is required

v2 Android plugin requires the use of the Gradle build process.

The provided github project templates include demo Godot projects for quick testing.

Copy the plugin's output directory (addons/<plugin_name>) to the target Godot project's directory

Open the project in the Godot Editor; the Editor should detect the plugin

Navigate to Project -> Project Settings... -> Plugins, and ensure the plugin is enabled

Install the Godot Android build template by clicking on Project -> Install Android Build Template...

Navigate to Project -> Export...

In the Export window, create an Android export preset

In the Android export preset, scroll to Gradle Build and set Use Gradle Build to true

Update the project's scripts as needed to access the plugin's functionality. For example:

Connect an Android device to your machine and run the project on it

Since they are also Android libraries, Godot v2 Android plugins can be stripped from their EditorExportPlugin packaging and provided as raw AAR binaries for use as libraries alongside the Godot Android library by Android apps.

If targeting this use-case, make sure to include additional instructions for how the AAR binaries should be included (e.g: custom additions to the Android app's manifest).

Godot Android Plugins Samples

Godot Android Plugin Template

GDExtension Android Plugin Template

To make it easier to access the exposed Java / Kotlin APIs in the Godot Editor, it's recommended to provide one (or multiple) gdscript wrapper class(es) for your plugin users to interface with.

If planning to use the GDExtension functionality in the Godot Editor, it is recommended that the GDExtension's native binaries are compiled not just for Android, but also for the OS onto which developers / users intend to run the Godot Editor. Not doing so may prevent developers / users from writing code that accesses the plugin from within the Godot Editor.

This may involve creating dummy plugins for the host OS just so the API is published to the editor. You can use the godot-cpp-template github template for reference on how to do so.

Check adb logcat for possible problems, then:

Check that the methods exposed by the plugin used the following Java types: void, boolean, int, float, java.lang.String, org.godotengine.godot.Dictionary, int[], byte[], float[], java.lang.String[].

More complex datatypes are not supported for now.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (json):
```json
dependencies {
    implementation("org.godotengine:godot:4.2.0.stable")
}
```

Example 2 (gdscript):
```gdscript
if Engine.has_singleton("MyPlugin"):
    var singleton = Engine.get_singleton("MyPlugin")
    print(singleton.myPluginFunction("World"))
```

Example 3 (typescript):
```typescript
<meta-data
    android:name="org.godotengine.plugin.v2.[PluginName]"
    android:value="[plugin.init.ClassFullName]" />
```

Example 4 (json):
```json
dependencies {
    implementation("org.godotengine:godot:4.2.0.stable")
}
```

---

## HScrollBar

**URL:** https://docs.godotengine.org/en/stable/classes/class_hscrollbar.html

**Contents:**
- HScrollBar
- Description
- User-contributed notes

Inherits: ScrollBar < Range < Control < CanvasItem < Node < Object

A horizontal scrollbar that goes from left (min) to right (max).

A horizontal scrollbar, typically used to navigate through content that extends beyond the visible width of a control. It is a Range-based control and goes from left (min) to right (max).

Please read the User-contributed notes policy before submitting a comment.

---

## Importing images

**URL:** https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_images.html

**Contents:**
- Importing images
- Supported image formats
- Importing textures
  - Changing import type
  - Detect 3D
- Import options
  - Compress > Mode
  - Compress > High Quality
  - Compress > HDR Compression
  - Compress > Normal Map

Godot can import the following image formats:

BMP (.bmp) - No support for 16-bit per pixel images. Only 1-bit, 4-bit, 8-bit, 24-bit, and 32-bit per pixel images are supported.

DirectDraw Surface (.dds) - If mipmaps are present in the texture, they will be loaded directly. This can be used to achieve effects using custom mipmaps.

Khronos Texture (.ktx) - Decoding is done using libktx. Only supports 2D images. Cubemaps, texture arrays and de-padding are not supported.

OpenEXR (.exr) - Supports HDR (highly recommended for panorama skies).

Radiance HDR (.hdr) - Supports HDR (highly recommended for panorama skies).

JPEG (.jpg, .jpeg) - Doesn't support transparency per the format's limitations.

PNG (.png) - Precision is limited to 8 bits per channel upon importing (no HDR images).

Truevision Targa (.tga)

SVG (.svg) - SVGs are rasterized using ThorVG when importing them. Support is limited; complex vectors may not render correctly. Text must be converted to paths; otherwise, it won't appear in the rasterized image. You can check whether ThorVG can render a certain vector correctly using its web-based viewer. For complex vectors, rendering them to PNGs using Inkscape is often a better solution. This can be automated thanks to its command-line interface.

WebP (.webp) - WebP files support transparency and can be compressed lossily or losslessly. The precision is limited to 8 bits per channel.

If you've compiled the Godot editor from source with specific modules disabled, some formats may not be available.

The default action in Godot is to import images as textures. Textures are stored in video memory. Their pixel data can't be accessed directly from the CPU without converting them back to an Image in a script. This is what makes drawing them efficient.

There are over a dozen import options that can be adjusted after selecting an image in the FileSystem dock:

Import options in the Import dock after selecting an image in the FileSystem dock. Some of these options are only visible with certain compression modes.

It is possible to choose other types of imported resources in the Import dock:

BitMap: 1-bit monochrome texture (intended to be used as a click mask in TextureButton and TouchScreenButton). This resource type cannot be displayed directly onto 2D or 3D nodes, but the pixel values can be queried from a script using get_bit.

Cubemap: Import the texture as a 6-sided cubemap, with interpolation between the cubemap's sides (seamless cubemaps), which can be sampled in custom shaders.

CubemapArray: Import the texture as a collection of 6-sided cubemaps, which can be sampled in custom shaders. This resource type can only be displayed when using the Forward+ or Mobile renderers, not the Compatibility renderer.

Font Data (Monospace Image Font): Import the image as a bitmap font where all characters have the same width. See Using Fonts.

Image: Import the image as-is. This resource type cannot be displayed directly onto 2D or 3D nodes, but the pixel values can be queried from a script using get_pixel.

Texture2D: Import the image as a 2-dimensional texture, suited for display on 2D and 3D surfaces. This is the default import mode.

Texture2DArray: Import the image as a collection of 2-dimensional textures. Texture2DArray is similar to a 3-dimensional texture, but without interpolation between layers. Built-in 2D and 3D shaders cannot display texture arrays, so you must create a custom shader in 2D or 3D to display a texture from a texture array.

Texture3D: Import the image as a 3-dimensional texture. This is not a 2D texture applied onto a 3D surface. Texture3D is similar to a texture array, but with interpolation between layers. Texture3D is typically used for FogMaterial density maps in volumetric fog, particle attractor vector fields, Environment 3D LUT color correction, and custom shaders.

TextureAtlas: Import the image as an atlas of different textures. Can be used to reduce memory usage for animated 2D sprites. Only supported in 2D due to missing support in built-in 3D shaders.

For Cubemap, the expected image order is X+, X-, Y+, Y-, Z+, Z- (in Godot's coordinate system, so Y+ is "up" and Z- is "forward"). Here are templates you can use for cubemap images (right-click > Save Link As…):

2×3 cubemap template (default layout option)

The default import options (no mipmaps and Lossless compression) are suited for 2D, but are not ideal for most 3D projects. Detect 3D makes Godot aware of when a texture is used in a 3D scene (such as a texture in a BaseMaterial3D). If this happens, several import options are changed so the texture flags are friendlier to 3D. Mipmaps are enabled and the compression mode is changed to VRAM Compressed unless Detect 3D > Compress To is changed. The texture is also reimported automatically.

A message is printed to the Output panel when a texture is detected to be used in 3D.

If you run into quality issues when a texture is detected to be used in 3D (e.g. for pixel art textures), change the Detect 3D > Compress To option before using the texture in 3D, or change Compress > Mode to Lossless after using the texture in 3D. This is preferable to disabling Detect 3D, as mipmap generation remains enabled to prevent textures from looking grainy at a distance.

In Godot 4.0, changing the texture filter and repeat mode is no longer done in the import options.

Instead, texture filter and repeat modes are changed in the CanvasItem properties in 2D (with a project setting acting as a default), and in a per-material configuration in 3D. In custom shaders, filter and repeat mode is changed on the sampler2D uniform using hints described in the Shading language documentation.

Images are one of the largest assets in a game. To handle them efficiently, they need to be compressed. Godot offers several compression methods, depending on the use case.

Lossless: This is the default and most common compression mode for 2D assets. It shows assets without any kind of artifacting, and disk compression is decent. It will use considerably more amount of video memory than VRAM Compression, though. This is also the recommended setting for pixel art.

Lossy: This is a good choice for large 2D assets. It has some artifacts, but less than VRAM compression and the file size is several times lower compared to Lossless or VRAM Uncompressed. Video memory usage isn't decreased by this mode; it's the same as with Lossless or VRAM Uncompressed.

VRAM Compressed: This is the default and most common compression mode for 3D assets. Size on disk is reduced and video memory usage is also decreased considerably (usually by a factor between 4 and 6). This mode should be avoided for 2D as it exhibits noticeable artifacts, especially for lower-resolution textures.

VRAM Uncompressed: Only useful for formats that can't be compressed, such as raw floating-point images.

Basis Universal: This alternative VRAM compression mode encodes the texture to a format that can be transcoded to most GPU-compressed formats at load-time. This provides very small files that make use of VRAM compression, at the cost of lower quality compared to VRAM Compressed and slow compression times. VRAM usage is usually the same as VRAM Compressed. Basis Universal does not support floating-point image formats (the engine will internally fall back to VRAM Compressed instead).

Even in 3D, "pixel art" textures should have VRAM compression disabled as it will negatively affect their appearance, without improving performance significantly due to their low resolution.

In this table, each of the 5 options are described together with their advantages and disadvantages ( = best, = worst):

Stored as Lossless WebP / PNG

Stored as S3TC, BPTC or ETC2 depending on platform

Transcoded to VRAM Compressed format

Estimated memory usage for a single RGBA8 texture with mipmaps enabled:

In the above table, memory usage will be reduced by 25% for images that do not have an alpha channel (RGB8). Memory usage will be further decreased by 25% for images that have mipmaps disabled.

Notice how at larger resolutions, the impact of VRAM compression is much greater. With a 4:1 compression ratio (6:1 for opaque textures with S3TC), VRAM compression effectively allows a texture to be twice as large on each axis, while using the same amount of memory on the GPU.

VRAM compression also reduces the memory bandwidth required to sample the texture, which can speed up rendering in memory bandwidth-constrained scenarios (which are frequent on integrated graphics and mobile). These factors combined make VRAM compression a must-have for 3D games with high-resolution textures.

You can preview how much memory a texture takes by double-clicking it in the FileSystem dock, then looking at the Inspector:

Previewing a texture in the Inspector. Credit: Red Brick 03 - Poly Haven

High-quality VRAM texture compression is only supported in the Forward+ and Mobile renderers.

When using the Compatibility renderer, this option is always considered disabled.

If enabled, uses BPTC compression on desktop platforms and ASTC compression on mobile platforms. When using BPTC, BC7 is used for SDR textures and BC6H is used for HDR textures.

If disabled (default), uses the faster but lower-quality S3TC compression on desktop platforms and ETC2 on mobile/web platforms. When using S3TC, DXT1 (BC1) is used for opaque textures and DXT5 (BC3) is used for transparent or normal map (RGTC) textures.

BPTC and ASTC support VRAM compression for HDR textures, but S3TC and ETC2 do not (see HDR Compression below).

This option only has an effect on textures that are imported as HDR formats in Godot (.hdr and .exr files).

If set to Disabled, never uses VRAM compression for HDR textures, regardless of whether they're opaque or transparent. Instead, the texture is converted to RGBE9995 (9-bits per channel + 5-bit exponent = 32 bits per pixel) to reduce memory usage compared to a half-float or single-precision float image format.

If set to Opaque Only (default), only uses VRAM compression for opaque HDR textures. This is due to a limitation of HDR formats, as there is no VRAM-compressed HDR format that supports transparency at the same time.

If set to Always, will force VRAM compression even for HDR textures with an alpha channel. To perform this, the alpha channel is discarded on import.

When using a texture as normal map, only the red and green channels are required. Given regular texture compression algorithms produce artifacts that don't look that nice in normal maps, the RGTC compression format is the best fit for this data. Forcing this option to Enable will make Godot import the image as RGTC compressed. By default, it's set to Detect. This means that if the texture is ever detected to be used as a normal map, it will be changed to Enable and reimported automatically.

Note that RGTC compression affects the resulting normal map image. You will have to adjust custom shaders that use the normal map's blue channel to take this into account. Built-in material shaders already ignore the blue channel in a normal map (regardless of the actual normal map's contents).

In the example below, the normal map with RGTC compression is able to preserve its detail much better, while using the same amount of memory as a standard RGBA VRAM-compressed texture:

Normal map with standard VRAM compression (left) and with RGTC VRAM compression (right)

Godot requires the normal map to use the X+, Y+ and Z+ coordinates, which is known as an OpenGL-style normal map. If you've imported a material made to be used with another engine, it may be DirectX-style. In this case, the normal map needs to be converted by enabling the Normal Map Invert Y import option.

More information about normal maps (including a coordinate order table for popular engines) can be found here.

If set to sRGB Friendly (default), prevents the RG color format from being used as it does not support sRGB color.

If set to Optimized, allows the RG color format to be used if the texture does not use the blue channel.

A third option Normal Map (RG Channels) is only available in layered textures (Cubemap, CubemapArray, Texture2DArray and Texture3D). This forces all layers from the texture to be imported with the RG color format, with only the red and green channels preserved. RGTC compression is able to preserve its detail much better, while using the same amount of memory as a standard RGBA VRAM-compressed texture. This only has an effect on textures with the VRAM Compressed or Basis Universal compression modes.

If enabled, smaller versions of the texture are generated on import. For example, a 64×64 texture will generate 6 mipmaps (32×32, 16×16, 8×8, 4×4, 2×2, 1×1). This has several benefits:

Textures will not become grainy in the distance (in 3D), or if scaled down due to camera zoom or CanvasItem scale (in 2D).

Performance will improve if the texture is displayed in the distance, since sampling smaller versions of the original texture is faster and requires less memory bandwidth.

The downside of mipmaps is that they increase memory usage by roughly 33%.

It's recommended to enable mipmaps in 3D. However, in 2D, this should only be enabled if your project visibly benefits from having mipmaps enabled. If the camera never zooms out significantly, there won't be a benefit to enabling mipmaps but memory usage will increase.

Mipmaps > Limit is currently not implemented and has no effect when changed.

If set to a value greater than -1, limits the maximum number of mipmaps that can be generated. This can be decreased if you don't want textures to become too low-resolution at extreme distances, at the cost of some graininess.

The color channel to consider as a roughness map in this texture. Only effective if Roughness > Src Normal is not empty.

The path to the texture to consider as a normal map for roughness filtering on import. Specifying this can help decrease specular aliasing slightly in 3D.

Roughness filtering on import is only used in 3D rendering, not 2D.

This puts pixels of the same surrounding color in transition from transparent to opaque areas. For textures displayed with bilinear filtering, this helps mitigate the outline effect when exporting images from an image editor.

It's recommended to leave this enabled (as it is by default), unless this causes issues for a particular image.

An alternative to fixing darkened borders with Fix Alpha Border is to use premultiplied alpha. By enabling this option, the texture will be converted to this format. A premultiplied alpha texture requires specific materials to be displayed correctly:

In 2D, a CanvasItemMaterial will need to be created and configured to use the Premul Alpha blend mode on CanvasItems that use this texture. In custom canvas item shaders, render_mode blend_premul_alpha; should be used.

In 3D, a BaseMaterial3D will need to be created and configured to use the Premul Alpha blend mode on materials that use this texture. In custom spatial shaders, render_mode blend_premul_alpha; should be used.

Godot requires the normal map to use the X+, Y+ and Z+ coordinates, which is known as an OpenGL-style normal map. If you've imported a material made to be used with another engine, it may be DirectX-style. In this case, the normal map needs to be converted by enabling the Normal Map Invert Y import option.

More information about normal maps (including a coordinate order table for popular engines) can be found here.

Some HDR images you can find online may be broken and contain sRGB color data (instead of linear color data). It is advised not to use those files. If you absolutely have to, enabling this option on will make them look correct.

Enabling HDR as sRGB on well-formatted HDR images will cause the resulting image to look too dark, so leave this disabled if unsure.

Some HDR panorama images you can find online may contain extremely bright pixels, due to being taken from real life sources without any clipping.

While these HDR panorama images are accurate to real life, this can cause the radiance map generated by Godot to contain sparkles when used as a background sky. This can be seen in material reflections (even on rough materials in extreme cases). Enabling HDR Clamp Exposure can resolve this using a smart clamping formula that does not introduce visible clipping – glow will keep working when looking at the background sky.

If set to a value greater than 0, the size of the texture is limited on import to a value smaller than or equal to the value specified here. For non-square textures, the size limit affects the longer dimension, with the shorter dimension scaled to preserve aspect ratio. Resizing is performed using cubic interpolation.

This can be used to reduce memory usage without affecting the source images, or avoid issues with textures not displaying on mobile/web platforms (as these usually can't display textures larger than 4096×4096).

This changes the Compress > Mode option that is used when a texture is detected as being used in 3D.

Changing this import option only has an effect if a texture is detected as being used in 3D. Changing this to Disabled then reimporting will not change the existing compress mode on a texture (if it's detected to be used in 3D), but choosing VRAM Compressed or Basis Universal will.

This is only available for SVG images.

The scale the SVG should be rendered at, with 1.0 being the original design size. Higher values result in a larger image. Note that unlike font oversampling, this affects the physical size the SVG is rendered at in 2D. See also Editor > Scale With Editor Scale below.

This is only available for SVG images.

If true, scales the imported image to match the editor's display scale factor. This should be enabled for editor plugin icons and custom class icons, but should be left disabled otherwise.

This is only available for SVG images.

If checked, converts the imported image's colors to match the editor's icon and font color palette. This assumes the image uses the exact same colors as Godot's own color palette for editor icons, with the source file designed for a dark editor theme. This should be enabled for editor plugin icons and custom class icons, but should be left disabled otherwise.

As the SVG library used in Godot doesn't support rasterizing text found in SVG images, text must be converted to a path first. Otherwise, text won't appear in the rasterized image.

There are two ways to achieve this in a non-destructive manner, so you can keep editing the original text afterwards:

Select your text object in Inkscape, then duplicate it in place by pressing Ctrl + D and use Path > Object to Path. Hide the original text object afterwards using the Layers and Objects dock.

Use the Inkscape command line to export an SVG from another SVG file with text converted to paths:

To support multiple resolutions with crisp visuals at high resolutions, you will need to use high-resolution source images (suited for the highest resolution you wish to support without blurriness, which is typically 4K in modern desktop games).

There are 2 ways to proceed:

Use a high base resolution in the project settings (such as 4K), then use the textures at original scale. This is an easier approach.

Use a low base resolution in the project settings (such as 1080p), then downscale textures when using them. This is often more difficult and can make various calculations in script tedious, so the approach described above is recommended instead.

After doing this, you may notice that textures become grainy at lower viewport resolutions. To resolve this, enable Mipmaps on textures used in 2D in the Import dock. This will increase memory usage.

Enabling mipmaps can also make textures appear blurrier, but you can choose to make textures sharper (at the cost of some graininess) by setting Rendering > Textures > Default Filters > Texture Mipmap Bias to a negative value.

While there's no "one size fits all" recommendation, here are some general recommendations for choosing texture sizes in 3D:

The size of a texture should be adjusted to have a consistent texel density compared to surrounding objects. While this cannot be ensured perfectly when sticking to power-of-two texture sizes, it's usually possible to keep texture detail fairly consistent throughout a 3D scene.

The smaller the object appears on screen, the smaller its texture should be. For example, a tree that only appears in the background doesn't need a texture resolution as high as other objects the player may be able to walk close to.

Using power-of-two texture sizes is recommended, but is not required. Textures don't have to be square – sizes such as 1024×512 are acceptable.

There are diminishing returns to using large texture sizes, despite the increased memory usage and loading times. Most modern 3D games not using a pixel art style stick to 2048×2048 textures on average, with 1024×1024 and 512×512 for textures spanning smaller surfaces.

When working with physically-based materials in 3D, you can reduce memory usage and file size without affecting quality too much by using a lower resolution for certain texture maps. This works especially well for textures that only feature low-frequency detail (such as a normal map for a snow texture).

If you have control over how the 3D models are created, these tips are also worth exploring:

When working with 3D models that are mostly symmetrical, you may be able to use mirrored UVs to double the effective texel density. This may look unnatural when used on human faces though.

When working with 3D models using a low-poly style and plain colors, you can rely on vertex colors instead of textures to represent colors on the model's surfaces.

Images can be loaded and saved at runtime using runtime file loading and saving, including from an exported project.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
inkscape --export-text-to-path --export-filename svg_with_text_converted_to_path.svg svg_with_text.svg
```

---

## Introducing XR tools

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/introducing_xr_tools.html

**Contents:**
- Introducing XR tools
- Installing XR Tools
- Basic hands
- More information
- User-contributed notes

Out of the box Godot gives you all the basic support to setup an XR project. XR specific game mechanics however need to be implemented on top of this foundation. While Godot makes this relatively easy this can still be a daunting task.

For this reason Godot has developed a toolkit called Godot XR Tools that implements many of the basic mechanics found in XR games, from locomotion to object interaction to UI interaction.

This toolkit is designed to work with both OpenXR and WebXR runtimes. We'll be using this as a base for our documentation here. It helps developers hit the ground running but for more specific use cases building your own logic is just as valid. In that case XR tools can help in providing inspiration.

Continuing on from our project we started in Setting up XR we want to add in the Godot XR Tools library. This can be downloaded from the Godot XR Tools releases page. Find the latest release for Godot 4, and under Assets, download the godot-xr-tools.zip file. You can also find it in the asset library with the title "Godot XR Tools for Godot 4".

If you're using the zip file, once it's downloaded unzip it. You will notice the files are held within a godot-xr-tools subfolder. Inside of this folder you will find an addons folder. It is this folder that you want to copy in its entirety to your Godot project folder. Your project should now look something like this:

Now open up your project in Godot, if you haven't already, and give it a minute or so to import all the resources of the plugin. If it asks for a path to Blender to be set you can just click the option to disable blender import and restart the editor.

After the import finishes you may notice that several "failed to load script" messages popped up, that's normal, the plugin just needs to be enabled in the project settings.

Next open the Project menu and select Project Settings... Now go to the Plugins tab and enable the plugin.

After doing that you need to close and re-open your project so everything is properly enabled.

Just to get a feel of things we're going to add a few standard components that dress up our scene starting with hands for our player.

OpenXR supports full hand tracking however there currently are significant differences in capabilities between the different XR Runtimes.

As a reliable alternative Godot XR Tools comes with a number of rigged hand scenes that react on trigger and grip inputs of your controller. These hands come in low and high poly versions, come in a few configurations, a number of animation files to control finger positions and a number of different textures.

In your scene tree select your left hand XRController3D node. Now click on the instantiate Child Scene button to add a child scene. Click the addons toggle so the addons folder can be searched. Then search for left_hand_low.tscn, and select it.

As you can see from the path of this scene, low poly models are in the lowpoly subfolder while high poly models are in the highpoly subfolder. You will want to use the low poly versions if you plan to release your game on mobile devices.

The default hand we chose is just a hand. The other options are:

tac_glove - the hand is wearing a glove with fingers exposed

full_glove - the hand is wearing a glove that covers the entire hand

Finally each hand comes in a physics version. This exposes all the bones. We'll look at how that can be used in another tutorial.

We repeat the same for the right hand.

We'll continue with adding features to our tutorial project using Godot XR tools in the next couple of pages. More detailed information about the toolkit can be found on the toolkits help pages.

Please read the User-contributed notes policy before submitting a comment.

---

## Marshalls

**URL:** https://docs.godotengine.org/en/stable/classes/class_marshalls.html

**Contents:**
- Marshalls
- Description
- Methods
- Method Descriptions
- User-contributed notes

Data transformation (marshaling) and encoding helpers.

Provides data transformation and encoding utility functions.

base64_to_raw(base64_str: String)

base64_to_utf8(base64_str: String)

base64_to_variant(base64_str: String, allow_objects: bool = false)

raw_to_base64(array: PackedByteArray)

utf8_to_base64(utf8_str: String)

variant_to_base64(variant: Variant, full_objects: bool = false)

PackedByteArray base64_to_raw(base64_str: String) 🔗

Returns a decoded PackedByteArray corresponding to the Base64-encoded string base64_str.

String base64_to_utf8(base64_str: String) 🔗

Returns a decoded string corresponding to the Base64-encoded string base64_str.

Variant base64_to_variant(base64_str: String, allow_objects: bool = false) 🔗

Returns a decoded Variant corresponding to the Base64-encoded string base64_str. If allow_objects is true, decoding objects is allowed.

Internally, this uses the same decoding mechanism as the @GlobalScope.bytes_to_var() method.

Warning: Deserialized objects can contain code which gets executed. Do not use this option if the serialized object comes from untrusted sources to avoid potential security threats such as remote code execution.

String raw_to_base64(array: PackedByteArray) 🔗

Returns a Base64-encoded string of a given PackedByteArray.

String utf8_to_base64(utf8_str: String) 🔗

Returns a Base64-encoded string of the UTF-8 string utf8_str.

String variant_to_base64(variant: Variant, full_objects: bool = false) 🔗

Returns a Base64-encoded string of the Variant variant. If full_objects is true, encoding objects is allowed (and can potentially include code).

Internally, this uses the same encoding mechanism as the @GlobalScope.var_to_bytes() method.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRActionBindingModifier

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxractionbindingmodifier.html

**Contents:**
- OpenXRActionBindingModifier
- Description
- User-contributed notes

Inherits: OpenXRBindingModifier < Resource < RefCounted < Object

Inherited By: OpenXRAnalogThresholdModifier

Binding modifier that applies on individual actions related to an interaction profile.

Binding modifier that applies on individual actions related to an interaction profile.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRActionMap

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxractionmap.html

**Contents:**
- OpenXRActionMap
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Collection of OpenXRActionSet and OpenXRInteractionProfile resources for the OpenXR module.

OpenXR uses an action system similar to Godots Input map system to bind inputs and outputs on various types of XR controllers to named actions. OpenXR specifies more detail on these inputs and outputs than Godot supports.

Another important distinction is that OpenXR offers no control over these bindings. The bindings we register are suggestions, it is up to the XR runtime to offer users the ability to change these bindings. This allows the XR runtime to fill in the gaps if new hardware becomes available.

The action map therefore needs to be loaded at startup and can't be changed afterwards. This resource is a container for the entire action map.

add_action_set(action_set: OpenXRActionSet)

add_interaction_profile(interaction_profile: OpenXRInteractionProfile)

create_default_action_sets()

find_action_set(name: String) const

OpenXRInteractionProfile

find_interaction_profile(name: String) const

get_action_set(idx: int) const

get_action_set_count() const

OpenXRInteractionProfile

get_interaction_profile(idx: int) const

get_interaction_profile_count() const

remove_action_set(action_set: OpenXRActionSet)

remove_interaction_profile(interaction_profile: OpenXRInteractionProfile)

Array action_sets = [] 🔗

void set_action_sets(value: Array)

Array get_action_sets()

Collection of OpenXRActionSets that are part of this action map.

Array interaction_profiles = [] 🔗

void set_interaction_profiles(value: Array)

Array get_interaction_profiles()

Collection of OpenXRInteractionProfiles that are part of this action map.

void add_action_set(action_set: OpenXRActionSet) 🔗

void add_interaction_profile(interaction_profile: OpenXRInteractionProfile) 🔗

Add an interaction profile.

void create_default_action_sets() 🔗

Setup this action set with our default actions.

OpenXRActionSet find_action_set(name: String) const 🔗

Retrieve an action set by name.

OpenXRInteractionProfile find_interaction_profile(name: String) const 🔗

Find an interaction profile by its name (path).

OpenXRActionSet get_action_set(idx: int) const 🔗

Retrieve the action set at this index.

int get_action_set_count() const 🔗

Retrieve the number of actions sets in our action map.

OpenXRInteractionProfile get_interaction_profile(idx: int) const 🔗

Get the interaction profile at this index.

int get_interaction_profile_count() const 🔗

Retrieve the number of interaction profiles in our action map.

void remove_action_set(action_set: OpenXRActionSet) 🔗

Remove an action set.

void remove_interaction_profile(interaction_profile: OpenXRInteractionProfile) 🔗

Remove an interaction profile.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRActionSet

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxractionset.html

**Contents:**
- OpenXRActionSet
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Collection of OpenXRAction resources that make up an action set.

Action sets in OpenXR define a collection of actions that can be activated in unison. This allows games to easily change between different states that require different inputs or need to reinterpret inputs. For instance we could have an action set that is active when a menu is open, an action set that is active when the player is freely walking around and an action set that is active when the player is controlling a vehicle.

Action sets can contain the same action with the same name, if such action sets are active at the same time the action set with the highest priority defines which binding is active.

add_action(action: OpenXRAction)

get_action_count() const

remove_action(action: OpenXRAction)

void set_actions(value: Array)

Collection of actions for this action set.

String localized_name = "" 🔗

void set_localized_name(value: String)

String get_localized_name()

The localized name of this action set.

void set_priority(value: int)

The priority for this action set.

void add_action(action: OpenXRAction) 🔗

Add an action to this action set.

int get_action_count() const 🔗

Retrieve the number of actions in our action set.

void remove_action(action: OpenXRAction) 🔗

Remove an action from this action set.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRAction

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxraction.html

**Contents:**
- OpenXRAction
- Description
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

This resource defines an OpenXR action. Actions can be used both for inputs (buttons, joysticks, triggers, etc.) and outputs (haptics).

OpenXR performs automatic conversion between action type and input type whenever possible. An analog trigger bound to a boolean action will thus return false if the trigger is depressed and true if pressed fully.

Actions are not directly bound to specific devices, instead OpenXR recognizes a limited number of top level paths that identify devices by usage. We can restrict which devices an action can be bound to by these top level paths. For instance an action that should only be used for hand held controllers can have the top level paths "/user/hand/left" and "/user/hand/right" associated with them. See the reserved path section in the OpenXR specification for more info on the top level paths.

Note that the name of the resource is used to register the action with.

ActionType OPENXR_ACTION_BOOL = 0

This action provides a boolean value.

ActionType OPENXR_ACTION_FLOAT = 1

This action provides a float value between 0.0 and 1.0 for any analog input such as triggers.

ActionType OPENXR_ACTION_VECTOR2 = 2

This action provides a Vector2 value and can be bound to embedded trackpads and joysticks.

ActionType OPENXR_ACTION_POSE = 3

There is currently no description for this enum. Please help us by contributing one!

ActionType action_type = 1 🔗

void set_action_type(value: ActionType)

ActionType get_action_type()

String localized_name = "" 🔗

void set_localized_name(value: String)

String get_localized_name()

The localized description of this action.

PackedStringArray toplevel_paths = PackedStringArray() 🔗

void set_toplevel_paths(value: PackedStringArray)

PackedStringArray get_toplevel_paths()

A collections of toplevel paths to which this action can be bound.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedStringArray for more details.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRAnalogThresholdModifier

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxranalogthresholdmodifier.html

**Contents:**
- OpenXRAnalogThresholdModifier
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: OpenXRActionBindingModifier < OpenXRBindingModifier < Resource < RefCounted < Object

The analog threshold binding modifier can modify a float input to a boolean input with specified thresholds.

The analog threshold binding modifier can modify a float input to a boolean input with specified thresholds.

See XR_VALVE_analog_threshold for in-depth details.

OpenXRHapticBase off_haptic 🔗

void set_off_haptic(value: OpenXRHapticBase)

OpenXRHapticBase get_off_haptic()

Haptic pulse to emit when the user releases the input.

float off_threshold = 0.4 🔗

void set_off_threshold(value: float)

float get_off_threshold()

When our input value falls below this, our output becomes false.

OpenXRHapticBase on_haptic 🔗

void set_on_haptic(value: OpenXRHapticBase)

OpenXRHapticBase get_on_haptic()

Haptic pulse to emit when the user presses the input.

float on_threshold = 0.6 🔗

void set_on_threshold(value: float)

float get_on_threshold()

When our input value is equal or larger than this value, our output becomes true. It stays true until it falls under the off_threshold value.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRAPIExtension

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrapiextension.html

**Contents:**
- OpenXRAPIExtension
- Description
- Tutorials
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Makes the OpenXR API available for GDExtension.

OpenXRAPIExtension makes OpenXR available for GDExtension. It provides the OpenXR API to GDExtension through the get_instance_proc_addr() method, and the OpenXR instance through get_instance().

It also provides methods for querying the status of OpenXR initialization, and helper methods for ease of use of the API with GDExtension.

XrResult documentation

XrInstance documentation

XrSpace documentation

XrSession documentation

XrSystemId documentation

xrBeginSession documentation

XrPosef documentation

action_get_handle(action: RID)

begin_debug_label_region(label_name: String)

end_debug_label_region()

find_action(name: String, action_set: RID)

get_error_string(result: int)

get_hand_tracker(hand_index: int)

get_instance_proc_addr(name: String)

get_next_frame_time()

get_predicted_display_time()

get_projection_layer()

get_render_state_z_far()

get_render_state_z_near()

get_supported_swapchain_formats()

get_swapchain_format_name(swapchain_format: int)

insert_debug_label(label_name: String)

OpenXRAlphaBlendModeSupport

is_environment_blend_mode_alpha_supported()

openxr_is_enabled(check_run_in_editor: bool) static

openxr_swapchain_acquire(swapchain: int)

openxr_swapchain_create(create_flags: int, usage_flags: int, swapchain_format: int, width: int, height: int, sample_count: int, array_size: int)

openxr_swapchain_free(swapchain: int)

openxr_swapchain_get_image(swapchain: int)

openxr_swapchain_get_swapchain(swapchain: int)

openxr_swapchain_release(swapchain: int)

register_composition_layer_provider(extension: OpenXRExtensionWrapper)

register_frame_info_extension(extension: OpenXRExtensionWrapper)

register_projection_views_extension(extension: OpenXRExtensionWrapper)

set_custom_play_space(space: const void*)

set_emulate_environment_blend_mode_alpha_blend(enabled: bool)

set_object_name(object_type: int, object_handle: int, object_name: String)

set_render_region(render_region: Rect2i)

set_velocity_depth_texture(render_target: RID)

set_velocity_target_size(target_size: Vector2i)

set_velocity_texture(render_target: RID)

transform_from_pose(pose: const void*)

unregister_composition_layer_provider(extension: OpenXRExtensionWrapper)

unregister_frame_info_extension(extension: OpenXRExtensionWrapper)

unregister_projection_views_extension(extension: OpenXRExtensionWrapper)

xr_result(result: int, format: String, args: Array)

enum OpenXRAlphaBlendModeSupport: 🔗

OpenXRAlphaBlendModeSupport OPENXR_ALPHA_BLEND_MODE_SUPPORT_NONE = 0

Means that XRInterface.XR_ENV_BLEND_MODE_ALPHA_BLEND isn't supported at all.

OpenXRAlphaBlendModeSupport OPENXR_ALPHA_BLEND_MODE_SUPPORT_REAL = 1

Means that XRInterface.XR_ENV_BLEND_MODE_ALPHA_BLEND is really supported.

OpenXRAlphaBlendModeSupport OPENXR_ALPHA_BLEND_MODE_SUPPORT_EMULATING = 2

Means that XRInterface.XR_ENV_BLEND_MODE_ALPHA_BLEND is emulated.

int action_get_handle(action: RID) 🔗

Returns the corresponding XrAction OpenXR handle for the given action RID.

void begin_debug_label_region(label_name: String) 🔗

Begins a new debug label region, this label will be reported in debug messages for any calls following this until end_debug_label_region() is called. Debug labels can be stacked.

Returns true if OpenXR is initialized for rendering with an XR viewport.

void end_debug_label_region() 🔗

Marks the end of a debug label region. Removes the latest debug label region added by calling begin_debug_label_region().

RID find_action(name: String, action_set: RID) 🔗

Returns the RID corresponding to an Action of a matching name, optionally limited to a specified action set.

String get_error_string(result: int) 🔗

Returns an error string for the given XrResult.

int get_hand_tracker(hand_index: int) 🔗

Returns the corresponding XRHandTrackerEXT handle for the given hand index value.

Returns the XrInstance created during the initialization of the OpenXR API.

int get_instance_proc_addr(name: String) 🔗

Returns the function pointer of the OpenXR function with the specified name, cast to an integer. If the function with the given name does not exist, the method returns 0.

Note: openxr/util.h contains utility macros for acquiring OpenXR functions, e.g. GDEXTENSION_INIT_XR_FUNC_V(xrCreateAction).

int get_next_frame_time() 🔗

Returns the predicted display timing for the next frame.

int get_play_space() 🔗

Returns the play space, which is an XrSpace cast to an integer.

int get_predicted_display_time() 🔗

Returns the predicted display timing for the current frame.

int get_projection_layer() 🔗

Returns a pointer to the render state's XrCompositionLayerProjection struct.

Note: This method should only be called from the rendering thread.

float get_render_state_z_far() 🔗

Returns the far boundary value of the camera frustum.

Note: This is only accessible in the render thread.

float get_render_state_z_near() 🔗

Returns the near boundary value of the camera frustum.

Note: This is only accessible in the render thread.

Returns the OpenXR session, which is an XrSession cast to an integer.

PackedInt64Array get_supported_swapchain_formats() 🔗

Returns an array of supported swapchain formats.

String get_swapchain_format_name(swapchain_format: int) 🔗

Returns the name of the specified swapchain format.

int get_system_id() 🔗

Returns the id of the system, which is an XrSystemId cast to an integer.

void insert_debug_label(label_name: String) 🔗

Inserts a debug label, this label is reported in any debug message resulting from the OpenXR calls that follows, until any of begin_debug_label_region(), end_debug_label_region(), or insert_debug_label() is called.

OpenXRAlphaBlendModeSupport is_environment_blend_mode_alpha_supported() 🔗

Returns OpenXRAlphaBlendModeSupport denoting if XRInterface.XR_ENV_BLEND_MODE_ALPHA_BLEND is really supported, emulated or not supported at all.

bool is_initialized() 🔗

Returns true if OpenXR is initialized.

Returns true if OpenXR is running (xrBeginSession was successfully called and the swapchains were created).

bool openxr_is_enabled(check_run_in_editor: bool) static 🔗

Returns true if OpenXR is enabled.

void openxr_swapchain_acquire(swapchain: int) 🔗

Acquires the image of the provided swapchain.

int openxr_swapchain_create(create_flags: int, usage_flags: int, swapchain_format: int, width: int, height: int, sample_count: int, array_size: int) 🔗

Returns a pointer to a new swapchain created using the provided parameters.

void openxr_swapchain_free(swapchain: int) 🔗

Destroys the provided swapchain and frees it from memory.

RID openxr_swapchain_get_image(swapchain: int) 🔗

Returns the RID of the provided swapchain's image.

int openxr_swapchain_get_swapchain(swapchain: int) 🔗

Returns the XrSwapchain handle of the provided swapchain.

void openxr_swapchain_release(swapchain: int) 🔗

Releases the image of the provided swapchain.

void register_composition_layer_provider(extension: OpenXRExtensionWrapper) 🔗

Registers the given extension as a composition layer provider.

void register_frame_info_extension(extension: OpenXRExtensionWrapper) 🔗

Registers the given extension as modifying frame info via the OpenXRExtensionWrapper._set_frame_wait_info_and_get_next_pointer(), OpenXRExtensionWrapper._set_view_locate_info_and_get_next_pointer(), or OpenXRExtensionWrapper._set_frame_end_info_and_get_next_pointer() virtual methods.

void register_projection_views_extension(extension: OpenXRExtensionWrapper) 🔗

Registers the given extension as a provider of additional data structures to projections views.

void set_custom_play_space(space: const void*) 🔗

Sets the reference space used by OpenXR to the given XrSpace (cast to a void *).

void set_emulate_environment_blend_mode_alpha_blend(enabled: bool) 🔗

If set to true, an OpenXR extension is loaded which is capable of emulating the XRInterface.XR_ENV_BLEND_MODE_ALPHA_BLEND blend mode.

void set_object_name(object_type: int, object_handle: int, object_name: String) 🔗

Set the object name of an OpenXR object, used for debug output. object_type must be a valid OpenXR XrObjectType enum and object_handle must be a valid OpenXR object handle.

void set_render_region(render_region: Rect2i) 🔗

Sets the render region to render_region, overriding the normal render target's rect.

void set_velocity_depth_texture(render_target: RID) 🔗

Sets the render target of the velocity depth texture.

void set_velocity_target_size(target_size: Vector2i) 🔗

Sets the target size of the velocity and velocity depth textures.

void set_velocity_texture(render_target: RID) 🔗

Sets the render target of the velocity texture.

Transform3D transform_from_pose(pose: const void*) 🔗

Creates a Transform3D from an XrPosef.

void unregister_composition_layer_provider(extension: OpenXRExtensionWrapper) 🔗

Unregisters the given extension as a composition layer provider.

void unregister_frame_info_extension(extension: OpenXRExtensionWrapper) 🔗

Unregisters the given extension as modifying frame info.

void unregister_projection_views_extension(extension: OpenXRExtensionWrapper) 🔗

Unregisters the given extension as a provider of additional data structures to projections views.

bool xr_result(result: int, format: String, args: Array) 🔗

Returns true if the provided XrResult (cast to an integer) is successful. Otherwise returns false and prints the XrResult converted to a string, with the specified additional information.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRBindingModifier

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrbindingmodifier.html

**Contents:**
- OpenXRBindingModifier
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: OpenXRActionBindingModifier, OpenXRIPBindingModifier

Binding modifier base class.

Binding modifier base class. Subclasses implement various modifiers that alter how an OpenXR runtime processes inputs.

_get_description() virtual required const

_get_ip_modification() virtual required

String _get_description() virtual required const 🔗

Return the description of this class that is used for the title bar of the binding modifier editor.

PackedByteArray _get_ip_modification() virtual required 🔗

Returns the data that is sent to OpenXR when submitting the suggested interacting bindings this modifier is a part of.

Note: This must be data compatible with an XrBindingModificationBaseHeaderKHR structure.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRDpadBindingModifier

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrdpadbindingmodifier.html

**Contents:**
- OpenXRDpadBindingModifier
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: OpenXRIPBindingModifier < OpenXRBindingModifier < Resource < RefCounted < Object

The DPad binding modifier converts an axis input to a dpad output.

The DPad binding modifier converts an axis input to a dpad output, emulating a DPad. New input paths for each dpad direction will be added to the interaction profile. When bound to actions the DPad emulation will be activated. You should not combine dpad inputs with normal inputs in the same action set for the same control, this will result in an error being returned when suggested bindings are submitted to OpenXR.

See XR_EXT_dpad_binding for in-depth details.

Note: If the DPad binding modifier extension is enabled, all dpad binding paths will be available in the action map. Adding the modifier to an interaction profile allows you to further customize the behavior.

OpenXRActionSet action_set 🔗

void set_action_set(value: OpenXRActionSet)

OpenXRActionSet get_action_set()

Action set for which this dpad binding modifier is active.

float center_region = 0.1 🔗

void set_center_region(value: float)

float get_center_region()

Center region in which our center position of our dpad return true.

String input_path = "" 🔗

void set_input_path(value: String)

String get_input_path()

Input path for this dpad binding modifier.

bool is_sticky = false 🔗

void set_is_sticky(value: bool)

If false, when the joystick enters a new dpad zone this becomes true.

If true, when the joystick remains in active dpad zone, this remains true even if we overlap with another zone.

OpenXRHapticBase off_haptic 🔗

void set_off_haptic(value: OpenXRHapticBase)

OpenXRHapticBase get_off_haptic()

Haptic pulse to emit when the user releases the input.

OpenXRHapticBase on_haptic 🔗

void set_on_haptic(value: OpenXRHapticBase)

OpenXRHapticBase get_on_haptic()

Haptic pulse to emit when the user presses the input.

float threshold = 0.6 🔗

void set_threshold(value: float)

float get_threshold()

When our input value is equal or larger than this value, our dpad in that direction becomes true. It stays true until it falls under the threshold_released value.

float threshold_released = 0.4 🔗

void set_threshold_released(value: float)

float get_threshold_released()

When our input value falls below this, our output becomes false.

float wedge_angle = 1.5707964 🔗

void set_wedge_angle(value: float)

float get_wedge_angle()

The angle of each wedge that identifies the 4 directions of the emulated dpad.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRExtensionWrapperExtension

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrextensionwrapperextension.html

**Contents:**
- OpenXRExtensionWrapperExtension
- Description
- User-contributed notes

Deprecated: Use OpenXRExtensionWrapper instead.

Inherits: OpenXRExtensionWrapper < Object

Allows implementing OpenXR extensions with GDExtension.

OpenXRExtensionWrapperExtension allows implementing OpenXR extensions with GDExtension. The extension should be registered with OpenXRExtensionWrapper.register_extension_wrapper().

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRExtensionWrapper

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrextensionwrapper.html

**Contents:**
- OpenXRExtensionWrapper
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherited By: OpenXRExtensionWrapperExtension, OpenXRFutureExtension, OpenXRRenderModelExtension

Allows implementing OpenXR extensions with GDExtension.

OpenXRExtensionWrapper allows implementing OpenXR extensions with GDExtension. The extension should be registered with register_extension_wrapper().

_get_composition_layer(index: int) virtual

_get_composition_layer_count() virtual

_get_composition_layer_order(index: int) virtual

_get_requested_extensions() virtual

_get_suggested_tracker_names() virtual

_get_viewport_composition_layer_extension_properties() virtual

_get_viewport_composition_layer_extension_property_defaults() virtual

_on_before_instance_created() virtual

_on_event_polled(event: const void*) virtual

_on_instance_created(instance: int) virtual

_on_instance_destroyed() virtual

_on_main_swapchains_created() virtual

_on_post_draw_viewport(viewport: RID) virtual

_on_pre_draw_viewport(viewport: RID) virtual

_on_pre_render() virtual

_on_process() virtual

_on_register_metadata() virtual

_on_session_created(session: int) virtual

_on_session_destroyed() virtual

_on_state_exiting() virtual

_on_state_focused() virtual

_on_state_idle() virtual

_on_state_loss_pending() virtual

_on_state_ready() virtual

_on_state_stopping() virtual

_on_state_synchronized() virtual

_on_state_visible() virtual

_on_sync_actions() virtual

_on_viewport_composition_layer_destroyed(layer: const void*) virtual

_set_android_surface_swapchain_create_info_and_get_next_pointer(property_values: Dictionary, next_pointer: void*) virtual

_set_frame_end_info_and_get_next_pointer(next_pointer: void*) virtual

_set_frame_wait_info_and_get_next_pointer(next_pointer: void*) virtual

_set_hand_joint_locations_and_get_next_pointer(hand_index: int, next_pointer: void*) virtual

_set_instance_create_info_and_get_next_pointer(next_pointer: void*) virtual

_set_projection_views_and_get_next_pointer(view_index: int, next_pointer: void*) virtual

_set_reference_space_create_info_and_get_next_pointer(reference_space_type: int, next_pointer: void*) virtual

_set_session_create_and_get_next_pointer(next_pointer: void*) virtual

_set_swapchain_create_info_and_get_next_pointer(next_pointer: void*) virtual

_set_system_properties_and_get_next_pointer(next_pointer: void*) virtual

_set_view_locate_info_and_get_next_pointer(next_pointer: void*) virtual

_set_viewport_composition_layer_and_get_next_pointer(layer: const void*, property_values: Dictionary, next_pointer: void*) virtual

register_extension_wrapper()

int _get_composition_layer(index: int) virtual 🔗

Returns a pointer to an XrCompositionLayerBaseHeader struct to provide the given composition layer.

This will only be called if the extension previously registered itself with OpenXRAPIExtension.register_composition_layer_provider().

int _get_composition_layer_count() virtual 🔗

Returns the number of composition layers this extension wrapper provides via _get_composition_layer().

This will only be called if the extension previously registered itself with OpenXRAPIExtension.register_composition_layer_provider().

int _get_composition_layer_order(index: int) virtual 🔗

Returns an integer that will be used to sort the given composition layer provided via _get_composition_layer(). Lower numbers will move the layer to the front of the list, and higher numbers to the end. The default projection layer has an order of 0, so layers provided by this method should probably be above or below (but not exactly) 0.

This will only be called if the extension previously registered itself with OpenXRAPIExtension.register_composition_layer_provider().

Dictionary _get_requested_extensions() virtual 🔗

Returns a Dictionary of OpenXR extensions related to this extension. The Dictionary should contain the name of the extension, mapped to a bool * cast to an integer:

If the bool * is a nullptr this extension is mandatory.

If the bool * points to a boolean, the boolean will be updated to true if the extension is enabled.

PackedStringArray _get_suggested_tracker_names() virtual 🔗

Returns a PackedStringArray of positional tracker names that are used within the extension wrapper.

Array[Dictionary] _get_viewport_composition_layer_extension_properties() virtual 🔗

Gets an array of Dictionarys that represent properties, just like Object._get_property_list(), that will be added to OpenXRCompositionLayer nodes.

Dictionary _get_viewport_composition_layer_extension_property_defaults() virtual 🔗

Gets a Dictionary containing the default values for the properties returned by _get_viewport_composition_layer_extension_properties().

void _on_before_instance_created() virtual 🔗

Called before the OpenXR instance is created.

bool _on_event_polled(event: const void*) virtual 🔗

Called when there is an OpenXR event to process. When implementing, return true if the event was handled, return false otherwise.

void _on_instance_created(instance: int) virtual 🔗

Called right after the OpenXR instance is created.

void _on_instance_destroyed() virtual 🔗

Called right before the OpenXR instance is destroyed.

void _on_main_swapchains_created() virtual 🔗

Called right after the main swapchains are (re)created.

void _on_post_draw_viewport(viewport: RID) virtual 🔗

Called right after the given viewport is rendered.

Note: The draw commands might only be queued at this point, not executed.

void _on_pre_draw_viewport(viewport: RID) virtual 🔗

Called right before the given viewport is rendered.

void _on_pre_render() virtual 🔗

Called right before the XR viewports begin their rendering step.

void _on_process() virtual 🔗

Called as part of the OpenXR process handling. This happens right before general and physics processing steps of the main loop. During this step controller data is queried and made available to game logic.

void _on_register_metadata() virtual 🔗

Allows extensions to register additional controller metadata. This function is called even when the OpenXR API is not constructed as the metadata needs to be available to the editor.

Extensions should also provide metadata regardless of whether they are supported on the host system. The controller data is used to setup action maps for users who may have access to the relevant hardware.

void _on_session_created(session: int) virtual 🔗

Called right after the OpenXR session is created.

void _on_session_destroyed() virtual 🔗

Called right before the OpenXR session is destroyed.

void _on_state_exiting() virtual 🔗

Called when the OpenXR session state is changed to exiting.

void _on_state_focused() virtual 🔗

Called when the OpenXR session state is changed to focused. This state is the active state when the game runs.

void _on_state_idle() virtual 🔗

Called when the OpenXR session state is changed to idle.

void _on_state_loss_pending() virtual 🔗

Called when the OpenXR session state is changed to loss pending.

void _on_state_ready() virtual 🔗

Called when the OpenXR session state is changed to ready. This means OpenXR is ready to set up the session.

void _on_state_stopping() virtual 🔗

Called when the OpenXR session state is changed to stopping.

void _on_state_synchronized() virtual 🔗

Called when the OpenXR session state is changed to synchronized. OpenXR also returns to this state when the application loses focus.

void _on_state_visible() virtual 🔗

Called when the OpenXR session state is changed to visible. This means OpenXR is now ready to receive frames.

void _on_sync_actions() virtual 🔗

Called when OpenXR has performed its action sync.

void _on_viewport_composition_layer_destroyed(layer: const void*) virtual 🔗

Called when a composition layer created via OpenXRCompositionLayer is destroyed.

layer is a pointer to an XrCompositionLayerBaseHeader struct.

int _set_android_surface_swapchain_create_info_and_get_next_pointer(property_values: Dictionary, next_pointer: void*) virtual 🔗

Adds additional data structures to Android surface swapchains created by OpenXRCompositionLayer.

property_values contains the values of the properties returned by _get_viewport_composition_layer_extension_properties().

int _set_frame_end_info_and_get_next_pointer(next_pointer: void*) virtual 🔗

Adds additional data structures to XrFrameEndInfo.

This will only be called if the extension previously registered itself with OpenXRAPIExtension.register_frame_info_extension().

int _set_frame_wait_info_and_get_next_pointer(next_pointer: void*) virtual 🔗

Adds additional data structures to XrFrameWaitInfo.

This will only be called if the extension previously registered itself with OpenXRAPIExtension.register_frame_info_extension().

int _set_hand_joint_locations_and_get_next_pointer(hand_index: int, next_pointer: void*) virtual 🔗

Adds additional data structures when each hand tracker is created.

int _set_instance_create_info_and_get_next_pointer(next_pointer: void*) virtual 🔗

Adds additional data structures when the OpenXR instance is created.

int _set_projection_views_and_get_next_pointer(view_index: int, next_pointer: void*) virtual 🔗

Adds additional data structures to the projection view of the given view_index.

int _set_reference_space_create_info_and_get_next_pointer(reference_space_type: int, next_pointer: void*) virtual 🔗

Adds additional data structures to XrReferenceSpaceCreateInfo.

int _set_session_create_and_get_next_pointer(next_pointer: void*) virtual 🔗

Adds additional data structures when the OpenXR session is created.

int _set_swapchain_create_info_and_get_next_pointer(next_pointer: void*) virtual 🔗

Adds additional data structures when creating OpenXR swapchains.

int _set_system_properties_and_get_next_pointer(next_pointer: void*) virtual 🔗

Adds additional data structures when querying OpenXR system abilities.

int _set_view_locate_info_and_get_next_pointer(next_pointer: void*) virtual 🔗

Adds additional data structures to XrViewLocateInfo.

This will only be called if the extension previously registered itself with OpenXRAPIExtension.register_frame_info_extension().

int _set_viewport_composition_layer_and_get_next_pointer(layer: const void*, property_values: Dictionary, next_pointer: void*) virtual 🔗

Adds additional data structures to composition layers created by OpenXRCompositionLayer.

property_values contains the values of the properties returned by _get_viewport_composition_layer_extension_properties().

layer is a pointer to an XrCompositionLayerBaseHeader struct.

OpenXRAPIExtension get_openxr_api() 🔗

Returns the created OpenXRAPIExtension, which can be used to access the OpenXR API.

void register_extension_wrapper() 🔗

Registers the extension. This should happen at core module initialization level.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRFutureExtension

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrfutureextension.html

**Contents:**
- OpenXRFutureExtension
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: OpenXRExtensionWrapper < Object

The OpenXR Future extension allows for asynchronous APIs to be used.

This is a support extension in OpenXR that allows other OpenXR extensions to start asynchronous functions and get a callback after this function finishes. It is not intended for consumption within GDScript but can be accessed from GDExtension.

cancel_future(future: int)

register_future(future: int, on_success: Callable = Callable())

void cancel_future(future: int) 🔗

Cancels an in-progress future. future must be an XrFutureEXT value previously returned by an API that started an asynchronous function.

bool is_active() const 🔗

Returns true if futures are available in the OpenXR runtime used. This function will only return a usable result after OpenXR has been initialized.

OpenXRFutureResult register_future(future: int, on_success: Callable = Callable()) 🔗

Register an OpenXR Future object so we monitor for completion. future must be an XrFutureEXT value previously returned by an API that started an asynchronous function.

You can optionally specify on_success, it will be invoked on successful completion of the future.

Or you can use the returned OpenXRFutureResult object to await its OpenXRFutureResult.completed signal.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
var future_result = OpenXRFutureExtension.register_future(future)
await future_result.completed
if future_result.get_status() == OpenXRFutureResult.RESULT_FINISHED:
    # Handle your success
    pass
```

---

## OpenXRFutureResult

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrfutureresult.html

**Contents:**
- OpenXRFutureResult
- Description
- Methods
- Signals
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Result object tracking the asynchronous result of an OpenXR Future object.

Result object tracking the asynchronous result of an OpenXR Future object, you can use this object to track the result status.

get_result_value() const

set_result_value(result_value: Variant)

completed(result: OpenXRFutureResult) 🔗

Emitted when the asynchronous function is finished or has been cancelled.

ResultStatus RESULT_RUNNING = 0

The asynchronous function is running.

ResultStatus RESULT_FINISHED = 1

The asynchronous function has finished.

ResultStatus RESULT_CANCELLED = 2

The asynchronous function has been cancelled.

void cancel_future() 🔗

Cancel this future, this will interrupt and stop the asynchronous function.

int get_future() const 🔗

Return the XrFutureEXT value this result relates to.

Variant get_result_value() const 🔗

Returns the result value of our asynchronous function (if set by the extension). The type of this result value depends on the function being called. Consult the documentation of the relevant function.

ResultStatus get_status() const 🔗

Returns the status of this result.

void set_result_value(result_value: Variant) 🔗

Stores the result value we expose to the user.

Note: This method should only be called by an OpenXR extension that implements an asynchronous function.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRHapticBase

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrhapticbase.html

**Contents:**
- OpenXRHapticBase
- Description
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: OpenXRHapticVibration

OpenXR Haptic feedback base class.

This is a base class for haptic feedback resources.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRHapticVibration

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrhapticvibration.html

**Contents:**
- OpenXRHapticVibration
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: OpenXRHapticBase < Resource < RefCounted < Object

Vibration haptic feedback.

This haptic feedback resource makes it possible to define a vibration based haptic feedback pulse that can be triggered through actions in the OpenXR action map.

float amplitude = 1.0 🔗

void set_amplitude(value: float)

float get_amplitude()

The amplitude of the pulse between 0.0 and 1.0.

void set_duration(value: int)

The duration of the pulse in nanoseconds. Use -1 for a minimum duration pulse for the current XR runtime.

float frequency = 0.0 🔗

void set_frequency(value: float)

float get_frequency()

The frequency of the pulse in Hz. 0.0 will let the XR runtime chose an optimal frequency for the device used.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRIPBindingModifier

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxripbindingmodifier.html

**Contents:**
- OpenXRIPBindingModifier
- Description
- User-contributed notes

Inherits: OpenXRBindingModifier < Resource < RefCounted < Object

Inherited By: OpenXRDpadBindingModifier

Binding modifier that applies directly on an interaction profile.

Binding modifier that applies directly on an interaction profile.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRRenderModelExtension

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrrendermodelextension.html

**Contents:**
- OpenXRRenderModelExtension
- Description
- Methods
- Signals
- Method Descriptions
- User-contributed notes

Inherits: OpenXRExtensionWrapper < Object

This class implements the OpenXR Render Model Extension.

This class implements the OpenXR Render Model Extension, if enabled it will maintain a list of active render models and provides an interface to the render model data.

render_model_create(render_model_id: int)

render_model_destroy(render_model: RID)

render_model_get_all()

render_model_get_animatable_node_count(render_model: RID) const

render_model_get_animatable_node_name(render_model: RID, index: int) const

render_model_get_animatable_node_transform(render_model: RID, index: int) const

render_model_get_confidence(render_model: RID) const

render_model_get_root_transform(render_model: RID) const

render_model_get_subaction_paths(render_model: RID)

render_model_get_top_level_path(render_model: RID) const

render_model_is_animatable_node_visible(render_model: RID, index: int) const

render_model_new_scene_instance(render_model: RID) const

render_model_added(render_model: RID) 🔗

Emitted when a new render model is added.

render_model_removed(render_model: RID) 🔗

Emitted when a render model is removed.

render_model_top_level_path_changed(render_model: RID) 🔗

Emitted when the top level path associated with a render model changed.

bool is_active() const 🔗

Returns true if OpenXR's render model extension is supported and enabled.

Note: This only returns a valid value after OpenXR has been initialized.

RID render_model_create(render_model_id: int) 🔗

Creates a render model object within OpenXR using a render model id.

Note: This function is exposed for dependent OpenXR extensions that provide render model ids to be used with the render model extension.

void render_model_destroy(render_model: RID) 🔗

Destroys a render model object within OpenXR that was previously created with render_model_create().

Note: This function is exposed for dependent OpenXR extensions that provide render model ids to be used with the render model extension.

Array[RID] render_model_get_all() 🔗

Returns an array of all currently active render models registered with this extension.

int render_model_get_animatable_node_count(render_model: RID) const 🔗

Returns the number of animatable nodes this render model has.

String render_model_get_animatable_node_name(render_model: RID, index: int) const 🔗

Returns the name of the given animatable node.

Transform3D render_model_get_animatable_node_transform(render_model: RID, index: int) const 🔗

Returns the current local transform for an animatable node. This is updated every frame.

TrackingConfidence render_model_get_confidence(render_model: RID) const 🔗

Returns the tracking confidence of the tracking data for the render model.

Transform3D render_model_get_root_transform(render_model: RID) const 🔗

Returns the root transform of a render model. This is the tracked position relative to our XROrigin3D node.

PackedStringArray render_model_get_subaction_paths(render_model: RID) 🔗

Returns a list of active subaction paths for this render_model.

Note: If different devices are bound to your actions than available in suggested interaction bindings, this information shows paths related to the interaction bindings being mimicked by that device.

String render_model_get_top_level_path(render_model: RID) const 🔗

Returns the top level path associated with this render_model. If provided this identifies whether the render model is associated with the player's hands or other body part.

bool render_model_is_animatable_node_visible(render_model: RID, index: int) const 🔗

Returns true if this animatable node should be visible.

Node3D render_model_new_scene_instance(render_model: RID) const 🔗

Returns an instance of a subscene that contains all MeshInstance3D nodes that allow you to visualize the render model.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRRenderModelManager

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrrendermodelmanager.html

**Contents:**
- OpenXRRenderModelManager
- Description
- Properties
- Signals
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: Node3D < Node < Object

Helper node that will automatically manage displaying render models.

This helper node will automatically manage displaying render models. It will create new OpenXRRenderModel nodes as controllers and other hand held devices are detected, and remove those nodes when they are deactivated.

Note: If you want more control over this logic you can alternatively call OpenXRRenderModelExtension.render_model_get_all() to obtain a list of active render model ids and create OpenXRRenderModel instances for each render model id provided.

render_model_added(render_model: OpenXRRenderModel) 🔗

Emitted when a render model node is added as a child to this node.

render_model_removed(render_model: OpenXRRenderModel) 🔗

Emitted when a render model child node is about to be removed from this node.

enum RenderModelTracker: 🔗

RenderModelTracker RENDER_MODEL_TRACKER_ANY = 0

All active render models are shown regardless of what tracker they relate to.

RenderModelTracker RENDER_MODEL_TRACKER_NONE_SET = 1

Only active render models are shown that are not related to any tracker we manage.

RenderModelTracker RENDER_MODEL_TRACKER_LEFT_HAND = 2

Only active render models are shown that are related to the left hand tracker.

RenderModelTracker RENDER_MODEL_TRACKER_RIGHT_HAND = 3

Only active render models are shown that are related to the right hand tracker.

String make_local_to_pose = "" 🔗

void set_make_local_to_pose(value: String)

String get_make_local_to_pose()

Position render models local to this pose (this will adjust the position of the render models container node).

RenderModelTracker tracker = 0 🔗

void set_tracker(value: RenderModelTracker)

RenderModelTracker get_tracker()

Limits render models to the specified tracker. Include: 0 = All render models, 1 = Render models not related to a tracker, 2 = Render models related to the left hand tracker, 3 = Render models related to the right hand tracker.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXRVisibilityMask

**URL:** https://docs.godotengine.org/en/stable/classes/class_openxrvisibilitymask.html

**Contents:**
- OpenXRVisibilityMask
- Description
- User-contributed notes

Inherits: VisualInstance3D < Node3D < Node < Object

Draws a stereo correct visibility mask.

The visibility mask allows us to black out the part of the render result that is invisible due to lens distortion.

As this is rendered first, it prevents fragments with expensive lighting calculations to be processed as they are discarded through z-checking.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXR body tracking

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/openxr_body_tracking.html

**Contents:**
- OpenXR body tracking
- HTC Tracker support
- User-contributed notes

Support for full body tracking in OpenXR is only just becoming available for a select few platforms. As support solidifies information will be added to this page.

An option that has been available for some time is doing full body tracking using HTC trackers. These are currently supported through SteamVR and on HTC Elite XR headsets. They are exposed through the action map system.

These trackers are identified by their roles which are assigned to them when configured. Simply add XRController3D nodes as children to the XROrigin3D node and assign one of the following trackers:

/user/vive_tracker_htcx/role/handheld_object

/user/vive_tracker_htcx/role/left_foot

/user/vive_tracker_htcx/role/right_foot

/user/vive_tracker_htcx/role/left_shoulder

/user/vive_tracker_htcx/role/right_shoulder

/user/vive_tracker_htcx/role/left_elbow

/user/vive_tracker_htcx/role/right_elbow

/user/vive_tracker_htcx/role/left_knee

/user/vive_tracker_htcx/role/right_knee

/user/vive_tracker_htcx/role/waist

/user/vive_tracker_htcx/role/chest

/user/vive_tracker_htcx/role/camera

/user/vive_tracker_htcx/role/keyboard

You can now use these as targets for IK modifiers on a full body avatar.

Please read the User-contributed notes policy before submitting a comment.

---

## OpenXR composition layers

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/openxr_composition_layers.html

**Contents:**
- OpenXR composition layers
- Introduction
- Setting up the SubViewport
- Adding a composition layer
- Making the interface work
- Hole punching
- User-contributed notes

In XR games you generally want to create user interactions that happen in 3D space and involve users touching objects as if they are touching them in real life.

Sometimes however creating a more traditional 2D interface is unavoidable. In XR however you can't just add 2D components to your scene. Godot needs depth information to properly position these elements so they appear at a comfortable place for the user. Even with depth information there are headsets with slanted displays that make it impossible for the standard 2D pipeline to correctly render the 2D elements.

The solution then is to render the UI to a SubViewport and display the result of this using a ViewportTexture on a 3D mesh. The QuadMesh is a suitable option for this.

See the GUI in 3D example project for an example of this approach.

The problem with displaying the viewport in this way is that the rendered result is sampled for lens distortion by the XR runtime and the resulting quality loss can make UI text hard to read.

OpenXR offers a solution to this problem through composition layers. With composition layers it is possible for the contents of a viewport to be projected on a surface after lens distortion resulting in a much higher quality end result.

As not all XR runtimes support all composition layer types, Godot implements a fallback solution where we render the viewport as part of the normal scene but with the aforementioned quality limitations.

When the composition layer is supported, it is the XR runtime that presents the subviewport. This means the UI is only visible in the headset, it will not be accessible by Godot and will thus not be shown when you have a spectator view on the desktop.

There are currently 3 nodes that expose this functionality:

OpenXRCompositionLayerCylinder shows the contents of the SubViewport on the inside of a cylinder (or "slice" of a cylinder).

OpenXRCompositionLayerEquirect shows the contents of the SubViewport on the interior of a sphere (or "slice" of a sphere).

OpenXRCompositionLayerQuad shows the contents of the SubViewport on a flat rectangle.

The first step is adding a SubViewport for our 2D UI, this doesn't require any specific steps. For our example we do mark the viewport as transparent.

You can now create the 2D UI by adding child nodes to the SubViewport as you normally would. It is advisable to save the 2D UI in a subscene, this makes it easier to do your layout.

The update mode "When Visible" will not work as Godot can't determine whether the viewport is visible to the user. When assigning our viewport to a composition layer Godot will automatically adjust this.

The second step is adding our composition layer. We can add the correct composition layer node as a child node of our XROrigin3D node. This is very important as the XR runtime positions everything in relation to our origin.

We want to position the composition layer so it is at eye height and roughly 1 to 1.5 meters away from the player.

We now assign the SubViewport to the Layer Viewport property and enable Alpha Blend.

As the player can walk away from the origin point, you will want to reposition the composition layer when the player recenters the view. Using the reference space Local Floor will apply this logic automatically.

So far we're only displaying our UI, to make it work we need to add some code. For this example we're going to keep things simple and make one of the controllers work as a pointer. We'll then simulate mouse actions with this pointer.

This code also requires a MeshInstance3D node called Pointer to be added as a child to our OpenXRCompositionLayerQuad node. We configure a SphereMesh with a radius 0.01 meters. We'll be using this as a helper to visualize where the user is pointing.

The main function that drives this functionality is the intersects_ray function on our composition layer node. This function takes the global position and orientation of our pointer and returns the UV where our ray intersects our viewport. It returns Vector2(-1.0, -1.0) if we're not pointing at our viewport.

We start with setting up some variables, important here are the export variables which identify our controller node with which we point to our screen.

Next we define a helper function that takes the value returned from intersects_ray and gives us the global position for that intersection point. This implementation only works for our OpenXRCompositionLayerQuad node.

We also define a helper function that takes our intersect value and returns our location in the viewport's local coordinate system:

The main logic happens in our _process function. Here we start by hiding our pointer, we then check if we have a valid controller and viewport, and we call intersects_ray with the position and orientation of our controller:

Next we check if we're intersecting with our viewport. If so, we check if our button is pressed and place our pointer at our intersection point.

If we were intersecting in our previous process call and our pointer has moved, we prepare an InputEventMouseMotion object to simulate our mouse moving and send that to our viewport for further processing.

If we've just released our button we also prepare an InputEventMouseButton object to simulate a button release and send that to our viewport for further processing.

Or if we've just pressed our button we prepare an InputEventMouseButton object to simulate a button press and send that to our viewport for further processing.

Next we remember our state for next frame.

Finally, if we aren't intersecting, we clear our state.

As the composition layer is composited on top of the render result, it can be rendered in front of objects that are actually forward of the viewport.

By enabling hole punch you instruct Godot to render a transparent object where our viewport is displayed. It does this in a way that fills the depth buffer and clears the current rendering result. Anything behind our viewport will now be cleared, while anything in front of our viewport will be rendered as usual.

You also need to set Sort Order to a negative value, the XR compositor will now draw the viewport first, and then overlay our rendering result.

Use case showing how the user's hand is incorrectly obscured by a composition layer when hole punching is not used.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
extends OpenXRCompositionLayerQuad

const NO_INTERSECTION = Vector2(-1.0, -1.0)

@export var controller : XRController3D
@export var button_action : String = "trigger_click"

var was_pressed : bool = false
var was_intersect : Vector2 = NO_INTERSECTION

...
```

Example 2 (swift):
```swift
...

func _intersect_to_global_pos(intersect : Vector2) -> Vector3:
    if intersect != NO_INTERSECTION:
        var local_pos : Vector2 = (intersect - Vector2(0.5, 0.5)) * quad_size
        return global_transform * Vector3(local_pos.x, -local_pos.y, 0.0)
    else:
        return Vector3()

...
```

Example 3 (swift):
```swift
...

func _intersect_to_viewport_pos(intersect : Vector2) -> Vector2i:
    if layer_viewport and intersect != NO_INTERSECTION:
        var pos : Vector2 = intersect * Vector2(layer_viewport.size)
        return Vector2i(pos)
    else:
        return Vector2i(-1, -1)

...
```

Example 4 (gdscript):
```gdscript
...

# Called every frame. 'delta' is the elapsed time since the previous frame.
func _process(_delta):
    # Hide our pointer, we'll make it visible if we're interacting with the viewport.
    $Pointer.visible = false

    if controller and layer_viewport:
        var controller_t : Transform3D = controller.global_transform
        var intersect : Vector2 = intersects_ray(controller_t.origin, -controller_t.basis.z)

...
```

---

## OpenXR hand tracking

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/openxr_hand_tracking.html

**Contents:**
- OpenXR hand tracking
- Introduction
- Demo project
- The Hand Tracking API
  - Hand tracking node
  - Rigged hand mesh
  - The hand skeleton modifier
- The hand tracking data source
- Handling user input
  - The hand interaction profile

This page focuses specifically on the feature set exposed through OpenXR. Parts of the functionality presented here also applies to WebXR and can by provided by other XR interfaces.

When discussing hand tracking it is important to know that there are differences of opinion as to where lines are drawn. The practical result of this is that there are differences in implementation between the different OpenXR runtimes. You may find yourself in a place where chosen hardware doesn't support a piece of the puzzle or does things differently enough from the other platforms that you need to do extra work.

That said, recent improvements to the OpenXR specification are closing these gaps and as platforms implement these improvements we are getting closer to a future where we have either full portability between platforms or at least a clear way to detect the capabilities of a platform.

When we look at the early days of VR the focus of the major platforms was on tracked controller based input. Here we are tracking a physical device that also has buttons for further input. From the tracking data we can infer the location of the player's hands but no further information is known, traditionally it was left up to the game to implement a mechanism to display the player's hand and animate the fingers based on further input from the controller, be it due to buttons being pressed or through proximity sensors. Often fingers are also placed based on context, what the user is holding, and what action a user is performing.

More recently optical hand tracking has become a popular solution, where cameras track the user's hands and full tracking data for the hand and finger positions becomes available. Many vendors saw this as completely separate from controller tracking and introduced independent APIs to access hand and finger positions and orientation data. When handling input, it was up to the game developer to implement a gesture detection mechanism.

This split also exists in OpenXR, where controller tracking is handled primarily by the action map system, while optical hand tracking is primarily handled by the hand tracking API extension.

However, the world is not that black and white and we're seeing a number of scenarios where we cross the line:

Devices that fit in both categories, such as tracked gloves and controllers such as the Index controller that also perform finger tracking.

XR Runtimes that implement inferred hand tracking from controller data as a means to solve proper finger placement for multiple controllers.

XR applications that wish to seamlessly switch between controller and hand tracking offering the same user experience regardless of approach used.

OpenXR is answering this call by introducing further extensions that lets us query the capabilities of the XR runtime/hardware or that add further functionality across this divide. The problem that currently does remain is that there are gaps in adopting these extensions, with some platforms thus not reporting capabilities to their full extent. As such you may need to test for the features available on specific hardware and adjust your approach accordingly.

The information presented on this page was used to create a demo project that can be found here.

As mentioned in our introduction, the hand tracking API is primarily used with optical hand tracking and on many platforms only works when the user is not holding a controller. Some platforms support controller inferred hand tracking meaning that you will get hand tracking data even if the user is holding a controller. This includes SteamVR, Meta Quest (currently native only but Meta link support is likely coming), and hopefully soon others as well.

The hand tracking implementation in Godot has been standardized around the Godot Humanoid Skeleton and works both in OpenXR and WebXR. The instructions below will thus work in both environments.

In order to use the hand tracking API with OpenXR you first need to enable it. This can be done in the project settings:

For some standalone XR devices you also need to configure the hand tracking extension in export settings, for instance for Meta Quest:

Now you need to add 3 components into your scene for each hand:

A tracked node to position the hand.

A properly skinned hand mesh with skeleton.

A skeleton modifier that applies finger tracking data to the skeleton.

The hand tracking system uses separate hand trackers to track the position of the player's hands within our tracking space.

This information has been separated out for the following use cases:

Tracking happens in the local space of the XROrigin3D node. This node must be a child of the XROrigin3D node in order to be correctly placed.

This node can be used as an IK target when an upper body mesh with arms is used instead of separate hand meshes.

Actual placement of the hands may be loosely bound to the tracking in scenarios such as avatar creation UIs, fake mirrors, or similar situations resulting in the hand mesh and finger tracking being localized elsewhere.

We'll concentrate on the first use case only.

For this you need to add an XRNode3D node to your XROrigin3D node.

On this node the tracker should be set to /user/hand_tracker/left or /user/hand_tracker/right for the left or right hand respectively.

The pose should remain set to default, no other option will work here.

The checkbox Show When Tracked will automatically hide this node if no tracking data is available, or make this node visible if tracking data is available.

In order to display our hand we need a hand mesh that is properly rigged and skinned. For this Godot uses the hand bone structure as defined for the Godot Humanoid but optionally supporting an extra tip bone for each finger.

The OpenXR hand tracking demo contains example glTF files of properly rigged hands.

We will be using those here and add them as a child to our XRNode3D node. We also need to enable editable children to gain access to our Skeleton3D node.

Finally we need to add an XRHandModifier3D node as a child to our Skeleton3D node. This node will obtain the finger tracking data from OpenXR and apply it the hand model.

You need to set the Hand Tracker property to either /user/hand_tracker/left or /user/hand_tracker/right depending on whether we are apply the tracking data of respectively the left or right hand.

You can also set the Bone Update mode on this node.

Full applies the hand tracking data fully. This does mean that the skeleton positioning will potentially reflect the size of the actual hand of the user. This can lead to scrunching effect if meshes aren't weighted properly to account for this. Make sure you test your game with players of all sizes when optical hand tracking is used!

Rotation Only will only apply rotation to the bones of the hands and keep the bone length as is. In this mode the size of the hand mesh doesn't change.

With this added, when we run the project we should see the hand correctly displayed if hand tracking is supported.

This is an OpenXR extension that provides information about the source of the hand tracking data. At this moment only a few runtimes implement it but if it is available, Godot will activate it.

If this extension is not supported and thus unknown is returned, you can make the following assumptions:

If you are using SteamVR (including Steam link), only controller based hand tracking is supported.

For any other runtime, if hand tracking is supported, only optical hand tracking is supported (Note, Meta Link currently fall into this category).

In all other cases, no hand tracking is supported at all.

You can access this information through code:

This example logs the state for the left hand.

If in this example no hand tracker is returned by get_tracker, this means the hand tracking API is not supported on the XR runtime at all.

If there is a tracker but has_tracking_data is false, the user's hand is currently not being tracked. This is likely caused by one of the following reasons:

The player's hand is not visible by any of the tracking cameras on the headset

The player is currently using a controller and the headset only supports optical hand tracking

The controller is turned off and only controller hand tracking is supported.

Reacting to actions performed by the user is handled through The XR action map if controllers are used. In the action map you can map various inputs like the trigger or joystick on the controller to an action. This can then drive logic in your game.

When hand tracking is used we originally had no such inputs, inputs are driven by gestures made by the user such as making a fist to grab or pinching the thumb and index finger together to select something. It was up to the game developer to implement this.

Recognizing that there is an increasing demand for applications that can switch seamlessly between controller and hand tracking and the need some form of basic input capability, a number of extensions were added to the specification that provide some basic gesture recognition and can be used with the action map.

The hand interaction profile extension is a new core extension which supports pinch, grasp, and poke gestures and related poses. There is still limited support for this extension but it should become available in more runtimes in the near future.

The pinch gesture is triggered by pinching your thumb and index finger together. This is often used as a select gesture for menu systems, similar to using your controller to point at an object and press the trigger to select and is thus often mapped as such.

The pinch pose is a pose positioned in the middle between the tip of the thumb and the tip of the index finger and oriented such that a ray cast can be used to identify a target.

The pinch float input is a value between 0.0 (the tip of the thumb and index finger are apart) and 1.0 (the tip of the thumb and index finger are touching).

The pinch ready input is true when the tips of the fingers are (close to) touching.

The grasp gesture is triggered by making a fist and is often used to pick items up, similar to engaging the squeeze input on controllers.

The grasp float input is a value between 0.0 (open hand) and 1.0 (fist).

The grasp ready input is true when the user made a fist.

The poke gesture is triggered by extending your index finger, this one is a bit of an exception as the pose at the tip of your index finger is often used to poke an interactable object. The poke pose is a pose positioned on the tip of the index finger.

Finally the aim activate (ready) input is defined as an input that is 1.0/true when the index finger is extended and pointing at a target that can be activated. How runtimes interpret this, is not clear.

With this setup the normal left_hand and right_hand trackers are used and you can thus seamlessly switch between controller and hand tracking input.

You need to enable the hand interaction profile extension in the OpenXR project settings.

The Microsoft hand interaction profile extension was introduced by Microsoft and loosely mimics the simple controller profile. Meta has also added support for this extension but only on their native OpenXR client, it is currently not available over Meta Link.

Pinch support is exposed through the select input, the value of which is 0.0 when the tip of the thumb and index finger are apart and 1.0 when they are together.

Note that in this profile the aim pose is redefined as a pose between thumb and index finger, oriented so a ray cast can be used to identify a target.

Grasp support is exposed through the squeeze input, the value of which is 0.0 when the hand is open, and 1.0 when a fist is made.

With this setup the normal left_hand and right_hand trackers are used and you can thus seamlessly switch between controller and hand tracking input.

The HTC hand interaction profile extension was introduced by HTC and is defined similarly to the Microsoft extension. It is only supported by HTC for the Focus 3 and Elite XR headsets.

See the Microsoft hand interaction profile for the gesture support.

The defining difference is that this extension introduces two new trackers, /user/hand_htc/left and /user/hand_htc/right. This means that extra logic needs to be implemented to switch between the default trackers and the HTC specific trackers when the user puts down, or picks up, their controller.

The simple controller profile is a standard core profile defined as a fallback profile when a controller is used for which no profile exists.

There are a number of OpenXR runtimes that will mimic controllers through the simple controller profile when hand tracking is used.

Unfortunately there is no sound way to determine whether an unknown controller is used or whether hand tracking is emulating a controller through this profile.

XR runtimes are free to define how the simple controller profile operates, so there is also no certainty to how this profile is mapped to gestures.

The most common mapping seems to be that select click is true when the tip of the thumb and index fingers are touching while the user's palm is facing away from the user. menu click will be true when tip of the thumb and index fingers are touching while the user's palm is facing towards the user.

With this setup the normal left_hand and right_hand trackers are used and you can thus seamlessly switch between controller and hand tracking input.

As some of these interaction profiles have overlap it is important to know that you can add each profile to your action map and the XR runtime will choose the best fitting profile.

For instance, a Meta Quest supports both the Microsoft hand interaction profile and simple controller profile. If both are specified the Microsoft hand interaction profile will take precedence and will be used.

The expectation is that once Meta supports the core hand interaction profile extension, that profile will take precedence over both Microsoft and simple controller profiles.

If the platform doesn't support any interaction profiles when hand tracking is used, or if you're building an application where you need more complicated gesture support you're going to need to build your own gesture recognition system.

You can obtain the full hand tracking data through the XRHandTracker resource for each hand. You can obtain the hand tracker by calling XRServer.get_tracker and using either /user/hand_tracker/left or /user/hand_tracker/left as the tracker. This resource provides access to all the joint information for the given hand.

Detailing out a full gesture recognition algorithm goes beyond the scope of this manual however there are a number of community projects you can look at:

Julian Todd's Auto hands library

Malcolm Nixons Hand Pose Detector

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (yaml):
```yaml
var hand_tracker : XRHandTracker = XRServer.get_tracker('/user/hand_tracker/left')
if hand_tracker:
    if hand_tracker.has_tracking_data:
        if hand_tracker.hand_tracking_source == XRHandTracker.HAND_TRACKING_SOURCE_UNKNOWN:
            print("Hand tracking source unknown")
        elif hand_tracker.hand_tracking_source == XRHandTracker.HAND_TRACKING_SOURCE_UNOBSTRUCTED:
            print("Hand tracking source is optical hand tracking")
        elif hand_tracker.hand_tracking_source == XRHandTracker.HAND_TRACKING_SOURCE_CONTROLLER:
            print("Hand tracking data is inferred from controller data")
        else:
            print("Unknown hand tracking source ", hand_tracker.hand_tracking_source)
    else:
        print("Hand is currently not being tracked")
else:
    print("No hand tracker registered")
```

---

## OpenXR Render Models

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/openxr_render_models.html

**Contents:**
- OpenXR Render Models
- OpenXR Render models node
  - Render model manager example
- Render model node
- Backend access
- User-contributed notes

A cornerstone of OpenXR's API design is being as platform agnostic as possible. A great example of this is OpenXR's action map system where XR runtimes have to support core interaction profiles to fall back on, if no interaction profile exists for the hardware being used. This ensures that OpenXR applications keep functioning even when used on hardware that didn't exist when the application was released, or that the developers of the application did not have access too.

A consequence of this is that the application developer doesn't know with any certainty what hardware is being used, as the XR runtime could be mimicking other hardware. The application developer thus can't show anything in relation to the actual hardware used, the most common use case being showing the controllers the user is currently holding.

Showing the correct controller models and having these models correctly positioned is important to a proper sense of immersion.

This is where OpenXR's render models API comes in. This API allows us to query the XR runtime for 3D assets that are correct for the physical hardware being used. The API also allows us to query the position of this hardware within the tracking volume and the correct positioning of subcomponents of this hardware.

For instance, we can correctly position and animate the trigger or show buttons being pressed.

For those runtimes that support the controller data source for hand tracking , we can also correctly position the user's fingers and hand according to the shape of the controller. Do note that this works in combination with the hand joints motion range extension to prevent clipping of the fingers.

The OpenXRRenderModelManager node can be used to automate most of the render models functionality. This node keeps track of the active render models currently made available by the XR runtime.

It will create child nodes for each active render model resulting in that render model being displayed.

This node must have an XROrigin3D node as an ancestor.

If tracker is set to Any our node will show all render models currently being tracked. In this scenario this node must be a direct child of our XROrigin3D node.

If tracker is set to None set our node will only show render models for which no tracker has been identified. In this scenario this node must also be a direct child of our XROrigin3D node.

If tracker is set to Left Hand or Right Hand our node will only show render models related to our left or right hand respectively. In this scenario, our node can be placed deeper in the scene tree.

For most XR runtimes this means the render model represents a controller that is actually being held by the user but this is not a guarantee. Some XR runtimes will always set the tracker to either the left or right hand even if the controller is not currently held but is being tracked. You should always test this as this will lead to unwanted behavior.

In this scenario we can also specify an action for a pose in the action map by setting the make_local_to_pose property to the pose action. Use this in combination with an XRController3D node that is using the same pose and you can now add a layer that allows you to deviate from the tracked position of both your controller and the related render model (see example below).

Combining the above with hand tracking does introduce the problem that hand tracking is completely independent from the action map system. You will need to combine the hand tracking and controller tracking poses to properly offset the render models.

This falls beyond the scope of this documentation.

You can download our render models demo which implements the setup described below.

In this setup we find an OpenXRRenderModelManager node directly underneath our XROrigin3D node. On this node our target property is set to None set and will handle showing all render models that are currently not related to our left or right hand controllers.

We then see the same setup for our left and right hand so we'll focus on just the left hand.

We have an XRController3D that will track the location of our hand.

We are using the grip pose in this example. The palm pose is arguably more suitable and predictable however it is not supported by all XR runtimes. See the hand tracking demo project for a solution to switching between these poses based on what is supported.

As a child of the node we have an AnimatableBody3D node that follows the tracked location of the hand but will interact with physics objects to stop the player's hand from going through walls etc. This node has a collision shape that encapsulates the hand.

It is important to set the physics priority so that this logic runs after any physics logic that moves the XROrigin3D node or the hand will lag a frame behind.

The script below shows a basic implementation for this that you can build upon.

Finally we see another OpenXRRenderModelManager node, this one with target set to the appropriate hand and make_local_to_pose set to the correct pose. This will ensure that the render models related to this hand are properly shown and offset if our collision handler has altered the location.

The OpenXRRenderModel node implements all the logic to display and position a given render model provided by the render models API.

Instances of this node are added by the render model manager node we used up above but you can interact with these directly if you wish.

Whenever Godot obtains information about a new render model an RID is created to reference that render model.

By assigning that RID to the render_model property on this node, the node will start displaying the render model and manage both the transform that places the render model in the correct place and animates all the sub objects.

The get_top_level_path function will return the top level path associated with this render model. This will point to either the left or right hand. As the top level path can be set or cleared depending on whether the user picks up, or puts down, the controller you can connect to the render_model_top_level_path_changes signal and react to these changes.

Depending on your setup of the OpenXRRenderModelManager nodes, render models will be removed or added as their top level path changes.

The nodes we've detailed out above handle all the display logic for us but it is possible to interact with the data that drives this directly and create your own implementation.

For this you can access the OpenXRRenderModelExtension singleton.

This object also lets you query whether render models are supported and enabled on the device currently being used by calling the is_active function on this object.

The built-in logic implements the interaction render model API that lists all render models related to controllers and similar devices that are present in the action map. It will automatically create and remove render model entities that are exposed through this API.

As other extensions become available these can be implemented in a GDExtension plugin. Such a plugin can call render_model_create and render_model_destroy to create the object that will provide access to that render model through the core render models API.

You should not destroy a render model outside of this logic.

You can connect to the render_model_added and render_model_removed signals to be informed when new render models are added or removed.

The core methods for working with this API are listed below:

Provides an array of RIDs for all render models that are being tracked.

render_model_new_scene_instance

Provides a new scene that contains all meshes needed to display the render model.

render_model_get_subaction_paths

Provides a list of subaction paths from your action map related to this render mode.

render_model_get_top_level_path

Returns the top level path associated with this render model (if any). Use the render_model_top_level_path_changed signal to react to this changing.

render_model_get_confidence

Returns the tracking confidence for the tracking data for this render model.

render_model_get_root_transform

Returns the root transform for this render model within our current reference space. This can be used to place the render model in space.

render_model_get_animatable_node_count

Returns the number of nodes in our render model scene that can be animated

render_model_get_animatable_node_name

Returns the name of the node that we can animate. Note that this node can be any number of levels deep within the scene.

render_model_is_animatable_node_visible

Returns true if this animatable node should be visible

render_model_get_animatable_node_transform

Returns the transform for this animatable node. This is a local transform that can be directly applied.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
class_name CollisionHands3D
extends AnimatableBody3D

func _ready():
    # Make sure these are set correctly.
    top_level = true
    sync_to_physics = false
    process_physics_priority = -90

func _physics_process(_delta):
    # Follow our parent node around.
    var dest_transform = get_parent().global_transform

    # We just apply rotation for this example.
    global_basis = dest_transform.basis

    # Attempt to move to where our tracked hand is.
    move_and_collide(dest_transform.origin - global_position)
```

---

## OpenXR Settings

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/openxr_settings.html

**Contents:**
- OpenXR Settings
- General settings
  - Enabled
  - Default Action Map
  - Form Factor
  - View Configuration
  - Reference Space
    - Local
    - Stage
    - Local Floor

OpenXR has its own set of settings that are applied when OpenXR starts. While it is possible for OpenXR extensions implemented through Godot plugins to add additional settings, we will only discuss the settings in the core of Godot here.

This setting enables the OpenXR module when Godot starts. This is required when the Vulkan backend is used. For other backends you can enable OpenXR at any time by calling initialize on the OpenXRInterface.

This also needs to be enabled to get access to the action map editor.

You can use the --xr-mode on command line switch to force this to on.

This specifies the path of the action map file that OpenXR will load and communicate to the XR Runtime.

This specifies whether your game is designed for:

Head Mounted devices such as a Meta Quest, Valve Index, or Magic Leap,

Handheld devices such as phones.

If the device on which you run your game does not match the selection here, OpenXR will fail to initialise.

This specifies the view configuration your game is designed for:

Mono, your game provides a single image output. E.g. phone based AR;

Stereo, your game provides stereo image output. E.g. head mounted devices.

If the device on which you run your game does not match the selection here, OpenXR will fail to initialise.

OpenXR has additional view configurations for very specific devices that Godot doesn't support yet. For instance, Varjo headsets have a quad view configuration that outputs two sets of stereo images. These may be supported in the near future.

Within XR all elements like the player's head and hands are tracked within a tracking volume. At the base of this tracking volume is our origin point, which maps our virtual space to the real space. There are however different scenarios that place this point in different locations, depending on the XR system used. In OpenXR these scenarios are well defined and selected by setting a reference space.

The local reference space places our origin point at the player's head by default. Some XR runtimes will do this each time your game starts, others will make the position persist over sessions.

This reference space however does not prevent the user from walking away so you will need to detect if the user does so if you wish to prevent the user from leaving the vehicle they are controlling, which could potentially be game breaking.

This reference space is the best option for games like flight simulators or racing simulators where we want to place the XROrigin3D node where the player's head should be.

When the user enacts the recenter option on their headset, the method of which is different per XR runtime, the XR runtime will move the XRCamera3D to the XROrigin3D node. The OpenXRInterface will also emit the pose_recentered signal so your game can react accordingly.

Any other XR tracked elements such as controllers or anchors will also be adjusted accordingly.

You should not call center_on_hmd when using this reference space.

The stage reference space is our default reference space and places our origin point at the center of our play space. For XR runtimes that allow you to draw out a guardian boundary this location and its orientation is often set by the user. Other XR runtimes may decide on the placement of this point by other means. It is however a stationary point in the real world.

This reference space is the best option for room scale games where the user is expected to walk around a larger space, or for games where there is a need to switch between game modes. See Room Scale for more information.

When the user enacts the recenter option on their headset, the method of which is different per XR runtime, the XR runtime will not change the origin point. The OpenXRInterface will emit the pose_recentered signal and it is up to the game to react appropriately. Not doing so will prevent your game from being accepted on various stores.

In Godot you can do this by calling the center_on_hmd function on the XRServer:

Calling XRServer.center_on_hmd(XRServer.RESET_BUT_KEEP_TILT, false) will move the XRCamera3D node to the XROrigin3D node similar to the Local reference space.

Calling XRServer.center_on_hmd(XRServer.RESET_BUT_KEEP_TILT, true) will move the XRCamera3D node above the XROrigin3D node keeping the player's height, similar to the Local Floor reference space.

Any other XR tracked elements such as controllers or anchors will also be adjusted accordingly.

The local floor reference space is similar to the local reference space as it positions the origin point where the player is. In this mode however the height of the player is kept. Same as with the local reference space, some XR runtimes will persist this location over sessions.

It is thus not guaranteed the player will be standing on the origin point, the only guarantee is that they were standing there when the user last recentered. The player is thus also free to walk away.

This reference space is the best option of games where the user is expected to stand in the same location or for AR type games where the user's interface elements are bound to the origin node and are quickly placed at the player's location on recenter.

When the user enacts the recenter option on their headset, the method of which is different per XR runtime, the XR runtime will move the XRCamera3D above the XROrigin3D node but keeping the player's height. The OpenXRInterface will also emit the pose_recentered signal so your game can react accordingly.

Be careful using this mode in combination with virtual movement of the player. The user recentering in this scenario can be unpredictable unless you counter the move when handling the recenter signal. This can even be game breaking as the effect in this scenario would be the player teleporting to whatever abstract location the origin point was placed at during virtual movement, including the ability for players teleporting into locations that should be off limits. It is better to use the Stage mode in this scenario and limit resetting to orientation only when a pose_recentered signal is received.

Any other XR tracked elements such as controllers or anchors will also be adjusted accordingly.

You should not call center_on_hmd when using this reference space.

The environment blend mode defines how our rendered output is blended into "the real world" provided this is supported by the headset.

Opaque means our output obscures the real world, we are in VR mode.

Additive means our output is added to the real world, this is an AR mode where optics do not allow us to fully obscure the real world (e.g. Hololens),

Alpha means our output is blended with the real world using the alpha output (viewport should have transparent background enabled), this is an AR mode where optics can fully obscure the real world (Magic Leap, all pass through devices, etc.).

If a mode is selected that is not supported by the headset, the first available mode will be selected.

Some OpenXR devices have separate systems for enabling/disabling passthrough. From Godot 4.3 onwards selecting the alpha blend mode will also perform these extra steps. This does require the latest vendor plugin to be installed.

Sets the foveation level used when rendering provided this feature is supported by the hardware used. Foveation is a technique where the further away from the center of the viewport we render content, the lower resolution we render at. Most XR runtimes only support fixed foveation, but some will take eye tracking into account and use the focal point for this effect.

The higher the level, the better the performance gains, but also the more reduction in quality there is in the user's peripheral vision.

Compatibility renderer only, for Mobile and Forward+ renderer, set the vrs_mode property on Viewport to VRS_XR.

This feature is disabled if post effects are used such as glow, bloom, or DOF.

When enabled the foveation level will be adjusted automatically depending on current GPU load. It will be adjusted between low and the select foveation level in the previous setting. It is therefore best to combine this setting with foveation level set to high.

Compatibility renderer only

If enabled an OpenXR supplied depth buffer will be used while rendering which is submitted alongside the rendered image. The XR runtime can use this for improved reprojection.

Enabling this feature will disable stencil support during rendering. Not many XR runtimes make use of this, it is advised to leave this setting off unless it provides noticeable benefits for your use case.

If enabled, this will result in an alert message presented to the user if OpenXR fails to start. We don't always receive feedback from the XR system as to why starting fails. If we do, we log this to the console. Common failure reasons are:

No OpenXR runtime is installed on the host system.

Microsoft's WMR OpenXR runtime is currently active, this only supports DirectX and will fail if OpenGL or Vulkan is used.

SteamVR is used but no headset is connected/turned on.

Disable this if you support a fallback mode in your game so it can be played in desktop mode when no VR headset is connected, or if you're handling the failure condition yourself by checking OpenXRInterface.is_initialized().

This subsection allows you to enable to various optional OpenXR extensions. Keep in mind that the extensions will only work if the OpenXR runtime (SteamVR, Oculus, etc) the project is ran with supports them.

Enabling this will log debug messages from the XR runtime.

This allows you to choose which debug messages are logged.

This enables the hand tracking extension when supported by the device used. This is on by default for legacy reasons. The hand tracking extension provides access to data that allows you to visualise the user's hands with correct finger positions. Depending on platform capabilities the hand tracking data can be inferred from controller inputs, come from data gloves, come from optical hand tracking sensors or any other applicable source.

If your game only supports controllers this should be turned off.

See the page on hand tracking for additional details.

Enabling this means hand tracking may use the exact position of fingers, usually what a headset camera sees.

Enabling this means hand tracking may use the controller itself, and infer where fingers are based on controller input or sensors on the controller.

Enabling this extension allows the use of two new hand tracking poses. Pinch pose which is the location between the thumb and index finger pointing forward, and poke pose which is at the tip of the index finger.

This also allows 3 more gesture based inputs. Pinch, when the user pinches their thumb and index finger together. Aim activation, when the index finger is fully extended. And Grasps, when the user makes a fist.

When a hand interaction profile and controller interaction profile are supplied, the runtime will switch between profiles depending on if optical tracking is used or if the user is holding a controller.

If only a hand interaction profile is supplied any runtime should use hand interaction even if a controller is being held.

This enables the eye gaze interaction extension when supported by the device used. When enabled we will get feedback from eye tracking through a pose situated between the user's eyes orientated in the direction the user is looking. This will be a unified orientation.

In order to use this functionality you need to edit your action map and add a new pose action, say eye_pose. Now add a new interaction profile for the eye gaze interaction and map the eye_pose:

Don't forget to save!

Next add a new XRController3D node to your origin node and set its tracker property to /user/eyes_ext and set its pose property to eye_pose.

Now you can add things to this controller node such as a raycast, and control things with your eyes.

This extension is used to query the XR runtime for 3D assets of the hardware being used, usually a controller, as well as the position of that hardware. You can find a detailed guide on how to use it here.

These control whether or not binding modifiers can be used. Binding modifiers are used to apply thresholds or offset values. You can find information on how to use and set them up on the XR action map page here.

Allow analog threshold binding modifiers.

Allow D-pad binding modifiers.

Please read the User-contributed notes policy before submitting a comment.

---

## PackedByteArray

**URL:** https://docs.godotengine.org/en/stable/classes/class_packedbytearray.html

**Contents:**
- PackedByteArray
- Description
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A packed array of bytes.

An array specifically designed to hold bytes. Packs data tightly, so it saves memory for large array sizes.

PackedByteArray also provides methods to encode/decode various types to/from bytes. The way values are encoded is an implementation detail and shouldn't be relied upon when interacting with external apps.

Note: Packed arrays are always passed by reference. To get a copy of an array that can be modified independently of the original array, use duplicate(). This is not the case for built-in properties and methods. In these cases the returned packed array is a copy, and changing it will not affect the original value. To update a built-in property of this type, modify the returned array and then assign it to the property again.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

PackedByteArray(from: PackedByteArray)

PackedByteArray(from: Array)

append_array(array: PackedByteArray)

bsearch(value: int, before: bool = true)

bswap16(offset: int = 0, count: int = -1)

bswap32(offset: int = 0, count: int = -1)

bswap64(offset: int = 0, count: int = -1)

compress(compression_mode: int = 0) const

count(value: int) const

decode_double(byte_offset: int) const

decode_float(byte_offset: int) const

decode_half(byte_offset: int) const

decode_s8(byte_offset: int) const

decode_s16(byte_offset: int) const

decode_s32(byte_offset: int) const

decode_s64(byte_offset: int) const

decode_u8(byte_offset: int) const

decode_u16(byte_offset: int) const

decode_u32(byte_offset: int) const

decode_u64(byte_offset: int) const

decode_var(byte_offset: int, allow_objects: bool = false) const

decode_var_size(byte_offset: int, allow_objects: bool = false) const

decompress(buffer_size: int, compression_mode: int = 0) const

decompress_dynamic(max_output_size: int, compression_mode: int = 0) const

encode_double(byte_offset: int, value: float)

encode_float(byte_offset: int, value: float)

encode_half(byte_offset: int, value: float)

encode_s8(byte_offset: int, value: int)

encode_s16(byte_offset: int, value: int)

encode_s32(byte_offset: int, value: int)

encode_s64(byte_offset: int, value: int)

encode_u8(byte_offset: int, value: int)

encode_u16(byte_offset: int, value: int)

encode_u32(byte_offset: int, value: int)

encode_u64(byte_offset: int, value: int)

encode_var(byte_offset: int, value: Variant, allow_objects: bool = false)

find(value: int, from: int = 0) const

get(index: int) const

get_string_from_ascii() const

get_string_from_multibyte_char(encoding: String = "") const

get_string_from_utf8() const

get_string_from_utf16() const

get_string_from_utf32() const

get_string_from_wchar() const

has(value: int) const

has_encoded_var(byte_offset: int, allow_objects: bool = false) const

insert(at_index: int, value: int)

push_back(value: int)

remove_at(index: int)

resize(new_size: int)

rfind(value: int, from: int = -1) const

set(index: int, value: int)

slice(begin: int, end: int = 2147483647) const

to_color_array() const

to_float32_array() const

to_float64_array() const

to_int32_array() const

to_int64_array() const

to_vector2_array() const

to_vector3_array() const

to_vector4_array() const

operator !=(right: PackedByteArray)

operator +(right: PackedByteArray)

operator ==(right: PackedByteArray)

operator [](index: int)

PackedByteArray PackedByteArray() 🔗

Constructs an empty PackedByteArray.

PackedByteArray PackedByteArray(from: PackedByteArray)

Constructs a PackedByteArray as a copy of the given PackedByteArray.

PackedByteArray PackedByteArray(from: Array)

Constructs a new PackedByteArray. Optionally, you can pass in a generic Array that will be converted.

bool append(value: int) 🔗

Appends an element at the end of the array (alias of push_back()).

void append_array(array: PackedByteArray) 🔗

Appends a PackedByteArray at the end of this array.

int bsearch(value: int, before: bool = true) 🔗

Finds the index of an existing value (or the insertion index that maintains sorting order, if the value is not yet present in the array) using binary search. Optionally, a before specifier can be passed. If false, the returned index comes after all existing entries of the value in the array.

Note: Calling bsearch() on an unsorted array results in unexpected behavior.

void bswap16(offset: int = 0, count: int = -1) 🔗

Swaps the byte order of count 16-bit segments of the array starting at offset. Swap is done in-place. If count is less than zero, all segments to the end of array are processed, if processed data size is not a multiple of 2, the byte after the last processed 16-bit segment is not modified.

void bswap32(offset: int = 0, count: int = -1) 🔗

Swaps the byte order of count 32-bit segments of the array starting at offset. Swap is done in-place. If count is less than zero, all segments to the end of array are processed, if processed data size is not a multiple of 4, bytes after the last processed 32-bit segment are not modified.

void bswap64(offset: int = 0, count: int = -1) 🔗

Swaps the byte order of count 64-bit segments of the array starting at offset. Swap is done in-place. If count is less than zero, all segments to the end of array are processed, if processed data size is not a multiple of 8, bytes after the last processed 64-bit segment are not modified.

Clears the array. This is equivalent to using resize() with a size of 0.

PackedByteArray compress(compression_mode: int = 0) const 🔗

Returns a new PackedByteArray with the data compressed. Set the compression mode using one of CompressionMode's constants.

int count(value: int) const 🔗

Returns the number of times an element is in the array.

float decode_double(byte_offset: int) const 🔗

Decodes a 64-bit floating-point number from the bytes starting at byte_offset. Fails if the byte count is insufficient. Returns 0.0 if a valid number can't be decoded.

float decode_float(byte_offset: int) const 🔗

Decodes a 32-bit floating-point number from the bytes starting at byte_offset. Fails if the byte count is insufficient. Returns 0.0 if a valid number can't be decoded.

float decode_half(byte_offset: int) const 🔗

Decodes a 16-bit floating-point number from the bytes starting at byte_offset. Fails if the byte count is insufficient. Returns 0.0 if a valid number can't be decoded.

int decode_s8(byte_offset: int) const 🔗

Decodes a 8-bit signed integer number from the bytes starting at byte_offset. Fails if the byte count is insufficient. Returns 0 if a valid number can't be decoded.

int decode_s16(byte_offset: int) const 🔗

Decodes a 16-bit signed integer number from the bytes starting at byte_offset. Fails if the byte count is insufficient. Returns 0 if a valid number can't be decoded.

int decode_s32(byte_offset: int) const 🔗

Decodes a 32-bit signed integer number from the bytes starting at byte_offset. Fails if the byte count is insufficient. Returns 0 if a valid number can't be decoded.

int decode_s64(byte_offset: int) const 🔗

Decodes a 64-bit signed integer number from the bytes starting at byte_offset. Fails if the byte count is insufficient. Returns 0 if a valid number can't be decoded.

int decode_u8(byte_offset: int) const 🔗

Decodes a 8-bit unsigned integer number from the bytes starting at byte_offset. Fails if the byte count is insufficient. Returns 0 if a valid number can't be decoded.

int decode_u16(byte_offset: int) const 🔗

Decodes a 16-bit unsigned integer number from the bytes starting at byte_offset. Fails if the byte count is insufficient. Returns 0 if a valid number can't be decoded.

int decode_u32(byte_offset: int) const 🔗

Decodes a 32-bit unsigned integer number from the bytes starting at byte_offset. Fails if the byte count is insufficient. Returns 0 if a valid number can't be decoded.

int decode_u64(byte_offset: int) const 🔗

Decodes a 64-bit unsigned integer number from the bytes starting at byte_offset. Fails if the byte count is insufficient. Returns 0 if a valid number can't be decoded.

Variant decode_var(byte_offset: int, allow_objects: bool = false) const 🔗

Decodes a Variant from the bytes starting at byte_offset. Returns null if a valid variant can't be decoded or the value is Object-derived and allow_objects is false.

int decode_var_size(byte_offset: int, allow_objects: bool = false) const 🔗

Decodes a size of a Variant from the bytes starting at byte_offset. Requires at least 4 bytes of data starting at the offset, otherwise fails.

PackedByteArray decompress(buffer_size: int, compression_mode: int = 0) const 🔗

Returns a new PackedByteArray with the data decompressed. Set buffer_size to the size of the uncompressed data. Set the compression mode using one of CompressionMode's constants.

Note: Decompression is not guaranteed to work with data not compressed by Godot, for example if data compressed with the deflate compression mode lacks a checksum or header.

PackedByteArray decompress_dynamic(max_output_size: int, compression_mode: int = 0) const 🔗

Returns a new PackedByteArray with the data decompressed. Set the compression mode using one of CompressionMode's constants. This method only accepts brotli, gzip, and deflate compression modes.

This method is potentially slower than decompress(), as it may have to re-allocate its output buffer multiple times while decompressing, whereas decompress() knows it's output buffer size from the beginning.

GZIP has a maximal compression ratio of 1032:1, meaning it's very possible for a small compressed payload to decompress to a potentially very large output. To guard against this, you may provide a maximum size this function is allowed to allocate in bytes via max_output_size. Passing -1 will allow for unbounded output. If any positive value is passed, and the decompression exceeds that amount in bytes, then an error will be returned.

Note: Decompression is not guaranteed to work with data not compressed by Godot, for example if data compressed with the deflate compression mode lacks a checksum or header.

PackedByteArray duplicate() 🔗

Creates a copy of the array, and returns it.

void encode_double(byte_offset: int, value: float) 🔗

Encodes a 64-bit floating-point number as bytes at the index of byte_offset bytes. The array must have at least 8 bytes of allocated space, starting at the offset.

void encode_float(byte_offset: int, value: float) 🔗

Encodes a 32-bit floating-point number as bytes at the index of byte_offset bytes. The array must have at least 4 bytes of space, starting at the offset.

void encode_half(byte_offset: int, value: float) 🔗

Encodes a 16-bit floating-point number as bytes at the index of byte_offset bytes. The array must have at least 2 bytes of space, starting at the offset.

void encode_s8(byte_offset: int, value: int) 🔗

Encodes a 8-bit signed integer number (signed byte) at the index of byte_offset bytes. The array must have at least 1 byte of space, starting at the offset.

void encode_s16(byte_offset: int, value: int) 🔗

Encodes a 16-bit signed integer number as bytes at the index of byte_offset bytes. The array must have at least 2 bytes of space, starting at the offset.

void encode_s32(byte_offset: int, value: int) 🔗

Encodes a 32-bit signed integer number as bytes at the index of byte_offset bytes. The array must have at least 4 bytes of space, starting at the offset.

void encode_s64(byte_offset: int, value: int) 🔗

Encodes a 64-bit signed integer number as bytes at the index of byte_offset bytes. The array must have at least 8 bytes of space, starting at the offset.

void encode_u8(byte_offset: int, value: int) 🔗

Encodes a 8-bit unsigned integer number (byte) at the index of byte_offset bytes. The array must have at least 1 byte of space, starting at the offset.

void encode_u16(byte_offset: int, value: int) 🔗

Encodes a 16-bit unsigned integer number as bytes at the index of byte_offset bytes. The array must have at least 2 bytes of space, starting at the offset.

void encode_u32(byte_offset: int, value: int) 🔗

Encodes a 32-bit unsigned integer number as bytes at the index of byte_offset bytes. The array must have at least 4 bytes of space, starting at the offset.

void encode_u64(byte_offset: int, value: int) 🔗

Encodes a 64-bit unsigned integer number as bytes at the index of byte_offset bytes. The array must have at least 8 bytes of space, starting at the offset.

int encode_var(byte_offset: int, value: Variant, allow_objects: bool = false) 🔗

Encodes a Variant at the index of byte_offset bytes. A sufficient space must be allocated, depending on the encoded variant's size. If allow_objects is false, Object-derived values are not permitted and will instead be serialized as ID-only.

bool erase(value: int) 🔗

Removes the first occurrence of a value from the array and returns true. If the value does not exist in the array, nothing happens and false is returned. To remove an element by index, use remove_at() instead.

void fill(value: int) 🔗

Assigns the given value to all elements in the array. This can typically be used together with resize() to create an array with a given size and initialized elements.

int find(value: int, from: int = 0) const 🔗

Searches the array for a value and returns its index or -1 if not found. Optionally, the initial search index can be passed.

int get(index: int) const 🔗

Returns the byte at the given index in the array. If index out-of-bounds or negative, this method fails and returns 0.

This method is similar (but not identical) to the [] operator. Most notably, when this method fails, it doesn't pause project execution if run from the editor.

String get_string_from_ascii() const 🔗

Converts ASCII/Latin-1 encoded array to String. Fast alternative to get_string_from_utf8() if the content is ASCII/Latin-1 only. Unlike the UTF-8 function this function maps every byte to a character in the array. Multibyte sequences will not be interpreted correctly. For parsing user input always use get_string_from_utf8(). This is the inverse of String.to_ascii_buffer().

String get_string_from_multibyte_char(encoding: String = "") const 🔗

Converts system multibyte code page encoded array to String. If conversion fails, empty string is returned. This is the inverse of String.to_multibyte_char_buffer().

The values permitted for encoding are system dependent. If encoding is empty string, system default encoding is used.

For Windows, see Code Page Identifiers .NET names.

For macOS and Linux/BSD, see libiconv library documentation and iconv --list for a list of supported encodings.

String get_string_from_utf8() const 🔗

Converts UTF-8 encoded array to String. Slower than get_string_from_ascii() but supports UTF-8 encoded data. Use this function if you are unsure about the source of the data. For user input this function should always be preferred. Returns empty string if source array is not valid UTF-8 string. This is the inverse of String.to_utf8_buffer().

String get_string_from_utf16() const 🔗

Converts UTF-16 encoded array to String. If the BOM is missing, little-endianness is assumed. Returns empty string if source array is not valid UTF-16 string. This is the inverse of String.to_utf16_buffer().

String get_string_from_utf32() const 🔗

Converts UTF-32 encoded array to String. Returns empty string if source array is not valid UTF-32 string. This is the inverse of String.to_utf32_buffer().

String get_string_from_wchar() const 🔗

Converts wide character (wchar_t, UTF-16 on Windows, UTF-32 on other platforms) encoded array to String. Returns empty string if source array is not valid wide string. This is the inverse of String.to_wchar_buffer().

bool has(value: int) const 🔗

Returns true if the array contains value.

bool has_encoded_var(byte_offset: int, allow_objects: bool = false) const 🔗

Returns true if a valid Variant value can be decoded at the byte_offset. Returns false otherwise or when the value is Object-derived and allow_objects is false.

String hex_encode() const 🔗

Returns a hexadecimal representation of this array as a String.

int insert(at_index: int, value: int) 🔗

Inserts a new element at a given position in the array. The position must be valid, or at the end of the array (idx == size()).

bool is_empty() const 🔗

Returns true if the array is empty.

bool push_back(value: int) 🔗

Appends an element at the end of the array.

void remove_at(index: int) 🔗

Removes an element from the array by index.

int resize(new_size: int) 🔗

Sets the size of the array. If the array is grown, reserves elements at the end of the array. If the array is shrunk, truncates the array to the new size. Calling resize() once and assigning the new values is faster than adding new elements one by one.

Returns @GlobalScope.OK on success, or one of the following Error constants if this method fails: @GlobalScope.ERR_INVALID_PARAMETER if the size is negative, or @GlobalScope.ERR_OUT_OF_MEMORY if allocations fail. Use size() to find the actual size of the array after resize.

Reverses the order of the elements in the array.

int rfind(value: int, from: int = -1) const 🔗

Searches the array in reverse order. Optionally, a start search index can be passed. If negative, the start index is considered relative to the end of the array.

void set(index: int, value: int) 🔗

Changes the byte at the given index.

Returns the number of elements in the array.

PackedByteArray slice(begin: int, end: int = 2147483647) const 🔗

Returns the slice of the PackedByteArray, from begin (inclusive) to end (exclusive), as a new PackedByteArray.

The absolute value of begin and end will be clamped to the array size, so the default value for end makes it slice to the size of the array by default (i.e. arr.slice(1) is a shorthand for arr.slice(1, arr.size())).

If either begin or end are negative, they will be relative to the end of the array (i.e. arr.slice(0, -2) is a shorthand for arr.slice(0, arr.size() - 2)).

Sorts the elements of the array in ascending order.

PackedColorArray to_color_array() const 🔗

Returns a copy of the data converted to a PackedColorArray, where each block of 16 bytes has been converted to a Color variant.

Note: The size of the input array must be a multiple of 16 (size of four 32-bit float variables). The size of the new array will be byte_array.size() / 16. If the original data can't be converted to Color variants, the resulting data is undefined.

PackedFloat32Array to_float32_array() const 🔗

Returns a copy of the data converted to a PackedFloat32Array, where each block of 4 bytes has been converted to a 32-bit float (C++ float).

The size of the input array must be a multiple of 4 (size of 32-bit float). The size of the new array will be byte_array.size() / 4.

If the original data can't be converted to 32-bit floats, the resulting data is undefined.

PackedFloat64Array to_float64_array() const 🔗

Returns a copy of the data converted to a PackedFloat64Array, where each block of 8 bytes has been converted to a 64-bit float (C++ double, Godot float).

The size of the input array must be a multiple of 8 (size of 64-bit double). The size of the new array will be byte_array.size() / 8.

If the original data can't be converted to 64-bit floats, the resulting data is undefined.

PackedInt32Array to_int32_array() const 🔗

Returns a copy of the data converted to a PackedInt32Array, where each block of 4 bytes has been converted to a signed 32-bit integer (C++ int32_t).

The size of the input array must be a multiple of 4 (size of 32-bit integer). The size of the new array will be byte_array.size() / 4.

If the original data can't be converted to signed 32-bit integers, the resulting data is undefined.

PackedInt64Array to_int64_array() const 🔗

Returns a copy of the data converted to a PackedInt64Array, where each block of 8 bytes has been converted to a signed 64-bit integer (C++ int64_t, Godot int).

The size of the input array must be a multiple of 8 (size of 64-bit integer). The size of the new array will be byte_array.size() / 8.

If the original data can't be converted to signed 64-bit integers, the resulting data is undefined.

PackedVector2Array to_vector2_array() const 🔗

Returns a copy of the data converted to a PackedVector2Array, where each block of 8 bytes or 16 bytes (32-bit or 64-bit) has been converted to a Vector2 variant.

Note: The size of the input array must be a multiple of 8 or 16 (depending on the build settings, see Vector2 for more details). The size of the new array will be byte_array.size() / (8 or 16). If the original data can't be converted to Vector2 variants, the resulting data is undefined.

PackedVector3Array to_vector3_array() const 🔗

Returns a copy of the data converted to a PackedVector3Array, where each block of 12 or 24 bytes (32-bit or 64-bit) has been converted to a Vector3 variant.

Note: The size of the input array must be a multiple of 12 or 24 (depending on the build settings, see Vector3 for more details). The size of the new array will be byte_array.size() / (12 or 24). If the original data can't be converted to Vector3 variants, the resulting data is undefined.

PackedVector4Array to_vector4_array() const 🔗

Returns a copy of the data converted to a PackedVector4Array, where each block of 16 or 32 bytes (32-bit or 64-bit) has been converted to a Vector4 variant.

Note: The size of the input array must be a multiple of 16 or 32 (depending on the build settings, see Vector4 for more details). The size of the new array will be byte_array.size() / (16 or 32). If the original data can't be converted to Vector4 variants, the resulting data is undefined.

bool operator !=(right: PackedByteArray) 🔗

Returns true if contents of the arrays differ.

PackedByteArray operator +(right: PackedByteArray) 🔗

Returns a new PackedByteArray with contents of right added at the end of this array. For better performance, consider using append_array() instead.

bool operator ==(right: PackedByteArray) 🔗

Returns true if contents of both arrays are the same, i.e. they have all equal bytes at the corresponding indices.

int operator [](index: int) 🔗

Returns the byte at index index. Negative indices can be used to access the elements starting from the end. Using index out of array's bounds will result in an error.

Note that the byte is returned as a 64-bit int.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var array = PackedByteArray([11, 46, 255])
print(array.hex_encode()) # Prints "0b2eff"
```

Example 2 (swift):
```swift
byte[] array = [11, 46, 255];
GD.Print(array.HexEncode()); // Prints "0b2eff"
```

---

## PackedColorArray

**URL:** https://docs.godotengine.org/en/stable/classes/class_packedcolorarray.html

**Contents:**
- PackedColorArray
- Description
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A packed array of Colors.

An array specifically designed to hold Color. Packs data tightly, so it saves memory for large array sizes.

Differences between packed arrays, typed arrays, and untyped arrays: Packed arrays are generally faster to iterate on and modify compared to a typed array of the same type (e.g. PackedColorArray versus Array[Color]). Also, packed arrays consume less memory. As a downside, packed arrays are less flexible as they don't offer as many convenience methods such as Array.map(). Typed arrays are in turn faster to iterate on and modify than untyped arrays.

Note: Packed arrays are always passed by reference. To get a copy of an array that can be modified independently of the original array, use duplicate(). This is not the case for built-in properties and methods. In these cases the returned packed array is a copy, and changing it will not affect the original value. To update a built-in property of this type, modify the returned array and then assign it to the property again.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

PackedColorArray(from: PackedColorArray)

PackedColorArray(from: Array)

append_array(array: PackedColorArray)

bsearch(value: Color, before: bool = true)

count(value: Color) const

find(value: Color, from: int = 0) const

get(index: int) const

has(value: Color) const

insert(at_index: int, value: Color)

push_back(value: Color)

remove_at(index: int)

resize(new_size: int)

rfind(value: Color, from: int = -1) const

set(index: int, value: Color)

slice(begin: int, end: int = 2147483647) const

to_byte_array() const

operator !=(right: PackedColorArray)

operator +(right: PackedColorArray)

operator ==(right: PackedColorArray)

operator [](index: int)

PackedColorArray PackedColorArray() 🔗

Constructs an empty PackedColorArray.

PackedColorArray PackedColorArray(from: PackedColorArray)

Constructs a PackedColorArray as a copy of the given PackedColorArray.

PackedColorArray PackedColorArray(from: Array)

Constructs a new PackedColorArray. Optionally, you can pass in a generic Array that will be converted.

Note: When initializing a PackedColorArray with elements, it must be initialized with an Array of Color values:

bool append(value: Color) 🔗

Appends an element at the end of the array (alias of push_back()).

void append_array(array: PackedColorArray) 🔗

Appends a PackedColorArray at the end of this array.

int bsearch(value: Color, before: bool = true) 🔗

Finds the index of an existing value (or the insertion index that maintains sorting order, if the value is not yet present in the array) using binary search. Optionally, a before specifier can be passed. If false, the returned index comes after all existing entries of the value in the array.

Note: Calling bsearch() on an unsorted array results in unexpected behavior.

Clears the array. This is equivalent to using resize() with a size of 0.

int count(value: Color) const 🔗

Returns the number of times an element is in the array.

PackedColorArray duplicate() 🔗

Creates a copy of the array, and returns it.

bool erase(value: Color) 🔗

Removes the first occurrence of a value from the array and returns true. If the value does not exist in the array, nothing happens and false is returned. To remove an element by index, use remove_at() instead.

void fill(value: Color) 🔗

Assigns the given value to all elements in the array. This can typically be used together with resize() to create an array with a given size and initialized elements.

int find(value: Color, from: int = 0) const 🔗

Searches the array for a value and returns its index or -1 if not found. Optionally, the initial search index can be passed.

Color get(index: int) const 🔗

Returns the Color at the given index in the array. If index out-of-bounds or negative, this method fails and returns Color(0, 0, 0, 1).

This method is similar (but not identical) to the [] operator. Most notably, when this method fails, it doesn't pause project execution if run from the editor.

bool has(value: Color) const 🔗

Returns true if the array contains value.

int insert(at_index: int, value: Color) 🔗

Inserts a new element at a given position in the array. The position must be valid, or at the end of the array (idx == size()).

bool is_empty() const 🔗

Returns true if the array is empty.

bool push_back(value: Color) 🔗

Appends a value to the array.

void remove_at(index: int) 🔗

Removes an element from the array by index.

int resize(new_size: int) 🔗

Sets the size of the array. If the array is grown, reserves elements at the end of the array. If the array is shrunk, truncates the array to the new size. Calling resize() once and assigning the new values is faster than adding new elements one by one.

Returns @GlobalScope.OK on success, or one of the following Error constants if this method fails: @GlobalScope.ERR_INVALID_PARAMETER if the size is negative, or @GlobalScope.ERR_OUT_OF_MEMORY if allocations fail. Use size() to find the actual size of the array after resize.

Reverses the order of the elements in the array.

int rfind(value: Color, from: int = -1) const 🔗

Searches the array in reverse order. Optionally, a start search index can be passed. If negative, the start index is considered relative to the end of the array.

void set(index: int, value: Color) 🔗

Changes the Color at the given index.

Returns the number of elements in the array.

PackedColorArray slice(begin: int, end: int = 2147483647) const 🔗

Returns the slice of the PackedColorArray, from begin (inclusive) to end (exclusive), as a new PackedColorArray.

The absolute value of begin and end will be clamped to the array size, so the default value for end makes it slice to the size of the array by default (i.e. arr.slice(1) is a shorthand for arr.slice(1, arr.size())).

If either begin or end are negative, they will be relative to the end of the array (i.e. arr.slice(0, -2) is a shorthand for arr.slice(0, arr.size() - 2)).

Sorts the elements of the array in ascending order.

PackedByteArray to_byte_array() const 🔗

Returns a PackedByteArray with each color encoded as bytes.

bool operator !=(right: PackedColorArray) 🔗

Returns true if contents of the arrays differ.

PackedColorArray operator +(right: PackedColorArray) 🔗

Returns a new PackedColorArray with contents of right added at the end of this array. For better performance, consider using append_array() instead.

bool operator ==(right: PackedColorArray) 🔗

Returns true if contents of both arrays are the same, i.e. they have all equal Colors at the corresponding indices.

Color operator [](index: int) 🔗

Returns the Color at index index. Negative indices can be used to access the elements starting from the end. Using index out of array's bounds will result in an error.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var array = PackedColorArray([Color(0.1, 0.2, 0.3), Color(0.4, 0.5, 0.6)])
```

---

## PackedFloat32Array

**URL:** https://docs.godotengine.org/en/stable/classes/class_packedfloat32array.html

**Contents:**
- PackedFloat32Array
- Description
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A packed array of 32-bit floating-point values.

An array specifically designed to hold 32-bit floating-point values (float). Packs data tightly, so it saves memory for large array sizes.

If you need to pack 64-bit floats tightly, see PackedFloat64Array.

Note: Packed arrays are always passed by reference. To get a copy of an array that can be modified independently of the original array, use duplicate(). This is not the case for built-in properties and methods. In these cases the returned packed array is a copy, and changing it will not affect the original value. To update a built-in property of this type, modify the returned array and then assign it to the property again.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

PackedFloat32Array(from: PackedFloat32Array)

PackedFloat32Array(from: Array)

append_array(array: PackedFloat32Array)

bsearch(value: float, before: bool = true)

count(value: float) const

find(value: float, from: int = 0) const

get(index: int) const

has(value: float) const

insert(at_index: int, value: float)

push_back(value: float)

remove_at(index: int)

resize(new_size: int)

rfind(value: float, from: int = -1) const

set(index: int, value: float)

slice(begin: int, end: int = 2147483647) const

to_byte_array() const

operator !=(right: PackedFloat32Array)

operator +(right: PackedFloat32Array)

operator ==(right: PackedFloat32Array)

operator [](index: int)

PackedFloat32Array PackedFloat32Array() 🔗

Constructs an empty PackedFloat32Array.

PackedFloat32Array PackedFloat32Array(from: PackedFloat32Array)

Constructs a PackedFloat32Array as a copy of the given PackedFloat32Array.

PackedFloat32Array PackedFloat32Array(from: Array)

Constructs a new PackedFloat32Array. Optionally, you can pass in a generic Array that will be converted.

bool append(value: float) 🔗

Appends an element at the end of the array (alias of push_back()).

void append_array(array: PackedFloat32Array) 🔗

Appends a PackedFloat32Array at the end of this array.

int bsearch(value: float, before: bool = true) 🔗

Finds the index of an existing value (or the insertion index that maintains sorting order, if the value is not yet present in the array) using binary search. Optionally, a before specifier can be passed. If false, the returned index comes after all existing entries of the value in the array.

Note: Calling bsearch() on an unsorted array results in unexpected behavior.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

Clears the array. This is equivalent to using resize() with a size of 0.

int count(value: float) const 🔗

Returns the number of times an element is in the array.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

PackedFloat32Array duplicate() 🔗

Creates a copy of the array, and returns it.

bool erase(value: float) 🔗

Removes the first occurrence of a value from the array and returns true. If the value does not exist in the array, nothing happens and false is returned. To remove an element by index, use remove_at() instead.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

void fill(value: float) 🔗

Assigns the given value to all elements in the array. This can typically be used together with resize() to create an array with a given size and initialized elements.

int find(value: float, from: int = 0) const 🔗

Searches the array for a value and returns its index or -1 if not found. Optionally, the initial search index can be passed.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

float get(index: int) const 🔗

Returns the 32-bit float at the given index in the array. If index out-of-bounds or negative, this method fails and returns 0.0.

This method is similar (but not identical) to the [] operator. Most notably, when this method fails, it doesn't pause project execution if run from the editor.

bool has(value: float) const 🔗

Returns true if the array contains value.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

int insert(at_index: int, value: float) 🔗

Inserts a new element at a given position in the array. The position must be valid, or at the end of the array (idx == size()).

bool is_empty() const 🔗

Returns true if the array is empty.

bool push_back(value: float) 🔗

Appends an element at the end of the array.

void remove_at(index: int) 🔗

Removes an element from the array by index.

int resize(new_size: int) 🔗

Sets the size of the array. If the array is grown, reserves elements at the end of the array. If the array is shrunk, truncates the array to the new size. Calling resize() once and assigning the new values is faster than adding new elements one by one.

Returns @GlobalScope.OK on success, or one of the following Error constants if this method fails: @GlobalScope.ERR_INVALID_PARAMETER if the size is negative, or @GlobalScope.ERR_OUT_OF_MEMORY if allocations fail. Use size() to find the actual size of the array after resize.

Reverses the order of the elements in the array.

int rfind(value: float, from: int = -1) const 🔗

Searches the array in reverse order. Optionally, a start search index can be passed. If negative, the start index is considered relative to the end of the array.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

void set(index: int, value: float) 🔗

Changes the float at the given index.

Returns the number of elements in the array.

PackedFloat32Array slice(begin: int, end: int = 2147483647) const 🔗

Returns the slice of the PackedFloat32Array, from begin (inclusive) to end (exclusive), as a new PackedFloat32Array.

The absolute value of begin and end will be clamped to the array size, so the default value for end makes it slice to the size of the array by default (i.e. arr.slice(1) is a shorthand for arr.slice(1, arr.size())).

If either begin or end are negative, they will be relative to the end of the array (i.e. arr.slice(0, -2) is a shorthand for arr.slice(0, arr.size() - 2)).

Sorts the elements of the array in ascending order.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

PackedByteArray to_byte_array() const 🔗

Returns a copy of the data converted to a PackedByteArray, where each element has been encoded as 4 bytes.

The size of the new array will be float32_array.size() * 4.

bool operator !=(right: PackedFloat32Array) 🔗

Returns true if contents of the arrays differ.

PackedFloat32Array operator +(right: PackedFloat32Array) 🔗

Returns a new PackedFloat32Array with contents of right added at the end of this array. For better performance, consider using append_array() instead.

bool operator ==(right: PackedFloat32Array) 🔗

Returns true if contents of both arrays are the same, i.e. they have all equal floats at the corresponding indices.

float operator [](index: int) 🔗

Returns the float at index index. Negative indices can be used to access the elements starting from the end. Using index out of array's bounds will result in an error.

Note that float type is 64-bit, unlike the values stored in the array.

Please read the User-contributed notes policy before submitting a comment.

---

## PackedFloat64Array

**URL:** https://docs.godotengine.org/en/stable/classes/class_packedfloat64array.html

**Contents:**
- PackedFloat64Array
- Description
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A packed array of 64-bit floating-point values.

An array specifically designed to hold 64-bit floating-point values (double). Packs data tightly, so it saves memory for large array sizes.

If you only need to pack 32-bit floats tightly, see PackedFloat32Array for a more memory-friendly alternative.

Differences between packed arrays, typed arrays, and untyped arrays: Packed arrays are generally faster to iterate on and modify compared to a typed array of the same type (e.g. PackedFloat64Array versus Array[float]). Also, packed arrays consume less memory. As a downside, packed arrays are less flexible as they don't offer as many convenience methods such as Array.map(). Typed arrays are in turn faster to iterate on and modify than untyped arrays.

Note: Packed arrays are always passed by reference. To get a copy of an array that can be modified independently of the original array, use duplicate(). This is not the case for built-in properties and methods. In these cases the returned packed array is a copy, and changing it will not affect the original value. To update a built-in property of this type, modify the returned array and then assign it to the property again.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

PackedFloat64Array(from: PackedFloat64Array)

PackedFloat64Array(from: Array)

append_array(array: PackedFloat64Array)

bsearch(value: float, before: bool = true)

count(value: float) const

find(value: float, from: int = 0) const

get(index: int) const

has(value: float) const

insert(at_index: int, value: float)

push_back(value: float)

remove_at(index: int)

resize(new_size: int)

rfind(value: float, from: int = -1) const

set(index: int, value: float)

slice(begin: int, end: int = 2147483647) const

to_byte_array() const

operator !=(right: PackedFloat64Array)

operator +(right: PackedFloat64Array)

operator ==(right: PackedFloat64Array)

operator [](index: int)

PackedFloat64Array PackedFloat64Array() 🔗

Constructs an empty PackedFloat64Array.

PackedFloat64Array PackedFloat64Array(from: PackedFloat64Array)

Constructs a PackedFloat64Array as a copy of the given PackedFloat64Array.

PackedFloat64Array PackedFloat64Array(from: Array)

Constructs a new PackedFloat64Array. Optionally, you can pass in a generic Array that will be converted.

bool append(value: float) 🔗

Appends an element at the end of the array (alias of push_back()).

void append_array(array: PackedFloat64Array) 🔗

Appends a PackedFloat64Array at the end of this array.

int bsearch(value: float, before: bool = true) 🔗

Finds the index of an existing value (or the insertion index that maintains sorting order, if the value is not yet present in the array) using binary search. Optionally, a before specifier can be passed. If false, the returned index comes after all existing entries of the value in the array.

Note: Calling bsearch() on an unsorted array results in unexpected behavior.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

Clears the array. This is equivalent to using resize() with a size of 0.

int count(value: float) const 🔗

Returns the number of times an element is in the array.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

PackedFloat64Array duplicate() 🔗

Creates a copy of the array, and returns it.

bool erase(value: float) 🔗

Removes the first occurrence of a value from the array and returns true. If the value does not exist in the array, nothing happens and false is returned. To remove an element by index, use remove_at() instead.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

void fill(value: float) 🔗

Assigns the given value to all elements in the array. This can typically be used together with resize() to create an array with a given size and initialized elements.

int find(value: float, from: int = 0) const 🔗

Searches the array for a value and returns its index or -1 if not found. Optionally, the initial search index can be passed.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

float get(index: int) const 🔗

Returns the 64-bit float at the given index in the array. If index out-of-bounds or negative, this method fails and returns 0.0.

This method is similar (but not identical) to the [] operator. Most notably, when this method fails, it doesn't pause project execution if run from the editor.

bool has(value: float) const 🔗

Returns true if the array contains value.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

int insert(at_index: int, value: float) 🔗

Inserts a new element at a given position in the array. The position must be valid, or at the end of the array (idx == size()).

bool is_empty() const 🔗

Returns true if the array is empty.

bool push_back(value: float) 🔗

Appends an element at the end of the array.

void remove_at(index: int) 🔗

Removes an element from the array by index.

int resize(new_size: int) 🔗

Sets the size of the array. If the array is grown, reserves elements at the end of the array. If the array is shrunk, truncates the array to the new size. Calling resize() once and assigning the new values is faster than adding new elements one by one.

Returns @GlobalScope.OK on success, or one of the following Error constants if this method fails: @GlobalScope.ERR_INVALID_PARAMETER if the size is negative, or @GlobalScope.ERR_OUT_OF_MEMORY if allocations fail. Use size() to find the actual size of the array after resize.

Reverses the order of the elements in the array.

int rfind(value: float, from: int = -1) const 🔗

Searches the array in reverse order. Optionally, a start search index can be passed. If negative, the start index is considered relative to the end of the array.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

void set(index: int, value: float) 🔗

Changes the float at the given index.

Returns the number of elements in the array.

PackedFloat64Array slice(begin: int, end: int = 2147483647) const 🔗

Returns the slice of the PackedFloat64Array, from begin (inclusive) to end (exclusive), as a new PackedFloat64Array.

The absolute value of begin and end will be clamped to the array size, so the default value for end makes it slice to the size of the array by default (i.e. arr.slice(1) is a shorthand for arr.slice(1, arr.size())).

If either begin or end are negative, they will be relative to the end of the array (i.e. arr.slice(0, -2) is a shorthand for arr.slice(0, arr.size() - 2)).

Sorts the elements of the array in ascending order.

Note: @GDScript.NAN doesn't behave the same as other numbers. Therefore, the results from this method may not be accurate if NaNs are included.

PackedByteArray to_byte_array() const 🔗

Returns a copy of the data converted to a PackedByteArray, where each element has been encoded as 8 bytes.

The size of the new array will be float64_array.size() * 8.

bool operator !=(right: PackedFloat64Array) 🔗

Returns true if contents of the arrays differ.

PackedFloat64Array operator +(right: PackedFloat64Array) 🔗

Returns a new PackedFloat64Array with contents of right added at the end of this array. For better performance, consider using append_array() instead.

bool operator ==(right: PackedFloat64Array) 🔗

Returns true if contents of both arrays are the same, i.e. they have all equal doubles at the corresponding indices.

float operator [](index: int) 🔗

Returns the float at index index. Negative indices can be used to access the elements starting from the end. Using index out of array's bounds will result in an error.

Please read the User-contributed notes policy before submitting a comment.

---

## PackedInt32Array

**URL:** https://docs.godotengine.org/en/stable/classes/class_packedint32array.html

**Contents:**
- PackedInt32Array
- Description
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A packed array of 32-bit integers.

An array specifically designed to hold 32-bit integer values. Packs data tightly, so it saves memory for large array sizes.

Note: This type stores signed 32-bit integers, which means it can take values in the interval [-2^31, 2^31 - 1], i.e. [-2147483648, 2147483647]. Exceeding those bounds will wrap around. In comparison, int uses signed 64-bit integers which can hold much larger values. If you need to pack 64-bit integers tightly, see PackedInt64Array.

Note: Packed arrays are always passed by reference. To get a copy of an array that can be modified independently of the original array, use duplicate(). This is not the case for built-in properties and methods. In these cases the returned packed array is a copy, and changing it will not affect the original value. To update a built-in property of this type, modify the returned array and then assign it to the property again.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

PackedInt32Array(from: PackedInt32Array)

PackedInt32Array(from: Array)

append_array(array: PackedInt32Array)

bsearch(value: int, before: bool = true)

count(value: int) const

find(value: int, from: int = 0) const

get(index: int) const

has(value: int) const

insert(at_index: int, value: int)

push_back(value: int)

remove_at(index: int)

resize(new_size: int)

rfind(value: int, from: int = -1) const

set(index: int, value: int)

slice(begin: int, end: int = 2147483647) const

to_byte_array() const

operator !=(right: PackedInt32Array)

operator +(right: PackedInt32Array)

operator ==(right: PackedInt32Array)

operator [](index: int)

PackedInt32Array PackedInt32Array() 🔗

Constructs an empty PackedInt32Array.

PackedInt32Array PackedInt32Array(from: PackedInt32Array)

Constructs a PackedInt32Array as a copy of the given PackedInt32Array.

PackedInt32Array PackedInt32Array(from: Array)

Constructs a new PackedInt32Array. Optionally, you can pass in a generic Array that will be converted.

bool append(value: int) 🔗

Appends an element at the end of the array (alias of push_back()).

void append_array(array: PackedInt32Array) 🔗

Appends a PackedInt32Array at the end of this array.

int bsearch(value: int, before: bool = true) 🔗

Finds the index of an existing value (or the insertion index that maintains sorting order, if the value is not yet present in the array) using binary search. Optionally, a before specifier can be passed. If false, the returned index comes after all existing entries of the value in the array.

Note: Calling bsearch() on an unsorted array results in unexpected behavior.

Clears the array. This is equivalent to using resize() with a size of 0.

int count(value: int) const 🔗

Returns the number of times an element is in the array.

PackedInt32Array duplicate() 🔗

Creates a copy of the array, and returns it.

bool erase(value: int) 🔗

Removes the first occurrence of a value from the array and returns true. If the value does not exist in the array, nothing happens and false is returned. To remove an element by index, use remove_at() instead.

void fill(value: int) 🔗

Assigns the given value to all elements in the array. This can typically be used together with resize() to create an array with a given size and initialized elements.

int find(value: int, from: int = 0) const 🔗

Searches the array for a value and returns its index or -1 if not found. Optionally, the initial search index can be passed.

int get(index: int) const 🔗

Returns the 32-bit integer at the given index in the array. If index out-of-bounds or negative, this method fails and returns 0.

This method is similar (but not identical) to the [] operator. Most notably, when this method fails, it doesn't pause project execution if run from the editor.

bool has(value: int) const 🔗

Returns true if the array contains value.

int insert(at_index: int, value: int) 🔗

Inserts a new integer at a given position in the array. The position must be valid, or at the end of the array (idx == size()).

bool is_empty() const 🔗

Returns true if the array is empty.

bool push_back(value: int) 🔗

Appends a value to the array.

void remove_at(index: int) 🔗

Removes an element from the array by index.

int resize(new_size: int) 🔗

Sets the size of the array. If the array is grown, reserves elements at the end of the array. If the array is shrunk, truncates the array to the new size. Calling resize() once and assigning the new values is faster than adding new elements one by one.

Returns @GlobalScope.OK on success, or one of the following Error constants if this method fails: @GlobalScope.ERR_INVALID_PARAMETER if the size is negative, or @GlobalScope.ERR_OUT_OF_MEMORY if allocations fail. Use size() to find the actual size of the array after resize.

Reverses the order of the elements in the array.

int rfind(value: int, from: int = -1) const 🔗

Searches the array in reverse order. Optionally, a start search index can be passed. If negative, the start index is considered relative to the end of the array.

void set(index: int, value: int) 🔗

Changes the integer at the given index.

Returns the number of elements in the array.

PackedInt32Array slice(begin: int, end: int = 2147483647) const 🔗

Returns the slice of the PackedInt32Array, from begin (inclusive) to end (exclusive), as a new PackedInt32Array.

The absolute value of begin and end will be clamped to the array size, so the default value for end makes it slice to the size of the array by default (i.e. arr.slice(1) is a shorthand for arr.slice(1, arr.size())).

If either begin or end are negative, they will be relative to the end of the array (i.e. arr.slice(0, -2) is a shorthand for arr.slice(0, arr.size() - 2)).

Sorts the elements of the array in ascending order.

PackedByteArray to_byte_array() const 🔗

Returns a copy of the data converted to a PackedByteArray, where each element has been encoded as 4 bytes.

The size of the new array will be int32_array.size() * 4.

bool operator !=(right: PackedInt32Array) 🔗

Returns true if contents of the arrays differ.

PackedInt32Array operator +(right: PackedInt32Array) 🔗

Returns a new PackedInt32Array with contents of right added at the end of this array. For better performance, consider using append_array() instead.

bool operator ==(right: PackedInt32Array) 🔗

Returns true if contents of both arrays are the same, i.e. they have all equal ints at the corresponding indices.

int operator [](index: int) 🔗

Returns the int at index index. Negative indices can be used to access the elements starting from the end. Using index out of array's bounds will result in an error.

Note that int type is 64-bit, unlike the values stored in the array.

Please read the User-contributed notes policy before submitting a comment.

---

## PackedInt64Array

**URL:** https://docs.godotengine.org/en/stable/classes/class_packedint64array.html

**Contents:**
- PackedInt64Array
- Description
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A packed array of 64-bit integers.

An array specifically designed to hold 64-bit integer values. Packs data tightly, so it saves memory for large array sizes.

Note: This type stores signed 64-bit integers, which means it can take values in the interval [-2^63, 2^63 - 1], i.e. [-9223372036854775808, 9223372036854775807]. Exceeding those bounds will wrap around. If you only need to pack 32-bit integers tightly, see PackedInt32Array for a more memory-friendly alternative.

Differences between packed arrays, typed arrays, and untyped arrays: Packed arrays are generally faster to iterate on and modify compared to a typed array of the same type (e.g. PackedInt64Array versus Array[int]). Also, packed arrays consume less memory. As a downside, packed arrays are less flexible as they don't offer as many convenience methods such as Array.map(). Typed arrays are in turn faster to iterate on and modify than untyped arrays.

Note: Packed arrays are always passed by reference. To get a copy of an array that can be modified independently of the original array, use duplicate(). This is not the case for built-in properties and methods. In these cases the returned packed array is a copy, and changing it will not affect the original value. To update a built-in property of this type, modify the returned array and then assign it to the property again.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

PackedInt64Array(from: PackedInt64Array)

PackedInt64Array(from: Array)

append_array(array: PackedInt64Array)

bsearch(value: int, before: bool = true)

count(value: int) const

find(value: int, from: int = 0) const

get(index: int) const

has(value: int) const

insert(at_index: int, value: int)

push_back(value: int)

remove_at(index: int)

resize(new_size: int)

rfind(value: int, from: int = -1) const

set(index: int, value: int)

slice(begin: int, end: int = 2147483647) const

to_byte_array() const

operator !=(right: PackedInt64Array)

operator +(right: PackedInt64Array)

operator ==(right: PackedInt64Array)

operator [](index: int)

PackedInt64Array PackedInt64Array() 🔗

Constructs an empty PackedInt64Array.

PackedInt64Array PackedInt64Array(from: PackedInt64Array)

Constructs a PackedInt64Array as a copy of the given PackedInt64Array.

PackedInt64Array PackedInt64Array(from: Array)

Constructs a new PackedInt64Array. Optionally, you can pass in a generic Array that will be converted.

bool append(value: int) 🔗

Appends an element at the end of the array (alias of push_back()).

void append_array(array: PackedInt64Array) 🔗

Appends a PackedInt64Array at the end of this array.

int bsearch(value: int, before: bool = true) 🔗

Finds the index of an existing value (or the insertion index that maintains sorting order, if the value is not yet present in the array) using binary search. Optionally, a before specifier can be passed. If false, the returned index comes after all existing entries of the value in the array.

Note: Calling bsearch() on an unsorted array results in unexpected behavior.

Clears the array. This is equivalent to using resize() with a size of 0.

int count(value: int) const 🔗

Returns the number of times an element is in the array.

PackedInt64Array duplicate() 🔗

Creates a copy of the array, and returns it.

bool erase(value: int) 🔗

Removes the first occurrence of a value from the array and returns true. If the value does not exist in the array, nothing happens and false is returned. To remove an element by index, use remove_at() instead.

void fill(value: int) 🔗

Assigns the given value to all elements in the array. This can typically be used together with resize() to create an array with a given size and initialized elements.

int find(value: int, from: int = 0) const 🔗

Searches the array for a value and returns its index or -1 if not found. Optionally, the initial search index can be passed.

int get(index: int) const 🔗

Returns the 64-bit integer at the given index in the array. If index out-of-bounds or negative, this method fails and returns 0.

This method is similar (but not identical) to the [] operator. Most notably, when this method fails, it doesn't pause project execution if run from the editor.

bool has(value: int) const 🔗

Returns true if the array contains value.

int insert(at_index: int, value: int) 🔗

Inserts a new integer at a given position in the array. The position must be valid, or at the end of the array (idx == size()).

bool is_empty() const 🔗

Returns true if the array is empty.

bool push_back(value: int) 🔗

Appends a value to the array.

void remove_at(index: int) 🔗

Removes an element from the array by index.

int resize(new_size: int) 🔗

Sets the size of the array. If the array is grown, reserves elements at the end of the array. If the array is shrunk, truncates the array to the new size. Calling resize() once and assigning the new values is faster than adding new elements one by one.

Returns @GlobalScope.OK on success, or one of the following Error constants if this method fails: @GlobalScope.ERR_INVALID_PARAMETER if the size is negative, or @GlobalScope.ERR_OUT_OF_MEMORY if allocations fail. Use size() to find the actual size of the array after resize.

Reverses the order of the elements in the array.

int rfind(value: int, from: int = -1) const 🔗

Searches the array in reverse order. Optionally, a start search index can be passed. If negative, the start index is considered relative to the end of the array.

void set(index: int, value: int) 🔗

Changes the integer at the given index.

Returns the number of elements in the array.

PackedInt64Array slice(begin: int, end: int = 2147483647) const 🔗

Returns the slice of the PackedInt64Array, from begin (inclusive) to end (exclusive), as a new PackedInt64Array.

The absolute value of begin and end will be clamped to the array size, so the default value for end makes it slice to the size of the array by default (i.e. arr.slice(1) is a shorthand for arr.slice(1, arr.size())).

If either begin or end are negative, they will be relative to the end of the array (i.e. arr.slice(0, -2) is a shorthand for arr.slice(0, arr.size() - 2)).

Sorts the elements of the array in ascending order.

PackedByteArray to_byte_array() const 🔗

Returns a copy of the data converted to a PackedByteArray, where each element has been encoded as 8 bytes.

The size of the new array will be int64_array.size() * 8.

bool operator !=(right: PackedInt64Array) 🔗

Returns true if contents of the arrays differ.

PackedInt64Array operator +(right: PackedInt64Array) 🔗

Returns a new PackedInt64Array with contents of right added at the end of this array. For better performance, consider using append_array() instead.

bool operator ==(right: PackedInt64Array) 🔗

Returns true if contents of both arrays are the same, i.e. they have all equal ints at the corresponding indices.

int operator [](index: int) 🔗

Returns the int at index index. Negative indices can be used to access the elements starting from the end. Using index out of array's bounds will result in an error.

Please read the User-contributed notes policy before submitting a comment.

---

## PackedStringArray

**URL:** https://docs.godotengine.org/en/stable/classes/class_packedstringarray.html

**Contents:**
- PackedStringArray
- Description
- Tutorials
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A packed array of Strings.

An array specifically designed to hold Strings. Packs data tightly, so it saves memory for large array sizes.

If you want to join the strings in the array, use String.join().

Differences between packed arrays, typed arrays, and untyped arrays: Packed arrays are generally faster to iterate on and modify compared to a typed array of the same type (e.g. PackedStringArray versus Array[String]). Also, packed arrays consume less memory. As a downside, packed arrays are less flexible as they don't offer as many convenience methods such as Array.map(). Typed arrays are in turn faster to iterate on and modify than untyped arrays.

Note: Packed arrays are always passed by reference. To get a copy of an array that can be modified independently of the original array, use duplicate(). This is not the case for built-in properties and methods. In these cases the returned packed array is a copy, and changing it will not affect the original value. To update a built-in property of this type, modify the returned array and then assign it to the property again.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

Operating System Testing Demo

PackedStringArray(from: PackedStringArray)

PackedStringArray(from: Array)

append(value: String)

append_array(array: PackedStringArray)

bsearch(value: String, before: bool = true)

count(value: String) const

find(value: String, from: int = 0) const

get(index: int) const

has(value: String) const

insert(at_index: int, value: String)

push_back(value: String)

remove_at(index: int)

resize(new_size: int)

rfind(value: String, from: int = -1) const

set(index: int, value: String)

slice(begin: int, end: int = 2147483647) const

to_byte_array() const

operator !=(right: PackedStringArray)

operator +(right: PackedStringArray)

operator ==(right: PackedStringArray)

operator [](index: int)

PackedStringArray PackedStringArray() 🔗

Constructs an empty PackedStringArray.

PackedStringArray PackedStringArray(from: PackedStringArray)

Constructs a PackedStringArray as a copy of the given PackedStringArray.

PackedStringArray PackedStringArray(from: Array)

Constructs a new PackedStringArray. Optionally, you can pass in a generic Array that will be converted.

bool append(value: String) 🔗

Appends an element at the end of the array (alias of push_back()).

void append_array(array: PackedStringArray) 🔗

Appends a PackedStringArray at the end of this array.

int bsearch(value: String, before: bool = true) 🔗

Finds the index of an existing value (or the insertion index that maintains sorting order, if the value is not yet present in the array) using binary search. Optionally, a before specifier can be passed. If false, the returned index comes after all existing entries of the value in the array.

Note: Calling bsearch() on an unsorted array results in unexpected behavior.

Clears the array. This is equivalent to using resize() with a size of 0.

int count(value: String) const 🔗

Returns the number of times an element is in the array.

PackedStringArray duplicate() 🔗

Creates a copy of the array, and returns it.

bool erase(value: String) 🔗

Removes the first occurrence of a value from the array and returns true. If the value does not exist in the array, nothing happens and false is returned. To remove an element by index, use remove_at() instead.

void fill(value: String) 🔗

Assigns the given value to all elements in the array. This can typically be used together with resize() to create an array with a given size and initialized elements.

int find(value: String, from: int = 0) const 🔗

Searches the array for a value and returns its index or -1 if not found. Optionally, the initial search index can be passed.

String get(index: int) const 🔗

Returns the String at the given index in the array. Returns an empty string and prints an error if the access is out of bounds. Negative indices are not supported; they will always consider the value to be out of bounds and return an empty string.

This is similar to using the [] operator (array[index]), except that operator supports negative indices and causes a debugger break if out-of-bounds access is performed.

bool has(value: String) const 🔗

Returns true if the array contains value.

int insert(at_index: int, value: String) 🔗

Inserts a new element at a given position in the array. The position must be valid, or at the end of the array (idx == size()).

bool is_empty() const 🔗

Returns true if the array is empty.

bool push_back(value: String) 🔗

Appends a string element at end of the array.

void remove_at(index: int) 🔗

Removes an element from the array by index.

int resize(new_size: int) 🔗

Sets the size of the array. If the array is grown, reserves elements at the end of the array. If the array is shrunk, truncates the array to the new size. Calling resize() once and assigning the new values is faster than adding new elements one by one.

Returns @GlobalScope.OK on success, or one of the following Error constants if this method fails: @GlobalScope.ERR_INVALID_PARAMETER if the size is negative, or @GlobalScope.ERR_OUT_OF_MEMORY if allocations fail. Use size() to find the actual size of the array after resize.

Reverses the order of the elements in the array.

int rfind(value: String, from: int = -1) const 🔗

Searches the array in reverse order. Optionally, a start search index can be passed. If negative, the start index is considered relative to the end of the array.

void set(index: int, value: String) 🔗

Changes the String at the given index.

Returns the number of elements in the array.

PackedStringArray slice(begin: int, end: int = 2147483647) const 🔗

Returns the slice of the PackedStringArray, from begin (inclusive) to end (exclusive), as a new PackedStringArray.

The absolute value of begin and end will be clamped to the array size, so the default value for end makes it slice to the size of the array by default (i.e. arr.slice(1) is a shorthand for arr.slice(1, arr.size())).

If either begin or end are negative, they will be relative to the end of the array (i.e. arr.slice(0, -2) is a shorthand for arr.slice(0, arr.size() - 2)).

Sorts the elements of the array in ascending order.

PackedByteArray to_byte_array() const 🔗

Returns a PackedByteArray with each string encoded as UTF-8. Strings are null terminated.

bool operator !=(right: PackedStringArray) 🔗

Returns true if contents of the arrays differ.

PackedStringArray operator +(right: PackedStringArray) 🔗

Returns a new PackedStringArray with contents of right added at the end of this array. For better performance, consider using append_array() instead.

bool operator ==(right: PackedStringArray) 🔗

Returns true if contents of both arrays are the same, i.e. they have all equal Strings at the corresponding indices.

String operator [](index: int) 🔗

Returns the String at index index. Negative indices can be used to access the elements starting from the end. Using index out of array's bounds will result in an error.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var string_array = PackedStringArray(["hello", "world"])
var string = " ".join(string_array)
print(string) # "hello world"
```

---

## PlaceholderCubemapArray

**URL:** https://docs.godotengine.org/en/stable/classes/class_placeholdercubemaparray.html

**Contents:**
- PlaceholderCubemapArray
- Description
- User-contributed notes

Inherits: PlaceholderTextureLayered < TextureLayered < Texture < Resource < RefCounted < Object

A CubemapArray without image data.

This class replaces a CubemapArray or a CubemapArray-derived class in 2 conditions:

In dedicated server mode, where the image data shouldn't affect game logic. This allows reducing the exported PCK's size significantly.

When the CubemapArray-derived class is missing, for example when using a different engine version.

Note: This class is not intended for rendering or for use in shaders. Operations like calculating UV are not guaranteed to work.

Please read the User-contributed notes policy before submitting a comment.

---

## Platform-specific

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/index.html

**Contents:**
- Platform-specific

Godot supports both running the editor and exporting projects on several platforms. Usage of the engine is generally similar across platforms, but there are some platform-specific considerations, which are covered in this section.

For platform-specific versions of the editor, see Using the XR editor, Using the Android editor, and Using the Web editor. For exporting to specific platforms, see the Export section.

---

## ProgressBar

**URL:** https://docs.godotengine.org/en/stable/classes/class_progressbar.html

**Contents:**
- ProgressBar
- Description
- Properties
- Theme Properties
- Enumerations
- Property Descriptions
- Theme Property Descriptions
- User-contributed notes

Inherits: Range < Control < CanvasItem < Node < Object

A control used for visual representation of a percentage.

A control used for visual representation of a percentage. Shows the fill percentage in the center. Can also be used to show indeterminate progress. For more fill modes, use TextureProgressBar instead.

editor_preview_indeterminate

Color(0.95, 0.95, 0.95, 1)

FillMode FILL_BEGIN_TO_END = 0

The progress bar fills from begin to end horizontally, according to the language direction. If Control.is_layout_rtl() returns false, it fills from left to right, and if it returns true, it fills from right to left.

FillMode FILL_END_TO_BEGIN = 1

The progress bar fills from end to begin horizontally, according to the language direction. If Control.is_layout_rtl() returns false, it fills from right to left, and if it returns true, it fills from left to right.

FillMode FILL_TOP_TO_BOTTOM = 2

The progress fills from top to bottom.

FillMode FILL_BOTTOM_TO_TOP = 3

The progress fills from bottom to top.

bool editor_preview_indeterminate 🔗

void set_editor_preview_indeterminate(value: bool)

bool is_editor_preview_indeterminate_enabled()

If false, the indeterminate animation will be paused in the editor.

void set_fill_mode(value: int)

The fill direction. See FillMode for possible values.

bool indeterminate = false 🔗

void set_indeterminate(value: bool)

bool is_indeterminate()

When set to true, the progress bar indicates that something is happening with an animation, but does not show the fill percentage or value.

bool show_percentage = true 🔗

void set_show_percentage(value: bool)

bool is_percentage_shown()

If true, the fill percentage is displayed on the bar.

Color font_color = Color(0.95, 0.95, 0.95, 1) 🔗

The color of the text.

Color font_outline_color = Color(0, 0, 0, 1) 🔗

The tint of text outline of the ProgressBar.

int outline_size = 0 🔗

The size of the text outline.

Note: If using a font with FontFile.multichannel_signed_distance_field enabled, its FontFile.msdf_pixel_range must be set to at least twice the value of outline_size for outline rendering to look correct. Otherwise, the outline may appear to be cut off earlier than intended.

Font used to draw the fill percentage if show_percentage is true.

Font size used to draw the fill percentage if show_percentage is true.

StyleBox background 🔗

The style of the background.

The style of the progress (i.e. the part that fills the bar).

Please read the User-contributed notes policy before submitting a comment.

---

## RenderDataRD

**URL:** https://docs.godotengine.org/en/stable/classes/class_renderdatard.html

**Contents:**
- RenderDataRD
- Description
- User-contributed notes

Inherits: RenderData < Object

Render data implementation for the RenderingDevice based renderers.

Note: This is an internal rendering server object, do not instantiate this from script.

This object manages all render data for the rendering device based renderers.

Note: This is an internal rendering server object only exposed for GDExtension plugins.

Please read the User-contributed notes policy before submitting a comment.

---

## Room scale in XR

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/xr_room_scale.html

**Contents:**
- Room scale in XR
- Origin centric solution
- Step 1
- Step 2
- Step 3
- Character body centric solution
- Step 1
- Step 2
- Step 3
- When the player walks to somewhere they shouldn't

One of the staples of XR projects is the ability to walk around freely in a large space. This space is often constrained by the room the player is physically in with tracking sensors placed within this space. With the advent of inside out tracking however ever larger play spaces are possible.

As a developer this introduces a number of interesting challenges. In this document we will look at a number of the challenges you may face and outline some solutions. We'll discuss the issues and challenges for seated XR games in another document.

Often developers sit behind their desk while building the foundation to their game. In this mode the issues with developing for room scale don't show themselves until it is too late. The advice here is to start testing while standing up and walking around as early as possible. Once you are happy your foundation is solid, you can develop in comfort while remaining seated.

In traditional first person games a player is represented by a CharacterBody3D node. This node is moved by processing traditional controller, mouse or keyboard input. A camera is attached to this node at a location roughly where the player's head will be.

Applying this model to the XR setup, we add an XROrigin3D node as a child of the character body, and add an XRCamera3D as a child of the origin node. At face value this seems to work. However, upon closer examination this model does not take into account that there are two forms of movement in XR. The movement through controller input, and the physical movement of the player in the real world.

As a result, the origin node does not represent the position of the player. It represents the center, or start of, the tracking space in which the player can physically move. As the player moves around their room this movement is represented through the tracking of the player's headset. In game this translates to the camera node's position being updated accordingly. For all intents and purposes, we are tracking a disembodied head. Unless body tracking is available, we have no knowledge of the position or orientation of the player's body.

The first problem this causes is fairly obvious. When the player moves with controller input, we can use the same approach in normal games and move the player in a forward direction. However the player isn't where we think they are and as we move forward we're checking collisions in the wrong location.

The second problem really shows itself when the player walks further away from the center of the tracking space and uses controller input to turn. If we rotate our character body, the player will be moved around the room in a circular fashion.

If we fix the above issues, we will find a third issue. When the path for the player is blocked in the virtual world, the player can still physically move forward.

We will look at solving the first two problem with two separate solutions, and then discuss dealing with the third.

Looking at the first approach for solving this we are going to change our structure. This is the approach currently implemented in XR Tools.

In this setup we mark the character body as top level so it does not move with the origin.

We also have a helper node that tells us where our neck joint is in relation to our camera. We use this to determine where our body center is.

Processing our character movement is now done in three steps.

The Origin centric movement demo contains a more elaborate example of the technique described below.

In the first step we're going to process the physical movement of the player. We determine where the player is right now, and attempt to move our character body there.

Note that we're returning true from our _process_on_physical_movement function when we couldn't move our player all the way.

The second step is to handle rotation of the player as a result of user input.

As the input used can differ based on your needs we are simply calling the function _get_rotational_input. This function should obtain the necessary input and return the rotational speed in radians per second.

For our example we are going to keep this simple and straight forward. We are not going to worry about comfort features such as snap turning and applying a vignette. We highly recommend implementing such comfort features.

We've added the call for processing our rotation to our physics process but we are only executing this if we were able to move our player fully. This means that if the player moves somewhere they shouldn't, we don't process further movement.

The third and final step is moving the player forwards, backwards or sideways as a result of user input.

Just like with the rotation the inputs differ from project to project so we are simply calling the function _get_movement_input. This function should obtain the necessary input and return a directional vector scaled to the required velocity.

Just like with rotation we're keeping it simple. Here too it is advisable to look at adding comfort settings.

In this setup we are going to keep our character body as our root node and as such is easier to combine with traditional game mechanics.

Here we have a standard character body with collision shape, and our XR origin node and camera as normal children. We also have our neck helper node.

Processing our character movement is done in the same three steps but implemented slightly differently.

The Character centric movement demo contains a more elaborate example of the technique described below.

In this approach step 1 is where all the magic happens. Just like with our previous approach we will be applying our physical movement to the character body, but we will counter that movement on the origin node.

This will ensure that the player's location stays in sync with the character body's location.

In essence the code above will move the character body to where the player is, and then move the origin node back in equal amounts. The result is that the player stays centered above the character body.

We start with applying the rotation. The character body should be facing where the player was looking the previous frame. We calculate our camera orientation in the space of the character body. We can now calculate the angle by which the player has rotated their head. We rotate our character body by the same amount so our character body faces the same direction as the player. And then we reverse the rotation on the origin node so the camera ends up aligned with the player again.

For the movement we do much the same. The character body should be where the player was standing the previous frame. We calculate by how much the player has moved from this location. Then we attempt to move the character body to this location.

As the player may hit a collision body and be stopped, we only move the origin point back by the amount we actually moved the character body. The player may thus move away from this location but that will be reflected in the positioning of the player.

As with our previous solution we return true if this is the case.

In this step we again apply the rotation based on controller input. However in this case the code is nearly identical to how one would implement this in a normal first person game.

As the input used can differ based on your needs we are simply calling the function _get_rotational_input. This function should obtain the necessary input and return the rotational speed in radians per second.

For step three we again apply the movement based on controller input. However just like at step 2, we can now implement this as we would in a normal first person game.

Just like with the rotation the inputs differ from project to project so we are simply calling the function _get_movement_input. This function should obtain the necessary input and return a directional vector scaled to the required velocity.

Think of a situation where the player is outside a locked room. You don't want the player to go into that room until the door is unlocked. You also don't want the player to see what is in this room.

The logic for moving the player through controller input nicely prevents this. The player encounters a static body, and the code prevents the player from moving into the room.

However with XR, nothing is preventing the player from taking a real step forward.

With both the approaches worked out up above we will prevent the character body from moving where the player can't go. As the player has physically moved to this location, the camera will now have moved into the room.

The logical solution would be to prevent the movement altogether and adjust the placement of the XR origin point so the player stays outside of the room.

The problem with this approach is that physical movement is now not replicated in the virtual space. This will cause nausea for the player.

What many XR games do instead, is to measure the distance between where the player physically is, and where the player's virtual body has been left behind. As this distance increases, usually to a distance of a few centimeters, the screen slowly blacks out.

Our solutions up above would allow us to add this logic into the code at the end of step 1.

Further improvements to the code presented could be:

allowing controller input as long as this distance is still small,

still applying gravity to the player even when controller input is disabled.

The movement demos in our demo repository contain an example of blacking out the screen when a user walks into restricted areas.

The above provides two good options as starting points for implementing room scale XR games.

A few more things that are worth pointing out that you will likely want to implement:

The height of the camera can be used to detect whether the player is standing up, crouching, jumping or lying down. You can adjust the size and orientation of the collision shape accordingly. Extra bonus points for adding multiple collision shapes so the head and body have their own, more accurately sized, shapes.

When a scene first loads, the player may be far away from the center of the tracking space. This could result in the player spawning into a different room than our origin point. The game will now attempt, and fail, to move the player body from the starting point to where the player is standing. You should implement a reset function that moves the origin point so the player is in the correct starting position.

Both of the above improvements require the player to be ready and standing up straight. There is no guarantee as the player may still be putting their headset on.

Many games, including XR Tools, solve this by introducing an intro screen or loading screen where the player must press a button when they are ready. This starting environment is often a large location where the positioning of the player has little impact on what the player sees. When the player is ready, and presses the button, this is the moment you record the position and height of the camera.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
func _process_on_physical_movement(delta):
  # Remember our current velocity, we'll apply that later
  var current_velocity = $CharacterBody3D.velocity

  # Remember where our player body currently is
  var org_player_body: Vector3 = $CharacterBody3D.global_transform.origin

  # Determine where our player body should be
  var player_body_location: Vector3 = $XRCamera3D.transform * $XRCamera3D/Neck.transform.origin
  player_body_location.y = 0.0
  player_body_location = global_transform * player_body_location

  # Attempt to move our character
  $CharacterBody3D.velocity = (player_body_location - org_player_body) / delta
  $CharacterBody3D.move_and_slide()

  # Set back to our current value
  $CharacterBody3D.velocity = current_velocity

  # Check if we managed to move all the way, ignoring height change
  var movement_left = player_body_location - $CharacterBody3D.global_transform.origin
  movement_left.y = 0.0
  if (movement_left).length() > 0.01:
    # We'll talk more about what we'll do here later on
    return true
  else:
    return false

func _physics_process(delta):
  var is_colliding = _process_on_physical_movement(delta)
```

Example 2 (swift):
```swift
func _get_rotational_input() -> float:
  # Implement this function to return rotation in radians per second.
  return 0.0

func _copy_player_rotation_to_character_body():
  # We only copy our forward direction to our character body, we ignore tilt
  var camera_forward: Vector3 = -$XRCamera3D.global_transform.basis.z
  var body_forward: Vector3 = Vector3(camera_forward.x, 0.0, camera_forward.z)

  $CharacterBody3D.global_transform.basis = Basis.looking_at(body_forward, Vector3.UP)

func _process_rotation_on_input(delta):
  var t1 := Transform3D()
  var t2 := Transform3D()
  var rot := Transform3D()

  # We are going to rotate the origin around the player
  var player_position = $CharacterBody3D.global_transform.origin - global_transform.origin

  t1.origin = -player_position
  t2.origin = player_position
  rot = rot.rotated(Vector3(0.0, 1.0, 0.0), _get_rotational_input() * delta)
  global_transform = (global_transform * t2 * rot * t1).orthonormalized()

  # Now ensure our player body is facing the correct way as well
  _copy_player_rotation_to_character_body()

func _physics_process(delta):
  var is_colliding = _process_on_physical_movement(delta)
  if !is_colliding:
    _process_rotation_on_input(delta)
```

Example 3 (swift):
```swift
var gravity = ProjectSettings.get_setting("physics/3d/default_gravity")

func _get_movement_input() -> Vector2:
  # Implement this to return requested directional movement in meters per second.
  return Vector2()

func _process_movement_on_input(delta):
  # Remember where our player body currently is
  var org_player_body: Vector3 = $CharacterBody3D.global_transform.origin

  # We start with applying gravity
  $CharacterBody3D.velocity.y -= gravity * delta

  # Now we add in our movement
  var input: Vector2 = _get_movement_input()
  var movement: Vector3 = ($CharacterBody3D.global_transform.basis * Vector3(input.x, 0, input.y))
  $CharacterBody3D.velocity.x = movement.x
  $CharacterBody3D.velocity.z = movement.z

  # Attempt to move our player
  $CharacterBody3D.move_and_slide()

  # And now apply the actual movement to our origin
  global_transform.origin += $CharacterBody3D.global_transform.origin - org_player_body

func _physics_process(delta):
  var is_colliding = _process_on_physical_movement(delta)
  if !is_colliding:
    _process_rotation_on_input(delta)
    _process_movement_on_input(delta)
```

Example 4 (swift):
```swift
# Helper variables to keep our code readable
@onready var origin_node = $XROrigin3D
@onready var camera_node = $XROrigin3D/XRCamera3D
@onready var neck_position_node = $XROrigin3D/XRCamera3D/Neck

func _process_on_physical_movement(delta) -> bool:
  # Remember our current velocity, we'll apply that later
  var current_velocity = velocity

  # Start by rotating the player to face the same way our real player is
  var camera_basis: Basis = origin_node.transform.basis * camera_node.transform.basis
  var forward: Vector2 = Vector2(camera_basis.z.x, camera_basis.z.z)
  var angle: float = forward.angle_to(Vector2(0.0, 1.0))

  # Rotate our character body
  transform.basis = transform.basis.rotated(Vector3.UP, angle)

  # Reverse this rotation our origin node
  origin_node.transform = Transform3D().rotated(Vector3.UP, -angle) * origin_node.transform

  # Now apply movement, first move our player body to the right location
  var org_player_body: Vector3 = global_transform.origin
  var player_body_location: Vector3 = origin_node.transform * camera_node.transform * neck_position_node.transform.origin
  player_body_location.y = 0.0
  player_body_location = global_transform * player_body_location

  velocity = (player_body_location - org_player_body) / delta
  move_and_slide()

  # Now move our XROrigin back
  var delta_movement = global_transform.origin - org_player_body
  origin_node.global_transform.origin -= delta_movement

  # Return our value
  velocity = current_velocity

  if (player_body_location - global_transform.origin).length() > 0.01:
    # We'll talk more about what we'll do here later on
    return true
  else:
    return false

func _physics_process(delta):
  var is_colliding = _process_on_physical_movement(delta)
```

---

## ScrollBar

**URL:** https://docs.godotengine.org/en/stable/classes/class_scrollbar.html

**Contents:**
- ScrollBar
- Description
- Properties
- Theme Properties
- Signals
- Property Descriptions
- Theme Property Descriptions
- User-contributed notes

Inherits: Range < Control < CanvasItem < Node < Object

Inherited By: HScrollBar, VScrollBar

Abstract base class for scrollbars.

Abstract base class for scrollbars, typically used to navigate through content that extends beyond the visible area of a control. Scrollbars are Range-based controls.

3 (overrides Control)

0.0 (overrides Range)

Emitted when the scrollbar is being scrolled.

float custom_step = -1.0 🔗

void set_custom_step(value: float)

float get_custom_step()

Overrides the step used when clicking increment and decrement buttons or when using arrow keys when the ScrollBar is focused.

Texture2D decrement 🔗

Icon used as a button to scroll the ScrollBar left/up. Supports custom step using the custom_step property.

Texture2D decrement_highlight 🔗

Displayed when the mouse cursor hovers over the decrement button.

Texture2D decrement_pressed 🔗

Displayed when the decrement button is being pressed.

Texture2D increment 🔗

Icon used as a button to scroll the ScrollBar right/down. Supports custom step using the custom_step property.

Texture2D increment_highlight 🔗

Displayed when the mouse cursor hovers over the increment button.

Texture2D increment_pressed 🔗

Displayed when the increment button is being pressed.

Used as texture for the grabber, the draggable element representing current scroll.

StyleBox grabber_highlight 🔗

Used when the mouse hovers over the grabber.

StyleBox grabber_pressed 🔗

Used when the grabber is being dragged.

Used as background of this ScrollBar.

StyleBox scroll_focus 🔗

Used as background when the ScrollBar has the GUI focus.

Please read the User-contributed notes policy before submitting a comment.

---

## Setting up XR

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/setting_up_xr.html

**Contents:**
- Setting up XR
- Introduction to the XR system in Godot
- Which Renderer to use
- OpenXR
- Setting up the XR scene
- User-contributed notes

Godot provides a modular XR system that abstracts many of the different XR platform specifics away from the user. At the core sits the XRServer which acts as a central interface to the XR system that allows users to discover interfaces and interact with the components of the XR system.

Each supported XR platform is implemented as an XRInterface. A list of supported platforms can be found on the list of features page here. Supported interfaces register themselves with the XRServer and can be queried with the find_interface method on the XRServer. When the desired interface is found it can be initialized by calling initialize on the interface.

A registered interface means nothing more than that the interface is available, if the interface is not supported by the host system, initialization may fail and return false. This can have many reasons and sadly the reasons differ from platform to platform. It can be because the user hasn't installed the required software, or that the user simply hasn't plugged in their headset. You as a developer must thus react properly on an interface failing to initialize.

Due to the special requirements for output in XR, especially for head mounted devices that supply different images to each eye, the XRServer in Godot will override various features in the rendering system. For stand-alone devices this means the final output is handled by the XRInterface and Godot's usual output system is disabled. For desktop XR devices that work as a second screen it is possible to dedicate a separate Viewport to handle the XR output, leaving the main Godot window available for displaying alternative content.

Note that only one interface can be responsible for handling the output to an XR device, this is known as the primary interface and by default will be the first interface that is initialized. Godot currently thus only supports implementations with a single headset. It is possible, but increasingly uncommon, to have a secondary interface, for example to add tracking to an otherwise 3DOF only device.

There are three XR specific node types that you will find in nearly all XR applications:

XROrigin3D represents, for all intents and purposes, the center point of your play space. That is an oversimplified statement but we'll go into more detail later. All objects tracked in physical space by the XR platform are positioned in relation to this point.

XRCamera3D represents the (stereo) camera that is used when rendering output for the XR device. The positioning of this node is controlled by the XR system and updated automatically using the tracking information provided by the XR platform.

XRController3D represents a controller used by the player, commonly there are two, one held in each hand. These nodes give access to various states on these controllers and send out signals when the player presses buttons on them. The positioning of this node is controlled by the XR system and updated automatically using the tracking information provided by the XR platform.

There are other XR related nodes and there is much more to say about these three nodes, but we'll get into that later on.

Godot has 3 renderer options for projects: Compatibility, Mobile, and Forward+. The current recommendation is to use the Mobile renderer for any desktop VR project, and use the Compatibility renderer for any project running on a standalone headset like the Meta Quest 3. XR projects will run with the Forward+ renderer, but it isn't well optimized for XR right now compared to the other two.

OpenXR is a new industry standard that allows different XR platforms to present themselves through a standardised API to XR applications. This standard is an open standard maintained by the Khronos Group and thus aligns very well with Godot's interests.

The Vulkan implementation of OpenXR is closely integrated with Vulkan, taking over part of the Vulkan system. This requires tight integration of certain core graphics features in the Vulkan renderer which are needed before the XR system is setup. This was one of the main deciding factors to include OpenXR as a core interface.

This also means OpenXR needs to be enabled when Godot starts in order to set things up correctly. Check the Enabled setting in your project settings under XR > OpenXR.

You can find several other settings related to OpenXR here as well. These can't be changed while your application is running. The default settings will get us started, but for more information on what's here see OpenXR Settings.

You'll also need to go to XR > Shaders in the project settings and check the Enabled box to enable them. Once you've done that click the Save & Restart button.

Many post process effects have not yet been updated to support stereoscopic rendering. Using these will have adverse effects.

Every XR application needs at least an XROrigin3D and an XRCamera3D node. Most will have two XRController3D, one for the left hand and one for the right. Keep in mind that the camera and controller nodes should be children of the origin node. Add these nodes to a new scene and rename the controller nodes to LeftHand and RightHand, your scene should look something like this:

The warning icons are expected and should go away after you configure the controllers. Select the left hand and set it up as follows:

Right now all these nodes are on the floor, they will be positioned correctly in runtime. To help during development, it can be helpful to move the camera upwards so its y is set to 1.7, and move the controller nodes to -0.5, 1.0, -0.5 and 0.5, 1.0, -0.5 for respectively the left and right hand.

Next we need to add a script to our root node. Add the following code into this script:

This code fragment assumes we are using OpenXR, if you wish to use any of the other interfaces you can change the find_interface call.

As you can see in the code snippet above, we turn off v-sync. When using OpenXR you are outputting the rendering results to an HMD that often requires us to run at 90Hz or higher. If your monitor is a 60hz monitor and v-sync is turned on, you will limit the output to 60 frames per second.

XR interfaces like OpenXR perform their own sync.

Also note that by default the physics engine runs at 60Hz as well and this can result in choppy physics. You should set Engine.physics_ticks_per_second to a higher value.

If you run your project at this point in time, everything will work but you will be in a dark world. So to finish off our starting point add a DirectionalLight3D and a WorldEnvironment node to your scene. You may wish to also add a mesh instance as a child to each controller node just to temporarily visualise them. Make sure you configure a sky in your world environment.

Now run your project, you should be floating somewhere in space and be able to look around.

While traditional level switching can definitely be used with XR applications, where this scene setup is repeated in each level, most find it easier to set this up once and loading levels as a subscene. If you do switch scenes and replicate the XR setup in each one, do make sure you do not run initialize multiple times. The effect can be unpredictable depending on the XR interface used.

For the rest of this basic tutorial series we will create a game that uses a single scene.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Node3D

var xr_interface: XRInterface

func _ready():
    xr_interface = XRServer.find_interface("OpenXR")
    if xr_interface and xr_interface.is_initialized():
        print("OpenXR initialized successfully")

        # Turn off v-sync!
        DisplayServer.window_set_vsync_mode(DisplayServer.VSYNC_DISABLED)

        # Change our main viewport to output to the HMD
        get_viewport().use_xr = true
    else:
        print("OpenXR not initialized, please check if your headset is connected")
```

Example 2 (swift):
```swift
using Godot;

public partial class MyNode3D : Node3D
{
    private XRInterface _xrInterface;

    public override void _Ready()
    {
        _xrInterface = XRServer.FindInterface("OpenXR");
        if(_xrInterface != null && _xrInterface.IsInitialized())
        {
            GD.Print("OpenXR initialized successfully");

            // Turn off v-sync!
            DisplayServer.WindowSetVsyncMode(DisplayServer.VSyncMode.Disabled);

            // Change our main viewport to output to the HMD
            GetViewport().UseXR = true;
        }
        else
        {
            GD.Print("OpenXR not initialized, please check if your headset is connected");
        }
    }
}
```

---

## TextParagraph

**URL:** https://docs.godotengine.org/en/stable/classes/class_textparagraph.html

**Contents:**
- TextParagraph
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Holds a paragraph of text.

Abstraction over TextServer for handling a single paragraph of text.

BitField[LineBreakFlag]

BitField[JustificationFlag]

text_overrun_behavior

add_object(key: Variant, size: Vector2, inline_align: InlineAlignment = 5, length: int = 1, baseline: float = 0.0)

add_string(text: String, font: Font, font_size: int, language: String = "", meta: Variant = null)

draw(canvas: RID, pos: Vector2, color: Color = Color(1, 1, 1, 1), dc_color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const

draw_dropcap(canvas: RID, pos: Vector2, color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const

draw_dropcap_outline(canvas: RID, pos: Vector2, outline_size: int = 1, color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const

draw_line(canvas: RID, pos: Vector2, line: int, color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const

draw_line_outline(canvas: RID, pos: Vector2, line: int, outline_size: int = 1, color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const

draw_outline(canvas: RID, pos: Vector2, outline_size: int = 1, color: Color = Color(1, 1, 1, 1), dc_color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const

get_dropcap_lines() const

get_dropcap_rid() const

get_dropcap_size() const

get_inferred_direction() const

get_line_ascent(line: int) const

get_line_count() const

get_line_descent(line: int) const

get_line_object_rect(line: int, key: Variant) const

get_line_objects(line: int) const

get_line_range(line: int) const

get_line_rid(line: int) const

get_line_size(line: int) const

get_line_underline_position(line: int) const

get_line_underline_thickness(line: int) const

get_line_width(line: int) const

get_non_wrapped_size() const

hit_test(coords: Vector2) const

resize_object(key: Variant, size: Vector2, inline_align: InlineAlignment = 5, baseline: float = 0.0)

set_bidi_override(override: Array)

set_dropcap(text: String, font: Font, font_size: int, dropcap_margins: Rect2 = Rect2(0, 0, 0, 0), language: String = "")

tab_align(tab_stops: PackedFloat32Array)

HorizontalAlignment alignment = 0 🔗

void set_alignment(value: HorizontalAlignment)

HorizontalAlignment get_alignment()

Paragraph horizontal alignment.

BitField[LineBreakFlag] break_flags = 3 🔗

void set_break_flags(value: BitField[LineBreakFlag])

BitField[LineBreakFlag] get_break_flags()

Line breaking rules. For more info see TextServer.

String custom_punctuation = "" 🔗

void set_custom_punctuation(value: String)

String get_custom_punctuation()

Custom punctuation character list, used for word breaking. If set to empty string, server defaults are used.

Direction direction = 0 🔗

void set_direction(value: Direction)

Direction get_direction()

Text writing direction.

String ellipsis_char = "…" 🔗

void set_ellipsis_char(value: String)

String get_ellipsis_char()

Ellipsis character used for text clipping.

BitField[JustificationFlag] justification_flags = 163 🔗

void set_justification_flags(value: BitField[JustificationFlag])

BitField[JustificationFlag] get_justification_flags()

Line fill alignment rules.

float line_spacing = 0.0 🔗

void set_line_spacing(value: float)

float get_line_spacing()

Additional vertical spacing between lines (in pixels), spacing is added to line descent. This value can be negative.

int max_lines_visible = -1 🔗

void set_max_lines_visible(value: int)

int get_max_lines_visible()

Limits the lines of text shown.

Orientation orientation = 0 🔗

void set_orientation(value: Orientation)

Orientation get_orientation()

bool preserve_control = false 🔗

void set_preserve_control(value: bool)

bool get_preserve_control()

If set to true text will display control characters.

bool preserve_invalid = true 🔗

void set_preserve_invalid(value: bool)

bool get_preserve_invalid()

If set to true text will display invalid characters.

OverrunBehavior text_overrun_behavior = 0 🔗

void set_text_overrun_behavior(value: OverrunBehavior)

OverrunBehavior get_text_overrun_behavior()

The clipping behavior when the text exceeds the paragraph's set width.

void set_width(value: float)

bool add_object(key: Variant, size: Vector2, inline_align: InlineAlignment = 5, length: int = 1, baseline: float = 0.0) 🔗

Adds inline object to the text buffer, key must be unique. In the text, object is represented as length object replacement characters.

bool add_string(text: String, font: Font, font_size: int, language: String = "", meta: Variant = null) 🔗

Adds text span and font to draw it.

Clears text paragraph (removes text and inline objects).

void clear_dropcap() 🔗

void draw(canvas: RID, pos: Vector2, color: Color = Color(1, 1, 1, 1), dc_color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const 🔗

Draw all lines of the text and drop cap into a canvas item at a given position, with color. pos specifies the top left corner of the bounding box. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used.

void draw_dropcap(canvas: RID, pos: Vector2, color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const 🔗

Draw drop cap into a canvas item at a given position, with color. pos specifies the top left corner of the bounding box. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used.

void draw_dropcap_outline(canvas: RID, pos: Vector2, outline_size: int = 1, color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const 🔗

Draw drop cap outline into a canvas item at a given position, with color. pos specifies the top left corner of the bounding box. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used.

void draw_line(canvas: RID, pos: Vector2, line: int, color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const 🔗

Draw single line of text into a canvas item at a given position, with color. pos specifies the top left corner of the bounding box. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used.

void draw_line_outline(canvas: RID, pos: Vector2, line: int, outline_size: int = 1, color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const 🔗

Draw outline of the single line of text into a canvas item at a given position, with color. pos specifies the top left corner of the bounding box. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used.

void draw_outline(canvas: RID, pos: Vector2, outline_size: int = 1, color: Color = Color(1, 1, 1, 1), dc_color: Color = Color(1, 1, 1, 1), oversampling: float = 0.0) const 🔗

Draw outlines of all lines of the text and drop cap into a canvas item at a given position, with color. pos specifies the top left corner of the bounding box. If oversampling is greater than zero, it is used as font oversampling factor, otherwise viewport oversampling settings are used.

int get_dropcap_lines() const 🔗

Returns number of lines used by dropcap.

RID get_dropcap_rid() const 🔗

Returns drop cap text buffer RID.

Vector2 get_dropcap_size() const 🔗

Returns drop cap bounding box size.

Direction get_inferred_direction() const 🔗

Returns the text writing direction inferred by the BiDi algorithm.

float get_line_ascent(line: int) const 🔗

Returns the text line ascent (number of pixels above the baseline for horizontal layout or to the left of baseline for vertical).

int get_line_count() const 🔗

Returns number of lines in the paragraph.

float get_line_descent(line: int) const 🔗

Returns the text line descent (number of pixels below the baseline for horizontal layout or to the right of baseline for vertical).

Rect2 get_line_object_rect(line: int, key: Variant) const 🔗

Returns bounding rectangle of the inline object.

Array get_line_objects(line: int) const 🔗

Returns array of inline objects in the line.

Vector2i get_line_range(line: int) const 🔗

Returns character range of the line.

RID get_line_rid(line: int) const 🔗

Returns TextServer line buffer RID.

Vector2 get_line_size(line: int) const 🔗

Returns size of the bounding box of the line of text. Returned size is rounded up.

float get_line_underline_position(line: int) const 🔗

Returns pixel offset of the underline below the baseline.

float get_line_underline_thickness(line: int) const 🔗

Returns thickness of the underline.

float get_line_width(line: int) const 🔗

Returns width (for horizontal layout) or height (for vertical) of the line of text.

Vector2 get_non_wrapped_size() const 🔗

Returns the size of the bounding box of the paragraph, without line breaks.

Vector2i get_range() const 🔗

Returns the character range of the paragraph.

RID get_rid() const 🔗

Returns TextServer full string buffer RID.

Vector2 get_size() const 🔗

Returns the size of the bounding box of the paragraph.

int hit_test(coords: Vector2) const 🔗

Returns caret character offset at the specified coordinates. This function always returns a valid position.

bool resize_object(key: Variant, size: Vector2, inline_align: InlineAlignment = 5, baseline: float = 0.0) 🔗

Sets new size and alignment of embedded object.

void set_bidi_override(override: Array) 🔗

Overrides BiDi for the structured text.

Override ranges should cover full source text without overlaps. BiDi algorithm will be used on each range separately.

bool set_dropcap(text: String, font: Font, font_size: int, dropcap_margins: Rect2 = Rect2(0, 0, 0, 0), language: String = "") 🔗

Sets drop cap, overrides previously set drop cap. Drop cap (dropped capital) is a decorative element at the beginning of a paragraph that is larger than the rest of the text.

void tab_align(tab_stops: PackedFloat32Array) 🔗

Aligns paragraph to the given tab-stops.

Please read the User-contributed notes policy before submitting a comment.

---

## VScrollBar

**URL:** https://docs.godotengine.org/en/stable/classes/class_vscrollbar.html

**Contents:**
- VScrollBar
- Description
- Properties
- User-contributed notes

Inherits: ScrollBar < Range < Control < CanvasItem < Node < Object

A vertical scrollbar that goes from top (min) to bottom (max).

A vertical scrollbar, typically used to navigate through content that extends beyond the visible height of a control. It is a Range-based control and goes from top (min) to bottom (max). Note that this direction is the opposite of VSlider's.

size_flags_horizontal

0 (overrides Control)

1 (overrides Control)

Please read the User-contributed notes policy before submitting a comment.

---

## Where to go from here

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/xr_next_steps.html

**Contents:**
- Where to go from here
- XR Toolkits
- User-contributed notes

Now that we have the basics covered there are several options to look at for your XR game dev journey:

You can take a look at the Advanced topics section.

You can look at a number of XR demos here.

You can find 3rd party tutorials on our Tutorials and resources page.

There are various XR toolkits available that implement more complex XR logic ready for you to use. We have a small introduction to Godot XR Tools that you can look at, a toolkit developed by core contributors of Godot.

There are more toolkits available for Godot:

Godot XR handtracking toolkit (GDScript)

Godot XR Kit (GDScript)

Godot XR Tools (GDScript)

Please read the User-contributed notes policy before submitting a comment.

---

## XMLParser

**URL:** https://docs.godotengine.org/en/stable/classes/class_xmlparser.html

**Contents:**
- XMLParser
- Description
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Provides a low-level interface for creating parsers for XML files.

Provides a low-level interface for creating parsers for XML files. This class can serve as base to make custom XML parsers.

To parse XML, you must open a file with the open() method or a buffer with the open_buffer() method. Then, the read() method must be called to parse the next nodes. Most of the methods take into consideration the currently parsed node.

Here is an example of using XMLParser to parse an SVG file (which is based on XML), printing each element and its attributes as a dictionary:

get_attribute_count() const

get_attribute_name(idx: int) const

get_attribute_value(idx: int) const

get_current_line() const

get_named_attribute_value(name: String) const

get_named_attribute_value_safe(name: String) const

get_node_data() const

get_node_name() const

get_node_offset() const

has_attribute(name: String) const

open_buffer(buffer: PackedByteArray)

NodeType NODE_NONE = 0

There's no node (no file or buffer opened).

NodeType NODE_ELEMENT = 1

An element node type, also known as a tag, e.g. <title>.

NodeType NODE_ELEMENT_END = 2

An end of element node type, e.g. </title>.

NodeType NODE_TEXT = 3

A text node type, i.e. text that is not inside an element. This includes whitespace.

NodeType NODE_COMMENT = 4

A comment node type, e.g. <!--A comment-->.

NodeType NODE_CDATA = 5

A node type for CDATA (Character Data) sections, e.g. <![CDATA[CDATA section]]>.

NodeType NODE_UNKNOWN = 6

An unknown node type.

int get_attribute_count() const 🔗

Returns the number of attributes in the currently parsed element.

Note: If this method is used while the currently parsed node is not NODE_ELEMENT or NODE_ELEMENT_END, this count will not be updated and will still reflect the last element.

String get_attribute_name(idx: int) const 🔗

Returns the name of an attribute of the currently parsed element, specified by the idx index.

String get_attribute_value(idx: int) const 🔗

Returns the value of an attribute of the currently parsed element, specified by the idx index.

int get_current_line() const 🔗

Returns the current line in the parsed file, counting from 0.

String get_named_attribute_value(name: String) const 🔗

Returns the value of an attribute of the currently parsed element, specified by its name. This method will raise an error if the element has no such attribute.

String get_named_attribute_value_safe(name: String) const 🔗

Returns the value of an attribute of the currently parsed element, specified by its name. This method will return an empty string if the element has no such attribute.

String get_node_data() const 🔗

Returns the contents of a text node. This method will raise an error if the current parsed node is of any other type.

String get_node_name() const 🔗

Returns the name of a node. This method will raise an error if the currently parsed node is a text node.

Note: The content of a NODE_CDATA node and the comment string of a NODE_COMMENT node are also considered names.

int get_node_offset() const 🔗

Returns the byte offset of the currently parsed node since the beginning of the file or buffer. This is usually equivalent to the number of characters before the read position.

NodeType get_node_type() 🔗

Returns the type of the current node. Compare with NodeType constants.

bool has_attribute(name: String) const 🔗

Returns true if the currently parsed element has an attribute with the name.

bool is_empty() const 🔗

Returns true if the currently parsed element is empty, e.g. <element />.

Error open(file: String) 🔗

Opens an XML file for parsing. This method returns an error code.

Error open_buffer(buffer: PackedByteArray) 🔗

Opens an XML raw buffer for parsing. This method returns an error code.

Parses the next node in the file. This method returns an error code.

Error seek(position: int) 🔗

Moves the buffer cursor to a certain offset (since the beginning) and reads the next node there. This method returns an error code.

void skip_section() 🔗

Skips the current section. If the currently parsed node contains more inner nodes, they will be ignored and the cursor will go to the closing of the current element.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var parser = XMLParser.new()
parser.open("path/to/file.svg")
while parser.read() != ERR_FILE_EOF:
    if parser.get_node_type() == XMLParser.NODE_ELEMENT:
        var node_name = parser.get_node_name()
        var attributes_dict = {}
        for idx in range(parser.get_attribute_count()):
            attributes_dict[parser.get_attribute_name(idx)] = parser.get_attribute_value(idx)
        print("The ", node_name, " element has the following attributes: ", attributes_dict)
```

Example 2 (json):
```json
var parser = new XmlParser();
parser.Open("path/to/file.svg");
while (parser.Read() != Error.FileEof)
{
    if (parser.GetNodeType() == XmlParser.NodeType.Element)
    {
        var nodeName = parser.GetNodeName();
        var attributesDict = new Godot.Collections.Dictionary();
        for (int idx = 0; idx < parser.GetAttributeCount(); idx++)
        {
            attributesDict[parser.GetAttributeName(idx)] = parser.GetAttributeValue(idx);
        }
        GD.Print($"The {nodeName} element has the following attributes: {attributesDict}");
    }
}
```

---

## XRFaceTracker

**URL:** https://docs.godotengine.org/en/stable/classes/class_xrfacetracker.html

**Contents:**
- XRFaceTracker
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: XRTracker < RefCounted < Object

An instance of this object represents a tracked face and its corresponding blend shapes. The blend shapes come from the Unified Expressions standard, and contain extended details and visuals for each blend shape. Additionally the Tracking Standard Comparison page documents the relationship between Unified Expressions and other standards.

As face trackers are turned on they are registered with the XRServer.

XR documentation index

64 (overrides XRTracker)

get_blend_shape(blend_shape: BlendShapeEntry) const

set_blend_shape(blend_shape: BlendShapeEntry, weight: float)

enum BlendShapeEntry: 🔗

BlendShapeEntry FT_EYE_LOOK_OUT_RIGHT = 0

Right eye looks outwards.

BlendShapeEntry FT_EYE_LOOK_IN_RIGHT = 1

Right eye looks inwards.

BlendShapeEntry FT_EYE_LOOK_UP_RIGHT = 2

Right eye looks upwards.

BlendShapeEntry FT_EYE_LOOK_DOWN_RIGHT = 3

Right eye looks downwards.

BlendShapeEntry FT_EYE_LOOK_OUT_LEFT = 4

Left eye looks outwards.

BlendShapeEntry FT_EYE_LOOK_IN_LEFT = 5

Left eye looks inwards.

BlendShapeEntry FT_EYE_LOOK_UP_LEFT = 6

Left eye looks upwards.

BlendShapeEntry FT_EYE_LOOK_DOWN_LEFT = 7

Left eye looks downwards.

BlendShapeEntry FT_EYE_CLOSED_RIGHT = 8

Closes the right eyelid.

BlendShapeEntry FT_EYE_CLOSED_LEFT = 9

Closes the left eyelid.

BlendShapeEntry FT_EYE_SQUINT_RIGHT = 10

Squeezes the right eye socket muscles.

BlendShapeEntry FT_EYE_SQUINT_LEFT = 11

Squeezes the left eye socket muscles.

BlendShapeEntry FT_EYE_WIDE_RIGHT = 12

Right eyelid widens beyond relaxed.

BlendShapeEntry FT_EYE_WIDE_LEFT = 13

Left eyelid widens beyond relaxed.

BlendShapeEntry FT_EYE_DILATION_RIGHT = 14

Dilates the right eye pupil.

BlendShapeEntry FT_EYE_DILATION_LEFT = 15

Dilates the left eye pupil.

BlendShapeEntry FT_EYE_CONSTRICT_RIGHT = 16

Constricts the right eye pupil.

BlendShapeEntry FT_EYE_CONSTRICT_LEFT = 17

Constricts the left eye pupil.

BlendShapeEntry FT_BROW_PINCH_RIGHT = 18

Right eyebrow pinches in.

BlendShapeEntry FT_BROW_PINCH_LEFT = 19

Left eyebrow pinches in.

BlendShapeEntry FT_BROW_LOWERER_RIGHT = 20

Outer right eyebrow pulls down.

BlendShapeEntry FT_BROW_LOWERER_LEFT = 21

Outer left eyebrow pulls down.

BlendShapeEntry FT_BROW_INNER_UP_RIGHT = 22

Inner right eyebrow pulls up.

BlendShapeEntry FT_BROW_INNER_UP_LEFT = 23

Inner left eyebrow pulls up.

BlendShapeEntry FT_BROW_OUTER_UP_RIGHT = 24

Outer right eyebrow pulls up.

BlendShapeEntry FT_BROW_OUTER_UP_LEFT = 25

Outer left eyebrow pulls up.

BlendShapeEntry FT_NOSE_SNEER_RIGHT = 26

Right side face sneers.

BlendShapeEntry FT_NOSE_SNEER_LEFT = 27

Left side face sneers.

BlendShapeEntry FT_NASAL_DILATION_RIGHT = 28

Right side nose canal dilates.

BlendShapeEntry FT_NASAL_DILATION_LEFT = 29

Left side nose canal dilates.

BlendShapeEntry FT_NASAL_CONSTRICT_RIGHT = 30

Right side nose canal constricts.

BlendShapeEntry FT_NASAL_CONSTRICT_LEFT = 31

Left side nose canal constricts.

BlendShapeEntry FT_CHEEK_SQUINT_RIGHT = 32

Raises the right side cheek.

BlendShapeEntry FT_CHEEK_SQUINT_LEFT = 33

Raises the left side cheek.

BlendShapeEntry FT_CHEEK_PUFF_RIGHT = 34

Puffs the right side cheek.

BlendShapeEntry FT_CHEEK_PUFF_LEFT = 35

Puffs the left side cheek.

BlendShapeEntry FT_CHEEK_SUCK_RIGHT = 36

Sucks in the right side cheek.

BlendShapeEntry FT_CHEEK_SUCK_LEFT = 37

Sucks in the left side cheek.

BlendShapeEntry FT_JAW_OPEN = 38

BlendShapeEntry FT_MOUTH_CLOSED = 39

BlendShapeEntry FT_JAW_RIGHT = 40

Pushes jawbone right.

BlendShapeEntry FT_JAW_LEFT = 41

BlendShapeEntry FT_JAW_FORWARD = 42

Pushes jawbone forward.

BlendShapeEntry FT_JAW_BACKWARD = 43

Pushes jawbone backward.

BlendShapeEntry FT_JAW_CLENCH = 44

BlendShapeEntry FT_JAW_MANDIBLE_RAISE = 45

BlendShapeEntry FT_LIP_SUCK_UPPER_RIGHT = 46

Upper right lip part tucks in the mouth.

BlendShapeEntry FT_LIP_SUCK_UPPER_LEFT = 47

Upper left lip part tucks in the mouth.

BlendShapeEntry FT_LIP_SUCK_LOWER_RIGHT = 48

Lower right lip part tucks in the mouth.

BlendShapeEntry FT_LIP_SUCK_LOWER_LEFT = 49

Lower left lip part tucks in the mouth.

BlendShapeEntry FT_LIP_SUCK_CORNER_RIGHT = 50

Right lip corner folds into the mouth.

BlendShapeEntry FT_LIP_SUCK_CORNER_LEFT = 51

Left lip corner folds into the mouth.

BlendShapeEntry FT_LIP_FUNNEL_UPPER_RIGHT = 52

Upper right lip part pushes into a funnel.

BlendShapeEntry FT_LIP_FUNNEL_UPPER_LEFT = 53

Upper left lip part pushes into a funnel.

BlendShapeEntry FT_LIP_FUNNEL_LOWER_RIGHT = 54

Lower right lip part pushes into a funnel.

BlendShapeEntry FT_LIP_FUNNEL_LOWER_LEFT = 55

Lower left lip part pushes into a funnel.

BlendShapeEntry FT_LIP_PUCKER_UPPER_RIGHT = 56

Upper right lip part pushes outwards.

BlendShapeEntry FT_LIP_PUCKER_UPPER_LEFT = 57

Upper left lip part pushes outwards.

BlendShapeEntry FT_LIP_PUCKER_LOWER_RIGHT = 58

Lower right lip part pushes outwards.

BlendShapeEntry FT_LIP_PUCKER_LOWER_LEFT = 59

Lower left lip part pushes outwards.

BlendShapeEntry FT_MOUTH_UPPER_UP_RIGHT = 60

Upper right part of the lip pulls up.

BlendShapeEntry FT_MOUTH_UPPER_UP_LEFT = 61

Upper left part of the lip pulls up.

BlendShapeEntry FT_MOUTH_LOWER_DOWN_RIGHT = 62

Lower right part of the lip pulls up.

BlendShapeEntry FT_MOUTH_LOWER_DOWN_LEFT = 63

Lower left part of the lip pulls up.

BlendShapeEntry FT_MOUTH_UPPER_DEEPEN_RIGHT = 64

Upper right lip part pushes in the cheek.

BlendShapeEntry FT_MOUTH_UPPER_DEEPEN_LEFT = 65

Upper left lip part pushes in the cheek.

BlendShapeEntry FT_MOUTH_UPPER_RIGHT = 66

Moves upper lip right.

BlendShapeEntry FT_MOUTH_UPPER_LEFT = 67

Moves upper lip left.

BlendShapeEntry FT_MOUTH_LOWER_RIGHT = 68

Moves lower lip right.

BlendShapeEntry FT_MOUTH_LOWER_LEFT = 69

Moves lower lip left.

BlendShapeEntry FT_MOUTH_CORNER_PULL_RIGHT = 70

Right lip corner pulls diagonally up and out.

BlendShapeEntry FT_MOUTH_CORNER_PULL_LEFT = 71

Left lip corner pulls diagonally up and out.

BlendShapeEntry FT_MOUTH_CORNER_SLANT_RIGHT = 72

Right corner lip slants up.

BlendShapeEntry FT_MOUTH_CORNER_SLANT_LEFT = 73

Left corner lip slants up.

BlendShapeEntry FT_MOUTH_FROWN_RIGHT = 74

Right corner lip pulls down.

BlendShapeEntry FT_MOUTH_FROWN_LEFT = 75

Left corner lip pulls down.

BlendShapeEntry FT_MOUTH_STRETCH_RIGHT = 76

Mouth corner lip pulls out and down.

BlendShapeEntry FT_MOUTH_STRETCH_LEFT = 77

Mouth corner lip pulls out and down.

BlendShapeEntry FT_MOUTH_DIMPLE_RIGHT = 78

Right lip corner is pushed backwards.

BlendShapeEntry FT_MOUTH_DIMPLE_LEFT = 79

Left lip corner is pushed backwards.

BlendShapeEntry FT_MOUTH_RAISER_UPPER = 80

Raises and slightly pushes out the upper mouth.

BlendShapeEntry FT_MOUTH_RAISER_LOWER = 81

Raises and slightly pushes out the lower mouth.

BlendShapeEntry FT_MOUTH_PRESS_RIGHT = 82

Right side lips press and flatten together vertically.

BlendShapeEntry FT_MOUTH_PRESS_LEFT = 83

Left side lips press and flatten together vertically.

BlendShapeEntry FT_MOUTH_TIGHTENER_RIGHT = 84

Right side lips squeeze together horizontally.

BlendShapeEntry FT_MOUTH_TIGHTENER_LEFT = 85

Left side lips squeeze together horizontally.

BlendShapeEntry FT_TONGUE_OUT = 86

Tongue visibly sticks out of the mouth.

BlendShapeEntry FT_TONGUE_UP = 87

Tongue points upwards.

BlendShapeEntry FT_TONGUE_DOWN = 88

Tongue points downwards.

BlendShapeEntry FT_TONGUE_RIGHT = 89

BlendShapeEntry FT_TONGUE_LEFT = 90

BlendShapeEntry FT_TONGUE_ROLL = 91

Sides of the tongue funnel, creating a roll.

BlendShapeEntry FT_TONGUE_BLEND_DOWN = 92

Tongue arches up then down inside the mouth.

BlendShapeEntry FT_TONGUE_CURL_UP = 93

Tongue arches down then up inside the mouth.

BlendShapeEntry FT_TONGUE_SQUISH = 94

Tongue squishes together and thickens.

BlendShapeEntry FT_TONGUE_FLAT = 95

Tongue flattens and thins out.

BlendShapeEntry FT_TONGUE_TWIST_RIGHT = 96

Tongue tip rotates clockwise, with the rest following gradually.

BlendShapeEntry FT_TONGUE_TWIST_LEFT = 97

Tongue tip rotates counter-clockwise, with the rest following gradually.

BlendShapeEntry FT_SOFT_PALATE_CLOSE = 98

Inner mouth throat closes.

BlendShapeEntry FT_THROAT_SWALLOW = 99

The Adam's apple visibly swallows.

BlendShapeEntry FT_NECK_FLEX_RIGHT = 100

Right side neck visibly flexes.

BlendShapeEntry FT_NECK_FLEX_LEFT = 101

Left side neck visibly flexes.

BlendShapeEntry FT_EYE_CLOSED = 102

Closes both eye lids.

BlendShapeEntry FT_EYE_WIDE = 103

Widens both eye lids.

BlendShapeEntry FT_EYE_SQUINT = 104

Squints both eye lids.

BlendShapeEntry FT_EYE_DILATION = 105

BlendShapeEntry FT_EYE_CONSTRICT = 106

Constricts both pupils.

BlendShapeEntry FT_BROW_DOWN_RIGHT = 107

Pulls the right eyebrow down and in.

BlendShapeEntry FT_BROW_DOWN_LEFT = 108

Pulls the left eyebrow down and in.

BlendShapeEntry FT_BROW_DOWN = 109

Pulls both eyebrows down and in.

BlendShapeEntry FT_BROW_UP_RIGHT = 110

Right brow appears worried.

BlendShapeEntry FT_BROW_UP_LEFT = 111

Left brow appears worried.

BlendShapeEntry FT_BROW_UP = 112

Both brows appear worried.

BlendShapeEntry FT_NOSE_SNEER = 113

BlendShapeEntry FT_NASAL_DILATION = 114

Both nose canals dilate.

BlendShapeEntry FT_NASAL_CONSTRICT = 115

Both nose canals constrict.

BlendShapeEntry FT_CHEEK_PUFF = 116

BlendShapeEntry FT_CHEEK_SUCK = 117

Sucks in both cheeks.

BlendShapeEntry FT_CHEEK_SQUINT = 118

BlendShapeEntry FT_LIP_SUCK_UPPER = 119

Tucks in the upper lips.

BlendShapeEntry FT_LIP_SUCK_LOWER = 120

Tucks in the lower lips.

BlendShapeEntry FT_LIP_SUCK = 121

BlendShapeEntry FT_LIP_FUNNEL_UPPER = 122

Funnels in the upper lips.

BlendShapeEntry FT_LIP_FUNNEL_LOWER = 123

Funnels in the lower lips.

BlendShapeEntry FT_LIP_FUNNEL = 124

Funnels in both lips.

BlendShapeEntry FT_LIP_PUCKER_UPPER = 125

Upper lip part pushes outwards.

BlendShapeEntry FT_LIP_PUCKER_LOWER = 126

Lower lip part pushes outwards.

BlendShapeEntry FT_LIP_PUCKER = 127

BlendShapeEntry FT_MOUTH_UPPER_UP = 128

Raises the upper lips.

BlendShapeEntry FT_MOUTH_LOWER_DOWN = 129

Lowers the lower lips.

BlendShapeEntry FT_MOUTH_OPEN = 130

Mouth opens, revealing teeth.

BlendShapeEntry FT_MOUTH_RIGHT = 131

BlendShapeEntry FT_MOUTH_LEFT = 132

BlendShapeEntry FT_MOUTH_SMILE_RIGHT = 133

Right side of the mouth smiles.

BlendShapeEntry FT_MOUTH_SMILE_LEFT = 134

Left side of the mouth smiles.

BlendShapeEntry FT_MOUTH_SMILE = 135

Mouth expresses a smile.

BlendShapeEntry FT_MOUTH_SAD_RIGHT = 136

Right side of the mouth expresses sadness.

BlendShapeEntry FT_MOUTH_SAD_LEFT = 137

Left side of the mouth expresses sadness.

BlendShapeEntry FT_MOUTH_SAD = 138

Mouth expresses sadness.

BlendShapeEntry FT_MOUTH_STRETCH = 139

BlendShapeEntry FT_MOUTH_DIMPLE = 140

BlendShapeEntry FT_MOUTH_TIGHTENER = 141

BlendShapeEntry FT_MOUTH_PRESS = 142

Mouth presses together.

BlendShapeEntry FT_MAX = 143

Represents the size of the BlendShapeEntry enum.

PackedFloat32Array blend_shapes = PackedFloat32Array() 🔗

void set_blend_shapes(value: PackedFloat32Array)

PackedFloat32Array get_blend_shapes()

The array of face blend shape weights with indices corresponding to the BlendShapeEntry enum.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedFloat32Array for more details.

float get_blend_shape(blend_shape: BlendShapeEntry) const 🔗

Returns the requested face blend shape weight.

void set_blend_shape(blend_shape: BlendShapeEntry, weight: float) 🔗

Sets a face blend shape weight.

Please read the User-contributed notes policy before submitting a comment.

---

## XRPositionalTracker

**URL:** https://docs.godotengine.org/en/stable/classes/class_xrpositionaltracker.html

**Contents:**
- XRPositionalTracker
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: XRTracker < RefCounted < Object

Inherited By: XRBodyTracker, XRControllerTracker, XRHandTracker

An instance of this object represents a device that is tracked, such as a controller or anchor point. HMDs aren't represented here as they are handled internally.

As controllers are turned on and the XRInterface detects them, instances of this object are automatically added to this list of active tracking objects accessible through the XRServer.

The XRNode3D and XRAnchor3D both consume objects of this type and should be used in your project. The positional trackers are just under-the-hood objects that make this all work. These are mostly exposed so that GDExtension-based interfaces can interact with them.

XR documentation index

get_input(name: StringName) const

get_pose(name: StringName) const

has_pose(name: StringName) const

invalidate_pose(name: StringName)

set_input(name: StringName, value: Variant)

set_pose(name: StringName, transform: Transform3D, linear_velocity: Vector3, angular_velocity: Vector3, tracking_confidence: TrackingConfidence)

button_pressed(name: String) 🔗

Emitted when a button on this tracker is pressed. Note that many XR runtimes allow other inputs to be mapped to buttons.

button_released(name: String) 🔗

Emitted when a button on this tracker is released.

input_float_changed(name: String, value: float) 🔗

Emitted when a trigger or similar input on this tracker changes value.

input_vector2_changed(name: String, vector: Vector2) 🔗

Emitted when a thumbstick or thumbpad on this tracker moves.

pose_changed(pose: XRPose) 🔗

Emitted when the state of a pose tracked by this tracker changes.

pose_lost_tracking(pose: XRPose) 🔗

Emitted when a pose tracked by this tracker stops getting updated tracking data.

profile_changed(role: String) 🔗

Emitted when the profile of our tracker changes.

TrackerHand TRACKER_HAND_UNKNOWN = 0

The hand this tracker is held in is unknown or not applicable.

TrackerHand TRACKER_HAND_LEFT = 1

This tracker is the left hand controller.

TrackerHand TRACKER_HAND_RIGHT = 2

This tracker is the right hand controller.

TrackerHand TRACKER_HAND_MAX = 3

Represents the size of the TrackerHand enum.

TrackerHand hand = 0 🔗

void set_tracker_hand(value: TrackerHand)

TrackerHand get_tracker_hand()

Defines which hand this tracker relates to.

String profile = "" 🔗

void set_tracker_profile(value: String)

String get_tracker_profile()

The profile associated with this tracker, interface dependent but will indicate the type of controller being tracked.

Variant get_input(name: StringName) const 🔗

Deprecated: Use through XRControllerTracker.

Returns an input for this tracker. It can return a boolean, float or Vector2 value depending on whether the input is a button, trigger or thumbstick/thumbpad.

XRPose get_pose(name: StringName) const 🔗

Returns the current XRPose state object for the bound name pose.

bool has_pose(name: StringName) const 🔗

Returns true if the tracker is available and is currently tracking the bound name pose.

void invalidate_pose(name: StringName) 🔗

Marks this pose as invalid, we don't clear the last reported state but it allows users to decide if trackers need to be hidden if we lose tracking or just remain at their last known position.

void set_input(name: StringName, value: Variant) 🔗

Deprecated: Use through XRControllerTracker.

Changes the value for the given input. This method is called by an XRInterface implementation and should not be used directly.

void set_pose(name: StringName, transform: Transform3D, linear_velocity: Vector3, angular_velocity: Vector3, tracking_confidence: TrackingConfidence) 🔗

Sets the transform, linear velocity, angular velocity and tracking confidence for the given pose. This method is called by an XRInterface implementation and should not be used directly.

Please read the User-contributed notes policy before submitting a comment.

---

## XRServer

**URL:** https://docs.godotengine.org/en/stable/classes/class_xrserver.html

**Contents:**
- XRServer
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Server for AR and VR features.

The AR/VR server is the heart of our Advanced and Virtual Reality solution and handles all the processing.

XR documentation index

camera_locked_to_origin

Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)

add_interface(interface: XRInterface)

add_tracker(tracker: XRTracker)

center_on_hmd(rotation_mode: RotationMode, keep_height: bool)

clear_reference_frame()

find_interface(name: String) const

get_interface(idx: int) const

get_interface_count() const

get_interfaces() const

get_reference_frame() const

get_tracker(tracker_name: StringName) const

get_trackers(tracker_types: int)

remove_interface(interface: XRInterface)

remove_tracker(tracker: XRTracker)

interface_added(interface_name: StringName) 🔗

Emitted when a new interface has been added.

interface_removed(interface_name: StringName) 🔗

Emitted when an interface is removed.

reference_frame_changed() 🔗

Emitted when the reference frame transform changes.

tracker_added(tracker_name: StringName, type: int) 🔗

Emitted when a new tracker has been added. If you don't use a fixed number of controllers or if you're using XRAnchor3Ds for an AR solution, it is important to react to this signal to add the appropriate XRController3D or XRAnchor3D nodes related to this new tracker.

tracker_removed(tracker_name: StringName, type: int) 🔗

Emitted when a tracker is removed. You should remove any XRController3D or XRAnchor3D points if applicable. This is not mandatory, the nodes simply become inactive and will be made active again when a new tracker becomes available (i.e. a new controller is switched on that takes the place of the previous one).

tracker_updated(tracker_name: StringName, type: int) 🔗

Emitted when an existing tracker has been updated. This can happen if the user switches controllers.

TrackerType TRACKER_HEAD = 1

The tracker tracks the location of the player's head. This is usually a location centered between the player's eyes. Note that for handheld AR devices this can be the current location of the device.

TrackerType TRACKER_CONTROLLER = 2

The tracker tracks the location of a controller.

TrackerType TRACKER_BASESTATION = 4

The tracker tracks the location of a base station.

TrackerType TRACKER_ANCHOR = 8

The tracker tracks the location and size of an AR anchor.

TrackerType TRACKER_HAND = 16

The tracker tracks the location and joints of a hand.

TrackerType TRACKER_BODY = 32

The tracker tracks the location and joints of a body.

TrackerType TRACKER_FACE = 64

The tracker tracks the expressions of a face.

TrackerType TRACKER_ANY_KNOWN = 127

Used internally to filter trackers of any known type.

TrackerType TRACKER_UNKNOWN = 128

Used internally if we haven't set the tracker type yet.

TrackerType TRACKER_ANY = 255

Used internally to select all trackers.

RotationMode RESET_FULL_ROTATION = 0

Fully reset the orientation of the HMD. Regardless of what direction the user is looking to in the real world. The user will look dead ahead in the virtual world.

RotationMode RESET_BUT_KEEP_TILT = 1

Resets the orientation but keeps the tilt of the device. So if we're looking down, we keep looking down but heading will be reset.

RotationMode DONT_RESET_ROTATION = 2

Does not reset the orientation of the HMD, only the position of the player gets centered.

bool camera_locked_to_origin = false 🔗

void set_camera_locked_to_origin(value: bool)

bool is_camera_locked_to_origin()

If set to true, the scene will be rendered as if the camera is locked to the XROrigin3D.

Note: This doesn't provide a very comfortable experience for users. This setting exists for doing benchmarking or automated testing, where you want to control what is rendered via code.

XRInterface primary_interface 🔗

void set_primary_interface(value: XRInterface)

XRInterface get_primary_interface()

The primary XRInterface currently bound to the XRServer.

Transform3D world_origin = Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0) 🔗

void set_world_origin(value: Transform3D)

Transform3D get_world_origin()

The current origin of our tracking space in the virtual world. This is used by the renderer to properly position the camera with new tracking data.

Note: This property is managed by the current XROrigin3D node. It is exposed for access from GDExtensions.

float world_scale = 1.0 🔗

void set_world_scale(value: float)

float get_world_scale()

The scale of the game world compared to the real world. By default, most AR/VR platforms assume that 1 game unit corresponds to 1 real world meter.

void add_interface(interface: XRInterface) 🔗

Registers an XRInterface object.

void add_tracker(tracker: XRTracker) 🔗

Registers a new XRTracker that tracks a physical object.

void center_on_hmd(rotation_mode: RotationMode, keep_height: bool) 🔗

This is an important function to understand correctly. AR and VR platforms all handle positioning slightly differently.

For platforms that do not offer spatial tracking, our origin point (0, 0, 0) is the location of our HMD, but you have little control over the direction the player is facing in the real world.

For platforms that do offer spatial tracking, our origin point depends very much on the system. For OpenVR, our origin point is usually the center of the tracking space, on the ground. For other platforms, it's often the location of the tracking camera.

This method allows you to center your tracker on the location of the HMD. It will take the current location of the HMD and use that to adjust all your tracking data; in essence, realigning the real world to your player's current position in the game world.

For this method to produce usable results, tracking information must be available. This often takes a few frames after starting your game.

You should call this method after a few seconds have passed. For example, when the user requests a realignment of the display holding a designated button on a controller for a short period of time, or when implementing a teleport mechanism.

void clear_reference_frame() 🔗

Clears the reference frame that was set by previous calls to center_on_hmd().

XRInterface find_interface(name: String) const 🔗

Finds an interface by its name. For example, if your project uses capabilities of an AR/VR platform, you can find the interface for that platform by name and initialize it.

Transform3D get_hmd_transform() 🔗

Returns the primary interface's transformation.

XRInterface get_interface(idx: int) const 🔗

Returns the interface registered at the given idx index in the list of interfaces.

int get_interface_count() const 🔗

Returns the number of interfaces currently registered with the AR/VR server. If your project supports multiple AR/VR platforms, you can look through the available interface, and either present the user with a selection or simply try to initialize each interface and use the first one that returns true.

Array[Dictionary] get_interfaces() const 🔗

Returns a list of available interfaces the ID and name of each interface.

Transform3D get_reference_frame() const 🔗

Returns the reference frame transform. Mostly used internally and exposed for GDExtension build interfaces.

XRTracker get_tracker(tracker_name: StringName) const 🔗

Returns the positional tracker with the given tracker_name.

Dictionary get_trackers(tracker_types: int) 🔗

Returns a dictionary of trackers for tracker_types.

void remove_interface(interface: XRInterface) 🔗

Removes this interface.

void remove_tracker(tracker: XRTracker) 🔗

Removes this tracker.

Please read the User-contributed notes policy before submitting a comment.

---

## XRTracker

**URL:** https://docs.godotengine.org/en/stable/classes/class_xrtracker.html

**Contents:**
- XRTracker
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Inherited By: XRFaceTracker, XRPositionalTracker

This object is the base of all XR trackers.

XR documentation index

String description = "" 🔗

void set_tracker_desc(value: String)

String get_tracker_desc()

The description of this tracker.

StringName name = &"Unknown" 🔗

void set_tracker_name(value: StringName)

StringName get_tracker_name()

The unique name of this tracker. The trackers that are available differ between various XR runtimes and can often be configured by the user. Godot maintains a number of reserved names that it expects the XRInterface to implement if applicable:

"head" identifies the XRPositionalTracker of the player's head

"left_hand" identifies the XRControllerTracker in the player's left hand

"right_hand" identifies the XRControllerTracker in the player's right hand

"/user/hand_tracker/left" identifies the XRHandTracker for the player's left hand

"/user/hand_tracker/right" identifies the XRHandTracker for the player's right hand

"/user/body_tracker" identifies the XRBodyTracker for the player's body

"/user/face_tracker" identifies the XRFaceTracker for the player's face

TrackerType type = 128 🔗

void set_tracker_type(value: TrackerType)

TrackerType get_tracker_type()

Please read the User-contributed notes policy before submitting a comment.

---

## XRVRS

**URL:** https://docs.godotengine.org/en/stable/classes/class_xrvrs.html

**Contents:**
- XRVRS
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Helper class for XR interfaces that generates VRS images.

This class is used by various XR interfaces to generate VRS textures that can be used to speed up rendering.

make_vrs_texture(target_size: Vector2, eye_foci: PackedVector2Array)

float vrs_min_radius = 20.0 🔗

void set_vrs_min_radius(value: float)

float get_vrs_min_radius()

The minimum radius around the focal point where full quality is guaranteed if VRS is used as a percentage of screen size.

Rect2i vrs_render_region = Rect2i(0, 0, 0, 0) 🔗

void set_vrs_render_region(value: Rect2i)

Rect2i get_vrs_render_region()

The render region that the VRS texture will be scaled to when generated.

float vrs_strength = 1.0 🔗

void set_vrs_strength(value: float)

float get_vrs_strength()

The strength used to calculate the VRS density map. The greater this value, the more noticeable VRS is.

RID make_vrs_texture(target_size: Vector2, eye_foci: PackedVector2Array) 🔗

Generates the VRS texture based on a render target_size adjusted by our VRS tile size. For each eyes focal point passed in eye_foci a layer is created. Focal point should be in NDC.

The result will be cached, requesting a VRS texture with unchanged parameters and settings will return the cached RID.

Please read the User-contributed notes policy before submitting a comment.

---

## XR

**URL:** https://docs.godotengine.org/en/stable/tutorials/xr/index.html

**Contents:**
- XR
- Basic Tutorial
- Advanced topics
- Godot XR Tools

This section of the manual covers everything related to XR ( Virtual Reality and Augmented Reality).

---
