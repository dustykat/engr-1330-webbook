# WHILE ... loop
## Sentinel-controlled repetition.

When loop control is based on the value of what we are processing, sentinel-controlled repetition is used. 
Sentinel-controlled repetition is also called indefinite repetition because it is not known in advance how many times the loop will be executed. 
It is a repetition procedure for solving a problem by using a sentinel value (also called a signal value, a dummy value or a flag value) to indicate "end of process". 
The sentinel value itself need not be a part of the processed data.

One common example of using sentinel-controlled repetition is when we are processing data from a file and we do not know in advance when we would reach the end of the file. 

We can use both `for` and `while` loops, for __Sentinel__ controlled repetition, but the `while` loop is more common.

### Structured `WHILE` loop
The `while` loop repeats a block of instructions inside the loop while a condition remainsvtrue.

First a generic syntax

    while condition is true:
        execute a
        execute b
    ....

Notice our friends the colon `:` and the indentation again.

# Example `while` loops


```python
# sum numbers from 1 to n
howmany = int(input('Enter N'))
accumulator = 0.0
counter = 1
while counter <= howmany:
    accumulator = accumulator + float(counter)
    counter += 1
print( 'Sum from 1 to ',howmany, 'is %.3f' % accumulator  )
```

    Enter N 3


    Sum from 1 to  3 is 6.000



```python
# sum even numbers from 1 to n
howmany = int(input('Enter N'))
accumulator = 0.0
counter = 1
while counter <= howmany:
    if counter%2 == 0:
        accumulator = accumulator + float(counter)
    counter += 1
print( 'Sum of Evens 1 to ',howmany, 'is %.3f' % accumulator  )
```

    Enter N 33


    Sum of Evens 1 to  33 is 272.000



```python
howmany = int(input('Enter N'))
linetoprint=''
counter = 1
while counter <= howmany:
    linetoprint=linetoprint + '*'
    counter += 1
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

1. Computational and Inferential Thinking Ani Adhikari and John DeNero, Computational and Inferential Thinking, The Foundations of Data Science, Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND) Chapters 3-6 https://www.inferentialthinking.com/chapters/03/programming-in-python.html

2. Learn Python the Hard Way (Online Book) (https://learnpythonthehardway.org/book/)  Recommended for beginners who want a complete course in programming with Python.

3. LearnPython.org (Interactive Tutorial) (https://www.learnpython.org/)  Short, interactive tutorial for those who just need a quick way to pick up Python syntax.

4. Brian Christian and Tom Griffiths (2016) ALGORITHMS TO LIVE BY: The Computer Science of Human Decisions Henry Holt and Co. (https://www.amazon.com/Algorithms-Live-Computer-Science-Decisions/dp/1627790365)




```python

```
