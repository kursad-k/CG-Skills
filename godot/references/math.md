# Godot - Math

**Pages:** 20

---

## AABB

**URL:** https://docs.godotengine.org/en/stable/classes/class_aabb.html

**Contents:**
- AABB
- Description
- Tutorials
- Properties
- Constructors
- Methods
- Operators
- Property Descriptions
- Constructor Descriptions
- Method Descriptions

A 3D axis-aligned bounding box.

The AABB built-in Variant type represents an axis-aligned bounding box in a 3D space. It is defined by its position and size, which are Vector3. It is frequently used for fast overlap tests (see intersects()). Although AABB itself is axis-aligned, it can be combined with Transform3D to represent a rotated or skewed bounding box.

It uses floating-point coordinates. The 2D counterpart to AABB is Rect2. There is no version of AABB that uses integer coordinates.

Note: Negative values for size are not supported. With negative size, most AABB methods do not work correctly. Use abs() to get an equivalent AABB with a non-negative size.

Note: In a boolean context, an AABB evaluates to false if both position and size are zero (equal to Vector3.ZERO). Otherwise, it always evaluates to true.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

Math documentation index

AABB(position: Vector3, size: Vector3)

encloses(with: AABB) const

expand(to_point: Vector3) const

get_endpoint(idx: int) const

get_longest_axis() const

get_longest_axis_index() const

get_longest_axis_size() const

get_shortest_axis() const

get_shortest_axis_index() const

get_shortest_axis_size() const

get_support(direction: Vector3) const

grow(by: float) const

has_point(point: Vector3) const

intersection(with: AABB) const

intersects(with: AABB) const

intersects_plane(plane: Plane) const

intersects_ray(from: Vector3, dir: Vector3) const

intersects_segment(from: Vector3, to: Vector3) const

is_equal_approx(aabb: AABB) const

merge(with: AABB) const

operator !=(right: AABB)

operator *(right: Transform3D)

operator ==(right: AABB)

Vector3 end = Vector3(0, 0, 0) 🔗

The ending point. This is usually the corner on the top-right and back of the bounding box, and is equivalent to position + size. Setting this point affects the size.

Vector3 position = Vector3(0, 0, 0) 🔗

The origin point. This is usually the corner on the bottom-left and forward of the bounding box.

Vector3 size = Vector3(0, 0, 0) 🔗

The bounding box's width, height, and depth starting from position. Setting this value also affects the end point.

Note: It's recommended setting the width, height, and depth to non-negative values. This is because most methods in Godot assume that the position is the bottom-left-forward corner, and the end is the top-right-back corner. To get an equivalent bounding box with non-negative size, use abs().

Constructs an AABB with its position and size set to Vector3.ZERO.

AABB AABB(from: AABB)

Constructs an AABB as a copy of the given AABB.

AABB AABB(position: Vector3, size: Vector3)

Constructs an AABB by position and size.

Returns an AABB equivalent to this bounding box, with its width, height, and depth modified to be non-negative values.

Note: It's recommended to use this method when size is negative, as most other methods in Godot assume that the size's components are greater than 0.

bool encloses(with: AABB) const 🔗

Returns true if this bounding box completely encloses the with box. The edges of both boxes are included.

AABB expand(to_point: Vector3) const 🔗

Returns a copy of this bounding box expanded to align the edges with the given to_point, if necessary.

Vector3 get_center() const 🔗

Returns the center point of the bounding box. This is the same as position + (size / 2.0).

Vector3 get_endpoint(idx: int) const 🔗

Returns the position of one of the 8 vertices that compose this bounding box. With an idx of 0 this is the same as position, and an idx of 7 is the same as end.

Vector3 get_longest_axis() const 🔗

Returns the longest normalized axis of this bounding box's size, as a Vector3 (Vector3.RIGHT, Vector3.UP, or Vector3.BACK).

See also get_longest_axis_index() and get_longest_axis_size().

int get_longest_axis_index() const 🔗

Returns the index to the longest axis of this bounding box's size (see Vector3.AXIS_X, Vector3.AXIS_Y, and Vector3.AXIS_Z).

For an example, see get_longest_axis().

float get_longest_axis_size() const 🔗

Returns the longest dimension of this bounding box's size.

For an example, see get_longest_axis().

Vector3 get_shortest_axis() const 🔗

Returns the shortest normalized axis of this bounding box's size, as a Vector3 (Vector3.RIGHT, Vector3.UP, or Vector3.BACK).

See also get_shortest_axis_index() and get_shortest_axis_size().

int get_shortest_axis_index() const 🔗

Returns the index to the shortest axis of this bounding box's size (see Vector3.AXIS_X, Vector3.AXIS_Y, and Vector3.AXIS_Z).

For an example, see get_shortest_axis().

float get_shortest_axis_size() const 🔗

Returns the shortest dimension of this bounding box's size.

For an example, see get_shortest_axis().

Vector3 get_support(direction: Vector3) const 🔗

Returns the vertex's position of this bounding box that's the farthest in the given direction. This point is commonly known as the support point in collision detection algorithms.

float get_volume() const 🔗

Returns the bounding box's volume. This is equivalent to size.x * size.y * size.z. See also has_volume().

AABB grow(by: float) const 🔗

Returns a copy of this bounding box extended on all sides by the given amount by. A negative amount shrinks the box instead.

bool has_point(point: Vector3) const 🔗

Returns true if the bounding box contains the given point. By convention, points exactly on the right, top, and front sides are not included.

Note: This method is not reliable for AABB with a negative size. Use abs() first to get a valid bounding box.

bool has_surface() const 🔗

Returns true if this bounding box has a surface or a length, that is, at least one component of size is greater than 0. Otherwise, returns false.

bool has_volume() const 🔗

Returns true if this bounding box's width, height, and depth are all positive. See also get_volume().

AABB intersection(with: AABB) const 🔗

Returns the intersection between this bounding box and with. If the boxes do not intersect, returns an empty AABB. If the boxes intersect at the edge, returns a flat AABB with no volume (see has_surface() and has_volume()).

Note: If you only need to know whether two bounding boxes are intersecting, use intersects(), instead.

bool intersects(with: AABB) const 🔗

Returns true if this bounding box overlaps with the box with. The edges of both boxes are always excluded.

bool intersects_plane(plane: Plane) const 🔗

Returns true if this bounding box is on both sides of the given plane.

Variant intersects_ray(from: Vector3, dir: Vector3) const 🔗

Returns the first point where this bounding box and the given ray intersect, as a Vector3. If no intersection occurs, returns null.

The ray begin at from, faces dir and extends towards infinity.

Variant intersects_segment(from: Vector3, to: Vector3) const 🔗

Returns the first point where this bounding box and the given segment intersect, as a Vector3. If no intersection occurs, returns null.

The segment begins at from and ends at to.

bool is_equal_approx(aabb: AABB) const 🔗

Returns true if this bounding box and aabb are approximately equal, by calling Vector3.is_equal_approx() on the position and the size.

bool is_finite() const 🔗

Returns true if this bounding box's values are finite, by calling Vector3.is_finite() on the position and the size.

AABB merge(with: AABB) const 🔗

Returns an AABB that encloses both this bounding box and with around the edges. See also encloses().

bool operator !=(right: AABB) 🔗

Returns true if the position or size of both bounding boxes are not equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

AABB operator *(right: Transform3D) 🔗

Inversely transforms (multiplies) the AABB by the given Transform3D transformation matrix, under the assumption that the transformation basis is orthonormal (i.e. rotation/reflection is fine, scaling/skew is not).

aabb * transform is equivalent to transform.inverse() * aabb. See Transform3D.inverse().

For transforming by inverse of an affine transformation (e.g. with scaling) transform.affine_inverse() * aabb can be used instead. See Transform3D.affine_inverse().

bool operator ==(right: AABB) 🔗

Returns true if both position and size of the bounding boxes are exactly equal, respectively.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
var box = AABB(Vector3(5, 0, 5), Vector3(-20, -10, -5))
var absolute = box.abs()
print(absolute.position) # Prints (-15.0, -10.0, 0.0)
print(absolute.size)     # Prints (20.0, 10.0, 5.0)
```

Example 2 (csharp):
```csharp
var box = new Aabb(new Vector3(5, 0, 5), new Vector3(-20, -10, -5));
var absolute = box.Abs();
GD.Print(absolute.Position); // Prints (-15, -10, 0)
GD.Print(absolute.Size);     // Prints (20, 10, 5)
```

Example 3 (csharp):
```csharp
var a = AABB(Vector3(0, 0, 0), Vector3(4, 4, 4))
var b = AABB(Vector3(1, 1, 1), Vector3(3, 3, 3))
var c = AABB(Vector3(2, 2, 2), Vector3(8, 8, 8))

print(a.encloses(a)) # Prints true
print(a.encloses(b)) # Prints true
print(a.encloses(c)) # Prints false
```

Example 4 (csharp):
```csharp
var a = new Aabb(new Vector3(0, 0, 0), new Vector3(4, 4, 4));
var b = new Aabb(new Vector3(1, 1, 1), new Vector3(3, 3, 3));
var c = new Aabb(new Vector3(2, 2, 2), new Vector3(8, 8, 8));

GD.Print(a.Encloses(a)); // Prints True
GD.Print(a.Encloses(b)); // Prints True
GD.Print(a.Encloses(c)); // Prints False
```

---

## Advanced vector math

**URL:** https://docs.godotengine.org/en/stable/tutorials/math/vectors_advanced.html

**Contents:**
- Advanced vector math
- Planes
  - Distance to plane
  - Away from the origin
  - Constructing a plane in 2D
  - Some examples of planes
- Collision detection in 3D
- More information
- User-contributed notes

The dot product has another interesting property with unit vectors. Imagine that perpendicular to that vector (and through the origin) passes a plane. Planes divide the entire space into positive (over the plane) and negative (under the plane), and (contrary to popular belief) you can also use their math in 2D:

Unit vectors that are perpendicular to a surface (so, they describe the orientation of the surface) are called unit normal vectors. Though, usually they are just abbreviated as normals. Normals appear in planes, 3D geometry (to determine where each face or vertex is siding), etc. A normal is a unit vector, but it's called normal because of its usage. (Just like we call (0,0) the Origin!).

The plane passes by the origin and the surface of it is perpendicular to the unit vector (or normal). The side the vector points to is the positive half-space, while the other side is the negative half-space. In 3D this is exactly the same, except that the plane is an infinite surface (imagine an infinite, flat sheet of paper that you can orient and is pinned to the origin) instead of a line.

Now that it's clear what a plane is, let's go back to the dot product. The dot product between a unit vector and any point in space (yes, this time we do dot product between vector and position), returns the distance from the point to the plane:

But not just the absolute distance, if the point is in the negative half space the distance will be negative, too:

This allows us to tell which side of the plane a point is.

I know what you are thinking! So far this is nice, but real planes are everywhere in space, not only passing through the origin. You want real plane action and you want it now.

Remember that planes not only split space in two, but they also have polarity. This means that it is possible to have perfectly overlapping planes, but their negative and positive half-spaces are swapped.

With this in mind, let's describe a full plane as a normal N and a distance from the origin scalar D. Thus, our plane is represented by N and D. For example:

For 3D math, Godot provides a Plane built-in type that handles this.

Basically, N and D can represent any plane in space, be it for 2D or 3D (depending on the amount of dimensions of N) and the math is the same for both. It's the same as before, but D is the distance from the origin to the plane, travelling in N direction. As an example, imagine you want to reach a point in the plane, you will just do:

This will stretch (resize) the normal vector and make it touch the plane. This math might seem confusing, but it's actually much simpler than it seems. If we want to tell, again, the distance from the point to the plane, we do the same but adjusting for distance:

The same thing, using a built-in function:

This will, again, return either a positive or negative distance.

Flipping the polarity of the plane can be done by negating both N and D. This will result in a plane in the same position, but with inverted negative and positive half spaces:

Godot also implements this operator in Plane. So, using the format below will work as expected:

So, remember, the plane's main practical use is that we can calculate the distance to it. So, when is it useful to calculate the distance from a point to a plane? Let's see some examples.

Planes clearly don't come out of nowhere, so they must be built. Constructing them in 2D is easy, this can be done from either a normal (unit vector) and a point, or from two points in space.

In the case of a normal and a point, most of the work is done, as the normal is already computed, so calculate D from the dot product of the normal and the point.

For two points in space, there are actually two planes that pass through them, sharing the same space but with normal pointing to the opposite directions. To compute the normal from the two points, the direction vector must be obtained first, and then it needs to be rotated 90 degrees to either side:

The rest is the same as the previous example. Either point_a or point_b will work, as they are in the same plane:

Doing the same in 3D is a little more complex and is explained further down.

Here is an example of what planes are useful for. Imagine you have a convex polygon. For example, a rectangle, a trapezoid, a triangle, or just any polygon where no faces bend inwards.

For every segment of the polygon, we compute the plane that passes by that segment. Once we have the list of planes, we can do neat things, for example checking if a point is inside the polygon.

We go through all planes, if we can find a plane where the distance to the point is positive, then the point is outside the polygon. If we can't, then the point is inside.

Code should be something like this:

Pretty cool, huh? But this gets much better! With a little more effort, similar logic will let us know when two convex polygons are overlapping too. This is called the Separating Axis Theorem (or SAT) and most physics engines use this to detect collision.

With a point, just checking if a plane returns a positive distance is enough to tell if the point is outside. With another polygon, we must find a plane where all the other polygon points return a positive distance to it. This check is performed with the planes of A against the points of B, and then with the planes of B against the points of A:

Code should be something like this:

As you can see, planes are quite useful, and this is the tip of the iceberg. You might be wondering what happens with non convex polygons. This is usually just handled by splitting the concave polygon into smaller convex polygons, or using a technique such as BSP (which is not used much nowadays).

This is another bonus bit, a reward for being patient and keeping up with this long tutorial. Here is another piece of wisdom. This might not be something with a direct use case (Godot already does collision detection pretty well) but it's used by almost all physics engines and collision detection libraries :)

Remember that converting a convex shape in 2D to an array of 2D planes was useful for collision detection? You could detect if a point was inside any convex shape, or if two 2D convex shapes were overlapping.

Well, this works in 3D too, if two 3D polyhedral shapes are colliding, you won't be able to find a separating plane. If a separating plane is found, then the shapes are definitely not colliding.

To refresh a bit a separating plane means that all vertices of polygon A are in one side of the plane, and all vertices of polygon B are in the other side. This plane is always one of the face-planes of either polygon A or polygon B.

In 3D though, there is a problem to this approach, because it is possible that, in some cases a separating plane can't be found. This is an example of such situation:

To avoid it, some extra planes need to be tested as separators, these planes are the cross product between the edges of polygon A and the edges of polygon B

So the final algorithm is something like:

For more information on using vector math in Godot, see the following article:

Matrices and transforms

If you would like additional explanation, you should check out 3Blue1Brown's excellent video series Essence of Linear Algebra.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var distance = normal.dot(point)
```

Example 2 (gdscript):
```gdscript
var distance = normal.Dot(point);
```

Example 3 (gdscript):
```gdscript
var point_in_plane = N*D
```

Example 4 (gdscript):
```gdscript
var pointInPlane = N * D;
```

---

## Basis

**URL:** https://docs.godotengine.org/en/stable/classes/class_basis.html

**Contents:**
- Basis
- Description
- Tutorials
- Properties
- Constructors
- Methods
- Operators
- Constants
- Property Descriptions
- Constructor Descriptions

A 3×3 matrix for representing 3D rotation and scale.

The Basis built-in Variant type is a 3×3 matrix used to represent 3D rotation, scale, and shear. It is frequently used within a Transform3D.

A Basis is composed by 3 axis vectors, each representing a column of the matrix: x, y, and z. The length of each axis (Vector3.length()) influences the basis's scale, while the direction of all axes influence the rotation. Usually, these axes are perpendicular to one another. However, when you rotate any axis individually, the basis becomes sheared. Applying a sheared basis to a 3D model will make the model appear distorted.

Orthogonal if its axes are perpendicular to each other.

Normalized if the length of every axis is 1.0.

Uniform if all axes share the same length (see get_scale()).

Orthonormal if it is both orthogonal and normalized, which allows it to only represent rotations (see orthonormalized()).

Conformal if it is both orthogonal and uniform, which ensures it is not distorted.

For a general introduction, see the Matrices and transforms tutorial.

Note: Godot uses a right-handed coordinate system, which is a common standard. For directions, the convention for built-in types like Camera3D is for -Z to point forward (+X is right, +Y is up, and +Z is back). Other objects may use different direction conventions. For more information, see the 3D asset direction conventions tutorial.

Note: The basis matrices are exposed as column-major order, which is the same as OpenGL. However, they are stored internally in row-major order, which is the same as DirectX.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

Math documentation index

Matrices and transforms

Matrix Transform Demo

Basis(axis: Vector3, angle: float)

Basis(from: Quaternion)

Basis(x_axis: Vector3, y_axis: Vector3, z_axis: Vector3)

from_euler(euler: Vector3, order: int = 2) static

from_scale(scale: Vector3) static

get_euler(order: int = 2) const

get_rotation_quaternion() const

is_equal_approx(b: Basis) const

looking_at(target: Vector3, up: Vector3 = Vector3(0, 1, 0), use_model_front: bool = false) static

orthonormalized() const

rotated(axis: Vector3, angle: float) const

scaled(scale: Vector3) const

scaled_local(scale: Vector3) const

slerp(to: Basis, weight: float) const

tdotx(with: Vector3) const

tdoty(with: Vector3) const

tdotz(with: Vector3) const

operator !=(right: Basis)

operator *(right: Basis)

operator *(right: Vector3)

operator *(right: float)

operator *(right: int)

operator /(right: float)

operator /(right: int)

operator ==(right: Basis)

operator [](index: int)

IDENTITY = Basis(1, 0, 0, 0, 1, 0, 0, 0, 1) 🔗

The identity Basis. This is an orthonormal basis with no rotation, no shear, and a scale of Vector3.ONE. This also means that:

The x points right (Vector3.RIGHT);

The y points up (Vector3.UP);

The z points back (Vector3.BACK).

If a Vector3 or another Basis is transformed (multiplied) by this constant, no transformation occurs.

Note: In GDScript, this constant is equivalent to creating a Basis without any arguments. It can be used to make your code clearer, and for consistency with C#.

FLIP_X = Basis(-1, 0, 0, 0, 1, 0, 0, 0, 1) 🔗

When any basis is multiplied by FLIP_X, it negates all components of the x axis (the X column).

When FLIP_X is multiplied by any basis, it negates the Vector3.x component of all axes (the X row).

FLIP_Y = Basis(1, 0, 0, 0, -1, 0, 0, 0, 1) 🔗

When any basis is multiplied by FLIP_Y, it negates all components of the y axis (the Y column).

When FLIP_Y is multiplied by any basis, it negates the Vector3.y component of all axes (the Y row).

FLIP_Z = Basis(1, 0, 0, 0, 1, 0, 0, 0, -1) 🔗

When any basis is multiplied by FLIP_Z, it negates all components of the z axis (the Z column).

When FLIP_Z is multiplied by any basis, it negates the Vector3.z component of all axes (the Z row).

Vector3 x = Vector3(1, 0, 0) 🔗

The basis's X axis, and the column 0 of the matrix.

On the identity basis, this vector points right (Vector3.RIGHT).

Vector3 y = Vector3(0, 1, 0) 🔗

The basis's Y axis, and the column 1 of the matrix.

On the identity basis, this vector points up (Vector3.UP).

Vector3 z = Vector3(0, 0, 1) 🔗

The basis's Z axis, and the column 2 of the matrix.

On the identity basis, this vector points back (Vector3.BACK).

Constructs a Basis identical to IDENTITY.

Note: In C#, this constructs a Basis with all of its components set to Vector3.ZERO.

Basis Basis(from: Basis)

Constructs a Basis as a copy of the given Basis.

Basis Basis(axis: Vector3, angle: float)

Constructs a Basis that only represents rotation, rotated around the axis by the given angle, in radians. The axis must be a normalized vector.

Note: This is the same as using rotated() on the IDENTITY basis. With more than one angle consider using from_euler(), instead.

Basis Basis(from: Quaternion)

Constructs a Basis that only represents rotation from the given Quaternion.

Note: Quaternions only store rotation, not scale. Because of this, conversions from Basis to Quaternion cannot always be reversed.

Basis Basis(x_axis: Vector3, y_axis: Vector3, z_axis: Vector3)

Constructs a Basis from 3 axis vectors. These are the columns of the basis matrix.

float determinant() const 🔗

Returns the determinant of this basis's matrix. For advanced math, this number can be used to determine a few attributes:

If the determinant is exactly 0.0, the basis is not invertible (see inverse()).

If the determinant is a negative number, the basis represents a negative scale.

Note: If the basis's scale is the same for every axis, its determinant is always that scale by the power of 3.

Basis from_euler(euler: Vector3, order: int = 2) static 🔗

Constructs a new Basis that only represents rotation from the given Vector3 of Euler angles, in radians.

The Vector3.x should contain the angle around the x axis (pitch);

The Vector3.y should contain the angle around the y axis (yaw);

The Vector3.z should contain the angle around the z axis (roll).

The order of each consecutive rotation can be changed with order (see EulerOrder constants). By default, the YXZ convention is used (@GlobalScope.EULER_ORDER_YXZ): the basis rotates first around the Y axis (yaw), then X (pitch), and lastly Z (roll). When using the opposite method get_euler(), this order is reversed.

Basis from_scale(scale: Vector3) static 🔗

