# SIMD

SIMD stands for

Single Instruction Multiple Data.

Instead of processing one value at a time,

modern CPUs process multiple values using vector registers.

Example

```
A1 A2 A3 A4

+

B1 B2 B3 B4

↓

C1 C2 C3 C4
```

One instruction performs four additions simultaneously.

Modern instruction sets include

- SSE
- AVX
- AVX2
- AVX-512
- ARM NEON

SIMD is widely used in

- AI inference
- Image processing
- Audio processing
- Scientific computing