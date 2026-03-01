## **Process Management**

### **1. Introduction**

Process Management is a fundamental function of an Operating System (OS) that deals with the creation, scheduling, execution, synchronization, and termination of processes. A **process** is a program in execution, along with its associated resources such as CPU registers, memory, files, and I/O devices.
The primary goal of process management is to ensure efficient CPU utilization, fairness among processes, and correct execution in a multi-programming environment.

---

### **2. Process**

A **process** consists of:

* **Program Code (Text Section)** – executable instructions
* **Data Section** – global and static variables
* **Heap** – dynamically allocated memory
* **Stack** – function calls, local variables, and return addresses
* **Process Control Block (PCB)** – metadata used by the OS to manage the process

Each process is independent and executes in its own address space.

---

### **3. Process States**

During its lifetime, a process transitions through various states:

<p align="center">
  <img 
    src="https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter3/3_02_ProcessState.jpg"
    alt="Process State Diagram"
    width="600"
  />
</p>

Common process states include:

* **New** – Process is being created
* **Ready** – Process is waiting to be assigned to the CPU
* **Running** – Process is currently executing on the CPU
* **Waiting (Blocked)** – Process is waiting for I/O or some event
* **Terminated** – Process has completed execution

Some systems also include **Suspended Ready** and **Suspended Blocked** states.

---

### **4. Process Control Block (PCB)**

The **PCB** is a data structure maintained by the OS for each process. It contains:

* Process ID (PID)
* Process State
* Program Counter
* CPU Registers
* CPU Scheduling Information (priority, queue pointers)
* Memory Management Information
* Accounting Information
* I/O Status Information

The PCB allows the OS to perform **context switching** efficiently.

---

### **5. Context Switching**

Context switching is the mechanism by which the OS saves the state of the currently running process and loads the state of the next scheduled process.
Although necessary for multitasking, context switching introduces overhead since the CPU performs no useful work during the switch.

---

### **6. Process Scheduling**

Process scheduling determines which process gets CPU time and for how long. The OS scheduler aims to:

* Maximize CPU utilization
* Minimize waiting time, turnaround time, and response time
* Ensure fairness and avoid starvation

#### **Types of Schedulers**

* **Long-Term Scheduler** – Selects processes to admit into the ready queue
* **Short-Term Scheduler** – Selects the next process to execute on the CPU
* **Medium-Term Scheduler** – Handles process suspension and resumption

#### **Scheduling Algorithms**

* First Come First Serve (FCFS)
* Shortest Job First (SJF)
* Priority Scheduling
* Round Robin (RR)
* Multilevel Queue Scheduling

---

### **7. Process Creation**

Processes can be created by:

* System initialization
* A running process invoking a system call (e.g., `fork()`)
* User requests

During creation, the OS:

1. Assigns a unique PID
2. Allocates memory and resources
3. Initializes PCB
4. Places the process in the ready queue

Parent–child relationships may exist between processes.

---

### **8. Process Termination**

A process terminates when:

* It completes execution normally
* It encounters an error or exception
* It is terminated by another process or the OS

On termination, the OS releases all resources allocated to the process and removes its PCB.

---

### **9. Inter-Process Communication (IPC)**

IPC allows processes to communicate and synchronize their actions.
Common IPC mechanisms include:

* Pipes
* Message Queues
* Shared Memory
* Semaphores
* Signals

IPC is essential in concurrent and distributed systems.

---

### **10. Process Synchronization**

When multiple processes access shared resources, synchronization is required to prevent race conditions.
Key concepts include:

* Critical Section
* Mutual Exclusion
* Semaphores
* Mutex Locks
* Monitors

Proper synchronization ensures data consistency and system stability.

---

### **11. Importance of Process Management**

Process management is crucial because it:

* Enables multitasking and multi-user systems
* Ensures fair and efficient CPU allocation
* Prevents deadlocks and starvation
* Improves system performance and responsiveness

---

### **12. Conclusion**

Process Management is a core responsibility of an Operating System that ensures orderly execution of multiple processes. By efficiently handling process states, scheduling, synchronization, and communication, the OS provides a stable, responsive, and high-performance computing environment.
