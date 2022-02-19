# Complexities For Some Common Loops

```java
for(int i=0; i<n; i++) {
    // Doing Constant Work
}
```
> `Time Complexity` : **O(N)**, `Space Complexity` : **O(1)** 
---

```java
for(int i=0; i<n; i=i+c) {
    // Doing Constant Work
}
```
> This loop will run for **n/c** times     
> `Time Complexity` : **O(N)**, `Space Complexity` : **O(1)** 
---

```java
for(int i=n; i>0; i=i-c) {
    // Doing Constant Work
}
```
> This loop will run for **n/c** times     
> `Time Complexity` : **O(N)**, `Space Complexity` : **O(1)** 
---

```java
for(int i=0; i<n; i=i*c) {
    // Doing Constant Work
}
```
> Here 'c' is any constant.      
> Every time 'i' will get incremented by 'c' so this loop will run for **log<sub>c</sub>n** times.   
> `Time Complexity` : **O(logN)**, `Space Complexity` : **O(1)** 
---

```java
for(int i=n; i>0; i=i/c) {
    // Doing Constant Work
}
```
> Here 'c' is any constant.      
> Every time 'i' will get decremented by 'c' so this loop will run for **log<sub>c</sub>n** times.   
> `Time Complexity` : **O(logN)**, `Space Complexity` : **O(1)** 
---