Constructs a new Basis that only represents scale, with no rotation or shear, from the given scale vector.

Note: In linear algebra, the matrix of this basis is also known as a diagonal matrix.

Vector3 get_euler(order: int = 2) const 🔗

Returns this basis's rotation as a Vector3 of Euler angles, in radians. For the returned value:

The Vector3.x contains the angle around the x axis (pitch);

The Vector3.y contains the angle around the y axis (yaw);

The Vector3.z contains the angle around the z axis (roll).

The order of each consecutive rotation can be changed with order (see EulerOrder constants). By default, the YXZ convention is used (@GlobalScope.EULER_ORDER_YXZ): Z (roll) is calculated first, then X (pitch), and lastly Y (yaw). When using the opposite method from_euler(), this order is reversed.

Note: For this method to return correctly, the basis needs to be orthonormal (see orthonormalized()).

Note: Euler angles are much more intuitive but are not suitable for 3D math. Because of this, consider using the get_rotation_quaternion() method instead, which returns a Quaternion.

Note: In the Inspector dock, a basis's rotation is often displayed in Euler angles (in degrees), as is the case with the Node3D.rotation property.

Quaternion get_rotation_quaternion() const 🔗

Returns this basis's rotation as a Quaternion.

Note: Quaternions are much more suitable for 3D math but are less intuitive. For user interfaces, consider using the get_euler() method, which returns Euler angles.

Vector3 get_scale() const 🔗

Returns the length of each axis of this basis, as a Vector3. If the basis is not sheared, this value is the scaling factor. It is not affected by rotation.

Note: If the value returned by determinant() is negative, the scale is also negative.

Basis inverse() const 🔗

Returns the inverse of this basis's matrix.

bool is_conformal() const 🔗

Returns true if this basis is conformal. A conformal basis is both orthogonal (the axes are perpendicular to each other) and uniform (the axes share the same length). This method can be especially useful during physics calculations.

bool is_equal_approx(b: Basis) const 🔗

Returns true if this basis and b are approximately equal, by calling @GlobalScope.is_equal_approx() on all vector components.

bool is_finite() const 🔗

Returns true if this basis is finite, by calling @GlobalScope.is_finite() on all vector components.

Basis looking_at(target: Vector3, up: Vector3 = Vector3(0, 1, 0), use_model_front: bool = false) static 🔗

Creates a new Basis with a rotation such that the forward axis (-Z) points towards the target position.

By default, the -Z axis (camera forward) is treated as forward (implies +X is right). If use_model_front is true, the +Z axis (asset front) is treated as forward (implies +X is left) and points toward the target position.

The up axis (+Y) points as close to the up vector as possible while staying perpendicular to the forward axis. The returned basis is orthonormalized (see orthonormalized()).

The target and the up cannot be Vector3.ZERO, and shouldn't be colinear to avoid unintended rotation around local Z axis.

Basis orthonormalized() const 🔗

Returns the orthonormalized version of this basis. An orthonormal basis is both orthogonal (the axes are perpendicular to each other) and normalized (the axes have a length of 1.0), which also means it can only represent a rotation.

It is often useful to call this method to avoid rounding errors on a rotating basis:

Basis rotated(axis: Vector3, angle: float) const 🔗

Returns a copy of this basis rotated around the given axis by the given angle (in radians).

The axis must be a normalized vector (see Vector3.normalized()). If angle is positive, the basis is rotated counter-clockwise around the axis.

Basis scaled(scale: Vector3) const 🔗

Returns this basis with each axis's components scaled by the given scale's components.

The basis matrix's rows are multiplied by scale's components. This operation is a global scale (relative to the parent).

Basis scaled_local(scale: Vector3) const 🔗

Returns this basis with each axis scaled by the corresponding component in the given scale.

The basis matrix's columns are multiplied by scale's components. This operation is a local scale (relative to self).

Basis slerp(to: Basis, weight: float) const 🔗

Performs a spherical-linear interpolation with the to basis, given a weight. Both this basis and to should represent a rotation.

Example: Smoothly rotate a Node3D to the target basis over time, with a Tween:

float tdotx(with: Vector3) const 🔗

Returns the transposed dot product between with and the x axis (see transposed()).

This is equivalent to basis.x.dot(vector).

float tdoty(with: Vector3) const 🔗

Returns the transposed dot product between with and the y axis (see transposed()).

This is equivalent to basis.y.dot(vector).

float tdotz(with: Vector3) const 🔗

Returns the transposed dot product between with and the z axis (see transposed()).

This is equivalent to basis.z.dot(vector).

Basis transposed() const 🔗

Returns the transposed version of this basis. This turns the basis matrix's columns into rows, and its rows into columns.

bool operator !=(right: Basis) 🔗

Returns true if the components of both Basis matrices are not equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Basis operator *(right: Basis) 🔗

Transforms (multiplies) the right basis by this basis.

This is the operation performed between parent and child Node3Ds.

Vector3 operator *(right: Vector3) 🔗

Transforms (multiplies) the right vector by this basis, returning a Vector3.

Basis operator *(right: float) 🔗

Multiplies all components of the Basis by the given float. This affects the basis's scale uniformly, resizing all 3 axes by the right value.

Basis operator *(right: int) 🔗

Multiplies all components of the Basis by the given int. This affects the basis's scale uniformly, resizing all 3 axes by the right value.

Basis operator /(right: float) 🔗

Divides all components of the Basis by the given float. This affects the basis's scale uniformly, resizing all 3 axes by the right value.

Basis operator /(right: int) 🔗

Divides all components of the Basis by the given int. This affects the basis's scale uniformly, resizing all 3 axes by the right value.

bool operator ==(right: Basis) 🔗

Returns true if the components of both Basis matrices are exactly equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Vector3 operator [](index: int) 🔗

Accesses each axis (column) of this basis by their index. Index 0 is the same as x, index 1 is the same as y, and index 2 is the same as z.

Note: In C++, this operator accesses the rows of the basis matrix, not the columns. For the same behavior as scripting languages, use the set_column and get_column methods.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var basis = Basis.IDENTITY
print("| X | Y | Z")
print("| %.f | %.f | %.f" % [basis.x.x, basis.y.x, basis.z.x])
print("| %.f | %.f | %.f" % [basis.x.y, basis.y.y, basis.z.y])
print("| %.f | %.f | %.f" % [basis.x.z, basis.y.z, basis.z.z])
# Prints:
# | X | Y | Z
# | 1 | 0 | 0
# | 0 | 1 | 0
# | 0 | 0 | 1
```

Example 2 (csharp):
```csharp
# Creates a Basis whose z axis points down.
var my_basis = Basis.from_euler(Vector3(TAU / 4, 0, 0))

print(my_basis.z) # Prints (0.0, -1.0, 0.0)
```

Example 3 (csharp):
```csharp
// Creates a Basis whose z axis points down.
var myBasis = Basis.FromEuler(new Vector3(Mathf.Tau / 4.0f, 0.0f, 0.0f));

GD.Print(myBasis.Z); // Prints (0, -1, 0)
```

Example 4 (csharp):
```csharp
var my_basis = Basis.from_scale(Vector3(2, 4, 8))

print(my_basis.x) # Prints (2.0, 0.0, 0.0)
print(my_basis.y) # Prints (0.0, 4.0, 0.0)
print(my_basis.z) # Prints (0.0, 0.0, 8.0)
```

---

## Beziers, curves and paths

**URL:** https://docs.godotengine.org/en/stable/tutorials/math/beziers_and_curves.html

**Contents:**
- Beziers, curves and paths
- Quadratic Bezier
- Cubic Bezier
- Adding control points
- Curve2D, Curve3D, Path and Path2D
- Evaluating
- Drawing
- Traversal
- User-contributed notes

Bezier curves are a mathematical approximation of natural geometric shapes. We use them to represent a curve with as little information as possible and with a high level of flexibility.

Unlike more abstract mathematical concepts, Bezier curves were created for industrial design. They are a popular tool in the graphics software industry.

They rely on interpolation, which we saw in the previous article, combining multiple steps to create smooth curves. To better understand how Bezier curves work, let's start from its simplest form: Quadratic Bezier.

Take three points, the minimum required for Quadratic Bezier to work:

To draw a curve between them, we first interpolate gradually over the two vertices of each of the two segments formed by the three points, using values ranging from 0 to 1. This gives us two points that move along the segments as we change the value of t from 0 to 1.

We then interpolate q0 and q1 to obtain a single point r that moves along a curve.

This type of curve is called a Quadratic Bezier curve.

(Image credit: Wikipedia)

Building upon the previous example, we can get more control by interpolating between four points.

We first use a function with four parameters to take four points as an input, p0, p1, p2 and p3:

We apply a linear interpolation to each couple of points to reduce them to three:

We then take our three points and reduce them to two:

Here is the full function:

The result will be a smooth curve interpolating between all four points:

(Image credit: Wikipedia)

Cubic Bezier interpolation works the same in 3D, just use Vector3 instead of Vector2.

Building upon Cubic Bezier, we can change the way two of the points work to control the shape of our curve freely. Instead of having p0, p1, p2 and p3, we will store them as:

point0 = p0: Is the first point, the source

control0 = p1 - p0: Is a vector relative to the first control point

control1 = p3 - p2: Is a vector relative to the second control point

point1 = p3: Is the second point, the destination

This way, we have two points and two control points which are relative vectors to the respective points. If you've used graphics or animation software before, this might look familiar:

This is how graphics software presents Bezier curves to the users, and how they work and look in Godot.

There are two objects that contain curves: Curve3D and Curve2D (for 3D and 2D respectively).

They can contain several points, allowing for longer paths. It is also possible to set them to nodes: Path3D and Path2D (also for 3D and 2D respectively):

Using them, however, may not be completely obvious, so following is a description of the most common use cases for Bezier curves.

Only evaluating them may be an option, but in most cases it's not very useful. The big drawback with Bezier curves is that if you traverse them at constant speed, from t = 0 to t = 1, the actual interpolation will not move at constant speed. The speed is also an interpolation between the distances between points p0, p1, p2 and p3 and there is not a mathematically simple way to traverse the curve at constant speed.

Let's do an example with the following pseudocode:

As you can see, the speed (in pixels per second) of the circle varies, even though t is increased at constant speed. This makes beziers difficult to use for anything practical out of the box.

Drawing beziers (or objects based on the curve) is a very common use case, but it's also not easy. For pretty much any case, Bezier curves need to be converted to some sort of segments. This is normally difficult, however, without creating a very high amount of them.

The reason is that some sections of a curve (specifically, corners) may require considerable amounts of points, while other sections may not:

Additionally, if both control points were 0, 0 (remember they are relative vectors), the Bezier curve would just be a straight line (so drawing a high amount of points would be wasteful).

Before drawing Bezier curves, tessellation is required. This is often done with a recursive or divide and conquer function that splits the curve until the curvature amount becomes less than a certain threshold.

The Curve classes provide this via the Curve2D.tessellate() function (which receives optional stages of recursion and angle tolerance arguments). This way, drawing something based on a curve is easier.

The last common use case for the curves is to traverse them. Because of what was mentioned before regarding constant speed, this is also difficult.

To make this easier, the curves need to be baked into equidistant points. This way, they can be approximated with regular interpolation (which can be improved further with a cubic option). To do this, just use the Curve3D.sample_baked() method together with Curve2D.get_baked_length(). The first call to either of them will bake the curve internally.

Traversal at constant speed, then, can be done with the following pseudo-code:

And the output will, then, move at constant speed:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func _quadratic_bezier(p0: Vector2, p1: Vector2, p2: Vector2, t: float):
    var q0 = p0.lerp(p1, t)
    var q1 = p1.lerp(p2, t)
```

Example 2 (csharp):
```csharp
private Vector2 QuadraticBezier(Vector2 p0, Vector2 p1, Vector2 p2, float t)
{
    Vector2 q0 = p0.Lerp(p1, t);
    Vector2 q1 = p1.Lerp(p2, t);
}
```

Example 3 (gdscript):
```gdscript
var r = q0.lerp(q1, t)
return r
```

Example 4 (csharp):
```csharp
Vector2 r = q0.Lerp(q1, t);
return r;
```

---

## FBXState

**URL:** https://docs.godotengine.org/en/stable/classes/class_fbxstate.html

**Contents:**
- FBXState
- Description
- Properties
- Property Descriptions
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: GLTFState < Resource < RefCounted < Object

The FBXState handles the state data imported from FBX files.

allow_geometry_helper_nodes

bool allow_geometry_helper_nodes = false 🔗

void set_allow_geometry_helper_nodes(value: bool)

bool get_allow_geometry_helper_nodes()

If true, the import process used auxiliary nodes called geometry helper nodes. These nodes help preserve the pivots and transformations of the original 3D model during import.

Please read the User-contributed notes policy before submitting a comment.

---

## Interpolation

**URL:** https://docs.godotengine.org/en/stable/tutorials/math/interpolation.html

**Contents:**
- Interpolation
- Vector interpolation
- Transform interpolation
- Smoothing motion
- User-contributed notes

Interpolation is a common operation in graphics programming, which is used to blend or transition between two values. Interpolation can also be used to smooth movement, rotation, etc. It's good to become familiar with it in order to expand your horizons as a game developer.

The basic idea is that you want to transition from A to B. A value t, represents the states in-between.

For example, if t is 0, then the state is A. If t is 1, then the state is B. Anything in-between is an interpolation.

Between two real (floating-point) numbers, an interpolation can be described as:

And often simplified to:

The name of this type of interpolation, which transforms a value into another at constant speed is "linear". So, when you hear about Linear Interpolation, you know they are referring to this formula.

There are other types of interpolations, which will not be covered here. A recommended read afterwards is the Bezier page.

Vector types (Vector2 and Vector3) can also be interpolated, they come with handy functions to do it Vector2.lerp() and Vector3.lerp().

For cubic interpolation, there are also Vector2.cubic_interpolate() and Vector3.cubic_interpolate(), which do a Bezier style interpolation.

Here is example pseudo-code for going from point A to B using interpolation:

It will produce the following motion:

It is also possible to interpolate whole transforms (make sure they have either uniform scale or, at least, the same non-uniform scale). For this, the function Transform3D.interpolate_with() can be used.

Here is an example of transforming a monkey from Position1 to Position2:

Using the following pseudocode:

And again, it will produce the following motion:

Interpolation can be used to smoothly follow a moving target value, such as a position or a rotation. Each frame, lerp() moves the current value towards the target value by a fixed percentage of the remaining difference between the values. The current value will smoothly move towards the target, slowing down as it gets closer. Here is an example of a circle following the mouse using interpolation smoothing:

Here is how it looks:

This is useful for smoothing camera movement, for allies following the player (ensuring they stay within a certain range), and for many other common game patterns.

Despite using delta, the formula used above is framerate-dependent, because the weight parameter of lerp() represents a percentage of the remaining difference in values, not an absolute amount to change. In _physics_process(), this is usually fine because physics is expected to maintain a constant framerate, and therefore delta is expected to remain constant.

For a framerate-independent version of interpolation smoothing that can also be used in process(), use the following formula instead:

Deriving this formula is beyond the scope of this page. For an explanation, see Improved Lerp Smoothing or watch Lerp smoothing is broken.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (unknown):
```unknown
interpolation = A * (1 - t) + B * t
```

Example 2 (unknown):
```unknown
interpolation = A + (B - A) * t
```

Example 3 (gdscript):
```gdscript
var t = 0.0

func _physics_process(delta):
    t += delta * 0.4

    $Sprite2D.position = $A.position.lerp($B.position, t)
```

Example 4 (json):
```json
private float _t = 0.0f;

public override void _PhysicsProcess(double delta)
{
    _t += (float)delta * 0.4f;

    Marker2D a = GetNode<Marker2D>("A");
    Marker2D b = GetNode<Marker2D>("B");
    Sprite2D sprite = GetNode<Sprite2D>("Sprite2D");

    sprite.Position = a.Position.Lerp(b.Position, _t);
}
```

---

## PackedVector2Array

**URL:** https://docs.godotengine.org/en/stable/classes/class_packedvector2array.html

**Contents:**
- PackedVector2Array
- Description
- Tutorials
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A packed array of Vector2s.

An array specifically designed to hold Vector2. Packs data tightly, so it saves memory for large array sizes.

Differences between packed arrays, typed arrays, and untyped arrays: Packed arrays are generally faster to iterate on and modify compared to a typed array of the same type (e.g. PackedVector2Array versus Array[Vector2]). Also, packed arrays consume less memory. As a downside, packed arrays are less flexible as they don't offer as many convenience methods such as Array.map(). Typed arrays are in turn faster to iterate on and modify than untyped arrays.

Note: Packed arrays are always passed by reference. To get a copy of an array that can be modified independently of the original array, use duplicate(). This is not the case for built-in properties and methods. In these cases the returned packed array is a copy, and changing it will not affect the original value. To update a built-in property of this type, modify the returned array and then assign it to the property again.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

Grid-based Navigation with AStarGrid2D Demo

PackedVector2Array(from: PackedVector2Array)

PackedVector2Array(from: Array)

append(value: Vector2)

append_array(array: PackedVector2Array)

bsearch(value: Vector2, before: bool = true)

count(value: Vector2) const

erase(value: Vector2)

find(value: Vector2, from: int = 0) const

get(index: int) const

has(value: Vector2) const

insert(at_index: int, value: Vector2)

push_back(value: Vector2)

remove_at(index: int)

resize(new_size: int)

rfind(value: Vector2, from: int = -1) const

set(index: int, value: Vector2)

slice(begin: int, end: int = 2147483647) const

to_byte_array() const

operator !=(right: PackedVector2Array)

operator *(right: Transform2D)

operator +(right: PackedVector2Array)

operator ==(right: PackedVector2Array)

operator [](index: int)

PackedVector2Array PackedVector2Array() 🔗

Constructs an empty PackedVector2Array.

PackedVector2Array PackedVector2Array(from: PackedVector2Array)

Constructs a PackedVector2Array as a copy of the given PackedVector2Array.

PackedVector2Array PackedVector2Array(from: Array)

Constructs a new PackedVector2Array. Optionally, you can pass in a generic Array that will be converted.

Note: When initializing a PackedVector2Array with elements, it must be initialized with an Array of Vector2 values:

bool append(value: Vector2) 🔗

Appends an element at the end of the array (alias of push_back()).

void append_array(array: PackedVector2Array) 🔗

Appends a PackedVector2Array at the end of this array.

int bsearch(value: Vector2, before: bool = true) 🔗

Finds the index of an existing value (or the insertion index that maintains sorting order, if the value is not yet present in the array) using binary search. Optionally, a before specifier can be passed. If false, the returned index comes after all existing entries of the value in the array.

Note: Calling bsearch() on an unsorted array results in unexpected behavior.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

Clears the array. This is equivalent to using resize() with a size of 0.

int count(value: Vector2) const 🔗

Returns the number of times an element is in the array.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

PackedVector2Array duplicate() 🔗

Creates a copy of the array, and returns it.

bool erase(value: Vector2) 🔗

Removes the first occurrence of a value from the array and returns true. If the value does not exist in the array, nothing happens and false is returned. To remove an element by index, use remove_at() instead.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

void fill(value: Vector2) 🔗

Assigns the given value to all elements in the array. This can typically be used together with resize() to create an array with a given size and initialized elements.

int find(value: Vector2, from: int = 0) const 🔗

Searches the array for a value and returns its index or -1 if not found. Optionally, the initial search index can be passed.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

Vector2 get(index: int) const 🔗

Returns the Vector2 at the given index in the array. If index out-of-bounds or negative, this method fails and returns Vector2(0, 0).

This method is similar (but not identical) to the [] operator. Most notably, when this method fails, it doesn't pause project execution if run from the editor.

bool has(value: Vector2) const 🔗

Returns true if the array contains value.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

int insert(at_index: int, value: Vector2) 🔗

Inserts a new element at a given position in the array. The position must be valid, or at the end of the array (idx == size()).

bool is_empty() const 🔗

Returns true if the array is empty.

bool push_back(value: Vector2) 🔗

Inserts a Vector2 at the end.

void remove_at(index: int) 🔗

Removes an element from the array by index.

int resize(new_size: int) 🔗

Sets the size of the array. If the array is grown, reserves elements at the end of the array. If the array is shrunk, truncates the array to the new size. Calling resize() once and assigning the new values is faster than adding new elements one by one.

Returns @GlobalScope.OK on success, or one of the following Error constants if this method fails: @GlobalScope.ERR_INVALID_PARAMETER if the size is negative, or @GlobalScope.ERR_OUT_OF_MEMORY if allocations fail. Use size() to find the actual size of the array after resize.

Reverses the order of the elements in the array.

int rfind(value: Vector2, from: int = -1) const 🔗

Searches the array in reverse order. Optionally, a start search index can be passed. If negative, the start index is considered relative to the end of the array.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

void set(index: int, value: Vector2) 🔗

Changes the Vector2 at the given index.

Returns the number of elements in the array.

PackedVector2Array slice(begin: int, end: int = 2147483647) const 🔗

Returns the slice of the PackedVector2Array, from begin (inclusive) to end (exclusive), as a new PackedVector2Array.

The absolute value of begin and end will be clamped to the array size, so the default value for end makes it slice to the size of the array by default (i.e. arr.slice(1) is a shorthand for arr.slice(1, arr.size())).

If either begin or end are negative, they will be relative to the end of the array (i.e. arr.slice(0, -2) is a shorthand for arr.slice(0, arr.size() - 2)).

Sorts the elements of the array in ascending order.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

