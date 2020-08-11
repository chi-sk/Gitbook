
[toc]



## 1. 二维数组中的查找
在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
```cpp
class Solution {
public:
	bool Find(int target, vector<vector<int> > array) {
        if(array.empty()) return false;
		int row = array.size()-1;
		int col = array[0].size()-1;
        for(int i=0,j=col;i<=row&&j>=0;)
        {
            if(array[i][j]>target)
                j--;
            else if(array[i][j]<target)
                i++;
            else return true;
        }
        return false;
	}
};

```	
## 2. 替换空格 
请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

```cpp
class Solution {
public:
	void replaceSpace(char *str,int length) {
 //       if(!str||length<=0) return;
        int space_count = 0;
        for(int i = 0;i<length;i++)
            if(str[i]==' ')
                space_count++;
        int new_length = length+2*space_count;
        str[new_length--] = '\0';
        for(int i = length-1;i>=0;i--)
        {
            if(str[i]!=' ')
                str[new_length--] = str[i];
            else{
                str[new_length--] = '0';
                str[new_length--] = '2';
                str[new_length--] = '%';
            }
        }
	}
};

```	
## 3. 从尾到头打印链表
```cpp
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> res;
        ListNode *pt = head;
        while(pt)
            res.push_back(pt->val),pt=pt->next;
        return vector<int>(res.rbegin(),res.rend());
    }
};
//递归实现
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> res;
        hp(head,res);
        return res;
    }
    void hp(ListNode *pt,vector<int> &res)
    {
        if(pt) hp(pt->next,res);
        else return ;
        res.push_back(pt->val);
    }
};

```	 
## 4. 重建二叉树 
 输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。
```cpp
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> vin) {
     if(pre.size()==0||vin.size()==0)return nullptr;
        return hp(pre,vin,0,pre.size()-1,0,vin.size()-1);
    }
    TreeNode* hp(vector<int>& pre,vector<int>& vin,int prestart,int preend,int instart,int inend)
    {
        if(preend - prestart!=inend - instart) return nullptr;
        TreeNode* node = new TreeNode(pre[prestart]);
        int i = 0,len = 0;
        for(i=instart;i<=inend;i++)
        {if(vin[i]==node->val) break;}
        if(i>inend) return nullptr;
        len = i-instart;
        if(i>instart) node->left = hp(pre,vin,prestart+1,prestart+1+len-1,instart,instart+len-1);else node->left = nullptr;
        if(i<inend) node->right = hp(pre,vin,prestart+1+len,preend,instart+len+1,inend); else node->right = nullptr;
        return node;
    }
};

```	
## 5. 用两个栈实现队列 
用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。
```cpp
class Solution
{
public:
    void push(int node) {
        stack1.push(node);
    }
    int pop() {
         
        if(stack2.empty())
        {
            while(!stack1.empty())
                stack2.push(stack1.top()),
                stack1.pop();
        }
            int value = stack2.top();
            stack2.pop();
            return value;
    }

private:
    stack<int> stack1;
    stack<int> stack2;
};

```	
## 6. 旋转数组的最小数字 
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。
例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。
NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。
```cpp
class Solution {
public:
    int minNumberInRotateArray(vector<int> rotateArray) {
        if(rotateArray.size()==0)return 0;
        return search2(rotateArray);
        
    }
    int search(vector<int> & arr)
    {
        int left = 0,right = arr.size()-1;
        int mid = left + (right - left)/2;
        if(arr[left]==arr[mid]&&arr[mid]==arr[right])
            return *min_element(arr.begin(),arr.end());
        while(left<=right)
        {
            mid = left + (right - left)/2;
            if(arr[mid]>arr[left]) left = mid;
            else if(arr[mid]<arr[right])right = mid;
            else return arr[right];
        }
 //       return arr[left];
    }
    int search2(vector<int> arr)
    {
        int left = 0,right = arr.size()-1;
        int mid = 0;
        while(left<right)
        {
            mid = left+(right-left)/2;
            if(arr[mid]<arr[right]) right = mid;
            else if(arr[mid] > arr[left]) left = mid+1;
            else left++;
        }
        return arr[left];
    }
};

```	
## 7. 斐波那契数列 
大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。

