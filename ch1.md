# 关于对象 Object Lessons

## 加上封装后的布局成本 Layout Costs for Adding Encapsulation

`Zero-cost abstraction`最关键的地方是`Don't pay for things you don't use`。它在于可以为你提供代码的抽象，而不加额外的负担。

`C++`被称为`Zero-cost abstraction`，某种程度上，这代表着你可以定义`class`，也可以把`class`转化分离为你熟悉的`struct`与一系列算法。而定义`class`这样的抽象，与你手动这样写相比，并非增加额外的精力与开销：

```cpp
struct Point3D {
  float x;
  float y;
  float z;
}

float x,y,z;
```

当然`Point3D`是一个`POD(Plain Old Data)`。实现上更多是包含继承，甚至泛型等，这些也并不增加运行时成本。

真正增加空间和时间等成本的是由`virtual`引起的：

- Virtual function：支持高效的运行期多态。
- Virtual base class：虚继承。例如被菱形方式继承的`base class`。

## C++ 对象模型 The C++ Object Model
