# STL1：数据结构|容器

### 第一部分 顺序容器概述

容器是一些特定类型对象的集合，**顺序容器(sequential container)** 中数据结构的元素位置与元素加入时的位置对应而不依赖于元素的值。有以下的类型：

> **array 数组：** 固定大小，支持快速随机访问，不能改变大小。
>
> **vector 向量：最常用** 可变大小，支持快速随机访问，在尾部之外的位置插入删除元素可能很慢。
>
> **string 字符串：** 与vector相似，但专门用于保存字符。
>
> **deque 双端队列：** 支持快速随机访问，在头尾位置插入/删除速度很快。
>
> **list 双向链表：** 支持双向顺序访问，在任何位置都能很快插入/删除数据。
>
> **forward_list 单向链表：** 支持单向顺序访问，在任何位置都能很快插入/删除数据。迭代器不支持--操作。
>
>> **set 集合：** 非顺序容器
>>
>> **map 哈希表：** 非顺序容器
>>

通常容器在其同名的头文件中。使用容器时需要`<类型>`​来标明容器的元素类型。  
容器甚至可以保存自身的类型`vector<vector<int> >`​

> 类型别名：
>
>> iterator 迭代器类型
>>
>> const_iterator 只读迭代器类型
>>
>> size_type 表示容器大小的无符号整数类型
>>
>> difference_type 保存两个迭代器之间距离的有符号整数类型
>>
>> value_type 元素的类型
>>
>> reference 元素的左值类型(等价于value_type&)
>>
>> const_reference 元素的const左值类型
>>
>
> 构造函数(构造器)
>
>> C c; 默认构造器
>>
>> C c1(c2); 构造c2的拷贝c1
>>
>> C c(b,e); 将迭代器b和e指定的范围内的元素拷贝到c中(array不支持)
>>
>> C c{a,b,c...}; 列表初始化
>>
>
> 赋值与交换
>
>> c1 = c2; c1 = {a,b,c...} 赋值
>>
>> a.swap(b); 交换元素，等价于 swap(a,b);
>>
>
> 大小
>
>> c.size() 元素数目(forward_list不支持)
>>
>> c.max_size() c可保存的最大元素数目
>>
>> c.empty 判断c中是否有元素
>>
>
> 添加与删除(array不适用)
>
>> c.insert(args) 把args中的元素拷贝进c
>>
>> c.emplace(inits) 使用inits构造c中的一个元素
>>
>> c.erase(args) 删除args指定的元素
>>
>> c.clear() 删除c中所有的元素，返回void
>>
>
> 关系运算符
>
>> 所有容器都支持 == !=
>>
>> 关系运算符< <= > >= (无序关联容器不支持)
>>
>
> 获取迭代器
>
>> c.begin() 返回指向c的首元素的迭代器
>>
>> c.end() 返回指向c的尾元素的后一个位置的迭代器
>>
>> c.cbegin() 与 c.cend() 返回const_iterator
>>
>
> 反向迭代器(不支持forward_list)
>
>> reverse_iterator 逆序寻址元素的迭代器
>>
>> const_reverse_iterator 只读逆序寻址元素的迭代器
>>
>> c.rbegin() 返回指向c的尾元素的迭代器
>>
>> c.rend() 返回指向c的首元素的前一个位置的迭代器
>>
>> c.crbegin() 与 c.crend() 返回const_reverse_iterator
>>

### 第二部分 顺序容器操作

​![image](assets/image-20241002174601-jq8p3al.png)​

​![image](assets/image-20241002174652-j1ah70m.png)​

​![image](assets/image-20241002174711-lob6obt.png)​

​![image](assets/image-20241002174727-nv6q1te.png)​

​![image](assets/image-20241002174750-xwvm2vh.png)​

​![image](assets/image-20241002174823-mmzunm7.png)​

### 第一部分 String类型

​![image](assets/image-20241002174855-utonr85.png)​

​![image](assets/image-20241002174916-17oksyy.png)​

​![image](assets/image-20241002174928-q7h9vs8.png)​

​![image](assets/image-20241002174943-ri5adga.png)​

​![image](assets/image-20241002174953-h6hsm79.png)​

​![image](assets/image-20241002175007-0l79n35.png)​

​![image](assets/image-20241002175018-3f66ahp.png)​

​`#include <string>`​ `using std::string;`​

一种特殊初始化`string mystring(5, 'x');`​ 等效于`string mystring = "xxxxx";`​

