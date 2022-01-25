# Radix Sort
> Read [this](https://www.geeksforgeeks.org/radix-sort/) article for more information about Radix Sort.           
### Algorithm
> radixSort(arr,size)
>  1. find max of input array arr. 
>  2. find number of digits d in max. 
>  //run the for loop for d times and each time use counting sort to sort arr elements basis on unit,ten's, hundred's etc places.
>  3. for i = 1 to d
>      3.1 sort the array elements according to ith place digits using countingSort.
>-------------------------------------------------------------------
> countingSort(array, sizeOfArr, place)
>  1. k --> find largest element among dth place elements.
>  2. initialize count array with all elements as zeros.
>  3. for i = 0 to (size-1)
>      3.1 find the total count of each unique digit in dth place of elements and store the count at ith index in the count array.
>  4. for i = 0 to k
>      4.1 find the cumulative sum and store it in count array itself. 
>  5. for j = (size-1) to 1
>      5.1 store the elements from input array to output array using index from count array.
>      5.2 decrease count of each element stored by 1.
```java
class RadixSort {
    public static void radixSort(int[] arr) {
        // find maximun element
        int max = arr[0];
        for(int i=1; i<arr.length; i++) {
            if(arr[i] > max) {
                max = arr[i];
            }
        }
        
        for(int exp=1; max/exp > 1; exp*=10) {
            countSort(arr, exp);
        }
    }
    
    public static void countSort(int[] arr, int exp) {
        // any number can lie between 0-9
        int[] count = new int[10];
        for(int val: arr) {
            int e = (val/exp)%10;
            count[e]++;
        }
        
        // subtracting 1 in count[0] to make 0 based indexing 
        count[0] = count[0]-1;
        for(int i=1; i<count.length; i++) {
            count[i] += count[i-1];
        }
        
        int[] output = new int[arr.length];
        for(int i=arr.length-1; i>=0; i--) {
            int e = (arr[i]/exp)%10;
            output[count[e]] = arr[i];
            count[e]--;
        }
        
        for(int i=0; i<arr.length; i++) {
            arr[i] = output[i];
        }
    }    
}
```
> `Time Complexity` : **O(d(n+k))**, where d is the number of digits in the largest element(max) of the input array, n is the number of elements in the array and k is the range of the elements.          
> For Decimal numbers k is 10 so we can ignore k, so Time Complexity is **O(d*n)**     
> `Auxiliary Space` : **O(n+k)**, same as count sort.             
> `Stable` : **Yes** 
---  
Video Explanations -> [Radix Sort](https://youtu.be/Il45xNUHGp0) 
<hr>
