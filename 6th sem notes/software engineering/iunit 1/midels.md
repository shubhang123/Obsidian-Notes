# Software Development Process Models or Software Life cycle models

---


## Software Life cycle models: The Waterfall Model
*The First SDLC Methodology - The Waterfall Method - 1970s to 90s*

*   **Oldest** and most **straightforward**.
*   Also referred to as a **linear-sequential life cycle model**.
*   Very **simple** to understand and use.
*   Each phase must be completed fully before the next phase can begin.
*   Basically, used for the **project** which is **small** and there are **no uncertain requirements**.
*   Phases **do not overlap**.
*   At the end of each phase, a review takes place to determine:
    *   if the project is on the right path and
    *   whether or not to continue or discard the project.

### Waterfall Model Phases
Waterfall is **broken down into phases**, and other modern methodologies can even pull from these phases and utilize them, these phases are:
*   Requirement Analysis
*   System Design
*   Implementation
*   Testing
*   Deployment
*   Maintenance

*[Image: Diagram of the Waterfall Model showing sequential phases]*

After the entire architecture, data structures, and functional designs are ready, the development team starts coding the software. Only after all code is written can integration and validation start.
This means that the **code is not tested before the Testing phase and only unit tests are executed during development.**

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

### Advantages of waterfall model:
*   This **model** is simple and easy to understand and use.
*   It is **easy to manage** due to the rigidity of the model – each phase has specific deliverables and a review process.
*   In this model phases are processed and completed one at a time.
*   Phases **do not overlap**.
*   Waterfall model **works well for smaller projects** where requirements are very well understood.

### Disadvantages of waterfall model:
*   **Not suitable for the projects where requirements are at a moderate to high risk of changing**.
*   Due to the lack of feedback from customers or other stakeholders during the design and development process, it was quite common for Waterfall teams to **build unnecessary or under-used features**, leading to **wasted time, effort, and money**.
*   Once an application is in the **testing** stage, it is **very difficult to go back and change** something that was not well-thought out in the concept stage.
*   **No working software is produced until late** during the life cycle.
*   **High amounts of risk and uncertainty**.
*   **Not a good model for complex and object-oriented projects**. Poor model for long and ongoing projects.

---

## Software Life cycle models: Iterative Waterfall Model
Feedback paths are provided for error correction as & when detected later in a phase.
Though errors are inevitable, but it is desirable to detect them in the same phase in which they occur. If so, this can reduce the effort to correct the bug.

*[Image: Diagram of Iterative Waterfall Model showing feedback loops]*

---

## Software Life cycle models: Iterative Model

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

---

## Software Life cycle models: Incremental Model

*[Image: Diagram illustrating the Incremental Model concept]*

*   The **most adopted** models of software development process.
*   The software requirement is broken down into many standalone modules in the software development life cycle.
*   Once the **modules are split** then **incremental development will be carried out in steps** covering all the analysis, designing, implementation, carrying out all the required testing or verification and maintenance.

*[Image: Detailed diagram of the Incremental Model showing increments being built and integrated]*

In incremental models, each iteration stage is developed and hence each stage will be going through requirements, design, coding and finally the testing modules of the software development life cycle.
Functionality developed in each stage will be added on the previously developed functionality and this repeats until the software is fully developed.
Every subsequent release of the module adds function to the previous release. The process continues until the complete system achieved.
At each incremental stage there will be **thorough review based on which the decision on the next stage will be taken out.**

---

## Software Life cycle models: Iterative Incremental model

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

## Software Life cycle models: The Prototyping Model

The **Prototype method revolves around the creation of a low fidelity (reliability) prototype** for the purposes of collecting **early feedback from prospective users**. From there, prototypes are evolved into final software requirements.

The prototype model requires that before carrying out the development of actual software, a working prototype of the system should be built.
A prototype is a **toy implementation of the system**.
A prototype usually turns out to be a **very crude version** of the actual system, possible exhibiting **limited functional capabilities, low reliability, and inefficient performance** as compared to actual software.

In many instances, the client only has a general view of what is expected from the software product. In such a scenario where there is an **absence of detailed information regarding the input to the system, the processing needs, and the output requirement, the prototyping model may be employed.**

*[Image: Diagram of the Prototyping Model showing the iterative prototype development and refinement process]*

### Steps of Prototype Model
1.  Requirement Gathering and Analyst
2.  Quick Decision
3.  Build a Prototype
4.  Assessment or User Evaluation
5.  Prototype Refinement
6.  Engineer Product

