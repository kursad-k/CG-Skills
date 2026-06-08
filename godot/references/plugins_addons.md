# Godot - Plugins Addons

**Pages:** 6

---

## Creating iOS plugins

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/ios/ios_plugin.html

**Contents:**
- Creating iOS plugins
- Loading and using an existing plugin
- Creating an iOS plugin
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

This page explains what iOS plugins can do for you, how to use an existing plugin, and the steps to code a new one.

iOS plugins allow you to use third-party libraries and support iOS-specific features like In-App Purchases, GameCenter integration, ARKit support, and more.

An iOS plugin requires a .gdip configuration file, a binary file which can be either .a static library or .xcframework containing .a static libraries, and possibly other dependencies. To use it, you need to:

Copy the plugin's files to your Godot project's res://ios/plugins directory. You can also group files in a sub-directory, like res://ios/plugins/my_plugin.

The Godot editor automatically detects and imports .gdip files inside res://ios/plugins and its subdirectories.

You can find and activate detected plugins by going to Project -> Export... -> iOS and in the Options tab, scrolling to the Plugins section.

When a plugin is active, you can access it in your code using Engine.get_singleton():

The plugin's files have to be in the res://ios/plugins/ directory or a subdirectory, otherwise the Godot editor will not automatically detect them.

At its core, a Godot iOS plugin is an iOS library (.a archive file or .xcframework containing static libraries) with the following requirements:

The library must have a dependency on the Godot engine headers.

The library must come with a .gdip configuration file.

An iOS plugin can have the same functionality as a Godot module but provides more flexibility and doesn't require to rebuild the engine.

Here are the steps to get a plugin's development started. We recommend using Xcode as your development environment.

The Godot iOS Plugins.

The Godot iOS plugin template gives you all the boilerplate you need to get your iOS plugin started.

To build an iOS plugin:

Create an Objective-C static library for your plugin inside Xcode.

Add the Godot engine header files as a dependency for your plugin library in HEADER_SEARCH_PATHS. You can find the setting inside the Build Settings tab:

Download the Godot engine source from the Godot GitHub page.

Run SCons to generate headers. You can learn the process by reading Compiling for iOS. You don't have to wait for compilation to complete to move forward as headers are generated before the engine starts to compile.

You should use the same header files for iOS plugins and for the iOS export template.

In the Build Settings tab, specify the compilation flags for your static library in OTHER_CFLAGS. The most important ones are -fcxx-modules, -fmodules, and -DDEBUG if you need debug support. Other flags should be the same you use to compile Godot. For instance:

Add the required logic for your plugin and build your library to generate a .a file. You will probably need to build both debug and release target .a files. Depending on your needs, pick either or both. If you need both debug and release .a files, their name should match following pattern: [PluginName].[TargetType].a. You can also build the static library with your SCons configuration.

The iOS plugin system also supports .xcframework files. To generate one, you can use a command such as:

Create a Godot iOS Plugin configuration file to help the system detect and load your plugin:

The configuration file extension must be gdip (e.g.: MyPlugin.gdip).

The configuration file format is as follow:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
if Engine.has_singleton("MyPlugin"):
    var singleton = Engine.get_singleton("MyPlugin")
    print(singleton.foo())
```

Example 2 (unknown):
```unknown
-DPTRCALL_ENABLED -DDEBUG_ENABLED -DDEBUG_MEMORY_ALLOC -DDISABLE_FORCED_INLINE -DTYPED_METHOD_BIND
```

Example 3 (unknown):
```unknown
xcodebuild -create-xcframework -library [DeviceLibrary].a -library [SimulatorLibrary].a -output [PluginName].xcframework
```

Example 4 (typescript):
```typescript
[config]
    name="MyPlugin"
    binary="MyPlugin.a"

    initialization="init_my_plugin"
    deinitialization="deinit_my_plugin"

    [dependencies]
    linked=[]
    embedded=[]
    system=["Foundation.framework"]

    capabilities=["arkit", "metal"]

    files=["data.json"]

    linker_flags=["-ObjC"]

    [plist]
    PlistKeyWithDefaultType="Some Info.plist key you might need"
    StringPlistKey:string="String value"
    IntegerPlistKey:integer=42
    BooleanPlistKey:boolean=true
    RawPlistKey:raw="
    <array>
        <string>UIInterfaceOrientationPortrait</string>
    </array>
    "
    StringPlistKeyToInput:string_input="Type something"

