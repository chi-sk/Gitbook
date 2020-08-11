# STL使用总结
----------------
## vector
```c++
vector<int> f,f1;
vector<int>::iterator iter,q,h;
int n,x;
```
<style>
table th:first-of-type{
    width:20px;
}


</style>
|vector           |向量|
|:----|:---|
|assign(q,h);     |f先清空,然后把来自另一个vector的从q到h的元素复制进来|
|assign(n,x);     |f先清空，然后赋为n个x |
|at(x);           |返回下标x位置的数据 |
|back();          |最后一个元素 |
|begin();         ||
|capacity();      |当前vector分配的大小|
|cbegin();||
|cend();||
|clear();         |清空所以元素,返回void |
|crbegin();||
|crend();||
|data();||
|emplace();||
|emplace_back();||
|empty();||
|end();||
|erase(iter);     |删除iter指向的元素，返回所删除值后面的元素的迭代器，若删除的是最后一个元素返回f.end()一样的位置|
|erase(q,h);      |删除q-h所有元素（包括q，不包括h)，返回指向后面的的若h就是f.end(),还返回f.end();|
|front();|返回第一个元素 |
|get_allocator();||
|insert(iter,x)   |在iter前面插入x，返回指向新添加元素的迭代器; |
|insert(iter,n,x);|在iter前面插入n个x，返回void; |
|insert(iter,q,h);|在迭代器iter前面插入q和h范围内的所以元素；|
|max_size();||
|operator=||
|operator[]|返回第n个元素|
|push_back(x)     |在尾部插入元素x,返回void;|
|pop_back();      |删除最后一个元素，返回void,可以直接赋值f1=f;可以直接比较大小|
|rbegin();        ||
|rend();          ||
|reserve();       |改变当前vector所分配空间的大小|
|resize();        ||
|shrink_to_fit();||
|size();          |返回类型：vector<int>::size_type,也可直接用int，long|
|f1=swap(f);      ||
## list
|list          |  双向链表              |
|:-------------|:---------------|
|assign();||
|back();||
|begin();||
|cbegin();||
|cend();||
|clear();||
|crbegin();||
|crend();||
|emplace();||
|emplace_back();||
|emplace_front();||
|empty();||
|end();||
|erase();||
|front();||
|get_allocator();||
|insert();||
|max_size();||
|merge();||
|operator=||
|pop_back();||
|pop_front();  |返回void        |
|push_back();||
|push_front(x);|不能用f[n]来访问|
|rbegin();||
|remove();||
|remove_if();||
|rend();||
|resize();||
|reverse();||
|size();||
|sort();||
|splice();||
|swap();||
|unique();||

## queue
|queue   |  队列                                        |
|:-------|:-----------------------------------------|
|push(x);|将x接到队列的末端                         |
|pop();  |删除队列中第一个元素，并不会返回该元素的值|
|front();|访问队首的元素                            |
|back(); |访问队尾的元素                            |
|empty();|如果队列为空，返回true                    |
|size(); |返回队列中元素的个数                      |

## stack
|stack   |堆栈容器                       |
|--------|----------------------------------|
|empty();|当栈为空时，返回true              |
|size(); |返回栈中元素的数目                |
|pop();  |删除栈顶元素，不返回值            |
|top();  |返回栈顶元素的值，但不删除栈顶元素|
|push(x);|入栈                              |
## deque
|deque         |双向队列容器，两头都有vector的高效性质，还可以实现元素的随机访问|
|:-------------|:-----------------------------------------------------------|
|push_front(x);|                                                            |
|f[n];         |                                                            |
|pop_front();  |返回void                                                    |

## priority_queue
**定义方法**
```c++
priority_queue<int,vector<int>,greater<int>>
priority_queue<int,vector<int>,less<int>>
priority_queue<int>
```
|priority_queue|一种按值排序的队列容器               |
|:--------------|:----------------------------------|
|empty();      |队列为空，返回true                |
|size();       |返回队列元素的个数                |
|front();      |返回队首值，但不删除              |
|pop();        |删除队首元素，不返回值            |
|top(）;       |返回具有最高优先级的元素，但不删除|
|push();       |在适当位置插入新元素              |

## set和multiset
|set                             |集合容器/允许出现重复元素的集合容器            |
|:--------------------------------|:--------------------------------------------|
|begin();                        |返回一个指向第一个元素的迭代器              |
|clear();                        |清除所有元素                                |
|count(x);                       |返回某个元素的个数                          |
|empty（);                       |如果集合为空，返回true                      |
|end();                          |返回指向最后一个元素的迭代器                |
|equal_range();                  |返回集合中与给定值相等的上下限的两个迭代器  |
|erase(x);                       |删除集合中的元素                            |
|find(x);                        |返回一个指向被查找元素x的迭代器             |
|get_allocator();                |返回集合的分配器                            |
|insert(x);                      |在集合中插入元素                            |
|insert(set1.begin(),set1.end());|                                            |
|lower_bound();                  |返回指向大于(或等于)某值的第一个元素的迭代器|
|key_comp();                     |返回一个用于元素间值比较的函数              |
|max_size()                      |返回集合能容纳的元素的最大限值              |
|rbegin();                       |返回指向最后一个元素的迭代器                |
|rend();                         |返回一个指向第一个元素的迭代器              |
|size();                         |集合中元素的数目                            |
|swap();                         |交换两个集合变量                            |
|upper_bound();                  |返回大于某个值元素的迭代器                  |
|value_comp();                   |返回一个用于比较元素间的值的函数            |

