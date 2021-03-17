```python
# Script block to identify host, user, and kernel
import sys
! echo 'HID : ' $HOSTNAME
! echo 'UID : ' $USER
! pwd
print(sys.executable) #print(sys.version) #print(sys.version_info)
```

    HID :  atomickitty
    UID :  sensei
    /home/sensei/1330-textbook-webroot/ctds-webbook/docs/lesson0
    /opt/jupyterhub/bin/python3



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



# JupyterLab/iPython Fundamentals

Last GitHub Commit Date: none

## Topics
- JupyterLab (iPython) as a programming environment 
- Programming as a problem solving process
- The CCMR Approach

## JupyterLab (iPython) Environment

### The tools:
**JupyterLab** [https://jupyter.org/](https://jupyter.org/) is a web-based interactive development environment for Jupyter notebooks, code, and data. 

**Jupyter Notebook** is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations and narrative text. Uses include: data organizing and transformation, numerical simulation, statistical modeling, visualization, machine learning, and other similar types of uses. 

**JupyterHub** [https://github.com/jupyterhub/jupyterhub](https://github.com/jupyterhub/jupyterhub) is a multi-user Hub that spawns, manages, and proxies multiple instances of the single-user Jupyter notebook server.

All these tools allow use of various coding languages; Python is the choice for ENGR 1330.  Installing JupyterLab on your own computer is relatively straightforward if it is an Intel-based Linux, Macintosh, or Windows machine - simply use Anaconda [https://www.anaconda.com/](https://www.anaconda.com/) as the installer.

Installing onto an ARM-based machine is more difficult, but possible (this notebook was created on a Raspberry Pi). With both Apple and Microsoft abandoning Intel one can only hope for Anaconda builds for aarch64 (ARM).  

### This course:

You will create and use Jupyter Notebooks that use the **ipython** kernel, the notebook files will look like `filename.ipynb`; these are ASCII files that the JupyterLab interprets and runs.

## Python

The programming language we will use is Python (actually iPython). Python is an example of a high-level language; other high-level languages include C, C++, PHP, FORTRAN, ADA, Pascal, Go, Java, etc (there are a lot).

As you might infer from the name high-level language, there are also low-level languages, sometimes referred to as machine languages or assembly languages. Machine language is the encoding of instructions in binary so that they can be directly executed by the computer. Assembly language uses a slightly easier format to refer to the low level instructions. Loosely speaking, computers can only execute programs written in low-level languages. To be exact, computers can actually only execute programs written in machine language. Thus, programs written in a high-level language (and even those in assembly language) have to be processed before they can run. This extra processing takes some time, which is a small disadvantage of high-level languages. However, the advantages to high-level languages are enormous.

First, it is much easier to program in a high-level language. Programs written in a high-level language take less time to write, they are shorter and easier to read, and they are more likely to be correct. Second, high-level languages are portable, meaning that they can run on different kinds of computers with few or no modifications. Low-level programs can run on only one kind of computer and have to be rewritten to run on another.

Due to these advantages, almost all programs are written in high-level languages. Low-level languages are used only for a few specialized applications, and for device drivers.

Two kinds of programs process high-level languages into low-level languages: interpreters and compilers. An interpreter reads a high-level program and executes it, meaning that it does what the program says. It processes the program a little at a time, alternately reading lines and performing computations.

![](interpreter.png)

||Interpreted Program. Image from [https://runestone.academy/runestone/books/published/thinkcspy/GeneralIntro/ThePythonProgrammingLanguage.html](https://runestone.academy/runestone/books/published/thinkcspy/GeneralIntro/ThePythonProgrammingLanguage.html)||
|---|------------|---|

A compiler reads the program and translates it completely before the program starts running. In this case, the high-level program is called the source code, and the translated program is called the object code or the executable. Once a program is compiled, you can execute it repeatedly without further translation.

![](compiler.png)

||Compiled Prorgam. Image from: [https://runestone.academy/runestone/books/published/thinkcspy/GeneralIntro/ThePythonProgrammingLanguage.html](https://runestone.academy/runestone/books/published/thinkcspy/GeneralIntro/ThePythonProgrammingLanguage.html)||
|---|------------|---|

Many modern languages use both processes. They are first compiled into a lower level language, called byte code, and then interpreted by a program called a virtual machine. Python uses both processes, but because of the way programmers interact with it, it is usually considered an interpreted language.

As a language, python is a formal language that has certain requirements and structure called "syntax."

Formal languages are languages that are designed by people for specific applications. For example, the notation that mathematicians use is a formal language that is particularly good at denoting relationships among numbers and symbols. Chemists use a formal language to represent the chemical structure of molecules. Programming languages are formal languages that have been designed to express computations.

Formal languages have strict rules about syntax. For example, 3+3=6 is a syntactically correct mathematical statement, but 3=+6& is not. 

Syntax rules come in two flavors, pertaining to **tokens** and **structure**. **Tokens** are the basic elements of the language, such as words, numbers, and chemical elements. One of the problems with 3=+6& is that & is not a legal token in mathematics (at least as far as we know). 

The second type of syntax rule pertains to the structure of a statement— that is, the way the tokens are arranged. The statement 3=+6& is structurally illegal (in mathematics) because you don’t place a plus sign immediately after an equal sign (of course we will in python!). 

When you read a sentence in English or a statement in a formal language, you have to figure out what the structure of the sentence is; This process is called **parsing**.

For example, when you hear the sentence, “The other shoe fell”, you understand that the other shoe is the subject and fell is the verb. Once you have parsed a sentence, you can figure out what it means, or the semantics of the sentence. Assuming that you know what a shoe is and what it means to fall, you will understand the general implication of this sentence.

### Good Resources:

- Learn Python the Hard Way (Online Book) [https://learnpythonthehardway.org/book/](https://learnpythonthehardway.org/book/)  Recommended for beginners who want a complete course in programming with Python.
- LearnPython.org (Interactive Tutorial) [https://www.learnpython.org/](https://www.learnpython.org/)  Short, interactive tutorial for those who just need a quick way to pick up Python syntax.
- How to Think Like a Computer Scientist (Interactive Book) [https://runestone.academy/runestone/books/published/thinkcspy/index.html](https://runestone.academy/runestone/books/published/thinkcspy/index.html) Interactive "CS 101" course taught in Python that really focuses on the art of problem solving. 
- How to Learn Python for Data Science, The Self-Starter Way [https://elitedatascience.com/learn-python-for-data-science](https://elitedatascience.com/learn-python-for-data-science) 



## Readings

Computational and Inferential Thinking Ani Adhikari and John DeNero, Computational and Inferential Thinking, The Foundations of Data Science, Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND) Chapter 1 [https://www.inferentialthinking.com/chapters/01/what-is-data-science.htmlhttps://www.inferentialthinking.com/chapters/01/what-is-data-science.html](https://www.inferentialthinking.com/chapters/01/what-is-data-science.html)
