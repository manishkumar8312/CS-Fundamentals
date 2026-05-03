# Chapter 10: Security and Protection

Security and protection are fundamental to any operating system. This chapter covers the goals of security, authentication methods, access control models, protection mechanisms, common attacks, and encryption techniques that safeguard data and resources.

---

## Security Goals: Confidentiality, Integrity, Availability

The **CIA triad** defines the core objectives of information security.

| Goal | Meaning | Example failure |
|------|---------|----------------|
| **Confidentiality** | Preventing unauthorised access to information. | Hacker steals password file. |
| **Integrity** | Ensuring data is not tampered with or modified without permission. | Malware alters system binaries. |
| **Availability** | Ensuring systems and data are accessible when needed. | Denial‑of‑service (DoS) attack makes website unreachable. |

**Real‑life analogy**: A bank vault:
- **Confidentiality**: Only authorised staff can see inside.
- **Integrity**: Money stored cannot be altered (counterfeiting prevented).
- **Availability**: The vault is accessible during business hours.

---

## Authentication

**Authentication** verifies the identity of a user or process. Common factors:

### 1. Something you know (passwords, PINs)

Most common, but vulnerable to guessing, theft, phishing.

- **Password storage**: Modern OSes store **hashed** passwords (not plaintext) using algorithms like bcrypt, SHA‑256 with salt.
- **Salt**: Random value added to each password before hashing to prevent rainbow table attacks.

### 2. Something you have (smart card, security token, phone)

Adds a second factor; usually combined with password (two‑factor authentication – 2FA).

- **Hardware tokens**: YubiKey, RSA SecurID.
- **Software tokens**: TOTP (Google Authenticator) – time‑based one‑time password.

### 3. Something you are (biometrics)

Fingerprint, iris scan, face recognition, voice.

- **Pros**: Hard to forge, convenient.
- **Cons**: Not changeable if compromised; false positives/negatives.

### Multi‑factor Authentication (MFA)

Combines two or more factors. For example, password (knowledge) + SMS code (possession). Greatly increases security.

**Real‑life analogy**: Entering a secure building:
- Password = keycode at the door.
- Security token = keycard.
- Biometric = fingerprint scanner.
- MFA = keycard + PIN.

---

## Access Control

Once authenticated, the OS must decide what resources a user can access and what operations are allowed. Three classic models.

### DAC (Discretionary Access Control)

The **owner** of a resource decides who can access it. Common in general‑purpose OSes (Unix permissions, Windows ACLs).

- **Unix permissions**: Read, write, execute for owner, group, others.
- **Problem**: Users may accidentally grant excessive permissions.

**Real‑life**: You own a house; you give keys to friends as you wish.

### MAC (Mandatory Access Control)

The **system** (OS) enforces a global policy that users cannot override. Used in high‑security environments (military, SELinux, AppArmor).

- **Labels**: Each resource and user has a security label (e.g., “Top Secret”, “Secret”, “Unclassified”).
- **Rules**: A user can access a resource only if their clearance dominates the resource’s label.

**Real‑life**: Military document classification – a “Secret” clearance holder cannot read “Top Secret” documents, regardless of their wishes.

### RBAC (Role‑Based Access Control)

Permissions are assigned to **roles**, and users are assigned to roles. Roles reflect job functions (e.g., “Doctor”, “Nurse”, “Accountant”).

- **Advantage**: Simplify administration – change role permissions, not per user.
- **Examples**: Database systems, enterprise applications, Windows groups.

**Real‑life**: Hospital – doctors have prescription rights; nurses have patient care rights; receptionists can only schedule appointments. Users are assigned to roles.

---

## Protection Mechanisms: Capabilities and Access Matrix

The OS needs internal structures to enforce access control.

### Access Matrix

A conceptual table where rows represent **subjects** (users, processes) and columns represent **objects** (files, devices). Each cell contains the allowed **operations** (read, write, execute, delete).

| Subject | File A | File B | Printer |
|---------|--------|--------|---------|
| Alice   | r,w    | r      | (none)  |
| Bob     | r      | r,w    | print   |

- **Implementation**:
  - **Access Control Lists (ACLs)**: Attach a list to each object (column of matrix). Windows NTFS, POSIX ACLs.
  - **Capabilities**: Attach a list to each subject (row of matrix). Each capability is an unforgeable token granting access to a specific object with specific rights.

### Capability

A capability is a ticket that gives a process permission to perform certain operations on an object. Often implemented as a protected, kernel‑managed reference.

- **Advantage**: Easy to delegate; fine‑grained.
- **Disadvantage**: Need to revoke capabilities (can be complex).
- **Examples**: Early research OS (Hydra, KeyKOS), some microkernels (seL4).

**Real‑life analogy**: 
- **ACL**: A bouncer’s list at a club – each club has its own list of allowed guests.
- **Capability**: A wristband – you show it to enter; different colours give different access.

---

## Principle of Least Privilege

The **principle of least privilege** states that a process (or user) should be granted only the minimum privileges necessary to perform its task, and only for the minimum time needed.

- **Benefit**: Limits damage from bugs or attacks.
- **Examples**:
  - Unix `setuid` programs drop privileges after initial setup.
  - Web browsers run tabs in sandboxes with limited file access.
  - Linux capabilities: break root privileges into small pieces (`CAP_NET_ADMIN`, `CAP_SYS_ADMIN`).

