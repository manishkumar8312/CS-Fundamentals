# Deadlocks

A **deadlock** is a situation in an operating system where a set of processes are **permanently blocked** because each process is holding one or more resources and is waiting for resources held by other processes in the same set.

Deadlocks usually occur in systems where **multiple processes compete for limited shared resources**.

---

## 1. System Model

The system consists of:

* A finite number of **processes**
* A finite number of **resource types**

### Resource Types

* **Reusable resources**: CPU, memory, files, I/O devices
* **Consumable resources**: Signals, messages, interrupts

### Resource Usage Sequence

A process follows this order:

1. Request resource
2. Use resource
3. Release resource

If a resource is unavailable, the requesting process must **wait**.

---

## 2. Deadlock Characterization

A deadlock occurs **if and only if** the following **four necessary conditions** hold simultaneously.

### 1. Mutual Exclusion

At least one resource must be **non-shareable**, meaning only one process can use it at a time.

### 2. Hold and Wait

A process is holding at least one resource and waiting for additional resources.

### 3. No Preemption

Resources cannot be forcibly taken from a process; they must be released voluntarily.

### 4. Circular Wait

A circular chain of processes exists where each process is waiting for a resource held by the next process.

If **any one** of these conditions is prevented, a deadlock **cannot occur**.

---

## 3. Deadlock Prevention

Deadlock prevention ensures that **at least one of the four necessary conditions never holds**.

### Prevention Techniques

| Condition        | Prevention Strategy                              |
| ---------------- | ------------------------------------------------ |
| Mutual Exclusion | Make resources sharable where possible           |
| Hold and Wait    | Force processes to request all resources at once |
| No Preemption    | Preempt resources when a process waits           |
| Circular Wait    | Impose a strict ordering of resources            |

### Disadvantages

* Poor resource utilization
* Reduced system throughput
* Not practical for large systems

---

## 4. Deadlock Avoidance

Deadlock avoidance requires **advance information** about resource requirements and ensures the system never enters an **unsafe state**.

### Safe State

A system is in a **safe state** if there exists a sequence of processes such that each process can complete execution without leading to deadlock.

### Unsafe State

* Not necessarily deadlock
* But may lead to deadlock

Deadlock avoidance dynamically checks every resource request before granting it.

---

## 5. Banker’s Algorithm

Banker’s Algorithm is a **deadlock avoidance algorithm** that determines whether granting a resource request keeps the system in a safe state.

### Data Structures Used

* **Available**: Number of available instances of each resource
* **Max**: Maximum demand of each process
* **Allocation**: Resources currently allocated
* **Need**: Remaining resources required

  ```
  Need = Max − Allocation
  ```

### Algorithm Steps

1. Check if `Request ≤ Need`
2. Check if `Request ≤ Available`
3. Temporarily allocate resources
4. Check for a safe sequence
5. Grant request only if system remains safe

### Limitations

* Requires prior knowledge of maximum resource needs
* High overhead
* Not suitable for real-time systems

---

## 6. Deadlock Detection

Instead of preventing or avoiding deadlocks, the system:

* Allows deadlocks to occur
* Periodically checks for deadlocks

### Detection Techniques

* **Single instance per resource**: Use **Wait-For Graph**
* **Multiple instances**: Use detection algorithm similar to Banker’s

### Wait-For Graph

* Nodes represent processes
* Edge `Pi → Pj` means `Pi` is waiting for `Pj`
* A cycle in the graph indicates a deadlock

---

## 7. Deadlock Recovery

Once a deadlock is detected, the system must recover.

### Recovery Methods

#### 1. Process Termination

* Abort all deadlocked processes
* Abort one process at a time until deadlock is resolved

Criteria for selection:

* Process priority
* Resources held
* Execution time remaining

---

#### 2. Resource Preemption

* Select a victim process
* Preempt its resources
* Rollback process to a safe state

### Problems in Recovery

* Starvation
* Rollback overhead
* Selecting correct victim process

---

## Comparison of Deadlock Handling Techniques

| Technique  | Deadlock Occurrence | Overhead |
| ---------- | ------------------- | -------- |
| Prevention | Never               | High     |
| Avoidance  | Never               | Moderate |
| Detection  | Possible            | Low      |
| Recovery   | After detection     | Moderate |

---

## Key Exam and Interview Points

* All **four conditions** must hold for deadlock
* Breaking circular wait is the easiest prevention method
* Banker’s Algorithm ensures safe state
* Detection uses wait-for graph
* Recovery may cause starvation

---

## Summary

Deadlocks are a critical issue in operating systems involving **resource contention and concurrency**.
Understanding prevention, avoidance, detection, and recovery techniques is essential for **system design and examinations**.

---

⭐ **Star this repository if you find it helpful**


