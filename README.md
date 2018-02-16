# Deduplication Problem
#### ~ Solution by Shubham Barudwale

This program is developed to identify and extract the unique names from the list of multiple entries of names. This solution is developed using `fuzzy logic` which uses `Levenshtein distance` to find the similarity in the names and other fields in table.

## Problem with detailed explanation

A data given is the table containing various names of people and their details. Four fields given are **First name, Last Name, Gender and Date of Birth.** From these four fields we have to find out how many distinct people are present in the dataset.

#### Challenge:
The main challenge in this type of question is the person can write his/her name in many different ways which can be ambiguous. For example,

John Franklin Kennedy can write his name in following possible ways:
```
  - John Franklin Kennedy
  - John F. Kennedy
  - John F Kennedy
  - John Kennedy
  - Kennedy John F.
```
and so on...

So, it is very difficult to predict if all of them are same person's name or not.
As we are given date of birth and gender of each individual the problem becomes more feasible than taking only names in account.

Even after taking the names and date of birth into account there might be some ambiguous names which are difficult to identify. For example,
```
   - John F Kennedy            M    19/12/1998
   - John Fernando Kennedy     M    19/12/1998
```
If we consider this situation where first person is actually John Franklin Kennedy and second one is John Fernando Kennedy in above comparison one can think that both are same.

So likewise, many situations can happen which can lead answer to wrong decision.
Looking at the problem we need to specify how many exact distinct people are present in the given dataset.


## Approach to Solve problem

Even if many misleading names are possible in the data we are given two main factors of each individual to reduce the error that is **Gender and Date of Birth.**

1) To reduce chances of false matching of names I first sorted the given data with columns date of birth, Gender, First Name and Last Name accordingly. This provides the ordered distinction between each entry by Date of Birth and Gender.
2) Add a column in data Frame by concatenating First and Last Name for further process.
3) Now take each individual name entry from newly created name (by appending First Name and Last Name) and push it to list until all the other attributes e.g. Date of Birth and Gender are same.
4) Now apply Fuzzy matching on those similar names to find out distinct name. Fuzzy String matching uses Levenshtein distance with threshold value to identify distinct strings. (I have used threshold value as 90)
5) Store all distinct names and print them.

This approach gives all the 51 distinct names in the list of 104 names correctly.

## Implementation Requirements
Following libraries are required for implementation of the given code.

```
 Pandas      :  $ pip install pandas
 Numpy       :  $ pip install numpy
 FuzzyWuzzy  : $ pip install fuzzywuzzy
 Levenshtein : $ sudo apt-get install python-levenshtein
```

## 	

In information theory, Linguistics and computer science, the `Levenshtein distance` is a string metric for measuring the difference between two sequences. Informally, the Levenshtein distance between two words is the minimum number of single-character edits (insertions, deletions or substitutions) required to change one word into the other. Levenshtein distance may also be referred to as `edit distance`.

#### Implementation of Levenshtein Distance
```py
//len_s and len_t are the number of characters in string s and t respectively

int LevenshteinDistance(const char *s, int len_s, const char *t, int len_t)
{
  int cost;

  /* base case: empty strings

  if (len_s == 0) return len_t;
  if (len_t == 0) return len_s;

  /* test if last characters of the strings match */
  if (s[len_s-1] == t[len_t-1])
      cost = 0;
  else
      cost = 1;

  /* return minimum of delete char from s, delete char from t, and delete char from both */
  return minimum(LevenshteinDistance(s, len_s - 1, t, len_t    ) + 1,
                 LevenshteinDistance(s, len_s    , t, len_t - 1) + 1,
                 LevenshteinDistance(s, len_s - 1, t, len_t - 1) + cost);
}
```
