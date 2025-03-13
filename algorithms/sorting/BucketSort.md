# Bucket Sort

Bucket sort is a linear sorting algorithm for sorting numbers in a range. Each bucket in bucket sort contains a count for that element.

## Algorithm

In order to work with bucket sort, the maximum and minimum numbers should be known. We iterate through each element and count how many times the element has been seen. The algorithm goes as follows:

* Create an array of size `maxNum`. Initialize the array with zeros.
* Iterate through each element and increase the count.

### Code

```Java
public int[] bucketSort(int[] nums, int maxNum) {
    int[] buckets = new int[maxNum + 1];

    Arrays.sort(buckets, 0);

    for (int num : nums) {
        buckets[num] += 1;
    }

    return buckets;
}
```

### Example

Input array

```java
arr = {1, 5, 9, 2, 1, 3, 10, 4, 2, 2, 1, 5};
```

Output

```java
buckets = [0, 3, 3, 1, 2, 0, 0, 0, 1, 1];
```

## Analysis

* **Time Complexity**: **O(n)**. The algorithm runs through each element (**O(n)**) and increments the count (**O(1)**).
* **Space Complexity**: **O(maxNum)**. A separate array is required to store the counts. The size of the array depends on the maximum number.
