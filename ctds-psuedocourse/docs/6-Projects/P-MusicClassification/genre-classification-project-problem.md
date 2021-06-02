# 1. The Dataset (20 points)

Our dataset is a table of songs, each with a name, an artist, and a genre.  For each song, we also know how frequently certain words occur in that song.  More precisely, we have a list of approximately 5000 words.  For each of these words, for each song, each item in the table describes the proportion of the song's lyrics that are the particular word.

For example, the lyrics of "In Your Eyes" is 168 words long. The word "like" appears twice:  $\frac{2}{168} \approx 0.0119$ of the words in the song. Similarly, the word "love" appears 10 times: $\frac{10}{168} \approx 0.0595$ of the words. 

Our dataset doesn't contain all information about a song.  For example, it doesn't include the total number of words in each song, or information about the order of words in the song, let alone the melody, instruments, or rhythm. Nonetheless, you may find that word counts alone are sufficient to build an accurate genre classifier.

Run the cell below to read the `lyrics` table. **It may take up to a minute to load.**


```python
import pandas as pd
```


```python
df = pd.read_csv("lyrics_clean.csv")
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
      <th>Title</th>
      <th>Artist</th>
      <th>Genre</th>
      <th>i</th>
      <th>the</th>
      <th>you</th>
      <th>to</th>
      <th>and</th>
      <th>a</th>
      <th>me</th>
      <th>...</th>
      <th>writer</th>
      <th>motivo</th>
      <th>bake</th>
      <th>insist</th>
      <th>wel</th>
      <th>santo</th>
      <th>pe</th>
      <th>gee</th>
      <th>colleg</th>
      <th>kad</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Slicker Than Your Average</td>
      <td>Craig David</td>
      <td>Hip-hop</td>
      <td>0.049536</td>
      <td>0.017028</td>
      <td>0.035604</td>
      <td>0.020124</td>
      <td>0.007740</td>
      <td>0.006192</td>
      <td>0.058824</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Right There</td>
      <td>MF Grimm</td>
      <td>Hip-hop</td>
      <td>0.037825</td>
      <td>0.054374</td>
      <td>0.023641</td>
      <td>0.049645</td>
      <td>0.009456</td>
      <td>0.016548</td>
      <td>0.018913</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Talkin' All That</td>
      <td>Cashis</td>
      <td>Hip-hop</td>
      <td>0.056738</td>
      <td>0.049645</td>
      <td>0.051418</td>
      <td>0.010638</td>
      <td>0.026596</td>
      <td>0.033688</td>
      <td>0.007092</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>It Only Hurts Me When I Cry</td>
      <td>Raul Malo</td>
      <td>Country</td>
      <td>0.096491</td>
      <td>0.074561</td>
      <td>0.030702</td>
      <td>0.017544</td>
      <td>0.026316</td>
      <td>0.017544</td>
      <td>0.021930</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Is It Too Late Now</td>
      <td>Lester Flatt &amp; Earl Scruggs</td>
      <td>Country</td>
      <td>0.043902</td>
      <td>0.000000</td>
      <td>0.073171</td>
      <td>0.019512</td>
      <td>0.000000</td>
      <td>0.014634</td>
      <td>0.034146</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 4979 columns</p>
</div>



**Question 1.1**: Print the number of rows and columns in the dataset 


```python

```

**Question 1.2**: Find the proportion of the word `like` in the song `In Your Eyes`


```python

```

**Question 1.3:** Set `expected_row_sum` to the number that you expect will result from summing all proportions in each row, excluding the first three columns. 


```python
# Set row_sum to a number that's the (approximate) sum of each row of word proportions.
expected_row_sum = ...
```

Verify your answer by doing sum along the columns for each row


```python

