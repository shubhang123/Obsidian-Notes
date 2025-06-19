Great! Let’s begin with the **first topic** in your syllabus.

---

## 🛠️ Trojans and Backdoors

### Trojans

A **Trojan Horse**, or simply **Trojan**, is a type of malicious software that disguises itself as a legitimate application or file to trick users into installing it. Once executed, it can perform unauthorized actions without the user's consent or knowledge.

Trojans do not replicate themselves like viruses or worms. Instead, they rely on users to spread them—often through social engineering tactics, fake software, or email attachments.

### Backdoors

A **Backdoor** is a hidden method used by attackers to bypass normal authentication or security mechanisms of a system. Once installed—often via a Trojan—it allows remote access to the compromised system, enabling the attacker to control the system or extract data.
### **Overt and Covert Channels**

In computer security, **communication channels** can be classified into **overt** and **covert** channels based on their visibility and legitimacy.

- An **Overt Channel** is a legitimate, intended, and documented communication path used for normal system operations. For example, sending data over HTTP, HTTPS, FTP, or SMTP protocols are overt channel operations because they follow intended and transparent communication rules.
    
- A **Covert Channel**, in contrast, is an **unauthorized or hidden communication path** that violates the security policy of a system. It is used to transfer information in a way that is not intended for communication, often by exploiting features or flaws in the system. Attackers commonly use covert channels to leak data or send commands between infected systems and control servers without detection.
    

Covert channels are **dangerous because they are hard to detect** and can be embedded within seemingly legitimate activities. For instance, timing variations in network packet transmission, or manipulating unused bits in protocol headers, can serve as covert communication methods.