## string
- string的初始化方式
```c++
string s;                          //生成一个空字符串s 
string s(str);                     //拷贝构造函数生成str的复制品 
string s(str, stridx);             // 将字符串str内"始于位置stridx"的部分当作字符串的初值 
string s(str, stridx, strlen) ;    // 将字符串str内"始于stridx且长度顶多strlen"的部分作为字符串的初值 
string s(cstr) ;                   // 将C字符串（以NULL结束）作为s的初值 
string s(chars, chars_len) ;       // 将C字符串前chars_len个字符作为字符串s的初值。 
string s(num, ‘c’) ;               // 生成一个字符串，包含num个c字符 
string s(“value”);  string s=“value”;  // 将s初始化为一个字符串字面值副本
string s(begin, end);              // 以区间begin/end(不包含end)内的字符作为字符串s的初值 
string s1(“hello”);
string s3=s1+”world”;  //合法操作
string s4=”hello”+”world”;  //非法操作：两个字符串字面值相加
s.~string();                       //销毁所有字符，释放内存 

```
使用标准C++中string类，必须要包含
```cpp
#include <string>// 注意是<string>，不是<string.h>，带.h的是C语言中的头文件

using  std::string;

using  std::wstring;
```
或
```cpp
using namespace std;
```
```c++
int pos;
char ch[100];
getline(cin,s);
```
|string               |iter前插t 
|---------------------|---------------------------|
| `string &operator=(const string &s);`,assign();|把字符串s赋给当前字符串|
|`string &assign(const char *s);`|用c类型字符串s赋值|
|`string &assign(const char *s,int n);`|用c字符串s开始的n个字符赋值|
|`string &assign(const string &s);`|把字符串s赋给当前字符串|
|`string &assign(int n,char c);`|用n个字符c赋值给当前字符串|
|`string &assign(const string &s,int start,int n);`|把字符串s中从start开始的n个字符赋给当前字符串|
|`string &assign(const_iterator first,const_itertor last);`|把first和last迭代器之间的部分赋给字符串|
|`string &operator+=(const string &s);`|在尾部添加字符|
|`string &append(const char *s);`|把c类型字符串s连接到当前字符串结尾|
|`string &append(const char *s,int n);`|把c类型字符串s的前n个字符连接到当前字符串结尾|
|`string &append(const string &s);`|同operator+=()|
|`string &append(const string &s,int pos,int n);`|把字符串s中从pos开始的n个字符连接到当前字符串的结尾|
|`string &append(int n,char c);`|在当前字符串结尾添加n个字符c|
|`string &append(const_iterator first,const_iterator last);`|把迭代器first和last之间的部分连接到当前字符串的结尾|
|`const char &operator[](int n) const;` <br>`const char &at(int n) const;`<br>`char &operator[](int n);`<br>`char &at(int n);`|存取单一字符,at函数提供范围检查，<br>当越界时会抛出out_of_range异常，<br>下标运算符[]不提供检查访问。 |
|back();||
|begin();end();|提供类似STL的迭代器支持|
|int capacity()const;|返回当前容量（即string中不必增加内存即可存放的元素个数）|
|cbegin();||
|cend();||
|clear();|删除全部字符|
|compare();||
|int copy(char *s, int n, int pos = 0) const;|将某值赋值为一个C_string |
|crbegin();||
|crend();||
|const char *data()const; |返回c风格的字符串 |
|const char *data()const;//|将内容以字符数组形式返回 无’\0’|
|bool empty()const; |判断字符串是否为空|
|end();||
|earse(iter);          ||
|earse(q,h);          ||
|earse(pos,n);        |删除pos开始的n个字符  |
|find(s1)             |s1在s中第一次出现的位置  |
|find_first_not_of(s1)|每个s1都有四种重载版本 s1,pos（从pos开始找），<br>s1,pos,n(匹配s1的前n个字母）|
|find_first_of(s1)    |在s中查找s任意字符第一次出现    |
|find_last_not_of(s1) |    |
|find_last_of(s1)     |在s中查找s任意字符最后一次出现 |
|front();||
|get_allocator();|返回配置器|
|insert(iter,t);      |iter前插t  |
|insert(iter,n,t);    |iter前n个插t  |
|insert(iter,q,h);    | |
|insert(pos,n,t);     |在pos前插入n个t|
|insert(pos,ch,n);    | |
|insert(pos,ch);      ||
|length();||
|int max_size()const;|返回string对象中可存放的最大字符串的长度|
|pop_back();||
|push_back();||
|rbegin();rend();|逆向迭代器|
|replace(q,h,s1);     |   |
|replace(pos.len.s1); |删除pos开始的len个字符并以s1代替插进去  |
|reserve();|保留一定量内存以容纳一定数量的字符|
|void resize(int len,char c);|把字符串当前大小置为len，并用字符c填充不足的部分|
|rfind(s1)            |s1在s中最后一次出现的位置  |
|swap();|交换两个字符串的内容|
|shrink_to_fit();||
|`int size()const;`<br> `int length()const;`|返回当前字符串的大小|
|substr(pos,n);       |返回从pos开始的n个字符的字符串      |
|substr(pos);         ||
|bool operator==(const string &s1,const string &s2)const;|比较两个字符串是否相等|
|==,!=,<,<=,>,>=,compare();|均被重载用于字符串的比较|
|s==s1,s>s1,s<s1 | 字符串的比较     |
| >>,getline();|从stream读取某值|
|<<|将谋值写入stream|

**string类的字符操作：**
```cpp
const char &operator[](int n)const;
const char &at(int n)const;
char &operator[](int n);
char &at(int n);
operator[]和at()均返回当前字符串中第n个字符的位置，但at函数提供范围检查，当越界时会抛出out_of_range异常，下标运算符[]不提供检查访问。
const char *data()const;//返回一个非null终止的c字符数组
const char *c_str()const;//返回一个以null终止的c字符串
int copy(char *s, int n, int pos = 0) const;//把当前串中以pos开始的n个字符拷贝到以s为起始位置的字符数组中，返回实际拷贝的数目
```
**string的特性描述:**
```cpp
int capacity()const;    //返回当前容量（即string中不必增加内存即可存放的元素个数）
int max_size()const;    //返回string对象中可存放的最大字符串的长度
int size()const;        //返回当前字符串的大小
int length()const;       //返回当前字符串的长度
bool empty()const;        //当前字符串是否为空
void resize(int len,char c);//把字符串当前大小置为len，并用字符c填充不足的部分

```
**string类的输入输出操作:**
```cpp
string类重载运算符operator>>用于输入，同样重载运算符operator<<用于输出操作。
函数getline(istream &in,string &s);用于从输入流in中读取字符串到s中，以换行符'\n'分开。
```
**string的赋值：**
```cpp
string &operator=(const string &s);//把字符串s赋给当前字符串
string &assign(const char *s);//用c类型字符串s赋值
string &assign(const char *s,int n);//用c字符串s开始的n个字符赋值
string &assign(const string &s);//把字符串s赋给当前字符串
string &assign(int n,char c);//用n个字符c赋值给当前字符串
string &assign(const string &s,int start,int n);//把字符串s中从start开始的n个字符赋给当前字符串
string &assign(const_iterator first,const_itertor last);//把first和last迭代器之间的部分赋给字符串
```
**string的连接：**
```cpp
string &operator+=(const string &s);//把字符串s连接到当前字符串的结尾 
string &append(const char *s);            //把c类型字符串s连接到当前字符串结尾
string &append(const char *s,int n);//把c类型字符串s的前n个字符连接到当前字符串结尾
string &append(const string &s);    //同operator+=()
string &append(const string &s,int pos,int n);//把字符串s中从pos开始的n个字符连接到当前字符串的结尾
string &append(int n,char c);        //在当前字符串结尾添加n个字符c
string &append(const_iterator first,const_iterator last);//把迭代器first和last之间的部分连接到当前字符串的结尾
```
**string的比较：**
```cpp
bool operator==(const string &s1,const string &s2)const;//比较两个字符串是否相等
运算符">","<",">=","<=","!="均被重载用于字符串的比较；
int compare(const string &s) const;//比较当前字符串和s的大小
int compare(int pos, int n,const string &s)const;//比较当前字符串从pos开始的n个字符组成的字符串与s的大小
int compare(int pos, int n,const string &s,int pos2,int n2)const;//比较当前字符串从pos开始的n个字符组成的字符串与s中

　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　//pos2开始的n2个字符组成的字符串的大小
int compare(const char *s) const;
int compare(int pos, int n,const char *s) const;
int compare(int pos, int n,const char *s, int pos2) const;
compare函数在>时返回1，<时返回-1，==时返回0   

```
**string的子串：**
```cpp
string substr(int pos = 0,int n = npos) const;//返回pos开始的n个字符组成的字符串
```
**string的交换：**
```cpp
void swap(string &s2);    //交换当前字符串与s2的值
```
**string类的查找函数：**
```cpp
int find(char c, int pos = 0) const;//从pos开始查找字符c在当前字符串的位置
int find(const char *s, int pos = 0) const;//从pos开始查找字符串s在当前串中的位置
int find(const char *s, int pos, int n) const;//从pos开始查找字符串s中前n个字符在当前串中的位置
int find(const string &s, int pos = 0) const;//从pos开始查找字符串s在当前串中的位置
//查找成功时返回所在位置，失败返回string::npos的值 
int rfind(char c, int pos = npos) const;//从pos开始从后向前查找字符c在当前串中的位置
int rfind(const char *s, int pos = npos) const;
int rfind(const char *s, int pos, int n = npos) const;
int rfind(const string &s,int pos = npos) const;
//从pos开始从后向前查找字符串s中前n个字符组成的字符串在当前串中的位置，成功返回所在位置，失败时返回string::npos的值 
int find_first_of(char c, int pos = 0) const;//从pos开始查找字符c第一次出现的位置
int find_first_of(const char *s, int pos = 0) const;
int find_first_of(const char *s, int pos, int n) const;
int find_first_of(const string &s,int pos = 0) const;
//从pos开始查找当前串中第一个在s的前n个字符组成的数组里的字符的位置。查找失败返回string::npos 
int find_first_not_of(char c, int pos = 0) const;
int find_first_not_of(const char *s, int pos = 0) const;
int find_first_not_of(const char *s, int pos,int n) const;
int find_first_not_of(const string &s,int pos = 0) const;
//从当前串中查找第一个不在串s中的字符出现的位置，失败返回string::npos 
int find_last_of(char c, int pos = npos) const;
int find_last_of(const char *s, int pos = npos) const;
int find_last_of(const char *s, int pos, int n = npos) const;
int find_last_of(const string &s,int pos = npos) const; 
int find_last_not_of(char c, int pos = npos) const;
int find_last_not_of(const char *s, int pos = npos) const;
int find_last_not_of(const char *s, int pos, int n) const;
int find_last_not_of(const string &s,int pos = npos) const;
//find_last_of和find_last_not_of与find_first_of和find_first_not_of相似，只不过是从后向前查找
```
**string类的替换函数：**
```cpp
string &replace(int p0, int n0,const char *s);//删除从p0开始的n0个字符，然后在p0处插入串s
string &replace(int p0, int n0,const char *s, int n);//删除p0开始的n0个字符，然后在p0处插入字符串s的前n个字符
string &replace(int p0, int n0,const string &s);//删除从p0开始的n0个字符，然后在p0处插入串s
string &replace(int p0, int n0,const string &s, int pos, int n);//删除p0开始的n0个字符，然后在p0处插入串s中从pos开始的n个字符
string &replace(int p0, int n0,int n, char c);//删除p0开始的n0个字符，然后在p0处插入n个字符c
string &replace(iterator first0, iterator last0,const char *s);//把[first0，last0）之间的部分替换为字符串s
string &replace(iterator first0, iterator last0,const char *s, int n);//把[first0，last0）之间的部分替换为s的前n个字符
string &replace(iterator first0, iterator last0,const string &s);//把[first0，last0）之间的部分替换为串s
string &replace(iterator first0, iterator last0,int n, char c);//把[first0，last0）之间的部分替换为n个字符c
string &replace(iterator first0, iterator last0,const_iterator first, const_iterator last);//把[first0，last0）之间的部分替换成[first，last）之间的字符串
```
**string类的插入函数：**
```cpp
string &insert(int p0, const char *s);
string &insert(int p0, const char *s, int n);
string &insert(int p0,const string &s);
string &insert(int p0,const string &s, int pos, int n);
//前4个函数在p0位置插入字符串s中pos开始的前n个字符
string &insert(int p0, int n, char c);//此函数在p0处插入n个字符c
iterator insert(iterator it, char c);//在it处插入字符c，返回插入后迭代器的位置
void insert(iterator it, const_iterator first, const_iterator last);//在it处插入[first，last）之间的字符
void insert(iterator it, int n, char c);//在it处插入n个字符c
```
**string类的删除函数:**
```cpp
iterator erase(iterator first, iterator last);//删除[first，last）之间的所有字符，返回删除后迭代器的位置
iterator erase(iterator it);//删除it指向的字符，返回删除后迭代器的位置
string &erase(int pos = 0, int n = npos);//删除pos开始的n个字符，返回修改后的字符串
```
**string类的迭代器处理：**
```cpp
string类提供了向前和向后遍历的迭代器iterator，迭代器提供了访问各个字符的语法，类似于指针操作，迭代器不检查范围。
用string::iterator或string::const_iterator声明迭代器变量，const_iterator不允许改变迭代的内容。常用迭代器函数有：
const_iterator begin()const;
iterator begin();                //返回string的起始位置
const_iterator end()const;
iterator end();                    //返回string的最后一个字符后面的位置
const_iterator rbegin()const;
iterator rbegin();                //返回string的最后一个字符的位置
const_iterator rend()const;
iterator rend();                    //返回string第一个字符位置的前面
rbegin和rend用于从后向前的迭代访问，通过设置迭代器string::reverse_iterator,string::const_reverse_iterator实现
```
**字符串流处理：**
通过定义ostringstream和istringstream变量实现，`#include <sstream>`头文件中
例如：
```cpp
 string input("hello,this is a test");
    istringstream is(input);
    string s1,s2,s3,s4;
    is>>s1>>s2>>s3>>s4;//s1="hello,this",s2="is",s3="a",s4="test"
    ostringstream os;
    os<<s1<<s2<<s3<<s4;
    cout<<os.str();
```
参考文献：[标准C++中的string类的用法总结 ](https://www.cnblogs.com/xFreedom/archive/2011/05/16/2048037.html)
## map
```c++
map<string,int> f;
map<string,int>::key_type 键的类型
map<string,int>::mapped_type 值的类型
map<string,int>::value_type pair类型,其中first为一个常量，而sencond为一个可变量
//下标读取有危险(如果没有会插入）
```
|map             ||
|----------------|--|
|begin();        ||
|cbegin();        ||
|cend();||
|clear();        ||
|count("hello")  |返回”hello"出现的次数，对于map，返回的就是0或1 |
|crbeging();||
|crend();||
|emplace();||
|emplace_hint();||
|empty();        ||
|end();          ||
|equal_range();  ||
|erase();        |1.传入键（返回0or1)，2.传入迭代器(void)，3.传入一对迭代器(void)|
|find("hello")   |返回对应的迭代器，否则返回f.end()处|
|get_allocator();|返回map的配置器|
|insert();       ||
|insert_or_assign();||
|key_comp();     ||
|lower_bound();  ||
|max_size();     ||
|operator=||
|operator[]||
|rbegin();       ||
|rend();         ||
|size();         ||
|swap();         ||
|try_emplace();||
|upper_bound();  ||
|value_comp();   ||



## bitset
|    bitset    |                       |
|:------------:|:----------------------|
|    any()     |是否存在为1的二进制位  |
|    none()    |                       |
|    size()    |                       |
|     f[n]     |下标寻址               |
|   test(n)    |                       |
|    set()     |全部置为1              |
|    set(n)    |第n位置为1             |
|   reset()    |全部置为0              |
|   reset(n)   |                       |
|flip()逐位取反|                       |
|   flip(n)    |                       |
|  to_ulong()  |把它返回会unsigned long|




|aa|bb|cc|
|--|--|--|
|1 |2 |  |
|3 |> |4 |
|5 |6 |  |
|^ |7 |8 |

## STL六大组件
---  
### **容器（Container）**
在数据存储上，有一种对象类型，它可以持有其它对象或指向其它对像的指针，这种对象类型就叫做容器。
STL 对定义的通用容器分三类：顺序性容器、关联式容器和容器适配器。 

**顺序性容器** 是 一种各元素之间有顺序关系的线性表，是一种线性结构的可序群集。顺序性容器中的每个元素均有固定的位置，除非用删除或插入的操作改变这个位置。这个位置和 元素本身无关，而和操作的时间和地点有关，顺序性容器不会根据元素的特点排序而是直接保存了元素操作时的逻辑顺序。比如我们一次性对一个顺序性容器追加三 个元素，这三个元素在容器中的相对位置和追加时的逻辑次序是一致的。 

**关联式容器** 和 顺序性容器不一样，关联式容器是非线性的树结构，更准确的说是二叉树结构。各元素之间没有严格的物理上的顺序关系，也就是说元素在容器中并没有保存元素置 入容器时的逻辑顺序。但是关联式容器提供了另一种根据元素特点排序的功能，这样迭代器就能根据元素的特点“顺序地”获取元素。 

关联式容器另一个显著的特点是它是以键值的方式来保存数据，就是说它能把关键字和值关联起来保存，而顺序性容器只能保存一种（可以认为它只保存关键字，也可以认为它只保存值）。这在下面具体的容器类中可以说明这一点。 

**容器适配器** 是一个比较抽象的概念， C++的 解释是：适配器是使一事物的行为类似于另一事物的行为的一种机制。容器适配器是让一种已存在的容器类型采用另一种不同的抽象类型的工作方式来实现的一种机 制。其实仅是发生了接口转换。那么你可以把它理解为容器的容器，它实质还是一个容器，只是他不依赖于具体的标准容器类型，可以理解是容器的模版。或者把它 理解为容器的接口，而适配器具体采用哪种容器类型去实现，在定义适配器的时候可以由你决定。 

下表列出STL 定义的三类容器所包含的具体容器类：
|顺序性容器||
|---|---|
|vector|从后面快速的插入与删除，直接访问任何元素|
|list|双链表，从任何地方快速插入与删除|
|deque|从前面或后面快速的插入与删除，直接访问任何元素|

|关联容器 ||
|---|---|
|set|快速查找，不允许重复值 |
|multiset|快速查找，允许重复值 |
|map|一对多映射，基于关键字快速查找，不允许重复值 |
|multimap|一对多映射，基于关键字快速查找，允许重复值|

|容器适配器 ||
|---|---|
|stack|后进先出|
|queue|先进先出 |
|priority_queue|最高优先级元素总是第一个出列|
### **算法（Algorithm）**
STL提供了大约100个实现算法的模版函数，比如算法for_each将为指定序列中的每一个元素调用指定的函数，stable_sort以你所指定的规则对序列进行稳定性排序等等。只要我们熟悉了STL之后，许多代码可以被大大的化简，只需要通过调用一两个算法模板，就可以完成所需要的功能并大大地提升效率。
算法部分主要由头文件`<algorithm>`，`<numeric>`和`<functional>`组成。
`<algorithm>`是所有STL头文件中最大的一个（尽管它很好理解），它是由一大堆模版函数组成的，可以认为每个函数在很大程度上都是独立的，其中常用到的功能范围涉及到比较、交换、查找、遍历操作、复制、修改、移除、反转、排序、合并等等。
`<numeric>`体积很小，只包括几个在序列上面进行简单数学运算的模板函数，包括加法和乘法在序列上的一些操作。
`<functional>`中则定义了一些模板类，用以声明函数对象
STL中算法大致分为四类：
1）非可变序列算法：指不直接修改其所操作的容器内容的算法。
2）可变序列算法：指可以修改它们所操作的容器内容的算法。
3）排序算法：对序列进行排序和合并的算法、搜索算法以及有序序列上的集合操作。
4）数值算法：对容器内容进行数值计算。
### **迭代器（Iterator）**

- 迭代器类似C++的指针，能够使程序方便快捷的访问STL容器的内容，STL定义了5仲类型的迭代器，根据使用方法而命名，按其类型包含输入、输出、前向、双向和随机访问迭代器。

- 指针是c语言中就有的东西，迭代器是c++中才有的，指针用起来灵活高效，迭代器功能更丰富些。
- 迭代器提供一个对容器对象或者string对象的访问的方法，并且定义了容器范围。

**迭代器按照定义方式分成以下四种：**
正向迭代器定义方法
```cpp
容器类名::iterator  迭代器名;
```
常量正向迭代器定义方法：
```cpp
容器类名::const_iterator  迭代器名;
```
反向迭代器定义方法：
```cpp
容器类名::reverse_iterator  迭代器名;
```
常量反向迭代器定义方法：
```cpp
容器类名::const_reverse_iterator  迭代器名;
```
**常用的迭代器操作**
1)所有容器的迭代器都可进行的操作
```cpp
*iter 、 ++iter 、 --iter、 iter1==iter2、 iter1!=iter2
```
2)vector和deque容器的迭代器可进行的额外操作
```cpp
iter+n、 iter-n 、 > 、 >= 、 < 、 <=
//这是因为vector和deque容器实际上是两个数组，只有对数组才能执行额外操作;
```
3)迭代器范围
```cpp
[begin,end)
```
**不同容器的迭代器的功能:**
|容器|迭代器功能|
|---|---|
|vector|随机访问|
|deque|随机访问|
|list|双向|
|set/multiset|双向|
|map/multimap|双向|
|stack|不支持迭代器|
|queue|不支持迭代器|
|priority_queue|不支持迭代器|
### 仿函数（Function object）

