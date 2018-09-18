一. dispatch_group
dispatch_group是GCD(Grand Central Dispatch)中的一组方法，他有一个组的概念，可以把相关的任务归并到一个组内来执行，通过监听组内所有任务的执行情况来做相应处理。

dispatch_group_enter 
用于添加对应任务组中的未执行完毕的任务数，执行一次，未执行完毕的任务数加1，当未执行完毕任务数为0的时候，才会使dispatch_group_wait解除阻塞和dispatch_group_notify的block执行

dispatch_group_leave
用于减少任务组中的未执行完毕的任务数，执行一次，未执行完毕的任务数减1，dispatch_group_enter和dispatch_group_leave要匹配，不然系统会认为group任务没有执行完毕

dispatch_group_wait
等待组任务完成，会阻塞当前线程，当任务组执行完毕时，才会解除阻塞当前线程

二.dispatch_barrier
多线程开发过程中,我们如果想在前面的任务完成后再去执行后面的某些操作,我们可以采用dispatch_barrier_async
例子：

dispatch_queue_t concurrentQueue = dispatch_queue_create("my.concurrent.queue", DISPATCH_QUEUE_CONCURRENT);
dispatch_async(concurrentQueue, ^(){
NSLog(@"block 1");
});
dispatch_async(concurrentQueue, ^(){
NSLog(@"block 2");
});
dispatch_async(concurrentQueue, ^(){
NSLog(@"block 3");
});
dispatch_barrier_async(concurrentQueue, ^(){
NSLog(@"barrier"); 
});
dispatch_async(concurrentQueue, ^(){
NSLog(@"block 4");
});
dispatch_async(concurrentQueue, ^(){
NSLog(@"block 5");
});
dispatch_async(concurrentQueue, ^(){
NSLog(@"block 6");
});
block 1 - 6 都是可以并发执行的，但是由于barrier的存在，在block 1 - 3 执行完成之后，才会执行barrier,在barrier执行完成之后，才会并发执行剩下的block 4 - 6

三.dispatch_semaphore
dispatch_semaphore_create 
dispatch_semaphore_signal :发信号量
dispatch_semaphore_wait(semaphore,DISPATCH_TIME_FOREVER)
其中DISPATCH_TIME_FOREVER 时间性质，决定了是一直阻塞还是到目前 semaphore 需要保证信号量不为0；

四.关于线程的同步并发 同步串行 
同步并发：队列中的线程会一起执行，但是同一时间段只能有一个线程执行，其他线程等待
同步串行：


