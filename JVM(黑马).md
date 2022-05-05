---


## 引言

---

### 什么是JVM

---

好处

- 一次编写，处处运行
- 自动内存管理，垃圾回收功能
- 数组下标越界检查
- 多态


jvm，jre，jdk区别
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651040479891-6873b0ef-736d-4687-afea-e28cbc49ebf5.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=701&id=u39169163&margin=%5Bobject%20Object%5D&name=image.png&originHeight=701&originWidth=1167&originalType=binary&ratio=1&rotation=0&showTitle=false&size=398606&status=done&style=none&taskId=u536e633a-c2ef-4246-90d4-cb865558843&title=&width=1167)

基础类库：util等
编译工具：javac，javap等

### 常见的jvm

---

oricle HOTSPOT
eclipde openJ9

### 学习路线

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651040728140-18ea2d24-8fc4-4b31-aabc-d6896610c48e.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=693&id=ufb0504da&margin=%5Bobject%20Object%5D&name=image.png&originHeight=693&originWidth=1321&originalType=binary&ratio=1&rotation=0&showTitle=false&size=422787&status=done&style=none&taskId=u54c86db9-ff7a-49e1-9d75-285cb30103c&title=&width=1321)



## 内存结构

---


### 程序计数器

---

- 下一条jvm指令的执行地址

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651041003087-accac63e-0b97-40d1-bd80-5806cffd3deb.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=781&id=u8b94818e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=781&originWidth=1744&originalType=binary&ratio=1&rotation=0&showTitle=false&size=555522&status=done&style=none&taskId=u68ec62fc-5c52-4845-b26c-9dc083838a6&title=&width=1744)

特点

- 线程私有（每个线程都有自己的程序计数器）
- 不会存在内存溢出


### 虚拟机栈

---

栈：线程运行需要的内存空间
栈帧：每个方法运行时需要的内存（参数，局部变量，返回地址）

每个线程只能有一个活动栈帧，对应正在执行的方法

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651041414859-59fc8e08-161f-4b90-9569-e629c45be0be.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=748&id=u220b2c22&margin=%5Bobject%20Object%5D&name=image.png&originHeight=748&originWidth=1235&originalType=binary&ratio=1&rotation=0&showTitle=false&size=390783&status=done&style=none&taskId=u94c59171-323c-4c18-bf54-5d19a1975ed&title=&width=1235)

常见问题：

- 垃圾是否涉及栈内存（不会， 因为是方法调用）
- 栈内存是不是越大越好

-Xss， 默认是1M
栈内存越多，可用的线程数就越少了

- 方法内的局部变量是否线程安全

如果方法局部变量没有逃离方法作用范围，就是线程安全的
如果局部变量引用了对象，并逃离了方法的作用范围，就需要考虑线程安全问题
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651041655206-79b4580f-74bf-49b1-8f36-789576cb4c8f.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=418&id=uceb83e38&margin=%5Bobject%20Object%5D&name=image.png&originHeight=418&originWidth=624&originalType=binary&ratio=1&rotation=0&showTitle=false&size=113786&status=done&style=none&taskId=uaab72921-f551-450a-814b-78f706a3e20&title=&width=624)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651041621091-3da30a32-afc2-487a-bbd2-ae210727ef2b.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=683&id=ua36a8cc7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=683&originWidth=1194&originalType=binary&ratio=1&rotation=0&showTitle=false&size=328250&status=done&style=none&taskId=uc3e1c6ba-0e04-44c7-aedc-952c8be4676&title=&width=1194)

栈内存溢出（stackoverflowError）

- 栈帧过多
- 栈帧过大

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651041979047-205c671a-b82d-469f-af39-af1a2b132842.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=482&id=u26e143d9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=482&originWidth=733&originalType=binary&ratio=1&rotation=0&showTitle=false&size=161408&status=done&style=none&taskId=ud30a3c37-1610-4fde-a8ea-f0d4e6f1396&title=&width=733)
可以通过Edit config调整栈内存
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651042046458-ddb60b17-f7fe-4205-ba0d-d31943790c84.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=417&id=u04e4d33f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=417&originWidth=1345&originalType=binary&ratio=1&rotation=0&showTitle=false&size=195182&status=done&style=none&taskId=u84c653d6-f104-4779-916e-fa224bc33a6&title=&width=1345)
调整为256k后，发现递归次数从20000 -> 5000


类之间循环引用溢出
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651042234949-29422448-7305-4e8b-b9a5-637ab4879108.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=641&id=u817f727c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=641&originWidth=657&originalType=binary&ratio=1&rotation=0&showTitle=false&size=190294&status=done&style=none&taskId=ud58c9943-0928-4b54-9afc-52ce18faff3&title=&width=657)


线程运行诊断

1.cpu占用过多

定位进程：top命令查看cpu占用情况
定位线程：ps H -eo pid,tid,%cpu | grep 线程id 定位哪个线程占用过高
jdk定位线程: jstack 进程号  根据线程id找到有问题的代码行数

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651042690773-e565c2d2-d19d-4a65-9afe-44c4862325b1.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=188&id=udc29338f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=188&originWidth=1345&originalType=binary&ratio=1&rotation=0&showTitle=false&size=243670&status=done&style=none&taskId=u76f89359-dc47-4cc0-a566-a48ea2af4cb&title=&width=1345)
看到第8行代码有问题
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651042705148-037b57a1-8e19-4383-a72c-b04482f6620f.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=275&id=u22679b63&margin=%5Bobject%20Object%5D&name=image.png&originHeight=275&originWidth=881&originalType=binary&ratio=1&rotation=0&showTitle=false&size=133741&status=done&style=none&taskId=uff3a071c-8141-4cd8-ac8e-a252a050db9&title=&width=881)


2.程序运行了很长时间没有得到结果

jstack发现了死锁
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651042842723-7f9750c8-269a-4c96-85ca-d7f3fd0e116e.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=730&id=u2c4cd344&margin=%5Bobject%20Object%5D&name=image.png&originHeight=730&originWidth=1381&originalType=binary&ratio=1&rotation=0&showTitle=false&size=812582&status=done&style=none&taskId=u12cd0d7b-a4a0-4cb1-a119-2eddc8dfc83&title=&width=1381)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651042881356-971896da-3c76-4539-9f69-369daf88a94c.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=734&id=ue45e2251&margin=%5Bobject%20Object%5D&name=image.png&originHeight=734&originWidth=1010&originalType=binary&ratio=1&rotation=0&showTitle=false&size=325270&status=done&style=none&taskId=u63e287b2-3467-437d-8fa3-790786ce758&title=&width=1010)



### 本地方法栈

---

给本地方法的执行提供内存空间





### 堆

---

通过new创建对象都使用堆内存

特点

- 线程共享的，堆中对象需要考虑线程安全问题
- 存在垃圾回收

堆内存溢出（OutOfMemoryError: Heap space）

- 虚拟机参数 -Xms 8m 默认4G

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651043202185-b0c8af97-56b0-4e0a-9635-ced3be68bd61.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=783&id=u18721dc1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=783&originWidth=1119&originalType=binary&ratio=1&rotation=0&showTitle=false&size=417356&status=done&style=none&taskId=u174d1ff7-a99d-4dd8-8dae-84ef54952ae&title=&width=1119)


堆内存诊断

