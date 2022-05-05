---


大纲

- 持续集成及jenkins介绍
- jenkins安装和持续集成环境配置
- jekins构建maven项目
- jenkins+docker+springcloud微服务持续集成
- k8s构建jekins持续集成平台


软件开发一般阶段
需求分析-设计-实现-测试-进化

瀑布模型

- 优点：按部就班，为每个项目节点设置检查点
- 缺点：各阶段产生大量文档，开发是线性，增加了开发风险，不适应用户需求的变化

敏捷开发

- 迭代开发+增量开发
- 早期交付，降低风险

持续集成（CI）
让产品快速迭代，并且保持高质量
步骤

- 提交
- 测试
- 构建
- 测试
- 部署
- 回滚

组成要素

- 自动完成
- 代码仓库
- 持续集成服务器



## jekins安装和持续集成环境配置

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651155348125-3246fef0-7123-4aed-a4b1-62390db67781.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=314&id=ufaa33a83&margin=%5Bobject%20Object%5D&name=image.png&originHeight=392&originWidth=1143&originalType=binary&ratio=1&rotation=0&showTitle=false&size=364375&status=done&style=none&taskId=u812120e8-7823-4ae6-ae4d-eb30e0e8a7b&title=&width=914.4)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651155418825-23f5c20a-af96-489d-975c-c65b53a428a8.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=202&id=uc801836e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=253&originWidth=1188&originalType=binary&ratio=1&rotation=0&showTitle=false&size=73250&status=done&style=none&taskId=ua462a5dc-3224-418f-a4c1-1b0845d20e0&title=&width=950.4)


### GitLab的安装

---

gitlab使得代码都保存在自己服务器上，可以看作github的个人版

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651155540763-9b1f57d5-c3c6-4196-bedf-3c7e866b5619.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=506&id=u4252082c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=633&originWidth=970&originalType=binary&ratio=1&rotation=0&showTitle=false&size=147702&status=done&style=none&taskId=u894e6d50-edf3-48cf-af75-6931f5bdb23&title=&width=776)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651155602494-bea3d708-3cd3-4b37-b49e-5d298f35ed30.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=498&id=u1d79b1f5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=623&originWidth=1161&originalType=binary&ratio=1&rotation=0&showTitle=false&size=188405&status=done&style=none&taskId=u64c4e0e7-d8d1-4688-8f06-d3ceba5f352&title=&width=928.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651155631584-3ce6340a-dfda-4128-8138-d12e232d1fab.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=285&id=uf8cee51e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=356&originWidth=853&originalType=binary&ratio=1&rotation=0&showTitle=false&size=68922&status=done&style=none&taskId=u3cd812ce-fb6c-45f1-a8e0-cb980a85e2c&title=&width=682.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651155921375-8346b927-4958-47d8-8104-04093b490dba.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=414&id=uad4d0d20&margin=%5Bobject%20Object%5D&name=image.png&originHeight=518&originWidth=1511&originalType=binary&ratio=1&rotation=0&showTitle=false&size=245440&status=done&style=none&taskId=u2a5946b7-9f90-43c4-8993-e7167477dca&title=&width=1208.8)
这里是更改root账户密码，比如更改为123456
下一个页面就是root账户登陆

之后就是组管理和用户管理了
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651156272162-98790856-33d9-48c4-8c9c-7fbc90f41049.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=271&id=u545fcb73&margin=%5Bobject%20Object%5D&name=image.png&originHeight=339&originWidth=1204&originalType=binary&ratio=1&rotation=0&showTitle=false&size=134989&status=done&style=none&taskId=u25a11399-23cd-421f-9079-347ad28b845&title=&width=963.2)

### 源码推送到gitlab

---

- 在跟目录创建git版本控制（这个时候项目文件会变红）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651156508964-ae67d69c-3784-44f2-87d3-e4dc88bfe092.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=86&id=u3c74d0aa&margin=%5Bobject%20Object%5D&name=image.png&originHeight=107&originWidth=613&originalType=binary&ratio=1&rotation=0&showTitle=false&size=70061&status=done&style=none&taskId=uef31045c-6b21-44cd-90c6-8c15425f22a&title=&width=490.4)

- git add到缓存区（这个时候项目会变绿，显示已经到了缓存区）
- ![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651156553001-79761155-719e-47bd-919c-6005e1cc68b1.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=530&id=ued05bdd9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=662&originWidth=1076&originalType=binary&ratio=1&rotation=0&showTitle=false&size=469847&status=done&style=none&taskId=u168f4ef7-3948-4549-a8d7-df39d5de978&title=&width=860.8)
- - git commit（提交到本地仓库）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651156672910-a8261389-a98f-45e7-ab98-69cb7cf6349a.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=450&id=u4167a911&margin=%5Bobject%20Object%5D&name=image.png&originHeight=563&originWidth=1182&originalType=binary&ratio=1&rotation=0&showTitle=false&size=268071&status=done&style=none&taskId=u6fac494a-37a3-4206-b11f-540618e9f2c&title=&width=945.6)

- 设置远程仓库（比如添加http地址）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651156699551-2d0bc181-5794-4a47-9f18-dd288d324086.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=306&id=u896857d7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=383&originWidth=1134&originalType=binary&ratio=1&rotation=0&showTitle=false&size=347400&status=done&style=none&taskId=u8fbe25f7-0944-46e4-9c87-670478aa9ae&title=&width=907.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651156732950-9303b20f-9371-4ee7-b786-4813b46ada41.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=201&id=u2b85e71f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=251&originWidth=693&originalType=binary&ratio=1&rotation=0&showTitle=false&size=65217&status=done&style=none&taskId=u6176126d-fdf6-4b56-a52f-9e715503634&title=&width=554.4)

- push代码

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651156763414-121d8fb8-2396-4818-a8e0-e0eb159aff27.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=193&id=ud12cc7e8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=241&originWidth=1131&originalType=binary&ratio=1&rotation=0&showTitle=false&size=229277&status=done&style=none&taskId=uce7fb09c-eca3-4d56-a516-8c6a5618e23&title=&width=904.8)


