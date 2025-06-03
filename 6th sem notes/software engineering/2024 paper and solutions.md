# RGPV Software Engineering & Agile - May 2024 Complete Solutions

**Course:** CI-601 (CSIT) | **Program:** B.Tech. VI Semester | **Max Marks:** 70

---

## Question 1

### 1a) System Engineering Hierarchy & Restraining Factors (7 marks)

**System Engineering Hierarchy:**

System engineering follows a hierarchical approach that can be viewed at multiple levels:

1. **World View (Business Domain)**
    
    - Defines overall business or product domain
    - Establishes broad objectives and constraints
    - Example: E-commerce, Healthcare, Banking
2. **Domain View (Application Domain)**
    
    - Focuses on specific application area within the business domain
    - Defines system boundaries and interfaces
    - Example: Online payment system within e-commerce
3. **Element View (Software Elements)**
    
    - Individual software components and their interactions
    - Detailed design and implementation level
    - Example: Authentication module, database interface
4. **Detailed View (Module Implementation)**
    
    - Internal structure of individual elements
    - Code-level implementation details

**Restraining Factors in System Model Construction:**

1. **Complexity Constraints**
    
    - System complexity may exceed modeling capabilities
    - Interdependencies between components are difficult to capture
2. **Resource Limitations**
    
    - Time and budget constraints
    - Limited expertise and tools
3. **Requirement Volatility**
    
    - Changing requirements during modeling
    - Incomplete or ambiguous specifications
4. **Technical Constraints**
    
    - Hardware/software platform limitations
    - Integration challenges with existing systems
5. **Organizational Factors**
    
    - Communication gaps between stakeholders
    - Conflicting priorities and objectives

### 1b) Waterfall Model & Problems (7 marks)

**Waterfall Model:**

```
Requirements Analysis
        ↓
System Design
        ↓
Implementation
        ↓
Integration & Testing
        ↓
Deployment
        ↓
Maintenance
```

**Phases Description:**

1. **Requirements Analysis:** Gather and document all requirements
2. **System Design:** Create system architecture and design
3. **Implementation:** Code development based on design
4. **Integration & Testing:** Combine modules and test the system
5. **Deployment:** Install system in production environment
6. **Maintenance:** Ongoing support and modifications

**Problems with Waterfall Model:**

1. **Inflexibility to Changes**
    
    - Difficult to accommodate requirement changes
    - Late discovery of issues is expensive to fix
2. **Late Testing**
    
    - Testing occurs only after implementation
    - Defects discovered late in the cycle
3. **No Working Software Until Late**
    
    - No deliverable until project completion
    - Client cannot see progress
4. **Poor Risk Management**
    
    - Risks identified late in the process
    - No early feedback mechanism
5. **Unrealistic Assumptions**
    
    - Assumes requirements are completely known upfront
    - Linear progression rarely matches reality

---

## Question 2

### 2a) Configuration Management & Four Steps (7 marks)

**Configuration Management:**

Configuration Management (CM) is a process of identifying, organizing, and controlling changes to software work products throughout the software development lifecycle. It ensures that changes are made systematically and that the integrity of the software is maintained.

**Four Steps of Configuration Management:**

1. **Configuration Identification**
    
    - Identify configuration items (CIs)
    - Establish baselines
    - Create unique naming conventions
    - Document CI relationships and dependencies
2. **Configuration Control**
    
    - Control changes to configuration items
    - Change request evaluation and approval
    - Impact analysis of proposed changes
    - Authorization of changes through Change Control Board (CCB)
3. **Configuration Status Accounting**
    
    - Record and report configuration information
    - Track status of configuration items
    - Maintain change history and audit trails
    - Generate status reports for management
4. **Configuration Auditing**
    
    - Verify that CIs conform to requirements
    - Ensure completeness and correctness
    - Physical configuration audit
    - Functional configuration audit

### 2b) Functional and Behavioral Modeling (7 marks)

**Functional Modeling:**

Represents what the system does - the functions and processes.

**Example - Library Management System:**

