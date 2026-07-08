# CPU Cache —— Why Modern CPUs Need Cache?

## Background

Modern CPUs execute instructions much faster than main memory (RAM) can provide data.

If every memory access had to wait for RAM, the CPU would spend a significant amount of time idle.

To reduce memory latency, modern processors introduce one or more levels of **CPU Cache**, which are much smaller but significantly faster than RAM.

The goal of cache is **not to increase computing power**, but to reduce the waiting time for memory accesses.

---

## CPU Cache vs Memory

| CPU Cache | Main Memory (RAM) |
|-----------|-------------------|
| Very fast | Much slower |
| Small capacity | Large capacity |
| Located on the CPU chip | Located outside the CPU |
| Frequently accessed data | All program data |

The CPU always attempts to read data from the cache first.

If the data is not present in the cache, it must be fetched from memory.

---

## Why Cache Is Needed

A simplified access path is shown below.

```
CPU
 │
 ▼
L1 Cache
 │
 ▼
L2 Cache
 │
 ▼
L3 Cache
 │
 ▼
Memory
```

The farther the data is from the CPU, the longer the access latency.

Therefore, reducing memory accesses greatly improves CPU performance.

---

## Direct-Mapped Cache

One simple cache organization is **Direct Mapping**.

Each memory block can only be stored in one specific cache line.

```
Memory Blocks

0
4
8
12
 │
 ▼
Cache Line 0

1
5
9
13
 │
 ▼
Cache Line 1

2
6
10
14
 │
 ▼
Cache Line 2
```

Since memory is much larger than cache, **multiple memory blocks map to the same cache line**.

When different memory blocks compete for the same cache line, cache replacement occurs.

---

## Address Structure

A memory address is divided into three parts.

```
+-----------+---------+---------+
|    Tag    |  Index  | Offset  |
+-----------+---------+---------+
```

### Offset

Determines which byte inside the cache line is accessed.

### Index

Determines which cache line should be checked.

### Tag

Identifies which memory block is currently stored in that cache line.

---

## Valid Bit

Each cache line contains a **Valid Bit**.

```
Valid = 0

↓

Cache line is empty.

↓

Cache Miss
```

```
Valid = 1

↓

Compare Tag

↓

Tag matches

↓

Cache Hit
```

A cache hit requires **both**:

- Valid Bit = 1
- Tag matches

---

## Cache Read

When the CPU reads data:

```
CPU

↓

Check Cache

↓

Hit ?

├── Yes
│
└── Read directly

↓

No

↓

Read from Memory

↓

Replace Cache Line

↓

Return Data
```

A cache miss requires fetching data from memory before execution can continue.

---

## Cache Write Policies

Writing data introduces another challenge.

The CPU must keep both **Cache** and **Memory** consistent.

### Write Through

The CPU writes data to:

- Cache
- Memory

at the same time.

```
CPU

↓

Cache

↓

Write Buffer

↓

Memory
```

A **Write Buffer** allows the CPU to continue executing while memory is updated in the background.

However, if the write buffer becomes full, the CPU must wait.

---

### Write Back

Another strategy is **Write Back**.

The CPU only updates the cache.

A **Dirty Bit** is set to indicate that memory is outdated.

```
Dirty = 1

↓

Cache has newer data.

↓

Memory will be updated later.
```

The modified cache line is written back to memory **only when it is replaced (evicted)**.

Compared with Write Through, Write Back usually provides higher performance.

---

## Memory Transfer

Memory is divided into many **cache blocks (cache lines)**.

When a cache miss occurs, the CPU does not fetch only one byte.

Instead, it loads an entire cache line (for example, 64 Bytes).

```
Memory

□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□

↓

Load one Cache Line

↓

CPU Cache
```

This improves performance because programs often access nearby memory locations.

This characteristic is called **Spatial Locality**.

---

## Summary

CPU Cache improves performance by reducing memory access latency.

Key concepts include:

- Cache Line
- Direct Mapping
- Tag
- Index
- Offset
- Valid Bit
- Dirty Bit
- Write Through
- Write Back
- Spatial Locality

Understanding cache behavior is one of the foundations of computer architecture and performance optimization.

---

# Reflection

Before learning CPU Cache, I simply knew that cache is faster than memory.

Now I understand:

- Why CPUs need cache.
- How memory is mapped into cache.
- How cache determines Hit and Miss.
- Why Write Through and Write Back exist.
- Why modern CPUs transfer an entire cache line instead of a single byte.

This is my first step toward understanding how modern processors are designed.