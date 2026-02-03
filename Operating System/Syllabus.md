## **Operating System Syllabus**

![Image](https://images.openai.com/static-rsc-3/eSqr15h_mLNyuDA4EkHENHCr4qbprs0KIrR775L8AqMSyf2M7hCxGQdDn1PlYv24eWvD9tHxUL6YATEjteF1VUHxzfCLSb2qv_vffcJ1EI0?purpose=fullsize)

![Image](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter3/3_02_ProcessState.jpg)

![Image](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter5/5_DeterministicChart.jpg)

![Image](https://ms.codes/cdn/shop/articles/gant.png?v=1707881301)

![Image](https://www.researchgate.net/publication/301703085/figure/fig2/AS%3A670017049870349%401536755921751/Gantt-charts-when-burst-time-is-in-random-order-for-Case-II-art-I-a-Gantt-chart-for.png)

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

* Scheduling objectives and criteria
* Preemptive and non-preemptive scheduling
* CPU scheduling algorithms

  * First Come First Serve (FCFS)
  * Shortest Job First (SJF)
  * Shortest Remaining Time First (SRTF)
  * Priority Scheduling
  * Round Robin Scheduling
* Starvation and aging
* Gantt chart based problems

---

### **5. Process Synchronization**

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

* System model
* Deadlock characterization
* Deadlock prevention
* Deadlock avoidance

  * Banker’s Algorithm
* Deadlock detection
* Deadlock recovery

---

### **7. Memory Management**

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