```
Data Flow Diagram (DFD):
[Student] → (Issue Book) → [Book Database]
[Librarian] → (Add Book) → [Book Database]
[Book Database] → (Generate Report) → [Management]
```

**Components:**

- **Processes:** Issue Book, Return Book, Add Book
- **Data Stores:** Book Database, Student Database
- **External Entities:** Student, Librarian, Management
- **Data Flows:** Book Request, Book Details, Reports

**Behavioral Modeling:**

Represents how the system behaves over time - state changes and interactions.

**Example - Book State Diagram:**

```
[Available] → (Issue) → [Issued] → (Return) → [Available]
     ↓                      ↓
(Reserve)              (Overdue)
     ↓                      ↓
[Reserved]            [Overdue]
```

**State Transition Table:**

|Current State|Event|Next State|Action|
|---|---|---|---|
|Available|Issue|Issued|Update database|
|Issued|Return|Available|Calculate fine|
|Issued|Overdue|Overdue|Send notice|

**Key Differences:**

- Functional modeling focuses on data flow and processes
- Behavioral modeling focuses on states and state transitions
- Both complement each other for complete system understanding

---

## Question 3

### 3a) COCOMO Model for Cost Estimation (7 marks)

**COCOMO (Constructive Cost Model):**

COCOMO is an algorithmic software cost estimation model developed by Barry Boehm. It estimates effort, development time, and team size for software projects.

**Three Models of COCOMO:**

1. **Basic COCOMO**
    
    - Simple estimation based on program size
    - Formula: Effort = a × (KLOC)^b
    - Development Time = c × (Effort)^d
2. **Intermediate COCOMO**
    
    - Considers 15 cost driver attributes
    - More accurate than Basic COCOMO
    - Effort Adjustment Factor (EAF) applied
3. **Detailed COCOMO**
    
    - Phase-sensitive effort multipliers
    - Most accurate but complex
    - Different multipliers for each development phase

**Project Categories:**

1. **Organic Mode** (a=2.4, b=1.05, c=2.5, d=0.38)
    
    - Small teams with good experience
    - Familiar, stable environment
    - Example: Business applications
2. **Semi-detached Mode** (a=3.0, b=1.12, c=2.5, d=0.35)
    
    - Medium-sized teams
    - Mixed experience levels
    - Example: Database systems
3. **Embedded Mode** (a=3.6, b=1.20, c=2.5, d=0.32)
    
    - Large projects with tight constraints
    - Complex, innovative systems
    - Example: Real-time systems

**Example Calculation (Organic Mode):**

- Given: KLOC = 10
- Effort = 2.4 × (10)^1.05 = 2.4 × 10.47 = 25.1 person-months
- Development Time = 2.5 × (25.1)^0.38 = 2.5 × 3.5 = 8.75 months

### 3b) Decomposition, Abstraction & Modularity in Software Design (7 marks)

**Decomposition:**

Process of breaking down a complex system into smaller, manageable components.

**Levels of Decomposition:**

1. **System Level:** Break system into subsystems
2. **Subsystem Level:** Break subsystems into modules
3. **Module Level:** Break modules into functions
4. **Function Level:** Break functions into statements

**Example:**

```
E-commerce System
├── User Management Subsystem
│   ├── Authentication Module
│   ├── User Profile Module
│   └── Access Control Module
├── Product Management Subsystem
│   ├── Catalog Module
│   ├── Inventory Module
│   └── Search Module
└── Order Management Subsystem
    ├── Shopping Cart Module
    ├── Payment Module
    └── Shipping Module
```

**Abstraction:**

Process of hiding implementation details while showing only essential features.

**Levels of Abstraction:**

1. **Procedural Abstraction:** Hide algorithmic details
2. **Data Abstraction:** Hide data representation details
3. **Control Abstraction:** Hide control flow details

**Example:**

```
// High-level abstraction
processPayment(amount, cardDetails)

// Lower-level details hidden:
// - Encryption algorithms
// - Bank communication protocols
// - Transaction validation logic
```

**Modularity:**

