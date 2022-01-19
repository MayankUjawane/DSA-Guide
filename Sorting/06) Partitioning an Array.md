# Partitioning an Array
> **Algorithm**      
> 1. We will use two pointers i and j.         
> 2. Will check if number is greater than pivot than we will just increment i pointer.       
> 3. If number is less or equal to the pivot than we will swap the array value of i and j index.         
> 4. In the end, numbers less or equal to pivot will lie between 0 to j-1 index.       
> 5. And the numbers greater than pivot will lie between j to i-1 index.          
```java
public static void arrayPartition(int[] arr, int pivot) {
    // numbers > pivot will lie between j to i-1 index
    // numbers <= pivot will liew between 0 to j-1 index
    int i=0;
    int j=0;
    while(i < arr.length) {
        if(arr[i] > pivot) {
            i++;
        } else {
            //swap arr[i] to arr[j]
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;
            j++;
        }
    }
}
```
> `Time Complexity` : **O(n)**   
> `Auxiliary Space` : **O(1)**         
---
### Applications      
1. Sort 0's and 1's in array.     
2. Sort odd and even in array.        
3. Separate 0 and non-zero in array.      
----
Video Explanations -> [Partitioning an Array](https://youtu.be/if40LxQ8_Xo?list=PL-Jc9J83PIiFc7hJ5eeCb579PS8p-en4f) 
<hr>
