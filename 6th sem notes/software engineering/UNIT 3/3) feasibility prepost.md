
### Feasibility

After the **software scope** has been identified and agreed upon with the customer, it is crucial to determine if the project is **feasible**. Feasibility analysis assesses whether the software can be built to meet the defined scope. This includes evaluating several key factors:

- **Human Resources**: The planner evaluates the software scope to identify the necessary skills among human resources. The availability of these skills is a critical aspect of feasibility.
- **Reusable Software Components**: It is important to specify requirements for reusable software components early in the process. This allows for technical evaluation and timely acquisition, which impacts feasibility. The "make/buy" decision, which considers whether acquiring software (e.g., commercial off-the-shelf systems or COTS) is quicker or less costly than internal development, including customisation and external support, is a key aspect of determining feasibility .
- **Environmental Resources**: This refers to the hardware and software tools that will support the software project, also known as the software engineering environment (SEE). The availability of these resources for a specified time window must be established at the earliest practical time.

Defining technical feasibility is one of the tasks within concept development projects, which explore the potential for new technology. Ultimately, the negotiation of requirements also involves balancing functionality and performance against real-world constraints like time, people, and budget, ensuring a project plan that meets stakeholder needs and reflects feasibility. During requirements review, one of the questions asked is whether each requirement is **achievable in the technical environment** that will house the system or product.

### Specifications

A **specification** can take various forms in the context of computer-based systems and software. It might be any of the following, or a combination thereof:

- A **written document**.
- A set of **graphical models**.
- A **formal mathematical model**.
- A collection of **usage scenarios**.
- A **prototype**.

While some suggest using a "standard template" for specifications to ensure consistency and understandability, flexibility may be necessary depending on the project. For large systems, a written document combining natural language and graphical models may be ideal. However, for smaller products or those in well-understood technical environments, usage scenarios alone might suffice. The **formality and format of a specification vary with the size and complexity of the software to be built**.

The **Software Requirements Specification (SRS)** is a work product created when a detailed description of all aspects of the software is needed before the project begins. It's important to note that a formal SRS is **not always written**. However, it may be justified in specific circumstances:

- When software is to be developed by a **third party**.
- When a **lack of specification would create severe business issues**.
- When a system is **extremely complex or business critical**.

The requirements model, which includes scenario-based, class-based, and behavioral elements, feeds into the creation of design models. The requirements model (and the SRS) provides the means for both the developer and customer to assess the quality of the software once it's built. The requirements model is considered the first technical representation of a system, enabling engineers to better understand requirements and the design to achieve them.

**Formal specification languages** are distinct due to their precise nature. They are composed of three primary components:

1. A **syntax** that defines the specific notation.
2. A **semantic domain** to define a "universe of objects" used to describe the system.
3. A set of **relations** that define semantic rules for manipulating objects properly and satisfying the specification.

These languages, such as **OCL, Z, LARCH, and VDM**, allow for a clear statement of requirements, eliminating the ambiguity that often occurs with natural language or graphical notation. They model a system as a series of state transitions to represent what developers will observe as the program executes, which can help uncover defects. This aims to develop fault-free systems and ensure that requirements are interpreted unambiguously.

### Pre/Post Conditions

**Preconditions** and **postconditions** are key concepts, particularly in formal methods and design by contract.

- **Preconditions** are statements about **assumptions that must be verified before using a component or executing an operation**.
- **Postconditions** are statements about **guaranteed services a component will deliver, or the state of the system after an operation or action has been completed**.

These assertions are added to component specifications. They help developers understand what to expect from a component and how it behaves under certain conditions, making it easier to identify qualified components and fostering trust in their reuse. Design by contract specifically focuses on defining clear and verifiable component interface specifications through preconditions and postconditions.

OCL (Object Constraint Language) is a formal modeling language that can be used to express various constraints, including pre- and postconditions, guards, and other characteristics related to objects in UML models. Formal methods, by using concepts like data invariants, states, and operations with associated pre- and postconditions, aim to develop fault-free systems and ensure that requirements are interpreted unambiguously.

### Algebraic Specification (as part of Formal Methods)

While the sources do not explicitly use the term "algebraic specification" as a distinct heading, they extensively describe **formal specification languages** and **formal methods**, which inherently rely on mathematical and logical principles that encompass algebraic concepts.

**Key Characteristics of Formal Specification Languages:**

- **Precision and Unambiguity**: Unlike natural languages (e.g., English) or graphical notations (e.g., UML), formal specification languages allow requirements or design to be interpreted in only one way, thereby eliminating ambiguity.
- **Components of Formal Languages**: A formal specification language is typically composed of three primary components:
    1. A **syntax** that defines the specific notation used for representation.
    2. A **semantic domain** that defines a "universe of objects" used to describe the system.
    3. A set of **relations** that define the semantic rules for manipulating objects correctly and satisfying the specification.
