# C++ primer plus

## 第一章 预备知识

- 面向对象

## 第二章 开始学习C++

- 如果编译器到达main()函数末尾时没有遇到返回语句，则认为main()函数以return 0结尾

- **endl**

  - 
    
    ```c++
    cout<<endl;//表示换行
    ```

- cout

  - 
    
    ```C++
    cout<<XXX;//输出
    ```

- cin

  - `cin>>输入`

- 类简介

  - 类定义描述的是数据格式及其用法，例如有一个著名演员的类，小李子就是这个类的一个对象
  - 类描述了一种数据类型的全部属性（包括可使用它执行的操作），对象是根据这些描述创建的实体

- cmath

  - sqrt（double)
    - 开根号，返回double值

  - pow(double a,double b)
    - 求a的b次方，返回double值

  - rand(void)
    - 返回一个随机整数

## 第三章 处理数据

- 3.1 简单变量

  - 命名规则
    - 只能用字母字符，数字和下划线
    - 名称的第一个字符不能是数字
    - 区分大小写
    - 不能用关键字

- 3.2 const限定符

  - ```C++
    const type name=value;
    ```

    能够明确指定类型

    可用于数组和结构体

    可以使用C++的作用域规则将定义限制在特定的函数或文件中

- 3.3 浮点数

  - 表示方法（两种）

    - X.XXXXX

    - E表示法：X.XXEX

  - 浮点类型

    - float 32位

    - double 64位（默认情况下的浮点类型）

    - long doulbe 80,96或128位

  - cfloat

    - DBL_DIG/FLT_DIG/LDBL_DIG
      - double,float,long double的有效数字的字节数

    - DBL_MANT_DIG/FLT_MANT_DIG/LDBL_MANT_DIG
      - double，float,long double的尾数的字节数

    - DBL_MAX/MIN_10_EXP/FLT_MAX/MIN_10_EXP/LDBL_MAX/MIN_10_EXP
      - double,float,lobg double的指数部分的最大最小值

  - cout.setf()

    - cout会删除浮点数结尾的零,用成员函数.setf调整cout的行为

    - 显示float的所有位数：在下一个输出的cout前加上这个 cout.setf(ios_base::fixed, ios_base::floatfield);

  - 精度丢失
    - 原因
      - 有一些小数例如0.1，1.1没有精确的二进制数表示（因为转换的时候会出现一个无法达到结束条件的二进制数列），所以会出现精度丢失问题

- 3.4 运算符

  - 注意运算顺序

- 3.5 类型转换

  - 浮点转整型
    - C++截取整数部分（丢弃小数，而不是四舍五入）
  - {}初始化进行的转换
    - 不允许缩窄
      - 如：char c1{10000000}，char不能容纳这个数，初始化非法
  - 表达式中的转换
    - 整型提升
      - bool,char,unsigned char,signed char,short自动转换为int
  - 传递参数时的转换
  - 强制类型转换
    - (typename)value

- 3.6 auto声明

  - 编译器将类型设置成与初始值相同

## 第四章 复合类型

### 4.1 数组

- 创建数组typename arrayname[arraysize]

  - 从0开始，编译器不会检测数组下标是否有效

- 初始化

  - 只有在定义数组时才能初始化，不能将一个数组赋值给另一个数组
  - int num[]={1,2,3,4},形如这样初始化，编译器将自动计算元素个数并使用相应空间

- C++独有初始化

  - 省略等号

  - 初始化为零时，大括号内可以不包含任何东西

  - 禁止缩窄转换

  - ```C++
    int num{};
    ```

### 4.2 字符串

- C风格

  - 以空字符\0（ASCII码为0）结尾

- 字符串常量

  - ```C++
    char bird[]="Bubbles";
    ```

    用引号括起的字符串隐式地包括结尾的空字符

- cstring

  - strlen()
    - 计算字符串的长度，不计算空字符

- ```c++
  cin.getline(name,Size);
  cin.get;
  ```

  cin使用空白（空格，制表符和换行符）来确定字符串的结束位置

  - getline()
    - 读取整行，丢弃换行符。在读取完的末尾加一个空白符
  - get(){代替C的getchar}
    - 读取整行，将换行符保留在输入流中
    - 合并写法：cin.get(XX).get;解决换行符遗留问题

### 4.3 string类简介

```C++
#include<iostream>
#include<string>//使用string类的头文件
using namespace std;
int main()
{
    string a,b.c;
    getline(cin,a);//读取一行string；
    getline(cin,b);
    c=a+b;//string可直接相加拼接
    c=a;//string直接赋值
}
```

- 原时字符串raw

  ```C++
  R"+*XXXXXXXX+*"
  ```

  原始字符串是什么，输出的就是什么

