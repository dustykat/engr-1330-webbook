<!-- Script Block to set tables to left alignment -->
<style>
  table {margin-left: 0 !important;}
</style>



### Example 1 Problem Solving Process - Compute Arithmetic Mean

This example considers a need to compute an arithmetic mean, and what the process might look like.  The example goes through the steps involved, and even includes some JupyterLab/iPython scripting; students are not expected to understand the code syntax at this point, but it is included to illustrate an end result of the simple directive to compute a mean value.  

### Step 1. Problem Statement
Develop script to compute the arithmetic mean of a stream of data of unknown length.

### Step 2. Identify inputs, outputs, governing principles

For this example these are straightforward enough to simply itemize:

  - Inputs: The data stream 
  - Governing equation: $ \bar x = \frac{1}{N} \sum_{i=1}^{N} x_i $ where $N$ is the number of items in the data stream, and $x_i$ is the value of the i-th element.
  - Outputs: The arithmetic mean $\bar x$

### Step 3. Create a sample problem 
Create a sample problem suitable for "by-hand" execution for testing the general solution.

|Data|
|:---|
|23.43|
|37.43|
|34.91|
|28.37|
|30.62|

The arithmetic mean requires us to count how many elements are in the data stream (in this case there are 5) and compute their sum (in this case 154.76), and finally divide the sum by the count and report this result as the arithmetic mean.

$$ \bar x = \frac{1}{5}(23.43+37.43+34.91+28.37+30.62)=\frac{154.76}{5}=30.95 $$

### Step 4 Develop a general solution (Algorithm)

Here is where we create an algorithm. 
The by-hand exercise helps identify the required steps in an “algorithm” or recipe to compute mean values. First we essentially capture or read the values then count how many there are (either as we go or as a separate step), then sum the values, then divide the values by the count, and finally report the result.

In a flow-chart it would look like:

![](Lesson1-flowchart.png)

||Flowchart for Artihmetic Mean Algorithm||
|---|------------|---|

### Step 5. Generalization (Algorithm into Code)

Convert the algorithm expressed in the above into running code and test it with the "by-hand" example,  and other small datasets until we are convinced it works correctly.

In a simple JupyterLab script


```python
# Arithmetic Mean in Very Elementary and Primative Python
xlist = [23.43,37.43,34.91,28.37,30.62] # list is a type of data structure
howlong = len(xlist) # len is a built-in function that returns how many items in a list
accumulator = 0 # a variable to accumulate the sum
for i in range(howlong):
    accumulator = accumulator + xlist[i]
print("arithmetic mean = ",(accumulator/howlong))
```

    arithmetic mean =  30.951999999999998


### Step 6. Refinement.

This step we would refine the code to generalize the algorithm.  In the example we want a way to supply the `xlist` from a file perhaps, and tidy the output by rounding to only two decimal places - rounding is relatively simple:


```python
# Arithmetic Mean in Very Elementary and Primative Python
xlist = [23.43,37.43,34.91,28.37,30.62] # list is a type of data structure
howlong = len(xlist) # len is a built-in function that returns how many items in a list
accumulator = 0 # a variable to accumulate the sum
for i in range(howlong):
    accumulator = accumulator + xlist[i]
print("arithmetic mean = ",round((accumulator/howlong),2))
```

    arithmetic mean =  30.95


Reading from a file, is a bit more complicated.  We need to create a connection to the file, then read the contents into our script, then put the contents into the `xlist`


```python
xlist=[] # list (null) is a type of data structure
externalfile = open("data.txt",'r') # create connection to file, set to read (r), file must exist
how_many_lines = 0
for line in externalfile: # parse each line, append to xlist
    xlist.append(line)
    how_many_lines += 1
externalfile.close() # close the file connection

howlong = len(xlist) # len is a built-in function that returns how many items in a list
accumulator = 0 # a variable to accumulate the sum
for i in range(howlong):
    accumulator = accumulator + float(xlist[i])
print("arithmetic mean = ",round((accumulator/howlong),2))
```

    arithmetic mean =  30.95


Finally, if we want to reuse the code a lot, it is convienent to make it into a function


```python
def average(inputlist):
# inputlist should be a list of values
    howlong = len(inputlist) # len is a built-in function that returns how many items in a list
    accumulator = 0 # a variable to accumulate the sum
    for i in range(howlong):
        accumulator = accumulator + float(inputlist[i])
    result = (accumulator/howlong)
    return(result)
```

Put our file reading and compute mean code here


```python
xlist=[] # list (null) is a type of data structure
externalfile = open("data.txt",'r') # create connection to file, set to read (r), file must exist
how_many_lines = 0
for line in externalfile: # parse each line, append to xlist
    xlist.append(line)
    how_many_lines += 1
externalfile.close() # close the file connection
print("arithmetic mean = ",round(average(xlist),2))
```

    arithmetic mean =  30.95


So the simple task of computing the mean of a collection of values, is a bit more complex when decomposed than it first appears, but illustrates a five step process (with a refinement step).  Keep in mind throughout the course this generic process is always going on in the background.


```python

```

