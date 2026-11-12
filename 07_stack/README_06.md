# Stack behavior in 06.asm

This file is the 32-bit version of the same basic stack pattern as 05.asm. It demonstrates that the same LIFO rules apply in 32-bit mode, but using `EAX`, `EBX`, and `ESP` instead of the 64-bit registers.

## 1. Initial register state

The program begins with:

```asm
_start:
    mov eax, 0x11223344
    mov ebx, 0x1234

    push eax
    push ebx
```

At this point:

- `EAX = 0x11223344`
- `EBX = 0x1234`

These are both 32-bit values, and each `push` stores a full 32-bit value on the stack.

## 2. Pushing values onto the stack

The operation `push eax` does:

```text
ESP = ESP - 4
[ESP] = 0x11223344
```

Then `push ebx` does:

```text
ESP = ESP - 4
[ESP] = 0x00001234
```

The stack now holds the values in this order:

```text
top -> [ESP] = 0x00001234
       [ESP + 4] = 0x11223344
```

This is the classic stack pattern: the most recently pushed value is placed at the top of the stack.

## 3. Pop operations restore values in reverse order

The next instructions are:

```asm
    pop ebx
    pop eax
```

### `pop ebx`

```text
EBX = [ESP]
ESP = ESP + 4
```

This reads the top value, which is `0x00001234`, and restores it to `EBX`.

### `pop eax`

```text
EAX = [ESP]
ESP = ESP + 4
```

This reads the remaining value, which is `0x11223344`, and restores it to `EAX`.

At the end, `ESP` has returned to the same location it had before the pushes.

## 4. `ESP` movement

The pointer movement is:

```text
Before pushes:      ESP = S
push eax:           ESP = S - 4
push ebx:           ESP = S - 8
pop ebx:            ESP = S - 4
pop eax:            ESP = S
```

This demonstrates the LIFO nature of the stack exactly, just in 32-bit form.

## 5. Conclusion

This program is a simple illustration of saving temporary register values while doing other work or preserving data across steps. Even though no other work happens in the program, the behavior clearly shows how the stack is used as a temporary storage area for 32-bit values.

It is the same concept as in 64-bit mode, but with smaller data width and different register names.

## 6. Runtime observation

When assembled and executed, the program exited successfully with status code `0`. There was no printed output, because this example only manipulates registers and the stack and then exits. The notable runtime fact is that the values were restored correctly after the pops, because the program exited normally without any stack corruption or crash.

