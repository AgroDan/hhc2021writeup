# Level 5 - *Conversions and Comparisons*

!!! abstract "Objective"
    Pull all of the levers by submitting the requested data for each using `lever.pull(data)` to disable the Yeeter trap at the KringleCon entrance.

!!! tip "Hint"
    Move the elf to the lever. Get the lever data `lever.data()` and perform the appropriate action to the data. Submit the modified data using `lever.pull(modified_data)`.

![Map 5](/img/term_tec/img7.png)

What I started with
```python
import elf, munchkins, levers, lollipops, yeeters, pits
# Fix/Complete Code below
lever0, lever1, lever2, lever3, lever4 = levers.get()
# Solve for each lever, moving to the space
# on the lever before calling leverN.pull()

# Don't forget to move to the KringleCon entrance!
```

!!! abstract "Lever 4 challenge"
    Calling `lever.data()` will return a string to you. Take this string and concatenate it with a string of `" concatenate"`. Submit these two concatenated strings using `lever.pull(concatenated_strings)` .

!!! abstract "Lever 3 challenge"
    Submit the inverse bool object returned by pulling `lever.data()` to this lever using `lever.pull(inversed_bool_object)`. For example, if `True` is returned, then you must submit `False`.

!!! abstract "Lever 2 challenge"
    Add one `1 +` to the integer returned from running `lever.data()`. Then submit this modified int using `lever.pull(int_one_plus)`.

!!! abstract "Lever 1 challenge"
    Append the int `1` to the end of the list returned from running `lever.data()`. Submit this new list using `lever.pull(appended_list)`.

!!! abstract "Lever 0 challenge"
    lever.data() will return a `dict` object. Add a key and value pair to this dictionary of `"strkey":"strvalue"` and then submit this modified dictionary using `lever.pull(modified_dict)`.

Solution:

```python
import elf, munchkins, levers, lollipops, yeeters, pits
lever0, lever1, lever2, lever3, lever4 = levers.get()
elf.moveTo(lever4.position)
lever4.pull(lever4.data()+" concatenate")
elf.moveTo(lever3.position)
lever3.pull(not lever3.data())
elf.moveTo(lever2.position)
lever2.pull(lever2.data()+1)
elf.moveTo(lever1.position)
hohoho = lever1.data()
hohoho.append(1)
lever1.pull(hohoho)
elf.moveTo(lever0.position)
hohoho = lever0.data()
hohoho['strkey'] = 'strvalue'
lever0.pull(hohoho)
elf.moveUp(2)
```