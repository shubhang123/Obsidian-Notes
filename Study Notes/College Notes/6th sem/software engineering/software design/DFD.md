# Data Flow Diagrams (DFDs)

## 1. Introduction to Data Flow Diagrams (DFDs)

A Data Flow Diagram (DFD) is a graphical representation of the "flow" of data through an information system. It models the system's processes, the data stores that hold information, and the external entities that interact with the system by providing or receiving data. DFDs are a core tool in structured analysis and design methodologies.

**Key Purpose:**
*   To illustrate how data is processed by a system in terms of inputs and outputs.
*   To show what the system does, not *how* it does it (i.e., it's a logical model, not a physical one).
*   To provide a clear and understandable view of system boundaries, processes, data storage, and external interactions.
*   To facilitate communication between analysts, designers, and users.

## 2. Components (Symbols/Notations) of a DFD

DFDs use a set of standardized symbols to represent system components. The two most common notation sets are Yourdon & Coad/DeMarco and Gane & Sarson. The concepts are similar, but the graphical symbols differ slightly.

| Component           | Yourdon & Coad / DeMarco Symbol | Gane & Sarson Symbol        | Description                                                                                                                               |
|---------------------|---------------------------------|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **Process**         | Circle (Bubble)                 | Rounded Rectangle (Lozenge) | Represents an activity or function that transforms input data flow(s) into output data flow(s). Named with a verb-noun phrase (e.g., "Process Payment"). |
| **Data Flow**       | Arrow                           | Arrow                       | Represents the movement of data between processes, data stores, and external entities. Named with a noun describing the data (e.g., "Payment Details"). |
| **Data Store**      | Two Parallel Lines / Open-ended Rectangle | Open-ended Rectangle        | Represents a repository where data is stored for later use (e.g., a file, database table, or manual record). Named with a plural noun (e.g., "Customers"). |
| **External Entity** (Terminator/Source/Sink) | Rectangle                       | Rectangle                   | Represents an external person, organization, or system that provides data to the system (source) or receives data from the system (sink). Named with a noun (e.g., "Customer", "Bank"). |

## 3. Types of Data Flow Diagrams (Levels of DFDs)

DFDs are typically drawn in a hierarchical manner, starting with a high-level overview and progressively decomposing into more detailed diagrams. This is known as "leveling" or "partitioning."

### 3.1. Level 0 DFD (Context Diagram)
*   **Purpose:** Provides the highest-level view of the entire system as a single process. It establishes the system's boundary and its interactions with the external environment.
*   **Characteristics:**
    *   Contains **only one process bubble** representing the entire system.
    *   Shows all major **external entities** that interact with the system.
    *   Shows all major **data flows** between the external entities and the system.
    *   **No data stores** are typically shown at this level, as they are considered internal to the system.
    *   It sets the scope of the system being modeled.
*   **Numbering:** The single process is usually numbered "0".

### 3.2. Level 1 DFD (Overview Diagram)
*   **Purpose:** Decomposes or "explodes" the single process from the Context Diagram (Level 0) into its major sub-processes.
*   **Characteristics:**
    *   Shows the primary functions or processes within the system.
    *   Shows data flows between these major processes.
    *   Introduces **major data stores** that are shared between these processes.
    *   Maintains the same external entities and external data flows as shown in the Level 0 DFD (this is called **balancing**).
*   **Numbering:** Processes are typically numbered 1.0, 2.0, 3.0, etc. (or simply 1, 2, 3).

### 3.3. Level 2 DFD (Detailed Diagram) and Lower Levels (Level n DFD)
*   **Purpose:** Further decomposes a specific process from a Level 1 DFD (or any higher-level DFD) into more detailed sub-processes.
*   **Characteristics:**
    *   Provides a more granular view of a particular part of the system.
    *   Shows data flows and data stores relevant to the decomposed process.
    *   Must **balance** with its parent process in the higher-level DFD. This means the inputs and outputs of the decomposed process in the Level 2 DFD must match the inputs and outputs of the parent process in the Level 1 DFD.
    *   Decomposition continues until processes are considered "primitive" – meaning they are simple enough to be described by a mini-specification (e.g., structured English, decision table, pseudocode) without further decomposition.
*   **Numbering:** If process 3.0 from Level 1 is decomposed, its sub-processes in Level 2 would be numbered 3.1, 3.2, 3.3, etc. If process 3.2 is further decomposed, its sub-processes would be 3.2.1, 3.2.2, etc.

### 3.4. Logical vs. Physical DFDs

*   **Logical DFD:**
    *   **Focus:** *What* the system does.
    *   Describes the business activities and data flows without specifying how they are implemented.
    *   Independent of technology (hardware, software, file organization).
    *   Uses business-oriented names for processes and data.
    *   Helps in understanding business requirements.
    *   Typically created during the analysis phase.

*   **Physical DFD:**
    *   **Focus:** *How* the system is implemented (or will be implemented).
    *   Describes the actual physical components, such as specific programs, files, databases, users, and devices.
    *   Includes details about implementation, such as file names, database table names, specific program names, and communication methods.
    *   Helps in system design and implementation.
    *   Typically derived from the logical DFD during the design phase.
    *   Physical DFDs may show:
        *   Manual processes vs. automated processes.
        *   Specific data storage media (e.g., "Customer Oracle Table" instead of just "Customers").
        *   Error handling processes and data flows.
        *   User interface screens as sources/sinks of data.

## 4. Characteristics and Rules for Drawing DFDs

### 4.1. General Characteristics:
*   **Hierarchical:** Can be decomposed into multiple levels of detail.
*   **Graphical:** Uses symbols for easy understanding.
*   **Non-procedural:** Shows data flow, not control flow or processing sequence (unlike flowcharts). Does not show decisions or loops explicitly within a single diagram (these are in mini-specs).
*   **Data-Centric:** Focuses on the movement and transformation of data.
*   **System Boundary:** Clearly defines what is part of the system and what is external.

### 4.2. Naming Conventions:
*   **Processes:** Use verb-noun phrases (e.g., "Calculate Tax," "Update Inventory"). Should be descriptive of the transformation.
*   **Data Flows:** Use nouns or noun phrases that describe the data being transported (e.g., "Customer Order," "Validated Invoice").
*   **Data Stores:** Use plural nouns that describe the collection of data (e.g., "Employees," "Products").
*   **External Entities:** Use nouns that describe the source or sink of data (e.g., "Customer," "Supplier," "Billing System").

### 4.3. Key Rules and Guidelines:
*   **Balancing:** Data flows entering and leaving a parent process bubble must be equivalent to the data flows entering and leaving the child DFD that decomposes that parent bubble. This ensures consistency across levels.
*   **Process Rules:**
    *   A process must have at least one input data flow and at least one output data flow. (No "black holes" - inputs only, or "miracles" - outputs only).
    *   Processes transform data; they don't just pass it through unchanged.
*   **Data Flow Rules:**
    *   A data flow must originate from or terminate at a process.
        *   Data cannot flow directly between two external entities.
        *   Data cannot flow directly between an external entity and a data store (it must go through a process).
        *   Data cannot flow directly between two data stores (it must go through a process).
    *   Data flows are one-way. Bi-directional flow should be represented by two separate arrows.
*   **Data Store Rules:**
    *   Data can only be moved to/from a data store by a process.
    *   A data store must have at least one input data flow (to populate it) and at least one output data flow (to use the data), though not necessarily on the same DFD level or at the same time.
*   **External Entity Rules:**
    *   External entities are outside the system boundary.
    *   Data flows must connect external entities to processes.
*   **Numbering:**
    *   Context Diagram process is "0".
    *   Level 1 processes are 1.0, 2.0, etc.
    *   Lower-level processes use a decimal extension of their parent process number (e.g., 2.1, 2.2 for children of 2.0).
*   **Clarity and Simplicity:**
    *   Avoid overly complex DFDs. A general guideline is 5-9 processes per diagram (the "magic number 7 +/- 2"). If more, consider further decomposition or grouping.
    *   Minimize crossing data flow lines.
    *   Ensure all symbols are clearly labeled.
*   **Iteration:** DFD creation is often an iterative process. Initial DFDs are refined as understanding of the system grows.

## 5. Advantages of DFDs
*   **Communication:** Simple graphical notation makes them easy to understand by both technical and non-technical stakeholders.
*   **System Understanding:** Helps in comprehending the scope, boundaries, and functions of a system.
*   **Analysis Tool:** Useful for identifying missing or redundant data flows, processes, or data stores.
*   **Documentation:** Serves as good documentation for the system's data processing logic.
*   **Basis for Design:** Logical DFDs form a foundation for creating physical DFDs and subsequently, system design.
*   **Modularity:** The leveled approach supports a top-down decomposition, making complex systems manageable.

## 6. Disadvantages/Limitations of DFDs
*   **No Control Information:** DFDs do not explicitly show control flow, decision logic, or sequencing of operations (this is typically detailed in process specifications or mini-specs).
*   **Timing:** DFDs do not inherently represent timing aspects of processes.
*   **Static View:** They represent a snapshot of data flow, not the dynamic behavior of the system over time.
*   **Physical Aspects:** Logical DFDs deliberately omit implementation details, which are necessary for actual construction.
*   **Can Become Complex:** For very large systems, even leveled DFDs can become numerous and intricate to manage without proper tools.
*   **Subjectivity:** The level of detail and decomposition can sometimes be subjective.

DFDs remain a valuable technique in system analysis, especially for understanding and modeling the functional aspects and data transformations within information systems.