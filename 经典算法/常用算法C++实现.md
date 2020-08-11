### 快速找素数的一种方法
```cpp

int main() {
    int n, i, j, tMin = 0x7fffffff;
    vector<int> chart(50001, 1);
    vector<int> prim;
        for(chart[1] = 0, i = 2; i < chart.size(); i++) {
        if(chart[i]) {
            prim.push_back(i); // 依次把素数放进去
            for(j = i*i; j < chart.size(); j += i)
                chart[j] = 0;
        }
    }
    for(auto m:prim) cout<<m<<" ";
}

```


### 字典树的一种非常神奇的实现
题目描述
给出n个只包含小写字母'a'~'z'的字符串s1,s2,…sns_1,s_2,\dots s_ns1​,s2​,…sn​，我们称一个字符串sis_isi​为原根，当且仅当给出的其他任何字符串都不是它的前缀。

现在牛牛想知道给出的字符串中有多少个原根。
（相同字符串互为前缀） 
示例1 
3,["a","ab","ba"]
输出: 2
说明:


"a"是原根
因为"a"是"ab"的前缀，所以"ab"不是原根
"ba"是原根


```cpp
#include <numeric>
 
class Solution {
public:
    int solve(int n, vector<string>& s) {
        vector<vector<int>> trie(1, vector<int>(26));
        vector<int> a(1);
        for (auto si: s) {
            int i = 0, j = 0;
            while (j < si.length() && trie[i][si[j] - 'a']) i = trie[i][si[j++] - 'a'];
            a[i] = 0;
            while (j < si.length()) {
                i = trie[i][si[j++] - 'a'] = trie.size();
                trie.push_back(vector<int>(26));
                a.push_back(j == si.length());
            }
        }
        return accumulate(a.begin(), a.end(), 0);
    }
};
```


### 不使用加法运算求两个整数的和
```cpp
unsigned int add(unsigned int a, unsigned int b)
{
	unsigned int temp = 0;
	for (; b;)
	{
		temp = a ^ b;
		b = (a & b) << 1;
		a = temp;
	}
	return a;
}
```
### 冒泡排序
```cpp
void swap(vector<int>& arr,int i,int j)
{
	int temp = 0;
	temp = arr[i];
	arr[i] = arr[j];
	arr[j] = temp;

}
void BubbleSort(vector<int> &arr)
{
	for (int i = 0; i < arr.size(); i++)
	{
		for (int j = arr.size() - 2; j >=i; j--)
		{
			if (arr[j] < arr[j + 1])
			{
				swap(arr,j,j+1);
			}
		}
	}
}
```
### 插入排序
```cpp
void InsertSort(vector<int> &arr)
{
	int temp = arr[0];
//	int min = 0;
	for (int i = 1; i < arr.size(); i++)
	{
		if (arr[i] < arr[i-1])
		{
			temp = arr[i];
			int j = i - 1;
			for (; j>=0&&arr[j] > temp; j--)
			{
				arr[j + 1] = arr[j];
			}
			arr[j + 1] = temp;
		}
	}
}
```
### 翻转字符转
```cpp
void reverse(char* left,char *right)
{
	char temp;
	for (; (right - left + 1) / 2 > 0;)
	{
		temp = *left;
		*left = *right;
		*right = temp;
		left++; right--;
	}

}
void reverse(string *s)
{
	string s_ = *s;
	int pl = 0,pr = s_.size()-1;
	char temp;
	for (; (pr - pl)+1 / 2 > 0;)
	{
		temp = s_[pl];
		s_[pl] = s_[pr];
		s_[pr] = temp;
		pl++; pr--;
	}
	*s = s_;
}
```
### 判断一个字符串是否为回文串
```cpp

//是回文串返回1，不是则返回0.
bool palindromic(string s)
	{
		int pl = 0, pr = s.size() - 1;
		int i = 0;
		if (s.size() == 1)
			return 1;
		for (; (pr - pl + 1) / 2 > 0;)
		{
			if (s[pl] != s[pr])
				return 0;
			pl++; pr--;

		}
	return 1;
}
```
### 去除字符串中多余的空格
```cpp
//去除字符串中多余的空格，每个单词间只保留一个空格
//输入：char* 字符串
//输出：char*字符转
void fun2(char* s)
{
	char *ch = s, i = 0;
	if (s == nullptr) return;
	while (*ch++ == ' ');
	ch--;
	while (*ch != '\0')
	{   
//		while (*ch++ == ' ');
		
		if (*ch != ' ')
			* (s + i++) = *ch++;
		else if (*(s + i-1) == ' ')
			    ch++;
		     else
			   *(s + i++) = ' ';
	}
	*(s + i - 1) == ' '? *(s + i - 1) = '\0': * (s + i) = '\0';
}
```
### 查找字符串中的最长回文串
```cpp
string longestPalindrome(string s) {
	int slen = 0, sptr = 0;
	int L = 0, R = 0;
	if (s.size() < 1)
		return s;
	for (int i = 0, a = 0; i < 2 * s.size() - slen; i++)
	{
		a = 0; L = i / 2; R = i / 2;
		if (i % 2 == 1) R++;
		for (;; a++) {
			if (s.size() == 1)
				break;
			if (L - a<0 || R + a>s.size() || s[L - a] != s[R + a])
				break;
		}
		if (2 * a-1 + R - L > slen) {
			slen = 2 * a - 1 + R - L; sptr = L - a + 1;
		}
	}
	return s.substr(sptr, slen);
}


```
### 求组合数
```cpp
//求1到n范围内的所有整数中（包含1和n），任意取4个能构成多少种无序组合，并将其返回
vector<vector<int>> combine(int n, int k) {
	if (k > n || k < 0) return {};
	if (k == 0) return { {} };
	vector<vector<int>> res = combine(n - 1, k - 1);
	for (auto& a : res) a.push_back(n);
	for (auto& a : combine(n - 1, k)) res.push_back(a);
	return res;
}

```
### 翻转单链表
```cpp
/*
struct List {
	int data;
	List* next;
};
*/
List* reverstlist(List* list)
{
	if (list == NULL || list->next == NULL)
		return list;
	List* p = list, * q = list->next, * r = q->next;
	p->next = NULL;
	while (q->next != NULL)
	{
		q->next = p;
		p = q;
		q = r;
		r = r->next;
	}
	q->next = p;
	return q;
}
```
背包九讲
```cpp
#include "iostream"
#include "cstring"
#include "algorithm"
using namespace std;
 const int N = 1001;
 
 int n,m;
 int f[N];
 int v[N],w[N];
 
 int main()
 {
     cin>>n>>m;
     for(int i = 1;i<=n;i++) cin>>v[i]>>w[i];
     for(int i = 1;i<=n;i++)
        for(int j = m; j>=v[i];j--)
        {
            f[j] = max(f[j],f[j-v[i]]+w[i]);
        }
    
    cout<<f[m];
 }
```




