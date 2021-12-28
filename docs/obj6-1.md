# Introduction

??? cite
    
    # Welcome to Shellcode Primer!
  
    This is a training program conceived by Jack Frost (yes, THE Jack Frost) to train trolls how to build exploit code, from the ground up. This will teach how to write working x64 shellcode to read a file and print it to standard output!
  
    If you're new to this, we recommend reading this introduction thoroughly!

    ## Introduction
  
    In this challenge, you will be hand-crafting increasingly complex shellcode, written in x64. If that sounds scary, don't fret! We will guide you step by step!

    Choose your challenge on the left (Introduction will be open by default), read the instructions on the top, and start writing code! We'll provide the basic structure of the code to help make sure you're heading in the right direction.

    ## What is Shellcode?

    Shellcode is small, position-independent assembly code that is typically executed as the payload of an exploit. For the initial challenges, you'll write code and see what it does - no exploit required.
  
    The important thing about shellcode is that it doesn't typically have access to libraries or functions that you might be accustomed to; it needs to be entirely self-contained! Even normally simple things like defining a string or opening a file can  be tricky. We'll cover those things as they come up!
  
    ## Using Shellcode Primer
  
    As you type code, it will be assembled in the background. Assembling takes the assembly code you write and translates it into machine code (which is represented as a series of hex characters). We use the metasm Ruby library to assemble, in case you want to work on your code locally:
    ```ruby
    require 'metasm'
    assembled = Metasm::Shellcode.assemble(Metasm::X86_64.new, payload['code']).encode_string.unpack('H*').pop()
    ```
          
    When your code successfully assembles, you can execute it by clicking the Execute button at the bottom. That'll run the code in a virtual machine, and instrument each step so you can see exactly what's going on!

    ## Good Luck!

The above was given as the introduction. No challenge here, but the code presented below shows the basics of how assembly code is written.


```asm
; Set up some registers (sorta like variables) with values
; In the debugger, look how these change!
mov rax, 0
mov rbx, 1
mov rcx, 2
mov rdx, 3
mov rsi, 4
mov rdi, 5
mov rbp, 6

; Push and pop - watch how the stack changes!
push 0x12345678
pop rax

push 0x1111
push 0x2222
push 0x3333
pop rax
pop rax
pop rax

; This creates a string and references it in rax - watch the debugger!
call getstring
  db "Hello World!",0
getstring:
pop rax

; Finally, return 0x1337
mov rax, 0x1337
ret

```