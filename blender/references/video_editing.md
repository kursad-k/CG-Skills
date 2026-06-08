# Blender - Video Editing

**Pages:** 14

---

## Cache¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/sequencer/sidebar/cache.html

**Contents:**
- Cache¶
- Cache Settings¶
  - Display¶

The Cache is used to store preview frames in memory so they can be displayed much faster during playback, rather than being re-rendered for each frame. This is especially useful for maintaining smooth performance when editing or scrubbing through a sequence.

The total cache memory limit can be configured in the System tab of the Preferences.

Which frames are cached can be visualized by enabling Show Cache in the Timeline overlay settings.

Sidebar ‣ Cache ‣ Cache Settings

This panel allows configuration of how and when image data is cached during editing. These settings apply globally to all strips in the Video Sequence Editor.

When enabled, Blender will automatically prefetch and cache frames after the current frame in the background. This can result in smoother playback performance.

Note: prefetching is not currently supported for Scene strips.

Caches raw image data immediately after it is read from disk. This speeds up adjustments to strip parameters such as color correction, but increases memory usage.

Caches the final composited image for each frame, allowing faster playback of fully processed strips.

Visual indicators in the Timeline showing which frames are cached.

Displays a red bar in the Timeline below frames cached in their raw state.

Displays a blue bar at the top of Timeline for frames cached in their final composited state.

A readout at the bottom of the panel shows real-time statistics about cache usage:

Current Cache Size: Total amount of memory currently used by the cache system.

Raw: Memory usage by raw image cache.

Final: Memory usage by final rendered frame cache.

---

## Channels¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/sequencer/channels.html

**Contents:**
- Channels¶
- Channel Region¶

A channel is a horizontal track that’s similar to a layer in an image editing program: higher channels are displayed in front of lower ones.

Within each channel, you can create one or more strips, which contain either a segment of video content (a rendered scene, an external video file…) or an effect (color blending, blurring…). The X axis represents time, so the further a strip is placed to the right, the later it will play in the final video.

While a channel can contain multiple strips, they can’t overlap each other. If you want two strips to play at the same time, you need to place them in different channels.

The Channel region sits on the left side of the editor and contains the channel properties listed below. Its visibility can be toggled with View ‣ Channels.

The name of the channel. Double-click to change.

Disable the entire channel so that none of its strips can be seen (or heard) in the final video. Note that you can also mute individual strips.

Lock the entire channel to protect all its strips against accidental changes. Note that you can also lock individual strips.

---

## Display Mode¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/preview/display/display_mode.html

**Contents:**
- Display Mode¶
- Image Preview¶
- Luma Waveform¶
- RGB Parade¶
- Chroma Vectorscope¶
- Histogram¶

Using this pop-up, you can choose between displaying the preview image or a scope that visualizes its color distribution.

Previews what the final video will look like, and lets you change the image layout using various tools.

This scope visualizes the luminosity (brightness) distribution of the image, letting you see at a glance if there’s enough contrast and if any areas are under- or overexposed.

The scope works by plotting a curve for each scanline in the current video frame. Another way of saying this is that each pixel column in the luma waveform is a brightness histogram of the corresponding pixel column in the frame. Specifically:

The horizontal position of a pixel in the waveform refers to a pixel column in the frame.

The vertical position of a pixel in the waveform refers to a brightness value, going from 0 at the bottom to 1 at the top.

The brightness of a pixel in the waveform indicates how many pixels in the above frame column have the above brightness. If no pixels in the frame column have this brightness, the waveform pixel is black. If at least three pixels in the frame column have this brightness, the waveform pixel is white.

When this scope is selected, you have the following option in Sidebar ‣ View ‣ View Settings:

The examples below show two images and their corresponding luma waveforms.

The various horizontal lines in the luma waveform match the uniform-colored lines of the picture. Note that the ‘gray 20%’ one-pixel width line (inside the yellow strip) is represented in the Luma waveform by a gray line. The two lines drawing an “X” are from the two monochrome gradients. Finally, the broken line matches the colored gradient at the bottom.¶

The curves are quite visible. We found a luma of 80-100% for the sky, a luma around 40% for the sea, and a luma of 10-20% for the mountains, growing around 40% for the sunny part.¶

