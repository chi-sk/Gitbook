# C++学习笔记

### 指向类成员函数的指针的使用：

```C++
class A {
public:
	void fun();
};
void A::fun()
{
	cout << "Hello World !" << endl;
}
typedef void (A::* pp)();
int main()
{
pp ip;
	ip = &A::fun;
	(b.*ip)();
}
```


```flow
st=>start: Start
op=>operation: Your Operation
cond=>condition: Yes or No?
e=>end

st->op->cond
cond(yes)->e
cond(no)->op
```
- [ ] **七月旅行准备**
    - [ ] 准备邮轮上需要携带的物品
    - [ ] 浏览日本免税店的物品
    - [x] 购买蓝宝石公主号七月一日的船票

<table>
    <tr>
        <th colspan="2">值班人员</th>
        <th>星期一</th>
        <th>星期二</th>
        <th>星期三</th>
    </tr>
    <tr>
	<td>kongbai</td>
        <td>李强</td>
        <td>张明</td>
        <td>王平</td>
    </tr>
</table>

| 项目        | 价格   | 
| --------   | -----:  | 
| 计算机     | \$1600 |  
|            |   \$12   | 
| 管线        |    \$1    | 

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
