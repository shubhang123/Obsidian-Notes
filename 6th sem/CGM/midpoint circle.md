 # Midpoint Circle Drawing Algorithm in Computer Graphics

## Introduction

The Midpoint Circle Drawing Algorithm is an efficient method for drawing circles on a raster display in computer graphics. It improves upon the general circle drawing method by using integer arithmetic and a decision parameter, avoiding expensive floating-point operations like square roots. Developed as an extension of the midpoint line algorithm, it leverages the circle's 8-way symmetry to minimize computations, making it suitable for real-time graphics applications.

## Theory

The algorithm is based on the equation of a circle centered at the origin $(0, 0)$ with radius $r$:

$$x^2 + y^2 = r^2$$

For a circle centered at $(h, k)$, the equation is:

$$(x - h)^2 + (y - k)^2 = r^2$$

The Midpoint Circle Algorithm works by:

1. Computing points in the **first octant** (where $0 \leq x \leq y$ and $x, y \geq 0$) of the circle.
2. Using 8-way symmetry to plot corresponding points in the other seven octants.
3. Employing a decision parameter to choose between two possible pixels at each step, based on the midpoint between them.

### Decision Parameter

The algorithm starts at the point $(0, r)$ (top of the circle) and moves through the first octant, deciding whether to move horizontally (increment $x$) and/or vertically (decrement $y$). At each step, it evaluates the midpoint between two possible pixels to determine which is closer to the true circle.

Define the circle function:

$$f(x, y) = x^2 + y^2 - r^2$$

- If $f(x, y) = 0$, the point $(x, y)$ lies on the circle.
- If $f(x, y) < 0$, the point is inside the circle.
- If $f(x, y) > 0$, the point is outside the circle.

At each step, given a pixel $(x_k, y_k)$, the algorithm considers two possible next pixels in the first octant:

- **East (E)**: $(x_k + 1, y_k)$
- **South-East (SE)**: $(x_k + 1, y_k - 1)$

It evaluates the midpoint between these two pixels at $(x_k + 1, y_k - 0.5)$ and computes the decision parameter $d$:

$$d = f(x_k + 1, y_k - 0.5) = (x_k + 1)^2 + (y_k - 0.5)^2 - r^2$$

- If $d < 0$, the midpoint is inside the circle, so choose the East pixel $(x_k + 1, y_k)$.
- If $d \geq 0$, the midpoint is on or outside the circle, so choose the South-East pixel $(x_k + 1, y_k - 1)$.

### Initial Decision Parameter

Start at $(x_0, y_0) = (0, r)$:

- Initial midpoint: $(1, r - 0.5)$
- Initial decision parameter:

$$d_0 = f(1, r - 0.5) = 1^2 + (r - 0.5)^2 - r^2 = 1 + (r^2 - r + 0.25) - r^2 = 1.25 - r$$

For integer arithmetic, multiply through by 4 to eliminate fractions, but typically, we approximate $d_0 \approx 1 - r$ for simplicity in integer-based implementations.

### Updates to Decision Parameter

At each step, update $d$ based on the chosen pixel:

- If East is chosen ($d < 0$):

$$d_{\text{new}} = d + 2x_k + 3$$

- If South-East is chosen ($d \geq 0$):

$$d_{\text{new}} = d + 2x_k - 2y_k + 5$$

These updates are derived by computing the difference in $f(x, y)$ at the next midpoint.

## Algorithm Steps

1. **Input**: Radius $r$ and center $(h, k)$ of the circle.
2. **Initialize**:
    - Start at $(x, y) = (0, r)$.
    - Initial decision parameter: $d = 1 - r$ (approximation for integer arithmetic).
3. **Plot Initial Points**:
    - Plot $(h \pm 0, k \pm r)$ and $(h \pm r, k \pm 0)$ (four cardinal points).
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
void drawCircleMidpoint(int h, int k, int r) {
    int x = 0, y = r;
    int d = 1 - r; // Initial decision parameter

    // Plot initial points at cardinal directions
    plot(h + x, k + y); // (0, r)
    plot(h - x, k + y); // (0, r)
    plot(h + x, k - y); // (0, -r)
    plot(h - x, k - y); // (0, -r)
    plot(h + y, k + x); // (r, 0)
    plot(h - y, k + x); // (-r, 0)
    plot(h + y, k - x); // (r, 0)
    plot(h - y, k - x); // (-r, 0)

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

- **Efficiency**: Uses only integer arithmetic, avoiding floating-point operations like square roots.
- **Accuracy**: Produces a smooth circle by selecting the pixel closest to the true circle at each step.
- **Symmetry**: Leverages 8-way symmetry to minimize computations.
- **Hardware Suitability**: Ideal for early graphics hardware with limited floating-point capabilities.

## Disadvantages

- **Complexity**: Slightly more complex to understand and implement than the general method due to the decision parameter.
- **Limited to Circles**: Specifically designed for circles, not easily adaptable to other curves without modification.
- **Initial Approximation**: The initial decision parameter $d = 1 - r$ is an approximation, which may introduce minor errors for very small radii (though negligible in practice).

## Applications

- **Graphics Libraries**: Widely used in graphics APIs and libraries (e.g., OpenGL, SDL) for rendering circles.
- **Real-Time Rendering**: Suitable for real-time applications like games and simulations due to its efficiency.
- **Digital Art Tools**: Used in drawing software for creating circular shapes and curves.

## Notes

- The Midpoint Circle Algorithm is a significant improvement over the general method, as it eliminates the need for square root calculations and floating-point arithmetic.
- It can be extended to draw arcs by limiting the iteration to a specific angular range.
- For filled circles, the algorithm can be modified to plot all pixels between symmetric points (e.g., from $(h-x, k+y)$ to $(h+x, k+y)$) at each step.