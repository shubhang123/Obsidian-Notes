
# 📘 **Complete Notes on Requirement Engineering**

---

## 📌 1. **Definition: Requirement Engineering**

**Requirement Engineering (RE)** is a systematic process of defining, documenting, and maintaining the requirements for a software system.  
It involves understanding **what the user needs** and ensuring that the system being built **meets those needs**.

---

## 📌 2. **Difficulties in Requirement Engineering**

Requirement Engineering can be challenging due to several reasons:

### 🛑 Common Difficulties:

- **Ambiguous Requirements**: Vague or unclear statements lead to misinterpretation.
    
- **Incomplete Requirements**: Some features or constraints are missing.
    
- **Changing Requirements**: Stakeholders may change needs mid-project.
    
- **Conflicting Requirements**: Stakeholders may have opposing views.
    
- **Communication Gaps**: Between clients, users, and developers.
    
- **Lack of Stakeholder Involvement**: Leads to irrelevant or incorrect requirements.
    
- **Poor Domain Knowledge**: Developers may not fully understand the business context.
    
- **Non-verifiable Requirements**: Some cannot be tested (e.g., "System must be user-friendly").
    

---

## 📌 3. **Types of Requirements**

### ✅ Known Requirements

- Clearly stated and understood.
    
- Example: “Login must use OTP.”
    

### ❓ Unknown Requirements

- Not known at the start but discovered during development.
    
- Example: Need for caching after performance issues arise.
    

### 💡 Undreamt Requirements

- Users didn’t know they needed it until they see it.
    
- Example: Swipe-to-delete feature in email apps.
    

---

## 📌 4. **Steps in Requirement Engineering Process**

### 🔁 The steps are:

|Step|Description|
|---|---|

### 1. **Inception**

- Identify stakeholders.
    
- Understand business context.
    
- Establish high-level goals and feasibility.
    
- Outcome: Vision or project charter.
    

### 2. **Elicitation**

- Gather user and stakeholder needs.
    
- Techniques: Interviews, Surveys, Observation, Prototyping, Workshops.
    

### 3. **Elaboration**

- Analyze, structure, and detail the requirements.
    
- Use diagrams (UML, DFDs) and models.
    
- Define functional and non-functional requirements.
    

### 4. **Negotiation**

- Resolve conflicts between stakeholders.
    
- Prioritize requirements using MoSCoW, Kano Model, etc.
    

### 5. **Specification**

- Document requirements formally.
    
- Create the **SRS (Software Requirement Specification)** document.
    

### 6. **Validation**

- Ensure requirements are correct, complete, and feasible.
    
- Use reviews, walkthroughs, and acceptance criteria.
    

### 7. **Management**

- Track changes, maintain versions.
    
- Create a **Requirements Traceability Matrix (RTM)**.
    

---

## 📌 5. **Requirement Elicitation**

### 🧠 **Definition**:

The process of collecting requirements from stakeholders through various techniques to understand what the system should do.

---

### 📋 **Methods of Requirement Elicitation**

|Method|Description|Use Case|
|---|---|---|
|**Interviews**|Direct Q&A with stakeholders|For in-depth understanding|
|**Surveys/Questionnaires**|Written questions to many users|When user base is large|
|**Observation**|Watch users in their environment|For replacing manual systems|
|**Workshops**|Collaborative requirement sessions|When dealing with multiple stakeholders|
|**Prototyping**|Build a mock-up to get feedback|Useful for UI-heavy systems|
|**Document Analysis**|Study existing systems, manuals|For system migration or upgrade|
|**Use Cases**|Describes user interactions with the system|Clarifies functional requirements|

---

## 📌 6. **Requirement Analysis**

### 🎯 **Goal**:

To understand, validate, prioritize, and organize the requirements collected.

### 📌 **Activities**:

- Categorization: Functional, Non-functional, Business, User, System
    
- Prioritization: Must-have, Should-have, Could-have, Won’t-have
    
- Modeling: DFDs, ER diagrams, Use case diagrams
    
- Risk Analysis: Identifying risks related to requirements
    
- Conflict Resolution: Aligning competing requirements
    

### ✅ **Outcomes**:

- A clear, structured set of requirements ready for specification.
    
- Identified and resolved conflicts.
    
- Validated scope and feasibility.
    

---

## 📌 7. **Software Quality Assurance (SQA)**

### 🔧 **Definition**:

SQA is a set of activities that ensure software processes and products conform to requirements, standards, and procedures.

### 📌 **Activities of SQA**:

- Quality Planning
    
- Process Definition
    
- Reviews and Inspections
    
- Testing and Validation
    
- Metrics and Reporting
    
- Configuration Management
    
- Audits and Compliance
    
- Risk Management
    
- Training and Documentation
    

---

## 📌 8. **SQA Plan and its Components**

### 📄 **SQA Plan**:

A formal document that outlines how quality will be assured throughout the software lifecycle.

### 📋 **Key Constituents**:

1. **Purpose and Scope**
    
2. **Reference Documents**
    
3. **Quality Goals**
    
4. **SQA Tasks and Activities**
    
5. **Roles and Responsibilities**
    
6. **Standards and Practices**
    
7. **Tools and Techniques**
    
8. **Metrics**
    
9. **Reviews and Audits**
    
10. **Risk Management**
    
11. **Training**
    
12. **Change Control**
    
13. **Configuration Management**
    

---

## 📌 9. **Feasibility Study**

### 🎯 **Definition**:

A feasibility study assesses whether the project is technically, financially, legally, and operationally viable.

### 📌 **Types of Feasibility**:

|Type|Focus|
|---|---|
|**Technical**|Can the system be built with current tech?|
|**Economic**|Is the project cost-effective?|
|**Operational**|Will users and business adopt it?|
|**Legal**|Are there regulatory/legal constraints?|
|**Schedule**|Can it be delivered on time?|

---

## 🧾 Summary Diagram (Visual Flow)

```
Requirement Engineering Process
┌────────────┐
│ Inception  │
└────┬───────┘
     ▼
┌───────────────┐
│ Elicitation   │
└────┬──────────┘
     ▼
┌───────────────┐
│ Elaboration   │
└────┬──────────┘
     ▼
┌───────────────┐
│ Negotiation   │
└────┬──────────┘
     ▼
┌───────────────┐
│ Specification │
└────┬──────────┘
     ▼
┌───────────────┐
│ Validation    │
└────┬──────────┘
     ▼
┌───────────────┐
│ Management    │
└───────────────┘
```
