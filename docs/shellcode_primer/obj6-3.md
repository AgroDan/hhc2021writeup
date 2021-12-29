# Getting Started

??? cite "Getting Started"
    # 3) Getting Started

    Welcome! Are you ready to learn how to write shellcode? We hope so! First, some tips:

    -   Comments are denoted with a semicolon (`;`)
    -   Don't forget to look at the debugger, line by line, if something is wrong
    -   **Really, don't forget to read the error list!** We check each place where you might go wrong in your code
    -   Your code for each level is saved in your browser, so you can leave and come back, refresh the page, and hop back to previous levels to borrow code

    ---

    This level currently fails to build because it has no code. Can you add a `ret`urn statement at the end? Don't worry about what it's actually returning (yet!)

    Feel free to check previous levels!

    ## Hints
    -   The opcode to return is `ret`
    -   The solution is literally just `ret` - return!

The answer to this code is extremely simple. Just add a `ret` command!

```asm
; This is a comment! We'll use comments to help guide your journey.
; Right now, we just need to RETurn!
;
; Enter a return statement below and hit Execute to see what happens!

ret
```