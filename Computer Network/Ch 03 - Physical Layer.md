## Chapter 3: Physical Layer

### 1. Transmission Media

#### 1.1 Guided Media (Wired)

```mermaid
    flowchart TD
        A[Guided Media] --> B[Twisted Pair]
        A --> C[Coaxial Cable]
        A --> D[Optical Fiber]

        B --> B1[UTP Unshielded]
        B --> B2[STP Shielded]
        B1 -.-> B1a[Cat5e, Cat6]

        C --> C1[Baseband Digital]
        C --> C2[Broadband Analog]

        D --> D1[Single-mode Long distance]
        D --> D2[Multi-mode Short distance]
```

#### 1.2 Unguided Media (Wireless)

```mermaid
flowchart LR
    subgraph Wireless
        R[Radio Waves<br/>3 kHz – 1 GHz<br/>Omnidirectional]
        M[Microwaves<br/>1 GHz – 300 GHz<br/>Directional / Line-of-sight]
        I[Infrared<br/>300 GHz – 400 THz<br/>Short range]
    end
```

---

### 2. Signal Types: Analog vs Digital
**Digital Signal:** A digital signal is a discrete signal that represents data using specific values, usually in binary form (0 and 1). It changes in steps rather than continuously. Digital signals are less affected by noise, easier to store, process, and transmit, and are widely used in computers and modern communication systems.
*Digital signal representation using state diagram* – each state is a voltage level over a bit interval:

```mermaid
stateDiagram-v2
    [*] --> Bit1_High : Bit 1
    Bit1_High --> Bit0_Low : Bit 0
    Bit0_Low --> Bit1_High : Bit 1
    Bit1_High --> Bit1_High2 : Bit 1
    Bit1_High2 --> Bit0_Low2 : Bit 0
    Bit0_Low2 --> [*]
    note right of Bit1_High : +V
    note right of Bit0_Low : -V
```
**Analog Signal:** An analog signal is a continuous signal that varies smoothly with time. It can take an infinite number of values within a given range. These signals represent real-world physical quantities such as sound, temperature, and light. However, analog signals are more prone to noise and distortion during transmission.

---

### 3. Transmission Modes

```mermaid
sequenceDiagram
    participant A as Device A
    participant B as Device B

    Note over A,B: Simplex (A → B only)
    A->>B: Data
    Note right of B: B cannot send

    Note over A,B: Half-duplex (one at a time)
    A->>B: Data
    B-->>A: Ack (after A finishes)

    Note over A,B: Full-duplex (simultaneous)
    A->>B: Data
    B->>A: Data
```

---

### 4. Line Coding Techniques

Instead of `gantt`, I use **state diagrams** to show voltage levels over time.

#### 4.1 NRZ‑L (Non‑Return to Zero, Level)

Bits: `1 0 1 1 0 0 1`  
Voltage: `+V` for 1, `-V` for 0.

```mermaid
stateDiagram-v2
    [*] --> Vplus : Bit 1 (+V)
    Vplus --> Vminus : Bit 0 (-V)
    Vminus --> Vplus : Bit 1 (+V)
    Vplus --> Vplus2 : Bit 1 (+V)
    Vplus2 --> Vminus2 : Bit 0 (-V)
    Vminus2 --> Vminus3 : Bit 0 (-V)
    Vminus3 --> Vplus3 : Bit 1 (+V)
    Vplus3 --> [*]
```

#### 4.2 Manchester Coding (IEEE 802.3)

Each bit has a mid‑bit transition:  
- `1` = high→low  
- `0` = low→high

Bits: `1 0 1 0`

```mermaid
stateDiagram-v2
    [*] --> High1 : Bit1 start high
    High1 --> Low1 : mid transition (1)
    Low1 --> Low2 : Bit0 start low
    Low2 --> High2 : mid transition (0)
    High2 --> Low3 : Bit1 start high
    Low3 --> High3 : mid transition (1)
    High3 --> Low4 : Bit0 start high?
    Low4 --> [*]
```

*Simpler view* – use a table:

| Bit | Start level | Mid transition | End level |
|-----|-------------|----------------|-----------|
| 1   | High        | → Low          | Low       |
| 0   | Low         | → High         | High      |
| 1   | High        | → Low          | Low       |
| 0   | Low         | → High         | High      |

#### 4.3 Bipolar AMI (Alternate Mark Inversion)

- `0` → 0V  
- `1` → alternating +V and -V  

Bits: `1 0 1 1 0 1`

```mermaid
stateDiagram-v2
    [*] --> Plus : Bit1 (+V)
    Plus --> Zero : Bit0 (0V)
    Zero --> Minus : Bit1 (-V)
    Minus --> Plus2 : Bit1 (+V)
    Plus2 --> Zero2 : Bit0 (0V)
    Zero2 --> Minus2 : Bit1 (-V)
    Minus2 --> [*]
```

---

### 5. Data Rate Concepts

#### 5.1 Nyquist Theorem (Noiseless)

Formula:

```text
C = 2B log2(L)  | B = Bandwidth, L = number of levels,C = Capacity
```

#### 5.2 Shannon Capacity (Noisy)

Formula:

```text
C = B log2(1 + S/N) | C = Capacity, B = Bandwidth, S/N = Signal to Noise Ratio
```

**Relationship diagram** – using a flowchart:

```mermaid
flowchart TD
    subgraph NYQ[Nyquist Theorem]
        N1["Max symbol rate = 2B symbols/s"]
        N2["With L levels: C = 2B log2(L)"]
    end
    subgraph SHN[Shannon Capacity]
        S1["Max bits/s given SNR"]
        S2["C = B log2(1 + S/N)"]
    end
    PRAC["Actual data rate <= min(Nyquist, Shannon)"]
    NYQ --> PRAC
    SHN --> PRAC
```

**Key insight**:  
- Nyquist tells how fast you can send symbols (no noise).  
- Shannon tells how many bits per symbol you can actually use (with noise).  

**Example**: Telephone line with B = 3.1 kHz, SNR = 30 dB (S/N = 1000)  
- Shannon: C ≈ 3100 × log₂(1001) ≈ 30.9 kbps  
- Nyquist with L=4 (2 bits/symbol): C = 2×3100×2 = 12.4 kbps  
→ The channel is limited by Nyquist if you only use 4 levels. With better SNR you could increase L, but noise limits L to √(1+S/N) ≈ 31.6, giving Nyquist C ≈ 2×3100×log₂(31.6) ≈ 30.9 kbps – same as Shannon.

---

## Summary Table

| Concept | Formula | Limiting Factor |
|---------|---------|----------------|
| **Nyquist** | C = 2B log2(L) | Bandwidth & number of levels |
| **Shannon** | C = B log2(1+S/N) | Bandwidth & SNR |

---
