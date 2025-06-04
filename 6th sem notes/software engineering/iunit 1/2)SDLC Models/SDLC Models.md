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

An evolutionary software process model that couples the **iterative feature of prototyping with the controlled and systematic aspects of the linear sequential model.**
It implements the potential for **rapid development** of new versions of the software.

Using the spiral model, the **software is developed in a series of incremental releases.**
During the early iterations, the additional release may be a **paper model or prototype**.
During later iterations, more and more **complete versions** of the engineered system are produced.
Provides support for **Risk Handling**.

*[Image: General Spiral Model diagram showing iterative cycles through planning, risk analysis, engineering, and evaluation.]*

*[Image: Detailed Spiral Model diagram showing the four quadrants for each cycle.]*

*[Image: Another variation or detailed view of the Spiral Model.]*

### Each cycle in the spiral is divided into four parts:

**(A) Objective setting/Objectives determination and identify alternative solutions**
*   Requirements are gathered from the customers.
*   Objectives are identified, elaborated, and analyzed at the start of every phase.
*   Alternative solutions possible for the phase are proposed in this quadrant.
*   Each cycle in the spiral starts with the **identification of purpose** for that cycle, the **various alternatives** that are possible for achieving the **targets,** and the **constraints** that exists.
*   Estimating the cost, schedule and resources for the iteration.
*   Understanding the system requirements for continuous communication between the **system analyst and the customer**.
*   Examine the **risks** associated with these objectives.

**(B) Risk identification, assessment and reduction:**
*   The next phase in the cycle is to **calculate** these various alternatives based on the goals and constraints.
*   The focus of evaluation in this stage is located on the **risk perception** for the project.
*   A **detailed analysis is carried out** for each identified project risk.
*   **Identification of potential risk** is done while **risk mitigation strategy is planned and finalized.**
*   Steps are taken to reduce the risks. For example, if there is a risk that the requirements are inappropriate, a prototype system may be developed.
*   All the **possible solutions are evaluated** to select the best possible solution.
*   Then the **risks associated with that solution are identified.**
*   The **risks are resolved** using the best possible strategy.
*   At the end of this quadrant, the **Prototype is built** for the best possible solution.

**(C) Development and validation/Engineering/Develop next version of the Product:**
*   The next phase is to **Develop strategies that resolve uncertainties and risks**.
*   This process may include activities such as benchmarking, simulation, and **prototyping**.
*   **Develop** and validate the next level of the product after resolving the identified risks.
*   It includes testing, coding and deploying software at the customer site.
*   The identified features are developed and verified through testing.
*   At the end of the third quadrant, the next version of the software is available.

**(D) Review and plan for the next Phase/Evaluation:**
*   The **Customers evaluate the so far developed version** of the software.
*   In the end, **planning for the next phase** is started.
*   The **project is reviewed**, and a choice made whether to continue with a further period of the spiral.
*   If it is determined to keep, plans are drawn up for the next step of the project.
*   Also, includes identifying and monitoring risks such as schedule slippage and cost overrun.

*[Image: Simplified Spiral Model focusing on the review and planning for the next phase.]*

### Risk Handling in Spiral Model
A risk is any adverse situation that might affect the successful completion of a software project.
**The most important feature of the spiral model is handling these unknown risks after the project has started.**
Such risk resolutions are easier done by developing a prototype. The spiral model supports coping up with risks by providing the scope to build a prototype at every phase of the software development.

The **risk-driven feature** of the spiral model allows it to accommodate any mixture of:
*   a specification-oriented,
*   prototype-oriented,
*   simulation-oriented,
*   or another type of approach.

An essential element of the model is that **each period of the spiral is completed by a review** that includes all the products developed during that cycle, including plans for the next cycle.
The spiral model works for development as well as enhancement projects.