### Advantage of Prototype Model
*   Reduce the risk of incorrect user requirement
*   Good where **requirement are changing/uncommitted**
*   Regular visible process aids management
*   Support **early product marketing**
*   Reduce Maintenance cost.
*   Errors can be detected much earlier as the system is made side by side.

### When to use Prototype Model
*   Prototype model should be used when the desired system needs to have a **lot of interaction with the end users**.
*   Typically, **online systems, web interfaces** have a very high amount of interaction with end users, are best suited for Prototype model. It might take a while for a system to be built that allows ease of use and needs minimal training for the end user.
*   Prototyping ensures that the **end users constantly work with the system and provide a feedback** which is incorporated in the prototype to result in a useable system. They are excellent for designing good human computer interface systems.

### Advantages of Prototype Model (Additional)
*   Users are actively involved in the development.
*   Since in this methodology a **working model** of the system is provided, the users get a **better understanding of the system being developed.**
*   **Errors** can be detected much **earlier.**
*   **Quicker user feedback** is available leading to better solutions.
*   Missing functionality can be identified easily.
*   Confusing or difficult functions can be identified in each and every iteration.
*   Requirement validation, Quick implementation of incomplete but functional and application model.

### Disadvantage of Prototype Model
*   An **unstable/badly implemented prototype** often becomes the final product.
*   Leads to **implementing and then repairing** way of building systems.
*   Require **extensive customer involvement**.
*   Costs customer money.
*   Needs **committed customer**.
*   Difficult to finish if customer withdraws.
*   May be too customer specific.
*   Difficult to know **how long the project will last**.
*   Prototyping tools are **expensive**.
*   **Special tools & techniques** are required to build a prototype.
*   It is a **time-consuming** process.

---

## Software Life cycle models: Evolutionary Process Model
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

---

## Software Life cycle models: The spiral model
*Risk-driven software development process model.*

### Spiral Model (Boehm)
Initially proposed by Boehm,
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

---

## Software Life cycle models: RAD Model
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

*[Image: Diagram of the RAD Model showing its phases: Business Modeling, Data Modeling, Process Modeling, Application Generation, Testing & Turnover.]*

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

---

## Software Life cycle models: RUP Model (Rational Unified Process) Model

### Unified Process
Unified process (UP) is an:
*   **architecture-centric,**
*   **use-case driven,**
*   **iterative and incremental**
development process that **leverages** unified modeling language and is **compliant with the system process engineering metamodel.**

Unified process can be **applied to different software systems** with **different levels of technical and managerial complexity** across **various domains and organizational cultures**.
UP is also referred to as the unified software development process.
UP has the following major characteristics:
*   It is use-case driven
*   It is architecture-centric
*   It is risk focused
*   It is iterative and incremental

### RUP Model
Stands for **"Rational Unified Process."**
*   An agile software development method.
*   Created by Rational corporation and is designed and documented using UML (Unified Modeling Language).
*   Software development process from Rational, a division of IBM.
*   It **divides the development process into four distinct phases** that each involve business modeling, analysis and design, implementation, testing, and deployment.

The Rational Unified Process (RUP) is **Iterative and Agile**.
*   Iterative, meaning repeating. Iterative because all the process’s core activities repeat throughout the project.
*   The process is agile because various components can be adjusted, and phases of the cycle can be repeated until the software meets requirements and objectives.

The process should be looked at from **two dimensions**.
*   Firstly, there is the **time dimension**, represented by the horizontal axis. The time dimension is **expressed in terms of the phases and cycles, iterations, and milestones.**
*   The **vertical axis is the process dimension**. This dimension represents the static aspect of the process and is **described in terms of activities, artefacts, workers, and workflow.**

*[Image: Diagram of the RUP Model showing phases (horizontal) and disciplines/workflows (vertical). Phases: Inception, Elaboration, Construction, Transition. Workflows: Business Modeling, Requirements, Analysis & Design, Implementation, Test, Deployment, etc.]*

### Rational Unified Process: time dimension
The **time dimension means the dynamic organisation from the process over time.**
The **software’s life cycle is itself divided further into cycles.** Each cycle corresponds to, for example, a period in which a new generation of a product is being worked on.
Each phase is finalized with a milestone.
A milestone is a **point in time where decisions of critical importance must to be made.**

The **Rational Unified Process (RUP) divides development into the four consecutive phases:**
*   Inception phase
*   Elaboration phase
*   Construction phase
*   Transition phase

### RUP Phases Overview
*   **Phase 1: Inception**
    “Inception - The idea for the project is stated. The development team determines if the project is worth pursuing and what resources will be needed.”
