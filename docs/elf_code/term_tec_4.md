## Level 3 - *Don't Get Yeeted!*

!!! abstract "Objective"
    Move the elf to collect the lollipops and get to the KringleCon entrance.

!!! tip "Hint"
    You can walk past the Yeeter once you complete `lever0`'s task and `lever0.pull(modified_data)` in the desired way to disable to Yeeter trap. Click on the lever 0 object in the **CURRENT LEVEL OBJECTS** panel for more information.

![Map 3](/img/term_tec/img5.png)

The code I started with:
```python
import elf, munchkins, levers, lollipops, yeeters, pits
lever0 = levers.get(0)
lollipop0 = lollipops.get(0)
```

This lever has an objective:

!!! abstract "Lever objective"
    _Add_ **2** to the returned `int` value of running the function `lever0.data()` .  
  
    For example, if you wanted to _multiply_ the value by **3** and store to a variable, you could do:  
    `sum = lever0.data() * 3`  
  
    Then submit the sum using:  
    `lever0.pull(sum)`

!!! abstract "Note"
    If you submit a correct answer to `lever.pull(answer)`, then the lever and its corresponding trap will be disabled.  
  
    In order to run `lever.pull(answer)` with lever _(#0)_, you **must** be standing in its grid square located at _(x:6,y:12)_.  
  
    This particular lever object can be saved to a variable named lever using `lever = levers.get(0)`

Solution
```python
import elf, munchkins, levers, lollipops, yeeters, pits
lever0 = levers.get(0)
lollipop0 = lollipops.get(0)
elf.moveTo(lever0.position)
lever0.pull(lever0.data()+2)
elf.moveTo(lollipop0.position)
elf.moveUp(10)
```
