# 可扩充向量

```c++
template <typename T>
void Vector<T>::expand() { // 向量空间不足时扩容
  if (_size < _capacity) return; // 尚未满员时，不必扩容
  _capacity = max(_capacity, DEFAULT_CAPACITY); // 不低于最小容量
  T* oldElem = _elem; _elem = new T[_capacity <<= 1]; // 容量加倍
  for (int i = 0; i < _size; i++) // 复制原向量内容
    _elem[i] = oldElem[i]; // T为基本类型，或已重载赋值操作符'='
   delete [] oldElem; // 释放原空间
}
```

得益于向量的封装，尽管扩容之后数据区
