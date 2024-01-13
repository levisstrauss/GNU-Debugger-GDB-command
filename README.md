### GNU Debugger (GDB) Commands
     These are some of the most common GDB commands you will use:
```bash
  sudo apt-get install gdb
```
```bash
  gcc -g myprogram.c -o myprogram
```
```bash
  - Starting GDB with the myprogram:
  gdb ./myprogram
```
```bash
  - Run the program:
   (gdb) run
```
```bash
  - To run your program with arguments
   (gdb) run arg1 arg2
```
```bash
  - To set a breakpoint at the beginning of the main function:
   (gdb) break main
```

```bash
  - To set a breakpoint at line 20 in myfile.c:
   (gdb) break myfile.c:20 or break 20
```
```bash
  - To resume program execution after a breakpoint or pause:
   (gdb) continue
```
```bash
  - To execute the next line of code, stepping over function calls:
   (gdb) next
```
```bash
  - To execute the next line of code, stepping into function calls:
   (gdb) step
```
```bash
  - To list the source code around the current line:
   (gdb) list
```
```bash
  - To list lines 1 to 10 of the current file:
   (gdb) list 1,10
```

```bash
  - To print the value of a variable x:
   (gdb) print x
```
```bash
  - To print the 4th element of an array a:
   (gdb) print a[3]
```
```bash
  - To show the call stack:
   (gdb) backtrace
```
```bash
  - To show local variables:
   (gdb) info locals
```
```bash
  - To show all breakpoints:
   (gdb) info breakpoints
```
```bash
  - To set a watchpoint on a variable x:
   (gdb) watch x
```
```bash
  - To select the third frame in the stack:
    (gdb) frame 3
```
```bash
  - To exit GDB:
    (gdb) quit
```

```bash
  - To disable breakpoint 1:
    (gdb) disable 1
```
```bash
  - To enable breakpoint 1:
    (gdb) enable 1
```
```bash
  - To assign the value 10 to a variable x:
    (gdb) set var x=10
```
```bash
  - To remove the breakpoint at line 20 in myfile.c:
    gdb) clear myfile.c:20
```

```bash
- On Linix, GDB is the standard debugger for C/C++ programs.
- sudo apt-get install gdb
- gcc man.c -o main.out   # Compile the program with debugging symbols
- ./main.out             # Run the program
```
### Another alternative way with the flag -g

```bash
- gcc -o main.c main main.c -g  // Create a debug information file
- wc -c main.c                  // Check the size of the file
- lay next                      // This will show the source code and the assembly code 
- break main                    // Set a breakpoint at the beginning of the main function
- break 15                      // Set a breakpoint at line 15
- run                           // Run the program

// So now, we can step line by line through the program with the next command
// With these commands: in c and in assembly codes
- next             // Step to the next line
- nexti            // Step to the next instruction
- step             // Step into the next line, but step into any function calls
- stepi            // Step into the next instruction, but step into any function calls
- ref              // Refresh the screen
- continue         // Continue running the program until the next breakpoint
- finish           // Continue running the program until the current function is finished
- print <variable> // Print the value of a variable
- info registers   // Print the values of all registers
- quit             // Quit GDB
```
### Using Core files and GDB to debug crashes in our code
     - The core is an elf that contain the full state of the program when it crashed.

```bash
- gcc -o inventory info.c -g // Compile the program with debugging symbols
- ulimit -c unlimited // This will allow the creation of unlimited core files
- cat /proc/sys/kernel/core_pattern // This will show the name of the core file 
- ls to see the core file at that location
- sudo su   // Change to root

// This will create a new core file if none exists
- echo "./new_core" > /proc/sys/kernel/core_pattern // Change the name of the core file
- echo "/tmp/core.%e.%p.%h.%t" > /proc/sys/kernel/core_pattern // Change the name of the core file
- exit // Exit from root

// To run the gdb with the core file
- gdb ./main ./core       // This will run the gdb with the core file
- x/i $pc                 // This will show the instruction pointer
- info registers          // This will show the registers
```

### Reverse Engineering
     - Reverse engineering is the process of taking a compiled binary and trying to understand how it works.
     - The most common tools for reverse engineering are:
```bash
- xxd name | less // This will show the hexdump of the file
- strings name-of-binary-files | less // This will show all the strings of the file
- objdump -d -Mintel name-of-binary-files | less // This will show the assembly code of the file  disassembler
- ./text
- cd downloads/ // Go to the downloads folder
- ./idafree82_linux.run // Run the ida free
- cd ~/idafree-8.2 // Will be created in the home directory
- ls
- ./ida64 // Run the ida64
- import the binary file as elf 64 bits ok
```
### NB: 
    - We have a code and we don't know what that code is doing
    - We take that code and we transform it into binary code
    - We put that binary code into an objump
    - We then put the objdump into ida64 and use that to extract the functionality of the code
    - It is very important to understand the assembly code

