# 1. 比赛规则
![[Pasted image 20240305222223.png]]![[Pasted image 20240305222253.png]]
http://cspro.org

考试内容主要覆盖大学计算机专业所学习的程序设计、数据结构以及算法，以及相关的数学基础知识。包括但不限于：

(1)程序设计基础

逻辑与数学运算，分支循环，过程调用(递归)，字符串操作，文件操作等。

(2)数据结构

线性表（数组、队列、栈、链表）、树（堆、排序二叉树）、哈希表、集合与映射、图。

(3)算法与算法设计策略

排序与查找，枚举，贪心策略，分治策略，递推与递归，动态规划，搜索，图论算法，计算几何，字符串算法、线段树、随机算法，近似算法等。

Dev-CPP或Eclipse
![[Pasted image 20240305222637.png]]
![[Pasted image 20240305222756.png]]
# 2. 笔记
## rw. 输入输出处理
## d. define
## s. 字符串处理
### \<string>
#### 大小和容量
str.length()
#### 读数据
getline(cin, str)，读取直到遇到'\\n'
#### 将一整行字符串分割
```c++
#include<sstream>
/**/
string line;
getline(cin,line);
istringstream iss(line);
while (iss>>word){
	cout<<word<<endl;
}
```

#### erase()
`erase()`函数用于删除字符串中的一部分或特定字符。它有几种重载形式，常用的有：

- `erase(size_t pos, size_t len)`: 从位置`pos`开始删除`len`个字符。如果`len`是`std::string::npos`，则删除到字符串末尾。
- `erase(iterator position)`: 删除位于`position`迭代器位置的字符。
- `erase(iterator first, iterator last)`: 删除从`first`到`last`（不包括`last`）范围内的所有字符。
- ### `remove()`
`std::remove()`算法属于`<algorithm>`头文件，它将不需要的元素移动到容器的末尾，并返回一个指向新逻辑末尾的迭代器。然后，可以使用`erase()`来删除这些元素。
```cpp
isbn.erase(std::remove(isbn.begin(), isbn.end(), '-'), isbn.end());
```
#### insert()

`insert()`函数用于在字符串的指定位置插入字符或另一个字符串。它也有多种重载形式，常用的有：

- `insert(size_t pos, const std::string& str)`: 在位置`pos`插入字符串`str`。
- `insert(size_t pos, const std::string& str, size_t subpos, size_t sublen)`: 在位置`pos`插入字符串`str`的一个子串，子串从`subpos`开始，长度为`sublen`。
- `insert(size_t pos, const char* s)`: 在位置`pos`插入C风格字符串`s`。
- `insert(iterator p, char c)`: 在迭代器`p`指定的位置插入字符`c`。
#### substr()

### \<cstring>
## t. STL使用
### \<map>
#### find()
`if (myMap.find(key)!=myMap.end()) {//键存在}` 迭代器返回位置
`if (myMap.count(key) > 0) {//键存在}` count返回0表示不存在，1表示存在
### \<set>
#### 元素处理
s.find()，寻找是否在set中，如果不在，返回s.end()迭代器，否则返回对应位置迭代器
s.insert(el)
s.erase(el)
#### 容量和大小
s.size()
s.clear()
s.empty()
### \<vector>
#### 访问
vec.at(index)，带边界检查
vec\[index]，不带边界检查
vec.front()，访问第一个元素
vec.back()，访问最后一个元素
#### 修改
vec.push_back(el)，添加元素到末尾
vec.pop_back(el)，从末尾弹出
vec.insert(vec.begin()+index, el)，在index+1个位置插入元素el
vec.erase(vec.begin()+index)，在index+1个位置删除元素
vec.clear()，清空
大小和容量
vec.empty()
vec.size()
vec.resize()，新元素会初始化
vec.capacity()，容量
vec.shrink_to_fit()，移除多余未使用的容量



