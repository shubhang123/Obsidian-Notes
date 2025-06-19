---

## **Phishing – Methods**

---

### **What is Phishing?**

**Phishing** is a **social engineering attack** used by cybercriminals to trick individuals into revealing sensitive information such as usernames, passwords, credit card numbers, or banking credentials. It relies on **deception** and **psychological manipulation** rather than technical vulnerabilities.

---

### **Common Methods of Phishing**

1. **Email Phishing**
    
    - The most widespread form.
        
    - Attackers send emails that appear to be from legitimate sources (banks, social networks, e-commerce platforms).
        
    - Contains fake links leading to **spoofed websites** designed to steal login credentials or install malware.
        
2. **Spear Phishing**
    
    - A targeted form of phishing.
        
    - The attacker crafts personalized messages for a specific individual or organization using known personal details.
        
    - Often used in corporate espionage or to breach high-value accounts.
        
3. **Smishing (SMS Phishing)**
    
    - Delivers phishing content through **text messages**.
        
    - May contain shortened URLs or urgent messages (e.g., “Your account has been locked”).
        
4. **Vishing (Voice Phishing)**
    
    - Uses **phone calls** to impersonate officials (bank agents, IRS, tech support).
        
    - Victims are tricked into providing sensitive information over the call.
        
5. **Social Media Phishing**
    
    - Fake profiles or posts are used to lure users into clicking links or sharing data.
        
    - Often disguised as contests, news, or free offers.
        
6. **Search Engine Phishing**
    
    - Attackers create fake websites that are indexed by search engines.
        
    - Unsuspecting users click on these during regular searches, not realizing they're fraudulent.
        
7. **Malvertising (Malicious Advertising)**
    
    - Involves placing malicious ads on legitimate websites.
        
    - Clicking the ad redirects users to a phishing page or triggers a malware download.
        

---

Each of these methods plays on **trust and urgency**, convincing the user to act quickly—often without verifying authenticity.

---

Let me know when to continue with:  
👉 **Phishing – Process**.

---

## **Phishing – Process**

---

### **Overview**

The **phishing process** is a **step-by-step strategy** used by attackers to **deceive victims** into revealing sensitive information. The process is often simple but highly effective, relying more on **social manipulation** than on complex technical methods.

---

### **Steps in the Phishing Process**

1. **Preparation and Target Selection**
    
    - The attacker identifies a **target group or individual**.
        
    - In broad phishing, this could be the general public (e.g., “Verify your bank account”).
        
    - In spear phishing, the attacker collects detailed information about the victim (e.g., from LinkedIn, data breaches, or social media).
        
2. **Crafting a Deceptive Message**
    
    - A **fake but convincing message** is created, usually imitating a trustworthy entity like a bank, company, or government agency.
        
    - The message includes:
        
        - Logos and branding to appear authentic.
            
        - Urgent or fear-inducing language (e.g., “Your account will be locked!”).
            
        - A **malicious link** or attachment.
            
3. **Delivery of the Message**
    
    - The phishing content is delivered via:
        
        - **Email** (most common)
            
        - **SMS** (smishing)
            
        - **Phone call** (vishing)
            
        - **Social media messages**
            
    - The attacker relies on the victim opening the message and acting quickly without thinking.
        
4. **Deception and Data Capture**
    
    - The victim clicks on the link or opens an attachment.
        
    - This redirects to a **spoofed website** or launches malware.
        
    - The victim is asked to **enter credentials**, personal information, or even perform financial transactions.
        
    - The entered data is silently **captured and sent to the attacker**.
        
5. **Exploitation of Information**
    
    - The attacker uses the stolen data to:
        
        - **Log into accounts**
            
        - **Steal money**
            
        - **Spread malware**
            
        - **Launch further attacks**
            
        - **Sell the data on the dark web**
            

---

### Summary

The phishing process is carefully designed to **imitate trust, create urgency, and bypass rational thinking**, making even technically aware users vulnerable if they’re not vigilant.

---

Let me know when you're ready for:  
👉 **Phishing – Attack Types** (starting with **Man-in-the-Middle Attacks**).

---

## **Phishing – Attack Types: Man-in-the-Middle (MITM) Attacks**

---

### **What is a Man-in-the-Middle (MITM) Attack?**

