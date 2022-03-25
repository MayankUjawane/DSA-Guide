# Number Of Subsets
Question -> [Number Of Subsets](https://www.codingninjas.com/codestudio/problems/number-of-subsets_3952532)    

### Recursion
```java
public class Solution {
    public static int findWays(int num[], int tar) {
        int n = num.length;
        return findWays(n-1, num, tar);
    }
    public static int findWays(int index, int[] num, int target) {
        if(target < 0) return 0;
        if(target == 0) return 1;
        if(index == 0) return (target==num[0]) ? 1 : 0;
        
        int take = findWays(index-1, num, target-num[index]);
        int notTake = findWays(index-1, num, target);
        return take+notTake;
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
    public static int findWays(int num[], int tar) {
        int n = num.length;
        int[][] dp = new int[n][tar+1];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return findWays(n-1, num, tar, dp);
    }
    public static int findWays(int index, int[] num, int target, int[][] dp) {
        if(target < 0) return 0;
        if(target == 0) return 1;
        if(index == 0) return (target==num[0]) ? 1 : 0;
        
        if(dp[index][target] != -1) return dp[index][target];
        int take = findWays(index-1, num, target-num[index], dp);
        int notTake = findWays(index-1, num, target, dp);
        return dp[index][target] = (take+notTake);
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
    public static int findWays(int num[], int tar) {
        int n = num.length;
        int[][] dp = new int[n][tar+1];
        // base case
        for(int i=0; i<n; i++) dp[i][0] = 1;
        if(num[0] <= tar) dp[0][num[0]] = 1;
        
        for(int index=1; index<n; index++) {
            for(int target=1; target<=tar; target++) {
                int notTake = dp[index-1][target];
                int take = 0;
                if(target >= num[index]) take = dp[index-1][target-num[index]];
                dp[index][target] = take + notTake;
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
    public static int findWays(int num[], int tar) {
        int n = num.length;
        int[] prev = new int[tar+1];
        // base case
        prev[0] = 1;
        if(num[0] <= tar) prev[num[0]] = 1;
        
        for(int index=1; index<n; index++) {
            int[] curr = new int[tar+1];
            curr[0] = 1;
            for(int target=1; target<=tar; target++) {
                int notTake = prev[target];
                int take = 0;
                if(target >= num[index]) take = prev[target-num[index]];
                curr[target] = take + notTake;
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
Video Explanations -> [Number Of Subsets](https://youtu.be/ZHyb-A2Mte4?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