Principle of dividing software into separate, interchangeable components.

**Characteristics of Good Modules:**

1. **High Cohesion:** Elements within module work together
2. **Low Coupling:** Minimal dependencies between modules
3. **Information Hiding:** Internal details not visible outside
4. **Well-defined Interfaces:** Clear communication mechanisms

**Benefits:**

- Easier maintenance and debugging
- Parallel development possible
- Code reusability
- Better testing capabilities

---

## Question 4

### 4a) Reverse Engineering & Legacy Software Improvement (7 marks)

**Reverse Engineering Definition:**

Reverse Engineering is the process of analyzing a software system to identify its components and their interrelationships, and create representations of the system at higher levels of abstraction.

**Reverse Engineering Process:**

1. **Code Analysis**
    
    - Parse source code
    - Identify program structure
    - Extract design information
2. **Data Analysis**
    
    - Analyze data structures
    - Identify relationships
    - Create data models
3. **Interface Analysis**
    
    - Study user interfaces
    - Document interaction patterns
    - Identify usability issues
4. **Architecture Recovery**
    
    - Reconstruct system architecture
    - Identify components and connections
    - Document design decisions

**How Reverse Engineering Improves Legacy Software:**

1. **Understanding Legacy Systems**
    
    - Documentation often missing or outdated
    - Helps understand system functionality
    - Identifies system dependencies
2. **Impact Analysis**
    
    - Analyze effects of proposed changes
    - Identify affected components
    - Reduce risk of modifications
3. **Migration Planning**
    
    - Plan system migration to new platforms
    - Identify reusable components
    - Design migration strategy
4. **Quality Improvement**
    
    - Identify design flaws and bottlenecks
    - Restructure code for better maintainability
    - Optimize performance issues
5. **Knowledge Transfer**
    
    - Transfer knowledge to new team members
    - Create proper documentation
    - Preserve business logic understanding

**Benefits:**

- Reduced maintenance costs
- Better system understanding
- Easier system evolution
- Risk mitigation in changes

### 4b) Software Requirement Specification for Library Management System (7 marks)

**SOFTWARE REQUIREMENT SPECIFICATION** **Library Management System**

**1. INTRODUCTION**

**1.1 Purpose** This document specifies requirements for a Library Management System to automate library operations including book management, member management, and circulation control.

**1.2 Scope** The system will manage books, members, staff, and library transactions including issue, return, and reservation of books.

**2. FUNCTIONAL REQUIREMENTS**

**2.1 Book Management**

- Add, modify, delete book records
- Search books by title, author, ISBN, category
- Track book availability status
- Generate book reports

**2.2 Member Management**

- Register new members
- Update member information
- Track member borrowing history
- Manage member categories (student, faculty, staff)

**2.3 Circulation Management**

- Issue books to members
- Process book returns
- Calculate and collect fines
- Handle book reservations
- Generate overdue notices

**2.4 Reports and Analytics**

- Popular books report
- Member activity report
- Overdue books report
- Financial reports (fines collected)

**3. NON-FUNCTIONAL REQUIREMENTS**

**3.1 Performance**

- System should handle 1000 concurrent users
- Response time < 3 seconds for queries
- 99.9% system availability

**3.2 Security**

- User authentication and authorization
- Data encryption for sensitive information
- Audit trail for all transactions

**3.3 Usability**

- Intuitive user interface
- Online help system
- Multi-language support

**4. SYSTEM INTERFACES**

**4.1 User Interfaces**

- Web-based interface for librarians
- Mobile app for members
- Admin console for system administration

**4.2 Hardware Interfaces**

- Barcode scanner integration
- Printer support for receipts and reports

**4.3 Software Interfaces**

- Database management system
- Email system for notifications
- Backup and recovery system

**5. CONSTRAINTS**

- Must work on Windows and Linux platforms
- Compatible with existing library hardware
- Budget limitation of $50,000

---

## Question 5

### 5a) Two Software Metrics with Advantages & Disadvantages (7 marks)

**Metric 1: Lines of Code (LOC)**

