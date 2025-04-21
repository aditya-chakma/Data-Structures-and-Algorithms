# Bits reverse

Bits reverse is a typical computer science problem. We can reverse bits in multiple ways and here are some awesome engineering solution to this simple problem.

## Bit by bit

We can reverse bits of a number bit by bit. Start by processing from the LSB or the rightmost bit and slowly move left checking each bit and update.

### Algorithm

Start with the LSB or the rightmost bit. Check the bit and append the bit to resulting number.

```Java
private int reverse(int num) {
    int reversedNum = 0;

    for (int i = 0; i < 32; i++) {
        // shift result by 1 bit to make space for the new bit
        reversedNum <<= 1;

        // check the rightmost bit
        if (num & 1 != 0) {
            reversedNum != 1;
        }

        // move num by 1 bit
        num >>= 1;
    }

    return reversedNum;
}
```

**Time complexity:** `O(1)`
**Space complexity:** `O(1)`

## Reverse by blocks of 8

What if the reverse method is called multiple times? Maybe we call the method for same number more than once. In that case, we will have to do the same calculation multiple times. We can avoid this calculation by storing the already calculated result in a map and access the result in O(1) time.