**Real‑life**: A hotel valet – they can park your car but cannot open your room safe.

---

## Malicious Software (Malware)

Malware is software designed to harm or infiltrate a system.

| Type | Description | Propagation | Payload |
|------|-------------|-------------|---------|
| **Virus** | Attaches to legitimate programs; requires user action (running infected program). | File infection | Corruption, theft, backdoor. |
| **Worm** | Self‑replicates across networks without user action. | Network exploits, emails | Resource exhaustion, backdoor. |
| **Trojan** | Disguised as legitimate software; does not self‑replicate. | Social engineering | Data theft, ransomware. |
| **Rootkit** | Hides its presence (files, processes, network connections) from OS. | Often installed after initial compromise | Stealth, persistent backdoor. |
| **Ransomware** | Encrypts user files and demands payment. | Trojan, worm, exploit | File encryption. |
| **Spyware** | Collects user information secretly. | Bundled with freeware | Keylogging, browsing data. |

**Real‑life analogy**:
- **Virus**: A contagious disease spread by touch.
- **Worm**: A airborne pathogen that spreads itself through ventilation systems.
- **Trojan**: A delivery box labeled “gift” that contains a bomb.
- **Rootkit**: A spy who can delete security camera footage so you never know they were there.

---

## Buffer Overflow Attacks and Defenses

A **buffer overflow** occurs when a program writes data beyond the allocated buffer bounds, overwriting adjacent memory. Attackers exploit this to inject malicious code or change execution flow.

### Classic stack overflow

```c
void vulnerable(char *str) {
    char buffer[64];
    strcpy(buffer, str);   // no bounds check
}
```

If `str` is longer than 64 bytes, it overwrites the return address on the stack. An attacker crafts input that places attacker code (shellcode) and sets the return address to point to it.

### Defenses

| Defense | Description | Effectiveness |
|---------|-------------|---------------|
| **Non‑executable stack** (NX bit) | Mark stack memory as non‑executable. Prevents shellcode execution. | Bypassed by return‑to‑libc or ROP. |
| **Address Space Layout Randomization (ASLR)** | Randomise base addresses of stack, heap, libraries. Attacker cannot know return address location. | Effective; brute‑force possible on 32‑bit. |
| **Stack canaries** | Place a secret value (canary) before return address. If overflow overwrites it, program aborts. | Very effective; used by GCC (`-fstack-protector`). |
| **Bounds checking** | Compile‑time or runtime checks (e.g., Rust, Safe C extensions). | Most thorough, but performance cost. |
| **Control Flow Integrity (CFI)** | Restrict program jumps to a precomputed set of valid targets. | Emerging standard (e.g., Intel CET). |

**Real‑life analogy**: A hotel keycard system. Buffers are like mail slots – if you shove in a long package, it might push the room door open. Defenses are like making the slot too narrow (little canary) or randomising which door the key opens (ASLR).

---

## Encryption Basics for OS Security

Encryption transforms data to prevent unauthorised reading. Modern OSes use encryption to protect data at rest (disk) and in transit (network).

### Symmetric Encryption

Same key encrypts and decrypts.

- **Algorithms**: AES (Advanced Encryption Standard), ChaCha20.
- **Use**: Full‑disk encryption (FDE), file encryption, network session encryption (TLS).

### Asymmetric Encryption (Public Key)

Two keys: public key (encrypts), private key (decrypts). Infeasible to derive private from public.

- **Algorithms**: RSA, ECC (Elliptic Curve Cryptography).
- **Use**: Key exchange, digital signatures, authentication.

### Full‑Disk Encryption (FDE)

Encrypts the entire storage device (except boot block). The OS decrypts on‑the‑fly using a key derived from a passphrase, TPM (Trusted Platform Module), or USB token.

- **Examples**: Windows BitLocker, macOS FileVault, Linux LUKS (dm‑crypt).
- **Threat model**: Protects against physical theft of device; does not protect against a compromised running system.

**How LUKS works** (simplified):
1. User enters passphrase.
2. Passphrase decrypts a master key stored in LUKS header.
3. Master key decrypts disk blocks on‑the‑fly.

**Real‑life analogy**: A safe (encrypted disk) with a combination lock (passphrase). Even if a thief steals the safe, they cannot read documents inside without the combination.

---

## Summary

| Concept | Key takeaway |
|---------|--------------|
| Security goals | Confidentiality, integrity, availability (CIA triad). |
| Authentication | Something you know (password), have (token), are (biometric); MFA combines factors. |
| Access control | DAC (owner decides), MAC (system decides), RBAC (roles). |
| Protection mechanisms | Access matrix; implemented as ACLs (per object) or capabilities (per subject). |
| Least privilege | Grant minimal rights for minimal time to limit damage. |
| Malware types | Viruses (attach), worms (self‑spread), trojans (disguised), rootkits (hide), ransomware (encrypt). |
| Buffer overflow defenses | NX bit, ASLR, stack canaries, bounds checking, CFI. |
| Encryption for OS | Full‑disk encryption (BitLocker, FileVault, LUKS) protects against physical theft. |

Security is not a product but a continuous process. Understanding these OS‑level mechanisms is the first step toward building and maintaining trustworthy systems.