# Godot - Navigation

**Pages:** 6

---

## NavigationPolygon

**URL:** https://docs.godotengine.org/en/stable/classes/class_navigationpolygon.html

**Contents:**
- NavigationPolygon
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: Resource < RefCounted < Object

A 2D navigation mesh that describes a traversable surface for pathfinding.

A navigation mesh can be created either by baking it with the help of the NavigationServer2D, or by adding vertices and convex polygon indices arrays manually.

To bake a navigation mesh at least one outline needs to be added that defines the outer bounds of the baked area.

Adding vertices and polygon indices manually.

Using NavigationMeshes

Navigation Polygon 2D Demo

parsed_collision_mask

sample_partition_type

source_geometry_group_name

&"navigation_polygon_source_geometry_group"

add_outline(outline: PackedVector2Array)

add_outline_at_index(outline: PackedVector2Array, index: int)

add_polygon(polygon: PackedInt32Array)

get_navigation_mesh()

get_outline(idx: int) const

get_outline_count() const

get_parsed_collision_mask_value(layer_number: int) const

get_polygon(idx: int)

get_polygon_count() const

make_polygons_from_outlines()

remove_outline(idx: int)

set_outline(idx: int, outline: PackedVector2Array)

set_parsed_collision_mask_value(layer_number: int, value: bool)

set_vertices(vertices: PackedVector2Array)

enum SamplePartitionType: 🔗

SamplePartitionType SAMPLE_PARTITION_CONVEX_PARTITION = 0

Convex partitioning that yields navigation mesh with convex polygons.

SamplePartitionType SAMPLE_PARTITION_TRIANGULATE = 1

Triangulation partitioning that yields navigation mesh with triangle polygons.

SamplePartitionType SAMPLE_PARTITION_MAX = 2

Represents the size of the SamplePartitionType enum.

enum ParsedGeometryType: 🔗

ParsedGeometryType PARSED_GEOMETRY_MESH_INSTANCES = 0

Parses mesh instances as obstruction geometry. This includes Polygon2D, MeshInstance2D, MultiMeshInstance2D, and TileMap nodes.

Meshes are only parsed when they use a 2D vertices surface format.

ParsedGeometryType PARSED_GEOMETRY_STATIC_COLLIDERS = 1

Parses StaticBody2D and TileMap colliders as obstruction geometry. The collider should be in any of the layers specified by parsed_collision_mask.

ParsedGeometryType PARSED_GEOMETRY_BOTH = 2

Both PARSED_GEOMETRY_MESH_INSTANCES and PARSED_GEOMETRY_STATIC_COLLIDERS.

ParsedGeometryType PARSED_GEOMETRY_MAX = 3

Represents the size of the ParsedGeometryType enum.

enum SourceGeometryMode: 🔗

SourceGeometryMode SOURCE_GEOMETRY_ROOT_NODE_CHILDREN = 0

Scans the child nodes of the root node recursively for geometry.

SourceGeometryMode SOURCE_GEOMETRY_GROUPS_WITH_CHILDREN = 1

Scans nodes in a group and their child nodes recursively for geometry. The group is specified by source_geometry_group_name.

SourceGeometryMode SOURCE_GEOMETRY_GROUPS_EXPLICIT = 2

Uses nodes in a group for geometry. The group is specified by source_geometry_group_name.

SourceGeometryMode SOURCE_GEOMETRY_MAX = 3

Represents the size of the SourceGeometryMode enum.

float agent_radius = 10.0 🔗

void set_agent_radius(value: float)

float get_agent_radius()

The distance to erode/shrink the walkable surface when baking the navigation mesh.

Note: The radius must be equal or higher than 0.0. If the radius is 0.0, it won't be possible to fix invalid outline overlaps and other precision errors during the baking process. As a result, some obstacles may be excluded incorrectly from the final navigation mesh, or may delete the navigation mesh's polygons.

Rect2 baking_rect = Rect2(0, 0, 0, 0) 🔗

void set_baking_rect(value: Rect2)

Rect2 get_baking_rect()

If the baking Rect2 has an area the navigation mesh baking will be restricted to its enclosing area.

Vector2 baking_rect_offset = Vector2(0, 0) 🔗

void set_baking_rect_offset(value: Vector2)

Vector2 get_baking_rect_offset()

The position offset applied to the baking_rect Rect2.

float border_size = 0.0 🔗

void set_border_size(value: float)

float get_border_size()

The size of the non-navigable border around the bake bounding area defined by the baking_rect Rect2.

In conjunction with the baking_rect the border size can be used to bake tile aligned navigation meshes without the tile edges being shrunk by agent_radius.

float cell_size = 1.0 🔗

void set_cell_size(value: float)

float get_cell_size()

The cell size used to rasterize the navigation mesh vertices. Must match with the cell size on the navigation map.

int parsed_collision_mask = 4294967295 🔗

void set_parsed_collision_mask(value: int)

int get_parsed_collision_mask()

The physics layers to scan for static colliders.

Only used when parsed_geometry_type is PARSED_GEOMETRY_STATIC_COLLIDERS or PARSED_GEOMETRY_BOTH.

ParsedGeometryType parsed_geometry_type = 2 🔗

void set_parsed_geometry_type(value: ParsedGeometryType)

ParsedGeometryType get_parsed_geometry_type()

Determines which type of nodes will be parsed as geometry.

SamplePartitionType sample_partition_type = 0 🔗

void set_sample_partition_type(value: SamplePartitionType)

SamplePartitionType get_sample_partition_type()

Partitioning algorithm for creating the navigation mesh polys.

StringName source_geometry_group_name = &"navigation_polygon_source_geometry_group" 🔗

void set_source_geometry_group_name(value: StringName)

StringName get_source_geometry_group_name()

The group name of nodes that should be parsed for baking source geometry.

Only used when source_geometry_mode is SOURCE_GEOMETRY_GROUPS_WITH_CHILDREN or SOURCE_GEOMETRY_GROUPS_EXPLICIT.

SourceGeometryMode source_geometry_mode = 0 🔗

void set_source_geometry_mode(value: SourceGeometryMode)

SourceGeometryMode get_source_geometry_mode()

The source of the geometry used when baking.