- jps：查看当前系统有哪些java进程
- jmap -heap：查看堆内存占用情况（某个时刻）
- jconsole：图形工具(连续监测)

jps
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651043443486-d3bd8258-33af-4d69-9d59-5db46c6c425e.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=236&id=u57b309ab&margin=%5Bobject%20Object%5D&name=image.png&originHeight=236&originWidth=620&originalType=binary&ratio=1&rotation=0&showTitle=false&size=80448&status=done&style=none&taskId=u4ffa47ef-8868-4945-9127-8cd38f564a1&title=&width=620)
jmap
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651043461879-427d7de8-b433-4410-b5ef-2aa828d52119.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=75&id=uab8cada2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=75&originWidth=766&originalType=binary&ratio=1&rotation=0&showTitle=false&size=40479&status=done&style=none&taskId=u094b08c0-7242-4136-891d-26e5b79459d&title=&width=766)
Eden区域发生了显著变化

jconsole
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651043671868-06e80616-e7f4-45d1-a433-3c08903d20e9.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=870&id=u9478578d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=870&originWidth=1204&originalType=binary&ratio=1&rotation=0&showTitle=false&size=178861&status=done&style=none&taskId=u429ec682-2720-4664-aa80-d866062665b&title=&width=1204)


垃圾回收后，内存占用还是很高

jvisualvm: 可视化展示虚拟机
可以抓取快照（dump）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651044023939-7b360ce8-b25a-4ded-8e3f-5ac063816c6c.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=622&id=uf9aa7d21&margin=%5Bobject%20Object%5D&name=image.png&originHeight=622&originWidth=1659&originalType=binary&ratio=1&rotation=0&showTitle=false&size=551846&status=done&style=none&taskId=u69bc8714-040b-4ec5-920a-4852e4c8376&title=&width=1659)
arraylist占用太大
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651044002598-739928a9-e58b-4f7b-8025-e0fb4d518a2a.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=490&id=u32ccdd53&margin=%5Bobject%20Object%5D&name=image.png&originHeight=490&originWidth=1084&originalType=binary&ratio=1&rotation=0&showTitle=false&size=274288&status=done&style=none&taskId=u9471905f-c958-4f55-9698-8a870eb8b63&title=&width=1084)


### 方法区

---

线程共享，存储类的结构，虚拟机启动时被创建，逻辑上属于堆的组成部分
jdk8之前，永久代属于堆内存的一部分
jdk8之后，元空间，使用本地内存

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651044351277-5f409c92-5603-4ccd-b0dc-f445e9a97fac.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=918&id=ue761d37a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=918&originWidth=1373&originalType=binary&ratio=1&rotation=0&showTitle=false&size=400221&status=done&style=none&taskId=ufa7e5326-2d6f-4d63-b1c9-654c4eb50e0&title=&width=1373)


方法区内存溢出
> -XX:MaxMetaspaceSize=8m 最大元空间大小，不然本地内存4G

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651044588618-2d591c7b-18d7-4bb8-839d-9f696374d5eb.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=672&id=ue6b2802a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=672&originWidth=1451&originalType=binary&ratio=1&rotation=0&showTitle=false&size=395499&status=done&style=none&taskId=u2175b137-b81a-4e54-b39b-ae8a1aec9a4&title=&width=1451)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651044670449-a0964957-327c-433c-aba6-4c413fe655de.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=209&id=ud15dd7f8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=209&originWidth=786&originalType=binary&ratio=1&rotation=0&showTitle=false&size=203071&status=done&style=none&taskId=u50937458-16ac-4eef-b8ac-7f2487c4f00&title=&width=786)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651044771317-22e0680b-05c1-40be-8503-3af9a896f04a.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=397&id=u32f00166&margin=%5Bobject%20Object%5D&name=image.png&originHeight=397&originWidth=1334&originalType=binary&ratio=1&rotation=0&showTitle=false&size=221501&status=done&style=none&taskId=u614cff92-de07-4c6b-823f-2fa2c2a4bcd&title=&width=1334)


场景

- spring
- mybatis

运行时常量池

二进制字节码：类的信息，常量池，类方法定义，包含了虚拟机指令

javap 反编译字节码

例：javap -v HelloWorld.class

- 基本信息

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651045045969-b4e6657e-ecd5-4314-ae1b-9e3f2c3506e7.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=354&id=u3b569d3d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=354&originWidth=873&originalType=binary&ratio=1&rotation=0&showTitle=false&size=263069&status=done&style=none&taskId=uada10860-8c3d-44a6-ad03-f99c6708c13&title=&width=873)

- 常量池![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651045085261-2b66ad92-3985-4e01-8acc-e0f0e5c9d9f9.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=371&id=uab8cf2ad&margin=%5Bobject%20Object%5D&name=image.png&originHeight=371&originWidth=1087&originalType=binary&ratio=1&rotation=0&showTitle=false&size=234641&status=done&style=none&taskId=u16b45b65-c9e1-4bc4-a33b-3ed1e7f6eb4&title=&width=1087)
- 类方法定义

构造方法
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651045111329-4fd4d1e5-ad52-4172-99d0-5d7a401276f1.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=290&id=u1c19ff4d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=290&originWidth=978&originalType=binary&ratio=1&rotation=0&showTitle=false&size=133149&status=done&style=none&taskId=uf72d5539-795f-4e97-8ebc-ff7c94c9b24&title=&width=978)
main方法:包含虚拟机指令
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651045132111-dd96449c-5d27-4bc0-940f-6ee770b98488.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=272&id=ub9b3cb69&margin=%5Bobject%20Object%5D&name=image.png&originHeight=272&originWidth=1208&originalType=binary&ratio=1&rotation=0&showTitle=false&size=197599&status=done&style=none&taskId=u9e89185b-f7fb-4bd0-ac63-d630e02c718&title=&width=1208)
#2 查常量池表



运行时常量池
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651045370119-0dd53cea-7058-4b79-b62e-7c8db80831a9.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=223&id=u4061366d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=223&originWidth=1327&originalType=binary&ratio=1&rotation=0&showTitle=false&size=245283&status=done&style=none&taskId=u5da5eb24-c536-4eb4-a4a8-f1a2c8a1a8a&title=&width=1327)

StringTable
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651045562632-e6b954fc-139b-42f1-a3b5-67aae641c673.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=435&id=u8e3c6992&margin=%5Bobject%20Object%5D&name=image.png&originHeight=435&originWidth=1211&originalType=binary&ratio=1&rotation=0&showTitle=false&size=267115&status=done&style=none&taskId=uc8b67461-d149-4676-bc66-4e6dc5a5b75&title=&width=1211)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651045663652-a711af9d-8534-49a5-b69a-a874e066b597.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=789&id=uc18abe4e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=789&originWidth=1515&originalType=binary&ratio=1&rotation=0&showTitle=false&size=510843&status=done&style=none&taskId=ued4bd20b-eb33-452f-b185-4364bbf2979&title=&width=1515)
toString 中内部是 new String 和stringtable中的不一样，会打印false

