## **Threads**  
A **thread** is a small task running inside a program (process).  
Think of it like a worker inside a factory. A program can have multiple threads working together to complete tasks faster.  

---

### **Threads vs Processes (Simple Explanation)**  

| Feature            | Process (Big Program) | Thread (Small Task in a Program) |
|--------------------|----------------------|---------------------------------|
| **What it is?**   | A full program running independently. | A smaller part of a program doing work. |
| **Memory**        | Each process has its own memory. | Threads share memory inside the process. |
| **Communication** | Harder (needs special techniques like IPC). | Easier (they can share data easily). |
| **Speed**        | Slower to create and manage. | Faster to create and switch between. |
| **Crashes**      | One process crash doesn’t affect others. | If one thread crashes, it may crash the whole program. |
| **Example**      | Chrome and MS Word running separately. | Multiple tabs inside Chrome running together. |

---
**Simple Analogy:**  
- A **process** is like a full restaurant. It has its own kitchen, tables, and staff.  
- A **thread** is like a waiter in the restaurant. Multiple waiters (threads) work together in the same restaurant (process) to serve customers efficiently.  
---

### **User-Level vs Kernel-Level Threads**  

| Feature            | User-Level Threads (ULT) | Kernel-Level Threads (KLT) |
|--------------------|------------------------|----------------------------|
| **Managed by**    | User-space libraries    | Operating system kernel    |
| **Context Switching** | Faster (no system call) | Slower (requires system call) |
| **Scheduling**    | Handled in user space  | Managed by OS scheduler    |
| **Blocking**      | One blocked thread blocks all | One blocked thread doesn’t affect others |
| **OS Awareness**  | OS is unaware of threads | OS manages individual threads |
| **Performance**   | Faster but limited control | Slower but better system optimization |
| **Example**       | Java Threads, Pthreads (user mode) | Windows Threads, Linux `kthread` |

---

### **Process-based vs Thread-based Multitasking**  

| Feature            | Process-based Multitasking | Thread-based Multitasking |
|--------------------|--------------------------|--------------------------|
| **Definition**    | Running multiple processes | Running multiple threads in a single process |
| **Memory Space**  | Each process has separate memory | Threads share memory within the process |
| **Communication** | Expensive (IPC needed)    | Faster (shared memory) |
| **Context Switching** | Slow (high overhead)   | Fast (less overhead) |
| **Example**       | Running Chrome & VS Code  | Multiple tabs in Chrome |

---

### **Multi-threading Models**  

| Model | Description | Pros | Cons | Example |
|-------|------------|------|------|---------|
| **Many-to-One** | Multiple user threads map to **one** kernel thread | Easy to manage | No parallelism, blocking affects all threads | Green threads (older JVMs) |
| **One-to-One** | Each user thread maps to **one** kernel thread | True parallelism, independent scheduling | High overhead | Windows & Linux pthreads |
| **Many-to-Many** | Multiple user threads map to **a few** kernel threads | Balanced performance, avoids blocking issues | Complex implementation | Solaris, modern Linux pthreads |

---