void add_outline(outline: PackedVector2Array) 🔗

Appends a PackedVector2Array that contains the vertices of an outline to the internal array that contains all the outlines.

void add_outline_at_index(outline: PackedVector2Array, index: int) 🔗

Adds a PackedVector2Array that contains the vertices of an outline to the internal array that contains all the outlines at a fixed position.

void add_polygon(polygon: PackedInt32Array) 🔗

Adds a polygon using the indices of the vertices you get when calling get_vertices().

Clears the internal arrays for vertices and polygon indices.

void clear_outlines() 🔗

Clears the array of the outlines, but it doesn't clear the vertices and the polygons that were created by them.

void clear_polygons() 🔗

Clears the array of polygons, but it doesn't clear the array of outlines and vertices.

NavigationMesh get_navigation_mesh() 🔗

Returns the NavigationMesh resulting from this navigation polygon. This navigation mesh can be used to update the navigation mesh of a region with the NavigationServer3D.region_set_navigation_mesh() API directly.

PackedVector2Array get_outline(idx: int) const 🔗

Returns a PackedVector2Array containing the vertices of an outline that was created in the editor or by script.

int get_outline_count() const 🔗

Returns the number of outlines that were created in the editor or by script.

bool get_parsed_collision_mask_value(layer_number: int) const 🔗

Returns whether or not the specified layer of the parsed_collision_mask is enabled, given a layer_number between 1 and 32.

PackedInt32Array get_polygon(idx: int) 🔗

Returns a PackedInt32Array containing the indices of the vertices of a created polygon.

int get_polygon_count() const 🔗

Returns the count of all polygons.

PackedVector2Array get_vertices() const 🔗

Returns a PackedVector2Array containing all the vertices being used to create the polygons.

void make_polygons_from_outlines() 🔗

Deprecated: Use NavigationServer2D.parse_source_geometry_data() and NavigationServer2D.bake_from_source_geometry_data() instead.

Creates polygons from the outlines added in the editor or by script.

void remove_outline(idx: int) 🔗

Removes an outline created in the editor or by script. You have to call make_polygons_from_outlines() for the polygons to update.

void set_outline(idx: int, outline: PackedVector2Array) 🔗

Changes an outline created in the editor or by script. You have to call make_polygons_from_outlines() for the polygons to update.

void set_parsed_collision_mask_value(layer_number: int, value: bool) 🔗

Based on value, enables or disables the specified layer in the parsed_collision_mask, given a layer_number between 1 and 32.

void set_vertices(vertices: PackedVector2Array) 🔗