**Description:** Lines of Code is a size-oriented metric that measures the number of executable lines of code in a software program, excluding comments and blank lines.

**Calculation:**

- Count physical lines of code
- Exclude comments, blank lines, and declarations
- Can be measured as KLOC (Thousand Lines of Code)

**Advantages:**

1. **Simple to Measure:** Easy to count and automate
2. **Widely Used:** Industry standard metric
3. **Historical Data:** Extensive historical data available
4. **Effort Estimation:** Used in effort estimation models like COCOMO
5. **Progress Tracking:** Can track development progress
6. **Language Independent:** Can be applied to any programming language

**Disadvantages:**

1. **Language Dependency:** Different languages require different LOC for same functionality
2. **Quality Independence:** More lines don't mean better quality
3. **Programmer Bias:** Encourages verbose programming
4. **Functionality Ignorance:** Doesn't consider complexity or difficulty
5. **Reuse Penalty:** Penalizes code reuse and libraries
6. **Design Impact:** May discourage good design practices

**Metric 2: Function Point (FP)**

**Description:** Function Point is a function-oriented metric that measures software size based on functionality delivered to the user, independent of programming language.

**Components:**

1. External Inputs (EI)
2. External Outputs (EO)
3. External Inquiries (EQ)
4. Internal Logical Files (ILF)
5. External Interface Files (EIF)

**Calculation:** FP = [EI × 4 + EO × 5 + EQ × 4 + ILF × 10 + EIF × 7] × CAF

Where CAF = Complexity Adjustment Factor (0.65 to 1.35)

**Advantages:**

1. **Language Independent:** Same FP value regardless of programming language
2. **User-Oriented:** Based on user functionality
3. **Early Estimation:** Can be calculated from requirements
4. **Quality Focus:** Encourages focus on functionality
5. **Standardized:** IEEE standard (IEEE 1045)
6. **Productivity Measure:** Good for measuring productivity across projects

**Disadvantages:**

1. **Complex Calculation:** Requires training and experience
2. **Subjective Elements:** Complexity factors can be subjective
3. **Time Consuming:** Takes time to calculate accurately
4. **Limited Applicability:** Not suitable for all types of software
5. **Maintenance Overhead:** Requires updates when requirements change
6. **Industry Variation:** Interpretation may vary across organizations

### 5b) Differences between Software Design and Project Planning (7 marks)

**SOFTWARE DESIGN vs PROJECT PLANNING**

|Aspect|Software Design|Project Planning|
|---|---|---|
|**Purpose**|Define system architecture and structure|Define project execution strategy|
|**Focus**|Technical solution and implementation|Resource allocation and scheduling|
|**Output**|Design documents, models, prototypes|Project plan, schedules, budgets|
|**Timeline**|During design phase|Before and throughout project|
|**Stakeholders**|Developers, architects, analysts|Project managers, clients, stakeholders|

**Detailed Differences:**

**1. Objective**

- **Software Design:** Create technical blueprint for software construction
- **Project Planning:** Establish roadmap for project execution and delivery

**2. Activities**

- **Software Design:**
    
    - Architecture design
    - Interface design
    - Database design
    - Algorithm design
    - Component design
- **Project Planning:**
    
    - Task identification
    - Resource allocation
    - Schedule development
    - Risk assessment
    - Budget estimation

**3. Deliverables**

- **Software Design:**
    
    - System architecture diagrams
    - Database schemas
    - Interface specifications
    - Design documents
    - Prototypes
- **Project Planning:**
    
    - Work breakdown structure
    - Project schedules
    - Resource plans
    - Risk management plans
    - Quality assurance plans

**4. Skills Required**

- **Software Design:**
    
    - Technical expertise
    - Domain knowledge
    - Design patterns
    - Technology understanding
- **Project Planning:**
    
    - Management skills
    - Estimation techniques
    - Risk analysis
    - Communication skills

**5. Success Criteria**

- **Software Design:**
    
    - Meets functional requirements
    - Scalable and maintainable
    - Performance requirements met
    - Quality standards achieved
