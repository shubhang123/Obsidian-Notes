Here is a comprehensive response to your query, drawing on the provided sources:

### Feasibility Study

A **feasibility study** is a critical part of project planning that assesses whether software can be built to meet a defined scope. At the **project inception** stage, a **rough feasibility analysis** is conducted to help establish a business case for the idea. This involves defining goals, features, and functions for the first increment of development [NEW SOURCE]. For MobileApp development, developers must also consider human, social, cultural, and organisational factors that might impact the proposed MobileApp's business targets and functionality [NEW SOURCE]. Once the scope of a software project has been identified and agreed upon with the customer, it is then necessary to ask: **"Can we build software to meet this scope? Is the project feasible?"**.

### Informal and Formal Specifications

A **specification** in software engineering can take various forms, including a written document, a collection of graphical models, a formal mathematical model, a set of usage scenarios, a prototype, or any combination of these. The **formality and format of a specification vary with the size and complexity of the software to be built**.

#### Informal Specifications

For **smaller products or systems residing in well-understood technical environments, usage scenarios (such as use cases) may be sufficient** as a specification. In agile processes, requirements are frequently elicited through **informal representations like natural language descriptions, rough outlines, and sketches**. However, **requirements written using natural languages are often ambiguous or incomplete**. For large systems, a written document that combines natural language descriptions with graphical models might be the most suitable approach.

A **Software Requirements Specification (SRS)** is a work product created when a detailed description of all aspects of the software is needed before the project commences. While not always written, an SRS may be justified when software is developed by a third party, if a lack of specification could lead to severe business issues, or for extremely complex or business-critical systems. A typical SRS template includes sections for overall description, system features, external interface requirements (user, hardware, software, communications), and other non-functional requirements such as performance, safety, and security, along with appendices for a glossary, analysis models, and an issues list. A key concern during **requirements validation** is **consistency**, which can be ensured by using the analysis model.

#### Formal Specifications

**Formal methods are mathematically based techniques for describing system properties**. They offer frameworks for systematically specifying, developing, and verifying systems, moving away from ad hoc approaches. A **formal specification language** typically includes three main components:

- **Syntax**: Defines the specific notation used, often based on standard set theory notation and predicate calculus.
- **Semantic Domain**: Defines the "universe of objects" used to describe the system.
- **Relations**: A set of semantic rules that define how objects can be manipulated properly to satisfy the specification.

The use of a mathematically based specification language significantly increases the likelihood of achieving desired properties because its **formal syntax enables requirements or design to be interpreted in only one way, thereby eliminating ambiguity** common in natural language or graphical notations like UML. Formal methods use the descriptive capabilities of **set theory and logic notation to create clear statements of facts (requirements)**. This allows for **formal proof of correctness** to be applied to the requirements model, ensuring system conformance to its specification. Horizontal refinement of discrete models (elaborating software states from abstract to concrete) serves as the basis for enabling traceability of software requirements. Formal specifications for security requirements can also aid in creating test cases for model-based security testing.

The **Cleanroom Strategy**, a formal software development approach, refines requirements using a "stepwise expansion of mathematical functions into structures of logical connectives and subfunctions" until they can be directly stated in the programming language. During Cleanroom design, a **formal correctness verification** is performed at each refinement level by attaching generic correctness conditions to structured programming constructs. The act of modeling a system as a series of state transitions can itself uncover defects.

Despite these advantages, concerns about the applicability of formal methods in a business environment include:

- They are currently **time-consuming and expensive** to develop.
- **Extensive training is required**, as few software developers possess the necessary mathematical background.
- It is **difficult to use these models as a communication mechanism for technically unsophisticated customers**.
- They were devised for deterministic programs and may not fully account for programs designed to run forever, or the role of interrupt handlers in real-time systems.

Examples of formal specification languages include **OCL, Z, LARCH, and VDM**. The **Z language**, for instance, applies typed sets, relations, and functions within first-order predicate logic to build schemas that structure the formal specification.

### Pre/Post Conditions

