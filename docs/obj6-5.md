# System Calls

??? cite

    # 5) System Calls

    If you've made it this far, I bet you're wondering how to make your shellcode _do_ something!

    If you're familiar with Python, you might know how to use the `open()` function. If you know C, you might know the `fopen()` function. But what these and similar functions have in common is one thing: they're library code. And because shellcode needs to be self contained, we don't have (easy) access to library code!

    So how do we deal with that?

    Linux has something called a `syscall`, or system call. A syscall is a request that a program makes that asks Linux - the kernel - to do something. And it turns out, at the end of the day, all of those library calls ultimately end with a syscall. [Here is a list of available syscalls on x64](https://blog.rchapman.org/posts/Linux_System_Call_Table_for_x86_64/) ([alternative](https://chromium.googlesource.com/chromiumos/docs/+/master/constants/syscalls.md))

    To perform a syscall:

    -   The number for the desired syscall is moved into `rax`
    -   The first parameter is moved into `rdi`, the second into `rsi`, and the third into `rdx` (there are others, but not many syscalls need more than 3 parameters)
    -   Execute the `syscall` instruction

    The second `syscall` executes, Linux flips into kernel mode and we can no longer debug it. When it's finished, it returns the result in `rax`.

    ---

    For this challenge, we're going to call `sys_exit` to exit the process with exit code 99.

    Can you prepare `rax` and `rdi` with the correct values to exit?

    As always, feel free to mess around as much as you like!

    ## Hints
    -   Start by consulting a syscall table and finding the number for `sys_exit`, and `mov`ing that into `rax`
    -   Next, `mov` the desired return value into `rdi` (the first parameter to every syscall)
    -   Finally, use the literal `syscall` instruction
    -   If something isn't working, be sure to read the problem list in the debugger! It tries to detect any and all issues

This challenge was a little bit more involved as it showed how things get "executed" in Assembly. Using the `syscall` directive, the assembler would know what function to call from the Linux System Call table based on what numeric value was placed in the `rax` register. This was similar to the x86 architecture, though instead of the `syscall` statement and the `rax` register being used, the number pertaining to the Syscall function was moved to the `eax` register, and an `int 0x80` directive was used instead. Otherwise it is the same basic principle.

```asm
; TODO: Find the syscall number for sys_exit and put it in rax
; sys_exit is 60

mov rax, 60
; TODO: Put the exit_code we want (99) in rdi

mov rdi, 99

; Perform the actual syscall
syscall
```

The answer here was to move `60` into the `rax` register to signify a `sys_exit` call, then moved `99` into the `rdi` register for its argument, which exits the program with a code of `99`.