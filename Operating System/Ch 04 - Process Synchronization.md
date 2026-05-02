# Chapter 4: Process Synchronization

When multiple processes or threads access shared data concurrently, the results can become unpredictable or incorrect. Process synchronization ensures that cooperative processes execute in a controlled manner, preventing race conditions and preserving data integrity. This chapter covers the classic problems, solutions, and system‑level tools used to coordinate access to shared resources.

---

## Critical Section Problem

A **critical section** is a segment of code that accesses shared variables or resources (e.g., a file, a global counter) that must not be executed simultaneously by more than one process or thread.

The **critical section problem** is to design a protocol that ensures when one process is inside its critical section, no other process is allowed to enter its own critical section that accesses the same shared resources.

**Structure of a typical process** (with a critical section):

```c
do {
    // Entry section – request permission to enter critical section
    // Critical section – access shared variables
    // Exit section – release permission
    // Remainder section – non‑critical work
} while (true);
```

**Real‑life analogy**: An ATM machine (critical section). Only one person can use the ATM at a time. People waiting (processes) must coordinate – if two tried to use it simultaneously, the system could double‑dispense cash or corrupt balances.

---

## Solution Requirements

A valid solution to the critical‑section problem must satisfy **three conditions**:

| Requirement | Meaning |
|-------------|---------|
| **Mutual exclusion** | If process Pᵢ is executing in its critical section, no other process can be in its critical section. |
| **Progress** | If no process is in its critical section and some processes wish to enter, only those not in their remainder sections can participate in deciding who enters next. The selection cannot be postponed indefinitely. |
| **Bounded waiting** | After a process makes a request to enter its critical section, there is a bound (limit) on the number of other processes that can enter before that request is granted. No starvation. |

---

## Software Solutions: Peterson’s Algorithm

Peterson’s algorithm (1981) is a classic software‑only solution for **two processes** (P0 and P1) that satisfies all three requirements. It works even without hardware atomic operations.

**Data structures**:
- `int turn;` – indicates whose turn it is to enter.
- `bool flag[2];` – each `flag[i]` indicates that process i is ready to enter.

**Algorithm for process i** (the other process is j = 1‑i):

```c
do {
    flag[i] = true;           // I want to enter
    turn = j;                 // Let the other go first (courtesy)
    while (flag[j] && turn == j);  // Busy wait if other is ready and it's its turn

    // Critical section

    flag[i] = false;          // I'm done

    // Remainder section
} while (true);
```

**Why it works**:
- **Mutual exclusion**: If both processes want to enter, `turn` can be either 0 or 1, so only one proceeds.
- **Progress**: If one process is in its remainder section, `flag[j]` is false, so the other enters immediately.
- **Bounded waiting**: Each process waits at most one turn for the other.

**Real‑life analogy**: Two people sharing a single phone booth. They each raise a hand (`flag[i]=true`) and politely say “You go first” (`turn = j`). If both raise their hands, the one whose turn it is (according to the last spoken “you first”) steps back and lets the other go.

> **Note**: Peterson’s algorithm is elegant but does not work on modern CPU architectures with out‑of‑order execution unless memory barriers are used. It remains a pedagogical classic.

---

## Hardware Support: Test‑and‑Set and Compare‑and‑Swap

Modern processors provide atomic hardware instructions that read, modify, and write memory in one uninterruptible step. These instructions are used to build efficient synchronization primitives.

### Test‑and‑Set (TAS)

Atomically reads a memory location and writes a `true` (or 1) into it.

**Pseudo‑code**:

```c
bool test_and_set(bool *target) {
    bool old = *target;
    *target = true;
    return old;
}
```

**Mutual exclusion using TAS** (shared variable `lock = false` initially):

```c
do {
    while (test_and_set(&lock));  // busy wait
    // Critical section
    lock = false;
    // Remainder section
} while (true);
```

### Compare‑and‑Swap (CAS)

Atomically compares a variable with a given value; if equal, it swaps with a new value.

```c
int compare_and_swap(int *value, int expected, int new_value) {
    int old = *value;
    if (old == expected)
        *value = new_value;
    return old;
}
```

