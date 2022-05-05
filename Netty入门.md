---


## HelloWorld

---

- 导入依赖
- 服务器端

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650945420826-3bf8de85-96f3-4f8e-a6e3-d5b100fe753c.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=544&id=u576885f5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=680&originWidth=1427&originalType=binary&ratio=1&rotation=0&showTitle=false&size=437604&status=done&style=none&taskId=uf6919fb8-3ec3-4a3a-abf8-7c5d9c309f9&title=&width=1141.6)
1.ServerBootstap 启动器，负责组装组件，启动服务器
2.NioEventLoopGroup : (selector, thread) group组
3.NioServerSocketChannel: 选择NioServerSocketChannel实现
4.childHandle: worker需要执行哪些读写逻辑
5.channelInitializer: channel
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650945818301-24dc3915-0143-448d-98f7-2e1de735689f.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=706&id=u9c97ad80&margin=%5Bobject%20Object%5D&name=image.png&originHeight=883&originWidth=1568&originalType=binary&ratio=1&rotation=0&showTitle=false&size=743365&status=done&style=none&taskId=ubae9720b-e798-459d-b0c9-fcfcab357fc&title=&width=1254.4)

- client

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650946035839-53c0d9db-598b-4bbf-9c97-65bc6d250dd3.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=641&id=u262f82af&margin=%5Bobject%20Object%5D&name=image.png&originHeight=801&originWidth=1317&originalType=binary&ratio=1&rotation=0&showTitle=false&size=548664&status=done&style=none&taskId=u9328330c-c47e-4cc0-b15a-dd4d09b285d&title=&width=1053.6)

- 执行流程

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650946358775-a491b3e7-f483-4904-9c01-b7bedad702c9.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=690&id=u49f0ce32&margin=%5Bobject%20Object%5D&name=image.png&originHeight=862&originWidth=1769&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1222688&status=done&style=none&taskId=ud29b6c6e-1107-4379-8dd5-d944e0f0295&title=&width=1415.2)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650946628741-7de113e3-7c6c-4b89-a4c6-4ab6ca9474dd.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=442&id=uf50601da&margin=%5Bobject%20Object%5D&name=image.png&originHeight=553&originWidth=972&originalType=binary&ratio=1&rotation=0&showTitle=false&size=463409&status=done&style=none&taskId=u1ed12e2b-2d46-44ef-bd75-c6232fd472b&title=&width=777.6)


## 组件

---


### EventLoop

---

- 普通任务(不指定线程数的话默认是核心数 * 2)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650947770428-dd66c7d2-357e-4339-baac-4079eb0932fb.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=669&id=ua858bab4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=836&originWidth=1358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=511664&status=done&style=none&taskId=u4a8319e9-26af-4785-92db-fec025dec60&title=&width=1086.4)

- 定时任务

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650947871091-bb86df31-3e1d-4285-8ee3-e049c155c4e1.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=199&id=u659e9972&margin=%5Bobject%20Object%5D&name=image.png&originHeight=249&originWidth=783&originalType=binary&ratio=1&rotation=0&showTitle=false&size=132834&status=done&style=none&taskId=u06c36727-859b-44f8-9c8b-37a0c4c31fc&title=&width=626.4)

- IO事件

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650948189578-de890753-123d-49fa-a7ca-29271e3606bf.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=601&id=u5d6a3974&margin=%5Bobject%20Object%5D&name=image.png&originHeight=751&originWidth=1435&originalType=binary&ratio=1&rotation=0&showTitle=false&size=551663&status=done&style=none&taskId=ubf070ad1-d818-4822-af11-a679745ddea&title=&width=1148)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650948231351-29a7122a-43b7-4eae-b4ce-0e855d7a8a55.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=574&id=u90923773&margin=%5Bobject%20Object%5D&name=image.png&originHeight=717&originWidth=1103&originalType=binary&ratio=1&rotation=0&showTitle=false&size=405557&status=done&style=none&taskId=u1dfaee50-22e0-4cc4-aaae-1439515ef8a&title=&width=882.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650948420332-ad64b078-4c1c-4774-b585-8d8e6a5d4d87.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=511&id=uc981bfb3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=639&originWidth=817&originalType=binary&ratio=1&rotation=0&showTitle=false&size=320639&status=done&style=none&taskId=u9812b2f7-8d84-4de7-ad85-fefdddffb9f&title=&width=653.6)


