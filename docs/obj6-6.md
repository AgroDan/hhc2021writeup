# Calling into the Void

??? cite
    # 6) Calling Into the Void

    Before we learn how to use the _Really Good_ syscalls, let's try something fun: crash our shellcode on purpose!

    You might think I'm mad, but there's a method to my madness. Run the code below and watch what happens! No need to modify it, unless you want to. :)

    Be sure to look at the debugger to see what's going on! Especially notice the top of the stack at the `ret` instruction.

    ## Hints

    -   This challenge is already solved - just click `Execute` and win! ….but…
    -   It's valuable to look at the debugger to help understand what's going on - how did we end up executing code at 0x12345678?

This was not really a challenge but rather an example of how we can crash the application by manipulating the stack and not performing any necessary cleanup before calling a return statement, which would otherwise `pop` the stack and use the resulting value as the return address, since whenever a function is called in assembly, the memory address of the last place it was reading instructions from is pushed onto the stack before moving.

```asm
; Push this value to the stack
push 0x12345678

; Try to return
ret
```

No changes here, just pushed a garbage value onto the stack before returning, forcing a segfault since the return address was changed after pushing `0x12345678` onto the stack.