常量字符串拼接
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651045890146-3234b46e-092e-466f-824c-c40db816bb32.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=310&id=uf939fab9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=310&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=191932&status=done&style=none&taskId=u9f74ed41-18ff-400d-8378-d8fb1fda199&title=&width=1200)


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651045988453-bee649d0-336c-42fd-9034-3b7e9355073e.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=296&id=u536afbe1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=296&originWidth=948&originalType=binary&ratio=1&rotation=0&showTitle=false&size=258662&status=done&style=none&taskId=udb342708-57b2-4264-b9f0-d05a3799621&title=&width=948)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651046080229-f0b8864b-0315-403a-a482-5f07cfb0cb8d.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=422&id=u42ebe06b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=422&originWidth=1433&originalType=binary&ratio=1&rotation=0&showTitle=false&size=244123&status=done&style=none&taskId=u0d91c8e4-ac62-416f-b10d-412b695747a&title=&width=1433)



常见面试题
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651046229757-1ca44e78-e8e1-466a-8f0c-a0cca323e203.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=687&id=u06c23414&margin=%5Bobject%20Object%5D&name=image.png&originHeight=687&originWidth=1156&originalType=binary&ratio=1&rotation=0&showTitle=false&size=335657&status=done&style=none&taskId=u2df32e33-5698-44e7-ad8c-4e93d70fe7d&title=&width=1156)



stringtable内存位置验证
jdk 1.6
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651046390357-563d126d-bc6f-4f36-9c68-9c72ed119332.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=575&id=udbf491ee&margin=%5Bobject%20Object%5D&name=image.png&originHeight=575&originWidth=926&originalType=binary&ratio=1&rotation=0&showTitle=false&size=261041&status=done&style=none&taskId=u1f26b6ff-6b24-41e6-a2df-3f0fab9fb97&title=&width=926)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651046398575-166e9a36-1025-42aa-b5c8-e57025fc09c3.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=102&id=u3ecb78b0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=102&originWidth=872&originalType=binary&ratio=1&rotation=0&showTitle=false&size=99233&status=done&style=none&taskId=ueba4f444-1ac8-4af6-b2cd-73a0a4d47d2&title=&width=872)

jdk1.8

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651046444483-77dbaeea-00a1-471b-8533-172915f1e82b.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=151&id=u4167275a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=151&originWidth=808&originalType=binary&ratio=1&rotation=0&showTitle=false&size=144283&status=done&style=none&taskId=uebe6df30-1089-4171-9167-f5aef575f85&title=&width=808)
如果90%时间花费在GC但只有2%的堆空间被回收，则会报上面的错
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651046517047-14ac9acb-4e85-4ea3-b830-03b4ded13287.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=253&id=u7ac3442d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=253&originWidth=1482&originalType=binary&ratio=1&rotation=0&showTitle=false&size=294798&status=done&style=none&taskId=u8ae8d4aa-9173-4df5-996d-d6bfc61abe6&title=&width=1482)


stringtable垃圾回收
无用的字符串常量就会被垃圾回收掉

stringtable性能调优

-XX:StringTableSize=2000，hash表的长度是2000，会导致碰撞几率变大，速度边慢，所以可以适当的调大这个数子
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651046962763-2aac219d-3be2-40fc-b0df-0e31a70f9034.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=166&id=u2f49634c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=166&originWidth=1020&originalType=binary&ratio=1&rotation=0&showTitle=false&size=62578&status=done&style=none&taskId=u88d2aadf-2ede-4379-ba11-4f6c4eb6862&title=&width=1020)


### 直接内存

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651047085236-b69295dd-b889-42fc-b6e3-5374186b649c.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=279&id=u4451b6ad&margin=%5Bobject%20Object%5D&name=image.png&originHeight=279&originWidth=896&originalType=binary&ratio=1&rotation=0&showTitle=false&size=108457&status=done&style=none&taskId=u76647695-ee9e-43d0-9673-a766d0562f5&title=&width=896)
内存溢出
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651047296953-0cba2272-dabb-473f-b157-1a5d01d1d851.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=143&id=u80ced228&margin=%5Bobject%20Object%5D&name=image.png&originHeight=143&originWidth=903&originalType=binary&ratio=1&rotation=0&showTitle=false&size=165980&status=done&style=none&taskId=uf5229ea0-a3d1-454d-969c-61e01660821&title=&width=903)

bytebuffer的回收
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651047538131-aead1cfe-2a5c-4543-8910-9e5d6b384f16.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=204&id=u0aad2200&margin=%5Bobject%20Object%5D&name=image.png&originHeight=204&originWidth=1386&originalType=binary&ratio=1&rotation=0&showTitle=false&size=200485&status=done&style=none&taskId=u4de02e61-a0d2-420a-9d7a-df13afe1720&title=&width=1386)


-XX:+DisableExplicitGC 禁用显式的垃圾回收，会影响直接内存占用较大的问题



## 垃圾回收

---


### 如何判断垃圾可以被回收

---


#### 引用计数法
> 循环引用的问题


#### 可达性分析算法
> 根对象来判断，扫描一个对象，看这个对象是否能够被根对象到达，不能则回收


Memory Analyzer(MAT)工具
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651048101270-0fc4bb02-b45d-499e-aa63-5128c3a10401.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=246&id=ub0df4cec&margin=%5Bobject%20Object%5D&name=image.png&originHeight=246&originWidth=781&originalType=binary&ratio=1&rotation=0&showTitle=false&size=148122&status=done&style=none&taskId=uafb3a274-e30b-44c8-9465-271d0061781&title=&width=781)

- 系统类

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651048174238-79c478e5-9a64-40e7-b71e-1358c39f394b.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=390&id=ucd9e1f21&margin=%5Bobject%20Object%5D&name=image.png&originHeight=390&originWidth=1147&originalType=binary&ratio=1&rotation=0&showTitle=false&size=441210&status=done&style=none&taskId=u65582605-91f0-486e-9f35-e87f48fdd46&title=&width=1147)

- native stack

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651048204270-9ffe2bce-b74b-413a-80d9-8a727a3d6d5d.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=133&id=u0f8dec28&margin=%5Bobject%20Object%5D&name=image.png&originHeight=133&originWidth=1081&originalType=binary&ratio=1&rotation=0&showTitle=false&size=79303&status=done&style=none&taskId=ubf45120b-a50e-48fd-b12e-9f58f265dce&title=&width=1081)

- busy monitor（正在加锁的对象）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651048225246-b2bd41cf-0b11-43e6-a61a-592acf567ab9.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=94&id=u9e26ee78&margin=%5Bobject%20Object%5D&name=image.png&originHeight=94&originWidth=812&originalType=binary&ratio=1&rotation=0&showTitle=false&size=56146&status=done&style=none&taskId=u6ca34f30-fe4e-4b47-9172-88878f7c3f0&title=&width=812)

-  Thread

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651048253363-cd6ab887-8bd4-4a15-8463-494a74e81740.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=151&id=u5f8a4cb2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=151&originWidth=784&originalType=binary&ratio=1&rotation=0&showTitle=false&size=96398&status=done&style=none&taskId=u680ee362-8e73-4b96-b2d0-08df60884bb&title=&width=784)


#### 四种引用

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651048557261-88e67a98-3200-444b-b153-ab2e46f1f645.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=743&id=u6c233f99&margin=%5Bobject%20Object%5D&name=image.png&originHeight=743&originWidth=1440&originalType=binary&ratio=1&rotation=0&showTitle=false&size=649324&status=done&style=none&taskId=ua0c5ddb5-407f-449c-a6ec-d78cde8b087&title=&width=1440)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651048901828-6ced02bd-1393-4d76-b8eb-e943221aaa81.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=814&id=u420d12e6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=814&originWidth=1381&originalType=binary&ratio=1&rotation=0&showTitle=false&size=800675&status=done&style=none&taskId=uc43ec5e5-96b3-4a83-a130-4ecafe90614&title=&width=1381)

