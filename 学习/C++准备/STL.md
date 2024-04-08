# 常用STL容器基本说明与常见用法
## 基本数学函数

- **绝对值**:
    
    - `abs(x)`：计算整数的绝对值。
    - `fabs(x)`：计算浮点数的绝对值。
- **三角函数**:
    
    - `sin(x)`：计算x（弧度）的正弦。
    - `cos(x)`：计算x（弧度）的余弦。
    - `tan(x)`：计算x（弧度）的正切。
- **反三角函数**:
    
    - `asin(x)`：计算x的反正弦值，返回值为弧度。
    - `acos(x)`：计算x的反余弦值，返回值为弧度。
    - `atan(x)`：计算x的反正切值，返回值为弧度。
- **指数和对数函数**:
    
    - `exp(x)`：计算e的x次幂。
    - `log(x)`：计算x的自然对数（以e为底）。
    - `log10(x)`：计算x的常用对数（以10为底）。
- **幂函数和平方根**:
    
    - `pow(x, y)`：计算x的y次幂。
    - `sqrt(x)`：计算x的平方根。
- **四舍五入和取整**:
    
    - `ceil(x)`：向上取整，返回不小于x的最小整数。
    - `floor(x)`：向下取整，返回不大于x的最大整数。
    - `round(x)`：四舍五入到最接近的整数。
## string
`std::string`是C++标准库中用于处理文本字符串的类。它封装了char数组的操作，提供了丰富的成员函数来进行字符串的创建、访问、修改、搜索、比较和转换等操作。

## vector
`std::vector`是一个封装了动态大小数组的顺序容器。它能够存储任意类型的对象，从简单的内置类型到复杂的对象。

## map
`std::map`是一个关联容器，包含键值对，其中每个键唯一，并且按照特定顺序排序。它提供了基于键的快速查找能力。

## set
`std::set`是一个关联容器，包含一个键的集合，其中每个键唯一，并且自动排序。它主要用于快速查找、插入和删除。

## pair
`std::pair`是一个结构体，可以存储两个值，这两个值可以是不同的类型。`pair`常用于将两个值作为一个单元返回或传递。

## unordered_map
`std::unordered_map`是一个关联容器，包含键值对，其中每个键唯一。它使用哈希表实现，因此提供了平均常数时间复杂度的查找、插入和删除操作。

## unordered_set
`std::unordered_set`是一个关联容器，包含一个键的集合，其中每个键唯一。它使用哈希表实现，提供了快速的查找、插入和删除。

## stack
`std::stack`是一个容器适配器，提供后进先出(LIFO)的数据结构。它只允许在栈顶进行添加或移除元素的操作。

## queue
`std::queue`是一个容器适配器，提供先进先出(FIFO)的数据结构。它只允许在队列的末尾添加元素，在队列的开头移除元素。

## deque
`std::deque`是一个双端队列容器，允许在容器的前端和后端快速插入和删除。

## priority_queue
`std::priority_queue`是一个容器适配器，提供优先队列的功能。它允许插入元素，并且能够以排序的顺序从队列中取出元素。

# 常用接口及使用方法

# `std::string`的更多函数和接口解释

## 修改和更新字符串
- `replace(pos, len, str)`: 从`pos`位置开始，替换`len`长度的字符为字符串`str`。
- `substr(pos, len)`: 返回从`pos`位置开始，长度为`len`的子字符串。
- `push_back(ch)`: 在字符串末尾添加字符`ch`。
- `pop_back()`: 删除字符串末尾的字符。

## 字符和字符串的插入与删除
- `insert(pos, str)`: 在`pos`位置插入字符串`str`。
- `erase(pos, len)`: 从`pos`位置开始删除`len`长度的字符。

## 字符串比较
- `compare(str)`: 比较当前字符串和`str`。如果当前字符串小于、等于、大于`str`，则返回负数、0、正数。

## 字符访问
- `operator[](pos)`: 访问位于`pos`位置的字符。
- `at(pos)`: 访问位于`pos`位置的字符，如果`pos`超出范围，抛出`std::out_of_range`异常。

## 字符串搜索
- `rfind(str, pos)`: 从`pos`位置开始，反向查找字符串`str`第一次出现的位置。
- `find_first_of(str, pos)`: 从`pos`位置开始，查找在字符串`str`中任一字符第一次出现的位置。
- `find_last_of(str, pos)`: 从`pos`位置开始，反向查找在字符串`str`中任一字符最后一次出现的位置。
- `find_first_not_of(str, pos)`: 从`pos`位置开始，查找第一个不在字符串`str`中的字符。
- `find_last_not_of(str, pos)`: 从`pos`位置开始，反向查找最后一个不在字符串`str`中的字符。

## 字符串转换
- `stoi(str)`, `stol(str)`, `stoll(str)`: 将字符串`str`转换为整数类型（分别为`int`, `long`, `long long`）。
- `stof(str)`, `stod(str)`, `stold(str)`: 将字符串`str`转换为浮点数类型（分别为`float`, `double`, `long double`）。

