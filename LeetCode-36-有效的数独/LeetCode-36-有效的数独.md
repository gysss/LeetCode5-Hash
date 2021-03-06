### 要求
判断一个 9x9 的数独是否有效。只需要根据以下规则，验证已经填入的数字是否有效即可。

数字 1-9 在每一行只能出现一次。
数字 1-9 在每一列只能出现一次。
数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。

### 示例
输入:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
输出: true

输入:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
输出: false
解释: 除了第一行的第一个数字从 5 改为 8 以外，空格内其他数字均与 示例1 相同。但由于位于左上角的 3x3 宫内有两个 8 存在, 因此这个数独是无效的。

### python代码
思路：建立三个函数，分别是判断题目中的三个要求

```python
class Solution:
    def isValidRow(self, board):   
        for i in range(9):
            list_ = []
            for j in range(9):
                if board[i][j] != '.' and board[i][j] in list_:
                    return False
                list_.append(board[i][j])
        return True

    def isValidColumn(self, board):
        for j in range(9):
            list_ = []
            for i in range(9):
                if board[i][j] != '.' and board[i][j] in list_:
                    return False
                list_.append(board[i][j])
        return True
                
    def isValidSquare(self, board):
        for i in range(0, 9, 3):
            for j in range(0, 9, 3):
                list_ = []
                for k in range(i, i+3):
                    for l in range(j, j+3):
                        if board[k][l] != '.' and board[k][l] in list_:
                            return False
                        list_.append(board[k][l])
        return True
    
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """
        return self.isValidRow(board) and self.isValidColumn(board) and self.isValidSquare(board)
```