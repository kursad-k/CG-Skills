# Godot - Engine Details

**Pages:** 46

---

## 2D coordinate systems and 2D transforms — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/2d_coordinate_systems.html

**Contents:**
- 2D coordinate systems and 2D transforms
- Introduction
- Godot 2D coordinate systems
- Node transforms
- User-contributed notes

This is a detailed overview of the available 2D coordinate systems and 2D transforms that are built in. The basic concepts are covered in Viewport and canvas transforms.

Transform2D are matrices that convert coordinates from one coordinate system to another. In order to use them, it is beneficial to know which coordinate systems are available in Godot. For a deeper understanding, the Matrices and transforms tutorial offers insights to the underlying functionality.

The following graphic gives an overview of Godot 2D coordinate systems and the available node-transforms, transform-functions and coordinate-system related functions. At the left is the OS Window Manager screen, at the right are the CanvasItems. For simplicity reasons this graphic doesn't include SubViewport, SubViewportContainer, ParallaxLayer and ParallaxBackground all of which also influence transforms.

The graphic is based on a node tree of the following form: Root Window (embed Windows) ⇒ Window (don't embed Windows) ⇒ CanvasLayer ⇒ CanvasItem ⇒ CanvasItem ⇒ CanvasItem. There are more complex combinations possible, like deeply nested Window and SubViewports, however this example intends to provide an overview of the methodology in general.

Click graphic to enlarge.

This is the local coordinate system of a CanvasItem.

This is the local coordinate system of the parent's CanvasItem. When positioning CanvasItems in the Canvas, they usually inherit the transformations of their parent CanvasItems. An exceptions is CanvasItems.top_level.

As mentioned in the previous tutorial Canvas layers, there are two types of canvases (Viewport canvas and CanvasLayer canvas) and both have a canvas coordinate system. These are also called world coordinates. A Viewport can contain multiple Canvases with different coordinate systems.

This is the coordinate system of the Viewport.

This is only used internally for functionality like 3D-camera ray projections.

Every Viewport (Window or SubViewport) in the scene tree is embedded either in a different node or in the OS Window Manager. This coordinate system's origin is identical to the top-left corner of the Window or SubViewport and its scale is the one of the embedder or the OS Window Manager.

If the embedder is the OS Window Manager, then they are also called Screen Coordinates.

The origin of this coordinate system is the top-left corner of the embedding node or the OS Window Manager screen. Its scale is the one of the embedder or the OS Window Manager.

If the embedder is the OS Window Manager, then they are also called Absolute Screen Coordinates.

Each of the mentioned nodes have one or more transforms associated with them and the combination of these nodes infer the transforms between the different coordinate systems. With a few exceptions, the transforms are Transform2D and the following list shows details and effects of each of them.

CanvasItems are either Control-nodes or Node2D-nodes.

For Control nodes this transform consists of a position relative to the parent's origin and a scale and rotation around a pivot point.

For Node2D nodes transform consists of position, rotation, scale and skew.

The transform affects the item itself and usually also child-CanvasItems and in the case of a SubViewportContainer it affects the contained SubViewport.

The CanvasLayer's transform affects all CanvasItems within the CanvasLayer. It doesn't affect other CanvasLayers or Windows in its Viewport.

The follow viewport transform is an automatically calculated transform, that is based on the Viewport's canvas transform and the CanvasLayer's follow viewport scale and can be used, if enabled, to achieve a pseudo-3D effect. It affects the same child nodes as the CanvasLayer transform.

The canvas transform affects all CanvasItems in the Viewport's default canvas. It also affects CanvasLayers, that have follow viewport transform enabled. The Viewport's active Camera2D works by changing this transform. It doesn't affect this Viewport's embedded Windows.

Viewports also have a global canvas transform. This is the master transform and affects all individual Canvas Layer and embedded Window transforms. This is primarily used in Godot's CanvasItem Editor.

Finally, Viewports have a stretch transform, which is used when resizing or stretching the viewport. This transform is used for Windows as described in Multiple resolutions, but can also be manually set on SubViewports by means of size and size_2d_override. Its translation, rotation and skew are the default values and it can only have non-default scale.

In order to scale and position the Window's content as described in Multiple resolutions, each Window contains a window transform. It is for example responsible for the black bars at the Window's sides so that the Viewport is displayed with a fixed aspect ratio.

Every Window also has a position to describe its position within its embedder. The embedder can be another Viewport or the OS Window Manager.

stretch together with stretch_shrink declare for a SubViewportContainer if and by what integer factor the contained SubViewport should be scaled in comparison to the container's size.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Android Studio — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/configuring_an_ide/android_studio.html

**Contents:**
- Android Studio
- Importing the project
- Android Studio project layout
- Building & debugging the editor module
- Building & debugging the app module
- User-contributed notes

Android Studio is a free IDE for Android development made by Google and JetBrains. It's based on IntelliJ IDEA and has a feature-rich editor which supports Java and C/C++. It can be used to work on Godot's core engine as well as the Android platform codebase.

From the Android Studio's welcome window select Open.

Android Studio's welcome window.

Navigate to <Godot root directory>/platform/android/java and select the settings.gradle file.

Android Studio will import and index the project.

The project is organized using Android Studio's modules:

the Godot java and native code and make it available as a reusable dependency / artifact.

The artifact generated by this module is made available for other Android modules / projects to use as a dependency, via MavenCentral.

the source code for the Android port of the Godot Editor.

This module has a dependency on the lib module.

the source code for the Android build templates.

This module has a dependency on the lib module.

Select the Run/Debug Configurations drop down and select editor.

Select Run > Run 'editor' from the top menu or click the Run icon.

Open the Build Variants window using View > Tools Windows > Build Variants from the top menu.

In the Build Variants window, make sure that in the Active Build Variant column, the :editor entry is set to one of the Dev variants.

Open the Run/Debug Configurations window by clicking on Run > Edit Configurations... on the top menu.

In the Run/Debug Configurations window, select the editor entry, and under Debugger make sure the Debug Type is set to Dual (Java + Native)

Click the + sign under the Symbol Directories section, and add the lib module directory: platform/android/java/lib

Select Run > Debug 'editor' from the top menu or click the Debug icon.

The app module requires the presence of a Godot project in its assets directory (<Godot root directory>/platform/android/java/app/assets) to run. This is usually handled by the Godot Editor during the export process. While developing in Android Studio, it's necessary to manually add a Godot project under that directory to replicate the export process. Once that's done, you can follow the instructions below to run/debug the app module:

Select the Run/Debug Configurations drop down and select app.

Select Run > Run 'app' from the top menu or click the Run icon.

Open the Build Variants window using View > Tools Windows > Build Variants from the top menu.

In the Build Variants window, make sure that in the Active Build Variant column, the :app entry is set to one of the Dev variants.

Open the Run/Debug Configurations window by clicking on Run > Edit Configurations... on the top menu.

In the Run/Debug Configurations window, select the app entry, and under Debugger make sure the Debug Type is set to Dual (Java + Native)

Click the + sign under the Symbol Directories section, and add the lib module directory: platform/android/java/lib

Select Run > Debug 'app' from the top menu or click the Debug icon.

If you run into any issues, ask for help in Godot's Android dev channel.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Binding to external libraries — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/binding_to_external_libraries.html

**Contents:**
- Binding to external libraries
- Modules
- Using the module
- User-contributed notes

The Summator example in Custom modules in C++ is great for small, custom modules, but what if you want to use a larger, external library? Let's look at an example using Festival, a speech synthesis (text-to-speech) library written in C++.

To bind to an external library, set up a module directory similar to the Summator example:

Next, you will create a header file with a TTS class:

And then you'll add the cpp file.

Just as before, the new class needs to be registered somehow, so two more files need to be created:

These files must be in the top-level folder of your module (next to your SCsub and config.py files) for the module to be registered properly.

These files should contain the following:

Next, you need to create an SCsub file so the build system compiles this module:

You'll need to install the external library on your machine to get the .a library files. See the library's official documentation for specific instructions on how to do this for your operation system. We've included the installation commands for Linux below, for reference.

The voices that Festival uses (and any other potential external/3rd-party resource) all have varying licenses and terms of use; some (if not most) of them may be be problematic with Godot, even if the Festival Library itself is MIT License compatible. Please be sure to check the licenses and terms of use.

The external library will also need to be installed inside your module to make the source files accessible to the compiler, while also keeping the module code self-contained. The festival and speech_tools libraries can be installed from the modules/tts/ directory via git using the following commands:

If you don't want the external repository source files committed to your repository, you can link to them instead by adding them as submodules (from within the modules/tts/ directory), as seen below:

Please note that Git submodules are not used in the Godot repository. If you are developing a module to be merged into the main Godot repository, you should not use submodules. If your module doesn't get merged in, you can always try to implement the external library as a GDExtension.

To add include directories for the compiler to look at you can append it to the environment's paths:

If you want to add custom compiler flags when building your module, you need to clone env first, so it won't add those flags to whole Godot build (which can cause errors). Example SCsub with custom flags:

The final module should look like this:

You can now use your newly created module from any script:

And the output will be is_spoken: True if the text is spoken.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## CLion — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/configuring_an_ide/clion.html

**Contents:**
- CLion
- Importing the project
- Compiling and debugging the project
- Ignoring object and library files
- User-contributed notes

CLion is a JetBrains IDE for C++ that's free for individual, non-commercial development.

CLion can import a project's compilation database file, commonly named compile_commands.json. To generate the compilation database file, open the terminal, change to the Godot root directory, and run:

Then, open the Godot root directory with CLion and wait for the project to be fully indexed. If code completion, parameter information, or refactoring are not enabled, you will need to load the project with CMake. To do this, find the CMakeLists.txt file in the platform\android\java\nativeSrcsConfigs directory, right click and select Load CMake Project. Once the project reloads, a godot build configuration will be added. This configuration can be safely deleted as the CMake file will not build the project and only exists for loading the project in JetBrains IDEs.

For compile_commands.json to load correctly in CLion, you must first have the Visual Studio toolchain configured for CLion.

Navigate to Preferences > Build, Execution, Deployment > Toolchains

Click the + button and select Visual Studio

CLion will attempt to detect your Visual Studio installation. If it is unsuccessful, use the file icon to the right of Toolset: to select the directory with your Visual Studio installation.

You may exit and reload CLion and it will reload compile_commands.json

CLion does not support compiling and debugging Godot via SCons out of the box. This can be achieved by creating a custom build target and run configuration in CLion. Before creating a custom build target, you must compile Godot once on the command line, to generate the Godot executable. Open the terminal, change into the Godot root directory, and execute:

To add a custom build target that invokes SCons for compilation:

Open CLion and navigate to Preferences > Build, Execution, Deployment > Custom Build Targets

Click Add target and give the target a name, e.g. Godot debug.

Click ... next to the Build: selectbox, then click the + button in the External Tools dialog to add a new external tool.

Give the tool a name, e.g. Build Godot debug, set Program to scons, set Arguments to the compilation settings you want (see compiling Godot), and set the Working directory to $ProjectFileDir$, which equals the Godot root directory. Click OK to create the tool.

CLion does not expand shell commands like scons -j$(nproc). Use concrete values instead, e.g. scons -j8.

Back in the External Tools dialog, click the + again to add a second external tool for cleaning the Godot build via SCons. Give the tool a name, e.g. Clean Godot debug, set Program to scons, set Arguments to -c (which will clean the build), and set the Working directory to $ProjectFileDir$. Click OK to create the tool.

Close the External Tools dialog. In the Custom Build Target dialog for the custom Godot debug build target, select the Build Godot debug tool from the Build select box, and select the Clean Godot debug tool from the Clean select box. Click OK to create the custom build target.

In the main IDE window, click Add Configuration.

In the Run/Debug Configuration dialog, click Add new..., then select Custom Build Application to create a new custom run/debug configuration.

Give the run/debug configuration a name, e.g. Godot debug, select the Godot debug custom build target as the Target. Select the Godot executable in the bin/ folder as the Executable, and set the Program arguments to --editor --path path-to-your-project/, where path-to-your-project/ should be a path pointing to an existing Godot project. If you omit the --path argument, you will only be able to debug the Godot Project Manager window. Click OK to create the run/debug configuration.

You can now build, run, debug, profile, and Valgrind check the Godot editor via the run configuration.

When playing a scene, the Godot editor will spawn a separate process. You can debug this process in CLion by going to Run > Attach to process..., typing godot, and selecting the Godot process with the highest pid (process ID), which will usually be the running project.

After building Godot in CLion, you may see the object and library files showing up in the Project view.

You can configure CLion to ignore those files:

Open CLion and navigate to Preferences > Editor > File Types > Ignored Files and Folders

Click the + button to add *.o and *.a to the list. In Windows, you would add *.obj and *.dll.

Now, the files should be ignored in the Project view.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Code::Blocks — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/configuring_an_ide/code_blocks.html

**Contents:**
- Code::Blocks
- Creating a new project
- Configuring the build
- Configuring the run
- Adding files to the project
- Code style configuration
- User-contributed notes

Code::Blocks is a free, open-source, cross-platform IDE.

From Code::Blocks' main screen, click Create a new project or select File > New > Project....

In the New from template window, from Projects, select Empty project, and click Go.

Click Next, to pass the welcome to the new empty project wizard.

The project file should be created in the root of the cloned project folder. To achieve this, first, ensure that the Project title is the same as the folder name that Godot was cloned into. Unless you cloned the project into a folder with a different name, this will be godot.

Second, ensure that the Folder to create project in is the folder you ran the Git clone command from, not the godot project folder. Confirm that the Resulting filename field will create the project file in the root of the cloned project folder.

The compiler and configuration settings are managed through SCons and will be configured later. However, it's worth deselecting the Create "Release" configuration option; so only a single build target is created before clicking Finish.

The first step is to change the project properties. Right-click on the new project and select Properties....

Check the This is a custom Makefile property. Click OK to save the changes.

The next step is to change the build options. Right-click on the new project and select Build Options....

Select the "Make" commands tab and remove all the existing commands for all the build targets. For each build target enter the SCons command for creating the desired build in the Build project/target field. The minimum is scons. For details on the SCons build options, see Introduction to the buildsystem. It's also useful to add the scons --clean command in the Clean project/target field to the project's default commands.

If you're using Windows, all the commands need to be preceded with cmd /c to initialize the command interpreter.

Code::Blocks should now be configured to build Godot; so either select Build > Build, click the gear button, or press Ctrl + F9.

Once SCons has successfully built the desired target, reopen the project Properties... and select the Build targets tab. In the Output filename field, browse to the bin folder and select the compiled file.

Deselect the Auto-generate filename prefix and Auto-generate filename extension options.

Code::Blocks should now be configured to run your compiled Godot executable; so either select Build > Run, click the green arrow button, or press Ctrl + F10.

There are two additional points worth noting. First, if required, the Execution working dir field can be used to test specific projects, by setting it to the folder containing the project.godot file. Second, the Build targets tab can be used to add and remove build targets for working with and creating different builds.

To add all the Godot code files to the project, right-click on the new project and select Add files recursively....

It should automatically select the project folder; so simply click Open. By default, all code files are included, so simply click OK.

Before editing any files, remember that all code needs to comply with the code style guidelines. One important difference with Godot is the use of tabs for indents. Therefore, the key default editor setting that needs to be changed in Code::Blocks is to enable tabs for indents. This setting can be found by selecting Settings > Editor.

Under General Settings, on the Editor Settings tab, under Tab Options check Use TAB character.

That's it. You're ready to start contributing to Godot using the Code::Blocks IDE. Remember to save the project file and the Workspace. If you run into any issues, ask for help in one of Godot's community channels.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Common engine methods and macros — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/common_engine_methods_and_macros.html

**Contents:**
- Common engine methods and macros
- Print text
- Format a string
- Convert an integer or float to a string
- Internationalize a string
- Clamp a value
- Microbenchmarking
- Get project/editor settings
- Error macros
- User-contributed notes

Godot's C++ codebase makes use of dozens of custom methods and macros which are used in almost every file. This page is geared towards beginner contributors, but it can also be useful for those writing custom C++ modules.

If you need to add placeholders in your messages, use format strings as described below.

The vformat() function returns a formatted String. It behaves in a way similar to C's sprintf():

In most cases, try to use vformat() instead of string concatenation as it makes for more readable code.

This is not needed when printing numbers using print_line(), but you may still need to perform manual conversion for some other use cases.

There are two types of internationalization in Godot's codebase:

TTR(): Editor ("tools") translations will only be processed in the editor. If a user uses the same text in one of their projects, it won't be translated if they provide a translation for it. When contributing to the engine, this is generally the macro you should use for localizable strings.

RTR(): Runtime translations will be automatically localized in projects if they provide a translation for the given string. This kind of translation shouldn't be used in editor-only code.

To insert placeholders in localizable strings, wrap the localization macro in a vformat() call as follows:

When using vformat() and a translation macro together, always wrap the translation macro in vformat(), not the other way around. Otherwise, the string will never match the translation as it will have the placeholder already replaced when it's passed to TranslationServer.

Godot provides macros for clamping a value with a lower bound (MAX), an upper bound (MIN) or both (CLAMP):

This works with any type that can be compared to other values (like int and float).

If you want to benchmark a piece of code but don't know how to use a profiler, use this snippet:

This will print the time spent between the begin declaration and the end declaration.

You may have to #include "core/os/time.h" if it's not present already.

When opening a pull request, make sure to remove this snippet as well as the include if it wasn't there previously.

There are four macros available for this:

If a default value has been specified elsewhere, don't specify it again to avoid repetition:

It's recommended to use GLOBAL_DEF/EDITOR_DEF only once per setting and use GLOBAL_GET/EDITOR_GET in all other places where it's referenced.

Godot features many error macros to make error reporting more convenient.

Conditions in error macros work in the opposite way of GDScript's built-in assert() function. An error is reached if the condition inside evaluates to true, not false.

Only variants with custom messages are documented here, as these should always be used in new contributions. Make sure the custom message provided includes enough information for people to diagnose the issue, even if they don't know C++. In case a method was passed invalid arguments, you can print the invalid value in question to ease debugging.

For internal error checking where displaying a human-readable message isn't necessary, remove _MSG at the end of the macro name and don't supply a message argument.

Also, always try to return processable data so the engine can keep running well.

See core/error/error_macros.h in Godot's codebase for more information about each error macro.

Some functions return an error code (materialized by a return type of Error). This value can be returned directly from an error macro. See the list of available error codes in core/error/error_list.h.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Compiling for Android — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/compiling_for_android.html

**Contents:**
- Compiling for Android
- Note
- Requirements
- Setting up the buildsystem
- Building the export templates
  - Adding support for x86 devices
  - Cleaning the generated export templates
- Using the export templates
  - Installing the templates
- Building the Godot editor

This page describes how to compile Android export template binaries from source. If you're looking to export your project to Android instead, read Exporting for Android.

In most cases, using the built-in deployer and export templates is good enough. Compiling the Android APK manually is mostly useful for custom builds or custom packages for the deployer.

Also, you still need to follow the steps mentioned in the Exporting for Android tutorial before attempting to build a custom export template.

For compiling under Windows, Linux or macOS, the following is required:

SCons 4.0+ build system.

Android SDK (command-line tools are sufficient).

Required SDK components will be automatically installed.

On Linux, do not use an Android SDK provided by your distribution's repositories as it will often be outdated.

On macOS, do not use an Android SDK provided by Homebrew as it will not be installed in a unified location.

Gradle (will be downloaded and installed automatically if missing).

JDK 17 (either OpenJDK or Oracle JDK).

You can download a build from Adoptium.

To get the Godot source code for compiling, see Getting the source.

For a general overview of SCons usage for Godot, see Introduction to the buildsystem.

Set the environment variable ANDROID_HOME to point to the Android SDK. If you downloaded the Android command-line tools, this would be the folder where you extracted the contents of the ZIP archive.

Windows: Press Windows + R, type "control system", then click on Advanced system settings in the left pane, then click on Environment variables on the window that appears.

Linux or macOS: Add the text export ANDROID_HOME="/path/to/android-sdk" to your .bashrc or .zshrc where /path/to/android-sdk points to the root of the SDK directories.

Install the necessary SDK components in this folder:

Accept the SDK component licenses by running the following command where android_sdk_path is the path to the Android SDK, then answering all the prompts with y:

Complete setup by running the following command where android_sdk_path is the path to the Android SDK.

After setting up the SDK and environment variables, be sure to restart your terminal to apply the changes. If you are using an IDE with an integrated terminal, you need to restart the IDE.

Run scons platform=android. If this fails, go back and check the steps. If you completed the setup correctly, the NDK will begin downloading. If you are trying to compile GDExtension, you need to first compile the engine to download the NDK, then you can compile GDExtension.

Godot needs three export templates for Android: the optimized "release" template (android_release.apk), the debug template (android_debug.apk), and the Gradle build template (android_source.zip). As Google requires all APKs to include ARMv8 (64-bit) libraries since August 2019, the commands below build templates containing both ARMv7 and ARMv8 libraries.

Compiling the standard export templates is done by calling SCons from the Godot root directory with the following arguments:

Release template (used when exporting with Debugging Enabled unchecked)

Debug template (used when exporting with Debugging Enabled checked)

(Optional) Dev template (used when troubleshooting)

The resulting templates will be located under the bin directory:

bin/android_release.apk for the release template

bin/android_debug.apk for the debug template

bin/android_dev.apk for the dev template

bin/android_source.zip for the Gradle build template

If you are changing the list of architectures you're building, remember to add generate_android_binaries=yes to the last architecture you're building, so that the template files are generated after the build.

To include debug symbols in the generated templates, add the debug_symbols=yes parameters to the SCons command.

Note that you can include separate_debug_symbols=yes to generate the debug symbols in a separate *-native-debug-symbols.zip file.

If you want to enable Vulkan validation layers, see Vulkan validation layers on Android.

If you also want to include support for x86 and x86_64 devices, run the SCons command a third and fourth time with the arch=x86_32, and arch=x86_64 arguments before building the APK with Gradle. For example, for the release template:

This will create template binaries that works on all platforms. The final binary size of exported projects will depend on the platforms you choose to support when exporting; in other words, unused platforms will be removed from the binary.

You can use the following commands to remove the generated export templates:

Godot needs release and debug binaries that were compiled against the same version/commit as the editor. If you are using official binaries for the editor, make sure to install the matching export templates, or build your own from the same version.

When exporting your game, Godot uses the templates as a base, and updates their content as needed.

The newly-compiled templates (android_debug.apk , android_release.apk, and android_source.zip) must be copied to Godot's templates folder with their respective names. The templates folder can be located in:

Windows: %APPDATA%\Godot\export_templates\<version>\

Linux: $HOME/.local/share/godot/export_templates/<version>/

macOS: $HOME/Library/Application Support/Godot/export_templates/<version>/

<version> is of the form major.minor[.patch].status using values from version.py in your Godot source repository (e.g. 4.1.3.stable or 4.2.dev). You also need to write this same version string to a version.txt file located next to your export templates.

However, if you are writing your custom modules or custom C++ code, you might instead want to configure your template binaries as custom export templates in the project export menu. You must have Advanced Options enabled to set this.

You don't even need to copy them, you can just reference the resulting file in the bin\ directory of your Godot source folder, so that the next time you build you will automatically have the custom templates referenced.

Compiling the editor is done by calling SCons from the Godot root directory with the following arguments:

You can add the dev_build=yes parameter to generate a dev build of the Godot editor.

You can add the debug_symbols=yes parameters to include the debug symbols in the generated build.

Note that you can include separate_debug_symbols=yes to generate the debug symbols in a separate *-native-debug-symbols.zip file.

You can skip certain architectures depending on your target device to speed up compilation.

Remember to add generate_android_binaries=yes to the last architecture you're building, so that binaries are generated after the build.

The resulting binaries will be located under bin/android_editor_builds/.

You can use the following commands to remove the generated editor binaries:

With an Android device with Developer Options enabled, connect the Android device to your computer via its charging cable to a USB/USB-C port. Open up a Terminal/Command Prompt and run the following commands from the root directory with the following arguments:

Double-check that you've set the ANDROID_HOME environment variable. This is required for the platform to appear in SCons' list of detected platforms. See Setting up the buildsystem for more information.

Android might complain the application is not correctly installed. If so:

Check that the debug keystore is properly generated.

Check that the jarsigner executable is from JDK 8.

If it still fails, open a command line and run logcat:

Then check the output while the application is installed; the error message should be presented there. Seek assistance if you can't figure it out.

If the application runs but exits immediately, this might be due to one of the following reasons:

Make sure to use export templates that match your editor version; if you use a new Godot version, you have to update the templates too.

libgodot_android.so is not in libs/<arch>/ where <arch> is the device's architecture.

The device's architecture does not match the exported one(s). Make sure your templates were built for that device's architecture, and that the export settings included support for that architecture.

In any case, adb logcat should also show the cause of the error.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Compiling for iOS — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/compiling_for_ios.html

**Contents:**
- Compiling for iOS
- Requirements
- Compiling
- Run
- Troubleshooting
  - Fatal error: 'cstdint' file not found
- User-contributed notes

This page describes how to compile iOS export template binaries from source. If you're looking to export your project to iOS instead, read Exporting for iOS.

SCons 4.0+ build system.

Launch Xcode once and install iOS support. If you have already launched Xcode and need to install iOS support, go to Xcode -> Settings... -> Platforms.

Go to Xcode -> Settings... -> Locations -> Command Line Tools and select an installed version. Even if one is already selected, re-select it.

Download and follow README instructions to build a static .xcframework from the MoltenVK SDK.

If you have Homebrew installed, you can easily install SCons using the following command:

Installing Homebrew will also fetch the Command Line Tools for Xcode automatically if you don't have them already.

Similarly, if you have MacPorts installed, you can easily install SCons using the following command:

To get the Godot source code for compiling, see Getting the source.

For a general overview of SCons usage for Godot, see Introduction to the buildsystem.

Open a Terminal, go to the root folder of the engine source code and type the following to compile a debug build:

To compile a release build:

To create an Xcode project like in the official builds, you need to use the template located in misc/dist/ios_xcode. The release and debug libraries should be placed in libgodot.ios.debug.xcframework and libgodot.ios.release.xcframework respectively. This process can be automated by using the generate_bundle=yes option on the last SCons command used to build export templates (so that all binaries can be included).

The MoltenVK static .xcframework folder must also be placed in the ios_xcode folder once it has been created. MoltenVK is always statically linked on iOS; there is no dynamic linking option available, unlike macOS.

Compiling for the iOS simulator is currently not supported as per GH-102149.

Apple Silicon Macs can run iOS apps natively, so you can run exported iOS projects directly on an Apple Silicon Mac without needing the iOS simulator.

To run on a device, follow these instructions: Exporting for iOS.

iOS exports can run directly on an Apple Silicon Mac. To run exported iOS project on Mac, open exported project in Xcode and select My Mac in the Run Destinations dropdown.

If you get a compilation error of this form early on, it's likely because the Xcode command line tools installation needs to be repaired after a macOS or Xcode update:

Run these two commands to reinstall Xcode command line tools (enter your administrator password as needed):

If it still does not work, try updating Xcode from the Mac App Store and try again.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Compiling for Linux, *BSD — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/compiling_for_linuxbsd.html

**Contents:**
- Compiling for Linux, *BSD
- Requirements
  - Distro-specific one-liners
- Compiling
- Compiling with AccessKit support
- Running a headless/server build
- Building export templates
- Cross-compiling for RISC-V devices
- Using Clang and LLD for faster development
- Using mold for faster development

This page describes how to compile Linux editor and export template binaries from source. If you're looking to export your project to Linux instead, read Exporting for Linux.

For compiling under Linux or other Unix variants, the following is required:

SCons 4.0+ build system.

pkg-config (used to detect the development libraries listed below).

Development libraries:

X11, Xcursor, Xinerama, Xi and XRandR.

Wayland and wayland-scanner.

Optional - libudev (build with udev=yes).

To get the Godot source code for compiling, see Getting the source.

For a general overview of SCons usage for Godot, see Introduction to the buildsystem.

For audio support, you can optionally install pulseaudio.

Start a terminal, go to the root dir of the engine source code and type:

Prior to Godot 4.0, the Linux/*BSD target was called x11 instead of linuxbsd. If you are looking to compile Godot 3.x, make sure to use the 3.x branch of this documentation.

If you are compiling Godot to make changes or contribute to the engine, you may want to use the SCons options dev_build=yes or dev_mode=yes. See Development and production aliases for more info.

If all goes well, the resulting binary executable will be placed in the "bin" subdirectory. This executable file contains the whole engine and runs without any dependencies. Executing it will bring up the Project Manager.

If you wish to compile using Clang rather than GCC, use this command:

Using Clang appears to be a requirement for OpenBSD, otherwise fonts would not build. For RISC-V architecture devices, use the Clang compiler instead of the GCC compiler.

If you are compiling Godot for production use, you can make the final executable smaller and faster by adding the SCons option production=yes. This enables additional compiler optimizations and link-time optimization.

LTO takes some time to run and requires about 7 GB of available RAM while compiling. If you're running out of memory with the above option, use production=yes lto=none or production=yes lto=thin for a lightweight but less effective form of LTO.

If you want to use separate editor settings for your own Godot builds and official releases, you can enable Self-contained mode by creating a file called ._sc_ or _sc_ in the bin/ folder.

AccessKit provides support for screen readers.

By default, Godot is built with AccessKit dynamically linked. You can use it by placing accesskit.so alongside the executable.

You can use dynamically linked AccessKit with export templates as well, rename the SO to accesskit.{architecture}.so and place them alongside the export template executables, and the libraries will be automatically copied during the export process.

To compile Godot with statically linked AccessKit:

Download the pre-built static libraries from godot-accesskit-c-static library, and unzip them.

When building Godot, add accesskit_sdk_path={path} to tell SCons where to look for the AccessKit libraries:

You can optionally build the godot-angle-static libraries yourself with the following steps:

Clone the godot-accesskit-c-static directory and navigate to it.

Run the following command:

The AccessKit static library should be built using the same compiler you are using for building Godot.

To run in headless mode which provides editor functionality to export projects in an automated manner, use the normal build:

And then use the --headless command line argument:

To compile a debug server build which can be used with remote debugging tools, use:

To compile a server build which is optimized to run dedicated game servers, use:

Linux binaries usually won't run on distributions that are older than the distribution they were built on. If you wish to distribute binaries that work on most distributions, you should build them on an old distribution such as Ubuntu 20.04. You can use a virtual machine or a container to set up a suitable build environment.

To build Linux or *BSD export templates, run the build system with the following parameters:

Note that cross-compiling for the opposite bits (64/32) as your host platform is not always straight-forward and might need a chroot environment.

To create standard export templates, the resulting files in the bin/ folder must be copied to:

and named like this (even for *BSD which is seen as "Linux/X11" by Godot):

However, if you are writing your custom modules or custom C++ code, you might instead want to configure your binaries as custom export templates in the project export menu. You must have Advanced Options enabled to set this.

You don't even need to copy them, you can just reference the resulting files in the bin/ directory of your Godot source folder, so the next time you build, you automatically have the custom templates referenced.

To cross-compile Godot for RISC-V devices, we need to setup the following items:

riscv-gnu-toolchain. While we are not going to use this directly, it provides us with a sysroot, as well as header and libraries files that we will need. There are many versions to choose from, however, the older the toolchain, the more compatible our final binaries will be. If in doubt, use this version, and download riscv64-glibc-ubuntu-20.04-gcc-nightly-2023.07.07-nightly.tar.gz. Extract it somewhere and remember its path.

mold. This fast linker, is the only one that correctly links the resulting binary. Download it, extract it, and make sure to add its bin folder to your PATH. Run mold --help | grep support to check if your version of Mold supports RISC-V. If you don't see RISC-V, your Mold may need to be updated.

To make referencing our toolchain easier, we can set an environment variable like this:

This way, we won't have to manually set the directory location each time we want to reference it.

With all the above setup, we are now ready to build Godot.

Go to the root of the source code, and execute the following build command:

RISC-V GCC has bugs with its atomic operations which prevent it from compiling Godot correctly. That's why Clang is used instead. Make sure that it can compile to RISC-V. You can verify by executing this command clang -print-targets, make sure you see riscv64 on the list of targets.

The code above includes adding $RISCV_TOOLCHAIN_PATH/bin to the PATH, but only for the following scons command. Since riscv-gnu-toolchain uses its own Clang located in the bin folder, adding $RISCV_TOOLCHAIN_PATH/bin to your user's PATH environment variable may block you from accessing another version of Clang if one is installed. For this reason it's not recommended to make adding the bin folder permanent. You can also omit the PATH="$RISCV_TOOLCHAIN_PATH/bin:$PATH" line if you want to use scons with self-installed version of Clang, but it may have compatibility issues with riscv-gnu-toolchain.

The command is similar in nature, but with some key changes. ccflags and linkflags append additional flags to the build. --sysroot points to a folder simulating a Linux system, it contains all the headers, libraries, and .so files Clang will use. --gcc-toolchain tells Clang where the complete toolchain is, and -target riscv64-unknown-linux-gnu indicates to Clang the target architecture, and OS we want to build for.

If all went well, you should now see a bin directory, and within it, a binary similar to the following:

You can now copy this executable to your favorite RISC-V device, then launch it there by double-clicking, which should bring up the project manager.

If you later decide to compile the export templates, copy the above build command but change the value of target to template_debug for a debug build, or template_release for a release build.

You can also use Clang and LLD to build Godot. This has two upsides compared to the default GCC + GNU ld setup:

LLD links Godot significantly faster compared to GNU ld or gold. This leads to faster iteration times.

Clang tends to give more useful error messages compared to GCC.

To do so, install Clang and the lld package from your distribution's package manager then use the following SCons command:

After the build is completed, a new binary with a .llvm suffix will be created in the bin/ folder.

It's still recommended to use GCC for production builds as they can be compiled using link-time optimization, making the resulting binaries smaller and faster.

If this error occurs:

There are two solutions:

In your SCons command, add the parameter use_static_cpp=no.

Follow these instructions to configure, build, and install libatomic_ops. Then, copy /usr/lib/libatomic_ops.a to /usr/lib/libatomic.a, or create a soft link to libatomic_ops by command ln -s /usr/lib/libatomic_ops.a /usr/lib/libatomic.a. The soft link can ensure the latest libatomic_ops will be used without the need to copy it every time when it is updated.

For even faster linking compared to LLD, you can use mold. mold can be used with either GCC or Clang.

As of January 2023, mold is not readily available in Linux distribution repositories, so you will have to install its binaries manually.

Download mold binaries from its releases page.

Extract the .tar.gz file, then move the extracted folder to a location such as .local/share/mold.

Add $HOME/.local/share/mold/bin to your user's PATH environment variable. For example, you can add the following line at the end of your $HOME/.bash_profile file:

Open a new terminal (or run source "$HOME/.bash_profile"), then use the following SCons command when compiling Godot:

Godot bundles the source code of various third-party libraries. You can choose to use system versions of third-party libraries instead. This makes the Godot binary faster to link, as third-party libraries are dynamically linked. Therefore, they don't need to be statically linked every time you build the engine (even on small incremental changes).

However, not all Linux distributions have packages for third-party libraries available (or they may not be up-to-date).

Moving to system libraries can reduce linking times by several seconds on slow CPUs, but it requires manual testing depending on your Linux distribution. Also, you may not be able to use system libraries for everything due to bugs in the system library packages (or in the build system, as this feature is less tested).

To compile Godot with system libraries, install these dependencies on top of the ones listed in the Distro-specific one-liners:

After installing all required packages, use the following command to build Godot:

On Debian stable, you will need to remove builtin_embree=no as the system-provided Embree version is too old to work with Godot's latest master branch (which requires Embree 4).

You can view a list of all built-in libraries that have system alternatives by running scons -h, then looking for options starting with builtin_.

When using system libraries, the resulting binary is not portable across Linux distributions anymore. Do not use this approach for creating binaries you intend to distribute to others, unless you're creating a package for a Linux distribution.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Compiling for macOS — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/compiling_for_macos.html

**Contents:**
- Compiling for macOS
- Requirements
- Compiling
- Compiling with AccessKit support
  - Automatic .app bundle creation
  - Manual .app bundle creation
- Running a headless/server build
- Building export templates
- Cross-compiling for macOS from Linux
- Troubleshooting

This page describes how to compile macOS editor and export template binaries from source. If you're looking to export your project to macOS instead, read Exporting for macOS.

For compiling under macOS, the following is required:

SCons 4.0+ build system.

Xcode (or the more lightweight Command Line Tools for Xcode).

Vulkan SDK for MoltenVK (macOS doesn't support Vulkan out of the box). The latest Vulkan SDK version can be installed quickly by running misc/scripts/install_vulkan_sdk_macos.sh within the Godot source repository.

If you have Homebrew installed, you can easily install SCons using the following command:

Installing Homebrew will also fetch the Command Line Tools for Xcode automatically if you don't have them already.

Similarly, if you have MacPorts installed, you can easily install SCons using the following command:

To get the Godot source code for compiling, see Getting the source.

For a general overview of SCons usage for Godot, see Introduction to the buildsystem.

Start a terminal, go to the root directory of the engine source code.

To compile for Intel (x86-64) powered Macs, use:

To compile for Apple Silicon (ARM64) powered Macs, use:

If you are compiling Godot to make changes or contribute to the engine, you may want to use the SCons options dev_build=yes or dev_mode=yes. See Development and production aliases for more info.

If all goes well, the resulting binary executable will be placed in the bin/ subdirectory. This executable file contains the whole engine and runs without any dependencies. Executing it will bring up the Project Manager.

Using a standalone editor executable is not recommended, it should be always packaged into a .app bundle to avoid UI activation issues.

If you want to use separate editor settings for your own Godot builds and official releases, you can enable Self-contained mode by creating a file called ._sc_ or _sc_ in the bin/ folder.

AccessKit provides support for screen readers.

By default, Godot is built with AccessKit dynamically linked. You can use it by placing accesskit.dylib alongside the standalone executable or in the app bundle's Frameworks folder.

You can use dynamically linked AccessKit with export templates as well, rename the DYLIB to accesskit.{architecture}.dylib and place them inside the export template app bundle Frameworks folder, and the libraries will be automatically copied during the export process.

To compile Godot with statically linked AccessKit:

Download the pre-built static libraries from godot-accesskit-c-static library, and unzip them.

When building Godot, add accesskit_sdk_path={path} to tell SCons where to look for the AccessKit libraries:

You can optionally build the godot-angle-static libraries yourself with the following steps:

Clone the godot-accesskit-c-static directory and navigate to it.

Run the following command:

The AccessKit static library should be built using the same compiler you are using for building Godot.

To automatically create a .app bundle like in the official builds, use the generate_bundle=yes option on the last SCons command used to build editor:

To support both architectures in a single "Universal 2" binary, run the above two commands and then use lipo to bundle them together:

To create a .app bundle, you need to use the template located in misc/dist/macos_tools.app. Typically, for an optimized editor binary built with dev_build=yes:

If you are building the master branch, you also need to include support for the MoltenVK Vulkan portability library. By default, it will be linked statically from your installation of the Vulkan SDK for macOS. You can also choose to link it dynamically by passing use_volk=yes and including the dynamic library in your .app bundle:

To run in headless mode which provides editor functionality to export projects in an automated manner, use the normal build:

And then use the --headless command line argument:

To compile a debug server build which can be used with remote debugging tools, use:

To compile a release server build which is optimized to run dedicated game servers, use:

To build macOS export templates, you have to compile using the targets without the editor: target=template_release (release template) and target=template_debug.

Official templates are Universal 2 binaries which support both ARM64 and Intel x86_64 architectures.

To support ARM64 (Apple Silicon) + Intel x86_64:

To support ARM64 (Apple Silicon) only (smaller file size, but less compatible with older hardware):

To create a .app bundle like in the official builds, you need to use the template located in misc/dist/macos_template.app. This process can be automated by using the generate_bundle=yes option on the last SCons command used to build export templates (so that all binaries can be included). This option also takes care of calling lipo to create a Universal 2 binary from two separate ARM64 and x86_64 binaries (if both were compiled beforehand).

You also need to include support for the MoltenVK Vulkan portability library. By default, it will be linked statically from your installation of the Vulkan SDK for macOS. You can also choose to link it dynamically by passing use_volk=yes and including the dynamic library in your .app bundle:

In most cases, static linking should be preferred as it makes distribution easier. The main upside of dynamic linking is that it allows updating MoltenVK without having to recompile export templates.

You can then zip the macos_template.app folder to reproduce the macos.zip template from the official Godot distribution:

It is possible to compile for macOS in a Linux environment (and maybe also in Windows using the Windows Subsystem for Linux). For that, you'll need to install OSXCross to be able to use macOS as a target. First, follow the instructions to install it:

Clone the OSXCross repository somewhere on your machine (or download a ZIP file and extract it somewhere), e.g.:

Follow the instructions to package the SDK: https://github.com/tpoechtrager/osxcross#packaging-the-sdk

Follow the instructions to install OSXCross: https://github.com/tpoechtrager/osxcross#installation

After that, you will need to define the OSXCROSS_ROOT as the path to the OSXCross installation (the same place where you cloned the repository/extracted the zip), e.g.:

Now you can compile with SCons like you normally would:

If you have an OSXCross SDK version different from the one expected by the SCons buildsystem, you can specify a custom one with the osxcross_sdk argument:

If you get a compilation error of this form early on, it's likely because the Xcode command line tools installation needs to be repaired after a macOS or Xcode update:

Run these two commands to reinstall Xcode command line tools (enter your administrator password as needed):

If it still does not work, try updating Xcode from the Mac App Store and try again.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Compiling for the Web — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/compiling_for_web.html

**Contents:**
- Compiling for the Web
- Requirements
- Building export templates
- GDExtension
- Building the editor
- User-contributed notes

This page describes how to compile HTML5 editor and export template binaries from source. If you're looking to export your project to HTML5 instead, read Exporting for the Web.

To compile export templates for the Web, the following is required:

SCons 4.0+ build system.

To get the Godot source code for compiling, see Getting the source.

For a general overview of SCons usage for Godot, see Introduction to the buildsystem.

Before starting, confirm that emcc is available in your PATH. This is usually configured by the Emscripten SDK, e.g. when invoking emsdk activate and source ./emsdk_env.sh/emsdk_env.bat.

Open a terminal and navigate to the root directory of the engine source code. Then instruct SCons to build the Web platform. Specify target as either template_release for a release build or template_debug for a debug build:

By default, the JavaScriptBridge singleton will be built into the engine. Official export templates also have the JavaScript singleton enabled. Since eval() calls can be a security concern, the javascript_eval option can be used to build without the singleton:

By default, WebWorker threads support is enabled. To disable it and only use a single thread, the threads option can be used to build the web template without threads support:

The engine will now be compiled to WebAssembly by Emscripten. Once finished, the resulting file will be placed in the bin subdirectory. Its name is godot.web.template_release.wasm32.zip for release or godot.web.template_debug.wasm32.zip for debug.

Finally, rename the zip archive to web_release.zip for the release template:

And web_debug.zip for the debug template:

The default export templates do not include GDExtension support for performance and compatibility reasons. See the export page for more info.

You can build the export templates using the option dlink_enabled=yes to enable GDExtension support:

Once finished, the resulting file will be placed in the bin subdirectory. Its name will have _dlink added.

Finally, rename the zip archives to web_dlink_release.zip and web_dlink_release.zip for the release template:

It is also possible to build a version of the Godot editor that can run in the browser. The editor version is not recommended over the native build. You can build the editor with:

Once finished, the resulting file will be placed in the bin subdirectory. Its name will be godot.web.editor.wasm32.zip. You can upload the zip content to your web server and visit it with your browser to use the editor.

Refer to the export page for the web server requirements.

The Godot repository includes a Python script to host a local web server. This can be used to test the web editor locally.

After compiling the editor, extract the ZIP archive that was created in the bin/ folder, then run the following command in the Godot repository root:

This will serve the contents of the bin/ folder and open the default web browser automatically. In the page that opens, access godot.editor.html and you should be able to test the web editor this way.

Note that for production use cases, this Python-based web server should not be used. Instead, you should use an established web server such as Apache or nginx.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Compiling for visionOS — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/compiling_for_visionos.html

**Contents:**
- Compiling for visionOS
- User-contributed notes

This page describes how to compile visionOS export template binaries from source. If you're looking to export your project to visionOS instead, see Exporting for visionOS.

Compiling instructions for visionOS are currently identical to Compiling for iOS, except you should replace instances of platform=ios with platform=visionos in the SCons options. See the linked page for details.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Compiling for Windows — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/compiling_for_windows.html

**Contents:**
- Compiling for Windows
- Requirements
- Setting up SCons
- Downloading Godot's source
- Compiling
  - Selecting a compiler
  - Running SCons
- Compiling with support for Direct3D 12
- Compiling with AccessKit support
- Compiling with ANGLE support

This page describes how to compile Windows editor and export template binaries from source. If you're looking to export your project to Windows instead, read Exporting for Windows.

For compiling under Windows, the following is required:

A C++ compiler. Use one of the following:

Visual Studio Community, version 2019 or later. Visual Studio 2022 is recommended. Make sure to enable C++ in the list of workflows to install. If you've already installed Visual Studio without C++ support, run the installer again; it should present you a Modify button. Supports x86_64, x86_32, and arm64.

MinGW-w64 with GCC can be used as an alternative to Visual Studio. Be sure to install/configure it to use the posix thread model. Important: When using MinGW to compile the master branch, you need GCC 9 or later. Supports x86_64 and x86_32 only.

MinGW-LLVM with clang can be used as an alternative to Visual Studio and MinGW-w64. Supports x86_64, x86_32, and arm64.

Python 3.8+. Make sure to enable the option to add Python to the PATH in the installer.

SCons 4.0+ build system. Using the latest release is recommended, especially for proper support of recent Visual Studio releases.

If you have Scoop installed, you can easily install MinGW and other dependencies using the following command:

Scons will still need to be installed via pip

If you have MSYS2 installed, you can easily install MinGW and other dependencies using the following command:

For each MSYS2 MinGW subsystem, you should then run pip3 install scons in its shell.

To get the Godot source code for compiling, see Getting the source.

For a general overview of SCons usage for Godot, see Introduction to the buildsystem.

To install SCons, open the command prompt and run the following command:

If you are prompted with the message Defaulting to user installation because normal site-packages is not writeable, you may have to run that command again using elevated permissions. Open a new command prompt as an Administrator then run the command again to ensure that SCons is available from the PATH.

To check whether you have installed Python and SCons correctly, you can type python --version and scons --version into a command prompt (cmd.exe).

If the commands above don't work, make sure to add Python to your PATH environment variable after installing it, then check again. You can do so by running the Python installer again and enabling the option to add Python to the PATH.

If SCons cannot detect your Visual Studio installation, it might be that your SCons version is too old. Update it to the latest version with python -m pip install --upgrade scons.

Refer to Getting the source for detailed instructions.

The tutorial will assume from now on that you placed the source code in C:\godot.

To prevent slowdowns caused by continuous virus scanning during compilation, add the Godot source folder to the list of exceptions in your antivirus software.

For Windows Defender, hit the Windows key, type "Windows Security" then hit Enter. Click on Virus & threat protection on the left panel. Under Virus & threat protection settings click on Manage Settings and scroll down to Exclusions. Click Add or remove exclusions then add the Godot source folder.

SCons will automatically find and use an existing Visual Studio installation. If you do not have Visual Studio installed, it will attempt to use MinGW instead. If you already have Visual Studio installed and want to use MinGW-w64, pass use_mingw=yes to the SCons command line. Note that MSVC builds cannot be performed from the MSYS2 or MinGW shells. Use either cmd.exe or PowerShell instead. If you are using MinGW-LLVM, pass both use_mingw=yes and use_llvm=yes to the SCons command line.

During development, using the Visual Studio compiler is usually a better idea, as it links the Godot binary much faster than MinGW. However, MinGW can produce more optimized binaries using link-time optimization (see below), making it a better choice for production use. This is particularly the case for the GDScript VM which performs much better with MinGW compared to MSVC. Therefore, it's recommended to use MinGW to produce builds that you distribute to players.

All official Godot binaries are built in custom containers using MinGW.

After opening a command prompt, change to the root directory of the engine source code (using cd) and type:

When compiling with multiple CPU threads, SCons may warn about pywin32 being missing. You can safely ignore this warning.

If you are compiling Godot to make changes or contribute to the engine, you may want to use the SCons options dev_build=yes or dev_mode=yes. See Development and production aliases for more info.

If all goes well, the resulting binary executable will be placed in C:\godot\bin\ with the name godot.windows.editor.x86_32.exe or godot.windows.editor.x86_64.exe. By default, SCons will build a binary matching your CPU architecture, but this can be overridden using arch=x86_64, arch=x86_32, or arch=arm64.

This executable file contains the whole engine and runs without any dependencies. Running it will bring up the Project Manager.

If you are compiling Godot for production use, you can make the final executable smaller and faster by adding the SCons option production=yes. This enables additional compiler optimizations and link-time optimization.

LTO takes some time to run and requires up to 30 GB of available RAM while compiling (depending on toolchain). If you're running out of memory with the above option, use production=yes lto=none or production=yes lto=thin (LLVM only) for a lightweight but less effective form of LTO.

If you want to use separate editor settings for your own Godot builds and official releases, you can enable Self-contained mode by creating a file called ._sc_ or _sc_ in the bin/ folder.

By default, builds of Godot do not contain support for the Direct3D 12 graphics API.

You can install the required dependencies by running python misc/scripts/install_d3d12_sdk_windows.py in the Godot source repository. After running this script, add the d3d12=yes SCons option to enable Direct3D 12 support. This will use the default paths for the various dependencies, which match the ones used in the script.

You can find the detailed steps below if you wish to set up dependencies manually, but the above script handles everything for you (including the optional PIX and Agility SDK components).

godot-nir-static library. We compile the Mesa libraries you will need into a static library. Download it anywhere, unzip it and remember the path to the unzipped folder, you will need it below.

You can optionally build the godot-nir-static libraries yourself with the following steps:

Install the Python package mako which is needed to generate some files.

Clone the godot-nir-static directory and navigate to it.

If you are building with MinGW-w64, add use_mingw=yes to the scons command, you can also specify the build architecture using arch={architecture}. If you are building with MinGW-LLVM, add both use_mingw=yes and use_llvm=yes to the scons command.

If you are building with MinGW and the binaries are not located in the PATH, add mingw_prefix="/path/to/mingw" to the scons command.

The Mesa static library should be built using the same compiler and the same CRT (if you are building with MinGW) you are using for building Godot.

Optionally, you can compile with the following for additional features:

PIX is a performance tuning and debugging application for Direct3D12 applications. If you compile-in support for it, you can get much more detailed information through PIX that will help you optimize your game and troubleshoot graphics bugs. To use it, download the WinPixEventRuntime package. You will be taken to a NuGet package page where you can click "Download package" to get it. Once downloaded, change the file extension to .zip and unzip the file to some path.

Agility SDK can be used to provide access to the latest Direct3D 12 features without relying on driver updates. To use it, download the latest Agility SDK package. You will be taken to a NuGet package page where you can click "Download package" to get it. Once downloaded, change the file extension to .zip and unzip the file to some path.

If you use a preview version of the Agility SDK, remember to enable developer mode in Windows; otherwise it won't be used.

If you want to use a PIX with MinGW build, navigate to PIX runtime directory and use the following commands to generate import library:

When building Godot, you will need to tell SCons to use Direct3D 12 and where to look for the additional libraries:

Or, with all options enabled:

For the Agility SDK's DLLs you have to explicitly choose the kind of workflow. Single-arch is the default (DLLs copied to bin/). If you pass agility_sdk_multi_arch=yes to SCons, you'll opt-in for multi-arch. DLLs will be copied to the appropriate bin/<arch>/ subdirectories and at runtime the right one will be loaded.

AccessKit provides support for screen readers.

By default, Godot is built with AccessKit dynamically linked. You can use it by placing accesskit.dll alongside the executable.

You can use dynamically linked AccessKit with export templates as well, rename the DLL to accesskit.{architecture}.dll and place them alongside the export template executables, and the libraries will be automatically copied during the export process.

To compile Godot with statically linked AccessKit:

Download the pre-built static libraries from godot-accesskit-c-static library, and unzip them.

When building Godot, add accesskit_sdk_path={path} to tell SCons where to look for the AccessKit libraries:

You can optionally build the godot-angle-static libraries yourself with the following steps:

Clone the godot-accesskit-c-static directory and navigate to it.

Run the following command:

The AccessKit static library should be built using the same compiler and the same CRT (if you are building with MinGW) you are using for building Godot.

ANGLE provides a translation layer from OpenGL ES 3.x to Direct3D 11 and can be used to improve support for the Compatibility renderer on some older GPUs with outdated OpenGL drivers and on Windows for ARM.

By default, Godot is built with dynamically linked ANGLE, you can use it by placing libEGL.dll and libGLESv2.dll alongside the executable.

You can use dynamically linked ANGLE with export templates as well, rename the DLLs to libEGL.{architecture}.dll and libGLESv2.{architecture}.dll and place them alongside the export template executables, and the libraries will be automatically copied during the export process.

To compile Godot with statically linked ANGLE:

Download the pre-built static libraries from godot-angle-static library, and unzip them.

When building Godot, add angle_libs={path} to tell SCons where to look for the ANGLE libraries:

You can optionally build the godot-angle-static libraries yourself with the following steps:

Clone the godot-angle-static directory and navigate to it.

Run the following command:

If you are buildng with MinGW, add use_mingw=yes to the command, you can also specify the build architecture using arch={architecture}. If you are building with MinGW-LLVM, add both use_mingw=yes and use_llvm=yes to the scons command.

If you are building with MinGW and the binaries are not located in the PATH, add mingw_prefix="/path/to/mingw" to the scons command.

The ANGLE static library should be built using the same compiler and the same CRT (if you are building with MinGW) you are using for building Godot.

Using an IDE is not required to compile Godot, as SCons takes care of everything. But if you intend to do engine development or debugging of the engine's C++ code, you may be interested in configuring a code editor or an IDE.

Folder-based editors don't require any particular setup to start working with Godot's codebase. To edit projects with Visual Studio they need to be set up as a solution.

You can create a Visual Studio solution via SCons by running SCons with the vsproj=yes parameter, like this:

You will be able to open Godot's source in a Visual Studio solution now, and able to build Godot using Visual Studio's Build button.

See Visual Studio for further details.

If you get a compilation failure when using MSVC, make sure to apply the latest updates. You can do so by starting the Visual Studio IDE and using Continue without code, then Help > Check for Updates in the menu bar at the top. Install all updates, then try compiling again.

If you are a Linux or macOS user, you need to install MinGW-w64, which typically comes in 32-bit and 64-bit variants, or MinGW-LLVM, which comes as a single archive for all target architectures. The package names may differ based on your distribution, here are some known ones:

Before attempting the compilation, SCons will check for the following binaries in your PATH environment variable:

If the binaries are not located in the PATH (e.g. /usr/bin), you can define the following environment variable to give a hint to the build system:

Where /path/to/mingw is the path containing the bin directory where i686-w64-mingw32-gcc and x86_64-w64-mingw32-gcc are located (e.g. /opt/mingw-w64 if the binaries are located in /opt/mingw-w64/bin).

To make sure you are doing things correctly, executing the following in the shell should result in a working compiler (the version output may differ based on your system):

If you are building with MinGW-LLVM, add use_llvm=yes to the scons command.

When cross-compiling for Windows using MinGW-w64, keep in mind only x86_64 and x86_32 architectures are supported. MinGW-LLVM supports arm64 as well. Be sure to specify the right arch= option when invoking SCons if building from a different architecture.

Cross-compiling from some Ubuntu versions may lead to this bug, due to a default configuration lacking support for POSIX threading.

You can change that configuration following those instructions, for 64-bit:

Windows export templates are created by compiling Godot without the editor, with the following flags:

If you plan on replacing the standard export templates, copy these to the following location, replacing <version> with the version identifier (such as 4.2.1.stable or 4.3.dev):

With the following names:

However, if you are using custom modules or custom engine code, you may instead want to configure your binaries as custom export templates in the project export menu. You must have Advanced Options enabled to set this.

You don't need to copy them in this case, just reference the resulting files in the bin\ directory of your Godot source folder, so the next time you build, you will automatically have the custom templates referenced.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Compiling with .NET — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/compiling_with_dotnet.html

**Contents:**
- Compiling with .NET
- Requirements
- Enable the .NET module
- Generate the glue
- Building the managed libraries
  - Build Platform
  - NuGet packages
  - Building without depending on deprecated features (NO_DEPRECATED)
  - Double Precision Support (REAL_T_IS_DOUBLE)
- Examples

You can use dotnet --info to check which .NET SDK versions are installed.

C# support for Godot has historically used the Mono runtime instead of the .NET Runtime and internally many things are still named mono instead of dotnet or otherwise referred to as mono.

By default, the .NET module is disabled when building. To enable it, add the option module_mono_enabled=yes to the SCons command line, while otherwise following the instructions for building the desired Godot binaries.

Parts of the sources of the managed libraries are generated from the ClassDB. These source files must be generated before building the managed libraries. They can be generated by any .NET-enabled Godot editor binary by running it with the parameters --headless --generate-mono-glue followed by the path to an output directory. This path must be modules/mono/glue in the Godot directory:

This command will tell Godot to generate the C# bindings for the Godot API at modules/mono/glue/GodotSharp/GodotSharp/Generated, and the C# bindings for the editor tools at modules/mono/glue/GodotSharp/GodotSharpEditor/Generated. Once these files are generated, you can build Godot's managed libraries for all the desired targets without having to repeat this process.

<godot_binary> refers to the editor binary you compiled with the .NET module enabled. Its exact name will differ based on your system and configuration, but should be of the form bin/godot.<platform>.editor.<arch>.mono, e.g. bin/godot.linuxbsd.editor.x86_64.mono or bin/godot.windows.editor.x86_32.mono.exe. Be especially aware of the .mono suffix! If you've previously compiled Godot without .NET support, you might have similarly named binaries without this suffix. These binaries can't be used to generate the .NET glue.

The glue sources must be regenerated every time the ClassDB-registered API changes. That is, for example, when a new method is registered to the scripting API or one of the parameters of such a method changes. Godot will print an error at startup if there is an API mismatch between ClassDB and the glue sources.

Once you have generated the .NET glue, you can build the managed libraries with the build_assemblies.py script:

If everything went well, the GodotSharp directory, containing the managed libraries, should have been created in the bin directory.

By default, all development builds share a version number, which can cause some issues with caching of the NuGet packages. To solve this issue either use GODOT_VERSION_STATUS to give every build a unique version or delete GodotNuGetFallbackFolder after every build to clear the package cache.

Unlike "classical" Godot builds, when building with the .NET module enabled (and depending on the target platform), a data directory may be created both for the editor and for exported projects. This directory is important for proper functioning and must be distributed together with Godot. More details about this directory in Data directory.

Provide the --godot-platform=<platform> argument to control for which platform specific the libraries are built. Omit this argument to build for the current system.

This currently only controls the inclusion of the support for Visual Studio as an external editor, the libraries are otherwise identical.

The API assemblies, source generators, and custom MSBuild project SDK are distributed as NuGet packages. This is all transparent to the user, but it can make things complicated during development.

In order to use Godot with a development version of those packages, a local NuGet source must be created where MSBuild can find them.

First, pick a location for the local NuGet source. If you don't have a preference, create an empty directory at one of these recommended locations:

On Windows, C:\Users\<username>\MyLocalNugetSource

On Linux, *BSD, etc., ~/MyLocalNugetSource

This path is referred to later as <my_local_source>.

After picking a directory, run this .NET CLI command to configure NuGet to use your local source:

When you run the build_assemblies.py script, pass <my_local_source> to the --push-nupkgs-local option:

This option ensures the packages will be added to the specified local NuGet source and that conflicting versions of the package are removed from the NuGet cache. It's recommended to always use this option when building the C# solutions during development to avoid mistakes.

When building Godot without deprecated classes and functions, i.e. the deprecated=no argument for scons, the managed libraries must also be built without dependencies to deprecated code. This is done by passing the --no-deprecated argument:

When building Godot with double precision support, i.e. the precision=double argument for scons, the managed libraries must be adjusted to match by passing the --precision=double argument:

The data directory is a dependency for Godot binaries built with the .NET module enabled. It contains important files for the correct functioning of Godot. It must be distributed together with the Godot executable.

The name of the data directory for the Godot editor will always be GodotSharp. This directory contains an Api subdirectory with the Godot API assemblies and a Tools subdirectory with the tools required by the editor, like the GodotTools assemblies and its dependencies.

On macOS, if the Godot editor is distributed as a bundle, the GodotSharp directory may be placed in the <bundle_name>.app/Contents/Resources/ directory inside the bundle.

The data directory for exported projects is generated by the editor during the export. It is named data_<APPNAME>_<ARCH>, where <APPNAME> is the application name as specified in the project setting application/config/name and <ARCH> is the current architecture of the export.

In the case of multi-architecture exports multiple such data directories will be generated.

The following is the list of command-line options available when building with the .NET module:

module_mono_enabled=yes | no

Build Godot with the .NET module enabled.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Compiling with PCK encryption key — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/compiling_with_script_encryption_key.html

**Contents:**
- Compiling with PCK encryption key
- Step by step
- Troubleshooting
- User-contributed notes

The export dialog gives you the option to encrypt your PCK file with a 256-bit AES key when releasing your project. This will make sure your scenes, scripts and other resources are not stored in plain text and can not easily be ripped by some script kiddie.

Of course, the key needs to be stored in the binary, but if it's compiled, optimized and without symbols, it would take some effort to find it.

For this to work, you need to build the export templates from source, with that same key.

This will not work if you use official, precompiled export templates. It is absolutely required to compile your own export templates to use PCK encryption.

Generate a 256-bit AES key in hexadecimal format. You can use the aes-256-cbc variant from this service.

Alternatively, you can generate it yourself using OpenSSL command-line tools:

The output in godot.gdkey should be similar to:

You can generate the key without redirecting the output to a file, but that way you can minimize the risk of exposing the key.

Set this key as environment variable in the console that you will use to compile Godot, like this:

Compile Godot export templates and set them as custom export templates in the export preset options.

Set the encryption key in the Encryption tab of the export preset:

Add filters for the files/folders to encrypt. By default, include filters are empty and nothing will be encrypted.

Export the project. The project should run with the files encrypted now.

If you get an error like below, it means the key wasn't properly included in your Godot build. Godot is encrypting PCK file during export, but can't read it at runtime.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Core types — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/core_types.html

**Contents:**
- Core types
- Definitions
- Memory model
- Allocating memory
- Containers
- Math types
- NodePath
- RID
- User-contributed notes

Godot has a rich set of classes and templates that compose its core, and everything is built upon them.

This reference will try to list them in order for their better understanding.

Godot uses the standard C99 datatypes, such as uint8_t, uint32_t, int64_t, etc. which are nowadays supported by every compiler. Reinventing the wheel for those is not fun, as it makes code more difficult to read.

In general, care is not taken to use the most efficient datatype for a given task unless using large structures or arrays. int is used through most of the code unless necessary. This is done because nowadays every device has at least a 32-bit bus and can do such operations in one cycle. It makes code more readable too.

For files or memory sizes, size_t is used, which is guaranteed to be 64-bit.

For Unicode characters, CharType instead of wchar_t is used, because many architectures have 4 bytes long wchar_t, where 2 bytes might be desired. However, by default, this has not been forced and CharType maps directly to wchar_t.

PC is a wonderful architecture. Computers often have gigabytes of RAM, terabytes of storage and gigahertz of CPU, and when an application needs more resources the OS will swap out the inactive ones. Other architectures (like mobile or consoles) are in general more limited.

The most common memory model is the heap, where an application will request a region of memory, and the underlying OS will try to fit it somewhere and return it. This often works best and is flexible, but over time and with abuse, this can lead to segmentation.

Segmentation slowly creates holes that are too small for most common allocations, so that memory is wasted. There is a lot of literature about heap and segmentation, so this topic will not be developed further here. Modern operating systems use paged memory, which helps mitigate the problem of segmentation but doesn't solve it.

However, in many studies and tests, it is shown that given enough memory, if the maximum allocation size is below a given threshold in proportion to the maximum heap size and proportion of memory intended to be unused, segmentation will not be a problem over time as it will remain constant. In other words, leave 10-20% of your memory free and perform all small allocations and you are fine.

Godot ensures that all objects that can be allocated dynamically are small (less than a few kB at most). But what happens if an allocation is too large (like an image or mesh geometry or large array)? In this case Godot has the option to use a dynamic memory pool. This memory needs to be locked to be accessed, and if an allocation runs out of memory, the pool will be rearranged and compacted on demand. Depending on the need of the game, the programmer can configure the dynamic memory pool size.

Godot has many tools for tracking memory usage in a game, especially during debug. Because of this, the regular C and C++ library calls should not be used. Instead, a few other ones are provided.

For C-style allocation, Godot provides a few macros:

These are equivalent to the usual malloc(), realloc(), and free() of the C standard library.

For C++-style allocation, special macros are provided:

These are equivalent to new, delete, new[], and delete[] respectively.

memnew/memdelete also use a little C++ magic and notify Objects right after they are created, and right before they are deleted.

For dynamic memory, use one of Godot's sequence types such as Vector<> or LocalVector<>. Vector<> behaves much like an STL std::vector<>, but is simpler and uses Copy-On-Write (CoW) semantics. CoW copies of Vector<> can safely access the same data from different threads, but several threads cannot access the same Vector<> instance safely. It can be safely passed via public API if it has a Packed alias.

The Packed*Array types are aliases for specific Vector<*> types (e.g., PackedByteArray, PackedInt32Array) that are accessible via GDScript. Outside of core, prefer using the Packed*Array aliases for functions exposed to scripts, and Vector<> for other occasions.

LocalVector<> is much more like std::vector than Vector<>. It is non-CoW, with less overhead. It is intended for internal use where the benefits of CoW are not needed. Note that neither LocalVector<> nor Vector<> are drop-in replacements for each other. They are two unrelated types with similar interfaces, both using a buffer as their storage strategy.

List<> is another Godot sequence type, using a doubly-linked list as its storage strategy. Prefer Vector<> (or LocalVector<>) over List<> unless you're sure you need it, as cache locality and memory fragmentation tend to be more important with small collections.

Godot provides its own set of containers, which means STL containers like std::string and std::vector are generally not used in the codebase. See Why does Godot not use STL (Standard Template Library)? for more information.

A  icon denotes the type is part of Variant. This means it can be used as a parameter or return value of a method exposed to the scripting API.

Closest C++ STL datatype

Use this as the "default" string type. String uses UTF-32 encoding to simplify processing thanks to its fixed character size.

Use this as the "default" vector type. Uses copy-on-write (COW) semantics. This means it's generally slower but can be copied around almost for free. Use LocalVector instead where COW isn't needed and performance matters.

Use this as the "default" set type.

Use this as the "default" map type. Does not preserve insertion order. Note that pointers into the map, as well as iterators, are not stable under mutations. If either of these affordances are needed, use HashMap instead.

Uses string interning for fast comparisons. Use this for static strings that are referenced frequently and used in multiple locations in the engine.

Closer to std::vector in semantics, doesn't use copy-on-write (COW) thus it's faster than Vector. Prefer it over Vector when copying it cheaply is not needed.

Values can be of any Variant type. No static typing is imposed. Uses shared reference counting, similar to std::shared_ptr. Uses Vector<Variant> internally.

Subclass of Array but with static typing for its elements. Not to be confused with Packed*Array, which is internally a Vector.

Alias of Vector, e.g. PackedColorArray = Vector<Color>. Only a limited list of packed array types are available (use TypedArray otherwise).

Linked list type. Generally slower than other array/vector types. Prefer using other types in new code, unless using List avoids the need for type conversions.

Vector with a fixed capacity (more similar to boost::container::static_vector). This container type is more efficient than other vector-like types because it makes no heap allocations.

Represents read-only access to a contiguous array without needing to copy any data. Note that Span is designed to be a high performance API: It does not perform parameter correctness checks in the same way you might be used to with other Godot containers. Use with care. Span can be constructed from most array-like containers (e.g. vector.span()).

Uses a red-black tree for faster access.

Uses copy-on-write (COW) semantics. This means it's generally slower but can be copied around almost for free. The performance benefits of VSet aren't established, so prefer using other types.

Defensive (robust but slow) map type. Preserves insertion order. Pointers to keys and values, as well as iterators, are stable under mutation. Use this map type when either of these affordances are needed. Use AHashMap otherwise.

Map type that uses a red-black tree to find keys. The performance benefits of RBMap aren't established, so prefer using other types.

Keys and values can be of any Variant type. No static typing is imposed. Uses shared reference counting, similar to std::shared_ptr. Preserves insertion order. Uses HashMap<Variant> internally.

Subclass of Dictionary but with static typing for its keys and values.

Stores a single pair. See also KeyValue in the same file, which uses read-only keys.

There are several linear math types available in the core/math directory:

This is a special datatype used for storing paths in a scene tree and referencing them in an optimized manner:

core/string/node_path.h

RIDs are Resource IDs. Servers use these to reference data stored in them. RIDs are opaque, meaning that the data they reference can't be accessed directly. RIDs are unique, even for different types of referenced data:

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Cross-compiling for iOS on Linux — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/cross-compiling_for_ios_on_linux.html

**Contents:**
- Cross-compiling for iOS on Linux
- Disclaimer
- Requirements
- Configuring the environment
  - Preparing the SDK
  - Toolchain
- Compiling Godot for iPhone
- User-contributed notes

The procedure for this is somewhat complex and requires a lot of steps, but once you have the environment properly configured you can compile Godot for iOS anytime you want.

While it is possible to compile for iOS on a Linux environment, Apple is very restrictive about the tools to be used (especially hardware-wise), allowing pretty much only their products to be used for development. So this is not official. However, in 2010 Apple said they relaxed some of the App Store review guidelines to allow any tool to be used, as long as the resulting binary does not download any code, which means it should be OK to use the procedure described here and cross-compiling the binary.

XCode with the iOS SDK (you must be logged into an Apple ID to download Xcode).

Clang >= 3.5 for your development machine installed and in the PATH. It has to be version >= 3.5 to target arm64 architecture.

xar and pbzx (required to extract the .xip archive Xcode comes in).

For building xar and pbzx, you may want to follow this guide.

cctools-port for the needed build tools. The procedure for building is quite peculiar and is described below.

This also has some extra dependencies: automake, autogen, libtool.

Extract the Xcode .xip file you downloaded from Apple's developer website:

Note that for the commands below, you will need to replace the version (x.x) with whatever iOS SDK version you're using. If you don't know your iPhone SDK version, you can see the JSON file inside of Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs.

Pack the SDK so that cctools can use it:

Copy the tools to a nicer place. Note that the SCons scripts for building will look under usr/bin inside the directory you provide for the toolchain binaries, so you must copy to such subdirectory, akin to the following commands:

Now you should have the iOS toolchain binaries in $HOME/iostoolchain/usr/bin.

Once you've done the above steps, you should keep two things in your environment: the built toolchain and the iPhoneOS SDK directory. Those can stay anywhere you want since you have to provide their paths to the SCons build command.

For the iPhone platform to be detected, you need the OSXCROSS_IOS environment variable defined to anything.

Now you can compile for iPhone using SCons like the standard Godot way, with some additional arguments to provide the correct paths:

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Custom AudioStreams — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/custom_audiostreams.html

**Contents:**
- Custom AudioStreams
- Introduction
  - References:
- What for?
- Create an AudioStream
  - References:
- Create an AudioStreamPlayback
  - Resampling
  - References:
- User-contributed notes

AudioStream is the base class of all audio emitting objects. AudioStreamPlayer binds onto an AudioStream to emit PCM data into an AudioServer which manages audio drivers.

All audio resources require two audio based classes: AudioStream and AudioStreamPlayback. As a data container, AudioStream contains the resource and exposes itself to GDScript. AudioStream references its own internal custom AudioStreamPlayback which translates AudioStream into PCM data.

This guide assumes the reader knows how to create C++ modules. If not, refer to this guide Custom modules in C++.

servers/audio/audio_stream.h

scene/audio/audio_stream_player.cpp

Binding external libraries (like Wwise, FMOD, etc).

Adding custom audio queues

Adding support for more audio formats

An AudioStream consists of three components: data container, stream name, and an AudioStreamPlayback friend class generator. Audio data can be loaded in a number of ways such as with an internal counter for a tone generator, internal/external buffer, or a file reference.

Some AudioStreams need to be stateless such as objects loaded from ResourceLoader. ResourceLoader loads once and references the same object regardless how many times load is called on a specific resource. Therefore, playback state must be self-contained in AudioStreamPlayback.

servers/audio/audio_stream.h

AudioStreamPlayer uses mix callback to obtain PCM data. The callback must match sample rate and fill the buffer.

Since AudioStreamPlayback is controlled by the audio thread, i/o and dynamic memory allocation are forbidden.

Godot's AudioServer currently uses 44100 Hz sample rate. When other sample rates are needed such as 48000, either provide one or use AudioStreamPlaybackResampled. Godot provides cubic interpolation for audio resampling.

Instead of overloading mix, AudioStreamPlaybackResampled uses _mix_internal to query AudioFrames and get_stream_sampling_rate to query current mix rate.

core/math/audio_frame.h

servers/audio/audio_stream.h

scene/audio/audio_stream_player.cpp

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Custom Godot servers — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/custom_godot_servers.html

**Contents:**
- Custom Godot servers
- Introduction
  - References
- What for?
- Creating a Godot server
- Custom managed resource data
  - References
- Registering the class in GDScript
  - Bind methods
- MessageQueue

Godot implements multi-threading as servers. Servers are daemons which manage data, process it, and push the result. Servers implement the mediator pattern which interprets resource ID and process data for the engine and other modules. In addition, the server claims ownership for its RID allocations.

This guide assumes the reader knows how to create C++ modules and Godot data types. If not, refer to Custom modules in C++.

Why does Godot use servers and RIDs?

Adding artificial intelligence.

Adding custom asynchronous threads.

Adding support for a new input device.

Adding writing threads.

Adding a custom VoIP protocol.

At minimum, a server must have a static instance, a sleep timer, a thread loop, an initialization state and a cleanup procedure.

Godot servers implement a mediator pattern. All data types inherit RID_Data. RID_Owner<MyRID_Data> owns the object when make_rid is called. During debug mode only, RID_Owner maintains a list of RIDs. In practice, RIDs are similar to writing object-oriented C code.

Servers are allocated in register_types.cpp. The constructor sets the static instance and init() creates the managed thread; unregister_types.cpp cleans up the server.

Since a Godot server class creates an instance and binds it to a static singleton, binding the class might not reference the correct instance. Therefore, a dummy class must be created to reference the proper Godot server.

In register_server_types(), Engine::get_singleton()->add_singleton is used to register the dummy class in GDScript.

servers/register_server_types.cpp

The dummy class binds singleton methods to GDScript. In most cases, the dummy class methods wraps around.

It is possible to emit signals to GDScript by calling the GDScript dummy object.

In order to send commands into SceneTree, MessageQueue is a thread-safe buffer to queue set and call methods for other threads. To queue a command, obtain the target object RID and use either push_call, push_set, or push_notification to execute the desired behavior. The queue will be flushed whenever either SceneTree::idle or SceneTree::iteration is executed.

core/object/message_queue.cpp

Here is the GDScript sample code:

The actual Hilbert Hotel is impossible.

Connecting signal example code is pretty hacky.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Custom modules in C++ — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/custom_modules_in_cpp.html

**Contents:**
- Custom modules in C++
- Modules
- What for?
- Creating a new module
- Using the module
- Compiling a module externally
- Customizing module types initialization
- Writing custom documentation
- Writing custom unit tests
- Adding custom editor icons

Godot allows extending the engine in a modular way. New modules can be created and then enabled/disabled. This allows for adding new engine functionality at every level without modifying the core, which can be split for use and reuse in different modules.

Modules are located in the modules/ subdirectory of the build system. By default, dozens of modules are enabled, such as GDScript (which, yes, is not part of the base engine), GridMap support, a regular expressions module, and others. As many new modules as desired can be created and combined. The SCons build system will take care of it transparently.

While it's recommended that most of a game be written in scripting (as it is an enormous time saver), it's perfectly possible to use C++ instead. Adding C++ modules can be useful in the following scenarios:

Binding an external library to Godot (like PhysX, FMOD, etc).

Optimize critical parts of a game.

Adding new functionality to the engine and/or editor.

Porting an existing game to Godot.

Write a whole, new game in C++ because you can't live without C++.

While it is possible to use modules for custom game logic, GDExtension is generally more suited as it doesn't require recompiling the engine after every code change.

C++ modules are mainly needed when GDExtension doesn't suffice and deeper engine integration is required.

Before creating a module, make sure to download the source code of Godot and compile it.

To create a new module, the first step is creating a directory inside modules/. If you want to maintain the module separately, you can checkout a different VCS into modules and use it.

The example module will be called "summator" (godot/modules/summator). Inside we will create a summator class:

And then the cpp file.

Then, the new class needs to be registered somehow, so two more files need to be created:

These files must be in the top-level folder of your module (next to your SCsub and config.py files) for the module to be registered properly.

These files should contain the following:

Next, we need to create an SCsub file so the build system compiles this module:

With multiple sources, you can also add each file individually to a Python string list:

This allows for powerful possibilities using Python to construct the file list using loops and logic statements. Look at some modules that ship with Godot by default for examples.

To add include directories for the compiler to look at you can append it to the environment's paths:

If you want to add custom compiler flags when building your module, you need to clone env first, so it won't add those flags to whole Godot build (which can cause errors). Example SCsub with custom flags:

And finally, the configuration file for the module, this is a Python script that must be named config.py:

The module is asked if it's OK to build for the specific platform (in this case, True means it will build for every platform).

And that's it. Hope it was not too complex! Your module should look like this:

You can then zip it and share the module with everyone else. When building for every platform (instructions in the previous sections), your module will be included.

You can now use your newly created module from any script:

The output will be 60.

The previous Summator example is great for small, custom modules, but what if you want to use a larger, external library? Refer to Binding to external libraries for details about binding to external libraries.

If your module is meant to be accessed from the running project (not just from the editor), you must also recompile every export template you plan to use, then specify the path to the custom template in each export preset. Otherwise, you'll get errors when running the project as the module isn't compiled in the export template. See the Compiling pages for more information.

Compiling a module involves moving the module's sources directly under the engine's modules/ directory. While this is the most straightforward way to compile a module, there are a couple of reasons as to why this might not be a practical thing to do:

Having to manually copy modules sources every time you want to compile the engine with or without the module, or taking additional steps needed to manually disable a module during compilation with a build option similar to module_summator_enabled=no. Creating symbolic links may also be a solution, but you may additionally need to overcome OS restrictions like needing the symbolic link privilege if doing this via script.

Depending on whether you have to work with the engine's source code, the module files added directly to modules/ changes the working tree to the point where using a VCS (like git) proves to be cumbersome as you need to make sure that only the engine-related code is committed by filtering changes.

So if you feel like the independent structure of custom modules is needed, lets take our "summator" module and move it to the engine's parent directory:

Compile the engine with our module by providing custom_modules build option which accepts a comma-separated list of directory paths containing custom C++ modules, similar to the following:

The build system shall detect all modules under the ../modules directory and compile them accordingly, including our "summator" module.

Any path passed to custom_modules will be converted to an absolute path internally as a way to distinguish between custom and built-in modules. It means that things like generating module documentation may rely on a specific path structure on your machine.

Introduction to the buildsystem - Custom modules build option.

Modules can interact with other built-in engine classes during runtime and even affect the way core types are initialized. So far, we've been using register_summator_types as a way to bring in module classes to be available within the engine.

A crude order of the engine setup can be summarized as a list of the following type registration methods:

Our Summator class is initialized during the register_module_types() call. Imagine that we need to satisfy some common module runtime dependency (like singletons), or allow us to override existing engine method callbacks before they can be assigned by the engine itself. In that case, we want to ensure that our module classes are registered before any other built-in type.

This is where we can define an optional preregister_summator_types() method which will be called before anything else during the preregister_module_types() engine setup stage.

We now need to add this method to register_types header and source files:

Unlike other register methods, we have to explicitly define MODULE_SUMMATOR_HAS_PREREGISTER to let the build system know what relevant method calls to include at compile time. The module's name has to be converted to uppercase as well.

Writing documentation may seem like a boring task, but it is highly recommended to document your newly created module to make it easier for users to benefit from it. Not to mention that the code you've written one year ago may become indistinguishable from the code that was written by someone else, so be kind to your future self!

There are several steps in order to setup custom docs for the module:

Make a new directory in the root of the module. The directory name can be anything, but we'll be using the doc_classes name throughout this section.

Now, we need to edit config.py, add the following snippet:

The get_doc_path() function is used by the build system to determine the location of the docs. In this case, they will be located in the modules/summator/doc_classes directory. If you don't define this, the doc path for your module will fall back to the main doc/classes directory.

The get_doc_classes() method is necessary for the build system to know which registered classes belong to the module. You need to list all of your classes here. The classes that you don't list will end up in the main doc/classes directory.

You can use Git to check if you have missed some of your classes by checking the untracked files with git status. For example:

Now we can generate the documentation:

We can do this via running Godot's doctool i.e. godot --doctool <path>, which will dump the engine API reference to the given <path> in XML format.

In our case we'll point it to the root of the cloned repository. You can point it to an another folder, and just copy over the files that you need.

Now if you go to the godot/modules/summator/doc_classes folder, you will see that it contains a Summator.xml file, or any other classes, that you referenced in your get_doc_classes function.

Edit the file(s) following the class reference primer and recompile the engine.

Once the compilation process is finished, the docs will become accessible within the engine's built-in documentation system.

In order to keep documentation up-to-date, all you'll have to do is simply modify one of the XML files and recompile the engine from now on.

If you change your module's API, you can also re-extract the docs, they will contain the things that you previously added. Of course if you point it to your godot folder, make sure you don't lose work by extracting older docs from an older engine build on top of the newer ones.

Note that if you don't have write access rights to your supplied <path>, you might encounter an error similar to the following:

It's possible to write self-contained unit tests as part of a C++ module. If you are not familiar with the unit testing process in Godot yet, please refer to Unit testing.

The procedure is the following:

Create a new directory named tests/ under your module's root:

Create a new test suite: test_summator.h. The header must be prefixed with test_ so that the build system can collect it and include it as part of the tests/test_main.cpp where the tests are run.

Write some test cases. Here's an example:

Compile the engine with scons tests=yes, and run the tests with the following command:

You should see the passing assertions now.

Similarly to how you can write self-contained documentation within a module, you can also create your own custom icons for classes to appear in the editor.

For the actual process of creating editor icons to be integrated within the engine, please refer to Editor icons first.

Once you've created your icon(s), proceed with the following steps:

Make a new directory in the root of the module named icons. This is the default path for the engine to look for module's editor icons.

Move your newly created svg icons (optimized or not) into that folder.

Recompile the engine and run the editor. Now the icon(s) will appear in editor's interface where appropriate.

If you'd like to store your icons somewhere else within your module, add the following code snippet to config.py to override the default path:

Use GDCLASS macro for inheritance, so Godot can wrap it.

Use _bind_methods to bind your functions to scripting, and to allow them to work as callbacks for signals.

Avoid multiple inheritance for classes exposed to Godot, as GDCLASS doesn't support this. You can still use multiple inheritance in your own classes as long as they're not exposed to Godot's scripting API.

But this is not all, depending what you do, you will be greeted with some (hopefully positive) surprises.

If you inherit from Node (or any derived node type, such as Sprite2D), your new class will appear in the editor, in the inheritance tree in the "Add Node" dialog.

If you inherit from Resource, it will appear in the resource list, and all the exposed properties can be serialized when saved/loaded.

By this same logic, you can extend the Editor and almost any area of the engine.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Custom platform ports — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/custom_platform_ports.html

**Contents:**
- Custom platform ports
- Official platform ports
- Creating a custom platform port
  - Required features of a platform port
  - Optional features of a platform port
- Distributing a custom platform port
- User-contributed notes

Similar to Custom modules in C++, Godot's multi-platform architecture is designed in a way that allows creating platform ports without modifying any existing source code.

An example of a custom platform port distributed independently from the engine is FRT, which targets single-board computers. Note that this platform port currently targets Godot 3.x; therefore, it does not use the DisplayServer abstraction that is new in Godot 4.

Some reasons to create custom platform ports might be:

You want to port your game to consoles, but wish to write the platform layer yourself. This is a long and arduous process, as it requires signing NDAs with console manufacturers, but it allows you to have full control over the console porting process.

You want to port Godot to an exotic platform that isn't currently supported.

If you have questions about creating a custom platform port, feel free to ask in the #platforms channel of the Godot Contributors Chat.

Godot is a modern engine with modern requirements. Even if you only intend to run simple 2D projects on the target platform, it still requires an amount of memory that makes it unviable to run on most retro consoles. For reference, in Godot 4, an empty project with nothing visible requires about 100 MB of RAM to run on Linux (50 MB in headless mode).

If you want to run Godot on heavily memory-constrained platforms, older Godot versions have lower memory requirements. The porting process is similar, with the exception of DisplayServer not being split from the OS singleton.

The official platform ports can be used as a reference when creating a custom platform port:

While platform code is usually self-contained, there are exceptions to this rule. For instance, audio drivers that are shared across several platforms and rendering drivers are located in the drivers/ folder of the Godot source code.

Creating a custom platform port is a large undertaking which requires prior knowledge of the platform's SDKs. Depending on what features you need, the amount of work needed varies:

At the very least, a platform port must have methods from the OS singleton implemented to be buildable and usable for headless operation. A logo.svg (32×32) vector image must also be present within the platform folder. This logo is displayed in the Export dialog for each export preset targeting the platform in question.

See this implementation for the Linux/*BSD platform as an example. See also the OS singleton header for reference.

If your target platform is UNIX-like, consider inheriting from the OS_Unix class to get much of the work done automatically.

If the platform is not UNIX-like, you might use the Windows port as a reference.

A detect.py file must be created within the platform's folder with all methods implemented. This file is required for SCons to detect the platform as a valid option for compiling. See the detect.py file for the Linux/*BSD platform as an example.

All methods should be implemented within detect.py as follows:

is_active(): Can be used to temporarily disable building for a platform. This should generally always return True.

get_name(): Returns the platform's user-visible name as a string.

can_build(): Return True if the host system is able to build for the target platform, False otherwise. Do not put slow checks here, as this is queried when the list of platforms is requested by the user. Use configure() for extensive dependency checks instead.

get_opts(): Returns the list of SCons build options that can be defined by the user for this platform.

get_flags(): Returns the list of overridden SCons flags for this platform.

configure(): Perform build configuration, such as selecting compiler options depending on SCons options chosen.

In practice, headless operation doesn't suffice if you want to see anything on screen and handle input devices. You may also want audio output for most games.

Some links on this list point to the Linux/*BSD platform implementation as a reference.

One or more DisplayServers, with the windowing methods implemented. DisplayServer also covers features such as mouse support, touchscreen support and tablet driver (for pen input). See the DisplayServer singleton header for reference.

For platforms not featuring full windowing support (or if it's not relevant for the port you are making), most windowing functions can be left mostly unimplemented. These functions can be made to only check if the window ID is MAIN_WINDOW_ID and specific operations like resizing may be tied to the platform's screen resolution feature (if relevant). Any attempt to create or manipulate other window IDs can be rejected.

If the target platform supports the graphics APIs in question: Rendering context for Vulkan, Direct3D 12 OpenGL 3.3 or OpenGL ES 3.0.

Input handlers for keyboard and controller.

One or more audio drivers. The audio driver can be located in the platform/ folder (this is done for the Android and Web platforms), or in the drivers/ folder if multiple platforms may be using this audio driver. See the AudioServer singleton header for reference.

Crash handler, for printing crash backtraces when the game crashes. This allows for easier troubleshooting on platforms where logs aren't readily accessible.

Text-to-speech driver (for accessibility).

Export handler (for exporting from the editor, including One-click deploy). Not required if you intend to export only a PCK from the editor, then run the export template binary directly by renaming it to match the PCK file. See the EditorExportPlatform header for reference. run_icon.svg (16×16) should be present within the platform folder if One-click deploy is implemented for the target platform. This icon is displayed at the top of the editor when one-click deploy is set up for the target platform.

If the target platform doesn't support running Vulkan, Direct3D 12, OpenGL 3.3, or OpenGL ES 3.0, you have two options:

Use a library at runtime to translate Vulkan or OpenGL calls to another graphics API. For example, MoltenVK is used on macOS to translate Vulkan to Metal at runtime.

Create a new renderer from scratch. This is a large undertaking, especially if you want to support both 2D and 3D rendering with advanced features.

Before distributing a custom platform port, make sure you're allowed to distribute all the code that is being linked against. Console SDKs are typically under NDAs which prevent redistribution to the public.

Platform ports are designed to be as self-contained as possible. Most of the code can be kept within a single folder located in platform/. Like Custom modules in C++, this allows for streamlining the build process by making it possible to git clone a platform folder within a Godot repository clone's platform/ folder, then run scons platform=<name>. No other steps are necessary for building, unless third-party platform-specific dependencies need to be installed first.

However, when a custom rendering driver is needed, another folder must be added in drivers/. In this case, the platform port can be distributed as a fork of the Godot repository, or as a collection of several folders that can be added over a Godot Git repository clone.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Custom resource format loaders — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/custom_resource_format_loaders.html

**Contents:**
- Custom resource format loaders
- Introduction
  - References
- What for?
- What not?
  - References
- Creating a ResourceFormatLoader
- Creating a ResourceFormatSaver
- Creating custom data types
  - Considerations

ResourceFormatLoader is a factory interface for loading file assets. Resources are primary containers. When load is called on the same file path again, the previous loaded Resource will be referenced. Naturally, loaded resources must be stateless.

This guide assumes the reader knows how to create C++ modules and Godot data types. If not, refer to this guide: Custom modules in C++

core/io/resource_loader.cpp

Adding new support for many file formats

Machine learning models

ImageFormatLoader should be used to load images.

core/io/image_loader.h

Each file format consist of a data container and a ResourceFormatLoader.

ResourceFormatLoaders are classes which return all the necessary metadata for supporting new extensions in Godot. The class must return the format name and the extension string.

In addition, ResourceFormatLoaders must convert file paths into resources with the load function. To load a resource, load must read and handle data serialization.

If you'd like to be able to edit and save a resource, you can implement a ResourceFormatSaver:

Godot may not have a proper substitute within its Core types or managed resources. Godot needs a new registered data type to understand additional binary formats such as machine learning models.

Here is an example of creating a custom datatype:

Some libraries may not define certain common routines such as IO handling. Therefore, Godot call translations are required.

For example, here is the code for translating FileAccess calls into std::istream.

core/io/file_access.h

Godot registers ResourcesFormatLoader with a ResourceLoader handler. The handler selects the proper loader automatically when load is called.

core/io/resource_loader.cpp

Save a file called demo.json with the following contents and place it in the project's root folder:

Then attach the following script to any node:

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Debugging on macOS — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/debugging/macos_debug.html

**Contents:**
- Debugging on macOS
- Debugging Godot editor
- Debugging exported project
- User-contributed notes

Attaching a debugger to the signed macOS process requires the "com.apple.security.get-task-allow" entitlement, which is not enabled by default, since apps can't be notarized as long as it is enabled. If you want to debug an official build of the editor it should be re-signed with the proper entitlements.

Create an editor.entitlements text file with the following contents:

Then use the following command to re-sign the editor:

To allow debugging, select the codesign\debugging (com.apple.security.get-task-allow) entitlement during the export. When it is selected, notarization is not supported and should be disabled.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Editor icons — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/editor/creating_icons.html

**Contents:**
- Editor icons
- Creating icons
- Color conversion for light editor themes
- Icon optimization
- Integrating and sharing the icons
- Troubleshooting
- References
- User-contributed notes

When a new class is created and exposed to scripting, the editor's interface will display it with a default icon representing the base class it inherits from. In most cases, it's still recommended to create icons for new classes to improve the user experience.

To create new icons, you first need a vector graphics editor installed. For instance, you can use the open source Inkscape editor.

Clone the godot repository containing all the editor icons:

The icons must be created in a vector graphics editor in SVG format. There are two main requirements to follow:

Icons must be 16×16. In Inkscape, you can configure the document size in File > Document Properties.

Lines should be snapped to pixels whenever possible to remain crisp at lower DPI. You can create a 16×16 grid in Inkscape to make this easier.

Once you're satisfied with the icon's design, save the icon in the cloned repository's editor/icons folder. The icon name should match the intended name in a case-sensitive manner. For example, to create an icon for CPUParticles2D, name the file CPUParticles2D.svg.

If the user has configured their editor to use a light theme, Godot will convert the icon's colors based on a set of predefined color mappings. This is to ensure the icon always displays with a sufficient contrast rate. Try to restrict your icon's color palette to colors found in the list above. Otherwise, your icon may become difficult to read on a light background.

Import > Import As > Texture2D

Set editor/convert_colors_with_editor_theme to true

Because the editor renders SVGs once at load time, they need to be small in size so they can be efficiently parsed. When the pre-commit hook runs, it automatically optimizes the SVG using svgo.

While this optimization step won't impact the icon's quality noticeably, it will still remove editor-only information such as guides. Therefore, it's recommended to keep the source SVG around if you need to make further changes.

If you're contributing to the engine itself, you should make a pull request to add optimized icons to editor/icons in the main repository. Recompile the engine to make it pick up new icons for classes.

It's also possible to create custom icons within a module. If you're creating your own module and don't plan to integrate it with Godot, you don't need to make a separate pull request for your icons to be available within the editor as they can be self-contained.

For specific instructions on how to create module icons, refer to Creating custom module icons.

If icons don't appear in the editor, make sure that:

Each icon's filename matches the naming requirement as described previously.

modules/svg is enabled (it should be enabled by default). Without it, icons won't appear in the editor at all.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## GDScript grammar — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/file_formats/gdscript_grammar.html

**Contents:**
- GDScript grammar
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

This is the formal grammar of GDScript written in EBNF, for reference purposes.

This grammar is descriptive only, derived from the reference documentation and current implementation. The GDScript parser is not generated from a grammar definition. Inconsistencies here likely mean an error in this grammar, not a bug in GDScript.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Getting the source — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/getting_source.html

**Contents:**
- Getting the source
- Downloading the Godot source code
- User-contributed notes

Before getting into the SCons build system and compiling Godot, you need to actually download the Godot source code.

The source code is available on GitHub and while you can manually download it via the website, in general you want to do it via the git version control system.

If you are compiling in order to make contributions or pull requests, you should follow the instructions from the Pull Request workflow.

If you don't know much about git yet, there are a great number of tutorials available on various websites.

In general, you need to install git and/or one of the various GUI clients.

Afterwards, to get the latest development version of the Godot source code (the unstable master branch), you can use git clone.

If you are using the git command line client, this is done by entering the following in a terminal:

For any stable release, visit the release page and click on the link for the release you want. You can then download and extract the source from the download link on the page.

With git, you can also clone a stable release by specifying its branch or tag after the --branch (or just -b) argument:

The maintenance branches are used to release further patches on each minor version.

You can get the source code for each release and pre-release in .tar.xz format from godotengine/godot-builds on GitHub. This lacks version control information but has a slightly smaller download size.

After downloading the Godot source code, you can continue to compiling Godot.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Godot's architecture diagram — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/godot_architecture_diagram.html

**Contents:**
- Godot's architecture diagram
- User-contributed notes

The following diagram describes the architecture used by Godot, from the core components down to the abstracted drivers, via the scene structure and the servers.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Handling compatibility breakages — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/handling_compatibility_breakages.html

**Contents:**
- Handling compatibility breakages
- A practical example
- User-contributed notes

So you've added a new parameter to a method, changed the return type, changed the type of a parameter, or changed its default value, and now the automated testing is complaining about compatibility breakages?

Breaking compatibility should be avoided, but when necessary there are systems in place to handle this in a way that makes the transition as smooth as possible.

These changes are taken from pull request #88047, which added new pathing options to AStarGrid2D and other AStar classes. Among other changes, these methods were modified in core/math/a_star_grid_2d.h:

This meant adding new compatibility method bindings to the file, which should be in the protected section of the code, usually placed next to _bind_methods():

They should start with an _ to indicate that they are internal, and end with _bind_compat_ followed by the PR number that introduced the change (88047 in this example). These compatibility methods need to be implemented in a dedicated file, like core/math/a_star_grid_2d.compat.inc in this case:

Unless the change in compatibility is complex, the compatibility method should call the modified method directly, instead of duplicating that method. Make sure to match the default arguments for that method (in the example above this would be false).

This file should always be placed next to the original file, and have .compat.inc at the end instead of .cpp or .h. Next, this should be included in the .cpp file we're adding compatibility methods to, so core/math/a_star_grid_2d.cpp:

And finally, the changes reported by the API validation step should be added to the relevant validation file. Because this was done during the development of 4.3, this would be misc/extension_api_validation/4.2-stable.expected (including changes not shown in this example):

The instructions for how to add to that file are at the top of the file itself.

If you get a "Hash changed" error for a method, it means that the compatibility binding is missing or incorrect. Such lines shouldn't be added to the .expected file, but fixed by binding the proper compatibility method.

And that's it! You might run into a bit more complicated cases, like rearranging arguments, changing return types, etc., but this covers the basic on how to use this system.

For more information, see pull request #76446.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Inheritance class tree — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/inheritance_class_tree.html

**Contents:**
- Inheritance class tree
- Object
- Reference
- Control
- Node2D
- Node3D
- User-contributed notes

Source files: class_tree.zip.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Internal rendering architecture — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/internal_rendering_architecture.html

**Contents:**
- Internal rendering architecture
- Rendering methods
  - Forward+
  - Mobile
  - Compatibility
  - Why not deferred rendering?
- Rendering drivers
  - Vulkan
  - Direct3D 12
  - Metal

This page is a high-level overview of Godot 4's internal renderer design. It does not apply to previous Godot versions.

The goal of this page is to document design decisions taken to best suit Godot's design philosophy, while providing a starting point for new rendering contributors.

If you have questions about rendering internals not answered here, feel free to ask in the #rendering channel of the Godot Contributors Chat.

If you have difficulty understanding concepts on this page, it is recommended to go through an OpenGL tutorial such as LearnOpenGL.

Modern low-level APIs (Vulkan/Direct3D 12/Metal) require intermediate knowledge of higher-level APIs (OpenGL/Direct3D 11) to be used effectively. Thankfully, contributors rarely need to work directly with low-level APIs. Godot's renderers are built entirely on OpenGL and RenderingDevice, which is our abstraction over Vulkan/Direct3D 12/Metal.

This is a forward renderer that uses a clustered approach to lighting.

Clustered lighting uses a compute shader to group lights into a 3D frustum aligned grid. Then, at render time, pixels can lookup what lights affect the grid cell they are in and only run light calculations for lights that might affect that pixel.

This approach can greatly speed up rendering performance on desktop hardware, but is substantially less efficient on mobile.

This is a forward renderer that uses a traditional single-pass approach to lighting. Internally, it is called Forward Mobile.

Intended for mobile platforms, but can also run on desktop platforms. This rendering method is optimized to perform well on mobile GPUs. Mobile GPUs have a very different architecture compared to desktop GPUs due to their unique constraints around battery usage, heat, and overall bandwidth limitations of reading and writing data. Compute shaders also have very limited support or aren't supported at all. As a result, the mobile renderer purely uses raster-based shaders (fragment/vertex).

Unlike desktop GPUs, mobile GPUs perform tile-based rendering. Instead of rendering the whole image as a single unit, the image is divided in smaller tiles that fit within the faster internal memory of the mobile GPU. Each tile is rendered and then written out to the destination texture. This all happens automatically on the graphics driver.

The problem is that this introduces bottlenecks in our traditional approach. For desktop rendering, we render all opaque geometry, then handle the background, then transparent geometry, then post-processing. Each pass will need to read the current result into tile memory, perform its operations and then write it out again. We then wait for all tiles to be completed before moving on to the next pass.

The first important change in the mobile renderer is that the mobile renderer does not use the RGBA16F texture formats that the desktop renderer does. Instead, it is using an R10G10B10A2 UNORM texture format. This halves the bandwidth required and has further improvements as mobile hardware often further optimizes for 32-bit formats. The tradeoff is that the mobile renderer has limited HDR capabilities due to the reduced precision and maximum values in the color data.

The second important change is the use of sub-passes whenever possible. Sub-passes allows us to perform the rendering steps end-to-end per tile saving on the overhead introduced by reading from and writing to the tiles between each rendering pass. The ability to use sub-passes is limited by the inability to read neighboring pixels, as we're constrained to working within a single tile.

This limitation of subpasses results in not being able to implement features such as glow and depth of field efficiently. Similarly, if there is a requirement to read from the screen texture or depth texture, we must fully write out the rendering result limiting our ability to use sub-passes. When such features are enabled, a mix of sub-passes and normal passes are used, and these features result in a notable performance penalty.

On desktop platforms, the use of sub-passes won't have any impact on performance. However, this rendering method can still perform better than Forward+ in simple scenes thanks to its lower complexity and lower bandwidth usage. This is especially noticeable on low-end GPUs, integrated graphics or in VR applications.

Given its low-end focus, this rendering method does not provide high-end rendering features such as SDFGI and Volumetric fog and fog volumes. Several post-processing effects are also not available.

This is the only rendering method available when using the OpenGL driver. This rendering method is not available when using Vulkan, Direct3D 12, or Metal.

This is a traditional (non-clustered) forward renderer. Internally, it is called GL Compatibility. It's intended for old GPUs that don't have Vulkan support, but still works very efficiently on newer hardware. Specifically, it is optimized for older and lower-end mobile devices. However, many optimizations carry over making it a good choice for older and lower-end desktop as well.

Like the Mobile renderer, the Compatibility renderer uses an R10G10B10A2 UNORM texture for 3D rendering. Unlike the mobile renderer, colors are tonemapped and stored in sRGB format so there is no HDR support. This avoids the need for a tonemapping pass and allows us to use the lower bit texture without substantial banding.

The Compatibility renderer uses a traditional forward single-pass approach to drawing objects with lights, but it uses a multi-pass approach to draw lights with shadows. Specifically, in the first pass, it can draw multiple lights without shadows and up to one DirectionalLight3D with shadows. In each subsequent pass, it can draw up to one OmniLight3D, one SpotLight3D and one DirectionalLight3D with shadows. Lights with shadows will affect the scene differently than lights without shadows, as the lighting is blended in sRGB space instead of linear space. This difference in lighting will impact how the scene looks and needs to be kept in mind when designing scenes for the Compatibility renderer.

Given its low-end focus, this rendering method does not provide high-end rendering features (even less so compared to Mobile). Most post-processing effects are not available.

Forward rendering generally provides a better tradeoff for performance versus flexibility, especially when a clustered approach to lighting is used. While deferred rendering can be faster in some cases, it's also less flexible and requires using hacks to be able to use MSAA. Since games with a less realistic art style can benefit a lot from MSAA, we chose to go with forward rendering for Godot 4 (like Godot 3).

That said, parts of the forward renderer are performed with a deferred approach to allow for some optimizations when possible. This applies to VoxelGI and SDFGI in particular.

A clustered deferred renderer may be developed in the future. This renderer could be used in situations where performance is favored over flexibility.

Godot 4 supports the following graphics APIs:

This is the main driver in Godot 4, with most of the development focus going towards this driver.

Vulkan 1.0 is required as a baseline, with optional Vulkan 1.1 and 1.2 features used when available. volk is used as a Vulkan loader, and Vulkan Memory Allocator is used for memory management.

Both the Forward+ and Mobile Rendering methods are supported when using the Vulkan driver.

Vulkan context creation:

drivers/vulkan/vulkan_context.cpp

Direct3D 12 context creation:

drivers/d3d12/d3d12_context.cpp

Like Vulkan, the Direct3D 12 driver targets modern platforms only. It is designed to target both Windows and Xbox (whereas Vulkan can't be used directly on Xbox).

Both the Forward+ and Mobile Rendering methods can be used with Direct3D 12.

Core shaders are shared with the Vulkan renderer. Shaders are transpiled from SPIR-V to DXIL using Mesa NIR (more information).

This driver is still experimental and only available in Godot 4.3 and later. While Direct3D 12 allows supporting Direct3D-exclusive features on Windows 11 such as windowed optimizations and Auto HDR, Vulkan is still recommended for most projects. See the pull request that introduced Direct3D 12 support for more information.

Godot provides a native Metal driver that works on all Apple Silicon hardware (macOS ARM). Compared to using the MoltenVK translation layer, this is significantly faster, particularly in CPU-bound scenarios.

Both the Forward+ and Mobile Rendering methods can be used with Metal.

Core shaders are shared with the Vulkan renderer. Shaders are transpiled from GLSL to MSL using SPIRV-Cross.

Godot also supports Metal rendering via MoltenVK, which is used as a fallback when native Metal support is not available (e.g. on x86 macOS).

This driver is still experimental and only available in Godot 4.4 and later. See the pull request that introduced Metal support for more information.

This driver uses OpenGL ES 3.0 and targets legacy and low-end devices that don't support Vulkan. OpenGL 3.3 Core Profile is used on desktop platforms to run this driver, as most graphics drivers on desktop don't support OpenGL ES. WebGL 2.0 is used for web exports.

It is possible to use OpenGL ES 3.0 directly on desktop platforms by passing the --rendering-driver opengl3_es command line argument, although this will only work on graphics drivers that feature native OpenGL ES support (such as Mesa).

Only the Compatibility rendering method can be used with the OpenGL driver.

Core shaders are entirely different from the Vulkan renderer.

Many advanced features are not supported with this driver, as it targets low-end devices first and foremost.

The following rendering API + rendering method combinations are currently possible:

Vulkan + Forward+ (optionally through MoltenVK on macOS and iOS)

Vulkan + Mobile (optionally through MoltenVK on macOS and iOS)

Direct3D 12 + Forward+

OpenGL + Compatibility (optionally through ANGLE on Windows and macOS)

Each combination has its own limitations and performance characteristics. Make sure to test your changes on all rendering methods if possible before opening a pull request.

The OpenGL driver does not use the RenderingDevice abstraction.

To make the complexity of modern low-level graphics APIs more manageable, Godot uses its own abstraction called RenderingDevice.

This means that when writing code for modern rendering methods, you don't actually use the Vulkan, Direct3D 12, or Metal APIs directly. While this is still lower-level than an API like OpenGL, this makes working on the renderer easier, as RenderingDevice will abstract many API-specific quirks for you. The RenderingDevice presents a similar level of abstraction as WebGPU.

Vulkan RenderingDevice implementation:

drivers/vulkan/rendering_device_driver_vulkan.cpp

Direct3D 12 RenderingDevice implementation:

drivers/d3d12/rendering_device_driver_d3d12.cpp

Metal RenderingDevice implementation:

drivers/metal/rendering_device_driver_metal.mm

This diagram represents the structure of rendering classes in Godot, including the RenderingDevice abstraction:

While shaders in Godot projects are written using a custom language inspired by GLSL, core shaders are written directly in GLSL.

These core shaders are embedded in the editor and export template binaries at compile-time. To see any changes you've made to those GLSL shaders, you need to recompile the editor or export template binary.

Some material features such as height mapping, refraction and proximity fade are not part of core shaders, and are performed in the default BaseMaterial3D using the Godot shader language instead (not GLSL). This is done by procedurally generating the required shader code depending on the features enabled in the material.

By convention, shader files with _inc in their name are included in other GLSL files for better code reuse. Standard GLSL preprocessing is used to achieve this.

Core material shaders will be used by every material in the scene – both with the default BaseMaterial3D and custom shaders. As a result, these shaders must be kept as simple as possible to avoid performance issues and ensure shader compilation doesn't become too slow.

If you use if branching in a shader, performance may decrease as VGPR usage will increase in the shader. This happens even if all pixels evaluate to true or false in a given frame.

If you use #if preprocessor branching, the number of required shader versions will increase in the scene. In a worst-case scenario, adding a single boolean #define can double the number of shader versions that may need to be compiled in a given scene. In some cases, Vulkan specialization constants can be used as a faster (but more limited) alternative.

This means there is a high barrier to adding new built-in material features in Godot, both in the core shaders and BaseMaterial3D. While BaseMaterial3D can make use of dynamic code generation to only include the shader code if the feature is enabled, it'll still require generating more shader versions when these features are used in a project. This can make shader compilation stutter more noticeable in complex 3D scenes.

See The Shader Permutation Problem and Branching on a GPU blog posts for more information.

Core GLSL material shaders:

Forward+: servers/rendering/renderer_rd/shaders/forward_clustered/scene_forward_clustered.glsl

Mobile: servers/rendering/renderer_rd/shaders/forward_mobile/scene_forward_mobile.glsl

Compatibility: drivers/gles3/shaders/scene.glsl

Material shader generation:

scene/resources/material.cpp

Other GLSL shaders for Forward+ and Mobile rendering methods:

servers/rendering/renderer_rd/shaders/

modules/lightmapper_rd/

Other GLSL shaders for the Compatibility rendering method:

drivers/gles3/shaders/

The following is only applicable in the Forward+ and Mobile rendering methods, not in Compatibility. Multiple Viewports can be used to emulate this when using the Compatibility renderer, or to perform 2D resolution scaling.

2D and 3D are rendered to separate buffers, as 2D rendering in Godot is performed in LDR sRGB-space while 3D rendering uses HDR linear space.

The color format used for 2D rendering is RGB8 (RGBA8 if the Transparent property on the Viewport is enabled). 3D rendering uses a 24-bit unsigned normalized integer depth buffer, or 32-bit signed floating-point if a 24-bit depth buffer is not supported by the hardware. 2D rendering does not use a depth buffer.

3D resolution scaling is performed differently depending on whether bilinear or FSR 1.0 scaling is used. When bilinear scaling is used, no special upscaling shader is run. Instead, the viewport's texture is stretched and displayed with a linear sampler (which makes the filtering happen directly on the hardware). This allows maximizing the performance of bilinear 3D scaling.

The configure() function in RenderSceneBuffersRD reallocates the 2D/3D buffers when the resolution or scaling changes.

Dynamic resolution scaling isn't supported yet, but is planned in a future Godot release.

2D and 3D rendering buffer configuration C++ code:

servers/rendering/renderer_rd/storage_rd/render_scene_buffers_rd.cpp

servers/rendering/renderer_rd/effects/fsr.cpp

2D light rendering is performed in a single pass to allow for better performance with large amounts of lights.

All rendering methods feature 2D batching to improve performance, which is especially noticeable with lots of text on screen.

MSAA can be enabled in 2D to provide "automatic" line and polygon antialiasing, but FXAA does not affect 2D rendering as it's calculated before 2D rendering begins. Godot's 2D drawing methods such as the Line2D node or some CanvasItem draw_*() methods provide their own way of antialiasing based on triangle strips and vertex colors, which don't require MSAA to work.

A 2D signed distance field representing LightOccluder2D nodes in the viewport is automatically generated if a user shader requests it. This can be used for various effects in custom shaders, such as 2D global illumination. It is also used to calculate particle collisions in 2D.

2D SDF generation GLSL shader:

servers/rendering/renderer_rd/shaders/canvas_sdf.glsl

In the Forward+ renderer, Vulkan instancing is used to group rendering of identical opaque or alpha-tested objects for performance. (Alpha-blended objects are never instanced.) This is not as fast as static mesh merging, but it still allows instances to be culled individually.

Decal rendering is currently not available in the Compatibility renderer.

The Forward+ renderer uses clustered lighting. This allows using as many lights as you want; performance largely depends on screen coverage. Shadow-less lights can be almost free if they don't occupy much space on screen.

All rendering methods also support rendering up to 8 directional lights at the same time (albeit with lower shadow quality when more than one light has shadows enabled).

The Mobile renderer uses a single-pass lighting approach, with a limitation of 8 OmniLights + 8 SpotLights affecting each Mesh resource (plus a limitation of 256 OmniLights + 256 SpotLights in the camera view). These limits are hardcoded and can't be adjusted in the project settings.

The Compatibility renderer uses a hybrid single-pass + multi-pass lighting approach. Lights without shadows are rendered in a single pass. Lights with shadows are rendered in multiple passes. This is required for performance reasons on mobile devices. As a result, performance does not scale well with many shadow-casting lights. It is recommended to only have a handful of lights with shadows in the camera frustum at a time and for those lights to be spread apart so that each object is only touched by 1 or 2 shadowed lights at a time. The maximum number of lights visible at once can be adjusted in the project settings.

In all 3 methods, lights without shadows are much cheaper than lights with shadows. To improve performance, lights are only updated when the light is modified or when objects in its radius are modified. Godot currently doesn't separate static shadow rendering from dynamic shadow rendering, but this is planned in a future release.

Clustering is also used for reflection probes and decal rendering in the Forward+ renderer.

Both Forward+ and Mobile methods use PCF to filter shadow maps and create a soft penumbra. Instead of using a fixed PCF pattern, these methods use a vogel disk pattern which allows for changing the number of samples and smoothly changing the quality.

Godot also supports percentage-closer soft shadows (PCSS) for more realistic shadow penumbra rendering. PCSS shadows are limited to the Forward+ renderer as they're too demanding to be usable in the Mobile renderer. PCSS also uses a vogel-disk shaped kernel.

Additionally, both shadow-mapping techniques rotate the kernel on a per-pixel basis to help soften under-sampling artifacts.

The Compatibility renderer supports shadow mapping for DirectionalLight3D, OmniLight3D, and SpotLight3D lights.

Only available in the Forward+ renderer, not the Mobile or Compatibility renderers.

Godot uses a custom TAA implementation based on the old TAA implementation from Spartan Engine.

Temporal antialiasing requires motion vectors to work. If motion vectors are not correctly generated, ghosting will occur when the camera or objects move.

Motion vectors are generated on the GPU in the main material shader. This is done by running the vertex shader corresponding to the previous rendered frame (with the previous camera transform) in addition to the vertex shader for the current rendered frame, then storing the difference between them in a color buffer.

Alternatively, FSR 2.2 can be used as an upscaling solution that also provides its own temporal antialiasing algorithm. FSR 2.2 is implemented on top of the RenderingDevice abstraction as opposed to using AMD's reference code directly.

servers/rendering/renderer_rd/shaders/effects/taa_resolve.glsl

servers/rendering/renderer_rd/effects/fsr2.cpp

servers/rendering/renderer_rd/shaders/effects/fsr2/

VoxelGI and SDFGI are only available in the Forward+ renderer, not the Mobile or Compatibility renderers.

LightmapGI baking is only available in the Forward+ and Mobile renderers, and can only be performed within the editor (not in an exported project). LightmapGI rendering is supported by the Compatibility renderer.

Godot supports voxel-based GI (VoxelGI), signed distance field GI (SDFGI) and lightmap baking and rendering (LightmapGI). These techniques can be used simultaneously if desired.

Lightmap baking happens on the GPU using Vulkan compute shaders. The GPU-based lightmapper is implemented in the LightmapperRD class, which inherits from the Lightmapper class. This allows for implementing additional lightmappers, paving the way for a future port of the CPU-based lightmapper present in Godot 3.x. This would allow baking lightmaps while using the Compatibility renderer.

servers/rendering/renderer_rd/environment/gi.cpp

scene/3d/voxel_gi.cpp - VoxelGI node

editor/plugins/voxel_gi_editor_plugin.cpp - Editor UI for the VoxelGI node

Core GI GLSL shaders:

servers/rendering/renderer_rd/shaders/environment/voxel_gi.glsl

servers/rendering/renderer_rd/shaders/environment/voxel_gi_debug.glsl - VoxelGI debug draw mode

servers/rendering/renderer_rd/shaders/environment/sdfgi_debug.glsl - SDFGI Cascades debug draw mode

servers/rendering/renderer_rd/shaders/environment/sdfgi_debug_probes.glsl - SDFGI Probes debug draw mode

servers/rendering/renderer_rd/shaders/environment/sdfgi_integrate.glsl

servers/rendering/renderer_rd/shaders/environment/sdfgi_preprocess.glsl

servers/rendering/renderer_rd/shaders/environment/sdfgi_direct_light.glsl

Lightmapper C++ code:

scene/3d/lightmap_gi.cpp - LightmapGI node

editor/plugins/lightmap_gi_editor_plugin.cpp - Editor UI for the LightmapGI node

scene/3d/lightmapper.cpp - Abstract class

modules/lightmapper_rd/lightmapper_rd.cpp - GPU-based lightmapper implementation

Lightmapper GLSL shaders:

modules/lightmapper_rd/lm_raster.glsl

modules/lightmapper_rd/lm_compute.glsl

modules/lightmapper_rd/lm_blendseams.glsl

Only available in the Forward+ and Mobile renderers, not the Compatibility renderer.

The Forward+ and Mobile renderers use different approaches to DOF rendering, with different visual results. This is done to best match the performance characteristics of the target hardware. In Forward+, DOF is performed using a compute shader. In Mobile, DOF is performed using a fragment shader (raster).

Box, hexagon and circle bokeh shapes are available (from fastest to slowest). Depth of field can optionally be jittered every frame to improve its appearance when temporal antialiasing is enabled.

Depth of field C++ code:

servers/rendering/renderer_rd/effects/bokeh_dof.cpp

Depth of field GLSL shader (compute - used for Forward+):

servers/rendering/renderer_rd/shaders/effects/bokeh_dof.glsl

Depth of field GLSL shader (raster - used for Mobile):

servers/rendering/renderer_rd/shaders/effects/bokeh_dof_raster.glsl

Only available in the Forward+ renderer, not the Mobile or Compatibility renderers.

The Forward+ renderer supports screen-space ambient occlusion, screen-space indirect lighting, screen-space reflections and subsurface scattering.

SSAO uses an implementation derived from Intel's ASSAO (converted to Vulkan). SSIL is derived from SSAO to provide high-performance indirect lighting.

When both SSAO and SSIL are enabled, parts of SSAO and SSIL are shared to reduce the performance impact.

SSAO and SSIL are performed at half resolution by default to improve performance. SSR is always performed at half resolution to improve performance.

Screen-space effects C++ code:

servers/rendering/renderer_rd/effects/ss_effects.cpp

Screen-space ambient occlusion GLSL shader:

servers/rendering/renderer_rd/shaders/effects/ssao.glsl

servers/rendering/renderer_rd/shaders/effects/ssao_blur.glsl

servers/rendering/renderer_rd/shaders/effects/ssao_interleave.glsl

servers/rendering/renderer_rd/shaders/effects/ssao_importance_map.glsl

Screen-space indirect lighting GLSL shader:

servers/rendering/renderer_rd/shaders/effects/ssil.glsl

servers/rendering/renderer_rd/shaders/effects/ssil_blur.glsl

servers/rendering/renderer_rd/shaders/effects/ssil_interleave.glsl

servers/rendering/renderer_rd/shaders/effects/ssil_importance_map.glsl

Screen-space reflections GLSL shader:

servers/rendering/renderer_rd/shaders/effects/screen_space_reflection.glsl

servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_scale.glsl

servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_filter.glsl

Subsurface scattering GLSL:

servers/rendering/renderer_rd/shaders/effects/subsurface_scattering.glsl

Godot supports using shaders to render the sky background. The radiance map (which is used to provide ambient light and reflections for PBR materials) is automatically updated based on the sky shader.

The SkyMaterial resources such as ProceduralSkyMaterial, PhysicalSkyMaterial and PanoramaSkyMaterial generate a built-in shader for sky rendering. This is similar to what BaseMaterial3D provides for 3D scene materials.

A detailed technical implementation can be found in the Custom sky shaders in Godot 4.0 article.

Sky rendering C++ code:

servers/rendering/renderer_rd/environment/sky.cpp - Sky rendering

scene/resources/sky.cpp - Sky resource (not to be confused with sky rendering)

scene/resources/sky_material.cpp SkyMaterial resources (used in the Sky resource)

Sky rendering GLSL shader:

Only available in the Forward+ renderer, not the Mobile or Compatibility renderers.

Godot supports a frustum-aligned voxel (froxel) approach to volumetric fog rendering. As opposed to a post-processing filter, this approach is more general-purpose as it can work with any light type. Fog can also use shaders for custom behavior, which allows animating the fog or using a 3D texture to represent density.

The FogMaterial resource generates a built-in shader for FogVolume nodes. This is similar to what BaseMaterial3D provides for 3D scene materials.

A detailed technical explanation can be found in the Fog Volumes arrive in Godot 4.0 article.

Volumetric fog C++ code:

servers/rendering/renderer_rd/environment/fog.cpp - General volumetric fog

scene/3d/fog_volume.cpp - FogVolume node

scene/resources/fog_material.cpp - FogMaterial resource (used by FogVolume)

Volumetric fog GLSL shaders:

servers/rendering/renderer_rd/shaders/environment/volumetric_fog.glsl

servers/rendering/renderer_rd/shaders/environment/volumetric_fog_process.glsl

While modern GPUs can handle drawing a lot of triangles, the number of draw calls in complex scenes can still be a bottleneck (even with Vulkan, Direct3D 12, and Metal).

Godot 4 supports occlusion culling to reduce overdraw (when the depth prepass is disabled) and reduce vertex throughput. This is done by rasterizing a low-resolution buffer on the CPU using Embree. The buffer's resolution depends on the number of CPU threads on the system, as this is done in parallel. This buffer includes occluder shapes that were baked in the editor or created at runtime.

As complex occluders can introduce a lot of strain on the CPU, baked occluders can be simplified automatically when generated in the editor.

Godot's occlusion culling doesn't support dynamic occluders yet, but OccluderInstance3D nodes can still have their visibility toggled or be moved. However, this will be slow when updating complex occluders this way. Therefore, updating occluders at runtime is best done only on simple occluder shapes such as quads or cuboids.

This CPU-based approach has a few advantages over other solutions, such as portals and rooms or a GPU-based culling solution:

No manual setup required (but can be tweaked manually for best performance).

No frame delay, which is problematic in cutscenes during camera cuts or when the camera moves fast behind a wall.

Works the same on all rendering drivers and methods, with no unpredictable behavior depending on the driver or GPU hardware.

Occlusion culling is performed by registering occluder meshes, which is done using OccluderInstance3D nodes (which themselves use Occluder3D resources). RenderingServer then performs occlusion culling by calling Embree in RendererSceneOcclusionCull.

Occlusion culling C++ code:

scene/3d/occluder_instance_3d.cpp

servers/rendering/renderer_scene_occlusion_cull.cpp

Godot supports manually authored hierarchical level of detail (HLOD), with distances specified by the user in the inspector.

In RenderingSceneCull, the _scene_cull() and _render_scene() functions are where most of the LOD determination happens. Each viewport can render the same mesh with different LODs (to allow for split screen rendering to look correct).

Visibility range C++ code:

servers/rendering/renderer_scene_cull.cpp

The ImporterMesh class is used for the 3D mesh import workflow in the editor. Its generate_lods() function handles generating using the meshoptimizer library.

LOD mesh generation also generates shadow meshes at the same time. These are meshes that have their vertices welded regardless of smoothing and materials. This is used to improve shadow rendering performance by lowering the vertex throughput required to render shadows.

The RenderingSceneCull class's _render_scene() function determines which mesh LOD should be used when rendering. Each viewport can render the same mesh with different LODs (to allow for split screen rendering to look correct).

The mesh LOD is automatically chosen based on a screen coverage metric. This takes resolution and camera FOV changes into account without requiring user intervention. The threshold multiplier can be adjusted in the project settings.

To improve performance, shadow rendering and reflection probe rendering also choose their own mesh LOD thresholds (which can be different from the main scene rendering).

Mesh LOD generation on import C++ code:

scene/resources/importer_mesh.cpp

Mesh LOD determination C++ code:

servers/rendering/renderer_scene_cull.cpp

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Introduction to editor development — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/editor/introduction_to_editor_development.html

**Contents:**
- Introduction to editor development
- Technical choices
- Directory structure
- Editor dependencies in scene/ files
- Development tips
- User-contributed notes

On this page, you will learn:

The design decisions behind the Godot editor.

How to work efficiently on the Godot editor's C++ code.

This guide is aimed at current or future engine contributors. To create editor plugins in GDScript, see Making plugins instead.

If you are new to Godot, we recommended you to read Godot's design philosophy before continuing. Since the Godot editor is a Godot project written in C++, much of the engine's philosophy applies to the editor.

The Godot editor is drawn using Godot's renderer and UI system. It does not rely on a toolkit such as GTK or Qt. This is similar in spirit to software like Blender. While using toolkits makes it easier to achieve a "native" appearance, they are also quite heavy and their licensing is not compatible with Godot's.

The editor is fully written in C++. It can't contain any GDScript or C# code.

The editor's code is fully self-contained in the editor/ folder of the Godot source repository.

Some editor functionality is also implemented via modules. Some of these are only enabled in editor builds to decrease the binary size of export templates. See the modules/ folder in the Godot source repository.

Some important files in the editor are:

editor/editor_node.cpp: Main editor initialization file. Effectively the "main scene" of the editor.

editor/project_manager.cpp: Main Project Manager initialization file. Effectively the "main scene" of the Project Manager.

editor/plugins/canvas_item_editor_plugin.cpp: The 2D editor viewport and related functionality (toolbar at the top, editing modes, overlaid helpers/panels, …).

editor/plugins/node_3d_editor_plugin.cpp: The 3D editor viewport and related functionality (toolbar at the top, editing modes, overlaid panels, …).

editor/plugins/node_3d_editor_gizmos.cpp: Where the 3D editor gizmos are defined and drawn. This file doesn't have a 2D counterpart as 2D gizmos are drawn by the nodes themselves.

When working on an editor feature, you may have to modify files in Godot's GUI nodes, which you can find in the scene/ folder.

One rule to keep in mind is that you must not introduce new dependencies to editor/ includes in other folders such as scene/. This applies even if you use #ifdef TOOLS_ENABLED.

To make the codebase easier to follow and more self-contained, the allowed dependency order is:

editor/ -> scene/ -> servers/ -> core/

This means that files in editor/ can depend on includes from scene/, servers/, and core/. But, for example, while scene/ can depend on includes from servers/ and core/, it cannot depend on includes from editor/.

Currently, there are some dependencies to editor/ includes in scene/ files, but they are in the process of being removed.

To iterate quickly on the editor, we recommend to set up a test project and open it from the command line after compiling the editor. This way, you don't have to go through the Project Manager every time you start Godot.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Introduction to the buildsystem — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/introduction_to_the_buildsystem.html

**Contents:**
- Introduction to the buildsystem
- Using multi-threading
- Platform selection
- Resulting binary
- Target
- Development and production aliases
- Dev build
- Debugging symbols
- Optimization level
- Architecture

Godot is a primarily C++ project and it uses the SCons build system. We love SCons for how maintainable and easy to set up it makes our buildsystem. And thanks to that compiling Godot from source can be as simple as running:

This produces an editor build for your current platform, operating system, and architecture. You can change what gets built by specifying a target, a platform, and/or an architecture. For example, to build an export template used for running exported games, you can run:

If you plan to debug or develop the engine, then you might want to enable the dev_build option to enable dev-only debugging code:

Following sections in the article will explain these and other universal options in more detail. But before you can compile Godot, you need to install a few prerequisites. Please refer to the platform documentation to learn more:

Compiling for Android

Compiling for Linux, *BSD

Compiling for the Web

Compiling for Windows

These articles cover in great detail both how to setup your environment to compile Godot on a specific platform, and how to compile for that platform. Please feel free to go back and forth between them and this article to reference platform-specific and universal configuration options.

The build process may take a while, depending on how powerful your system is. By default, Godot's SCons setup is configured to use all CPU threads but one (to keep the system responsive during compilation). If the system has 4 CPU threads or fewer, it will use all threads by default.

If you want to adjust how many CPU threads SCons will use, use the -j<threads> parameter to specify how many threads will be used for the build.

Example for using 12 threads:

Godot's build system will begin by detecting the platforms it can build for. If not detected, the platform will simply not appear on the list of available platforms. The build requirements for each platform are described in the rest of this tutorial section.

SCons is invoked by just calling scons. If no platform is specified, SCons will detect the target platform automatically based on the host platform. It will then start building for the target platform right away.

To list the available target platforms, use scons platform=list:

To build for a platform (for example, linuxbsd), run with the platform= (or p= to make it short) argument:

The resulting binaries will be placed in the bin/ subdirectory, generally with this naming convention:

For the previous build attempt, the result would look like this:

This means that the binary is for Linux or *BSD (not both), is not optimized, has the whole editor compiled in, and is meant for 64 bits.

A Windows binary with the same configuration will look like this:

Copy that binary to any location you like, as it contains the Project Manager, editor and all means to execute the game. However, it lacks the data to export it to the different platforms. For that the export templates are needed (which can be either downloaded from godotengine.org, or you can build them yourself).

Aside from that, there are a few standard options that can be set in all build targets, and which will be explained below.

The target option controls if the editor is compiled and debug flags are used. Optimization levels (optimize) and whether each build contains debug symbols (debug_symbols) is controlled separately from the target. Each mode means:

target=editor: Build an editor binary (defines TOOLS_ENABLED and DEBUG_ENABLED)

target=template_debug: Build a debug export template (defines DEBUG_ENABLED)

target=template_release: Build a release export template

The editor is enabled by default in all PC targets (Linux, Windows, macOS), disabled for everything else. Disabling the editor produces a binary that can run projects but does not include the editor or the Project Manager.

The list of command line arguments available varies depending on the build type.

When creating builds for development (running debugging/profiling tools), you often have different goals compared to production builds (making binaries as fast and small as possible).

Godot provides two aliases for this purpose:

dev_mode=yes is an alias for verbose=yes warnings=extra werror=yes tests=yes. This enables warnings-as-errors behavior (similar to Godot's continuous integration setup) and also builds unit tests so you can run them locally.

production=yes is an alias for use_static_cpp=yes debug_symbols=no lto=auto. Statically linking libstdc++ allows for better binary portability when compiling for Linux. This alias also enables link-time optimization when compiling for Linux, Web and Windows with MinGW, but keeps LTO disabled when compiling for macOS, iOS or Windows with MSVC. This is because LTO on those platforms is very slow to link or has issues with the generated code.

You can manually override options from those aliases by specifying them on the same command line with different values. For example, you can use scons production=yes debug_symbols=yes to create production-optimized binaries with debugging symbols included.

dev_build should not be confused with dev_mode, which is an alias for several development-related options (see above).

When doing engine development the dev_build option can be used together with target to enable dev-specific code. dev_build defines DEV_ENABLED, disables optimization (-O0//0d), enables generating debug symbols, and does not define NDEBUG (so assert() works in thirdparty libraries).

This flag appends the .dev suffix (for development) to the generated binary name.

There are additional SCons options to enable sanitizers, which are tools you can enable at compile-time to better debug certain engine issues. See Using sanitizers for more information.

By default, debug_symbols=no is used, which means no debugging symbols are included in compiled binaries. Use debug_symbols=yes to include debug symbols within compiled binaries, which allows debuggers and profilers to work correctly. Debugging symbols are also required for Godot's crash stacktraces to display with references to source code files and lines.

The downside is that debugging symbols are large files (significantly larger than the binaries themselves). As a result, official binaries currently do not include debugging symbols. This means you need to compile Godot yourself to have access to debugging symbols.

When using debug_symbols=yes, you can also use separate_debug_symbols=yes to put debug information in a separate file with a .debug suffix. This allows distributing both files independently. Note that on Windows, when compiling with MSVC, debugging information is always written to a separate .pdb file regardless of separate_debug_symbols.

Use the strip <path/to/binary> command to remove debugging symbols from a binary you've already compiled.

Several compiler optimization levels can be chosen from:

optimize=speed_trace (default when targeting non-Web platforms): Favors execution speed at the cost of larger binary size. Optimizations may sometimes negatively impact debugger usage (stack traces may be less accurate. If this occurs to you, use optimize=debug instead.

optimize=speed: Favors even more execution speed, at the cost of even larger binary size compared to optimize=speed_trace. Even less friendly to debugging compared to optimize=debug, as this uses the most aggressive optimizations available.

optimize=size (default when targeting the Web platform): Favors small binaries at the cost of slower execution speed.

optimize=size_extra: Favors even smaller binaries, at the cost of even slower execution speed compared to optimize=size.

optimize=debug: Only enables optimizations that do not impact debugging in any way. This results in faster binaries than optimize=none, but slower binaries than optimize=speed_trace.

optimize=none: Do not perform any optimization. This provides the fastest build times, but the slowest execution times.

optimize=custom (advanced users only): Do not pass optimization arguments to the C/C++ compilers. You will have to pass arguments manually using the cflags, ccflags and cxxflags SCons options.

The arch option is meant to control the CPU or OS version intended to run the binaries. It is focused mostly on desktop platforms and ignored everywhere else.

Supported values for the arch option are auto, x86_32, x86_64, arm32, arm64, rv64, ppc32, ppc64 and wasm32.

This flag appends the value of arch to resulting binaries when relevant. The default value arch=auto detects the architecture that matches the host platform.

It's possible to compile modules residing outside of Godot's directory tree, along with the built-in modules.

A custom_modules build option can be passed to the command line before compiling. The option represents a comma-separated list of directory paths containing a collection of independent C++ modules that can be seen as C++ packages, just like the built-in modules/ directory.

For instance, it's possible to provide both relative, absolute, and user directory paths containing such modules:

If there's any custom module with the exact directory name as a built-in module, the engine will only compile the custom one. This logic can be used to override built-in module implementations.

Custom modules in C++

Sometimes, you may encounter an error due to generated files being present. You can remove them by using scons --clean <options>, where <options> is the list of build options you've used to build Godot previously.

Alternatively, you can use git clean -fixd which will clean build artifacts for all platforms and configurations. Beware, as this will remove all untracked and ignored files in the repository. Don't run this command if you have uncommitted work!

There are several other build options that you can use to configure the way Godot should be built (compiler, debug options, etc.) as well as the features to include/disable.

Check the output of scons --help for details about each option for the version you are willing to compile.

The default custom.py file can be created at the root of the Godot Engine source to initialize any SCons build options passed via the command line:

You can also disable some of the built-in modules before compiling, saving some time it takes to build the engine. See Optimizing a build for size page for more details.

You can use the online Godot build options generator to generate a custom.py file containing SCons options. You can then save this file and place it at the root of your Godot source directory.

Another custom file can be specified explicitly with the profile command line option, both overriding the default build configuration:

Build options set from the file can be overridden by the command line options.

It's also possible to override the options conditionally:

SCONSFLAGS is an environment variable which is used by the SCons to set the options automatically without having to supply them via the command line.

For instance, you may want to force a number of CPU threads with the aforementioned -j option for all future builds:

Regular builds tend to be bottlenecked by including large numbers of headers in each compilation translation unit. Primarily to speed up development (rather than for production builds), Godot offers a "single compilation unit" build (aka "Unity / Jumbo" build).

For the folders accelerated by this option, multiple .cpp files are compiled in each translation unit, so headers can be shared between multiple files, which can dramatically decrease build times.

To perform an SCU build, use the scu_build=yes SCons option.

When developing a Pull Request using SCU builds, be sure to make a regular build prior to submitting the PR. This is because SCU builds by nature include headers from earlier .cpp files in the translation unit, therefore won't catch all the includes you will need in a regular build. The CI will catch these errors, but it will usually be faster to catch them on a local build on your machine.

Official export templates are downloaded from the Godot Engine site: godotengine.org. However, you might want to build them yourself (in case you want newer ones, you are using custom modules, or simply don't trust your own shadow).

If you download the official export templates package and unzip it, you will notice that most files are optimized binaries or packages for each platform:

To create those yourself, follow the instructions detailed for each platform in this same tutorial section. Each platform explains how to create its own template.

The version.txt file should contain the corresponding Godot version identifier. This file is used to install export templates in a version-specific directory to avoid conflicts. For instance, if you are building export templates for Godot 3.1.1, version.txt should contain 3.1.1.stable on the first line (and nothing else). This version identifier is based on the major, minor, patch (if present) and status lines of the version.py file in the Godot Git repository.

If you are developing for multiple platforms, macOS is definitely the most convenient host platform for cross-compilation, since you can cross-compile for every target. Linux and Windows come in second place, but Linux has the advantage of being the easier platform to set this up.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## JetBrains Rider — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/configuring_an_ide/rider.html

**Contents:**
- JetBrains Rider
- Importing the project
- Compiling and debugging the project
- Debug visualizers
- Unit testing
- Profiling
- Known issues
- User-contributed notes

JetBrains Rider is a commercial JetBrains IDE for C++, C# and GDScript that uses the same solution system as Visual Studio.

This documentation is for contributing to the game engine, not for using JetBrains Rider as a C# or GDScript editor. To code C# or GDScript in an external editor, see the C# guide to configure an external editor.

If you already use Visual Studio as your main IDE, you can use the same solution file in Rider. Rider and Visual Studio use the same solution format, so you can switch between the two IDEs without rebuilding the solution file. Debug configurations need to be changed when going from one IDE to another.

If you are starting from the scratch, please follow instructions, specifically:

Install all the dependencies.

Figure out the scons command for compiling to target a specific platform.

Provide scons with additional arguments to request a solution file generation:

Add vsproj=yes dev_build=yes to the scons command

The vsproj parameter signals that you want Visual Studio solution generated. The dev_build parameter ensures the debug symbols are included, allowing to e.g. step through code using breakpoints.

Open the generated godot.sln in Rider.

Ensure that the appropriate Solution configuration is selected on the Rider toolbar. It affects resolve of the SDKs, code analysis, build, run, etc.

Rider comes with a built-in debugger that can be used to debug the Godot project. You can launch the debugger by pressing the Debug icon at the top of the screen, this only works for the Project Manager, if you want to debug the editor, you need to configure the debugger first.

Click on the Godot > Edit Configurations option at the top of the screen.

Ensure the following values for the C++ Project Run Configuration:

Exe Path : $(LocalDebuggerCommand)

Program Arguments: -e --path <path to the Godot project>

Working Directory: $(LocalDebuggerWorkingDirectory)

Before Launch has a value of "Build Project"

This will tell the executable to debug the specified project without opening the Project Manager. Use the root path to the project folder, not project.godot file path.

Finally click on "Apply" and "OK" to save the changes.

When you press the Debug icon at the top of the screen, JetBrains Rider will launch the Godot editor with the debugger attached.

Alternatively you can use Run > Attach to Process to attach the debugger to a running Godot instance.

You can find the Godot instance by searching for godot.editor and then clicking Attach with LLDB

Debug visualizers customize how complex data structures are displayed during debugging. For Windows "natvis" (short for "Native Visualization") built-in with Godot are automatically used. For other operating systems, similar functionality can be setup manually.

Please follow RIDER-123535.

Leverage Rider doctest support. Please refer to the instructions.

Please refer to the profiling instructions.

Please consult the JetBrains Rider documentation for any specific information about the JetBrains IDE.

Debugging Windows MinGV build - symbols are not loaded. Reported RIDER-106816.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## KDevelop — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/configuring_an_ide/kdevelop.html

**Contents:**
- KDevelop
- Importing the project
- Debugging the project
- User-contributed notes

KDevelop is a free, open source IDE for all desktop platforms.

From the KDevelop's main screen select Open Project.

KDevelop's main screen.

Navigate to the Godot root folder and select it.

On the next screen, choose Custom Build System for the Project Manager.

After the project has been imported, open the project configuration by right-clicking on it in the Projects panel and selecting Open Configuration.. option.

Under Language Support open the Includes/Imports tab and add the following paths:

Under Custom Build System add a new build configuration with the following settings:

See Introduction to the buildsystem for a full list of arguments.

Apply the changes and close the configuration window.

Select Run > Configure Launches... from the top menu.

Click Add to create a new launch configuration.

Select Executable option and specify the path to your executable located in the <Godot root directory>/bin folder. The name depends on your build configuration, e.g. godot.linuxbsd.editor.dev.x86_64 for 64-bit LinuxBSD platform with platform=linuxbsd, target=editor, and dev_build=yes.

If you run into any issues, ask for help in one of Godot's community channels.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Object class — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/object_class.html

**Contents:**
- Object class
- General definition
  - References:
- Registering an Object
  - References:
- Constants
- Properties (set/get)
- Binding properties using _set/_get/_get_property_list
- Dynamic casting
- Signals

This page describes the C++ implementation of objects in Godot. Looking for the Object class reference? Have a look here.

Object is the base class for almost everything. Most classes in Godot inherit directly or indirectly from it. Objects provide reflection and editable properties, and declaring them is a matter of using a single macro like this:

This adds a lot of functionality to Objects. For example:

ClassDB is a static class that holds the entire list of registered classes that inherit from Object, as well as dynamic bindings to all their methods properties and integer constants.

Classes are registered by calling:

Registering it will allow the class to be instanced by scripts, code, or creating them again when deserializing.

Registering as virtual is the same but it can't be instanced.

Object-derived classes can override the static function static void _bind_methods(). When one class is registered, this static function is called to register all the object methods, properties, constants, etc. It's only called once. If an Object derived class is instanced but has not been registered, it will be registered as virtual automatically.

Inside _bind_methods, there are a couple of things that can be done. Registering functions is one:

Default values for arguments can be passed as parameters at the end:

Default values must be provided in the same order as they are declared, skipping required arguments and then providing default values for the optional ones. This matches the syntax for declaring methods in C++.

D_METHOD is a macro that converts "methodname" to a StringName for more efficiency. Argument names are used for introspection, but when compiling on release, the macro ignores them, so the strings are unused and optimized away.

Check _bind_methods of Control or Object for more examples.

If just adding modules and functionality that is not expected to be documented as thoroughly, the D_METHOD() macro can safely be ignored and a string passing the name can be passed for brevity.

core/object/class_db.h

Classes often have enums such as:

For these to work when binding to methods, the enum must be declared convertible to int. A macro is provided to help with this:

The constants can also be bound inside _bind_methods, by using:

Objects export properties, properties are useful for the following:

Serializing and deserializing the object.

Creating a list of editable values for the Object derived class.

Properties are usually defined by the PropertyInfo() class and constructed as:

This is an integer property named "amount". The hint is a range, and the range goes from 0 to 49 in steps of 1 (integers). It is only usable for the editor (editing the value visually) but won't be serialized.

This is a string property, can take any string but the editor will only allow the defined hint ones. Since no usage flags were specified, the default ones are PROPERTY_USAGE_STORAGE and PROPERTY_USAGE_EDITOR.

There are plenty of hints and usage flags available in object.h, give them a check.

Properties can also work like C# properties and be accessed from script using indexing, but this usage is generally discouraged, as using functions is preferred for legibility. Many properties are also bound with categories, such as "animation/frame" which also make indexing impossible unless using operator [].

From _bind_methods(), properties can be created and bound as long as set/get functions exist. Example:

This creates the property using the setter and the getter.

An additional method of creating properties exists when more flexibility is desired (i.e. adding or removing properties on context).

The following functions can be overridden in an Object derived class, they are NOT virtual, DO NOT make them virtual, they are called for every override and the previous ones are not invalidated (multilevel call).

This is also a little less efficient since p_property must be compared against the desired names in serial order.

Godot provides dynamic casting between Object-derived classes, for example:

If cast fails, NULL is returned. This system uses RTTI, but it also works fine (although a bit slower) when RTTI is disabled. This is useful on platforms where a small binary size is ideal, such as HTML5 or consoles (with low memory footprint).

Objects can have a set of signals defined (similar to Delegates in other languages). This example shows how to connect to them:

The method _node_entered_tree must be registered to the class using ClassDB::bind_method (explained before).

Adding signals to a class is done in _bind_methods, using the ADD_SIGNAL macro, for example:

All objects in Godot have a _notification method that allows it to respond to engine level callbacks that may relate to it. More information can be found on the Godot notifications page.

RefCounted inherits from Object and holds a reference count. It is the base for reference counted object types. Declaring them must be done using Ref<> template. For example:

myref is reference counted. It will be freed when no more Ref<> templates point to it.

core/object/reference.h

Resource inherits from RefCounted, so all resources are reference counted. Resources can optionally contain a path, which reference a file on disk. This can be set with resource.set_path(path), though this is normally done by the resource loader. No two different resources can have the same path; attempting to do so will result in an error.

Resources without a path are fine too.

Resources can be loaded with the ResourceLoader API, like this:

If a reference to that resource has been loaded previously and is in memory, the resource loader will return that reference. This means that there can be only one resource loaded from a file referenced on disk at the same time.

resourceinteractiveloader (TODO)

core/io/resource_loader.h

Saving a resource can be done with the resource saver API:

The instance will be saved, and sub resources that have a path to a file will be saved as a reference to that resource. Sub resources without a path will be bundled with the saved resource and assigned sub-IDs, like res://someresource.res::1. This also helps to cache them when loaded.

core/io/resource_saver.h

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Optimizing a build for size — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/compiling/optimizing_for_size.html

**Contents:**
- Optimizing a build for size
- Rationale
- Stripping binaries
- Compiling with link-time optimization
- Optimizing for size instead of speed
- Detecting used features from the current project and disabling unused features
- Disabling advanced text server
- Disabling 3D
- Disabling advanced GUI objects
- Disabling physics engines

Sometimes, it is desired to optimize a build for size rather than speed. This means not compiling unused functions from the engine, as well as using specific compiler flags to aid on decreasing build size. Common situations include creating builds for mobile and Web platforms.

This tutorial aims to give an overview on different methods to create a smaller binary. Before continuing, it is recommended to read the previous tutorials on compiling Godot for each platform.

The options below are listed from the most important (greatest size savings) to the least important (lowest size savings).

Space savings: Very high

Performed in official builds: Yes

If you build Windows (MinGW), Linux or macOS binaries from source, remember to strip debug symbols from binaries by installing the strip package from your distribution then running:

On Windows, strip.exe is included in most MinGW toolchain setups.

This will reduce the size of compiled binaries by a factor between 5× and 10×. The downside is that crash backtraces will no longer provide accurate information (which is useful for troubleshooting the cause of a crash). C++ profilers will also no longer be able to display function names (this does not affect the built-in GDScript profiler).

The above command will not work on Windows binaries compiled with MSVC and platforms such as Android and Web. Instead, pass debug_symbols=no on the SCons command line when compiling.

Performed in official builds: Yes

Enabling link-time optimization produces more efficient binaries, both in terms of performance and file size. It works by eliminating duplicate template functions and unused code. It can currently be used with the GCC and MSVC compilers:

Linking becomes much slower and more RAM-consuming with this option, so it should be used only for release builds. You need to have at least 8 GB of RAM available for successful linking with LTO enabled. Since the operating system and programs will take up some RAM, in practice, you need 12 GB of RAM installed in your system (preferably 16 GB) to compile Godot with LTO enabled.

Performed in official builds: Yes, but only for web builds

Godot 3.1 onwards allows compiling using size optimizations (instead of speed). To enable this, set the optimize flag to size:

Some platforms such as WebAssembly already use this mode by default.

Godot 4.5 introduced the size_extra option, which can further reduce size.

Space savings: Moderate to high depending on project

Difficulty: Easy to medium depending on project

Performed in official builds: No

Godot features an Using the engine compilation configuration editor tool that can detect the features used in the current project and create a build profile. Once saved, this build profile can then be passed to SCons when compiling custom export templates:

Note that for certain projects, the feature detection may be too aggressive and disable features that are actually needed at runtime. This can occur if certain features are used in a way that their usage cannot be detected statically (such as a script being procedurally created and run at runtime).

More specific features can be disabled by following the sections below, but remember that many of them are automatically detected by the engine compilation configuration detector.

Performed in official builds: No

By default, Godot uses an advanced text server with the support for the following features:

Right-to-left typesetting and complex scripts, required to write languages such as Arabic and Hebrew.

Font ligatures and OpenType features (such as small capitals, fractions and slashed zero).

Godot provides a fallback text server that isn't compiled by default. This text server can be used as a lightweight alternative to the default advanced text server:

If you only intend on supporting Latin, Greek and Cyrillic-based languages in your project, the fallback text server should suffice.

This fallback text server can also process large amounts of text more quickly than the advanced text server. This makes the fallback text server a good fit for mobile/web projects.

Remember to always pass module_text_server_fb_enabled=yes when using module_text_server_adv_enabled=no. Otherwise, the compiled binary won't contain any text server, which means no text will be displayed at all when running the project.

Space savings: Moderate

Performed in official builds: No

For 2D games, having the whole 3D engine available usually makes no sense. Because of this, there is a build flag to disable it:

Tools must be disabled in order to use this flag, as the editor is not designed to operate without 3D support. Without it, the binary size can be reduced by about 15%.

Space savings: Moderate

Performed in official builds: No

Most small games don't require complex GUI controls such as Tree, ItemList, TextEdit or GraphEdit. They can be disabled using a build flag:

This is everything that will be disabled:

PopupMenu (will make all popup menus unavailable in code for classes that use them, like LineEdit, even though those classes are still available)

Space savings: Low to moderate

Performed in official builds: No

If your 3D project uses Jolt Physics, you can disable GodotPhysics3D at compile-time as it will never be used:

Inversely, if your 3D project uses GodotPhysics3D, you can disable Jolt Physics at compile-time:

If your project uses 3D rendering but not physics (or 2D rendering but not physics), you can also disable 2D or 3D physics entirely. Most 3D projects can take advantage of this, as they don't make use of 2D physics:

Space savings: Very low to moderate depending on modules

Difficulty: Medium to hard depending on modules

Performed in official builds: No

A lot of Godot's functions are offered as modules. You can see a list of modules with the following command:

The list of modules that can be disabled will appear, together with all build options. If you are working on a simple 2D game, you could disable a lot of them:

If this proves not to work for your use case, you should review the list of modules and see which ones you actually still need for your game (e.g. you might want to keep networking-related modules, regex support, minimp3/ogg/vorbis to play music, or theora to play videos).

Alternatively, you can supply a list of disabled modules by creating custom.py at the root of the source, with the contents similar to the following:

Overriding the build options.

This section is only relevant when distributing the files on a desktop platform that doesn't perform its own compression or packing. As such, this advice is relevant when you distribute ZIP archives on itch.io or GitHub Releases.

Platforms like Steam already apply their own compression scheme, so you don't need to create a ZIP archive to distribute files in the first place.

As an aside, you can look into optimizing the distribution of your project itself. This can be done even without recompiling the export template.

7-Zip can be used to create ZIP archives that are more efficient than usual, while remaining compatible with every ZIP extractor (including Windows' own built-in extractor). ZIP size reduction in a large project can reach dozens of megabytes compared to a typical ZIP compressor, although average savings are in the 1-5 MB range. Creating this ZIP archive will take longer than usual, but it will extract just as fast as any other ZIP archive.

When using the 7-Zip GUI, this is done by creating a ZIP archive with the Ultra compression mode. When using the command line, this is done using the following command:

Enabling gzip or Brotli compression for all file types from the web export (especially the .wasm and .pck) can reduce the download size significantly, leading to faster loading times, especially on slow connections.

Creating precompressed gzip or Brotli files with a high compression level can be even more efficient, as long as the web server is configured to serve those files when they exist. When supported, Brotli should be preferred over gzip as it has a greater potential for file size reduction.

See Serving the files for instructions.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Qt Creator — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/configuring_an_ide/qt_creator.html

**Contents:**
- Qt Creator
- Importing the project
- Debugging the project
- Code style configuration
- User-contributed notes

Qt Creator is a free, open source IDE for all desktop platforms.

From the Qt Creator's main screen select New Project > Import Project > Import Existing Project.

Under Location select the Godot root folder.

Next, you can choose which folders and files will be visible to the project. While C/C++ files are added automatically, other extensions can be potentially useful: *.glsl for shader files, *.py for buildsystem files, *.java for Android platform development, *.mm for macOS platform development.

You can change this configuration later by right-clicking on your project and selecting the Edit Files... option.

Open the project_name.includes file and add a line containing . to it to correctly enable the code completion.

From the left-side menu select Projects and open the Build tab.

Delete the predefined make build step.

Click Add Build Step > Custom Process Step to add a new build step with the following settings:

See Introduction to the buildsystem for a full list of arguments.

If the build fails with Could not start process "scons", it can mean that scons is not in your PATH environment variable. In this case, you'll have to specify the full path to the SCons binary.

From the left-side menu select Projects and open the Run tab.

Under Executable specify the path to your executable located in the <Godot root directory>/bin folder. The name depends on your build configuration, e.g. godot.linuxbsd.editor.dev.x86_64 for 64-bit LinuxBSD platform with platform=editor and dev_build=yes. You can use %{buildDir} to reference the project root, e.g: %{buildDir}/bin/godot.linuxbsd.editor.dev.x86_64.

If you want to run a specific project, specify its root folder under Working directory.

If you want to run the editor, add -e to the Command line arguments field.

To learn more about command line arguments, refer to the command line tutorial.

Developers must follow the project's code style and the IDE should help them follow it. By default, Qt Creator uses spaces for indentation which doesn't match the Godot code style guidelines. You can change this behavior by changing the Code Style in Tools > Options > C++.

Click on Edit to change the current settings, then click on Copy Built-in Code Style button to set a new code style. Set a name for it (e.g. Godot) and change the Tab policy to be Tabs Only.

If you run into any issues, ask for help in one of Godot's community channels.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## TSCN file format — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/file_formats/tscn.html

**Contents:**
- TSCN file format
- File structure
  - Entries inside the file
- The scene tree
  - NodePath
  - Skeleton3D
  - BoneAttachment3D
  - AnimationPlayer
- Resources
  - External resources

The TSCN (text scene) file format represents a single scene tree inside Godot. Unlike binary SCN files, TSCN files have the advantage of being mostly human-readable and easy for version control systems to manage.

The ESCN (exported scene) file format is identical to the TSCN file format, but is used to indicate to Godot that the file has been exported from another program and should not be edited by the user from within Godot. Unlike SCN and TSCN files, during import, ESCN files are compiled to binary SCN files stored inside the .godot/imported/ folder. This reduces the data size and speeds up loading, as binary formats are faster to load compared to text-based formats.

To make files more compact, properties equal to the default value are not stored in scene/resource files. It is possible to write them manually, but they will be discarded when saving the file.

For those looking for a complete description, the parsing is handled in the file resource_format_text.cpp in the ResourceFormatLoaderText class.

The scene and resource file formats have changed significantly in Godot 4, with the introduction of string-based UIDs to replace incremental integer IDs.

Mesh, skeleton and animation data is also stored differently compared to Godot 3. You can read about some of the changes in this article: Animation data rework for 4.0

Scenes and resources saved with Godot 4.x contain format=3 in their header, whereas Godot 3.x uses format=2 instead.

There are five main sections inside the TSCN file:

The file descriptor looks like [gd_scene load_steps=4 format=3 uid="uid://cecaux1sm7mo0"] and should be the first entry in the file. The load_steps parameter is equal to the total amount of resources (internal and external) plus one (for the file itself). If the file has no resources, load_steps is omitted. The engine will still load the file correctly if load_steps is incorrect, but this will affect loading bars and any other piece of code relying on that value.

uid is a unique string-based identifier representing the scene. This is used by the engine to track files that are moved around, even while the editor is closed. Scripts can also load UID-based resources using the uid:// path prefix to avoid relying on filesystem paths. This makes it possible to move around a file in the project, but still be able to load it in scripts without having to modify the script. Godot does not use external files to keep track of IDs, which means no central metadata storage location is required within the project. See this pull request for detailed information.

These sections should appear in order, but it can be hard to distinguish them. The only difference between them is the first element in the heading for all of the items in the section. For example, the heading of all external resources should start with [ext_resource ...].

A TSCN file may contain single-line comments starting with a semicolon (;). However, comments will be discarded when saving the file using the Godot editor. Whitespace within a TSCN file is not significant (except within strings), but extraneous whitespace will be discarded when saving the file.

A heading looks like [<resource_type> key1=value1 key2=value2 key3=value3 ...] where resource_type is one of:

Below every heading comes zero or more key = value pairs. The values can be complex datatypes such as Arrays, Transforms, Colors, and so on. For example, a Node3D looks like:

The scene tree is made up of… nodes! The heading of each node consists of its name, parent and (most of the time) a type. For example: [node name="PlayerCamera" type="Camera" parent="Player/Head"]

Other valid keywords include:

index (sets the order of appearance in the tree; if absent, inherited nodes will take precedence over plain ones)

The first node in the file, which is also the scene root, must not have a parent="Path/To/Node" entry in its heading. All scene files should have exactly one scene root. If it doesn't, Godot will fail to import the file. The parent path of other nodes should be absolute, but shouldn't contain the scene root's name. If the node is a direct child of the scene root, the path should be ".". Here is an example scene tree (but without any node content):

To make the file structure easier to grasp, you can save a file with any given node or resource and then inspect it yourself in an external editor. You can also make incremental changes in the Godot editor, and keep an external text editor open on the .tscn or .tres file with auto-reload enabled to see what changes.

Here is an example of a scene containing a RigidBody3D-based ball with collision, visuals (mesh + light) and a camera parented to the RigidBody3D:

A tree structure is not enough to represent the whole scene. Godot uses a NodePath(Path/To/Node) structure to refer to another node or attribute of the node anywhere in the scene tree. Paths are relative to the current node, with NodePath(".") pointing to the current node and NodePath("") pointing to no node at all.

For instance, MeshInstance3D uses NodePath() to point to its skeleton. Likewise, Animation tracks use NodePath() to point to node properties to animate.

NodePath can also point to a property using a :property_name suffix, and even point to a specific component for vector, transform and color types. This is used by Animation resources to point to specific properties to animate. For example, NodePath("MeshInstance3D:scale.x") points to the x component of the scale Vector3 property in MeshInstance3D.

For example, the skeleton property in the MeshInstance3D node called mesh points to its parent, Armature01:

The Skeleton3D node inherits the Node3D node, but may also have a list of bones described in key-value pairs in the format bones/<id>/<attribute> = value. The bone attributes consist of:

These attributes are all optional. For instance, a bone may only define position or rotation without defining the other properties.

Here's an example of a skeleton node with two bones:

The BoneAttachment3D node is an intermediate node to describe some node being parented to a single bone in a Skeleton node. The BoneAttachment has a bone_name = "name of bone" property, as well as a property for the matching bone index.

An example of a Marker3D node parented to a bone in Skeleton:

The AnimationPlayer node works with one or more animation libraries stored in AnimationLibrary resources. An animation library is a collection of individual Animation resources, whose structure is documented here.

This split between animations themselves and animation libraries was done in Godot 4, so that animations can be imported separately from 3D meshes, which is a common workflow in 3D animation software. See the original pull request for details.

If the library name is empty, then it acts acts the unique source of animations for this AnimationPlayer. This allows using <animation_name> directly to play animations from script. If you name the library, then you must play it as <library_name>/<animation_name>. This ensures backwards compatibility and keeps the existing workflow if you don't want to use multiple animation libraries.

Resources are components that make up the nodes. For example, a MeshInstance3D node will have an accompanying ArrayMesh resource. The ArrayMesh resource may be either internal or external to the TSCN file.

References to the resources are handled by unique string-based IDs in the resource's heading. This is different from the uid property, which each external resource also has (but subresources don't).

External resources and internal resources are referred to with ExtResource("id") and SubResource("id"), respectively. Because there have different methods to refer to internal and external resources, you can have the same ID for both an internal and external resource.

For example, to refer to the resource [ext_resource type="Material" uid="uid://c4cp0al3ljsjv" path="res://material.tres" id="1_7bt6s"], you would use ExtResource("1_7bt6s").

External resources are links to resources not contained within the TSCN file itself. An external resource consists of a path, a type, a UID (used to map its filesystem location to a unique identifier) and an ID (used to refer to the resource in the scene file).

Godot always generates absolute paths relative to the resource directory and thus prefixed with res://, but paths relative to the TSCN file's location are also valid.

Some example external resources are:

Like TSCN files, a TRES file may contain single-line comments starting with a semicolon (;). However, comments will be discarded when saving the resource using the Godot editor. Whitespace within a TRES file is not significant (except within strings), but extraneous whitespace will be discarded when saving the file.

A TSCN file can contain meshes, materials and other data. These are contained in the internal resources section of the file. The heading for an internal resource looks similar to those of external resources, except that it doesn't have a path. Internal resources also have key=value pairs under each heading. For example, a capsule collision shape looks like:

Some internal resources contain links to other internal resources (such as a mesh having a material). In this case, the referring resource must appear before the reference to it. This means that order matters in the file's internal resources section.

An ArrayMesh consists of several surfaces contained in the _surfaces array (notice the leading underscore). Each surface's data is stored in a dictionary with the following keys:

aabb: The computed axis-aligned bounding box for visibility.

attribute_data: Vertex attribute data, such as normals, tangents, vertex colors, UV1, UV2 and custom vertex data.

bone_aabbs: The axis-aligned bounding box of each bone for visibility.

format: The surface's buffer format.

index_count: The number of indices in the surface. This must match index_data's size.

index_data: The index data, which determines which vertices from vertex_data are drawn.

lods: Level of detail variations, stored as an array. Each LOD level represents two values in the array. The first value is the percentage of screen space the LOD level is most suited for (edge length); the second value is the list of indices that should be drawn for the given LOD level.

material: The material used when drawing the surface.

name: The surface's name. This can be used in scripts and is imported from 3D DCCs.

primitive: The surface's primitive type, matching the Mesh.PrimitiveType Godot enum. 0 = points, 1 = lines, 2 = line strip, 3 = triangles (most common), 4 = triangle strip.

skin_data: Bone weight data.

vertex_count: Number of vertices in the surface. This must match vertex_data's size.

vertex_data: The vertex position data.

Here's an example of an ArrayMesh saved to its own .tres file. Some fields were shortened with ... for brevity:

Each animation has the following properties:

length: The animation's length in seconds. Note that keyframes may be placed outside the [0; length] interval, but they may have no effect depending on the interpolation mode chosen.

loop_mode: 0 = no looping, 1 = wrap-around looping, 2 = clamped looping.

step: The step size to use when editing this animation in the editor. This is only used in the editor; it doesn't affect animation playback in any way.

Each track is described by a list of key-value pairs in the format tracks/<id>/<attribute>. Each track includes:

type: The track's type. This defines what kind of properties may be animated by this track, and how it'll be exposed to the user in the editor. Valid types are value (generic property track), position_3d, rotation_3d, scale_3d, blend_shape (optimized 3D animation tracks), method (method call tracks), bezier (Bezier curve tracks), audio (audio playback tracks), animation (tracks that play other animations).

imported: true if the track was created from an imported 3D scene, false if it was manually created by the user in the Godot editor or using a script.

enabled: true if the track is effective, false if it was disabled in the editor.

path: Path to the node property that will be affected by the track. The property is written after the node path with a : separator.

interp: The interpolation mode to use. 0 = nearest, 1 = linear, 2 = cubic, 3 = linear angle, 4 = cubic angle.

loop_wrap: true if the track is designed to wrap around when the animation is looping, false if the track clamps to the first/last keyframes.

keys: The animation track's values. This attribute's structure depends on the type.

Here is a scene containing an AnimationPlayer that scales down a cube over time using a generic property track. The AnimationLibrary workflow was not used, so the animation library has an empty name (but the animation is still given a scale_down name). Note that the RESET track was not created in this AnimationPlayer for brevity:

For generic property value tracks, keys is a dictionary containing 3 arrays with positions in times (PackedFloat32Array), easing values in transitions (PackedFloat32Array) and values in values (Array). There is an additional update property, which is an integer with the values 0 = continuous, 1 = discrete, 2 = capture.

Here is a second Animation resource that makes use of the 3D Position and 3D Rotation tracks. These tracks (in addition to the 3D Scale track) replace Transform tracks from Godot 3. They are optimized for fast playback and can optionally be compressed.

The downside of these optimized track types is that they can't use custom easing values. Instead, all keyframes use linear interpolation. That said, you can still opt for using nearest or cubic interpolation for all keyframes in a given track by changing the track's interpolation mode.

For 3D position, rotation and scale tracks, keys is a PackedFloat32Array with all values stored in a sequence.

In the visual guide below, T is the keyframe's time in seconds since the start of the animation, E is the keyframe's transition (currently always 1). For 3D position and scale tracks, X, Y, Z are the Vector3's coordinates. For 3D rotation tracks, X, Y, Z and W are the Quaternion's coordinates.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Unit testing — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/unit_testing.html

**Contents:**
- Unit testing
- Platform and target support
- Running tests
  - Filtering tests
- Writing tests
  - Subcases
  - Assertions
  - Logging
  - Testing failure paths
  - Special tags in test case names

Godot Engine allows to write unit tests directly in C++. The engine integrates the doctest unit testing framework which gives ability to write test suites and test cases next to production code, but since the tests in Godot go through a different main entry point, the tests reside in a dedicated tests/ directory instead, which is located at the root of the engine source code.

C++ unit tests can be run on Linux, macOS, and Windows operating systems.

Tests can only be run with editor tools enabled, which means that export templates cannot be tested currently.

Before tests can be actually run, the engine must be compiled with the tests build option enabled (and any other build option you typically use), as the tests are not compiled as part of the engine by default:

Once the build is done, run the tests with a --test command-line option:

The test run can be configured with the various doctest-specific command-line options. To retrieve the full list of supported options, run the --test command with the --help option:

Any other options and arguments after the --test command are treated as arguments for doctest.

Tests are compiled automatically if you use the dev_mode=yes SCons option. dev_mode=yes is recommended if you plan on contributing to the engine development as it will automatically treat compilation warnings as errors. The continuous integration system will fail if any compilation warnings are detected, so you should strive to fix all warnings before opening a pull request.

By default, all tests are run if you don't supply any extra arguments after the --test command. But if you're writing new tests or would like to see the successful assertions output coming from those tests for debugging purposes, you can run the tests of interest with the various filtering options provided by doctest.

The wildcard syntax * is supported for matching any number of characters in test suites, test cases, and source file names:

For instance, to run only the String unit tests, run:

Successful assertions output can be enabled with the --success (-s) option, and can be combined with any combination of filtering options above, for instance:

Specific tests can be skipped with corresponding -exclude options. As of now, some tests include random stress tests which take a while to execute. In order to skip those kind of tests, run the following command:

Test suites represent C++ header files which must be included as part of the main test entry point in tests/test_main.cpp. Most test suites are located directly under tests/ directory.

All header files are prefixed with test_, and this is a naming convention which the Godot build system relies on to detect tests throughout the engine.

Here's a minimal working test suite with a single test case written:

You can quickly generate new tests using the create_test.py script found in the tests/ directory. This script automatically creates a new test file with the required boilerplate code in the appropriate location. It's also able to automatically include the new header in tests/test_main.cpp using invasive mode (-i flag). To view usage instructions, run the script with the -h flag.

The tests/test_macros.h header encapsulates everything which is needed for writing C++ unit tests in Godot. It includes doctest assertion and logging macros such as CHECK as seen above, and of course the definitions for writing test cases themselves.

tests/test_macros.h source code for currently implemented macros and aliases for them.

Test cases are created using TEST_CASE function-like macro. Each test case must have a brief description written in parentheses, optionally including custom tags which allow to filter the tests at runtime, such as [String], [Stress] etc.

Test cases are written in a dedicated namespace. This is not required, but allows to prevent naming collisions for when other static helper functions are written to accommodate the repeating testing procedures such as populating common test data for each test, or writing parameterized tests.

Godot supports writing tests per C++ module. For instructions on how to write module tests, refer to Writing custom unit tests.

In situations where you have a common setup for several test cases with only slight variations, subcases can be very helpful. Here's an example:

Each SUBCASE causes the TEST_CASE to be executed from the beginning. Subcases can be nested to an arbitrary depth, but it is advised to limit nesting to no more than one level deep.

A list of all commonly used assertions used throughout the Godot tests, sorted by severity.

Test if condition holds true. Fails the entire test immediately if the condition does not hold true.

Test if condition does not hold true. Fails the entire test immediately if the condition holds true.

Test if condition holds true. Marks the test run as failing, but allow to run other assertions.

Test if condition does not hold true. Marks the test run as failing, but allow to run other assertions.

Test if condition holds true. Does not fail the test under any circumstance, but logs a warning if something does not hold true.

Test if condition does not hold true. Does not fail the test under any circumstance, but logs a warning if something holds true.

All of the above assertions have corresponding *_MESSAGE macros, which allow to print optional message with rationale of what should happen.

Prefer to use CHECK for self-explanatory assertions and CHECK_MESSAGE for more complex ones if you think that it deserves a better explanation.

doctest: Assertion macros.

The test output is handled by doctest itself, and does not rely on Godot printing or logging functionality at all, so it's recommended to use dedicated macros which allow to log test output in a format written by doctest.

Marks the test as failing, but continue the execution. Can be wrapped in conditionals for complex checks.

Fails the test immediately. Can be wrapped in conditionals for complex checks.

Different reporters can be chosen at runtime. For instance, here's how the output can be redirected to an XML file:

doctest: Logging macros.

Sometimes, it's not always feasible to test for an expected result. With the Godot development philosophy of that the engine should not crash and should gracefully recover whenever a non-fatal error occurs, it's important to check that those failure paths are indeed safe to execute without crashing the engine.

Unexpected behavior can be tested in the same way as anything else. The only problem this creates is that the error printing shall unnecessarily pollute the test output with errors coming from the engine itself (even if the end result is successful).

To alleviate this problem, use ERR_PRINT_OFF and ERR_PRINT_ON macros directly within test cases to temporarily disable the error output coming from the engine, for instance:

These tags can be added to the test case name to modify or extend the test environment:

Required for test cases that rely on a scene tree with MessageQueue to be available. It also enables a mock rendering server and ThemeDB.

Like [SceneTree], but with additional editor-related infrastructure available, such as EditorSettings.

Initializes the AudioServer using a mock audio driver.

Creates the default 2D navigation server and makes it available for testing.

Creates the default 3D navigation server and makes it available for testing.

You can use them together to combine multiple test environment extensions.

The following macros can be use to test signals:

SIGNAL_WATCH(object, "signal_name")

Starts watching the specified signal on the given object.

SIGNAL_UNWATCH(object, "signal_name")

Stops watching the specified signal on the given object.

SIGNAL_CHECK("signal_name", Vector<Vector<Variant>>)

Checks the arguments of all fired signals. The outer vector contains each fired signal, while the inner vector contains the list of arguments for that signal. The order of signals is significant.

SIGNAL_CHECK_FALSE("signal_name")

Checks if the specified signal was not fired.

SIGNAL_DISCARD("signal_name")

Discards all records of the specified signal.

Below is an example demonstrating the use of these macros:

Test tools are advanced methods which allow you to run arbitrary procedures to facilitate the process of manual testing and debugging the engine internals.

These tools can be run by supplying the name of a tool after the --test command-line option. For instance, the GDScript module implements and registers several tools to help the debugging of the tokenizer, parser, and compiler:

If any such tool is detected, then the rest of the unit tests are skipped.

Test tools can be registered anywhere throughout the engine as the registering mechanism closely resembles of what doctest provides while registering test cases using dynamic initialization technique, but usually these can be registered at corresponding register_types.cpp sources (per module or core).

Here's an example of how GDScript registers test tools in modules/gdscript/register_types.cpp:

The custom command-line parsing can be performed by a test tool itself with the help of OS get_cmdline_args method.

Godot uses doctest to prevent regressions in GDScript during development. There are several types of test scripts which can be written:

tests for expected errors;

Therefore, the process of writing integration tests for GDScript is the following:

Pick a type of a test script you'd like to write, and create a new GDScript file under the modules/gdscript/tests/scripts directory within corresponding sub-directory.

Write GDScript code. The test script must have a function called test() which takes no arguments. Such function will be called by the test runner. The test should not have any dependency unless it's part of the test too. Global classes (using class_name) are registered before the runner starts, so those should work if needed.

Here's an example test script:

Change directory to the Godot source repository root.

Generate *.out files to update the expected results from the output:

You may add the --print-filenames option to see filenames as their test outputs are generated. If you are working on a new feature that is causing hard crashes, you can use this option to quickly find which test file causes the crash and debug from there.

Run GDScript tests with:

This also accepts the --print-filenames option (see above).

If no errors are printed and everything goes well, you're done!

Make sure the output does have the expected values before submitting a pull request. If --gdscript-generate-tests produces *.out files which are unrelated to newly added tests, you should revert those files back and only commit *.out files for new tests.

The GDScript test runner is meant for testing the GDScript implementation, not for testing user scripts nor testing the engine using scripts. We recommend writing new tests for already resolved issues related to GDScript at GitHub, or writing tests for currently working features.

If your test case requires that there is no test() function present inside the script file, you can disable the runtime section of the test by naming the script file so that it matches the pattern *.notest.gd. For example, "test_empty_file.notest.gd".

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Using C++ profilers — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/debugging/using_cpp_profilers.html

**Contents:**
- Using C++ profilers
- Recommended profilers
- Setting up Godot
- Benchmarking startup/shutdown times
- Profiler-specific instructions
  - VerySleepy
  - HotSpot
  - Xcode Instruments
- User-contributed notes

To optimize Godot's performance, you need to know what to optimize first. To this end, profilers are useful tools.

There is a built-in GDScript profiler in the editor, but using C++ profiler may be useful in cases where the GDScript profiler is not accurate enough or is missing information due to bugs in the profiler.

VerySleepy (Windows only)

Xcode Instruments (macOS only)

These profilers may not be the most powerful or flexible options, but their standalone operation and limited feature set tends to make them easier to use.

To get useful profiling information, it is absolutely required to use a Godot build that includes debugging symbols. Official binaries do not include debugging symbols, since these would make the download size significantly larger.

To get profiling data that best matches the production environment (but with debugging symbols), you should compile binaries with the production=yes debug_symbols=yes SCons options.

It is possible to run a profiler on less optimized builds (e.g. target=template_debug without LTO), but results will naturally be less representative of real world conditions.

Do not strip debugging symbols on the binaries using the strip command after compiling the binaries. Otherwise, you will no longer get useful profiling information when running a profiler.

If you're looking into optimizing Godot's startup/shutdown performance, you can tell the profiler to use the --quit command line option on the Godot binary. This will exit Godot just after it finished starting. The --quit option works with --editor, --project-manager or --path <path to project directory> (which runs a project directly).

See Command line tutorial for more command line arguments supported by Godot.

Start the Godot editor or your project first. If you start the Project Manager, make sure to edit or run a project first. Otherwise, the profiler will not track the child process since the Project Manager will spawn a child process for every project edited or run.

Open VerySleepy and select the Godot executable in the list of processes on the left:

Click the Profile All button on the right to start profiling.

Perform the actions you wish to profile in the editor or project. When you're done, click Stop (not Abort).

Wait for the results window to appear.

Once the results window appears, filter the view to remove external modules (such as the graphics driver). You can filter by module by finding a line whose Module matches the Godot executable name, right-clicking that line then choosing Filter Module to <Godot executable name> in the dropdown that appears.

Your results window should now look something like this:

Open HotSpot. Click Record Data:

In the next window, specify the path to the Godot binary that includes debug symbols.

Specify command line arguments to run a specific project, with or without the editor.

The path to the working directory can be anything if an absolute path is used for the --path command line argument. Otherwise, it must be set to that the relative path to the project is valid.

Make sure Elevate Privileges is checked if you have administrative privileges. While not essential for profiling Godot, this will ensure all events can be captured. Otherwise, some events may be missing in the capture. Your settings should now look something like this:

Click Start Recording and perform the actions you wish to profile in the editor/project.

Quit the editor/project normally or use the Stop Profiling button in HotSpot to stop profiling early. Stopping profiling early can result in cleaner profiles if you're not interested in the engine's quit procedure.

Click View Results and wait for the profiling visualization to be generated:

Use the tabs at the top to navigate between the different views. These views show the same data, but in different ways. The Flame Graph tab is a good way to see which functions take up the most time at a glance. These functions are therefore the most important ones to optimize, since optimizing them will improve performance the most.

At the bottom of all tabs except Summary, you will also see a list of CPU threads started by the engine among with the CPU utilization for each thread. This lets you see threads that can be a bottleneck at a given point in time.

If you don't want the startup procedure to be included in the profile, you can also attach HotSpot to a running process by clicking Record Data then setting the Launch Application dropdown option to Attach To Process(es).

This process attachment-based workflow is similar to the one used by VerySleepy.

Open Xcode. Select Open Developer Tool - Instruments from the Xcode app menu:

Double-click on Time Profiler in the Instruments window:

In the Time Profiler window, click on the Target menu, select Choose target... and specify the path to the Godot binary, command line arguments and environment variables in the next window.

You can also attach the Time Profiler to a running process by selecting it from the Target menu.

Click the Start an immediate mode recording button to start profiling.

Perform the actions you wish to profile in the editor or project. When you're done, click the Stop button.

Wait for the results to appear.

At the bottom of the window you will see a call tree for all CPU threads started, and the Heaviest Stack Trace overview.

Select Hide system libraries in the Call Tree menu (at the bottom of window) to remove external modules.

You can use the timeline at the top of the window to display details for the specific time period.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Using sanitizers — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/debugging/using_sanitizers.html

**Contents:**
- Using sanitizers
- What are sanitizers?
- Using sanitizers on Godot
- Address sanitizer (ASAN)
- Leak sanitizer (LSAN)
- Memory sanitizer (MSAN)
- Thread sanitizer (TSAN)
- Undefined behavior sanitizer (UBSAN)
- Platform-specific sanitizers
  - Web

Sanitizers are static instrumentation tools that help find bugs that traditional debuggers usually cannot catch. This is particularly useful when combined with Unit testing in continuous integration.

Sanitizers can be used on Windows, macOS and Linux by using the Clang (LLVM), GCC or Visual Studio compilers. Certain platforms may also have their own sanitizers available. In situations where a single sanitizer is provided by several different compilers, remember that their output and behavior will differ slightly.

Sanitizers require recompiling the binary. This means you cannot use official Godot binaries to run sanitizers.

When compiling with any of the sanitizers enabled, the resulting binary will have the .san suffix added to its name to distinguish it from a binary without sanitizers.

There is a performance impact as many additional runtime checks need to be performed. Memory utilization will also increase. It is possible to enable certain combinations of multiple sanitizers in a single build. Beware of the performance impact when using multiple sanitizers at once though, as the resulting binary may be excessively slow.

Certain options can be passed to sanitizers without having to recompile the binary using environment variables.

Available in Clang and GCC.

Supported platforms: Linux, macOS, Windows (Visual Studio), Web

Clang ASAN documentation

The address sanitizer is generally the most frequently used sanitizer. It can diagnose issues such as buffer overruns and out-of-bounds access. If the engine crashes with a message such as free(): invalid pointer, this is typically the result of a buffer overrun. (This message is printed by the C runtime, not Godot.)

In certain situations (such as detecting uninitialized memory reads), the address sanitizer doesn't suffice. The Memory sanitizer (MSAN) should be used instead.

It is also possible to detect use-after-return situations by specifying the ASAN_OPTIONS=detect_stack_use_after_return=1 environment variable before running Godot (not when compiling it). This increases the address sanitizer's runtime overhead, so only enable this feature when you actually need it.

To enable the address sanitizer in a Godot build, pass the use_asan=yes SCons option when compiling. Enabling ASAN generally makes the resulting binary about 2× slower.

Due to a design decision, the address, memory and thread sanitizers are mutually exclusive. This means you can only use one of those sanitizers in a given binary.

Available in Clang and GCC.

Supported platforms: Linux, Web

Clang LSAN documentation

The leak sanitizer can detect memory leaks, which are situations where memory that is no longer in use is never freed by the running program. This can potentially lead to out-of-memory situations if the program runs for long enough. Since Godot may run on dedicated servers for months or even years without a restart, it's important to fix memory leaks when they occur.

To enable the leak sanitizer in a Godot build, pass the use_lsan=yes SCons option when compiling. Enabling LSAN only has a small performance overhead, but the program will be much slower to exit as leak detection occurs when the program exits.

Available in Clang only, not GCC.

Supported platforms: Linux

Clang MSAN documentation

The memory sanitizer complements the Address sanitizer (ASAN). Unlike the address sanitizer, the memory sanitizer can detect uninitialized memory reads.

To enable the memory sanitizer in a Godot build, pass the use_msan=yes SCons option when compiling. Enabling MSAN generally makes the resulting binary about 3× slower.

Due to a design decision, the address, memory and thread sanitizers are mutually exclusive. This means you can only use one of those sanitizers in a given binary.

Available in Clang and GCC.

Supported platforms: Linux, macOS

Clang TSAN documentation

The thread sanitizer is used to track down race conditions related to multithreading. A race condition is when multiple threads try to modify the same data at the same time. Since thread scheduling can be ordered in any fashion by the operating system, this leads to incorrect behavior that only occurs occasionally (and can be difficult to track as a result). To prevent a race condition, you need to add a lock to ensure only one thread can access the shared data at a given time.

To enable the thread sanitizer in a Godot build, pass the use_tsan=yes SCons option when compiling. Enabling TSAN generally makes the resulting binary 10× slower, while also multiplying memory usage by an approximately 8× factor.

Due to a design decision, the address, memory and thread sanitizers are mutually exclusive. This means you can only use one of those sanitizers in a given binary.

On Linux, if you stumble upon the following error:

FATAL: ThreadSanitizer: unexpected memory mapping

You may need to temporarily lower the Address Space Layout Randomization (ASLR) entropy in your system with:

Or preferably disable it entirely with:

And as soon as you are done with the thread sanitizer, increase the ASLR entropy with:

Or re-enable ASLR with:

Rebooting your machine will also revert the ASLR state to its default values.

It's important to revert the changes as soon as possible because lowering the ASLR entropy or disabling ASLR entirely can be a security risk.

Available in Clang and GCC.

Supported platforms: Linux, macOS, Web

Clang UBSAN documentation

The undefined behavior sanitizer is used to track down situations where the program exhibits random and unpredictable behavior. This is due to C/C++ code that is accepted by the compiler, but is not correct. Compiling with a different set of optimizations can also change the observed results of undefined behavior.

To enable the undefined behavior sanitizer in a Godot build, pass the use_ubsan=yes SCons option when compiling. Enabling UBSAN only has a small performance overhead.

When compiling for the Web, there are 2 additional sanitizer SCons options available:

use_assertions=yes enables runtime Emscripten assertions, which can catch various issues.

use_safe_heap=yes enables Emscripten's SAFE_HEAP sanitizer. It provides similar functionality to ASAN, but it focuses on issues that are specific to WebAssembly. SAFE_HEAP is not guaranteed to be compatible with ASAN and UBSAN in the same binary, so you may have to build it separately.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Validation layers — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/debugging/vulkan/vulkan_validation_layers.html

**Contents:**
- Validation layers
- Windows
- macOS
- Linux, *BSD
- iOS
- Web
- Android
  - Enabling validation layers
    - Build validation layers from official sources
    - Copy libraries

Validation layers enable developers to verify their application's correct use of the Vulkan API. Validation layers can be enabled in both debug and release builds, including in exported projects.

Enabling validation layers has a performance impact, so only enable them when you actually need the output to debug the application.

Install the Vulkan SDK https://vulkan.lunarg.com/sdk/home, which contains validation layers as part of its default installation. No need to enable any optional features in the installer; installing the core Vulkan SDK suffices. You don't need to reboot after installing the SDK, but you may need to close and reopen your current terminal.

After installing the Vulkan SDK, run Godot with the --gpu-validation command line argument. You can also specify --gpu-abort which will make Godot quit as soon as a validation error happens. This can prevent your system from freezing if a validation error occurs.

Official Godot macOS builds do not support validation layers, as these are statically linked against the Vulkan SDK. Dynamic linking must be used instead.

In practice, this means that using validation layers on macOS requires you to use a Godot build compiled with the use_volk=yes SCons option. Compiling for macOS. If testing validation layers on an exported project, you must recompile the export template and specify it as a custom export template in your project's macOS export preset.

Install the Vulkan SDK https://vulkan.lunarg.com/sdk/home, which contains validation layers as part of its default installation. No need to enable any optional features in the installer; installing the core Vulkan SDK suffices. You don't need to reboot after installing the SDK, but you may need to close and reopen your current terminal.

After installing the Vulkan SDK, run a Godot binary that was compiled with use_volk=yes SCons option. Specify the --gpu-validation command line argument. You can also specify --gpu-abort which will make Godot quit as soon as a validation error happens. This can prevent your system from freezing if a validation error occurs.

Install Vulkan validation layers from your distribution's repositories:

You don't need to reboot after installing the validation layers, but you may need to close and reopen your current terminal.

After installing the package, run Godot with the --gpu-validation command line argument. You can also specify --gpu-abort which will make Godot quit as soon as a validation error happens. This can prevent your system from freezing if a validation error occurs.

Validation layers are currently not supported on iOS.

Validation layers are not supported on the web platform, as there is no support for Vulkan there.

After enabling validation layers on Android, a developer can see errors and warning messages in the adb logcat output.

To build Android libraries, follow the instructions on Khronos' repository. After a successful build, the libraries will be located in Vulkan-ValidationLayers/build-android/libs.

Copy libraries from Vulkan-ValidationLayers/build-android/libs to godot/platform/android/java/app/libs/debug/vulkan_validation_layers.

Your Godot source directory tree should look like on the example below:

If the subdirectory libs/debug/vulkan_validation_layers doesn't exist, create it.

Linked validation layers are automatically loaded and enabled in Android debug builds. You can use Godot's One-click deploy feature to quickly test your project with the validation layers enabled.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Variant class — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/architecture/variant_class.html

**Contents:**
- Variant class
- About
  - References
- List of variant types
- Containers: Array and Dictionary
  - References
- User-contributed notes

Variant is the most important datatype in Godot. A Variant takes up only 24 bytes on 64-bit platforms (20 bytes on 32-bit platforms) and can store almost any engine datatype inside of it. Variants are rarely used to hold information for long periods of time, instead they are used mainly for communication, editing, serialization and generally moving data around.

Store almost any datatype.

Perform operations between many variants (GDScript uses Variant as its atomic/native datatype).

Be hashed, so it can be compared quickly to other variants.

Be used to convert safely between datatypes.

Be used to abstract calling methods and their arguments (Godot exports all its functions through variants).

Be used to defer calls or move data between threads.

Be serialized as binary and stored to disk, or transferred via network.

Be serialized to text and use it for printing values and editable settings.

Work as an exported property, so the editor can edit it universally.

Be used for dictionaries, arrays, parsers, etc.

Basically, thanks to the Variant class, writing Godot itself was a much, much easier task, as it allows for highly dynamic constructs not common of C++ with little effort. Become a friend of Variant today.

All types within Variant except Nil and Object cannot be null and must always store a valid value. These types within Variant are therefore called non-nullable types.

One of the Variant types is Nil which can only store the value null. Therefore, it is possible for a Variant to contain the value null, even though all Variant types excluding Nil and Object are non-nullable.

core/variant/variant.h

These types are available in Variant:

Nil (can only store null)

2D counterpart of AABB

3D counterpart of Rect2

Both Array and Dictionary are implemented using variants. A Dictionary can match any datatype used as key to any other datatype. An Array just holds an array of Variants. Of course, a Variant can also hold a Dictionary or an Array inside, making it even more flexible.

Modifications to a container will modify all references to it. A Mutex should be created to lock it if multi-threaded access is desired.

core/variant/dictionary.h

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Visual Studio Code — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/configuring_an_ide/visual_studio_code.html

**Contents:**
- Visual Studio Code
- Importing the project
- Debugging the project
- Configuring Intellisense
- User-contributed notes

This documentation is for contributions to the game engine, and not using Visual Studio Code as a C# or GDScript editor. To code C# or GDScript in an external editor, see the C# guide to configure an external editor or the GDScript guide to using an external text editor.

Visual Studio Code is a free cross-platform code editor by Microsoft (not to be confused with Visual Studio).

Make sure the C/C++ extension is installed. You can find instructions in the official documentation. Alternatively, clangd can be used instead.

When using the clangd extension, run scons compiledb=yes.

From the Visual Studio Code's main screen open the Godot root folder with File > Open Folder....

Press Ctrl + Shift + P to open the command prompt window and enter Configure Task.

Select the Create tasks.json file from template option.

If there is no such option as Create tasks.json file from template available, either delete the file if it already exists in your folder or create a .vscode/tasks.json file manually. See Tasks in Visual Studio Code for more details on tasks.

Within the tasks.json file find the "tasks" array and add a new section to it:

An example of a filled out tasks.json.

Arguments can be different based on your own setup and needs. See Introduction to the buildsystem for a full list of arguments.

To run and debug the project you need to create a new configuration in the launch.json file.

Press Ctrl + Shift + D to open the Run panel.

If launch.json file is missing you will be prompted to create a new one.

Select C++ (GDB/LLDB). There may be another platform-specific option here. If selected, adjust the configuration example provided accordingly.

Within the launch.json file find the "configurations" array and add a new section to it:

An example of a filled out launch.json.

Due to sporadic performance issues, it is recommended to use LLDB over GDB on Unix-based systems. Make sure that the CodeLLDB extension is installed for configurations using lldb.

If you encounter issues with lldb, you may consider using gdb (see the LinuxBSD_gdb configuration).

Do note that lldb may work better with LLVM-based builds. See Compiling for Linux, *BSD for further information.

The name under program depends on your build configuration, e.g. godot.linuxbsd.editor.dev.x86_64 for 64-bit LinuxBSD platform with target=editor and dev_build=yes.

For the C/C++ extension:

To fix include errors you may be having, you need to configure some settings in the c_cpp_properties.json file.

First, make sure to build the project since some files need to be generated.

Edit the C/C++ Configuration file either with the UI or with text:

Add an include path for your platform, for example, ${workspaceFolder}/platform/windows.

Add defines for the editor TOOLS_ENABLED, debug builds DEBUG_ENABLED, and tests TESTS_ENABLED.

Make sure the compiler path is configured correctly to the compiler you are using. See Introduction to the buildsystem for further information on your platform.

The c_cpp_properties.json file should look similar to this for Windows:

Alternatively, you can use the scons argument compiledb=yes and set the compile commands setting compileCommands to compile_commands.json, found in the advanced section of the C/C++ Configuration UI.

This argument can be added to your build task in tasks.json since it will need to be run whenever files are added or moved.

If you run into any issues, ask for help in one of Godot's community channels.

To get linting on class reference XML files, install the vscode-xml extension.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Visual Studio — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/configuring_an_ide/visual_studio.html

**Contents:**
- Visual Studio
- Importing the project
- Debugging the project
- User-contributed notes

Visual Studio Community is a Windows-only IDE by Microsoft that's free for individual use or non-commercial use within organizations. It has many useful features, such as memory view, performance view, source control and more.

This documentation is for contributions to the game engine, and not using Visual Studio as a C# editor. To code C# in an external editor, see the C# guide to configure an external editor.

Visual Studio requires a solution file to work on a project. While Godot does not come with the solution file, it can be generated using SCons.

Navigate to the Godot root folder and open a Command Prompt or PowerShell window.

You can now open the project by double-clicking on the godot.sln in the project root or by using the Open a project or solution option inside of the Visual Studio.

Use the Build top menu to build the project.

Visual Studio must be configured with the C++ package. It can be selected in the installer:

Visual Studio features a powerful debugger. This allows the user to examine Godot's source code, stop at specific points in the code, inspect the current execution context, and make live changes to the codebase.

You can launch the project with the debugger attached using the Debug > Start Debugging option from the top menu. However, unless you want to debug the Project Manager specifically, you'd need to configure debugging options first. This is due to the fact that when the Godot Project Manager opens a project, the initial process is terminated and the debugger gets detached.

To configure the launch options to use with the debugger use Project > Properties from the top menu:

Open the Debugging section and under Command Arguments add two new arguments: the -e flag opens the editor instead of the Project Manager, and the --path argument tells the executable to open the specified project (must be provided as an absolute path to the project root, not the project.godot file; if the path contains spaces be sure to pass it inside double quotation marks).

To learn more about command line arguments, refer to the command line tutorial.

Even if you start the project without a debugger attached it can still be connected to the running process using Debug > Attach to Process... menu.

To check that everything is working, put a breakpoint in main.cpp and press F5 to start debugging.

If you run into any issues, ask for help in one of Godot's community channels.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---

## Xcode — Godot Engine (stable) documentation in English

**URL:** https://docs.godotengine.org/en/stable/engine_details/development/configuring_an_ide/xcode.html

**Contents:**
- Xcode
- Importing the project
- Debugging the project
- User-contributed notes

Xcode is a free macOS-only IDE. You can download it from the Mac App Store.

From Xcode's main screen create a new project using the Other > External Build System template.

Now choose a name for your project and set the path to scons executable in build tool (to find the path you can type where scons in a terminal).

Open the main target from the Targets section and select the Info tab.

Fill out the form with the following settings:

See Introduction to the buildsystem for a full list of arguments.

A full path to the Godot root folder

Add a Command Line Tool target which will be used for indexing the project by choosing File > New > Target....

Select macOS > Application > Command Line Tool.

Name it something so you know not to compile with this target (e.g. GodotXcodeIndex).

For this target open the Build Settings tab and look for Header Search Paths.

Set Header Search Paths to the absolute path to the Godot root folder. You need to include subdirectories as well. To achieve that, add two two asterisks (**) to the end of the path, e.g. /Users/me/repos/godot-source/**.

Add the Godot source to the project by dragging and dropping it into the project file browser.

Select Create groups for the Added folders option and check only your command line indexing target in the Add to targets section.

Xcode will now index the files. This may take a few minutes.

Once Xcode is done indexing, you should have jump-to-definition, autocompletion, and full syntax highlighting.

To enable debugging support you need to edit the external build target's build and run schemes.

Open the scheme editor of the external build target.

Locate the Build > Post Actions section.

Add a new script run action

Under Provide build settings from select your project. This allows to reference the project directory within the script.

Create a script that will give the binary a name that Xcode can recognize, e.g.:

Build the external build target.

Open the scheme editor again and select Run.

Set the Executable to the file you linked in your post-build action script.

Check Debug executable.

You can add two arguments on the Arguments tab: the -e flag opens the editor instead of the Project Manager, and the --path argument tells the executable to open the specified project (must be provided as an absolute path to the project root, not the project.godot file).

To check that everything is working, put a breakpoint in platform/macos/godot_main_macos.mm and run the project.

If you run into any issues, ask for help in one of Godot's community channels.

Please read the User-contributed notes policy before submitting a comment.

© Copyright 2014-present Juan Linietsky, Ariel Manzur and the Godot community (CC BY 3.0).

---
