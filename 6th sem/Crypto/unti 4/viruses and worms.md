---

## **Viruses and Worms – Characteristics**

---

### **Introduction**

**Viruses** and **worms** are both types of **self-replicating malware**, but they behave differently. A **virus** attaches itself to a host file or program and requires **user action** to spread, whereas a **worm** is a **standalone program** that spreads **automatically** across networks without any human interaction.

Despite these differences, both aim to **propagate**, **disrupt systems**, and **cause damage or unauthorized access**.

---

### **Characteristics of Viruses**

- **Host-dependent**: A virus cannot function independently and must attach to an executable file, document macro, or boot sector.
    
- **Activation required**: It needs to be run or opened by a user to start infecting.
    
- **Spreads through file transfers, USBs, email attachments**, etc.
    
- **Can lie dormant** until triggered by certain events (e.g., a specific date).
    
- May **delete files, corrupt programs, slow down system performance**, or display annoying messages.
    
- Some viruses are **polymorphic** (change their code to avoid detection) or **metamorphic** (rewrite themselves entirely).
    

---

### **Characteristics of Worms**

- **Independent and self-replicating**: A worm does not need a host file; it can execute and spread by itself.
    
- **Network-aware**: Exploits system vulnerabilities or weak network configurations to spread (e.g., via open ports or email address books).
    
- **Spreads rapidly**, often causing **network congestion** or service downtime.
    
- Can deliver **payloads** like backdoors, ransomware, or other malware.
    
- Often used in the creation of **botnets**—a network of infected computers controlled remotely.
    

---

#### Key Differences at a Glance

|Feature|Virus|Worm|
|---|---|---|
|Needs host|Yes|No|
|Spreads automatically|No|Yes|
|User interaction|Required|Not required|
|Primary target|Files|Networks|
|Damage type|Corrupts/infects files|Consumes bandwidth/resources|

---

Let me know when to continue with:  
👉 **Working of Viruses and Worms**.

---

## **Viruses and Worms – Working**

---

### **Working of a Virus**

A **computer virus** operates much like a biological virus: it infects a host, replicates, and spreads to new environments. Here's how it works:

1. **Infection**:
    
    - A virus attaches itself to a legitimate file or program (like `.exe`, `.doc`, or `.dll`).
        
    - When the user opens or runs the infected file, the virus code is executed.
        
2. **Replication**:
    
    - The virus scans the system for other files to infect.
        
    - It embeds a copy of itself into these files, often without changing the file size or structure noticeably.
        
3. **Execution of Payload**:
    
    - Some viruses contain harmful payloads that activate after certain conditions are met (e.g., on a specific date or after a number of executions).
        
    - The payload can range from displaying messages to deleting files or formatting the disk.
        
4. **Persistence**:
    
    - Viruses often use stealth techniques to remain undetected, such as hiding in memory or using code obfuscation.
        
    - They may also disable antivirus tools or replicate to backup locations to reinfect the system later.
        

---

### **Working of a Worm**

A **worm** differs from a virus in that it is self-contained and designed to propagate itself independently, primarily through network connections.

1. **Execution**:
    
    - Once executed (e.g., through a malicious email attachment or an exploit), the worm activates immediately.
        
2. **Scanning and Propagation**:
    
    - The worm scans the local network or internet for vulnerable systems (e.g., systems with open ports or weak security).
        
    - Once a vulnerable system is found, the worm copies itself over and executes remotely.
        
3. **Replication**:
    
    - On each new system, the worm repeats the process—scanning, exploiting, and infecting.
        
    - It may create copies of itself in multiple locations to ensure continued survival.
        
4. **Optional Payload**:
    
    - Some worms do nothing more than replicate, but many carry additional payloads such as ransomware, spyware, or backdoors.
        
5. **Impact**:
    
    - Even if no malicious payload is delivered, the sheer volume of replication can lead to **network slowdowns**, **service crashes**, and **system instability**.
        

---

Let me know when to continue with:  
👉 **Infection Phase**.

---

## **Viruses and Worms – Infection Phase**

---

### **Infection Phase**

The **infection phase** is the **initial stage** of a virus or worm’s lifecycle, where the malicious software establishes itself on a system or within a network. This phase involves preparing for replication and future payload execution.

