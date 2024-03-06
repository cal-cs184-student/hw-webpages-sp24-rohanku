# Homework 3

## Overview

TODO

## Part 1

In this part, we randomly sampled rays within each pixel, converted them to world space,
and implemented ray-triangle and ray-sphere intersection.

### Ray Generation

Our goal is to render an image of size W x H.
We imagine that pixel `(x, y)` spans an axis-aligned unit square with corners `(x, y)`
and `(x+1, y+1)`.
To uniformly sample a random location within this pixel, we start by sampling from a unit square,
i.e. one with corners `(0, 0)` and `(1, 1)`. We then translate by `(x, y)` to obtain a location within
the desired pixel.

Next, we use the camera's position to translate the pixel location we sampled into
a ray in world coordinates.

To do this, we start by translating the pixel location into normalized image space: that is,
we treat the bottom left of the image frame as `(0, 0)`, and the top left as `(1, 1)`.
Doing this is simple: we just divide the pixel-space x coordinate by the image width (in pixels),
and the pixel-space y coordinate by the image height (in pixels).

We now convert the image space coordinates to a ray in camera space,
as shown in this figure from the HW spec:

![](./images/camerarays.png)

If the normalized image space coordinate is `(x, y)`, the corresponding point
in camera space is `C = ( lerp(x, -tan(0.5 * hFov), tan(0.5 * hFov)), lerp(y, -tan(0.5 * vFov), tan(0.5 * vFov)), -1 )`.
The origin of the ray in camera space is always `(0, 0, 0)`. The direction of the ray is the vector `C`,
though we scale it to have unit norm.

Now that we have a ray in camera space, we can convert the ray to world space.
The origin of the ray translates to the camera position `pos`, and the direction of the ray
becomes `c2w * C` (normalized appropriately), where `c2w` is the camera to world transformation matrix of the camera.

We now have a ray in world space coordinates.

### Ray Intersection

#### Triangles

We used the Moller Trumbore algorithm to perform ray-triangle intersection.
The Moller Trumbore algorithm solves the following system of equations:

$$ O + tD = (1 - b_1 - b_2) P_0 + b_1 P_1 + b_2 P_2 $$

where $O$ is the origin of the ray, $D$ is the direction of the ray, and $P_0$, $P_1$, and $P_2$ are vertices of the triangle.
This is a system of 3 equations in 3 unknowns ($t, b_1, b_2$).
We can solve it analytically:

$$ t = \frac{S_2 \cdot E_2}{S_1 \cdot E_1} $$
$$ b_1 = \frac{S_1 \cdot S}{S_1 \cdot E_1} $$
$$ b_2 = \frac{S_2 \cdot D}{S_1 \cdot E_1} $$

where $E_1 = P_1 - P_0$, $E_2 = P_2 - P_0$, $S = O - P_0$, $S_1 = D \times E_2$, and $S_2 = S \times E_1$.

If $S_1 \cdot E_1 = 0$, $b_1 < 0$, $b_2 < 0$, or $1 - b_1 - b_2 < 0$, there is no intersection:
the ray either is parallel to the plane of the triangle, or intersects the plane of the triangle
outside the bounds of the triangle.

Conveniently, this algorithm gives us the barycentric coordinates of the intersection point
with respect to the vertices of the triangle. We use these to interpolate the surface normal vector
at the intersection point, given the normal vectors at each of the vertices.

#### Spheres

To perform ray-sphere intersection, we solve the following system of equations:

$$ P = O + t D$$
$$ (P - C) \cdot (P - C) = R^2 $$

where $O$ and $D$ are the origin and direction of the ray, respectively;
$P$ is the intersection point; $C$ is the center of the sphere; and $R$ is the radius of the sphere.
This system of equations is a quadratic in $t$, and can be written as

$$ a t^2 + bt + c = 0 $$
where $a = d \cdot d$, $b = 2 (o - c) \cdot d$, and $c = (o - c) \cdot (o - c) - R^2$.

We solve the quadratic using the quadratic formula

$$ t = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}.$$

We discard any solutions not within the minimum and maximum allowed `t` of the ray.


