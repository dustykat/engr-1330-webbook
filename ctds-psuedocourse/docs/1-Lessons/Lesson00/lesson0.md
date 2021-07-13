**Download** (right-click, save target as ...) this page as a jupyterlab notebook from:

[https://3.137.111.182/engr-1330-webroot/engr-1330-webbook/ctds-psuedocourse/docs/1-Lessons/Lesson00/lesson0.ipynb](https://3.137.111.182/engr-1330-webroot/engr-1330-webbook/ctds-psuedocourse/docs/1-Lessons/Lesson00/lesson0.ipynb)


## Introduction to Computational Thinking with Data Science: 

Copyright © 2021 Theodore G. Cleveland, Farhang Forghanparast, Dinesh Sundaravadivelu Devarajan, Turgut Batuhan Baturalp (Batu), Tanja Karp, Long Nguyen, and Mona Rizvi. *The contents of this book are licensed for free consumption under the following license:* [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)](https://creativecommons.org/licenses/by-nc-nd/4.0/).

Last GitHub Commit Date: 13 July 2021



```python
%%html
<!-- Script Block to set tables to left alignment -->
<style>
  table {margin-left: 0 !important;}
</style>
```


<!-- Script Block to set tables to left alignment -->
<style>
  table {margin-left: 0 !important;}
</style>



## Computational Thinking Concepts

Computational thinking (CT) refers to the thought processes involved in expressing solutions as computational steps or algorithms that can be carried out by a computer. 

Much of what follows is borrowed from [https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2696102/](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2696102/).

Computational thinking is taking an approach to solving problems, designing systems and understanding human behaviour that draws on concepts fundamental to computing [http://www.cs.cmu.edu/~15110-s13/Wing06-ct.pdf](http://www.cs.cmu.edu/~15110-s13/Wing06-ct.pdf).

Computational thinking is a kind of analytical thinking:

- It shares with mathematical thinking in the general ways in which we might approach solving a problem. 
- It shares with engineering thinking in the general ways in which we might approach designing and evaluating a large, complex system that operates within the constraints of the real world. - It shares with scientific thinking in the general ways in which we might approach understanding computability, intelligence, the mind and human behaviour.

The essence of computational thinking is **abstraction** and **automation**. 
In computing, we abstract notions beyond the physical dimensions of time and space. Our abstractions are extremely general because they are symbolic, where numeric abstractions are just a special case.

### CT Foundations

CT is literally a process for breaking down a problem into smaller parts, looking for patterns in the problems, identifying what kind of information is needed, developing a step-by-step solution, and implementing that solution. 

1. Decomposition
2. Pattern Recognition
3. Abstraction
4. Algorithms
5. System Integration (implementation)

#### Decomposition
Decomposition is the process of taking a complex problem and breaking it into more manageable sub-problems. Examples include:  

- Writing a paper:  
 - Introduction 
 - Body 
 - Conclusion 
 
- Wide-viewed (Panorama) image: 
 - Taking multiple overlapped photos 
 - Stitch them
 
Decomposition often leaves a **framework** of sub-problems that later have to be **assembled (system integration)** to produce a desired solution.
 
#### Pattern Recognition
Refers to finding similarities, or shared characteristics of problems.  Allows a complex problem to become easier to solve. Allows use of same solution method for each occurrence of the pattern. 

Pattern recognition allows use of **automation** to process things - its a fundamental drilled shaft of CT.  It also provides a way to use analogs from old problems to address new situations; it too will require **assembly (system integration)** to produce a desired solution.

#### Abstraction

Determine important characteristics of the problem and ignore characteristics that are not important. Use these characteristics to create a representation of what we are trying to solve. 

Books in an online bookstore

|Important| NOT important| 
|:--------|:-------------|
|title    | Cover color  |
|ISBN     |Author’s hometown| 
|Authors  | ... |
|...      | ... |


#### Algorithms
Step-by-step instructions of how to solve a problem (https://en.wikipedia.org/wiki/Algorithm). 
Identifies what is to be done, and the order in which they should be done.

![https://3.137.111.182/engr-1330-webroot/engr-1330-webbook/ctds-psuedocourse/docs/1-Lessons/Lesson00/algorithm.png](https://3.137.111.182/engr-1330-webroot/engr-1330-webbook/ctds-psuedocourse/docs/1-Lessons/Lesson00/algorithm.png)

||Image from [https://www.newyorker.com/magazine/2021/01/18/whats-wrong-with-the-way-we-work?utm_source=pocket-newtab](https://www.newyorker.com/magazine/2021/01/18/whats-wrong-with-the-way-we-work?utm_source=pocket-newtab)||
|---|------------|---|

An algorithm is a **finite** sequence of defined, instructions, typically to solve a class of problems or to perform a computation. Algorithms are unambiguous and are used as specifications for performing calculations, data processing, automated reasoning, and other tasks. Starting from an initial state and initial input (perhaps empty), the instructions describe a computation that, when executed, proceeds through a finite number of defined successive states, eventually producing "output" and terminating at a final ending state. The transition from one state to the next is not necessarily deterministic; some algorithms, known as randomized algorithms, can incorporate random input.

#### System Integration (implementation)

System integration is the assembly of the parts above into the complete (integrated) solution.  Integration combines parts into a program which is the realization of an algorithm using a syntax that the computer can understand. 

## Data Science and Practice

Data science is leveraging existing data sources, to create new ones as needed in order to extract meaningful information and actionable insights through business domain expertise, effective communication and results interpretation. Data science uses relevant statistical techniques, programming languages, software packages and libraries, and data infrastructure; The insights are used to drive business decisions and take actions intended to achieve business goals. 

Why is this important for engineers? Because engineering is a business! 

A list of typical skills [https://elitedatascience.com/data-science-resources](https://elitedatascience.com/data-science-resources):

- Foundational Skills
    - **Programming and Data Manipulation** 
    - **Statistics and Probability**
- Technical Skills
    - Data Collection
    - SQL
    - **Data Visualization**
    - **Applied Machine Learning**
- Business Skills
    - **Communication**
    - Creativity and Innovation
    - Operations and Strategy
    - Business Analytics
- Supplementary Skills
    - Natural Language Processing
    - Recommendation Systems
    - **Time Series Analysis**
- Practice
    - **Projects**
    - Competitions
    - Problem Solving Challenges



## Programming as a problem solving process
The entire point of this course is to develop problem solving skills and begin using some tools (Statistics, Numerical Methods, Data Science, implemented as JupyterLab/Python programs).

The scientific method [https://en.wikipedia.org/wiki/Scientific_method](https://en.wikipedia.org/wiki/Scientific_method) is one example of an effective problem solving strategy. Stated as a protocol it goes something like:

1. Observation: Formulation of a question
2. Hypothesis: A  conjecture that may explain observed behavior. Falsifiable by an experiment whose outcome conflicts with predictions deduced from the hypothesis
3. Prediction: How the experiment should conclude if hypothesis is correct 
4. Testing: Experimental design, and conduct of the experiment.
5. Analysis: Interpretation of experimental results
 
This protocol can be directly adapted to CT/DS problems as:

1. Define the problem (problem statement)
2. Gather information (identify known and unknown values, and governing equations)
3. Generate and evaluate potential solutions
4. Refine and implement a solution
5. Verify and test the solution.

For actual computational methods the protocol becomes:

1. Explicitly state the problem
2. Gather and state Input information, Governing equations or principles, and the required output information.
3. Work a sample problem by-hand for testing the general solution.
4. Develop a general solution method (coding).
5. Test the general solution against the by-hand example(s), then apply to the real problem.

Oddly enough the first step is the most important and sometimes the most difficult. In a practical problem, step 2 is sometimes difficult because a skilled programmer is needed to translate the governing principles into an algorithm for the general solution (step 4).

### Example 1 Problem Solving Process

Consider a need to compute an arithmetic mean, what would the process look like?

**Step 1.** Develop script to compute the arithmetic mean of a stream of data of unknown length.

**Step 2.** 
  - Inputs: The data stream 
  - Governing equation: $ \bar x = \frac{1}{N} \sum_{i=1}^{N} x_i $ where $N$ is the number of items in the data stream, and $x_i$ is the value of the i-th element.
  - Outputs: The arithmetic mean $\bar x$

**Step 3.** Work a sample problem by-hand for testing the general solution.

|Data|
|---:|
|23.43|
|37.43|
|34.91|
|28.37|
|30.62|

The arithmetic mean requires us to count how many elements are in the data stream (in this case there are 5) and compute their sum (in this case 154.76), and finally divide the sum by the count and report this result as the arithmetic mean.

$$ \bar x = \frac{1}{5}(23.43+37.43+34.91+28.37+30.62)=\frac{154.76}{5}=30.95 $$

**Step 4.** Develop a general solution (code)

The by-hand exercise helps identify the required steps in an “algorithm” or recipe to compute mean values. First we essentially capture or read the values then count how many there are (either as we go or as a separate step), then sum the values, then divide the values by the count, and finally report the result.

In a flow-chart it would look like:

![https://3.137.111.182/engr-1330-webroot/engr-1330-webbook/ctds-psuedocourse/docs/1-Lessons/Lesson00/Lesson1-flowchart.png](https://3.137.111.182/engr-1330-webroot/engr-1330-webbook/ctds-psuedocourse/docs/1-Lessons/Lesson00/Lesson1-flowchart.png)

||Flowchart for Artihmetic Mean Algorithm||
|---|------------|---|

**Step 5.** This step we would code the algorithm expressed in the figure and test it with the by-hand data and other small datasets until we are convinced it works correctly.

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


**Step 6.** This step we would refine the code to generalize the algorithm.  In the example we want a way to supply the `xlist` from a file perhaps, and tidy the output by rounding to only two decimal places - rounding is relatively simple:


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


So the simple task of computing the mean of a collection of values, is a bit more complex when decomposed that it first appears, but illustrates a five step process (with a refinement step).  Throughout the course this process is always in the background.

## CCMR Approach

A lot of the problems we will encounter from a CT/DS perspective have already been solved, or at least analogs have been solved.  It is perfectly acceptable to use prior work for a new set of conditions as long as proper attribution is made.  We call this process CCMR:

1. **Copy:** Find a solution to your problem from some online example:  SourceForge, StackOverflow, GeeksForGeeks, DigitalOcean, etc.
2. **Cite:** Cite the original source.  In general a citation will look like one of the references below, but a URL to the source is sufficient at first.
3. **Modify:** Modify the original cited work for your specific needs.  Note the changes in the code using comment statements.
4. **Run:** Apply the modified code to the problem of interest. 

In cases where we use CCMR we are not so much programming and developing our own work as scaffolding parts [https://en.wikipedia.org/wiki/Scaffold_(programming)](https://en.wikipedia.org/wiki/Scaffold_(programming)) - a legitimate and valuable engineering activity.

## Readings

Computational and Inferential Thinking Ani Adhikari and John DeNero, Computational and Inferential Thinking, The Foundations of Data Science, Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND) Chapter 1 [ https://www.inferentialthinking.com/chapters/01/what-is-data-science.html](https://www.inferentialthinking.com/chapters/01/what-is-data-science.html)
