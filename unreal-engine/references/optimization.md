# Unreal-Engine - Optimization

**Pages:** 14

---

## Audio Memory Management

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-memory-management-in-unreal-engine

**Contents:**
- Audio Memory Management

A collection of topics related to audio memory management in Unreal Engine.



---

## Stat Commands

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine

**Contents:**
- Stat Commands
        - Prerequisite topics
- Stat Command Table
- Select Commands
  - Levels
    - Use Case
    - Usage
      - Level Color Codes
  - StartFile
    - Use Case

Console commands specific to displaying game statistics

In order to understand and use the content on this page, make sure you are familiar with the following topics:

To profile their Unreal Engine (UE) projects, developers can enter the following stat commands into the console while running their game in Play In Editor (PIE) mode.

Click for full image.

To locate a stat command from the Editor's Stat menu, select the dropdown arrow next to the Viewport Setting button.

Click for full image.

Running the editor with the LOG command enables developers to record useful information from a stat dump, and to do so, enable the editor (game project) to generate a log file by running it with the LOG command (for example, UnrealEditor.exe -silent LOG=MyLog.txt).

Type stat followed by a space and any of these commands to activate them:

<?> <sort=distance|class|name|waves|default> <-debug> <off> Shows active SoundCues and SoundWaves.

Starts a statistics capture, creating a new file in the Profiling directory.

Stop this operation with the stat StopFile command.

Overall frame time as well as the game thread, rendering thread, and GPU times.

This is a great stat command to start with because it helps developers focus their profiling work.

The stat levels command displays level streaming information, which are grouped under the persistent level.

This command is useful for developers wanting to view a list of currently active levels, including whether they are visible, pre-loading, loading, or unloading. Additionally, this command displays how many seconds it took to go from a load request to load finish.

To view streaming level information, enter stat levels into PIE Console. To determine what state a level is in, refer to the Level Color Codes table below.

Click for full image.

The stat startfile command starts a statistics capture, and creates a new file in a Profiling directory. Typically, the engine saves statistics captures under <PROJECT_DIRECTORY>\Saved\Profiling\UnrealStats.

To profile a project's performance with Session Frontend Profiler, capture statistical samples and log them to *.uestats files.

To capture and log statistics to a *.uestats file, enter stat startfile into PIE Console.

To prevent StartFile from bloating the disk with large uestats files, run stat StopFile. Additionally, even if PIE Mode is closed, StartFile continues running in the background, which can result in bloated log files, so make sure to run the StopFile command to stop logging the project's performance.

To load statistics into Session Frontend Profiler:

After Session Frontend loads the file, the capture data is visible in the Profiler for further analysis. Read the Profiler Tool Reference to learn more about reviewing profile captures in Session Frontend.

Click for full image.

The stat stopfile command stops a statistics capture that was started by the StartFile command. Additionally, the StopFile command closes the file that was created in the Profiling directory.

To prevent StartFile from bloating the disk with large uestats files, run stat StopFile. Additionally, even if PIE Mode is closed, StartFile will continue running in the background, which can result in bloated log files, so make sure to run the StopFile command to stop logging the project's performance.

To stop capturing and logging statistics, enter stat stopfile into PIE Console.

Typically, developers want to determine if a bottleneck (negative performance impact) exists in the Game thread, in the Draw (rendering) thread, or on the GPU.

Click for full image.

The stat unit command displays performance information for the project's Frame, Game, Draw, GPU, RHIT, and DynRes threads.

If supported (and enabled), Dynamic Resolution shows Primary Screen Percentage by Secondary Screen Percentage.

To determine the project's bottleneck, launch the game in a non-debug build, and enter stat unit into PIE Console.



---

## Testing and Optimizing Your Content

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-optimizing-your-content?application_version=5.4

**Contents:**
- Testing and Optimizing Your Content
- Topics

How to make sure your content does what you expect it to, at the quality and frame rates that you need.

Unreal Engine includes tools and features that help developers test and optimize content for applications that need to run at framerates for high-quality experiences.

To learn more, read about the following topics.



---

## Testing and Optimizing Your Content

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-optimizing-your-content

