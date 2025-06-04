# Software Life cycle models
1.  Classical Waterfall Model
2.  Iterative waterfall model
3.  Iterative Incremental model
4.  Prototyping model
5.  Spiral model
    *   Win-Win Spiral
6.  RUP process model
7.  V-Shape Model
8.  RAD Model
9.  Big bang model
10. Agile Process model
    *   Popular frameworks
        *   Scrum
        *   Kanban
        *   Extreme Programming
        *   Lean
        *   DevOps
---

# Waterfall Model

The **Waterfall Model** is the simplest Software Development Life Cycle (SDLC) model in which phases are organized in a **linear and sequential** manner.  
It is called the **Waterfall Model** because its diagrammatic representation resembles a waterfall. It is also known as the **Classical Life Cycle Model**.

This model is mainly used for **small to medium-sized projects** with **clear, well-defined requirements**, where the technology and tools to be used are **well-known and stable**.  
It is suitable for projects where **minimal changes are expected** during development and where **predictability** is prioritized.
### When to use the waterfall model:
*   This model is used only when the **requirements** are very well **known, clear and fixed**.
*   Product definition is **stable**.
*   Technology is understood.
*   There are **no ambiguous requirements**.
*   **Ample resources** with required **expertise** are available freely.
*   The project is **short**.
*   Very less customer interaction is involved during the development of the product.
*   Once the product is ready then only it can be demoted to the end users.
*   Once the product is developed and if any failure occurs then the **cost of fixing such issues are very high**, because we need to update everywhere from document till the logic.
---
### Advantages

- Easy to understand and implement, with well-defined stages and clear milestones.
    
- Each phase has a well-defined input and output; phases are processed and completed one at a time without overlap.
    
- Low cost and easy to schedule, as all team members are not required to work concurrently—allowing them to work on multiple projects.
    

---
### Disadvantages

- Not suitable for accommodating changes or iterations once development has started.
    
- Difficult to gather complete and accurate requirements at the beginning.
    
- Working software is produced only at the final phase, making it unsuitable for **large, sophisticated projects**.
    
- High levels of risk and uncertainty.
    
![[waterfall.png]]
---

# Prototype Model

In many cases, customers are **unsure about the exact functionality** they want in the software. As a result, the final product may not match their expectations.

The **Prototype Model** is an **iterative** software development approach that involves building an **early working model** (prototype) of the system with **limited functionality**, **low reliability**, and **unverified performance**.

The prototype is then **shown to the user**, who provides feedback. Based on this feedback, the prototype is **modified and rebuilt**, and the updated version is again presented to the user. This **loop continues** until the customer is satisfied.

Once the prototype has been refined to the point where the user is satisfied, a **final Software Requirement Specification (SRS)** document is created. This document becomes the foundation for the actual system development.

Creating a prototype helps in understanding the customer’s needs more precisely and assists in developing the **actual design and architecture** of the final product.

---

## Types of Prototype Model

### 1. **Evolutionary Prototype**

- This type of prototype is **gradually refined and evolved** into the final product.
    
- It is **not discarded**; rather, it serves as the base upon which the final system is built.
    
- Useful when requirements are **incomplete or constantly changing**.
    
- Focuses on delivering a **working system** early and improves it with user feedback.
    

> ✅ _Use Case:_ Long-term projects where requirements are expected to evolve.

---

### 2. **Throwaway (Rapid) Prototype**

- Also called **Rapid Prototyping**, this model creates a prototype **quickly** to understand user requirements.
    
- The prototype is built only to gather feedback and is **discarded after use**.
    
- The actual system is then developed from scratch based on the final, clarified requirements.
    

> ✅ _Use Case:_ When the goal is to understand unclear or vague requirements quickly, without reusing the prototype code.

---

Let me know if you want a visual diagram or side-by-side comparison between the two types.







### 
![[prototype.png]]
---

### Advantages

- Encourages **active user involvement** during early stages.
    
- Helps clarify **user requirements** and expectations.
    
- Provides **quick feedback** to developers, reducing the chances of software mismatches.
    
- Reduces the risk of **miscommunication** between client and developer.
    
### Disadvantages

