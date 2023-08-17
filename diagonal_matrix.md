# **题目描述**
>给你一个大小为 m x n 的矩阵 mat ，请以对角线遍历的顺序，用一个数组返回这个矩阵中的所有元素。  

**示例 1：**  
>输入：mat = [[1,2,3],[4,5,6],[7,8,9]]  
>输出：[1,2,4,7,5,3,6,8,9]  

**示例 2：**
>输入：mat = [[1,2],[3,4]]  
>输出：[1,2,3,4]  

**提示：**
>m == mat.length  
>n == mat[i].length  
>1 <= m, n <= 104  
>1 <= m * n <= 104  
>-105 <= mat[i][j] <= 105  

<br/>

# **解法**
    int* findDiagonalOrder(int** mat, int matSize, int* matColSize, int* returnSize){
        int col_len = (*matColSize);
        *returnSize = matSize * col_len;
        int *res = (int *)malloc(sizeof(int) * (*returnSize));
        int row = 0;
        int col = 0;
        int flag = 1;
        for(int i = 0; i < (*returnSize); i++){
            res[i] = mat[row][col];
            if(flag == 1){
                if(row == 0 || col == (col_len - 1)){
                    if(col != (col_len - 1)){
                        col++;
                    }else{
                        row++;
                    }
                    flag = 0;
                }else{
                    row--;
                    col++;
                }
            }else{
                if(col == 0 || row == (matSize - 1)){
                    if(row != (matSize - 1)){
                        row++;
                    }else{
                        col++;
                    }
                    flag = 1;
                }else{
                    row++;
                    col--;
                }
            }
        }
        return res;
    }

# **主要思路**
>根据方向来判定路线，上升路线到顶下如果右边有数先右边数据，否则走下部数据。下降路线到边界如果下面有数据先下面数据，否则走右边数据