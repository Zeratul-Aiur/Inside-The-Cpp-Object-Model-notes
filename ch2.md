# 构造函数语意学 The Semantics of Constructors

## Default Constructor 的构造操作

明确什么时候是**程序需要默认构造函数**，什么时候是**编译器需要默认构造函数**。

对于`class X`，如果没有用户声明的构造函数，那么会有一个默认构造函数被隐式声明出来。它将是一个`trivial constructor`，是一个什么都不做的构造函数。

**特殊地**，`Global objects`的内存保证会在程序启用的时候被清为0；`Local objects`配置于程序的堆栈中，堆对象配置于自由空间中，都不一定会被清为0，它们的内容将是内存上次被使用后的遗留。
