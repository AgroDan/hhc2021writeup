# Level 4 - *Data Types*

!!! abstract "Objective"
    Pull ALL of the levers by submitting the requested data for each using `lever.pull(data)` to disable the Yeeter trap at the KringleCon entrance.

!!! tip "Hints"
    Move the elf to the lever. Get the lever data `lever.data()` and perform the appropriate action to the data. Submit the modified data using `lever.pull(modified_data)`.

    This level requires you to check and convert variable data types (bool, int, str, float, list, dict, etc.) This [link](https://www.freecodecamp.org/news/the-python-guide-for-beginners/#types) should prove useful. Some data type examples include:

    -   `10` - This has a data type of `int`
    -   `"Hello World"` - This has a data type of `str`
    -   `[1,2,3]` - This has a data type of `list`. This list contains three `int` objects.

![Map 4](/img/term_tec/img6.png)

What I started with:
```python
import elf, munchkins, levers, lollipops, yeeters, pits
# Complete the code below:
lever0, lever1, lever2, lever3, lever4 = levers.get()
# Move onto lever4
elf.moveLeft(2)
# This lever wants a str object:
lever4.pull("A String")
# Need more code below:
```

All the levers here asked to send it a specific datatype. Strings, booleans, integers, lists, and dictionaries.

Solution:
```python
import elf, munchkins, levers, lollipops, yeeters, pits
lever0, lever1, lever2, lever3, lever4 = levers.get()
elf.moveLeft(2)
lever4.pull("Ho ho ho!")
elf.moveTo(lever3.position)
lever3.pull(True)
elf.moveTo(lever2.position)
lever2.pull(1225)
elf.moveTo(lever1.position)
lever1.pull(['Merry', 'Christmas!'])
elf.moveTo(lever0.position)
lever0.pull({'Merriness': 100})
elf.moveUp(2)
```