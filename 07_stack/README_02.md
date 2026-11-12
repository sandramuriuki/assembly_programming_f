# Stack behavior in 02.asm

This example shows how the stack is used to save the current frame pointer and return address while a function runs.

## 1. Starting the program

The code begins with:

```asm
_start:
    call work
    mov rax, 60
    xor rdi, rdi
    syscall
```

The first instruction, `call work`, is the key stack operation here. A `call` does not merely jump; it pushes the return address onto the stack.

### Before `call`

- `RIP` points to the instruction after `call`
- `RSP` is at its current top-of-stack position

### During `call work`

- `RSP = RSP - 8`
- the return address (the address of `mov rax, 60`) is written to `[RSP]`

The program then jumps into `work`.

## 2. Function prologue: saving the frame

Inside `work`:

```asm
work:
    push rbp
    mov rbp, rsp
    sub rsp, 16
```

This is the classic stack-frame setup.

### `push rbp`

- `RSP = RSP - 8`
- `[RSP] = old RBP`

This saves the caller’s base pointer so it can be restored later.

### `mov rbp, rsp`

Now `RBP` points to the current top-of-stack after the saved frame pointer has been placed. This gives the function a stable reference point.

### `sub rsp, 16`

This reserves 16 bytes of local space for two 8-byte values. The stack grows downward again:

```text
old RSP = S
after push rbp: S - 8
after sub rsp,16: S - 24
```

Now the function can store local values at `[rbp - 8]` and `[rbp - 16]`.

## 3. Storing local values

The function then does:

```asm
    mov qword [rbp - 8], 100
    mov qword [rbp - 16], 200
```

These are stored in the newly reserved stack slots:

- `[rbp - 8] = 100`
- `[rbp - 16] = 200`

This is a typical use of the stack to allocate local variables. The values are not in registers anymore; they live in memory relative to `RBP`.

## 4. Reading the values back

The code then does:

```asm
    mov rax, [rbp - 8]
    mov rbx, [rbp - 16]
```

This loads the stored values from the stack frame into scratch registers. The stack is still serving as temporary local storage.

## 5. Cleaning up the frame

Before returning, the function does:

```asm
    mov rsp, rbp
    pop rbp
    ret
```

This unwinds the frame.

### `mov rsp, rbp`

This sets `RSP` back to the location where the saved `RBP` sits. That effectively removes the local area.

### `pop rbp`

- `RBP = [RSP]`
- `RSP = RSP + 8`

This restores the caller’s base pointer.

### `ret`

`ret` pops the return address that was placed on the stack by `call work`.

- `RIP = [RSP]`
- `RSP = RSP + 8`

Control returns to the instruction after `call work`.



This is the exact pattern used by function frames in x86-64 assembly.

## 6. Runtime observation

When assembled and executed, the program exited with status `0` and produced no console output. There was no visible program output because it only uses the stack for frame management and register transfers. The important runtime fact is that the stack pointer was restored to its original value before exit, confirming that the function frame was correctly torn down.


