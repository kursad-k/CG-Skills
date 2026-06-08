# Blender - Files Assets

**Pages:** 1

---

## File Browser¶

**URL:** https://docs.blender.org/manual/en/latest/editors/file_browser.html

**Contents:**
- File Browser¶
- Interface¶
  - Main Region¶
    - Previews¶
  - Directory Region¶
    - Display Settings¶
    - Filter Settings¶
  - Execution Region¶
  - Quick Access Region¶
    - Bookmarks¶

The File Browser is used in all file-related operations. These include:

Opening and saving blend-files.

Browsing the content of other blend-files when appending or linking data-blocks (see Linked Libraries).

Importing from/exporting to other file formats.

Updating the locations of previously imported media (images, videos, fonts…).

The most common way to use this editor is through modal operators (like opening or saving a blend-file). The File Browser will appear in a new window, wait for you to select a file, and then close again.

You can also use the File Browser like a regular, permanently visible editor. In fact, the predefined Video Editing workspace uses it this way. This lets you drag-and-drop media from the browser straight into e.g. the 3D Viewport or the Video Sequencer, saving you some overhead.

The main region lists files, folders, or blend-file contents. Hovering over an item will show a tooltip with extra information.

In its Thumbnail display mode, the File Browser supports many types of previews. These include:

Image and video formats

In order to get previews for data-blocks, these must first be generated. See Blend-Files Previews.

The File Browser in Thumbnail mode.¶

Above the file list, there’s a textbox showing the current folder path, along with buttons for navigating.

Move to previous folder in navigation history.

Move to next folder in navigation history.

Move up to parent directory.

Refresh current folder.

Create a new directory inside the current one.

The current folder path. Tab will auto-complete an existing path. If you type a nonexistent path, you will be prompted to create it.

Filter items by name. The wildcard * will match anything, e.g. bl*er will match both blender and blogger. There is always an implicit wildcard at the start and end of the search text, so blender will also match test_blender_file.blend. This field can also be used to filter some specific file extension (e.g. .png will list all PNG files).

Control how files are displayed.

Displays files and folders in a vertical list.

Displays files and folders in a horizontal list.

The size of the thumbnails.

The number of directory levels to show at once in a flat way.

List only the current directory’s content.

List the whole content of a blend-file (only available when linking or appending data-blocks).

List all subdirectories’ content, one level of recursion.

List all subdirectories’ content, two levels of recursion.

List all subdirectories’ content, three levels of recursion.

Showing several levels of directories at once can be handy to e.g. see your whole collection of textures, even if you have arranged them in a nice set of directories to avoid having hundreds of files in a single place.

In the Append/Link case, showing the content of the whole blend-file lets you link different types of data-blocks in a single operation.

The more levels you show at once, the more time it will take to list them all.

Sorts items by one of the four methods:

Sort the file list alphabetically.

Sort the file list by extension/type.

Sort files by modification time.

The toggle with the funnel icon controls whether filtering is enabled or not. The dropdown button next to it shows the filtering options.

Filters files by categories, like folders, blend-files, images, etc.

When appending or linking, you can also filter by data-block categories, like scenes, animations, materials, etc.

Shows hidden files (starting with a .).

These controls are at the bottom of the editor.

Text field to edit the file name and extension. Turns red to warn you about overwriting an existing file. Tab will auto-complete to existing names in the current directory.

Adds/increases or removes/decreases a trailing number in your file name (used e.g. to store different versions of a file).

Closes the File Browser and cancels the operation.

Confirm the current directory and file name. You can also double-click a file or data-block in the main region.

The region on the left contains a few panels that let you quickly jump to certain directories with a single click.

A custom list of folders that you use often. You can use the buttons to the right of the list to add/remove/move items.

Common directories such as the home directory in Linux or the “Documents” folder in Windows.

Drives and network mounts.

Recently accessed folders.

Clicking the down arrow button to the right reveals Clear Recent Items to fully clear this list.

You can control how many folders appear in this list with the Recent Files number field of the Save & Load tab in the Preferences.

The right region shows the options of the calling operator. Besides the common actions listed below, many import/export add-ons will also expose their options there.

See Opening & Saving.

See Supported Graphics Formats.

See Linked libraries.

For the common option:

The header only contains two menus, one with the standard editor View controls and the other to list a few Selecting operators for the sake of discoverability. These menus are not visible when the browser is in a modal window.

Double-click a directory to enter it.

Takes you up one level of directory.

You can also drag and drop a file or directory from your file manager into the Blender File Browser. This will navigate to the item and select it.

Click LMB to select a single item. Additionally hold Ctrl to add/remove that item to/from the selection, or Shift to select a range of items.

Dragging with LMB starts a box selection.

You can always select several entries in the File Browser – the last selected one is considered the active one. If the calling operation expects a single path (like e.g. the main blend-file Open one), it will get that active item’s path, and the other selected items will be ignored.

It is also possible to select/deselect files by “walking” through them using the arrow keys:

Press an arrow key to select the next/previous file in the list and deselect all the others.

Hold Shift to keep the current selection (and add to it).

Hold Shift-Ctrl to invert the selection as you pass over it.

If no file is selected, the arrow key navigation selects the first or last file in the directory, depending on the arrow direction.

The following operations are available in the file list’s context menu.

Use the operating system to perform an action on the file or directory. The options listed below might not be available on all operating systems.

Create a new file of this type.

Search for files of this type.

Run as specific user.

Show OS Properties for this item.

Search for items in this folder.

Open a command prompt here.

Delete the currently selected files or directories by moving them to the operating system’s “trash”.

Note, on Linux deleting directories requires KDE or GNOME.

Change the name of the currently selected file or directory.

---
