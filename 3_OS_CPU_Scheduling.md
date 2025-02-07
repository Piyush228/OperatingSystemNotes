
# CPU Scheduling in OS   

## **🔹 What is CPU Scheduling?**  
CPU scheduling is the process of selecting a process from the **ready queue** and assigning it to the CPU for execution. Since there are multiple processes waiting, the OS must decide which process will execute **next** to ensure **efficient CPU utilization** and **fairness**.

---

## **📌 Process Scheduling Types**  
Process scheduling is categorized into three types based on when decisions are made:

| **Scheduler Type** | **Function** | **Frequency** |
|-------------------|-------------|--------------|
| **Long-Term Scheduler** | Controls the admission of new processes into the system (decides which jobs enter the ready queue). | **Infrequent** (Runs when a new process starts) |
| **Medium-Term Scheduler** | Swaps processes in and out of memory (used in virtual memory-based systems). | **Occasional** |
| **Short-Term Scheduler (CPU Scheduler)** | Decides which process gets the CPU next from the ready queue. | **Frequent (Milliseconds level)** |

---

### **📌 Three Types of Schedulers in OS [In Simple Terms]**  

Schedulers **manage processes** at different stages. Think of it like a **restaurant** where customers (processes) arrive, wait for their turn, and get served.  

| **Scheduler Type** | **What it Does?** | **How Often It Works?** | **Example** |
|-------------------|----------------|----------------|----------------|
| **Long-Term Scheduler** | Decides which processes **should enter the system** for execution. | **Rarely runs** (only when new processes start). | Like a **restaurant manager** deciding how many customers to allow inside at a time. |
| **Medium-Term Scheduler** | Temporarily **removes processes from memory** (swapping) to make space for more important ones. | **Occasionally runs** (when memory is full). | Like a waiter **asking a customer to wait outside** if the restaurant is full. |
| **Short-Term Scheduler (CPU Scheduler)** | Decides **which process runs next on the CPU**. | **Very frequently runs** (every few milliseconds). | Like a chef deciding **which dish to cook next** from the pending orders. |

---

### **📌 Example: A Restaurant Analogy** 🍽️  

Imagine a **restaurant** where customers (processes) come in and place orders. The restaurant has limited tables (CPU & memory), so it needs a system to manage them efficiently.  

1️⃣ **Long-Term Scheduler (Entry Management)**  
   - If too many customers arrive, the **restaurant manager** (Long-Term Scheduler) **limits** how many can enter.  
   - If the restaurant has only **10 tables**, but **20 customers** arrive, the manager lets in only **10** and tells the rest to wait outside.  
   - In OS, this means **limiting the number of processes in the system** to prevent overload.  

2️⃣ **Medium-Term Scheduler (Swapping Out Customers)**  
   - If the restaurant is **too crowded**, the **manager** may **ask some customers to wait outside** for a while and call them back later.  
   - This is similar to **swapping** in OS: some processes are temporarily removed from memory to free up space.  

3️⃣ **Short-Term Scheduler (Who Gets Served Next?)**  
   - The **chef (CPU)** decides **which order to cook first**.  
   - If a **VIP guest (high-priority process)** arrives, the chef **starts preparing their dish first** (like priority scheduling).  
   - If orders are taken in the **order they arrived**, it's like **First Come, First Serve (FCFS) scheduling**.  

---

### **📌 Key Takeaways**  
- **Long-Term Scheduler** decides **who enters the system** (controls workload).  
- **Medium-Term Scheduler** decides **who needs to be temporarily removed** (memory management).  
- **Short-Term Scheduler** decides **who gets CPU next** (ensures quick task execution).  


📌 **Diagram of Process Scheduling**  
```plaintext
+------------------+
| New Processes   |
+------------------+
       ↓   (Long-Term Scheduler)
+------------------+
| Ready Queue     |
+------------------+
       ↓   (Short-Term Scheduler)
+------------------+
| CPU Execution   |
+------------------+
       ↓   (Process completes or moves to I/O)
+------------------+
| Waiting Queue   |
+------------------+
       ↑   (Medium-Term Scheduler)
```
✅ **Short-Term Scheduler is the most important** because it decides which process gets CPU time!

---

## **📌 Preemptive vs Non-Preemptive Scheduling**  

| **Type** | **Description** | **Example** |
|----------|----------------|-------------|
| **Preemptive Scheduling** | CPU can switch to another process **before** the current process completes. | Round Robin, Preemptive SJF [Shortest Job First], Preemptive Priority Scheduling |
| **Non-Preemptive Scheduling** | Once a process starts executing, it **runs until it completes or goes into waiting**. | FCFS, Non-Preemptive SJF, Non-Preemptive Priority Scheduling |

