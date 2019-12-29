# zuoye
#### 9.11

###### vector<int> vec;   

###### vector<int> vec(10);    

###### vector<int> vec(10,1);  

###### vector<int> vec{1,2,3,4,5};

#### 9.20

###### list<int> list1(5,7);

###### list<int>::iterator it1 = list1.begin();

###### for (it1; it1 != list1.end(); it1++)

###### {

###### 	if ((*it1)%2 == 0)

###### 	{

###### 		deque1.push_back(*it1);

###### 	} 

###### 	else

###### 	{

###### 		deque2.push_back(*it1);

###### 	}

###### }

#### 9.29

###### resize()改变容器的大小，多删少补并初始化，需要默认初始化的，则需要参数类型有默认构造函数。

#### 9.52

###### stack栈适配器有其特有操作，pop()—删除栈顶元素、push()—将元素压栈表示其进出栈操作，top()返回栈顶元素，但不弹出。先进后出。

###### queue和priority_queue操作类似，注意该pop()和push()等操作与stack不同。先进先出。

#### 10.3

###### 标准库基本上都是对一个范围内的容器进行操作，所以参数中总会有两个表示范围的迭代器

###### int a[10] = {0,1,2,5,4,5,4,5,4,5};

###### vector<int> vec(a,a+10);

###### cout<<"元素之和为："<<accumulate(vec.begin(),vec.end(),0);

#### 10.15

###### [a] (int &b) {cout<<a+b;}

#### 10.34

###### 反向迭代器，加上r，反向迭代器需要的是递减运算符，操作会从cbegin()反向处理string，rbegin()指向的是最后一个元素，rend()指向的是首元素之前的位置，通过调用反向迭代器的base()成员函数，可以将其转换为对应的普通迭代器

#### 10.42

###### sort()需要随机访问迭代器，所以不能用于list和forward_list，对于list和forward_list应优先使用其成员函数版本的算法，皆返回void，remove()删除元素，reverse()反转元素顺序，sort()排序，unique()删除相同元素，链表类型还定义了splice成员算法，其实链表数据结构所特有的，主要用于合并两个链表

#### 11.17

###### 第三个back_inserter()需要使用push_back()，而set不能够使用push_back()

#### 11.38

###### 用这个无序容器应该是不影响操作的

#### 13.12

###### 当指向一个对象的引用或者指针离开作用域是，析构函数并不会执行

#### 13.46

###### (a)：f()为函数的返回值，临时值，属于右值，&&

###### (b)：vi[0]为变量，属于左值，&

###### (c)：r1为变量，属于左值，&

###### (d)：右侧为表达式，属于右值，&&

#### 13.49

###### 类的移动构造函数：参数为该类类型的右值引用，任何额外参数须有默认参数，一旦资源被移动，源对象对移动之后的资源已经不再有控制权，最后源对象会被销毁。移动操作不会报出任何异常，因为其不分配资源。不抛出异常的移动构造函数和移动赋值运算符必须标记为noexpect，移动后的源对象可能会在移动后被销毁，所以必须进入可析构的状态——将源对象的指针成员置为nullptr来实现

#### 13.58

~~~c++
class Foo {
public:
	Foo sorted()&&;
	Foo sorted() const&;

private:
	vector<int> data;
};

Foo Foo::sorted() &&
{
	sort(data.begin(), data.end());
	std::cout << "&&" << std::endl; 
	return *this;
}

Foo Foo::sorted() const &
{
```c++
std::cout << "const &" << std::endl; 

return Foo(*this).sorted(); 
```

}

int main()
{
	Foo().sorted(); 
	Foo f;
	f.sorted(); 
}

~~~

#### 15.1

###### 面向对象程序设计的三个基本概念：数据抽象、继承和动态绑定(核心概念)

###### 数据抽象：将类的接口与实现分离

###### 继承：我们可以定义与其他类相似但完全不相同的新类

###### 动态绑定：在使用这些彼此相似的类时，在一定程度上忽略他们的区别，统一使用它们的对象

#### 15.12

###### 当然有需要啊，两个不一样的，override是表示对其基类函数的覆盖，final是表示此函数不能再被其他的函数所覆盖

#### 15.16

```c++
class limit_quote : public Disc_quote
{
public:
	limit_quote();
	limit_quote(const string&book, double price, size_t qty,double disc):Disc_quote(book,price,qty,disc){}
	double net_price(size_t n) const
	{
		if (n > quantity)
		{
			return quantity*(1-_discount)*price+(n-quantity)*price;
		} 
		else
		{
			return quantity*(1-_discount)*price;
		}
	}
};

```

#### 16.11

###### 类模版的定义：与函数模版不同的是，编译器不会为类模版推断模版参数类型，所以我们在使用类模版时，需要显式地指出元素的类型，在其定义中，模版参数可以当作类型使用，用来表示类保存的元素的类型

###### 一个类模版的每个实例都会形成一个独立的类，与其他实例化的类之间并没有特殊的访问权限,实例化时，编译器会重写类模版，将模版参数替换为给定的模版实参

###### 在一个类模版中使用另一种模版，通常不会将一个实际的类型当作其模版实参，而将模版自己的参数当作被使用模版的实参

#### 16.19

###### Have.h

```c++
#ifndef HAVE_H
#define HAVE_H

template <typename T> void Have(T &t)
{

	for (size_t i = 0; i < t.size(); ++i)
	{

		cout<<t[i]<<endl;

	}
}
```

```c++
int main(int argc,char** argv)
{
	vector<int> vec1;
	vec1.push_back(2);
	vec1.push_back(3);
	Have(vec1);
	system("pause");
	return 0;
}
```

#### 16.41

```c++

#ifndef REU_TYPE_H
#define REU_TYPE_H
 
template <typename T> auto sum(const T&a,const T&b) ->decltype(a+b)
{
	return a+b;
}
#include <iostream>
#include <vector>
#include <list>
#include <string>
#include "Reu_type.h"
using namespace std;
 
 
int main(int argc,char** argv)
{
	int a = 566669;
	int b = 595955;
	cout<<sum(a,b);
	cin.get();
	return 0;
}
```

#### 16.62

```c++

#ifndef SHOW_TIMES_H
#define SHOW_TIMES_H
 
template<typename T, typename U> int show_times(const T& vec,const U& val)
{
	int showtimes = 0;
	for (size_t i = 0; i < vec.size(); ++i)
	{
		if(vec[i] == val)
		{
			++showtimes;
		}
	}
	return showtimes;
}
#include <iostream>
#include <vector>
#include <list>
#include <string>
#include "show_times.h"
using namespace std;
 
int main(int argc,char** argv)
{
	vector<int> vec1;
	vec1.push_back(1);
	vec1.push_back(2);
	int a = 1;
	cout<<a<<"出现次数为："<<show_times(vec1,a)<<endl;
 
	vector<double> vec2;
	vec2.push_back(1.2);
	vec2.push_back(2.4);
	double b = 1.2;
	cout<<b<<"出现次数为："<<show_times(vec2,b)<<endl;
 
	vector<string> vec3;
	vec3.push_back(string("123"));
	vec3.push_back(string("23"));
	string c = "123";
	cout<<c<<"出现次数为："<<show_times(vec3,c)<<endl;
	cin.get();
	return 0;
}

```

