# Godot - Platform Export

**Pages:** 41

---

## Android in-app purchases

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/android/android_in_app_purchases.html

**Contents:**
- Android in-app purchases
- Usage
  - Getting started
  - Initialize the plugin
  - Query available items
  - Query user purchases
  - Purchase an item
  - Processing a purchase item
  - Check purchase state
  - Consumables

Godot offers a first-party GodotGooglePlayBilling Android plugin compatible with Godot 4.2+ which uses the Google Play Billing library.

Make sure you have enabled and successfully set up Android Gradle Builds. Follow the installation instructions on the GodotGooglePlayBilling github page.

To use the GodotGooglePlayBilling API:

Access the BillingClient.

Connect to its signals to receive billing results.

Call start_connection.

Initialization example:

The API must be in a connected state prior to use. The connected signal is sent when the connection process succeeds. You can also use is_ready() to determine if the plugin is ready for use. The get_connection_state() function returns the current connection state of the plugin.

Return values for get_connection_state():

Once the API has connected, query product IDs using query_product_details(). You must successfully complete a product details query before calling the purchase(), purchase_subscription(), or update_subscription() functions, or they will return an error. query_product_details() takes two parameters: an array of product ID strings and the type of product being queried. The product type should be BillingClient.ProductType.INAPP for normal in-app purchases or BillingClient.ProductType.SUBS for subscriptions. The ID strings in the array should match the product IDs defined in the Google Play Console entry for your app.

Example use of query_product_details():

To retrieve a user's purchases, call the query_purchases() function passing a product type to query. The product type should be BillingClient.ProductType.INAPP for normal in-app purchases or BillingClient.ProductType.SUBS for subscriptions. The query_purchases_response signal is sent with the result. The signal has a single parameter: a Dictionary with a response code and either an array of purchases or a debug message. Only active subscriptions and non-consumed one-time purchases are included in the purchase array.

Example use of query_purchases():

To launch the billing flow for an item: Use purchase() for in-app products, passing the product ID string. Use purchase_subscription() for subscriptions, passing the product ID and base plan ID. You may also optionally provide an offer ID.

For both purchase() and purchase_subscription(), you can optionally pass a boolean to indicate whether offers are personallised

Reminder: you must query the product details for an item before you can pass it to purchase(). This method returns a dictionary indicating whether the billing flow was successfully launched. It includes a response code and either an array of purchases or a debug message.

Example use of purchase():

The result of the purchase will be sent through the on_purchases_updated signal.

The query_purchases_response and on_purchases_updated signals provide an array of purchases in Dictionary format. The purchase Dictionary includes keys that map to values of the Google Play Billing Purchase class.

Check the purchase_state value of a purchase to determine if a purchase was completed or is still pending.

PurchaseState values:

If a purchase is in a PENDING state, you should not award the contents of the purchase or do any further processing of the purchase until it reaches the PURCHASED state. If you have a store interface, you may wish to display information about pending purchases needing to be completed in the Google Play Store. For more details on pending purchases, see Handling pending transactions in the Google Play Billing Library documentation.

If your in-app item is not a one-time purchase but a consumable item (e.g. coins) which can be purchased multiple times, you can consume an item by calling consume_purchase() passing the purchase_token value from the purchase dictionary. Calling consume_purchase() automatically acknowledges a purchase. Consuming a product allows the user to purchase it again, it will no longer appear in subsequent query_purchases() calls unless it is repurchased.

Example use of consume_purchase():

If your in-app item is a one-time purchase, you must acknowledge the purchase by calling the acknowledge_purchase() function, passing the purchase_token value from the purchase dictionary. If you do not acknowledge a purchase within three days, the user automatically receives a refund, and Google Play revokes the purchase. If you are calling comsume_purchase() it automatically acknowledges the purchase and you do not need to call acknowledge_purchase().

Example use of acknowledge_purchase():

Subscriptions work mostly like regular in-app items. Use BillingClient.ProductType.SUBS as the second argument to query_product_details() to get subscription details. Pass BillingClient.ProductType.SUBS to query_purchases() to get subscription purchase details.

You can check is_auto_renewing in the a subscription purchase returned from query_purchases() to see if a user has cancelled an auto-renewing subscription.

You need to acknowledge new subscription purchases, but not automatic subscription renewals.

If you support upgrading or downgrading between different subscription levels, you should use update_subscription() to use the subscription update flow to change an active subscription. Like purchase(), results are returned by the on_purchases_updated signal. These are the parameters of update_subscription():

old_purchase_token: The purchase token of the currently active subscription

replacement_mode: The replacement mode to apply to the subscription

product_id: The product ID of the new subscription to switch to

base_plan_id: The base plan ID of the target subscription

offer_id: The offer ID under the base plan (optional)

is_offer_personalized: Whether to enable personalized pricing (optional)

The replacement modes values are defined as:

Default behavior is WITH_TIME_PRORATION.

Example use of update_subscription:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var billing_client: BillingClient
func _ready():
    billing_client = BillingClient.new()
    billing_client.connected.connect(_on_connected) # No params
    billing_client.disconnected.connect(_on_disconnected) # No params
    billing_client.connect_error.connect(_on_connect_error) # response_code: int, debug_message: String
    billing_client.query_product_details_response.connect(_on_query_product_details_response) # response: Dictionary
    billing_client.query_purchases_response.connect(_on_query_purchases_response) # response: Dictionary
    billing_client.on_purchase_updated.connect(_on_purchase_updated) # response: Dictionary
    billing_client.consume_purchase_response.connect(_on_consume_purchase_response) # response: Dictionary
    billing_client.acknowledge_purchase_response.connect(_on_acknowledge_purchase_response) # response: Dictionary

    billing_client.start_connection()
```

Example 2 (typescript):
```typescript
# Matches BillingClient.ConnectionState in the Play Billing Library.
# Access in your script as: BillingClient.ConnectionState.CONNECTED
enum ConnectionState {
    DISCONNECTED, # This client was not yet connected to billing service or was already closed.
    CONNECTING, # This client is currently in process of connecting to billing service.
    CONNECTED, # This client is currently connected to billing service.
    CLOSED, # This client was already closed and shouldn't be used again.
}
```

Example 3 (go):
```go
func _on_connected():
  billing_client.query_product_details(["my_iap_item"], BillingClient.ProductType.INAPP) # BillingClient.ProductType.SUBS for subscriptions.

func _on_query_product_details_response(query_result: Dictionary):
    if query_result.response_code == BillingClient.BillingResponseCode.OK:
        print("Product details query success")
        for available_product in query_result.product_details:
            print(available_product)
    else:
        print("Product details query failed")
        print("response_code: ", query_result.response_code, "debug_message: ", query_result.debug_message)
```

Example 4 (go):
```go
func _query_purchases():
    billing_client.query_purchases(BillingClient.ProductType.INAPP) # Or BillingClient.ProductType.SUBS for subscriptions.

func _on_query_purchases_response(query_result: Dictionary):
    if query_result.response_code == BillingClient.BillingResponseCode.OK:
        print("Purchase query success")
        for purchase in query_result.purchases:
            _process_purchase(purchase)
    else:
        print("Purchase query failed")
        print("response_code: ", query_result.response_code, "debug_message: ", query_result.debug_message)
```

---

## Blender ESCN exporter

**URL:** https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/escn_exporter/index.html

**Contents:**
- Blender ESCN exporter

To export from Blender to Godot 4.x, use one of the available 3D formats.

The plugin Godot Blender Exporter is not maintained or supported in Godot 4.x. While not officially supported, the plugin may partially work for some Godot and Blender versions, particularly before Blender version 4.0. For complete docs on the Blender exporter, see the previous version of this page.

---

## CameraServer

**URL:** https://docs.godotengine.org/en/stable/classes/class_cameraserver.html

**Contents:**
- CameraServer
- Description
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Server keeping track of different cameras accessible in Godot.

The CameraServer keeps track of different cameras accessible in Godot. These are external cameras such as webcams or the cameras on your phone.

It is notably used to provide AR modules with a video feed from the camera.

Note: This class is currently only implemented on Linux, Android, macOS, and iOS. On other platforms no CameraFeeds will be available. To get a CameraFeed on iOS, the camera plugin from godot-ios-plugins is required.

add_feed(feed: CameraFeed)

remove_feed(feed: CameraFeed)

camera_feed_added(id: int) 

Emitted when a CameraFeed is added (e.g. a webcam is plugged in).

camera_feed_removed(id: int) 

Emitted when a CameraFeed is removed (e.g. a webcam is unplugged).

camera_feeds_updated() 

Emitted when camera feeds are updated.

FeedImage FEED_RGBA_IMAGE = 0

The RGBA camera image.

FeedImage FEED_YCBCR_IMAGE = 0

The YCbCr camera image.

FeedImage FEED_Y_IMAGE = 0

The Y component camera image.

FeedImage FEED_CBCR_IMAGE = 1

The CbCr component camera image.

bool monitoring_feeds = false 

void set_monitoring_feeds(value: bool)

bool is_monitoring_feeds()

If true, the server is actively monitoring available camera feeds.

This has a performance cost, so only set it to true when you're actively accessing the camera.

Note: After setting it to true, you can receive updated camera feeds through the camera_feeds_updated signal.

void add_feed(feed: CameraFeed) 

Adds the camera feed to the camera server.

Array[CameraFeed] feeds() 

Returns an array of CameraFeeds.

CameraFeed get_feed(index: int) 

Returns the CameraFeed corresponding to the camera with the given index.

int get_feed_count() 

Returns the number of CameraFeeds registered.

void remove_feed(feed: CameraFeed) 

Removes the specified camera feed.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    CameraServer.camera_feeds_updated.connect(_on_camera_feeds_updated)
    CameraServer.monitoring_feeds = true

func _on_camera_feeds_updated():
    var feeds = CameraServer.feeds()
```

Example 2 (gdscript):
```gdscript
public override void _Ready()
{
    CameraServer.CameraFeedsUpdated += OnCameraFeedsUpdated;
    CameraServer.MonitoringFeeds = true;
}

void OnCameraFeedsUpdated()
{
    var feeds = CameraServer.Feeds();
}
```

---

## Console support in Godot

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/consoles.html

**Contents:**
- Console support in Godot
- Console porting process
- Console publishing process
- Third-party support
- Middleware
- User-contributed notes

In order to develop for consoles in Godot, you need access to the console SDK and export templates for it. These export templates need to be developed either by yourself or someone hired to do it, or provided by a third-party company.

Currently, the only console Godot officially supports is Steam Deck (through the official Linux export templates).

The reasons other consoles are not officially supported are the risks of legal liability, disproportionate cost, and open source licensing issues. The reasons are explained in more detail in this article About Official Console Ports

As explained, however, it is possible to port your games to consoles thanks to services provided by third-party companies.

In practice, the process is quite similar to Unity and Unreal Engine. In other words, there is no engine that is legally allowed to distribute console export templates without requiring the user to prove that they are a licensed console developer.

Regardless of the engine used to create the game, the process to publish a game to a console platform is as follows:

Register a developer account on the console manufacturer's website, then sign NDAs and publishing contracts. This requires you to have a registered legal entity.

Gain access to the publishing platform by passing the acceptance process. This can take up to several months. Note that this step is significantly easier if an established publisher is backing your game. Nintendo is generally known to be more accepting of smaller developers, but this is not guaranteed.

Get access to developer tools and order a console specially made for developers (devkit). The cost of those devkits is confidential.

Port your game to the console platform or pay a company to do it.

To be published, your game needs to be rated in the regions you'd like to sell it in. For example, game ratings are handled by ESRB in North America, and PEGI in Europe. Indie developers can generally get a rating for cheaper compared to more established developers.

Due to the complexity of the process, many studios and developers prefer to outsource console porting.

You can read more about the console publishing process in this article: Godot and consoles, all you need to know

Console ports of Godot are offered by third-party companies (which have ported Godot on their own). Some of these companies also offer publishing of your games to various consoles.

The following is a list of some of the providers:

Lone Wolf Technology offers Switch and Playstation 4 porting and publishing of Godot games.

