# Partitions With Given Difference
Question -> [Partitions With Given Difference](https://www.codingninjas.com/codestudio/problems/partitions-with-given-difference_3751628)    

### Recursion
```java
public class Solution {
    public static int countPartitions(int n, int d, int[] arr) {
        int totalSum = 0;
        for(int num : arr) totalSum += num;
        // (s1-s2 = D) and s1 = totalSum - s2, so (T.S. - 2s2 = D)
        // s2 = (TotalSum-D)/2;
        // so we can solve this question by using number of subsets with sum s2
        // TotalSum-D should be even and must greater than zero
        if(totalSum-d < 0 || (totalSum-d)%2 != 0) return 0;
        int target = (totalSum-d)/2;
        int modulo = (int)Math.pow(10,9)+7;
        return findSubsets(n-1, arr, target, modulo);
    }
    public static int findSubsets(int index, int[] arr, int target, int modulo) {
        if(index == 0) {
            if(arr[0] == 0 && target == 0) return 2;
            if(arr[0] == target || target == 0) return 1;
            return 0;
        }
        int take = 0;
        if(target >= arr[index]) take = findSubsets(index-1, arr, target-arr[index], modulo);
        int notTake = findSubsets(index-1, arr, target, modulo);
        return (take+notTake) % modulo;
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
    public static int countPartitions(int n, int d, int[] arr) {
        int totalSum = 0;
        for(int num : arr) totalSum += num;
        // (s1-s2 = D) and s1 = totalSum - s2, so (T.S. - 2s2 = D)
        // s2 = (TotalSum-D)/2;
        // so we can solve this question by using number of subsets with sum s2
        // TotalSum-D should be even and must greater than zero
        if(totalSum-d < 0 || (totalSum-d)%2 != 0) return 0;
        int target = (totalSum-d)/2;
        int modulo = (int)Math.pow(10,9)+7;
        int[][] dp = new int[n][target+1];
        for(int[] row : dp) Arrays.fill(row,-1);
        return findSubsets(n-1, arr, target, modulo, dp);
    }
    public static int findSubsets(int index, int[] arr, int target, int modulo, int[][] dp) {
        if(index == 0) {
            if(arr[0] == 0 && target == 0) return 2;
            if(arr[0] == target || target == 0) return 1;
            return 0;
        }
        if(dp[index][target] != -1) return dp[index][target];
        int take = 0;
        if(target >= arr[index]) take = findSubsets(index-1, arr, target-arr[index], modulo, dp);
        int notTake = findSubsets(index-1, arr, target, modulo, dp);
        return dp[index][target] = (take+notTake) % modulo;
    }
}
```
> `Time Complexity` : **O(N\*T)**, T = target          
> `Space Complexity` : **O(N)+O(N\*T)**, for Recursion Stack and dp array
---
### Tabulation
```java
import java.util.*;
public class Solution {
    public static int countPartitions(int n, int d, int[] arr) {
        int totalSum = 0;
        for(int num : arr) totalSum += num;
        // (s1-s2 = D) and s1 = totalSum - s2, so (T.S. - 2s2 = D)
        // s2 = (TotalSum-D)/2;
        // so we can solve this question by using number of subsets with sum s2
        // TotalSum-D should be even and must greater than zero
        if(totalSum-d < 0 || (totalSum-d)%2 != 0) return 0;
        int target = (totalSum-d)/2;
        int modulo = (int)Math.pow(10,9)+7;
        return findSubsets(n, arr, target, modulo);
    }
    public static int findSubsets(int n, int[] arr, int tar, int modulo) {
        int[][] dp = new int[n][tar+1];
        // base case
        if(arr[0] == 0) dp[0][0] = 2; // when arr[0]=0 and target=0 then we have two option of take and not take
        else dp[0][0] = 1; // when arr[0] != 0 but target=0 then we have one option of not take
        
        if(arr[0] != 0 && arr[0] <= tar) dp[0][arr[0]] = 1;
        
        for(int index=1; index<n; index++) {
            for(int target=0; target<=tar; target++) {
                int take = 0;
                if(arr[index] <= target) take = dp[index-1][target-arr[index]];
                int notTake = dp[index-1][target];
                dp[index][target] = (take+notTake) % modulo;
            }
        }
        return dp[n-1][tar];
    }
}
```
> `Time Complexity` : **O(N\*T)**, T = target           
> `Space Complexity` : **O(N\*T)**
---
### Tabulation with Space Optimization
```java
import java.util.*;
public class Solution {
    public static int countPartitions(int n, int d, int[] arr) {
        int totalSum = 0;
        for(int num : arr) totalSum += num;
        // (s1-s2 = D) and s1 = totalSum - s2, so (T.S. - 2s2 = D)
        // s2 = (TotalSum-D)/2;
        // so we can solve this question by using number of subsets with sum s2
        // TotalSum-D should be even and must greater than zero
        if(totalSum-d < 0 || (totalSum-d)%2 != 0) return 0;
        int target = (totalSum-d)/2;
        int modulo = (int)Math.pow(10,9)+7;
        return findSubsets(n, arr, target, modulo);
    }
    public static int findSubsets(int n, int[] arr, int tar, int modulo) {
        int[] prev = new int[tar+1];
        // base case
        if(arr[0] == 0) prev[0] = 2; // when arr[0]=0 and target=0 then we have two option of take and not take
        else prev[0] = 1; // when arr[0] != 0 but target=0 then we have one option of not take
        if(arr[0] != 0 && arr[0] <= tar) prev[arr[0]] = 1;
        
        for(int index=1; index<n; index++) {
            int[] curr = new int[tar+1];
            for(int target=0; target<=tar; target++) {
                int take = 0;
                if(arr[index] <= target) take = prev[target-arr[index]];
                int notTake = prev[target];
                curr[target] = (take+notTake) % modulo;
            }
            prev = curr;
        }
        return prev[tar];
    }
}
```
> `Time Complexity` : **O(N\*T)**, T = target           
> `Space Complexity` : **O(T)+O(T)**, for prev and curr arrays.
---
Video Explanations -> [Partitions With Given Difference](https://youtu.be/zoilQD1kYSg?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