KMP算法C++实现
```cpp
#include <iostream>
using namespace std;
int __next[20] = {-1};//全局变量int数组

void get_next(string temp, int next[])
{//求解next数组
    int len_temp = (int)temp.length();
    next[1] = 0;//KMP算法中j == 0时，已单独处理。故不必处理next[0],在本例中，在初始化next时，将next[0]=-1；
    int j = 1,k = -1;//k表示temp数组的下标
    while (j < len_temp)//停止条件为 j==len_temp
    {//如何计算呢？ 从j=1开始一个一个计算，直到全部计算结束
        if (k == -1 || temp[j] == temp[k])//temp[j]?temp[k]的结果才是核心条件，k==0是对特殊条件的处理
        {
            next[++j] = ++k;
            /*
            j++;
            k++;
            if (temp[j] != temp[k])
                next[j] = k;
            else
                next[j] = next[k];
            */
        }//已知假设条件是next[j]=k,根据next函数定义可得next[j+1]=k+1
        else
        {
            k = next[k]; //为什么要用k=next[k]?
        }//因为在temp[j]?temp[k]为假后，需要计算P1···Pk在Pk匹配失败后需要移动到的位置，这恰恰也可以看作是部分的KMP算法
        //以P1···Plen_temp作为主串,以P1···Pk为字串在k处失配后的处理，故用k=next[k]
    }
}
void getNext(int next[],int lengthP,string pat){//lengthP为模式串P的长度 

      int j=0,k=-1;//j为P串的下标，k用来记录该下标对应的next数组的值 
      next[0]=-1;//初始化0下标下的next数组值为-1 
      while(j<lengthP){ //对模式串进行扫描 
         if(k==-1||pat[j]==pat[k]){//串后缀与前缀没有相等的子串或者此时j下标下的字符与k下的字符相等。 
             j++;k++; 
             next[j]=k;//设置next数组j下标的值为k 
         }else
             k=next[k];//缩小子串的范围继续比较 
     }
 }

int KMP(string str, string temp)
{
    int len_str = (int)str.length();
    int len_temp = (int)temp.length();
    int i=0;
    int j=0;
    while (i<len_str && j<len_temp)
    {
        if (str[i] == temp[j])//逐个字符进行对比
        {//为真，对比下一个字符
            i++;
            j++;
        }
        else
        {//为假时，有两种情形
            if (j == 0)
                i++;//在本轮匹配的第一个位置匹配失败，需移动到主串的下一个字符开始匹配
            else
                j = __next[j];//在本轮匹配的非第一个位置匹配失败，根据next数组确定从模式串的什么位置开始匹配
        }
    }
    if (j == len_temp)//返回数组下标
        return i - j;
    else
        return -1;
}

int main() {

    string str =  "abcabcbabcabdgct";
    string temp = "aaaaaaa";
    //  a  b  a  c
    //  0  0  1  0  ->1
    // -1  0  0  1  next[]
    
    //  a  a  b
    //  0  1  0 ->1
    // -1  0  1 next[]
    
    //  a  a  a  b
    //  0  1  1  0 ->1
    // -1  0  1  1 next[]
    
    //  a  b  c  a  b  d  a  b  c  d
    //  0  0  0  1  2  0  1  2  3  0 ->1
    // -1  0  0  0  1  2  0  1  2  3 next[]
    get_next(temp, __next);
    cout<<KMP(str, temp)<<endl;
    system("pause");
    return 0;
}



class Solution {
public:
    int strStr(string haystack, string needle) {
        // 建立偏移表
        int hSize=haystack.size();
        int nSize=needle.size();
        unordered_map<char, int> pianyi;
        for(int i=0;i<nSize;i++) pianyi[needle[i]]=nSize-i;

        // 遍历
        int i=0;
        while(i<=hSize-nSize){
            if(haystack.substr(i,nSize)==needle) return i;
            else{
                // 查询substr后的字符的偏移值
                if(i+nSize>hSize-1) return -1;
                else{
                    if(pianyi.find(haystack[i+nSize])!=pianyi.end()){
                        i+=pianyi[haystack[i+nSize]];
                    }
                    else{
                        i+=nSize+1;
                    }
                }
            }
        }

        return -1;
    }
};
```
