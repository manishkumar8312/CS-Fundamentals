# 🖥️ Operating System


# Chapter 1: Introduction to Operating Systems

### Topics

* Definition and objectives of an Operating System
* Functions of an Operating System
* Types of Operating Systems

  * Batch OS
  * Time-Sharing OS
  * Distributed OS
  * Real-Time OS
* Operating System Structures

  * Monolithic Architecture
  * Layered Architecture
  * Microkernel Architecture
* System Calls
* Kernel Mode vs User Mode
* Interrupts and Traps
* Booting Process

---

# Chapter 2: Process Management

### Topics

* Process concept
* Process vs Program
* Process states and state transitions
* Process Control Block (PCB)
* Context Switching
* Process scheduling queues
* Process creation and termination
* Fork() and Exec() concepts
* Zombie and Orphan processes
* Inter-Process Communication (IPC)

  * Shared Memory
  * Message Passing

---

# Chapter 3: Thread Management

### Topics

* Thread concept
* Single-threaded vs Multi-threaded processes
* User-level threads
* Kernel-level threads
* Multithreading models
* Thread libraries (Pthreads)
* Thread vs Process comparison
* Multicore programming basics

---

# Chapter 4: CPU Scheduling

### Topics

* Scheduling objectives and criteria
* Preemptive vs Non-preemptive scheduling
* Scheduling metrics

  * Turnaround Time
  * Waiting Time
  * Response Time
  * Throughput
  * CPU Utilization
* CPU Scheduling Algorithms

  * FCFS
  * SJF
  * SRTF
  * Priority Scheduling
  * Round Robin
* Starvation and Aging
* Gantt chart–based numerical problems

---

# Chapter 5: Process Synchronization

### Topics

* Critical Section Problem
* Race Condition
* Mutual Exclusion
* Peterson’s Algorithm
* Test and Set instruction
* Spinlocks
* Synchronization mechanisms

  * Mutex Locks
  * Semaphores
  * Monitors
* Classical Synchronization Problems

  * Producer–Consumer
  * Readers–Writers
  * Dining Philosophers

---

# Chapter 6: Deadlocks

### Topics

* System model
* Deadlock characterization (Coffman conditions)
* Resource Allocation Graph (RAG)
* Safe State concept
* Deadlock prevention
* Deadlock avoidance

  * Banker’s Algorithm
* Deadlock detection
* Deadlock recovery

---

# Chapter 7: Memory Management (Most Important Section)

### Topics

* Memory management requirements
* Internal vs External fragmentation
* Contiguous memory allocation
* Memory allocation strategies

  * First Fit
  * Best Fit
  * Worst Fit
* Paging
* Segmentation
* Virtual Memory
* Demand Paging
* Copy-on-Write
* TLB (Translation Lookaside Buffer)
* Page replacement algorithms

  * FIFO
  * LRU
  * Optimal
* Belady’s Anomaly
* Working Set Model
* Thrashing

---

# Chapter 8: File System

### Topics

* File concepts and attributes
* File access methods
* Directory structures
* File allocation methods

  * Contiguous Allocation
  * Linked Allocation
  * Indexed Allocation
* Free space management
* Inode concept
* FAT vs NTFS (basic idea)
* Journaling file systems
* File protection and security

---

# Chapter 9: I/O Management

### Topics

* I/O hardware
* I/O software
* Interrupt-driven I/O
* Direct Memory Access (DMA)
* Buffering and Caching
* Disk scheduling
* Disk scheduling algorithms

  * FCFS
  * SSTF
  * SCAN
  * C-SCAN
  * LOOK

---

# Chapter 10: Protection and Security

### Topics

* Goals of protection
* Domain of protection
* Access Matrix model
* Authentication and Authorization
* CIA Triad

  * Confidentiality
  * Integrity
  * Availability
* Security threats and vulnerabilities
* Malware types

  * Virus
  * Worm
  * Trojan
* Basics of Cryptography

  * Symmetric Encryption
  * Asymmetric Encryption

---
## ⭐ Support

If this repository adds value to your learning, consider giving it a ⭐ to show your support.