- 将boss和worker分开，accept和read，write分开

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650948657504-57314804-941f-43dc-9b03-55affc66c8a5.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=197&id=u7835d13f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=246&originWidth=1385&originalType=binary&ratio=1&rotation=0&showTitle=false&size=252182&status=done&style=none&taskId=u33926418-d310-44e1-90fd-91ca5392f59&title=&width=1108)

- 独立的eventloop处理heavy thing

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650948987760-33540bc2-3e20-4d1b-8539-b0c34b8142dd.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=532&id=u9036ffd7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=665&originWidth=1517&originalType=binary&ratio=1&rotation=0&showTitle=false&size=718824&status=done&style=none&taskId=ua503cf5e-bd34-48b8-9fda-aadac685c42&title=&width=1213.6)

- handler换人

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650949272682-c1bf87f5-41ab-482e-ad8c-e23c45979486.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=500&id=uecf705f7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=625&originWidth=1694&originalType=binary&ratio=1&rotation=0&showTitle=false&size=901992&status=done&style=none&taskId=u3be30cf2-eb7c-448a-b91b-52f64924ac6&title=&width=1355.2)


### channel

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650949341421-b083a360-3f92-4525-81a2-bde9ec67c736.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=314&id=u0244fe1b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=393&originWidth=892&originalType=binary&ratio=1&rotation=0&showTitle=false&size=192959&status=done&style=none&taskId=u37130744-f3c0-4d53-adf4-c8b3032f7fd&title=&width=713.6)

- channelFuture

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650949592596-16720309-8a7b-47df-95af-d655bfdf071b.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=594&id=uf356926e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=743&originWidth=1246&originalType=binary&ratio=1&rotation=0&showTitle=false&size=546499&status=done&style=none&taskId=ubb731d8b-0f1f-4354-9286-0c001e4420b&title=&width=996.8)
sync() 会阻塞住，只有当别的线程建立连接后，才会向下执行

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650949788057-fdfc2ce2-1941-4aaa-9f8f-ebd98f9e89f5.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=483&id=u6492864b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=604&originWidth=1084&originalType=binary&ratio=1&rotation=0&showTitle=false&size=399905&status=done&style=none&taskId=u9aa7abaa-0366-4101-86a8-890fcc3d2f0&title=&width=867.2)

客户端持续输入
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650950041897-090f1c53-7321-46fd-840d-cb924fb8b7ef.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=673&id=u62cfe402&margin=%5Bobject%20Object%5D&name=image.png&originHeight=841&originWidth=1182&originalType=binary&ratio=1&rotation=0&showTitle=false&size=547985&status=done&style=none&taskId=u8a67e526-7976-41f4-a8ae-2957f995736&title=&width=945.6)
关闭处理
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650950301272-214d0565-1b6c-44c6-9cc6-81a82462d069.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=303&id=u72d7517a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=379&originWidth=994&originalType=binary&ratio=1&rotation=0&showTitle=false&size=237598&status=done&style=none&taskId=u7898c540-42ae-42a5-8a71-69a62252460&title=&width=795.2)
停止客户端enventloop线程
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650950391459-8c6a30ea-3a5d-4f94-b5cd-e9bb81e9df34.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=218&id=u8e1580f2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=272&originWidth=960&originalType=binary&ratio=1&rotation=0&showTitle=false&size=237801&status=done&style=none&taskId=ua5121adb-8974-4cbf-bd98-ac70dcc6d85&title=&width=768)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650950403629-5ff0720a-a019-48bf-a2b2-6b6b4cef3815.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=348&id=u341d4079&margin=%5Bobject%20Object%5D&name=image.png&originHeight=435&originWidth=936&originalType=binary&ratio=1&rotation=0&showTitle=false&size=247001&status=done&style=none&taskId=u43d0e5ef-1583-473e-82fe-1a73c39260a&title=&width=748.8)

为什么异步
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650950646583-e965473d-0cb1-4f6f-88b9-9ac250808a81.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=411&id=u58d8ba28&margin=%5Bobject%20Object%5D&name=image.png&originHeight=514&originWidth=1106&originalType=binary&ratio=1&rotation=0&showTitle=false&size=250432&status=done&style=none&taskId=u951a5c66-71c5-4bf7-bb68-81335b14c11&title=&width=884.8)


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650950633575-efebd0bf-aac2-42ff-91a0-fbfcf38d95f3.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=537&id=u929b7891&margin=%5Bobject%20Object%5D&name=image.png&originHeight=671&originWidth=556&originalType=binary&ratio=1&rotation=0&showTitle=false&size=308964&status=done&style=none&taskId=ua6f6b709-b697-449a-a94f-e0396e18444&title=&width=444.8)


