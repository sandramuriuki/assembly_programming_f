# Stack behavior in 05.asm

This example shows how the stack is used to temporarily store full register values and then restore them in reverse order. It is a good demonstration of stack discipline and register preservation.

## 1. Initial values

The program starts with:

```asm
_start:
    mov rax, 0x1122334455667788
    mov rbx, 0x1234

    push rax
    push rbx
```

At this stage:

- `RAX = 0x1122334455667788`
- `RBX = 0x1234`

These are both full 64-bit register values.

## 2. Pushing full registers onto the stack

Each `push` subtracts 8 bytes from `RSP` and writes the full 64-bit value to the new top-of-stack position.

### `push rax`

```text
RSP = RSP - 8
[RSP] = 0x1122334455667788
```

### `push rbx`

```text
RSP = RSP - 8
[RSP] = 0x0000000000001234
```

Now the stack contains:

```text
top -> [RSP] = 0x1234
       [RSP + 8] = 0x1122334455667788
```

The newest pushed value is at the top, so it will be the first value popped.

## 3. The `pop` operations

The next instructions are:

```asm
    pop rbx
    pop rax
```

### `pop rbx`

```text
RBX = [RSP]
RSP = RSP + 8
```

So `RBX` receives the value `0x1234`.

### `pop rax`

```text
RAX = [RSP]
RSP = RSP + 8
```

So `RAX` receives the earlier value `0x1122334455667788`.

At this point, the stack is restored to its prior state, and `RSP` has returned to the original value.

## 4. How `RSP` changes

The stack pointer moves like this:

```text
Before pushes:      RSP = S
push rax:           RSP = S - 8
push rbx:           RSP = S - 16
pop rbx:            RSP = S - 8
pop rax:            RSP = S
```

This is exactly how a proper LIFO stack works.

## 5. Conclusion

This program demonstrates that the stack can preserve register values across multiple operations without permanently changing the data in the registers. It is especially common when a function needs to temporarily save registers before using them for other work.

The stack acts as a temporary holding area for full 64-bit values.

## 6. Runtime observation

When this file was assembled and run, it exited successfully with status `0`. There was no terminal output because the program does not print anything. The important program behavior is not visible output, but the fact that the register values are restored in reverse order after the pops. That confirms the stack was used correctly and returned to the original state.


