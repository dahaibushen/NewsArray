1.例子：
int val = 10;
void (^blk)(void) = ^{ printf("val=%d\n",val);
                               }; 
val = 2; 
blk();
结果为10；
原因：block 在实现时就会对它引用到的它所在方法中定义的栈变量进行一次只读拷贝，然后在 block 块内使用该只读拷贝；换句话说block截获自动变量的瞬时值；或者block捕获的是自动变量的副本。

2.例子：
__block int val = 10; void (^blk)(void) = ^{printf("val=%d\n",val);};
val = 2;
blk();
结果为2；
3.循环引用问题
3.1确认当前对象A是否引用了Block ,而Block又是否引用了对象A；
4.block类型
4.1 全局数据区的block对象
void (^blk)(void) = ^{
NSLog(@"Global Block");
};
blk();
NSLog(@"%@", [blk class]);
理解： 无引用外部变量，运行时也无须外部变量参与，块所使用的整个内存区域，在编译期就已经确定

4.2   堆上block对象
4.3   栈上block对象
4.4   全局块不引用外部变量，所以不用考虑。
        堆块引用的外部变量，不是原始的外部变量，是拷贝到堆中的副本。
        栈块本身就在栈中，引用外部变量不会拷贝到堆中。
