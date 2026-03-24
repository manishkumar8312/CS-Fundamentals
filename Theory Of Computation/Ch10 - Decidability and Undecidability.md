# Decidability and Undecidability

Decidability is a central concept in the theory of computation that classifies problems based on whether they can be solved by an algorithm. It builds directly on the computational power of Turing Machines.

---

## 1. Recursive and Recursively Enumerable Languages

### Recursive (Decidable) Languages

A language ( L ) is **recursive** if there exists a Turing Machine that:

* Halts on **every input**, and
* Accepts if the string belongs to ( L ), otherwise rejects

**Key Property:**
Every input leads to a definite answer (YES/NO).

---

### Recursively Enumerable (RE) Languages

A language ( L ) is **recursively enumerable** if there exists a Turing Machine that:

* Accepts strings in ( L )
* May **loop forever** for strings not in ( L )

**Key Difference:**

| Property | Recursive     | Recursively Enumerable |
| -------- | ------------- | ---------------------- |
| Halting  | Always halts  | May not halt           |
| Decision | Yes/No always | Only YES guaranteed    |

---

### Relationship

$$
\text{Recursive} \subseteq \text{Recursively Enumerable}
$$

---

## 2. Decidable Languages

A language is **decidable** if there exists a Turing Machine that decides it.

### Characteristics:

* Always halts
* Gives correct YES/NO answer
* Corresponds to **recursive languages**

### Example:
$$
* ( L = { a^n b^n \mid n \geq 0 } )
$$
* Checking whether a string has equal number of `a`s followed by `b`s is decidable

---

## 3. Undecidable Languages

A language is **undecidable** if:

* No Turing Machine exists that can decide it for all inputs

### Characteristics:

* No algorithm can always give an answer
* Some inputs may cause infinite loops

### Example:

* Halting Problem
* Post Correspondence Problem (PCP)

---

## 4. Halting Problem

The **Halting Problem** is one of the most famous undecidable problems introduced by Alan Turing.

### Problem Statement

Given:

* A Turing Machine ( M )
* An input string ( w )

Determine whether:

$$
M \text{ halts on input } w
$$

---

### Visualization

![Image](https://images.openai.com/static-rsc-4/qhH35PeXmBjUHm-91_E08pW_OSFIK47c1kyt_qeoE7LQGcoqtHqfOaorYbr8HSO2OZIWwj3J1LictWCdt4H_4astbobhe2gs671hGDr2DPeVNlUZ7dU5QStf8E00nac9WtuVGe7ogXmS3Cwwm5ZGIN45APM4X2SoZsi1CNiKqo89EB7RA1kVZT66GGPeLx6F?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/BqDjGEhatchWz4Xzf_4KYyIXks9MRKLvAiaiGLRTvCl6qcjYqS_dWttOQwRABBk0CoS_NU27gyF9xPC2f1c8_3IXexapOM2G-ZpZnZwwe9KhFWuMxNv-8blcoFgFqs8MLMP_xyrMQ_JjUoRzCH1-e0KxVgFQflrwo6jBYisoZ4jT-JVojiMkg2m0Y92OQnbu?purpose=fullsize)

---

### Key Result

* There is **no general algorithm** that solves the Halting Problem for all inputs

---

### Proof Idea (Contradiction)

1. Assume a machine ( H ) exists that solves halting
2. Construct another machine that contradicts its behavior
3. Leads to logical inconsistency

Therefore, such a machine cannot exist

---

## 5. Reductions and Reduction Techniques

Reduction is a powerful method used to prove undecidability.

### Concept

If problem ( A ) can be reduced to problem ( B ):

$$
A \leq B
$$

* If ( A ) is undecidable, then ( B ) must also be undecidable

---

### Intuition

* Transform one problem into another
* Solve ( A ) using ( B )
* If ( B ) were solvable, ( A ) would also be solvable

---

### Types of Reductions

* Mapping reduction
* Turing reduction

---

### Visualization

![Image](https://images.openai.com/static-rsc-4/aeDn6WRQbFxQvHIWEdJHlYYrGeg4DbeCVrG3zif6l_L-Hfim2nmjXlwgDb2cN3o36KVSnMUQlsq2ZehtHMTwA3Un3TcOECGY1g74L62TZhO4dRr_ExfRfSsru1FyKy6sozYpp4dmfeaQZC8FSYpLDLHfkYZutETQ_rUjGDN9BBcx1oJ34KXlbuL8srQt_ke8?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/jHEvm4ng_7kuyfHyWKmZ0iSdBqWU8lMFMpwsB1L8MFMFb__L2m7EbnjyT6_1CLBpzpL16v73QoTxmbfDfxo2LPW8istCLFFvhVANEdbI7Zj0a6PcDbA28ptJiaKLFHVuP8Tybk6hNgrXf5aG_mU94h4L8ye55tIRt7V91RlCEOU30Couy9PeZdevQ18tC_ve?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/a_4t0Q_VB7mmw91zoDiVGX7pQhE-FdANdYNErhQTNQ46ULtCEcWxl93bUIhEKsr68OVfQOBjSylB1swJ9n5nHwaaOgZA9vAUYsJoZD8oKvfSCNejvWQjJ-yTSGfhKUguD7idQQRBbr6TTjQhinw4CNtflPF848nSYba2OIM3BR8QYJ2LLrAOhj5SH3qllsqj?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/TCfamhyIODwVxlbLKXLEWpbPrr1R8q9BOqLnibowwLVcNb6jTUwQwNxEWJltCfnZmDExMJnGN6I7Ozg6KN0jBcVIYCS-AKEUU9F_jHlvzOeIQhA89VFnEwJocWKAZwiEnxV6SDzO4AshlFfmS-qia6Yn0d_Dw3-WX7q_FDezA0K7VYsq0x6KQ6Bye1kF4vxx?purpose=fullsize)

---

## 6. Proofs of Undecidability

To prove a problem is undecidable:

### Step-by-Step Method

1. Start with a known undecidable problem (e.g., Halting Problem)
2. Reduce it to the target problem
3. Show transformation is valid
4. Conclude target problem is undecidable

---

### Example Strategy

To prove language ( L ) is undecidable:

* Assume ( L ) is decidable
* Use it to solve Halting Problem
* This creates contradiction
* Therefore, ( L ) is undecidable

---

## 7. Important Observations

* All decidable languages are recursively enumerable
* Not all recursively enumerable languages are decidable
* Undecidability shows limits of computation
* Many real-world problems (e.g., program verification) are undecidable

---

## 8. Summary

* Recursive languages correspond to decidable problems
* Recursively enumerable languages may not halt for all inputs
* Halting Problem is the foundation of undecidability
* Reductions are the main tool for proving undecidability
* Undecidable problems define the boundaries of algorithmic computation