### Future & Promise

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650950693270-c300fc90-b390-4e10-954e-f0f60c8c500f.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=230&id=u6220bf6b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=287&originWidth=1130&originalType=binary&ratio=1&rotation=0&showTitle=false&size=324278&status=done&style=none&taskId=u3a257709-888c-48cc-88ae-6ba14902efe&title=&width=904)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650950836403-6975793b-8cb8-486b-b5ec-7ebc9de6f5f9.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=696&id=u66fd9255&margin=%5Bobject%20Object%5D&name=image.png&originHeight=870&originWidth=1151&originalType=binary&ratio=1&rotation=0&showTitle=false&size=466026&status=done&style=none&taskId=u7ffc5ed5-6998-4cce-8931-57191c6eed9&title=&width=920.8)

jdk
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650950965810-21c6fe60-f1d3-47a0-a1ac-7770bcbbe489.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=558&id=u3c0db12e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=697&originWidth=1210&originalType=binary&ratio=1&rotation=0&showTitle=false&size=384914&status=done&style=none&taskId=u00a9c70a-afae-4736-a170-38a703d01dd&title=&width=968)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650951039871-93926ca8-ed42-479f-89f0-de56207e5393.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=80&id=ua22618f7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=100&originWidth=774&originalType=binary&ratio=1&rotation=0&showTitle=false&size=99553&status=done&style=none&taskId=ubda9a584-b0b1-465c-9354-c78842863b3&title=&width=619.2)


enventloop

- 同步

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650951220464-f85e3f98-50d7-4185-92eb-4838f9a2e1e7.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=432&id=u0b4bf859&margin=%5Bobject%20Object%5D&name=image.png&originHeight=540&originWidth=916&originalType=binary&ratio=1&rotation=0&showTitle=false&size=305417&status=done&style=none&taskId=ua8bd6cf9-ad55-4152-b217-17c4b4b51a6&title=&width=732.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650951314226-82324130-bb1b-4228-ab78-b2bb5329ba91.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=80&id=u75598540&margin=%5Bobject%20Object%5D&name=image.png&originHeight=100&originWidth=894&originalType=binary&ratio=1&rotation=0&showTitle=false&size=115366&status=done&style=none&taskId=u95a16e1e-9f6b-4a16-b4fe-7d3d5549ff4&title=&width=715.2)

- 异步

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650951276104-2bf3b9b9-28cb-40b9-8b9e-9a1f6e1c8b32.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=474&id=u49d56cd5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=593&originWidth=1102&originalType=binary&ratio=1&rotation=0&showTitle=false&size=380892&status=done&style=none&taskId=udb60da4d-6bff-4a1d-b436-4d623081493&title=&width=881.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650951297764-4db05da7-0d74-4f4e-b632-7f9432f099d6.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=63&id=u8142e413&margin=%5Bobject%20Object%5D&name=image.png&originHeight=79&originWidth=917&originalType=binary&ratio=1&rotation=0&showTitle=false&size=96924&status=done&style=none&taskId=u6df2bdff-e360-41a9-b827-ef02e325680&title=&width=733.6)


promise
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650951654712-72be8757-ef4d-404e-bad3-954ed5b3f166.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=678&id=u80252ad7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=847&originWidth=1070&originalType=binary&ratio=1&rotation=0&showTitle=false&size=598663&status=done&style=none&taskId=u35c2e504-4510-40b2-bc89-6602bcf5c5c&title=&width=856)


### Handler & Pipeline

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650951809155-6b617387-6e0c-4e15-8740-cccc5c8100b5.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=196&id=u2295024d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=245&originWidth=1112&originalType=binary&ratio=1&rotation=0&showTitle=false&size=252003&status=done&style=none&taskId=u512f1572-ade3-4f57-a94f-26f24529a80&title=&width=889.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650951895337-4a22c176-bb3b-4804-8863-351adee769d3.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=666&id=u7241e5d0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=833&originWidth=1430&originalType=binary&ratio=1&rotation=0&showTitle=false&size=622877&status=done&style=none&taskId=u8443685d-f2ed-4387-8d4f-47c58a77b05&title=&width=1144)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650952005440-23bbf6f0-69d0-4d3a-bc31-2faf484fde29.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=451&id=u40d9616b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=564&originWidth=1210&originalType=binary&ratio=1&rotation=0&showTitle=false&size=502779&status=done&style=none&taskId=u119e4319-cdf8-4e55-91ba-fa63017faa9&title=&width=968)
入站从前往后，出站从后往前