Shows three waveforms – for the red, green, and blue color channels – instead of just one for the overall image brightness.

This scope visualizes the color distribution of the image. Each point has:

An angle indicating its hue.

A distance-from-center indicating its saturation.

A brightness indicating how many pixels in the video frame have the above hue and saturation.

Corresponding Chroma Vectorscope.¶

Shows three overlapping graphs, one for each color channel. Within each graph:

The X axis corresponds to color intensity, going from 0 on the left (black) to 1 on the right (fully red/green/blue).

The Y axis corresponds to number of pixels.

Use this mode to balance out the tonal range in an image. A well-balanced image should have nice and smooth distribution of color values.

Corresponding Histogram.¶

---

## Gizmos¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/preview/display/gizmos.html

**Contents:**
- Gizmos¶

Clicking (Show Gizmo) toggles all gizmos in the Video Sequencer. The drop-down button displays a popover with more detailed settings, which are described below.

Enable/disable the navigation gizmo.

Enable/disable the gizmo of the active tool.

---

## Header¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/preview/header.html

**Contents:**
- Header¶
- View Menu¶
- Select Menu¶
- Strip Menu¶
- Image Menu¶
- Pivot Point¶
- Display Mode¶
- Display Channels¶
- Gizmos¶
- Overlays¶

Header in Preview mode.¶

Show or hide the Toolbar.

Show or hide the Sidebar.

Show or hide the settings for the currently selected tool.

Show or hide the Sidebar.

Show a preview of the start or end frame of a strip while transforming its respective handle.

Reloads external files and refreshes the current frame preview. This is useful when you modified an external file or made a change in a scene that Blender didn’t detect.

Pan and zoom the view to focus on the selected image.

Pan and zoom the view so that the entire video is visible. This enables Zoom to Fit.

Menu with convenient zoom levels and operations. The zoom levels are calculated based on the images resolution compared to the screen resolution.

12.5% (1:8) Numpad8 zoom out to a factor of 12.5%.

25% (1:4) Numpad4 zoom out to a factor of 25%.

50% (1:2) Numpad2 zoom out to a factor of 50%.

100% (1:1) Numpad1 resets the zoom to 100%.

200% (2:1) Ctrl-Numpad2 zoom in to a factor of 200%.

400% (4:1) Ctrl-Numpad4 zoom in to a factor of 400%.

800% (8:1) Ctrl-Numpad8 zoom in to a factor of 800%.

Zooms the view in or out.

Like Frame All, but uses as much space in the editor as possible.

Zoom in the view to the nearest item contained in the border.

As long as this option is enabled, the preview will automatically zoom to keep the video size synchronized with the editor size.

Show the current frame preview as a Render Result where you can save it as an image file.

Save previews of the frames in the scene range (or the preview range, if active) to a video file or a series of image files. See the Output panel for details.

Sequence Render Image and Sequence Render Animation don’t render the final video by default – specifically, they don’t render Scene Strips, instead using the preview’s shading mode (which is initially Solid).

To output a video where the Scene Strips are rendered, use the Render menu in the top-bar, or change Sidebar ‣ View ‣ Scene Strip Display ‣ Shading to Rendered.

Exports Text strips, which can act as subtitles, to a SubRip file (.srt). The exported file contains all Text strips in the video sequence.

Switch the editor mode between Sequencer and Preview.

Area controls. See the user interface documentation for more information.

See Selecting Strips.

See Editing Strips for more information.

Starts mirror operation based on mouse cursor position

Mirrors the image in global X coordinates

Mirrors the image in global Y coordinates

Mirrors the image in local X coordinates

Mirrors the image in local Y coordinates

The Duplicate operator creates a copy of the selected strip(s) and places them in the nearest available channel above the original.

The duplicated content remain selected, allowing immediate repositioning.

Adds selected strips to copy-paste buffer.

Paste strips from copy-paste buffer.

See Insert Keyframe with Keying Set.

See Set Active Keying Set.

See Delete Keyframes.

Reveals all hidden/muted strips.

Mutes the selected strips.

Mutes all strips except for the currently selected strips.

Delete selected strips

Moves the origin of the image strip without changing the strip’s content position.

