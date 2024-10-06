# 构造函数语意学 The Semantics of Constructors

## 2.1 Default Constructor 的构造操作

- 明确什么时候是**程序需要默认构造函数**，什么时候是**编译器需要默认构造函数**。
- 对于`class X`，如果没有程序声明的构造函数，那么会有一个默认构造函数被隐式声明出来。它将是一个`trivial constructor`，是一个什么都不做的构造函数。
- **特殊地**，`Global objects`的内存保证会在**程序启用的时候**被清为0；`Local objects`配置于程序的堆栈中，堆对象配置于自由空间中，都不一定会被清为0，它们的内容将是内存上次被使用后的遗留。

### “带有 Default Constructor” 的 Member Class Object

- 如果一个`class`没有任何`constructor`，但它内含一个`member object`，而后者有`default constructor`，那么这个`class`的`implicit default constructor`就是`nontrivial`，编译器需要为该`class`**合成**出一个`default constructor`。编译器会扩张已存在的`constructors`，在其中安插一些代码，使得`user code`被执行前，先调用必要的`default constructors`。

  ```cpp
  class Foo {
  public:
    Foo();
  };

  class Bar {
  public:
    Foo foo_;
    char *str_;
  }
  ```

  - 这里`Bar`的隐式构造函数会自动调用`Foo`的默认构造函数，但它并不产生任何代码来初始化`Bar::str_`。**初始化`Bar::foo_`是编译器的责任，初始化`Bar::str_`则是程序员的责任。**
  - 如果`Bar`包含多个`member class object`，那么会以`member objects`在`class`中的声明顺序来依次调用。

- 再次注意，**被合成的`default constructor`只满足编译器的需要，而不是程序的需要。**

### “带有 Default Constructor” 的 Base Class

- 同样，如果一个没有任何`constructors`的`class`派生自一个带有`default constructor`的`base class`，那么这个派生类的`default constructor`会被视为`nontrivial`，并因此需要被合成出来。
- 将会根据声明的继承顺序，依次调用其`default constructor`。

### “带有一个 Virtual Function” 的 Class

- 有两种情况:
  - `class`声明或继承一个`virtual function`。
  - `class`派生自一个继承串链，其中有一个或多个`virtual base classes`。
- 编译器也会合成出`default constructor`，以便正确的初始化每一个`class object`的虚函数指针。

### “带有一个 Virtual Base Class” 的 Class

- 不同编译器实现之间存在较大差异。
