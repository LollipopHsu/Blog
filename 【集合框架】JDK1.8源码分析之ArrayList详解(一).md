【集合框架】JDK1.8源码分析之ArrayList详解(一)
================
## 一. 从ArrayList字表面推测
   ArrayList类的命名是由Array和List单词组合而成，Array的中文意思是数组，List的中文意思是列表。从ArrayList字表面推测,ArrayList类是否有数组和列表的特征？那么，这些特征这在ArrayList类中又是怎么体现的？

## ArrayList源码分析

```
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```
从上面的代码可知道，以下几点
 1. 继承了AbstractList类，实现了List，意味着ArrayList是一个数组队列，提供了诸如增删改查、遍历等功能。
 2. 实现了RandomAccess接口，意味着ArrayList提供了随机访问的功能。RandomAccess接口在Java中是用来被List实现，用  来提供快速访问功能的。在ArrayList中，即我们可以通过元素的序号快速获取元素对象。
 3. 实现了Cloneable接口，意味着ArrayList实现了clone()函数，能被克隆。
 4. 实现了java.io.Serializable接口，意味着ArrayList能够通过序列化进行传输。 
## ArrayList的属性
````
    /**
     * Default initial capacity.
     */
    private static final int DEFAULT_CAPACITY = 10;

    /**
     * Shared empty array instance used for empty instances.
     */
    private static final Object[] EMPTY_ELEMENTDATA = {};

    /**
     * Shared empty array instance used for default sized empty instances. We
     * distinguish this from EMPTY_ELEMENTDATA to know how much to inflate when
     * first element is added.
     */
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};

    /**
     * The array buffer into which the elements of the ArrayList are stored.
     * The capacity of the ArrayList is the length of this array buffer. Any
     * empty ArrayList with elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA
     * will be expanded to DEFAULT_CAPACITY when the first element is added.
     */
    transient Object[] elementData; // non-private to simplify nested class access

    /**
     * The size of the ArrayList (the number of elements it contains).
     *
     * @serial
     */
    private int size;
````
 * DEFAULT_CAPACITY ：默认容量大小为10。
 * EMPTY_ELEMENTDATA ：用于Constructs有参数传入，如果参数等于零，则使用该属性。
 * DEFAULTCAPACITY_EMPTY_ELEMENTDATA ：用于Constructs无参数传入默认大小为10（具体运用于add中），使用使用该属性。
 * size ：当前容量大小
 
 ## 构造分析
 ### 有参数构造Method
 传入initialCapacity参数，如果参数大于零，创建一个大小为initialCapacity的数组
 ````
 /**
     * Constructs an empty list with the specified initial capacity.
     *
     * @param  initialCapacity  the initial capacity of the list
     * @throws IllegalArgumentException if the specified initial capacity
     *         is negative
     */
    public ArrayList(int initialCapacity) {
        if (initialCapacity > 0) {
        //new一个大小为initialCapacity的数组
            this.elementData = new Object[initialCapacity];
        } else if (initialCapacity == 0) {
            this.elementData = EMPTY_ELEMENTDATA;
        } else {
            throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        }
    }
 ````
## 无参数构造Method
里面只有一个操作就是把 `elementData` 设置为 `DEFAULTCAPACITY_EMPTY_ELEMENTDATA` 这个空数组。
````
// 无参的构造函数，传入一个空数组  这时候会创建一个大小为10的数组，具体操作在 add 中  
 public ArrayList() {  
 this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;  
 }
````
## 增删查改Method
### add Method
这个方法首先调用了 `ensureCapacityInternal()` 这个方法里面就判断了当前的 `elementData` 是否等于 `DEFAULTCAPACITY_EMPTY_ELEMENTDATA` 如果是的话，就把数组的大小设置为 10 然后进行扩容操作,这里刚好解释了为什么采用无参构造的List 的大小是 10 ，这里扩容操作调用的方法是 `ensureExplicitCapacity` 里面就干了一件事如果用户指定的大小 大于当前长度就扩容，扩容的方法采用了 `Arrays.copy` 方法，这个方法实现原理是 new 出一个新的数组，然后调用 `System.arraycopy` 拷贝数组，最后返回新的数组。
````
public boolean add(E e) {  
 // 当调用了无参构造，设置大小为10  
 ensureCapacityInternal(size + 1);  // Increments modCount   
 elementData[size++] = e;  
 return true;  
}  
  
private void ensureCapacityInternal(int minCapacity) {  
 // 如果当前数组是默认空数组就设置为 10和 size+1中的最小值  
 // 这也就是说为什么说无参构造 new 的数组大小是 10  
 if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {  
 minCapacity = Math.max(DEFAULT_CAPACITY, minCapacity);  
 }  
  
 ensureExplicitCapacity(minCapacity);  
}  
  
private void ensureExplicitCapacity(int minCapacity) {  
 modCount++;  
  
 // 若用户指定的最小容量 > 最小扩充容量，则以用户指定的为准，否则还是 10  
 if (minCapacity - elementData.length > 0)  
 grow(minCapacity);  
}  
  
private void grow(int minCapacity) {  
 // overflow-conscious code  
 int oldCapacity = elementData.length;  
 // 1.5倍增长  
 int newCapacity = oldCapacity + (oldCapacity >> 1);  
 if (newCapacity - minCapacity < 0)  
 newCapacity = minCapacity;  
 if (newCapacity - MAX_ARRAY_SIZE > 0)  
 newCapacity = hugeCapacity(minCapacity);  
 // minCapacity is usually close to size, so this is a win:  
 elementData = Arrays.copyOf(elementData, newCapacity);  
}
````

### Remove Method
通过index知道位置，然后index位置的值被index+1位置的值往前覆盖，覆盖的次数为size - index - 1
````
/**
     * Removes the element at the specified position in this list.
     * Shifts any subsequent elements to the left (subtracts one from their
     * indices).
     *
     * @param index the index of the element to be removed
     * @return the element that was removed from the list
     * @throws IndexOutOfBoundsException {@inheritDoc}
     */
    public E remove(int index) {
        rangeCheck(index);

        modCount++;
        E oldValue = elementData(index);

        int numMoved = size - index - 1;
        if (numMoved > 0)
            System.arraycopy(elementData, index+1, elementData, index,
                             numMoved);
        elementData[--size] = null; // clear to let GC do its work

        return oldValue;
    }
````

### get Method
通过index 来访问元素
````
public E get(int index) {
			//检测范围
            rangeCheck(index);
            checkForComodification();
            return ArrayList.this.elementData(offset + index);
        }
 
````
### set Method
通过index知道要修改的元素并替换了
````
  public E set(int index, E e) {
            rangeCheck(index);
            checkForComodification();
            E oldValue = ArrayList.this.elementData(offset + index);
            ArrayList.this.elementData[offset + index] = e;
           
````





  
 


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM2NzU4NDA3N119
-->