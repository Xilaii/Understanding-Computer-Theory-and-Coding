1. **许多问题是以递归形式描述的，往往也可以用递归形式来解决，但之所以在描述问题和提出解决思路时选用递归，仅仅是因为对于人类来说，递归的语义更清晰，便于理解；然而，当编程解决这些问题时，用迭代去实现往往远远比递归实现更高效，主要有两个原因：**
    1. **递归的运行成本高**，递归涉及到十分频繁的函数调用和返回，相应地需要频繁的现场保护和恢复、栈帧的增长和弹出，同时，如果其中包含 C++ 对象，还会有大量对象的构造函数和析构函数的调用，这些隐含的运行成本在递归深入时会越来越成为负担
    2. **递归会导致大量重复运算**，各个递归分支之间相互独立，某递归分支已经运算出的结果，其余分支并不知情，而是各自做各自的运算，运算的中间结果不能共享，因此递归存在大量的重复运算，并且这些重复运算随递归深度呈指数规模增长，造成极其可观的 overhead，这是递归低效的主要原因
    + 综上，对于能够用迭代形式实现的程序，应该尽量用迭代，避免递归

2. **程序占用内存太多可能会因此而降低所有进程的运行效率，因为代码膨胀会导致额外的 paging，降低指令 cache 的命中率**

3. **平均而言，一个程序执行时间的80%会花在20%的代码上**

4. **什么是工厂函数(factory function)？**
    + factory 要解决的问题是，希望能创建一个对象，但创建过程比较复杂，希望对外隐藏这些细节
    + 不管用什么语言，创建什么资源，当开始为"创建"本身写代码时，就是在用"工厂模式"了
    + 至于工厂函数，就是基于工厂模式编写的用于创建对象的函数

5. **堆是灵活管理空间的唯一选择**

6. **字符串和字符不是同一类型**
	+ 字符串在表达式中的返回值是首字符地址
	+ 而字符返回的是字符

7. **要养成所有指针在使用前都先检查其是否为野指针的习惯**

8. **将整数直接赋给指针并非不可实现，但是由于正常情况下这种操作很少见，编译器会将其定义为错误以提示我们**

9. **数组名和指针的关系**
    1. 数组名的值是数组首个元素的地址，此时数组名可以当做一个指针常量使用
	    + 是指针常量，而不是指针变量，因此对数组名赋值是不允许的
	2. 数组名不只是一个指针常量，它还包括数组长度等属性
	    + 这些属性应该是由编译器在编译阶段维护的，以防出错

10. **多维数组的元素是数**
	+ 多维数组在作为形参时，必须指定较低维度的长度，因为多维数组与数组不同，它不仅有长度，还有"形状"信息

11. **malloc 是从内存池中提取一块连续的可用内存**
    + malloc 返回的指针无类型，因此可以将其强制转换为其他类型
	+ malloc 输入参数只有 size，因此需要计算尺寸
	+ malloc 分配内存存在失败的可能（比如内存池太小），因此有必要在使用前检查是否成功

12. **数组的长度究竟可不可以在运行时再确定？**
    + 两种情况：
	    + 位于静态存储区的数组，其长度必须在声明时期就指定，而不能在运行时才确定，因为静态存储区的内容是先于程序运行就初始化好了的
		+ 位于运行时栈上的数组，其长度可以在运行时再确定，因为栈上的空间原本就是灵活的，根据需要增长对应的尺寸即可

13. **C 语言函数只能返回标量值，而不能返回数组**
    + 这一点与 Python 大不相同
	+ 结构体属于标量类型
	+ 若实在想要返回数组，可以将其封装在结构体中再传递

14. **什么叫格式化的输入/输出和未格式化的输入/输出？**
    + 两种形式都用于操纵字符串，区别在于后只是简单地将流按字符串格式读入，而前者执行数字和其他变量的内部和外部表示形式之间的转换

15. **C 语言函数中的可选参数的原理是什么？**
	+ 本质上就是利用一个基准参数，再结合类型不断从这个基准参数往栈的下面寻找下一个，由于下一个地址需要结合当前的类型来确定，因此必须要进行格式化，这一格式化的过程由 va\_list, va\_start, va\_end 来辅助
	+ 对于可变参数，传入的所有参数都会被压入栈中，不管是否会被处理，没有方法能知道实际到底传入了多少参数

16. **unsigned 存在的意义是什么？**
	+ unsigned 与 signed 的区别在于符号位的解析，在 C 中所有数据默认都是 signed，也就是带符号位
	+ 此外在赋值时，如果存在字长增加，例如 int -> long，signed 会进行高位填充，而 unsigned 则不会

17. **当一个字符串常量出现在表达式中时，其值为指针常量。**
	+ 编译器把这些字符的一份拷贝存储在内存的某个位置(通常是常量存储区），并用指针指向之

18. **指针还可以指向函数，但在将这种函数指针初始化之前要知道其原型**
	+ int (\*pf)(int) = &f;
	+ &操作符是可选的，因为函数名被使用时总是由编译器把它转化为函数指针，&操作符只是显式地说明了这一任务
	+ 其实在运行时，调用某个函数就是跳转，因此函数名的本质就是地址，而函数原型则是决定了参数传递方式；调用函数所需要的信息无非是三个：指令跳转地址（好知道往哪里跳转）、参数（好知道怎样增长栈）、返回值类型（好知道怎样为返回值安排栈空间），而函数指针+函数原型就包含了所有这些需要的信息
	+ 其实 C++ 中的多态就是基于函数指针来实现的，每个对象携带的虚函数表指针指向的虚函数表里储存的就是各个虚函数的函数指针

19. **怎样知道数组是否越界？数组的长度信息存储在哪里？**
	+ 程序并不知道是否越界，要程序员自己清楚，有时候会报"数组越界"的错，是因为编译器提供了辅助功能，运行时并无法得知

20. **类型转换有两种，一种是将值的精度调整后新建一个变量，另一种是直接原样赋复制，但是改变其解析方式，例如 C++ 的 reinterpret\_cast**

21. **完全二叉树有一绝大好处：若用数组形式存储，每个节点都可以方便地计算出其父节点的位置（很方便），也可以直接计算出子节点的位置**

22. **表示算法复杂度的方法不止 Big-Oh 一种，还有诸如 Big-Omega、Big-Theta、Little-Oh 等，Big-Oh 虽然是最常用的，但它并不适合用在小数据量的情况下**

23. **单向链表相对于双向链表有两大劣势：**
	+ 对于双向链表，可以通过每一个节点找到其他所有节点，而单向链表必须从头开始往后找
	+ 对于"往某个元素前插入元素"这一操作，单向链表的效率很低

24. **short 是指两个字节长度的数据类型**


