# CPU Scheduling

CPU Scheduling is a fundamental concept in **Operating Systems** that determines how processes are allocated CPU time when multiple processes are present in the system. Efficient scheduling improves CPU utilization, throughput, and overall system performance.

---

## Scheduling Objectives and Criteria

### Objectives

* Maximize CPU utilization
* Maximize throughput
* Minimize turnaround time
* Minimize waiting time
* Minimize response time
* Ensure fairness and avoid starvation

### Scheduling Criteria

* **Arrival Time (AT):** Time when a process enters the ready queue
* **Burst Time (BT):** CPU time required by the process
* **Completion Time (CT):** Time when execution finishes
* **Turnaround Time (TAT):**

  ```
  TAT = CT − AT
  ```
* **Waiting Time (WT):**

  ```
  WT = TAT − BT
  ```
* **Response Time (RT):**

  ```
  RT = First CPU Allocation − AT
  ```

---

## Preemptive vs Non-Preemptive Scheduling

### Non-Preemptive

Once the CPU is allocated, the process runs until completion or blocking.

* FCFS
* Non-preemptive SJF
* Non-preemptive Priority

### Preemptive

CPU can be taken away from a running process.

* SRTF
* Preemptive Priority
* Round Robin

---

## CPU Scheduling Algorithms with Solved Numericals

---

## 1. First Come First Serve (FCFS)

### Description

Processes execute in the order of arrival. It is simple but inefficient due to the **convoy effect**.

### Example

| Process | AT | BT |
| ------- | -- | -- |
| P1      | 0  | 4  |
| P2      | 1  | 3  |
| P3      | 2  | 5  |

### Gantt Chart

```
| P1 | P2 | P3 |
0    4    7    12
```

### Calculations

| Process | CT | TAT | WT |
| ------- | -- | --- | -- |
| P1      | 4  | 4   | 0  |
| P2      | 7  | 6   | 3  |
| P3      | 12 | 10  | 5  |

* Average WT = **2.67**
* Average TAT = **6.67**

---

## 2. Shortest Job First (SJF – Non-Preemptive)

### Description

The process with the smallest burst time executes first. It provides **minimum average waiting time**.

### Example

| Process | AT | BT |
| ------- | -- | -- |
| P1      | 0  | 7  |
| P2      | 2  | 4  |
| P3      | 4  | 1  |
| P4      | 5  | 4  |

### Gantt Chart

```
| P1 | P3 | P2 | P4 |
0    7    8    12   16
```

### Calculations

| Process | CT | TAT | WT |
| ------- | -- | --- | -- |
| P1      | 7  | 7   | 0  |
| P2      | 12 | 10  | 6  |
| P3      | 8  | 4   | 3  |
| P4      | 16 | 11  | 7  |

* Average WT = **4**
* Average TAT = **8**

---

## 3. Shortest Remaining Time First (SRTF)

### Description

Preemptive version of SJF. CPU is always assigned to the process with the **least remaining time**.

### Example

| Process | AT | BT |
| ------- | -- | -- |
| P1      | 0  | 8  |
| P2      | 1  | 4  |
| P3      | 2  | 2  |
| P4      | 3  | 1  |

### Gantt Chart

```
| P1 | P2 | P3 | P4 | P2 | P1 |
0    1    2    4    5    7    14
```

### Calculations

| Process | CT | TAT | WT |
| ------- | -- | --- | -- |
| P1      | 14 | 14  | 6  |
| P2      | 7  | 6   | 2  |
| P3      | 4  | 2   | 0  |
| P4      | 5  | 2   | 1  |

* Average WT = **2.25**
* Average TAT = **6**

---

## 4. Priority Scheduling (Non-Preemptive)

### Description

CPU is allocated based on priority. Lower number indicates higher priority.

### Example

| Process | AT | BT | Priority |
| ------- | -- | -- | -------- |
| P1      | 0  | 6  | 2        |
| P2      | 1  | 4  | 1        |
| P3      | 2  | 5  | 3        |

### Execution Order

```
P1 → P2 → P3
```

### Calculations

| Process | CT | TAT | WT |
| ------- | -- | --- | -- |
| P1      | 6  | 6   | 0  |
| P2      | 10 | 9   | 5  |
| P3      | 15 | 13  | 8  |

* **Starvation possible**
* **Aging** is used to prevent starvation

---

## 5. Round Robin Scheduling

### Description

Each process gets CPU for a fixed **time quantum** in a cyclic order. Suitable for **time-sharing systems**.

### Example

Time Quantum = **2**

| Process | AT | BT |
| ------- | -- | -- |
| P1      | 0  | 5  |
| P2      | 1  | 4  |
| P3      | 2  | 2  |

### Gantt Chart

```
| P1 | P2 | P3 | P1 | P2 | P1 |
0    2    4    6    8    10   11
```

### Calculations

| Process | CT | TAT | WT |
| ------- | -- | --- | -- |
| P1      | 11 | 11  | 6  |
| P2      | 10 | 9   | 5  |
| P3      | 6  | 4   | 2  |

---

## Starvation and Aging

* **Starvation:** A process waits indefinitely due to scheduling policy
* **Aging:** Gradually increases priority of waiting processes to ensure fairness

---

## Algorithm Comparison

| Algorithm   | Preemptive | Starvation | Best Use Case         |
| ----------- | ---------- | ---------- | --------------------- |
| FCFS        | No         | No         | Batch systems         |
| SJF         | No         | Yes        | Optimal waiting time  |
| SRTF        | Yes        | Yes        | Time-critical systems |
| Priority    | Both       | Yes        | Real-time systems     |
| Round Robin | Yes        | No         | Time-sharing systems  |

---

## Key Exam and Interview Points

* SJF provides minimum average waiting time
* Round Robin improves response time
* Aging prevents starvation
* Always compute **CT → TAT → WT** in numericals

---

## Visual Reference (Optional)

![Image](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter5/5_DeterministicChart.jpg)

![Image](https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1672308972553-Round%20Robin%20Scheduling%20Program%20in%20C13.png)

---

### Note

This document focuses on **conceptual clarity, numericals, and interview readiness**, avoiding unnecessary complexity.

