# **题目描述**
>给你一幅由 N × N 矩阵表示的图像，其中每个像素的大小为 4 字节。请你设计一种算法，将图像旋转 >90 度。不占用额外内存空间能否做到？  

**示例 1:**  
>给定 matrix = 
>[  
>&emsp;[1,2,3],  
>&emsp;[4,5,6],  
>&emsp;[7,8,9]  
>],  
>原地旋转输入矩阵，使其变为:  
>[  
>&emsp;[7,4,1],  
>&emsp;[8,5,2],  
>&emsp;[9,6,3]  
>]  

**示例 2:**
>
>给定 matrix =  
>[  
>&emsp;[ 5, 1, 9,11],  
>&emsp;[ 2, 4, 8,10],  
>&emsp;[13, 3, 6, 7],  
>&emsp;[15,14,12,16]  
>],   
>原地旋转输入矩阵，使其变为:  
>[  
>&emsp;[15,13, 2, 5],  
>&emsp;[14, 3, 4, 1],  
>&emsp;[12, 6, 8, 9],  
>&emsp;[16, 7,10,11]  
>]  

<br/>

# **解法**
    void rotate(int** matrix, int matrixSize, int* matrixColSize){
        int index = 0;
        //确定交换环数
        for(int i = matrixSize; i > 1; i-=2){
            //确定每一环交换的次数
            for(int j = 0; j < i -1; j++){
                //旋转
                int increase = index + j;
                int decrease = matrixSize - 1 - index -j;
                int fixNum = matrixSize - 1 - index;
                int temp = matrix[index][index+j];
                matrix[index][increase] = matrix[decrease][index];
                matrix[decrease][index] = matrix[fixNum][decrease];
                matrix[fixNum][decrease] = matrix[increase][fixNum];
                matrix[increase][fixNum] = temp;
            }
            index++;
        }
    }

# **主要思路**
>按照矩阵四个角相互交换的方式逐渐旋转