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
|vector           ||
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
|list          |                |
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


## stack
|stack   |后进先出栈                        |
|--------|----------------------------------|
|empty();|当栈为空时，返回true              |
|size(); |返回栈中元素的数目                |
|pop();  |删除栈顶元素，不返回值            |
|top();  |返回栈顶元素的值，但不删除栈顶元素|
|push(x);|入栈                              |
## deque
|deque         |双端队列，两头都有vector的高效性质，还可以实现元素的随机访问|
|:-------------|:-----------------------------------------------------------|
|push_front(x);|                                                            |
|f[n];         |                                                            |
|pop_front();  |返回void                                                    |
## queue
|queue   |                                          |
|:-------|:-----------------------------------------|
|push(x);|将x接到队列的末端                         |
|pop();  |删除队列中第一个元素，并不会返回该元素的值|
|front();|访问队首的元素                            |
|back(); |访问队尾的元素                            |
|empty();|如果队列为空，返回true                    |
|size(); |返回队列中元素的个数                      |
## ——priority_queue
**定义方法**
```c++
priority_queue<int,vector<int>,greater<int>>
priority_queue<int,vector<int>,less<int>>
priority_queue<int>
```
|priority_queue|有优先级管理的队列                |
|--------------|----------------------------------|
|empty();      |队列为空，返回true                |
|size();       |返回队列元素的个数                |
|front();      |返回队首值，但不删除              |
|pop();        |删除队首元素，不返回值            |
|top(）;       |返回具有最高优先级的元素，但不删除|
|push();       |在适当位置插入新元素              |
## string
-string的初始化方式
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
```c++
int pos;
char ch[100];
getline(cin,s);
```
|string               |iter前插t                                                                 |
|---------------------|--------------------------------------------------------------------------|
| =,assign();|赋以新值|
|+=,append(),push_back();|在尾部添加字符|
|[],at();|存取单一字符 |
|back();||
|begin();end();|提供类似STL的迭代器支持|
|capacity();|返回重新分配之前的字符容量|
|cbegin();||
|cend();||
|clear();|删除全部字符|
|compare();||
|copy();|将某值赋值为一个C_string |
|crbegin();||
|crend();||
|c_str(); |返回c风格的字符串 |
|data();|将内容以字符数组形式返回 无’\0’|
|empty();|判断字符串是否为空|
|end();||
|earse(iter);          ||
|earse(q,h);          ||
|earse(pos,n);        |删除pos开始的n个字符  |
|find(s1)             |s1在s中第一次出现的位置  |
|find_first_not_of(s1)|每个s1都有四种重载版本 s1,pos（从pos开始找），s1,pos,n(匹配s1的前n个字母）|
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
|max_size();|返回字符的可能最大个数|
|pop_back();||
|push_back();||
|rbegin();rend();|逆向迭代器|
|replace(q,h,s1);     |   |
|replace(pos.len.s1); |删除pos开始的len个字符并以s1代替插进去  |
|reserve();|保留一定量内存以容纳一定数量的字符|
|resize();||
|rfind(s1)            |s1在s中最后一次出现的位置  |
|swap();|交换两个字符串的内容|
|shrink_to_fit();||
|size(),length();|返回字符数量|
|substr(pos,n);       |返回从pos开始的n个字符的字符串      |
|substr(pos);         ||
|==,!=,<,<=,>,>=,compare();|比较字符串 |
|s==s1,s>s1,s<s1 | 字符串的比较     |
| >>,getline();|从stream读取某值|
|<<|将谋值写入stream|

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



## ——set和multiset
|set                             |                                            |
|--------------------------------|--------------------------------------------|
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

## ——bitset
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
容器（Container）

算法（Algorithm）

迭代器（Iterator）

仿函数（Function object）

适配器（Adaptor）

空间配置器（allocator）


|       迭代器功能       |                     |
|:----------------------:|:--------------------|
|输入迭代器Input iterator|Reads forward|istream|
|    
                    |                     |
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