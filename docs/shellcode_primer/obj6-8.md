# Hello, World

??? cite "Hello, World!"
    # Hello, World!

    So remember how last level, we got the address of `nop` and returned it?

    Did you see that `nop` execute? Nope! We jumped right over it, but stored its address en-route. What can we do by knowing our own address?

    Well, since shellcode is, by definition, self-contained, you can do other fun stuff like include data alongside the code!

    What if the return address isn't an instruction at all, but a string?

    ---

    For this next exercise, we include a plaintext string - `'Hello World'` - as part of the code. It's just sitting there in memory. If you look at the compiled code, it's all basically `Hello World`, which doesn't run.

    Instead of trying to run it, can you `call` past it, and `pop` its address into `rax`?

    Don't forget to check the debugger after to see it in `rax`!

    ## Hints
    - This is pretty much the same as the previous challenge, except `nop` has been replaced with a string

This was essentially the same challenge as the previous one, only now we jumped over a location of where a string is stored in memory.

```asm
; This would be a good place for a call
call merry_christmas
; This is the literal string 'Hello World', null terminated, as code. Except
; it'll crash if it actually tries to run, so we'd better jump over it!
db 'Hello World',0

; This would be a good place for a label and a pop
merry_christmas:
pop rax

; This would be a good place for a re... oh wait, it's already here. Hooray!
ret
```

My changes: Added the `call merry_christmas` line, then the function itself.