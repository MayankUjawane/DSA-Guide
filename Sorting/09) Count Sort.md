# Count Sort
> Counting sort is a sorting technique that is based on the **keys between specific ranges**.       
> This sorting technique **doesn't perform sorting by comparing elements**. It performs sorting by counting objects having **distinct key values like hashing**. 
> After that, it performs some arithmetic operations to calculate each object's index position in the output sequence. 
> Counting sort is **not used as a general-purpose sorting algorithm**.         
> Counting sort is effective when **range is not greater than number of objects** to be sorted. It can be used to **sort the negative input values** also.      
### Algorithm
> 1. Find the maximum and minimum elements from the given array.
> 2. Now, initialize array of length (max - min + 1) having all 0 elements. This array will be used to store the frequency of the elements in the given array.
> 3. Store the frequency of each array element at their corresponding index in the frequency array.
> 4. Now, find the actual position of each element in output array by converting frequency array to prefix sum array.
> 5. Build output array by traversing arr in reverse order to make count sort stable.
```java
class CountSort {
    public static void countSort(int[] arr) {
        // finding min and max elements 
        int min=arr[0], max=arr[0];
        for(int val: arr) {
            min = Math.min(min, val);
            max = Math.max(max, val);
        }
        
        // creating frequency array to store frequency of each element
        int range = max-min+1;
        int[] freq = new int[range];
        for(int val: arr) {
            int ind = val-min;
            freq[ind]++; 
        }
        
        // converting frequency array to prefix sum array so that freq[i] 
        // now contains actual position of each element in output array
        for(int i=1; i<freq.length; i++) {
            freq[i] = freq[i] + freq[i-1];
        }
        
        // Build the output character array
        int[] output = new int[arr.length];
        // To make count sort stable we are operating in reverse order.
        for(int i=arr.length-1; i>=0; i--) {
            int element = arr[i];
            int freqIndex = element-min;
            // subtracting 1 to make 0 based indexing
            int ind = freq[freqIndex] - 1;
            output[ind] = element;
            freq[freqIndex]--;
        }
        
        // Store the sorted elements into main array 
        for (int i = 0; i < arr.length; i++) {
            arr[i] = output[i];
        }
    }
}
```
> `Time Complexity` : **O(n+k)**, where n is the number of elements in the array and k is the range of the elements.    
> `Auxiliary Space` : **O(k)**, k is the range of the elements.       
> Larger the range of elements in the given array, larger is the space complexity, hence space complexity of counting sort is bad if the
> range of integers are very large as the auxiliary array of that size has to be made.         
> `Stable` : **Yes** 
---  
Video Explanations -> [Count Sort](https://youtu.be/p-OyKUgIrx4?list=PL-Jc9J83PIiFc7hJ5eeCb579PS8p-en4f) 
<hr>
