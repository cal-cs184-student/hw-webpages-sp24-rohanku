# Homework 2

## Overview

We implemented de Casteljau's algorithm to evaluate points along Bezier curves.

Given N control points and a parameter t between 0 and 1, de Casteljau's algorithm
linearly interpolates (with parameter t) between each pair of consecutive points,
producing a new set of N-1 points.
This process is repeated on the set of N-1 points from the previous step,
yielding a set of N-2 points. We repeatedly perform interpolation until
only one point remains. This point is on the Bezier curve.

In pseudocode, one step of de Casteljau's algorithm looks like this:

```
evaluateStep(N, t, points):
    output = []
    for i = 0 to N-1
        output.append(lerp(points[i], points[i+1], t))
    return output
```

We created a Bezier curve with 6 control points, as shown below:

```
6
0.100 0.300   0.200 0.300   0.300 0.450   0.400 0.800   0.700 0.250     0.900 0.300     0.300 0.700
```

Here are screenshots of de Casteljau's algorithm at various steps for the curve above.
