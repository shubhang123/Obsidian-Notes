Here are comprehensive notes on unit testing, integration testing, and system testing, drawing upon the provided sources:

## Software Testing Strategy: An Overview

Software testing is a planned and systematic set of activities that aim to uncover errors in software. It is a critical component of **verification and validation (V&V)**, where verification asks, "Are we building the product right?" and validation asks, "Are we building the right product?". Testing should be conducted systematically to avoid wasting time, expending unnecessary effort, and allowing errors to go undetected.

A fundamental principle of software testing is to **begin "in the small" and progress toward "testing in the large"**. This means starting with individual components and gradually moving to integrated clusters and finally the entire system. An effective testing strategy ensures that errors surface as early as possible and progress is measurable. A **Test Specification** is a key work product that documents the testing approach, defining the overall strategy, specific steps, and types of tests.

The overall strategy for software testing can be viewed as a series of four sequential steps: **unit testing, integration testing, validation testing, and system testing**. Each step broadens the scope of testing. For large projects, testing may be conducted by an independent test group.

## Unit Testing

**Definition and Focus:**

- **Unit testing** focuses the verification effort on the smallest unit of software design, typically the **software component or module**.
- Its primary goal is to uncover errors within the boundary of an individual module by testing important control paths.
- The **unit test focuses on the internal processing logic and data structures** within a component's boundaries.
- This type of testing can be conducted in parallel for multiple components.

**Key Considerations and Tasks:**

- **Module interface testing**: Ensures that information properly flows into and out of the program unit.
- **Local data structures examination**: Verifies data integrity within temporary storage during algorithm execution.
- **Independent path exercising**: Guarantees that all statements in a module have been executed at least once.
- **Boundary conditions testing**: Ensures the module operates correctly at processing limits. Errors often occur at these boundaries.
- **Error-handling paths testing**: Crucial to ensure these paths function correctly if invoked.
- Common errors found during unit testing include erroneous computations, incorrect comparisons, or improper control flow.

**Unit Test Environment (Drivers and Stubs):**

- Since a component is typically not a stand-alone program, **driver and/or stub software** often needs to be developed for each unit test.
- A **driver** is a "main program" that accepts test-case data, passes it to the component being tested, and prints relevant results.
- **Stubs** replace modules that are called by the component under test but have not yet been implemented or integrated.
- Comprehensive unit testing may not always be possible due to resource limitations; in such cases, it's advised to select **critical modules and those with high cyclomatic complexity** for unit testing.

**Unit Testing in the Object-Oriented (OO) Context:**

- In OO software, the concept of a "unit" changes due to **encapsulation**.
- The smallest testable unit becomes the **encapsulated class**, rather than just an individual operation.
- Operations (methods) within a class are the smallest testable units, but they cannot be tested in isolation.
- Class testing is driven by the **operations encapsulated by the class and its state behavior**.
- If an operation is defined for a superclass and inherited by subclasses, it must be tested in the context of each subclass, as its usage may vary subtly.
- The design of unit tests can occur **before coding begins**. This approach, similar to Extreme Programming (XP), helps ensure that the code developed will pass the tests.
- XP teams develop a series of **unit tests to exercise each user story** before writing code. These unit tests are implemented using a framework for automation, supporting a **regression testing strategy**.

## Integration Testing

**Definition and Objective:**

- **Integration testing** is a systematic technique for **constructing the software architecture while simultaneously conducting tests to uncover errors associated with interfacing**.
- The objective is to take unit-tested components and build the program structure dictated by the design.
- It addresses problems such as data loss across interfaces, inadvertent adverse effects between components, subfunctions not producing desired major functions when combined, magnified imprecision, and issues with global data structures.

**Incremental vs. "Big Bang" Integration:**

- **"Big bang" integration** involves combining all components in advance and testing the entire program as a whole. This approach often leads to chaos, making error isolation and correction difficult.
- **Incremental integration** is the preferred approach, where the program is constructed and tested in small increments. This makes errors easier to isolate and correct, ensures interfaces are more completely tested, and allows for a systematic test approach.

**Types of Incremental Integration Strategies:**

