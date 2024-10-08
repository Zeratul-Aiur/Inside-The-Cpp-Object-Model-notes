# Data 语意学 The Semantics of Data

- 每一个类对象大小的影响因素：
  - 非静态成员变量的大小。
  - `virtual`特性。
  - 内存对齐。

## 3.2 Data Member 的布局 Data Member Layout

- 非静态成员变量在内存中的顺序和其声明顺序是一致的。
- 但是**不一定是连续的**，因为中间可能有内存对齐的填补物。
- `virtual`机制的指针所放的位置和编译器有关。

### 内存对齐

- 内存对齐可以减少 CPU 访问内存的次数，提高访问速度。

## 3.3 Data Member 的存取

- 静态变量都被放在一个全局区，与类的大小无关，正如对其取地址得到的是与类无关的数据类型。如果两个类有相同的静态成员变量，编译器会暗自为其名称编码，使其两个名称都不同。
- 非静态成员变量则是直接放在对象内，经由对象的地址和在类中的偏移地址取得，但是在继承体系下，情况就会不一样，因为编译器无法确定此时的指针指的具体是父类对象还是子类对象。

## 3.4 “继承” 与 Data Member

- 把**数据放在类中**和**通过继承**的内存布局可能不同，因为每个类需要内存对齐。

## 3.6 指向 Data Members 的指针 Pointer to Data Members

- 虚函数指针通常放在**起始处或尾端**，与编译器有关，C++ 标准允许放在类中的任何位置。
