此部分较为精简，只供面试前联想记忆使用，需要先熟读相关的内容知识才能发挥其作用。推荐书籍《STL源码剖析》（侯捷）。

六大组件及其关系 
空间配置器、容器、迭代器、算法、仿函数、适配器

内存管理：内存配置和对象构造/析构分开。 
使用双层级配置器：第一级直接 malloc，free；第二级内存池（维护 16 个自由链表）

迭代器：一种智能指针

Vector： 动态分配的数组，连续线性空间； 
维护 3 个迭代器：start，finish，end_of_storage 
无备用空间->若为 0，配置为 1，否则配置为 2 倍 
需要重新配置、移动数据、释放原空间，所以迭代器失效

List：环状的双向链表，尾部有空白节点（为满足左闭右开），节点不保证连续存在，迭代器不失效。内部有一个 last 迭代器指向尾端空白节点（其 next 为 begin 迭代器）。 
List 不能使用算法 sort（只接受随机存取迭代器），它有自己内置的 sort。

Deque：双向开口的连续线性空间，没有容量概念，动态地以分段连续空间组合而成， 随时可增加新空间并链接起来（伪连续，负担落在迭代器身上） 
使用中控器 map，存的指针，指向实际存储块 
迭代器失效： 
a. 在deque容器首部或者尾部插入元素不会使得任何迭代器失效； 
b. 在其首部或尾部删除元素则只会使指向被删除元素的迭代器失效； 
c. 在deque容器的任何其他位置的插入和删除操作将使指向该容器元素的所有迭代器失效。

优先队列：使用最大堆实现，用 vector 存储。

Set：红黑树实现，自动排序，key=value，不允许相同的 key，不能通过迭代器改变元素 的值，insert，erase 不影响迭代器。

Map：红黑树实现，自动排序，元素为 pair，不允许相同 key，key 不可改，value 可改， 迭代器不失效。

Multiset：key 可重复，使用 insert_equal()而不是 insert_unique()

Hash：没有自动排序，使用开链法解决冲突，以质数计算桶个数，预先计算好 28 个质 数并存储，需要的时候查找“最接近某数并大于某数”的质数。 
插入时可能进行表格重建（元素个数>桶个数，避免单个桶太长），找下一个质数，设立 新的 vector。 
对每个旧桶，找出节点落在哪一个新桶里，最后交换新旧 vector，释放旧空间。 
解决冲突的方法： 
线性探测 
二次探测 
随机探测 
双重哈希 
再哈希 
拉链法

红黑树 O(log n)：1. 节点非红即黑，2. 根为黑，3. 红子必黑，4. NULL 为黑，5. 任一 节点到 null 的任何路径所含黑节点数相同。
由规则 5，新增节点为红，由规则 3，其父节点为黑（否则需要调整） 
要点：若父为红，检查叔叔节点（特殊情况：空树） 
非严格平衡：以牺牲 search 为代价，rebalance 快（旋转次数少）。

仿函数：函数对象，重载了 operator() 
不用函数指针：1.抽象性要求； 2.函数指针无法和 STL 其他组件搭配产生灵活变化。
