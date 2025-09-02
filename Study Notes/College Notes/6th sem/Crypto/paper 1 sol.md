Below is a comprehensive solution to the question paper, addressing each part systematically with detailed explanations and artifacts where applicable. Each question is worth 14 marks, so I’ll ensure clarity, depth, and relevance to maximize understanding while adhering to the artifact generation guidelines for specific technical content.

---

### Question 1
**a) Give a brief note on Cyber Security. Explain Active and Passive attacks.**

**Cyber Security**: Cyber security involves protecting computer systems, networks, devices, and data from unauthorized access, attacks, or damage. It encompasses technologies, processes, and practices to ensure confidentiality, integrity, and availability (CIA triad) of information. Key areas include network security, application security, endpoint security, data security, and incident response.

**Active Attacks**: These involve an attacker actively altering or disrupting a system or data. The goal is to manipulate, destroy, or interrupt services. Examples:
- **Masquerade**: Pretending to be a legitimate user to gain unauthorized access.
- **Denial of Service (DoS)**: Overloading a system to disrupt availability.
- **Modification**: Altering data during transmission (e.g., changing bank transaction details).

**Passive Attacks**: These involve monitoring or eavesdropping without altering data or systems. The goal is to gather information covertly. Examples:
- **Eavesdropping**: Intercepting communication (e.g., packet sniffing).
- **Traffic Analysis**: Analyzing communication patterns to infer sensitive information.
- **Release of Message Contents**: Capturing and reading confidential data.

**Key Difference**: Active attacks modify or disrupt systems, while passive attacks focus on unauthorized information gathering without detection.

---

**b) What are Intruders? With the help of a suitable example explain intrusion detection system.**

**Intruders**: Intruders are unauthorized individuals or entities attempting to access, misuse, or harm a system or network. Types include:
- **Masquerader**: An outsider posing as a legitimate user.
- **Misfeasor**: A legitimate user abusing privileges.
- **Clandestine User**: Someone seizing supervisory control to evade detection.

**Intrusion Detection System (IDS)**: An IDS monitors network or system activities for malicious behavior or policy violations, alerting administrators or taking automated actions. Types include:
- **Host-based IDS**: Monitors a single host (e.g., log analysis).
- **Network-based IDS**: Monitors network traffic (e.g., packet analysis).

**Example**: Consider a network-based IDS like Snort deployed in a corporate network. Snort analyzes incoming packets against a rule set to detect suspicious activity, such as a SQL injection attempt (e.g., detecting “`UNION SELECT`” in HTTP requests). If detected, it logs the event and alerts the security team. Below is a simplified Snort rule example:


alert tcp any any -> 192.168.1.0/24 80 (msg:"SQL Injection Attempt"; content:"UNION SELECT"; nocase; sid:1000001;)


This rule triggers an alert for packets containing “UNION SELECT” destined for the web server on port 80.

---

### Question 2
**Discuss the following terms:**

**a) Misconfiguration Attack**: Exploits errors in system or application settings, such as default passwords, open ports, or excessive permissions. Example: An attacker accesses an unsecured AWS S3 bucket due to misconfigured access controls, stealing sensitive data.

**b) Post-attack IDS**: An IDS that analyzes logs or system states after an attack to identify what occurred, aiding forensic analysis. Example: Reviewing audit logs post-breach to trace an attacker’s actions, like unauthorized file access.

**c) Penetration Testing**: A simulated cyberattack to evaluate system vulnerabilities, authorized by the system owner. It identifies weaknesses (e.g., unpatched software) and suggests remediation. Types include black-box (no prior knowledge) and white-box (full knowledge) testing.

**d) Brute-force Attack**: An attack attempting all possible combinations to guess credentials or keys. Example: Trying every password combination to crack a user account. Countermeasures include account lockouts and strong password policies.

**e) Active IDS**: An IDS that not only detects but also responds to threats in real-time, such as blocking malicious IP addresses or terminating suspicious sessions. Example: An active IDS detects a port scan and updates firewall rules to block the attacker’s IP.

---

### Question 3
**a) Explain non-alphabetic substitution cipher? Also discuss letter frequency attack on mono-alphabetic substitution cipher?**

**Non-alphabetic Substitution Cipher**: A cipher replacing plaintext characters with non-alphabetic symbols (e.g., numbers, special characters, or glyphs). Unlike alphabetic substitution (e.g., Caesar cipher), it uses arbitrary symbols. Example: Mapping A=1, B=2, ..., Z=26. A more complex version might use unique symbols like A=★, B=♠.

