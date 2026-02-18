# Memory Management

Memory Management is a fundamental function of an Operating System responsible for managing primary memory (RAM). It handles allocation, deallocation, protection, and mapping of memory to ensure efficient execution of multiple processes. Proper memory management directly impacts system performance, reliability, and resource utilization.

---

## Memory Management Requirements

An effective memory management system must satisfy the following requirements:

* **Relocation** – Programs should execute correctly irrespective of their physical location in memory.
* **Protection** – Processes must not access memory belonging to other processes.
* **Sharing** – Memory should be shareable among processes when required.
* **Logical Organization** – Programs should be organized into logical units such as code, data, and stack.
* **Physical Organization** – Efficient handling of primary and secondary memory.

<div style="text-align: center;">
  <img src="https://assets.enterprisestorageforum.com/uploads/2021/02/data-storage-memory-management-optimizing-computer-memory_6019c48f54470.png" alt="Memory Management" />
</div>

<div style="text-align: center;">
  <img src="https://static.afteracademy.com/images/what-is-the-difference-between-logical-and-physical-address-wrt-operating-system-mapping-physical-and-virtual-addresses-3c4b40c3385b8fef.jpg" alt="Logical and Physical Address" />
</div>

---

## Contiguous Memory Allocation

In contiguous memory allocation, each process is allocated a single continuous block of physical memory.

### Characteristics

* Memory is divided into fixed or variable-sized partitions.
* A process occupies exactly one partition.

### Advantages

* Simple implementation
* Fast memory access

### Disadvantages

* External fragmentation
* Limited flexibility for dynamic memory growth

<div style="text-align: center;">
  <img src="https://scaler.com/topics/images/Contiguous%20memory%20allocation%20in%20os_Inner%20Image-01.webp" alt="Contiguous Memory Allocation" />
</div>

<div style="text-align: center;">
  <img src="https://study.com/cimages/multimages/16/580d9d7c-0231-458d-9455-0ad52a14edaf_partition_10.png" alt="Memory Partitions" />
</div>

---

## Memory Allocation Strategies

When variable-sized partitions are used, the operating system applies allocation strategies to select an appropriate free block.

### First Fit

* Allocates the first available block that is large enough.
* Faster allocation but leads to fragmentation near the beginning of memory.

### Best Fit

* Allocates the smallest block that satisfies the requirement.
* Reduces internal waste but increases external fragmentation.

### Worst Fit

* Allocates the largest available block.
* Leaves large unused memory spaces; rarely used in practice.

<div style="text-align: center;">
  <img src="https://www.poriyaan.in/media/imgPori/images51/MJvO4WK.jpg" alt="Memory Allocation Strategies" />
</div>

---

## Paging

Paging is a non-contiguous memory management technique that divides memory into fixed-size blocks.

### Key Concepts

* Logical memory is divided into **pages**.
* Physical memory is divided into **frames**.
* Page tables map pages to frames.

### Advantages

* Eliminates external fragmentation
* Supports virtual memory

### Disadvantages

* Internal fragmentation
* Additional overhead for page tables

<div style="text-align: center;">
  <img src="https://exposnitc.github.io/img/address_translation.png" alt="Paging Address Translation" />
</div>

---

## Segmentation

Segmentation divides a program into logical segments based on functionality.

### Characteristics

* Each segment has a base and limit.
* Segments include code, data, stack, etc.

### Advantages

* Logical view of memory
* Better protection and sharing

### Disadvantages

* External fragmentation
* More complex memory management

<div style="text-align: center;">
  <img src="https://assets.enterprisestorageforum.com/uploads/2021/02/paging-and-segmentation_6019c4f2d369c.png" alt="Paging and Segmentation" />
</div>

---

## Virtual Memory

Virtual memory allows processes to execute without being fully loaded into main memory.

### Benefits

* Execution of programs larger than physical memory
* Improved memory utilization
* Higher degree of multiprogramming

### Implementation

* Typically implemented using paging
* Uses secondary storage such as disks

<div style="text-align: center;">
  <img src="https://upload.wikimedia.org/wikipedia/commons/6/6e/Virtual_memory.svg" alt="Virtual Memory" />
</div>


---

## Demand Paging

Demand paging loads memory pages only when they are required during execution.

### Working

* A page is loaded into memory only when a page fault occurs.
* Reduces unnecessary memory allocation.

### Advantages

* Faster program startup
* Efficient use of memory

### Disadvantages

* Page faults cause execution delays
* May lead to thrashing if not controlled

<div style="text-align: center;">
  <img src="https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter9/9_10_PageReplacement.jpg" alt="Demand Paging" />
</div>


---

## Page Replacement Algorithms

When a page fault occurs and no free frames are available, a page replacement algorithm selects a page to remove.

### FIFO (First In First Out)

* Replaces the page that entered memory first.
* Simple but suffers from Belady’s anomaly.

### LRU (Least Recently Used)

* Replaces the page that has not been used for the longest time.
* Good performance but requires tracking usage history.

### Optimal

* Replaces the page that will not be used for the longest future time.
* Produces minimum page faults; theoretical benchmark.

<div style="text-align: center;">
  <img src="https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1675407302244-FIFO%20Page%20Replacement%20Algorithm1.png" alt="Page Replacement Algorithms" />
</div>

---

## Thrashing

Thrashing occurs when the system spends most of its time handling page faults rather than executing processes.

### Causes

* Excessive multiprogramming
* Insufficient memory frames
* Poor memory allocation policies

### Effects

* High disk I/O
* Low CPU utilization
* Severe performance degradation

### Prevention Techniques

* Working set model
* Page fault frequency control
* Reducing degree of multiprogramming

<div style="text-align: center;">
  <img src="https://media.licdn.com/dms/image/v2/D5612AQEVPv8z5EV9lA/article-cover_image-shrink_720_1280/B56ZZor9.nHAAI-/0/1745513088012?e=2147483647&t=STS-89VL-dr5oh-PyD4vwANk0QQBfR5NONtT_QFLKRY&v=beta" alt="Thrashing" />
</div>


---

## Conclusion

Memory Management is a critical Operating System concept that ensures efficient utilization of memory resources while maintaining system stability and performance. Understanding allocation techniques, paging, segmentation, virtual memory, and page replacement algorithms is essential for academic learning, competitive examinations, and technical interviews.