模拟入站出站
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650952557494-a0f044d8-307b-4c4a-ac67-aa364eea35dc.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=507&id=u6215fca5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=634&originWidth=1319&originalType=binary&ratio=1&rotation=0&showTitle=false&size=431628&status=done&style=none&taskId=u90e9b1f7-6627-4b9c-b9af-4d59a9441df&title=&width=1055.2)


### ByteBuf

---

- 创建

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650952645252-a5b27e32-a116-4de9-a6ac-608555a23683.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=476&id=uab203852&margin=%5Bobject%20Object%5D&name=image.png&originHeight=595&originWidth=1089&originalType=binary&ratio=1&rotation=0&showTitle=false&size=389224&status=done&style=none&taskId=ufa9eef9a-d8da-4d2c-b262-de575739080&title=&width=871.2)

- 直接内存和堆内存

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650952716251-3c4314c5-5594-4819-b1f0-fa2b50435eea.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=351&id=u4e8de1bb&margin=%5Bobject%20Object%5D&name=image.png&originHeight=439&originWidth=1116&originalType=binary&ratio=1&rotation=0&showTitle=false&size=329913&status=done&style=none&taskId=ua316739b-daa7-47ae-b3c5-30fd3035f9e&title=&width=892.8)

- 池化和非池化

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650952822914-0c26ad0b-edf3-42b4-a142-253b217c9eec.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=416&id=u53e39543&margin=%5Bobject%20Object%5D&name=image.png&originHeight=520&originWidth=1152&originalType=binary&ratio=1&rotation=0&showTitle=false&size=421796&status=done&style=none&taskId=u4c879384-0964-4a46-a06d-70c6ddcdff5&title=&width=921.6)

- 写入方法

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650953084130-b34ee406-a45b-45e4-9196-d1fbd0980fb6.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=674&id=u0c1f6b3e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=842&originWidth=1139&originalType=binary&ratio=1&rotation=0&showTitle=false&size=426507&status=done&style=none&taskId=uc9fcd528-63fb-4804-b2eb-31b03e85b4a&title=&width=911.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650953151037-6956e172-3feb-4d86-9daa-60c8836a6335.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=205&id=ue96240a7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=256&originWidth=1131&originalType=binary&ratio=1&rotation=0&showTitle=false&size=208389&status=done&style=none&taskId=u3fd91d80-b9dc-4852-b09f-b07f8527872&title=&width=904.8)

- 垃圾回收

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650953245438-e360449e-c128-43d9-af18-cdcdd070cc98.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=137&id=u8b1dc935&margin=%5Bobject%20Object%5D&name=image.png&originHeight=171&originWidth=924&originalType=binary&ratio=1&rotation=0&showTitle=false&size=169227&status=done&style=none&taskId=uc55d5f65-dcfd-4f5a-b753-63f90419fc1&title=&width=739.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650953290728-0814091f-cd98-4ce9-a178-a6aabe2fb387.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=206&id=u3862121a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=257&originWidth=1116&originalType=binary&ratio=1&rotation=0&showTitle=false&size=256309&status=done&style=none&taskId=ua95ae5d5-1b7f-47f4-a838-4f60a3102dd&title=&width=892.8)
头尾释放内存

slice零拷贝的体现![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650953637355-10ba382b-2a37-4e88-be71-5d5e905623d4.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=494&id=u36eb5dc1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=618&originWidth=984&originalType=binary&ratio=1&rotation=0&showTitle=false&size=333031&status=done&style=none&taskId=u96305653-52ef-4fb7-a258-14ae92d01db&title=&width=787.2)
composite
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650953858106-c505a864-bc6b-471e-b428-e4c3aef585c4.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=425&id=uce2a37c3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=531&originWidth=963&originalType=binary&ratio=1&rotation=0&showTitle=false&size=319395&status=done&style=none&taskId=u382b0890-70c1-4712-b63e-6de7119673d&title=&width=770.4)

优势
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650953925683-989e878e-771b-4efd-a7ab-6cc546c7d418.png#clientId=ue9b8ea73-7a5c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=230&id=u71f7b0b5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=287&originWidth=808&originalType=binary&ratio=1&rotation=0&showTitle=false&size=177868&status=done&style=none&taskId=u0e76e560-92ae-4304-8f49-cad5a9cb539&title=&width=646.4)
