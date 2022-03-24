# Partition a set into two subsets such that the difference of subset sums is minimum
Question -> [Partition a set into two subsets such that the difference of subset sums is minimum](https://www.codingninjas.com/codestudio/problems/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum_842494)    

### Recursion
```java
public class Solution {
    public static int minSubsetSumDifference(int[] arr, int n) {
        int totalSum = 0;
        for(int num : arr) totalSum += num;
        return minSubsetSumDifference(n-1, arr, 0, totalSum);
    }
    public static int minSubsetSumDifference(int index, int[] arr, int sum, int totalSum) {
        if(index < 0) {
            int secondSetSum = totalSum - sum;
            return Math.abs(sum - secondSetSum);
        }
        int take = minSubsetSumDifference(index-1, arr, sum+arr[index], totalSum);
        int notTake = minSubsetSumDifference(index-1, arr, sum, totalSum);
        return Math.min(take,notTake);
    }
}
```         
> `Recurrence Realtion` : **T(N) = 2(T(N-1))+C**     
> `Time Complexity` : **O(2<sup>(N)</sup>)**          
> `Space Complexity` : **O(N)**    
---
### Memorization
```java
import java.util.*;
public class Solution {
    public static int minSubsetSumDifference(int[] arr, int n) {
        int totalSum = 0;
        for(int num : arr) totalSum += num;
        int[][] dp = new int[n][totalSum+1];
        for(int[] row : dp) Arrays.fill(row,-1);
        return minSubsetSumDifference(n-1, arr, 0, totalSum, dp);
    }
    public static int minSubsetSumDifference(int index, int[] arr, int sum, int totalSum, int[][] dp) {
        if(index < 0) {
            int secondSetSum = totalSum - sum;
            return Math.abs(sum - secondSetSum);
        }
        if(dp[index][sum] != -1) return dp[index][sum];
        int take = minSubsetSumDifference(index-1, arr, sum+arr[index], totalSum, dp);
        int notTake = minSubsetSumDifference(index-1, arr, sum, totalSum, dp);
        return dp[index][sum] = Math.min(take,notTake);
    }
}

```
> `Time Complexity` : **O(N\*K)**, K = totalSum          
> `Space Complexity` : **O(N)+O(N\*K)**, for Recursion Stack and dp array
---
### Tabulation
```java
public class Solution {
    public static int minSubsetSumDifference(int[] arr, int n) {
        int totalSum = 0;
        for(int num : arr) totalSum += num;
        boolean[][] dp = new boolean[n][totalSum+1];
        // for target sum = 0
        for(int index=0; index<n; index++) {
            dp[index][0] = true;
        }
        // when index=0 and target=arr[0]
        dp[0][arr[0]] = true;
        
        for(int index=1; index<n; index++) {
            for(int target=1; target<=totalSum; target++) {
                boolean notTake = dp[index-1][target];
                boolean take = false;
                if(arr[index] <= target) take = dp[index-1][target-arr[index]];
                dp[index][target] = (take || notTake);
            }
        }
        
        int minDiff = Integer.MAX_VALUE;
        for(int target=0; target<=totalSum/2; target++) {
            if(dp[n-1][target] == false) continue;
            int firstSetSum = target;
            int secondSetSum = totalSum - target;
            int diff = Math.abs(firstSetSum - secondSetSum);
            minDiff = Math.min(minDiff,diff);
        }
        return minDiff;
    }
}

```
> `Time Complexity` : **O(N\*K)**          
> `Space Complexity` : **O(N\*K)**
---
### Tabulation with Space Optimization
```java
public class Solution {
    public static int minSubsetSumDifference(int[] arr, int n) {
        int totalSum = 0;
        for(int num : arr) totalSum += num;
        boolean[] prev = new boolean[totalSum+1];
        prev[0] = true;
        prev[arr[0]] = true;
        
        for(int index=1; index<n; index++) {
            boolean[] curr = new boolean[totalSum+1];
            curr[0] = true;
            for(int target=1; target<=totalSum; target++) {
                boolean notTake = prev[target];
                boolean take = false;
                if(arr[index] <= target) take = prev[target-arr[index]];
                curr[target] = (take || notTake);
            }
            prev = curr;
        }
        
        int minDiff = Integer.MAX_VALUE;
        for(int target=0; target<=totalSum/2; target++) {
            if(prev[target] == false) continue;
            int firstSetSum = target;
            int secondSetSum = totalSum - target;
            int diff = Math.abs(firstSetSum - secondSetSum);
            minDiff = Math.min(minDiff,diff);
        }
        return minDiff;
    }
}

```
> `Time Complexity` : **O(N\*K)**          
> `Space Complexity` : **O(K)+O(K)**, for prev and curr arrays.
---
Video Explanations -> [Partition a set into two subsets such that the difference of subset sums is minimum](https://youtu.be/GS_OqZb2CWc?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