The ``config`` section and fields are required and defined as follow:

    -   **name**: name of the plugin

    -   **binary**: this should be the filepath of the plugin library (``a`` or ``xcframework``) file.

        -   The filepath can be relative (e.g.: ``MyPlugin.a``, ``MyPlugin.xcframework``) in which case it's relative to the directory where the ``gdip`` file is located.
        -   The filepath can be absolute: ``res://some_path/MyPlugin.a`` or ``res://some_path/MyPlugin.xcframework``.
        -   In case you need multitarget library usage, the filename should be ``MyPlugin.a`` and ``.a`` files should be named as ``MyPlugin.release.a`` and ``MyPlugin.debug.a``.
        -   In case you use multitarget ``xcframework`` libraries, their filename in the configuration should be ``MyPlugin.xcframework``. The ``.xcframework`` files should be named as ``MyPlugin.release.xcframework`` and ``MyPlugin.debug.xcframework``.

The ``dependencies`` and ``plist`` sections are optional and defined as follow:

    -   **dependencies**:

        -   **linked**: contains a list of iOS frameworks that the iOS application should be linked with.

        -   **embedded**: contains a list of iOS frameworks or libraries that should be both linked and embedded into the resulting iOS application.

        -   **system**: contains a list of iOS system frameworks that are required for plugin.

        -   **capabilities**: contains a list of iOS capabilities that is required for plugin. A list of available capabilities can be found at `Apple UIRequiredDeviceCapabilities documentation page <https://developer.apple.com/documentation/bundleresources/information_property_list/uirequireddevicecapabilities>`_.

        -   **files**: contains a list of files that should be copied on export. This is useful for data files or images.

        -   **linker_flags**: contains a list of linker flags to add to the Xcode project when exporting the plugin.

    -   **plist**: should have keys and values that should be present in ``Info.plist`` file.

        -   Each line should follow pattern: ``KeyName:KeyType=KeyValue``
        -   Supported values for ``KeyType`` are ``string``, ``integer``, ``boolean``, ``raw``, ``string_input``
        -   If no type is used (e.g.: ``KeyName="KeyValue"``) ``string`` type will be used.
        -   If ``raw`` type is used value for corresponding key will be stored in ``Info.plist`` as is.
        -   If ``string_input`` type is used you will be able to modify value in Export window.
```

---

## Integrating with Android APIs

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/android/javaclasswrapper_and_androidruntimeplugin.html

**Contents:**
- Integrating with Android APIs
- JavaClassWrapper (Godot singleton)
- AndroidRuntime plugin
  - Example: Show an Android toast
  - Example: Vibrate the device
  - Example: Accessing inner classes
  - Example: Calling a constructor
- User-contributed notes

The Android platform has numerous APIs as well as a rich ecosystem of third-party libraries with wide and diverse functionality, like push notifications, analytics, authentication, ads, etc...

These don't make sense in Godot core itself so Godot has long provided an Android plugin system. The Android plugin system enables developers to create Godot Android plugins using Java or Kotlin code, which provides an interface to access and use Android APIs or third-party libraries in Godot projects from GDScript, C# or GDExtension.

Writing an Android plugin however requires knowledge of Java or Kotlin code, which most Godot developers do not have. As such there are many Android APIs and third-party libraries that don't have a Godot plugin that developers can interface with. In fact, this is one of the main reasons that developers cite for not being able to switch to Godot from other game engines.

To address this, we've introduced a couple of tools in Godot 4.4 to simplify the process for developers to access Android APIs and third-party libraries.

JavaClassWrapper is a Godot singleton which allows creating instances of Java / Kotlin classes and calling methods on them using only GDScript, C# or GDExtension.

In the code snippet above, JavaClassWrapper is used from GDScript to access the Java LocalDateTime and DateTimeFormatter classes. Through JavaClassWrapper, we can call the Java classes methods directly from GDScript as if they were GDScript methods.

JavaClassWrapper is great, but to do many things on Android, you need access to various Android lifecycle / runtime objects. AndroidRuntime plugin is a built-in Godot Android plugin that allows you to do this.

Combining JavaClassWrapper and AndroidRuntime plugin allows developers to access and use Android APIs without switching away from GDScript, or using any tools aside from Godot itself. This is huge for the adoption of Godot for Android development:

If you need to do something simple, or only use a small part of a third-party library, you don't have to make a plugin

It allows developers to quickly integrate Android functionality

It allows developers to create Godot addons using only GDScript and JavaClassWrapper (no Java or Kotlin needed)

For exports using gradle, Godot will automatically include .jar or .aar files it find in the project addons directory. So to use a third-party library, you can just drop its .jar or .aar file in the addons directory, and call its method directly from GDScript using JavaClassWrapper.

Java inner classes can be accessed using the $ sign:

A constructor is invoked by calling a method with the same name as the class.

This example creates an intent to send a text:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
class MyAndroidSingleton(godot: Godot?) : GodotPlugin(godot) {
        @UsedByGodot
        fun doSomething(value: String) {
                // ...
        }
}
```

