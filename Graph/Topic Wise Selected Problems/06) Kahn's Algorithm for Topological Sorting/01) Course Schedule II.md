# Course Schedule II
Question -> [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)    

### Implementation
```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        int[] ans = new int[numCourses];
        if(prerequisites.length == 0) {
            for(int i=0; i<numCourses; i++) {
                ans[i] = i;
            }
            return ans;
        }
        
        List<List<Integer>> graph = new ArrayList();
        for(int i=0; i<numCourses; i++) {
            graph.add(new ArrayList());
        }
        int[] inDegree = new int[numCourses];
        for(int[] arr: prerequisites) {
            int dependent = arr[0];
            int independent = arr[1];
            graph.get(independent).add(dependent);
            inDegree[dependent]++;
        }
        
        Queue<Integer> q = new LinkedList();
        for(int i=0; i<numCourses; i++) {
            if(inDegree[i] == 0) q.offer(i);
        }
        
        int index=0;
        while(!q.isEmpty()) {
            int top = q.poll();
            ans[index++] = top;
            
            for(int ngb: graph.get(top)) {
                inDegree[ngb]--;
                if(inDegree[ngb] == 0) q.offer(ngb);
            }
        }
        
        // Check to see if topological sort is possible or not
        if(index == numCourses) return ans;
        
        return new int[0];
    }
}
``` 
> `Time Complexity` : **O(V+E)**     
> `Space Complexity` : **O(V+E)**   
---