### 持续集成服务器搭建

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651156896051-0c545ed7-f9bc-4c71-aeb6-f0f81ddc607f.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=654&id=u21ffc4e5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=817&originWidth=693&originalType=binary&ratio=1&rotation=0&showTitle=false&size=138813&status=done&style=none&taskId=uf827d49a-ae6e-48b3-88c9-e426da87d9c&title=&width=554.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651156931379-5b78ab33-5244-4f6e-a8a3-f531d9fdd6a7.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=329&id=u32bdea61&margin=%5Bobject%20Object%5D&name=image.png&originHeight=411&originWidth=875&originalType=binary&ratio=1&rotation=0&showTitle=false&size=96267&status=done&style=none&taskId=u36824609-2e1f-4393-a985-0b1eb2d39f8&title=&width=700)
修改用户为root，这样你可以通过root用户来连接， 不然你需要创建一个jekins的用户

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157143096-44ad96ca-eef8-4d9e-8b35-ac28b3806d96.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=406&id=u9ad3b676&margin=%5Bobject%20Object%5D&name=image.png&originHeight=507&originWidth=1381&originalType=binary&ratio=1&rotation=0&showTitle=false&size=241068&status=done&style=none&taskId=u6341a476-a5bd-49e8-abc9-d1557bf51e2&title=&width=1104.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157157437-273f12a7-108d-47ce-84ae-963efd355149.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=51&id=u423ed21f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=64&originWidth=938&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86162&status=done&style=none&taskId=ud405d7e8-081b-4c62-af88-c32083ddee1&title=&width=750.4)

跳过插件安装，之后进去使用国内网站安装
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157238045-fd74d248-c90a-4352-9156-edf0a681852e.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=352&id=u98bab79a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=440&originWidth=907&originalType=binary&ratio=1&rotation=0&showTitle=false&size=76609&status=done&style=none&taskId=u62527317-71d5-432d-aded-9050fa1e51a&title=&width=725.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157257306-5caeb646-6888-4234-9822-2c4ab60a2eed.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=597&id=u646e56d1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=746&originWidth=1300&originalType=binary&ratio=1&rotation=0&showTitle=false&size=214294&status=done&style=none&taskId=u537d65b1-8fdc-4d87-a995-adece930ac8&title=&width=1040)



安装jekins插件
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157325707-aeaeeea6-7b5d-4853-ba5d-12d886545724.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=408&id=u14e6011f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=510&originWidth=950&originalType=binary&ratio=1&rotation=0&showTitle=false&size=185537&status=done&style=none&taskId=u3d794dd5-eadb-4248-87be-67bafc00c9b&title=&width=760)![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157406828-a644bcda-7d11-4bf5-a47f-946aea261d9f.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=508&id=u9922f592&margin=%5Bobject%20Object%5D&name=image.png&originHeight=635&originWidth=1129&originalType=binary&ratio=1&rotation=0&showTitle=false&size=282392&status=done&style=none&taskId=u9cdba22d-e54a-4792-9f7e-e567f913c65&title=&width=903.2)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157556598-b01019c5-0d00-42b7-a9c5-72b2cdc7acfe.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=537&id=u33a70127&margin=%5Bobject%20Object%5D&name=image.png&originHeight=671&originWidth=1173&originalType=binary&ratio=1&rotation=0&showTitle=false&size=234454&status=done&style=none&taskId=u7ff9ccff-1856-4e6e-90d7-8ff004db936&title=&width=938.4)


jekins权限分配

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157684190-7586537a-2704-436e-9660-c0b6782ccb6d.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=699&id=u3ca1d637&margin=%5Bobject%20Object%5D&name=image.png&originHeight=874&originWidth=1201&originalType=binary&ratio=1&rotation=0&showTitle=false&size=407658&status=done&style=none&taskId=ua64983ca-ab3d-4cef-b048-d7a182639c2&title=&width=960.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157738637-0caa91f2-311c-4ae6-b32c-e8a21375d0a5.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=437&id=u49e2228a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=546&originWidth=876&originalType=binary&ratio=1&rotation=0&showTitle=false&size=134801&status=done&style=none&taskId=uf8bf00a0-c057-4262-a4e7-574880635ec&title=&width=700.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157758152-826c12cd-1e9d-4909-b308-6716a082f7ee.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=687&id=u0a985bb9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=859&originWidth=1158&originalType=binary&ratio=1&rotation=0&showTitle=false&size=269602&status=done&style=none&taskId=u2a6e6679-cf51-417c-8dc9-8699fb531c6&title=&width=926.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157863041-13b4d49e-3cfe-40ef-83f5-00949f81c030.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=579&id=u131d714c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=724&originWidth=929&originalType=binary&ratio=1&rotation=0&showTitle=false&size=169979&status=done&style=none&taskId=ud39115df-3c70-47c2-a0c2-764b8d5625f&title=&width=743.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157904103-39fa9e30-f43d-4c7f-ba34-43753babf7a1.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=344&id=ued39c623&margin=%5Bobject%20Object%5D&name=image.png&originHeight=430&originWidth=974&originalType=binary&ratio=1&rotation=0&showTitle=false&size=123335&status=done&style=none&taskId=u4e4dcd0d-8780-4380-9fcb-614cd226ef0&title=&width=779.2)
分配角色给人员
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651157979282-9afcf866-4af0-4a85-b444-3cc7e8f521ea.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=501&id=u0739fc6c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=626&originWidth=773&originalType=binary&ratio=1&rotation=0&showTitle=false&size=139111&status=done&style=none&taskId=u74435c38-bca9-44b6-af39-e2b1066cdd7&title=&width=618.4)
凭证管理
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651158062180-970133ca-471e-4de6-bff0-074fe6c6c50e.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=741&id=u7d05859a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=926&originWidth=1159&originalType=binary&ratio=1&rotation=0&showTitle=false&size=296476&status=done&style=none&taskId=u8582157e-baf1-488e-aa4e-a05b61df5a8&title=&width=927.2)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651158164089-8eb7b6bc-aadb-4286-a88f-17862d75a5ea.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=459&id=u02669766&margin=%5Bobject%20Object%5D&name=image.png&originHeight=574&originWidth=1607&originalType=binary&ratio=1&rotation=0&showTitle=false&size=133495&status=done&style=none&taskId=ub08e016f-2e32-42f0-95e8-4367d7b5874&title=&width=1285.6)


拉取gitlab项目
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651158252303-1303f28a-2409-46e4-8033-626b390fab27.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=635&id=u6006f311&margin=%5Bobject%20Object%5D&name=image.png&originHeight=794&originWidth=975&originalType=binary&ratio=1&rotation=0&showTitle=false&size=277555&status=done&style=none&taskId=ue5f38d3f-394b-49bd-8b8b-7d07d22675a&title=&width=780)


- 添加凭证

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651158340080-a71c4f91-6e33-4ad3-8fad-366a2f2add77.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=457&id=u653ceda2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=571&originWidth=1425&originalType=binary&ratio=1&rotation=0&showTitle=false&size=116045&status=done&style=none&taskId=u4da3b17a-f054-4251-8fda-7620696e855&title=&width=1140)

