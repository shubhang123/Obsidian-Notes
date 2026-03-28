---
title: "Risk mgmt"
aliases: []
type: "note"
area: "study"
topic:
  - "6th-sem"
  - "software-engineering"
  - "unit-1"
status: "seed"
created: 2026-03-28
updated: 2026-03-28
tags:
  - "area/study"
  - "type/note"
  - "topic/6th-sem"
  - "topic/software-engineering"
  - "topic/unit-1"
---


## 🛡️ Safety and Risk Assessment in Software Engineering

---

### 🔷 **Safety**

**Software safety** is a **software quality assurance activity** that focuses on:

- **Identifying and assessing potential hazards** in software
    
- Understanding how such hazards could cause **system-wide failure**
    
- Ensuring that **design features are specified early** to either **eliminate** or **control** these hazards
    

> Unlike **reliability**, which deals with the **likelihood of failure**, **safety** is concerned with **how failures can lead to catastrophic outcomes** (mishaps).

**Key Characteristics:**

- Software is analysed within the **context of the entire system** (e.g., hardware, human interactions, and environment).
    
- **Security** is considered a **prerequisite** for safety — a vulnerable system is an unsafe system.
    
- **Example**: In a computer-based **cruise control** system:
    
    - Hazards may include **uncontrolled acceleration** or **failure to respond to the brake pedal**.
        

---

### 🔶 **Risk Assessment**

**Risk Assessment** is a key part of **risk management**, aimed at **understanding and managing uncertainty** in software projects.

#### 📌 What is a Risk?

A **risk** is defined as a:

- **Potential problem**
    
- Characterised by **uncertainty**
    
- Accompanied by a possibility of **loss**
    

---

### 🔎 Steps in Risk Assessment:

---

#### 1️⃣ **Risk Identification**

- Systematically specify potential **threats** to the project or product.
    
- Risks may be:
    
    - **Known**
        
    - **Predictable**
        
    - **Unpredictable**
        
- Categorised as:
    
    - **Generic risks** – affect all projects (e.g., staffing issues, unrealistic deadlines)
        
    - **Product-specific risks** – unique to the software being developed
        

---

#### 2️⃣ **Risk Projection (Estimation)**

- Rate each risk based on:
    
    - **Likelihood (Probability)**
        
    - **Impact (Consequence)**
        
- Use a **risk table** to prioritise:
    
    - High-probability + High-impact risks are addressed first.
        
- Calculate **Risk Exposure (RE)**:
    
    Risk Exposure (RE)=Probability×Cost\text{Risk Exposure (RE)} = \text{Probability} \times \text{Cost}
- If **RE exceeds 50%** of the project’s estimated cost, the **project's viability must be re-evaluated**.
    

---

#### 3️⃣ **Risk Refinement**

- General risks are broken down into more detailed and manageable components.
    
- A common approach is using the **CTC format**:
    
    - **Condition**: Under what condition does the risk occur?
        
    - **Transition**: What causes the condition to become active?
        
    - **Consequence**: What is the result or loss if the risk occurs?
        

---

#### 4️⃣ **Risk Mitigation, Monitoring, and Management (RMMM)**

- Develop a **comprehensive strategy** that includes:
    
    - **Risk avoidance** (change plans to prevent risk)
        
    - **Risk monitoring** (keep track of risk indicators)
        
    - **Contingency planning** (prepare fallback plans if the risk materialises)
        

---

#### 🔐 **Security Risk Analysis**

- A vital component of risk management
    
- Involves:
    
    - **Threat modelling** – identifying and evaluating security threats
        
    - **Risk prioritisation** – using metrics like **Annual Loss Expectancy (ALE)**
        
    - **Incident Response Plan (IRP)** – outlining actions if a threat becomes real
        

---

### ✅ Summary

|Aspect|Safety|Risk Assessment|
|---|---|---|
|Focus|Preventing catastrophic failures|Identifying, prioritising, and managing project risks|
|Key Concern|How failures lead to harm|Likelihood and impact of uncertain events|
|Analysis Scope|System-wide, includes software-hardware interaction|Project-wide, includes planning and budgeting|
|Tools|Hazard analysis, FMEA, fault trees|Risk table, CTC analysis, threat modelling|
|Relationship|Depends on reliability and security|Enhances reliability and success rate|

---

Let me know if you'd like this converted into a PDF or formatted as a printable one-pager!