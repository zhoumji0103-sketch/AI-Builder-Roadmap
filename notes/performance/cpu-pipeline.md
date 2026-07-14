# CPU Pipeline

## Modern CPU Front-End

The front-end is responsible for fetching and decoding instructions.

```
Branch Predictor
        ↓
Instruction Cache
        ↓
Decode
        ↓
Micro-Operations
```

The branch predictor attempts to predict future execution paths.

Instructions are fetched from the instruction cache rather than memory whenever possible.

Complex instructions may be decoded into multiple micro-operations.

---

## Modern CPU Back-End

The back-end executes instructions using multiple execution units.

```
Issue Queue
      ↓
ALU
Load
Store
Branch
Vector
Floating Point
```

Instructions may execute out of order.

However, results are committed in program order.

---

## Branch Prediction

Branches interrupt the pipeline.

To avoid stalls, CPUs predict branch outcomes.

Correct predictions improve performance.

Incorrect predictions require flushing the pipeline and restarting execution.

---

## Out-of-Order Execution

Independent instructions may execute simultaneously.

Execution order differs from program order.

Final results are committed in order, preserving correctness.

---

# Summary

Modern processors improve performance through

- Pipeline
- Branch Prediction
- Out-of-Order Execution
- Multiple Execution Units