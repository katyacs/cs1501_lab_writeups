# Lab 4 Write-Up

## Code

```java
class Solution {
    public int maxProduct(int[] nums) {
        Arrays.sort(nums);
        return((nums[nums.length - 1] -1) *(nums[nums.length - 2] -1));
    }
}
```
## Description
For this problem, you need to find the two greatest integer values in the array given, 
returning the product of the two integers subtracted by one.
To do this I used Arrays.sort in Java and then returned the value of the last index subtracted by one multiplied by the value of the second to last index subtracted by one.
This works because Arrays.sort sorts the array in ascending order so the last two indexes store the maximum two values.

## Complexity Analysis
Sorting, which is the only consequential work that my program does, takes O($n log n$) as Arrays.sort() uses Timsort.
I could have made this more efficient (linear run time) by just using a single loop to keep track of the two max values while traversing the array once.
