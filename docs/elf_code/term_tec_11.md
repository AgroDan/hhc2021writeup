# Level 10 - *Munchkin Dodging Finale*

!!!+ note "Objective"
    Dodge the munchkins to get to the KringleCon entrance.

???+ note "Hints"
    You want to move once each munchkin is the furthest grid coordinates aways on the x axis (which will be `6` for each munchkin). Use while loops and implement a conditional check using the `elf.position["x"]` and `munchkin.position["x"]` values to check how far away the munchkin is before using `moveTo` to the next lollipops position. When using while loops, use a small delay of `time.sleep(0.05)` to ensure the browser does not lock up.

![Map 10](/img/term_tec/img12.png)

These munchkins are under strict orders to never be friendly! I have to sneak past them as they move back and forth.

Original code:

```python
import elf, munchkins, levers, lollipops, yeeters, pits
import time
muns = munchkins.get()
lols = lollipops.get()[::-1]
for index, mun in enumerate(muns):
    # need to wait while absolute distance between
    # elf.position["x"] and mun.position['x'] is less than 6
    # then we move to next lollipop
    # We can use time.sleep(0.05) to add a small delay in a while loop
```

Solution:

```python
import elf, munchkins, levers, lollipops, yeeters, pits
import time
muns = munchkins.get()
lols = lollipops.get()[::-1]
for index, mun in enumerate(muns):
    while abs(elf.position["x"]-mun.position["x"]) < 6:
        time.sleep(0.05)
    
    elf.moveTo(lols[index].position)

elf.moveLeft(6)
elf.moveUp(2)
```

ELVES RULE MUNCHKINS DROOL

![Elves Rule Munchkins Drool](/img/term_tec/img13.png)