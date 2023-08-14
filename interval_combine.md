# **题目描述**
>以数组 intervals 表示若干个区间的集合，其中单个区间为 intervals[i] = [starti, endi] 。>请你合并所有重叠的区间，并返回 一个不重叠的区间数组，该数组需恰好覆盖输入中的所有区间 。

**示例 1：**
>
>输入：intervals = [[1,3],[2,6],[8,10],[15,18]]  
>输出：[[1,6],[8,10],[15,18]]  
>解释：区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].  

**示例 2：**

>输入：intervals = [[1,4],[4,5]]  
>输出：[[1,5]]  
>解释：区间 [1,4] 和 [4,5] 可被视为重叠区间。  

**提示：**
>1 <= intervals.length <= 104  
>intervals[i].length == 2  
>0 <= starti <= endi <= 104  

<br/>

# **解法**
    static int cmp(int **p1, int **p2)
    {
        return (p1[0][0] > p2[0][0]);
    }

    int** merge(int** intervals, int intervalsSize, int* intervalsColSize, int* returnSize, int** returnColumnSizes){
        int count = 0;
        int left = 0, right = 0;

        //分配空间
        int** array = (int **)malloc(sizeof(int *) * intervalsSize);
        (*returnColumnSizes) = (int *)malloc(sizeof(int)*intervalsSize);
        for(int i = 0; i < intervalsSize; i++){
            array[i] = (int *)malloc(sizeof(int) * (*intervalsColSize));
            (*returnColumnSizes)[i] = (*intervalsColSize);
        }

        //排序intervals
        qsort(intervals, intervalsSize, sizeof(int *), cmp);

        //合并
        for(; right < intervalsSize - 1; right++){
            if(intervals[right][1] < intervals[right+1][0]){
                array[count][0] = intervals[left][0];
                array[count][1] = intervals[right][1];
                count++;
                left = right + 1;
            }else{
                intervals[right+1][1] = intervals[right][1] > intervals[right+1][1] ?  intervals[right][1]:intervals[right+1][1];
            }
        }

        //最后一组
        array[count][0] = intervals[left][0];
        array[count][1] = intervals[right][1];

        *returnSize = count + 1;

        return array;
    }

**主要思路**
>先排序，后更新右边界判定