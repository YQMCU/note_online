## 1. 检测QT是否安装

```dos
which qmake
qmake -v
```


## 2. c++ 编译

```dos
g++ -ansi -pedantic -Wall -o execFile fac.cpp
```

* `-ansi` 关闭与 ISO C++ 冲突的 GNU 扩展
* `-pedantic` 输出严格 ISO C++ 所要求的所有警告，阻止所有程序使用禁用的扩展语法
* `-Wall` 输出那些即使符合标准也可能被认为有问题的警告


## 3. 输入与输出

```cpp
#include <iostream>
```

* `cin` 标准输入流，默认为标准输入设备，即键盘
* `cout` 标准输出流，默认为标准输出设备，即控制台屏幕
* `cerr` 标准错误流，另一个输出到控制台屏幕的输出流，它频繁刷新，经常用来显示错误信息

```cpp
/**
 * @file src/iostream/io.cpp
 */

#include <string>
#include <iostream>

int main()
{
	using namespace std;
    const int THISYEAR = 2006;
    string yourName;
    int birthYear;

    cout << " What is your name? " << flush;
	cin >> yourName;

    cout << "What year were you born? ";
    cin >> birthYear;

    cout << "Your name is " << yourName
    	 << " and you are approximately "
         << (THISYEAR - birthYear)
         << " years old. " << endl;
}

```

## 4. 长字符串的c++处理

```cpp
#include <iostream>
#include <string>

int main()
{
	using namespace std;
    const * charstr = "this is one very long string "
    				  " so I will continue it on the next line";
    string str = charstr;
    cout << str << endl;
    cut << "\nA\tb\\c\'d\"" << endl;
    return 0;
}
```

## 5. c/c++ 数据类型

* 布尔型(bool)
* 字符型(char，wchar_t)
* 整型(short，int，long)
* 浮点型(double，float，long double 等)
* 指针(int \*，char \*，bool \*，double \*，void \* 等)

C和C++语言都使用 `void` 来表示没有类型信息的情况。

修饰关键字：

* short
* long
* signed
* unsigned

## 6. char 和 wchar_t

* char 多字节字符

    char ch = 'S';
    char ch = '中';

* wchar_t 宽字符 (所有字符都是2个字节，定义需要加L)

	wchar_t ch = L'S';
    wchar_t ch = L'中';

## 7. main 函数

```cpp
int main(int argc, char* argv[])
int main(int argc, char* * argv)
int main(int argCount, char* const argValue[])
```

## 8. C++ 标准库字符串

```cpp
#include <string>
#include <iostream>

int main()
{
	using namespace std;
    string s1("This "), s2("is a "), s3("string.");
    s1 += s2;
    string s4 = s1 + s3;
    cout << s4 << endl;

    string s5("The length of that string is: ");
    cout << s5 << s4.length << " characters." << endl;
    cout << "Enter a senstence: " << endl;
	getline(cin,s2);
    cout << "Here is your senstence: \n" << s2 << endl;
    cout << "The length of it was: " << s2.length() << endl;
    return 0;
}
```

## 9. 流

**流**是用来进行读写的对象，为此，标准库定义了 `<iostream>`，而 Qt 定义了 <QTextStream> 来提供对应的功能。


## 10. 文件的读写

* ofstream 写入文件 类比 cout

* ifstream 读入文件 类比 cin

***具体用法后期补充***


## 11. new 和 delete

new 运算符从内存堆中分配内存，并且返回指向最新分配对象的指针。

delete 运算符的作用是释放动态分配的内存，将其返回给内存堆。

如果不对new运算符返回的指针进行delete操作，则会引起内存泄露。


## 12. const

使用关键字 const 来保护指针和不需要根据函数行为进行改变的引用参数是一种非常好的编程习惯，只读的引用参数可以同时具有传引用的效率和传值的安全性。

const的函数不能对其数据成员进行修改操作

const的对象，不能引用非const的成员函数

***const函数的使用，参见下一节(class 类)的code片段。***

## 13. class 类

```cpp
/**
 * @file src/classes/fraction.h
 */

#ifndef _FRACTION_H_
#define _FRACTION_H_

#include <string>
using namespace std;

class Fraction{
	public:
    	void set(int numerator, int denominator);
        double toDouble() const;
        string toString() const;
    private:
    	int m_Numerator;
        int m_Denominator;
}

#endif
```


```cpp
/**
 * @file src/classes/fraction.cpp
 */
#include "fraction.h"
#include <sstream>

void Fraction::set(int nn, int nd)
{
	m_Numerator = nn;
    m_Denominator = nd;
}

double Fraction::toDouble() const
{
	return 1.0 * m_Numerator / m_Denominator;
}

string Fraction::toString() const
{
	ostringstream sstr;
    sstr << m_Numerator << "/" << m_Denominator;
    return sstr.str();
}

```


类成员访问限定符有：public,protected,private

* 该类的一个实例对象均可访问public成员
* protected成员只能在本类的成员函数或其派生类的成员函数的定义中使用
* private成员仅仅允许在本来的成员函数中进行访问


## 14. 块作用域

使用{}框起来的程序成为块作用域（内部作用域），块作用域中定义的变量，对外界不可见，不可访问。


## 15. 封装

封装是面向对象编程中的第一个概念性步骤，它主要包括:

* 把数据和操作数据的函数一起封装在命名风格良好的类中
* 提供命名清晰、文档丰富的公共函数，使类的使用者能够利用这些函数对此类的对象进行任何必需的操作
* 隐藏具体的实现细节

一个类的公共函数的原型集合称为此类的公共接口。

**非公共成员集合**与**函数定义本身**组成了类的具体实现。

封装的一个直接优势就是它允许程序员使用一致的类成员命名机制。


## 16. UML简介

UML即统一建模语言，是一种面向对象设计语言，我们使用UML图是因为相对于程序代码， UML图能更加精确、直观地描述类中的重要元素以及类之间的关系。

UML包含的内容绝不仅仅是类图，其他的UML图可以展示类之间如何合作，用户如何与类交互等。













