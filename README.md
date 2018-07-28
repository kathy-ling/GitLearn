# GitLearn
全排列在笔试面试中很热门，因为它难度适中，既可以考察递归实现，又能进一步考察非递归的实现，便于区分出考生的水平。所以在百度和迅雷的校园招聘以及程序员和软件设计师的考试中都考到了，因此本文对全排列作下总结帮助大家更好的学习和理解。对本文有任何补充之处，欢迎大家指出。
首先来看看题目是如何要求的（百度迅雷校招笔试题）。
#一、字符串的排列
用C++写一个函数, 如 Foo(const char *str), 打印出 str 的全排列,
如 abc 的全排列: abc, acb, bca, dac, cab, cba
##一、全排列的递归实现

为方便起见，用123来示例下。123的全排列有123、132、213、231、312、321这六种。首先考虑213和321这二个数是如何得出的。显然这二个都是123中的1与后面两数交换得到的。然后可以将123的第二个数和每三个数交换得到132。同理可以根据213和321来得231和312。因此可以知道——全排列就是从第一个数字起每个数分别与它后面的数字交换。找到这个规律后，递归的代码就很容易写出来了：

```
#include<iostream>  
using namespace std;  
#include<assert.h>  
  
void Permutation(char* pStr, char* pBegin)  
{  
    assert(pStr && pBegin);  
  
    if(*pBegin == '\0')  
        printf("%s\n",pStr);  
    else  
    {  
        for(char* pCh = pBegin; *pCh != '\0'; pCh++)  
        {  
            swap(*pBegin,*pCh);  
            Permutation(pStr, pBegin+1);  
            swap(*pBegin,*pCh);  
        }  
    }  
}  
  
int main(void)  
{  
    char str[] = "abc";  
    Permutation(str,str);  
    return 0;  
}  
```
