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

BST: 结点 ~ 词条 ~ 关键码

顺序性：任一结点均不小于/不大于其左/右后代

为简化起见，禁止重复词条

这种简化，应用中不自然，算法中不必要

### 单调性

中序遍历，单调非降

微观 顺序性 宏观 单调性

### 接口

```c++
template <typename T> class BST : public BinTree<T> {// 由BinTree派生
  public: // 以 virtual 修饰，以便派生类重写
    virtual BinNodePosi(T) & search( const T & ); // 查找
    virtual BinNodePosi(T) insert( const T & ); // 插入
    virtual bool remove( const T & ); // 删除
  protected:
    BinNodePosi(T) _hot; // 命中结点的父亲
    BinNodePosi(T) connect34( // 3 + 4 重构
      BinNodePosi(T), BinNodePosi(T), BinNodePosi(T),
      BinNodePosi(T), BinNodePosi(T), BinNodePosi(T), BinNodePosi(T));
    BinNodePosi(T) rotateAt( BinNodePosi(T) ); // 旋转调整
};
```
