# 二叉搜索树 BST

## 概述

### 循关键码访问 key call-by-key

大小比较 与 相等比较

Entry 词条

```c++
template <typename K, typename V> struct Entry { // 词条模板类
  K key; V value; // 关键码、数值
  Entry( K k = K(), V v = V() ) : key(k), value(v) {}; // 默认构造函数
  Entry( Entry<K, V> const & e ) : key(e.key), value(e.value) {}; // 克隆
// 比较器、判等器（从此，不必严格区分词条及其对应的关键码）
  bool operator< ( Entry<K, V> const & e ) { return key < e.key; } // 小于
  bool operator> ( Entry<K, V> const & e ) { return key > e.key; } // 大于
  bool operator==( Entry<K, V> const & e ) { return key == e.key; } // 等于
  bool operator!=( Entry<K, V> const & e ) { return key != e.key; } // 不等
}
```

### 有序性