This is useful for adjusting the reference point for transformations like rotation, scaling, or further positioning. For example, shifting the origin to a corner of the image allows rotations to pivot around that corner, rather than the default center.

Resets the position, rotation, or scale of the selected images.

Resizes the selected images so that they’re as large as possible while still fitting completely inside the video. They don’t get cropped, and their aspect ratio stays the same.

Resizes the selected images to that they fill the entire video space. They may get cropped, but their aspect ratio stays the same.

Resizes the selected images to match the video dimensions. They don’t get cropped, but their aspect ratio may change.

Display the preview image with transparency over a checkerboard pattern.

Ignore the transparency of the preview image (fully transparent areas will be black).

See Sequencer Preview Overlays.

---

## Navigating¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/sequencer/navigating.html

**Contents:**
- Navigating¶
- Header¶
  - View Menu¶
  - Marker Menu¶
  - Sequencer Scene¶
- Playback Controls¶
- Main View¶
  - Adjusting the View¶
  - Playhead¶

Video Sequencer Header.¶

The View menu controls the editor’s view settings.

Show or hide the Toolbar.

Show or hide the Sidebar.

Show or hide the settings for the currently selected tool.

Displays a pop-up panel to alter properties of the last completed operation. See Adjust Last Operation.

Show or hide the Channel Region.

Show or hide the Playback Controls.

Reloads external files and refreshes the current frame preview. This is useful when you modified an external file or made a change in a scene that Blender didn’t detect.

Zooms the display to show only the selected strips.

Zooms the display to show all strips.

Reset the horizontal view to the current scene frame range, taking the preview range into account if it is active.

Centers the horizontal timeline on the current frame.

Click and drag to draw a rectangle and zoom to this rectangle.

Prevents you from panning higher than the highest used channel.

Shows the marker region. When disabled, the Marker menu is also hidden and marker operators are not available in this editor.

Shows seconds instead of frames on the time axis.

Synchronizes the horizontal panning and scale of the editor with other time-based editors that also have this option enabled. That way, they always show the same section of time.

Start or stop animation playback. This will start playback in all editors.

Scrolls the timeline so the current frame is in the center.

Moves the playhead to the nearest strip border (start or end) that’s before the current frame.

Moves the playhead to the nearest strip border (start or end) that’s after the current frame.

Moves the playhead to the nearest strip center that’s before the current frame.

Moves the playhead to the nearest strip center that’s after the current frame.

Interactively define the frame range used for preview playback/rendering.

As long as this range is active, playback will be limited to it, letting you repeatedly view a segment of the video without having to manually rewind each time. It also limits the range that gets rendered by Sequence Render Animation (see below).

Apply a preview range that encompasses the selected strips.

Clears the preview range.

Set the Start frame of the scene to the current frame.

Set the End frame of the scene to the current frame.

Set the Start and End frames of the scene so they encompass the selected strips.

Show the current frame preview as a Render Result where you can save it as an image file.

Save previews of the frames in the scene range (or the preview range, if active) to a video file or a series of image files. See the Output panel for details.

Sequence Render Image and Sequence Render Animation don’t render the final video by default – specifically, they don’t render Scene Strips, instead using the preview’s shading mode (which is initially Solid).

To output a video where the Scene Strips are rendered, use the Render menu in the top-bar, or change Sidebar ‣ View ‣ Scene Strip Display ‣ Shading to Rendered. The latter option is only available if the Video Sequencer is in the Preview or Sequencer & Preview mode.

Exports Text strips, which can act as subtitles, to a SubRip file (.srt). The exported file contains all Text strips in the video sequence.

Switch the editor mode between Sequencer and Preview.

Area controls. See the user interface documentation for more information.

Markers are used to denote frames with key points or significant events within an animation. Like with most animation editors, markers are shown at the bottom of the editor.

Markers in animation editor.¶

See Editing Markers for details.

A data-block menu to select a scene. The Sequencer Scene is the scene that the edit shown in the Sequencer is contained in.

The Playback Controls region contains controls and options related to playback, keying, auto keyframing, and transport.

These settings allow you to:

Control how animations are previewed and synchronized with audio.

Insert and manage keyframes through keying sets and auto keying.

Navigate the timeline using playback and transport controls.

