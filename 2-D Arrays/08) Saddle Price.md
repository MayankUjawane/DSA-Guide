# Saddle Price
Question -> [Saddle Price](https://nados.io/question/saddle-price?zen=true)    

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

        for(int row=0; row<n; row++) {
            //finding minimum in rth row
            int minCol = 0;
            for(int c=1; c<n; c++) {
                if(arr[row][c] < arr[row][minCol]) {
                    minCol = c;
                }
            }

            //checking if it is maximum in that column
            boolean flag = true;
            for(int r=0; r<n; r++) {
                if(arr[r][minCol] > arr[row][minCol]) {
                    flag = false;
                    break;
                }
            }

            if(flag == true) {
                System.out.println(arr[row][minCol]);
                return;
            }
        }
        System.out.println("Invalid input");
    }
}
```
---
Video Explanations -> [Saddle Price](https://youtu.be/6YIWq2JGzEQ?list=PL-Jc9J83PIiFkOETg2Ybq-FMuJjkZSGeH)   
<hr>
