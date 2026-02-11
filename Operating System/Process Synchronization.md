# Process Synchronization

Process Synchronization is a core concept in **Operating Systems** that deals with the coordination of concurrent processes to ensure **correct, consistent, and predictable execution** when they share common resources.

Improper synchronization can lead to incorrect results, data inconsistency, and system instability.

---

## Critical Section Problem

### Critical Section

A **critical section** is a part of the program where shared resources (variables, files, memory) are accessed.

If multiple processes enter the critical section simultaneously, it can lead to inconsistency.

### Structure of a Process

```
do {
   Entry Section
   Critical Section
   Exit Section
   Remainder Section
} while (true);
```

### Requirements of Critical Section Problem

1. **Mutual Exclusion**
   Only one process can be in the critical section at a time.

2. **Progress**
   If no process is in the critical section, the decision of who enters next cannot be postponed indefinitely.

3. **Bounded Waiting**
   A process must not wait indefinitely to enter the critical section.

---

## Race Condition

A **race condition** occurs when multiple processes access and modify shared data simultaneously, and the final result depends on the **order of execution**.

### Example

Two processes increment the same variable `count` concurrently.

```
count = count + 1
```

This operation is not atomic and may produce incorrect results without synchronization.

---

## Mutual Exclusion

**Mutual Exclusion** ensures that only one process accesses the critical section at any given time.

### Why It Is Needed

* Prevents data inconsistency
* Ensures correctness
* Avoids race conditions

---

## Synchronization Mechanisms

---

## 1. Mutex Locks

### Definition

A **Mutex (Mutual Exclusion) Lock** allows only one process to access a critical section.

### Working

* `lock()` → Enter critical section
* `unlock()` → Exit critical section

### Characteristics

* Binary state (locked / unlocked)
* Busy waiting possible (spinlock)

### Pseudocode

```
lock(mutex);
critical section
unlock(mutex);
```

### Limitations

* Busy waiting wastes CPU cycles
* Risk of deadlock if not handled properly

---

## 2. Semaphores

### Definition

A **Semaphore** is a synchronization variable that controls access to shared resources.

### Types

* **Binary Semaphore** (0 or 1)
* **Counting Semaphore** (0 to n)

### Operations

```
wait(S)  // decrement
signal(S) // increment
```

### Working

* `wait()` blocks process if resource unavailable
* `signal()` wakes waiting process

### Advantages

* No busy waiting
* Suitable for multiple resource instances

### Disadvantages

* Complex to implement
* Programming errors may cause deadlock

---

## 3. Monitors

### Definition

A **Monitor** is a high-level synchronization construct that combines:

* Mutual exclusion
* Condition variables
* Resource management

### Characteristics

* Only one process can be active in a monitor at a time
* Easier to use than semaphores
* Supported by high-level languages

### Condition Variables

```
wait()
signal()
```

### Advantages

* Cleaner and safer than semaphores
* Less error-prone

---

## Classical Synchronization Problems

---

## 1. Producer–Consumer Problem

### Problem Description

* Producer produces data and places it in a buffer
* Consumer consumes data from the buffer
* Buffer has limited size

### Issues

* Producer should not produce if buffer is full
* Consumer should not consume if buffer is empty

### Solution Using Semaphores

* `mutex` → mutual exclusion
* `empty` → empty slots
* `full` → filled slots

<p align="center">
  <img 
    src="https://ocw.mit.edu/courses/6-004-computation-structures-spring-2017/a9b2e2d16758fa0c0e3fa62a4b217399_Slide15.png"
    alt="Critical Section Problem Diagram"
    width="600"
    height="350"
  >
</p>

### Key Insight

Ensures synchronization between producing and consuming processes without data loss.

---

## 2. Readers–Writers Problem

### Problem Description

* Multiple readers can read simultaneously
* Only one writer can write at a time
* Writer must have exclusive access

### Types

* **Readers Preference**
* **Writers Preference**

### Issues

* Starvation of writers or readers

<p align="center">
  <img 
    src="https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1678856087244-1-01%20%2817%29.png"
    alt="Critical Section Problem Diagram"
    width="600"
    height="350"
  >
</p>


### Solution

* Use semaphores and counters
* Ensure fairness using priority or queueing

---

## 3. Dining Philosophers Problem

### Problem Description

* Philosophers sit around a table
* Each needs two forks to eat
* Forks are shared between philosophers

### Problems Arising

* Deadlock
* Starvation


<p align="center">
  <img 
    src="https://upload.wikimedia.org/wikipedia/commons/8/81/Dining_philosophers_diagram.jpg"
    alt="Critical Section Problem Diagram"
    width="600"
    height="350"
  >
</p>


### Solutions

* Allow at most 4 philosophers to eat
* Pick forks in a fixed order
* Use monitors or semaphores

---

## Comparison of Synchronization Mechanisms

| Mechanism | Busy Waiting | Ease of Use | Deadlock Risk |
| --------- | ------------ | ----------- | ------------- |
| Mutex     | Yes          | Easy        | Medium        |
| Semaphore | No           | Moderate    | High          |
| Monitor   | No           | Easy        | Low           |

---

## Common Problems in Synchronization

* Deadlock
* Starvation
* Priority Inversion
* Livelock

---

## Exam and Interview Points

* Critical section must satisfy **ME, Progress, Bounded Waiting**
* Mutex is binary; semaphore can be counting
* Monitors are safer than semaphores
* Producer–Consumer uses **three semaphores**
* Dining Philosophers explains deadlock clearly

---

## Summary

Process Synchronization ensures:

* Correct execution of concurrent processes
* Protection of shared resources
* System reliability and consistency

It is one of the **most frequently asked topics** in OS interviews and competitive exams.

---

### Note

This document focuses on **conceptual clarity and classical problem understanding**, making it suitable for **exams, interviews, and system-level thinking**.

