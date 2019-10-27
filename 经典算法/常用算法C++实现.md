
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