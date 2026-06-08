# Blender - Compositing

**Pages:** 2

---

## Compositor¶

**URL:** https://docs.blender.org/manual/en/latest/editors/compositor.html

**Contents:**
- Compositor¶
- Interface¶
  - Header¶
    - Gizmos¶
  - Asset Shelf¶

The Compositor lets you manage nodes for compositing.

Nodes in the Compositor.¶

The use of the Compositor is explained in Compositing.

Chooses which node group (compositor node tree) to display and edit. Each Scene can have its own compositor node tree. You can also create and switch to custom node groups for reuse.

When enabled, the editor always displays the selected node tree, regardless of the active scene. This is useful when working with multiple scenes but wanting to keep the compositor focused on one node tree.

Controls the display of gizmos in the Compositor.

Clicking (Show Gizmos) toggles all gizmos in the Compositor The drop-down button displays a popover with more detailed settings, which are described below.

Display a context-sensitive gizmo for the currently selected node. This may include transform controls or other visual aids depending on the node type.

The Asset Shelf provides quick access to compositor node assets, allowing users to drag and drop predefined node setups directly into the compositor workspace. Any node group marked as an asset will appear here automatically.

Located at the bottom of the editor, the shelf offers a compact and easily accessible interface for inserting and organizing compositor assets. Compared to the Asset Browser, it integrates more seamlessly into the compositing workflow and can be shown or hidden as needed.

The Asset Shelf helps users:

Quickly build node setups using reusable assets.

Explore common compositing techniques and effects.

Work entirely within Blender for post-processing.

The Asset Shelf can be toggled on or off from the compositor editor’s header.

---

## Spreadsheet¶

**URL:** https://docs.blender.org/manual/en/latest/editors/spreadsheet.html

**Contents:**
- Spreadsheet¶
- Header¶
  - View Menu¶
- Main Region¶
- Data Set Region¶
  - Context Path¶
    - Viewer Path¶
    - Viewer Data¶
  - Geometry¶
  - Domain¶

The Spreadsheet editor is used to inspect the geometry attributes of the active object, typically in order to debug geometry nodes.

The Spreadsheet editor.¶

This option is only available if the object is in Edit Mode. When checked, only data for the selected geometry elements is shown.

Whether to use the filters that are defined in the Sidebar (see below).

Show or hide the tab panel on the left for creating and manipulating markers and masks.

Show or hide the Sidebar.

Display attributes with names starting with a period that are meant for internal use.

Area controls. See the user interface documentation for more information.

The main region displays the attribute data in a spreadsheet format. Each column corresponds to an attribute or data property, and each row represents an element such as a vertex, face, spline, or instance.

Column names and row indices remain visible while scrolling both vertically and horizontally.

Columns can be resized by clicking and dragging the vertical line between columns.

Double clicking the vertical line automatically sizes the column to fit the content.

Columns can be reordered by clicking and dragging the column header.

Tooltips give more detail about the value, depending on the type. For example, Byte Color attributes are displayed as scene linear floats, but the actual integer values are displayed when hovering over the float values, and Matrix attribute values are only displayed in tooltips.

Located on the left, this region controls which data is displayed in the spreadsheet.

Displays the active object name in the panel header.

Clicking one of the arrows between the names to hide the modifier.

Clicking the icon locks the Spreadsheet editor to the currently active object and data path, keeping it visible even if you select another object. Click again to unlock.

Defines which state of the object’s data is displayed:

Shows data with all modifiers applied.

Shows the original object data, without modifiers.

Displays data from the active Viewer Node in Geometry Nodes.

You can also toggle between Evaluated and Viewer Node by clicking the / icon in the Viewer node’s header.

Visible when Object Evaluation State is set to Viewer Node.

Shows the path from the modifier to the active viewer node. If the viewer node is nested inside group nodes, each group will appear in the path.

Visible when Object Evaluation State is set to Viewer Node.

Specifies which Viewer Items from the active Viewer node is displayed in the Spreadsheet Editor.

When a Viewer node outputs multiple data sets (for example, geometry and one or more evaluated fields), each of these appears as a separate Viewer Item. This setting allows choosing which item to display, such as a specific attribute, value field, or geometry component, without changing the Viewer node connection itself.

The available viewer items depend on the currently active Viewer node and its connected inputs. Changing the active viewer or modifying its connections will update this list automatically.

Lets you browse nested geometries (e.g., a mesh inside an instance or a geometry collection).

Lets you choose the attribute domain to display, such as mesh vertices or curve splines.

The number of elements in each domain is shown next to its entry.

When the selected geometry component is a Volume, the Spreadsheet displays detailed information about each grid contained in the volume. Each grid represents a single data field, such as density, color, or velocity, and can be inspected individually to understand its structure and memory usage.

The following information is shown for each grid:

Grid Name – The name of the grid data, such as density or temperature.

Data Type – The type of data stored in the grid, for example Float, Vector, or Boolean.

Class – The grid class, describing its purpose or usage, such as Fog Volume, Level Set, or Level Set.

Extent – The grid’s bounding box in voxel coordinates. Shows the number of voxels in the X, Y, and Z directions.

Voxels – The total number of active voxels in the grid. This includes all voxels that are explicitly stored, even when contained in tiles (e.g., a single leaf tile contains 512 voxels).

Leaf Voxels – The number of active voxels stored in leaf nodes. Unlike Voxels, this count excludes voxels that belong to higher-level tiles.

Tiles – The number of active tiles in the grid. Tiles are higher-level voxel containers used by sparse volume formats (like OpenVDB) to optimize storage.

Size – The estimated memory size of the grid, including all voxel and tile data currently allocated.

These statistics make it possible to analyze the complexity, density, and performance cost of volumetric data produced by Geometry Nodes or imported volume files.

Since volume grids use a sparse data structure, the Extent can be much larger than the actual number of active voxels. Only active regions of the grid are stored in memory, which keeps volume data efficient even for large domains.

In the Sidebar, you can define filters so that only the rows matching these filters are displayed. Click Add Row Filter and set up the properties described below.

Uncheck to temporarily disable the filter.

The name of the column to filter on. If there is no column with the specified name, the filter will be grayed out and ignored.

If you want to filter on an attribute from another domain, you can use the Store Named Attribute Node to create a copy that’s converted to the current domain, then filter on that.

For numerical columns, you can select one of the following comparison operators. Other columns only support Equal To.

Only display rows whose value for the column is equal to the filter value (within the specified threshold).

Only display rows whose value for the column is greater than the filter value.

Only display rows whose value for the column is less than the filter value.

The filter value to compare the row value to.

How much the row’s value is allowed to deviate from the filter value before it is excluded.

The status bar shows how many rows and columns there are, and how many rows remain after filtering.

---
