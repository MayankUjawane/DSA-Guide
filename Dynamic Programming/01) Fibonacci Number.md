# Fibonacci Number
Question -> [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)    

### Recursion
```java
class Main {
    public int fib(int n) {
        return fibonacci(n);
    }
    
    public int fibonacci(int n) {
        if(n <= 1) return n;
        return fibonacci(n-1)+fibonacci(n-2);
    }
}
```
> `Time Complexity` : **O(2<sup>N</sup>)**          
> `Space Complexity` : **O(N)**
---
### Memoization
```java
class Main {
    public int fib(int n) {
        int[] dp = new int[n+1];
        return fibonacci(n, dp);
    }
    public int fibonacci(int n, int[] dp) {
        if(n <= 1) return n;
        if(dp[n] != 0) return dp[n];
        return dp[n] = fibonacci(n-1, dp)+fibonacci(n-2, dp);
    }
}
```
> `Time Complexity` : **O(N)**          
> `Space Complexity` : **O(N)+O(N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Main {
    public int fib(int n) {
        if(n <= 1) return n;
        int[] dp = new int[n+1];
        dp[0] = 0;
        dp[1] = 1;
        for(int i=2; i<=n; i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
}
```
> `Time Complexity` : **O(N)**          
> `Space Complexity` : **O(N)**
---
### Tabulation with Space Optimization
```java
class Main {
    public int fib(int n) {
        if(n <= 1) return n;
        int prev2 = 0, prev1 = 1;
        for(int i=2; i<=n; i++) {
            int curr = prev1 + prev2;
            prev2 = prev1;
            prev1 = curr;
        }
        return prev1;
    }
}
```
> `Time Complexity` : **O(N)**          
> `Space Complexity` : **O(1)**
---
Video Explanations -> [Fibonacci Number](https://youtu.be/tyB0ztf0DNY?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
