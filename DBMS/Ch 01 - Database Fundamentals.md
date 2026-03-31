## Chapter 1: Database Fundamentals

---

## 1. What is a DBMS?

<div align="center" style="margin: 20px 0;">
<img src="https://images.openai.com/static-rsc-4/2D2zeCfsggvthzggSfg447dXvXJhrR6x_i59p1vLaOWtBW52-WPuZH737RIb_Q3zS61OJYBDZvN8iBBfINUlcrCdovpMMatosFInWynLHQJAfc_wMT47uY-3HGyzIILVSsBDv9NBWYM7NipTZrDx8CQxXy7rIly1VKC-J2uAbyK1QLOBkBIMvpUSLMq1EhdV?purpose=fullsize" width="280" height="200" />
<img src="https://images.openai.com/static-rsc-4/sE2Zn4FktE3vdr89PFHwTpnTjdokIHxaqZcJ1Qy69o3HZAOwYogWO92_3EzUHXN30Fm5ff7eYxnlwysxXPy4TMYldjSRIKGp1nxZiWPwaL23mPSJKSv_vpbUT2pBhkheRecn59beCCYw5Ws0LUK6DQUk1Mffg_LjAE2PXOlAHi9nfMzUectXjYR9UcmFJH7P?purpose=fullsize" width="280" height="200" />
<img src="https://images.openai.com/static-rsc-4/v8t7C-JLFbcaSdhXXKiA1_aZZfqjYrLukewmAaDBLm5H_76QWnVbhAhm11MhiXh_hRf37gZl9KOASjPEuxaRYJTFjC7DBRfbc01czmMnUNN7pCFyG42nFMYvfybbBlDqFqz_TYVZIDeytLo5m0fzPVvPxuKbCzOocBb3CTWhQmD4XfWsEK4BdyEIlw_4P12p?purpose=fullsize" width="280" height="200" />
</div>

A **Database Management System (DBMS)** is a software system that allows users to **store, organize, retrieve, and manage data efficiently**.

It provides:

* A **structured way** to store data
* **Query mechanisms** (like SQL)
* **Security and control** over data access

### How DBMS Works:

1. User sends a query (e.g., “Find student marks”)
2. DBMS processes the query
3. Data is fetched from database
4. Result is returned to the user

### Detailed Example:

Consider a **college management system**:

* Tables:

  * `Students(ID, Name, Course)`
  * `Marks(ID, Subject, Score)`
* If a teacher wants marks:

  ```sql
  SELECT Name, Score 
  FROM Students, Marks 
  WHERE Students.ID = Marks.ID;
  ```

DBMS handles storage, joins, and retrieval internally.

---

## 2. Advantages of DBMS over File System

<div align="center" style="margin: 20px 0;">
<img src="https://images.openai.com/static-rsc-4/_ck5vKXQ62VJyD4UVfqGM1V5ZFbKCWmxyYiO9hoAiTO_gNwcSoFgTiXnnLuSDRO6MoAQzZQT5FgArpNJgwDNPg-6T9Q1S0tXSMXV-fkzZizeOMefBSqrliciyXW0lBmg_FRIKX87Na29-snVXWHnwM9GT7Nd2tgJGITRhKLX8lsOhaTLIt0T1bJETQBsf-iK?purpose=fullsize" width="280" height="200" />
<img src="https://images.openai.com/static-rsc-4/Gu5eMltRDBsp9ChQyJLPSt0NNbUjzLquTORt7dlklxLIUmposoUmd89JzfUJ0j6oTa1m51QMyVudKyZ6drXkS9S2D0cT_MGDX0VX2LMM6hTs-W20g9AWDMkuAPBFjeTvKW23q2biHDJKJHxGT3fgPgKXkCOo28idc9UQFyquoSaPQOMOjdhDQGDlpvRTIpQE?purpose=fullsize" width="280" height="200" />
</div>



### Problem with File System:

Data is stored in separate files → leads to duplication and inconsistency.

### Example (File System Issue):

* Student name stored in:

  * Fee file
  * Marks file
* If name changes in one file but not the other → **inconsistency**

### DBMS Solutions:

| Feature        | File System    | DBMS     |
| -------------- | -------------- | -------- |
| Redundancy     | High           | Low      |
| Consistency    | Poor           | High     |
| Security       | Limited        | Strong   |
| Data Integrity | No constraints | Enforced |
| Concurrency    | Difficult      | Managed  |

### Real Example:

* In DBMS, updating student name updates it everywhere due to centralized storage.

---

## 3. Data Abstraction

<div align="center" style="margin: 20px 0;">
<img src="https://images.openai.com/static-rsc-4/j73MQuqcKwnwvO7XuAD-_zfu-vGjifmMeFVoLAOW5jVcPplHR4GdWhXEjI-Rbhh268yLb7jfJXCW0jN1YhQjwJhnT17U_i9owfzRYcuvojsgiQFoQVfWrJ8T2WMQYiPGqZk5Z3vdsnUZGE-p9NuNj-c7VVsMfu4be-84-zbf2aaM9uSn-UGeFV3ubQGobGoH?purpose=fullsize" width="300" height="200" />
<img src="https://images.openai.com/static-rsc-4/0ovaj8Nk2tMpEz6ykF138DHBjGv30Ve5TXKYydD8OudNXz-Ul1gWrM2JyasGfgowJEOlO2zTduo_CmM1DetL9qQja1f7p9h6217fd55ipAb8xAo_6-Fc6UEr_GgNrkYhTbhsXJvdG_0iTwZcn9XJm0uUM30M7hGALjMYs8S7UBcpzR8JP07oe5CVFgsRXfLV?purpose=fullsize" width="300" height="200" />
</div>

