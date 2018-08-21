拷贝需要根据具体类型比如NSString NSMutableString 类型
以及使用的拷贝方法：比如copy 跟mutableCopy来确认对象的内存地址是否发生变化，以及新生成的对象的类型
 比如：一次深拷贝
 NSMutableString*str1 = [NSMutableString stringWithFormat:@"bbb"];
 NSString*copyStr1 = [str1 copy];
 NSLog(@"str1 = %p copyStr1 = %p",str1,copyStr1);
 NSLog(@"str1 = %p copyStr1= %p",&str1,&copyStr1);
 
 输出结果：str1 = 0x7fa522712cd0 copyStr1 = 0x7fa522717ba0
 指针地址：str1 = 0x7fff529e9a98 copyStr1= 0x7fff529e9a90
 小结：对可变字符串的copy，我们默认进行了一次深拷贝，直接拷贝了对象。
 

