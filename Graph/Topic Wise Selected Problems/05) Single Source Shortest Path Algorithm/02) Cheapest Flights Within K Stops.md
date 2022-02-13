# Cheapest Flights Within K Stops
Question -> [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)    

### Implementation Using Bellman Ford
```java
class Solution {
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
        int[] previous = new int[n];
        int[] current = new int[n];
        for(int i=0; i<n; i++) {
            previous[i] = Integer.MAX_VALUE;
            current[i] = Integer.MAX_VALUE;
        }
        
        // since k stops are allowed so dest will be at k+1 level from src
        previous[src] = 0;
        for(int i=0; i<k+1; i++) {
            for(int[] flight: flights) {
                int from = flight[0];
                int to = flight[1];
                int price = flight[2];
                if(previous[from] == Integer.MAX_VALUE) continue;
                if(previous[from] + price < current[to]) {
                    current[to] = previous[from] + price;
                }
            }
            previous = current.clone();
        }
        
        if(previous[dst] == Integer.MAX_VALUE) {
            return -1;
        }
        return previous[dst];
    }
}
``` 
> `Time Complexity` : **O(E\*k)**     
> `Space Complexity` : **O(N)+O(N)**, where N = Number of Vertices.   
---
Video Explanations -> [Cheapest Flights Within K Stops](https://www.youtube.com/watch?v=5eIK3zUdYmE)  
<hr>
