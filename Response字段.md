文章出处： https://www.jianshu.com/p/f9b8dd4f3c85

Headers {
"Access-Control-Allow-Origin" =     (
"*"
);
Age =     (
49185
);
"Cache-Control" =     (
"max-age=86400"
);
Connection =     (
"keep-alive"
);
"Content-Length" =     (
239003
);
"Content-Type" =     (
"image/jpeg"
);
Date =     (
"Tue, 14 Aug 2018 14:10:10 GMT"
);
EagleId =     (
74cf649615343049957403942e
);

// 是一个 hash 值 用作 Request 缓存请求头，每一个资源文件都对应一个唯一的 ETag 值， 服务器单独负责判断记号是什么及其含义，并在HTTP响应头中将其传送到客户端
Etag =     (
"\"149495AF87634ACD9907DB9240FCEC9A\""
);
//原理： 
1、当浏览器首次请求资源的时候，服务器会返回200的状态码（ok）,内容为请求的资源，同时response header会有一个ETag标记，该标记是服务器端根据容器（IIS或者Apache等等）中配置的ETag生成策略生成的一串唯一标识资源的字符串，ETag格式为 ETag:"856247206"

2、当浏览器第2次请求该资源时，浏览器会在传递给服务器的request中添加If-None-Match报头，询问服务器改文件在上次获取后是否修改了，报头格式：If-None-Match:"856246825"

3、服务器在获取到浏览器的请求后，会根据请求的资源查找对应的ETag，将当前服务器端指定资源对应的Etag与request中的If-None-Match进行对比，如果相同，说明资源没有修改，服务器返回304状态码（Not Modified），内容为空；如果对比发现不相同，则返回200状态码，同时将新的Etag添加到返回浏览器的response中。


//1.给出的日期/时间之后的时间，就被响应认为是过时
//2.需和Last-Modified结合使用。用于控制请求文件的有效时间，当请求数据在有效期内时客户端浏览器从缓存请求数据而不是服务器端
//3.当缓存中数据失效或过期，才决定从服务器更新数据。
Expires =     (
"Wed, 27 Jul 2022 06:51:42 GMT"
);


//注释： 上次修改（时间）
"Last-Modified" =     (
"Thu, 27 Jul 2017 06:51:43 GMT"
);
//更新原理 (结合使用code= 200 code= 3##)
1、在浏览器首次请求某个资源时，服务器端返回的状态码是200 （ok），内容是你请求的资源，同时有一个Last-Modified的属性标记(Reponse Header)，标识此文件在服务期端最后被修改的时间，格式：Last-Modified:Tue, 24 Feb 2009 08:01:04 GMT

2、浏览器第二次请求该资源时，根据HTTP协议的规定，浏览器会向服务器传送If-Modified-Since报头(Request Header)，询问该文件是否在指定时间之后有被修改过，格式为：If-Modified-Since:Tue, 24 Feb 2009 08:01:04 GMT

3、如果服务器端的资源没有变化，则服务器返回304状态码（Not Modified），内容为空，这样就节省了传输数据量。当服务器端代码发生改变，则服务器返回200状态码（ok），内容为请求的资源，和第一次请求资源时类似。从而保证在资源没有修改时不向客户端重复发出资源，也保证当服务器有变化时，客户端能够及时得到最新的资源。



Server =     (
Tengine
);
"Timing-Allow-Origin" =     (
"*"
);
Via =     (
"cache14.l2et15[0,304-0,H], cache15.l2et15[1,0], cache9.cn1240[0,200-0,H], cache2.cn1240[1,0]"
);
"X-Cache" =     (
"HIT TCP_MEM_HIT dirn:8:840892423 mlen:-1"
);
"X-Swift-CacheTime" =     (
47188
);
"X-Swift-SaveTime" =     (
"Wed, 15 Aug 2018 01:03:42 GMT"
);
"x-oss-hash-crc64ecma" =     (
6406122444033743544
);
"x-oss-object-type" =     (
Normal
);
"x-oss-request-id" =     (
5B72E2C2488C307004B65223
);
"x-oss-storage-class" =     (
Standard
);
} 