仿函数是早期的命名，C++标准规格定案后采用的新名称是函数对象（function objects）（也就是一种具有函数特质的对象）。

**为什么要有仿函数**
由于函数指针毕竟不能满足STL对抽象对象的需求，也不能满足软件积木的需求——函数指针无法和STL其它组件（如配接器adapter）搭配使用，产生更灵活的变化。

**仿函数的作用:**
在C++的STL提供的各种算法，例如sort()。往往有两个版本，其中一个是最长用的某种运算的版本（operator<）;第二个版本则表现出最泛化的演算流程，允许用户“以template参数来指定所需要采取的策略”。
**仿函数实现示例**
```cpp
//仿函数1,比较大小
template<typename T> struct comp
{
    bool operator()(T in1, T in2) const
    {
        return (in1>in2);
    }
};
 
comp<int> m_comp_objext;
cout << m_comp_objext(6, 3) << endl;     //使用对象调用
cout << comp<int>()(1, 2) << endl;       //使用仿函数实现,comp<int>()(1, 2)是产生一个临时（无名的）对象。
```
**仿函数详细说明**
在下面的使用场景（统计一个容器中的符合规定的元素），将说明之前提到的函数指针为什么不能在STL中替换掉仿函数
```cpp
bool my_count(int num)
{
    return (num < 5);
}
 
int a[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
std::vector<int> v_a(a, a+10);
cout << "count: " << std::count_if(v_a.begin(), v_a.end(), my_count);
```
在上面我们传递进去了一个函数指针作为count_if的比较条件。但是现在根据新的需求，不再统计容器中小于5的变量个数，改为了8或者3。那么最直接的方法就是加一个参数threshold就可以了，就像下面这样
```cpp
bool my_count(int num， int threshold)
{
    return (num < threshold));
}

```
但是这样的写法STL中是不能使用的，而且当容器中的元素类型发生变化的时候就不能使用了，更要命的是不能使用模板函数。
那么，既然多传递传递参数不能使用，那就把需要传递进来的那个参数设置为全局的变量，那样确实能够实现当前情况下对阈值条件的修改，但是修改起来存在隐患（要是没有初始化就调用怎么办）。因而解决这样问题的方式就是仿函数,如下所示：
```cpp
template<typename T> struct my_count1
{
    my_count1(T a)
    {
        threshold = a;
    }
    T threshold;
    bool operator()(T num)
    {
        return (num < threshold);
    }
};
 
int a[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
std::vector<int> v_a(a, a+10);
 
cout << "count: " << std::count_if(v_a.begin(), v_a.end(), my_count1<int>(8));

```
### 适配器（Adaptor）
适配器是标准库里一个通用的概念。容器、迭代器、和函数都有适配器。本质上，一个适配器是一种机制，使得某种事物的行为看起来像另外一种事物一样。
**通俗易懂的说，适配器更通俗易懂的翻译是改造器。是把一个事物，改造一下接口等等。使得其看起来像一个新的事物。适配器其实是一种应用在STL的设计模式。**
C++中有很多适配器的实现和用法，比如：
1.容器适配器：C++STL的容器stack和queue ，默认就是改造了deque。