软引用对象
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651048992012-9a30b304-455c-4ac3-8b83-86ee8fb696e5.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=454&id=ud6b1a39b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=454&originWidth=896&originalType=binary&ratio=1&rotation=0&showTitle=false&size=267040&status=done&style=none&taskId=u1bc9d928-acad-49c9-9c5a-a911dad9108&title=&width=896)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049027288-8ff1a0db-e9ab-412d-8516-77ba34096fc6.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=372&id=u482b4603&margin=%5Bobject%20Object%5D&name=image.png&originHeight=372&originWidth=187&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63699&status=done&style=none&taskId=u9636ec94-6393-4638-9ff4-ae9a7f17648&title=&width=187)
第4次循环时，把前面的软引用垃圾回收掉了

设置引用队列
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049175668-09078bc0-2f4f-4003-9507-3c06c07998e5.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=816&id=u2dce5109&margin=%5Bobject%20Object%5D&name=image.png&originHeight=816&originWidth=1044&originalType=binary&ratio=1&rotation=0&showTitle=false&size=468426&status=done&style=none&taskId=u80b1999d-c2c0-4d61-8335-a76e6c46d4c&title=&width=1044)


弱引用
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049224645-d0fb26f7-2d48-438d-a29b-2fb03c560fd4.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=611&id=u9564df41&margin=%5Bobject%20Object%5D&name=image.png&originHeight=611&originWidth=889&originalType=binary&ratio=1&rotation=0&showTitle=false&size=296471&status=done&style=none&taskId=u3cef7c22-518f-4021-a6ff-4a9ce3d8752&title=&width=889)




### 垃圾回收算法

---

#### 标记清除

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049384435-71e4deb0-7e86-4421-8582-5ef02679cb46.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=617&id=ube25f7c7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=617&originWidth=879&originalType=binary&ratio=1&rotation=0&showTitle=false&size=210043&status=done&style=none&taskId=u52c37d72-3009-4fd8-8355-1e6967a847e&title=&width=879)
特点：
速度快，会产生内存碎片

#### 标记整理

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049450373-7d3465d2-db8d-40ab-ade7-e143ba1f1a7c.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=628&id=uff30cabe&margin=%5Bobject%20Object%5D&name=image.png&originHeight=628&originWidth=1373&originalType=binary&ratio=1&rotation=0&showTitle=false&size=333772&status=done&style=none&taskId=u07d1e3a8-a16f-4e25-9883-ae70d9ef29a&title=&width=1373)
特点：
无内存碎片，效率低


#### 复制

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049555461-8f8b1549-2741-4e2d-adf9-b3e325fd9cf5.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=408&id=u47f2acc8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=408&originWidth=1510&originalType=binary&ratio=1&rotation=0&showTitle=false&size=238689&status=done&style=none&taskId=uc6ee6e89-33c2-4041-8fec-c06b8368c50&title=&width=1510)
特点
没内存碎片，但需要双倍内存空间


### 分代回收

---


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049641306-c95d2055-1f72-4253-b6e7-ddf7a8cd8640.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=352&id=uc42ace5f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=352&originWidth=1530&originalType=binary&ratio=1&rotation=0&showTitle=false&size=158054&status=done&style=none&taskId=u977ce998-c426-4130-9f79-9e7e2f37578&title=&width=1530)


Endian满了
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049755122-dca4352d-1ebe-4a58-ae97-b7e636bfaf1f.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=383&id=u571cab40&margin=%5Bobject%20Object%5D&name=image.png&originHeight=383&originWidth=1552&originalType=binary&ratio=1&rotation=0&showTitle=false&size=191311&status=done&style=none&taskId=u84a07d8c-9f5a-4334-999c-3488b27d7e0&title=&width=1552)

- Minor GC
- 伊甸园的到 To区，交换from和to区域
- 生命+1

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049834557-34b9cb8f-320a-4325-8eee-3011ce3bcbc3.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=337&id=u1b607770&margin=%5Bobject%20Object%5D&name=image.png&originHeight=337&originWidth=1541&originalType=binary&ratio=1&rotation=0&showTitle=false&size=183751&status=done&style=none&taskId=ucda83bf7-215a-4b65-9206-764d519b408&title=&width=1541)



Endian又满了
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049865196-6d07b269-ed2c-49cb-9c73-be1ba79a9fcd.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=348&id=uaa8a5155&margin=%5Bobject%20Object%5D&name=image.png&originHeight=348&originWidth=1498&originalType=binary&ratio=1&rotation=0&showTitle=false&size=188160&status=done&style=none&taskId=u6164b010-470e-43ce-b4ca-283650bfc0c&title=&width=1498)

- minor gc
- 伊甸园-> to, from ->to
- 生命+1
- from和to交换

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049924258-ca51e518-5f36-46be-a8b4-b28dc8aab1b7.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=331&id=ue576f39c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=331&originWidth=1515&originalType=binary&ratio=1&rotation=0&showTitle=false&size=171272&status=done&style=none&taskId=u6127bf82-9788-4c80-bc22-fb5338ee9aa&title=&width=1515)



幸存区寿命>15, 转移到老年代
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651049997662-001de0b0-06f2-4192-86b1-6dfbe05c1e6c.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=387&id=udc10b568&margin=%5Bobject%20Object%5D&name=image.png&originHeight=387&originWidth=1521&originalType=binary&ratio=1&rotation=0&showTitle=false&size=198596&status=done&style=none&taskId=u3f724c3d-e3b8-4680-bd90-da3c35944b8&title=&width=1521)



老年代内存不足
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050034554-22cacc67-07d8-4b73-90ef-a25e72969455.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=505&id=u6cfece48&margin=%5Bobject%20Object%5D&name=image.png&originHeight=505&originWidth=1583&originalType=binary&ratio=1&rotation=0&showTitle=false&size=283042&status=done&style=none&taskId=u12e7977d-4a3c-4e21-8342-057a424e257&title=&width=1583)

- full gc

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050141326-c0dd8320-d295-436c-a61b-1ae33baf9317.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=729&id=u18161368&margin=%5Bobject%20Object%5D&name=image.png&originHeight=729&originWidth=1365&originalType=binary&ratio=1&rotation=0&showTitle=false&size=605545&status=done&style=none&taskId=u2137807d-9c77-4f78-9d97-0565403c348&title=&width=1365)

相关的vm参数
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050207980-7452e843-f6cc-4497-8399-fd95a0b72b4a.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=608&id=u08abb406&margin=%5Bobject%20Object%5D&name=image.png&originHeight=608&originWidth=1284&originalType=binary&ratio=1&rotation=0&showTitle=false&size=368872&status=done&style=none&taskId=ubaefa727-1229-4c9e-b020-c3dd72ae630&title=&width=1284)
示例
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050431543-e9ee2b7d-da78-4524-b843-aba6cee22ba9.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=328&id=ue7074289&margin=%5Bobject%20Object%5D&name=image.png&originHeight=328&originWidth=1034&originalType=binary&ratio=1&rotation=0&showTitle=false&size=218422&status=done&style=none&taskId=ud424fdbe-f890-4e25-ba96-433ffb4935b&title=&width=1034)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050373573-6d5929de-c3e0-4665-9998-c8365ae4416a.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=251&id=ue887e486&margin=%5Bobject%20Object%5D&name=image.png&originHeight=251&originWidth=1281&originalType=binary&ratio=1&rotation=0&showTitle=false&size=426293&status=done&style=none&taskId=u9e818635-a43c-4863-80e3-1d1cc07c147&title=&width=1281)

