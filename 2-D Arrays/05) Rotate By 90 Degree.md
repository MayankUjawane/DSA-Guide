# Rotate By 90 Degree
Question -> [Rotate By 90 Degree](https://nados.io/question/rotate-by-90-degree?zen=true)    

### Implementation
```java
public class Main {
    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] arr = new int[n][n];
        for(int i=0; i<n; i++) {
            for(int j=0; j<n; j++) {
                arr[i][j] = sc.nextInt();
            }
        }
        //Transpose Matrix
        for(int i=0; i<n; i++) {
            for(int j=i; j<n; j++) {
                int temp = arr[i][j];
                arr[i][j] = arr[j][i];
                arr[j][i] = temp;
            }
        }
        //Reverse the Rows
        for(int r=0; r<n; r++) {
            int lc = 0, rc = n-1;
            while(lc < rc) {
                int temp = arr[r][rc];
                arr[r][rc] = arr[r][lc];
                arr[r][lc] = temp;

                lc++;
                rc--;
            }
        }
        display(arr);
    }
    
    public static void display(int[][] arr){
        for(int i = 0; i < arr.length; i++){
            for(int j = 0; j < arr[0].length; j++){
                System.out.print(arr[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```
> `Time Complexity` : **O(Row\*Column)** 
---
Video Explanations -> [Rotate By 90 Degree](https://youtu.be/SoxrXQbhCPI?list=PL-Jc9J83PIiFkOETg2Ybq-FMuJjkZSGeH)   
<hr>
