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