### 4.4 结构简介

```C++
#include<iostream>
using namespace std;
struct  player{
    char name[20];
    float height;
    float weight;
};//外部结构声明，所有函数可用
int main()
{
    struct nil{
        int a;
        int b;
        int c;
    };//内部声明，仅该函数可用
    player goat{Jordan,1.98,80kg};
    //结构变量初始化
    nil zero{};
    //括号内空，各个成员全被设置为0
   	player laker[100];
	laker[0] = {
		"kobe",
		1.98,
		80
	};
    //结构数组
    cout<<laker[0].name;
    //访问结构成员
}
```

### 4.5 共用体/联合（union)

```C++
union Cool{
    int a;
    int b;
    int c;
};
//类似于结构体，但一次只能存储一个成员值。例如，union MVP {string name,int 球衣号码};因为一个球员可以用名字和球衣号码来区分，所以只用一个就能知道谁是mvp；这比结构更节省空间
```

### 4.6 枚举（enum)

```C++
enum spectrum{red,orange,yellow};
//默认情况下，将整数值赋值给枚举量。red=0,orange=1,以此类推
spectrum band;
//枚举变量声明
band=red;
//合法
band=2000;
//不合法。在不进行强制转换的前提下，枚举变量只有定义的枚举值能进行赋值
enum shit{a,b=100,c,d=100}
//设置枚举值，a=0,b=100,c=101,d=100
```

### 4.7 指针和自由存储空间

```C++
int a;
&a;
//地址运算符，获取一个变量的存储地址
int *p;
//指针声明，指针是指向地址的一种特殊变量。
//指针名是地址。
//空指针在C++中指向值为0的指针，不指向有效数据
//*运算符：间接值或接触引用。因为指针名存储的是地址，所以*p代表的就是存储在这个地址的值
int *pn=new int;
//new动态分配内存，节约资源
//这句声明==给pn分配int数据类型这么长的空间（4个字节），并将该内存的首地址返回给pn。
int i=5;int*pn=new int[i*5];
//分配i*5这么多int数据类型的空间，并将该内存的首地址返回给pn。
//如果调用pn[1000]，产生数组越界（覆盖另一内存区域的值），因为pn[1000]并没有在new动态分配的空间之内
*pn;//指向第一个元素
pn[x];//后续的元素这么引用
delete pn;
//清除动态分配的pn的空间
delete[]pn;
//清楚动态分配的数组的空间
//如果new了不delete，会发生内存泄漏

```

### 4.8 指针，数组和指针算术

- pn++？
  - 指针指向元素的地址往下一个元素的地址移动
- sizeof（pn）
  - sizeof对数组求所有元素的字节，对指针只求指针

- 4.8.3 指针和字符串

  - cout对提供地址的字符串
    - 给cout提供一个字符的地址，则它将从该字符开始打印，直到遇到空字符为止

  - 指针初始化字符串
    - char *pn="awesome";

- 4.8.4 new创建动态结构

  - 声明？
    - 结构名 *pn=new 结构名;

  - 访问成员

    - pn->成员名;

    - (*pn).成员名;【因为*pn就是结构本身，直接当成结构用】

- 4.8.5 自动存储，静态存储和动态存储

  - 自动存储
    - 自动变量是一个局部变量，作用域为包含它的代码块。（代码块是被包含在花括号中的一段代码）自动变量存储在栈中，后进先出（LIFO).

  - 静态存储
    - 静态变量有两种实现方式，在函数外面定义它；使用关键字static；

  - 动态存储
    - 动态变量存储在自由存储空间（堆）中，由new和delete管理，独立于静态和自动变量的组成空间，完全不受程序和函数的生存时间控制。

### 4.9 类型组合（略）

### 4.10 数组的替代品

- 模板类 vector

  ```C++
  #include<vector>
  vector<typename> vt(n);
  //n可以是常量，也可以是变量
  //开一个能存储n个typename类型的vector
  ```

- 模板类 array

  - 为什么用array？

    - vector类的功能比数组强大，但是运行效率低。如果需要长度固定的数组，而且要更方便和安全，那么array就诞生了

    ```C++
    #include<array>
    array<typename,n_elem>ai;
    //array声明，n_elem只能是常量
    //可以将一个array对象赋给另一个array对象
    ai[-2]=xx;
    //危险。
    //找到ai指向的地址，向前移两个数据类型大小，并对这个地址的元素进行赋值==将信息存储在array的外面，会抹除原地址对应元素，发生超界错误
    ai.at(-2);
    //程序会检测n是否合法。
    //避免出现超界错误，发现非法索引，中断程序，代价是运行变慢
    ```

## 第五章  循环和关系表达式（略）

