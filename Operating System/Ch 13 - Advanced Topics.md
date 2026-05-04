# Chapter 13: Advanced Topics

This chapter covers specialised areas of operating systems that extend beyond general‑purpose computing: real‑time and embedded systems, mobile platforms, performance profiling, and fault tolerance. These topics highlight how OS principles adapt to different constraints and environments.

---

## Real‑Time Operating Systems (RTOS)

A **Real‑Time Operating System** guarantees that tasks meet their timing deadlines. Correctness depends not only on logical results but also on when results are produced.

### Hard vs Soft Real‑Time

| Type | Deadline violation consequence | Examples |
|------|-------------------------------|----------|
| **Hard real‑time** | Catastrophic (system failure, injury) | Airbag deployment, pacemaker, flight control |
| **Soft real‑time** | Performance degradation (multimedia glitches) | Video playback, audio streaming, games |

### Key RTOS Features

- **Deterministic scheduling** (fixed‑priority preemptive, like Rate‑Monotonic)
- **Low interrupt latency** (short time from interrupt to handler start)
- **Minimal blocking** (priority inheritance to prevent priority inversion)
- **Predictable memory allocation** (avoid dynamic allocation or provide deterministic allocators)

### Examples: VxWorks and FreeRTOS

| Feature | **VxWorks** (Wind River) | **FreeRTOS** (Amazon) |
|---------|--------------------------|------------------------|
| Type | Commercial, hard real‑time | Open source, lightweight |
| Kernel | Monolithic with modular extensions | Microkernel‑like (minimal core) |
| Typical hardware | PowerPC, ARM, x86 (high‑end) | ARM Cortex‑M, AVR, small MCUs |
| Memory footprint | Hundreds of KB to MB | As low as 4‑10 KB |
| Scheduling | Priority preemptive, round‑robin, time slicing | Priority preemptive, cooperative option |
| Use cases | Mars rovers, aerospace, industrial robots | IoT sensors, consumer electronics, hobbyist projects |

**Real‑life analogy**: 
- **Hard real‑time**: A car’s airbag – must deploy within milliseconds of impact; even 1 ms late could be fatal.
- **Soft real‑time**: A music player – a 50 ms delay in decoding is annoying but not catastrophic.

---

## Embedded Operating Systems

Embedded OSes run on specialised devices with limited resources (CPU, memory, power). They are optimised for **efficiency**, **reliability**, and **real‑time** behaviour.

### Characteristics

- **Resource constraints**: KB to MB of RAM, MHz processors.
- **Single purpose**: Often runs one application forever (e.g., microwave, thermostat).
- **Static configuration**: No user installation or dynamic loading.
- **Low boot time**: Typically seconds or less.

### Common Embedded OSes

| OS | Typical use |
|----|--------------|
| **FreeRTOS** | Microcontrollers, IoT sensors |
| **Zephyr** | Linux Foundation, wearables, embedded |
| **Embedded Linux** | Routers, set‑top boxes, infotainment (customisable but heavier) |
| **RT‑Linux (PREEMPT_RT)** | Linux with real‑time patches for industrial control |
| **ThreadX** (Azure RTOS) | High‑reliability (space, medical devices) |

### Example: Embedded Linux vs RTOS

- **Embedded Linux** (Yocto, Buildroot): Full OS, networking, drivers, but larger (1‑10 MB kernel). Non‑deterministic unless patched.
- **FreeRTOS**: Minimal kernel (4‑10 KB), deterministic, but fewer features.

**Real‑life analogy**: 
- **Embedded Linux**: A mini‑PC inside a car dashboard – powerful but takes time to boot.
- **FreeRTOS**: A simple microcontroller in a digital watch – tiny, instant‑on, but only does one thing well.

---

## Mobile Operating System Features

Mobile OSes (Android, iOS) extend general‑purpose OS features with constraints: **battery life**, **sensor integration**, and **user mobility**.

### Power Management

Battery capacity is limited. Mobile OSes aggressively save power:

| Technique | Description |
|-----------|-------------|
| **CPU throttling** | Reduce frequency or core count when idle (DVFS – Dynamic Voltage & Frequency Scaling). |
| **Suspend states** | Deep sleep (Doze mode on Android, App Nap on iOS). CPU stops, only wake‑on interrupts. |
| **Background restrictions** | Limit network and CPU for background apps (Android Background Execution Limits, iOS Background App Refresh). |
| **Battery‑aware scheduling** | EAS (Energy‑Aware Scheduling) on Linux/Android: schedule tasks on efficient cores. |

### Sensor Integration

Mobile OSes provide frameworks for hardware sensors:

| Sensor | Typical use | OS abstraction |
|--------|-------------|----------------|
| **Accelerometer** | Screen rotation, step counting | SensorManager (Android), CoreMotion (iOS) |
| **Gyroscope** | Game orientation, AR | Same |
| **GPS** | Location services | LocationManager |
| **Camera** | Photos, barcode scanning | Camera API |
| **Fingerprint** | Biometric authentication | BiometricPrompt |

### Other Mobile‑Specific Features

