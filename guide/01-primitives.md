# Primitives

Primitives are the basic values in Rumi. They consist of signed and unsigned integers of various sizes (`int`, `s8`, `s16`, `s32`, `s64`, `u8`, `u16`, `u32`, `u64`), booleans (`bool`), strings (`string`) and floating points (`f32`, `f64`). Strings are implemented as pointers to characters (`*u8` in rumi and `char*` in C). When used directly, primitives are allocated on the stack.