1. **Top-Down Integration Testing:**
    
    - **Definition**: An incremental approach where modules are integrated by moving downward through the control hierarchy, starting with the main control module.
    - **Steps**:
        1. The main control module serves as a **test driver**, and **stubs** (replacements for subordinate components) are used for all directly subordinate components.
        2. Subordinate stubs are replaced one at a time with actual components (either depth-first or breadth-first).
        3. Tests are conducted as each component is integrated.
        4. Upon completion of each set of tests, another stub is replaced.
        5. **Regression testing** may be conducted to ensure no new errors have been introduced.
    - **Benefits**: Verifies major control or decision points early in the process. If depth-first integration is chosen, a complete function of the software can be implemented and demonstrated early, building confidence.
    - **Challenges**: Complex stubs may be required.
2. **Bottom-Up Integration Testing:**
    
    - **Definition**: Begins construction and testing with **atomic modules** (components at the lowest levels of the program structure).
    - **Steps**:
        1. Low-level components are combined into **clusters** (sometimes called builds) that perform a specific software subfunction.
        2. A **driver** (a control program) is written to coordinate test-case input and output for the cluster.
        3. The cluster is tested.
        4. Drivers are removed, and clusters are combined, moving upward in the program structure.
    - **Benefits**: Eliminates the need for complex stubs, as the functionality provided by subordinate components is always available. As integration moves upward, the need for separate test drivers lessens.
3. **Hybrid Integration:**
    
    - While not explicitly defined as "hybrid integration" in the sources, it is implied that a combined approach can be beneficial. For example, if the top two levels of the program structure are integrated top-down, and lower levels use bottom-up integration, the number of drivers can be substantially reduced, simplifying integration of clusters. This suggests that elements of both strategies can be combined.

**Important Integration Testing Concepts:**

- **Regression Testing**: Each time a new module is added or code is modified, the software changes, potentially introducing side effects. Regression testing involves re-executing a subset of tests to ensure that changes have not propagated unintended side effects or caused new errors. The **regression test suite** should include tests for all software functions, tests focusing on areas likely affected by changes, and tests for modified components.
- **Smoke Testing**: An integration testing approach commonly used for product software, designed as a pacing mechanism for time-critical projects.
    - **Activities**:
        1. Software components are integrated into a **build** (including data files, libraries, and reusable modules).
        2. Tests are designed to expose "show-stopper" errors that could significantly delay the project.
        3. The build is integrated with other builds and smoke tested daily.
    - **Benefits**: Provides a realistic assessment of integration progress, minimizes integration risk by uncovering incompatibilities early, and ensures stability for more thorough testing. It can be characterized as a rolling integration strategy.

**Integration Testing in the Object-Oriented (OO) Context:**

- Traditional top-down and bottom-up strategies have little meaning in OO software due to the lack of an obvious hierarchical control structure.
- Integrating operations one at a time into a class is often impossible due to direct and indirect interactions between components.
- Two main strategies exist for OO integration testing:
    1. **Thread-based testing**: Integrates the set of classes required to respond to one input or event for the system. Each thread is integrated and tested individually, with regression testing applied.
    2. **Use-based testing**: Begins system construction by testing **independent classes** (those that use very few, if any, server classes). After independent classes are tested, **dependent classes** (those that use independent classes) are tested in layers until the entire system is constructed.
- **Cluster testing** is a step in OO integration testing where a cluster of collaborating classes is exercised by designing test cases to uncover errors in their collaborations.
- **Drivers and stubs** are used differently in OO integration: Drivers can test lowest-level operations or whole groups of classes, and can replace user interfaces. Stubs are used when collaboration between classes is needed but one or more collaborating classes are not fully implemented.

## System Testing

**Definition and Purpose:**

- **System testing** occurs after software has been validated and incorporated into a larger system. It verifies that all system elements (e.g., software, hardware, people, databases) mesh properly and that overall system function and performance are achieved.
- System testing often falls outside the scope of software engineering and is not conducted solely by software engineers.

**Types of System Testing:**

- **Recovery Testing**: Verifies the system's ability to recover from failures and restart operations after a system crash.
- **Security Testing**: Verifies that built-in protection mechanisms for the system will, in fact, protect it from improper penetration and unauthorized access. This involves assessing potential vulnerabilities and attempting to exploit them.
- **Stress Testing**: Executes a system in a manner that demands resources in abnormal quantity, frequency, or volume to determine failure points. For WebApps, it assesses response time and reliability as demands on server-side resources increase.
- **Performance Testing**: Designed to test the run-time performance of software within the context of an integrated system. It assesses processing speed, data throughput, and response time, and occurs throughout all testing steps, but true performance is ascertained only after full system integration. Often coupled with stress testing.

