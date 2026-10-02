# DIV Operation - 8-bit Divisor
## EFLAGS Analysis - div1

### Carry Flag (CF) — UNDEFINED

The `DIV` instruction does not define the Carry Flag.

Therefore, after the division, CF cannot reliably be classified as either set or cleared.

**CF = Undefined**

### Parity Flag (PF) — UNDEFINED

Unlike `ADD` and `SUB`, `DIV` does not define the Parity Flag.

Therefore, the value displayed by GDB cannot be used to determine whether the quotient has even or odd parity.

**PF = Undefined**

### Auxiliary Carry Flag (AF) — UNDEFINED (1)

The `DIV` instruction does not define AF, so it could either be 0 or 1. In this case it showed 1.

Therefore:

**AF = Undefined**

### Zero Flag (ZF) — UNDEFINED

The Zero Flag is not determined by whether the quotient is zero.

Although the quotient is `14`, `DIV` does not define ZF.

Therefore:

**ZF = Undefined**

### Sign Flag (SF) — UNDEFINED

`DIV` does not define the Sign Flag.

The fact that the quotient is positive does not mean SF is cleared.

Therefore:

**SF = Undefined**

### Overflow Flag (OF) — UNDEFINED

The Overflow Flag is also undefined after `DIV`.

The fact that the division produces a valid quotient does not mean OF is cleared.

Therefore:

**OF = Undefined**

### Interrupt Flag (IF) — UNCHANGED (1)

`DIV` does not modify the Interrupt Flag.

Therefore:

**IF = Unchanged**

## Final Result



```text
CF = Undefined
PF = Undefined
AF = Undefined (1)
ZF = Undefined
SF = Undefined
OF = Undefined
IF = Unchanged
[ AF IF ]
```