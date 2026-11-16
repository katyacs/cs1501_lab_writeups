# Lab 9 Write-Up

## Code

```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        int [] arr = new int[n];
        for(int i = 0; i < n; i++)
        {
            if(i < 2) //if i is 1 or 0
                arr[i] = cost[i];
            else
            {
                int min = Math.min(arr[i-1], arr[i-2]);
                arr[i] = cost[i] + min;
            }     
        }
        return Math.min(arr[n-1], arr[n-2]);
    }
}
```
## Description
You are given an array cost and cost[i] is the price of stepping on stair i. You can either climb one step or two steps after paying, and you can start at index 0 or 1. 
You have to find the minimum total cost to reach the top, which is the position just past the last stair. 
I used dynamic programming where arr[i] stores the minimum cost to land on stair i, computed as cost[i] + min(arr[i-1], arr[i-2]), and the result will be min(arr[n-1], arr[n-2]).

## Runtime
The runtime is O(n) because a single loop visits each of the n stairs once and does constant work per iteration.

## Memory
The space complexity is O(n) because the arr array stores one value for each of the n stairs.
