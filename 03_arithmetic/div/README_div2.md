# DIV Operation — 16-bit Divisor

## EFLAGS Analysis

### CF — UNDEFINED

`DIV` does not define CF.

**CF = Undefined**

### PF — UNDEFINED 

`DIV` does not define PF.

**PF = Undefined**

### AF — UNDEFINED (1)

`DIV` does not define AF.  Therefore, the could either be 0 or 1. In this case it was 1.

**AF = Undefined**

### ZF — UNDEFINED

Even though the quotient is `166` and therefore not zero, `DIV` does not use the quotient to determine ZF.

**ZF = Undefined**

### SF — UNDEFINED

`DIV` does not define SF.

The positive quotient does not mean SF is automatically cleared.

**SF = Undefined**

### OF — UNDEFINED

`DIV` does not define OF.

The successful division does not imply that OF is cleared.

**OF = Undefined**

### IF — UNCHANGED (1)

`DIV` does not modify IF.

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