Sets the vertices that can be then indexed to create polygons with the add_polygon() method.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
var new_navigation_mesh = NavigationPolygon.new()
var bounding_outline = PackedVector2Array([Vector2(0, 0), Vector2(0, 50), Vector2(50, 50), Vector2(50, 0)])
new_navigation_mesh.add_outline(bounding_outline)
NavigationServer2D.bake_from_source_geometry_data(new_navigation_mesh, NavigationMeshSourceGeometryData2D.new());
$NavigationRegion2D.navigation_polygon = new_navigation_mesh
```

Example 2 (csharp):
```csharp
var newNavigationMesh = new NavigationPolygon();
Vector2[] boundingOutline = [new Vector2(0, 0), new Vector2(0, 50), new Vector2(50, 50), new Vector2(50, 0)];
newNavigationMesh.AddOutline(boundingOutline);
NavigationServer2D.BakeFromSourceGeometryData(newNavigationMesh, new NavigationMeshSourceGeometryData2D());
GetNode<NavigationRegion2D>("NavigationRegion2D").NavigationPolygon = newNavigationMesh;
```

Example 3 (csharp):
```csharp
var new_navigation_mesh = NavigationPolygon.new()
var new_vertices = PackedVector2Array([Vector2(0, 0), Vector2(0, 50), Vector2(50, 50), Vector2(50, 0)])
new_navigation_mesh.vertices = new_vertices
var new_polygon_indices = PackedInt32Array([0, 1, 2, 3])
new_navigation_mesh.add_polygon(new_polygon_indices)
$NavigationRegion2D.navigation_polygon = new_navigation_mesh
```

Example 4 (csharp):
```csharp
var newNavigationMesh = new NavigationPolygon();
Vector2[] newVertices = [new Vector2(0, 0), new Vector2(0, 50), new Vector2(50, 50), new Vector2(50, 0)];
newNavigationMesh.Vertices = newVertices;
int[] newPolygonIndices = [0, 1, 2, 3];
newNavigationMesh.AddPolygon(newPolygonIndices);
GetNode<NavigationRegion2D>("NavigationRegion2D").NavigationPolygon = newNavigationMesh;
```

---

## Optimizing Navigation Performance

**URL:** https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_optimizing_performance.html

**Contents:**
- Optimizing Navigation Performance
- Performance problems with parsing scene tree nodes
- Performance problems with navigation mesh baking
- Performance problems with NavigationAgent path queries
- Performance problems with the actual path search
- Performance problems with navigation map synchronization
- User-contributed notes

Common Navigation related performance problems can be categorized into the following topics:

Performance problems with parsing scene tree nodes for navigation mesh baking.

Performance problems with baking the actual navigation mesh.

Performance problems with NavigationAgent path queries.

Performance problems with the actual path search.

Performance problems with synchronizing the navigation map.

In the following sections information can be found on how to identify and fix or at least mitigate their impact on framerates.

Prefer using simple shapes with as few edges as possible e.g. nothing rounded like a circle, sphere or torus.

Prefer using physics collision shapes over complex visual meshes as source geometry as meshes need to be copied from the GPU and are commonly much more detailed than necessary.

In general avoid using very complex geometry as source geometry for baking navigation meshes. E.g. never use a very detailed visual mesh, as parsing its shape to data arrays and voxelizing it for the navigation mesh baking will take a long time for no real quality gain on the final navigation mesh. Instead, use a very simplified level of detail version of a shape. Even better, use very primitive shapes like boxes and rectangles that only roughly cover the same geometry but still yield a baked result good enough for pathfinding.

Prefer using simple physics collision shapes over visual meshes, as the source geometry for baking navigation meshes. Physics shapes are by default very limited and optimized shapes that are easy and quick to parse. A visual mesh on the other hand can range from simple to complex. On top, to gain access to visual mesh data the parser needs to request the mesh data arrays from the RenderingServer as visual mesh data is stored directly on the GPU and is not cached on the CPU. This requires locking the RenderingServer thread and can severely impact framerate at runtime while the rendering runs multi-threaded. If the rendering runs single-threaded, the framerate impact might be even worse and the mesh parsing might freeze the entire game for a few seconds on complex meshes.

At runtime, always prefer to use a background thread for baking navigation meshes.

Increase NavigationMesh cell_size and cell_height to create less voxels.

Change the SamplePartitionType from watershed to monotone or layers to gain baking performance.

NEVER scale source geometry with nodes to avoid precision errors. Most scale applies only visually and shapes that are very large at their base scale require still a lot of extra processing even while downscaled.

Baking navigation meshes at runtime should always be done in a background thread if possible. Even small sized navigation meshes can take far longer to bake than what is possible to squeeze into a single frame, at least if the framerate should stay at a bearable level.

Complexity of source geometry data parsed from scene tree nodes has big impact on baking performance as everything needs to be mapped to a grid / voxels. For runtime baking performance the NavigationMesh cell size and cell height should be set as high as possible without causing navigation mesh quality problems for a game. If cell size or cell height is set too low the baking is forced to create an excessive amount of voxels to process the source geometry. If the source geometry spans over a very large game world it is even possible that the baking process runs out of memory in the middle and crashes the game. The partition type can also be lowered depending on how complex the games source geometry is to gain some performance. E.g. games with mostly flat surfaces with blocky geometry can get away with the monotone or layers mode that are a lot faster to bake (e.g. because they require no distance field pass).

Never scale source geometry with nodes. Not only can it result in a lot of precision errors with wrongly matched vertices and edges but also some scaling only exists as visuals and not in the actual parsed data. E.g. if a mesh is downscaled visually in the Editor, e.g. the scale set to 0.001 on a MeshInstance, the mesh still requires a gigantic and very complex voxel grid to be processed for the baking.

Avoid unnecessary path resets and queries every frame in NavigationAgent scripts.

Avoid updating all NavigationAgent paths in the same frame.

Logical errors and wasteful operations in the custom NavigationAgent scripts are very common causes of performance issues, e.g. watch out for resetting the path every single frame. By default NavigationAgents are optimized to only query new paths when the target position changes, the navigation map changes or they are forced too far away from the desired path distance.

E.g. when AI should move to the player, the target position should not be set to the player position every single frame as this queries a new path every frame. Instead, the distance from the current target position to the player position should be compared and only when the player has moved too far away a new target position should be set.

Do not check beforehand if a target position is reachable every frame. What looks like an innocent check is the equivalent of an expensive path query behind the scene. If the plan is to request a new path anyway should the position be reachable, a path should be queried directly. By looking at the last position of the returned path and if that position is in a "reachable" distance to the checked position it answers the "is this position reachable?" question. This avoids doing the equivalent of two full path queries every frame for the same NavigationAgent.

Divide the total number of NavigationAgents into update groups or use random timers so that they do not all request new paths in the same frame.

Optimize overdetailed navigation meshes by reducing the amount of polygons and edges.

The cost of the actual path search correlates directly with the amount of navigation mesh polygons and edges and not the real size of a game world. If a giant game world uses very optimized navigation meshes with only few polygons that cover large areas, performance should be acceptable. If the game world is splintered into very small navigation meshes that each have tiny polygons (like for TileMaps) pathfinding performance will be reduced.

A common problem is a sudden performance drop when a target position is not reachable in a path query. This performance drop is "normal" and the result of a too large, too unoptimized navigation mesh with way to much polygons and edges to search through. In normal path searches where the target position can be reached quickly the pathfinding will do an early exit as soon as the position is reached which can hide this lack of optimization for a while. If the target position can not be reached the pathfinding has to do a far longer search through the available polygons to confirm that the position is absolutely not reachable.

Merge navigation meshes polygons by vertex instead of by edge connection wherever possible.

When changes are made to e.g. navigation meshes or navigation regions, the NavigationServer needs to synchronize the navigation map. Depending on the complexity of navigation meshes, this can take a significant amount of time which may impact the framerate.

The NavigationServer merges navigation meshes either by vertex or by edge connection. The merge by vertex happens when the two vertex of two different edges land in the same map grid cells. This is a rather quick and low-cost operation. The merge by edge connection happens in a second pass for all still unmerged edges. All the free edges are checked for possible edge connections by both distance and angle which is rather costly.

So apart from the general rule to have as few polygon edges as possible, as many edges as possible should be merged by vertex upfront so only a few edges are left for the more costly edge connection calculation. The debug Navigation PerformanceMonitor can be used to get statistics on how many polygons and edges are available and how many of them are unmerged or not merged by vertex. If the ratio between vertex merged and edge connections is way off (vertex should be significantly higher) the navigation meshes are properly created or placed very inefficient.

Please read the User-contributed notes policy before submitting a comment.

---

## Support different actor locomotion

**URL:** https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_different_actor_locomotion.html

**Contents:**
- Support different actor locomotion
- User-contributed notes

To support different actor locomotion like crouching and crawling, a similar map setup as supporting Support different actor types is required.

Bake different navigation meshes with an appropriate height for crouched or crawling actors so they can find paths through those narrow sections in your game world.

When an actor changes locomotion state, e.g. stands up, starts crouching or crawling, query the appropriate map for a path.

If the avoidance behavior should also change with the locomotion e.g. only avoid while standing or only avoid other agents in the same locomotion state, switch the actor's avoidance agent to another avoidance map with each locomotion change.

While a path query can be execute immediately for multiple maps, the avoidance agent map switch will only take effect after the next server synchronization.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (typescript):
```typescript
func update_path():

    if actor_standing:
        path = NavigationServer3D.map_get_path(standing_navigation_map_rid, start_position, target_position, true)
    elif actor_crouching:
        path = NavigationServer3D.map_get_path(crouched_navigation_map_rid, start_position, target_position, true)
    elif actor_crawling:
        path = NavigationServer3D.map_get_path(crawling_navigation_map_rid, start_position, target_position, true)

