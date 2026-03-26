## Introduction to Computational Complexity

Computational complexity studies the **resources required to solve computational problems**, primarily **time** and **space**, as a function of input size. It is a core part of Theory of Computation and helps classify problems based on their inherent difficulty.

---

## Time Complexity

<div style="display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; margin: 12px 0;">
  <img src="https://images.openai.com/static-rsc-4/tUg1rSM93MngmLObu8pQ_KETnxMLqSryZKPCZiJ1TaqVON2kC6_wLsTgnt96GzmDVS8KASg8oa11-NM0wyeKUQ8pDV1EnNSCT7N1-HEjzUCjEKeKswLxqAd_SyeDEtzgR6Bb8FPG5wAswcERZDgmdPWHB3XsfFYc13NF7DtSPwW9V8vBKVeiHD04tHMeQhEc?purpose=fullsize" alt="Time complexity diagram 1" width="380" height="240" />
  <img src="https://images.openai.com/static-rsc-4/A4l-QId6XMU-saj4labixPQhlqS9nKQ29bIfpiSNMxcpTdvjjyMN5amEUWl5DKrkxy2oxAsqaTMaM0oXg7lCUSzwufVRRN3tOUDZnI-PUK-0xneCwLTXonNlnYMYo_GYm0xA69K-Qi13HlU46Y_NACNnb3wI085XRGIRgb5t0n1GrcSKlWls2do_s-LLBJH7?purpose=fullsize" alt="Time complexity diagram 2" width="380" height="240" />
</div>

### Definition

Time complexity measures the **number of basic operations** an algorithm performs as a function of input size $n$.

### Common Cases

* **Best Case**: Minimum time taken
* **Average Case**: Expected time
* **Worst Case**: Maximum time (most important in analysis)

### Examples

* Linear Search -> $O(n)$
* Binary Search -> $O(\log n)$
* Bubble Sort -> $O(n^2)$

### Key Insight

We focus on **growth rate**, not exact execution time.

---

## Space Complexity

<div style="display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; margin: 12px 0;">
  <img src="https://images.openai.com/static-rsc-4/yMB56x4OxVVujq5dwmuO9g_uZ51RwTFUfanbs1-uA5hgB88riFijSUwC8hWyPy2CNNg5Cq68WxE24SGP9mK2sF_0pB8vrnzltv7RIslD2JXtAEDKXoBLMrhj7aGQ426U3-CdlMkWHM_PW_IM07ZXOuPX_XuQZp2tn64yEC2pIJu6t3HbJzNRGEC5zAJQKU7M?purpose=fullsize" alt="Space complexity diagram 1" width="280" height="180" />
  <img src="https://images.openai.com/static-rsc-4/1fReh8O95kHWE5gCWZFd2cOGMmhgICKYzBOClUdCxCDpUzXiRwduFs5FjQJuVMzBfkkQcVubECT6adFOSNAMPjKIhZnuSfqAjgc3jfgMcfd5_8ORqvOICg5sYnMLDw20MfCKU0uGT-DXa8RSrv4Tvyt8EhyYcroLBLwFNHCqnraJsl2PpRvV9Nf6QuCOYjpZ?purpose=fullsize" alt="Space complexity diagram 2" width="280" height="180" />
  <img src="https://images.openai.com/static-rsc-4/d1CwtBrYbnyZiHKqc-oYC3ySxq91xHAPnoOgC3qqmSOsONnUaeErF6w55nVLekWQw3LMVVYMyYJvBqRNy-Qbh0rUWFOzNJEqFwHLVvzAaili7RT3Rym4GHJe1zC1hpK1ZjwK0vBAkzeXXZpSEY1980lECcasOfNlJQu4d36sFjmIq7P_0-8OARG8JchjJ1Uz?purpose=fullsize" alt="Space complexity diagram 3" width="280" height="180" />
</div>

### Definition

Space complexity measures the **total memory used** by an algorithm, including:

* Input space
* Auxiliary space (extra memory)

### Examples

* Iterative algorithm -> $O(1)$ space
* Recursive Fibonacci -> $O(n)$ stack space

### Key Insight

