# COMP10001-Foundations-of-Computing
COMP10001 Foundations of Computing S2

Q1
Write a function non_increasing_tst(ts, delta) that returns a Boolean value indicating whether the time series is 'non-increasing', i.e., successive values never increase by more than a given threshold.

The function takes two arguments,

ts: a time series as a list of integers, containing at least two values.
delta: an integer ≥ 0 such that the positive change between two successive values in the time series must be greater than delta for the change to be considered as an 'increase'.
The function should return True if there is no pair of consecutive values ts[i] and ts[i+1] in the time series such that (ts[i+1] – ts[i]) > delta, or False otherwise.

You can assume that the input arguments are correctly formatted.

For example- you are given a time series in the form of a list of integers e.g., the daily Covid case count leckietopia = [58, 54, 54, 52, 54, 50, 47]

The time series in leckietopia has a small increase from 52 to 54 However, if we tolerate noise of at least 2 in the differences between successive readings, then this time series could be considered to be consistently falling or steady, i.e., 'non-increasing'.

Here are some example calls to the function:

>>> leckietopia = [58, 54, 54, 52, 54, 50, 47]
>>> print(non_increasing_tst(leckietopia, 0))
False
>>> print(non_increasing_tst(leckietopia, 1))
False
>>> print(non_increasing_tst(leckietopia, 2))
True
>>> print(non_increasing_tst([100, 90, 80, 70, 70, 60], 0))
True

------*-------*--------*--------*--------*--------*---------*---------*---------*---------*----------*---------*---------*-------*-------*-------*------------------------

Q2
We might be interested in testing whether a time series contains a particular 'pattern', such as two decreases in value in successive values (e.g., the definition of a recession), or a sequence of alternating increases and decreases (e.g., a steady breathing rhythm in a patient).

To do this we first need to a way to specify the pattern to search for. We will represent a pattern as a string, which can contain the characters 'u' for up (or increase), 'd' for down (or decrease), and 's' for steady (no change). For example, 'dd' represents two successive decreases in value, 'ud' represents an increase in value followed by a decrease, 'dssu' represents a decrease in value followed by two steady values followed by an increase.

Write a function contains_tst(ts, pattern, delta) that returns whether the given time series matches the given pattern.

The parameters of this function are as follows:

ts: a time series as a list of integers, containing at least two values
pattern: a string of one or more characters, where the possible characters that can appear in pattern are 'u', 's' and 'd'
delta: an integer ≥ 0 such that the absolute value of the change between two successive values in the time series must be less than or equal to delta for the two successive values to be considered steady ('s')
The function returns True if given pattern matches a sequence of consecutive values in ts and if not, returns False.

Assumptions:

You can assume that the input arguments are syntactically correct given the description on this and on the previous slides.
Here are some example calls to the function:

>>> leckietopia = [58, 54, 54, 52, 54, 50, 47]
>>> print(contains_tst(leckietopia, 'sdud', 0))
True
>>> print(contains_tst(leckietopia, 'sdud', 2))
False
>>> print(contains_tst(leckietopia, 'sss', 2))
True
>>> print(contains_tst(leckietopia, 'dd', 0))
True
>>> print(contains_tst([1, 2, 1, 8, 1, 2], 'udud', 0))
True
>>> print(contains_tst([1, 2, 1, 8, 1, 2], 'udud', 2))
False

------*-------*--------*--------*--------*--------*---------*---------*---------*---------*----------*---------*---------*-------*-------*-------*------------------------

Q3
Write a function closest_tst(ts, ts_list) that given a time series ts, and a list of time series ts_list, returns the index of the time series in ts_list that has the smallest distance to ts (i.e., is most similar to ts):

The function takes the following arguments,

ts: a time series as a list of integers, containing at least two values
ts_list: a list of one or more time series, where each time series in ts_list is a list of integers, and has the same length as ts
The function returns an integer corresponding to index of the time series in ts_list that has the smallest distance to ts (if there are multiple time series in ts_list that have the equal smallest distance to ts, then return the index of the first such time series)

Assumptions

You can assume that the input arguments are correctly formatted and all time series have the same length.
Here are some example calls to your function:

>>> t1 = [10, 10, 10, 10]
>>> t2 = [10, 10, 20, 20]
>>> t3 = [0, 0, 40, 40]
>>> t4 = [100, 100, 100, 100]
>>> t5 = [10, 10, 20, 10]
>>> print(closest_tst(t1, [t3, t2, t1]))
2
>>> print(closest_tst(t4, [t1, t2, t3]))
0
>>> print(closest_tst(t1, [t2, t5]))
1

------*-------*--------*--------*--------*--------*---------*---------*---------*---------*----------*---------*---------*-------*-------*-------*------------------------

Q4
Write a function anomaly_tst(ts, w, threshold) that given a time series ts, a subsequence length w, and an anomaly cut-off threshold threshold , returns the index of the subsequence in ts that has the highest mean distance above the threshold (or -1 if no subsequence has a mean distance above the threshold). If there is more than one subsequence that has the same mean distance that is the max and above the threshold, then return the index of the first such time series.

The function takes the following parameters:

ts: a time series as a list of integers, containing at least two values
w: an integer > 0 that specifies the length of subsequences
threshold: a integer > 0, where the mean distance of a subsequence must be greater than this threshold if it is to be considered as an anomaly.
Assumptions:

You can assume that the input arguments are correctly formatted.
Here are some example calls to your function:

>>> ts = [3, 0, 2, 40, 1]
>>> print(anomaly_tst(ts, 2, 40))
2
>>> print(anomaly_tst(ts, 2, 100))
-1
>>> print(anomaly_tst([10, 10, 10, 10, 0, 0, 10], 2, 12))
4
>>> print(anomaly_tst([10, 10, 10, 10, 10, 10, 10], 3, 12))
-1
