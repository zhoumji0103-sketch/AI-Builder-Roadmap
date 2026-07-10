# Virtual Memory —— How Modern Operating Systems Manage Memory

## Background

Modern operating systems do not allow programs to access physical memory directly.

Instead, every program uses **virtual addresses**.

The CPU and the Memory Management Unit (MMU) cooperate to translate virtual addresses into physical addresses before accessing memory.

Virtual memory is one of the most important abstractions in modern operating systems.

---

## Why Virtual Memory?

Virtual memory solves several important problems.

### 1. Process Isolation

Each process has its own virtual address space.

```
Process A

0x00000000
...
0xffffffff
```

```
Process B

0x00000000
...
0xffffffff
```

Although both processes appear to use the same addresses, they are mapped to different physical memory pages.

---

### 2. Memory Protection

One process cannot directly access another process's memory.

The operating system controls page table permissions to prevent illegal access.

---

### 3. Demand Paging

Programs are usually much larger than the amount of memory they actually use.

Only the required pages are loaded into memory.

Remaining pages stay on disk until needed.

---

### 4. Memory Sharing

Shared libraries (such as libc) can be mapped into multiple processes simultaneously without duplicating physical memory.

---

## Address Translation

The CPU never directly accesses physical memory.

The simplified workflow is:

```
Program

↓

Virtual Address

↓

MMU

↓

Physical Address

↓

Cache

↓

Memory
```

The MMU performs address translation using the page table.

---

## Page Table

A virtual address is divided into:

```
+----------------------+------------+
| Virtual Page Number  | Offset     |
+----------------------+------------+
```

The Virtual Page Number indexes the page table.

The page table returns the corresponding physical page frame.

Finally, the offset locates the exact byte inside that page.

---

## Page Fault

If the required page is not currently in memory,

```
Present Bit = 0
```

the CPU raises a **Page Fault**.

The operating system then:

1. Loads the page from disk.
2. Finds a free page frame (or replaces an existing one).
3. Updates the page table.
4. Restarts the instruction.

---

## Summary

Virtual memory provides:

- Process isolation
- Memory protection
- Demand paging
- Memory sharing

Without virtual memory, modern multitasking operating systems would be almost impossible.