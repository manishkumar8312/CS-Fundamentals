# Chapter 2: Relational Model

The **Relational Model**, introduced by E.F. Codd in 1970, is the mathematical foundation of modern relational database systems. It organizes data into **relations** (tables) governed by strict structural and integrity rules. This chapter covers the core concepts tested in GATE.

---

## Table of Contents

1. [Core Terminology](#1-core-terminology)
2. [Keys](#2-keys)
3. [Integrity Constraints](#3-integrity-constraints)
4. [Relational Schema](#4-relational-schema)
5. [Quick Reference Summary](#5-quick-reference-summary)
6. [GATE PYQ Pointers](#6-gate-pyq-pointers)

---

## 1. Core Terminology

### Relation

A **relation** is a two-dimensional table with rows and columns. Formally, a relation $R$ on domains $D_1, D_2, \ldots, D_n$ is a subset of the Cartesian product $D_1 \times D_2 \times \cdots \times D_n$.

**Key properties of a relation:**

- Every cell contains exactly one atomic (indivisible) value — **1NF** requirement.
- All values in a column are of the same domain.
- Column order is insignificant.
- Row order is insignificant.
- No two rows are identical (no duplicate tuples).

**Example — `Student` Relation:**

| RollNo | Name    | Age | Branch |
|--------|---------|-----|--------|
| 101    | Arjun   | 20  | CSE    |
| 102    | Priya   | 21  | ECE    |
| 103    | Rahul   | 20  | CSE    |

---

### Tuple

A **tuple** is a single row in a relation. It represents one entity instance. In the example above, `(101, Arjun, 20, CSE)` is a tuple.

- The number of tuples in a relation is its **cardinality**.

---

### Attribute

An **attribute** is a named column of a relation. Each attribute has an associated **domain** — the set of permissible values.

- The number of attributes is the **degree** (or **arity**) of the relation.
- For the `Student` table: degree = 4, cardinality = 3.

---

### Domain

A **domain** is the set of all possible atomic values an attribute can take.

| Attribute | Domain Example         |
|-----------|------------------------|
| `Age`     | Integers in [1, 150]   |
| `Name`    | Strings of length ≤ 50 |
| `Branch`  | {CSE, ECE, ME, CE}     |

> **NULL** is a special marker indicating an unknown or missing value. NULL belongs to every domain.

---

## 2. Keys

Keys are used to **uniquely identify tuples** in a relation and to **establish relationships** between relations.

---

### 2.1 Super Key

> A **super key** is any set of one or more attributes that can **uniquely identify** every tuple in a relation.

A super key may contain extra (redundant) attributes.

**Example — `Student(RollNo, Name, Age, Branch)`:**

- `{RollNo}` — super key
- `{RollNo, Name}` — super key (redundant `Name`)
- `{RollNo, Name, Age}` — super key (redundant `Name`, `Age`)
- `{Name}` — NOT necessarily a super key (two students can share a name)

**Formula:** If $K$ is a super key of $R$, then for any two distinct tuples $t_1, t_2 \in R$: $t_1[K] \neq t_2[K]$.

---

### 2.2 Candidate Key

> A **candidate key** is a **minimal super key** — a super key with no redundant attributes.

Removing any attribute from a candidate key causes it to lose uniqueness.

**Example:**

Relation: `Employee(EmpID, Aadhar, Name, Dept)`

Suppose both `EmpID` and `Aadhar` uniquely identify an employee.

| Key | Is Minimal? | Is Candidate Key? |
|-----|-------------|-------------------|
| `{EmpID}` | Yes | **Yes** |
| `{Aadhar}` | Yes | **Yes** |
| `{EmpID, Aadhar}` | No | No (super key) |
| `{EmpID, Name}` | No | No (super key) |

> A relation may have **multiple candidate keys**. One of them is chosen as the primary key.

---

### 2.3 Primary Key

> A **primary key** is the candidate key **selected by the database designer** to uniquely identify tuples. It is denoted by underlining the attribute name in the schema.

**Rules:**

- Only **one** primary key per relation.
- Must be **unique** across all tuples.
- Must **not contain NULL** (Entity Integrity Rule).

**Schema Notation:**

```
Student(<u>RollNo</u>, Name, Age, Branch)
```

**Example:**

From the candidate keys `{EmpID}` and `{Aadhar}`, the designer chooses `EmpID` as the primary key.

```
Employee(<u>EmpID</u>, Aadhar, Name, Dept)
```

---

### 2.4 Foreign Key

> A **foreign key** is an attribute (or set of attributes) in relation $R_1$ that **references the primary key** of relation $R_2$, enforcing a link between the two relations.

**Rules:**

- The foreign key value must either match some primary key value in the referenced relation, or be NULL.
- This is enforced by the **Referential Integrity Constraint**.

**Example:**

```
Department(<u>DeptID</u>, DeptName)

Employee(<u>EmpID</u>, Name, DeptID*)
                              ↑
                    Foreign Key → references Department(DeptID)
```

| Employee |        |        |
|----------|--------|--------|
| EmpID    | Name   | DeptID |
| E01      | Arjun  | D01    |
| E02      | Priya  | D02    |
| E03      | Rahul  | D01    |

| Department |           |
|------------|-----------|
| DeptID     | DeptName  |
| D01        | CSE       |
| D02        | ECE       |

`DeptID` in `Employee` is a **foreign key** referencing `DeptID` in `Department`.

> **Important:** A foreign key need not have the same attribute name as the referenced primary key, but their **domains must match**.

---

### Key Hierarchy — Summary

```
All Attribute Subsets
        │
        ▼
    Super Keys
  (uniquely identify tuples)
        │
        ▼
  Candidate Keys
  (minimal super keys)
        │
        ▼
   Primary Key          ←── one candidate key selected
  (not null, unique)

   Foreign Key          ←── references a primary key in another relation
```

---

## 3. Integrity Constraints

Integrity constraints are **rules** enforced by the DBMS to maintain the correctness and consistency of the database.

---

### 3.1 Domain Constraint

Every attribute value must belong to the attribute's domain. No value outside the domain is permitted.

```
Age = -5     → VIOLATION (age cannot be negative)
Branch = XYZ → VIOLATION (XYZ not in {CSE, ECE, ME, CE})
```

---

### 3.2 Entity Integrity Constraint

> The **primary key** of a relation must **never be NULL**.

Since the primary key uniquely identifies a tuple, a NULL value would mean the tuple cannot be identified — which is logically unsound.

```
Student(RollNo=NULL, Name='Arjun', ...) → VIOLATION
```

---

### 3.3 Referential Integrity Constraint

> Every **foreign key** value must either:
> 1. Match a value in the **primary key of the referenced relation**, or  
> 2. Be **NULL**.

**Example violation:**

```
Employee(EmpID='E04', Name='Sneha', DeptID='D99')
```
If `D99` does not exist in `Department`, this is a **referential integrity violation**.

**On Delete / On Update Actions:**

| Action | Behavior |
|--------|----------|
| `CASCADE` | Propagate the change to referencing tuples |
| `SET NULL` | Set the foreign key to NULL |
| `SET DEFAULT` | Set the foreign key to its default value |
| `RESTRICT / NO ACTION` | Reject the operation |

---

### 3.4 Key Constraint

- All values of the primary key (and candidate keys) must be **unique** across all tuples.

---

### 3.5 Semantic Integrity (General Constraints)

Business rules not captured by the above, often enforced with `CHECK` clauses.

```sql
CHECK (Age >= 18 AND Age <= 60)
CHECK (Salary > 0)
```

---

## 4. Relational Schema

A **relational schema** is the **structural description** of a relation — its name, attributes, domains, and constraints. It does not contain actual data.

**Notation:**

```
RelationName(Attribute1 : Domain1, Attribute2 : Domain2, ..., AttributeN : DomainN)
```

Or more commonly in GATE:

```
RelationName(<u>PrimaryKeyAttr</u>, Attr2, Attr3, ForeignKeyAttr*)
```

---

### Full Schema Example

Consider a small university database:

```
Student(<u>RollNo</u>, Name, Age, DeptID*)

Department(<u>DeptID</u>, DeptName, HOD*)

Faculty(<u>FacultyID</u>, Name, DeptID*)

Course(<u>CourseID</u>, Title, Credits, FacultyID*)

Enrollment(<u>RollNo*</u>, <u>CourseID*</u>, Grade)
```

**Observations:**

- `Enrollment` has a **composite primary key** `(RollNo, CourseID)`.
- `Enrollment.RollNo` → foreign key referencing `Student(RollNo)`.
- `Enrollment.CourseID` → foreign key referencing `Course(CourseID)`.
- `Department.HOD` → foreign key referencing `Faculty(FacultyID)`.

---

### Schema vs Instance

| Aspect | Schema | Instance |
|--------|--------|----------|
| Definition | Structure / blueprint of the relation | Actual data stored at a point in time |
| Changes | Rarely (DDL operations) | Frequently (DML operations) |
| Also called | Intension | Extension |
| Example | `Student(RollNo, Name, Age)` | The rows in the `Student` table |

---

## 5. Quick Reference Summary

| Concept | Definition | Key Rule |
|---------|------------|----------|
| **Relation** | A table with rows and columns | No duplicate tuples; atomic values |
| **Tuple** | A single row | Represents one entity instance |
| **Attribute** | A named column | Has an associated domain |
| **Super Key** | Set of attributes that uniquely identifies tuples | May have redundant attributes |
| **Candidate Key** | Minimal super key | No proper subset is a super key |
| **Primary Key** | Chosen candidate key | Unique + NOT NULL |
| **Foreign Key** | Attribute referencing another relation's PK | Must match PK or be NULL |
| **Entity Integrity** | PK cannot be NULL | Mandatory |
| **Referential Integrity** | FK must match PK or be NULL | Enforced on insert/update/delete |
| **Domain Constraint** | Value must lie within attribute domain | Mandatory |
| **Schema** | Structural description of a relation | Does not include data |
| **Instance** | Actual data at a point in time | Changes with DML operations |

---

## 6. Summary 


1. **Counting super keys:** If a relation has $n$ attributes and the minimal candidate key has $k$ attributes, the number of super keys = $2^{n-k}$ (since any subset of non-key attributes can be added to the candidate key). Adjust when multiple candidate keys exist.

2. **Candidate key identification:** Given functional dependencies, find the closure of attribute sets and determine which sets are candidate keys (their closure = all attributes, and no proper subset achieves this).

3. **Referential integrity violations:** Given two tables and a DML operation, identify whether it violates referential integrity. Pay attention to insertions into the referencing table and deletions from the referenced table.

4. **NULL handling:** NULL is not equal to NULL (`NULL ≠ NULL` in SQL logic). Entity integrity prohibits NULL in primary keys. Foreign keys may be NULL.

5. **Schema normalization connection:** Understanding candidate keys is a prerequisite for BCNF/3NF questions in later chapters.