- 项目源码管理

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651158381434-88cdcfd1-c818-4656-8fe7-1283db43dd11.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=346&id=u10dd4183&margin=%5Bobject%20Object%5D&name=image.png&originHeight=432&originWidth=1455&originalType=binary&ratio=1&rotation=0&showTitle=false&size=148726&status=done&style=none&taskId=u76db2017-fc2a-4b96-a9e2-ec2ce3ff78c&title=&width=1164)

- build

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651158428808-2ea66fff-6d1f-411b-ad29-927fe17dd577.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=610&id=uf1472887&margin=%5Bobject%20Object%5D&name=image.png&originHeight=763&originWidth=1644&originalType=binary&ratio=1&rotation=0&showTitle=false&size=740819&status=done&style=none&taskId=u4cadf6d1-e28c-4faa-b56c-e04a5107270&title=&width=1315.2)


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651158542892-8897c57b-173a-47c4-8117-eab21d1385f4.png#clientId=u9c4053cb-1d9e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=648&id=u6148106f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=810&originWidth=1003&originalType=binary&ratio=1&rotation=0&showTitle=false&size=184430&status=done&style=none&taskId=udb4b3653-4d34-4955-bf0e-780b2b3b458&title=&width=802.4)
复制公钥到gitlab
复制私钥到jenkins


maven环境配置

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651204364321-0ce4d66a-841f-4073-a5f8-705994b28543.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=542&id=ufb8f0b00&margin=%5Bobject%20Object%5D&name=image.png&originHeight=678&originWidth=1087&originalType=binary&ratio=1&rotation=0&showTitle=false&size=197542&status=done&style=none&taskId=u01d2b492-1bd5-4f49-9457-80ab87af721&title=&width=869.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651204491056-ada72506-7dc0-4c53-bb82-f7e140aa2dbd.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=532&id=ufd3c31d6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=665&originWidth=1172&originalType=binary&ratio=1&rotation=0&showTitle=false&size=145468&status=done&style=none&taskId=u5dbf05c8-5996-462d-ae81-e697cf978bd&title=&width=937.6)
新增环境变量
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651204584732-b6fa2cb4-4893-4ebe-8a0f-bb5266d48b56.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=614&id=u204a31ff&margin=%5Bobject%20Object%5D&name=image.png&originHeight=767&originWidth=1168&originalType=binary&ratio=1&rotation=0&showTitle=false&size=172107&status=done&style=none&taskId=u79ec4434-b6a0-4438-91d2-c845071f439&title=&width=934.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651204635994-a701f578-c49e-491a-a28f-a07d69933bac.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=449&id=uf9c4714f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=561&originWidth=928&originalType=binary&ratio=1&rotation=0&showTitle=false&size=156682&status=done&style=none&taskId=uba5e70bf-1afe-4d5e-a08c-bd555526749&title=&width=742.4)

测试
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651204727603-168859bb-2ef6-4331-a9aa-af464caf0cc4.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=286&id=ua3f236e6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=357&originWidth=1018&originalType=binary&ratio=1&rotation=0&showTitle=false&size=46281&status=done&style=none&taskId=udc76a2b5-27cc-42e7-aa58-850069274d6&title=&width=814.4)


### Tomcat服务器安装和配置

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651204807806-4b92c632-772b-46c2-8a71-ade5aa9841ce.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=522&id=ucebb7a52&margin=%5Bobject%20Object%5D&name=image.png&originHeight=653&originWidth=866&originalType=binary&ratio=1&rotation=0&showTitle=false&size=187309&status=done&style=none&taskId=u9da38686-7940-44b5-91fd-200d0a7ddf6&title=&width=692.8)
添加tomcat角色，开启远程访问功能
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651204921616-d0279fff-525a-4fdd-87e5-3f97a4727a03.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=726&id=ude3954bc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=908&originWidth=1242&originalType=binary&ratio=1&rotation=0&showTitle=false&size=488212&status=done&style=none&taskId=ubc2274b3-1125-43ec-850d-63fc4b9a48a&title=&width=993.6)


## jekins构建maven项目

---


构建风格类型

- 自由风格类型
- maven项目
- 流水线项目


### 自由风格项目构建

---

- 拉取代码
- 编译打包

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651211365431-39affa98-5433-4897-990f-c36e04259cb4.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=313&id=ub40952be&margin=%5Bobject%20Object%5D&name=image.png&originHeight=391&originWidth=927&originalType=binary&ratio=1&rotation=0&showTitle=false&size=80587&status=done&style=none&taskId=u926e194f-2f64-458e-84c5-e95b1911490&title=&width=741.6)

- 部署

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651211419775-ac3237be-ccbc-4cd6-ba01-48ece96611f4.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=602&id=u31c70d94&margin=%5Bobject%20Object%5D&name=image.png&originHeight=752&originWidth=1001&originalType=binary&ratio=1&rotation=0&showTitle=false&size=206502&status=done&style=none&taskId=u29e372b2-fc0c-4076-8874-b22ad21f7b4&title=&width=800.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651211524108-b3444071-8523-4208-80a1-ee417fa7da49.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=529&id=u0649ebc0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=661&originWidth=1335&originalType=binary&ratio=1&rotation=0&showTitle=false&size=203572&status=done&style=none&taskId=u4590a30b-4ead-47f1-997b-12d1f2a76c4&title=&width=1068)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651211567070-b6cbef3e-56e2-4b3f-869c-f4ca5fc18bc6.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=112&id=u734f2d4d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=140&originWidth=880&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86648&status=done&style=none&taskId=u16b44d6a-cbed-49b5-abf2-1b06129409b&title=&width=704)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651211620127-5eebdb26-78cc-4fd5-9142-4a4965fe8a02.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=226&id=u99fc5a5c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=283&originWidth=646&originalType=binary&ratio=1&rotation=0&showTitle=false&size=38835&status=done&style=none&taskId=uac71f97e-4c59-4661-8084-e3eb58c70e5&title=&width=516.8)

### maven项目风格构建

---


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651211739294-faf53853-74e2-43a0-9afa-75e855389bcf.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=603&id=u1dc569ce&margin=%5Bobject%20Object%5D&name=image.png&originHeight=754&originWidth=730&originalType=binary&ratio=1&rotation=0&showTitle=false&size=340447&status=done&style=none&taskId=uf69bf1ab-1e1a-40f8-ab2b-56cd2f700a3&title=&width=584)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651211865200-834c6620-f30c-4957-b7b3-c68fcd03316f.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=240&id=u68ef8ed8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=300&originWidth=1060&originalType=binary&ratio=1&rotation=0&showTitle=false&size=44502&status=done&style=none&taskId=uf1fe470d-00ef-4dc1-8d30-1e736a94d62&title=&width=848)


