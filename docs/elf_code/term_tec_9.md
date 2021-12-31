# Level 8 - *Two Paths, Your Choice*

!!! abstract "Objective"
    Navigate past the obstacles and avoid the munchkin watching the KringleCon entrance.

!!! tip "Hints"
    Reduce the number of lines necessary to reach the KringleCon entrance by using a loop. This [link](https://www.freecodecamp.org/news/the-python-guide-for-beginners/#forloops) on `for` loops will be helpful.

    There are two paths for you to choose from. Choosing the lever takes more steps but may be easier to solve.

![Map 8](/img/term_tec/img10.png)

This one has a munchkin! I have the choice of asking the munchkin to pass, or pulling the lever and ending his tyranny.

First, the munchkin solution:

```python
import elf, munchkins, levers, lollipops, yeeters, pits
all_lollipops = lollipops.get()
for lollipop in all_lollipops:
    elf.moveTo(lollipop.position)
# After loop we solve the lever or munchkin challenge and move to end.
elf.moveLeft(8)
elf.moveUp(2)
munchkin = munchkins.get(0)
munchkin.answer(next((k for k, v in munchkin.ask().items() if v == 'lollipop')))
elf.moveUp(2)
```

TODO: The next solution