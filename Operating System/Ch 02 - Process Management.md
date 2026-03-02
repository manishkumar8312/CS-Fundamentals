# Process Management (Operating System)

A comprehensive reference for understanding process management concepts in Operating Systems. Suitable for academic study, interviews, and technical documentation.

---

## 1. Process Concept

A **process** is a program in execution.

When a program is loaded into memory and begins execution, it becomes a process. A process is an active entity and contains:

* Program code (Text section)
* Program Counter (PC)
* Stack (function calls, local variables)
* Heap (dynamic memory allocation)
* Data section (global/static variables)
* CPU registers

A process is more than just the program code; it also includes the current activity and execution context.

---

## 2. Process vs Program

| Program            | Process                |
| ------------------ | ---------------------- |
| Passive entity     | Active entity          |
| Stored on disk     | Resides in main memory |
| No execution state | Has execution state    |
| Static             | Dynamic                |

A single program can create multiple processes. For example, running the same executable multiple times results in multiple independent processes.

---

## 3. Process States and State Transitions

### Process States

1. **New** – Process is being created.
2. **Ready** – Process is waiting for CPU allocation.
3. **Running** – Process instructions are being executed.
4. **Waiting (Blocked)** – Process is waiting for I/O or an external event.
5. **Terminated** – Process execution has completed.

### Process State Transition Diagram

<div align="center">

![Process State Diagram](https://upload.wikimedia.org/wikipedia/commons/5/53/Process_state_diagram.svg)

</div>

### State Transitions

* New → Ready
* Ready → Running
* Running → Waiting
* Waiting → Ready
* Running → Terminated
* Running → Ready (Preemption)

---

## 4. Process Control Block (PCB)

The **Process Control Block (PCB)** is a data structure maintained by the operating system to store all information about a process.

### PCB Contains:

* Process ID (PID)
* Process State
* Program Counter
* CPU Registers
* CPU Scheduling Information
* Memory Management Information
* Accounting Information
* I/O Status Information

### PCB Structure Diagram

The PCB is essential for context switching and process management.

---

## 5. Context Switching

**Context Switching** is the process of saving the state of the currently running process and loading the state of another process.

Steps involved:

1. Save current process state into its PCB.
2. Load next process state from its PCB.
3. Resume execution.

Context switching introduces overhead because no useful work is done during the switch.

---

## 6. Process Scheduling Queues

Processes move between various scheduling queues:

* Job Queue – All processes in the system.
* Ready Queue – Processes waiting for CPU.
* Device Queues – Processes waiting for I/O devices.

### Scheduling Queue Diagram

The CPU scheduler selects processes from the ready queue.

---

## 7. Process Creation and Termination

### Process Creation

A process may create several new processes via system calls.

Reasons for process creation:

* System initialization
* User request
* Batch job submission
* Parent process creates child process

### Process Termination

A process terminates when:

* It finishes execution.
* It encounters a fatal error.
* It is killed by another process.
* The operating system terminates it.

---

## 8. fork() and exec() Concepts

These are system calls in UNIX-based systems.

### fork()

* Creates a new child process.
* The child process is an exact copy of the parent.
* Returns:

  * 0 to child
  * Child PID to parent
  * -1 on failure

### exec()

* Replaces the current process image with a new program.
* Does not create a new process.
* Used after `fork()` in most cases.

Typical pattern:

```c
pid_t pid = fork();

if (pid == 0) {
    execl("/bin/ls", "ls", NULL);
}
```

---

## 9. Zombie and Orphan Processes

### Zombie Process

* A process that has finished execution.
* Still has an entry in the process table.
* Parent has not called `wait()`.

Zombie exists until the parent collects its exit status.

### Orphan Process

* A child process whose parent has terminated.
* Adopted by the init process (PID 1).

---

## 10. Inter-Process Communication (IPC)

Processes may need to communicate and synchronize with each other.

There are two main IPC models:

---

### 10.1 Shared Memory

* Multiple processes share a common memory region.
* Fast communication.
* Requires synchronization mechanisms (semaphores, mutex).

Working:

1. OS creates shared memory region.
2. Processes attach to it.
3. They read/write data.

Advantages:

* High speed
* Efficient for large data

Disadvantages:

* Synchronization complexity

---

### 10.2 Message Passing

* Processes communicate by sending messages.
* No shared memory.
* Safer and easier to implement.

Types:

* Direct Communication
* Indirect Communication (via mailboxes)

Advantages:

* No shared memory issues
* Suitable for distributed systems

Disadvantages:

* Slower than shared memory

---

# Conclusion

Process management is a core responsibility of the operating system. It includes:

* Process lifecycle management
* Context switching
* Scheduling
* Creation and termination
* Inter-process communication

Understanding these concepts is essential for system programming, operating system design, and technical interviews.

