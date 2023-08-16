# **题目描述**
>编写一种算法，若M × N矩阵中某个元素为0，则将其所在的行与列清零。  

**示例 1：**  
>输入：  
>&emsp;[  
>&emsp;&emsp;[1,1,1],  
>&emsp;&emsp;[1,0,1],  
>&emsp;&emsp;[1,1,1]  
>&emsp;]  
>输出：
>&emsp;[  
>&emsp;&emsp;[1,0,1],  
>&emsp;&emsp;[0,0,0],  
>&emsp;&emsp;[1,0,1]  
>&emsp;]  

**示例 2：**  
>输入：  
>&emsp;[  
>&emsp;&emsp;[0,1,2,0],  
>&emsp;&emsp;[3,4,5,2],  
>&emsp;&emsp;[1,3,1,5]  
>&emsp;]  
>输出：  
>&emsp;[  
>&emsp;&emsp;[0,0,0,0],  
>&emsp;&emsp;[0,4,5,0],  
>&emsp;&emsp;[0,3,1,0]  
>&emsp;]  

<br/>

# **解法**
    void setZeroes(int** matrix, int matrixSize, int* matrixColSize){
        int *row = (int *)malloc(sizeof(int) * matrixSize);
        int *col = (int *)malloc(sizeof(int) * (*matrixColSize));
        memset(row, 0, sizeof(int) * matrixSize);
        memset(col, 0, sizeof(int) * (*matrixColSize));

        for(int i = 0; i < matrixSize; i++){
            for(int j = 0; j < (*matrixColSize); j++){
                if(matrix[i][j] == 0){
                    row[i] = 1;
                    col[j] = 1;
                }
            }
        }

        for(int i = 0; i < matrixSize; i++){
            for(int j = 0; j < (*matrixColSize); j++){
                if(row[i] == 1 || col[j] == 1){
                    matrix[i][j] = 0;
                }
            }
        }
    }

**主要思路**
>找出所有行列的位置，并标记，然后清除对应行列的值