---
title: "Processing Multiple Files and Writing Files"
teaching: 25
exercises: 10
questions:
- "How do I analyze multiple files at once?"
objectives:
- "Import a python library."
- "Use python library funtions."
- "Process multiple files using a `for` loop."
- "Print output to a new text file."
keypoints:
- "Use the glob function in the python library glob to find all the files you want to analyze."
- "You can have multiple `for` loops nested inside each other."
- "Python can only print strings to files."
- "Don't forget to close files so python will actually write them."
---
## Processing multiple files

In our previous lesson, we parsed values from output files.  While you might have seen the utility of doing such a thing, you might have also wondered why we didn't just search the file and cut and paste the values we wanted into a spreadsheet.  If you only have 1 or 2 files, this might be a very reasonable thing to do.  But what if you had 100 files to analyze?  What if you had 1000?  In such a case the cutting and pasting method would be very tedious and time consuming.  

One of the real powers of writing a program to analyze your data is that you can just as easily analyze 100 files as 1 file.  In this example, we are going to parse the cif files for a whole series of structures and parse the cell parameters and calculate the cell volume for each one.  The cif files are all saved in a folder called orthorhombic that you should have downloaded in the setup for this lesson.  Make sure the folder is in the same directory as the directory where you are writing and executing your code.

To analyze multiple files, we will need to import a python **library**.  A **library** is a set of modules which contain functions. The functions within a library or module are usually related to one another. Using libraries and in Python reduces the amount of code you have to write. In the last lesson, we imported `os.path`, which was a module that handled filepaths for us.

In this lesson, we will be using the `glob` library, which will help us read in multiple files from our computer.  Within a library there are  modules and functions which do a specific computational task.  Usually a function has some type of input and gives a particular output.  To use a function that is in a library, you often use the dot notation introduced in the previous lesson.  In general
```
import library_name
output = library_name.funtion_name(input)
```
{: .language-python}

We are going to import two libraries.  One is the `os` library which controls functions related to the operating system of your computer. We used this library in the last lesson to handle filepaths.  The other is the `glob` library which contains functions to help us analyze multiple files.  If we are going to analyze multiple files, we first need to specify where those files are located.

>## Exercise
>
> How would you use the `os.path` module to point to the directory where your cif files are?
>
>> ## Solution
>> ~~~
>> outfile_directory = os.path.join('structures', 'orthorhombic')
>> ~~~
>> {: .language-python}
> {: .solution}
{: .challenge}

In order to get all of the files which match a specific pattern, we will use the wildcard character `*`.

```
file_location = os.path.join('structures', 'orthorhombic', '*.cif')
print(file_location)
```
{: .language-python}
```
structures/orthorhombic/*.cif
```
{: .output}

This specifies that we want to look for all the files in a directory called `structures/orthorhombic` that end in ".cif".  The * is the wildcard character which matches any number of any character.  

