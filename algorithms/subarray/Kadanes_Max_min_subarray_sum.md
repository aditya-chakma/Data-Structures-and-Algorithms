# Kadanes Algorithm

Problem: **Find sum of subarray with maximum sum**

If we are to find the sum of a subarray with maximum sum, we need to iterate through all possible subarrays and find the maximum sum of its elements. First, find the start and end of a subarray <b>O(n<sup>2</sup>)</b>. For each of these subarray's calculate the sum. This would take <b>O(n<sup>3</sup>)</b> time.

```Java
int maxSum = nums[0];
for (int start = 0; start < len; i++) {
    for (int end = start + 1; end <= len; end ++) {
        int currentSum = 0;
        // find subarray elements sum for subarrays starting at `start` and ending at `end`
        for (int i = start; i < end; i++) {
            currentSum += nums[i];
        }
        currentSum = Math.max(maxSum, currentSum);
    }
}
```

We can optimize this brute for approach. If we notice, we find that, the prefix sum is same for all subarrays starting at a particular potision. With this simple observation, we can ommit the last loop. And the time complexity becomes <b>O(n<sup>2</sup>)</b>

```Java
int maxSum = nums[0];
for (int start = 0; start < len; start++) {
    int currSum = 0;
    for (int end = start; end < len; end++) {
        currSum += nums[end];
        maxSum = Math.max(maxSum, currSum);
    }
}
```

Kadanes algorithm is used to find max or min subarray sum in `O(n)` time.

## Algorithm

Kadanes algorithm uses a simple trick. In case of maximization problem, we need to maximize the subarray sum. The subarray might contain positive and negative numbers. If we observe carefully, we will notice that, negative numbers do not contribute in maximizing the subarray sum. However, we can not entirely discard them, as they might lead to a better sum result.

```Java
arr1 = {-1, -2, -3}
arr2 = {10, -5, 20}
```

If we keep summing elements of `arr1`, the total sum would keep getting smaller. Hence, we discard the negative numbers. On the other hand, if we discard `-5` and restart the subarray, the sum would be 20, whereas the maximum sum is 25. Hence, we need a way to tell when to restart the subarray.

Notice that, if the current running sum becomes negative, summing with the array will also become negative, and it would not contribute to the maximum sum. If we ever encounter a negative running sum, we can safely discard it.

### Here is the algorithm

* Initialize `maxSum` to be negative infinite.
* Initialize `currentSum` to zero.
* For each `element` in `nums`
  * Add `element` to currentSum
  * Take maximum between `maxSum` and `currentSum`
  * If `currentSum` is less than zero, set `currentSum` to zero

### Code

```Java
int maxSum = Integer.MIN_VALUE;
int currentSum = 0;
for (int num : nums) {
    currentSum += num;
    maxSum = Math.max(maxSum, currentSum);
    currentSum = Math.max(currentSum, 0);
}
```

### Analysis

* Time Complexity: `O(n)`. The algorithm runs through each element, which takes `O(n)` time. For each element, we calculate the `currentSum`, and `maxSum`. This takes `O(1)` time. Hence the total time complexity is `O(n)`.
* Space complexity: `O(1)`. The algorithm does not take any extra space. Hence, the space complexity is `O(1)`.