Example 2 (gdscript):
```gdscript
var LocalDateTime = JavaClassWrapper.wrap("java.time.LocalDateTime")
var DateTimeFormatter = JavaClassWrapper.wrap("java.time.format.DateTimeFormatter")

var datetime = LocalDateTime.now()
var formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss")

print(datetime.format(formatter))
```

Example 3 (php):
```php
# Retrieve the AndroidRuntime singleton.
var android_runtime = Engine.get_singleton("AndroidRuntime")
if android_runtime:
    # Retrieve the Android Activity instance.
    var activity = android_runtime.getActivity()

    # Create a Godot Callable to wrap the toast display logic.
    var toast_callable = func():
        # Use JavaClassWrapper to retrieve the android.widget.Toast class, then make and show a toast using the class APIs.
        var ToastClass = JavaClassWrapper.wrap("android.widget.Toast")
        ToastClass.makeText(activity, "This is a test", ToastClass.LENGTH_LONG).show()

    # Wrap the Callable in a Java Runnable and run it on the Android UI thread to show the toast.
    activity.runOnUiThread(android_runtime.createRunnableFromGodotCallable(toast_callable))
```

Example 4 (gdscript):
```gdscript
# Retrieve the AndroidRuntime singleton.
var android_runtime = Engine.get_singleton("AndroidRuntime")
if android_runtime:
    # Retrieve the Android Vibrator system service and check if the device supports it.
    var vibrator_service = android_runtime.getApplicationContext().getSystemService("vibrator")
    if vibrator_service and vibrator_service.hasVibrator():
        # Configure and run a VibrationEffect.
        var VibrationEffect = JavaClassWrapper.wrap("android.os.VibrationEffect")
        var effect = VibrationEffect.createOneShot(500, VibrationEffect.DEFAULT_AMPLITUDE)
        vibrator_service.vibrate(effect)
```

---

## iOS plugins

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/ios/index.html

**Contents:**
- iOS plugins

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

---

## Navigation debug tools

**URL:** https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_debug_tools.html

**Contents:**
- Navigation debug tools
- Enabling navigation debug
- Navigation debug settings
- Debug navigation mesh polygons
- Debug edge connections
- Debug performance
- User-contributed notes

The debug tools, properties and functions are only available in Godot debug builds. Do not use any of them in code that will be part of a release build.

The navigation debug visualizations are enabled by default inside the editor. To visualize navigation meshes and connections at runtime too, enable the option Visible Navigation in the editor Debug menu.

In Godot debug builds the navigation debug can also be toggled through the NavigationServer singletons from scripts.

Debug visualizations are currently based on Nodes in the SceneTree. If the NavigationServer2D or NavigationServer3D APIs are used exclusively then changes will not be reflected by the debug navigation tools.

