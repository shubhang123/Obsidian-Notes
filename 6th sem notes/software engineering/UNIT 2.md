# Unit II: Software Metrics, Estimation, and Tracking (Detailed Concepts)

## 1. Measures, Metrics, and Indicators

### 1.1. Core Definitions and Distinctions

*   **Measure:**
    *   A fundamental concept involving the direct quantification of a specific attribute of a software product, process, or resource.
    *   It provides a single, objective data point representing the magnitude or dimension of the attribute.
    *   Examples: Number of lines of code written, number of test cases executed, CPU execution time for a function.
    *   Characteristics: Typically objective, directly observable or countable.

*   **Metric:**
    *   A more derived and often more insightful quantification that relates one or more measures, or a measure to a standard or baseline.
    *   It aims to provide a degree to which a system, component, or process possesses a given attribute, offering context to raw measures.
    *   Metrics are often used for comparison, trend analysis, and decision-making.
    *   Examples: Defect density (defects/KLOC), test coverage (lines covered/total lines), requirements volatility (changed requirements/total requirements).
    *   Characteristics: Often calculated, comparative, provides a scale or degree.

*   **Indicator:**
    *   A metric, or a combination of metrics, that provides a signal or insight into the state, performance, or quality of a software process, project, or product.
    *   Indicators help in identifying potential problems, opportunities for improvement, or the achievement of goals. They act as diagnostic tools.
    *   Examples: A consistently increasing defect density trend might *indicate* a decline in code quality or review effectiveness. A high schedule variance *indicates* the project is behind schedule.
    *   Characteristics: Interpretive, provides actionable insight, often used for monitoring and control.

### 1.2. Role and Importance in Software Engineering
Effective measurement through measures, metrics, and indicators is crucial for:
*   **Understanding:** Gaining objective insights into current processes, products, and project status.
*   **Control:** Monitoring performance against plans and taking corrective actions when deviations occur.
*   **Prediction:** Forecasting future outcomes, such as project completion time, cost, or potential defects.
*   **Improvement:** Identifying areas of weakness in processes or products and guiding improvement efforts based on data.
*   **Communication:** Providing a common, objective language for discussing project status and quality with stakeholders.
*   **Decision Making:** Supporting informed decisions based on quantitative evidence rather than intuition alone.

## 2. Metrics in the Process and Project Domains

### 2.1. Process Metrics

Process metrics are concerned with the effectiveness and efficiency of the software development process itself. They are typically collected across multiple projects over extended periods to identify long-term trends and facilitate continuous process improvement (CPI).

#### Key Characteristics of Process Metrics:
*   **Strategic Focus:** Aimed at improving the overall capability of the organization to produce quality software.
*   **Long-Term Collection:** Data is aggregated over time and across projects.
*   **Baseline Establishment:** Used to establish baselines for performance and quality.
*   **Examples (Conceptual):**
    *   **Cost of Quality (CoQ):**
        *   **Definition:** A framework for quantifying the total cost associated with achieving (or not achieving) product quality. It encompasses all efforts to prevent, find, and correct defects.
        *   **Components:**
            *   **Prevention Costs:** Investments made to prevent defects from occurring in the first place (e.g., quality planning, training, formal technical reviews, tool acquisition).
            *   **Appraisal Costs:** Costs incurred to determine the degree of conformance to quality requirements (e.g., inspections, testing, equipment calibration, audits).
            *   **Failure Costs:** Costs resulting from products or services not conforming to requirements.
                *   **Internal Failure Costs:** Defects found *before* delivery to the customer (e.g., rework, scrap, re-testing, failure analysis).
                *   **External Failure Costs:** Defects found *after* delivery to the customer (e.g., warranty claims, product returns, complaint handling, liability costs, loss of goodwill).
    *   **Cost of Poor Quality (CoPQ):**
        *   **Definition:** Specifically focuses on the costs incurred due to failures (both internal and external) and the cost of appraisal activities needed to detect these failures. It represents the financial impact of not getting things right the first time.
        *   Often seen as a subset of CoQ, highlighting the "waste" in a process.
    *   **Defect Density:**
        *   **Definition:** A measure of the number of defects identified in a software component or system, normalized by its size (e.g., KLOC or Function Points).
        *   Used to compare the quality of different modules or projects, or to track quality trends over time for a process.
    *   **Review Efficiency:**
        *   **Definition:** The effectiveness of formal review processes (like inspections or walkthroughs) in detecting defects before they move to later stages (e.g., testing or deployment).
        *   Typically calculated as the percentage of defects found during reviews out of the total defects found internally up to a certain point.
    *   **Testing Efficiency:**
        *   **Definition:** The effectiveness of the testing process in identifying defects.
        *   Can be measured by comparing defects found during internal testing phases versus those found later (e.g., in acceptance testing or by the customer).
    *   **Defect Removal Efficiency (DRE):**
        *   **Definition:** A measure of the percentage of defects that have been removed from the software product prior to its delivery to the end-user.
        *   Calculated for specific phases (e.g., DRE for design reviews, DRE for unit testing) or for the overall pre-release process.
        *   `DRE = (Defects_found_before_delivery / (Defects_found_before_delivery + Defects_found_after_delivery)) * 100`
    *   **Residual Defect Density:**
        *   **Definition:** The number of defects that remain in the software *after* it has been released to customers, normalized by size.
        *   An indicator of the quality experienced by the end-users.

