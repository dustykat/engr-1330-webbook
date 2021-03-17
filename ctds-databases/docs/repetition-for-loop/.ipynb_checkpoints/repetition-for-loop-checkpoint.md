# FOR ... loop
## Count controlled repetition structure
Count-controlled repetition is also called definite repetition because the number of repetitions is known before the loop begins executing. 
When we do not know in advance the number of times we want to execute a statement, count-controlled repetition becomes a challenge, instead we would use sentinel-controlled repetition. 

A count-controlled repetition will exit after running a certain number of times. 
The count is kept in a variable called an index or counter. 
When the index reaches a certain value (the loop bound) the loop will end. 

Count-controlled repetition requires

* control variable (or loop counter)
* initial value of the control variable
* increment (or decrement) by which the control variable is modified each iteration through the loop
* condition that tests for the final value of the control variable 

We can use both `for` and `while` loops, for count controlled repetition, but the `for` loop in combination with the `range()` function is more common.

### Structured `FOR` loop
We have seen the for loop already, but we will formally introduce it here. The `for` loop executes a block of code repeatedly until the condition in the `for` statement is no longer true.

### Looping through an iterable
An iterable is anything that can be looped over - typically a list, string, or tuple. 
The syntax for looping through an iterable is illustrated by an example.

First a generic syntax

    for a in iterable:
    print(a)
    
Notice our friends the colon `:` and the indentation.

#### The `range()` function to create an iterable

The `range(begin,end,increment)` function will create an iterable starting at a value of begin, in steps defined by increment (`begin += increment`), ending at `end`. 

So a generic syntax becomes

    for a in range(begin,end,increment):
    print(a)

The examples that follow are count-controlled repetition (increment skip if greater)

## Example `for` loops


```python
# sum numbers from 1 to n
howmany = int(input('Enter N'))
accumulator = 0.0
for i in range(1,howmany+1,1):
    accumulator = accumulator + float(i)
print( 'Sum from 1 to ',howmany, 'is %.3f' % accumulator  )
```

    Enter N 3


    Sum from 1 to  3 is 6.000



```python
# sum even numbers from 1 to n
howmany = int(input('Enter N'))
accumulator = 0.0
for i in range(1,howmany+1,1):
    if i%2 == 0:
        accumulator = accumulator + float(i)
print( 'Sum of Evens from 1 to ',howmany, 'is %.3f' % accumulator  )
```

    Enter N 3


    Sum of Evens from 1 to  3 is 2.000



```python
howmany = int(input('Enter N'))
linetoprint=''
for i in range(1,howmany+1,1):
    linetoprint=linetoprint + '*'
    print(linetoprint)
```

    Enter N 3


    *
    **
    ***



```python
howmany = int(input('Enter N'))
linetoprint=''
myiterable = range(1,howmany+1,1)  # using range to make an iterable
for i in myiterable:
    linetoprint=linetoprint + '*'
    print(linetoprint)
```

    Enter N 33


    *
    **
    ***
    ****
    *****
    ******
    *******
    ********
    *********
    **********
    ***********
    ************
    *************
    **************
    ***************
    ****************
    *****************
    ******************
    *******************
    ********************
    *********************
    **********************
    ***********************
    ************************
    *************************
    **************************
    ***************************
    ****************************
    *****************************
    ******************************
    *******************************
    ********************************
    *********************************


### References

1. Computational and Inferential Thinking Ani Adhikari and John DeNero, Computational and Inferential Thinking, The Foundations of Data Science, Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND) Chapters 3-6 [https://www.inferentialthinking.com/chapters/03/programming-in-python.html](https://www.inferentialthinking.com/chapters/03/programming-in-python.html)

2. Learn Python the Hard Way (Online Book) [https://learnpythonthehardway.org/book/](https://learnpythonthehardway.org/book/)  Recommended for beginners who want a complete course in programming with Python.

3. LearnPython.org (Interactive Tutorial) [https://www.learnpython.org/](https://www.learnpython.org/)  Short, interactive tutorial for those who just need a quick way to pick up Python syntax.

4. Brian Christian and Tom Griffiths (2016) ALGORITHMS TO LIVE BY: The Computer Science of Human Decisions Henry Holt and Co.[https://www.amazon.com/Algorithms-Live-Computer-Science-Decisions/dp/1627790365](https://www.amazon.com/Algorithms-Live-Computer-Science-Decisions/dp/1627790365)



```python

```