func change_agent_avoidance_state():

    if actor_standing:
        NavigationServer3D.agent_set_map(avoidance_agent_rid, standing_navigation_map_rid)
    elif actor_crouching:
        NavigationServer3D.agent_set_map(avoidance_agent_rid, crouched_navigation_map_rid)
    elif actor_crawling:
        NavigationServer3D.agent_set_map(avoidance_agent_rid, crawling_navigation_map_rid)
```

Example 2 (json):
```json
private void UpdatePath()
{
    if (_actorStanding)
    {
        _path = NavigationServer3D.MapGetPath(_standingNavigationMapRid, _startPosition, _targetPosition, true);
    }
    else if (_actorCrouching)
    {
        _path = NavigationServer3D.MapGetPath(_crouchedNavigationMapRid, _startPosition, _targetPosition, true);
    }
    else if (_actorCrawling)
    {
        _path = NavigationServer3D.MapGetPath(_crawlingNavigationMapRid, _startPosition, _targetPosition, true);
    }
}

private void ChangeAgentAvoidanceState()
{
    if (_actorStanding)
    {
        NavigationServer3D.AgentSetMap(_avoidanceAgentRid, _standingNavigationMapRid);
    }
    else if (_actorCrouching)
    {
        NavigationServer3D.AgentSetMap(_avoidanceAgentRid, _crouchedNavigationMapRid);
    }
    else if (_actorCrawling)
    {
        NavigationServer3D.AgentSetMap(_avoidanceAgentRid, _crawlingNavigationMapRid);
    }
}
```

---

## Using NavigationAgents

**URL:** https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_using_navigationagents.html

**Contents:**
- Using NavigationAgents
- NavigationAgent Pathfinding
- NavigationAgent Pathfollowing
  - Pathfollowing common problems
- NavigationAgent Avoidance
- NavigationAgent Script Templates
- User-contributed notes

NavigationsAgents are helper nodes that combine functionality for pathfinding, path following and agent avoidance for a Node2D/3D inheriting parent node. They facilitate common calls to the NavigationServer API on behalf of the parent actor node in a more convenient manner for beginners.

2D and 3D version of NavigationAgents are available as NavigationAgent2D and NavigationAgent3D respectively.

New NavigationAgent nodes will automatically join the default navigation map on the World2D/World3D.

NavigationsAgent nodes are optional and not a hard requirement to use the navigation system. Their entire functionality can be replaced with scripts and direct calls to the NavigationServer API.

For more advanced uses consider Using NavigationPathQueryObjects over NavigationAgent nodes.

NavigationAgents query a new navigation path on their current navigation map when their target_position is set with a global position.

The result of the pathfinding can be influenced with the following properties.

The navigation_layers bitmask can be used to limit the navigation meshes that the agent can use.

The pathfinding_algorithm controls how the pathfinding travels through the navigation mesh polygons in the path search.

The path_postprocessing sets if or how the raw path corridor found by the pathfinding is altered before it is returned.

The path_metadata_flags enable the collection of additional path point meta data returned by the path.

The simplify_path and simplify_epsilon properties can be used to remove less critical points from the path.

Disabling path meta flags will disable related signal emissions on the agent.

After a target_position has been set for the agent, the next position to follow in the path can be retrieved with the get_next_path_position() function.

Once the next path position is received, move the parent actor node of the agent towards this path position with your own movement code.

The navigation system never moves the parent node of a NavigationAgent. The movement is entirely in the hands of users and their custom scripts.

NavigationAgents have their own internal logic to proceed with the current path and call for updates.

The get_next_path_position() function is responsible for updating many of the agent's internal states and properties. The function should be repeatedly called once every physics_process until is_navigation_finished() tells that the path is finished. The function should not be called after the target position or path end has been reached as it can make the agent jitter in place due to the repeated path updates. Always check very early in script with is_navigation_finished() if the path is already finished.

The following distance properties influence the path following behavior.

At path_desired_distance from the next path position, the agent advances its internal path index to the subsequent next path position.

At target_desired_distance from the target path position, the agent considers the target position to be reached and the path at its end.

At path_max_distance from the ideal path to the next path position, the agent requests a new path because it was pushed too far off.

The important updates are all triggered with the get_next_path_position() function when called in _physics_process().

NavigationAgents can be used with process but are still limited to a single update that happens in physics_process.

Script examples for various nodes commonly used with NavigationAgents can be found further below.

There are some common user problems and important caveats to consider when writing agent movement scripts.

If an agent queries a path before the navigation map synchronisation, e.g. in a _ready() function, the path might return empty. In this case the get_next_path_position() function will return the same position as the agent parent node and the agent will consider the path end reached. This is fixed by making a deferred call or using a callback e.g. waiting for the navigation map changed signal.

This is usually caused by very frequent path updates every single frame, either deliberate or by accident (e.g. max path distance set too short). The pathfinding needs to find the closest position that are valid on navigation mesh. If a new path is requested every single frame the first path positions might end up switching constantly in front and behind the agent's current position, causing it to dance between the two positions.

If an agent moves very fast it might overshoot the path_desired_distance check without ever advancing the path index. This can lead to the agent backtracking to the path point now behind it until it passes the distance check to increase the path index. Increase the desired distances accordingly for your agent speed and update rate usually fixes this as well as a more balanced navigation mesh polygon layout with not too many polygon edges cramped together in small spaces.

Same as with stuck dancing agents between two positions, this is usually caused by very frequent path updates every single frame. Depending on your navigation mesh layout, and especially when an agent is directly placed over a navigation mesh edge or edge connection, expect path positions to be sometimes slightly "behind" your actors current orientation. This happens due to precision issues and can not always be avoided. This is usually only a visible problem if actors are instantly rotated to face the current path position.

This section explains how to use the navigation avoidance specific to NavigationAgents.

In order for NavigationAgents to use the avoidance feature the avoidance_enabled property must be set to true.

The velocity_computed signal of the NavigationAgent node must be connected to receive the safe velocity calculation result.

Set the velocity of the NavigationAgent node in _physics_process() to update the agent with the current velocity of the agent's parent node.

While avoidance is enabled on the agent the safe_velocity vector will be received with the velocity_computed signal every physics frame. This velocity vector should be used to move the NavigationAgent's parent node in order to avoidance collision with other avoidance using agents or avoidance obstacles.

Only other agents on the same map that are registered for avoidance themself will be considered in the avoidance calculation.

The following NavigationAgent properties are relevant for avoidance:

The property height is available in 3D only. The height together with the current global y-axis position of the agent determines the vertical placement of the agent in the avoidance simulation. Agents using the 2D avoidance will automatically ignore other agents or obstacles that are below or above them.

The property radius controls the size of the avoidance circle, or in case of 3D sphere, around the agent. This area describes the agents body and not the avoidance maneuver distance.

The property neighbor_distance controls the search radius of the agent when searching for other agents that should be avoided. A lower value reduces processing cost.

The property max_neighbors controls how many other agents are considered in the avoidance calculation if they all have overlapping radius. A lower value reduces processing cost but a too low value may result in agents ignoring the avoidance.

The properties time_horizon_agents and time_horizon_obstacles control the avoidance prediction time for other agents or obstacles in seconds. When agents calculate their safe velocities they choose velocities that can be kept for this amount of seconds without colliding with another avoidance object. The prediction time should be kept as low as possible as agents will slow down their velocities to avoid collision in that timeframe.

The property max_speed controls the maximum velocity allowed for the agents avoidance calculation. If the agents parents moves faster than this value the avoidance safe_velocity might not be accurate enough to avoid collision.

The property use_3d_avoidance switches the agent between the 2D avoidance (xz axis) and the 3D avoidance (xyz axis) on the next update. Note that 2D avoidance and 3D avoidance run in separate avoidance simulations so agents split between them do not affect each other.

The properties avoidance_layers and avoidance_mask are bitmasks similar to e.g. physics layers. Agents will only avoid other avoidance objects that are on an avoidance layer that matches at least one of their own avoidance mask bits.

The avoidance_priority makes agents with a higher priority ignore agents with a lower priority. This can be used to give certain agents more importance in the avoidance simulation, e.g. important non-playable characters, without constantly changing their entire avoidance layers or mask.

Avoidance exists in its own space and has no information from navigation meshes or physics collision. Behind the scene avoidance agents are just circles with different radius on a flat 2D plane or spheres in an otherwise empty 3D space. NavigationObstacles can be used to add some environment constrains to the avoidance simulation, see Using NavigationObstacles.

Avoidance does not affect the pathfinding. It should be seen as an additional option for constantly moving objects that cannot be (re)baked to a navigation mesh efficiently in order to move around them.

RVO avoidance makes implicit assumptions about natural agent behavior. E.g. that agents move on reasonable passing sides that can be assigned when they encounter each other. This means that very clinical avoidance test scenarios will commonly fail. E.g. agents moved directly against each other with perfect opposite velocities will fail because the agents can not get their passing sides assigned.

Using the NavigationAgent avoidance_enabled property is the preferred option to toggle avoidance. The following code snippets can be used to toggle avoidance on agents, create or delete avoidance callbacks or switch avoidance modes.

The following sections provides script templates for nodes commonly used with NavigationAgents.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends NavigationAgent2D

func _ready() -> void:
    var agent: RID = get_rid()
    # Enable avoidance
    NavigationServer2D.agent_set_avoidance_enabled(agent, true)
    # Create avoidance callback
    NavigationServer2D.agent_set_avoidance_callback(agent, Callable(self, "_avoidance_done"))

    # Disable avoidance
    NavigationServer2D.agent_set_avoidance_enabled(agent, false)
    # Delete avoidance callback
    NavigationServer2D.agent_set_avoidance_callback(agent, Callable())
```