## 第六章 分支语句和逻辑运算符

### 6.8 简单文件输入/输出

```C++
#inlcude<fstream>
//文件输入输出头文件
#include<iostream>
#include<string>
using namespace std;
int main()
{
    string a;
    ofstream outFile;
    //文件输出指针
    ifstream inFile;
    //文件输入指针
    outFile.open("test.txt");
    //打开文件进行输出
    //不存在test.txt新建一个；已存在，抹掉test.txt的所有内容后进行输出。
    outFile<<"Yes!";
    //进行输出
    outFile.close();
    //关闭文件指针
    inFile.open("test.txt");
    //打开输入文件
    inFile>>a;
    //用打开的文件给string a赋值
    inFile.getline(a,200);
    //获取一整行字符串，ifstream类似cin的用法
    inFile.close();
    //关闭文件指针
    return 0;
}
```

## 第七章 函数——C++的编程模块

### 7.1 复习函数基本知识（略）

### 7.2 函数参数和按值传递

- 函数内部的变量是局部变量，函数调用结束即销毁。

### 7.3 函数和数组（略）

### 7.4 函数和二维数组

- ```C++
  int ar2[][4]{};
  //二维数组本质，第一个括号的元素是指向第二个扩员的元素（数组）的指针
  ```

### 7.5 函数和C-风格字符串

-      ```C++
  char *str="Cool";
  //创建一个char类型的指针，指向字符串的第一个字符
  str++;
  //指针增加一个字节，指向下个字符
  ```

### 7.6 函数和结构

- 函数可以返回结构

### 7.7 函数和string对象

### 7.8 函数和array对象

### 7.9 递归

```c++
#include<iostream>
const int Len = 66;
const int Divs = 6;
using namespace std;
void subdivide(char ar[], int low, int high, int level);
int main()
{
	char ruler[Len];
	int i;
	for (i = 1; i < Len - 2; i++)
		ruler[i] = ' ';
	//尺子初始化为全空格
	ruler[Len - 1] = '\0';
	int max = Len - 2;
	int min = 0;
	ruler[min] = ruler[max] = '|';
	//尺子最上面那层标上刻度
	cout << ruler << endl;
	//输出最上层的尺子
	for (i = 1; i <= Divs; i++)
	{
		subdivide(ruler, min, max, i);
		cout << ruler << endl;
		//循环输出尺子的每一层
		for (int j = 1; j < Len - 2; j++)
		{
			ruler[j] = ' ';
		}
	}
	return 0;
}
void subdivide(char ar[], int low, int high, int level)//分治法递归
{
	if (level == 0)
		return;
	//结束条件
	int mid = (high + low) / 2;
	ar[mid] = '|';
	//根据尺子规律可以发现，在两条|的中间位置会又有一条|
	subdivide(ar, low, mid, level - 1);
	//递归调用。mid和low之间填|
	subdivide(ar, mid, high, level - 1);
	//递归调用，mid和high之间填|
}
```

### 7.10 函数指针（初探）

- 函数地址
  - 函数地址是存储其机器语言代码的内存的开始地址

```c++
#include<iostream>
void function();
int function1(int a, int b);
//定义两个函数
int main()
{
	void (*fp)();
    //没有参数，返回类型为void类型的函数指针
	int (*fn)(int a, int b);
    //有两个int参数，返回类型为int类型的函数指针
	fp = function;
    //fp指向function函数
	fn = function1;
    //fn指向function1函数
 
  //另外，还有返回函数指针的函数指针；返回函数指针的函数指针与数组，函数套中套。
    //这种情况下，可读性非常差。必须想办法简化
    //第一种，用auto声明
    //第二种，用typedf简化前面的套中套
    //例如
    typedef void(*f_pfr)();
    f_ptf f();//返回值是函数指针的函数定义
}
```

## 第8章 函数探幽

### 8.1 C++内联函数

- 内联函数不允许递归
- 内联代码运行速度比常规函数快，但占用更多的内存

```C++
#include<iostream>
inline double square(double x){return x*x;}
//内联函数定义与声明
using namespace std;
int main()
{
    double a=3.0,b=4.0;
    cout<<square(a);
    //合法
    cout<<square(a+b);
    //合法
    return 0;
    
    //注意与C宏定义#define的区别。
    //C++是按值传递，C是通过文本替换
}
```

### 8.2 引用变量

- 引用变量必须在声明引用时将其初始化。
- 引用变量一旦与某个变量关联起来，就不能成为其他变量的引用
- 尽可能使用const
  - const可以便面无意中修改数据的编程错误
  - const使函数能够处理const和非const实参，否则只能接受非const数据
  - 使用const引用使函数能够正确生成并使用临时变量

