# Matrix Multiplication
Question -> [Matrix Multiplication](https://nados.io/question/matrix-multiplication?zen=true)    

### Implementation
```java
public class Main {
    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);
        int r1 = sc.nextInt();
        int c1 = sc.nextInt();
        int[][] a1 = new int[r1][c1];
        for(int i=0; i<r1; i++) {
            for(int j=0; j<c1; j++) {
                a1[i][j] = sc.nextInt();
            }
        }

        int r2 = sc.nextInt();
        int c2 = sc.nextInt();
        int[][] a2 = new int[r2][c2];
        for(int i=0; i<r2; i++) {
            for(int j=0; j<c2; j++) {
                a2[i][j] = sc.nextInt();
            }
        }

        if(c1 != r2) {
            System.out.println("Invalid input");
            return;
        }

        int[][] product = new int[r1][c2];
        for(int i=0; i<product.length; i++) {
            for(int j=0; j<product[0].length; j++) {
                for(int k=0; k<r2; k++) {
                    product[i][j] += a1[i][k]*a2[k][j];
                }
            }
        }

        for(int i=0; i<product.length; i++) {
            for(int j=0; j<product[0].length; j++) {
                System.out.print(product[i][j]+" ");
            }
            System.out.println();
        }
    }
}
```
> `Time Complexity` : **O(Row1\*Column2\*Column1)**, Column1 = Row2       
> `Space Complexity` : **O(Row1*Column2)**
---
Video Explanations -> [Matrix Multiplication](https://youtu.be/0dGuTLr6xT4?list=PL-Jc9J83PIiFkOETg2Ybq-FMuJjkZSGeH)   
<hr>