- Customer demand can increase after seeing prototype asking for the product early.
    
- without proper management itreations can take lot of time
    
- if user is not satisfied the customer can lose intrest in the project

# Spiral Model

The **Spiral Model** was first introduced by **Barry Boehm in 1986**, and it emphasizes **risk management** at every phase of the software development lifecycle.  
It is a **combination of iterative development** and the **systematic aspects of the Waterfall Model**, with a strong focus on **risk assessment**.

In this model:

- The **radial dimension** represents the **cumulative cost** incurred so far.
    
- Each **loop** around the spiral indicates a **development phase**, and the path length represents the **cost of the phase**.
    
- The **angular dimension** (i.e., rotation from the starting point) represents the **progress** in completing each phase.
    

Each loop of the spiral (starting from the x-axis and moving **clockwise through 360°**) represents one phase of the development process. Each phase is divided into **four major sectors**:
![[Pasted image 20250604144239.png]]
---

## 📐 Sectors of the Spiral Model

1. **Determine Objectives and Plan the Next Phase**
    
    - Define goals, alternatives, and constraints.
        
    - Plan for the upcoming iteration.
        
2. **Risk Analysis**
    
    - Identify and analyze risks.
        
    - Explore ways to eliminate or mitigate the highest-risk elements.
        
3. **Engineering (Development and Testing)**
    
    - Actual development of the product: designing, coding, and testing.
        
4. **Customer Evaluation**
    
    - Review by the customer and validation of the deliverable.
        
    - Feedback is collected to refine objectives and plan the next iteration.
        

---

## ✅ Advantages

- **Risk is explicitly assessed and managed** at every phase.
    
- Supports **early development of prototypes** for better customer feedback.
    
- Allows for **changes and refinements** at each loop.
    
- Suitable for **complex and high-risk projects**.
    
- Focuses on **continuous improvement** through iterative refinement.
    

---

## ❌ Disadvantages

- Can be **complex to manage and implement** due to its flexible and evolving nature.
    
- **Not suitable for small or low-risk projects** (overhead is too high).
    
- **Requires expertise in risk assessment** and project planning.
    
- Can be **expensive and time-consuming**, especially if too many iterations are involved.
    

---

# Iterative Model

*[Image: Diagram of the Iterative Model]*

In this Model, you can **start with** some of the software specifications and **develop the first version of the software.**
After the first version if there is a need to change the software, then a **new version of the software is created with a new iteration.**
Every release of the Iterative Model finishes in an exact and fixed period that is called iteration.

The Iterative Model allows the **accessing earlier phases, in which the variations made respectively.**
The final output of the project renewed at the end of the Software Development Life Cycle (SDLC) process.

### The various phases of Iterative model are as follows:
1.  **Requirement gathering & analysis**: Requirements are **gathered** from customers and **check by an analyst** whether requirements **will fulfil or not**. Analyst checks that need will **achieve within budget or not**.
2.  **Design**: Team design the software by the different diagrams like Data Flow diagram, activity diagram, class diagram, state transition diagram, etc.
3.  **Implementation**: In the implementation, requirements are written in the coding language and transformed into computer programmes which are called Software.
4.  **Testing**: software testing starts using different test methods : white box, black box, and grey box test methods.
5.  **Deployment**: After completing all the phases, software is deployed to its work environment.
6.  **Review**: In this phase, after the product deployment, review phase is performed **to check the behaviour and validity of the developed product**. And if there are **any error found** then the **process starts again from the requirement gathering**.
7.  **Maintenance**: In the maintenance phase, after deployment of the software in the working environment there may be some bugs, some errors or new updates are required. Maintenance involves debugging and new addition options.

### When to use the Iterative Model?
*   When **requirements** are defined **clearly and easy** to understand.
*   When the **software application is large**.
*   When there is a **requirement of changes in future**.

### Advantage (Pros) of Iterative Model:
*   Testing and debugging during smaller iteration is easy.
*   A **Parallel development** can plan.
*   It is **easily acceptable to ever-changing needs** of the project.
*   **Risks are identified and resolved during iteration**.
*   Limited time spent on documentation and extra time on designing.