- **Mathematical Basis**: The syntactic domain is often based on syntax derived from **standard set theory notation and predicate calculus**. The descriptive facilities of **set theory and logic notation** enable a clear statement of requirements. The sources also mention that formal methods model a system as a **series of state transitions** and that a black-box specification, which describes behavior, stimuli, and response, can use a mathematical function to transform inputs into outputs. The inclusion of "values of algebraic expressions" in a discussion of formal methods further highlights their mathematical and potentially algebraic nature.
- **Examples**: Representative formal specification languages mentioned include **OCL (Object Constraint Language), Z, LARCH, and VDM**. OCL, for instance, allows for the expression of constraints, pre- and postconditions, and guards related to objects in UML models. The Z language applies **typed sets, relations, and functions within the context of first-order predicate logic** to build schemas, which structure the formal specification.
- **Benefits**: Formal methods are used in an effort to develop fault-free systems and ensure that requirements are interpreted unambiguously. They can reduce rework over the project lifetime, offering a significant return on investment despite potentially slowing the delivery of the first software increment. For critical system components, formal correctness proofs can increase confidence that the system conforms to its specification.
- **Limitations**: Formal methods were primarily devised for deterministic programs. They may not fully account for hidden states when using abstract data types, potentially making assertions more complex than the code itself. They typically discourage expression side effects common in some application domains.

### Requirements Analysis Models

**Requirements models**, also referred to as **analysis models**, are the first technical representation of a system and are created to help software engineers better understand requirements and the design that will achieve those requirements. They primarily represent customer requirements by depicting the software across three domains: the **information domain, the functional domain, and the behavioral domain**.

**Overall Objectives and Philosophy of Requirements Modeling**:

- To **describe what the customer requires**.
- To **establish a basis for the creation of a software design**.
- To **define a set of requirements that can be validated once the software is built**.
- The analysis model acts as a **bridge between a system-level description and the software design**.

**Types of Requirements Analysis Models**: Requirements analysis can result in one or more of the following model types:

- **Scenario-based models**: These depict the system from the user's point of view, often using **use cases** (narratives or templates describing actor-system interactions). They can be supplemented by activity diagrams and swimlane diagrams.
- **Class-oriented models**: These represent **object-oriented classes**, including their attributes, operations (methods/services), relationships, and collaborations. UML is predominantly used for object-oriented analysis.
- **Behavioral and patterns-based models**: These depict how the software behaves in response to external "events". **State diagrams and sequence diagrams** are common notations for behavioral modeling. Analysis patterns (reoccurring characteristics in a problem domain) can be integrated into these models to facilitate problem-solving and transformation into design models.
- **Data models**: These describe the information domain for the problem.
- **Flow-oriented models**: These represent the system's functional elements and how they transform data as it moves through the system.

**Relationship to Design Models**: The requirements model (analysis model) provides necessary information for creating the four design models: **data/class design, architectural design, interface design, and component-level design**. Elements of the requirements model are directly traceable to parts of the design model.

### Connection between Algebraic Specification (Formal Methods) and Requirements Analysis Models

Formal methods provide a rigorous approach to defining and verifying requirements, which can be applied to the artifacts created during requirements analysis.

- **Validation and Verification**: Formal methods, through their use of formal specification languages, enable the application of **formal proof of correctness to the requirements model**. This can help assess the quality of the analysis model and uncover defects that arise from ambiguous or incomplete requirements written in natural language. Verification begins with high-level specifications and moves towards design detail, ensuring conformance.
- **Consistency and Quality Assessment**: During requirements validation, the specification is assessed for consistency, omissions, and errors. The analysis model can be used to ensure that requirements are consistently stated. The ability of formal methods to ensure that requirements are interpreted in only one way significantly aids in this consistency check.
- **Security Modeling**: Formal methods can augment the security analysis and verification of systems by using formal specifications for security requirements, which can assist in creating test cases for model-based security testing. Security models are formal descriptions of software system security policy that capture key security requirements and rules for enforcement.
- **Box Structure Specification**: The Cleanroom software engineering approach uses a **box structure specification method**. This method involves refining black boxes (specifying behavior as a function mapping stimuli to responses, potentially mathematically) into state boxes and then clear boxes, with correctness verification occurring at each refinement step. This hierarchical partitioning and rigorous verification are aligned with the principles of formal methods applied to requirements.

In essence, while requirements analysis models (scenario, class, behavioral) describe _what_ the system should do, formal methods, including those with an algebraic foundation, offer a powerful, verifiable mathematical notation to state these requirements precisely and rigorously, ensuring correctness and reducing ambiguity before proceeding to design and construction.