**Contents:**
- Testing and Optimizing Your Content
- Topics

How to make sure your content does what you expect it to, at the quality and frame rates that you need.

Unreal Engine includes tools and features that help developers test and optimize content for applications that need to run at framerates for high-quality experiences.

To learn more, read about the following topics.



---

## Testing and Optimizing Your Content

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-optimizing-your-content?application_version=4.27

**Contents:**
- Testing and Optimizing Your Content
- Topics

How to make sure your content does what you expect it to, at the quality and frame rates that you need.

Unreal Engine includes tools and features that help developers test and optimize content for applications that need to run at framerates for high-quality experiences. To learn more, read about the following topics.



---

## Testing and Optimizing Your Content

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-optimizing-your-content?application_version=5.6

**Contents:**
- Testing and Optimizing Your Content
- Topics

How to make sure your content does what you expect it to, at the quality and frame rates that you need.

Unreal Engine includes tools and features that help developers test and optimize content for applications that need to run at framerates for high-quality experiences.

To learn more, read about the following topics.



---

## Testing and Optimizing Your Content

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-optimizing-your-content?application_version=5.3

**Contents:**
- Testing and Optimizing Your Content
- Topics

How to make sure your content does what you expect it to, at the quality and frame rates that you need.

Unreal Engine includes tools and features that help developers test and optimize content for applications that need to run at framerates for high-quality experiences.

To learn more, read about the following topics.



---

## Testing and Optimizing Your Content

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-optimizing-your-content?application_version=5.0

**Contents:**
- Testing and Optimizing Your Content
- Topics

How to make sure your content does what you expect it to, at the quality and frame rates that you need.

Unreal Engine includes tools and features that help developers test and optimize content for applications that need to run at framerates for high-quality experiences.

To learn more, read about the following topics.



---

## Testing and Optimizing Your Content

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-optimizing-your-content?application_version=5.5

**Contents:**
- Testing and Optimizing Your Content
- Topics

How to make sure your content does what you expect it to, at the quality and frame rates that you need.

Unreal Engine includes tools and features that help developers test and optimize content for applications that need to run at framerates for high-quality experiences.

To learn more, read about the following topics.



---

## Testing and Optimizing Your Content

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-optimizing-your-content?application_version=5.1

**Contents:**
- Testing and Optimizing Your Content
- Topics

How to make sure your content does what you expect it to, at the quality and frame rates that you need.

Unreal Engine includes tools and features that help developers test and optimize content for applications that need to run at framerates for high-quality experiences.

To learn more, read about the following topics.



---

## Testing and Optimizing Your Content

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-optimizing-your-content?application_version=5.2

**Contents:**
- Testing and Optimizing Your Content
- Topics

How to make sure your content does what you expect it to, at the quality and frame rates that you need.

Unreal Engine includes tools and features that help developers test and optimize content for applications that need to run at framerates for high-quality experiences.

To learn more, read about the following topics.



---

## Testing and Optimizing Your Content

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-optimizing-your-content?application_version=5.7

**Contents:**
- Testing and Optimizing Your Content
- Topics

How to make sure your content does what you expect it to, at the quality and frame rates that you need.

Unreal Engine includes tools and features that help developers test and optimize content for applications that need to run at framerates for high-quality experiences.

To learn more, read about the following topics.



---

## Unreal Insights

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine

**Contents:**
- Unreal Insights
- Setting Up Unreal Insights
  - Launch From Editor
  - Launch a prebuild of Unreal Insights
  - Build From Source
- Trace
  - Shut Down Trace Server
  - Configuring the Unreal Trace Server
- Unreal Insights Session Browser
  - Trace Store

Profile your project's performance with Unreal Insights.

Unreal Insights is a telemetry capture and analysis suite that can capture events from your project at high data rates. Unreal Insights helps you identify areas of data that might require optimization.

The major components of Unreal Insights are:

Visualization of the major components of the Unreal Insights framework.

Trace sessions are self-describing, and compatible with different engine release versions. They are stored in .utrace files. Any companion data that is generated is stored in .ucache files located within the same directory as your trace files.

