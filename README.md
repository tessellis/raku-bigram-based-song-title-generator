# raku-bigram-based-song-title-generator
An automatic bigram-based Raku program that generates song titles given a seed word based on the statistical occurrences of word pairs across the One Million Song Dataset

# Program Description
## Bigram Counts
A bigramLinks to an external site. is a sequence of two adjacent words in a text. The frequency distribution of bigrams, or more generally n-grams, in text data is  commonly used in statistical natural language processing. Across this corpus of one million song titles, you will count all the bigram words.

First, you need split the title string into individual words. Next, you should use an associative array to keep track of these word pair counts. That is, for every word, you must keep track of the count for each word that follows it. More specifically, use the variable ``` %counts ``` as a hash of hashes. The first key is 
, the second key is 
 , and the value is the count of the number of times that words 
  and 
  appear sequentially in song titles across the entire corpus.

Complete the function build bigrams. Here is some pseudocode that describes the task.
```
foreach title in tracks array
  split title into individual words
    if there is more than one word
      while there are adjacent word pairs
        update count for word pair by 1
      end while
    end if
end foreach
```

## Most Common Word
Now you are going to build a probabilistic song title. First begin by completing the function "most common word" ``` mcw ```. This function takes in one argument, some word, and returns the word that most often followed that word in the dataset.

When you first extract all possible successive words to the given seed word, sort the set of keys. When comparing counts and you encounter a tie, stick with the first word found. This ensures that you will get the same results as the grading test cases. 

You can now use the command  ``` mcw WORD ```, where ``` WORD ``` is the argument passed to the function.

## Building a Song Title
Now you are going to use this ``` mcw ``` function to string together a song title. Beginning with a given starting word, write an iterative structure that strings together words that most commonly follow each other in the dataset. Continue until a word does not have a successive word in the dataset (check for whitespace or newline) or the count of words in your title reaches the variable ``` $SEQUENCE_LENGTH ```. Complete the function ``` sequence ```.

You can now use the command ```sequence WORD``` where ```WORD``` is the seed word. 

## Unwanted Recursion
As you examine your new song titles, you probably notice a lot of repeated phrases such as "of the world" and "ready for you". Think about why that happens.

This repetition happens because these words occurred very often in either order of each other in the corpus. We can fix this repetition by allowing each word to appear in the title only once. 

Add a data structure to track the word history. The empty hash ```%word_history``` is provided as a global variable. Edit ```sequence``` so that every time a word is used in your title it is added it to word history. Treat ```%word_history``` as map to Booleans values (0 or 1) in which ```%word_history{"word"}=1``` indicates that the word word has been seen before. If a word has not been seen before ```%word_history{"word"}``` conveniently returns the default value of ```undefined```. 

Next go back and edit the ```mcw``` function. Presently, it picks the most common word to follow the seed word. Modify this so that it picks the most common word only if it has not yet been used in the sequence. If the most common word has already been used, pick the next most common word, and so on.

Make sure you clear your word history every time that ```sequence``` is called. The history should start over for each new sequence.

## Menu System
| command | argument | description |
|---|---|---|
| ```build``` |	| build the bigram model |
| ```debug``` | on | turn on debug mode |
| | off | turn off debug mode |
| ```count``` | tracks | counts tracks in ```@tracks``` |
| | words | counts words in @tracks |
| | characters | counts tracks in ```@tracks``` |
| | characters | counts tracks in ```@tracks``` |
| ```filter``` | title | extract title from original input |
|  | comments | removes extra phrases |
|  | punctuation | removes extra punctuation |
|  | unicode | removes non-Unicode and whitespace |
| ```load``` | ```FILE``` | loads the given ```FILE``` |
| ```length``` |	```INT```	| update ```$SEQUENCE LENGTH=INT``` |
| ```mcw``` |	```WORD``` | print most common word to follow WORD |
| ```name``` | | print sequence based on your name |
| ```preprocess``` | |		run all filter tasks and build |
| ```print```	| | ```INT``` | prints all tracks to file ```tracks.out``` |
| | | ```INT``` | prints only ```INT``` tracks to ```stdout``` |
| ```random``` | | |	print sequence based on random word |
| ```stopwords```	| on | filter stopwords on |
| | off | filter stopwords off |
| ```sequence``` | ```WORD``` | find sequence to follow ```WORD``` |

## Testing
In the directory tests you will find a number of pairs of files representing the given input and expected output of the test.

``` raku lab2.raku < ./tests/t01.in ```
The above line will execute lab2.raku piping in the commands given in file t01.in. You can compare your result with the expected output given in file t01.out.

Test t01 checks mcw.

Test t02 checks sequence.


