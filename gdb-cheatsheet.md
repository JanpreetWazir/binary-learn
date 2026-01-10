# 🐞 GDB Cheat Sheet (Practical & Usage-Sorted)

A complete, workflow-oriented reference for **GNU Debugger (gdb)**.  
Useful for **C/C++ debugging, reverse engineering, and exploit development**.

---

## 📌 1. Starting GDB

```bash
gdb ./binary                  # Load binary
gdb ./binary core             # Load with core dump
gdb ./binary -p <pid>         # Attach to running process
gdb -tui ./binary             # Text User Interface mode
```

**Compile with debug symbols:**

```bash
gcc -g program.c -o program
gcc -g -O0 program.c -o program  # Disable optimization for easier debugging
```

---

## ▶️ 2. Program Execution Control

| Command | Description |
|---------|-------------|
| `run` / `r` | Start program |
| `run arg1 arg2` | Run with arguments |
| `start` | Stop at main() |
| `continue` / `c` | Resume execution |
| `next` / `n` | Next line (skip functions) |
| `step` / `s` | Step into function |
| `finish` | Run until function returns |
| `until` | Run until next line |
| `until <line>` | Run until specific line |
| `kill` | Stop program |
| `quit` / `q` | Exit gdb |

---

## 🧱 3. Breakpoints

**Setting breakpoints:**

```gdb
break main                    # Break at function
break function_name           # Break at specific function
break file.c:25               # Break at line number
break *0x401234               # Break at address
break main if x == 10         # Conditional breakpoint
tbreak main                   # Temporary breakpoint (removed after hit)
```

**Managing breakpoints:**

```gdb
info breakpoints              # List all breakpoints
info break                    # Short form
delete 1                      # Delete breakpoint #1
delete                        # Delete all breakpoints
disable 1                     # Disable breakpoint #1
enable 1                      # Enable breakpoint #1
clear                         # Clear all breakpoints
clear function_name           # Clear breakpoint at function
```

---

## 👁️ 4. Variables & Memory

**Print variables:**

```gdb
print x                       # Print variable x
print *ptr                    # Dereference pointer
print arr[2]                  # Array element
print/x var                   # Print in hexadecimal
print/t var                   # Print in binary
print/d var                   # Print in decimal
```

**Expressions:**

```gdb
print x+5                     # Evaluate expression
print strlen(buf)             # Call function
print sizeof(struct_name)     # Get size
set var x = 10                # Modify variable
```

**Examine memory:**

```gdb
x/4x 0x601050                 # 4 hex words at address
x/10i $rip                    # 10 instructions at RIP
x/s buffer                    # String at buffer
x/16bx buffer                 # 16 bytes in hex
```

**Format specification:**

```
x/<count><format><size> <address>
```

**Format letters:**
- `x` = hex
- `d` = decimal
- `u` = unsigned
- `o` = octal
- `t` = binary
- `a` = address
- `c` = char
- `f` = float
- `s` = string
- `i` = instruction

**Size letters:**
- `b` = byte (8 bits)
- `h` = halfword (16 bits)
- `w` = word (32 bits)
- `g` = giant (64 bits)

---

## 📚 5. Stack & Backtrace

```gdb
backtrace                     # Show call stack
bt                            # Short form
bt full                       # Include local variables
bt 10                         # Show only 10 frames
frame 2                       # Switch to frame #2
info frame                    # Current frame info
info args                     # Function arguments
info locals                   # Local variables
up                            # Move up one frame
down                          # Move down one frame
```

---

## 🧠 6. Registers & CPU State

```gdb
info registers                # All registers
info registers rip rsp rbp    # Specific registers
print $rax                    # Print register value
print/x $rax                  # Print in hex
set $rax = 0                  # Modify register
set $pc = 0x401000            # Change program counter
```

**Common registers:**
- **x86-64**: `rax`, `rbx`, `rcx`, `rdx`, `rsi`, `rdi`, `rbp`, `rsp`, `rip`
- **x86**: `eax`, `ebx`, `ecx`, `edx`, `esi`, `edi`, `ebp`, `esp`, `eip`
- **ARM**: `r0-r15`, `pc`, `sp`, `lr`

---

## 🧵 7. Threads & Forks

**Thread management:**

```gdb
info threads                  # List all threads
thread 2                      # Switch to thread #2
thread apply all bt           # Backtrace for all threads
thread apply all command      # Run command on all threads
```

**Fork handling:**

```gdb
set follow-fork-mode child    # Follow child process
set follow-fork-mode parent   # Follow parent (default)
set detach-on-fork off        # Debug both parent and child
info inferiors                # List processes
inferior 2                    # Switch to process #2
```

---

## 📂 8. Source, Symbols & Files

**Source code:**

```gdb
list                          # Show source around current line
list main                     # Show source for function
list 20,40                    # Show lines 20-40
list file.c:25                # Show specific file location
set listsize 20               # Set number of lines to display
```

**Symbol information:**

```gdb
info functions                # List all functions
info variables                # List all variables
info types                    # List all types
info sources                  # List source files
info files                    # Show file/section info
whatis variable               # Show type
ptype variable                # Show detailed type
```

**Loading symbols:**

