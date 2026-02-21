# File System

<p align="center">
  <img src="https://raw.githubusercontent.com/Codecademy/docs/main/media/file-system-structure.png" width="420" height="260"/>
  <img src="https://www.scaler.com/topics/images/file-allocation-methods-in-os_thumbnail.webp" width="420" height="260"/>
</p>

A **File System** is a core component of an **Operating System** responsible for managing data storage and retrieval on secondary storage devices such as hard disks, SSDs, and flash drives. It provides a logical abstraction over physical storage, enabling users and applications to store, access, modify, and protect data efficiently.

---

## 1. File Concepts and Attributes

### File Concept

A **file** is a named collection of related information stored on non-volatile storage. It is the smallest logical unit of data storage managed by the operating system.

### File Attributes

Every file is associated with metadata that describes its characteristics:

* **Name** – Human-readable identifier
* **Identifier** – Unique internal number used by the OS
* **Type** – Text, binary, executable, etc.
* **Location** – Pointers to disk blocks containing the file
* **Size** – Current size of the file in bytes
* **Protection** – Access permissions
* **Time and Date** – Creation, modification, and last access timestamps
* **Owner** – User or process that owns the file

---

## 2. File Access Methods

File access methods determine how data within a file can be read or written.

### Sequential Access

* Data is accessed in a fixed order
* Read/write operations move the file pointer forward
* Suitable for text files and logs

### Direct (Random) Access

* Any block of the file can be accessed directly
* Efficient for databases and large data files

### Indexed Access

* An index contains pointers to all file blocks
* Supports both sequential and random access

---

## 3. Directory Structures

Directories organize files and provide a mechanism for naming and searching.

### Single-Level Directory

* All files stored in one directory
* Simple structure
* Name conflicts are common

### Two-Level Directory

* Separate directory for each user
* Reduces naming conflicts

### Tree-Structured Directory

* Hierarchical structure with subdirectories
* Most commonly used in modern operating systems

### Acyclic Graph Directory

* Allows sharing of files and directories
* Prevents cycles

---

## 4. File Allocation Methods

File allocation methods define how disk blocks are assigned to files.

### Contiguous Allocation

* File occupies consecutive disk blocks

**Advantages**

* Simple to implement
* Fast sequential and direct access

**Disadvantages**

* External fragmentation
* Difficult to expand files

---

### Linked Allocation

* File blocks linked using pointers

**Advantages**

* No external fragmentation
* Easy file growth

**Disadvantages**

* Slow random access
* Pointer overhead
* Risk of pointer corruption

---

### Indexed Allocation

* An index block stores addresses of all file blocks

**Advantages**

* Efficient direct and sequential access
* No external fragmentation

**Disadvantages**

* Extra space required for index block
* Overhead for small files

---

## 5. Free Space Management

The operating system must track unused disk blocks efficiently.

### Bit Vector

* Each block represented by a bit
* `0` indicates free, `1` indicates allocated
* Simple and fast allocation

### Linked List

* Free blocks linked together
* No wasted space
* Slow to search for large free areas

### Grouping

* First free block stores addresses of multiple free blocks
* Reduces traversal time

### Counting

* Maintains count of contiguous free blocks
* Efficient for contiguous allocation

---

## 6. File Protection and Security

File protection ensures controlled access to files and prevents unauthorized usage.

### Access Control

* Defines who can read, write, or execute a file
* Implemented using access control lists or permission bits

### User Authentication

* Verifies user identity before granting access

### Encryption

* Protects file data from unauthorized access
* Ensures confidentiality

### Backup and Recovery

* Prevents data loss due to failures or corruption

---

## Conclusion

The file system is a crucial part of an operating system that provides structured data storage, efficient access mechanisms, and robust security. Understanding file concepts, allocation strategies, directory structures, and protection mechanisms is essential for designing and managing modern operating systems.
