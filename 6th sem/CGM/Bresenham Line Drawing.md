# Bresenham's Line Drawing Algorithm

## Why Was It Needed?

In early computer graphics, hardware had limited processing power and lacked floating-point arithmetic units. The Digital Differential Analyzer (DDA) algorithm, while effective, relied on floating-point calculations, which were computationally expensive and slow on such systems. Bresenham's line drawing algorithm, developed by Jack E. Bresenham in 1962, addressed this by using only integer arithmetic, making it faster and more suitable for real-time graphics applications on early raster displays. It provided an efficient way to plot lines on a discrete pixel grid with minimal computational overhead.

## Theory

Bresenham's algorithm draws a line between two points $(x_0, y_0)$ and $(x_1, y_1)$ on a raster grid by selecting the closest pixels to the ideal line path. It assumes a discrete grid where pixels are located at integer coordinates. The algorithm minimizes the error between the ideal line and the plotted pixels using integer-based decision variables, eliminating the need for floating-point operations.

For a line with slope $m = \frac{dy}{dx}$, where $dx = x_1 - x_0$ and $dy = y_1 - y_0$, the algorithm decides whether to increment the $y$-coordinate or keep it constant as $x$ increments (for slopes $|m| \leq 1$). It uses a decision parameter to track the error and determine the next pixel to plot, ensuring the line stays as close as possible to the true path.

## Algorithm Steps (for Slope $|m| \leq 1$)

1. Input the two endpoints: $(x_0, y_0)$ and $(x_1, y_1)$.
2. Calculate differences:  
    $$dx = x_1 - x_0, \quad dy = y_1 - y_0$$
3. Initialize the decision parameter:  
    $$p_0 = 2dy - dx$$
4. Set the starting pixel at $(x_0, y_0)$.
5. For each $x$ from $x_0$ to $x_1$:
    - Plot the pixel at $(x, y)$.
    - If $p < 0$:
        - Keep $y$ unchanged.
        - Update $p = p + 2dy$.
    - Else:
        - Increment $y = y + 1$ (or $y = y - 1$ if $dy < 0$).
        - Update $p = p + 2dy - 2dx$.
    - Increment $x = x + 1$.
6. For slopes $|m| > 1$, swap the roles of $x$ and $y$ and iterate over $y$.

## Advantages

- **Efficiency**: Uses only integer arithmetic, making it fast on hardware with limited processing capabilities.
- **Simplicity**: Straightforward implementation with minimal memory usage.
- **Accuracy**: Selects the closest pixels to the ideal line, producing visually accurate lines on a discrete grid.
- **Hardware Compatibility**: Ideal for early graphics hardware lacking floating-point support.

## Disadvantages

- **Limited to Integer Coordinates**: Less flexible for non-integer endpoints or sub-pixel accuracy compared to DDA.
- **Slope Handling**: Requires separate handling for slopes $|m| > 1$, increasing code complexity.
- **Less Smooth for Steep Slopes**: May produce slightly jagged lines for steep slopes due to discrete pixel selection.
- **Not Generalizable**: Primarily designed for lines, less adaptable for other curves compared to DDA.

## Pseudocode

```c
void Bresenham(int x0, int y0, int x1, int y1) {
    int dx = abs(x1 - x0), dy = abs(y1 - y0);
    int sx = x0 < x1 ? 1 : -1, sy = y0 < y1 ? 1 : -1;
    int err = dx - dy, e2;
    
    while (true) {
        plot(x0, y0);
        if (x0 == x1 && y0 == y1) break;
        e2 = 2 * err;
        if (e2 > -dy) {
            err -= dy;
            x0 += sx;
        }
        if (e2 < dx) {
            err += dx;
            y0 += sy;
        } 
    }
}
```