PackedByteArray to_byte_array() const 🔗

Returns a PackedByteArray with each vector encoded as bytes.

bool operator !=(right: PackedVector2Array) 🔗

Returns true if contents of the arrays differ.

PackedVector2Array operator *(right: Transform2D) 🔗

Returns a new PackedVector2Array with all vectors in this array inversely transformed (multiplied) by the given Transform2D transformation matrix, under the assumption that the transformation basis is orthonormal (i.e. rotation/reflection is fine, scaling/skew is not).

array * transform is equivalent to transform.inverse() * array. See Transform2D.inverse().

For transforming by inverse of an affine transformation (e.g. with scaling) transform.affine_inverse() * array can be used instead. See Transform2D.affine_inverse().

PackedVector2Array operator +(right: PackedVector2Array) 🔗

Returns a new PackedVector2Array with contents of right added at the end of this array. For better performance, consider using append_array() instead.

bool operator ==(right: PackedVector2Array) 🔗

Returns true if contents of both arrays are the same, i.e. they have all equal Vector2s at the corresponding indices.

Vector2 operator [](index: int) 🔗

Returns the Vector2 at index index. Negative indices can be used to access the elements starting from the end. Using index out of array's bounds will result in an error.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
var array = PackedVector2Array([Vector2(12, 34), Vector2(56, 78)])
```

---

## PackedVector3Array

**URL:** https://docs.godotengine.org/en/stable/classes/class_packedvector3array.html

**Contents:**
- PackedVector3Array
- Description
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A packed array of Vector3s.

An array specifically designed to hold Vector3. Packs data tightly, so it saves memory for large array sizes.

Differences between packed arrays, typed arrays, and untyped arrays: Packed arrays are generally faster to iterate on and modify compared to a typed array of the same type (e.g. PackedVector3Array versus Array[Vector3]). Also, packed arrays consume less memory. As a downside, packed arrays are less flexible as they don't offer as many convenience methods such as Array.map(). Typed arrays are in turn faster to iterate on and modify than untyped arrays.

Note: Packed arrays are always passed by reference. To get a copy of an array that can be modified independently of the original array, use duplicate(). This is not the case for built-in properties and methods. In these cases the returned packed array is a copy, and changing it will not affect the original value. To update a built-in property of this type, modify the returned array and then assign it to the property again.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

PackedVector3Array(from: PackedVector3Array)

PackedVector3Array(from: Array)

append(value: Vector3)

append_array(array: PackedVector3Array)

bsearch(value: Vector3, before: bool = true)

count(value: Vector3) const

erase(value: Vector3)

find(value: Vector3, from: int = 0) const

get(index: int) const

has(value: Vector3) const

insert(at_index: int, value: Vector3)

push_back(value: Vector3)

remove_at(index: int)

resize(new_size: int)

rfind(value: Vector3, from: int = -1) const

set(index: int, value: Vector3)

slice(begin: int, end: int = 2147483647) const

to_byte_array() const

operator !=(right: PackedVector3Array)

operator *(right: Transform3D)

operator +(right: PackedVector3Array)

operator ==(right: PackedVector3Array)

operator [](index: int)

PackedVector3Array PackedVector3Array() 🔗

Constructs an empty PackedVector3Array.

PackedVector3Array PackedVector3Array(from: PackedVector3Array)

Constructs a PackedVector3Array as a copy of the given PackedVector3Array.

PackedVector3Array PackedVector3Array(from: Array)

Constructs a new PackedVector3Array. Optionally, you can pass in a generic Array that will be converted.

Note: When initializing a PackedVector3Array with elements, it must be initialized with an Array of Vector3 values:

bool append(value: Vector3) 🔗

Appends an element at the end of the array (alias of push_back()).

void append_array(array: PackedVector3Array) 🔗

Appends a PackedVector3Array at the end of this array.

int bsearch(value: Vector3, before: bool = true) 🔗

Finds the index of an existing value (or the insertion index that maintains sorting order, if the value is not yet present in the array) using binary search. Optionally, a before specifier can be passed. If false, the returned index comes after all existing entries of the value in the array.

Note: Calling bsearch() on an unsorted array results in unexpected behavior.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

Clears the array. This is equivalent to using resize() with a size of 0.

int count(value: Vector3) const 🔗

Returns the number of times an element is in the array.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

PackedVector3Array duplicate() 🔗

Creates a copy of the array, and returns it.

bool erase(value: Vector3) 🔗

Removes the first occurrence of a value from the array and returns true. If the value does not exist in the array, nothing happens and false is returned. To remove an element by index, use remove_at() instead.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

void fill(value: Vector3) 🔗

Assigns the given value to all elements in the array. This can typically be used together with resize() to create an array with a given size and initialized elements.

int find(value: Vector3, from: int = 0) const 🔗

Searches the array for a value and returns its index or -1 if not found. Optionally, the initial search index can be passed.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

Vector3 get(index: int) const 🔗

Returns the Vector3 at the given index in the array. If index out-of-bounds or negative, this method fails and returns Vector3(0, 0, 0).

This method is similar (but not identical) to the [] operator. Most notably, when this method fails, it doesn't pause project execution if run from the editor.

bool has(value: Vector3) const 🔗

Returns true if the array contains value.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

int insert(at_index: int, value: Vector3) 🔗

Inserts a new element at a given position in the array. The position must be valid, or at the end of the array (idx == size()).

bool is_empty() const 🔗

Returns true if the array is empty.

bool push_back(value: Vector3) 🔗

Inserts a Vector3 at the end.

void remove_at(index: int) 🔗

Removes an element from the array by index.

int resize(new_size: int) 🔗

Sets the size of the array. If the array is grown, reserves elements at the end of the array. If the array is shrunk, truncates the array to the new size. Calling resize() once and assigning the new values is faster than adding new elements one by one.

Returns @GlobalScope.OK on success, or one of the following Error constants if this method fails: @GlobalScope.ERR_INVALID_PARAMETER if the size is negative, or @GlobalScope.ERR_OUT_OF_MEMORY if allocations fail. Use size() to find the actual size of the array after resize.

Reverses the order of the elements in the array.

int rfind(value: Vector3, from: int = -1) const 🔗

Searches the array in reverse order. Optionally, a start search index can be passed. If negative, the start index is considered relative to the end of the array.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

void set(index: int, value: Vector3) 🔗

Changes the Vector3 at the given index.

Returns the number of elements in the array.

PackedVector3Array slice(begin: int, end: int = 2147483647) const 🔗

Returns the slice of the PackedVector3Array, from begin (inclusive) to end (exclusive), as a new PackedVector3Array.

The absolute value of begin and end will be clamped to the array size, so the default value for end makes it slice to the size of the array by default (i.e. arr.slice(1) is a shorthand for arr.slice(1, arr.size())).

If either begin or end are negative, they will be relative to the end of the array (i.e. arr.slice(0, -2) is a shorthand for arr.slice(0, arr.size() - 2)).

Sorts the elements of the array in ascending order.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

PackedByteArray to_byte_array() const 🔗

Returns a PackedByteArray with each vector encoded as bytes.

bool operator !=(right: PackedVector3Array) 🔗

Returns true if contents of the arrays differ.

PackedVector3Array operator *(right: Transform3D) 🔗

Returns a new PackedVector3Array with all vectors in this array inversely transformed (multiplied) by the given Transform3D transformation matrix, under the assumption that the transformation basis is orthonormal (i.e. rotation/reflection is fine, scaling/skew is not).

array * transform is equivalent to transform.inverse() * array. See Transform3D.inverse().

For transforming by inverse of an affine transformation (e.g. with scaling) transform.affine_inverse() * array can be used instead. See Transform3D.affine_inverse().

PackedVector3Array operator +(right: PackedVector3Array) 🔗

Returns a new PackedVector3Array with contents of right added at the end of this array. For better performance, consider using append_array() instead.

bool operator ==(right: PackedVector3Array) 🔗

Returns true if contents of both arrays are the same, i.e. they have all equal Vector3s at the corresponding indices.

Vector3 operator [](index: int) 🔗

Returns the Vector3 at index index. Negative indices can be used to access the elements starting from the end. Using index out of array's bounds will result in an error.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
var array = PackedVector3Array([Vector3(12, 34, 56), Vector3(78, 90, 12)])
```

---

## PackedVector4Array

**URL:** https://docs.godotengine.org/en/stable/classes/class_packedvector4array.html

**Contents:**
- PackedVector4Array
- Description
- Constructors
- Methods
- Operators
- Constructor Descriptions
- Method Descriptions
- Operator Descriptions
- User-contributed notes

A packed array of Vector4s.

An array specifically designed to hold Vector4. Packs data tightly, so it saves memory for large array sizes.

Differences between packed arrays, typed arrays, and untyped arrays: Packed arrays are generally faster to iterate on and modify compared to a typed array of the same type (e.g. PackedVector4Array versus Array[Vector4]). Also, packed arrays consume less memory. As a downside, packed arrays are less flexible as they don't offer as many convenience methods such as Array.map(). Typed arrays are in turn faster to iterate on and modify than untyped arrays.

Note: Packed arrays are always passed by reference. To get a copy of an array that can be modified independently of the original array, use duplicate(). This is not the case for built-in properties and methods. In these cases the returned packed array is a copy, and changing it will not affect the original value. To update a built-in property of this type, modify the returned array and then assign it to the property again.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

PackedVector4Array(from: PackedVector4Array)

PackedVector4Array(from: Array)

append(value: Vector4)

append_array(array: PackedVector4Array)

bsearch(value: Vector4, before: bool = true)

count(value: Vector4) const

erase(value: Vector4)

find(value: Vector4, from: int = 0) const

get(index: int) const

has(value: Vector4) const

insert(at_index: int, value: Vector4)

push_back(value: Vector4)

remove_at(index: int)

resize(new_size: int)

rfind(value: Vector4, from: int = -1) const

set(index: int, value: Vector4)

slice(begin: int, end: int = 2147483647) const

to_byte_array() const

operator !=(right: PackedVector4Array)

operator +(right: PackedVector4Array)

operator ==(right: PackedVector4Array)

operator [](index: int)

PackedVector4Array PackedVector4Array() 🔗

Constructs an empty PackedVector4Array.

PackedVector4Array PackedVector4Array(from: PackedVector4Array)

Constructs a PackedVector4Array as a copy of the given PackedVector4Array.

PackedVector4Array PackedVector4Array(from: Array)

Constructs a new PackedVector4Array. Optionally, you can pass in a generic Array that will be converted.

Note: When initializing a PackedVector4Array with elements, it must be initialized with an Array of Vector4 values:

bool append(value: Vector4) 🔗

Appends an element at the end of the array (alias of push_back()).

void append_array(array: PackedVector4Array) 🔗

Appends a PackedVector4Array at the end of this array.

int bsearch(value: Vector4, before: bool = true) 🔗

Finds the index of an existing value (or the insertion index that maintains sorting order, if the value is not yet present in the array) using binary search. Optionally, a before specifier can be passed. If false, the returned index comes after all existing entries of the value in the array.

Note: Calling bsearch() on an unsorted array results in unexpected behavior.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

Clears the array. This is equivalent to using resize() with a size of 0.

int count(value: Vector4) const 🔗

Returns the number of times an element is in the array.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

PackedVector4Array duplicate() 🔗

Creates a copy of the array, and returns it.

bool erase(value: Vector4) 🔗

Removes the first occurrence of a value from the array and returns true. If the value does not exist in the array, nothing happens and false is returned. To remove an element by index, use remove_at() instead.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

void fill(value: Vector4) 🔗

Assigns the given value to all elements in the array. This can typically be used together with resize() to create an array with a given size and initialized elements.

int find(value: Vector4, from: int = 0) const 🔗

Searches the array for a value and returns its index or -1 if not found. Optionally, the initial search index can be passed.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

Vector4 get(index: int) const 🔗

Returns the Vector4 at the given index in the array. If index out-of-bounds or negative, this method fails and returns Vector4(0, 0, 0, 0).

This method is similar (but not identical) to the [] operator. Most notably, when this method fails, it doesn't pause project execution if run from the editor.

bool has(value: Vector4) const 🔗

Returns true if the array contains value.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

int insert(at_index: int, value: Vector4) 🔗

Inserts a new element at a given position in the array. The position must be valid, or at the end of the array (idx == size()).

bool is_empty() const 🔗

Returns true if the array is empty.

bool push_back(value: Vector4) 🔗

Inserts a Vector4 at the end.

void remove_at(index: int) 🔗

Removes an element from the array by index.

int resize(new_size: int) 🔗

Sets the size of the array. If the array is grown, reserves elements at the end of the array. If the array is shrunk, truncates the array to the new size. Calling resize() once and assigning the new values is faster than adding new elements one by one.

Returns @GlobalScope.OK on success, or one of the following Error constants if this method fails: @GlobalScope.ERR_INVALID_PARAMETER if the size is negative, or @GlobalScope.ERR_OUT_OF_MEMORY if allocations fail. Use size() to find the actual size of the array after resize.

Reverses the order of the elements in the array.

int rfind(value: Vector4, from: int = -1) const 🔗

Searches the array in reverse order. Optionally, a start search index can be passed. If negative, the start index is considered relative to the end of the array.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

void set(index: int, value: Vector4) 🔗

Changes the Vector4 at the given index.

Returns the number of elements in the array.

PackedVector4Array slice(begin: int, end: int = 2147483647) const 🔗

Returns the slice of the PackedVector4Array, from begin (inclusive) to end (exclusive), as a new PackedVector4Array.

The absolute value of begin and end will be clamped to the array size, so the default value for end makes it slice to the size of the array by default (i.e. arr.slice(1) is a shorthand for arr.slice(1, arr.size())).

If either begin or end are negative, they will be relative to the end of the array (i.e. arr.slice(0, -2) is a shorthand for arr.slice(0, arr.size() - 2)).

Sorts the elements of the array in ascending order.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this method may not be accurate if NaNs are included.

PackedByteArray to_byte_array() const 🔗

Returns a PackedByteArray with each vector encoded as bytes.

bool operator !=(right: PackedVector4Array) 🔗

Returns true if contents of the arrays differ.

PackedVector4Array operator +(right: PackedVector4Array) 🔗

Returns a new PackedVector4Array with contents of right added at the end of this array. For better performance, consider using append_array() instead.

bool operator ==(right: PackedVector4Array) 🔗

Returns true if contents of both arrays are the same, i.e. they have all equal Vector4s at the corresponding indices.

Vector4 operator [](index: int) 🔗