n<=39 
```cpp
class Solution {
public:
    int Fibonacci(int n) {
    int p = 0,q = 0,r = 1;
    for(int i = 0;i<n;i++)
        p = q,q = r,r = p+q;
    return q;
    }
};

```	
## 8. 跳台阶 
一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。
```cpp
class Solution {
public:
    int jumpFloor(int number) {
        int p = 0,q = 1,r = 1;
        for(int i = 0;i<number;i++)
            r = p+q,p = q,q = r;
        return r;
    }
};

```	
## 9. 变态跳台阶
一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。 
```cpp
class Solution {
public:
    int jumpFloorII(int number) {
    return pow(2,number-1);
    }
};

```	
## 10. 矩形覆盖 
 我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？

比如n=3时，2*3的矩形块有3种覆盖方法： 
```cpp
class Solution {
public:
    int rectCover(int number) {
        if(number<=0) return 0;
    int p = 0,q = 1,r = 1;
        for(int i = 1;i<number;i++)
            p = q,q = r,r = p+q;
        return r;
    }
};

```	
## 11. 二进制中1的个数 
输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

```cpp
class Solution {
public:
     int  NumberOf1(int n) {
         int count  = 0;
         while(n)
         {
             count++;
             n = n&(n-1);
         }
         return count;
     }
     int  solution_2(int n) {
         int count = 0;
         for(int i = 0;i<32;i++)
         {
             if(n&1==1)
                 count++;
             n>>=1;
         }
         return count;
     }
};

```	
## 12. 数值的整数次方 

给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

保证base和exponent不同时为0

```cpp
class Solution {
public:
    double Power(double base, int exponent) {
    double res = 1;
    unsigned int bit = 1;
    if(base==0) return 0;
    if(exponent==0) return 1;
    unsigned int un = exponent;
    if(exponent<0)
       un = -(exponent+1),un++,base = 1/base;
    while(un)
    {
        if(un&bit)
            res*=base;
        base*=base;
        un&=~bit;
        bit<<=1;
    }
    return res;
    }
};

```	
## 13. 调整数组顺序使奇数位于偶数前面 
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。
```cpp
```	
## 14. 链表中倒数第k个结点 
输入一个链表，输出该链表中倒数第k个结点。
```cpp


```	
## 15. 反转链表 
输入一个链表，反转链表后，输出新链表的表头。
```cpp


```	
## 16. 合并两个排序的链表 
输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。
```cpp


```	
## 17. 树的子结构 
输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）
```cpp


```	
## 18. 二叉树的镜像 
操作给定的二叉树，将其变换为源二叉树的镜像。
```cpp


```	
## 19. 顺时针打印矩阵 
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.
```cpp


```	
## 20. 包含min函数的栈
 定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。