## 字符串流
- `std::stringstream`, `std::istringstream`, `std::ostringstream`: 这些类提供了字符串和其他数据类型之间的转换功能。通过使用这些字符串流，可以方便地读取或写入字符串中的数据。

## 字符串编码转换
C++标准库本身不直接提供字符串编码转换的功能。但是，可以使用第三方库如`iconv`或C++17引入的`std::wstring_convert`来进行编码转换，例如从UTF-8转换到UTF-16。

## 字符串的迭代
- `begin()`, `end()`: 返回指向字符串第一个字符和末尾字符后一位置的迭代器。
- `rbegin()`, `rend()`: 返回指向字符串最后一个字符和开头字符前一位置的反向迭代器。

## 字符串的容量和大小
- `size()`, `length()`: 返回字符串的长度。
- `capacity()`: 返回在重新分配之前字符串可以容纳的最大字符数。
- `resize(n)`: 调整字符串的长度为`n`，如果`n`小于当前长度，多余的字符被删除；如果`n`大于当前长度，会添加相应数量的字符。
- `shrink_to_fit()`: 请求移除未使用的容量，减少内存使用。

## 字符串和数字之间的转换
除了前面提到的`stoi`、`stol`等函数外，C++11还提供了`to_string`函数，可以将数值转换为字符串。

```cpp
std::string str = std::to_string(12345); // 将整数转换为字符串
```

## 字符串的比较和排序
`std::string`提供了多种比较操作符（`==`, `!=`, `<`, `>`, `<=`, `>=`），可以直接用于字符串的比较。此外，`std::lexicographical_compare`函数可以用于比较两个序列（包括字符串）的字典序。

## 字符串字面量
C++11引入了原始字符串字面量（Raw String Literal），使得编写包含多个转义字符的字符串变得更加简单。

```cpp
std::string path = R"(C:\Program Files\Example)"; // 使用原始字符串字面量
```

这些是`std::string`类提供的一些主要功能和接口。C++标准库中的字符串处理功能非常强大，通过熟练使用这些功能，可以有效地处理各种字符串相关的问题。
在C++中，读入字符串可以通过多种方式实现，主要依赖于`<iostream>`, `<sstream>`, 和 `<string>` 库。以下是一些常用的方法：

### 使用`<iostream>`库

直接使用`cin`来读取字符串。这种方法适用于读取不包含空格的单个单词。

```cpp
#include <iostream>
using namespace std;

int main() {
    string str;
    cin >> str;
    cout << str << endl;
    return 0;
}
```

### 使用`getline()`函数读取一整行

当需要读取包含空格的一整行文本时，可以使用`getline()`函数。

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str;
    getline(cin, str);
    cout << str << endl;
    return 0;
}
```

### 使用`<sstream>`库解析字符串

当你需要从一个字符串中提取并解析多个值时，`<sstream>`库提供的`stringstream`类非常有用。

```cpp
#include <iostream>
#include <sstream>
#include <string>
using namespace std;

int main() {
    string line = "123 456 789";
    stringstream ss(line);
    int number;
    while (ss >> number) {
        cout << number << endl;
    }
    return 0;
}
```

这些方法是C++中读入和处理字符串的基础，可以根据具体需求选择合适的方法。
# vector
- `push_back()`: 在末尾添加一个元素。
- `pop_back()`: 删除末尾元素。
- `size()`: 返回容器中的元素数。
- `empty()`: 检查容器是否为空。

# map
- `insert()`: 插入键值对。
- `erase()`: 根据键删除元素。
- `find()`: 查找键对应的迭代器。
- `size()`: 返回容器中的元素数。

# set
- `insert()`: 插入元素。
- `erase()`: 删除元素。
- `find()`: 查找元素的迭代器。
- `size()`: 返回容器中的元素数。

# pair
- `first`, `second`: 访问pair的第一个和第二个元素。
- 在C++中，`pair`是一个非常实用的容器，它可以存储一对值，这两个值可以是相同类型或不同类型。`pair`定义在`<utility>`头文件中。以下是`pair`的一些常用使用方法：

### 创建和初始化

```cpp
#include <utility> // 包含pair
#include <string>
#include <iostream>

int main() {
    // 直接初始化
    std::pair<int, std::string> p1(1, "Apple");

    // 使用make_pair函数
    auto p2 = std::make_pair(2, "Banana");

    // C++11及以后版本的列表初始化
    std::pair<int, std::string> p3 = {3, "Cherry"};

    std::cout << p1.second << std::endl; // 输出: Apple
    std::cout << p2.second << std::endl; // 输出: Banana
    std::cout << p3.second << std::endl; // 输出: Cherry

    return 0;
}
```

### 访问元素

`pair`的两个元素可以通过`.first`和`.second`成员访问。

```cpp
std::cout << p1.first << ", " << p1.second << std::endl; // 输出: 1, Apple
```

### 比较操作

`pair`支持比较操作（==, !=, <, <=, >, >=）。比较是首先基于`.first`元素进行的，如果`.first`相等，则基于`.second`元素。

```cpp
if (p1 < p2) {
    std::cout << "p1 is less than p2" << std::endl;
}
```

### 用作容器的元素

`pair`经常用作标准容器（如`std::map`和`std::set`）的元素类型。

```cpp
#include <map>

