# Linear Search   
### Algorithm
> * Step 1: Traverse the array
> * Step 2: Match the key element with array element
> * Step 3: If key element is found, return the index position of the array element
> * Step 4: If key element is not found, return -1

### Implementation
```java
public class Solution{
    public int linearSearch(int[] arr, int key){    
        for(int i=0; i<arr.length; i++){    
            if(arr[i] == key){    
                return i;    
            }    
        }    
        return -1;    
    }
}
```
> `Time Complexity` : **O(n)**       
> `Space Complexity` : **O(1)**
---