Adjust frame ranges and preview specific segments of the animation.

Set the active scene and time based on the current scene strip. See the workspace settings.

For a detailed description of all properties and controls commonly found in the footer, see the Playback Controls documentation.

Use these shortcuts to adjust the view:

Horizontal scroll: use Ctrl-Wheel, or drag the horizontal scrollbar.

Vertical scroll: use Shift-Wheel, or drag the vertical scrollbar.

Scale view: Ctrl-MMB and drag left/right (horizontal scale) or up/down (vertical scale). Alternatively, you can drag the circles on the scrollbars with LMB.

The Playhead is the blue vertical line with the current time at the top. To see how to interact with it see the Playhead documentation. In addition to that, the Video Sequencer has a special case where if you start dragging on a strip, that strip will be highlighted and displayed solo in the preview (all other strips are temporarily muted).

If scrubbing (or regular playback) performs poorly, you can speed it up by creating proxies.

The current frame is synchronized across all editors, so if you move the Playhead in the Timeline editor for example, it will move in the Video Sequence editor as well (and vice versa).

---

## Proxy¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/sequencer/sidebar/proxy.html

**Contents:**
- Proxy¶
- Proxy Settings¶
- Strip Proxy & Timecode¶

As projects involve increasingly high-resolution footage, the performance of the video preview can decrease drastically. To combat this, Blender can generate proxies – copies of the original footage stored at a lower quality and/or resolution – to maintain a smooth editing experience without compromising visual fidelity in the end result.

The quickest way to set up proxies for videos is to simply select a Proxy Render Size in the View tab (visible when the editor is in Preview or Sequencer & Preview mode). This will automatically enable the selected proxy resolution in all the strips and start generating the downscaled video files.

You can use the Proxy tab if you want to configure proxies in more detail (or create proxies for image sequences).

Sidebar region ‣ Proxy ‣ Proxy Settings

Contains scene-wide proxy settings.

How proxies are stored for the project.

Each strip can specify where to store its proxies (see below).

All proxies are stored in one directory.

The location to store the proxies for the project.

Shows a pop-over that lets you choose the resolution(s) to generate and whether to overwrite existing proxy files. Once you confirm with the Set button, your choices are applied to the selected strips. You can view and tweak the settings for individual strips in the Strip Proxy & Timecode panel (see below).

In the Preview mode, where the Proxy tab is not available, this is instead done through the menu View ‣ Proxy ‣ Setup.

Generates proxies and time indices for the selected strips.

In the Preview mode, where the Proxy tab is not available, this is instead done through the menu View ‣ Proxy ‣ Rebuild.

Sidebar region ‣ Proxy & Timecode ‣ Strip Proxy & Timecode

Contains strip-specific proxy settings. The checkbox in the header can be used to enable/disable proxy generation.

By default, all generated proxy videos are stored to the folder <path of original footage>/BL_proxy/<clip name>, but this can be changed to a custom directory using this option.

Allows you to use preexisting proxies.

The resolution(s) of the proxy videos to generate; multiple sizes can be selected.

Whether to overwrite existing proxy files or keep them.

Controls the level of lossy compression applied to the image, expressed as a percentage. Lossy compression reduces file size by discarding some image data, which may result in a loss of detail.

0%: Maximum compression, producing the smallest file size but the most noticeable quality loss.

100%: No compression, preserving full image quality at the cost of a larger file size.

When you are working with footage directly copied from a camera without preprocessing it, there might be numerous artifacts, mostly due to seeking to a given frame in the sequence. This happens because such footage usually does not have correct frame rate values in the file header. This issue can still arise when the source clip has the same frame rate as the scene settings. In order for Blender to correctly calculate the frames and frame rate there are two possible solutions:

Preprocess your video with e.g. MEncoder to repair the file header and insert the correct keyframes.

Use the Timecode Index option in Blender.

Ignore generated timecodes, seek in movie stream based on calculated timestamp.

Seek based on timestamps read from movie stream, giving the best match between scene and movie times.

Effectively convert movie to an image sequence, ignoring incomplete or dropped frames, and changes in frame rate.

Record Run is the Timecode Index which usually is best to use, but if the source file is totally damaged, Record Run No Gaps will be the only chance of getting an acceptable result.

