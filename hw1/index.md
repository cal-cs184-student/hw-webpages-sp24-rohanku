# Homework 1

# Overview

We implemented rasterizing of triangles with various sampling methods. It was interesting seeing how the
various techniques for improving render quality we learned in lectures worked out in practice.

## Task 1

To rasterize a triangle, we:
* Compute the triangle's bounding box
* For each pixel within the bounding box, check if the pixel is within the triangle (this involves 3 line tests).
* If the pixel is within the triangle, set the pixel's color to that of the triangle.

To calculate which side of a line a point `(x, y)` falls on, we compute

> `- (x - x0) * (y1 - y0) + (y - y0) * (x1 - x0)`

where `(x0, y0)` and `(x1, y1)` are two points on the line.

If all the line tests or are


This algorithm checks each sample within nonnegativeding boxnonpositivetriangle.

## Task 2

We essentially just updated the `sample_buffer` to contain the unrolled supersampled pixels.
We then stored the rasterized color of each supersampled pixel in `sample_buffer`, and later downsampled
via averaging in `resolve_to_framebuffer`. We had to modify several areas to match our unrolling scheme, which was
as follows:

> For a pixel at `(x, y, a, b)` where `x` is the x-coordinate, `y` is the y-coordinate, `a` is the supersampled x-coordinate
> within the pixel, and `b` is the supersampled y-coordinate within the pixel, the color is stored in 
> `sample_buffer[y * width * sample_rate + x * sample_rate + a * sqrt_sample_rate + b]`.

We also needed to update functions that changed the width, height, or sample rate to accordingly resize the sample buffer.

Supersampling is useful since it allows us to incorporate more information about the triangle into the limited number of pixels
in the framebuffer by sampling at more points.

Screenshots of `basic/test4.svg` are included below. These results are observed since pixels are no longer either fully inside or outside
the triangle, but rather can visually show pixels that are only partially inside of the triangle.