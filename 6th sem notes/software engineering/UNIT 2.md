# Unit II: Software Metrics, Estimation, and Tracking

## 1. Measures, Metrics, and Indicators

### 1.1. Definitions

*   **Measure:** A quantitative indication of the extent, amount, dimension, capacity, or size of some attribute of a product or process. It's a single data point.
    *   *Example:* Number of errors found in a module (e.g., 5 errors).
*   **Metric:** A quantitative measure of the degree to which a system, component, or process possesses a given attribute. It often involves combining one or more measures. Metrics provide context.
    *   *Example:* Defect density (errors per KLOC), calculated from 'number of errors' (measure) and 'lines of code' (measure).
*   **Indicator:** A metric or combination of metrics that provide insight into the software process, a software project, or the product itself. It helps in understanding, controlling, or improving.
    *   *Example:* A rising trend in defect density might *indicate* a problem with development practices or inadequate reviews.

### 1.2. Importance
Measurement is fundamental to any engineering discipline. In software engineering, metrics help to:
*   Characterize (understand current processes/products)
*   Evaluate (assess status against plans)
*   Predict (forecast future outcomes)
*   Improve (identify areas for enhancement)

## 2. Metrics in the Process and Project Domains

### 2.1. Process Metrics
Process metrics are collected across all projects and over long periods. They aim to provide indicators that lead to long-term software process improvement.

#### Top Process Metrics (from PPT):

*   **Cost of Quality (CoQ):**
    *   **Definition:** A measure of the performance of quality initiatives in an organization, expressed in monetary terms. It includes all costs incurred in preventing, detecting, and remediating defects.
    *   **Formula:**
        ```
        CoQ = (Review Effort + Testing Effort + Verification Review Effort + Verification Testing Effort + QA Effort + Configuration Management Effort + Measurement Effort + Training Effort + Rework Review Effort + Rework Testing Effort) / Total Effort * 100
        ```
    *   **Components:**
        *   **Prevention Costs:** Planning, formal technical reviews, training, test equipment.
        *   **Appraisal Costs:** In-process and inter-process inspection, equipment calibration and maintenance, testing.
        *   **Failure Costs:**
            *   **Internal Failure Costs:** Rework, repair, failure mode analysis (before delivery).
            *   **External Failure Costs:** Complaint resolution, product return and replacement, help-line support, warranty work (after delivery).

*   **Cost of Poor Quality (CoPQ):**
    *   **Definition:** The cost associated with implementing imperfect processes and products, specifically the cost of rework and failures.
    *   **Formula:**
        ```
        CoPQ = (Rework Effort) / Total Effort * 100
        ```

*   **Defect Density:**
    *   **Definition:** The number of defects detected in the software during development (or a specific phase) divided by the size of the software (typically in KLOC or FP).
    *   **Formula:**
        ```
        Defect Density = Total Number of Defects / Project Size (in KLOC or FP)
        ```

*   **Review Efficiency:**
    *   **Definition:** The efficiency in harnessing/detecting review defects in the verification stage. It measures how many defects are caught by reviews before testing or release.
    *   **Formula:**
        ```
        Review Efficiency = (Number of Defects Caught in Review / Total Number of Defects Caught Internally) * 100
        ```
        *(Note: "Total number of defects caught" can also refer to all defects caught up to a certain point, including testing.)*

*   **Testing Efficiency:**
    *   **Definition:** A measure of how effective the testing process is at finding defects before the software reaches the customer (acceptance testing).
    *   **Formula (from PPT):**
        ```
        Testing Efficiency = 1 – ((Defects Found in Acceptance) / Total Number of Testing Defects) * 100
        ```
        *(Note: "Total number of testing defects" usually means defects found by the development/test team before acceptance. A more common DRE-like formula for testing would be: (Defects found by internal testing) / (Defects found by internal testing + Defects found by user/customer after delivery) * 100)*

*   **Defect Removal Efficiency (DRE):**
    *   **Definition:** Quantifies the efficiency with which defects were detected and prevented from reaching the customer. Can be calculated for a phase or overall.
    *   **Formula (overall DRE from PPT):**
        ```
        DRE = (1 – (Total Defects Caught by Customer / Total Number of Defects)) * 100
        ```
        Or more commonly:
        ```
        DRE = (Defects found before delivery) / (Defects found before delivery + Defects found after delivery) * 100
        ```

*   **Residual Defect Density:**
    *   **Definition:** The number of defects found by the customer after release, per unit size of the software.
    *   **Formula (from PPT, seems to be a percentage of customer-found defects):**
        ```
        Residual Defect Density = (Total Number of Defects Found by a Customer) / (Total Number of Defects Including Customer Found Defects) * 100
        ```
        *(A more standard definition would be: (Defects Found by Customer) / Size of Software (KLOC or FP))*

### 2.2. Project Metrics
Project metrics enable a software project manager to:
*   Minimize the development schedule by making adjustments to avoid delays and mitigate potential problems.
*   Assess product quality on an ongoing basis and, when necessary, modify the technical approach to improve quality.
*   Track project progress and manage resources.

#### Top Project Metrics (from PPT):

*   **What is a Project Metric?**
    *   Metrics that pertain to project quality.
    *   Used to quantify defects, cost, schedule, productivity, and estimation of various resources and deliverables.