Returns the Vector4 at index index. Negative indices can be used to access the elements starting from the end. Using index out of array's bounds will result in an error.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var array = PackedVector4Array([Vector4(12, 34, 56, 78), Vector4(90, 12, 34, 56)])
```

---

## Plane

**URL:** https://docs.godotengine.org/en/stable/classes/class_plane.html

**Contents:**
- Plane
- Description
- Tutorials
- Properties
- Constructors
- Methods
- Operators
- Constants
- Property Descriptions
- Constructor Descriptions

A plane in Hessian normal form.

Represents a normalized plane equation. normal is the normal of the plane (a, b, c normalized), and d is the distance from the origin to the plane (in the direction of "normal"). "Over" or "Above" the plane is considered the side of the plane towards where the normal is pointing.

Math documentation index

Plane(a: float, b: float, c: float, d: float)

Plane(normal: Vector3)

Plane(normal: Vector3, d: float)

Plane(normal: Vector3, point: Vector3)

Plane(point1: Vector3, point2: Vector3, point3: Vector3)

distance_to(point: Vector3) const

has_point(point: Vector3, tolerance: float = 1e-05) const

intersect_3(b: Plane, c: Plane) const

intersects_ray(from: Vector3, dir: Vector3) const

intersects_segment(from: Vector3, to: Vector3) const

is_equal_approx(to_plane: Plane) const

is_point_over(point: Vector3) const

project(point: Vector3) const

operator !=(right: Plane)

operator *(right: Transform3D)

operator ==(right: Plane)

PLANE_YZ = Plane(1, 0, 0, 0) 🔗

A plane that extends in the Y and Z axes (normal vector points +X).

PLANE_XZ = Plane(0, 1, 0, 0) 🔗

A plane that extends in the X and Z axes (normal vector points +Y).

PLANE_XY = Plane(0, 0, 1, 0) 🔗

A plane that extends in the X and Y axes (normal vector points +Z).

The distance from the origin to the plane, expressed in terms of normal (according to its direction and magnitude). Actual absolute distance from the origin to the plane can be calculated as abs(d) / normal.length() (if normal has zero length then this Plane does not represent a valid plane).

In the scalar equation of the plane ax + by + cz = d, this is d, while the (a, b, c) coordinates are represented by the normal property.

Vector3 normal = Vector3(0, 0, 0) 🔗

The normal of the plane, typically a unit vector. Shouldn't be a zero vector as Plane with such normal does not represent a valid plane.

In the scalar equation of the plane ax + by + cz = d, this is the vector (a, b, c), where d is the d property.

The X component of the plane's normal vector.

The Y component of the plane's normal vector.

The Z component of the plane's normal vector.

Constructs a default-initialized Plane with all components set to 0.

Plane Plane(from: Plane)

Constructs a Plane as a copy of the given Plane.

Plane Plane(a: float, b: float, c: float, d: float)

Creates a plane from the four parameters. The three components of the resulting plane's normal are a, b and c, and the plane has a distance of d from the origin.

Plane Plane(normal: Vector3)

Creates a plane from the normal vector. The plane will intersect the origin.

The normal of the plane must be a unit vector.

Plane Plane(normal: Vector3, d: float)

Creates a plane from the normal vector and the plane's distance from the origin.

The normal of the plane must be a unit vector.

Plane Plane(normal: Vector3, point: Vector3)

Creates a plane from the normal vector and a point on the plane.

The normal of the plane must be a unit vector.

Plane Plane(point1: Vector3, point2: Vector3, point3: Vector3)

Creates a plane from the three points, given in clockwise order.

float distance_to(point: Vector3) const 🔗

Returns the shortest distance from the plane to the position point. If the point is above the plane, the distance will be positive. If below, the distance will be negative.

Vector3 get_center() const 🔗

Returns the center of the plane.

bool has_point(point: Vector3, tolerance: float = 1e-05) const 🔗

Returns true if point is inside the plane. Comparison uses a custom minimum tolerance threshold.

Variant intersect_3(b: Plane, c: Plane) const 🔗

Returns the intersection point of the three planes b, c and this plane. If no intersection is found, null is returned.

Variant intersects_ray(from: Vector3, dir: Vector3) const 🔗

Returns the intersection point of a ray consisting of the position from and the direction normal dir with this plane. If no intersection is found, null is returned.

Variant intersects_segment(from: Vector3, to: Vector3) const 🔗

Returns the intersection point of a segment from position from to position to with this plane. If no intersection is found, null is returned.

bool is_equal_approx(to_plane: Plane) const 🔗

Returns true if this plane and to_plane are approximately equal, by running @GlobalScope.is_equal_approx() on each component.

bool is_finite() const 🔗

Returns true if this plane is finite, by calling @GlobalScope.is_finite() on each component.

bool is_point_over(point: Vector3) const 🔗

Returns true if point is located above the plane.

Plane normalized() const 🔗

Returns a copy of the plane, with normalized normal (so it's a unit vector). Returns Plane(0, 0, 0, 0) if normal can't be normalized (it has zero length).

Vector3 project(point: Vector3) const 🔗

Returns the orthogonal projection of point into a point in the plane.

bool operator !=(right: Plane) 🔗

Returns true if the planes are not equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Plane operator *(right: Transform3D) 🔗

Inversely transforms (multiplies) the Plane by the given Transform3D transformation matrix.

plane * transform is equivalent to transform.affine_inverse() * plane. See Transform3D.affine_inverse().

bool operator ==(right: Plane) 🔗

Returns true if the planes are exactly equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Plane operator unary+() 🔗

Returns the same value as if the + was not there. Unary + does nothing, but sometimes it can make your code more readable.

Plane operator unary-() 🔗

Returns the negative value of the Plane. This is the same as writing Plane(-p.normal, -p.d). This operation flips the direction of the normal vector and also flips the distance value, resulting in a Plane that is in the same place, but facing the opposite direction.

Please read the User-contributed notes policy before submitting a comment.

---

## Projection

**URL:** https://docs.godotengine.org/en/stable/classes/class_projection.html

**Contents:**
- Projection
- Description
- Properties
- Constructors
- Methods
- Operators
- Enumerations
- Constants
- Property Descriptions
- Constructor Descriptions

A 4×4 matrix for 3D projective transformations.

A 4×4 matrix used for 3D projective transformations. It can represent transformations such as translation, rotation, scaling, shearing, and perspective division. It consists of four Vector4 columns.

For purely linear transformations (translation, rotation, and scale), it is recommended to use Transform3D, as it is more performant and requires less memory.

Used internally as Camera3D's projection matrix.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

Projection(from: Projection)

Projection(from: Transform3D)

Projection(x_axis: Vector4, y_axis: Vector4, z_axis: Vector4, w_axis: Vector4)

create_depth_correction(flip_y: bool) static

create_fit_aabb(aabb: AABB) static

create_for_hmd(eye: int, aspect: float, intraocular_dist: float, display_width: float, display_to_lens: float, oversample: float, z_near: float, z_far: float) static

create_frustum(left: float, right: float, bottom: float, top: float, z_near: float, z_far: float) static

create_frustum_aspect(size: float, aspect: float, offset: Vector2, z_near: float, z_far: float, flip_fov: bool = false) static

create_light_atlas_rect(rect: Rect2) static

create_orthogonal(left: float, right: float, bottom: float, top: float, z_near: float, z_far: float) static

create_orthogonal_aspect(size: float, aspect: float, z_near: float, z_far: float, flip_fov: bool = false) static

create_perspective(fovy: float, aspect: float, z_near: float, z_far: float, flip_fov: bool = false) static

create_perspective_hmd(fovy: float, aspect: float, z_near: float, z_far: float, flip_fov: bool, eye: int, intraocular_dist: float, convergence_dist: float) static

get_far_plane_half_extents() const

get_fovy(fovx: float, aspect: float) static

get_lod_multiplier() const

get_pixels_per_meter(for_pixel_width: int) const

get_projection_plane(plane: int) const

get_viewport_half_extents() const

is_orthogonal() const

jitter_offseted(offset: Vector2) const

perspective_znear_adjusted(new_znear: float) const

operator !=(right: Projection)

operator *(right: Projection)

operator *(right: Vector4)

operator ==(right: Projection)

operator [](index: int)

Planes PLANE_NEAR = 0

The index value of the projection's near clipping plane.

The index value of the projection's far clipping plane.

Planes PLANE_LEFT = 2

The index value of the projection's left clipping plane.

The index value of the projection's top clipping plane.

Planes PLANE_RIGHT = 4

The index value of the projection's right clipping plane.

Planes PLANE_BOTTOM = 5

The index value of the projection bottom clipping plane.

IDENTITY = Projection(1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1) 🔗

A Projection with no transformation defined. When applied to other data structures, no transformation is performed.

ZERO = Projection(0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0) 🔗

A Projection with all values initialized to 0. When applied to other data structures, they will be zeroed.

Vector4 w = Vector4(0, 0, 0, 1) 🔗

The projection matrix's W vector (column 3). Equivalent to array index 3.

Vector4 x = Vector4(1, 0, 0, 0) 🔗

The projection matrix's X vector (column 0). Equivalent to array index 0.

Vector4 y = Vector4(0, 1, 0, 0) 🔗

The projection matrix's Y vector (column 1). Equivalent to array index 1.

Vector4 z = Vector4(0, 0, 1, 0) 🔗

The projection matrix's Z vector (column 2). Equivalent to array index 2.

Projection Projection() 🔗

Constructs a default-initialized Projection identical to IDENTITY.

Note: In C#, this constructs a Projection identical to ZERO.

Projection Projection(from: Projection)

Constructs a Projection as a copy of the given Projection.

Projection Projection(from: Transform3D)

Constructs a Projection as a copy of the given Transform3D.

Projection Projection(x_axis: Vector4, y_axis: Vector4, z_axis: Vector4, w_axis: Vector4)

Constructs a Projection from four Vector4 values (matrix columns).

Projection create_depth_correction(flip_y: bool) static 🔗

Creates a new Projection that projects positions from a depth range of -1 to 1 to one that ranges from 0 to 1, and flips the projected positions vertically, according to flip_y.

Projection create_fit_aabb(aabb: AABB) static 🔗

Creates a new Projection that scales a given projection to fit around a given AABB in projection space.

Projection create_for_hmd(eye: int, aspect: float, intraocular_dist: float, display_width: float, display_to_lens: float, oversample: float, z_near: float, z_far: float) static 🔗

Creates a new Projection for projecting positions onto a head-mounted display with the given X:Y aspect ratio, distance between eyes, display width, distance to lens, oversampling factor, and depth clipping planes.

eye creates the projection for the left eye when set to 1, or the right eye when set to 2.

Projection create_frustum(left: float, right: float, bottom: float, top: float, z_near: float, z_far: float) static 🔗

Creates a new Projection that projects positions in a frustum with the given clipping planes.

Projection create_frustum_aspect(size: float, aspect: float, offset: Vector2, z_near: float, z_far: float, flip_fov: bool = false) static 🔗

Creates a new Projection that projects positions in a frustum with the given size, X:Y aspect ratio, offset, and clipping planes.

flip_fov determines whether the projection's field of view is flipped over its diagonal.

Projection create_light_atlas_rect(rect: Rect2) static 🔗

Creates a new Projection that projects positions into the given Rect2.

Projection create_orthogonal(left: float, right: float, bottom: float, top: float, z_near: float, z_far: float) static 🔗

Creates a new Projection that projects positions using an orthogonal projection with the given clipping planes.

Projection create_orthogonal_aspect(size: float, aspect: float, z_near: float, z_far: float, flip_fov: bool = false) static 🔗

Creates a new Projection that projects positions using an orthogonal projection with the given size, X:Y aspect ratio, and clipping planes.

flip_fov determines whether the projection's field of view is flipped over its diagonal.

Projection create_perspective(fovy: float, aspect: float, z_near: float, z_far: float, flip_fov: bool = false) static 🔗

Creates a new Projection that projects positions using a perspective projection with the given Y-axis field of view (in degrees), X:Y aspect ratio, and clipping planes.

flip_fov determines whether the projection's field of view is flipped over its diagonal.

Projection create_perspective_hmd(fovy: float, aspect: float, z_near: float, z_far: float, flip_fov: bool, eye: int, intraocular_dist: float, convergence_dist: float) static 🔗

Creates a new Projection that projects positions using a perspective projection with the given Y-axis field of view (in degrees), X:Y aspect ratio, and clipping distances. The projection is adjusted for a head-mounted display with the given distance between eyes and distance to a point that can be focused on.

eye creates the projection for the left eye when set to 1, or the right eye when set to 2.

flip_fov determines whether the projection's field of view is flipped over its diagonal.

float determinant() const 🔗

Returns a scalar value that is the signed factor by which areas are scaled by this matrix. If the sign is negative, the matrix flips the orientation of the area.

The determinant can be used to calculate the invertibility of a matrix or solve linear systems of equations involving the matrix, among other applications.

Projection flipped_y() const 🔗

Returns a copy of this Projection with the signs of the values of the Y column flipped.

float get_aspect() const 🔗

Returns the X:Y aspect ratio of this Projection's viewport.

Vector2 get_far_plane_half_extents() const 🔗

Returns the dimensions of the far clipping plane of the projection, divided by two.

float get_fov() const 🔗

Returns the horizontal field of view of the projection (in degrees).

float get_fovy(fovx: float, aspect: float) static 🔗

Returns the vertical field of view of the projection (in degrees) associated with the given horizontal field of view (in degrees) and aspect ratio.

Note: Unlike most methods of Projection, aspect is expected to be 1 divided by the X:Y aspect ratio.

float get_lod_multiplier() const 🔗

Returns the factor by which the visible level of detail is scaled by this Projection.

int get_pixels_per_meter(for_pixel_width: int) const 🔗

Returns for_pixel_width divided by the viewport's width measured in meters on the near plane, after this Projection is applied.

Plane get_projection_plane(plane: int) const 🔗

Returns the clipping plane of this Projection whose index is given by plane.

plane should be equal to one of PLANE_NEAR, PLANE_FAR, PLANE_LEFT, PLANE_TOP, PLANE_RIGHT, or PLANE_BOTTOM.

Vector2 get_viewport_half_extents() const 🔗

Returns the dimensions of the viewport plane that this Projection projects positions onto, divided by two.

float get_z_far() const 🔗

Returns the distance for this Projection beyond which positions are clipped.

float get_z_near() const 🔗

Returns the distance for this Projection before which positions are clipped.

Projection inverse() const 🔗

Returns a Projection that performs the inverse of this Projection's projective transformation.

bool is_orthogonal() const 🔗

Returns true if this Projection performs an orthogonal projection.

Projection jitter_offseted(offset: Vector2) const 🔗

Returns a Projection with the X and Y values from the given Vector2 added to the first and second values of the final column respectively.

Projection perspective_znear_adjusted(new_znear: float) const 🔗

Returns a Projection with the near clipping distance adjusted to be new_znear.

Note: The original Projection must be a perspective projection.

bool operator !=(right: Projection) 🔗

Returns true if the projections are not equal.

Note: Due to floating-point precision errors, this may return true, even if the projections are virtually equal. An is_equal_approx method may be added in a future version of Godot.

Projection operator *(right: Projection) 🔗

Returns a Projection that applies the combined transformations of this Projection and right.

Vector4 operator *(right: Vector4) 🔗

Projects (multiplies) the given Vector4 by this Projection matrix.

bool operator ==(right: Projection) 🔗

Returns true if the projections are equal.

Note: Due to floating-point precision errors, this may return false, even if the projections are virtually equal. An is_equal_approx method may be added in a future version of Godot.

Vector4 operator [](index: int) 🔗

Returns the column of the Projection with the given index.

Indices are in the following order: x, y, z, w.

Please read the User-contributed notes policy before submitting a comment.

---

## Quaternion

**URL:** https://docs.godotengine.org/en/stable/classes/class_quaternion.html

**Contents:**
- Quaternion
- Description
- Tutorials
- Properties
- Constructors
- Methods
- Operators
- Constants
- Property Descriptions
- Constructor Descriptions

A unit quaternion used for representing 3D rotations.

The Quaternion built-in Variant type is a 4D data structure that represents rotation in the form of a Hamilton convention quaternion. Compared to the Basis type which can store both rotation and scale, quaternions can only store rotation.

A Quaternion is composed by 4 floating-point components: w, x, y, and z. These components are very compact in memory, and because of this some operations are more efficient and less likely to cause floating-point errors. Methods such as get_angle(), get_axis(), and slerp() are faster than their Basis counterparts.

For a great introduction to quaternions, see this video by 3Blue1Brown. You do not need to know the math behind quaternions, as Godot provides several helper methods that handle it for you. These include slerp() and spherical_cubic_interpolate(), as well as the * operator.

Note: Quaternions must be normalized before being used for rotation (see normalized()).

Note: Similarly to Vector2 and Vector3, the components of a quaternion use 32-bit precision by default, unlike float which is always 64-bit. If double precision is needed, compile the engine with the option precision=double.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

3Blue1Brown's video on Quaternions

Online Quaternion Visualization

Third Person Shooter (TPS) Demo

Advanced Quaternion Visualization

Quaternion(from: Quaternion)

Quaternion(arc_from: Vector3, arc_to: Vector3)

Quaternion(axis: Vector3, angle: float)

Quaternion(from: Basis)

Quaternion(x: float, y: float, z: float, w: float)

angle_to(to: Quaternion) const

dot(with: Quaternion) const

from_euler(euler: Vector3) static

get_euler(order: int = 2) const

is_equal_approx(to: Quaternion) const

is_normalized() const

length_squared() const

slerp(to: Quaternion, weight: float) const

slerpni(to: Quaternion, weight: float) const

spherical_cubic_interpolate(b: Quaternion, pre_a: Quaternion, post_b: Quaternion, weight: float) const

spherical_cubic_interpolate_in_time(b: Quaternion, pre_a: Quaternion, post_b: Quaternion, weight: float, b_t: float, pre_a_t: float, post_b_t: float) const

operator !=(right: Quaternion)

operator *(right: Quaternion)

operator *(right: Vector3)

operator *(right: float)

operator *(right: int)

operator +(right: Quaternion)

operator -(right: Quaternion)

operator /(right: float)

operator /(right: int)

operator ==(right: Quaternion)

operator [](index: int)

IDENTITY = Quaternion(0, 0, 0, 1) 🔗

The identity quaternion, representing no rotation. This has the same rotation as Basis.IDENTITY.

If a Vector3 is rotated (multiplied) by this quaternion, it does not change.

Note: In GDScript, this constant is equivalent to creating a Quaternion without any arguments. It can be used to make your code clearer, and for consistency with C#.

W component of the quaternion. This is the "real" part.

Note: Quaternion components should usually not be manipulated directly.

X component of the quaternion. This is the value along the "imaginary" i axis.

Note: Quaternion components should usually not be manipulated directly.

Y component of the quaternion. This is the value along the "imaginary" j axis.

Note: Quaternion components should usually not be manipulated directly.

Z component of the quaternion. This is the value along the "imaginary" k axis.

Note: Quaternion components should usually not be manipulated directly.

Quaternion Quaternion() 🔗

Constructs a Quaternion identical to IDENTITY.

Note: In C#, this constructs a Quaternion with all of its components set to 0.0.

Quaternion Quaternion(from: Quaternion)

Constructs a Quaternion as a copy of the given Quaternion.

Quaternion Quaternion(arc_from: Vector3, arc_to: Vector3)

Constructs a Quaternion representing the shortest arc between arc_from and arc_to. These can be imagined as two points intersecting a sphere's surface, with a radius of 1.0.

Quaternion Quaternion(axis: Vector3, angle: float)

Constructs a Quaternion representing rotation around the axis by the given angle, in radians. The axis must be a normalized vector.

Quaternion Quaternion(from: Basis)

Constructs a Quaternion from the given rotation Basis.

This constructor is faster than Basis.get_rotation_quaternion(), but the given basis must be orthonormalized (see Basis.orthonormalized()). Otherwise, the constructor fails and returns IDENTITY.

Quaternion Quaternion(x: float, y: float, z: float, w: float)

Constructs a Quaternion defined by the given values.

Note: Only normalized quaternions represent rotation; if these values are not normalized, the new Quaternion will not be a valid rotation.

float angle_to(to: Quaternion) const 🔗

Returns the angle between this quaternion and to. This is the magnitude of the angle you would need to rotate by to get from one to the other.

Note: The magnitude of the floating-point error for this method is abnormally high, so methods such as is_zero_approx will not work reliably.

float dot(with: Quaternion) const 🔗

Returns the dot product between this quaternion and with.

This is equivalent to (quat.x * with.x) + (quat.y * with.y) + (quat.z * with.z) + (quat.w * with.w).

Quaternion exp() const 🔗

Returns the exponential of this quaternion. The rotation axis of the result is the normalized rotation axis of this quaternion, the angle of the result is the length of the vector part of this quaternion.

Quaternion from_euler(euler: Vector3) static 🔗

Constructs a new Quaternion from the given Vector3 of Euler angles, in radians. This method always uses the YXZ convention (@GlobalScope.EULER_ORDER_YXZ).

float get_angle() const 🔗

Returns the angle of the rotation represented by this quaternion.

Note: The quaternion must be normalized.

Vector3 get_axis() const 🔗

Returns the rotation axis of the rotation represented by this quaternion.

Vector3 get_euler(order: int = 2) const 🔗

Returns this quaternion's rotation as a Vector3 of Euler angles, in radians.

The order of each consecutive rotation can be changed with order (see EulerOrder constants). By default, the YXZ convention is used (@GlobalScope.EULER_ORDER_YXZ): Z (roll) is calculated first, then X (pitch), and lastly Y (yaw). When using the opposite method from_euler(), this order is reversed.

Quaternion inverse() const 🔗

Returns the inverse version of this quaternion, inverting the sign of every component except w.

bool is_equal_approx(to: Quaternion) const 🔗

Returns true if this quaternion and to are approximately equal, by calling @GlobalScope.is_equal_approx() on each component.

bool is_finite() const 🔗

Returns true if this quaternion is finite, by calling @GlobalScope.is_finite() on each component.

bool is_normalized() const 🔗

Returns true if this quaternion is normalized. See also normalized().

float length() const 🔗

Returns this quaternion's length, also called magnitude.

float length_squared() const 🔗

Returns this quaternion's length, squared.

Note: This method is faster than length(), so prefer it if you only need to compare quaternion lengths.

Quaternion log() const 🔗

Returns the logarithm of this quaternion. Multiplies this quaternion's rotation axis by its rotation angle, and stores the result in the returned quaternion's vector part (x, y, and z). The returned quaternion's real part (w) is always 0.0.

Quaternion normalized() const 🔗

Returns a copy of this quaternion, normalized so that its length is 1.0. See also is_normalized().

Quaternion slerp(to: Quaternion, weight: float) const 🔗

Performs a spherical-linear interpolation with the to quaternion, given a weight and returns the result. Both this quaternion and to must be normalized.

Quaternion slerpni(to: Quaternion, weight: float) const 🔗

Performs a spherical-linear interpolation with the to quaternion, given a weight and returns the result. Unlike slerp(), this method does not check if the rotation path is smaller than 90 degrees. Both this quaternion and to must be normalized.

Quaternion spherical_cubic_interpolate(b: Quaternion, pre_a: Quaternion, post_b: Quaternion, weight: float) const 🔗

Performs a spherical cubic interpolation between quaternions pre_a, this vector, b, and post_b, by the given amount weight.

Quaternion spherical_cubic_interpolate_in_time(b: Quaternion, pre_a: Quaternion, post_b: Quaternion, weight: float, b_t: float, pre_a_t: float, post_b_t: float) const 🔗

Performs a spherical cubic interpolation between quaternions pre_a, this vector, b, and post_b, by the given amount weight.

It can perform smoother interpolation than spherical_cubic_interpolate() by the time values.

bool operator !=(right: Quaternion) 🔗

Returns true if the components of both quaternions are not exactly equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Quaternion operator *(right: Quaternion) 🔗

Composes (multiplies) two quaternions. This rotates the right quaternion (the child) by this quaternion (the parent).

Vector3 operator *(right: Vector3) 🔗

Rotates (multiplies) the right vector by this quaternion, returning a Vector3.

Quaternion operator *(right: float) 🔗

Multiplies each component of the Quaternion by the right float value.

This operation is not meaningful on its own, but it can be used as a part of a larger expression.

Quaternion operator *(right: int) 🔗

Multiplies each component of the Quaternion by the right int value.

This operation is not meaningful on its own, but it can be used as a part of a larger expression.

Quaternion operator +(right: Quaternion) 🔗

Adds each component of the left Quaternion to the right Quaternion.

This operation is not meaningful on its own, but it can be used as a part of a larger expression, such as approximating an intermediate rotation between two nearby rotations.

Quaternion operator -(right: Quaternion) 🔗

Subtracts each component of the left Quaternion by the right Quaternion.

This operation is not meaningful on its own, but it can be used as a part of a larger expression.

Quaternion operator /(right: float) 🔗

Divides each component of the Quaternion by the right float value.

This operation is not meaningful on its own, but it can be used as a part of a larger expression.

Quaternion operator /(right: int) 🔗

Divides each component of the Quaternion by the right int value.

This operation is not meaningful on its own, but it can be used as a part of a larger expression.

bool operator ==(right: Quaternion) 🔗

Returns true if the components of both quaternions are exactly equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

float operator [](index: int) 🔗

Accesses each component of this quaternion by their index.

Index 0 is the same as x, index 1 is the same as y, index 2 is the same as z, and index 3 is the same as w.

Quaternion operator unary+() 🔗

Returns the same value as if the + was not there. Unary + does nothing, but sometimes it can make your code more readable.

Quaternion operator unary-() 🔗

Returns the negative value of the Quaternion. This is the same as multiplying all components by -1. This operation results in a quaternion that represents the same rotation.

Please read the User-contributed notes policy before submitting a comment.

---

## Rect2

**URL:** https://docs.godotengine.org/en/stable/classes/class_rect2.html

**Contents:**
- Rect2
- Description
- Tutorials
- Properties
- Constructors
- Methods
- Operators
- Property Descriptions
- Constructor Descriptions
- Method Descriptions

A 2D axis-aligned bounding box using floating-point coordinates.

The Rect2 built-in Variant type represents an axis-aligned rectangle in a 2D space. It is defined by its position and size, which are Vector2. It is frequently used for fast overlap tests (see intersects()). Although Rect2 itself is axis-aligned, it can be combined with Transform2D to represent a rotated or skewed rectangle.

For integer coordinates, use Rect2i. The 3D equivalent to Rect2 is AABB.

Note: Negative values for size are not supported. With negative size, most Rect2 methods do not work correctly. Use abs() to get an equivalent Rect2 with a non-negative size.

Note: In a boolean context, a Rect2 evaluates to false if both position and size are zero (equal to Vector2.ZERO). Otherwise, it always evaluates to true.

There are notable differences when using this API with C#. See C# API differences to GDScript for more information.

Math documentation index

Rect2(position: Vector2, size: Vector2)

Rect2(x: float, y: float, width: float, height: float)

encloses(b: Rect2) const

expand(to: Vector2) const

get_support(direction: Vector2) const

grow(amount: float) const

grow_individual(left: float, top: float, right: float, bottom: float) const

grow_side(side: int, amount: float) const

has_point(point: Vector2) const

intersection(b: Rect2) const

intersects(b: Rect2, include_borders: bool = false) const

is_equal_approx(rect: Rect2) const

merge(b: Rect2) const

operator !=(right: Rect2)

operator *(right: Transform2D)

operator ==(right: Rect2)

Vector2 end = Vector2(0, 0) 🔗

The ending point. This is usually the bottom-right corner of the rectangle, and is equivalent to position + size. Setting this point affects the size.

Vector2 position = Vector2(0, 0) 🔗

The origin point. This is usually the top-left corner of the rectangle.

Vector2 size = Vector2(0, 0) 🔗

The rectangle's width and height, starting from position. Setting this value also affects the end point.

Note: It's recommended setting the width and height to non-negative values, as most methods in Godot assume that the position is the top-left corner, and the end is the bottom-right corner. To get an equivalent rectangle with non-negative size, use abs().

Constructs a Rect2 with its position and size set to Vector2.ZERO.

Rect2 Rect2(from: Rect2)

Constructs a Rect2 as a copy of the given Rect2.

Rect2 Rect2(from: Rect2i)

Constructs a Rect2 from a Rect2i.

Rect2 Rect2(position: Vector2, size: Vector2)

Constructs a Rect2 by position and size.

Rect2 Rect2(x: float, y: float, width: float, height: float)

Constructs a Rect2 by setting its position to (x, y), and its size to (width, height).

Returns a Rect2 equivalent to this rectangle, with its width and height modified to be non-negative values, and with its position being the top-left corner of the rectangle.

Note: It's recommended to use this method when size is negative, as most other methods in Godot assume that the position is the top-left corner, and the end is the bottom-right corner.

bool encloses(b: Rect2) const 🔗

Returns true if this rectangle completely encloses the b rectangle.

Rect2 expand(to: Vector2) const 🔗

Returns a copy of this rectangle expanded to align the edges with the given to point, if necessary.

float get_area() const 🔗

Returns the rectangle's area. This is equivalent to size.x * size.y. See also has_area().

Vector2 get_center() const 🔗

Returns the center point of the rectangle. This is the same as position + (size / 2.0).

Vector2 get_support(direction: Vector2) const 🔗

Returns the vertex's position of this rect that's the farthest in the given direction. This point is commonly known as the support point in collision detection algorithms.

Rect2 grow(amount: float) const 🔗

Returns a copy of this rectangle extended on all sides by the given amount. A negative amount shrinks the rectangle instead. See also grow_individual() and grow_side().

Rect2 grow_individual(left: float, top: float, right: float, bottom: float) const 🔗

Returns a copy of this rectangle with its left, top, right, and bottom sides extended by the given amounts. Negative values shrink the sides, instead. See also grow() and grow_side().

Rect2 grow_side(side: int, amount: float) const 🔗

Returns a copy of this rectangle with its side extended by the given amount (see Side constants). A negative amount shrinks the rectangle, instead. See also grow() and grow_individual().

bool has_area() const 🔗

Returns true if this rectangle has positive width and height. See also get_area().

bool has_point(point: Vector2) const 🔗

Returns true if the rectangle contains the given point. By convention, points on the right and bottom edges are not included.

Note: This method is not reliable for Rect2 with a negative size. Use abs() first to get a valid rectangle.

Rect2 intersection(b: Rect2) const 🔗

Returns the intersection between this rectangle and b. If the rectangles do not intersect, returns an empty Rect2.

Note: If you only need to know whether two rectangles are overlapping, use intersects(), instead.

bool intersects(b: Rect2, include_borders: bool = false) const 🔗

Returns true if this rectangle overlaps with the b rectangle. The edges of both rectangles are excluded, unless include_borders is true.

bool is_equal_approx(rect: Rect2) const 🔗

Returns true if this rectangle and rect are approximately equal, by calling Vector2.is_equal_approx() on the position and the size.

bool is_finite() const 🔗

Returns true if this rectangle's values are finite, by calling Vector2.is_finite() on the position and the size.

Rect2 merge(b: Rect2) const 🔗

Returns a Rect2 that encloses both this rectangle and b around the edges. See also encloses().

bool operator !=(right: Rect2) 🔗

Returns true if the position or size of both rectangles are not equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Rect2 operator *(right: Transform2D) 🔗

Inversely transforms (multiplies) the Rect2 by the given Transform2D transformation matrix, under the assumption that the transformation basis is orthonormal (i.e. rotation/reflection is fine, scaling/skew is not).

rect * transform is equivalent to transform.inverse() * rect. See Transform2D.inverse().

For transforming by inverse of an affine transformation (e.g. with scaling) transform.affine_inverse() * rect can be used instead. See Transform2D.affine_inverse().

bool operator ==(right: Rect2) 🔗

Returns true if both position and size of the rectangles are exactly equal, respectively.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var rect = Rect2(25, 25, -100, -50)
var absolute = rect.abs() # absolute is Rect2(-75, -25, 100, 50)
```

