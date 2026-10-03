# Technical Interview + HR Prep

This document contains a comprehensive question bank and prep guide for the technical and HR interview rounds for **Specialist Programmer (SP)** and **Digital Specialist Engineer (DSE)** roles.

---

## 1. Object-Oriented Programming (OOP) — 30-Question Bank

### A. Core Pillars & Principles
1. **Explain Encapsulation with a real-world example.**
   - *Key Point*: Binding data and methods into a single unit (class) and hiding internal implementation using access modifiers (`private`/`protected`). Example: A bank account hiding `balance` and exposing `deposit()`/`withdraw()`.
2. **What is Abstraction and how does it differ from Encapsulation?**
   - *Key Point*: Abstraction hides *complexity* (showing *what* an object does), while encapsulation hides *data/state* (showing *how* access is restricted). Abstract classes and interfaces achieve abstraction.
3. **Differentiate between Single, Multiple, Multilevel, Hierarchical, and Hybrid Inheritance.**
   - *Key Point*: Highlight that Java does not support multiple inheritance with classes (to avoid the Diamond Problem), but achieves it through interfaces. C++ supports multiple inheritance directly.
4. **What is Compile-Time vs. Run-Time Polymorphism?**
   - *Key Point*: Compile-time (Static): Method Overloading and Operator Overloading (resolved at compile time). Run-time (Dynamic): Method Overriding via virtual functions / dynamic dispatch (resolved at runtime).
5. **What is the Diamond Problem in Multiple Inheritance and how is it resolved?**
   - *Key Point*: Occurs when a class inherits from two classes that both inherit from a common superclass. Resolved in C++ using `virtual` inheritance, and in Java by using Interfaces with `default` methods.

### B. Class Design & Advanced OOP Concepts
6. **What is the difference between an Abstract Class and an Interface?**
   - *Key Point*: Abstract classes can have instance variables, constructors, and concrete methods. Interfaces (traditionally) contain only method signatures (though modern Java allows `default` and `static` methods). A class can implement multiple interfaces but extend only one abstract class.
7. **What is the purpose of constructors and destructors? Can a constructor be private?**
   - *Key Point*: Constructors initialize objects; destructors clean up resources. A private constructor prevents external instantiation (used in Singleton design pattern and utility classes).
8. **What is Method Overloading vs. Method Overriding?**
   - *Key Point*: Overloading: Same method name, different parameter list in the same class. Overriding: Same method signature in a subclass providing a specific implementation.
9. **Explain `super` and `this` keywords (or `base` and `this`).**
   - *Key Point*: `this` refers to the current object instance; `super` refers to the parent class instance or constructor.
10. **What is Composition vs. Inheritance ("Has-A" vs. "Is-A")? Why prefer Composition?**
    - *Key Point*: Inheritance creates tight coupling ("Is-A"). Composition combines objects ("Has-A"), providing greater flexibility, easier testing, and dynamic behavior swapping.

### C. Design Patterns & Best Practices
11. **Explain the Singleton Pattern and how to implement it safely.**
    - *Key Point*: Ensures a class has only one instance and provides a global point of access. In multi-threaded environments, use double-checked locking or static inner helper classes (Bill Pugh Singleton).
12. **What is the Factory Method Pattern?**
    - *Key Point*: Defines an interface for creating an object, but lets subclasses decide which class to instantiate.
13. **What is the Observer Pattern?**
    - *Key Point*: Defines a one-to-many dependency where when one object changes state, all its dependents are notified automatically (e.g., event listeners, pub/sub).
14. **What are the SOLID principles? Summarize each letter.**
    - *Key Point*: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion.
15. **What is a Copy Constructor and Deep Copy vs. Shallow Copy?**
    - *Key Point*: Shallow copy copies primitive values and reference pointers (shared memory). Deep copy duplicates referenced objects recursively, creating independent memory copies.

