# **题目描述**
>编写一个函数来查找字符串数组中的最长公共前缀。  
>如果不存在公共前缀，返回空字符串 ""。  

**示例 1：**
>输入：strs = ["flower","flow","flight"]  
>输出："fl"  

**示例 2：**
>输入：strs = ["dog","racecar","car"]  
>输出：""  
>解释：输入不存在公共前缀。  

**提示：**
>1 <= strs.length <= 200  
>0 <= strs[i].length <= 200  
>strs[i] 仅由小写英文字母组成  

<br/>

# **解法**
    char * longestCommonPrefix(char ** strs, int strsSize){
        char* res = (char*)malloc(sizeof(char) *200);
        int index = 0;
        while(strs[0][index] != '\0'){
            for(int i = 1; i < strsSize; i++){
                if(strs[i][index] == '\0' || strs[i][index] != strs[0][index]){
                    res[index] = '\0';
                    return res;
                }  
            }
            res[index] = strs[0][index];
            index++;
            
        }
        res[index] = '\0';
        return res;   
    }

# **主要思路**
>主要分配一个最大的buf进行填充，C不支持数组自动填充