### pipeline项目风格构建

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651212021481-880049c0-718f-4af5-984b-93b4d30d5404.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=263&id=u3b7b4a15&margin=%5Bobject%20Object%5D&name=image.png&originHeight=329&originWidth=1205&originalType=binary&ratio=1&rotation=0&showTitle=false&size=175432&status=done&style=none&taskId=ueaeff949-a14a-46f2-996e-1dc2e145d08&title=&width=964)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651212095130-aaef2339-c74b-4b67-a1cf-e345f88ddbaf.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=703&id=uba0e40ae&margin=%5Bobject%20Object%5D&name=image.png&originHeight=879&originWidth=816&originalType=binary&ratio=1&rotation=0&showTitle=false&size=363681&status=done&style=none&taskId=uc435563b-8d69-4a66-8bf0-845ef7b08d9&title=&width=652.8)


- 声明式

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651212328276-28a2015d-7ad0-4a71-802f-0b35e0d19e69.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=440&id=u5b1f4c4e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=550&originWidth=785&originalType=binary&ratio=1&rotation=0&showTitle=false&size=127199&status=done&style=none&taskId=u424f9b00-ed6e-4cf1-a58d-4baf4a99d0f&title=&width=628)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651212346020-f3cdcb94-78fa-418c-99c4-f2b51ace9324.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=298&id=u0c1993c6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=373&originWidth=990&originalType=binary&ratio=1&rotation=0&showTitle=false&size=127063&status=done&style=none&taskId=u11ef1f87-553d-4029-b163-5396f5135ff&title=&width=792)

- 脚本式

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651212403616-8d9ec5e6-eb98-420e-ac91-4e94583c1c89.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=252&id=ub80c4639&margin=%5Bobject%20Object%5D&name=image.png&originHeight=315&originWidth=609&originalType=binary&ratio=1&rotation=0&showTitle=false&size=97947&status=done&style=none&taskId=u019322a5-eb37-4f9e-8380-847217096f5&title=&width=487.2)


具体流程

拉取代码

- 片段生成器

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651212545194-c355013b-982a-4eef-994c-3f2041c66ae2.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=368&id=u9eba7490&margin=%5Bobject%20Object%5D&name=image.png&originHeight=460&originWidth=1374&originalType=binary&ratio=1&rotation=0&showTitle=false&size=129502&status=done&style=none&taskId=u35682515-fcb8-4576-a973-8b808624e87&title=&width=1099.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651212578200-0ad53d34-64c9-4611-b9c4-69ef83da05eb.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=168&id=u8720639b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=210&originWidth=1407&originalType=binary&ratio=1&rotation=0&showTitle=false&size=155858&status=done&style=none&taskId=u48bfe897-a5c3-46ad-bd50-bd665c7d724&title=&width=1125.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651212597580-61669fcb-60b5-4c9b-978a-5f4e7d98c6d0.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=293&id=u1846d31f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=366&originWidth=1174&originalType=binary&ratio=1&rotation=0&showTitle=false&size=109664&status=done&style=none&taskId=ud00e3572-73ae-4257-bf72-7e6d4bb544d&title=&width=939.2)


编译打包

- 代码生成器

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651212902463-00226d5b-06d3-455f-a4db-5cf8368f44fd.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=368&id=ua5592458&margin=%5Bobject%20Object%5D&name=image.png&originHeight=460&originWidth=1088&originalType=binary&ratio=1&rotation=0&showTitle=false&size=53190&status=done&style=none&taskId=u1c36ecdc-0b7a-48a5-a3ef-ddb8f0a0973&title=&width=870.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651212927148-2188a704-5049-48a6-a19e-4ce0e5154d18.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=297&id=u190594f7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=371&originWidth=1110&originalType=binary&ratio=1&rotation=0&showTitle=false&size=121980&status=done&style=none&taskId=ueee12e36-c931-4047-b8f9-089bb7fb979&title=&width=888)

- 直接执行shell脚本

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651212954306-643a5fa1-30de-406a-9e49-a02525b9644f.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=303&id=u16cb729a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=379&originWidth=1006&originalType=binary&ratio=1&rotation=0&showTitle=false&size=118167&status=done&style=none&taskId=uf7ea7c73-5a65-4ef7-a50d-bbbf0ed02c3&title=&width=804.8)

部署

- 代码生成器

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651213002165-99d19167-5bb4-4217-9de3-7d398f8381cd.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=421&id=u7702d8e6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=526&originWidth=1274&originalType=binary&ratio=1&rotation=0&showTitle=false&size=136087&status=done&style=none&taskId=u2d76d354-3687-4e01-b057-a98e8418114&title=&width=1019.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651213025871-b8bd19e5-a597-4dd6-80e8-c0ce50722866.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=372&id=u4d2d56ac&margin=%5Bobject%20Object%5D&name=image.png&originHeight=465&originWidth=1316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=214919&status=done&style=none&taskId=u0bd74d17-735d-4411-89b2-4cb51c22875&title=&width=1052.8)

本地保存脚本
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651213197072-97a77c6d-a1bd-414c-adf3-6b5d33f95c97.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=534&id=u6bc63a2e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=668&originWidth=1872&originalType=binary&ratio=1&rotation=0&showTitle=false&size=346614&status=done&style=none&taskId=u144a2ec4-28af-47d7-b84b-6c9426ea331&title=&width=1497.6)
执行脚本
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651213439779-496c7f13-417e-4e92-bf0e-252203c70692.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=553&id=u1dca05d2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=691&originWidth=1404&originalType=binary&ratio=1&rotation=0&showTitle=false&size=220714&status=done&style=none&taskId=ue50d9acc-1147-4699-a860-f5a83f807e2&title=&width=1123.2)



构建细节-常见构建触发器

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651213658528-0d48de17-d2fd-4d87-bc05-3c3e8bb72f0a.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=232&id=u96757f73&margin=%5Bobject%20Object%5D&name=image.png&originHeight=290&originWidth=934&originalType=binary&ratio=1&rotation=0&showTitle=false&size=57271&status=done&style=none&taskId=ufb7cd5f8-357e-4103-99bf-2d0ab92d5a0&title=&width=747.2)