### 2.2. Project Metrics

Project metrics are tactical and are used by project managers and the software team to adapt the project workflow and technical activities. They provide insight into the current state of an ongoing project.

#### Key Characteristics of Project Metrics:
*   **Tactical Focus:** Used for immediate monitoring and control of a specific project.
*   **Short-Term Collection:** Data is relevant to the current project lifecycle.
*   **Performance Monitoring:** Tracks progress against schedule, budget, and quality targets for the specific project.
*   **Examples (Conceptual):**
    *   **Schedule Variance (SV):**
        *   **Definition:** A measure of a project's schedule performance, indicating whether the project is ahead of, on, or behind its planned schedule.
        *   In Earned Value Management (EVM), `SV = Earned Value (EV) - Planned Value (PV)`.
            *   **Planned Value (PV):** The budgeted cost of work scheduled to be completed by a specific date.
            *   **Earned Value (EV):** The budgeted cost of work actually performed/completed by that specific date.
        *   A positive SV indicates being ahead of schedule; negative SV indicates being behind.
    *   **Schedule Variance for a Phase:** Applying the SV concept specifically to a distinct phase of the project to monitor its individual progress.
    *   **Effort Variance:**
        *   **Definition:** The difference between the planned effort for an activity or project and the actual effort expended.
        *   Indicates whether more or less effort than planned is being consumed.
    *   **Effort Variance for a Phase:** Applying effort variance calculation to individual project phases.
    *   **Size Variance:**
        *   **Definition:** The difference between the initially estimated size of the software (e.g., in KLOC or FP) and its actual or current re-estimated size.
        *   Helps track scope creep or inaccuracies in initial size estimation.
    *   **Requirement Stability Index (RSI):**
        *   **Definition:** A measure of the amount of change occurring in the project requirements over time.
        *   High stability is generally desirable. Low stability indicates significant changes, which can impact schedule, cost, and quality.
        *   Calculated by tracking the number of added, deleted, and modified requirements relative to the initial baseline.
    *   **Productivity Metrics (Project-Specific):**
        *   **Definition:** Measures of output (e.g., KLOC, FP, test cases, features) per unit of input (e.g., effort in person-months, cost).
        *   Examples:
            *   **Project Productivity:** `Actual Project Size / Actual Effort Expended`.
            *   **Test Case Preparation Productivity:** `Number of Test Cases Prepared / Effort for Preparation`.
            *   **Test Case Execution Productivity:** `Number of Test Cases Executed / Effort for Execution`.
            *   **Defect Detection Productivity:** `Number of Defects Detected / Effort for Detection Activities`.
            *   **Defect Fixation Productivity:** `Number of Defects Fixed / Effort for Fixation`.

## 3. Software Measurement

Software measurement is the process by which numbers or symbols are assigned to attributes of software entities (products, processes, resources) in such a way as to describe them according to clearly defined rules.

### 3.1. Categories of Software Measures

*   **Direct Measures (Internal Attributes):**
    *   Attributes of a software entity that can be measured purely in terms of the entity itself, without reference to its behavior or execution.
    *   These are often directly countable or observable.
    *   Examples:
        *   **Product:** Lines of Code (LOC), Cyclomatic Complexity, number of modules, number of parameters per function, memory size.
        *   **Process:** Effort expended (person-hours), cost (dollars), duration (days), number of defects found during reviews.
        *   **Resource:** Staff experience, hardware capacity.