### Why is Spiral Model called Meta Model?
It subsumes all the other SDLC models.
For example:
*   A **single loop** spiral actually represents the **Iterative Waterfall Model.**
*   The spiral model incorporates the stepwise approach of the Classical Waterfall Model.
*   The spiral model uses the approach of the **Prototyping Model** by building a prototype at the start of each phase as a risk-handling technique.
*   Also, the spiral model can be considered as supporting the **Evolutionary model – the iterations along the spiral** can be considered as evolutionary levels through which the complete system is built.
*   Risk handling is inherently built into this model.
*   The spiral model is suitable for development of technically challenging software products that are prone to several kinds of risks.
*   However, this model is **much more complex** than the other models – this is **probably a factor deterring its use in ordinary projects**.

### When to use Spiral Model?
*   When **project is large**.
*   When **releases are required to be frequent**.
*   When **creation of a prototype is applicable**.
*   When **risk and costs evaluation is important**.
*   For **medium to high-risk projects**.
*   When **requirements are unclear and complex**.
*   When **changes may require at any time**.
*   When **long term project commitment is not feasible** due to changes in economic priorities.

### Advantages of Spiral Model:
*   **Risk Handling**: The projects with many unknown risks that occur as the development proceeds, in that case, Spiral Model is the best development model to follow due to the risk analysis and risk handling at every phase.
*   **Good for large projects**: It is recommended to use the Spiral Model in large and complex projects.
*   **Flexibility in Requirements**: Change requests in the Requirements at later phase can be incorporated accurately by using this model.
*   **Customer Satisfaction**: Customer can see the development of the product at the early phase of the software development and thus, they habituated with the system by using it before completion of the total product.
*   **Additional functionality or changes can be done at a later stage.**
*   **Cost estimation becomes easy** as the prototype building is done in small fragments.
*   **Continuous or repeated development** helps in risk management.
*   **Development is fast** and features are added in a systematic way in Spiral development.
*   There is always a **space for customer feedback**.

### Disadvantages of Spiral Model:
*   Risk of not meeting the schedule or budget.
*   Spiral may go on indefinitely.
*   Spiral development **works best for large projects only** also **demands risk assessment expertise**.
*   For its smooth operation **spiral model protocol needs to be followed strictly**.
*   **Documentation is more** as it has intermediate phases.
*   Spiral software development is **not advisable for smaller project,** it might cost them a lot.

---

## Software Life cycle models: Win-Win Spiral Model
The **Win-Win spiral model** add-on to the spiral model.

The **stages in this model are same as the stages in the spiral approach.**
The **only difference is that** there is a discussion and negotiations of the stakeholders’ win conditions on the requirements that need to be included in the current iteration of the software takes place between the development team and the customer at the time of the identifying the requirements.

### Why Win-Win Spiral Model?
The spiral model suggests a framework activity that addresses **customer communication to elicit project requirements from the customer.**
In an ideal context, the developer simply asks the customer what is required and the customer provides sufficient detail to proceed.
Unfortunately, this rarely happens.
In reality, the **customer and the developer enter into a process of negotiation,** where the customer may be asked to balance functionality, performance, and other product or system characteristics against cost and time to market.

The best negotiations strive for a **“win-win” result**.
That is:
*   **the customer wins by getting the system or product that satisfies the majority of the customer’s needs**
*   **the developer wins by working to realistic and achievable budgets and deadlines.**
Boehm’s WINWIN spiral model defines a set of negotiation activities at the beginning of each pass around the spiral.

Rather than a single customer communication activity, the following activities are defined:
1.  Identification of the system or subsystem’s key “**stakeholders.**”
2.  Determination of the stakeholders’ “**win conditions.**”
3.  **Negotiation of the stakeholders’ win conditions** to reconcile them into a set of win-win conditions for all concerned (including the software project team).

The WINWIN spiral model introduces **three process milestones, called anchor points**.
Anchor points help:
*   establish the **completion of one cycle around** the spiral and
*   **provide decision milestones** before the software project proceeds.
In essence, the anchor points **represent three different views of progress** as the project traverses the spiral.

