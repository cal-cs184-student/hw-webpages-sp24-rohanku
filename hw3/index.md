# Homework 3

## Overview

We implemented ray tracing algorithms and data structures for speeding up these algorithms. We also implemented lighting via
sampling. Many of the issues we ran into were related to normalizing quantities correctly and using vectors in the correct
coordinate frame. We were able to debug by reasoning through the possible causes of the errors seen in the render and finding
the relevant lines of code.

## Part 1

TODO

## Part 2

The BVH is constructed recursively. First, the bounding box of the current node is set to the union of the primitives' bounding boxes.
The `start` and `end` iterators are pointed to the start and end of the list of primitives.
If the number of nodes is smaller than `max_leaf_size`, then the node is returned immediately.

Otherwise, we find the average of the centroids of all of the primitive. We then split the primitives by centroid according to the axis
of the average centroid in which the current bounding box is the longest. If either the left or right sets are empty, we move one element
from the non-empty set to the empty one.

We then recursively construct the left and right nodes, point to them, and return the finalized node.
