# 观前提醒

本篇文章共4070词，读完大概需要11分钟。

![](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202303091322672.jpeg)

# 写在前面

本篇文章将为你讲解C++动态内存管理，也就是`new`系列套件，但是由于C++兼容C语言，所以我会提及C语言的动态内存管理方式，也就是`malloc`系列套件。如果你学过C语言并且对C语言动态内存管理方式有一定的了解，那么本文的对比讲解也许能对你的理解有所帮助，那如果你没有接触过C语言可以选择性的观看本文章的内容。

# 虚拟内存

在聊内存管理之前，我们先来简单了解一下**虚拟内存**。虚拟内存是一个**抽象概念**，它为每个进程提供独占主存的假象。为什么要提供这个假象呢？下面我在这简单解释一下，毕竟这是属于操作系统的知识，这里只需要简单理解一下能帮助我们理解就行。

进程是跑在操作系统之上的，而操作系统为更好地封装以保护自身的安全，不提供真正地物理内存而给进程提供这个假象，让程序使用这套虚拟内存间接的与计算机沟通。也就是说，一份代码为了能与计算机沟通，必须遵守虚拟内存的规则，那么程序编译的时候就也需要遵守这套虚拟内存的规则。

这是从整体的角度看待，下面从语言的角度看内存区域划分也就是虚拟进程地址空间。

## 虚拟进程地址空间

### 分布

![虚拟进程地址空间](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202302281708574.jpg)

在本篇文章中，我们只需要关注这几个区域：

* 代码段：存放可执行的代码和只读常量。
* 数据段：存放全局数据、静态数据。
* 堆：程序运行时创建，用于程序运行时申请动态内存，堆是可以向上增长的（堆区空间不够分配时）。在堆区的数据存储空间是由用户自主申请，自主释放的。
* 栈：程序运行时创建，又叫堆栈，存放非静态局部变量、函数参数、返回值等。栈区的数据存储空间由系统自动分配，自动释放（如直接定义的局部变量，存储在函数栈帧中，当该函数结束时，函数栈帧销毁，栈区空间减小，局部数据的空间自然就释放了）。

参照下图看看C++程序内容对应的位置：

![image-20230228215330876](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202302282153274.png)

### 大小

在32位平台上，一个地址（指针）能标识的二进制数字位数有32位。而一个指针指向的地址空间大小是一个字节，那么，也就是说，在32位机器中，虚拟进程地址空间的大小为4G。

![32位进程地址空间大小](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202303052209715.png)



而在虚拟进程空间中，栈区的预留空间通常只有几M（具体由不同操作系统决定），堆区的预留空间大小一般没有软限制，Linux下通常小于3G，windows下通常小于2G。**栈区和堆区可利用空间相差之大**由此可见。

### 空间的划分与内存管理

通过上面的内容我们知道两个结论：

1. 栈区的可利用空间相比堆区很少。
2. 堆区的资源需要我们主动申请以及释放，可以灵活地根据我们的需求存储数据。

所以，由于栈区可利用空间小，C/C++程序经常需要使用堆上的空间存储数据，并且，堆上的空间资源需要用户也就是我们程序员通过代码申请，那么**C/C++就需要提供一套申请堆上空间资源的方法**，这个方法也叫做**C/C++动态内存管理**。在C语言中，管理动态内存的方式是`malloc`/`calloc`/`realloc`/`free`几个函数组成的套件。在C++中，则是`new`/`new type[]`/`delete`/`delete[]`几个操作符组成的套件。



# C/C++动态内存使用（管理）方式

## C语言动态内存管理方式：`malloc`/`calloc`/`realloc`/`free`

使用演示：

```c++
void test()
{
	int* p1 = (int*)malloc(sizeof(int));
	int* p2 = (int*)calloc(4,sizeof(int));
	int* p3 = (int*)realloc(p2, sizeof(int) * 8);

	free(p1);
	free(p3);
}
```