*   **Indirect Measures (External Attributes):**
    *   Attributes of a software entity that can only be measured with respect to how the entity relates to its environment, often involving its behavior during execution or use.
    *   These are often derived from direct measures or observed during operation.
    *   Examples:
        *   **Product:** Functionality (measured by Function Points), quality, usability, reliability, maintainability, performance (response time, throughput).
        *   **Process:** Development productivity (FP/person-month), defect removal efficiency.

### 3.2. Principles of Good Measurement
*   **Clear Definition:** Measures and metrics should have precise, unambiguous definitions.
*   **Objectivity:** Measurement should be free from personal bias.
*   **Repeatability/Reliability:** Different people or the same person at different times should get consistent results when applying the measurement process.
*   **Validity:** The measure or metric should accurately reflect the attribute it is intended to quantify.
*   **Usefulness:** The measurement should provide information that is valuable for decision-making or process improvement.
*   **Automation:** Where possible, measurement collection should be automated to reduce effort and improve consistency.
*   **Economy:** The cost of collecting and analyzing data should not outweigh the benefits.

## 4. Metrics of Software Quality

Software quality is a multi-faceted concept. Quality metrics aim to quantify various aspects of software quality, both from an internal (structural) and external (behavioral/user-perceived) perspective.

### 4.1. McCall's Quality Factors (Classic Model)
Provides a framework for categorizing quality attributes:
*   **Product Operation:**
    *   **Correctness:** The extent to which a program satisfies its specifications and fulfills the user's mission objectives. (Metrics: Defect density, errors per KLOC).
    *   **Reliability:** The extent to which a program can be expected to perform its intended function with required precision. (Metrics: MTBF, failure rate, availability).
    *   **Efficiency:** The amount of computing resources and code required by a program to perform its function. (Metrics: Execution time, memory usage, throughput).
    *   **Integrity:** The extent to which access to software or data by unauthorized persons can be controlled. (Metrics: Security vulnerability counts).
    *   **Usability:** The effort required to learn, operate, prepare input for, and interpret output of a program. (Metrics: Task completion time, user error rates, satisfaction scores).
*   **Product Revision:**
    *   **Maintainability:** The effort required to locate and fix an error in an operational program. (Metrics: MTTR, cyclomatic complexity, code churn).
    *   **Flexibility:** The effort required to modify an operational program. (Metrics: Coupling, cohesion).
    *   **Testability:** The effort required to test a program to ensure that it performs its intended function. (Metrics: Test coverage, basis path coverage).
*   **Product Transition:**
    *   **Portability:** The effort required to transfer a program from one hardware and/or software system environment to another. (Metrics: Platform-dependent code, number of compilers supported).
    *   **Reusability:** The extent to which a program (or parts of it) can be reused in other applications. (Metrics: Component size, interface complexity).
    *   **Interoperability:** The effort required to couple one system with another. (Metrics: Number of standard interfaces used).

### 4.2. ISO 9126 / ISO 25010 Quality Model
A more modern standard, categorizing quality into characteristics and sub-characteristics:
*   **Functional Suitability:** (Completeness, Correctness, Appropriateness)
*   **Performance Efficiency:** (Time behavior, Resource utilization, Capacity)
*   **Compatibility:** (Co-existence, Interoperability)
*   **Usability:** (Appropriateness recognizability, Learnability, Operability, User error protection, User interface aesthetics, Accessibility)
*   **Reliability:** (Maturity, Availability, Fault tolerance, Recoverability)
*   **Security:** (Confidentiality, Integrity, Non-repudiation, Accountability, Authenticity)
*   **Maintainability:** (Modularity, Reusability, Analyzability, Modifiability, Testability)
*   **Portability:** (Adaptability, Installability, Replaceability)

For each sub-characteristic, specific metrics can be defined and measured.

## 5. S/W Reliability

Software reliability is the probability that a software system will perform its intended functions without failure for a specified period under stated conditions. It's a critical aspect of software quality, especially for mission-critical systems.

### 5.1. Key Terminology and Metrics

