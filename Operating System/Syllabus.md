# OPERATING SYSTEMS

## Chapter 1: Introduction to Operating Systems

* What is an Operating System?
* Roles of an OS: resource manager, virtual machine, interface
* Computer system architecture: CPU, memory, I/O devices
* OS structure: monolithic, layered, microkernel, hybrid
* User mode vs kernel mode
* System calls and API
* OS services and utilities
* Booting process

---

## Chapter 2: Process Management

* Process concept: program vs process
* Process states: new, ready, running, waiting, terminated
* Process Control Block (PCB)
* Process scheduling queues
* Context switching
* Process creation and termination (fork, exec, wait, exit)
* Process hierarchies
* Process vs thread
* User-level threads vs kernel-level threads
* Multithreading models: many-to-one, one-to-one, many-to-many

---

## Chapter 3: CPU Scheduling

* Scheduling criteria: CPU utilization, throughput, turnaround time, waiting time, response time
* Preemptive vs non-preemptive scheduling
* Scheduling algorithms:

  * First-Come, First-Served (FCFS)
  * Shortest Job First (SJF) – non-preemptive and preemptive (SRTF)
  * Round Robin (RR)
  * Priority scheduling (with aging)
  * Multilevel queue scheduling
  * Multilevel feedback queue

* Thread scheduling
* Real-time scheduling (rate-monotonic, earliest deadline first)

---

## Chapter 4: Process Synchronization

* Critical section problem
* Solution requirements: mutual exclusion, progress, bounded waiting
* Software solutions: Peterson’s algorithm
* Hardware support: test-and-set, compare-and-swap
* Mutex locks and spinlocks
* Semaphores (binary and counting)
* Classical synchronization problems:

  * Bounded buffer (producer-consumer)
  * Readers-writers
  * Dining philosophers
  * Sleeping barber

* Monitors and condition variables
* Synchronization in POSIX threads (mutex, condition variables)

---

## Chapter 5: Deadlocks

* Deadlock characterization: mutual exclusion, hold and wait, no preemption, circular wait
* Resource allocation graph
* Methods for handling deadlocks:

  * Deadlock prevention (breaking the four conditions)
  * Deadlock avoidance (Banker’s algorithm)
  * Deadlock detection (with recovery)
  * Deadlock ignorance (Ostrich algorithm)

---

## Chapter 6: Memory Management

* Memory hierarchy
* Address binding: compile time, load time, execution time
* Logical vs physical address space
* Memory allocation:

  * Contiguous allocation (fixed and dynamic partitions)
  * External and internal fragmentation
  * Compaction

* Paging:

  * Page table (PTE: frame number, dirty, valid, reference bits)
  * Address translation
  * Multi-level page tables
  * Inverted page tables
  * Translation Lookaside Buffer (TLB)

* Segmentation:

  * Segment table
  * Segmentation with paging (Intel x86)

---

## Chapter 7: Virtual Memory

* Demand paging
* Page fault handling
* Copy-on-write
* Page replacement algorithms:

  * FIFO (Belady’s anomaly)
  * Optimal (MIN)
  * LRU (Least Recently Used)
  * Clock (Second-Chance)
  * LFU, MFU

* Thrashing and working set model
* Page size selection
* TLB reach and coverage
* Memory-mapped files

---

## Chapter 8: File Systems

* File concept: attributes, operations, types
* Directory structure: single-level, two-level, tree-structured, acyclic graph, general graph
* File system mounting
* File allocation methods:

  * Contiguous allocation
  * Linked allocation (FAT)
  * Indexed allocation (i-node)

* Free space management:

  * Bit vector
  * Linked list
  * Grouping
  * Counting

* Disk scheduling:

  * FCFS, SSTF, SCAN, C-SCAN, LOOK, C-LOOK

* File system layout (boot block, superblock, inode blocks, data blocks)
* Journaling and log-structured file systems
* File system examples: ext4, NTFS, FAT32

---

## Chapter 9: Input/Output Systems

* I/O hardware: ports, buses, controllers
* Polling vs interrupts
* Direct Memory Access (DMA)
* I/O software layers: interrupt handlers, device drivers, device-independent I/O, user-space I/O
* Buffering, caching, spooling
* Block and character devices
* Disk structure (tracks, cylinders, sectors)
* RAID levels (0, 1, 5, 6, 10)

---

## Chapter 10: Security and Protection

* Security goals: confidentiality, integrity, availability
* Authentication: passwords, biometrics, two-factor
* Access control: DAC, MAC, RBAC
* Protection mechanisms: capabilities, access matrix
* Principle of least privilege
* Malicious software: viruses, worms, trojans, rootkits
* Buffer overflow attacks and defenses
* Encryption basics for OS security (full-disk encryption)

---

## Chapter 11: Virtualization and Cloud Computing

* Virtual machine concepts: hypervisors (Type 1, Type 2)
* Virtualization vs emulation
* Para-virtualization and hardware-assisted virtualization
* Containers vs virtual machines (Docker, LXC)
* Cloud computing models: IaaS, PaaS, SaaS
* Challenges: isolation, performance, security

---

## Chapter 12: Distributed Operating Systems (Overview)

* Distributed system models (client-server, peer-to-peer)
* Remote Procedure Call (RPC) and message passing
* Network transparency and naming
* Distributed synchronization (Lamport clocks, vector clocks)
* Distributed mutual exclusion (centralized, distributed, token-based)
* Distributed file systems (NFS, AFS)
* Consensus (Paxos, Raft - conceptual)

---


## Chapter 13: Advanced Topics

* Real-time operating systems (RTOS): VxWorks, FreeRTOS
* Embedded operating systems
* Mobile OS features (power management, sensors)
* System performance profiling (perf, DTrace)
* Fault tolerance and check-pointing

---

## Support

If this syllabus helps you master Operating Systems, consider giving the repository a star. Contributions, corrections, and additional project ideas are always welcome.