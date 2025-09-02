## Dak Madad — Line of Action Report

_(Prepared 15 May 2025)_

---

### 1. Objectives & Goals

|#|Objective|Success Metric|
|---|---|---|
|1|Launch a live pilot of Dak Madad at one local sorting & delivery hub in Indore|Pilot running by **31 Jul 2025** with QR-based processing on ≥90 % of registered posts|
|2|Cut sorting/delivery errors caused by address / PIN issues|≥10 % reduction in mis-routed items during pilot period|
|3|Produce a repeatable roll-out playbook for India Post|Playbook approved by India Post HQ by **30 Sep 2025**|

---

### 2. Action Items, Responsibilities & Timelines

|#|Action Item|Priority|Responsibility|Start|End|Status|Dependencies / Risks|Mitigation|
|---|---|---|---|---|---|---|---|---|
|1|Finalize Technical Architecture Document (TAD)|High|**Tilak** (Lead), Shubhang|16 May 25|25 May 25|In Progress|None|Iterative reviews with India Post IT|
|2|Build Batch Geocoding & PIN-Validation Module|High|**Shriyash** (Backend), Vinamra|20 May 25|20 Jun 25|Pending|MapMyIndia API access|Temp key from Google Maps until license signed|
|3|Secure MapMyIndia Licensing & SLA|High|**Tilak** (Biz Dev)|18 May 25|10 Jun 25|Pending|Budget approval|Escalate via India Post MoU if delayed|
|4|Integrate QR Generator into Receipt Workflow|High|**Rewa** (Mobile)|01 Jun 25|30 Jun 25|Pending|#2 complete|Use static QR template for test batch|
|5|Multilingual UI/UX Enhancements (Hindi, Marathi)|Med|**Shubhang** (Frontend)|22 May 25|22 Jun 25|Pending|None|Community translation review|
|6|Data-Security & Encryption Audit|Med|**Vinamra** (Security)|10 Jun 25|25 Jun 25|Pending|#1 draft ready|Use OWASP ASVS checklist|
|7|Staff Training & Pilot Dry-Run|High|**India Post Training Cell**, guided by Tilak|26 Jun 25|05 Jul 25|Pending|#4 complete|Staggered 2-hour sessions to avoid ops disruption|
|8|Pilot Go-Live at Indore Hub|High|**Operations Team** (Sorting lead: Akhilesh S.)|06 Jul 25|31 Jul 25|Pending|#3-#7 complete|On-site tech support for week 1|
|9|KPI Collection & Evaluation Report|High|**Shriyash** (Data), India Post MIS|01 Aug 25|20 Aug 25|Pending|Pilot data|Automated dashboards; weekly syncs|
|10|Roll-out Playbook & Scale Plan|Med|**Tilak** (PM)|15 Aug 25|30 Sep 25|Pending|#9 complete|Workshop with regional managers|

---

### 3. Resources Required

- **Manpower:** 5 core developers, 1 India Post IT liaison, 1 Ops champion at hub
    
- **Budget:** ₹12 L for pilot (licenses, training, hardware)
    
- **Tech:** MapMyIndia enterprise API, 10 rugged Android devices, thermal QR printers
    
- **Tools:** GitHub, JIRA, Grafana, SMS gateway
    

---

### 4. Current Overall Status

|Indicator|Value|
|---|---|
|Preparation Deliverables|40 % complete|
|Technical Build|20 % complete|
|External Agreements (MapMyIndia)|Negotiation stage|
|Risk Level|**Moderate**|

---

### 5. Key Dependencies & Risks

1. **MapMyIndia licensing delay** → could block geocoding accuracy
    
2. **Training slot conflicts** with postal peak hours
    
3. **Data-privacy clearance** for live address data
    
4. **Change-management resistance** from staff
    

---

### 6. Mitigation Strategies

|Risk|Mitigation|
|---|---|
|Licensing delay|Temporary Google Maps keys; escalate via India Post procurement|
|Training conflicts|Split sessions; provide video modules|
|Privacy clearance|Conduct formal DPA review; encrypt PII at rest|
|Staff resistance|Early demos, quick-win metrics, feedback loop|

---

### 7. Follow-Up & Review Schedule

