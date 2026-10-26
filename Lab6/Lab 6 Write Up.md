# Lab 6
## Code

```java
class Solution {
    public int findJudge(int n, int[][] trust) {
        if(n == 1)
            return 1;
        int[] truster = new int[n +1];
        int[] trustee = new int[n+1];
        for(int i = 0; i < trust.length; i++)
        {
            int trusterIndex = trust[i][0];
            truster[trusterIndex]++;
            int trusteeIndex = trust[i][1];
            trustee[trusteeIndex]++;

        }

        for(int i = 1; i <= n; i++)
        {
            if(truster[i] == 0 && trustee[i] == n -1)
                return i;
        }
        return -1;
    }
}
```

## Description:
For this problem, we were given n people in a town and a list of trust relationships, where each pair [a,b] means person a trusts person b. We had to find the person who trusts no one and who everyone trusts or return -1 if no such person exists. To do this, I used two counting arrays; one tracking how many people each person trusts and one tracking how many people trust each person. First, I handle the edge case where n is 1, since the only person is automatically the judge. Then I loop through the trust list once, incrementing the truster count for the first person in each pair and the trustee count for the second. Finally, I loop through each person from 1 to n and return the one who trusts nobody (truster count of 0) and is trusted by everyone else (trustee count of n - 1). If no one meets both conditions, I return -1.

## Runtime Analysis: 
My program takes O(n + t), where n is the number of people and t is the length of the trust array. Looping through the trust list takes O(t), and the final loop over the people takes O(n).

## Space Complexity:
I created two new arrays the size of n, so space complexity is linear as it is O(2n) which simplifies to O(n).
