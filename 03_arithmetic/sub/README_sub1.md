# SUB Operation — 8-bit Subtraction

## EFLAGS Analysis - sub1

### Carry Flag (CF) — SET (1)

For subtraction, CF indicates that a **borrow** was required.

The unsigned values are:

```text
50 - 80
```

Since `50` is smaller than `80`, the subtraction requires a borrow.

Therefore:

**CF = 1 (set)**

### Parity Flag (PF) — SET (1)

The result is:

```text
11100010
```

It contains four `1` bits:

```text
11100010
^^^  ^
4 ones
```

Four is even.

Therefore:

**PF = 1 (set)**

### Auxiliary Carry Flag (AF) — CLEARED (0)

AF is set when a borrow occurs from bit 4 during subtraction.

Looking at the lower nibbles:

```text
0010 - 0000
```

there is no borrow within the lower nibble itself.

Therefore:

**AF = 0 (cleared)**

### Zero Flag (ZF) — CLEARED (0)

The result is:

```text
11100010
```

which is not zero.

Therefore:

**ZF = 0 (cleared)**

### Sign Flag (SF) — SET (1)

The most significant bit of the 8-bit result is `1`:

```text
11100010
^
MSB
```

Therefore:

**SF = 1 (set)**

### Overflow Flag (OF) — CLEARED (0)

Signed overflow occurs in subtraction when the operands have different signs and the result cannot be represented in the signed range.

Here:

```text
50 - 80 = -30
```

The signed 8-bit range is:

```text
-128 to +127
```

`-30` is within this range.

Therefore, no signed overflow occurs:

**OF = 0 (cleared)**

### Interrupt Flag (IF) — UNCHANGED (1)

`SUB` does not modify IF.

**IF = Unchanged**

                 

## Final Result

```text
CF = 1
PF = 1
AF = 0
ZF = 0
SF = 1
OF = 0
IF = Unchanged (1)
 [ CF PF SF IF ]
```
