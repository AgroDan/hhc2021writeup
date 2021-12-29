# Level 7 - *Up Down Loopiness*

!!!+ note "Objective"
    Navigate through the obstacles and collect the lollipop before arriving at the KringleCon entrance.

???+ note "Hints"
    Using a `for` loop can reduce how many lines and/or object function calls are used. This [link](https://www.freecodecamp.org/news/the-python-guide-for-beginners/#forloops) on `for` loops may be helpful.

    Using `elf.moveLeft(40)` will move your elf as far as possible before hitting an obstacle or the end of the screen. Use however large a number you think you need!

![Map 7](/img/term_tec/img9.png)

No levers, just restrictive as to how much code you can enter.

Solution
```python
import elf, munchkins, levers, lollipops, yeeters, pits
lollipop = lollipops.get(0)
for num in range(2):
    elf.moveLeft(2)
    elf.moveUp(11)
    elf.moveLeft(2)
    elf.moveDown(11)

elf.moveTo(lollipop.position)
elf.moveUp(10)
```