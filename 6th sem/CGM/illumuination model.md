Absolutely! Here's the **in-depth theory of the Basic Illumination Model** rewritten using LaTeX-style math with `$...$` delimiters, perfect for use in **Obsidian**, **Notion**, or any Markdown+LaTeX environment.

---

# 🌟 Basic Illumination Model (Phong Model) — In-Depth with LaTeX

The **Phong Illumination Model** simulates how light interacts with a surface to produce realistic lighting. It combines **ambient**, **diffuse**, and **specular** components to compute the final intensity:

I=Iambient+Idiffuse+IspecularI = I_{\text{ambient}} + I_{\text{diffuse}} + I_{\text{specular}}

---

## 🔶 1. Ambient Illumination

### 💡 Concept:

Simulates **indirect light** scattered from the environment. It ensures all surfaces are slightly lit even without direct light.

### 📐 Formula:

Iambient=ka⋅IaI_{\text{ambient}} = k_a \cdot I_a

- $k_a$: Ambient reflection coefficient of the material
    
- $I_a$: Ambient light intensity in the scene
    

✅ Independent of surface orientation, light direction, or viewer position.

---

## 🔶 2. Diffuse Illumination (Lambertian Reflection)

### 💡 Concept:

Simulates **matte reflection** on rough surfaces. The brightness depends on the **angle** between the light direction and surface normal.

### 📐 Formula:

Idiffuse=kd⋅Il⋅max⁡(0,N⃗⋅L⃗)I_{\text{diffuse}} = k_d \cdot I_l \cdot \max(0, \vec{N} \cdot \vec{L})

- $k_d$: Diffuse reflection coefficient
    
- $I_l$: Intensity of the point light
    
- $\vec{N}$: Surface normal (unit vector)
    
- $\vec{L}$: Vector from surface point to light (unit vector)
    
- $\vec{N} \cdot \vec{L} = \cos\theta$
    

If $\theta > 90^\circ$, the light is behind the surface → no diffuse light.

---

## 🔶 3. Specular Illumination (Highlights)

### 💡 Concept:

Models **shiny or glossy surfaces** that reflect light in a preferred direction. A **highlight** is seen when the viewer aligns with the reflected ray.

### 📐 Formula:

Ispecular=ks⋅Il⋅max⁡(0,R⃗⋅V⃗)nI_{\text{specular}} = k_s \cdot I_l \cdot \max(0, \vec{R} \cdot \vec{V})^n

- $k_s$: Specular reflection coefficient
    
- $I_l$: Light intensity
    
- $\vec{R}$: Perfect reflection vector of $\vec{L}$ about $\vec{N}$
    
- $\vec{V}$: View direction (unit vector from point to camera)
    
- $n$: Shininess exponent (larger = smaller, sharper highlight)
    

**Reflection vector formula:**

R⃗=2(N⃗⋅L⃗)N⃗−L⃗\vec{R} = 2(\vec{N} \cdot \vec{L})\vec{N} - \vec{L}

---

## 🧠 Final Phong Illumination Equation

I=kaIa+∑lights[kdIl(N⃗⋅L⃗)+ksIl(R⃗⋅V⃗)n]I = k_a I_a + \sum_{\text{lights}} \left[ k_d I_l (\vec{N} \cdot \vec{L}) + k_s I_l (\vec{R} \cdot \vec{V})^n \right]

Each light contributes its own diffuse and specular term.

---

## 🧩 Vector Summary

|Vector|Description|
|---|---|
|$\vec{N}$|Unit surface normal|
|$\vec{L}$|Unit vector to light source|
|$\vec{V}$|Unit vector to viewer|
|$\vec{R}$|Reflection vector|
|$\vec{H}$|Halfway vector (used in Blinn-Phong)|

---

## 🔬 Material Coefficients

|Symbol|Meaning|
|---|---|
|$k_a$|Ambient reflection coefficient|
|$k_d$|Diffuse reflection coefficient|
|$k_s$|Specular reflection coefficient|
|$n$|Shininess exponent|

Each coefficient may be defined per color channel (R, G, B).

---

## 🚫 Limitations of Phong Model

- No **shadows**, **reflections**, or **refractions**
    
- No **global illumination** (no light bouncing)
    
- Assumes **point lights** only
    
- Not physically accurate — it's empirical
    

---

## 🔧 Extensions

- **Blinn-Phong Model**: Uses a **halfway vector** $\vec{H} = \frac{\vec{L} + \vec{V}}{|\vec{L} + \vec{V}|}$ to simplify specular computation.
    
- **Cook-Torrance Model**: More physically-based, includes microfacet theory.
    
- **PBR (Physically Based Rendering)**: Modern rendering with energy-conserving BRDFs.
    

---

Let me know if you'd like a **vector diagram**, or the **Blinn-Phong model** written the same way!