**Letter Frequency Attack on Mono-alphabetic Substitution Cipher**: Mono-alphabetic ciphers (including non-alphabetic ones) map each plaintext letter to a single ciphertext symbol consistently. This preserves letter frequency patterns, making it vulnerable to frequency analysis. Steps:
1. **Analyze Ciphertext**: Count the frequency of each symbol.
2. **Compare with Language Norms**: Match high-frequency symbols to common letters (e.g., E, T in English).
3. **Refine with Context**: Use digram/trigram frequencies (e.g., “TH”, “ING”) and trial-and-error to map other letters.

**Example**: For ciphertext “★★♠♠★♠”, if ★ is most frequent, it likely maps to E. If English frequency (E=12.7%, T=9.1%) aligns, ★=E, ♠=T. Partial decryption and context (e.g., word patterns) confirm the mapping. Countermeasures include using poly-alphabetic ciphers (e.g., Vigenère) to flatten frequency distributions.

---

**b) Explain how public-key encryption is used to distribute secret key?**

**Public-Key Encryption for Secret Key Distribution**: Public-key cryptography (e.g., RSA) uses a pair of keys: a public key (widely shared) and a private key (secret). To distribute a secret key (e.g., for symmetric encryption like AES):
1. **Sender Encrypts Secret Key**: Alice generates a secret key (K) for symmetric encryption. She encrypts K with Bob’s public key (PK_B), producing ciphertext C = E(PK_B, K).
2. **Transmission**: Alice sends C to Bob securely over an insecure channel.
3. **Receiver Decrypts**: Bob uses his private key (SK_B) to decrypt C, recovering K = D(SK_B, C).
4. **Symmetric Communication**: Both use K for fast, symmetric encryption/decryption of messages.

**Advantages**: Eliminates the need for a secure key exchange channel, as only the public key is shared. Ensures confidentiality since only Bob’s private key can decrypt C.

**Example**: Alice sends an AES key to Bob using RSA. She encrypts the 256-bit AES key with Bob’s RSA public key and sends it. Bob decrypts it with his RSA private key, then both use AES for secure communication.

---

### Question 4
**a) Explain Linear and Differential Cryptanalysis in detail.**

**Linear Cryptanalysis**:
- **Concept**: Exploits linear relationships between plaintext, ciphertext, and key bits in a cipher. It approximates the cipher’s operations (e.g., S-boxes) with linear equations.
- **Process**:
  1. Identify linear approximations: Find equations like P[i] ⊕ C[j] ⊕ K[k] = 0 that hold with probability p ≠ 0.5.
  2. Collect plaintext-ciphertext pairs: Analyze many pairs to compute the bias (deviation of p from 0.5).
  3. Key recovery: High bias suggests correct key bits; low bias indicates incorrect ones.
- **Application**: Effective against block ciphers like DES. Requires ~2^43 known plaintexts for DES.
- **Countermeasure**: Use non-linear S-boxes and increase diffusion.

**Differential Cryptanalysis**:
- **Concept**: Analyzes how differences in plaintext pairs propagate to ciphertext differences, revealing key information.
- **Process**:
  1. Choose plaintext pairs (P, P’) with a specific difference ΔP = P ⊕ P’.
  2. Observe ciphertext pairs (C, C’) and their difference ΔC = C ⊕ C’.
  3. Build differential trails: Identify high-probability paths where ΔP → ΔC through cipher rounds.
  4. Key recovery: High-probability differentials suggest correct subkey values.
- **Application**: Breaks DES with ~2^47 chosen plaintexts. Effective against ciphers with weak diffusion.
- **Countermeasure**: Increase rounds, use strong S-boxes, and enhance diffusion.

**Comparison**:
- Linear: Uses linear approximations; works with known plaintexts.
- Differential: Uses input-output differences; often requires chosen plaintexts.
- Both exploit cipher weaknesses but require large data and computational resources.

---

**b) How is ski different from block-dance attack?**

(Note: Assuming “ski” is a typo for “side-channel attack” and “block-dance attack” for “block cipher attack” or a specific attack like “slide attack”. If otherwise, please clarify.)

**Side-Channel Attack vs. Slide Attack**:
- **Side-Channel Attack**:
  - Targets implementation weaknesses, not the algorithm itself.
  - Exploits physical leakage (e.g., power consumption, timing, electromagnetic emissions).
  - Example: Differential Power Analysis (DPA) on AES measures power usage to deduce key bits.
  - Applicability: Any cipher with physical implementation (e.g., smart cards).
  - Countermeasure: Masking, noise injection, constant-time operations.