Example 2 (gdscript):
```gdscript
using Godot;

public partial class MyNavigationAgent2D : NavigationAgent2D
{
    public override void _Ready()
    {
        Rid agent = GetRid();
        // Enable avoidance
        NavigationServer2D.AgentSetAvoidanceEnabled(agent, true);
        // Create avoidance callback
        NavigationServer2D.AgentSetAvoidanceCallback(agent, Callable.From(AvoidanceDone));

        // Disable avoidance
        NavigationServer2D.AgentSetAvoidanceEnabled(agent, false);
        //Delete avoidance callback
        NavigationServer2D.AgentSetAvoidanceCallback(agent, default);
    }

    private void AvoidanceDone() { }
}
```

Example 3 (gdscript):
```gdscript
extends NavigationAgent3D

func _ready() -> void:
    var agent: RID = get_rid()
    # Enable avoidance
    NavigationServer3D.agent_set_avoidance_enabled(agent, true)
    # Create avoidance callback
    NavigationServer3D.agent_set_avoidance_callback(agent, Callable(self, "_avoidance_done"))
    # Switch to 3D avoidance
    NavigationServer3D.agent_set_use_3d_avoidance(agent, true)

    # Disable avoidance
    NavigationServer3D.agent_set_avoidance_enabled(agent, false)
    # Delete avoidance callback
    NavigationServer3D.agent_set_avoidance_callback(agent, Callable())
    # Switch to 2D avoidance
    NavigationServer3D.agent_set_use_3d_avoidance(agent, false)
```

Example 4 (gdscript):
```gdscript
using Godot;

public partial class MyNavigationAgent3D : NavigationAgent3D
{
    public override void _Ready()
    {
        Rid agent = GetRid();
        // Enable avoidance
        NavigationServer3D.AgentSetAvoidanceEnabled(agent, true);
        // Create avoidance callback
        NavigationServer3D.AgentSetAvoidanceCallback(agent, Callable.From(AvoidanceDone));
        // Switch to 3D avoidance
        NavigationServer3D.AgentSetUse3DAvoidance(agent, true);

        // Disable avoidance
        NavigationServer3D.AgentSetAvoidanceEnabled(agent, false);
        //Delete avoidance callback
        NavigationServer3D.AgentSetAvoidanceCallback(agent, default);
        // Switch to 2D avoidance
        NavigationServer3D.AgentSetUse3DAvoidance(agent, false);
    }

    private void AvoidanceDone() { }
}
```

---

## Using NavigationPathQueryObjects

