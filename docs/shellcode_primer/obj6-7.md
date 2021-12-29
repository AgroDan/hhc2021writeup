# Getting RIP

??? cite "Getting RIP"
    # 7) Getting RIP

    What happened in the last exercise? Why did it crash at `0x12345678`? And did you notice that 0x12345678 was on top of the stack when `ret` happened?

    The short story is this: `call` pushes the return address onto the stack, and `ret` jumps to it. Whaaaat??

    This is going to be long, but hopefully will make it all clear!

    ---

    Let's back up a bit. At any given point, the instruction currently being executed is stored in a special register called the instruction pointer (`rip`), which you may also hear called a program counter (`pc`).

    What is the `rip` value at the first line in our code? Well, since we have a debugger, we know that it's `0x13370000`. But sometimes you don't know and need to find out.

    The most obvious answer is to treat it like a normal register, like this:

    `mov rax, rip`  
    `ret`  

    Does that work? Nope! You can't directly access `rip`. That means we need a trick!

    ---

    When you use `call` in x64, the CPU doesn't care where it's calling, or whether there's a `ret` waiting for it. The CPU assumes that, if the author put a `call` in, there will naturally be a `ret` on the other end. Doing anything else would just be silly! So `call` pushes the return address onto the stack before jumping into a function. When the function complete, the `ret` instruction uses the return address on the stack to know where to return to.

    The CPU assumes that, sometime later, a `ret` will execute. The `ret` assumes that at some point earlier a `call` happened, and that means that the top of the stack has the return address. The `ret` will retrieve the return address off the top of the stack (using `pop`) and jump to it.

    Of course, we can execute `pop` too! If we `pop` the return address off the stack, instead of jumping to it, the address goes into a register. Hmm! Does that also sound like `mov REG, rip` to you?

    ---

    For this exercise, can you `pop` the address after the call - the _No Op_ (`nop`) instruction - into `rax` then return?

    ## Hints

    -   Nothing above the `nop` instruction should (or can) be modified
    -   After the `place_below_the_nop:` label, the top of the stack is the value you want - you can see it in the debugger!
    -   The `pop REG` instruction will remove the top value from the stack and put it in the register identified by `REG` (replace `REG` with the register name)
    -   If you do anything else to the stack, like `pop` a second time, the `ret` at the end of the function will no longer work!

This challenge shows a technique we can use to leak the location of the last instruction. This is useful for when working with protections such as ASLR and PIC(?), which randomizes the location of the code within the virtual memory space, and can be used for writing shellcode that relies on some form of math to find out where to send instructions to executable code.

```asm
; Remember, this call pushes the return address to the stack
call place_below_the_nop

; This is where the function *thinks* it is supposed to return
nop

; This is a 'label' - as far as the call knows, this is the start of a function
place_below_the_nop:

; TODO: Pop the top of the stack into rax
pop rax

; Return from our code, as in previous levels
ret
```

Simply added `pop rax`

This allows us to find the address of the `nop` instruction.

The basic idea here is that when the `call` function happens, it jumps to the `place_below_the_nop` label. It then pops the address off the stack and into rax, then returns to *somewhere*.