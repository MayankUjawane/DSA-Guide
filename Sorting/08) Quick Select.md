# Quick Select
### Algorithm
> **Quickselect is a selection algorithm** to find the **k-th smallest element** in an unordered list.         
> The algorithm is similar to QuickSort. The difference is, instead of recurring for both sides (after finding pivot), **it recurs only for the part that contains the 
> k-th smallest element**. The logic is simple, if index of partitioned element is more than k, then we recur for left part. If index is same as k, we have found the 
> k-th smallest element and we return. If index is less than k, then we recur for right part. This reduces the expected complexity from O(n log n) to **O(n)**, with a 
> **worst case of O(n^2)**.
```java
class QuickSelect {
    // finds the kth position (of the sorted array) in a given unsorted array i.e this function
    // can be used to find both kth largest and kth smallest element in the array.
    // ASSUMPTION: all elements in arr[] are distinct
    public static int quickSelect(int[] arr, int start, int end, int kPosition) {
        int pivotIndex = partition(arr, start, end);
        // checking for k-1 index because kth position element will be present at k-1 index in array.
        if(pivotIndex < kPosition-1) {
            return quickSelect(arr, pivotIndex+1, end, kPosition);
        } else if(pivotIndex > kPosition-1) {
            return quickSelect(arr, start, pivotIndex-1, kPosition);
        } else {
            return arr[pivotIndex];
        }
    }
    
    public static int partition(int[] arr, int start, int end){
        int pivot = arr[end];
        int i = start, j=start;
        
        while(i<=end) {
            if(arr[i] > pivot) {
                i++;
            } else {
                int temp = arr[j];
                arr[j] = arr[i];
                arr[i] = temp;
                i++;
                j++;
            }
        }
        return j-1;
    }
}
```
> `Average Case` : **O(n)**   
> `Worst Case` : **θ(n2)**    
> `Best Case` : **θ(n)**   
> `Auxiliary Space` : **O(n)**            
---  
Video Explanations -> [Quick Select](https://youtu.be/fnbImb8lo88?list=PL-Jc9J83PIiFc7hJ5eeCb579PS8p-en4f) 
<hr>