*   **Failure:** Any deviation of the observed behavior of the software from the specified or expected behavior.
*   **Fault (Defect/Bug):** A static characteristic of the software (e.g., an incorrect line of code) that may lead to a failure when executed under particular conditions.
*   **Error:** A human action that results in a fault.
*   **Mean Time To Failure (MTTF):** The average time a system operates correctly before the *first* failure occurs, or between failures for systems that are not repaired immediately. Crucial for non-repairable systems or when repair is very costly/time-consuming.
*   **Mean Time To Repair (MTTR):** The average time taken to diagnose and repair a fault after a failure has occurred and restore the system to operational status.
*   **Mean Time Between Failures (MTBF):** The average time elapsed from one failure to the next in a repairable system. `MTBF = MTTF + MTTR`.
*   **Availability (A):** The probability that the software system is operational and accessible when needed.
    *   `A = MTTF / (MTTF + MTTR)` or `A = MTBF_operational / (MTBF_operational + MTTR_downtime)`.
    *   Often expressed as a percentage (e.g., 99.999% "five nines" availability).
*   **Failure Rate (λ):** The number of failures per unit time. In the useful life phase of a system (constant failure rate), `λ = 1 / MTTF`.
*   **Probability Of Failure On Demand (POFOD):** The likelihood that the system will fail when a service is requested. Relevant for safety-critical systems where demands are infrequent.
*   **Rate Of Occurrence Of Failure (ROCOF):** The frequency of occurrence of unexpected behavior (failures). Similar to failure rate but can be observed over any time interval.

### 5.2. Software Reliability Models
Mathematical models used to estimate, predict, and assess software reliability based on failure data collected during testing or operation.
*   **Types of Models:**
    *   **Reliability Growth Models:** Assume that as faults are detected and removed, the software's reliability improves. These are dynamic models applied during testing.
        *   *Examples:* Jelinski-Moranda, Musa Basic Execution Time Model, Goel-Okumoto NHPP, Littlewood-Verrall.
    *   **Static Defect Models:** Attempt to predict the number of faults or reliability based on static characteristics of the software (e.g., size, complexity metrics) or the development process.
*   **Challenges in Modeling:**
    *   Software failures are often due to design faults, not physical wear-out.
    *   The operating environment significantly affects failure occurrence.
    *   Accurate failure data collection is crucial but can be difficult.

## 6. Software Estimation Techniques

Software estimation is the process of predicting the most realistic amount of effort (person-hours/months), cost, time, and resources required to build or maintain a software system.

### 6.1. Importance and Challenges
*   **Importance:** Crucial for project planning, bidding, resource allocation, and managing stakeholder expectations.
*   **Challenges:**
    *   Uncertainty in requirements.
    *   Changing technology.
    *   Lack of historical data.
    *   Human factors (skill, experience).
    *   Pressure to provide low estimates.

### 6.2. Project Size Estimation
Estimating the "size" of the software is a primary input to most effort and cost estimation models. Size is a proxy for the amount of work involved.

#### 6.2.1. Lines of Code (LOC) / Source Lines of Code (SLOC)
*   **Definition:** A direct measure of software size based on counting the number of lines in the source code.
*   **Counting Conventions:** Rules must be established (e.g., exclude comments, blank lines; how to count declarations vs. executable statements). KLOC (Thousand Lines of Code) is a common unit.
*   **Estimation Methods:**
    *   **Expert Judgment:** Based on experience with similar projects.
    *   **Analogy:** Comparing with completed similar projects.
    *   **Decomposition:** Breaking the system into smaller components, estimating LOC for each, and summing them up.
*   **Advantages:** Simple to understand and measure (once code exists).
*   **Disadvantages/Shortcomings:**
    *   **Language Dependency:** LOC varies greatly between programming languages for the same functionality.
    *   **Programmer Skill Dependency:** Different programmers may write different amounts of code for the same task.
    *   **Poor Indicator of Complexity/Effort:** Does not directly reflect algorithmic complexity or design effort.
    *   **Discourages Reuse & High-Level Languages:** Using libraries or more expressive languages leads to lower LOC, which can be misinterpreted.
    *   **Difficult to Estimate Accurately Early:** Precise LOC is unknown until coding is well underway or complete.
    *   **Focuses on Coding Activity:** Underestimates effort for other phases like design, testing, documentation.

#### 6.2.2. Function Point (FP) Analysis
*   **Definition:** An indirect measure of software size based on quantifying the functionality provided to the user, from the user's perspective.
*   **Core Principle:** Size is a function of the number and complexity of user-recognizable functions.
*   **Advantages:**
    *   Language and technology independent.
    *   Can be estimated early in the lifecycle (from requirements).
    *   Correlates well with effort.
