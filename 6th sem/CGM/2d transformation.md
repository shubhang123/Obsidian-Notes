Below is a detailed explanation of transformations in 2D, covering all types, their mathematical representations, and applications. I’ve used `$` to enclose LaTeX math expressions for inline formatting, as requested.

---

# Transformations in 2D: A Detailed Explanation

Transformations in 2D are operations that change the position, orientation, size, or shape of objects in a two-dimensional plane. They are widely used in fields like computer graphics, animation, CAD (Computer-Aided Design), and robotics to manipulate objects efficiently. In this explanation, we’ll explore each type of transformation, provide their mathematical formulations using matrices, and discuss their practical applications.

---

## What Are Transformations?
A transformation is a mapping from one coordinate system to another. In 2D, we typically work with points represented as \((x, y)\), and a transformation produces a new point \((x', y')\). These operations can be expressed mathematically, often using matrices, making them computationally efficient for applications like rendering graphics or simulating motion.

Let’s dive into the main types of 2D transformations.

---

## 1. Translation
Translation moves an object by shifting it along the x and y axes by specified distances.

- **Definition**: If the translation distances are \(t_x\) (along x) and \(t_y\) (along y), the new coordinates of a point \((x, y)\) become:
  \[
  x' = x + t_x, \quad y' = y + t_y
  \]
  In vector form:
  \[
  \begin{bmatrix}
  x' \\
  y'
  \end{bmatrix}
  =
  \begin{bmatrix}
  x \\
  y
  \end{bmatrix}
  +
  \begin{bmatrix}
  t_x \\
  t_y
  \end{bmatrix}
  \]
- **Properties**:
  - Preserves the shape, size, and orientation of the object (a **rigid transformation**).
  - Cannot be represented as a 2x2 matrix multiplication alone, which leads us to use homogeneous coordinates (explained later).
- **Example**: Moving a point from \((2, 3)\) by \(t_x = 1\), \(t_y = 4\) results in \((3, 7)\).

---

## 2. Rotation
Rotation turns an object around a fixed point, usually the origin, by an angle \(\theta\).

- **Definition**: The transformation matrix for a rotation by angle \(\theta\) (counterclockwise when \(\theta\) is positive) is:
  \[
  \begin{bmatrix}
  \cos\theta & -\sin\theta \\
  \sin\theta & \cos\theta
  \end{bmatrix}
  \]
  The new coordinates are:
  \[
  \begin{bmatrix}
  x' \\
  y'
  \end{bmatrix}
  =
  \begin{bmatrix}
  \cos\theta & -\sin\theta \\
  \sin\theta & \cos\theta
  \end{bmatrix}
  \begin{bmatrix}
  x \\
  y
  \end{bmatrix}
  \]
  Or explicitly:
  \[
  x' = x \cos\theta - y \sin\theta, \quad y' = x \sin\theta + y \cos\theta
  \]
- **Properties**:
  - Preserves distances and angles (another **rigid transformation**).
  - Rotations around points other than the origin require combining translation and rotation.
- **Example**: Rotating \((1, 0)\) by \(\theta = 90^\circ\) (\(\cos 90^\circ = 0\), \(\sin 90^\circ = 1\)) gives \((0, 1)\).

---

## 3. Scaling
Scaling changes the size of an object, either uniformly or non-uniformly, along the x and y axes.

- **Definition**: With scaling factors \(s_x\) (x-direction) and \(s_y\) (y-direction), the matrix is:
  \[
  \begin{bmatrix}
  s_x & 0 \\
  0 & s_y
  \end{bmatrix}
  \]
  So:
  \[
  \begin{bmatrix}
  x' \\
  y'
  \end{bmatrix}
  =
  \begin{bmatrix}
  s_x & 0 \\
  0 & s_y
  \end{bmatrix}
  \begin{bmatrix}
  x \\
  y
  \end{bmatrix}
  \]
  Or:
  \[
  x' = s_x x, \quad y' = s_y y
  \]
- **Properties**:
  - **Uniform scaling** (\(s_x = s_y\)): Preserves angles but changes size.
  - **Non-uniform scaling** (\(s_x \neq s_y\)): Distorts shapes.
  - \(s > 1\) enlarges, \(0 < s < 1\) shrinks, and \(s < 0\) reflects and scales.