std::map<int, std::string> m;
m.insert(std::make_pair(1, "One"));
m[2] = "Two";
```

这些是`pair`在C++中的一些常用使用方法。`pair`因其简单和灵活性，在实际编程中被广泛使用，尤其是在需要将两个相关联的数据作为一个单元处理时。

# unordered_map
- `insert()`: 插入键值对。
- `erase()`: 根据键删除元素。
- `find()`: 查找键对应的迭代器。
- `size()`: 返回容器中的元素数。

# unordered_set
- `insert()`: 插入元素。
- `erase()`: 删除元素。
- `find()`: 查找元素的迭代器。
- `size()`: 返回容器中的元素数。

# stack
- `push()`: 在栈顶添加元素。
- `pop()`: 移除栈顶元素。
- `top()`: 访问栈顶元素。
- `empty()`: 检查栈是否为空。

# queue
- `push()`: 在队列末尾添加元素。
- `pop()`: 移除队列开头的元素。
- `front()`, `back()`: 访问队列的第一个和最后一个元素。
- `empty()`: 检查队列是否为空。

# deque
- `push_back()`, `push_front()`: 在末尾/开头添加元素。
- `pop_back()`, `pop_front()`: 删除末尾/开头元素。
- `size()`: 返回容器中的元素数。
- `empty()`: 检查容器是否为空。

# `std::priority_queue`的更多接口及自定义比较方法

`std::priority_queue`是C++标准模板库(STL)中的一个容器适配器，它提供了一组特定的接口，用于管理一个满足堆属性的底层容器。默认情况下，`std::priority_queue`实现了一个大根堆。

## 主要接口

- `empty()`: 检查优先队列是否为空。
- `size()`: 返回优先队列中的元素数量。
- `top()`: 访问优先队列顶部的元素。
- `push(const value_type& val)`: 向优先队列中插入一个元素。
- `pop()`: 移除优先队列顶部的元素。
- `emplace(Args&&... args)`: 直接在优先队列中构造一个元素，避免复制或移动操作。

## 自定义比较方法

要自定义`std::priority_queue`的比较方法，以实现大根堆或小根堆，可以在声明`priority_queue`时指定比较函数。

### 小根堆

使用`std::greater<T>`作为比较函数，可以实现小根堆。

```cpp
#include <queue>
#include <vector>
#include <functional>

std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;
```

### 大根堆

虽然`std::priority_queue`默认就是大根堆，但如果需要明确指定比较函数，可以使用`std::less<T>`。

```cpp
#include <queue>
#include <vector>
#include <functional>

std::priority_queue<int, std::vector<int>, std::less<int>> maxHeap;
```

### 自定义比较类型

如果需要对自定义类型的对象进行排序，可以定义一个比较类或比较函数。

```cpp
struct MyCompare {
    bool operator()(int a, int b) {
        return a > b; // 小根堆
        // return a < b; // 大根堆
    }
};

std::priority_queue<int, std::vector<int>, MyCompare> customHeap;
```

通过这种方式，可以灵活地定义优先队列的行为，满足不同的需求。



在C++中，常用的排序函数主要是`std::sort`，它定义在`<algorithm>`头文件中。`std::sort`函数非常灵活，支持对数组和STL容器（如`std::vector`, `std::deque`等）中的元素进行排序。此外，它允许通过重载比较函数来自定义排序规则。

### 基本用法

对于基本数据类型数组或STL容器，可以直接使用`std::sort`进行默认的升序排序。

```cpp
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> vec = {4, 1, 3, 5, 2};
    std::sort(vec.begin(), vec.end());
}
```

### 自定义比较函数

`std::sort`允许通过第三个参数传递自定义的比较函数或函数对象，以实现自定义排序规则。

```cpp
#include <algorithm>
#include <vector>

bool compare(int a, int b) {
    return a > b; // 降序排序
}

int main() {
    std::vector<int> vec = {4, 1, 3, 5, 2};
    std::sort(vec.begin(), vec.end(), compare);
}
```

或者使用lambda表达式进行更简洁的定义：

```cpp
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> vec = {4, 1, 3, 5, 2};
    std::sort(vec.begin(), vec.end(), [](int a, int b) {
        return a > b; // 降序排序
    });
}
```

### 对STL容器的支持

`std::sort`函数支持任何提供随机访问迭代器的容器，如`std::vector`, `std::deque`。但是，它不适用于`std::list`或`std::forward_list`，因为这些容器不支持随机访问迭代器。对于`std::list`，应使用成员函数`list::sort`进行排序。

### 稳定排序

如果需要保持等值元素的相对顺序，可以使用`std::stable_sort`，它的用法与`std::sort`相同，但通常速度稍慢，因为它保证了排序的稳定性。

```cpp
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> vec = {4, 1, 3, 5, 2};
    std::stable_sort(vec.begin(), vec.end());
}
```

这些是C++中常用的排序函数及其重载和对STL容器支持的排序方法。

```cpp
class CompareMyClass {
public:
    bool operator()(const MyClass& a, const MyClass& b) const {
        return a.value < b.value;
    }
};
```