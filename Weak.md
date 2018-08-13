扫描文件： grep -r -n "prefs:root" ./

#1.weak表其实是一个hash（哈希）表
Key是所指对象的地址，Value是weak指针的地址数组。

#2.weak 的实现原理可以概括一下三步：

2.1、初始化时：runtime会调用objc_initWeak函数，初始化一个新的weak指针指向对象的地址。

2.2、添加引用时：objc_initWeak函数会调用 objc_storeWeak() 函数， objc_storeWeak() 的作用是更新指针指向，创建对应的弱引用表。

2.3、释放时，调用clearDeallocating函数。clearDeallocating函数首先根据对象地址获取所有weak指针地址的数组，然后遍历这个数组把其中的数据设为nil，最后把这个entry从weak表中删除，最后清理对象的记录。

#3.实际操作流程
3.1 objc_initWeak()函数将附有__weak修饰符的变量初始化为0后,
将赋值对象b作为参数调用objc_storeWeak()函数.
objc_storeWeak函数把第二个参数（赋值对象b）的内存地址作为键值key，将第一个参数（weak修饰的属性变量a）的内存地址（&a）作为value，注册到 weak 表中。如果第二个参数（b）为0（nil），那么把变量（a）的内存地址（&a）从weak表中删除
3.2 流程理解
把objc_storeWeak(&a, b)理解为：objc_storeWeak(value, key)，并且当key变nil，将value置nil。

在b非nil时，a和b指向同一个内存地址，在b变nil时，a变nil。此时向a发送消息不会崩溃：在Objective-C中向nil发送消息是安全的。

而如果a是由assign修饰的，则： 在b非nil时，a和b指向同一个内存地址，在b变nil时，a还是指向该内存地址，变野指针。此时向a发送消息极易崩溃
#4释放
(1) 从weak表中获取废弃对象的地址为键值的记录.
(2) 将包含在记录中的所有附有__weak修饰符的变量的地址,赋值为nil.
(3) 从weak表中删除该记录.
(4) 从引用计数表中删除废弃对象的地址为键值的记录.