The appearance of navigation debug can be changed in the ProjectSettings under debug/shapes/navigation. Certain debug features can also be enabled or disabled at will but may require a scene restart to take effect.

If enable_edge_lines is enabled, the edges of navigation mesh polygons will be highlighted. If enable_edge_lines_xray is also enabled, the edges of navigation meshes will be visible through geometry.

If enable_geometry_face_random_color is enabled, the color of each navigation mesh face will be mixed with a random color that is itself mixed with the color specified in geometry_face_color.

When two navigation meshes are connected within edge_connection_margin distance, the connection is overlaid. The color of the overlay is controlled by edge_connection_color. The connections can be made visible through geometry with enable_edge_connections_xray.

Edge connections are only visible when the NavigationServer is active.

To measure NavigationServer performance a dedicated monitor exists that can be found within the Editor Debugger under Debugger->Monitors->Navigation Process.

Navigation Process shows how long the NavigationServer spends updating its internals this update frame in milliseconds. Navigation Process works similar to Process for visual frame rendering and Physics Process for collision and fixed updates.

Navigation Process accounts for all updates to navigation maps, navigation regions and navigation agents as well as all the avoidance calculations for the update frame.

Navigation Process does NOT include pathfinding performance cause pathfinding operates on the navigation map data independently from the server process update.

Navigation Process should be in general kept as low and as stable as possible for runtime performance to avoid frame rate issues. Note that since the NavigationServer process update happens in the middle of the physics update an increase in Navigation Process will automatically increase Physics Process by the same amount.

Navigation also provides more detailed statistics about the current navigation related objects and navigation map composition on the NavigationServer.

Navigation statistics shown here can not be judged as good or bad for performance as it depends entirely on the project what can be considered as reasonable or horribly excessive.

