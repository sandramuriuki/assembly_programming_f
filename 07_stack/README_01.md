# Stack behavior in 01.asm

This program demonstrates the simplest stack pattern: storing register values, then restoring them with `push` and `pop` in reverse order.

## 1. Start of execution

The program begins with:

```asm
_start:
    mov rax, 100
    mov rbx, 200
```

At this point:

- `RAX = 100`
- `RBX = 200`
- `RSP` still points to the top of the stack as it was before the program started.

No stack memory has been used yet.

## 2. Pushing values onto the stack

Next the code does:

```asm
    push rax
    push rbx
```

On x86-64, each `push` instruction subtracts 8 bytes from `RSP` and stores the full 64-bit register value at the new top of the stack.

### Step-by-step

1. `push rax`
   - `RSP = RSP - 8`
   - `[RSP] = 100`

2. `push rbx`
   - `RSP = RSP - 8`
   - `[RSP] = 200`

This means the stack now has this logical shape:

```text
top -> [RSP] = 200
       [RSP + 8] = 100
```

The last value pushed is the first value popped, which is the defining behavior of a stack: LIFO.

## 3. Pop operations

Then the code does:

```asm
    pop rcx
    pop rdx
```

Each `pop` does the opposite of `push`:

1. `pop rcx`
   - `RCX = [RSP]`
   - `RSP = RSP + 8`
   - `RCX = 200`

2. `pop rdx`
   - `RDX = [RSP]`
   - `RSP = RSP + 8`
   - `RDX = 100`

At the end of the pops, `RSP` returns to the same value it had before the `push` operations. The stack is effectively restored to its original state.

## 4. Conclusion

This program shows that the stack is a temporary storage area for preserving data across operations. The values do not vanish permanently; they are simply moved to and from the top of the stack.

The final stack pointer movement is:

```text
Before pushes: RSP = S
After push rax: RSP = S - 8
After push rbx: RSP = S - 16
After pop rcx: RSP = S - 8
After pop rdx: RSP = S
```

## 5. Runtime observation

When this file was assembled and executed, it exited successfully with status code `0` and produced no visible output. That is expected: the program only manipulates registers and the stack; it does not print text or write to a file. The important observation is that the stack pointer moves down during pushes and back up during pops, then returns to its original value before exit.


