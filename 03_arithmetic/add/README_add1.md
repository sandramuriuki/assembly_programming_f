# ADD Operation 

## EFLAGS Analysis - add1

### 1. Carry Flag (CF) — CLEARED (0)

The Carry Flag indicates whether an unsigned addition produces a carry out of the most significant bit.

There is no carry beyond the 8th bit. The result fits within the range of an 8-bit unsigned value (`0–255`).

Therefore:

**CF = 0 (cleared)**

---

### 2. Zero Flag (ZF) — CLEARED (0)

The Zero Flag is set when the result of an arithmetic operation is zero.

The result is:

```text
10000010
```

This is `130`, not zero.

Therefore:

**ZF = 0 (cleared)**

---

### 3. Sign Flag (SF) — SET (1)

The Sign Flag reflects the most significant bit of the result.

The result is:

```text
10000010
^
MSB
```

The most significant bit is `1`, so the Sign Flag is set.

Therefore:

**SF = 1 (set)**


---

### 4. Overflow Flag (OF) — SET (1)

The Overflow Flag indicates that the result of a **signed** arithmetic operation cannot be represented using the available number of bits.

For an 8-bit signed value, the valid range is:

```text
-128 to +127
```

The operands are:

```text
120 = 01111000
10  = 00001010
```

Both operands are positive because their most significant bits are `0`.

However, their mathematical sum is:

```text
120 + 10 = 130
```

`130` cannot be represented as a positive signed 8-bit integer because the maximum positive value is `127`.

The 8-bit result is:

```text
10000010
```

Its most significant bit is `1`, which makes it appear negative when interpreted as a signed 8-bit value.

Therefore, a signed overflow occurred:

**OF = 1 (set)**

---

### 5. Parity Flag (PF) — SET (1)

The Parity Flag is set when the least significant byte of the result contains an **even number of 1 bits**.

The result is:

```text
10000010
```

It contains two `1` bits:

```text
1 000001 0
^       ^
1       1
```

There are **2 ones**, which is an even number.

Therefore:

**PF = 1 (set)**

---

### 6. Auxiliary Carry Flag (AF) — SET (1)

The Auxiliary Carry Flag is set when there is a carry from bit 3 to bit 4, which corresponds to a carry between the lower and upper 4-bit portions of the byte.

Consider the lower bits:

```text
1000
+1010
----
0010
```

There is a carry from bit 3 to bit 4:

```text
  01111000
+ 00001010
-----------
  10000010
       ^
       carry from the lower 4 bits
```

Therefore, the Auxiliary Carry Flag is :

**AF = 1 (set)**

---
# 7. Interrupt Flag (IF) — UNCHANGED (1)

The Interrupt Flag controls whether the processor recognizes maskable hardware interrupts.

The `ADD` instruction does **not** modify IF.



---
## Final Result

```text
CF = 0
PF = 1
AF = 1
ZF = 0
SF = 1
OF = 1
IF = Unchanged (1)
 [ PF AF SF IF OF ]
```