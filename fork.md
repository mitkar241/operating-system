# Fork
---

- [ ] [fork() in C - geeksforgeeks](https://www.geeksforgeeks.org/fork-system-call/)
- [x] [Explain concept of fork - geeksforgeeks](https://practice.geeksforgeeks.org/problems/explain-concept-of-fork)

## Definition
---
fork() is a system call in UNIX like operating system to create a copy of a process (parent process), which is called child process, which runs concurrently with the process that makes the fork() call (parent process). After a new child process is created, both processes will execute the next instruction following the fork() system call. A child process uses the same pc(program counter), same CPU registers, same open files which use in the parent process.

## Return Value
---
System call fork() is used to create processes. It takes no arguments and returns an integer value as a process ID. Below are different values returned by fork().

- `Negative Value`: creation of a child process was unsuccessful.
- `Zero`: Returned to the newly created child process.
- `Positive value`: Returned to parent or caller. The value contains process ID of newly created child process.

## Identify Parent Process
---
To distinguish parent from child follow steps:-

- If fork() call returns negative value.creation of child process was unsucessful
- If return 0 means child process is created.
- If it is positive then process_id is given to parent can be fetched used get_process_id

`N.B.` child process can be distinguished from parent process using PID and PPID.

## Consequence
---
fork() is implemented using copy-on-write pages, so the only penalty that it incurs is the time and memory required to duplicate the parent’s page tables, and to create a unique task structure for the child.

## Use Case
---
- Google chrome uses fork() to handle each page in process.
- Apache uses to handle multiple servers
- Scripting languages use fork indirectly to start child processes

## Calculation
---
If fork() is executed successfully then it makes two copy of fork() one for child and one for parent. So If fork() is called n times, total process created are 2^n. So Child count = (2^n - 1)