*   **Process of FP Calculation (IFPUG - International Function Point Users Group - is a common standard):**
    1.  **Determine Type of FP Count:** (Development, Enhancement, Application).
    2.  **Identify Application Boundary:** Defines what is internal versus external to the application being counted.
    3.  **Count Data Functions:**
        *   **Internal Logical Files (ILFs):** User-identifiable, logically related groups of data maintained *within* the application boundary.
        *   **External Interface Files (EIFs):** User-identifiable, logically related groups of data referenced by the application but maintained *outside* its boundary (by another application).
    4.  **Count Transactional Functions:**
        *   **External Inputs (EIs):** Elementary processes that process data or control information entering the application from outside the boundary.
        *   **External Outputs (EOs):** Elementary processes that send data or control information outside the application boundary.
        *   **External Inquiries (EQs):** Elementary processes with both input and output components that result in data retrieval without altering any ILFs.
    5.  **Determine Complexity for Each Function:** Each identified ILF, EIF, EI, EO, EQ is classified as Low, Average, or High complexity based on rules involving Data Element Types (DETs), Record Element Types (RETs), and File Types Referenced (FTRs).
    6.  **Calculate Unadjusted Function Points (UFP):** Multiply the count of each function type by its complexity weight and sum the results.
        `(Count_EI_Low * W_EI_L) + (Count_EI_Avg * W_EI_A) + ... + (Count_EIF_High * W_EIF_H)`
        (Standard IFPUG weights: EI: L=3,A=4,H=6; EO: L=4,A=5,H=7; EQ: L=3,A=4,H=6; ILF: L=7,A=10,H=15; EIF: L=5,A=7,H=10)
    7.  **Determine Value Adjustment Factor (VAF) / General System Characteristics (GSCs):**
        *   Assess 14 GSCs that describe the general processing complexity of the application.
        *   Each GSC is rated on a scale of 0 (no influence) to 5 (strong influence).
        *   Examples of GSCs: Data Communications, Distributed Data Processing, Performance, Heavily Used Configuration, Transaction Rate, On-Line Data Entry, End User Efficiency, On-Line Update, Complex Processing, Reusability, Installation Ease, Operational Ease, Multiple Sites, Facilitate Change.
        *   **Total Degree of Influence (DI):** Sum of the ratings for all 14 GSCs (`DI = Σ fi`).
        *   **VAF Calculation:** `VAF = (DI * 0.01) + 0.65`. (VAF ranges from 0.65 to 1.35).
    8.  **Calculate Adjusted Function Points (FP):**
        `FP = UFP * VAF`.
*   **Shortcomings:**
    *   **Subjectivity:** Identification of functions and GSC rating can be subjective.
    *   **Time-Consuming:** Can be a detailed and lengthy process for large systems.
    *   **Training Required:** Requires trained personnel for accurate counting.
    *   Less suited for some types of systems (e.g., purely scientific/algorithmic, real-time embedded systems with minimal user I/O). (Feature Points and other variants try to address this).

### 6.3. Empirical Estimation Models
Models based on data derived from a wide range of completed software projects. They use formulas or algorithms that relate size to effort, cost, and duration.

#### 6.3.1. COCOMO (Constructive Cost Model)
*   Developed by Barry Boehm, one of the most widely known and used empirical models.
*   **Basic Principle:** Relates software size (in KLOC) to effort (in Person-Months) and development time (TDEV in months).
*   **Project Modes:** Categorizes projects to account for differing development environments and team characteristics.
    *   **Organic Mode:** Small, experienced teams, familiar environment, flexible requirements, less than 50 KLOC.
    *   **Semi-Detached Mode:** Mixed experience, moderately rigid requirements, up to 300 KLOC.
    *   **Embedded Mode:** Tight constraints (hardware, software, operational), complex, innovative, often large KLOC.
*   **COCOMO Levels:**
    *   **Basic COCOMO:**
        *   Provides a quick, rough estimate.
        *   Effort: `E = a * (KLOC)^b`
        *   TDEV: `TDEV = c * (E)^d`
        *   Coefficients `a, b, c, d` vary based on the project mode (Organic, Semi-Detached, Embedded).
    *   **Intermediate COCOMO:**
        *   Refines Basic COCOMO by incorporating an **Effort Adjustment Factor (EAF)**.
        *   EAF is the product of multipliers associated with 15 **Cost Drivers** (categorized into Product, Hardware, Personnel, and Project attributes).
        *   Each cost driver is rated (e.g., Very Low to Extra High), and each rating has a specific multiplier.
        *   Nominal Effort: `E_nominal = a_i * (KLOC)^(b_i)` (coefficients `a_i, b_i` differ from Basic COCOMO).
        *   Adjusted Effort: `E_adjusted = E_nominal * EAF`.
        *   TDEV formula remains similar, using the adjusted effort.
    *   **Detailed COCOMO:**
        *   Extends Intermediate COCOMO by applying cost drivers and effort multipliers at the phase level (e.g., requirements, design, coding, testing) of the software lifecycle.
        *   Provides more granular estimates.