添加元素(一次垃圾回收)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050493376-bcdbfc76-98ba-4e28-bf5b-b05b96273a23.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=338&id=u5dcab0f9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=338&originWidth=980&originalType=binary&ratio=1&rotation=0&showTitle=false&size=251188&status=done&style=none&taskId=u38e7e02e-36ae-47b5-a1c4-3309e82c3c7&title=&width=980)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050504023-68006cb1-11c1-4696-90a9-3e5cb392bad0.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=314&id=u596a88e6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=314&originWidth=1732&originalType=binary&ratio=1&rotation=0&showTitle=false&size=549053&status=done&style=none&taskId=u4a6c5ac0-2b76-4947-9f7d-779734fa609&title=&width=1732)

添加元素（二次垃圾回收）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050603253-04dc3b48-bbee-4b32-8c54-91d581333a8e.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=188&id=u2eeddfcf&margin=%5Bobject%20Object%5D&name=image.png&originHeight=188&originWidth=966&originalType=binary&ratio=1&rotation=0&showTitle=false&size=142273&status=done&style=none&taskId=u9108e433-193b-4600-8a96-a1d92fce84e&title=&width=966)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050610424-2a84d6c5-b6c6-4b7a-8414-6ede530f51a5.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=320&id=u7ae74d1b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=320&originWidth=1735&originalType=binary&ratio=1&rotation=0&showTitle=false&size=626074&status=done&style=none&taskId=uf1641020-c456-4afa-a555-adcb92dc25a&title=&width=1735)


大对象直接到老年代
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050728513-818d8820-74d8-4209-bc10-845732517105.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=200&id=u7a03ff04&margin=%5Bobject%20Object%5D&name=image.png&originHeight=200&originWidth=941&originalType=binary&ratio=1&rotation=0&showTitle=false&size=117292&status=done&style=none&taskId=uf8e6a380-8422-49b7-8366-3cbc4710347&title=&width=941)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050738185-25e03273-f670-4244-bc27-ddb25cf665fc.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=270&id=ue1720024&margin=%5Bobject%20Object%5D&name=image.png&originHeight=270&originWidth=1272&originalType=binary&ratio=1&rotation=0&showTitle=false&size=451181&status=done&style=none&taskId=u9c2db5ae-574f-4508-8741-282218e28dc&title=&width=1272)


子线程堆溢出
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050829388-ab7a05c6-4fd7-421d-ae67-eb736fef4310.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=341&id=ue09be2a9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=341&originWidth=1064&originalType=binary&ratio=1&rotation=0&showTitle=false&size=217537&status=done&style=none&taskId=u7a6b3054-1afc-4634-9793-b1410f70fa4&title=&width=1064)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651050841114-86ad4ac4-6887-4f9d-ae47-74dfe65bd333.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=438&id=uae283a86&margin=%5Bobject%20Object%5D&name=image.png&originHeight=438&originWidth=1437&originalType=binary&ratio=1&rotation=0&showTitle=false&size=733667&status=done&style=none&taskId=ua76cb1ef-b987-4f05-b71e-3789f19ce6e&title=&width=1437)





### 垃圾回收器

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651051028605-b929687b-2dc8-4cad-860a-af7f5e29235b.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=646&id=uab024023&margin=%5Bobject%20Object%5D&name=image.png&originHeight=646&originWidth=1002&originalType=binary&ratio=1&rotation=0&showTitle=false&size=235912&status=done&style=none&taskId=u01b8aa5a-b12b-4fbd-857a-5514d61c9f7&title=&width=1002)

#### 串行

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651051087199-0f7a67d1-0c1f-4ad7-8cac-5d941c374590.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=425&id=u7823b263&margin=%5Bobject%20Object%5D&name=image.png&originHeight=425&originWidth=1310&originalType=binary&ratio=1&rotation=0&showTitle=false&size=281416&status=done&style=none&taskId=u15186a3a-2a93-408e-9cbd-3990319f4b0&title=&width=1310)


#### 吞吐量优先

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651051321010-ed93fe62-b7fe-4db2-b94f-c5a8ec1307bf.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=704&id=u11bdc80c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=704&originWidth=1334&originalType=binary&ratio=1&rotation=0&showTitle=false&size=411400&status=done&style=none&taskId=u6352a2c7-140f-4a46-a525-b929aa7f206&title=&width=1334)


#### 响应时间优先

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651051404296-8092ef28-f4f4-4ff7-97c1-ecec9ea9123d.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=618&id=ua88e0b63&margin=%5Bobject%20Object%5D&name=image.png&originHeight=618&originWidth=1291&originalType=binary&ratio=1&rotation=0&showTitle=false&size=516665&status=done&style=none&taskId=uc7d5497d-51b6-4efe-9fcd-9de01bfa3b0&title=&width=1291)


#### G1回收器

---

JDK9默认，废弃了原来的CMS垃圾回收器

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651051632913-328dc9b3-86a3-4641-8245-260bac00ce21.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=798&id=u9dcbc8d9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=798&originWidth=1124&originalType=binary&ratio=1&rotation=0&showTitle=false&size=356724&status=done&style=none&taskId=u3e97253b-c68f-48bf-893b-a34e013b68e&title=&width=1124)
 

#### 回收阶段

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651051734215-4cc8ce06-073f-437e-a9d3-daa999aebc00.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=709&id=uac661473&margin=%5Bobject%20Object%5D&name=image.png&originHeight=709&originWidth=866&originalType=binary&ratio=1&rotation=0&showTitle=false&size=325316&status=done&style=none&taskId=uc084cba0-2727-4b4a-b9fe-585f705efc0&title=&width=866)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651052007857-cd51b6f4-913e-4b86-b892-f3017a3222f0.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=691&id=u956bb45b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=691&originWidth=779&originalType=binary&ratio=1&rotation=0&showTitle=false&size=313554&status=done&style=none&taskId=u7646e2d1-239d-44d2-a004-5c7795553f5&title=&width=779)



#### 垃圾回收调优

---

- 内存
- 锁竞争
- cpu占用
- io




## 字节码技术

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651052925633-a00db6ff-e412-40d6-b89a-4947a40b65f4.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=906&id=u95fbf21b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=906&originWidth=1404&originalType=binary&ratio=1&rotation=0&showTitle=false&size=398822&status=done&style=none&taskId=u0eea2445-7bf0-4ee0-8490-8ab9b1d2223&title=&width=1404)


类文件结构
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651053034461-ba6371b6-67d7-4f06-8a21-15ddba01865b.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=809&id=u6f3ee793&margin=%5Bobject%20Object%5D&name=image.png&originHeight=809&originWidth=1189&originalType=binary&ratio=1&rotation=0&showTitle=false&size=269906&status=done&style=none&taskId=u73fbb9ef-6dc1-458b-ad3d-b9834d1d2b4&title=&width=1189)![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651053034495-ce07cdb1-4d89-40ec-bc92-ee9955d83cbe.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=809&id=u932047e0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=809&originWidth=1189&originalType=binary&ratio=1&rotation=0&showTitle=false&size=269906&status=done&style=none&taskId=ud14df3a2-30ba-4026-89c9-a2cabc59917&title=&width=1189)