**Special Considerations:**

- A common problem during system testing is "finger pointing," where different development teams blame each other for errors; this should be anticipated and mitigated.
- For **real-time systems**, a specific four-step strategy is proposed:
    1. **Task testing**: Each task is tested independently using conventional tests.
    2. **Behavioral testing**: Tests examine the behavior of the system as a consequence of events (e.g., user interrupts, mechanical interrupts, system interrupts, failure modes).
    3. **Intertask testing**: Focuses on time-related errors, testing asynchronous tasks with different data rates and processing loads to uncover synchronization errors or issues with message queues/data storage sizing.
    4. **System testing (Real-Time specific)**: Software and hardware are integrated, and tests are conducted to uncover errors at their interface, focusing on how interrupts are handled (priorities, processing).

## Other type of testing

# Regression Testing
**Regression testing** is a crucial software engineering activity focused on ensuring that **changes made to software do not introduce unintended side effects or new errors**. It involves the **re-execution of a subset of tests** that have already been conducted.

Here's a breakdown of regression testing based on the sources:

- **Purpose and Importance**
    
    - Its primary goal is to **ensure that changes (whether due to testing or other reasons) have not propagated unintended side effects**.
    - It helps to **ensure that new errors have not been introduced** into the software.
    - It is used to **check system behavior after changes are applied** to a software product.
    - The strategy is vital for **reducing "side effects"**.
- **When it is Conducted**
    
    - Regression testing may be performed **each time a new module is added** as part of integration testing.
    - It is recommended to run regression tests **every time a major change is made** to the software, including the integration of new components.
    - In agile development processes, such as those with daily build cycles, regression testing is **mandated** to prevent changes from producing unintended side effects.
    - For continuously evolving WebApps, testing, including regression tests, is an **ongoing activity**.
    - In Test-Driven Development (TDD), a **regression test suite** is run **with every change** to ensure that new code has not generated side effects in older code. When an error is found in TDD and the code is refactored (corrected), **all tests created to that point are re-executed**.
- **How it is Conducted**
    
    - Regression testing can be conducted **manually**, by re-executing a subset of all test cases.
    - **Automated capture/playback tools** can be used. These tools allow software engineers to capture test cases and their results for subsequent playback and comparison.
    - A **regression test suite** is formed by selecting a subset of tests to be executed. This suite typically includes three classes of test cases:
        - A **representative sample of tests** that will exercise all software functions.
        - **Additional tests that focus on software functions that are likely to be affected by the change**.
        - **Tests that focus on the software components that have been changed**.
    - As integration testing progresses, the number of regression tests can grow quite large. Therefore, the regression test suite should be designed to **include only those tests that address one or more classes of errors in each of the major program functions**.
- **Related Concepts**
    
    - Extreme Programming (XP) encourages a **regression testing strategy**.
    - The concept is directly linked to **Test-Driven Development (TDD)** as an iterative flow where tests are created before code, and all tests are rerun after any code change or correction.

# White-Box Testing

**White-box testing**, also known as **glass-box testing** or **structural testing**, is a test-case design philosophy that relies on the **internal logical structure** of the software to derive test cases. It is considered "testing in the small" and is typically applied to small program components, such as modules or small groups of modules.

**Purpose and Focus**:

- The primary goal is to derive test cases that **guarantee all independent paths within a module have been exercised at least once**.
- It ensures that **all logical decisions are exercised on their true and false sides**.
- It executes **all loops at their boundaries and within their operational bounds**.
- It **exercises internal data structures to ensure their validity**.
- It helps uncover errors due to erroneous computations, incorrect comparisons, or improper control flow.
- This type of testing can only be designed **after component-level design (or source code) exists**, as it requires knowledge of the program's logical details.
- It is generally **applied early in the testing process**.

**Techniques**:

