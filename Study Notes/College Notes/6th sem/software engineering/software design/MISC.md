Software design is a **pivotal activity** within software engineering, serving as the technical core regardless of the chosen software process model. It commences after software requirements have been thoroughly analysed and modelled, setting the stage for subsequent code generation and testing. The essence of design lies in **creating a representation or model of the software**, which can be assessed for quality and refined prior to coding.

### Software Design Objectives

The overarching objective of software design is to **apply a set of principles, concepts, and practices that result in the development of a high-quality system or product**. The aim is to **create a software model that accurately implements all customer requirements and delights its users**. Designers must carefully evaluate various alternatives to arrive at the optimal solution for project stakeholders.

A well-crafted software design should fulfil the following criteria:

- **Implement all explicit requirements** outlined in the requirements model, while also accommodating any implicit requirements desired by stakeholders.
- Serve as a **clear, comprehensible guide** for those responsible for code generation, testing, and ongoing software support.
- Provide a **comprehensive overview of the software**, addressing its data, functional, and behavioural aspects from an implementation viewpoint.

**Software quality is fundamentally established during the design phase**. Critical quality attributes that must be considered from the outset of design include:

- **Functionality**: assessed by evaluating the program's feature set and capabilities, the generality of its functions, and its overall security.
- **Usability**: evaluated based on human factors, aesthetic appeal, consistency, and accompanying documentation.
- **Reliability**: measured by the frequency and severity of failures, accuracy of output, mean-time-to-failure (MTTF), and the system's ability to recover from failures.
- **Performance**: judged by processing speed, response time, resource consumption, throughput, and efficiency.
- **Supportability**: evaluated by the ease with which the program can be extended, errors corrected, and adapted to new environments.

### Design Concepts and Techniques

Software design involves a **hierarchical progression of technical work**, starting from broad framework activities and moving through specific actions to detailed tasks. It transitions from a "big picture" perspective to a more granular view, defining the intricate details necessary for implementation. The **design model consists of four primary elements**: data, architecture, components, and interface.

**1. Top-Down and Stepwise Refinement:**

- Early design approaches focused on techniques for **refining software structures in a top-down, "structured" manner**.
- **Stepwise refinement** is a core design concept. It is applied iteratively, for instance, in component-level design, where each software component is elaborated through successive iterations. This process involves defining an operation to ensure high cohesion (meaning the operation performs a single, specific function) and subsequently expanding its details.
- The **Cleanroom Strategy**, a formal software development approach, refines requirements through a "stepwise expansion of mathematical functions into structures of logical connectives and subfunctions" until they can be directly expressed in the programming language.

**2. Bottom-Up Techniques:**

- While not explicitly defined as a broad _design_ technique for overall system structure, the concept of **"bottom-up integration"** is a strategy employed during testing. This approach implies that individual low-level components are tested first and then progressively integrated upwards to form the complete software package.

**3. Team Design:**

- Software engineers are responsible for executing all design tasks. The success of software engineering is heavily reliant on **skilled and motivated individuals**.
- "People" constitute one of the four critical Ps (People, Product, Process, Project) that significantly influence software project management. It is crucial to **organise people into effective teams**, foster motivation for high-quality work, and ensure coordination for efficient communication. **Agile teams**, for example, are a recognised team structure.
- **Collaborative development** is essential, requiring all stakeholders to share information regarding business goals, system requirements, and architectural design issues. Design discussions and reviews are inherently collaborative activities.

**4. Modularity:**

- **Modularity** is a fundamental design concept. It provides a mechanism to implement the principle of "separation of concerns".
- **Effective modularity** dictates that each module (component) should concentrate solely on one well-defined aspect of the system.
- **Functional independence**, achieved through **high cohesion** and **low coupling**, is a key design concept linked to modularity. **Cohesion** reflects a module's "singleness of purpose," while **coupling** measures the interdependence between modules [236 (index), 122]. Designs exhibiting high cohesion and low coupling are generally more testable and maintainable.

**5. Functional Decomposition:**

- Functional decomposition is implied within the concept of problem decomposition, where product functions are broken down into their constituent parts.
- Within the generic design task set, this involves defining the functionality and behaviour for each major function and subsequently deriving a model that represents these functions and behaviours.
- The general principle of **refinement** (including stepwise refinement) supports functional decomposition, allowing designers to elaborate software from abstract concepts to lower levels of abstraction, detailing logical operations [7, 237 (index), 109].

**6. Data Flow Design:**

