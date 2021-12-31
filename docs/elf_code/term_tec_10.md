# Level 9 - *Yeeter Swirl*

This challenge looks [vaguely familiar...](https://hhc2020.agrohacksstuff.io/#kiosk10/#stage-7-yeeter-swirl)

!!! abstract "Objective"
    Follow the swirl being careful not to step on any traps (or get yeeted off the map). **Note:** The `elf.moveTo(object)` function has been disabled for this challenge.

!!! tip "Hint"
    Use loops and an incrementing count to take the exact number of steps. Some sample code has been started for you but needs to be fixed/finished.

![Map 9](/img/term_tec/img11.png)

The levers all ask that you pull with a number that is incremented, for example lever0 is pulled with `lever.pull(0)`, lever1 is `lever.pull(1)`, etc.

Starting code, most of the fun stuff is already completed:

```python
import elf, munchkins, levers, lollipops, yeeters, pits

def func_to_pass_to_mucnhkin(list_of_lists):
    sum_of_ints_in_list_of_lists = 9
    return sum_of_ints_in_list_of_lists

all_levers = levers.get()
# Create Movement pattern:
moves = [elf.moveDown, elf.moveLeft, elf.moveUp, elf.moveRight] * 2

# We iterate over each move in moves getting an index (i) number that increments by one each time
for i, move in enumerate(moves):
    # We need to call each move
    # if i is less than the len(all_levers), we pull the lever
    
# We should be at lollipop 2. We need to 
# Get to munchkin and answer their question
# by passing our finished function

```

!!! abstract "The Munchkin's challenge"
    `munchkin.ask()` will not be used for my challenge. Instead, create a function that will accept one argument.

    For example:

    ```
    def YourFunctionNameHere(one_argument):
        // some function code will go here
        return some_desired_data
    ```

    Your created function will be passed a randomized `list` containing `list`'s which contain `str`'s and `int`'s.

    For example:

    ```
    [
        [1,"sdff",2,9,"olidfhj",6],
        [2,5,1,"jdhgwe",4],
        ["wyuier",2,2,9,2,"jfghwgfb",5],
        [4,"bnwc",9]
    ]
    ```

    Your created function must be able to iterate over this randomized list and each of its child `list`'s and return the total sum of adding all of the `int`'s in all of the child `list`'s.

    Once you have created this function and are sure it will return the desired sum, pass your created function as an argument to me:

    `munchkin.answer(YourFunctionNameHere)`

    If your passed function works properly, I will become friendly and move out of your way.

Solution

```python
import elf, munchkins, levers, lollipops, yeeters, pits

def func_to_pass_to_munchkin(list_of_lists):
    sum_of_ints_in_list_of_lists = 0
    for i in list_of_lists:
        for j in i:
            if type(j) is int:
                sum_of_ints_in_list_of_lists += j
    return sum_of_ints_in_list_of_lists

all_levers = levers.get()
# Create Movement pattern:
moves = [elf.moveDown, elf.moveLeft, elf.moveUp, elf.moveRight] * 2

# We iterate over each move in moves getting an index (i) number that increments by one each time
for i, move in enumerate(moves):
    move(i+1)
    if i < len(all_levers):
        all_levers[i].pull(i)
elf.moveUp(2)
elf.moveLeft(4)
munchkin = munchkins.get(0)
munchkin.answer(func_to_pass_to_munchkin)
elf.moveUp(1)
```