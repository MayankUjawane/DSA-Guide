# Alien Dictionary
Question -> [Alien Dictionary](https://nados.io/question/alien-dictionary?zen=true)    

### Implementation
```java
class Solution {
    public static String alienOrder(String[] words) {
        int n = words.length;
        // S.C.-> O(26)
        Map<Character,Integer> indegree = new HashMap();
        // S.C.-> O(V+E), V can be upto 26 only and E=N-1 since every alternate words can make 1 edge
        // S.C.-> O(N)
        Map<Character, Set<Character>> map = new HashMap();
        
        // O(N*M) N=Total Words, M=Maximum length of all words
        for(String word: words) {
            for(char c: word.toCharArray()) {
                if(map.containsKey(c)) continue;
                indegree.put(c, 0);
            }
        }
        // O(N*M)
        for(int i=0; i<n-1; i++) {
            String w1 = words[i];
            String w2 = words[i+1];
            int length = Math.min(w1.length(), w2.length());
            boolean flag = false;

            for(int j=0; j<length; j++) {
                char c1 = w1.charAt(j);
                char c2 = w2.charAt(j);
                if(c1 != c2) {
                    map.putIfAbsent(c1, new HashSet());
                    Set<Character> set = map.get(c1);
                    set.add(c2);
                    map.put(c1, set);
                    indegree.put(c2, indegree.get(c2)+1);
                    flag = true;
                    break;
                }
            }
            // for the test cases like "abc" "ab"
            if(flag == false && w1.length() > w2.length()) {
                return "";
            }
        }
        
        return topologicalSort(map, indegree);
    }
    
    // O(V+E) here V=total unique characters=26 and E=N-1 since alternate words can make one edge
    // O(N-1)
    public static String topologicalSort(Map<Character,Set<Character>> map, Map<Character,Integer> indegree) {
        StringBuilder sb = new StringBuilder();
        Queue<Character> q = new LinkedList();
        for(Character c: indegree.keySet()) {
            if(indegree.get(c) == 0) {
                q.add(c);
            }
        }

        while(!q.isEmpty()) {
            Character top = q.poll();
            sb.append(top);
            
            // if node does note have any neighbors
            if(!map.containsKey(top)) continue;

            Iterator<Character> it = map.get(top).iterator();
            while(it.hasNext()) {
                char c = it.next();
                indegree.put(c, indegree.get(c)-1);
                if(indegree.get(c) == 0) q.add(c);
            }
        }
        // if graph has cycle then sb will not contain all the characters
        return (sb.length() == indegree.size()) ? sb.toString() : "";
    }
}
``` 
> `Time Complexity` : **O(N\*M)**, where N=Total Words, M=Maximum length of all words               
> `Space Complexity` : **O(N)**   
---
Video Explanations -> [Alien Dictionary](https://youtu.be/_u1Mn4_2hIo)  
<hr>
