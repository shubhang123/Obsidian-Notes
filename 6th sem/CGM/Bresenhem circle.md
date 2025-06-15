# Bresenham Circle Drawing Algorithm in Computer Graphics

## Introduction

The Bresenham Circle Drawing Algorithm (often synonymous with the Midpoint Circle Algorithm in many contexts) is an efficient method for drawing circles on a raster display. It uses integer arithmetic to avoid floating-point operations, making it ideal for early graphics hardware. The algorithm leverages the circle's 8-way symmetry to minimize computations, plotting pixels in all octants by computing points in just one octant.

## Theory

The algorithm is based on the equation of a circle centered at the origin $(0, 0)$ with radius $r$:

$$x^2 + y^2 = r^2$$

For a circle centered at $(h, k)$, the equation becomes:

$$(x - h)^2 + (y - k)^2 = r^2$$

The Bresenham Circle Algorithm works by:

1. Computing points in the **first octant** (where $0 \leq x \leq y$ and $x, y \geq 0$).
2. Using 8-way symmetry to plot points in the other seven octants.
3. Using a decision parameter to choose between two possible pixels at each step, based on which pixel is closer to the true circle.

### Decision Parameter

Define the circle function:

$$f(x, y) = x^2 + y^2 - r^2$$

- $f(x, y) = 0$: Point is on the circle.
- $f(x, y) < 0$: Point is inside the circle.
- $f(x, y) > 0$: Point is outside the circle.

Start at $(x, y) = (0, r)$ and move through the first octant. At each step, given a pixel $(x_k, y_k)$, the algorithm considers two possible next pixels:

- **East (E)**: $(x_k + 1, y_k)$
- **South-East (SE)**: $(x_k + 1, y_k - 1)$

It evaluates the midpoint between these pixels at $(x_k + 1, y_k - 0.5)$ and computes the decision parameter $d$:

$$d = f(x_k + 1, y_k - 0.5) = (x_k + 1)^2 + (y_k - 0.5)^2 - r^2$$

- If $d < 0$, the midpoint is inside the circle, so choose East $(x_k + 1, y_k)$.
- If $d \geq 0$, the midpoint is on or outside the circle, so choose South-East $(x_k + 1, y_k - 1)$.

### Initial Decision Parameter

At the starting point $(0, r)$:

$$d_0 = f(1, r - 0.5) = 1^2 + (r - 0.5)^2 - r^2$$

$$d_0 = 1 + (r^2 - r + 0.25) - r^2 = 1.25 - r$$

For integer arithmetic, this is approximated as $d_0 = 1 - r$ (adjustments are made in implementations to handle fractions).

### Updates to Decision Parameter

- If East is chosen ($d < 0$):

$$d_{\text{new}} = d + 2x_k + 3$$

- If South-East is chosen ($d \geq 0$):

$$d_{\text{new}} = d + 2x_k - 2y_k + 5$$

These updates ensure the algorithm uses only integer arithmetic.

## Algorithm Steps

1. **Input**: Radius $r$ and center $(h, k)$.
2. **Initialize**:
    - $x = 0$, $y = r$
    - Decision parameter: $d = 1 - r$
3. **Plot Initial Points**:
    - Plot cardinal points: $(h \pm 0, k \pm r)$, $(h \pm r, k \pm 0)$.
4. **Iterate Through First Octant**:
    - While $x \leq y$:
        - Plot points in all 8 octants:
            - $(h + x, k + y)$, $(h - x, k + y)$, $(h + x, k - y)$, $(h - x, k - y)$
            - $(h + y, k + x)$, $(h - y, k + x)$, $(h + y, k - x)$, $(h - y, k - x)$
        - If $d < 0$:
            - $d = d + 2x + 3$
            - $x = x + 1$
        - Else:
            - $d = d + 2x - 2y + 5$
            - $x = x + 1$, $y = y - 1$

## Pseudocode

```c
void drawCircleBresenham(int h, int k, int r) {
    int x = 0, y = r;
    int d = 1 - r; // Initial decision parameter

    // Plot initial cardinal points
    plot(h + x, k + y);
    plot(h - x, k + y);
    plot(h + x, k - y);
    plot(h - x, k - y);
    plot(h + y, k + x);
    plot(h - y, k + x);
    plot(h + y, k - x);
    plot(h - y, k - x);

    while (x <= y) {
        // Plot points in all 8 octants
        plot(h + x, k + y);
        plot(h - x, k + y);
        plot(h + x, k - y);
        plot(h - x, k - y);
        plot(h + y, k + x);
        plot(h - y, k + x);
        plot(h + y, k - x);
        plot(h - y, k - x);

        if (d < 0) {
            d = d + 2 * x + 3;
            x++;
        } else {
            d = d + 2 * (x - y) + 5;
            x++;
            y--;
        }
    }
}
```

## Advantages

- **Efficiency**: Uses only integer arithmetic, eliminating floating-point operations.
- **Accuracy**: Selects the pixel closest to the true circle at each step.
- **Symmetry**: Reduces computations by leveraging 8-way symmetry.
- **Hardware Compatibility**: Ideal for early graphics hardware with limited floating-point support.

## Disadvantages

- **Complexity**: More complex to understand than the general circle drawing method.
- **Limited to Circles**: Not easily adaptable to other shapes without modification.
- **Approximation in Initialization**: The initial $d = 1 - r$ is an approximation, which may introduce minor errors for very small radii.

## Applications

- **Graphics Rendering**: Used in graphics libraries (e.g., OpenGL, SDL) for drawing circles.
- **Real-Time Systems**: Suitable for games and simulations due to its efficiency.
- **Digital Design**: Employed in design tools for creating circular shapes.

## Notes

- The Bresenham Circle Algorithm is often identical to the Midpoint Circle Algorithm in practice, with minor variations in how the decision parameter is initialized or updated.
- It can be extended to draw arcs by limiting the iteration to a specific angular range.
- For filled circles, modify the algorithm to plot all pixels between symmetric points at each step.