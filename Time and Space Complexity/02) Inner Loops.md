# Complexities for Loops having Inner Loops

```java
for(int i=0; i<n; i++) {
    for(int j=0; j<n; j++) {
        // Doing Constant Work
    }
}
```
> Outer loop will run for **n** times and for every outer loop inner loop will run for **n** times, so in total loops will run for **n\*n** times.     
> `Time Complexity` : **O(N<sup>2</sup>)**, `Space Complexity` : **O(1)** 
---

```java
for(int i=0; i<n; i++) {
    for(int j=0; j<n; j=j*2) {
        // Doing Constant Work
    }
}
```
> Outer loop will run for **n** times and for every outer loop inner loop will run for **logn** times, so in total loops will run for **nlogn** times.     
> `Time Complexity` : **O(NlogN)**, `Space Complexity` : **O(1)** 
---

```java
int j;
for(int i=0; i<n; i+j) {
    for(j=0; j<k; j++) {
        // Doing Constant Work
    }
}
```
> i+j = i+k, since when inner loop ends j becomes equal to k.        
> Inner Loop will run for k times and outer loop will run for N/k times          
> `Time Complexity` : **O(N)**, `Space Complexity` : **O(1)** 
---

```java
for(int i=0; i<n; i++) {
    for(int j=i; j<n; j++) {
        // Doing Constant Work
    }
}
```
> In total loops will run for **N+(N-1)+(N-2)+......+1** times and this is a sum of N natural numbers which is **N(N-1)/2**.          
> `Time Complexity` : **O(N<sup>2</sup>)**, `Space Complexity` : **O(1)** 
---

```java
for(int i=1; i<=n; i++) {
    for(int j=0; j<i; j++) {
        // Doing Constant Work
    }
}
```
> In total loops will run for **1+2+....+N** times and this is a sum of N natural numbers which is **N(N-1)/2**.          
> `Time Complexity` : **O(N<sup>2</sup>)**, `Space Complexity` : **O(1)** 
---

```java
for(int i=1; i<=n; i=i*2) {
    for(int j=0; j<i; j++) {
        // Doing Constant Work
    }
}
```
> Outer loop will run for **logN** times.   
> Inner loop will run for **1+2+4+8+....** continues till logN times. This is forming GP and sum of N numbers of GP is a(r<sup>n</sup>-1)/r-1 and     
> here n = logn, so **1(2<sup>logn</sup>-1)/2-1** which will be **2<sup>logn</sup>** and by using log properties it will become **n<sup>log2</sup>** which is **n**    
> hence in total loop will run for **n** times.               
> `Time Complexity` : **O(N)**, `Space Complexity` : **O(1)** 
---