- 魔数（4个字节）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651053100707-fd4dc3c8-133e-4fe5-a478-4bfe92be0747.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=155&id=ud67dad2e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=155&originWidth=820&originalType=binary&ratio=1&rotation=0&showTitle=false&size=74264&status=done&style=none&taskId=u7dc5cd9f-d264-4817-ad85-c5960249602&title=&width=820)

- 版本（4个字节）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651053152167-a52f3115-972e-48e3-837a-8595d2ea9a94.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=177&id=u78acb782&margin=%5Bobject%20Object%5D&name=image.png&originHeight=177&originWidth=715&originalType=binary&ratio=1&rotation=0&showTitle=false&size=80087&status=done&style=none&taskId=uf1790f03-56fb-42fc-b781-0d6f3ee8212&title=&width=715)

- 常量池

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651053204315-5f28bdfb-b5d5-476d-b09a-0545e2423d01.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=167&id=u3a8b99b4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=167&originWidth=1191&originalType=binary&ratio=1&rotation=0&showTitle=false&size=133355&status=done&style=none&taskId=ucc5d330b-c731-4893-ba07-f7a3a95f841&title=&width=1191)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651053256428-61ebdc55-e550-4e70-a4de-f33897b12f9c.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=203&id=u06b18e32&margin=%5Bobject%20Object%5D&name=image.png&originHeight=203&originWidth=1400&originalType=binary&ratio=1&rotation=0&showTitle=false&size=171810&status=done&style=none&taskId=u9f5b020a-1e1a-478d-9527-0c94db85b12&title=&width=1400)![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651053277123-652c6662-95de-441e-b63f-b7c2f2d435b1.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=249&id=u844abd50&margin=%5Bobject%20Object%5D&name=image.png&originHeight=249&originWidth=1453&originalType=binary&ratio=1&rotation=0&showTitle=false&size=217759&status=done&style=none&taskId=u94dded84-4fdb-4ee7-8f10-c2dd01547f6&title=&width=1453)

- 访问标识和继承信息

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651053522883-8d4ec61c-f28d-40af-8a57-c1def33552d3.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=547&id=udf2d58c5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=547&originWidth=1464&originalType=binary&ratio=1&rotation=0&showTitle=false&size=416923&status=done&style=none&taskId=u0ba7d428-2f74-4252-b908-c24204d87e8&title=&width=1464)

- 成员变量信息
- 方法信息
- 附加属性



javap工具

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651053895725-8d72dc2a-cb59-42d8-bc57-a7a7aaedc6fc.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=411&id=u4156a833&margin=%5Bobject%20Object%5D&name=image.png&originHeight=411&originWidth=1154&originalType=binary&ratio=1&rotation=0&showTitle=false&size=353726&status=done&style=none&taskId=u977158c5-8015-4626-81a9-162b31b99b0&title=&width=1154)


图解代码执行
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054190362-c030f7c2-7c37-4039-a42c-d6a9fc735399.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=610&id=u52f6e275&margin=%5Bobject%20Object%5D&name=image.png&originHeight=610&originWidth=1299&originalType=binary&ratio=1&rotation=0&showTitle=false&size=367575&status=done&style=none&taskId=u76991809-8f40-45be-ae2d-acae75555dd&title=&width=1299)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054241267-9b915121-4c87-46e0-aa09-88338cc0434f.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=578&id=u7047a47b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=578&originWidth=1273&originalType=binary&ratio=1&rotation=0&showTitle=false&size=359281&status=done&style=none&taskId=udd995f06-e3c4-415f-bf74-3fee29040d6&title=&width=1273)
执行方法区的第一条指令bipush10
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054327152-769d6f5f-b5ea-4d78-8391-076746f001d2.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=619&id=ub2ef0db9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=619&originWidth=1333&originalType=binary&ratio=1&rotation=0&showTitle=false&size=448434&status=done&style=none&taskId=uebb8aa4a-d537-4849-bf80-117024f759f&title=&width=1333)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054375012-a9d3a8c1-7e20-4759-8d10-00a6fc9ecb6f.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=703&id=u8048c9e9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=703&originWidth=1338&originalType=binary&ratio=1&rotation=0&showTitle=false&size=527461&status=done&style=none&taskId=u8dd3d548-61b7-4390-b744-39aa7a67d60&title=&width=1338)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054425603-28e8143b-2730-4d0d-8cbd-f3f636848655.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=905&id=u27f3e829&margin=%5Bobject%20Object%5D&name=image.png&originHeight=905&originWidth=1273&originalType=binary&ratio=1&rotation=0&showTitle=false&size=621839&status=done&style=none&taskId=uddb9d777-d98b-4b79-bbb7-57c7b74b727&title=&width=1273)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054462266-6e4d4e41-b306-4cf9-abf2-a75bcc989d90.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=577&id=u048977ca&margin=%5Bobject%20Object%5D&name=image.png&originHeight=577&originWidth=1310&originalType=binary&ratio=1&rotation=0&showTitle=false&size=472216&status=done&style=none&taskId=uf7ca5e3d-dcf8-4fed-901d-dfa5bac9fa8&title=&width=1310)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054518737-cae16bcd-a49f-4bb7-83e0-a51dc98daee4.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=923&id=u151bf29e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=923&originWidth=1359&originalType=binary&ratio=1&rotation=0&showTitle=false&size=801452&status=done&style=none&taskId=ub05054fa-989c-48ba-ac83-19a56156bfc&title=&width=1359)



字节码分析如下代码
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054887942-21d1a0d5-bf34-4835-a56f-e33d06dc9218.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=600&id=ubaeeaf06&margin=%5Bobject%20Object%5D&name=image.png&originHeight=600&originWidth=970&originalType=binary&ratio=1&rotation=0&showTitle=false&size=223892&status=done&style=none&taskId=u40364aaa-3815-4326-bfa2-6a9f61cf08b&title=&width=970)

i++ 与 ++i 区别

---

i++
> i进入操作数栈，然后局部变量表+1，但是操作数栈还是原来的

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054707269-4819ba8b-6018-4152-847f-1fd61a1367ea.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=931&id=u3b7ae170&margin=%5Bobject%20Object%5D&name=image.png&originHeight=931&originWidth=1251&originalType=binary&ratio=1&rotation=0&showTitle=false&size=452041&status=done&style=none&taskId=u9bf14f5c-b703-40aa-bbbb-61dbe95cd99&title=&width=1251)

++i
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054802594-def15007-aebe-4246-9f01-0c14b380445f.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=930&id=u238c7060&margin=%5Bobject%20Object%5D&name=image.png&originHeight=930&originWidth=1084&originalType=binary&ratio=1&rotation=0&showTitle=false&size=444552&status=done&style=none&taskId=ue5f72128-cb81-42ea-831d-17066e5397d&title=&width=1084)