```C++
int a;
int &b=a;
//引用变量声明。即变量int a的另一个名字叫b。
void swap(int &a,int&b)
{
    int temp;
    temp=a;
    a=b;
    b=temp;
}
//函数按引用传递，能够改变原变量的值。
```

### 8.3 默认参数

```C++
char*left(const char*str,int n=1);
//带默认参数列表的函数声明
left(str);
//省略默认参数，默认n=1
left(str,3);
//存在n，n=3覆盖默认参数n=1
int hapo(int a,int b=2,int c=3);
//合法，带默认参数的函数必须从右向左添加默认值
int hapo(int a,int b=2,int c);
//不合法，不满足从右向左规则
```

### 8.4 函数重载

```C++
void yes();
void yes(int a,int b);
int yes(char a,int b);
//调用yes函数时，将根据提供的参数列表自动选择相应的yes函数
```

### 8.5 函数模板

```C++
template <typename T>
void Swap(T &a,T &b)
//当调用swap时，编译器将根据提供的参数列表自动替换T。
//如要交换两个int类型的数，T就是int
```

## 第9章 内存模型和名称空间

### 9.1 单独编译

- 即能将头文件，程序主体和类定义分开编译，然后再各自链接组成一个完整的程序

```C++
#ifndef COORDIN_H_
#endif
//这两个能C++避免出现重复编译
//#ifndef表示如果在整个编译过程中没有碰到COORDIN_H_,编译器将查看#ifndef和#endif之间的内容，否则不查看
```

### 9.2 存储持续性，作用域和链接性（初探）

## 第10章 对象和类

### 10.1 过程性编程和面向对象编程(略)

### 10.2 抽象和类

- 类对象的默认访问控制是:private

```c++
class Student{   //约定俗成，类声明首字母大写
    public:
    int number;//类成员
    double score;//类成员
    void display();//类成员函数
}
void Student::display()
{
    cout<<"A student";
}//成员函数定义
```



### 10.3 类的构造函数和析构函数

- 构造函数

  - ```c++
    class Student {
    public:
    	Student(int number=0, string name="0", double socre=0, double team=0);//这个就是构造函数，构造一个带默认参数的对象
    	int number;
    	string name;
    	double score;
    	double team;
    };
    Student::Student(int a, string b, double c, double d)
    {
    	number = a;
    	name = b;
    	score = c;
    	team = d;
    }//构造函数定义
    ```

- 析构函数

  - 用构造函数创建对象后，程序负责跟踪该对象，直到其过期为止。对象过期时，程序将自动调用析构函数完成清理工作。（如，当构造函数用了new时，析构函数相当于执行了delete）

```c++
class Student {
public:
	Student(int number=0, string name="0", double socre=0, double team=0);//这个就是构造函数，构造一个带默认参数的对象
    ~Student();//析构函数的原型必须是这样的，不带任何参数
	int number;
	string name;
	double score;
	double team;
};
Student::~Student()
{
}//析构函数只是用来清理构造函数的，不承担任何重要的工作，所以析构函数可以不执行任何操作

//就算没有显式定义析构函数，编译器会自动根据程序运行情况隐式地声明和调用一个默认析构函数
```

### 10.4 this 指针

- this是const指针，一切企图修改该指针地操作都是不允许的
- this只能在成员函数内部使用
- 只有当对象被创建后this才有意义，因此不能在static成员函数中使用

```c++
class Test {
public:
	Test(int number = 0, string name = "\0", int score = 0);
	int number;
	string name;
	int score;
};
Test::Test(int number, string name, int score)
{
    number=number;
    //形参和成员变量名称相同，编译器将此句当作给形参赋值。
	this->number = number;
    //用了this指针以后，this指向成员变量number。
    //所以这句的意思是，将形成number的值赋给成员变量number。
	this->name = name;
	this->score = score;
}
```



### 10.5 对象数组

```c++
class Student {
public:
	Student(int number=0, string name="0", double socre=0, double team=0);
	int number;
	string name;
	double score;
	double team;
};
void sort(Student A, Student B, Student C, Student D)
{
	Student arr[4];//对象数组。跟数组差不多，只是数组成员是类而已。
	arr[0] = A;
	arr[1] = B;
	arr[2] = C;
	arr[3] = D;
    arr[3].number=0;//访问D对象的number成员变量
```

### 10.6 类作用域

- 在类中定义常量

  - ```c++
    class Bakery
    {
        private:
        const int Months=12;//非法，因为在创建类对象以前，程序并没有给这个类划分存储空间，所以没有内存来存储这个常量
        static const int Months=12;//合法。使用了关键字static，Months变量将与其他静态变量存储在一起，而不是存储在对象中，而且Months能够被所有Bakery对象共享
    };
    ```