*   **Phase 2: Elaboration**
    “ Elaboration - The project's architecture and required resources are further evaluated. Developers consider possible applications of the software and costs associated with the development.”
*   **Phase 3: Construction**
    “Construction - The project is developed and completed. The software is designed, written, and tested.”
*   **Phase 4: Transition**
    “Transition - The software is released to the public. Final adjustments or updates are made based on feedback from end users.”

### Phase 1: Inception
Depending on the project, the result of the first phase could be:
*   A vision statement
*   First use case (20% completed)
*   Market research results
*   Financial prognosis
*   Risk assessment
*   Project plan
*   Corporate or business model
*   Prototypes

The results should then be assessed according to several criteria:
*   Were all interested parties included and do they all agree?
*   Are the requirements of the development reliable?
*   Are the costs credible? What are the priorities and risks?

### Phase 2: Elaboration
“Elaboration - The project's architecture and required resources are further evaluated. Developers consider possible applications of the software and costs associated with the development.”
During the elaboration phase, the system’s requirements and its required architecture are assessed and analysed.
This is where the project begins to take shape.
The objective of the elaboration phase is to analyse products and to lay a foundation for the future architecture.

Results of the elaboration phase include:
*   Use case (80% completed)
*   Description of the feasible architecture
*   Project development plan
*   Prototypes for tackling risks
*   User manual

Criteria for the results:
*   Is the architecture stable?
*   Are important risks being tackled?
*   Is the development plan sufficiently detailed and accurate?
*   Do all interested parties agree on the current design?
*   Are the expenditures acceptable?

### Phase 3: Construction
“Construction - The project is developed and completed. The software is designed, written, and tested.”
Here the software system is constructed in its entirety.
The majority of coding also takes place in this phase.
In this production process, the emphasis is on managing costs and means, as well as ensuring quality.

Results from the production phase include:
*   Fully completed software system
*   User manual

To be assessed according to:
*   Is the product stable and complete enough for use?
*   Are all interested parties/users ready for the transition into the product’s usage?
*   Are all the expenditures and means still in good order?

### Phase 4: Transition
“Transition - The software is released to the public. Final adjustments or updates are made based on feedback from end users.”
The objective of the transition phase is to transfer the product to its new user.
As soon as the user starts using the system, problems almost always arise that require changes to be made to the system.
The goal, however, is to ensure a positive and smooth transition to the user.

Results and activities in the last phase:
*   Beta testing
*   Conversion of existing user databases
*   Training new users
*   Rolling out of the project to marketing and distribution
Input from the new users should guide the assessment here.

### Advantages of RUP Model
*   It allows us to deal with changing requirements within the project’s development life cycle as per the client or customer needs, i.e. it welcomes change.
*   It supports incremental build the software product.
*   It provides proper documentation of the software product.
*   It helps to use the resources efficiently.
*   It helps to identify issues early in the process life cycle.
*   It improves process control and risk management.
*   It enhances team productivity.
*   It helps reduces unexpected development costs.

### Disadvantages of RUP Model
*   It is a complex model to implement as it has multiple stages of the workflow.
*   It is challenging for organizations to implement which has, small team size or projects.
*   It should be highly result-oriented from individuals or teams.
*   It emphasizes the integration of modules throughout the software development process, so this creates trouble during the testing phase.

---

## The V-model
*Verification and Validation model.*
Process executes in a sequential manner in V-shape.

It is based on the **association of a testing phase for each corresponding development stage**.
It follows a **sequential design process same as the waterfall model.**
Testing of the device is planned in parallel with a corresponding stage of development.
The next phase starts only after completion of the previous phase i.e. for each development activity, there is a testing activity corresponding to it.

*[Image: Diagram of the V-Model, showing development phases on the left descending arm (Requirements, High-Level Design, Low-Level Design, Coding) and testing phases on the right ascending arm (Unit Testing, Integration Testing, System Testing, Acceptance Testing), with arrows connecting corresponding phases.]*

The left side of the model is Software Development Life Cycle – **SDLC**
The right side of the model is Software Test Life Cycle – **STLC**
The entire figure looks like a V, hence the name V – model.

**SDLC:** SDLC is Software Development Life Cycle. It is the sequence of activities carried out by Developers to design and develop high-quality software.
**STLC:** STLC is Software Testing Life Cycle. It consists of a series of activities carried out by Testers methodologically to test your software product.

*[Image: V-Model diagram emphasizing Verification on the left (design phases) and Validation on the right (testing phases).]*

### Verification:
It involves a **static analysis method (review)** done without executing code.
This evaluation procedure is carried out at the time of development to check whether specific requirements will meet or not.