**URL:** https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_using_navigationpathqueryobjects.html

**Contents:**
- Using NavigationPathQueryObjects
- Creating a basic path query
- Path postprocessing options
- Path simplification
- Path metadata
- Excluding or including regions
- Path clipping and limits
- User-contributed notes

Path query parameters expose various options to improve pathfinding performance or lower memory consumption.

They cater to more advanced pathfinding needs that the high-level nodes can not always cover.

See the respective option sections below.

NavigationPathQueryObjects can be used together with NavigationServer.query_path() to obtain a heavily customized navigation path including optional metadata about the path.

This requires more setup compared to obtaining a normal NavigationPath but lets you tailor the pathfinding and provided path data to the different needs of a project.

NavigationPathQueryObjects consist of a pair of objects, a NavigationPathQueryParameters object holding the customization options for the query and a NavigationPathQueryResult that receives (regular) updates with the resulting path and metadata from the query.

2D and 3D versions of NavigationPathQueryParameters are available as NavigationPathQueryParameters2D and NavigationPathQueryParameters3D respectively.

2D and 3D versions of NavigationPathQueryResult are available as NavigationPathQueryResult2D and NavigationPathQueryResult3D respectively.

Both parameters and result are used as a pair with the NavigationServer.query_path() function.

For the available customization options, see further below. See also the descriptions for each parameter in the class reference.

While not a strict requirement, both objects are intended to be created once in advance, stored in a persistent variable for the agent and reused for every followup path query with updated parameters.

Reusing the same objects improves performance when frequently creating objects or allocating memory.

The following script creates the objects and provides a query_path() function to create new navigation paths. The resulting path is identical to using NavigationServer.map_get_path() while reusing the objects.

Path post-processing differences depending on navigation mesh polygon layout.

A path query search travels from the closest navigation mesh polygon edge to the closest edge along the available polygons. If possible it builds a polygon corridor towards the target position polygon.

This raw "search" polygon corridor path is not very optimized and usually a bad fit for agents to travel along. E.g. the closest edge point on a navigation mesh polygon might cause a huge detour for agents on larger polygons. In order to improve the quality of paths returned by the query various path_postprocessing options exist.

The PATH_POSTPROCESSING_CORRIDORFUNNEL post-processing shortens paths by funneling paths around corners inside the available polygon corridor.

This is the default post-processing and usually also the most useful as it gives the shortest path result inside the available polygon corridor. If the polygon corridor is already suboptimal, e.g. due to a suboptimal navigation mesh layout, the funnel can snap to unexpected polygon corners causing detours.

The PATH_POSTPROCESSING_EDGECENTERED post-processing forces all path points to be placed in the middle of the crossed polygon edges inside the available polygon corridor.

This post-processing is usually only useful when used with strictly tile-like navigation mesh polygons that are all evenly sized and where the expected path following is also constrained to cell centers, e.g. typical grid game with movement constrained to grid cell centers.

The PATH_POSTPROCESSING_NONE post-processing returns the path as is how the pathfinding traveled inside the available polygon corridor.

This post-processing is very useful for debug as it shows how the path search traveled from closest edge point to closet edge point and what polygons it picked. A lot of unexpected or suboptimal path results can be immediately explained by looking at this raw path and polygon corridor.

Path simplification can help steering agents or agents that jitter on thin polygon edges.

Path point difference with or without path simplification.

If simplify_path is enabled a variant of the Ramer-Douglas-Peucker path simplification algorithm is applied to the path. This algorithm straightens paths by removing less relevant path points depending on the simplify_epsilon used.

Path simplification helps with all kinds of agent movement problems in "open fields" that are caused by having many unnecessary polygon edges. E.g. a terrain mesh when baked to a navigation mesh can cause an excessive polygon count due to all the small (but for pathfinding almost meaningless) height variations in the terrain.

Path simplification also helps with "steering" agents because they only have more critical corner path points to aim for.

Path simplification is an additional final post-processing of the path. It adds extra performance costs to the query so only enable when actually needed.

Path simplification is exposed on the NavigationServer as a generic function. It can be used outside of navigation queries for all kinds of position arrays as well.

Disabling unneeded path metadata options can improve performance and lower memory consumption.

A path query can return additional metadata for every path point.

The PATH_METADATA_INCLUDE_TYPES flag collects an array with the primitive information about the point owners, e.g. if a point belongs to a region or link.

The PATH_METADATA_INCLUDE_RIDS flag collects an array with the RIDs of the point owners. Depending on point owner primitive, these RIDs can be used with the various NavigationServer functions related to regions or links.

The PATH_METADATA_INCLUDE_OWNERS flag collects an array with the ObjectIDs of the point owners. These object IDs can be used with @GlobalScope.instance_from_id() to retrieve the node behind that object instance, e.g. a NavigationRegion or NavigationLink node.

By default all path metadata is collected as this metadata can be essential for more advanced navigation gameplay.

E.g. to know what path point maps to what object or node owner inside the SceneTree.

E.g. to know if a path point is the start or end of a navigation link that requires scripted takeover.

For the most basic path uses metadata is not always needed. Path metadata collection can be selectively disabled to gain some performance and reduce memory consumption.

Region filters can greatly help with performance on large navigation maps that are region partitioned.

Query parameters allow limiting the pathfinding to specific region navigation meshes.

If a large navigation map is well partitioned into smaller regions this can greatly help with performance as the query can skip a large number of polygons at one of the earliest checks in the path search.

By default and if left empty all regions of the queried navigation map are included.

If a region RID is added to the excluded_regions array the region's navigation mesh will be ignored in the path search.

If a region RID is added to the included_regions array the region's navigation mesh will be considered in the path search and also all other regions not included will be ignored as well.

If a region ends up both included and excluded it is considered excluded.

Region filters are very effective for performance when paired with navigation region chunks that are aligned on a grid. This way the filter can be set to only include the start position chunk and surrounding chunks instead of the entire navigation map.

Even if the target might be outside these surrounding chunks (can always add more "rings") the pathfinding will try to create a path to the polygon closest to the target. This usually creates half-paths heading in the general direction that are good enough, all for a fraction of the performance cost of a full map search.

The following addition to the basic path query script showcases the idea how to integrate a region chunk mapping with the region filters. This is not a full working example.

