# Turing Machines (TM)

A **Turing Machine (TM)** is a mathematical model of computation introduced by Alan Turing. It is a fundamental model in the theory of computation and is capable of simulating any algorithm.

---

## 1. Definition and Components of a Turing Machine

A Turing Machine is formally defined as:

M = (**Q**, **Σ (Sigma)**, **Γ (Gamma)**, **δ (delta)**, **q₀**, **B**, **F**)

Where:

* **Q** → Finite set of states
* **Σ (Sigma)** → Input alphabet (excluding blank symbol)
* **Γ (Gamma)** → Tape alphabet (includes blank symbol)
* **δ (delta)** → Transition function
* **q₀** → Initial state
* **B** → Blank symbol
* **F** → Set of accepting (final) states

### Working Structure

<img src="https://images.openai.com/static-rsc-4/nH5tGeofTbdo6dU2m8QacaxwdJmRh0cZNlIbe-Uv234iPl-D3WCVtsktpGZVxcWMjuOvAzoZMx57l8eCrk-Fa6L0eN51Ix8CbpGIxdV1QKHHfHRHs-U6pT5nDRVtXTPhltKON4-awTmY_6i13BoFZvBJfJKHZkp72MX0tXYpb0WD6acW0Bzr4E0LpiQfBdwb?purpose=fullsize" alt="Image" width="800" height="450" style="display:block; margin:16px auto; max-width:100%; height:auto; object-fit:contain;" />

<img src="https://images.openai.com/static-rsc-4/ZVOMWPhifOGzjLDNhX77hcvBL_7Wv7kSO364dtIzyayLxEs1GVpRryPo_6DnrsZlDeX_Sb-kd51ANmYNtpAw0gSBwIejiFb04iUYa5Z7iTHYJxnEKPQMnN-c5FMhfPdNn0AqRZwUtiCXc6UciWR57TSIKrn3yxkWx4jdy3xhxrQBaV_wfX5ycbAp8SASA2Tp?purpose=fullsize" alt="Image" width="800" height="450" style="display:block; margin:16px auto; max-width:100%; height:auto; object-fit:contain;" />

A Turing Machine consists of:

* **Infinite Tape** divided into cells
* **Tape Head** that can read, write, and move left or right
* **Finite Control Unit** (like a program with states)

---

## 2. Instantaneous Descriptions (IDs)

An **Instantaneous Description (ID)** represents the current configuration of a Turing Machine.

It includes:

* Current state
* Tape contents
* Head position

### Representation

$$
\alpha q \beta
$$

Where:

* $\alpha$ → Left part of tape
* $q$ → Current state
* $\beta$ → Current symbol and right part

### Example

If tape = `abb`, head at first `b`, state = $q_1$:

$$
a q_1 bb
$$

This means the machine is in state $q_1$, scanning symbol `b`.

---

## 3. Language Acceptance by Turing Machine

A Turing Machine **accepts a string** if:

* It reaches a **final (accepting) state**, or
* It halts in an accepting configuration

### Acceptance Types

* **Acceptance by Final State**
* **Acceptance by Halting**

### Rejection

* The machine enters a non-accepting halt state, or
* It runs forever (does not halt)

---

## 4. Design of Turing Machines for Simple Languages

### Example 1: Language ( L = { a^n b^n \mid n \geq 1 } )

**Idea:**

1. Replace first `a` with `X`
2. Move right to find corresponding `b`, replace with `Y`
3. Return to start
4. Repeat until all symbols are matched

### Transition Strategy

* ( q_0 ): Find `a` → mark as `X`
* ( q_1 ): Move right to find `b` → mark as `Y`
* ( q_2 ): Return left
* Accept if only `X` and `Y` remain

### Visualization

<img src="https://images.openai.com/static-rsc-4/4WgoBeSfIoBbnF0ly-NuCXFPhQGEBnNoVMG8fzAneeSEI5dBdAt12_eIhIXsBfAQL0qL7VFssTyFrLgxNoWOypYnOXT0l_zLmYvjDCZWSS7HElKasbO7pSW8VIk18cvFpkJpyJNYF_j4y18tusthbBXEY2nsdLhDQOS_s3AMrkuBu69KACviHVFNYsbWk1rv?purpose=fullsize" alt="Image" width="800" height="450" style="display:block; margin:16px auto; max-width:100%; height:auto; object-fit:contain;" />

<img src="https://images.openai.com/static-rsc-4/SY0wF_-AO1ZqOyRo0Joo4joOQB1hrH2H4VtwqGh3DSHCk1DDtH1vuj_Nnox2mTZpCoUINUX8FyObnegjpoEY3FK6YIIcbTrwaeQFHymXT0Rh2ku_u1LKvUsB5v01Rm7ImH_oaFe0BfrocLVf3kTFpeCzaqMft12wOcAu3qz46JgQo8OGDPa0i1JubmLVh3g3?purpose=fullsize" alt="Image" width="800" height="450" style="display:block; margin:16px auto; max-width:100%; height:auto; object-fit:contain;" />

---

### Example 2: Palindrome Language

$$
L = { w \mid w = w^R }
$$

**Approach:**

* Compare first and last symbols
* Mark them
* Repeat for inner substring

---

## 5. Variants of Turing Machines

Different variations of Turing Machines exist, but all have the same computational power.

---

### 5.1 Multi-Tape Turing Machine

