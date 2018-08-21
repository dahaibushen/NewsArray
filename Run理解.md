动态运行时的理解：
尽量把决定从编译器推迟到运行期处理；
在运行的时候才会去确定对象的类型跟方法。因此可以再程序运行时动态的修改类和对象中的所有属性跟方法；
 run time ：
1.类的各个方面的动态配置
2.消息传递

struct objc_class {
Class isa  OBJC_ISA_AVAILABILITY;
#if !__OBJC2__
Class super_class;//父类
const char *name;//类名
long version;//类的版本信息，默认为0
long info;//类信息，供运行期使用的一些位标识
long instance_size;//类的实例变量大小
struct objc_ivar_list *ivars;// 类的成员变量链表
struct objc_method_list **methodLists;// 方法链表
struct objc_cache *cache;//方法缓存
struct objc_protocol_list *protocols;//协议链表#
endif} 

OBJC2_UNAVAILABLE;