```gdb
symbol-file binary            # Load symbol file
add-symbol-file lib.so 0xaddr # Add shared library symbols
```

---

## ⚠️ 9. Signals & Crashes

```gdb
info signals                  # List signal handling
info handle                   # Same as above
handle SIGSEGV stop           # Stop on segfault
handle SIGSEGV nostop         # Don't stop on segfault
handle SIGSEGV noprint        # Don't print message
handle all print              # Print all signals
```

**Analyzing core dumps:**

```bash
gdb ./binary core             # Load core dump
```

```gdb
bt                            # Show where it crashed
info registers                # Check register state
info threads                  # Check thread state
```

---

## 🔁 10. Watchpoints

**Set watchpoints:**

```gdb
watch x                       # Break when x is written
watch *ptr                    # Break when memory at ptr changes
watch x if x > 10             # Conditional watchpoint
rwatch x                      # Break when x is read
awatch x                      # Break when x is read or written
```

**Manage watchpoints:**

```gdb
info watchpoints              # List watchpoints
delete <num>                  # Delete watchpoint
disable <num>                 # Disable watchpoint
enable <num>                  # Enable watchpoint
```

---

## 🔐 11. Reverse Engineering / Exploit Dev

**Disassembly:**

```gdb
disassemble main              # Disassemble function
disassemble /r main           # Include raw bytes
disassemble /m main           # Include source lines
disassemble 0x401000,0x401100 # Disassemble address range
set disassembly-flavor intel  # Use Intel syntax
set disassembly-flavor att    # Use AT&T syntax
```

**Memory mapping:**

```gdb
info proc mappings            # Show memory map
info files                    # Show loaded files/sections
info sharedlibrary            # Show loaded libraries
```

**Search memory:**

```gdb
find 0x400000, 0x500000, "/bin/sh"          # Find string
find /b 0x400000, +0x100000, 0x41, 0x42     # Find bytes
```

**Security settings:**

```gdb
set disable-randomization on  # Disable ASLR (default)
set disable-randomization off # Enable ASLR
show disable-randomization    # Check current setting
```

**Pattern generation (for buffer overflows):**

```gdb
pattern create 200            # Requires pwndbg/gef
pattern offset 0x61616169     # Find offset
```

---

## 🧪 12. Quality of Life

**Hooks (auto-execute commands):**

```gdb
define hook-stop
    bt
    info registers
    x/10i $rip
end
```

**Display values automatically:**

```gdb
display x                     # Show x after each stop
display/x $rax                # Show rax in hex
info display                  # List auto-display
delete display 1              # Remove auto-display
```

**Command aliases:**

```gdb
alias ll = list
alias bp = break
```

**History:**

```bash
~/.gdb_history                # Command history file
```

**Configuration file:**

```bash
~/.gdbinit                    # Auto-loaded on startup
```

**Example .gdbinit:**

```gdb
set disassembly-flavor intel
set pagination off
set history save on
set history filename ~/.gdb_history
set history size 10000
```

---

## 🧩 13. GDB Extensions

| Tool | Purpose | URL |
|------|---------|-----|
| **pwndbg** | Exploit development | https://github.com/pwndbg/pwndbg |
| **gef** | Reverse engineering | https://github.com/hugsy/gef |
| **peda** | Python Exploit Dev Assistance | https://github.com/longld/peda |

**Install pwndbg:**

```bash
git clone https://github.com/pwndbg/pwndbg
cd pwndbg
./setup.sh
```

**Install GEF:**

```bash
bash -c "$(curl -fsSL https://gef.blah.cat/sh)"
```

**Install PEDA:**

```bash
git clone https://github.com/longld/peda.git ~/peda
echo "source ~/peda/peda.py" >> ~/.gdbinit
```

---

## 📌 14. Minimal Daily Workflow

```gdb
gdb ./a.out                   # Start gdb
break main                    # Set breakpoint
run                           # Start program
next                          # Step over
step                          # Step into
print x                       # Inspect variable
bt                            # View call stack
continue                      # Resume execution
quit                          # Exit
```

---

## 🎯 15. Quick Reference Card

**Essential commands for everyday use:**

```gdb
# Starting
gdb ./program                 # Load program
r                             # Run
start                         # Run and stop at main

# Breakpoints
b main                        # Break at main
b *0x401234                   # Break at address
info b                        # List breakpoints

# Execution
n                             # Next line
s                             # Step into
c                             # Continue
finish                        # Return from function

# Inspection
p variable                    # Print variable
x/10x $rsp                    # Examine stack
bt                            # Backtrace
info registers                # Show registers

# Memory
x/s 0x601050                  # String at address
x/10i $rip                    # Instructions at RIP
watch variable                # Watch for changes

# Exit
q                             # Quit
```

---

## 📖 Additional Resources

- **Official Documentation**: https://sourceware.org/gdb/documentation/
- **GDB Tutorial**: https://www.gnu.org/software/gdb/documentation/
- **Debugging with GDB** (Book): https://sourceware.org/gdb/current/onlinedocs/gdb/

---

**💡 Pro Tip**: Use GDB with extensions like pwndbg or GEF for enhanced exploit development and reverse engineering capabilities!
