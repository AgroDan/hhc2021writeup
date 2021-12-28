# Hello, World!!

??? cite
    # Hello, World!!

    Remember syscalls? Earlier, we used them to call an exit. Now let's try another!

    This time, instead of getting a pointer to the string `Hello World`, we're going to print it to standard output (stdout).

    Have another look [at the syscall table](https://blog.rchapman.org/posts/Linux_System_Call_Table_for_x86_64/). Can you find `sys_write`, and use to to print the string `Hello World!` to stdout?

    Note: stdout's file descriptor is `1`.

    ## Hints
    -   This is a combination of the last several levels
    -   Refer to `System Calls`, but use `sys_write` instead of `sys_exit` and update the arguments accordingly
    -   Refer to `Hello, World!` on how to get a string reference into a register (i.e., `call` / `pop`)
    -   Don't forget to read the boilerplate comments - they indicate which registers to use

Now we're starting to get our hands dirty. We can utilize some of the functions within the Linux Syscall Table to start executing our own self-contained code.

To complete this exercise, first I had to look up the `sys_write` system call.

![TEMP](img/obj6-9/img1.png)

So according to this, I need to put a value of `1` in the `rax` register, send `1` to the `rdi` register (since 1 is STDOUT), the address location of the string I want to send in `rsi`, and the size of the string in `rdx`.

```asm
; TODO: Get a reference to this string into the correct register
call happy_holidays
db 'Hello World!',0

happy_holidays:
pop rax

; TODO: Set rsi to the second argument (buf - this is the "Hello World" string)
; Now we have the address of the Hello World string in rax.
; according to the sys_write docs, I need to send this to rsi
mov rsi, rax

; TODO: Set rax to the correct syscall number for sys_write
; now lets set up everything else
; the sys_write system call is a val of 1 in rax
mov rax, 1

; TODO: Set rdi to the first argument (the file descriptor, 1)
; use the file descriptor of 1 for STDOUT
mov rdi, 1

; TODO: Set rdx to the third argument (length of the string, in bytes)
; size of the string is 12
mov rdx, 12

; Set up a call to sys_write
syscall

; Return cleanly
ret
```

Note: I wrote all of the code in one little block and didn't realize there were lines starting with "TODO" that showed explicitly what to do. I just merged my own comments with the TODO lines.