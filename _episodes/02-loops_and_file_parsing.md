---
title: "File Parsing"
teaching: 20
exercises: 25
questions:
- "How do I sort through all the information in a text file and extract particular pieces of information?"
objectives:
- "Use a for loop to perform the same action on the items in a list."
- "Use the append function to create new lists in for loops."
- "Open a file and read in its contents line by line."
- "Search for a particular string in a file."
- "Manipulate strings and change data types."
- "Print to a new file."
keypoints:
- "Indentation is very important in `for` loops and `if` statements.  Don't forget the `:` and to indent the items in the loop."
- "You should use the os.path module to work with file paths."
- "One of the most flexible ways to read in the lines of a file is the `readlines()` function."
- "An `if` statement can be used to find a particular string within a file."
- "The split() function can be used to seperate the elements of a string."
- "You will often need to recast data into a different data type when it was read in as a string."
---
## Repeating an operation many times: for loops
Often, you will want to do something to every element of a list.  The structure
to do this is called a `for` loop.  The general structure of a `for` loop is
```
for variable in list:
    do things using variable # This line is not executable python!
```
{: .language-python}

There are two very important pieces of syntax for the `for` loop. Notice the colon `:` after the word list. You will always have a colon at the end of a `for` statement. If you forget the colon, you will get an error when you try to run your code.

The second thing to notice is that the lines of code under the `for` loop (the things you want to do several times) are indented. Indentation is very important in python.  There is nothing like an `end` or `exit` statement that tells you that you are finished with the loop. The indentation shows you what statements are in the loop. Each indentation is 4 spaces by convention in Python 3. However, if you are using an editor which understands Python, it will do the correct indentation for you when you press the tab key on your keyboard. In fact, the Jupyter notebook will notice that you used a colon (`:`) in the previous line, and will indent for you (so you will not need to press tab).

In the last episode, we had a list of energies in kcal. Let's use a loop to change all of our energies in kcal to kJ.
```
for number in energy_kcal:
    kJ = number * 4.184
    print(kJ)
```
{: .language-python}

```
-56.0656
-11.296800000000001
22.593600000000002
176.1464
```
{: .output}

Now it seems like we are really getting somewhere with our program!  But it would be even better if instead of just printing the values, it saved them in a new list.  To do this, we are going to use the `append` function that we discovered in the last episode.  The `append` function adds a new item to the end of an existing list.  The general form of the append function is
```
list_name.append(new_thing)
```
{: .language-python}

Try running this block of code.  See if you can figure out why it doesn't work.
```
for number in energy_kcal:
    kJ = number * 4.184
    energy_kJ.append(kJ)

print(energy_kJ)
```
{: .language-python}
```
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-12-595146886489> in <module>()
      2 for number in energy_kcal:
      3     kJ = number*4.184
----> 4     energy_kJ.append(kJ)
      5
      6 print(energy_kJ)

NameError: name 'energy_kJ' is not defined
```
{: .error}

This code doesn't work because on the first iteration of our loop, the list `energy_kJ` doesn't exist.  To make it work, we have to start the list outside of the loop.  The list can be blank when we start it, but we have to start it.

```
energy_kJ = []
for number in energy_kcal:
    kJ = number * 4.184
    energy_kJ.append(kJ)

print(energy_kJ)
```
{: .language-python}

```
[-56.0656, -12.1336, 22.593600000000002, 176.1464]
```
{: .output}

## Making choices: logic Statements
Within your code, you may need to evaluate a variable and then do something if the variable has a particular value.  This type of logic is handled by an `if` statement.  In the following example, we only append the negative numbers to a new list.
```
negative_energy_kJ = []

for number in energy_kJ:
    if number < 0:
        negative_energy_kJ.append(number)

print(negative_energy_kJ)
```
{: .language-python}
```
[-56.0656, -11.296800000000001]
```
{: .output}