|Checkpoint|Date|Purpose|
|---|---|---|
|Internal TAD Review|25 May 25|Freeze architecture|
|Licensing Status Call|05 Jun 25|Confirm API availability|
|Dry-Run Review|05 Jul 25|Go/No-Go decision|
|Mid-Pilot Review|20 Jul 25|Course-correction|
|Pilot Close-out & KPI Review|20 Aug 25|Decide scaling|

---

**Prepared by:**  
Tilak Neema (Project Manager) – on behalf of Team LeakCode404

---

_This Line of Action Report provides a clear roadmap, responsibilities, and risk-mitigation plan to guide Dak Madad from pilot launch through to network-wide scaling._


---
Here’s the revised Line of Action Report—removed direct references to “GPO” and instead using “local sorting and delivery hub.”

---

📄 **Dak Madad – Line of Action Report**  
AI-Powered Delivery Post Office Identification System  
Date: 15 May 2025

**Prepared by:** LeakCode404 (Tilak Neema, Shriyash Chakrawarty, Shriyash Beohar, Rewa Takzare, Vinamra Hetawal)

---

### 1. Objective

Operationalize Dak Madad via a focused pilot at a local sorting-and-delivery hub in Indore, validate core workflows and technology, then refine and scale across the network.

---

### 2. Pilot Launch: Local Sorting & Delivery Hub (Indore)

- Select the Indore facility’s sorting and last-mile delivery unit for end-to-end testing.
    
- Allows controlled validation of bulk data handling, QR-based tracking, address correction, and feedback loops.
    

---

### 3. Phase-Wise Implementation Plan

**Phase 1 – Pilot Rollout (June–July 2025)**

- Install mobile app for staff and integrate Dak Madad into existing sorting/dispatch workflow
    
- Batch-process address data for geolocation and QR code generation on registered-post receipts
    
- Train delivery personnel on QR scanning, route assistance, and feedback capture
    
- Monitor real-time performance metrics and error logs
    

**Phase 2 – Evaluation & Optimization (August 2025)**

- Measure impacts: delivery accuracy gains, sorting speed improvements, user feedback
    
- Identify technical or operational adjustments (throughput tuning, UI refinements)
    
- Update standard operating procedures for broader rollout
    

**Phase 3 – Scaling & Integration (September–December 2025)**

- Extend deployment to additional regional hubs in tier-2 cities (e.g., Bhopal, Vadodara, Jaipur)
    
- Formalize API integrations and secure partnerships (MapMyIndia licensing, internal address database)
    
- Begin compiling national address-correction repository (DigiPIN)
    

---

### 4. Key Technical Actions

- Develop a backend batch-geocoding and PIN-validation module
    
- Integrate MapMyIndia API as primary geolocation service (fallback: Google Maps)
    
- Implement multilingual UI support for Hindi, Marathi, Gujarati, Tamil, etc.
    
- Enforce end-to-end encryption, fine-grained access controls, and audit trails
    

---

### 5. Documentation & Communications (Pre-Third Meeting Deliverables)

- **Technical Architecture Document:** Data flows, modules, integration points, security
    
- **Gap Analysis Report:** Issues observed at the Indore sorting/delivery unit and how Dak Madad fills each gap
    
- **Meeting Summaries:** Key outcomes from April 11 and April 30 sessions
    
- **SIH Experience Deck:** Evolution of Dak Madad from concept to working prototype
    
- **MapMyIndia Collaboration Plan:** API capabilities, licensing terms, data-accuracy benchmarks
    

---

### 6. Immediate Next Steps

- Finalize and print all technical deliverables
    
- Engage MapMyIndia to confirm API access, pricing, and SLA
    
- Rehearse stakeholder presentation (target: first week of June)
    
- Coordinate pilot logistics and staff training schedule
    

---

### 7. Expected Impact at Pilot Site

- **10–15%** uplift in sorting and delivery efficiency
    
- Significant reduction in misrouted items via AI-driven address correction
    
- Real-time visibility and accountability through QR-enabled scans and user feedback
    
- Establishment of foundational DigiPIN data for nationwide roll-out
    

---

Let me know if you’d like this formatted as a styled PDF/Word document, or embedded into your slide deck next!