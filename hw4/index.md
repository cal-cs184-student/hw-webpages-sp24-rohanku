# Homework 4

## Overview

We implemented cloth simulation using point masses and springs. We added support for forces like gravity and intersection with collision objects.

## Part 1

Some screenshots of the wireframe:

![](images/p1_full_mesh.png)
![](images/p1_zoomed_mesh.png)

Without shearing constraints:
![](images/p1_wo_shearing.png)

Shearing constraints only:
![](images/p1_shearing_only.png)

All constraints:
![](images/p1_all.png)

## Part 3

### Sphere

`ks = 5000`
![](images/p3_5000.png)

`ks = 500`
![](images/p3_500.png)

`ks = 50000`
![](images/p3_50000.png)

For higher `ks` values, the cloth becomes more stiff, causing it to have less folds and conform less to the shape of the sphere.

### Plane
![](images/p3_plane.png)

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