- **Project Planning:**
    
    - On-time delivery
    - Within budget
    - Resource utilization
    - Stakeholder satisfaction

**6. Dependencies**

- **Software Design:** Depends on requirements and constraints
- **Project Planning:** Depends on scope, resources, and timeline

---

## Question 6

### 6a) Factors Causing Difficulty in Software Testing (7 marks)

**Factors Causing Testing Difficulties:**

**1. Complexity of Software**

- **Large Scale Systems:** Modern software systems are extremely complex
- **Integration Issues:** Multiple components interact in unpredictable ways
- **Concurrency Problems:** Multi-threaded applications create timing issues
- **Distributed Systems:** Network-based systems have additional failure points

**2. Input Space Explosion**

- **Infinite Input Combinations:** Impossible to test all possible inputs
- **Boundary Conditions:** Edge cases are difficult to identify
- **Data Dependencies:** Complex relationships between input parameters
- **State Space Explosion:** Too many possible system states to test

**3. Requirement-Related Issues**

- **Ambiguous Requirements:** Unclear specifications lead to uncertain test cases
- **Changing Requirements:** Requirements changes invalidate existing tests
- **Missing Requirements:** Incomplete specifications leave gaps in testing
- **Conflicting Requirements:** Contradictory requirements create confusion

**4. Environment Dependencies**

- **Platform Variations:** Different operating systems and hardware
- **Configuration Differences:** Various system configurations to test
- **Third-party Dependencies:** External libraries and services
- **Version Compatibility:** Multiple versions of dependent software

**5. Human Factors**

- **Tester Limitations:** Limited domain knowledge and experience
- **Communication Gaps:** Misunderstanding between developers and testers
- **Cognitive Biases:** Testers may miss obvious defects
- **Time Pressure:** Insufficient time allocated for thorough testing

**6. Technical Challenges**

- **Non-deterministic Behavior:** Random or time-dependent behavior
- **Error Propagation:** Errors may not manifest immediately
- **Resource Constraints:** Limited testing infrastructure and tools
- **Legacy Code:** Poorly documented and structured existing code

**7. Economic Constraints**

- **Budget Limitations:** Insufficient funds for comprehensive testing
- **Time Constraints:** Pressure to release software quickly
- **Resource Allocation:** Limited testing personnel and equipment
- **Cost-Benefit Analysis:** Difficult to justify testing costs

### 6b) Differentiate Between (7 marks)

**i) White Box vs Black Box Testing**

|Aspect|White Box Testing|Black Box Testing|
|---|---|---|
|**Definition**|Testing based on internal code structure|Testing based on external functionality|
|**Knowledge**|Requires knowledge of internal code|No knowledge of internal code required|
|**Focus**|Code coverage and logic paths|Input-output behavior|
|**Tester**|Usually performed by developers|Performed by testers or end users|
|**Techniques**|Statement, branch, path coverage|Equivalence partitioning, boundary value|

**Detailed Comparison:**

**White Box Testing:**

- **Also Known As:** Glass box, structural, clear box testing
- **Purpose:** Verify internal program logic and structure
- **Coverage Criteria:**
    - Statement coverage
    - Branch coverage
    - Path coverage
    - Condition coverage
- **Advantages:**
    - Thorough testing of code logic
    - Early detection of coding errors
    - Optimization opportunities identified
- **Disadvantages:**
    - Time-consuming and expensive
    - Requires programming knowledge
    - May miss missing functionality

**Black Box Testing:**

- **Also Known As:** Functional, behavioral testing
- **Purpose:** Verify system functionality against requirements
- **Test Design:** Based on specifications and requirements
- **Techniques:**
    - Equivalence class partitioning
    - Boundary value analysis
    - Decision table testing
    - State transition testing
- **Advantages:**
    - User perspective testing
    - No programming knowledge required
    - Unbiased testing approach
- **Disadvantages:**
    - Limited coverage of code paths
    - Difficult to identify redundant tests
    - Cannot detect unused code

**ii) Cohesion vs Coupling**

