## 查找

### 1. 基本概念

- 分类

  > 查找分为静态查找表和动态查找表。

- 平均查找长度

  > 为确定记录在查找表中的位置，需和给定关键字进行比较的次数的期望值称为查找算法在查找成功时的平均查找长度。简单的理解就是找到目标值时，遍历了查找表中多少个元素

### 2. 静态查找表

#### 2.1 顺序查找

> 定义：从表的一端开始逐个比较。
>
> 平均查找长度：`ASL = (n+1)/2`
>
> 优缺点：缺点是在n较大时，平均查找长度比较大。优点是适应面广，简单，对查找表没什么要求。

#### 2.2 折半查找

> 定义：查找表存储在一维数组中，表中元素按递增/递减排序。然后先让关键字和表中中间的元素比较，若相等则返回，否则根据关键字和该中间元素的大小决定从哪边继续查找。
>
> 平均查找长度：`ASL = (n+1)/nlog(n+1) - 1`，当n较大时，ASL约等于`log(n+1) - 1`
>
> 优缺点：优点是效率高，缺点是对查找表的要求比较高(递增或递减)，当需要对表进行插入或删除时，需要移动大量的元素，所以折半查找适用于表不易变动，且又经常进行查找的情况。

#### 2.3 分块查找

>定义：首先将表分成若干块，每一块的关键字不一定有序，但块之间是有序的，即后一块中所有记录的关键字均大于前一块中最大的关键字。
>
>平均查找长度为ASL = (n/s+s)/2 + 1。
>
>优缺点：平均查找长度介于顺序查找和折半查找之间

### 3. 动态查找表

动态查找表的特点是表结构本身是在查找过程中动态生成的，即对于给定值key，若表中存在关键字key的记录，则查找成功；否则插入关键字为key的记录。

#### 3.1 二叉排序树（BST）

左孩子<根<右孩子

- 二叉排序树的查找节点过程：先将关键字key与二叉排序树的根节点比较，若等于，则返回根节点；若key<root.data，则从左子树中再次寻找；否则在右子树中查找。
- 二叉排序树的插入节点过程：首先是根据查找过程找到newKey要插入的位置，比如它应该插入作为f节点的左孩子p，那么就应该执行操作p.lchild = f.lchild，f.lchild = p;
- 二叉排序树的删除节点过程：首先是找到要删除的节点所在的位置，然后根据要删除的节点是叶子节点，还是只有左孩子或是右孩子或是其他情况来进行具体的操作。

#### 3.2 平衡二叉树（AVL）

左子树的和右子树的高度之差的绝对值不超过1。所以，若将二叉树结点的平衡因子定义为该结点左子树的高度减去右子树的高度，则平衡二叉树上所有结点的平衡因子只可能是-1、0和1。只要有一个结点的平衡因子的绝对值大于1，那么就不是平衡二叉树。

- 平衡二叉树的插入操作

  - LL型单向右旋平衡处理。若要插入的结点是在A结点的左子树的左孩子处，并且会出现失衡，那么就要进行向右的顺时针旋转操作。
  - RR型单向左旋平衡处理。若要插入的结点是在A结点的右子树的右孩子处，并且会出现失衡，那么就要进行向左的逆时针旋转操作。
  - LR型先左后右双向旋转平衡处理。即在A结点的左子树的右孩子处插入，那么就要进行先左旋后右旋。
  - RL型先右后左双向旋转平衡处理。即在A结点的右子树的左孩子处插入，那么就要进行先右旋后左旋。

- 平衡二叉树的删除操作

  略

#### 3.3 B_树

略

### 4. 哈希表

根据设定的哈希函数H(key)和处理冲突的方法，将一组关键字映射到一个有限的连续的地址集（区间）上，并以关键字在地址集中的“像”作为记录在表中的存储位置，这种表称为哈希表，这一映射过程称为哈希造表或散列，所得的存储位置称为哈希地址或散列地址。

对于哈希表，主要考虑两个问题：如何构造哈希函数和如何解决冲突。

#### 4.1 哈希函数的构造方法

> 常用的哈希函数构造方法有直接定址法、数字分析法、平方取中法、折叠法、随机数法和除留余数法等。

#### 4.2 处理冲突的方法

- 开放定址法
- 链地址法（常用）。对于发生冲突时，将同一哈希值的关键字存储为链表
- 再哈希法。即在同义词发生地址冲突时计算另一个哈希函数地址，直到冲突不再发生。
- 建立一个公共溢出区。一旦发生冲突，都填入到公共溢出区中。

#### 4.3 哈希表的查找

哈希查找的特点

- 由于有哈希冲突的存在，所以仍需以平均查找长度衡量哈希表的查找效率。
- 装填因子：a = 表中装入的记录数/哈希表的长度。