*   **Schedule Variance (SV):**
    *   **Definition:** Any difference between the scheduled completion of an activity (or project) and the actual completion. It helps determine if you are ahead of or behind schedule.
    *   **Formulas (from PPT 1):**
        1.  General percentage form:
            ```
            SV = ((Actual Calendar Days – Planned Calendar Days) + Start Variance) / Planned Calendar Days * 100
            ```
            (*"Start Variance" here likely refers to any initial delay in starting the project/activity, measured in days.*)
        2.  **Earned Value Management (EVM) based SV (More Common):**
            *   `SV = EV – PV`
            *   **Planned Value (PV):** The budgeted cost of work scheduled. What you planned to have accomplished (and spent) by a certain date.
                *   `PV = (Planned % Complete) x (BAC)`
            *   **Earned Value (EV):** The budgeted cost of work performed. The value of the work actually completed.
                *   `EV = (% of Completed Work) x (BAC)`
            *   **Budget at Completion (BAC):** The total anticipated budget for the project.
            *   **Actual Cost (AC):** The actual cost incurred for the work performed. (Not directly in SV, but part of Cost Variance: CV = EV - AC)
            *   **Interpretation:**
                *   SV > 0: Ahead of schedule.
                *   SV = 0: On schedule.
                *   SV < 0: Behind schedule.
        3.  Alternative terms (EVM):
            *   `SV = BCWP – BCWS`
            *   **BCWP (Budgeted Cost of Work Performed):** Same as EV.
            *   **BCWS (Budgeted Cost of Work Scheduled):** Same as PV.

    *   **Schedule Variance for a Phase:**
        *   **Definition:** The deviation between planned and actual schedules for a specific phase within a project.
        *   **Formula (from PPT):**
            ```
            SV(phase) = (Actual Calendar Days for Phase - Planned Calendar Days for Phase + Start Variance for Phase) / (Planned Calendar Days for Phase) * 100
            ```

    *   **Example of EVM Schedule Variance (from PPT):**
        *   Planned project length: 6 months
        *   Time worked to date: 3 months
        *   Project cost (BAC): $120,000
        *   Actual cost (AC): $55,000 (Not used for SV calculation, but good for context)
        *   Planned percent of project complete: 50%
        *   Actual percent of project complete: 35%

        *   **PV Calculation:**
            `PV = Planned % Complete * BAC = 0.50 * $120,000 = $60,000`
        *   **EV Calculation:**
            `EV = Actual % Complete * BAC = 0.35 * $120,000 = $42,000`
        *   **SV Calculation:**
            `SV = EV - PV = $42,000 - $60,000 = -$18,000`
            *Result: The project is $18,000 worth of work behind schedule.*
        *   **SV as a percentage (of planned progress):**
            `SV% = SV / PV = -$18,000 / $60,000 = -0.30 = -30%`
            *Result: The project is 30% behind schedule in terms of value.*

    *   **Benefits of Calculating Schedule Variance:**
        1.  Getting an Accurate View of a Project’s Progress
        2.  Monitoring Costs (indirectly, by comparing planned vs. actual work value)
        3.  Managing Stakeholder Expectations

