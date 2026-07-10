# TLB —— Speeding Up Address Translation

## Background

Every memory access requires virtual-to-physical address translation.

If the CPU had to access the page table for every load or store instruction, memory accesses would become much slower.

To solve this problem, modern processors introduce the **Translation Lookaside Buffer (TLB)**.

---

## What is a TLB?

The TLB is a small, high-speed cache that stores recently used page table entries.

It caches **address translations**, not program data.

```
CPU

↓

TLB

↓

Hit ?

├── Yes
│
└── Physical Address

↓

No

↓

Page Table

↓

Update TLB
```

---

## TLB Hit

If the required mapping already exists inside the TLB,

the CPU immediately obtains the physical address.

No page table lookup is required.

---

## TLB Miss

If the mapping is not found,

the CPU performs a page table walk.

If the page exists in memory,

the translation is inserted into the TLB.

---

## Page Fault

If the page table indicates the page is not present,

the operating system handles a page fault.

```
TLB Miss

↓

Page Table

↓

Present ?

├── Yes
│
└── Update TLB

↓

No

↓

Page Fault

↓

Disk

↓

Memory

↓

Update Page Table

↓

Update TLB
```

---

## Why Not Cache the Entire Page Table?

The page table is extremely large.

Caching the entire page table would be expensive and inefficient.

Instead, the TLB stores only the most frequently used address translations.

This significantly reduces translation latency.

---

## Summary

The TLB improves CPU performance by caching virtual-to-physical address mappings.

It should be viewed as a **cache for the page table**, rather than a cache for memory data.