### 10.7 抽象数据类型（abstract data type,ADT）

- 栈(先进后出)

## 第11章 使用类

### 11.1 运算符重载

1. 重载限制
   1. 重载后的运算符必须至少有一个操作数是用户定义的类型
   2. 使用运算时不能违反运算符原来的句法规则，不能修改运算符的优先级
   3. 不能创建新运算符
   4. 不能重载下面的运算符
      - sizeof
      - .
      - .*
      - ::
      - ?:
      - typeid
      - const_cast
      - dynamic_cast
      - reinterpret_cast
      - static_cast
      - 后面四个都是强制类型转换运算符
   5. 下面的运算符只能通过成员函数进行重载
      - =
      - ()
      - []
      - ->

- 例子

```c++
#include <iostream>
//实现实数，虚数相加
using namespace std;
class complex{
public:
    complex();
    complex(double real, double imag);//构造函数
public:
    //声明运算符重载,重载"+"运算符
    complex operator+(const complex &A) const;
    void display() const;
private:
    double m_real;  //实部
    double m_imag;  //虚部
};
complex::complex(): m_real(0.0), m_imag(0.0){ }//构造函数定义
complex::complex(double real, double imag): m_real(real), m_imag(imag){ }//构造函数定义
//实现运算符重载
complex complex::operator+(const complex &A) const{
    complex B;
    B.m_real = this->m_real + A.m_real;
    B.m_imag = this->m_imag + A.m_imag;
    return B;
}
void complex::display() const{
    cout<<m_real<<" + "<<m_imag<<"i"<<endl;
}
int main(){
    complex c1(4.3, 5.8);
    complex c2(2.4, 3.7);
    complex c3;
    c3 = c1 + c2;//重载后的运算
    c3.display();
    return 0;
}
```

### 11.2 友元

1. 为什么使用友元函数
   1. 通过让函数成为类的友元，可以赋予该函数与类的成员函数相同的访问权限。

- 例，常用于重载<<

```c++
#include<iostream>
#include<string>
using namespace std;
class Student {
public:
	Student(int number = 0, string name = "0", double socre = 0, double team = 0);
    friend ostream& operator<<(ostream& os, const Student& t);
    //友元函数声明
private:
	int number;
	string name;
	double score;
	double team;
};
//友元函数重载<<定义
//ostream是iostream的输出类（cout所属的类，在这个类中重载，就能重载cout<<）
ostream& operator<<(ostream& os, const Student& t)
    //os指代的其实就是cout
    //参数是引用变量的形式，运行更快
{
	os << t.number << endl << t.name << endl << t.score << endl << t.team << endl << endl;
	return os;
    //返回os（cout）
    //能让它接着其他的输出，即cout<<Student A<<"YES,I WILL"<<endl;
    //而不用一行一行的写
    
    //原理:(cout<<Student A)这个是重载过的<<，执行完毕后返回cout
    //即变成了：(新cout)<<"YES,I WILL"<<endl;
    //后面内容满足ostream类cout的输出条件，所以接着输出
}
```

### 11.3 重载运算符：作为成员函数还是非成员函数

```c++
class Time{
  Time operator+(const Time &t) const/*const为了避免传递的参数和该函数被改变*/;
    //成员函数版本
    //+号需要两个操作数，而成员函数的操作数只有一个。这个参数是显式表示的操作数，另外一个操作数是被隐式传递的调用对象。
    friend Time operator+(const Time &t1,const Time &t2);
    //友元函数重载+号就必须要有两个操作数，因为它不能隐式传递
};
```

## 第12章 类和动态内存分配

### 12.1 动态内存和类

演示如何构建string类

## 第13章 类继承

 ### 13.1 一个简单的派生例子

1. 派生类需要在声明里添加什么？

   1. 派生类自己的构造函数
   2. 派生类可以根据需要添加额外的数据成员和成员函数
   3. 派生类创建之前一定会创建基类

2. 声明例子

   ```c++
   class TableTennisPlayer {
   private:
   	string firstname;
   	string lastname;
   	bool Table;
   public:
   	TableTennisPlayer(const string& fn = "none", const string& ln = "none", bool ht = false);
   };//基类声明
   
   //派生类声明。该例为公有派生
   class ratedplayer:public TableTennisPlayer {
   private:
       unsigned int rating;
       public ratedplayer();//派生类的构造函数
       public ratedplayer(unsigned int r,const TableTennisPlayer &tp );//派生类的又一构造函数，同样支持函数重载
       public ratedplayer(int r,string &fn,string &ln,bool ht);
       //有一个参数是基类的对象，间接使用基类的成员变量
   };
   ratedplayer::raterplayer(int r,string &fn,string &ln,bool ht):TableTennisPlayer(fn,ln,ht)
   {
       rating=r;
   }
   //第三个构造函数定义
   //1.参数fn,,ln,ht的值会传递给基类TableTennisPlayer的构造函数，同时创建一个基类对象
   //2.然后进入这个函数体，赋值rating，并创建一个ratedplayer类对象
   //ps.如果没有显式调用基类构造函数，程序将使用默认的基类构造函数（无参的，或者都初始化的）
   ```