|Aspect|Cohesion|Coupling|
|---|---|---|
|**Definition**|Measure of how closely elements within a module work together|Measure of interdependence between modules|
|**Desirability**|High cohesion is desirable|Low coupling is desirable|
|**Focus**|Internal module relationships|Inter-module relationships|
|**Impact**|Affects module maintainability|Affects system flexibility|
|**Types**|7 types (functional to coincidental)|6 types (data to content)|

**Detailed Comparison:**

**Cohesion Types (Best to Worst):**

1. **Functional Cohesion:** Elements contribute to single well-defined task
2. **Sequential Cohesion:** Output of one element is input to next
3. **Communicational Cohesion:** Elements operate on same data
4. **Procedural Cohesion:** Elements follow specific sequence
5. **Temporal Cohesion:** Elements executed at same time
6. **Logical Cohesion:** Elements perform similar functions
7. **Coincidental Cohesion:** Elements have no meaningful relationship

**Example of High Cohesion:**

```
class Calculator {
    add(a, b)
    subtract(a, b)
    multiply(a, b)
    divide(a, b)
}
// All methods perform arithmetic operations
```

**Coupling Types (Best to Worst):**

1. **Data Coupling:** Modules communicate through parameters
2. **Stamp Coupling:** Modules share composite data structure
3. **Control Coupling:** One module controls another's execution
4. **External Coupling:** Modules share externally imposed format
5. **Common Coupling:** Modules share global data
6. **Content Coupling:** One module modifies another's data

**Example of Low Coupling:**

```
// Module A
result = calculateTax(income, rate)

// Module B  
function calculateTax(income, rate) {
    return income * rate
}
// Modules communicate only through parameters
```

**Impact on Software Quality:**

- **High Cohesion + Low Coupling** = Better maintainability, reusability, and testability
- **Low Cohesion + High Coupling** = Difficult maintenance, poor reusability, complex testing

---

## Question 7

### 7a) Brief Note on Agile Metrics (7 marks)

**Agile Metrics Overview:**

Agile metrics are measurements used to track progress, quality, and team performance in Agile development environments. Unlike traditional metrics, Agile metrics focus on delivering value, team collaboration, and continuous improvement.

**Key Characteristics:**

- **Value-focused:** Measure business value delivery
- **Team-centric:** Focus on team performance and improvement
- **Transparent:** Visible to all stakeholders
- **Actionable:** Provide insights for decision-making
- **Lightweight:** Easy to collect and maintain

**Important Agile Metrics:**

**1. Velocity**

- **Definition:** Amount of work completed in a sprint
- **Measurement:** Story points or user stories completed per sprint
- **Purpose:** Sprint planning and capacity forecasting
- **Calculation:** Sum of story points of completed user stories

**2. Burndown Charts**

- **Sprint Burndown:** Work remaining vs. time in current sprint
- **Release Burndown:** Work remaining vs. time for entire release
- **Purpose:** Track progress and identify potential delays
- **Components:** Ideal line vs. actual progress line

**3. Lead Time and Cycle Time**

- **Lead Time:** Time from request to delivery
- **Cycle Time:** Time from start of work to completion
- **Purpose:** Measure process efficiency and predictability
- **Improvement:** Identify bottlenecks and optimize flow

**4. Cumulative Flow Diagram (CFD)**

- **Purpose:** Visualize work flow through different stages
- **Components:** Shows work in progress across all stages
- **Benefits:** Identify bottlenecks and work distribution

**5. Team Satisfaction and Happiness Index**

- **Measurement:** Regular team surveys and retrospectives
- **Purpose:** Monitor team morale and engagement
- **Indicators:** Team collaboration, motivation, and job satisfaction

**6. Defect Metrics**

- **Defect Discovery Rate:** Bugs found per sprint
- **Defect Resolution Time:** Time to fix reported bugs
- **Escaped Defects:** Bugs found in production
- **Purpose:** Track quality and testing effectiveness

**7. Customer Satisfaction**

