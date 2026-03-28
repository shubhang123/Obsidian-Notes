---
title: "1) requirement engineernig"
aliases: []
type: "note"
area: "study"
topic:
  - "6th-sem"
  - "software-engineering"
  - "unit-2"
status: "seed"
created: 2026-03-28
updated: 2026-03-28
tags:
  - "area/study"
  - "type/note"
  - "topic/6th-sem"
  - "topic/software-engineering"
  - "topic/unit-2"
---


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


Here are **detailed and structured notes** on **Functional and Non-Functional Requirements** in Software Engineering.

---

## ✅ **Software Requirements Overview**

In Software Engineering, **requirements** describe what the system should **do** and **how well** it should do it. These are broadly classified as:

1. **Functional Requirements**
    
2. **Non-Functional Requirements**
    

Both are essential to define the **complete behavior** and **quality** of a software system.

---

## 🔷 1. **Functional Requirements (FRs)**

---

### 🔍 **Definition**:

> Functional Requirements define **what the system should do** — they describe the **specific behavior, features, and functions** of the system.

They outline the **services, tasks, or functions** the software must perform.

---

### 📘 **Examples**:

- The system shall allow users to **register and log in**.
    
- The ATM shall **dispense cash** when a valid PIN and amount are entered.
    
- The e-commerce system must allow customers to **add items to a cart** and **checkout**.
    

---

### ⚙️ **Characteristics**:

- Derived from **business requirements** or **use cases**
    
- Usually represented through **SRS**, **use case diagrams**, or **user stories**
    
- Must be **clear**, **complete**, and **testable**
    

---

### 🧩 **Common Functional Areas**:

|Function Type|Description|
|---|---|
|**User Interface**|What the user can do (e.g., log in, fill forms)|
|**Data Processing**|What transformations are applied to data|
|**Business Rules**|Logic for calculations, discounts, workflows|
|**External Interfaces**|Interactions with other systems or APIs|

---

## 🔶 2. **Non-Functional Requirements (NFRs)**

---

### 🔍 **Definition**:

> Non-Functional Requirements define **how the system performs** its functions. They describe the **quality attributes**, constraints, and **system properties**.

---

### 📘 **Examples**:

- The system should respond to user input **within 2 seconds**.
    
- The system must be available **99.99% of the time**.
    
- Passwords should be stored using **SHA-256 encryption**.
    
- The system should support **10,000 concurrent users**.
    

---

### 🧩 **Categories of NFRs**:

|Category|Description|Example|
|---|---|---|
|**Performance**|Speed, response time, throughput|"Search results within 1 second"|
|**Scalability**|Ability to grow with user load|"Support 10k → 1M users"|
|**Reliability**|Continuous correct service|"System available 99.99%"|
|**Usability**|Ease of use|"User can complete signup in ≤ 3 steps"|
|**Security**|Data protection, access control|"Passwords encrypted, 2FA required"|
|**Maintainability**|Ease of changes and updates|"Codebase should have <10 CC per function"|
|**Portability**|Run on various platforms|"App runs on Windows, macOS, Linux"|
|**Compliance**|Legal and regulatory constraints|"Must follow GDPR rules"|

---

### ⚙️ **Characteristics**:

- Often expressed as **constraints**
    
- Harder to measure than functional requirements
    
- Crucial for **user satisfaction and long-term success**
    
- Represent **system-level** expectations
    

---

## 🔁 **Comparison Table: Functional vs Non-Functional Requirements**

|Feature|**Functional Requirement**|**Non-Functional Requirement**|
|---|---|---|
|**Describes**|**What** the system should do|**How well** it performs|
|**Type**|Functional features|Quality attributes|
|**Focus**|User interactions, features|Performance, security, scalability|
|**Testability**|Usually easy to test|Often hard to test precisely|
|**Examples**|Login, register, search|Load time <2 sec, encryption|
|**Stakeholder**|Business Analyst, End-user|Architect, QA, DevOps, Security team|
|**Representation**|Use cases, user stories|Service Level Agreements (SLAs), metrics|

---

## 🔐 **Importance of Both**:

|Requirement Type|Importance|
|---|---|
|Functional|Ensures the system delivers required **features**|
|Non-Functional|Ensures the system meets **user expectations**, quality, and compliance|

A system **can fail even if all functional requirements are met** if the non-functional ones are ignored — e.g., a website that works but is slow, insecure, or hard to use.

---

## ✅ Summary:

|Term|Functional Requirement|Non-Functional Requirement|
|---|---|---|
|Focus|**Behavior** of the system|**Quality** of the system|
|Scope|Specific tasks and interactions|System-wide constraints and attributes|
|Measurement|Pass/fail via test cases|Often with metrics or SLAs|
|Critical for|Building the right features|Building the features right|

---

Let me know if you’d like examples in the form of **use case tables**, **SRS templates**, or **Agile user stories vs NFR backlogs**!