Example 2 (gdscript):
```gdscript
var rect = new Rect2(25, 25, -100, -50);
var absolute = rect.Abs(); // absolute is Rect2(-75, -25, 100, 50)
```

Example 3 (csharp):
```csharp
var rect = Rect2(0, 0, 5, 2)

rect = rect.expand(Vector2(10, 0)) # rect is Rect2(0, 0, 10, 2)
rect = rect.expand(Vector2(-5, 5)) # rect is Rect2(-5, 0, 15, 5)
```

Example 4 (csharp):
```csharp
var rect = new Rect2(0, 0, 5, 2);

rect = rect.Expand(new Vector2(10, 0)); // rect is Rect2(0, 0, 10, 2)
rect = rect.Expand(new Vector2(-5, 5)); // rect is Rect2(-5, 0, 15, 5)
```

---

## Vector2i

**URL:** https://docs.godotengine.org/en/stable/classes/class_vector2i.html

**Contents:**
- Vector2i
- Description
- Tutorials
- Properties
- Constructors
- Methods
- Operators
- Enumerations
- Constants
- Property Descriptions

A 2D vector using integer coordinates.

A 2-element structure that can be used to represent 2D grid coordinates or any other pair of integers.

It uses integer coordinates and is therefore preferable to Vector2 when exact precision is required. Note that the values are limited to 32 bits, and unlike Vector2 this cannot be configured with an engine build option. Use int or PackedInt64Array if 64-bit values are needed.

Note: In a boolean context, a Vector2i will evaluate to false if it's equal to Vector2i(0, 0). Otherwise, a Vector2i will always evaluate to true.

Math documentation index

3Blue1Brown Essence of Linear Algebra

Vector2i(from: Vector2i)

Vector2i(from: Vector2)

Vector2i(x: int, y: int)

clamp(min: Vector2i, max: Vector2i) const

clampi(min: int, max: int) const

distance_squared_to(to: Vector2i) const

distance_to(to: Vector2i) const

length_squared() const

max(with: Vector2i) const

max_axis_index() const

maxi(with: int) const

min(with: Vector2i) const

min_axis_index() const

mini(with: int) const

snapped(step: Vector2i) const

snappedi(step: int) const

operator !=(right: Vector2i)

operator %(right: Vector2i)

operator %(right: int)

operator *(right: Vector2i)

operator *(right: float)

operator *(right: int)

operator +(right: Vector2i)

operator -(right: Vector2i)

operator /(right: Vector2i)

operator /(right: float)

operator /(right: int)

operator <(right: Vector2i)

operator <=(right: Vector2i)

operator ==(right: Vector2i)

operator >(right: Vector2i)

operator >=(right: Vector2i)

operator [](index: int)

Enumerated value for the X axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the Y axis. Returned by max_axis_index() and min_axis_index().

ZERO = Vector2i(0, 0) 🔗

Zero vector, a vector with all components set to 0.

ONE = Vector2i(1, 1) 🔗

One vector, a vector with all components set to 1.

MIN = Vector2i(-2147483648, -2147483648) 🔗

Min vector, a vector with all components equal to INT32_MIN. Can be used as a negative integer equivalent of Vector2.INF.

MAX = Vector2i(2147483647, 2147483647) 🔗

Max vector, a vector with all components equal to INT32_MAX. Can be used as an integer equivalent of Vector2.INF.

LEFT = Vector2i(-1, 0) 🔗

Left unit vector. Represents the direction of left.

RIGHT = Vector2i(1, 0) 🔗

Right unit vector. Represents the direction of right.

UP = Vector2i(0, -1) 🔗

Up unit vector. Y is down in 2D, so this vector points -Y.

DOWN = Vector2i(0, 1) 🔗

Down unit vector. Y is down in 2D, so this vector points +Y.

The vector's X component. Also accessible by using the index position [0].

The vector's Y component. Also accessible by using the index position [1].

Vector2i Vector2i() 🔗

Constructs a default-initialized Vector2i with all components set to 0.

Vector2i Vector2i(from: Vector2i)

Constructs a Vector2i as a copy of the given Vector2i.

Vector2i Vector2i(from: Vector2)

Constructs a new Vector2i from the given Vector2 by truncating components' fractional parts (rounding towards zero). For a different behavior consider passing the result of Vector2.ceil(), Vector2.floor() or Vector2.round() to this constructor instead.

Vector2i Vector2i(x: int, y: int)

Constructs a new Vector2i from the given x and y.

Vector2i abs() const 🔗

Returns a new vector with all components in absolute values (i.e. positive).

float aspect() const 🔗

Returns the aspect ratio of this vector, the ratio of x to y.

Vector2i clamp(min: Vector2i, max: Vector2i) const 🔗

Returns a new vector with all components clamped between the components of min and max, by running @GlobalScope.clamp() on each component.

Vector2i clampi(min: int, max: int) const 🔗

Returns a new vector with all components clamped between min and max, by running @GlobalScope.clamp() on each component.

int distance_squared_to(to: Vector2i) const 🔗

Returns the squared distance between this vector and to.

This method runs faster than distance_to(), so prefer it if you need to compare vectors or need the squared distance for some formula.

float distance_to(to: Vector2i) const 🔗

Returns the distance between this vector and to.

float length() const 🔗

Returns the length (magnitude) of this vector.

int length_squared() const 🔗

Returns the squared length (squared magnitude) of this vector.

This method runs faster than length(), so prefer it if you need to compare vectors or need the squared distance for some formula.

Vector2i max(with: Vector2i) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector2i(maxi(x, with.x), maxi(y, with.y)).

int max_axis_index() const 🔗

Returns the axis of the vector's highest value. See AXIS_* constants. If all components are equal, this method returns AXIS_X.

Vector2i maxi(with: int) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector2i(maxi(x, with), maxi(y, with)).

Vector2i min(with: Vector2i) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector2i(mini(x, with.x), mini(y, with.y)).

int min_axis_index() const 🔗

Returns the axis of the vector's lowest value. See AXIS_* constants. If all components are equal, this method returns AXIS_Y.

Vector2i mini(with: int) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector2i(mini(x, with), mini(y, with)).

Vector2i sign() const 🔗

Returns a new vector with each component set to 1 if it's positive, -1 if it's negative, and 0 if it's zero. The result is identical to calling @GlobalScope.sign() on each component.

Vector2i snapped(step: Vector2i) const 🔗

Returns a new vector with each component snapped to the closest multiple of the corresponding component in step.

Vector2i snappedi(step: int) const 🔗

Returns a new vector with each component snapped to the closest multiple of step.

bool operator !=(right: Vector2i) 🔗

Returns true if the vectors are not equal.

Vector2i operator %(right: Vector2i) 🔗

Gets the remainder of each component of the Vector2i with the components of the given Vector2i. This operation uses truncated division, which is often not desired as it does not work well with negative numbers. Consider using @GlobalScope.posmod() instead if you want to handle negative numbers.

Vector2i operator %(right: int) 🔗

Gets the remainder of each component of the Vector2i with the given int. This operation uses truncated division, which is often not desired as it does not work well with negative numbers. Consider using @GlobalScope.posmod() instead if you want to handle negative numbers.

Vector2i operator *(right: Vector2i) 🔗

Multiplies each component of the Vector2i by the components of the given Vector2i.

Vector2 operator *(right: float) 🔗

Multiplies each component of the Vector2i by the given float. Returns a Vector2.

Vector2i operator *(right: int) 🔗

Multiplies each component of the Vector2i by the given int.

Vector2i operator +(right: Vector2i) 🔗

Adds each component of the Vector2i by the components of the given Vector2i.

Vector2i operator -(right: Vector2i) 🔗

Subtracts each component of the Vector2i by the components of the given Vector2i.

Vector2i operator /(right: Vector2i) 🔗

Divides each component of the Vector2i by the components of the given Vector2i.

Vector2 operator /(right: float) 🔗

Divides each component of the Vector2i by the given float. Returns a Vector2.

Vector2i operator /(right: int) 🔗

Divides each component of the Vector2i by the given int.

bool operator <(right: Vector2i) 🔗

Compares two Vector2i vectors by first checking if the X value of the left vector is less than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors. This operator is useful for sorting vectors.

bool operator <=(right: Vector2i) 🔗

Compares two Vector2i vectors by first checking if the X value of the left vector is less than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors. This operator is useful for sorting vectors.

bool operator ==(right: Vector2i) 🔗

Returns true if the vectors are equal.

bool operator >(right: Vector2i) 🔗

Compares two Vector2i vectors by first checking if the X value of the left vector is greater than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors. This operator is useful for sorting vectors.

bool operator >=(right: Vector2i) 🔗

Compares two Vector2i vectors by first checking if the X value of the left vector is greater than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors. This operator is useful for sorting vectors.

int operator [](index: int) 🔗

Access vector components using their index. v[0] is equivalent to v.x, and v[1] is equivalent to v.y.

Vector2i operator unary+() 🔗

Returns the same value as if the + was not there. Unary + does nothing, but sometimes it can make your code more readable.

Vector2i operator unary-() 🔗

Returns the negative value of the Vector2i. This is the same as writing Vector2i(-v.x, -v.y). This operation flips the direction of the vector while keeping the same magnitude.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
print(Vector2i(10, -20) % Vector2i(7, 8)) # Prints (3, -4)
```

Example 2 (swift):
```swift
print(Vector2i(10, -20) % 7) # Prints (3, -6)
```

Example 3 (swift):
```swift
print(Vector2i(10, 20) * Vector2i(3, 4)) # Prints (30, 80)
```

Example 4 (swift):
```swift
print(Vector2i(10, 15) * 0.9) # Prints (9.0, 13.5)
```

---

## Vector2

**URL:** https://docs.godotengine.org/en/stable/classes/class_vector2.html

**Contents:**
- Vector2
- Description
- Tutorials
- Properties
- Constructors
- Methods
- Operators
- Enumerations
- Constants
- Property Descriptions

A 2D vector using floating-point coordinates.

A 2-element structure that can be used to represent 2D coordinates or any other pair of numeric values.

It uses floating-point coordinates. By default, these floating-point values use 32-bit precision, unlike float which is always 64-bit. If double precision is needed, compile the engine with the option precision=double.

See Vector2i for its integer counterpart.

Note: In a boolean context, a Vector2 will evaluate to false if it's equal to Vector2(0, 0). Otherwise, a Vector2 will always evaluate to true.

Math documentation index

3Blue1Brown Essence of Linear Algebra

Matrix Transform Demo

Vector2(from: Vector2)

Vector2(from: Vector2i)

Vector2(x: float, y: float)

angle_to(to: Vector2) const

angle_to_point(to: Vector2) const

bezier_derivative(control_1: Vector2, control_2: Vector2, end: Vector2, t: float) const

bezier_interpolate(control_1: Vector2, control_2: Vector2, end: Vector2, t: float) const

bounce(n: Vector2) const

clamp(min: Vector2, max: Vector2) const

clampf(min: float, max: float) const

cross(with: Vector2) const

cubic_interpolate(b: Vector2, pre_a: Vector2, post_b: Vector2, weight: float) const

cubic_interpolate_in_time(b: Vector2, pre_a: Vector2, post_b: Vector2, weight: float, b_t: float, pre_a_t: float, post_b_t: float) const

direction_to(to: Vector2) const

distance_squared_to(to: Vector2) const

distance_to(to: Vector2) const

dot(with: Vector2) const

from_angle(angle: float) static

is_equal_approx(to: Vector2) const

is_normalized() const

is_zero_approx() const

length_squared() const

lerp(to: Vector2, weight: float) const

limit_length(length: float = 1.0) const

max(with: Vector2) const

max_axis_index() const

maxf(with: float) const

min(with: Vector2) const

min_axis_index() const

minf(with: float) const

move_toward(to: Vector2, delta: float) const

posmod(mod: float) const

posmodv(modv: Vector2) const

project(b: Vector2) const

reflect(line: Vector2) const

rotated(angle: float) const

slerp(to: Vector2, weight: float) const

slide(n: Vector2) const

snapped(step: Vector2) const

snappedf(step: float) const

operator !=(right: Vector2)

operator *(right: Transform2D)

operator *(right: Vector2)

operator *(right: float)

operator *(right: int)

operator +(right: Vector2)

operator -(right: Vector2)

operator /(right: Vector2)

operator /(right: float)

operator /(right: int)

operator <(right: Vector2)

operator <=(right: Vector2)

operator ==(right: Vector2)

operator >(right: Vector2)

operator >=(right: Vector2)

operator [](index: int)

Enumerated value for the X axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the Y axis. Returned by max_axis_index() and min_axis_index().

ZERO = Vector2(0, 0) 🔗

Zero vector, a vector with all components set to 0.

ONE = Vector2(1, 1) 🔗

One vector, a vector with all components set to 1.

INF = Vector2(inf, inf) 🔗

Infinity vector, a vector with all components set to @GDScript.INF.

LEFT = Vector2(-1, 0) 🔗

Left unit vector. Represents the direction of left.

RIGHT = Vector2(1, 0) 🔗

Right unit vector. Represents the direction of right.

UP = Vector2(0, -1) 🔗

Up unit vector. Y is down in 2D, so this vector points -Y.

DOWN = Vector2(0, 1) 🔗

Down unit vector. Y is down in 2D, so this vector points +Y.

The vector's X component. Also accessible by using the index position [0].

The vector's Y component. Also accessible by using the index position [1].

Constructs a default-initialized Vector2 with all components set to 0.

Vector2 Vector2(from: Vector2)

Constructs a Vector2 as a copy of the given Vector2.

Vector2 Vector2(from: Vector2i)

Constructs a new Vector2 from Vector2i.

Vector2 Vector2(x: float, y: float)

Constructs a new Vector2 from the given x and y.

Vector2 abs() const 🔗

Returns a new vector with all components in absolute values (i.e. positive).

float angle() const 🔗

Returns this vector's angle with respect to the positive X axis, or (1, 0) vector, in radians.

For example, Vector2.RIGHT.angle() will return zero, Vector2.DOWN.angle() will return PI / 2 (a quarter turn, or 90 degrees), and Vector2(1, -1).angle() will return -PI / 4 (a negative eighth turn, or -45 degrees).

Illustration of the returned angle.

Equivalent to the result of @GlobalScope.atan2() when called with the vector's y and x as parameters: atan2(y, x).

float angle_to(to: Vector2) const 🔗

Returns the signed angle to the given vector, in radians.

Illustration of the returned angle.

float angle_to_point(to: Vector2) const 🔗

Returns the angle between the line connecting the two points and the X axis, in radians.

a.angle_to_point(b) is equivalent of doing (b - a).angle().

Illustration of the returned angle.

float aspect() const 🔗

Returns the aspect ratio of this vector, the ratio of x to y.

Vector2 bezier_derivative(control_1: Vector2, control_2: Vector2, end: Vector2, t: float) const 🔗

Returns the derivative at the given t on the Bézier curve defined by this vector and the given control_1, control_2, and end points.

Vector2 bezier_interpolate(control_1: Vector2, control_2: Vector2, end: Vector2, t: float) const 🔗

Returns the point at the given t on the Bézier curve defined by this vector and the given control_1, control_2, and end points.

Vector2 bounce(n: Vector2) const 🔗

Returns the vector "bounced off" from a line defined by the given normal n perpendicular to the line.

Note: bounce() performs the operation that most engines and frameworks call reflect().

Vector2 ceil() const 🔗

Returns a new vector with all components rounded up (towards positive infinity).

Vector2 clamp(min: Vector2, max: Vector2) const 🔗

Returns a new vector with all components clamped between the components of min and max, by running @GlobalScope.clamp() on each component.

Vector2 clampf(min: float, max: float) const 🔗

Returns a new vector with all components clamped between min and max, by running @GlobalScope.clamp() on each component.

float cross(with: Vector2) const 🔗

Returns the 2D analog of the cross product for this vector and with.

This is the signed area of the parallelogram formed by the two vectors. If the second vector is clockwise from the first vector, then the cross product is the positive area. If counter-clockwise, the cross product is the negative area. If the two vectors are parallel this returns zero, making it useful for testing if two vectors are parallel.

Note: Cross product is not defined in 2D mathematically. This method embeds the 2D vectors in the XY plane of 3D space and uses their cross product's Z component as the analog.

Vector2 cubic_interpolate(b: Vector2, pre_a: Vector2, post_b: Vector2, weight: float) const 🔗

Performs a cubic interpolation between this vector and b using pre_a and post_b as handles, and returns the result at position weight. weight is on the range of 0.0 to 1.0, representing the amount of interpolation.

Vector2 cubic_interpolate_in_time(b: Vector2, pre_a: Vector2, post_b: Vector2, weight: float, b_t: float, pre_a_t: float, post_b_t: float) const 🔗

Performs a cubic interpolation between this vector and b using pre_a and post_b as handles, and returns the result at position weight. weight is on the range of 0.0 to 1.0, representing the amount of interpolation.

It can perform smoother interpolation than cubic_interpolate() by the time values.

Vector2 direction_to(to: Vector2) const 🔗

Returns the normalized vector pointing from this vector to to. This is equivalent to using (b - a).normalized().

float distance_squared_to(to: Vector2) const 🔗

Returns the squared distance between this vector and to.

This method runs faster than distance_to(), so prefer it if you need to compare vectors or need the squared distance for some formula.

float distance_to(to: Vector2) const 🔗

Returns the distance between this vector and to.

float dot(with: Vector2) const 🔗

Returns the dot product of this vector and with. This can be used to compare the angle between two vectors. For example, this can be used to determine whether an enemy is facing the player.

The dot product will be 0 for a right angle (90 degrees), greater than 0 for angles narrower than 90 degrees and lower than 0 for angles wider than 90 degrees.

When using unit (normalized) vectors, the result will always be between -1.0 (180 degree angle) when the vectors are facing opposite directions, and 1.0 (0 degree angle) when the vectors are aligned.

Note: a.dot(b) is equivalent to b.dot(a).

Vector2 floor() const 🔗

Returns a new vector with all components rounded down (towards negative infinity).

Vector2 from_angle(angle: float) static 🔗

Creates a Vector2 rotated to the given angle in radians. This is equivalent to doing Vector2(cos(angle), sin(angle)) or Vector2.RIGHT.rotated(angle).

Note: The length of the returned Vector2 is approximately 1.0, but is is not guaranteed to be exactly 1.0 due to floating-point precision issues. Call normalized() on the returned Vector2 if you require a unit vector.

bool is_equal_approx(to: Vector2) const 🔗

Returns true if this vector and to are approximately equal, by running @GlobalScope.is_equal_approx() on each component.

bool is_finite() const 🔗

Returns true if this vector is finite, by calling @GlobalScope.is_finite() on each component.

bool is_normalized() const 🔗

Returns true if the vector is normalized, i.e. its length is approximately equal to 1.

bool is_zero_approx() const 🔗

Returns true if this vector's values are approximately zero, by running @GlobalScope.is_zero_approx() on each component.

This method is faster than using is_equal_approx() with one value as a zero vector.

float length() const 🔗

Returns the length (magnitude) of this vector.

float length_squared() const 🔗

Returns the squared length (squared magnitude) of this vector.

This method runs faster than length(), so prefer it if you need to compare vectors or need the squared distance for some formula.

Vector2 lerp(to: Vector2, weight: float) const 🔗

Returns the result of the linear interpolation between this vector and to by amount weight. weight is on the range of 0.0 to 1.0, representing the amount of interpolation.

Vector2 limit_length(length: float = 1.0) const 🔗

Returns the vector with a maximum length by limiting its length to length. If the vector is non-finite, the result is undefined.

Vector2 max(with: Vector2) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector2(maxf(x, with.x), maxf(y, with.y)).

int max_axis_index() const 🔗

Returns the axis of the vector's highest value. See AXIS_* constants. If all components are equal, this method returns AXIS_X.

Vector2 maxf(with: float) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector2(maxf(x, with), maxf(y, with)).

Vector2 min(with: Vector2) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector2(minf(x, with.x), minf(y, with.y)).

int min_axis_index() const 🔗

Returns the axis of the vector's lowest value. See AXIS_* constants. If all components are equal, this method returns AXIS_Y.

Vector2 minf(with: float) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector2(minf(x, with), minf(y, with)).

Vector2 move_toward(to: Vector2, delta: float) const 🔗

Returns a new vector moved toward to by the fixed delta amount. Will not go past the final value.

Vector2 normalized() const 🔗

Returns the result of scaling the vector to unit length. Equivalent to v / v.length(). Returns (0, 0) if v.length() == 0. See also is_normalized().

Note: This function may return incorrect values if the input vector length is near zero.

Vector2 orthogonal() const 🔗

Returns a perpendicular vector rotated 90 degrees counter-clockwise compared to the original, with the same length.

Vector2 posmod(mod: float) const 🔗

Returns a vector composed of the @GlobalScope.fposmod() of this vector's components and mod.

Vector2 posmodv(modv: Vector2) const 🔗

Returns a vector composed of the @GlobalScope.fposmod() of this vector's components and modv's components.

Vector2 project(b: Vector2) const 🔗

Returns a new vector resulting from projecting this vector onto the given vector b. The resulting new vector is parallel to b. See also slide().

Note: If the vector b is a zero vector, the components of the resulting new vector will be @GDScript.NAN.

Vector2 reflect(line: Vector2) const 🔗

Returns the result of reflecting the vector from a line defined by the given direction vector line.

Note: reflect() differs from what other engines and frameworks call reflect(). In other engines, reflect() takes a normal direction which is a direction perpendicular to the line. In Godot, you specify the direction of the line directly. See also bounce() which does what most engines call reflect().

Vector2 rotated(angle: float) const 🔗

Returns the result of rotating this vector by angle (in radians). See also @GlobalScope.deg_to_rad().

Vector2 round() const 🔗

Returns a new vector with all components rounded to the nearest integer, with halfway cases rounded away from zero.

Vector2 sign() const 🔗

Returns a new vector with each component set to 1.0 if it's positive, -1.0 if it's negative, and 0.0 if it's zero. The result is identical to calling @GlobalScope.sign() on each component.

Vector2 slerp(to: Vector2, weight: float) const 🔗

Returns the result of spherical linear interpolation between this vector and to, by amount weight. weight is on the range of 0.0 to 1.0, representing the amount of interpolation.

This method also handles interpolating the lengths if the input vectors have different lengths. For the special case of one or both input vectors having zero length, this method behaves like lerp().

Vector2 slide(n: Vector2) const 🔗

Returns a new vector resulting from sliding this vector along a line with normal n. The resulting new vector is perpendicular to n, and is equivalent to this vector minus its projection on n. See also project().

Note: The vector n must be normalized. See also normalized().

Vector2 snapped(step: Vector2) const 🔗

Returns a new vector with each component snapped to the nearest multiple of the corresponding component in step. This can also be used to round the components to an arbitrary number of decimals.

Vector2 snappedf(step: float) const 🔗

Returns a new vector with each component snapped to the nearest multiple of step. This can also be used to round the components to an arbitrary number of decimals.

bool operator !=(right: Vector2) 🔗

Returns true if the vectors are not equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

Vector2 operator *(right: Transform2D) 🔗

Inversely transforms (multiplies) the Vector2 by the given Transform2D transformation matrix, under the assumption that the transformation basis is orthonormal (i.e. rotation/reflection is fine, scaling/skew is not).

vector * transform is equivalent to transform.inverse() * vector. See Transform2D.inverse().

For transforming by inverse of an affine transformation (e.g. with scaling) transform.affine_inverse() * vector can be used instead. See Transform2D.affine_inverse().

Vector2 operator *(right: Vector2) 🔗

Multiplies each component of the Vector2 by the components of the given Vector2.

Vector2 operator *(right: float) 🔗

Multiplies each component of the Vector2 by the given float.

Vector2 operator *(right: int) 🔗

Multiplies each component of the Vector2 by the given int.

Vector2 operator +(right: Vector2) 🔗

Adds each component of the Vector2 by the components of the given Vector2.

Vector2 operator -(right: Vector2) 🔗

Subtracts each component of the Vector2 by the components of the given Vector2.

Vector2 operator /(right: Vector2) 🔗

Divides each component of the Vector2 by the components of the given Vector2.

Vector2 operator /(right: float) 🔗

Divides each component of the Vector2 by the given float.

Vector2 operator /(right: int) 🔗

Divides each component of the Vector2 by the given int.

bool operator <(right: Vector2) 🔗

Compares two Vector2 vectors by first checking if the X value of the left vector is less than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator <=(right: Vector2) 🔗

Compares two Vector2 vectors by first checking if the X value of the left vector is less than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator ==(right: Vector2) 🔗

Returns true if the vectors are exactly equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator >(right: Vector2) 🔗

Compares two Vector2 vectors by first checking if the X value of the left vector is greater than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator >=(right: Vector2) 🔗

Compares two Vector2 vectors by first checking if the X value of the left vector is greater than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

float operator [](index: int) 🔗

Access vector components using their index. v[0] is equivalent to v.x, and v[1] is equivalent to v.y.

Vector2 operator unary+() 🔗

Returns the same value as if the + was not there. Unary + does nothing, but sometimes it can make your code more readable.

Vector2 operator unary-() 🔗

Returns the negative value of the Vector2. This is the same as writing Vector2(-v.x, -v.y). This operation flips the direction of the vector while keeping the same magnitude. With floats, the number zero can be either positive or negative.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
print(Vector2.from_angle(0)) # Prints (1.0, 0.0)
print(Vector2(1, 0).angle()) # Prints 0.0, which is the angle used above.
print(Vector2.from_angle(PI / 2)) # Prints (0.0, 1.0)
```