Other logic operations include
- equal to `==`
- not equal to `!=`
- greater than `>`
- less than `<`
- greater than or equal to `>=`
- less than or equal to `<=`

Notice that we use two equals signs (`==`) to check if two things are equal. **Why?** <br>

If you are comparing strings, not numbers, you use different logic operators like `is`, `in`, or `is not`.  We will see these types of logic operators used in our next lesson.

### Compound comparisons
More than one condition can be checked at the same time, by using `and`, `or`, and `not`.
```
negative_numbers = []
for number in energy_kJ:
    if number < 0 or number == 0:
        negative_numbers.append(number)

print(negative_numbers)
```
{: .language-python}
```
[-56.0656, -11.296800000000001]
```
{: .output}

When using `or` for compound comparisons:
* `or` is **True** if *at least one* condition is True
* `or` is **False** if *all* conditions are False

Sometimes you may want to check several conditions in sequence:

~~~
data_list_2 = [-12.23, 0, 0, 48.16, 48.21, 48.94, 0, 47.59]
correct_data = []
for number in data_list_2:
    if number < 0:
        print('data point is negative, discarding!')
    elif number == 0:
        print('data point is missing or zero!')
    else:
        correct_data.append(number)
data_average = sum(correct_data) / len(correct_data)
print("The number of data points is", len(correct_data))
print("The average of the points is", data_average)
~~~
{: .language-python}
~~~
data point is negative, discarding!
data point is missing or zero!
data point is missing or zero!
data point is missing or zero!
The number of data points is 4
The average of the points is 48.225
~~~
{: .output}



>## Exercise
>
> The following list contains some floating point numbers and some numbers which  have been saved as strings.  Copy this list exactly into your code.
> ~~~
> data_list = ['-12.5', 14.4, 8.1, '42']
> ~~~
> {: .language-python}
> Set up a `for` loop to go over each element of `data_list`.  If the element is a string (`str`), recast it as a float.  Save *all* of the numbers to a new list called `number_list`.  Pay close attention to your indentation!
>
>> ## Solution
>> ~~~
>> data_list = ['-12.5', 14.4, 8.1, '42']
>> number_list = []
>> for item in data_list:
>>     if type(item) is str:
>>         item = float(item)
>>     number_list.append(item)
>>
>> print(number_list)
>> ~~~
>> {: .output}
> {: .solution}
{: .challenge}




## Working with files
One of the most common tasks in research is analyzing data.  Many computational chemistry programs output text files that include a large amount of information including text and data that you need to analyze.  Often, you need to sort through the output file and identify particular pieces of information that are most important to you.  In general, this is called file parsing.

### Working with file paths - the `os.path` module
For this section, we will be working with the file `ethanol.out` in the `outfiles` directory.

To see this, go to a new cell and type `ls`. `ls` stands for 'list', and will list all of the contents of the current directory. **This command is not a Python command, but will work in the Jupyter notebook**. To see everything in the `data` directory, type

~~~
ls data
~~~

You should see something like
~~~
2_h2o.xyz caffeine.xyz CuOH.cif distance_data_headers.csv water.xyz
~~~
{: .output}


In order to parse a file, you must tell Python the location of the file, or the "file path". For example, you can see what folder your Jupyter notebook is in by typing `pwd` into a cell in your notebook and evaluating it. `pwd` stands for 'print working directory', and can also be used in your terminal to see what directory you're in.

After evaluating the cell with `pwd`, you should see an output similar to the following if you are on Mac or Linux:
~~~
'/Users/YOUR_USER_NAME/ProfDev_python'
~~~
{: .output}

or similar to this if you are on Windows
~~~
'C:\Users\YOU_USER_NAME\Desktop\ProfDev-python'
~~~
{: .output}

Notice that the file paths are different for these two systems. The Windows system uses a backslash ('\\'), while Mac and Linux use a forward slash ('/') for filepaths.

