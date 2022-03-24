# Subset Sum Equal To K
Question -> [Subset Sum Equal To K](https://www.codingninjas.com/codestudio/problems/subset-sum-equal-to-k_1550954)    

### Recursion
```java
public class Solution {
    public static boolean subsetSumToK(int n, int k, int[] arr){
	return subsetSum(n-1, k, arr);
    }
    public static boolean subsetSum(int index, int target, int[] arr) {
        if(target < 0) return false;
        if(target == 0) return true;
        if(index == 0) return (arr[index] == target);
        
        boolean take = subsetSum(index-1, target-arr[index], arr);
        boolean notTake = subsetSum(index-1, target, arr);
        return (take || notTake);
    }
}
```         
> `Recurrence Realtion` : **T(N) = 2(T(N-1))+C**     
> `Time Complexity` : **O(2<sup>(N)</sup>)**          
> `Space Complexity` : **O(N)**    
---
### Memorization
```java
public class Solution {
    public static boolean subsetSumToK(int n, int k, int[] arr) {
        int[][] dp = new int[n][k+1];
        return subsetSum(n-1, k, arr, dp);
    }
    public static boolean subsetSum(int index, int target, int[] arr, int[][] dp) {
        if(target < 0) return false;
        if(target == 0) return true;
        if(index == 0) return (arr[index] == target);
        
        if(dp[index][target] != 0) return (dp[index][target] == 1);
        boolean take = subsetSum(index-1, target-arr[index], arr, dp);
        boolean notTake = subsetSum(index-1, target, arr, dp);
        
        boolean ans = (take || notTake);
        dp[index][target] = (ans==true) ? 1 : 2;
        return ans;
    }
}
```
> `Time Complexity` : **O(N\*K)**, K = target          
> `Space Complexity` : **O(N)+O(N\*K)**, for Recursion Stack and dp array
---
### Tabulation
```java
public class Solution {
    public static boolean subsetSumToK(int n, int k, int[] arr) {
        boolean[][] dp = new boolean[n][k+1];
        // base case
        // for target = 0 at any index
        for(int index=0; index<n; index++) {
            dp[index][0] = true;
        }
        // when at index=0, target is equal to arr[0]
        if(arr[0] <= k) dp[0][arr[0]] = true;
        
        for(int index=1; index<n; index++) {
            for(int target=1; target<=k; target++) {
                boolean taken = false;
                if(target >= arr[index]) {
                    taken = dp[index-1][target-arr[index]];
                }
                boolean notTaken = dp[index-1][target];
                dp[index][target] = (taken || notTaken);
            }
        }
        return dp[n-1][k];
    }
}
```
> `Time Complexity` : **O(N\*K)**          
> `Space Complexity` : **O(N\*K)**
---
### Tabulation with Space Optimization
```java
public class Solution {
    public static boolean subsetSumToK(int n, int k, int[] arr) {
        boolean[] prev = new boolean[k+1];
        // for target = 0 at any index
        prev[0] = true;
        // when at index=0, target is equal to arr[0]
        if(arr[0] <= k) prev[arr[0]] = true;
        
        for(int index=1; index<n; index++) {
            boolean[] curr = new boolean[k+1];
            curr[0] = true;
            for(int target=1; target<=k; target++) {
                boolean taken = false;
                if(target >= arr[index]) {
                    taken = prev[target-arr[index]];
                }
                boolean notTaken = prev[target];
                curr[target] = (taken || notTaken);
            }
            prev = curr;
        }
        return prev[k];
    }
}
```
> `Time Complexity` : **O(N\*K)**          
> `Space Complexity` : **O(K)+O(K)**, for prev and curr arrays.
---
Video Explanations -> [Subset Sum Equal To K](https://youtu.be/fWX9xDmIzRI?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