**Using CAS for mutual exclusion**:

```c
do {
    while (compare_and_swap(&lock, 0, 1) != 0); // wait until lock becomes 0
    // Critical section
    lock = 0;
    // Remainder section
} while (true);
```

**Real‑life analogy**: A restroom key. TAS is like grabbing the key if it’s available and simultaneously marking it “taken” in one motion. CAS is like saying “If the key is on the hook, take it and leave a ‘busy’ sign; otherwise, do nothing.”

---

## Mutex Locks and Spinlocks

A **mutex** (MUTual EXclusion) is a simple locking mechanism that supports `acquire()` and `release()` operations.

- **Mutex lock (blocking)**: If a thread cannot acquire the lock, it is put to sleep (context switch). Good for long critical sections.
- **Spinlock**: If a thread cannot acquire the lock, it busy‑waits (spins) in a loop, consuming CPU. Good for short critical sections (no context‑switch overhead).

**Implementation using test‑and‑set**:

```c
void acquire(lock) {
    while (test_and_set(&lock->flag));  // spin
}
void release(lock) {
    lock->flag = false;
}
```

| Feature | Mutex (blocking) | Spinlock |
|---------|------------------|----------|
| Waiting behaviour | Thread sleeps | Thread spins (busy‑wait) |
| CPU usage during wait | Almost zero | High (wastes cycles) |
| Context switch overhead | Yes (to scheduler and back) | None |
| Best when | Critical section long or I/O involved | Critical section very short |

**Real‑life analogy**:
- **Mutex**: Waiting for a meeting room – you go to your office (sleep) and get notified when free.
- **Spinlock**: Waiting for a red light – you keep the engine running, tapping the steering wheel.

---

## Semaphores

A **semaphore** is an integer variable that, apart from initialisation, can only be accessed via two atomic operations: `wait()` (also called P, down, decrement) and `signal()` (V, up, increment).

### Binary Semaphore

Takes only values 0 and 1 – behaves like a mutex lock.

```c
wait(S) {
    while (S <= 0);  // busy wait (or block)
    S--;
}
signal(S) {
    S++;
}
```

### Counting Semaphore

Can take any non‑negative integer: represents the number of available resources.

- `wait(S)` decrements; if `S < 0`, process blocks.
- `signal(S)` increments; if there are blocked processes, one is woken.

**Implementation with blocking** (to avoid busy waiting):

```c
typedef struct {
    int value;
    struct process *waiting_queue;
} semaphore;

void wait(semaphore *S) {
    S->value--;
    if (S->value < 0) {
        // add this process to waiting_queue
        block();  // OS puts process to sleep
    }
}

void signal(semaphore *S) {
    S->value++;
    if (S->value <= 0) {
        // remove a process from waiting_queue
        wakeup(); // OS makes it ready
    }
}
```

**Example**: Three printers. Initialize semaphore `printers = 3`. Each process does `wait(&printers)` before printing, `signal(&printers)` after. The fourth process will block until one printer becomes free.

**Real‑life analogy**: Parking garage with 50 spaces. A counter shows available spots. `wait()` = car enters (counter‑‑). `signal()` = car leaves (counter++). If the counter reaches zero, cars must queue (block) outside.

---

## Classical Synchronization Problems

These classic problems illustrate the challenges of synchronization and the use of semaphores, mutexes, and monitors.

### 1. Bounded Buffer (Producer‑Consumer)

**Problem**: A fixed‑size buffer. Producers write data into it; consumers take data out. The producer must not write into a full buffer; the consumer must not read from an empty buffer. No two producers (or consumers) should access the buffer simultaneously.

**Solution using semaphores**:

```c
semaphore mutex = 1;     // protects buffer access
semaphore empty = n;     // number of empty slots
semaphore full = 0;      // number of filled slots

// Producer
do {
    // produce an item
    wait(&empty);         // wait if no empty slot
    wait(&mutex);         // enter critical section
    // add item to buffer
    signal(&mutex);       // leave critical section
    signal(&full);        // increment filled count
} while (true);

// Consumer
do {
    wait(&full);          // wait if nothing to consume
    wait(&mutex);
    // remove item from buffer
    signal(&mutex);
    signal(&empty);       // now one more empty slot
    // consume the item
} while (true);
```

