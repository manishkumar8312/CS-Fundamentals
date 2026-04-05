# Chapter 1: Database Fundamentals

## 1. What is DBMS?

A **Database Management System (DBMS)** is software that enables users to define, create, maintain, and control access to databases. It acts as an intermediary between the user/application and the physical data storage.

**Examples**: MySQL, PostgreSQL, Oracle, MongoDB, SQLite.

```mermaid
flowchart LR
    User[User / Application] --> DBMS[DBMS Software]
    DBMS --> DB[Database]
    DB --> Data[Structured Data]
```

**Key functions of a DBMS**:
- Data definition (creating tables, constraints)
- Data manipulation (insert, update, delete, query)
- Data security and integrity enforcement
- Concurrent access control
- Backup and recovery

---

## 2. Advantages of DBMS over File System

| Feature | File System | DBMS |
|---------|-------------|------|
| Data redundancy | High (data duplicated) | Controlled, minimal |
| Data inconsistency | Common | Avoided via constraints |
| Data access | Requires custom programs | Standard query language (SQL) |
| Concurrent access | No control, may corrupt | Built‑in concurrency control |
| Security | Limited | User authentication, privileges |
| Backup & recovery | Manual | Automated, consistent |
| Data integrity | Application‑dependent | Enforced by DBMS |

```mermaid
flowchart TD
    subgraph FS[File System Issues]
        F1[Data Redundancy]
        F2[Inconsistent Data]
        F3[No Concurrency Control]
        F4[Poor Security]
    end
    subgraph DBMS[DBMS Advantages]
        D1[Redundancy Controlled]
        D2[Data Consistency]
        D3[Concurrency Management]
        D4[Security and Integrity]
    end
    FS -->|Solved by| DBMS
```

**Detailed explanation**:

- **Redundancy & Inconsistency**: In file systems, the same data may be stored in multiple files (redundancy). Updates in one file may not reflect in others (inconsistency). DBMS normalizes data and uses constraints to eliminate redundancy.
- **Concurrent access**: File systems allow multiple users to read/write same file – leads to lost updates or corrupted data. DBMS uses locking and transactions.
- **Security**: DBMS provides granular access control (user, role, table, column level).
- **Backup & Recovery**: DBMS automatically logs changes and can restore to a consistent state after a crash.

---

## 3. Data Abstraction

Data abstraction hides complex storage details and provides users with a simplified view. It has **three levels**:

| Level | Description | Perspective |
|-------|-------------|-------------|
| **Physical** | How data is actually stored (bits, blocks, indexes, compression) | Low‑level, DBA |
| **Logical** | What data is stored and the relationships (tables, records, data types) | Database designer |
| **View** | Customised data presentation for specific users (subsets, derived columns) | End users / applications |

```mermaid
flowchart TD
    User[End User] --> View[View Level]
    View --> Logical[Logical Level]
    Logical --> Physical[Physical Level]
    
    ViewDesc["Custom views, security restrictions"]
    LogicalDesc["Tables, records, relationships"]
    PhysicalDesc["Storage structures, indexing, compression"]
    
    View -.-> ViewDesc
    Logical -.-> LogicalDesc
    Physical -.-> PhysicalDesc
```

**Example**: A bank database
- **Physical**: Data stored on disk blocks with B‑tree indexes on account numbers.
- **Logical**: Tables `Customer(custID, name)`, `Account(accNo, custID, balance)`.
- **View**: A teller sees only account balances; a manager sees all customer details.

---

## 4. Data Independence

**Data independence** means changes at one level do not require changes at higher levels.

### 4.1 Logical Data Independence
- **Change**: Logical schema (adding a column, changing data type, merging tables).
- **Unaffected**: External views and application programs.

### 4.2 Physical Data Independence
- **Change**: Physical storage (switching from sequential to indexed file organisation, using different compression, adding indexes).
- **Unaffected**: Logical schema and views.

```mermaid
flowchart TD
    subgraph Changes
        L["Logical Schema Change (e.g., add column)"]
        P["Physical Storage Change (e.g., new index)"]
    end
    subgraph Independence
        LDI["Logical Data Independence - Views remain unchanged"]
        PDI["Physical Data Independence - Logical schema unchanged"]
    end
    L --> LDI
    P --> PDI
    LDI --> App[Applications work unchanged]
    PDI --> App
```

**Why it matters**:
- Without logical independence, adding a single field would break every application.
- Without physical independence, optimising storage (e.g., adding an index) would require rewriting all queries.

---

## 5. Schema vs Instance

| Term | Definition | Analogy | Change Frequency |
|------|------------|---------|------------------|
| **Schema** | The overall design / blueprint of the database (tables, columns, constraints) | Class definition in OOP | Very rarely (months/years) |
| **Instance** | The actual data stored in the database at a particular moment | Objects of the class | Every insert/update/delete |

**Example** – A `Student` table schema:

```
Student(rollNo: int, name: varchar(20), age: int)
```

An instance (snapshot of data at one moment):

| rollNo | name  | age |
|--------|-------|-----|
| 101    | Alice | 20  |
| 102    | Bob   | 22  |

```mermaid
flowchart LR
    subgraph Schema
        S["Database Schema - Table definitions, constraints, relationships"]
    end
    subgraph Instance
        I["Database Instance - Actual data rows"]
    end
    S -- "defines structure for" --> I
    I -- "changes over time (insert, update, delete)" --> I
    S -- "remains stable" --> S
```

**State diagram** for instance changes over time:

```mermaid
stateDiagram-v2
    [*] --> Empty : Initial schema created
    Empty --> Populated : Insert data
    Populated --> Populated : Update or Delete rows
    Populated --> Empty : Truncate table
    Populated --> [*] : Drop database
```

**Important**:
- A database may have many instances over its lifetime, but only one schema (unless altered).
- Schema evolution (using `ALTER TABLE`) changes the blueprint but preserves existing data as much as possible.

---

## Summary Table

| Concept | Key Point |
|---------|-----------|
| **DBMS** | Software for managing structured data with security, concurrency, and recovery |
| **Advantages over file system** | No redundancy, consistency, concurrency, security, integrity |
| **Data abstraction levels** | Physical (storage), Logical (tables), View (user‑specific) |
| **Data independence** | Logical (schema changes hide from views) & Physical (storage changes hide from schema) |
| **Schema vs Instance** | Schema = blueprint (stable); Instance = actual data (dynamic) |

---