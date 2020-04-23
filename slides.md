---
title: 'Class 7: Chapter 13: Case Study: data structure'
separator: '\-\-\-\-\-'
verticalSeparator: '\+\+\+\+\+'
theme: 'moon'
revealOptions:
    transition: 'fade'
---

### ITSE-1042 Intermediate Python

-----

##### Chapter 13: Case Study: data structure

+++++

Notes:
- Tuples add value with multiple outputs in returns and multiple inputs


The str type methods in the Python Standard Library are helpful for word problem analysis and changes: 
- Text Sequence Type str
-- https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str   
- String Methods   
-- https://docs.python.org/3/library/stdtypes.html#string-methods     
-- https://www.w3schools.com/python/python_ref_string.asp    
-- Examples: str.replace, str.split, str.strip, str.lstrip, str.lstrip, str.upper, str.lower, str.splitlines, 
   str.ljust, str.rjust, etc   
- Whitespace characters are typically a space, tab, or formfeed 
- The string module in Python contains two useful predefined strings:   
-- string.punctuation - String of characters which are considered the punctuation characters in the current locale.   
-- string.whitespace - String containing all characters that are considered whitespace. These characters are usually
space, tab, linefeed, return, formfeed, and vertical tab.   
- The datastucutres in Python provide useful methods for manipulating a lists and dictionary/histogram (ex. the sort method):       
-- https://docs.python.org/3/tutorial/datastructures.html   
-- https://docs.python.org/3/howto/sorting.html   



+++++

##### Case study: data structure

+++++

##### 13.1 Word frequency analysis

+++++

<pre class="stretch"><code class="python" data-trim data-noescape>
#!/usr/bin/env python3

# Exercise 13.1
#
# 1. Write a function named "strip_and_lower" that reads "emma.txt", breaks each 
# line into words, strips whitespace and punctuation from the words, and 
# converts them to lowercase. Nothing should be returned at this time. 
#
# Hint: The string module provides a string named "whitespace", which contains 
# space, tab, newline, etc., and "punctuation" which contains the punctuation
# characters. Let's see if we can make Python swear:
#
# >>> import string
# >>> string.punctuation
# '!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~'
</code></pre>

+++++

<pre class="stretch"><code class="python" data-trim data-noescape>
#!/usr/bin/env python3

# Exercise 13.2
#
# 1. Modify your function from the previous exercise to skip over the header 
# information at the beginning of the file, and process the rest of the words 
# as before. Then modify the function to count the total number of words in 
# the book, and the number of times each word is used. Use a histogram to
# collect this info and return that dictionary -- where the key is the word 
# and the value is the number of times it occured. 
</code></pre>

+++++

<pre class="stretch"><code class="python" data-trim data-noescape>
#!/usr/bin/env python3

# Exercise 13.3
#
# Question 1
# 1. Modify the function from the previous exercise to return a list of the
# 20 most frequently used words in the book in order of usage, decending.
</code></pre>

+++++

##### 13.2 Random Numbers

+++++

Most computers are deterministic and provid the same outputs for the same inputs everytime. This can be undesirable in some cases where you would want a unpredicable output. A good example of this is with gaming. 

+++++