A **Man-in-the-Middle (MITM)** attack is a type of phishing technique where the attacker **secretly intercepts and possibly alters the communication** between two parties who believe they are directly communicating with each other. The attacker acts as an invisible intermediary, either **passively eavesdropping** or **actively manipulating** the data in transit.

In phishing, MITM is used to **intercept login credentials, session tokens, banking information, or confidential messages**, often without either party realizing it.

---

### **How It Works**

1. **Interception**
    
    - The attacker places themselves between the user and the intended destination, often by:
        
        - **ARP spoofing** (on LANs)
            
        - **DNS poisoning**
            
        - **Compromised Wi-Fi networks**
            
        - **Rogue access points**
            
2. **Session Hijacking or Data Relay**
    
    - The attacker **forwards the traffic** to the real destination to avoid suspicion.
        
    - While doing so, they can:
        
        - **Record** login credentials.
            
        - **Inject malicious scripts or links** into otherwise legitimate content.
            
        - **Modify responses** to trick users into taking further harmful actions.
            
3. **Exfiltration**
    
    - The captured data is saved or transmitted to the attacker's server.
        
    - In some cases, attackers may **gain full control over the session**, especially if session tokens or cookies are stolen.
        

---

### **Example Scenario**

A user connects to a public Wi-Fi at a café. The attacker, controlling the access point or using ARP spoofing, intercepts the login request to a banking site. The user enters credentials on a fake page served by the attacker, who then relays them to the real bank site, making the interaction appear genuine—all while stealing the credentials.

---

### **Preventive Measures**

- **Use HTTPS everywhere** (and verify the certificate).
    
- Avoid entering sensitive data on **public or unknown networks**.
    
- Enable **multi-factor authentication (MFA)**.
    
- Use **VPNs** to encrypt traffic on untrusted networks.
    
- Employ **HSTS (HTTP Strict Transport Security)** on websites.
    

---

Let me know when to proceed to:  
👉 **Phishing – URL Obfuscation Attacks**.

---

## **Phishing – URL Obfuscation Attacks**

---

### **What is a URL Obfuscation Attack?**

**URL Obfuscation** is a phishing technique in which the attacker disguises or manipulates a web address (URL) to **trick users into visiting a malicious site** that appears to be legitimate. The goal is to **bypass the user’s judgment** and make the malicious URL appear trustworthy—often mimicking the look and structure of well-known websites.

---

### **Techniques Used in URL Obfuscation**

1. **Misspelled Domains (Typosquatting)**
    
    - Example: `www.gooogle.com` instead of `www.google.com`
        
    - Relies on **user typing mistakes** or **visual similarity**.
        
2. **Subdomain Spoofing**
    
    - Example: `www.paypal.com.secure-login.com`
        
    - The real domain is `secure-login.com`, not `paypal.com`.
        
    - Designed to **look legitimate** at a glance.
        
3. **Hex/Decimal IP Encoding**
    
    - Using numeric or hexadecimal IP addresses instead of readable domain names.
        
    - Example: `http://0xA9FEA0C0` might point to a malicious server.
        
    - Hard for users to recognize.
        
4. **Homograph Attacks (Unicode Spoofing)**
    
    - Replace Latin characters with **lookalike Unicode characters**.
        
    - Example: `аmazon.com` (Cyrillic "а") vs `amazon.com` (Latin "a").
        
5. **Long URLs with Legitimate Words**
    
    - Include real brand names in paths to look credible.
        
    - Example: `http://maliciousdomain.com/secure/update/paypal/account/login.html`
        
6. **URL Shorteners**
    
    - Use services like `bit.ly`, `tinyurl`, or `goo.gl` to hide actual destination.
        
    - Users cannot see where they’re being redirected.
        

---

### **Why It Works**

- Users often **skim URLs quickly**, focusing on familiar brand names.
    
- Mobile users may see only **partial URLs**, increasing risk.
    
- Attackers use **SSL certificates** and padlock icons to falsely signal legitimacy.
    

---

### **How to Prevent URL Obfuscation Attacks**

- Always **hover over links** to preview the real URL.
    
- Look for **unexpected subdomains** or misspelled domain names.
    
- Use **trusted bookmarks** or manually type URLs.
    
- Rely on **browser-based anti-phishing filters** and **security extensions**.
    
- Educate users on how to **read URLs carefully**.
    

---

Let me know when you’re ready for:  
👉 **Phishing – Hidden Attacks**.