### Validation:
It involves **dynamic analysis method (functional, non-functional),** testing is done by executing code.
Validation is the process to classify the software after the completion of the development process to determine whether the software meets the customer expectations and requirements.

### When to use V-Model?
*   When the **requirement is well defined** and not ambiguous.
*   The V-shaped model should be used for **small to medium-sized projects** where requirements are clearly defined and fixed.
*   The V-shaped model should be chosen when **sample technical resources are available** with **essential technical expertise**.

### Advantage (Pros) of V-Model:
*   Easy to Understand.
*   Testing Methods like planning, test designing happens well before coding.
*   This saves a lot of time. Hence a higher chance of success over the waterfall model.
*   Avoids the downward flow of the defects.
*   Works well for small plans where requirements are easily understood.

### Disadvantage (Cons) of V-Model:
*   Very rigid and least flexible.
*   Not a good for a complex project.
*   Software is developed during the implementation stage, so no early prototypes of the software are produced.
*   If any changes happen in the midway, then the test documents along with the required documents, has to be updated.
*   High risk and uncertainty.
*   It is not suitable for projects where requirements are not clear and contains high risk of changing.
*   This model does not support iteration of phases.
*   It does not easily handle concurrent events.

---

## Software Life cycle models: The New Millennium: Agile Takes Over
*(Also part of Unit 5)*
Combination of iterative and incremental process models with focus on **process adaptability and customer satisfaction** by rapid delivery of working software product.

With no single methodology presenting a suitable alternative to Waterfall, which was woefully too slow and risky, 17 pioneers in software engineering gathered to create the **Agile “Software Development” Manifesto on February 11th, 2001.**
[https://agilemanifesto.org/history.html](https://agilemanifesto.org/history.html)

*[Image: The Agile Manifesto logo or a graphic representing its core values.]*

**Agile** is the mainstream methodology used in **modern software development,** and **expands its influence beyond coding into many aspects of product development, from ideation to customer experience.**

The Agile methodology breaks a project down into multiple cycles, each passing through some or all of the SDLC phases.
The **focus is on people and how they work together to get the project done.**
Agile calls for **continuous collaboration between team members and stakeholders with regular cycles of feedback and iteration.**

The Agile model was primarily designed to help a project to adapt to change requests quickly. Thus, it facilitate **quick project completion.**
To accomplish this task agility is required.
**Agility** is achieved by:
*   **fitting the process to the project,**
*   **removing activities that may not be essential for a specific project.**
Also, anything that is wastage of time and effort is avoided.

*[Image: A diagram illustrating the iterative and incremental nature of Agile development, possibly showing sprints or iterations.]*

### Agile Methods
*   Break the product into small incremental builds.
*   These builds are provided in iterations.
*   Each iteration typically lasts from about one to three weeks.

Each incremental part is developed over an iteration.
Each iteration is intended to be small and easily manageable and that can be completed within a couple of weeks only.
At a time one iteration is planned, developed and deployed to the customers.
Long-term plans are not made.

Every iteration involves cross functional teams working simultaneously on various areas like:
*   Planning
*   Requirements Analysis
*   Design
*   Coding
*   Unit Testing and
*   Acceptance Testing.
At the end of the iteration, a working product is displayed to the customer and important stakeholders.

### The Agile Manifesto’s 4 Core Values

*[Image: A visual representation of the 4 Core Values of the Agile Manifesto.]*

1.  **Individuals and interactions** over processes and tools
2.  **Working software** over comprehensive documentation
3.  **Customer collaboration** over contract negotiation
4.  **Responding to change** over following a plan

#### 1) Individuals and interactions over processes and tools
In Agile development, self-organization and motivation are important, as are interactions like co-location and pair programming.

#### 2) Working software over comprehensive documentation
Demo working software is considered the best means of communication with the customers to understand their requirements, instead of just depending on documentation.

#### 3) Customer collaboration over contract negotiation
As the requirements cannot be gathered completely in the beginning of the project due to various factors, continuous customer interaction is very important to get proper product requirements.

#### 4) Responding to change over following a plan
Agile Development is focused on **quick responses to change and continuous development.**

### Advantages of Agile Methodology
*   Deliver software **well-tailored to an ever-growing understanding of customer demands.**
*   Software is **deployed more quickly** and **improved more regularly.**
*   **Better code hygiene** including style, readability, and structuring.
*   **Flexible and adaptable process** enables pivots or changes mid-project.
*   Doesn’t require a complete list of requirements upfront.
*   Makes room to act on organizational learning as the project progresses.
*   **Transparency and continuous communication** with involved stakeholders.