---

### **In Virus Lifecycle**

1. **Entry Point**:  
    A virus enters a system via:
    
    - Infected files (executables, documents with macros).
        
    - USB drives or portable storage.
        
    - Email attachments or downloads.
        
    - Exploits in vulnerable software.
        
2. **Attachment**:  
    The virus attaches itself to host programs, boot sectors, or system files, often modifying them slightly to embed its code.
    
3. **Activation**:  
    The virus remains dormant until the host program is executed. Upon activation:
    
    - It loads into memory.
        
    - Begins scanning for more files to infect.
        
    - May use system calls or direct memory access for stealth.
        

---

### **In Worm Lifecycle**

1. **Execution**:  
    A worm may be introduced through:
    
    - Opening a malicious attachment or link.
        
    - Exploiting a network vulnerability (e.g., open SMB shares, unpatched software).
        
    - Drive-by downloads from compromised websites.
        
2. **System Penetration**:  
    Unlike viruses, worms don’t need a host file. Once executed, they:
    
    - Copy themselves to multiple directories.
        
    - Modify registry entries for persistence.
        
    - Start scanning for vulnerable targets on the network.
        
3. **Self-replication Initiation**:  
    The worm begins automated replication—sending copies of itself via email, P2P networks, or direct connections.
    

---

#### **Goal of the Infection Phase**

The objective is to **establish a foothold**, remain **undetected**, and prepare for either:

- **Propagation** (spreading to other systems), or
    
- **Payload execution** (damaging the system, stealing data, etc.)
    

---

Let me know when you're ready to proceed to:  
👉 **Attack Phase**.

---

## **Viruses and Worms – Attack Phase**

---

### **Attack Phase**

The **attack phase** is the stage during which a virus or worm **executes its intended malicious payload**. This phase may begin immediately after infection or remain dormant until a specific condition is met—such as a date, number of infections, or user activity. The goal is to **damage the system**, **steal data**, or **create disruption**.

---

### **In the Case of Viruses**

After successfully infecting host files and replicating:

- The virus **activates its payload**, which could be:
    
    - **Data destruction**: Deleting or overwriting files.
        
    - **System disruption**: Slowing down the computer, causing application crashes.
        
    - **Visual effects**: Displaying pop-ups or screens.
        
    - **File corruption**: Making files unusable or modifying their contents.
        
    - **Privilege escalation**: Gaining deeper access to the system.
        
- Some viruses execute a **logic bomb**, triggering the payload under certain conditions (e.g., on April 1st or after the 10th execution).
    

---

### **In the Case of Worms**

Worms, after replicating across systems, may:

- **Deliver secondary malware** like ransomware, spyware, or backdoors.
    
- **Use the host machine in a botnet** to:
    
    - Launch DDoS attacks.
        
    - Send spam emails.
        
    - Spread more worms or viruses.
        
- **Steal confidential data** and forward it to a remote server.
    
- **Sabotage critical services**, including servers, databases, or entire networks.
    

Even worms without a destructive payload can cause harm by:

- **Exhausting bandwidth** and server resources.
    
- **Overloading networks**, resulting in downtime or latency.
    
- **Disrupting business operations**, especially in large-scale attacks.
    

---

### Summary

The **attack phase** determines the **impact and intent** of the virus or worm—ranging from mild annoyance to catastrophic system or data loss. In some cases, the malware simply opens the door for future attacks or maintains stealth to conduct prolonged surveillance or exploitation.

---

Let me know when to proceed to:  
👉 **Sniffers – Definition**.

---

## **Sniffers – Definition**

---

### **What is a Sniffer?**

A **sniffer** (also known as a **packet analyzer** or **network analyzer**) is a tool—either software or hardware—that is used to **capture and monitor network traffic**. Sniffers operate at the **data link layer** of the OSI model, allowing them to intercept and log network packets as they travel across the network.

While sniffers can be used for **legitimate purposes** such as network troubleshooting, performance monitoring, and protocol analysis, they are often exploited by attackers to **eavesdrop** on sensitive data like login credentials, emails, session tokens, and unencrypted communications.

---

### **Modes of Operation**