Truly nondeterministic is hard to accomplish, but we can make it seem so pretty easily using the random model (that is actually more of a psudorandom module.

+++++

The function random returns a random float between 0.0 and 1.0 (including 0.0 but not 1.0).

```python
import random
for i in range(10):
    x = random.random()
    print(x)
# Example Output:
# 0.7198071255818801
# 0.5938534709819878
# 0.3569282483020323
# 0.902230923916121
# 0.4779205640671651
# 0.38543858569616263
# 0.31952247933914135
# 0.10524277242134572
# 0.8906385919234846
# 0.4154703646191147
```
+++++

The function randint takes parameters low and high and returns an integer between low and high (including both).

```python
random.randint(5, 10)
# 5
random.randint(5, 10)
# 9
```

+++++

To choose an element from a sequence at random, you can use choice:

```python
t = [1, 2, 3]
random.choice(t)
# 2
random.choice(t)
# 3
```

+++++

##### 13.3 Word histogram

Here is a program that reads a file and builds a histogram of the words in the file:

```python
import string
def process_file(filename):
    hist = dict()
    fp = open(filename)
    for line in fp:
        process_line(line, hist)
    return hist
    
def process_line(line, hist):
    line = line.replace('-', ' ')
    for word in line.split():
        word = word.strip(string.punctuation + string.whitespace)
        word = word.lower()
        hist[word] = hist.get(word, 0) + 1

hist = process_file('emma.txt')
```

Note:
This program reads emma.txt, which contains the text of Emma by Jane Austen.
process_file loops through the lines of the file, passing them one at a time to
process_line. The histogram hist is being used as an accumulator.
process_line uses the string method replace to replace hyphens with spaces before using
split to break the line into a list of strings. It traverses the list of words and uses strip
and lower to remove punctuation and convert to lower case. (It is a shorthand to say that
strings are “converted”; remember that strings are immutable, so methods like strip and
lower return new strings.)
Finally, process_line updates the histogram by creating a new item or incrementing an
existing one.

+++++

To count the total number of words in the file, we can add up the frequencies in the histogram:

```python
def total_words(hist):
    return sum(hist.values())
```    
    
+++++

The number of different words is just the number of items in the dictionary:

```python
def different_words(hist):
    return len(hist)
```

+++++

##### 13.4 Most common words

+++++

To find the most common words, we can make a list of tuples, where each tuple contains a word and its frequency, and sort it.

+++++

The following function takes a histogram and returns a list of word-frequency tuples:

```python
def most_common(hist):
    t = []
    for key, value in hist.items():
        t.append((value, key))
        t.sort(reverse=True)
    return t
```

Note:
In each tuple, the frequency appears first, so the resulting list is sorted by frequency. 

+++++

Here is a loop that prints the ten most common words:

```python
t = most_common(hist)
print('The most common words are:')
for freq, word in t[:10]:
    print(word, freq, sep='\t')
```

Note:
I use the keyword argument sep to tell print to use a tab character as a “separator”, rather
than a space, so the second column is lined up.
This code can be simplified using the key parameter of the sort function. If you are curious,
you can read about it at https://wiki.python.org/moin/HowTo/Sorting

+++++

##### 13.5 Optional parameters

+++++

We have seen built-in functions and methods that take optional arguments. It is possible to write programmer-defined functions with optional arguments, too.

Here is a function that prints the most common words in a histogram:

```python
def print_most_common(hist, num=10):
    t = most_common(hist)
    print('The most common words are:') 
    for freq, word in t[:num]:
        print(word, freq, sep='\t')
```

Note:
The first parameter is required; the second is optional. The default value of num is 10.

+++++

If you only provide one argument:

```python
print_most_common(hist)
```

num gets the default value. 

If you provide two arguments:

```python
print_most_common(hist, 20)
```

num gets the value of the argument instead. 

Note:
In other words, the optional argument overrides the default value.
If a function has both required and optional parameters, all the required parameters have
to come first, followed by the optional ones.

+++++

##### 13.6 Dictionary subtraction

+++++

Finding the words from the book that are not in the word list from words.txt is a problem
you might recognize as set subtraction.

Note:
that is, we want to find all the words from one set (the words in the book) that are not in the other (the words in the list).

+++++

subtract takes dictionaries d1 and d2 and returns a new dictionary that contains all the keys from d1 that are not in d2.

```python
def subtract(d1, d2):
    res = dict()
    for key in d1:
        if key not in d2:
        res[key] = None
    return res
```

+++++

To find the words in the book that are not in words.txt, we can use process_file to build a histogram for words.txt, and then subtract:

```python
words = process_file('words.txt')
diff = subtract(hist, words)
print("Words in the book that aren't in the word list:")
for word in diff:
    print(word, end=' ')
```

+++++

##### 13.7 Random words

+++++

To choose a random word from the histogram, the simplest algorithm is to build a list with multiple copies of each word, according to the observed frequency, and then choose from the list:

```python
def random_word(h):
    t = []
    for word, freq in h.items():
        t.extend([word] * freq)
    return random.choice(t)
```

The expression [word] * freq creates a list with freq copies of the string word. 

Note: 
The extend method is similar to append except that the argument is a sequence.
This algorithm works, but it is not very efficient; each time you choose a random word, it
rebuilds the list, which is as big as the original book. An obvious improvement is to build
the list once and then make multiple selections, but the list is still big.

+++++

An alternative is:

1. Use keys to get a list of the words in the book.
2. Build a list that contains the cumulative sum of the word frequencies (see Exercise 10.2). The last item in this list is the total number of words in the book, n.
3. Choose a random number from 1 to n. Use a bisection search (See Exercise 10.10) to find the index where the random number would be inserted in the cumulative sum.
4. Use the index to find the corresponding word in the word list.

+++++

Homework is 13.4 and 13.5
