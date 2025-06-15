# World Coordinate System and Screen Coordinate System in Computer Graphics

In computer graphics, the **world coordinate system** and the **screen coordinate system** are two essential frameworks used to define and display a scene. Below, I'll explain what each system is, their differences, and how they relate through a series of transformations.

---

## World Coordinate System

The **world coordinate system** (or **world space**) is the global reference frame for a 3D scene. It's where all objects, such as models, lights, and cameras, are positioned and oriented relative to one another.

- **Definition**: A 3D Cartesian coordinate system (with $x$, $y$, and $z$ axes) that serves as the "universe" of the graphics application.
- **Purpose**:
    - Defines the absolute positions, rotations, and scales of objects.
    - Acts as a common space for all elements in the scene, independent of the viewer or display.
- **Example**: In a video game, a car might be placed at coordinates $(10, 0, 5)$ in world space, indicating its position relative to the scene's origin.

---

## Screen Coordinate System

The **screen coordinate system** (or **screen space**) is the 2D coordinate system of the display, such as a monitor or window. It represents the final positions of pixels where the scene is rendered.

- **Definition**: A 2D system where coordinates correspond to pixel locations, typically with the origin at the top-left corner.
- **Purpose**:
    - Specifies where objects appear on the screen after all transformations.
    - Used for rasterization, the process of converting shapes into pixels.
- **Example**: On a 1920x1080 screen, coordinates range from $(0, 0)$ (top-left) to $(1919, 1079)$ (bottom-right).

---

## How They Relate: Transformations from World to Screen

To render a 3D scene from the world coordinate system onto the 2D screen coordinate system, a sequence of transformations is applied. This process, part of the **graphics pipeline**, converts a point in world space, like $\mathbf{P}_w = (x_w, y_w, z_w)$, into screen space, like $\mathbf{P}_s = (x_s, y_s)$. Here's how it works:

### 1. View Transformation

- **What it does**: Moves the scene from world space to **camera space** (or eye space), aligning it with the camera's position and orientation.
- **How**: Applies a view matrix $\mathbf{V}$ that repositions the world so the camera is at the origin, looking along a specific axis.
- **Result**: $\mathbf{P}_c = \mathbf{V} \cdot \mathbf{P}_w$, where $\mathbf{P}_c$ is the point in camera space.

### 2. Projection Transformation

- **What it does**: Projects the 3D scene from camera space to **clip space**, preparing it for 2D rendering.
- **How**: Uses a projection matrix $\mathbf{P}$:
    - **Perspective projection**: Simulates depth, making distant objects smaller.
    - **Orthographic projection**: Preserves sizes, ignoring depth.
- **Result**: $\mathbf{P}_p = \mathbf{P} \cdot \mathbf{P}_c$, a homogeneous coordinate in clip space.

### 3. Perspective Division

- **What it does**: Converts clip space to **normalized device coordinates (NDC)**, normalizing coordinates to a standard range.
- **How**: Divides the clip space coordinates by their homogeneous $w$-component.
- **Result**: $\mathbf{P}_{ndc} = \left( \frac{\mathbf{P}_p.x}{\mathbf{P}_p.w}, \frac{\mathbf{P}_p.y}{\mathbf{P}_p.w}, \frac{\mathbf{P}_p.z}{\mathbf{P}_p.w} \right)$, where $x$, $y$, and $z$ are between $-1$ and $1$.

### 4. Viewport Transformation

- **What it does**: Maps NDC to screen space, adjusting for the display's resolution.
- **How**: Scales and translates NDC to pixel coordinates based on screen width $w$ and height $h$: $$x_s = \left( \frac{\mathbf{P}_{ndc}.x + 1}{2} \right) \cdot w, \quad y_s = \left( \frac{\mathbf{P}_{ndc}.y + 1}{2} \right) \cdot h$$
- **Result**: $\mathbf{P}_s = (x_s, y_s)$, the final 2D screen coordinates.

### Combined Transformation

The full process can be summarized as: $$\mathbf{P}_s = \text{viewport} \left( \text{ndc} \left( \text{projection} \left( \text{view} \left( \mathbf{P}_w \right) \right) \right) \right)$$

---

## Key Differences

|**Feature**|**World Coordinate System**|**Screen Coordinate System**|
|---|---|---|
|**Dimensions**|3D (or 2D for 2D graphics)|2D|
|**Units**|Arbitrary (e.g., meters)|Pixels (discrete)|
|**Origin**|Scene-defined (e.g., center)|Top-left of the screen|
|**Role**|Scene layout and object placement|Final rendering on the display|

---

## Practical Example

Imagine a point $\mathbf{P}_w = (1, 2, 3)$ in world space:

1. **View Transformation**: The camera adjusts it to $\mathbf{P}_c$ based on its position.
2. **Projection Transformation**: It's projected to clip space $\mathbf{P}_p$, accounting for perspective.
3. **Perspective Division**: Normalized to $\mathbf{P}_{ndc}$ (e.g., $(0.5, 0.5, 0.7)$).
4. **Viewport Transformation**: On a 800x600 screen, it becomes $\mathbf{P}_s = (600, 450)$.

This point is now a pixel on the screen, ready to be rendered.

---

## Summary

- The **world coordinate system** is the 3D global space where the scene is defined.
- The **screen coordinate system** is the 2D space of the display where the scene is shown.
- They connect through the graphics pipeline, using view, projection, and viewport transformations to map 3D world coordinates to 2D screen pixels.

This relationship is the foundation of rendering 3D graphics on a 2D screen! Let me know if you'd like more details or examples.