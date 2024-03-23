# Homework 4

## Overview

We implemented cloth simulation using point masses and springs. We added support for forces like gravity and intersection with collision objects.

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

## Part 3

`ks = 5000`

`ks = 500`

`ks = 50000`

For higher `ks` values, the cloth becomes more stiff, causing it to have less folds and conform less to the shape of the sphere.
