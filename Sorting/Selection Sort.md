# Selection Sort
> The selection sort algorithm sorts an array by repeatedly finding the minimum element (considering ascending order) from unsorted part and putting it 
> at the beginning of the unsorted part. 
> The algorithm maintains two subarrays in a given array.
> 1) The subarray which is already sorted. 
> 2) Remaining subarray which is unsorted.

```java
void sort(int arr[]) {
    int n = arr.length;
    // One by one move boundary of unsorted subarray
    for(int i = 0; i < n-1; i++) {
        // Find the minimum element in unsorted array
        int min_idx = i;
        for(int j=i+1; j < n; j++)
            if (arr[j] < arr[min_idx])
                min_idx = j;

        // Swap the found minimum element with the first element of unsorted subarray
        int temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}
```
> `Time Complexity` : **O(n^2)**                         
> `Auxiliary Space` : **O(1)**    
> `In Place` : **Yes**, it does not require extra space.        
> `Sorting In Place` : **Yes**           
> `Stable` : **No**, The default implementation is not stable. However it can be made stable.    
---
Video Explanations -> [Selection Sort](https://www.youtube.com/watch?v=xWBP4lzkoyM) 
<hr>
