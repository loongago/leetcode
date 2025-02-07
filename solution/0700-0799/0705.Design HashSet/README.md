# [705. 设计哈希集合](https://leetcode-cn.com/problems/design-hashset)

[English Version](/solution/0700-0799/0705.Design%20HashSet/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->
<p>不使用任何内建的哈希表库设计一个哈希集合</p>

<p>具体地说，你的设计应该包含以下的功能</p>

<ul>
	<li><code>add(value)</code>：向哈希集合中插入一个值。</li>
	<li><code>contains(value)</code> ：返回哈希集合中是否存在这个值。</li>
	<li><code>remove(value)</code>：将给定值从哈希集合中删除。如果哈希集合中没有这个值，什么也不做。</li>
</ul>

<p><br>
<strong>示例:</strong></p>

<pre>MyHashSet hashSet = new MyHashSet();
hashSet.add(1); &nbsp; &nbsp; &nbsp; &nbsp; 
hashSet.add(2); &nbsp; &nbsp; &nbsp; &nbsp; 
hashSet.contains(1); &nbsp;&nbsp;&nbsp;// 返回 true
hashSet.contains(3); &nbsp;&nbsp;&nbsp;// 返回 false (未找到)
hashSet.add(2); &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
hashSet.contains(2); &nbsp;&nbsp;&nbsp;// 返回 true
hashSet.remove(2); &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
hashSet.contains(2); &nbsp;&nbsp;&nbsp;// 返回  false (已经被删除)
</pre>

<p><br>
<strong>注意：</strong></p>

<ul>
	<li>所有的值都在&nbsp;<code>[0, 1000000]</code>的范围内。</li>
	<li>操作的总数目在<code>[1, 10000]</code>范围内。</li>
	<li>不要使用内建的哈希集合库。</li>
</ul>

## 解法

<!-- 这里可写通用的实现逻辑 -->

数组实现。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class MyHashSet:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.data = [False] * 1000001

    def add(self, key: int) -> None:
        self.data[key] = True

    def remove(self, key: int) -> None:
        self.data[key] = False

    def contains(self, key: int) -> bool:
        """
        Returns true if this set contains the specified element
        """
        return self.data[key]



# Your MyHashSet object will be instantiated and called as such:
# obj = MyHashSet()
# obj.add(key)
# obj.remove(key)
# param_3 = obj.contains(key)
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

- 可以一次性开辟一个大的数组，存放所有元素。

```java
class MyHashSet {

    private boolean[] data;

    /** Initialize your data structure here. */
    public MyHashSet() {
        data = new boolean[1000001];
    }

    public void add(int key) {
        data[key] = true;
    }

    public void remove(int key) {
        data[key] = false;
    }

    /** Returns true if this set contains the specified element */
    public boolean contains(int key) {
        return data[key];
    }
}

/**
 * Your MyHashSet object will be instantiated and called as such:
 * MyHashSet obj = new MyHashSet();
 * obj.add(key);
 * obj.remove(key);
 * boolean param_3 = obj.contains(key);
 */
```

- 也可以开辟一个大小为 `SIZE` 的数组，数组的每个位置是一个链表。

```java
class MyHashSet {

    private static final int SIZE = 1000;
    private LinkedList[] data;

    /** Initialize your data structure here. */
    public MyHashSet() {
        data = new LinkedList[SIZE];
        Arrays.fill(data, new LinkedList<Integer>());
    }

    public void add(int key) {
        int index = hash(key);
        Iterator<Integer> iterator = data[index].iterator();
        while (iterator.hasNext()) {
            Integer e = iterator.next();
            if (e == key) return;
        }
        data[index].addFirst(key);
    }

    public void remove(int key) {
        int index = hash(key);
        ListIterator<Integer> iterator = data[index].listIterator();
        while (iterator.hasNext()) {
            Integer e = iterator.next();
            if (e == key) iterator.remove();
        }
    }

    /** Returns true if this set contains the specified element */
    public boolean contains(int key) {
        int index = hash(key);
        Iterator<Integer> iterator = data[index].iterator();
        while (iterator.hasNext()) {
            Integer e = iterator.next();
            if (e == key) return true;
        }
        return false;
    }

    private int hash(int key) {
        return key % SIZE;
    }
}

/**
 * Your MyHashSet object will be instantiated and called as such:
 * MyHashSet obj = new MyHashSet();
 * obj.add(key);
 * obj.remove(key);
 * boolean param_3 = obj.contains(key);
 */
```

### **...**

```

```

<!-- tabs:end -->
