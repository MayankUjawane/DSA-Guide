# Parallel Courses
Question -> [Parallel Courses](https://www.codingninjas.com/codestudio/problems/parallel-courses_1376444)    

### Implementation
```java
import java.util.*;
public class Solution {
    public static int parallelCourses(int n, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList();
        for(int i=0; i<=n; i++) {
            graph.add(new ArrayList());
        }
        int[] inDegree = new int[n+1];
        for(int[] arr: prerequisites) {
            int independent = arr[0];
            int dependent = arr[1];
            graph.get(independent).add(dependent);
            inDegree[dependent]++;
        }
        
        Queue<Integer> q = new LinkedList();
        for(int i=1; i<=n; i++) {
            if(inDegree[i] == 0) q.offer(i);
        }
        
        int numberOfSemester = 0, count = 0;
        while(!q.isEmpty()) {
            int size = q.size();
            count += size;
            for(int i=0; i<size; i++) {
               	int top = q.poll();
                for(int ngb: graph.get(top)) {
                    inDegree[ngb]--;
                    if(inDegree[ngb] == 0) q.offer(ngb);
                } 
            }
            numberOfSemester++;
        }
        
        return (count == n) ? numberOfSemester : -1;
    }
}
``` 
> `Time Complexity` : **O(V+E)**, here V=number of courses and E=prerequisites.length     
> `Space Complexity` : **O(V+E)**   
---