When we write a script, we want it to be usable on any operating system, thus we will use a python module called `os.path` that will allow us to define file paths in a general way.

In order to get the path to the `tree-rings.txt` file in a general way, type
~~~
import os

data_file = os.path.join('data', 'CuOH.cif')
print(data_file)
~~~
{: .python}

You should see something similar to the following
~~~
data/CuOH.cif
~~~
{:. .output}

Here, we have specified that our filepath contains the 'data' directory, and the `os.path` module has made this into a filepath that is usable by our system. If you are on Windows, you will instead see that a backslash is used.

> ## Absolute and relative paths
> File paths can be *absolute*, or *relative*.
>
> A relative file path gives the location relative to the directory we are in. Thus, if we are in the `ProfDev-python` directory, the relative filepath for the `tree-rings.txt` file would be `data/tree-rings.txt`
>
> An absolute filepath gives the complete path to a file. This file path could be used from anywhere on a computer, and would access the same file. For example, the absolute filepath to the  `tree-rings.txt` file on a Mac might be `Users/YOUR_USER_NAME/Desktop/ProfDev-python/data/tree-rings.txt`. You can get the absolute path of a file using `os.path.abspath(path)`, where path is the relative path of the file.
{: .callout}

> ## Python `pathlib`
> We are working with the `os.path` module here, and this is how you will see people handle file paths in most Python code. However, as of Python 3.6, there is also a `pathlib` module in the Python standard library that can be used to represent and manipulate filepaths. `os.path` works with filepaths as strings, while in the `pathlib` module, paths are objects. A good overview of the pathlib module can be found [here](https://realpython.com/python-pathlib/).
{: .callout}

## Reading a file

In Python, there are many ways in python to read in information from a text file.  The best method to use depends on the type of data and the type of analysis you are performing.  If you have a file with lots of different types of information, text and numbers, with different types of formatting, the most generic way to read in information is the `readlines()` function.  Before you can read in a file, you have to open the file using the file path we defined above. This will create a file object, or filehandle.  The file we will be analyzing in this example is a Crystallographic Information File.

```
outfile = open(data_file,"r")
data = outfile.readlines()
```
{: .language-python}
This code opens a file for reading and assigns it to the filehandle  `outfile`. The `r` argument in the function stands for `read`. Other arguments might be `w` for `write` if we want to write new information to the file, or `a` for append if we want to add new information at the end of the file.

In the next line, we use the `readlines` function to get our file as a list of strings.  Notice the dot notation introduced last lesson; readlines acts on the file object given right before the dot.  The function creates a list called data where each element of the list is a string that is one line of the file.  This is always how the
`readlines()` function works.

> ## `readlines` function behavior
> Note that the `readlines` function can only be used on a file object one time. If you forget to set `outfile.readlines()` equal to a variable, you must `open` the file again in order to get the contents of the file.
{: .callout}

After you open and read information from a file object, you should always close the file.

~~~
outfile.close()
~~~
{: .language-python}

> ## An alternative way to open a file.
> Alternatively, you can open a file using `context-manager`. In this case, the context manager will automatically handle closing of the file. To use a context manager to open and close the file, you use the word `with`, and put everything you want to be done while the file is open in an indented block.
> ~~~
> with open(data_file,"r") as outfile:
>     data = outfile.readlines()
> ~~~
> {: .language-python}
>
> This is often the preferred way to deal with files because you do not have to remember to close the file.
{: .callout}


> ## Check Your Understanding
> Check that your file was read in correctly by determining how many lines are in the file.
>> ## Answer
>> ~~~
>> print(len(data))
>> ~~~
>> {: .language-python}
>> ~~~
>> 105
>> ~~~
>> {: .output}
> {: .solution}
{: .challenge}

## Searching for a pattern in your file
The file we opened is crystallographic information file for copper hydroxide, Cu(OH)2, which contains (amongst other things) the size of the unit cell. As stated previously, the `readlines()` function put the file contents into a list where each element is a line of the file. Earlier, we learnt that `for` loops can be used to execute the same code repeatedly. We can use a for loop to iterate through elements in a list.

Let's take a look at what's in the file.

~~~
for line in data:
    print(line)
~~~
{: .language-python}

This will print exactly what is in the file.

If you look through the output, you will see that there are three lines that give the unit cell dimensions. The lines begin with "_cell_length_a", "_cell_length_b" and "_cell_length_c". We want to search through this file and find those three lines, and print only those lines. We can do this using an `if` statement.

Returning to our file example,

```
for line in data:
    if '_cell_length_a' in line:
        cell_dimension_a_line = line
        print(cell_dimension_a_line)
```
{: .language-python}

```
_cell_length_a     2.947
```
{: .output}

Remember that `readlines()` saves each line of the file as a string, so `line` is a string that contains the whole line.  For our analysis, we are only interested in the cell dimension (which is in Angstrom), we need to split up the line so we can save just the number as a different variable name. To do this, we use a new function called `split`.  The `split` function takes a string and divides it into its components using a *delimiter*.

The *delimiter* is specified as an argument to the function (put in the parenthesis `()`). If you do not specify a delimiter, a space is used by default. Let's try this out.

~~~
cell_dimension_a_line.split()
~~~
{: .language-python}

~~~
['_cell_length_a', '2.947']
~~~
{: .language-output}

Or, we can use the underscore ('_') as the delimiter.

~~~
cell_dimension_a_line.split('_')
~~~
{: .language-python}


~~~
['', 'cell', 'length', 'a     2.947\n']
~~~
{: .language-output}

When we use '_' as the delimiter, a list with four elements is returned. It is split where an underscore was found. Because the first character in the string was an underscore, the first list element is empty. This split is less useful to us than the default split.

We can save the output of this function to a variable as a new list. In the example below, we take the line we found in the `for` loop and split it up into its individual words.

```
words = cell_dimension_a_line.split()
print(words)
```
{: .language-python}

```
['_cell_length_a', '2.947']
```
{: .output}

From this `print` statement, we now see that we have a list called words, where we have split `_cell_dimension_a_line`.  The cell dimension is the second element of this list, so we can now save it as a new variable.

```python
cell_a = words[1]
print(cell_a)
```
{: .language-python}

> ## Python negative indexing
> We also recogize that "cell_a" is the last element of the list. Therefore, an alternative way to assign `cell_a` is:
> ```python
> cell_a = words[-1]
> print(cell_a)
> ```
>
> In the example above,  the index value of `-1` gives the last element, and `-2` would give the second last element of a list, and so on. An excelent tutorial on Python list accessed by index can be found [here](https://realpython.com/python-lists-tuples/#list-elements-can-be-accessed-by-index)
{: .callout}



```
2.947
```
{: .output}

If we now try to do a math operation on cell_a, we get an error message?  Why do you think that is?
```
cell_a + 50
```
{: .language-python}
```
TypeError                                 Traceback (most recent call last)
<ipython-input-59-76bf387f977e> in <module>
----> 1 cell_a + 50

TypeError: must be str, not int
```
{: .error}
Even though `cell_a` looks like a number to us, it is really a string, so we can not add an integer to it.  We need to change the data type of cell_a to a float. This is called *casting*.

```
cell_a = float(cell_a)
```
{: .language-python}

Now it will work.  If we thought ahead we could have changed the data type when we assigned the variable originally.

```
cell_a = float(words[1])
```
{: .language-python}

>## Exercise on File Parsing
Use the provided CuOH.cif file. As previously stated, the file contains all three cell dimensions (*a*,*b* nd *c). Extract all three cell parameters (in Angstrom) from the file and calculate the cell volume, **V = abc**  Your code's output should look something like this:
> ~~~
>_cell_length_a     2.947
>_cell_length_b    10.593
>_cell_length_c     5.256
> Cell volume = 164.079553176 A^3
> ~~~
> {: language.python}
>
> > ## Solution
>>
>> This is one possible solution for the parsing exercise
>> ~~~
>>#Find the lines we need
>>with open('CuOH.cif',"r") as outfile:
>>    for line in outfile:
>>        if '_cell_length' in line:
>>            print(line)
>>            cell_dimension_lines.append(line)
>># Now split the numbers from the text and cast them to floats
>>cell_dimensions = []
>>for cdim in cell_dimension_lines:
>>    this_dimension = float(cdim.split()[-1])
>>    cell_dimensions.append(this_dimension)
>>print ('Cell volume = ',cell_dimensions[0]*cell_dimensions[1]*cell_dimensions[2], 'A^3')
>> ~~~
>> {: .language-python}
> {: .solution}
{: .challenge}

## Searching for a particular line number in your file
There is a lot of other information in the file we might be interested in.  For example, we might want to find the original paper where the structure was published. If we look through the file in a text editor, can find a line that reads:

_journal_paper_doi


and then the DOI (Digital Object Identifier) is written two lines later.  In this case, we don't want to pull something out of this line, as we did in our previous example, but we want to know which line of the file this is so that we can then pull the DOI from the line two lines later.  

When you use a for loop, it is easy to have python keep up with the line numbers using the `enumerate` command.  The general syntax is
```
for linenum, line in enumerate(list_name):
    do things in the loop
```
{: .language-python}

In this notation, there are now *two* variables you can use in your loop commands, `linenum` (which can be named something else) will keep up with what iteration you are on in the loop, in this case what line you are on in the file. The variable `line` (which could be named something else) functions exactly as it did before, holding the actual information from the list.  Finally, instead of just giving the list name you use `enumerate(list_name)`.  

> ## `Enumerate` with index other than 0:
> `enumerate(list_name)` will start with 0-index so the first line will be label as '0', to change this behavior, use `start` variable in enumerate. For example, to start with index of "1" you can do:
> ```python
> for linenum, line in enumerate(data, start=1):
>   # do something with 'linenum' and 'line'
{: .callout}

This block of code searches our file for the line that contains "_journal_paper_doi" and reports the line number.
```
for linenum, line in enumerate(data):
    if '_journal_paper_doi' in line:
        print(linenum)
        print(line)
```
{: .language-python}
```
53
_journal_paper_doi
```
{: .output}
Now we know that this is line 53 in our file (remember that you start counting at zero!). 

>## Check Your Understanding
>What would be printed if you entered the following:
>~~~
> print(data[52])
> print(data[53])
> print(data[54])
> print(data[55])
> print(data[56])
> ~~~
>{: .language.python}
>
>> ## Answer
>>
>> It prints line 52-56 of the list `data` which is the line that contains "_journal_paper_doi" (line 53), the line before it (line 52) and the three lines after it. Line 55 is the one that contains the DOI.  
>> ~~~
>>_cell_formula_units_Z 4
>>
>>_journal_paper_doi
>>
>>;
>>
>>10.1107/S0108270190006230
>>
>>;
>> ~~~
>> {: .output}
> {: .solution}
{: .challenge}

## A final note about regular expressions
Sometimes you will need to match something more complex than just a particular word or phrase in your output file.  Sometimes you will need to match a particular word, but only if it is found at the beginning of a line.  Or perhaps you will need to match a particular pattern of data, like a capital letter followed by a number, but you won't know the exact letter and number you are looking for.  These types of matching situations are handled with something called *regular expressions* which is accessed through the python module `re`.  While using regular expressions (regex) is outside the scope of this tutorial, they are very useful and you might want to learn more about them in the future.  A tutorial can be found at [Automate the Boring Stuff with Python](https://automatetheboringstuff.com/2e/chapter7/) book.  A great test site for regex is [here](https://regex101.com/)

{% include links.md %}