注意：保证测试中不会当栈为空的时候，对栈调用pop()或者min()或者top()方法。 
```cpp


```	
## 21. 栈的压入、弹出序列 
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）
```cpp


```	
## 22. 从上往下打印二叉树 
从上往下打印出二叉树的每个节点，同层节点从左至右打印。
```cpp


```	
## 23. 二叉搜索树的后序遍历序列 
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。
```cpp


```	
## 24. 二叉树中和为某一值的路径 
输入一颗二叉树的根节点和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。(注意: 在返回值的list中，数组长度大的数组靠前)
```cpp


```	
## 25. 复杂链表的复制 
输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）
```cpp


```	
## 26. 二叉搜索树与双向链表 
输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。
```cpp


```	
## 27. 字符串的排列 
输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。
输入一个字符串,长度不超过9(可能有字符重复),字符只包括大小写字母。
```cpp


```	
## 28. 数组中出现次数超过一半的数字 
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。
```cpp


```	
## 29. 最小的K个数 
输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。
```cpp


```	
## 30. 连续子数组的最大和 
HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。给一个数组，返回它的最大连续子序列的和，你会不会被他忽悠住？(子向量的长度至少是1)
```cpp


```	
## 31. 整数中1出现的次数（从1到n整数中1出现的次数） 
求出1~13的整数中1出现的次数,并算出100~1300的整数中1出现的次数？为此他特别数了一下1~13中包含1的数字有1、10、11、12、13因此共出现6次,但是对于后面问题他就没辙了。ACMer希望你们帮帮他,并把问题更加普遍化,可以很快的求出任意非负整数区间中1出现的次数（从1 到 n 中1出现的次数）。
```cpp


```		
## 32. 把数组排成最小的数 
输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。
```cpp


```	
## 33. 丑数 
把只包含质因子2、3和5的数称作丑数（Ugly Number）。例如6、8都是丑数，但14不是，因为它包含质因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。
```cpp


```	
## 34. 第一个只出现一次的字符位置 
在一个字符串(0<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1（需要区分大小写）.
```cpp


```	
## 35. 数组中的逆序对 
在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007
```cpp


```	
## 36. 两个链表的第一个公共结点 
输入两个链表，找出它们的第一个公共结点。（注意因为传入数据是链表，所以错误测试数据的提示是用其他方式显示的，保证传入数据是正确的）
```cpp


```	
## 37. 数字在排序数组中出现的次数 
统计一个数字在排序数组中出现的次数。
```cpp


```	
## 38. 二叉树的深度 
输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。
```cpp


```	
## 39. 平衡二叉树 
输入一棵二叉树，判断该二叉树是否是平衡二叉树。
```cpp


```	
## 40. 数组中只出现一次的数字 
一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。
```cpp


```	
## 41. 和为S的连续正数序列 
小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!
要求输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序
```cpp


```	
## 42. 和为S的两个数字 
输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。
```cpp


```	
## 43. 左旋转字符串 
汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！
```cpp


```	
## 44. 翻转单词顺序列 
牛客最近来了一个新员工Fish，每天早晨总是会拿着一本英文杂志，写些句子在本子上。同事Cat对Fish写的内容颇感兴趣，有一天他向Fish借来翻看，但却读不懂它的意思。例如，“student. a am I”。后来才意识到，这家伙原来把句子单词的顺序翻转了，正确的句子应该是“I am a student.”。Cat对一一的翻转这些单词顺序可不在行，你能帮助他么？
```cpp


```	
## 45. 扑克牌顺子 
LL今天心情特别好,因为他去买了一副扑克牌,发现里面居然有2个大王,2个小王(一副牌原本是54张^_^)...他随机从中抽出了5张牌,想测测自己的手气,看看能不能抽到顺子,如果抽到的话,他决定去买体育彩票,嘿嘿！！“红心A,黑桃3,小王,大王,方片5”,“Oh My God!”不是顺子.....LL不高兴了,他想了想,决定大\小 王可以看成任何数字,并且A看作1,J为11,Q为12,K为13。上面的5张牌就可以变成“1,2,3,4,5”(大小王分别看作2和4),“So Lucky!”。LL决定去买体育彩票啦。 现在,要求你使用这幅牌模拟上面的过程,然后告诉我们LL的运气如何， 如果牌能组成顺子就输出true，否则就输出false。为了方便起见,你可以认为大小王是0。
```cpp


```	
## 46. 孩子们的游戏(圆圈中最后剩下的数) 

每年六一儿童节,牛客都会准备一些小礼物去看望孤儿院的小朋友,今年亦是如此。HF作为牛客的资深元老,自然也准备了一些小游戏。其中,有个游戏是这样的:首先,让小朋友们围成一个大圈。然后,他随机指定一个数m,让编号为0的小朋友开始报数。每次喊到m-1的那个小朋友要出列唱首歌,然后可以在礼品箱中任意的挑选礼物,并且不再回到圈中,从他的下一个小朋友开始,继续0...m-1报数....这样下去....直到剩下最后一个小朋友,可以不用表演,并且拿到牛客名贵的“名侦探柯南”典藏版(名额有限哦!!^_^)。请你试着想下,哪个小朋友会得到这份礼品呢？(注：小朋友的编号是从0到n-1)

如果没有小朋友，请返回-1

```cpp


```	
## 47. 求1+2+3+...+n 
求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。
```cpp


```	
## 48. 不用加减乘除做加法 
写一个函数，求两个整数之和，要求在函数体内不得使用+、-、*、/四则运算符号。
```cpp


```	
## 49. 把字符串转换成整数 
将一个字符串转换成一个整数，要求不能使用字符串转换整数的库函数。 数值为0或者字符串不是一个合法的数值则返回0
```cpp


```	
## 50. 数组中重复的数字 
在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。
```cpp


```	
## 51. 构建乘积数组 
给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。（注意：规定B[0] = A[1] * A[2] * ... * A[n-1]，B[n-1] = A[0] * A[1] * ... * A[n-2];）
```cpp


```	
## 52. 正则表达式匹配 
请实现一个函数用来匹配包括'.'和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（包含0次）。 在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但是与"aa.a"和"ab*a"均不匹配
```cpp


```	
## 53. 表示数值的字符串 
请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。
```cpp


```	
## 54. 字符流中第一个不重复的字符 
请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。
```cpp


```		
## 55. 链表中环的入口结点 
给一个链表，若其中包含环，请找出该链表的环的入口结点，否则，输出null。
```cpp


```	
## 56. 删除链表中重复的结点 
在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5
```cpp


```	
## 57. 二叉树的下一个结点 
给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。
```cpp


```	
## 58. 对称的二叉树 
请实现一个函数，用来判断一颗二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。
```cpp


```	
## 59. 按之字形顺序打印二叉树 
请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。
```cpp


```	
## 60. 把二叉树打印成多行 
从上到下按层打印二叉树，同一层结点从左至右输出。每一层输出一行。
```cpp


```	
## 61. 序列化二叉树 
 请实现两个函数，分别用来序列化和反序列化二叉树

二叉树的序列化是指：把一棵二叉树按照某种遍历方式的结果以某种格式保存为字符串，从而使得内存中建立起来的二叉树可以持久保存。序列化可以基于先序、中序、后序、层序的二叉树遍历方式来进行修改，序列化的结果是一个字符串，序列化时通过 某种符号表示空节点（#），以 ！ 表示一个结点值的结束（value!）。

二叉树的反序列化是指：根据某种遍历顺序得到的序列化字符串结果str，重构二叉树。
```cpp


```	
## 62. 二叉搜索树的第k个结点 
给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4。
```cpp


```	
## 63. 数据流中的中位数 
如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。我们使用Insert()方法读取数据流，使用GetMedian()方法获取当前读取数据的中位数。
```cpp


```	
## 64. 滑动窗口的最大值 
给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。例如，如果输入数组{2,3,4,2,6,2,5,1}及滑动窗口的大小3，那么一共存在6个滑动窗口，他们的最大值分别为{4,4,6,6,6,5}； 针对数组{2,3,4,2,6,2,5,1}的滑动窗口有以下6个： {[2,3,4],2,6,2,5,1}， {2,[3,4,2],6,2,5,1}， {2,3,[4,2,6],2,5,1}， {2,3,4,[2,6,2],5,1}， {2,3,4,2,[6,2,5],1}， {2,3,4,2,6,[2,5,1]}。
```cpp


```	
## 65. 矩阵中的路径 
请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则该路径不能再进入该格子。 例如:​  矩阵中包含一条字符串"bcced"的路径，但是矩阵中不包含"abcb"路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。
```
⎡​  a b c e  ⎤​
|  s f c s |
⎣  a d e e ⎦
```

```cpp


```	
## 66. 机器人的运动范围 
地上有一个m行和n列的方格。一个机器人从坐标0,0的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于k的格子。 例如，当k为18时，机器人能够进入方格（35,37），因为3+5+3+7 = 18。但是，它不能进入方格（35,38），因为3+5+3+8 = 19。请问该机器人能够达到多少个格子？
```cpp
class Solution {
public:
    int movingCount(int threshold, int rows, int cols)
    {
        if(rows<0||cols<0)return 0;
        vector<vector<bool>> Fmatrix(rows,vector<bool>(cols,false));
        return hp(Fmatrix,threshold,0,0);
    }
    int hp(vector<vector<bool>> &Fmat,int k,int rows,int cols)
    {
        if(rows<0||rows>=Fmat.size()||cols<0||cols>=Fmat[0].size()) return 0;
        int res = 0;
        if(!Fmat[rows][cols])
        {
            Fmat[rows][cols] = true;
            if(GetDigitSum(cols,rows)>k) return 0;
            else res++;
            res = res+hp(Fmat,k,rows-1,cols)+hp(Fmat,k,rows+1,cols)+hp(Fmat,k,rows,cols-1)+hp(Fmat,k,rows,cols+1);
             return res;
        }
        return 0;
    }
    int GetDigitSum(int rows,int cols)
    {
        int sum = 0;
        while(rows)
            sum+=rows%10,rows/=10;
        while(cols)
            sum+=cols%10,cols/=10;
        return sum;
    }
};

```	
## 67. 剪绳子 
给你一根长度为n的绳子，请把绳子剪成整数长的m段（m、n都是整数，n>1并且m>1），每段绳子的长度记为k[0],k[1],...,k[m]。请问k[0]xk[1]x...xk[m]可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。
```cpp
class Solution {
public:
    int cutRope(int number) {
        int res = 1;
        while(number>=5)
        {
            number-=3;
            res*=3;
        }
        if(number==4)
            return res*4;
        if(number==3)
            return res==1?2:res*3;
        if(number==2)
            return res==1?1:res*2;
    }
};

```	
优化:
```cpp
class Solution {
public:
    int cutRope(int number) {
        int res = 1;
        if(number>0&&number<4)
            return number-1;
        while(number>4)
        {
            number-=3;
            res*=3;
        }
        return number*res;
    }
};
```