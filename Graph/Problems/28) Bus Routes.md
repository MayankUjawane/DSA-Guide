# Bus Routes
Question -> [Bus Routes](https://leetcode.com/problems/bus-routes/)    

### Implementation
```java
class Solution {
    public int numBusesToDestination(int[][] routes, int source, int target) {
        if(source == target) return 0;
        
        HashMap<Integer, ArrayList<Integer>> map = new HashMap<>();
        int numberOfBuses = routes.length;
        for(int i=0; i<numberOfBuses; i++) {
            for(int j=0; j<routes[i].length; j++) {
                int busStop = routes[i][j];
                ArrayList<Integer> buses = map.getOrDefault(busStop, new ArrayList<Integer>());
                buses.add(i);
                map.put(busStop, buses);
            }
        }
        
        HashSet<Integer> visitedBusStop = new HashSet<>();
        boolean[] visitedBus = new boolean[numberOfBuses];
        Queue<Integer> q = new LinkedList<>();
        q.offer(source);
        visitedBusStop.add(source);
        
        int level = 1;
        while(!q.isEmpty()) {
            int size = q.size();
            for(int i=0; i<size; i++) {
                int s = q.poll();
                ArrayList<Integer> buses = map.get(s);
                for(int bus: buses) {
                    if(visitedBus[bus] == false) {
                        visitedBus[bus] = true;
                        for(int stop: routes[bus]) {
                            if(!visitedBusStop.contains(stop)) {
                                if(stop == target) return level;
                                q.offer(stop);
                                visitedBusStop.add(stop);
                            }
                        }
                    }
                }
            }
            level++;
        }
        return -1;
    }
}
```
> `Time Complexity` : **O(N)**, where N = row * column      
> `Space Complexity` : **O(N)**              
Video Explanations -> [Bus Routes](https://youtu.be/WhuiqhMXhxM)  
<hr>