- 触发远程构建

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651213760584-c0a318bf-c458-4128-9085-88e3db4296ed.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=146&id=u663f1cb3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=182&originWidth=1194&originalType=binary&ratio=1&rotation=0&showTitle=false&size=180446&status=done&style=none&taskId=u31405673-de8c-4b6c-aec8-d0d4ac15bbc&title=&width=955.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651213802716-405ab976-8ae5-4d91-a2ec-4cec88c6d3c3.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=84&id=uf2ce31dd&margin=%5Bobject%20Object%5D&name=image.png&originHeight=105&originWidth=1008&originalType=binary&ratio=1&rotation=0&showTitle=false&size=107769&status=done&style=none&taskId=u97f11ba7-dca9-41d3-991c-4dd694c84fb&title=&width=806.4)

- 其他工程构建后触发

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651213876050-c5589dd7-7a50-4db8-92c6-8bed6a0f595d.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=166&id=u233377f8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=207&originWidth=888&originalType=binary&ratio=1&rotation=0&showTitle=false&size=73746&status=done&style=none&taskId=u56019036-1774-4818-aa1d-666e75ea6e4&title=&width=710.4)

- 定时构建

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651213948706-5368f8c0-3b8c-4064-912c-4ba27aa933c3.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=711&id=uaacad5d3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=889&originWidth=838&originalType=binary&ratio=1&rotation=0&showTitle=false&size=206344&status=done&style=none&taskId=u1b94e932-eedd-4334-a209-9120fd26d29&title=&width=670.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651214118383-fd58808d-aae2-4986-b48d-e142f30bcfd3.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=168&id=u306fde86&margin=%5Bobject%20Object%5D&name=image.png&originHeight=210&originWidth=627&originalType=binary&ratio=1&rotation=0&showTitle=false&size=23797&status=done&style=none&taskId=uca5c5ab2-e15e-46a0-97ca-0fec8de309e&title=&width=501.6)
隔两分钟构建一次

- 轮询SCM

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651214171569-098c36dd-03f2-4118-a657-25931b94b1de.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=327&id=u19218b96&margin=%5Bobject%20Object%5D&name=image.png&originHeight=409&originWidth=1085&originalType=binary&ratio=1&rotation=0&showTitle=false&size=160490&status=done&style=none&taskId=u598541d8-1b39-4b07-9c86-67fd67b1ce6&title=&width=868)



jekins构建细节（gitlab hook）

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651214354941-ee6090a3-32de-4d20-984b-72b83421b01e.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=340&id=u8d256e31&margin=%5Bobject%20Object%5D&name=image.png&originHeight=425&originWidth=846&originalType=binary&ratio=1&rotation=0&showTitle=false&size=112974&status=done&style=none&taskId=u26373656-a5ce-4df5-82e6-ed7be71ee6e&title=&width=676.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651214374268-36954139-e698-414b-823d-74815244a786.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=467&id=u27397c65&margin=%5Bobject%20Object%5D&name=image.png&originHeight=584&originWidth=955&originalType=binary&ratio=1&rotation=0&showTitle=false&size=239419&status=done&style=none&taskId=u57787070-e8ab-4105-a875-8ecc059f1c7&title=&width=764)
配置jenkins
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651214640096-69164bd3-19bc-4bf4-94fb-db96f9c7e2f5.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=492&id=ude669959&margin=%5Bobject%20Object%5D&name=image.png&originHeight=615&originWidth=1438&originalType=binary&ratio=1&rotation=0&showTitle=false&size=289763&status=done&style=none&taskId=u97c1df48-09e0-4a98-a560-b56a1a95fc6&title=&width=1150.4)
配置gitlab
开启web hook
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651214703401-fcfec785-5c3b-4129-ba3a-ef7ab8f86a5b.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=342&id=udffdb1f6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=428&originWidth=1263&originalType=binary&ratio=1&rotation=0&showTitle=false&size=207965&status=done&style=none&taskId=ue01e5a0e-ed6c-4ff4-806f-32866e8c82d&title=&width=1010.4)
配置项目setting
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651214739562-4bb4fbe5-f995-403e-a181-daeecfea66e4.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=630&id=u1daa3f02&margin=%5Bobject%20Object%5D&name=image.png&originHeight=787&originWidth=1325&originalType=binary&ratio=1&rotation=0&showTitle=false&size=334307&status=done&style=none&taskId=ufc560928-b932-4420-b7e4-623d8082c05&title=&width=1060)
关闭jenkins的认证
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651214908476-3f381e0c-9b40-4d04-a46a-05cd744647d7.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=118&id=u63b2e50c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=148&originWidth=948&originalType=binary&ratio=1&rotation=0&showTitle=false&size=45246&status=done&style=none&taskId=u5caf6b3f-a217-4a40-93b4-1f5a9eb39d9&title=&width=758.4)



jekins构建细节-参数化构建

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651215512988-06c425b9-3f0a-450f-8cf3-467a2e19b87f.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=345&id=u32644862&margin=%5Bobject%20Object%5D&name=image.png&originHeight=431&originWidth=713&originalType=binary&ratio=1&rotation=0&showTitle=false&size=96226&status=done&style=none&taskId=ud63b1d48-95d9-4c05-9faa-f6f439183a3&title=&width=570.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651215640061-cc992ab3-5643-4686-b5ee-9cbb8c4aed97.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=482&id=u754b7e5c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=603&originWidth=1131&originalType=binary&ratio=1&rotation=0&showTitle=false&size=212095&status=done&style=none&taskId=u160b9625-e698-45c9-9e6d-4c82529a10c&title=&width=904.8)



jenkins构建细节--配置邮箱服务器发送构建结果

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651215859711-30d152c0-52b2-4f3c-97b2-7acb1ebbbcfc.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=524&id=u730086ee&margin=%5Bobject%20Object%5D&name=image.png&originHeight=655&originWidth=1194&originalType=binary&ratio=1&rotation=0&showTitle=false&size=259045&status=done&style=none&taskId=u814c9934-a3bf-4260-98e5-00e4cd20273&title=&width=955.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651216076689-c74c4533-d501-4a8e-b68e-73a2de718105.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=553&id=u331b9941&margin=%5Bobject%20Object%5D&name=image.png&originHeight=691&originWidth=1270&originalType=binary&ratio=1&rotation=0&showTitle=false&size=142992&status=done&style=none&taskId=u6425d03a-7f4a-44b0-887e-a8f08803a1b&title=&width=1016)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651216190533-52ec410f-6265-404c-9630-e4783262ae75.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=436&id=u29fd0673&margin=%5Bobject%20Object%5D&name=image.png&originHeight=545&originWidth=1022&originalType=binary&ratio=1&rotation=0&showTitle=false&size=142413&status=done&style=none&taskId=ubab63a15-a496-4fe8-b0df-7674ab7a9b1&title=&width=817.6)

