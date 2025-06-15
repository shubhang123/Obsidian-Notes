
Here is the extracted text from the image:

---

**Steps of Sutherland Hodgman Polygon Clipping Algorithm:**

1. Read the coordinates of all vertices of the polygon. ✔
    
2. Read the coordinates of the clipping window. ✔
    
3. Consider the left edge of the window. ✔
    
4. Compare the vertices of the edge of the polygon individually with the clipping plane.
    
5. Save the resulting intersections and the vertices according to the rules.
    
6. Repeat step ④ and ⑤ for the remaining edges of the clipping window.
    
7. Each time pass the resultant list of vertices to the next edge of the clipping window.
    
8. STOP.
    

---

Let me know if you'd like this reformatted, converted to a flowchart, or turned into code.
Here's the Sutherland-Hodgman Polygon Clipping Algorithm written in text based on the handwritten notes:

**Sutherland-Hodgman Polygon Clipping Algorithm:**

**Input:**

- Polygon vertices: C₁ = Xₘₐₓ, C₂ = Yₘₐₓ, C₃ = Xₘᵢₙ, C₄ = Yₘᵢₙ corresponding to the left, right, top, and bottom window boundaries
- The polygon is specified in terms of its vertex list Vᵢₙ = {V₁, V₂, ..., Vₙ} where the vertices are named anticlockwise

**Algorithm Steps:**

1. **Initialize:** Input your clippers
    
2. **For each clipper in the order C₁, C₂, C₃, C₄:**
    
3. **Set output vertex list Vₒᵤₜ = NULL, i=1, j=1**
    
4. **Repeat:**
    
5. **Consider the vertex pair Vᵢ & Vⱼ in Vᵢₙ**
    
6. **If Vᵢ is inside and Vⱼ outside then:**
    
    - Add the intersection point of the clipper with the edge (Vᵢ, Vⱼ) to Vₒᵤₜ
7. **Else if both the vertices are inside the clipper then:**
    
8. **Add Vⱼ to Vₒᵤₜ**
    
9. **Else if Vᵢ is outside & Vⱼ inside of the clipper then:**
    
10. **Add the intersection point of the clipper with the edge (Vᵢ, Vⱼ) and Vⱼ to Vₒᵤₜ**
    
11. **Else:**
    
    - **Add NULL to Vₒᵤₜ**
12. **End if**
    
13. **Until all edges (i.e. consecutive vertex pairs) in Vᵢₙ are checked**
    
14. **Set Vᵢₙ = Vₒᵤₜ**
    
15. **End for**
    
16. **Return Vₒᵤₜ**
    

This algorithm clips a polygon against a rectangular window by processing each edge of the clipping window sequentially, maintaining a list of vertices that represent the clipped polygon after each stage.