#  STL使用总结 
  
----------------
##  ——vector
  
```c++
vector<int> f,f1;
vector<int>::iterator iter,q,h;
int n,x;
```
<style>
table th:first-of-type{
    width:200px;
}
  
</style>
|vector||
|:---|:---|
|push_back(x)|在尾部插入元素x,返回void; |
|pop_back();|删除最后一个元素，返回void,可以直接赋值f1=f;可以直接比较大小|
|insert(iter,x)|在iter前面插入x，返回指向新添加元素的迭代器;|
|insert(iter,n,x);|在iter前面插入n个x，返回void; |
|insert(iter,q,h);|在迭代器iter前面插入q和h范围内的所以元素；|
|size();|返回类型：vector<int>::size_type,也可直接用int，long|
|begin();||
|end();||
|rbegin();||
|rend();||
|empty();|如果数组为空，返回true|
|back();|最后一个元素|
|front();|返回第一个元素|
|at(x);|返回下标x位置的数据|
|f[n];|返回第n个元素|
|erase(iter);|删除iter指向的元素，返回所删除值后面的元素的迭代器，若删除的是最后一个元素返回f.end()一样的位置|
|erase(q,h);|删除q-h所有元素（包括q，不包括h)，返回指向后面的的若h就是f.end(),还返回f.end();|
|clear();|清空所以元素,返回void|
|f1=swap(f);||
|resize();||
|reserve();|改变当前vector所分配空间的大小|
|capacity();|当前vector分配的大小|
|assign(q,h);|f先清空,然后把来自另一个vector的从q到h的元素复制进来|
|assign(n,x);|f先清空，然后赋为n个x|
##  ——list
  
|list|支持快速插入删除,就是个链表|
|:---|:---|
|push_front(x);|不能用f[n]来访问|
|pop_front();|返回void|
##  ——stack
  
|stack|后进先出栈|
|---|---|
|empty();|当栈为空时，返回true|
|size();|返回栈中元素的数目|
|pop();|删除栈顶元素，不返回值|
|top();|返回栈顶元素的值，但不删除栈顶元素|
|push(x);|入栈|
##  ——deque
  
|deque|双端队列，两头都有vector的高效性质，还，可以实现元素的随机访问|
|:---|:---|
|push_front(x);||
|f[n];||
|pop_front();|返回void|
##  ——queue
  
|queue||
|:-|:-|
|push(x);|将x接到队列的末端|
|pop();|删除队列中第一个元素，并不会返回该元素的值|
|front();|访问队首的元素|
|back();|访问队尾的元素|
|empty();|如果队列为空，返回true|
|size();|返回队列中元素的个数|
##  ——priority_queue
  