Sensibly set limits can greatly help with performance on large navigation maps, especially when targets end up being unreachable.

Clipping returned paths to specific distances.

Query parameters allow clipping returned paths to specific lengths. These options clip the path as a part of post-processing. The path is still searched as if at full length, so it will have the same quality. Path length clipping can be helpful in creating paths that better fit constrained gameplay, e.g. tactical games with limited movement ranges.

The path_return_max_length property can be used to clip the returned path to a specific max length.

The path_return_max_radius property can be used to clip the returned path inside a circle (2D) or sphere (3D) radius around the start position.

Query parameters allow limiting the path search to only search up to a specific distance or a specific number of searched polygons. These options are for performance and affect the path search directly.

The path_search_max_distance property can be used to stop the path search when going over this distance from the start position.

The path_search_max_polygons property can be used to stop the path search when going over this searched polygon number.

When the path search is stopped by reaching a limit the path resets and creates a path from the start position polygon to the polygon found so far that is closest to the target position.

While good for performance, if path search limit values are set too low they can affect the path quality very negatively. Depending on polygon layout and search pattern the returned paths might go into completely wrong directions instead of the direction of the target.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
extends Node2D

# Prepare query objects.
var query_parameters := NavigationPathQueryParameters2D.new()
var query_result := NavigationPathQueryResult2D.new()

func query_path(p_start_position: Vector2, p_target_position: Vector2, p_navigation_layers: int = 1) -> PackedVector2Array:
    if not is_inside_tree():
        return PackedVector2Array()

    var map: RID = get_world_2d().get_navigation_map()

    if NavigationServer2D.map_get_iteration_id(map) == 0:
        # This map has never synced and is empty, no point in querying it.
        return PackedVector2Array()

    query_parameters.map = map
    query_parameters.start_position = p_start_position
    query_parameters.target_position = p_target_position
    query_parameters.navigation_layers = p_navigation_layers

    NavigationServer2D.query_path(query_parameters, query_result)
    var path: PackedVector2Array = query_result.get_path()

    return path
```

Example 2 (swift):
```swift
extends Node3D

# Prepare query objects.
var query_parameters := NavigationPathQueryParameters3D.new()
var query_result := NavigationPathQueryResult3D.new()

func query_path(p_start_position: Vector3, p_target_position: Vector3, p_navigation_layers: int = 1) -> PackedVector3Array:
    if not is_inside_tree():
        return PackedVector3Array()

    var map: RID = get_world_3d().get_navigation_map()

    if NavigationServer3D.map_get_iteration_id(map) == 0:
        # This map has never synced and is empty, no point in querying it.
        return PackedVector3Array()

    query_parameters.map = map
    query_parameters.start_position = p_start_position
    query_parameters.target_position = p_target_position
    query_parameters.navigation_layers = p_navigation_layers

    NavigationServer3D.query_path(query_parameters, query_result)
    var path: PackedVector3Array = query_result.get_path()

    return path
```

Example 3 (swift):
```swift
extends Node2D

# ...

var chunk_id_to_region_rid: Dictionary[Vector2i, RID] = {}

func query_path(p_start_position: Vector2, p_target_position: Vector2, p_navigation_layers: int = 1) -> PackedVector2Array:

    # ...

    var regions_around_start_position: Array[RID] = []

    var chunk_rings: int = 1 # Increase for very small regions or more quality.
    var start_chunk_id: Vector2i = floor(p_start_position / float(chunk_size))

    for y: int in range(start_chunk_id.y - chunk_rings, start_chunk_id.y + chunk_rings):
        for x: int in range(start_chunk_id.x - chunk_rings, start_chunk_id.x + chunk_rings):
            var chunk_id: Vector2i = Vector2i(x, y)
            if chunk_id_to_region_rid.has(chunk_id):
                var region: RID = chunk_id_to_region_rid[chunk_id]
                regions_around_start_position.push_back(region)

    query_parameters.included_regions = regions_around_start_position

    # ...
```

Example 4 (swift):
```swift
extends Node3D

# ...

var chunk_id_to_region_rid: Dictionary[Vector3i, RID] = {}

func query_path(p_start_position: Vector3, p_target_position: Vector3, p_navigation_layers: int = 1) -> PackedVector3Array:

    # ...

    var regions_around_start_position: Array[RID] = []

    var chunk_rings: int = 1 # Increase for very small regions or more quality.
    var start_chunk_id: Vector3i = floor(p_start_position / float(chunk_size))
    var y: int = 0 # Assume a planar navigation map for simplicity.

    for z: int in range(start_chunk_id.z - chunk_rings, start_chunk_id.z + chunk_rings):
        for x: int in range(start_chunk_id.x - chunk_rings, start_chunk_id.x + chunk_rings):
            var chunk_id: Vector3i = Vector3i(x, y, z)
            if chunk_id_to_region_rid.has(chunk_id):
                var region: RID = chunk_id_to_region_rid[chunk_id]
                regions_around_start_position.push_back(region)

    query_parameters.included_regions = regions_around_start_position

    # ...
