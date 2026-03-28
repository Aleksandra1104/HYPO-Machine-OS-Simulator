# HYPO OS & CPU Simulator (Java)

A Java-based simulation of a simple operating system and CPU architecture, implementing process management, memory allocation, scheduling, and instruction execution.

This project models core OS concepts such as process control blocks (PCBs), ready/waiting queues, dynamic memory management, and interrupt handling.

---

## Features

- **CPU Simulation**
  - Instruction execution with registers and stack support
  - Program Counter (PC) tracking and context switching

- **Absolute Loader**
  - Loads HYPO executable files into memory
  - Prepares processes for execution

- **Process Management**
  - Process Control Blocks (PCBs)
  - Ready Queue and Waiting Queue
  - Context switching (save/restore state)

- **Scheduling**
  - Priority-based scheduling
  - Time-slicing for process execution

- **Memory Management**
  - Dynamic allocation using free lists
  - Memory deallocation with block merging
  - Separation of OS and user memory regions

- **Interrupts & System Calls**
  - I/O completion handling
  - Memory allocation / deallocation
  - Clock get/set operations

- **Debugging & Logging**
  - Memory dump to console
  - Output logs for system state inspection

---

## Getting Started

### Compilation

```bash
javac HypoMachine.java
```

### Running the Simulator

```bash
java HypoMachine
```

### Running Executables

Once the simulator starts, you will be prompted to enter an interrupt ID:

```
Enter interrupt ID: 0 - no interrupt, 1 - run program, 2 - shutdown system, 3 - Input operation completion (io_getc), 4 - Output operation completion (io_putc): 
```

**To run an executable file:**

1. Enter `1` when prompted for the interrupt ID (to run a program)
2. When prompted for the filename, enter the executable file name (e.g., `executable1.txt`)

The simulator will load and execute the file. Output will be written to `output.txt` and displayed on the console.

**To shutdown the system:**
- Enter `2` when prompted for the interrupt ID

### Interrupt Types

- **0 - No interrupt**: Continue execution without processing an interrupt
- **1 - Run program**: Load and execute an executable file (e.g., `executable1.txt`)
- **2 - Shutdown system**: Terminate all processes and shutdown the simulator
- **3 - Input operation completion (io_getc)**: Handle input completion for a process that was waiting for character input. You will need to provide:
  - The Process ID (PID) of the process completing the input operation
  - A character to be read by the process (stored as ASCII value in the process's GPR4 register)
- **4 - Output operation completion (io_putc)**: Handle output completion for a process that was waiting to output a character. You will need to provide:
  - The Process ID (PID) of the process completing the output operation

#### Finding the Process ID (PID)

When a process is created, the simulator displays its Process Control Block (PCB) which includes the PID. The PID is printed to both the console and the `output.txt` file with the format:

```
Process Control Block <PID>
PCB address = ..., Next PCB Ptr = ..., PID = <PID>, State = ..., ...
```

The PID is automatically assigned starting from 1 and increments sequentially for each new process created. You can view the created processes and their PIDs from the console output or the `output.txt` file.