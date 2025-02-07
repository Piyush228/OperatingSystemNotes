## **🔹 What is a Process?**
A **process** is an **active entity** that represents **a running instance of a program**. It contains:
- **Program Code (Text Section)** – The actual instructions executed by the CPU.
- **Program Counter (PC)** – Keeps track of the next instruction to execute.
- **Stack** – Stores function calls, return addresses, local variables.
- **Heap** – Stores dynamically allocated memory.
- **Data Section** – Contains global/static variables.

📌 **Example:**  
When you open **Google Chrome**, multiple processes start running:
- One **main process** manages the UI.
- Separate **rendering processes** handle web pages.
- **Network processes** manage internet connections.

---

## **📌 Process Creation & Deletion**

### **🔹 Process Creation**  
When a process is created, the OS performs the following steps:
1. **Assigns a Unique Process ID (PID).**
2. **Allocates Memory (Stack, Heap, Data, Code).**
3. **Loads the Program Code into Memory.**
4. **Initializes Registers & Process Control Block (PCB).**
5. **Schedules the Process in the Ready Queue.**

📌 **Diagram for Process Creation**  
```plaintext
+--------------------+
| User Requests     |  (Program Execution)
+--------------------+
         ↓
+--------------------+
| OS Creates PCB    |
+--------------------+
         ↓
+--------------------+
| Allocates Memory  |
+--------------------+
         ↓
+--------------------+
| Loads into Ready  |  (Process waits for CPU)
+--------------------+
```

---

### **🔹 Process Creation Example in C (Using `fork()`)**
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    int pid = fork(); // Creates a new process

    if (pid == 0) {
        printf("Child Process: PID = %d\n", getpid());
    } else {
        printf("Parent Process: PID = %d\n", getpid());
    }

    return 0;
}
```
📌 **Process Tree Created**
```
Parent Process (PID 1001)
    |
    |---> fork() called
    |
    ├── Parent Process (PID 1001)
    ├── Child Process (PID 1002)
```
✅ **Each process gets a unique PID assigned by the OS.**

---

### **🔹 Process Termination (Deletion)**
A process can be **terminated** due to:
1. **Normal Exit** – Process finishes execution.
2. **Abort by Parent** – Parent process terminates the child.
3. **Timeout** – Exceeded execution time.
4. **Fatal Error** – Segmentation fault, illegal instruction.
5. **Killed by Another Process** – e.g., `kill` command in Linux.

📌 **Example: Killing a process in Linux**
```bash
ps
kill -9 <PID>
```
📌 **Diagram for Process Termination**
```plaintext
+--------------------+
| Process Running    |
+--------------------+
         ↓
+--------------------+
| OS Terminates PCB |
+--------------------+
         ↓
+--------------------+
| Frees Memory      |
+--------------------+
         ↓
+--------------------+
| Process Removed   |
+--------------------+
```

---

## **📌 Process States in OS**
A process goes through multiple states during execution.  

### **🔹 5 States of a Process**
📌 **Diagram for Process States**
```plaintext
         +---------+
         |  New    |  (Process Created)
         +---------+
              ↓
        +---------+       +-----------+
  ----- |  Ready  | ----> | Running   |
  |     +---------+       +-----------+
  |            ↑                |
  |            |                ↓
  |      +------------+    +-----------+
  |      |  Waiting   |    | Terminated |
  |      +------------+    +-----------+
  |            ↑
  |            |
  +------------+
```

| **State** | **Description** |
|-----------|----------------|
| **New** | Process is created but not yet scheduled for execution. |
| **Ready** | Process is waiting in the queue to be assigned a CPU. |
| **Running** | Process is being executed by the CPU. |
| **Waiting** | Process is waiting for I/O (e.g., reading a file). |
| **Terminated** | Process has completed execution and is removed from memory. |

📌 **Example:**  
- **Opening a Text Editor** → Moves to **New** state.
- **Waiting for CPU time** → Stays in **Ready** state.
- **Typing text** → Moves to **Running** state.
- **Saving the file** → Moves to **Waiting** state (I/O operation).
- **Closing the editor** → Moves to **Terminated** state.

---

## **📌 Process Control Block (PCB)**
The **Process Control Block (PCB)** stores all information about a process.

### **🔹 Structure of a PCB**
```
+---------------------------+
| Process ID (PID)          |
| Process State             |
| Program Counter (PC)      |
| CPU Registers             |
| Memory Information        |
| Open Files                |
| I/O Status                |
| Process Priority          |
+---------------------------+
```

📌 **Details Stored in PCB**
| **Field** | **Description** |
|-----------|----------------|
| **PID** | Unique process identifier |
| **State** | New, Ready, Running, Waiting, Terminated |
| **Program Counter** | Address of the next instruction to execute |
| **CPU Registers** | Stores process-specific register values |
| **Memory Info** | Base & limit registers, page tables |
| **I/O Status** | Devices allocated to the process |
| **Priority** | Used for scheduling decisions |

📌 **Diagram for PCB**
```plaintext
+------------------------------------------------+
| Process ID (PID) : 1234                        |
| State: Running                                 |
| Program Counter: 0x00432F                      |
| CPU Registers: {eax, ebx, ecx, edx}            |
| Memory: {Base: 0x1000, Limit: 0x2000}          |
| Open Files: {file1.txt, input.txt}             |
+------------------------------------------------+
```

✅ **Why PCB is Important?**
- **Stores process information** (ID, state, memory usage). 
- Helps OS **manage processes efficiently**.
- **Maintains process state** during context switching.
- Allows process **scheduling and execution tracking**.

---

## **📌 Summary (Deep Insights)**  
| **Concept** | **Explanation** |
|-------------|----------------|
| **Process** | Running instance of a program |
| **Process Creation** | `fork()` creates a new process |
| **Process Termination** | Happens when process completes or is forcefully terminated |
| **Process States** | New, Ready, Running, Waiting, Terminated |
| **PCB (Process Control Block)** | Stores all process details (PID, state, memory info, etc.) |

---

## **🔥 Final Thoughts**
- Every **running program is a process**.
- OS **manages multiple processes using process states**.
- **PCB stores process details** and is essential for multitasking.
- Understanding process creation (`fork()`), scheduling, and termination helps in **OS development & debugging**.


---
---
Here are some **important Linux commands** related to **process management** with **one-line explanations**:

| **Command** | **Explanation** |
|------------|----------------|
| `ps` | Lists currently running processes. |
| `ps aux` | Displays all processes with detailed info. |
| `top` | Shows real-time CPU & memory usage of processes. |
| `htop` | Interactive version of `top` for better process monitoring. |
| `pidof <process>` | Finds the PID of a running process. |
| `pgrep <name>` | Searches for processes by name and returns PID. |
| `kill <PID>` | Sends a termination signal to a process. |
| `kill -9 <PID>` | Forcefully kills a process. |
| `pkill <name>` | Kills a process by name instead of PID. |
| `nice -n <priority> <command>` | Starts a process with a given priority. |
| `renice <priority> <PID>` | Changes the priority of a running process. |
| `nohup <command> &` | Runs a process in the background and prevents termination after logout. |
| `jobs` | Lists background jobs. |
| `fg <job_id>` | Brings a background job to the foreground. |
| `bg <job_id>` | Resumes a stopped job in the background. |
| `strace -p <PID>` | Traces system calls made by a process. |
| `lsof -p <PID>` | Lists open files used by a process. |
| `watch -n 1 ps aux` | Monitors running processes every second. |
| `systemctl restart <service>` | Restarts a system service. |
| `service <name> stop/start` | Stops or starts a service. |

---
---

# **📌 CPU Scheduling in OS **  

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