构造方法
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054970083-0cc9ef91-b790-4a87-966a-9db8cae6ee79.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=542&id=u16fb7c32&margin=%5Bobject%20Object%5D&name=image.png&originHeight=542&originWidth=717&originalType=binary&ratio=1&rotation=0&showTitle=false&size=75932&status=done&style=none&taskId=u2f189fb5-be2c-485e-a8a8-a94cd6a96f5&title=&width=717)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651054997153-2e495995-c761-40d9-afe4-eeea9e8a2a50.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=417&id=u52088133&margin=%5Bobject%20Object%5D&name=image.png&originHeight=417&originWidth=1341&originalType=binary&ratio=1&rotation=0&showTitle=false&size=278588&status=done&style=none&taskId=u152e8835-a9c9-4d4e-a572-6d48ec765b4&title=&width=1341)


init
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651055047598-60e7b64d-f6dc-4fe9-8f77-d9ffff261bd7.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=1001&id=u87d771df&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1001&originWidth=798&originalType=binary&ratio=1&rotation=0&showTitle=false&size=294882&status=done&style=none&taskId=u82b9bcee-f494-4651-beca-611d4562e48&title=&width=798)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651055104416-c5e16f6f-838d-4a28-bfc8-18ee0bb8ee83.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=469&id=uf4ce1046&margin=%5Bobject%20Object%5D&name=image.png&originHeight=469&originWidth=1343&originalType=binary&ratio=1&rotation=0&showTitle=false&size=378622&status=done&style=none&taskId=u6840b797-1b89-4c60-98ba-f95b6b34824&title=&width=1343)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651055137685-5f7ffb10-4f9c-4132-808e-a54c91dea48e.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=850&id=u8df2476f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=850&originWidth=965&originalType=binary&ratio=1&rotation=0&showTitle=false&size=470333&status=done&style=none&taskId=u8baa4b21-1b9a-43dc-8ab0-e24620ef3ea&title=&width=965)





方法调用
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651055172922-cfaa766b-b74b-42c7-b190-d7be63bc6e5e.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=746&id=u8041b3f9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=746&originWidth=702&originalType=binary&ratio=1&rotation=0&showTitle=false&size=266196&status=done&style=none&taskId=u3e36afa8-dd17-4d03-b068-7ba755249c2&title=&width=702)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651055254755-04abeb30-1504-4f1a-a8b8-ff560690aca6.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=585&id=ucdf77ffe&margin=%5Bobject%20Object%5D&name=image.png&originHeight=585&originWidth=1196&originalType=binary&ratio=1&rotation=0&showTitle=false&size=353571&status=done&style=none&taskId=ud9a4f9dd-885a-41f7-ad13-78b9dab3d75&title=&width=1196)



多态

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651055468970-2532779c-e863-480e-8c67-2518e885d6ab.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=404&id=u81f763f6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=404&originWidth=1112&originalType=binary&ratio=1&rotation=0&showTitle=false&size=267916&status=done&style=none&taskId=ua4ed0b34-6826-4ec1-9b0f-2963cd7614a&title=&width=1112)


异常处理

---

exception table
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651055562446-a43c0e12-f3b5-42f7-b2df-d3cc7f8c9780.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=676&id=ue1b412a2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=676&originWidth=785&originalType=binary&ratio=1&rotation=0&showTitle=false&size=296407&status=done&style=none&taskId=u111cd0b3-b84e-4a0a-bbf4-f0efa7eb12d&title=&width=785)


## 语法糖

---

- 默认构造器
- 自动拆装箱
- 泛型集合取值

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651056838181-cdfd1a69-63a4-453e-a53a-d2129aec606b.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=302&id=u0ef88bc9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=302&originWidth=1263&originalType=binary&ratio=1&rotation=0&showTitle=false&size=221033&status=done&style=none&taskId=u893a9383-2456-4331-a853-ee01ea56a54&title=&width=1263)

- 可变参数

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651056929966-586ac0c6-438c-4625-918d-c964925d164f.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=877&id=u63b41213&margin=%5Bobject%20Object%5D&name=image.png&originHeight=877&originWidth=937&originalType=binary&ratio=1&rotation=0&showTitle=false&size=501538&status=done&style=none&taskId=uc133759b-73bd-4b45-9481-399ca43f1ae&title=&width=937)

- foreach循环

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651056992741-b4d6e489-25c9-495b-b421-01597c0a7943.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=919&id=ua9fc2cc9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=919&originWidth=1269&originalType=binary&ratio=1&rotation=0&showTitle=false&size=465616&status=done&style=none&taskId=u2ebb6d8a-e3e2-4de1-a99c-29030686005&title=&width=1269)

- switch字符串
- sewitch枚举
- 枚举类

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651057121310-733662ae-cb47-43ae-94f0-ec48ef756bdc.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=658&id=uba3a2cf9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=658&originWidth=948&originalType=binary&ratio=1&rotation=0&showTitle=false&size=271956&status=done&style=none&taskId=u5ac4651b-92f7-44b8-b398-36bb533b1c6&title=&width=948)

- try-with-resource

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651057192858-f7532d85-fb6a-423f-8ef4-08a24249045f.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=837&id=u99936783&margin=%5Bobject%20Object%5D&name=image.png&originHeight=837&originWidth=1327&originalType=binary&ratio=1&rotation=0&showTitle=false&size=544955&status=done&style=none&taskId=u331ced79-88d0-465a-b47b-6bf87d71ee8&title=&width=1327)


## 类加载阶段

---

#### 加载

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651057398091-065fd3e4-9c19-4c65-93f4-a51c877cb9a4.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=603&id=uf0852f17&margin=%5Bobject%20Object%5D&name=image.png&originHeight=603&originWidth=1293&originalType=binary&ratio=1&rotation=0&showTitle=false&size=447326&status=done&style=none&taskId=u751d62b9-d52c-419b-8726-9433a62ea30&title=&width=1293)

#### 链接

---

验证--准备--解析（将常量池的符号引用解析为直接引用）

#### 初始化

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651057670475-ac19d874-d46e-4326-95c4-947e6022769a.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=763&id=u0c94f109&margin=%5Bobject%20Object%5D&name=image.png&originHeight=763&originWidth=945&originalType=binary&ratio=1&rotation=0&showTitle=false&size=538612&status=done&style=none&taskId=u8cf7bdf2-2715-4e0b-bf4e-d8deec62f03&title=&width=945)


## 类加载器

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651057729543-85f36ead-7c3f-4731-adfc-172c70f0b40b.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=346&id=u23bcb695&margin=%5Bobject%20Object%5D&name=image.png&originHeight=346&originWidth=1359&originalType=binary&ratio=1&rotation=0&showTitle=false&size=271381&status=done&style=none&taskId=u724a0902-6fea-4e45-af7e-fee82b77a9e&title=&width=1359)

#### 双亲委派加载模式

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651057924107-b46f7301-eb65-4275-a1ba-517c07d1cadf.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=860&id=u80a79d37&margin=%5Bobject%20Object%5D&name=image.png&originHeight=860&originWidth=1286&originalType=binary&ratio=1&rotation=0&showTitle=false&size=660032&status=done&style=none&taskId=u8200b61e-8b40-4819-802c-42272ea7303&title=&width=1286)


## 运行期优化

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651058270880-b2483ce7-4e54-4870-9010-72074b3c06db.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=762&id=u822a63e8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=762&originWidth=1407&originalType=binary&ratio=1&rotation=0&showTitle=false&size=781558&status=done&style=none&taskId=u8ad47b0f-4a2c-470b-9f47-1d8eb5f04de&title=&width=1407)
逃逸分析
方法内联
字段优化
反射优化



