# Subarrays of an Array
> Subarray -> A subarray is a **contiguous part of array**. An array that is inside another array. 
> For example, consider the array [1, 2, 3, 4], There are 10 non-empty sub-arrays. The subarrays are (1), (2), (3), (4), (1,2), (2,3), (3,4), (1,2,3), (2,3,4) and (1,2,3,4).      
> In general, for an array/string of size n, there are **n(n+1)/2** non-empty subarrays/substrings.  
>   
> Question -> [Subarrays of an Array](https://www.pepcoding.com/resources/online-java-foundation/function-and-arrays/subarray-problem-official/ojquestion)

### Iterative (Print length wise subarray)
```java
public class Solution{
    public void printSubArrays(int[] arr, int n) {
        // Length of sub-array
        for (int length=1; length<=n; length++) {
            // Starting Index
            for (int start=0; start<=n-length; start++)  {
                // Ending Index
                int end = start + length - 1;
                // Print subarray between current starting and ending index
                for (int k=start; k<=end; k++) {
                    System.out.print(arr[k]+" ");
                }
                System.out.println();
            }
        }
    }
}
```
> `Time Complexity` : **O(n^3)**       
> `Space Complexity` : **O(1)**
---
### Iterative
```java
public class Solution{
    public void printSubArrays(int[] arr, int n) {
        // Pick starting point
        for (int i=0; i<n; i++) {
            // Pick ending point
            for (int j=i; j<n; j++)  {
                // Print subarray between current starting and ending points
                for (int k=i; k<=j; k++) {
                    System.out.print(arr[k]+" ");
                }
                System.out.println();
            }
        }
    }
}
```
> `Time Complexity` : **O(n^3)**       
> `Space Complexity` : **O(1)**
---
### Recursion
```java
public class Solution{
    // Recursive function to print all possible subarrays for given array
    public void printSubArrays(int[] arr, int start, int end) {    
        // Stop if we have reached the end of the array    
        if (end == arr.length) {
            return;
        } 
        // Increment the end point and start from 0
        else if (start > end) {
            printSubArrays(arr, 0, end + 1);
        }
        // Print the subarray and increment the starting point
        else {
            System.out.print("[");
            for (int i = start; i < end; i++){
                System.out.print(arr[i]+", ");
            }

            System.out.println(arr[end]+"]");
            printSubArrays(arr, start + 1, end);
        }
        return;
    }
}
```
> `Time Complexity` : **O(n^3)**       
> `Space Complexity` : **O(n^2)**
---
Video Explanations -> [Subarrays of an Array](https://youtu.be/lUdWGkCUD54?list=PL-Jc9J83PIiHOV7lm2uSw4ZiVsIRsGS6r), [Time Complexity Explanation](https://youtu.be/T6lOtastw6A)
<hr>