- **Net Promoter Score (NPS):** Customer loyalty measurement
- **User Feedback:** Direct customer input and reviews
- **Usage Analytics:** How customers use the product
- **Purpose:** Ensure value delivery to end users

**Benefits of Agile Metrics:**

- **Continuous Improvement:** Data-driven retrospectives
- **Transparency:** Clear visibility into team performance
- **Predictability:** Better estimation and planning
- **Quality Focus:** Early identification of quality issues
- **Value Delivery:** Focus on customer value creation

### 7b) Agile Model Phases, Pros and Cons (7 marks)

**Phases of Agile Model:**

**1. Project Initiation**

- **Activities:** Define project vision and scope
- **Deliverables:** Project charter, initial product backlog
- **Duration:** 1-2 weeks
- **Key Stakeholders:** Product owner, stakeholders, team

**2. Planning Phase**

- **Release Planning:** Define features for each release
- **Sprint Planning:** Plan work for upcoming sprint
- **Estimation:** Story point estimation using planning poker
- **Deliverables:** Release plan, sprint backlog

**3. Development Iterations (Sprints)**

- **Duration:** 1-4 weeks (typically 2 weeks)
- **Activities:**
    - Daily stand-up meetings
    - Development and testing
    - Continuous integration
    - Collaboration and communication
- **Deliverables:** Working software increment

**4. Review and Retrospective**

- **Sprint Review:** Demonstrate completed work to stakeholders
- **Sprint Retrospective:** Team reflects on process improvements
- **Deliverables:** Feedback, improvement actions
- **Duration:** 2-4 hours per sprint

**5. Release and Deployment**

- **Activities:** Deploy working software to production
- **User Training:** Train end users on new features
- **Documentation:** Update user documentation
- **Support:** Provide ongoing support

**6. Monitoring and Maintenance**

- **Performance Monitoring:** Monitor system performance
- **User Feedback:** Collect and analyze user feedback
- **Bug Fixes:** Address production issues
- **Continuous Improvement:** Implement lessons learned

**PROS of Agile Model:**

**1. Customer Satisfaction**

- Frequent delivery of working software
- Customer involvement throughout development
- Quick response to changing requirements

**2. Flexibility and Adaptability**

- Easy to accommodate requirement changes
- Iterative approach allows course correction
- Embraces change rather than resisting it

**3. Quality Improvement**

- Continuous testing and integration
- Regular code reviews and refactoring
- Early defect detection and resolution

**4. Team Collaboration**

- Face-to-face communication
- Self-organizing teams
- Collective ownership and responsibility

**5. Risk Mitigation**

- Early and frequent delivery reduces risks
- Regular feedback identifies issues early
- Incremental development minimizes failure impact

**6. Faster Time to Market**

- Working software delivered in short iterations
- Parallel development and testing
- Reduced documentation overhead

**CONS of Agile Model:**

**1. Documentation Challenges**

- Less emphasis on comprehensive documentation
- May lead to knowledge gaps
- Difficulty in maintenance without proper documentation

**2. Requirement Uncertainty**

- Lack of detailed upfront requirements
- Scope creep due to changing requirements
- Difficulty in estimating total project cost

**3. Team Dependency**

- Requires experienced and skilled team members
- Heavy reliance on team collaboration
- Difficult with distributed teams

**4. Customer Availability**

- Requires active customer participation
- May be challenging if customer is not available
- Decisions may be delayed without customer input

**5. Scalability Issues**

- Difficult to scale for large projects
- Coordination challenges with multiple teams
- May not suit all types of projects

**6. Management Challenges**

- Requires cultural shift in organization
- Traditional managers may find it difficult to adapt
- Requires different project tracking and control methods

---

## Question 8: Brief Notes (14 marks total - 3.5 marks each)

### a) KANBAN (3.5 marks)

**KANBAN Definition:** Kanban is a visual workflow management method that uses cards and boards to visualize work, limit work-in-progress, and maximize efficiency.

**Key Principles:**