```

## Word Stemming
The columns other than Title, Artist, and Genre in the `lyrics` table are all words that appear in some of the songs in our dataset.  Some of those names have been *stemmed*, or abbreviated heuristically, in an attempt to make different [inflected](https://en.wikipedia.org/wiki/Inflection) forms of the same base word into the same string.  For example, the column "manag" is the sum of proportions of the words "manage", "manager", "managed", and "managerial" (and perhaps others) in each song.  

Stemming makes it a little tricky to search for the words you want to use, so we have provided another dataframe that will let you see examples of unstemmed versions of each stemmed word.  Run the code below to load it.

**Question 1.4**: Read the vocabulary from the given file `mxm_reverse_mapping_safe.csv` and store it into a variale `vocab_mapping`


```python
vocab_mapping = ...
vocab_mapping
```

**Question 1.5**: Compare if the number of stemmed words in the vocabulary is the same with one in the song lyrics dataset.


```python

```

**Question 1.6:** Assign `unchanged` to the **percentage** of words in `vocab_table` that are the same as their stemmed form. 


```python

```

**Question 1.7:** Assign `stemmed_message` to the stemmed version of the word "message".


```python
# Set stemmed_message to the stemmed version of "message" (which
# should be a string).  

```

**Question 1.8:** Assign `unstemmed_singl` to the word in `vocab_table` that has "singl" as its stemmed form. (*Note that multiple English words may stem to "singl", but only one example appears in `vocab_table`.*)


```python
# Set unstemmed_singl to the unstemmed version of "single" (which
# should be a string).

```

**Question 1.9:** What word in `vocab_table` was shortened the most by this stemming process? Assign `most_shortened` to the word. *hint: function len(str) will return the length of the input string `str`. You will do a loop over rows of the vocabulary to compute the length of each word.*


```python

```

## Splitting the dataset
We're going to use our `lyrics` dataset for three purposes.  First, we want to *train* various song genre classifiers.  Second, we want to *validate* which classifier is most effective. Finally, we want to *test* the performance of our final classifier. Hence, we need three different datasets: *training*, *validation*, and *test*.

The purpose of a classifier is to generalize to unseen data that is similar to the training data. Therefore, we must ensure that there are no songs that appear in two different sets. We do so by splitting the dataset randomly. The dataset has already been permuted randomly, so it's easy to split.  We just take the top for training, the next part for validation, and the last for test. 

**Question 1.10**: Split the data with the ratio `80%` for training and `20%` for testing. 


```python

```

**Question 1.11**: Draw a horizontal bar chart with three bars that shows the proportion of Country songs in each of the training and testing datasets.

# 2. K-Nearest Neighbors (20 points)

K-Nearest Neighbors (k-NN) is a classification algorithm.  Given some *features* of an unseen example, it decides whether that example belongs to one or the other of two categories based on its similarity to previously seen examples.  

A feature we have about each song is *the proportion of times a particular word appears in the lyrics*, and the categories are two music genres: hip-hop and country.  The algorithm requires many previously seen examples for which both the features and categories are known: that's the `train_lyrics` table.

We're going to visualize the algorithm, instead of just describing it. To get started, let's pick colors for the genres.


```python
# Just run this cell to define genre_color.

def genre_color(genre):
    """Assign a color to each genre."""
    if genre == 'Country':
        return 'gold'
    elif genre == 'Hip-hop':
        return 'blue'
    else:
        return 'green'