---

## Sequencer¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/sequencer/index.html

**Contents:**
- Sequencer¶

The Sequencer view type shows a timeline and allows placing and editing strips.

The Sequencer view and its components.¶

---

## Sequencer & Preview¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/sequencer_preview.html

**Contents:**
- Sequencer & Preview¶

This view type shows both the preview and the sequencer inside one editor.

Figure 1: Combined Sequencer & Preview¶

In general, it’s better to avoid this view type and instead have two editors, one serving as the Preview and the other as the Sequencer. Reasons for this include:

Most of the Preview tools, such as Move and Rotate, are not available in Sequencer & Preview.

You can’t add a small editor (such as a File Browser) on the side that only takes up the height of the preview.

You can’t maximize the preview on another screen.

One way of getting two separate editors is to simply open the default Video Editing workspace. (You may need to click the “+” icon to the right of the tabs to find it.)

---

## Sequencer Preview Overlays¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/preview/display/overlays.html

**Contents:**
- Sequencer Preview Overlays¶

Clicking (Show Overlays) toggles all overlays in the Video Sequencer. The drop-down button displays a popover with more detailed settings, which are described below.

Shows an outline around the selected images.

Shows the Frame Overlay for comparing the current frame to a reference frame.

Shows guides indicating the video area where content can be seen across all screens.

---

## Sidebar¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/preview/sidebar.html

**Contents:**
- Sidebar¶
- Tool¶
- View¶
  - View Settings¶
  - 2D Cursor¶
  - Frame Overlay¶
  - Safe Areas¶
  - Scene Strip Display¶
  - Annotations¶
- Metadata¶

The Sidebar can be toggled with the menu item View ‣ Sidebar or with the shortcut N.

The image below shows two Video Sequencers, one in Preview mode and one in Sequencer mode, both with their Sidebar open.

Settings for the active tool.

What to do when dragging LMB on a place other than the tool’s gizmo.

Perform the same action as when dragging the gizmo.

Move the image under the mouse cursor.

Drag a selection rectangle and select all the images that are partially or completely inside it.

Sidebar ‣ View tab ‣ View Settings

Controls the preview resolution. Lower values have worse detail but better performance.

Disable the preview entirely.

Preview at the full resolution without using proxies.

Preview at a downscaled resolution, optionally using proxies (see below). Even selecting 100% can give a performance benefit due to the reduced image quality and corresponding smaller file size.

Enable the use of proxies, which are copies of original footage stored at a lower resolution and/or quality for better preview performance.

Proxies can be configured in the Proxy tab of the Sidebar, which is however only visible in the Sequencer and Sequencer & Preview modes.

Setting this to 0 shows all channels. Setting it to something higher will only show the channels up to and including that number.

Highlight overexposed (bright white) areas using a zebra pattern. The threshold can be adjusted with the slider.

Render missing images/movies with a solid magenta color. When disabled, missing content will render fully transparent.

Strips with missing content will be displayed as red in the timeline.

Sidebar ‣ View tab ‣ 2D Cursor

The 2D Cursor is the white-red circle with a crosshair that is shown in the preview region (provided that the 2D Cursor overlay is enabled). It can be used as a Pivot Point for rotating and scaling images.

The location of the 2D Cursor relative to the center of the video. The edges are 0.5 away, so (0.5, 0.5) is the top right corner.

The 2D Cursor’s location can also be set with the Cursor tool or by dragging with Shift-RMB.

Sidebar ‣ View tab ‣ Frame Overlay

The Frame Overlay lets you display a reference frame for comparing to the current frame.

Lets you drag a rectangle to define the bounds of the overlay. Instead of clicking this button, you can also press O while hovering over the preview.

The time offset between the reference frame and the current frame, in frames.

How the reference frame should be displayed.

Display part of the reference frame (defined by the Overlay Region) on top of the current frame.

Display only the reference frame.

Display only the current frame.

Each Video Sequencer editor can have its own Overlay Type. This means you can open two of them for showing the current frame and the reference frame next to each other.

Keep displaying the same reference frame, even when moving to a different time point. This works by automatically adjusting the Frame Offset.