To start Unreal Insights from the Unreal Editor, navigate to the Trace/Insights Status Bar Widget located in the bottom toolbar of the Editor.

When you run a Trace to profile your project data, you can choose from multiple workflow options that vary depending on your Unreal Engine Build and Operating System. For more information about these workflow options, see the following pages:

If you installed a binary version of Unreal Engine you should have a compiled version of Unreal Insights located in the following directory:

If you don't have a binary version of the engine installed, or you want to compile Unreal Insights from source, you can use the following options:

Trace is a structured logging framework for tracing instrumentation events from a running process. The Unreal Trace Server runs in the background as a single server instance and can be shared between multiple projects or branches. It is an optimized program that has minimal impact on performance and does not include a User Interface.

The Trace Server is launched automatically by a separate server process executable, UnrealTraceServer.exe, which is located in the Engine/Binaries/Win64 directory folder.

The Trace Server has two components:

The Trace Server stores configuration and log files in:

The default Store folder is created here.

For additional documentation see the following pages:

The server can be shut down using the "kill" command:

> UnrealTraceServer kill

You can configure the Unreal Trace Server to add additional directories to scan for trace files like the download folder or the profiling directory of a specific project. In Unreal Insights, you can control these settings to:

Set the trace store directory. This is the location where new traces are saved.

Set additional trace directories and additional sources for trace files, for example, your user Download folder.

When configured with additional watch folders, multiple traces, and their corresponding trace file origin will be displayed with the associated color

As of UE 5.3, the Unreal Trace Server is enabled for all desktop platforms. This deprecates the store which was hosted in Unreal Insights for Linux and Mac.

Follow the steps below to Configure the Unreal Trace Server.

Open Unreal Insights. This will start the Unreal Trace Server, if not already running, on Windows, Mac, or Linux

Click on the Manage store settings dropdown button then modify the default store directory by clicking the "Set Trace Store directory" button. When starting a new trace the file will be stored in this directory.

The old trace store directory is automatically added to watch folders.

You can add one or more watch folders by clicking the Add directory button. If the new folder contains trace files they will appear in the session list with an icon colored by a unique color.

The Unreal Insights Session Browser is an interface to observe trace data. To launch the browser, navigate to the bottom toolbar, and click Trace > Insights > Unreal Insights (Session Browser.)

The Trace Store is an interface for you to observe and manage all of your stored Trace Sessions. The recorded traces are stored as files in a folder and Unreal Insights watches this folder for any data changes and then exposes the list of available traces to Unreal Insights UI.

For more information, see the Session Browser page.

The connection tab provides an interface to connect to a running game or editor with a trace server. It features multiple options to change your connection settings.

For more information, see the Session Browser page.

There are multiple options to choose to load a Trace for Analysis. You can:

For more information, see the Session Browser page.

If a live Trace session connects to the tool, it also appears in the list. Live sessions display the word LIVE in the status column and update in real-time while you analyze them. Otherwise, they are identical to pre-recorded sessions.

The tool can connect to multiple sessions at the same time, and it automatically records data for all of them as the data streams in. To analyze these sessions in real-time, load them from the list the same way you load pre-recorded sessions.

For more information, see the Session Browser page.

When viewing a session in Unreal Insights, you can select Menu in the upper-left corner of the window to access the menu.

In the menu, you can access several functions, including the following:

The Timing Insights window collects performance data. It displays the data for CPU and GPU tracks. These tracks feature multiple sub-menus to help you sort and visualize the various processing tasks and the amount of time your project spends on executing them.

The Timing Insights window features the Frames panel (1), the Timing panel filters (2), the Timing panel (3), the Log panel (4),Timers and Counters tabs (5) and the Callers and Callees panels (6).

See the Timing Insights

The Memory Insights component allows you to investigate memory usage and call stack tracing in your project.

Memory Insights traces events for every allocation, reallocation, or free event that occurs during runtime, then reconstructs that memory usage pattern during analysis.

See the Memory Insights documentation for instructions on how to set up, trace, query, and sort your data.

Unreal Insights includes Networking Insights to analyze, optimize and debug network traffic.

Refer to the Networking Insights for additional documentation.