Efficient algorithms balance **time vs memory trade-off**.

---

## Asymptotic Notations

<div style="display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; margin: 12px 0;">
  <img src="https://images.openai.com/static-rsc-4/vSLH26Ozx_lp2osbPRgM5aT0oU639I99ssA6ZIrlgzA50oQU85fjGBvLgVFcSamLOiOs9aUouRpc6MDGLkp8jGpveMSAhDg61wVcEY5ZTiNaxBdbAvrKpcI5y54DugauGAg99KVe0W7svDr0JYOGKSDvKRgwVf1X1n6ewnVqfyGm4CKOw6PZ1XiXMAxRPtdZ?purpose=fullsize" alt="Asymptotic notation diagram 1" width="380" height="240" />
  <img src="https://images.openai.com/static-rsc-4/cfW10CStLmNFzG2LNDs1XRoOiVuVtDMuXmJBQdXGBRWv2swR01Yu2CiKe5icscn-4LrHpFl4UDe0FkItEbZH8seeNHaNjvwNZkJ03nQBv1djx4UnQzPxKjqAaBpRTl1E4mYDzvEA-zDxzdY9WpDY0ahzl8y0zfLp_88c5jxt5aEWpFxYrDwj9QC92bTIZeR7?purpose=fullsize" alt="Asymptotic notation diagram 2" width="380" height="240" />
</div>


### Purpose

To describe **growth of functions** for large input sizes.

### Important Notations

#### 1. Big-O Notation $O(f(n))$

* Upper bound (worst-case)
* Example: $O(n^2)$

#### 2. Omega Notation $\Omega(f(n))$

* Lower bound (best-case)

#### 3. Theta Notation $\Theta(f(n))$

* Tight bound (exact growth)

### Example

If an algorithm takes $3n^2 + 5n + 2$, then:

* $O(n^2)$
* $\Omega(n^2)$
* $\Theta(n^2)$

---

## Complexity Classes

<div style="display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; margin: 12px 0;">
  <img src="https://images.openai.com/static-rsc-4/Xc19rMov54XJ9I7_tMUXWhZTwYSStHHq34778iP1PePWpzGHMKbCq0XI5rPohGunmoDqyr9WL5jc2nY0Cip4mQeF6leFXuEFe0p20XoZqHM6m5GvcplB37DIkHAQ_MOP3I-GQfTGhxRE-7I-_RRHeE0iJyxZZH9NdlmqBJXMrDbM2Y_vHV22CbBUcY0tC79-?purpose=fullsize" alt="Complexity class diagram 1" width="320" height="210" />
  <img src="https://images.openai.com/static-rsc-4/j976x4KyR7zd7DI5WIOHPG_FBz_PnbE_LLonvprBZGQ4vx8IeKMAIeBhNHeidiBxsSJ0tNl0EULfW2kdDioXTn2BKCteKtvVdpPrp9o5iKz2kGiloWsRkEnu7vgGaP8hspgbEi00QSd76Tl7Kl9V7Uw8ZrEk58hIRS9OxFjsqLOAUZgG4CRcxvn5CTQiz_OL?purpose=fullsize" alt="Complexity class diagram 2" width="320" height="210" />
  <img src="https://images.openai.com/static-rsc-4/-56fXLSLL5Nd_27_HmXyjQ0m2D_bgDSNxyiNePtr016hwy_KLXgeKbSrrYg6yPosCLvz5z_alW8utGd7u-w-kwxrjrDocBp3EUFtKWo8luKp7Pd3v3rjyF3P-IbTggC2nNrEgthygDzIBEumoohRD5_Lj-sP8shSUra43M1M2sx7KTI67yA0cEqwFdaY7iEs?purpose=fullsize" alt="Complexity class diagram 3" width="320" height="210" />
</div>

### Definition

Complexity classes group problems based on the **resources required to solve them**.

---

## Class P (Polynomial Time)

### Definition

Class **P** contains problems that can be solved in **polynomial time** by a deterministic machine.

### Examples

