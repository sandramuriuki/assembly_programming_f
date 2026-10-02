# MUL Operation — 16-bit Multiplication

## EFLAGS Analysis - mul2

### Carry Flag (CF) — SET (1)

For a 16-bit `MUL`, the 32-bit result is stored in `DX:AX`.

CF is set when the upper 16 bits of the result are nonzero.

The result is:

```text
DX:AX = 0009 27C0h
```

Since:

```text
DX = 0009h
```

is nonzero, the product does not fit entirely within the lower 16 bits.

Therefore:

**CF = 1 (set)**

### Overflow Flag (OF) — SET (1)

For `MUL`, OF is set under the same condition as CF: when the upper half of the product is nonzero.

Since:

```text
DX = 0009h
```

is nonzero:

**OF = 1 (set)**

### Parity Flag (PF) — UNDEFINED

`MUL` does not define PF.

The number of `1` bits in the result therefore cannot be used to determine PF.

**PF = Undefined**

### Auxiliary Carry Flag (AF) — UNDEFINED

`MUL` does not define AF.

**AF = Undefined**

### Zero Flag (ZF) — UNDEFINED

The result is nonzero, but `MUL` does not define ZF.

Therefore:

**ZF = Undefined**

### Sign Flag (SF) — UNDEFINED

`MUL` does not define SF.

Therefore:

**SF = Undefined**

### Interrupt Flag (IF) — UNCHANGED (1)

`MUL` does not modify IF.

**IF = Unchanged**
                      

## Final Result


```text
CF = 1
OF = 1

PF = Undefined
AF = Undefined
ZF = Undefined
SF = Undefined
IF = Unchanged (1)
 [ CF IF OF ]
```
