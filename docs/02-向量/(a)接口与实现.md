# Vector 向量

Abstract Data Type vs. Data Structure

抽象数据类型 = 数据模型 + 定义在该模型上的一组操作

              抽象定义     外部的逻辑特性        操作&语义
              
              一种定义     不考虑时间复杂度      不涉及数据的存储方式

数据结构 = 基于某种特定语言，实现ADT的一整套算法

           具体实现         内部的表示与实现     完整的算法
           
           多种实现         与复杂度密切相关     要考虑数据的具体存储机制

ADT + implementation

## vector ADT

从数组到向量

linear array

向量是数组的抽象与泛化，由一组元素按线性次序封装而成

各元素与\[0, n)内的秩（rank）一一对应    // 循秩访问（call-by-rank）

元素的类型不限于基本类型

操作、管理维护更加简化、统一与安全

可更为便捷地参与复杂数据结构的定制与实现

### 向量ADT接口

| 操作          | 功能                                               | 适用对象 |
| ------------- | -------------------------------------------------- | -------- |
| size()        | 报告向量当前的规模（元素总数）                     | 向量     |
| get(r)        | 获取秩为r的元素                                    | 向量     |
| put(r, e)     | 用e替换秩为r元素的数值                             | 向量     |
| insert(r, e)  | e作为秩为r元素的插入，原后继元素依次后移           | 向量     |
| remove(r)     | 删除秩为r的元素，返回该元素中原存放的对象          | 向量     |
| disordered()  | 判断所有元素是否已按非降序排列                     | 向量     |
| sort()        | 调整各元素的位置，使之按非降序排列                 | 向量     |
| find(e)       | 查找目标元素e                                      | 向量     |
| search(e)     | 查找目标元素e，返回不大于e且秩最大的元素           | 有序向量 |
| deduplicate() | 剔除重复元素                                       | 向量     |
| uniquify()    | 剔除重复元素                                       | 有序向量 |
| traverse()    | 遍历向量并统一处理所有元素，处理方法由函数对象指定 | 向量     |

### ADT 操作

### 构造与析构

vector 模板类

```c++
Vector(int c = DEFAULT_CAPACITY)
  { _elem = new T[_capacity = c]; _size = 0; } // 默认
  
Vector(T const * A, Rank lo, Rank hi) // 数组区间复制
  { copyFrom(A, lo, hi); }
  
Vector(Vector<T> const & V, Rank lo, Rank hi)
  { copyFrom(V._elem, lo, hi); } // 向量区间复制

Vector(Vector<T> const & V)
  { copyFrom(V._elem, 0, V._size); } // 向量整体复制
  
// 析构
~Vector() { delete [] _elem; } // 释放内部空间
```

### 复制 copyFrom

```c++
template <typename T> // T为基本类型，或已重载赋值操作符'='
void Vector<T>::copyFrom(T* const A, Rank lo, Rank hi) {
  _elem = new T[_capacity = 2*(hi - lo)]; // 分配空间
  _size = 0; // 规模清零
  while (lo < hi) // A[lo, hi) 内的元素逐一
    _elem[_size++] = A[lo++]; // 复制至_elem[0, hi-lo)
}
```
