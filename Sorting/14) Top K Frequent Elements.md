# Top K Frequent Elements
Question -> [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)    

### Implementation
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer,Integer> map = new HashMap();
        for(int num : nums) {
            map.put(num,map.getOrDefault(num,0)+1);
        }
        
        int[] unique = new int[map.size()];
        int i=0;
        for(Map.Entry<Integer,Integer> e : map.entrySet()) {
            unique[i++] = e.getKey();
        }
        
        quickSelect(map, unique, 0, unique.length-1, unique.length-k);
        
        int[] ans = new int[k];
        i = 0, j = unique.length-k;
        while(i < k) {
            ans[i++] = unique[j++];
        }
        
        return ans;
    }
    private void quickSelect(Map<Integer,Integer> freq, int[] arr, int start, int end, int target) {
        int index = partition(freq, arr, start, end);
        
        if(index == target) {
            return;
        } else if(index < target) {
            quickSelect(freq, arr, index+1, end, target);
        } else {
            quickSelect(freq, arr, start, index-1, target);
        }
    }
    private int partition(Map<Integer,Integer> freq, int[] arr, int start, int end) {
        int pivot = arr[end];
        int pivotFreq = freq.get(pivot);
        
        for(int i=start; i<end; i++) {
            if(freq.get(arr[i]) < pivotFreq) {
                swap(arr, start, i);
                start++;
            }
        }
        swap(arr, start, end);
        return start;
    }
    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```
> `Time Complexity` : **O(N)**     
> `Space Complexity` : **O(N)**
---
