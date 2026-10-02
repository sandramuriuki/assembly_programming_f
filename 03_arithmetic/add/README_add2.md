# ADD Operation
# EFLAGS Analysis - add2


## 1. Carry Flag (CF) — CLEARED (0)

The Carry Flag is set when an addition produces a carry beyond the most significant bit of the destination operand.

Here, the operation is a 16-bit addition:

```text
  0111110100000000
+ 0000000111110100
------------------
  0111111011110100
```

There is no carry beyond the 16th bit.

The result `32500` is also within the unsigned 16-bit range of `0–65535`.

Therefore:

**CF = 0 (cleared)**

---

## 2. Parity Flag (PF) — CLEARED (0)

The Parity Flag is determined by the number of `1` bits in the **least significant byte** of the result.

The complete 16-bit result is:

```text
01111110 11110100
```

The least significant byte is:

```text
11110100
```

It contains five `1` bits:

```text
11110100
^^^^^
5 ones
```

Five is an odd number.

Therefore:

**PF = 0 (cleared)**


---

## 3. Auxiliary Carry Flag (AF) — CLEARED (0)

The Auxiliary Carry Flag is set when there is a carry from bit 3 to bit 4 of the result, meaning there is a carry between the lower and upper nibbles.

Look at the lowest 4 bits:

```text
0000 + 0100 = 0100
```

There is no carry from bit 3 to bit 4.

Therefore:

**AF = 0 (cleared)**

---

## 4. Zero Flag (ZF) — CLEARED (0)

The Zero Flag is set when the result of the arithmetic operation is zero.

The result is:

```text
32500
```

which is not zero.

Therefore:

**ZF = 0 (cleared)**

---

## 5. Sign Flag (SF) — CLEARED (0)

The Sign Flag reflects the most significant bit of the result.

The 16-bit result is:

```text
0111111011110100
^
MSB
```

The most significant bit is `0`.

Therefore:

**SF = 0 (cleared)**

The result is also positive when interpreted as a signed 16-bit integer.

---

## 6. Overflow Flag (OF) — CLEARED (0)

The Overflow Flag indicates signed overflow.

For a 16-bit signed integer, the range is:

```text
-32768 to +32767
```

The operands are:

```text
32000
+ 500
------
32500
```

The result `32500` is less than the maximum signed 16-bit value of `32767`.

Therefore, the result can be represented correctly as a signed 16-bit number.

Both operands are positive and the result is also positive.

Therefore:

**OF = 0 (cleared)**

---

# 7. Interrupt Flag (IF) — UNCHANGED (1)

The Interrupt Flag controls whether the processor recognizes maskable hardware interrupts.

The `ADD` instruction does **not** modify IF.



---
## Final Result

```text
CF = 0
PF = 0
AF = 0
ZF = 0
SF = 0
OF = 0
IF = Unchanged (1)
[ IF ]
```