### D. Language-Specific OOP Quirks (Java / C++ / Python)
16. **Why is `String` immutable in Java?**
    - *Key Point*: Security, thread safety, string pooling (memory optimization), and hashing consistency (cached hash code).
17. **What is the `final` / `const` keyword in Java/C++?**
    - *Key Point*: `final` class cannot be inherited; `final` method cannot be overridden; `final` variable cannot be reassigned.
18. **Explain Virtual Functions and VTables in C++.**
    - *Key Point*: Virtual functions enable runtime dynamic dispatch via a Virtual Table (vtable) and Virtual Pointer (vptr) per object instance.
19. **What are Garbage Collection basics and `finalize()` / `System.gc()` in Java?**
    - *Key Point*: Automatic memory management tracking unreferenced objects using mark-and-sweep algorithms. `System.gc()` is a request, not a guarantee.
20. **What is Method Hiding (Static Method Overriding)?**
    - *Key Point*: If a subclass defines a static method with the same signature as a static method in the superclass, the method is hidden, not overridden. Resolves by reference type, not instance type.

### E. Practical Design Questions
21. **Design a class hierarchy for a Vehicle Rental System.**
22. **Design an Employee Payroll System using Inheritance and Abstract Classes.**
23. **How would you handle Exception Handling in OOP cleanly?**
24. **What is Dependency Injection and why is it useful?**
25. **What is the difference between Static and Dynamic Binding?**
26. **Explain Interface Segregation Principle with a code example.**
27. **What is an Inline Function in C++?**
28. **How does Python handle OOP and Private Attributes (`__var`)?**
29. **What is Operator Overloading? Give an example.**
30. **What is a Destructor vs. Garbage Collector?**

---

## 2. SQL & DBMS — 20-Question Practice Bank

### A. SQL Query Writing Prompts
1. **Find the 2nd Highest Salary from an `Employee` table.**
   ```sql
   SELECT MAX(salary) FROM Employee 
   WHERE salary < (SELECT MAX(salary) FROM Employee);
   -- Or using OFFSET:
   SELECT DISTINCT salary FROM Employee ORDER BY salary DESC LIMIT 1 OFFSET 1;
   ```
2. **Find all employees who earn more than their direct manager.**
   ```sql
   SELECT e.name AS Employee 
   FROM Employee e 
   JOIN Employee m ON e.manager_id = m.id 
   WHERE e.salary > m.salary;
   ```
3. **Find duplicate email addresses in a `Users` table.**
   ```sql
   SELECT email FROM Users 
   GROUP BY email 
   HAVING COUNT(email) > 1;
   ```
4. **Get the top 3 highest-paid employees in each department using Window Functions.**
   ```sql
   WITH RankedEmployees AS (
       SELECT name, salary, department_id,
              DENSE_RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) as rnk
       FROM Employee
   )
   SELECT name, salary, department_id FROM RankedEmployees WHERE rnk <= 3;
   ```
5. **Delete duplicate records from a table while keeping the row with the lowest `id`.**
   ```sql
   DELETE e1 FROM Employee e1
   INNER JOIN Employee e2 
   ON e1.email = e2.email AND e1.id > e2.id;
   ```
6. **Write a query to find employees who have NOT placed any orders (`LEFT JOIN` / `NOT EXISTS`).**
7. **Calculate the 7-day moving average of daily sales.**
8. **Pivot a monthly sales table into quarterly columns.**
9. **Find consecutive available seats in a cinema database.**
10. **Retrieve all records where a text column contains a specific substring pattern (`LIKE` / Regex).**

