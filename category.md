category:
1.添加属性
@property的本质其实是 ivar(实例变量)+getter+setter；
@property有两个对应的词，一个是 @synthesize，一个是 @dynamic;
@synthesize和 @dynamic都没写，那么默认的就是@syntheszie var = _var;
@synthesize表示如果属性没有手动实现setter和getter方法，编译器会自动加上这两个方法。
@dynamic

@dynamic 告诉编译器：属性的 setter 与 getter 方法由用户自己实现，不自动生成。假如一个属性被声明为 @dynamic var，而且你没有提供 @setter方法和 @getter 方法，编译的时候没问题，但是当程序运行到 instance.var = someVar，由于缺 setter 方法会导致程序崩溃；或者当运行到 someVar = var 时，由于缺 getter 方法同样会导致崩溃。编译时没问题，运行时才执行相应的方法，这就是所谓的动态绑定。

category用结构体category_t（在objc-runtime-new.h中可以找到此定义），它包含了
1)、类的名字（name）
2)、类（cls）
3)、category中所有给类添加的实例方法的列表（instanceMethods）
4)、category中所有添加的类方法的列表（classMethods）
5)、category实现的所有协议的列表（protocols）
6)、category中添加的所有属性（instanceProperties）

typedef struct category_t {
const char *name;
classref_t cls;
struct method_list_t *instanceMethods;
struct method_list_t *classMethods;
struct protocol_list_t *protocols;
struct property_list_t *instanceProperties;
} category_t;

那么根本原因又是什么呢？
category 它是在运行期决议的。 因为在运行期即编译完成后，对象的内存布局已经确定，如果添加实例变量就会破坏类的内部布局，这对编译型语言来说是灾难性的。
