# 🖥️ Operating System Syllabus

A structured and exam-oriented syllabus covering all fundamental concepts of **Operating Systems**, suitable for **B.Tech CSE**, **GATE**, and **technical interviews**.

---

## 1. Introduction to Operating Systems

<p align="center">
  <img src="https://images.openai.com/static-rsc-3/eSqr15h_mLNyuDA4EkHENHCr4qbprs0KIrR775L8AqMSyf2M7hCxGQdDn1PlYv24eWvD9tHxUL6YATEjteF1VUHxzfCLSb2qv_vffcJ1EI0?purpose=fullsize" width="45%"/>
  <img src="https://images.openai.com/static-rsc-3/9rrzPa82tWLLf8ZBijRV6YreksaYxD8FvprTCdzez1keS0LjUcPwxGXPAMgg8RQgGGqCLrvDRm-btK5KGQI4CqpEGqrLRW1FQEVPaZSv9CA?purpose=fullsize" width="45%"/>
</p>

### Topics
- Definition and objectives of an Operating System
- Functions of an Operating System
- Types of Operating Systems  
  - Batch Operating Systems  
  - Time-Sharing Operating Systems  
  - Distributed Operating Systems  
  - Real-Time Operating Systems
- Operating System Structures  
  - Monolithic Structure  
  - Layered Structure  
  - Microkernel Architecture  

---

## 2. Process Management

<p align="center">
  <img src="https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter3/3_02_ProcessState.jpg" width="45%"/>
  <img src="https://scaler.com/topics/images/structure-of-process-control-block.webp" width="45%"/>
</p>

### Topics
- Process concept
- Process vs Program
- Process states and state transitions
- Process Control Block (PCB)
- Context switching
- Process creation and termination
- Inter-Process Communication (IPC)

---

## 3. Thread Management

### Topics
- Thread concept
- Single-threaded and multi-threaded processes
- User-level threads
- Kernel-level threads
- Multithreading models

---

## 4. CPU Scheduling

<p align="center">
  <img src="https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter5/5_DeterministicChart.jpg" width="45%"/>
  <img src="https://figures.semanticscholar.org/108fdfb49867dcacb8a7894962e45088005c9c72/8-TableI-1.png" width="45%"/>
</p>

### Topics
- Scheduling objectives and criteria
- Preemptive and non-preemptive scheduling
- CPU scheduling algorithms  
  - First Come First Serve (FCFS)  
  - Shortest Job First (SJF)  
  - Shortest Remaining Time First (SRTF)  
  - Priority Scheduling  
  - Round Robin Scheduling
- Starvation and aging
- Gantt chart–based numerical problems

---

## 5. Process Synchronization

<p align="center">
  <img src="https://www.tutorialspoint.com/operating_system/images/os_critical_section.jpg" width="45%"/>
  <img src="https://fiveable.me/_next/image?q=75&url=https%3A%2F%2Fstorage.googleapis.com%2Fstatic.prod.fiveable.me%2Fsearch-images%252F%2522Synchronization_primitives_in_operating_systems%253A_semaphores_mutexes_monitors_and_their_roles_in_concurrency.%2522-81738215139404631492.png&w=3840" width="45%"/>
</p>

### Topics
- Critical section problem
- Race condition
- Mutual exclusion
- Synchronization mechanisms  
  - Mutex locks  
  - Semaphores  
  - Monitors
- Classical synchronization problems  
  - Producer–Consumer  
  - Readers–Writers  
  - Dining Philosophers

---

## 6. Deadlocks

<p align="center">
  <img src="https://static.afteracademy.com/images/what-is-deadlock-and-what-are-its-four-necessary-conditions-deadlock-example.png" width="45%"/>
  <img src="https://www.boardinfinity.com/blog/content/images/2022/11/Your-paragraph-text--50-.jpg" width="45%"/>
</p>

### Topics
- System model
- Deadlock characterization
- Deadlock prevention
- Deadlock avoidance  
  - Banker’s Algorithm
- Deadlock detection
- Deadlock recovery

---

## 7. Memory Management

<p align="center">
  <img src="https://assets.enterprisestorageforum.com/uploads/2021/02/paging-and-segmentation_6019c4f207ec5.png" width="45%"/>
  <img src="https://www.researchgate.net/publication/380941775/figure/tbl1/AS%3A11431281247918521%401716989407322/Comparison-of-Page-Replacement-algorithms.png" width="45%"/>
</p>

### Topics
- Memory management requirements
- Contiguous memory allocation
- Memory allocation strategies  
  - First Fit  
  - Best Fit  
  - Worst Fit
- Paging
- Segmentation
- Virtual memory
- Demand paging
- Page replacement algorithms  
  - FIFO  
  - LRU  
  - Optimal
- Thrashing

---

## 8. File System

<p align="center">
  <img src="https://raw.githubusercontent.com/Codecademy/docs/main/media/file-system-structure.png" width="45%"/>
  <img src="https://www.scaler.com/topics/images/file-allocation-methods-in-os_thumbnail.webp" width="45%"/>
</p>

### Topics
- File concepts and attributes
- File access methods
- Directory structures
- File allocation methods  
  - Contiguous allocation  
  - Linked allocation  
  - Indexed allocation
- Free space management
- File protection and security

---

## 9. I/O Management

<p align="center">
  <img src="https://almablog-media.s3.ap-south-1.amazonaws.com/Image_1_9f9c22b338.png" width="45%"/>
  <img src="https://assets.omscs.io/notes/38B48ADB-1EC5-4771-A87B-92D9102ADA69.png" width="45%"/>
</p>

### Topics
- I/O hardware
- I/O software
- Disk scheduling
- Disk scheduling algorithms  
  - FCFS  
  - SSTF  
  - SCAN  
  - C-SCAN  
  - LOOK

---

## 10. Protection and Security

### Topics
- Goals of protection
- Domain of protection
- Access matrix
- Authentication and authorization
- Security threats and vulnerabilities

---

⭐ **Star this repository if you find it helpful**
