# 字典
Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。   
这种key-value存储方式，在放进去的时候，必须根据key算出value的存放位置，这样，取的时候才能根据key直接拿到value   
* 格式
d = {key1 : value1, key2 : value2 }   (方括号也可以)
### 字典的数据
* 初始指定
如同上述格式
### key
* 通过key放入   
d[key] = value    一个key只能对应一个value，所以，多次对一个key放入value，后面的值会把前面的值冲掉
* key 假如不存在   
dict会报错
* 如何避开key不存在的错误  
一是通过in判断key是否存在     
  key in d      true则存在，false则不存在    
二是通过dict提供的get()方法    
  如果key不存在，可以返回None(交互环境中不显示结果)，或者自己指定的value    
```
>>> d.get(key)
>>> d.get(key, the value)
the value
```
* 删除key
pop(key): d.pop(key)   此key对应的value也会被删除
* 注意
dict内部存放的顺序和key放入的顺序是没有关系的   
dict的查找速度很快，不会随着key的增加而变慢，但是占用的内存会很大   
* dict的Key必须是不可变对象，且不能重复
* 这个通过key计算位置的算法称为哈希算法（Hash）

# 集合
set，集合，和dict类似，也是一组key的集合，但不存储value    
key不能重复，重复的对象会自动过滤不显示
### 相关操作
* 创建一个集合
要创建一个set，需要提供一个list作为输入集合  
  set（[.....]）    
使用大括号 { } 或者 set() 函数创建集合，注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典    
set = {value}    set(value)
* 增加元素
add(key):   s.add(8)    
update(x):  s.update(x)   参数可以是列表，元组，字典等
* 删除元素
remove（key）： s.remove(8)
s.discard(x):   也是移除集合中的元素，且如果元素不存在，不会发生错误
s.pop() : 随机删除
### 运算
set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作：
* 交集&：
s1 & s2  
{2, 3}  
* 并集|：
 s1 | s2  
{1, 2, 3, 4} 
* 集合s1中包含而集合s2中不包含的元素
s1 - s2   
{'r', 'd', 'b'}   
* 不同时包含于a和b的元素
s1 ^ s2    

* 集合推导式(Set comprehension)
>>> a = {x for x in 'abracadabra' if x not in 'abc'}    
>>> a    
{'r', 'd'}    

### 相关操作
* 集合元素个数  
len(s)
* 清空集合  
s.clear()
* 判断元素是否在集合中存在  
  x in s  ： true，false
* copy()	拷贝一个集合  
x = y.copy()
* difference()	返回多个集合的差集  
返回一个集合，元素包含在集合 x ，但不在集合 y   
z = x.difference(y)    
* difference_update()	移除两个集合中都存在的元素  
x.difference_update(y)    

*difference_update() 方法与 difference() 方法的区别在于 difference() 方法返回一个移除相同元素的新集合，而 difference_update() 方法是直接在原来的集合中移除元素，没有返回值。

* intersection()	用于返回两个或更多集合中都包含的元素，即交集   
set.intersection(set1, set2 ... etc)

* intersection_update()	返回集合的交集。  
set.intersection_update(set1, set2 ... etc)   
*intersection_update() 方法不同于 intersection() 方法，因为 intersection() 方法是返回一个新的集合，而 intersection_update() 方法是在原始的集合上移除不重叠的元素。  

* isdisjoint()	判断两个集合是否包含相同的元素，如果没有返回 True，否则返回 False。  
z = x.isdisjoint(y)  

* issubset()	判断指定集合是否为该方法参数集合的子集。  
z = x.issubset(y)   返回true，false

* issuperset()	判断该方法的参数集合是否为指定集合的子集  
z = x.issuperset(y)    返回true，false

* symmetric_difference()	返回两个集合组成的新集合，但会移除两个集合的重复元素   
z = x.symmetric_difference(y)

* symmetric_difference_update()	移除当前集合中在另外一个指定集合相同的元素，并将另外一个指定集合中不同的元素插入到当前集合中。  
x.symmetric_difference_update(y) 在原始集合 x 中移除与 y 集合中的重复元素，并将不重复的元素插入到集合 x 中  

* union()	返回两个集合的并集，即包含了所有集合的元素，重复的元素只会出现一次  
z = x.union(y)   
set.union(set1, set2...)   


* 集合和字典都不能放入可变对象   


### 帮助理解的相关知识——来自网友

* dict则为了快速查找使用了一种特别的方法，哈希表。哈希表采用哈希函数从key计算得到一个数字（哈希函数有个特点：对于不同的key，有很大的概率得到的哈希值也不同），然后直接把value存储到这个数字所对应的地址上，比如key='ABC'，value=10，经过哈希函数得到key对应的哈希值为123，那么就申请一个有1000个地址（从0到999）的内存，然后把10存放在地址为123的地方。类似的，对于key='BCD'，value=20，得到key的哈希值为234，那么就把20存放在地址为234的地方。对于这样的表查找起来是非常方便的。只要给出key，计算得到哈希值，然后直接到对应的地址去找value就可以了。无论有几个元素，都可以直接找到value，无需遍历整个表。不过虽然dict查找速度快，但内存浪费严重，你看我们只存储了两个元素，都要申请一个长度为1000的内存。

* 现在你知道为啥key要用不可变对象了吧？因为不可变对象是常量，每次的哈希值算出来都是固定的，这样就不会出错。比如key='ABC'，value=10，存储地址为123，假设我突发奇想，把key改成'BCD'，那么当查找'BCD'的value的时候就会去234的地址找，但那里啥也没有，这就乱套了。

* 你看我们上面有一句话：对于不同的key，有很大的概率得到的哈希值也不同。那么有很小的概率不同的key可以得到相同的哈希值了？没错，比如对于我们的例子来说，哈希值只有3位，那么只要元素个数超过1000，就一定会有至少两个key的哈希值相同（鸽笼原理），这种情况叫“冲突”，设计哈希表的时候要采取办法减少冲突，实在冲突了也要想办法补救。不过这是编译器的事情






























