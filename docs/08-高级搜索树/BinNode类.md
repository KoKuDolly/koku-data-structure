# BinNode类

```c++
#define BinNodePosi(T) BinNode<T>*

template <typename T> struct BinNode {
  BinNodePosi(T) parent, lChild, rChild; // 父亲 孩子
  T Data; int height; int size(); // 高度 子树规模
  BinNodePosi(T) insertAsLC( T const & ); // 作为左孩子插入新节点
  BinNodePosi(T) insertAsRC( T const & ); // 作为右孩子插入新节点
  BinNodePosi(T) succ(); // （中序遍历意义下）当前节点的直接后继
  template <typename VST> void travLevel( VST & ); // 子树层次遍历
  template <typename VST> void travPre( VST & ); // 子树先序遍历
  template <typename VST> void travIn( VST & ); // 子树中序遍历
  template <typename VST> void travPost ( VST & ); // 子树后序遍历
}
```