*   **COCOMO II (Successor Model):**
    *   Developed to address modern software development practices (e.g., object-orientation, reuse, COTS, spiral/incremental models).
    *   Comprises a suite of models:
        *   **Application Composition Model:** For early estimation of projects built using prototyping, GUI builders, etc. Uses **Object Points**.
        *   **Early Design Model:** For use after requirements are stabilized and an initial architecture is defined. Uses **Unadjusted Function Points (UFP)** and 7 coarse-grained cost drivers (Scale Factors and Effort Multipliers).
        *   **Post-Architecture Model:** The most detailed model, used when the architecture is well-defined. Uses **KSLOC** (Source Lines of Code, can be adapted from FP) and 17 cost drivers (5 Scale Factors and 12 Effort Multipliers).
    *   **Scale Factors in COCOMO II:** Account for factors that cause diseconomies of scale (Precedentedness, Development Flexibility, Architecture/Risk Resolution, Team Cohesion, Process Maturity).
*   **Strengths of COCOMO:** Well-documented, widely used, provides a structured approach.
*   **Weaknesses of COCOMO:** Relies on KLOC (which has its own estimation issues), calibration to local environment is crucial for accuracy, cost driver ratings can be subjective.

## 7. Project Tracking and Scheduling

### 7.1. Project Tracking
The ongoing process of comparing actual project progress against the planned progress, identifying deviations, and taking corrective actions.

*   **Key Activities:**
    *   **Monitoring Milestones:** Checking if key deliverables and checkpoints are met on time.
    *   **Tracking Effort:** Recording actual effort spent on tasks and comparing with planned effort.
    *   **Tracking Costs:** Monitoring actual expenditure against the budget.
    *   **Quality Monitoring:** Tracking defect discovery rates, DRE, etc.
    *   **Scope Monitoring:** Ensuring the project stays within the defined scope and managing changes.
*   **Techniques:**
    *   **Regular Status Meetings:** For team updates and issue discussion.
    *   **Progress Reports:** Formal documentation of status, issues, and risks.
    *   **Time Sheets:** For effort tracking.
    *   **Earned Value Management (EVM):** A comprehensive technique integrating scope, schedule, and cost.
        *   **Planned Value (PV):** Budgeted cost of work scheduled.
        *   **Earned Value (EV):** Budgeted cost of work performed.
        *   **Actual Cost (AC):** Actual cost of work performed.
        *   **Schedule Variance (SV) = EV - PV**
        *   **Cost Variance (CV) = EV - AC**
        *   **Schedule Performance Index (SPI) = EV / PV**
        *   **Cost Performance Index (CPI) = EV / AC**

### 7.2. Project Scheduling
The process of defining project activities, their logical sequence, estimating their durations, and assigning resources to them to create a project timeline.

*   **Key Steps:**
    1.  **Work Breakdown Structure (WBS):** Decomposing the project into smaller, manageable tasks or work packages.
    2.  **Activity Definition:** Clearly defining each task from the WBS.
    3.  **Activity Sequencing:** Determining the dependencies between activities (e.g., finish-to-start, start-to-start).
    4.  **Resource Estimation:** Identifying the type and quantity of resources (personnel, tools, facilities) needed for each activity.
    5.  **Duration Estimation:** Estimating the time required to complete each activity with the assigned resources.
    6.  **Schedule Development:** Integrating the above information to create the project schedule.
*   **Scheduling Tools and Techniques:**
    *   **Gantt Charts:** Bar charts visually representing tasks, their durations, start/end dates, and dependencies over a timeline. Good for visualization and communication.
    *   **Network Diagrams (PERT/CPM):**
        *   **PERT (Program Evaluation and Review Technique):** Uses probabilistic time estimates (optimistic, most likely, pessimistic) to calculate expected duration. Good for R&D projects with uncertainty.
        *   **CPM (Critical Path Method):** Determines the sequence of activities (the "critical path") that dictates the minimum project duration. Activities on the critical path have zero slack or float. Any delay in a critical path activity delays the entire project.
    *   **Critical Chain Project Management (CCPM):** Focuses on managing resource constraints and buffers.