- **Example**: Scaling \((2, 3)\) with \(s_x = 2\), \(s_y = 0.5\) results in \((4, 1.5)\).

---

## 4. Reflection
Reflection flips an object over a line, such as the x-axis, y-axis, or \(y = x\).

- **Common Matrices**:
  - **Across the x-axis**:
    \[
    \begin{bmatrix}
    1 & 0 \\
    0 & -1
    \end{bmatrix}
    \]
    \(x' = x\), \(y' = -y\)
  - **Across the y-axis**:
    \[
    \begin{bmatrix}
    -1 & 0 \\
    0 & 1
    \end{bmatrix}
    \]
    \(x' = -x\), \(y' = y\)
  - **Across \(y = x\)**:
    \[
    \begin{bmatrix}
    0 & 1 \\
    1 & 0
    \end{bmatrix}
    \]
    \(x' = y\), \(y' = x\)
- **Properties**:
  - Preserves distances but reverses orientation (e.g., flips handedness).
- **Example**: Reflecting \((1, 2)\) over the y-axis gives \((-1, 2)\).

---

## 5. Shearing
Shearing tilts an object, shifting points along one axis proportional to their coordinate on the other axis.

- **Definition**:
  - **X-direction shear** (factor \(k\)):
    \[
    \begin{bmatrix}
    1 & k \\
    0 & 1
    \end{bmatrix}
    \]
    \(x' = x + k y\), \(y' = y\)
  - **Y-direction shear** (factor \(k\)):
    \[
    \begin{bmatrix}
    1 & 0 \\
    k & 1
    \end{bmatrix}
    \]
    \(x' = x\), \(y' = y + k x\)
- **Properties**:
  - Transforms rectangles into parallelograms, preserving area but not angles.
- **Example**: X-shearing \((1, 1)\) with \(k = 2\) gives \((3, 1)\).

---

## 6. Affine Transformations
Affine transformations combine linear transformations (rotation, scaling, shearing) with translation.

- **General Form**: 
  \[
  \begin{bmatrix}
  x' \\
  y'
  \end{bmatrix}
  =
  \begin{bmatrix}
  a & b \\
  c & d
  \end{bmatrix}
  \begin{bmatrix}
  x \\
  y
  \end{bmatrix}
  +
  \begin{bmatrix}
  t_x \\
  t_y
  \end{bmatrix}
  \]
- **Properties**:
  - Preserves straight lines and ratios of distances.
  - Represented efficiently using homogeneous coordinates.

---

## Homogeneous Coordinates
To unify all transformations, including translation, as matrix multiplications, we use **homogeneous coordinates**. A 2D point \((x, y)\) becomes \((x, y, 1)\), and transformations are 3x3 matrices:

- **Translation**:
  \[
  \begin{bmatrix}
  1 & 0 & t_x \\
  0 & 1 & t_y \\
  0 & 0 & 1
  \end{bmatrix}
  \]
- **Rotation**:
  \[
  \begin{bmatrix}
  \cos\theta & -\sin\theta & 0 \\
  \sin\theta & \cos\theta & 0 \\
  0 & 0 & 1
  \end{bmatrix}
  \]
- **Scaling**:
  \[
  \begin{bmatrix}
  s_x & 0 & 0 \\
  0 & s_y & 0 \\
  0 & 0 & 1
  \end{bmatrix}
  \]
- **Benefit**: Multiple transformations can be combined by matrix multiplication, e.g., \(T \cdot R\) for rotation followed by translation.

---

## Order of Transformations
The sequence of transformations matters because matrix multiplication is **not commutative**. For example:
- **Rotation then Translation**: Rotates around the origin, then moves.
- **Translation then Rotation**: Moves, then rotates around the new position.

In practice, transformations are often applied in a standard order like scaling, rotation, then translation (SRT).

---

## Applications
2D transformations are critical in:
- **Computer Graphics**: Positioning and animating objects.
- **Animation**: Creating smooth motion and deformations.
- **CAD**: Designing precise geometric shapes.
- **Image Processing**: Resizing, rotating, or warping images.

---

This covers the core types of 2D transformations, their math (using $ for LaTeX), and their uses. Let me know if you’d like examples or further details!