Pineapple Works offers Nintendo Switch 1 & 2, Xbox One & Xbox Series X/S, PlayStation 5 porting and publishing of Godot games (GDScript/C#).

RAWRLAB games offers Switch porting of Godot games.

mazette! games offers Switch, Xbox One and Xbox Series X/S porting and publishing of Godot games.

Olde Sküül offers Switch, Xbox One, Playstation 4 & Playstation 5 porting and publishing of Godot games.

Tuanisapps offers Switch porting and publishing of Godot games.

Seaven Studio offers Switch, Xbox One, Xbox Series, PlayStation 4 & PlayStation 5 porting of Godot games.

Sickhead Games offers console porting to Nintendo Switch, PlayStation 4, PlayStation 5, Xbox One, and Xbox Series X/S for Godot games.

If your company offers porting, or porting and publishing services for Godot games, feel free to contact the Godot Foundation to add your company to the list above.

Middleware ports are available through the console vendor's website. They provide you with a version of Godot that can natively run on the console. Typically, you do the actual work of adapting your game to the various consoles yourself. In other words, the middleware provided has ported Godot to the console, you just need to port your game, which is significantly less work in most cases.

W4 Games offers official middleware ports for Nintendo Switch, Xbox Series X/S, and Playstation 5.

Please read the User-contributed notes policy before submitting a comment.

---

## Custom HTML page for Web export

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/web/customizing_html5_shell.html

**Contents:**
- Custom HTML page for Web export
- Setup
- Starting the project
- Customizing the behavior
- Customizing the presentation
- Debugging
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

While Web export templates provide a default HTML page fully capable of launching the project without any further customization, it may be beneficial to create a custom HTML page. While the game itself cannot easily be directly controlled from the outside yet, such page allows to customize the initialization process for the engine.

Some use-cases where customizing the default page is useful include:

Loading files from a different directory than the page;

Loading a .zip file instead of a .pck file as the main pack;

Loading the engine from a different directory than the main pack file;

Adding a click-to-play button so that games can be started in the fullscreen mode;

Loading some extra files before the engine starts, making them available in the project file system as soon as possible;

Passing custom command line arguments, e.g. -s to start a MainLoop script.

The default HTML page is available in the Godot Engine repository at /misc/dist/html/full-size.html but the following template can be used as a much simpler example:

As shown by the example above, it is mostly a regular HTML document, with few placeholders which needs to be replaced during export, an html <canvas> element, and some simple JavaScript code that calls the Engine() class.

The only required placeholders are:

$GODOT_URL: The name of the main JavaScript file, which provides the Engine() class required to start the engine and that must be included in the HTML as a <script>. The name is generated from the Export Path during the export process.

$GODOT_CONFIG: A JavaScript object, containing the export options and can be later overridden. See EngineConfig for the full list of overrides.

The following optional placeholders will enable some extra features in your custom HTML template.

$GODOT_PROJECT_NAME: The project name as defined in the Name setting in Project Settings > Application > Config. It is a good idea to use it as a <title> in your template.

$GODOT_HEAD_INCLUDE: A custom string to include in the HTML document just before the end of the <head> tag. It is customized in the export options under the Html / Head Include section. While you fully control the HTML page you create, this variable can be useful for configuring parts of the HTML head element from the Godot Editor, e.g. for different Web export presets.

$GODOT_SPLASH: The path to the image used as the boot splash as defined in the Image setting in Project Settings > Application > Boot Splash.

$GODOT_SPLASH_COLOR The splash screen background color as defined in the BG Color setting in Project Settings > Application > Boot Splash, converted to a hex color code.

$GODOT_SPLASH_CLASSES: This placeholder provides a string of setting names and their values, which affect the splash screen. This string is meant to be used as a set of CSS class names, which allows styling the splash image based on the splash project settings. The following settings from Project Settings > Application > Boot Splash are provided, represented by the class names shown below depending on the setting's boolean value:

Show Image: show-image--true, show-image--false

Fullsize: fullsize--true, fullsize--false

Use Filter: use-filter--true, use-filter--false

When the custom page is ready, it can be selected in the export options under the Html / Custom Html Shell section.

To be able to start the game, you need to write a script that initializes the engine — the control code. This process consists of three steps, but as shown here, most of them can be skipped depending on how much customization is needed.

See the HTML5 shell class reference, for the full list of methods and options available.

First, the engine must be loaded, then it needs to be initialized, and after this the project can finally be started. You can perform every of these steps manually and with great control. However, in the simplest case all you need to do is to create an instance of the Engine() class with the exported configuration, and then call the engine.startGame method optionally overriding any EngineConfig parameters.

This snippet of code automatically loads and initializes the engine before starting the game. It uses the given configuration to load the engine. The engine.startGame method is asynchronous and returns a Promise. This allows your control code to track if the game was loaded correctly without blocking execution or relying on polling.

In case your project needs to have special control over the start arguments and dependency files, the engine.start method can be used instead. Note, that this method do not automatically preload the pck file, so you will probably want to manually preload it (and any other extra file) via the engine.preloadFile method.

Optionally, you can also manually engine.init to perform specific actions after the module initialization, but before the engine starts.

This process is a bit more complex, but gives you full control over the engine startup process.

To load the engine manually the Engine.load() static method must be called. As this method is static, multiple engine instances can be spawned if the share the same wasm.

Multiple instances cannot be spawned by default, as the engine is immediately unloaded after it is initialized. To prevent this from happening see the unloadAfterInit override option. It is still possible to unload the engine manually afterwards by calling the Engine.unload() static method. Unloading the engine frees browser memory by unloading files that are no longer needed once the instance is initialized.

In the Web environment several methods can be used to guarantee that the game will work as intended.

If you target a specific version of WebGL, or just want to check if WebGL is available at all, you can call the Engine.isWebGLAvailable() method. It optionally takes an argument that allows to test for a specific major version of WebGL.

As the real executable file does not exist in the Web environment, the engine only stores a virtual filename formed from the base name of loaded engine files. This value affects the output of the OS.get_executable_path() method and defines the name of the automatically started main pack. The executable override option can be used to override this value.

Several configuration options can be used to further customize the look and behavior of the game on your page.

By default, the first canvas element on the page is used for rendering. To use a different canvas element the canvas override option can be used. It requires a reference to the DOM element itself.

The way the engine resize the canvas can be configured via the canvasResizePolicy override option.

If your game takes some time to load, it may be useful to display a custom loading UI which tracks the progress. This can be achieved with the onProgress callback option, which allows to set up a callback function that will be called regularly as the engine loads new bytes.

Be aware that in some cases total can be 0. This means that it cannot be calculated.

If your game supports multiple languages, the locale override option can be used to force a specific locale, provided you have a valid language code string. It may be good to use server-side logic to determine which languages a user may prefer. This way the language code can be taken from the Accept-Language HTTP header, or determined by a GeoIP service.

To debug exported projects, it may be useful to read the standard output and error streams generated by the engine. This is similar to the output shown in the editor console window. By default, standard console.log and console.warn are used for the output and error streams respectively. This behavior can be customized by setting your own functions to handle messages.

Use the onPrint override option to set a callback function for the output stream, and the onPrintError override option to set a callback function for the error stream.

When handling the engine output, keep in mind that it may not be desirable to print it out in the finished product.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (html):
```html
<!DOCTYPE html>
<html>
    <head>
        <title>My Template</title>
        <meta charset="UTF-8">
    </head>
    <body>
        <canvas id="canvas"></canvas>
        <script src="$GODOT_URL"></script>
        <script>
            var engine = new Engine($GODOT_CONFIG);
            engine.startGame();
        </script>
    </body>
</html>
```

Example 2 (javascript):
```javascript
const engine = new Engine($GODOT_CONFIG);
engine.startGame({
    /* optional override configuration, eg. */
    // unloadAfterInit: false,
    // canvasResizePolicy: 0,
    // ...
});
```

Example 3 (javascript):
```javascript
const myWasm = 'mygame.wasm';
const myPck = 'mygame.pck';
const engine = new Engine();
Promise.all([
    // Load and init the engine
    engine.init(myWasm),
    // And the pck concurrently
    engine.preloadFile(myPck),
]).then(() => {
    // Now start the engine.
    return engine.start({ args: ['--main-pack', myPck] });
}).then(() => {
    console.log('Engine has started!');
});
```

Example 4 (css):
```css
const canvasElement = document.querySelector("#my-canvas-element");
engine.startGame({ canvas: canvasElement });
```

---

## Exporting for Android

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_android.html

**Contents:**
- Exporting for Android
- Install OpenJDK 17
- Download the Android SDK
- Setting it up in Godot
- Providing launcher icons
- Exporting for Google Play Store
- Optimizing the file size
- Environment variables
- Export options
- User-contributed notes

This page describes how to export a Godot project to Android. If you're looking to compile export template binaries from source instead, read Compiling for Android.

Exporting for Android has fewer requirements than compiling Godot for Android. The following steps detail what is needed to set up the Android SDK and the engine.

Projects written in C# can be exported to Android as of Godot 4.2, but support is experimental and some limitations apply.

Download and install OpenJDK 17.

Higher versions of the JDK are also supported, but we recommend using JDK 17 for optimal compatibility and stability.

Download and install the Android SDK.

You can install the Android SDK using Android Studio Iguana (version 2023.2.1) or later.

Run it once to complete the SDK setup using these instructions.

Ensure that the required packages are installed as well.

Android SDK Platform-Tools version 35.0.0 or later

Android SDK Build-Tools version 35.0.0

Android SDK Platform 35

Android SDK Command-line Tools (latest)

Ensure that the NDK and CMake are installed and configured.

CMake version 3.10.2.4988404

NDK version r28b (28.1.13356709)

Alternatively, you can install the Android SDK with the sdkmanager command line tool.

Install the command line tools package using these instructions.

Once the command line tools are installed, run the following sdkmanager command to complete the setup process:

If you are using Linux, do not use an Android SDK provided by your distribution's repositories as it will often be outdated.

Enter the Editor Settings screen (under the Godot tab for macOS, or the Editor tab for other platforms). This screen contains the editor settings for the user account in the computer (it's independent of the project).

Scroll down to the section where the Android settings are located:

In that screen, 2 paths need to be set:

Java SDK Path should be the location where OpenJDK 17 was installed.

Android Sdk Path should be the location where the Android SDK was installed. - For example %LOCALAPPDATA%\Android\Sdk\ on Windows or /Users/$USER/Library/Android/sdk/ on macOS.

Once that is configured, everything is ready to export to Android!

If you get an error saying "Could not install to device.", make sure you do not have an application with the same Android package name already installed on the device (but signed with a different key).

If you have an application with the same Android package name but a different signing key already installed on the device, you must remove the application in question from the Android device before exporting to Android again.

Launcher icons are used by Android launcher apps to represent your application to users. Godot only requires high-resolution icons (for xxxhdpi density screens) and will automatically generate lower-resolution variants.

There are three types of icons:

Main Icon: The "classic" icon. This will be used on all Android versions up to Android 8 (Oreo), exclusive. Must be at least 192×192 px.

Adaptive Icons: Starting from Android 8 (inclusive), Adaptive Icons were introduced. Applications will need to include separate background and foreground icons to have a native look. The user's launcher application will control the icon's animation and masking. Must be at least 432×432 px.

Themed Icons (optional): Starting from Android 13 (inclusive), Themed Icons were introduced. Applications will need to include a monochrome icon to enable this feature. The user's launcher application will control the icon's theme. Must be at least 432×432 px.

It's important to adhere to some rules when designing adaptive icons. Google Design has provided a nice article that helps to understand those rules and some of the capabilities of adaptive icons.

The most important adaptive icon design rule is to have your icon critical elements inside the safe zone: a centered circle with a diameter of 66dp (264 pixels on xxxhdpi) to avoid being clipped by the launcher.

If you don't provide the requested icons (except for Monochrome), Godot will replace them using a fallback chain, trying the next in line when the current one fails:

Main Icon: Provided main icon -> Project icon -> Default Godot main icon.

Adaptive Icon Foreground: Provided foreground icon -> Provided main icon -> Project icon -> Default Godot foreground icon.

Adaptive Icon Background: Provided background icon -> Default Godot background icon.

It's highly recommended to provide all the requested icons with their specified resolutions. This way, your application will look great on all Android devices and versions.

All new apps uploaded to Google Play after August 2021 must be an AAB (Android App Bundle) file.

Uploading an AAB or APK to Google's Play Store requires you to sign using a non-debug keystore file; such a file can be generated like this:

This keystore and key are used to verify your developer identity, remember the password and keep it in a safe place! It is suggested to use only upper and lowercase letters and numbers. Special characters may cause errors. Use Google's Android Developer guides to learn more about app signing.

Now fill in the following forms in your Android Export Presets:

Release: Enter the path to the keystore file you just generated.

Release User: Replace with the key alias.

Release Password: Key password. Note that the keystore password and the key password currently have to be the same.

Don't forget to uncheck the Export With Debug checkbox while exporting.

If you're working with APKs and not AABs, by default, the APK will contain native libraries for both ARMv7 and ARMv8 architectures. This increases its size significantly. To create a smaller file, uncheck either Armeabi-v 7a or Arm 64 -v 8a in your project's Android export preset. This will create an APK that only contains a library for a single architecture. Note that applications targeting ARMv7 can also run on ARMv8 devices, but the opposite is not true. The reason you don't do this to save space with AABs is that Google automatically splits up the AAB on their backend, so the user only downloads what they need.

You can optimize the size further by compiling an Android export template with only the features you need. See Optimizing a build for size for more information.

You can use the following environment variables to set export options outside of the editor. During the export process, these override the values that you set in the export menu.

Encryption / Encryption Key

GODOT_SCRIPT_ENCRYPTION_KEY

Options / Keystore / Debug

GODOT_ANDROID_KEYSTORE_DEBUG_PATH

Options / Keystore / Debug User

GODOT_ANDROID_KEYSTORE_DEBUG_USER

Options / Keystore / Debug Password

GODOT_ANDROID_KEYSTORE_DEBUG_PASSWORD

Options / Keystore / Release

GODOT_ANDROID_KEYSTORE_RELEASE_PATH

Options / Keystore / Release User

GODOT_ANDROID_KEYSTORE_RELEASE_USER

Options / Keystore / Release Password

GODOT_ANDROID_KEYSTORE_RELEASE_PASSWORD

You can find a full list of export options available in the EditorExportPlatformAndroid class reference.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (typescript):
```typescript
sdkmanager --sdk_root=<android_sdk_path> "platform-tools" "build-tools;35.0.0" "platforms;android-35" "cmdline-tools;latest" "cmake;3.10.2.4988404" "ndk;28.1.13356709"
```

Example 2 (unknown):
```unknown
keytool -v -genkey -keystore mygame.keystore -alias mygame -keyalg RSA -validity 10000
```

---

## Exporting for dedicated servers

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_dedicated_servers.html

**Contents:**
- Exporting for dedicated servers
- Editor versus export template
- Export approaches
- Exporting a project for a dedicated server
- Starting the dedicated server
- Next steps
- User-contributed notes

If you want to run a dedicated server for your project on a machine that doesn't have a GPU or display server available, you'll need to run Godot with the headless display server and Dummy audio driver.

Since Godot 4.0, this can be done by running a Godot binary on any platform with the --headless command line argument, or running a project exported as dedicated server. You do not need to use a specialized server binary anymore, unlike Godot 3.x.

It is possible to use either an editor or export template (debug or release) binary in headless mode. Which one you should use depends on your use case:

Export template: Use this one for running dedicated servers. It does not contain editor functionality, and is therefore smaller and more optimized.

Editor: This binary contains editor functionality and is intended to be used for exporting projects. This binary can be used to run dedicated servers, but it's not recommended as it's larger and less optimized.

There are two ways to export a project for a server:

Create a separate export preset for the platform that will host the server, then export your project as usual.

Export a PCK file only, preferably for the platform that matches the platform that will host the server. Place this PCK file in the same folder as an export template binary, rename the binary to have the same name as the PCK (minus the file extension), then run the binary.

Both methods should result in identical output. The rest of the page will focus on the first approach.

See Exporting projects for more information.

If you export a project as usual when targeting a server, you will notice that the PCK file is just as large as for the client. This is because it includes all resources, including those the server doesn't need (such as texture data). Additionally, headless mode won't be automatically used; the user will have to specify --headless to make sure no window spawns.

Many resources such as textures can be stripped from the PCK file to greatly reduce its size. Godot offers a way to do this for textures and materials in a way that preserves references in scene or resource files (built-in or external).

To begin doing so, make sure you have a dedicated export preset for your server, then select it, go to its Resources tab and change its export mode:

Choosing the Export as dedicated server export mode in the export preset

When this export mode is chosen, the dedicated_server feature tag is automatically added to the exported project.

If you do not wish to use this export mode but still want the feature tag, you can write the name dedicated_server in the Features tab of the export preset. This will also force --headless when running the exported project.

After selecting this export mode, you will be presented with a list of resources in the project:

Choosing resources to keep, keep with stripped visuals or remove

Ticking a box allows you to override options for the specified file or folder. Checking boxes does not affect which files are exported; this is done by the options selected for each checkbox instead.

Files within a checked folder will automatically use the parent's option by default, which is indicated by the (Inherited) suffix for the option name (and the option name being grayed out). To change the option for a file whose option is currently inherited, you must tick the box next to it first.

Strip Visuals: Export this resource, with visual files (textures and materials) replaced by placeholder classes. Placeholder classes store the image size (as it's sometimes used to position elements in a 2D scene), but nothing else.

Keep: Export this resource as usual, with visual files intact.

Remove: The file is not included in the PCK. This is useful to ignore scenes and resources that only the client needs. If you do so, make sure the server doesn't reference these client-only scenes and resources in any way.

The general recommendation is to use Strip Visuals whenever possible, unless the server needs to access image data such as pixels' colors. For example, if your server generates collision data based on an image's contents, you need to use Keep for that particular image.

To check the file structure of your exported PCK, use the Export PCK/ZIP... button with a .zip file extension, then open the resulting ZIP file in a file manager.

Be careful when using the Remove mode, as scenes/resources that reference a removed file will no longer be able to load successfully.

If you wish to remove specific resources but make the scenes still be able to load without them, you'll have to remove the reference in the scene file and load the files to the nodes' properties using load() in a script. This approach can be used to strip resources that Godot doesn't support replacing with placeholders yet, such as audio.

Removing textures is often what makes the greatest impact on the PCK size, so it is recommended to stick with Strip Visuals at first.

With the above options used, a PCK for the client (which exports all resources normally) will look as follows:

The PCK's file structure for the server will look as follows:

If both your client and server are part of the same Godot project, you will have to add a way to start the server directly using a command-line argument.

If you exported the project using the Export as dedicated server export mode (or have added dedicated_server as a custom feature tag), you can use the dedicated_server feature tag to detect whether a dedicated server PCK is being used:

If you also wish to host a server when using the built-in --headless command line argument, this can be done by adding the following code snippet in your main scene (or an autoload)'s _ready() method:

If you wish to use a custom command line argument, this can be done by adding the following code snippet in your main scene (or an autoload)'s _ready() method:

It's a good idea to add at least one of the above command-line arguments to start a server, as it can be used to test server functionality from the command line without having to export the project.

If your client and server are separate Godot projects, your server should most likely be configured in a way where running the main scene starts a server automatically.

On Linux, to make your dedicated server restart after a crash or system reboot, you can create a systemd service. This also lets you view server logs in a more convenient fashion, with automatic log rotation provided by systemd. When making your project hostable as a systemd service, you should also enable the application/run/flush_stdout_on_print project setting. This way, journald (the systemd logging service) can collect logs while the process is running.

If you have experience with containers, you could also look into wrapping your dedicated server in a Docker container. This way, it can be used more easily in an automatic scaling setup (which is outside the scope of this tutorial).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
.
├── .godot
│   ├── exported
│   │   └── 133200997
│   │       └── export-78c237d4bfdb4e1d02e0b5f38ddfd8bd-scene.scn
│   ├── global_script_class_cache.cfg
│   ├── imported
│   │   ├── map_data.png-ce840618f399a990343bfc7298195a13.ctex
│   │   ├── music.ogg-fa883da45ae49695a3d022f64e60aee2.oggvorbisstr
│   │   └── sprite.png-7958af25f91bb9dbae43f35388f8e840.ctex
│   └── uid_cache.bin
├── client
│   ├── music.ogg.import
│   └── sprite.png.import
├── server
│   └── map_data.png.import
├── test
│   └── scene.gd
└── unused
│   └── development_test.gd
├── project.binary
├── scene.gd
├── scene.tscn.remap
```

Example 2 (unknown):
```unknown
.
├── .godot
│   ├── exported
│   │   └── 3400186661
│   │       ├── export-78c237d4bfdb4e1d02e0b5f38ddfd8bd-scene.scn
│   │       ├── export-7958af25f91bb9dbae43f35388f8e840-sprite.res  # Placeholder texture
│   │       └── export-fa883da45ae49695a3d022f64e60aee2-music.res
│   ├── global_script_class_cache.cfg
│   ├── imported
│   │   └── map_data.png-ce840618f399a990343bfc7298195a13.ctex
│   └── uid_cache.bin
├── client
│   ├── music.ogg.import
│   └── sprite.png.import  # Points to placeholder texture
└── server
│   └── map_data.png.import
├── project.binary
├── scene.gd
├── scene.tscn.remap
```

Example 3 (markdown):
```markdown
# Note: Feature tags are case-sensitive.
if OS.has_feature("dedicated_server"):
    # Run your server startup code here...
    pass
```

Example 4 (json):
```json
// Note: Feature tags are case-sensitive.
if (OS.HasFeature("dedicated_server"))
{
    // Run your server startup code here...
}
```

---

## Exporting for iOS

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_ios.html

**Contents:**
- Exporting for iOS
- Requirements
- Export a Godot project to Xcode
- Active development considerations
  - Steps to link a Godot project folder to Xcode
- Plugins for iOS
- Environment variables
- Troubleshooting
  - xcode-select points at wrong SDK location
- Export options

This page describes how to export a Godot project to iOS. If you're looking to compile export template binaries from source instead, read Compiling for iOS.

These are the steps to load a Godot project in Xcode. This allows you to build and deploy to an iOS device, build a release for the App Store, and do everything else you can normally do with Xcode.

Projects written in C# can be exported to iOS as of Godot 4.2, but support is experimental and some limitations apply.

You must export for iOS from a computer running macOS with Xcode installed.

Download the Godot export templates. Use the Godot menu: Editor > Manage Export Templates

In the Godot editor, open the Export window from the Project menu. When the Export window opens, click Add.. and select iOS.

The App Store Team ID and (Bundle) Identifier options in the Application category are required. Leaving them blank will cause the exporter to throw an error.

After you click Export Project, there are still two important options left:

Path is an empty folder that will contain the exported Xcode project files.

File will be the name of the Xcode project and several project specific files and directories.

This tutorial uses exported_xcode_project_name, but you will use your project's name. When you see exported_xcode_project_name in the following steps, replace it with the name you used instead.

Avoid using spaces when you choose your exported_xcode_project_name as this can lead to corruption in your XCode project file.

When the export completes, the output folder should look like this:

Exporting for the iOS simulator is currently not supported as per GH-102149.

Apple Silicon Macs can run iOS apps natively, so you can run exported iOS projects directly on an Apple Silicon Mac without needing the iOS simulator.

Opening exported_xcode_project_name.xcodeproj lets you build and deploy like any other iOS app.

The above method creates an exported project that you can build for release, but you have to re-export every time you make a change in Godot.

While developing, you can speed this process up by linking your Godot project files directly into your app.

In the following example:

exported_xcode_project_name is the name of the exported iOS application (as above).

godot_project_to_export is the name of the Godot project.

godot_project_to_export must not be the same as exported_xcode_project_name to prevent signing issues in Xcode.

Start from an exported iOS project (follow the steps above).

In Finder, drag the Godot project folder into the Xcode file browser.

In the dialog, make sure to select Action: Reference files in place and Groups: Create folders. Uncheck Targets: exported_xcode_project_name.

See the godot_project_to_export folder in the Xcode file browser.

Select the godot project in the Project navigator. Then on the other side of the XCode window, in the File Inspector, make these selections:

Location: Relative to Project

Build Rules: Apply Once to Folder

add your project to Target Membership

Delete exported_xcode_project_name.pck from the Xcode project in the project navigator.

8. Open exported_xcode_project_name-Info.plist and add a string property named godot_path (this is the real key name) with a value godot_project_to_export (this is the name of your project)

That's it! You can now edit your project in the Godot editor and build it in Xcode when you want to run it on a device.

Special iOS plugins can be used in Godot. Check out the Plugins for iOS page.

You can use the following environment variables to set export options outside of the editor. During the export process, these override the values that you set in the export menu.

Encryption / Encryption Key

GODOT_SCRIPT_ENCRYPTION_KEY

Options / Application / Provisioning Profile UUID Debug

GODOT_IOS_PROVISIONING_PROFILE_UUID_DEBUG

Options / Application / Provisioning Profile UUID Release

GODOT_IOS_PROVISIONING_PROFILE_UUID_RELEASE

xcode-select is a tool that comes with Xcode and among other things points at iOS SDKs on your Mac. If you have Xcode installed, opened it, agreed to the license agreement, and installed the command line tools, xcode-select should point at the right location for the iPhone SDK. If it somehow doesn't, Godot will fail exporting to iOS with an error that may look like this:

In this case, Godot is trying to find the Platforms folder containing the iPhone SDK inside the /Library/Developer/CommandLineTools/ folder, but the Platforms folder with the iPhone SDK is actually located under /Applications/Xcode.app/Contents/Developer. To verify this, you can open up Terminal and run the following command to see what xcode-select points at:

To fix xcode-select pointing at a wrong location, enter this command in Terminal:

After running this command, Godot should be able to successfully export to iOS.

You can find a full list of export options available in the EditorExportPlatformIOS class reference.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (jsx):
```jsx
MSB3073: The command ""clang" <LOTS OF PATHS AND COMMAND LINE ARGUMENTS HERE>
"/Library/Developer/CommandLineTools/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk"" exited with code 1.
```

Example 2 (sql):
```sql
xcode-select -p
```

Example 3 (sql):
```sql
sudo xcode-select -switch /Applications/Xcode.app
```

---

## Exporting for Linux

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_linux.html

**Contents:**
- Exporting for Linux
- Environment variables
- Export options
- User-contributed notes

This page describes how to export a Godot project to Linux. If you're looking to compile editor or export template binaries from source instead, read Compiling for Linux, *BSD.

The simplest way to distribute a game for PC is to copy the executable (godot), compress the folder and send it to someone else. However, this is often not desired.

Godot offers a more elegant approach for PC distribution when using the export system. When exporting for Linux, the exporter takes all the project files and creates a data.pck file. This file is bundled with a specially optimized binary that is smaller, faster and does not contain the editor and debugger.

You can use the following environment variables to set export options outside of the editor. During the export process, these override the values that you set in the export menu.

Encryption / Encryption Key

GODOT_SCRIPT_ENCRYPTION_KEY

You can find a full list of export options available in the EditorExportPlatformLinuxBSD class reference.

Please read the User-contributed notes policy before submitting a comment.

---

## Exporting for macOS

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_macos.html

**Contents:**
- Exporting for macOS
- Requirements
- Code signing and notarization
  - If you have an Apple Developer ID Certificate and exporting from macOS
    - To sign exported app
    - To notarize exported app
  - If you have an Apple Developer ID Certificate and exporting from Linux or Windows
    - To sign exported app
    - To notarize exported app
  - If you do not have an Apple Developer ID Certificate

This page describes how to export a Godot project to macOS. If you're looking to compile editor or export template binaries from source instead, read Compiling for macOS.

macOS apps exported with the official export templates are exported as a single "Universal 2" binary .app bundle, a folder with a specific structure which stores the executable, libraries and all the project files. This bundle can be exported as is, packed in a ZIP archive, or packed in a DMG disk image (only supported when exporting from macOS). Universal binaries for macOS support both Intel x86_64 and ARM64 (Apple Silicon) architectures.

Due to file system limitations, .app bundles exported from Windows lack the executable flag and won't run on macOS. Projects exported as .zip are not affected by this issue. To run .app bundles exported from Windows on macOS, transfer the .app to a device running macOS or Linux and use the chmod +x {executable_name} terminal command to add the executable permission. The main executable located in the Contents/MacOS/ subfolder, as well as optional helper executables in the Contents/Helpers/ subfolder, should have the executable permission for the .app bundle to be valid.

Download the Godot export templates. Use the Godot menu: Editor > Manage Export Templates.

A valid and unique Bundle identifier should be set in the Application section of the export options.

Projects exported without code signing and notarization will be blocked by Gatekeeper if they are downloaded from unknown sources, see the Running Godot apps on macOS page for more information.

By default, macOS will run only applications that are signed and notarized. If you use any other signing configuration, see Running Godot apps on macOS for workarounds.

To notarize an app, you must have a valid Apple Developer ID Certificate.

Install Xcode command line tools and open Xcode at least once or run the sudo xcodebuild -license accept command to accept license agreement.

Select Xcode codesign in the Code Signing > Codesign option.

Set valid Apple ID certificate identity (certificate "Common Name") in the Code Signing > Identity section.

Select Xcode altool in the Notarization > Notarization option.

Disable the Debugging entitlement.

Set valid Apple ID login / app. specific password or App Store Connect API UUID / Key in the Notarization section.

You can use the xcrun notarytool history command to check notarization status and use the xcrun notarytool log {ID} command to download the notarization log.

If you encounter notarization issues, see Resolving common notarization issues for more info.

After notarization is completed, staple the ticket to the exported project.

Install PyOxidizer rcodesign, and configure the path to rcodesign in the Editor Settings > Export > macOS > rcodesign.

Select PyOxidizer rcodesign in the Code Signing > Codesign option.

Set valid Apple ID PKCS #12 certificate file and password in the Code Signing section.

Select PyOxidizer rcodesign in the Notarization > Notarization option.

Disable the Debugging entitlement.

Set valid App Store Connect API UUID / Key in the Notarization section.

You can use the rcodesign notary-log command to check notarization status.

After notarization is completed, use the rcodesign staple command to staple the ticket to the exported project.

Select Built-in (ad-hoc only) in the Code Signing > Codesign option.

Select Disabled in the Notarization > Notarization option.

In this case Godot will use an ad-hoc signature, which will make running an exported app easier for the end users, see the Running Godot apps on macOS page for more information.

Tool to use for code signing.

The "Full Name" or "Common Name" of the signing identity, store in the macOS keychain. [1]

The PKCS #12 certificate file. [2]

Password for the certificate file. [2]

Array of command line arguments passed to the code signing tool.

This option is visible only when signing with Xcode codesign.

These options are visible only when signing with PyOxidizer rcodesign.

Tool to use for notarization.

Apple ID account name (email address). [3]

Apple ID app-specific password. See Using app-specific passwords to enable two-factor authentication and create app password. [3]

Team ID ("Organization Unit"), if your Apple ID belongs to multiple teams (optional). [3]

Apple App Store Connect API issuer UUID.

Apple App Store Connect API key.

You should set either Apple ID Name/Password or App Store Connect API UUID/Key.

These options are visible only when notarizing with Xcode altool.

See Notarizing macOS Software Before Distribution for more info.

Hardened Runtime entitlements manage security options and resource access policy. See Hardened Runtime for more info.

Allow JIT Code Execution [4]

Allows creating writable and executable memory for JIT code. If you are using add-ons with dynamic or self-modifying native code, enable them according to the add-on documentation.

Allow Unsigned Executable Memory [4]

Allows creating writable and executable memory without JIT restrictions. If you are using add-ons with dynamic or self-modifying native code, enable them according to the add-on documentation.

Allow DYLD Environment Variables [4]

Allows app to uss dynamic linker environment variables to inject code. If you are using add-ons with dynamic or self-modifying native code, enable them according to the add-on documentation.

Disable Library Validation

Allows app to load arbitrary libraries and frameworks. Enable it if you are using GDExtension add-ons or ad-hoc signing, or want to support user-provided external add-ons.

Enable if you need to use the microphone or other audio input sources, if it's enabled you should also provide usage message in the privacy/microphone_usage_description option.

Enable if you need to use the camera, if it's enabled you should also provide usage message in the privacy/camera_usage_description option.

Enable if you need to use location information from Location Services, if it's enabled you should also provide usage message in the privacy/location_usage_description option.

[5] Enable to allow access contacts in the user's address book, if it's enabled you should also provide usage message in the privacy/address_book_usage_description option.

[5] Enable to allow access to the user's calendar, if it's enabled you should also provide usage message in the privacy/calendar_usage_description option.

[5] Enable to allow access to the user's Photos library, if it's enabled you should also provide usage message in the privacy/photos_library_usage_description option.

[5] Enable to allow app to send Apple events to other apps.

[6] You can temporarily enable this entitlement to use native debugger (GDB, LLDB) with the exported app. This entitlement should be disabled for production export.

The Allow JIT Code Execution, Allow Unsigned Executable Memory and Allow DYLD Environment Variables entitlements are always enabled for the Godot Mono exports, and are not visible in the export options.

These features aren't supported by Godot out of the box, enable them only if you are using add-ons which require them.

To notarize an app, you must disable the Debugging entitlement.

The App Sandbox restricts access to user data, networking and devices. Sandboxed apps can't access most of the file system, can't use custom file dialogs and execute binaries (using OS.execute and OS.create_process) outside the .app bundle. See App Sandbox for more info.

To distribute an app through the App Store, you must enable the App Sandbox.

Enable to allow app to listen for incoming network connections.

Enable to allow app to establish outgoing network connections.

Enable to allow app to interact with USB devices. This entitlement is required to use wired controllers.

Enable to allow app to interact with Bluetooth devices. This entitlement is required to use wireless controllers.

Allows read or write access to the user's "Downloads" folder.

Allows read or write access to the user's "Pictures" folder.

Allows read or write access to the user's "Music" folder.

Allows read or write access to the user's "Movies" folder.

Files User Selected [7]

Allows read or write access to arbitrary folder. To gain access, a folder must be selected from the native file dialog by the user.

List of helper executables to embedded to the app bundle. Sandboxed app are limited to execute only these executable.

You can optionally provide usage messages for various folders in the privacy/*_folder_usage_description options.

You can override default entitlements by selecting custom entitlements file, in this case all other entitlement are ignored.

You can use the following environment variables to set export options outside of the editor. During the export process, these override the values that you set in the export menu.

Encryption / Encryption Key

GODOT_SCRIPT_ENCRYPTION_KEY

Options / Codesign / Certificate File

GODOT_MACOS_CODESIGN_CERTIFICATE_FILE

Options / Codesign / Certificate Password

GODOT_MACOS_CODESIGN_CERTIFICATE_PASSWORD

Options / Codesign / Provisioning Profile

GODOT_MACOS_CODESIGN_PROVISIONING_PROFILE

Options / Notarization / API UUID

GODOT_MACOS_NOTARIZATION_API_UUID

Options / Notarization / API Key

GODOT_MACOS_NOTARIZATION_API_KEY

Options / Notarization / API Key ID

GODOT_MACOS_NOTARIZATION_API_KEY_ID

Options / Notarization / Apple ID Name

GODOT_MACOS_NOTARIZATION_APPLE_ID_NAME

Options / Notarization / Apple ID Password

GODOT_MACOS_NOTARIZATION_APPLE_ID_PASSWORD

You can find a full list of export options available in the EditorExportPlatformMacOS class reference.

Please read the User-contributed notes policy before submitting a comment.

---

## Exporting for the Web

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_web.html

**Contents:**
- Exporting for the Web
- Export file name
- WebGL version
- Mobile considerations
- Audio playback
- Export options
  - Thread and extension support
  - Exporting as a Progressive Web App (PWA)
- Limitations
  - Using cookies for data persistence

This page describes how to export a Godot project to HTML5. If you're looking to compile editor or export template binaries from source instead, read Compiling for the Web.

HTML5 export allows publishing games made in Godot Engine to the browser. This requires support for WebAssembly and WebGL 2.0 in the user's browser.

Projects written in C# using Godot 4 currently cannot be exported to the web. See this blog post for more information.

To use C# on web platforms, use Godot 3 instead.

Use the browser-integrated developer console, usually opened with F12 or Ctrl + Shift + I (Cmd + Option + I on macOS), to view debug information like JavaScript, engine, and WebGL errors.

If the shortcut doesn't work, it's because Godot actually captures the input. You can still open the developer console by accessing the browser's menu.

Due to security concerns with SharedArrayBuffer due to various exploits, the use of multiple threads for the Web platform has multiple drawbacks, including requiring specific server-side headers and complete cross-origin isolation (meaning no ads, nor third-party integrations on the website hosting your game).

Since Godot 4.3, Godot supports exporting your game on a single thread, which solves this issue. While it has some drawbacks on its own (it cannot use threads, and is not as performant as the multi-threaded export), it doesn't require as much overhead to install. It is also more compatible overall with stores like itch.io or Web publishers like Poki or CrazyGames. The single-threaded export works very well on macOS and iOS too, where it always had compatibility issues with multiple threads exports.

For these reasons, it is the preferred and now default way to export your games on the Web.

For more information, see this blog post about single-threaded Web export.

See the list of open issues on GitHub related to the web export for a list of known bugs.

We suggest users to export their Web projects with index.html as the file name. index.html is usually the default file loaded by web servers when accessing the parent directory, usually hiding the name of that file.

The Godot 4 Web export expects some files to be named the same name as the one set in the initial export. Some issues could occur if some exported files are renamed, including the main HTML file.

Godot 4.0 and later can only target WebGL 2.0 (using the Compatibility rendering method). Forward+/Mobile are not supported on the web platform, as these rendering methods are designed around modern low-level graphics APIs. Godot currently does not support WebGPU, which is a prerequisite for allowing Forward+/Mobile to run on the web platform.

See Can I use WebGL 2.0 for a list of browser versions supporting WebGL 2.0. Note that Safari has several issues with WebGL 2.0 support that other browsers don't have, so we recommend using a Chromium-based browser or Firefox if possible.

The Web export can run on mobile platforms with some caveats. While native Android and iOS exports will always perform better by a significant margin, the Web export allows people to run your project without going through app stores.

Remember that CPU and GPU performance is at a premium when running on mobile devices. This is even more the case when running a project exported to Web (as it's WebAssembly instead of native code). See Performance section of the documentation for advice on optimizing your project. If your project runs on platforms other than Web, you can use Feature tags to apply low-end-oriented settings when running the project exported to Web.

To speed up loading times on mobile devices, you should also compile an optimized export template with unused features disabled. Depending on the features used by your project, this can reduce the size of the WebAssembly payload significantly, making it faster to download and initialize (even when cached).

Since Godot 4.3, audio playback is done using the Web Audio API on the web platform. This Sample playback mode allows for low latency even when the project is exported without thread support, but it has several limitations:

AudioEffects are not supported.

Reverberation and doppler effects are not supported.

Procedural audio generation is not supported.

Positional audio may not always work correctly depending on the node's properties.

To use Godot's own audio playback system on the web platform, you can change the default playback mode using the Audio > General > Default Playback Type.web project setting, or change the Playback Type property to Stream on an AudioStreamPlayer, AudioStreamPlayer2D or AudioStreamPlayer3D node. This leads to increased latency (especially when thread support is disabled), but it allows the full suite of Godot's audio features to work.

If a runnable web export template is available, a button appears between the Stop scene and Play edited Scene buttons in the editor to quickly open the game in the default browser for testing.

If your project uses GDExtension, Extension Support needs to be enabled.

If you plan to use VRAM compression make sure that VRAM Texture Compression is enabled for the targeted platforms (enabling both For Desktop and For Mobile will result in a bigger, but more compatible export).

If a path to a Custom HTML shell file is given, it will be used instead of the default HTML page. See Custom HTML page for Web export.

Head Include is appended into the <head> element of the generated HTML page. This allows to, for example, load webfonts and third-party JavaScript APIs, include CSS, or run JavaScript code.

The window size will automatically match the browser window size by default. If you want to use a fixed size instead regardless of the browser window size, change Canvas Resize Policy to None. This allows controlling the window size with custom JavaScript code in the HTML shell. You can also set it to Project to make it behave closer to a native export, according to the project settings.

Each project must generate their own HTML file. On export, several text placeholders are replaced in the generated HTML file specifically for the given export options. Any direct modifications to that HTML file will be lost in future exports. To customize the generated file, use the Custom HTML shell option.

If Thread Support is enabled, the exported project will be able to make use of multithreading to improve performance. This also allows for low-latency audio playback when the playback type is set to Stream (instead of the default Sample that is used in web exports). Enabling this feature requires the use of cross-origin isolation headers, which are described in the Serving the files section below.

If Extensions Support is enabled, GDExtensions will be able to be loaded. Note that GDExtensions still need to be specifically compiled for the web platform to work. Like thread support, enabling this feature requires the use of cross-origin isolation headers.

If Progressive Web App > Enable is enabled, it will have several effects:

Configure high-resolution icons, a display mode and screen orientation. These are configured at the end of the Progressive Web App section in the export options. These options are used if the user adds the project to their device's homescreen, which is common on mobile platforms. This is also supported on desktop platforms, albeit in a more limited capacity.

Allow the project to be loaded without an Internet connection if it has been loaded at least once beforehand. This works thanks to the service worker that is installed when the project is first loaded in the user's browser. This service worker provides a local fallback when no Internet connection is available.

Note that web browsers can choose to evict the cached data if the user runs low on disk space, or if the user hasn't opened the project for a while. To ensure data is cached for a longer duration, the user can bookmark the page, or ideally add it to their device's home screen.

If the offline data is not available because it was evicted from the cache, you can configure an Offline Page that will be displayed in this case. The page must be in HTML format and will be saved on the client's machine the first time the project is loaded.

Ensure cross-origin isolation headers are always present, even if the web server hasn't been configured to send them. This allows exports with threads enabled to work when hosted on any website, even if there is no way for you to control the headers it sends.

This behavior can be disabled by unchecking Enable Cross Origin Isolation Headers in the Progressive Web App section.

For security and privacy reasons, many features that work effortlessly on native platforms are more complicated on the web platform. Following is a list of limitations you should be aware of when porting a Godot game to the web.

Browser vendors are making more and more functionalities only available in secure contexts, this means that such features are only be available if the web page is served via a secure HTTPS connection (localhost is usually exempt from such requirement).

Users must allow cookies (specifically IndexedDB) if persistence of the user:// file system is desired. When playing a game presented in an iframe, third-party cookies must also be enabled. Incognito/private browsing mode also prevents persistence.

The method OS.is_userfs_persistent() can be used to check if the user:// file system is persistent, but can give false positives in some cases.

The project will be paused by the browser when the tab is no longer the active tab in the user's browser. This means functions such as _process() and _physics_process() will no longer run until the tab is made active again by the user (by switching back to the tab). This can cause networked games to disconnect if the user switches tabs for a long duration.

This limitation does not apply to unfocused browser windows. Therefore, on the user's side, this can be worked around by running the project in a separate window instead of a separate tab.

Browsers do not allow arbitrarily entering full screen. The same goes for capturing the cursor. Instead, these actions have to occur as a response to a JavaScript input event. In Godot, this means entering full screen from within a pressed input event callback such as _input or _unhandled_input. Querying the Input singleton is not sufficient, the relevant input event must currently be active.

For the same reason, the full screen project setting doesn't work unless the engine is started from within a valid input event handler. This requires customization of the HTML page.

Some browsers restrict autoplay for audio on websites. The easiest way around this limitation is to request the player to click, tap or press a key/button to enable audio, for instance when displaying a splash screen at the start of your game.

Google offers additional information about their Web Audio autoplay policies.

Apple's Safari team also posted additional information about their Auto-Play Policy Changes for macOS.

Access to microphone requires a secure context.

Since Godot 4.3, by default Web exports will use samples instead of streams to play audio.

This is due to the way browsers prefer to play audio and the lack of processing power available when exporting Web games with the Use Threads export option off.

Please note that audio effects aren't yet implemented for samples.

Low-level networking is not implemented due to lacking support in browsers.

Currently, only HTTP client, HTTP requests, WebSocket (client) and WebRTC are supported.

The HTTP classes also have several restrictions on the HTML5 platform:

Accessing or changing the StreamPeer is not possible

Threaded/Blocking mode is not available

Cannot progress more than once per frame, so polling in a loop will freeze

Host verification cannot be disabled

Subject to same-origin policy

Clipboard synchronization between engine and the operating system requires a browser supporting the Clipboard API, additionally, due to the API asynchronous nature might not be reliable when accessed from GDScript.

Requires a secure context.

Gamepads will not be detected until one of their button is pressed. Gamepads might have the wrong mapping depending on the browser/OS/gamepad combination, sadly the Gamepad API does not provide a reliable way to detect the gamepad information necessary to remap them based on model/vendor/OS due to privacy considerations.

Requires a secure context.

Exporting for the web generates several files to be served from a web server, including a default HTML page for presentation. A custom HTML file can be used, see Custom HTML page for Web export.

Only when exporting with Use Threads, to ensure low audio latency and the ability to use Thread in web exports, Godot 4 web exports use SharedArrayBuffer. This requires a secure context, while also requiring the following CORS headers to be set when serving the files:

If you don't control the web server or are unable to add response headers, check Progressive Web App > Enable in the export options. This applies a service worker-based workaround that allows the project to run by simulating the presence of these response headers. A secure context is still required in this case.

If the client doesn't receive the required response headers or the service worker-based workaround is not applied, the project will not run.

The generated .html file can be used as DirectoryIndex in Apache servers and can be renamed to e.g. index.html at any time. Its name is never depended on by default.

The HTML page draws the game at maximum size within the browser window. This way, it can be inserted into an <iframe> with the game's size, as is common on most web game hosting sites.

The other exported files are served as they are, next to the .html file, names unchanged. The .wasm file is a binary WebAssembly module implementing the engine. The .pck file is the Godot main pack containing your game. The .js file contains start-up code and is used by the .html file to access the engine. The .png file contains the boot splash image.

The .pck file is binary, usually delivered with the MIME-type application/octet-stream. The .wasm file is delivered as application/wasm.

Delivering the WebAssembly module (.wasm) with a MIME-type other than application/wasm can prevent some start-up optimizations.

Delivering the files with server-side compression is recommended especially for the .pck and .wasm files, which are usually large in size. The WebAssembly module compresses particularly well, down to around a quarter of its original size with gzip compression. Consider using Brotli precompression if supported on your web server for further file size savings.

Hosts that provide on-the-fly compression: GitHub Pages (gzip)

Hosts that don't provide on-the-fly compression: itch.io, GitLab Pages (supports manual gzip precompression)

The Godot repository includes a Python script to host a local web server. This script is intended for testing the web editor, but it can also be used to test exported projects.

Save the linked script to a file called serve.py, move this file to the folder containing the exported project's index.html, then run the following command in a command prompt within the same folder:

On Windows, you can open a command prompt in the current folder by holding Shift and right-clicking on empty space in Windows Explorer, then choosing Open PowerShell window here.

This will serve the contents of the current folder and open the default web browser automatically.

Note that for production use cases, this Python-based web server should not be used. Instead, you should use an established web server such as Apache or nginx.

See the dedicated page on how to interact with JavaScript and access some unique Web browser features.

You can use the following environment variables to set export options outside of the editor. During the export process, these override the values that you set in the export menu.

Encryption / Encryption Key

GODOT_SCRIPT_ENCRYPTION_KEY

If you use one-click deploy in multiple projects, you may notice that one of the projects you've previously deployed is shown instead of the project you're currently working on. This is due to service worker caching which currently lacks an automated cache busting mechanism.

As a workaround, you can manually unregister the current service worker so that the cache is reset. This also allows a new service worker to be registered. In Chromium-based browsers, open the Developer Tools by pressing F12 or Ctrl + Shift + I (Cmd + Option + I on macOS), then click on the Application tab in DevTools (it may be hidden behind a chevron icon if the devtools pane is narrow). You can either check Update on reload and reload the page, or click Unregister next to the service worker that is currently registered, then reload the page.

Unregistering the service worker in Chromium-based browsers' DevTools

The procedure is similar in Firefox. Open developer tools by pressing F12 or Ctrl + Shift + I (Cmd + Option + I on macOS), click on the Application tab in DevTools (it may be hidden behind a chevron icon if the devtools pane is narrow). Click Unregister next to the service worker that is currently registered, then reload the page.

Unregistering the service worker in Firefox's DevTools

You can find a full list of export options available in the EditorExportPlatformWeb class reference.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
Cross-Origin-Opener-Policy: same-origin
Cross-Origin-Embedder-Policy: require-corp
```

Example 2 (markdown):
```markdown
# You may need to replace `python` with `python3` on some platforms.
python serve.py --root .
```

---

## Exporting for visionOS

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_visionos.html

**Contents:**
- Exporting for visionOS
- User-contributed notes

This page describes how to export a Godot project to visionOS. If you're looking to compile export template binaries from source instead, see Compiling for visionOS.

Exporting instructions for visionOS are currently identical to Compiling for iOS, except you should add a visionOS export preset instead of iOS. See the linked page for details.

Note that currently, only exporting an application for use on a flat plane within the headset is supported. Immersive experiences are not supported.

Please read the User-contributed notes policy before submitting a comment.

---

## Exporting for Windows

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_windows.html

**Contents:**
- Exporting for Windows
- Changing the executable icon
- Code signing
  - Setup
- Environment variables
- Export options
- User-contributed notes

This page describes how to export a Godot project to Windows. If you're looking to compile editor or export template binaries from source instead, read Compiling for Windows.

The simplest way to distribute a game for PC is to copy the executable (godot.exe), compress the folder and send it to someone else. However, this is often not desired.

Godot offers a more elegant approach for PC distribution when using the export system. When exporting for Windows, the exporter takes all the project files and creates a data.pck file. This file is bundled with a specially optimized binary that is smaller, faster and does not contain the editor and debugger.

Godot will automatically use whatever image is set as your project's icon in the project settings, and convert it to an ICO file for the exported project. If you want to manually create an ICO file for greater control over how the icon looks at different resolutions then see the Manually changing application icon for Windows page.

Godot is capable of automatic code signing on export. To do this you must have the Windows SDK (on Windows) or osslsigncode (on any other OS) installed. You will also need a package signing certificate, information on creating one can be found here.

If you export for Windows with embedded PCK files, you will not be able to sign the program as it will break.

On Windows, PCK embedding is also known to cause false positives in antivirus programs. Therefore, it's recommended to avoid using it unless you're distributing your project via Steam as it bypasses code signing and antivirus checks.

Settings need to be changed in two places. First, in the editor settings, under Export > Windows. Click on the folder next to the Sign Tool setting, if you're using Windows navigate to and select SignTool.exe, if you're on a different OS select osslsigncode.

The second location is the Windows export preset, which can be found in Project > Export.... Add a windows desktop preset if you haven't already. Under options there is a code signing category.

Enabled must be set to true, and Identity must be set to the signing certificate. The other settings can be adjusted as needed. Once this is Done Godot will sign your project on export.

You can use the following environment variables to set export options outside of the editor. During the export process, these override the values that you set in the export menu.

Encryption / Encryption Key

GODOT_SCRIPT_ENCRYPTION_KEY

Options / Codesign / Identity Type

GODOT_WINDOWS_CODESIGN_IDENTITY_TYPE

Options / Codesign / Identity

GODOT_WINDOWS_CODESIGN_IDENTITY

Options / Codesign / Password

GODOT_WINDOWS_CODESIGN_PASSWORD

You can find a full list of export options available in the EditorExportPlatformWindows class reference.

Please read the User-contributed notes policy before submitting a comment.

---

## Exporting packs, patches, and mods

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/exporting_pcks.html

**Contents:**
- Exporting packs, patches, and mods
- Use cases
- Overview of PCK/ZIP files
- Generating PCK files
- Opening PCK or ZIP files at runtime
  - Troubleshooting
- Summary
- User-contributed notes

Oftentimes, one would like to add functionality to one's game after it has been deployed.

Examples of this include...

Downloadable Content: the ability to add features and content to one's game.

Patches: the ability to fix a bug that is present in a shipped product.

Mods: grant other people the ability to create content for one's game.

These tools help developers to extend their development beyond the initial release.

Godot enables this via a feature called resource packs (PCK files, with the .pck extension, or ZIP files).

incremental updates/patches

no source code disclosure needed for mods

more modular project structure

users don't have to replace the entire game

The first part of using them involves exporting and delivering the project to players. Then, when one wants to add functionality or content later on, they just deliver the updates via PCK/ZIP files to the users.

PCK/ZIP files usually contain, but are not limited to:

any other asset suitable for import into the game

The PCK/ZIP files can even be an entirely different Godot project, which the original game loads in at runtime.

It is possible to load both PCK and ZIP files as additional packs at the same time. See PCK versus ZIP pack file formats for a comparison of the two formats.

If you want to load loose files at runtime (not packed in a PCK or ZIP by Godot), consider using Runtime file loading and saving instead. This is useful for loading user-generated content that is not made with Godot, without requiring users to pack their mods into a specific file format.

The downside of this approach is that it's less transparent to the game logic, as it will not benefit from the same resource management as PCK/ZIP files.

In order to pack all resources of a project into a PCK file, open the project and go to Project > Export and click on Export PCK/ZIP. Also, make sure to have an export preset selected while doing so.

Another method would be to export from the command line with --export-pack. The output file must with a .pck or .zip file extension. The export process will build that type of file for the chosen platform.

If one wishes to support mods for their game, they will need their users to create similarly exported files. Assuming the original game expects a certain structure for the PCK's resources and/or a certain interface for its scripts, then either...

The developer must publicize documentation of these expected structures/ interfaces, expect modders to install Godot Engine, and then also expect those modders to conform to the documentation's defined API when building mod content for the game (so that it will work). Users would then use Godot's built in exporting tools to create a PCK file, as detailed above.

The developer uses Godot to build a GUI tool for adding their exact API content to a project. This Godot tool must either run on a tools-enabled build of the engine or have access to one (distributed alongside or perhaps in the original game's files). The tool can then use the Godot executable to export a PCK file from the command line with OS.execute(). The game itself shouldn't use a tool-build of the engine (for security), so it's best to keep the modding tool and game separate.

To load a PCK or ZIP file, one uses the ProjectSettings singleton. The following example expects a mod.pck file in the directory of the game's executable. The PCK or ZIP file contains a mod_scene.tscn test scene in its root.

By default, if you import a file with the same file path/name as one you already have in your project, the imported one will replace it. This is something to watch out for when creating DLC or mods. You can solve this problem by using a tool that isolates mods to a specific mods subfolder.

However, it is also a way of creating patches for one's own game. A PCK/ZIP file of this kind can fix the content of a previously loaded PCK/ZIP (therefore, the order in which packs are loaded matters).

To opt out of this behavior, pass false as the second argument to ProjectSettings.load_resource_pack().

For a C# project, you need to build the DLL and place it in the project directory first. Then, before loading the resource pack, you need to load its DLL as follows: Assembly.LoadFile("mod.dll")

If you are loading a resource pack and are not noticing any changes, it may be due to the pack being loaded too late. This is particularly the case with menu scenes that may preload other scenes using preload(). This means that loading a pack in the menu will not affect the other scene that was already preloaded.

To avoid this, you need to load the pack as early as possible. To do so, create a new autoload script and call ProjectSettings.load_resource_pack() in the autoload script's _init() function, rather than _enter_tree() or _ready().

This tutorial explains how to add mods, patches, or DLC to a game. The most important thing is to identify how one plans to distribute future content for their game and develop a workflow that is customized for that purpose. Godot should make that process smooth regardless of which route a developer pursues.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _your_function():
    # This could fail if, for example, mod.pck cannot be found.
    var success = ProjectSettings.load_resource_pack(OS.get_executable_path().get_base_dir().path_join("mod.pck"))

    if success:
        # Now one can use the assets as if they had them in the project from the start.
        var imported_scene = load("res://mod_scene.tscn")
```

Example 2 (sql):
```sql
private void YourFunction()
{
    // This could fail if, for example, mod.pck cannot be found.
    var success = ProjectSettings.LoadResourcePack(OS.get_executable_path().get_base_dir().path_join("mod.pck));

    if (success)
    {
        // Now one can use the assets as if they had them in the project from the start.
        var importedScene = (PackedScene)ResourceLoader.Load("res://mod_scene.tscn");
    }
}
```

---

## Exporting projects

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/exporting_projects.html

**Contents:**
- Exporting projects
- Why export?
  - On PC
  - On mobile
- Export menu
  - Export templates
  - Resource options
- Configuration files
- Exporting from the command line
- PCK versus ZIP pack file formats

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

Originally, Godot did not have any means to export projects. The developers would compile the proper binaries and build the packages for each platform manually.

When more developers (and even non-programmers) started using it, and when our company started taking more projects at the same time, it became evident that this was a bottleneck.

Distributing a game project on PC with Godot is rather easy. Drop the Godot binary in the same directory as the project.godot file, then compress the project directory and you are done.

It sounds simple, but there are probably a few reasons why the developer may not want to do this. The first one is that it may not be desirable to distribute loads of files. Some developers may not like curious users peeking at how the game was made, others may find it inelegant, and so on. Another reason is that the developer might prefer a specially-compiled binary, which is smaller in size, more optimized and does not include tools like the editor and debugger.

Finally, Godot has a simple but efficient system for creating DLCs as extra package files.

The same scenario on mobile platforms is a little worse. To distribute a project on those devices, a binary for each of those platforms is built, then added to a native project together with the game data.

This can be troublesome because it means that the developer must be familiarized with the SDK of each platform before even being able to export. While learning each SDK is always encouraged, it can be frustrating to be forced to do it at an undesired time.

There is also another problem with this approach: different devices prefer some data in different formats to run. The main example of this is texture compression. All PC hardware uses S3TC (BC) compression and that has been standardized for more than a decade, but mobile devices use different formats for texture compression, such as ETC1 and ETC2.

After many attempts at different export workflows, the current one has proven to work the best. At the time of this writing, not all platforms are supported yet, but the supported platforms continue to grow.

To open the export menu, click the Export button:

The export menu will open. However, it will be completely empty. This is because we need to add an export preset.

To create an export preset, click the Add… button at the top of the export menu. This will open a drop-down list of platforms to choose from for an export preset.

The default options are often enough to export, so tweaking them is usually not necessary. However, many platforms require additional tools (SDKs) to be installed to be able to export. Additionally, Godot needs export templates installed to create packages. The export menu will complain when something is missing and will not allow the user to export for that platform until they resolve it:

At that time, the user is expected to come back to the documentation and follow instructions on how to properly set up that platform.

The buttons at the bottom of the menu allow you to export the project in a few different ways:

Export All: Export the project as a playable build (Godot executable and project data) for all the presets defined. All presets must have an Export Path defined for this to work.

Export Project: Export the project as a playable build (Godot executable and project data) for the selected preset.

Export PCK/ZIP: Export the project resources as a PCK or ZIP package. This is not a playable build, it only exports the project data without a Godot executable.

Apart from setting up the platform, the export templates must be installed to be able to export projects. They can be obtained as a TPZ file (which is a renamed ZIP archive) from the download page of the website.

Once downloaded, they can be installed using the Install Export Templates option in the editor:

When exporting, Godot makes a list of all the files to export and then creates the package. There are 3 different modes for exporting:

Export all resources in the project

Export selected scenes (and dependencies)

Export selected resources (and dependencies)

Export all resources in the project will export every resource in the project. Export selected scenes and Export selected resources gives you a list of the scenes or resources in the project, and you have to select every scene or resource you want to export.

Export all resources in the project except resources checked below does exactly what it says, everything will be exported except for what you select in the list.

Export as dedicated server will remove all visuals from a project and replace them with a placeholder. This includes Cubemap, CubemapArray, Material, Mesh, Texture2D, Texture2DArray, Texture3D. You can also go into the list of files and specify specific visual resources that you do wish to keep.

Files and folders whose name begin with a period will never be included in the exported project. This is done to prevent version control folders like .git from being included in the exported PCK file.

Below the list of resources are two filters that can be setup. The first allows non-resource files such as .txt, .json and .csv to be exported with the project. The second filter can be used to exclude every file of a certain type without manually deselecting every one. For example, .png files.

The export configuration is stored in two files that can both be found in the project directory:

export_presets.cfg: This file contains the vast majority of the export configuration and can be safely committed to version control. There is nothing in here that you would normally have to keep secret.

.godot/export_credentials.cfg: This file contains export options that are considered confidential, like passwords and encryption keys. It should generally not be committed to version control or shared with others unless you know exactly what you are doing.

Since the credentials file is usually kept out of version control systems, some export options will be missing if you clone the project to a new machine. The easiest way to deal with this is to copy the file manually from the old location to the new one.

In production, it is useful to automate builds, and Godot supports this with the --export-release and --export-debug command line parameters. Exporting from the command line still requires an export preset to define the export parameters. A basic invocation of the command would be:

This will export to some_name.exe, assuming there is a preset called "Windows Desktop" and the template can be found. (The export preset name must be written within quotes if it contains spaces or special characters.) The output path is relative to the project path or absolute; it does not respect the directory the command was invoked from.

The output file extension should match the one used by the Godot export process:

macOS: .app or .zip (or .dmg when exporting from macOS)

Linux: Any extension (including none). .x86_64 is typically used for 64-bit x86 binaries.

You can also configure it to export only the PCK or ZIP file, allowing a single exported main pack file to be used with multiple Godot executables. When doing so, the export preset name must still be specified on the command line:

It is often useful to combine the --export-release flag with the --path flag, so that you do not need to cd to the project folder before running the command:

See Command line tutorial for more information about using Godot from the command line.

Each format has its upsides and downsides. PCK is the default and recommended format for most use cases, but you may want to use a ZIP archive instead depending on your needs.

Uncompressed format. Larger file size, but faster to read/write.

Not readable and writable using tools normally present on the user's operating system, even though there are third-party tools to extract and create PCK files.

Compressed format. Smaller file size, but slower to read/write.

Readable and writable using tools normally present on the user's operating system. This can be useful to make modding easier (see also Exporting packs, patches, and mods).

Due to a known bug, when using a ZIP file as a pack file, the exported binary will not try to use it automatically. Therefore, you have to create a launcher script that the player can double-click or run from a terminal to launch the project:

Save the launcher script and place it in the same folder as the exported binary. On Linux, make sure to give executable permissions to the launcher script using the command chmod +x launch.sh.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
godot --export-release "Windows Desktop" some_name.exe
```

Example 2 (unknown):
```unknown
godot --export-pack "Windows Desktop" some_name.pck
```

Example 3 (unknown):
```unknown
godot --path /path/to/project --export-release "Windows Desktop" some_name.exe
```

Example 4 (markdown):
```markdown
:: launch.bat (Windows)
@echo off
my_project.exe --main-pack my_project.zip

# launch.sh (Linux)
./my_project.x86_64 --main-pack my_project.zip
```

---

## Export

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/index.html

**Contents:**
- Export

This section is about exporting a build of your project. If you're trying to export properties from a script, see GDScript exported properties or C# exported properties.

---

## ExternalTexture

**URL:** https://docs.godotengine.org/en/stable/classes/class_externaltexture.html

**Contents:**
- ExternalTexture
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Texture2D < Texture < Resource < RefCounted < Object

Texture which displays the content of an external buffer.

Displays the content of an external buffer provided by the platform.

Requires the OES_EGL_image_external extension (OpenGL) or VK_ANDROID_external_memory_android_hardware_buffer extension (Vulkan).

Note: This is currently only supported in Android builds.

resource_local_to_scene

false (overrides Resource)

get_external_texture_id() const

set_external_buffer_id(external_buffer_id: int)

Vector2 size = Vector2(256, 256) 

void set_size(value: Vector2)

External texture size.

int get_external_texture_id() const 

Returns the external texture ID.

Depending on your use case, you may need to pass this to platform APIs, for example, when creating an android.graphics.SurfaceTexture on Android.

void set_external_buffer_id(external_buffer_id: int) 

Sets the external buffer ID.

Depending on your use case, you may need to call this with data received from a platform API, for example, SurfaceTexture.getHardwareBuffer() on Android.

Please read the User-contributed notes policy before submitting a comment.

---

## Feature tags

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/feature_tags.html

**Contents:**
- Feature tags
- Introduction
- Default features
- Custom features
- Overriding project settings
- Default overrides
- Taking feature tags into account when reading project settings
- Customizing the build
- User-contributed notes

Godot has a special system to tag availability of features. Each feature is represented as a string, which can refer to many of the following:

Platform architecture (64-bit or 32-bit, x86 or ARM).

Platform type (desktop, mobile, Web).

Supported texture compression algorithms on the platform.

Whether a build is debug or release (debug includes the editor).

Whether the project is running from the editor or a "standalone" binary.

Features can be queried at runtime from the singleton API by calling:

OS feature tags are used by GDExtension to determine which libraries to load. For example, a library for linux.debug.editor.x86_64 will be loaded only on a debug editor build for Linux x86_64.

Here is a list of most feature tags in Godot. Keep in mind they are case-sensitive:

Running on Android (but not within a Web browser)

Running on *BSD (but not within a Web browser)

Running on Linux (but not within a Web browser)

Running on macOS (but not within a Web browser)

Running on iOS (but not within a Web browser)

Running on visionOS (but not within a Web browser)

Running on Linux or *BSD

Running on a debug build (including the editor)

Running on a release build

Running on an editor build

Running on an editor build, and inside the editor

Running on an editor build, and running the project

Running on a non-editor (export template) build

Running on a double-precision build

Running on a single-precision build

Running on a 64-bit build (any architecture)

Running on a 32-bit build (any architecture)

Running on a 64-bit x86 build

Running on a 32-bit x86 build

Running on an x86 build (any bitness)

Running on a 64-bit ARM build

Running on a 32-bit ARM build

Running on an ARM build (any bitness)

Running on a 64-bit RISC-V build

Running on a RISC-V build (any bitness)

Running on a 64-bit PowerPC build

Running on a 32-bit PowerPC build

Running on a PowerPC build (any bitness)

Running on a 64-bit WebAssembly build (not yet possible)

Running on a 32-bit WebAssembly build

Running on a WebAssembly build (any bitness)

Host OS is a mobile platform

Host OS is a PC platform (desktop/laptop)

Host OS is a Web browser

Running without threading support

Running with threading support

Host OS is a Web browser running on Android

Host OS is a Web browser running on iOS

Host OS is a Web browser running on Linux or *BSD

Host OS is a Web browser running on macOS

Host OS is a Web browser running on Windows

Textures using ETC1 compression are supported

Textures using ETC2 compression are supported

Textures using S3TC (DXT/BC) compression are supported

Movie Maker mode is active

Project was exported with shader baking enabled (only applies to the exported project, not when running in the editor)

Project was exported as a dedicated server (only applies to the exported project, not when running in the editor)

With the exception of texture compression, web_<platform> and movie feature tags, default feature tags are immutable. This means that they will not change depending on runtime conditions. For example, OS.has_feature("mobile") will return false when running a project exported to Web on a mobile device.

To check whether a project exported to Web is running on a mobile device, use OS.has_feature("web_android") or OS.has_feature("web_ios").

It is possible to add custom features to a build; use the relevant field in the export preset used to generate it:

Custom feature tags are only used when running the exported project (including with One-click deploy). They are not used when running the project from the editor, even if the export preset marked as Runnable for your current platform has custom feature tags defined.

Custom feature tags are also not used in EditorExportPlugin scripts. Instead, feature tags in EditorExportPlugin will reflect the device the editor is currently running on.

Features can be used to override specific configuration values in the Project Settings. This allows you to better customize any configuration when doing a build.

In the following example, a different icon is added for the demo build of the game (which was customized in a special export preset, which, in turn, includes only demo levels).

The desired configuration is selected, which effectively copies its properties to the panel above (1). The "demo_build" feature tag is selected (2). The configuration is added to the project settings (3).

After overriding, a new field is added for this specific configuration.

When using the project settings "override.cfg" functionality (which is unrelated to feature tags), remember that feature tags still apply. Therefore, make sure to also override the setting with the desired feature tag(s) if you want them to override base project settings on all platforms and configurations.

There are already a lot of settings that come with overrides by default; they can be found in many sections of the project settings.

By default, feature tags are not taken into account when reading project settings using the typical approaches (ProjectSettings.get_setting or ProjectSettings.get). Instead, you must use ProjectSettings.get_setting_with_override.

For example, with the following project settings:

Using ProjectSettings.get_setting("section/subsection/example") will return "Release" regardless of whether a debug build is currently running. On the other hand, ProjectSettings.get_setting_with_override("section/subsection/example") will obey feature tags and will return "Debug" if using a debug build.

Feature tags can be used to customize a build process too, by writing a custom ExportPlugin. They are also used to specify which shared library is loaded and exported in GDExtension.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
OS.has_feature(name)
```

Example 2 (unknown):
```unknown
OS.HasFeature(name);
```

Example 3 (json):
```json
[section]

subsection/example = "Release"
subsection/example.debug = "Debug"
```

---

## HTTPRequest

**URL:** https://docs.godotengine.org/en/stable/classes/class_httprequest.html

**Contents:**
- HTTPRequest
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

A node with the ability to send HTTP(S) requests.

A node with the ability to send HTTP requests. Uses HTTPClient internally.

Can be used to make HTTP requests, i.e. download or upload files or web content via HTTP.

Warning: See the notes and warnings on HTTPClient for limitations, especially regarding TLS security.

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

Example: Contact a REST API and print one of its returned fields:

Example: Load an image using HTTPRequest and display it:

Note: HTTPRequest nodes will automatically handle decompression of response bodies. An Accept-Encoding header will be automatically added to each of your requests, unless one is already specified. Any response with a Content-Encoding: gzip header will automatically be decompressed and delivered to you as uncompressed bytes.

get_body_size() const

get_downloaded_bytes() const

get_http_client_status() const

request(url: String, custom_headers: PackedStringArray = PackedStringArray(), method: Method = 0, request_data: String = "")

request_raw(url: String, custom_headers: PackedStringArray = PackedStringArray(), method: Method = 0, request_data_raw: PackedByteArray = PackedByteArray())

set_http_proxy(host: String, port: int)

set_https_proxy(host: String, port: int)

set_tls_options(client_options: TLSOptions)

request_completed(result: int, response_code: int, headers: PackedStringArray, body: PackedByteArray) 

Emitted when a request is completed.

Result RESULT_SUCCESS = 0

Result RESULT_CHUNKED_BODY_SIZE_MISMATCH = 1

Request failed due to a mismatch between the expected and actual chunked body size during transfer. Possible causes include network errors, server misconfiguration, or issues with chunked encoding.

Result RESULT_CANT_CONNECT = 2

Request failed while connecting.

Result RESULT_CANT_RESOLVE = 3

Request failed while resolving.

Result RESULT_CONNECTION_ERROR = 4

Request failed due to connection (read/write) error.

Result RESULT_TLS_HANDSHAKE_ERROR = 5

Request failed on TLS handshake.

Result RESULT_NO_RESPONSE = 6

Request does not have a response (yet).

Result RESULT_BODY_SIZE_LIMIT_EXCEEDED = 7

Request exceeded its maximum size limit, see body_size_limit.

Result RESULT_BODY_DECOMPRESS_FAILED = 8

Request failed due to an error while decompressing the response body. Possible causes include unsupported or incorrect compression format, corrupted data, or incomplete transfer.

Result RESULT_REQUEST_FAILED = 9

Request failed (currently unused).

Result RESULT_DOWNLOAD_FILE_CANT_OPEN = 10

HTTPRequest couldn't open the download file.

Result RESULT_DOWNLOAD_FILE_WRITE_ERROR = 11

HTTPRequest couldn't write to the download file.

Result RESULT_REDIRECT_LIMIT_REACHED = 12

Request reached its maximum redirect limit, see max_redirects.

Result RESULT_TIMEOUT = 13

Request failed due to a timeout. If you expect requests to take a long time, try increasing the value of timeout or setting it to 0.0 to remove the timeout completely.

bool accept_gzip = true 

void set_accept_gzip(value: bool)

bool is_accepting_gzip()

If true, this header will be added to each request: Accept-Encoding: gzip, deflate telling servers that it's okay to compress response bodies.

Any Response body declaring a Content-Encoding of either gzip or deflate will then be automatically decompressed, and the uncompressed bytes will be delivered via request_completed.

If the user has specified their own Accept-Encoding header, then no header will be added regardless of accept_gzip.

If false no header will be added, and no decompression will be performed on response bodies. The raw bytes of the response body will be returned via request_completed.

int body_size_limit = -1 

void set_body_size_limit(value: int)

int get_body_size_limit()

Maximum allowed size for response bodies. If the response body is compressed, this will be used as the maximum allowed size for the decompressed body.

int download_chunk_size = 65536 

void set_download_chunk_size(value: int)

int get_download_chunk_size()

The size of the buffer used and maximum bytes to read per iteration. See HTTPClient.read_chunk_size.

Set this to a lower value (e.g. 4096 for 4 KiB) when downloading small files to decrease memory usage at the cost of download speeds.

String download_file = "" 

void set_download_file(value: String)

String get_download_file()

The file to download into. Will output any received file into it.

int max_redirects = 8 

void set_max_redirects(value: int)

int get_max_redirects()

Maximum number of allowed redirects.

float timeout = 0.0 

void set_timeout(value: float)

The duration to wait in seconds before a request times out. If timeout is set to 0.0 then the request will never time out. For simple requests, such as communication with a REST API, it is recommended that timeout is set to a value suitable for the server response time (e.g. between 1.0 and 10.0). This will help prevent unwanted timeouts caused by variation in server response times while still allowing the application to detect when a request has timed out. For larger requests such as file downloads it is suggested the timeout be set to 0.0, disabling the timeout functionality. This will help to prevent large transfers from failing due to exceeding the timeout value.

bool use_threads = false 

void set_use_threads(value: bool)

bool is_using_threads()

If true, multithreading is used to improve performance.

void cancel_request() 

Cancels the current request.

int get_body_size() const 

Returns the response body length.

Note: Some Web servers may not send a body length. In this case, the value returned will be -1. If using chunked transfer encoding, the body length will also be -1.

int get_downloaded_bytes() const 

Returns the number of bytes this HTTPRequest downloaded.

Status get_http_client_status() const 

Returns the current status of the underlying HTTPClient.

Error request(url: String, custom_headers: PackedStringArray = PackedStringArray(), method: Method = 0, request_data: String = "") 

Creates request on the underlying HTTPClient. If there is no configuration errors, it tries to connect using HTTPClient.connect_to_host() and passes parameters onto HTTPClient.request().

Returns @GlobalScope.OK if request is successfully created. (Does not imply that the server has responded), @GlobalScope.ERR_UNCONFIGURED if not in the tree, @GlobalScope.ERR_BUSY if still processing previous request, @GlobalScope.ERR_INVALID_PARAMETER if given string is not a valid URL format, or @GlobalScope.ERR_CANT_CONNECT if not using thread and the HTTPClient cannot connect to host.

Note: When method is HTTPClient.METHOD_GET, the payload sent via request_data might be ignored by the server or even cause the server to reject the request (check RFC 7231 section 4.3.1 for more details). As a workaround, you can send data as a query string in the URL (see String.uri_encode() for an example).

Note: It's recommended to use transport encryption (TLS) and to avoid sending sensitive information (such as login credentials) in HTTP GET URL parameters. Consider using HTTP POST requests or HTTP headers for such information instead.

Error request_raw(url: String, custom_headers: PackedStringArray = PackedStringArray(), method: Method = 0, request_data_raw: PackedByteArray = PackedByteArray()) 

Creates request on the underlying HTTPClient using a raw array of bytes for the request body. If there is no configuration errors, it tries to connect using HTTPClient.connect_to_host() and passes parameters onto HTTPClient.request().

Returns @GlobalScope.OK if request is successfully created. (Does not imply that the server has responded), @GlobalScope.ERR_UNCONFIGURED if not in the tree, @GlobalScope.ERR_BUSY if still processing previous request, @GlobalScope.ERR_INVALID_PARAMETER if given string is not a valid URL format, or @GlobalScope.ERR_CANT_CONNECT if not using thread and the HTTPClient cannot connect to host.

void set_http_proxy(host: String, port: int) 

Sets the proxy server for HTTP requests.

The proxy server is unset if host is empty or port is -1.

void set_https_proxy(host: String, port: int) 

Sets the proxy server for HTTPS requests.

The proxy server is unset if host is empty or port is -1.

void set_tls_options(client_options: TLSOptions) 

Sets the TLSOptions to be used when connecting to an HTTPS server. See TLSOptions.client().

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _ready():
    # Create an HTTP request node and connect its completion signal.
    var http_request = HTTPRequest.new()
    add_child(http_request)
    http_request.request_completed.connect(self._http_request_completed)

    # Perform a GET request. The URL below returns JSON as of writing.
    var error = http_request.request("https://httpbin.org/get")
    if error != OK:
        push_error("An error occurred in the HTTP request.")

    # Perform a POST request. The URL below returns JSON as of writing.
    # Note: Don't make simultaneous requests using a single HTTPRequest node.
    # The snippet below is provided for reference only.
    var body = JSON.new().stringify({"name": "Godette"})
    error = http_request.request("https://httpbin.org/post", [], HTTPClient.METHOD_POST, body)
    if error != OK:
        push_error("An error occurred in the HTTP request.")

# Called when the HTTP request is completed.
func _http_request_completed(result, response_code, headers, body):
    var json = JSON.new()
    json.parse(body.get_string_from_utf8())
    var response = json.get_data()

    # Will print the user agent string used by the HTTPRequest node (as recognized by httpbin.org).
    print(response.headers["User-Agent"])
```

Example 2 (gdscript):
```gdscript
public override void _Ready()
{
    // Create an HTTP request node and connect its completion signal.
    var httpRequest = new HttpRequest();
    AddChild(httpRequest);
    httpRequest.RequestCompleted += HttpRequestCompleted;

    // Perform a GET request. The URL below returns JSON as of writing.
    Error error = httpRequest.Request("https://httpbin.org/get");
    if (error != Error.Ok)
    {
        GD.PushError("An error occurred in the HTTP request.");
    }

    // Perform a POST request. The URL below returns JSON as of writing.
    // Note: Don't make simultaneous requests using a single HTTPRequest node.
    // The snippet below is provided for reference only.
    string body = new Json().Stringify(new Godot.Collections.Dictionary
    {
        { "name", "Godette" }
    });
    error = httpRequest.Request("https://httpbin.org/post", null, HttpClient.Method.Post, body);
    if (error != Error.Ok)
    {
        GD.PushError("An error occurred in the HTTP request.");
    }
}

// Called when the HTTP request is completed.
private void HttpRequestCompleted(long result, long responseCode, string[] headers, byte[] body)
{
    var json = new Json();
    json.Parse(body.GetStringFromUtf8());
    var response = json.GetData().AsGodotDictionary();

    // Will print the user agent string used by the HTTPRequest node (as recognized by httpbin.org).
    GD.Print((response["headers"].AsGodotDictionary())["User-Agent"]);
}
```

Example 3 (gdscript):
```gdscript
func _ready():
    # Create an HTTP request node and connect its completion signal.
    var http_request = HTTPRequest.new()
    add_child(http_request)
    http_request.request_completed.connect(self._http_request_completed)

    # Perform the HTTP request. The URL below returns a PNG image as of writing.
    var error = http_request.request("https://placehold.co/512.png")
    if error != OK:
        push_error("An error occurred in the HTTP request.")

# Called when the HTTP request is completed.
func _http_request_completed(result, response_code, headers, body):
    if result != HTTPRequest.RESULT_SUCCESS:
        push_error("Image couldn't be downloaded. Try a different image.")

    var image = Image.new()
    var error = image.load_png_from_buffer(body)
    if error != OK:
        push_error("Couldn't load the image.")

    var texture = ImageTexture.create_from_image(image)

    # Display the image in a TextureRect node.
    var texture_rect = TextureRect.new()
    add_child(texture_rect)
    texture_rect.texture = texture
```

Example 4 (gdscript):
```gdscript
public override void _Ready()
{
    // Create an HTTP request node and connect its completion signal.
    var httpRequest = new HttpRequest();
    AddChild(httpRequest);
    httpRequest.RequestCompleted += HttpRequestCompleted;

    // Perform the HTTP request. The URL below returns a PNG image as of writing.
    Error error = httpRequest.Request("https://placehold.co/512.png");
    if (error != Error.Ok)
    {
        GD.PushError("An error occurred in the HTTP request.");
    }
}

// Called when the HTTP request is completed.
private void HttpRequestCompleted(long result, long responseCode, string[] headers, byte[] body)
{
    if (result != (long)HttpRequest.Result.Success)
    {
        GD.PushError("Image couldn't be downloaded. Try a different image.");
    }
    var image = new Image();
    Error error = image.LoadPngFromBuffer(body);
    if (error != Error.Ok)
    {
        GD.PushError("Couldn't load the image.");
    }

    var texture = ImageTexture.CreateFromImage(image);

    // Display the image in a TextureRect node.
    var textureRect = new TextureRect();
    AddChild(textureRect);
    textureRect.Texture = texture;
}
```

---

## JavaClass

**URL:** https://docs.godotengine.org/en/stable/classes/class_javaclass.html

**Contents:**
- JavaClass
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Represents a class from the Java Native Interface.

Represents a class from the Java Native Interface. It is returned from JavaClassWrapper.wrap().

Note: This class only works on Android. On any other platform, this class does nothing.

Note: This class is not to be confused with JavaScriptObject.

get_java_class_name() const

get_java_method_list() const

get_java_parent_class() const

String get_java_class_name() const 

Returns the Java class name.

Array[Dictionary] get_java_method_list() const 

Returns the object's Java methods and their signatures as an Array of dictionaries, in the same format as Object.get_method_list().

JavaClass get_java_parent_class() const 

Returns a JavaClass representing the Java parent class of this class.

Please read the User-contributed notes policy before submitting a comment.

---

## JavaObject

**URL:** https://docs.godotengine.org/en/stable/classes/class_javaobject.html

**Contents:**
- JavaObject
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Represents an object from the Java Native Interface.

Represents an object from the Java Native Interface. It can be returned from Java methods called on JavaClass or other JavaObjects. See JavaClassWrapper for an example.

Note: This class only works on Android. On any other platform, this class does nothing.

Note: This class is not to be confused with JavaScriptObject.

get_java_class() const

JavaClass get_java_class() const 

Returns the JavaClass that this object is an instance of.

Please read the User-contributed notes policy before submitting a comment.

---

## JavaScriptBridge

**URL:** https://docs.godotengine.org/en/stable/classes/class_javascriptbridge.html

**Contents:**
- JavaScriptBridge
- Description
- Tutorials
- Methods
- Signals
- Method Descriptions
- User-contributed notes

Singleton that connects the engine with the browser's JavaScript context in Web export.

The JavaScriptBridge singleton is implemented only in the Web export. It's used to access the browser's JavaScript context. This allows interaction with embedding pages or calling third-party JavaScript APIs.

Note: This singleton can be disabled at build-time to improve security. By default, the JavaScriptBridge singleton is enabled. Official export templates also have the JavaScriptBridge singleton enabled. See Compiling for the Web in the documentation for more information.

Exporting for the Web: Calling JavaScript from script

create_callback(callable: Callable)

create_object(object: String, ...) vararg

download_buffer(buffer: PackedByteArray, name: String, mime: String = "application/octet-stream")

eval(code: String, use_global_execution_context: bool = false)

get_interface(interface: String)

is_js_buffer(javascript_object: JavaScriptObject)

js_buffer_to_packed_byte_array(javascript_buffer: JavaScriptObject)

pwa_needs_update() const

pwa_update_available() 

Emitted when an update for this progressive web app has been detected but is waiting to be activated because a previous version is active. See pwa_update() to force the update to take place immediately.

JavaScriptObject create_callback(callable: Callable) 

Creates a reference to a Callable that can be used as a callback by JavaScript. The reference must be kept until the callback happens, or it won't be called at all. See JavaScriptObject for usage.

Note: The callback function must take exactly one Array argument, which is going to be the JavaScript arguments object converted to an array.

Variant create_object(object: String, ...) vararg 

Creates a new JavaScript object using the new constructor. The object must a valid property of the JavaScript window. See JavaScriptObject for usage.

void download_buffer(buffer: PackedByteArray, name: String, mime: String = "application/octet-stream") 

Prompts the user to download a file containing the specified buffer. The file will have the given name and mime type.

Note: The browser may override the MIME type provided based on the file name's extension.

Note: Browsers might block the download if download_buffer() is not being called from a user interaction (e.g. button click).

Note: Browsers might ask the user for permission or block the download if multiple download requests are made in a quick succession.

Variant eval(code: String, use_global_execution_context: bool = false) 

Execute the string code as JavaScript code within the browser window. This is a call to the actual global JavaScript function eval().

If use_global_execution_context is true, the code will be evaluated in the global execution context. Otherwise, it is evaluated in the execution context of a function within the engine's runtime environment.

void force_fs_sync() 

Force synchronization of the persistent file system (when enabled).

Note: This is only useful for modules or extensions that can't use FileAccess to write files.

JavaScriptObject get_interface(interface: String) 

Returns an interface to a JavaScript object that can be used by scripts. The interface must be a valid property of the JavaScript window. The callback must accept a single Array argument, which will contain the JavaScript arguments. See JavaScriptObject for usage.

bool is_js_buffer(javascript_object: JavaScriptObject) 

Returns true if the given javascript_object is of type [code]ArrayBuffer[/code], [code]DataView[/code], or one of the many typed array objects.

PackedByteArray js_buffer_to_packed_byte_array(javascript_buffer: JavaScriptObject) 

Returns a copy of javascript_buffer's contents as a PackedByteArray. See also is_js_buffer().

bool pwa_needs_update() const 

Returns true if a new version of the progressive web app is waiting to be activated.

Note: Only relevant when exported as a Progressive Web App.

Performs the live update of the progressive web app. Forcing the new version to be installed and the page to be reloaded.

Note: Your application will be reloaded in all browser tabs.

Note: Only relevant when exported as a Progressive Web App and pwa_needs_update() returns true.

Please read the User-contributed notes policy before submitting a comment.

---

## JavaScriptObject

**URL:** https://docs.godotengine.org/en/stable/classes/class_javascriptobject.html

**Contents:**
- JavaScriptObject
- Description
- User-contributed notes

Inherits: RefCounted < Object

A wrapper class for web native JavaScript objects.

JavaScriptObject is used to interact with JavaScript objects retrieved or created via JavaScriptBridge.get_interface(), JavaScriptBridge.create_object(), or JavaScriptBridge.create_callback().

Note: Only available in the Web platform.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Node

var _my_js_callback = JavaScriptBridge.create_callback(myCallback) # This reference must be kept
var console = JavaScriptBridge.get_interface("console")

func _init():
    var buf = JavaScriptBridge.create_object("ArrayBuffer", 10) # new ArrayBuffer(10)
    print(buf) # Prints [JavaScriptObject:OBJECT_ID]
    var uint8arr = JavaScriptBridge.create_object("Uint8Array", buf) # new Uint8Array(buf)
    uint8arr[1] = 255
    prints(uint8arr[1], uint8arr.byteLength) # Prints "255 10"

    # Prints "Uint8Array(10) [ 0, 255, 0, 0, 0, 0, 0, 0, 0, 0 ]" in the browser's console.
    console.log(uint8arr)

    # Equivalent of JavaScriptBridge: Array.from(uint8arr).forEach(myCallback)
    JavaScriptBridge.get_interface("Array").from(uint8arr).forEach(_my_js_callback)

func myCallback(args):
    # Will be called with the parameters passed to the "forEach" callback
    # [0, 0, [JavaScriptObject:1173]]
    # [255, 1, [JavaScriptObject:1173]]
    # ...
    # [0, 9, [JavaScriptObject:1180]]
    print(args)
```

---

## JNISingleton

**URL:** https://docs.godotengine.org/en/stable/classes/class_jnisingleton.html

**Contents:**
- JNISingleton
- Description
- Tutorials
- User-contributed notes

Singleton that connects the engine with Android plugins to interface with native Android code.

The JNISingleton is implemented only in the Android export. It's used to call methods and connect signals from an Android plugin written in Java or Kotlin. Methods and signals can be called and connected to the JNISingleton as if it is a Node. See Java Native Interface - Wikipedia for more information.

Creating Android plugins

Please read the User-contributed notes policy before submitting a comment.

---

## Manually changing application icon for Windows

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/changing_application_icon_for_windows.html

**Contents:**
- Manually changing application icon for Windows
- Creating a custom ICO file
- Changing the taskbar icon
- Changing the file icon
- Testing the result
- User-contributed notes

Windows applications use a Windows only format called ICO for their file icon and taskbar icon. Since Godot 4.1, Godot can create an ICO file for you based on the icon file defined in the Windows export preset. Supported formats are PNG, WebP, and SVG. If no icon is defined in the Windows export preset, the application/config/icon project setting is used automatically instead.

This means you no longer need to follow the steps in this section to manually create an ICO file, unless you wish to have control over the icon design depending on its displayed size.

You can create your application icon in any program but you will have to convert it to an ICO file using a program such as GIMP.

This video tutorial goes over how to export an ICO file with GIMP.

It is also possible to convert a PNG image to an hiDPI-friendly ICO file using this ImageMagick command:

Depending on which version of ImageMagick you installed, you might need to leave out the magick and run this command instead:

For the ICO file to effectively replace the default Godot icon, it must contain all the sizes included in the default Godot icon: 16×16, 32×32, 48×48, 64×64, 128×128, 256×256. If the ICO file does not contain all the sizes, the default Godot icon will be kept for the sizes that weren't overridden.

The above ImageMagick command takes this into account.

The taskbar icon is the icon that shows up on the taskbar when your project is running.

To change the taskbar icon, go to Project > Project Settings > Application > Config, make sure Advanced Settings are enabled to see the setting, then go to Windows Native Icon. Click on the folder icon and select your ICO file.

This setting only changes the icon for your exported game on Windows. To set the icon for macOS, use Macos Native Icon. And for any other platform, use the Icon setting.

The file icon is the icon of the executable that you click on to start the project.

To do that, you will need to specify the icon when exporting. Go to Project > Export. Assuming you have already created a Windows Desktop preset, select your icon in ICO format in the Application > Icon field.

You can now export the project. If it worked correctly, you should see this:

If your icon isn't showing up properly try clearing the icon cache. To do so, open the Run dialog and enter ie4uinit.exe -ClearIconCache or ie4uinit.exe -show.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
magick convert icon.png -define icon:auto-resize=256,128,64,48,32,16 icon.ico
```

Example 2 (unknown):
```unknown
convert icon.png -define icon:auto-resize=256,128,64,48,32,16 icon.ico
```

---

## One-click deploy

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/one-click_deploy.html

**Contents:**
- One-click deploy
- What is one-click deploy?
- Supported platforms
- Using one-click deploy
- Troubleshooting
  - Android
  - Web
- User-contributed notes

One-click deploy is a feature that is available once a platform is properly configured and a supported device is connected to the computer. Since things can go wrong at many levels (platform may not be configured correctly, SDK may be incorrectly installed, device may be improperly configured, etc.), it's good to let the user know that it exists.

After adding an Android export preset marked as Runnable, Godot can detect when a USB device is connected to the computer and offer the user to automatically export, install and run the project (in debug mode) on the device. This feature is called one-click deploy.

One-click deploy is only available once you've added an export template marked as Runnable in the Export dialog. You can mark several export presets as runnable, but only one preset per platform may be marked as runnable. If you mark a second preset in a given platform as runnable, the other preset will no longer be marked as runnable.

Android: Exports the project with debugging enabled and runs it on the connected device.

Make sure to follow the steps described in Exporting for Android. Otherwise, the one-click deploy button won't appear.

If you have more than one device connected, Godot will ask you which device the project should be exported to.

iOS: Exports the project with debugging enabled and runs it on the connected device.

Make sure to follow the steps described in Exporting for iOS. Otherwise, the one-click deploy button won't appear.

For each new bundle identifier, export the project, open it in the Xcode, and build at least once to create new provisioning profile or create a provisioning profile in the Apple Developer account dashboard.

If you have more than one device connected, Godot will ask you which device the project should be exported to.

Desktop platforms: Exports the project with debugging enabled and runs it on the remote computer via SSH.

Web: Starts a local web server and runs the exported project by opening the default web browser. This is only accessible on localhost by default. See Troubleshooting for making the exported project accessible on remote devices.

Enable developer mode on your mobile device then enable USB debugging in the device's settings.

After enabling USB debugging, connect the device to your PC using a USB cable.

For advanced users, it should also be possible to use wireless ADB.

Install Xcode, accept Xcode license and login with your Apple Developer account.

If you are using Xcode 14 or earlier, install ios-deploy and set path to ios-deploy in the Editor Settings (see Export ⇾ iOS ⇾ iOS Deploy).

Pair your mobile device with a Mac.

Enable developer mode on your device.

Device can be connected via USB or local network.

Make sure the device is on the same local network and a correct network interface is selected in the editor settings (see Network ⇾ Debug ⇾ Remote Host). By default, the editor is listening for localhost connections only.

Device screen should be unlocked.

Enable SSH Remote Deploy and configure connection settings in the project export setting.

Make sure there is an export preset marked as Runnable for the target platform (Android, iOS or Web).

If everything is configured correctly and with no errors, platform-specific icons will appear in the top-right corner of the editor.

Click the button to export to the desired platform in one click.

If you can't see the device in the list of devices when running the adb devices command in a terminal, it will not be visible by Godot either. To resolve this:

Check if USB debugging is enabled and authorized on the device. Try unlocking your device and accepting the authorization prompt if you see any. If you can't see this prompt, running adb devices on your PC should make the authorization prompt appear on the device.

Try revoking the debugging authorization in the device's developer settings, then follow the steps again.

Try using USB debugging instead of wireless debugging or vice versa. Sometimes, one of those can work better than the other.

On Linux, you may be missing the required udev rules for your device to be recognized.

By default, the web server started by the editor is only accessible from localhost. This means the web server can't be reached by other devices on the local network or the Internet (if port forwarding is set up on the router). This is done for security reasons, as you may not want other devices to be able to access the exported project while you're testing it. Binding to localhost also prevents a firewall popup from appearing when you use one-click deploy for the web platform.

To make the local web server accessible over the local network, you'll need to change the Export > Web > HTTP Host editor setting to 0.0.0.0. You will also need to enable Export > Web > Use TLS as SharedArrayBuffer requires the use of a secure connection to work, unless connecting to localhost. However, since other clients will be connecting to a remote device, the use of TLS is absolutely required here.

To make the local web server accessible over the Internet, you'll also need to forward the Export > Web > HTTP Port port specified in the Editor Settings (8060 by default) in TCP on your router. This is usually done by accessing your router's web interface then adding a NAT rule for the port in question. For IPv6 connections, you should allow the port in the router's IPv6 firewall instead. Like for local network devices, you will also need to enable Export > Web > Use TLS.

When Use TLS is enabled, you will get a warning from your web browser as Godot will use a temporary self-signed certificate. You can safely ignore it and bypass the warning by clicking Advanced and then Proceed to (address).

If you have an SSL/TLS certificate that is trusted by browsers, you can specify the paths to the key and certificate files in the Export > Web > TLS Key and Export > Web > TLS Certificate. This will only work if the project is accessed through a domain name that is part of the TLS certificate.

When using one-click deploy on different projects, it's possible that a previously edited project is being shown instead. This is due to service worker caching not being cleared automatically. See Troubleshooting for instructions on unregistering the service worker, which will effectively clear the cache and resolve the issue.

Please read the User-contributed notes policy before submitting a comment.

---

## PacketPeerDTLS

**URL:** https://docs.godotengine.org/en/stable/classes/class_packetpeerdtls.html

**Contents:**
- PacketPeerDTLS
- Description
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: PacketPeer < RefCounted < Object

This class represents a DTLS peer connection. It can be used to connect to a DTLS server, and is returned by DTLSServer.take_connection().

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

Warning: TLS certificate revocation and certificate pinning are currently not supported. Revoked certificates are accepted as long as they are otherwise valid. If this is a concern, you may want to use automatically managed certificates with a short validity period.

connect_to_peer(packet_peer: PacketPeerUDP, hostname: String, client_options: TLSOptions = null)

disconnect_from_peer()

Status STATUS_DISCONNECTED = 0

A status representing a PacketPeerDTLS that is disconnected.

Status STATUS_HANDSHAKING = 1

A status representing a PacketPeerDTLS that is currently performing the handshake with a remote peer.

Status STATUS_CONNECTED = 2

A status representing a PacketPeerDTLS that is connected to a remote peer.

Status STATUS_ERROR = 3

A status representing a PacketPeerDTLS in a generic error state.

Status STATUS_ERROR_HOSTNAME_MISMATCH = 4

An error status that shows a mismatch in the DTLS certificate domain presented by the host and the domain requested for validation.

Error connect_to_peer(packet_peer: PacketPeerUDP, hostname: String, client_options: TLSOptions = null) 

Connects a packet_peer beginning the DTLS handshake using the underlying PacketPeerUDP which must be connected (see PacketPeerUDP.connect_to_host()). You can optionally specify the client_options to be used while verifying the TLS connections. See TLSOptions.client() and TLSOptions.client_unsafe().

void disconnect_from_peer() 

Disconnects this peer, terminating the DTLS session.

Status get_status() const 

Returns the status of the connection.

Poll the connection to check for incoming packets. Call this frequently to update the status and keep the connection working.

Please read the User-contributed notes policy before submitting a comment.

---

## PacketPeerStream

**URL:** https://docs.godotengine.org/en/stable/classes/class_packetpeerstream.html

**Contents:**
- PacketPeerStream
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: PacketPeer < RefCounted < Object

Wrapper to use a PacketPeer over a StreamPeer.

PacketStreamPeer provides a wrapper for working using packets over a stream. This allows for using packet based code with StreamPeers. PacketPeerStream implements a custom protocol over the StreamPeer, so the user should not read or write to the wrapped StreamPeer directly.

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

input_buffer_max_size

output_buffer_max_size

int input_buffer_max_size = 65532 

void set_input_buffer_max_size(value: int)

int get_input_buffer_max_size()

There is currently no description for this property. Please help us by contributing one!

int output_buffer_max_size = 65532 

void set_output_buffer_max_size(value: int)

int get_output_buffer_max_size()

There is currently no description for this property. Please help us by contributing one!

StreamPeer stream_peer 

void set_stream_peer(value: StreamPeer)

StreamPeer get_stream_peer()

The wrapped StreamPeer object.

Please read the User-contributed notes policy before submitting a comment.

---

## PacketPeerUDP

**URL:** https://docs.godotengine.org/en/stable/classes/class_packetpeerudp.html

**Contents:**
- PacketPeerUDP
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: PacketPeer < RefCounted < Object

UDP packet peer. Can be used to send and receive raw UDP packets as well as Variants.

Example: Send a packet:

Example: Listen for packets:

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

bind(port: int, bind_address: String = "*", recv_buf_size: int = 65536)

connect_to_host(host: String, port: int)

get_local_port() const

get_packet_ip() const

get_packet_port() const

is_socket_connected() const

join_multicast_group(multicast_address: String, interface_name: String)

leave_multicast_group(multicast_address: String, interface_name: String)

set_broadcast_enabled(enabled: bool)

set_dest_address(host: String, port: int)

Error bind(port: int, bind_address: String = "*", recv_buf_size: int = 65536) 

Binds this PacketPeerUDP to the specified port and bind_address with a buffer size recv_buf_size, allowing it to receive incoming packets.

If bind_address is set to "*" (default), the peer will be bound on all available addresses (both IPv4 and IPv6).

If bind_address is set to "0.0.0.0" (for IPv4) or "::" (for IPv6), the peer will be bound to all available addresses matching that IP type.

If bind_address is set to any valid address (e.g. "192.168.1.101", "::1", etc.), the peer will only be bound to the interface with that address (or fail if no interface with the given address exists).

Closes the PacketPeerUDP's underlying UDP socket.

Error connect_to_host(host: String, port: int) 

Calling this method connects this UDP peer to the given host/port pair. UDP is in reality connectionless, so this option only means that incoming packets from different addresses are automatically discarded, and that outgoing packets are always sent to the connected address (future calls to set_dest_address() are not allowed). This method does not send any data to the remote peer, to do that, use PacketPeer.put_var() or PacketPeer.put_packet() as usual. See also UDPServer.

Note: Connecting to the remote peer does not help to protect from malicious attacks like IP spoofing, etc. Think about using an encryption technique like TLS or DTLS if you feel like your application is transferring sensitive information.

int get_local_port() const 

Returns the local port to which this peer is bound.

String get_packet_ip() const 

Returns the IP of the remote peer that sent the last packet(that was received with PacketPeer.get_packet() or PacketPeer.get_var()).

int get_packet_port() const 

Returns the port of the remote peer that sent the last packet(that was received with PacketPeer.get_packet() or PacketPeer.get_var()).

bool is_bound() const 

Returns whether this PacketPeerUDP is bound to an address and can receive packets.

bool is_socket_connected() const 

Returns true if the UDP socket is open and has been connected to a remote address. See connect_to_host().

Error join_multicast_group(multicast_address: String, interface_name: String) 

Joins the multicast group specified by multicast_address using the interface identified by interface_name.

You can join the same multicast group with multiple interfaces. Use IP.get_local_interfaces() to know which are available.

Note: Some Android devices might require the CHANGE_WIFI_MULTICAST_STATE permission for multicast to work.

Error leave_multicast_group(multicast_address: String, interface_name: String) 

Removes the interface identified by interface_name from the multicast group specified by multicast_address.

void set_broadcast_enabled(enabled: bool) 

Enable or disable sending of broadcast packets (e.g. set_dest_address("255.255.255.255", 4343). This option is disabled by default.

Note: Some Android devices might require the CHANGE_WIFI_MULTICAST_STATE permission and this option to be enabled to receive broadcast packets too.

Error set_dest_address(host: String, port: int) 

Sets the destination address and port for sending packets and variables. A hostname will be resolved using DNS if needed.

Note: set_broadcast_enabled() must be enabled before sending packets to a broadcast address (e.g. 255.255.255.255).

Waits for a packet to arrive on the bound address. See bind().

Note: wait() can't be interrupted once it has been called. This can be worked around by allowing the other party to send a specific "death pill" packet like this:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (sql):
```sql
var peer = PacketPeerUDP.new()

# Optionally, you can select the local port used to send the packet.
peer.bind(4444)

peer.set_dest_address("1.1.1.1", 4433)
peer.put_packet("hello".to_utf8_buffer())
```

Example 2 (gdscript):
```gdscript
var peer

func _ready():
    peer = PacketPeerUDP.new()
    peer.bind(4433)


func _process(_delta):
    if peer.get_available_packet_count() > 0:
        var array_bytes = peer.get_packet()
        var packet_string = array_bytes.get_string_from_ascii()
        print("Received message: ", packet_string)
```

Example 3 (gdscript):
```gdscript
socket = PacketPeerUDP.new()
# Server
socket.set_dest_address("127.0.0.1", 789)
socket.put_packet("Time to stop".to_ascii_buffer())

# Client
while socket.wait() == OK:
    var data = socket.get_packet().get_string_from_ascii()
    if data == "Time to stop":
        return
```

Example 4 (csharp):
```csharp
var socket = new PacketPeerUdp();
// Server
socket.SetDestAddress("127.0.0.1", 789);
socket.PutPacket("Time to stop".ToAsciiBuffer());

// Client
while (socket.Wait() == OK)
{
    string data = socket.GetPacket().GetStringFromASCII();
    if (data == "Time to stop")
    {
        return;
    }
}
```

---

## Resolving crashes on Android

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/android/resolving_crashes_on_android.html

**Contents:**
- Resolving crashes on Android
- Getting Native Debug symbols for official templates
- Getting Native Debug symbols for custom builds
- Uploading Symbols to Google Play Console
- Manually Symbolicating Crash Logs
- User-contributed notes

When your game crashes on Android, you often see obfuscated stack traces in Play Console or other crash reporting tools like Firebase Crashlytics. To make these stack traces human-readable (symbolicated), you need native debug symbols that correspond to your game's exported build.

Godot now provides downloadable native debug symbols for each official export template.

Native debug symbol files are provided for every stable Godot release and can be downloaded from the GitHub release page.

For example, to get the native debug symbols for version 4.5.1.stable:

Go to the 4.5.1.stable release page

Download the release artifact Godot_native_debug_symbols.4.5.1.stable.template_release.android.zip

Your exported template and its native debug symbols must come from the same build, so you can use the official symbols only if you are using the official export templates. If you are building custom export templates, you need to generate matching symbol files yourself.

To do so, add debug_symbols=yes separate_debug_symbols=yes to your scons build command. This will generate a file named android-template-release-native-symbols.zip containing the native debug symbols for your custom build.

If you are building for multiple architectures, you should include the separate_debug_symbols=yes only in the last build command, similar to how generate_android_binaries=yes is used.

Follow these steps to upload the native debug symbols:

In the left menu, navigate to Test and release > Latest releases and bundles.

Now choose the relevant bundle and open it.

Select the Downloads tab, and scroll down to the Assets section.

Next to Native debug symbols, click the upload arrow icon.

Select and upload the corresponding native debug symbols file for that build version.

Alternatively, you can upload the symbols when creating a new release:

On the Create release page, locate your new release bundle.

Click the three-dot menu beside it.

Choose Upload native debug symbols (.zip) from the menu.

Select and upload the corresponding native debug symbols file for that build version.

You can also symbolicate the crash logs manually using the ndk-stack tool included in the Android NDK.

If you already have the Android SDK installed, you can find the ndk-stack tool inside the ndk folder in your SDK location. Otherwise, you can download the NDK directly from the NDK downloads page.

Extract the native debug symbols zip you downloaded earlier (or generated with your custom build).

Save your crash log to a text file (for example, crash.txt).

Run ndk-stack with the path to the symbol directory that matches the crash's CPU architecture (for example, arm64-v8a):

The output will display a symbolicated trace, showing file names and line numbers in Godot's source code (or your custom build).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
scons platform=android target=template_release debug_symbols=yes separate_debug_symbols=yes generate_android_binaries=yes
```

Example 2 (unknown):
```unknown
scons platform=android arch=arm32 target=template_release debug_symbols=yes
scons platform=android arch=arm64 target=template_release debug_symbols=yes
scons platform=android arch=x86_32 target=template_release debug_symbols=yes
scons platform=android arch=x86_64 target=template_release debug_symbols=yes separate_debug_symbols=yes generate_android_binaries=yes
```

Example 3 (unknown):
```unknown
ndk-stack -sym path/to/native_debug_symbols/arm64-v8a/ -dump crash.txt
```

---

## Running Godot apps on macOS

**URL:** https://docs.godotengine.org/en/stable/tutorials/export/running_on_macos.html

**Contents:**
- Running Godot apps on macOS
- App is signed, notarized and distributed via App Store
- App is signed, notarized and distributed outside App Store
- App is signed (including ad-hoc signatures) but not notarized
- App is not signed, executable is linker-signed
- Neither app nor executable is signed (relevant for Apple Silicon Macs only)
- User-contributed notes

This page covers running Godot projects on macOS. If you haven't exported your project yet, read Exporting for macOS first.

By default, macOS will run only applications that are signed and notarized.

When running an app from the Downloads folder or when still in quarantine, Gatekeeper will perform path randomization as a security measure. This breaks access to relative paths from the app, which the app relies upon to work. To resolve this issue, move the app to the /Applications folder.

In general, macOS apps should avoid relying on relative paths from the application folder.

Depending on the way a macOS app is signed and distributed, the following scenarios are possible:

App developers need to join the Apple Developer Program, and configure signing and notarization options during export, then upload the app to the App Store.

The app should run out of the box, without extra user interaction required.

App developers need to join the Apple Developer Program, and configure signing and notarization options during export, then distribute the app as ".DMG" or ".ZIP" archive.

When you run the app for the first time, the following dialog is displayed:

Click Open to start the app.

If you see the following warning dialog, your Mac is set up to allow apps only from the App Store.

To allow third-party apps, open System Preferences, click Security & Privacy, then click General, unlock settings, and select App Store and identified developers.

App developer used self-signed certificate or ad-hoc signing (default Godot behavior for exported project).

When you run the app for the first time, the following dialog is displayed:

To run this app, you can temporarily override Gatekeeper:

Either open System Preferences, click Security & Privacy, then click General, and click Open Anyway.

Or, right-click (Control-click) on the app icon in the Finder window and select Open from the menu.

Then click Open in the confirmation dialog.

Enter your password if you're prompted.

Another option is to disable Gatekeeper entirely. Note that this does decrease the security of your computer by allowing you to run any software you want. To do this, run sudo spctl --master-disable in the Terminal, enter your password, and then the Anywhere option will be available:

Note that Gatekeeper will re-enable itself when macOS updates.

App is built using official export templates, but it is not signed.

When you run the app for the first time, the following dialog is displayed:

To run this app, you should remove the quarantine extended file attribute manually:

Open Terminal.app (press Cmd + Space and enter Terminal).

Navigate to the folder containing the target application.

Use the cd path_to_the_app_folder command, e.g. cd ~/Downloads/ if it's in the Downloads folder.

Run the command xattr -dr com.apple.quarantine "Unsigned Game.app" (including quotation marks and .app extension).

App is built using custom export templates, compiled using OSXCross, and it is not signed at all.

When you run the app for the first time, the following dialog is displayed:

To run this app, you can ad-hoc sign it yourself:

Install Xcode for the App Store, start it and confirm command line tools installation.

Open Terminal.app (press Cmd + Space and enter Terminal).

Navigate to the folder containing the target application.

Use the cd path_to_the_app_folder command, e.g. cd ~/Downloads/ if it's in the Downloads folder.

Run the following commands:

xattr -dr com.apple.quarantine "Unsigned Game.app" (including quotation marks and ".app" extension).

codesign -s - --force --deep "Unsigned Game.app" (including quotation marks and ".app" extension).

Please read the User-contributed notes policy before submitting a comment.

---

## StreamPeerTCP

**URL:** https://docs.godotengine.org/en/stable/classes/class_streampeertcp.html

**Contents:**
- StreamPeerTCP
- Description
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: StreamPeer < RefCounted < Object

A stream peer that handles TCP connections.

A stream peer that handles TCP connections. This object can be used to connect to TCP servers, or also is returned by a TCP server.

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

bind(port: int, host: String = "*")

connect_to_host(host: String, port: int)

disconnect_from_host()

get_connected_host() const

get_connected_port() const

get_local_port() const

set_no_delay(enabled: bool)

Status STATUS_NONE = 0

The initial status of the StreamPeerTCP. This is also the status after disconnecting.

Status STATUS_CONNECTING = 1

A status representing a StreamPeerTCP that is connecting to a host.

Status STATUS_CONNECTED = 2

A status representing a StreamPeerTCP that is connected to a host.

Status STATUS_ERROR = 3

A status representing a StreamPeerTCP in error state.

Error bind(port: int, host: String = "*") 

Opens the TCP socket, and binds it to the specified local address.

This method is generally not needed, and only used to force the subsequent call to connect_to_host() to use the specified host and port as source address. This can be desired in some NAT punchthrough techniques, or when forcing the source network interface.

Error connect_to_host(host: String, port: int) 

Connects to the specified host:port pair. A hostname will be resolved if valid. Returns @GlobalScope.OK on success.

void disconnect_from_host() 

Disconnects from host.

String get_connected_host() const 

Returns the IP of this peer.

int get_connected_port() const 

Returns the port of this peer.

int get_local_port() const 

Returns the local port to which this peer is bound.

Status get_status() const 

Returns the status of the connection.

Poll the socket, updating its state. See get_status().

void set_no_delay(enabled: bool) 

If enabled is true, packets will be sent immediately. If enabled is false (the default), packet transfers will be delayed and combined using Nagle's algorithm.

Note: It's recommended to leave this disabled for applications that send large packets or need to transfer a lot of data, as enabling this can decrease the total available bandwidth.

Please read the User-contributed notes policy before submitting a comment.

---

## StreamPeerTLS

**URL:** https://docs.godotengine.org/en/stable/classes/class_streampeertls.html

**Contents:**
- StreamPeerTLS
- Description
- Tutorials
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: StreamPeer < RefCounted < Object

A stream peer that handles TLS connections.

A stream peer that handles TLS connections. This object can be used to connect to a TLS server or accept a single TLS client connection.

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

accept_stream(stream: StreamPeer, server_options: TLSOptions)

connect_to_stream(stream: StreamPeer, common_name: String, client_options: TLSOptions = null)

disconnect_from_stream()

Status STATUS_DISCONNECTED = 0

A status representing a StreamPeerTLS that is disconnected.

Status STATUS_HANDSHAKING = 1

A status representing a StreamPeerTLS during handshaking.

Status STATUS_CONNECTED = 2

A status representing a StreamPeerTLS that is connected to a host.

Status STATUS_ERROR = 3

A status representing a StreamPeerTLS in error state.

Status STATUS_ERROR_HOSTNAME_MISMATCH = 4

An error status that shows a mismatch in the TLS certificate domain presented by the host and the domain requested for validation.

Error accept_stream(stream: StreamPeer, server_options: TLSOptions) 

Accepts a peer connection as a server using the given server_options. See TLSOptions.server().

Error connect_to_stream(stream: StreamPeer, common_name: String, client_options: TLSOptions = null) 

Connects to a peer using an underlying StreamPeer stream and verifying the remote certificate is correctly signed for the given common_name. You can pass the optional client_options parameter to customize the trusted certification authorities, or disable the common name verification. See TLSOptions.client() and TLSOptions.client_unsafe().

void disconnect_from_stream() 

Disconnects from host.

Status get_status() const 

Returns the status of the connection.

StreamPeer get_stream() const 

Returns the underlying StreamPeer connection, used in accept_stream() or connect_to_stream().

Poll the connection to check for incoming bytes. Call this right before StreamPeer.get_available_bytes() for it to work properly.

Please read the User-contributed notes policy before submitting a comment.

---

## StreamPeer

**URL:** https://docs.godotengine.org/en/stable/classes/class_streampeer.html

**Contents:**
- StreamPeer
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Inherited By: StreamPeerBuffer, StreamPeerExtension, StreamPeerGZIP, StreamPeerTCP, StreamPeerTLS

Abstract base class for interacting with streams.

StreamPeer is an abstract base class mostly used for stream-based protocols (such as TCP). It provides an API for sending and receiving data through streams as raw data or strings.

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

get_available_bytes() const

get_partial_data(bytes: int)

get_string(bytes: int = -1)

get_utf8_string(bytes: int = -1)

get_var(allow_objects: bool = false)

put_data(data: PackedByteArray)

put_double(value: float)

put_float(value: float)

put_half(value: float)

put_partial_data(data: PackedByteArray)

put_string(value: String)

put_utf8_string(value: String)

put_var(value: Variant, full_objects: bool = false)

bool big_endian = false 

void set_big_endian(value: bool)

bool is_big_endian_enabled()

If true, this StreamPeer will using big-endian format for encoding and decoding.

Gets a signed byte from the stream.

Gets a signed 16-bit value from the stream.

Gets a signed 32-bit value from the stream.

Gets a signed 64-bit value from the stream.

int get_available_bytes() const 

Returns the number of bytes this StreamPeer has available.

Array get_data(bytes: int) 

Returns a chunk data with the received bytes. The number of bytes to be received can be requested in the bytes argument. If not enough bytes are available, the function will block until the desired amount is received. This function returns two values, an Error code and a data array.

Gets a double-precision float from the stream.

Gets a single-precision float from the stream.

Gets a half-precision float from the stream.

Array get_partial_data(bytes: int) 

Returns a chunk data with the received bytes. The number of bytes to be received can be requested in the bytes argument. If not enough bytes are available, the function will return how many were actually received. This function returns two values: an Error code and a data array.

String get_string(bytes: int = -1) 

Gets an ASCII string with byte-length bytes from the stream. If bytes is negative (default) the length will be read from the stream using the reverse process of put_string().

Gets an unsigned byte from the stream.

Gets an unsigned 16-bit value from the stream.

Gets an unsigned 32-bit value from the stream.

Gets an unsigned 64-bit value from the stream.

String get_utf8_string(bytes: int = -1) 

Gets a UTF-8 string with byte-length bytes from the stream (this decodes the string sent as UTF-8). If bytes is negative (default) the length will be read from the stream using the reverse process of put_utf8_string().

Variant get_var(allow_objects: bool = false) 

Gets a Variant from the stream. If allow_objects is true, decoding objects is allowed.

Internally, this uses the same decoding mechanism as the @GlobalScope.bytes_to_var() method.

Warning: Deserialized objects can contain code which gets executed. Do not use this option if the serialized object comes from untrusted sources to avoid potential security threats such as remote code execution.

void put_8(value: int) 

Puts a signed byte into the stream.

void put_16(value: int) 

Puts a signed 16-bit value into the stream.

void put_32(value: int) 

Puts a signed 32-bit value into the stream.

void put_64(value: int) 

Puts a signed 64-bit value into the stream.

Error put_data(data: PackedByteArray) 

Sends a chunk of data through the connection, blocking if necessary until the data is done sending. This function returns an Error code.

void put_double(value: float) 

Puts a double-precision float into the stream.

void put_float(value: float) 

Puts a single-precision float into the stream.

void put_half(value: float) 

Puts a half-precision float into the stream.

Array put_partial_data(data: PackedByteArray) 

Sends a chunk of data through the connection. If all the data could not be sent at once, only part of it will. This function returns two values, an Error code and an integer, describing how much data was actually sent.

void put_string(value: String) 

Puts a zero-terminated ASCII string into the stream prepended by a 32-bit unsigned integer representing its size.

Note: To put an ASCII string without prepending its size, you can use put_data():

void put_u8(value: int) 

Puts an unsigned byte into the stream.

void put_u16(value: int) 

Puts an unsigned 16-bit value into the stream.

void put_u32(value: int) 

Puts an unsigned 32-bit value into the stream.

void put_u64(value: int) 

Puts an unsigned 64-bit value into the stream.

void put_utf8_string(value: String) 

Puts a zero-terminated UTF-8 string into the stream prepended by a 32 bits unsigned integer representing its size.

Note: To put a UTF-8 string without prepending its size, you can use put_data():

void put_var(value: Variant, full_objects: bool = false) 

Puts a Variant into the stream. If full_objects is true encoding objects is allowed (and can potentially include code).

Internally, this uses the same encoding mechanism as the @GlobalScope.var_to_bytes() method.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
put_data("Hello world".to_ascii_buffer())
```

Example 2 (unknown):
```unknown
PutData("Hello World".ToAsciiBuffer());
```

Example 3 (unknown):
```unknown
put_data("Hello world".to_utf8_buffer())
```

Example 4 (unknown):
```unknown
PutData("Hello World".ToUtf8Buffer());
```

---

## TCPServer

**URL:** https://docs.godotengine.org/en/stable/classes/class_tcpserver.html

**Contents:**
- TCPServer
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

A TCP server. Listens to connections on a port and returns a StreamPeerTCP when it gets an incoming connection.

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

get_local_port() const

is_connection_available() const

listen(port: int, bind_address: String = "*")

int get_local_port() const 

Returns the local port this server is listening to.

bool is_connection_available() const 

Returns true if a connection is available for taking.

bool is_listening() const 

Returns true if the server is currently listening for connections.

Error listen(port: int, bind_address: String = "*") 

Listen on the port binding to bind_address.

If bind_address is set as "*" (default), the server will listen on all available addresses (both IPv4 and IPv6).

If bind_address is set as "0.0.0.0" (for IPv4) or "::" (for IPv6), the server will listen on all available addresses matching that IP type.

If bind_address is set to any valid address (e.g. "192.168.1.101", "::1", etc.), the server will only listen on the interface with that address (or fail if no interface with the given address exists).

StreamPeerTCP take_connection() 

If a connection is available, returns a StreamPeerTCP with the connection.

Please read the User-contributed notes policy before submitting a comment.

---

## The JavaScriptBridge singleton

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/web/javascript_bridge.html

**Contents:**
- The JavaScriptBridge singleton
- Interacting with JavaScript
- Callbacks
- Can I use my favorite library?
- The eval interface
- Downloading files
- User-contributed notes

In web builds, the JavaScriptBridge singleton allows interaction with JavaScript and web browsers, and can be used to implement some functionalities unique to the web platform.

Sometimes, when exporting Godot for the Web, it might be necessary to interface with external JavaScript code like third-party SDKs, libraries, or simply to access browser features that are not directly exposed by Godot.

The JavaScriptBridge singleton provides methods to wrap a native JavaScript object into a Godot JavaScriptObject that tries to feel natural in the context of Godot scripting (e.g. GDScript and C#).

The JavaScriptBridge.get_interface() method retrieves an object in the global scope.

The JavaScriptBridge.create_object() creates a new object via the JavaScript new constructor.

As you can see, by wrapping JavaScript objects into JavaScriptObject you can interact with them like they were native Godot objects, calling their methods, and retrieving (or even setting) their properties.

Base types (int, floats, strings, booleans) are automatically converted (floats might lose precision when converted from Godot to JavaScript). Anything else (i.e. objects, arrays, functions) are seen as JavaScriptObjects themselves.

Calling JavaScript code from Godot is nice, but sometimes you need to call a Godot function from JavaScript instead.

This case is a bit more complicated. JavaScript relies on garbage collection, while Godot uses reference counting for memory management. This means you have to explicitly create callbacks (which are returned as JavaScriptObjects themselves) and you have to keep their reference.

Arguments passed by JavaScript to the callback will be passed as a single Godot Array.

Callback methods created via JavaScriptBridge.get_interface() (_my_callback in the above example) must take exactly one Array argument, which is going to be the JavaScript arguments object converted to an array. Otherwise, the callback method will not be called.

Here is another example that asks the user for the Notification permission and waits asynchronously to deliver a notification if the permission is granted:

You most likely can. First, you have to include your library in the page. You can customize the Head Include during export (see below), or even write your own template.

In the example below, we customize the Head Include to add an external library (axios) from a content delivery network, and a second <script> tag to define our own custom function:

We can then access both the library and the function from Godot, like we did in previous examples:

The eval method works similarly to the JavaScript function of the same name. It takes a string as an argument and executes it as JavaScript code. This allows interacting with the browser in ways not possible with script languages integrated into Godot.

The value of the last JavaScript statement is converted to a GDScript value and returned by eval() under certain circumstances:

JavaScript number is returned as float

JavaScript boolean is returned as bool

JavaScript string is returned as String

JavaScript ArrayBuffer, TypedArray, and DataView are returned as PackedByteArray

Any other JavaScript value is returned as null.

HTML5 export templates may be built without support for the singleton to improve security. With such templates, and on platforms other than HTML5, calling JavaScriptBridge.eval will also return null. The availability of the singleton can be checked with the web feature tag:

GDScript's multi-line strings, surrounded by 3 quotes """ as in my_func3() above, are useful to keep JavaScript code readable.

The eval method also accepts a second, optional Boolean argument, which specifies whether to execute the code in the global execution context, defaulting to false to prevent polluting the global namespace:

Downloading files (e.g. a save game) from the Godot Web export to the user's computer can be done by directly interacting with JavaScript, but given it is a very common use case, Godot exposes this functionality to scripting via a dedicated JavaScriptBridge.download_buffer() function which lets you download any generated buffer.

Here is a minimal example on how to use it:

And here is a more complete example on how to download a previously saved file:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Node

func _ready():
    # Retrieve the `window.console` object.
    var console = JavaScriptBridge.get_interface("console")
    # Call the `window.console.log()` method.
    console.log("test")
```

Example 2 (gdscript):
```gdscript
extends Node

func _ready():
    # Call the JavaScript `new` operator on the `window.Array` object.
    # Passing 10 as argument to the constructor:
    # JS: `new Array(10);`
    var arr = JavaScriptBridge.create_object("Array", 10)
    # Set the first element of the JavaScript array to the number 42.
    arr[0] = 42
    # Call the `pop` function on the JavaScript array.
    arr.pop()
    # Print the value of the `length` property of the array (9 after the pop).
    print(arr.length)
```

Example 3 (gdscript):
```gdscript
extends Node

# Here we create a reference to the `_my_callback` function (below).
# This reference will be kept until the node is freed.
var _callback_ref = JavaScriptBridge.create_callback(_my_callback)

func _ready():
    # Get the JavaScript `window` object.
    var window = JavaScriptBridge.get_interface("window")
    # Set the `window.onbeforeunload` DOM event listener.
    window.onbeforeunload = _callback_ref

func _my_callback(args):
    # Get the first argument (the DOM event in our case).
    var js_event = args[0]
    # Call preventDefault and set the `returnValue` property of the DOM event.
    js_event.preventDefault()
    js_event.returnValue = ''
```

Example 4 (gdscript):
```gdscript
extends Node

# Here we create a reference to the `_on_permissions` function (below).
# This reference will be kept until the node is freed.
var _permission_callback = JavaScriptBridge.create_callback(_on_permissions)

func _ready():
    # NOTE: This is done in `_ready` for simplicity, but SHOULD BE done in response
    # to user input instead (e.g. during `_input`, or `button_pressed` event, etc.),
    # otherwise it might not work.

    # Get the `window.Notification` JavaScript object.
    var notification = JavaScriptBridge.get_interface("Notification")
    # Call the `window.Notification.requestPermission` method which returns a JavaScript
    # Promise, and bind our callback to it.
    notification.requestPermission().then(_permission_callback)

func _on_permissions(args):
    # The first argument of this callback is the string "granted" if the permission is granted.
    var permission = args[0]
    if permission == "granted":
        print("Permission granted, sending notification.")
        # Create the notification: `new Notification("Hi there!")`
        JavaScriptBridge.create_object("Notification", "Hi there!")
    else:
        print("No notification permission.")
```

---

## Troubleshooting

**URL:** https://docs.godotengine.org/en/stable/tutorials/troubleshooting.html

**Contents:**
- Troubleshooting
- The editor runs slowly and uses all my CPU and GPU resources, making my computer noisy
- The editor stutters and flickers on my variable refresh rate monitor (G-Sync/FreeSync)
- The editor or project takes a very long time to start
- The Godot editor appears frozen after clicking the system console
- The Godot editor's macOS dock icon gets duplicated every time it is manually moved
- Some text such as "NO DC" appears in the top-left corner of the Project Manager and editor window
- A microphone or "refresh" icon appears in the bottom-right corner of the Project Manager and editor window
- The editor or project appears overly sharp or blurry
- The editor or project appears to have washed out colors

This page lists common issues encountered when using Godot and possible solutions.

See Using the Web editor for caveats specific to the Web version of the Godot editor.

This is a known issue, especially on macOS since most Macs have Retina displays. Due to Retina displays' higher pixel density, everything has to be rendered at a higher resolution. This increases the load on the GPU and decreases perceived performance.

There are several ways to improve performance and battery life:

In 3D, click the Perspective button in the top left corner and enable Half Resolution. The 3D viewport will now be rendered at half resolution, which can be up to 4 times faster.

Open the Editor Settings and increase the value of Low Processor Mode Sleep (µsec) to 33000 (30 FPS). This value determines the amount of microseconds between frames to render. Higher values will make the editor feel less reactive, but will help decrease CPU and GPU usage significantly.

If you have a node that causes the editor to redraw continuously (such as particles), hide it and show it using a script in the _ready() method. This way, it will be hidden in the editor, but will still be visible in the running project.

This is a known issue. Variable refresh rate monitors need to adjust their gamma curves continuously to emit a consistent amount of light over time. This can cause flicker to appear in dark areas of the image when the refresh rate varies a lot, which occurs as the Godot editor only redraws when necessary.

There are several workarounds for this:

Enable Interface > Editor > Update Continuously in the Editor Settings. Keep in mind this will increase power usage and heat/noise emissions since the editor will now be rendering constantly, even if nothing has changed on screen. To alleviate this, you can increase Low Processor Mode Sleep (µsec) to 33000 (30 FPS) in the Editor Settings. This value determines the amount of microseconds between frames to render. Higher values will make the editor feel less reactive, but will help decrease CPU and GPU usage significantly.

Alternatively, disable variable refresh rate on your monitor or in the graphics driver.

VRR flicker can be reduced on some displays using the VRR Control or Fine Tune Dark Areas options in your monitor's OSD. These options may increase input lag or result in crushed blacks.

If using an OLED display, use the Black (OLED) editor theme preset in the Editor Settings. This hides VRR flicker thanks to OLED's perfect black levels.

When using one of the Vulkan-based renderers (Forward+ or Mobile), the first startup is expected to be relatively long. This is because shaders need to be compiled before they can be cached. Shaders also need to be cached again after updating Godot, after updating graphics drivers or after switching graphics cards.

If the issue persists after the first startup, this is a known bug on Windows when you have specific USB peripherals connected. In particular, Corsair's iCUE software seems to cause this bug. Try updating your USB peripherals' drivers to their latest version. If the bug persists, you need to disconnect the specific peripheral before opening the editor. You can then connect the peripheral again.

Firewall software such as Portmaster may also cause the debug port to be blocked. This causes the project to take a long time to start, while being unable to use debugging features in the editor (such as viewing print() output). You can work this around by changing the debug port used by the project in the Editor Settings (Network > Debug > Remote Port). The default is 6007; try another value that is greater than 1024, such as 7007.

On Windows, when loading the project for the first time after the PC is turned on, Windows Defender will cause the filesystem cache validation on project startup to take significantly longer. This is especially noticeable in projects with a large number of files. Consinder adding the project folder to the list of exclusions by going to Virus & threat protection > Virus & threat protection settings > Add or remove exclusions.

When running Godot on Windows with the system console enabled, you can accidentally enable selection mode by clicking inside the command window. This Windows-specific behavior pauses the application to let you select text inside the system console. Godot cannot override this system-specific behavior.

To solve this, select the system console window and press Enter to leave selection mode.

If you open the Godot editor and manually change the position of the dock icon, then restart the editor, you will get a duplicate dock icon all the way to the right of the dock.

This is due to a design limitation of the macOS dock. The only known way to resolve this would be to merge the project manager and editor into a single process, which means the project manager would no longer spawn a separate process when starting the editor. While using a single process instance would bring several benefits, it isn't planned to be done in the near future due to the complexity of the task.

To avoid this issue, keep the Godot editor's dock icon at its default location as created by macOS.

This is caused by the NVIDIA graphics driver injecting an overlay to display information.

To disable this overlay on Windows, restore your graphics driver settings to the default values in the NVIDIA Control Panel.

To disable this overlay on Linux, open nvidia-settings, go to X Screen 0 > OpenGL Settings then uncheck Enable Graphics API Visual Indicator.

This is caused by the NVIDIA graphics driver injecting an overlay to display instant replay information on ShadowPlay recording. This overlay can only be seen on Windows, as Linux does not have support for ShadowPlay.

To disable this overlay, press Alt + Z (default shortcut for the NVIDIA overlay) and disable Settings > HUD Layout > Status Indicator in the NVIDIA overlay.

Alternatively, you can install the new NVIDIA app <https://www.nvidia.com/en-us/software/nvidia-app/> which replaces GeForce Experience and does not suffer from this issue. Unlike GeForce Experience, the NVIDIA app draws the replay indicator in the corner of the screen as opposed to the corner of each window.

Correct appearance (left), oversharpened appearance due to graphics driver sharpening (right)

If the editor or project appears overly sharp, this is likely due to image sharpening being forced on all Vulkan or OpenGL applications by your graphics driver. You can disable this behavior in the graphics driver's control panel:

NVIDIA (Windows): Open the start menu and choose NVIDIA Control Panel. Open the Manage 3D settings tab on the left. In the list in the middle, scroll to Image Sharpening and set it to Sharpening Off.

AMD (Windows): Open the start menu and choose AMD Software. Click the settings "cog" icon in the top-right corner. Go to the Graphics tab then disable Radeon Image Sharpening.

If the editor or project appears overly blurry, this is likely due to FXAA being forced on all Vulkan or OpenGL applications by your graphics driver.

NVIDIA (Windows): Open the start menu and choose NVIDIA Control Panel. Open the Manage 3D settings tab on the left. In the list in the middle, scroll to Fast Approximate Antialiasing and set it to Application Controlled.

NVIDIA (Linux): Open the applications menu and choose NVIDIA X Server Settings. Select to Antialiasing Settings on the left, then uncheck Enable FXAA.

AMD (Windows): Open the start menu and choose AMD Software. Click the settings "cog" icon in the top-right corner. Go to the Graphics tab, scroll to the bottom and click Advanced to unfold its settings. Disable Morphological Antialiasing.

Third-party vendor-independent utilities such as vkBasalt may also force sharpening or FXAA on all Vulkan applications. You may want to check their configuration as well.

After changing options in the graphics driver or third-party utilities, restart Godot to make the changes effective.

If you still wish to force sharpening or FXAA on other applications, it's recommended to do so on a per-application basis using the application profiles system provided by graphics drivers' control panels.

On Windows, this is usually caused by incorrect OS or monitor settings, as Godot currently does not support HDR output (even though it may internally render in HDR).

As most displays are not designed to display SDR content in HDR mode, it is recommended to disable HDR in the Windows settings when not running applications that use HDR output. On Windows 11, this can be done by pressing Windows + Alt + B (this shortcut is part of the Xbox Game Bar app). To toggle HDR automatically based on applications currently running, you can use AutoActions.

If you insist on leaving HDR enabled, it is possible to somewhat improve the result by ensuring the display is configured to use HGIG tonemapping (as opposed to DTM), then using the Windows HDR calibration app. It is also strongly recommended to use Windows 11 instead of Windows 10 when using HDR. The end result will still likely be inferior to disabling HDR on the display, though.

Support for HDR output is planned in a future release.

This is a known issue on Linux with NVIDIA graphics when using the proprietary driver. There is no definitive fix yet, as suspend on Linux + NVIDIA is often buggy when OpenGL or Vulkan is involved. The Compatibility rendering method (which uses OpenGL) is generally less prone to suspend-related issues compared to the Forward+ and Mobile renderers (which use Vulkan).

The NVIDIA driver offers an experimental option to preserve video memory after suspend which may resolve this issue. This option has been reported to work better with more recent NVIDIA driver versions.

To avoid losing work, save scenes in the editor before putting the PC to sleep.

This is usually caused by forgetting to specify a filter for non-resource files in the Export dialog. By default, Godot will only include actual resources into the PCK file. Some files commonly used, such as JSON files, are not considered resources. For example, if you load test.json in the exported project, you need to specify *.json in the non-resource export filter. See Resource options for more information.

Also, note that files and folders whose names begin with a period will never be included in the exported project. This is done to prevent version control folders like .git from being included in the exported PCK file.

On Windows, this can also be due to case sensitivity issues. If you reference a resource in your script with a different case than on the filesystem, loading will fail once you export the project. This is because the virtual PCK filesystem is case-sensitive, while Windows's filesystem is case-insensitive by default.

This could be caused by a number of things such as an editor plugin, GDExtension addon, or something else. In this scenario it's recommended that you open the project in recovery mode, and attempt to find and fix whatever is causing the crashes. See the Project Manager page for more information.

Please read the User-contributed notes policy before submitting a comment.

---

## Upgrading from Godot 4.4 to Godot 4.5

**URL:** https://docs.godotengine.org/en/stable/tutorials/migrating/upgrading_to_godot_4.5.html

**Contents:**
- Upgrading from Godot 4.4 to Godot 4.5
- Breaking changes
  - Core
  - Rendering
  - GLTF
  - Text
  - XR
  - Editor plugins
- Behavior changes
  - TileMapLayer

For most games and apps made with 4.4 it should be relatively safe to migrate to 4.5. This page intends to cover everything you need to pay attention to when migrating your project.

If you are migrating from 4.4 to 4.5, the breaking changes listed here might affect you. Changes are grouped by areas/systems.

In order to support new Google Play requirements Android now requires targeting .NET 9 when exporting C# projects to Android, other platforms continue to use .NET 8 as the minimum required version but newer versions are supported and encouraged.

If you are using C# in your project and want to export to Android, you will need to upgrade your project to .NET 9 (see Upgrading to a new .NET version for instructions).

This article indicates whether each breaking change affects GDScript and whether the C# breaking change is binary compatible or source compatible:

Binary compatible - Existing binaries will load and execute successfully without recompilation, and the run-time behavior won't change.

Source compatible - Source code will compile successfully without changes when upgrading Godot.

Method set_scope replaced by set_method

Method get_rpc_config renamed to get_node_rpc_config

Method set_name changes name parameter type from String to StringName

Method file_dialog_show adds a new parent_window_id optional parameter

Method file_dialog_with_options_show adds a new parent_window_id optional parameter

Method texture_create_from_extension adds a new mipmaps optional parameter

Method instance_reset_physics_interpolation removed

Method instance_set_interpolated removed

In C#, the enum RenderingDevice.Features breaks compatibility because of the way the bindings generator detects the enum prefix. New members were added to the enum in GH-103941 that caused the enum member Address to be renamed to BufferDeviceAddress.

Property byte_offset changes type metadata from int32 to int64

Property component_type changes type from int to GLTFAccessor::GLTFComponentType

Property count changes type metadata from int32 to int64

Property sparse_count changes type metadata from int32 to int64

Property sparse_indices_byte_offset changes type metadata from int32 to int64

Property sparse_indices_component_type changes type from int to GLTFAccessor::GLTFComponentType

Property sparse_values_byte_offset changes type metadata from int32 to int64

Property byte_length changes type metadata from int32 to int64

Property byte_offset changes type metadata from int32 to int64

Property byte_stride changes type metadata from int32 to int64

As a result of changing the type metadata, the C# bindings changed the type from int (32-bytes) to long (64-bytes).

Method draw_char adds a new oversampling optional parameter

Method draw_char_outline adds a new oversampling optional parameter

Method draw_multiline_string adds a new oversampling optional parameter

Method draw_multiline_string_outline adds a new oversampling optional parameter

Method draw_string adds a new oversampling optional parameter

Method draw_string_outline adds a new oversampling optional parameter

Method draw_char adds a new oversampling optional parameter

Method draw_char_outline adds a new oversampling optional parameter

Method draw_multiline_string adds a new oversampling optional parameter

Method draw_multiline_string_outline adds a new oversampling optional parameter

Method draw_string adds a new oversampling optional parameter

Method draw_string_outline adds a new oversampling optional parameter

Method add_image adds a new alt_text optional parameter

Method add_image replaced size_in_percent parameter by width_in_percent and height_in_percent

Method push_strikethrough adds optional color parameter

Method push_table adds a new name optional parameter

Method push_underline adds optional color parameter

Method update_image replaced size_in_percent parameter by width_in_percent and height_in_percent

Method draw adds a new oversampling optional parameter

Method draw_outline adds a new oversampling optional parameter

Method draw adds a new oversampling optional parameter

Method draw_dropcap adds a new oversampling optional parameter

Method draw_dropcap_outline adds a new oversampling optional parameter

Method draw_line adds a new oversampling optional parameter

Method draw_line_outline adds a new oversampling optional parameter

Method draw_outline adds a new oversampling optional parameter

Method font_draw_glyph adds a new oversampling optional parameter

Method font_draw_glyph_outline adds a new oversampling optional parameter

Method shaped_text_draw adds a new oversampling optional parameter

Method shaped_text_draw_outline adds a new oversampling optional parameter

Method add_button adds a new alt_text optional parameter

Method _font_draw_glyph adds a new oversampling optional parameter

Method _font_draw_glyph_outline adds a new oversampling optional parameter

Method _shaped_text_draw adds a new oversampling optional parameter

Method _shaped_text_draw_outline adds a new oversampling optional parameter

Method register_composition_layer_provider changes extension parameter type from OpenXRExtensionWrapperExtension to OpenXRExtensionWrapper

Method register_projection_views_extension changes extension parameter type from OpenXRExtensionWrapperExtension to OpenXRExtensionWrapper

Method unregister_composition_layer_provider changes extension parameter type from OpenXRExtensionWrapperExtension to OpenXRExtensionWrapper

Method unregister_projection_views_extension changes extension parameter type from OpenXRExtensionWrapperExtension to OpenXRExtensionWrapper

OpenXRBindingModifierEditor

Type OpenXRBindingModifierEditor changed API type from Core to Editor

OpenXRInteractionProfileEditor

Type OpenXRInteractionProfileEditor changed API type from Core to Editor

OpenXRInteractionProfileEditorBase

Type OpenXRInteractionProfileEditorBase changed API type from Core to Editor

Classes OpenXRBindingModifierEditor, OpenXRInteractionProfileEditor, and OpenXRInteractionProfileEditorBase are only available in the editor. Using them outside of the editor will result in a compilation error.

In C#, this means the types are moved from the GodotSharp assembly to the GodotSharpEditor assembly. Make sure to wrap code that uses these types in a #if TOOLS block to ensure they are not included in an exported game.

This change was also backported to 4.4.1.

Method get_forced_export_files adds a new preset optional parameter

EditorUndoRedoManager

Method create_action adds a new mark_unsaved optional parameter

EditorExportPlatformExtension

Method _get_option_icon changes return type from ImageTexture to Texture2D

In 4.5, some behavior changes have been introduced, which might require you to adjust your project.

TileMapLayer.get_coords_for_body_rid() will return different values in 4.5 compared to 4.4, as TileMapLayer physics chunking is enabled by default. Higher values of TileMapLayer.physics_quadrant_size will make this function less precise. To get the exact cell coordinates like in 4.4 and prior versions, you need to set TileMapLayer.physics_quadrant_size to 1, which disables physics chunking.

A fix has been made to the 3D model importers to correctly handle non-joint nodes within a skeleton hierarchy (GH-104184). To preserve compatibility, the default behavior is to import existing files with the same behavior as before (GH-107352). New .gltf, .glb, .blend, and .fbx files (without a corresponding .import file) will be imported with the new behavior. However, for existing files, if you want to use the new behavior, you must change the "Naming Version" option at the bottom of the Import dock:

Resource.duplicate(true) (which performs deep duplication) now only duplicates resources internal to the resource file it's called on. In 4.4, this duplicated everything instead, including external resources. If you were deep-duplicating a resource that contained references to other external resources, those external resources aren't duplicated anymore. You must call Resource.duplicate_deep(RESOURCE_DEEP_DUPLICATE_ALL) instead to keep the old behavior.

ProjectSettings.add_property_info() now prints a warning when the dictionary parameter has missing keys or invalid keys. Most importantly, it will now warn when a usage key is passed, as this key is not used. This was also the case before 4.5, but it was silently ignored instead. As a reminder, to set property usage information correctly, you must use ProjectSettings.set_as_basic(), ProjectSettings.set_restart_if_changed(), or ProjectSettings.set_as_internal() instead.

In C#, StringExtensions.PathJoin now avoids adding an extra path separator when the original string is empty, or when the appended path starts with a path separator (GH-105281).

In C#, StringExtensions.GetExtension now returns an empty string instead of the original string when the original string does not contain an extension (GH-108041).

In C#, the Quaternion(Vector3, Vector3) constructor now correctly creates a quaternion representing the shortest arc between the two input vectors. Previously, it would return incorrect values for certain inputs (GH-107618).

By default, the regions in a NavigationServer map now update asynchronously using threads to improve performance. This can cause additional delay in the update due to thread synchronisation. The asynchronous region update can be toggled with the navigation/world/region_use_async_iterations project setting.

The merging of navmeshes in the NavigationServer has changed processing order. Regions now merge and cache internal navmeshes first, then the remaining free edges are merged by the navigation map. If a project had navigation map synchronisation errors before, it might now have shifted affected edges, making already existing errors in a layout more noticeable in the pathfinding. The navigation/2d_or_3d/merge_rasterizer_cell_scale project setting can be set to a lower value to increase the detail of the rasterization grid (with 0.01 being the smallest cell size possible). If edge merge errors still persist with the lowest possible rasterization scale value, the error may be caused by overlap: two navmeshes are stacked on top of each other, causing geometry conflict.

When the 3D physics engine is set to Jolt Physics, you will now always have overlaps between Area3D and static bodies reported by default, as the physics/jolt_physics_3d/simulation/areas_detect_static_bodies project setting has been removed (GH-105746). If you still want such overlaps to be ignored, you will need to change the collision mask or layer of either the Area3D or the static body instead.

In GDScript, calls to functions RichTextLabel::add_image and RichTextLabel::update_image will continue to work, but the size_in_percent argument will now be used as the value for width_in_percent and height_in_percent will default to false (GH-107347). To restore the previous behavior, you can explicitly set height_in_percent to the same value you were passing as size_in_percent.

Please read the User-contributed notes policy before submitting a comment.

---

## WebRTCDataChannel

**URL:** https://docs.godotengine.org/en/stable/classes/class_webrtcdatachannel.html

**Contents:**
- WebRTCDataChannel
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: PacketPeer < RefCounted < Object

Inherited By: WebRTCDataChannelExtension

There is currently no description for this class. Please help us by contributing one!

get_buffered_amount() const

get_max_packet_life_time() const

get_max_retransmits() const

get_ready_state() const

is_negotiated() const

was_string_packet() const

WriteMode WRITE_MODE_TEXT = 0

Tells the channel to send data over this channel as text. An external peer (non-Godot) would receive this as a string.

WriteMode WRITE_MODE_BINARY = 1

Tells the channel to send data over this channel as binary. An external peer (non-Godot) would receive this as array buffer or blob.

ChannelState STATE_CONNECTING = 0

The channel was created, but it's still trying to connect.

ChannelState STATE_OPEN = 1

The channel is currently open, and data can flow over it.

ChannelState STATE_CLOSING = 2

The channel is being closed, no new messages will be accepted, but those already in queue will be flushed.

ChannelState STATE_CLOSED = 3

The channel was closed, or connection failed.

WriteMode write_mode = 1 

void set_write_mode(value: WriteMode)

WriteMode get_write_mode()

The transfer mode to use when sending outgoing packet. Either text or binary.

Closes this data channel, notifying the other peer.

int get_buffered_amount() const 

Returns the number of bytes currently queued to be sent over this channel.

Returns the ID assigned to this channel during creation (or auto-assigned during negotiation).

If the channel is not negotiated out-of-band the ID will only be available after the connection is established (will return 65535 until then).

String get_label() const 

Returns the label assigned to this channel during creation.

int get_max_packet_life_time() const 

Returns the maxPacketLifeTime value assigned to this channel during creation.

Will be 65535 if not specified.

int get_max_retransmits() const 

Returns the maxRetransmits value assigned to this channel during creation.

Will be 65535 if not specified.

String get_protocol() const 

Returns the sub-protocol assigned to this channel during creation. An empty string if not specified.

ChannelState get_ready_state() const 

Returns the current state of this channel.

bool is_negotiated() const 

Returns true if this channel was created with out-of-band configuration.

bool is_ordered() const 

Returns true if this channel was created with ordering enabled (default).

Reserved, but not used for now.

bool was_string_packet() const 

Returns true if the last received packet was transferred as text. See write_mode.

Please read the User-contributed notes policy before submitting a comment.

---

## WebRTCPeerConnection

**URL:** https://docs.godotengine.org/en/stable/classes/class_webrtcpeerconnection.html

**Contents:**
- WebRTCPeerConnection
- Description
- Methods
- Signals
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Inherited By: WebRTCPeerConnectionExtension

Interface to a WebRTC peer connection.

A WebRTC connection between the local computer and a remote peer. Provides an interface to connect, maintain and monitor the connection.

Setting up a WebRTC connection between two peers may not seem a trivial task, but it can be broken down into 3 main steps:

The peer that wants to initiate the connection (A from now on) creates an offer and send it to the other peer (B from now on).

B receives the offer, generate and answer, and sends it to A).

A and B then generates and exchange ICE candidates with each other.

After these steps, the connection should become connected. Keep on reading or look into the tutorial for more information.

add_ice_candidate(media: String, index: int, name: String)

create_data_channel(label: String, options: Dictionary = {})

get_connection_state() const

get_gathering_state() const

get_signaling_state() const

initialize(configuration: Dictionary = {})

set_default_extension(extension_class: StringName) static

set_local_description(type: String, sdp: String)

set_remote_description(type: String, sdp: String)

data_channel_received(channel: WebRTCDataChannel) 

Emitted when a new in-band channel is received, i.e. when the channel was created with negotiated: false (default).

The object will be an instance of WebRTCDataChannel. You must keep a reference of it or it will be closed automatically. See create_data_channel().

ice_candidate_created(media: String, index: int, name: String) 

Emitted when a new ICE candidate has been created. The three parameters are meant to be passed to the remote peer over the signaling server.

session_description_created(type: String, sdp: String) 

Emitted after a successful call to create_offer() or set_remote_description() (when it generates an answer). The parameters are meant to be passed to set_local_description() on this object, and sent to the remote peer over the signaling server.

enum ConnectionState: 

ConnectionState STATE_NEW = 0

The connection is new, data channels and an offer can be created in this state.

ConnectionState STATE_CONNECTING = 1

The peer is connecting, ICE is in progress, none of the transports has failed.

ConnectionState STATE_CONNECTED = 2

The peer is connected, all ICE transports are connected.

ConnectionState STATE_DISCONNECTED = 3

At least one ICE transport is disconnected.

ConnectionState STATE_FAILED = 4

One or more of the ICE transports failed.

ConnectionState STATE_CLOSED = 5

The peer connection is closed (after calling close() for example).

enum GatheringState: 

GatheringState GATHERING_STATE_NEW = 0

The peer connection was just created and hasn't done any networking yet.

GatheringState GATHERING_STATE_GATHERING = 1

The ICE agent is in the process of gathering candidates for the connection.

GatheringState GATHERING_STATE_COMPLETE = 2

The ICE agent has finished gathering candidates. If something happens that requires collecting new candidates, such as a new interface being added or the addition of a new ICE server, the state will revert to gathering to gather those candidates.

enum SignalingState: 

SignalingState SIGNALING_STATE_STABLE = 0

There is no ongoing exchange of offer and answer underway. This may mean that the WebRTCPeerConnection is new (STATE_NEW) or that negotiation is complete and a connection has been established (STATE_CONNECTED).

SignalingState SIGNALING_STATE_HAVE_LOCAL_OFFER = 1

The local peer has called set_local_description(), passing in SDP representing an offer (usually created by calling create_offer()), and the offer has been applied successfully.

SignalingState SIGNALING_STATE_HAVE_REMOTE_OFFER = 2

The remote peer has created an offer and used the signaling server to deliver it to the local peer, which has set the offer as the remote description by calling set_remote_description().

SignalingState SIGNALING_STATE_HAVE_LOCAL_PRANSWER = 3

The offer sent by the remote peer has been applied and an answer has been created and applied by calling set_local_description(). This provisional answer describes the supported media formats and so forth, but may not have a complete set of ICE candidates included. Further candidates will be delivered separately later.

SignalingState SIGNALING_STATE_HAVE_REMOTE_PRANSWER = 4

A provisional answer has been received and successfully applied in response to an offer previously sent and established by calling set_local_description().

SignalingState SIGNALING_STATE_CLOSED = 5

The WebRTCPeerConnection has been closed.

Error add_ice_candidate(media: String, index: int, name: String) 

Add an ice candidate generated by a remote peer (and received over the signaling server). See ice_candidate_created.

Close the peer connection and all data channels associated with it.

Note: You cannot reuse this object for a new connection unless you call initialize().

WebRTCDataChannel create_data_channel(label: String, options: Dictionary = {}) 

Returns a new WebRTCDataChannel (or null on failure) with given label and optionally configured via the options dictionary. This method can only be called when the connection is in state STATE_NEW.

There are two ways to create a working data channel: either call create_data_channel() on only one of the peer and listen to data_channel_received on the other, or call create_data_channel() on both peers, with the same values, and the "negotiated" option set to true.

Note: You must keep a reference to channels created this way, or it will be closed.

Error create_offer() 

Creates a new SDP offer to start a WebRTC connection with a remote peer. At least one WebRTCDataChannel must have been created before calling this method.

If this functions returns @GlobalScope.OK, session_description_created will be called when the session is ready to be sent.

ConnectionState get_connection_state() const 

Returns the connection state.

GatheringState get_gathering_state() const 

Returns the ICE GatheringState of the connection. This lets you detect, for example, when collection of ICE candidates has finished.

SignalingState get_signaling_state() const 

Returns the signaling state on the local end of the connection while connecting or reconnecting to another peer.

Error initialize(configuration: Dictionary = {}) 

Re-initialize this peer connection, closing any previously active connection, and going back to state STATE_NEW. A dictionary of configuration options can be passed to configure the peer connection.

Valid configuration options are:

Call this method frequently (e.g. in Node._process() or Node._physics_process()) to properly receive signals.

void set_default_extension(extension_class: StringName) static 

Sets the extension_class as the default WebRTCPeerConnectionExtension returned when creating a new WebRTCPeerConnection.

Error set_local_description(type: String, sdp: String) 

Sets the SDP description of the local peer. This should be called in response to session_description_created.

After calling this function the peer will start emitting ice_candidate_created (unless an Error different from @GlobalScope.OK is returned).

Error set_remote_description(type: String, sdp: String) 

Sets the SDP description of the remote peer. This should be called with the values generated by a remote peer and received over the signaling server.

If type is "offer" the peer will emit session_description_created with the appropriate answer.

If type is "answer" the peer will start emitting ice_candidate_created.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (json):
```json
{
    "negotiated": true, # When set to true (default off), means the channel is negotiated out of band. "id" must be set too. "data_channel_received" will not be called.
    "id": 1, # When "negotiated" is true this value must also be set to the same value on both peer.

    # Only one of maxRetransmits and maxPacketLifeTime can be specified, not both. They make the channel unreliable (but also better at real time).
    "maxRetransmits": 1, # Specify the maximum number of attempt the peer will make to retransmits packets if they are not acknowledged.
    "maxPacketLifeTime": 100, # Specify the maximum amount of time before giving up retransmitions of unacknowledged packets (in milliseconds).
    "ordered": true, # When in unreliable mode (i.e. either "maxRetransmits" or "maxPacketLifetime" is set), "ordered" (true by default) specify if packet ordering is to be enforced.

    "protocol": "my-custom-protocol", # A custom sub-protocol string for this channel.
}
```

Example 2 (json):
```json
{
    "iceServers": [
        {
            "urls": [ "stun:stun.example.com:3478" ], # One or more STUN servers.
        },
        {
            "urls": [ "turn:turn.example.com:3478" ], # One or more TURN servers.
            "username": "a_username", # Optional username for the TURN server.
            "credential": "a_password", # Optional password for the TURN server.
        }
    ]
}
```

---

## Web

**URL:** https://docs.godotengine.org/en/stable/tutorials/platform/web/index.html

**Contents:**
- Web

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

---