* Sorting (Merge Sort -> $O(n \log n)$)
* Shortest path (Dijkstra's algorithm)

### Key Idea

* Efficient and tractable problems

---

## Class NP (Nondeterministic Polynomial Time)

### Definition

Class **NP** contains problems whose solutions can be **verified in polynomial time**.

### Key Idea

* Finding solution may be hard
* Verifying solution is easy

### Example

* Given a subset, verify if sum = target (Subset Sum problem)

---

## Relationship Between P and NP

* $P \subseteq NP$
* Big open problem:
  **Is $P = NP$?** (unsolved)

---

## NP-Hard Problems

### Definition

A problem is **NP-Hard** if:

* It is at least as hard as the hardest problems in NP
* It may or may not belong to NP

### Key Points

* No requirement for polynomial verification
* Can be even harder than NP problems

### Example

* Halting Problem

---

## NP-Complete Problems

### Definition

A problem is **NP-Complete** if:

1. It is in NP
2. It is NP-Hard

### Key Insight

* Hardest problems within NP
* If one NP-Complete problem is solved in polynomial time ->
  All NP problems become polynomial

### Examples

* Traveling Salesman Problem (decision version)
* Boolean Satisfiability Problem (SAT)

---

## Relationships Among Classes

<div style="display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; margin: 12px 0;">
  <img src="https://images.openai.com/static-rsc-4/Q4bltzwHHx0tpjTvX90IsJGdsmy-YlHMOvmkP90aOa1VElQLawLt8xp6M5c0bwzhlV3cGITttoTfcD_np4XbaRjP_QFIpGKrbLT4y9ucrzLNsvx8sq7whz07GOLnRRKvK-jtw8kf7Zvf5Z1nyUmYmCrw_LhuR6yolvCRzHK6ZpA7R4g5wvcHvqmN-mr9Avxg?purpose=fullsize" alt="Class relationship diagram 2" width="280" height="180" />
  <img src="https://images.openai.com/static-rsc-4/e9ocJLOr_bTKBKl6B4IjTRW_650meh6OFR5s2ANS03_8fOps1zYNH9jG6QBfJ40iPLDYmBhQDUB18DlpW6N0VQ9KREzR9cNoTWIvHoOFBu243w-IXDSEAQO5YXf6DZN864k2k3otna_pvybLI8NKfkADkfonzvKm45zGBHL_6wD32aL-iAoFDVtvsG25Sct5?purpose=fullsize" alt="Class relationship diagram 3" width="280" height="180" />
  <img src="https://images.openai.com/static-rsc-4/qAaWWO_y8ZA8aWNuwO6eWgDuUHm6_bluqWMDMebvAYJ5FQnZwIVKVjJXC9oQ5uDvbZUVDbEEc6CtUSclvJEx2i3ma_choA60kNDbNX8i8xKpH10ohhOYPdUlhYc7ucfm8f4vCkcBPbZYjZp3yjbxU1epu_3NCGGcpavGwJV7_fHx7eqVqVxfTtHN7AVIMcbC?purpose=fullsize" alt="Class relationship diagram 4" width="280" height="180" />
</div>

### Inclusion Structure

- **P ⊆ NP**  
  Problems solvable in polynomial time are also verifiable in polynomial time.

- **NP-Complete ⊆ NP**  
  NP-Complete problems are a subset of NP.

- **NP-Hard ⊇ NP-Complete**  
  NP-Hard problems include all NP-Complete problems (and possibly more).

### Visual Interpretation

* NP-Complete lies at intersection of NP and NP-Hard
* NP-Hard includes problems outside NP

---

## Summary Table

| Class       | Definition                      | Key Property     |
| ----------- | ------------------------------- | ---------------- |
| P           | Solvable in polynomial time     | Efficient        |
| NP          | Verifiable in polynomial time   | Easy to check    |
| NP-Hard     | At least as hard as NP problems | May not be in NP |
| NP-Complete | NP + NP-Hard                    | Hardest in NP    |

---

## Final Understanding

* **Time & Space Complexity** -> Measure efficiency
* **Asymptotic Notations** -> Describe growth
* **P vs NP** -> Efficiency vs verification
* **NP-Complete** -> Most critical problems in CS

---
