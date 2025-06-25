
# System Configuration Management (SCM)

## Introduction

Changes should be:

- Analyzed before they are made to the existing system.
    
- Recorded before they are implemented.
    
- Reported to have details of before and after.
    
- Controlled in a manner that will improve quality and reduce error.
    

This is where the need for **System Configuration Management (SCM)** arises.

## Why SCM?

- Multiple people are working on software which is consistently updating.
    
- It may be a method where multiple versions, branches, and authors are involved in a software project.
    
- The team is geographically distributed and works concurrently.
    
- Changes in user requirements, policy, budget, and schedules need to be accommodated.
    

SCM is the discipline which:

- Identifies change.
    
- Monitors and controls change.
    
- Ensures the proper implementation of change made to the item.
    
- Audits and reports on the change made.
    

It enables teams:

- To track changes made to the software system.
    
- To identify when and why changes were made.
    
- To manage the integration of these changes into the final product.
    

**Configuration Management (CM)** is a technique of identifying, organizing, and controlling modification to software being built by a programming team.

SCM involves a set of processes and tools that help to manage the different components of a software system, including source code, documentation, and other assets.

## Advantages

- It provides the tool to ensure that changes are being properly implemented.
    
- It has the capability of describing and storing the various constituents of software.
    
- SCM is used in keeping a system in a consistent state by automatically producing derived versions upon modification of the same component.
    

## The SCM Process Defines a Number of Tasks:

- Identification of objects in the software configuration
    
- Version Control
    
- Change Control
    
- Configuration Audit
    
- Status Reporting
    

---

### Identification of Objects in the Software Configuration

- **Basic Object**: Unit of text created by a software engineer during analysis, design, code, or test.
    
- **Aggregate Object**: A collection of essential objects and other aggregate objects. (e.g., Design Specification)
    

The interrelationships between configuration objects can be described with a **Module Interconnection Language (MIL)**.

Tasks include:

- Identifying the configuration items from products.
    
- Establishing relationships among items.
    

---

### Version Control

- Combines procedures and tools to handle different versions of configuration objects that are generated during the software process.
    
- Creating versions/specifications of the existing product to build new products with the help of an SCM system.
    

#### Example:

- After some changes, the version of a configuration object changes from `1.0` to `1.1`.
    
- Minor corrections and changes result in versions `1.1.1` and `1.1.2`, followed by a major update `1.2`.
    
- Development continues through `1.3` and `1.4`, eventually reaching a new path with `2.0`.
    
- Both versions may be supported concurrently.
    

---

### Change Control

- Controls changes to **Configuration Items (CI)**.
    

---

### Configuration Auditing

- A software configuration audit complements the formal technical review of the process and product.
    

---

### Configuration Status Reporting

- Sometimes also called **status accounting**.
    
- Provides accurate status and current configuration data to:
    
    - Developers
        
    - Testers
        
    - End users
        
    - Customers
        
    - Stakeholders
        

Documentation includes:

- Admin Guides
    
- User Guides
    
- FAQs
    
- Release Notes
    
- Installation Guides
    
- Configuration Guides
    

---

## Key Objectives of SCM

- **Control the evolution of software systems**: Ensures that changes are properly planned, tested, and integrated into the final product.
    
- **Enable collaboration and coordination**: Ensures that all team members are working on the same version and that changes are properly integrated.
    
- **Provide version control**: Helps manage and track different versions and revert to earlier ones if needed.
    
- **Facilitate replication and distribution**: Makes sure software can be easily replicated and deployed in test, production, and customer environments.
    

> **SCM** is a critical component of software development. Effective SCM practices can improve quality, increase reliability, enhance efficiency, and reduce the risk of errors.

---