1. **Visualize Work:** Use boards with columns representing workflow stages
2. **Limit WIP:** Restrict work-in-progress to prevent bottlenecks
3. **Manage Flow:** Optimize the flow of work through the system
4. **Make Policies Explicit:** Clear rules for moving work between stages
5. **Continuous Improvement:** Regular review and optimization

**Components:**

- **Kanban Board:** Visual representation of workflow
- **Cards:** Represent work items or tasks
- **Columns:** Represent different stages (To Do, In Progress, Done)
- **WIP Limits:** Maximum items allowed in each column

**Benefits:**

- Improved visibility and transparency
- Better resource utilization
- Reduced lead times
- Continuous delivery capability

### b) Code Review (3.5 marks)

**Code Review Definition:** Code review is a systematic examination of source code by one or more developers other than the author to identify defects, improve code quality, and share knowledge.

**Types of Code Reviews:**

1. **Formal Review:** Structured process with defined roles
2. **Walkthrough:** Author presents code to reviewers
3. **Inspection:** Rigorous examination using checklists
4. **Pair Programming:** Real-time collaborative coding

**Process:**

1. Author submits code for review
2. Reviewers examine code for defects and improvements
3. Feedback provided through comments and suggestions
4. Author addresses feedback and updates code
5. Final approval and code integration

**Benefits:**

- Early defect detection (cheaper than testing)
- Knowledge sharing among team members
- Code quality improvement
- Adherence to coding standards
- Reduced maintenance costs

**Best Practices:**

- Review small chunks of code
- Use checklists for common issues
- Focus on logic and design, not style
- Provide constructive feedback

### c) Extreme Programming (XP) (3.5 marks)

**Extreme Programming Definition:** XP is an Agile software development methodology that emphasizes frequent releases, continuous testing, and close collaboration with customers.

**Core Values:**

1. **Communication:** Constant communication among team members
2. **Simplicity:** Do the simplest thing that works
3. **Feedback:** Get feedback early and often
4. **Courage:** Make necessary changes and decisions

**Key Practices:**

1. **Planning Game:** Customer and developers plan releases together
2. **Small Releases:** Frequent delivery of small, functional software
3. **Simple Design:** Keep design simple and clean
4. **Test-Driven Development:** Write tests before code
5. **Pair Programming:** Two developers work together on same code
6. **Collective Code Ownership:** Anyone can change any code
7. **Continuous Integration:** Integrate and test code frequently
8. **Refactoring:** Continuously improve code structure
9. **40-Hour Week:** Maintain sustainable work pace

**Benefits:**

- High-quality software through continuous testing
- Reduced risk through frequent releases
- Improved customer satisfaction
- Better team collaboration

**Challenges:**

- Requires cultural change
- Customer must be actively involved
- May not suit all project types

## d)Object Oriented Design (OOD)

Object Oriented Design is a software design methodology that structures software systems around objects rather than functions and logic. It's a crucial phase in software engineering that translates requirements into a blueprint for implementation.

**Key Concepts:**

**Objects and Classes:** Objects are real-world entities with attributes (data) and methods (behavior). Classes serve as templates or blueprints for creating objects.

**Core Principles:**

- **Encapsulation:** Bundling data and methods together while hiding internal implementation details
- **Inheritance:** Creating new classes based on existing classes, promoting code reuse
- **Polymorphism:** Objects of different types responding to the same interface in their own way
- **Abstraction:** Hiding complex implementation details and showing only essential features

**Design Process:**

1. Identify objects from problem domain
2. Define class relationships and hierarchies
3. Specify object interactions and communication
4. Design class interfaces and method signatures

**Benefits:**

- Enhanced code reusability and maintainability
- Better problem decomposition and modularity
- Easier debugging and testing
- Natural mapping to real-world problems
- Supports incremental development

**Common Design Patterns:**

- Singleton, Factory, Observer, Strategy patterns
- Model-View-Controller (MVC) architecture

**Tools:** UML diagrams (class, sequence, use case) are commonly used to visualize and document OOD.

OOD forms the foundation for object-oriented programming languages like Java, C++, Python, and C#, making it essential for modern software development.