*   **Effort Variance (EV):** (Note: PPT uses EV for Effort Variance, which conflicts with Earned Value. Context is key. Let's use EffortVar for clarity here.)
    *   **Definition:** Difference between the planned outlined efforts and the effort required to actually undertake the task.
    *   **Formula:**
        ```
        EffortVar = (Actual Effort – Planned Effort) / Planned Effort * 100
        ```

*   **Effort Variance for a Phase:**
    *   **Formula:**
        ```
        EffortVar(phase) = (Actual Effort for Phase – Planned Effort for Phase) / Planned Effort for Phase * 100
        ```

*   **Size Variance:**
    *   **Definition:** Difference between the estimated size of the project and the actual size of the project (normally KLOC or FP).
    *   **Formula:**
        ```
        Size Variance = (Actual Size – Estimated Size) / Estimated Size * 100
        ```

*   **Requirement Stability Index (RSI):**
    *   **Definition:** Provides visibility to the magnitude and impact of requirement changes.
    *   **Formula:**
        ```
        RSI = (1 - ((Number of Changed Requirements + Number of Deleted Requirements + Number of Added Requirements) / Total Number of Initial Requirements)) * 100
        ```
        *(Note: A higher RSI indicates more stability. If there are many changes, the term in the parenthesis becomes larger, (1 - large_term) becomes smaller or negative, then *100. A more intuitive formula might be: `RSI = (Total Initial Requirements - (Changed + Deleted + Added)) / Total Initial Requirements * 100`. However, the PPT formula implies (1 - (proportion of change)) * 100. If (Changed+Deleted+Added) > Initial, RSI becomes negative, indicating massive scope creep.)*
        A more common way to express this is Total Changes / Initial Requirements. The PPT formula aims to show percentage *stability*. So if 0 changes, RSI = (1-0)*100 = 100%. If Initial = 100, Changed=10, Deleted=5, Added=5, then (1 - (10+5+5)/100)*100 = (1 - 0.2)*100 = 80% stable.

*   **Productivity Metrics:**
    *   **Definition (General):** A measure of output from a related process for a unit of input.
    *   **Productivity (Project):**
        ```
        Project Productivity = Actual Project Size (KLOC or FP) / Actual Effort Expended (person-months)
        ```
    *   **Productivity (for Test Case Preparation):**
        ```
        Productivity_TestCasePrep = Actual Number of Test Cases / Actual Effort Expended in Test Case Preparation
        ```
    *   **Productivity (for Test Case Execution):**
        ```
        Productivity_TestCaseExec = Actual Number of Test Cases Executed / Actual Effort Expended in Testing
        ```
    *   **Productivity (Defect Detection):**
        ```
        Productivity_DefectDetection = Actual Number of Defects (Review + Testing) / Actual Effort Spent on (Review + Testing)
        ```
    *   **Productivity (Defect Fixation):**
        ```
        Productivity_DefectFixation = Actual Number of Defects Fixed / Actual Effort Spent on Defect Fixation
        ```

## 3. Software Measurement
Software measurement is the process of assigning a numeric value or symbol to an attribute of a software product or process through a defined procedure. It can be categorized into:
*   **Direct Measures:** Attributes that can be measured directly (e.g., cost, effort, LOC, speed, memory size, defects reported).
*   **Indirect Measures:** Attributes that are measured in terms of their effect on other attributes (e.g., quality, complexity, efficiency, reliability, maintainability). Function Points are an indirect measure of size.

## 4. Metrics of Software Quality

Quality metrics focus on the characteristics of the software product itself and the process used to develop it.
Key quality aspects and their potential metrics:

*   **Correctness:** Freedom from defects.
    *   *Metrics:* Defect Density, Defects per KLOC, Defects found during testing/reviews.
*   **Reliability:** The probability of failure-free operation for a specified time in a specified environment.
    *   *Metrics:* Mean Time Between Failure (MTBF), Mean Time To Failure (MTTF), Availability (see section on S/W Reliability).
*   **Efficiency:** The relationship between the performance level and the amount of resources used.
    *   *Metrics:* Response time, throughput, CPU utilization, memory usage.
*   **Maintainability:** The ease with which a software system can be modified to correct faults, improve performance, or adapt to a changed environment.
    *   *Metrics:* Mean Time To Repair (MTTR), Cyclomatic Complexity, Cohesion, Coupling, Lines of Code per module.
*   **Usability:** The ease with which users can learn, operate, and prepare inputs/outputs for a system.
    *   *Metrics:* Task completion time, error rates during use, user satisfaction scores.
*   **Portability:** The ease with which software can be transferred from one hardware or software environment to another.
    *   *Metrics:* Number of platform-dependent modules/LOC.
*   **Testability:** The effort required to test a program to ensure it performs its intended function.
    *   *Metrics:* Test coverage, number of test cases.

(Also see Process Metrics like CoQ, CoPQ, DRE, Review Efficiency, Testing Efficiency as they indirectly reflect quality.)

## 5. S/W Reliability

Software reliability is the probability that software will operate without failure for a specified period under specified conditions.

### 5.1. Key Reliability Metrics

*   **Mean Time To Failure (MTTF):** The average time the system operates correctly before a failure occurs.
    *   Primarily used for systems that cannot be repaired or where repair time is negligible.
*   **Mean Time To Repair (MTTR):** The average time taken to repair a system after a failure.
    *   Includes time for diagnosis, repair, and re-testing.
*   **Mean Time Between Failures (MTBF):** The average time between consecutive failures.
    *   `MTBF = MTTF + MTTR`
    *   For systems that are repaired and put back into operation.
*   **Availability:** The probability that the system is operational and accessible when required for use.
    *   `Availability = MTTF / (MTTF + MTTR) * 100%`
    *   Or `Availability = MTBF_system_uptime / (MTBF_system_uptime + MTTR_system_downtime) * 100%`
*   **Failure Rate (λ):** The frequency with which a system or component fails, expressed in failures per unit of time.
    *   `λ = 1 / MTTF` (for constant failure rate period)

### 5.2. Software Reliability Models
These are mathematical models used to predict or estimate software reliability.
*   **Reliability Growth Models:** Assume reliability improves over time as defects are found and fixed (e.g., Jelinski-Moranda, Musa Basic Execution Time Model, Goel-Okumoto Non-Homogeneous Poisson Process Model).
*   **Static Models:** Use code attributes (e.g., complexity, size) to predict reliability.

## 6. Software Estimation Techniques

Software estimation involves predicting the effort, cost, time, and resources required to develop a software system.

### 6.1. Project Size Estimation
Accurate estimation of project size is central to estimating all other project parameters (effort, cost, time).

*   **Meaning of "Project Size":** Not just bytes or executable size, but a measure of the problem complexity in terms of effort and time required to develop the product.

### 6.2. Lines of Code (LOC) Estimation

*   **Definition:** Measures the size of a project by counting the number of source instructions in the developed program. Comment lines and header lines are typically ignored.
*   **Estimation Process (Systematic Guessing):**
    1.  Divide the problem into modules.
    2.  Divide modules into sub-modules, and so on, until leaf-level modules are small enough to be predicted.
    3.  Estimate LOC for each leaf-level module (often based on past experience with similar modules).
    4.  Sum the estimates for all leaf-level modules to get the total size estimation.
*   **Shortcomings of LOC:**
    1.  **Coding Activity Alone:** Ignores design, testing, and other efforts which can be disproportionate to coding.
    2.  **Language Dependent:** The LOC count for the same functionality varies significantly between different programming languages.
    3.  **Instruction Choice Dependent:** Different programmers can produce different LOC counts for the same problem and language due to varying coding styles.
    4.  **Poor Correlation with Quality/Efficiency:** Larger LOC does not imply better quality or efficiency. Can encourage verbose, inefficient code.
    5.  **Penalizes Higher-Level Languages & Reuse:** Using libraries or higher-level languages results in lower LOC, which might be wrongly interpreted as lower effort or productivity. Discourages code reuse if productivity is measured as LOC/person-month.
    6.  **Measures Lexical Complexity:** Does not address logical or structural complexity effectively.
    7.  **Difficult to Estimate Accurately Early:** Precise LOC can only be known after development. Early estimates are guesses.

### 6.3. Function Point (FP) Estimation

Proposed by Albrecht (IBM) in 1979/1983 to overcome LOC shortcomings.

*   **Concept:** Software size is directly dependent on the number and complexity of different high-level functions or features it supports. It measures functionality from the user's perspective.
*   **Advantages over LOC:**
    *   Language independent.
    *   Can be estimated earlier in the lifecycle, from requirements specifications.
*   **Basic Parameters (Information Domain Values):**
    1.  **External Inputs (EI):** Data crossing the boundary from outside to inside. Each unique user data or control input type that enters the external boundary of the application. (Group related inputs).
    2.  **External Outputs (EO):** Data passing from inside to outside the application boundary. Each unique user data or control output type that leaves the external boundary. (Group related outputs).
    3.  **External Inquiries (EQ):** An input/output combination where an input causes an immediate output, with no processing or file updates. Each unique input/output combination where an input causes and generates an immediate output.
    4.  **Internal Logical Files (ILF):** User-identifiable groups of logically related data that reside entirely within the application boundary and are maintained through EIs.
    5.  **External Interface Files (EIF):** User-identifiable groups of logically related data that are used for reference purposes only, reside outside the application, and are maintained by another application.

#### FP Computation Steps:

**Step 1: Compute Unadjusted Function Points (UFP)**
Count each of the five parameters. Classify each count as Simple, Average, or Complex. Use weighting factors (standard weights often used if complexity not assessed at this stage, or use a table like below from PPT):

| Parameter          | Simple | Average | Complex |
| ------------------ | ------ | ------- | ------- |
| External Inputs (EI) | 3      | 4       | 6       |
| External Outputs (EO)| 4      | 5       | 7       |
| External Inquiries(EQ)| 3      | 4       | 6       |
| Internal Logical Files (ILF)| 7    | 10      | 15      |
| External Interface Files (EIF)| 5  | 7       | 10      |

*   **UFP Formula (using average weights if complexity isn't detailed yet, as in one PPT example):**
    `UFP = (Number of EIs * 4) + (Number of EOs * 5) + (Number of EQs * 4) + (Number of ILFs * 10) + (Number of EIFs * 7 or 10)`
    *(Note: PPT slide 32 of Project Size Estimation uses 10 for EIF, slide 42 uses 7 for average EIF. Standard IFPUG uses 7 for average EIF, 5 for simple, 10 for complex).*
    Let's assume you will be given the weights or complexity matrix.

**Step 2: Compute the Value Adjustment Factor (VAF) / Technical Complexity Factor (TCF)**
This factor adjusts the UFP based on 14 General System Characteristics (GSCs). Each GSC is rated on a scale of 0 (no influence) to 5 (strong influence).

*   **General System Characteristics (GSCs) - Examples:**
    1.  Data communications
    2.  Distributed data processing
    3.  Performance
    4.  Heavily used configuration
    5.  Transaction rate
    6.  Online data entry
    7.  End-user efficiency
    8.  Online update
    9.  Complex processing
    10. Reusability
    11. Installation ease
    12. Operational ease
    13. Multiple sites
    14. Facilitate change

*   **Calculate Total Degree of Influence (DI or TDI):** Sum the ratings (0-5) for all 14 GSCs. `DI = Σ(fi)` (where fi is the rating for the i-th GSC). Max DI = 14 * 5 = 70.
*   **Calculate VAF (or TCF):**
    `VAF = (DI * 0.01) + 0.65`
    Or `TCF = 0.65 + (0.01 * DI)`
    The VAF ranges from 0.65 (DI=0) to 1.35 (DI=70).

**Step 3: Compute Final Function Points (FP)**
`FP = UFP * VAF` (or `FP = UFP * TCF`)

**Alternative FP Calculation Flow (seen in some PPT slides, possibly simplified for a specific context):**
1.  `F = 14 * scale` (where 'scale' is an overall complexity assessment from 0-5, e.g., 3 for average). This 'F' seems to be a proxy for DI.
2.  `CAF = 0.65 + (0.01 * F)` (CAF here is VAF/TCF)
3.  Count UFP using a complexity matrix (Simple, Average, Complex) for EIs, EOs, EQs, ILFs, EIFs.
4.  `FP = UFP * CAF`

#### FP Numerical Examples:

**Example 1 (Supermarket Software from PPT - Project Size Est. slide 60-63):**
*   Problem: Develop supermarket software. Customers register, purchase, get CN. Awards for high purchases.
*   Parameter Identification:
    *   Inputs: 3 (customer details for registration, purchase details, year-end processing trigger)
    *   Outputs: 2 (CN displayed, annual award list)
    *   Inquiries: 1 (clerk presenting card to check out staff - implies a query to validate CN or credit purchase)
    *   ILFs: 2 (customer details file, daily purchase records file)
    *   EIFs: 0
*   **Step 1: UFP Calculation (Initial - assuming average complexity from formula on slide 32)**
    `UFP = (3 * 4) + (2 * 5) + (1 * 4) + (2 * 10) + (0 * 10) = 12 + 10 + 4 + 20 + 0 = 46`
*   **Step 1 Refined (UFP with complexity adjustment - slide 62):**
    *   Assume all parameters moderate (average weights) except one output (CN display) is simple.
    *   Moderate EIs: 3 * 4 = 12
    *   Outputs: 1 simple (CN) * 4 (simple weight) = 4; 1 moderate (award list) * 5 (avg weight) = 5. Total EO value = 9.
        *(Slide 62 has a slightly different interpretation: UFP = 3*4 (EI) + 1*5 (Output-moderate) + 1*4 (Output-simple, which is odd if there are only 2 total outputs, should be one *each* complexity, or sum counts for each complexity level). Let's re-evaluate as per standard method:
        EI: 3 moderate = 3 * 4 = 12
        EO: 1 simple = 1 * 4 = 4; 1 moderate = 1 * 5 = 5. Total EO count = 2, weighted sum = 9
        EQ: 1 moderate = 1 * 4 = 4
        ILF: 2 moderate = 2 * 10 = 20
        EIF: 0
        Refined UFP = 12 + 9 + 4 + 20 + 0 = 45*
        The slide 62 equation `UFP = 3×4 + 1×5 +1×4 + 1×4 + 10×2 + 0×10 = 45` seems to be mixing counts and weights in a non-standard way. It looks like: 3 EIs (avg), 1 EO (avg), 1 EQ (avg), **1 ILF (avg)**, **1 ILF (avg)**, 0 EIF. This sums to 45. Let's use their UFP=45.
*   **Step 2: VAF/TCF Calculation**
    *   Assume "various project characteristics determining the complexity ... to be average."
    *   Average rating for each of 14 GSCs = 3 (as per example on slide 65 where F=14*scale, scale=3 for avg).
    *   `DI = 14 * 3 = 42` (Slide 63 says 14*4=56 for "average values", this is a discrepancy. Let's use their 56 for this example).
    *   `TCF = 0.65 + (0.01 * DI) = 0.65 + (0.01 * 56) = 0.65 + 0.56 = 1.21`
*   **Step 3: Final FP**
    *   `FP = UFP * TCF = 45 * 1.21 = 54.45 FP`

**Example 2 (Given values, all average complexity - Project Size Est. slide 65-67):**
*   User Input = 50, User Output = 40, User Inquiries = 35, User Files = 6, External Interface = 4.
*   Weighting factors are average. Complexity adjustment factors (GSCs) are average.
*   **Step 1: VAF/TCF (called CAF here)**
    *   Average GSC rating means scale = 3.
    *   `F (proxy for DI) = 14 * scale = 14 * 3 = 42`
    *   `CAF = 0.65 + (0.01 * F) = 0.65 + (0.01 * 42) = 0.65 + 0.42 = 1.07`
*   **Step 2: UFP (using average weights from table on slide 42/58)**
    *   EI: 50 * 4 (avg) = 200
    *   EO: 40 * 5 (avg) = 200
    *   EQ: 35 * 4 (avg) = 140
    *   ILF: 6 * 10 (avg) = 60
    *   EIF: 4 * 7 (avg) = 28
    *   `UFP = 200 + 200 + 140 + 60 + 28 = 628`
*   **Step 3: Final FP**
    *   `FP = UFP * CAF = 628 * 1.07 = 671.96 FP`

**Example 3 (Given counts, specific GSC ratings - Project Size Est. slide 69-71):**
*   EI=24, EO=46, EQ=8, ILF=4, EIF=2
*   Effort = 36.9 p-m, Tech_docs = 265 pages, User_docs = 122 pages, Cost = $7744/month
*   GSC ratings (fi): 4, 1, 0, 3, 3, 5, 4, 4, 3, 3, 2, 2, 4, 5
*   **Step 1: UFP (assuming average weights as GSC ratings are separate)**
    *   EI: 24 * 4 = 96
    *   EO: 46 * 5 = 230 (Slide 70 shows 46*4=184, implying EO weight is 4. This means EO complexity is considered simple. Let's use the slide's table)
        *Correction based on slide 70 weighing factor column:*
        EI: 24 * 4 = 96
        EO: 46 * 4 = 184  (Weight suggests these are treated as 'simple' or a specific assigned weight)
        EQ: 8 * 6 = 48    (Weight suggests 'complex')
        ILF: 4 * 10 = 40  (Weight suggests 'average')
        EIF: 2 * 5 = 10   (Weight suggests 'simple')
        `UFP (Count-total from slide) = 96 + 184 + 48 + 40 + 10 = 378`
*   **Step 2: VAF/TCF**
    *   `DI = Σ(fi) = 4+1+0+3+3+5+4+4+3+3+2+2+4+5 = 43`
    *   `VAF = 0.65 + (0.01 * DI) = 0.65 + (0.01 * 43) = 0.65 + 0.43 = 1.08`
*   **Step 3: Final FP**
    *   `FP = UFP * VAF = 378 * 1.08 = 408.24 FP` (Slide shows 408)
*   **Other Calculations:**
    *   Productivity = FP / Effort = 408 / 36.9 = 11.05 FP/p-m (Slide 11.1)
    *   Total Pages of Documentation = Tech_docs + User_docs = 265 + 122 = 387 pages
    *   Documentation = Total Pages / FP = 387 / 408 = 0.948 pages/FP
    *   Cost per Function = (Cost/Month * Effort_Months) / FP (This is total cost / FP)
        Or, if Cost = $7744/month *is* the total project cost (unlikely if effort is 36.9 p-m), then Cost/FP.
        More likely: Cost per Function = (Total Cost) / FP. Total Cost = Effort * Cost_per_p-m.
        Productivity = 11.1 FP/p-m. Cost = $7744/month.
        Cost per FP = Cost_per_p-m / Productivity_FP_per_p-m = $7744 / 11.1 = $697.65 per FP.
        The slide calculates: Cost per Function = Cost / Productivity = $7744 / 11.1 = $700 (approx). This assumes $7744 is the cost per some unit that relates to 11.1 productivity units. It's likely ($/PM) / (FP/PM) = $/FP.

**Example 4 (Given counts with complexities - Project Size Est. slide 73-74):**
*   EI (Avg): 22 => 22 * 4 = 88
*   EO (Low/Simple): 45 => 45 * 4 = 180
*   EQ (High/Complex): 06 => 06 * 6 = 36
*   ILF (Avg): 05 => 05 * 10 = 50
*   EIF (Low/Simple): 02 => 02 * 5 = 10 (Slide 74 has 02*5, IFPUG EIF simple is 5)
    *   `UFP (Total Count Factor TC from slide) = 88 + 180 + 36 + 50 + 10 = 364`
    *   (Slide 74 calculations: (22\*4)+(45\*5)+(06\*6)+(05\*10)+(02\*5) = 88+225+36+50+10 = 409. It used EO(Low) with weight 5, which is Average for EO, not Low. Let's follow slide's UFP of 409).
*   GSC ratings (Xi): 5,1,0,4,3,5,4,3,4,5,2,3,4,2
*   **Step 1: VAF/TCF**
    *   `DI = Σ(Xi) = 5+1+0+4+3+5+4+3+4+5+2+3+4+2 = 45`
    *   `VAF = 0.65 + (0.01 * DI) = 0.65 + (0.01 * 45) = 0.65 + 0.45 = 1.10`
*   **Step 2: Final FP**
    *   `FP = UFP * VAF = 409 * 1.10 = 449.9 FP` (Slide shows 450)

#### FP Shortcomings:
*   **Subjectivity:**
    *   Identifying and classifying EIs, EOs, EQs, ILFs, EIFs can be subjective.
    *   Rating GSCs (0-5) is subjective.
    *   Grouping input/output data items can be subjective.
*   **Algorithmic Complexity:** Does not directly account for the algorithmic complexity of a function. A complex algorithm might have few I/O but require significant effort. (Feature Points attempt to address this by adding an "Algorithm" parameter).
*   **Focus on Transactional Systems:** Better suited for information processing systems rather than computationally intensive or real-time systems.

#### Backfiring
Process of converting FP to LOC or vice-versa. Requires historical data for specific languages/environments.
*Example:* 1 FP ≈ 100 lines of COBOL code (this is a rough average, actuals vary).

## 7. Empirical Models like COCOMO

Empirical estimation models are based on historical data and statistical analysis. COCOMO (Constructive Cost Model) by Barry Boehm is one of the most well-known.

### 7.1. COCOMO Overview
*   Predicts effort (in Person-Months) and development time (in Months).
*   Based on project size (KLOC - Thousand Lines of Code).
*   Three levels of COCOMO:
    1.  **Basic COCOMO:** Good for quick, early, rough estimates.
    2.  **Intermediate COCOMO:** Considers 15 "cost drivers" to refine estimates.
    3.  **Detailed COCOMO:** Phase-sensitive effort multipliers.

### 7.2. COCOMO Project Modes
COCOMO categorizes projects into three modes based on team experience, project complexity, and development environment:

1.  **Organic Mode:**
    *   Relatively small, simple projects.
    *   Small, experienced teams.
    *   Familiar development environment.
    *   Less rigid requirements.
    *   *Example:* Simple data processing, small inventory system.

2.  **Semi-Detached Mode:**
    *   Intermediate size and complexity.
    *   Mixed team experience (some experienced, some less so).
    *   Requirements may be a mix of rigid and less defined.
    *   *Example:* Utility programs, database systems, moderately complex OS components.

3.  **Embedded Mode:**
    *   Complex projects with tight constraints (hardware, software, operational).
    *   Team may be less familiar with aspects of the system.
    *   Very rigid requirements and interfaces.
    *   High need for innovation.
    *   *Example:* Real-time systems, avionics, complex OS.

### 7.3. Basic COCOMO Formulas

*   **Effort (E) in Person-Months (PM):**
    `E = a * (KLOC) ^ b`
*   **Development Time (TDEV) in Months (M):**
    `TDEV = c * (E) ^ d`
*   **Average Staffing (S):**
    `S = E / TDEV` (persons)

**Coefficients for Basic COCOMO:**

| Project Mode  | `a`  | `b`  | `c`  | `d`  |
| ------------- | ---- | ---- | ---- | ---- |
| Organic       | 2.4  | 1.05 | 2.5  | 0.38 |
| Semi-Detached | 3.0  | 1.12 | 2.5  | 0.35 |
| Embedded      | 3.6  | 1.20 | 2.5  | 0.32 |

#### Basic COCOMO Numerical Examples:

**Assume a project is estimated to be 30 KLOC.**

1.  **Organic Mode Calculation:**
    *   `E = 2.4 * (30) ^ 1.05 = 2.4 * 34.96 ≈ 83.9 PM`
    *   `TDEV = 2.5 * (83.9) ^ 0.38 = 2.5 * 5.78 ≈ 14.45 M`
    *   `S = 83.9 / 14.45 ≈ 5.8 persons`

2.  **Semi-Detached Mode Calculation:**
    *   `E = 3.0 * (30) ^ 1.12 = 3.0 * 45.46 ≈ 136.38 PM`
    *   `TDEV = 2.5 * (136.38) ^ 0.35 = 2.5 * 5.82 ≈ 14.55 M`
    *   `S = 136.38 / 14.55 ≈ 9.37 persons`

3.  **Embedded Mode Calculation:**
    *   `E = 3.6 * (30) ^ 1.20 = 3.6 * 61.48 ≈ 221.33 PM`
    *   `TDEV = 2.5 * (221.33) ^ 0.32 = 2.5 * 5.68 ≈ 14.2 M`
    *   `S = 221.33 / 14.2 ≈ 15.58 persons`

### 7.4. Intermediate COCOMO
*   Refines Basic COCOMO estimates using 15 cost drivers related to:
    *   **Product Attributes:** Required reliability (RELY), Database size (DATA), Product complexity (CPLX).
    *   **Hardware Attributes:** Execution
## 7.4. Intermediate COCOMO (Continued)
*   Refines Basic COCOMO estimates using 15 cost drivers related to:
    *   **Product Attributes:** Required reliability (RELY), Database size (DATA), Product complexity (CPLX).
    *   **Hardware Attributes:** Execution time constraint (TIME), Main storage constraint (STOR), Virtual machine volatility (VIRT), Computer turnaround time (TURN).
    *   **Personnel Attributes:** Analyst capability (ACAP), Applications experience (AEXP), Programmer capability (PCAP), Virtual machine experience (VEXP), Programming language experience (LEXP).
    *   **Project Attributes:** Modern programming practices (MODP), Use of software tools (TOOL), Required development schedule (SCED).
*   Each cost driver is rated on a scale (e.g., Very Low, Low, Nominal, High, Very High, Extra High). Each rating has a corresponding effort multiplier value.
*   **Effort Adjustment Factor (EAF):** The product of all 15 cost driver multipliers.
    `EAF = M1 * M2 * ... * M15`
*   **Intermediate COCOMO Effort Formula:**
    `E = a * (KLOC) ^ b * EAF`
    (The coefficients `a` and `b` are slightly different for Intermediate COCOMO compared to Basic, specific to the mode).

**Coefficients for Intermediate COCOMO Nominal Effort:**

| Project Mode  | `a_i`| `b_i`|
| ------------- | -----| -----|
| Organic       | 3.2  | 1.05 |
| Semi-Detached | 3.0  | 1.12 |
| Embedded      | 2.8  | 1.20 |

*   **Development Time (TDEV) for Intermediate COCOMO:**
    `TDEV = c * (E) ^ d` (uses the *adjusted* Effort `E`, and the `c` and `d` coefficients are the same as Basic COCOMO for the respective mode).

#### Intermediate COCOMO Numerical Example:

Suppose we have a 100 KLOC project, determined to be **Semi-Detached**.
*   Initial Nominal Effort: `E_nominal = 3.0 * (100) ^ 1.12 = 3.0 * 177.83 ≈ 533.5 PM`

Now, let's assume the following cost driver ratings and their (hypothetical) multipliers (actual multipliers are found in COCOMO tables):

| Cost Driver | Rating    | Multiplier |
| ----------- | --------- | ---------- |
| RELY        | High      | 1.15       |
| DATA        | High      | 1.08       |
| CPLX        | Very High | 1.30       |
| TIME        | Nominal   | 1.00       |
| STOR        | High      | 1.06       |
| VIRT        | Low       | 0.87       |
| TURN        | Low       | 0.87       |
| ACAP        | High      | 0.86       |
| AEXP        | Nominal   | 1.00       |
| PCAP        | High      | 0.86       |
| VEXP        | Low       | 0.90       |
| LEXP        | Nominal   | 1.00       |
| MODP        | High      | 0.91       |
| TOOL        | High      | 0.91       |
| SCED        | Nominal   | 1.00       |

*   **Calculate EAF:**
    `EAF = 1.15 * 1.08 * 1.30 * 1.00 * 1.06 * 0.87 * 0.87 * 0.86 * 1.00 * 0.86 * 0.90 * 1.00 * 0.91 * 0.91 * 1.00`
    `EAF ≈ 0.83` (This is a sample calculation; ensure you multiply all 15 correctly).

*   **Calculate Adjusted Effort:**
    `E_adjusted = E_nominal * EAF = 533.5 PM * 0.83 ≈ 442.8 PM`

*   **Calculate Development Time (TDEV) for Semi-Detached (c=2.5, d=0.35):**
    `TDEV = 2.5 * (442.8) ^ 0.35 = 2.5 * 7.98 ≈ 19.95 Months`

### 7.5. COCOMO II
*   A successor to COCOMO 81, designed to address modern software development practices (e.g., object-oriented approaches, reuse, COTS integration).
*   Includes models for:
    *   **Application Composition Model:** Used during early stages when prototyping or UI development is dominant. Uses Object Points (similar to FPs but for GUIs, reports, 3GL components).
    *   **Early Design Model:** Used after requirements are stabilized and basic architecture is known. Uses Unadjusted Function Points (UFP) and 7 coarse-grained cost drivers.
    *   **Post-Architecture Model:** Used when the system architecture is well-defined. Uses KSLOC (Source Lines of Code), and 17 cost drivers. This is the most detailed model in COCOMO II.

COCOMO II is more complex and generally requires specialized tools for effective use.

## 8. Project Tracking and Scheduling

### 8.1. Project Tracking
Project tracking involves monitoring the progress of a project against its plan. It helps in:
*   Identifying deviations from the schedule, budget, and scope.
*   Taking corrective actions.
*   Reporting status to stakeholders.
*   Key tracking activities:
    *   Monitoring milestones.
    *   Tracking effort spent.
    *   Tracking costs incurred.
    *   Monitoring defect rates.
    *   Using Earned Value Management (EVM) - see Schedule Variance section.

### 8.2. Project Scheduling
Project scheduling is the process of defining project activities, sequencing them, estimating their duration, and allocating resources to them.
*   **Work Breakdown Structure (WBS):** Hierarchical decomposition of the total scope of work to be carried out by the project team.
*   **Activity Definition:** Identifying the specific actions to be performed to produce the project deliverables.
*   **Activity Sequencing:** Identifying and documenting relationships among project activities (e.g., using PERT/CPM).
    *   **PERT (Program Evaluation and Review Technique):** Uses probabilistic time estimates (optimistic, most likely, pessimistic).
    *   **CPM (Critical Path Method):** Determines the longest path of activities (critical path), which dictates the shortest project duration. Activities on the critical path have zero slack/float.
*   **Resource Allocation:** Assigning resources (people, equipment, materials) to activities.
*   **Duration Estimation:** Estimating the number of work periods needed to complete individual activities.
*   **Schedule Development Tools:** Gantt charts, PERT charts, network diagrams.

#### Gantt Charts:
*   Bar charts that illustrate a project schedule.
*   List activities on the vertical axis and time on the horizontal axis.
*   Show start and end dates, durations, and sometimes dependencies and resources.

#### PERT/CPM Network Diagrams:
*   Graphical representation of project activities and their dependencies.
*   Nodes represent activities or events, and arrows represent dependencies or durations.
*   Help identify the critical path.

## 9. Reverse Engineering

### 9.1. Definition
Reverse engineering is the process of analyzing a subject system (software, hardware, or product) to:
*   Identify the system's components and their interrelationships.
*   Create representations of the system in another form or at a higher level of abstraction.
*   Understand its design and functionality, often when original documentation is missing or outdated.

It does **not** involve changing the system or creating a new system based on the reverse-engineered model (that would be re-engineering).

### 9.2. Goals of Reverse Engineering
*   **Cope with Complexity:** Understand large, complex legacy systems.
*   **Generate Alternate Views:** Create different abstractions of the system (e.g., data flow diagrams, control flow graphs from code).
*   **Recover Lost Information:** Recreate design specifications or documentation.
*   **Detect Side Effects:** Identify unintended consequences of system operations.
*   **Facilitate Reuse:** Identify components that can be reused in new systems.
*   **Improve Maintainability:** Provide insights that help in modifying and maintaining the system.
*   **Migration/Re-platforming:** Understand a system before migrating it to a new platform.

### 9.3. Reverse Engineering Process
Typically involves:
1.  **Information Gathering:** Collecting all available artifacts (source code, executables, existing documentation, database schemas, user manuals).
2.  **System Analysis:**
    *   **Static Analysis:** Analyzing the system without executing it (e.g., parsing source code, analyzing data structures, control flow analysis).
    *   **Dynamic Analysis:** Analyzing the system while it is executing (e.g., tracing execution paths, monitoring function calls, performance profiling).
3.  **Model Generation:** Creating abstract representations (e.g., UML diagrams, flowcharts, data models).
4.  **Understanding and Documentation:** Interpreting the generated models and documenting the findings.

### 9.4. Levels of Abstraction in Reverse Engineering
*   **Source Code Level:** Analyzing syntax, structure, data types, control flow within the code.
*   **Design Level:** Abstracting design elements like module structures, component interactions, architectural patterns.
*   **Requirements Level:** (Most difficult) Attempting to infer the original functional and non-functional requirements the system was built to satisfy.

### 9.5. Tools for Reverse Engineering
*   **Disassemblers/Decompilers:** Convert machine code or bytecode back into a higher-level language (often assembly or a C-like representation).
*   **Static Analysis Tools:** Parse source code to extract structural information, metrics, call graphs, etc. (e.g., Understand, SonarQube).
*   **Dynamic Analysis Tools:** Profilers, debuggers, tracers.
*   **Modeling Tools:** UML modeling tools that can import code or database schemas to generate diagrams.

### 9.6. Challenges
*   **Incomplete Information:** Source code or full system access may not be available.
*   **Complexity of Legacy Systems:** Often large, poorly structured, and undocumented.
*   **Language Obscurity:** Dealing with old or proprietary programming languages.
*   **Tool Limitations:** No single tool can perfectly reverse engineer all aspects of a complex system.
*   **Effort Intensive:** Can be a very time-consuming and manual process.

## 10. Summary of Key Concepts

*   **Measures, Metrics, Indicators:** Fundamental for understanding and controlling software processes and products.
*   **Process vs. Project Metrics:** Process metrics for long-term improvement; project metrics for managing individual projects.
*   **Software Measurement:** Can be direct (e.g., LOC) or indirect (e.g., FP, quality).
*   **Quality Metrics:** Cover various aspects like correctness, reliability, efficiency, maintainability.
*   **S/W Reliability:** Focuses on failure-free operation, with metrics like MTTF, MTBF, Availability.
*   **Estimation Techniques:**
    *   **LOC:** Simple but flawed, language-dependent, difficult to estimate early.
    *   **FP:** Language-independent, measures functionality, can be estimated from requirements, involves UFP and VAF/TCF based on GSCs.
    *   **COCOMO:** Empirical model (Basic, Intermediate, COCOMO II) using KLOC to estimate effort and time, with modes (Organic, Semi-Detached, Embedded) and cost drivers.
*   **Project Tracking & Scheduling:** Essential for managing project progress, resources, and timelines using tools like Gantt charts and PERT/CPM.
*   **Reverse Engineering:** Analyzing an existing system to understand its design and functionality, often for maintenance, migration, or documentation recovery.

This comprehensive set of notes should cover all the topics in your Unit II syllabus, drawing from the provided presentations and elaborating where needed. Remember to practice the numerical examples to solidify your understanding of FP and COCOMO calculations.