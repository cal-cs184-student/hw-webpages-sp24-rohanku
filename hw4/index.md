# Homework 4

## Overview

We implemented cloth simulation, treating the cloth as a collection of point masses and springs,
and Verlet integration to update the positions of the masses over time.
We added support for forces like gravity and intersection with collision objects.
Finally, we implemented various shaders to give our cloth color and texture.

## Part 1

Some screenshots of the wireframe:

![](images/p1_full_mesh.png]
![](images/p1_zoomed_mesh.png]

Without shearing constraints:
![](images/p1_wo_shearing.png]

Shearing constraints only:
![](images/p1_shearing_only.png]

All constraints:
![](images/p1_all.png]

## Part 2

In the subparts below, all parameters were set to their defaults
except for the parameter being investigated.

### Spring Constant

With a low `ks`, the cloth has more fine-grained wrinkles, and it sags more in its final state.
With a high `ks`, the cloth better retains its rectangular shape: it sags less, and has few wrinkles.
Here's a visual comparison:

`ks = 100 N/m`:

![](images/p2_ks_100.png]

`ks = 50000 N/m`:

![](images/p2_ks_50k.png]

### Density

With a low density, the cloth sags less in its final state and has fewer wrinkles.
It also looks "airy" as it falls slowly.
With a high density, the opposite is true: the cloth sags more and has more wrinkles,
and doesn't quite have the same illusion of falling slowly.

A visual comparison of the final states:

`density = 1 g/cm2`

![](images/p2_density_1.png]

`density = 100 g/cm2`

![](images/p2_density_100.png]

### Damping

With a high damping, the cloth moves/falls very slowly.
With a low damping, the cloth flutters wildly as it falls,
and it takes longer to converge to its resting state.
For 0 damping, the cloth may not ever converge.

Here is a comparison of the cloth as it is falling.

Damping = 1%

![](images/p2_high_damping.png]

Damping = 0%

![](images/p2_low_damping.png]

### Final State

Here is an image of the cloth from `pinned4` in its final state.
All parameters were set at their default values.

![](images/p2_default_pinned4.png]


## Part 3

`ks = 5000`
![](images/p3_5000.png]

`ks = 500`
![](images/p3_500.png]

`ks = 50000`
![](images/p3_50000.png]

For higher `ks` values, the cloth becomes more stiff, causing it to have less folds and conform less to the shape of the sphere.

## Part 4

Here are a few images of the falling cloth. All parameters are set to the default values.

![](images/p4_img0.png]

![](images/p4_img1.png]

![](images/p4_img2.png]

![](images/p4_img3.png]

Using a lower density seems to reduce the driving force pushing the cloth to be flat;
even after several seconds, the cloth is noticeably more wrinkled, and only a small
portion of it lies flat on the plane.

Here are images showing the behavior of the cloth with `density = 1 g/cm2`.

![](images/p4_dens1_img0.png]

![](images/p4_dens1_img1.png]

![](images/p4_dens1_img2.png]

A high `ks` makes the cloth "stiffer". It forms fewer wrinkles, and
it takes longer to flatten out wrinkles.

Here are images showing the behavior of the cloth with `ks = 50000 N/m`.

![](images/p4_ks_50k_img0.png]

![](images/p4_ks_50k_img1.png]

![](images/p4_ks_50k_img2.png]

## Part 5

### Shaders

Shaders are programs that compute a single color based on a given vertex and other relevant parameters. Having a specific API allows these shaders to run quickly and in parallel.
Vertex shaders operate on the geometric properties of vertices and provide necessary data to fragment shaders. Fragment shaders use the geometric properties from the vertex shader
to compute the color of a fragment of the scene.

### Blinn-Phong shading

The Blinn-Phong shading model incorporates ambient (a constant contribution from the environment), diffuse (uniformly in all direction), and specular (brighter at the reflection angle) components to compute the color of a fragment.

Ambient only:
![](images/p5_t2_ambient_only.png)

Diffuse only:
![](images/p5_t2_diffuse_only.png)

Specular only:
![](images/p5_t2_specular_only.png)

All:
![](images/p5_t2_all.png)

### Texture mapping

![](images/p5_t3.png)

### Displacement and bump mapping

Sphere with bump mapping:
![](images/p5_sphere_bump.png)

Cloth with bump mapping:
![](images/p5_cloth_bump.png)

Sphere with displacement mapping:
![](images/p5_sphere_displacement.png)

Sphere with bump mapping (coarseness `16`):
![](images/p5_sphere_bump_16.png)

Sphere with displacement mapping (coarseness `16`):
![](images/p5_sphere_displacement_16.png)

Sphere with bump mapping (coarseness `128`):
![](images/p5_sphere_bump_128.png)

Sphere with displacement mapping (coarseness `128`):
![](images/p5_sphere_displacement_128.png)

### Mirror shader

![](images/p5_t5.png)
