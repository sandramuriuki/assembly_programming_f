# SUB Operation — 16-bit Subtraction

## EFLAGS Analysis - sub2

### Carry Flag (CF) — SET (1)

For subtraction, CF indicates whether an unsigned borrow was required.

Here:

```text
1000 - 2000
```

Since `1000 < 2000`, the subtraction requires a borrow.

Therefore:

**CF = 1 (set)**

### Parity Flag (PF) — SET (1)

PF is determined by the least significant byte of the result.

The result is:

```text
11111100 00011000
```

The low byte is:

```text
00011000
```

It contains two `1` bits.

Two is even, therefore:

**PF = 1 (set)**

### Auxiliary Carry Flag (AF) — CLEARED (0)

AF is set when a borrow occurs from bit 4 during subtraction.

Looking at the lower bits:

```text
1000 - 0000 = 1000
```

There is no borrow from bit 4.

Therefore:

**AF = 0 (cleared)**

### Zero Flag (ZF) — CLEARED (0)

The result is:

```text
-1000
```

which is not zero.

Therefore:

**ZF = 0 (cleared)**

### Sign Flag (SF) — SET (1)

The most significant bit of the 16-bit result is `1`:

```text
1111110000011000
^
MSB
```

Therefore:

**SF = 1 (set)**

### Overflow Flag (OF) — CLEARED (0)

The signed 16-bit range is:

```text
-32768 to +32767
```

The result is:

```text
1000 - 2000 = -1000
```

`-1000` is within the signed 16-bit range.

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
IF = Unchanged
 [ CF PF SF IF ]
```