2.迭代器适配器：反向迭代器，在正向迭代器的基础上改造而成。


思想：

A改造了B,A就要代表了B,A就要提供接口给人们使用。 但A自己所做的主要的事情都是交给B做。A是作为一个桥梁，是使用者和幕后的B的一个桥梁。

实现：

A拥有了B的功能，在编程上有两种方法实现，一种是继承，一种是内含。

在C++STL里，所有的适配器 都是一种内含的方法。

总结：适配器是设计模式在STL中的一种体现。
**使用场合**
从两个角度说，为什么要学习C++的函数适配器bind（）函数。

考虑一种情况,有一个数组，一个需求是 计算出容器中小于50的数的个数。

很多人立即想到有一个算法是count_if(beg,end,pred);

beg和end是容器的范围，而pred可以是一个函数。不过对于我们这个需求，这个函数有点特殊，它需要接受两个参数，第一个参数就是容器中的元素，第二个参数是50。这就有两个问题出现了，
第一个问题: count_if 所要求的pred函数必须只能接受一个参数。而我们的需求需要接受两个。

第二个问题： 如果程序中我们的需求变了呢？比如我们在后面的程序要计算的是容器中小于40的数的个数呢？我们当然可以编写很多个函数来解决这个问题，但这不符合软件工程的思想。