- Software design methods are **information-driven**, drawing from the data, functional, and behavioural domains established during analysis modelling.
- **Interface design** describes how the software communicates with other systems and human users, inherently involving a **flow of information** (e.g., data and/or control). Usage scenarios and behavioural models provide much of the necessary information for interface design.
- The **Data Design Element** is one of the four key elements of the design model. At the architectural level, it focuses on files or databases, while at the component level, it addresses the data structures required to implement local data objects.

**7. Data Structure Design:**

- The **design of data is considered as important as the design of processing functions**. Software design should always commence with a **consideration of data**, which forms the foundation for all other design elements.
- The **Data Design Element** specifically defines the major data structures necessary to implement the software [244 (index)].
- **Component-level design** provides a complete description of each software component's internal details, which includes defining **data structures for all local data objects** and the algorithmic details for all processing functions.

### User Interface Design

**User interface design (UI design)** is the process of creating an effective communication medium between a human user and a computer. It is a significant software engineering action, increasingly referred to as **usability design**.

Key aspects of UI design include:

- **Process**: It is an **iterative process** that is guided by predefined design principles.
- **Elements**: UI design involves identifying interface objects and actions, and then creating a screen layout that forms the basis for a user interface prototype. It incorporates:
    - **Aesthetic elements**: such as layout, colour, graphics, and interaction mechanisms.
    - **Ergonomic elements**: including information layout and placement, metaphors, and UI navigation.
    - **Technical elements**: such as UI patterns and reusable components.
- **Prototyping**: The interface design elements depict information flow into and out of the system and between components. A user interface prototype is a work product generated during this process.
- **Task Set**: Designing the user interface is a specific task within the generic design task set. It includes reviewing task analysis, specifying action sequences based on user scenarios, creating behavioural models of the interface, defining interface objects and control mechanisms, and conducting reviews for necessary revisions.
- **Metrics**: Metrics exist specifically for user interface design.
- **MobileApps**: For MobileApps, UI design must consider human, social, cultural, and organizational factors [NEW SOURCE]. Interface design for MobileApps also takes into account specific input mechanisms (e.g., touch, gesture, voice, virtual keyboard) and display characteristics (e.g., limited screen size, diverse displays) [576 (index)]. UI testing is also a component of MobileApp testing strategies.

### Object-Oriented Design

**Object-oriented design** represents a more contemporary approach to software design, forming a core concept within the discipline [238 (index)].

- It primarily focuses on the **elaboration of design classes** that originate from both the problem domain and the underlying infrastructure.
- In the context of component-based development, components can be conceived and designed as **object-oriented classes or collections of classes**.
- The **Unified Process (UP)**, described as a "use case driven, architecture-centric, iterative and incremental" software process, is structured as a framework for UML methods and tools, which frequently leverage object-oriented principles.
- **UML (Unified Modeling Language)**, detailed in Appendix 1, is a tool used to visualise, specify, construct, and document the artefacts of software-intensive systems. UML is deeply intertwined with object-oriented concepts.
- Specific metrics for object-oriented designs are available for quantitative analysis.

### Design Patterns and Implementation Strategies

**Design patterns** are a foundational concept in software design. They represent well-established, reusable solutions to recurring problems encountered during software design [233 (index)].

- **Pattern-based software design** is a distinct approach within software engineering practice. It encourages a way of "thinking in patterns".
- A **pattern-organising table** can be constructed to assist in pattern-based design.
- Patterns are employed in conjunction with architectural, component-level, and user interface design.
- Different categories of design patterns exist:
    - **Architectural patterns**: describe broad system categories, encompassing components, connectors, and constraints. These patterns facilitate the reuse of high-level design concepts.
    - **Component-level design patterns**: focus on the internal structure and behaviour of individual components [9, 360 (index), 122].
    - **User interface design patterns**: specifically applied in the design of user interfaces [9, 362 (index)].
    - **WebApp design patterns**: tailored for web application development [9, 364 (index)].
    - **Patterns for Mobile Apps**: also cater to the unique design challenges of mobile applications [9, 366 (index)].
- **Implementation Strategies**: While the sources do not detail a separate section on specific "implementation strategies" for patterns, they indicate that once a pattern is selected, it guides subsequent architectural, component-level, and interface design tasks. For instance, patterns can be effectively combined with refactoring and test-driven development to form a robust design approach. The "design tasks" for pattern-based design involve identifying and applying these patterns, which then inform the detailed design and construction activities. The complete design model, including its architectural, interface, and component-level elements, is influenced by the chosen patterns.