## 8. Reverse Engineering

The process of analyzing an existing software system to understand its components, their interrelationships, and its design, often to create higher-level abstractions or recover lost information. It focuses on understanding, not modifying or recreating (which is re-engineering).

### 8.1. Objectives and Motivations
*   **Understanding Legacy Systems:** To maintain, enhance, or migrate old systems where documentation is poor or missing.
*   **Redocumentation:** Creating or updating documentation based on the actual system.
*   **Design Recovery:** Extracting design information (architecture, component interactions) from code.
*   **Code Comprehension:** Helping developers understand complex or unfamiliar code.
*   **Identifying Reusable Components:** Finding parts of an existing system that can be reused.
*   **Facilitating Maintenance and Evolution:** Making it easier to modify and evolve the system.
*   **Migration Planning:** Understanding a system before migrating it to a new platform or technology.
*   **Security Analysis:** Identifying vulnerabilities by understanding system structure and behavior.

### 8.2. Process Activities
1.  **Information Collection:** Gathering all available artifacts (source code, executables, database schemas, existing documentation, user manuals, test cases).
2.  **System Analysis:**
    *   **Static Analysis:** Examining the system's code and structure without executing it. Techniques include parsing, control flow analysis, data flow analysis, metrics calculation.
    *   **Dynamic Analysis:** Observing the system's behavior during execution. Techniques include tracing, profiling, debugging, monitoring function calls and data changes.
3.  **Abstraction and Model Generation:** Creating higher-level representations from the analyzed information, such as:
    *   Architectural diagrams (e.g., component diagrams, deployment diagrams).
    *   UML diagrams (class diagrams, sequence diagrams).
    *   Data models (ER diagrams).
    *   Control flow graphs, call graphs.
4.  **Interpretation and Documentation:** Understanding the generated models and documenting the findings about the system's structure, behavior, and design.

### 8.3. Levels of Abstraction
Reverse engineering can operate at different levels:
*   **Implementation Level:** Understanding source code, data structures, algorithms.
*   **Structural/Design Level:** Identifying modules, components, interfaces, and their relationships (architectural recovery).
*   **Functional/Requirements Level:** (Most challenging) Inferring the intended functionality and high-level requirements the system was built to address.

### 8.4. Tools and Techniques
*   **Source Code Browsers and Analyzers:** Help navigate and understand code structure.
*   **Disassemblers and Decompilers:** Convert machine code or bytecode to assembly or a higher-level representation (often with limitations).
*   **Profilers and Tracers:** For dynamic analysis.
*   **Modeling Tools with Reverse Engineering Capabilities:** (e.g., some UML tools can generate class diagrams from code).
*   **Database Schema Reverse Engineering Tools:** Generate ER diagrams from database definitions.

### 8.5. Challenges
*   **Complexity:** Legacy systems can be very large and convoluted.
*   **Incompleteness:** Missing source code or documentation.
*   **Obfuscation:** Code might be intentionally or unintentionally hard to understand.
*   **Language and Platform Diversity:** Dealing with outdated or obscure technologies.
*   **Tool Limitations:** No single tool can fully automate the process; significant human expertise is required.
*   **Effort and Cost:** Can be a very time-consuming and expensive undertaking.

This detailed conceptual overview should provide a strong foundation for your understanding of Unit II.

Below are the canonical **COCOMO formulas** with the coefficient tables you need for both the original _COCOMO ’81_ family and the modern _COCOMO II_ family.  
(Values are those published by Barry Boehm’s research group; organisations sometimes calibrate them to their own history.)

---

## 1 COCOMO ’81

### 1.1 Basic model (three development “modes”)

|Mode|Effort coefficient **a**|Effort exponent **b**|Schedule coefficient **c**|Schedule exponent **d**|When this mode applies|
|---|---|---|---|---|---|
|**Organic**|2.4|1.05|2.5|0.38|Small, stable, well-understood business apps; cohesive team, little innovation needed|
|**Semi-detached**|3.0|1.12|2.5|0.35|Medium-sized systems, mixed experience levels, some constraints|
|**Embedded**|3.6|1.20|2.5|0.32|Real-time or mission-critical systems with tight hardware/regulation constraints|

**Formulas**

