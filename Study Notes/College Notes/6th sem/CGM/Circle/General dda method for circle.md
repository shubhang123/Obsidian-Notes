Here’s the DDA‐style circle drawing algorithm laid out as a clear sequence of steps:

1. **Inputs**
    
    - Center: (xc,yc)(x_c, y_c)
        
    - Radius: rr
        
2. **Initialize Starting Point**
    
    - Set
        
        x  =  r,y  =  0. x \;=\; r,\quad y \;=\; 0.
3. **Loop Condition**
    
    - Continue while x  ≥  yx \;\ge\; y (i.e. through the first 45° octant).
        
4. **Plot Symmetric Points**
    
    - For each (x,y)(x,y), plot all eight reflections around (xc,yc)(x_c,y_c):
        
        (xc±x,  yc±y)and(xc±y,  yc±x). (x_c \pm x,\;y_c \pm y) \quad\text{and}\quad (x_c \pm y,\;y_c \pm x).
5. **Compute Differential Increments**
    
    - Using  
        Δx=yr,Δy=− xr\displaystyle \Delta x = \frac{y}{r},\quad \Delta y = -\,\frac{x}{r}
        
6. ## **Update Coordinates**
    
    x  ←  x+Δx,y  ←  y+Δy. x \;\leftarrow\; x + \Delta x, \quad y \;\leftarrow\; y + \Delta y.
7. **Repeat**
    
    - Go back to Step 3 until the loop terminates.
        
8. **Done**
    
    - All octants have been filled by symmetry; the circle is complete.
        

---

### Pseudocode (for reference)

```c
void drawCircleDDA(int xc, int yc, int r) {
    float x = r, y = 0;
    while (x >= y) {
        // 1. Plot the 8 symmetric points
        plot8(xc, yc, round(x), round(y));

        // 2. Compute and apply DDA increments
        float dx =  y / r;
        float dy = -x / r;
        x += dx;
        y += dy;
    }
}
```

This stepwise form ensures you compute only one octant and mirror via symmetry, using simple adds and divides each iteration.