# Homework 2

## Overview

## Part 1

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

Here are screenshots of de Casteljau's algorithm at various steps for the curve with control points shown above.

The control points:

![](images/q1level0.png)

1 evaluation step:

![](images/q1level1.png)

2 evaluation steps:

![](images/q1level2.png)

3 evaluation steps:

![](images/q1level3.png)

4 evaluation steps:

![](images/q1level4.png)

5 evaluation steps:

![](images/q1level5.png)

6 evaluation steps:

![](images/q1level6.png)

The final curve:

![](images/q1curve.png)

The final curve:

![](images/q1curve.png)

Here is another curve formed by moving the control points:

![](images/q1anotherCurve.png)

Here are the de Casteljau evaluation steps, with the t parameter modified:

![](images/q1anotherCurveWithSteps.png)

## Part 2

The de Casteljau algorithm can be extended from Bezier curves to Bezier surfaces.
To produce a Bezier surface, we start with an NxN grid of control points P(ij).
For a Bezier surface, there are two interpolation parameters: u and v.
Both independently range from 0 to 1.

The i'th row of control points is P(i*), where i identifies a row, and
we range over the second index. This row contains N control points.
We use de Casteljau's algorithm to interpolate across each row of control points,
using the u interpolation parameter. This produces a set of N new points, one per row.
We then perform another evaluation of de Casteljau's algorithm using this set
of N points, and the interpolation parameter v. This produces a point on the Bezier surface.

We can repeat this procedure for several u and v to build the full Bezier surface.

Here are screenshots of `bez/teapot.bez`:

![](q2wireframe.png)

![](q2nowireframe.png)
