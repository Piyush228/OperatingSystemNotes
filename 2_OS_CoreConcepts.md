## **🔹 What is a Process?**
A **process** is an **active entity** that represents a running instance of a program. It contains:
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
A process **transitions** through various states:

### **🔹 5 States of a Process**
📌 **Diagram for Process States**
```plaintext
         +---------+
         |  New    |  (Process Created)
         +---------+
              ↓
        +---------+       +-----------+
  ----> |  Ready  | ----> | Running   |
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

Would you like **real-world case studies** or **Linux command examples** related to process management? 😊