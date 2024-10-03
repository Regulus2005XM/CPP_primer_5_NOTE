# CPP基础3：IO操作流

### 第一部分 IO库

##### 头文件iostream

​`istream`​和`wistream`​从流读取数据

​`ostream`​和`wostream`​向流写入数据

​`iostream`​和`wiostream`​读写流

标准库定义了4个IO对象，`cin`​标准输入，`cout`​标准输出，`cerr`​标准错误，`clog`​一般信息  
这四个对象也有对应的`w-`​版本。

不能对流类型进行初始化、赋值、拷贝的操作。

##### 头文件fstream

​`ifstream`​和`wifstream`​从文件读取数据

​`ofstream`​和`wofstream`​向文件写入数据

​`fstream`​和`wfstream`​读写文件

​![image](assets/image-20241002164602-cc9ye5z.png)​

​![image](assets/image-20241002164734-ljarpbu.png)​

##### 头文件sstream

​`istringstream`​和`w-`​版本，从`string`​读取数据

​`ostringstream`​和`w-`​版本，向`string`​写入数据

​`stringstream`​和`w-`​版本，读写`string`​

​![image](assets/image-20241002164800-s53jxp7.png)​

##### 条件状态

​`strm::iostate`​ 提供表达条件状态的完整功能

​`strm::badbit`​ 指出流已崩溃

​`strm::failbit`​ 指出一个IO操作失败了

​`strm::eofbit`​ 指出流到达了文件结束

​`strm::goodbit`​ 指出流未处于错误状态

​`s.eof() s.fail() s.bad() s.good()`​ 对应`-bit`​置位则返回`true`​

​`s.clear( /...)`​ 将流`s`​中的所有条件状态位复位，将流的状态设置为有效。可以指定参数。

​`s.setstate(...)`​ 将流`s`​中的对应条件状态位置位

​`s.rdstate()`​ 返回流`s`​的当前条件状态，返回值类型为`strm::iostate`​

##### 缓冲区

缓冲区在以下情况刷新：

1）程序结束时`main`​函数的`return`​操作会刷新缓冲区。  
2）缓冲区已满。  
3）有操纵符（如`end1`​）显式刷新缓冲区。  
4）从操纵符`unitbuf`​设置流的内部状态来清空缓冲区。  
5）一个输出流关联到另一个流，读写被关联流时，缓冲区刷新。  
	默认`cin`​和`cerr`​关联到`cout`​，读`cin`​或写`cerr`​会导致`cout`​的缓冲区刷新。

​`end1`​输出换行`\n`​并刷新缓冲区，`flush`​刷新缓冲区，`ends`​输出空格`\ `​并刷新缓冲区

​`cout << unitbuf;`​ 设置所有输出操作都立刻刷新，无缓冲。  
​`cout << nounitbuf;`​ 设置回到正常缓冲模式。
