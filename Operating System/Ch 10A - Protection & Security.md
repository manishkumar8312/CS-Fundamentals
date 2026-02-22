# Protection & Security

Protection and Security are fundamental components of an Operating System that ensure system resources are accessed in a controlled, authorized, and safe manner. Protection focuses on internal access control mechanisms, while security addresses defense against both internal and external threats.

---

## 1. Goals of Protection

The primary goal of protection is to regulate access to system resources and prevent misuse.

### Key Objectives

* Prevent unauthorized access to system resources
* Ensure data integrity and consistency
* Enable controlled sharing of resources
* Protect processes from mutual interference
* Enforce the principle of least privilege

Protection mechanisms ensure correct usage of resources even when users are trusted.

---

## 2. Domain of Protection

A domain of protection specifies the access rights available to a user or process.

### Definition

A domain is defined as a set of *(object, rights)* pairs:

* **Object**: File, memory segment, device, or CPU
* **Rights**: Read, write, execute, delete

### Types of Domains

* User domain
* Kernel domain
* Process domain

### Domain Switching

* **Static switching**: Domain remains fixed throughout execution
* **Dynamic switching**: Domain changes during execution, such as during system calls

---

## 3. Access Matrix

The access matrix is a conceptual model used to represent the access rights of domains over objects.

### Structure

* Rows represent domains
* Columns represent objects
* Matrix entries specify access rights

### Implementations

* Access Control Lists (ACLs)
* Capability Lists

The access matrix is a logical model and is implemented in optimized forms in real systems.

---

## 4. Authentication and Authorization

### Authentication

Authentication verifies the identity of a user or process.

#### Common Methods

* Password-based authentication
* Biometric authentication
* Two-factor authentication
* Smart cards

---

### Authorization

Authorization determines the actions a user or process is permitted to perform.

* Controls access to files, memory, and devices
* Enforced through permissions and role-based policies

Authentication precedes authorization in all secure systems.

---

## 5. Security Threats and Vulnerabilities

### Common Security Threats

* Malware such as viruses, worms, and trojans
* Denial of Service (DoS) attacks
* Phishing and social engineering attacks
* Man-in-the-middle attacks
* Privilege escalation attacks

---

### Vulnerabilities

* Weak authentication mechanisms
* Software bugs and design flaws
* Improper access control
* Unpatched systems
* Misconfigured permissions

---

## 6. Difference Between Protection and Security

| Protection                   | Security                                      |
| ---------------------------- | --------------------------------------------- |
| Internal access control      | Defense against external and internal attacks |
| Focuses on authorized users  | Focuses on malicious entities                 |
| Operating system mechanism   | System-wide policy and enforcement            |
| Prevents misuse of resources | Prevents breaches and attacks                 |

---

## Conclusion

Protection and Security together form the foundation of a reliable and secure operating system. Protection mechanisms such as domains and access matrices regulate access to system resources, while security mechanisms defend against threats and vulnerabilities. Their combined use ensures system integrity, confidentiality, and availability.