- **Slide Attack**:
  - A cryptanalytic attack targeting block ciphers with repetitive round structures.
  - Exploits identical subkey schedules or weak key expansion (e.g., in Feistel ciphers).
  - Process: “Slide” one encryption against another to align rounds, reducing complexity.
  - Example: Effective against ciphers like simplified DES with identical subkeys.
  - Countermeasure: Use unique subkeys per round, strong key schedules.

**Key Difference**: Side-channel attacks exploit physical implementation flaws, while slide attacks target algorithmic weaknesses in block cipher design.

---

**c) Describe encryption operation of DES algorithm.**

**Data Encryption Standard (DES)**:
- **Overview**: A symmetric block cipher with a 64-bit block size and 56-bit key (plus 8 parity bits). Uses a Feistel network with 16 rounds.
- **Encryption Process**:
  1. **Initial Permutation (IP)**: Rearrange the 64-bit plaintext using a fixed permutation table.
  2. **Split**: Divide the 64-bit block into two 32-bit halves (L_0, R_0).
  3. **16 Rounds**:
     - For round i (i=1 to 16):
       - **Expansion**: Expand R_(i-1) from 32 to 48 bits using an expansion table.
       - **Key Mixing**: XOR the expanded R_(i-1) with a 48-bit subkey K_i (derived from the 56-bit key via key schedule).
       - **Substitution**: Pass the result through 8 S-boxes, each mapping 6 bits to 4 bits (non-linear transformation).
       - **Permutation**: Apply a 32-bit permutation (P-box) to the S-box output.
       - **Combine**: XOR the result with L_(i-1) to get R_i; set L_i = R_(i-1).
  4. **Final Swap**: Swap L_16 and R_16 to get R_16 || L_16.
  5. **Inverse Initial Permutation (IP⁻¹)**: Apply the inverse of IP to produce the 64-bit ciphertext.


function DES_Encrypt(plaintext, key):
    // Initial Permutation
    block = InitialPermutation(plaintext)
    // Split into left and right halves
    L, R = block[0:32], block[32:64]
    // 16 rounds
    for i = 1 to 16:
        subkey = GenerateSubkey(key, i)
        expanded_R = Expand(R)
        mixed = expanded_R XOR subkey
        substituted = SBox(mixed)
        permuted = Permute(substituted)
        new_R = L XOR permuted
        L = R
        R = new_R
    // Final swap
    block = R || L
    // Inverse Initial Permutation
    ciphertext = InverseInitialPermutation(block)
    return ciphertext


**Key Schedule**: The 64-bit key is permuted (PC-1), split into two 28-bit halves, rotated left per round, and permuted (PC-2) to generate 48-bit subkeys.

---

### Question 5
**a) Explain The Ticket Granting Server (TGS) scheme in Kerberos.**

**Kerberos TGS Scheme**:
- **Overview**: Kerberos is a network authentication protocol using symmetric cryptography to provide secure access to services. The Ticket Granting Server (TGS) is a core component issuing service tickets after initial authentication.
- **Components**:
  - **Authentication Server (AS)**: Verifies user identity.
  - **TGS**: Issues tickets for service access.
  - **Key Distribution Center (KDC)**: Hosts AS and TGS.
- **Process**:
  1. **User Authentication**:
     - User sends ID to AS.
     - AS verifies user in the database and sends:
       - A session key (S_U,TGS) encrypted with the user’s key.
       - A Ticket Granting Ticket (TGT) encrypted with the TGS’s key, containing S_U,TGS and user details.
  2. **Service Request**:
     - User decrypts S_U,TGS and sends TGT, service ID, and an authenticator (encrypted with S_U,TGS) to TGS.
     - TGS decrypts TGT, verifies the authenticator, and issues:
       - A service ticket encrypted with the service’s key, containing a new session key (S_U,S).
       - S_U,S encrypted with S_U,TGS for the user.
  3. **Service Access**:
     - User sends the service ticket and an authenticator (encrypted with S_U,S) to the service.
     - Service decrypts the ticket, verifies the authenticator, and grants access.

**Security**: Uses timestamps and nonces to prevent replay attacks; tickets have expiration times.

---

**b) What is Steganography? What is the use of that purpose?**

**Steganography**:
- **Definition**: The practice of hiding secret information within non-secret data (e.g., images, audio) to avoid detection. Unlike cryptography, which obscures content, steganography conceals the existence of the message.
- **Techniques**:
  - **LSB (Least Significant Bit)**: Modify the least significant bits of image pixels to embed data.
  - **Audio Steganography**: Embed data in inaudible frequency ranges.
  - **Text Steganography**: Use formatting or invisible characters.

