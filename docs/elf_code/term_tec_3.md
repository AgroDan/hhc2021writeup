# Level 2 - *Get moveTo'ing*

???+ note "Objective"
    Move the elf to collect the lollipops and get to the KingleCon entrance

!!!+ note "Hint"
    The `elf.moveTo` function should help reduce the number of elf move function calls, if used properly.

![Map 2](/img/term_tec/img4.png)

The code I was presented with...
```python
import elf, munchkins, levers, lollipops, yeeters, pits
# Gets all lollipops as a list
all_lollipops = lollipops.get()
# Can set lollipop1 using:
lollipop1 = all_lollipops[1]
# Can also set lollipop0 using:
lollipop0 = lollipops.get(0)
# or:
lollipop0 = all_lollipops[1]
elf.moveTo(lollipop1.position)
```

Solution:
```python
import elf, munchkins, levers, lollipops, yeeters, pits
all_lollipops = lollipops.get()
elf.moveTo(all_lollipops[1].position)
elf.moveTo(all_lollipops[0].position)
elf.moveLeft(3)
elf.moveUp(6)
```