```text
Effort (Person-Months)        E  = a · (KLOC)^b
Development Time (Months)     T  = c · (E)^d
Average Staff                 P  = E / T
Productivity                  = KLOC / E
```

---

### 1.2 Intermediate model

Adds a single **EAF (Effort-Adjustment Factor)**—the product of 15 cost-driver multipliers that cover Product, Platform, Personnel and Project attributes.

```
E  = a · (KLOC)^b · EAF
T  = c · (E)^d
```

Cost-driver snapshot (full table has six rating levels each):

|Driver|V. Low|Low|Nom|High|V. High|X-High|
|---|---|---|---|---|---|---|
|RELY – Required reliability|0.75|0.88|**1.00**|1.15|1.40|–|
|DATA – Data size|–|0.94|**1.00**|1.08|1.16|–|
|PCAP – Programmer capability|1.46|1.19|**1.00**|0.86|0.71|–|
|…|||||||

_Multiply all the chosen multipliers together to get EAF._

---

### 1.3 Detailed model

_Same core equations_ but applies the cost drivers **phase-by-phase** (requirements, design, code & unit test, integration, etc.) and allocates the resulting effort across each phase using distribution tables supplied by Boehm.

---

## 2 COCOMO II

COCOMO II has two operational forms:

- **Early-Design** (model when you only know major system pieces).
    
- **Post-Architecture** (model after full architecture is fixed).
    

Both share the general equation

```text
Effort (PM)  = A · Size^E · Π  EM_i
Schedule (M) = 3.67 · Effort^F
```

### 2.1 Parameters and drivers

|Symbol|Meaning|Default value|
|---|---|---|
|**A**|Calibration constant (industry default)|**2.94**|
|**Size**|KSLOC _or_ equivalent KSLOC from Function-Point “back-firing”|—|
|**E**|Economy-of-scale exponent|B + 0.01 Σ **SF**j|
|**B**|Baseline exponent offset|**0.91**|
|**Σ SFj**|Sum of the 5 **Scale Factors**|5 × (1 – 5) → 0–25|
|**EMi**|17 Effort Multipliers (Post-Arch) or 7 (ED)|0.7 – 1.74|
|**F**|Schedule exponent|0.28 + 0.2 (E – B)|

#### 2.1.1 Scale Factors (affect **E**)

|SF|Very Low|Low|Nominal|High|Very High|Extra High|
|---|---|---|---|---|---|---|
|**PREC** – precedentedness|6.20|4.96|**3.72**|2.48|1.24|–|
|**FLEX** – development flexibility|5.07|4.05|**3.04**|2.03|1.01|–|
|**RESL** – architecture & risk resolution|7.07|5.65|**4.24**|2.83|1.41|–|
|**TEAM** – team cohesion|5.48|4.38|**3.29**|2.19|1.10|–|
|**PMAT** – process maturity|7.80|6.24|**4.68**|3.12|1.56|–|

_(Add the chosen numeric values, then plug into E = B + 0.01 ΣSF.)_

#### 2.1.2 Effort Multipliers (snapshot)

|Category|EM|VL|L|N|H|VH|XH|
|---|---|---|---|---|---|---|---|
|Product|**RELY** – required reliability|0.82|0.92|**1.00**|1.10|1.26|1.39|
|Platform|**TIME** – execution time constraint|–|–|**1.00**|1.11|1.30|1.66|
|Personnel|**PCAP** – programmer capability|1.42|1.17|**1.00**|0.86|0.70|–|
|Project|**SCED** – schedule compression|–|1.14|**1.00**|1.00|1.00|1.00|
|…||||||||

_Multiply all selected EMs; substitute into the main effort formula._

### 2.2 Schedule exponent **F**

```
F = 0.28 + 0.2 · (E – B)
```

As E rises (from high scale-factor ratings), F rises, reflecting diseconomies-of-scale that lengthen schedules.

---

## 3 Using the tables

1. **Size the system** in _KSLOC_ or _Function Points → back-firing_ → KSLOC.
    
2. Pick the development **mode** (’81) _or_ rate the **scale factors** (II).
    
3. Select cost-driver / EM ratings.
    
4. Plug into the formulas to compute **Effort**, **Time**, **Avg Staff**, **Productivity**.
    
5. Calibrate **a, A, etc.** with local historical data for ±20 % accuracy.
    

These tables and equations form the backbone of most commercial parametric-estimation tools and remain the industry baseline for scope-/effort-/cost planning.