Next we are going to use a function called `glob` in the library called `glob`.  It is a little confusing since the function and the library have the same name, but we will see other examples where this is not the case later.  The output of the function `glob` is a list of all the filenames that fit the pattern specified in the input.   The input is the file location.
```
import glob
filenames = glob.glob(file_location)
print(filenames)
```
{: .language-python}
```
['structures/orthorhombic/spacegroup_74.cif', 'structures/orthorhombic/spacegroup_72.cif', 'structures/orthorhombic/spacegroup_70.cif', 'structures/orthorhombic/spacegroup_68.cif', 'structures/orthorhombic/spacegroup_66.cif', 'structures/orthorhombic/spacegroup_64.cif', 'structures/orthorhombic/spacegroup_62.cif', 'structures/orthorhombic/spacegroup_73.cif', 'structures/orthorhombic/spacegroup_71.cif', 'structures/orthorhombic/spacegroup_69.cif', 'structures/orthorhombic/spacegroup_67.cif', 'structures/orthorhombic/spacegroup_65.cif', 'structures/orthorhombic/spacegroup_63.cif', 'structures/orthorhombic/spacegroup_61.cif', 'structures/orthorhombic/spacegroup_60.cif', 'structures/orthorhombic/spacegroup_59.cif', 'structures/orthorhombic/spacegroup_58.cif', 'structures/orthorhombic/spacegroup_57.cif', 'structures/orthorhombic/spacegroup_56.cif', 'structures/orthorhombic/spacegroup_55.cif', 'structures/orthorhombic/spacegroup_54.cif', 'structures/orthorhombic/spacegroup_53.cif', 'structures/orthorhombic/spacegroup_52.cif', 'structures/orthorhombic/spacegroup_51.cif', 'structures/orthorhombic/spacegroup_50.cif', 'structures/orthorhombic/spacegroup_49.cif', 'structures/orthorhombic/spacegroup_48.cif', 'structures/orthorhombic/spacegroup_47.cif', 'structures/orthorhombic/spacegroup_46.cif', 'structures/orthorhombic/spacegroup_45.cif', 'structures/orthorhombic/spacegroup_44.cif', 'structures/orthorhombic/spacegroup_43.cif', 'structures/orthorhombic/spacegroup_42.cif', 'structures/orthorhombic/spacegroup_41.cif', 'structures/orthorhombic/spacegroup_40.cif', 'structures/orthorhombic/spacegroup_39.cif', 'structures/orthorhombic/spacegroup_38.cif', 'structures/orthorhombic/spacegroup_37.cif', 'structures/orthorhombic/spacegroup_36.cif', 'structures/orthorhombic/spacegroup_35.cif', 'structures/orthorhombic/spacegroup_34.cif', 'structures/orthorhombic/spacegroup_33.cif', 'structures/orthorhombic/spacegroup_32.cif', 'structures/orthorhombic/spacegroup_31.cif', 'structures/orthorhombic/spacegroup_30.cif', 'structures/orthorhombic/spacegroup_29.cif', 'structures/orthorhombic/spacegroup_28.cif', 'structures/orthorhombic/spacegroup_27.cif', 'structures/orthorhombic/spacegroup_26.cif', 'structures/orthorhombic/spacegroup_25.cif', 'structures/orthorhombic/spacegroup_24.cif', 'structures/orthorhombic/spacegroup_23.cif', 'structures/orthorhombic/spacegroup_22.cif', 'structures/orthorhombic/spacegroup_21.cif', 'structures/orthorhombic/spacegroup_20.cif', 'structures/orthorhombic/spacegroup_19.cif', 'structures/orthorhombic/spacegroup_18.cif', 'structures/orthorhombic/spacegroup_17.cif', 'structures/orthorhombic/spacegroup_16.cif']
```
{: .output}

This will give us a list of all the files which end in `*.cif` in the `orthorhombic` directory. Now if we want to parse every file we just read in, we will use a `for` loop to go through each file.
```
for f in filenames:
    ciffile = open(f,'r')
    data = ciffile.readlines()
    ciffile.close()
    for line in data:
        if '_cell_length_a' in line:
            cell_dimension_a_line = line
            words = cell_dimension_a_line.split()
            cell_a = float(words[1])
            print(cell_a)
```
{: .language-python}

```
7.06
9.005
9.829
13.714
17.083
...
...
...
9.336
10.44
10.331
16.912
8.806
```
{: .output}

There are many more lines in the output (**How many?**), but the output has been abbreviated here using "...". Notice that in this code we actually used two `for` loops, one nested inside the other.  The outer `for` loop counts over the filenames we read in earlier.  The inner `for` loop counts over the line in each file, just as we did in our previous file parsing lesson.  

The output our code currently generates is not that useful.  It doesn't show us which file each cell dimension value came from and it only grabs the *a* dimension, not the *b* and *c*.  

We want to print the name of the file with the cell dimension. We can use `os.path.basename`, which is another function in `os.path` to get just the name of the file.

~~~
first_file = filenames[0]
print(first_file)

file_name = os.path.basename(first_file)
print(file_name)
~~~
{: .language-python}

~~~
structures/orthorhombic/spacegroup_74.cif
spacegroup_74.cif
~~~
{: .output}

> ## Exercise
>
> How would you extract the file name (without the extension) from the example above?
>
>> ## Solution
>> You can use the `str.split` function introduced in the last lesson, and split at the '.' character.
>> ~~~
>> split_filename = file_name.split('.')
>> file_name = split_filename[0]
>> print(file_name)
>> ~~~
>> {: .language-python}
> {: .solution}
{: .challenge}

Using the solution above, we can modify our loop so that it prints the file name along with the *a* cell dimension.