- **App sandboxing**: Each app runs as its own user (UID) with restricted permissions (Android UID isolation, iOS App Sandbox).
- **Push notifications**: Wake app without keeping it running (Google FCM, Apple APNs).
- **Seamless updates**: A/B partitions – update while system runs; reboot to new version (Android, iOS).

**Real‑life analogy**: A smartphone is like a Swiss Army knife – many tools in one, but the battery is the limited resource. Power management is like the knife auto‑closing tools when not in use to save energy.

---

## System Performance Profiling (perf, DTrace)

Profiling tools help developers and administrators understand where a system spends time and resources.

### perf (Linux)

`perf` is the Linux standard profiling tool. It uses hardware performance counters (CPU cycles, cache misses, branches) and software events (context switches, page faults).

**Common commands**:

```bash
perf stat ls          # Counts hardware events for a command
perf record -g ls     # Samples stack traces (graph)
perf report           # View results
perf top              # Live view of hottest functions
```

**Output example**: CPU cycles, instructions per cycle, cache misses, branch mispredictions.

### DTrace (Solaris, BSD, macOS, limited Linux)

Created by Sun Microsystems, DTrace allows **dynamic instrumentation** – you can trace kernel or user functions without recompiling or restarting the system. Uses D scripting language.

**Use cases**:
- System call tracing (`dtrace -n 'syscall:::entry { printf("%s\n", probefunc); }'`)
- File I/O latency analysis
- Memory allocation tracking

### Other profiling tools

| Tool | Platform | Purpose |
|------|----------|---------|
| **strace** | Linux | Trace system calls |
| **ltrace** | Linux | Trace library calls |
| **Valgrind** | Linux | Memory profiling, cache simulation |
| **eBPF/bpftrace** | Linux | Modern dynamic tracing (superset of DTrace concepts) |
| **Instruments** | macOS/iOS | GUI performance tools (CPU, memory, energy) |
| **Android Studio Profiler** | Android | CPU, memory, network profiling |

**Real‑life analogy**: 
- **perf**: A fuel consumption meter in a car – tells you how much fuel (CPU cycles) each part of your journey uses.
- **DTrace**: A dashboard with meters you can attach to any component on-the-fly without stopping the car (dynamic instrumentation).

---

## Fault Tolerance and Checkpointing

**Fault tolerance** is the ability of a system to continue operating correctly despite failures (hardware, software, network). **Checkpointing** is a key technique for fault tolerance.

### Checkpointing

Periodically save the full state of a process (memory, registers, open files) to stable storage. If the process crashes, it can be **restarted from the last checkpoint** (rollback recovery).

**Types**:

| Type | Description | Overhead |
|------|-------------|----------|
| **Application‑level** | Programmer inserts checkpoint calls in code. | Low (targeted) |
| **System‑level** | OS transparently checkpoints processes (e.g., CRIU in Linux). | High (saves entire memory) |
| **Incremental** | Only save pages modified since last checkpoint. | Medium |

### CRIU (Checkpoint/Restore In Userspace)

Linux tool that can freeze a running container or process, checkpoint its state to disk, and later restore it – possibly on a different machine.

**Use cases**: Live migration of containers, fast snapshotting for debugging.

### Other Fault Tolerance Techniques

| Technique | Description |
|-----------|-------------|
| **Replication** | Run multiple identical copies; vote on outputs. |
| **Primary/backup** | One active node; standby takes over on failure (heartbeats). |
| **Transactions (ACID)** | Atomic, consistent, isolated, durable operations – rollback on failure. |
| **RAID (disk)** | Redundant disks tolerate drive failure (Chapter 9). |
| **Watchdog timers** | Reset system if a process becomes unresponsive (common in embedded/RTOS). |

### Failure Models

Distributed systems classify failures:

- **Fail‑stop**: Node halts cleanly; others can detect.
- **Byzantine failure**: Node behaves arbitrarily (malicious, buggy). Requires Byzantine fault tolerance (BFT) – expensive.
- **Network partition**: Subset of nodes cannot communicate.

**Real‑life analogy**: A pilot’s flight recorder (black box) – in case of crash, you restart from recorded data? Actually, checkpointing is like saving a video game every few minutes. If the game crashes, you restart from the last save, not from the beginning.

---

## Summary

| Topic | Key takeaway |
|-------|--------------|
| RTOS | Guarantees timing deadlines; VxWorks (hard real‑time, commercial), FreeRTOS (lightweight, open source). |
| Embedded OS | Resource‑constrained, single‑purpose; FreeRTOS, Embedded Linux. |
| Mobile OS features | Power management (DVFS, background limits), sensor frameworks, app sandboxing. |
| System profiling | perf (Linux hardware counters), DTrace (dynamic instrumentation). |
| Checkpointing | Save process state periodically; CRIU enables container live migration. |
| Fault tolerance | Replication, primary/backup, transactions, RAID, watchdogs. |

Advanced topics demonstrate the breadth of operating systems beyond the desktop. Real‑time constraints, power budgets, performance tuning, and fault resilience are critical in modern computing – from tiny sensors to cloud data centres.