因此：我们C++11引入了bind这个函数适配器，它接受一个函数，生成一个新的函数来改变原来函数的参数列表。比如减少原来函数的参数个数，或者顺序。使得它满足新的需求。
**使用方法**
```cpp
//头文件和命名空间
#include<functional>

using namespace std::placeholders; //主要为了后面的占位符

//使用举例
bind(函数名，arg_list);
```
arg_list 是一个被逗号分隔的原来函数的参数列表，里面可包含占位符.n代表新的函数里的参数的位置。 看下简单的例子，就会很快就懂了。
**改造一个函数**
```cpp
double my_divide(double x, double y)
	{
		return x/y;
	}
        //给x绑定为10，y绑定为2。
        auto fn_five = bind(bind_::my_divide, 10, 2);	//return 10/2
	cout << fn_five() << endl;//5
        //使用占位符_1，新生成的函数里面有一个参数。并且对应到到原来函数的第一个参数中。
	auto fn_half = bind(bind_::my_divide, _1, 2);	//x/2
	cout << fn_half(10) << endl;					//5
        //使用两个占位符_2,_1。新生成的函数里面有两个参数，并且两个参数的调用顺序被改变。
	auto fn_invert = bind(bind_::my_divide, _2, _1);	//return y/x
	cout << fn_invert(10, 2) << endl;					//0.2
        //设定返回类型
	auto fn_rounding = bind<int>(bind_::my_divide, _1, _2);	//return int(x/y)
	cout << fn_rounding(10, 3) << endl;             //3
```
**总结一下**
1.bind 的参数列表中有几个 _n，新生成的函数里面就有几个参数。

