# CPP基础1：程序架构

一个函数(function)包含四部分：  
返回类型(return type)，函数名(function name)，形参列表(parameter list)，函数体(function body)  
函数的最后一部分是大括号指示的函数体，是一个**语句块(block of statements)** 。

除main函数之外，函数可以通过改变形参列表重载。

函数`function(int m, int n){...}`​可以有默认实参`function(int m, int n = 1){...}`​

调用时可以省略靠后的有默认值的实参`function(5,8);或function(5);`​

程序从`main`​函数开始，它的返回类型必须为`int`​，时一种**内置类型（built-in type）,**  即语言自身定义的类型。  
大多数系统中`main`​的`return 0;`​返回值代表成功，非0值指出错误类型。

在函数的返回类型前加上关键字`inline`​，变成内联函数以减小开销。

‍

编译器具备集成开发环境(Integrated Developed Environment, IDE)

源文件(source file)在不同的IDE中有不同的后缀命名约定，如`.cc`​ `.cxx`​ `.cpp`​ `.cp`​ `.C`​

头文件在C语言中为`.h`​后缀，在C++中无后缀。

‍

用命令行`$ CC project1.cpp`​来编译文件并生成同名的`.exe`​文件。

执行`.exe`​文件时可忽略其拓展名，命令行`$ project1`​，一些系统中需要命令行`$ .\project1`​

通过命令行`$ echo %ERRORLEVEL%`​来访问`main`​函数的返回值。

命令行`$ project1 <infile>outfile`​ 使得程序从当前目录下的infile读取输入，oufile进行输出

‍

头文件（header）：`#include <iostream>`​

​`std::cout << "Hello World!" << std::end1;`​

​`运算顺序：(std::cout << "Hello World!") << std::end1;`​

​`等价于：	std::cout << "Hello World!";`​ 字符串字面值常量(string literal)  
​`		std::cout << std::end1;`​ 操纵符(manipulator)，end1结束当前行，  
并将与设备关联的缓冲区(buffer)中的内容刷到设备中。

表达式：由一个或多个运算对象与运算符组成，执行后产生一个计算结果。

​`<<`​运算符 接受两个运算对象，左侧必须为`ostream`​对象，右侧是要打印的值，  
此运算符将给定的值写到给定的`ostream`​对象中，  
输出运算符的计算结果是其左侧运算对象。

前缀`std`​指出`cout`​与`end1`​定义在名为`std`​的命名空间(namespace)中，  
使用作用域运算符`::`​来指出命名空间中的名字。

变量(variable)与初始化(initialize)与赋值(assignment)

​`>>`​运算符一样接受右侧，返回左侧，左侧必须为`istream`​对象

​`std::cin >> v1 >> v2`​

注释(comments)

条件语句：

​`if(condition1){statement1} else if(consition2){statement2} else {statement3}`​

​`switch(x){case 1: ... case 2: ... default: ...}`​ 符合case后一直执行到switch结尾。

迭代/循环语句：

​`while (condition) {statement}`​

​`do{statement}while(condition);`​

​`for (init-statement; condition; expression) {statement}`​

​`for(declaration : expression) { statement }`​

跳转语句：

​`break;`​ 作用于for/do while/while/switch

​`continue;`​ 作用于for/while/do while

​`goto mylable: ... mylable:`​ 弃用

‍

参数(实参)(argument)

C++中逻辑&&和逻辑||依然短路。

错误处理：`try{...throw 错误类;...}catch(...){...}catch(...){...}`​

​![image](assets/image-20241002003544-uk2skjk.png)​

预处理宏`assert(expr)`​，表达式为`false`​时直接终止程序运行并输出错误信息。  
写入`#define NDEBUG`​ 可以关闭所有`assert`​

​`__func__`​当前调试的函数  
​`__FILE__`​文件名  
​`__LINE__`​当前行号  
​`__TIME__`​文件编译时间  
​`__DATE__`​文件编译日期

表达式把运算对象通过运算符生成一个结果

C++的表达式分为右值(rvalue，读作are-value)，左值(lvalue，读作"ell-value")  
右值使用的是对象的值(内容)，左值使用的是对象的身份(在内存的位置)

|结合律|运算符|元数|功能||结合律|运算符|元数|功能||结合律|运算符|元数|功能|<br />|
| --------| --------| ------| --------| --| --------| --------| ------| --------| --| --------| --------| ------------| --------| ----|
||+|1|正号|||-|1|负号||右|!|1|非||
||+||加|||-||减|||<br />||||
||*||乘|||/||除|||%||求余||
|左|<|<=|==||左|>|>=|!=||左|&&|\|\||=||
||^|1|位求反||<br />|<<|2|位左移|||>>|2|位右移||
||&|2|位与|||\||2|位或|||^|2|位异或||
||++|||||--|||||？：|3|条件||

​`sizeof(type)`​和`sizeof(expr)`​返回字节数，得到`size_t`​ 类型的数值。

使用`using namespce::name;`​ 之后使用`name`​时就不必再说明其命名空间。
