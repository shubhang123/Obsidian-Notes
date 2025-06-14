# Digital Differential Analyzer (DDA) Algorithm

## Theory

The Digital Differential Analyzer (DDA) algorithm is used in computer graphics to draw lines between two points on a raster grid. It calculates intermediate pixel coordinates along a straight line between the start point $(x_0, y_0)$ and end point $(x_1, y_1)$ by using the difference in their $x$ and $y$ coordinates (hence "differential"). The algorithm selects the closest pixel to the ideal line path at each step, ensuring a visually smooth line on a discrete grid.

The DDA algorithm is based on the linear interpolation of coordinates. For a line, the slope $m$ is calculated as:

# $$m = \frac{y_1 - y_0}{x_1 - x_0}$$

Depending on whether the slope is less than or greater than 1, the algorithm iterates over the $x$- or $y$-axis, respectively, to minimize the number of steps and ensure accuracy.

## Steps of the DDA Algorithm

1. Input the two endpoints: $(x_0, y_0)$ and $(x_1, y_1)$.
    
2. Calculate the differences:
    
    $$dx = x_1 - x_0, \quad dy = y_1 - y_0$$
    
3. Determine the number of steps based on the larger difference:
    
    $$\text{steps} = \max(|dx|, |dy|)$$
    
4. Calculate the increments for $x$ and $y$ per step:
    
    $$x_{\text{inc}} = \frac{dx}{\text{steps}}, \quad y_{\text{inc}} = \frac{dy}{\text{steps}}$$
    
5. Initialize the starting point: $x = x_0$, $y = y_0$.
    
6. For each step from 1 to $\text{steps}$:
    
    - Plot the pixel at $(\text{round}(x), \text{round}(y))$.
    - Update coordinates: $x = x + x_{\text{inc}}$, $y = y + y_{\text{inc}}$.

## Advantages

- **Efficiency**: Faster than direct line equations as it uses incremental calculations.
- **Precision**: Produces smoother lines by selecting the closest pixels to the true line.
- **Versatility**: Works for lines with any slope, unlike Bresenham’s algorithm, which is optimized for integer-based slopes.

## Disadvantages

- **Floating-Point Operations**: Requires floating-point arithmetic, which can be slower on hardware without floating-point support.
- **Rounding Errors**: Repeated rounding can lead to slight inaccuracies in pixel placement.
- **Complexity**: Slightly more complex than Bresenham’s algorithm due to floating-point calculations.

## Pseudocode

```c
void DDA(float x0, float y0, float x1, float y1) {
    float dx = x1 - x0, dy = y1 - y0;
    float steps = max(abs(dx), abs(dy));
    float x_inc = dx / steps, y_inc = dy / steps;
    float x = x0, y = y0;
    
    for (int i = 0; i <= steps; i++) {
        plot(round(x), round(y));
        x += x_inc;
        y += y_inc;
    }
}
```