---
title: "4 software metrics"
type: "note"
area: "study"
topic:
  - "6th-sem"
  - "software-engineering"
status: "draft"
created: 2026-03-28
updated: 2026-03-28
tags:
  - "area/study"
  - "type/note"
  - "topic/6th-sem"
---

Here is a **detailed and comprehensive explanation of all major types of software metrics**, their definitions, formulas, uses, advantages, and limitations.

---

## 🔰 **What are Software Metrics?**

> **Software metrics** are **quantitative measures** that are used to assess different aspects of software development and software quality, such as complexity, performance, maintainability, reliability, and productivity.

They provide **objective insight** into the development process and the product, helping in **project tracking**, **quality assurance**, **risk analysis**, and **process improvement**.

---

## 🧩 **Classification of Software Metrics**

Software metrics can be classified broadly into:

1. **Product Metrics**
    
2. **Process Metrics**
    
3. **Project Metrics**
    
4. **Internal vs External Metrics**
    
5. **Size-Oriented vs Function-Oriented Metrics**
    
6. **Code-Based vs Design-Based Metrics**
    

---

## 1️⃣ **Product Metrics**

> Measure **characteristics of the software product** itself — its size, complexity, design quality, performance, and correctness.

### 🔹 Common Product Metrics:

|Metric|Description|Formula / Details|
|---|---|---|
|**Lines of Code (LOC)**|Measures size of source code|Count number of physical/executable lines|
|**Function Points (FP)**|Measures size based on functionality delivered to user|FP = UFP × TCF (from input/output/inquiry/file complexity + 14 GSCs)|
|**Cyclomatic Complexity**|Measures decision complexity in control flow|M = E – N + 2P or M = D + 1|
|**Halstead Metrics**|Based on operators and operands|Vocabulary (n), Program Length (N), Volume, Difficulty, Effort|
|**Defect Density**|Measures code quality via defects|Defect Density = Defects / KLOC|
|**Maintainability Index**|Assesses maintainability of code|Weighted formula using LOC, Cyclomatic Complexity, Halstead Volume|
|**Code Churn**|Measures how frequently code changes|Code Churn = Lines Added + Modified – Deleted|

---

## 2️⃣ **Process Metrics**

> Measure the **efficiency and effectiveness of software development and maintenance processes**.

### 🔹 Common Process Metrics:

|Metric|Description|Notes|
|---|---|---|
|**Defect Removal Efficiency (DRE)**|% of total defects removed before release|DRE = (Defects found before release / Total defects) × 100|
|**Review Efficiency**|Defects found during reviews vs total|High value indicates strong early testing|
|**Test Coverage**|% of code executed by tests|Test Coverage = Covered LOC / Total LOC|
|**Cycle Time**|Time to complete one unit of work|Used in Agile/DevOps|
|**Lead Time**|Time from request to delivery|Key for customer responsiveness|

---

## 3️⃣ **Project Metrics**

> Concerned with **project-level tracking** — cost, schedule, effort, resource allocation, risk, and productivity.

### 🔹 Common Project Metrics:

|Metric|Description|Formula|
|---|---|---|
|**Schedule Variance (SV)**|Measures deviation from planned schedule|SV = EV – PV|
|**Cost Variance (CV)**|Difference between earned value and actual cost|CV = EV – AC|
|**Effort Variance**|Estimated effort vs actual effort|EV = (Estimated – Actual) / Estimated × 100|
|**Productivity**|Output per unit input|Productivity = LOC / person-hour or FP / person-month|
|**Requirement Stability Index**|Change in requirements over time|RSI = 1 – (Number of changes / Total requirements)|

---

## 4️⃣ **Internal vs External Metrics**

|Type|Description|Example|
|---|---|---|
|**Internal Metrics**|Applied **within** the system (code structure, design, logic)|LOC, Cyclomatic Complexity, Coupling|
|**External Metrics**|Applied to **system behavior** (observable by users)|Reliability, Response Time, Availability, Usability|

---

## 5️⃣ **Size-Oriented vs Function-Oriented Metrics**

### 🔹 Size-Oriented Metrics:

- Based on physical size of software (e.g., LOC)
    
- Examples: LOC, KLOC, Defects/KLOC, Errors/1000 LOC
    

### 🔹 Function-Oriented Metrics:

- Based on functionality delivered to the user
    
- Examples: Function Points, FP/Person-Month, Defects/FP
    

---

## 6️⃣ **Code Quality Metrics (Design-Based)**

|Metric|What it Measures|Good Range|
|---|---|---|
|**Cohesion**|Degree to which elements of a module belong together|High cohesion preferred|
|**Coupling**|Degree of interdependence between modules|Low coupling preferred|
|**Depth of Inheritance Tree (DIT)**|Depth of class hierarchy|Moderate depth is good|
|**Number of Children (NOC)**|Subclasses under a class|Helps identify reuse or complexity|
|**Class Fan-in/Fan-out**|Number of classes using/used by a class|Too high = complex dependencies|

---

## 📘 **Advanced Metrics**

### 1. **Halstead Metrics**:

Based on software vocabulary:

- n1 = number of distinct operators
    
- n2 = number of distinct operands
    
- N1 = total number of operators
    
- N2 = total number of operands
    

Program Length (N)=N1+N2\text{Program Length (N)} = N1 + N2 Vocabulary (n)=n1+n2\text{Vocabulary (n)} = n1 + n2 Volume (V)=N⋅log⁡2(n)\text{Volume (V)} = N \cdot \log_2(n) Difficulty (D)=(n1/2)⋅(N2/n2)\text{Difficulty (D)} = (n1/2) \cdot (N2/n2) Effort (E)=D⋅V\text{Effort (E)} = D \cdot V

---

### 2. **Maintainability Index (MI)**:

A composite metric using:

- Cyclomatic Complexity (CC)
    
- Halstead Volume (V)
    
- Lines of Code (LOC)
    

MI=171−5.2⋅log⁡(V)−0.23⋅CC−16.2⋅log⁡(LOC)MI = 171 - 5.2 \cdot \log(V) - 0.23 \cdot CC - 16.2 \cdot \log(LOC)

- **MI > 85** → easy to maintain
    
- **65 < MI < 85** → moderate
    
- **< 65** → hard to maintain
    

---

## 🧠 **Summary Table**

|Type|Examples|Purpose|
|---|---|---|
|**Product Metrics**|LOC, FP, Defect Density|Measure software quality & size|
|**Process Metrics**|DRE, Review Efficiency|Evaluate development/testing process|
|**Project Metrics**|Cost, Time, Effort, Productivity|Track and control project execution|
|**Internal Metrics**|Cyclomatic Complexity, Cohesion|Assess internal code quality|
|**External Metrics**|Reliability, Usability|Reflect real-world software usage|
|**Size/Function Metrics**|LOC vs FP|Choose based on stage, visibility, and abstraction|

---

Let me know if you'd like visual charts or a breakdown of specific metrics per SDLC phase!
