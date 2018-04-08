## 36. Valid Sudoku

### Description

Determine if a Sudoku is valid, according to: Sudoku Puzzles - The Rules.

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

### My performance
- Came up with the approach in 7 mins
- Could not implement it within 30 mins

### My thought process/approach
- hashset, validate the valid num, check if it already contains the digit
- do this for all the row, all cols, all 9 sub-boxes
- to do rows, O(n^2)
- to do cols, O(n^2)
- to do sub-boxes, O(n^2)

### Complexity analysis
- Time complexity : O(N^2), or constant if the size is guaranteed to be 9
- space complexity: O(N^2), or constant if the size is guaranteed to be 9
  
### My solution/attempt

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        if (board == null) {
            return false;
        }
        
        int n = 9;
        HashSet<Integer> rowSet = new HashSet<>();
        HashSet<Integer> colSet = new HashSet<>();
        
        for (int i = 0; i < n; i++) {
            rowSet = new HashSet<>();
            colSet = new HashSet<>();
            for (int j = 0; j < n; j++) {
                if (board[i][j] == '.') {
                    continue;
                }
                int rowDigit = (int) (board[i][j] - '0');
                int colDigit = (int) (board[j][i] - '0');
                if (rowSet.contains(rowDigit) || colSet.contains(colDigit)) {
                    return false;
                }
                rowSet.add(rowDigit);
                colSet.add(colDigit);
            }
        }
        int count = 0;
        HashSet<Integer> subBox = new HashSet<>();
        while (count <= 6) {
            for (int i = 0; i < n; i++) {
                if (i % 3 == 0) {
                    subBox = new HashSet<>();
                }
                for (int j = count; j < count + 3; j++) {
                    if (board[i][j] == '.') {
                        continue;
                    }
                    int digit = (int) (board[i][j] - '0');
                    if (subBox.contains(digit)) {
                        return false;
                    }
                    subBox.add(digit);
                }

            } 
            count += 3;
        }
        
        return true;
    }
}
```

### Solution
Solution by Lorraine921 - https://leetcode.com/problems/valid-sudoku/discuss/15450/Shared-my-concise-Java-code

```java
public boolean isValidSudoku(char[][] board) {
    for(int i = 0; i<9; i++){
        HashSet<Character> rows = new HashSet<Character>();
        HashSet<Character> columns = new HashSet<Character>();
        HashSet<Character> cube = new HashSet<Character>();
        for (int j = 0; j < 9;j++){
            if(board[i][j]!='.' && !rows.add(board[i][j]))
                return false;
            if(board[j][i]!='.' && !columns.add(board[j][i]))
                return false;
            int RowIndex = 3*(i/3);
            int ColIndex = 3*(i%3);
            if(board[RowIndex + j/3][ColIndex + j%3]!='.' && !cube.add(board[RowIndex + j/3][ColIndex + j%3]))
                return false;
        }
    }
    return true;
}
```

### Lessons learned
- The main point was to figure out how to traverse the sub-cube within the nested loop (same loop for row and col check)
- Make use of j%3 operation for horizontally moving (0,1,2 -> 0,1,2 -> 0,1,2)
- Make use of j/3 operation for vertically moving (0 -> 1 -> 2)