Slate Insights extends Unreal Insights to help developers improve the performance of their UI. it provides tools to identify the root cause of a specific Slate and UMG update.

See Slate Insights for additional documentation.

Asset Loading Insights provides a way to profile the amount of time it takes to load a project's assets into UnrealEngine. Asset Loading Insights is based on the data traced from the AssetLoadTime trace channel.

This profiling tool is useful in several ways, including the following:

Unreal Cooking Insights allows you to gather and display information about the way packages are cooked in your project. Long cooking times can significantly affect the productivity of teams that are working on larger projects. By displaying the time it takes to cook each package, you can observe which packages to focus your investigation into optimizing. See Cooking Insights for additional documentation.

To get the most out of the many features that ship with Unreal Insights, You can customize your project's output with macros and command-line options.

Refer to the Reference for additional documentation.



**Examples:**

Example 1 (unknown):
```unknown
Engine\Binaries[Platform]\UnrealInsights[.exe]
```

Example 2 (unknown):
```unknown
Engine/Build/BatchFiles/RunUBT.bat UnrealInsights Win64 Development
```

Example 3 (unknown):
```unknown
./Engine/Build/BatchFiles/RunUBT.sh UnrealInsights [Linux|Mac] Development
```

---

## Unreal Insights on Android Devices

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-unreal-insights-to-profile-android-games-for-unreal-engine

**Contents:**
- Unreal Insights on Android Devices
        - Prerequisite topics
- Recommended Setup and Prerequisites
- Compile Unreal Insights
- Enable AndroidFileServer For Your Project
- Package your UE Android Project
- Connect to Your Android Device in the Device Manager
- Add UECommandline.txt to Your Android Device With Trace Enabled
- Launch Timing Insights With a Live Trace Session
- Load a Recorded Trace Session From Your Android Device

Step-by-step guide for attaching the Unreal Insights profiler to an Android application running on a test device.

In order to understand and use the content on this page, make sure you are familiar with the following topics:

Unreal Insights is a profiling tool that can record and review performance data for your Unreal Engine (UE) applications, including builds deployed on target devices. To record trace sessions, you need to run applications with Unreal Insights command line arguments. To provide these arguments on an Android device, you will need to follow some extra steps, detailed in this guide.

In this quickstart guide, you will:

Set up Unreal Insights with your Unreal Engine installation.

Deploy a build to your Android device.

Add UECommandline.txt to the deployed Android application and provide the needed arguments to record Unreal Insights trace information.

Launch Unreal Insights and attach it to the build on your Android device.

You can use any Android project with this guide. This quickstart guide uses a new project with the following settings:

Mobile/Tablet Platform

Scalable 2D/3D Quality

To follow this guide, you will need:

A version of the Android SDK compatible with your version of Unreal Engine. See the Android SDK setup guide.

Android support enabled for your project. See the Android Quickstart guide.

An Android device set up for USB or WiFi debugging with your computer. See Setting Up Your Android Device for Development.

Check the Engine/Binaries/ folder for your operating system in your Unreal Engine install directory to see if Unreal Insights is already built. For example, on Windows you would see UnrealInsights.exe in Engine/Binaries/Win64 if it is already built.

This executable is available in builds distributed through the Epic Games Launcher. If you are using a source code build and it is not present, open your Unreal Engine solution in your IDE and build the project listed under Programs/UnrealInsights.

In a later step, you will need to push a command line file to your Android device to enable Unreal Insights trace channels. To do this, you will need the Android File Server (AFS) plugin, which embeds a file server with your project that you can connect to using Unreal Android File Tool (UAFT). This is an alternative to Android Debug Bridge (adb) and is specifically created for Unreal Engine projects, providing more direct access to the UE application and its file paths. To add AFS to your project, follow these steps:

Enable the AndroidFileServer plugin.

Enable the Use AndroidFileServer setting in Project Settings > Plugins > AndroidFileServer. This will make it possible to connect to the UnrealAndroidFileTool (UAFT) and manage files in a later section.

Configure your other settings as needed for your organization's security and network needs.

For more information about configuring AFS and UAFT, see their documentation.

This walkthrough uses a device's serial number to connect with UAFT, but you can also use the Security Token in the Plugins > AndroidFileServer settings.