```


```python
genre_color('Country')
```




    'gold'




```python
genre_color('Hip-hop')
```




    'blue'



## Classifying a  song

In k-NN, we classify a song by finding the `k` songs in the *training set* that are most similar according to the features we choose. We call those songs with similar features the "neighbors".  The k-NN algorithm assigns the song to the most common category among its `k` neighbors.

Let's limit ourselves to just 2 features for now, so we can plot each song.  The features we will use are the proportions of the words "like" and "love" in the lyrics.  Taking the song "In Your Eyes" (in the test set), 0.0119 of its words are "like" and 0.0595 are "love". This song appears in the test set, so let's imagine that we don't yet know its genre.

First, we need to make our notion of similarity more precise.  We will say that the *dissimilarity*, or *distance* between two songs is the straight-line distance between them when we plot their features in a scatter diagram. This distance is called the Euclidean ("yoo-KLID-ee-un") distance.  

For example, in the song *Insane in the Brain* (in the training set), 0.0203 of all the words in the song are "like" and 0 are "love".  Its distance from *In Your Eyes* on this 2-word feature set is $\sqrt{(0.0119 - 0.0203)^2 + (0.0595 - 0)^2} \approx 0.06$.  (If we included more or different features, the distance could be different.)

A third song, *Sangria Wine* (in the training set), is 0.0044 "like" and 0.0925 "love".



**Question 2.1**: Define a function that creates a plot to display a test song and some training songs in a two-dimensional space defined by two features. Utilize the function to visualize the songs *In Your Eyes*, *Sangria Wine*, and *Insane in the Brain*.

hint: the function has four arguments and it does not return anything but it plots the songs in 2D space:

* test_song: has string datatype, is the name of a song
* training_songs: has list datatype, is a list of songs
* x_feature: has string datatype, is the name of a feature.
* y_feature: has string datatype, is the name of another feature.


```python
import matplotlib.pyplot as plt

def plot_with_two_features(test_song, training_songs, x_feature, y_feature):
    """Plot a test song and training songs using two features."""

```


```python
# visualize the distances of the songs In Your Eyes, Sangria Wine, and Insane in the Brain.
training = ["Sangria Wine", "Insane In The Brain"]
test_song = "In Your Eyes"
plot_with_two_features(test_song, training, "like", "love")
```

**Question 2.2**: Utilize the `plot_with_two_features` function and plot the positions of the three songs *Sangria Wine*, *Lookin' for Love*, *Insane In The Brain* together with the song *In Your Eyes*. Which one is closer to *In Your Eyes* and what is its genre?

**Question 2.3.** Complete the function `distance_two_features` that computes the Euclidean distance between any two songs, using two features. Utilize the function `distance_two_features`  to show that *Lookin' for Love* is closer to *In Your Eyes* than *Insane In The Brain*. 


```python
import math as m

def distance_two_features(title0, title1, x_feature, y_feature):
    """Compute the distance between two songs, represented as rows."""
    
    return ...
```

The nearest neighbor to a song is the example in the training set that has the smallest distance from that song.

**Question 2.4.**  What are the names and genres of the 7 closest songs to "In Your Eyes" in  `train_lyrics`, by Euclidean distance for the 2 features "like" and "love"?  To answer this question, make a dataframe named `close_songs` containing those 7 songs with columns "Title", "Artist", "Genre", "like", and "love" from the `lyrics` dataframe, as well as a column called `distance` that contains the distance from "In Your Eyes" **sorted in ascending order**.


```python

```

**Question 2.5 .** Find the most common value in the column `Genre` of the dataframe `close_songs`. In case of a tie, it can return any of the most common values.


```python

```

Congratulations are in order -- you've classified your first song!

# 3. Features (20 points)

Now, we're going to extend our classifier to consider more than two features at a time.

Euclidean distance still makes sense with more than two features. For `n` different features, we compute the difference between corresponding feature values for two songs, square each of the `n`  differences, sum up the resulting numbers, and take the square root of the sum.

#### Question 3.1
Write a function to compute the Euclidean distance between two **arrays** of features of *arbitrary* (but equal) length.  Use it to compute the distance between the first song in the training set and the first song in the test set, *using all of the features*.  (Remember that the title, artist, and genre of the songs are not features.)

**Hint:** The function has two arguments which are two arrays representing the two lists of features: 


```python
import numpy as np

def distance(features1, features2):
    """The Euclidean distance between two arrays of feature values."""
    
    return ...
```

## Creating your own feature set

Unfortunately, using all of the features has some downsides.  One clear downside is *computational* -- computing Euclidean distances just takes a long time when we have lots of features.  You might have noticed that in the last question!

So we're going to select just 20.  We'd like to choose features that are very *discriminative*. That is, features which lead us to correctly classify as much of the test set as possible.  This process of choosing features that will make a classifier work well is sometimes called *feature selection*, or more broadly *feature engineering*.

#### Question 3.2
Look through the list of features (the labels of the `lyrics` table after the first three).  Choose 20 common words that you think might let you distinguish between country and hip-hop songs. Make sure to choose words that are frequent enough that every song contains at least one of them. Don't just choose the 20 most frequent, though... you can do much better.

The first time you answer this question, spend some time looking through the features, but not more than 15 minutes.


```python

