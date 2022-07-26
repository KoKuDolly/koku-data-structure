# red-black-tree

## 红黑树的动机

总结的说：为了具备对历史版本的访问，实现 Persistent structrure ，引入了平衡树，AVL的删除操作无法做到常量级，所以引出了红黑树。

线性结构：向量、列表、栈、队列

半线性结构：树

非线性结构：图

都属于是 ephemeral 结构，状态稍纵即逝。

Persistent structrure：支持对历史版本的访问

T.search(ver, key); T.insert(ver, key); T.remove(ver, key);

蛮力实现：每个版本独立保存；各版本入口自成一格搜索结构

单次操作（logh + logn），累计h*n 时间/空间  h = |history|

挑战：可否将复杂度控制在 (n + h*logn)

可以： 相邻版本之间的关联性

08XA1-4 O(1)重构

**关联性**：大量共享，少量更新：每个版本的新增复杂度为 logn

能否进一步提高，比如总体O(n+h)、单版本O(1)?可以

**就树形结构拓扑而言，相邻版本之间的差异不能超过O(1) 常数级别**

AVL insert 操作 满足 O(1) remove 操作 Ologn

红黑树 的 insert remove 可以满足 O(1) 常数级别的要求

## 红黑树的结构

BBST 二叉搜索树

lifting 上浮 提升  -> 提升变换

末端结点

(2, 4) 4 阶的 B 树 == 红黑树

平衡性 
定理：包含n个内部结点的红黑树T，高度h=O(logn)

$\log_2{(n+1)}$ $\leq$ h $\leq$ 2*$\log_2{(n+1)}$

若 T 高度为 h，黑高度为H，则 h = R + H <= 2H

若T所对应的B树为$T_B$，则H即是$T_B$的高度

$T_B$的每个结点，包含且仅包含T的一个黑结点

于是 H $\leq$ $log_[4/2]{\frac{n+1}{2}+1}$ $\leq$ $log_2{(n+1)}$

### 接口定义 C++

```c++
template <typename T> class RedBlack : public BST<T> {
  public: // BST::search()等其余接口可直接沿用
             BinNodePosi(T) inert( const T & e ); // 插入（重写）
             bool remove( const T & e ); // 删除（重写）
  protected: void solveDoubleRed( BinNodePosi(T) x ); // 双红修正
             void solveDoubleBlack( BinNodePosi(T) x ); // 双黑修正
             int updateHeight ( BinNodePosi(T) x ); // 更新结点x的高度（黑高度）
};
template <typename T> int RedBlack<T>::updateHeight( BinNodePosi(T) x ) {
  x->height = max( stature( x->lc ), stature( x->rc ) );
  if ( IsBlack( x ) ) x->height++; return x->height; // 只计黑结点
}
```
