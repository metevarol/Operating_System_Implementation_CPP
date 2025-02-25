# Operating System Implementation

## Introduction
This project builds upon the Primitive Operating System implemented by Viktor Engelmann. The goal was to add new features to the existing system and document the improvements.

## Prerequisites

### 1- For Ubuntu 22.04.2, you need install:
```bash
sudo apt-get install g++ binutils libc6-dev-i386
sudo apt-get install VirtualBox grub2 xorriso
```
### 2- After that you can run this command:
```bash
make mykernel.iso
```
### 3- Then you should create new virtual machine with this ISO file on VirtualBox with name: "My Operating System".

### 4- After that you can run this command for open OS on VirtualBox
```bash
make run
```
## Operating System Kernel
The operating system kernel (`kernel.cpp`) performs basic functions such as managing hardware resources, handling interrupts, and providing system calls. Key components include:

- **Global Descriptor Table**: Manages memory segmentation, allowing the OS to safely access different memory segments.
- **Task Manager**: Enables multitasking by tracking all processes and managing their status, priority levels, and other parameters.
- **Interrupt Manager**: Manages interrupts generated by hardware or software.
- **Syscall Handler**: Handles system calls, enabling switching from user mode to kernel mode.
- **Driver Manager**: Manages hardware drivers and provides communication between hardware (e.g., keyboard, mouse) and the OS.

## Operating System Functions

### Multiprogramming
- **Process Management and Multitasking**: Managed by the `TaskManager` class, which contains an array of tasks and methods for creating new processes using `AddTask` and `fork`.
- **Process Table**: An array in the `TaskManager` class that stores all processes, selected and processed by the `Schedule` method.
- **Process**: Each `Task` class represents a process with fields such as `pid`, `ppid`, `priority`, etc.

### System Calls
- **POSIX System Calls**:
  - `sysfork()`: Creates a new process.
  - `getpid()`: Returns the PID of the current process.
  - `sysexit()`: Terminates the current process.
  - `waitpid()`: Makes a process wait for another process with a known PID.
  - `sysexecve()`: Sets a new entry point for the process to run a desired function.
- **Custom System Calls**:
  - `sys_process_table()`: Prints the process table.
  - `set_priority(int priority)`: Changes the current processing priority.
  - `sys_get_priority()`: Gets the current processing priority.
  - `sys_interrupt_count()`: Changes priority after a certain time.
  - `set_aging(int pid)`: Provides process aging to prevent starvation.
  - `set_state(int state)`: Updates the process state.

### Interrupt Handling
- **Timer Interrupts**: Activates the scheduler for multiprogramming.
- **Keyboard Interrupts**: Handles keyboard events and implements input functions.
- **Mouse Interrupts**: Handles mouse events such as movement and button clicks.

## Scheduler and Scheduling Strategies
- **Round Robin Scheduler**: Basic scheduler that switches processes on timer interrupts.
- **Round Robin with States and Waitpid Control**: Adds state control and waitpid features.
- **Priority-Based Round Robin Scheduler**: Runs high-priority processes first, supports aging to prevent starvation.

## Strategies and Implementations
- **Part A: Round Robin and Process Management**: Implements Round Robin scheduling for loaded tasks.
- **Part B: Priority-Based Scheduling**: Implements various strategies to prioritize processes.
- **Part C: Interactive Input Handling**: Implements strategies for handling interactive input from users.

## Sample Runs and Results
Sample runs and results are provided in the report, demonstrating the functionality of the implemented features and strategies.

Part A Sample Run:

![Part A - 1](https://github.com/metevarol/Implementing_OS_and_System_Calls_with_CPP/blob/109c5b0c5c9f6bf2cf07625b11703ff14202bae2/sample_runs/parta_1.png)
![Part A - 2](https://github.com/metevarol/Implementing_OS_and_System_Calls_with_CPP/blob/109c5b0c5c9f6bf2cf07625b11703ff14202bae2/sample_runs/parta_2.png)
![Part A - 3](https://github.com/metevarol/Implementing_OS_and_System_Calls_with_CPP/blob/109c5b0c5c9f6bf2cf07625b11703ff14202bae2/sample_runs/parta_3.png)


## Conclusion
The project successfully extends the Primitive Operating System with new features and improvements, providing a more robust and functional system for managing processes and hardware resources.

