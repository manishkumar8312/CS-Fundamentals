# Chapter 11: Numerical Topics in Computer Networks

This document provides a structured overview of essential numerical problems in computer networking. It is intended for students, educators, and practitioners who wish to develop proficiency through example problems and solutions. The following five topics are covered in detail.

## Topics Covered

1. **Subnetting** – IPv4 addressing, subnet masks, CIDR, VLSM, network and broadcast address calculation.
2. **Transmission Delay and Propagation Delay** – Packet transmission time, signal propagation time, and total latency.
3. **Bandwidth–Delay Product** – Link capacity multiplied by round‑trip time, buffering requirements, and window size optimisation.
4. **CRC (Cyclic Redundancy Check)** – Polynomial arithmetic, modulo‑2 division, error detection, and generator polynomials.
5. **Sliding Window Protocol** – Go‑Back‑N, Selective Repeat, window size, sequence number space, and throughput computation.

Each section includes:
- Key formulas with clear notation.
- Step‑by‑step worked examples.
- Practice problems (solutions provided in the `/solutions` directory).
- Python scripts for automation (located in `/scripts`).

---

## 1. Subnetting

### Key Formulas
- Number of subnets = 2<sup>s</sup>, where `s` is the number of borrowed bits.
- Hosts per subnet = 2<sup>h</sup> – 2, where `h` is the number of host bits remaining.
- Subnet mask = network prefix with `s` additional 1s.
- Block size (address increment) = 2<sup>h</sup>.

### Example Problem
**Given:** 192.168.1.0/24, need 4 subnets.  
**Solution:**  
- Borrow `s = log2(4) = 2` bits.  
- New subnet mask = /26 (255.255.255.192).  
- Host bits remaining `h = 6` → hosts per subnet = 2<sup>6</sup> – 2 = 62.  
- Subnet addresses: 192.168.1.0, 64, 128, 192.

---

## 2. Transmission Delay and Propagation Delay

### Key Formulas
- Transmission delay = `L / R`  
  (L = packet length in bits, R = link transmission rate in bps)
- Propagation delay = `d / s`  
  (d = physical distance, s = signal propagation speed, typically 2×10<sup>8</sup> m/s for copper/fibre)
- Total latency = Transmission delay + Propagation delay + queuing + processing (queuing/processing often omitted in basic problems)

### Example Problem
**Given:** Packet length 1500 bytes, link speed 10 Mbps, distance 2000 km, propagation speed 2×10<sup>8</sup> m/s.  
**Solution:**  
- Transmission delay = (1500 × 8) / (10×10<sup>6</sup>) = 0.0012 s = 1.2 ms.  
- Propagation delay = 2000×10<sup>3</sup> / (2×10<sup>8</sup>) = 0.01 s = 10 ms.  
- Total latency = 1.2 + 10 = 11.2 ms.

---

## 3. Bandwidth–Delay Product

### Key Formula
- Bandwidth–delay product (BDP) = Bandwidth (bps) × Round‑Trip Time (RTT in seconds)  
  Units: bits (or bytes when divided by 8).

### Significance
BDP represents the amount of data “in flight” on the link before the sender receives an acknowledgment. It determines the minimum window size required for full link utilisation.

### Example Problem
**Given:** Bandwidth = 100 Mbps, RTT = 50 ms.  
**Solution:**  
BDP = 100×10<sup>6</sup> × 0.05 = 5×10<sup>6</sup> bits = 625,000 bytes.  
To saturate the link, the sender’s window should be at least 625,000 bytes (or approximately 417 packets of 1500 bytes).

---

## 4. Cyclic Redundancy Check (CRC)

### Key Concepts
- CRC uses polynomial division (modulo‑2) to generate a checksum.
- Sender appends `n` check bits (where `n` = degree of generator polynomial).
- Receiver divides received data by the same generator; remainder zero indicates no error.

### Procedure
1. Append `n` zero bits to the data word (where `n` = degree of generator polynomial).
2. Divide the augmented data by the generator polynomial using XOR (modulo‑2 division).
3. The remainder (of length `n`) is the CRC checksum.
4. Transmit original data followed by the checksum.
5. Receiver performs division; if remainder ≠ 0, error detected.

### Example Problem
**Given:** Data = `110101`, Generator = `1011` (degree 3).  
**Solution (steps):**  
- Append 3 zeros: `110101000`.  
- Divide by `1011` using XOR:  
  (Detailed division yields remainder `011`).  
- Transmitted frame: `110101011`.  
- At receiver, division by `1011` gives remainder `000` → no error.

---

## 5. Sliding Window Protocol

### Key Formulas
- Maximum window size (Go‑Back‑N) = 2<sup>n</sup> – 1, where `n` = number of bits in sequence number field.
- Maximum window size (Selective Repeat) = 2<sup>n‑1</sup>.
- Throughput = (Window size × Packet size) / RTT, provided window ≤ BDP.

### Example Problem (Go‑Back‑N)
**Given:** 3‑bit sequence number (0–7), RTT = 200 ms, packet size = 1000 bytes, bandwidth = 2 Mbps.  
**Solution:**  
- Max window size = 2<sup>3</sup> – 1 = 7 packets.  
- BDP = 2×10<sup>6</sup> × 0.2 = 400,000 bits = 50,000 bytes = 50 packets (of 1000 bytes).  
- Window (7 packets) is smaller than BDP (50 packets), so link is not fully utilised.  
- Throughput = (7 × 1000 × 8) / 0.2 = 280,000 bps = 0.28 Mbps.

---

## Usage

1. Study the formulas and worked examples in each section.
2. Attempt the practice problems located in `/problems`.
3. Verify your answers using the solution guides in `/solutions`.
4. Use the Python scripts in `/scripts` to automate calculations and test edge cases.

## Contribution

Contributions are welcome. Please ensure that all additions include clear derivations, maintain a professional tone, and include test cases where applicable.

## License

This content is provided under the MIT License. You are free to use, modify, and distribute it with proper attribution.
