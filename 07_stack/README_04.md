# Stack behavior in 04.asm

This is the 32-bit equivalent of a stack-frame example. It demonstrates the use of the stack for saving the previous base pointer and allocating local variables inside a function.


## 1. The `call` pushes a return address

A 32-bit call behaves the same as in 64-bit mode, except the stack pointer is `ESP` and the return address is 4 bytes long instead of 8.

```text
ESP = ESP - 4
[ESP] = return address
```

This is how the CPU remembers where execution should continue when `work` returns.

## 2. Function prologue

Inside `work`:

```asm
work:
    push ebp
    mov ebp, esp
    sub esp, 8
```

This is the 32-bit stack-frame setup.

### `push ebp`

- `ESP = ESP - 4`
- `[ESP] = old EBP`

This preserves the previous base pointer so it can be restored later.

### `mov ebp, esp`

Now `EBP` points at the saved frame pointer, and the function has a stable place to refer to its local data.

### `sub esp, 8`

This reserves 8 bytes of stack space for local variables. In 32-bit mode, each slot is 4 bytes, so `sub esp, 8` creates two 32-bit local slots.

The layout is now conceptually:

```text
[ebp - 4] = local slot 1
[ebp - 8] = local slot 2
```

## 3. Local variables are stored on the stack

The function does:

```asm
    mov dword [ebp - 4], 100
    mov dword [ebp - 8], 200
```

This stores the values in the reserved space. In other words, the stack holds the local values for the function rather than the registers.

Then:

```asm
    mov eax, [ebp - 4]
    mov ebx, [ebp - 8]
```

`EAX` and `EBX` are loaded from those stack locations. This demonstrates that stack memory is usable as temporary local storage.

## 4. Frame cleanup

Before returning, the function executes:

```asm
    mov esp, ebp
    pop ebp
    ret
```

### `mov esp, ebp`

This removes the local variable area by resetting `ESP` back to the saved `EBP` position.

### `pop ebp`

- `EBP = [ESP]`
- `ESP = ESP + 4`

This restores the caller’s base pointer.

### `ret`

The return instruction pops the saved return address from the stack and resumes execution after the `call`.


## 5. Runtime observation

When assembled and executed, the program exits successfully with status `0`. There was no visible output, because it performs only register and stack manipulation and then exits via the Linux i386 syscall. The important runtime observation is that after the function returns, the register and stack state are consistent and the process exits normally.