**Real‑life**: A pizza delivery counter (buffer). The baker (producer) makes pizzas and puts them on a shelf. The cashier (consumer) takes them for customers. The baker stops if the shelf is full (`empty=0`). The cashier waits if the shelf is empty (`full=0`). Only one person touches the shelf at a time (`mutex`).

### 2. Readers‑Writers

**Problem**: A shared database. Multiple readers can read simultaneously, but a writer needs exclusive access. Variations:
- **First readers‑writers problem** (no reader starvation): Readers have priority; writers may starve.
- **Second readers‑writers problem** (writer priority): Writers have priority; readers may starve.

**Solution (first, with reader priority)**:

```c
semaphore rw_mutex = 1;   // writer access
semaphore mutex = 1;      // protects read_count
int read_count = 0;

// Writer
do {
    wait(&rw_mutex);
    // write to database
    signal(&rw_mutex);
} while (true);

// Reader
do {
    wait(&mutex);
    read_count++;
    if (read_count == 1)
        wait(&rw_mutex);   // first reader locks writer out
    signal(&mutex);
    
    // reading performed
    
    wait(&mutex);
    read_count--;
    if (read_count == 0)
        signal(&rw_mutex); // last reader unlocks writer
    signal(&mutex);
} while (true);
```

**Real‑life**: A library book. Many people can read the same book simultaneously (readers). But only one person can update the book (writer) – and while updating, no one should read a half‑written version.

### 3. Dining Philosophers

**Problem**: Five philosophers sit around a table with five chopsticks (or forks). Each philosopher needs two chopsticks to eat – the one on the left and the one on the right. They alternate between thinking and eating. The challenge is to avoid deadlock and starvation.

**Naïve solution** (leads to deadlock if all grab left chopstick simultaneously).

**Solution using semaphores** (with deadlock avoidance: pick up both chopsticks only if both free):

```c
semaphore chopstick[5] = {1,1,1,1,1};
semaphore mutex = 1;   // to prevent deadlock (allow only 4 philosophers at table)

void philosopher(int i) {
    while (true) {
        think();
        wait(&mutex);
        wait(&chopstick[i]);
        wait(&chopstick[(i+1)%5]);
        signal(&mutex);
        eat();
        signal(&chopstick[i]);
        signal(&chopstick[(i+1)%5]);
    }
}
```

**Other solutions**: limit 4 philosophers at a time, asymmetric (odd pick left then right, even right then left), or use a monitor.

**Real‑life**: A group of friends sharing a communal bowl of rice and spoons. Each needs two spoons to serve themselves. Coordination prevents everyone holding one spoon forever (deadlock).

### 4. Sleeping Barber

**Problem**: A barber shop with one barber, one barber chair, and a number of waiting chairs. If no customers, the barber sleeps. A customer arriving wakes the barber if asleep. If the barber is busy, the customer waits in a waiting chair if available; otherwise leaves.

**Solution** (skeleton using semaphores):

```c
semaphore customers = 0;   // waiting customers
semaphore barber = 0;      // barber ready
semaphore mutex = 1;       // protects waiting count
int waiting = 0;           // number waiting
int CHAIRS = 5;

// Barber process
do {
    wait(&customers);       // sleep if no customers
    wait(&mutex);
    waiting--;              // one waiting enters
    signal(&barber);        // barber is ready
    signal(&mutex);
    // cut hair
} while (true);

// Customer process
wait(&mutex);
if (waiting < CHAIRS) {
    waiting++;
    signal(&customers);     // wake barber if needed
    signal(&mutex);
    wait(&barber);          // wait for barber
    // get haircut
} else {
    signal(&mutex);         // shop full, leave
}
```

**Real‑life**: Exactly the described barber shop, with the barber napping between customers.

---

## Monitors and Condition Variables

