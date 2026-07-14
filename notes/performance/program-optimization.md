# Program Optimization

## Overview

Program performance depends on the entire computing stack rather than a single component.

Typical optimization opportunities include:

- Better algorithms
- Compiler optimization
- Instruction Set Architecture (ISA)
- CPU microarchitecture
- Memory hierarchy
- Operating system

---

# Common Optimization Techniques

## 1. Loop Invariant Code Motion

Move calculations that never change outside the loop.

Example:

```cpp
int len = strlen(s);

for (...)
{
    ...
}
```

---

## 2. Reduce Memory Access

Accessing registers is much faster than repeatedly accessing memory.

Keeping frequently used values in local variables helps the compiler allocate registers.

---

## 3. Strength Reduction

Replace expensive arithmetic with cheaper operations.

Examples:

- multiplication → shift
- division → shift
- repeated multiplication → incremental addition

---

## 4. Eliminate Dependency

Independent computations allow multiple execution units to work simultaneously.

Instead of

sum += a[i];

Use multiple accumulators.

---

## 5. Loop Unrolling

Process multiple iterations in one loop body.

Benefits:

- fewer branch instructions
- better instruction-level parallelism
- higher throughput

---

## 6. Data Locality

Arrange memory accesses to improve cache hit rate.

Good cache locality often provides larger speedups than micro-optimizations.

---

## 7. SIMD

Modern CPUs provide vector instructions that process multiple data elements with one instruction.

Widely used in AI, graphics and scientific computing.

---

# Summary

High-performance software is achieved through collaboration between algorithms, compilers, CPU architecture and memory systems.