# Storage Devices

## Volatile Memory

Volatile memory loses data when power is removed.

Examples:

- SRAM
- DRAM

### SRAM

- Used for CPU Cache
- Very fast
- Does not require refresh
- Expensive

### DRAM

- Used for Main Memory
- High density
- Requires periodic refresh
- Slower than SRAM

---

## Non-Volatile Memory

Non-volatile memory preserves data without power.

Examples:

- Flash Memory
- SSD
- EEPROM

---

## Flash Memory

Flash memory is organized into

```
Block
    ↓
Page
```

Pages can be read individually.

However, updating existing data requires erasing an entire block before rewriting.

---

## Flash Translation Layer (FTL)

Modern SSDs use the Flash Translation Layer (FTL).

The FTL manages:

- Wear leveling
- Garbage collection
- Logical-to-physical address mapping

Applications are unaware of these internal operations.

---

## Bus Arbitration

Multiple devices may request access to the bus simultaneously.

Traditional shared buses require bus arbitration.

Modern systems reduce contention using:

- Point-to-point links
- PCIe
- Ring Bus
- Mesh Network
- High-speed interconnects

---

## Summary

Storage devices are optimized for different goals.

Caches optimize speed.

DRAM optimizes capacity.

SSDs optimize persistence and cost.