### 13.2 多态公有继承

1. 定义
   - 不同的对象使用同一种方法，实现的行为不同
2. 怎么实现
   - 在派生类中重新定义基类的方法
   - 并使用虚方法

```c++
class Brass{
    public:
    virtual void function();//虚方法声明
};
class Brassplus : public Brass{
    public:
    virtual void function();//虚方法声明
}
int main()
{
    Brass A;
    Brassplus B;
    Brass &a=A;
    Brassplus &b=B;
    A.function();//调用Brass中的function
    B.function();//调用Brassplus中的function
    //下面这两个（引用和指针）如果没有使用虚方法的话，都会使用Brass类中的funtion
    //使用了虚方法就和上面那两个一样
    a.function();
    b.function();
}

//如果Brassplus包含一个执行某些操作的析构函数，则Brass必须有一个虚析构函数，即使该析构函数不执行任何操作。
```

3. (伪)实现指针数组容纳不同对象

   ```c++
   class Test{
       void function();
   };
   class Testplus{};
   int main()
   {
       Test *p[4]; //Test类指针数组
       Test A;
       Testplus B;
       p[0]=A;//Test类指针指向Test类对象，合情合理！
       p[1]=B;//Test类指针指向Testplus（派生类）对象，儿子和老子，同样合理！
       p[2]=new Test;//当然也能new一个
       p[1]->funtion();//指针数组调用成员函数写法！
       delete p[2];//new了要delete好习惯！
       return 0;
   } 
   ```

### 13.3 静态联编和动态联编

1. 什么是联编
   - 决定源代码执行哪一个函数的操作（为函数名赋予正确的函数代码块）

2. 静态联编
   - 编译时完成的联编（程序生成前）
3. 动态联编
   - 编译完成后的联编，由用户输入决定执行哪一个函数
4. 向上强制转换
   - 派生类转换为基类，编译器完成隐式转换，不用显式声明
5. 向下强制转换
   - 基类转换为派生类，必须显式声明
6. 虚函数和动态联编
   1. 虚函数都是动态联编
   2. 虚函数工作原理
   3. 存在虚函数的类在新建对象时，都会为这个对象添加一个隐藏成员——虚函数表（的地址）。在调用这个类的成员函数时，指针指向虚函数表的存储区域，在这个存储区域（虚函数表）中寻找对应的函数的地址，再利用这个地址调用函数
7. 使用虚函数的代价
   1. 每个对象都将增大，增大量为存储地址的空间
   2. 对于每个类，编译器都将创建一个虚函数地址表（数组）
   3. 对于每个函数调用，都需要执行一项额外的操作，即到表中查找地址
8. 虚函数注意事项
   1. 派生类不能继承基类的构造函数，所以构造函数不能是虚函数
   2. 析构函数应当时虚函数，除非不用做基类（不做基类，通常也将析构函数写成虚的）
   3. 友元不能是虚函数，因为只有成员是才能是虚函数
   4. 如果派生类没有重新定义函数，将使用该函数的基类版本
   5. 重新定义会隐藏方法，也就是说，如果派生类和基类都有同名虚函数，派生类不能调用基类的虚函数，因为它被隐藏了（本质是派生类的虚函数表里没有对应函数的地址），基类同理

### 13.4 访问控制:protected

对外界对象，protected==private

对派生类，protected==public

### 13.5 抽象基类

用来规范继承的代码。

假如，要实现一个图形类，派生类有圆，椭圆等等。再假设要写一个显示这个图形数据的功能。如果每个子类各自写一个函数，那么每个人有不同的命名，命名不好统一（或者说，没有实现基类必须要有的功能）。

但是，每个子类函数又不可能在一个函数里实现，这时，就有了抽象基类（ABC）的概念。

``virtual void View()=0;``这定义了一个纯虚函数，纯虚函数可以没有定义，也可以有定义。这样，子类就能够通过这个接口访问父类以及用规范地写View函数。

注意：包含纯虚函数地类只用作基类，且不能为这个类创建对象

## 第14章 C++中的代码重用

### 14.1 包含对象成员的类