**Uses**:
- **Covert Communication**: Securely transmit sensitive data (e.g., military intelligence).
- **Watermarking**: Embed ownership information in media.
- **Data Hiding**: Protect intellectual property or prevent unauthorized access.

**Example**: Embedding a text message in an image by altering pixel RGB values slightly, undetectable to the human eye.

---

### Question 6
**What do you mean by Digital Certificate? Discuss Digital signature and Certificate Authority.**

**Digital Certificate**:
- **Definition**: An electronic document binding a public key to an entity (e.g., person, organization) to prove identity. Issued by a Certificate Authority (CA).
- **Components**:
  - Public key, entity details (e.g., name, organization).
  - CA’s digital signature, validity period, serial number.
- **Use**: Establishes trust in secure communications (e.g., HTTPS, email signing).

**Digital Signature**:
- **Definition**: A cryptographic mechanism to verify the authenticity and integrity of a message or document.
- **Process**:
  1. Sender hashes the message (e.g., using SHA-256).
  2. Encrypts the hash with their private key to create the signature.
  3. Sends the message and signature.
  4. Receiver decrypts the signature with the sender’s public key, hashes the message, and compares hashes.
- **Purpose**: Ensures non-repudiation, integrity, and authenticity.

**Certificate Authority (CA)**:
- **Role**: A trusted entity issuing, managing, and revoking digital certificates.
- **Functions**:
  - Verifies applicant identity before issuing certificates.
  - Maintains Certificate Revocation Lists (CRLs) for invalid certificates.
  - Signs certificates with its private key to ensure authenticity.
- **Example**: DigiCert, Let’s Encrypt. Browsers trust CAs to validate HTTPS websites.

**Example**: A website’s SSL certificate, signed by a CA, contains its public key. Browsers verify the CA’s signature to trust the site.

---

### Question 7
**Explain IP Security (IPSec) along with its applications.**

**IP Security (IPSec)**:
- **Overview**: A protocol suite securing IP communications by authenticating and encrypting packets. Operates at the network layer, protecting all upper-layer protocols.
- **Components**:
  - **Authentication Header (AH)**: Provides integrity and authentication but no confidentiality.
  - **Encapsulating Security Payload (ESP)**: Provides confidentiality, integrity, and authentication.
  - **Internet Key Exchange (IKE)**: Manages security associations (SAs) and key exchange.
- **Modes**:
  - **Transport Mode**: Protects payload; used between hosts.
  - **Tunnel Mode**: Protects entire packet; used in VPNs.
- **Security Associations (SA)**: Define security parameters (e.g., keys, algorithms) for unidirectional communication.

**Operation**:
1. Establish SAs via IKE (e.g., using Diffie-Hellman for key exchange).
2. Apply AH/ESP to packets based on policy (e.g., encrypt with AES, authenticate with HMAC-SHA).
3. Transmit secured packets; receiver verifies/decrypts using SA parameters.

**Applications**:
- **VPNs**: Secure site-to-site or remote access connections (e.g., corporate networks).
- **Secure Remote Access**: Protect data for teleworkers.
- **Secure Routing**: Authenticate routing protocol updates.
- **E-commerce**: Secure online transactions over public networks.

**Advantages**: Transparent to applications, supports IPv4/IPv6, flexible security policies.

---

### Question 8
**Write short notes on any two of the following:**

**a) Phishing Attack**:
- **Definition**: A social engineering attack where attackers impersonate trusted entities to trick users into revealing sensitive information (e.g., passwords, credit card details).
- **Methods**: Email, SMS, or fake websites mimicking legitimate services (e.g., a fake bank login page).
- **Example**: An email claiming to be from PayPal, urging users to “verify” their account via a malicious link.
- **Prevention**: User education, email filters, two-factor authentication (2FA).

**b) Black and White Hat Hackers**:
- **Black Hat Hackers**: Malicious hackers exploiting vulnerabilities for personal gain, data theft, or disruption. Example: Deploying ransomware.
- **White Hat Hackers**: Ethical hackers testing systems with permission to identify vulnerabilities. Example: Penetration testers hired by companies.
- **Key Difference**: Intent and authorization. Black hats act illegally; white hats work legally to improve security.

---

This response covers all questions comprehensively, with artifacts for technical content (e.g., Snort rule, DES pseudocode) wrapped in `<xaiArtifact>` tags as per guidelines. Each section is structured to address the 14-mark weightage with clear, concise, and detailed explanations. If further clarification is needed, please specify!