~~~
for f in filenames:
    # Get the molecule name
    file_name = os.path.basename(f)
    split_filname = file_name.split('.')
    molecule_name = split_filename[0]

    # Read the data
    outfile = open(f,'r')
    data = outfile.readlines()
    outfile.close()

    # Loop through the data
    for line in data:
        if '_cell_length_a' in line:
            cell_dimension_a_line = line
            words = cell_dimension_a_line.split()
            cell_a = float(words[1])
            print(molecule_name, cell_a)
~~~
{: .language-python}

~~~
spacegroup_74 7.06
spacegroup_73 11.712
spacegroup_72 9.005
spacegroup_71 2.559
spacegroup_70 9.829
spacegroup_69 5.459
...
...
...
spacegroup_21 9.336
spacegroup_20 10.44
spacegroup_19 10.331
spacegroup_18 16.912
spacegroup_17 8.806
~~~
{: .output}


## Printing to a File
Finally, it might be useful to print our results in a new file, such that we could share our results with colleagues or or e-mail them to our advisor.  Much like when we read in a file, the first step to writing output to a file is opening that file for writing.  In general to open a file for writing you use the syntax
```
filehandle = open('file_name.txt', 'w+')
```
{: .language-python}

The `w` means open the file for writing.  If you use `w+` that means open the file for writing and if the file does not exist, create it.  You can also use `a` for append to an existing file or `a+`.  The difference between `w+` and `a+` is that `w+` will overwrite the file if it already exists, whereas `a+` will keep what is already there and just add additional text to the file.  

Python can only write strings to files.  Our current print statement is not a string; it prints two python variables.  To convert what we have now to a string, you place a capital **F** in front of the line you want to print and enclose it in single quotes.  Each python variable is placed in braces. Then you can either print the line (as we have done before) or you can use the `filehandle.write()` command to print it to a file.

To make the printing neater, we will separate the file name from the energy using a tab. To insert a tab, we use the special character `\t`.

```
datafile = open('cell_dimensions.txt','w+')  #This opens the file for writing
for f in filenames:
    # Get the molecule name
    file_name = os.path.basename(f)
    split_filename = file_name.split('.')
    molecule_name = split_filename[0]

    # Read the data
    outfile = open(f,'r')
    data = outfile.readlines()
    outfile.close()

    # Loop through the data
    for line in data:
        if '_cell_length_a' in line:
            cell_dimension_a_line = line
            words = cell_dimension_a_line.split()
            cell_a = float(words[1])
            datafile.write(F'{molecule_name} \t  {cell_a} \n')
datafile.close()
```
{: .language-python}

After you run this command, look in the directory where you ran your code and find the "cell_dimensions.txt" file.  Open it in a text editor and look at the file.

In the file writing line, notice the `\n` at the end of the line.  This is the newline character.  Without it, the text in our file would just be all smushed together on one line.  Also, the `filehandle.close()` command is very important.  Think about a computer as someone who has a very good memory, but is very slow at writing.  Therefore, when you tell the computer to write a line, it remembers what you want it to write, but it doesn't actually write the new file until you tell it you are finished.   The `datafile.close()` command tells the computer you are finished giving it lines to write and that it should go ahead and write the file now.  If you are trying to write a file and the file keeps coming up empty, it is probably because you forgot to close the file. Also remember that once you close the filehandle, it no longer exists within your python environment, so if you try to write to it after you've closed it, you'll get an error. 

## A final note about string formatting
The F'string' notation that you can use with the print or the write command lets you format strings in many ways.  You could include other words or whole sentences.  For example, we could change the file writing line to
```
datafile.write(F'For the file {molecule_name} the a cell dimension is {cell_a} in Angstrom.')
```
{: .language-python}
where anything in the braces is a python variable and it will print the value of that variable.  

## Mini Assignment
Now we can bring together the things we've learnt in the last two episodes:

> ## File parsing exercise
> Above, we only extracted the *a* cell dimension and we used the name of the file as the molecule name. Extend your script above to extract the actual chemical name from the file, as well as the *a*, *b* and *c* cell dimensions. Print the filename, molecule name and the three cell dimensions to a file called "orthorhombic_cell_data.txt".When you open it, it should look like this: 
>
> ~~~
> Molecule Filename      Molecule Name   cell_a      cell_b      cell_c
> spacegroup_74    Disodium magnesium aluminium fluoride   7.06    10.0    7.303
> spacegroup_73    Disodium dihydroxodioxosilicate octahydrate     11.712      16.973      11.565
> spacegroup_72    Lead tricopper bis(vanadate) dichloride     9.005   11.046      9.349
> spacegroup_71    Nickel vanadium (2/1)   2.559   7.641   3.549
> spacegroup_70    Disodium sulfate(VI)    9.829   12.302      5.868
> ...
> ~~~
>
> `...` indicates that you will have many more rows. We've only shown the first 5 here.
>
> If you are unsure of where to start with this assignment, check the hint section! Also look back at your notebooks for the last episode where we extracted some of this information. You should be able to re-use bits of code that you've already written.
>
>> ## Hints
>> It helps when you are writing code to break up what you have to do into steps. Overall, we want to get four pieces of information (chemical name, and three cell dimsions) from each file. How do we do that?
>>
>> If you think about the steps you will need to do this assignment you might come up with a list like:
>>
>> 1. Make a list of all the cif files to read
>> 2. Read the data in each file
>> 3. Loop through the lines in the file.
>> 4. Get the information from the four lines we are interested in. 
>> 4a. The chemical name is not on the same line as the thing we search for
>> 4b. Each of the three cell parameters can be read from the same line as the thing we search for
>> 5. Write the information to a file.
>>
>> It can be helpful when you code to write out these steps and work on it in pieces. Try to write the code using these steps. Note that as you write the code, you may come up with other steps! First, thing about what you have to do for step 1, and write the code for that. Next, think about how you would do step 2 and write the code for that. You can troubleshoot each step using print statments. The steps build on each other, so you can work on getting each piece written before moving on to the next step.
> {: .solution}
>
>> ## Solution
>> The following is one potential solution, though you may have come up with another. Just make sure that your text file looks like the solution given in the problem statememt.
>>
>> This solution will walk through writing the code step-by-step. If you do not wish to walk through step-by-step, simply skip to the end of the solution.
>>
>> Let's start with the steps we thought of in the hint to write this code in pieces.
>>
>> ~~~
>> # Make a list of all the cif files to read
>>
>> # Read the data in each file
>>
>> # Get the information from the four lines we are interested in. 
>>     # Loop through the lines in the data
>>     # The chemical name is not on the same line as the thing we search for
>>     # Each of the three cell parameters can be read from the same line as the thing we search for
>>
>> # Write the information to a file.
>> ~~~
>> {: .language-python}
>>
>> For part one, you will realize that you need to build a file path and then glob all the files in that file path. To do that, out code looks like this: 
>>
>> ~~~
>> import os
>> import glob
>>
>> # Make a list of all the cif files to read
>> # Build the filepath and glob
>> file_location = os.path.join('structures', 'orthorhombic', '*.cif') #*
>> filenames = glob.glob(file_location)
>>
>> # Read the data in each file
>>
>>
>> # Get the information from the four lines we are interested in. 
>> # The chemical name is not on the same line as the thing we search for
>> # Each of the three cell parameters can be read from the same line as the thing we search for
>>
>> # Write the information to a file.
>> ~~~
>> {: .language-python}
>>
>> This code will not appear to do anything, but it builds a filepath, and globs the all the files in that path. To check that everything does what you want it to, you could add some print statements. 
>>
>> Our second step is reading the data from each cif file. We did this earlier in a for loop using a function called `readlines`. Recall from `readlines` that the file will need to be open to do this, so need to open each file in the loop and then close it after we have read the data from the file. 
>>
>> ~~~
>> import os
>> import glob
>>
>> # Make a list of all the cif files to read
>> # Build the filepath and glob
>> file_location = os.path.join('structures', 'orthorhombic', '*.cif') #*
>> filenames = glob.glob(file_location)
>>
>> # Read the data in each file
>> for f in filenames:
>>     # Get the file name of the individual file
>>     file_name = os.path.basename(f)
>>     split_filename = file_name.split('.')
>>     molecule_file_name = split_filename[0]
>>     molecule_file_names.append(molecule_file_name)
>> 
>>     # Read the data
>>     ciffile = open(f,'r')
>>     data = ciffile.readlines()
>>     ciffile.close()
>>
>>
>> # Get the information from the four lines we are interested in. 
>>     # Loop through the lines in the data
>>     # The chemical name is not on the same line as the thing we search for
>>     # Each of the three cell parameters can be read from the same line as the thing we search for
>>
>> # Write the information to a file.
>> ~~~
>> {: .language-python}
>>
>> We know that readlines gives us a list where every line is an element of a list. We need to loop through the lines in the file, and we will do this using a second `for` loop.
>>
>> ~~~
>> import os
>> import glob
>>
>> # Make a list of all the cif files to read
>> # Build the filepath and glob
>> file_location = os.path.join('structures', 'orthorhombic', '*.cif') #*
>> filenames = glob.glob(file_location)
>>
>> # Read the data in each file
>> for f in filenames:
>>     # Get the file name of the individual file
>>     file_name = os.path.basename(f)
>>     split_filename = file_name.split('.')
>>     molecule_file_name = split_filename[0]
>>     molecule_file_names.append(molecule_file_name)
>> 
>>     # Read the data
>>     ciffile = open(f,'r')
>>     data = ciffile.readlines()
>>     ciffile.close()
>>
>> # Get the information from the four lines we are interested in. 
>>     # Loop through the lines in the data
>>     for linenum, line in enumerate(data):
>>         # The chemical name is not on the same line as the thing we search for
>>         if '_chemical_name_systematic' in line:
>>                 name_line = linenum + 2
>>                 molecule_name = data[name_line].rstrip('\n') #We use rstrip() to remove the newline character
>>         # Each of the three cell parameters can be read from the same line as the thing we search for
>>         if '_cell_length_a' in line:
>>             cell_dimension_a_line = line
>>             words = cell_dimension_a_line.split()
>>             cell_a = float(words[1])
>>         elif '_cell_length_b' in line:
>>             cell_dimension_b_line = line
>>             words = cell_dimension_b_line.split()
>>             cell_b = float(words[1])
>>         elif '_cell_length_c' in line:
>>             cell_dimension_c_line = line
>>             words = cell_dimension_c_line.split()
>>             cell_c = float(words[1])
>>
>> # Write the information to a file.
>> ~~~
>> {: .language-python}
>>
>> Now all that is left to do is to write this information to a file. We will need to open the file before the loop, write to it inside the loop, and finally close it outside of the loop. Our final code is:
>>
>> ~~~
>> import os
>> import glob
>>
>> # Make a list of all the cif files to read
>> # Build the filepath and glob
>> file_location = os.path.join('structures', 'orthorhombic', '*.cif') #*
>> filenames = glob.glob(file_location)
>>
>> # Read the data in each file
>> for f in filenames:
>>     # Get the file name of the individual file
>>     file_name = os.path.basename(f)
>>     split_filename = file_name.split('.')
>>     molecule_file_name = split_filename[0]
>>     molecule_file_names.append(molecule_file_name)
>> 
>>     # Read the data
>>     ciffile = open(f,'r')
>>     data = ciffile.readlines()
>>     ciffile.close()
>>
>> # Get the information from the four lines we are interested in. 
>>     # Loop through the lines in the data
>>     for linenum, line in enumerate(data):
>>         # The chemical name is not on the same line as the thing we search for
>>         if '_chemical_name_systematic' in line:
>>                 name_line = linenum + 2
>>                 molecule_name = data[name_line].rstrip('\n') #We use rstrip() to remove the newline character
>>         # Each of the three cell parameters can be read from the same line as the thing we search for
>>         if '_cell_length_a' in line:
>>             cell_dimension_a_line = line
>>             words = cell_dimension_a_line.split()
>>             cell_a = float(words[1])
>>         elif '_cell_length_b' in line:
>>             cell_dimension_b_line = line
>>             words = cell_dimension_b_line.split()
>>             cell_b = float(words[1])
>>         elif '_cell_length_c' in line:
>>             cell_dimension_c_line = line
>>             words = cell_dimension_c_line.split()
>>             cell_c = float(words[1])
>>
>>     # Write the information to a file.
>>     datafile.write(F'{molecule_file_name} \t {molecule_name} \t {cell_a} \t {cell_b} \t {cell_c}\n')
>>        
>>datafile.close()
>> ~~~
>> {: .language-python}
> {: .solution}
{: .challenge}

{% include links.md %}