<img src="https://images.openai.com/static-rsc-4/-nsL7rWR9PIskAuucgXj9OwcHqAGbPrx9SlP05ninfzZTXRerJ_rCdd-umveCxfj_NLNLLJCA8Ez4shYALfutr1knGXrZu4jXRVVoZQeiIqpVnFuaNcoyc-YRSfS8ef0R2HqVy8CnLUKQz3U0IjxB2akrISGvJyPHKYyP_dwokKo4RsocXN9yudCOxflrnSo?purpose=fullsize" alt="Image" width="800" height="450" style="display:block; margin:16px auto; max-width:100%; height:auto; object-fit:contain;" />

<img src="https://images.openai.com/static-rsc-4/obfqywZRMJQ-vAak83snu5mGsSOK2tFrG-86s2xrhcKN2NjsvLV5M7baAtA9IBQoWHoyf9IFJZIgYdyqwLgKBs5pRy1_A9SeuEyJ7kUpFN0s2RezJPe3SErau9bNYUPPfuf_mU_8aqXL_cBpx8U_lW4zPjRQrJMGuYrV5-M6oB0wrUNO_UX3quaiROwyS69L?purpose=fullsize" alt="Image" width="800" height="450" style="display:block; margin:16px auto; max-width:100%; height:auto; object-fit:contain;" />

<img src="https://images.openai.com/static-rsc-4/JA9vJOuUGgZGK6n0Ela2de2-xGGJFA4JzTFCfD6W4Ri3Qh_38VGILZTMfyREvjg7fi3gTQ_XM3bJ04yviWCU13qzBxbmsFIePihR6fCoTtBVU-JidZrVty3TgonLmISUJS6T9CnsmTedwSi3PhwJ7-QN2MT6rpActnExHF56t33BV9Ni2pM3ZqXeCSD9LKYU?purpose=fullsize" alt="Image" width="800" height="450" style="display:block; margin:16px auto; max-width:100%; height:auto; object-fit:contain;" />

* Has multiple tapes and heads
* Each tape operates independently
* Transition function:

$$
\delta(q, a_1, a_2, ..., a_k)
$$

**Advantage:** Faster computation
**Power:** Same as single-tape TM

---

### 5.2 Non-Deterministic Turing Machine (NTM)

<img src="https://images.openai.com/static-rsc-4/qO0ZEzg4Ckspj9cOvz6pK5iQtnS0UR-wimjNYHJt6qZFFUy61QcthQ3BpDm_2WYLPx4cEzw8c-l72BeF_DNNJJDWdwO4QHW4SQhdhD3J8nP8PdgFDl6BxObLLlcmvh6aXpZoed9KDdDSYJKWibOmjfnNh2yuLJojoRMzwaKXkiSa42WAl0QIwzlYdTTih3bd?purpose=fullsize" alt="Image" width="800" height="450" style="display:block; margin:16px auto; max-width:100%; height:auto; object-fit:contain;" />

<img src="https://images.openai.com/static-rsc-4/njUxF8OhOYaH1STbA2inSkzRwSuFWRCPnDtnif0gLOkX8qvHJ-Hh9GebtLZA8sIUZAxQtFgp_uoGu94ZeH45UsmBk8xfnJmhRqQXZjkwz2b-04d1i4OgVcp66dnhe_m4yHywSmHI4B9yUmp8SbSjluh2GZWhblzgeMDH5-wkHzUlxj_1GKMpkVVABmZJobMm?purpose=fullsize" alt="Image" width="800" height="450" style="display:block; margin:16px auto; max-width:100%; height:auto; object-fit:contain;" />

<img src="https://images.openai.com/static-rsc-4/1gmIuZeoulfFopHEacUuPrWrUUzYBMxLTpz2EPq2KLzcWLBTWmheIPiOn77FPSrV9QjAIB3det_tZszXl-AfWNWIcWwdT4_rqy0zSjiqVByXv-GLnwqujfjD61nTs6vYmVs7E4Zrl5s2amTDK6yfi8jfN3QW1UnGE8MC4w9NYNHsLKYscVScKi7QynGr8ZfD?purpose=fullsize" alt="Image" width="800" height="450" style="display:block; margin:16px auto; max-width:100%; height:auto; object-fit:contain;" />


* Can have multiple possible moves for a given state
* Explores multiple computation paths

**Acceptance Condition:**

* Accepts if **any branch** reaches an accepting state

---

### 5.3 Other Variants

* Multi-head Turing Machine
* Two-dimensional tape TM
* Universal Turing Machine (UTM)

---

## 6. Equivalence of Turing Machine Models

All variants of Turing Machines are **computationally equivalent**.

### Key Idea

* Any variant can be simulated by a **standard single-tape deterministic TM**

### Examples

* Multi-tape TM → Simulated using track encoding on one tape
* NTM → Simulated using systematic exploration (like BFS of computation tree)

### Conclusion

$$
	ext{All TM variants recognize the same class of languages}
$$

---

## 7. Important Observations

* Turing Machines define the class of **recursively enumerable languages**
* They form the basis of the **Church-Turing Thesis**
* They are used to study **decidability and computability**

---

## 8. Summary

* Turing Machine is the most powerful standard model of computation
* Uses an infinite tape and a read/write head
* Instantaneous Descriptions capture configurations
* Can recognize complex languages beyond context-free languages
* Variants like multi-tape and nondeterministic TMs do not increase computational power