**定义方法**
```c++
priority_queue<int,vector<int>,greater<int>>
priority_queue<int,vector<int>,less<int>>
priority_queue<int>
```
|priority_queue|有优先级管理的队列|
|---|---|
|empty();|队列为空，返回true|
|size();|返回队列元素的个数|
|front();|返回队首值，但不删除|
|pop();|删除队首元素，不返回值|
|top(）;|返回具有最高优先级的元素，但不删除|
|push();|在适当位置插入新元素|
##  ——string
  
```c++
int pos;
char ch[100];
getline(cin,s);
```
|string |iter前插t|
|---|---|
|insert(iter,t);|iter前插t|
|insert(iter,n,t); |iter前n个插t|
|insert(iter,q,h);||
|arse(iter);||
|earse(q,h);||
|insert(pos,n,t);|在pos前插入n个t|
|insert(pos,ch,n);||
|insert(pos,ch);||
|earse(pos,n);|删除pos开始的n个字符|
|substr(pos,n);|返回从pos开始的n个字符的字符串|
|substr(pos);||
|replace(pos.len.s1);|删除pos开始的len个字符并以s1代替插进去|
|replace(q,h,s1);||
|find(s1)|s1在s中第一次出现的位置|
|rfind(s1)|s1在s中最后一次出现的位置|
|find_first_of(s1)|在s中查找s任意字符第一次出现|
|find_last_of(s1)|在s中查找s任意字符最后一次出现|
|find_first_not_of(s1)|每个s1都有四种重载版本 s1,pos（从pos开始找），s1,pos,n(匹配s1的前n个字母）|
|find_last_not_of(s1)||
|s==s1,s>s1,s<s1|字符串的比较|
##  ——map
  
```c++
map<string,int> f;
map<string,int>::key_type 键的类型
map<string,int>::mapped_type 值的类型
map<string,int>::value_type pair类型,其中first为一个常量，而sencond为一个可变量
//下标读取有危险(如果没有会插入）
```
|map||
|---|---|
|begin();||
|clear();||
|count("hello")|返回”hello"出现的次数，对于map，返回的就是0或1|
|empty();||
|end();||
|equal_range();||
|erase();|1.传入键（返回0or1)，2.传入迭代器(void)，3.传入一对迭代器(void)|
|find("hello")|返回对应的迭代器，否则返回f.end()处|
|get_allocator();|返回map的配置器|
|insert();||
|key_comp();||
|lower_bound();||
|max_size();||
|rbegin();||
|rend();||
|size();||
|swap();||
|upper_bound();||
|value_comp();||
  
  
  
##  ——set和multiset
  
|set||
|---|---|
|begin();|返回一个指向第一个元素的迭代器|
|clear();|清除所有元素|
|count(x);|返回某个元素的个数|
|empty（);|如果集合为空，返回true|
|end();|返回指向最后一个元素的迭代器|
|equal_range();|返回集合中与给定值相等的上下限的两个迭代器|
|erase(x);|删除集合中的元素|
|find(x);|返回一个指向被查找元素x的迭代器|
|get_allocator();|返回集合的分配器|
|insert(x);|在集合中插入元素|
|insert(set1.begin(),set1.end());||
|lower_bound();|返回指向大于(或等于)某值的第一个元素的迭代器|
|key_comp();|返回一个用于元素间值比较的函数|
|max_size()|返回集合能容纳的元素的最大限值|
|rbegin();|返回指向最后一个元素的迭代器|
|rend();|返回一个指向第一个元素的迭代器|
|size();|集合中元素的数目|
|swap();|交换两个集合变量|
|upper_bound();|返回大于某个值元素的迭代器|
|value_comp();|返回一个用于比较元素间的值的函数|
  
##  ——bitset
  
|bitset||
|:-|:---|
|any()|是否存在为1的二进制位|
|none()||
|size()||
|f[n]|下标寻址|
|test(n)||
|set() |全部置为1|
|set(n)|第n位置为1|
|reset()|全部置为0|
|reset(n)||
|flip()逐位取反||
|flip(n)||
|to_ulong()|把它返回会unsigned long|
  
  
##  ——bitset2
  
|bitset||
|:-|:---|
|any()|是否存在为1的二进制位|
|none()||
|size()||
|f[n]|下标寻址|
|test(n)||
|set() |全部置为1|
|set(n)|第n位置为1|
|reset()|全部置为0|
|reset(n)||
|flip()逐位取反||
|flip(n)||
|to_ulong()|把它返回会unsigned long|
  
|aa|bb|cc|
|--|--|--|
|1||2|
|3|>|4|
|5|6||
|^|7|8|
  
##  STL六大组件
  
---  
容器（Container）
  
算法（Algorithm）
  
迭代器（Iterator）
  
仿函数（Function object）
  
适配器（Adaptor）
  
空间配置器（allocator）
  
  
|迭代器功能|
|:-:|:-|
|输入迭代器Input iterator|Reads forward|istream|
|||
  
<table>
    <tr>
        <td>列3一</td> 
        <td>列2二</td> 
   </tr>
   <tr>
        <td colspan="2">合并行</td>    
   </tr>
   <tr>
        <td>列5一</td> 
        <td>列5二</td> 
   </tr>
    <tr>
        <td rowspan="2">合并列</td>    
        <td align="center">行二列二</td>  
    </tr>
    <tr>
        <td>行三列二</td>  
    </tr>
</table>
  
  
<table>
    <tr>
        <td align = "center">列666一</td> 
        <td>列一</td> 
   </tr>
    <tr>
        <td colspan="2">合并行555555555555555555555555555</td>    
    </tr>
    <tr>
        <td colspan="2">合并行</td>    
    </tr>
</table>
  
  
..* **前导空格**
- houhouhou  