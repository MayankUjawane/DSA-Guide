# Ninja’s Training
Question -> [Ninja’s Training](https://www.codingninjas.com/codestudio/problems/ninja-s-training_3621003)    

### Recursion
```java
import java.util.*;
public class Solution {
    public static int ninjaTraining(int n, int points[][]) {
        return ninjaTraining(n-1, points, 3);
    }
    public static int ninjaTraining(int day, int points[][], int lastTask) {
        if(day == 0) {
            int max = Integer.MIN_VALUE;
            for(int currTask=0; currTask<3; currTask++) {
                if(currTask != lastTask) {
                    int point = points[0][currTask];
                    max = Math.max(max, point);
                }
            }
            return max;
        }
        
        int max = Integer.MIN_VALUE;
        for(int currTask=0; currTask<3; currTask++) {
            if(currTask != lastTask) {
                int point = points[day][currTask]+ninjaTraining(day-1, points, currTask);
                max = Math.max(max, point);
            }
        }
        return max;
    }
}
```
> `Recurrence Relation` : **T(n) = 2(T(n-1))+3C**           
> `Time Complexity` : **O(2<sup>N</sup>)**          
> `Space Complexity` : **O(N)**
---
### Memorization
```java
import java.util.*;
public class Solution {
    public static int ninjaTraining(int n, int points[][]) {
        int[][] dp = new int[n][4];
        for (int[] row : dp) {
            Arrays.fill(row, -1);
        } 
        return ninjaTraining(n-1, points, 3, dp);
    }
    public static int ninjaTraining(int day, int points[][], int lastTask, int[][] dp) {
        if(dp[day][lastTask] != -1) return dp[day][lastTask];

        if(day == 0) {
            int max = Integer.MIN_VALUE;
            for(int currTask=0; currTask<3; currTask++) {
                if(currTask != lastTask) {
                    int point = points[0][currTask];
                    max = Math.max(max, point);
                }
            }
            return dp[day][lastTask] = max;
        }
        
        int max = Integer.MIN_VALUE;
        for(int currTask=0; currTask<3; currTask++) {
            if(currTask != lastTask) {
                int point = points[day][currTask]+ninjaTraining(day-1, points, currTask, dp);
                max = Math.max(max, point);
            }
        }
        return dp[day][lastTask] = max;
    }
}
```
> `Time Complexity` : **O(3(N\*3))**    
>  There are N\*3 states and for every state, we are running a for loop iterating three times.       
> `Space Complexity` : **O(N)+O(N\*4)**, for Recursion Stack and dp array
---
### Tabulation
```java
import java.util.*;
class Solution {
    public static int ninjaTraining(int n, int points[][]) {
        int[][] dp = new int[n][3];
        // base case
        dp[0][0] = Math.max(points[0][1],points[0][2]);
        dp[0][1] = Math.max(points[0][0],points[0][2]);
        dp[0][2] = Math.max(points[0][0],points[0][1]);
        
        for(int day=1; day<n; day++) {
            for(int lastTask=0; lastTask<3; lastTask++) {
                dp[day][lastTask] = 0;
                for(int currTask=0; currTask<3; currTask++) {
                    if(currTask == lastTask) continue;
                    int point = points[day][currTask]+dp[day-1][currTask];
                    dp[day][lastTask] = Math.max(dp[day][lastTask],point);
                }
            }
        }
        // maximum of all ways is the answer
        int ans = 0;
        for(int task=0; task<3; task++) {
            ans = Math.max(ans,dp[n-1][task]);
        }
        return ans;
    }
}
```
> `Time Complexity` : **O(3(N\*3))**          
> `Space Complexity` : **O(N\*3)**
---
### Tabulation with Space Optimization
```java
import java.util.*;
public class Solution {
    public static int ninjaTraining(int n, int points[][]) {
        int[] prev = new int[3];
        // base case
        prev[0] = Math.max(points[0][1],points[0][2]);
        prev[1] = Math.max(points[0][0],points[0][2]);
        prev[2] = Math.max(points[0][0],points[0][1]);
        
        for(int day=1; day<n; day++) {
            int[] curr = new int[3];
            for(int lastTask=0; lastTask<3; lastTask++) {
                curr[lastTask] = 0;
                for(int currTask=0; currTask<3; currTask++) {
                    if(currTask == lastTask) continue;
                    int point = points[day][currTask] + prev[currTask];
                    curr[lastTask] = Math.max(curr[lastTask],point);
                }
            }
            prev = curr;
        }
        // maximum of all ways is the answer
        int ans = 0;
        for(int task=0; task<3; task++) {
            ans = Math.max(ans,prev[task]);
        }
        return ans;
    }
}
```
> `Time Complexity` : **O(3(N\*3))**          
> `Space Complexity` : **O(1)**
---
Video Explanations -> [Ninja’s Training](https://youtu.be/AE39gJYuRog?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