### Disadvantage (Cons) of Iterative Model:
*   It is **not suitable for smaller projects**.
*   **More Resources** may be required.
*   **Design can be changed again and again** because of imperfect requirements.
*   **Requirement changes** can cause **over budget**.
*   Project **completion date not confirmed** because of changing requirements.
# Incremental Model

The **Incremental Model** is a software development approach where the product is designed, implemented, and tested **incrementally** (a little more is added each time) until the complete system is ready.

Instead of delivering the complete software at once, it is developed in **small, manageable parts (increments)**. Each increment adds **functional capabilities** to the previous version.

---

## 🛠️ Key Characteristics

- Each increment is a **functional component** of the system.
    
- The first increment is often the **core product** with basic features.
    
- Subsequent increments **enhance or extend** the existing product.
    
- User feedback from each increment can influence future development.
    
- Can be used with **both linear and iterative approaches**.
    

---

## 🔁 Phases of the Incremental Model

1. **Requirements Analysis**
    
2. **Design of the Increment**
    
3. **Implementation and Testing**
    
4. **Integration with Previous Increments**
    
5. **User Evaluation and Feedback**
    
6. **Repeat Until Final Product is Complete**
    

---

## ✅ Advantages

- **Faster delivery** of working software; early increments can be released and used.
    
- **Easier to test and debug**, since issues are confined to individual increments.
    
- Allows **partial implementation** of the system when full functionality is not yet known.
    
- **Customer feedback** can be incorporated early and frequently.
    
- **Low initial delivery cost** and reduced risk.
    
- Well-suited for projects with **clear high-priority features** needed early.
    

---

## ❌ Disadvantages

- **Requires good planning** and clear modular architecture to divide increments properly.
    
- Integration of increments may become **complex** as the number of increments increases.
    
- If requirements are **poorly understood**, initial increments may need rework.
    
- Not suitable for **tight-budget or low-resource** projects if ongoing development costs are high.
    
- **Incomplete system** in early phases may not be acceptable to all stakeholders.
    

---



# Differences

### 🧩 **Aspect**: Evolutionary Development Models

|**Feature**|**Details**|
|---|---|
|**Focus**|Adaptation and evolution of software based on changing requirements and user feedback.|
|**Initial Release**|Often starts with a basic prototype or partially functional system.|
|**Development Approach**|Develops through repeated cycles, refining and expanding with each iteration.|
|**Feedback Integration**|Strong emphasis on user feedback, often leading to major changes between stages.|
|**Examples**|Prototyping Model, Spiral Model, Agile Development, RAD.|

---

## 🔁 Iterative Enhancement Models

|**Feature**|**Details**|
|---|---|
|**Focus**|Continuous improvement and refinement of a working software system.|
|**Initial Release**|Starts with a functional version having basic features.|
|**Development Approach**|Enhances the system through successive iterations, each adding improvements.|
|**Feedback Integration**|Uses feedback in each iteration to make small, incremental changes.|
|**Examples**|Agile Development (focused on refinement), Iterative Development Model.|

---

## ✅ Difference Between Evolutionary and Iterative Enhancement Models

|**Criteria**|**Evolutionary Development Models**|**Iterative Enhancement Models**|
|---|---|---|
|**Purpose**|Focus on adapting to changing requirements from the beginning.|Focus on refining an already working system.|
|**Initial Output**|Prototype or partial system.|Functional system with basic capabilities.|
|**Nature of Changes**|Often major changes between stages.|Typically small, incremental improvements.|
|**Feedback Usage**|Guides direction and structure of the product.|Used to refine and improve specific parts of the product.|
|**Examples**|Prototyping, Spiral, RAD, Agile.|Agile (enhancement-centric), Iterative Development Model.|

Let me know if you'd like this in a printable or presentation-ready format!

# Iterative Incremental model

*[Image: Diagram of the Iterative Incremental Model combining both approaches]*

The Iterative methodology was an early precursor to Agile. It **emphasized iterative and incremental action**.
Its earliest reported use was as part of NASA’s Project Mercury in the early 1960s.
The Iterative model is repetition incarnate.
Instead of starting with fully known requirements, **implement a set of software requirements**, then test, evaluate and pinpoint further requirements.
A new version of the software is produced with each phase, or iteration. Rinse and repeat until the complete system is ready.

