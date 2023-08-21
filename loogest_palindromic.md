# **题目描述**
>给你一个字符串 s，找到 s 中最长的回文子串。  
>如果字符串的反序与原始字符串相同，则该字符串称为回文字符串。  

**示例 1：**
>输入：s = "babad"  
>输出："bab"  
>解释："aba" 同样是符合题意的答案。  

**示例 2：**
>输入：s = "cbbd"  
>输出："bb"  

**提示：**
>1 <= s.length <= 1000  
>s 仅由数字和英文字母组成  


<br/>

# **暴力解法**
    char * longestPalindrome(char * s){
        int len = strlen(s);
        if(len <= 1){
            return s;
        }

        int start = 0;
        int end = 0;

        for(int i = 0; i < len; i++){
            //以i为中心的最长子串
            int left = i - 1;
            int right = i + 1;
            while(left >= 0 && right < len){
                if(s[left] != s[right]){
                    break;
                }
                left--;
                right++;
            }
            if((right - left - 2) > (end - start)){
                start = left + 1;
                end = right - 1;
            }

            //以i为边界的最长子串
            int left1 = i;
            int right1 = i + 1;

            while(left1 >= 0 && right1 < len){
                if(s[left1] != s[right1]){
                    break;
                }
                left1--;
                right1++;
            }
            if((right1 - left1 - 2) > (end - start)){
                start = left1 + 1;
                end = right1 - 1;
            }
        }

        int length = end - start +1;
        char *res = (char *)malloc(sizeof(char) * (length + 1));
        memcpy(res, (s + start), (length));
        res[length] = '\0';

        return res;
    }

# **主要思路**
>轮询所有元素，分别已该元素为中心，或已该元素和右侧的一个元素为中心进行遍历，找出最长回文串