A **monitor** is a high‑level abstraction that provides a clean, structured way to achieve synchronization. It is a programming language construct (e.g., in Java, C#) or a library concept (e.g., `pthread_cond` in C).

- The monitor **encapsulates** shared variables and the operations that can access them.
- Only **one thread** at a time can be active inside a monitor (automatic mutual exclusion).
- **Condition variables** allow a thread to wait inside the monitor for a certain condition to become true, temporarily releasing the monitor lock.

**Condition variable operations**:
- `wait(cond, mutex)`: release mutex, block on cond, re‑acquire mutex when signalled.
- `signal(cond)`: wake one waiting thread (if any).
- `broadcast(cond)`: wake all waiting threads.

**Example: Bounded buffer using a monitor** (pseudo‑code):

```c
monitor BoundedBuffer {
    int buffer[N];
    int count = 0, in = 0, out = 0;
    condition notFull, notEmpty;

    void produce(int item) {
        while (count == N)
            wait(notFull);
        buffer[in] = item;
        in = (in+1) % N;
        count++;
        signal(notEmpty);
    }

    int consume() {
        while (count == 0)
            wait(notEmpty);
        int item = buffer[out];
        out = (out+1) % N;
        count--;
        signal(notFull);
        return item;
    }
}
```

**Real‑life analogy**: A restroom with a single key (monitor lock). If the restroom is occupied, you wait on a “vacant” condition. When the occupant leaves, they signal – one waiting person enters.

---

## Synchronization in POSIX Threads (Pthreads)

POSIX threads (pthreads) provide a standard API for multithreading on Unix‑like systems. Common synchronization primitives:

### Mutexes

```c
#include <pthread.h>

pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;

// In threads
pthread_mutex_lock(&mutex);
// critical section
pthread_mutex_unlock(&mutex);
```

`pthread_mutex_trylock()` attempts non‑blocking lock acquisition.

### Condition Variables

Used together with a mutex:

```c
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;

// Thread that waits for a condition
pthread_mutex_lock(&mutex);
while (condition_not_met) {
    pthread_cond_wait(&cond, &mutex);
}
// condition met, do work
pthread_mutex_unlock(&mutex);

// Thread that signals the condition
pthread_mutex_lock(&mutex);
// change state so condition becomes true
pthread_cond_signal(&cond);   // wake one waiting thread
pthread_mutex_unlock(&mutex);
```

- `pthread_cond_broadcast()` wakes all waiting threads.
- Always use a **while loop** (not `if`) with `pthread_cond_wait()` to handle spurious wakeups.

### Example: Producer‑Consumer with pthreads

```c
#define N 10
int buffer[N];
int in = 0, out = 0, count = 0;
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t notFull = PTHREAD_COND_INITIALIZER;
pthread_cond_t notEmpty = PTHREAD_COND_INITIALIZER;

void *producer(void *arg) {
    int item;
    while (1) {
        item = produce_item();
        pthread_mutex_lock(&mutex);
        while (count == N)
            pthread_cond_wait(&notFull, &mutex);
        buffer[in] = item;
        in = (in+1) % N;
        count++;
        pthread_cond_signal(&notEmpty);
        pthread_mutex_unlock(&mutex);
    }
}
```

**Real‑life**: A ticket booking system – the mutex prevents double booking; condition variables let a thread wait for a seat to become available.

---

## Summary

| Concept | Key takeaway |
|---------|--------------|
| Critical section | Code segment accessing shared resources that must be mutually exclusive. |
| Requirements | Mutual exclusion, progress, bounded waiting. |
| Peterson’s algorithm | Software solution for two processes (pedagogical, not widely used in practice). |
| Hardware support | TAS, CAS – atomic instructions that simplify lock implementation. |
| Mutex / Spinlock | Mutex blocks, spinlock busy‑waits. Choose based on critical section length. |
| Semaphores | Counting semaphores manage resources; binary semaphores act as mutexes. |
| Classical problems | Bounded buffer, readers‑writers, dining philosophers, sleeping barber. |
| Monitors | Language construct with automatic mutual exclusion and condition variables. |
| Pthreads | Standard Unix threading API with `pthread_mutex` and `pthread_cond`. |

Understanding process synchronization is crucial to writing correct concurrent programs. The next chapter explores deadlock – what happens when synchronization goes wrong.