Sidebar ‣ View tab ‣ Safe Areas

Shows guides indicating the video area where content can be seen across all screens.

Sidebar ‣ View tab ‣ Scene Strip Display

Controls how Scene Strips are displayed in the preview.

The shading mode to use.

Use the Workbench render settings from the current scene rather than the scenes referenced by the strips. Only available for the Wireframe and Solid shading modes.

Sidebar ‣ View tab ‣ Annotations

For managing the Annotations in the Sequencer.

Sidebar ‣ Metadata tab

Lists information that has been encoded in the currently visible movie or image file (not the file referenced by the selected strip). This can include the filename, the creation date, the camera model etc. This also works for images produced by Blender; see Render Output for the metadata that can be included in this case.

Other graphics programs may also store metadata, but only the text in the header field “Comments” can be read.

Some of this metadata can also be made visible in the preview with the Metadata overlay.

The metadata can’t be edited from Blender. Instead, you can use an external program such as exiftool. For example, the command to change the “Comments” field is:

exiftool --comments="My new comment" name-of-file.png

Metadata is only displayed for images/movies that don’t have an effect applied.

---

## Strip¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/sequencer/sidebar/strip.html

**Contents:**
- Strip¶
- Header¶
- Compositing¶
- Transform¶
- Crop¶
- Video¶
- Color¶
- Sound¶
- Time¶
- Source¶

Strip type, represented by an icon.

A text field to adjust the name of the strip, which is shown on the strip in the timeline.

Strips are given a Default Color based on their type; using the color tag, you can assign a custom color to help organize your sequence.

Uncheck to prevent the strip from producing output.

Sidebar ‣ Strip ‣ Compositing

The method for blending the current strip with strips in lower channels. See Blend Modes for more information.

The opacity (alpha) of the strip.

When this property is animated, the opacity is drawn as an overlay on the strip. The overlay will look like a dark section that follows the animation curve. This can be hidden by disabling the F-Curves.

Sidebar ‣ Strip ‣ Transform

The technique used to estimate the values of pixels at non-integer coordinates within the image.

Automatically choose filter based on scaling factor.

No scale, no rotation, integer positions: Nearest

Scaling up by more than 2x: Cubic Mitchell

Scaling down by more than 2x: Box

No interpolation; uses nearest neighboring pixel (fastest).

Interpolate between 2×2 samples.

Cubic Mitchell filter on 4×4 samples.

Cubic B-Spline filter (blurry but no ringing) on 4×4 samples.

Averages source image samples that fall under destination pixel.

Used to move the frames along the X and Y axis.

Scale the image on the X and Y axis.

Rotates the input two-dimensionally along the Z axis.

Mirrors the image along the X axis (left to right) or the Y axis (top to bottom).

Sidebar ‣ Strip ‣ Crop

Used to crop the source image. Use Top, Left, Bottom, and Right to control the number of pixels that are cropped.

Sidebar ‣ Strip ‣ Video

Display every nth frame. For example, if you set this to 10, the strip will only display frames 1, 11, 21, 31, 41… of the source.

It is important to realize that this property is a float value. This allows you to strobe effect synced exactly to a beat.

Plays the strip backwards starting from the last frame in the sequence.

Sidebar ‣ Strip ‣ Color

Adjusts the vividness of colors in the image.

Multiplies the colors by this value. This will increase the brightness.

Multiply alpha along with color channels when using the Multiply option.

Converts input to float data.

Sidebar ‣ Strip ‣ Sound

Working with sound is documented further at Sound Strip.

Adjusts the perceived loudness or intensity of the sound.

When this property is animated, the volume is drawn as an overlay on the strip. The overlay will look like a dark section that follows the animation curve. This can be hidden by disabling the F-Curves. The value is also reflected in the waveform.

Offset of the sound from the beginning of the strip, expressed in seconds.

Mixdown all audio channels into a single channel.

Used to pan the audio between speakers in multichannel audio. Only mono sources can be panned; if the source file is not mono, enable Mono to mix the channels together.

This value basically represents the angle at which it’s played if you multiply the value by 90 degrees.

For stereo, output panning works from left (-1) to center (0) and finally right (1).

To address rear speakers, you can pan to those with higher values, where -2 is back left and 2 is back right.