针对项目定制邮件模板
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651216261611-281d0727-26c5-43b3-9fc3-f4ef3cf5db57.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=390&id=u831c68d6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=488&originWidth=1623&originalType=binary&ratio=1&rotation=0&showTitle=false&size=532396&status=done&style=none&taskId=ube4470d4-256f-4d49-828e-061f8eb124d&title=&width=1298.4)
jenkins中post
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651216323815-44593691-372d-4810-8713-d67440c742b9.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=673&id=ued13e256&margin=%5Bobject%20Object%5D&name=image.png&originHeight=841&originWidth=1275&originalType=binary&ratio=1&rotation=0&showTitle=false&size=366622&status=done&style=none&taskId=u4e4cdf22-ac04-44f7-94e9-e093e4dd674&title=&width=1020)


代码审查（sonarqube）

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651216597298-ee04a2ee-3b7a-49c1-bd45-e772a6e011fc.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=508&id=u87baeee9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=635&originWidth=556&originalType=binary&ratio=1&rotation=0&showTitle=false&size=161356&status=done&style=none&taskId=u97ec9eaf-61e3-4e1a-b4ed-fd80b8f3c87&title=&width=444.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651216650166-bbc36c69-8a4c-4020-8cc5-d8e9a03a66ed.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=678&id=u0c670c4e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=848&originWidth=1189&originalType=binary&ratio=1&rotation=0&showTitle=false&size=220305&status=done&style=none&taskId=ub5860903-3e22-4eb9-9c50-53092b934b8&title=&width=951.2)
切换到sonar账户
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651216848426-4443d369-7329-4fca-88e1-b4195f1a5555.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=68&id=u59b81b94&margin=%5Bobject%20Object%5D&name=image.png&originHeight=85&originWidth=964&originalType=binary&ratio=1&rotation=0&showTitle=false&size=68254&status=done&style=none&taskId=u408b691e-8f03-4a92-b17e-e7faab395d9&title=&width=771.2)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651216902589-904912c3-78bb-4163-9943-9dad5a349bb5.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=463&id=u4a8cc51e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=579&originWidth=829&originalType=binary&ratio=1&rotation=0&showTitle=false&size=161048&status=done&style=none&taskId=uded208a0-6237-4144-b8d3-da6b2a10e67&title=&width=663.2)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651216947922-829035b6-4be5-4031-b966-52bbf970f770.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=268&id=uc0217e9b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=335&originWidth=1170&originalType=binary&ratio=1&rotation=0&showTitle=false&size=114022&status=done&style=none&taskId=u58f89ff4-bb01-4c80-b393-88fd16c2b96&title=&width=936)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651217022245-f52cd997-eb4b-4599-aafa-5c29d6ae1df6.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=543&id=u06c7fffc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=679&originWidth=770&originalType=binary&ratio=1&rotation=0&showTitle=false&size=202414&status=done&style=none&taskId=ucdb8b87b-ff29-4430-bbdf-802b206d99d&title=&width=616)
jenkins安装solarcobe
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651217084531-9f0868ed-7242-473a-9fcf-fb5312854b2c.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=512&id=udaf1fe6f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=640&originWidth=1326&originalType=binary&ratio=1&rotation=0&showTitle=false&size=194094&status=done&style=none&taskId=u4bcc436d-ba5d-4431-9e19-f10203c0ae5&title=&width=1060.8)

非流水线项目代码审查

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651217394751-4155d461-f67b-43a3-a13c-acdc99f85344.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=566&id=u3783360c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=708&originWidth=1223&originalType=binary&ratio=1&rotation=0&showTitle=false&size=366515&status=done&style=none&taskId=u68e49d07-f75b-41f9-9e6f-f2464c3226c&title=&width=978.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651217440996-a869746f-4e04-407e-b740-3e8d63badf1f.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=178&id=u1e853c1a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=222&originWidth=1393&originalType=binary&ratio=1&rotation=0&showTitle=false&size=103106&status=done&style=none&taskId=u053ec2f0-7c98-417b-a226-2646d77806e&title=&width=1114.4)


流水线项目

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651217587758-1cdf1dd3-5359-492e-b179-8d110e2affa0.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=419&id=u0fb662f9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=524&originWidth=1133&originalType=binary&ratio=1&rotation=0&showTitle=false&size=358895&status=done&style=none&taskId=uaa4d912b-04e5-4670-86f0-014fb24b957&title=&width=906.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651217641751-9c8a74e0-df51-4ae0-abe2-017fb97422d7.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=558&id=u5f69f5c4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=698&originWidth=1163&originalType=binary&ratio=1&rotation=0&showTitle=false&size=258751&status=done&style=none&taskId=u80f4138d-41cc-4eea-8b4d-c8dd32f625c&title=&width=930.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651217739388-22986652-c65a-459f-834a-b57cfabe06c2.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=170&id=uefe1e14e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=213&originWidth=1406&originalType=binary&ratio=1&rotation=0&showTitle=false&size=113334&status=done&style=none&taskId=u4575d666-f458-487a-8bd2-1de01d14d6e&title=&width=1124.8)


## Jenkins + Docker + springcloud集成

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651468391058-e9c66641-9fe9-484b-8e68-e249351aa793.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=518&id=uf562dd6e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=647&originWidth=1171&originalType=binary&ratio=1&rotation=0&showTitle=false&size=467069&status=done&style=none&taskId=u25d7240f-1030-4526-a7c5-66cbdeab971&title=&width=936.8)


### springcloud微服务部署

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651468634677-0257101c-9b47-4d57-a098-b1891d100546.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=440&id=ue4e2a216&margin=%5Bobject%20Object%5D&name=image.png&originHeight=550&originWidth=1199&originalType=binary&ratio=1&rotation=0&showTitle=false&size=201840&status=done&style=none&taskId=u6e8b2d8d-8579-44da-abe0-dc6de2ec493&title=&width=959.2)
父工程build配置
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651468760715-3c9f926b-dbbf-40b8-ba49-0924ab249ba0.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=192&id=u99e2bc3b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=240&originWidth=902&originalType=binary&ratio=1&rotation=0&showTitle=false&size=121955&status=done&style=none&taskId=uc366b988-180a-4274-92d4-54774d91600&title=&width=721.6)

### 前端部署
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651468848043-be635da7-9104-4389-b769-8388d58aecc0.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=556&id=u01b9821c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=695&originWidth=907&originalType=binary&ratio=1&rotation=0&showTitle=false&size=263289&status=done&style=none&taskId=ub0daf2c4-5846-4070-9f8a-bcaa6dd39de&title=&width=725.6)