​`string s2(s1);`​ 等效于`string s2 = s1;`​

使用`=`​号是时拷贝初始化(copy initialization)，不使用时是直接初始化(direct initialization)  

string的操作：  
​`os<<s`​ 将s写到输出流os中，返回os  
​`is>>s`​ 从is读取字符串赋给s，默认以空白分隔，返回is（读取时会先跳过开头的空白）  
​`getline(is,s)`​ 从is中读取一行赋给s，返回is（读入空白，读入换行符但是不存到string里）  
​`s.empty()`​ 判断s是否为空  
​`s.size()`​ 返回s中字符的个数，返回的不是`int`​或`unsigned int`​，而是`string::size_type`​类型，  
其保证了可以存下任何大小的`string`​类型的大小。  
​`s[n]`​ 返回s中第n个字符的引用  
​`s1+s2`​ 返回s1和s2连接后的结果，甚至可以使用`+=`​  
注意不能`+`​两个字面值，即`+`​两侧需要至少有一个`string`​  
​`string s3 = "x" + "y" + s1;`​错误  
​`string s4 = s1 + s2 + "x";`​正确

`== != > >= <=`​ 利用字典序进行比较和判断（注意`"abc" < "abcde"`​）

输入流作为条件语句时，流有效就为`true`​（没遇到非法输入或文件结尾）

cctype头文件中的函数（C中的xxx.h文件被更新为了cxxx）  

```java
isalnum(c) //字母或数字
isalpha(c) //字母
iscntrl(c) //控制字符
isdigit(c) //数字
isgraph(c) //不是空格，可以打印
islower(c) //小写字母
isprint(c) //可打印（空格或具有可视形式）
ispunct(c) //标点符号（即不是控制字符/数字/字母/可打印空白）
isspace(c) //空白（空格/横制表/纵制表/回车/换行/进纸）
isupper(c) //大写字母
isxdigit(c) //十六进制数字
tolower(c) //输出小写字母
toupper(c) //输出大写字母
```

​`for(auto c : str){cout << c << ecd1;}`​ 竖着输出str字符串

​`for(auto &c : s){c = toupper(c);}`​ 把s字符串转为全大写

### 第二部分 Vector类模板

​`#include <vector>`​ `using std::vector;`​

C++有类模板(class template)和函数模板，模板是为编译器生成类或者函数编写的一份说明，  
编译器根据模版创建类或函数的过程称为实例化(instantiation)

需要提供额外信息来指定模板实例化成什么样的类。`vector<int> ivec;`​

​`vector<int> aivec{3,4,5};`​ 向量(3,4,5)  
​`vector<int> bivec(5);`​ 向量(0,0,0,0,0)  
​`vector<int> civec(2,8);`​ 向量(8,8)  
​`vector<int> divec(aivec);`​ 拷贝另一个向量

用`ivec.push_back(i);`​ 来在向量尾部压入一个新数值

​`v.empty();`​ 判断是否为空  
​`v.size();`​ 元素个数，返回值vector<类型>::size_type  
​`v[n]`​ 返回v中第n个位置上元素的引用  
​`== != < <= > >=`​ 按字典序进行比较操作

### 第三部分 迭代器(iterator)

迭代器类似于指针，提供了对对象的间接访问。

​`v.begin()`​是第一个元素的迭代器，`v.end()`​是最后一个元素再往后一个的迭代器

​`*iter`​ 返回迭代器iter所指元素的引用  
​`iter->mem`​ 获取指向的元素的成员，等价于`(*iter).mem`​  
​`++iter --iter`​ 指向下一个/上一个元素  
​`== != > >= < <= + - * /`​都能操作

类型名`vector<int>::iterator`​ `string::iterator`​

### 第四部分 数组

数组与vector不同在于数组不能随便改变大小。

​`int a[3] = {1,2,3};`​

数组下标使用`size_t`​类型。

​`begin(a)`​函数返回指向首元素的指针，`end(a)`​函数返回指向尾元素的下一位置的指针。

多维数组`int b[3][3] = {{1,2,3},{0,0,0}};`​

### 第几部分 容器适配器

​![image](assets/image-20241002175152-pukov6u.png)​

​![image](assets/image-20241002175201-4kskcb0.png)​

​![image](assets/image-20241002175211-u2s3opk.png)​

​![image](assets/image-20241002175219-vps5mat.png)​

​![image](assets/image-20241002175227-zagjk1r.png)​