Example 2 (csharp):
```csharp
print(Vector2(10, 20) * Vector2(3, 4)) # Prints (30.0, 80.0)
```

Example 3 (csharp):
```csharp
print(Vector2(10, 20) + Vector2(3, 4)) # Prints (13.0, 24.0)
```

Example 4 (csharp):
```csharp
print(Vector2(10, 20) - Vector2(3, 4)) # Prints (7.0, 16.0)
```

---

## Vector3i

**URL:** https://docs.godotengine.org/en/stable/classes/class_vector3i.html

**Contents:**
- Vector3i
- Description
- Tutorials
- Properties
- Constructors
- Methods
- Operators
- Enumerations
- Constants
- Property Descriptions

A 3D vector using integer coordinates.

A 3-element structure that can be used to represent 3D grid coordinates or any other triplet of integers.

It uses integer coordinates and is therefore preferable to Vector3 when exact precision is required. Note that the values are limited to 32 bits, and unlike Vector3 this cannot be configured with an engine build option. Use int or PackedInt64Array if 64-bit values are needed.

Note: In a boolean context, a Vector3i will evaluate to false if it's equal to Vector3i(0, 0, 0). Otherwise, a Vector3i will always evaluate to true.

Math documentation index

3Blue1Brown Essence of Linear Algebra

Vector3i(from: Vector3i)

Vector3i(from: Vector3)

Vector3i(x: int, y: int, z: int)

clamp(min: Vector3i, max: Vector3i) const

clampi(min: int, max: int) const

distance_squared_to(to: Vector3i) const

distance_to(to: Vector3i) const

length_squared() const

max(with: Vector3i) const

max_axis_index() const

maxi(with: int) const

min(with: Vector3i) const

min_axis_index() const

mini(with: int) const

snapped(step: Vector3i) const

snappedi(step: int) const

operator !=(right: Vector3i)

operator %(right: Vector3i)

operator %(right: int)

operator *(right: Vector3i)

operator *(right: float)

operator *(right: int)

operator +(right: Vector3i)

operator -(right: Vector3i)

operator /(right: Vector3i)

operator /(right: float)

operator /(right: int)

operator <(right: Vector3i)

operator <=(right: Vector3i)

operator ==(right: Vector3i)

operator >(right: Vector3i)

operator >=(right: Vector3i)

operator [](index: int)

Enumerated value for the X axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the Y axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the Z axis. Returned by max_axis_index() and min_axis_index().

ZERO = Vector3i(0, 0, 0) 🔗

Zero vector, a vector with all components set to 0.

ONE = Vector3i(1, 1, 1) 🔗

One vector, a vector with all components set to 1.

MIN = Vector3i(-2147483648, -2147483648, -2147483648) 🔗

Min vector, a vector with all components equal to INT32_MIN. Can be used as a negative integer equivalent of Vector3.INF.

MAX = Vector3i(2147483647, 2147483647, 2147483647) 🔗

Max vector, a vector with all components equal to INT32_MAX. Can be used as an integer equivalent of Vector3.INF.

LEFT = Vector3i(-1, 0, 0) 🔗

Left unit vector. Represents the local direction of left, and the global direction of west.

RIGHT = Vector3i(1, 0, 0) 🔗

Right unit vector. Represents the local direction of right, and the global direction of east.

UP = Vector3i(0, 1, 0) 🔗

DOWN = Vector3i(0, -1, 0) 🔗

FORWARD = Vector3i(0, 0, -1) 🔗

Forward unit vector. Represents the local direction of forward, and the global direction of north.

BACK = Vector3i(0, 0, 1) 🔗

Back unit vector. Represents the local direction of back, and the global direction of south.

The vector's X component. Also accessible by using the index position [0].

The vector's Y component. Also accessible by using the index position [1].

The vector's Z component. Also accessible by using the index position [2].

Vector3i Vector3i() 🔗

Constructs a default-initialized Vector3i with all components set to 0.

Vector3i Vector3i(from: Vector3i)

Constructs a Vector3i as a copy of the given Vector3i.

Vector3i Vector3i(from: Vector3)

Constructs a new Vector3i from the given Vector3 by truncating components' fractional parts (rounding towards zero). For a different behavior consider passing the result of Vector3.ceil(), Vector3.floor() or Vector3.round() to this constructor instead.

Vector3i Vector3i(x: int, y: int, z: int)

Returns a Vector3i with the given components.

Vector3i abs() const 🔗

Returns a new vector with all components in absolute values (i.e. positive).

Vector3i clamp(min: Vector3i, max: Vector3i) const 🔗

Returns a new vector with all components clamped between the components of min and max, by running @GlobalScope.clamp() on each component.

Vector3i clampi(min: int, max: int) const 🔗

Returns a new vector with all components clamped between min and max, by running @GlobalScope.clamp() on each component.

int distance_squared_to(to: Vector3i) const 🔗

Returns the squared distance between this vector and to.

This method runs faster than distance_to(), so prefer it if you need to compare vectors or need the squared distance for some formula.

float distance_to(to: Vector3i) const 🔗

Returns the distance between this vector and to.

float length() const 🔗

Returns the length (magnitude) of this vector.

int length_squared() const 🔗

Returns the squared length (squared magnitude) of this vector.

This method runs faster than length(), so prefer it if you need to compare vectors or need the squared distance for some formula.

Vector3i max(with: Vector3i) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector3i(maxi(x, with.x), maxi(y, with.y), maxi(z, with.z)).

int max_axis_index() const 🔗

Returns the axis of the vector's highest value. See AXIS_* constants. If all components are equal, this method returns AXIS_X.

Vector3i maxi(with: int) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector3i(maxi(x, with), maxi(y, with), maxi(z, with)).

Vector3i min(with: Vector3i) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector3i(mini(x, with.x), mini(y, with.y), mini(z, with.z)).

int min_axis_index() const 🔗

Returns the axis of the vector's lowest value. See AXIS_* constants. If all components are equal, this method returns AXIS_Z.

Vector3i mini(with: int) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector3i(mini(x, with), mini(y, with), mini(z, with)).

Vector3i sign() const 🔗

Returns a new vector with each component set to 1 if it's positive, -1 if it's negative, and 0 if it's zero. The result is identical to calling @GlobalScope.sign() on each component.

Vector3i snapped(step: Vector3i) const 🔗

Returns a new vector with each component snapped to the closest multiple of the corresponding component in step.

Vector3i snappedi(step: int) const 🔗

Returns a new vector with each component snapped to the closest multiple of step.

bool operator !=(right: Vector3i) 🔗

Returns true if the vectors are not equal.

Vector3i operator %(right: Vector3i) 🔗

Gets the remainder of each component of the Vector3i with the components of the given Vector3i. This operation uses truncated division, which is often not desired as it does not work well with negative numbers. Consider using @GlobalScope.posmod() instead if you want to handle negative numbers.

Vector3i operator %(right: int) 🔗

Gets the remainder of each component of the Vector3i with the given int. This operation uses truncated division, which is often not desired as it does not work well with negative numbers. Consider using @GlobalScope.posmod() instead if you want to handle negative numbers.

Vector3i operator *(right: Vector3i) 🔗

Multiplies each component of the Vector3i by the components of the given Vector3i.

Vector3 operator *(right: float) 🔗

Multiplies each component of the Vector3i by the given float. Returns a Vector3.

Vector3i operator *(right: int) 🔗

Multiplies each component of the Vector3i by the given int.

Vector3i operator +(right: Vector3i) 🔗

Adds each component of the Vector3i by the components of the given Vector3i.

Vector3i operator -(right: Vector3i) 🔗

Subtracts each component of the Vector3i by the components of the given Vector3i.

Vector3i operator /(right: Vector3i) 🔗

Divides each component of the Vector3i by the components of the given Vector3i.

Vector3 operator /(right: float) 🔗

Divides each component of the Vector3i by the given float. Returns a Vector3.

Vector3i operator /(right: int) 🔗

Divides each component of the Vector3i by the given int.

bool operator <(right: Vector3i) 🔗

Compares two Vector3i vectors by first checking if the X value of the left vector is less than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, and then with the Z values. This operator is useful for sorting vectors.

bool operator <=(right: Vector3i) 🔗

Compares two Vector3i vectors by first checking if the X value of the left vector is less than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, and then with the Z values. This operator is useful for sorting vectors.

bool operator ==(right: Vector3i) 🔗

Returns true if the vectors are equal.

bool operator >(right: Vector3i) 🔗

Compares two Vector3i vectors by first checking if the X value of the left vector is greater than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, and then with the Z values. This operator is useful for sorting vectors.

bool operator >=(right: Vector3i) 🔗

Compares two Vector3i vectors by first checking if the X value of the left vector is greater than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, and then with the Z values. This operator is useful for sorting vectors.

int operator [](index: int) 🔗

Access vector components using their index. v[0] is equivalent to v.x, v[1] is equivalent to v.y, and v[2] is equivalent to v.z.

Vector3i operator unary+() 🔗

Returns the same value as if the + was not there. Unary + does nothing, but sometimes it can make your code more readable.

Vector3i operator unary-() 🔗

