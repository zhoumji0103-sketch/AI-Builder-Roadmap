# Memory Hierarchy

## Why Memory Hierarchy Exists

Modern computers organize storage into multiple layers instead of using a single large memory.

Each level makes a trade-off between:

- Capacity
- Latency
- Cost

The closer storage is to the CPU, the faster and more expensive it becomes.

```
Registers
    ↓
L1 Cache
    ↓
L2 Cache
    ↓
L3 Cache
    ↓
DRAM
    ↓
SSD
    ↓
Network Storage
```

---

## Memory Access Flow

When a program accesses data, the CPU searches through the hierarchy.

```
CPU
    ↓
L1 Cache
    ↓
L2 Cache
    ↓
L3 Cache
    ↓
DRAM
```

If the required page is not in DRAM,

```
Page Fault
      ↓
Operating System
      ↓
SSD
      ↓
DRAM
```

After the page is loaded, the instruction is executed again.

---

## Locality

Modern memory hierarchies rely on locality.

### Temporal Locality

Recently accessed data is likely to be accessed again.

### Spatial Locality

Nearby memory locations are likely to be accessed soon.

These two principles are the foundation of cache design.

---

## Summary

The memory hierarchy improves performance by storing frequently used data closer to the CPU while keeping storage costs reasonable.