Navigation statistics help with identifying performance bottlenecks that are less obvious because the source might not always have a visible representation. E.g. pathfinding performance issues created by overly detailed navigation meshes with thousand of edges / polygons or problems caused by procedural navigation gone wrong.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
NavigationServer2D.set_debug_enabled(false)
NavigationServer3D.set_debug_enabled(true)
```

Example 2 (unknown):
```unknown
NavigationServer2D.SetDebugEnabled(false);
NavigationServer3D.SetDebugEnabled(true);
```

---

## Plugins for iOS

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/ios/plugins_for_ios.html

**Contents:**
- Plugins for iOS
- Accessing plugin singletons
- Asynchronous methods
- Store Kit
  - purchase
    - Parameters
    - Response event
  - request_product_info
    - Parameters
    - Response event

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

Godot provides StoreKit, GameCenter, iCloud services and other plugins. They are using same model of asynchronous calls explained below.

ARKit and Camera access are also provided as plugins.

Latest updates, documentation and source code can be found at Godot iOS plugins repository

To access plugin functionality, you first need to check that the plugin is exported and available by calling the Engine.has_singleton() function, which returns a registered singleton.

Here's an example of how to do this in GDScript:

When requesting an asynchronous operation, the method will look like this:

The parameter will usually be a Dictionary, with the information necessary to make the request, and the call will have two phases. First, the method will immediately return an Error value. If the Error is not 'OK', the call operation is completed, with an error probably caused locally (no internet connection, API incorrectly configured, etc). If the error value is 'OK', a response event will be produced and added to the 'pending events' queue. Example:

Remember that when a call returns OK, the API will always produce an event through the pending_event interface, even if it's an error, or a network timeout, etc. You should be able to, for example, safely block the interface waiting for a reply from the server. If any of the APIs don't behave this way it should be treated as a bug.

The pending event interface consists of two methods:

get_pending_event_count() Returns the number of pending events on the queue.

Variant pop_pending_event() Pops the first event from the queue and returns it.

Implemented in Godot iOS InAppStore plugin.

The Store Kit API is accessible through the InAppStore singleton. It is initialized automatically.

The following methods are available and documented below:

Purchases a product ID through the Store Kit API. You have to call finish_transaction(product_id) once you receive a successful response or call set_auto_finish_transaction(true) prior to calling purchase(). These two methods ensure the transaction is completed.

Takes a dictionary as a parameter, with one field, product_id, a string with your product ID. Example:

The response event will be a dictionary with the following fields:

Requests the product info on a list of product IDs.

Takes a dictionary as a parameter, with a single product_ids key to which a string array of product IDs is assigned. Example:

The response event will be a dictionary with the following fields:

Restores previously made purchases on user's account. This will create response events for each previously purchased product ID.

The response events will be dictionaries with the following fields:

If set to true, once a purchase is successful, your purchase will be finalized automatically. Call this method prior to calling purchase().

Takes a boolean as a parameter which specifies if purchases should be automatically finalized. Example:

If you don't want transactions to be automatically finalized, call this method after you receive a successful purchase response.

Takes a string product_id as an argument. product_id specifies what product to finalize the purchase on. Example:

Implemented in Godot iOS GameCenter plugin.

The Game Center API is available through the GameCenter singleton. It has the following methods:

and the pending events interface:

Authenticates a user in Game Center.

The response event will be a dictionary with the following fields:

Posts a score to a Game Center leaderboard.

Takes a dictionary as a parameter, with two fields:

category a string with the category name

The response event will be a dictionary with the following fields:

Modifies the progress of a Game Center achievement.

Takes a Dictionary as a parameter, with 3 fields:

name (string) the achievement name

progress (float) the achievement progress from 0.0 to 100.0 (passed to GKAchievement::percentComplete)

show_completion_banner (bool) whether Game Center should display an achievement banner at the top of the screen

The response event will be a dictionary with the following fields:

Clears all Game Center achievements. The function takes no parameters.

The response event will be a dictionary with the following fields:

Request all the Game Center achievements the player has made progress on. The function takes no parameters.

The response event will be a dictionary with the following fields:

Request the descriptions of all existing Game Center achievements regardless of progress. The function takes no parameters.

The response event will be a dictionary with the following fields:

Displays the built-in Game Center overlay showing leaderboards, achievements, and challenges.

Takes a Dictionary as a parameter, with two fields:

view (string) (optional) the name of the view to present. Accepts "default", "leaderboards", "achievements", or "challenges". Defaults to "default".

leaderboard_name (string) (optional) the name of the leaderboard to present. Only used when "view" is "leaderboards" (or "default" is configured to show leaderboards). If not specified, Game Center will display the aggregate leaderboard.

The response event will be a dictionary with the following fields:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var in_app_store
var game_center

func _ready():
    if Engine.has_singleton("InAppStore"):
        in_app_store = Engine.get_singleton("InAppStore")
    else:
        print("iOS IAP plugin is not available on this platform.")

    if Engine.has_singleton("GameCenter"):
        game_center = Engine.get_singleton("GameCenter")
    else:
        print("iOS Game Center plugin is not available on this platform.")
```

Example 2 (unknown):
```unknown
Error purchase(Variant params);
```

Example 3 (gdscript):
```gdscript
func on_purchase_pressed():
    var result = in_app_store.purchase({ "product_id": "my_product" })
    if result == OK:
        animation.play("busy") # show the "waiting for response" animation
    else:
        show_error()

# put this on a 1 second timer or something
func check_events():
    while in_app_store.get_pending_event_count() > 0:
        var event = in_app_store.pop_pending_event()
        if event.type == "purchase":
            if event.result == "ok":
                show_success(event.product_id)
            else:
                show_error()
```

Example 4 (julia):
```julia
Error purchase(Variant params)
   Error request_product_info(Variant params)
   Error restore_purchases()
   void set_auto_finish_transaction(bool enable)
   void finish_transaction(String product_id)

and the pending events interface:

::

   int get_pending_event_count()
   Variant pop_pending_event()
```

---

## SurfaceTool

**URL:** https://docs.godotengine.org/en/stable/classes/class_surfacetool.html

**Contents:**
- SurfaceTool
- Description
- Tutorials
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Helper tool to create geometry.

The SurfaceTool is used to construct a Mesh by specifying vertex attributes individually. It can be used to construct a Mesh from a script. All properties except indices need to be added before calling add_vertex(). For example, to add vertex colors and UVs:

The above SurfaceTool now contains one vertex of a triangle which has a UV coordinate and a specified Color. If another vertex were added without calling set_uv() or set_color(), then the last values would be used.

Vertex attributes must be passed before calling add_vertex(). Failure to do so will result in an error when committing the vertex information to a mesh.

Additionally, the attributes used before the first vertex is added determine the format of the mesh. For example, if you only add UVs to the first vertex, you cannot add color to any of the subsequent vertices.

See also ArrayMesh, ImmediateMesh and MeshDataTool for procedural geometry generation.

Note: Godot uses clockwise winding order for front faces of triangle primitive modes.

Using the SurfaceTool

add_index(index: int)

add_triangle_fan(vertices: PackedVector3Array, uvs: PackedVector2Array = PackedVector2Array(), colors: PackedColorArray = PackedColorArray(), uv2s: PackedVector2Array = PackedVector2Array(), normals: PackedVector3Array = PackedVector3Array(), tangents: Array[Plane] = [])

add_vertex(vertex: Vector3)

append_from(existing: Mesh, surface: int, transform: Transform3D)

begin(primitive: PrimitiveType)

commit(existing: ArrayMesh = null, flags: int = 0)

create_from(existing: Mesh, surface: int)

create_from_arrays(arrays: Array, primitive_type: PrimitiveType = 3)

create_from_blend_shape(existing: Mesh, surface: int, blend_shape: String)

generate_lod(nd_threshold: float, target_index_count: int = 3)

generate_normals(flip: bool = false)

get_custom_format(channel_index: int) const

get_primitive_type() const

get_skin_weight_count() const

optimize_indices_for_cache()

set_bones(bones: PackedInt32Array)

set_color(color: Color)

set_custom(channel_index: int, custom_color: Color)

set_custom_format(channel_index: int, format: CustomFormat)

set_material(material: Material)

set_normal(normal: Vector3)

set_skin_weight_count(count: SkinWeightCount)

set_smooth_group(index: int)

set_tangent(tangent: Plane)

set_uv2(uv2: Vector2)

set_weights(weights: PackedFloat32Array)

CustomFormat CUSTOM_RGBA8_UNORM = 0

Limits range of data passed to set_custom() to unsigned normalized 0 to 1 stored in 8 bits per channel. See Mesh.ARRAY_CUSTOM_RGBA8_UNORM.

CustomFormat CUSTOM_RGBA8_SNORM = 1

Limits range of data passed to set_custom() to signed normalized -1 to 1 stored in 8 bits per channel. See Mesh.ARRAY_CUSTOM_RGBA8_SNORM.

CustomFormat CUSTOM_RG_HALF = 2

Stores data passed to set_custom() as half precision floats, and uses only red and green color channels. See Mesh.ARRAY_CUSTOM_RG_HALF.

CustomFormat CUSTOM_RGBA_HALF = 3

Stores data passed to set_custom() as half precision floats and uses all color channels. See Mesh.ARRAY_CUSTOM_RGBA_HALF.

CustomFormat CUSTOM_R_FLOAT = 4

Stores data passed to set_custom() as full precision floats, and uses only red color channel. See Mesh.ARRAY_CUSTOM_R_FLOAT.

CustomFormat CUSTOM_RG_FLOAT = 5

Stores data passed to set_custom() as full precision floats, and uses only red and green color channels. See Mesh.ARRAY_CUSTOM_RG_FLOAT.

CustomFormat CUSTOM_RGB_FLOAT = 6

Stores data passed to set_custom() as full precision floats, and uses only red, green and blue color channels. See Mesh.ARRAY_CUSTOM_RGB_FLOAT.

CustomFormat CUSTOM_RGBA_FLOAT = 7

Stores data passed to set_custom() as full precision floats, and uses all color channels. See Mesh.ARRAY_CUSTOM_RGBA_FLOAT.

CustomFormat CUSTOM_MAX = 8

Used to indicate a disabled custom channel.

enum SkinWeightCount: 

