# CPP基础2：数据类型

### 第一部分

> 算数类型(arithmetic type)
>
>> 整型(integral type) 包括字符和布尔类型在内
>>
>> 浮点型
>>
>
> 空类型(void)

|类型|中文名|最小长度||类型|中文名|最小长度||类型|中文名|最小长度|
| ----------| -------------| ----------| --| ----------| -------------| ----------| --| -------------| ----------| ----------|
|bool|布尔类型|未定义||char|字符|8 bit||wchar_t|宽字符|16 bit|
|char16_t|Unicode字符|16 bit||char32_t|Unicode字符|32 bit||short|短整型|16 bit|
|int|整型|16 bit||long|长整型|32 bit||long long|长整型|64 bit|
|float|单精度|6位尾数||double|双精度|10位尾数||long double|扩展精度|10位尾数|

整型(除去布尔型与扩展字符型)分为带符号的(signed)和无符号的(unsigned)

大多数类型支持转换(convert)

字面值常量(literal)可以写作八进制(0前缀)，十六进制(0X/0x前缀)

字符前缀：u(char16_t) U(char32_t) L(wchar_t) u8(UTF-8)  
整型前缀：U(unsigned) L(long) LL(long long)  
浮点前缀：F(float) L(long double)

不能直接使用：  
不可打印(nonprintable)字符：退格等没有可视图符的控制字符。  
特殊含义字符：使用转义序列(escape sequence)

|说明|转义||说明|转义||说明|转义||说明|转义|
| -----------| ------| --| ----------| -------------| --| --------| -------------| --| --------| -------------|
|换行|\n||退格|\b||回车|\r||进纸|\f|
|横向制表|\t||纵向制表|\v||单引号|\\'||双引号|\\\"|
|报警/响铃|\a||问号|\\\?||反斜线|\\\\||||

区分初始化与赋值：使用{value}而不是=value来初始化，  
这称为列表初始化(list initialization)，这样当初始化可能丢失信息时会报错。

​`int i{0};`​ 代替 `int i = 0;`​

默认初始化(default initialized)：函数体之外的变量初始化为0，函数体内部的变量不被初始化(uninitialized)，  
其值是未定义的(undefined)

C++支持分离式编程(separate compilation)机制，把程序分为多个文件。  
声明(declaration)规定变量的类型与名字，可用`extern int i;`​表示  
定义(definition)还申请存储空间并初始化，  
变量只能被定义一次，但是可以被多次声明。

C++是一种静态类型(statically typed)语言，在编译阶段进行类型检查(type checking)

标识符(变量名)(identifier)由字母、数字、下划线组成，以字母或下划线开头  
自定义标识符不能：连续出现两个下划线`a__aa`​，下划线紧连大写字母开头`_Add`​  
定义在函数体外的标识符不能：以下划线开头`_i`​

变量名一般小写开头，类名一般大写开头，宏定义一般全部大写

作用域(scope)分为全局作用域(global scope)和块作用域(block scope)  
在内层作用域(inner scope)定义的新名字会覆盖外层定义域(outer scope)的名字。

const修饰符表示不可变常量，必须初始化。  
const类型默认只在一个文件中使用

想要让一个const在多个文件中传递，需要在声明与定义时都用`extern const`​

const的引用与指针也需要是const来保证不变性。

顶层const(top-level const)表示指针本身就是常量  
底层const(low-level const)表示指针指向的对象是一个常量。

### 复合类型：引用与指针

复合类型(compound type)是基于其他类型定义的类型，如引用和指针。

引用(reference)(指左值引用(lvalue reference)) `&变量名`​

​`int &rei = i;`​ 引用必须被初始化，相当于为已有变量起一个新名字。

指针(pointer)

​`int *pi = &i;`​ 使用取地址符`&`​获取对象的地址。

​`int *pi_ = pi`​ 将一个指针赋值给另一个指针

​`*pi == i`​ 使用解引用符`*`​来使用指针指向的对象。

定义时的`*`​标明是指针类型，使用时的`*`​进行解引用。

指针的类型需要与其指向的对象类型严格匹配。

生成空指针，其不指向任何对象：`int *p1 = nullptr;`​

指针能直接放在条件表达式里，非空指针(非0)都会返回`true`​，空指针返回`false`​

​`void*`​指针可以指向任何对象，但由于不知道对象的具体类型，  
无法用这个指针对对象进行算数操作等。

可以继续定义指针的指针类型`**`​等

定义类型别名的方法：  
1）使用`typedef double a, *b;`​ 这样a是double的同义词，b是double*的同义词。  
2）使用别名声明`using newint = int;`​ 这样newint是int的同义词。

使用`auto k = i + j;`​让编译器自动判断表达式的结果是什么类型。

把函数的返回值类型作为变量的类型`decltype(function()) sum = x + y;`​

把其他变量的类型作为变量的类型`decltype(i) j = i_;`​

自定义结构体 `struct 类名 { 类体 };`​

预处理器(preprocessor)在编译之前执行：

​`#include <xxx.h>`​用指定的头文件的内容替换`#include`​语句

头文件保护符(header guard)：  
​`#define xxx`​ 把一个名字设定为预处理变量  
​`#ifdef xxx`​ 当 预处理变量 已定义时为`true`​  
​`#ifndef xxx`​ 当 预处理变量 未定义时为`true`​  
​`#endif xxx`​ 作为`#if...`​指令的结束

一般把预处理变量的变量名全部大写。
