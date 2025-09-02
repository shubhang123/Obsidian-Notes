  The Cohen-Sutherland line clipping algorithm clips a line segment to a rectangular window by determining which parts lie inside or outside the window. Here are the steps, followed by the mathematical formulation:

### Steps
1. **Assign Region Codes**:
   - Divide the 2D space into 9 regions based on the clipping window with boundaries $x_{min}$, $x_{max}$, $y_{min}$, $y_{max}$.
   - Each region is assigned a 4-bit code (TBRL: Top, Bottom, Right, Left) for a point $(x, y)$:
     - Bit 1 (T): $y > y_{max}$ (1 if true, 0 if false)
     - Bit 2 (B): $y < y_{min}$ (1 if true, 0 if false)
     - Bit 3 (R): $x > x_{max}$ (1 if true, 0 if false)
     - Bit 4 (L): $x < x_{min}$ (1 if true, 0 if false)
   - Compute codes for both endpoints of the line segment, $P_1(x_1, y_1)$ and $P_2(x_2, y_2)$.

1. **Check Trivial Cases**: 
   - **Accept**: If both endpoints have codes 0000 (logical AND = 0), the line is fully inside.
   - **Reject**: If the logical AND of the codes is non-zero, the line is fully outside (both points share a common out-of-bounds region).

3. **Clip Non-Trivial Cases**:
   - If neither accepted nor rejected, clip the line against one window boundary at a time (e.g., left, right, top, bottom).
   - For an endpoint outside (non-zero code), compute the intersection of the line with the boundary it violates.
   - Update the endpoint to the intersection point and recalculate its region code.
   - Repeat until the line is either accepted (both codes 0000) or rejected (AND non-zero).

4. **Repeat Until Resolved**:
   - Continue clipping against boundaries until the line is fully accepted or rejected.

### Mathematical Formulation
Given a line segment from $P_1(x_1, y_1)$ to $P_2(x_2, y_2)$ and a clipping window defined by $x_{min}$, $x_{max}$, $y_{min}$, $y_{max}$:

#### Region Code Assignment
For a point $(x, y)$, the 4-bit code is:
- $c_1 = (y > y_{max}) \ll 3 + (y < y_{min}) \ll 2 + (x > x_{max}) \ll 1 + (x < x_{min})$
- Similarly for $P_1$ and $P_2$, compute codes $c_1$ and $c_2$.

#### Trivial Accept/Reject
- Accept if $c_1 = 0$ and $c_2 = 0$.
- Reject if $c_1 \& c_2 \neq 0$.

#### Intersection with Boundaries
For a line parameterized as $(x, y) = (x_1 + t(x_2 - x_1), y_1 + t(y_2 - y_1))$, where $0 \leq t \leq 1$:
- **Left ($x = x_{min}$)**:
  \[
  $$t = \frac{x_{min} - x_1}{x_2 - x_1}, \quad y = y_1 + t(y_2 - y_1)$$
  \]
- **Right ($x = x_{max}$)**:
  \[
  $$t = \frac{x_{max} - x_1}{x_2 - x_1}, \quad y = y_1 + t(y_2 - y_1)$$
  \]
- **Bottom ($y = y_{min}$)**:
  \[
  $$t = \frac{y_{min} - y_1}{y_2 - y_1}, \quad x = x_1 + t(x_2 - x_1)$$
  \]
- **Top ($y = y_{max}$)**:
  \[
  $$t = \frac{y_{max} - y_1}{y_2 - y_1}, \quad x = x_1 + t(x_2 - x_1)$$
  \]
- If $t$ is outside $[0, 1]$, the intersection is not on the segment.

#### Update Endpoint
Replace the outside endpoint with the intersection point and recompute its region code. Repeat until trivial accept or reject.

This algorithm efficiently clips lines by leveraging binary region codes and iterative boundary intersections.