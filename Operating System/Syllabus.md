## **Operating System Syllabus**

![Image](https://images.openai.com/static-rsc-3/eSqr15h_mLNyuDA4EkHENHCr4qbprs0KIrR775L8AqMSyf2M7hCxGQdDn1PlYv24eWvD9tHxUL6YATEjteF1VUHxzfCLSb2qv_vffcJ1EI0?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-3/9rrzPa82tWLLf8ZBijRV6YreksaYxD8FvprTCdzez1keS0LjUcPwxGXPAMgg8RQgGGqCLrvDRm-btK5KGQI4CqpEGqrLRW1FQEVPaZSv9CA?purpose=fullsize)

---

### **1. Introduction to Operating Systems**

* Definition and objectives of an Operating System
* Functions of an Operating System
* Types of Operating Systems

  * Batch Operating Systems
  * Time-Sharing Operating Systems
  * Distributed Operating Systems
  * Real-Time Operating Systems
* Operating System Structures

  * Monolithic Structure
  * Layered Structure
  * Microkernel Architecture

---

### **2. Process Management**

![Image](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter3/3_02_ProcessState.jpg)

![Image](https://scaler.com/topics/images/structure-of-process-control-block.webp)

* Process concept
* Process vs Program
* Process states and state transitions
* Process Control Block (PCB)
* Context switching
* Process creation and termination
* Inter-Process Communication (IPC)

---

### **3. Thread Management**

* Thread concept
* Single-threaded and multi-threaded processes
* User-level threads
* Kernel-level threads
* Multithreading models

---

### **4. CPU Scheduling**

![Image](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter5/5_DeterministicChart.jpg)

![Image](https://figures.semanticscholar.org/108fdfb49867dcacb8a7894962e45088005c9c72/8-TableI-1.png)

* Scheduling objectives and criteria
* Preemptive and non-preemptive scheduling
* CPU scheduling algorithms

  * First Come First Serve (FCFS)
  * Shortest Job First (SJF)
  * Shortest Remaining Time First (SRTF)
  * Priority Scheduling
  * Round Robin Scheduling
* Starvation and aging
* Gantt chart–based problems

---

### **5. Process Synchronization**

![Image](https://www.tutorialspoint.com/operating_system/images/os_critical_section.jpg)

![Image](https://fiveable.me/_next/image?q=75\&url=https%3A%2F%2Fstorage.googleapis.com%2Fstatic.prod.fiveable.me%2Fsearch-images%252F%2522Synchronization_primitives_in_operating_systems%253A_semaphores_mutexes_monitors_and_their_roles_in_concurrency.%2522-81738215139404631492.png\&w=3840)

* Critical section problem
* Race condition
* Mutual exclusion
* Synchronization mechanisms

  * Mutex locks
  * Semaphores
  * Monitors
* Classical synchronization problems

  * Producer–Consumer
  * Readers–Writers
  * Dining Philosophers

---

### **6. Deadlocks**

![Image](https://static.afteracademy.com/images/what-is-deadlock-and-what-are-its-four-necessary-conditions-deadlock-example.png)

![Image](https://www.boardinfinity.com/blog/content/images/2022/11/Your-paragraph-text--50-.jpg)

* System model
* Deadlock characterization
* Deadlock prevention
* Deadlock avoidance

  * Banker’s Algorithm
* Deadlock detection
* Deadlock recovery

---

### **7. Memory Management**

![Image](https://assets.enterprisestorageforum.com/uploads/2021/02/paging-and-segmentation_6019c4f207ec5.png)

![Image](https://www.researchgate.net/publication/380941775/figure/tbl1/AS%3A11431281247918521%401716989407322/Comparison-of-Page-Replacement-algorithms.png)

* Memory management requirements
* Contiguous memory allocation
* Memory allocation strategies

  * First Fit
  * Best Fit
  * Worst Fit
* Paging
* Segmentation
* Virtual memory
* Demand paging
* Page replacement algorithms

  * FIFO
  * LRU
  * Optimal
* Thrashing

---

### **8. File System**

![Image](https://raw.githubusercontent.com/Codecademy/docs/main/media/file-system-structure.png)

![Image](https://www.scaler.com/topics/images/file-allocation-methods-in-os_thumbnail.webp)

* File concepts and attributes
* File access methods
* Directory structures
* File allocation methods

  * Contiguous allocation
  * Linked allocation
  * Indexed allocation
* Free space management
* File protection and security

---

### **9. I/O Management**

![Image](https://almablog-media.s3.ap-south-1.amazonaws.com/Image_1_9f9c22b338.png)

![Image](https://assets.omscs.io/notes/38B48ADB-1EC5-4771-A87B-92D9102ADA69.png)

* I/O hardware
* I/O software
* Disk scheduling
* Disk scheduling algorithms

  * FCFS
  * SSTF
  * SCAN
  * C-SCAN
  * LOOK

---

### **10. Protection and Security**

* Goals of protection
* Domain of protection
* Access matrix
* Authentication and authorization
* Security threats and vulnerabilities

---