📌📌📌 **Example:**  📌📌📌  
- **Preemptive:** If process **P1** is running and a higher priority process **P2** arrives, **P1 is paused**, and **P2 runs**.
- **Non-Preemptive:** Once **P1** starts, it **runs until completion** before **P2** gets CPU.

---

## **📌 CPU Scheduling Algorithms**  

### **1️⃣ First Come First Serve (FCFS)**
📌 **Concept**: The process that arrives **first** gets the CPU first.  
📌 **Type**: **Non-Preemptive**  

#### **Example:**  
| Process | Arrival Time | Burst Time |
|---------|-------------|------------|
| P1      | 0 ms        | 5 ms       |
| P2      | 1 ms        | 3 ms       |
| P3      | 2 ms        | 8 ms       |

**Gantt Chart:**  
```plaintext
| P1 | P2 | P3 |
0    5    8   16
```
✅ **Drawback**: **Higher waiting time for longer processes (Convoy effect).**

---

### **2️⃣ Shortest Job First (SJF)**
📌 **Concept**: The process with the **shortest burst time** executes first.  
📌 **Type**: Can be **Preemptive** or **Non-Preemptive**  

#### **Example (Non-Preemptive SJF):**  
| Process | Arrival Time | Burst Time |
|---------|-------------|------------|
| P1      | 0 ms        | 7 ms       |
| P2      | 1 ms        | 3 ms       |
| P3      | 2 ms        | 2 ms       |

**Gantt Chart:**  
```plaintext
| P3 | P2 | P1 |
2    5    12
```
✅ **Advantage**: Minimizes average waiting time.  
❌ **Disadvantage**: Can cause **Starvation** (long processes may never get CPU).

---

### **3️⃣ Round Robin (RR)**
📌 **Concept**: Each process gets CPU for a **fixed time quantum** (e.g., 2ms). If it doesn’t finish, it goes back to the ready queue.  
📌 **Type**: **Preemptive**  

#### **Example (Quantum = 2ms):**  
| Process | Arrival Time | Burst Time |
|---------|-------------|------------|
| P1      | 0 ms        | 5 ms       |
| P2      | 1 ms        | 3 ms       |
| P3      | 2 ms        | 4 ms       |

**Gantt Chart:**  
```plaintext
| P1 | P2 | P3 | P1 | P3 | P1 |
0    2    4    6    8    10   12
```
✅ **Advantage**: Ensures fairness & prevents **Starvation**.  
❌ **Disadvantage**: Too small time quantum leads to **frequent context switching**.

---

### **4️⃣ Priority Scheduling**
📌 **Concept**: The process with **higher priority** gets CPU first.  
📌 **Type**: Can be **Preemptive** or **Non-Preemptive**  

#### **Example:**  
| Process | Arrival Time | Burst Time | Priority (Lower = Higher Priority) |
|---------|-------------|------------|-----------------------------------|
| P1      | 0 ms        | 5 ms       | 3                                 |
| P2      | 1 ms        | 3 ms       | 1                                 |
| P3      | 2 ms        | 8 ms       | 2                                 |

**Gantt Chart:**  
```plaintext
| P2 | P3 | P1 |
1    4    12
```
✅ **Advantage**: Important processes get CPU first.  
❌ **Disadvantage**: Can lead to **Starvation** (low-priority processes may never run).

📌 **Solution to Starvation**: **Aging** (increase priority of waiting processes over time).

---

## **📌 Summary Table**  
| **Algorithm** | **Type** | **Best Used For** | **Disadvantages** |
|--------------|---------|------------------|------------------|
| **FCFS** | Non-Preemptive | Simple, First-Come execution | High waiting time (Convoy effect) |
| **SJF** | Both | Minimum waiting time | Starvation of long processes |
| **Round Robin** | Preemptive | Fair CPU time for all | Too many context switches if quantum is too small |
| **Priority Scheduling** | Both | High-priority task execution | Starvation of low-priority tasks |

---

## **🔥 Final Thoughts**
- **FCFS** is **easy but inefficient** for multitasking.
- **SJF** gives **lowest average waiting time** but can cause **starvation**.
- **Round Robin** ensures **fair CPU time** but needs a **good time quantum**.
- **Priority Scheduling** is useful for **critical tasks**, but **aging is needed** to prevent starvation.

---
---