### Win-Win Spiral Model Anchor points:
1.  **Life cycle objectives (LCO):**
    Defines a set of objectives for each major software engineering activity. For example, as part of LCO, a set of objectives establishes the definition of top-level system/product requirements.
2.  **Life cycle architecture (LCA):**
    Establishes objectives that must be met as the system and software architecture is defined. For example, as part of LCA, the software project team must demonstrate that it has evaluated the applicability of off-the-shelf and reusable software components and considered their impact on architectural decisions.
3.  **Initial operational capability (IOC):**
    Represents a set of objectives associated with the preparation of the software for installation/ distribution, site preparation prior to installation, and assistance required by all parties that will use or support the software.
![[Pasted image 20250604144239.png]]

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
# RAD Model
*Rapid Application Development Model (RAD)*

First proposed by IBM in 1980’s.
The critical feature of this model is the use of **powerful development tools and techniques.**
Software development process is based on **prototyping without any specific planning.**
There is **less attention paid to the planning and more priority is given to the development tasks.**
It targets at developing software in a short span of time.

It focuses on input-output source and destination of the information.
It emphasizes on delivering projects in small pieces; the larger projects are divided into a series of smaller projects.
The main features of RAD modeling are that it **focuses on the reuse of templates, tools, processes, and code.**

### SDLC RAD modeling has following phases:
*   Business Modeling
*   Data Modeling
*   Process Modeling
*   Application Generation
*   Testing and Turnover


![[Pasted image 20250604151954.png]]
### (A) Business Modeling
The business model for the product under development is designed on basis of the **flow of information and distribution between various business channels.**
The **information flow among business functions is defined by answering questions like** what data drives the business process, what data is generated, who generates it, where does the information go, who process it and so on.

### (B) Data Modeling
The information collected from business modeling is reviewed , refined and analyzed into a set of data objects that are significant for the business.
The attributes of all data sets is identified and defined.
The relation between these data objects are established and defined in detail in relevance to the business model.

### (C) Process Modeling
The data object sets that is declared in the data modeling phase is transformed to achieve the business information flow necessary to implement a business function and achieve specific business objectives as per the business model.
The **process model for any changes or enhancements to the data object sets is defined in this phase.**
Process descriptions for adding, deleting, retrieving or modifying a data object are given.

### (D) Application Generation
The **actual system is built and coding is done by using automation tools.**
Automated tools are used for the construction of the software, to convert process and data models into prototypes.
Even they use the **4th GL/5th GL techniques.**

### (E) Testing and Turnover
Many of the programming components have already been tested since RAD emphasis reuse. As prototypes are individually tested during every iteration, the overall testing time is reduced in RAD.
However, **the data flow and the interfaces between all the components need to be thoroughly tested with complete test coverage.** The new part must be tested, and all interfaces must be fully exercised.
Since most of the programming components have already been tested, it reduces the risk of any major issues.

### When to use RAD Methodology?
*   When a **system needs to be produced in a short span of time** (2-3 months).
*   When the **requirements are known**.
*   When the **user will be involved all through the life cycle**.
*   When **technical risk is less**.
*   When a **budget is high enough** to afford designers for modeling along with the cost of automated tools for code generation.

### Advantages of RAD Model:
*   This model is **flexible for change**.
*   Each **phase in RAD brings highest priority functionality** to the customer.
*   It **reduced development time.**
*   It increases the **reusability of features**.
*   It is useful when you have to **reduce the overall project risk.**
*   Due to code generators and code reuse, there is a **reduction of manual coding.**
*   Due to prototyping in nature, there is a **possibility of lesser defects.**

### Disadvantages of RAD Model:
*   It required **highly skilled designers**.
*   All application is not compatible with RAD.
*   For smaller projects, we cannot use the RAD model.
*   On the **high technical risk, it's not suitable**.
*   Required user involvement.
*   **Reduced scalability** occurs because a RAD developed application begins as a prototype and evolves into a finished application.
*   Progress and problems accustomed are hard to track as such there is **no documentation to demonstrate what has been done.**