*[Image: Another representation of Iterative Incremental Model phases]*

### Advantage / Disadvantage
*   **Advantage**: This model gives you a **working version early** in the process and makes it **less expensive to implement changes.**
*   **Disadvantage**: **Resources can quickly be eaten up** by repeating the process again and again.

### The various phases of incremental model are as follows:
1.  **Requirement analysis**: crucial role. The product analysis expert identifies the requirements, and the system functional requirements are understood by the requirement analysis team.
2.  **Design & Development**: the design of the system functionality and the development method are finished with success. When software develops new practicality, the incremental model uses style and development phase.
3.  **Testing**: the testing phase **checks the performance of each existing function as well as additional functionality**. In the testing phase, the various methods are used to test the behavior of each task.
4.  **Implementation**: Implementation phase **enables the coding phase of the development system.** It involves the final coding that design in the designing and development phase and tests the functionality in the testing phase. After completion of this phase, the number of the product working is enhanced and upgraded up to the final system product.

### When to use Iterative Incremental Model:
*   The **Requirements should be known clearly and understood**, when there is a **demand for the early release** of the product is there, when there are **high-risk features** and **requirement goals are present in the objective of the software**.
*   This kind of methodologies are mainly followed by **product-based companies** as the defects risk in the developed software are quite minimum and used in developing software in web applications.
*   This model is also preferred when the **project has lengthy development schedules.**
*   Also, if the development is adopting **new technology** in the software development, then also this method is preferred as the **developers are new to the technology**.
*   When the **requirements are superior**.
*   A project has a **lengthy development schedule**.
*   When Software **team are not very well skilled or trained**.
*   When the customer demands a **quick release** of the product.
*   You can **develop prioritized requirements first.**

### Advantages of Iterative Incremental Model:
*   Since the object will be divided into incremental stages, it will be made sure that **100% requirements are achieved** and **100% objective of the software**.
*   Since there is testing at each incremental phase there will be **multiple testing for the software** and **more the testing better the result and fewer defects**.
*   By adopting this approach, we can **lower the initial delivery cost**.
*   This model is **flexible** and **incurs less cost** when there is a change in the requirement or the scope.
*   The user or the **customer can provide feedback on each stage** so work effort will be valued and sudden changes in the requirement can be prevented.
*   By following this model **errors can be identified quiet easily**.
*   Easier to test and debug.
*   Simple to manage risk because it handled during its iteration.
*   The Client gets important functionality early.

### Disadvantages of Iterative Incremental Model:
*   Need for good **planning**.
*   Total Cost is **high**.
*   Well defined module interfaces are needed.

---
# Evolutionary Process Model
The evolutionary model is a combination of the **Iterative** and **Incremental models** of the software development life cycle.
Source: [https://artoftesting.com/evolutionary-model-in-software-engineering](https://artoftesting.com/evolutionary-model-in-software-engineering)

Resembles the **iterative enhancement model**.
This model differs from the iterative enhancement model in the sense that **this does not require a useful product at the end of each cycle.**
In evolutionary development, requirements are **implemented by category rather than by priority**.

*[Image: Diagram of the Evolutionary Process Model]*

For example, in a **simple database application**:
*   one cycle might implement the graphical user Interface (**GUI**),
*   another **file** manipulation,
*   another **queries** and
*   another **updates**.
All four cycles must complete before there is a working product available.
GUI allows the users to interact with the system, file manipulation allow the data to be saved and retrieved, queries allow user to get out of the system, and updates allows users to put data into the system.

### Benefits of Evolutionary Process Model
*   Use of EVO brings a **significant reduction in risk** for software projects.
*   EVO can **reduce costs** by providing a structured, disciplined avenue for experimentation.
*   EVO allows the marketing department access to early deliveries, facilitating the development of documentation and demonstration.
*   Better fit the product to **user needs and market requirements.**
*   Manage **project risk with the definition of early cycle content.**
*   **Uncover key issues early and focus attention appropriately**.
*   Increase the opportunity to hit market windows.
*   **Accelerate sales cycles with early customer exposure**.
*   **Increase management visibility of project progress**.