2.bind的一个作用是可以改变参数的顺序和参数的个数。
**解决我们开头的问题**
考虑一种情况,有一个数组，一个需求是 计算出容器中小于50的数的个数。很多人立即想到有一个算法是count_if(beg,end,pred);

深入一点：我们前面说bind的形式是： bind(函数名，arg_list);

其实bind改造的不一定是函数，而是可调用对象。：包括函数，函数指针，函数对象，lambda表达式。
这里我们采用改造标准库函数对象的方式解决这个问题。
```cpp
vector<int>  v{15,37,94,50,73,58,28,90};
auto fn=bind(less<int>(),_1,50);
cout<<coutif(v.begin(),v.end(),fn_);//3
 
```
以上适配器相关内容参考自博客[C++适配器](https://zhuanlan.zhihu.com/p/55924014)
### 空间配置器（allocator）

在STL中，Memory Allocator 处于最底层的位置，为一切的 Container 提供存储服务，是一切其他组件的基石。对于一般使用 STL 的用户而言，Allocator 是不可见的，如果需要对 STL 进行扩展，如编写自定义的容器，就需要调用 Allocator 的内存分配函数进行空间配置。

在C++中，一个对象的内存配置和释放一般都包含两个步骤，对于内存的配置，首先是调用operator new来配置内存，然后调用对象的类的构造函数进行初始化；而对于内存释放，首先是调用析构函数，然后调用 operator delete进行释放。

STL空间配置器更多详细内容参考博客；[STL空间配置器allocator详解](https://blog.csdn.net/xy913741894/article/details/66974004)

---
## C++ 标准库概览

C++ 标准库以若干头文件的方式提供,下面简单介绍一个各头文件的内容。
### 第一部分 容器 Containers
- **\<array\>**
C++11 新增。提供了容器类模板 std::array，固定大小数组的容器。
- **\<bitset\>**
提供了专门用来存放位组（一系列 bit）的容器类 std::bitset。
- **\<deque\>**
提供了双向队列容器类模板 std::deque。
- **\<forward_list\>**
C++11 新增。提供了单向链表容器类模板 std::forward_list。
- **\<list\>**
提供了双向链表容器类模板 std::list。
- **\<map\>**
提供了类模板 std::map 和 std::multimap，前者是有序的一组偶对，后者与前者类似但允许键重复。
- **\<queue\>**
提供了由 std::duque （经过适配器模式）包装而来的容器类 std::queue，即单向队列。还提供了优先队列std::priority_queue。
- **\<set\>**
提供了容器类模板 std::set 和 std::multiset。
- **\<stack\>**
提供了由 std::duque （经过适配器模式）包装而来的容器类 std::stack，即栈。
- **\<unordered_map\>**
C++11 新增。提供了容器类模板 std::unordered_map 和 std::unordered_multimap，它们都属于哈希表（散列表）。
- **\<unordered_set\>**
C++11 新增。提供了容器类模板 std::unordered_set 和 std::unordered_multiset。
- **\<vector\>**
提供了容器类模板 std::vector，即动态数组。
### 第二部分 通用 General
- **\<algorithm\>**
提供了很多针对 STL 容器的算法。
- **\<chrono\>**
提供了诸如 std::chrono::duration 和 std::chrono::time_point 等的时间元素，还有时钟。
- **\<functional\>**
提供了一些函数对象（如仿函数）。
- **\<iterator\>**
提供了与迭代器相关的一些类和模板。
- **\<memory\>**
提供了 C++ 内存管理的工具，例如 std::unique_ptr，std::shared_ptr，std::weak_ptr。
- **\<stdexcept\>**
这里面有一些表示异常的类，例如 std::exception，std::logic_error，std::runtime_error。
- **\<tuple\>**
C++11 新增。提供了元组 std::tuple。
- **\<utility\>**
提供了类模板偶对 std::pair 。所谓偶对，就是放在一起的、有序的两个东西 (a,b)。提供了 namespacestd::rel_ops，用来更简便地使用运算符重载。
### 第三部分 本地化 Localization
- **\<locale\>**
以类和函数的形式封装了与区域有关的操作。
- **\<codecvt>**
提供了不同代码页（code page）之间字符编码的转换功能。
### 第四部分 字符串 Strings
- **\<string>**
提供了 C++ 标准的字符串类和字符串模板。
- **\<regex>**
C++11 新增。提供了用正则表达式进行字符串匹配的功能。
### 第五部分 流与输入输出 Streams and Input/Output
- **\<fstream>**
提供了对文件的输入输出设施。
- **\<iomanip>**
提供了控制输出格式的功能。例如，基于特定的进制数格式化整数，或者控制浮点数的精度。
- **\<ios>**
提供了 iostream 需要的一些类型和函数。
- **\<iosfwd>**
提供了一些与 I/O 有关的转发操作。
- **\<iostream>**
提供了 C++ 输入与输出的基础层。
- **\<istream>**
提供了类模板 std::istream 和其他与输入相关的辅助类。
- **\<ostream>**
提供了类模板 std::ostream 和其他与输出相关的辅助类。
- **\<sstream>**
提供了类模板 std::stringstream 和其他用来处理字符串流的类。
- **\<streambuf>**
提供了对字符序列（文件或字符串）进行读写的基础设施。
### 第六部分 辅助 Language support
- **\<exception>**
提供了一些与异常处理有关的类型和函数。
- **\<limits>**
提供了类模板 std::numeric_limits，用来描述基本数字类型的最值。
- **\<new>**
与 new 和 delete 运算符有关的一些类型和函数。
- **\<typeinfo>**
C++ 运行时的类型信息的一些工具。
### 第七部分 线程支持 Thread support library
- **\<thread>**
C++11新增。提供了使用线程所需要的类和 namespace。
- **\<mutex>**
C++11新增。这里面有互斥对象（mutex），锁（lock），还有 once（一种用来保证某函数在某进程中只执行一次的对象）。
- **\<condition_variable>**
C++11新增。条件变量。一个条件变量代表一个条件，当一个条件变量等待时，它会阻塞当前线程，直到它代表的条件为真。
- **\<future>**
C++11新增。可以用它来进行便捷的异步操作，以免代码中出现一大堆回调函数。
### 第八部分 数学与数值计算 Numerics library
使得 C++ 程序可以执行（不完善的）数学运算的组件。
- **\<complex>**
复数相关。
- **\<random>**
（伪）随机数相关。
- **\<valarray>**
定义了五个类模板 valarray，slice_array，gslice_array，mask_array，indirect_array，两个类slice，gslice，还有一系列相关的函数模板。
- **\<numeric>**
一些通用的数学运算。
### 第九部分 C 标准库 C standard library
C 标准库也可以在 C++ 中使用。