- **Normal (Non-Promiscuous) Mode**: The sniffer captures only packets addressed to the host machine.
    
- **Promiscuous Mode**: The sniffer captures **all packets** on the network segment, regardless of destination. This is the mode typically used in **malicious sniffing**.
    

---

### **Common Sniffing Tools**

- **Wireshark** – A widely-used open-source packet analyzer.
    
- **tcpdump** – A command-line sniffer tool for UNIX/Linux systems.
    
- **Ettercap**, **Cain & Abel**, **dsniff** – Often used in hacking and penetration testing.
    

---

A sniffer is often the **first tool used in a cyberattack**, especially in **passive reconnaissance**, where the attacker silently gathers data without altering network traffic.

---

Let me know when you’re ready to move on to:  
👉 **Spoofing** (as part of Sniffers).

---

## **Sniffers – Spoofing**

---

### **What is Spoofing in the Context of Sniffers?**

**Spoofing** refers to the act of **impersonating a legitimate device or user** on a network to deceive systems, intercept data, or gain unauthorized access. When combined with sniffing tools, spoofing becomes a **powerful technique** for capturing traffic that is not normally visible to the attacker.

---

### **Types of Spoofing Relevant to Sniffing**

1. **ARP Spoofing (Address Resolution Protocol Spoofing)**:
    
    - The attacker sends **fake ARP messages** onto the local network.
        
    - These messages associate the attacker’s MAC address with the IP address of a legitimate device (e.g., a router or server).
        
    - As a result, traffic meant for the legitimate device is **redirected to the attacker**, enabling packet sniffing and manipulation.
        
2. **IP Spoofing**:
    
    - The attacker **fakes the source IP address** in packet headers.
        
    - Often used to bypass IP-based authentication or to impersonate trusted devices.
        
3. **DNS Spoofing**:
    
    - The attacker responds to DNS queries with **forged responses**, redirecting users to malicious websites where data can be sniffed or stolen.
        

---

### **Why Spoofing is Used in Sniffing Attacks**

- To **gain visibility into targeted traffic** that wouldn’t normally pass through the attacker’s machine.
    
- To **bypass switched networks**, which isolate traffic to specific ports (unlike hubs).
    
- To **redirect or manipulate communication**, allowing for more advanced attacks like Man-in-the-Middle (MITM).
    

---

### **Consequences**

When spoofing is successfully combined with sniffing:

- **Login credentials**, **session cookies**, and **sensitive data** can be intercepted.
    
- **Communications can be modified** or **replayed**.
    
- Attackers may gain **long-term access** to systems or user accounts.
    

---

Let me know when to continue with:  
👉 **Sniffing** (detailed explanation as the next subtopic).

---

## **Sniffers – Sniffing**

---

### **What is Sniffing?**

**Sniffing** is the act of **intercepting and analyzing network traffic** using a tool known as a **sniffer**. It involves monitoring data packets as they travel across a network, often with the intent to gather sensitive information like usernames, passwords, session tokens, credit card numbers, and other confidential data.

Sniffing can be:

- **Passive** – Simply listening to and logging packets without altering them.
    
- **Active** – Involves manipulating or injecting traffic (often combined with spoofing or redirection techniques).
    

---

### **How Sniffing Works**

Sniffers work by placing the network interface card (NIC) into **promiscuous mode**, which allows the system to **capture all packets** traversing the network segment—not just those addressed to the host. On networks that use a hub, this is straightforward. On switched networks, attackers often use **ARP spoofing**, **MAC flooding**, or **port mirroring** to gain access to more traffic.

Once packets are captured, sniffers:

- Decode the data based on known protocol formats (like HTTP, FTP, SMTP, POP3).
    
- Display information in readable formats, exposing sensitive content if it's unencrypted.
    

---

### Legitimate vs. Malicious Use

- **Legitimate Use**: Network admins use sniffing for:
    
    - Troubleshooting connectivity issues.
        
    - Analyzing traffic patterns.
        
    - Debugging application performance.
        
- **Malicious Use**:
    
    - Intercepting credentials or session cookies.
        
    - Extracting sensitive documents or files.
        
    - Launching further attacks based on intercepted data.
        