SkinWeightCount SKIN_4_WEIGHTS = 0

Each individual vertex can be influenced by only 4 bone weights.

SkinWeightCount SKIN_8_WEIGHTS = 1

Each individual vertex can be influenced by up to 8 bone weights.

void add_index(index: int) 

Adds a vertex to index array if you are using indexed vertices. Does not need to be called before adding vertices.

void add_triangle_fan(vertices: PackedVector3Array, uvs: PackedVector2Array = PackedVector2Array(), colors: PackedColorArray = PackedColorArray(), uv2s: PackedVector2Array = PackedVector2Array(), normals: PackedVector3Array = PackedVector3Array(), tangents: Array[Plane] = []) 

Inserts a triangle fan made of array data into Mesh being constructed.

Requires the primitive type be set to Mesh.PRIMITIVE_TRIANGLES.

void add_vertex(vertex: Vector3) 

Specifies the position of current vertex. Should be called after specifying other vertex properties (e.g. Color, UV).

void append_from(existing: Mesh, surface: int, transform: Transform3D) 

Append vertices from a given Mesh surface onto the current vertex array with specified Transform3D.

void begin(primitive: PrimitiveType) 

Called before adding any vertices. Takes the primitive type as an argument (e.g. Mesh.PRIMITIVE_TRIANGLES).

Clear all information passed into the surface tool so far.

ArrayMesh commit(existing: ArrayMesh = null, flags: int = 0) 

Returns a constructed ArrayMesh from current information passed in. If an existing ArrayMesh is passed in as an argument, will add an extra surface to the existing ArrayMesh.

The flags argument can be the bitwise OR of Mesh.ARRAY_FLAG_USE_DYNAMIC_UPDATE, Mesh.ARRAY_FLAG_USE_8_BONE_WEIGHTS, or Mesh.ARRAY_FLAG_USES_EMPTY_VERTEX_ARRAY.

Array commit_to_arrays() 

Commits the data to the same format used by ArrayMesh.add_surface_from_arrays(), ImporterMesh.add_surface(), and create_from_arrays(). This way you can further process the mesh data using the ArrayMesh or ImporterMesh APIs.

void create_from(existing: Mesh, surface: int) 

Creates a vertex array from an existing Mesh.

void create_from_arrays(arrays: Array, primitive_type: PrimitiveType = 3) 

Creates this SurfaceTool from existing vertex arrays such as returned by commit_to_arrays(), Mesh.surface_get_arrays(), Mesh.surface_get_blend_shape_arrays(), ImporterMesh.get_surface_arrays(), and ImporterMesh.get_surface_blend_shape_arrays(). primitive_type controls the type of mesh data, defaulting to Mesh.PRIMITIVE_TRIANGLES.

void create_from_blend_shape(existing: Mesh, surface: int, blend_shape: String) 

Creates a vertex array from the specified blend shape of an existing Mesh. This can be used to extract a specific pose from a blend shape.

Removes the index array by expanding the vertex array.

PackedInt32Array generate_lod(nd_threshold: float, target_index_count: int = 3) 

Deprecated: This method is unused internally, as it does not preserve normals or UVs. Consider using ImporterMesh.generate_lods() instead.

Generates an LOD for a given nd_threshold in linear units (square root of quadric error metric), using at most target_index_count indices.

void generate_normals(flip: bool = false) 

Generates normals from vertices so you do not have to do it manually. If flip is true, the resulting normals will be inverted. generate_normals() should be called after generating geometry and before committing the mesh using commit() or commit_to_arrays(). For correct display of normal-mapped surfaces, you will also have to generate tangents using generate_tangents().

Note: generate_normals() only works if the primitive type is set to Mesh.PRIMITIVE_TRIANGLES.

Note: generate_normals() takes smooth groups into account. To generate smooth normals, set the smooth group to a value greater than or equal to 0 using set_smooth_group() or leave the smooth group at the default of 0. To generate flat normals, set the smooth group to -1 using set_smooth_group() prior to adding vertices.

void generate_tangents() 

Generates a tangent vector for each vertex. Requires that each vertex already has UVs and normals set (see generate_normals()).

