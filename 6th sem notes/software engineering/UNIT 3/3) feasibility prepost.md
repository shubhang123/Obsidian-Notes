
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