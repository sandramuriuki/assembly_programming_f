# Stack behavior in 03.asm

This program demonstrates the simplest form of function call and return in assembly: the `call` instruction pushes a return address onto the stack, and `ret` pops it back so execution resumes at the correct point.

## 1. Start of execution

The program begins with:

```asm
_start:
    mov rax, 10
    call calculate

after_call:
    ; RAX should now be 15
    nop
```

At this point:

- `RAX = 10`
- `RSP` is unchanged from the initial stack state

The key step is the `call calculate` instruction.

## 2. `call` and the return address

The `call` instruction performs two actions:

1. it pushes the address of the next instruction (`after_call`) onto the stack,
2. it jumps to `calculate`.

In stack terms:

```text
RSP = RSP - 8
[RSP] = address of after_call
```

The saved address is the value that will be restored by `ret`.

## 3. The calculation function

The function is:

```asm
calculate:
    add rax, 5
    ret
```

The value in `RAX` is originally `10`.

When `add rax, 5` executes, the register becomes:

```text
RAX = 15
```

This is the only arithmetic operation in the function.

## 4. `ret` restores control flow

The `ret` instruction is what uses the stack to return execution to the caller.

It does:

```text
RIP = [RSP]
RSP = RSP + 8
```

So the stored return address is popped from the top of the stack and execution continues at the label `after_call`.

By the time execution reaches `after_call`, `RAX` is still `15` because the add instruction modified the register before the return. This is why the comment says:

```asm
; RAX should now be 15
```



No local variables are pushed or popped here; the stack is used only to preserve the program counter so execution can resume correctly.

## 5. Runtime observation

When run, the program exited cleanly with status code `0` and produced no terminal output. This is expected because the program does not print anything; it only modifies `RAX` and uses `call`/`ret` to branch and return. The important observation is that the stack preserved the return address successfully, because the program returned to `after_call` without skipping or crashing.