- **Basis Path Testing**: A white-box technique that derives a logical complexity measure of a procedural design, using this measure to define a basis set of execution paths. Test cases from this method are guaranteed to execute every statement in the program at least once. **Cyclomatic complexity (V(G))** is a useful software metric derived from graph theory that defines the number of independent paths in the basis set, providing an upper bound for the number of tests needed to ensure all statements are executed.
- **Control Structure Testing**: This broadens testing coverage and improves white-box testing quality, including:
    - **Condition Testing**: Exercises the logical conditions contained within a program module.
    - **Data Flow Testing**: Selects program test paths based on the locations where variables are defined and used.
    - **Loop Testing**: Focuses exclusively on the validity of loop constructs. It categorises loops into simple, concatenated, nested, and unstructured types. Specific tests are applied for each type, such as covering no passes, one pass, two passes, m passes, and boundary passes (n-1, n, n+1) for simple loops. For nested loops, testing starts at the innermost loop with outer loops set to minimum values, then works outwards. Unstructured loops should ideally be redesigned for effective testing.

# Black-Box Testing

**Black-box testing**, also known as **behavioral testing** or **functional testing**, focuses on the **functional requirements of the software**. It takes an **external view** of the product, conducting tests at the software interface with little regard for the internal logical structure. It is a **complementary approach to white-box testing**, likely to uncover a different class of errors.

**Purpose and Focus**:

- It enables the derivation of **sets of input conditions that will fully exercise all functional requirements** for a program.
- It attempts to find errors in categories such as: **incorrect or missing functions, interface errors, errors in data structures or external database access, behavior or performance errors, and initialization and termination errors**.
- Unlike white-box testing, black-box testing tends to be **applied during later stages of testing**.
- It disregards the control structure and focuses on the **information domain** of the software.
- It aims to answer questions like how functional validity is tested, how system behavior and performance are tested, what classes of input make good test cases, and how sensitive the system is to certain input values.
- The goal is to design test cases that reduce the number of additional tests needed and provide insight into the presence or absence of classes of errors.
- It is considered "testing in the large".

**Techniques**:

- **Graph-Based Testing Methods**: Involves understanding objects and their relationships in the software and then defining tests to verify these relationships.
- **Equivalence Partitioning**: Divides the input domain of a program into **classes of data** from which test cases are derived. Guidelines include defining one valid and one invalid equivalence class for ranges, members of a set, or Boolean conditions.
- **Boundary Value Analysis (BVA)**: This technique **complements equivalence partitioning** by focusing on test cases at the **"edges" of an equivalence class**. It is based on the observation that a greater number of errors occur at the boundaries of the input domain. It derives test cases from both input and output domains, including values just above and below the specified boundaries.
- **Orthogonal Array Testing**: Applicable when the input domain is relatively small but too large for exhaustive testing. It is particularly useful for finding **"region faults"** and enables the design of test cases that provide **maximum test coverage with a reasonable number of test cases**. This method can detect and isolate all **single mode faults** and all **double mode faults**, and often many **multi-mode faults** as well.
- **Scenario-Based Test Design**: After unit and integration tests, this approach is used to determine if the software will perform in a manner that satisfies users. It aims to uncover errors associated with incorrect specifications and interactions among subsystems. In object-oriented systems, it dominates validation testing, making the **use case a primary driver** for these tests.

# **Stress testing** 
is a specialised software engineering activity designed to determine the **robustness of software by confronting programs with abnormal situations** [i]. The main goal is to understand **how a system fails when stressed beyond its operational limits**, rather than degrading gently or shutting down abruptly [i].

Key aspects include:

- **Purpose**: To find out at what point (users, transactions, data) performance becomes unacceptable, which components cause degradation, and how the system fails [i]. It also checks if transactions are lost or data integrity is affected when capacity is exceeded [i].
- **Methodology**: It involves **executing a system in a manner that demands resources in abnormal quantity, frequency, or volume** [i]. This can mean generating high interrupt rates, increasing input data rates significantly, or demanding maximum memory [i].
- **Relationship to other testing**: Stress testing is a **continuation of load testing**, pushing variables beyond normal operational limits, whereas load testing examines real-world loading within normal bounds [i]. Both are part of performance testing [i].
- **Specific applications**:
    - **WebApps**: Assesses response time and reliability as demands on server-side resource capacity increase [i].
    - **MobileApps**: Aims to find errors under extreme conditions unique to mobile, such as running multiple apps concurrently, processing many transactions, or storing excessively large data [i]. It also checks for graceful degradation without compromising security [i]. Ideally, it's performed "in the wild" on actual user devices [i].

