# Level 6 - *Types and Conditionals*

!!! abstract "Objective"
    Move the elf to the lever. Get the lever data `lever.data()` and perform the appropriate action to the data. Submit the modified data using `lever.pull(modified_data)`.

!!! tip "Hints"
    This level requires the use of operators to compare and modify data. This [link](https://www.freecodecamp.org/news/the-python-guide-for-beginners/#operators) on operators should help.  
  
    Data types will also need to be checked using conditionals in `if`, `elif`, `else` statements. This [link](https://www.freecodecamp.org/news/the-python-guide-for-beginners/#operators) on conditionals should help.  
  
    You will also need to use conditionals to check data types. This [link](https://www.freecodecamp.org/news/the-python-guide-for-beginners/#types) on types should help.

    For example, if you want to check the type of a variable, you could use:

    `if type(var) == str:`  
    `print("Its a string!")`
 
 ![Map 6](/img/term_tec/img8.png)
 
 !!! abstract "Lever Objective"
    Calling `lever.data()` will return a boolean, a number, a list of integers, a string, or a dict with `"a"` and an integer to you. For a boolean, return the inverse. For a number, return double the number. For a list of integers, return that list with each integer incremented by 1. For a string, return the string concatenated with itself. For a dict, return the dict with `a`'s value + 1. Submit this response using `lever.pull(conditional_answer)` .

    **Note**  
  
    If you submit a correct answer to `lever.pull(answer)`, then the lever and its corresponding trap will be disabled.  
  
    In order to run `lever.pull(answer)` with lever _(#0)_, you **must** be standing in its grid square located at _(x:2,y:4)_.  
  
    This particular lever object can be saved to a variable named lever using `lever = levers.get(0)`

Solution:

```python
import elf, munchkins, levers, lollipops, yeeters, pits
def holiday_cheer(obj):
    if type(obj) is str:
        return obj+obj
    if type(obj) is bool:
        return not obj
    if type(obj) is int:
        return obj*2
    if type(obj) is list:
        return [i+1 for i in obj]
    if type(obj) is dict:
        obj['a'] += 1
        return obj

lever = levers.get(0)
elf.moveTo(lever.position)
lever.pull(holiday_cheer(lever.data()))
elf.moveUp(2)
```