For smooth animation you can assign values outside the soft bounds, since the angle wraps around over multiple rotations.

The number of audio channels can be configured in the Audio Output settings.

When enabled, this option maintains the original pitch of the audio even when the playback speed of the strip is changed. When disabled, adjusting the playback speed of a sound strip also alters its pitch (for example, slowing down lowers the pitch, and speeding up raises it).

This option is useful when synchronizing audio to video edits or animations that require timing adjustments without affecting tone or musical key.

Display an approximate waveform of the sound file inside of the Sound strip. The waveform reflects strip volume and its animation using keyframes.

Clipping audio, i.e. values over 100% amplitude, will be shown in red.

This option is only visible if the Waveforms overlay is set to Strip.

Sidebar ‣ Strip ‣ Time

The Time panel is used to control source and timeline position of the strip.

Prevents the strip from being moved.

Toggle visibility and selectability of Retiming Keys.

Changes the channel number, or row, of the strip.

Changes the starting frame of the strip, which is the same as selecting and moving the strip.

Changes the length (in frames) of the strip. This works by changing the end frame, which is the same as selecting and moving the strip’s right handle.

Shows the ending time and frame of the strip.

Positive values will move the strip’s handles inwards, making it start later than the start of the source material and stop before its end. This lets you trim down the source material to the part you need. You can enable the Offsets overlay to see the start and end of the full source file.

Negative values will move the strip’s handles outwards, making it start earlier than the start of the source material and stop after its end. This lets you show the first and/or last frame as a frozen image for some time.

Instead of adjusting these offsets in the Sidebar, you can also drag the strip’s handles.

Used for trimming frames off the start/end of the source material. At first sight, this does the same as the Strip Offset properties, but you can in fact combine them to hold (freeze) a frame other than the first or last one. For example, if you set the Hold Offset Start to 10 and the Strip Offset Start to -20, the video will first show the 11th frame of the source for 21 frames, and then play the remaining frames.

The Playhead’s frame number relative to the start of the strip.

Sidebar ‣ Strip ‣ Source

The Source panel shows (and lets you change) the file which the strip points to, as well as how this file should be displayed.

The folder containing the source file for the strip.

The name of the source file. Note that file names are limited to 256 characters.

The color space of the source file.

The list of color spaces depends on the active OCIO config. The default supported color spaces are described in detail here: Default OpenColorIO Configuration

If the source file has an Alpha (transparency) channel, you can choose between Straight Alpha and Premultiplied Alpha.

The video stream to use, in case there are multiple.

Applies deinterlacing to analog video.

Displays information about the strip’s media.

Resolution of the active strip’s image output.

The frame rate encoded into the video file. If this value does not match the scene’s Frame Rate, the perceived speed of the media will be wrong unless the speed is changed to account for the difference.

The directory that contains the source file(s).

The name of the source file. For image sequences, this will be different for each frame.

Opens a File Browser to let you select a new set of images (as an alternative to modifying the above textboxes). Same as Strip ‣ Inputs ‣ Change Paths/Files.

Data-block menu to select a sound.

Path to the file used by the selected sound data-block.

Pack the sound into the blend-file.

Sound file is decoded and loaded into the RAM.

Displays information about the strip’s media.

The number of samples per second the audio is encoded at.

The number of audio channels encoded into the audio stream.

---

## Toolbar¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/preview/toolbar.html

**Contents:**
- Toolbar¶

Select images by dragging a box. All images that intersect the box will be selected.

Select images by dragging a circle. All images that intersect the path of the circle will be selected.

Select images by drawing a lasso.

Lets you move the 2D Cursor by clicking or dragging with LMB.

While dragging, you can press X or Y to constrain movement to an axis.

If you need extra precision, you can hold Shift to move the cursor more slowly than the mouse, or type a number to move it by an exact amount.

The header shows how far the cursor has traveled, including the distance along each axis.

Instead of this tool, you can also drag the mouse while holding Shift-RMB (works with all tools) or adjust the 2D Cursor Location in Sidebar ‣ View.

By default, the 2D Cursor is only shown while dragging it. To make it permanently visible, enable the 2D Cursor overlay.

