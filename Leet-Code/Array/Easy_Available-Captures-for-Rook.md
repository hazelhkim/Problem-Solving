# Available Captures for Rook

<img width="834" alt="Screen Shot 2019-09-28 at 9 24 05 PM" src="https://user-images.githubusercontent.com/46575719/65824397-5ee9c200-e236-11e9-9456-9f847f2819dc.png">
<img width="830" alt="Screen Shot 2019-09-28 at 9 24 16 PM" src="https://user-images.githubusercontent.com/46575719/65824399-601aef00-e236-11e9-849f-2e48efe8fb85.png">
<img width="827" alt="Screen Shot 2019-09-28 at 9 24 25 PM" src="https://user-images.githubusercontent.com/46575719/65824400-614c1c00-e236-11e9-8ae9-781d9e0fa2ed.png">


```java
    public int numRookCaptures(char[][] board) {
        int x0 = 0, y0 = 0, res = 0;
        for (int i = 0; i < 8; ++i)
            for (int j = 0; j < 8; ++j)
                if (board[i][j] == 'R') {
                    x0 = i;
                    y0 = j;
                }

        for (int[] d : new int[][] {{1, 0}, {0, 1}, { -1, 0}, {0, -1}}) {
            for (int x = x0 + d[0], y = y0 + d[1]; 0 <= x && x < 8 && 0 <= y && y < 8; x += d[0], y += d[1]) {
                if (board[x][y] == 'p') res++;
                if (board[x][y] != '.') break;
            }
        }
        return res;
    }

```