这里我就不作过多讲解了，对C语言内存管理方式不够了解或者已经比较生疏了的话可以看看我的[这篇文章](https://blog.csdn.net/crrrush/article/details/126881269)。

## C++内存管理方式

由于C++是兼容C的，所以C语言内存管理方式在C++中可以继续使用，但C语言的内存管理方式并不适合C++中的某些场景，且使用起来比较麻烦，因此C++又提出了自己的内存管理方式：**通过`new`和`delete`操作符进行动态内存管理**。

## `new`/`delete`操作内置类型

```c++
void test()
{
	//动态申请一个int类型大小的空间
	int* ptr1 = new int;

	//动态申请一个int类型大小的空间并初始化为10
	int* ptr2 = new int(10);

	//动态申请5个int类型大小的空间
	int* ptr3 = new int[5];
    
    //批量申请空间并初始化
    int* ptr4 = new int[10]{1，2，3，4};//后面未指定的为0
    
    
	//返还申请到的空间
	delete ptr1;
	delete ptr2;
	delete[] ptr3;
    delete[] ptr4;
}
```

![image-20230302101446626](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202303021014973.png)

C++对于内置类型的操作和C语言那一套相比只是**简化**了。但是，如果你对C语言内存管理还熟悉的话，你应该还记得C语言申请完内存还需要检查是否申请成功，为什么C++没有了？其实有的，只不过面向对象的语言更喜欢用**捕异常**的方式解决，而捕异常的操作被内置到了`new`操作符底层中，下面的内容会提到。

**注意：申请和释放单个元素的空间，使用`new`和`delete`操作符，申请和释放连续的空间，使用`new[]`和`delete[]`，一定要匹配起来使用！！！**如果不匹配使用，会出现各种出人预料且棘手的问题（取决于编译器以及运行环境）。

## `new`/`delete`操作自定义类型

```c++
class A
{
public:
	A()
	{
		cout << "A():" << this << endl;
	}

	~A()
	{
		cout << "~A():" << this << endl;
	}
};

void test()
{
	// new/delete 和 malloc/free套件最大区别：
	// new/delete 对于自定义类型除了开空间还会调用构造函数和析构函数
	A* p1 = (A*)malloc(sizeof(A));
	A* p2 = new A;
	free(p1);
	delete p2;

	cout << "---------------------" << endl;// boundary

	p1 = (A*)malloc(10 * sizeof(A));
	p2 = new A[10];

	free(p1);
	delete[] p2;
}
```

运行截图：

![image-20230302105404121](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202303021054524.png)

**注意：在申请自定义类型的空间时，`new`会调用构造函数，`delete`会调用析构函数，而`malloc`/`free`不会。**

# `new`/`delete`底层讲解

`new`/`delete`本质其实还是通过对`malloc`和`free`的封装实现的，下面**从里到外**带你看看是如何封装的。

## `operator new`与`operator delete`函数

```c++
/*
operator new：该函数实际通过malloc来申请空间，当malloc申请空间成功时直接返回；申请空间
失败，尝试执行空间不足应对措施，如果改应对措施用户设置了，则继续申请，否则抛异常。
*/
void* __CRTDECL operator new(size_t size) _THROW1(_STD bad_alloc)
{
	// try to allocate size bytes
	void* p;
	while ((p = malloc(size)) == 0)
		if (_callnewh(size) == 0)
		{
			// report no memory
			// 如果申请内存失败了，这里会抛出bad_alloc 类型异常
			static const std::bad_alloc nomem;
			_RAISE(nomem);
		}
	return (p);
}
/*
operator delete: 该函数最终是通过free来释放空间的
*/
void operator delete(void* pUserData)
{
	_CrtMemBlockHeader* pHead;

	RTCCALLBACK(_RTC_Free_hook, (pUserData, 0));
    
	if (pUserData == NULL)
		return;
    
	_mlock(_HEAP_LOCK); /* block other threads */
	__TRY
        
	/* get a pointer to memory block header */
	pHead = pHdr(pUserData);
    
	/* verify block type */
	_ASSERTE(_BLOCK_TYPE_IS_VALID(pHead->nBlockUse));
	
    _free_dbg(pUserData, pHead->nBlockUse);
	
    __FINALLY
		_munlock(_HEAP_LOCK); /* release other threads */
	__END_TRY_FINALLY
		
    return;
}
/*
free的实现
*/
#define free(p) _free_dbg(p, _NORMAL_BLOCK)
```

![image-20230302125623268](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202303021256316.png)

![image-20230302125925809](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202303021259858.png)

通过上述两个全局函数的实现知道，**`operator new`实际也是通过`malloc`来申请空间**，如果`malloc`申请空间成功就直接返回，否则执行用户提供的空间不足应对措施，如果用户提供该措施就继续申请，否则**抛异常**。**`operator delete`最终也是通过`free`来释放空间的**。

**注意：`operator new`和`operator delete`这两个函数不是操作符重载！重载操作符函数至少有一个参数是自定义类型参数，这两个函数是库里面实现的全局函数。这只是C++设计时一个命名失误。**



## `new`和`delete`的实现原理

### 内置类型

如果申请的是内置类型的空间，`new`和`malloc`，`delete`和`free`基本类似，不同的地方是：`new`/`delete`申请和释放的是单个元素的空间，`new[]`和`delete[]`申请的是连续空间，而且`new`在申请空间失败时会抛异常，`malloc`会返回`NULL`。

### 自定义类型

* **`new`的原理**
  1. 调用`operator new`函数申请空间。
  2. 在申请的空间上执行构造函数，完成对象的构造。
* **`delete`的原理**
  1. 在空间上执行析构函数，完成对象中资源的清理工作。
  2. 调用`operator delete`函数释放对象。
* **`new T[N]`的原理**
  1. 调用`operator new[]`函数，在`operator new[]`中实际调用`operator new`函数完成N个对象空间的申请。
  1. 在申请的空间上执行N次拷贝构造函数。
* **`delete[]`的原理**
  1. 在释放的对象空间上执行N次析构函数，完成N个对象中资源的清理。
  2. 调用`operator delete[]`释放空间，实际在`operator delete[]`中调用`operator delete`来释放空间。

以`new`为例，简单看看汇编验证一下：

实验代码：

```c++
class A
{
public:
	A(int a = 0) :_a(a) {cout << "A():" << this << endl;}

	~A() {cout << "~A():" << this << endl;}

private:
	int _a;
};

int main()
{
	A* a1 = new A(1);

	delete a1;

	return 0;
}
```

运行截图：

![image-20230308150436757](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202303081504833.png)



# 定位new（placement-new）

定位new表达式是在**已分配的原始内存空间中调用构造函数初始化一个对象**。

**使用格式：**

**`new(place_address)type`或者`new(place_address)type(initializer-list)`**

**place_address必须是一个指针，initializer-list是类型的初始化列表。**

使用演示：

```c++
class A
{
public:
	A(int a = 0) :_a(a) {cout << "A():" << this << endl;}

	~A() {cout << "~A():" << this << endl;}

private:
	int _a;
};

//定位new / replacement new
int main()
{
	A* p1 = (A*)malloc(sizeof A);
	//p1现在指向的不过是A对象相同大小的一段空间，还不是算是一个对象，因为构造函数没有执行
	new(p1)A;
	p1->~A();//析构函数	显式调用公有成员函数
	free(p1);

	A* p2 = (A*)operator new(sizeof A);
	new(p2)A(10);
	p2->~A();
	operator delete(p2);

	return 0;
}
```

运行截图：

![image-20230307124627673](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202303071246923.png)



**使用场景：**

相比于`new`，定位new并不怎么好用，所以**实际应用场景非常少**，一般是配合**内存池**使用的（池化技术）。因为内存池分配出的内存没有初始化，所以如果是自定义类型的对象，需要使用`new`的定义表达式进行显示构造函数进行初始化。



# 常见面试题

## `malloc`/`free`和`new`/`delete`的区别

共同点：都是从堆上申请空间，并且需要从堆上申请空间，并且需要用户手动释放。

不同点：

1. `malloc`和`free`是函数，`new`和`delete`是操作符。
2. `malloc`申请的空间不会初始化，`new`可以初始化。
3. `malloc`申请空间时需要手动计算空间大小并传递，`new`只需在其后跟上空间所存储数据的类型即可，如果是多个对象，`[]`中指定对象个数即可。
4. `malloc`的返回值为`void*`，在使用时必须强制类型转换，`new`不需要，因为`new`后跟的是空间的类型。
5. `malloc`申请空间失败时，返回的是`NULL`，隐私使用时必须判空，`new`不需要，但是`new`需要捕获异常。
6. 申请自定义类型对象时，`malloc`/`free`只会开辟空间，不会调用构造函数与析构函数，而`new`在申请空间后会调用构造函数完成对象的初始化，`delete`在释放空间前会调用析构函数完成空间中资源的清理。

以上内容不必死记硬背，看看即可，只有你把本篇文章所讲的内容理解好自然就能将这两组套件的差异了然于胸。这两组套件**最本质的区别还是使用方式以及底层的差别**，只要理解了这点，结合前面的知识想讲出来不是什么难事。

## 内存泄漏

### 概念

由于C/C++的动态内存管理都是提供给用户（程序员）自行申请动态内存和返还动态内存的方式，由用户自行申请和返回动态内存资源，所以这就导致了一个问题，由于种种原因，程序可能会无法正常地返还资源。

演示：

```c++
void errorfunc()
{
	exit(-1);//这里直接退出程序跳过资源释放,代替实际更复杂的情况
}

void test()
{
	int* p1 = (int*)malloc(sizeof(int));
	int* p2 = new int;

	//free(p1);
	//delete p2;
	//忘记释放	代码本身的错误


	int* pa = new int[10];

	errorfunc();//导致程序出现异常的函数
	//由于程序已经出现异常，无法到执行delete[] pa，导致pa指向的资源没被释放，造成程序泄露
	delete[] pa;
}

int main()
{
	test();
	return 0;
}
```

### 危害

以上代码简单演示了内存泄露，但是，这样的代码真的会运行崩溃吗？来看看运行截图：

![image-20230308225919138](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202303082259187.png)

欸？没出现问题哦！这份代码不是向操作系统申请了资源没有返还吗？为什么操作系统不报警？

要解释这个现象需要涉及一些操作系统的知识，展开来讲内容太多了，这里简单解释一下。还记得本篇文章一开头讲的虚拟进程地址空间吗？操作系统为每一个程序提供一个独占内存的假象，程序实际使用的内存是经由虚拟地址映射到实际地址的，而对于一个进程，**当进程正常退出时，操作系统会自动回收这个进程对应的所有资源**，包括虚拟进程地址空间对应的一整块资源。

那么既然如此，内存泄露是不是就没有危害了？并不是，要知道，**并不是所有程序都是像这个程序一样很快就跑完的！**有的程序，例如操作系统，后台服务是需要一直挂着的，像这种程序**基本上很少结束甚至基本不会结束**，对于这样的程序，内存泄露就会导致程序崩溃甚至机器崩溃。

### 如何避免

1. 好的编程习惯，使用配套的内存管理套件，记得释放资源，起码最简单的错误不能犯。
2. 智能指针。
3. 第三方工具。

由于这个话题能谈的东西比较多，就不在本篇博客展开谈了。

# 结语

以上就是C++动态内存管理方式的讲解，希望能帮助到你的C++学习。如果你觉得做的还不错的话还请点赞收藏加分享，当然如果发现我写的有误或者有建议给我的话欢迎在评论区或者私信告诉我。