Lets you move the selected images by dragging with LMB. Alternatively, you can press G, move the mouse, and finally click LMB to confirm (or RMB to cancel).

If the Active Tools gizmo is enabled, you can drag one of the colored arrows to only move along that one axis. You can also press X or Y while moving: press once to constrain to the corresponding global axis, a second time to constrain to the local axis, and a third time to remove the constraint again. Yet another way is to hold MMB and move the mouse horizontally or vertically.

If you need more precision, you can do one of the following while moving:

Hold Shift to move more slowly.

Type a number to move by an exact amount.

The header shows how far the image has moved, including the offset along each axis.

Instead of using this tool, you can also adjust the Position in the Sidebar’s Strip tab (only available in the Sequencer and Sequencer & Preview modes).

Lets you rotate the selected images by holding LMB and moving the mouse in a circle. Alternatively, you can press R, move the mouse, and finally click LMB to confirm (or RMB to cancel).

Images are rotated around the Pivot Point, so if it’s off-center, the images will not just rotate but also move around it.

If you need more precision, you can do one of the following while rotating:

Hold Shift to rotate more slowly.

Hold Ctrl to rotate in increments of 5 degrees.

Type a number to rotate by an exact amount.

The header shows how much the image has rotated.

Instead of using this tool, you can also adjust the Rotation in the Sidebar’s Strip tab (only available in the Sequencer and Sequencer & Preview modes).

Lets you resize the selected images by dragging with LMB. Alternatively, you can press S, move the mouse, and finally click LMB to confirm (or RMB to cancel).

If the Active Tools gizmo is enabled, you can drag one of the colored lines to only scale along that one axis. You can also press X or Y while scaling: press once to constrain to the corresponding global axis, a second time to constrain to the local axis, and a third time to remove the constraint again. Yet another way is to hold MMB and move the mouse horizontally or vertically.

Images are scaled around the Pivot Point, so if it’s off-center and you scale down, the images will not just become smaller but also move towards it.

If you need more precision, you can do one of the following while scaling:

Hold Shift to scale more slowly.

Hold Ctrl to scale in increments of 10%.

Type a number to scale by an exact factor (e.g. .5 to make it half the size).

The header shows the current scale factor.

Instead of using this tool, you can also adjust the Scale in the Sidebar’s Strip tab (only available in the Sequencer and Sequencer & Preview modes).

Lets you move, rotate, and scale images all using one tool.

Drag the cross in the center to move the image.

Drag the dot on the protruding line to rotate.

Drag one of the corners to scale equally along both axes.

Drag one of the sides to scale along just one axis.

Lets you sample a pixel’s color by holding LMB. The editor will show the following information about it on the bottom:

The X and Y coordinates, in pixels relative to the top left corner.

The red, green, blue, and alpha components of the pixel, as decimal values between 0 and 1.

The red, green, and blue components of the pixel with Color Management applied.

The hue, saturation, value, and luminance components of the pixel with Color Management applied.

Sample tool example.¶

Draw free-hand annotations.

Draw a straight line annotation.

Draw a polygon annotation.

Erase previously drawn annotations.

---

## Toolbar¶

**URL:** https://docs.blender.org/manual/en/latest/editors/video_sequencer/sequencer/toolbar.html

**Contents:**
- Toolbar¶

Select strips by dragging a box. All strips that intersect the box will be selected.

Select strips by dragging a circle. All strips that intersect the path of the circle will be selected.

Select strips by drawing a lasso.

Cuts a strip in two. Specifically, it first shortens the strip so it only shows the content up to the cut point, then adds a second strip that shows the content after the cut point.

Splitting be done in two different ways:

Select the tool in the Toolbar and click a strip at the time point where you want to split it.

Alternatively, select one or more strips, place the Playhead at the time point where you want to split them, and press one of the keyboard shortcuts below.

You can choose between the following split types:

After splitting, it’s still possible to restore the cut content in the new strips by dragging their handles.

After splitting, it’s not possible to restore the cut content by dragging handles. However, you can still restore it by changing the Hold Offset in the Sidebar.

Moves only the content of the strip. By default, the tool only allows the content to be moved within strip handles. If this limit applies, the strip outline is drawn in red color. By pressing C the limiting is toggled on or off.

---
