# ENGR 1330 Computational Thinking with Data Science 
Last GitHub Commit Date: 14 February 2021

## Lesson 7 The Pandas module 
- About Pandas
- How to install
    - Anaconda
    - JupyterHub/Lab (on Linux)
    - JupyterHub/Lab (on MacOS)
    - JupyterHub/Lab (on Windoze)
- The Dataframe
    - Primatives
    - Using Pandas
    - Create, Modify, Delete datagrames
    - Slice Dataframes
    - Conditional Selection
    - Synthetic Programming (Symbolic Function Application)
    - Files
- Access Files from a remote Web Server
    - Get file contents
    - Get the actual file
    - Adaptations for encrypted servers (future semester)
---
### Special Script Blocks


```python
%%html
<!--Script block to left align Markdown Tables-->
<style>
  table {margin-left: 0 !important;}
</style>
```


<!--Script block to left align Markdown Tables-->
<style>
  table {margin-left: 0 !important;}
</style>



---
## Objectives
1. To understand the **dataframe abstraction** as implemented in the Pandas library(module).
    1. To be able to access and manipulate data within a dataframe
    2. To be able to obtain basic statistical measures of data within a dataframe
2. Read/Write from/to files
    1. MS Excel-type files (.xls,.xlsx,.csv) (LibreOffice files use the MS .xml standard)
    2. Ordinary ASCII (.txt) files 
3. Access files directly from a URL (advanced concept)
    1. Using a wget-type function
    2. Using a curl-type function
    3. Using API keys (future versions)


### Pandas: 
Pandas is the core library for dataframe manipulation in Python. It provides a high-performance multidimensional array object, and tools for working with these arrays. The library’s name is derived from the term ‘Panel Data’. 
If you are curious about Pandas, this cheat sheet is recommended: [https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)

#### Data Structure 
The Primary data structure is called a dataframe.  It is an **abstraction** where data are represented as a 2-dimensional mutable and heterogenous tabular data structure; much like a Worksheet in MS Excel. The structure itself is popular among statisticians and data scientists and business executives.  

According to the marketing department 
*"Pandas Provides rich data structures and functions designed to make working with data fast, easy, and expressive.  It is useful in data manipulation, cleaning, and analysis; Pandas excels in performance and productivity "*

---

# The Dataframe

