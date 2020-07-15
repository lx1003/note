## List、Set、Map三者的区别

- List接口存储一组不唯一可重复，有序的对象
- Set不允许重复的集合，不会有多个元素引用相同的对象
- Map使用键值对存储。Map会维护与Key有关联的值，Key不能重复

## ArrayList与LinkedList区别

1. 是否保证线程安全：ArrayList和LinkedList都是不同步的，不保证线程安全
2. 底层数据结构：ArrayList底层使用的是Object数组；LinkedList底层使用是双向链表数据结构
3. 插入和删除是否受元素位置的影响：ArrayList采用数组存储，所以插入和删除元素的时间复杂度受元素位置的影响，Linked List采用链表存储，所以对add(E e)方法的插入，删除元素时间复杂度不受元素位置的影响
4. LinkedList不支持高效的随机元素访问。而ArrayList支持。快速随机访问就是通过元素的序号快速获取元素对象
5. ArrayList的空间浪费主要体现在在list列表的结尾会预留一定的容量空间，而LinkedList的空间花费则体现在它的每一个元素都需要消耗比ArrayList更多的空间

------

------

## Collection体系

collection包含两大体系：List和Set

List的特点：存取有序，有索引，可以根据索引来进行取值，元素可以重复

Set的特点：存取无序，元素不可以重复

## List：

ArrayList，LinkedList，Vector（已过时）

List集合的特点就是存取有序，可以存储重复的元素，可以用下标进行元素的操作

ArrayList：底层是使用数组实现，查询速度快，增删速度慢

LinkedList：是基于链表结构实现的，所以查询速度慢，增删速度快，提供了特殊的方法，对头尾元素的操作

栈是先进后出，而队列是先进先出

## Set：

元素不重复，存取无需，无下标Set集合有：HashSet，LinkedHashSet，Treeset

在向HashSet集合中存储自定义对象时，为了保证set集合的唯一性，必须重写hashCode和equals方法

### LinkedHashSet

基于链表和哈希表共同实现，存取有序，元素唯一

### TreeSet

存取无序，元素唯一，可以进行排序（排序是在添加的时候进行排序）

TreeSet是基于二叉树的数据结构，二叉树的：一个节点下不能多余两个节点

## Collection体系总结

List:存取有序，元素有索引，元素可以重复

ArrayList：数组结构，查询快，增删慢，线程不安全，因此效率高

Vector：数组结构，查询快，增删慢，线程安全，效率低

LinkedList：链表结构，查询慢，增删快，线程不安全，效率高

Set：存取无序，元素无索引，元素不可以重复

HashSet：存储无序，元素无索引，元素不可以重复，底层是哈希表

LinkedHashSet：存储有序，元素不可以重复

TreeSet：存取无序，可以排序，元素不可以重复

## Map

Map是一个双列集合，其中保存的是键值对，键要求保持唯一性，值可以重复

键值一一对应，一个键只能对应一个值