Within formal methods, **preconditions** and **postconditions** are used to specify the state of a system. A **precondition describes what is known to be true before a specific action or use case is initiated**. For example, in a formal use case, the precondition describes the state of the system prior to the use case starting. **Postconditions** define the state of the system after an operation or function has completed. In Cleanroom software engineering, formal correctness verification involves checking that the postconditions of a function are met if its preconditions are satisfied.

### Algebraic Specification and Requirement Analysis Models

#### Algebraic Specification

While the term "algebraic specification" is not explicitly defined, the sources discuss the use of **mathematically based specification languages** that leverage "set theory and logic notation" to define system properties. The **Cleanroom Strategy** elaborates requirements using "stepwise expansion of mathematical functions into structures of logical connectives and subfunctions". Formal methods also involve **defining a "semantic domain" of objects and "relations" that dictate how these objects are properly manipulated to satisfy the specification**. The Z language, a formal specification language, specifically uses "typed sets, relations, and functions" to build schemas that structure the formal specification, where a schema describes the stored data a system accesses and alters (its "state").

#### Requirement Analysis Models

**Requirements models, also called analysis models**, are created to provide a **description of the required informational, functional, and behavioural domains for a computer-based system**. These models bridge the gap between a high-level system description (encompassing software, hardware, data, human, and other elements) and a detailed software design. The analysis model is a snapshot of requirements at any given time, evolving as more is learned about the system.

Requirements modeling approaches can include:

- **Scenario-based elements**: Describe the system from the user's point of view using basic and refined use cases, activity diagrams, and swimlane diagrams.
- **Class-based elements**: Define the objects manipulated by the system, their attributes, and relationships (e.g., class diagrams).
- **Behavioral elements**: Depict the system's states and classes, and the impact of events on these states, often using state diagrams and sequence diagrams.
- **Analysis patterns**: Reusable characteristics of a problem domain that reoccur across different applications, which can expedite model creation and increase the likelihood of applying sound design principles.
- **Content Model**: For Web and Mobile Apps, it models the information content, its structure, and relationships.
- **Functional Model**: Defines operations to manipulate content and other processing functions necessary for the end-user.
- **Interaction Model**: Describes how users interact with the application.
- **Navigation Model**: Defines the overall navigation strategy for the application.
- **Configuration Model**: Describes the environment and infrastructure where the app resides.

The inputs to requirements modeling are the information collected during communication, ranging from informal emails to detailed project briefs with usage scenarios. The output is a rigorous model providing detailed insight into the problem's structure and the shape of the solution. Models should focus on requirements visible within the problem or business domain, maintain a relatively high level of abstraction, and be kept as simple as possible.

Reviews of requirements models involve asking questions such as: "Are requirements stated clearly and unambiguously?" "Is the source of the requirement identified?" "Is each requirement bounded quantitatively?" "Do any requirements conflict with others?" "Is each requirement achievable and testable?". Metrics for requirements models focus on function, data, and behavior, aiming to provide quantitative insight into their specificity and completeness.

### Specification Design Tools

Various tools are used in software engineering to support the creation and analysis of specifications and designs:

- **UML Modeling Tools**: For building analysis and design models, including use cases, activity diagrams, class diagrams, state diagrams, and sequence diagrams. Examples include **UML Studio, Visio, and Visual UML**.
- **Formal Methods Tools**: These tools assist software teams in **specification and automating correctness proving**, often by defining a specialized language for theorem proving. Many are developed for research rather than commercial use.
- **Architectural Design Tools**:
    - **Architectural Description Languages (ADLs)**: Provide semantics and syntax for describing software architecture, enabling decomposition, composition, and representation of interfaces.
    - **Source Code Query Languages**: Can automate tasks like defining and checking architectural constraints.
    - **Reflexion Models (e.g., SAVE tool)**: Allow software engineers to build high-level architectural models and define relations between the model and source code, identifying missing or erroneous relations.
- **User Interface Prototype Tools**: Initial user interface prototypes, especially for mobile applications, can be created using informal methods like paper, sketches, index cards, or sticky notes to emulate interaction mechanisms, allowing assessment of layout and placement issues. Later prototypes may run on targeted mobile devices. During interface construction, a user interface tool kit may be used.
- **Requirements Management Tools**: Help identify, control, and track requirements and changes throughout the project life cycle.