```c++
#include<iostream>
#include<valarray>
//模板数组头文件
#include<string>
using namespace std;
//包含对象成员的类
class Student {
private:
	string name;
	valarray<int> number;
public:
	Student():name("Null"),number(){}//构造函数初始化列表，等价于
	//Student(string name="Null",valarray<int> number);
	explicit Student(int n) :name("Null"), number(n) {}//构造函数初始化列表，等价于
	//Student（string name="Null",valarray<int> number(n));
	//explicit屏蔽隐式转换，这里不屏蔽隐式转换，int n就是valarray<int> number这个数组里面的值
    explicit Student(string &name,int n):number(n),name(name){}
    //初始化列表顺序规则：按照类中成员的声明顺序先后初始化
    //所以，这里还是先初始化name，再初始化number
	virtual ~Student(){}
	//析构函数
};
Student::Student(int n) :name("Null"), number(n) {
}
int main()
{
	valarray<int> v1{ 1,2,3,4 };//同样满足列表初始化
	v1.size();//返回包含的元素数
	v1.sum();//返回所有元素的总和
	v1.max();//返回最大的元素
	v1.min();//返回最小的元素
	Student doh(10);
	//doh{string name="Null",valarray<int> number(10)}
	return 0;
}
```

### 14.2 私有继承

1. 三种继承
   1. 公有继承：基类属性不变，完整地被子类继承
   2. 私有继承：基类的所有成员被子类以私有成员形式继承，也就是说子类的子类不能再访问这个基类
   3. 保护继承：基类的所有成员被子类以保护成员形式继承，子类的子类能够访问这个基类（对派生类是公有，对外是私有）
2. 多重继承
   1. 使用多个基类的继承
3. 例子

```c++
#include<iostream>
#include<string>
#include<valarray>
using namespace std;
//多重继承
//且声明有私有继承。另外private是默认值，因此private，也是私有继承。
class Student :private string, valarray<double> {
private:
	typedef valarray<double> arr;
	string name;
	arr scores;
public:
	Student(string &m_name,int n):string(m_name),arr(n){}
	double max();
	using arr::sum;
	//表明这个类的对象可以使用sum方法
	//注意，using只是用成员名——没有圆括号，函数特征标和返回类型
	string re_name(string& name);
	//成员初始化列表使用类名，而不是成员名（私有继承区别1）
};
string Student::re_name(string& name)
{
	return(const string&)* this;
}
//访问基类成员的办法，强制类型转换（私有继承区别3）
//*this指针指向该函数存储在基类string中的name
//强制转换其返回子类从基类中继承string对象
//访问友元函数同理，强制类型转换（私有继承区别4）
Student::Student(string& m_name, int n) :string(m_name), arr(n) {}
double Student::max()
{
	return scores.max();
}
int main()
{
	string a = "A";
	Student A(a, 5);
	A.min();//非法，因为基类的方法已经变成私有的，类外无法访问（私有继承区别2）
	A.max();//合法，因为Student类中建立了一个函数，并在这个函数中调用了基类.max()的方法。相当于将.max()方法公有化。
	A.sum();//合法，调用基类方法的另一种方法
}

//私有继承区别5
//继承只能只用一个从基类继承而来的对象（当对象都没有名称时，将难以区分）
```

### 14.3 多重继承

1. 多重继承出现的问题

   1. 假设B,C都有同一个基类A，继承了B,C的子类D。``D member;A *pw=&member``

      那么这段代码就会出现二义性：pw指向B继承的A还是指向C继承的A。

      解决办法是类型转换``A *pw=(B *)&member``,这样pw指向的是B继承的A

2. 虚基类

   1. 从1可以看出，多个有相同基类的子类会各自建立自己的基类副本，但有时候又不需要这么多的副本，虚基类的意义就在这里。

      定义：虚基类使得多个有相同基类的派生出的对象只继承一个基类对象

      语法：``class B:virtual public class{};``(public,virtual的顺序无所谓)

   2. 不同的构造函数规则

      ```c++
      class A       //定义基类A
            { A(int i){}//基类构造函数，有一个参数
              ...};
         class B：virtual public A //A作为B的虚基类
            { B(int n):A(n){}    //B类构造函数，在初始化表中对虚基类初始化
              …}；
         class C：virtual public A //A作为C的虚基类
            { C(int n):A(n)){}   //C类构造函数，在初始化表中对虚基类初始化
              …}；
         class D：public B，public C //类D的构造函数，在初始化表中对所有基类初始化
            { D(int n):A(n)，B(n)，C(n){}
              …}；
      
      /*注意：
         1、在定义类D的构造函数时，与以往使用的方法有所不同。
      
      规定：在最后的派生类中不仅要负责对其直接基类进行初始化，还要负责对虚基类初始化。
      
         2、C++编译系统只执行最后的派生类对虚基类的构造函数的调用，而忽略虚基类的其他派生类(如类B和类c)对虚基类的构造函数的调用，这就保证了虚基类的数据成员不会被多次初始化。
         */
      ```