### Docker搭建镜像

---

下载docker
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651469211555-0c67316d-2bcd-4f32-b2fd-1c51fb02ad5c.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=618&id=u77d89c92&margin=%5Bobject%20Object%5D&name=image.png&originHeight=772&originWidth=1165&originalType=binary&ratio=1&rotation=0&showTitle=false&size=195710&status=done&style=none&taskId=u49b43046-891c-4cf7-a0ee-6aa05bfaebb&title=&width=932)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651469284073-4c680039-3575-4536-807a-645f0976bc57.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=706&id=u10b2cc32&margin=%5Bobject%20Object%5D&name=image.png&originHeight=882&originWidth=1087&originalType=binary&ratio=1&rotation=0&showTitle=false&size=253198&status=done&style=none&taskId=uaf1a88f2-945d-4167-8e74-16f27432f68&title=&width=869.6)


### Harbor安装与使用

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651469660922-dda78912-b8f4-45a2-8087-7a64f83ca79b.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=620&id=ud630ca4d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=775&originWidth=1191&originalType=binary&ratio=1&rotation=0&showTitle=false&size=299105&status=done&style=none&taskId=ue22f053e-d0d2-4c35-8be5-f76b64913c7&title=&width=952.8)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651469714618-856400dd-9518-4a0b-909f-ed6aeed0a008.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=442&id=u3621b2c3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=552&originWidth=871&originalType=binary&ratio=1&rotation=0&showTitle=false&size=80488&status=done&style=none&taskId=ub8718433-0521-4db3-9b88-5168d4cf782&title=&width=696.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651469840301-674a462b-af2a-4246-9fde-66f567df2753.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=476&id=u932f1095&margin=%5Bobject%20Object%5D&name=image.png&originHeight=595&originWidth=1152&originalType=binary&ratio=1&rotation=0&showTitle=false&size=101126&status=done&style=none&taskId=u452ae001-e2d3-46aa-a0fe-8eecebd5358&title=&width=921.6)

镜像上传

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651470007879-e9a12010-d773-4e17-98f5-58b555c171db.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=658&id=u54ebc68b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=823&originWidth=1226&originalType=binary&ratio=1&rotation=0&showTitle=false&size=320143&status=done&style=none&taskId=uf3124bf8-9d91-4dc4-8951-ffb859bc865&title=&width=980.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651470162124-81ec1036-409c-4b6a-aebc-2a3a23acc53c.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=452&id=u01117a4e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=565&originWidth=1193&originalType=binary&ratio=1&rotation=0&showTitle=false&size=333394&status=done&style=none&taskId=u9261aaae-d589-413b-8460-04b2988ca84&title=&width=954.4)
再次重新推送即可

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651470199650-cc9eb655-147d-4f7a-8091-92a0981fab8f.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=580&id=u5c998b80&margin=%5Bobject%20Object%5D&name=image.png&originHeight=725&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=195837&status=done&style=none&taskId=u91636273-e94a-4426-8f48-0646684f381&title=&width=960)

### 项目代码上传到gitlab

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651470488515-b9f55daa-86b3-41d6-823f-0261f6baefc3.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=201&id=u2f5e0ece&margin=%5Bobject%20Object%5D&name=image.png&originHeight=251&originWidth=1301&originalType=binary&ratio=1&rotation=0&showTitle=false&size=87256&status=done&style=none&taskId=u1944c83d-2ae9-4340-a4c5-bfb65e0c3f6&title=&width=1040.8)

### 从gitlab拉取项目源码

---

- 流水线

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651470567037-3bba0972-ee15-4fd2-9cc7-2b1533b7fdaf.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=593&id=u6c54b2c6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=741&originWidth=1000&originalType=binary&ratio=1&rotation=0&showTitle=false&size=216920&status=done&style=none&taskId=u6b71a60d-6a58-4dd8-8b31-401bd217639&title=&width=800)

- jenkinsfile

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651470692911-904ce310-e4c6-458a-8cc9-4d7caeacf2ed.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=344&id=u914514ba&margin=%5Bobject%20Object%5D&name=image.png&originHeight=430&originWidth=1458&originalType=binary&ratio=1&rotation=0&showTitle=false&size=204279&status=done&style=none&taskId=ud2f7d15b-cd39-4672-8aeb-1a3ec0fe1f8&title=&width=1166.4)

- 构建项目

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651470720269-e11de8f9-8f49-4859-afb1-a1da2ae72460.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=270&id=ua26d88fa&margin=%5Bobject%20Object%5D&name=image.png&originHeight=337&originWidth=1148&originalType=binary&ratio=1&rotation=0&showTitle=false&size=84288&status=done&style=none&taskId=u37c0ed71-5038-4018-bde3-53db0630fc4&title=&width=918.4)

### 提交到SonarQube代码审查

---

- sonar-project.properties

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651470790866-3f53fc10-421a-4a2e-9c44-c167c20596c1.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=580&id=ud6981583&margin=%5Bobject%20Object%5D&name=image.png&originHeight=725&originWidth=1187&originalType=binary&ratio=1&rotation=0&showTitle=false&size=535186&status=done&style=none&taskId=u73fdb5d4-ef4a-45a5-a00b-844942bad35&title=&width=949.6)

- jenkinsfile

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651470819088-7c353a21-ffa4-4290-83f5-e11e33c04f36.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=675&id=u032615ce&margin=%5Bobject%20Object%5D&name=image.png&originHeight=844&originWidth=1180&originalType=binary&ratio=1&rotation=0&showTitle=false&size=504313&status=done&style=none&taskId=u0a03841d-d4be-437c-976b-f9656fcdf45&title=&width=944)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651470990677-5aaa9931-47cf-4d6d-a697-d0075b05bb7f.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=424&id=u8b1c322a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=530&originWidth=1036&originalType=binary&ratio=1&rotation=0&showTitle=false&size=230191&status=done&style=none&taskId=u6d2c636e-26ed-4565-9ecf-f49ad85a71f&title=&width=828.8)


### 使用DockerFile编译，生成镜像

---

- 打包

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651471328681-6e7e79bc-8c36-462f-8fb6-e94e4caa93ab.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=586&id=uc0345c00&margin=%5Bobject%20Object%5D&name=image.png&originHeight=732&originWidth=917&originalType=binary&ratio=1&rotation=0&showTitle=false&size=331233&status=done&style=none&taskId=u9a1d4f4a-831d-4a97-9fc6-0f4cf213dee&title=&width=733.6)

