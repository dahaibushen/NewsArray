
ios 双缓冲机制，前帧缓存 后帧缓存 缓存好了才会指向该地址；
APP的冷启动概括为三大阶段



dyld，Apple的动态链接器，可以用来装载Mach-O文件（可执行文件、动态库等）



启动APP时，dyld所做的事情有

1.装载APP的可执行文件，同时会递归加载所有依赖的动态库

2.当dyld把可执行文件、动态库都装载完毕后，会通知Runtime进行下一步的处理



runtime



启动APP时，runtime所做的事情有

1.调用map_images进行可执行文件内容的解析和处理

2.在load_images中调用call_load_methods，调用所有Class和Category的+load方法

3.进行各种objc结构的初始化（注册Objc类 、初始化类对象等等）

4.调用C++静态初始化器和__attribute__((constructor))修饰的函数

到此为止，可执行文件和动态库中所有的符号(Class，Protocol，Selector，IMP，…)都已经按格式成功加载到内存中，被runtime 所管理



main



1.APP的启动由dyld主导，将可执行文件加载到内存，顺便加载所有依赖的动态库

2.并由runtime负责加载成objc定义的结构

3.所有初始化工作结束后，dyld就会调用main函数

4.接下来就是UIApplicationMain函数，AppDelegate的application:didFinishLaunchingWithOptions:方法