## java内存模型

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651058532825-eff43dc2-4ee4-4a8b-bc39-1562c47e3af4.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=360&id=u4c75737e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=360&originWidth=1337&originalType=binary&ratio=1&rotation=0&showTitle=false&size=379631&status=done&style=none&taskId=u2b95aa17-8b00-49b8-9486-a67f513defc&title=&width=1337)
### 原子性

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651058590361-b2a0338d-d134-4f21-960f-185c14c8a583.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=892&id=ud958afea&margin=%5Bobject%20Object%5D&name=image.png&originHeight=892&originWidth=1356&originalType=binary&ratio=1&rotation=0&showTitle=false&size=385970&status=done&style=none&taskId=uda7e4d26-1310-4053-8d02-7f9cc384d3f&title=&width=1356)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651058749752-4c0f07ab-4412-4e76-8dc6-bf7e973a05b4.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=753&id=u53ca8f6b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=753&originWidth=984&originalType=binary&ratio=1&rotation=0&showTitle=false&size=480617&status=done&style=none&taskId=u9148d18a-d84f-4cce-8625-706ddd7a88a&title=&width=984)

### 可见性

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651058975671-5cdf5271-a8a3-44b4-b2f4-ce59ade831d4.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=442&id=u22e1c20f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=442&originWidth=908&originalType=binary&ratio=1&rotation=0&showTitle=false&size=183686&status=done&style=none&taskId=u2ed0d385-1c7c-47b7-8c15-714decde0f0&title=&width=908)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651058960069-42d85d08-5004-420f-b94f-d19de34e99f4.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=445&id=ub07e3a1b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=445&originWidth=1147&originalType=binary&ratio=1&rotation=0&showTitle=false&size=307970&status=done&style=none&taskId=u88b6a12f-77a2-4d63-8645-a7c6d5f208a&title=&width=1147)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059001296-7af082d4-2052-417f-8ecf-c4ea6d6dd430.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=191&id=uaba93e71&margin=%5Bobject%20Object%5D&name=image.png&originHeight=191&originWidth=1330&originalType=binary&ratio=1&rotation=0&showTitle=false&size=227978&status=done&style=none&taskId=u4409bf95-f8b3-43c0-abc1-956eada9d12&title=&width=1330)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059034377-8ed388c7-9d42-4a26-9b62-35cfa6be71a8.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=110&id=ue71dce58&margin=%5Bobject%20Object%5D&name=image.png&originHeight=110&originWidth=1306&originalType=binary&ratio=1&rotation=0&showTitle=false&size=185859&status=done&style=none&taskId=uc77b1c7f-0537-42e3-8ca1-65179bb7ccc&title=&width=1306)


### 有序性

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059357948-eb21a66d-90c7-4c2c-9e95-5a76dcbf71c2.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=915&id=u9fa6cbe9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=915&originWidth=1377&originalType=binary&ratio=1&rotation=0&showTitle=false&size=530040&status=done&style=none&taskId=u0ce9c1bb-cc5c-4efc-968f-2216fedd755&title=&width=1377)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059230947-9e3dc0fa-6baf-4f5f-baa3-327ff009b61b.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=86&id=u4ce6078b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=86&originWidth=1243&originalType=binary&ratio=1&rotation=0&showTitle=false&size=109743&status=done&style=none&taskId=ua6efb041-6197-4514-817c-26a8164dabd&title=&width=1243)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059312688-440ba5ad-4dca-4db8-9642-c671cc7b6986.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=867&id=u9dce82e3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=867&originWidth=1124&originalType=binary&ratio=1&rotation=0&showTitle=false&size=411856&status=done&style=none&taskId=u42e7bad9-031f-4d68-afc6-69f9e27de83&title=&width=1124)


### happens-before

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059437257-feae8000-0f8f-40c7-873f-e1f38f065d75.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=480&id=uc149fad4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=480&originWidth=932&originalType=binary&ratio=1&rotation=0&showTitle=false&size=188812&status=done&style=none&taskId=u973e6af7-20fe-4020-b8d5-f487772d692&title=&width=932)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059472588-56e9a24a-5421-44d3-8049-d044a3d2b90e.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=619&id=uc1fcdadb&margin=%5Bobject%20Object%5D&name=image.png&originHeight=619&originWidth=1092&originalType=binary&ratio=1&rotation=0&showTitle=false&size=257682&status=done&style=none&taskId=u29352b44-c3b4-4e5d-848a-a17cdce14e3&title=&width=1092)

### CAS和原子类

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059539814-f041c00e-842a-4408-a129-d6e0d25d8a4b.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=686&id=u8387cc9e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=686&originWidth=1368&originalType=binary&ratio=1&rotation=0&showTitle=false&size=518281&status=done&style=none&taskId=u78d6d3b4-8067-4789-a1f5-5f845cd3daf&title=&width=1368)
用CAS和valatile可以实现无锁并发
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059656451-53e2a77e-8e71-40f1-b7cf-f413d1728380.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=340&id=u92fc0c45&margin=%5Bobject%20Object%5D&name=image.png&originHeight=340&originWidth=1321&originalType=binary&ratio=1&rotation=0&showTitle=false&size=478510&status=done&style=none&taskId=u60b866d5-2fc0-4ddd-a44a-d93b405c7ca&title=&width=1321)

乐观锁和悲观锁
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059734345-805d1637-dbe2-4d12-bdd4-77b7ad46e8ca.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=191&id=u39ddffca&margin=%5Bobject%20Object%5D&name=image.png&originHeight=191&originWidth=1333&originalType=binary&ratio=1&rotation=0&showTitle=false&size=286861&status=done&style=none&taskId=u30f848b6-a006-4301-9f6c-ba2ec1323df&title=&width=1333)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059774242-c77f0221-a0ce-4c1d-8c37-6d6d6acb6cfc.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=111&id=ue5430eb3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=111&originWidth=1339&originalType=binary&ratio=1&rotation=0&showTitle=false&size=172634&status=done&style=none&taskId=u6132f429-6fb8-4cd2-8daf-663cf87e6d9&title=&width=1339)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059808849-c3165006-8869-4768-b5cc-587390b424d3.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=826&id=u462ad287&margin=%5Bobject%20Object%5D&name=image.png&originHeight=826&originWidth=1112&originalType=binary&ratio=1&rotation=0&showTitle=false&size=463174&status=done&style=none&taskId=ucff8c46c-0cd4-4ac1-9e1a-2d24bba868c&title=&width=1112)

### synchronized优化

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651059876870-4a0ec0ac-2c29-4af3-9467-afd9bbe25913.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=163&id=uae9eb0bc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=163&originWidth=1353&originalType=binary&ratio=1&rotation=0&showTitle=false&size=227384&status=done&style=none&taskId=ua7b5c02d-65fe-4a0a-821a-8028456b036&title=&width=1353)
轻量级锁
> 多个线程交替占锁

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651060008798-f039c2e0-a8ea-4636-9df1-4e207d140961.png#clientId=uf03a39b4-7554-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=378&id=ub6ed85b3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=378&originWidth=1371&originalType=binary&ratio=1&rotation=0&showTitle=false&size=537910&status=done&style=none&taskId=uc57fbaa2-2e58-44df-aced-7a28f39bf08&title=&width=1371)
锁膨胀
重量锁（自旋）
偏向锁