- 镜像

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651471539816-5ca4ab72-77a1-46c9-a15b-aba20cc3666f.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=671&id=ua894b1db&margin=%5Bobject%20Object%5D&name=image.png&originHeight=839&originWidth=1186&originalType=binary&ratio=1&rotation=0&showTitle=false&size=474426&status=done&style=none&taskId=uf0a4715b-8d3d-4b3c-85f9-6209a554a6c&title=&width=948.8)

- jenkinsfile触发

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651471769118-f15ff22b-231f-41f6-81f1-d1b02c4f0f53.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=203&id=uc0723aa7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=254&originWidth=1085&originalType=binary&ratio=1&rotation=0&showTitle=false&size=123815&status=done&style=none&taskId=u495c25c4-292a-47eb-9407-6c93549c8ca&title=&width=868)

### 上传到Harbor镜像仓库

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651472102138-149f6af0-92c5-4684-9d77-93195e1bd4a0.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=522&id=u43a9a110&margin=%5Bobject%20Object%5D&name=image.png&originHeight=653&originWidth=1290&originalType=binary&ratio=1&rotation=0&showTitle=false&size=376509&status=done&style=none&taskId=u659e9d24-5157-4139-aae2-f77c2ad8468&title=&width=1032)


### 拉取镜像和发布应用

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651472310304-78fae0b1-a660-45b2-92d2-5f4c8d735d11.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=94&id=u54633b5d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=117&originWidth=1120&originalType=binary&ratio=1&rotation=0&showTitle=false&size=62861&status=done&style=none&taskId=u31b5cb51-c28a-4abd-8d27-0fedb105275&title=&width=896)




### 部署前端镜像网站

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651472444721-e142dc76-fb6a-42a0-9504-374b9191d3ad.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=239&id=u591eb94c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=299&originWidth=860&originalType=binary&ratio=1&rotation=0&showTitle=false&size=191944&status=done&style=none&taskId=u952fd40b-c73d-4765-a2f7-28d52d3a5c3&title=&width=688)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651472456184-f15f0847-ab67-41e7-99c6-4fc757778cb9.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=729&id=u52ee1bf2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=911&originWidth=986&originalType=binary&ratio=1&rotation=0&showTitle=false&size=286615&status=done&style=none&taskId=u26139795-9a57-4a49-8430-77e2bd0028b&title=&width=788.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651472540839-99fb5d36-365f-4896-a23a-d0d0f11ec67f.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=610&id=u254fc81d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=762&originWidth=1156&originalType=binary&ratio=1&rotation=0&showTitle=false&size=219292&status=done&style=none&taskId=uce90d7f3-e6a3-48eb-af90-247faf1177d&title=&width=924.8)
传到nginx里面的html里面

## Jenkins + Docker + springcloud 集群版

---


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651472870638-a8119041-cdd7-49af-a4f7-201e292bbd5e.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=478&id=u199a1dc0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=597&originWidth=1145&originalType=binary&ratio=1&rotation=0&showTitle=false&size=446428&status=done&style=none&taskId=u7c0fdf7e-e7a1-4020-b0f6-21bd7f8e64d&title=&width=916)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651473020527-3a39e4f2-db43-40ed-95d4-e3ca07613747.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=250&id=u47a91a93&margin=%5Bobject%20Object%5D&name=image.png&originHeight=312&originWidth=1141&originalType=binary&ratio=1&rotation=0&showTitle=false&size=148012&status=done&style=none&taskId=ubf127922-768c-4dda-8bb9-9b34d5489d4&title=&width=912.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651473056418-5eaef37d-242b-4dde-afe0-64e297967361.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=346&id=u446059a8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=432&originWidth=783&originalType=binary&ratio=1&rotation=0&showTitle=false&size=222461&status=done&style=none&taskId=u75bb3c57-c601-4a70-a327-999082fc6d1&title=&width=626.4)


## K8s + jenkins 

---


jenkins主从开发

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651473165319-fb2d87ce-ab66-4aca-985a-50feb71f957c.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=626&id=ua5ad47bc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=783&originWidth=1219&originalType=binary&ratio=1&rotation=0&showTitle=false&size=259109&status=done&style=none&taskId=u69bdfaa5-4b7b-421e-ae80-d2eb5638409&title=&width=975.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651473294325-1beec5cc-f99b-4153-8b08-413d38d2c610.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=298&id=u4cf3ef17&margin=%5Bobject%20Object%5D&name=image.png&originHeight=372&originWidth=1222&originalType=binary&ratio=1&rotation=0&showTitle=false&size=296124&status=done&style=none&taskId=uaecb490d-f552-4f4f-a290-7d2561be9c0&title=&width=977.6)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651473321884-fcbf708e-83fa-4da5-b768-102f722e3583.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=697&id=ufd0451a0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=871&originWidth=1219&originalType=binary&ratio=1&rotation=0&showTitle=false&size=424700&status=done&style=none&taskId=ue958d459-a632-448f-ae5e-51693847d9d&title=&width=975.2)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651473366558-7c9a4c95-ba69-4f25-ac0c-431671babfc2.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=428&id=ua53eb442&margin=%5Bobject%20Object%5D&name=image.png&originHeight=535&originWidth=1197&originalType=binary&ratio=1&rotation=0&showTitle=false&size=122630&status=done&style=none&taskId=u4458ae53-1423-4955-8e79-09d28f807fc&title=&width=957.6)


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651473513718-3e1a31f2-b536-4821-8bbe-66d80b3e2ad6.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=606&id=ubc474e1f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=758&originWidth=1224&originalType=binary&ratio=1&rotation=0&showTitle=false&size=250062&status=done&style=none&taskId=u0bd22763-b942-4be0-954d-f1a9b8f528b&title=&width=979.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651473531234-6712120e-4603-4547-9258-3c8da0bab115.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=136&id=u6665c688&margin=%5Bobject%20Object%5D&name=image.png&originHeight=170&originWidth=1129&originalType=binary&ratio=1&rotation=0&showTitle=false&size=35703&status=done&style=none&taskId=ud7881ad8-baea-4ac1-8a90-6d03257b45b&title=&width=903.2)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651473808724-4c994374-c4a0-4dbc-a08e-07eb867b859f.png#clientId=ua0e25056-4158-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=570&id=ufc25f4b1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=713&originWidth=1054&originalType=binary&ratio=1&rotation=0&showTitle=false&size=410025&status=done&style=none&taskId=ua5e5eec1-9596-4191-9688-65f40de42e1&title=&width=843.2)