Data abstraction means **hiding complex details and showing only necessary information**.

### Levels of Abstraction:

### 1. Physical Level (Internal Level)

* Describes how data is stored physically.
* Example:

  * Data stored using indexes, B-trees.

### 2. Logical Level (Conceptual Level)

* Describes structure of database.
* Example:

  ```sql
  Student(ID, Name, Course)
  ```

### 3. View Level (External Level)

* User-specific view of data.
* Example:

  * Admin sees full details
  * Teacher sees only Name and Marks

### Analogy:

* Physical → Hard disk storage
* Logical → Table structure
* View → What user sees

---

## 4. Data Independence

<div align="center" style="margin: 20px 0;">
<img src="https://images.openai.com/static-rsc-4/uyGICWljSIREeCCOoAXikBcFYRoNZYHZOWSL4ejrLX7EPTXUUowPeZoTLJ4bqbFYs_5nb3uwGZffUkXTR0g9-uy1-4AYw_C_UDg9__D5A8e8stx5zSXKU67EsX1pgEjp1EZos29QPjgI2sokjqciQ5hAHY97Q1SLI3ilt2PYjgQCJz0ft1uK1IgZK7THuWjE?purpose=fullsize" width="280" height="200" />
<img src="https://images.openai.com/static-rsc-4/uoZDKhLmbhTG1deDskiVDYrhmB1uwlDaOOlTliibQVMHZbq5PLk0roUrGr7otQKsO4nNIMdPoQTffPQYxQFlu-SppZ3YzuQIQdBibnoRLidGvKtGmvBGIJsXpTCw_pkfZwciQpaGhoEw_NFvclvA2TLCkDCLNCgOsL97oiZP-2GsbjjBV2PqgWOlXL02vUb5?purpose=fullsize" width="280" height="200" />
<img src="https://images.openai.com/static-rsc-4/_GtEOOiSouEcmCMETW-P4fw-_iI4mTWUuS6xzydNvXOCvByE_tWK3wLWRtB0LgWwRFaAZ8g07KsqzbQbjaibsbYKQKamS7spxjAjWBpBvkPhJEHAtAI5BRsmI_mRQWd_8sGx1nM5ohsFSFJiVpFS12Xq7ITRkO0lWa-GUoTDNEbDNFznPsbuu5EJ83TUlwRh?purpose=fullsize" width="280" height="200" />
</div>

Data independence ensures that **changes at one level do not affect others**.

### Types:

### 1. Physical Data Independence

* Change storage without affecting logical schema.
* Example:

  * Switching from linked list to B-tree storage.

### 2. Logical Data Independence

* Change logical schema without affecting views.
* Example:

  * Adding a column:

    ```sql
    ALTER TABLE Student ADD Age INT;
    ```
  * Existing applications still work.

---

## 5. Schema vs Instance

<div align="center" style="margin: 20px 0;">
<img src="https://images.openai.com/static-rsc-4/W8KfDIGsq0UGv9tPSEtS_pX9-iGyU9E1qLHiYIWDwX8U_oZaWzfvXlV4zhicpi23enFJO4oOT8AMWPPXXXzhzdjEPc8ZrK1U0wVGGZ9_iqQGsIzS-ua0Fq9rd7U56hyrpQG7c5hVwlBVO8TZQLCO6tJ1FP_BtO_AwQ8Tt55itpslr1zA791zzWkqI3BykyCS?purpose=fullsize" width="300" height="200" />
<img src="https://images.openai.com/static-rsc-4/azjxERBwzFi6Z3hVvrVdtfuxDFA5hpGr9gTMnbbzwCQzxWlGHv0HPr1-bBvSs2KVaU9e3WyZpwpIOMN5SY7Z2IooQtJTNHu_W7FJLmBHZS9_EL3H54fZD4Bx3d50wsR08S9p4-ihMeoz6Zrj9NtyGc67Hzh1BYPjA5tDxVWrswxtv_058LtuBvqOKxeiDMXk?purpose=fullsize" width="300" height="200" />
</div>


### Schema:

* Structure/design of database
* Defined once
* Rarely changes

Example:

```sql
Student(ID, Name, Course)
```

### Instance:

* Actual data at a particular time
* Changes frequently

Example (Instance at time T1):

```
1, Manish, CSE
2, Rahul, ECE
```

Example (Instance at time T2):

```
1, Manish, CSE
2, Rahul, ECE
3, Ankit, IT
```

### Key Difference:

| Feature | Schema           | Instance   |
| ------- | ---------------- | ---------- |
| Meaning | Structure        | Data       |
| Changes | Rare             | Frequent   |
| Example | Table definition | Table rows |

---

# Practice Questions

## 🔹 Conceptual Questions

1. What is a DBMS? Explain with a real-life example.
2. Differentiate between DBMS and file system.
3. Explain the three levels of data abstraction with examples.
4. What is data independence? Why is it important?
5. Differentiate between physical and logical data independence.
6. Define schema and instance with examples.