```

---

## Using NavigationServer

**URL:** https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_using_navigationservers.html

**Contents:**
- Using NavigationServer
- Communicating with the NavigationServer
- Threading and Synchronization
- 2D and 3D NavigationServer differences
- Waiting for synchronization
- Server Avoidance Callbacks
- User-contributed notes

2D and 3D version of the NavigationServer are available as NavigationServer2D and NavigationServer3D respectively.

To work with the NavigationServer means to prepare parameters for a query that can be sent to the NavigationServer for updates or requesting data.

To reference the internal NavigationServer objects like maps, regions and agents RIDs are used as identification numbers. Every navigation related node in the scene tree has a function that returns the RID for this node.

The NavigationServer does not update every change immediately but waits until the end of the physics frame to synchronize all the changes together.

Waiting for synchronization is required to apply changes to all maps, regions and agents. Synchronization is done because some updates like a recalculation of the entire navigation map are very expensive and require updated data from all other objects. Also the NavigationServer uses a threadpool by default for some functionality like avoidance calculation between agents.

Waiting is not required for most get() functions that only request data from the NavigationServer without making changes. Note that not all data will account for changes made in the same frame. E.g. if an avoidance agent changed the navigation map this frame the agent_get_map() function will still return the old map before the synchronization. The exception to this are nodes that store their values internally before sending the update to the NavigationServer. When a getter on a node is used for a value that was updated in the same frame it will return the already updated value stored on the node.

The NavigationServer is thread-safe as it places all API calls that want to make changes in a queue to be executed in the synchronization phase. Synchronization for the NavigationServer happens in the middle of the physics frame after scene input from scripts and nodes are all done.

The important takeaway is that most NavigationServer changes take effect after the next physics frame and not immediately. This includes all changes made by navigation related nodes in the scene tree or through scripts.

All setters and delete functions require synchronization.

NavigationServer2D and NavigationServer3D are equivalent in functionality for their dimension.

Technically it is possible to use the tools for creating navigation meshes in one dimension for the other dimension, e.g. baking a 2D navigation mesh with the 3D NavigationMesh when using flat 3D source geometry or creating 3D flat navigation meshes with the polygon outline draw tools of NavigationRegion2D and NavigationPolygons.

At the start of the game, a new scene or procedural navigation changes any path query to a NavigationServer will return empty or wrong.

The navigation map is still empty or not updated at this point. All nodes from the scene tree need to first upload their navigation related data to the NavigationServer. Each added or changed map, region or agent need to be registered with the NavigationServer. Afterward the NavigationServer requires a physics frame for synchronization to update the maps, regions and agents.

One workaround is to make a deferred call to a custom setup function (so all nodes are ready). The setup function makes all the navigation changes, e.g. adding procedural stuff. Afterwards the function waits for the next physics frame before continuing with path queries.

If RVO avoidance agents are registered for avoidance callbacks the NavigationServer dispatches their velocity_computed signals just before the PhysicsServer synchronization.

To learn more about NavigationAgents see Using NavigationAgents.

The simplified order of execution for NavigationAgents that use avoidance:

physics frame starts.

_physics_process(delta).

velocity property is set on NavigationAgent Node.

Agent sends velocity and position to NavigationServer.

NavigationServer waits for synchronization.

NavigationServer synchronizes and computes avoidance velocities for all registered avoidance agents.

NavigationServer sends safe velocity vector with signals for each registered avoidance agents.

Agents receive the signal and move their parent e.g. with move_and_slide or linear_velocity.

PhysicsServer synchronizes.

Therefore moving a physicsbody actor in the callback function with the safe velocity is perfectly thread- and physics-safe as all happens inside the same physics frame before the PhysicsServer commits to changes and does its own calculations.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Node3D

func _ready():
    # Use call deferred to make sure the entire scene tree nodes are setup
    # else await on 'physics_frame' in a _ready() might get stuck.
    custom_setup.call_deferred()

func custom_setup():

    # Create a new navigation map.
    var map: RID = NavigationServer3D.map_create()
    NavigationServer3D.map_set_up(map, Vector3.UP)
    NavigationServer3D.map_set_active(map, true)

    # Create a new navigation region and add it to the map.
    var region: RID = NavigationServer3D.region_create()
    NavigationServer3D.region_set_transform(region, Transform3D())
    NavigationServer3D.region_set_map(region, map)

    # Create a procedural navigation mesh for the region.
    var new_navigation_mesh: NavigationMesh = NavigationMesh.new()
    var vertices: PackedVector3Array = PackedVector3Array([
        Vector3(0, 0, 0),
        Vector3(9.0, 0, 0),
        Vector3(0, 0, 9.0)
    ])
    new_navigation_mesh.set_vertices(vertices)
    var polygon: PackedInt32Array = PackedInt32Array([0, 1, 2])
    new_navigation_mesh.add_polygon(polygon)
    NavigationServer3D.region_set_navigation_mesh(region, new_navigation_mesh)

    # Wait for NavigationServer sync to adapt to made changes.
    await get_tree().physics_frame

    # Query the path from the navigation server.
    var start_position: Vector3 = Vector3(0.1, 0.0, 0.1)
    var target_position: Vector3 = Vector3(1.0, 0.0, 1.0)
    var optimize_path: bool = true

    var path: PackedVector3Array = NavigationServer3D.map_get_path(
        map,
        start_position,
        target_position,
        optimize_path
    )

    print("Found a path!")
    print(path)
```

Example 2 (swift):
```swift
using Godot;

public partial class MyNode3D : Node3D
{
    public override void _Ready()
    {
        // Use call deferred to make sure the entire scene tree nodes are setup
        // else await on 'physics_frame' in a _Ready() might get stuck.
        CallDeferred(MethodName.CustomSetup);
    }

    private async void CustomSetup()
    {
        // Create a new navigation map.
        Rid map = NavigationServer3D.MapCreate();
        NavigationServer3D.MapSetUp(map, Vector3.Up);
        NavigationServer3D.MapSetActive(map, true);

        // Create a new navigation region and add it to the map.
        Rid region = NavigationServer3D.RegionCreate();
        NavigationServer3D.RegionSetTransform(region, Transform3D.Identity);
        NavigationServer3D.RegionSetMap(region, map);

        // Create a procedural navigation mesh for the region.
        var newNavigationMesh = new NavigationMesh()
        {
            Vertices =
            [
                new Vector3(0.0f, 0.0f, 0.0f),
                new Vector3(9.0f, 0.0f, 0.0f),
                new Vector3(0.0f, 0.0f, 9.0f),
            ],
        };
        int[] polygon = [0, 1, 2];
        newNavigationMesh.AddPolygon(polygon);
        NavigationServer3D.RegionSetNavigationMesh(region, newNavigationMesh);

        // Wait for NavigationServer sync to adapt to made changes.
        await ToSignal(GetTree(), SceneTree.SignalName.PhysicsFrame);

        // Query the path from the navigation server.
        var startPosition = new Vector3(0.1f, 0.0f, 0.1f);
        var targetPosition = new Vector3(1.0f, 0.0f, 1.0f);

        Vector3[] path = NavigationServer3D.MapGetPath(map, startPosition, targetPosition, optimize: true);

        GD.Print("Found a path!");
        GD.Print((Variant)path);
    }
}
```

---