Package your UE project and push it to your Android device. See Packaging Android Projects for detailed instructions. If you have already set up your test device, you can use the Quick Launch option at the top of the Platforms dropdown in Unreal Editor to build your project and push it directly to your device.

For more information about packaging your project, see the Build Operations guide.

To view a live trace on your device, you need to set it up for USB or wifi debugging and make sure it's available in your Device Manager. See Setting Up Your Android Device for Development for more information about setting up your Android device to connect with UE, and see the Device Manager page for more info about using the Device Manager.

Your application must run with a set of command line arguments to enable trace sessions in Unreal Insights. UE applications on Android can take command line arguments through a file called UECommandline.txt. To push a UECommandLine.txt file to your device with the needed arguments for Unreal Insights, follow these steps:

In your Unreal Engine install directory, open the Engine/Build/Android/UnrealGame folder.

Create an empty text file called UECommandline.txt.

Add the following parameters to this text file, substituting [ProjectName] with the name of your project:

Example UECommandline.txt

You can use the following arguments to get additional load time information:

Example UECommandline.txt

Run UnrealAndroidFileTool.exe with the devices command to see a list of the devices attached to your computer. Take note of the serial number for your target device, but do not include the @ prefix.

Run UnrealAndroidFileTool.exe with the shell command to connect it to your device in interactive mode. The following is an example of connecting to a device with a device serial number and a package name for ExampleGame. Substitute the example serial number with the one you obtained in the previous step, and substitute the package name with the one you provided for your application.

Use the push command to push UECommandLine.txt to your device, using the "commandfile shortcut in place of the target path. In the example below, the project is called ExampleGame.

Close UAFT by running the quit or exit command.

If you browse your device using your file system, you will see a UECommandline.txt file on your device in the UEGame/[ProjectName] directory. When you launch your application, it will now record trace data for Unreal Insights. You can configure what trace channels and features are active with more command lines, see Unreal Insights for more information.

Open your Unreal Engine install directory and navigate to the Engine/Binaries folder.

Locate UnrealInsights.exe in the folder for your platform and double-click it to open Unreal Insights.

In the Unreal Insights Session Browser, select a session with a LIVE status that is running on your Android device, then click the Open button.

The Timing Insights window will appear showing processing data for your CPU and GPU threads.

You can now use Unreal Insights to profile performance on your Android device.

Unreal Insights trace sessions are recorded so that you can pass them between developers and review them asynchronously. You can retrieve trace session files from your device using the follwing steps:

Run UAFT with the shell command to connect it to your device in interactive mode. The example below uses a placeholder for a device's serial number to designate the target device.

Use the pull command to pull the trace file you want to put on your computer. It should be saved under your game's Saved/Traces directory, which you can access with the ^saved shortcut.

The trace file that you designate with the first file path will appear in the directory you specify on your local machine with the second file path.

If you aren't sure what the name or filepath for your trace file is, use the ls command and the -R argument to get a list of the files in your project's directory. The ^project shortcut will give you a quick way to access it from the top level.

Close UAFT by running the quit or exit command.

Run Unreal Insights and load the trace session.

For more information about how to use Unreal Insights’ suite of profiling tools, see the Unreal Insights documentation.

For more information about Android File Server and UAFT, see the Android File Server documentation.



**Examples:**

Example 1 (unknown):
```unknown
../../../[ProjectName]/[ProjectName].uproject		-tracehost=127.0.0.1	-cpuprofilertrace
```

Example 2 (unknown):
```unknown
../../../[ProjectName]/[ProjectName].uproject  -tracehost=127.0.0.1 -filetrace -loadtimetrace  -statnamedevents -trace=Bookmark,Frame,CPU,GPU,LoadTime,File
```

Example 3 (unknown):
```unknown
UnrealAndroidFileTool.exe -s AB187923123CD123 -p -k [security token] com.OrganizationName.ExampleGame shell
```

Example 4 (unknown):
```unknown
push D:/UnrealEngine/Projects/ExampleGame/Engine/Build/Android/UnrealGame/UECommandLine.txt ^commandfile
```

---