Returns the negative value of the Vector3i. This is the same as writing Vector3i(-v.x, -v.y, -v.z). This operation flips the direction of the vector while keeping the same magnitude.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
print(Vector3i(10, -20, 30) % Vector3i(7, 8, 9)) # Prints (3, -4, 3)
```

Example 2 (swift):
```swift
print(Vector3i(10, -20, 30) % 7) # Prints (3, -6, 2)
```

Example 3 (swift):
```swift
print(Vector3i(10, 20, 30) * Vector3i(3, 4, 5)) # Prints (30, 80, 150)
```

Example 4 (swift):
```swift
print(Vector3i(10, 15, 20) * 0.9) # Prints (9.0, 13.5, 18.0)
```

---

## Vector3

**URL:** https://docs.godotengine.org/en/stable/classes/class_vector3.html

**Contents:**
- Vector3
- Description
- Tutorials
- Properties
- Constructors
- Methods
- Operators
- Enumerations
- Constants
- Property Descriptions

A 3D vector using floating-point coordinates.

A 3-element structure that can be used to represent 3D coordinates or any other triplet of numeric values.

It uses floating-point coordinates. By default, these floating-point values use 32-bit precision, unlike float which is always 64-bit. If double precision is needed, compile the engine with the option precision=double.

See Vector3i for its integer counterpart.

Note: In a boolean context, a Vector3 will evaluate to false if it's equal to Vector3(0, 0, 0). Otherwise, a Vector3 will always evaluate to true.

Math documentation index

3Blue1Brown Essence of Linear Algebra

Matrix Transform Demo

Vector3(from: Vector3)

Vector3(from: Vector3i)

Vector3(x: float, y: float, z: float)

angle_to(to: Vector3) const

bezier_derivative(control_1: Vector3, control_2: Vector3, end: Vector3, t: float) const

bezier_interpolate(control_1: Vector3, control_2: Vector3, end: Vector3, t: float) const

bounce(n: Vector3) const

clamp(min: Vector3, max: Vector3) const

clampf(min: float, max: float) const

cross(with: Vector3) const

cubic_interpolate(b: Vector3, pre_a: Vector3, post_b: Vector3, weight: float) const

cubic_interpolate_in_time(b: Vector3, pre_a: Vector3, post_b: Vector3, weight: float, b_t: float, pre_a_t: float, post_b_t: float) const

direction_to(to: Vector3) const

distance_squared_to(to: Vector3) const

distance_to(to: Vector3) const

dot(with: Vector3) const

is_equal_approx(to: Vector3) const

is_normalized() const

is_zero_approx() const

length_squared() const

lerp(to: Vector3, weight: float) const

limit_length(length: float = 1.0) const

max(with: Vector3) const

max_axis_index() const

maxf(with: float) const

min(with: Vector3) const

min_axis_index() const

minf(with: float) const

move_toward(to: Vector3, delta: float) const

octahedron_decode(uv: Vector2) static

octahedron_encode() const

outer(with: Vector3) const

posmod(mod: float) const

posmodv(modv: Vector3) const

project(b: Vector3) const

reflect(n: Vector3) const

rotated(axis: Vector3, angle: float) const

signed_angle_to(to: Vector3, axis: Vector3) const

slerp(to: Vector3, weight: float) const

slide(n: Vector3) const

snapped(step: Vector3) const

snappedf(step: float) const

operator !=(right: Vector3)

operator *(right: Basis)

operator *(right: Quaternion)

operator *(right: Transform3D)

operator *(right: Vector3)

operator *(right: float)

operator *(right: int)

operator +(right: Vector3)

operator -(right: Vector3)

operator /(right: Vector3)

operator /(right: float)

operator /(right: int)

operator <(right: Vector3)

operator <=(right: Vector3)

operator ==(right: Vector3)

operator >(right: Vector3)

operator >=(right: Vector3)

operator [](index: int)

Enumerated value for the X axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the Y axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the Z axis. Returned by max_axis_index() and min_axis_index().

ZERO = Vector3(0, 0, 0) 🔗

Zero vector, a vector with all components set to 0.

ONE = Vector3(1, 1, 1) 🔗

One vector, a vector with all components set to 1.

INF = Vector3(inf, inf, inf) 🔗

Infinity vector, a vector with all components set to @GDScript.INF.

LEFT = Vector3(-1, 0, 0) 🔗

Left unit vector. Represents the local direction of left, and the global direction of west.

RIGHT = Vector3(1, 0, 0) 🔗

Right unit vector. Represents the local direction of right, and the global direction of east.

UP = Vector3(0, 1, 0) 🔗

DOWN = Vector3(0, -1, 0) 🔗

FORWARD = Vector3(0, 0, -1) 🔗

Forward unit vector. Represents the local direction of forward, and the global direction of north. Keep in mind that the forward direction for lights, cameras, etc is different from 3D assets like characters, which face towards the camera by convention. Use MODEL_FRONT and similar constants when working in 3D asset space.

BACK = Vector3(0, 0, 1) 🔗

Back unit vector. Represents the local direction of back, and the global direction of south.

MODEL_LEFT = Vector3(1, 0, 0) 🔗

Unit vector pointing towards the left side of imported 3D assets.

MODEL_RIGHT = Vector3(-1, 0, 0) 🔗

Unit vector pointing towards the right side of imported 3D assets.

MODEL_TOP = Vector3(0, 1, 0) 🔗

Unit vector pointing towards the top side (up) of imported 3D assets.

MODEL_BOTTOM = Vector3(0, -1, 0) 🔗

Unit vector pointing towards the bottom side (down) of imported 3D assets.

MODEL_FRONT = Vector3(0, 0, 1) 🔗

Unit vector pointing towards the front side (facing forward) of imported 3D assets.

MODEL_REAR = Vector3(0, 0, -1) 🔗

Unit vector pointing towards the rear side (back) of imported 3D assets.

The vector's X component. Also accessible by using the index position [0].

The vector's Y component. Also accessible by using the index position [1].

The vector's Z component. Also accessible by using the index position [2].

Constructs a default-initialized Vector3 with all components set to 0.

Vector3 Vector3(from: Vector3)

Constructs a Vector3 as a copy of the given Vector3.

Vector3 Vector3(from: Vector3i)

Constructs a new Vector3 from Vector3i.

Vector3 Vector3(x: float, y: float, z: float)

Returns a Vector3 with the given components.

Vector3 abs() const 🔗

Returns a new vector with all components in absolute values (i.e. positive).

float angle_to(to: Vector3) const 🔗

Returns the unsigned minimum angle to the given vector, in radians.

Vector3 bezier_derivative(control_1: Vector3, control_2: Vector3, end: Vector3, t: float) const 🔗

Returns the derivative at the given t on the Bézier curve defined by this vector and the given control_1, control_2, and end points.

Vector3 bezier_interpolate(control_1: Vector3, control_2: Vector3, end: Vector3, t: float) const 🔗

Returns the point at the given t on the Bézier curve defined by this vector and the given control_1, control_2, and end points.

Vector3 bounce(n: Vector3) const 🔗

Returns the vector "bounced off" from a plane defined by the given normal n.

Note: bounce() performs the operation that most engines and frameworks call reflect().

Vector3 ceil() const 🔗

Returns a new vector with all components rounded up (towards positive infinity).

Vector3 clamp(min: Vector3, max: Vector3) const 🔗

Returns a new vector with all components clamped between the components of min and max, by running @GlobalScope.clamp() on each component.

Vector3 clampf(min: float, max: float) const 🔗

Returns a new vector with all components clamped between min and max, by running @GlobalScope.clamp() on each component.

Vector3 cross(with: Vector3) const 🔗

Returns the cross product of this vector and with.

This returns a vector perpendicular to both this and with, which would be the normal vector of the plane defined by the two vectors. As there are two such vectors, in opposite directions, this method returns the vector defined by a right-handed coordinate system. If the two vectors are parallel this returns an empty vector, making it useful for testing if two vectors are parallel.

Vector3 cubic_interpolate(b: Vector3, pre_a: Vector3, post_b: Vector3, weight: float) const 🔗

Performs a cubic interpolation between this vector and b using pre_a and post_b as handles, and returns the result at position weight. weight is on the range of 0.0 to 1.0, representing the amount of interpolation.

Vector3 cubic_interpolate_in_time(b: Vector3, pre_a: Vector3, post_b: Vector3, weight: float, b_t: float, pre_a_t: float, post_b_t: float) const 🔗

Performs a cubic interpolation between this vector and b using pre_a and post_b as handles, and returns the result at position weight. weight is on the range of 0.0 to 1.0, representing the amount of interpolation.

It can perform smoother interpolation than cubic_interpolate() by the time values.

Vector3 direction_to(to: Vector3) const 🔗

Returns the normalized vector pointing from this vector to to. This is equivalent to using (b - a).normalized().

float distance_squared_to(to: Vector3) const 🔗

Returns the squared distance between this vector and to.

This method runs faster than distance_to(), so prefer it if you need to compare vectors or need the squared distance for some formula.

float distance_to(to: Vector3) const 🔗

Returns the distance between this vector and to.

float dot(with: Vector3) const 🔗

Returns the dot product of this vector and with. This can be used to compare the angle between two vectors. For example, this can be used to determine whether an enemy is facing the player.

The dot product will be 0 for a right angle (90 degrees), greater than 0 for angles narrower than 90 degrees and lower than 0 for angles wider than 90 degrees.

When using unit (normalized) vectors, the result will always be between -1.0 (180 degree angle) when the vectors are facing opposite directions, and 1.0 (0 degree angle) when the vectors are aligned.

Note: a.dot(b) is equivalent to b.dot(a).

Vector3 floor() const 🔗

Returns a new vector with all components rounded down (towards negative infinity).

Vector3 inverse() const 🔗

Returns the inverse of the vector. This is the same as Vector3(1.0 / v.x, 1.0 / v.y, 1.0 / v.z).

bool is_equal_approx(to: Vector3) const 🔗

Returns true if this vector and to are approximately equal, by running @GlobalScope.is_equal_approx() on each component.

bool is_finite() const 🔗

Returns true if this vector is finite, by calling @GlobalScope.is_finite() on each component.

bool is_normalized() const 🔗

Returns true if the vector is normalized, i.e. its length is approximately equal to 1.

bool is_zero_approx() const 🔗

Returns true if this vector's values are approximately zero, by running @GlobalScope.is_zero_approx() on each component.

This method is faster than using is_equal_approx() with one value as a zero vector.

float length() const 🔗

Returns the length (magnitude) of this vector.

float length_squared() const 🔗

Returns the squared length (squared magnitude) of this vector.

This method runs faster than length(), so prefer it if you need to compare vectors or need the squared distance for some formula.

Vector3 lerp(to: Vector3, weight: float) const 🔗

Returns the result of the linear interpolation between this vector and to by amount weight. weight is on the range of 0.0 to 1.0, representing the amount of interpolation.

Vector3 limit_length(length: float = 1.0) const 🔗

Returns the vector with a maximum length by limiting its length to length. If the vector is non-finite, the result is undefined.

Vector3 max(with: Vector3) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector3(maxf(x, with.x), maxf(y, with.y), maxf(z, with.z)).

int max_axis_index() const 🔗

Returns the axis of the vector's highest value. See AXIS_* constants. If all components are equal, this method returns AXIS_X.

Vector3 maxf(with: float) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector3(maxf(x, with), maxf(y, with), maxf(z, with)).

Vector3 min(with: Vector3) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector3(minf(x, with.x), minf(y, with.y), minf(z, with.z)).

int min_axis_index() const 🔗

Returns the axis of the vector's lowest value. See AXIS_* constants. If all components are equal, this method returns AXIS_Z.

Vector3 minf(with: float) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector3(minf(x, with), minf(y, with), minf(z, with)).

Vector3 move_toward(to: Vector3, delta: float) const 🔗

Returns a new vector moved toward to by the fixed delta amount. Will not go past the final value.

Vector3 normalized() const 🔗

Returns the result of scaling the vector to unit length. Equivalent to v / v.length(). Returns (0, 0, 0) if v.length() == 0. See also is_normalized().

Note: This function may return incorrect values if the input vector length is near zero.

Vector3 octahedron_decode(uv: Vector2) static 🔗

Returns the Vector3 from an octahedral-compressed form created using octahedron_encode() (stored as a Vector2).

Vector2 octahedron_encode() const 🔗

Returns the octahedral-encoded (oct32) form of this Vector3 as a Vector2. Since a Vector2 occupies 1/3 less memory compared to Vector3, this form of compression can be used to pass greater amounts of normalized() Vector3s without increasing storage or memory requirements. See also octahedron_decode().

Note: octahedron_encode() can only be used for normalized() vectors. octahedron_encode() does not check whether this Vector3 is normalized, and will return a value that does not decompress to the original value if the Vector3 is not normalized.

Note: Octahedral compression is lossy, although visual differences are rarely perceptible in real world scenarios.

Basis outer(with: Vector3) const 🔗

Returns the outer product with with.

Vector3 posmod(mod: float) const 🔗

Returns a vector composed of the @GlobalScope.fposmod() of this vector's components and mod.

Vector3 posmodv(modv: Vector3) const 🔗

Returns a vector composed of the @GlobalScope.fposmod() of this vector's components and modv's components.

Vector3 project(b: Vector3) const 🔗

Returns a new vector resulting from projecting this vector onto the given vector b. The resulting new vector is parallel to b. See also slide().

Note: If the vector b is a zero vector, the components of the resulting new vector will be @GDScript.NAN.

Vector3 reflect(n: Vector3) const 🔗

Returns the result of reflecting the vector through a plane defined by the given normal vector n.

Note: reflect() differs from what other engines and frameworks call reflect(). In other engines, reflect() returns the result of the vector reflected by the given plane. The reflection thus passes through the given normal. While in Godot the reflection passes through the plane and can be thought of as bouncing off the normal. See also bounce() which does what most engines call reflect().

Vector3 rotated(axis: Vector3, angle: float) const 🔗

Returns the result of rotating this vector around a given axis by angle (in radians). The axis must be a normalized vector. See also @GlobalScope.deg_to_rad().

Vector3 round() const 🔗

Returns a new vector with all components rounded to the nearest integer, with halfway cases rounded away from zero.

Vector3 sign() const 🔗

Returns a new vector with each component set to 1.0 if it's positive, -1.0 if it's negative, and 0.0 if it's zero. The result is identical to calling @GlobalScope.sign() on each component.

float signed_angle_to(to: Vector3, axis: Vector3) const 🔗

Returns the signed angle to the given vector, in radians. The sign of the angle is positive in a counter-clockwise direction and negative in a clockwise direction when viewed from the side specified by the axis.

Vector3 slerp(to: Vector3, weight: float) const 🔗

Returns the result of spherical linear interpolation between this vector and to, by amount weight. weight is on the range of 0.0 to 1.0, representing the amount of interpolation.

This method also handles interpolating the lengths if the input vectors have different lengths. For the special case of one or both input vectors having zero length, this method behaves like lerp().

Vector3 slide(n: Vector3) const 🔗

Returns a new vector resulting from sliding this vector along a plane with normal n. The resulting new vector is perpendicular to n, and is equivalent to this vector minus its projection on n. See also project().

Note: The vector n must be normalized. See also normalized().

Vector3 snapped(step: Vector3) const 🔗

Returns a new vector with each component snapped to the nearest multiple of the corresponding component in step. This can also be used to round the components to an arbitrary number of decimals.

Vector3 snappedf(step: float) const 🔗

Returns a new vector with each component snapped to the nearest multiple of step. This can also be used to round the components to an arbitrary number of decimals.

bool operator !=(right: Vector3) 🔗

Returns true if the vectors are not equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

Vector3 operator *(right: Basis) 🔗

Inversely transforms (multiplies) the Vector3 by the given Basis matrix, under the assumption that the basis is orthonormal (i.e. rotation/reflection is fine, scaling/skew is not).

vector * basis is equivalent to basis.transposed() * vector. See Basis.transposed().

For transforming by inverse of a non-orthonormal basis (e.g. with scaling) basis.inverse() * vector can be used instead. See Basis.inverse().

Vector3 operator *(right: Quaternion) 🔗

Inversely transforms (multiplies) the Vector3 by the given Quaternion.

vector * quaternion is equivalent to quaternion.inverse() * vector. See Quaternion.inverse().

Vector3 operator *(right: Transform3D) 🔗

Inversely transforms (multiplies) the Vector3 by the given Transform3D transformation matrix, under the assumption that the transformation basis is orthonormal (i.e. rotation/reflection is fine, scaling/skew is not).

vector * transform is equivalent to transform.inverse() * vector. See Transform3D.inverse().

For transforming by inverse of an affine transformation (e.g. with scaling) transform.affine_inverse() * vector can be used instead. See Transform3D.affine_inverse().

Vector3 operator *(right: Vector3) 🔗

Multiplies each component of the Vector3 by the components of the given Vector3.

Vector3 operator *(right: float) 🔗

Multiplies each component of the Vector3 by the given float.

Vector3 operator *(right: int) 🔗

Multiplies each component of the Vector3 by the given int.

Vector3 operator +(right: Vector3) 🔗

Adds each component of the Vector3 by the components of the given Vector3.

Vector3 operator -(right: Vector3) 🔗

Subtracts each component of the Vector3 by the components of the given Vector3.

Vector3 operator /(right: Vector3) 🔗

Divides each component of the Vector3 by the components of the given Vector3.

Vector3 operator /(right: float) 🔗

Divides each component of the Vector3 by the given float.

Vector3 operator /(right: int) 🔗

Divides each component of the Vector3 by the given int.

bool operator <(right: Vector3) 🔗

Compares two Vector3 vectors by first checking if the X value of the left vector is less than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, and then with the Z values. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator <=(right: Vector3) 🔗

Compares two Vector3 vectors by first checking if the X value of the left vector is less than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, and then with the Z values. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator ==(right: Vector3) 🔗

Returns true if the vectors are exactly equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator >(right: Vector3) 🔗

Compares two Vector3 vectors by first checking if the X value of the left vector is greater than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, and then with the Z values. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator >=(right: Vector3) 🔗

Compares two Vector3 vectors by first checking if the X value of the left vector is greater than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, and then with the Z values. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

float operator [](index: int) 🔗

Access vector components using their index. v[0] is equivalent to v.x, v[1] is equivalent to v.y, and v[2] is equivalent to v.z.

Vector3 operator unary+() 🔗

Returns the same value as if the + was not there. Unary + does nothing, but sometimes it can make your code more readable.

Vector3 operator unary-() 🔗

Returns the negative value of the Vector3. This is the same as writing Vector3(-v.x, -v.y, -v.z). This operation flips the direction of the vector while keeping the same magnitude. With floats, the number zero can be either positive or negative.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
print(Vector3(10, 20, 30) * Vector3(3, 4, 5)) # Prints (30.0, 80.0, 150.0)
```

Example 2 (csharp):
```csharp
print(Vector3(10, 20, 30) + Vector3(3, 4, 5)) # Prints (13.0, 24.0, 35.0)
```

Example 3 (csharp):
```csharp
print(Vector3(10, 20, 30) - Vector3(3, 4, 5)) # Prints (7.0, 16.0, 25.0)
```

Example 4 (csharp):
```csharp
print(Vector3(10, 20, 30) / Vector3(2, 5, 3)) # Prints (5.0, 4.0, 10.0)
```

---

## Vector4i

**URL:** https://docs.godotengine.org/en/stable/classes/class_vector4i.html

**Contents:**
- Vector4i
- Description
- Properties
- Constructors
- Methods
- Operators
- Enumerations
- Constants
- Property Descriptions
- Constructor Descriptions

A 4D vector using integer coordinates.

A 4-element structure that can be used to represent 4D grid coordinates or any other quadruplet of integers.

It uses integer coordinates and is therefore preferable to Vector4 when exact precision is required. Note that the values are limited to 32 bits, and unlike Vector4 this cannot be configured with an engine build option. Use int or PackedInt64Array if 64-bit values are needed.

Note: In a boolean context, a Vector4i will evaluate to false if it's equal to Vector4i(0, 0, 0, 0). Otherwise, a Vector4i will always evaluate to true.

Vector4i(from: Vector4i)

Vector4i(from: Vector4)

Vector4i(x: int, y: int, z: int, w: int)

clamp(min: Vector4i, max: Vector4i) const

clampi(min: int, max: int) const

distance_squared_to(to: Vector4i) const

distance_to(to: Vector4i) const

length_squared() const

max(with: Vector4i) const

max_axis_index() const

maxi(with: int) const

min(with: Vector4i) const

min_axis_index() const

mini(with: int) const

snapped(step: Vector4i) const

snappedi(step: int) const

operator !=(right: Vector4i)

operator %(right: Vector4i)

operator %(right: int)

operator *(right: Vector4i)

operator *(right: float)

operator *(right: int)

operator +(right: Vector4i)

operator -(right: Vector4i)

operator /(right: Vector4i)

operator /(right: float)

operator /(right: int)

operator <(right: Vector4i)

operator <=(right: Vector4i)

operator ==(right: Vector4i)

operator >(right: Vector4i)

operator >=(right: Vector4i)

operator [](index: int)

Enumerated value for the X axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the Y axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the Z axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the W axis. Returned by max_axis_index() and min_axis_index().

ZERO = Vector4i(0, 0, 0, 0) 🔗

Zero vector, a vector with all components set to 0.

ONE = Vector4i(1, 1, 1, 1) 🔗

One vector, a vector with all components set to 1.

MIN = Vector4i(-2147483648, -2147483648, -2147483648, -2147483648) 🔗

Min vector, a vector with all components equal to INT32_MIN. Can be used as a negative integer equivalent of Vector4.INF.

MAX = Vector4i(2147483647, 2147483647, 2147483647, 2147483647) 🔗

Max vector, a vector with all components equal to INT32_MAX. Can be used as an integer equivalent of Vector4.INF.

The vector's W component. Also accessible by using the index position [3].

The vector's X component. Also accessible by using the index position [0].

The vector's Y component. Also accessible by using the index position [1].

The vector's Z component. Also accessible by using the index position [2].

Vector4i Vector4i() 🔗

Constructs a default-initialized Vector4i with all components set to 0.

Vector4i Vector4i(from: Vector4i)

Constructs a Vector4i as a copy of the given Vector4i.

Vector4i Vector4i(from: Vector4)

Constructs a new Vector4i from the given Vector4 by truncating components' fractional parts (rounding towards zero). For a different behavior consider passing the result of Vector4.ceil(), Vector4.floor() or Vector4.round() to this constructor instead.

Vector4i Vector4i(x: int, y: int, z: int, w: int)

Returns a Vector4i with the given components.

Vector4i abs() const 🔗

Returns a new vector with all components in absolute values (i.e. positive).

Vector4i clamp(min: Vector4i, max: Vector4i) const 🔗

Returns a new vector with all components clamped between the components of min and max, by running @GlobalScope.clamp() on each component.

Vector4i clampi(min: int, max: int) const 🔗

Returns a new vector with all components clamped between min and max, by running @GlobalScope.clamp() on each component.

int distance_squared_to(to: Vector4i) const 🔗

Returns the squared distance between this vector and to.

This method runs faster than distance_to(), so prefer it if you need to compare vectors or need the squared distance for some formula.

float distance_to(to: Vector4i) const 🔗

Returns the distance between this vector and to.

float length() const 🔗

Returns the length (magnitude) of this vector.

int length_squared() const 🔗

Returns the squared length (squared magnitude) of this vector.

This method runs faster than length(), so prefer it if you need to compare vectors or need the squared distance for some formula.

Vector4i max(with: Vector4i) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector4i(maxi(x, with.x), maxi(y, with.y), maxi(z, with.z), maxi(w, with.w)).

int max_axis_index() const 🔗

Returns the axis of the vector's highest value. See AXIS_* constants. If all components are equal, this method returns AXIS_X.

Vector4i maxi(with: int) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector4i(maxi(x, with), maxi(y, with), maxi(z, with), maxi(w, with)).

Vector4i min(with: Vector4i) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector4i(mini(x, with.x), mini(y, with.y), mini(z, with.z), mini(w, with.w)).

int min_axis_index() const 🔗

Returns the axis of the vector's lowest value. See AXIS_* constants. If all components are equal, this method returns AXIS_W.

Vector4i mini(with: int) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector4i(mini(x, with), mini(y, with), mini(z, with), mini(w, with)).

Vector4i sign() const 🔗

Returns a new vector with each component set to 1 if it's positive, -1 if it's negative, and 0 if it's zero. The result is identical to calling @GlobalScope.sign() on each component.

Vector4i snapped(step: Vector4i) const 🔗

Returns a new vector with each component snapped to the closest multiple of the corresponding component in step.

Vector4i snappedi(step: int) const 🔗

Returns a new vector with each component snapped to the closest multiple of step.

bool operator !=(right: Vector4i) 🔗

Returns true if the vectors are not equal.

Vector4i operator %(right: Vector4i) 🔗

Gets the remainder of each component of the Vector4i with the components of the given Vector4i. This operation uses truncated division, which is often not desired as it does not work well with negative numbers. Consider using @GlobalScope.posmod() instead if you want to handle negative numbers.

Vector4i operator %(right: int) 🔗

Gets the remainder of each component of the Vector4i with the given int. This operation uses truncated division, which is often not desired as it does not work well with negative numbers. Consider using @GlobalScope.posmod() instead if you want to handle negative numbers.

Vector4i operator *(right: Vector4i) 🔗

Multiplies each component of the Vector4i by the components of the given Vector4i.

Vector4 operator *(right: float) 🔗

Multiplies each component of the Vector4i by the given float.

Returns a Vector4 value due to floating-point operations.

Vector4i operator *(right: int) 🔗

Multiplies each component of the Vector4i by the given int.

Vector4i operator +(right: Vector4i) 🔗

Adds each component of the Vector4i by the components of the given Vector4i.

Vector4i operator -(right: Vector4i) 🔗

Subtracts each component of the Vector4i by the components of the given Vector4i.

Vector4i operator /(right: Vector4i) 🔗

Divides each component of the Vector4i by the components of the given Vector4i.

Vector4 operator /(right: float) 🔗

Divides each component of the Vector4i by the given float.

Returns a Vector4 value due to floating-point operations.

Vector4i operator /(right: int) 🔗

Divides each component of the Vector4i by the given int.

bool operator <(right: Vector4i) 🔗

