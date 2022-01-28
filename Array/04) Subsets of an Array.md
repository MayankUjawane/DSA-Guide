# Subsets of an Array
> A subsequence is a sequence that can be derived from another sequence by removing zero or more elements, without changing the order of the remaining elements.     
>  For example, consider the array [1, 2, 3, 4], there are 15 non-empty sub-sequences. They are (1), (2), (3), (4), (1,2), (1,3),(1,4), (2,3), (2,4), (3,4), (1,2,3), (1,2,4), 
>  (1,3,4), (2,3,4), (1,2,3,4).      
>  More generally, we can say that for a **sequence of size n, we have (2^n) sub-sequences in total** in which **(2^n-1) are non-empty sub-sequences**.       
>  
> Question -> [Subsets of an Array](https://www.pepcoding.com/resources/online-java-foundation/function-and-arrays/subsets-of-array-official/ojquestion)    

### Iterative
```java
public class Solution{
    public void printSubsequence(int[] arr, int n) {
        int limit = (int) Math.pow(2, n);
        // Outer loop will run for 2^n times
        for(int i=0; i<limit; i++) {
            StringBuilder sb = new StringBuilder();
            int temp = i;
            // Inner loop will run n times to print subsequences
            for(int j=n-1; j>=0; j--) {
                // converting i to its equivalent binary
                int remainder = temp % 2;
                temp = temp/2;
                // leaving the arr[j] element
                if(remainder == 0) {
                    sb.insert(0,"-\t");
                } // including the arr[j] element
                else {
                    sb.insert(0, arr[j]+"\t");
                }
            }
            System.out.println(sb);
        }
    }
}
```
> `Time Complexity` : **O(k\*(2^n))**, where k is the time required to print all the subsequences       
> `Space Complexity` : **O(n)**
---
Video Explanations -> [Subsets of an Array](https://youtu.be/iKSI_9NHR1M?list=PL-Jc9J83PIiHOV7lm2uSw4ZiVsIRsGS6r)   
<hr>

### Recursive
```java
public class Solution{
    public void printSubsequences(int[] arr, int index, ArrayList<Integer> path) {
        // Print the subsequence
        if (index == arr.length) {
            // Condition to avoid printing empty subsequence
            if (path.size() > 0) System.out.println(path);
            
            return;
        }
        
        // Subsequence without including the element at current index
        printSubsequences(arr, index + 1, path);
         
        path.add(arr[index]);
         
        // Subsequence including the element at current index
        printSubsequences(arr, index + 1, path);
         
        // Remove the recently inserted element at the time of Backtrack
        path.remove(path.size() - 1);
    }
}
```
> `Time Complexity` : **O(k\*(2^n))**, where k is the time required to print all the subsequences       
> `Space Complexity` : **O(n)+O(n)**, for recursion stack and arraylist
---
Video Explanations -> [SubSequences of an array Recursive Solution](https://youtu.be/HEzpaUOAcds)   
<hr>
