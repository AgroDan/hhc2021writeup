# Loops

??? cite "Loops"
    # 2) Loops

    Although you won't have to worry about writing a loop for any of these lessons, showing how a loop works is a good demo for the debugger.

    Look at the code below, then execute it (no need to change it). Watch how the same code repeats, over and over, with `rax` changing in each loop.

    Notice how the code listing below isn't the same as what is executed in the debugger. In the History section of the debugger, the instructions will change to show what is executed to achieve what you describe in the assembly source code.

Another example challenge, no answer here is needed. It simply shows how a loop is performed using Assembly.

```asm
; We want to loop 5 times - you can change this if you want!
mov rax, 5

; Top of the loop
top:
  ; Decrement rax
  dec rax

  ; Jump back to the top until rax is zero
  jnz top

; Cleanly return after the loop
ret

```