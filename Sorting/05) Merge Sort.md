# Merge Sort
> **Algorithm**      
> 1. Find the middle point to divide the array into two halves:            
>         middle m = (l+r)/2
> 2. Call mergeSort for first half:          
>         Call mergeSort(arr, l, m)
> 3. Call mergeSort for second half:        
>         Call mergeSort(arr, m+1, r)
> 4. Merge the two halves sorted in step 2 and 3:         
>         Call merge(arr, l, m, r)
>            
```java
class MergeSort {
    public void mergeSort(int arr[], int beg, int end) {  
        if (beg < end) {  
            int mid = (beg + end) / 2;  
            mergeSort(arr, beg, mid);  
            mergeSort(arr, mid + 1, end);  
            merge(arr, beg, mid, end);  
        }  
    }
    
    /* Function to merge the subarrays of arr[] */ 
    public void merge(int arr[], int beg, int mid, int end) {    
        int n1 = mid - beg + 1;    
        int n2 = end - mid;    
          
        int LeftArray[n1], RightArray[n2]; //temporary arrays  
          
        /* copy data to temp arrays */  
        for (int i = 0; i < n1; i++)    
        LeftArray[i] = arr[beg + i];    
        for (int j = 0; j < n2; j++)    
        RightArray[j] = arr[mid + 1 + j];    
          
        int i = 0; /* initial index of first sub-array */  
        int j = 0; /* initial index of second sub-array */   
        int k = beg;  /* initial index of merged sub-array */  
          
        while (i < n1 && j < n2) {    
            if(LeftArray[i] <= RightArray[j]) {    
                arr[k] = LeftArray[i];    
                i++;    
            } else {    
                arr[k] = RightArray[j];    
                j++;    
            }    
            k++;    
        } 
        
        while (i<n1) {    
            arr[k] = LeftArray[i];    
            i++;    
            k++;    
        }    
          
        while (j<n2) {    
            arr[k] = RightArray[j];    
            j++;    
            k++;    
        }    
    }
}
```
> `Time Complexity` : **θ(nLogn)**   
> `Auxiliary Space` : **O(n)**     
> `Algorithmic Paradigm` : **Divide and Conquer**     
> `Sorting In Place` : **No**          
> `Stable` : **Yes**         
### Drawbacks of Merge Sort
> * Slower comparative to the other sort algorithms for smaller tasks.
> * Merge sort algorithm requires an additional memory space of 0(n) for the temporary array.
> * It goes through the whole process even if the array is sorted.

### Applications of Merge Sort     
> Merge Sort is useful for sorting **linked lists** in O(nLogn) time.          
> In the case of linked lists, the case is different mainly due to the difference in memory allocation of arrays and linked lists. 
> Unlike arrays, linked list nodes may not be adjacent in memory. Unlike an array, in the linked list, we can insert items in the middle in 
> O(1) extra space and O(1) time. Therefore, the merge operation of merge sort can be implemented without extra space for linked lists.
> In arrays, we can do random access as elements are contiguous in memory. Let us say we have an integer (4-byte) array A and let the address of A[0] 
> be x then to access A[i], we can directly access the memory at (x + i*4). Unlike arrays, we can not do random access in the linked list. Quick Sort 
> requires a lot of this kind of access. In a linked list to access i’th index, we have to travel each and every node from the head to i’th node as we 
> don’t have a continuous block of memory. Therefore, the overhead increases for quicksort. Merge sort accesses data sequentially and the need of random access is low.
---
Video Explanations -> [Merge Sort](https://youtu.be/JSceec-wEyw) 
<hr>
