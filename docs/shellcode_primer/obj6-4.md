# Returning a Value

??? cite "Returning a Value"
    # 4) Returning a Value

    Now that we have an empty function, we can start building some code! Let's learn what a _register_ is.

    A register is like a variable, except there are a small number of them - you have about eight general purpose 64-bit integers registers on amd64 (we won't talk about floating point or other special registers):

    -   rax
    -   rbx
    -   rcx
    -   rdx
    -   rdi
    -   rsi
    -   rbp
    -   rsp

    All mathy stuff that a computer does (add, subtract, xor, etc) operates on registers, not directly on memory. So they're super important!

    Specific registers have some implicit meaning, mostly by convention. For example, when a function returns, its return value is typically put in `rax`. Let's do that!

    To move a value into a register, use the `mov` instruction; for example:

    `mov rdx, 1`

    In a higher-level language this would be equivalent to:

    `rdx = 1` —

    For this level, can you return the number '1337' from your function?

    That means that `rax` must equal `1337` when the function returns.

    ## Hints:

    -   Unlike most languages, you don't return values with `ret X`; instead, you set `rax` to a value, then return
    -   To set a register, use `mov REGNAME, value`; for example, `mov rcx, 123`
    -   The return register is `rax`
    -   If something isn't working, don't forget to check the debugger that pops up when you click Execute! It'll show you the state of every register at every step

For this challenge, all we needed to do was move the numeric value `1337` into the `rax` register. Easy peasy.

```asm
; TODO: Set rax to 1337

mov rax, 1337

; Return, just like we did last time
ret

```