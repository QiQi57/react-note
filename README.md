### react diff 算法 要点：
# 虚拟dom树比较 基于三个策略：
1.dom节点跨层级移动比较少，只对同层的节点进行比较
2.类型相同的节点（组件）总会生成类似的树形结构
3.同一层级子元素根据key比较

# Tree Diff：
两棵树只会对同一层次的节点进行比较。

# component diff (组件间比较)：
1.如果是同类型的组件，则按照策略比较virtual dom 树
2.如果不是同类型组件，unmount 组件
3.shouldComponentUpdate 控制是否需要比较组件

# element diff (元素间的比较)：
当节点处于同一层时，react diff 提供了三种节点操作，INSERT_MARKUP（插入）、MOVE_EXISTING（移动）和 REMOVE_NODE（删除）。

INSERT_MARKUP, 新的component类型不在老的集合里，在新的集合里

MOVE_EXISTING, 新的集合和老的集合 都有component 类型，可更新类型，移动操作，
复用以前节点。

REMOVE_NODE（删除），老的集合有，新的集合没有；或者，新老集合都有，但是类型不同

# 优化方案：
react通过设置唯一key 对 element diff 进行优化
实用 shouldComponentUpdate 控制是否需要比较组件
列表中将最后一个节点 移动到首部，会移动整个列表，应该避免

# 比较算法模拟：
1.有一个list 元素ABCD，展示DEBA，diff算法如何比较的？
2.队列首部插入元素，如何比较的？


-- 官方版本：
两个不同类型的元素会产生不同的树型结构
元素设置key，在重新render时保持稳定

1.根节点比较
根节点类型不同，销毁old tree，重新构建dom树
根节点类型相同，如果属性修改，会更新属性，
递归比较子节点，
使用key提升性能