### 14.4 类模板（重要）

1. 什么是类模板

   1. 类模板，可以定义相同的操作，但是拥有不同数据类型的成员属性。

2. 例子

   ```c++
   template<class T1, class T2,int size>//声明模板前要加这句
       //表明有两种类型T1，T2
       //类型参数表可以出现非类型参数
   class Pair {
   public:
   	T1 key;//T1类型的key
   	T2 value;//T2类型的value
   	Pair(T1 k, T2 v) :key(v), value(v) {}//初始化列表
   	bool operator<(const Pair<T1, T2>& p)const;//重载“<”运算符
       //参数为Pair类对象的引用
   };
   template <class T1, class T2>
       //实现成员函数时也要加这句
   bool Pair<T1, T2>/*（解析域也要加<T1,T2>*/::operator<(const Pair<T1, T2>& p)const
   {
   	return key < p.key;
   }
   int main()
   {
       Pair<string,int>student("Tom,19")
          //实例化一个类，Pair<string,int>,行话:类模板的实例化 
           //T1类型为string,T2类型为int
          return 0;
   }
   
   //类模板，原来的那个模板
   //模板类，实例化的类模板
   ```

3. 函数模板作为类模板成员

   ```c++
   #include<iostream>
   using namespace std;
   template <class T>//类模板
   class A {
   public:
   	template<class T2>//函数模板
   	//函数模板的类型名不能与类模板的类型名同名
   	void Func(T2 t) { cout << t; }
   };
   ```

   

4. 继承相关

   1. 类模板派生类模板

   ```c++
   #include<iostream>
   using namespace std;
   template <class T1,class T2>
   class A {};
   //基类类模板
   template <class T1,class T2>
   class B:public A<T2,T1>{};
   //派生基类类模板
   //类型参数表可以相同也可以不同
   ```

   2. 模板类派生类模板
   
      ```c++
      template <class T>
      
      class base
      
      {
      ……
      
      };
      
       
      
      class derive:public base<int>
      
      {
      ……
      
      };
      
      //在定义derive类时，base已实例化成了int型的模板类。
      //所以编译结束时一共有两个模板类，base和derive
      ```
   
      
   
   3. 普通类派生类模板
   
      ```c++
      class MyBase            //普通类
      { 
          int v1; 
      };
       
      template<class T>
      class MyDrived: public MyBase    //MyDrived:模板类 继承自普通类
      { 
          T v; 
      };
       
      int main ()
      { 
          MyDrived <char> obj1; 
          return 0; 
      }
      ```
   
      
   
   4. 模板类派生普通类
   
      ```c++
      
      template <class T>
      class MyBase
      { 
          T v1; 
          int n; 
      };
       
      class MyDrived: public MyBase <int>         //普通的类继承自 特定模板类
      {     
          double v; 
      };
       
      int main() 
      { 
          MyDrived   obj1; 
          return 0; 
      }
      ```

## 第15章 友元，异常和其他

### 15.1 友元

1. 类并非只能拥有友元函数，也可以将类作为友元。友元类的所有方法都可以访问原始类的私有成员和保护成员。

2. 友元类声明可以位于公有，私有或保护部分，其所在位置无关紧要。

   ```c++
   #pragma once
   //类全部成为友元类
   class Tv {
   public:
   	friend class remote;//友元类声明
   	bool open();
   protected:
   	int channel;
   };
   class remote {
   public:
   	void set(Tv& T, int ch) {
   		T.channel = ch;
   	}//直接设置基类数据
   	bool is_open(Tv& T) { return T.open(); }//调用基类函数
   };
   //好处：不必设置继承多个父类的子类
   ```

3. 能使特定的类成员成为另一个了类的友元（有点麻烦，必须注意声明和定义的顺序）

   ```c++
   #pragma once
   class Tv;//前向声明
   class Remote
   {
   public:
   	void set_chan(Tv &t,int c);
   };
   class Tv {
   public:
   	friend void Remote::set_chan(Tv& t, int c);//Remote特定成员作为友元
   };
   
   //对于Tv类，如果前面没有Remote类及其方法的声明，编译器不知道Remote是类。所以，Remote声明要放在Tv前面
   //而对于Remote类，它的方法中又要调用Tv的引用参数，而Tv的声明又在Remote之后，同样，编译器也不直到Tv是个类
   //所以，就必须使用前向声明来解决上述问题
   ```

### 15.2 嵌套类







