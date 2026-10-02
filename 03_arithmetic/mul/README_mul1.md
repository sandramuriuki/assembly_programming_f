# MUL Operation — 8-bit Multiplication

## EFLAGS Analysis - mul1

### Carry Flag (CF) — CLEARED (0)

For an 8-bit `MUL`, the result is stored in the 16-bit `AX` register.

CF and OF are cleared when the upper half of the result is zero.

The result is:

```text
AX = 00000000 11111010
```

The upper 8 bits are all zero.

Therefore, the complete product fits within 8 bits.

**CF = 0 (cleared)**

### Overflow Flag (OF) — CLEARED (0)

OF has the same condition as CF for `MUL`.

The upper half of the result is zero:

```text
00000000 11111010
^^^^^^^^
upper half = 0
```

Therefore:

**OF = 0 (cleared)**

### Parity Flag (PF) — UNDEFINED

`MUL` does not define PF.

Even though the low byte `11111010` contains an even number of `1` bits, this does **not** allow us to conclude that PF is set.

**PF = Undefined**

### Auxiliary Carry Flag (AF) — UNDEFINED

`MUL` does not define AF.

**AF = Undefined**

### Zero Flag (ZF) — UNDEFINED

The result is `250`, not zero, but `MUL` does not define ZF.

Therefore, ZF cannot be inferred from the fact that the result is nonzero.

**ZF = Undefined**

### Sign Flag (SF) — UNDEFINED

`MUL` does not define SF.

The fact that the result's most significant bit is `0` does not mean SF is guaranteed to be cleared.

**SF = Undefined**

### Interrupt Flag (IF) — UNCHANGED (1)

`MUL` does not modify IF.

**IF = Unchanged**

## Final Result

```text
CF = 0
PF = Undefined
AF = Undefined
ZF = Undefined
SF = Undefined
OF = 0
IF = Unchanged (1)
 [ IF ]
```