### B. DBMS Theory & Database Architecture
11. **Explain the ACID properties of a Transaction.**
    - *Atomicity* (All or nothing), *Consistency* (Valid state transitions), *Isolation* (Concurrent transactions don't interfere), *Durability* (Committed data survives crashes). Use a Bank Transfer scenario.
12. **Differentiate between `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, and `FULL OUTER JOIN`.**
13. **What is Normalization? Explain 1NF, 2NF, 3NF, and BCNF.**
    - *1NF*: Atomic values, no repeating groups.
    - *2NF*: 1NF + no partial dependency (all non-key attributes fully dependent on primary key).
    - *3NF*: 2NF + no transitive dependency (non-key attributes depend only on primary key).
    - *BCNF*: 3NF + for every functional dependency $X \rightarrow Y$, $X$ must be a super key.
14. **What is Indexing in SQL? How do B-Trees and Hash Indexes work?**
    - *Key Point*: Indexes speed up SELECT queries at the cost of slower INSERT/UPDATE operations. B-Trees support range queries ($O(\log N)$); Hash indexes support exact match lookups ($O(1)$).
15. **What is the difference between `WHERE` and `HAVING` clauses?**
    - `WHERE` filters rows *before* aggregation; `HAVING` filters aggregated groups *after* `GROUP BY`.
16. **Differentiate between `TRUNCATE`, `DROP`, and `DELETE`.**
    - `DELETE`: DML command, deletes specific rows, row-by-row logging, rollback possible.
    - `TRUNCATE`: DDL command, removes all rows by deallocating pages, faster, rollback DB dependent.
    - `DROP`: DDL command, removes entire table structure and data from schema.
17. **What is Primary Key vs. Unique Key vs. Foreign Key?**
18. **Explain Database Deadlocks and how DBMS detects/prevents them.**
19. **What is Clustered vs. Non-Clustered Index?**
    - Clustered index alters physical storage order of data (only 1 per table). Non-clustered index stores logical index pointers separate from data rows (multiple per table).
20. **What is Database Sharding vs. Replication?**

---

## 3. Computer Science Fundamentals (OS & Computer Networks)

### Operating Systems (OS)
- **Process vs. Thread**: A process is an independent executing program with its own memory address space. A thread is a lightweight execution unit inside a process sharing memory/resources.
- **Deadlock Conditions (Coffman Conditions)**: 1. Mutual Exclusion, 2. Hold and Wait, 3. No Preemption, 4. Circular Wait.
- **CPU Scheduling Algorithms**: FCFS, Shortest Job First (SJF), Round Robin (RR), Priority Scheduling. Differentiate preemptive vs non-preemptive.
- **Virtual Memory & Paging**: Virtual memory allows execution of processes larger than physical RAM. Paging divides memory into fixed-size pages. Page Fault occurs when a referenced page is not in RAM.

### Computer Networks (CN)
- **OSI Model 7 Layers**: Application, Presentation, Session, Transport, Network, Data Link, Physical.
- **TCP vs. UDP**:
  - *TCP*: Connection-oriented, reliable, guaranteed delivery, flow/congestion control, three-way handshake (SYN, SYN-ACK, ACK).
  - *UDP*: Connectionless, fast, unreliable/unacknowledged, lower overhead (ideal for streaming, gaming, DNS).
- **HTTP vs. HTTPS**: HTTPS encrypts traffic using TLS/SSL over port 43, while HTTP transmits unencrypted plaintext over port 80.
- **GET vs. POST**: GET requests data (parameters in URL, idempotent). POST submits data to be processed (data in payload body, non-idempotent).

---

## 4. HR & Behavioral Round — 20-Prompt Bank

1. **"Tell me about yourself and walk me through your technical background."**
   - *Strategy*: Keep it to 90 seconds. Present structure: Education $\rightarrow$ Key Technical Skills & Projects $\rightarrow$ Internship/Achievements $\rightarrow$ Why you're excited for SP/DSE.
2. **"Why Infosys? Why SP/DSE specifically instead of standard SE?"**
   - *Strategy*: Highlight Infosys' digital transformation focus, global presence, continuous training infrastructure (Infosys Springboard/Mysore training campus), and your ambition to work on core engineering problems.
3. **"Describe a time you faced a major technical bug or project roadblock. How did you resolve it?"**
   - *Strategy*: Use STAR Method (Situation, Task, Action, Result). Focus on debugging tools, systematic isolation, git rollback, or consulting documentation.
4. **"How do you handle disagreement with a teammate over technology stack or design choice?"**
   - *Strategy*: Focus on data-driven discussion, benchmark comparisons, listening to trade-offs, and aligning with project deadlines.
5. **"Where do you see yourself in 3 to 5 years technical career-wise?"**
   - *Strategy*: Technical leadership / Senior Architect track. Continuous learning, mastering cloud/system architecture, and mentoring junior engineers.
6. **Describe a situation where you had to work under tight deadlines.**
7. **What is your biggest technical strength and your biggest area of improvement?**
8. **Have you ever failed a project or missed a deadline? What did you learn?**
9. **How do you keep yourself updated with new technologies and frameworks?**
10. **Are you comfortable relocating to any Infosys DC (Development Center) across India or working in shifts if required?**
11. **Explain a complex technical concept from your project to a non-technical person.**
12. **What would you do if you are assigned a technology stack you have never worked on before?**
13. **What makes you a good team player?**
14. **How do you handle feedback or criticism on your code during peer code reviews?**
15. **If you have multiple competing deadlines, how do you prioritize tasks?**
16. **What is your understanding of Infosys' core values (C-LIFE - Client Value, Leadership by Example, Integrity & Transparency, Fairness, Excellence)?**
17. **Why should we hire you over other candidates?**
18. **Tell me about an internship or project experience that didn't go as planned.**
19. **What are your salary expectations or expectations from the SP/DSE training program?**
20. **Do you have any questions for us?** (Always ask 2 smart questions about engineering stack or team structure!).

---

## 5. Mock Technical Interview Walkthrough Scenarios

### Scenario 1: Array & Algorithm Optimization Pivot
- **Interviewer**: "Given an array of integers, find if there exist two numbers that sum up to Target."
- **Candidate Answer**: "Brute force uses two nested loops in $O(N^2)$ time. We can optimize to $O(N)$ time using a Hash Map by storing each number's complement (`Target - num`)."
- **Follow-up Probe**: "What if the array is already sorted and we are constrained to $O(1)$ extra space?"
- **Candidate Answer**: "We use Two Pointers starting at index `0` and `N-1`. If `sum < Target`, increment `left`; if `sum > Target`, decrement `right`."

### Scenario 2: OOP & Class Design Deep-Dive
- **Interviewer**: "Design a Car Rental System using Object-Oriented Principles."
- **Candidate Answer**: Outlines `Vehicle` base class, `Car`/`Bike` subclasses, `RentalReservation`, `Customer`, and `PaymentProcessor`. Demonstrates Encapsulation (private fields), Polymorphism (`calculateRentalFee()`), and Factory pattern for creating vehicle types.

### Scenario 3: SQL Optimization & Indexing Pivot
- **Interviewer**: "Your SQL query taking 15 seconds to execute on a 10-million-row table. How do you debug it?"
- **Candidate Answer**: "1. Run `EXPLAIN ANALYZE` to check for full table scans. 2. Verify if proper Indexes exist on columns used in `WHERE` and `JOIN` clauses. 3. Avoid wildcard leads like `LIKE '%term'`. 4. Ensure window functions or subqueries are not repeating redundant computations."

### Scenario 4: Resume Project Defense
- **Interviewer**: "You used FastAPI and MongoDB in your project. Why NoSQL over SQL for this use case?"
- **Candidate Answer**: Explains schema flexibility, JSON document structure alignment with REST API payloads, horizontal scaling requirement, vs relational integrity tradeoffs.

### Scenario 5: Live Code Optimization & Big-O Defense
- **Interviewer**: "Can you write a function to detect if a directed graph contains a cycle?"
- **Candidate Answer**: Demonstrates DFS with 3-color marking (`UNVISITED`, `VISITING`, `VISITED`) or Kahn's Algorithm (BFS with In-degree array). Explains $O(V + E)$ time and $O(V)$ space complexity.