AABB get_aabb() const 

Returns the axis-aligned bounding box of the vertex positions.

CustomFormat get_custom_format(channel_index: int) const 

Returns the format for custom channel_index (currently up to 4). Returns CUSTOM_MAX if this custom channel is unused.

PrimitiveType get_primitive_type() const 

Returns the type of mesh geometry, such as Mesh.PRIMITIVE_TRIANGLES.

SkinWeightCount get_skin_weight_count() const 

By default, returns SKIN_4_WEIGHTS to indicate only 4 bone influences per vertex are used.

Returns SKIN_8_WEIGHTS if up to 8 influences are used.

Note: This function returns an enum, not the exact number of weights.

Shrinks the vertex array by creating an index array. This can improve performance by avoiding vertex reuse.

void optimize_indices_for_cache() 

Optimizes triangle sorting for performance. Requires that get_primitive_type() is Mesh.PRIMITIVE_TRIANGLES.

void set_bones(bones: PackedInt32Array) 

Specifies an array of bones to use for the next vertex. bones must contain 4 integers.

void set_color(color: Color) 

Specifies a Color to use for the next vertex. If every vertex needs to have this information set and you fail to submit it for the first vertex, this information may not be used at all.

Note: The material must have BaseMaterial3D.vertex_color_use_as_albedo enabled for the vertex color to be visible.

void set_custom(channel_index: int, custom_color: Color) 

Sets the custom value on this vertex for channel_index.

set_custom_format() must be called first for this channel_index. Formats which are not RGBA will ignore other color channels.

void set_custom_format(channel_index: int, format: CustomFormat) 

Sets the color format for this custom channel_index. Use CUSTOM_MAX to disable.

Must be invoked after begin() and should be set before commit() or commit_to_arrays().

void set_material(material: Material) 

Sets Material to be used by the Mesh you are constructing.

void set_normal(normal: Vector3) 

Specifies a normal to use for the next vertex. If every vertex needs to have this information set and you fail to submit it for the first vertex, this information may not be used at all.

void set_skin_weight_count(count: SkinWeightCount) 

Set to SKIN_8_WEIGHTS to indicate that up to 8 bone influences per vertex may be used.

By default, only 4 bone influences are used (SKIN_4_WEIGHTS).

Note: This function takes an enum, not the exact number of weights.

void set_smooth_group(index: int) 

Specifies the smooth group to use for the next vertex. If this is never called, all vertices will have the default smooth group of 0 and will be smoothed with adjacent vertices of the same group. To produce a mesh with flat normals, set the smooth group to -1.

Note: This function actually takes a uint32_t, so C# users should use uint32.MaxValue instead of -1 to produce a mesh with flat normals.

void set_tangent(tangent: Plane) 

Specifies a tangent to use for the next vertex. If every vertex needs to have this information set and you fail to submit it for the first vertex, this information may not be used at all.

void set_uv(uv: Vector2) 

Specifies a set of UV coordinates to use for the next vertex. If every vertex needs to have this information set and you fail to submit it for the first vertex, this information may not be used at all.

void set_uv2(uv2: Vector2) 

Specifies an optional second set of UV coordinates to use for the next vertex. If every vertex needs to have this information set and you fail to submit it for the first vertex, this information may not be used at all.

void set_weights(weights: PackedFloat32Array) 

Specifies weight values to use for the next vertex. weights must contain 4 values. If every vertex needs to have this information set and you fail to submit it for the first vertex, this information may not be used at all.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
var st = SurfaceTool.new()
st.begin(Mesh.PRIMITIVE_TRIANGLES)
st.set_color(Color(1, 0, 0))
st.set_uv(Vector2(0, 0))
st.add_vertex(Vector3(0, 0, 0))
```

Example 2 (csharp):
```csharp
var st = new SurfaceTool();
st.Begin(Mesh.PrimitiveType.Triangles);
st.SetColor(new Color(1, 0, 0));
st.SetUV(new Vector2(0, 0));
st.AddVertex(new Vector3(0, 0, 0));
```

---
