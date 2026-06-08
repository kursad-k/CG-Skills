# Blender - Scripting

**Pages:** 1

---

## Python Console¶

**URL:** https://docs.blender.org/manual/en/latest/editors/python_console.html

**Contents:**
- Python Console¶
- Interface¶
  - Header Menus¶
    - View Menu¶
    - Console Menu¶
  - Main View¶
- Usage¶
  - Aliases¶
  - First Look at the Console Environment¶
  - Auto Completion¶

The Python Console offers a quick way to test code snippets and explore Blender’s API. It executes whatever you type on its >>> prompt and has command history and auto-complete.

Increases/decreases the font size.

Moves the cursor to the beginning of the previous word. If the cursor is in the middle of a word, the cursor is moved to the beginning of the current word.

Moves the cursor to the end of the next word. If the cursor is in the middle of a word, the cursor is moved to the end of the current word.

Moves the cursor to the start of the current line.

Shift-Home: Selects all text between the cursor and the start of the current line.

Moves the cursor to the end of the current line.

Shift-End: Selects all text between the cursor and the end of the current line.

Refreshes the console, giving the view a fresh start. Note that command history is not cleared.

Removes everything from the prompt line.

Deletes everything between the cursor and the beginning of the previous word (separated by periods). If the cursor is in the middle of a word, deletes everything to the beginning of the current word.

Deletes everything between the cursor and the end of the next word. If the cursor is in the middle of a word, deletes everything to the end of the current word.

Copies the full history buffer to the clipboard. This can be pasted into a text file to be used as a Python script.

Copies the selected text into the clipboard and deletes it.

Copies the selected text into the clipboard.

Pastes into the command line.

Inserts a tab character at the cursor.

Unindents the selection.

Changes the current command to the previous one from the command history.

Changes the current command to the next one from the command history.

LMB – Moves the cursor along the input line.

Left / Right – Moves the cursor by one character.

Ctrl-Left / Ctrl-Right – Moves the cursor by one word.

Shift-Left / Shift-Right – Selects characters to the left/right.

Shift-Ctrl-Left / Shift-Ctrl-Right – Selects words to the left/right.

Ctrl-A Selects all text and text history.

Backspace / Delete – Erase characters.

Ctrl-Backspace / Ctrl-Delete – Erase words.

Return – Execute command.

Shift-Return – Add to command history without executing.

Some variables and modules are available for convenience:

C: Quick access to bpy.context.

D: Quick access to bpy.data.

bpy: Top level Blender Python API module.

To see the list of global functions and variables, type dir() and press Return to execute it.

The Console can preview the available members of a module or variable. As an example, type bpy. and press Tab:

The submodules are listed in green. Attributes and methods will be listed in the same way, with methods being indicated by a trailing (.

This module gives you access to the current scene, the currently selected objects, the current object mode, and so on.

For the commands below to show the proper output, make sure you have selected object(s) in the 3D Viewport.

Get the current 3D Viewport mode (Object, Edit, Sculpt, etc.):

Get the active object:

Change the active object’s X coordinate to 1:

Move the active object by 0.5 along the X axis:

Change all three location coordinates in one go:

Change only the X and Y coordinates:

Get the selected objects:

Get the selected objects excluding the active one:

Gives you access to all the data in the blend-file, regardless of whether it’s currently active or selected.

“Operators” are actions that are normally triggered from a button or menu item but can also be called programmatically. See the bpy.ops API documentation for a list of all operators.

**Examples:**

Example 1 (unknown):
```unknown
bpy.context.mode
```

Example 2 (unknown):
```unknown
bpy.context.object
bpy.context.active_object
```

Example 3 (unknown):
```unknown
bpy.context.object.location.x = 1
```

Example 4 (unknown):
```unknown
bpy.context.object.location.x += 0.5
```

---