Compares two Vector4i vectors by first checking if the X value of the left vector is less than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, Z values of the two vectors, and then with the W values. This operator is useful for sorting vectors.

bool operator <=(right: Vector4i) 🔗

Compares two Vector4i vectors by first checking if the X value of the left vector is less than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, Z values of the two vectors, and then with the W values. This operator is useful for sorting vectors.

bool operator ==(right: Vector4i) 🔗

Returns true if the vectors are exactly equal.

bool operator >(right: Vector4i) 🔗

Compares two Vector4i vectors by first checking if the X value of the left vector is greater than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, Z values of the two vectors, and then with the W values. This operator is useful for sorting vectors.

bool operator >=(right: Vector4i) 🔗

Compares two Vector4i vectors by first checking if the X value of the left vector is greater than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, Z values of the two vectors, and then with the W values. This operator is useful for sorting vectors.

int operator [](index: int) 🔗

Access vector components using their index. v[0] is equivalent to v.x, v[1] is equivalent to v.y, v[2] is equivalent to v.z, and v[3] is equivalent to v.w.

Vector4i operator unary+() 🔗

Returns the same value as if the + was not there. Unary + does nothing, but sometimes it can make your code more readable.

Vector4i operator unary-() 🔗

Returns the negative value of the Vector4i. This is the same as writing Vector4i(-v.x, -v.y, -v.z, -v.w). This operation flips the direction of the vector while keeping the same magnitude.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
print(Vector4i(10, -20, 30, -40) % Vector4i(7, 8, 9, 10)) # Prints (3, -4, 3, 0)
```

Example 2 (swift):
```swift
print(Vector4i(10, -20, 30, -40) % 7) # Prints (3, -6, 2, -5)
```

Example 3 (swift):
```swift
print(Vector4i(10, 20, 30, 40) * Vector4i(3, 4, 5, 6)) # Prints (30, 80, 150, 240)
```

Example 4 (swift):
```swift
print(Vector4i(10, 20, 30, 40) * 2) # Prints (20.0, 40.0, 60.0, 80.0)
```

---

## Vector4

**URL:** https://docs.godotengine.org/en/stable/classes/class_vector4.html

**Contents:**
- Vector4
- Description
- Properties
- Constructors
- Methods
- Operators
- Enumerations
- Constants
- Property Descriptions
- Constructor Descriptions

A 4D vector using floating-point coordinates.

A 4-element structure that can be used to represent 4D coordinates or any other quadruplet of numeric values.

It uses floating-point coordinates. By default, these floating-point values use 32-bit precision, unlike float which is always 64-bit. If double precision is needed, compile the engine with the option precision=double.

See Vector4i for its integer counterpart.

Note: In a boolean context, a Vector4 will evaluate to false if it's equal to Vector4(0, 0, 0, 0). Otherwise, a Vector4 will always evaluate to true.

Vector4(from: Vector4)

Vector4(from: Vector4i)

Vector4(x: float, y: float, z: float, w: float)

clamp(min: Vector4, max: Vector4) const

clampf(min: float, max: float) const

cubic_interpolate(b: Vector4, pre_a: Vector4, post_b: Vector4, weight: float) const

cubic_interpolate_in_time(b: Vector4, pre_a: Vector4, post_b: Vector4, weight: float, b_t: float, pre_a_t: float, post_b_t: float) const

direction_to(to: Vector4) const

distance_squared_to(to: Vector4) const

distance_to(to: Vector4) const

dot(with: Vector4) const

is_equal_approx(to: Vector4) const

is_normalized() const

is_zero_approx() const

length_squared() const

lerp(to: Vector4, weight: float) const

max(with: Vector4) const

max_axis_index() const

maxf(with: float) const

min(with: Vector4) const

min_axis_index() const

minf(with: float) const

posmod(mod: float) const

posmodv(modv: Vector4) const

snapped(step: Vector4) const

snappedf(step: float) const

operator !=(right: Vector4)

operator *(right: Projection)

operator *(right: Vector4)

operator *(right: float)

operator *(right: int)

operator +(right: Vector4)

operator -(right: Vector4)

operator /(right: Vector4)

operator /(right: float)

operator /(right: int)

operator <(right: Vector4)

operator <=(right: Vector4)

operator ==(right: Vector4)

operator >(right: Vector4)

operator >=(right: Vector4)

operator [](index: int)

Enumerated value for the X axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the Y axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the Z axis. Returned by max_axis_index() and min_axis_index().

Enumerated value for the W axis. Returned by max_axis_index() and min_axis_index().

ZERO = Vector4(0, 0, 0, 0) 🔗

Zero vector, a vector with all components set to 0.

ONE = Vector4(1, 1, 1, 1) 🔗

One vector, a vector with all components set to 1.

INF = Vector4(inf, inf, inf, inf) 🔗

Infinity vector, a vector with all components set to @GDScript.INF.

The vector's W component. Also accessible by using the index position [3].

The vector's X component. Also accessible by using the index position [0].

The vector's Y component. Also accessible by using the index position [1].

The vector's Z component. Also accessible by using the index position [2].

Constructs a default-initialized Vector4 with all components set to 0.

Vector4 Vector4(from: Vector4)

Constructs a Vector4 as a copy of the given Vector4.

Vector4 Vector4(from: Vector4i)

Constructs a new Vector4 from the given Vector4i.

Vector4 Vector4(x: float, y: float, z: float, w: float)

Returns a Vector4 with the given components.

Vector4 abs() const 🔗

Returns a new vector with all components in absolute values (i.e. positive).

Vector4 ceil() const 🔗

Returns a new vector with all components rounded up (towards positive infinity).

Vector4 clamp(min: Vector4, max: Vector4) const 🔗

Returns a new vector with all components clamped between the components of min and max, by running @GlobalScope.clamp() on each component.

Vector4 clampf(min: float, max: float) const 🔗

Returns a new vector with all components clamped between min and max, by running @GlobalScope.clamp() on each component.

Vector4 cubic_interpolate(b: Vector4, pre_a: Vector4, post_b: Vector4, weight: float) const 🔗

Performs a cubic interpolation between this vector and b using pre_a and post_b as handles, and returns the result at position weight. weight is on the range of 0.0 to 1.0, representing the amount of interpolation.

Vector4 cubic_interpolate_in_time(b: Vector4, pre_a: Vector4, post_b: Vector4, weight: float, b_t: float, pre_a_t: float, post_b_t: float) const 🔗

Performs a cubic interpolation between this vector and b using pre_a and post_b as handles, and returns the result at position weight. weight is on the range of 0.0 to 1.0, representing the amount of interpolation.

It can perform smoother interpolation than cubic_interpolate() by the time values.

Vector4 direction_to(to: Vector4) const 🔗

Returns the normalized vector pointing from this vector to to. This is equivalent to using (b - a).normalized().

float distance_squared_to(to: Vector4) const 🔗

Returns the squared distance between this vector and to.

This method runs faster than distance_to(), so prefer it if you need to compare vectors or need the squared distance for some formula.

float distance_to(to: Vector4) const 🔗

Returns the distance between this vector and to.

float dot(with: Vector4) const 🔗

Returns the dot product of this vector and with.

Vector4 floor() const 🔗

Returns a new vector with all components rounded down (towards negative infinity).

Vector4 inverse() const 🔗

Returns the inverse of the vector. This is the same as Vector4(1.0 / v.x, 1.0 / v.y, 1.0 / v.z, 1.0 / v.w).

bool is_equal_approx(to: Vector4) const 🔗

Returns true if this vector and to are approximately equal, by running @GlobalScope.is_equal_approx() on each component.

bool is_finite() const 🔗

Returns true if this vector is finite, by calling @GlobalScope.is_finite() on each component.

bool is_normalized() const 🔗

Returns true if the vector is normalized, i.e. its length is approximately equal to 1.

bool is_zero_approx() const 🔗

Returns true if this vector's values are approximately zero, by running @GlobalScope.is_zero_approx() on each component.

This method is faster than using is_equal_approx() with one value as a zero vector.

float length() const 🔗

Returns the length (magnitude) of this vector.

float length_squared() const 🔗

Returns the squared length (squared magnitude) of this vector.

This method runs faster than length(), so prefer it if you need to compare vectors or need the squared distance for some formula.

Vector4 lerp(to: Vector4, weight: float) const 🔗

Returns the result of the linear interpolation between this vector and to by amount weight. weight is on the range of 0.0 to 1.0, representing the amount of interpolation.

Vector4 max(with: Vector4) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector4(maxf(x, with.x), maxf(y, with.y), maxf(z, with.z), maxf(w, with.w)).

int max_axis_index() const 🔗

Returns the axis of the vector's highest value. See AXIS_* constants. If all components are equal, this method returns AXIS_X.

Vector4 maxf(with: float) const 🔗

Returns the component-wise maximum of this and with, equivalent to Vector4(maxf(x, with), maxf(y, with), maxf(z, with), maxf(w, with)).

Vector4 min(with: Vector4) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector4(minf(x, with.x), minf(y, with.y), minf(z, with.z), minf(w, with.w)).

int min_axis_index() const 🔗

Returns the axis of the vector's lowest value. See AXIS_* constants. If all components are equal, this method returns AXIS_W.

Vector4 minf(with: float) const 🔗

Returns the component-wise minimum of this and with, equivalent to Vector4(minf(x, with), minf(y, with), minf(z, with), minf(w, with)).

Vector4 normalized() const 🔗

Returns the result of scaling the vector to unit length. Equivalent to v / v.length(). Returns (0, 0, 0, 0) if v.length() == 0. See also is_normalized().

Note: This function may return incorrect values if the input vector length is near zero.

Vector4 posmod(mod: float) const 🔗

Returns a vector composed of the @GlobalScope.fposmod() of this vector's components and mod.

Vector4 posmodv(modv: Vector4) const 🔗

Returns a vector composed of the @GlobalScope.fposmod() of this vector's components and modv's components.

Vector4 round() const 🔗

Returns a new vector with all components rounded to the nearest integer, with halfway cases rounded away from zero.

Vector4 sign() const 🔗

Returns a new vector with each component set to 1.0 if it's positive, -1.0 if it's negative, and 0.0 if it's zero. The result is identical to calling @GlobalScope.sign() on each component.

Vector4 snapped(step: Vector4) const 🔗

Returns a new vector with each component snapped to the nearest multiple of the corresponding component in step. This can also be used to round the components to an arbitrary number of decimals.

Vector4 snappedf(step: float) const 🔗

Returns a new vector with each component snapped to the nearest multiple of step. This can also be used to round the components to an arbitrary number of decimals.

bool operator !=(right: Vector4) 🔗

Returns true if the vectors are not equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

Vector4 operator *(right: Projection) 🔗

Transforms (multiplies) the Vector4 by the transpose of the given Projection matrix.

For transforming by inverse of a projection projection.inverse() * vector can be used instead. See Projection.inverse().

Vector4 operator *(right: Vector4) 🔗

Multiplies each component of the Vector4 by the components of the given Vector4.

Vector4 operator *(right: float) 🔗

Multiplies each component of the Vector4 by the given float.

Vector4 operator *(right: int) 🔗

Multiplies each component of the Vector4 by the given int.

Vector4 operator +(right: Vector4) 🔗

Adds each component of the Vector4 by the components of the given Vector4.

Vector4 operator -(right: Vector4) 🔗

Subtracts each component of the Vector4 by the components of the given Vector4.

Vector4 operator /(right: Vector4) 🔗

Divides each component of the Vector4 by the components of the given Vector4.

Vector4 operator /(right: float) 🔗

Divides each component of the Vector4 by the given float.

Vector4 operator /(right: int) 🔗

Divides each component of the Vector4 by the given int.

bool operator <(right: Vector4) 🔗

Compares two Vector4 vectors by first checking if the X value of the left vector is less than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, Z values of the two vectors, and then with the W values. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator <=(right: Vector4) 🔗

Compares two Vector4 vectors by first checking if the X value of the left vector is less than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, Z values of the two vectors, and then with the W values. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator ==(right: Vector4) 🔗

Returns true if the vectors are exactly equal.

Note: Due to floating-point precision errors, consider using is_equal_approx() instead, which is more reliable.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator >(right: Vector4) 🔗

Compares two Vector4 vectors by first checking if the X value of the left vector is greater than the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, Z values of the two vectors, and then with the W values. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

bool operator >=(right: Vector4) 🔗

Compares two Vector4 vectors by first checking if the X value of the left vector is greater than or equal to the X value of the right vector. If the X values are exactly equal, then it repeats this check with the Y values of the two vectors, Z values of the two vectors, and then with the W values. This operator is useful for sorting vectors.

Note: Vectors with @GDScript.NAN elements don't behave the same as other vectors. Therefore, the results from this operator may not be accurate if NaNs are included.

float operator [](index: int) 🔗

Access vector components using their index. v[0] is equivalent to v.x, v[1] is equivalent to v.y, v[2] is equivalent to v.z, and v[3] is equivalent to v.w.

Vector4 operator unary+() 🔗

Returns the same value as if the + was not there. Unary + does nothing, but sometimes it can make your code more readable.

Vector4 operator unary-() 🔗

Returns the negative value of the Vector4. This is the same as writing Vector4(-v.x, -v.y, -v.z, -v.w). This operation flips the direction of the vector while keeping the same magnitude. With floats, the number zero can be either positive or negative.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
print(Vector4(10, 20, 30, 40) * Vector4(3, 4, 5, 6)) # Prints (30.0, 80.0, 150.0, 240.0)
```

Example 2 (swift):
```swift
print(Vector4(10, 20, 30, 40) * 2) # Prints (20.0, 40.0, 60.0, 80.0)
```

Example 3 (swift):
```swift
print(Vector4(10, 20, 30, 40) + Vector4(3, 4, 5, 6)) # Prints (13.0, 24.0, 35.0, 46.0)
```

Example 4 (swift):
```swift
print(Vector4(10, 20, 30, 40) - Vector4(3, 4, 5, 6)) # Prints (7.0, 16.0, 25.0, 34.0)
```

---

## Vector math

**URL:** https://docs.godotengine.org/en/stable/tutorials/math/vector_math.html

**Contents:**
- Vector math
- Introduction
- Coordinate systems (2D)
- Vector operations
  - Member access
  - Adding vectors
  - Scalar multiplication
- Practical applications
  - Movement
  - Pointing toward a target

This tutorial is a short and practical introduction to linear algebra as it applies to game development. Linear algebra is the study of vectors and their uses. Vectors have many applications in both 2D and 3D development and Godot uses them extensively. Developing a good understanding of vector math is essential to becoming a strong game developer.

This tutorial is not a formal textbook on linear algebra. We will only be looking at how it is applied to game development. For a broader look at the mathematics, see https://www.khanacademy.org/math/linear-algebra

In 2D space, coordinates are defined using a horizontal axis (x) and a vertical axis (y). A particular position in 2D space is written as a pair of values such as (4, 3).

If you're new to computer graphics, it might seem odd that the positive y axis points downwards instead of upwards, as you probably learned in math class. However, this is common in most computer graphics applications.

Any position in the 2D plane can be identified by a pair of numbers in this way. However, we can also think of the position (4, 3) as an offset from the (0, 0) point, or origin. Draw an arrow pointing from the origin to the point:

This is a vector. A vector represents a lot of useful information. As well as telling us that the point is at (4, 3), we can also think of it as an angle θ (theta) and a length (or magnitude) m. In this case, the arrow is a position vector - it denotes a position in space, relative to the origin.

A very important point to consider about vectors is that they only represent relative direction and magnitude. There is no concept of a vector's position. The following two vectors are identical:

Both vectors represent a point 4 units to the right and 3 units below some starting point. It does not matter where on the plane you draw the vector, it always represents a relative direction and magnitude.

You can use either method (x and y coordinates or angle and magnitude) to refer to a vector, but for convenience, programmers typically use the coordinate notation. For example, in Godot, the origin is the top-left corner of the screen, so to place a 2D node named Node2D 400 pixels to the right and 300 pixels down, use the following code:

Godot supports both Vector2 and Vector3 for 2D and 3D usage, respectively. The same mathematical rules discussed in this article apply to both types, and wherever we link to Vector2 methods in the class reference, you can also check out their Vector3 counterparts.

The individual components of the vector can be accessed directly by name.

When adding or subtracting two vectors, the corresponding components are added:

We can also see this visually by adding the second vector at the end of the first:

Note that adding a + b gives the same result as b + a.

Vectors represent both direction and magnitude. A value representing only magnitude is called a scalar. Scalars use the float type in Godot.

A vector can be multiplied by a scalar:

Multiplying a vector by a positive scalar does not change its direction, only its magnitude. Multiplying with a negative scalar results in a vector in the opposite direction. This is how you scale a vector.

Let's look at two common uses for vector addition and subtraction.

A vector can represent any quantity with a magnitude and direction. Typical examples are: position, velocity, acceleration, and force. In this image, the spaceship at step 1 has a position vector of (1, 3) and a velocity vector of (2, 1). The velocity vector represents how far the ship moves each step. We can find the position for step 2 by adding the velocity to the current position.

Velocity measures the change in position per unit of time. The new position is found by adding the velocity multiplied by the elapsed time (here assumed to be one unit, e.g. 1 s) to the previous position.

In a typical 2D game scenario, you would have a velocity in pixels per second, and multiply it by the delta parameter (time elapsed since the previous frame) from the _process() or _physics_process() callbacks.

In this scenario, you have a tank that wishes to point its turret at a robot. Subtracting the tank's position from the robot's position gives the vector pointing from the tank to the robot.

To find a vector pointing from A to B, use B - A.

A vector with magnitude of 1 is called a unit vector. They are also sometimes referred to as direction vectors or normals. Unit vectors are helpful when you need to keep track of a direction.

Normalizing a vector means reducing its length to 1 while preserving its direction. This is done by dividing each of its components by its magnitude. Because this is such a common operation, Godot provides a dedicated normalized() method for this:

Because normalization involves dividing by the vector's length, you cannot normalize a vector of length 0. Attempting to do so would normally result in an error. In GDScript though, trying to call the normalized() method on a vector of length 0 leaves the value untouched and avoids the error for you.

A common use of unit vectors is to indicate normals. Normal vectors are unit vectors aligned perpendicularly to a surface, defining its direction. They are commonly used for lighting, collisions, and other operations involving surfaces.

For example, imagine we have a moving ball that we want to bounce off a wall or other object:

The surface normal has a value of (0, -1) because this is a horizontal surface. When the ball collides, we take its remaining motion (the amount left over when it hits the surface) and reflect it using the normal. In Godot, there is a bounce() method to handle this. Here is a code example of the above diagram using a CharacterBody2D:

The dot product is one of the most important concepts in vector math, but is often misunderstood. Dot product is an operation on two vectors that returns a scalar. Unlike a vector, which contains both magnitude and direction, a scalar value has only magnitude.

The formula for dot product takes two common forms:

The mathematical notation ||A|| represents the magnitude of vector A, and Ax means the x component of vector A.

However, in most cases it is easiest to use the built-in dot() method. Note that the order of the two vectors does not matter:

The dot product is most useful when used with unit vectors, making the first formula reduce to just cos(θ). This means we can use the dot product to tell us something about the angle between two vectors:

When using unit vectors, the result will always be between -1 (180°) and 1 (0°).

We can use this fact to detect whether an object is facing toward another object. In the diagram below, the player P is trying to avoid the zombies A and B. Assuming a zombie's field of view is 180°, can they see the player?

The green arrows fA and fB are unit vectors representing the zombie's facing direction and the blue semicircle represents its field of view. For zombie A, we find the direction vector AP pointing to the player using P - A and normalize it, however, Godot has a helper method to do this called direction_to(). If the angle between this vector and the facing vector is less than 90°, then the zombie can see the player.

In code it would look like this:

Like the dot product, the cross product is an operation on two vectors. However, the result of the cross product is a vector with a direction that is perpendicular to both. Its magnitude depends on their relative angle. If two vectors are parallel, the result of their cross product will be a null vector.

The cross product is calculated like this:

With Godot, you can use the built-in Vector3.cross() method:

The cross product is not mathematically defined in 2D. The Vector2.cross() method is a commonly used analog of the 3D cross product for 2D vectors.

In the cross product, order matters. a.cross(b) does not give the same result as b.cross(a). The resulting vectors point in opposite directions.

One common use of cross products is to find the surface normal of a plane or surface in 3D space. If we have the triangle ABC we can use vector subtraction to find two edges AB and AC. Using the cross product, AB × AC produces a vector perpendicular to both: the surface normal.

Here is a function to calculate a triangle's normal:

In the dot product section above, we saw how it could be used to find the angle between two vectors. However, in 3D, this is not enough information. We also need to know what axis to rotate around. We can find that by calculating the cross product of the current facing direction and the target direction. The resulting perpendicular vector is the axis of rotation.

For more information on using vector math in Godot, see the following articles:

Matrices and transforms

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (csharp):
```csharp
$Node2D.position = Vector2(400, 300)
```

Example 2 (csharp):
```csharp
var node2D = GetNode<Node2D>("Node2D");
node2D.Position = new Vector2(400, 300);
```

Example 3 (csharp):
```csharp
# Create a vector with coordinates (2, 5).
var a = Vector2(2, 5)
# Create a vector and assign x and y manually.
var b = Vector2()
b.x = 3
b.y = 1
```

Example 4 (csharp):
```csharp
// Create a vector with coordinates (2, 5).
var a = new Vector2(2, 5);
// Create a vector and assign x and y manually.
var b = new Vector2();
b.X = 3;
b.Y = 1;
```

---