```

#### Question 3.3
In two sentences or less, describe how you selected your features. 


```python

```

#### Question 3.4
Use the `distance` function developed above to compute the distance from the first song in the test set to all the songs in the training set, **using your set of 20 features**.  Make a new dataframe called `genre_and_distances` with one row for each song in the training set and two columns:
* The `"Genre"` of the training song
* The `"Distance"` from the first song in the test set 

Ensure that `genre_and_distances` is **sorted in increasing order by distance to the first test song**.


```python

```

#### Question 3.5
Now compute the 5-nearest neighbors classification of the first song in the test set.  That is, decide on its genre by finding the most common genre among its 5 nearest neighbors, according to the distances you've calculated.  Then check whether your classifier chose the right genre.  (Depending on the features you chose, your classifier might not get this song right, and that's okay.)


```python

```

## A classifier function

Now it's time to write a single function that encapsulates this whole process of classification.

**Question 3.6.** Write a function called `classify`.  It should take the following arguments:
* An array of features for a song to classify ,
* A dataframe has similar structure of the original dataset,
* `k`, the number of neighbors to use in classification.

It should return the class your classifier picks for the given row of features (e.g., `'Country'` or `'Hip-hop'`). Test if the function works by classifying the first song in the test set using k=5.


```python
def classify(test_features, train_dataframe, k):
    """Return the most common class among k nearest neigbors to test_row."""

    return ...
```


```python

```

**Question 3.7.** Assign `grandpa_genre` to the genre predicted by your classifier for the song  "Grandpa Got Runned Over By A John Deere", using 9 neigbors.


```python

```

## Evaluating your classifier

Now that it's easy to use the classifier, let's see how accurate it is on the whole test set. But we will reduce the test set to 20 songs only to save computing power.

**Question 3.8.** Generate a new test set of 20 songs from your current test set


```python

```

**Question 3.9.** Classify every song in the newly generated test set, then compute the proportion of correct classifications. (It may take some minutes to complete the classification of these 20 songs)


```python

```

At this point, you've gone through one cycle of classifier design.  Let's summarize the steps:
1. From available data, select test and training sets.
2. Choose an algorithm you're going to use for classification.
3. Identify some features.
4. Define a classifier function using your features and the training set.
5. Evaluate its performance (the proportion of correct classifications) on the test set.


# 4. Feature design (15 points)

One way to interpret the accuracy of a classifier is to compare it to another classifier.

**Question 4.1.** Below we've provided 10 features selected by the staff `["come", "do", "have", "heart", "make", "never", "now", "wanna", "with", "yo"]`.  Build a 5-nearest-neighbor classifier using these features and compute its accuracy on the test set. 


```python

```

**Question 4.2.** Are the features you chose better or worse than the staff features at classifying the test set? Why do you think this is so?


```python

```

**Question 4.3.** Is there anything random about a classifier's accuracy measured in this way?  Is it possible that the difference in classifier performance is due to chance?  If so, describe (in 2-3 sentences) how you would investigate that.


```python

```

# 5. Computational thinking (15 points)

**<span style="color:red">The following questions are answered via a video of no more than 5 minutes. Everybody must speak. You will provide the link to that video in the answer box.</span>**

**Question 5.1**: Specifically refer to some lines of code, or the thought processes that you made in all the above solutions to elaborate computational concepts which are used in solving the project.


```python

```

**Question 5.2**: How did you work as a team to complete the project?


```python

```

**Question 5.3** (Optional - no credit): Draw a picture (or better yet, a data visualization) of life before, during, and/or after taking Computational Thinking with Data Science course.


```python

```
