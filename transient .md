##Hashtable 和 HashMap 的区别

transient 

java语言的关键字，[变量](https://baike.baidu.com/item/%E5%8F%98%E9%87%8F/3956968)[修饰符](https://baike.baidu.com/item/%E4%BF%AE%E9%A5%B0%E7%AC%A6)，如果用transient声明一个[实例变量](https://baike.baidu.com/item/%E5%AE%9E%E4%BE%8B%E5%8F%98%E9%87%8F)，当对象存储时，它的值不需要维持。换句话来说就是，用transient关键字标记的成员变量不参与序列化过程



Hashtable 的初始化

```java
/**
     * Constructs a new, empty hashtable with the specified initial
     * capacity and the specified load factor.
     *
     * @param      initialCapacity   the initial capacity of the hashtable.
     * @param      loadFactor        the load factor of the hashtable.
     * @exception  IllegalArgumentException  if the initial capacity is less
     *             than zero, or if the load factor is nonpositive.
     */
    public Hashtable(int initialCapacity, float loadFactor) {
	if (initialCapacity < 0)
	    throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        if (loadFactor <= 0 || Float.isNaN(loadFactor))
            throw new IllegalArgumentException("Illegal Load: "+loadFactor);

        if (initialCapacity==0)
            initialCapacity = 1;
	this.loadFactor = loadFactor;
	table = new Entry[initialCapacity];
	threshold = (int)(initialCapacity * loadFactor);
    }

    /**
     * Constructs a new, empty hashtable with the specified initial capacity
     * and default load factor (0.75).
     *
     * @param     initialCapacity   the initial capacity of the hashtable.
     * @exception IllegalArgumentException if the initial capacity is less
     *              than zero.
     */
    public Hashtable(int initialCapacity) {
	this(initialCapacity, 0.75f);
    }

    /**
     * Constructs a new, empty hashtable with a default initial capacity (11)
     * and load factor (0.75).
     */
    public Hashtable() {
	this(11, 0.75f);
    }

```



###Hashtable 

​	是线程安全的 ,它的方法是 synchronize的

​	继承的Dictionary 类		实现Map 接口

​	key不可为null

```java
	put(key,value){
		if (value == null) {
	    	throw new NullPointerException();
		}
	}
```



###HashMap 

​	是费线程安全的 ，方法不使用 synchronize

​	继承AbstractMap类，实现Map接口

​	key 可以为null

```java
public V put(K key, V value) {
        if (key == null)
            return putForNullKey(value);
        int hash = hash(key.hashCode());
        int i = indexFor(hash, table.length);
        for (Entry<K,V> e = table[i]; e != null; e = e.next) {
            Object k;
            if (e.hash == hash && ((k = e.key) == key || key.equals(k))) {
                V oldValue = e.value;
                e.value = value;
                e.recordAccess(this);
                return oldValue;
            }
        }

        modCount++;
        addEntry(hash, key, value, i);
        return null;
    }
```

​	去掉了 contains()方法 ,使用的的 containsKey ()和containsValue()



## List 和Map 的区别

​	List 是存储单列数据的集合；Map是存储的是Key和Value的双列数据集合

​	List 存储的数据是有顺序的，并且可以重复；Map 的数据存储是没有数据的，并且不允许Key重复 ，值可以重复

## List 、Set、Map 是否继承Collection 接口

​	List Set 都是继承了Collection 接口

​	Map 就是一个接口。没有继承Collection 

​	