A data table is called a `DataFrame` in pandas (and other programming environments too). The figure below from [https://pandas.pydata.org/docs/getting_started/index.html](https://pandas.pydata.org/docs/getting_started/index.html) illustrates a dataframe model:

![](01-table-dataframe.png) 

Each **column** and each **row** in a dataframe is called a series, the header row, and index column are special. 
Like MS Excel we can query the dataframe to find the contents of a particular `cell` using its **row name** and **column name**, or operate on entire **rows** and **columns**

To use pandas, we need to import the module.

## Computational Thinking Concepts

The CT concepts expressed within Pandas include:

- `Decomposition` :  Data interpretation, manipulation, and analysis of Pandas dataframes is an act of decomposition -- although the dataframes can be quite complex.
- `Abstraction` : The dataframe is a data representation abstraction that allows for placeholder operations, later substituted with specific contents for a problem; enhances reuse and readability.  We leverage the principle of algebraic replacement using these abstractions.
- `Algorithms` :  Data interpretation, manipulation, and analysis of dataframes are generally implemented as part of a supervisory algorithm.

## Module Set-Up

In principle, Pandas should be available in a default Anaconda install 
- You should not have to do any extra installation steps to install the library in Python
- You do have to **import** the library in your scripts

How to check
- Simply open a code cell and run `import pandas` if the notebook does not protest (i.e. pink block of error), the youis good to go.


```python
import pandas
```

If you do get an error, that means that you will have to install using `conda` or `pip`; you are on-your-own here!  On the **content server** the process is:

1. Open a new terminal from the launcher
2. Change to root user `su` then enter the root password
3. `sudo -H /opt/jupyterhib/bin/python3 -m pip install pandas`
4. Wait until the install is complete; for security, user `compthink` is not in the `sudo` group
5. Verify the install by trying to execute `import pandas` as above.

The process above will be similar on a Macintosh, or Windows if you did not use an Anaconda distribution.   Best is to have a sucessful anaconda install, or go to the [GoodJobUntilMyOrgansGetHarvested](https://apply.mysubwaycareer.com/us/en/). 

If you have to do this kind of install, you will have to do some reading, some references I find useful are:
1. https://jupyterlab.readthedocs.io/en/stable/user/extensions.html
2. https://www.pugetsystems.com/labs/hpc/Note-How-To-Install-JupyterHub-on-a-Local-Server-1673/#InstallJupyterHub
3. https://jupyterhub.readthedocs.io/en/stable/installation-guide-hard.html (This is the approach on the content server which has a functioning JupyterHub)


```python

```

### Dataframe-type Structure using primative python

First lets construct a dataframe like object using python primatives.
We will construct 3 lists, one for row names, one for column names, and one for the content.


```python
import numpy
mytabular = numpy.random.randint(1,100,(5,4))
myrowname = ['A','B','C','D','E']
mycolname = ['W','X','Y','Z']
mytable = [['' for jcol in range(len(mycolname)+1)] for irow in range(len(myrowname)+1)] #non-null destination matrix, note the implied loop construction
```

The above builds a placeholder named `mytable` for the psuedo-dataframe.
Next we populate the table, using a for loop to write the column names in the first row, row names in the first column, and the table fill for the rest of the table.


```python
for irow in range(1,len(myrowname)+1): # write the row names
    mytable[irow][0]=myrowname[irow-1]
for jcol in range(1,len(mycolname)+1): # write the column names
    mytable[0][jcol]=mycolname[jcol-1]  
for irow in range(1,len(myrowname)+1): # fill the table (note the nested loop)
    for jcol in range(1,len(mycolname)+1):
        mytable[irow][jcol]=mytabular[irow-1][jcol-1]
```

Now lets print the table out by row and we see we have a very dataframe-like structure


```python
for irow in range(0,len(myrowname)+1):
    print(mytable[irow][0:len(mycolname)+1])
```

    ['', 'W', 'X', 'Y', 'Z']
    ['A', 19, 21, 22, 81]
    ['B', 94, 75, 66, 44]
    ['C', 70, 56, 47, 63]
    ['D', 56, 80, 39, 39]
    ['E', 66, 78, 39, 15]


We can also query by row 


```python
print(mytable[3][0:len(mycolname)+1])
```

    ['C', 70, 56, 47, 63]


Or by column


```python
for irow in range(0,len(myrowname)+1):  #cannot use implied loop in a column slice
    print(mytable[irow][2])
```

    X
    21
    75
    56
    80
    78


Or by row+column index; sort of looks like a spreadsheet syntax.


```python
print(' ',mytable[0][3])
print(mytable[3][0],mytable[3][3])
```

      Y
    C 47


# Now we shall create a proper dataframe
We will now do the same using pandas


```python
mydf = pandas.DataFrame(numpy.random.randint(1,100,(5,4)), ['A','B','C','D','E'], ['W','X','Y','Z'])
mydf
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>97</td>
      <td>20</td>
      <td>61</td>
      <td>35</td>
    </tr>
    <tr>
      <th>B</th>
      <td>74</td>
      <td>8</td>
      <td>7</td>
      <td>99</td>
    </tr>
    <tr>
      <th>C</th>
      <td>75</td>
      <td>67</td>
      <td>52</td>
      <td>82</td>
    </tr>
    <tr>
      <th>D</th>
      <td>92</td>
      <td>83</td>
      <td>90</td>
      <td>28</td>
    </tr>
    <tr>
      <th>E</th>
      <td>80</td>
      <td>67</td>
      <td>4</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
</div>



We can also turn our table into a dataframe, notice how the constructor adds header row and index column


```python
mydf1 = pandas.DataFrame(mytable)
mydf1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td></td>
      <td>W</td>
      <td>X</td>
      <td>Y</td>
      <td>Z</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A</td>
      <td>19</td>
      <td>21</td>
      <td>22</td>
      <td>81</td>
    </tr>
    <tr>
      <th>2</th>
      <td>B</td>
      <td>94</td>
      <td>75</td>
      <td>66</td>
      <td>44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C</td>
      <td>70</td>
      <td>56</td>
      <td>47</td>
      <td>63</td>
    </tr>
    <tr>
      <th>4</th>
      <td>D</td>
      <td>56</td>
      <td>80</td>
      <td>39</td>
      <td>39</td>
    </tr>
    <tr>
      <th>5</th>
      <td>E</td>
      <td>66</td>
      <td>78</td>
      <td>39</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>



To get proper behavior, we can just reuse our original objects


```python
mydf2 = pandas.DataFrame(mytabular,myrowname,mycolname)
mydf2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>19</td>
      <td>21</td>
      <td>22</td>
      <td>81</td>
    </tr>
    <tr>
      <th>B</th>
      <td>94</td>
      <td>75</td>
      <td>66</td>
      <td>44</td>
    </tr>
    <tr>
      <th>C</th>
      <td>70</td>
      <td>56</td>
      <td>47</td>
      <td>63</td>
    </tr>
    <tr>
      <th>D</th>
      <td>56</td>
      <td>80</td>
      <td>39</td>
      <td>39</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>78</td>
      <td>39</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>



Why are `mydf` and `mydf2` different?


```python

```

### Getting the shape of dataframes

The shape method, which is available after the dataframe is constructed, will return the row and column rank (count) of a dataframe.


```python
mydf.shape
```




    (5, 4)




```python
mydf1.shape
```




    (6, 5)




```python
mydf2.shape
```




    (5, 4)




```python

```

### Appending new columns
To append a column simply assign a value to a new column name to the dataframe


```python
mydf['new']= 'NA'
```


```python
mydf
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>97</td>
      <td>20</td>
      <td>61</td>
      <td>35</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>B</th>
      <td>74</td>
      <td>8</td>
      <td>7</td>
      <td>99</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>C</th>
      <td>75</td>
      <td>67</td>
      <td>52</td>
      <td>82</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>D</th>
      <td>92</td>
      <td>83</td>
      <td>90</td>
      <td>28</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>E</th>
      <td>80</td>
      <td>67</td>
      <td>4</td>
      <td>24</td>
      <td>NA</td>
    </tr>
  </tbody>
</table>
</div>



## Appending new rows
This is sometimes a bit trickier but here is one way:
- create a copy of a row, give it a new name. 
- concatenate it back into the dataframe.


```python
newrow = mydf.loc[['E']].rename(index={"E": "X"}) # create a single row, rename the index
newtable = pandas.concat([mydf,newrow]) # concatenate the row to bottom of df - note the syntax
```


```python
newtable
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>97</td>
      <td>20</td>
      <td>61</td>
      <td>35</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>B</th>
      <td>74</td>
      <td>8</td>
      <td>7</td>
      <td>99</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>C</th>
      <td>75</td>
      <td>67</td>
      <td>52</td>
      <td>82</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>D</th>
      <td>92</td>
      <td>83</td>
      <td>90</td>
      <td>28</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>E</th>
      <td>80</td>
      <td>67</td>
      <td>4</td>
      <td>24</td>
      <td>NA</td>
    </tr>
    <tr>
      <th>X</th>
      <td>80</td>
      <td>67</td>
      <td>4</td>
      <td>24</td>
      <td>NA</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

### Removing Rows and Columns

To remove a column is straightforward, we use the drop method


```python
newtable.drop('new', axis=1, inplace = True)
newtable
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>97</td>
      <td>20</td>
      <td>61</td>
      <td>35</td>
    </tr>
    <tr>
      <th>B</th>
      <td>74</td>
      <td>8</td>
      <td>7</td>
      <td>99</td>
    </tr>
    <tr>
      <th>C</th>
      <td>75</td>
      <td>67</td>
      <td>52</td>
      <td>82</td>
    </tr>
    <tr>
      <th>D</th>
      <td>92</td>
      <td>83</td>
      <td>90</td>
      <td>28</td>
    </tr>
    <tr>
      <th>E</th>
      <td>80</td>
      <td>67</td>
      <td>4</td>
      <td>24</td>
    </tr>
    <tr>
      <th>X</th>
      <td>80</td>
      <td>67</td>
      <td>4</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
</div>



To remove a row, you really got to want to, easiest is probablty to create a new dataframe with the row removed


```python
newtable = newtable.loc[['A','B','D','E','X']] # select all rows except C
newtable
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>97</td>
      <td>20</td>
      <td>61</td>
      <td>35</td>
    </tr>
    <tr>
      <th>B</th>
      <td>74</td>
      <td>8</td>
      <td>7</td>
      <td>99</td>
    </tr>
    <tr>
      <th>D</th>
      <td>92</td>
      <td>83</td>
      <td>90</td>
      <td>28</td>
    </tr>
    <tr>
      <th>E</th>
      <td>80</td>
      <td>67</td>
      <td>4</td>
      <td>24</td>
    </tr>
    <tr>
      <th>X</th>
      <td>80</td>
      <td>67</td>
      <td>4</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# or just use drop with axis specify
newtable.drop('X', axis=0, inplace = True)
```


```python
newtable
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>97</td>
      <td>20</td>
      <td>61</td>
      <td>35</td>
    </tr>
    <tr>
      <th>B</th>
      <td>74</td>
      <td>8</td>
      <td>7</td>
      <td>99</td>
    </tr>
    <tr>
      <th>D</th>
      <td>92</td>
      <td>83</td>
      <td>90</td>
      <td>28</td>
    </tr>
    <tr>
      <th>E</th>
      <td>80</td>
      <td>67</td>
      <td>4</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
</div>



# Indexing
We have already been indexing, but a few examples follow:


```python
newtable['X'] #Selecing a single column
```




    A    20
    B     8
    D    83
    E    67
    Name: X, dtype: int64




```python
newtable[['X','W']] #Selecing a multiple columns
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>X</th>
      <th>W</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>20</td>
      <td>97</td>
    </tr>
    <tr>
      <th>B</th>
      <td>8</td>
      <td>74</td>
    </tr>
    <tr>
      <th>D</th>
      <td>83</td>
      <td>92</td>
    </tr>
    <tr>
      <th>E</th>
      <td>67</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>




```python
newtable.loc['E'] #Selecing rows based on label via loc[ ] indexer
```




    W    80
    X    67
    Y     4
    Z    24
    Name: E, dtype: int64




```python
newtable
    
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>97</td>
      <td>20</td>
      <td>61</td>
      <td>35</td>
    </tr>
    <tr>
      <th>B</th>
      <td>74</td>
      <td>8</td>
      <td>7</td>
      <td>99</td>
    </tr>
    <tr>
      <th>D</th>
      <td>92</td>
      <td>83</td>
      <td>90</td>
      <td>28</td>
    </tr>
    <tr>
      <th>E</th>
      <td>80</td>
      <td>67</td>
      <td>4</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
</div>




```python
newtable.loc[['E','D','B']] #Selecing multiple rows based on label via loc[ ] indexer
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>E</th>
      <td>80</td>
      <td>67</td>
      <td>4</td>
      <td>24</td>
    </tr>
    <tr>
      <th>D</th>
      <td>92</td>
      <td>83</td>
      <td>90</td>
      <td>28</td>
    </tr>
    <tr>
      <th>B</th>
      <td>74</td>
      <td>8</td>
      <td>7</td>
      <td>99</td>
    </tr>
  </tbody>
</table>
</div>




```python
newtable.loc[['B','E','D'],['X','Y']] #Selecting elements via both rows and columns via loc[ ] indexer
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>X</th>
      <th>Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>B</th>
      <td>8</td>
      <td>7</td>
    </tr>
    <tr>
      <th>E</th>
      <td>67</td>
      <td>4</td>
    </tr>
    <tr>
      <th>D</th>
      <td>83</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



# Conditional Selection


```python
mydf = pandas.DataFrame({'col1':[1,2,3,4,5,6,7,8],
                   'col2':[444,555,666,444,666,111,222,222],
                   'col3':['orange','apple','grape','mango','jackfruit','watermelon','banana','peach']})
mydf
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>444</td>
      <td>orange</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>555</td>
      <td>apple</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>666</td>
      <td>grape</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>444</td>
      <td>mango</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>666</td>
      <td>jackfruit</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>111</td>
      <td>watermelon</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>222</td>
      <td>banana</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>222</td>
      <td>peach</td>
    </tr>
  </tbody>
</table>
</div>




```python
#What fruit corresponds to the number 555 in ‘col2’?

mydf[mydf['col2']==555]['col3']
```




    1    apple
    Name: col3, dtype: object




```python
#What fruit corresponds to the minimum number in ‘col2’?

mydf[mydf['col2']==mydf['col2'].min()]['col3']
```




    5    watermelon
    Name: col3, dtype: object



# Descriptor Functions


```python
#Creating a dataframe from a dictionary

mydf = pandas.DataFrame({'col1':[1,2,3,4,5,6,7,8],
                   'col2':[444,555,666,444,666,111,222,222],
                   'col3':['orange','apple','grape','mango','jackfruit','watermelon','banana','peach']})
mydf
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>444</td>
      <td>orange</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>555</td>
      <td>apple</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>666</td>
      <td>grape</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>444</td>
      <td>mango</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>666</td>
      <td>jackfruit</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>111</td>
      <td>watermelon</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>222</td>
      <td>banana</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>222</td>
      <td>peach</td>
    </tr>
  </tbody>
</table>
</div>



### `head` method

Returns the first few rows, useful to infer structure


```python
#Returns only the first five rows

mydf.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>444</td>
      <td>orange</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>555</td>
      <td>apple</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>666</td>
      <td>grape</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>444</td>
      <td>mango</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>666</td>
      <td>jackfruit</td>
    </tr>
  </tbody>
</table>
</div>



### `info` method

Returns the data model (data column count, names, data types)


```python
#Info about the dataframe

mydf.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 8 entries, 0 to 7
    Data columns (total 3 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   col1    8 non-null      int64 
     1   col2    8 non-null      int64 
     2   col3    8 non-null      object
    dtypes: int64(2), object(1)
    memory usage: 320.0+ bytes


### `describe` method

Returns summary statistics of each numeric column.  
Also returns the minimum and maximum value in each column, and the IQR (Interquartile Range).  
Again useful to understand structure of the columns.


```python
#Statistics of the dataframe

mydf.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>8.00000</td>
      <td>8.0000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>4.50000</td>
      <td>416.2500</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2.44949</td>
      <td>211.8576</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.00000</td>
      <td>111.0000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2.75000</td>
      <td>222.0000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>4.50000</td>
      <td>444.0000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>6.25000</td>
      <td>582.7500</td>
    </tr>
    <tr>
      <th>max</th>
      <td>8.00000</td>
      <td>666.0000</td>
    </tr>
  </tbody>
</table>
</div>



### Counting and Sum methods

There are also methods for counts and sums by specific columns


```python
mydf['col2'].sum() #Sum of a specified column
```




    3330



The `unique` method returns a list of unique values (filters out duplicates in the list, underlying dataframe is preserved)


```python
mydf['col2'].unique() #Returns the list of unique values along the indexed column 
```




    array([444, 555, 666, 111, 222])



The `nunique` method returns a count of unique values


```python
mydf['col2'].nunique() #Returns the total number of unique values along the indexed column 
```




    5



The `value_counts()` method returns the count of each unique value (kind of like a histogram, but each value is the bin)


```python
mydf['col2'].value_counts()  #Returns the number of occurences of each unique value
```




    222    2
    444    2
    666    2
    111    1
    555    1
    Name: col2, dtype: int64



## Using functions in dataframes - symbolic apply

The power of **Pandas** is an ability to apply a function to each element of a dataframe series (or a whole frame) by a technique called symbolic (or synthetic programming) application of the function.

This employs principles of **pattern matching**, **abstraction**, and **algorithm development**; a holy trinity of Computational Thinning.

It's somewhat complicated but quite handy, best shown by an example:


```python
def times2(x):  # A prototype function to scalar multiply an object x by 2
    return(x*2)

print(mydf)
print('Apply the times2 function to col2')
mydf['col2'].apply(times2) #Symbolic apply the function to each element of column col2, result is another dataframe
```

       col1  col2        col3
    0     1   444      orange
    1     2   555       apple
    2     3   666       grape
    3     4   444       mango
    4     5   666   jackfruit
    5     6   111  watermelon
    6     7   222      banana
    7     8   222       peach
    Apply the times2 function to col2





    0     888
    1    1110
    2    1332
    3     888
    4    1332
    5     222
    6     444
    7     444
    Name: col2, dtype: int64



## Sorts 


```python
mydf.sort_values('col2', ascending = True) #Sorting based on columns 
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>111</td>
      <td>watermelon</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>222</td>
      <td>banana</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>222</td>
      <td>peach</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>444</td>
      <td>orange</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>444</td>
      <td>mango</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>555</td>
      <td>apple</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>666</td>
      <td>grape</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>666</td>
      <td>jackfruit</td>
    </tr>
  </tbody>
</table>
</div>




```python
mydf.sort_values('col3', ascending = True) #Lexiographic sort
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>555</td>
      <td>apple</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>222</td>
      <td>banana</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>666</td>
      <td>grape</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>666</td>
      <td>jackfruit</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>444</td>
      <td>mango</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>444</td>
      <td>orange</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>222</td>
      <td>peach</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>111</td>
      <td>watermelon</td>
    </tr>
  </tbody>
</table>
</div>



# Aggregating (Grouping Values) dataframe contents



```python
#Creating a dataframe from a dictionary

data = {
    'key' : ['A', 'B', 'C', 'A', 'B', 'C'],
    'data1' : [1, 2, 3, 4, 5, 6],
    'data2' : [10, 11, 12, 13, 14, 15],
    'data3' : [20, 21, 22, 13, 24, 25]
}

mydf1 = pandas.DataFrame(data)
mydf1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>data1</th>
      <th>data2</th>
      <th>data3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1</td>
      <td>10</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2</td>
      <td>11</td>
      <td>21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3</td>
      <td>12</td>
      <td>22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A</td>
      <td>4</td>
      <td>13</td>
      <td>13</td>
    </tr>
    <tr>
      <th>4</th>
      <td>B</td>
      <td>5</td>
      <td>14</td>
      <td>24</td>
    </tr>
    <tr>
      <th>5</th>
      <td>C</td>
      <td>6</td>
      <td>15</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Grouping and summing values in all the columns based on the column 'key'

mydf1.groupby('key').sum()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>data1</th>
      <th>data2</th>
      <th>data3</th>
    </tr>
    <tr>
      <th>key</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>5</td>
      <td>23</td>
      <td>33</td>
    </tr>
    <tr>
      <th>B</th>
      <td>7</td>
      <td>25</td>
      <td>45</td>
    </tr>
    <tr>
      <th>C</th>
      <td>9</td>
      <td>27</td>
      <td>47</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Grouping and summing values in the selected columns based on the column 'key'

mydf1.groupby('key')[['data1', 'data2']].sum()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>data1</th>
      <th>data2</th>
    </tr>
    <tr>
      <th>key</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>5</td>
      <td>23</td>
    </tr>
    <tr>
      <th>B</th>
      <td>7</td>
      <td>25</td>
    </tr>
    <tr>
      <th>C</th>
      <td>9</td>
      <td>27</td>
    </tr>
  </tbody>
</table>
</div>



# Filtering out missing values

Filtering and *cleaning* are often used to describe the process where data that does not support a narrative is removed ;typically for maintenance of profit applications, if the data are actually missing that is common situation where cleaning is justified.


```python
#Creating a dataframe from a dictionary

df = pandas.DataFrame({'col1':[1,2,3,4,None,6,7,None],
                   'col2':[444,555,None,444,666,111,None,222],
                   'col3':['orange','apple','grape','mango','jackfruit','watermelon','banana','peach']})
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>444.0</td>
      <td>orange</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>555.0</td>
      <td>apple</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>NaN</td>
      <td>grape</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>444.0</td>
      <td>mango</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>666.0</td>
      <td>jackfruit</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6.0</td>
      <td>111.0</td>
      <td>watermelon</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7.0</td>
      <td>NaN</td>
      <td>banana</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>222.0</td>
      <td>peach</td>
    </tr>
  </tbody>
</table>
</div>



Below we drop any row that contains a `NaN` code.


```python
df_dropped = df.dropna()
df_dropped
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>444.0</td>
      <td>orange</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>555.0</td>
      <td>apple</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>444.0</td>
      <td>mango</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6.0</td>
      <td>111.0</td>
      <td>watermelon</td>
    </tr>
  </tbody>
</table>
</div>



Below we replace `NaN` codes with some value, in this case 0


```python
df_filled1 = df.fillna(0)
df_filled1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>444.0</td>
      <td>orange</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>555.0</td>
      <td>apple</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>0.0</td>
      <td>grape</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>444.0</td>
      <td>mango</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.0</td>
      <td>666.0</td>
      <td>jackfruit</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6.0</td>
      <td>111.0</td>
      <td>watermelon</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7.0</td>
      <td>0.0</td>
      <td>banana</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.0</td>
      <td>222.0</td>
      <td>peach</td>
    </tr>
  </tbody>
</table>
</div>



Below we replace `NaN` codes with some value, in this case the mean value of of the column in which the missing value code resides.


```python
df_filled2 = df.fillna(df.mean())
df_filled2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.000000</td>
      <td>444.0</td>
      <td>orange</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.000000</td>
      <td>555.0</td>
      <td>apple</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.000000</td>
      <td>407.0</td>
      <td>grape</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.000000</td>
      <td>444.0</td>
      <td>mango</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.833333</td>
      <td>666.0</td>
      <td>jackfruit</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6.000000</td>
      <td>111.0</td>
      <td>watermelon</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7.000000</td>
      <td>407.0</td>
      <td>banana</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3.833333</td>
      <td>222.0</td>
      <td>peach</td>
    </tr>
  </tbody>
</table>
</div>



---
## Reading a File into a Dataframe

Pandas has methods to read common file types, such as `csv`,`xlsx`, and `json`.  
Ordinary text files are also quite manageable.

On a machine you control you can write script to retrieve files from the internet and process them.



```python
readfilecsv = pandas.read_csv('CSV_ReadingFile.csv')  #Reading a .csv file
print(readfilecsv)
```

        a   b   c   d
    0   0   1   2   3
    1   4   5   6   7
    2   8   9  10  11
    3  12  13  14  15


Similar to reading and writing .csv files, you can also read and write .xslx files as below (useful to know this)


```python
# xlsx reads deprecated here is a hack using openpyxl
readfileexcel = pandas.read_excel('Excel_ReadingFile.xlsx', sheet_name='Sheet1', engine='openpyxl') #Reading a .xlsx file
print(readfileexcel)
```

       Unnamed: 0   a   b   c   d
    0           0   0   1   2   3
    1           1   4   5   6   7
    2           2   8   9  10  11
    3           3  12  13  14  15


# Writing a dataframe to file


```python
#Creating and writing to a .csv file
readfilecsv = pandas.read_csv('CSV_ReadingFile.csv')
readfilecsv.to_csv('CSV_WritingFile1.csv')
readfilecsv = pandas.read_csv('CSV_WritingFile1.csv')
print(readfilecsv)
```

       Unnamed: 0   a   b   c   d
    0           0   0   1   2   3
    1           1   4   5   6   7
    2           2   8   9  10  11
    3           3  12  13  14  15



```python
#Creating and writing to a .csv file by excluding row labels 
readfilecsv = pandas.read_csv('CSV_ReadingFile.csv')
readfilecsv.to_csv('CSV_WritingFile2.csv', index = False)
readfilecsv = pandas.read_csv('CSV_WritingFile2.csv')
print(readfilecsv)
```

        a   b   c   d
    0   0   1   2   3
    1   4   5   6   7
    2   8   9  10  11
    3  12  13  14  15



```python
#Creating and writing to a .xlsx file
readfileexcel = pandas.read_excel('Excel_ReadingFile.xlsx', sheet_name='Sheet1', engine='openpyxl')
readfileexcel.to_excel('Excel_WritingFile.xlsx', sheet_name='MySheet', index = False, engine='openpyxl')
readfileexcel = pandas.read_excel('Excel_WritingFile.xlsx', sheet_name='MySheet', engine='openpyxl')
print(readfileexcel)
```

       Unnamed: 0   a   b   c   d
    0           0   0   1   2   3
    1           1   4   5   6   7
    2           2   8   9  10  11
    3           3  12  13  14  15


---

## Downloading files from websites (optional)

This section shows how to get files from a remote computer.   There are several ways to get the files, most importantly  you need the FQDN to the file.

### Method 1: Get data from a file on a remote server (unencrypted)
This section shows how to obtain data files from public URLs.  

Prerequesites:

- You know the FQDN to the file it will be in structure of "http://server-name/.../filename.ext"
- The server is running ordinary (unencrypted) web services, i.e. `http://...`

#### Web Developer Notes
If you want to distribute files (web developers) the files need to be in the server webroot, but can be deep into the heirarchial structure.

Here we will do an example with a file that contains topographic data in XYZ format, without header information.

The first few lines of the remote file look like:

    74.90959724	93.21251922	0
    75.17907367	64.40278759	0
    94.9935575	93.07951286	0
    95.26234119	64.60091165	0
    54.04976655	64.21159095	0
    54.52914363	35.06934342	0
    75.44993558	34.93079513	0
    75.09317373	5.462959114	0
    74.87357468	10.43130083	0
    74.86249082	15.72938748	0

And importantly it is tab delimited.

The module to manipulate url in python is called ``urllib``

Google search to learn more, here we are using only a small component without exception trapping.
    


```python
#Step 1: import needed modules to interact with the internet
from urllib.request import urlopen # import a method that will connect to a url and read file contents
import pandas #import pandas
```

This next code fragment sets a string called ``remote_url``; it is just a variable, name can be anything that honors python naming rules.
Then the ``urllib`` function ``urlopen`` with read and decode methods is employed, the result is stored in an object named ``elevationXYZ``


```python
#Step 2: make the connection to the remote file (actually its implementing "bash curl -O http://fqdn/path ...")
remote_url = 'http://www.rtfmps.com/share_files/pip-corner-sumps.txt' # 
elevationXYZ = urlopen(remote_url).read().decode().split() # Gets the file contents as a single vector, comma delimited, file is not retained locally
```

At this point the object exists as a single vector with hundreds of elements. We now need to structure the content.  Here using python primatives, and knowing how the data are supposed to look, we prepare variables to recieve the structured results


```python
#Step 3 Python primatives to structure the data, or use fancy modules (probably easy in numpy)
howmany = len(elevationXYZ) # how long is the vector?
nrow = int(howmany/3)
xyz = [[0 for j in range(3)] for j in range(nrow)] # null space to receive data define columnX
```

Now that everything is ready, we can extract from the object the values we want into ``xyz``


```python
#Step4 Now will build xyz as a matrix with 3 columns
index = 0
for irow in range(0,nrow):
    xyz[irow][0]=float(elevationXYZ[index])
    xyz[irow][1]=float(elevationXYZ[index+1])
    xyz[irow][2]=float(elevationXYZ[index+2])
    index += 3 #increment the index
```

``xyz`` is now a 3-column float array and can now probably be treated as a data frame.
Here we use a ``pandas`` method to build the dataframe.


```python
df = pandas.DataFrame(xyz)
```

Get some info, yep three columns (ordered triples to be precise!)


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 774 entries, 0 to 773
    Data columns (total 3 columns):
     #   Column  Non-Null Count  Dtype  
    ---  ------  --------------  -----  
     0   0       774 non-null    float64
     1   1       774 non-null    float64
     2   2       774 non-null    float64
    dtypes: float64(3)
    memory usage: 18.3 KB


And some summary statistics (meaningless for these data), but now have taken data from the internet and prepared it for analysis.


```python
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>774.000000</td>
      <td>774.000000</td>
      <td>774.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>52.064621</td>
      <td>48.770060</td>
      <td>2.364341</td>
    </tr>
    <tr>
      <th>std</th>
      <td>30.883400</td>
      <td>32.886277</td>
      <td>1.497413</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-2.113554</td>
      <td>-11.360960</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>25.640786</td>
      <td>21.809579</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>55.795821</td>
      <td>49.059950</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>76.752290</td>
      <td>75.015933</td>
      <td>4.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>111.726727</td>
      <td>115.123931</td>
      <td>4.000000</td>
    </tr>
  </tbody>
</table>
</div>



And lets look at the first few rows


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>74.909597</td>
      <td>93.212519</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>75.179074</td>
      <td>64.402788</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>94.993557</td>
      <td>93.079513</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>95.262341</td>
      <td>64.600912</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>54.049767</td>
      <td>64.211591</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

### Method 2: Get the actual file from a remote web server (unencrypted)

- You know the FQDN to the file it will be in structure of "http://server-name/.../filename.ext"
- The server is running ordinary (unencrypted) web services, i.e. `http://...`

We will need a module to interface with the remote server, in this example lets use something different than ``urllib``. Here we will use ``requests`` , so first we load the module


```python
import requests # Module to process http/https requests
```

Now we will generate a ``GET`` request to the remote http server.  I chose to do so using a variable to store the remote URL so I can reuse code in future projects.  The ``GET`` request (an http/https method) is generated with the requests method ``get`` and assigned to an object named ``rget`` -- the name is arbitrary.  Next we extract the file from the ``rget`` object and write it to a local file with the name of the remote file - esentially automating the download process. Then we import the ``pandas`` module.


```python
remote_url="http://54.243.252.9/engr-1330-psuedo-course/MyJupyterNotebooks/42-DataScience-EvaporationAnalysis/all_quads_gross_evaporation.csv"  # set the url
rget = requests.get(remote_url, allow_redirects=True)  # get the remote resource, follow imbedded links
open('all_quads_gross_evaporation.csv','wb').write(rget.content) # extract from the remote the contents, assign to a local file same name
import pandas as pd # Module to process dataframes (not absolutely needed but somewhat easier than using primatives, and gives graphing tools)
```


```python
# verify file exists
! pwd
! ls -la
```

    /home/sensei/1330-textbook-webroot/docs/lesson7
    total 1412
    drwxrwxr-x  3 sensei sensei   4096 Feb 16 20:57 .
    drwxr-xr-x 10 sensei sensei   4096 Feb 16 20:30 ..
    drwxrwxr-x  2 sensei sensei   4096 Feb 16 20:53 .ipynb_checkpoints
    -rw-rw-r--  1 sensei sensei  21150 Feb 15 15:58 01-table-dataframe.png
    -rw-rw-r--  1 sensei sensei     51 Feb 15 15:58 CSV_ReadingFile.csv
    -rw-rw-r--  1 sensei sensei     55 Feb 16 20:59 CSV_WritingFile1.csv
    -rw-rw-r--  1 sensei sensei     46 Feb 16 20:59 CSV_WritingFile2.csv
    -rw-rw-r--  1 sensei sensei 693687 Feb 15 15:58 ENGR-1330-Lesson8-Dev.html
    -rw-rw-r--  1 sensei sensei 166938 Feb 15 15:58 ENGR-1330-Lesson8-Dev.ipynb
    -rw-rw-r--  1 sensei sensei   5508 Feb 15 15:58 Excel_ReadingFile.xlsx
    -rw-rw-r--  1 sensei sensei   5041 Feb 16 20:59 Excel_WritingFile.xlsx
    -rw-rw-r--  1 sensei sensei 363498 Feb 16 20:59 all_quads_gross_evaporation.csv
    -rw-rw-r--  1 sensei sensei 108222 Feb 16 20:57 lesson7.ipynb
    -rw-rw-r--  1 sensei sensei  40566 Feb 15 15:58 output_126_1.png


Now we can read the file contents and check its structure, before proceeding.


```python
evapdf = pd.read_csv("all_quads_gross_evaporation.csv",parse_dates=["YYYY-MM"]) # Read the file as a .CSV assign to a dataframe evapdf
evapdf.head() # check structure
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>YYYY-MM</th>
      <th>104</th>
      <th>105</th>
      <th>106</th>
      <th>107</th>
      <th>108</th>
      <th>204</th>
      <th>205</th>
      <th>206</th>
      <th>207</th>
      <th>...</th>
      <th>911</th>
      <th>912</th>
      <th>1008</th>
      <th>1009</th>
      <th>1010</th>
      <th>1011</th>
      <th>1108</th>
      <th>1109</th>
      <th>1110</th>
      <th>1210</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1954-01-01</td>
      <td>1.80</td>
      <td>1.80</td>
      <td>2.02</td>
      <td>2.24</td>
      <td>2.24</td>
      <td>2.34</td>
      <td>1.89</td>
      <td>1.80</td>
      <td>1.99</td>
      <td>...</td>
      <td>1.42</td>
      <td>1.30</td>
      <td>2.50</td>
      <td>2.42</td>
      <td>1.94</td>
      <td>1.29</td>
      <td>2.59</td>
      <td>2.49</td>
      <td>2.22</td>
      <td>2.27</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1954-02-01</td>
      <td>4.27</td>
      <td>4.27</td>
      <td>4.13</td>
      <td>3.98</td>
      <td>3.90</td>
      <td>4.18</td>
      <td>4.26</td>
      <td>4.27</td>
      <td>4.26</td>
      <td>...</td>
      <td>2.59</td>
      <td>2.51</td>
      <td>4.71</td>
      <td>4.30</td>
      <td>3.84</td>
      <td>2.50</td>
      <td>5.07</td>
      <td>4.62</td>
      <td>4.05</td>
      <td>4.18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1954-03-01</td>
      <td>4.98</td>
      <td>4.98</td>
      <td>4.62</td>
      <td>4.25</td>
      <td>4.20</td>
      <td>5.01</td>
      <td>4.98</td>
      <td>4.98</td>
      <td>4.68</td>
      <td>...</td>
      <td>3.21</td>
      <td>3.21</td>
      <td>6.21</td>
      <td>6.06</td>
      <td>5.02</td>
      <td>3.21</td>
      <td>6.32</td>
      <td>6.20</td>
      <td>5.68</td>
      <td>5.70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1954-04-01</td>
      <td>6.09</td>
      <td>5.94</td>
      <td>5.94</td>
      <td>6.07</td>
      <td>5.27</td>
      <td>6.31</td>
      <td>5.98</td>
      <td>5.89</td>
      <td>5.72</td>
      <td>...</td>
      <td>3.83</td>
      <td>3.54</td>
      <td>6.45</td>
      <td>6.25</td>
      <td>4.92</td>
      <td>3.54</td>
      <td>6.59</td>
      <td>6.44</td>
      <td>5.88</td>
      <td>5.95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1954-05-01</td>
      <td>5.41</td>
      <td>5.09</td>
      <td>5.14</td>
      <td>4.40</td>
      <td>3.61</td>
      <td>5.57</td>
      <td>4.56</td>
      <td>4.47</td>
      <td>4.18</td>
      <td>...</td>
      <td>3.48</td>
      <td>3.97</td>
      <td>7.92</td>
      <td>8.13</td>
      <td>6.31</td>
      <td>3.99</td>
      <td>7.75</td>
      <td>7.98</td>
      <td>7.40</td>
      <td>7.40</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 93 columns</p>
</div>



Structure looks like a spreadsheet as expected; lets plot the time series for cell '911'


```python
evapdf.plot.line(x='YYYY-MM',y='911') # Plot quadrant 911 evaporation time series 
```




    <AxesSubplot:xlabel='YYYY-MM'>




    
![png](output_126_1.png)
    


### Method 3: Get the actual file from an encrypted server

This section is saved for future semesters

---

## References
Overland, B. (2018). Python Without Fear. Addison-Wesley 
ISBN 978-0-13-468747-6. 

Grus, Joel (2015). Data Science from Scratch: First Principles with Python O’Reilly
Media. Kindle Edition.

Precord, C. (2010) wxPython 2.8 Application Development Cookbook Packt Publishing Ltd. Birmingham , B27 6PA, UK 
ISBN 978-1-849511-78-0.


```python
# Preamble script block to identify host, user, and kernel
import sys
! hostname
! whoami
print(sys.executable)
print(sys.version)
print(sys.version_info)
```

    atomickitty
    sensei
    /opt/jupyterhub/bin/python3
    3.8.5 (default, Jul 28 2020, 12:59:40) 
    [GCC 9.3.0]
    sys.version_info(major=3, minor=8, micro=5, releaselevel='final', serial=0)



```python

```
