**Software maintenance** refers to the **ongoing activities that begin almost immediately after software is released to end users**. It is considered a critical aspect of an application's life cycle and is often **the most costly activity**, with organisations sometimes expending as much as 60 to 70 per cent of all resources on it. Maintenance continues throughout the entire life cycle of an application.

### Categories of Maintenance Activities

The sources describe the core functions, or types, of software maintenance, which align with commonly understood categories:

- **Adaptive Maintenance**: This type of maintenance involves **modifying the application to meet a changing operational or business environment**. This is essential because demands on business functions and information technology are constantly evolving, placing competitive pressure on organisations. The ability of software to be **adaptable** is a key component of its overall maintainability.
- **Perfective Maintenance (Enhancing Functionality)**: While the specific term "perfective maintenance" is not explicitly used, the sources describe this core activity as **implementing new capabilities or improvements requested by stakeholders to meet their evolving needs**. This is crucial for **maintaining user satisfaction over the software's lifetime**, as its functional content must be continually increased.
- **Corrective Maintenance (Correcting Defects)**: This involves **addressing and fixing errors (defects) that are discovered in the software** once it has been deployed. Defects are defined as problems reported by a user after the program has been released for general use. Effort required to locate and fix an error is a factor of maintainability.
- **User Support**: This involves **providing assistance as users integrate the application into their personal or business workflow**. This includes activities such as help lines and documentation.

### Advantages of Software Maintenance

The necessity for and advantages of robust software maintenance practices, including adaptive and perfective activities, stem from several factors:

- **Extended Software Life and Relevance**: Maintenance activities, along with reengineering when necessary, are **required to extend the effective life of legacy systems**. It ensures software keeps pace with continuously **changing demands on business functions and information technology**, which are evolving at a rapid pace and creating competitive pressure.
- **Cost-Effectiveness in the Long Term**: While maintenance is a costly activity, applying **solid software engineering practices throughout the software process facilitates maintenance activities**, potentially reducing rework and overall costs in the long run. For older products, **reengineering** can be a cost-effective business strategy when maintenance becomes increasingly difficult, as it helps create versions of existing programs with **higher quality and better maintainability**.
- **Improved Quality and Reliability**: By correcting defects and adapting to new environments or enhancing functionality, maintenance helps **sustain and improve the software's overall quality attributes**, including reliability, usability, and maintainability itself. **Quality and maintainability are inherent outcomes of good design**. The Law of Declining Quality states that the quality of systems will appear to decline unless rigorously maintained and adapted.
- **Sustainable Development**: Agile processes promote "sustainable development" by emphasising quality attributes like maintainability, allowing software teams to maintain a constant pace indefinitely. This implies that well-maintained software allows for more consistent and long-term development efforts.
- **User Satisfaction**: Continuous adaptation and enhancement of functionality are crucial for **maintaining user satisfaction** over the software's lifetime.

Software maintenance refers to **ongoing activities that begin almost immediately after software is released to end users**. It is a critical aspect of an application's life cycle, often representing **the most costly activity**, with organisations sometimes expending as much as 60 to 70 per cent of all resources on it.

The core functions of software maintenance include:

- **Correcting defects**: Addressing and fixing errors that are uncovered in the software. This is a continuous effort, as user feedback after deployment frequently reports defects.
- **Adapting the software**: Modifying the application to meet a changing operational or business environment. This is crucial because demands on business functions and information technology are constantly evolving, placing competitive pressure on organisations.
- **Enhancing functionality**: Implementing new capabilities or improvements requested by stakeholders to meet their evolving needs.
- **Supporting users**: Providing assistance as users integrate the application into their personal or business workflow. This includes activities such as help lines and documentation.

**Maintainability** is a key quality attribute of software that directly impacts maintenance efforts. It is defined as a **qualitative indication of the ease with which existing software can be corrected, adapted, or enhanced**. Maintainability is enhanced by:

- Effective modularity.
- The use of design patterns.
- Well-defined coding standards and conventions that lead to self-documenting and understandable source code.
- The application of various quality assurance techniques to uncover potential maintenance problems before release.
- **Program maintainability and program understandability are parallel concepts**: the more difficult a program is to understand, the more difficult it is to maintain.
- A time-oriented metric for maintainability is **mean-time-to-change (MTTC)**, which measures the time taken to analyse a change request, design the modification, implement it, test it, and distribute it to users.

**Relationship with Other Software Engineering Activities:**

- **Software Quality Assurance (SQA)**: SQA is pivotal to building high-quality software and plays a significant role in maintenance. It establishes the infrastructure for solid software engineering methods and quality control actions. SQA also works to ensure that software support activities, including maintenance, are conducted with quality as a dominant concern.
- **Software Configuration Management (SCM)**: This umbrella activity, applied throughout the software process, is essential for managing change. SCM can be viewed as a **software quality assurance activity** and helps control all software work products and the changes made to them, which is vital for effective maintenance.
- **Reviews and Audits**: Technical reviews are conducted to find errors and uncover issues early in the software process, which reduces the effort required for correction later during maintenance. Security risk management plans should also be periodically reviewed as part of the maintenance process.
- **Metrics**: All software metrics can be applied to both new software development and the maintenance of existing software. The **software maturity index (SMI)**, for instance, can be used for planning software maintenance activities; as SMI approaches 1.0, the product begins to stabilise.
- **Post-Mortem Evaluations**: These are conducted to extract lessons learned, evaluate planned versus actual schedules, collect and analyse software project metrics, and gather feedback from team members and customers. The findings are recorded to improve future processes, including maintenance.

**Reengineering**: When maintenance becomes increasingly difficult for an old product, **reengineering** can be considered. This involves rebuilding the product to add functionality, improve performance, enhance reliability, and crucially, boost maintainability. The process of software reengineering encompasses:

- Inventory analysis.
- **Document restructuring**: Addressing weak or non-existent documentation in legacy systems, with options ranging from not creating any new documentation to fully documenting critical systems depending on their importance.
- Reverse engineering.
- Program and data restructuring.
- Forward engineering. The overall intent of these activities is to create versions of existing programs that exhibit higher quality and better maintainability.

**Reverse engineering** in software is the **process of analysing an existing program to create a representation of it at a higher level of abstraction than its source code** [Pressman, p. 770]. Its primary goal is **design recovery**, which means extracting design information such as data, architectural, and procedural aspects from the current software [Pressman, p. 770].

Key characteristics and aspects of reverse engineering include:

- **Abstraction Level**: The aim is to extract design information at as high a level of sophistication as possible, moving from low-level procedural designs to higher-level object or data models [Pressman, p. 770].
- **Completeness**: While complete procedural design is easier to derive, developing complete UML diagrams or models is more challenging, with completeness generally decreasing as abstraction level increases [Pressman, p. 770].
- **Interactivity**: The process often requires significant human analyst involvement with automated tools, especially for achieving greater completeness at higher abstraction levels [Pressman, p. 770].
- **Directionality**: It moves from a lower abstraction (source code) to a higher one (design representations), which is the opposite of forward engineering [Pressman, p. 770].

The process typically involves **restructuring code** to improve its quality, **extracting abstractions** to develop meaningful specifications, and then **refining and simplifying** these abstractions [Pressman, p. 770]. Reverse engineering can be applied to understand a system's data (program or system level), its processing (from statement to system level), and its user interfaces, even if the re-engineered interface will be radically different [Pressman, p. 770].