---

### Encryption as a Defense

Sniffing is particularly dangerous on **unencrypted connections**. Protocols like HTTP, Telnet, and FTP transmit data in plain text, making them vulnerable. Using **encrypted protocols** (e.g., HTTPS, SSH, SFTP, TLS/SSL) significantly reduces the risk of sniffing.

---

Let me know when to continue with:  
👉 **Vulnerable Protocols**.

---

## **Sniffers – Vulnerable Protocols**

---

### **Overview**

Certain network protocols are inherently **insecure** because they transmit data in **cleartext** (unencrypted), making them highly vulnerable to sniffing attacks. If a sniffer is active on the network, these protocols can easily **leak sensitive information**, including login credentials, email contents, and session information.

---

### **Common Vulnerable Protocols**

1. **HTTP (HyperText Transfer Protocol)**
    
    - Transmits web data (including login forms) without encryption.
        
    - Passwords and session tokens can be intercepted directly.
        
    - Secure alternative: **HTTPS** (uses TLS encryption).
        
2. **FTP (File Transfer Protocol)**
    
    - Used for transferring files between systems.
        
    - Sends usernames and passwords in plain text.
        
    - Secure alternative: **SFTP (SSH File Transfer Protocol)** or **FTPS**.
        
3. **Telnet**
    
    - Used for remote command-line access.
        
    - Sends every keystroke, including login credentials, in cleartext.
        
    - Secure alternative: **SSH (Secure Shell)**.
        
4. **SMTP, POP3, IMAP (Email Protocols)**
    
    - These email protocols often send login credentials and emails unencrypted.
        
    - Secure alternatives: Use **SMTP over SSL/TLS**, **POP3S**, and **IMAPS**.
        
5. **SNMP v1/v2 (Simple Network Management Protocol)**
    
    - Used for monitoring and managing network devices.
        
    - Transmits data, including community strings (like passwords), in cleartext.
        
    - Secure alternative: **SNMPv3** (supports encryption and authentication).
        

---

### Why These Protocols Are Still Used

- **Legacy systems**.
    
- **Misconfiguration** or lack of awareness.
    
- Some tools or devices (especially IoT) only support insecure versions.
    

---

### Security Implication

Using these protocols in modern networks **without encryption** gives attackers a clear window into internal communications, enabling:

- **Credential theft**.
    
- **Session hijacking**.
    
- **Unauthorized access** to systems and services.
    

---

Let me know when to continue with:  
👉 **Types of Sniffers**.


---

## **Sniffers – Types**

---

### **1. Passive Sniffers**

Passive sniffers **only listen** to network traffic without injecting any data or interacting with the network. They operate in **promiscuous mode**, capturing every packet they can "see" on a shared network segment like a hub or an unsecured wireless network.

#### **Use Cases:**

- Used in environments where traffic is naturally broadcast (e.g., Ethernet hubs).
    
- Suitable for **eavesdropping** on unencrypted data.
    
- Harder to detect since they do not generate any traffic.
    

---

### **2. Active Sniffers**

Active sniffers are more **aggressive**. They work on switched networks where traffic is directed only to specific ports, so they must **manipulate the network** to intercept packets not originally meant for them.

#### **Techniques Used:**

- **ARP Spoofing**: Redirect traffic to the attacker’s system.
    
- **MAC Flooding**: Overload the switch's MAC address table to force it into hub-like behavior.
    
- **DHCP Spoofing**: Provide rogue DHCP responses to control network routing.
    
- **Port Mirroring Exploits**: Abuse switch configurations to duplicate traffic to the attacker’s port.
    

#### **Use Cases:**

- Used in **penetration testing** or **malicious attacks** on switched networks.
    
- Can be detected by intrusion detection systems due to abnormal behavior.
    

---

### Summary Table

|Type|Visibility|Network Type|Detectability|Techniques Involved|
|---|---|---|---|---|
|Passive Sniffer|Silent|Hubs or open Wi-Fi|Hard to detect|Promiscuous mode only|
|Active Sniffer|Manipulative|Switched networks|Easier to detect|ARP spoofing, MAC flooding|

---

Let me know when to continue with:  
👉 **Phishing – Methods**.