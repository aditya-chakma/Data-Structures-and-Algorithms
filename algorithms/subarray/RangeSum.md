# Range Sum

There are several algorithm for range sum: Fenwick Tree / Binary Index Tree and Segment Tree. These are primary considered data structure. However, in this article we will discuss about a simple applicaiton of range sum.

**The Problem**: You are given an array of size `n` and a 2D array `querry` of size `m`. Each element of `query` consist of 3 integers. The start and end of a range `q[0]` and `q[1]` and `value`. Elements in range `[start, end]` (inclusive) must be incremented by `value`. Return the resulting array after applying the queries.

For example:

```Java
// input
array=[1,2,3,4,5,6], query=[[1,5,1], [4,6,2]]
//output
result=[2,3,4,7,8,8]
```

Explaination:

```Java
// After applying [1,5,1]
result=[2,3,4,5,6,6]
// After applying [4,6,2]
result=[2,3,4,7,8,8]
```

**Brute Force:**
The brute force solution for this problem would be to iterate through the quries, and for each query, apply the changes in the array. But this solution is inefficient, as it would take <b>O(n<sup>2</sup>)</b> operations.

## Algorithm

We do not need to apply these changes immediately. We can store these changes in an array called the diff array. We keep track of the ranges, and also the value that needs to be changed. Finally we do a prefix sum on the diff array, and add the current prefix sum with the value of nums to get the actual answer.

### The algorithm

1. Define an array `diff` of size n + 1;
2. Loop through each query and update diff
3. Loop through diff and compute prefix sum

   a. Calculate the prefix sum and add with num to get the actual answer.

### Code

```Java
    public int[] rangeSum(int[] nums, int[][] queries) {
        int qLen = queries.length;
        int len = nums.length;
        int[] diff = new int[len + 1];

        for (int[] query : queries) {
            int start = query[0];
            int end = query[1];
            int val = query[2];

            diff[start] += val;
            diff[end + 1] -= val;
        }

        int prefixSum = 0;
        for (int i = 0; i < len; i++) {
            prefixSum += diff[i];
            nums[i] += prefixSum;
        }

        return prefixSum;
    }
```

## Analysis

* **Time Complexity**: `O(n)`. Computing diff takes `O(n)` time. And computing the result takes `O(n)` time.
* **Space Complexity**: `O(n)`. We need to store the result array, which takes `O(n)` space.
